---
title: "(obsolète) Classificateur binaire - Azure | Microsoft Docs"
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
redirect_document_id: TRUE
ms.openlocfilehash: 1a83392f90bb5a9fb183334c03ccec20dd3f3520
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-binary-classifier"></a><span data-ttu-id="5fb7d-103">(obsolète) Classificateur binaire</span><span class="sxs-lookup"><span data-stu-id="5fb7d-103">(deprecated) Binary Classifier</span></span>

> [!NOTE]
> <span data-ttu-id="5fb7d-104">Microsoft DataMarket va être supprimé et cette API est désormais obsolète.</span><span class="sxs-lookup"><span data-stu-id="5fb7d-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="5fb7d-105">Vous trouverez de nombreux exemples d’expériences et d’API dans la [galerie Cortana Intelligence](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="5fb7d-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="5fb7d-106">Pour plus d’informations sur la galerie, consultez [Partager et découvrir des solutions dans la galerie Cortana Intelligence](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="5fb7d-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="5fb7d-107">Supposez que vous disposiez d'un jeu de données et que vous aimeriez prédire une variable dépendante binaire sur base de variables indépendantes.</span><span class="sxs-lookup"><span data-stu-id="5fb7d-107">Suppose you have a dataset and would like to predict a binary dependent variable based on the independent variables.</span></span> <span data-ttu-id="5fb7d-108">La « régression logistique » est une technique statistique très répandue qui est utilisée pour de telles prédictions.</span><span class="sxs-lookup"><span data-stu-id="5fb7d-108">‘Logistic Regression’ is a popular statistical technique used for such predictions.</span></span> <span data-ttu-id="5fb7d-109">Ici, la variable dépendante est binaire ou dichotomique et p correspond à la probabilité de la présence de la caractéristique d’intérêt.</span><span class="sxs-lookup"><span data-stu-id="5fb7d-109">Here the dependent variable is binary or dichotomous, and p is the probability of presence of the characteristic of interest.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="5fb7d-110">Dans un scénario simple, un chercheur tente de prédire si un étudiant potentiel est susceptible d’accepter l’offre d’admission pour une université en fonction d’informations (moyenne générale au lycée, revenus familiaux, pays/état de résidence, sexe).</span><span class="sxs-lookup"><span data-stu-id="5fb7d-110">A simple scenario could be where a researcher is trying to predict whether a prospective student is likely to accept an admission offer to a university based on information (GPA in high school, family income, resident state, gender).</span></span> <span data-ttu-id="5fb7d-111">Le résultat prédit correspond à la probabilité qu’un éventuel futur étudiant accepte l’offre d’admission.</span><span class="sxs-lookup"><span data-stu-id="5fb7d-111">The predicted outcome is the probability of the prospective student accepting the admission offer.</span></span> <span data-ttu-id="5fb7d-112">Ce [service web](https://datamarket.azure.com/dataset/aml_labs/log_regression) correspond au modèle de régression logistique pour les données et renvoie la valeur de probabilité (y) pour chacune des observations dans les données.</span><span class="sxs-lookup"><span data-stu-id="5fb7d-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/log_regression) fits the logistic regression model to the data and outputs the probability value (y) for each of the observations in the data.</span></span>  

> <span data-ttu-id="5fb7d-113">Les utilisateurs peuvent potentiellement accéder à ce service web par le biais d’une application mobile, d’un site web ou même d’un ordinateur local, par exemple.</span><span class="sxs-lookup"><span data-stu-id="5fb7d-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="5fb7d-114">Mais l’objectif du service web est également de servir d’exemple d’utilisation d’Azure Machine Learning pour créer des services web avec le code R.</span><span class="sxs-lookup"><span data-stu-id="5fb7d-114">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="5fb7d-115">Avec seulement quelques lignes de code R et quelques clics dans Azure Machine Learning Studio, vous pouvez créer une expérience avec le code R et la publier en tant que service web.</span><span class="sxs-lookup"><span data-stu-id="5fb7d-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="5fb7d-116">Le service web peut ensuite être publié sur Azure Marketplace afin que les utilisateurs et les appareils du monde entier l’utilisent sans que l’auteur du service web n’ait à configurer l’infrastructure.</span><span class="sxs-lookup"><span data-stu-id="5fb7d-116">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="5fb7d-117">Utilisation du service web</span><span class="sxs-lookup"><span data-stu-id="5fb7d-117">Consumption of web service</span></span>
<span data-ttu-id="5fb7d-118">Ce service web fournit les valeurs prédites de la variable dépendante sur base des variables indépendantes pour toutes les observations.</span><span class="sxs-lookup"><span data-stu-id="5fb7d-118">This web service gives the predicted values of the dependent variable based on the independent variables for all of the observations.</span></span> <span data-ttu-id="5fb7d-119">Le service web attend de l’utilisateur final qu’il entre ses données sous forme de chaîne, dans laquelle les lignes sont séparées par des virgules (,) et les colonnes sont séparées par des points-virgules (;).</span><span class="sxs-lookup"><span data-stu-id="5fb7d-119">The web service expects the end user to input data as a string where rows are separated by comma (,) and columns are separated by semicolon (;).</span></span> <span data-ttu-id="5fb7d-120">Le service web attend 1 ligne à la fois et requiert que la première colonne soit la variable dépendante.</span><span class="sxs-lookup"><span data-stu-id="5fb7d-120">The web service expects 1 row at a time and expects the first column to be the dependent variable.</span></span> <span data-ttu-id="5fb7d-121">Un exemple de jeu de données pourrait ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="5fb7d-121">An example dataset could look like this:</span></span>

![Exemples de données][1]

<span data-ttu-id="5fb7d-123">Les observations sans variable dépendante doivent être entrées en tant que « NA » pour y.</span><span class="sxs-lookup"><span data-stu-id="5fb7d-123">Observations without a dependent variable should be input as “NA” for y.</span></span> <span data-ttu-id="5fb7d-124">Les données d’entrée pour le jeu de données ci-dessus seraient les suivantes : « 1;5;2,1;1;6,0;5.3;2.1,0;5;5,0;3;4,1;2;1,NA;3;4 ».</span><span class="sxs-lookup"><span data-stu-id="5fb7d-124">The data input for the above dataset would be the following string: “1;5;2,1;1;6,0;5.3;2.1,0;5;5,0;3;4,1;2;1,NA;3;4”.</span></span> <span data-ttu-id="5fb7d-125">La sortie correspond à la valeur prédite pour chacune des lignes selon les variables indépendantes.</span><span class="sxs-lookup"><span data-stu-id="5fb7d-125">The output is the predicted value for each of the rows based on the independent variables.</span></span> 

> <span data-ttu-id="5fb7d-126">Étant hébergé sur Azure Marketplace, ce service est un service OData. Il peut être appelé à l’aide des méthodes POST ou GET.</span><span class="sxs-lookup"><span data-stu-id="5fb7d-126">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="5fb7d-127">Il existe plusieurs façons d’utiliser le service de manière automatique (un exemple d’application est disponible [ici](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)).</span><span class="sxs-lookup"><span data-stu-id="5fb7d-127">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="5fb7d-128">Début du code C# pour l'utilisation du service web :</span><span class="sxs-lookup"><span data-stu-id="5fb7d-128">Starting C# code for web service consumption:</span></span>
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


## <a name="creation-of-web-service"></a><span data-ttu-id="5fb7d-129">Création du service web</span><span class="sxs-lookup"><span data-stu-id="5fb7d-129">Creation of web service</span></span>
> <span data-ttu-id="5fb7d-130">Ce service web a été créé à l’aide d’Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="5fb7d-130">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="5fb7d-131">Pour un essai gratuit, ainsi que des vidéos de présentation relatives à la création d’expériences et à la [publication de services web](machine-learning-publish-a-machine-learning-web-service.md), consultez [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="5fb7d-131">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="5fb7d-132">Voici une capture d'écran de l'expérience qui a créé le service web et l'exemple de code pour chacun des modules dans l'expérience.</span><span class="sxs-lookup"><span data-stu-id="5fb7d-132">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="5fb7d-133">À partir d’Azure Machine Learning, une nouvelle expérience vierge a été créée et deux modules [Exécuter le script R][execute-r-script] ont été importés dans l’espace de travail.</span><span class="sxs-lookup"><span data-stu-id="5fb7d-133">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules pulled onto the workspace.</span></span> <span data-ttu-id="5fb7d-134">Ce service web exécute une expérience Azure Machine Learning avec un script R sous-jacent.</span><span class="sxs-lookup"><span data-stu-id="5fb7d-134">This web service runs an Azure Machine Learning experiment with an underlying R script.</span></span> <span data-ttu-id="5fb7d-135">Cette expérience se divise en 2 parties : définition du schéma et modèle d’apprentissage + évaluation.</span><span class="sxs-lookup"><span data-stu-id="5fb7d-135">There are 2 parts to this experiment: schema definition, and training model + scoring.</span></span> <span data-ttu-id="5fb7d-136">Le premier module définit la structure attendue du jeu de données en entrée, où la première variable correspond à la variable dépendante et les autres variables sont indépendantes.</span><span class="sxs-lookup"><span data-stu-id="5fb7d-136">The first module defines the expected structure of the input dataset, where the first variable is the dependent variable and the remaining variables are independent.</span></span> <span data-ttu-id="5fb7d-137">Le deuxième module correspond à un modèle de régression logistique générique pour les données en entrée.</span><span class="sxs-lookup"><span data-stu-id="5fb7d-137">The second module fits a generic logistic regression model for the input data.</span></span>    

![Flux de l’expérience][2]

#### <a name="module-1"></a><span data-ttu-id="5fb7d-139">Module 1 :</span><span class="sxs-lookup"><span data-stu-id="5fb7d-139">Module 1:</span></span>
    #Schema definition  
    data <- data.frame(value = "1;2;3,1;5;6,0;8;9", stringsAsFactors=FALSE) 
    maml.mapOutputPort("data");  

#### <a name="module-2"></a><span data-ttu-id="5fb7d-140">Module 2 :</span><span class="sxs-lookup"><span data-stu-id="5fb7d-140">Module 2:</span></span>
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


## <a name="limitations"></a><span data-ttu-id="5fb7d-141">Limitations</span><span class="sxs-lookup"><span data-stu-id="5fb7d-141">Limitations</span></span>
<span data-ttu-id="5fb7d-142">Il s'agit d'un exemple très simple de service web de classification binaire.</span><span class="sxs-lookup"><span data-stu-id="5fb7d-142">This is a very simple example of a binary classification web service.</span></span> <span data-ttu-id="5fb7d-143">Comme illustré dans l’exemple de code ci-dessus, aucune interception des erreurs n’est implémentée et le service suppose que tout correspond à une variable binaire/continue (aucune fonctionnalité de catégorie n’est autorisée), dans la mesure où le service entre uniquement des valeurs numériques au moment de la création de ce service web.</span><span class="sxs-lookup"><span data-stu-id="5fb7d-143">As can be seen from the example code above, no error catching is implemented and the service assumes everything is a binary/continuous variable (no categorical features allowed), as the service only inputs numeric values at the time of the creation of this web service.</span></span> <span data-ttu-id="5fb7d-144">En outre, le service gère actuellement une limite de taille pour les données, en raison de la nature de la demande/réponse de l’appel de service web et du fait que le modèle est adapté chaque fois que le service web est appelé.</span><span class="sxs-lookup"><span data-stu-id="5fb7d-144">Also, the service currently handles limited data size, due to the request/response nature of the web service call and the fact that the model is being fit every time the web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="5fb7d-145">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="5fb7d-145">FAQ</span></span>
<span data-ttu-id="5fb7d-146">Pour les questions fréquemment posées relatives à l’utilisation du service web ou à la publication sur Azure Marketplace, consultez [ce lien](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="5fb7d-146">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-binary-classifier/binary1.png
[2]: ./media/machine-learning-r-csharp-binary-classifier/binary2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

