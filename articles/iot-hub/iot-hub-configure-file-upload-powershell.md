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
# <a name="configure-iot-hub-file-uploads-using-powershell"></a><span data-ttu-id="101ab-104">Configurer les chargements de fichiers IoT Hub à l’aide de Powershell</span><span class="sxs-lookup"><span data-stu-id="101ab-104">Configure IoT Hub file uploads using PowerShell</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

<span data-ttu-id="101ab-105">toouse hello [fonctionnalité de téléchargement de fichiers dans le IoT Hub][lnk-upload], vous devez d’abord associer un compte de stockage Azure avec votre IoT hub.</span><span class="sxs-lookup"><span data-stu-id="101ab-105">toouse hello [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure storage account with your IoT hub.</span></span> <span data-ttu-id="101ab-106">Vous pouvez utiliser un compte de stockage existant ou en créer un nouveau.</span><span class="sxs-lookup"><span data-stu-id="101ab-106">You can use an existing storage account or create a new one.</span></span>

<span data-ttu-id="101ab-107">toocomplete ce didacticiel, vous devez hello suivant :</span><span class="sxs-lookup"><span data-stu-id="101ab-107">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="101ab-108">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="101ab-108">An active Azure account.</span></span> <span data-ttu-id="101ab-109">Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit][lnk-free-trial] en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="101ab-109">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="101ab-110">[Applets de commande Azure PowerShell][lnk-powershell-install].</span><span class="sxs-lookup"><span data-stu-id="101ab-110">[Azure PowerShell cmdlets][lnk-powershell-install].</span></span>
* <span data-ttu-id="101ab-111">Un IoT Hub Azure.</span><span class="sxs-lookup"><span data-stu-id="101ab-111">An Azure IoT hub.</span></span> <span data-ttu-id="101ab-112">Si vous n’avez pas un hub IoT, vous pouvez utiliser hello [applet de commande New-AzureRmIoTHub] [ lnk-powershell-iothub] toocreate un ou utilisez hello portail trop[créez un hub IoT] [ lnk-portal-hub].</span><span class="sxs-lookup"><span data-stu-id="101ab-112">If you don't have an IoT hub, you can use hello [New-AzureRmIoTHub cmdlet][lnk-powershell-iothub] toocreate one or use hello portal too[Create an IoT hub][lnk-portal-hub].</span></span>
* <span data-ttu-id="101ab-113">Un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="101ab-113">An Azure storage account.</span></span> <span data-ttu-id="101ab-114">Si vous n’avez pas un compte de stockage Azure, vous pouvez utiliser hello [applets de commande PowerShell de stockage Azure] [ lnk-powershell-storage] toocreate un ou utilisez hello portail trop[créer un compte de stockage] [ lnk-portal-storage].</span><span class="sxs-lookup"><span data-stu-id="101ab-114">If you don't have an Azure storage account, you can use hello [Azure Storage PowerShell cmdlets][lnk-powershell-storage] toocreate one or use hello portal too[Create a storage account][lnk-portal-storage].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="101ab-115">Se connecter à votre compte Azure et le définir</span><span class="sxs-lookup"><span data-stu-id="101ab-115">Sign in and set your Azure account</span></span>

<span data-ttu-id="101ab-116">Connectez-vous à tooyour compte Azure, puis sélectionnez votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="101ab-116">Sign in tooyour Azure account and select your subscription.</span></span>

1. <span data-ttu-id="101ab-117">À l’invite de commandes PowerShell hello, exécutez hello **AzureRmAccount de connexion** applet de commande :</span><span class="sxs-lookup"><span data-stu-id="101ab-117">At hello PowerShell prompt, run hello **Login-AzureRmAccount** cmdlet:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="101ab-118">Si vous avez plusieurs abonnements Azure, l’ouverture de session tooAzure accorde vous accédez tooall hello Azure abonnements associés à vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="101ab-118">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="101ab-119">Utilisez hello toolist hello abonnements Azure disponibles pour vous toouse de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="101ab-119">Use hello following command toolist hello Azure subscriptions available for you toouse:</span></span>

    ```powershell
    Get-AzureRMSubscription
    ```

    <span data-ttu-id="101ab-120">Utilisez hello suivant abonnement tooselect de commande que vous souhaitez toouse toorun hello commandes toomanage votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="101ab-120">Use hello following command tooselect subscription that you want toouse toorun hello commands toomanage your IoT hub.</span></span> <span data-ttu-id="101ab-121">Vous pouvez utiliser le nom de l’abonnement hello ou ID de sortie hello de la commande précédente hello :</span><span class="sxs-lookup"><span data-stu-id="101ab-121">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

## <a name="retrieve-your-storage-account-details"></a><span data-ttu-id="101ab-122">Récupérez vos détails du compte de stockage</span><span class="sxs-lookup"><span data-stu-id="101ab-122">Retrieve your storage account details</span></span>

<span data-ttu-id="101ab-123">Hello étapes suivantes supposent que vous avez créé votre compte de stockage à l’aide de hello **le Gestionnaire de ressources** modèle de déploiement et pas hello **classique** modèle de déploiement.</span><span class="sxs-lookup"><span data-stu-id="101ab-123">hello following steps assume that you created your storage account using hello **Resource Manager** deployment model, and not hello **Classic** deployment model.</span></span>

<span data-ttu-id="101ab-124">tooconfigure fichier télécharge à partir de vos appareils, vous avez besoin d’une chaîne de connexion hello pour un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="101ab-124">tooconfigure file uploads from your devices, you need hello connection string for an Azure storage account.</span></span> <span data-ttu-id="101ab-125">compte de stockage Hello doit être Bonjour même abonnement que votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="101ab-125">hello storage account must be in hello same subscription as your IoT hub.</span></span> <span data-ttu-id="101ab-126">Vous devez également le nom hello d’un conteneur d’objets blob dans le compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="101ab-126">You also need hello name of a blob container in hello storage account.</span></span> <span data-ttu-id="101ab-127">Utilisez hello suivant commande tooretrieve vos clés de compte de stockage :</span><span class="sxs-lookup"><span data-stu-id="101ab-127">Use hello following command tooretrieve your storage account keys:</span></span>

```powershell
Get-AzureRmStorageAccountKey `
  -Name {your storage account name} `
  -ResourceGroupName {your storage account resource group}
```

<span data-ttu-id="101ab-128">Prenez note de hello **key1** valeur de clé de compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="101ab-128">Make a note of hello **key1** storage account key value.</span></span> <span data-ttu-id="101ab-129">Vous en avez besoin dans hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="101ab-129">You need it in hello following steps.</span></span>

<span data-ttu-id="101ab-130">Vous pouvez utiliser un conteneur d’objets blob existant pour les chargements de fichiers ou en créer un nouveau :</span><span class="sxs-lookup"><span data-stu-id="101ab-130">You can either use an existing blob container for your file uploads or create new one:</span></span>

* <span data-ttu-id="101ab-131">toolist hello existant conteneurs d’objets blob dans votre compte de stockage, utilisez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="101ab-131">toolist hello existing blob containers in your storage account, use hello following commands:</span></span>

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    Get-AzureStorageContainer -Context $ctx
    ```

* <span data-ttu-id="101ab-132">toocreate un conteneur d’objets blob dans votre compte de stockage, hello utilisation suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="101ab-132">toocreate a blob container in your storage account, use hello following commands:</span></span>

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    New-AzureStorageContainer `
        -Name {your new container name} `
        -Permission Off `
        -Context $ctx
    ```

## <a name="configure-your-iot-hub"></a><span data-ttu-id="101ab-133">Configuration de votre IoT Hub</span><span class="sxs-lookup"><span data-stu-id="101ab-133">Configure your IoT hub</span></span>

<span data-ttu-id="101ab-134">Vous pouvez désormais configurer votre tooenable de hub IoT [fonctionnalité de téléchargement de fichiers] [ lnk-upload] à l’aide des informations de compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="101ab-134">You can now configure your IoT hub tooenable [file upload functionality][lnk-upload] using your storage account details.</span></span>

<span data-ttu-id="101ab-135">configuration de Hello nécessite hello valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="101ab-135">hello configuration requires hello following values:</span></span>

<span data-ttu-id="101ab-136">**Conteneur de stockage**: un conteneur d’objets blob dans un compte de stockage Azure dans votre tooassociate abonnement Azure actuel avec votre IoT hub.</span><span class="sxs-lookup"><span data-stu-id="101ab-136">**Storage container**: A blob container in an Azure storage account in your current Azure subscription tooassociate with your IoT hub.</span></span> <span data-ttu-id="101ab-137">Vous avez extrait les informations de compte de stockage nécessaires hello Bonjour précédant la section.</span><span class="sxs-lookup"><span data-stu-id="101ab-137">You retrieved hello necessary storage account information in hello preceding section.</span></span> <span data-ttu-id="101ab-138">IoT Hub génère automatiquement les URI de SAS avec le conteneur d’objets blob toothis écriture des autorisations pour les appareils toouse lorsqu’ils téléchargent des fichiers.</span><span class="sxs-lookup"><span data-stu-id="101ab-138">IoT Hub automatically generates SAS URIs with write permissions toothis blob container for devices toouse when they upload files.</span></span>

<span data-ttu-id="101ab-139">**Recevoir des notifications pour les fichiers chargés** : activez ou désactivez les notifications de chargement de fichiers.</span><span class="sxs-lookup"><span data-stu-id="101ab-139">**Receive notifications for uploaded files**: Enable or disable file upload notifications.</span></span>

<span data-ttu-id="101ab-140">**SAS TTL**: ce paramètre est hello time-to-live de hello SAS URI retourné toohello appareil par IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="101ab-140">**SAS TTL**: This setting is hello time-to-live of hello SAS URIs returned toohello device by IoT Hub.</span></span> <span data-ttu-id="101ab-141">Heure de tooone la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="101ab-141">Set tooone hour by default.</span></span>

<span data-ttu-id="101ab-142">**Fichier de paramètres par défaut de durée de vie de notification**: hello time-to-live d’une notification de téléchargement de fichier avant son expiration.</span><span class="sxs-lookup"><span data-stu-id="101ab-142">**File notification settings default TTL**: hello time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="101ab-143">Valeur tooone jour par défaut.</span><span class="sxs-lookup"><span data-stu-id="101ab-143">Set tooone day by default.</span></span>

<span data-ttu-id="101ab-144">**Nombre maximal de diffusions de notification de fichiers**: hello fréquence hello IoT Hub tentatives toodeliver une notification de téléchargement de fichier.</span><span class="sxs-lookup"><span data-stu-id="101ab-144">**File notification maximum delivery count**: hello number of times hello IoT Hub attempts toodeliver a file upload notification.</span></span> <span data-ttu-id="101ab-145">Too10 la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="101ab-145">Set too10 by default.</span></span>

<span data-ttu-id="101ab-146">Hello, suivant les paramètres de téléchargement du fichier PowerShell applet de commande hello tooconfigure de votre hub IoT, utilisez :</span><span class="sxs-lookup"><span data-stu-id="101ab-146">Use hello following PowerShell cmdlet tooconfigure hello file upload settings on your IoT hub:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="101ab-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="101ab-147">Next steps</span></span>

<span data-ttu-id="101ab-148">Pour plus d’informations sur les fonctionnalités de téléchargement de fichier hello IoT Hub, consultez [télécharger des fichiers à partir d’un appareil][lnk-upload].</span><span class="sxs-lookup"><span data-stu-id="101ab-148">For more information about hello file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload].</span></span>

<span data-ttu-id="101ab-149">Suivez ces liens de toolearn plus d’informations sur la gestion de Azure IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="101ab-149">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="101ab-150">[Gérer en bloc des appareils IoT][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="101ab-150">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="101ab-151">[Métriques d’IoT Hub][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="101ab-151">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="101ab-152">[Surveillance des opérations][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="101ab-152">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="101ab-153">toofurther Explorez les fonctionnalités de hello d’IoT Hub, consultez :</span><span class="sxs-lookup"><span data-stu-id="101ab-153">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="101ab-154">[Guide du développeur IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="101ab-154">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="101ab-155">[Simulation d’un appareil avec IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="101ab-155">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="101ab-156">[Sécuriser votre solution IoT hello d’arrière-plan][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="101ab-156">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

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