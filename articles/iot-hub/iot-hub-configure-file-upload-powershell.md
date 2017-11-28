---
title: Utilisation de Azure PowerShell pour configurer le chargement du fichier | Microsoft Docs
description: "Comment utiliser les applets de commande Azure PowerShell pour configurer votre IoT Hub afin d’activer les téléchargements de fichiers à partir d’appareils connectés. Comprend des informations sur la configuration du compte de stockage Azure de destination."
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
ms.openlocfilehash: a72bda794b2da3e044c46249559610d06b1f1843
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="configure-iot-hub-file-uploads-using-powershell"></a><span data-ttu-id="5cd9c-104">Configurer les chargements de fichiers IoT Hub à l’aide de Powershell</span><span class="sxs-lookup"><span data-stu-id="5cd9c-104">Configure IoT Hub file uploads using PowerShell</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

<span data-ttu-id="5cd9c-105">Pour utiliser la [fonctionnalité de chargement de fichiers dans IoT Hub][lnk-upload], vous devez d’abord associer un compte de stockage Azure à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5cd9c-105">To use the [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure storage account with your IoT hub.</span></span> <span data-ttu-id="5cd9c-106">Vous pouvez utiliser un compte de stockage existant ou en créer un nouveau.</span><span class="sxs-lookup"><span data-stu-id="5cd9c-106">You can use an existing storage account or create a new one.</span></span>

<span data-ttu-id="5cd9c-107">Pour réaliser ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="5cd9c-107">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="5cd9c-108">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="5cd9c-108">An active Azure account.</span></span> <span data-ttu-id="5cd9c-109">Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="5cd9c-109">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="5cd9c-110">[Applets de commande Azure PowerShell][lnk-powershell-install].</span><span class="sxs-lookup"><span data-stu-id="5cd9c-110">[Azure PowerShell cmdlets][lnk-powershell-install].</span></span>
* <span data-ttu-id="5cd9c-111">Un IoT Hub Azure.</span><span class="sxs-lookup"><span data-stu-id="5cd9c-111">An Azure IoT hub.</span></span> <span data-ttu-id="5cd9c-112">Si vous n’avez pas de IoT Hub, vous pouvez utiliser [l’applet de commande New-AzureRmIoTHub][lnk-powershell-iothub] afin d’en créer un ou utiliser le portail pour [créer un IoT Hub][lnk-portal-hub].</span><span class="sxs-lookup"><span data-stu-id="5cd9c-112">If you don't have an IoT hub, you can use the [New-AzureRmIoTHub cmdlet][lnk-powershell-iothub] to create one or use the portal to [Create an IoT hub][lnk-portal-hub].</span></span>
* <span data-ttu-id="5cd9c-113">Un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="5cd9c-113">An Azure storage account.</span></span> <span data-ttu-id="5cd9c-114">Si vous n’avez pas de compte de stockage Azure, vous pouvez utiliser [l’applet de commande PowerShell de stockage Azure][lnk-powershell-storage] afin d’en créer un ou utiliser le portail pour [créer un compte de stockage][lnk-portal-storage].</span><span class="sxs-lookup"><span data-stu-id="5cd9c-114">If you don't have an Azure storage account, you can use the [Azure Storage PowerShell cmdlets][lnk-powershell-storage] to create one or use the portal to [Create a storage account][lnk-portal-storage].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="5cd9c-115">Se connecter à votre compte Azure et le définir</span><span class="sxs-lookup"><span data-stu-id="5cd9c-115">Sign in and set your Azure account</span></span>

<span data-ttu-id="5cd9c-116">Vous connecter à votre compte Azure et sélectionner votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="5cd9c-116">Sign in to your Azure account and select your subscription.</span></span>

1. <span data-ttu-id="5cd9c-117">À l’invite PowerShell, exécutez l’applet de commande **Login-AzureRmAccount** :</span><span class="sxs-lookup"><span data-stu-id="5cd9c-117">At the PowerShell prompt, run the **Login-AzureRmAccount** cmdlet:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="5cd9c-118">Si vous possédez plusieurs abonnements Azure, la connexion à Azure vous donne accès à tous les abonnements Azure associés à vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="5cd9c-118">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="5cd9c-119">Utilisez la commande suivante pour répertorier les abonnements Azure que vous pouvez utiliser :</span><span class="sxs-lookup"><span data-stu-id="5cd9c-119">Use the following command to list the Azure subscriptions available for you to use:</span></span>

    ```powershell
    Get-AzureRMSubscription
    ```

    <span data-ttu-id="5cd9c-120">Utilisez la commande suivante pour sélectionner l’abonnement que vous souhaitez utiliser afin d'exécuter les commandes pour gérer votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5cd9c-120">Use the following command to select subscription that you want to use to run the commands to manage your IoT hub.</span></span> <span data-ttu-id="5cd9c-121">Vous pouvez utiliser le nom de l’abonnement ou l’ID de la sortie de la commande précédente :</span><span class="sxs-lookup"><span data-stu-id="5cd9c-121">You can use either the subscription name or ID from the output of the previous command:</span></span>

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

## <a name="retrieve-your-storage-account-details"></a><span data-ttu-id="5cd9c-122">Récupérez vos détails du compte de stockage</span><span class="sxs-lookup"><span data-stu-id="5cd9c-122">Retrieve your storage account details</span></span>

<span data-ttu-id="5cd9c-123">Les étapes suivantes supposent que vous avez créé votre compte de stockage à l’aide du modèle de déploiement de **Resource Manager** et non à partir du modèle de déploiement **classique**.</span><span class="sxs-lookup"><span data-stu-id="5cd9c-123">The following steps assume that you created your storage account using the **Resource Manager** deployment model, and not the **Classic** deployment model.</span></span>

<span data-ttu-id="5cd9c-124">Pour configurer les chargements de fichiers en provenance de vos appareils, vous avez besoin de la chaîne de connexion d’un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="5cd9c-124">To configure file uploads from your devices, you need the connection string for an Azure storage account.</span></span> <span data-ttu-id="5cd9c-125">Le compte de stockage doit être situé dans le même abonnement que votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5cd9c-125">The storage account must be in the same subscription as your IoT hub.</span></span> <span data-ttu-id="5cd9c-126">Vous avez également besoin du nom d’un conteneur d’objets blob dans le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="5cd9c-126">You also need the name of a blob container in the storage account.</span></span> <span data-ttu-id="5cd9c-127">Utilisez la commande suivante pour récupérer vos clés de compte de stockage :</span><span class="sxs-lookup"><span data-stu-id="5cd9c-127">Use the following command to retrieve your storage account keys:</span></span>

```powershell
Get-AzureRmStorageAccountKey `
  -Name {your storage account name} `
  -ResourceGroupName {your storage account resource group}
```

<span data-ttu-id="5cd9c-128">Prenez note de la valeur de clé de compte de stockage **key1** .</span><span class="sxs-lookup"><span data-stu-id="5cd9c-128">Make a note of the **key1** storage account key value.</span></span> <span data-ttu-id="5cd9c-129">Vous en aurez besoin dans les étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="5cd9c-129">You need it in the following steps.</span></span>

<span data-ttu-id="5cd9c-130">Vous pouvez utiliser un conteneur d’objets blob existant pour les chargements de fichiers ou en créer un nouveau :</span><span class="sxs-lookup"><span data-stu-id="5cd9c-130">You can either use an existing blob container for your file uploads or create new one:</span></span>

* <span data-ttu-id="5cd9c-131">Pour répertorier les conteneurs d’objets blob existants dans votre compte de stockage, utilisez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="5cd9c-131">To list the existing blob containers in your storage account, use the following commands:</span></span>

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    Get-AzureStorageContainer -Context $ctx
    ```

* <span data-ttu-id="5cd9c-132">Pour créer un conteneur d’objet blob dans votre compte de stockage, utilisez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="5cd9c-132">To create a blob container in your storage account, use the following commands:</span></span>

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    New-AzureStorageContainer `
        -Name {your new container name} `
        -Permission Off `
        -Context $ctx
    ```

## <a name="configure-your-iot-hub"></a><span data-ttu-id="5cd9c-133">Configuration de votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="5cd9c-133">Configure your IoT hub</span></span>

<span data-ttu-id="5cd9c-134">Vous pouvez désormais configurer votre IoT Hub pour activer la [fonctionnalité de chargement de fichiers][lnk-upload] à l’aide des détails de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="5cd9c-134">You can now configure your IoT hub to enable [file upload functionality][lnk-upload] using your storage account details.</span></span>

<span data-ttu-id="5cd9c-135">La configuration requiert les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="5cd9c-135">The configuration requires the following values:</span></span>

<span data-ttu-id="5cd9c-136">**Conteneur de stockage** : Un conteneur d’objets blob dans un compte de stockage Azure de votre abonnement Azure actuel à associer à votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5cd9c-136">**Storage container**: A blob container in an Azure storage account in your current Azure subscription to associate with your IoT hub.</span></span> <span data-ttu-id="5cd9c-137">Vous avez extrait les informations de compte de stockage nécessaires dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="5cd9c-137">You retrieved the necessary storage account information in the preceding section.</span></span> <span data-ttu-id="5cd9c-138">IoT Hub génère automatiquement des URI SAS avec des autorisations d’écriture pour ce conteneur d’objets blob pour les appareils à utiliser lorsqu’ils chargent des fichiers.</span><span class="sxs-lookup"><span data-stu-id="5cd9c-138">IoT Hub automatically generates SAS URIs with write permissions to this blob container for devices to use when they upload files.</span></span>

<span data-ttu-id="5cd9c-139">**Recevoir des notifications pour les fichiers chargés** : activez ou désactivez les notifications de chargement de fichiers.</span><span class="sxs-lookup"><span data-stu-id="5cd9c-139">**Receive notifications for uploaded files**: Enable or disable file upload notifications.</span></span>

<span data-ttu-id="5cd9c-140">**SAS TTL**: ce paramètre est la durée de vie des URI de signature d’accès partagé renvoyés à l’appareil par IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5cd9c-140">**SAS TTL**: This setting is the time-to-live of the SAS URIs returned to the device by IoT Hub.</span></span> <span data-ttu-id="5cd9c-141">Défini sur 1 heure par défaut.</span><span class="sxs-lookup"><span data-stu-id="5cd9c-141">Set to one hour by default.</span></span>

<span data-ttu-id="5cd9c-142">**Durée de vie par défaut des paramètres de notification de fichiers**: la durée de vie d’une notification de chargement avant son expiration.</span><span class="sxs-lookup"><span data-stu-id="5cd9c-142">**File notification settings default TTL**: The time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="5cd9c-143">Défini sur 1 jour par défaut.</span><span class="sxs-lookup"><span data-stu-id="5cd9c-143">Set to one day by default.</span></span>

<span data-ttu-id="5cd9c-144">**Nombre maximal de remises de notifications de fichier**: le nombre de tentatives de remise d’une notification de chargement de fichier par l’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5cd9c-144">**File notification maximum delivery count**: The number of times the IoT Hub attempts to deliver a file upload notification.</span></span> <span data-ttu-id="5cd9c-145">Défini sur 10 par défaut.</span><span class="sxs-lookup"><span data-stu-id="5cd9c-145">Set to 10 by default.</span></span>

<span data-ttu-id="5cd9c-146">Utilisez l’applet de commande PowerShell suivant pour configurer les paramètres de chargement sur votre IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="5cd9c-146">Use the following PowerShell cmdlet to configure the file upload settings on your IoT hub:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="5cd9c-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5cd9c-147">Next steps</span></span>

<span data-ttu-id="5cd9c-148">Pour plus d’informations sur les fonctionnalités de chargement de fichiers d’IoT Hub, consultez [Chargements de fichiers avec IoT Hub][lnk-upload].</span><span class="sxs-lookup"><span data-stu-id="5cd9c-148">For more information about the file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload].</span></span>

<span data-ttu-id="5cd9c-149">Suivez ces liens pour en savoir plus sur la gestion de Azure IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="5cd9c-149">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="5cd9c-150">[Gérer en bloc des appareils IoT][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="5cd9c-150">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="5cd9c-151">[Métriques d’IoT Hub][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="5cd9c-151">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="5cd9c-152">[Surveillance des opérations][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="5cd9c-152">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="5cd9c-153">Pour explorer davantage les capacités de IoT Hub, consultez :</span><span class="sxs-lookup"><span data-stu-id="5cd9c-153">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="5cd9c-154">[Guide du développeur IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="5cd9c-154">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="5cd9c-155">[Simulation d’un appareil avec IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="5cd9c-155">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="5cd9c-156">[Sécuriser votre solution IoT de bout en bout][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="5cd9c-156">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

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