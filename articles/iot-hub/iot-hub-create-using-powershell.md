---
title: "Créer un IoT Hub Azure à l’aide d’une cmdlet PowerShell | Microsoft Docs"
description: "Comment utiliser une cmdlet PowerShell pour créer un IoT Hub."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 02227adeb8a9a7463506efa44ddc2977f8aae65a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-iot-hub-using-the-new-azurermiothub-cmdlet"></a><span data-ttu-id="377c2-103">Créez un IoT Hub à l’aide de la cmdlet New-AzureRmIotHub</span><span class="sxs-lookup"><span data-stu-id="377c2-103">Create an IoT hub using the New-AzureRmIotHub cmdlet</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="377c2-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="377c2-104">Introduction</span></span>

<span data-ttu-id="377c2-105">Vous pouvez utiliser les cmdlets Azure PowerShell pour créer et gérer des IoT Hubs Azure.</span><span class="sxs-lookup"><span data-stu-id="377c2-105">You can use Azure PowerShell cmdlets to create and manage Azure IoT hubs.</span></span> <span data-ttu-id="377c2-106">Ce didacticiel vous montre comment créer un IoT Hub à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="377c2-106">This tutorial shows you how to create an IoT hub with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="377c2-107">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Azure Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="377c2-107">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="377c2-108">Cet article traite de l’utilisation du modèle de déploiement Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="377c2-108">This article covers using the Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="377c2-109">Pour réaliser ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="377c2-109">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="377c2-110">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="377c2-110">An active Azure account.</span></span> <br/><span data-ttu-id="377c2-111">Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="377c2-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="377c2-112">[Applets de commande Azure PowerShell][lnk-powershell-install].</span><span class="sxs-lookup"><span data-stu-id="377c2-112">[Azure PowerShell cmdlets][lnk-powershell-install].</span></span>

## <a name="connect-to-your-azure-subscription"></a><span data-ttu-id="377c2-113">Connectez-vous à un abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="377c2-113">Connect to your Azure subscription</span></span>
<span data-ttu-id="377c2-114">Dans une invite de commandes PowerShell, entrez la commande suivante pour vous connecter à votre abonnement Azure :</span><span class="sxs-lookup"><span data-stu-id="377c2-114">In a PowerShell command prompt, enter the following command to sign in to your Azure subscription:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="377c2-115">Si vous possédez plusieurs abonnements Azure, la connexion à Azure vous donne accès à tous les abonnements Azure associés à vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="377c2-115">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="377c2-116">Utilisez la commande suivante pour répertorier les abonnements Azure que vous pouvez utiliser :</span><span class="sxs-lookup"><span data-stu-id="377c2-116">Use the following command to list the Azure subscriptions available for you to use:</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="377c2-117">Utilisez la commande suivante pour sélectionner l’abonnement que vous souhaitez utiliser afin d'exécuter les commandes pour créer votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="377c2-117">Use the following command to select subscription that you want to use to run the commands to create your IoT hub.</span></span> <span data-ttu-id="377c2-118">Vous pouvez utiliser le nom de l’abonnement ou l’ID de la sortie de la commande précédente :</span><span class="sxs-lookup"><span data-stu-id="377c2-118">You can use either the subscription name or ID from the output of the previous command:</span></span>

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

## <a name="create-resource-group"></a><span data-ttu-id="377c2-119">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="377c2-119">Create resource group</span></span>

<span data-ttu-id="377c2-120">Vous avez besoin d’un groupe de ressources pour déployer un IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="377c2-120">You need a resource group to deploy an IoT hub.</span></span> <span data-ttu-id="377c2-121">Vous pouvez utiliser un groupe de ressources existant ou en créer un.</span><span class="sxs-lookup"><span data-stu-id="377c2-121">You can use an existing resource group or create a new one.</span></span>

<span data-ttu-id="377c2-122">Vous pouvez utiliser la commande suivante pour détecter les emplacements où vous pouvez déployer un IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="377c2-122">You can use the following command to discover the locations where you can deploy an IoT hub:</span></span>

```powershell
((Get-AzureRmResourceProvider `
  -ProviderNamespace Microsoft.Devices).ResourceTypes `
  | Where-Object ResourceTypeName -eq IoTHubs).Locations
```

<span data-ttu-id="377c2-123">Pour créer un groupe de ressources pour votre IoT Hub dans l’un des emplacements pris en charge pour l’IoT Hub, utilisez la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="377c2-123">To create a resource group for your IoT hub in one of the supported locations for IoT Hub, use the following command.</span></span> <span data-ttu-id="377c2-124">Cet exemple crée un groupe de ressources appelé **MyIoTRG1** dans la région **États-Unis de l’Est** :</span><span class="sxs-lookup"><span data-stu-id="377c2-124">This example creates a resource group called **MyIoTRG1** in the **East US** region:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="create-an-iot-hub"></a><span data-ttu-id="377c2-125">Créer un hub IoT</span><span class="sxs-lookup"><span data-stu-id="377c2-125">Create an IoT hub</span></span>

<span data-ttu-id="377c2-126">Pour créer un IoT Hub dans le groupe de ressources que vous avez créé à l’étape précédente, utilisez la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="377c2-126">To create an IoT hub in the resource group you created in the previous step, use the following command.</span></span> <span data-ttu-id="377c2-127">Cet exemple crée un hub **S1** appelé **MyTestIoTHub** dans la région **États-Unis de l’Est** :</span><span class="sxs-lookup"><span data-stu-id="377c2-127">This example creates an **S1** hub called **MyTestIoTHub** in the **East US** region:</span></span>

```powershell
New-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub `
    -SkuName S1 -Units 1 `
    -Location "East US"
```

<span data-ttu-id="377c2-128">Le nom du IoT Hub doit être unique.</span><span class="sxs-lookup"><span data-stu-id="377c2-128">The name of the IoT hub must be unique.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


<span data-ttu-id="377c2-129">Vous pouvez afficher tous les IoT Hubs de votre abonnement à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="377c2-129">You can list all the IoT hubs in your subscription using the following command:</span></span>

```powershell
Get-AzureRmIotHub
```

<span data-ttu-id="377c2-130">L’exemple précédent ajoute un IoT Hub S1 Standard qui vous est facturé.</span><span class="sxs-lookup"><span data-stu-id="377c2-130">The previous example adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="377c2-131">Vous pouvez supprimer l’IoT Hub à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="377c2-131">You can delete the IoT hub using the following command:</span></span>

```powershell
Remove-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub
```

<span data-ttu-id="377c2-132">Vous pouvez également supprimer un groupe de ressources et toutes les ressources qu’il contient à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="377c2-132">Alternatively, you can remove a resource group and all the resources it contains using the following command:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name MyIoTRG1
```

## <a name="next-steps"></a><span data-ttu-id="377c2-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="377c2-133">Next steps</span></span>

<span data-ttu-id="377c2-134">Maintenant que vous avez déployé un IoT Hub à l’aide d’une cmdlet PowerShell, vous pouvez aller encore plus loin :</span><span class="sxs-lookup"><span data-stu-id="377c2-134">Now you have deployed an IoT hub using a PowerShell cmdlet, you may want to explore further:</span></span>

* <span data-ttu-id="377c2-135">Découvrez d’autres [cmdlets PowerShell pour travailler avec votre IoT Hub][lnk-iothub-cmdlets].</span><span class="sxs-lookup"><span data-stu-id="377c2-135">Discover other [PowerShell cmdlets for working with your IoT hub][lnk-iothub-cmdlets].</span></span>
* <span data-ttu-id="377c2-136">Découvrez les capacités de [l’API REST du fournisseur de ressources IoT Hub][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="377c2-136">Read about the capabilities of the [IoT Hub resource provider REST API][lnk-rest-api].</span></span>

<span data-ttu-id="377c2-137">Pour en savoir plus sur le développement pour IoT Hub, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="377c2-137">To learn more about developing for IoT Hub, see the following articles:</span></span>

* <span data-ttu-id="377c2-138">[Présentation du Kit de développement logiciel (SDK) C][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="377c2-138">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="377c2-139">[Kits de développement logiciel (SDK) Azure IoT][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="377c2-139">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="377c2-140">Pour explorer davantage les capacités de IoT Hub, consultez :</span><span class="sxs-lookup"><span data-stu-id="377c2-140">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="377c2-141">[Simulation d’un appareil avec IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="377c2-141">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-iothub-cmdlets]: https://docs.microsoft.com/powershell/module/azurerm.iothub/
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
