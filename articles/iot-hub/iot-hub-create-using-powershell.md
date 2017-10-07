---
title: "aaaCreate un IoT Hub de Azure à l’aide d’une applet de commande PowerShell | Documents Microsoft"
description: "Comment toouse un toocreate d’applet de commande PowerShell un IoT hub."
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
ms.openlocfilehash: 005cd8d48eb39d2e8b1bfb9ef84330d4aae4658f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-new-azurermiothub-cmdlet"></a><span data-ttu-id="fdc7a-103">Créez un IoT hub à l’aide d’applet de commande New-AzureRmIotHub de hello</span><span class="sxs-lookup"><span data-stu-id="fdc7a-103">Create an IoT hub using hello New-AzureRmIotHub cmdlet</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="fdc7a-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="fdc7a-104">Introduction</span></span>

<span data-ttu-id="fdc7a-105">Vous pouvez utiliser toocreate d’applets de commande Azure PowerShell et gérer Azure IoT hubs.</span><span class="sxs-lookup"><span data-stu-id="fdc7a-105">You can use Azure PowerShell cmdlets toocreate and manage Azure IoT hubs.</span></span> <span data-ttu-id="fdc7a-106">Ce didacticiel vous montre comment toocreate un IoT hub avec PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fdc7a-106">This tutorial shows you how toocreate an IoT hub with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="fdc7a-107">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Azure Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="fdc7a-107">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="fdc7a-108">Cet article décrit à l’aide du modèle de déploiement du Gestionnaire de ressources Azure hello.</span><span class="sxs-lookup"><span data-stu-id="fdc7a-108">This article covers using hello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="fdc7a-109">toocomplete ce didacticiel, vous devez hello suivant :</span><span class="sxs-lookup"><span data-stu-id="fdc7a-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="fdc7a-110">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="fdc7a-110">An active Azure account.</span></span> <br/><span data-ttu-id="fdc7a-111">Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="fdc7a-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="fdc7a-112">[Applets de commande Azure PowerShell][lnk-powershell-install].</span><span class="sxs-lookup"><span data-stu-id="fdc7a-112">[Azure PowerShell cmdlets][lnk-powershell-install].</span></span>

## <a name="connect-tooyour-azure-subscription"></a><span data-ttu-id="fdc7a-113">Se connecter tooyour abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="fdc7a-113">Connect tooyour Azure subscription</span></span>
<span data-ttu-id="fdc7a-114">Dans une invite de commandes PowerShell, entrez hello suivant toosign de commande dans tooyour abonnement Azure :</span><span class="sxs-lookup"><span data-stu-id="fdc7a-114">In a PowerShell command prompt, enter hello following command toosign in tooyour Azure subscription:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="fdc7a-115">Si vous avez plusieurs abonnements Azure, l’ouverture de session tooAzure accorde vous accédez tooall hello Azure abonnements associés à vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="fdc7a-115">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="fdc7a-116">Utilisez hello toolist hello abonnements Azure disponibles pour vous toouse de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="fdc7a-116">Use hello following command toolist hello Azure subscriptions available for you toouse:</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="fdc7a-117">Utilisez hello suivant abonnement tooselect de commande que vous souhaitez toouse toorun hello commandes toocreate votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="fdc7a-117">Use hello following command tooselect subscription that you want toouse toorun hello commands toocreate your IoT hub.</span></span> <span data-ttu-id="fdc7a-118">Vous pouvez utiliser le nom de l’abonnement hello ou ID de sortie hello de la commande précédente hello :</span><span class="sxs-lookup"><span data-stu-id="fdc7a-118">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

## <a name="create-resource-group"></a><span data-ttu-id="fdc7a-119">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="fdc7a-119">Create resource group</span></span>

<span data-ttu-id="fdc7a-120">Vous avez besoin d’un toodeploy de groupe de ressources un IoT hub.</span><span class="sxs-lookup"><span data-stu-id="fdc7a-120">You need a resource group toodeploy an IoT hub.</span></span> <span data-ttu-id="fdc7a-121">Vous pouvez utiliser un groupe de ressources existant ou en créer un.</span><span class="sxs-lookup"><span data-stu-id="fdc7a-121">You can use an existing resource group or create a new one.</span></span>

<span data-ttu-id="fdc7a-122">Vous pouvez utiliser hello commande toodiscover hello emplacements où vous pouvez déployer un hub IoT suivants :</span><span class="sxs-lookup"><span data-stu-id="fdc7a-122">You can use hello following command toodiscover hello locations where you can deploy an IoT hub:</span></span>

```powershell
((Get-AzureRmResourceProvider `
  -ProviderNamespace Microsoft.Devices).ResourceTypes `
  | Where-Object ResourceTypeName -eq IoTHubs).Locations
```

<span data-ttu-id="fdc7a-123">toocreate un groupe de ressources pour votre hub IoT dans un des emplacements hello pris en charge pour le IoT Hub, hello utilisez commande suivante.</span><span class="sxs-lookup"><span data-stu-id="fdc7a-123">toocreate a resource group for your IoT hub in one of hello supported locations for IoT Hub, use hello following command.</span></span> <span data-ttu-id="fdc7a-124">Cet exemple crée un groupe de ressources appelé **MyIoTRG1** Bonjour **États-Unis** région :</span><span class="sxs-lookup"><span data-stu-id="fdc7a-124">This example creates a resource group called **MyIoTRG1** in hello **East US** region:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="create-an-iot-hub"></a><span data-ttu-id="fdc7a-125">Créer un hub IoT</span><span class="sxs-lookup"><span data-stu-id="fdc7a-125">Create an IoT hub</span></span>

<span data-ttu-id="fdc7a-126">toocreate un hub IoT hello groupe de ressources créé à l’étape précédente hello, hello utilisez commande suivante.</span><span class="sxs-lookup"><span data-stu-id="fdc7a-126">toocreate an IoT hub in hello resource group you created in hello previous step, use hello following command.</span></span> <span data-ttu-id="fdc7a-127">Cet exemple crée un **S1** hub appelé **MyTestIoTHub** Bonjour **États-Unis** région :</span><span class="sxs-lookup"><span data-stu-id="fdc7a-127">This example creates an **S1** hub called **MyTestIoTHub** in hello **East US** region:</span></span>

```powershell
New-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub `
    -SkuName S1 -Units 1 `
    -Location "East US"
```

<span data-ttu-id="fdc7a-128">nom de Hello de hub IoT de hello doit être unique.</span><span class="sxs-lookup"><span data-stu-id="fdc7a-128">hello name of hello IoT hub must be unique.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


<span data-ttu-id="fdc7a-129">Vous pouvez répertorier tous les hubs IoT de hello dans votre abonnement à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="fdc7a-129">You can list all hello IoT hubs in your subscription using hello following command:</span></span>

```powershell
Get-AzureRmIotHub
```

<span data-ttu-id="fdc7a-130">Hello l’exemple précédent ajoute un IoT Hub Standard S1 pour lequel vous êtes facturé.</span><span class="sxs-lookup"><span data-stu-id="fdc7a-130">hello previous example adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="fdc7a-131">Vous pouvez supprimer hello IoT hub à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="fdc7a-131">You can delete hello IoT hub using hello following command:</span></span>

```powershell
Remove-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub
```

<span data-ttu-id="fdc7a-132">Ou bien, vous pouvez supprimer un groupe de ressources et tous les hello ressources qu’il contient à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="fdc7a-132">Alternatively, you can remove a resource group and all hello resources it contains using hello following command:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name MyIoTRG1
```

## <a name="next-steps"></a><span data-ttu-id="fdc7a-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fdc7a-133">Next steps</span></span>

<span data-ttu-id="fdc7a-134">Maintenant vous avez déployé un IoT hub à l’aide d’une applet de commande PowerShell, vous souhaiterez peut-être tooexplore supplémentaire :</span><span class="sxs-lookup"><span data-stu-id="fdc7a-134">Now you have deployed an IoT hub using a PowerShell cmdlet, you may want tooexplore further:</span></span>

* <span data-ttu-id="fdc7a-135">Découvrez d’autres [cmdlets PowerShell pour travailler avec votre IoT Hub][lnk-iothub-cmdlets].</span><span class="sxs-lookup"><span data-stu-id="fdc7a-135">Discover other [PowerShell cmdlets for working with your IoT hub][lnk-iothub-cmdlets].</span></span>
* <span data-ttu-id="fdc7a-136">En savoir plus sur les fonctions hello Hello [fournisseur de ressources IoT Hub API REST][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="fdc7a-136">Read about hello capabilities of hello [IoT Hub resource provider REST API][lnk-rest-api].</span></span>

<span data-ttu-id="fdc7a-137">toolearn plus sur le développement pour IoT Hub, consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="fdc7a-137">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="fdc7a-138">[Introduction tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="fdc7a-138">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="fdc7a-139">[Kits de développement logiciel (SDK) Azure IoT][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="fdc7a-139">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="fdc7a-140">toofurther Explorez les fonctionnalités de hello d’IoT Hub, consultez :</span><span class="sxs-lookup"><span data-stu-id="fdc7a-140">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="fdc7a-141">[Simulation d’un appareil avec IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="fdc7a-141">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-iothub-cmdlets]: https://docs.microsoft.com/powershell/module/azurerm.iothub/
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
