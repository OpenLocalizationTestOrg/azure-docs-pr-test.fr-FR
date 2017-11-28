---
title: "(obsolète) Test de différence des proportions - Azure | Microsoft Docs"
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
redirect_document_id: TRUE
ms.openlocfilehash: a08f91ca76eef2562caeb9eb64cec5e549ed2f5f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-difference-in-proportions-test"></a><span data-ttu-id="ff938-103">(obsolète) Test de différence des proportions</span><span class="sxs-lookup"><span data-stu-id="ff938-103">(deprecated) Difference in Proportions Test</span></span>

> [!NOTE]
> <span data-ttu-id="ff938-104">Microsoft DataMarket va être supprimé et cette API est désormais obsolète.</span><span class="sxs-lookup"><span data-stu-id="ff938-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="ff938-105">Vous trouverez de nombreux exemples d’expériences et d’API dans la [galerie Cortana Intelligence](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="ff938-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="ff938-106">Pour plus d’informations sur la galerie, consultez [Partager et découvrir des solutions dans la galerie Cortana Intelligence](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="ff938-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="ff938-107">Deux proportions sont-elles différentes d'un point de vue statistique ?</span><span class="sxs-lookup"><span data-stu-id="ff938-107">Are two proportions statistically different?</span></span> <span data-ttu-id="ff938-108">Supposons qu'un utilisateur souhaite comparer deux films pour déterminer si l'un présente une proportion nettement supérieure de « J'aime » par rapport à l'autre.</span><span class="sxs-lookup"><span data-stu-id="ff938-108">Suppose a user wants to compare two movies to determine if one movie has a significantly higher proportion of ‘likes’ when compared to the other.</span></span> <span data-ttu-id="ff938-109">Avec un échantillon de grande taille, il peut exister une différence statistiquement importante entre les proportions 0,50 et 0,51.</span><span class="sxs-lookup"><span data-stu-id="ff938-109">With a large sample, there could be a statistically significant difference between the proportions 0.50 and 0.51.</span></span> <span data-ttu-id="ff938-110">Avec un petit échantillon, il peut ne pas y avoir suffisamment de données pour déterminer si ces proportions sont réellement différentes.</span><span class="sxs-lookup"><span data-stu-id="ff938-110">With a small sample, there may not be enough data to determine if these proportions are actually different.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="ff938-111">Ce [service web](https://datamarket.azure.com/dataset/aml_labs/prop_test) effectue un test d’hypothèse de la différence entre deux proportions basé sur le nombre de réussites entré par l’utilisateur et le nombre total d’essais pour les 2 groupes de comparaison.</span><span class="sxs-lookup"><span data-stu-id="ff938-111">This [web service](https://datamarket.azure.com/dataset/aml_labs/prop_test) conducts a hypothesis test of the difference in two proportions based on user input of the number of successes and the total number of trials for the 2 comparison groups.</span></span> <span data-ttu-id="ff938-112">Exemple de scénario possible : ce service web pourrait être appelé à partir d’une application de comparaison de films afin d’indiquer à l’utilisateur si un film est vraiment « aimé » plus souvent que les autres, en fonction de la classification des films.</span><span class="sxs-lookup"><span data-stu-id="ff938-112">In one possible scenario, this web service could be called from within a movie comparison app, telling the user whether one of the movies is really ‘liked’ more often than the other, based on movie ratings.</span></span>

> <span data-ttu-id="ff938-113">Les utilisateurs peuvent potentiellement accéder à ce service web par le biais d’une application mobile, d’un site web ou même d’un ordinateur local, par exemple.</span><span class="sxs-lookup"><span data-stu-id="ff938-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="ff938-114">Mais l’objectif du service web est également de servir d’exemple d’utilisation d’Azure Machine Learning pour créer des services web avec le code R.</span><span class="sxs-lookup"><span data-stu-id="ff938-114">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="ff938-115">Avec seulement quelques lignes de code R et quelques clics dans Azure Machine Learning Studio, vous pouvez créer une expérience avec le code R et la publier en tant que service web.</span><span class="sxs-lookup"><span data-stu-id="ff938-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="ff938-116">Le service web peut ensuite être publié sur Azure Marketplace afin que les utilisateurs et les appareils du monde entier l’utilisent sans que l’auteur du service web n’ait à configurer l’infrastructure.</span><span class="sxs-lookup"><span data-stu-id="ff938-116">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="ff938-117">Utilisation du service web</span><span class="sxs-lookup"><span data-stu-id="ff938-117">Consumption of web service</span></span>
<span data-ttu-id="ff938-118">Ce service accepte 4 arguments et effectue un test d'hypothèse des proportions.</span><span class="sxs-lookup"><span data-stu-id="ff938-118">This service accepts 4 arguments and does a hypothesis test of proportions.</span></span>

<span data-ttu-id="ff938-119">Les arguments d'entrée sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="ff938-119">The input arguments are:</span></span>

* <span data-ttu-id="ff938-120">Successes1 : nombre d’événements de succès dans l’échantillon 1</span><span class="sxs-lookup"><span data-stu-id="ff938-120">Successes1 - Number of success events in sample 1.</span></span>
* <span data-ttu-id="ff938-121">Successes2 : nombre d’événements de succès dans l’échantillon 2</span><span class="sxs-lookup"><span data-stu-id="ff938-121">Successes2 - Number of success events in sample 2.</span></span>
* <span data-ttu-id="ff938-122">Total1 - taille de l’échantillon 1.</span><span class="sxs-lookup"><span data-stu-id="ff938-122">Total1 -  Size of sample 1.</span></span>
* <span data-ttu-id="ff938-123">Total2 : taille de l’échantillon 2</span><span class="sxs-lookup"><span data-stu-id="ff938-123">Total2 - Size of sample 2.</span></span>

<span data-ttu-id="ff938-124">La sortie du service correspond au résultat du test d’hypothèse, ainsi qu’à la statistique de khi carré, la fraction décimale, la valeur p, la proportion dans l’échantillon 1/2 et les limites d’intervalle de confiance.</span><span class="sxs-lookup"><span data-stu-id="ff938-124">The output of the service is the result of the hypothesis test along with the chi-square statistic, df, p-value, and proportion in sample 1/2 and confidence interval bounds.</span></span>

> <span data-ttu-id="ff938-125">Étant hébergé sur Azure Marketplace, ce service est un service OData. Il peut être appelé à l’aide des méthodes POST ou GET.</span><span class="sxs-lookup"><span data-stu-id="ff938-125">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="ff938-126">Il existe plusieurs façons d’utiliser le service de manière automatique (un exemple d’application est disponible [ici](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx)).</span><span class="sxs-lookup"><span data-stu-id="ff938-126">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="ff938-127">Début du code C# pour l'utilisation du service web :</span><span class="sxs-lookup"><span data-stu-id="ff938-127">Starting C# code for web service consumption:</span></span>
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


## <a name="creation-of-web-service"></a><span data-ttu-id="ff938-128">Création du service web</span><span class="sxs-lookup"><span data-stu-id="ff938-128">Creation of web service</span></span>
> <span data-ttu-id="ff938-129">Ce service web a été créé à l’aide d’Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="ff938-129">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="ff938-130">Pour un essai gratuit, ainsi que des vidéos de présentation relatives à la création d’expériences et à la [publication de services web](machine-learning-publish-a-machine-learning-web-service.md), consultez [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="ff938-130">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="ff938-131">Voici une capture d'écran de l'expérience qui a créé le service web et l'exemple de code pour chacun des modules dans l'expérience.</span><span class="sxs-lookup"><span data-stu-id="ff938-131">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="ff938-132">À partir d’Azure Machine Learning, une nouvelle expérience vide a été créée avec deux modules [Exécuter le script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="ff938-132">From within Azure Machine Learning, a new blank experiment was created with two [Execute R Script][execute-r-script] modules.</span></span> <span data-ttu-id="ff938-133">Dans le premier module, le schéma de données est défini alors que le second module utilise la commande prop.test dans R pour effectuer le test d’hypothèse pour 2 proportions.</span><span class="sxs-lookup"><span data-stu-id="ff938-133">In the first module the data schema is defined, while the second module uses the prop.test command within R to perform the hypothesis test for 2 proportions.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="ff938-134">Flux de l’expérience :</span><span class="sxs-lookup"><span data-stu-id="ff938-134">Experiment flow:</span></span>
![Flux de l’expérience][2]

#### <a name="module-1"></a><span data-ttu-id="ff938-136">Module 1 :</span><span class="sxs-lookup"><span data-stu-id="ff938-136">Module 1:</span></span>
    ####Schema definition  
    data.set=data.frame(successes1=50,successes2=60,total1=100,total2=100);
    maml.mapOutputPort("data.set"); #send data to output port
    dataset1 = maml.mapInputPort(1) #read data from input port


#### <a name="module-2"></a><span data-ttu-id="ff938-137">Module 2 :</span><span class="sxs-lookup"><span data-stu-id="ff938-137">Module 2:</span></span>
    test=prop.test(c(dataset1$successes1[1],dataset1$successes2[1]),c(dataset1$total1[1],dataset1$total2[1])) #conduct hypothesis test

    result=data.frame(
    result=ifelse(test$p.value<0.05,"The proportions are different!",
    "The proportions aren't different statistically."),
    ChiSquarestatistic=round(test$statistic,2),df=test$parameter,
    pvalue=round(test$p.value,4),
    proportion1=round(test$estimate[1],4),
    proportion2=round(test$estimate[2],4),
    confintlow=round(test$conf.int[1],4),
    confinthigh=round(test$conf.int[2],4)) 

    maml.mapOutputPort("result"); #output port


## <a name="limitations"></a><span data-ttu-id="ff938-138">Limitations</span><span class="sxs-lookup"><span data-stu-id="ff938-138">Limitations</span></span>
<span data-ttu-id="ff938-139">Il s’agit d’un exemple très simple permettant de tester la différence dans 2 proportions.</span><span class="sxs-lookup"><span data-stu-id="ff938-139">This is a very simple example for a test of difference in 2 proportions.</span></span> <span data-ttu-id="ff938-140">Comme illustré dans l'exemple de code ci-dessus, aucune interception des erreurs n'est implémentée et le service suppose que toutes les variables sont continues.</span><span class="sxs-lookup"><span data-stu-id="ff938-140">As can be seen from the example code above, no error catching is implemented and the service assumes that all the variables are continuous.</span></span>

## <a name="faq"></a><span data-ttu-id="ff938-141">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="ff938-141">FAQ</span></span>
<span data-ttu-id="ff938-142">Pour les questions fréquemment posées relatives à l’utilisation du service web ou à la publication sur Azure Marketplace, consultez [ce lien](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="ff938-142">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img1.png
[2]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

