---
title: "Services web Azure Machine Learning : déploiement et consommation | Microsoft Docs"
description: "Ressources pour le déploiement et la consommation de services web."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: 47635376-d1f4-4ea4-a6af-bd1f99f69a69
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 539c2abb053a0f981be0374defe45cf4d96b740b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-web-services-deployment-and-consumption"></a><span data-ttu-id="f28c6-103">Services web Azure Machine Learning : déploiement et consommation</span><span class="sxs-lookup"><span data-stu-id="f28c6-103">Azure Machine Learning Web Services: Deployment and consumption</span></span>
<span data-ttu-id="f28c6-104">Vous pouvez utiliser des modèles et flux de travail de l’apprentissage automatique toodeploy Azure Machine Learning en tant que services web.</span><span class="sxs-lookup"><span data-stu-id="f28c6-104">You can use Azure Machine Learning toodeploy machine-learning workflows and models as web services.</span></span> <span data-ttu-id="f28c6-105">Ces services web peuvent ensuite être utilisé toocall hello l’apprentissage automatique modèles à partir d’applications sur des prévisions hello Internet toodo en temps réel ou en mode batch.</span><span class="sxs-lookup"><span data-stu-id="f28c6-105">These web services can then be used toocall hello machine-learning models from applications over hello Internet toodo predictions in real time or in batch mode.</span></span> <span data-ttu-id="f28c6-106">Les services web hello étant RESTful, vous pouvez les appeler à partir de différents langages de programmation et les plateformes, comme .NET et Java et d’applications, telles qu’Excel.</span><span class="sxs-lookup"><span data-stu-id="f28c6-106">Because hello web services are RESTful, you can call them from various programming languages and platforms, such as .NET and Java, and from applications, such as Excel.</span></span>

<span data-ttu-id="f28c6-107">Hello les sections suivantes fournissent des liens toowalkthroughs, le code et documentation toohelp vous aider à démarrer.</span><span class="sxs-lookup"><span data-stu-id="f28c6-107">hello next sections provide links toowalkthroughs, code, and documentation toohelp get you started.</span></span>

## <a name="deploy-a-web-service"></a><span data-ttu-id="f28c6-108">Déployer un service web</span><span class="sxs-lookup"><span data-stu-id="f28c6-108">Deploy a web service</span></span>
### <a name="with-azure-machine-learning-studio"></a><span data-ttu-id="f28c6-109">Avec Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="f28c6-109">With Azure Machine Learning Studio</span></span>
<span data-ttu-id="f28c6-110">Machine Learning Studio et du portail de Services Web de Microsoft Azure Machine Learning hello vous aider à déployer et gérer un service web sans écrire de code.</span><span class="sxs-lookup"><span data-stu-id="f28c6-110">Machine Learning Studio and hello Microsoft Azure Machine Learning Web Services portal help you deploy and manage a web service without writing code.</span></span>

<span data-ttu-id="f28c6-111">Hello liens suivants fournissent des informations générales sur la façon de toodeploy un nouveau service web :</span><span class="sxs-lookup"><span data-stu-id="f28c6-111">hello following links provide general Information about how toodeploy a new web service:</span></span>

* <span data-ttu-id="f28c6-112">Pour obtenir une présentation toodeploy un nouveau service web qui est basé sur le Gestionnaire de ressources Azure, voir [déployer un nouveau service web](machine-learning-webservice-deploy-a-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="f28c6-112">For an overview about how toodeploy a new web service that's based on Azure Resource Manager, see [Deploy a new web service](machine-learning-webservice-deploy-a-web-service.md).</span></span>
* <span data-ttu-id="f28c6-113">Pour une procédure pas à pas sur la façon toodeploy un service web, consultez [déployer un service web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="f28c6-113">For a walkthrough about how toodeploy a web service, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="f28c6-114">Pour une procédure pas à pas complète sur la façon toocreate et déployer un service web, consultez [procédure pas à pas étape 1 : créer un espace de travail Machine Learning](machine-learning-walkthrough-1-create-ml-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="f28c6-114">For a full walkthrough about how toocreate and deploy a web service, see [Walkthrough Step 1: Create a Machine Learning workspace](machine-learning-walkthrough-1-create-ml-workspace.md).</span></span>
* <span data-ttu-id="f28c6-115">Pour des exemples spécifiques de déploiement d’un service web, consultez :</span><span class="sxs-lookup"><span data-stu-id="f28c6-115">For specific examples that deploy a web service, see:</span></span>

  * [<span data-ttu-id="f28c6-116">Procédure pas à pas, étape 5 : Déployer le service web de Azure Machine Learning hello</span><span class="sxs-lookup"><span data-stu-id="f28c6-116">Walkthrough Step 5: Deploy hello Azure Machine Learning web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
  * [<span data-ttu-id="f28c6-117">Comment toodeploy un site web de service toomultiple régions</span><span class="sxs-lookup"><span data-stu-id="f28c6-117">How toodeploy a web service toomultiple regions</span></span>](machine-learning-how-to-deploy-to-multiple-regions.md)

### <a name="with-web-services-resource-provider-apis-azure-resource-manager-apis"></a><span data-ttu-id="f28c6-118">Avec les API du fournisseur de ressources des services web (API Azure Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="f28c6-118">With web services resource provider APIs (Azure Resource Manager APIs)</span></span>
<span data-ttu-id="f28c6-119">fournisseur de ressources Azure Machine Learning Hello pour les services web permet le déploiement et la gestion des services web à l’aide d’appels d’API REST.</span><span class="sxs-lookup"><span data-stu-id="f28c6-119">hello Azure Machine Learning resource provider for web services enables deployment and management of web services by using REST API calls.</span></span> <span data-ttu-id="f28c6-120">Pour plus de détails, consultez la référence [Service web Machine Learning (REST)](/rest/api/machinelearning/index).</span><span class="sxs-lookup"><span data-stu-id="f28c6-120">For additional details, see the [Machine Learning Web Service (REST)](/rest/api/machinelearning/index) reference.</span></span>

<!-- [Machine Learning Web Service (REST)](https://msdn.microsoft.com/library/azure/mt767538.aspx) reference. -->


### <a name="with-powershell-cmdlets"></a><span data-ttu-id="f28c6-121">Avec des applets de commande PowerShell</span><span class="sxs-lookup"><span data-stu-id="f28c6-121">With PowerShell cmdlets</span></span>
<span data-ttu-id="f28c6-122">Le fournisseur de ressources Azure Machine Learning pour les services web permet le déploiement et la gestion des services web au moyen d’applets de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f28c6-122">Azure Machine Learning resource provider for web services enables deployment and management of web services by using PowerShell cmdlets.</span></span>

<span data-ttu-id="f28c6-123">applets de commande hello toouse, vous devez vous connecter tooyour compte Azure dans l’environnement PowerShell de hello à l’aide de hello [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="f28c6-123">toouse hello cmdlets, you must first sign in tooyour Azure account from within hello PowerShell environment by using hello [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span> <span data-ttu-id="f28c6-124">Si vous n’êtes pas familiarisé avec le fonctionnement des commandes toocall PowerShell qui sont basées sur le Gestionnaire de ressources, consultez [à l’aide de Azure PowerShell avec Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).</span><span class="sxs-lookup"><span data-stu-id="f28c6-124">If you are unfamiliar with how toocall PowerShell commands that are based on Resource Manager, see [Using Azure PowerShell with Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).</span></span>

<span data-ttu-id="f28c6-125">tooexport votre prédictive de faire des essais, d’utiliser [cet exemple de code](https://github.com/ritwik20/AzureML-WebServices).</span><span class="sxs-lookup"><span data-stu-id="f28c6-125">tooexport your predictive experiment, use [this sample code](https://github.com/ritwik20/AzureML-WebServices).</span></span> <span data-ttu-id="f28c6-126">Après avoir créé le fichier .exe de hello à partir du code hello, vous pouvez taper :</span><span class="sxs-lookup"><span data-stu-id="f28c6-126">After you create hello .exe file from hello code, you can type:</span></span>

    C:\<folder>\GetWSD <experiment-url> <workspace-auth-token>

<span data-ttu-id="f28c6-127">Exécute l’application hello crée un modèle JSON du service web.</span><span class="sxs-lookup"><span data-stu-id="f28c6-127">Running hello application creates a web service JSON template.</span></span> <span data-ttu-id="f28c6-128">toouse hello modèle toodeploy un service web, vous devez ajouter hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="f28c6-128">toouse hello template toodeploy a web service, you must add hello following information:</span></span>

* <span data-ttu-id="f28c6-129">Nom et clé du compte de stockage</span><span class="sxs-lookup"><span data-stu-id="f28c6-129">Storage account name and key</span></span>

    <span data-ttu-id="f28c6-130">Vous pouvez obtenir le nom de compte de stockage hello et la clé à partir de deux hello [portail Azure](https://portal.azure.com/) ou hello [portail Azure classic](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="f28c6-130">You can get hello storage account name and key from either hello [Azure portal](https://portal.azure.com/) or hello [Azure classic portal](http://manage.windowsazure.com/).</span></span>
* <span data-ttu-id="f28c6-131">ID de plan d’engagement</span><span class="sxs-lookup"><span data-stu-id="f28c6-131">Commitment plan ID</span></span>

    <span data-ttu-id="f28c6-132">Vous pouvez obtenir l’ID de plan hello de hello [Azure Machine Learning Services Web](https://services.azureml.net) portail en vous connectant et en cliquant sur un nom de plan.</span><span class="sxs-lookup"><span data-stu-id="f28c6-132">You can get hello plan ID from hello [Azure Machine Learning Web Services](https://services.azureml.net) portal by signing in and clicking a plan name.</span></span>

<span data-ttu-id="f28c6-133">Ajoutez-les modèle JSON de toohello en tant qu’enfants de hello *propriétés* nœud hello de même niveau en tant que hello *MachineLearningWorkspace* nœud.</span><span class="sxs-lookup"><span data-stu-id="f28c6-133">Add them toohello JSON template as children of hello *Properties* node at hello same level as hello *MachineLearningWorkspace* node.</span></span>

<span data-ttu-id="f28c6-134">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="f28c6-134">Here's an example:</span></span>

    "StorageAccount": {
            "name": "YourStorageAccountName",
            "key": "YourStorageAccountKey"
    },
    "CommitmentPlan": {
        "id": "subscriptions/YouSubscriptionID/resourceGroups/YourResourceGroupID/providers/Microsoft.MachineLearning/commitmentPlans/YourPlanName"
    }

<span data-ttu-id="f28c6-135">Consultez hello suivant des articles et exemples de code pour plus d’informations :</span><span class="sxs-lookup"><span data-stu-id="f28c6-135">See hello following articles and sample code for additional details:</span></span>

* <span data-ttu-id="f28c6-136">[Applets de commande Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt767952.aspx) sur MSDN</span><span class="sxs-lookup"><span data-stu-id="f28c6-136">[Azure Machine Learning Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) reference on MSDN</span></span>
* <span data-ttu-id="f28c6-137">Exemple de [procédure pas à pas](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) sur GitHub</span><span class="sxs-lookup"><span data-stu-id="f28c6-137">Sample [walkthrough](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) on GitHub</span></span>

## <a name="consume-hello-web-services"></a><span data-ttu-id="f28c6-138">Utiliser les services web hello</span><span class="sxs-lookup"><span data-stu-id="f28c6-138">Consume hello web services</span></span>
### <a name="from-hello-azure-machine-learning-web-services-ui-testing"></a><span data-ttu-id="f28c6-139">À partir de hello Azure Machine Learning Services interface utilisateur Web (test)</span><span class="sxs-lookup"><span data-stu-id="f28c6-139">From hello Azure Machine Learning Web Services UI (Testing)</span></span>
<span data-ttu-id="f28c6-140">Vous pouvez tester votre service web à partir du portail de Services Web de Azure Machine Learning hello.</span><span class="sxs-lookup"><span data-stu-id="f28c6-140">You can test your web service from hello Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="f28c6-141">Cela comprend le test du service de requête-réponse hello (RR) et des interfaces de service de l’exécution par lots (BES).</span><span class="sxs-lookup"><span data-stu-id="f28c6-141">This includes testing hello Request-Response service (RRS) and Batch Execution service (BES) interfaces.</span></span>

* [<span data-ttu-id="f28c6-142">Déployer comme un nouveau service web</span><span class="sxs-lookup"><span data-stu-id="f28c6-142">Deploy a new web service</span></span>](machine-learning-webservice-deploy-a-web-service.md)
* [<span data-ttu-id="f28c6-143">Déploiement d’un service web Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f28c6-143">Deploy an Azure Machine Learning web service</span></span>](machine-learning-publish-a-machine-learning-web-service.md)
* [<span data-ttu-id="f28c6-144">Procédure pas à pas, étape 5 : Déployer le service web de Azure Machine Learning hello</span><span class="sxs-lookup"><span data-stu-id="f28c6-144">Walkthrough Step 5: Deploy hello Azure Machine Learning web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)

### <a name="from-excel"></a><span data-ttu-id="f28c6-145">À partir d’Excel</span><span class="sxs-lookup"><span data-stu-id="f28c6-145">From Excel</span></span>
<span data-ttu-id="f28c6-146">Vous pouvez télécharger un modèle Excel qui utilise le service web de hello :</span><span class="sxs-lookup"><span data-stu-id="f28c6-146">You can download an Excel template that consumes hello web service:</span></span>

* [<span data-ttu-id="f28c6-147">Utilisation d’un service web Microsoft Azure Machine Learning à partir de Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="f28c6-147">Consuming an Azure Machine Learning web service from Excel</span></span>](machine-learning-consuming-from-excel.md)
* [<span data-ttu-id="f28c6-148">Complément Excel de services web Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f28c6-148">Excel add-in for Azure Machine Learning Web Services</span></span>](machine-learning-excel-add-in-for-web-services.md)

### <a name="from-a-rest-based-client"></a><span data-ttu-id="f28c6-149">À partir d’un client basé sur REST</span><span class="sxs-lookup"><span data-stu-id="f28c6-149">From a REST-based client</span></span>
<span data-ttu-id="f28c6-150">Les services web Azure Machine Learning sont des API RESTful.</span><span class="sxs-lookup"><span data-stu-id="f28c6-150">Azure Machine Learning Web Services are RESTful APIs.</span></span> <span data-ttu-id="f28c6-151">Vous pouvez utiliser ces API à partir de différentes plateformes, telles que .NET, Python, R, Java, hello de etc. **consommer** page de votre service web sur hello [portail de Services Web de Microsoft Azure Machine Learning](https://services.azureml.net) a exemple code qui peut vous aider à commencer.</span><span class="sxs-lookup"><span data-stu-id="f28c6-151">You can consume these APIs from various platforms, such as .NET, Python, R, Java, etc. hello **Consume** page for your web service on hello [Microsoft Azure Machine Learning Web Services portal](https://services.azureml.net) has sample code that can help you get started.</span></span> <span data-ttu-id="f28c6-152">Pour plus d’informations, consultez [comment tooconsume un service Web de Azure Machine Learning](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="f28c6-152">For more information, see [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>
