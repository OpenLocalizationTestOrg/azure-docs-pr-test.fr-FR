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
# <a name="create-an-iot-hub-using-hello-new-azurermiothub-cmdlet"></a>Créez un IoT hub à l’aide d’applet de commande New-AzureRmIotHub de hello

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a>Introduction

Vous pouvez utiliser toocreate d’applets de commande Azure PowerShell et gérer Azure IoT hubs. Ce didacticiel vous montre comment toocreate un IoT hub avec PowerShell.

> [!NOTE]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Azure Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement du Gestionnaire de ressources Azure hello.

toocomplete ce didacticiel, vous devez hello suivant :

* Un compte Azure actif. <br/>Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.
* [Applets de commande Azure PowerShell][lnk-powershell-install].

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

## <a name="create-resource-group"></a>Créer un groupe de ressources

Vous avez besoin d’un toodeploy de groupe de ressources un IoT hub. Vous pouvez utiliser un groupe de ressources existant ou en créer un.

Vous pouvez utiliser hello commande toodiscover hello emplacements où vous pouvez déployer un hub IoT suivants :

```powershell
((Get-AzureRmResourceProvider `
  -ProviderNamespace Microsoft.Devices).ResourceTypes `
  | Where-Object ResourceTypeName -eq IoTHubs).Locations
```

toocreate un groupe de ressources pour votre hub IoT dans un des emplacements hello pris en charge pour le IoT Hub, hello utilisez commande suivante. Cet exemple crée un groupe de ressources appelé **MyIoTRG1** Bonjour **États-Unis** région :

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="create-an-iot-hub"></a>Créer un hub IoT

toocreate un hub IoT hello groupe de ressources créé à l’étape précédente hello, hello utilisez commande suivante. Cet exemple crée un **S1** hub appelé **MyTestIoTHub** Bonjour **États-Unis** région :

```powershell
New-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub `
    -SkuName S1 -Units 1 `
    -Location "East US"
```

nom de Hello de hub IoT de hello doit être unique.

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


Vous pouvez répertorier tous les hubs IoT de hello dans votre abonnement à l’aide de hello de commande suivante :

```powershell
Get-AzureRmIotHub
```

Hello l’exemple précédent ajoute un IoT Hub Standard S1 pour lequel vous êtes facturé. Vous pouvez supprimer hello IoT hub à l’aide de hello de commande suivante :

```powershell
Remove-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub
```

Ou bien, vous pouvez supprimer un groupe de ressources et tous les hello ressources qu’il contient à l’aide de hello de commande suivante :

```powershell
Remove-AzureRmResourceGroup -Name MyIoTRG1
```

## <a name="next-steps"></a>Étapes suivantes

Maintenant vous avez déployé un IoT hub à l’aide d’une applet de commande PowerShell, vous souhaiterez peut-être tooexplore supplémentaire :

* Découvrez d’autres [cmdlets PowerShell pour travailler avec votre IoT Hub][lnk-iothub-cmdlets].
* En savoir plus sur les fonctions hello Hello [fournisseur de ressources IoT Hub API REST][lnk-rest-api].

toolearn plus sur le développement pour IoT Hub, consultez hello suivant des articles :

* [Introduction tooC SDK][lnk-c-sdk]
* [Kits de développement logiciel (SDK) Azure IoT][lnk-sdks]

toofurther Explorez les fonctionnalités de hello d’IoT Hub, consultez :

* [Simulation d’un appareil avec IoT Edge][lnk-iotedge]

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-iothub-cmdlets]: https://docs.microsoft.com/powershell/module/azurerm.iothub/
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
