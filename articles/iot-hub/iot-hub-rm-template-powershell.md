---
title: "aaaCreate un IoT Hub de Azure à l’aide d’un modèle (PowerShell) | Documents Microsoft"
description: "Comment toouse un toocreate de modèle Azure Resource Manager un IoT Hub avec PowerShell."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 7eade855-c289-4ffb-b5ef-02be8c5f670f
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: e98ff5e898200cd727b9326fb3df393e43b021e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-azure-resource-manager-template-powershell"></a><span data-ttu-id="b702e-103">Créer un IoT Hub avec un modèle Azure Resource Manager (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="b702e-103">Create an IoT hub using Azure Resource Manager template (PowerShell)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="b702e-104">Vous pouvez utiliser le Gestionnaire de ressources Azure toocreate et gérer les hubs Azure IoT par programme.</span><span class="sxs-lookup"><span data-stu-id="b702e-104">You can use Azure Resource Manager toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="b702e-105">Ce didacticiel vous montre comment toouse un toocreate de modèle Azure Resource Manager un IoT hub avec PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b702e-105">This tutorial shows you how toouse an Azure Resource Manager template toocreate an IoT hub with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="b702e-106">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Azure Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="b702e-106">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="b702e-107">Cet article décrit à l’aide du modèle de déploiement du Gestionnaire de ressources Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b702e-107">This article covers using hello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="b702e-108">toocomplete ce didacticiel, vous devez hello suivant :</span><span class="sxs-lookup"><span data-stu-id="b702e-108">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="b702e-109">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="b702e-109">An active Azure account.</span></span> <br/><span data-ttu-id="b702e-110">Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="b702e-110">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="b702e-111">[Azure PowerShell 1.0][lnk-powershell-install] ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="b702e-111">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

> [!TIP]
> <span data-ttu-id="b702e-112">article de Hello [à l’aide de Azure PowerShell avec Azure Resource Manager] [ lnk-powershell-arm] fournit plus d’informations sur les modèles de PowerShell et le Gestionnaire de ressources Azure toouse toocreate Azure ressources.</span><span class="sxs-lookup"><span data-stu-id="b702e-112">hello article [Using Azure PowerShell with Azure Resource Manager][lnk-powershell-arm] provides more information about how toouse PowerShell and Azure Resource Manager templates toocreate Azure resources.</span></span>

## <a name="connect-tooyour-azure-subscription"></a><span data-ttu-id="b702e-113">Se connecter tooyour abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="b702e-113">Connect tooyour Azure subscription</span></span>

<span data-ttu-id="b702e-114">Dans une invite de commandes PowerShell, entrez hello suivant toosign de commande dans tooyour abonnement Azure :</span><span class="sxs-lookup"><span data-stu-id="b702e-114">In a PowerShell command prompt, enter hello following command toosign in tooyour Azure subscription:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="b702e-115">Si vous avez plusieurs abonnements Azure, l’ouverture de session tooAzure accorde vous accédez tooall hello Azure abonnements associés à vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="b702e-115">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="b702e-116">Utilisez hello toolist hello abonnements Azure disponibles pour vous toouse de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b702e-116">Use hello following command toolist hello Azure subscriptions available for you toouse:</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="b702e-117">Utilisez hello suivant abonnement tooselect de commande que vous souhaitez toouse toorun hello commandes toocreate votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="b702e-117">Use hello following command tooselect subscription that you want toouse toorun hello commands toocreate your IoT hub.</span></span> <span data-ttu-id="b702e-118">Vous pouvez utiliser le nom de l’abonnement hello ou ID de sortie hello de la commande précédente hello :</span><span class="sxs-lookup"><span data-stu-id="b702e-118">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

<span data-ttu-id="b702e-119">Vous pouvez utiliser hello suivant toodiscover de commandes où vous pouvez déployer un IoT hub et hello actuellement pris en charge que les versions d’API :</span><span class="sxs-lookup"><span data-stu-id="b702e-119">You can use hello following commands toodiscover where you can deploy an IoT hub and hello currently supported API versions:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).Locations
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).ApiVersions
```

<span data-ttu-id="b702e-120">Créer un toocontain de groupe de ressources votre IoT hub à l’aide de hello suivant de commande dans un des emplacements hello pris en charge pour le IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b702e-120">Create a resource group toocontain your IoT hub using hello following command in one of hello supported locations for IoT Hub.</span></span> <span data-ttu-id="b702e-121">Cet exemple crée un groupe de ressources appelé **MyIoTRG1**:</span><span class="sxs-lookup"><span data-stu-id="b702e-121">This example creates a resource group called **MyIoTRG1**:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="submit-a-template-toocreate-an-iot-hub"></a><span data-ttu-id="b702e-122">Envoyer un toocreate de modèle un IoT hub</span><span class="sxs-lookup"><span data-stu-id="b702e-122">Submit a template toocreate an IoT hub</span></span>

<span data-ttu-id="b702e-123">Utilisez un toocreate de modèle JSON un IoT hub dans votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="b702e-123">Use a JSON template toocreate an IoT hub in your resource group.</span></span> <span data-ttu-id="b702e-124">Vous pouvez également utiliser un gestionnaire de ressources Azure modèle toomake modifications tooan existant IoT hub.</span><span class="sxs-lookup"><span data-stu-id="b702e-124">You can also use an Azure Resource Manager template toomake changes tooan existing IoT hub.</span></span>

1. <span data-ttu-id="b702e-125">Utilisez un toocreate de l’éditeur de texte un modèle Azure Resource Manager nommé **template.json** avec hello suivant toocreate de définition de ressource, un hub IoT standard.</span><span class="sxs-lookup"><span data-stu-id="b702e-125">Use a text editor toocreate an Azure Resource Manager template called **template.json** with hello following resource definition toocreate a new standard IoT hub.</span></span> <span data-ttu-id="b702e-126">Cet exemple ajoute hello IoT Hub Bonjour **États-Unis** région, crée deux groupes de consommateurs (**cg1** et **cg2**) sur hello concentrateur d’événements compatible avec le point de terminaison et utilise hello **2016-02-03** version de l’API.</span><span class="sxs-lookup"><span data-stu-id="b702e-126">This example adds hello IoT Hub in hello **East US** region, creates two consumer groups (**cg1** and **cg2**) on hello Event Hub-compatible endpoint, and uses hello **2016-02-03** API version.</span></span> <span data-ttu-id="b702e-127">Ce modèle également attend vous toopass dans le nom de hub IoT hello en tant qu’un paramètre appelé **hubName**.</span><span class="sxs-lookup"><span data-stu-id="b702e-127">This template also expects you toopass in hello IoT hub name as a parameter called **hubName**.</span></span> <span data-ttu-id="b702e-128">Pour la liste actuelle des emplacements qui prennent en charge de IoT Hub hello consultez [Azure Status][lnk-status].</span><span class="sxs-lookup"><span data-stu-id="b702e-128">For hello current list of locations that support IoT Hub see [Azure Status][lnk-status].</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "hubName": {
          "type": "string"
        }
      },
      "resources": [
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs",
        "name": "[parameters('hubName')]",
        "location": "East US",
        "sku": {
          "name": "S1",
          "tier": "Standard",
          "capacity": 1
        },
        "properties": {
          "location": "East US"
        }
      },
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs/eventhubEndpoints/ConsumerGroups",
        "name": "[concat(parameters('hubName'), '/events/cg1')]",
        "dependsOn": [
          "[concat('Microsoft.Devices/Iothubs/', parameters('hubName'))]"
        ]
      },
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs/eventhubEndpoints/ConsumerGroups",
        "name": "[concat(parameters('hubName'), '/events/cg2')]",
        "dependsOn": [
          "[concat('Microsoft.Devices/Iothubs/', parameters('hubName'))]"
        ]
      }
      ],
      "outputs": {
        "hubKeys": {
          "value": "[listKeys(resourceId('Microsoft.Devices/IotHubs', parameters('hubName')), '2016-02-03')]",
          "type": "object"
        }
      }
    }
    ```

2. <span data-ttu-id="b702e-129">Enregistrez le fichier de modèle Azure Resource Manager hello sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="b702e-129">Save hello Azure Resource Manager template file on your local machine.</span></span> <span data-ttu-id="b702e-130">Cet exemple suppose que vous l’enregistrez dans un dossier appelé **c:\templates**.</span><span class="sxs-lookup"><span data-stu-id="b702e-130">This example assumes you save it in a folder called **c:\templates**.</span></span>

3. <span data-ttu-id="b702e-131">Exécutez hello suivant commande toodeploy votre nouveau IoT hub, en passant de nom de hello de votre hub IoT en tant que paramètre.</span><span class="sxs-lookup"><span data-stu-id="b702e-131">Run hello following command toodeploy your new IoT hub, passing hello name of your IoT hub as a parameter.</span></span> <span data-ttu-id="b702e-132">Dans cet exemple, le nom hello de hub IoT de hello est `abcmyiothub`.</span><span class="sxs-lookup"><span data-stu-id="b702e-132">In this example, hello name of hello IoT hub is `abcmyiothub`.</span></span> <span data-ttu-id="b702e-133">nom de Hello de votre IoT hub doit être globalement unique :</span><span class="sxs-lookup"><span data-stu-id="b702e-133">hello name of your IoT hub must be globally unique:</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -ResourceGroupName MyIoTRG1 -TemplateFile C:\templates\template.json -hubName abcmyiothub
    ```
  [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

4. <span data-ttu-id="b702e-134">sortie de Hello affiche clés hello pour hello IoT hub que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="b702e-134">hello output displays hello keys for hello IoT hub you created.</span></span>

5. <span data-ttu-id="b702e-135">tooverify votre application ajoutée hello nouveau hub IoT, visitez hello [portail Azure] [ lnk-azure-portal] et afficher la liste des ressources.</span><span class="sxs-lookup"><span data-stu-id="b702e-135">tooverify your application added hello new IoT hub, visit hello [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="b702e-136">Vous pouvez également utiliser hello **Get-AzureRmResource** applet de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b702e-136">Alternatively, use hello **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="b702e-137">Cet exemple d’application ajoute un IoT Hub S1 Standard qui vous est facturé.</span><span class="sxs-lookup"><span data-stu-id="b702e-137">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="b702e-138">Vous pouvez supprimer hello IoT hub via hello [portail Azure] [ lnk-azure-portal] ou à l’aide de hello **Remove-AzureRmResource** applet de commande PowerShell lorsque vous avez terminé.</span><span class="sxs-lookup"><span data-stu-id="b702e-138">You can delete hello IoT hub through hello [Azure portal][lnk-azure-portal] or by using hello **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b702e-139">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b702e-139">Next steps</span></span>

<span data-ttu-id="b702e-140">Maintenant vous avez déployé un IoT hub à l’aide d’un modèle de gestionnaire de ressources Azure avec PowerShell, vous souhaiterez peut-être tooexplore supplémentaire :</span><span class="sxs-lookup"><span data-stu-id="b702e-140">Now you have deployed an IoT hub using an Azure Resource Manager template with PowerShell, you may want tooexplore further:</span></span>

* <span data-ttu-id="b702e-141">En savoir plus sur les fonctions hello Hello [fournisseur de ressources IoT Hub API REST][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="b702e-141">Read about hello capabilities of hello [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="b702e-142">Lecture [vue d’ensemble du Gestionnaire de ressources Azure] [ lnk-azure-rm-overview] toolearn plus sur les fonctionnalités du Gestionnaire de ressources Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b702e-142">Read [Azure Resource Manager overview][lnk-azure-rm-overview] toolearn more about hello capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="b702e-143">toolearn plus sur le développement pour IoT Hub, consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="b702e-143">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="b702e-144">[Introduction tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="b702e-144">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="b702e-145">[Kits de développement logiciel (SDK) Azure IoT][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="b702e-145">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="b702e-146">toofurther Explorez les fonctionnalités de hello d’IoT Hub, consultez :</span><span class="sxs-lookup"><span data-stu-id="b702e-146">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="b702e-147">[Simulation d’un appareil avec Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="b702e-147">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-powershell-install]: /powershell/azure/install-azurerm-ps
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-azure-rm-overview]: ../azure-resource-manager/resource-group-overview.md
[lnk-powershell-arm]: ../azure-resource-manager/powershell-azure-resource-manager.md

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
