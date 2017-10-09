---
title: "un service web de Machine Learning avec un modèle d’application web d’aaaConsume | Documents Microsoft"
description: "Utilisez un modèle d’application web dans Azure Marketplace tooconsume un service web prédictif dans Azure Machine Learning."
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
ms.openlocfilehash: 1199377bead470807d58ca7f7a667175cbb88450
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-azure-machine-learning-web-service-with-a-web-app-template"></a><span data-ttu-id="0f870-104">Utilisation d’un service Web Microsoft Azure Machine Learning à l’aide d’un modèle d’application Web</span><span class="sxs-lookup"><span data-stu-id="0f870-104">Consume an Azure Machine Learning web service with a web app template</span></span>

<span data-ttu-id="0f870-105">Une fois vous avez développé votre modèle de prévision et déployé en tant que service web Azure à l’aide de la Machine Learning Studio, ou à l’aide des outils tels que R ou Python, vous pouvez accéder au modèle mis à hello à l’aide d’une API REST.</span><span class="sxs-lookup"><span data-stu-id="0f870-105">Once you've developed your predictive model and deployed it as an Azure web service using Machine Learning Studio, or using tools such as R or Python, you can access hello operationalized model using a REST API.</span></span>

<span data-ttu-id="0f870-106">Il existe plusieurs façons tooconsume hello API REST accès hello service web et.</span><span class="sxs-lookup"><span data-stu-id="0f870-106">There are a number of ways tooconsume hello REST API and access hello web service.</span></span> <span data-ttu-id="0f870-107">Par exemple, vous pouvez écrire une application en c#, R, ou Python à l’aide de hello exemple de code généré lorsque vous avez déployé le service web de hello (disponible dans hello [portail de Services Web Machine Learning](https://services.azureml.net/quickstart) ou tableau de bord de service web hello dans Machine Learning Studio).</span><span class="sxs-lookup"><span data-stu-id="0f870-107">For example, you can write an application in C#, R, or Python using hello sample code generated for you when you deployed hello web service (available in hello [Machine Learning Web Services Portal](https://services.azureml.net/quickstart) or in hello web service dashboard in Machine Learning Studio).</span></span> <span data-ttu-id="0f870-108">Ou vous pouvez utiliser le classeur Microsoft Excel de hello exemple créé à hello même temps.</span><span class="sxs-lookup"><span data-stu-id="0f870-108">Or you can use hello sample Microsoft Excel workbook created for you at hello same time.</span></span>

<span data-ttu-id="0f870-109">Mais hello tooaccess rapidement et facilement votre service web se fait via les modèles d’application hello Web disponibles dans hello [Azure Marketplace des applications Web](https://azure.microsoft.com/marketplace/web-applications/all/).</span><span class="sxs-lookup"><span data-stu-id="0f870-109">But hello quickest and easiest way tooaccess your web service is through hello Web App Templates available in hello [Azure Web App Marketplace](https://azure.microsoft.com/marketplace/web-applications/all/).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="hello-azure-machine-learning-web-app-templates"></a><span data-ttu-id="0f870-110">Hello modèles d’application Web Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="0f870-110">hello Azure Machine Learning Web App Templates</span></span>
<span data-ttu-id="0f870-111">modèles d’application web Hello disponibles Bonjour Azure Marketplace peuvent générer une application web personnalisée qui connaît les données d’entrée et les résultats attendus de votre service web.</span><span class="sxs-lookup"><span data-stu-id="0f870-111">hello web app templates available in hello Azure Marketplace can build a custom web app that knows your web service's input data and expected results.</span></span> <span data-ttu-id="0f870-112">Vous devez toodo est de fournir des données et le service web d’hello web application accès tooyour et modèle de hello hello rest.</span><span class="sxs-lookup"><span data-stu-id="0f870-112">All you need toodo is give hello web app access tooyour web service and data, and hello template does hello rest.</span></span>

<span data-ttu-id="0f870-113">Il existe deux modèles :</span><span class="sxs-lookup"><span data-stu-id="0f870-113">Two templates are available:</span></span>

* [<span data-ttu-id="0f870-114">Modèle d’application Web Azure ML Request-Response Service</span><span class="sxs-lookup"><span data-stu-id="0f870-114">Azure ML Request-Response Service Web App Template</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/)
* [<span data-ttu-id="0f870-115">Modèle d’application Web Azure ML Batch Execution Service</span><span class="sxs-lookup"><span data-stu-id="0f870-115">Azure ML Batch Execution Service Web App Template</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/)

<span data-ttu-id="0f870-116">Chaque modèle crée un exemple d’application ASP.NET, à l’aide de hello URI de l’API et la clé de votre service web et le déploie comme un tooAzure du site web.</span><span class="sxs-lookup"><span data-stu-id="0f870-116">Each template creates a sample ASP.NET application, using hello API URI and Key for your web service, and deploys it as a web site tooAzure.</span></span> <span data-ttu-id="0f870-117">modèle de Service de requête-réponse (RR) Hello crée une application web qui vous permet de toosend une seule ligne de données toohello web service tooget un résultat unique.</span><span class="sxs-lookup"><span data-stu-id="0f870-117">hello Request-Response Service (RRS) template creates a web app that allows you toosend a single row of data toohello web service tooget a single result.</span></span> <span data-ttu-id="0f870-118">modèle de Service de l’exécution de lot (BES) Hello crée une application web qui vous permet de toosend nombre de lignes de données tooget plusieurs résultats.</span><span class="sxs-lookup"><span data-stu-id="0f870-118">hello Batch Execution Service (BES) template creates a web app that allows you toosend many rows of data tooget multiple results.</span></span>

<span data-ttu-id="0f870-119">Aucun codage n’est nécessaire de toouse ces modèles.</span><span class="sxs-lookup"><span data-stu-id="0f870-119">No coding is required toouse these templates.</span></span> <span data-ttu-id="0f870-120">Vous devez simplement spécifier hello clé API et l’URI et les versions de modèle de hello application hello pour vous.</span><span class="sxs-lookup"><span data-stu-id="0f870-120">You just supply hello API Key and URI, and hello template builds hello application for you.</span></span>

<span data-ttu-id="0f870-121">clé de hello API tooget et l’URI de requête pour un service web :</span><span class="sxs-lookup"><span data-stu-id="0f870-121">tooget hello API key and Request URI for a web service:</span></span>

1. <span data-ttu-id="0f870-122">Bonjour [portail de Services Web](https://services.azureml.net/quickstart), pour un service web, cliquez sur **Services Web** haut hello.</span><span class="sxs-lookup"><span data-stu-id="0f870-122">In hello [Web Services Portal](https://services.azureml.net/quickstart), for a New web service, click **Web Services** at hello top.</span></span> <span data-ttu-id="0f870-123">Pour un service web classique, cliquez sur **Services web classiques**.</span><span class="sxs-lookup"><span data-stu-id="0f870-123">Or for a Classic web service click **Classic Web Services**.</span></span>
2. <span data-ttu-id="0f870-124">Cliquez sur hello web service tooaccess.</span><span class="sxs-lookup"><span data-stu-id="0f870-124">Click hello web service you want tooaccess.</span></span>
3. <span data-ttu-id="0f870-125">Pour un service web standard, cliquez sur hello point de terminaison tooaccess.</span><span class="sxs-lookup"><span data-stu-id="0f870-125">For a Classic web service, click hello endpoint you want tooaccess.</span></span>
4. <span data-ttu-id="0f870-126">Cliquez sur **consommer** haut hello.</span><span class="sxs-lookup"><span data-stu-id="0f870-126">Click **Consume** at hello top.</span></span>
5. <span data-ttu-id="0f870-127">Hello de copie **principal** ou **clé secondaire** et l’enregistrer.</span><span class="sxs-lookup"><span data-stu-id="0f870-127">Copy hello **Primary** or **Secondary Key** and save it.</span></span>
6. <span data-ttu-id="0f870-128">Si vous créez un modèle de Service de requête-réponse (RR), copiez hello **demande-réponse** URI et l’enregistrer.</span><span class="sxs-lookup"><span data-stu-id="0f870-128">If you're creating a Request-Response Service (RRS) template, copy hello **Request-Response** URI and save it.</span></span> <span data-ttu-id="0f870-129">Si vous créez un modèle de Service de l’exécution de lot (BES), copiez hello **de requêtes de lots** URI et l’enregistrer.</span><span class="sxs-lookup"><span data-stu-id="0f870-129">If you're creating a Batch Execution Service (BES) template, copy hello **Batch Requests** URI and save it.</span></span>


## <a name="how-toouse-hello-request-response-service-rrs-template"></a><span data-ttu-id="0f870-130">Comment toouse hello modèle de Service de requête-réponse (RR)</span><span class="sxs-lookup"><span data-stu-id="0f870-130">How toouse hello Request-Response Service (RRS) template</span></span>
<span data-ttu-id="0f870-131">Suivez ces modèle application étapes toouse hello RR web, comme indiqué dans hello suivant schéma.</span><span class="sxs-lookup"><span data-stu-id="0f870-131">Follow these steps toouse hello RRS web app template, as shown in hello following diagram.</span></span>

![Modèle de processus toouse RR web][image1]


<!--    ![API Key][image3] -->

<!-- This value will look like this:
   
        https://ussouthcentral.services.azureml.net/workspaces/<workspace-id>/services/<service-id>/execute?api-version=2.0&details=true
   
    ![Request URI][image4] -->

1. <span data-ttu-id="0f870-133">Accédez toohello [portail Azure](https://portal.azure.com), **connexion**, cliquez sur **nouveau**, recherchez et sélectionnez **l’application Web Azure ML avec requête-réponse Service**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="0f870-133">Go toohello [Azure portal](https://portal.azure.com), **Login**, click **New**, search for and select **Azure ML Request-Response Service Web App**, then click **Create**.</span></span> 
   
   * <span data-ttu-id="0f870-134">Donnez un nom unique à votre application Web.</span><span class="sxs-lookup"><span data-stu-id="0f870-134">Give your web app a unique name.</span></span> <span data-ttu-id="0f870-135">URL de Hello de hello web application sera ce nom, suivi par `.azurewebsites.net.` , par exemple,`http://carprediction.azurewebsites.net.`</span><span class="sxs-lookup"><span data-stu-id="0f870-135">hello URL of hello web app will be this name followed by `.azurewebsites.net.` For example, `http://carprediction.azurewebsites.net.`</span></span>
   * <span data-ttu-id="0f870-136">Sélectionnez hello abonnement Azure et des services sous lequel votre service web est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="0f870-136">Select hello Azure subscription and services under which your web service is running.</span></span>
   * <span data-ttu-id="0f870-137">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="0f870-137">Click **Create**.</span></span>
     
     ![Créer une application web][image5]

4. <span data-ttu-id="0f870-139">Lorsque Azure a terminé le déploiement de l’application hello web, cliquez sur hello **URL** hello page de paramètres d’application web dans Azure, ou entrez l’URL de hello dans un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="0f870-139">When Azure has finished deploying hello web app, click hello **URL** on hello web app settings page in Azure, or enter hello URL in a web browser.</span></span> <span data-ttu-id="0f870-140">Par exemple, `http://carprediction.azurewebsites.net.`</span><span class="sxs-lookup"><span data-stu-id="0f870-140">For example, `http://carprediction.azurewebsites.net.`</span></span>
5. <span data-ttu-id="0f870-141">Lorsque hello web application première s’exécute qu’il vous demandera hello **API poster une URL** et **clé API**.</span><span class="sxs-lookup"><span data-stu-id="0f870-141">When hello web app first runs it will ask you for hello **API Post URL** and **API Key**.</span></span>
   <span data-ttu-id="0f870-142">Entrez les valeurs hello vous avez enregistré précédemment (**URI de requête** et **clé API**, respectivement).</span><span class="sxs-lookup"><span data-stu-id="0f870-142">Enter hello values you saved earlier (**Request URI** and **API Key**, respectively).</span></span>
     
     <span data-ttu-id="0f870-143">Cliquez sur **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="0f870-143">Click **Submit**.</span></span>
     
     ![Entrer l’URI de publication et la clé de l’API][image6]

6. <span data-ttu-id="0f870-145">Hello web application affiche son **Configuration de l’application Web** page avec les paramètres du service web en cours hello.</span><span class="sxs-lookup"><span data-stu-id="0f870-145">hello web app displays its **Web App Configuration** page with hello current web service settings.</span></span> <span data-ttu-id="0f870-146">Ici vous pouvez modifier les paramètres de toohello utilisés par l’application web hello.</span><span class="sxs-lookup"><span data-stu-id="0f870-146">Here you can make changes toohello settings used by hello web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0f870-147">Modification des paramètres de hello ici les modifie uniquement pour cette application web.</span><span class="sxs-lookup"><span data-stu-id="0f870-147">Changing hello settings here only changes them for this web app.</span></span> <span data-ttu-id="0f870-148">Il ne change pas les paramètres par défaut hello de votre service web.</span><span class="sxs-lookup"><span data-stu-id="0f870-148">It doesn't change hello default settings of your web service.</span></span> <span data-ttu-id="0f870-149">Par exemple, si vous modifiez hello **Description** ici ne change pas description hello indiquée sur le tableau de bord du service hello web dans Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="0f870-149">For example, if you change hello **Description** here it doesn't change hello description shown on hello web service dashboard in Machine Learning Studio.</span></span>
   > 
   > 
   
    <span data-ttu-id="0f870-150">Lorsque vous avez terminé, cliquez sur **enregistrer les modifications**, puis cliquez sur **accédez tooHome Page**.</span><span class="sxs-lookup"><span data-stu-id="0f870-150">When you're done, click **Save changes**, and then click **Go tooHome Page**.</span></span>

7. <span data-ttu-id="0f870-151">Page d’accueil, vous pouvez saisir les valeurs service web de tooyour toosend de hello.</span><span class="sxs-lookup"><span data-stu-id="0f870-151">From hello home page you can enter values toosend tooyour web service.</span></span> <span data-ttu-id="0f870-152">Cliquez sur **Submit** lorsque vous avez terminé, et hello résultat est retourné.</span><span class="sxs-lookup"><span data-stu-id="0f870-152">Click **Submit** when you're done, and hello result will be returned.</span></span>

<span data-ttu-id="0f870-153">Si vous souhaitez tooreturn toohello **Configuration** page, aller toohello `setting.aspx` page de l’application web hello.</span><span class="sxs-lookup"><span data-stu-id="0f870-153">If you want tooreturn toohello **Configuration** page, go toohello `setting.aspx` page of hello web app.</span></span> <span data-ttu-id="0f870-154">Par exemple : `http://carprediction.azurewebsites.net/setting.aspx.` vous sera à nouveau clé de hello API demandées tooenter - vous avez besoin que tooaccess hello page et mettre à jour les paramètres hello.</span><span class="sxs-lookup"><span data-stu-id="0f870-154">For example: `http://carprediction.azurewebsites.net/setting.aspx.` You will be prompted tooenter hello API key again - you need that tooaccess hello page and update hello settings.</span></span>

<span data-ttu-id="0f870-155">Vous pouvez arrêter, redémarrer ou supprimer l’application web de hello Bonjour Azure portal comme toute autre application web.</span><span class="sxs-lookup"><span data-stu-id="0f870-155">You can stop, restart, or delete hello web app in hello Azure portal like any other web app.</span></span> <span data-ttu-id="0f870-156">Tant qu’il est en cours d’exécution, vous pouvez parcourir l’adresse d’accueil web toohello et entrez les nouvelles valeurs.</span><span class="sxs-lookup"><span data-stu-id="0f870-156">As long as it is running you can browse toohello home web address and enter new values.</span></span>

## <a name="how-toouse-hello-batch-execution-service-bes-template"></a><span data-ttu-id="0f870-157">Comment toouse hello modèle de Service de l’exécution de lot (BES)</span><span class="sxs-lookup"><span data-stu-id="0f870-157">How toouse hello Batch Execution Service (BES) template</span></span>
<span data-ttu-id="0f870-158">Vous pouvez utiliser hello BES modèle d’application web Bonjour même sauf comme modèle de RR hello, cette application web hello créé vous permettra de toosubmit plusieurs lignes de données et de recevoir plusieurs résultats.</span><span class="sxs-lookup"><span data-stu-id="0f870-158">You can use hello BES web app template in hello same way as hello RRS template, except that hello web app that's created will allow you toosubmit multiple rows of data and receive multiple results.</span></span>

<span data-ttu-id="0f870-159">valeurs d’entrée de Hello pour un service web de l’exécution par lots peuvent provenir de stockage Azure ou un fichier local ; résultats de Hello sont stockés dans un conteneur de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="0f870-159">hello input values for a batch execution web service can come from Azure storage or a local file; hello results are stored in an Azure storage container.</span></span>
<span data-ttu-id="0f870-160">Par conséquent, vous aurez besoin une toohold de conteneur de stockage Azure hello résultats retournés par l’application web hello et vous aurez besoin de tooget vos données d’entrée prêt.</span><span class="sxs-lookup"><span data-stu-id="0f870-160">So, you'll need an Azure storage container toohold hello results returned by hello web app, and you'll need tooget your input data ready.</span></span>

![Traiter toouse BES modèle web][image2]

1. <span data-ttu-id="0f870-162">Suivez hello même hello toocreate de procédure BES web application que pour les modèles de RR hello, à l’exception de go trop[modèle d’application Azure ML lot l’exécution du Service Web](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) tooopen hello modèle BES sur Azure Marketplace, puis cliquez sur **créer l’application Web** .</span><span class="sxs-lookup"><span data-stu-id="0f870-162">Follow hello same procedure toocreate hello BES web app as for hello RRS template, except go too[Azure ML Batch Execution Service Web App Template](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) tooopen hello BES template on Azure Marketplace and click **Create Web App**.</span></span>

2. <span data-ttu-id="0f870-163">toospecify où vous souhaitez que les résultats de hello stockés, entrez les informations de conteneur de destination hello sur hello la page d’accueil de l’application web.</span><span class="sxs-lookup"><span data-stu-id="0f870-163">toospecify where you want hello results stored, enter hello destination container information on hello web app home page.</span></span> <span data-ttu-id="0f870-164">Spécifiez également où l’application hello web peut obtenir les valeurs d’entrée hello, dans un fichier local ou un conteneur de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="0f870-164">Also specify where hello web app can get hello input values, either in a local file or an Azure storage container.</span></span>
   <span data-ttu-id="0f870-165">Cliquez sur **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="0f870-165">Click **Submit**.</span></span>
   
    ![Informations sur le stockage][image7]

<span data-ttu-id="0f870-167">l’application Hello web affiche une page avec l’état du travail.</span><span class="sxs-lookup"><span data-stu-id="0f870-167">hello web app will display a page with job status.</span></span>
<span data-ttu-id="0f870-168">Lorsque hello est terminée, vous aurez emplacement hello de résultats hello dans le stockage blob Azure.</span><span class="sxs-lookup"><span data-stu-id="0f870-168">When hello job has completed you'll be given hello location of hello results in Azure blob storage.</span></span> <span data-ttu-id="0f870-169">Vous avez également option hello du téléchargement de fichiers local de hello résultats tooa.</span><span class="sxs-lookup"><span data-stu-id="0f870-169">You also have hello option of downloading hello results tooa local file.</span></span>

## <a name="for-more-information"></a><span data-ttu-id="0f870-170">Pour plus d’informations</span><span class="sxs-lookup"><span data-stu-id="0f870-170">For more information</span></span>
<span data-ttu-id="0f870-171">toolearn plus d’informations sur...</span><span class="sxs-lookup"><span data-stu-id="0f870-171">toolearn more about...</span></span>

* <span data-ttu-id="0f870-172">la création d’une expérience d’apprentissage automatique avec Machine Learning Studio, consultez [Création de votre première expérience dans Azure Machine Learning Studio](machine-learning-create-experiment.md)</span><span class="sxs-lookup"><span data-stu-id="0f870-172">creating a machine learning experiment with Machine Learning Studio, see [Create your first experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md)</span></span>
* <span data-ttu-id="0f870-173">Comment toodeploy votre apprentissage faire des essais en tant qu’un service web, consultez [déployer un service web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md)</span><span class="sxs-lookup"><span data-stu-id="0f870-173">how toodeploy your machine learning experiment as a web service, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md)</span></span>
* <span data-ttu-id="0f870-174">autres façons tooaccess votre service web, consultez [comment tooconsume un service Web de Azure Machine Learning](machine-learning-consume-web-services.md)</span><span class="sxs-lookup"><span data-stu-id="0f870-174">other ways tooaccess your web service, see [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md)</span></span>

[image1]: media/machine-learning-consume-web-service-with-web-app-template/rrs-web-template-flow.png
[image2]: media/machine-learning-consume-web-service-with-web-app-template/bes-web-template-flow.png
[image3]: media/machine-learning-consume-web-service-with-web-app-template/api-key.png
[image4]: media/machine-learning-consume-web-service-with-web-app-template/post-uri.png
[image5]: media/machine-learning-consume-web-service-with-web-app-template/create-web-app.png
[image6]: media/machine-learning-consume-web-service-with-web-app-template/web-service-info.png
[image7]: media/machine-learning-consume-web-service-with-web-app-template/storage.png
