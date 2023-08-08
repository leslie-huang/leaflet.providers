
<!-- README.md is generated from README.Rmd. Please edit that file -->

# leaflet.providers

<!-- badges: start -->

[![CRAN
status](https://www.r-pkg.org/badges/version/leaflet.providers)](https://CRAN.R-project.org/package=leaflet.providers)
[![R-CMD-check](https://github.com/rstudio/leaflet.providers/actions/workflows/R-CMD-check.yaml/badge.svg)](https://github.com/rstudio/leaflet.providers/actions)
[![Codecov test
coverage](https://codecov.io/gh/rstudio/leaflet.providers/branch/main/graph/badge.svg)](https://app.codecov.io/gh/rstudio/leaflet.providers?branch=main)

<!-- badges: end -->

The goal of `leaflet.providers` is to provide regularly updated data on
the third-party tile providers supported by `leaflet`. The data is
extracted from
[leaflet-providers.js](https://github.com/leaflet-extras/leaflet-providers).

While `leaflet.providers` will be regularly released with updated
providers data, the package comes with functions `use_providers()` and
`get_providers()`, which enable users to fetch up-to-date providers
information directly from
[leaflet-providers.js](https://github.com/leaflet-extras/leaflet-providers)
between package updates and to load this providers data in `leaflet`.
Users may also fetch older versions of the providers data with the
`leaflet-providers.js` version number.

## Installation

You can install the released version of `leaflet.providers` from
[CRAN](https://CRAN.R-project.org):

``` r
# CRAN version
install.packages("leaflet.providers")
```

And the development version from [GitHub](https://github.com/) with:

``` r
pak::pak("rstudio/leaflet.providers")
```

## Example

The following are basic example of the default providers data that comes
`leaflet.providers` as well as the available methods to fetch and load
custom providers.

### Default providers

``` r
library(leaflet.providers)

str(providers_default(), max.level = 2)
```

<div style="height:150px; overflow-y: scroll;">

    #> List of 4
    #>  $ version_num      : chr "1.13.0"
    #>  $ providers        :List of 231
    #>   ..$ OpenStreetMap                         : chr "OpenStreetMap"
    #>   ..$ OpenStreetMap.Mapnik                  : chr "OpenStreetMap.Mapnik"
    #>   ..$ OpenStreetMap.DE                      : chr "OpenStreetMap.DE"
    #>   ..$ OpenStreetMap.CH                      : chr "OpenStreetMap.CH"
    #>   ..$ OpenStreetMap.France                  : chr "OpenStreetMap.France"
    #>   ..$ OpenStreetMap.HOT                     : chr "OpenStreetMap.HOT"
    #>   ..$ OpenStreetMap.BZH                     : chr "OpenStreetMap.BZH"
    #>   ..$ OpenSeaMap                            : chr "OpenSeaMap"
    #>   ..$ OPNVKarte                             : chr "OPNVKarte"
    #>   ..$ OpenTopoMap                           : chr "OpenTopoMap"
    #>   ..$ OpenRailwayMap                        : chr "OpenRailwayMap"
    #>   ..$ OpenFireMap                           : chr "OpenFireMap"
    #>   ..$ SafeCast                              : chr "SafeCast"
    #>   ..$ Stadia                                : chr "Stadia"
    #>   ..$ Stadia.AlidadeSmooth                  : chr "Stadia.AlidadeSmooth"
    #>   ..$ Stadia.AlidadeSmoothDark              : chr "Stadia.AlidadeSmoothDark"
    #>   ..$ Stadia.OSMBright                      : chr "Stadia.OSMBright"
    #>   ..$ Stadia.Outdoors                       : chr "Stadia.Outdoors"
    #>   ..$ Thunderforest                         : chr "Thunderforest"
    #>   ..$ Thunderforest.OpenCycleMap            : chr "Thunderforest.OpenCycleMap"
    #>   ..$ Thunderforest.Transport               : chr "Thunderforest.Transport"
    #>   ..$ Thunderforest.TransportDark           : chr "Thunderforest.TransportDark"
    #>   ..$ Thunderforest.SpinalMap               : chr "Thunderforest.SpinalMap"
    #>   ..$ Thunderforest.Landscape               : chr "Thunderforest.Landscape"
    #>   ..$ Thunderforest.Outdoors                : chr "Thunderforest.Outdoors"
    #>   ..$ Thunderforest.Pioneer                 : chr "Thunderforest.Pioneer"
    #>   ..$ Thunderforest.MobileAtlas             : chr "Thunderforest.MobileAtlas"
    #>   ..$ Thunderforest.Neighbourhood           : chr "Thunderforest.Neighbourhood"
    #>   ..$ CyclOSM                               : chr "CyclOSM"
    #>   ..$ Hydda                                 : chr "Hydda"
    #>   ..$ Hydda.Full                            : chr "Hydda.Full"
    #>   ..$ Hydda.Base                            : chr "Hydda.Base"
    #>   ..$ Hydda.RoadsAndLabels                  : chr "Hydda.RoadsAndLabels"
    #>   ..$ Jawg                                  : chr "Jawg"
    #>   ..$ Jawg.Streets                          : chr "Jawg.Streets"
    #>   ..$ Jawg.Terrain                          : chr "Jawg.Terrain"
    #>   ..$ Jawg.Sunny                            : chr "Jawg.Sunny"
    #>   ..$ Jawg.Dark                             : chr "Jawg.Dark"
    #>   ..$ Jawg.Light                            : chr "Jawg.Light"
    #>   ..$ Jawg.Matrix                           : chr "Jawg.Matrix"
    #>   ..$ MapBox                                : chr "MapBox"
    #>   ..$ MapTiler                              : chr "MapTiler"
    #>   ..$ MapTiler.Streets                      : chr "MapTiler.Streets"
    #>   ..$ MapTiler.Basic                        : chr "MapTiler.Basic"
    #>   ..$ MapTiler.Bright                       : chr "MapTiler.Bright"
    #>   ..$ MapTiler.Pastel                       : chr "MapTiler.Pastel"
    #>   ..$ MapTiler.Positron                     : chr "MapTiler.Positron"
    #>   ..$ MapTiler.Hybrid                       : chr "MapTiler.Hybrid"
    #>   ..$ MapTiler.Toner                        : chr "MapTiler.Toner"
    #>   ..$ MapTiler.Topo                         : chr "MapTiler.Topo"
    #>   ..$ MapTiler.Voyager                      : chr "MapTiler.Voyager"
    #>   ..$ Stamen                                : chr "Stamen"
    #>   ..$ Stamen.Toner                          : chr "Stamen.Toner"
    #>   ..$ Stamen.TonerBackground                : chr "Stamen.TonerBackground"
    #>   ..$ Stamen.TonerHybrid                    : chr "Stamen.TonerHybrid"
    #>   ..$ Stamen.TonerLines                     : chr "Stamen.TonerLines"
    #>   ..$ Stamen.TonerLabels                    : chr "Stamen.TonerLabels"
    #>   ..$ Stamen.TonerLite                      : chr "Stamen.TonerLite"
    #>   ..$ Stamen.Watercolor                     : chr "Stamen.Watercolor"
    #>   ..$ Stamen.Terrain                        : chr "Stamen.Terrain"
    #>   ..$ Stamen.TerrainBackground              : chr "Stamen.TerrainBackground"
    #>   ..$ Stamen.TerrainLabels                  : chr "Stamen.TerrainLabels"
    #>   ..$ Stamen.TopOSMRelief                   : chr "Stamen.TopOSMRelief"
    #>   ..$ Stamen.TopOSMFeatures                 : chr "Stamen.TopOSMFeatures"
    #>   ..$ TomTom                                : chr "TomTom"
    #>   ..$ TomTom.Basic                          : chr "TomTom.Basic"
    #>   ..$ TomTom.Hybrid                         : chr "TomTom.Hybrid"
    #>   ..$ TomTom.Labels                         : chr "TomTom.Labels"
    #>   ..$ Esri                                  : chr "Esri"
    #>   ..$ Esri.WorldStreetMap                   : chr "Esri.WorldStreetMap"
    #>   ..$ Esri.DeLorme                          : chr "Esri.DeLorme"
    #>   ..$ Esri.WorldTopoMap                     : chr "Esri.WorldTopoMap"
    #>   ..$ Esri.WorldImagery                     : chr "Esri.WorldImagery"
    #>   ..$ Esri.WorldTerrain                     : chr "Esri.WorldTerrain"
    #>   ..$ Esri.WorldShadedRelief                : chr "Esri.WorldShadedRelief"
    #>   ..$ Esri.WorldPhysical                    : chr "Esri.WorldPhysical"
    #>   ..$ Esri.OceanBasemap                     : chr "Esri.OceanBasemap"
    #>   ..$ Esri.NatGeoWorldMap                   : chr "Esri.NatGeoWorldMap"
    #>   ..$ Esri.WorldGrayCanvas                  : chr "Esri.WorldGrayCanvas"
    #>   ..$ OpenWeatherMap                        : chr "OpenWeatherMap"
    #>   ..$ OpenWeatherMap.Clouds                 : chr "OpenWeatherMap.Clouds"
    #>   ..$ OpenWeatherMap.CloudsClassic          : chr "OpenWeatherMap.CloudsClassic"
    #>   ..$ OpenWeatherMap.Precipitation          : chr "OpenWeatherMap.Precipitation"
    #>   ..$ OpenWeatherMap.PrecipitationClassic   : chr "OpenWeatherMap.PrecipitationClassic"
    #>   ..$ OpenWeatherMap.Rain                   : chr "OpenWeatherMap.Rain"
    #>   ..$ OpenWeatherMap.RainClassic            : chr "OpenWeatherMap.RainClassic"
    #>   ..$ OpenWeatherMap.Pressure               : chr "OpenWeatherMap.Pressure"
    #>   ..$ OpenWeatherMap.PressureContour        : chr "OpenWeatherMap.PressureContour"
    #>   ..$ OpenWeatherMap.Wind                   : chr "OpenWeatherMap.Wind"
    #>   ..$ OpenWeatherMap.Temperature            : chr "OpenWeatherMap.Temperature"
    #>   ..$ OpenWeatherMap.Snow                   : chr "OpenWeatherMap.Snow"
    #>   ..$ HERE                                  : chr "HERE"
    #>   ..$ HERE.normalDay                        : chr "HERE.normalDay"
    #>   ..$ HERE.normalDayCustom                  : chr "HERE.normalDayCustom"
    #>   ..$ HERE.normalDayGrey                    : chr "HERE.normalDayGrey"
    #>   ..$ HERE.normalDayMobile                  : chr "HERE.normalDayMobile"
    #>   ..$ HERE.normalDayGreyMobile              : chr "HERE.normalDayGreyMobile"
    #>   ..$ HERE.normalDayTransit                 : chr "HERE.normalDayTransit"
    #>   ..$ HERE.normalDayTransitMobile           : chr "HERE.normalDayTransitMobile"
    #>   .. [list output truncated]
    #>  $ providers_details:List of 36
    #>   ..$ OpenStreetMap   :List of 3
    #>   ..$ OpenSeaMap      :List of 2
    #>   ..$ OPNVKarte       :List of 2
    #>   ..$ OpenTopoMap     :List of 2
    #>   ..$ OpenRailwayMap  :List of 2
    #>   ..$ OpenFireMap     :List of 2
    #>   ..$ SafeCast        :List of 2
    #>   ..$ Stadia          :List of 3
    #>   ..$ Thunderforest   :List of 3
    #>   ..$ CyclOSM         :List of 2
    #>   ..$ Hydda           :List of 3
    #>   ..$ Jawg            :List of 3
    #>   ..$ MapBox          :List of 2
    #>   ..$ MapTiler        :List of 3
    #>   ..$ Stamen          :List of 3
    #>   ..$ TomTom          :List of 3
    #>   ..$ Esri            :List of 3
    #>   ..$ OpenWeatherMap  :List of 3
    #>   ..$ HERE            :List of 3
    #>   ..$ HEREv3          :List of 3
    #>   ..$ FreeMapSK       :List of 2
    #>   ..$ MtbMap          :List of 2
    #>   ..$ CartoDB         :List of 3
    #>   ..$ HikeBike        :List of 3
    #>   ..$ BasemapAT       :List of 3
    #>   ..$ nlmaps          :List of 3
    #>   ..$ NASAGIBS        :List of 3
    #>   ..$ NLS             :List of 2
    #>   ..$ JusticeMap      :List of 3
    #>   ..$ GeoportailFrance:List of 3
    #>   ..$ OneMapSG        :List of 3
    #>   ..$ USGS            :List of 3
    #>   ..$ WaymarkedTrails :List of 3
    #>   ..$ OpenAIP         :List of 2
    #>   ..$ OpenSnowMap     :List of 3
    #>   ..$ AzureMaps       :List of 3
    #>  $ src              : chr "(function (root, factory) {\n\tif (typeof define === 'function' && define.amd) {\n\t\t// AMD. Register as an an"| __truncated__
    #>  - attr(*, "class")= chr "leaflet_providers"

</div>

### Fetch custom providers

Users may use a specific version number of `leaflet-providers.js` by
passing the version number to `use_providers()`.

``` r
# Retrieve v 1.7.0
providers_170 <- get_providers("1.7.0")

# Load custom providers data
use_providers(providers_170)
# shorthand method
use_providers("1.7.0")

# Reset loaded providers to default providers
use_providers()
```

Now that `use_providers()` has been called with a custom
`leaflet.providers` object obtained via `get_providers()` (in this case,
a previous version of the data),
[`leaflet`](https://rstudio.github.io/leaflet/) will use the custom
providers instead of the default provider data.

> Note that the package `V8` is required for `get_providers()`.

### View the loaded providers data

#### The version number of the source leaflet-providers.js

``` r
providers_loaded()$version_num
#> [1] "1.13.0"
```

#### Supported tile providers

``` r
names(providers_loaded()$providers)
```

<div style="height:150px; overflow-y: scroll;">

    #>   [1] "OpenStreetMap"                         
    #>   [2] "OpenStreetMap.Mapnik"                  
    #>   [3] "OpenStreetMap.DE"                      
    #>   [4] "OpenStreetMap.CH"                      
    #>   [5] "OpenStreetMap.France"                  
    #>   [6] "OpenStreetMap.HOT"                     
    #>   [7] "OpenStreetMap.BZH"                     
    #>   [8] "OpenSeaMap"                            
    #>   [9] "OPNVKarte"                             
    #>  [10] "OpenTopoMap"                           
    #>  [11] "OpenRailwayMap"                        
    #>  [12] "OpenFireMap"                           
    #>  [13] "SafeCast"                              
    #>  [14] "Stadia"                                
    #>  [15] "Stadia.AlidadeSmooth"                  
    #>  [16] "Stadia.AlidadeSmoothDark"              
    #>  [17] "Stadia.OSMBright"                      
    #>  [18] "Stadia.Outdoors"                       
    #>  [19] "Thunderforest"                         
    #>  [20] "Thunderforest.OpenCycleMap"            
    #>  [21] "Thunderforest.Transport"               
    #>  [22] "Thunderforest.TransportDark"           
    #>  [23] "Thunderforest.SpinalMap"               
    #>  [24] "Thunderforest.Landscape"               
    #>  [25] "Thunderforest.Outdoors"                
    #>  [26] "Thunderforest.Pioneer"                 
    #>  [27] "Thunderforest.MobileAtlas"             
    #>  [28] "Thunderforest.Neighbourhood"           
    #>  [29] "CyclOSM"                               
    #>  [30] "Hydda"                                 
    #>  [31] "Hydda.Full"                            
    #>  [32] "Hydda.Base"                            
    #>  [33] "Hydda.RoadsAndLabels"                  
    #>  [34] "Jawg"                                  
    #>  [35] "Jawg.Streets"                          
    #>  [36] "Jawg.Terrain"                          
    #>  [37] "Jawg.Sunny"                            
    #>  [38] "Jawg.Dark"                             
    #>  [39] "Jawg.Light"                            
    #>  [40] "Jawg.Matrix"                           
    #>  [41] "MapBox"                                
    #>  [42] "MapTiler"                              
    #>  [43] "MapTiler.Streets"                      
    #>  [44] "MapTiler.Basic"                        
    #>  [45] "MapTiler.Bright"                       
    #>  [46] "MapTiler.Pastel"                       
    #>  [47] "MapTiler.Positron"                     
    #>  [48] "MapTiler.Hybrid"                       
    #>  [49] "MapTiler.Toner"                        
    #>  [50] "MapTiler.Topo"                         
    #>  [51] "MapTiler.Voyager"                      
    #>  [52] "Stamen"                                
    #>  [53] "Stamen.Toner"                          
    #>  [54] "Stamen.TonerBackground"                
    #>  [55] "Stamen.TonerHybrid"                    
    #>  [56] "Stamen.TonerLines"                     
    #>  [57] "Stamen.TonerLabels"                    
    #>  [58] "Stamen.TonerLite"                      
    #>  [59] "Stamen.Watercolor"                     
    #>  [60] "Stamen.Terrain"                        
    #>  [61] "Stamen.TerrainBackground"              
    #>  [62] "Stamen.TerrainLabels"                  
    #>  [63] "Stamen.TopOSMRelief"                   
    #>  [64] "Stamen.TopOSMFeatures"                 
    #>  [65] "TomTom"                                
    #>  [66] "TomTom.Basic"                          
    #>  [67] "TomTom.Hybrid"                         
    #>  [68] "TomTom.Labels"                         
    #>  [69] "Esri"                                  
    #>  [70] "Esri.WorldStreetMap"                   
    #>  [71] "Esri.DeLorme"                          
    #>  [72] "Esri.WorldTopoMap"                     
    #>  [73] "Esri.WorldImagery"                     
    #>  [74] "Esri.WorldTerrain"                     
    #>  [75] "Esri.WorldShadedRelief"                
    #>  [76] "Esri.WorldPhysical"                    
    #>  [77] "Esri.OceanBasemap"                     
    #>  [78] "Esri.NatGeoWorldMap"                   
    #>  [79] "Esri.WorldGrayCanvas"                  
    #>  [80] "OpenWeatherMap"                        
    #>  [81] "OpenWeatherMap.Clouds"                 
    #>  [82] "OpenWeatherMap.CloudsClassic"          
    #>  [83] "OpenWeatherMap.Precipitation"          
    #>  [84] "OpenWeatherMap.PrecipitationClassic"   
    #>  [85] "OpenWeatherMap.Rain"                   
    #>  [86] "OpenWeatherMap.RainClassic"            
    #>  [87] "OpenWeatherMap.Pressure"               
    #>  [88] "OpenWeatherMap.PressureContour"        
    #>  [89] "OpenWeatherMap.Wind"                   
    #>  [90] "OpenWeatherMap.Temperature"            
    #>  [91] "OpenWeatherMap.Snow"                   
    #>  [92] "HERE"                                  
    #>  [93] "HERE.normalDay"                        
    #>  [94] "HERE.normalDayCustom"                  
    #>  [95] "HERE.normalDayGrey"                    
    #>  [96] "HERE.normalDayMobile"                  
    #>  [97] "HERE.normalDayGreyMobile"              
    #>  [98] "HERE.normalDayTransit"                 
    #>  [99] "HERE.normalDayTransitMobile"           
    #> [100] "HERE.normalDayTraffic"                 
    #> [101] "HERE.normalNight"                      
    #> [102] "HERE.normalNightMobile"                
    #> [103] "HERE.normalNightGrey"                  
    #> [104] "HERE.normalNightGreyMobile"            
    #> [105] "HERE.normalNightTransit"               
    #> [106] "HERE.normalNightTransitMobile"         
    #> [107] "HERE.reducedDay"                       
    #> [108] "HERE.reducedNight"                     
    #> [109] "HERE.basicMap"                         
    #> [110] "HERE.mapLabels"                        
    #> [111] "HERE.trafficFlow"                      
    #> [112] "HERE.carnavDayGrey"                    
    #> [113] "HERE.hybridDay"                        
    #> [114] "HERE.hybridDayMobile"                  
    #> [115] "HERE.hybridDayTransit"                 
    #> [116] "HERE.hybridDayGrey"                    
    #> [117] "HERE.hybridDayTraffic"                 
    #> [118] "HERE.pedestrianDay"                    
    #> [119] "HERE.pedestrianNight"                  
    #> [120] "HERE.satelliteDay"                     
    #> [121] "HERE.terrainDay"                       
    #> [122] "HERE.terrainDayMobile"                 
    #> [123] "HEREv3"                                
    #> [124] "HEREv3.normalDay"                      
    #> [125] "HEREv3.normalDayCustom"                
    #> [126] "HEREv3.normalDayGrey"                  
    #> [127] "HEREv3.normalDayMobile"                
    #> [128] "HEREv3.normalDayGreyMobile"            
    #> [129] "HEREv3.normalDayTransit"               
    #> [130] "HEREv3.normalDayTransitMobile"         
    #> [131] "HEREv3.normalNight"                    
    #> [132] "HEREv3.normalNightMobile"              
    #> [133] "HEREv3.normalNightGrey"                
    #> [134] "HEREv3.normalNightGreyMobile"          
    #> [135] "HEREv3.normalNightTransit"             
    #> [136] "HEREv3.normalNightTransitMobile"       
    #> [137] "HEREv3.reducedDay"                     
    #> [138] "HEREv3.reducedNight"                   
    #> [139] "HEREv3.basicMap"                       
    #> [140] "HEREv3.mapLabels"                      
    #> [141] "HEREv3.trafficFlow"                    
    #> [142] "HEREv3.carnavDayGrey"                  
    #> [143] "HEREv3.hybridDay"                      
    #> [144] "HEREv3.hybridDayMobile"                
    #> [145] "HEREv3.hybridDayTransit"               
    #> [146] "HEREv3.hybridDayGrey"                  
    #> [147] "HEREv3.pedestrianDay"                  
    #> [148] "HEREv3.pedestrianNight"                
    #> [149] "HEREv3.satelliteDay"                   
    #> [150] "HEREv3.terrainDay"                     
    #> [151] "HEREv3.terrainDayMobile"               
    #> [152] "FreeMapSK"                             
    #> [153] "MtbMap"                                
    #> [154] "CartoDB"                               
    #> [155] "CartoDB.Positron"                      
    #> [156] "CartoDB.PositronNoLabels"              
    #> [157] "CartoDB.PositronOnlyLabels"            
    #> [158] "CartoDB.DarkMatter"                    
    #> [159] "CartoDB.DarkMatterNoLabels"            
    #> [160] "CartoDB.DarkMatterOnlyLabels"          
    #> [161] "CartoDB.Voyager"                       
    #> [162] "CartoDB.VoyagerNoLabels"               
    #> [163] "CartoDB.VoyagerOnlyLabels"             
    #> [164] "CartoDB.VoyagerLabelsUnder"            
    #> [165] "HikeBike"                              
    #> [166] "HikeBike.HikeBike"                     
    #> [167] "HikeBike.HillShading"                  
    #> [168] "BasemapAT"                             
    #> [169] "BasemapAT.basemap"                     
    #> [170] "BasemapAT.grau"                        
    #> [171] "BasemapAT.overlay"                     
    #> [172] "BasemapAT.terrain"                     
    #> [173] "BasemapAT.surface"                     
    #> [174] "BasemapAT.highdpi"                     
    #> [175] "BasemapAT.orthofoto"                   
    #> [176] "nlmaps"                                
    #> [177] "nlmaps.standaard"                      
    #> [178] "nlmaps.pastel"                         
    #> [179] "nlmaps.grijs"                          
    #> [180] "nlmaps.luchtfoto"                      
    #> [181] "NASAGIBS"                              
    #> [182] "NASAGIBS.ModisTerraTrueColorCR"        
    #> [183] "NASAGIBS.ModisTerraBands367CR"         
    #> [184] "NASAGIBS.ViirsEarthAtNight2012"        
    #> [185] "NASAGIBS.ModisTerraLSTDay"             
    #> [186] "NASAGIBS.ModisTerraSnowCover"          
    #> [187] "NASAGIBS.ModisTerraAOD"                
    #> [188] "NASAGIBS.ModisTerraChlorophyll"        
    #> [189] "NLS"                                   
    #> [190] "JusticeMap"                            
    #> [191] "JusticeMap.income"                     
    #> [192] "JusticeMap.americanIndian"             
    #> [193] "JusticeMap.asian"                      
    #> [194] "JusticeMap.black"                      
    #> [195] "JusticeMap.hispanic"                   
    #> [196] "JusticeMap.multi"                      
    #> [197] "JusticeMap.nonWhite"                   
    #> [198] "JusticeMap.white"                      
    #> [199] "JusticeMap.plurality"                  
    #> [200] "GeoportailFrance"                      
    #> [201] "GeoportailFrance.plan"                 
    #> [202] "GeoportailFrance.parcels"              
    #> [203] "GeoportailFrance.orthos"               
    #> [204] "OneMapSG"                              
    #> [205] "OneMapSG.Default"                      
    #> [206] "OneMapSG.Night"                        
    #> [207] "OneMapSG.Original"                     
    #> [208] "OneMapSG.Grey"                         
    #> [209] "OneMapSG.LandLot"                      
    #> [210] "USGS"                                  
    #> [211] "USGS.USTopo"                           
    #> [212] "USGS.USImagery"                        
    #> [213] "USGS.USImageryTopo"                    
    #> [214] "WaymarkedTrails"                       
    #> [215] "WaymarkedTrails.hiking"                
    #> [216] "WaymarkedTrails.cycling"               
    #> [217] "WaymarkedTrails.mtb"                   
    #> [218] "WaymarkedTrails.slopes"                
    #> [219] "WaymarkedTrails.riding"                
    #> [220] "WaymarkedTrails.skating"               
    #> [221] "OpenAIP"                               
    #> [222] "OpenSnowMap"                           
    #> [223] "OpenSnowMap.pistes"                    
    #> [224] "AzureMaps"                             
    #> [225] "AzureMaps.MicrosoftImagery"            
    #> [226] "AzureMaps.MicrosoftBaseDarkGrey"       
    #> [227] "AzureMaps.MicrosoftBaseRoad"           
    #> [228] "AzureMaps.MicrosoftBaseHybridRoad"     
    #> [229] "AzureMaps.MicrosoftTerraMain"          
    #> [230] "AzureMaps.MicrosoftWeatherInfraredMain"
    #> [231] "AzureMaps.MicrosoftWeatherRadarMain"

</div>

#### Tile providers’ details

``` r
str(providers_loaded()$providers_details)
```

<div style="height:150px; overflow-y: scroll;">

    #> List of 36
    #>  $ OpenStreetMap   :List of 3
    #>   ..$ url     : chr "https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"
    #>   ..$ options :List of 2
    #>   .. ..$ maxZoom    : int 19
    #>   .. ..$ attribution: chr "&copy; <a href=\"https://www.openstreetmap.org/copyright\">OpenStreetMap</a> contributors"
    #>   ..$ variants:List of 6
    #>   .. ..$ Mapnik: Named list()
    #>   .. ..$ DE    :List of 2
    #>   .. .. ..$ url    : chr "https://{s}.tile.openstreetmap.de/tiles/osmde/{z}/{x}/{y}.png"
    #>   .. .. ..$ options:List of 1
    #>   .. .. .. ..$ maxZoom: int 18
    #>   .. ..$ CH    :List of 2
    #>   .. .. ..$ url    : chr "https://tile.osm.ch/switzerland/{z}/{x}/{y}.png"
    #>   .. .. ..$ options:List of 2
    #>   .. .. .. ..$ maxZoom: int 18
    #>   .. .. .. ..$ bounds : int [1:2, 1:2] 45 48 5 11
    #>   .. ..$ France:List of 2
    #>   .. .. ..$ url    : chr "https://{s}.tile.openstreetmap.fr/osmfr/{z}/{x}/{y}.png"
    #>   .. .. ..$ options:List of 2
    #>   .. .. .. ..$ maxZoom    : int 20
    #>   .. .. .. ..$ attribution: chr "&copy; OpenStreetMap France | {attribution.OpenStreetMap}"
    #>   .. ..$ HOT   :List of 2
    #>   .. .. ..$ url    : chr "https://{s}.tile.openstreetmap.fr/hot/{z}/{x}/{y}.png"
    #>   .. .. ..$ options:List of 1
    #>   .. .. .. ..$ attribution: chr "{attribution.OpenStreetMap}, Tiles style by <a href=\"https://www.hotosm.org/\" target=\"_blank\">Humanitarian "| __truncated__
    #>   .. ..$ BZH   :List of 2
    #>   .. .. ..$ url    : chr "https://tile.openstreetmap.bzh/br/{z}/{x}/{y}.png"
    #>   .. .. ..$ options:List of 2
    #>   .. .. .. ..$ attribution: chr "{attribution.OpenStreetMap}, Tiles courtesy of <a href=\"http://www.openstreetmap.bzh/\" target=\"_blank\">Bret"| __truncated__
    #>   .. .. .. ..$ bounds     : num [1:2, 1:2] 46.2 50 -5.5 0.7
    #>  $ OpenSeaMap      :List of 2
    #>   ..$ url    : chr "https://tiles.openseamap.org/seamark/{z}/{x}/{y}.png"
    #>   ..$ options:List of 1
    #>   .. ..$ attribution: chr "Map data: &copy; <a href=\"http://www.openseamap.org\">OpenSeaMap</a> contributors"
    #>  $ OPNVKarte       :List of 2
    #>   ..$ url    : chr "https://tileserver.memomaps.de/tilegen/{z}/{x}/{y}.png"
    #>   ..$ options:List of 2
    #>   .. ..$ maxZoom    : int 18
    #>   .. ..$ attribution: chr "Map <a href=\"https://memomaps.de/\">memomaps.de</a> <a href=\"http://creativecommons.org/licenses/by-sa/2.0/\""| __truncated__
    #>  $ OpenTopoMap     :List of 2
    #>   ..$ url    : chr "https://{s}.tile.opentopomap.org/{z}/{x}/{y}.png"
    #>   ..$ options:List of 2
    #>   .. ..$ maxZoom    : int 17
    #>   .. ..$ attribution: chr "Map data: {attribution.OpenStreetMap}, <a href=\"http://viewfinderpanoramas.org\">SRTM</a> | Map style: &copy; "| __truncated__
    #>  $ OpenRailwayMap  :List of 2
    #>   ..$ url    : chr "https://{s}.tiles.openrailwaymap.org/standard/{z}/{x}/{y}.png"
    #>   ..$ options:List of 2
    #>   .. ..$ maxZoom    : int 19
    #>   .. ..$ attribution: chr "Map data: {attribution.OpenStreetMap} | Map style: &copy; <a href=\"https://www.OpenRailwayMap.org\">OpenRailwa"| __truncated__
    #>  $ OpenFireMap     :List of 2
    #>   ..$ url    : chr "http://openfiremap.org/hytiles/{z}/{x}/{y}.png"
    #>   ..$ options:List of 2
    #>   .. ..$ maxZoom    : int 19
    #>   .. ..$ attribution: chr "Map data: {attribution.OpenStreetMap} | Map style: &copy; <a href=\"http://www.openfiremap.org\">OpenFireMap</a"| __truncated__
    #>  $ SafeCast        :List of 2
    #>   ..$ url    : chr "https://s3.amazonaws.com/te512.safecast.org/{z}/{x}/{y}.png"
    #>   ..$ options:List of 2
    #>   .. ..$ maxZoom    : int 16
    #>   .. ..$ attribution: chr "Map data: {attribution.OpenStreetMap} | Map style: &copy; <a href=\"https://blog.safecast.org/about/\">SafeCast"| __truncated__
    #>  $ Stadia          :List of 3
    #>   ..$ url     : chr "https://tiles.stadiamaps.com/tiles/alidade_smooth/{z}/{x}/{y}{r}.png"
    #>   ..$ options :List of 2
    #>   .. ..$ maxZoom    : int 20
    #>   .. ..$ attribution: chr "&copy; <a href=\"https://stadiamaps.com/\">Stadia Maps</a>, &copy; <a href=\"https://openmaptiles.org/\">OpenMa"| __truncated__
    #>   ..$ variants:List of 4
    #>   .. ..$ AlidadeSmooth    :List of 1
    #>   .. .. ..$ url: chr "https://tiles.stadiamaps.com/tiles/alidade_smooth/{z}/{x}/{y}{r}.png"
    #>   .. ..$ AlidadeSmoothDark:List of 1
    #>   .. .. ..$ url: chr "https://tiles.stadiamaps.com/tiles/alidade_smooth_dark/{z}/{x}/{y}{r}.png"
    #>   .. ..$ OSMBright        :List of 1
    #>   .. .. ..$ url: chr "https://tiles.stadiamaps.com/tiles/osm_bright/{z}/{x}/{y}{r}.png"
    #>   .. ..$ Outdoors         :List of 1
    #>   .. .. ..$ url: chr "https://tiles.stadiamaps.com/tiles/outdoors/{z}/{x}/{y}{r}.png"
    #>  $ Thunderforest   :List of 3
    #>   ..$ url     : chr "https://{s}.tile.thunderforest.com/{variant}/{z}/{x}/{y}.png?apikey={apikey}"
    #>   ..$ options :List of 4
    #>   .. ..$ attribution: chr "&copy; <a href=\"http://www.thunderforest.com/\">Thunderforest</a>, {attribution.OpenStreetMap}"
    #>   .. ..$ variant    : chr "cycle"
    #>   .. ..$ apikey     : chr "<insert your api key here>"
    #>   .. ..$ maxZoom    : int 22
    #>   ..$ variants:List of 9
    #>   .. ..$ OpenCycleMap : chr "cycle"
    #>   .. ..$ Transport    :List of 1
    #>   .. .. ..$ options:List of 1
    #>   .. .. .. ..$ variant: chr "transport"
    #>   .. ..$ TransportDark:List of 1
    #>   .. .. ..$ options:List of 1
    #>   .. .. .. ..$ variant: chr "transport-dark"
    #>   .. ..$ SpinalMap    :List of 1
    #>   .. .. ..$ options:List of 1
    #>   .. .. .. ..$ variant: chr "spinal-map"
    #>   .. ..$ Landscape    : chr "landscape"
    #>   .. ..$ Outdoors     : chr "outdoors"
    #>   .. ..$ Pioneer      : chr "pioneer"
    #>   .. ..$ MobileAtlas  : chr "mobile-atlas"
    #>   .. ..$ Neighbourhood: chr "neighbourhood"
    #>  $ CyclOSM         :List of 2
    #>   ..$ url    : chr "https://{s}.tile-cyclosm.openstreetmap.fr/cyclosm/{z}/{x}/{y}.png"
    #>   ..$ options:List of 2
    #>   .. ..$ maxZoom    : int 20
    #>   .. ..$ attribution: chr "<a href=\"https://github.com/cyclosm/cyclosm-cartocss-style/releases\" title=\"CyclOSM - Open Bicycle render\">"| __truncated__
    #>  $ Hydda           :List of 3
    #>   ..$ url     : chr "https://{s}.tile.openstreetmap.se/hydda/{variant}/{z}/{x}/{y}.png"
    #>   ..$ options :List of 3
    #>   .. ..$ maxZoom    : int 20
    #>   .. ..$ variant    : chr "full"
    #>   .. ..$ attribution: chr "Tiles courtesy of <a href=\"http://openstreetmap.se/\" target=\"_blank\">OpenStreetMap Sweden</a> &mdash; Map d"| __truncated__
    #>   ..$ variants:List of 3
    #>   .. ..$ Full          : chr "full"
    #>   .. ..$ Base          : chr "base"
    #>   .. ..$ RoadsAndLabels: chr "roads_and_labels"
    #>  $ Jawg            :List of 3
    #>   ..$ url     : chr "https://{s}.tile.jawg.io/{variant}/{z}/{x}/{y}{r}.png?access-token={accessToken}"
    #>   ..$ options :List of 6
    #>   .. ..$ attribution: chr "<a href=\"http://jawg.io\" title=\"Tiles Courtesy of Jawg Maps\" target=\"_blank\">&copy; <b>Jawg</b>Maps</a> {"| __truncated__
    #>   .. ..$ minZoom    : int 0
    #>   .. ..$ maxZoom    : int 22
    #>   .. ..$ subdomains : chr "abcd"
    #>   .. ..$ variant    : chr "jawg-terrain"
    #>   .. ..$ accessToken: chr "<insert your access token here>"
    #>   ..$ variants:List of 6
    #>   .. ..$ Streets: chr "jawg-streets"
    #>   .. ..$ Terrain: chr "jawg-terrain"
    #>   .. ..$ Sunny  : chr "jawg-sunny"
    #>   .. ..$ Dark   : chr "jawg-dark"
    #>   .. ..$ Light  : chr "jawg-light"
    #>   .. ..$ Matrix : chr "jawg-matrix"
    #>  $ MapBox          :List of 2
    #>   ..$ url    : chr "https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}{r}?access_token={accessToken}"
    #>   ..$ options:List of 6
    #>   .. ..$ attribution: chr "&copy; <a href=\"https://www.mapbox.com/about/maps/\" target=\"_blank\">Mapbox</a> {attribution.OpenStreetMap} "| __truncated__
    #>   .. ..$ tileSize   : int 512
    #>   .. ..$ maxZoom    : int 18
    #>   .. ..$ zoomOffset : int -1
    #>   .. ..$ id         : chr "mapbox/streets-v11"
    #>   .. ..$ accessToken: chr "<insert your access token here>"
    #>  $ MapTiler        :List of 3
    #>   ..$ url     : chr "https://api.maptiler.com/maps/{variant}/{z}/{x}/{y}{r}.{ext}?key={key}"
    #>   ..$ options :List of 8
    #>   .. ..$ attribution: chr "<a href=\"https://www.maptiler.com/copyright/\" target=\"_blank\">&copy; MapTiler</a> <a href=\"https://www.ope"| __truncated__
    #>   .. ..$ variant    : chr "streets"
    #>   .. ..$ ext        : chr "png"
    #>   .. ..$ key        : chr "<insert your MapTiler Cloud API key here>"
    #>   .. ..$ tileSize   : int 512
    #>   .. ..$ zoomOffset : int -1
    #>   .. ..$ minZoom    : int 0
    #>   .. ..$ maxZoom    : int 21
    #>   ..$ variants:List of 9
    #>   .. ..$ Streets : chr "streets"
    #>   .. ..$ Basic   : chr "basic"
    #>   .. ..$ Bright  : chr "bright"
    #>   .. ..$ Pastel  : chr "pastel"
    #>   .. ..$ Positron: chr "positron"
    #>   .. ..$ Hybrid  :List of 1
    #>   .. .. ..$ options:List of 2
    #>   .. .. .. ..$ variant: chr "hybrid"
    #>   .. .. .. ..$ ext    : chr "jpg"
    #>   .. ..$ Toner   : chr "toner"
    #>   .. ..$ Topo    : chr "topo"
    #>   .. ..$ Voyager : chr "voyager"
    #>  $ Stamen          :List of 3
    #>   ..$ url     : chr "https://stamen-tiles-{s}.a.ssl.fastly.net/{variant}/{z}/{x}/{y}{r}.{ext}"
    #>   ..$ options :List of 6
    #>   .. ..$ attribution: chr "Map tiles by <a href=\"http://stamen.com\">Stamen Design</a>, <a href=\"http://creativecommons.org/licenses/by/"| __truncated__
    #>   .. ..$ subdomains : chr "abcd"
    #>   .. ..$ minZoom    : int 0
    #>   .. ..$ maxZoom    : int 20
    #>   .. ..$ variant    : chr "toner"
    #>   .. ..$ ext        : chr "png"
    #>   ..$ variants:List of 12
    #>   .. ..$ Toner            : chr "toner"
    #>   .. ..$ TonerBackground  : chr "toner-background"
    #>   .. ..$ TonerHybrid      : chr "toner-hybrid"
    #>   .. ..$ TonerLines       : chr "toner-lines"
    #>   .. ..$ TonerLabels      : chr "toner-labels"
    #>   .. ..$ TonerLite        : chr "toner-lite"
    #>   .. ..$ Watercolor       :List of 2
    #>   .. .. ..$ url    : chr "https://stamen-tiles-{s}.a.ssl.fastly.net/{variant}/{z}/{x}/{y}.{ext}"
    #>   .. .. ..$ options:List of 4
    #>   .. .. .. ..$ variant: chr "watercolor"
    #>   .. .. .. ..$ ext    : chr "jpg"
    #>   .. .. .. ..$ minZoom: int 1
    #>   .. .. .. ..$ maxZoom: int 16
    #>   .. ..$ Terrain          :List of 1
    #>   .. .. ..$ options:List of 3
    #>   .. .. .. ..$ variant: chr "terrain"
    #>   .. .. .. ..$ minZoom: int 0
    #>   .. .. .. ..$ maxZoom: int 18
    #>   .. ..$ TerrainBackground:List of 1
    #>   .. .. ..$ options:List of 3
    #>   .. .. .. ..$ variant: chr "terrain-background"
    #>   .. .. .. ..$ minZoom: int 0
    #>   .. .. .. ..$ maxZoom: int 18
    #>   .. ..$ TerrainLabels    :List of 1
    #>   .. .. ..$ options:List of 3
    #>   .. .. .. ..$ variant: chr "terrain-labels"
    #>   .. .. .. ..$ minZoom: int 0
    #>   .. .. .. ..$ maxZoom: int 18
    #>   .. ..$ TopOSMRelief     :List of 2
    #>   .. .. ..$ url    : chr "https://stamen-tiles-{s}.a.ssl.fastly.net/{variant}/{z}/{x}/{y}.{ext}"
    #>   .. .. ..$ options:List of 3
    #>   .. .. .. ..$ variant: chr "toposm-color-relief"
    #>   .. .. .. ..$ ext    : chr "jpg"
    #>   .. .. .. ..$ bounds : int [1:2, 1:2] 22 51 -132 -56
    #>   .. ..$ TopOSMFeatures   :List of 1
    #>   .. .. ..$ options:List of 3
    #>   .. .. .. ..$ variant: chr "toposm-features"
    #>   .. .. .. ..$ bounds : int [1:2, 1:2] 22 51 -132 -56
    #>   .. .. .. ..$ opacity: num 0.9
    #>  $ TomTom          :List of 3
    #>   ..$ url     : chr "https://{s}.api.tomtom.com/map/1/tile/{variant}/{style}/{z}/{x}/{y}.{ext}?key={apikey}"
    #>   ..$ options :List of 7
    #>   .. ..$ variant    : chr "basic"
    #>   .. ..$ maxZoom    : int 22
    #>   .. ..$ attribution: chr "<a href=\"https://tomtom.com\" target=\"_blank\">&copy;  1992 - 2023 TomTom.</a> "
    #>   .. ..$ subdomains : chr "abcd"
    #>   .. ..$ style      : chr "main"
    #>   .. ..$ ext        : chr "png"
    #>   .. ..$ apikey     : chr "<insert your API key here>"
    #>   ..$ variants:List of 3
    #>   .. ..$ Basic : chr "basic"
    #>   .. ..$ Hybrid: chr "hybrid"
    #>   .. ..$ Labels: chr "labels"
    #>  $ Esri            :List of 3
    #>   ..$ url     : chr "https://server.arcgisonline.com/ArcGIS/rest/services/{variant}/MapServer/tile/{z}/{y}/{x}"
    #>   ..$ options :List of 2
    #>   .. ..$ variant    : chr "World_Street_Map"
    #>   .. ..$ attribution: chr "Tiles &copy; Esri"
    #>   ..$ variants:List of 10
    #>   .. ..$ WorldStreetMap   :List of 1
    #>   .. .. ..$ options:List of 1
    #>   .. .. .. ..$ attribution: chr "{attribution.Esri} &mdash; Source: Esri, DeLorme, NAVTEQ, USGS, Intermap, iPC, NRCAN, Esri Japan, METI, Esri Ch"| __truncated__
    #>   .. ..$ DeLorme          :List of 1
    #>   .. .. ..$ options:List of 4
    #>   .. .. .. ..$ variant    : chr "Specialty/DeLorme_World_Base_Map"
    #>   .. .. .. ..$ minZoom    : int 1
    #>   .. .. .. ..$ maxZoom    : int 11
    #>   .. .. .. ..$ attribution: chr "{attribution.Esri} &mdash; Copyright: &copy;2012 DeLorme"
    #>   .. ..$ WorldTopoMap     :List of 1
    #>   .. .. ..$ options:List of 2
    #>   .. .. .. ..$ variant    : chr "World_Topo_Map"
    #>   .. .. .. ..$ attribution: chr "{attribution.Esri} &mdash; Esri, DeLorme, NAVTEQ, TomTom, Intermap, iPC, USGS, FAO, NPS, NRCAN, GeoBase, Kadast"| __truncated__
    #>   .. ..$ WorldImagery     :List of 1
    #>   .. .. ..$ options:List of 2
    #>   .. .. .. ..$ variant    : chr "World_Imagery"
    #>   .. .. .. ..$ attribution: chr "{attribution.Esri} &mdash; Source: Esri, i-cubed, USDA, USGS, AEX, GeoEye, Getmapping, Aerogrid, IGN, IGP, UPR-"| __truncated__
    #>   .. ..$ WorldTerrain     :List of 1
    #>   .. .. ..$ options:List of 3
    #>   .. .. .. ..$ variant    : chr "World_Terrain_Base"
    #>   .. .. .. ..$ maxZoom    : int 13
    #>   .. .. .. ..$ attribution: chr "{attribution.Esri} &mdash; Source: USGS, Esri, TANA, DeLorme, and NPS"
    #>   .. ..$ WorldShadedRelief:List of 1
    #>   .. .. ..$ options:List of 3
    #>   .. .. .. ..$ variant    : chr "World_Shaded_Relief"
    #>   .. .. .. ..$ maxZoom    : int 13
    #>   .. .. .. ..$ attribution: chr "{attribution.Esri} &mdash; Source: Esri"
    #>   .. ..$ WorldPhysical    :List of 1
    #>   .. .. ..$ options:List of 3
    #>   .. .. .. ..$ variant    : chr "World_Physical_Map"
    #>   .. .. .. ..$ maxZoom    : int 8
    #>   .. .. .. ..$ attribution: chr "{attribution.Esri} &mdash; Source: US National Park Service"
    #>   .. ..$ OceanBasemap     :List of 1
    #>   .. .. ..$ options:List of 3
    #>   .. .. .. ..$ variant    : chr "Ocean_Basemap"
    #>   .. .. .. ..$ maxZoom    : int 13
    #>   .. .. .. ..$ attribution: chr "{attribution.Esri} &mdash; Sources: GEBCO, NOAA, CHS, OSU, UNH, CSUMB, National Geographic, DeLorme, NAVTEQ, and Esri"
    #>   .. ..$ NatGeoWorldMap   :List of 1
    #>   .. .. ..$ options:List of 3
    #>   .. .. .. ..$ variant    : chr "NatGeo_World_Map"
    #>   .. .. .. ..$ maxZoom    : int 16
    #>   .. .. .. ..$ attribution: chr "{attribution.Esri} &mdash; National Geographic, Esri, DeLorme, NAVTEQ, UNEP-WCMC, USGS, NASA, ESA, METI, NRCAN,"| __truncated__
    #>   .. ..$ WorldGrayCanvas  :List of 1
    #>   .. .. ..$ options:List of 3
    #>   .. .. .. ..$ variant    : chr "Canvas/World_Light_Gray_Base"
    #>   .. .. .. ..$ maxZoom    : int 16
    #>   .. .. .. ..$ attribution: chr "{attribution.Esri} &mdash; Esri, DeLorme, NAVTEQ"
    #>  $ OpenWeatherMap  :List of 3
    #>   ..$ url     : chr "http://{s}.tile.openweathermap.org/map/{variant}/{z}/{x}/{y}.png?appid={apiKey}"
    #>   ..$ options :List of 4
    #>   .. ..$ maxZoom    : int 19
    #>   .. ..$ attribution: chr "Map data &copy; <a href=\"http://openweathermap.org\">OpenWeatherMap</a>"
    #>   .. ..$ apiKey     : chr "<insert your api key here>"
    #>   .. ..$ opacity    : num 0.5
    #>   ..$ variants:List of 11
    #>   .. ..$ Clouds              : chr "clouds"
    #>   .. ..$ CloudsClassic       : chr "clouds_cls"
    #>   .. ..$ Precipitation       : chr "precipitation"
    #>   .. ..$ PrecipitationClassic: chr "precipitation_cls"
    #>   .. ..$ Rain                : chr "rain"
    #>   .. ..$ RainClassic         : chr "rain_cls"
    #>   .. ..$ Pressure            : chr "pressure"
    #>   .. ..$ PressureContour     : chr "pressure_cntr"
    #>   .. ..$ Wind                : chr "wind"
    #>   .. ..$ Temperature         : chr "temp"
    #>   .. ..$ Snow                : chr "snow"
    #>  $ HERE            :List of 3
    #>   ..$ url     : chr "https://{s}.{base}.maps.api.here.com/maptile/2.1/{type}/{mapID}/{variant}/{z}/{x}/{y}/{size}/{format}?app_id={a"| __truncated__
    #>   ..$ options :List of 12
    #>   .. ..$ attribution: chr "Map &copy; 1987-2023 <a href=\"http://developer.here.com\">HERE</a>"
    #>   .. ..$ subdomains : chr "1234"
    #>   .. ..$ mapID      : chr "newest"
    #>   .. ..$ app_id     : chr "<insert your app_id here>"
    #>   .. ..$ app_code   : chr "<insert your app_code here>"
    #>   .. ..$ base       : chr "base"
    #>   .. ..$ variant    : chr "normal.day"
    #>   .. ..$ maxZoom    : int 20
    #>   .. ..$ type       : chr "maptile"
    #>   .. ..$ language   : chr "eng"
    #>   .. ..$ format     : chr "png8"
    #>   .. ..$ size       : chr "256"
    #>   ..$ variants:List of 30
    #>   .. ..$ normalDay               : chr "normal.day"
    #>   .. ..$ normalDayCustom         : chr "normal.day.custom"
    #>   .. ..$ normalDayGrey           : chr "normal.day.grey"
    #>   .. ..$ normalDayMobile         : chr "normal.day.mobile"
    #>   .. ..$ normalDayGreyMobile     : chr "normal.day.grey.mobile"
    #>   .. ..$ normalDayTransit        : chr "normal.day.transit"
    #>   .. ..$ normalDayTransitMobile  : chr "normal.day.transit.mobile"
    #>   .. ..$ normalDayTraffic        :List of 1
    #>   .. .. ..$ options:List of 3
    #>   .. .. .. ..$ variant: chr "normal.traffic.day"
    #>   .. .. .. ..$ base   : chr "traffic"
    #>   .. .. .. ..$ type   : chr "traffictile"
    #>   .. ..$ normalNight             : chr "normal.night"
    #>   .. ..$ normalNightMobile       : chr "normal.night.mobile"
    #>   .. ..$ normalNightGrey         : chr "normal.night.grey"
    #>   .. ..$ normalNightGreyMobile   : chr "normal.night.grey.mobile"
    #>   .. ..$ normalNightTransit      : chr "normal.night.transit"
    #>   .. ..$ normalNightTransitMobile: chr "normal.night.transit.mobile"
    #>   .. ..$ reducedDay              : chr "reduced.day"
    #>   .. ..$ reducedNight            : chr "reduced.night"
    #>   .. ..$ basicMap                :List of 1
    #>   .. .. ..$ options:List of 1
    #>   .. .. .. ..$ type: chr "basetile"
    #>   .. ..$ mapLabels               :List of 1
    #>   .. .. ..$ options:List of 2
    #>   .. .. .. ..$ type  : chr "labeltile"
    #>   .. .. .. ..$ format: chr "png"
    #>   .. ..$ trafficFlow             :List of 1
    #>   .. .. ..$ options:List of 2
    #>   .. .. .. ..$ base: chr "traffic"
    #>   .. .. .. ..$ type: chr "flowtile"
    #>   .. ..$ carnavDayGrey           : chr "carnav.day.grey"
    #>   .. ..$ hybridDay               :List of 1
    #>   .. .. ..$ options:List of 2
    #>   .. .. .. ..$ base   : chr "aerial"
    #>   .. .. .. ..$ variant: chr "hybrid.day"
    #>   .. ..$ hybridDayMobile         :List of 1
    #>   .. .. ..$ options:List of 2
    #>   .. .. .. ..$ base   : chr "aerial"
    #>   .. .. .. ..$ variant: chr "hybrid.day.mobile"
    #>   .. ..$ hybridDayTransit        :List of 1
    #>   .. .. ..$ options:List of 2
    #>   .. .. .. ..$ base   : chr "aerial"
    #>   .. .. .. ..$ variant: chr "hybrid.day.transit"
    #>   .. ..$ hybridDayGrey           :List of 1
    #>   .. .. ..$ options:List of 2
    #>   .. .. .. ..$ base   : chr "aerial"
    #>   .. .. .. ..$ variant: chr "hybrid.grey.day"
    #>   .. ..$ hybridDayTraffic        :List of 1
    #>   .. .. ..$ options:List of 3
    #>   .. .. .. ..$ variant: chr "hybrid.traffic.day"
    #>   .. .. .. ..$ base   : chr "traffic"
    #>   .. .. .. ..$ type   : chr "traffictile"
    #>   .. ..$ pedestrianDay           : chr "pedestrian.day"
    #>   .. ..$ pedestrianNight         : chr "pedestrian.night"
    #>   .. ..$ satelliteDay            :List of 1
    #>   .. .. ..$ options:List of 2
    #>   .. .. .. ..$ base   : chr "aerial"
    #>   .. .. .. ..$ variant: chr "satellite.day"
    #>   .. ..$ terrainDay              :List of 1
    #>   .. .. ..$ options:List of 2
    #>   .. .. .. ..$ base   : chr "aerial"
    #>   .. .. .. ..$ variant: chr "terrain.day"
    #>   .. ..$ terrainDayMobile        :List of 1
    #>   .. .. ..$ options:List of 2
    #>   .. .. .. ..$ base   : chr "aerial"
    #>   .. .. .. ..$ variant: chr "terrain.day.mobile"
    #>  $ HEREv3          :List of 3
    #>   ..$ url     : chr "https://{s}.{base}.maps.ls.hereapi.com/maptile/2.1/{type}/{mapID}/{variant}/{z}/{x}/{y}/{size}/{format}?apiKey="| __truncated__
    #>   ..$ options :List of 11
    #>   .. ..$ attribution: chr "Map &copy; 1987-2023 <a href=\"http://developer.here.com\">HERE</a>"
    #>   .. ..$ subdomains : chr "1234"
    #>   .. ..$ mapID      : chr "newest"
    #>   .. ..$ apiKey     : chr "<insert your apiKey here>"
    #>   .. ..$ base       : chr "base"
    #>   .. ..$ variant    : chr "normal.day"
    #>   .. ..$ maxZoom    : int 20
    #>   .. ..$ type       : chr "maptile"
    #>   .. ..$ language   : chr "eng"
    #>   .. ..$ format     : chr "png8"
    #>   .. ..$ size       : chr "256"
    #>   ..$ variants:List of 28
    #>   .. ..$ normalDay               : chr "normal.day"
    #>   .. ..$ normalDayCustom         : chr "normal.day.custom"
    #>   .. ..$ normalDayGrey           : chr "normal.day.grey"
    #>   .. ..$ normalDayMobile         : chr "normal.day.mobile"
    #>   .. ..$ normalDayGreyMobile     : chr "normal.day.grey.mobile"
    #>   .. ..$ normalDayTransit        : chr "normal.day.transit"
    #>   .. ..$ normalDayTransitMobile  : chr "normal.day.transit.mobile"
    #>   .. ..$ normalNight             : chr "normal.night"
    #>   .. ..$ normalNightMobile       : chr "normal.night.mobile"
    #>   .. ..$ normalNightGrey         : chr "normal.night.grey"
    #>   .. ..$ normalNightGreyMobile   : chr "normal.night.grey.mobile"
    #>   .. ..$ normalNightTransit      : chr "normal.night.transit"
    #>   .. ..$ normalNightTransitMobile: chr "normal.night.transit.mobile"
    #>   .. ..$ reducedDay              : chr "reduced.day"
    #>   .. ..$ reducedNight            : chr "reduced.night"
    #>   .. ..$ basicMap                :List of 1
    #>   .. .. ..$ options:List of 1
    #>   .. .. .. ..$ type: chr "basetile"
    #>   .. ..$ mapLabels               :List of 1
    #>   .. .. ..$ options:List of 2
    #>   .. .. .. ..$ type  : chr "labeltile"
    #>   .. .. .. ..$ format: chr "png"
    #>   .. ..$ trafficFlow             :List of 1
    #>   .. .. ..$ options:List of 2
    #>   .. .. .. ..$ base: chr "traffic"
    #>   .. .. .. ..$ type: chr "flowtile"
    #>   .. ..$ carnavDayGrey           : chr "carnav.day.grey"
    #>   .. ..$ hybridDay               :List of 1
    #>   .. .. ..$ options:List of 2
    #>   .. .. .. ..$ base   : chr "aerial"
    #>   .. .. .. ..$ variant: chr "hybrid.day"
    #>   .. ..$ hybridDayMobile         :List of 1
    #>   .. .. ..$ options:List of 2
    #>   .. .. .. ..$ base   : chr "aerial"
    #>   .. .. .. ..$ variant: chr "hybrid.day.mobile"
    #>   .. ..$ hybridDayTransit        :List of 1
    #>   .. .. ..$ options:List of 2
    #>   .. .. .. ..$ base   : chr "aerial"
    #>   .. .. .. ..$ variant: chr "hybrid.day.transit"
    #>   .. ..$ hybridDayGrey           :List of 1
    #>   .. .. ..$ options:List of 2
    #>   .. .. .. ..$ base   : chr "aerial"
    #>   .. .. .. ..$ variant: chr "hybrid.grey.day"
    #>   .. ..$ pedestrianDay           : chr "pedestrian.day"
    #>   .. ..$ pedestrianNight         : chr "pedestrian.night"
    #>   .. ..$ satelliteDay            :List of 1
    #>   .. .. ..$ options:List of 2
    #>   .. .. .. ..$ base   : chr "aerial"
    #>   .. .. .. ..$ variant: chr "satellite.day"
    #>   .. ..$ terrainDay              :List of 1
    #>   .. .. ..$ options:List of 2
    #>   .. .. .. ..$ base   : chr "aerial"
    #>   .. .. .. ..$ variant: chr "terrain.day"
    #>   .. ..$ terrainDayMobile        :List of 1
    #>   .. .. ..$ options:List of 2
    #>   .. .. .. ..$ base   : chr "aerial"
    #>   .. .. .. ..$ variant: chr "terrain.day.mobile"
    #>  $ FreeMapSK       :List of 2
    #>   ..$ url    : chr "https://{s}.freemap.sk/T/{z}/{x}/{y}.jpeg"
    #>   ..$ options:List of 5
    #>   .. ..$ minZoom    : int 8
    #>   .. ..$ maxZoom    : int 16
    #>   .. ..$ subdomains : chr "abcd"
    #>   .. ..$ bounds     : num [1:2, 1:2] 47.2 49.8 16 22.6
    #>   .. ..$ attribution: chr "{attribution.OpenStreetMap}, vizualization CC-By-SA 2.0 <a href=\"http://freemap.sk\">Freemap.sk</a>"
    #>  $ MtbMap          :List of 2
    #>   ..$ url    : chr "http://tile.mtbmap.cz/mtbmap_tiles/{z}/{x}/{y}.png"
    #>   ..$ options:List of 1
    #>   .. ..$ attribution: chr "{attribution.OpenStreetMap} &amp; USGS"
    #>  $ CartoDB         :List of 3
    #>   ..$ url     : chr "https://{s}.basemaps.cartocdn.com/{variant}/{z}/{x}/{y}{r}.png"
    #>   ..$ options :List of 4
    #>   .. ..$ attribution: chr "{attribution.OpenStreetMap} &copy; <a href=\"https://carto.com/attributions\">CARTO</a>"
    #>   .. ..$ subdomains : chr "abcd"
    #>   .. ..$ maxZoom    : int 20
    #>   .. ..$ variant    : chr "light_all"
    #>   ..$ variants:List of 10
    #>   .. ..$ Positron            : chr "light_all"
    #>   .. ..$ PositronNoLabels    : chr "light_nolabels"
    #>   .. ..$ PositronOnlyLabels  : chr "light_only_labels"
    #>   .. ..$ DarkMatter          : chr "dark_all"
    #>   .. ..$ DarkMatterNoLabels  : chr "dark_nolabels"
    #>   .. ..$ DarkMatterOnlyLabels: chr "dark_only_labels"
    #>   .. ..$ Voyager             : chr "rastertiles/voyager"
    #>   .. ..$ VoyagerNoLabels     : chr "rastertiles/voyager_nolabels"
    #>   .. ..$ VoyagerOnlyLabels   : chr "rastertiles/voyager_only_labels"
    #>   .. ..$ VoyagerLabelsUnder  : chr "rastertiles/voyager_labels_under"
    #>  $ HikeBike        :List of 3
    #>   ..$ url     : chr "https://tiles.wmflabs.org/{variant}/{z}/{x}/{y}.png"
    #>   ..$ options :List of 3
    #>   .. ..$ maxZoom    : int 19
    #>   .. ..$ attribution: chr "{attribution.OpenStreetMap}"
    #>   .. ..$ variant    : chr "hikebike"
    #>   ..$ variants:List of 2
    #>   .. ..$ HikeBike   : Named list()
    #>   .. ..$ HillShading:List of 1
    #>   .. .. ..$ options:List of 2
    #>   .. .. .. ..$ maxZoom: int 15
    #>   .. .. .. ..$ variant: chr "hillshading"
    #>  $ BasemapAT       :List of 3
    #>   ..$ url     : chr "https://maps{s}.wien.gv.at/basemap/{variant}/{type}/google3857/{z}/{y}/{x}.{format}"
    #>   ..$ options :List of 7
    #>   .. ..$ maxZoom    : int 19
    #>   .. ..$ attribution: chr "Datenquelle: <a href=\"https://www.basemap.at\">basemap.at</a>"
    #>   .. ..$ subdomains : chr [1:5] "" "1" "2" "3" ...
    #>   .. ..$ type       : chr "normal"
    #>   .. ..$ format     : chr "png"
    #>   .. ..$ bounds     : num [1:2, 1:2] 46.36 49.04 8.78 17.19
    #>   .. ..$ variant    : chr "geolandbasemap"
    #>   ..$ variants:List of 7
    #>   .. ..$ basemap  :List of 1
    #>   .. .. ..$ options:List of 2
    #>   .. .. .. ..$ maxZoom: int 20
    #>   .. .. .. ..$ variant: chr "geolandbasemap"
    #>   .. ..$ grau     : chr "bmapgrau"
    #>   .. ..$ overlay  : chr "bmapoverlay"
    #>   .. ..$ terrain  :List of 1
    #>   .. .. ..$ options:List of 3
    #>   .. .. .. ..$ variant: chr "bmapgelaende"
    #>   .. .. .. ..$ type   : chr "grau"
    #>   .. .. .. ..$ format : chr "jpeg"
    #>   .. ..$ surface  :List of 1
    #>   .. .. ..$ options:List of 3
    #>   .. .. .. ..$ variant: chr "bmapoberflaeche"
    #>   .. .. .. ..$ type   : chr "grau"
    #>   .. .. .. ..$ format : chr "jpeg"
    #>   .. ..$ highdpi  :List of 1
    #>   .. .. ..$ options:List of 2
    #>   .. .. .. ..$ variant: chr "bmaphidpi"
    #>   .. .. .. ..$ format : chr "jpeg"
    #>   .. ..$ orthofoto:List of 1
    #>   .. .. ..$ options:List of 3
    #>   .. .. .. ..$ maxZoom: int 20
    #>   .. .. .. ..$ variant: chr "bmaporthofoto30cm"
    #>   .. .. .. ..$ format : chr "jpeg"
    #>  $ nlmaps          :List of 3
    #>   ..$ url     : chr "https://geodata.nationaalgeoregister.nl/tiles/service/wmts/{variant}/EPSG:3857/{z}/{x}/{y}.png"
    #>   ..$ options :List of 4
    #>   .. ..$ minZoom    : int 6
    #>   .. ..$ maxZoom    : int 19
    #>   .. ..$ bounds     : num [1:2, 1:2] 50.5 54 3.25 7.6
    #>   .. ..$ attribution: chr "Kaartgegevens &copy; <a href=\"https://www.kadaster.nl\">Kadaster</a>"
    #>   ..$ variants:List of 4
    #>   .. ..$ standaard: chr "brtachtergrondkaart"
    #>   .. ..$ pastel   : chr "brtachtergrondkaartpastel"
    #>   .. ..$ grijs    : chr "brtachtergrondkaartgrijs"
    #>   .. ..$ luchtfoto:List of 1
    #>   .. .. ..$ url: chr "https://service.pdok.nl/hwh/luchtfotorgb/wmts/v1_0/Actueel_ortho25/EPSG:3857/{z}/{x}/{y}.jpeg"
    #>  $ NASAGIBS        :List of 3
    #>   ..$ url     : chr "https://map1.vis.earthdata.nasa.gov/wmts-webmerc/{variant}/default/{time}/{tilematrixset}{maxZoom}/{z}/{y}/{x}.{format}"
    #>   ..$ options :List of 7
    #>   .. ..$ attribution  : chr "Imagery provided by services from the Global Imagery Browse Services (GIBS), operated by the NASA/GSFC/Earth Sc"| __truncated__
    #>   .. ..$ bounds       : num [1:2, 1:2] -85.1 85.1 -180 180
    #>   .. ..$ minZoom      : int 1
    #>   .. ..$ maxZoom      : int 9
    #>   .. ..$ format       : chr "jpg"
    #>   .. ..$ time         : chr ""
    #>   .. ..$ tilematrixset: chr "GoogleMapsCompatible_Level"
    #>   ..$ variants:List of 7
    #>   .. ..$ ModisTerraTrueColorCR: chr "MODIS_Terra_CorrectedReflectance_TrueColor"
    #>   .. ..$ ModisTerraBands367CR : chr "MODIS_Terra_CorrectedReflectance_Bands367"
    #>   .. ..$ ViirsEarthAtNight2012:List of 1
    #>   .. .. ..$ options:List of 2
    #>   .. .. .. ..$ variant: chr "VIIRS_CityLights_2012"
    #>   .. .. .. ..$ maxZoom: int 8
    #>   .. ..$ ModisTerraLSTDay     :List of 1
    #>   .. .. ..$ options:List of 4
    #>   .. .. .. ..$ variant: chr "MODIS_Terra_Land_Surface_Temp_Day"
    #>   .. .. .. ..$ format : chr "png"
    #>   .. .. .. ..$ maxZoom: int 7
    #>   .. .. .. ..$ opacity: num 0.75
    #>   .. ..$ ModisTerraSnowCover  :List of 1
    #>   .. .. ..$ options:List of 4
    #>   .. .. .. ..$ variant: chr "MODIS_Terra_NDSI_Snow_Cover"
    #>   .. .. .. ..$ format : chr "png"
    #>   .. .. .. ..$ maxZoom: int 8
    #>   .. .. .. ..$ opacity: num 0.75
    #>   .. ..$ ModisTerraAOD        :List of 1
    #>   .. .. ..$ options:List of 4
    #>   .. .. .. ..$ variant: chr "MODIS_Terra_Aerosol"
    #>   .. .. .. ..$ format : chr "png"
    #>   .. .. .. ..$ maxZoom: int 6
    #>   .. .. .. ..$ opacity: num 0.75
    #>   .. ..$ ModisTerraChlorophyll:List of 1
    #>   .. .. ..$ options:List of 4
    #>   .. .. .. ..$ variant: chr "MODIS_Terra_Chlorophyll_A"
    #>   .. .. .. ..$ format : chr "png"
    #>   .. .. .. ..$ maxZoom: int 7
    #>   .. .. .. ..$ opacity: num 0.75
    #>  $ NLS             :List of 2
    #>   ..$ url    : chr "https://nls-{s}.tileserver.com/nls/{z}/{x}/{y}.jpg"
    #>   ..$ options:List of 5
    #>   .. ..$ attribution: chr "<a href=\"http://geo.nls.uk/maps/\">National Library of Scotland Historic Maps</a>"
    #>   .. ..$ bounds     : num [1:2, 1:2] 49.6 61.7 -12 3
    #>   .. ..$ minZoom    : int 1
    #>   .. ..$ maxZoom    : int 18
    #>   .. ..$ subdomains : chr "0123"
    #>  $ JusticeMap      :List of 3
    #>   ..$ url     : chr "https://www.justicemap.org/tile/{size}/{variant}/{z}/{x}/{y}.png"
    #>   ..$ options :List of 3
    #>   .. ..$ attribution: chr "<a href=\"http://www.justicemap.org/terms.php\">Justice Map</a>"
    #>   .. ..$ size       : chr "county"
    #>   .. ..$ bounds     : int [1:2, 1:2] 14 72 -180 -56
    #>   ..$ variants:List of 9
    #>   .. ..$ income        : chr "income"
    #>   .. ..$ americanIndian: chr "indian"
    #>   .. ..$ asian         : chr "asian"
    #>   .. ..$ black         : chr "black"
    #>   .. ..$ hispanic      : chr "hispanic"
    #>   .. ..$ multi         : chr "multi"
    #>   .. ..$ nonWhite      : chr "nonwhite"
    #>   .. ..$ white         : chr "white"
    #>   .. ..$ plurality     : chr "plural"
    #>  $ GeoportailFrance:List of 3
    #>   ..$ url     : chr "https://wxs.ign.fr/{apikey}/geoportail/wmts?REQUEST=GetTile&SERVICE=WMTS&VERSION=1.0.0&STYLE={style}&TILEMATRIX"| __truncated__
    #>   ..$ options :List of 8
    #>   .. ..$ attribution: chr "<a target=\"_blank\" href=\"https://www.geoportail.gouv.fr/\">Geoportail France</a>"
    #>   .. ..$ bounds     : int [1:2, 1:2] -75 81 -180 180
    #>   .. ..$ minZoom    : int 2
    #>   .. ..$ maxZoom    : int 18
    #>   .. ..$ apikey     : chr "choisirgeoportail"
    #>   .. ..$ format     : chr "image/png"
    #>   .. ..$ style      : chr "normal"
    #>   .. ..$ variant    : chr "GEOGRAPHICALGRIDSYSTEMS.PLANIGNV2"
    #>   ..$ variants:List of 3
    #>   .. ..$ plan   : chr "GEOGRAPHICALGRIDSYSTEMS.PLANIGNV2"
    #>   .. ..$ parcels:List of 1
    #>   .. .. ..$ options:List of 3
    #>   .. .. .. ..$ variant: chr "CADASTRALPARCELS.PARCELLAIRE_EXPRESS"
    #>   .. .. .. ..$ style  : chr "PCI vecteur"
    #>   .. .. .. ..$ maxZoom: int 20
    #>   .. ..$ orthos :List of 1
    #>   .. .. ..$ options:List of 3
    #>   .. .. .. ..$ maxZoom: int 19
    #>   .. .. .. ..$ format : chr "image/jpeg"
    #>   .. .. .. ..$ variant: chr "ORTHOIMAGERY.ORTHOPHOTOS"
    #>  $ OneMapSG        :List of 3
    #>   ..$ url     : chr "https://maps-{s}.onemap.sg/v3/{variant}/{z}/{x}/{y}.png"
    #>   ..$ options :List of 5
    #>   .. ..$ variant    : chr "Default"
    #>   .. ..$ minZoom    : int 11
    #>   .. ..$ maxZoom    : int 18
    #>   .. ..$ bounds     : num [1:2, 1:2] 1.56 1.16 104.11 103.5
    #>   .. ..$ attribution: chr "<img src=\"https://docs.onemap.sg/maps/images/oneMap64-01.png\" style=\"height:20px;width:20px;\"/> New OneMap "| __truncated__
    #>   ..$ variants:List of 5
    #>   .. ..$ Default : chr "Default"
    #>   .. ..$ Night   : chr "Night"
    #>   .. ..$ Original: chr "Original"
    #>   .. ..$ Grey    : chr "Grey"
    #>   .. ..$ LandLot : chr "LandLot"
    #>  $ USGS            :List of 3
    #>   ..$ url     : chr "https://basemap.nationalmap.gov/arcgis/rest/services/USGSTopo/MapServer/tile/{z}/{y}/{x}"
    #>   ..$ options :List of 2
    #>   .. ..$ maxZoom    : int 20
    #>   .. ..$ attribution: chr "Tiles courtesy of the <a href=\"https://usgs.gov/\">U.S. Geological Survey</a>"
    #>   ..$ variants:List of 3
    #>   .. ..$ USTopo       : Named list()
    #>   .. ..$ USImagery    :List of 1
    #>   .. .. ..$ url: chr "https://basemap.nationalmap.gov/arcgis/rest/services/USGSImageryOnly/MapServer/tile/{z}/{y}/{x}"
    #>   .. ..$ USImageryTopo:List of 1
    #>   .. .. ..$ url: chr "https://basemap.nationalmap.gov/arcgis/rest/services/USGSImageryTopo/MapServer/tile/{z}/{y}/{x}"
    #>  $ WaymarkedTrails :List of 3
    #>   ..$ url     : chr "https://tile.waymarkedtrails.org/{variant}/{z}/{x}/{y}.png"
    #>   ..$ options :List of 2
    #>   .. ..$ maxZoom    : int 18
    #>   .. ..$ attribution: chr "Map data: {attribution.OpenStreetMap} | Map style: &copy; <a href=\"https://waymarkedtrails.org\">waymarkedtrai"| __truncated__
    #>   ..$ variants:List of 6
    #>   .. ..$ hiking : chr "hiking"
    #>   .. ..$ cycling: chr "cycling"
    #>   .. ..$ mtb    : chr "mtb"
    #>   .. ..$ slopes : chr "slopes"
    #>   .. ..$ riding : chr "riding"
    #>   .. ..$ skating: chr "skating"
    #>  $ OpenAIP         :List of 2
    #>   ..$ url    : chr "https://{s}.tile.maps.openaip.net/geowebcache/service/tms/1.0.0/openaip_basemap@EPSG%3A900913@png/{z}/{x}/{y}.{ext}"
    #>   ..$ options:List of 7
    #>   .. ..$ attribution : chr "<a href=\"https://www.openaip.net/\">openAIP Data</a> (<a href=\"https://creativecommons.org/licenses/by-sa/3.0"| __truncated__
    #>   .. ..$ ext         : chr "png"
    #>   .. ..$ minZoom     : int 4
    #>   .. ..$ maxZoom     : int 14
    #>   .. ..$ tms         : logi TRUE
    #>   .. ..$ detectRetina: logi TRUE
    #>   .. ..$ subdomains  : chr "12"
    #>  $ OpenSnowMap     :List of 3
    #>   ..$ url     : chr "https://tiles.opensnowmap.org/{variant}/{z}/{x}/{y}.png"
    #>   ..$ options :List of 3
    #>   .. ..$ minZoom    : int 9
    #>   .. ..$ maxZoom    : int 18
    #>   .. ..$ attribution: chr "Map data: {attribution.OpenStreetMap} & ODbL, &copy; <a href=\"https://www.opensnowmap.org/iframes/data.html\">"| __truncated__
    #>   ..$ variants:List of 1
    #>   .. ..$ pistes: chr "pistes"
    #>  $ AzureMaps       :List of 3
    #>   ..$ url     : chr "https://atlas.microsoft.com/map/tile?api-version={apiVersion}&tilesetId={variant}&x={x}&y={y}&zoom={z}&language"| __truncated__
    #>   ..$ options :List of 5
    #>   .. ..$ attribution    : chr "See https://docs.microsoft.com/en-US/rest/api/maps/renderv2/getmaptilepreview for details."
    #>   .. ..$ apiVersion     : chr "2.0"
    #>   .. ..$ variant        : chr "microsoft.imagery"
    #>   .. ..$ subscriptionKey: chr "<insert your subscription key here>"
    #>   .. ..$ language       : chr "en-US"
    #>   ..$ variants:List of 7
    #>   .. ..$ MicrosoftImagery            : chr "microsoft.imagery"
    #>   .. ..$ MicrosoftBaseDarkGrey       : chr "microsoft.base.darkgrey"
    #>   .. ..$ MicrosoftBaseRoad           : chr "microsoft.base.road"
    #>   .. ..$ MicrosoftBaseHybridRoad     : chr "microsoft.base.hybrid.road"
    #>   .. ..$ MicrosoftTerraMain          : chr "microsoft.terra.main"
    #>   .. ..$ MicrosoftWeatherInfraredMain:List of 2
    #>   .. .. ..$ url    : chr "https://atlas.microsoft.com/map/tile?api-version={apiVersion}&tilesetId={variant}&x={x}&y={y}&zoom={z}&timeStam"| __truncated__
    #>   .. .. ..$ options:List of 3
    #>   .. .. .. ..$ timeStamp  : chr "2021-05-08T09:03:00Z"
    #>   .. .. .. ..$ attribution: chr "See https://docs.microsoft.com/en-US/rest/api/maps/renderv2/getmaptilepreview#uri-parameters for details."
    #>   .. .. .. ..$ variant    : chr "microsoft.weather.infrared.main"
    #>   .. ..$ MicrosoftWeatherRadarMain   :List of 2
    #>   .. .. ..$ url    : chr "https://atlas.microsoft.com/map/tile?api-version={apiVersion}&tilesetId={variant}&x={x}&y={y}&zoom={z}&timeStam"| __truncated__
    #>   .. .. ..$ options:List of 3
    #>   .. .. .. ..$ timeStamp  : chr "2021-05-08T09:03:00Z"
    #>   .. .. .. ..$ attribution: chr "See https://docs.microsoft.com/en-US/rest/api/maps/renderv2/getmaptilepreview#uri-parameters for details."
    #>   .. .. .. ..$ variant    : chr "microsoft.weather.radar.main"

</div>
