---
title: aaaUse ScaleR et SparkR avec Azure HDInsight | Documents Microsoft
description: "Utiliser ScaleR et SparkR avec R Server et HDInsight"
services: hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5a76f897-02e8-4437-8f2b-4fb12225854a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: da732ff0235cf465a1452b81750c7cdd0351eed5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="combine-scaler-and-sparkr-in-hdinsight"></a>Combiner ScaleR et SparkR dans HDInsight

Cet article explique comment toopredict vol des retards d’arrivée à l’aide un **ScaleR** modèle de régression logistique à partir des données sur les retards de vol et de la météo en souscrivant **SparkR**. Ce scénario montre les fonctions hello de ScaleR pour la manipulation de données sur Spark utilisé avec Microsoft R Server pour l’analytique. combinaison de Hello de ces technologies vous permet de tooapply hello dernières fonctionnalités de traitement distribué.

Bien que les deux packages s’exécutent sur le moteur d’exécution de Hadoop Spark, ils sont bloqués depuis le partage des données en mémoire, car ils requièrent chacun leur propre session Spark respective. Jusqu'à ce que ce problème est résolu dans une prochaine version de R Server, solution de contournement hello est toomaintain sans chevauchement Spark sessions et les données tooexchange via les fichiers intermédiaires. instructions Hello ici montrent que ces exigences sont tooachieve simple.

Nous utilisons un exemple ici partagé initialement dans une conversation à couches 2016 par Mario Inchiosa et Roni Burd qui est également disponible via hello webinaire [création d’une plateforme évolutive de science des données avec R](http://event.on24.com/eventRegistration/console/EventConsoleNG.jsp?uimode=nextgeneration&eventid=1160288&sessionid=1&key=8F8FB9E2EB1AEE867287CD6757D5BD40&contenttype=A&eventuserid=305999&playerwidth=1000&playerheight=650&caller=previewLobby&text_language_id=en&format=fhaudio). exemple de hello utilise SparkR toojoin hello jeu de données du délai arrivée airlines connue avec les données météorologiques dans les aéroports de départ et d’arrivée. Hello données jointes sont ensuite utilisées en tant que modèle de régression logistique ScaleR tooa d’entrée pour la prédiction de retard des vols arrivée.

Hello nous code de procédure pas à pas a été écrit à l’origine pour le serveur R en cours d’exécution sur Spark dans un cluster HDInsight sur Azure. Mais hello concept de hello utilisation de fonctions redémarrables SparkR et ScaleR dans un script est également valide dans le contexte de hello d’environnements sur site. Dans les éléments suivants de hello, nous supposons un niveau intermédiaire des connaissances de R et R hello [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction) bibliothèque du serveur de R. Nous présentons également l’utilisation de [SparkR](https://spark.apache.org/docs/2.1.0/sparkr.html) tout au long de ce scénario.

## <a name="hello-airline-and-weather-datasets"></a>jeux de données Hello compagnie aérienne et de la météo

Hello **AirOnTime08to12CSV** airlines de jeu de données public contient des informations sur l’arrivée des vols et les détails de départ pour tous les vols commerciaux dans hello USA, à partir d’octobre 1987 tooDecember 2012. Il s’agit d’un jeu de données volumineux puisqu’il contient près de 150 millions d’enregistrements au total. Une fois décompressé, sa taille est légèrement inférieure à 4 Go. Il est disponible à partir de hello [archives du gouvernement des États-Unis](http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236). Plus facilement, il est disponible sous forme de fichier zip (AirOnTimeCSV.zip) contenant un ensemble de 303 mensuel des fichiers CSV distincts de hello [référentiel du jeu de données Revolution Analytique](http://packages.revolutionanalytics.com/datasets/AirOnTime87to12/)

toosee hello effets de la météo des retards de vol, nous devons également les données météorologiques hello à chacun de ceux des aéroports hello. Ces données peuvent être téléchargées en tant que fichiers zip sous la forme brute, par mois, de hello [référentiel National océanique et Administration atmosphérique](http://www.ncdc.noaa.gov/orders/qclcd/). Pour des raisons de hello de cet exemple, nous extraire les données météorologiques de mai 2007 – décembre 2012 et utilisé des fichiers de données hello toutes les heures dans chaque espace de toilette mensuel de hello 68. les fichiers zip mensuel Hello également contient un mappage (YYYYMMstation.txt) entre la station de météo hello ID (WBAN), qu’il est associé (cas), l’aéroport hello et hello décalage de fuseau horaire d’aéroport à l’heure UTC (fuseau horaire). Toutes ces informations sont nécessaires lors de la jointure avec les données de retard et de la météo de billet d’avion hello.

## <a name="setting-up-hello-spark-environment"></a>Configurer l’environnement de Spark hello

première étape de Hello est tooset d’environnement de Spark hello. Commençons par pointant vers le répertoire toohello qui contient nos répertoires de données d’entrée, la création d’un contexte de calcul Spark et la création d’une fonction de journalisation pour la journalisation d’information toohello console :

```
workDir        <- '~'  
myNameNode     <- 'default' 
myPort         <- 0
inputDataDir   <- 'wasb://hdfs@myAzureAcccount.blob.core.windows.net'
hdfsFS         <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

# create a persistent Spark session tooreduce startup times 
#   (remember toostop it later!)
 
sparkCC        <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort, persistentRun=TRUE)

# create working directories 

rxHadoopMakeDir('/user')
rxHadoopMakeDir('user/RevoShare')
rxHadoopMakeDir('user/RevoShare/remoteuser')

(dataDir <- '/share')
rxHadoopMakeDir(dataDir)
rxHadoopListFiles(dataDir) 

setwd(workDir)
getwd()

# version of rxRoc that runs in a local CC 
rxRoc <- function(...){
  rxSetComputeContext(RxLocalSeq())
  roc <- RevoScaleR::rxRoc(...)
  rxSetComputeContext(sparkCC)
  return(roc)
}

logmsg <- function(msg) { cat(format(Sys.time(), "%Y-%m-%d %H:%M:%S"),':',msg,'\n') } 
t0 <- proc.time() 

#..start 

logmsg('Start') 
(trackers <- system("mapred job -list-active-trackers", intern = TRUE))
logmsg(paste('Number of task nodes=',length(trackers)))
```

Ensuite, nous ajoutez chemin de recherche toohello « Spark_Home » pour les packages R afin que nous pouvons utiliser SparkR et initialiser une session SparkR :

```
#..setup for use of SparkR  

logmsg('Initialize SparkR') 

.libPaths(c(file.path(Sys.getenv("SPARK_HOME"), "R", "lib"), .libPaths()))
library(SparkR)

sparkEnvir <- list(spark.executor.instances = '10',
                   spark.yarn.executor.memoryOverhead = '8000')

sc <- sparkR.init(
  sparkEnvir = sparkEnvir,
  sparkPackages = "com.databricks:spark-csv_2.10:1.3.0"
)

sqlContext <- sparkRSQL.init(sc)
```

## <a name="preparing-hello-weather-data"></a>Préparation des données météo hello

les données météorologiques tooprepare hello, nous sous-ensemble il toohello les colonnes nécessaires pour la modélisation : 

- « Visibility »
- « DryBulbCelsius »
- « DewPointCelsius »
- « RelativeHumidity »
- « WindSpeed »
- « Altimeter »

Ensuite, ajouter un code d’aéroport associé hello météo station puis convertir hello tooUTC de l’heure locale.

Nous commençons par créer un code d’aéroport fichier toomap info hello météo station (WBAN) tooan. Nous avons pu obtenir cette corrélation à partir du fichier de mappage hello incluse avec les données météo hello. Par hello de mappage *cas* (par exemple, LAX) champ dans le fichier de données météo hello trop*origine* dans les données de billet d’avion hello. Toutefois, se trouve que nous toohave un autre mappage disponible qui mappe *WBAN* trop*AirportID* (par exemple, 12892 pour LAX) et inclut *fuseau horaire* qui a été enregistré tooa Fichier CSV appelé « wban-à-aéroport-id-tz. CSV » que nous pouvons utiliser. Par exemple :

| AirportID | WBAN | TimeZone
|-----------|------|---------
| 10685 | 54831 | -6
| 14871 | 24232 | -8
| .. | .. | ..

Hello suivant code lectures chaque des données brutes météo toutes les heures de hello colonnes de fichiers, des sous-ensembles toohello nous avons besoin, fusionne le fichier de mappage de station météorologique hello, ajuste hello dates de mesures tooUTC et écrit une nouvelle version du fichier de hello :

```
# Look up AirportID and Timezone for WBAN (weather station ID) and adjust time

adjustTime <- function(dataList)
{
  dataset0 <- as.data.frame(dataList)
  
  dataset1 <- base::merge(dataset0, wbanToAirIDAndTZDF1, by = "WBAN")

  if(nrow(dataset1) == 0) {
    dataset1 <- data.frame(
      Visibility = numeric(0),
      DryBulbCelsius = numeric(0),
      DewPointCelsius = numeric(0),
      RelativeHumidity = numeric(0),
      WindSpeed = numeric(0),
      Altimeter = numeric(0),
      AdjustedYear = numeric(0),
      AdjustedMonth = numeric(0),
      AdjustedDay = integer(0),
      AdjustedHour = integer(0),
      AirportID = integer(0)
    )
    
    return(dataset1)
  }
  
  Year <- as.integer(substr(dataset1$Date, 1, 4))
  Month <- as.integer(substr(dataset1$Date, 5, 6))
  Day <- as.integer(substr(dataset1$Date, 7, 8))
  
  Time <- dataset1$Time
  Hour <- ceiling(Time/100)
  
  Timezone <- as.integer(dataset1$TimeZone)
  
  adjustdate = as.POSIXlt(sprintf("%4d-%02d-%02d %02d:00:00", Year, Month, Day, Hour), tz = "UTC") + Timezone * 3600

  AdjustedYear = as.POSIXlt(adjustdate)$year + 1900
  AdjustedMonth = as.POSIXlt(adjustdate)$mon + 1
  AdjustedDay   = as.POSIXlt(adjustdate)$mday
  AdjustedHour  = as.POSIXlt(adjustdate)$hour
  
  AirportID = dataset1$AirportID
  Weather = dataset1[,c("Visibility", "DryBulbCelsius", "DewPointCelsius", "RelativeHumidity", "WindSpeed", "Altimeter")]
  
  data.set = data.frame(cbind(AdjustedYear, AdjustedMonth, AdjustedDay, AdjustedHour, AirportID, Weather))
  
  return(data.set)
}

wbanToAirIDAndTZDF <- read.csv("wban-to-airport-id-tz.csv")

colInfo <- list(
  WBAN = list(type="integer"),
  Date = list(type="character"),
  Time = list(type="integer"),
  Visibility = list(type="numeric"),
  DryBulbCelsius = list(type="numeric"),
  DewPointCelsius = list(type="numeric"),
  RelativeHumidity = list(type="numeric"),
  WindSpeed = list(type="numeric"),
  Altimeter = list(type="numeric")
)

weatherDF <- RxTextData(file.path(inputDataDir, "WeatherRaw"), colInfo = colInfo)

weatherDF1 <- RxTextData(file.path(inputDataDir, "Weather"), colInfo = colInfo,
                filesystem=hdfsFS)

rxSetComputeContext("localpar")
rxDataStep(weatherDF, outFile = weatherDF1, rowsPerRead = 50000, overwrite = T,
           transformFunc = adjustTime,
           transformObjects = list(wbanToAirIDAndTZDF1 = wbanToAirIDAndTZDF))
```

## <a name="importing-hello-airline-and-weather-data-toospark-dataframes"></a>L’importation de données de billet d’avion et de la météo hello tooSpark trames de données

Maintenant, nous utilisons hello SparkR [read.df()](https://docs.databricks.com/spark/latest/sparkr/functions/read.df.html) tooimport hello météo et compagnie aérienne données tooSpark trames de données de la fonction. Cette fonction, comme beaucoup d’autres méthodes Spark, est exécutée en différé, ce qui signifie qu’elle est placée en file d’attente en vue de l’exécution, mais qu’elle n’est exécutée que lorsque cela est nécessaire.

```
airPath     <- file.path(inputDataDir, "AirOnTime08to12CSV")
weatherPath <- file.path(inputDataDir, "Weather") # pre-processed weather data
rxHadoopListFiles(airPath) 
rxHadoopListFiles(weatherPath) 

# create a SparkR DataFrame for hello airline data

logmsg('create a SparkR DataFrame for hello airline data') 
# use inferSchema = "false" for more robust parsing
airDF <- read.df(sqlContext, airPath, source = "com.databricks.spark.csv", 
                 header = "true", inferSchema = "false")

# Create a SparkR DataFrame for hello weather data

logmsg('create a SparkR DataFrame for hello weather data') 
weatherDF <- read.df(sqlContext, weatherPath, source = "com.databricks.spark.csv", 
                     header = "true", inferSchema = "true")
```

## <a name="data-cleansing-and-transformation"></a>Nettoyage et transformation des données

Ensuite, nous faisons un nettoyage des données de billet d’avion hello, nous avons importé les colonnes toorename. Nous uniquement conserver des variables hello nécessités et arrondir les heures planifiées de départ vers le bas toohello le plus proche tooenable heures la fusion avec les données les plus récentes météo hello au départ :

```
logmsg('clean hello airline data') 
airDF <- rename(airDF,
                ArrDel15 = airDF$ARR_DEL15,
                Year = airDF$YEAR,
                Month = airDF$MONTH,
                DayofMonth = airDF$DAY_OF_MONTH,
                DayOfWeek = airDF$DAY_OF_WEEK,
                Carrier = airDF$UNIQUE_CARRIER,
                OriginAirportID = airDF$ORIGIN_AIRPORT_ID,
                DestAirportID = airDF$DEST_AIRPORT_ID,
                CRSDepTime = airDF$CRS_DEP_TIME,
                CRSArrTime =  airDF$CRS_ARR_TIME
)

# Select desired columns from hello flight data. 
varsToKeep <- c("ArrDel15", "Year", "Month", "DayofMonth", "DayOfWeek", "Carrier", "OriginAirportID", "DestAirportID", "CRSDepTime", "CRSArrTime")
airDF <- select(airDF, varsToKeep)

# Apply schema
coltypes(airDF) <- c("character", "integer", "integer", "integer", "integer", "character", "integer", "integer", "integer", "integer")

# Round down scheduled departure time toofull hour.
airDF$CRSDepTime <- floor(airDF$CRSDepTime / 100)
```

Maintenant, nous effectuer des opérations similaires sur les données météorologiques hello :

```
# Average weather readings by hour
logmsg('clean hello weather data') 
weatherDF <- agg(groupBy(weatherDF, "AdjustedYear", "AdjustedMonth", "AdjustedDay", "AdjustedHour", "AirportID"), Visibility="avg",
                  DryBulbCelsius="avg", DewPointCelsius="avg", RelativeHumidity="avg", WindSpeed="avg", Altimeter="avg"
                  )

weatherDF <- rename(weatherDF,
                    Visibility = weatherDF$'avg(Visibility)',
                    DryBulbCelsius = weatherDF$'avg(DryBulbCelsius)',
                    DewPointCelsius = weatherDF$'avg(DewPointCelsius)',
                    RelativeHumidity = weatherDF$'avg(RelativeHumidity)',
                    WindSpeed = weatherDF$'avg(WindSpeed)',
                    Altimeter = weatherDF$'avg(Altimeter)'
)
```

## <a name="joining-hello-weather-and-airline-data"></a>Jointure de données météo et compagnie aérienne de hello

Nous utilisons désormais hello SparkR [join()](https://docs.databricks.com/spark/latest/sparkr/functions/join.html) toodo une jointure externe gauche de données de compagnie aérienne et de la météo hello par AirportID de départ et de date/heure de la fonction. jointure externe de Hello permet tooretain toutes les données de billet d’avion hello enregistre même s’il n’existe pas de données météo correspondantes. Suivant la jointure de hello, nous supprime certaines colonnes redondantes et renommer hello conservé tooremove hello entrants trame de données préfixe de colonne introduit par la jointure de hello.

```
logmsg('Join airline data with weather at Origin Airport')
joinedDF <- SparkR::join(
  airDF,
  weatherDF,
  airDF$OriginAirportID == weatherDF$AirportID &
    airDF$Year == weatherDF$AdjustedYear &
    airDF$Month == weatherDF$AdjustedMonth &
    airDF$DayofMonth == weatherDF$AdjustedDay &
    airDF$CRSDepTime == weatherDF$AdjustedHour,
  joinType = "left_outer"
)

# Remove redundant columns
vars <- names(joinedDF)
varsToDrop <- c('AdjustedYear', 'AdjustedMonth', 'AdjustedDay', 'AdjustedHour', 'AirportID')
varsToKeep <- vars[!(vars %in% varsToDrop)]
joinedDF1 <- select(joinedDF, varsToKeep)

joinedDF2 <- rename(joinedDF1,
                    VisibilityOrigin = joinedDF1$Visibility,
                    DryBulbCelsiusOrigin = joinedDF1$DryBulbCelsius,
                    DewPointCelsiusOrigin = joinedDF1$DewPointCelsius,
                    RelativeHumidityOrigin = joinedDF1$RelativeHumidity,
                    WindSpeedOrigin = joinedDF1$WindSpeed,
                    AltimeterOrigin = joinedDF1$Altimeter
)
```

De la même manière, nous joindre des données météo et compagnie aérienne hello, en fonction de l’arrivée AirportID et datetime :

```
logmsg('Join airline data with weather at Destination Airport')
joinedDF3 <- SparkR::join(
  joinedDF2,
  weatherDF,
  airDF$DestAirportID == weatherDF$AirportID &
    airDF$Year == weatherDF$AdjustedYear &
    airDF$Month == weatherDF$AdjustedMonth &
    airDF$DayofMonth == weatherDF$AdjustedDay &
    airDF$CRSDepTime == weatherDF$AdjustedHour,
  joinType = "left_outer"
)

# Remove redundant columns
vars <- names(joinedDF3)
varsToDrop <- c('AdjustedYear', 'AdjustedMonth', 'AdjustedDay', 'AdjustedHour', 'AirportID')
varsToKeep <- vars[!(vars %in% varsToDrop)]
joinedDF4 <- select(joinedDF3, varsToKeep)

joinedDF5 <- rename(joinedDF4,
                    VisibilityDest = joinedDF4$Visibility,
                    DryBulbCelsiusDest = joinedDF4$DryBulbCelsius,
                    DewPointCelsiusDest = joinedDF4$DewPointCelsius,
                    RelativeHumidityDest = joinedDF4$RelativeHumidity,
                    WindSpeedDest = joinedDF4$WindSpeed,
                    AltimeterDest = joinedDF4$Altimeter
                    )
```

## <a name="save-results-toocsv-for-exchange-with-scaler"></a>Enregistrer les tooCSV de résultats pour l’échange avec ScaleR

Jointures hello nous devons toodo avec SparkR se termine. Nous enregistrer les données de hello hello final Spark de trame de données « joinedDF5 » tooa CSV pour tooScaleR d’entrée et que vous fermez puis session SparkR de hello. Nous dire explicitement à SparkR toosave hello CSV résultant dans des partitions distinctes 80 tooenable suffisamment du parallélisme dans le traitement de ScaleR :

```
logmsg('output hello joined data from Spark tooCSV') 
joinedDF5 <- repartition(joinedDF5, 80) # write.df below will produce this many CSVs

# write result toodirectory of CSVs
write.df(joinedDF5, file.path(dataDir, "joined5Csv"), "com.databricks.spark.csv", "overwrite", header = "true")

# We can shut down hello SparkR Spark context now
sparkR.stop()

# remove non-data files
rxHadoopRemove(file.path(dataDir, "joined5Csv/_SUCCESS"))
```

## <a name="import-tooxdf-for-use-by-scaler"></a>TooXDF d’importation pour une utilisation par ScaleR

Nous pouvons utiliser le fichier CSV de hello de billet d’avion jointe et les données météorologiques en tant que-est pour la modélisation via une source de données de texte ScaleR. Mais nous importez-le tooXDF en premier lieu, car il est plus efficace lors de l’exécution de plusieurs opérations sur le jeu de données hello :

```
logmsg('Import hello CSV toocompressed, binary XDF format') 

# set hello Spark compute context for R Server 
rxSetComputeContext(sparkCC)
rxGetComputeContext()

colInfo <- list(
  ArrDel15 = list(type="numeric"),
  Year = list(type="factor"),
  Month = list(type="factor"),
  DayofMonth = list(type="factor"),
  DayOfWeek = list(type="factor"),
  Carrier = list(type="factor"),
  OriginAirportID = list(type="factor"),
  DestAirportID = list(type="factor"),
  RelativeHumidityOrigin = list(type="numeric"),
  AltimeterOrigin = list(type="numeric"),
  DryBulbCelsiusOrigin = list(type="numeric"),
  WindSpeedOrigin = list(type="numeric"),
  VisibilityOrigin = list(type="numeric"),
  DewPointCelsiusOrigin = list(type="numeric"),
  RelativeHumidityDest = list(type="numeric"),
  AltimeterDest = list(type="numeric"),
  DryBulbCelsiusDest = list(type="numeric"),
  WindSpeedDest = list(type="numeric"),
  VisibilityDest = list(type="numeric"),
  DewPointCelsiusDest = list(type="numeric")
)

joinedDF5Txt <- RxTextData(file.path(dataDir, "joined5Csv"),
                           colInfo = colInfo, fileSystem = hdfsFS)
rxGetInfo(joinedDF5Txt) 

destData <- RxXdfData(file.path(dataDir, "joined5XDF"), fileSystem = hdfsFS)

rxImport(inData = joinedDF5Txt, destData, overwrite = TRUE)

rxGetInfo(destData, getVarInfo = T)

# File name: /user/RevoShare/dev/delayDataLarge/joined5XDF 
# Number of composite data files: 80 
# Number of observations: 148619655 
# Number of variables: 22 
# Number of blocks: 320 
# Compression type: zlib 
# Variable information: 
#   Var 1: ArrDel15, Type: numeric, Low/High: (0.0000, 1.0000)
# Var 2: Year
# 26 factor levels: 1987 1988 1989 1990 1991 ... 2008 2009 2010 2011 2012
# Var 3: Month
# 12 factor levels: 10 11 12 1 2 ... 5 6 7 8 9
# Var 4: DayofMonth
# 31 factor levels: 1 3 4 5 7 ... 29 30 2 18 31
# Var 5: DayOfWeek
# 7 factor levels: 4 6 7 1 3 2 5
# Var 6: Carrier
# 30 factor levels: PI UA US AA DL ... HA F9 YV 9E VX
# Var 7: OriginAirportID
# 374 factor levels: 15249 12264 11042 15412 13930 ... 13341 10559 14314 11711 10558
# Var 8: DestAirportID
# 378 factor levels: 13303 14492 10721 11057 13198 ... 14802 11711 11931 12899 10559
# Var 9: CRSDepTime, Type: integer, Low/High: (0, 24)
# Var 10: CRSArrTime, Type: integer, Low/High: (0, 2400)
# Var 11: RelativeHumidityOrigin, Type: numeric, Low/High: (0.0000, 100.0000)
# Var 12: AltimeterOrigin, Type: numeric, Low/High: (28.1700, 31.1600)
# Var 13: DryBulbCelsiusOrigin, Type: numeric, Low/High: (-46.1000, 47.8000)
# Var 14: WindSpeedOrigin, Type: numeric, Low/High: (0.0000, 81.0000)
# Var 15: VisibilityOrigin, Type: numeric, Low/High: (0.0000, 90.0000)
# Var 16: DewPointCelsiusOrigin, Type: numeric, Low/High: (-41.7000, 29.0000)
# Var 17: RelativeHumidityDest, Type: numeric, Low/High: (0.0000, 100.0000)
# Var 18: AltimeterDest, Type: numeric, Low/High: (28.1700, 31.1600)
# Var 19: DryBulbCelsiusDest, Type: numeric, Low/High: (-46.1000, 53.9000)
# Var 20: WindSpeedDest, Type: numeric, Low/High: (0.0000, 136.0000)
# Var 21: VisibilityDest, Type: numeric, Low/High: (0.0000, 88.0000)
# Var 22: DewPointCelsiusDest, Type: numeric, Low/High: (-43.0000, 29.0000)

finalData <- RxXdfData(file.path(dataDir, "joined5XDF"), fileSystem = hdfsFS)

```

## <a name="splitting-data-for-training-and-test"></a>Fractionnement des données pour le test et l’apprentissage

Nous utiliser toosplit rxDataStep les données de 2012 hello pour le test et conserver reste hello pour l’apprentissage :

```
# split out hello training data

logmsg('split out training data as all data except year 2012')
trainDS <- RxXdfData( file.path(dataDir, "finalDataTrain" ),fileSystem = hdfsFS)

rxDataStep( inData = finalData, outFile = trainDS,
            rowSelection = ( Year != 2012 ), overwrite = T )

# split out hello testing data

logmsg('split out hello test data for year 2012') 
testDS <- RxXdfData( file.path(dataDir, "finalDataTest" ), fileSystem = hdfsFS)

rxDataStep( inData = finalData, outFile = testDS,
            rowSelection = ( Year == 2012 ), overwrite = T )

rxGetInfo(trainDS)
rxGetInfo(testDS)
```

## <a name="train-and-test-a-logistic-regression-model"></a>Effectuer l’apprentissage et tester un modèle de régression logistique

Vous êtes désormais prêt toobuild un modèle. toosee hello influence des données météorologiques de délai dans l’heure d’arrivée hello, nous utilisons routine de régression logistique de ScaleR. Nous utilisons il toomodel si un délai de l’arrivée de plus de 15 minutes est influencé par météo hello dans les aéroports de départ et d’arrivée hello :

```
logmsg('train a logistic regression model for Arrival Delay > 15 minutes') 
formula <- as.formula(ArrDel15 ~ Year + Month + DayofMonth + DayOfWeek + Carrier +
                     OriginAirportID + DestAirportID + CRSDepTime + CRSArrTime + 
                     RelativeHumidityOrigin + AltimeterOrigin + DryBulbCelsiusOrigin +
                     WindSpeedOrigin + VisibilityOrigin + DewPointCelsiusOrigin + 
                     RelativeHumidityDest + AltimeterDest + DryBulbCelsiusDest +
                     WindSpeedDest + VisibilityDest + DewPointCelsiusDest
                   )

# Use hello scalable rxLogit() function but set max iterations too3 for hello purposes of 
# this exercise 

logitModel <- rxLogit(formula, data = trainDS, maxIterations = 3)

base::summary(logitModel)
```

Maintenant nous allons voir comment il sur hello teste données en effectuant des prédictions examinant ROC et AUC.

```
# Predict over test data (Logistic Regression).

logmsg('predict over hello test data') 
logitPredict <- RxXdfData(file.path(dataDir, "logitPredict"), fileSystem = hdfsFS)

# Use hello scalable rxPredict() function

rxPredict(logitModel, data = testDS, outData = logitPredict,
          extraVarsToWrite = c("ArrDel15"), 
          type = 'response', overwrite = TRUE)

# Calculate ROC and Area Under hello Curve (AUC).

logmsg('calculate hello roc and auc') 
logitRoc <- rxRoc("ArrDel15", "ArrDel15_Pred", logitPredict)
logitAuc <- rxAuc(logitRoc)
head(logitAuc)
logitAuc

plot(logitRoc)
```

## <a name="scoring-elsewhere"></a>Notation depuis un autre emplacement

Nous pouvons également utiliser le modèle de hello pour le calcul de score des données sur une autre plateforme. En enregistrant le fichier des services Bureau à distance tooan transfert et l’importation de ce services Bureau à distance dans une environnement tel que SQL Server R Services de calcul de score de destination. Il est important tooensure niveaux hello des facteurs de hello toobe de données au score calculé correspondant à celles sur quel hello modèle a été créé. Que correspondance peut être obtenue en extrayant et enregistrer les informations de colonne hello associé hello modélisation des données par le biais de ScaleR `rxCreateColInfo()` (fonction), puis en appliquant cette source de données d’entrée de colonne informations toohello pour la prédiction. Suivant de hello nous enregistrer quelques lignes du jeu de données de test hello et extraire et utilisez hello les informations de colonne à partir de cet exemple de script de prédiction hello :

```
# save hello model and a sample of hello test dataset 

logmsg('save serialized version of hello model and a sample of hello test data')
rxSetComputeContext('localpar') 
saveRDS(logitModel, file = "logitModel.rds")
testDF <- head(testDS, 1000)  
saveRDS(testDF    , file = "testDF.rds"    )
list.files()

rxHadoopListFiles(file.path(inputDataDir,''))
rxHadoopListFiles(dataDir)

# stop hello spark engine 
rxStopEngine(sparkCC) 

logmsg('Done.')
elapsed <- (proc.time() - t0)[3]
logmsg(paste('Elapsed time=',sprintf('%6.2f',elapsed),'(sec)\n\n'))
```

## <a name="summary"></a>Résumé

Dans cet article, nous avons montré comment il est possible toocombine de SparkR pour la manipulation de données avec ScaleR pour le développement de modèles dans Hadoop Spark. Ce scénario nécessite de maintenir les sessions de Spark séparées, en n’exécutant qu’une session à la fois et d’échanger des données via des fichiers CSV. Bien que simple, ce processus est largement simplifié dans une prochaine version de R Server, lorsque SparkR et ScaleR peuvent partager une session Spark et, par conséquent, Spark DataFrames.

## <a name="next-steps-and-more-information"></a>Étapes suivantes et informations supplémentaires

- Pour plus d’informations sur l’utilisation du serveur de R sur Spark, consultez hello [guide Mise en route sur MSDN](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started)

- Pour obtenir des informations générales sur le serveur R, consultez hello [prise en main R](https://msdn.microsoft.com/microsoft-r/microsoft-r-get-started-node) l’article.

- Pour plus d’informations sur R Server sur HDInsight, consultez [Présentation de R Server sur Azure HDInsight](hdinsight-hadoop-r-server-overview.md) et [R Server sur Azure HDInsight](hdinsight-hadoop-r-server-get-started.md).

Pour plus d’informations sur l’utilisation de SparkR, consultez les pages suivantes :

- [Document Apache SparkR](https://spark.apache.org/docs/2.1.0/sparkr.html)

- [Vue d’ensemble de SparkR](https://docs.databricks.com/spark/latest/sparkr/overview.html) à partir de Databricks
