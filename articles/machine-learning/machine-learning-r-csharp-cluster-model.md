---
title: "AAA(deprecated) modèle de Cluster - Azure | Documents Microsoft"
description: "(obsolète) Modèle de cluster"
services: machine-learning
documentationcenter: 
author: FrancescaLazzeri
manager: jhubbard
editor: cgronlun
ms.assetid: 51b8d012-ed44-4312-920c-9c808dfd4ff6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: lazzeri
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 7b2dffb855a8d91114752b579115e97d07210e45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-cluster-model"></a><span data-ttu-id="84569-103">(obsolète) Modèle de cluster</span><span class="sxs-lookup"><span data-stu-id="84569-103">(deprecated) Cluster Model</span></span>

> [!NOTE]
> <span data-ttu-id="84569-104">Hello Microsoft DataMarket a été supprimée et que cette API est déconseillée.</span><span class="sxs-lookup"><span data-stu-id="84569-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="84569-105">Vous trouverez plusieurs API et les expériences d’exemple utile Bonjour [Cortana Intelligence galerie](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="84569-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="84569-106">Pour plus d’informations sur la galerie de hello, consultez [partager et découvrir des ressources Bonjour Cortana Intelligence galerie](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="84569-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="84569-107">Comment nous pouvons pour prédire les groupes de comportements de leur détenteur de crédit dans l’ordre tooreduce hello frais risque d’émetteurs de carte de crédit ?</span><span class="sxs-lookup"><span data-stu-id="84569-107">How can we predict groups of credit cardholders’ behaviors in order tooreduce hello charge-off risk of credit card issuers?</span></span> <span data-ttu-id="84569-108">Comment pouvons-nous nous définir des groupes de référence à la personnalité d’employés dans l’ordre tooimprove leurs performances au travail ?</span><span class="sxs-lookup"><span data-stu-id="84569-108">How can we define groups of personality traits of employees in order tooimprove their performance at work?</span></span> <span data-ttu-id="84569-109">Comment les médecins peuvent classifier les patients en groupes basés sur les caractéristiques de leurs diseases hello ?</span><span class="sxs-lookup"><span data-stu-id="84569-109">How can doctors classify patients into groups based on hello characteristics of their diseases?</span></span> <span data-ttu-id="84569-110">En principe, l’outil d’analyse des clusters permet d’apporter une réponse à toutes ces questions.</span><span class="sxs-lookup"><span data-stu-id="84569-110">In principle, all of these questions can be answered through cluster analysis.</span></span>   

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="84569-111">L’analyse des clusters classe un ensemble d’observations en au moins deux groupes inconnus s’excluant mutuellement, en fonction de combinaisons de variables.</span><span class="sxs-lookup"><span data-stu-id="84569-111">Cluster analysis classifies a set of observations into two or more mutually exclusive unknown groups based on combinations of variables.</span></span> <span data-ttu-id="84569-112">Hello d’analyse du cluster vise toodiscover un système d’organisation dans des groupes, des observations, généralement des personnes ou leurs caractéristiques, où des membres de groupes de hello partagent des propriétés en commun.</span><span class="sxs-lookup"><span data-stu-id="84569-112">hello purpose of cluster analysis is toodiscover a system of organizing observations, usually people or their characteristics, into groups, where members of hello groups share properties in common.</span></span> <span data-ttu-id="84569-113">Cela [service](https://datamarket.azure.com/dataset/aml_labs/k_cluster_model) utilise hello méthodologie de K-Means, une technique de clustering couramment utilisée, toocluster des données arbitraires dans des groupes.</span><span class="sxs-lookup"><span data-stu-id="84569-113">This [service](https://datamarket.azure.com/dataset/aml_labs/k_cluster_model) uses hello K-Means methodology, a commonly used clustering technique, toocluster arbitrary data into groups.</span></span> <span data-ttu-id="84569-114">Ce service web prend des données de hello et le nombre de hello de k clusters comme entrée et génère des prédictions qui de hello k groupes toowhich chaque observations appartient.</span><span class="sxs-lookup"><span data-stu-id="84569-114">This web service takes hello data and hello number of k clusters as input, and produces predictions of which of hello k groups toowhich each observations belongs.</span></span> 

> <span data-ttu-id="84569-115">Les utilisateurs peuvent potentiellement accéder à ce service web par le biais d’une application mobile, d’un site web ou même d’un ordinateur local, par exemple.</span><span class="sxs-lookup"><span data-stu-id="84569-115">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="84569-116">Mais hello objectif du service web de hello est également tooserve comme exemple illustrant comment Azure Machine Learning peuvent être des services web toocreate utilisé sur le code R.</span><span class="sxs-lookup"><span data-stu-id="84569-116">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="84569-117">Avec seulement quelques lignes de code R et quelques clics dans Azure Machine Learning Studio, vous pouvez créer une expérience avec le code R et la publier en tant que service web.</span><span class="sxs-lookup"><span data-stu-id="84569-117">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="84569-118">service web de Hello peut ensuite être publié toohello Azure Marketplace et consommé par les utilisateurs et périphériques sur Bonjour sans configuration d’infrastructure par l’auteur de hello du service web de hello.</span><span class="sxs-lookup"><span data-stu-id="84569-118">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="84569-119">Utilisation du service web</span><span class="sxs-lookup"><span data-stu-id="84569-119">Consumption of web service</span></span>
<span data-ttu-id="84569-120">Ce service web regroupe les données de hello en un ensemble de k groupes et des sorties hello affectation de groupe pour chaque ligne.</span><span class="sxs-lookup"><span data-stu-id="84569-120">This web service groups hello data into a set of k groups and outputs hello group assignment for each row.</span></span> <span data-ttu-id="84569-121">service web de Hello attend des données tooinput hello sous forme de chaîne où lignes sont séparées par des virgules (,) et les colonnes sont séparées par des points-virgules ( ;).</span><span class="sxs-lookup"><span data-stu-id="84569-121">hello web service expects hello end user tooinput data as a string where rows are separated by commas (,) and columns are separated by semicolons (;).</span></span> <span data-ttu-id="84569-122">service web de Hello attend 1 ligne à la fois.</span><span class="sxs-lookup"><span data-stu-id="84569-122">hello web service expects 1 row at a time.</span></span> <span data-ttu-id="84569-123">Un exemple de jeu de données pourrait ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="84569-123">An example dataset could look like this:</span></span>

![Exemples de données][1]

<span data-ttu-id="84569-125">Supposons que hello utilisateur souhaité tooseparate ces données en 3 groupes s’excluent mutuellement.</span><span class="sxs-lookup"><span data-stu-id="84569-125">Suppose hello user wanted tooseparate this data into 3 mutually exclusive groups.</span></span> <span data-ttu-id="84569-126">Hello des données d’entrée pour hello au-dessus de jeu de données serait suivant de hello : valeur = « 10 ; 5 ; 2,18 ; 1 ; 6,7 ; 5 ; 5,22 ; 3 ; 4,12 ; 2 ; 1,10 ; 3 ; 4 » ; k = « 3 ».</span><span class="sxs-lookup"><span data-stu-id="84569-126">hello data input for hello above dataset would be hello following: value = “10;5;2,18;1;6,7;5;5,22;3;4,12;2;1,10;3;4”; k=”3”.</span></span> <span data-ttu-id="84569-127">sortie de Hello est hello l’appartenance au groupe prévue pour chacune des lignes de hello.</span><span class="sxs-lookup"><span data-stu-id="84569-127">hello output is hello predicted group membership for each of hello rows.</span></span>

> <span data-ttu-id="84569-128">Ce service, comme hébergé sur hello Azure Marketplace, est un service OData ; Il peuvent être appelées par le biais des méthodes POST ou GET.</span><span class="sxs-lookup"><span data-stu-id="84569-128">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="84569-129">Il existe plusieurs manières de consommation de service hello de manière automatique (un exemple d’application est [ici](http://microsoftazuremachinelearning.azurewebsites.net/ClusterModel.aspx)).</span><span class="sxs-lookup"><span data-stu-id="84569-129">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/ClusterModel.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="84569-130">Début du code C# pour l'utilisation du service web :</span><span class="sxs-lookup"><span data-stu-id="84569-130">Starting C# code for web service consumption:</span></span>
    public class Input
    {
            public string value;
            public string k;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { value = TextBox1.Text, k = TextBox2.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }




## <a name="creation-of-web-service"></a><span data-ttu-id="84569-131">Création du service web</span><span class="sxs-lookup"><span data-stu-id="84569-131">Creation of web service</span></span>
> <span data-ttu-id="84569-132">Ce service web a été créé à l’aide d’Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="84569-132">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="84569-133">Pour un essai gratuit, ainsi que des vidéos de présentation relatives à la création d’expériences et à la [publication de services web](machine-learning-publish-a-machine-learning-web-service.md), consultez [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="84569-133">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="84569-134">Voici une capture d’écran d’expérience hello qui a créé un code de service et un exemple hello web pour chacun des modules hello au sein de l’expérience de hello.</span><span class="sxs-lookup"><span data-stu-id="84569-134">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="84569-135">À partir d’Azure Machine Learning, une nouvelle expérience vide a été créée et deux [Execute R Script] [ execute-r-script] extraite de modules sur l’espace de travail hello.</span><span class="sxs-lookup"><span data-stu-id="84569-135">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules pulled onto hello workspace.</span></span> <span data-ttu-id="84569-136">schéma de données Hello a été créé avec une simple [Execute R Script][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="84569-136">hello data schema was created with a simple [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="84569-137">Ensuite, schéma de données hello a été lié toohello du cluster modèle, créé à nouveau avec un [Execute R Script][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="84569-137">Then, hello data schema was linked toohello cluster model section, again created with an [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="84569-138">Bonjour [Execute R Script] [ execute-r-script] utilisé pour le modèle de cluster hello, hello web service utilise ensuite les fonction hello « k-means », qui est prédéfinie dans hello [Execute R Script] [ execute-r-script] d’Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="84569-138">In hello [Execute R Script][execute-r-script] used for hello cluster model, hello web service then utilizes hello “k-means” function, which is prebuilt into hello [Execute R Script][execute-r-script] of Azure Machine Learning.</span></span>    

![Flux de l’expérience][3]

#### <a name="module-1"></a><span data-ttu-id="84569-140">Module 1 :</span><span class="sxs-lookup"><span data-stu-id="84569-140">Module 1:</span></span>
    #Enter hello input data as a string 
    mydata <- data.frame(value = "1; 3; 5; 6; 7; 7, 5; 5; 6; 7; 2; 1, 3; 7; 2; 9; 56; 6, 1; 4; 5; 26; 4; 23, 15; 35; 6; 7; 12; 1, 32; 51; 62; 7; 21; 1", k=5, stringsAsFactors=FALSE)

    maml.mapOutputPort("mydata");     


#### <a name="module-2"></a><span data-ttu-id="84569-141">Module 2 :</span><span class="sxs-lookup"><span data-stu-id="84569-141">Module 2:</span></span>
    # Map 1-based optional input ports toovariables
    mydata <- maml.mapInputPort(1) # class: data.frame

    data.split <- strsplit(mydata[1,1], ",")[[1]]
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)
    data.split <- as.data.frame(t(data.split))

    data.split <- data.matrix(data.split)
    data.split <- data.frame(data.split)

    # K-Means cluster analysis
    fit <- kmeans(data.split, mydata$k) # k-cluster solution

    # Get cluster means 
    aggregate(data.split,by=list(fit$cluster),FUN=mean)
    # Append cluster assignment
    mydatafinal <- data.frame(t(fit$cluster))
    n_col=ncol(mydatafinal)
    colnames(mydatafinal) <- paste("V",1:n_col,sep="")

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("mydatafinal");


## <a name="limitations"></a><span data-ttu-id="84569-142">Limitations</span><span class="sxs-lookup"><span data-stu-id="84569-142">Limitations</span></span>
<span data-ttu-id="84569-143">Il s'agit d'un exemple très simple de service web de clustering.</span><span class="sxs-lookup"><span data-stu-id="84569-143">This is a very simple example of a clustering web service.</span></span> <span data-ttu-id="84569-144">Comme indiqué à partir du code d’exemple hello ci-dessus, aucune erreur interception n’est implémenté et service de hello suppose que tout est une variable continue (aucune fonctionnalité catégorielles autorisée), comme hello service uniquement les entrées numériques valeurs lors de la création de hello de ce site web hello service.</span><span class="sxs-lookup"><span data-stu-id="84569-144">As can be seen from hello example code above, no error catching is implemented and hello service assumes everything is a continuous variable (no categorical features allowed), as hello service only inputs numeric values at hello time of hello creation of this web service.</span></span> <span data-ttu-id="84569-145">En outre, service de hello gère actuellement taille limitée de données, en raison de la nature de demande/réponse toohello du service web de hello fait appel et hello que hello modèle est en cours correspondre à chaque fois hello web service est appelé.</span><span class="sxs-lookup"><span data-stu-id="84569-145">Also, hello service currently handles limited data size, due toohello request/response nature of hello web service call and hello fact that hello model is being fit every time hello web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="84569-146">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="84569-146">FAQ</span></span>
<span data-ttu-id="84569-147">Pour les questions fréquemment posées sur la consommation de service web de hello ou publication toohello Azure Marketplace, consultez [ici](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="84569-147">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-cluster-model/cluster-img1.png
[2]: ./media/machine-learning-r-csharp-cluster-model/cluster-img2.png
[3]: ./media/machine-learning-r-csharp-cluster-model/cluster-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

