---
title: aaaConnect tooa Service Web de Machine Learning | Documents Microsoft
description: "Avec c# ou Python, vous connecter tooan service Azure Machine Learning Web à l’aide d’une clé d’autorisation."
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
redirect_document_id: True
ms.openlocfilehash: 0108e71e30a05539a8c0ee93d5aadb07e3d1efa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-azure-machine-learning-web-service"></a><span data-ttu-id="5f3e8-103">Se connecter tooan Service Web de Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5f3e8-103">Connect tooan Azure Machine Learning Web Service</span></span>
<span data-ttu-id="5f3e8-104">Hello expérience des développeurs Azure Machine Learning est un Web service API toomake des prévisions à partir des données d’entrée en temps réel ou en mode batch.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-104">hello Azure Machine Learning developer experience is a Web service API toomake predictions from input data in real time or in batch mode.</span></span> <span data-ttu-id="5f3e8-105">Vous utilisez des prédictions de toocreate Azure Machine Learning Studio et déployez un service Web de Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-105">You use Azure Machine Learning Studio toocreate predictions and deploy an Azure Machine Learning Web service.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="5f3e8-106">toolearn comment toocreate et déployer un service Web d’apprentissage Machine à l’aide de la Machine Learning Studio :</span><span class="sxs-lookup"><span data-stu-id="5f3e8-106">toolearn about how toocreate and deploy a Machine Learning Web service using Machine Learning Studio:</span></span>

* <span data-ttu-id="5f3e8-107">Pour un didacticiel sur toocreate une expérience dans Machine Learning Studio, voir [créer votre première expérience](machine-learning-create-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="5f3e8-107">For a tutorial on how toocreate an experiment in Machine Learning Studio, see [Create your first experiment](machine-learning-create-experiment.md).</span></span>
* <span data-ttu-id="5f3e8-108">Pour plus d’informations sur la façon de toodeploy un service Web, consultez [déployer un service Web d’apprentissage Machine](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="5f3e8-108">For details on how toodeploy a Web service, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="5f3e8-109">Pour plus d’informations sur la Machine Learning en général, visitez hello [centre de Documentation Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="5f3e8-109">For more information about Machine Learning in general, visit hello [Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

## <a name="azure-machine-learning-web-service"></a><span data-ttu-id="5f3e8-110">Service web Microsoft Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5f3e8-110">Azure Machine Learning Web service</span></span>
<span data-ttu-id="5f3e8-111">Avec hello service Azure Machine Learning Web, une application externe communique avec un modèle de score de flux de travail Machine Learning en temps réel.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-111">With hello Azure Machine Learning Web service, an external application communicates with a Machine Learning workflow scoring model in real time.</span></span> <span data-ttu-id="5f3e8-112">Un appel de service Web d’apprentissage Machine retourne des résultats de prédiction tooan des applications externes.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-112">A Machine Learning Web service call returns prediction results tooan external application.</span></span> <span data-ttu-id="5f3e8-113">toomake un appel de service Web de la Machine Learning, vous passez une clé d’API qui est créée lorsque vous déployez une prédiction.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-113">toomake a Machine Learning Web service call, you pass an API key that is created when you deploy a prediction.</span></span> <span data-ttu-id="5f3e8-114">Hello service Web d’apprentissage Machine est basée sur REST, un choix d’architecture courante pour les projets de programmation web.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-114">hello Machine Learning Web service is based on REST, a popular architecture choice for web programming projects.</span></span>

<span data-ttu-id="5f3e8-115">Microsoft Azure Machine Learning propose deux types de service :</span><span class="sxs-lookup"><span data-stu-id="5f3e8-115">Azure Machine Learning has two types of services:</span></span>

* <span data-ttu-id="5f3e8-116">Le Service de requête-réponse (RR) – une faible latence, un service hautement évolutif qui fournit une interface toohello des modèles sans état créés et déployés à partir de hello Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-116">Request-Response Service (RRS) – A low latency, highly scalable service that provides an interface toohello stateless models created and deployed from hello Machine Learning Studio.</span></span>
* <span data-ttu-id="5f3e8-117">Service d’exécution de lot (Batch Execution Service, BES) : service asynchrone qui effectue la notation d’un lot pour les enregistrements de données.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-117">Batch Execution Service (BES) – An asynchronous service that scores a batch for data records.</span></span>

<span data-ttu-id="5f3e8-118">Pour plus d’informations sur les services web Machine Learning, consultez [Déployer un service web Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="5f3e8-118">For more information about Machine Learning Web services, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

## <a name="get-an-azure-machine-learning-authorization-key"></a><span data-ttu-id="5f3e8-119">Obtenir une clé d’autorisation Microsoft Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5f3e8-119">Get an Azure Machine Learning authorization key</span></span>
<span data-ttu-id="5f3e8-120">Lorsque vous déployez votre expérience, les clés API sont générées pour hello service Web.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-120">When you deploy your experiment, API keys are generated for hello Web service.</span></span> <span data-ttu-id="5f3e8-121">Vous pouvez récupérer les clés de hello depuis plusieurs emplacements.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-121">You can retrieve hello keys from several locations.</span></span>

### <a name="from-hello-microsoft-azure-machine-learning-web-services-portal"></a><span data-ttu-id="5f3e8-122">À partir du portail de Services Web de Microsoft Azure Machine Learning hello</span><span class="sxs-lookup"><span data-stu-id="5f3e8-122">From hello Microsoft Azure Machine Learning Web Services portal</span></span>
<span data-ttu-id="5f3e8-123">Connectez-vous à toohello [les Services Web de Microsoft Azure Machine Learning](https://services.azureml.net) portal.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-123">Sign in toohello [Microsoft Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span>

<span data-ttu-id="5f3e8-124">clé de hello API tooretrieve pour un service d’un site Web Machine Learning :</span><span class="sxs-lookup"><span data-stu-id="5f3e8-124">tooretrieve hello API key for a New Machine Learning Web service:</span></span>

1. <span data-ttu-id="5f3e8-125">Dans le portail de Services Web de Azure Machine Learning hello, cliquez sur **Services Web** menu du haut hello.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-125">In hello Azure Machine Learning Web Services portal, click **Web Services** hello top menu.</span></span>
2. <span data-ttu-id="5f3e8-126">Cliquez sur le service Web de hello pour lequel vous voulez tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-126">Click hello Web service for which you want tooretrieve hello key.</span></span>
3. <span data-ttu-id="5f3e8-127">Dans le menu supérieur de hello, cliquez sur **consommer**.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-127">On hello top menu, click **Consume**.</span></span>
4. <span data-ttu-id="5f3e8-128">Copiez et enregistrez hello **clé primaire**.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-128">Copy and save hello **Primary Key**.</span></span>

<span data-ttu-id="5f3e8-129">clé de hello API tooretrieve pour un service Web d’apprentissage Machine classique :</span><span class="sxs-lookup"><span data-stu-id="5f3e8-129">tooretrieve hello API key for a Classic Machine Learning Web service:</span></span>

1. <span data-ttu-id="5f3e8-130">Dans le portail de Services Web de Azure Machine Learning hello, cliquez sur **des Services Web classique** menu du haut hello.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-130">In hello Azure Machine Learning Web Services portal, click **Classic Web Services** hello top menu.</span></span>
2. <span data-ttu-id="5f3e8-131">Cliquez sur le service Web de hello avec lequel vous travaillez.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-131">Click hello Web service with which you are working.</span></span>
3. <span data-ttu-id="5f3e8-132">Cliquez sur le point de terminaison hello pour lequel vous voulez tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-132">Click hello endpoint for which you want tooretrieve hello key.</span></span>
4. <span data-ttu-id="5f3e8-133">Dans le menu supérieur de hello, cliquez sur **consommer**.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-133">On hello top menu, click **Consume**.</span></span>
5. <span data-ttu-id="5f3e8-134">Copiez et enregistrez hello **clé primaire**.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-134">Copy and save hello **Primary Key**.</span></span>

### <a name="classic-web-service"></a><span data-ttu-id="5f3e8-135">Service web classique</span><span class="sxs-lookup"><span data-stu-id="5f3e8-135">Classic Web service</span></span>
 <span data-ttu-id="5f3e8-136">Vous pouvez également récupérer une clé pour un service Web classique à partir de la Machine Learning Studio ou hello portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-136">You can also retrieve a key for a Classic Web service from Machine Learning Studio or hello Azure classic portal.</span></span>

#### <a name="machine-learning-studio"></a><span data-ttu-id="5f3e8-137">Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="5f3e8-137">Machine Learning Studio</span></span>
1. <span data-ttu-id="5f3e8-138">Dans la Machine Learning Studio, cliquez sur **SERVICES WEB** sur hello gauche.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-138">In Machine Learning Studio, click **WEB SERVICES** on hello left.</span></span>
2. <span data-ttu-id="5f3e8-139">Cliquez sur un service web.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-139">Click a Web service.</span></span> <span data-ttu-id="5f3e8-140">Hello **clé API** sur hello **tableau de bord** onglet.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-140">hello **API key** is on hello **DASHBOARD** tab.</span></span>

#### <a name="azure-classic-portal"></a><span data-ttu-id="5f3e8-141">Portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="5f3e8-141">Azure classic portal</span></span>
1. <span data-ttu-id="5f3e8-142">Cliquez sur **MACHINE LEARNING** sur hello gauche.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-142">Click **MACHINE LEARNING** on hello left.</span></span>
2. <span data-ttu-id="5f3e8-143">Cliquez sur espace hello dans lequel se trouve votre service Web.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-143">Click hello workspace in which your Web service is located.</span></span>
3. <span data-ttu-id="5f3e8-144">Cliquez sur **SERVICES WEB**.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-144">Click **WEB SERVICES**.</span></span>
4. <span data-ttu-id="5f3e8-145">Cliquez sur un service web.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-145">Click a Web service.</span></span>
5. <span data-ttu-id="5f3e8-146">Cliquez sur un point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-146">Click an endpoint.</span></span> <span data-ttu-id="5f3e8-147">Hello « Clé API » s’est arrêté à hello inférieur droit.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-147">hello “API KEY” is down at hello lower-right.</span></span>

## <span data-ttu-id="5f3e8-148"><a id="connect"></a>Connecter tooa Machine Learning Web service</span><span class="sxs-lookup"><span data-stu-id="5f3e8-148"><a id="connect"></a>Connect tooa Machine Learning Web service</span></span>
<span data-ttu-id="5f3e8-149">Vous pouvez vous connecter tooa service Web d’apprentissage Machine à l’aide de n’importe quel langage de programmation qui prend en charge de la réponse et requête HTTP.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-149">You can connect tooa Machine Learning Web service using any programming language that supports HTTP request and response.</span></span> <span data-ttu-id="5f3e8-150">Vous pouvez consulter des exemples en C#, Python et R sur l’une des pages d’aide du service web Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-150">You can view examples in C#, Python, and R from a Machine Learning Web service help page.</span></span>

<span data-ttu-id="5f3e8-151">**Aide de l’API Machine Learning** L’aide de l’API Machine Learning est créée quand vous déployez un service web.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-151">**Machine Learning API help** Machine Learning API help is created when you deploy a Web service.</span></span> <span data-ttu-id="5f3e8-152">Consultez la page [Procédure pas à pas : déploiement du service web Azure Machine Learning](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="5f3e8-152">See [Azure Machine Learning Walkthrough- Deploy Web Service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>
<span data-ttu-id="5f3e8-153">Hello aide des API d’apprentissage Machine contient des détails sur une service Web de prédiction.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-153">hello Machine Learning API help contains details about a prediction Web service.</span></span>

1. <span data-ttu-id="5f3e8-154">Cliquez sur le service Web de hello avec lequel vous travaillez.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-154">Click hello Web service with which you are working.</span></span>
2. <span data-ttu-id="5f3e8-155">Cliquez sur le point de terminaison hello pour lequel vous souhaitez tooview hello Page d’aide API.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-155">Click hello endpoint for which you want tooview hello API Help Page.</span></span>
3. <span data-ttu-id="5f3e8-156">Dans le menu supérieur de hello, cliquez sur **consommer**.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-156">On hello top menu, click **Consume**.</span></span>
4. <span data-ttu-id="5f3e8-157">Cliquez sur **page d’aide API** sous hello demande-réponse ou de points de terminaison de l’exécution par lots.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-157">Click **API help page** under either hello Request-Response or Batch Execution endpoints.</span></span>

<span data-ttu-id="5f3e8-158">**aide de Machine Learning API tooview pour un service d’un site Web**</span><span class="sxs-lookup"><span data-stu-id="5f3e8-158">**tooview Machine Learning API help for a New Web service**</span></span>

<span data-ttu-id="5f3e8-159">Bonjour portail de Services Web Azure Machine Learning :</span><span class="sxs-lookup"><span data-stu-id="5f3e8-159">In hello Azure Machine Learning Web Services Portal:</span></span>

1. <span data-ttu-id="5f3e8-160">Cliquez sur **SERVICES WEB** sur le menu du haut hello.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-160">Click **WEB SERVICES** on hello top menu.</span></span>
2. <span data-ttu-id="5f3e8-161">Cliquez sur le service Web de hello pour lequel vous voulez tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-161">Click hello Web service for which you want tooretrieve hello key.</span></span>

<span data-ttu-id="5f3e8-162">Cliquez sur **consommer** tooget hello URI pour hello Reposonse de demande et de Services d’exécution de lot exemple de code en c#, R et Python.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-162">Click **Consume** tooget hello URIs for hello Request-Reposonse and Batch Execution Services and Sample code in C#, R, and Python.</span></span>

<span data-ttu-id="5f3e8-163">Cliquez sur **API de Swagger** tooget Swagger en fonction de documentation pour hello API appelée à partir de hello fourni URI.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-163">Click **Swagger API** tooget Swagger based documentation for hello APIs called from hello supplied URIs.</span></span>

### <a name="c-sample"></a><span data-ttu-id="5f3e8-164">Exemple de code C#</span><span class="sxs-lookup"><span data-stu-id="5f3e8-164">C# Sample</span></span>
<span data-ttu-id="5f3e8-165">tooconnect tooa service Machine Learning Web, utilisez un **HttpClient** passage ScoreData.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-165">tooconnect tooa Machine Learning Web service, use an **HttpClient** passing ScoreData.</span></span> <span data-ttu-id="5f3e8-166">ScoreData contient un FeatureVector, un vecteur de fonctionnalités numériques à n dimensions représente hello ScoreData.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-166">ScoreData contains a FeatureVector, an n-dimensional vector of numerical features that represents hello ScoreData.</span></span> <span data-ttu-id="5f3e8-167">Vous authentifier le service de Machine Learning toohello avec une clé d’API.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-167">You authenticate toohello Machine Learning service with an API key.</span></span>

<span data-ttu-id="5f3e8-168">tooconnect tooa service Web d’apprentissage Machine, hello **Microsoft.AspNet.WebApi.Client** le package NuGet doit être installé.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-168">tooconnect tooa Machine Learning Web service, hello **Microsoft.AspNet.WebApi.Client** NuGet package must be installed.</span></span>

<span data-ttu-id="5f3e8-169">**Installer le package NuGet Microsoft.AspNet.WebApi.Client dans Microsoft Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="5f3e8-169">**Install Microsoft.AspNet.WebApi.Client NuGet in Visual Studio**</span></span>

1. <span data-ttu-id="5f3e8-170">Publier le dataset téléchargement hello UCI : 2 adulte classe dataset Service Web.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-170">Publish hello Download dataset from UCI: Adult 2 class dataset Web Service.</span></span>
2. <span data-ttu-id="5f3e8-171">Cliquez sur **Outils** > **Gestionnaire de package NuGet** > **Console du gestionnaire de package**.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-171">Click **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
3. <span data-ttu-id="5f3e8-172">Choisissez l'élément **Install-Package Microsoft.AspNet.WebApi.Client**.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-172">Choose **Install-Package Microsoft.AspNet.WebApi.Client**.</span></span>

<span data-ttu-id="5f3e8-173">**exemple de code hello toorun**</span><span class="sxs-lookup"><span data-stu-id="5f3e8-173">**toorun hello code sample**</span></span>

1. <span data-ttu-id="5f3e8-174">Publier « exemple 1 : télécharger le jeu de données à partir de UCI : adulte 2 classe dataset « expérience, de la part de hello, exemple de collection de Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-174">Publish "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of hello Machine Learning sample collection.</span></span>
2. <span data-ttu-id="5f3e8-175">Affecter apiKey avec la clé de hello à partir d’un service Web.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-175">Assign apiKey with hello key from a Web service.</span></span> <span data-ttu-id="5f3e8-176">Consultez **Obtenir une clé d’autorisation Microsoft Azure Machine Learning** plus haut.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-176">See **Get an Azure Machine Learning authorization key** above.</span></span>
3. <span data-ttu-id="5f3e8-177">Affecter serviceUri avec hello URI de requête.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-177">Assign serviceUri with hello Request URI.</span></span>

### <a name="python-sample"></a><span data-ttu-id="5f3e8-178">Exemple de code Python</span><span class="sxs-lookup"><span data-stu-id="5f3e8-178">Python Sample</span></span>
<span data-ttu-id="5f3e8-179">tooconnect tooa service Machine Learning Web, utilisez hello **urllib2** ScoreData de passage de bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-179">tooconnect tooa Machine Learning Web service, use hello **urllib2** library passing ScoreData.</span></span> <span data-ttu-id="5f3e8-180">ScoreData contient un FeatureVector, un vecteur de fonctionnalités numériques à n dimensions représente hello ScoreData.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-180">ScoreData contains a FeatureVector, an n-dimensional  vector of numerical features that represents hello ScoreData.</span></span> <span data-ttu-id="5f3e8-181">Vous authentifier le service de Machine Learning toohello avec une clé d’API.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-181">You authenticate toohello Machine Learning service with an API key.</span></span>

<span data-ttu-id="5f3e8-182">**exemple de code hello toorun**</span><span class="sxs-lookup"><span data-stu-id="5f3e8-182">**toorun hello code sample**</span></span>

1. <span data-ttu-id="5f3e8-183">Déployer « exemple 1 : télécharger le jeu de données à partir de UCI : adulte 2 classe dataset « expérience, de la part de hello, exemple de collection de Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-183">Deploy "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of hello Machine Learning sample collection.</span></span>
2. <span data-ttu-id="5f3e8-184">Affecter apiKey avec la clé de hello à partir d’un service Web.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-184">Assign apiKey with hello key from a Web service.</span></span> <span data-ttu-id="5f3e8-185">Consultez hello **obtenir une clé d’autorisation d’Azure Machine Learning** section près de début de hello de cet article.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-185">See hello **Get an Azure Machine Learning authorization key** section near hello beginning of this article.</span></span>
3. <span data-ttu-id="5f3e8-186">Affecter serviceUri avec hello URI de requête.</span><span class="sxs-lookup"><span data-stu-id="5f3e8-186">Assign serviceUri with hello Request URI.</span></span>

