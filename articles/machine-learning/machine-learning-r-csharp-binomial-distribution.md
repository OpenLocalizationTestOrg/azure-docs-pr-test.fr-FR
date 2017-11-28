---
title: AAA(deprecated) Suite de la Distribution binomiale - Azure | Documents Microsoft
description: "(obsolète) Suite de distribution binomiale"
services: machine-learning
documentationcenter: 
author: ireiter
manager: jhubbard
editor: cgronlun
ms.assetid: 6d102d57-8f20-4ab3-be31-02fcfe4d15ed
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
ms.openlocfilehash: 6f94436cd19abeb518d179f340c8d4f43fcf4520
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-binomial-distribution-suite"></a><span data-ttu-id="bd7e1-103">(obsolète) Suite de distribution binomiale</span><span class="sxs-lookup"><span data-stu-id="bd7e1-103">(deprecated) Binomial Distribution Suite</span></span>

> [!NOTE]
> <span data-ttu-id="bd7e1-104">Hello Microsoft DataMarket a été supprimée et que cette API est déconseillée.</span><span class="sxs-lookup"><span data-stu-id="bd7e1-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="bd7e1-105">Vous trouverez plusieurs API et les expériences d’exemple utile Bonjour [Cortana Intelligence galerie](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="bd7e1-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="bd7e1-106">Pour plus d’informations sur la galerie de hello, consultez [partager et découvrir des ressources Bonjour Cortana Intelligence galerie](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="bd7e1-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="bd7e1-107">Hello Suite de la Distribution binomiale est un ensemble d’exemples de services web ([binomiale Générateur](https://datamarket.azure.com/dataset/aml_labs/bdg5), [probabilité calculatrice](https://datamarket.azure.com/dataset/aml_labs/bdp4), [Quantile calculatrice](https://datamarket.azure.com/dataset/aml_labs/bdq5)) qui aident à générer et traiter les distributions de binomiale.</span><span class="sxs-lookup"><span data-stu-id="bd7e1-107">hello Binomial Distribution Suite is a set of sample web services ([Binomial Generator](https://datamarket.azure.com/dataset/aml_labs/bdg5), [Probability Calculator](https://datamarket.azure.com/dataset/aml_labs/bdp4), [Quantile Calculator](https://datamarket.azure.com/dataset/aml_labs/bdq5)) that help in generating and dealing with binomial distributions.</span></span> <span data-ttu-id="bd7e1-108">Hello services autorisent génération d’une séquence de distribution binomiale de n’importe quelle longueur du calcul d’étendue hors fonction de probabilité et la probabilité de calcul à partir d’un quantile donné.</span><span class="sxs-lookup"><span data-stu-id="bd7e1-108">hello services allow generating a binomial distribution sequence of any length, calculating quantiles out of given probability and calculating probability from a given quantile.</span></span> <span data-ttu-id="bd7e1-109">Chacun des services de hello émet différentes sorties en fonction de service de hello sélectionné (voir la description ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="bd7e1-109">Each of hello services emits different outputs based on hello selected service (see description below).</span></span> <span data-ttu-id="bd7e1-110">Hello Suite de la Distribution binomiale est basée sur hello R fonctions qbinom, rbinom et pbinom, qui sont inclus dans le package de statistiques hello R.</span><span class="sxs-lookup"><span data-stu-id="bd7e1-110">hello Binomial Distribution Suite is based on hello R functions qbinom, rbinom, and pbinom, which are included in hello R stats package.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="bd7e1-111">Ces services web pouvant être consommées par les utilisateurs – potentiellement directement sur le marketplace hello, via une application mobile, via un site Web, ou même sur un ordinateur local, par exemple.</span><span class="sxs-lookup"><span data-stu-id="bd7e1-111">These web services could be consumed by users – potentially directly on hello marketplace, through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="bd7e1-112">Mais hello objectif du service web de hello est également tooserve comme exemple illustrant comment Azure Machine Learning peuvent être des services web toocreate utilisé sur le code R.</span><span class="sxs-lookup"><span data-stu-id="bd7e1-112">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="bd7e1-113">Avec seulement quelques lignes de code R et quelques clics dans Azure Machine Learning Studio, vous pouvez créer une expérience avec le code R et la publier en tant que service web.</span><span class="sxs-lookup"><span data-stu-id="bd7e1-113">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="bd7e1-114">service web de Hello peut ensuite être publié toohello Azure Marketplace et consommé par les utilisateurs et périphériques sur Bonjour – infrastructure par l’auteur de hello du service web de hello n’exige aucune configuration.</span><span class="sxs-lookup"><span data-stu-id="bd7e1-114">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world – no infrastructure setup by hello author of hello web service is required.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="bd7e1-115">Utilisation du service web</span><span class="sxs-lookup"><span data-stu-id="bd7e1-115">Consumption of web service</span></span>
<span data-ttu-id="bd7e1-116">Hello Distribution binomiale Suite inclut hello suivant 3 services.</span><span class="sxs-lookup"><span data-stu-id="bd7e1-116">hello Binomial Distribution Suite includes hello following 3 services.</span></span>

### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="bd7e1-117">Calculatrice de quantile pour la distribution binomiale</span><span class="sxs-lookup"><span data-stu-id="bd7e1-117">Binomial Distribution Quantile Calculator</span></span>
<span data-ttu-id="bd7e1-118">Ce service accepte des arguments d’une distribution normale 4 et calcule hello associé quantile.</span><span class="sxs-lookup"><span data-stu-id="bd7e1-118">This service accepts 4 arguments of a normal distribution and calculates hello associated quantile.</span></span>
<span data-ttu-id="bd7e1-119">les arguments d’entrée Hello sont :</span><span class="sxs-lookup"><span data-stu-id="bd7e1-119">hello input arguments are:</span></span>

* <span data-ttu-id="bd7e1-120">p : probabilité unique agrégée de plusieurs essais</span><span class="sxs-lookup"><span data-stu-id="bd7e1-120">p - A single aggregated probability of multiple trials.</span></span>  
* <span data-ttu-id="bd7e1-121">taille - nombre hello d’essais.</span><span class="sxs-lookup"><span data-stu-id="bd7e1-121">size - hello number of trials.</span></span>
* <span data-ttu-id="bd7e1-122">probabilité - probabilité hello de réussite d’une version d’évaluation.</span><span class="sxs-lookup"><span data-stu-id="bd7e1-122">prob - hello probability of success in a trial.</span></span>
* <span data-ttu-id="bd7e1-123">Côté - L pour la partie inférieure de hello de distribution hello, U pour la partie supérieure de hello de distribution de hello.</span><span class="sxs-lookup"><span data-stu-id="bd7e1-123">Side - L for hello lower side of hello distribution, U for hello upper side of hello distribution.</span></span> 

<span data-ttu-id="bd7e1-124">sortie de Hello du service de hello est quantile hello calculée qui est associée à hello fonction de probabilité.</span><span class="sxs-lookup"><span data-stu-id="bd7e1-124">hello output of hello service is hello calculated quantile that is associated with hello given probability.</span></span>

### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="bd7e1-125">Calculatrice de probabilité de distribution binomiale</span><span class="sxs-lookup"><span data-stu-id="bd7e1-125">Binomial Distribution Probability Calculator</span></span>
<span data-ttu-id="bd7e1-126">Ce service accepte des arguments d’une distribution binomiale 4 et calcule la probabilité de hello associé.</span><span class="sxs-lookup"><span data-stu-id="bd7e1-126">This service accepts 4 arguments of a binomial distribution and calculates hello associated probability.</span></span>
<span data-ttu-id="bd7e1-127">les arguments d’entrée Hello sont :</span><span class="sxs-lookup"><span data-stu-id="bd7e1-127">hello input arguments are:</span></span>

* <span data-ttu-id="bd7e1-128">q : quantile unique d’un événement avec une distribution binomiale</span><span class="sxs-lookup"><span data-stu-id="bd7e1-128">q - A single quantile of an event with binomial distribution.</span></span> 
* <span data-ttu-id="bd7e1-129">taille - nombre hello d’essais.</span><span class="sxs-lookup"><span data-stu-id="bd7e1-129">size - hello number of trials.</span></span>
* <span data-ttu-id="bd7e1-130">probabilité - probabilité hello de réussite d’une version d’évaluation.</span><span class="sxs-lookup"><span data-stu-id="bd7e1-130">prob - hello probability of success in a trial.</span></span>
* <span data-ttu-id="bd7e1-131">côté - L pour la partie inférieure de hello de distribution hello, U pour la partie supérieure de hello de distribution de hello ou E est égale tooa le nombre unique de succès.</span><span class="sxs-lookup"><span data-stu-id="bd7e1-131">side - L for hello lower side of hello distribution, U for hello upper side of hello distribution, or E that is equal tooa single number of successes.</span></span>

<span data-ttu-id="bd7e1-132">sortie Hello du service de hello représente la probabilité hello calculé hello donné quantile est associée.</span><span class="sxs-lookup"><span data-stu-id="bd7e1-132">hello output of hello service is hello calculated probability that is associated with hello given quantile.</span></span>

### <a name="binomial-distribution-generator"></a><span data-ttu-id="bd7e1-133">Générateur de distribution binomiale</span><span class="sxs-lookup"><span data-stu-id="bd7e1-133">Binomial Distribution Generator</span></span>
<span data-ttu-id="bd7e1-134">Ce service accepte 3 arguments d'une distribution binomiale et génère une séquence aléatoire de nombres qui sont distribués selon une loi binomiale.</span><span class="sxs-lookup"><span data-stu-id="bd7e1-134">This service accepts 3 arguments of a binomial distribution and generates a random sequence of numbers that are binomially distributed.</span></span> <span data-ttu-id="bd7e1-135">Hello arguments suivants doivent être fournis tooit au sein de la demande de hello :</span><span class="sxs-lookup"><span data-stu-id="bd7e1-135">hello following arguments should be provided tooit within hello request:</span></span>

* <span data-ttu-id="bd7e1-136">n : nombre d’observations</span><span class="sxs-lookup"><span data-stu-id="bd7e1-136">n - Number of observations.</span></span> 
* <span data-ttu-id="bd7e1-137">size : nombre d’essais</span><span class="sxs-lookup"><span data-stu-id="bd7e1-137">size - Number of trials.</span></span>
* <span data-ttu-id="bd7e1-138">prob : probabilité de réussite</span><span class="sxs-lookup"><span data-stu-id="bd7e1-138">prob - Probability of success.</span></span>

<span data-ttu-id="bd7e1-139">sortie Hello du service de hello est une séquence de longueur n avec une distribution binomiale basée sur les arguments de taille et prob hello.</span><span class="sxs-lookup"><span data-stu-id="bd7e1-139">hello output of hello service is a sequence of length n with a binomial distribution based on hello size and prob arguments.</span></span>

> <span data-ttu-id="bd7e1-140">Ce service, comme hébergé sur hello Azure Marketplace, est un service OData ; Il peuvent être appelées par le biais des méthodes POST ou GET.</span><span class="sxs-lookup"><span data-stu-id="bd7e1-140">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="bd7e1-141">Il existe plusieurs manières de consommation de service hello de manière automatique (exemple applications sont ici : [Générateur](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionGenerator.aspx), [probabilité calculatrice](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionProbabilityCalculator.aspx), [Quantile calculatrice](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionQuantileCalculator)).</span><span class="sxs-lookup"><span data-stu-id="bd7e1-141">There are multiple ways of consuming hello service in an automated fashion (example apps are here: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionGenerator.aspx), [Probability Calculator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionProbabilityCalculator.aspx), [Quantile Calculator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionQuantileCalculator)).</span></span> 

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="bd7e1-142">Début du code C# pour l'utilisation du service web :</span><span class="sxs-lookup"><span data-stu-id="bd7e1-142">Starting C# code for web service consumption:</span></span>
### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="bd7e1-143">Calculatrice de quantile pour la distribution binomiale</span><span class="sxs-lookup"><span data-stu-id="bd7e1-143">Binomial Distribution Quantile Calculator</span></span>
    public class Input
    {
            public string p;
            public string size;
            public string prob;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void main()
    {
            var input = new Input() { p = TextBox1.Text, size = TextBox2.Text, prob = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }

### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="bd7e1-144">Calculatrice de probabilité de distribution binomiale</span><span class="sxs-lookup"><span data-stu-id="bd7e1-144">Binomial Distribution Probability Calculator</span></span>
    public class Input
    {
            public string q;
            public string size;
            public string prob;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { q = TextBox1.Text, size = TextBox2.Text, prob = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = " PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


### <a name="binomial-distribution-generator"></a><span data-ttu-id="bd7e1-145">Générateur de distribution binomiale</span><span class="sxs-lookup"><span data-stu-id="bd7e1-145">Binomial Distribution Generator</span></span>
    public class Input
    {
            public string n;
            public string size;
            public string p;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { n = TextBox1.Text, size = TextBox2.Text, p = TextBox3.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }





## <a name="creation-of-web-service"></a><span data-ttu-id="bd7e1-146">Création du service web</span><span class="sxs-lookup"><span data-stu-id="bd7e1-146">Creation of web service</span></span>
> <span data-ttu-id="bd7e1-147">Ce service web a été créé à l’aide d’Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="bd7e1-147">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="bd7e1-148">Pour un essai gratuit, ainsi que des vidéos de présentation relatives à la création d’expériences et à la [publication de services web](machine-learning-publish-a-machine-learning-web-service.md), consultez [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="bd7e1-148">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="bd7e1-149">Voici une capture d’écran d’expérience hello qui a créé un code de service et un exemple hello web pour chacun des modules hello au sein de l’expérience de hello.</span><span class="sxs-lookup"><span data-stu-id="bd7e1-149">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="bd7e1-150">Calculatrice de quantile pour la distribution binomiale</span><span class="sxs-lookup"><span data-stu-id="bd7e1-150">Binomial Distribution Quantile Calculator</span></span>
![Create workspace][4]

#### <a name="module-1"></a><span data-ttu-id="bd7e1-152">Module 1 :</span><span class="sxs-lookup"><span data-stu-id="bd7e1-152">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(p=0.1,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port
#### <a name="module-2"></a><span data-ttu-id="bd7e1-153">Module 2 :</span><span class="sxs-lookup"><span data-stu-id="bd7e1-153">Module 2:</span></span>
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    if (param$p < 0 ) {
    print('Bad input: p must be between 0 and 1')
    param$p = 0
    } else if (param$p > 1) {
    print('Bad input: p must be between 0 and 1')
    param$p = 1
    }

    if (param$prob < 0 ) {
    print('Bad input: prob must be between 0 and 1')
    param$prob = 0
    } else if (param$prob > 1) {
    print('Bad input: prob must be between 0 and 1')
    param$prob = 1
    }

    quantile = qbinom(param$p,size=param$size,prob=param$prob)
    df = data.frame(x=1:param$size, prob=dbinom(1:param$size, param$size, prob=param$prob))
    quantile

    if (param$side == 'U'){
    quantile = qbinom(param$p,size=param$size,prob=param$prob,lower.tail = F)
    band=subset(df,x>quantile)
    } else if (param$side =='L') {
    quantile = qbinom(param$p,size=param$size,prob=param$prob,lower.tail = T)
    band=subset(df,x<=quantile)
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(quantile)

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");


### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="bd7e1-154">Calculatrice de probabilité de distribution binomiale</span><span class="sxs-lookup"><span data-stu-id="bd7e1-154">Binomial Distribution Probability Calculator</span></span>
![Create workspace][5]

#### <a name="module-1"></a><span data-ttu-id="bd7e1-156">Module 1 :</span><span class="sxs-lookup"><span data-stu-id="bd7e1-156">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(q=5,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port


#### <a name="module-2"></a><span data-ttu-id="bd7e1-157">Module 2 :</span><span class="sxs-lookup"><span data-stu-id="bd7e1-157">Module 2:</span></span>
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    prob = pbinom(param$q,size=param$size,prob=param$prob)
    prob.eq = dbinom(param$q,size=param$size,prob=param$prob)
    df = data.frame(x=1:param$size, prob=dbinom(1:param$size, param$size, prob=param$prob))
    prob

    if (param$side == 'U'){
    prob = 1 - prob
    band=subset(df,x>param$q)
    } else if (param$side =='E') {
    prob = prob.eq
    band=subset(df,x==param$q)
    } else if (param$side =='L') {
    prob = prob
    band=subset(df,x<=param$q)
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(prob)

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

### <a name="binomial-distribution-generator"></a><span data-ttu-id="bd7e1-158">Générateur de distribution binomiale</span><span class="sxs-lookup"><span data-stu-id="bd7e1-158">Binomial Distribution Generator</span></span>
![Create workspace][6]

#### <a name="module-1"></a><span data-ttu-id="bd7e1-160">Module 1 :</span><span class="sxs-lookup"><span data-stu-id="bd7e1-160">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(n=50,size=10,p=.5);
    maml.mapOutputPort("data.set"); #send data toooutput port

#### <a name="module-2"></a><span data-ttu-id="bd7e1-161">Module 2 :</span><span class="sxs-lookup"><span data-stu-id="bd7e1-161">Module 2:</span></span>
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    dist = rbinom(param$n,param$size,param$p)

    output = as.data.frame(t(dist))

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

## <a name="limitations"></a><span data-ttu-id="bd7e1-162">Limites</span><span class="sxs-lookup"><span data-stu-id="bd7e1-162">Limitations</span></span>
<span data-ttu-id="bd7e1-163">Voici des exemples très simples qui entoure hello binomiale.</span><span class="sxs-lookup"><span data-stu-id="bd7e1-163">These are very simple examples surrounding hello binomial distribution.</span></span> <span data-ttu-id="bd7e1-164">Comme le montre hello exemple de code ci-dessus, peu interception des erreurs est implémentée.</span><span class="sxs-lookup"><span data-stu-id="bd7e1-164">As can be seen from hello example code above, little error catching is implemented.</span></span>

## <a name="faq"></a><span data-ttu-id="bd7e1-165">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="bd7e1-165">FAQ</span></span>
<span data-ttu-id="bd7e1-166">Pour les questions fréquemment posées sur la consommation de service web de hello ou publication toohello Azure Marketplace, consultez [ici](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="bd7e1-166">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_1.png

[2]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_2.png

[3]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_3.png

[4]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_4.png

[5]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_5.png

[6]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_6.png

