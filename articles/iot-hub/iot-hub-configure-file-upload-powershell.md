---
title: "téléchargement du fichier tooconfigure aaaUse hello Azure PowerShell | Documents Microsoft"
description: "Comment toouse hello Azure PowerShell cmdlets tooconfigure votre IoT hub tooenable téléchargements de fichiers à partir de périphériques connectés. Inclut des informations sur la configuration du compte de stockage Azure hello destination."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 915f1597-272d-4fd4-8c5b-a0ccb1df0d91
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 9dcdc41693c09cece411921b30c91d7b3db47395
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-iot-hub-file-uploads-using-powershell"></a>Configurer les chargements de fichiers IoT Hub à l’aide de Powershell

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

toouse hello [fonctionnalité de téléchargement de fichiers dans le IoT Hub][lnk-upload], vous devez d’abord associer un compte de stockage Azure avec votre IoT hub. Vous pouvez utiliser un compte de stockage existant ou en créer un nouveau.

toocomplete ce didacticiel, vous devez hello suivant :

* Un compte Azure actif. Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.
* [Applets de commande Azure PowerShell][lnk-powershell-install].
* Un IoT Hub Azure. Si vous n’avez pas un hub IoT, vous pouvez utiliser hello [applet de commande New-AzureRmIoTHub] [ lnk-powershell-iothub] toocreate un ou utilisez hello portail trop[créez un hub IoT] [ lnk-portal-hub].
* Un compte de stockage Azure. Si vous n’avez pas un compte de stockage Azure, vous pouvez utiliser hello [applets de commande PowerShell de stockage Azure] [ lnk-powershell-storage] toocreate un ou utilisez hello portail trop[créer un compte de stockage] [ lnk-portal-storage].

## <a name="sign-in-and-set-your-azure-account"></a>Se connecter à votre compte Azure et le définir

Connectez-vous à tooyour compte Azure, puis sélectionnez votre abonnement.

1. À l’invite de commandes PowerShell hello, exécutez hello **AzureRmAccount de connexion** applet de commande :

    ```powershell
    Login-AzureRmAccount
    ```

1. Si vous avez plusieurs abonnements Azure, l’ouverture de session tooAzure accorde vous accédez tooall hello Azure abonnements associés à vos informations d’identification. Utilisez hello toolist hello abonnements Azure disponibles pour vous toouse de commande suivante :

    ```powershell
    Get-AzureRMSubscription
    ```

    Utilisez hello suivant abonnement tooselect de commande que vous souhaitez toouse toorun hello commandes toomanage votre hub IoT. Vous pouvez utiliser le nom de l’abonnement hello ou ID de sortie hello de la commande précédente hello :

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

## <a name="retrieve-your-storage-account-details"></a>Récupérez vos détails du compte de stockage

Hello étapes suivantes supposent que vous avez créé votre compte de stockage à l’aide de hello **le Gestionnaire de ressources** modèle de déploiement et pas hello **classique** modèle de déploiement.

tooconfigure fichier télécharge à partir de vos appareils, vous avez besoin d’une chaîne de connexion hello pour un compte de stockage Azure. compte de stockage Hello doit être Bonjour même abonnement que votre hub IoT. Vous devez également le nom hello d’un conteneur d’objets blob dans le compte de stockage hello. Utilisez hello suivant commande tooretrieve vos clés de compte de stockage :

```powershell
Get-AzureRmStorageAccountKey `
  -Name {your storage account name} `
  -ResourceGroupName {your storage account resource group}
```

Prenez note de hello **key1** valeur de clé de compte de stockage. Vous en avez besoin dans hello comme suit.

Vous pouvez utiliser un conteneur d’objets blob existant pour les chargements de fichiers ou en créer un nouveau :

* toolist hello existant conteneurs d’objets blob dans votre compte de stockage, utilisez hello suivant de commandes :

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    Get-AzureStorageContainer -Context $ctx
    ```

* toocreate un conteneur d’objets blob dans votre compte de stockage, hello utilisation suivant de commandes :

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    New-AzureStorageContainer `
        -Name {your new container name} `
        -Permission Off `
        -Context $ctx
    ```

## <a name="configure-your-iot-hub"></a>Configuration de votre IoT Hub

Vous pouvez désormais configurer votre tooenable de hub IoT [fonctionnalité de téléchargement de fichiers] [ lnk-upload] à l’aide des informations de compte de stockage.

configuration de Hello nécessite hello valeurs suivantes :

**Conteneur de stockage**: un conteneur d’objets blob dans un compte de stockage Azure dans votre tooassociate abonnement Azure actuel avec votre IoT hub. Vous avez extrait les informations de compte de stockage nécessaires hello Bonjour précédant la section. IoT Hub génère automatiquement les URI de SAS avec le conteneur d’objets blob toothis écriture des autorisations pour les appareils toouse lorsqu’ils téléchargent des fichiers.

**Recevoir des notifications pour les fichiers chargés** : activez ou désactivez les notifications de chargement de fichiers.

**SAS TTL**: ce paramètre est hello time-to-live de hello SAS URI retourné toohello appareil par IoT Hub. Heure de tooone la valeur par défaut.

**Fichier de paramètres par défaut de durée de vie de notification**: hello time-to-live d’une notification de téléchargement de fichier avant son expiration. Valeur tooone jour par défaut.

**Nombre maximal de diffusions de notification de fichiers**: hello fréquence hello IoT Hub tentatives toodeliver une notification de téléchargement de fichier. Too10 la valeur par défaut.

Hello, suivant les paramètres de téléchargement du fichier PowerShell applet de commande hello tooconfigure de votre hub IoT, utilisez :

```powershell
Set-AzureRmIotHub `
    -ResourceGroupName "{your iot hub resource group}" `
    -Name "{your iot hub name}" `
    -FileUploadNotificationTtl "01:00:00" `
    -FileUploadSasUriTtl "01:00:00" `
    -EnableFileUploadNotifications $true `
    -FileUploadStorageConnectionString "DefaultEndpointsProtocol=https;AccountName={your storage account name};AccountKey={your storage account key};EndpointSuffix=core.windows.net" `
    -FileUploadContainerName "{your blob container name}" `
    -FileUploadNotificationMaxDeliveryCount 10
```

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur les fonctionnalités de téléchargement de fichier hello IoT Hub, consultez [télécharger des fichiers à partir d’un appareil][lnk-upload].

Suivez ces liens de toolearn plus d’informations sur la gestion de Azure IoT Hub :

* [Gérer en bloc des appareils IoT][lnk-bulk]
* [Métriques d’IoT Hub][lnk-metrics]
* [Surveillance des opérations][lnk-monitor]

toofurther Explorez les fonctionnalités de hello d’IoT Hub, consultez :

* [Guide du développeur IoT Hub][lnk-devguide]
* [Simulation d’un appareil avec IoT Edge][lnk-iotedge]
* [Sécuriser votre solution IoT hello d’arrière-plan][lnk-securing]

[lnk-upload]: iot-hub-devguide-file-upload.md

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-powershell-storage]: https://docs.microsoft.com/powershell/module/azurerm.storage/
[lnk-powershell-iothub]: https://docs.microsoft.com/powershell/module/azurerm.iothub/new-azurermiothub
[lnk-portal-hub]: iot-hub-create-through-portal.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal-storage]:../storage/common/storage-create-storage-account.md