---
title: "Créer un IoT Hub Azure à l’aide d’un modèle (PowerShell) | Microsoft Docs"
description: "Comment utiliser un modèle Azure Resource Manager pour créer un IoT Hub avec PowerShell."
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
ms.openlocfilehash: f83fac6cffc9e58582417324a4348ca3b6220f0c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-iot-hub-using-azure-resource-manager-template-powershell"></a><span data-ttu-id="7ff86-103">Créer un IoT Hub avec un modèle Azure Resource Manager (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="7ff86-103">Create an IoT hub using Azure Resource Manager template (PowerShell)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="7ff86-104">Vous pouvez utiliser Azure Resource Manager pour créer et gérer des hubs Azure IoT de façon programmée.</span><span class="sxs-lookup"><span data-stu-id="7ff86-104">You can use Azure Resource Manager to create and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="7ff86-105">Ce didacticiel vous montre comment utiliser un modèle Azure Resource Manager pour créer un IoT Hub à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7ff86-105">This tutorial shows you how to use an Azure Resource Manager template to create an IoT hub with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="7ff86-106">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Azure Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="7ff86-106">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="7ff86-107">Cet article traite de l’utilisation du modèle de déploiement Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7ff86-107">This article covers using the Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="7ff86-108">Pour réaliser ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="7ff86-108">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="7ff86-109">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="7ff86-109">An active Azure account.</span></span> <br/><span data-ttu-id="7ff86-110">Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="7ff86-110">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="7ff86-111">[Azure PowerShell 1.0][lnk-powershell-install] ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="7ff86-111">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

> [!TIP]
> <span data-ttu-id="7ff86-112">L’article [Utilisation d’Azure PowerShell avec Azure Resource Manager][lnk-powershell-arm] fournit des informations supplémentaires sur l’utilisation de PowerShell et des modèles Resource Manager pour créer des ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="7ff86-112">The article [Using Azure PowerShell with Azure Resource Manager][lnk-powershell-arm] provides more information about how to use PowerShell and Azure Resource Manager templates to create Azure resources.</span></span>

## <a name="connect-to-your-azure-subscription"></a><span data-ttu-id="7ff86-113">Connectez-vous à un abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="7ff86-113">Connect to your Azure subscription</span></span>

<span data-ttu-id="7ff86-114">Dans une invite de commandes PowerShell, entrez la commande suivante pour vous connecter à votre abonnement Azure :</span><span class="sxs-lookup"><span data-stu-id="7ff86-114">In a PowerShell command prompt, enter the following command to sign in to your Azure subscription:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="7ff86-115">Si vous possédez plusieurs abonnements Azure, la connexion à Azure vous donne accès à tous les abonnements Azure associés à vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="7ff86-115">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="7ff86-116">Utilisez la commande suivante pour répertorier les abonnements Azure que vous pouvez utiliser :</span><span class="sxs-lookup"><span data-stu-id="7ff86-116">Use the following command to list the Azure subscriptions available for you to use:</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="7ff86-117">Utilisez la commande suivante pour sélectionner l’abonnement que vous souhaitez utiliser afin d'exécuter les commandes pour créer votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="7ff86-117">Use the following command to select subscription that you want to use to run the commands to create your IoT hub.</span></span> <span data-ttu-id="7ff86-118">Vous pouvez utiliser le nom de l’abonnement ou l’ID de la sortie de la commande précédente :</span><span class="sxs-lookup"><span data-stu-id="7ff86-118">You can use either the subscription name or ID from the output of the previous command:</span></span>

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

<span data-ttu-id="7ff86-119">Vous pouvez utiliser les commandes suivantes pour découvrir où vous pouvez déployer un IoT Hub et les versions de l'API actuellement prises en charge :</span><span class="sxs-lookup"><span data-stu-id="7ff86-119">You can use the following commands to discover where you can deploy an IoT hub and the currently supported API versions:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).Locations
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).ApiVersions
```

<span data-ttu-id="7ff86-120">Créez un groupe de ressources pour contenir votre IoT Hub avec la commande suivante dans l’un des emplacements pris en charge pour l’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="7ff86-120">Create a resource group to contain your IoT hub using the following command in one of the supported locations for IoT Hub.</span></span> <span data-ttu-id="7ff86-121">Cet exemple crée un groupe de ressources appelé **MyIoTRG1**:</span><span class="sxs-lookup"><span data-stu-id="7ff86-121">This example creates a resource group called **MyIoTRG1**:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="submit-a-template-to-create-an-iot-hub"></a><span data-ttu-id="7ff86-122">Envoyer un modèle pour créer un hub IoT</span><span class="sxs-lookup"><span data-stu-id="7ff86-122">Submit a template to create an IoT hub</span></span>

<span data-ttu-id="7ff86-123">Utilisez un modèle JSON pour créer un IoT Hub dans votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="7ff86-123">Use a JSON template to create an IoT hub in your resource group.</span></span> <span data-ttu-id="7ff86-124">Vous pouvez également utiliser un modèle Azure Resource Manager pour apporter des modifications à un IoT Hub existant.</span><span class="sxs-lookup"><span data-stu-id="7ff86-124">You can also use an Azure Resource Manager template to make changes to an existing IoT hub.</span></span>

1. <span data-ttu-id="7ff86-125">Utilisez un éditeur de texte pour créer un modèle Azure Resource Manager appelé **template.json** avec la définition de ressource suivante pour créer un IoT Hub standard.</span><span class="sxs-lookup"><span data-stu-id="7ff86-125">Use a text editor to create an Azure Resource Manager template called **template.json** with the following resource definition to create a new standard IoT hub.</span></span> <span data-ttu-id="7ff86-126">Cet exemple ajoute l’IoT Hub dans la zone **États-Unis de l’Est**, crée deux groupes de consommateurs (**cg1** et **cg2**) sur le point de terminaison compatible Event Hubs et utilise la version de l’API **2016-02-03**.</span><span class="sxs-lookup"><span data-stu-id="7ff86-126">This example adds the IoT Hub in the **East US** region, creates two consumer groups (**cg1** and **cg2**) on the Event Hub-compatible endpoint, and uses the **2016-02-03** API version.</span></span> <span data-ttu-id="7ff86-127">Ce modèle vous demande également de transmettre le nom de l’IoT Hub en tant que paramètre appelé **hubName**.</span><span class="sxs-lookup"><span data-stu-id="7ff86-127">This template also expects you to pass in the IoT hub name as a parameter called **hubName**.</span></span> <span data-ttu-id="7ff86-128">Pour obtenir la liste des emplacements qui prennent en charge IoT Hub, voir [Statut Azure][lnk-status].</span><span class="sxs-lookup"><span data-stu-id="7ff86-128">For the current list of locations that support IoT Hub see [Azure Status][lnk-status].</span></span>

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

2. <span data-ttu-id="7ff86-129">Enregistrez le fichier de modèle Azure Resource Manager sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="7ff86-129">Save the Azure Resource Manager template file on your local machine.</span></span> <span data-ttu-id="7ff86-130">Cet exemple suppose que vous l’enregistrez dans un dossier appelé **c:\templates**.</span><span class="sxs-lookup"><span data-stu-id="7ff86-130">This example assumes you save it in a folder called **c:\templates**.</span></span>

3. <span data-ttu-id="7ff86-131">Exécutez la commande suivante pour déployer votre nouvel IoT Hub, en utilisant le nom de votre IoT Hub en tant que paramètre.</span><span class="sxs-lookup"><span data-stu-id="7ff86-131">Run the following command to deploy your new IoT hub, passing the name of your IoT hub as a parameter.</span></span> <span data-ttu-id="7ff86-132">Dans cet exemple, le nom de l’IoT Hub est `abcmyiothub`.</span><span class="sxs-lookup"><span data-stu-id="7ff86-132">In this example, the name of the IoT hub is `abcmyiothub`.</span></span> <span data-ttu-id="7ff86-133">Le nom de votre IoT Hub doit être globalement unique :</span><span class="sxs-lookup"><span data-stu-id="7ff86-133">The name of your IoT hub must be globally unique:</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -ResourceGroupName MyIoTRG1 -TemplateFile C:\templates\template.json -hubName abcmyiothub
    ```
  [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

4. <span data-ttu-id="7ff86-134">La sortie affiche les clés de l’IoT Hub que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="7ff86-134">The output displays the keys for the IoT hub you created.</span></span>

5. <span data-ttu-id="7ff86-135">Pour vérifier que votre application a bien ajouté le nouvel IoT Hub, accédez au [portail Azure][lnk-azure-portal] et affichez votre liste de ressources.</span><span class="sxs-lookup"><span data-stu-id="7ff86-135">To verify your application added the new IoT hub, visit the [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="7ff86-136">Vous pouvez également utiliser l’applet de commande PowerShell **Get-AzureRmResource**.</span><span class="sxs-lookup"><span data-stu-id="7ff86-136">Alternatively, use the **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="7ff86-137">Cet exemple d’application ajoute un IoT Hub S1 Standard qui vous est facturé.</span><span class="sxs-lookup"><span data-stu-id="7ff86-137">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="7ff86-138">Lorsque vous avez terminé, vous pouvez supprimer le IoT Hub via le [portail Azure][lnk-azure-portal] ou à l’aide de l’applet de commande PowerShell **Remove-AzureRmResource**.</span><span class="sxs-lookup"><span data-stu-id="7ff86-138">You can delete the IoT hub through the [Azure portal][lnk-azure-portal] or by using the **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ff86-139">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7ff86-139">Next steps</span></span>

<span data-ttu-id="7ff86-140">Maintenant que vous avez déployé un IoT Hub à l’aide d’un modèle Azure Resource Manager avec PowerShell, vous pouvez aller encore plus loin :</span><span class="sxs-lookup"><span data-stu-id="7ff86-140">Now you have deployed an IoT hub using an Azure Resource Manager template with PowerShell, you may want to explore further:</span></span>

* <span data-ttu-id="7ff86-141">Découvrez les capacités de l’[API REST du fournisseur de ressources IoT Hub][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="7ff86-141">Read about the capabilities of the [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="7ff86-142">Pour plus d’informations sur les capacités d’Azure Resource Manager, voir [Vue d’ensemble d’Azure Resource Manager][lnk-azure-rm-overview].</span><span class="sxs-lookup"><span data-stu-id="7ff86-142">Read [Azure Resource Manager overview][lnk-azure-rm-overview] to learn more about the capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="7ff86-143">Pour en savoir plus sur le développement pour IoT Hub, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="7ff86-143">To learn more about developing for IoT Hub, see the following articles:</span></span>

* <span data-ttu-id="7ff86-144">[Présentation du Kit de développement logiciel (SDK) C][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="7ff86-144">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="7ff86-145">[Kits de développement logiciel (SDK) Azure IoT][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="7ff86-145">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="7ff86-146">Pour explorer davantage les capacités de IoT Hub, consultez :</span><span class="sxs-lookup"><span data-stu-id="7ff86-146">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="7ff86-147">[Simulation d’un appareil avec Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="7ff86-147">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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
