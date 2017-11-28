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
# <a name="configure-iot-hub-file-uploads-using-azure-cli"></a><span data-ttu-id="4e3c6-103">Configurer les chargements de fichiers IoT Hub à l’aide d’Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4e3c6-103">Configure IoT Hub file uploads using Azure CLI</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

<span data-ttu-id="4e3c6-104">toouse hello [fonctionnalité de téléchargement de fichiers dans le IoT Hub][lnk-upload], vous devez d’abord associer un compte de stockage Azure avec votre IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4e3c6-104">toouse hello [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure Storage account with your IoT hub.</span></span> <span data-ttu-id="4e3c6-105">Vous pouvez utiliser un compte de stockage existant ou en créer un nouveau.</span><span class="sxs-lookup"><span data-stu-id="4e3c6-105">You can use an existing storage account or create a new one.</span></span>

<span data-ttu-id="4e3c6-106">toocomplete ce didacticiel, vous devez hello suivant :</span><span class="sxs-lookup"><span data-stu-id="4e3c6-106">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="4e3c6-107">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="4e3c6-107">An active Azure account.</span></span> <span data-ttu-id="4e3c6-108">Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="4e3c6-108">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="4e3c6-109">[Azure CLI 2.0][lnk-CLI-install].</span><span class="sxs-lookup"><span data-stu-id="4e3c6-109">[Azure CLI 2.0][lnk-CLI-install].</span></span>
* <span data-ttu-id="4e3c6-110">Un IoT Hub Azure.</span><span class="sxs-lookup"><span data-stu-id="4e3c6-110">An Azure IoT hub.</span></span> <span data-ttu-id="4e3c6-111">Si vous n’avez pas un hub IoT, vous pouvez utiliser hello `az iot hub create` [commande] [ lnk-cli-create-iothub] toocreate un ou utilisez hello trop portail [créer un hub IoT] [lnk-portail-hub].</span><span class="sxs-lookup"><span data-stu-id="4e3c6-111">If you don't have an IoT hub, you can use hello `az iot hub create` [command][lnk-cli-create-iothub] toocreate one or use hello portal too[Create an IoT hub][lnk-portal-hub].</span></span>
* <span data-ttu-id="4e3c6-112">Un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="4e3c6-112">An Azure Storage account.</span></span> <span data-ttu-id="4e3c6-113">Si vous n’avez pas un compte de stockage Azure, vous pouvez utiliser hello [Azure CLI 2.0 - gérer les comptes de stockage] [ lnk-manage-storage] toocreate un ou utilisez hello portail trop[créer un compte de stockage] [lnk-portal-storage].</span><span class="sxs-lookup"><span data-stu-id="4e3c6-113">If you don't have an Azure Storage account, you can use hello [Azure CLI 2.0 - Manage storage accounts][lnk-manage-storage] toocreate one or use hello portal too[Create a storage account][lnk-portal-storage].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="4e3c6-114">Se connecter à votre compte Azure et le définir</span><span class="sxs-lookup"><span data-stu-id="4e3c6-114">Sign in and set your Azure account</span></span>

<span data-ttu-id="4e3c6-115">Connectez-vous à tooyour compte Azure, puis sélectionnez votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="4e3c6-115">Sign in tooyour Azure account and select your subscription.</span></span>

1. <span data-ttu-id="4e3c6-116">À l’invite de commandes hello exécuter hello [commande login][lnk-login-command]:</span><span class="sxs-lookup"><span data-stu-id="4e3c6-116">At hello command prompt, run hello [login command][lnk-login-command]:</span></span>

    ```azurecli
    az login
    ```

    <span data-ttu-id="4e3c6-117">Suivez tooauthenticate d’instructions hello à l’aide de code de hello et connectez-vous à tooyour compte Azure via un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="4e3c6-117">Follow hello instructions tooauthenticate using hello code and sign in tooyour Azure account through a web browser.</span></span>

1. <span data-ttu-id="4e3c6-118">Si vous avez plusieurs abonnements Azure, l’ouverture de session tooAzure accorde vous accédez tooall hello associé à vos informations d’identification de comptes Azure.</span><span class="sxs-lookup"><span data-stu-id="4e3c6-118">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure accounts associated with your credentials.</span></span> <span data-ttu-id="4e3c6-119">Utilisez hello suivante [toolist de commande hello comptes Azure] [ lnk-az-account-command] disponibles pour vous toouse :</span><span class="sxs-lookup"><span data-stu-id="4e3c6-119">Use hello following [command toolist hello Azure accounts][lnk-az-account-command] available for you toouse:</span></span>

    ```azurecli
    az account list
    ```

    <span data-ttu-id="4e3c6-120">Utilisez hello suivant abonnement tooselect de commande que vous souhaitez toouse toorun hello commandes toocreate votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="4e3c6-120">Use hello following command tooselect subscription that you want toouse toorun hello commands toocreate your IoT hub.</span></span> <span data-ttu-id="4e3c6-121">Vous pouvez utiliser le nom de l’abonnement hello ou ID de sortie hello de la commande précédente hello :</span><span class="sxs-lookup"><span data-stu-id="4e3c6-121">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="retrieve-your-storage-account-details"></a><span data-ttu-id="4e3c6-122">Récupérez vos détails du compte de stockage</span><span class="sxs-lookup"><span data-stu-id="4e3c6-122">Retrieve your storage account details</span></span>

<span data-ttu-id="4e3c6-123">Hello étapes suivantes supposent que vous avez créé votre compte de stockage à l’aide de hello **le Gestionnaire de ressources** modèle de déploiement et pas hello **classique** modèle de déploiement.</span><span class="sxs-lookup"><span data-stu-id="4e3c6-123">hello following steps assume that you created your storage account using hello **Resource Manager** deployment model, and not hello **Classic** deployment model.</span></span>

<span data-ttu-id="4e3c6-124">tooconfigure fichier télécharge à partir de vos appareils, vous avez besoin d’une chaîne de connexion hello pour un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="4e3c6-124">tooconfigure file uploads from your devices, you need hello connection string for an Azure storage account.</span></span> <span data-ttu-id="4e3c6-125">compte de stockage Hello doit être Bonjour même abonnement que votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="4e3c6-125">hello storage account must be in hello same subscription as your IoT hub.</span></span> <span data-ttu-id="4e3c6-126">Vous devez également le nom hello d’un conteneur d’objets blob dans le compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="4e3c6-126">You also need hello name of a blob container in hello storage account.</span></span> <span data-ttu-id="4e3c6-127">Utilisez hello suivant commande tooretrieve vos clés de compte de stockage :</span><span class="sxs-lookup"><span data-stu-id="4e3c6-127">Use hello following command tooretrieve your storage account keys:</span></span>

```azurecli
az storage account show-connection-string --name {your storage account name} --resource-group {your storage account resource group}
```

<span data-ttu-id="4e3c6-128">Prenez note de hello **connectionString** valeur.</span><span class="sxs-lookup"><span data-stu-id="4e3c6-128">Make a note of hello **connectionString** value.</span></span> <span data-ttu-id="4e3c6-129">Vous en avez besoin dans hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="4e3c6-129">You need it in hello following steps.</span></span>

<span data-ttu-id="4e3c6-130">Vous pouvez utiliser un conteneur d’objets blob existant pour les chargements de fichiers ou en créer un nouveau :</span><span class="sxs-lookup"><span data-stu-id="4e3c6-130">You can either use an existing blob container for your file uploads or create new one:</span></span>

* <span data-ttu-id="4e3c6-131">toolist hello existant conteneurs d’objets blob dans votre compte de stockage, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4e3c6-131">toolist hello existing blob containers in your storage account, use hello following command:</span></span>

    ```azurecli
    az storage container list --connection-string "{your storage account connection string}"
    ```

* <span data-ttu-id="4e3c6-132">toocreate un conteneur d’objets blob dans votre compte de stockage, hello utilisez commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4e3c6-132">toocreate a blob container in your storage account, use hello following command:</span></span>

    ```azurecli
    az storage container create --name {container name} --connection-string "{your storage account connection string}"
    ```

## <a name="file-upload"></a><span data-ttu-id="4e3c6-133">Chargement de fichiers</span><span class="sxs-lookup"><span data-stu-id="4e3c6-133">File upload</span></span>

<span data-ttu-id="4e3c6-134">Vous pouvez désormais configurer votre tooenable de hub IoT [fonctionnalité de téléchargement de fichiers] [ lnk-upload] à l’aide des informations de compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="4e3c6-134">You can now configure your IoT hub tooenable [file upload functionality][lnk-upload] using your storage account details.</span></span>

<span data-ttu-id="4e3c6-135">configuration de Hello nécessite hello valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="4e3c6-135">hello configuration requires hello following values:</span></span>

<span data-ttu-id="4e3c6-136">**Conteneur de stockage**: un conteneur d’objets blob dans un compte de stockage Azure dans votre tooassociate abonnement Azure actuel avec votre IoT hub.</span><span class="sxs-lookup"><span data-stu-id="4e3c6-136">**Storage container**: A blob container in an Azure storage account in your current Azure subscription tooassociate with your IoT hub.</span></span> <span data-ttu-id="4e3c6-137">Vous avez extrait les informations de compte de stockage nécessaires hello Bonjour précédant la section.</span><span class="sxs-lookup"><span data-stu-id="4e3c6-137">You retrieved hello necessary storage account information in hello preceding section.</span></span> <span data-ttu-id="4e3c6-138">IoT Hub génère automatiquement les URI de SAS avec le conteneur d’objets blob toothis écriture des autorisations pour les appareils toouse lorsqu’ils téléchargent des fichiers.</span><span class="sxs-lookup"><span data-stu-id="4e3c6-138">IoT Hub automatically generates SAS URIs with write permissions toothis blob container for devices toouse when they upload files.</span></span>

<span data-ttu-id="4e3c6-139">**Recevoir des notifications pour les fichiers chargés** : activez ou désactivez les notifications de chargement de fichiers.</span><span class="sxs-lookup"><span data-stu-id="4e3c6-139">**Receive notifications for uploaded files**: Enable or disable file upload notifications.</span></span>

<span data-ttu-id="4e3c6-140">**SAS TTL**: ce paramètre est hello time-to-live de hello SAS URI retourné toohello appareil par IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4e3c6-140">**SAS TTL**: This setting is hello time-to-live of hello SAS URIs returned toohello device by IoT Hub.</span></span> <span data-ttu-id="4e3c6-141">Heure de tooone la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="4e3c6-141">Set tooone hour by default.</span></span>

<span data-ttu-id="4e3c6-142">**Fichier de paramètres par défaut de durée de vie de notification**: hello time-to-live d’une notification de téléchargement de fichier avant son expiration.</span><span class="sxs-lookup"><span data-stu-id="4e3c6-142">**File notification settings default TTL**: hello time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="4e3c6-143">Valeur tooone jour par défaut.</span><span class="sxs-lookup"><span data-stu-id="4e3c6-143">Set tooone day by default.</span></span>

<span data-ttu-id="4e3c6-144">**Nombre maximal de diffusions de notification de fichiers**: hello fréquence hello IoT Hub tentatives toodeliver une notification de téléchargement de fichier.</span><span class="sxs-lookup"><span data-stu-id="4e3c6-144">**File notification maximum delivery count**: hello number of times hello IoT Hub attempts toodeliver a file upload notification.</span></span> <span data-ttu-id="4e3c6-145">Too10 la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="4e3c6-145">Set too10 by default.</span></span>

<span data-ttu-id="4e3c6-146">Hello, suivant les paramètres de téléchargement du fichier CLI d’Azure commandes hello tooconfigure de votre hub IoT, utilisez :</span><span class="sxs-lookup"><span data-stu-id="4e3c6-146">Use hello following Azure CLI commands tooconfigure hello file upload settings on your IoT hub:</span></span>

<span data-ttu-id="4e3c6-147">Dans un shell bash, utilisez :</span><span class="sxs-lookup"><span data-stu-id="4e3c6-147">In a bash shell use:</span></span>

```azurecli
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.connectionString="{your storage account connection string}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.containerName="{your storage container name}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.sasTtlAsIso8601=PT1H0M0S

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

<span data-ttu-id="4e3c6-148">À une invite de commandes Windows, utilisez :</span><span class="sxs-lookup"><span data-stu-id="4e3c6-148">At a Windows command prompt use:</span></span>

```azurecli
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.connectionString="{your storage account connection string}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.containerName="{your storage container name}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.sasTtlAsIso8601=PT1H0M0S"

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

<span data-ttu-id="4e3c6-149">Vous pouvez examiner la configuration de téléchargement de fichier hello sur votre IoT hub à l’aide de hello commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4e3c6-149">You can review hello file upload configuration on your IoT hub using hello following command:</span></span>

```azurecli
az iot hub show --name {your iot hub name}
```

## <a name="next-steps"></a><span data-ttu-id="4e3c6-150">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4e3c6-150">Next steps</span></span>

<span data-ttu-id="4e3c6-151">Pour plus d’informations sur les fonctionnalités de téléchargement de fichier hello IoT Hub, consultez [télécharger des fichiers à partir d’un appareil][lnk-upload].</span><span class="sxs-lookup"><span data-stu-id="4e3c6-151">For more information about hello file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload].</span></span>

<span data-ttu-id="4e3c6-152">Suivez ces liens de toolearn plus d’informations sur la gestion de Azure IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="4e3c6-152">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="4e3c6-153">[Gérer en bloc des appareils IoT][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="4e3c6-153">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="4e3c6-154">[Métriques d’IoT Hub][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="4e3c6-154">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="4e3c6-155">[Surveillance des opérations][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="4e3c6-155">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="4e3c6-156">toofurther Explorez les fonctionnalités de hello d’IoT Hub, consultez :</span><span class="sxs-lookup"><span data-stu-id="4e3c6-156">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="4e3c6-157">[Guide du développeur IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="4e3c6-157">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="4e3c6-158">[Simulation d’un appareil avec IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="4e3c6-158">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="4e3c6-159">[Sécuriser votre solution IoT hello d’arrière-plan][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="4e3c6-159">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

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