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
# <a name="deprecated-binomial-distribution-suite"></a>(obsolète) Suite de distribution binomiale

> [!NOTE]
> Hello Microsoft DataMarket a été supprimée et que cette API est déconseillée. 
> 
> Vous trouverez plusieurs API et les expériences d’exemple utile Bonjour [Cortana Intelligence galerie](http://gallery.cortanaintelligence.com). Pour plus d’informations sur la galerie de hello, consultez [partager et découvrir des ressources Bonjour Cortana Intelligence galerie](machine-learning-gallery-how-to-use-contribute-publish.md).

Hello Suite de la Distribution binomiale est un ensemble d’exemples de services web ([binomiale Générateur](https://datamarket.azure.com/dataset/aml_labs/bdg5), [probabilité calculatrice](https://datamarket.azure.com/dataset/aml_labs/bdp4), [Quantile calculatrice](https://datamarket.azure.com/dataset/aml_labs/bdq5)) qui aident à générer et traiter les distributions de binomiale. Hello services autorisent génération d’une séquence de distribution binomiale de n’importe quelle longueur du calcul d’étendue hors fonction de probabilité et la probabilité de calcul à partir d’un quantile donné. Chacun des services de hello émet différentes sorties en fonction de service de hello sélectionné (voir la description ci-dessous). Hello Suite de la Distribution binomiale est basée sur hello R fonctions qbinom, rbinom et pbinom, qui sont inclus dans le package de statistiques hello R. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> Ces services web pouvant être consommées par les utilisateurs – potentiellement directement sur le marketplace hello, via une application mobile, via un site Web, ou même sur un ordinateur local, par exemple. Mais hello objectif du service web de hello est également tooserve comme exemple illustrant comment Azure Machine Learning peuvent être des services web toocreate utilisé sur le code R. Avec seulement quelques lignes de code R et quelques clics dans Azure Machine Learning Studio, vous pouvez créer une expérience avec le code R et la publier en tant que service web. service web de Hello peut ensuite être publié toohello Azure Marketplace et consommé par les utilisateurs et périphériques sur Bonjour – infrastructure par l’auteur de hello du service web de hello n’exige aucune configuration.
> 
> 

## <a name="consumption-of-web-service"></a>Utilisation du service web
Hello Distribution binomiale Suite inclut hello suivant 3 services.

### <a name="binomial-distribution-quantile-calculator"></a>Calculatrice de quantile pour la distribution binomiale
Ce service accepte des arguments d’une distribution normale 4 et calcule hello associé quantile.
les arguments d’entrée Hello sont :

* p : probabilité unique agrégée de plusieurs essais  
* taille - nombre hello d’essais.
* probabilité - probabilité hello de réussite d’une version d’évaluation.
* Côté - L pour la partie inférieure de hello de distribution hello, U pour la partie supérieure de hello de distribution de hello. 

sortie de Hello du service de hello est quantile hello calculée qui est associée à hello fonction de probabilité.

### <a name="binomial-distribution-probability-calculator"></a>Calculatrice de probabilité de distribution binomiale
Ce service accepte des arguments d’une distribution binomiale 4 et calcule la probabilité de hello associé.
les arguments d’entrée Hello sont :

* q : quantile unique d’un événement avec une distribution binomiale 
* taille - nombre hello d’essais.
* probabilité - probabilité hello de réussite d’une version d’évaluation.
* côté - L pour la partie inférieure de hello de distribution hello, U pour la partie supérieure de hello de distribution de hello ou E est égale tooa le nombre unique de succès.

sortie Hello du service de hello représente la probabilité hello calculé hello donné quantile est associée.

### <a name="binomial-distribution-generator"></a>Générateur de distribution binomiale
Ce service accepte 3 arguments d'une distribution binomiale et génère une séquence aléatoire de nombres qui sont distribués selon une loi binomiale. Hello arguments suivants doivent être fournis tooit au sein de la demande de hello :

* n : nombre d’observations 
* size : nombre d’essais
* prob : probabilité de réussite

sortie Hello du service de hello est une séquence de longueur n avec une distribution binomiale basée sur les arguments de taille et prob hello.

> Ce service, comme hébergé sur hello Azure Marketplace, est un service OData ; Il peuvent être appelées par le biais des méthodes POST ou GET. 
> 
> 

Il existe plusieurs manières de consommation de service hello de manière automatique (exemple applications sont ici : [Générateur](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionGenerator.aspx), [probabilité calculatrice](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionProbabilityCalculator.aspx), [Quantile calculatrice](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionQuantileCalculator)). 

### <a name="starting-c-code-for-web-service-consumption"></a>Début du code C# pour l'utilisation du service web :
### <a name="binomial-distribution-quantile-calculator"></a>Calculatrice de quantile pour la distribution binomiale
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

### <a name="binomial-distribution-probability-calculator"></a>Calculatrice de probabilité de distribution binomiale
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


### <a name="binomial-distribution-generator"></a>Générateur de distribution binomiale
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





## <a name="creation-of-web-service"></a>Création du service web
> Ce service web a été créé à l’aide d’Azure Machine Learning. Pour un essai gratuit, ainsi que des vidéos de présentation relatives à la création d’expériences et à la [publication de services web](machine-learning-publish-a-machine-learning-web-service.md), consultez [azure.com/ml](http://azure.com/ml). Voici une capture d’écran d’expérience hello qui a créé un code de service et un exemple hello web pour chacun des modules hello au sein de l’expérience de hello.
> 
> 

### <a name="binomial-distribution-quantile-calculator"></a>Calculatrice de quantile pour la distribution binomiale
![Create workspace][4]

#### <a name="module-1"></a>Module 1 :
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(p=0.1,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port
#### <a name="module-2"></a>Module 2 :
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


### <a name="binomial-distribution-probability-calculator"></a>Calculatrice de probabilité de distribution binomiale
![Create workspace][5]

#### <a name="module-1"></a>Module 1 :
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(q=5,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port


#### <a name="module-2"></a>Module 2 :
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

### <a name="binomial-distribution-generator"></a>Générateur de distribution binomiale
![Create workspace][6]

#### <a name="module-1"></a>Module 1 :
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(n=50,size=10,p=.5);
    maml.mapOutputPort("data.set"); #send data toooutput port

#### <a name="module-2"></a>Module 2 :
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    dist = rbinom(param$n,param$size,param$p)

    output = as.data.frame(t(dist))

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

## <a name="limitations"></a>Limites
Voici des exemples très simples qui entoure hello binomiale. Comme le montre hello exemple de code ci-dessus, peu interception des erreurs est implémentée.

## <a name="faq"></a>Forum Aux Questions
Pour les questions fréquemment posées sur la consommation de service web de hello ou publication toohello Azure Marketplace, consultez [ici](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_1.png

[2]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_2.png

[3]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_3.png

[4]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_4.png

[5]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_5.png

[6]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_6.png

