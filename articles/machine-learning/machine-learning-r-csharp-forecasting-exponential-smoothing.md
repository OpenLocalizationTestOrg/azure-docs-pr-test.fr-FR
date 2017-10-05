---
title: "(obsolète) Prévisions - Lissage exponentiel - Azure | Microsoft Docs"
description: "(obsolète) Service web : prévisions - Lissage exponentiel"
services: machine-learning
documentationcenter: 
author: yijichen
manager: jhubbard
editor: cgronlun
ms.assetid: a4150681-6eac-4145-9eca-0cdf60781dde
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: yijichen
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: TRUE
ms.openlocfilehash: 736d5d4adb8ecfd1e3372d273b64917f4a2e76ce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-forecasting---exponential-smoothing"></a><span data-ttu-id="4462d-103">(obsolète) Prévisions : lissage exponentiel</span><span class="sxs-lookup"><span data-stu-id="4462d-103">(deprecated) Forecasting - Exponential Smoothing</span></span>

> [!NOTE]
> <span data-ttu-id="4462d-104">Microsoft DataMarket va être supprimé et cette API est désormais obsolète.</span><span class="sxs-lookup"><span data-stu-id="4462d-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="4462d-105">Vous trouverez de nombreux exemples d’expériences et d’API dans la [galerie Cortana Intelligence](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="4462d-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="4462d-106">Pour plus d’informations sur la galerie, consultez [Partager et découvrir des solutions dans la galerie Cortana Intelligence](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="4462d-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="4462d-107">Ce [service web](https://datamarket.azure.com/dataset/aml_labs/ets) met en œuvre un modèle de lissage exponentiel (ETS) pour produire des prédictions basées sur les données d’historique fournies par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4462d-107">This [web service](https://datamarket.azure.com/dataset/aml_labs/ets) implements the Exponential Smoothing model (ETS) to produce predictions based on the historical data provided by the user.</span></span> <span data-ttu-id="4462d-108">La demande pour un produit spécifique va-t-elle augmenter cette année ?</span><span class="sxs-lookup"><span data-stu-id="4462d-108">Will the demand for a specific product increase this year?</span></span> <span data-ttu-id="4462d-109">Puis-je prévoir les ventes de mes produits pour Noël afin de planifier efficacement mon inventaire ?</span><span class="sxs-lookup"><span data-stu-id="4462d-109">Can I predict my product sales for the Christmas season, so that I can effectively plan my inventory?</span></span> <span data-ttu-id="4462d-110">Les modèles de prévision sont en mesure de répondre à ces questions.</span><span class="sxs-lookup"><span data-stu-id="4462d-110">Forecasting models are apt to address such questions.</span></span> <span data-ttu-id="4462d-111">Ces modèles examinent les tendances cachées et de saison sur la base des données passées afin de prévoir les tendances futures.</span><span class="sxs-lookup"><span data-stu-id="4462d-111">Given the past data, these models examine hidden trends and seasonality to predict future trends.</span></span>  

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="4462d-112">Les utilisateurs peuvent potentiellement accéder à ce service web par le biais d’une application mobile, d’un site web ou même d’un ordinateur local, par exemple.</span><span class="sxs-lookup"><span data-stu-id="4462d-112">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="4462d-113">Mais l’objectif du service web est également de servir d’exemple d’utilisation d’Azure Machine Learning pour créer des services web avec le code R.</span><span class="sxs-lookup"><span data-stu-id="4462d-113">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="4462d-114">Avec seulement quelques lignes de code R et quelques clics dans Azure Machine Learning Studio, vous pouvez créer une expérience avec le code R et la publier en tant que service web.</span><span class="sxs-lookup"><span data-stu-id="4462d-114">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="4462d-115">Le service web peut ensuite être publié sur Azure Marketplace afin que les utilisateurs et les appareils du monde entier l’utilisent sans que l’auteur du service web n’ait à configurer l’infrastructure.</span><span class="sxs-lookup"><span data-stu-id="4462d-115">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="4462d-116">Utilisation du service web</span><span class="sxs-lookup"><span data-stu-id="4462d-116">Consumption of web service</span></span>
<span data-ttu-id="4462d-117">Ce service accepte 4 arguments et calcule les prévisions ETS.</span><span class="sxs-lookup"><span data-stu-id="4462d-117">This service accepts 4 arguments and calculates the ETS forecasts.</span></span>
<span data-ttu-id="4462d-118">Les arguments d'entrée sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="4462d-118">The input arguments are:</span></span>

* <span data-ttu-id="4462d-119">Frequency : indique la fréquence des données brutes (quotidiennes/hebdomadaires/mensuelles/trimestrielles/annuelles)</span><span class="sxs-lookup"><span data-stu-id="4462d-119">Frequency - Indicates the frequency of the raw data (daily/weekly/monthly/quarterly/yearly).</span></span>
* <span data-ttu-id="4462d-120">Horizon : durée de validité des prévisions</span><span class="sxs-lookup"><span data-stu-id="4462d-120">Horizon - Future forecast time-frame.</span></span>
* <span data-ttu-id="4462d-121">Date : ajoute les nouvelles données de série temporelle</span><span class="sxs-lookup"><span data-stu-id="4462d-121">Date - Add in the new time series data for time.</span></span>
* <span data-ttu-id="4462d-122">Value : ajoute les nouvelles valeurs de données de série temporelle</span><span class="sxs-lookup"><span data-stu-id="4462d-122">Value - Add in the new time series data values.</span></span>

<span data-ttu-id="4462d-123">La sortie du service est constituée des valeurs prévisionnelles calculées.</span><span class="sxs-lookup"><span data-stu-id="4462d-123">The output of the service is the calculated forecast values.</span></span>

<span data-ttu-id="4462d-124">Exemple d'entrée :</span><span class="sxs-lookup"><span data-stu-id="4462d-124">Sample input could be:</span></span> 

* <span data-ttu-id="4462d-125">Frequency : 12</span><span class="sxs-lookup"><span data-stu-id="4462d-125">Frequency - 12</span></span>
* <span data-ttu-id="4462d-126">Horizon : 12</span><span class="sxs-lookup"><span data-stu-id="4462d-126">Horizon - 12</span></span>
* <span data-ttu-id="4462d-127">Date : 1/15/2012;2/15/2012;3/15/2012;4/15/2012;5/15/2012;6/15/2012;7/15/2012;8/15/2012;9/15/2012;10/15/2012;11/15/2012;12/15/2012; 1/15/2013;2/15/2013;3/15/2013;4/15/2013;5/15/2013;6/15/2013;7/15/2013;8/15/2013;9/15/2013;10/15/2013;11/15/2013;12/15/2013; 1/15/2014;2/15/2014;3/15/2014;4/15/2014;5/15/2014;6/15/2014;7/15/2014;8/15/2014;9/15/2014</span><span class="sxs-lookup"><span data-stu-id="4462d-127">Date - 1/15/2012;2/15/2012;3/15/2012;4/15/2012;5/15/2012;6/15/2012;7/15/2012;8/15/2012;9/15/2012;10/15/2012;11/15/2012;12/15/2012; 1/15/2013;2/15/2013;3/15/2013;4/15/2013;5/15/2013;6/15/2013;7/15/2013;8/15/2013;9/15/2013;10/15/2013;11/15/2013;12/15/2013; 1/15/2014;2/15/2014;3/15/2014;4/15/2014;5/15/2014;6/15/2014;7/15/2014;8/15/2014;9/15/2014</span></span>
* <span data-ttu-id="4462d-128">Value : 3.479;3.68;3.832;3.941;3.797;3.586;3.508;3.731;3.915;3.844;3.634;3.549;3.557;3.785;3.782;3.601;3.544;3.556;3.65;3.709;3.682;3.511; 3.429;3.51;3.523;3.525;3.626;3.695;3.711;3.711;3.693;3.571;3.509</span><span class="sxs-lookup"><span data-stu-id="4462d-128">Value - 3.479;3.68;3.832;3.941;3.797;3.586;3.508;3.731;3.915;3.844;3.634;3.549;3.557;3.785;3.782;3.601;3.544;3.556;3.65;3.709;3.682;3.511; 3.429;3.51;3.523;3.525;3.626;3.695;3.711;3.711;3.693;3.571;3.509</span></span>

> <span data-ttu-id="4462d-129">Étant hébergé sur Azure Marketplace, ce service est un service OData. Il peut être appelé à l’aide des méthodes POST ou GET.</span><span class="sxs-lookup"><span data-stu-id="4462d-129">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="4462d-130">Il existe plusieurs façons d’utiliser le service de manière automatique (un exemple d’application est disponible [ici](http://microsoftazuremachinelearning.azurewebsites.net/etsForecasting.aspx)).</span><span class="sxs-lookup"><span data-stu-id="4462d-130">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/etsForecasting.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="4462d-131">Début du code C# pour l'utilisation du service web :</span><span class="sxs-lookup"><span data-stu-id="4462d-131">Starting C# code for web service consumption:</span></span>
    public class Input
    {
            public string frequency;
            public string horizon;
            public string date;
            public string value;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { frequency = TextBox1.Text, horizon = TextBox2.Text, date = TextBox3.Text, value = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }



## <a name="creation-of-web-service"></a><span data-ttu-id="4462d-132">Création du service web</span><span class="sxs-lookup"><span data-stu-id="4462d-132">Creation of web service</span></span>
> <span data-ttu-id="4462d-133">Ce service web a été créé à l’aide d’Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="4462d-133">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="4462d-134">Pour un essai gratuit, ainsi que des vidéos de présentation relatives à la création d’expériences et à la [publication de services web](machine-learning-publish-a-machine-learning-web-service.md), consultez [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="4462d-134">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="4462d-135">Voici une capture d'écran de l'expérience qui a créé le service web et l'exemple de code pour chacun des modules dans l'expérience.</span><span class="sxs-lookup"><span data-stu-id="4462d-135">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="4462d-136">Dans Azure Machine Learning, une nouvelle expérience vide a été créée.</span><span class="sxs-lookup"><span data-stu-id="4462d-136">From within Azure Machine Learning, a new blank experiment was created.</span></span> <span data-ttu-id="4462d-137">Des exemples de données d’entrée ont été téléchargés avec un schéma de données prédéfini.</span><span class="sxs-lookup"><span data-stu-id="4462d-137">Sample input data was uploaded with a predefined data schema.</span></span> <span data-ttu-id="4462d-138">Le module [Exécuter le script R][execute-r-script], qui est lié au schéma de données, génère le modèle de prévision ETS à l’aide des fonctions « ets » et « forecast » de R.</span><span class="sxs-lookup"><span data-stu-id="4462d-138">Linked to the data schema is an [Execute R Script][execute-r-script] module that generates the ETS forecasting model by using ‘ets’ and ‘forecast’ functions from R.</span></span> 

![Flux de l’expérience][2]

#### <a name="module-1"></a><span data-ttu-id="4462d-140">Module 1 :</span><span class="sxs-lookup"><span data-stu-id="4462d-140">Module 1:</span></span>
    # Add in the CSV file with the data in the format shown below 
![Exemple de données][3]    

#### <a name="module-2"></a><span data-ttu-id="4462d-142">Module 2 :</span><span class="sxs-lookup"><span data-stu-id="4462d-142">Module 2:</span></span>
    # Data input
    data <- maml.mapInputPort(1) # class: data.frame
    library(forecast)

    # Preprocessing
    colnames(data) <- c("frequency", "horizon", "dates", "values")
    dates <- strsplit(data$dates, ";")[[1]]
    values <- strsplit(data$values, ";")[[1]]

    dates <- as.Date(dates, format = '%m/%d/%Y')
    values <- as.numeric(values)

    # Fit a time-series model
    train_ts<- ts(values, frequency=data$frequency)
    fit1 <- ets(train_ts)
    train_model <- forecast(fit1, h = data$horizon)
    plot(train_model)

    # Produce forcasting
    train_pred <- round(train_model$mean,2)
    data.forecast <- as.data.frame(t(train_pred))
    colnames(data.forecast) <- paste("Forecast", 1:data$horizon, sep="")

    # Data output
    maml.mapOutputPort("data.forecast");


## <a name="limitations"></a><span data-ttu-id="4462d-143">Limitations</span><span class="sxs-lookup"><span data-stu-id="4462d-143">Limitations</span></span>
<span data-ttu-id="4462d-144">Il s'agit d'un exemple très simple destiné aux prévisions ETS.</span><span class="sxs-lookup"><span data-stu-id="4462d-144">This is a very simple example for ETS forecasting.</span></span> <span data-ttu-id="4462d-145">Comme illustré dans l’exemple de code ci-dessus, aucune interception des erreurs n’est implémentée et le service suppose que toutes les variables sont des valeurs continues/positives et que la fréquence doit être un entier supérieur à 1.</span><span class="sxs-lookup"><span data-stu-id="4462d-145">As can be seen from the example code above, no error catching is implemented, and the service assumes that all the variables are continuous/positive values and the frequency should be an integer greater than 1.</span></span> <span data-ttu-id="4462d-146">La longueur des vecteurs de date et de valeur doit être identique.</span><span class="sxs-lookup"><span data-stu-id="4462d-146">The length of the date and value vectors should be the same.</span></span> <span data-ttu-id="4462d-147">La variable de la date doit respecter le format « mm/jj/aaaa ».</span><span class="sxs-lookup"><span data-stu-id="4462d-147">The date variable should adhere to the format ‘mm/dd/yyyy’.</span></span>

## <a name="faq"></a><span data-ttu-id="4462d-148">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="4462d-148">FAQ</span></span>
<span data-ttu-id="4462d-149">Pour les questions fréquemment posées relatives à l’utilisation du service web ou à la publication sur Azure Marketplace, consultez [ce lien](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="4462d-149">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-forecasting-exponential-smoothing/ets-img1.png
[2]: ./media/machine-learning-r-csharp-forecasting-exponential-smoothing/ets-img2.png
[3]: ./media/machine-learning-r-csharp-forecasting-exponential-smoothing/ets-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

