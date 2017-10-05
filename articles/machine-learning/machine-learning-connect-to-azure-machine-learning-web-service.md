---
title: "Connexion à un service web Microsoft Azure Machine Learning | Microsoft Docs"
description: "Via C# ou Python, vous pouvez vous connecter à un service web Microsoft Azure Machine Learning, au moyen d’une clé d’autorisation."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 59b07bab-b60f-48c4-a385-a162e50ec7c2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: garye
ROBOTS: NOINDEX
redirect_url: machine-learning-consume-web-services
redirect_document_id: TRUE
ms.openlocfilehash: 0fc6c7e921b18eb14a95fb737d8fb5ab5cc7e687
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-an-azure-machine-learning-web-service"></a><span data-ttu-id="f4788-103">Se connecter à un service web Microsoft Azure Machine Learning | Azure</span><span class="sxs-lookup"><span data-stu-id="f4788-103">Connect to an Azure Machine Learning Web Service</span></span>
<span data-ttu-id="f4788-104">L’expérience de développeur de Microsoft Azure Machine Learning correspond à une API de service web destinée à effectuer des prédictions à partir des données d’entrée, en temps réel ou en mode de lot.</span><span class="sxs-lookup"><span data-stu-id="f4788-104">The Azure Machine Learning developer experience is a Web service API to make predictions from input data in real time or in batch mode.</span></span> <span data-ttu-id="f4788-105">Vous utilisez Microsoft Azure Machine Learning Studio pour créer des prédictions et déployer un service web Microsoft Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f4788-105">You use Azure Machine Learning Studio to create predictions and deploy an Azure Machine Learning Web service.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="f4788-106">Pour savoir comment créer et déployer un service web Machine Learning à l’aide de Machine Learning Studio, consultez les pages suivantes :</span><span class="sxs-lookup"><span data-stu-id="f4788-106">To learn about how to create and deploy a Machine Learning Web service using Machine Learning Studio:</span></span>

* <span data-ttu-id="f4788-107">Pour accéder à un didacticiel sur la création d'une expérience dans Machine Learning Studio, consultez [Créer votre première expérience](machine-learning-create-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="f4788-107">For a tutorial on how to create an experiment in Machine Learning Studio, see [Create your first experiment](machine-learning-create-experiment.md).</span></span>
* <span data-ttu-id="f4788-108">Pour plus d’informations sur le déploiement d’un service web, consultez [Déployer un service web Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="f4788-108">For details on how to deploy a Web service, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="f4788-109">Pour plus d’informations sur Machine Learning en général, consultez le [Centre de documentation Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="f4788-109">For more information about Machine Learning in general, visit the [Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

## <a name="azure-machine-learning-web-service"></a><span data-ttu-id="f4788-110">Service web Microsoft Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f4788-110">Azure Machine Learning Web service</span></span>
<span data-ttu-id="f4788-111">Grâce au service web Microsoft Azure Machine Learning, une application externe peut communiquer avec le modèle de notation de workflow Machine Learning et ce, en temps réel.</span><span class="sxs-lookup"><span data-stu-id="f4788-111">With the Azure Machine Learning Web service, an external application communicates with a Machine Learning workflow scoring model in real time.</span></span> <span data-ttu-id="f4788-112">Un appel du service web Machine Learning renvoie les résultats d’une prédiction à une application externe.</span><span class="sxs-lookup"><span data-stu-id="f4788-112">A Machine Learning Web service call returns prediction results to an external application.</span></span> <span data-ttu-id="f4788-113">Pour créer cet appel, vous transmettez une clé API créée quand vous déployez une prédiction.</span><span class="sxs-lookup"><span data-stu-id="f4788-113">To make a Machine Learning Web service call, you pass an API key that is created when you deploy a prediction.</span></span> <span data-ttu-id="f4788-114">Le service web Machine Learning est basé sur l’architecture REST, souvent choisie pour les projets de programmation web.</span><span class="sxs-lookup"><span data-stu-id="f4788-114">The Machine Learning Web service is based on REST, a popular architecture choice for web programming projects.</span></span>

<span data-ttu-id="f4788-115">Microsoft Azure Machine Learning propose deux types de service :</span><span class="sxs-lookup"><span data-stu-id="f4788-115">Azure Machine Learning has two types of services:</span></span>

* <span data-ttu-id="f4788-116">Service de requête-réponse (Request-Response Service, RRS) : service hautement évolutif, à faible latence, qui constitue une interface pour les modèles sans état créés et déployés à partir de Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="f4788-116">Request-Response Service (RRS) – A low latency, highly scalable service that provides an interface to the stateless models created and deployed from the Machine Learning Studio.</span></span>
* <span data-ttu-id="f4788-117">Service d’exécution de lot (Batch Execution Service, BES) : service asynchrone qui effectue la notation d’un lot pour les enregistrements de données.</span><span class="sxs-lookup"><span data-stu-id="f4788-117">Batch Execution Service (BES) – An asynchronous service that scores a batch for data records.</span></span>

<span data-ttu-id="f4788-118">Pour plus d’informations sur les services web Machine Learning, consultez [Déployer un service web Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="f4788-118">For more information about Machine Learning Web services, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

## <a name="get-an-azure-machine-learning-authorization-key"></a><span data-ttu-id="f4788-119">Obtenir une clé d’autorisation Microsoft Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f4788-119">Get an Azure Machine Learning authorization key</span></span>
<span data-ttu-id="f4788-120">Quand vous déployez votre expérimentation, les clés API sont générées pour le service web.</span><span class="sxs-lookup"><span data-stu-id="f4788-120">When you deploy your experiment, API keys are generated for the Web service.</span></span> <span data-ttu-id="f4788-121">Vous pouvez récupérer les clés de plusieurs emplacements.</span><span class="sxs-lookup"><span data-stu-id="f4788-121">You can retrieve the keys from several locations.</span></span>

### <a name="from-the-microsoft-azure-machine-learning-web-services-portal"></a><span data-ttu-id="f4788-122">À partir du portail des services web Microsoft Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f4788-122">From the Microsoft Azure Machine Learning Web Services portal</span></span>
<span data-ttu-id="f4788-123">Connectez-vous au [portail des services web Microsoft Azure Machine Learning](https://services.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="f4788-123">Sign in to the [Microsoft Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span>

<span data-ttu-id="f4788-124">Pour récupérer la clé API pour un nouveau service web Machine Learning :</span><span class="sxs-lookup"><span data-stu-id="f4788-124">To retrieve the API key for a New Machine Learning Web service:</span></span>

1. <span data-ttu-id="f4788-125">Dans le portail Services web Microsoft Azure Machine Learning, cliquez sur **Services web** dans le menu du haut.</span><span class="sxs-lookup"><span data-stu-id="f4788-125">In the Azure Machine Learning Web Services portal, click **Web Services** the top menu.</span></span>
2. <span data-ttu-id="f4788-126">Cliquez sur le service web pour lequel vous souhaitez récupérer la clé.</span><span class="sxs-lookup"><span data-stu-id="f4788-126">Click the Web service for which you want to retrieve the key.</span></span>
3. <span data-ttu-id="f4788-127">Cliquez sur **Consommer**dans le menu du haut.</span><span class="sxs-lookup"><span data-stu-id="f4788-127">On the top menu, click **Consume**.</span></span>
4. <span data-ttu-id="f4788-128">Copiez et enregistrez la **clé primaire**.</span><span class="sxs-lookup"><span data-stu-id="f4788-128">Copy and save the **Primary Key**.</span></span>

<span data-ttu-id="f4788-129">Pour récupérer la clé API pour un service web Machine Learning classique :</span><span class="sxs-lookup"><span data-stu-id="f4788-129">To retrieve the API key for a Classic Machine Learning Web service:</span></span>

1. <span data-ttu-id="f4788-130">Dans le portail Services web Microsoft Azure Machine Learning, cliquez sur **Services web classiques** dans le menu du haut.</span><span class="sxs-lookup"><span data-stu-id="f4788-130">In the Azure Machine Learning Web Services portal, click **Classic Web Services** the top menu.</span></span>
2. <span data-ttu-id="f4788-131">Cliquez sur le service web que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="f4788-131">Click the Web service with which you are working.</span></span>
3. <span data-ttu-id="f4788-132">Cliquez sur le point de terminaison pour lequel vous souhaitez récupérer la clé.</span><span class="sxs-lookup"><span data-stu-id="f4788-132">Click the endpoint for which you want to retrieve the key.</span></span>
4. <span data-ttu-id="f4788-133">Cliquez sur **Consommer**dans le menu du haut.</span><span class="sxs-lookup"><span data-stu-id="f4788-133">On the top menu, click **Consume**.</span></span>
5. <span data-ttu-id="f4788-134">Copiez et enregistrez la **clé primaire**.</span><span class="sxs-lookup"><span data-stu-id="f4788-134">Copy and save the **Primary Key**.</span></span>

### <a name="classic-web-service"></a><span data-ttu-id="f4788-135">Service web classique</span><span class="sxs-lookup"><span data-stu-id="f4788-135">Classic Web service</span></span>
 <span data-ttu-id="f4788-136">Vous pouvez également récupérer une clé pour un service web classique par le biais de Machine Learning Studio ou du portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="f4788-136">You can also retrieve a key for a Classic Web service from Machine Learning Studio or the Azure classic portal.</span></span>

#### <a name="machine-learning-studio"></a><span data-ttu-id="f4788-137">Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="f4788-137">Machine Learning Studio</span></span>
1. <span data-ttu-id="f4788-138">Dans Machine Learning Studio, cliquez sur l’option **SERVICES WEB** figurant sur la gauche.</span><span class="sxs-lookup"><span data-stu-id="f4788-138">In Machine Learning Studio, click **WEB SERVICES** on the left.</span></span>
2. <span data-ttu-id="f4788-139">Cliquez sur un service web.</span><span class="sxs-lookup"><span data-stu-id="f4788-139">Click a Web service.</span></span> <span data-ttu-id="f4788-140">La **clé API** figure sur l’onglet **TABLEAU DE BORD**.</span><span class="sxs-lookup"><span data-stu-id="f4788-140">The **API key** is on the **DASHBOARD** tab.</span></span>

#### <a name="azure-classic-portal"></a><span data-ttu-id="f4788-141">Portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="f4788-141">Azure classic portal</span></span>
1. <span data-ttu-id="f4788-142">Cliquez sur l’option **MACHINE LEARNING** figurant sur la gauche.</span><span class="sxs-lookup"><span data-stu-id="f4788-142">Click **MACHINE LEARNING** on the left.</span></span>
2. <span data-ttu-id="f4788-143">Cliquez sur l’espace de travail dans lequel se trouve votre service web.</span><span class="sxs-lookup"><span data-stu-id="f4788-143">Click the workspace in which your Web service is located.</span></span>
3. <span data-ttu-id="f4788-144">Cliquez sur **SERVICES WEB**.</span><span class="sxs-lookup"><span data-stu-id="f4788-144">Click **WEB SERVICES**.</span></span>
4. <span data-ttu-id="f4788-145">Cliquez sur un service web.</span><span class="sxs-lookup"><span data-stu-id="f4788-145">Click a Web service.</span></span>
5. <span data-ttu-id="f4788-146">Cliquez sur un point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="f4788-146">Click an endpoint.</span></span> <span data-ttu-id="f4788-147">La « CLÉ API » se trouve sur la partie inférieure droite de la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="f4788-147">The “API KEY” is down at the lower-right.</span></span>

## <span data-ttu-id="f4788-148"><a id="connect"></a>Se connecter à un service web Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f4788-148"><a id="connect"></a>Connect to a Machine Learning Web service</span></span>
<span data-ttu-id="f4788-149">Vous pouvez vous connecter à un service web Machine Learning à l’aide de n’importe quel langage de programmation qui prend en charge les requêtes et réponses HTTP.</span><span class="sxs-lookup"><span data-stu-id="f4788-149">You can connect to a Machine Learning Web service using any programming language that supports HTTP request and response.</span></span> <span data-ttu-id="f4788-150">Vous pouvez consulter des exemples en C#, Python et R sur l’une des pages d’aide du service web Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f4788-150">You can view examples in C#, Python, and R from a Machine Learning Web service help page.</span></span>

<span data-ttu-id="f4788-151">**Aide de l’API Machine Learning** L’aide de l’API Machine Learning est créée quand vous déployez un service web.</span><span class="sxs-lookup"><span data-stu-id="f4788-151">**Machine Learning API help** Machine Learning API help is created when you deploy a Web service.</span></span> <span data-ttu-id="f4788-152">Consultez la page [Procédure pas à pas : déploiement du service web Azure Machine Learning](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="f4788-152">See [Azure Machine Learning Walkthrough- Deploy Web Service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>
<span data-ttu-id="f4788-153">L’aide sur l’API Machine Learning contient des détails sur un service web de prédiction.</span><span class="sxs-lookup"><span data-stu-id="f4788-153">The Machine Learning API help contains details about a prediction Web service.</span></span>

1. <span data-ttu-id="f4788-154">Cliquez sur le service web que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="f4788-154">Click the Web service with which you are working.</span></span>
2. <span data-ttu-id="f4788-155">Cliquez sur le point de terminaison pour lequel vous souhaitez afficher la page d’aide de l’API.</span><span class="sxs-lookup"><span data-stu-id="f4788-155">Click the endpoint for which you want to view the API Help Page.</span></span>
3. <span data-ttu-id="f4788-156">Cliquez sur **Consommer**dans le menu du haut.</span><span class="sxs-lookup"><span data-stu-id="f4788-156">On the top menu, click **Consume**.</span></span>
4. <span data-ttu-id="f4788-157">Cliquez sur la **page d’aide de l’API** sous le point de terminaison Requête-réponse ou Exécution par lot.</span><span class="sxs-lookup"><span data-stu-id="f4788-157">Click **API help page** under either the Request-Response or Batch Execution endpoints.</span></span>

<span data-ttu-id="f4788-158">**Pour afficher l’aide de l’API Machine Learning pour un nouveau service web**</span><span class="sxs-lookup"><span data-stu-id="f4788-158">**To view Machine Learning API help for a New Web service**</span></span>

<span data-ttu-id="f4788-159">Dans le portail des services web Azure Machine Learning :</span><span class="sxs-lookup"><span data-stu-id="f4788-159">In the Azure Machine Learning Web Services Portal:</span></span>

1. <span data-ttu-id="f4788-160">Cliquez sur **SERVICES WEB** dans le menu du haut.</span><span class="sxs-lookup"><span data-stu-id="f4788-160">Click **WEB SERVICES** on the top menu.</span></span>
2. <span data-ttu-id="f4788-161">Cliquez sur le service web pour lequel vous souhaitez récupérer la clé.</span><span class="sxs-lookup"><span data-stu-id="f4788-161">Click the Web service for which you want to retrieve the key.</span></span>

<span data-ttu-id="f4788-162">Cliquez sur **Consommer** pour obtenir l’URI des services requête-réponse et d’exécution par lots et des exemples de code en C#, R et Python.</span><span class="sxs-lookup"><span data-stu-id="f4788-162">Click **Consume** to get the URIs for the Request-Reposonse and Batch Execution Services and Sample code in C#, R, and Python.</span></span>

<span data-ttu-id="f4788-163">Cliquez sur **API Swagger** pour obtenir une documentation basée sur Swagger pour les API appelées à partir de l’URI fourni.</span><span class="sxs-lookup"><span data-stu-id="f4788-163">Click **Swagger API** to get Swagger based documentation for the APIs called from the supplied URIs.</span></span>

### <a name="c-sample"></a><span data-ttu-id="f4788-164">Exemple de code C#</span><span class="sxs-lookup"><span data-stu-id="f4788-164">C# Sample</span></span>
<span data-ttu-id="f4788-165">Pour vous connecter à un service web Machine Learning, utilisez un **HttpClient** qui transmet l’élément ScoreData.</span><span class="sxs-lookup"><span data-stu-id="f4788-165">To connect to a Machine Learning Web service, use an **HttpClient** passing ScoreData.</span></span> <span data-ttu-id="f4788-166">ScoreData contient un FeatureVector, un vecteur à n dimensions des fonctionnalités numériques qui représente le ScoreData.</span><span class="sxs-lookup"><span data-stu-id="f4788-166">ScoreData contains a FeatureVector, an n-dimensional vector of numerical features that represents the ScoreData.</span></span> <span data-ttu-id="f4788-167">Vous vous authentifiez auprès du service Machine Learning au moyen d’une clé API.</span><span class="sxs-lookup"><span data-stu-id="f4788-167">You authenticate to the Machine Learning service with an API key.</span></span>

<span data-ttu-id="f4788-168">Pour vous connecter à un service web Machine Learning, le package NuGet **Microsoft.AspNet.WebApi.Client** doit être installé.</span><span class="sxs-lookup"><span data-stu-id="f4788-168">To connect to a Machine Learning Web service, the **Microsoft.AspNet.WebApi.Client** NuGet package must be installed.</span></span>

<span data-ttu-id="f4788-169">**Installer le package NuGet Microsoft.AspNet.WebApi.Client dans Microsoft Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="f4788-169">**Install Microsoft.AspNet.WebApi.Client NuGet in Visual Studio**</span></span>

1. <span data-ttu-id="f4788-170">Publiez le service web « Téléchargement d’un jeu de données depuis l’UCI : jeu de données de classe Adult 2 ».</span><span class="sxs-lookup"><span data-stu-id="f4788-170">Publish the Download dataset from UCI: Adult 2 class dataset Web Service.</span></span>
2. <span data-ttu-id="f4788-171">Cliquez sur **Outils** > **Gestionnaire de package NuGet** > **Console du gestionnaire de package**.</span><span class="sxs-lookup"><span data-stu-id="f4788-171">Click **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
3. <span data-ttu-id="f4788-172">Choisissez l'élément **Install-Package Microsoft.AspNet.WebApi.Client**.</span><span class="sxs-lookup"><span data-stu-id="f4788-172">Choose **Install-Package Microsoft.AspNet.WebApi.Client**.</span></span>

<span data-ttu-id="f4788-173">**Pour exécuter l’exemple de code**</span><span class="sxs-lookup"><span data-stu-id="f4788-173">**To run the code sample**</span></span>

1. <span data-ttu-id="f4788-174">Publiez l’expérience « Exemple 1 : Téléchargement d’un jeu de données depuis l’UCI : jeu de données de classe Adult 2 », inclus dans la collection d’exemples Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f4788-174">Publish "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of the Machine Learning sample collection.</span></span>
2. <span data-ttu-id="f4788-175">Attribuez l’élément apiKey avec la clé à partir d’un service web.</span><span class="sxs-lookup"><span data-stu-id="f4788-175">Assign apiKey with the key from a Web service.</span></span> <span data-ttu-id="f4788-176">Consultez **Obtenir une clé d’autorisation Microsoft Azure Machine Learning** plus haut.</span><span class="sxs-lookup"><span data-stu-id="f4788-176">See **Get an Azure Machine Learning authorization key** above.</span></span>
3. <span data-ttu-id="f4788-177">Affectez l’élément serviceUri avec l’URI de requête.</span><span class="sxs-lookup"><span data-stu-id="f4788-177">Assign serviceUri with the Request URI.</span></span>

### <a name="python-sample"></a><span data-ttu-id="f4788-178">Exemple de code Python</span><span class="sxs-lookup"><span data-stu-id="f4788-178">Python Sample</span></span>
<span data-ttu-id="f4788-179">Pour vous connecter à un service web Machine Learning, utilisez la bibliothèque **urllib2** qui transmet l’élément ScoreData.</span><span class="sxs-lookup"><span data-stu-id="f4788-179">To connect to a Machine Learning Web service, use the **urllib2** library passing ScoreData.</span></span> <span data-ttu-id="f4788-180">ScoreData contient un FeatureVector, vecteur à n dimensions des fonctionnalités numériques qui représente le ScoreData.</span><span class="sxs-lookup"><span data-stu-id="f4788-180">ScoreData contains a FeatureVector, an n-dimensional  vector of numerical features that represents the ScoreData.</span></span> <span data-ttu-id="f4788-181">Vous vous authentifiez auprès du service Machine Learning au moyen d’une clé API.</span><span class="sxs-lookup"><span data-stu-id="f4788-181">You authenticate to the Machine Learning service with an API key.</span></span>

<span data-ttu-id="f4788-182">**Pour exécuter l’exemple de code**</span><span class="sxs-lookup"><span data-stu-id="f4788-182">**To run the code sample**</span></span>

1. <span data-ttu-id="f4788-183">Déployez l’expérience « Exemple 1 : Téléchargement d’un jeu de données depuis l’UCI : jeu de données de classe Adult 2 », inclus dans la collection d’exemples Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="f4788-183">Deploy "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of the Machine Learning sample collection.</span></span>
2. <span data-ttu-id="f4788-184">Attribuez l’élément apiKey avec la clé à partir d’un service web.</span><span class="sxs-lookup"><span data-stu-id="f4788-184">Assign apiKey with the key from a Web service.</span></span> <span data-ttu-id="f4788-185">Consultez la section **Obtenir une clé d’autorisation Microsoft Azure Machine Learning** au début de cet article.</span><span class="sxs-lookup"><span data-stu-id="f4788-185">See the **Get an Azure Machine Learning authorization key** section near the beginning of this article.</span></span>
3. <span data-ttu-id="f4788-186">Affectez l’élément serviceUri avec l’URI de requête.</span><span class="sxs-lookup"><span data-stu-id="f4788-186">Assign serviceUri with the Request URI.</span></span>

