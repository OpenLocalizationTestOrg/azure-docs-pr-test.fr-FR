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
# <a name="combine-scaler-and-sparkr-in-hdinsight"></a><span data-ttu-id="47fd0-103">Combiner ScaleR et SparkR dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="47fd0-103">Combine ScaleR and SparkR in HDInsight</span></span>

<span data-ttu-id="47fd0-104">Cet article explique comment toopredict vol des retards d’arrivée à l’aide un **ScaleR** modèle de régression logistique à partir des données sur les retards de vol et de la météo en souscrivant **SparkR**.</span><span class="sxs-lookup"><span data-stu-id="47fd0-104">This article shows how toopredict flight arrival delays using a **ScaleR** logistic regression model from data on flight delays and weather joined with **SparkR**.</span></span> <span data-ttu-id="47fd0-105">Ce scénario montre les fonctions hello de ScaleR pour la manipulation de données sur Spark utilisé avec Microsoft R Server pour l’analytique.</span><span class="sxs-lookup"><span data-stu-id="47fd0-105">This scenario demonstrates hello capabilities of ScaleR for data manipulation on Spark used with Microsoft R Server for analytics.</span></span> <span data-ttu-id="47fd0-106">combinaison de Hello de ces technologies vous permet de tooapply hello dernières fonctionnalités de traitement distribué.</span><span class="sxs-lookup"><span data-stu-id="47fd0-106">hello combination of these technologies enables you tooapply hello latest capabilities in distributed processing.</span></span>

<span data-ttu-id="47fd0-107">Bien que les deux packages s’exécutent sur le moteur d’exécution de Hadoop Spark, ils sont bloqués depuis le partage des données en mémoire, car ils requièrent chacun leur propre session Spark respective.</span><span class="sxs-lookup"><span data-stu-id="47fd0-107">Although both packages run on Hadoop’s Spark execution engine, they are blocked from in-memory data sharing as they each require their own respective Spark sessions.</span></span> <span data-ttu-id="47fd0-108">Jusqu'à ce que ce problème est résolu dans une prochaine version de R Server, solution de contournement hello est toomaintain sans chevauchement Spark sessions et les données tooexchange via les fichiers intermédiaires.</span><span class="sxs-lookup"><span data-stu-id="47fd0-108">Until this issue is addressed in an upcoming version of R Server, hello workaround is toomaintain non-overlapping Spark sessions, and tooexchange data through intermediate files.</span></span> <span data-ttu-id="47fd0-109">instructions Hello ici montrent que ces exigences sont tooachieve simple.</span><span class="sxs-lookup"><span data-stu-id="47fd0-109">hello instructions here show that these requirements are straightforward tooachieve.</span></span>

<span data-ttu-id="47fd0-110">Nous utilisons un exemple ici partagé initialement dans une conversation à couches 2016 par Mario Inchiosa et Roni Burd qui est également disponible via hello webinaire [création d’une plateforme évolutive de science des données avec R](http://event.on24.com/eventRegistration/console/EventConsoleNG.jsp?uimode=nextgeneration&eventid=1160288&sessionid=1&key=8F8FB9E2EB1AEE867287CD6757D5BD40&contenttype=A&eventuserid=305999&playerwidth=1000&playerheight=650&caller=previewLobby&text_language_id=en&format=fhaudio). exemple de hello utilise SparkR toojoin hello jeu de données du délai arrivée airlines connue avec les données météorologiques dans les aéroports de départ et d’arrivée.</span><span class="sxs-lookup"><span data-stu-id="47fd0-110">We use an example here initially shared in a talk at Strata 2016 by Mario Inchiosa and Roni Burd that is also available through hello webinar [Building a Scalable Data Science Platform with R](http://event.on24.com/eventRegistration/console/EventConsoleNG.jsp?uimode=nextgeneration&eventid=1160288&sessionid=1&key=8F8FB9E2EB1AEE867287CD6757D5BD40&contenttype=A&eventuserid=305999&playerwidth=1000&playerheight=650&caller=previewLobby&text_language_id=en&format=fhaudio). hello example uses SparkR toojoin hello well-known airlines arrival delay data set with weather data at departure and arrival airports.</span></span> <span data-ttu-id="47fd0-111">Hello données jointes sont ensuite utilisées en tant que modèle de régression logistique ScaleR tooa d’entrée pour la prédiction de retard des vols arrivée.</span><span class="sxs-lookup"><span data-stu-id="47fd0-111">hello data joined is then used as input tooa ScaleR logistic regression model for predicting flight arrival delay.</span></span>

<span data-ttu-id="47fd0-112">Hello nous code de procédure pas à pas a été écrit à l’origine pour le serveur R en cours d’exécution sur Spark dans un cluster HDInsight sur Azure.</span><span class="sxs-lookup"><span data-stu-id="47fd0-112">hello code we walkthrough was originally written for R Server running on Spark in an HDInsight cluster on Azure.</span></span> <span data-ttu-id="47fd0-113">Mais hello concept de hello utilisation de fonctions redémarrables SparkR et ScaleR dans un script est également valide dans le contexte de hello d’environnements sur site.</span><span class="sxs-lookup"><span data-stu-id="47fd0-113">But hello concept of mixing hello use of SparkR and ScaleR in one script is also valid in hello context of on-premises environments.</span></span> <span data-ttu-id="47fd0-114">Dans les éléments suivants de hello, nous supposons un niveau intermédiaire des connaissances de R et R hello [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction) bibliothèque du serveur de R.</span><span class="sxs-lookup"><span data-stu-id="47fd0-114">In hello following, we presume an intermediate level of knowledge of R and R hello [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction) library of R Server.</span></span> <span data-ttu-id="47fd0-115">Nous présentons également l’utilisation de [SparkR](https://spark.apache.org/docs/2.1.0/sparkr.html) tout au long de ce scénario.</span><span class="sxs-lookup"><span data-stu-id="47fd0-115">We also introduce use of [SparkR](https://spark.apache.org/docs/2.1.0/sparkr.html) while walking through this scenario.</span></span>

## <a name="hello-airline-and-weather-datasets"></a><span data-ttu-id="47fd0-116">jeux de données Hello compagnie aérienne et de la météo</span><span class="sxs-lookup"><span data-stu-id="47fd0-116">hello airline and weather datasets</span></span>

<span data-ttu-id="47fd0-117">Hello **AirOnTime08to12CSV** airlines de jeu de données public contient des informations sur l’arrivée des vols et les détails de départ pour tous les vols commerciaux dans hello USA, à partir d’octobre 1987 tooDecember 2012.</span><span class="sxs-lookup"><span data-stu-id="47fd0-117">hello **AirOnTime08to12CSV** airlines public dataset contains information on flight arrival and departure details for all commercial flights within hello USA, from October 1987 tooDecember 2012.</span></span> <span data-ttu-id="47fd0-118">Il s’agit d’un jeu de données volumineux puisqu’il contient près de 150 millions d’enregistrements au total.</span><span class="sxs-lookup"><span data-stu-id="47fd0-118">This is a large dataset: there are nearly 150 million records in total.</span></span> <span data-ttu-id="47fd0-119">Une fois décompressé, sa taille est légèrement inférieure à 4 Go.</span><span class="sxs-lookup"><span data-stu-id="47fd0-119">It is just under 4 GB unpacked.</span></span> <span data-ttu-id="47fd0-120">Il est disponible à partir de hello [archives du gouvernement des États-Unis](http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236).</span><span class="sxs-lookup"><span data-stu-id="47fd0-120">It is available from hello [U.S. government archives](http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236).</span></span> <span data-ttu-id="47fd0-121">Plus facilement, il est disponible sous forme de fichier zip (AirOnTimeCSV.zip) contenant un ensemble de 303 mensuel des fichiers CSV distincts de hello [référentiel du jeu de données Revolution Analytique](http://packages.revolutionanalytics.com/datasets/AirOnTime87to12/)</span><span class="sxs-lookup"><span data-stu-id="47fd0-121">More conveniently, it is available as a zip file (AirOnTimeCSV.zip) containing a set of 303 separate monthly CSV files from hello [Revolution Analytics dataset repository](http://packages.revolutionanalytics.com/datasets/AirOnTime87to12/)</span></span>

<span data-ttu-id="47fd0-122">toosee hello effets de la météo des retards de vol, nous devons également les données météorologiques hello à chacun de ceux des aéroports hello.</span><span class="sxs-lookup"><span data-stu-id="47fd0-122">toosee hello effects of weather on flight delays, we also need hello weather data at each of hello airports.</span></span> <span data-ttu-id="47fd0-123">Ces données peuvent être téléchargées en tant que fichiers zip sous la forme brute, par mois, de hello [référentiel National océanique et Administration atmosphérique](http://www.ncdc.noaa.gov/orders/qclcd/).</span><span class="sxs-lookup"><span data-stu-id="47fd0-123">This data can be downloaded as zip files in raw form, by month, from hello [National Oceanic and Atmospheric Administration repository](http://www.ncdc.noaa.gov/orders/qclcd/).</span></span> <span data-ttu-id="47fd0-124">Pour des raisons de hello de cet exemple, nous extraire les données météorologiques de mai 2007 – décembre 2012 et utilisé des fichiers de données hello toutes les heures dans chaque espace de toilette mensuel de hello 68.</span><span class="sxs-lookup"><span data-stu-id="47fd0-124">For hello purposes of this example, we pull weather data from May 2007 – December 2012 and used hello hourly data files within each of hello 68 monthly zips.</span></span> <span data-ttu-id="47fd0-125">les fichiers zip mensuel Hello également contient un mappage (YYYYMMstation.txt) entre la station de météo hello ID (WBAN), qu’il est associé (cas), l’aéroport hello et hello décalage de fuseau horaire d’aéroport à l’heure UTC (fuseau horaire).</span><span class="sxs-lookup"><span data-stu-id="47fd0-125">hello monthly zip files also contain a mapping (YYYYMMstation.txt) between hello weather station ID (WBAN), hello airport that it is associated with (CallSign), and hello airport’s time zone offset from UTC (TimeZone).</span></span> <span data-ttu-id="47fd0-126">Toutes ces informations sont nécessaires lors de la jointure avec les données de retard et de la météo de billet d’avion hello.</span><span class="sxs-lookup"><span data-stu-id="47fd0-126">All of this information is needed when joining with hello airline delay and weather data.</span></span>

## <a name="setting-up-hello-spark-environment"></a><span data-ttu-id="47fd0-127">Configurer l’environnement de Spark hello</span><span class="sxs-lookup"><span data-stu-id="47fd0-127">Setting up hello Spark environment</span></span>

<span data-ttu-id="47fd0-128">première étape de Hello est tooset d’environnement de Spark hello.</span><span class="sxs-lookup"><span data-stu-id="47fd0-128">hello first step is tooset up hello Spark environment.</span></span> <span data-ttu-id="47fd0-129">Commençons par pointant vers le répertoire toohello qui contient nos répertoires de données d’entrée, la création d’un contexte de calcul Spark et la création d’une fonction de journalisation pour la journalisation d’information toohello console :</span><span class="sxs-lookup"><span data-stu-id="47fd0-129">We begin by pointing toohello directory that contains our input data directories, creating a Spark compute context, and creating a logging function for informational logging toohello console:</span></span>

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

<span data-ttu-id="47fd0-130">Ensuite, nous ajoutez chemin de recherche toohello « Spark_Home » pour les packages R afin que nous pouvons utiliser SparkR et initialiser une session SparkR :</span><span class="sxs-lookup"><span data-stu-id="47fd0-130">Next we add “Spark_Home” toohello search path for R packages so that we can use SparkR, and initialize a SparkR session:</span></span>

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

## <a name="preparing-hello-weather-data"></a><span data-ttu-id="47fd0-131">Préparation des données météo hello</span><span class="sxs-lookup"><span data-stu-id="47fd0-131">Preparing hello weather data</span></span>

<span data-ttu-id="47fd0-132">les données météorologiques tooprepare hello, nous sous-ensemble il toohello les colonnes nécessaires pour la modélisation :</span><span class="sxs-lookup"><span data-stu-id="47fd0-132">tooprepare hello weather data, we subset it toohello columns needed for modeling:</span></span> 

- <span data-ttu-id="47fd0-133">« Visibility »</span><span class="sxs-lookup"><span data-stu-id="47fd0-133">"Visibility"</span></span>
- <span data-ttu-id="47fd0-134">« DryBulbCelsius »</span><span class="sxs-lookup"><span data-stu-id="47fd0-134">"DryBulbCelsius"</span></span>
- <span data-ttu-id="47fd0-135">« DewPointCelsius »</span><span class="sxs-lookup"><span data-stu-id="47fd0-135">"DewPointCelsius"</span></span>
- <span data-ttu-id="47fd0-136">« RelativeHumidity »</span><span class="sxs-lookup"><span data-stu-id="47fd0-136">"RelativeHumidity"</span></span>
- <span data-ttu-id="47fd0-137">« WindSpeed »</span><span class="sxs-lookup"><span data-stu-id="47fd0-137">"WindSpeed"</span></span>
- <span data-ttu-id="47fd0-138">« Altimeter »</span><span class="sxs-lookup"><span data-stu-id="47fd0-138">"Altimeter"</span></span>

<span data-ttu-id="47fd0-139">Ensuite, ajouter un code d’aéroport associé hello météo station puis convertir hello tooUTC de l’heure locale.</span><span class="sxs-lookup"><span data-stu-id="47fd0-139">Then we add an airport code associated with hello weather station and convert hello measurements from local time tooUTC.</span></span>

<span data-ttu-id="47fd0-140">Nous commençons par créer un code d’aéroport fichier toomap info hello météo station (WBAN) tooan.</span><span class="sxs-lookup"><span data-stu-id="47fd0-140">We begin by creating a file toomap hello weather station (WBAN) info tooan airport code.</span></span> <span data-ttu-id="47fd0-141">Nous avons pu obtenir cette corrélation à partir du fichier de mappage hello incluse avec les données météo hello.</span><span class="sxs-lookup"><span data-stu-id="47fd0-141">We could get this correlation from hello mapping file included with hello weather data.</span></span> <span data-ttu-id="47fd0-142">Par hello de mappage *cas* (par exemple, LAX) champ dans le fichier de données météo hello trop*origine* dans les données de billet d’avion hello.</span><span class="sxs-lookup"><span data-stu-id="47fd0-142">By mapping hello *CallSign* (for example, LAX) field in hello weather data file too*Origin* in hello airline data.</span></span> <span data-ttu-id="47fd0-143">Toutefois, se trouve que nous toohave un autre mappage disponible qui mappe *WBAN* trop*AirportID* (par exemple, 12892 pour LAX) et inclut *fuseau horaire* qui a été enregistré tooa Fichier CSV appelé « wban-à-aéroport-id-tz. CSV » que nous pouvons utiliser.</span><span class="sxs-lookup"><span data-stu-id="47fd0-143">However, we just happened toohave another mapping on hand that maps *WBAN* too*AirportID* (for example, 12892 for LAX) and includes *TimeZone* that has been saved tooa CSV file called “wban-to-airport-id-tz.CSV” that we can use.</span></span> <span data-ttu-id="47fd0-144">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="47fd0-144">For example:</span></span>

| <span data-ttu-id="47fd0-145">AirportID</span><span class="sxs-lookup"><span data-stu-id="47fd0-145">AirportID</span></span> | <span data-ttu-id="47fd0-146">WBAN</span><span class="sxs-lookup"><span data-stu-id="47fd0-146">WBAN</span></span> | <span data-ttu-id="47fd0-147">TimeZone</span><span class="sxs-lookup"><span data-stu-id="47fd0-147">TimeZone</span></span>
|-----------|------|---------
| <span data-ttu-id="47fd0-148">10685</span><span class="sxs-lookup"><span data-stu-id="47fd0-148">10685</span></span> | <span data-ttu-id="47fd0-149">54831</span><span class="sxs-lookup"><span data-stu-id="47fd0-149">54831</span></span> | <span data-ttu-id="47fd0-150">-6</span><span class="sxs-lookup"><span data-stu-id="47fd0-150">-6</span></span>
| <span data-ttu-id="47fd0-151">14871</span><span class="sxs-lookup"><span data-stu-id="47fd0-151">14871</span></span> | <span data-ttu-id="47fd0-152">24232</span><span class="sxs-lookup"><span data-stu-id="47fd0-152">24232</span></span> | <span data-ttu-id="47fd0-153">-8</span><span class="sxs-lookup"><span data-stu-id="47fd0-153">-8</span></span>
| <span data-ttu-id="47fd0-154">..</span><span class="sxs-lookup"><span data-stu-id="47fd0-154">..</span></span> | <span data-ttu-id="47fd0-155">..</span><span class="sxs-lookup"><span data-stu-id="47fd0-155">..</span></span> | <span data-ttu-id="47fd0-156">..</span><span class="sxs-lookup"><span data-stu-id="47fd0-156">..</span></span>

<span data-ttu-id="47fd0-157">Hello suivant code lectures chaque des données brutes météo toutes les heures de hello colonnes de fichiers, des sous-ensembles toohello nous avons besoin, fusionne le fichier de mappage de station météorologique hello, ajuste hello dates de mesures tooUTC et écrit une nouvelle version du fichier de hello :</span><span class="sxs-lookup"><span data-stu-id="47fd0-157">hello following code reads each of hello hourly raw weather data files, subsets toohello columns we need, merges hello weather station mapping file, adjusts hello date times of measurements tooUTC, and then writes out a new version of hello file:</span></span>

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

## <a name="importing-hello-airline-and-weather-data-toospark-dataframes"></a><span data-ttu-id="47fd0-158">L’importation de données de billet d’avion et de la météo hello tooSpark trames de données</span><span class="sxs-lookup"><span data-stu-id="47fd0-158">Importing hello airline and weather data tooSpark DataFrames</span></span>

<span data-ttu-id="47fd0-159">Maintenant, nous utilisons hello SparkR [read.df()](https://docs.databricks.com/spark/latest/sparkr/functions/read.df.html) tooimport hello météo et compagnie aérienne données tooSpark trames de données de la fonction.</span><span class="sxs-lookup"><span data-stu-id="47fd0-159">Now we use hello SparkR [read.df()](https://docs.databricks.com/spark/latest/sparkr/functions/read.df.html) function tooimport hello weather and airline data tooSpark DataFrames.</span></span> <span data-ttu-id="47fd0-160">Cette fonction, comme beaucoup d’autres méthodes Spark, est exécutée en différé, ce qui signifie qu’elle est placée en file d’attente en vue de l’exécution, mais qu’elle n’est exécutée que lorsque cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="47fd0-160">This function, like many other Spark methods, are executed lazily, meaning that they are queued for execution but not executed until required.</span></span>

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

## <a name="data-cleansing-and-transformation"></a><span data-ttu-id="47fd0-161">Nettoyage et transformation des données</span><span class="sxs-lookup"><span data-stu-id="47fd0-161">Data cleansing and transformation</span></span>

<span data-ttu-id="47fd0-162">Ensuite, nous faisons un nettoyage des données de billet d’avion hello, nous avons importé les colonnes toorename.</span><span class="sxs-lookup"><span data-stu-id="47fd0-162">Next we do some cleanup on hello airline data we’ve imported toorename columns.</span></span> <span data-ttu-id="47fd0-163">Nous uniquement conserver des variables hello nécessités et arrondir les heures planifiées de départ vers le bas toohello le plus proche tooenable heures la fusion avec les données les plus récentes météo hello au départ :</span><span class="sxs-lookup"><span data-stu-id="47fd0-163">We only keep hello variables needed, and round scheduled departure times down toohello nearest hour tooenable merging with hello latest weather data at departure:</span></span>

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

<span data-ttu-id="47fd0-164">Maintenant, nous effectuer des opérations similaires sur les données météorologiques hello :</span><span class="sxs-lookup"><span data-stu-id="47fd0-164">Now we perform similar operations on hello weather data:</span></span>

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

## <a name="joining-hello-weather-and-airline-data"></a><span data-ttu-id="47fd0-165">Jointure de données météo et compagnie aérienne de hello</span><span class="sxs-lookup"><span data-stu-id="47fd0-165">Joining hello weather and airline data</span></span>

<span data-ttu-id="47fd0-166">Nous utilisons désormais hello SparkR [join()](https://docs.databricks.com/spark/latest/sparkr/functions/join.html) toodo une jointure externe gauche de données de compagnie aérienne et de la météo hello par AirportID de départ et de date/heure de la fonction.</span><span class="sxs-lookup"><span data-stu-id="47fd0-166">We now use hello SparkR [join()](https://docs.databricks.com/spark/latest/sparkr/functions/join.html) function toodo a left outer join of hello airline and weather data by departure AirportID and datetime.</span></span> <span data-ttu-id="47fd0-167">jointure externe de Hello permet tooretain toutes les données de billet d’avion hello enregistre même s’il n’existe pas de données météo correspondantes.</span><span class="sxs-lookup"><span data-stu-id="47fd0-167">hello outer join allows us tooretain all hello airline data records even if there is no matching weather data.</span></span> <span data-ttu-id="47fd0-168">Suivant la jointure de hello, nous supprime certaines colonnes redondantes et renommer hello conservé tooremove hello entrants trame de données préfixe de colonne introduit par la jointure de hello.</span><span class="sxs-lookup"><span data-stu-id="47fd0-168">Following hello join, we remove some redundant columns, and rename hello kept columns tooremove hello incoming DataFrame prefix introduced by hello join.</span></span>

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

<span data-ttu-id="47fd0-169">De la même manière, nous joindre des données météo et compagnie aérienne hello, en fonction de l’arrivée AirportID et datetime :</span><span class="sxs-lookup"><span data-stu-id="47fd0-169">In a similar fashion, we join hello weather and airline data based on arrival AirportID and datetime:</span></span>

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

## <a name="save-results-toocsv-for-exchange-with-scaler"></a><span data-ttu-id="47fd0-170">Enregistrer les tooCSV de résultats pour l’échange avec ScaleR</span><span class="sxs-lookup"><span data-stu-id="47fd0-170">Save results tooCSV for exchange with ScaleR</span></span>

<span data-ttu-id="47fd0-171">Jointures hello nous devons toodo avec SparkR se termine.</span><span class="sxs-lookup"><span data-stu-id="47fd0-171">That completes hello joins we need toodo with SparkR.</span></span> <span data-ttu-id="47fd0-172">Nous enregistrer les données de hello hello final Spark de trame de données « joinedDF5 » tooa CSV pour tooScaleR d’entrée et que vous fermez puis session SparkR de hello.</span><span class="sxs-lookup"><span data-stu-id="47fd0-172">We save hello data from hello final Spark DataFrame “joinedDF5” tooa CSV for input tooScaleR and then close out hello SparkR session.</span></span> <span data-ttu-id="47fd0-173">Nous dire explicitement à SparkR toosave hello CSV résultant dans des partitions distinctes 80 tooenable suffisamment du parallélisme dans le traitement de ScaleR :</span><span class="sxs-lookup"><span data-stu-id="47fd0-173">We explicitly tell SparkR toosave hello resultant CSV in 80 separate partitions tooenable sufficient parallelism in ScaleR processing:</span></span>

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

## <a name="import-tooxdf-for-use-by-scaler"></a><span data-ttu-id="47fd0-174">TooXDF d’importation pour une utilisation par ScaleR</span><span class="sxs-lookup"><span data-stu-id="47fd0-174">Import tooXDF for use by ScaleR</span></span>

<span data-ttu-id="47fd0-175">Nous pouvons utiliser le fichier CSV de hello de billet d’avion jointe et les données météorologiques en tant que-est pour la modélisation via une source de données de texte ScaleR.</span><span class="sxs-lookup"><span data-stu-id="47fd0-175">We could use hello CSV file of joined airline and weather data as-is for modeling via a ScaleR text data source.</span></span> <span data-ttu-id="47fd0-176">Mais nous importez-le tooXDF en premier lieu, car il est plus efficace lors de l’exécution de plusieurs opérations sur le jeu de données hello :</span><span class="sxs-lookup"><span data-stu-id="47fd0-176">But we import it tooXDF first, since it is more efficient when running multiple operations on hello dataset:</span></span>

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

## <a name="splitting-data-for-training-and-test"></a><span data-ttu-id="47fd0-177">Fractionnement des données pour le test et l’apprentissage</span><span class="sxs-lookup"><span data-stu-id="47fd0-177">Splitting data for training and test</span></span>

<span data-ttu-id="47fd0-178">Nous utiliser toosplit rxDataStep les données de 2012 hello pour le test et conserver reste hello pour l’apprentissage :</span><span class="sxs-lookup"><span data-stu-id="47fd0-178">We use rxDataStep toosplit out hello 2012 data for testing and keep hello rest for training:</span></span>

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

## <a name="train-and-test-a-logistic-regression-model"></a><span data-ttu-id="47fd0-179">Effectuer l’apprentissage et tester un modèle de régression logistique</span><span class="sxs-lookup"><span data-stu-id="47fd0-179">Train and test a logistic regression model</span></span>

<span data-ttu-id="47fd0-180">Vous êtes désormais prêt toobuild un modèle.</span><span class="sxs-lookup"><span data-stu-id="47fd0-180">Now we are ready toobuild a model.</span></span> <span data-ttu-id="47fd0-181">toosee hello influence des données météorologiques de délai dans l’heure d’arrivée hello, nous utilisons routine de régression logistique de ScaleR.</span><span class="sxs-lookup"><span data-stu-id="47fd0-181">toosee hello influence of weather data on delay in hello arrival time, we use ScaleR’s logistic regression routine.</span></span> <span data-ttu-id="47fd0-182">Nous utilisons il toomodel si un délai de l’arrivée de plus de 15 minutes est influencé par météo hello dans les aéroports de départ et d’arrivée hello :</span><span class="sxs-lookup"><span data-stu-id="47fd0-182">We use it toomodel whether an arrival delay of greater than 15 minutes is influenced by hello weather at hello departure and arrival airports:</span></span>

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

<span data-ttu-id="47fd0-183">Maintenant nous allons voir comment il sur hello teste données en effectuant des prédictions examinant ROC et AUC.</span><span class="sxs-lookup"><span data-stu-id="47fd0-183">Now let’s see how it does on hello test data by making some predictions and looking at ROC and AUC.</span></span>

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

## <a name="scoring-elsewhere"></a><span data-ttu-id="47fd0-184">Notation depuis un autre emplacement</span><span class="sxs-lookup"><span data-stu-id="47fd0-184">Scoring elsewhere</span></span>

<span data-ttu-id="47fd0-185">Nous pouvons également utiliser le modèle de hello pour le calcul de score des données sur une autre plateforme.</span><span class="sxs-lookup"><span data-stu-id="47fd0-185">We can also use hello model for scoring data on another platform.</span></span> <span data-ttu-id="47fd0-186">En enregistrant le fichier des services Bureau à distance tooan transfert et l’importation de ce services Bureau à distance dans une environnement tel que SQL Server R Services de calcul de score de destination.</span><span class="sxs-lookup"><span data-stu-id="47fd0-186">By saving it tooan RDS file and then transferring and importing that RDS into a destination scoring environment such as SQL Server R Services.</span></span> <span data-ttu-id="47fd0-187">Il est important tooensure niveaux hello des facteurs de hello toobe de données au score calculé correspondant à celles sur quel hello modèle a été créé.</span><span class="sxs-lookup"><span data-stu-id="47fd0-187">It is important tooensure that hello factor levels of hello data toobe scored match those on which hello model was built.</span></span> <span data-ttu-id="47fd0-188">Que correspondance peut être obtenue en extrayant et enregistrer les informations de colonne hello associé hello modélisation des données par le biais de ScaleR `rxCreateColInfo()` (fonction), puis en appliquant cette source de données d’entrée de colonne informations toohello pour la prédiction.</span><span class="sxs-lookup"><span data-stu-id="47fd0-188">That match can be achieved by extracting and saving hello column infomation associated with hello modeling data via ScaleR’s `rxCreateColInfo()` function and then applying that column information toohello input data source for prediction.</span></span> <span data-ttu-id="47fd0-189">Suivant de hello nous enregistrer quelques lignes du jeu de données de test hello et extraire et utilisez hello les informations de colonne à partir de cet exemple de script de prédiction hello :</span><span class="sxs-lookup"><span data-stu-id="47fd0-189">In hello following we save a few rows of hello test dataset and extract and use hello column information from this sample in hello prediction script:</span></span>

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

## <a name="summary"></a><span data-ttu-id="47fd0-190">Résumé</span><span class="sxs-lookup"><span data-stu-id="47fd0-190">Summary</span></span>

<span data-ttu-id="47fd0-191">Dans cet article, nous avons montré comment il est possible toocombine de SparkR pour la manipulation de données avec ScaleR pour le développement de modèles dans Hadoop Spark.</span><span class="sxs-lookup"><span data-stu-id="47fd0-191">In this article, we’ve shown how it’s possible toocombine use of SparkR for data manipulation with ScaleR for model development in Hadoop Spark.</span></span> <span data-ttu-id="47fd0-192">Ce scénario nécessite de maintenir les sessions de Spark séparées, en n’exécutant qu’une session à la fois et d’échanger des données via des fichiers CSV.</span><span class="sxs-lookup"><span data-stu-id="47fd0-192">This scenario requires that you maintain separate Spark sessions, only running one session at a time, and exchange data via CSV files.</span></span> <span data-ttu-id="47fd0-193">Bien que simple, ce processus est largement simplifié dans une prochaine version de R Server, lorsque SparkR et ScaleR peuvent partager une session Spark et, par conséquent, Spark DataFrames.</span><span class="sxs-lookup"><span data-stu-id="47fd0-193">Although straightforward, this process should be even easier in an upcoming R Server release, when SparkR and ScaleR can share a Spark session and so share Spark DataFrames.</span></span>

## <a name="next-steps-and-more-information"></a><span data-ttu-id="47fd0-194">Étapes suivantes et informations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="47fd0-194">Next steps and more information</span></span>

- <span data-ttu-id="47fd0-195">Pour plus d’informations sur l’utilisation du serveur de R sur Spark, consultez hello [guide Mise en route sur MSDN](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started)</span><span class="sxs-lookup"><span data-stu-id="47fd0-195">For more information on use of R Server on Spark, see hello [Getting started guide on MSDN](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started)</span></span>

- <span data-ttu-id="47fd0-196">Pour obtenir des informations générales sur le serveur R, consultez hello [prise en main R](https://msdn.microsoft.com/microsoft-r/microsoft-r-get-started-node) l’article.</span><span class="sxs-lookup"><span data-stu-id="47fd0-196">For general information on R Server, see hello [Get started with R](https://msdn.microsoft.com/microsoft-r/microsoft-r-get-started-node) article.</span></span>

- <span data-ttu-id="47fd0-197">Pour plus d’informations sur R Server sur HDInsight, consultez [Présentation de R Server sur Azure HDInsight](hdinsight-hadoop-r-server-overview.md) et [R Server sur Azure HDInsight](hdinsight-hadoop-r-server-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="47fd0-197">For information on R Server on HDInsight, see [R Server on Azure HDInsight overview](hdinsight-hadoop-r-server-overview.md) and [R Server on Azure HDInsight](hdinsight-hadoop-r-server-get-started.md).</span></span>

<span data-ttu-id="47fd0-198">Pour plus d’informations sur l’utilisation de SparkR, consultez les pages suivantes :</span><span class="sxs-lookup"><span data-stu-id="47fd0-198">For more information on use of SparkR, see:</span></span>

- [<span data-ttu-id="47fd0-199">Document Apache SparkR</span><span class="sxs-lookup"><span data-stu-id="47fd0-199">Apache SparkR document</span></span>](https://spark.apache.org/docs/2.1.0/sparkr.html)

- <span data-ttu-id="47fd0-200">[Vue d’ensemble de SparkR](https://docs.databricks.com/spark/latest/sparkr/overview.html) à partir de Databricks</span><span class="sxs-lookup"><span data-stu-id="47fd0-200">[SparkR Overview](https://docs.databricks.com/spark/latest/sparkr/overview.html) from Databricks</span></span>
