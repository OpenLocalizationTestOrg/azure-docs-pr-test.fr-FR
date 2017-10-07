---
title: "téléchargement du fichier Azure IoT Hub aaaUnderstand | Documents Microsoft"
description: "Guide du développeur - fonctionnalité de téléchargement du fichier utilisation hello de toomanage IoT Hub téléchargement de fichiers à partir d’un conteneur d’objets blob Azure storage appareil tooan."
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
ms.openlocfilehash: d44f9303ead4fa282dc0baf70887af1b8a03293d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-with-iot-hub"></a><span data-ttu-id="7639f-103">Chargement de fichiers avec IoT Hub</span><span class="sxs-lookup"><span data-stu-id="7639f-103">Upload files with IoT Hub</span></span>

<span data-ttu-id="7639f-104">Comme détaillé dans hello [points de terminaison IoT Hub] [ lnk-endpoints] article, un périphérique peut initier le chargement d’un fichier en envoyant une notification via un point de terminaison du périphérique (**/devices/ {deviceId} / fichiers**).</span><span class="sxs-lookup"><span data-stu-id="7639f-104">As detailed in hello [IoT Hub endpoints][lnk-endpoints] article, a device can initiate a file upload by sending a notification through a device-facing endpoint (**/devices/{deviceId}/files**).</span></span> <span data-ttu-id="7639f-105">Lorsqu’un appareil avertit IoT Hub qu’un téléchargement est terminé, IoT Hub envoie un message de notification de téléchargement de fichier via hello **/messages/servicebound/filenotifications** côté service de point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="7639f-105">When a device notifies IoT Hub that an upload is complete, IoT Hub sends a file upload notification message through hello **/messages/servicebound/filenotifications** service-facing endpoint.</span></span>

<span data-ttu-id="7639f-106">Au lieu de l’échange de messages via IoT Hub lui-même, IoT Hub au lieu de cela joue un tooan répartiteur associé compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="7639f-106">Instead of brokering messages through IoT Hub itself, IoT Hub instead acts as a dispatcher tooan associated Azure Storage account.</span></span> <span data-ttu-id="7639f-107">Un périphérique demande un jeton de stockage à partir du IoT Hub qui est spécifique toohello fichier hello périphérique veut tooupload.</span><span class="sxs-lookup"><span data-stu-id="7639f-107">A device requests a storage token from IoT Hub that is specific toohello file hello device wishes tooupload.</span></span> <span data-ttu-id="7639f-108">Appareil de Hello utilise hello URI SAS tooupload hello fichier toostorage, et lorsque hello téléchargement est terminé appareil de hello envoie une notification d’achèvement tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="7639f-108">hello device uses hello SAS URI tooupload hello file toostorage, and when hello upload is complete hello device sends a notification of completion tooIoT Hub.</span></span> <span data-ttu-id="7639f-109">IoT Hub vérifie le téléchargement du fichier hello est terminé et qu’il ajoute ensuite un fichier téléchargement notification message toohello orientées service fichier notification point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="7639f-109">IoT Hub checks hello file upload is complete and then adds a file upload notification message toohello service-facing file notification endpoint.</span></span>

<span data-ttu-id="7639f-110">Avant de télécharger un fichier de tooIoT Hub à partir d’un appareil, vous devez configurer votre concentrateur par [association d’un stockage Azure] [ lnk-associate-storage] tooit de compte.</span><span class="sxs-lookup"><span data-stu-id="7639f-110">Before you upload a file tooIoT Hub from a device, you must configure your hub by [associating an Azure Storage][lnk-associate-storage] account tooit.</span></span>

<span data-ttu-id="7639f-111">Votre appareil peut ensuite [initialiser un téléchargement] [ lnk-initialize] , puis [notifier IoT hub] [ lnk-notify] quand le téléchargement de hello se termine.</span><span class="sxs-lookup"><span data-stu-id="7639f-111">Your device can then [initialize an upload][lnk-initialize] and then [notify IoT hub][lnk-notify] when hello upload completes.</span></span> <span data-ttu-id="7639f-112">Si vous le souhaitez, lorsqu’un périphérique notifie IoT Hub téléchargement hello est terminée, service de hello peut générer un [message de notification][lnk-service-notification].</span><span class="sxs-lookup"><span data-stu-id="7639f-112">Optionally, when a device notifies IoT Hub that hello upload is complete, hello service can generate a [notification message][lnk-service-notification].</span></span>

### <a name="when-toouse"></a><span data-ttu-id="7639f-113">Lorsque toouse</span><span class="sxs-lookup"><span data-stu-id="7639f-113">When toouse</span></span>

<span data-ttu-id="7639f-114">Utilisez fichier télécharger toosend media les fichiers et les lots de télémétrie volumineux téléchargés par les appareils connectés par intermittence ou la bande passante toosave compressé.</span><span class="sxs-lookup"><span data-stu-id="7639f-114">Use file upload toosend media files and large telemetry batches uploaded by intermittently connected devices or compressed toosave bandwidth.</span></span>

<span data-ttu-id="7639f-115">Consultez trop[des conseils de communication de périphérique dans le cloud] [ lnk-d2c-guidance] en cas de doute entre l’utilisation des propriétés signalées, messages appareil-à-cloud ou téléchargement du fichier.</span><span class="sxs-lookup"><span data-stu-id="7639f-115">Refer too[Device-to-cloud communication guidance][lnk-d2c-guidance] if in doubt between using reported properties, device-to-cloud messages, or file upload.</span></span>

## <a name="associate-an-azure-storage-account-with-iot-hub"></a><span data-ttu-id="7639f-116">Association d’un compte Stockage Azure à IoT Hub</span><span class="sxs-lookup"><span data-stu-id="7639f-116">Associate an Azure Storage account with IoT Hub</span></span>

<span data-ttu-id="7639f-117">fonctionnalité de téléchargement de fichier toouse hello, vous devez d’abord lier un toohello de compte de stockage Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="7639f-117">toouse hello file upload functionality, you must first link an Azure Storage account toohello IoT Hub.</span></span> <span data-ttu-id="7639f-118">Vous pouvez effectuer cette tâche via hello [portail Azure][lnk-management-portal], ou par programmation via hello [fournisseur de ressources IoT Hub API REST] [ lnk-resource-provider-apis].</span><span class="sxs-lookup"><span data-stu-id="7639f-118">You can complete this task either through hello [Azure portal][lnk-management-portal], or programmatically through hello [IoT Hub resource provider REST APIs][lnk-resource-provider-apis].</span></span> <span data-ttu-id="7639f-119">Une fois que vous avez associé un compte de stockage Azure à votre IoT Hub, hello service retourne un URI SAS tooa périphérique lors de l’appareil de hello initie une demande de téléchargement de fichier.</span><span class="sxs-lookup"><span data-stu-id="7639f-119">Once you have associated an Azure Storage account with your IoT Hub, hello service returns a SAS URI tooa device when hello device initiates a file upload request.</span></span>

> [!NOTE]
> <span data-ttu-id="7639f-120">Hello [kits de développement logiciel Azure IoT] [ lnk-sdks] automatiquement la poignée de la récupération hello URI SAS, téléchargement du fichier de hello et la notification IoT Hub d’un téléchargement terminé.</span><span class="sxs-lookup"><span data-stu-id="7639f-120">hello [Azure IoT SDKs][lnk-sdks] automatically handle retrieving hello SAS URI, uploading hello file, and notifying IoT Hub of a completed upload.</span></span>


## <a name="initialize-a-file-upload"></a><span data-ttu-id="7639f-121">Initialiser un téléchargement de fichier</span><span class="sxs-lookup"><span data-stu-id="7639f-121">Initialize a file upload</span></span>
<span data-ttu-id="7639f-122">IoT Hub a un point de terminaison spécifiquement pour les périphériques toorequest un URI SAS pour tooupload de stockage un fichier.</span><span class="sxs-lookup"><span data-stu-id="7639f-122">IoT Hub has an endpoint specifically for devices toorequest a SAS URI for storage tooupload a file.</span></span> <span data-ttu-id="7639f-123">processus de téléchargement de fichier tooinitiate hello, appareil de hello envoie une demande POST trop`{iot hub}.azure-devices.net/devices/{deviceId}/files` avec hello suivant le corps JSON :</span><span class="sxs-lookup"><span data-stu-id="7639f-123">tooinitiate hello file upload process, hello device sends a POST request too`{iot hub}.azure-devices.net/devices/{deviceId}/files` with hello following JSON body:</span></span>

```json
{
    "blobName": "{name of hello file for which a SAS URI will be generated}"
}
```

<span data-ttu-id="7639f-124">IoT Hub renvoie hello données, quel périphérique hello utilise le fichier de hello tooupload suivantes :</span><span class="sxs-lookup"><span data-stu-id="7639f-124">IoT Hub returns hello following data, which hello device uses tooupload hello file:</span></span>

```json
{
    "correlationId": "somecorrelationid",
    "hostName": "contoso.azure-devices.net",
    "containerName": "testcontainer",
    "blobName": "test-device1/image.jpg",
    "sasToken": "1234asdfSAStoken"
}
```

### <a name="deprecated-initialize-a-file-upload-with-a-get"></a><span data-ttu-id="7639f-125">Déconseillé : initialiser un téléchargement de fichier avec une commande GET</span><span class="sxs-lookup"><span data-stu-id="7639f-125">Deprecated: initialize a file upload with a GET</span></span>

> [!NOTE]
> <span data-ttu-id="7639f-126">Cette section décrit les fonctionnalités déconseillées de façon tooreceive un SAS URI à partir de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="7639f-126">This section describes deprecated functionality for how tooreceive a SAS URI from IoT Hub.</span></span> <span data-ttu-id="7639f-127">Utiliser la méthode POST de hello décrit précédemment.</span><span class="sxs-lookup"><span data-stu-id="7639f-127">Use hello POST method described previously.</span></span>

<span data-ttu-id="7639f-128">IoT Hub a deux fichiers toosupport de points de terminaison REST hello tooget un URI SAS pour le stockage, téléchargez et hello autres concentrateur de IoT hello toonotify d’un téléchargement terminé.</span><span class="sxs-lookup"><span data-stu-id="7639f-128">IoT Hub has two REST endpoints toosupport file upload, one tooget hello SAS URI for storage and hello other toonotify hello IoT hub of a completed upload.</span></span> <span data-ttu-id="7639f-129">Hello appareil lance les processus de téléchargement de fichier hello en envoyant un concentrateur de IoT GET toohello à `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`.</span><span class="sxs-lookup"><span data-stu-id="7639f-129">hello device initiates hello file upload process by sending a GET toohello IoT hub at `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`.</span></span> <span data-ttu-id="7639f-130">IoT hub de Hello retourne :</span><span class="sxs-lookup"><span data-stu-id="7639f-130">hello IoT hub returns:</span></span>

* <span data-ttu-id="7639f-131">URI SAS spécifique toohello fichier toobe téléchargé.</span><span class="sxs-lookup"><span data-stu-id="7639f-131">A SAS URI specific toohello file toobe uploaded.</span></span>
* <span data-ttu-id="7639f-132">Un ID de corrélation toobe utilisé une fois le téléchargement de hello est terminé.</span><span class="sxs-lookup"><span data-stu-id="7639f-132">A correlation ID toobe used once hello upload is completed.</span></span>

## <a name="notify-iot-hub-of-a-completed-file-upload"></a><span data-ttu-id="7639f-133">Notifier IoT Hub de la fin du téléchargement d’un fichier</span><span class="sxs-lookup"><span data-stu-id="7639f-133">Notify IoT Hub of a completed file upload</span></span>

<span data-ttu-id="7639f-134">Appareil de Hello est chargé pour le téléchargement hello toostorage de fichier à l’aide du SDK de stockage Azure hello.</span><span class="sxs-lookup"><span data-stu-id="7639f-134">hello device is responsible for uploading hello file toostorage using hello Azure Storage SDKs.</span></span> <span data-ttu-id="7639f-135">Lorsque le téléchargement de hello est terminé, les appareils hello envoie une demande POST trop`{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` avec hello suivant le corps JSON :</span><span class="sxs-lookup"><span data-stu-id="7639f-135">When hello upload is complete, hello device sends a POST request too`{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` with hello following JSON body:</span></span>

```json
{
    "correlationId": "{correlation ID received from hello initial request}",
    "isSuccess": bool,
    "statusCode": XXX,
    "statusDescription": "Description of status"
}
```

<span data-ttu-id="7639f-136">Hello valeur `isSuccess` est une valeur Boolean indiquant si le fichier de hello a été téléchargé correctement.</span><span class="sxs-lookup"><span data-stu-id="7639f-136">hello value of `isSuccess` is a Boolean representing whether hello file was uploaded successfully.</span></span> <span data-ttu-id="7639f-137">Hello le code d’état de `statusCode` est hello d’état de téléchargement de hello de hello fichier toostorage et hello `statusDescription` correspond toohello `statusCode`.</span><span class="sxs-lookup"><span data-stu-id="7639f-137">hello status code for `statusCode` is hello status for hello upload of hello file toostorage, and hello `statusDescription` corresponds toohello `statusCode`.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="7639f-138">Rubriques de référence :</span><span class="sxs-lookup"><span data-stu-id="7639f-138">Reference topics:</span></span>

<span data-ttu-id="7639f-139">Hello rubriques de référence suivantes vous fournissent plus d’informations sur le téléchargement de fichiers à partir d’un appareil.</span><span class="sxs-lookup"><span data-stu-id="7639f-139">hello following reference topics provide you with more information about uploading files from a device.</span></span>

## <a name="file-upload-notifications"></a><span data-ttu-id="7639f-140">Notifications de téléchargement de fichier</span><span class="sxs-lookup"><span data-stu-id="7639f-140">File upload notifications</span></span>

<span data-ttu-id="7639f-141">Éventuellement, lorsqu’un périphérique avertit IoT Hub qu’un téléchargement est terminé, IoT Hub peut générer un message de notification qui contient l’emplacement de stockage et le nom hello du fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="7639f-141">Optionally, when a device notifies IoT Hub that an upload is complete, IoT Hub can generate a notification message that contains hello name and storage location of hello file.</span></span>

<span data-ttu-id="7639f-142">Comme l’explique la section [Points de terminaison][lnk-endpoints], IoT Hub fournit des notifications de chargement de fichiers sous la forme de messages par le biais d’un point de terminaison côté service (**/messages/servicebound/fileuploadnotifications**).</span><span class="sxs-lookup"><span data-stu-id="7639f-142">As explained in [Endpoints][lnk-endpoints], IoT Hub delivers file upload notifications through a service-facing endpoint (**/messages/servicebound/fileuploadnotifications**) as messages.</span></span> <span data-ttu-id="7639f-143">sémantique de réception Hello pour les notifications de téléchargement de fichier sont hello même que pour les messages cloud-à-appareil et avez hello même [cycle de vie du message][lnk-lifecycle].</span><span class="sxs-lookup"><span data-stu-id="7639f-143">hello receive semantics for file upload notifications are hello same as for cloud-to-device messages and have hello same [message lifecycle][lnk-lifecycle].</span></span> <span data-ttu-id="7639f-144">Chaque message récupérée à partir du point de terminaison de la notification de téléchargement de hello fichier est un enregistrement JSON avec hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="7639f-144">Each message retrieved from hello file upload notification endpoint is a JSON record with hello following properties:</span></span>

| <span data-ttu-id="7639f-145">Propriété</span><span class="sxs-lookup"><span data-stu-id="7639f-145">Property</span></span> | <span data-ttu-id="7639f-146">Description</span><span class="sxs-lookup"><span data-stu-id="7639f-146">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7639f-147">EnqueuedTimeUtc</span><span class="sxs-lookup"><span data-stu-id="7639f-147">EnqueuedTimeUtc</span></span> |<span data-ttu-id="7639f-148">Horodatage indiquant quand la notification de hello a été créée.</span><span class="sxs-lookup"><span data-stu-id="7639f-148">Timestamp indicating when hello notification was created.</span></span> |
| <span data-ttu-id="7639f-149">deviceId</span><span class="sxs-lookup"><span data-stu-id="7639f-149">DeviceId</span></span> |<span data-ttu-id="7639f-150">**DeviceId** de dispositif hello hello fichier a été téléchargé.</span><span class="sxs-lookup"><span data-stu-id="7639f-150">**DeviceId** of hello device which uploaded hello file.</span></span> |
| <span data-ttu-id="7639f-151">BlobUri</span><span class="sxs-lookup"><span data-stu-id="7639f-151">BlobUri</span></span> |<span data-ttu-id="7639f-152">URI du fichier de hello téléchargé.</span><span class="sxs-lookup"><span data-stu-id="7639f-152">URI of hello uploaded file.</span></span> |
| <span data-ttu-id="7639f-153">BlobName</span><span class="sxs-lookup"><span data-stu-id="7639f-153">BlobName</span></span> |<span data-ttu-id="7639f-154">Nom de hello le fichier téléchargé.</span><span class="sxs-lookup"><span data-stu-id="7639f-154">Name of hello uploaded file.</span></span> |
| <span data-ttu-id="7639f-155">LastUpdatedTime</span><span class="sxs-lookup"><span data-stu-id="7639f-155">LastUpdatedTime</span></span> |<span data-ttu-id="7639f-156">Horodatage indiquant quand hello dernière mise à jour.</span><span class="sxs-lookup"><span data-stu-id="7639f-156">Timestamp indicating when hello file was last updated.</span></span> |
| <span data-ttu-id="7639f-157">BlobSizeInBytes</span><span class="sxs-lookup"><span data-stu-id="7639f-157">BlobSizeInBytes</span></span> |<span data-ttu-id="7639f-158">Taille de hello le fichier téléchargé.</span><span class="sxs-lookup"><span data-stu-id="7639f-158">Size of hello uploaded file.</span></span> |

<span data-ttu-id="7639f-159">**Exemple**.</span><span class="sxs-lookup"><span data-stu-id="7639f-159">**Example**.</span></span> <span data-ttu-id="7639f-160">Cet exemple montre le corps hello de télécharger le message de notification.</span><span class="sxs-lookup"><span data-stu-id="7639f-160">This example shows hello body of a file upload notification message.</span></span>

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

## <a name="file-upload-notification-configuration-options"></a><span data-ttu-id="7639f-161">Options de configuration de notification de téléchargement de fichier</span><span class="sxs-lookup"><span data-stu-id="7639f-161">File upload notification configuration options</span></span>

<span data-ttu-id="7639f-162">Chaque hub IoT expose hello des options de configuration pour les notifications de téléchargement de fichier suivantes :</span><span class="sxs-lookup"><span data-stu-id="7639f-162">Each IoT hub exposes hello following configuration options for file upload notifications:</span></span>

| <span data-ttu-id="7639f-163">Propriété</span><span class="sxs-lookup"><span data-stu-id="7639f-163">Property</span></span> | <span data-ttu-id="7639f-164">Description</span><span class="sxs-lookup"><span data-stu-id="7639f-164">Description</span></span> | <span data-ttu-id="7639f-165">Plage et valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="7639f-165">Range and default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7639f-166">**enableFileUploadNotifications**</span><span class="sxs-lookup"><span data-stu-id="7639f-166">**enableFileUploadNotifications**</span></span> |<span data-ttu-id="7639f-167">Contrôle si les notifications de téléchargement de fichier sont écrits de point de terminaison notifications toohello fichier.</span><span class="sxs-lookup"><span data-stu-id="7639f-167">Controls whether file upload notifications are written toohello file notifications endpoint.</span></span> |<span data-ttu-id="7639f-168">Valeur booléenne.</span><span class="sxs-lookup"><span data-stu-id="7639f-168">Bool.</span></span> <span data-ttu-id="7639f-169">Par défaut : True.</span><span class="sxs-lookup"><span data-stu-id="7639f-169">Default: True.</span></span> |
| <span data-ttu-id="7639f-170">**fileNotifications.ttlAsIso8601**</span><span class="sxs-lookup"><span data-stu-id="7639f-170">**fileNotifications.ttlAsIso8601**</span></span> |<span data-ttu-id="7639f-171">Durée de vie par défaut des notifications de téléchargement de fichier.</span><span class="sxs-lookup"><span data-stu-id="7639f-171">Default TTL for file upload notifications.</span></span> |<span data-ttu-id="7639f-172">Intervalle de ISO_8601 des too48H (au minimum 1 minute).</span><span class="sxs-lookup"><span data-stu-id="7639f-172">ISO_8601 interval up too48H (minimum 1 minute).</span></span> <span data-ttu-id="7639f-173">Par défaut : 1 heure.</span><span class="sxs-lookup"><span data-stu-id="7639f-173">Default: 1 hour.</span></span> |
| <span data-ttu-id="7639f-174">**fileNotifications.lockDuration**</span><span class="sxs-lookup"><span data-stu-id="7639f-174">**fileNotifications.lockDuration**</span></span> |<span data-ttu-id="7639f-175">Durée de verrouillage pour la file d’attente des notifications de téléchargement de fichier hello.</span><span class="sxs-lookup"><span data-stu-id="7639f-175">Lock duration for hello file upload notifications queue.</span></span> |<span data-ttu-id="7639f-176">too300 5 secondes (5 secondes au minimum).</span><span class="sxs-lookup"><span data-stu-id="7639f-176">5 too300 seconds (minimum 5 seconds).</span></span> <span data-ttu-id="7639f-177">Par défaut : 60 secondes.</span><span class="sxs-lookup"><span data-stu-id="7639f-177">Default: 60 seconds.</span></span> |
| <span data-ttu-id="7639f-178">**fileNotifications.maxDeliveryCount**</span><span class="sxs-lookup"><span data-stu-id="7639f-178">**fileNotifications.maxDeliveryCount**</span></span> |<span data-ttu-id="7639f-179">Nombre maximal de diffusions pour le fichier de hello télécharger la file d’attente de notification.</span><span class="sxs-lookup"><span data-stu-id="7639f-179">Maximum delivery count for hello file upload notification queue.</span></span> |<span data-ttu-id="7639f-180">1 too100.</span><span class="sxs-lookup"><span data-stu-id="7639f-180">1 too100.</span></span> <span data-ttu-id="7639f-181">Par défaut : 100.</span><span class="sxs-lookup"><span data-stu-id="7639f-181">Default: 100.</span></span> |

## <a name="additional-reference-material"></a><span data-ttu-id="7639f-182">Matériel de référence supplémentaire</span><span class="sxs-lookup"><span data-stu-id="7639f-182">Additional reference material</span></span>

<span data-ttu-id="7639f-183">Les autres rubriques de référence de hello guide du développeur IoT Hub sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="7639f-183">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="7639f-184">[Points de terminaison IoT Hub] [ lnk-endpoints] décrit hello différents points de terminaison qui expose de chaque IoT hub pour les opérations de gestion et d’exécution.</span><span class="sxs-lookup"><span data-stu-id="7639f-184">[IoT Hub endpoints][lnk-endpoints] describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="7639f-185">[Limitation et les quotas] [ lnk-quotas] décrit les quotas hello et la limitation des comportements qui s’appliquent toohello IoT Hub service.</span><span class="sxs-lookup"><span data-stu-id="7639f-185">[Throttling and quotas][lnk-quotas] describes hello quotas and throttling behaviors that apply toohello IoT Hub service.</span></span>
* <span data-ttu-id="7639f-186">[Azure IoT périphérique et service kits de développement logiciel] [ lnk-sdks] listes hello langue différents kits de développement logiciel vous pouvez utiliser lorsque vous développez des applications de périphérique et le service qui interagissent avec IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="7639f-186">[Azure IoT device and service SDKs][lnk-sdks] lists hello various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="7639f-187">[Langage de requête IoT Hub] [ lnk-query] décrit le langage de requête hello vous pouvez utiliser les informations de tooretrieve à partir de IoT Hub sur votre jumeaux de périphérique et les travaux.</span><span class="sxs-lookup"><span data-stu-id="7639f-187">[IoT Hub query language][lnk-query] describes hello query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="7639f-188">[Prise en charge IoT Hub MQTT] [ lnk-devguide-mqtt] fournit plus d’informations sur la prise en charge IoT Hub pour le protocole MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="7639f-188">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7639f-189">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7639f-189">Next steps</span></span>

<span data-ttu-id="7639f-190">Maintenant vous avez appris comment tooupload des fichiers à partir d’appareils à l’aide de IoT Hub, vous intéresser hello IoT Hub développeur guide rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="7639f-190">Now you have learned how tooupload files from devices using IoT Hub, you may be interested in hello following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="7639f-191">[Gérer les identités des appareils dans IoT Hub][lnk-devguide-identities]</span><span class="sxs-lookup"><span data-stu-id="7639f-191">[Manage device identities in IoT Hub][lnk-devguide-identities]</span></span>
* <span data-ttu-id="7639f-192">[Contrôle l’accès tooIoT Hub][lnk-devguide-security]</span><span class="sxs-lookup"><span data-stu-id="7639f-192">[Control access tooIoT Hub][lnk-devguide-security]</span></span>
* <span data-ttu-id="7639f-193">[Utiliser les configurations et état du périphérique jumeaux toosynchronize][lnk-devguide-device-twins]</span><span class="sxs-lookup"><span data-stu-id="7639f-193">[Use device twins toosynchronize state and configurations][lnk-devguide-device-twins]</span></span>
* <span data-ttu-id="7639f-194">[Appeler une méthode directe sur un appareil][lnk-devguide-directmethods]</span><span class="sxs-lookup"><span data-stu-id="7639f-194">[Invoke a direct method on a device][lnk-devguide-directmethods]</span></span>
* <span data-ttu-id="7639f-195">[Planifier des travaux sur plusieurs appareils][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="7639f-195">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="7639f-196">Si vous souhaitez que tootry certains des concepts hello décrits dans cet article, peut vous intéresser hello suivant IoT Hub didacticiel :</span><span class="sxs-lookup"><span data-stu-id="7639f-196">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorial:</span></span>

* <span data-ttu-id="7639f-197">[Fichiers tooupload à partir d’appareils toohello de cloud avec IoT Hub][lnk-fileupload-tutorial]</span><span class="sxs-lookup"><span data-stu-id="7639f-197">[How tooupload files from devices toohello cloud with IoT Hub][lnk-fileupload-tutorial]</span></span>

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
