---
title: Reformer un nouveau service web Azure Machine Learning avec PowerShell | Microsoft Docs
description: "Apprenez à reformer un modèle par programme et à mettre à jour le service web pour utiliser le modèle reformé dans Azure Machine Learning à l’aide des applets de commande PowerShell de gestion Machine Learning."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: 3953a398-6174-4d2d-8bbd-e55cf1639415
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: v-donglo
ms.openlocfilehash: 804dd59e62f38ee1878045d93211ee18e0d5bfce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="retrain-a-new-resource-manager-based-web-service-using-the-machine-learning-management-powershell-cmdlets"></a><span data-ttu-id="28cd0-103">Reformer un nouveau service web basé sur Resource Manager à l’aide des applets de commande PowerShell de gestion Machine Learning</span><span class="sxs-lookup"><span data-stu-id="28cd0-103">Retrain a New Resource Manager based web service using the Machine Learning Management PowerShell cmdlets</span></span>
<span data-ttu-id="28cd0-104">Quand vous reformez un nouveau service web, vous mettez à jour la définition de service web prédictif pour référencer le nouveau modèle formé.</span><span class="sxs-lookup"><span data-stu-id="28cd0-104">When you retrain a New web service, you update the predictive web service definition to reference the new trained model.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="28cd0-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="28cd0-105">Prerequisites</span></span>
<span data-ttu-id="28cd0-106">Vous devez configurer une expérience de formation et une expérimentation prédictive comme indiqué dans [Reformer des modèles Machine Learning par programme](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="28cd0-106">You must set up a training experiment and a predictive experiment as shown in [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="28cd0-107">L’expérience prédictive doit être déployée comme un service web Machine Learning basé sur Azure Resource Manager (nouveau).</span><span class="sxs-lookup"><span data-stu-id="28cd0-107">The predictive experiment must be deployed as an Azure Resource Manager (New) based machine learning web service.</span></span> <span data-ttu-id="28cd0-108">Pour déployer un nouveau service web, vous devez disposer d’autorisations suffisantes dans l’abonnement dans lequel déployer le service web.</span><span class="sxs-lookup"><span data-stu-id="28cd0-108">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="28cd0-109">Pour en savoir plus, consultez [Gérer un service web à l’aide du portail des services web Azure Machine Learning](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="28cd0-109">For more information, see [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="28cd0-110">Pour plus d’informations sur le déploiement de services web, consultez [Déployer un service web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="28cd0-110">For additional information on Deploying web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="28cd0-111">Ce processus requiert l’installation des applets de commande Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="28cd0-111">This process requires that you have installed the Azure Machine Learning Cmdlets.</span></span> <span data-ttu-id="28cd0-112">Pour obtenir des informations sur l’installation des applets de commande Machine Learning, consultez la référence [Azure Machine Learning Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) (Applets de commande Azure Machine Learning) sur MSDN.</span><span class="sxs-lookup"><span data-stu-id="28cd0-112">For information installing the Machine Learning cmdlets, see the [Azure Machine Learning Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) reference on MSDN.</span></span>

<span data-ttu-id="28cd0-113">Copiez les informations suivantes à partir de la sortie de reformation :</span><span class="sxs-lookup"><span data-stu-id="28cd0-113">Copied the following information from the retraining output:</span></span>

* <span data-ttu-id="28cd0-114">BaseLocation</span><span class="sxs-lookup"><span data-stu-id="28cd0-114">BaseLocation</span></span>
* <span data-ttu-id="28cd0-115">RelativeLocation</span><span class="sxs-lookup"><span data-stu-id="28cd0-115">RelativeLocation</span></span>

<span data-ttu-id="28cd0-116">Voici les étapes à suivre :</span><span class="sxs-lookup"><span data-stu-id="28cd0-116">The steps you take are:</span></span>

1. <span data-ttu-id="28cd0-117">Connectez-vous à votre compte Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="28cd0-117">Sign in to your Azure Resource Manager account.</span></span>
2. <span data-ttu-id="28cd0-118">Obtenir la définition du service web</span><span class="sxs-lookup"><span data-stu-id="28cd0-118">Get the web service definition</span></span>
3. <span data-ttu-id="28cd0-119">Exporter la définition du service web au format JSON</span><span class="sxs-lookup"><span data-stu-id="28cd0-119">Export the Web Service Definition as JSON</span></span>
4. <span data-ttu-id="28cd0-120">Mettez à jour la référence sur l’objet blob ilearner dans le JSON.</span><span class="sxs-lookup"><span data-stu-id="28cd0-120">Update the reference to the ilearner blob in the JSON.</span></span>
5. <span data-ttu-id="28cd0-121">Importer le JSON dans une définition du service web</span><span class="sxs-lookup"><span data-stu-id="28cd0-121">Import the JSON into a Web Service Definition</span></span>
6. <span data-ttu-id="28cd0-122">Mettre à jour le service web avec la nouvelle définition du service web</span><span class="sxs-lookup"><span data-stu-id="28cd0-122">Update the web service with new Web Service Definition</span></span>

## <a name="sign-in-to-your-azure-resource-manager-account"></a><span data-ttu-id="28cd0-123">Se connecter à son compte Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="28cd0-123">Sign in to your Azure Resource Manager account</span></span>
<span data-ttu-id="28cd0-124">Vous devez tout d’abord vous connecter à votre compte Azure à partir de l’environnement PowerShell à l’aide de l’applet de commande [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) .</span><span class="sxs-lookup"><span data-stu-id="28cd0-124">You must first sign in to your Azure account from within the PowerShell environment using the [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

## <a name="get-the-web-service-definition"></a><span data-ttu-id="28cd0-125">Obtenir la définition du service web</span><span class="sxs-lookup"><span data-stu-id="28cd0-125">Get the Web Service Definition</span></span>
<span data-ttu-id="28cd0-126">Ensuite, obtenez le service web en appelant l’applet de commande [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) .</span><span class="sxs-lookup"><span data-stu-id="28cd0-126">Next, get the Web Service by calling the [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span> <span data-ttu-id="28cd0-127">La définition du service web est une représentation interne du modèle formé du service web, qui n’est pas directement modifiable.</span><span class="sxs-lookup"><span data-stu-id="28cd0-127">The Web Service Definition is an internal representation of the trained model of the web service and is not directly modifiable.</span></span> <span data-ttu-id="28cd0-128">Vérifiez que vous récupérez la définition du service web pour votre expérience prédictive et non pour votre expérience de formation.</span><span class="sxs-lookup"><span data-stu-id="28cd0-128">Make sure that you are retrieving the Web Service Definition for your Predictive experiment and not your training experiment.</span></span>

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

<span data-ttu-id="28cd0-129">Pour déterminer le nom du groupe de ressources d’un service web existant, exécutez l’applet de commande Get-AzureRmMlWebService sans paramètres pour afficher les services web dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="28cd0-129">To determine the resource group name of an existing web service, run the Get-AzureRmMlWebService cmdlet without any parameters to display the web services in your subscription.</span></span> <span data-ttu-id="28cd0-130">Recherchez le service web et examinez son ID de service web.</span><span class="sxs-lookup"><span data-stu-id="28cd0-130">Locate the web service, and then look at its web service ID.</span></span> <span data-ttu-id="28cd0-131">Le nom du groupe de ressources est le quatrième élément de l’ID, juste après l’élément *resourceGroups* .</span><span class="sxs-lookup"><span data-stu-id="28cd0-131">The name of the resource group is the fourth element in the ID, just after the *resourceGroups* element.</span></span> <span data-ttu-id="28cd0-132">Dans l’exemple suivant, le nom du groupe de ressources est Default-MachineLearning-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="28cd0-132">In the following example, the resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

<span data-ttu-id="28cd0-133">Pour déterminer le nom du groupe de ressources d’un service web existant, vous pouvez également vous connecter au portail des services web Microsoft Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="28cd0-133">Alternatively, to determine the resource group name of an existing web service, log on to the Microsoft Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="28cd0-134">Sélectionnez le service web.</span><span class="sxs-lookup"><span data-stu-id="28cd0-134">Select the web service.</span></span> <span data-ttu-id="28cd0-135">Le nom de groupe de ressources est le cinquième élément de l’URL du service web, juste après l’élément *resourceGroups* .</span><span class="sxs-lookup"><span data-stu-id="28cd0-135">The resource group name is the fifth element of the URL of the web service, just after the *resourceGroups* element.</span></span> <span data-ttu-id="28cd0-136">Dans l’exemple suivant, le nom du groupe de ressources est Default-MachineLearning-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="28cd0-136">In the following example, the resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-the-web-service-definition-as-json"></a><span data-ttu-id="28cd0-137">Exporter la définition du service web au format JSON</span><span class="sxs-lookup"><span data-stu-id="28cd0-137">Export the Web Service Definition as JSON</span></span>
<span data-ttu-id="28cd0-138">Pour modifier la définition du modèle formé de manière à utiliser le modèle nouvellement formé, vous devez d’abord utiliser l’applet de commande [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) pour l’exporter vers un fichier au format JSON.</span><span class="sxs-lookup"><span data-stu-id="28cd0-138">To modify the definition to the trained model to use the newly Trained Model, you must first use the [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet to export it to a JSON format file.</span></span>

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-the-reference-to-the-ilearner-blob-in-the-json"></a><span data-ttu-id="28cd0-139">Mettez à jour la référence sur l’objet blob ilearner dans le JSON.</span><span class="sxs-lookup"><span data-stu-id="28cd0-139">Update the reference to the ilearner blob in the JSON.</span></span>
<span data-ttu-id="28cd0-140">Dans les ressources, recherchez le [modèle formé], mettez à jour la valeur *uri* dans le nœud *locationInfo* avec l’URI de l’objet blob ilearner.</span><span class="sxs-lookup"><span data-stu-id="28cd0-140">In the assets, locate the [trained model], update the *uri* value in the *locationInfo* node with the URI of the ilearner blob.</span></span> <span data-ttu-id="28cd0-141">L’URI est générée en combinant les valeurs *BaseLocation* et *RelativeLocation* de la sortie de l’appel de reformation BES.</span><span class="sxs-lookup"><span data-stu-id="28cd0-141">The URI is generated by combining the *BaseLocation* and the *RelativeLocation* from the output of the BES retraining call.</span></span> <span data-ttu-id="28cd0-142">Cela met à jour le chemin d’accès pour référencer le nouveau modèle formé.</span><span class="sxs-lookup"><span data-stu-id="28cd0-142">This updates the path to reference the new trained model.</span></span>

     "asset3": {
        "name": "Retrain Samp.le [trained model]",
        "type": "Resource",
        "locationInfo": {
          "uri": "https://mltestaccount.blob.core.windows.net/azuremlassetscontainer/baca7bca650f46218633552c0bcbba0e.ilearner"
        },
        "outputPorts": {
          "Results dataset": {
            "type": "Dataset"
          }
        }
      },

## <a name="import-the-json-into-a-web-service-definition"></a><span data-ttu-id="28cd0-143">Importer le JSON dans une définition du service web</span><span class="sxs-lookup"><span data-stu-id="28cd0-143">Import the JSON into a Web Service Definition</span></span>
<span data-ttu-id="28cd0-144">Vous devez utiliser l’applet de commande [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) pour convertir le fichier JSON modifié en une définition du service web que vous pouvez utiliser pour mettre à jour la définition de service web.</span><span class="sxs-lookup"><span data-stu-id="28cd0-144">You must use the [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet to convert the modified JSON file back into a Web Service Definition that you can use to update the Web Service Definition.</span></span>

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-the-web-service-with-new-web-service-definition"></a><span data-ttu-id="28cd0-145">Mettre à jour le service web avec la nouvelle définition du service web</span><span class="sxs-lookup"><span data-stu-id="28cd0-145">Update the web service with new Web Service Definition</span></span>
<span data-ttu-id="28cd0-146">Enfin, utilisez l’applet de commande [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) pour mettre à jour la définition de service web.</span><span class="sxs-lookup"><span data-stu-id="28cd0-146">Finally, you use [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet to update the Web Service Definition.</span></span>

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'  -ServiceUpdates $wsd

## <a name="summary"></a><span data-ttu-id="28cd0-147">Résumé</span><span class="sxs-lookup"><span data-stu-id="28cd0-147">Summary</span></span>
<span data-ttu-id="28cd0-148">À l’aide des applets de commande PowerShell Machine Learning, vous pouvez mettre à jour le modèle formé d’un service web prédictif en permettant des scénarios de type :</span><span class="sxs-lookup"><span data-stu-id="28cd0-148">Using the Machine Learning PowerShell management cmdlets, you can update the trained model of a predictive Web Service enabling scenarios such as:</span></span>

* <span data-ttu-id="28cd0-149">Nouvel apprentissage périodique d’un modèle avec de nouvelles données.</span><span class="sxs-lookup"><span data-stu-id="28cd0-149">Periodic model retraining with new data.</span></span>
* <span data-ttu-id="28cd0-150">Distribution d’un modèle auprès des clients dans le but de leur permettre d’effectuer à nouveau l’apprentissage du modèle avec leurs propres données.</span><span class="sxs-lookup"><span data-stu-id="28cd0-150">Distribution of a model to customers with the goal of letting them retrain the model using their own data.</span></span>

