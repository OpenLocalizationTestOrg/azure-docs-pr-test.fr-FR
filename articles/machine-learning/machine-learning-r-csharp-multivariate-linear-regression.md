---
title: "AAA(deprecated) Multivariate de régression linéaire - Azure | Documents Microsoft"
description: "(déconseillé) Régression linéaire multivariable"
services: machine-learning
documentationcenter: 
author: jaymathe
manager: jhubbard
editor: cgronlun
ms.assetid: 2fb78220-ced9-4564-a439-9e5df6772994
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: jaymathe
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 0ff7221cd06c0ef059b0c5bf327016588174dcfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-multivariate-linear-regression"></a><span data-ttu-id="4c681-103">(déconseillé) Régression linéaire multivariable</span><span class="sxs-lookup"><span data-stu-id="4c681-103">(deprecated) Multivariate Linear Regression</span></span>

> [!NOTE]
> <span data-ttu-id="4c681-104">Hello Microsoft DataMarket a été supprimée et que cette API est déconseillée.</span><span class="sxs-lookup"><span data-stu-id="4c681-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="4c681-105">Vous trouverez plusieurs API et les expériences d’exemple utile Bonjour [Cortana Intelligence galerie](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="4c681-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="4c681-106">Pour plus d’informations sur la galerie de hello, consultez [partager et découvrir des ressources Bonjour Cortana Intelligence galerie](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="4c681-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="4c681-107">Supposons que vous avez un jeu de données serez comme tooquickly prédire une variable dépendante (y) pour chaque personne (i) en fonction de variables indépendantes.</span><span class="sxs-lookup"><span data-stu-id="4c681-107">Suppose you have a dataset and would like tooquickly predict a dependent variable (y) for each individual (i) based on independent variables.</span></span> <span data-ttu-id="4c681-108">La régression linéaire est une technique statistique répandue qui est utilisée pour de telles prédictions.</span><span class="sxs-lookup"><span data-stu-id="4c681-108">Linear regression is a popular statistical technique used for such predictions.</span></span> <span data-ttu-id="4c681-109">Ici, hello variable dépendante y est supposé toobe une valeur continue.</span><span class="sxs-lookup"><span data-stu-id="4c681-109">Here hello dependent variable y is assumed toobe a continuous value.</span></span>  

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="4c681-110">Un scénario simple peut être où chercheur de hello tente de poids de hello toopredict d’un individu (y) en fonction de leur hauteur (x).</span><span class="sxs-lookup"><span data-stu-id="4c681-110">A simple scenario could be where hello researcher is trying toopredict hello weight of an individual (y) based on their height (x).</span></span> <span data-ttu-id="4c681-111">Un scénario plus avancé peut être où chercheur de hello comporte des informations supplémentaires pour hello individuel (par exemple, le poids, sexe, course) et tente de poids hello toopredict hello individuels.</span><span class="sxs-lookup"><span data-stu-id="4c681-111">A more advanced scenario could be where hello researcher has additional information for hello individual (such as weight, gender, race) and attempts toopredict hello weight of hello individual.</span></span> <span data-ttu-id="4c681-112">Cela [service web](https://datamarket.azure.com/dataset/aml_labs/multivariate_regression) sera ajusté hello toohello données du modèle de régression linéaire et sorties hello valeur prédite (y) pour chacun des observations hello dans les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="4c681-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/multivariate_regression) fits hello linear regression model toohello data and outputs hello predicted value (y) for each of hello observations in hello data.</span></span>

> <span data-ttu-id="4c681-113">Les utilisateurs peuvent potentiellement accéder à ce service web par le biais d’une application mobile, d’un site web ou même d’un ordinateur local, par exemple.</span><span class="sxs-lookup"><span data-stu-id="4c681-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="4c681-114">Mais hello objectif du service web de hello est également tooserve comme exemple illustrant comment Azure Machine Learning peuvent être des services web toocreate utilisé sur le code R.</span><span class="sxs-lookup"><span data-stu-id="4c681-114">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="4c681-115">Avec seulement quelques lignes de code R et quelques clics dans Azure Machine Learning Studio, vous pouvez créer une expérience avec le code R et la publier en tant que service web.</span><span class="sxs-lookup"><span data-stu-id="4c681-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="4c681-116">service web de Hello peut ensuite être publié toohello Azure Marketplace et consommé par les utilisateurs et périphériques sur Bonjour sans configuration d’infrastructure par l’auteur de hello du service web de hello.</span><span class="sxs-lookup"><span data-stu-id="4c681-116">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="4c681-117">Utilisation du service web</span><span class="sxs-lookup"><span data-stu-id="4c681-117">Consumption of web service</span></span>
<span data-ttu-id="4c681-118">Cette hello offre de service web a prédit des valeurs de variable dépendante de hello en fonction des variables indépendantes de hello pour toutes les observations de hello.</span><span class="sxs-lookup"><span data-stu-id="4c681-118">This web service gives hello predicted values of hello dependent variable based on hello independent variables for all of hello observations.</span></span> <span data-ttu-id="4c681-119">service web de Hello attend des données tooinput hello sous forme de chaîne où lignes sont séparées par des virgules (,) et les colonnes sont séparées par des points-virgules ( ;).</span><span class="sxs-lookup"><span data-stu-id="4c681-119">hello web service expects hello end user tooinput data as a string where rows are separated by commas (,) and columns are separated by semicolons (;).</span></span> <span data-ttu-id="4c681-120">service web de Hello attend 1 ligne à la fois et attend hello première colonne toobe hello variable dépendante.</span><span class="sxs-lookup"><span data-stu-id="4c681-120">hello web service expects 1 row at a time and expects hello first column toobe hello dependent variable.</span></span> <span data-ttu-id="4c681-121">Un exemple de jeu de données pourrait ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="4c681-121">An example dataset could look like this:</span></span>

![Exemples de données][1]

<span data-ttu-id="4c681-123">Les observations sans variable dépendante doivent être entrées en tant que « NA » pour y.</span><span class="sxs-lookup"><span data-stu-id="4c681-123">Observations without a dependent variable should be input as “NA” for y.</span></span> <span data-ttu-id="4c681-124">Hello données d’entrée pour hello au-dessus de jeu de données serait hello après chaîne : « 10 ; 5 2,18 ; 1 ; 6,6 ; 5.3 ; 2.1,7 ; 5 ; 5,22 ; 3 ; 4,12 ; 2 ; 1, NA, 3, 4 ».</span><span class="sxs-lookup"><span data-stu-id="4c681-124">hello data input for hello above dataset would be hello following string: “10;5;2,18;1;6,6;5.3;2.1,7;5;5,22;3;4,12;2;1,NA;3;4”.</span></span> <span data-ttu-id="4c681-125">Hello sortie hello valeur prévue pour chacune des lignes de hello repose sur les variables indépendantes de hello.</span><span class="sxs-lookup"><span data-stu-id="4c681-125">hello output is hello predicted value for each of hello rows based on hello independent variables.</span></span> 

> <span data-ttu-id="4c681-126">Ce service, comme hébergé sur hello Azure Marketplace, est un service OData ; Il peuvent être appelées par le biais des méthodes POST ou GET.</span><span class="sxs-lookup"><span data-stu-id="4c681-126">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="4c681-127">Il existe plusieurs manières de consommation de service hello de manière automatique (un exemple d’application est [ici](http://microsoftazuremachinelearning.azurewebsites.net/MultipleLinearRegressionService.aspx)).</span><span class="sxs-lookup"><span data-stu-id="4c681-127">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/MultipleLinearRegressionService.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="4c681-128">Début du code C# pour l'utilisation du service web :</span><span class="sxs-lookup"><span data-stu-id="4c681-128">Starting C# code for web service consumption:</span></span>
    public class Input
    {
            public string value;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { value = TextBox1.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }




## <a name="creation-of-web-service"></a><span data-ttu-id="4c681-129">Création du service web</span><span class="sxs-lookup"><span data-stu-id="4c681-129">Creation of web service</span></span>
> <span data-ttu-id="4c681-130">Ce service web a été créé à l’aide d’Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="4c681-130">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="4c681-131">Pour un essai gratuit, ainsi que des vidéos de présentation relatives à la création d’expériences et à la [publication de services web](machine-learning-publish-a-machine-learning-web-service.md), consultez [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="4c681-131">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="4c681-132">Voici une capture d’écran d’expérience hello qui a créé un code de service et un exemple hello web pour chacun des modules hello au sein de l’expérience de hello.</span><span class="sxs-lookup"><span data-stu-id="4c681-132">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="4c681-133">À partir d’Azure Machine Learning, une nouvelle expérience vide a été créée et deux [Execute R Script] [ execute-r-script] modules ont été collectés dans l’espace de travail hello.</span><span class="sxs-lookup"><span data-stu-id="4c681-133">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules were pulled onto hello workspace.</span></span> <span data-ttu-id="4c681-134">Ce service web exécute une expérience Azure Machine Learning avec un script R sous-jacent.</span><span class="sxs-lookup"><span data-stu-id="4c681-134">This web service runs an Azure Machine Learning experiment with an underlying R script.</span></span> <span data-ttu-id="4c681-135">Il existe 2 parties toothis expérimenter : définition de schéma, modèle d’apprentissage et de calcul de score.</span><span class="sxs-lookup"><span data-stu-id="4c681-135">There are 2 parts toothis experiment: schema definition, and training model + scoring.</span></span> <span data-ttu-id="4c681-136">module de première Hello définit la structure hello attendu de dataset d’entrée hello, où hello première variable est variable dépendante de hello et autres variables de hello sont indépendantes.</span><span class="sxs-lookup"><span data-stu-id="4c681-136">hello first module defines hello expected structure of hello input dataset, where hello first variable is hello dependent variable and hello remaining variables are independent.</span></span> <span data-ttu-id="4c681-137">module de deuxième Hello associe un modèle de régression linéaire générique pour les données d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="4c681-137">hello second module fits a generic linear regression model for hello input data.</span></span>  

![Flux de l’expérience][3]

#### <a name="module-1"></a><span data-ttu-id="4c681-139">Module 1 :</span><span class="sxs-lookup"><span data-stu-id="4c681-139">Module 1:</span></span>
#### <a name="schema-definition"></a><span data-ttu-id="4c681-140">Définition de schéma</span><span class="sxs-lookup"><span data-stu-id="4c681-140">Schema definition</span></span>
    data <- data.frame(value = "1;2;3,4;5;6,7;8;9", stringsAsFactors=FALSE) maml.mapOutputPort("data");  

#### <a name="module-2"></a><span data-ttu-id="4c681-141">Module 2 :</span><span class="sxs-lookup"><span data-stu-id="4c681-141">Module 2:</span></span>
#### <a name="lm-modeling"></a><span data-ttu-id="4c681-142">Modélisation LM</span><span class="sxs-lookup"><span data-stu-id="4c681-142">LM modeling</span></span>
    data <- maml.mapInputPort(1) # class: data.frame  

    data.split <- strsplit(data[1,1], ",")[[1]]  
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)  
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)  
    data.split <- as.data.frame(t(data.split)) 
    data.split <- data.matrix(data.split) 
    data.split <- data.frame(data.split) 
    model <- lm(data.split)  

    out=data.frame(predict(model,data.split))  
    out <- data.frame(t(out))

    maml.mapOutputPort("out");  

## <a name="limitations"></a><span data-ttu-id="4c681-143">Limitations</span><span class="sxs-lookup"><span data-stu-id="4c681-143">Limitations</span></span>
<span data-ttu-id="4c681-144">Il s'agit d'un exemple très simple de service web pour régressions linéaires multiples.</span><span class="sxs-lookup"><span data-stu-id="4c681-144">This is a very simple example of a multiple linear regression web service.</span></span> <span data-ttu-id="4c681-145">Comme indiqué à partir du code d’exemple hello ci-dessus, aucune erreur interception n’est implémenté et service de hello suppose que tout est une variable continue (aucune fonctionnalité catégorielles autorisée), comme hello service uniquement les entrées numériques valeurs lors de la création de hello de ce site web hello service.</span><span class="sxs-lookup"><span data-stu-id="4c681-145">As can be seen from hello example code above, no error catching is implemented and hello service assumes everything is a continuous variable (no categorical features allowed), as hello service only inputs numeric values at hello time of hello creation of this web service.</span></span> <span data-ttu-id="4c681-146">En outre, service de hello gère actuellement taille limitée de données, en raison de la nature de demande/réponse toohello du service web de hello fait appel et hello que hello modèle est en cours correspondre à chaque fois hello web service est appelé.</span><span class="sxs-lookup"><span data-stu-id="4c681-146">Also, hello service currently handles limited data size, due toohello request/response nature of hello web service call and hello fact that hello model is being fit every time hello web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="4c681-147">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="4c681-147">FAQ</span></span>
<span data-ttu-id="4c681-148">Pour les questions fréquemment posées sur la consommation de service web de hello ou publication toohello Azure Marketplace, consultez [ici](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="4c681-148">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img1.png
[2]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img2.png
[3]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

