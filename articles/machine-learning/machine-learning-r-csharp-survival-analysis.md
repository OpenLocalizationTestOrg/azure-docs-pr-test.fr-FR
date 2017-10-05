---
title: "(obsolète) Analyse de survie avec Azure Machine Learning | Microsoft Docs"
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
redirect_document_id: TRUE
ms.openlocfilehash: 7d4066d5f15a39c428d8035257c4841f9b3cc775
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-survival-analysis"></a><span data-ttu-id="1eb35-103">(obsolète) Analyse de survie</span><span class="sxs-lookup"><span data-stu-id="1eb35-103">(deprecated) Survival Analysis</span></span>

> [!NOTE]
> <span data-ttu-id="1eb35-104">Microsoft DataMarket va être supprimé et cette API est désormais obsolète.</span><span class="sxs-lookup"><span data-stu-id="1eb35-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="1eb35-105">Vous trouverez de nombreux exemples d’expériences et d’API dans la [galerie Cortana Intelligence](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="1eb35-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="1eb35-106">Pour plus d’informations sur la galerie, consultez [Partager et découvrir des solutions dans la galerie Cortana Intelligence](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="1eb35-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="1eb35-107">Dans de nombreux scénarios, le principal résultat évalué est la durée avant qu'un événement qui vous intéresse ne se produise.</span><span class="sxs-lookup"><span data-stu-id="1eb35-107">Under many scenarios, the main outcome under assessment is the time to an event of interest.</span></span> <span data-ttu-id="1eb35-108">En d’autres termes, vous posez la question « Quand cet événement</span><span class="sxs-lookup"><span data-stu-id="1eb35-108">In other words, the question “when this event will occur?”</span></span> <span data-ttu-id="1eb35-109">va-t-il se produire ? ».</span><span class="sxs-lookup"><span data-stu-id="1eb35-109">is asked.</span></span> <span data-ttu-id="1eb35-110">Par exemple, considérez les situations dans lesquelles les données décrivent le temps écoulé (jours, années, kilométrage, etc.) jusqu’à ce que l’événement se produise (rechute (maladie), obtention d’un doctorat, défaillance des plaquettes de frein).</span><span class="sxs-lookup"><span data-stu-id="1eb35-110">As examples, consider situations where the data describes the elapsed time (days, years, mileage, etc.) until the event of interest (disease relapse, PhD degree received, brake pad failure) occurs.</span></span> <span data-ttu-id="1eb35-111">Dans les données, chaque instance représente un objet spécifique (un ou une patient(e), un ou une étudiant(e), une voiture, etc.).</span><span class="sxs-lookup"><span data-stu-id="1eb35-111">Each instance in the data represents a specific object (a patient, a student, a car, etc.).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="1eb35-112">Ce [service web](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis) répond à la question « Quelle est la probabilité que l’événement se produise en n jours/heures/etc. (temps) pour l’objet x ? »</span><span class="sxs-lookup"><span data-stu-id="1eb35-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis) answers the question “what is the probability that the event of interest will occur by time n for object x?”</span></span> <span data-ttu-id="1eb35-113">Grâce au modèle d’analyse de survie, ce service web permet aux utilisateurs de fournir des données pour entraîner le modèle et le tester.</span><span class="sxs-lookup"><span data-stu-id="1eb35-113">By providing a survival analysis model, this web service enables users to supply data to train the model and test it.</span></span> <span data-ttu-id="1eb35-114">Le principal objectif de l'expérience est de modéliser la durée écoulée jusqu'à ce que l'événement se produise.</span><span class="sxs-lookup"><span data-stu-id="1eb35-114">The main theme of the experiment is to model the length of the elapsed time until the event of interest occurs.</span></span> 

> <span data-ttu-id="1eb35-115">Les utilisateurs peuvent potentiellement accéder à ce service web par le biais d’une application mobile, d’un site web ou même d’un ordinateur local, par exemple.</span><span class="sxs-lookup"><span data-stu-id="1eb35-115">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="1eb35-116">Mais l’objectif du service web est également de servir d’exemple d’utilisation d’Azure Machine Learning pour créer des services web avec le code R.</span><span class="sxs-lookup"><span data-stu-id="1eb35-116">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="1eb35-117">Avec seulement quelques lignes de code R et quelques clics dans Azure Machine Learning Studio, vous pouvez créer une expérience avec le code R et la publier en tant que service web.</span><span class="sxs-lookup"><span data-stu-id="1eb35-117">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="1eb35-118">Le service web peut ensuite être publié sur Azure Marketplace afin que les utilisateurs et les appareils du monde entier l’utilisent sans que l’auteur du service web n’ait à configurer l’infrastructure.</span><span class="sxs-lookup"><span data-stu-id="1eb35-118">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="1eb35-119">Utilisation du service web</span><span class="sxs-lookup"><span data-stu-id="1eb35-119">Consumption of web service</span></span>
<span data-ttu-id="1eb35-120">Le schéma de données d'entrée du service web est présenté dans le tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="1eb35-120">The input data schema of the web service is shown in the following table.</span></span> <span data-ttu-id="1eb35-121">Six types d’informations sont nécessaires : les données d’apprentissage, le données de test, la durée d’intérêt, l’index de dimension « temporelle », l’index de dimension de l’« événement » et les types de variables (continues ou facteur).</span><span class="sxs-lookup"><span data-stu-id="1eb35-121">Six pieces of information are needed as the input: training data, testing data, time of interest, the index of "time" dimension, the index of "event" dimension, and the variable types (continuous or factor).</span></span> <span data-ttu-id="1eb35-122">Les données d'apprentissage sont représentées par une chaîne, dans laquelle les lignes sont séparées par des virgules et les colonnes sont séparées par des points-virgules.</span><span class="sxs-lookup"><span data-stu-id="1eb35-122">The training data is represented with a string, where the rows are separated by comma, and the columns are separated by semicolon.</span></span> <span data-ttu-id="1eb35-123">Le nombre de fonctionnalités des données est flexible.</span><span class="sxs-lookup"><span data-stu-id="1eb35-123">The number of features of the data is flexible.</span></span> <span data-ttu-id="1eb35-124">Tous les éléments de la chaîne d'entrée doivent être numériques.</span><span class="sxs-lookup"><span data-stu-id="1eb35-124">All the elements in the input string must be numeric.</span></span> <span data-ttu-id="1eb35-125">Dans les données d’apprentissage, la dimension « temporelle » indique le nombre d’unités de temps (jours, années, kilométrage, etc.) qui s’est écoulé depuis le point de départ de l’étude (un patient suivant un programme de désintoxication, un étudiant commençant son doctorat, le début de la conduite d’une voiture, etc.) jusqu’à ce que l’événement se produise (le patient consomme de la drogue, l’étudiant obtient son doctorat, les plaquettes de frein de la voiture sont usées, etc.).</span><span class="sxs-lookup"><span data-stu-id="1eb35-125">In the training data, the “time” dimension indicates the number of time units (days, years, mileage, etc.) elapsed since the starting point of the study (a patient receiving drug treatment programs, a student starting PhD study, a car starting to be driven, etc.) until the event of interest (the patient returning to drug usage, the student obtaining the PhD degree, the car having brake pad failure, etc.) occurs.</span></span> <span data-ttu-id="1eb35-126">La dimension de l'« évènement » indique si l'évènement se produit à la fin de l'étude.</span><span class="sxs-lookup"><span data-stu-id="1eb35-126">The “event” dimension indicates whether the event of interest occurs at the end of the study.</span></span> <span data-ttu-id="1eb35-127">La valeur « event=1 » signifie que l’évènement se produit au moment indiqué par la dimension « temporelle » ; tandis que « event=0 » signifie que l’évènement n’a pas encore eu lieu au moment indiqué par la dimension « temporelle ».</span><span class="sxs-lookup"><span data-stu-id="1eb35-127">A value of “event=1” means that the event of interest occurs at the time indicated by the “time” dimension; “event=0” means that the event of interest has not occurred by the time indicated by the “time” dimension.</span></span>

* <span data-ttu-id="1eb35-128">trainingdata : il s’agit d’une chaîne de caractères.</span><span class="sxs-lookup"><span data-stu-id="1eb35-128">trainingdata - A character string.</span></span> <span data-ttu-id="1eb35-129">Les lignes sont séparées par des virgules et les colonnes sont séparées par des points-virgules.</span><span class="sxs-lookup"><span data-stu-id="1eb35-129">Rows are separated by comma, and columns are separated by semicolon.</span></span> <span data-ttu-id="1eb35-130">Chaque ligne inclut la dimension « temporelle », la dimension de l'« évènement » et les variables de prédiction.</span><span class="sxs-lookup"><span data-stu-id="1eb35-130">Each row includes “time” dimension, “event” dimension, and predictor variables.</span></span>
* <span data-ttu-id="1eb35-131">testingdata : il s’agit d’une ligne de données qui contient les variables de prédiction pour un objet particulier.</span><span class="sxs-lookup"><span data-stu-id="1eb35-131">testingdata - One row of data that contains predictor variables for a particular object.</span></span>
* <span data-ttu-id="1eb35-132">time_of_interest : le temps n écoulé.</span><span class="sxs-lookup"><span data-stu-id="1eb35-132">time_of_interest - The elapsed time of interest n.</span></span>
* <span data-ttu-id="1eb35-133">index_time : index de colonne de la dimension « temporelle » (à partir de 1).</span><span class="sxs-lookup"><span data-stu-id="1eb35-133">index_time - The column index of the “time” dimension (starting from 1).</span></span>
* <span data-ttu-id="1eb35-134">index_event : index de colonne de la dimension « événement » (à partir de 1).</span><span class="sxs-lookup"><span data-stu-id="1eb35-134">index_event - The column index of the “event” dimension (starting from 1).</span></span>
* <span data-ttu-id="1eb35-135">variable_types : une chaîne de caractères séparés par des points-virgules.</span><span class="sxs-lookup"><span data-stu-id="1eb35-135">variable_types - A character string with semicolons as separators in it.</span></span> <span data-ttu-id="1eb35-136">0 représente les variables continues et 1 représente les variables facteur.</span><span class="sxs-lookup"><span data-stu-id="1eb35-136">0 represents continuous variables and 1 represents factor variables.</span></span>

<span data-ttu-id="1eb35-137">La sortie est la probabilité qu'un événement se produise à un moment précis.</span><span class="sxs-lookup"><span data-stu-id="1eb35-137">The output is the probability of an event occurring by a specific time.</span></span> 

> <span data-ttu-id="1eb35-138">Étant hébergé sur Azure Marketplace, ce service est un service OData. Il peut être appelé à l’aide des méthodes POST ou GET.</span><span class="sxs-lookup"><span data-stu-id="1eb35-138">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="1eb35-139">Il existe plusieurs façons d’utiliser le service de manière automatique (un exemple d’application est disponible [ici](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx)).</span><span class="sxs-lookup"><span data-stu-id="1eb35-139">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx)).</span></span> 

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="1eb35-140">Début du code C# pour l'utilisation du service web :</span><span class="sxs-lookup"><span data-stu-id="1eb35-140">Starting C# code for web service consumption:</span></span>
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




<span data-ttu-id="1eb35-141">L'interprétation de ce test est la suivante.</span><span class="sxs-lookup"><span data-stu-id="1eb35-141">The interpretation of this test is as follows.</span></span> <span data-ttu-id="1eb35-142">Supposons que l’objectif des données est de modéliser le temps écoulé jusqu’à la rechute des patients ayant suivi un des deux programmes de désintoxication.</span><span class="sxs-lookup"><span data-stu-id="1eb35-142">Assuming the goal of the data is to model the elapsed time until the return to drug usage for the patients who received one of the two treatment programs.</span></span> <span data-ttu-id="1eb35-143">La sortie lue par le service web : pour les patients de 35 ans, ayant déjà suivi 2 traitements et suivant actuellement le programme de traitement résidentiel à long terme pour utilisation d’héroïne et de cocaïne, la probabilité de consommer de nouveau de la drogue est de 95,64 % au 500e jour.</span><span class="sxs-lookup"><span data-stu-id="1eb35-143">The output of the web service reads: for patients being 35 years old, having previous drug treatment 2 times, taking the long residential treatment program, and with both heroin and cocaine usage, the probability of returning to the drug usage is 95.64% by day 500.</span></span>

## <a name="creation-of-web-service"></a><span data-ttu-id="1eb35-144">Création du service web</span><span class="sxs-lookup"><span data-stu-id="1eb35-144">Creation of web service</span></span>
> <span data-ttu-id="1eb35-145">Ce service web a été créé à l’aide d’Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="1eb35-145">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="1eb35-146">Pour un essai gratuit, ainsi que des vidéos de présentation relatives à la création d’expériences et à la [publication de services web](machine-learning-publish-a-machine-learning-web-service.md), consultez [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="1eb35-146">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="1eb35-147">Voici une capture d'écran de l'expérience qui a créé le service web et l'exemple de code pour chacun des modules dans l'expérience.</span><span class="sxs-lookup"><span data-stu-id="1eb35-147">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="1eb35-148">À partir d’Azure Machine Learning, une nouvelle expérience vide a été créée et deux modules [Exécuter le script R][execute-r-script] ont été importés dans l’espace de travail.</span><span class="sxs-lookup"><span data-stu-id="1eb35-148">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules were pulled onto the workspace.</span></span> <span data-ttu-id="1eb35-149">Le schéma de données a été créé avec un simple module [Exécuter le script R][execute-r-script], qui définit le schéma de données d’entrée pour le service web.</span><span class="sxs-lookup"><span data-stu-id="1eb35-149">The data schema was created with a simple [Execute R Script][execute-r-script], which defines the input data schema for the web service.</span></span> <span data-ttu-id="1eb35-150">Ce module est ensuite lié au deuxième module [Exécuter le script R][execute-r-script] qui effectue la majeure partie du travail.</span><span class="sxs-lookup"><span data-stu-id="1eb35-150">This module is then linked to the second [Execute R Script][execute-r-script] module, which does major work.</span></span> <span data-ttu-id="1eb35-151">Ce module réalise le prétraitement des données, la création du modèle et les prédictions.</span><span class="sxs-lookup"><span data-stu-id="1eb35-151">This module does data preprocessing, model building, and predictions.</span></span> <span data-ttu-id="1eb35-152">Dans l'étape de prétraitement des données, les données d'entrée représentées par une chaîne longue sont transformées et converties en une trame de données.</span><span class="sxs-lookup"><span data-stu-id="1eb35-152">In the data preprocessing step, the input data represented by a long string is transformed and converted into a data frame.</span></span> <span data-ttu-id="1eb35-153">Dans l'étape de création du modèle, un package R externe « survival_2.37-7.zip » est tout d'abord installé pour effectuer l'analyse de survie.</span><span class="sxs-lookup"><span data-stu-id="1eb35-153">In the model building step, an external R package “survival_2.37-7.zip” is first installed for conducting survival analysis.</span></span> <span data-ttu-id="1eb35-154">La fonction « coxph » est ensuite exécutée après la tâche de traitement des données de série.</span><span class="sxs-lookup"><span data-stu-id="1eb35-154">Then the “coxph” function is executed after a series data processing tasks.</span></span> <span data-ttu-id="1eb35-155">Pour connaître les détails de la fonction « coxph » pour l’analyse de survie, consultez la documentation R.</span><span class="sxs-lookup"><span data-stu-id="1eb35-155">The details of the “coxph” function for survival analysis can be read from the R documentation.</span></span> <span data-ttu-id="1eb35-156">Dans l'étape de prédiction, une instance de test est fournie dans le modèle d'apprentissage avec la fonction « surfit » et la courbe de survie de cette instance de test est générée en tant que variable « curve ».</span><span class="sxs-lookup"><span data-stu-id="1eb35-156">In the prediction step, a testing instance is supplied into the trained model with the “surfit” function, and the survival curve for this testing instance is produced as “curve” variable.</span></span> <span data-ttu-id="1eb35-157">Enfin, vous obtenez la probabilité de la durée d'intérêt.</span><span class="sxs-lookup"><span data-stu-id="1eb35-157">Finally, the probability of the time of interest is obtained.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="1eb35-158">Flux de l’expérience :</span><span class="sxs-lookup"><span data-stu-id="1eb35-158">Experiment flow:</span></span>
![Flux de l’expérience][1]

#### <a name="module-1"></a><span data-ttu-id="1eb35-160">Module 1 :</span><span class="sxs-lookup"><span data-stu-id="1eb35-160">Module 1:</span></span>
    #Data schema with example data (replaced with data from web service)
    trainingdata="53;1;29;0;0;3,79;1;34;0;1;2,45;1;27;0;1;1,37;1;24;0;1;1,122;1;30;0;1;1,655;0;41;0;0;1,166;1;30;0;0;3,227;1;29;0;0;3,805;0;30;0;0;1,104;1;24;0;0;1,90;1;32;0;0;1,373;1;26;0;0;1,70;1;36;0;0;1”
    testingdata="35;2;1;1"
    time_of_interest="500"
    index_time="1"
    index_event="2"

    # 0 - continuous; 1 -  factor
    variable_types="0;0;1;1"

    sampleInput=data.frame(trainingdata,testingdata,time_of_interest,index_time,index_event,variable_types)

    maml.mapOutputPort("sampleInput"); #send data to output port

#### <a name="module-2"></a><span data-ttu-id="1eb35-161">Module 2 :</span><span class="sxs-lookup"><span data-stu-id="1eb35-161">Module 2:</span></span>
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

    # Prepare to build model
    attach(mydata)

    for (i in 1:n_col){ mydata[,i]=as.numeric(mydata[,i])} 
    d_time=paste("X",index_time,sep = "")
    d_event=paste("X",index_event,sep = "")
    v_time_event <- c(d_time,d_event)
    v_predictors = names(mydata)[!(names(mydata) %in% v_time_event)]

    variable_types = unlist(strsplit(as.character(variable_types),";"))

    len = length(v_predictors)
    c="" # Construct the execution string
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

    # Fit a Cox proportional hazards model and get the predicted survival curve for a testing instance 
    fit=eval(parse(text=f))

    testingdata = as.data.frame(matrix(testingdata, ncol=len,byrow = TRUE),stringsAsFactors=FALSE)
    names(testingdata)=v_predictors
    for (i in 1:len){ testingdata[,i]=as.numeric(testingdata[,i])}

    curve=survfit(fit,testingdata)

    # Based on user input, find the event occurrence probability
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

    #Pull out results to send to web service
    output=paste(round(100*output, 2), "%") 
    maml.mapOutputPort("output"); #output port




## <a name="limitations"></a><span data-ttu-id="1eb35-162">Limitations</span><span class="sxs-lookup"><span data-stu-id="1eb35-162">Limitations</span></span>
<span data-ttu-id="1eb35-163">Ce service web accepte uniquement les valeurs numériques sous forme de variables de fonctionnalité (colonnes).</span><span class="sxs-lookup"><span data-stu-id="1eb35-163">This web service can take only numerical values as feature variables (columns).</span></span> <span data-ttu-id="1eb35-164">La colonne « événement » peut uniquement avoir la valeur 0 ou 1.</span><span class="sxs-lookup"><span data-stu-id="1eb35-164">The “event” column can take only value 0 or 1.</span></span> <span data-ttu-id="1eb35-165">La colonne « temps » doit contenir un entier positif.</span><span class="sxs-lookup"><span data-stu-id="1eb35-165">The “time” column needs to be a positive integer.</span></span>

## <a name="faq"></a><span data-ttu-id="1eb35-166">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="1eb35-166">FAQ</span></span>
<span data-ttu-id="1eb35-167">Pour les questions fréquemment posées relatives à l’utilisation du service web ou à la publication sur Azure Marketplace, consultez [ce lien](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="1eb35-167">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-survival-analysis/survive_img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

