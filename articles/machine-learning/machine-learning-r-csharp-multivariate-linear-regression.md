---
title: "(déconseillé) Régression linéaire multivariable - Azure | Microsoft Docs"
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
redirect_document_id: TRUE
ms.openlocfilehash: 65a8005139e920cd19593e954fc1bf836354bdf3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-multivariate-linear-regression"></a><span data-ttu-id="4801f-103">(déconseillé) Régression linéaire multivariable</span><span class="sxs-lookup"><span data-stu-id="4801f-103">(deprecated) Multivariate Linear Regression</span></span>

> [!NOTE]
> <span data-ttu-id="4801f-104">Microsoft DataMarket va être mis hors service et cette API est désormais déconseillée.</span><span class="sxs-lookup"><span data-stu-id="4801f-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="4801f-105">Vous trouverez de nombreux exemples d’expériences et d’API dans la [galerie Cortana Intelligence](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="4801f-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="4801f-106">Pour plus d’informations sur la galerie, consultez [Partager et découvrir des ressources dans la galerie Cortana Intelligence](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="4801f-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="4801f-107">Supposons que vous disposez d’un jeu de données et que vous souhaitez prédire rapidement une variable dépendante (y) pour chaque individu (i) sur la base de variables indépendantes.</span><span class="sxs-lookup"><span data-stu-id="4801f-107">Suppose you have a dataset and would like to quickly predict a dependent variable (y) for each individual (i) based on independent variables.</span></span> <span data-ttu-id="4801f-108">La régression linéaire est une technique statistique répandue qui est utilisée pour de telles prédictions.</span><span class="sxs-lookup"><span data-stu-id="4801f-108">Linear regression is a popular statistical technique used for such predictions.</span></span> <span data-ttu-id="4801f-109">Ici, la variable dépendante y est supposée être une valeur continue.</span><span class="sxs-lookup"><span data-stu-id="4801f-109">Here the dependent variable y is assumed to be a continuous value.</span></span>  

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="4801f-110">Exemple de scénario simple : un chercheur tente de prédire le poids d'un individu (y) en fonction de sa taille (x).</span><span class="sxs-lookup"><span data-stu-id="4801f-110">A simple scenario could be where the researcher is trying to predict the weight of an individual (y) based on their height (x).</span></span> <span data-ttu-id="4801f-111">Exemple de scénario plus avancé : un chercheur dispose d'informations supplémentaires concernant la personne (par exemple, son poids, son genre et sa race) et tente de prédire son poids.</span><span class="sxs-lookup"><span data-stu-id="4801f-111">A more advanced scenario could be where the researcher has additional information for the individual (such as weight, gender, race) and attempts to predict the weight of the individual.</span></span> <span data-ttu-id="4801f-112">Ce [service web](https://datamarket.azure.com/dataset/aml_labs/multivariate_regression) correspond au modèle de régression linéaire pour les données et renvoie la valeur prédite (y) pour chacune des observations dans les données.</span><span class="sxs-lookup"><span data-stu-id="4801f-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/multivariate_regression) fits the linear regression model to the data and outputs the predicted value (y) for each of the observations in the data.</span></span>

> <span data-ttu-id="4801f-113">Les utilisateurs peuvent potentiellement accéder à ce service web par le biais d’une application mobile, d’un site web ou même d’un ordinateur local, par exemple.</span><span class="sxs-lookup"><span data-stu-id="4801f-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="4801f-114">Mais l’objectif du service web est également de servir d’exemple d’utilisation d’Azure Machine Learning pour créer des services web avec le code R.</span><span class="sxs-lookup"><span data-stu-id="4801f-114">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="4801f-115">Avec seulement quelques lignes de code R et quelques clics dans Azure Machine Learning Studio, vous pouvez créer une expérience avec le code R et la publier en tant que service web.</span><span class="sxs-lookup"><span data-stu-id="4801f-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="4801f-116">Le service web peut ensuite être publié sur Azure Marketplace afin que les utilisateurs et les appareils du monde entier l’utilisent sans que l’auteur du service web n’ait à configurer l’infrastructure.</span><span class="sxs-lookup"><span data-stu-id="4801f-116">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="4801f-117">Utilisation du service web</span><span class="sxs-lookup"><span data-stu-id="4801f-117">Consumption of web service</span></span>
<span data-ttu-id="4801f-118">Ce service web fournit les valeurs prédites de la variable dépendante sur base des variables indépendantes pour toutes les observations.</span><span class="sxs-lookup"><span data-stu-id="4801f-118">This web service gives the predicted values of the dependent variable based on the independent variables for all of the observations.</span></span> <span data-ttu-id="4801f-119">Le service web attend de l’utilisateur final qu’il entre ses données sous forme de chaîne, dans laquelle les lignes sont séparées par des virgules (,) et les colonnes sont séparées par des points-virgules (;).</span><span class="sxs-lookup"><span data-stu-id="4801f-119">The web service expects the end user to input data as a string where rows are separated by commas (,) and columns are separated by semicolons (;).</span></span> <span data-ttu-id="4801f-120">Le service web attend 1 ligne à la fois et requiert que la première colonne soit la variable dépendante.</span><span class="sxs-lookup"><span data-stu-id="4801f-120">The web service expects 1 row at a time and expects the first column to be the dependent variable.</span></span> <span data-ttu-id="4801f-121">Un exemple de jeu de données pourrait ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="4801f-121">An example dataset could look like this:</span></span>

![Exemples de données][1]

<span data-ttu-id="4801f-123">Les observations sans variable dépendante doivent être entrées en tant que « NA » pour y.</span><span class="sxs-lookup"><span data-stu-id="4801f-123">Observations without a dependent variable should be input as “NA” for y.</span></span> <span data-ttu-id="4801f-124">Les données d’entrée pour le jeu de données ci-dessus seraient les suivantes : « 10;5;2,18;1;6,6;5.3;2.1,7;5;5,22;3;4,12;2;1,NA;3;4 ».</span><span class="sxs-lookup"><span data-stu-id="4801f-124">The data input for the above dataset would be the following string: “10;5;2,18;1;6,6;5.3;2.1,7;5;5,22;3;4,12;2;1,NA;3;4”.</span></span> <span data-ttu-id="4801f-125">La sortie correspond à la valeur prédite pour chacune des lignes selon les variables indépendantes.</span><span class="sxs-lookup"><span data-stu-id="4801f-125">The output is the predicted value for each of the rows based on the independent variables.</span></span> 

> <span data-ttu-id="4801f-126">Étant hébergé sur Azure Marketplace, ce service est un service OData. Il peut être appelé à l’aide des méthodes POST ou GET.</span><span class="sxs-lookup"><span data-stu-id="4801f-126">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="4801f-127">Il existe plusieurs façons d’utiliser le service de manière automatique (un exemple d’application est disponible [ici](http://microsoftazuremachinelearning.azurewebsites.net/MultipleLinearRegressionService.aspx)).</span><span class="sxs-lookup"><span data-stu-id="4801f-127">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/MultipleLinearRegressionService.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="4801f-128">Début du code C# pour l'utilisation du service web :</span><span class="sxs-lookup"><span data-stu-id="4801f-128">Starting C# code for web service consumption:</span></span>
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




## <a name="creation-of-web-service"></a><span data-ttu-id="4801f-129">Création du service web</span><span class="sxs-lookup"><span data-stu-id="4801f-129">Creation of web service</span></span>
> <span data-ttu-id="4801f-130">Ce service web a été créé à l’aide d’Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="4801f-130">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="4801f-131">Pour un essai gratuit, ainsi que des vidéos de présentation relatives à la création d’expériences et à la [publication de services web](machine-learning-publish-a-machine-learning-web-service.md), consultez [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="4801f-131">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="4801f-132">Voici une capture d'écran de l'expérience qui a créé le service web et l'exemple de code pour chacun des modules dans l'expérience.</span><span class="sxs-lookup"><span data-stu-id="4801f-132">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="4801f-133">À partir d’Azure Machine Learning, une nouvelle expérience vide a été créée et deux modules [Exécuter le script R][execute-r-script] ont été importés dans l’espace de travail.</span><span class="sxs-lookup"><span data-stu-id="4801f-133">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules were pulled onto the workspace.</span></span> <span data-ttu-id="4801f-134">Ce service web exécute une expérience Azure Machine Learning avec un script R sous-jacent.</span><span class="sxs-lookup"><span data-stu-id="4801f-134">This web service runs an Azure Machine Learning experiment with an underlying R script.</span></span> <span data-ttu-id="4801f-135">Cette expérience se divise en 2 parties : définition du schéma et modèle d’apprentissage + évaluation.</span><span class="sxs-lookup"><span data-stu-id="4801f-135">There are 2 parts to this experiment: schema definition, and training model + scoring.</span></span> <span data-ttu-id="4801f-136">Le premier module définit la structure attendue du jeu de données en entrée, où la première variable correspond à la variable dépendante et les autres variables sont indépendantes.</span><span class="sxs-lookup"><span data-stu-id="4801f-136">The first module defines the expected structure of the input dataset, where the first variable is the dependent variable and the remaining variables are independent.</span></span> <span data-ttu-id="4801f-137">Le deuxième module correspond à un modèle de régression linéaire générique pour les données en entrée.</span><span class="sxs-lookup"><span data-stu-id="4801f-137">The second module fits a generic linear regression model for the input data.</span></span>  

![Flux de l’expérience][3]

#### <a name="module-1"></a><span data-ttu-id="4801f-139">Module 1 :</span><span class="sxs-lookup"><span data-stu-id="4801f-139">Module 1:</span></span>
#### <a name="schema-definition"></a><span data-ttu-id="4801f-140">Définition de schéma</span><span class="sxs-lookup"><span data-stu-id="4801f-140">Schema definition</span></span>
    data <- data.frame(value = "1;2;3,4;5;6,7;8;9", stringsAsFactors=FALSE) maml.mapOutputPort("data");  

#### <a name="module-2"></a><span data-ttu-id="4801f-141">Module 2 :</span><span class="sxs-lookup"><span data-stu-id="4801f-141">Module 2:</span></span>
#### <a name="lm-modeling"></a><span data-ttu-id="4801f-142">Modélisation LM</span><span class="sxs-lookup"><span data-stu-id="4801f-142">LM modeling</span></span>
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

## <a name="limitations"></a><span data-ttu-id="4801f-143">Limitations</span><span class="sxs-lookup"><span data-stu-id="4801f-143">Limitations</span></span>
<span data-ttu-id="4801f-144">Il s'agit d'un exemple très simple de service web pour régressions linéaires multiples.</span><span class="sxs-lookup"><span data-stu-id="4801f-144">This is a very simple example of a multiple linear regression web service.</span></span> <span data-ttu-id="4801f-145">Comme illustré dans l’exemple de code ci-dessus, aucune interception des erreurs n’est implémentée et le service suppose que tout correspond à une variable continue (aucune fonctionnalité de catégorie n’est autorisée), dans la mesure où le service entre uniquement des valeurs numériques au moment de la création de ce service web.</span><span class="sxs-lookup"><span data-stu-id="4801f-145">As can be seen from the example code above, no error catching is implemented and the service assumes everything is a continuous variable (no categorical features allowed), as the service only inputs numeric values at the time of the creation of this web service.</span></span> <span data-ttu-id="4801f-146">En outre, le service gère actuellement une limite de taille pour les données, en raison de la nature de la demande/réponse de l’appel de service web et du fait que le modèle est adapté chaque fois que le service web est appelé.</span><span class="sxs-lookup"><span data-stu-id="4801f-146">Also, the service currently handles limited data size, due to the request/response nature of the web service call and the fact that the model is being fit every time the web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="4801f-147">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="4801f-147">FAQ</span></span>
<span data-ttu-id="4801f-148">Pour les questions fréquemment posées relatives à l’utilisation du service web ou à la publication sur Azure Marketplace, consultez [ce lien](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="4801f-148">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img1.png
[2]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img2.png
[3]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

