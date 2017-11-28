---
title: AAA(deprecated) Distribution normale Web Service Suite - Azure | Documents Microsoft
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
redirect_document_id: True
ms.openlocfilehash: 8bdb5afd9fee88587f548d7c5299480f64289bbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-normal-distribution-suite"></a><span data-ttu-id="4af0b-103">(obsolète) Suite de distribution normale</span><span class="sxs-lookup"><span data-stu-id="4af0b-103">(deprecated) Normal Distribution Suite</span></span>

> [!NOTE]
> <span data-ttu-id="4af0b-104">Hello Microsoft DataMarket a été supprimée et que cette API est déconseillée.</span><span class="sxs-lookup"><span data-stu-id="4af0b-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="4af0b-105">Vous trouverez plusieurs API et les expériences d’exemple utile Bonjour [Cortana Intelligence galerie](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="4af0b-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="4af0b-106">Pour plus d’informations sur la galerie de hello, consultez [partager et découvrir des ressources Bonjour Cortana Intelligence galerie](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="4af0b-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="4af0b-107">Hello Distribution normale Suite est un ensemble d’exemples de services web ([Générateur](https://datamarket.azure.com/dataset/aml_labs/ndg7), [calculatrice de Quantile](https://datamarket.azure.com/dataset/aml_labs/ndq5), [probabilité calculatrice](https://datamarket.azure.com/dataset/aml_labs/ndp5)) qui aident dans la génération et la gestion distributions normales.</span><span class="sxs-lookup"><span data-stu-id="4af0b-107">hello Normal Distribution Suite is a set of sample web services ([Generator](https://datamarket.azure.com/dataset/aml_labs/ndg7), [Quantile Calculator](https://datamarket.azure.com/dataset/aml_labs/ndq5), [Probability Calculator](https://datamarket.azure.com/dataset/aml_labs/ndp5)) that help in generating and handling normal distributions.</span></span> <span data-ttu-id="4af0b-108">les services de Hello permettent la génération d’une séquence de distribution normale d’une longueur quelconque, du calcul de l’étendue à partir d’une probabilité donnée et le calcul de probabilité à partir d’un quantile donné.</span><span class="sxs-lookup"><span data-stu-id="4af0b-108">hello services allow generating a normal distribution sequence of any length, calculating quantiles from a given probability, and calculating probability from a given quantile.</span></span> <span data-ttu-id="4af0b-109">Chacun des services de hello émet différentes sorties en fonction de service de hello sélectionné (voir la description ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="4af0b-109">Each of hello services emits different outputs based on hello selected service (see description below).</span></span> <span data-ttu-id="4af0b-110">Hello Suite de la Distribution normale est basée sur hello R fonctions qnorm, rnorm et pnorm, qui sont inclus dans le package de statistiques de R.</span><span class="sxs-lookup"><span data-stu-id="4af0b-110">hello Normal Distribution Suite is based on hello R functions qnorm, rnorm, and pnorm, which are included in R stats package.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="4af0b-111">Les utilisateurs peuvent potentiellement accéder à ce service web par le biais d’une application mobile, d’un site web ou même d’un ordinateur local, par exemple.</span><span class="sxs-lookup"><span data-stu-id="4af0b-111">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="4af0b-112">Mais hello objectif du service web de hello est également tooserve comme exemple illustrant comment Azure Machine Learning peuvent être des services web toocreate utilisé sur le code R.</span><span class="sxs-lookup"><span data-stu-id="4af0b-112">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="4af0b-113">Avec seulement quelques lignes de code R et quelques clics dans Azure Machine Learning Studio, vous pouvez créer une expérience avec le code R et la publier en tant que service web.</span><span class="sxs-lookup"><span data-stu-id="4af0b-113">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="4af0b-114">service web de Hello peut ensuite être publié toohello Azure Marketplace et consommé par les utilisateurs et périphériques sur Bonjour sans configuration d’infrastructure par l’auteur de hello du service web de hello.</span><span class="sxs-lookup"><span data-stu-id="4af0b-114">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="4af0b-115">Utilisation du service web</span><span class="sxs-lookup"><span data-stu-id="4af0b-115">Consumption of web service</span></span>
<span data-ttu-id="4af0b-116">Hello Distribution normale Suite inclut hello suivant 3 services.</span><span class="sxs-lookup"><span data-stu-id="4af0b-116">hello Normal Distribution Suite includes hello following 3 services.</span></span>

### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="4af0b-117">Calculatrice de quantile pour la distribution normale</span><span class="sxs-lookup"><span data-stu-id="4af0b-117">Normal Distribution Quantile Calculator</span></span>
<span data-ttu-id="4af0b-118">Ce service accepte des arguments d’une distribution normale 4 et calcule hello associé quantile.</span><span class="sxs-lookup"><span data-stu-id="4af0b-118">This service accepts 4 arguments of a normal distribution and calculates hello associated quantile.</span></span>

<span data-ttu-id="4af0b-119">les arguments d’entrée Hello sont :</span><span class="sxs-lookup"><span data-stu-id="4af0b-119">hello input arguments are:</span></span>

* <span data-ttu-id="4af0b-120">p : probabilité unique d’un événement avec distribution normale</span><span class="sxs-lookup"><span data-stu-id="4af0b-120">p - A single probability of an event with normal distribution.</span></span> 
* <span data-ttu-id="4af0b-121">Moyenne - moyenne d’une distribution normale hello.</span><span class="sxs-lookup"><span data-stu-id="4af0b-121">Mean - hello normal distribution mean.</span></span>
* <span data-ttu-id="4af0b-122">SD - distribution normale hello écart type.</span><span class="sxs-lookup"><span data-stu-id="4af0b-122">SD - hello normal distribution standard deviation.</span></span> 
* <span data-ttu-id="4af0b-123">Côté - L pour la partie inférieure de hello de distribution de hello et U pour la partie supérieure de hello de distribution de hello.</span><span class="sxs-lookup"><span data-stu-id="4af0b-123">Side - L for hello lower side of hello distribution and U for hello upper side of hello distribution.</span></span>

<span data-ttu-id="4af0b-124">sortie de Hello du service de hello est quantile hello calculée qui est associée à hello fonction de probabilité.</span><span class="sxs-lookup"><span data-stu-id="4af0b-124">hello output of hello service is hello calculated quantile that is associated with hello given probability.</span></span>

### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="4af0b-125">Calculatrice de probabilité de distribution normale</span><span class="sxs-lookup"><span data-stu-id="4af0b-125">Normal Distribution Probability Calculator</span></span>
<span data-ttu-id="4af0b-126">Ce service accepte des arguments d’une distribution normale 4 et calcule la probabilité de hello associé.</span><span class="sxs-lookup"><span data-stu-id="4af0b-126">This service accepts 4 arguments of a normal distribution and calculates hello associated probability.</span></span>

<span data-ttu-id="4af0b-127">les arguments d’entrée Hello sont :</span><span class="sxs-lookup"><span data-stu-id="4af0b-127">hello input arguments are:</span></span>

* <span data-ttu-id="4af0b-128">q : quantile unique d’un événement avec une distribution normale</span><span class="sxs-lookup"><span data-stu-id="4af0b-128">q - A single quantile of an event with normal distribution.</span></span> 
* <span data-ttu-id="4af0b-129">Moyenne - moyenne d’une distribution normale hello.</span><span class="sxs-lookup"><span data-stu-id="4af0b-129">Mean - hello normal distribution mean.</span></span>
* <span data-ttu-id="4af0b-130">SD - distribution normale hello écart type.</span><span class="sxs-lookup"><span data-stu-id="4af0b-130">SD - hello normal distribution standard deviation.</span></span> 
* <span data-ttu-id="4af0b-131">Côté - L pour la partie inférieure de hello de distribution de hello et U pour la partie supérieure de hello de distribution de hello.</span><span class="sxs-lookup"><span data-stu-id="4af0b-131">Side - L for hello lower side of hello distribution and U for hello upper side of hello distribution.</span></span>

<span data-ttu-id="4af0b-132">sortie Hello du service de hello représente la probabilité hello calculé hello donné quantile est associée.</span><span class="sxs-lookup"><span data-stu-id="4af0b-132">hello output of hello service is hello calculated probability that is associated with hello given quantile.</span></span>

### <a name="normal-distribution-generator"></a><span data-ttu-id="4af0b-133">Générateur de distribution normale</span><span class="sxs-lookup"><span data-stu-id="4af0b-133">Normal Distribution Generator</span></span>
<span data-ttu-id="4af0b-134">Ce service accepte 3 arguments d'une distribution normale et génère une séquence aléatoire de nombres qui sont distribués normalement.</span><span class="sxs-lookup"><span data-stu-id="4af0b-134">This service accepts 3 arguments of a normal distribution and generates a random sequence of numbers that are normally distributed.</span></span> <span data-ttu-id="4af0b-135">Hello arguments suivants doivent être fournis tooit au sein de la demande de hello :</span><span class="sxs-lookup"><span data-stu-id="4af0b-135">hello following arguments should be provided tooit within hello request:</span></span>

* <span data-ttu-id="4af0b-136">n - nombre de hello d’observations.</span><span class="sxs-lookup"><span data-stu-id="4af0b-136">n - hello number of observations.</span></span> 
* <span data-ttu-id="4af0b-137">Moyenne - moyenne d’une distribution normale hello.</span><span class="sxs-lookup"><span data-stu-id="4af0b-137">mean - hello normal distribution mean.</span></span>
* <span data-ttu-id="4af0b-138">SD - distribution normale hello écart type.</span><span class="sxs-lookup"><span data-stu-id="4af0b-138">sd - hello normal distribution standard deviation.</span></span> 

<span data-ttu-id="4af0b-139">sortie Hello du service de hello est une séquence de longueur n avec une distribution normale basée sur les arguments moyenne et sd hello.</span><span class="sxs-lookup"><span data-stu-id="4af0b-139">hello output of hello service is a sequence of length n with a normal distribution based on hello mean and sd arguments.</span></span>

> <span data-ttu-id="4af0b-140">Ce service, comme hébergé sur hello Azure Marketplace, est un service OData ; Il peuvent être appelées par le biais des méthodes POST ou GET.</span><span class="sxs-lookup"><span data-stu-id="4af0b-140">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="4af0b-141">Il existe plusieurs manières de consommation de service hello de manière automatique (exemple applications sont ici : [Générateur](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionGenerator.aspx), [probabilité calculatrice](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionProbabilityCalculator.aspx), [Quantile calculatrice](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionQuantileCalculator.aspx)).</span><span class="sxs-lookup"><span data-stu-id="4af0b-141">There are multiple ways of consuming hello service in an automated fashion (example apps are here: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionGenerator.aspx), [Probability Calculator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionProbabilityCalculator.aspx), [Quantile Calculator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionQuantileCalculator.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="4af0b-142">Début du code C# pour l'utilisation du service web :</span><span class="sxs-lookup"><span data-stu-id="4af0b-142">Starting C# code for web service consumption:</span></span>
### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="4af0b-143">Calculatrice de quantile pour la distribution normale</span><span class="sxs-lookup"><span data-stu-id="4af0b-143">Normal Distribution Quantile Calculator</span></span>
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


### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="4af0b-144">Calculatrice de probabilité de distribution normale</span><span class="sxs-lookup"><span data-stu-id="4af0b-144">Normal Distribution Probability Calculator</span></span>
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

### <a name="normal-distribution-generator"></a><span data-ttu-id="4af0b-145">Générateur de distribution normale</span><span class="sxs-lookup"><span data-stu-id="4af0b-145">Normal Distribution Generator</span></span>
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


## <a name="creation-of-web-service"></a><span data-ttu-id="4af0b-146">Création du service web</span><span class="sxs-lookup"><span data-stu-id="4af0b-146">Creation of web service</span></span>
> <span data-ttu-id="4af0b-147">Ce service web a été créé à l’aide d’Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="4af0b-147">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="4af0b-148">Pour un essai gratuit, ainsi que des vidéos de présentation relatives à la création d’expériences et à la [publication de services web](machine-learning-publish-a-machine-learning-web-service.md), consultez [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="4af0b-148">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> 
> 
> 

<span data-ttu-id="4af0b-149">Voici une capture d’écran d’expérience hello qui a créé un code de service et un exemple hello web pour chacun des modules hello au sein de l’expérience de hello.</span><span class="sxs-lookup"><span data-stu-id="4af0b-149">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>

### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="4af0b-150">Calculatrice de quantile pour la distribution normale</span><span class="sxs-lookup"><span data-stu-id="4af0b-150">Normal Distribution Quantile Calculator</span></span>
<span data-ttu-id="4af0b-151">Flux de l’expérience :</span><span class="sxs-lookup"><span data-stu-id="4af0b-151">Experiment flow:</span></span>

![Flux de l’expérience][2]

    #Data schema with example data (replaced with data from web service)
    data.set=data.frame(p=0.1,mean=0,sd=1,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port

    # Map 1-based optional input ports toovariables
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

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="4af0b-153">Calculatrice de probabilité de distribution normale</span><span class="sxs-lookup"><span data-stu-id="4af0b-153">Normal Distribution Probability Calculator</span></span>
<span data-ttu-id="4af0b-154">Flux de l’expérience :</span><span class="sxs-lookup"><span data-stu-id="4af0b-154">Experiment flow:</span></span>

![Flux de l’expérience][3]

     #Data schema with example data (replaced with data from web service)
    data.set=data.frame(q=-1,mean=0,sd=1,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port

    # Map 1-based optional input ports toovariables
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

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

### <a name="normal-distribution-generator"></a><span data-ttu-id="4af0b-156">Générateur de distribution normale</span><span class="sxs-lookup"><span data-stu-id="4af0b-156">Normal Distribution Generator</span></span>
<span data-ttu-id="4af0b-157">Flux de l’expérience :</span><span class="sxs-lookup"><span data-stu-id="4af0b-157">Experiment flow:</span></span>

![Flux de l’expérience][4]

    #Data schema with example data (replaced with data from web service)
    data.set=data.frame(n=50,mean=0,sd=1);
    maml.mapOutputPort("data.set"); #send data toooutput port

    # Map 1-based optional input ports toovariables
    dataset1 <- maml.mapInputPort(1) # class: data.frame

    param = dataset1
    dist = rnorm(param$n,mean=param$mean,sd=param$sd)

    output = as.data.frame(t(dist))

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

## <a name="limitations"></a><span data-ttu-id="4af0b-159">Limites</span><span class="sxs-lookup"><span data-stu-id="4af0b-159">Limitations</span></span>
<span data-ttu-id="4af0b-160">Voici des exemples très simples qui entoure hello une distribution normale.</span><span class="sxs-lookup"><span data-stu-id="4af0b-160">These are very simple examples surrounding hello normal distribution.</span></span> <span data-ttu-id="4af0b-161">Comme le montre hello exemple de code ci-dessus, peu interception des erreurs est implémentée.</span><span class="sxs-lookup"><span data-stu-id="4af0b-161">As can be seen from hello example code above, little error catching is implemented.</span></span>

## <a name="faq"></a><span data-ttu-id="4af0b-162">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="4af0b-162">FAQ</span></span>
<span data-ttu-id="4af0b-163">Pour les questions fréquemment posées sur la consommation de service web de hello ou publication toohello Azure Marketplace, consultez [ici](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="4af0b-163">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-normal-distribution/normal-img1.png
[2]: ./media/machine-learning-r-csharp-normal-distribution/normal-img2.png
[3]: ./media/machine-learning-r-csharp-normal-distribution/normal-img3.png
[4]: ./media/machine-learning-r-csharp-normal-distribution/normal-img4.png

