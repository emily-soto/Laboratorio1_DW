Lab1\_Markdown
================
EmilySoto
15/8/2021

## Cargar librería

``` r
library(readxl)
library(lubridate)
```

    ## 
    ## Attaching package: 'lubridate'

    ## The following objects are masked from 'package:base':
    ## 
    ##     date, intersect, setdiff, union

``` r
library(readr)
```

# Problema 1

## Cargar archivos

``` r
enero <- data.frame(read_excel("Laboratorio_1/01-2018.xlsx"),fecha="2018-01-01") 
feb <- data.frame(read_excel("Laboratorio_1/02-2018.xlsx"),fecha="2018-02-01") 
marzo <- data.frame(read_excel("Laboratorio_1/03-2018.xlsx"),fecha="2018-03-01") 
abril <- data.frame(read_excel("Laboratorio_1/04-2018.xlsx"),fecha="2018-04-01") 
mayo <- data.frame(read_excel("Laboratorio_1/05-2018.xlsx"),fecha="2018-05-01") 
jun <- data.frame(read_excel("Laboratorio_1/06-2018.xlsx"),fecha="2018-06-01") 
jul <- data.frame(read_excel("Laboratorio_1/07-2018.xlsx"),fecha="2018-07-01")
jul <- jul[,-(9)] 
ago <- data.frame(read_excel("Laboratorio_1/08-2018.xlsx"),fecha="2018-08-01") 
```

    ## New names:
    ## * `` -> ...10

``` r
ago <- ago[,-(9:10)] 
sept<- data.frame(read_excel("Laboratorio_1/09-2018.xlsx"),fecha="2018-09-01")
sept <- sept[,-(9)] 
oct <- data.frame(read_excel("Laboratorio_1/10-2018.xlsx"),fecha="2018-10-01")
oct <- oct[,-(9)] 
nov <- data.frame(read_excel("Laboratorio_1/11-2018.xlsx"),fecha="2018-11-01")
nov <- nov[,-(9)] 
```

## Unir dataframes

``` r
df_final=rbind(enero, feb, marzo,abril,mayo,jun,jul,ago,sept,oct,nov)
head(df_final)
```

    ##   COD_VIAJE                                       CLIENTE UBICACION CANTIDAD
    ## 1  10000001       EL PINCHE OBELISCO / Despacho a cliente     76002     1200
    ## 2  10000002               TAQUERIA EL CHINITO |||Faltante     76002     1433
    ## 3  10000003      TIENDA LA BENDICION / Despacho a cliente     76002     1857
    ## 4  10000004                           TAQUERIA EL CHINITO     76002      339
    ## 5  10000005 CHICHARRONERIA EL RICO COLESTEROL |||Faltante     76001     1644
    ## 6  10000006                       UBIQUO LABS |||FALTANTE     76001     1827
    ##                          PILOTO      Q CREDITO        UNIDAD      fecha
    ## 1       Fernando Mariano Berrio 300.00      30 Camion Grande 2018-01-01
    ## 2        Hector Aragones Frutos 358.25      90 Camion Grande 2018-01-01
    ## 3          Pedro Alvarez Parejo 464.25      60 Camion Grande 2018-01-01
    ## 4          Angel Valdez Alegria  84.75      30         Panel 2018-01-01
    ## 5 Juan Francisco Portillo Gomez 411.00      30 Camion Grande 2018-01-01
    ## 6             Luis Jaime Urbano 456.75      30 Camion Grande 2018-01-01

## Exportar dataframe

``` r
write.csv(df_final,"df_final.csv", row.names = TRUE)
```

# Problema 2

``` r
lista=list(vect1=c(0,1,2,3,4,5,5,7,8,9), vect2=c(1,1,1,2,2,2,3,3,3), vect3=c(30,80,20,50,57,87,87,67,34))
lista
```

    ## $vect1
    ##  [1] 0 1 2 3 4 5 5 7 8 9
    ## 
    ## $vect2
    ## [1] 1 1 1 2 2 2 3 3 3
    ## 
    ## $vect3
    ## [1] 30 80 20 50 57 87 87 67 34

``` r
moda <- function(x) {
  val_unicos <- unique(x)
  val_unicos[which.max(tabulate(match(x, val_unicos)))]
}
```

``` r
lapply(lista, moda)
```

    ## $vect1
    ## [1] 5
    ## 
    ## $vect2
    ## [1] 1
    ## 
    ## $vect3
    ## [1] 87

# Problema 3

## Descargar y extraer archivos

``` r
download.file(url="https://portal.sat.gob.gt/portal/descarga/4801/analisis-estadistico-del-parque-vehicular/42399/informacion_para_analisis_estadistico_vehiculos_2019_diciembre.zip", destfile = "parque2019.zip")
```

``` r
unzip("parque2019.zip")
```

## Cargar archivo

``` r
parque2019=read_delim("INE_PARQUE_VEHICULAR_080120.txt",delim = "|")
```

    ## New names:
    ## * `` -> ...11

    ## Warning: One or more parsing issues, see `problems()` for details

    ## Rows: 2611540 Columns: 11

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: "|"
    ## chr (8): MES, NOMBRE_DEPARTAMENTO, NOMBRE_MUNICIPIO, MODELO_VEHICULO, LINEA_...
    ## dbl (2): ANIO_ALZA, CANTIDAD
    ## lgl (1): ...11

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
head(parque2019)
```

    ## # A tibble: 6 x 11
    ##   ANIO_ALZA MES   NOMBRE_DEPARTAMENTO NOMBRE_MUNICIPIO MODELO_VEHICULO
    ##       <dbl> <chr> <chr>               <chr>            <chr>          
    ## 1      2007 05    EL PROGRESO         "EL JICARO"      2007           
    ## 2      2007 05    ESCUINTLA           "SAN JOS\xc9"    2006           
    ## 3      2007 05    JUTIAPA             "MOYUTA"         2007           
    ## 4      2007 05    GUATEMALA           "FRAIJANES"      1997           
    ## 5      2007 05    QUETZALTENANGO      "QUETZALTENANGO" 2007           
    ## 6      2007 05    HUEHUETENANGO       "CUILCO"         1999           
    ## # ... with 6 more variables: LINEA_VEHICULO <chr>, TIPO_VEHICULO <chr>,
    ## #   USO_VEHICULO <chr>, MARCA_VEHICULO <chr>, CANTIDAD <dbl>, ...11 <lgl>
