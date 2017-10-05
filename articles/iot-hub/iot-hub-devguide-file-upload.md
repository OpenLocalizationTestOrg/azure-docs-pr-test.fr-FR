---
title: Bien comprendre le chargement de fichiers Azure IoT Hub | Microsoft Docs
description: "Guide du développeur - utilisez la fonctionnalité de chargement de fichier de IoT Hub pour gérer le chargement de fichiers depuis un appareil vers un conteneur d’objets blob de stockage Azure."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: a0427925-3e40-4fcd-96c1-2a31d1ddc14b
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 75a6b9bc3ecfe6d6901bb38e312d62333f38daf1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="upload-files-with-iot-hub"></a><span data-ttu-id="b3d55-103">Chargement de fichiers avec IoT Hub</span><span class="sxs-lookup"><span data-stu-id="b3d55-103">Upload files with IoT Hub</span></span>

<span data-ttu-id="b3d55-104">Comme nous l’avons expliqué dans l’article [Référence - Points de terminaison IoT Hub][lnk-endpoints], un appareil peut initier un chargement de fichiers en envoyant une notification par le biais d’un point de terminaison côté appareil (**/devices/{deviceId}/files**).</span><span class="sxs-lookup"><span data-stu-id="b3d55-104">As detailed in the [IoT Hub endpoints][lnk-endpoints] article, a device can initiate a file upload by sending a notification through a device-facing endpoint (**/devices/{deviceId}/files**).</span></span> <span data-ttu-id="b3d55-105">Lorsqu’un appareil indique à IoT Hub la fin d’un chargement, IoT Hub envoie un message de notification de chargement de fichiers via le point de terminaison côté service (**/messages/servicebound/filenotifications**).</span><span class="sxs-lookup"><span data-stu-id="b3d55-105">When a device notifies IoT Hub that an upload is complete, IoT Hub sends a file upload notification message through the **/messages/servicebound/filenotifications** service-facing endpoint.</span></span>

<span data-ttu-id="b3d55-106">Au lieu de distribuer les messages via sa propre plate-forme, IoT Hub joue le rôle de répartiteur vers un compte Stockage Azure associé.</span><span class="sxs-lookup"><span data-stu-id="b3d55-106">Instead of brokering messages through IoT Hub itself, IoT Hub instead acts as a dispatcher to an associated Azure Storage account.</span></span> <span data-ttu-id="b3d55-107">Un appareil demande à IoT Hub un jeton de stockage spécifique au fichier que l’appareil souhaite télécharger.</span><span class="sxs-lookup"><span data-stu-id="b3d55-107">A device requests a storage token from IoT Hub that is specific to the file the device wishes to upload.</span></span> <span data-ttu-id="b3d55-108">L’appareil utilise l’URI SAP pour télécharger le fichier vers le stockage. Une fois le téléchargement terminé, l’appareil envoie une notification à IoT Hub pour l’en informer.</span><span class="sxs-lookup"><span data-stu-id="b3d55-108">The device uses the SAS URI to upload the file to storage, and when the upload is complete the device sends a notification of completion to IoT Hub.</span></span> <span data-ttu-id="b3d55-109">IoT Hub vérifie que le chargement de fichiers est terminé, puis ajoute un message de notification de chargement de fichiers au point de terminaison côté service dédié à la notification de fichiers.</span><span class="sxs-lookup"><span data-stu-id="b3d55-109">IoT Hub checks the file upload is complete and then adds a file upload notification message to the service-facing file notification endpoint.</span></span>

<span data-ttu-id="b3d55-110">Avant de charger un fichier vers IoT Hub à partir d’un appareil, vous devez configurer votre hub en [l’associant à un compte de stockage Azure][lnk-associate-storage].</span><span class="sxs-lookup"><span data-stu-id="b3d55-110">Before you upload a file to IoT Hub from a device, you must configure your hub by [associating an Azure Storage][lnk-associate-storage] account to it.</span></span>

<span data-ttu-id="b3d55-111">Votre appareil peut ensuite [initialiser un chargement][lnk-initialize] puis [notifier IoT Hub][lnk-notify] lorsque le chargement est terminé.</span><span class="sxs-lookup"><span data-stu-id="b3d55-111">Your device can then [initialize an upload][lnk-initialize] and then [notify IoT hub][lnk-notify] when the upload completes.</span></span> <span data-ttu-id="b3d55-112">Éventuellement, lorsqu’un appareil notifie IoT Hub que le chargement est terminé, le service peut générer un [message de notification][lnk-service-notification].</span><span class="sxs-lookup"><span data-stu-id="b3d55-112">Optionally, when a device notifies IoT Hub that the upload is complete, the service can generate a [notification message][lnk-service-notification].</span></span>

### <a name="when-to-use"></a><span data-ttu-id="b3d55-113">Quand utiliser</span><span class="sxs-lookup"><span data-stu-id="b3d55-113">When to use</span></span>

<span data-ttu-id="b3d55-114">Utilisez le chargement des fichiers pour envoyer des fichiers multimédias et de gros traitements télémétriques par lots chargés par des appareils connectés par intermittence ou compressés pour économiser de la bande passante.</span><span class="sxs-lookup"><span data-stu-id="b3d55-114">Use file upload to send media files and large telemetry batches uploaded by intermittently connected devices or compressed to save bandwidth.</span></span>

<span data-ttu-id="b3d55-115">Reportez-vous à [l’aide sur la communication appareil-à-cloud][lnk-d2c-guidance] en cas de doute entre l’utilisation des propriétés signalées, des messages appareil-à-cloud ou du chargement de fichiers.</span><span class="sxs-lookup"><span data-stu-id="b3d55-115">Refer to [Device-to-cloud communication guidance][lnk-d2c-guidance] if in doubt between using reported properties, device-to-cloud messages, or file upload.</span></span>

## <a name="associate-an-azure-storage-account-with-iot-hub"></a><span data-ttu-id="b3d55-116">Association d’un compte Stockage Azure à IoT Hub</span><span class="sxs-lookup"><span data-stu-id="b3d55-116">Associate an Azure Storage account with IoT Hub</span></span>

<span data-ttu-id="b3d55-117">Pour utiliser la fonctionnalité de téléchargement de fichier, vous devez d’abord lier un compte Stockage Azure à IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b3d55-117">To use the file upload functionality, you must first link an Azure Storage account to the IoT Hub.</span></span> <span data-ttu-id="b3d55-118">Vous pouvez terminer ce travail en utilisant le [Portail Azure][lnk-management-portal], ou en exécutant un programme par le biais de [l’API REST de fournisseur de ressources IoT Hub][lnk-resource-provider-apis].</span><span class="sxs-lookup"><span data-stu-id="b3d55-118">You can complete this task either through the [Azure portal][lnk-management-portal], or programmatically through the [IoT Hub resource provider REST APIs][lnk-resource-provider-apis].</span></span> <span data-ttu-id="b3d55-119">Une fois que vous avez associé un compte Stockage Azure à IoT Hub, le service retourne un URI SAP vers un appareil lorsque ce dernier initie une demande de téléchargement de fichier.</span><span class="sxs-lookup"><span data-stu-id="b3d55-119">Once you have associated an Azure Storage account with your IoT Hub, the service returns a SAS URI to a device when the device initiates a file upload request.</span></span>

> [!NOTE]
> <span data-ttu-id="b3d55-120">Les kits [Azure IoT SDK][lnk-sdks] gèrent automatiquement la récupération de l’URI SAP, le chargement du fichier et l’envoi d’une notification à IoT Hub pour l’informer de la fin du chargement.</span><span class="sxs-lookup"><span data-stu-id="b3d55-120">The [Azure IoT SDKs][lnk-sdks] automatically handle retrieving the SAS URI, uploading the file, and notifying IoT Hub of a completed upload.</span></span>


## <a name="initialize-a-file-upload"></a><span data-ttu-id="b3d55-121">Initialiser un téléchargement de fichier</span><span class="sxs-lookup"><span data-stu-id="b3d55-121">Initialize a file upload</span></span>
<span data-ttu-id="b3d55-122">IoT Hub a un point de terminaison spécifique aux appareils pour demander une URI SAS pour le stockage afin de télécharger un fichier.</span><span class="sxs-lookup"><span data-stu-id="b3d55-122">IoT Hub has an endpoint specifically for devices to request a SAS URI for storage to upload a file.</span></span> <span data-ttu-id="b3d55-123">Pour initier le processus de chargement de fichiers, l’appareil envoie une requête POST à `{iot hub}.azure-devices.net/devices/{deviceId}/files` avec le corps JSON suivant :</span><span class="sxs-lookup"><span data-stu-id="b3d55-123">To initiate the file upload process, the device sends a POST request to `{iot hub}.azure-devices.net/devices/{deviceId}/files` with the following JSON body:</span></span>

```json
{
    "blobName": "{name of the file for which a SAS URI will be generated}"
}
```

<span data-ttu-id="b3d55-124">IoT Hub renvoie les données suivantes. L’appareil l’utilise pour télécharger le fichier :</span><span class="sxs-lookup"><span data-stu-id="b3d55-124">IoT Hub returns the following data, which the device uses to upload the file:</span></span>

```json
{
    "correlationId": "somecorrelationid",
    "hostName": "contoso.azure-devices.net",
    "containerName": "testcontainer",
    "blobName": "test-device1/image.jpg",
    "sasToken": "1234asdfSAStoken"
}
```

### <a name="deprecated-initialize-a-file-upload-with-a-get"></a><span data-ttu-id="b3d55-125">Déconseillé : initialiser un téléchargement de fichier avec une commande GET</span><span class="sxs-lookup"><span data-stu-id="b3d55-125">Deprecated: initialize a file upload with a GET</span></span>

> [!NOTE]
> <span data-ttu-id="b3d55-126">Cette section décrit les fonctionnalités déconseillées pour la réception d’une URI SAS d’IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b3d55-126">This section describes deprecated functionality for how to receive a SAS URI from IoT Hub.</span></span> <span data-ttu-id="b3d55-127">Utilisez la méthode POST décrite précédemment.</span><span class="sxs-lookup"><span data-stu-id="b3d55-127">Use the POST method described previously.</span></span>

<span data-ttu-id="b3d55-128">IoT Hub utilise deux points de terminaison REST pour prendre en charge le téléchargement de fichier, le premier afin d’obtenir l’URI SAP pour le stockage et le second pour informer IoT hub de la fin du téléchargement.</span><span class="sxs-lookup"><span data-stu-id="b3d55-128">IoT Hub has two REST endpoints to support file upload, one to get the SAS URI for storage and the other to notify the IoT hub of a completed upload.</span></span> <span data-ttu-id="b3d55-129">L’appareil lance le processus de téléchargement de fichier en envoyant une commande GET à IoT Hub à `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`.</span><span class="sxs-lookup"><span data-stu-id="b3d55-129">The device initiates the file upload process by sending a GET to the IoT hub at `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`.</span></span> <span data-ttu-id="b3d55-130">L’IoT Hub renvoie :</span><span class="sxs-lookup"><span data-stu-id="b3d55-130">The IoT hub returns:</span></span>

* <span data-ttu-id="b3d55-131">Un URI SAS spécifique au fichier à charger.</span><span class="sxs-lookup"><span data-stu-id="b3d55-131">A SAS URI specific to the file to be uploaded.</span></span>
* <span data-ttu-id="b3d55-132">Un ID de corrélation à utiliser une fois le chargement terminé.</span><span class="sxs-lookup"><span data-stu-id="b3d55-132">A correlation ID to be used once the upload is completed.</span></span>

## <a name="notify-iot-hub-of-a-completed-file-upload"></a><span data-ttu-id="b3d55-133">Notifier IoT Hub de la fin du téléchargement d’un fichier</span><span class="sxs-lookup"><span data-stu-id="b3d55-133">Notify IoT Hub of a completed file upload</span></span>

<span data-ttu-id="b3d55-134">L’appareil est chargé de télécharger le fichier vers le stockage à l’aide des kits SDK Stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="b3d55-134">The device is responsible for uploading the file to storage using the Azure Storage SDKs.</span></span> <span data-ttu-id="b3d55-135">Une fois le chargement terminé, l’appareil envoie une requête POST à `{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` avec le corps JSON suivant :</span><span class="sxs-lookup"><span data-stu-id="b3d55-135">When the upload is complete, the device sends a POST request to `{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` with the following JSON body:</span></span>

```json
{
    "correlationId": "{correlation ID received from the initial request}",
    "isSuccess": bool,
    "statusCode": XXX,
    "statusDescription": "Description of status"
}
```

<span data-ttu-id="b3d55-136">La valeur de `isSuccess` est une valeur booléenne indiquant si le fichier a été téléchargé avec succès.</span><span class="sxs-lookup"><span data-stu-id="b3d55-136">The value of `isSuccess` is a Boolean representing whether the file was uploaded successfully.</span></span> <span data-ttu-id="b3d55-137">Le code d’état de `statusCode` est l’état pour le téléchargement du fichier vers le stockage et `statusDescription` correspond à `statusCode`.</span><span class="sxs-lookup"><span data-stu-id="b3d55-137">The status code for `statusCode` is the status for the upload of the file to storage, and the `statusDescription` corresponds to the `statusCode`.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="b3d55-138">Rubriques de référence :</span><span class="sxs-lookup"><span data-stu-id="b3d55-138">Reference topics:</span></span>

<span data-ttu-id="b3d55-139">Les rubriques de référence suivantes vous fournissent des informations supplémentaires sur le téléchargement de fichiers depuis un appareil.</span><span class="sxs-lookup"><span data-stu-id="b3d55-139">The following reference topics provide you with more information about uploading files from a device.</span></span>

## <a name="file-upload-notifications"></a><span data-ttu-id="b3d55-140">Notifications de téléchargement de fichier</span><span class="sxs-lookup"><span data-stu-id="b3d55-140">File upload notifications</span></span>

<span data-ttu-id="b3d55-141">Éventuellement, lorsqu’un appareil informe IoT Hub de la fin d’un chargement, IoT Hub peut générer un message de notification contenant le nom et l’emplacement de stockage du fichier.</span><span class="sxs-lookup"><span data-stu-id="b3d55-141">Optionally, when a device notifies IoT Hub that an upload is complete, IoT Hub can generate a notification message that contains the name and storage location of the file.</span></span>

<span data-ttu-id="b3d55-142">Comme l’explique la section [Points de terminaison][lnk-endpoints], IoT Hub fournit des notifications de chargement de fichiers sous la forme de messages par le biais d’un point de terminaison côté service (**/messages/servicebound/fileuploadnotifications**).</span><span class="sxs-lookup"><span data-stu-id="b3d55-142">As explained in [Endpoints][lnk-endpoints], IoT Hub delivers file upload notifications through a service-facing endpoint (**/messages/servicebound/fileuploadnotifications**) as messages.</span></span> <span data-ttu-id="b3d55-143">La sémantique de réception des notifications de chargement de fichiers est identique à celle des messages cloud-à-appareil et présente le même [cycle de vie des messages][lnk-lifecycle].</span><span class="sxs-lookup"><span data-stu-id="b3d55-143">The receive semantics for file upload notifications are the same as for cloud-to-device messages and have the same [message lifecycle][lnk-lifecycle].</span></span> <span data-ttu-id="b3d55-144">Chaque message récupéré à partir du point de terminaison de notification de téléchargement de fichier est un enregistrement JSON qui possède les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="b3d55-144">Each message retrieved from the file upload notification endpoint is a JSON record with the following properties:</span></span>

| <span data-ttu-id="b3d55-145">Propriété</span><span class="sxs-lookup"><span data-stu-id="b3d55-145">Property</span></span> | <span data-ttu-id="b3d55-146">Description</span><span class="sxs-lookup"><span data-stu-id="b3d55-146">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b3d55-147">EnqueuedTimeUtc</span><span class="sxs-lookup"><span data-stu-id="b3d55-147">EnqueuedTimeUtc</span></span> |<span data-ttu-id="b3d55-148">Horodatage indiquant la date et l’heure de création de la notification.</span><span class="sxs-lookup"><span data-stu-id="b3d55-148">Timestamp indicating when the notification was created.</span></span> |
| <span data-ttu-id="b3d55-149">deviceId</span><span class="sxs-lookup"><span data-stu-id="b3d55-149">DeviceId</span></span> |<span data-ttu-id="b3d55-150">**DeviceId** de l’appareil qui a téléchargé le fichier.</span><span class="sxs-lookup"><span data-stu-id="b3d55-150">**DeviceId** of the device which uploaded the file.</span></span> |
| <span data-ttu-id="b3d55-151">BlobUri</span><span class="sxs-lookup"><span data-stu-id="b3d55-151">BlobUri</span></span> |<span data-ttu-id="b3d55-152">URI du fichier téléchargé.</span><span class="sxs-lookup"><span data-stu-id="b3d55-152">URI of the uploaded file.</span></span> |
| <span data-ttu-id="b3d55-153">BlobName</span><span class="sxs-lookup"><span data-stu-id="b3d55-153">BlobName</span></span> |<span data-ttu-id="b3d55-154">Nom du fichier téléchargé.</span><span class="sxs-lookup"><span data-stu-id="b3d55-154">Name of the uploaded file.</span></span> |
| <span data-ttu-id="b3d55-155">LastUpdatedTime</span><span class="sxs-lookup"><span data-stu-id="b3d55-155">LastUpdatedTime</span></span> |<span data-ttu-id="b3d55-156">Horodatage indiquant la date et l’heure de dernière mise à jour du fichier.</span><span class="sxs-lookup"><span data-stu-id="b3d55-156">Timestamp indicating when the file was last updated.</span></span> |
| <span data-ttu-id="b3d55-157">BlobSizeInBytes</span><span class="sxs-lookup"><span data-stu-id="b3d55-157">BlobSizeInBytes</span></span> |<span data-ttu-id="b3d55-158">Taille du fichier téléchargé.</span><span class="sxs-lookup"><span data-stu-id="b3d55-158">Size of the uploaded file.</span></span> |

<span data-ttu-id="b3d55-159">**Exemple**.</span><span class="sxs-lookup"><span data-stu-id="b3d55-159">**Example**.</span></span> <span data-ttu-id="b3d55-160">Voici un exemple illustrant le corps de message de notification de téléchargement de fichier.</span><span class="sxs-lookup"><span data-stu-id="b3d55-160">This example shows the body of a file upload notification message.</span></span>

```json
{
    "deviceId":"mydevice",
    "blobUri":"https://{storage account}.blob.core.windows.net/{container name}/mydevice/myfile.jpg",
    "blobName":"mydevice/myfile.jpg",
    "lastUpdatedTime":"2016-06-01T21:22:41+00:00",
    "blobSizeInBytes":1234,
    "enqueuedTimeUtc":"2016-06-01T21:22:43.7996883Z"
}
```

## <a name="file-upload-notification-configuration-options"></a><span data-ttu-id="b3d55-161">Options de configuration de notification de téléchargement de fichier</span><span class="sxs-lookup"><span data-stu-id="b3d55-161">File upload notification configuration options</span></span>

<span data-ttu-id="b3d55-162">Chaque IoT Hub expose les options de configuration suivantes pour les notifications de téléchargement de fichier :</span><span class="sxs-lookup"><span data-stu-id="b3d55-162">Each IoT hub exposes the following configuration options for file upload notifications:</span></span>

| <span data-ttu-id="b3d55-163">Propriété</span><span class="sxs-lookup"><span data-stu-id="b3d55-163">Property</span></span> | <span data-ttu-id="b3d55-164">Description</span><span class="sxs-lookup"><span data-stu-id="b3d55-164">Description</span></span> | <span data-ttu-id="b3d55-165">Plage et valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="b3d55-165">Range and default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b3d55-166">**enableFileUploadNotifications**</span><span class="sxs-lookup"><span data-stu-id="b3d55-166">**enableFileUploadNotifications**</span></span> |<span data-ttu-id="b3d55-167">Indique si les notifications de téléchargement de fichier sont écrites dans le point de terminaison de notification de fichier.</span><span class="sxs-lookup"><span data-stu-id="b3d55-167">Controls whether file upload notifications are written to the file notifications endpoint.</span></span> |<span data-ttu-id="b3d55-168">Valeur booléenne.</span><span class="sxs-lookup"><span data-stu-id="b3d55-168">Bool.</span></span> <span data-ttu-id="b3d55-169">Par défaut : True.</span><span class="sxs-lookup"><span data-stu-id="b3d55-169">Default: True.</span></span> |
| <span data-ttu-id="b3d55-170">**fileNotifications.ttlAsIso8601**</span><span class="sxs-lookup"><span data-stu-id="b3d55-170">**fileNotifications.ttlAsIso8601**</span></span> |<span data-ttu-id="b3d55-171">Durée de vie par défaut des notifications de téléchargement de fichier.</span><span class="sxs-lookup"><span data-stu-id="b3d55-171">Default TTL for file upload notifications.</span></span> |<span data-ttu-id="b3d55-172">Intervalle ISO_8601 jusqu’à 48h (minimum 1 minute).</span><span class="sxs-lookup"><span data-stu-id="b3d55-172">ISO_8601 interval up to 48H (minimum 1 minute).</span></span> <span data-ttu-id="b3d55-173">Par défaut : 1 heure.</span><span class="sxs-lookup"><span data-stu-id="b3d55-173">Default: 1 hour.</span></span> |
| <span data-ttu-id="b3d55-174">**fileNotifications.lockDuration**</span><span class="sxs-lookup"><span data-stu-id="b3d55-174">**fileNotifications.lockDuration**</span></span> |<span data-ttu-id="b3d55-175">Durée de verrouillage de la file d’attente des notifications de téléchargement de fichiers.</span><span class="sxs-lookup"><span data-stu-id="b3d55-175">Lock duration for the file upload notifications queue.</span></span> |<span data-ttu-id="b3d55-176">5 à 300 secondes (5 secondes au minimum).</span><span class="sxs-lookup"><span data-stu-id="b3d55-176">5 to 300 seconds (minimum 5 seconds).</span></span> <span data-ttu-id="b3d55-177">Par défaut : 60 secondes.</span><span class="sxs-lookup"><span data-stu-id="b3d55-177">Default: 60 seconds.</span></span> |
| <span data-ttu-id="b3d55-178">**fileNotifications.maxDeliveryCount**</span><span class="sxs-lookup"><span data-stu-id="b3d55-178">**fileNotifications.maxDeliveryCount**</span></span> |<span data-ttu-id="b3d55-179">Nombre maximal de diffusions pour la file d’attente de notification de téléchargement de fichier.</span><span class="sxs-lookup"><span data-stu-id="b3d55-179">Maximum delivery count for the file upload notification queue.</span></span> |<span data-ttu-id="b3d55-180">1 à 100.</span><span class="sxs-lookup"><span data-stu-id="b3d55-180">1 to 100.</span></span> <span data-ttu-id="b3d55-181">Par défaut : 100.</span><span class="sxs-lookup"><span data-stu-id="b3d55-181">Default: 100.</span></span> |

## <a name="additional-reference-material"></a><span data-ttu-id="b3d55-182">Matériel de référence supplémentaire</span><span class="sxs-lookup"><span data-stu-id="b3d55-182">Additional reference material</span></span>

<span data-ttu-id="b3d55-183">Les autres rubriques de référence dans le Guide du développeur IoT Hub comprennent :</span><span class="sxs-lookup"><span data-stu-id="b3d55-183">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="b3d55-184">La rubrique [Points de terminaison IoT Hub][lnk-endpoints] décrit les différents points de terminaison que chaque IoT Hub expose pour les opérations d’exécution et de gestion.</span><span class="sxs-lookup"><span data-stu-id="b3d55-184">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="b3d55-185">La rubrique [Référence - Quotas et limitation IoT Hub][lnk-quotas] décrit les quotas et le comportement de limitation qui s’appliquent au service IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b3d55-185">[Throttling and quotas][lnk-quotas] describes the quotas and throttling behaviors that apply to the IoT Hub service.</span></span>
* <span data-ttu-id="b3d55-186">La section [Azure IoT device et service SDK][lnk-sdks] répertorie les Kits de développement logiciel (SDK) en différents langages que vous pouvez utiliser pour le développement d’applications d’appareil et de service qui interagissent avec IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b3d55-186">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="b3d55-187">La rubrique [Référence - Langage de requête IoT Hub pour les jumeaux d’appareil, les travaux et le routage des messages][lnk-query] décrit le langage de requête permettant de récupérer à partir d’IoT Hub des informations sur des jumeaux d’appareil et des travaux.</span><span class="sxs-lookup"><span data-stu-id="b3d55-187">[IoT Hub query language][lnk-query] describes the query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="b3d55-188">La rubrique [Prise en charge de MQTT au niveau d’IoT Hub][lnk-devguide-mqtt] fournit des informations supplémentaires sur la prise en charge du protocole MQTT par IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b3d55-188">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3d55-189">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b3d55-189">Next steps</span></span>

<span data-ttu-id="b3d55-190">À présent que vous savez comment télécharger des fichiers depuis des appareils avec IoT Hub, vous serez peut-être intéressé par les rubriques suivantes du Guide du développeur IoT :</span><span class="sxs-lookup"><span data-stu-id="b3d55-190">Now you have learned how to upload files from devices using IoT Hub, you may be interested in the following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="b3d55-191">[Gérer les identités des appareils dans IoT Hub][lnk-devguide-identities]</span><span class="sxs-lookup"><span data-stu-id="b3d55-191">[Manage device identities in IoT Hub][lnk-devguide-identities]</span></span>
* <span data-ttu-id="b3d55-192">[Contrôler l’accès à IoT Hub][lnk-devguide-security]</span><span class="sxs-lookup"><span data-stu-id="b3d55-192">[Control access to IoT Hub][lnk-devguide-security]</span></span>
* <span data-ttu-id="b3d55-193">[Utiliser des représentations d’appareil pour synchroniser les données d’état et de configuration][lnk-devguide-device-twins]</span><span class="sxs-lookup"><span data-stu-id="b3d55-193">[Use device twins to synchronize state and configurations][lnk-devguide-device-twins]</span></span>
* <span data-ttu-id="b3d55-194">[Appeler une méthode directe sur un appareil][lnk-devguide-directmethods]</span><span class="sxs-lookup"><span data-stu-id="b3d55-194">[Invoke a direct method on a device][lnk-devguide-directmethods]</span></span>
* <span data-ttu-id="b3d55-195">[Planifier des travaux sur plusieurs appareils][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="b3d55-195">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="b3d55-196">Si vous souhaitez tenter de mettre en pratique certains des concepts décrits dans cet article, vous serez peut-être intéressé par le didacticiel IoT Hub suivant :</span><span class="sxs-lookup"><span data-stu-id="b3d55-196">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorial:</span></span>

* <span data-ttu-id="b3d55-197">[Charger des fichiers à partir d’appareils vers le cloud avec IoT Hub][lnk-fileupload-tutorial]</span><span class="sxs-lookup"><span data-stu-id="b3d55-197">[How to upload files from devices to the cloud with IoT Hub][lnk-fileupload-tutorial]</span></span>

[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-management-portal]: https://portal.azure.com
[lnk-fileupload-tutorial]: iot-hub-csharp-csharp-file-upload.md
[lnk-associate-storage]: iot-hub-devguide-file-upload.md#associate-an-azure-storage-account-with-iot-hub
[lnk-initialize]: iot-hub-devguide-file-upload.md#initialize-a-file-upload
[lnk-notify]: iot-hub-devguide-file-upload.md#notify-iot-hub-of-a-completed-file-upload
[lnk-service-notification]: iot-hub-devguide-file-upload.md#file-upload-notifications
[lnk-lifecycle]: iot-hub-devguide-messages-c2d.md#the-cloud-to-device-message-lifecycle
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[lnk-devguide-identities]: iot-hub-devguide-identity-registry.md
[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
