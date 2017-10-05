---
title: "Utilisation d’un service web Machine Learning à l’aide d’un modèle d’application web | Microsoft Docs"
description: "Utilisez un modèle d’application Web dans Azure Marketplace pour exploiter un service Web prédictif dans Azure Machine Learning."
keywords: "service Web, opérationnalisation, API REST, apprentissage automatique"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: e0d71683-61b9-4675-8df5-09ddc2f0d92d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye;raymondl
ms.openlocfilehash: 95aa1fa23d83ec0dcd00870179167e803bafbd16
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="consume-an-azure-machine-learning-web-service-with-a-web-app-template"></a><span data-ttu-id="3829d-104">Utilisation d’un service Web Microsoft Azure Machine Learning à l’aide d’un modèle d’application Web</span><span class="sxs-lookup"><span data-stu-id="3829d-104">Consume an Azure Machine Learning web service with a web app template</span></span>

<span data-ttu-id="3829d-105">Une fois vous avez développé votre modèle de prévision et l’avez déployé en tant que service web Azure à l’aide de Machine Learning Studio ou à l’aide d’outils comme R ou Python, vous pouvez accéder au modèle opérationnalisé à l’aide d’une API REST.</span><span class="sxs-lookup"><span data-stu-id="3829d-105">Once you've developed your predictive model and deployed it as an Azure web service using Machine Learning Studio, or using tools such as R or Python, you can access the operationalized model using a REST API.</span></span>

<span data-ttu-id="3829d-106">Il existe plusieurs moyens d’utiliser l’API REST et d’accéder au service Web.</span><span class="sxs-lookup"><span data-stu-id="3829d-106">There are a number of ways to consume the REST API and access the web service.</span></span> <span data-ttu-id="3829d-107">Vous pouvez par exemple écrire une application en C#, R ou Python à l’aide de l’exemple de code généré lors du déploiement du service web (disponible dans le [portail des services web Machine Learning](https://services.azureml.net/quickstart) ou dans Machine Learning Studio, dans le tableau de bord du service web).</span><span class="sxs-lookup"><span data-stu-id="3829d-107">For example, you can write an application in C#, R, or Python using the sample code generated for you when you deployed the web service (available in the [Machine Learning Web Services Portal](https://services.azureml.net/quickstart) or in the web service dashboard in Machine Learning Studio).</span></span> <span data-ttu-id="3829d-108">Vous pouvez également utiliser l’exemple de classeur Microsoft Excel créé en même temps.</span><span class="sxs-lookup"><span data-stu-id="3829d-108">Or you can use the sample Microsoft Excel workbook created for you at the same time.</span></span>

<span data-ttu-id="3829d-109">Mais le moyen le plus rapide et le plus simple d’accéder à votre service web consiste à utiliser les modèles d’application web disponibles dans [Azure Web App Marketplace](https://azure.microsoft.com/marketplace/web-applications/all/).</span><span class="sxs-lookup"><span data-stu-id="3829d-109">But the quickest and easiest way to access your web service is through the Web App Templates available in the [Azure Web App Marketplace](https://azure.microsoft.com/marketplace/web-applications/all/).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="the-azure-machine-learning-web-app-templates"></a><span data-ttu-id="3829d-110">Modèles d’applications Web de Microsoft Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="3829d-110">The Azure Machine Learning Web App Templates</span></span>
<span data-ttu-id="3829d-111">Les modèles d’applications Web disponibles dans Azure Marketplace peuvent générer une application Web personnalisée qui connaît les données d’entrée et les résultats attendus de votre service Web.</span><span class="sxs-lookup"><span data-stu-id="3829d-111">The web app templates available in the Azure Marketplace can build a custom web app that knows your web service's input data and expected results.</span></span> <span data-ttu-id="3829d-112">Il vous suffit de donner à l’application Web l’accès à votre service Web et aux données associées, et le modèle fait le reste.</span><span class="sxs-lookup"><span data-stu-id="3829d-112">All you need to do is give the web app access to your web service and data, and the template does the rest.</span></span>

<span data-ttu-id="3829d-113">Il existe deux modèles :</span><span class="sxs-lookup"><span data-stu-id="3829d-113">Two templates are available:</span></span>

* [<span data-ttu-id="3829d-114">Modèle d’application Web Azure ML Request-Response Service</span><span class="sxs-lookup"><span data-stu-id="3829d-114">Azure ML Request-Response Service Web App Template</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/)
* [<span data-ttu-id="3829d-115">Modèle d’application Web Azure ML Batch Execution Service</span><span class="sxs-lookup"><span data-stu-id="3829d-115">Azure ML Batch Execution Service Web App Template</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/)

<span data-ttu-id="3829d-116">Chaque modèle crée un exemple d’application ASP.NET, en utilisant l’URI et la clé de l’API correspondant à votre service Web, et le déploie en tant que site Web dans Azure.</span><span class="sxs-lookup"><span data-stu-id="3829d-116">Each template creates a sample ASP.NET application, using the API URI and Key for your web service, and deploys it as a web site to Azure.</span></span> <span data-ttu-id="3829d-117">Le modèle Request-Response (RRS) crée une application Web qui vous permet d’envoyer une seule ligne de données au service Web afin d’obtenir un résultat unique.</span><span class="sxs-lookup"><span data-stu-id="3829d-117">The Request-Response Service (RRS) template creates a web app that allows you to send a single row of data to the web service to get a single result.</span></span> <span data-ttu-id="3829d-118">Le modèle Batch Execution Service (BES) crée une application Web qui vous permet d’envoyer un grand nombre de lignes de données de manière à obtenir plusieurs résultats.</span><span class="sxs-lookup"><span data-stu-id="3829d-118">The Batch Execution Service (BES) template creates a web app that allows you to send many rows of data to get multiple results.</span></span>

<span data-ttu-id="3829d-119">Aucun code n’est nécessaire pour utiliser ces modèles.</span><span class="sxs-lookup"><span data-stu-id="3829d-119">No coding is required to use these templates.</span></span> <span data-ttu-id="3829d-120">Vous devez simplement spécifier la clé API et l’URI pour permettre au modèle de générer automatiquement l’application.</span><span class="sxs-lookup"><span data-stu-id="3829d-120">You just supply the API Key and URI, and the template builds the application for you.</span></span>

<span data-ttu-id="3829d-121">Pour obtenir la clé API et l’URI de requête pour un service web :</span><span class="sxs-lookup"><span data-stu-id="3829d-121">To get the API key and Request URI for a web service:</span></span>

1. <span data-ttu-id="3829d-122">Dans le [portail de services web](https://services.azureml.net/quickstart), pour un nouveau service web, cliquez sur **Services web** en haut.</span><span class="sxs-lookup"><span data-stu-id="3829d-122">In the [Web Services Portal](https://services.azureml.net/quickstart), for a New web service, click **Web Services** at the top.</span></span> <span data-ttu-id="3829d-123">Pour un service web classique, cliquez sur **Services web classiques**.</span><span class="sxs-lookup"><span data-stu-id="3829d-123">Or for a Classic web service click **Classic Web Services**.</span></span>
2. <span data-ttu-id="3829d-124">Cliquez sur le service web auquel vous souhaitez accéder.</span><span class="sxs-lookup"><span data-stu-id="3829d-124">Click the web service you want to access.</span></span>
3. <span data-ttu-id="3829d-125">Pour un service web classique, cliquez sur le point de terminaison auquel vous souhaitez accéder.</span><span class="sxs-lookup"><span data-stu-id="3829d-125">For a Classic web service, click the endpoint you want to access.</span></span>
4. <span data-ttu-id="3829d-126">Cliquez sur **Utiliser** en haut.</span><span class="sxs-lookup"><span data-stu-id="3829d-126">Click **Consume** at the top.</span></span>
5. <span data-ttu-id="3829d-127">Copiez la clé **primaire** ou **secondaire** et enregistrez-la.</span><span class="sxs-lookup"><span data-stu-id="3829d-127">Copy the **Primary** or **Secondary Key** and save it.</span></span>
6. <span data-ttu-id="3829d-128">Si vous créez un modèle de service de requête-réponse (RRS, Request-Response Service), copiez l’URI de la **requête-réponse** et enregistrez-le.</span><span class="sxs-lookup"><span data-stu-id="3829d-128">If you're creating a Request-Response Service (RRS) template, copy the **Request-Response** URI and save it.</span></span> <span data-ttu-id="3829d-129">Si vous créez un modèle de service d’exécution de lot (BES, Batch Execution Service), copiez l’URI des **requêtes de lots** et enregistrez-le.</span><span class="sxs-lookup"><span data-stu-id="3829d-129">If you're creating a Batch Execution Service (BES) template, copy the **Batch Requests** URI and save it.</span></span>


## <a name="how-to-use-the-request-response-service-rrs-template"></a><span data-ttu-id="3829d-130">Comment utiliser le modèle Request-Response Service (RRS)</span><span class="sxs-lookup"><span data-stu-id="3829d-130">How to use the Request-Response Service (RRS) template</span></span>
<span data-ttu-id="3829d-131">Procédez comme suit pour utiliser le modèle d’application web RRS (voir schéma ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="3829d-131">Follow these steps to use the RRS web app template, as shown in the following diagram.</span></span>

![Procédure d’utilisation du modèle Web RSS][image1]


<!--    ![API Key][image3] -->

<!-- This value will look like this:
   
        https://ussouthcentral.services.azureml.net/workspaces/<workspace-id>/services/<service-id>/execute?api-version=2.0&details=true
   
    ![Request URI][image4] -->

1. <span data-ttu-id="3829d-133">Accédez au [Portail Azure](https://portal.azure.com), **Connexion**, cliquez sur **Nouveau**, recherchez et sélectionnez **Azure ML Request-Response Service Web App**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="3829d-133">Go to the [Azure portal](https://portal.azure.com), **Login**, click **New**, search for and select **Azure ML Request-Response Service Web App**, then click **Create**.</span></span> 
   
   * <span data-ttu-id="3829d-134">Donnez un nom unique à votre application Web.</span><span class="sxs-lookup"><span data-stu-id="3829d-134">Give your web app a unique name.</span></span> <span data-ttu-id="3829d-135">L’URL de l’application web sera ce nom suivi de `.azurewebsites.net.` Par exemple, `http://carprediction.azurewebsites.net.`</span><span class="sxs-lookup"><span data-stu-id="3829d-135">The URL of the web app will be this name followed by `.azurewebsites.net.` For example, `http://carprediction.azurewebsites.net.`</span></span>
   * <span data-ttu-id="3829d-136">Sélectionnez l’abonnement Azure et les services sous lesquels est exécuté votre service Web.</span><span class="sxs-lookup"><span data-stu-id="3829d-136">Select the Azure subscription and services under which your web service is running.</span></span>
   * <span data-ttu-id="3829d-137">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="3829d-137">Click **Create**.</span></span>
     
     ![Créer une application web][image5]

4. <span data-ttu-id="3829d-139">Une fois le déploiement de l’application web terminé, cliquez sur l’ **URL** sur la page des paramètres de l’application web dans Azure, ou entrez l’URL dans un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="3829d-139">When Azure has finished deploying the web app, click the **URL** on the web app settings page in Azure, or enter the URL in a web browser.</span></span> <span data-ttu-id="3829d-140">Par exemple, `http://carprediction.azurewebsites.net.`</span><span class="sxs-lookup"><span data-stu-id="3829d-140">For example, `http://carprediction.azurewebsites.net.`</span></span>
5. <span data-ttu-id="3829d-141">À la première exécution de l’application web, vous êtes invité à renseigner **l’URL de publication de l’API** et la **clé API**.</span><span class="sxs-lookup"><span data-stu-id="3829d-141">When the web app first runs it will ask you for the **API Post URL** and **API Key**.</span></span>
   <span data-ttu-id="3829d-142">Entrez les valeurs que vous avez enregistrées précédemment (**URI de requête** et **Clé API** respectivement).</span><span class="sxs-lookup"><span data-stu-id="3829d-142">Enter the values you saved earlier (**Request URI** and **API Key**, respectively).</span></span>
     
     <span data-ttu-id="3829d-143">Cliquez sur **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="3829d-143">Click **Submit**.</span></span>
     
     ![Entrer l’URI de publication et la clé de l’API][image6]

6. <span data-ttu-id="3829d-145">L’application web affiche la page **Configuration de l’application web** avec les paramètres du service web actif.</span><span class="sxs-lookup"><span data-stu-id="3829d-145">The web app displays its **Web App Configuration** page with the current web service settings.</span></span> <span data-ttu-id="3829d-146">Vous pouvez ici modifier les paramètres utilisés par l’application Web.</span><span class="sxs-lookup"><span data-stu-id="3829d-146">Here you can make changes to the settings used by the web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="3829d-147">Une modification des paramètres à ce stade n’affecte que l’application Web concernée.</span><span class="sxs-lookup"><span data-stu-id="3829d-147">Changing the settings here only changes them for this web app.</span></span> <span data-ttu-id="3829d-148">Les paramètres par défaut de votre service Web ne seront pas modifiés.</span><span class="sxs-lookup"><span data-stu-id="3829d-148">It doesn't change the default settings of your web service.</span></span> <span data-ttu-id="3829d-149">Par exemple, si vous modifiez ici la **Description** , l’opération n’aura aucun effet sur la description affichée sur le tableau de bord du service web dans Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="3829d-149">For example, if you change the **Description** here it doesn't change the description shown on the web service dashboard in Machine Learning Studio.</span></span>
   > 
   > 
   
    <span data-ttu-id="3829d-150">Quand vous avez terminé, cliquez sur **Enregistrer les modifications**, puis cliquez sur **Atteindre la page de démarrage**.</span><span class="sxs-lookup"><span data-stu-id="3829d-150">When you're done, click **Save changes**, and then click **Go to Home Page**.</span></span>

7. <span data-ttu-id="3829d-151">Vous pouvez entrer les valeurs à envoyer à votre service web dans la page d’accueil.</span><span class="sxs-lookup"><span data-stu-id="3829d-151">From the home page you can enter values to send to your web service.</span></span> <span data-ttu-id="3829d-152">Cliquez sur **Envoyer** lorsque vous avez terminé. Le résultat est renvoyé.</span><span class="sxs-lookup"><span data-stu-id="3829d-152">Click **Submit** when you're done, and the result will be returned.</span></span>

<span data-ttu-id="3829d-153">Si vous souhaitez revenir à la page **Configuration**, accédez à la page `setting.aspx` de l’application web.</span><span class="sxs-lookup"><span data-stu-id="3829d-153">If you want to return to the **Configuration** page, go to the `setting.aspx` page of the web app.</span></span> <span data-ttu-id="3829d-154">Par exemple : `http://carprediction.azurewebsites.net/setting.aspx.`. Vous serez invité à saisir de nouveau la clé de l’API pour pouvoir accéder à la page et mettre à jour les paramètres.</span><span class="sxs-lookup"><span data-stu-id="3829d-154">For example: `http://carprediction.azurewebsites.net/setting.aspx.` You will be prompted to enter the API key again - you need that to access the page and update the settings.</span></span>

<span data-ttu-id="3829d-155">Vous pouvez arrêter, redémarrer ou supprimer l’application web dans le portail Azure comme n’importe quelle autre application web.</span><span class="sxs-lookup"><span data-stu-id="3829d-155">You can stop, restart, or delete the web app in the Azure portal like any other web app.</span></span> <span data-ttu-id="3829d-156">Tant qu’elle est en cours d’exécution, vous pouvez accéder à l’adresse Web de base et saisir les nouvelles valeurs.</span><span class="sxs-lookup"><span data-stu-id="3829d-156">As long as it is running you can browse to the home web address and enter new values.</span></span>

## <a name="how-to-use-the-batch-execution-service-bes-template"></a><span data-ttu-id="3829d-157">Comment utiliser le modèle Batch Execution Service (BES)</span><span class="sxs-lookup"><span data-stu-id="3829d-157">How to use the Batch Execution Service (BES) template</span></span>
<span data-ttu-id="3829d-158">Vous pouvez utiliser le modèle d’application Web BES de la même manière que le modèle RRS, à ceci près que l’application Web créée vous permettra d’envoyer plusieurs lignes de données et de recevoir plusieurs résultats.</span><span class="sxs-lookup"><span data-stu-id="3829d-158">You can use the BES web app template in the same way as the RRS template, except that the web app that's created will allow you to submit multiple rows of data and receive multiple results.</span></span>

<span data-ttu-id="3829d-159">Les valeurs d’entrée d’un service web d’exécution de lot peuvent provenir du stockage Azure ou d’un fichier local. Les résultats sont stockés dans un conteneur de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="3829d-159">The input values for a batch execution web service can come from Azure storage or a local file; the results are stored in an Azure storage container.</span></span>
<span data-ttu-id="3829d-160">Vous aurez donc besoin d’un conteneur de stockage Azure pour stocker les résultats renvoyés par l’application Web. Vous devrez également préparer vos données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="3829d-160">So, you'll need an Azure storage container to hold the results returned by the web app, and you'll need to get your input data ready.</span></span>

![Procédure d’utilisation du modèle Web BES][image2]

1. <span data-ttu-id="3829d-162">Pour créer l’application web BES, suivez la même procédure que celle utilisée pour le modèle RRS. Cependant, vous devrez cette fois accéder à [Azure ML Batch Execution Service Web App Template](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) pour ouvrir le modèle BES sur la Place de marché Azure, puis cliquer sur **Créer une application web**.</span><span class="sxs-lookup"><span data-stu-id="3829d-162">Follow the same procedure to create the BES web app as for the RRS template, except go to [Azure ML Batch Execution Service Web App Template](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) to open the BES template on Azure Marketplace and click **Create Web App**.</span></span>

2. <span data-ttu-id="3829d-163">Pour spécifier l’emplacement de stockage des résultats, indiquez les informations du conteneur de destination sur la page d’accueil de l’application Web.</span><span class="sxs-lookup"><span data-stu-id="3829d-163">To specify where you want the results stored, enter the destination container information on the web app home page.</span></span> <span data-ttu-id="3829d-164">Indiquez également l’emplacement d’où l’application Web pourra extraire ses valeurs d’entrée, à savoir dans un fichier local ou dans un conteneur de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="3829d-164">Also specify where the web app can get the input values, either in a local file or an Azure storage container.</span></span>
   <span data-ttu-id="3829d-165">Cliquez sur **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="3829d-165">Click **Submit**.</span></span>
   
    ![Informations sur le stockage][image7]

<span data-ttu-id="3829d-167">L’application Web affiche une page avec l’état de la tâche.</span><span class="sxs-lookup"><span data-stu-id="3829d-167">The web app will display a page with job status.</span></span>
<span data-ttu-id="3829d-168">Une fois la tâche terminée, vous obtiendrez l’emplacement des résultats dans le stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="3829d-168">When the job has completed you'll be given the location of the results in Azure blob storage.</span></span> <span data-ttu-id="3829d-169">Vous avez également la possibilité de télécharger les résultats dans un fichier local.</span><span class="sxs-lookup"><span data-stu-id="3829d-169">You also have the option of downloading the results to a local file.</span></span>

## <a name="for-more-information"></a><span data-ttu-id="3829d-170">Pour plus d’informations</span><span class="sxs-lookup"><span data-stu-id="3829d-170">For more information</span></span>
<span data-ttu-id="3829d-171">Pour en savoir plus sur...</span><span class="sxs-lookup"><span data-stu-id="3829d-171">To learn more about...</span></span>

* <span data-ttu-id="3829d-172">la création d’une expérience d’apprentissage automatique avec Machine Learning Studio, consultez [Création de votre première expérience dans Azure Machine Learning Studio](machine-learning-create-experiment.md)</span><span class="sxs-lookup"><span data-stu-id="3829d-172">creating a machine learning experiment with Machine Learning Studio, see [Create your first experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md)</span></span>
* <span data-ttu-id="3829d-173">le déploiement de votre expérience d’apprentissage automatique sous la forme d’un service web, consultez [Déploiement d’un service web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md)</span><span class="sxs-lookup"><span data-stu-id="3829d-173">how to deploy your machine learning experiment as a web service, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md)</span></span>
* <span data-ttu-id="3829d-174">d’autres manières d’accéder à votre service web, consultez [Utilisation d’un service web Azure Machine Learning](machine-learning-consume-web-services.md)</span><span class="sxs-lookup"><span data-stu-id="3829d-174">other ways to access your web service, see [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md)</span></span>

[image1]: media/machine-learning-consume-web-service-with-web-app-template/rrs-web-template-flow.png
[image2]: media/machine-learning-consume-web-service-with-web-app-template/bes-web-template-flow.png
[image3]: media/machine-learning-consume-web-service-with-web-app-template/api-key.png
[image4]: media/machine-learning-consume-web-service-with-web-app-template/post-uri.png
[image5]: media/machine-learning-consume-web-service-with-web-app-template/create-web-app.png
[image6]: media/machine-learning-consume-web-service-with-web-app-template/web-service-info.png
[image7]: media/machine-learning-consume-web-service-with-web-app-template/storage.png
