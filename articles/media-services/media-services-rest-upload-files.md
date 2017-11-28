---
title: "fichiers aaaUpload dans un compte Media Services à l’aide de REST | Documents Microsoft"
description: "Découvrez comment tooget média du contenu dans Media Services création et téléchargement d’éléments multimédias."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 41df7cbe-b8e2-48c1-a86c-361ec4e5251f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 2a92cecdc32d747d7a478946f069c15931eb32b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-rest"></a><span data-ttu-id="0f2cf-103">Charger des fichiers dans un compte Media Services à l’aide de REST</span><span class="sxs-lookup"><span data-stu-id="0f2cf-103">Upload files into a Media Services account using REST</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0f2cf-104">.NET</span><span class="sxs-lookup"><span data-stu-id="0f2cf-104">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="0f2cf-105">REST</span><span class="sxs-lookup"><span data-stu-id="0f2cf-105">REST</span></span>](media-services-rest-upload-files.md)
> * [<span data-ttu-id="0f2cf-106">Portail</span><span class="sxs-lookup"><span data-stu-id="0f2cf-106">Portal</span></span>](media-services-portal-upload-files.md)
> 
> 

<span data-ttu-id="0f2cf-107">Dans Media Services, vous téléchargez vos fichiers numériques dans une ressource.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-107">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="0f2cf-108">Hello [Asset](https://docs.microsoft.com/rest/api/media/operations/asset) entité peut contenir vidéo, audio, images, collections de miniatures, texte assure le suivi et sous-titres fichiers (et les métadonnées hello sur ces fichiers.)  Une fois que les fichiers de hello sont téléchargés en ressource de hello, votre contenu est stocké en toute sécurité dans le cloud hello pour le traitement et la diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-108">hello [Asset](https://docs.microsoft.com/rest/api/media/operations/asset) entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.)  Once hello files are uploaded into hello asset, your content is stored securely in hello cloud for further processing and streaming.</span></span> 

> [!NOTE]
> <span data-ttu-id="0f2cf-109">Hello suivant considérations s’appliquent :</span><span class="sxs-lookup"><span data-stu-id="0f2cf-109">hello following considerations apply:</span></span>
> 
> * <span data-ttu-id="0f2cf-110">Media Services utilise la valeur hello hello IAssetFile.Name propriété lors de la génération d’URL pour hello de diffusion en continu de contenu (par exemple, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Pour cette raison, l’encodage par pourcentage n’est pas autorisé.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-110">Media Services uses hello value of hello IAssetFile.Name property when building URLs for hello streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="0f2cf-111">Hello valeur Hello **nom** propriété ne peut pas avoir un des éléments suivants de hello [% réservés d’encodage de caractères](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): ! *' () ; : @& = + $, / ? % # [] ».</span><span class="sxs-lookup"><span data-stu-id="0f2cf-111">hello value of hello **Name** property cannot have any of hello following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="0f2cf-112">En outre, il ne peut exister un '.' pour l’extension de nom de fichier hello.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-112">Also, there can only be one '.' for hello file name extension.</span></span>
> * <span data-ttu-id="0f2cf-113">la longueur du nom de hello Hello ne doit pas dépasser 260 caractères.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-113">hello length of hello name should not be greater than 260 characters.</span></span>
> * <span data-ttu-id="0f2cf-114">Il existe une taille de fichier maximale toohello limite pris en charge pour le traitement dans Media Services.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-114">There is a limit toohello maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="0f2cf-115">Consultez [cela](media-services-quotas-and-limitations.md) pour plus d’informations sur la limite de taille de fichier hello.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-115">Please see [this](media-services-quotas-and-limitations.md) topic for details about hello file size limitation.</span></span>
> 

<span data-ttu-id="0f2cf-116">flux de travail Hello pour le téléchargement des éléments multimédias est divisé en hello les sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="0f2cf-116">hello basic workflow for uploading Assets is divided into hello following sections:</span></span>

* <span data-ttu-id="0f2cf-117">Créer une ressource</span><span class="sxs-lookup"><span data-stu-id="0f2cf-117">Create an Asset</span></span>
* <span data-ttu-id="0f2cf-118">Chiffrer une ressource (facultatif)</span><span class="sxs-lookup"><span data-stu-id="0f2cf-118">Encrypt an Asset (Optional)</span></span>
* <span data-ttu-id="0f2cf-119">Télécharger un stockage tooblob de fichier</span><span class="sxs-lookup"><span data-stu-id="0f2cf-119">Upload a file tooblob storage</span></span>

<span data-ttu-id="0f2cf-120">AMS vous permet également de ressources tooupload en bloc.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-120">AMS also enables you tooupload assets in bulk.</span></span> <span data-ttu-id="0f2cf-121">Pour plus d’informations, consultez [cette](media-services-rest-upload-files.md#upload_in_bulk) section.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-121">For more information, see [this](media-services-rest-upload-files.md#upload_in_bulk) section.</span></span>

> [!NOTE]
> <span data-ttu-id="0f2cf-122">Lors de l’accès aux entités dans Media Services, vous devez définir les valeurs et les champs d’en-tête spécifiques dans vos requêtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-122">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="0f2cf-123">Pour plus d'informations, consultez [Installation pour le développement REST API de Media Services](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="0f2cf-123">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
> 

## <a name="connect-toomedia-services"></a><span data-ttu-id="0f2cf-124">Connecter les Services de tooMedia</span><span class="sxs-lookup"><span data-stu-id="0f2cf-124">Connect tooMedia Services</span></span>

<span data-ttu-id="0f2cf-125">Pour plus d’informations sur la façon dont tooconnect toohello AMS API, consultez [hello accès API Azure Media Services avec l’authentification Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="0f2cf-125">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="0f2cf-126">Après vous être connecté toohttps://media.windows.net, vous recevrez une redirection 301 spécifiant un autre URI de Media Services.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-126">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="0f2cf-127">Vous devez effectuer les appels suivants toohello nouvel URI.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-127">You must make subsequent calls toohello new URI.</span></span>

## <a name="upload-assets"></a><span data-ttu-id="0f2cf-128">Téléchargement de ressources</span><span class="sxs-lookup"><span data-stu-id="0f2cf-128">Upload assets</span></span>

### <a name="create-an-asset"></a><span data-ttu-id="0f2cf-129">Créer une ressource</span><span class="sxs-lookup"><span data-stu-id="0f2cf-129">Create an asset</span></span>

<span data-ttu-id="0f2cf-130">Une ressource est un conteneur pour plusieurs types ou ensembles d’objets dans Media Services, y compris des fichiers vidéo, audio, des images, des collections de miniatures, des pistes textuelles et des légendes.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-130">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="0f2cf-131">Bonjour API REST, création d’un élément multimédia requiert l’envoi de POST solliciter des Services de tooMedia et placer toutes les informations de propriété concernant votre élément multimédia dans le corps de la demande hello.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-131">In hello REST API, creating an Asset requires sending POST request tooMedia Services and placing any property information about your asset in hello request body.</span></span>

<span data-ttu-id="0f2cf-132">Une des propriétés hello que vous pouvez spécifier lorsque la création d’un élément multimédia est **Options**.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-132">One of hello properties that you can specify when creating an asset is **Options**.</span></span> <span data-ttu-id="0f2cf-133">**Options** est une valeur d’énumération qui décrit les options de chiffrement hello un élément multimédia peut être créé avec.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-133">**Options** is an enumeration value that describes hello encryption options that an Asset can be created with.</span></span> <span data-ttu-id="0f2cf-134">Une valeur valide est une des valeurs hello dans liste hello ci-dessous, pas une combinaison de valeurs.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-134">A valid value is one of hello values from hello list below, not a combination of values.</span></span> 

* <span data-ttu-id="0f2cf-135">**None** = **0** : Aucun chiffrement ne sera utilisé.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-135">**None** = **0**: No encryption will be used.</span></span> <span data-ttu-id="0f2cf-136">Il s’agit de valeur par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-136">This is hello default value.</span></span> <span data-ttu-id="0f2cf-137">À noter que quand vous utilisez cette option, votre contenu n’est pas protégé pendant le transit ou le repos dans le stockage.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-137">Note that when using this option your content is not protected in transit or at rest in storage.</span></span>
    <span data-ttu-id="0f2cf-138">Si vous envisagez de toodeliver un fichier MP4 à l’aide d’un téléchargement progressif, utilisez cette option.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-138">If you plan toodeliver an MP4 using progressive download, use this option.</span></span> 
* <span data-ttu-id="0f2cf-139">**StorageEncrypted** = **1**: spécifiez si vous souhaitez pour votre toobe de fichiers chiffré avec chiffrement AES-256 bits pour le téléchargement et de stockage.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-139">**StorageEncrypted** = **1**: Specify if you want for your files toobe encrypted with AES-256 bit encryption for upload and storage.</span></span>
  
    <span data-ttu-id="0f2cf-140">Si votre ressource est stockée sous forme chiffrée, vous devez configurer une stratégie de remise de ressources.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-140">If your asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="0f2cf-141">Pour plus d'informations, consultez [Configuration de la stratégie de remise de ressources](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="0f2cf-141">For more information see [Configuring asset delivery policy](media-services-rest-configure-asset-delivery-policy.md).</span></span>
* <span data-ttu-id="0f2cf-142">**CommonEncryptionProtected** = **2** : spécifie si vous téléchargez des fichiers protégés par une méthode de chiffrement commune (comme PlayReady).</span><span class="sxs-lookup"><span data-stu-id="0f2cf-142">**CommonEncryptionProtected** = **2**: Specify if you are uploading files protected with a common encryption method (such as PlayReady).</span></span> 
* <span data-ttu-id="0f2cf-143">**EnvelopeEncryptionProtected** = **4** : indique si vous téléchargez un contenu au format HLS chiffré avec des fichiers AES.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-143">**EnvelopeEncryptionProtected** = **4**: Specify if you are uploading HLS encrypted with AES files.</span></span> <span data-ttu-id="0f2cf-144">Notez que les fichiers hello doivent avoir été codés et chiffrés par Transform Manager.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-144">Note that hello files must have been encoded and encrypted by Transform Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="0f2cf-145">Si votre élément multimédia utilise le chiffrement, vous devez créer un **ContentKey** et liez-la tooyour actifs comme décrit dans la rubrique suivante de hello :[comment toocreate une ContentKey](media-services-rest-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="0f2cf-145">If your asset will use encryption, you must create a **ContentKey** and link it tooyour asset as described in hello following topic:[How toocreate a ContentKey](media-services-rest-create-contentkey.md).</span></span> <span data-ttu-id="0f2cf-146">Notez que, après avoir téléchargé les fichiers hello en ressource de hello, vous devez tooupdate propriétés de chiffrement hello sur hello **AssetFile** entité avec les valeurs hello que vous avez obtenus lors de hello **Asset** chiffrement.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-146">Note that after you upload hello files into hello asset, you need tooupdate hello encryption properties on hello **AssetFile** entity with hello values you got during hello **Asset** encryption.</span></span> <span data-ttu-id="0f2cf-147">Cela à l’aide de hello **fusion** requête HTTP.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-147">Do it by using hello **MERGE** HTTP request.</span></span> 
> 
> 

<span data-ttu-id="0f2cf-148">Hello suivant montre l’exemple de comment toocreate un élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-148">hello following example shows how toocreate an asset.</span></span>

<span data-ttu-id="0f2cf-149">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="0f2cf-149">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Assets HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"Name":"BigBuckBunny.mp4"}

<span data-ttu-id="0f2cf-150">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="0f2cf-150">**HTTP Response**</span></span>

<span data-ttu-id="0f2cf-151">En cas de réussite, suivant de hello est retournée :</span><span class="sxs-lookup"><span data-stu-id="0f2cf-151">If successful, hello following is returned:</span></span>

    HTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 452
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Assets('nb%3Acid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: c59de965-bc89-4295-9a57-75d897e5221e
    request-id: e98be122-ae09-473a-8072-0ccd234a0657
    x-ms-request-id: e98be122-ae09-473a-8072-0ccd234a0657
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:06:40 GMT
    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets/@Element",
       "Id":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "State":0,
       "Created":"2015-01-18T22:06:40.6010903Z",
       "LastModified":"2015-01-18T22:06:40.6010903Z",
       "AlternateId":null,
       "Name":"BigBuckBunny.mp4",
       "Options":0,
       "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StorageAccountName":"storagetestaccount001"
    }

### <a name="create-an-assetfile"></a><span data-ttu-id="0f2cf-152">Création d’un AssetFile</span><span class="sxs-lookup"><span data-stu-id="0f2cf-152">Create an AssetFile</span></span>
<span data-ttu-id="0f2cf-153">Hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entité représente un fichier vidéo ou audio qui est stocké dans un conteneur d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-153">hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="0f2cf-154">Un fichier de ressources est toujours associé à une ressource et une ressource peut contenir un ou plusieurs fichiers de ressources.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-154">An asset file is always associated with an asset, and an asset may contain one or many asset files.</span></span> <span data-ttu-id="0f2cf-155">tâche d’encodeur Media Services Hello échoue si un objet de fichier actif n’est pas associé à un fichier numérique dans un conteneur d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-155">hello Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="0f2cf-156">Notez que hello **AssetFile** instance et le fichier multimédia lui-même de hello sont deux objets distincts.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-156">Note that hello **AssetFile** instance and hello actual media file are two distinct objects.</span></span> <span data-ttu-id="0f2cf-157">instance AssetFile de Hello contient des métadonnées sur le fichier du média hello, tandis que le fichier du média hello contient le contenu du média réel hello.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-157">hello AssetFile instance contains metadata about hello media file, while hello media file contains hello actual media content.</span></span>

<span data-ttu-id="0f2cf-158">Après avoir téléchargé votre fichier multimédia numérique sur un conteneur d’objets blob, vous allez utiliser hello **fusion** tooupdate hello AssetFile HTTP demande des informations sur votre fichier multimédia (comme indiqué plus loin dans la rubrique de hello).</span><span class="sxs-lookup"><span data-stu-id="0f2cf-158">After you upload your digital media file into a blob container, you will use hello **MERGE** HTTP request tooupdate hello AssetFile with information about your media file (as shown later in hello topic).</span></span> 

<span data-ttu-id="0f2cf-159">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="0f2cf-159">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Files HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net
    Content-Length: 164

    {  
       "IsEncrypted":"false",
       "IsPrimary":"false",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }

<span data-ttu-id="0f2cf-160">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="0f2cf-160">**HTTP Response**</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 535
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5')
    Server: Microsoft-IIS/8.5
    request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    x-ms-request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 00:34:07 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Files/@Element",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "Name":"BigBuckBunny.mp4",
       "ContentFileSize":"0",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "EncryptionVersion":null,
       "EncryptionScheme":null,
       "IsEncrypted":false,
       "EncryptionKeyId":null,
       "InitializationVector":null,
       "IsPrimary":false,
       "LastModified":"2015-01-19T00:34:08.1934137Z",
       "Created":"2015-01-19T00:34:08.1934137Z",
       "MimeType":"video/mp4",
       "ContentChecksum":null
    }

### <a name="creating-hello-accesspolicy-with-write-permission"></a><span data-ttu-id="0f2cf-161">Création de hello AccessPolicy avec autorisation d’écriture.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-161">Creating hello AccessPolicy with write permission.</span></span>

>[!NOTE]
><span data-ttu-id="0f2cf-162">Un nombre limite de 1 000 000 a été défini pour les différentes stratégies AMS (par exemple, pour la stratégie de localisateur ou pour ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="0f2cf-162">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="0f2cf-163">Vous devez utiliser hello ID de stratégie même si vous utilisez toujours hello même jours / autorisations d’accès, par exemple, les stratégies pour les localisateurs sont tooremain prévue en place pendant une longue période (non-téléchargement stratégies).</span><span class="sxs-lookup"><span data-stu-id="0f2cf-163">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="0f2cf-164">Pour plus d’informations, consultez [cette rubrique](media-services-dotnet-manage-entities.md#limit-access-policies) .</span><span class="sxs-lookup"><span data-stu-id="0f2cf-164">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="0f2cf-165">Avant de télécharger des fichiers dans le stockage d’objets blob, définissez l’accès de hello droits de stratégie pour l’écriture de tooan actif.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-165">Before uploading any files into blob storage, set hello access policy rights for writing tooan asset.</span></span> <span data-ttu-id="0f2cf-166">toodo que, VALIDEZ un toohello de demande HTTP entité de stratégies d’accès défini.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-166">toodo that, POST an HTTP request toohello AccessPolicies entity set.</span></span> <span data-ttu-id="0f2cf-167">N’oubliez pas de définir une valeur DurationInMinutes après la création ou vous recevrez en réponse un message d’erreur interne de serveur 500.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-167">Define a DurationInMinutes value upon creation or you will receive a 500 Internal Server error message back in response.</span></span> <span data-ttu-id="0f2cf-168">Pour plus d’informations sur AccessPolicies, consultez [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span><span class="sxs-lookup"><span data-stu-id="0f2cf-168">For more information on AccessPolicies, see [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span></span>

<span data-ttu-id="0f2cf-169">Hello suivant montre l’exemple de comment toocreate une stratégie d’accès :</span><span class="sxs-lookup"><span data-stu-id="0f2cf-169">hello following example shows how toocreate an AccessPolicy:</span></span>

<span data-ttu-id="0f2cf-170">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="0f2cf-170">**HTTP Request**</span></span>

    POST https://media.windows.net/api/AccessPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"Name":"NewUploadPolicy", "DurationInMinutes":"440", "Permissions":"2"} 

<span data-ttu-id="0f2cf-171">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="0f2cf-171">**HTTP Request**</span></span>

    If successful, hello following response is returned:

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 312
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae')
    Server: Microsoft-IIS/8.5
    request-id: 74c74545-7e0a-4cd6-a440-c1c48074a970
    x-ms-request-id: 74c74545-7e0a-4cd6-a440-c1c48074a970
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:18:06 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#AccessPolicies/@Element",
       "Id":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "Created":"2015-01-18T22:18:06.6370575Z",
       "LastModified":"2015-01-18T22:18:06.6370575Z",
       "Name":"NewUploadPolicy",
       "DurationInMinutes":440.0,
       "Permissions":2
    }

### <a name="get-hello-upload-url"></a><span data-ttu-id="0f2cf-172">Obtenir hello télécharger l’URL</span><span class="sxs-lookup"><span data-stu-id="0f2cf-172">Get hello Upload URL</span></span>
<span data-ttu-id="0f2cf-173">tooreceive hello URL de téléchargement réelle, créer un localisateur SAS.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-173">tooreceive hello actual upload URL, create a SAS Locator.</span></span> <span data-ttu-id="0f2cf-174">Les localisateurs définissent l’heure de début de hello et le type du point de terminaison de connexion pour les clients qui tooaccess des fichiers dans un élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-174">Locators define hello start time and type of connection endpoint for clients that want tooaccess Files in an Asset.</span></span> <span data-ttu-id="0f2cf-175">Vous pouvez créer plusieurs entités Locator pour une donnée AccessPolicy et Asset paire toohandle client différents besoins et demandes.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-175">You can create multiple Locator entities for a given AccessPolicy and Asset pair toohandle different client requests and needs.</span></span> <span data-ttu-id="0f2cf-176">Chacun de ces localisateurs utilisent la valeur de StartTime hello plus la valeur DurationInMinutes hello hello AccessPolicy toodetermine hello durée une URL peut être utilisée.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-176">Each of these Locators use hello StartTime value plus hello DurationInMinutes value of hello AccessPolicy toodetermine hello length of time a URL can be used.</span></span> <span data-ttu-id="0f2cf-177">Pour plus d’informations, consultez la rubrique [Localisateur](https://docs.microsoft.com/rest/api/media/operations/locator).</span><span class="sxs-lookup"><span data-stu-id="0f2cf-177">For more information, see [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>

<span data-ttu-id="0f2cf-178">Une URL SAS a hello suivant le format :</span><span class="sxs-lookup"><span data-stu-id="0f2cf-178">A SAS URL has hello following format:</span></span>

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

<span data-ttu-id="0f2cf-179">Certaines considérations s’appliquent :</span><span class="sxs-lookup"><span data-stu-id="0f2cf-179">Some considerations apply:</span></span>

* <span data-ttu-id="0f2cf-180">Vous ne pouvez avoir plus de cinq localisateurs uniques associés à une ressource donnée.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-180">You cannot have more than five unique Locators associated with a given Asset at one time.</span></span> <span data-ttu-id="0f2cf-181">Pour plus d’informations, consultez la rubrique Localisateur.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-181">For more information, see Locator.</span></span>
* <span data-ttu-id="0f2cf-182">Si vous avez besoin de tooupload vos fichiers immédiatement, vous devez définir les minutes de toofive valeur StartTime avant hello heure actuelle.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-182">If you need tooupload your files immediately, you should set your StartTime value toofive minutes before hello current time.</span></span> <span data-ttu-id="0f2cf-183">Cela vient du fait qu’il peut exister un décalage horaire entre votre ordinateur client et Media Services.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-183">This is because there may be clock skew between your client machine and Media Services.</span></span> <span data-ttu-id="0f2cf-184">En outre, votre valeur StartTime doit être hello respectant le format de date/heure : AAAA-MM-JJThh (par exemple, « 2014-05-23T17:53:50Z »).</span><span class="sxs-lookup"><span data-stu-id="0f2cf-184">Also, your StartTime value must be in hello following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>    
* <span data-ttu-id="0f2cf-185">Il peut y avoir un 30 à 40 secondes après la création d’un localisateur toowhen, il est disponible pour une utilisation de retarder.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-185">There may be a 30-40 second delay after a Locator is created toowhen it is available for use.</span></span> <span data-ttu-id="0f2cf-186">Ce problème s’applique tooboth URL SAS et les localisateurs d’origine.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-186">This issue applies tooboth SAS URL and Origin Locators.</span></span>

<span data-ttu-id="0f2cf-187">Bonjour à l’exemple suivant montre comment toocreate un localisateur d’URL SAS, tel que défini par hello la propriété de Type dans le corps de la demande hello (« 1 » pour un localisateur SAS) et « 2 » pour un localisateur d’origine à la demande.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-187">hello following example shows how toocreate a SAS URL Locator, as defined by hello Type property in hello request body ("1" for a SAS locator and "2" for an On-Demand origin locator).</span></span> <span data-ttu-id="0f2cf-188">Hello **chemin d’accès** propriété retournée contient les URL de hello que vous devez utiliser tooupload votre fichier.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-188">hello **Path** property returned contains hello URL that you must use tooupload your file.</span></span>

<span data-ttu-id="0f2cf-189">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="0f2cf-189">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Locators HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net
    {  
       "AccessPolicyId":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "AssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StartTime":"2015-02-18T16:45:53",
       "Type":1
    }

<span data-ttu-id="0f2cf-190">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="0f2cf-190">**HTTP Response**</span></span>

<span data-ttu-id="0f2cf-191">En cas de réussite, hello suivant la réponse est retournée :</span><span class="sxs-lookup"><span data-stu-id="0f2cf-191">If successful, hello following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 949
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54')
    Server: Microsoft-IIS/8.5
    request-id: 2adeb1f8-89c5-4cc8-aa4f-08cdfef33ae0
    x-ms-request-id: 2adeb1f8-89c5-4cc8-aa4f-08cdfef33ae0
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 03:01:29 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Locators/@Element",
       "Id":"nb:lid:UUID:af57bdd8-6751-4e84-b403-f3c140444b54",
       "ExpirationDateTime":"2015-02-19T00:05:53",
       "Type":1,
       "Path":"https://storagetestaccount001.blob.core.windows.net/asset-f438649c-313c-46e2-8d68-7d2550288247?sv=2012-02-12&sr=c&si=af57bdd8-6751-4e84-b403-f3c140444b54&sig=fE4btwEfZtVQFeC0Wh3Kwks2OFPQfzl5qTMW5YytiuY%3D&st=2015-02-18T16%3A45%3A53Z&se=2015-02-19T00%3A05%3A53Z",
       "BaseUri":"https://storagetestaccount001.blob.core.windows.net/asset-f438649c-313c-46e2-8d68-7d2550288247",
       "ContentAccessComponent":"?sv=2012-02-12&sr=c&si=af57bdd8-6751-4e84-b403-f3c140444b54&sig=fE4btwEfZtVQFeC0Wh3Kwks2OFPQfzl5qTMW5YytiuY%3D&st=2015-02-18T16%3A45%3A53Z&se=2015-02-19T00%3A05%3A53Z",
       "AccessPolicyId":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "AssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StartTime":"2015-02-18T16:45:53",
       "Name":null
    }

### <a name="upload-a-file-into-a-blob-storage-container"></a><span data-ttu-id="0f2cf-192">Téléchargement d’un fichier dans un conteneur de stockage d’objets blob</span><span class="sxs-lookup"><span data-stu-id="0f2cf-192">Upload a file into a blob storage container</span></span>
<span data-ttu-id="0f2cf-193">Une fois que vous avez hello AccessPolicy et l’ensemble de la recherche, le fichier hello est tooan téléchargé conteneur de stockage d’objets Blob Azure à l’aide de hello API REST de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-193">Once you have hello AccessPolicy and Locator set, hello actual file is uploaded tooan Azure Blob Storage container using hello Azure Storage REST APIs.</span></span> <span data-ttu-id="0f2cf-194">Vous devez télécharger les fichiers hello en tant qu’objets BLOB de blocs.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-194">You must upload hello files as block blobs.</span></span> <span data-ttu-id="0f2cf-195">Les objets blob de pages ne sont pas pris en charge par Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-195">Page blobs are not supported by Azure Media Services.</span></span>  

> [!NOTE]
> <span data-ttu-id="0f2cf-196">Vous devez ajouter le nom de fichier hello pour le fichier de hello souhaité tooupload toohello recherche **chemin d’accès** valeur reçue dans la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-196">You must add hello file name for hello file you want tooupload toohello Locator **Path** value received in hello previous section.</span></span> <span data-ttu-id="0f2cf-197">Par exemple, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="0f2cf-197">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="0f2cf-198">.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-198">.</span></span> <span data-ttu-id="0f2cf-199">.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-199">.</span></span> <span data-ttu-id="0f2cf-200">.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-200">.</span></span> 
> 
> 

<span data-ttu-id="0f2cf-201">Pour plus d’informations sur l’utilisation d’objets blob de stockage Microsoft Azure, consultez [API REST du service BLOB](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="0f2cf-201">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

### <a name="update-hello-assetfile"></a><span data-ttu-id="0f2cf-202">Mettre à jour hello AssetFile</span><span class="sxs-lookup"><span data-stu-id="0f2cf-202">Update hello AssetFile</span></span>
<span data-ttu-id="0f2cf-203">Maintenant que vous avez téléchargé votre fichier, mettre à jour des informations hello FileAsset taille (et autres).</span><span class="sxs-lookup"><span data-stu-id="0f2cf-203">Now that you've uploaded your file, update hello FileAsset size (and other) information.</span></span> <span data-ttu-id="0f2cf-204">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="0f2cf-204">For example:</span></span>

    MERGE https://media.windows.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5') HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {  
       "ContentFileSize":"1186540",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


<span data-ttu-id="0f2cf-205">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="0f2cf-205">**HTTP Response**</span></span>

<span data-ttu-id="0f2cf-206">Si la réussite, suivant de hello est retournée : HTTP/1.1 204 No Content</span><span class="sxs-lookup"><span data-stu-id="0f2cf-206">If successful, hello following is returned: HTTP/1.1 204 No Content</span></span>

### <a name="delete-hello-locator-and-accesspolicy"></a><span data-ttu-id="0f2cf-207">Supprimer hello recherche et la stratégie d’accès</span><span class="sxs-lookup"><span data-stu-id="0f2cf-207">Delete hello Locator and AccessPolicy</span></span>
<span data-ttu-id="0f2cf-208">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="0f2cf-208">**HTTP Request**</span></span>

    DELETE https://media.windows.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="0f2cf-209">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="0f2cf-209">**HTTP Response**</span></span>

<span data-ttu-id="0f2cf-210">En cas de réussite, suivant de hello est retournée :</span><span class="sxs-lookup"><span data-stu-id="0f2cf-210">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content 
    ...

<span data-ttu-id="0f2cf-211">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="0f2cf-211">**HTTP Request**</span></span>

    DELETE https://media.windows.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="0f2cf-212">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="0f2cf-212">**HTTP Response**</span></span>

<span data-ttu-id="0f2cf-213">En cas de réussite, suivant de hello est retournée :</span><span class="sxs-lookup"><span data-stu-id="0f2cf-213">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content 
    ...

## <span data-ttu-id="0f2cf-214"><a id="upload_in_bulk"></a>Téléchargement de ressources en bloc</span><span class="sxs-lookup"><span data-stu-id="0f2cf-214"><a id="upload_in_bulk"></a>Upload assets in bulk</span></span>
### <a name="create-hello-ingestmanifest"></a><span data-ttu-id="0f2cf-215">Créer hello IngestManifest</span><span class="sxs-lookup"><span data-stu-id="0f2cf-215">Create hello IngestManifest</span></span>
<span data-ttu-id="0f2cf-216">Hello IngestManifest est un conteneur pour un ensemble de ressources, des fichiers et des informations statistiques qui peuvent être utilisés progression de hello toodetermine de réception en bloc pour hello ensemble.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-216">hello IngestManifest is a container for a set of assets, asset files, and statistic information that can be used toodetermine hello progress of bulk ingesting for hello set.</span></span>

<span data-ttu-id="0f2cf-217">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="0f2cf-217">**HTTP Request**</span></span>

    POST https:// media.windows.net/API/IngestManifests HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 36
    Expect: 100-continue

    { "Name" : "ExampleManifestREST" }

### <a name="create-assets"></a><span data-ttu-id="0f2cf-218">Création de ressources</span><span class="sxs-lookup"><span data-stu-id="0f2cf-218">Create assets</span></span>
<span data-ttu-id="0f2cf-219">Avant de créer hello IngestManifestAsset, vous devez toocreate hello actif qui sera achevé à l’aide de la réception en bloc.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-219">Before creating hello IngestManifestAsset, you need toocreate hello Asset that will be completed using bulk ingesting.</span></span> <span data-ttu-id="0f2cf-220">Une ressource est un conteneur pour plusieurs types ou ensembles d’objets dans Media Services, y compris des fichiers vidéo, audio, des images, des collections de miniatures, des pistes textuelles et des légendes.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-220">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="0f2cf-221">Bonjour API REST, création d’un élément multimédia requiert envoyant un tooMicrosoft de demande HTTP POST Azure Media Services et en plaçant toutes les informations de propriété concernant votre élément multimédia dans le corps de la demande hello. Dans cet exemple, hello actif est créé à l’aide de l’option storageencrption (1) hello incluse avec le corps de la demande hello.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-221">In hello REST API, creating an Asset requires sending a HTTP POST request tooMicrosoft Azure Media Services and placing any property information about your asset in hello request body.In this example, hello Asset is created using hello StorageEncrption(1) option included with hello request body.</span></span>

<span data-ttu-id="0f2cf-222">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="0f2cf-222">**HTTP Response**</span></span>

    POST https://media.windows.net/API/Assets HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 55
    Expect: 100-continue

    { "Name" : "ExampleManifestREST_Asset", "Options" : 1 }

### <a name="create-hello-ingestmanifestassets"></a><span data-ttu-id="0f2cf-223">Créer hello IngestManifestAssets</span><span class="sxs-lookup"><span data-stu-id="0f2cf-223">Create hello IngestManifestAssets</span></span>
<span data-ttu-id="0f2cf-224">IngestManifestAssets représente les ressources dans un IngestManifest qui sont utilisées avec la réception en bloc.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-224">IngestManifestAssets represent Assets within an IngestManifest that are used with bulk ingesting.</span></span> <span data-ttu-id="0f2cf-225">manifeste de hello asset toohello Hello essentiellement de lier.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-225">hello basically link hello asset toohello manifest.</span></span> <span data-ttu-id="0f2cf-226">Azure Media Services surveille en interne pour le téléchargement du fichier hello selon les IngestManifestFiles collection associée toohello IngestManifestAsset.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-226">Azure Media Services watches internally for hello file upload based on IngestManifestFiles collection associated toohello IngestManifestAsset.</span></span> <span data-ttu-id="0f2cf-227">Une fois ces fichiers sont téléchargés, asset de hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-227">Once these files are uploaded, hello asset is completed.</span></span> <span data-ttu-id="0f2cf-228">Vous pouvez créer un IngestManifestAsset avec une demande HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-228">You can create a new IngestManifestAsset with a HTTP POST request.</span></span> <span data-ttu-id="0f2cf-229">Dans le corps de la demande hello, inclure hello Id d’IngestManifest et hello Id d’élément multimédia que hello IngestManifestAsset doit lier pour la réception en bloc.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-229">In hello request body, include hello IngestManifest Id and hello Asset Id that hello IngestManifestAsset should link together for bulk ingesting.</span></span>

<span data-ttu-id="0f2cf-230">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="0f2cf-230">**HTTP Response**</span></span>

    POST https://media.windows.net/API/IngestManifestAssets HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 152
    Expect: 100-continue
    { "ParentIngestManifestId" : "nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048", "Asset" : { "Id" : "nb:cid:UUID:b757929a-5a57-430b-b33e-c05c6cbef02e"}}


### <a name="create-hello-ingestmanifestfiles-for-each-asset"></a><span data-ttu-id="0f2cf-231">Créer hello IngestManifestFiles pour chaque élément multimédia</span><span class="sxs-lookup"><span data-stu-id="0f2cf-231">Create hello IngestManifestFiles for each Asset</span></span>
<span data-ttu-id="0f2cf-232">Un IngestManifestFile représente un objet blob réel vidéo ou audio qui sera téléchargé dans le cadre de la réception en bloc pour une ressource.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-232">An IngestManifestFile represents an actual video or audio blob object that will be uploaded as part of bulk ingesting for an asset.</span></span> <span data-ttu-id="0f2cf-233">Propriétés ne sont pas requises, sauf si l’élément multimédia de hello utilise une option de chiffrement liées au chiffrement.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-233">Encryption related properties are not required unless hello asset is using an encryption option.</span></span> <span data-ttu-id="0f2cf-234">exemple Hello utilisé dans cette section illustre la création d’un IngestManifestFile qui fait appel au StorageEncryption pour hello que élément multimédia créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-234">hello example used in this section demonstrates creating an IngestManifestFile that uses StorageEncryption for hello Asset previously created.</span></span>

<span data-ttu-id="0f2cf-235">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="0f2cf-235">**HTTP Response**</span></span>

    POST https://media.windows.net/API/IngestManifestFiles HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 367
    Expect: 100-continue

    { "Name" : "REST_Example_File.wmv", "ParentIngestManifestId" : "nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048", "ParentIngestManifestAssetId" : "nb:maid:UUID:beed8531-9a03-9043-b1d8-6a6d1044cdda", "IsEncrypted" : "true", "EncryptionScheme" : "StorageEncryption", "EncryptionVersion" : "1.0", "EncryptionKeyId" : "nb:kid:UUID:32e6efaf-5fba-4538-b115-9d1cefe43510" }

### <a name="upload-hello-files-tooblob-storage"></a><span data-ttu-id="0f2cf-236">Télécharger les fichiers de hello tooBlob stockage</span><span class="sxs-lookup"><span data-stu-id="0f2cf-236">Upload hello Files tooBlob Storage</span></span>
<span data-ttu-id="0f2cf-237">Vous pouvez utiliser n’importe quelle application de client haute vitesse capable de télécharger le conteneur de stockage blob pour les fichiers actifs hello toohello Uri fourni par hello propriété BlobStorageUriForUpload Hello IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-237">You can use any high speed client application capable of uploading hello asset files toohello blob storage container Uri provided by hello BlobStorageUriForUpload property of hello IngestManifest.</span></span> <span data-ttu-id="0f2cf-238">[Aspera On Demand pour l'Application Azure](http://go.microsoft.com/fwlink/?LinkId=272001)est un service de téléchargement à grande vitesse intéressant.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-238">One notable high speed upload service is [Aspera On Demand for Azure Application](http://go.microsoft.com/fwlink/?LinkId=272001).</span></span>

### <a name="monitor-bulk-ingest-progress"></a><span data-ttu-id="0f2cf-239">Surveillance de la progression de la réception en bloc</span><span class="sxs-lookup"><span data-stu-id="0f2cf-239">Monitor Bulk Ingest Progress</span></span>
<span data-ttu-id="0f2cf-240">Vous pouvez surveiller la progression de hello de réception des opérations pour un IngestManifest en interrogeant la propriété de statistiques hello Hello IngestManifest en bloc.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-240">You can monitor hello progress of bulk ingesting operations for an IngestManifest by polling hello Statistics property of hello IngestManifest.</span></span> <span data-ttu-id="0f2cf-241">Cette propriété est de type complexe [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics).</span><span class="sxs-lookup"><span data-stu-id="0f2cf-241">That property is a complex type, [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics).</span></span> <span data-ttu-id="0f2cf-242">toopoll hello propriété Statistics, soumettre une demande HTTP GET en passant hello ID d’IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-242">toopoll hello Statistics property, submit a HTTP GET request passing hello IngestManifest Id.</span></span>

## <a name="create-contentkeys-used-for-encryption"></a><span data-ttu-id="0f2cf-243">Créer des ContentKeys utilisées pour le chiffrement</span><span class="sxs-lookup"><span data-stu-id="0f2cf-243">Create ContentKeys used for encryption</span></span>
<span data-ttu-id="0f2cf-244">Si votre élément multimédia utilise le chiffrement, vous devez créer hello ContentKey toobe est utilisé pour le chiffrement avant de créer des fichiers d’éléments multimédias hello.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-244">If your asset will use encryption, you must create hello ContentKey toobe used for encryption before creating hello asset files.</span></span> <span data-ttu-id="0f2cf-245">Pour le chiffrement de stockage, hello propriétés suivantes doivent être incluses dans le corps de la demande hello.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-245">For storage encryption, hello following properties should be included in hello request body.</span></span>

| <span data-ttu-id="0f2cf-246">Propriété du corps de la demande</span><span class="sxs-lookup"><span data-stu-id="0f2cf-246">Request body property</span></span> | <span data-ttu-id="0f2cf-247">Description</span><span class="sxs-lookup"><span data-stu-id="0f2cf-247">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0f2cf-248">Id</span><span class="sxs-lookup"><span data-stu-id="0f2cf-248">Id</span></span> |<span data-ttu-id="0f2cf-249">Hello Id de ContentKey que nous générons nous-mêmes hello suivant à l’aide de mettre en forme, « Kid :<NEW GUID>».</span><span class="sxs-lookup"><span data-stu-id="0f2cf-249">hello ContentKey Id which we generate ourselves using hello following format, “nb:kid:UUID:<NEW GUID>”.</span></span> |
| <span data-ttu-id="0f2cf-250">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="0f2cf-250">ContentKeyType</span></span> |<span data-ttu-id="0f2cf-251">Type de clé de contenu hello il s’agit en tant qu’entier pour cette clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-251">This is hello content key type as an integer for this content key.</span></span> <span data-ttu-id="0f2cf-252">Nous transmettons la valeur hello 1 pour le chiffrement de stockage.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-252">We pass hello value 1 for storage encryption.</span></span> |
| <span data-ttu-id="0f2cf-253">EncryptedContentKey</span><span class="sxs-lookup"><span data-stu-id="0f2cf-253">EncryptedContentKey</span></span> |<span data-ttu-id="0f2cf-254">Nous créons une valeur de clé de contenu qui est une valeur de 256 bits (32 octets).</span><span class="sxs-lookup"><span data-stu-id="0f2cf-254">We create a new content key value which is a 256-bit (32 byte) value.</span></span> <span data-ttu-id="0f2cf-255">clé de Hello est chiffré à l’aide de hello stockage certificat X.509 de chiffrement que nous récupérons à partir de Microsoft Azure Media Services en exécutant une demande HTTP GET hello GetProtectionKeyId et GetProtectionKey méthodes.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-255">hello key is encrypted using hello storage encryption X.509 certificate which we retrieve from Microsoft Azure Media Services by executing a HTTP GET request for hello GetProtectionKeyId and GetProtectionKey Methods.</span></span> |
| <span data-ttu-id="0f2cf-256">ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="0f2cf-256">ProtectionKeyId</span></span> |<span data-ttu-id="0f2cf-257">Cela est hello id de clé de protection pour le certificat X.509 de chiffrement de stockage de hello a été utilisé tooencrypt notre clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-257">This is hello protection key id for hello storage encryption X.509 certificate that was used tooencrypt our content key.</span></span> |
| <span data-ttu-id="0f2cf-258">ProtectionKeyType</span><span class="sxs-lookup"><span data-stu-id="0f2cf-258">ProtectionKeyType</span></span> |<span data-ttu-id="0f2cf-259">Il s’agit de type de chiffrement de hello pour la clé de protection hello clé de contenu utilisés tooencrypt hello.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-259">This is hello encryption type for hello protection key that was used tooencrypt hello content key.</span></span> <span data-ttu-id="0f2cf-260">Cette valeur est StorageEncryption(1) dans notre exemple.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-260">This value is StorageEncryption(1) for our example.</span></span> |
| <span data-ttu-id="0f2cf-261">Somme de contrôle</span><span class="sxs-lookup"><span data-stu-id="0f2cf-261">Checksum</span></span> |<span data-ttu-id="0f2cf-262">somme de contrôle calculée Hello MD5 pour la clé de contenu hello.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-262">hello MD5 calculated checksum for hello content key.</span></span> <span data-ttu-id="0f2cf-263">Elle est calculée en chiffrant l’Id de contenu hello avec la clé de contenu hello.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-263">It is computed by encrypting hello content Id with hello content key.</span></span> <span data-ttu-id="0f2cf-264">Hello exemple de code montre comment toocalculate hello somme de contrôle.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-264">hello example code demonstrates how toocalculate hello checksum.</span></span> |

<span data-ttu-id="0f2cf-265">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="0f2cf-265">**HTTP Response**</span></span>

    POST https://media.windows.net/api/ContentKeys HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 572
    Expect: 100-continue

    {"Id" : "nb:kid:UUID:316d14d4-b603-4d90-b8db-0fede8aa48f8", "ContentKeyType" : 1, "EncryptedContentKey" : "Y4NPej7heOFa2vsd8ZEOcjjpu/qOq3RJ6GRfxa8CCwtAM83d6J2mKOeQFUmMyVXUSsBCCOdufmieTKi+hOUtNAbyNM4lY4AXI537b9GaY8oSeje0NGU8+QCOuf7jGdRac5B9uIk7WwD76RAJnqyep6U/OdvQV4RLvvZ9w7nO4bY8RHaUaLxC2u4aIRRaZtLu5rm8GKBPy87OzQVXNgnLM01I8s3Z4wJ3i7jXqkknDy4VkIyLBSQvIvUzxYHeNdMVWDmS+jPN9ScVmolUwGzH1A23td8UWFHOjTjXHLjNm5Yq+7MIOoaxeMlKPYXRFKofRY8Qh5o5tqvycSAJ9KUqfg==", "ProtectionKeyId" : "7D9BB04D9D0A4A24800CADBFEF232689E048F69C", "ProtectionKeyType" : 1, "Checksum" : "TfXtjCIlq1Y=" }

### <a name="link-hello-contentkey-toohello-asset"></a><span data-ttu-id="0f2cf-266">Lien hello ContentKey toohello actif</span><span class="sxs-lookup"><span data-stu-id="0f2cf-266">Link hello ContentKey toohello Asset</span></span>
<span data-ttu-id="0f2cf-267">Hello ContentKey est tooone associé ou les plus actifs en envoyant une demande HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-267">hello ContentKey is associated tooone or more assets by sending a HTTP POST request.</span></span> <span data-ttu-id="0f2cf-268">Hello demande suivante est un exemple toolink hello exemple ContentKey toohello exemple d’élément multimédia par Id.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-268">hello following request is an example toolink hello example ContentKey toohello example asset by Id.</span></span>

<span data-ttu-id="0f2cf-269">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="0f2cf-269">**HTTP Response**</span></span>

    POST https://media.windows.net/API/Assets('nb:cid:UUID:b3023475-09b4-4647-9d6d-6fc242822e68')/$links/ContentKeys HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 113
    Expect: 100-continue

    { "uri": "https://media.windows.net/api/ContentKeys('nb%3Akid%3AUUID%3A32e6efaf-5fba-4538-b115-9d1cefe43510')"}

<span data-ttu-id="0f2cf-270">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="0f2cf-270">**HTTP Response**</span></span>

    GET https://media.windows.net/API/IngestManifests('nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net

## <a name="next-steps"></a><span data-ttu-id="0f2cf-271">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0f2cf-271">Next steps</span></span>

<span data-ttu-id="0f2cf-272">Vous pouvez désormais encoder vos éléments multimédias téléchargés.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-272">You can now encode your uploaded assets.</span></span> <span data-ttu-id="0f2cf-273">Pour plus d'informations, consultez [Encode an asset using Media Encoder Standard with the Azure portal (Encoder un élément multimédia à l’aide de Media Encoder Standard avec le portail Azure)](media-services-portal-encode.md).</span><span class="sxs-lookup"><span data-stu-id="0f2cf-273">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="0f2cf-274">Vous pouvez également utiliser les fonctions Azure tootrigger un travail d’encodage basé sur un fichier qui arrivent dans le conteneur de hello configuré.</span><span class="sxs-lookup"><span data-stu-id="0f2cf-274">You can also use Azure Functions tootrigger an encoding job based on a file arriving in hello configured container.</span></span> <span data-ttu-id="0f2cf-275">Pour plus d’informations, consultez [cet exemple](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span><span class="sxs-lookup"><span data-stu-id="0f2cf-275">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="0f2cf-276">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="0f2cf-276">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="0f2cf-277">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="0f2cf-277">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[How tooGet a Media Processor]: media-services-get-media-processor.md

