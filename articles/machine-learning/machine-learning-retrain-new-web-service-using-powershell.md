---
title: aaaRetrain un service web de nouveau Azure Machine Learning avec PowerShell | Documents Microsoft
description: "Découvrez comment tooprogrammatically recycler un modèle et une mise à jour hello web service toouse hello qui vient d’être formé dans Azure Machine Learning à l’aide des applets de commande PowerShell de gestion de Machine Learning hello."
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
ms.openlocfilehash: 5b77fa82cfe17f0b4e90007ef81c506ab712475b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-new-resource-manager-based-web-service-using-hello-machine-learning-management-powershell-cmdlets"></a><span data-ttu-id="6353d-103">Recycler un service web de base du nouveau gestionnaire de ressources à l’aide des applets de commande PowerShell de gestion de Machine Learning hello</span><span class="sxs-lookup"><span data-stu-id="6353d-103">Retrain a New Resource Manager based web service using hello Machine Learning Management PowerShell cmdlets</span></span>
<span data-ttu-id="6353d-104">Lorsque vous recycler un nouveau service web, vous mettez à jour hello web prédictif service définition tooreference hello nouveau modèle formé.</span><span class="sxs-lookup"><span data-stu-id="6353d-104">When you retrain a New web service, you update hello predictive web service definition tooreference hello new trained model.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="6353d-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="6353d-105">Prerequisites</span></span>
<span data-ttu-id="6353d-106">Vous devez configurer une expérience de formation et une expérimentation prédictive comme indiqué dans [Reformer des modèles Machine Learning par programme](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="6353d-106">You must set up a training experiment and a predictive experiment as shown in [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="6353d-107">expérience de prédictive Hello doit être déployé comme une gestionnaire de ressources Azure (nouveau) en fonction du service web machine learning.</span><span class="sxs-lookup"><span data-stu-id="6353d-107">hello predictive experiment must be deployed as an Azure Resource Manager (New) based machine learning web service.</span></span> <span data-ttu-id="6353d-108">toodeploy un nouveau service web, vous devez disposer des autorisations suffisantes dans hello abonnement toowhich vous déployez le service web de hello.</span><span class="sxs-lookup"><span data-stu-id="6353d-108">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="6353d-109">Pour plus d’informations, consultez [gérer un service Web à l’aide du portail de Services Web de Azure Machine Learning hello](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="6353d-109">For more information, see [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="6353d-110">Pour plus d’informations sur le déploiement de services web, consultez [Déployer un service web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="6353d-110">For additional information on Deploying web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="6353d-111">Ce processus suppose que vous avez installé hello applets de commande Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="6353d-111">This process requires that you have installed hello Azure Machine Learning Cmdlets.</span></span> <span data-ttu-id="6353d-112">Pour plus d’informations d’installation des applets de commande hello Machine Learning, consultez hello [applets de commande Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt767952.aspx) référence sur MSDN.</span><span class="sxs-lookup"><span data-stu-id="6353d-112">For information installing hello Machine Learning cmdlets, see hello [Azure Machine Learning Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) reference on MSDN.</span></span>

<span data-ttu-id="6353d-113">Hello copié informations suivantes à partir de hello réapprentissage de sortie :</span><span class="sxs-lookup"><span data-stu-id="6353d-113">Copied hello following information from hello retraining output:</span></span>

* <span data-ttu-id="6353d-114">BaseLocation</span><span class="sxs-lookup"><span data-stu-id="6353d-114">BaseLocation</span></span>
* <span data-ttu-id="6353d-115">RelativeLocation</span><span class="sxs-lookup"><span data-stu-id="6353d-115">RelativeLocation</span></span>

<span data-ttu-id="6353d-116">étapes Hello sont :</span><span class="sxs-lookup"><span data-stu-id="6353d-116">hello steps you take are:</span></span>

1. <span data-ttu-id="6353d-117">Connectez-vous tooyour compte de gestionnaire de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="6353d-117">Sign in tooyour Azure Resource Manager account.</span></span>
2. <span data-ttu-id="6353d-118">Obtenir la définition du service web hello</span><span class="sxs-lookup"><span data-stu-id="6353d-118">Get hello web service definition</span></span>
3. <span data-ttu-id="6353d-119">Exportation hello définition du Service Web en tant que JSON</span><span class="sxs-lookup"><span data-stu-id="6353d-119">Export hello Web Service Definition as JSON</span></span>
4. <span data-ttu-id="6353d-120">Mise à jour hello toohello ilearner objet blob de référence Bonjour JSON.</span><span class="sxs-lookup"><span data-stu-id="6353d-120">Update hello reference toohello ilearner blob in hello JSON.</span></span>
5. <span data-ttu-id="6353d-121">Importer des hello JSON dans une définition de Service Web</span><span class="sxs-lookup"><span data-stu-id="6353d-121">Import hello JSON into a Web Service Definition</span></span>
6. <span data-ttu-id="6353d-122">Mettre à jour de service web de hello avec la nouvelle définition de Service Web</span><span class="sxs-lookup"><span data-stu-id="6353d-122">Update hello web service with new Web Service Definition</span></span>

## <a name="sign-in-tooyour-azure-resource-manager-account"></a><span data-ttu-id="6353d-123">Connectez-vous à tooyour compte de gestionnaire de ressources Azure</span><span class="sxs-lookup"><span data-stu-id="6353d-123">Sign in tooyour Azure Resource Manager account</span></span>
<span data-ttu-id="6353d-124">Vous devez tout d’abord vous connecter tooyour compte Azure dans l’environnement PowerShell de hello à l’aide de hello [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="6353d-124">You must first sign in tooyour Azure account from within hello PowerShell environment using hello [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

## <a name="get-hello-web-service-definition"></a><span data-ttu-id="6353d-125">Obtenir hello définition du Service Web</span><span class="sxs-lookup"><span data-stu-id="6353d-125">Get hello Web Service Definition</span></span>
<span data-ttu-id="6353d-126">Ensuite, obtenez hello Web Service en appelant hello [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="6353d-126">Next, get hello Web Service by calling hello [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span> <span data-ttu-id="6353d-127">Hello définition du Service Web est une représentation interne du modèle formé de hello du service web de hello et n’est pas directement modifiable.</span><span class="sxs-lookup"><span data-stu-id="6353d-127">hello Web Service Definition is an internal representation of hello trained model of hello web service and is not directly modifiable.</span></span> <span data-ttu-id="6353d-128">Assurez-vous que vous récupérez hello définition du Service Web pour votre expérience prédictive et pas votre expérience d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="6353d-128">Make sure that you are retrieving hello Web Service Definition for your Predictive experiment and not your training experiment.</span></span>

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

<span data-ttu-id="6353d-129">nom de groupe ressource toodetermine hello d’un service web existant, exécutez hello applet de commande Get-AzureRmMlWebService sans aucun service web de paramètres toodisplay hello dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="6353d-129">toodetermine hello resource group name of an existing web service, run hello Get-AzureRmMlWebService cmdlet without any parameters toodisplay hello web services in your subscription.</span></span> <span data-ttu-id="6353d-130">Recherchez le service web de hello et observez son ID de service web.</span><span class="sxs-lookup"><span data-stu-id="6353d-130">Locate hello web service, and then look at its web service ID.</span></span> <span data-ttu-id="6353d-131">nom Hello hello du groupe de ressources est hello quatrième élément de hello ID, juste après hello *resourceGroups* élément.</span><span class="sxs-lookup"><span data-stu-id="6353d-131">hello name of hello resource group is hello fourth element in hello ID, just after hello *resourceGroups* element.</span></span> <span data-ttu-id="6353d-132">Dans l’exemple suivant de hello, nom de groupe de ressources hello est par défaut-MachineLearning-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="6353d-132">In hello following example, hello resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

<span data-ttu-id="6353d-133">Vous pouvez également toodetermine hello nom groupe de ressources d’un service web existant, le portail de Services Web de Microsoft Azure Machine Learning toohello d’ouverture de session.</span><span class="sxs-lookup"><span data-stu-id="6353d-133">Alternatively, toodetermine hello resource group name of an existing web service, log on toohello Microsoft Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="6353d-134">Sélectionnez le service web de hello.</span><span class="sxs-lookup"><span data-stu-id="6353d-134">Select hello web service.</span></span> <span data-ttu-id="6353d-135">nom de groupe de ressources Hello est hello cinquième élément de hello les URL du service web de hello, juste après hello *resourceGroups* élément.</span><span class="sxs-lookup"><span data-stu-id="6353d-135">hello resource group name is hello fifth element of hello URL of hello web service, just after hello *resourceGroups* element.</span></span> <span data-ttu-id="6353d-136">Dans l’exemple suivant de hello, nom de groupe de ressources hello est par défaut-MachineLearning-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="6353d-136">In hello following example, hello resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-hello-web-service-definition-as-json"></a><span data-ttu-id="6353d-137">Exportation hello définition du Service Web en tant que JSON</span><span class="sxs-lookup"><span data-stu-id="6353d-137">Export hello Web Service Definition as JSON</span></span>
<span data-ttu-id="6353d-138">toomodify hello définition toohello formé modèle toouse Bonjour qui vient d’être formé, vous devez d’abord utiliser hello [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) tooexport de l’applet de commande il fichier de format tooa JSON.</span><span class="sxs-lookup"><span data-stu-id="6353d-138">toomodify hello definition toohello trained model toouse hello newly Trained Model, you must first use hello [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet tooexport it tooa JSON format file.</span></span>

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-hello-reference-toohello-ilearner-blob-in-hello-json"></a><span data-ttu-id="6353d-139">Mise à jour hello toohello ilearner objet blob de référence Bonjour JSON.</span><span class="sxs-lookup"><span data-stu-id="6353d-139">Update hello reference toohello ilearner blob in hello JSON.</span></span>
<span data-ttu-id="6353d-140">Dans les ressources hello, recherchez hello [modèle formé], mise à jour hello *uri* valeur Bonjour *locationInfo* nœud avec hello URI d’objet blob de hello ilearner.</span><span class="sxs-lookup"><span data-stu-id="6353d-140">In hello assets, locate hello [trained model], update hello *uri* value in hello *locationInfo* node with hello URI of hello ilearner blob.</span></span> <span data-ttu-id="6353d-141">URI Hello est généré en combinant hello *BaseLocation* et hello *RelativeLocation* à partir de la sortie hello Hello appel de reconversion BES.</span><span class="sxs-lookup"><span data-stu-id="6353d-141">hello URI is generated by combining hello *BaseLocation* and hello *RelativeLocation* from hello output of hello BES retraining call.</span></span> <span data-ttu-id="6353d-142">Cela met à jour hello chemin d’accès tooreference hello nouveau modèle formé.</span><span class="sxs-lookup"><span data-stu-id="6353d-142">This updates hello path tooreference hello new trained model.</span></span>

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

## <a name="import-hello-json-into-a-web-service-definition"></a><span data-ttu-id="6353d-143">Importer des hello JSON dans une définition de Service Web</span><span class="sxs-lookup"><span data-stu-id="6353d-143">Import hello JSON into a Web Service Definition</span></span>
<span data-ttu-id="6353d-144">Vous devez utiliser hello [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) applet de commande tooconvert hello modifié le fichier JSON dans une définition de Service Web que vous pouvez utiliser tooupdate hello définition du Service Web.</span><span class="sxs-lookup"><span data-stu-id="6353d-144">You must use hello [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert hello modified JSON file back into a Web Service Definition that you can use tooupdate hello Web Service Definition.</span></span>

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-hello-web-service-with-new-web-service-definition"></a><span data-ttu-id="6353d-145">Mettre à jour de service web de hello avec la nouvelle définition de Service Web</span><span class="sxs-lookup"><span data-stu-id="6353d-145">Update hello web service with new Web Service Definition</span></span>
<span data-ttu-id="6353d-146">Enfin, vous utilisez [AzureRmMlWebService de mise à jour](https://msdn.microsoft.com/library/azure/mt767922.aspx) applet de commande tooupdate hello définition du Service Web.</span><span class="sxs-lookup"><span data-stu-id="6353d-146">Finally, you use [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet tooupdate hello Web Service Definition.</span></span>

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'  -ServiceUpdates $wsd

## <a name="summary"></a><span data-ttu-id="6353d-147">Résumé</span><span class="sxs-lookup"><span data-stu-id="6353d-147">Summary</span></span>
<span data-ttu-id="6353d-148">À l’aide de la gestion des applets de commande PowerShell d’apprentissage Machine hello, vous pouvez mettre à jour hello le modèle formé d’un Service Web prédictive des scénarios tels que :</span><span class="sxs-lookup"><span data-stu-id="6353d-148">Using hello Machine Learning PowerShell management cmdlets, you can update hello trained model of a predictive Web Service enabling scenarios such as:</span></span>

* <span data-ttu-id="6353d-149">Nouvel apprentissage périodique d’un modèle avec de nouvelles données.</span><span class="sxs-lookup"><span data-stu-id="6353d-149">Periodic model retraining with new data.</span></span>
* <span data-ttu-id="6353d-150">Distribution d’un modèle de toocustomers avec comme objectif hello leur permettant de former le modèle de hello à l’aide de leurs propres données.</span><span class="sxs-lookup"><span data-stu-id="6353d-150">Distribution of a model toocustomers with hello goal of letting them retrain hello model using their own data.</span></span>

