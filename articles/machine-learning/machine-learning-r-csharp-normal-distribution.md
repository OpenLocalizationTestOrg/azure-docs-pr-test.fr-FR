---
title: "(obsolète) Suite de services web de distribution normale - Azure | Microsoft Docs"
description: "(obsolète) Suite de services web de distribution normale"
services: machine-learning
documentationcenter: 
author: ireiter
manager: jhubbard
editor: cgronlun
ms.assetid: aab7b92e-953b-43d8-b0af-031394406bfe
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: ireiter
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: TRUE
ms.openlocfilehash: 79d1621330ad56b0c62ca46cfac424c2306e371f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-normal-distribution-suite"></a><span data-ttu-id="88e77-103">(obsolète) Suite de distribution normale</span><span class="sxs-lookup"><span data-stu-id="88e77-103">(deprecated) Normal Distribution Suite</span></span>

> [!NOTE]
> <span data-ttu-id="88e77-104">Microsoft DataMarket va être supprimé et cette API est désormais obsolète.</span><span class="sxs-lookup"><span data-stu-id="88e77-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="88e77-105">Vous trouverez de nombreux exemples d’expériences et d’API dans la [galerie Cortana Intelligence](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="88e77-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="88e77-106">Pour plus d’informations sur la galerie, consultez [Partager et découvrir des solutions dans la galerie Cortana Intelligence](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="88e77-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="88e77-107">La suite de distribution normale correspond à un ensemble d’exemples de services web ([Générateur](https://datamarket.azure.com/dataset/aml_labs/ndg7), [Calculatrice de quantile](https://datamarket.azure.com/dataset/aml_labs/ndq5), [Calculatrice de probabilité](https://datamarket.azure.com/dataset/aml_labs/ndp5)) qui facilite la génération et la gestion des distributions normales.</span><span class="sxs-lookup"><span data-stu-id="88e77-107">The Normal Distribution Suite is a set of sample web services ([Generator](https://datamarket.azure.com/dataset/aml_labs/ndg7), [Quantile Calculator](https://datamarket.azure.com/dataset/aml_labs/ndq5), [Probability Calculator](https://datamarket.azure.com/dataset/aml_labs/ndp5)) that help in generating and handling normal distributions.</span></span> <span data-ttu-id="88e77-108">Les services permettent de générer une séquence de distribution normale de n’importe quelle longueur, de calculer les quantiles à partir d’une probabilité donnée et de calculer la probabilité à partir d’un quantile donné.</span><span class="sxs-lookup"><span data-stu-id="88e77-108">The services allow generating a normal distribution sequence of any length, calculating quantiles from a given probability, and calculating probability from a given quantile.</span></span> <span data-ttu-id="88e77-109">Chacun des services émet des résultats différents selon le service sélectionné (voir la description ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="88e77-109">Each of the services emits different outputs based on the selected service (see description below).</span></span> <span data-ttu-id="88e77-110">La suite de distribution normale repose sur les fonctions R qnorm, rnorm et pnorm qui sont incluses dans le package de statistiques R.</span><span class="sxs-lookup"><span data-stu-id="88e77-110">The Normal Distribution Suite is based on the R functions qnorm, rnorm, and pnorm, which are included in R stats package.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="88e77-111">Les utilisateurs peuvent potentiellement accéder à ce service web par le biais d’une application mobile, d’un site web ou même d’un ordinateur local, par exemple.</span><span class="sxs-lookup"><span data-stu-id="88e77-111">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="88e77-112">Mais l’objectif du service web est également de servir d’exemple d’utilisation d’Azure Machine Learning pour créer des services web avec le code R.</span><span class="sxs-lookup"><span data-stu-id="88e77-112">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="88e77-113">Avec seulement quelques lignes de code R et quelques clics dans Azure Machine Learning Studio, vous pouvez créer une expérience avec le code R et la publier en tant que service web.</span><span class="sxs-lookup"><span data-stu-id="88e77-113">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="88e77-114">Le service web peut ensuite être publié sur Azure Marketplace afin que les utilisateurs et les appareils du monde entier l’utilisent sans que l’auteur du service web n’ait à configurer l’infrastructure.</span><span class="sxs-lookup"><span data-stu-id="88e77-114">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="88e77-115">Utilisation du service web</span><span class="sxs-lookup"><span data-stu-id="88e77-115">Consumption of web service</span></span>
<span data-ttu-id="88e77-116">La suite de distribution normale inclut les 3 services suivants.</span><span class="sxs-lookup"><span data-stu-id="88e77-116">The Normal Distribution Suite includes the following 3 services.</span></span>

### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="88e77-117">Calculatrice de quantile pour la distribution normale</span><span class="sxs-lookup"><span data-stu-id="88e77-117">Normal Distribution Quantile Calculator</span></span>
<span data-ttu-id="88e77-118">Ce service accepte 4 arguments d'une distribution normale et calcule le quantile associé.</span><span class="sxs-lookup"><span data-stu-id="88e77-118">This service accepts 4 arguments of a normal distribution and calculates the associated quantile.</span></span>

<span data-ttu-id="88e77-119">Les arguments d'entrée sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="88e77-119">The input arguments are:</span></span>

* <span data-ttu-id="88e77-120">p : probabilité unique d’un événement avec distribution normale</span><span class="sxs-lookup"><span data-stu-id="88e77-120">p - A single probability of an event with normal distribution.</span></span> 
* <span data-ttu-id="88e77-121">Mean : moyenne de la distribution normale</span><span class="sxs-lookup"><span data-stu-id="88e77-121">Mean - The normal distribution mean.</span></span>
* <span data-ttu-id="88e77-122">SD : écart type de la distribution normale</span><span class="sxs-lookup"><span data-stu-id="88e77-122">SD - The normal distribution standard deviation.</span></span> 
* <span data-ttu-id="88e77-123">Side : L pour la partie inférieure de la distribution et U pour la partie supérieure de la distribution</span><span class="sxs-lookup"><span data-stu-id="88e77-123">Side - L for the lower side of the distribution and U for the upper side of the distribution.</span></span>

<span data-ttu-id="88e77-124">La sortie du service correspond au quantile calculé qui est associé à la probabilité donnée.</span><span class="sxs-lookup"><span data-stu-id="88e77-124">The output of the service is the calculated quantile that is associated with the given probability.</span></span>

### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="88e77-125">Calculatrice de probabilité de distribution normale</span><span class="sxs-lookup"><span data-stu-id="88e77-125">Normal Distribution Probability Calculator</span></span>
<span data-ttu-id="88e77-126">Ce service accepte 4 arguments d'une distribution normale et calcule la probabilité associée.</span><span class="sxs-lookup"><span data-stu-id="88e77-126">This service accepts 4 arguments of a normal distribution and calculates the associated probability.</span></span>

<span data-ttu-id="88e77-127">Les arguments d'entrée sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="88e77-127">The input arguments are:</span></span>

* <span data-ttu-id="88e77-128">q : quantile unique d’un événement avec une distribution normale</span><span class="sxs-lookup"><span data-stu-id="88e77-128">q - A single quantile of an event with normal distribution.</span></span> 
* <span data-ttu-id="88e77-129">Mean : moyenne de la distribution normale</span><span class="sxs-lookup"><span data-stu-id="88e77-129">Mean - The normal distribution mean.</span></span>
* <span data-ttu-id="88e77-130">SD : écart type de la distribution normale</span><span class="sxs-lookup"><span data-stu-id="88e77-130">SD - The normal distribution standard deviation.</span></span> 
* <span data-ttu-id="88e77-131">Side : L pour la partie inférieure de la distribution et U pour la partie supérieure de la distribution</span><span class="sxs-lookup"><span data-stu-id="88e77-131">Side - L for the lower side of the distribution and U for the upper side of the distribution.</span></span>

<span data-ttu-id="88e77-132">La sortie du service correspond à la probabilité calculée qui est associée au quantile donné.</span><span class="sxs-lookup"><span data-stu-id="88e77-132">The output of the service is the calculated probability that is associated with the given quantile.</span></span>

### <a name="normal-distribution-generator"></a><span data-ttu-id="88e77-133">Générateur de distribution normale</span><span class="sxs-lookup"><span data-stu-id="88e77-133">Normal Distribution Generator</span></span>
<span data-ttu-id="88e77-134">Ce service accepte 3 arguments d'une distribution normale et génère une séquence aléatoire de nombres qui sont distribués normalement.</span><span class="sxs-lookup"><span data-stu-id="88e77-134">This service accepts 3 arguments of a normal distribution and generates a random sequence of numbers that are normally distributed.</span></span> <span data-ttu-id="88e77-135">Les arguments suivants doivent lui être fournis au sein de la demande :</span><span class="sxs-lookup"><span data-stu-id="88e77-135">The following arguments should be provided to it within the request:</span></span>

* <span data-ttu-id="88e77-136">n : nombre d’observations</span><span class="sxs-lookup"><span data-stu-id="88e77-136">n - The number of observations.</span></span> 
* <span data-ttu-id="88e77-137">Mean : moyenne de la distribution normale</span><span class="sxs-lookup"><span data-stu-id="88e77-137">mean - The normal distribution mean.</span></span>
* <span data-ttu-id="88e77-138">SD : écart type de la distribution normale</span><span class="sxs-lookup"><span data-stu-id="88e77-138">sd - The normal distribution standard deviation.</span></span> 

<span data-ttu-id="88e77-139">La sortie du service est une séquence de longueur n avec une distribution normale basée sur les arguments mean et sd.</span><span class="sxs-lookup"><span data-stu-id="88e77-139">The output of the service is a sequence of length n with a normal distribution based on the mean and sd arguments.</span></span>

> <span data-ttu-id="88e77-140">Étant hébergé sur Azure Marketplace, ce service est un service OData. Il peut être appelé à l’aide des méthodes POST ou GET.</span><span class="sxs-lookup"><span data-stu-id="88e77-140">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="88e77-141">Il existe plusieurs façons d’utiliser le service de manière automatique (exemple d’applications : [Générateur](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionGenerator.aspx), [Calculatrice de probabilité](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionProbabilityCalculator.aspx), [Calculatrice de quantile](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionQuantileCalculator.aspx)).</span><span class="sxs-lookup"><span data-stu-id="88e77-141">There are multiple ways of consuming the service in an automated fashion (example apps are here: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionGenerator.aspx), [Probability Calculator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionProbabilityCalculator.aspx), [Quantile Calculator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionQuantileCalculator.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="88e77-142">Début du code C# pour l'utilisation du service web :</span><span class="sxs-lookup"><span data-stu-id="88e77-142">Starting C# code for web service consumption:</span></span>
### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="88e77-143">Calculatrice de quantile pour la distribution normale</span><span class="sxs-lookup"><span data-stu-id="88e77-143">Normal Distribution Quantile Calculator</span></span>
    public class Input
    {
            public string p;
            public string mean;
            public string sd;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { p = TextBox1.Text, mean = TextBox2.Text, sd = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="88e77-144">Calculatrice de probabilité de distribution normale</span><span class="sxs-lookup"><span data-stu-id="88e77-144">Normal Distribution Probability Calculator</span></span>
    public class Input
    {
            public string q;
            public string mean;
            public string sd;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { q = TextBox1.Text, mean = TextBox2.Text, sd = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }

### <a name="normal-distribution-generator"></a><span data-ttu-id="88e77-145">Générateur de distribution normale</span><span class="sxs-lookup"><span data-stu-id="88e77-145">Normal Distribution Generator</span></span>
    public class Input
    {
            public string n;
            public string mean;
            public string sd;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { n = TextBox1.Text, mean = TextBox2.Text, sd = TextBox3.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


## <a name="creation-of-web-service"></a><span data-ttu-id="88e77-146">Création du service web</span><span class="sxs-lookup"><span data-stu-id="88e77-146">Creation of web service</span></span>
> <span data-ttu-id="88e77-147">Ce service web a été créé à l’aide d’Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="88e77-147">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="88e77-148">Pour un essai gratuit, ainsi que des vidéos de présentation relatives à la création d’expériences et à la [publication de services web](machine-learning-publish-a-machine-learning-web-service.md), consultez [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="88e77-148">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> 
> 
> 

<span data-ttu-id="88e77-149">Voici une capture d'écran de l'expérience qui a créé le service web et l'exemple de code pour chacun des modules dans l'expérience.</span><span class="sxs-lookup"><span data-stu-id="88e77-149">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>

### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="88e77-150">Calculatrice de quantile pour la distribution normale</span><span class="sxs-lookup"><span data-stu-id="88e77-150">Normal Distribution Quantile Calculator</span></span>
<span data-ttu-id="88e77-151">Flux de l’expérience :</span><span class="sxs-lookup"><span data-stu-id="88e77-151">Experiment flow:</span></span>

![Flux de l’expérience][2]

    #Data schema with example data (replaced with data from web service)
    data.set=data.frame(p=0.1,mean=0,sd=1,side='L');
    maml.mapOutputPort("data.set"); #send data to output port

    # Map 1-based optional input ports to variables
    dataset1 <- maml.mapInputPort(1) # class: data.frame

    param = dataset1
    if (param$p < 0 ) {
    print('Bad input: p must be between 0 and 1')
    param$p = 0
    } else if (param$p > 1) {
    print('Bad input: p must be between 0 and 1')
    param$p = 1
    }
    q = qnorm(param$p,mean=param$mean,sd=param$sd)

    if (param$side == 'U'){
    q = 2* param$mean - q
    } else if (param$side =='L') {
    q = q
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(q)

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");

### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="88e77-153">Calculatrice de probabilité de distribution normale</span><span class="sxs-lookup"><span data-stu-id="88e77-153">Normal Distribution Probability Calculator</span></span>
<span data-ttu-id="88e77-154">Flux de l’expérience :</span><span class="sxs-lookup"><span data-stu-id="88e77-154">Experiment flow:</span></span>

![Flux de l’expérience][3]

     #Data schema with example data (replaced with data from web service)
    data.set=data.frame(q=-1,mean=0,sd=1,side='L');
    maml.mapOutputPort("data.set"); #send data to output port

    # Map 1-based optional input ports to variables
    dataset1 <- maml.mapInputPort(1) # class: data.frame

    param = dataset1
    prob = pnorm(param$q,mean=param$mean,sd=param$sd)

    if (param$side == 'U'){
    prob = 1 - prob
    } else if (param$side =='B') {
    prob = ifelse(prob<=0.5,prob * 2, 1)
    } else if (param$side =='L') {
    prob = prob
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(prob)

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");

### <a name="normal-distribution-generator"></a><span data-ttu-id="88e77-156">Générateur de distribution normale</span><span class="sxs-lookup"><span data-stu-id="88e77-156">Normal Distribution Generator</span></span>
<span data-ttu-id="88e77-157">Flux de l’expérience :</span><span class="sxs-lookup"><span data-stu-id="88e77-157">Experiment flow:</span></span>

![Flux de l’expérience][4]

    #Data schema with example data (replaced with data from web service)
    data.set=data.frame(n=50,mean=0,sd=1);
    maml.mapOutputPort("data.set"); #send data to output port

    # Map 1-based optional input ports to variables
    dataset1 <- maml.mapInputPort(1) # class: data.frame

    param = dataset1
    dist = rnorm(param$n,mean=param$mean,sd=param$sd)

    output = as.data.frame(t(dist))

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");

## <a name="limitations"></a><span data-ttu-id="88e77-159">Limitations</span><span class="sxs-lookup"><span data-stu-id="88e77-159">Limitations</span></span>
<span data-ttu-id="88e77-160">Il s’agit d’exemples très simples en rapport avec la distribution normale.</span><span class="sxs-lookup"><span data-stu-id="88e77-160">These are very simple examples surrounding the normal distribution.</span></span> <span data-ttu-id="88e77-161">Comme illustré dans l'exemple de code ci-dessus, l'interception des erreurs est mise œuvre de façon limitée.</span><span class="sxs-lookup"><span data-stu-id="88e77-161">As can be seen from the example code above, little error catching is implemented.</span></span>

## <a name="faq"></a><span data-ttu-id="88e77-162">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="88e77-162">FAQ</span></span>
<span data-ttu-id="88e77-163">Pour les questions fréquemment posées relatives à l’utilisation du service web ou à la publication sur Azure Marketplace, consultez [ce lien](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="88e77-163">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-normal-distribution/normal-img1.png
[2]: ./media/machine-learning-r-csharp-normal-distribution/normal-img2.png
[3]: ./media/machine-learning-r-csharp-normal-distribution/normal-img3.png
[4]: ./media/machine-learning-r-csharp-normal-distribution/normal-img4.png

