---
title: "AAA(deprecated) différence dans les Proportions Test - Azure | Documents Microsoft"
description: "(obsolète) Test de différence des proportions"
services: machine-learning
documentationcenter: 
author: aniedea
manager: jhubbard
editor: cgronlun
ms.assetid: 9356b821-5345-44f6-8e26-719f2dea5e6d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: aniedea
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 820aad377f9dec12b0ef455974aaa95f6e8d723a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-difference-in-proportions-test"></a><span data-ttu-id="0dc1d-103">(obsolète) Test de différence des proportions</span><span class="sxs-lookup"><span data-stu-id="0dc1d-103">(deprecated) Difference in Proportions Test</span></span>

> [!NOTE]
> <span data-ttu-id="0dc1d-104">Hello Microsoft DataMarket a été supprimée et que cette API est déconseillée.</span><span class="sxs-lookup"><span data-stu-id="0dc1d-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="0dc1d-105">Vous trouverez plusieurs API et les expériences d’exemple utile Bonjour [Cortana Intelligence galerie](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="0dc1d-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="0dc1d-106">Pour plus d’informations sur la galerie de hello, consultez [partager et découvrir des ressources Bonjour Cortana Intelligence galerie](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="0dc1d-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="0dc1d-107">Deux proportions sont-elles différentes d'un point de vue statistique ?</span><span class="sxs-lookup"><span data-stu-id="0dc1d-107">Are two proportions statistically different?</span></span> <span data-ttu-id="0dc1d-108">Supposons qu’un utilisateur souhaite toocompare deux films toodetermine si un nombre beaucoup plus élevé d’un film « aime » lorsque comparées toohello autres.</span><span class="sxs-lookup"><span data-stu-id="0dc1d-108">Suppose a user wants toocompare two movies toodetermine if one movie has a significantly higher proportion of ‘likes’ when compared toohello other.</span></span> <span data-ttu-id="0dc1d-109">Avec un exemple de grande taille, il peut y avoir une différence statistiquement significative entre des proportions hello 0,50 et 0.51.</span><span class="sxs-lookup"><span data-stu-id="0dc1d-109">With a large sample, there could be a statistically significant difference between hello proportions 0.50 and 0.51.</span></span> <span data-ttu-id="0dc1d-110">Avec un petit échantillon, il peut-être pas suffisamment toodetermine de données si ces proportions sont réellement différentes.</span><span class="sxs-lookup"><span data-stu-id="0dc1d-110">With a small sample, there may not be enough data toodetermine if these proportions are actually different.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="0dc1d-111">Cela [service web](https://datamarket.azure.com/dataset/aml_labs/prop_test) effectue un test d’hypothèse de différence hello dans des deux proportions en fonction de l’entrée d’utilisateur de nombre hello de succès et le nombre total de hello d’essais pour les groupes de comparaison hello 2.</span><span class="sxs-lookup"><span data-stu-id="0dc1d-111">This [web service](https://datamarket.azure.com/dataset/aml_labs/prop_test) conducts a hypothesis test of hello difference in two proportions based on user input of hello number of successes and hello total number of trials for hello 2 comparison groups.</span></span> <span data-ttu-id="0dc1d-112">Dans un scénario possible, ce service web peut être appelé à partir d’au sein d’une application de comparaison de film, indiquant les utilisateur hello si un des films de hello est vraiment 'aimé' plus souvent que hello autre, en fonction de classification des films.</span><span class="sxs-lookup"><span data-stu-id="0dc1d-112">In one possible scenario, this web service could be called from within a movie comparison app, telling hello user whether one of hello movies is really ‘liked’ more often than hello other, based on movie ratings.</span></span>

> <span data-ttu-id="0dc1d-113">Les utilisateurs peuvent potentiellement accéder à ce service web par le biais d’une application mobile, d’un site web ou même d’un ordinateur local, par exemple.</span><span class="sxs-lookup"><span data-stu-id="0dc1d-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="0dc1d-114">Mais hello objectif du service web de hello est également tooserve comme exemple illustrant comment Azure Machine Learning peuvent être des services web toocreate utilisé sur le code R.</span><span class="sxs-lookup"><span data-stu-id="0dc1d-114">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="0dc1d-115">Avec seulement quelques lignes de code R et quelques clics dans Azure Machine Learning Studio, vous pouvez créer une expérience avec le code R et la publier en tant que service web.</span><span class="sxs-lookup"><span data-stu-id="0dc1d-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="0dc1d-116">service web de Hello peut ensuite être publié toohello Azure Marketplace et consommé par les utilisateurs et périphériques sur Bonjour sans configuration d’infrastructure par l’auteur de hello du service web de hello.</span><span class="sxs-lookup"><span data-stu-id="0dc1d-116">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="0dc1d-117">Utilisation du service web</span><span class="sxs-lookup"><span data-stu-id="0dc1d-117">Consumption of web service</span></span>
<span data-ttu-id="0dc1d-118">Ce service accepte 4 arguments et effectue un test d'hypothèse des proportions.</span><span class="sxs-lookup"><span data-stu-id="0dc1d-118">This service accepts 4 arguments and does a hypothesis test of proportions.</span></span>

<span data-ttu-id="0dc1d-119">les arguments d’entrée Hello sont :</span><span class="sxs-lookup"><span data-stu-id="0dc1d-119">hello input arguments are:</span></span>

* <span data-ttu-id="0dc1d-120">Successes1 : nombre d’événements de succès dans l’échantillon 1</span><span class="sxs-lookup"><span data-stu-id="0dc1d-120">Successes1 - Number of success events in sample 1.</span></span>
* <span data-ttu-id="0dc1d-121">Successes2 : nombre d’événements de succès dans l’échantillon 2</span><span class="sxs-lookup"><span data-stu-id="0dc1d-121">Successes2 - Number of success events in sample 2.</span></span>
* <span data-ttu-id="0dc1d-122">Total1 - taille de l’échantillon 1.</span><span class="sxs-lookup"><span data-stu-id="0dc1d-122">Total1 -  Size of sample 1.</span></span>
* <span data-ttu-id="0dc1d-123">Total2 : taille de l’échantillon 2</span><span class="sxs-lookup"><span data-stu-id="0dc1d-123">Total2 - Size of sample 2.</span></span>

<span data-ttu-id="0dc1d-124">sortie Hello du service de hello résulte de hello d’hypothèse de hello avec hello appel statistique, df, p-valeur de test et proportion dans les limites du 1/2 et l’intervalle de confiance exemple.</span><span class="sxs-lookup"><span data-stu-id="0dc1d-124">hello output of hello service is hello result of hello hypothesis test along with hello chi-square statistic, df, p-value, and proportion in sample 1/2 and confidence interval bounds.</span></span>

> <span data-ttu-id="0dc1d-125">Ce service, comme hébergé sur hello Azure Marketplace, est un service OData ; Il peuvent être appelées par le biais des méthodes POST ou GET.</span><span class="sxs-lookup"><span data-stu-id="0dc1d-125">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="0dc1d-126">Il existe plusieurs manières de consommation de service hello de manière automatique (un exemple d’application est [ici](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx)).</span><span class="sxs-lookup"><span data-stu-id="0dc1d-126">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="0dc1d-127">Début du code C# pour l'utilisation du service web :</span><span class="sxs-lookup"><span data-stu-id="0dc1d-127">Starting C# code for web service consumption:</span></span>
    public class Input
    {
            public string successes1;
            public string successes2;
            public string total1;
            public string total2;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { successes1 = TextBox1.Text, successes2 = TextBox2.Text, total1 = TextBox3.Text, total2 = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


## <a name="creation-of-web-service"></a><span data-ttu-id="0dc1d-128">Création du service web</span><span class="sxs-lookup"><span data-stu-id="0dc1d-128">Creation of web service</span></span>
> <span data-ttu-id="0dc1d-129">Ce service web a été créé à l’aide d’Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="0dc1d-129">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="0dc1d-130">Pour un essai gratuit, ainsi que des vidéos de présentation relatives à la création d’expériences et à la [publication de services web](machine-learning-publish-a-machine-learning-web-service.md), consultez [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="0dc1d-130">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="0dc1d-131">Voici une capture d’écran d’expérience hello qui a créé un code de service et un exemple hello web pour chacun des modules hello au sein de l’expérience de hello.</span><span class="sxs-lookup"><span data-stu-id="0dc1d-131">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="0dc1d-132">À partir d’Azure Machine Learning, une nouvelle expérience vide a été créée avec deux modules [Exécuter le script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="0dc1d-132">From within Azure Machine Learning, a new blank experiment was created with two [Execute R Script][execute-r-script] modules.</span></span> <span data-ttu-id="0dc1d-133">Dans le module de première hello schéma de données hello est défini, que la deuxième du module hello utilise commande hello prop.test test d’hypothèse R tooperform hello pour 2 proportions.</span><span class="sxs-lookup"><span data-stu-id="0dc1d-133">In hello first module hello data schema is defined, while hello second module uses hello prop.test command within R tooperform hello hypothesis test for 2 proportions.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="0dc1d-134">Flux de l’expérience :</span><span class="sxs-lookup"><span data-stu-id="0dc1d-134">Experiment flow:</span></span>
![Flux de l’expérience][2]

#### <a name="module-1"></a><span data-ttu-id="0dc1d-136">Module 1 :</span><span class="sxs-lookup"><span data-stu-id="0dc1d-136">Module 1:</span></span>
    ####Schema definition  
    data.set=data.frame(successes1=50,successes2=60,total1=100,total2=100);
    maml.mapOutputPort("data.set"); #send data toooutput port
    dataset1 = maml.mapInputPort(1) #read data from input port


#### <a name="module-2"></a><span data-ttu-id="0dc1d-137">Module 2 :</span><span class="sxs-lookup"><span data-stu-id="0dc1d-137">Module 2:</span></span>
    test=prop.test(c(dataset1$successes1[1],dataset1$successes2[1]),c(dataset1$total1[1],dataset1$total2[1])) #conduct hypothesis test

    result=data.frame(
    result=ifelse(test$p.value<0.05,"hello proportions are different!",
    "hello proportions aren't different statistically."),
    ChiSquarestatistic=round(test$statistic,2),df=test$parameter,
    pvalue=round(test$p.value,4),
    proportion1=round(test$estimate[1],4),
    proportion2=round(test$estimate[2],4),
    confintlow=round(test$conf.int[1],4),
    confinthigh=round(test$conf.int[2],4)) 

    maml.mapOutputPort("result"); #output port


## <a name="limitations"></a><span data-ttu-id="0dc1d-138">Limitations</span><span class="sxs-lookup"><span data-stu-id="0dc1d-138">Limitations</span></span>
<span data-ttu-id="0dc1d-139">Il s’agit d’un exemple très simple permettant de tester la différence dans 2 proportions.</span><span class="sxs-lookup"><span data-stu-id="0dc1d-139">This is a very simple example for a test of difference in 2 proportions.</span></span> <span data-ttu-id="0dc1d-140">Comme indiqué à partir du code d’exemple hello ci-dessus, aucune erreur interception n’est implémenté et service de hello suppose que toutes les variables de hello sont continues.</span><span class="sxs-lookup"><span data-stu-id="0dc1d-140">As can be seen from hello example code above, no error catching is implemented and hello service assumes that all hello variables are continuous.</span></span>

## <a name="faq"></a><span data-ttu-id="0dc1d-141">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="0dc1d-141">FAQ</span></span>
<span data-ttu-id="0dc1d-142">Pour les questions fréquemment posées sur la consommation de service web de hello ou publication toohello Azure Marketplace, consultez [ici](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="0dc1d-142">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img1.png
[2]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

