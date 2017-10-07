---
title: AAA(deprecated) analyse de survie avec Azure Machine Learning | Documents Microsoft
description: "(obsolète) Probabilité d'occurrence d'un événement d'analyse de survie"
services: machine-learning
documentationcenter: 
author: zhangya
manager: jhubbard
editor: cgronlun
ms.assetid: a142fc45-cdfb-4971-910e-05dab8bc699e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: zhangya
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: af946d8df5ba650a9d74fbabbe3b15d3a07dd508
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-survival-analysis"></a><span data-ttu-id="a6acf-103">(obsolète) Analyse de survie</span><span class="sxs-lookup"><span data-stu-id="a6acf-103">(deprecated) Survival Analysis</span></span>

> [!NOTE]
> <span data-ttu-id="a6acf-104">Hello Microsoft DataMarket a été supprimée et que cette API est déconseillée.</span><span class="sxs-lookup"><span data-stu-id="a6acf-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="a6acf-105">Vous trouverez plusieurs API et les expériences d’exemple utile Bonjour [Cortana Intelligence galerie](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="a6acf-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="a6acf-106">Pour plus d’informations sur la galerie de hello, consultez [partager et découvrir des ressources Bonjour Cortana Intelligence galerie](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="a6acf-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="a6acf-107">Dans nombreux scénarios, le résultat de principal de hello en cours d’évaluation est événement tooan hello dignes d’intérêt.</span><span class="sxs-lookup"><span data-stu-id="a6acf-107">Under many scenarios, hello main outcome under assessment is hello time tooan event of interest.</span></span> <span data-ttu-id="a6acf-108">En d’autres termes, les question hello « lorsque cet événement se produit ? »</span><span class="sxs-lookup"><span data-stu-id="a6acf-108">In other words, hello question “when this event will occur?”</span></span> <span data-ttu-id="a6acf-109">va-t-il se produire ? ».</span><span class="sxs-lookup"><span data-stu-id="a6acf-109">is asked.</span></span> <span data-ttu-id="a6acf-110">Par exemple, vous devez prendre en compte les situations où les données de salutation décrivent hello temps (jours, années, consommation, etc.) jusqu'à ce que hello événements d’intérêt (Échec de remplissage de frein, degré de bloc reçu, RECHUTE de maladie) se produit.</span><span class="sxs-lookup"><span data-stu-id="a6acf-110">As examples, consider situations where hello data describes hello elapsed time (days, years, mileage, etc.) until hello event of interest (disease relapse, PhD degree received, brake pad failure) occurs.</span></span> <span data-ttu-id="a6acf-111">Dans les données de salutation, chaque instance représente un objet spécifique (un patient, un étudiant, une voiture, etc.).</span><span class="sxs-lookup"><span data-stu-id="a6acf-111">Each instance in hello data represents a specific object (a patient, a student, a car, etc.).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="a6acf-112">Cela [service web](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis) répond à la question de hello « quelle est la probabilité de hello hello des événements d’intérêt se produit en n fois pour l’objet x ? »</span><span class="sxs-lookup"><span data-stu-id="a6acf-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis) answers hello question “what is hello probability that hello event of interest will occur by time n for object x?”</span></span> <span data-ttu-id="a6acf-113">En fournissant un modèle d’analyse de survie, ce service web permet aux utilisateurs toosupply tootrain hello EDM et le tester.</span><span class="sxs-lookup"><span data-stu-id="a6acf-113">By providing a survival analysis model, this web service enables users toosupply data tootrain hello model and test it.</span></span> <span data-ttu-id="a6acf-114">le thème principal de l’expérience de hello Hello est toomodel hello hello écoulé Durée jusqu'à ce que l’événement hello d’intérêt se produit.</span><span class="sxs-lookup"><span data-stu-id="a6acf-114">hello main theme of hello experiment is toomodel hello length of hello elapsed time until hello event of interest occurs.</span></span> 

> <span data-ttu-id="a6acf-115">Les utilisateurs peuvent potentiellement accéder à ce service web par le biais d’une application mobile, d’un site web ou même d’un ordinateur local, par exemple.</span><span class="sxs-lookup"><span data-stu-id="a6acf-115">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="a6acf-116">Mais hello objectif du service web de hello est également tooserve comme exemple illustrant comment Azure Machine Learning peuvent être des services web toocreate utilisé sur le code R.</span><span class="sxs-lookup"><span data-stu-id="a6acf-116">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="a6acf-117">Avec seulement quelques lignes de code R et quelques clics dans Azure Machine Learning Studio, vous pouvez créer une expérience avec le code R et la publier en tant que service web.</span><span class="sxs-lookup"><span data-stu-id="a6acf-117">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="a6acf-118">service web de Hello peut ensuite être publié toohello Azure Marketplace et consommé par les utilisateurs et périphériques sur Bonjour sans configuration d’infrastructure par l’auteur de hello du service web de hello.</span><span class="sxs-lookup"><span data-stu-id="a6acf-118">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="a6acf-119">Utilisation du service web</span><span class="sxs-lookup"><span data-stu-id="a6acf-119">Consumption of web service</span></span>
<span data-ttu-id="a6acf-120">schéma de données d’entrée de Hello du service web de hello est présenté dans hello tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="a6acf-120">hello input data schema of hello web service is shown in hello following table.</span></span> <span data-ttu-id="a6acf-121">Six informations sont nécessaires en tant qu’entrée de hello : données d’apprentissage, données de test, d’intérêt, index hello de dimension de « heure », index hello de dimension de le « événement » et les types de variables hello (continues ou facteur).</span><span class="sxs-lookup"><span data-stu-id="a6acf-121">Six pieces of information are needed as hello input: training data, testing data, time of interest, hello index of "time" dimension, hello index of "event" dimension, and hello variable types (continuous or factor).</span></span> <span data-ttu-id="a6acf-122">données d’apprentissage Hello sont représentées par une chaîne, où les lignes de hello sont séparées par des virgules, et les colonnes de hello sont séparées par des points-virgules.</span><span class="sxs-lookup"><span data-stu-id="a6acf-122">hello training data is represented with a string, where hello rows are separated by comma, and hello columns are separated by semicolon.</span></span> <span data-ttu-id="a6acf-123">nombre de Hello des fonctionnalités de données de hello est flexible.</span><span class="sxs-lookup"><span data-stu-id="a6acf-123">hello number of features of hello data is flexible.</span></span> <span data-ttu-id="a6acf-124">Tous les éléments hello dans la chaîne d’entrée de hello doivent être numériques.</span><span class="sxs-lookup"><span data-stu-id="a6acf-124">All hello elements in hello input string must be numeric.</span></span> <span data-ttu-id="a6acf-125">Dans les données d’apprentissage hello, dimension hello « temps » indique hello plusieurs unités de temps (jours, années, consommation, etc.) s’est écoulé depuis le point de départ hello Hello étudier (un patient recevoir des programmes de traitement de médicament, une étude de bloc de départ étudiant, une voiture démarrage toobe fonction, etc.) jusqu'à ce que hello événements d’intérêt (patient hello retour de l’utilisation de toodrug, degré de bloc hello étudiant obtention hello, véhicule hello frein remplissage échec, etc.) se produit.</span><span class="sxs-lookup"><span data-stu-id="a6acf-125">In hello training data, hello “time” dimension indicates hello number of time units (days, years, mileage, etc.) elapsed since hello starting point of hello study (a patient receiving drug treatment programs, a student starting PhD study, a car starting toobe driven, etc.) until hello event of interest (hello patient returning toodrug usage, hello student obtaining hello PhD degree, hello car having brake pad failure, etc.) occurs.</span></span> <span data-ttu-id="a6acf-126">dimension de « événement » Hello indique si les événements hello d’intérêt se produit à fin hello d’étude de hello.</span><span class="sxs-lookup"><span data-stu-id="a6acf-126">hello “event” dimension indicates whether hello event of interest occurs at hello end of hello study.</span></span> <span data-ttu-id="a6acf-127">Une valeur de « événement = 1 » signifie que les événements d’intérêt de hello se produit au moment de hello indiqué par la dimension « temps » de hello ; « événement = 0 » signifie que les événements d’intérêt de hello n’a pas eu lieu après le temps hello indiqué par la dimension « temps » de hello.</span><span class="sxs-lookup"><span data-stu-id="a6acf-127">A value of “event=1” means that hello event of interest occurs at hello time indicated by hello “time” dimension; “event=0” means that hello event of interest has not occurred by hello time indicated by hello “time” dimension.</span></span>

* <span data-ttu-id="a6acf-128">trainingdata : il s’agit d’une chaîne de caractères.</span><span class="sxs-lookup"><span data-stu-id="a6acf-128">trainingdata - A character string.</span></span> <span data-ttu-id="a6acf-129">Les lignes sont séparées par des virgules et les colonnes sont séparées par des points-virgules.</span><span class="sxs-lookup"><span data-stu-id="a6acf-129">Rows are separated by comma, and columns are separated by semicolon.</span></span> <span data-ttu-id="a6acf-130">Chaque ligne inclut la dimension « temporelle », la dimension de l'« évènement » et les variables de prédiction.</span><span class="sxs-lookup"><span data-stu-id="a6acf-130">Each row includes “time” dimension, “event” dimension, and predictor variables.</span></span>
* <span data-ttu-id="a6acf-131">testingdata : il s’agit d’une ligne de données qui contient les variables de prédiction pour un objet particulier.</span><span class="sxs-lookup"><span data-stu-id="a6acf-131">testingdata - One row of data that contains predictor variables for a particular object.</span></span>
* <span data-ttu-id="a6acf-132">time_of_interest - temps hello de n d’intérêt.</span><span class="sxs-lookup"><span data-stu-id="a6acf-132">time_of_interest - hello elapsed time of interest n.</span></span>
* <span data-ttu-id="a6acf-133">index_time - index de colonne hello hello « dimension de temps » (à partir de 1).</span><span class="sxs-lookup"><span data-stu-id="a6acf-133">index_time - hello column index of hello “time” dimension (starting from 1).</span></span>
* <span data-ttu-id="a6acf-134">index_event - index de colonne hello de dimension de « événement » hello (à partir de 1).</span><span class="sxs-lookup"><span data-stu-id="a6acf-134">index_event - hello column index of hello “event” dimension (starting from 1).</span></span>
* <span data-ttu-id="a6acf-135">variable_types : une chaîne de caractères séparés par des points-virgules.</span><span class="sxs-lookup"><span data-stu-id="a6acf-135">variable_types - A character string with semicolons as separators in it.</span></span> <span data-ttu-id="a6acf-136">0 représente les variables continues et 1 représente les variables facteur.</span><span class="sxs-lookup"><span data-stu-id="a6acf-136">0 represents continuous variables and 1 represents factor variables.</span></span>

<span data-ttu-id="a6acf-137">sortie de Hello est la probabilité de hello d’un événement qui se produisent à une heure spécifique.</span><span class="sxs-lookup"><span data-stu-id="a6acf-137">hello output is hello probability of an event occurring by a specific time.</span></span> 

> <span data-ttu-id="a6acf-138">Ce service, comme hébergé sur hello Azure Marketplace, est un service OData ; Il peuvent être appelées par le biais des méthodes POST ou GET.</span><span class="sxs-lookup"><span data-stu-id="a6acf-138">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="a6acf-139">Il existe plusieurs manières de consommation de service hello de manière automatique (un exemple d’application est [ici](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx)).</span><span class="sxs-lookup"><span data-stu-id="a6acf-139">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx)).</span></span> 

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="a6acf-140">Début du code C# pour l'utilisation du service web :</span><span class="sxs-lookup"><span data-stu-id="a6acf-140">Starting C# code for web service consumption:</span></span>
    public class Input
    {
            public string trainingdata;
            public string testingdata;
            public string timeofinterest;
            public string indextime;
            public string indexevent;
            public string variabletypes;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { trainingdata = TextBox1.Text, testingdata = TextBox2.Text, timeofinterest = TextBox3.Text, indextime = TextBox4.Text, indexevent = TextBox5.Text, variabletypes = TextBox6.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }




<span data-ttu-id="a6acf-141">interprétation de Hello de ce test est la suivante.</span><span class="sxs-lookup"><span data-stu-id="a6acf-141">hello interpretation of this test is as follows.</span></span> <span data-ttu-id="a6acf-142">En supposant que l’objectif hello de données de hello est toomodel hello écoulé jusqu'à hello retourner toodrug utilisation de patients hello qui ont reçu un des programmes de traitement hello deux.</span><span class="sxs-lookup"><span data-stu-id="a6acf-142">Assuming hello goal of hello data is toomodel hello elapsed time until hello return toodrug usage for hello patients who received one of hello two treatment programs.</span></span> <span data-ttu-id="a6acf-143">Hello sortie de lectures de service web hello : patients en cours de 35 ans, ayant précédente médicament traitement 2 fois, en prenant le programme de traitement long résidentielle hello, et avec utilisation héroïne et cocaïne, probabilité hello de retour de l’utilisation de médicament toohello est % 95.64 par jour 500.</span><span class="sxs-lookup"><span data-stu-id="a6acf-143">hello output of hello web service reads: for patients being 35 years old, having previous drug treatment 2 times, taking hello long residential treatment program, and with both heroin and cocaine usage, hello probability of returning toohello drug usage is 95.64% by day 500.</span></span>

## <a name="creation-of-web-service"></a><span data-ttu-id="a6acf-144">Création du service web</span><span class="sxs-lookup"><span data-stu-id="a6acf-144">Creation of web service</span></span>
> <span data-ttu-id="a6acf-145">Ce service web a été créé à l’aide d’Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="a6acf-145">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="a6acf-146">Pour un essai gratuit, ainsi que des vidéos de présentation relatives à la création d’expériences et à la [publication de services web](machine-learning-publish-a-machine-learning-web-service.md), consultez [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="a6acf-146">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="a6acf-147">Voici une capture d’écran d’expérience hello qui a créé un code de service et un exemple hello web pour chacun des modules hello au sein de l’expérience de hello.</span><span class="sxs-lookup"><span data-stu-id="a6acf-147">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="a6acf-148">À partir d’Azure Machine Learning, une nouvelle expérience vide a été créée et deux [Execute R Script] [ execute-r-script] modules ont été collectés dans l’espace de travail hello.</span><span class="sxs-lookup"><span data-stu-id="a6acf-148">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules were pulled onto hello workspace.</span></span> <span data-ttu-id="a6acf-149">schéma de données Hello a été créé avec une simple [Execute R Script][execute-r-script], qui définit le schéma de données d’entrée hello pour le service web de hello.</span><span class="sxs-lookup"><span data-stu-id="a6acf-149">hello data schema was created with a simple [Execute R Script][execute-r-script], which defines hello input data schema for hello web service.</span></span> <span data-ttu-id="a6acf-150">Ce module est ensuite lié toohello deuxième [Execute R Script] [ execute-r-script] module, qui majeure de travail.</span><span class="sxs-lookup"><span data-stu-id="a6acf-150">This module is then linked toohello second [Execute R Script][execute-r-script] module, which does major work.</span></span> <span data-ttu-id="a6acf-151">Ce module réalise le prétraitement des données, la création du modèle et les prédictions.</span><span class="sxs-lookup"><span data-stu-id="a6acf-151">This module does data preprocessing, model building, and predictions.</span></span> <span data-ttu-id="a6acf-152">Dans l’étape de prétraitement hello données, les données d’entrée hello représentées par une longue chaîne sont transformées et converties en une trame de données.</span><span class="sxs-lookup"><span data-stu-id="a6acf-152">In hello data preprocessing step, hello input data represented by a long string is transformed and converted into a data frame.</span></span> <span data-ttu-id="a6acf-153">À l’étape de génération de modèle hello, un package R externe « survival_2.37-7.zip » est tout d’abord installé pour effectuer l’analyse de survie.</span><span class="sxs-lookup"><span data-stu-id="a6acf-153">In hello model building step, an external R package “survival_2.37-7.zip” is first installed for conducting survival analysis.</span></span> <span data-ttu-id="a6acf-154">Fonction de « coxph » hello est ensuite exécutée après une tâche de traitement des données de série.</span><span class="sxs-lookup"><span data-stu-id="a6acf-154">Then hello “coxph” function is executed after a series data processing tasks.</span></span> <span data-ttu-id="a6acf-155">Détails de Hello de fonction de « coxph » hello pour l’analyse de survie peuvent être lus à partir de la documentation de hello R.</span><span class="sxs-lookup"><span data-stu-id="a6acf-155">hello details of hello “coxph” function for survival analysis can be read from hello R documentation.</span></span> <span data-ttu-id="a6acf-156">À l’étape de prédiction hello, une instance de test est fournie dans le modèle formé de hello avec fonction de « surfit » hello et courbe de survie hello pour cette instance de test est généré en tant que variable de « curve ».</span><span class="sxs-lookup"><span data-stu-id="a6acf-156">In hello prediction step, a testing instance is supplied into hello trained model with hello “surfit” function, and hello survival curve for this testing instance is produced as “curve” variable.</span></span> <span data-ttu-id="a6acf-157">Enfin, probabilité hello de temps hello dignes d’intérêt est obtenue.</span><span class="sxs-lookup"><span data-stu-id="a6acf-157">Finally, hello probability of hello time of interest is obtained.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="a6acf-158">Flux de l’expérience :</span><span class="sxs-lookup"><span data-stu-id="a6acf-158">Experiment flow:</span></span>
![Flux de l’expérience][1]

#### <a name="module-1"></a><span data-ttu-id="a6acf-160">Module 1 :</span><span class="sxs-lookup"><span data-stu-id="a6acf-160">Module 1:</span></span>
    #Data schema with example data (replaced with data from web service)
    trainingdata="53;1;29;0;0;3,79;1;34;0;1;2,45;1;27;0;1;1,37;1;24;0;1;1,122;1;30;0;1;1,655;0;41;0;0;1,166;1;30;0;0;3,227;1;29;0;0;3,805;0;30;0;0;1,104;1;24;0;0;1,90;1;32;0;0;1,373;1;26;0;0;1,70;1;36;0;0;1”
    testingdata="35;2;1;1"
    time_of_interest="500"
    index_time="1"
    index_event="2"

    # 0 - continuous; 1 -  factor
    variable_types="0;0;1;1"

    sampleInput=data.frame(trainingdata,testingdata,time_of_interest,index_time,index_event,variable_types)

    maml.mapOutputPort("sampleInput"); #send data toooutput port

#### <a name="module-2"></a><span data-ttu-id="a6acf-161">Module 2 :</span><span class="sxs-lookup"><span data-stu-id="a6acf-161">Module 2:</span></span>
    #Read data from input port
    data <- maml.mapInputPort(1) 
    colnames(data) <- c("trainingdata","testingdata","time_of_interest","index_time","index_event","variable_types")

    # Preprocessing training data
    traindingdata=data$trainingdata
    y=strsplit(as.character(data$trainingdata),",")
    n_row=length(unlist(y))
    z=sapply(unlist(y), strsplit, ";", simplify = TRUE)
    mydata <- data.frame(matrix(unlist(z), nrow=n_row, byrow=T), stringsAsFactors=FALSE)
    n_col=ncol(mydata)

    # Preprocessing testing data
    testingdata=as.character(data$testingdata)
    testingdata=unlist(strsplit(testingdata,";"))

    # Preprocessing other input parameters
    time_of_interest=data$time_of_interest
    time_of_interest=as.numeric(as.character(time_of_interest))
    index_time = data$index_time
    index_event = data$index_event
    variable_types = data$variable_types

    # Necessary R packages
    install.packages("src/packages_survival/survival_2.37-7.zip",lib=".",repos=NULL,verbose=TRUE)
    library(survival)

    # Prepare toobuild model
    attach(mydata)

    for (i in 1:n_col){ mydata[,i]=as.numeric(mydata[,i])} 
    d_time=paste("X",index_time,sep = "")
    d_event=paste("X",index_event,sep = "")
    v_time_event <- c(d_time,d_event)
    v_predictors = names(mydata)[!(names(mydata) %in% v_time_event)]

    variable_types = unlist(strsplit(as.character(variable_types),";"))

    len = length(v_predictors)
    c="" # Construct hello execution string
    for (i in 1:len){
    if(i==len){
    if(variable_types[i]!=0){ c=paste(c, "factor(",v_predictors[i],")",sep="")}
     else{ c=paste(c, v_predictors[i])}
    }else{
    if(variable_types[i]!=0){c=paste(c, "factor(",v_predictors[i],") + ",sep="")}
    else{c=paste(c, v_predictors[i],"+")}
    }
    }
    f=paste("coxph(Surv(",d_time,",",d_event,") ~")
    f=paste(f,c)
    f=paste(f,", data=mydata )")

    # Fit a Cox proportional hazards model and get hello predicted survival curve for a testing instance 
    fit=eval(parse(text=f))

    testingdata = as.data.frame(matrix(testingdata, ncol=len,byrow = TRUE),stringsAsFactors=FALSE)
    names(testingdata)=v_predictors
    for (i in 1:len){ testingdata[,i]=as.numeric(testingdata[,i])}

    curve=survfit(fit,testingdata)

    # Based on user input, find hello event occurrence probability
    position_closest=which.min(abs(prob_event$time - time_of_interest))

    if(prob_event[position_closest,"time"]==time_of_interest){# exact match
    output=prob_event[position_closest,"prob"]
    }else{# not exact match
    if(time_of_interest>max(prob_event$time)){
    output=prob_event[position_closest,"prob"]
    }else if(time_of_interest<min(prob_event$time)){
    output=prob_event[position_closest,"prob"]
    }else{output=(prob_event[position_closest,"prob"]+prob_event[position_closest+1,"prob"])/2}
    }

    #Pull out results toosend tooweb service
    output=paste(round(100*output, 2), "%") 
    maml.mapOutputPort("output"); #output port




## <a name="limitations"></a><span data-ttu-id="a6acf-162">Limitations</span><span class="sxs-lookup"><span data-stu-id="a6acf-162">Limitations</span></span>
<span data-ttu-id="a6acf-163">Ce service web accepte uniquement les valeurs numériques sous forme de variables de fonctionnalité (colonnes).</span><span class="sxs-lookup"><span data-stu-id="a6acf-163">This web service can take only numerical values as feature variables (columns).</span></span> <span data-ttu-id="a6acf-164">colonne de « événement » Hello peut prendre la valeur 0 ou 1.</span><span class="sxs-lookup"><span data-stu-id="a6acf-164">hello “event” column can take only value 0 or 1.</span></span> <span data-ttu-id="a6acf-165">colonne de « time » Hello doit toobe un entier positif.</span><span class="sxs-lookup"><span data-stu-id="a6acf-165">hello “time” column needs toobe a positive integer.</span></span>

## <a name="faq"></a><span data-ttu-id="a6acf-166">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="a6acf-166">FAQ</span></span>
<span data-ttu-id="a6acf-167">Pour les questions fréquemment posées sur la consommation de service web de hello ou publication toohello Azure Marketplace, consultez [ici](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="a6acf-167">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-survival-analysis/survive_img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

