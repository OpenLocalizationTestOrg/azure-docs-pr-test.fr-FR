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
# <a name="create-an-iot-hub-using-azure-resource-manager-template-powershell"></a>Créer un IoT Hub avec un modèle Azure Resource Manager (PowerShell)

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

Vous pouvez utiliser le Gestionnaire de ressources Azure toocreate et gérer les hubs Azure IoT par programme. Ce didacticiel vous montre comment toouse un toocreate de modèle Azure Resource Manager un IoT hub avec PowerShell.

> [!NOTE]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Azure Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement du Gestionnaire de ressources Azure hello.

toocomplete ce didacticiel, vous devez hello suivant :

* Un compte Azure actif. <br/>Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.
* [Azure PowerShell 1.0][lnk-powershell-install] ou version ultérieure.

> [!TIP]
> article de Hello [à l’aide de Azure PowerShell avec Azure Resource Manager] [ lnk-powershell-arm] fournit plus d’informations sur les modèles de PowerShell et le Gestionnaire de ressources Azure toouse toocreate Azure ressources.

## <a name="connect-tooyour-azure-subscription"></a>Se connecter tooyour abonnement Azure

Dans une invite de commandes PowerShell, entrez hello suivant toosign de commande dans tooyour abonnement Azure :

```powershell
Login-AzureRmAccount
```

Si vous avez plusieurs abonnements Azure, l’ouverture de session tooAzure accorde vous accédez tooall hello Azure abonnements associés à vos informations d’identification. Utilisez hello toolist hello abonnements Azure disponibles pour vous toouse de commande suivante :

```powershell
Get-AzureRMSubscription
```

Utilisez hello suivant abonnement tooselect de commande que vous souhaitez toouse toorun hello commandes toocreate votre hub IoT. Vous pouvez utiliser le nom de l’abonnement hello ou ID de sortie hello de la commande précédente hello :

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

Vous pouvez utiliser hello suivant toodiscover de commandes où vous pouvez déployer un IoT hub et hello actuellement pris en charge que les versions d’API :

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).Locations
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).ApiVersions
```

Créer un toocontain de groupe de ressources votre IoT hub à l’aide de hello suivant de commande dans un des emplacements hello pris en charge pour le IoT Hub. Cet exemple crée un groupe de ressources appelé **MyIoTRG1**:

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="submit-a-template-toocreate-an-iot-hub"></a>Envoyer un toocreate de modèle un IoT hub

Utilisez un toocreate de modèle JSON un IoT hub dans votre groupe de ressources. Vous pouvez également utiliser un gestionnaire de ressources Azure modèle toomake modifications tooan existant IoT hub.

1. Utilisez un toocreate de l’éditeur de texte un modèle Azure Resource Manager nommé **template.json** avec hello suivant toocreate de définition de ressource, un hub IoT standard. Cet exemple ajoute hello IoT Hub Bonjour **États-Unis** région, crée deux groupes de consommateurs (**cg1** et **cg2**) sur hello concentrateur d’événements compatible avec le point de terminaison et utilise hello **2016-02-03** version de l’API. Ce modèle également attend vous toopass dans le nom de hub IoT hello en tant qu’un paramètre appelé **hubName**. Pour la liste actuelle des emplacements qui prennent en charge de IoT Hub hello consultez [Azure Status][lnk-status].

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

2. Enregistrez le fichier de modèle Azure Resource Manager hello sur votre ordinateur local. Cet exemple suppose que vous l’enregistrez dans un dossier appelé **c:\templates**.

3. Exécutez hello suivant commande toodeploy votre nouveau IoT hub, en passant de nom de hello de votre hub IoT en tant que paramètre. Dans cet exemple, le nom hello de hub IoT de hello est `abcmyiothub`. nom de Hello de votre IoT hub doit être globalement unique :

    ```powershell
    New-AzureRmResourceGroupDeployment -ResourceGroupName MyIoTRG1 -TemplateFile C:\templates\template.json -hubName abcmyiothub
    ```
  [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

4. sortie de Hello affiche clés hello pour hello IoT hub que vous avez créé.

5. tooverify votre application ajoutée hello nouveau hub IoT, visitez hello [portail Azure] [ lnk-azure-portal] et afficher la liste des ressources. Vous pouvez également utiliser hello **Get-AzureRmResource** applet de commande PowerShell.

> [!NOTE]
> Cet exemple d’application ajoute un IoT Hub S1 Standard qui vous est facturé. Vous pouvez supprimer hello IoT hub via hello [portail Azure] [ lnk-azure-portal] ou à l’aide de hello **Remove-AzureRmResource** applet de commande PowerShell lorsque vous avez terminé.

## <a name="next-steps"></a>Étapes suivantes

Maintenant vous avez déployé un IoT hub à l’aide d’un modèle de gestionnaire de ressources Azure avec PowerShell, vous souhaiterez peut-être tooexplore supplémentaire :

* En savoir plus sur les fonctions hello Hello [fournisseur de ressources IoT Hub API REST][lnk-rest-api].
* Lecture [vue d’ensemble du Gestionnaire de ressources Azure] [ lnk-azure-rm-overview] toolearn plus sur les fonctionnalités du Gestionnaire de ressources Azure hello.

toolearn plus sur le développement pour IoT Hub, consultez hello suivant des articles :

* [Introduction tooC SDK][lnk-c-sdk]
* [Kits de développement logiciel (SDK) Azure IoT][lnk-sdks]

toofurther Explorez les fonctionnalités de hello d’IoT Hub, consultez :

* [Simulation d’un appareil avec Azure IoT Edge][lnk-iotedge]

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
