---
title: "tooIoT de téléchargement de fichier aaaConfigure concentrateur à l’aide d’Azure CLI (az.py) | Documents Microsoft"
description: "Comment à l’aide de tooconfigure fileuploads tooAzure IoT Hub hello multiplateforme Azure CLI 2.0 (az.py)."
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
ms.openlocfilehash: 390113df2d96df9833b6aa383ed66805528614a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-iot-hub-file-uploads-using-azure-cli"></a>Configurer les chargements de fichiers IoT Hub à l’aide d’Azure CLI

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

toouse hello [fonctionnalité de téléchargement de fichiers dans le IoT Hub][lnk-upload], vous devez d’abord associer un compte de stockage Azure avec votre IoT hub. Vous pouvez utiliser un compte de stockage existant ou en créer un nouveau.

toocomplete ce didacticiel, vous devez hello suivant :

* Un compte Azure actif. Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.
* [Azure CLI 2.0][lnk-CLI-install].
* Un IoT Hub Azure. Si vous n’avez pas un hub IoT, vous pouvez utiliser hello `az iot hub create` [commande] [ lnk-cli-create-iothub] toocreate un ou utilisez hello trop portail [créer un hub IoT] [lnk-portail-hub].
* Un compte de stockage Azure. Si vous n’avez pas un compte de stockage Azure, vous pouvez utiliser hello [Azure CLI 2.0 - gérer les comptes de stockage] [ lnk-manage-storage] toocreate un ou utilisez hello portail trop[créer un compte de stockage] [lnk-portal-storage].

## <a name="sign-in-and-set-your-azure-account"></a>Se connecter à votre compte Azure et le définir

Connectez-vous à tooyour compte Azure, puis sélectionnez votre abonnement.

1. À l’invite de commandes hello exécuter hello [commande login][lnk-login-command]:

    ```azurecli
    az login
    ```

    Suivez tooauthenticate d’instructions hello à l’aide de code de hello et connectez-vous à tooyour compte Azure via un navigateur web.

1. Si vous avez plusieurs abonnements Azure, l’ouverture de session tooAzure accorde vous accédez tooall hello associé à vos informations d’identification de comptes Azure. Utilisez hello suivante [toolist de commande hello comptes Azure] [ lnk-az-account-command] disponibles pour vous toouse :

    ```azurecli
    az account list
    ```

    Utilisez hello suivant abonnement tooselect de commande que vous souhaitez toouse toorun hello commandes toocreate votre hub IoT. Vous pouvez utiliser le nom de l’abonnement hello ou ID de sortie hello de la commande précédente hello :

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="retrieve-your-storage-account-details"></a>Récupérez vos détails du compte de stockage

Hello étapes suivantes supposent que vous avez créé votre compte de stockage à l’aide de hello **le Gestionnaire de ressources** modèle de déploiement et pas hello **classique** modèle de déploiement.

tooconfigure fichier télécharge à partir de vos appareils, vous avez besoin d’une chaîne de connexion hello pour un compte de stockage Azure. compte de stockage Hello doit être Bonjour même abonnement que votre hub IoT. Vous devez également le nom hello d’un conteneur d’objets blob dans le compte de stockage hello. Utilisez hello suivant commande tooretrieve vos clés de compte de stockage :

```azurecli
az storage account show-connection-string --name {your storage account name} --resource-group {your storage account resource group}
```

Prenez note de hello **connectionString** valeur. Vous en avez besoin dans hello comme suit.

Vous pouvez utiliser un conteneur d’objets blob existant pour les chargements de fichiers ou en créer un nouveau :

* toolist hello existant conteneurs d’objets blob dans votre compte de stockage, utilisez hello de commande suivante :

    ```azurecli
    az storage container list --connection-string "{your storage account connection string}"
    ```

* toocreate un conteneur d’objets blob dans votre compte de stockage, hello utilisez commande suivante :

    ```azurecli
    az storage container create --name {container name} --connection-string "{your storage account connection string}"
    ```

## <a name="file-upload"></a>Chargement de fichiers

Vous pouvez désormais configurer votre tooenable de hub IoT [fonctionnalité de téléchargement de fichiers] [ lnk-upload] à l’aide des informations de compte de stockage.

configuration de Hello nécessite hello valeurs suivantes :

**Conteneur de stockage**: un conteneur d’objets blob dans un compte de stockage Azure dans votre tooassociate abonnement Azure actuel avec votre IoT hub. Vous avez extrait les informations de compte de stockage nécessaires hello Bonjour précédant la section. IoT Hub génère automatiquement les URI de SAS avec le conteneur d’objets blob toothis écriture des autorisations pour les appareils toouse lorsqu’ils téléchargent des fichiers.

**Recevoir des notifications pour les fichiers chargés** : activez ou désactivez les notifications de chargement de fichiers.

**SAS TTL**: ce paramètre est hello time-to-live de hello SAS URI retourné toohello appareil par IoT Hub. Heure de tooone la valeur par défaut.

**Fichier de paramètres par défaut de durée de vie de notification**: hello time-to-live d’une notification de téléchargement de fichier avant son expiration. Valeur tooone jour par défaut.

**Nombre maximal de diffusions de notification de fichiers**: hello fréquence hello IoT Hub tentatives toodeliver une notification de téléchargement de fichier. Too10 la valeur par défaut.

Hello, suivant les paramètres de téléchargement du fichier CLI d’Azure commandes hello tooconfigure de votre hub IoT, utilisez :

Dans un shell bash, utilisez :

```azurecli
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.connectionString="{your storage account connection string}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.containerName="{your storage container name}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.sasTtlAsIso8601=PT1H0M0S

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

À une invite de commandes Windows, utilisez :

```azurecli
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.connectionString="{your storage account connection string}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.containerName="{your storage container name}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.sasTtlAsIso8601=PT1H0M0S"

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

Vous pouvez examiner la configuration de téléchargement de fichier hello sur votre IoT hub à l’aide de hello commande suivante :

```azurecli
az iot hub show --name {your iot hub name}
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

[13]: ./media/iot-hub-configure-file-upload/file-upload-settings.png
[14]: ./media/iot-hub-configure-file-upload/file-upload-container-selection.png
[15]: ./media/iot-hub-configure-file-upload/file-upload-selected-container.png

[lnk-upload]: iot-hub-devguide-file-upload.md

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md


[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-CLI-install]: https://docs.microsoft.com/cli/azure/install-az-cli2
[lnk-login-command]: https://docs.microsoft.com/cli/azure/get-started-with-az-cli2
[lnk-az-account-command]: https://docs.microsoft.com/cli/azure/account
[lnk-az-register-command]: https://docs.microsoft.com/cli/azure/provider
[lnk-az-addcomponent-command]: https://docs.microsoft.com/cli/azure/component
[lnk-az-resource-command]: https://docs.microsoft.com/cli/azure/resource
[lnk-az-iot-command]: https://docs.microsoft.com/cli/azure/iot
[lnk-iot-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-manage-storage]:../storage/common/storage-azure-cli.md#manage-storage-accounts
[lnk-portal-storage]:../storage/common/storage-create-storage-account.md
[lnk-cli-create-iothub]: https://docs.microsoft.com/cli/azure/iot/hub#create