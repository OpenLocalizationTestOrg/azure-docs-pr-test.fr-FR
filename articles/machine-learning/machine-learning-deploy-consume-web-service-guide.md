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
ms.openlocfilehash: 18edabe267ec06c08074d7a7a6d71435cedc8489
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-machine-learning-web-services-deployment-and-consumption"></a><span data-ttu-id="ecba5-103">Services web Azure Machine Learning : déploiement et consommation</span><span class="sxs-lookup"><span data-stu-id="ecba5-103">Azure Machine Learning Web Services: Deployment and consumption</span></span>
<span data-ttu-id="ecba5-104">Vous pouvez utiliser Azure Machine Learning pour déployer des flux de travail et des modèles de Machine Learning en tant que services web.</span><span class="sxs-lookup"><span data-stu-id="ecba5-104">You can use Azure Machine Learning to deploy machine-learning workflows and models as web services.</span></span> <span data-ttu-id="ecba5-105">Ces services web peuvent ensuite servir à appeler les modèles Machine Learning à partir d’applications via Internet pour effectuer des prévisions en temps réel ou par lots.</span><span class="sxs-lookup"><span data-stu-id="ecba5-105">These web services can then be used to call the machine-learning models from applications over the Internet to do predictions in real time or in batch mode.</span></span> <span data-ttu-id="ecba5-106">Les services web, RESTful, peuvent être appelés avec divers langages et plateformes de programmation, notamment Java, .NET et des applications comme Excel.</span><span class="sxs-lookup"><span data-stu-id="ecba5-106">Because the web services are RESTful, you can call them from various programming languages and platforms, such as .NET and Java, and from applications, such as Excel.</span></span>

<span data-ttu-id="ecba5-107">Les sections suivantes fournissent des liens vers des procédures pas à pas, du code et de la documentation pour vous aider à démarrer.</span><span class="sxs-lookup"><span data-stu-id="ecba5-107">The next sections provide links to walkthroughs, code, and documentation to help get you started.</span></span>

## <a name="deploy-a-web-service"></a><span data-ttu-id="ecba5-108">Déployer un service web</span><span class="sxs-lookup"><span data-stu-id="ecba5-108">Deploy a web service</span></span>
### <a name="with-azure-machine-learning-studio"></a><span data-ttu-id="ecba5-109">Avec Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="ecba5-109">With Azure Machine Learning Studio</span></span>
<span data-ttu-id="ecba5-110">Machine Learning Studio et le portail des services web Microsoft Azure Machine Learning vous permettent de déployer et de gérer un service web sans avoir à écrire du code.</span><span class="sxs-lookup"><span data-stu-id="ecba5-110">Machine Learning Studio and the Microsoft Azure Machine Learning Web Services portal help you deploy and manage a web service without writing code.</span></span>

<span data-ttu-id="ecba5-111">Les liens suivants fournissent des informations générales sur le processus de déploiement d’un nouveau service web :</span><span class="sxs-lookup"><span data-stu-id="ecba5-111">The following links provide general Information about how to deploy a new web service:</span></span>

* <span data-ttu-id="ecba5-112">Pour une vue d’ensemble du déploiement d’un nouveau service web basé sur Azure Resource Manager, consultez [Déployer un nouveau service web](machine-learning-webservice-deploy-a-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="ecba5-112">For an overview about how to deploy a new web service that's based on Azure Resource Manager, see [Deploy a new web service](machine-learning-webservice-deploy-a-web-service.md).</span></span>
* <span data-ttu-id="ecba5-113">Pour une présentation du déploiement d’un service web, consultez [Déployer un service web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="ecba5-113">For a walkthrough about how to deploy a web service, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="ecba5-114">Pour une présentation complète de la création et du déploiement d’un service web, consultez [Étape 1 du didacticiel pas à pas : créer un espace de travail Machine Learning](machine-learning-walkthrough-1-create-ml-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="ecba5-114">For a full walkthrough about how to create and deploy a web service, see [Walkthrough Step 1: Create a Machine Learning workspace](machine-learning-walkthrough-1-create-ml-workspace.md).</span></span>
* <span data-ttu-id="ecba5-115">Pour des exemples spécifiques de déploiement d’un service web, consultez :</span><span class="sxs-lookup"><span data-stu-id="ecba5-115">For specific examples that deploy a web service, see:</span></span>

  * [<span data-ttu-id="ecba5-116">Étape 5 du didacticiel pas à pas : Déploiement du service web Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="ecba5-116">Walkthrough Step 5: Deploy the Azure Machine Learning web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
  * [<span data-ttu-id="ecba5-117">Comment déployer un service web dans plusieurs régions</span><span class="sxs-lookup"><span data-stu-id="ecba5-117">How to deploy a web service to multiple regions</span></span>](machine-learning-how-to-deploy-to-multiple-regions.md)

### <a name="with-web-services-resource-provider-apis-azure-resource-manager-apis"></a><span data-ttu-id="ecba5-118">Avec les API du fournisseur de ressources des services web (API Azure Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="ecba5-118">With web services resource provider APIs (Azure Resource Manager APIs)</span></span>
<span data-ttu-id="ecba5-119">Le fournisseur de ressources Azure Machine Learning pour les services web permet le déploiement et la gestion des services web au moyen d’appels d’API REST.</span><span class="sxs-lookup"><span data-stu-id="ecba5-119">The Azure Machine Learning resource provider for web services enables deployment and management of web services by using REST API calls.</span></span> <span data-ttu-id="ecba5-120">Pour plus de détails, consultez la référence [Service web Machine Learning (REST)](/rest/api/machinelearning/index).</span><span class="sxs-lookup"><span data-stu-id="ecba5-120">For additional details, see the [Machine Learning Web Service (REST)](/rest/api/machinelearning/index) reference.</span></span>

<!-- [Machine Learning Web Service (REST)](https://msdn.microsoft.com/library/azure/mt767538.aspx) reference. -->


### <a name="with-powershell-cmdlets"></a><span data-ttu-id="ecba5-121">Avec des applets de commande PowerShell</span><span class="sxs-lookup"><span data-stu-id="ecba5-121">With PowerShell cmdlets</span></span>
<span data-ttu-id="ecba5-122">Le fournisseur de ressources Azure Machine Learning pour les services web permet le déploiement et la gestion des services web au moyen d’applets de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ecba5-122">Azure Machine Learning resource provider for web services enables deployment and management of web services by using PowerShell cmdlets.</span></span>

<span data-ttu-id="ecba5-123">Pour utiliser les applets de commande, vous devez tout d’abord vous connecter à votre compte Azure à partir de l’environnement PowerShell à l’aide de l’applet de commande [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) .</span><span class="sxs-lookup"><span data-stu-id="ecba5-123">To use the cmdlets, you must first sign in to your Azure account from within the PowerShell environment by using the [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span> <span data-ttu-id="ecba5-124">Si vous ne savez pas comment appeler les commandes PowerShell basées sur Resource Manager, consultez [Utilisation d’Azure PowerShell avec Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).</span><span class="sxs-lookup"><span data-stu-id="ecba5-124">If you are unfamiliar with how to call PowerShell commands that are based on Resource Manager, see [Using Azure PowerShell with Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).</span></span>

<span data-ttu-id="ecba5-125">Pour exporter votre expérience prédictive, utilisez cet [exemple de code](https://github.com/ritwik20/AzureML-WebServices).</span><span class="sxs-lookup"><span data-stu-id="ecba5-125">To export your predictive experiment, use [this sample code](https://github.com/ritwik20/AzureML-WebServices).</span></span> <span data-ttu-id="ecba5-126">Après avoir créé le fichier .exe à partir du code, vous pouvez taper :</span><span class="sxs-lookup"><span data-stu-id="ecba5-126">After you create the .exe file from the code, you can type:</span></span>

    C:\<folder>\GetWSD <experiment-url> <workspace-auth-token>

<span data-ttu-id="ecba5-127">L’exécution de l’application crée un modèle JSON de service web.</span><span class="sxs-lookup"><span data-stu-id="ecba5-127">Running the application creates a web service JSON template.</span></span> <span data-ttu-id="ecba5-128">Pour utiliser le modèle afin de déployer un service web, vous devez ajouter les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="ecba5-128">To use the template to deploy a web service, you must add the following information:</span></span>

* <span data-ttu-id="ecba5-129">Nom et clé du compte de stockage</span><span class="sxs-lookup"><span data-stu-id="ecba5-129">Storage account name and key</span></span>

    <span data-ttu-id="ecba5-130">Vous pouvez récupérer le nom et la clé du compte de stockage à partir du [portail Azure](https://portal.azure.com/) ou du [portail Azure Classic](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="ecba5-130">You can get the storage account name and key from either the [Azure portal](https://portal.azure.com/) or the [Azure classic portal](http://manage.windowsazure.com/).</span></span>
* <span data-ttu-id="ecba5-131">ID de plan d’engagement</span><span class="sxs-lookup"><span data-stu-id="ecba5-131">Commitment plan ID</span></span>

    <span data-ttu-id="ecba5-132">Vous pouvez récupérer l’ID du plan sur le portail des [services web Azure Machine Learning](https://services.azureml.net) en vous connectant et en cliquant sur le nom d’un plan.</span><span class="sxs-lookup"><span data-stu-id="ecba5-132">You can get the plan ID from the [Azure Machine Learning Web Services](https://services.azureml.net) portal by signing in and clicking a plan name.</span></span>

<span data-ttu-id="ecba5-133">Ajoutez-les au modèle JSON en tant qu’enfants du nœud *Propriétés* au même niveau que le nœud *MachineLearningWorkspace*.</span><span class="sxs-lookup"><span data-stu-id="ecba5-133">Add them to the JSON template as children of the *Properties* node at the same level as the *MachineLearningWorkspace* node.</span></span>

<span data-ttu-id="ecba5-134">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="ecba5-134">Here's an example:</span></span>

    "StorageAccount": {
            "name": "YourStorageAccountName",
            "key": "YourStorageAccountKey"
    },
    "CommitmentPlan": {
        "id": "subscriptions/YouSubscriptionID/resourceGroups/YourResourceGroupID/providers/Microsoft.MachineLearning/commitmentPlans/YourPlanName"
    }

<span data-ttu-id="ecba5-135">Consultez les articles et les exemples de code suivants pour plus de détails :</span><span class="sxs-lookup"><span data-stu-id="ecba5-135">See the following articles and sample code for additional details:</span></span>

* <span data-ttu-id="ecba5-136">[Applets de commande Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt767952.aspx) sur MSDN</span><span class="sxs-lookup"><span data-stu-id="ecba5-136">[Azure Machine Learning Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) reference on MSDN</span></span>
* <span data-ttu-id="ecba5-137">Exemple de [procédure pas à pas](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) sur GitHub</span><span class="sxs-lookup"><span data-stu-id="ecba5-137">Sample [walkthrough](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) on GitHub</span></span>

## <a name="consume-the-web-services"></a><span data-ttu-id="ecba5-138">Utiliser des services web</span><span class="sxs-lookup"><span data-stu-id="ecba5-138">Consume the web services</span></span>
### <a name="from-the-azure-machine-learning-web-services-ui-testing"></a><span data-ttu-id="ecba5-139">À partir de l’interface utilisateur des services web Azure Machine Learning (test)</span><span class="sxs-lookup"><span data-stu-id="ecba5-139">From the Azure Machine Learning Web Services UI (Testing)</span></span>
<span data-ttu-id="ecba5-140">Vous pouvez tester votre service web sur le portail de services web Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="ecba5-140">You can test your web service from the Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="ecba5-141">Cela comprend le test du service de requête-réponse (RRS) et des interfaces de service d’exécution de lots (BES).</span><span class="sxs-lookup"><span data-stu-id="ecba5-141">This includes testing the Request-Response service (RRS) and Batch Execution service (BES) interfaces.</span></span>

* [<span data-ttu-id="ecba5-142">Déployer comme un nouveau service web</span><span class="sxs-lookup"><span data-stu-id="ecba5-142">Deploy a new web service</span></span>](machine-learning-webservice-deploy-a-web-service.md)
* [<span data-ttu-id="ecba5-143">Déploiement d’un service web Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="ecba5-143">Deploy an Azure Machine Learning web service</span></span>](machine-learning-publish-a-machine-learning-web-service.md)
* [<span data-ttu-id="ecba5-144">Étape 5 du didacticiel pas à pas : Déploiement du service web Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="ecba5-144">Walkthrough Step 5: Deploy the Azure Machine Learning web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)

### <a name="from-excel"></a><span data-ttu-id="ecba5-145">À partir d’Excel</span><span class="sxs-lookup"><span data-stu-id="ecba5-145">From Excel</span></span>
<span data-ttu-id="ecba5-146">Vous pouvez télécharger un modèle Excel qui consomme le service web :</span><span class="sxs-lookup"><span data-stu-id="ecba5-146">You can download an Excel template that consumes the web service:</span></span>

* [<span data-ttu-id="ecba5-147">Utilisation d’un service web Microsoft Azure Machine Learning à partir de Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="ecba5-147">Consuming an Azure Machine Learning web service from Excel</span></span>](machine-learning-consuming-from-excel.md)
* [<span data-ttu-id="ecba5-148">Complément Excel de services web Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="ecba5-148">Excel add-in for Azure Machine Learning Web Services</span></span>](machine-learning-excel-add-in-for-web-services.md)

### <a name="from-a-rest-based-client"></a><span data-ttu-id="ecba5-149">À partir d’un client basé sur REST</span><span class="sxs-lookup"><span data-stu-id="ecba5-149">From a REST-based client</span></span>
<span data-ttu-id="ecba5-150">Les services web Azure Machine Learning sont des API RESTful.</span><span class="sxs-lookup"><span data-stu-id="ecba5-150">Azure Machine Learning Web Services are RESTful APIs.</span></span> <span data-ttu-id="ecba5-151">Vous pouvez consommer ces API à partir de différentes plateformes, notamment .NET, Python, R, Java, etc. La page **Consommer** de votre service web sur le [portail des services web Microsoft Azure Machine Learning](https://services.azureml.net) contient des exemples de code susceptibles de vous aider à démarrer.</span><span class="sxs-lookup"><span data-stu-id="ecba5-151">You can consume these APIs from various platforms, such as .NET, Python, R, Java, etc. The **Consume** page for your web service on the [Microsoft Azure Machine Learning Web Services portal](https://services.azureml.net) has sample code that can help you get started.</span></span> <span data-ttu-id="ecba5-152">Pour plus d’informations, consultez [Utilisation d’un service Web Microsoft Azure Machine Learning](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="ecba5-152">For more information, see [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>
