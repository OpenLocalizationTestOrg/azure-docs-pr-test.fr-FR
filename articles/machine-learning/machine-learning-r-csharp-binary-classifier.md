---
title: AAA(deprecated) classifieur binaire - Azure | Documents Microsoft
description: "(obsolète) Classificateur binaire"
services: machine-learning
documentationcenter: 
author: jaymathe
manager: jhubbard
editor: cgronlun
ms.assetid: 8045038a-9dcf-44b9-a6de-7f1f8e791575
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
ms.openlocfilehash: 0496fcec9952ca243270caf67f55fe191b2dc9f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-binary-classifier"></a><span data-ttu-id="4ade9-103">(obsolète) Classificateur binaire</span><span class="sxs-lookup"><span data-stu-id="4ade9-103">(deprecated) Binary Classifier</span></span>

> [!NOTE]
> <span data-ttu-id="4ade9-104">Hello Microsoft DataMarket a été supprimée et que cette API est déconseillée.</span><span class="sxs-lookup"><span data-stu-id="4ade9-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="4ade9-105">Vous trouverez plusieurs API et les expériences d’exemple utile Bonjour [Cortana Intelligence galerie](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="4ade9-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="4ade9-106">Pour plus d’informations sur la galerie de hello, consultez [partager et découvrir des ressources Bonjour Cortana Intelligence galerie](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="4ade9-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="4ade9-107">Supposons que vous avez un jeu de données et que vous souhaitez toopredict une variable dépendante binaire en fonction des variables indépendantes de hello.</span><span class="sxs-lookup"><span data-stu-id="4ade9-107">Suppose you have a dataset and would like toopredict a binary dependent variable based on hello independent variables.</span></span> <span data-ttu-id="4ade9-108">La « régression logistique » est une technique statistique très répandue qui est utilisée pour de telles prédictions.</span><span class="sxs-lookup"><span data-stu-id="4ade9-108">‘Logistic Regression’ is a popular statistical technique used for such predictions.</span></span> <span data-ttu-id="4ade9-109">Variable dépendante de hello est binaire ou dichotomiques, et que p est probabilité hello de présence de caractéristique hello dignes d’intérêt.</span><span class="sxs-lookup"><span data-stu-id="4ade9-109">Here hello dependent variable is binary or dichotomous, and p is hello probability of presence of hello characteristic of interest.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="4ade9-110">Un scénario simple peut être où un chercheur tente toopredict si un étudiant potentiel est probablement tooaccept une université de tooa admission offre en fonction des informations (amp lycée, family revenu, état résident, sexe).</span><span class="sxs-lookup"><span data-stu-id="4ade9-110">A simple scenario could be where a researcher is trying toopredict whether a prospective student is likely tooaccept an admission offer tooa university based on information (GPA in high school, family income, resident state, gender).</span></span> <span data-ttu-id="4ade9-111">résultat prédit de Hello hello la probabilité d’est étudiant potentiel de hello accepter hello admission offre.</span><span class="sxs-lookup"><span data-stu-id="4ade9-111">hello predicted outcome is hello probability of hello prospective student accepting hello admission offer.</span></span> <span data-ttu-id="4ade9-112">Cela [service web](https://datamarket.azure.com/dataset/aml_labs/log_regression) sera ajusté hello toohello données du modèle de régression logistique et de sorties hello la valeur de probabilité (y) pour chacun des observations hello dans les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="4ade9-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/log_regression) fits hello logistic regression model toohello data and outputs hello probability value (y) for each of hello observations in hello data.</span></span>  

> <span data-ttu-id="4ade9-113">Les utilisateurs peuvent potentiellement accéder à ce service web par le biais d’une application mobile, d’un site web ou même d’un ordinateur local, par exemple.</span><span class="sxs-lookup"><span data-stu-id="4ade9-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="4ade9-114">Mais hello objectif du service web de hello est également tooserve comme exemple illustrant comment Azure Machine Learning peuvent être des services web toocreate utilisé sur le code R.</span><span class="sxs-lookup"><span data-stu-id="4ade9-114">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="4ade9-115">Avec seulement quelques lignes de code R et quelques clics dans Azure Machine Learning Studio, vous pouvez créer une expérience avec le code R et la publier en tant que service web.</span><span class="sxs-lookup"><span data-stu-id="4ade9-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="4ade9-116">service web de Hello peut ensuite être publié toohello Azure Marketplace et consommé par les utilisateurs et périphériques sur Bonjour sans configuration d’infrastructure par l’auteur de hello du service web de hello.</span><span class="sxs-lookup"><span data-stu-id="4ade9-116">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="4ade9-117">Utilisation du service web</span><span class="sxs-lookup"><span data-stu-id="4ade9-117">Consumption of web service</span></span>
<span data-ttu-id="4ade9-118">Cette hello offre de service web a prédit des valeurs de variable dépendante de hello en fonction des variables indépendantes de hello pour toutes les observations de hello.</span><span class="sxs-lookup"><span data-stu-id="4ade9-118">This web service gives hello predicted values of hello dependent variable based on hello independent variables for all of hello observations.</span></span> <span data-ttu-id="4ade9-119">service web de Hello attend des données tooinput hello sous forme de chaîne où lignes sont séparées par des virgules (,) et les colonnes sont séparées par des points-virgules ( ;).</span><span class="sxs-lookup"><span data-stu-id="4ade9-119">hello web service expects hello end user tooinput data as a string where rows are separated by comma (,) and columns are separated by semicolon (;).</span></span> <span data-ttu-id="4ade9-120">service web de Hello attend 1 ligne à la fois et attend hello première colonne toobe hello variable dépendante.</span><span class="sxs-lookup"><span data-stu-id="4ade9-120">hello web service expects 1 row at a time and expects hello first column toobe hello dependent variable.</span></span> <span data-ttu-id="4ade9-121">Un exemple de jeu de données pourrait ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="4ade9-121">An example dataset could look like this:</span></span>

![Exemples de données][1]

<span data-ttu-id="4ade9-123">Les observations sans variable dépendante doivent être entrées en tant que « NA » pour y.</span><span class="sxs-lookup"><span data-stu-id="4ade9-123">Observations without a dependent variable should be input as “NA” for y.</span></span> <span data-ttu-id="4ade9-124">Hello données d’entrée pour hello au-dessus de jeu de données serait hello après chaîne : « 1 ; 5 ; 2,1 ; 1 ; 6,0 ; 5.3 ; 2.1,0 ; 5 ; 5,0 ; 3 ; 4,1 ; 2 ; 1, NA ; 3 ; 4 ».</span><span class="sxs-lookup"><span data-stu-id="4ade9-124">hello data input for hello above dataset would be hello following string: “1;5;2,1;1;6,0;5.3;2.1,0;5;5,0;3;4,1;2;1,NA;3;4”.</span></span> <span data-ttu-id="4ade9-125">Hello sortie hello valeur prévue pour chacune des lignes de hello repose sur les variables indépendantes de hello.</span><span class="sxs-lookup"><span data-stu-id="4ade9-125">hello output is hello predicted value for each of hello rows based on hello independent variables.</span></span> 

> <span data-ttu-id="4ade9-126">Ce service, comme hébergé sur hello Azure Marketplace, est un service OData ; Il peuvent être appelées par le biais des méthodes POST ou GET.</span><span class="sxs-lookup"><span data-stu-id="4ade9-126">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="4ade9-127">Il existe plusieurs manières de consommation de service hello de manière automatique (un exemple d’application est [ici](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)).</span><span class="sxs-lookup"><span data-stu-id="4ade9-127">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="4ade9-128">Début du code C# pour l'utilisation du service web :</span><span class="sxs-lookup"><span data-stu-id="4ade9-128">Starting C# code for web service consumption:</span></span>
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


## <a name="creation-of-web-service"></a><span data-ttu-id="4ade9-129">Création du service web</span><span class="sxs-lookup"><span data-stu-id="4ade9-129">Creation of web service</span></span>
> <span data-ttu-id="4ade9-130">Ce service web a été créé à l’aide d’Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="4ade9-130">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="4ade9-131">Pour un essai gratuit, ainsi que des vidéos de présentation relatives à la création d’expériences et à la [publication de services web](machine-learning-publish-a-machine-learning-web-service.md), consultez [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="4ade9-131">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="4ade9-132">Voici une capture d’écran d’expérience hello qui a créé un code de service et un exemple hello web pour chacun des modules hello au sein de l’expérience de hello.</span><span class="sxs-lookup"><span data-stu-id="4ade9-132">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="4ade9-133">À partir d’Azure Machine Learning, une nouvelle expérience vide a été créée et deux [Execute R Script] [ execute-r-script] extraite de modules sur l’espace de travail hello.</span><span class="sxs-lookup"><span data-stu-id="4ade9-133">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules pulled onto hello workspace.</span></span> <span data-ttu-id="4ade9-134">Ce service web exécute une expérience Azure Machine Learning avec un script R sous-jacent.</span><span class="sxs-lookup"><span data-stu-id="4ade9-134">This web service runs an Azure Machine Learning experiment with an underlying R script.</span></span> <span data-ttu-id="4ade9-135">Il existe 2 parties toothis expérimenter : définition de schéma, modèle d’apprentissage et de calcul de score.</span><span class="sxs-lookup"><span data-stu-id="4ade9-135">There are 2 parts toothis experiment: schema definition, and training model + scoring.</span></span> <span data-ttu-id="4ade9-136">module de première Hello définit la structure hello attendu de dataset d’entrée hello, où hello première variable est variable dépendante de hello et autres variables de hello sont indépendantes.</span><span class="sxs-lookup"><span data-stu-id="4ade9-136">hello first module defines hello expected structure of hello input dataset, where hello first variable is hello dependent variable and hello remaining variables are independent.</span></span> <span data-ttu-id="4ade9-137">module de deuxième Hello associe un modèle de régression logistique générique pour les données d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="4ade9-137">hello second module fits a generic logistic regression model for hello input data.</span></span>    

![Flux de l’expérience][2]

#### <a name="module-1"></a><span data-ttu-id="4ade9-139">Module 1 :</span><span class="sxs-lookup"><span data-stu-id="4ade9-139">Module 1:</span></span>
    #Schema definition  
    data <- data.frame(value = "1;2;3,1;5;6,0;8;9", stringsAsFactors=FALSE) 
    maml.mapOutputPort("data");  

#### <a name="module-2"></a><span data-ttu-id="4ade9-140">Module 2 :</span><span class="sxs-lookup"><span data-stu-id="4ade9-140">Module 2:</span></span>
    #GLM modeling   
    data <- maml.mapInputPort(1) # class: data.frame  

    data.split <- strsplit(data[1,1], ",")[[1]] 
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE) 
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE) 
    data.split <- as.data.frame(t(data.split)) data.split <- 
    data.matrix(data.split) 
    data.split <- data.frame(data.split) 

    model <- glm(data.split$V1 ~., family='binomial', data=data.split)  
    out <- data.frame(predict(model,data.split, type="response")) 
    pred1 <- as.data.frame(out) 
    group <- array(1:nrow(pred1)) 
    for (i in 1:nrow(pred1))  
        {
        if(as.numeric(pred1[i,])>0.5) {group[i]=1} 
        else {group[i]=0}
        } 
    pred2 <- as.data.frame(group) 
    maml.mapOutputPort("pred2");  


## <a name="limitations"></a><span data-ttu-id="4ade9-141">Limitations</span><span class="sxs-lookup"><span data-stu-id="4ade9-141">Limitations</span></span>
<span data-ttu-id="4ade9-142">Il s'agit d'un exemple très simple de service web de classification binaire.</span><span class="sxs-lookup"><span data-stu-id="4ade9-142">This is a very simple example of a binary classification web service.</span></span> <span data-ttu-id="4ade9-143">Comme indiqué à partir du code d’exemple hello ci-dessus, aucune erreur interception n’est implémenté et service de hello suppose que tout est une variable continue/binaire (aucune fonctionnalité catégorielles autorisée), comme hello service uniquement les entrées numériques valeurs lors de la création de hello de ce hello service Web.</span><span class="sxs-lookup"><span data-stu-id="4ade9-143">As can be seen from hello example code above, no error catching is implemented and hello service assumes everything is a binary/continuous variable (no categorical features allowed), as hello service only inputs numeric values at hello time of hello creation of this web service.</span></span> <span data-ttu-id="4ade9-144">En outre, service de hello gère actuellement taille limitée de données, en raison de la nature de demande/réponse toohello du service web de hello fait appel et hello que hello modèle est en cours correspondre à chaque fois hello web service est appelé.</span><span class="sxs-lookup"><span data-stu-id="4ade9-144">Also, hello service currently handles limited data size, due toohello request/response nature of hello web service call and hello fact that hello model is being fit every time hello web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="4ade9-145">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="4ade9-145">FAQ</span></span>
<span data-ttu-id="4ade9-146">Pour les questions fréquemment posées sur la consommation de service web de hello ou publication toohello Azure Marketplace, consultez [ici](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="4ade9-146">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-binary-classifier/binary1.png
[2]: ./media/machine-learning-r-csharp-binary-classifier/binary2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

