---
title: "Configurer le téléchargement de fichiers vers IoT Hub à l’aide d’Azure CLI (az.py) | Microsoft Docs"
description: "Découvrez comment configurer les téléchargements de fichiers vers Azure IoT Hub à l’aide de l’interface Azure CLI 2.0 (az.py)."
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
ms.openlocfilehash: a9af26d7ebacf5513952786621aaa92f64be263b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="configure-iot-hub-file-uploads-using-azure-cli"></a><span data-ttu-id="0596b-103">Configurer les chargements de fichiers IoT Hub à l’aide d’Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0596b-103">Configure IoT Hub file uploads using Azure CLI</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

<span data-ttu-id="0596b-104">Pour utiliser la [fonctionnalité de chargement de fichiers dans IoT Hub][lnk-upload], vous devez d’abord associer un compte Stockage Azure à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0596b-104">To use the [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure Storage account with your IoT hub.</span></span> <span data-ttu-id="0596b-105">Vous pouvez utiliser un compte de stockage existant ou en créer un nouveau.</span><span class="sxs-lookup"><span data-stu-id="0596b-105">You can use an existing storage account or create a new one.</span></span>

<span data-ttu-id="0596b-106">Pour réaliser ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="0596b-106">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="0596b-107">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="0596b-107">An active Azure account.</span></span> <span data-ttu-id="0596b-108">Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="0596b-108">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="0596b-109">[Azure CLI 2.0][lnk-CLI-install].</span><span class="sxs-lookup"><span data-stu-id="0596b-109">[Azure CLI 2.0][lnk-CLI-install].</span></span>
* <span data-ttu-id="0596b-110">Un IoT Hub Azure.</span><span class="sxs-lookup"><span data-stu-id="0596b-110">An Azure IoT hub.</span></span> <span data-ttu-id="0596b-111">Si vous n’avez pas de IoT Hub, vous pouvez utiliser la `az iot hub create` [commande][lnk-cli-create-iothub] afin d’en créer un ou utiliser le portail pour [Créer un IoT Hub][lnk-portal-hub].</span><span class="sxs-lookup"><span data-stu-id="0596b-111">If you don't have an IoT hub, you can use the `az iot hub create` [command][lnk-cli-create-iothub] to create one or use the portal to [Create an IoT hub][lnk-portal-hub].</span></span>
* <span data-ttu-id="0596b-112">Un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="0596b-112">An Azure Storage account.</span></span> <span data-ttu-id="0596b-113">Si vous n’avez pas de compte de Stockage Azure, vous pouvez utiliser [Azure CLI 2.0 - Gérer les comptes de stockage][lnk-manage-storage] afin d’en créer un ou utiliser le portail pour [créer un compte de stockage][lnk-portal-storage].</span><span class="sxs-lookup"><span data-stu-id="0596b-113">If you don't have an Azure Storage account, you can use the [Azure CLI 2.0 - Manage storage accounts][lnk-manage-storage] to create one or use the portal to [Create a storage account][lnk-portal-storage].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="0596b-114">Se connecter à votre compte Azure et le définir</span><span class="sxs-lookup"><span data-stu-id="0596b-114">Sign in and set your Azure account</span></span>

<span data-ttu-id="0596b-115">Connectez-vous à votre compte Azure et sélectionnez votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="0596b-115">Sign in to your Azure account and select your subscription.</span></span>

1. <span data-ttu-id="0596b-116">Dans l’invite de commande, exécutez la [commande login][lnk-login-command]:</span><span class="sxs-lookup"><span data-stu-id="0596b-116">At the command prompt, run the [login command][lnk-login-command]:</span></span>

    ```azurecli
    az login
    ```

    <span data-ttu-id="0596b-117">Suivez les instructions pour vous authentifier à l’aide du code et vous connecter à votre compte Azure via un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="0596b-117">Follow the instructions to authenticate using the code and sign in to your Azure account through a web browser.</span></span>

1. <span data-ttu-id="0596b-118">Si vous possédez plusieurs abonnements Azure, la connexion à Azure vous donne accès à tous les abonnements Azure associés à vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="0596b-118">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure accounts associated with your credentials.</span></span> <span data-ttu-id="0596b-119">Utilisez la [commande suivante pour répertorier les comptes Azure][lnk-az-account-command] que vous pouvez utiliser :</span><span class="sxs-lookup"><span data-stu-id="0596b-119">Use the following [command to list the Azure accounts][lnk-az-account-command] available for you to use:</span></span>

    ```azurecli
    az account list
    ```

    <span data-ttu-id="0596b-120">Utilisez la commande suivante pour sélectionner l’abonnement que vous souhaitez utiliser afin d'exécuter les commandes pour créer votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0596b-120">Use the following command to select subscription that you want to use to run the commands to create your IoT hub.</span></span> <span data-ttu-id="0596b-121">Vous pouvez utiliser le nom de l’abonnement ou l’ID de la sortie de la commande précédente :</span><span class="sxs-lookup"><span data-stu-id="0596b-121">You can use either the subscription name or ID from the output of the previous command:</span></span>

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="retrieve-your-storage-account-details"></a><span data-ttu-id="0596b-122">Récupérez vos détails du compte de stockage</span><span class="sxs-lookup"><span data-stu-id="0596b-122">Retrieve your storage account details</span></span>

<span data-ttu-id="0596b-123">Les étapes suivantes supposent que vous avez créé votre compte de stockage à l’aide du modèle de déploiement de **Resource Manager** et non à partir du modèle de déploiement **classique**.</span><span class="sxs-lookup"><span data-stu-id="0596b-123">The following steps assume that you created your storage account using the **Resource Manager** deployment model, and not the **Classic** deployment model.</span></span>

<span data-ttu-id="0596b-124">Pour configurer les chargements de fichiers en provenance de vos appareils, vous avez besoin de la chaîne de connexion d’un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="0596b-124">To configure file uploads from your devices, you need the connection string for an Azure storage account.</span></span> <span data-ttu-id="0596b-125">Le compte de stockage doit être situé dans le même abonnement que votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0596b-125">The storage account must be in the same subscription as your IoT hub.</span></span> <span data-ttu-id="0596b-126">Vous avez également besoin du nom d’un conteneur d’objets blob dans le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="0596b-126">You also need the name of a blob container in the storage account.</span></span> <span data-ttu-id="0596b-127">Utilisez la commande suivante pour récupérer vos clés de compte de stockage :</span><span class="sxs-lookup"><span data-stu-id="0596b-127">Use the following command to retrieve your storage account keys:</span></span>

```azurecli
az storage account show-connection-string --name {your storage account name} --resource-group {your storage account resource group}
```

<span data-ttu-id="0596b-128">Notez le nom de la valeur **connectionString**.</span><span class="sxs-lookup"><span data-stu-id="0596b-128">Make a note of the **connectionString** value.</span></span> <span data-ttu-id="0596b-129">Vous en aurez besoin dans les étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="0596b-129">You need it in the following steps.</span></span>

<span data-ttu-id="0596b-130">Vous pouvez utiliser un conteneur d’objets blob existant pour les chargements de fichiers ou en créer un nouveau :</span><span class="sxs-lookup"><span data-stu-id="0596b-130">You can either use an existing blob container for your file uploads or create new one:</span></span>

* <span data-ttu-id="0596b-131">Pour répertorier les conteneurs d’objets blob existants dans votre compte de stockage, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="0596b-131">To list the existing blob containers in your storage account, use the following command:</span></span>

    ```azurecli
    az storage container list --connection-string "{your storage account connection string}"
    ```

* <span data-ttu-id="0596b-132">Pour créer un conteneur d’objet blob dans votre compte de stockage, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="0596b-132">To create a blob container in your storage account, use the following command:</span></span>

    ```azurecli
    az storage container create --name {container name} --connection-string "{your storage account connection string}"
    ```

## <a name="file-upload"></a><span data-ttu-id="0596b-133">Chargement de fichiers</span><span class="sxs-lookup"><span data-stu-id="0596b-133">File upload</span></span>

<span data-ttu-id="0596b-134">Vous pouvez désormais configurer votre IoT Hub pour activer la [fonctionnalité de chargement de fichiers][lnk-upload] à l’aide des détails de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="0596b-134">You can now configure your IoT hub to enable [file upload functionality][lnk-upload] using your storage account details.</span></span>

<span data-ttu-id="0596b-135">La configuration requiert les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="0596b-135">The configuration requires the following values:</span></span>

<span data-ttu-id="0596b-136">**Conteneur de stockage** : Un conteneur d’objets blob dans un compte de stockage Azure de votre abonnement Azure actuel à associer à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0596b-136">**Storage container**: A blob container in an Azure storage account in your current Azure subscription to associate with your IoT hub.</span></span> <span data-ttu-id="0596b-137">Vous avez extrait les informations de compte de stockage nécessaires dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="0596b-137">You retrieved the necessary storage account information in the preceding section.</span></span> <span data-ttu-id="0596b-138">IoT Hub génère automatiquement des URI SAS avec des autorisations d’écriture pour ce conteneur d’objets blob pour les appareils à utiliser lorsqu’ils chargent des fichiers.</span><span class="sxs-lookup"><span data-stu-id="0596b-138">IoT Hub automatically generates SAS URIs with write permissions to this blob container for devices to use when they upload files.</span></span>

<span data-ttu-id="0596b-139">**Recevoir des notifications pour les fichiers chargés** : activez ou désactivez les notifications de chargement de fichiers.</span><span class="sxs-lookup"><span data-stu-id="0596b-139">**Receive notifications for uploaded files**: Enable or disable file upload notifications.</span></span>

<span data-ttu-id="0596b-140">**SAS TTL**: ce paramètre est la durée de vie des URI de signature d’accès partagé renvoyés à l’appareil par IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0596b-140">**SAS TTL**: This setting is the time-to-live of the SAS URIs returned to the device by IoT Hub.</span></span> <span data-ttu-id="0596b-141">Défini sur 1 heure par défaut.</span><span class="sxs-lookup"><span data-stu-id="0596b-141">Set to one hour by default.</span></span>

<span data-ttu-id="0596b-142">**Durée de vie par défaut des paramètres de notification de fichiers**: la durée de vie d’une notification de chargement avant son expiration.</span><span class="sxs-lookup"><span data-stu-id="0596b-142">**File notification settings default TTL**: The time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="0596b-143">Défini sur 1 jour par défaut.</span><span class="sxs-lookup"><span data-stu-id="0596b-143">Set to one day by default.</span></span>

<span data-ttu-id="0596b-144">**Nombre maximal de remises de notifications de fichier**: le nombre de tentatives de remise d’une notification de chargement de fichier par l’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0596b-144">**File notification maximum delivery count**: The number of times the IoT Hub attempts to deliver a file upload notification.</span></span> <span data-ttu-id="0596b-145">Défini sur 10 par défaut.</span><span class="sxs-lookup"><span data-stu-id="0596b-145">Set to 10 by default.</span></span>

<span data-ttu-id="0596b-146">Utilisez les commandes Azure CLI suivantes pour configurer les paramètres de chargement sur votre IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="0596b-146">Use the following Azure CLI commands to configure the file upload settings on your IoT hub:</span></span>

<span data-ttu-id="0596b-147">Dans un shell bash, utilisez :</span><span class="sxs-lookup"><span data-stu-id="0596b-147">In a bash shell use:</span></span>

```azurecli
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.connectionString="{your storage account connection string}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.containerName="{your storage container name}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.sasTtlAsIso8601=PT1H0M0S

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

<span data-ttu-id="0596b-148">À une invite de commandes Windows, utilisez :</span><span class="sxs-lookup"><span data-stu-id="0596b-148">At a Windows command prompt use:</span></span>

```azurecli
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.connectionString="{your storage account connection string}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.containerName="{your storage container name}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.sasTtlAsIso8601=PT1H0M0S"

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

<span data-ttu-id="0596b-149">Vous pouvez consulter le fichier de configuration de téléchargement sur votre IoT Hub à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="0596b-149">You can review the file upload configuration on your IoT hub using the following command:</span></span>

```azurecli
az iot hub show --name {your iot hub name}
```

## <a name="next-steps"></a><span data-ttu-id="0596b-150">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0596b-150">Next steps</span></span>

<span data-ttu-id="0596b-151">Pour plus d’informations sur les fonctionnalités de chargement de fichiers d’IoT Hub, consultez [Chargements de fichiers avec IoT Hub][lnk-upload].</span><span class="sxs-lookup"><span data-stu-id="0596b-151">For more information about the file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload].</span></span>

<span data-ttu-id="0596b-152">Suivez ces liens pour en savoir plus sur la gestion de Azure IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="0596b-152">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="0596b-153">[Gérer en bloc des appareils IoT][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="0596b-153">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="0596b-154">[Métriques d’IoT Hub][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="0596b-154">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="0596b-155">[Surveillance des opérations][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="0596b-155">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="0596b-156">Pour explorer davantage les capacités de IoT Hub, consultez :</span><span class="sxs-lookup"><span data-stu-id="0596b-156">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="0596b-157">[Guide du développeur IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="0596b-157">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="0596b-158">[Simulation d’un appareil avec IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="0596b-158">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="0596b-159">[Sécuriser votre solution IoT de bout en bout][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="0596b-159">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

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