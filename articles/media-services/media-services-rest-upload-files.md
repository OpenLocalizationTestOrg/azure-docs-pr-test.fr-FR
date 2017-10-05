---
title: "Charger des fichiers dans un compte Media Services à l’aide de REST | Microsoft Docs"
description: "Apprenez à obtenir du contenu multimédia dans Media Services en créant et en chargeant des ressources."
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
ms.openlocfilehash: 955356ffe6fc524c1528364add7e2c2a336137b7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="upload-files-into-a-media-services-account-using-rest"></a><span data-ttu-id="91fc9-103">Charger des fichiers dans un compte Media Services à l’aide de REST</span><span class="sxs-lookup"><span data-stu-id="91fc9-103">Upload files into a Media Services account using REST</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="91fc9-104">.NET</span><span class="sxs-lookup"><span data-stu-id="91fc9-104">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="91fc9-105">REST</span><span class="sxs-lookup"><span data-stu-id="91fc9-105">REST</span></span>](media-services-rest-upload-files.md)
> * [<span data-ttu-id="91fc9-106">Portail</span><span class="sxs-lookup"><span data-stu-id="91fc9-106">Portal</span></span>](media-services-portal-upload-files.md)
> 
> 

<span data-ttu-id="91fc9-107">Dans Media Services, vous téléchargez vos fichiers numériques dans une ressource.</span><span class="sxs-lookup"><span data-stu-id="91fc9-107">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="91fc9-108">L’entité [Asset](https://docs.microsoft.com/rest/api/media/operations/asset) peut contenir des fichiers vidéo et audio, des images, des collections de miniatures, des pistes textuelles et des légendes (et les métadonnées concernant ces fichiers).  Une fois les fichiers téléchargés dans la ressource, votre contenu est stocké en toute sécurité dans le cloud et peut faire l’objet d’un traitement et d’une diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="91fc9-108">The [Asset](https://docs.microsoft.com/rest/api/media/operations/asset) entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files.)  Once the files are uploaded into the asset, your content is stored securely in the cloud for further processing and streaming.</span></span> 

> [!NOTE]
> <span data-ttu-id="91fc9-109">Les considérations suivantes s'appliquent :</span><span class="sxs-lookup"><span data-stu-id="91fc9-109">The following considerations apply:</span></span>
> 
> * <span data-ttu-id="91fc9-110">Media Services utilise la valeur de la propriété IAssetFile.Name lors de la génération d’URL pour le contenu de streaming (par exemple, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters). Pour cette raison, l’encodage par pourcentage n’est pas autorisé.</span><span class="sxs-lookup"><span data-stu-id="91fc9-110">Media Services uses the value of the IAssetFile.Name property when building URLs for the streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="91fc9-111">La valeur de la propriété **Name** ne peut pas comporter les [caractères réservés à l’encodage en pourcentage suivants](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters) : !*'();:@&=+$,/?%#[]".</span><span class="sxs-lookup"><span data-stu-id="91fc9-111">The value of the **Name** property cannot have any of the following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="91fc9-112">En outre, il ne peut exister qu’un ’.’ pour l’extension de nom de fichier.</span><span class="sxs-lookup"><span data-stu-id="91fc9-112">Also, there can only be one '.' for the file name extension.</span></span>
> * <span data-ttu-id="91fc9-113">La longueur du nom ne doit pas dépasser 260 caractères.</span><span class="sxs-lookup"><span data-stu-id="91fc9-113">The length of the name should not be greater than 260 characters.</span></span>
> * <span data-ttu-id="91fc9-114">Une limite est appliquée à la taille maximale de fichier prise en charge pour le traitement dans Media Services.</span><span class="sxs-lookup"><span data-stu-id="91fc9-114">There is a limit to the maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="91fc9-115">Consultez [cette rubrique](media-services-quotas-and-limitations.md) pour en savoir plus sur les limites de taille des fichiers.</span><span class="sxs-lookup"><span data-stu-id="91fc9-115">Please see [this](media-services-quotas-and-limitations.md) topic for details about the file size limitation.</span></span>
> 

<span data-ttu-id="91fc9-116">Le flux de travail classique de téléchargement de ressources se divise en différentes parties, à savoir :</span><span class="sxs-lookup"><span data-stu-id="91fc9-116">The basic workflow for uploading Assets is divided into the following sections:</span></span>

* <span data-ttu-id="91fc9-117">Créer une ressource</span><span class="sxs-lookup"><span data-stu-id="91fc9-117">Create an Asset</span></span>
* <span data-ttu-id="91fc9-118">Chiffrer une ressource (facultatif)</span><span class="sxs-lookup"><span data-stu-id="91fc9-118">Encrypt an Asset (Optional)</span></span>
* <span data-ttu-id="91fc9-119">Télécharger un fichier vers le stockage d'objets blob</span><span class="sxs-lookup"><span data-stu-id="91fc9-119">Upload a file to blob storage</span></span>

<span data-ttu-id="91fc9-120">AMS vous permet également de télécharger des ressources en bloc.</span><span class="sxs-lookup"><span data-stu-id="91fc9-120">AMS also enables you to upload assets in bulk.</span></span> <span data-ttu-id="91fc9-121">Pour plus d’informations, consultez [cette](media-services-rest-upload-files.md#upload_in_bulk) section.</span><span class="sxs-lookup"><span data-stu-id="91fc9-121">For more information, see [this](media-services-rest-upload-files.md#upload_in_bulk) section.</span></span>

> [!NOTE]
> <span data-ttu-id="91fc9-122">Lors de l’accès aux entités dans Media Services, vous devez définir les valeurs et les champs d’en-tête spécifiques dans vos requêtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="91fc9-122">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="91fc9-123">Pour plus d'informations, consultez [Installation pour le développement REST API de Media Services](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="91fc9-123">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
> 

## <a name="connect-to-media-services"></a><span data-ttu-id="91fc9-124">Connexion à Media Services</span><span class="sxs-lookup"><span data-stu-id="91fc9-124">Connect to Media Services</span></span>

<span data-ttu-id="91fc9-125">Pour savoir comment vous connecter à l’API AMS, consultez [Accéder à l’API Azure Media Services avec l’authentification Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="91fc9-125">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="91fc9-126">Après vous être connecté à https://media.windows.net, vous recevrez une redirection 301 spécifiant un autre URI Media Services.</span><span class="sxs-lookup"><span data-stu-id="91fc9-126">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="91fc9-127">Vous devez faire d’autres appels au nouvel URI.</span><span class="sxs-lookup"><span data-stu-id="91fc9-127">You must make subsequent calls to the new URI.</span></span>

## <a name="upload-assets"></a><span data-ttu-id="91fc9-128">Téléchargement de ressources</span><span class="sxs-lookup"><span data-stu-id="91fc9-128">Upload assets</span></span>

### <a name="create-an-asset"></a><span data-ttu-id="91fc9-129">Créer une ressource</span><span class="sxs-lookup"><span data-stu-id="91fc9-129">Create an asset</span></span>

<span data-ttu-id="91fc9-130">Une ressource est un conteneur pour plusieurs types ou ensembles d’objets dans Media Services, y compris des fichiers vidéo, audio, des images, des collections de miniatures, des pistes textuelles et des légendes.</span><span class="sxs-lookup"><span data-stu-id="91fc9-130">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="91fc9-131">Dans l’API REST, la création d’une ressource nécessite d’envoyer une demande POST vers Media Services et de placer les informations de propriété concernant votre ressource dans le corps de la demande.</span><span class="sxs-lookup"><span data-stu-id="91fc9-131">In the REST API, creating an Asset requires sending POST request to Media Services and placing any property information about your asset in the request body.</span></span>

<span data-ttu-id="91fc9-132">L’une des propriétés que vous pouvez spécifier lors de la création d’un élément multimédia est **Options**.</span><span class="sxs-lookup"><span data-stu-id="91fc9-132">One of the properties that you can specify when creating an asset is **Options**.</span></span> <span data-ttu-id="91fc9-133">**Options** est une valeur d’énumération qui décrit les options de chiffrement permettant de créer un élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="91fc9-133">**Options** is an enumeration value that describes the encryption options that an Asset can be created with.</span></span> <span data-ttu-id="91fc9-134">Une valeur valide est une des valeurs de la liste ci-dessous, et non une combinaison de valeurs.</span><span class="sxs-lookup"><span data-stu-id="91fc9-134">A valid value is one of the values from the list below, not a combination of values.</span></span> 

* <span data-ttu-id="91fc9-135">**None** = **0** : Aucun chiffrement ne sera utilisé.</span><span class="sxs-lookup"><span data-stu-id="91fc9-135">**None** = **0**: No encryption will be used.</span></span> <span data-ttu-id="91fc9-136">Il s’agit de la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="91fc9-136">This is the default value.</span></span> <span data-ttu-id="91fc9-137">À noter que quand vous utilisez cette option, votre contenu n’est pas protégé pendant le transit ou le repos dans le stockage.</span><span class="sxs-lookup"><span data-stu-id="91fc9-137">Note that when using this option your content is not protected in transit or at rest in storage.</span></span>
    <span data-ttu-id="91fc9-138">Si vous prévoyez de fournir un MP4 sous forme de téléchargement progressif, utilisez cette option.</span><span class="sxs-lookup"><span data-stu-id="91fc9-138">If you plan to deliver an MP4 using progressive download, use this option.</span></span> 
* <span data-ttu-id="91fc9-139">**StorageEncrypted** = **1** : spécifie si vous souhaitez que vos fichiers soient chiffrés avec le chiffrement AES-256 bits pour le chargement et le stockage.</span><span class="sxs-lookup"><span data-stu-id="91fc9-139">**StorageEncrypted** = **1**: Specify if you want for your files to be encrypted with AES-256 bit encryption for upload and storage.</span></span>
  
    <span data-ttu-id="91fc9-140">Si votre ressource est stockée sous forme chiffrée, vous devez configurer une stratégie de remise de ressources.</span><span class="sxs-lookup"><span data-stu-id="91fc9-140">If your asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="91fc9-141">Pour plus d'informations, consultez [Configuration de la stratégie de remise de ressources](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="91fc9-141">For more information see [Configuring asset delivery policy](media-services-rest-configure-asset-delivery-policy.md).</span></span>
* <span data-ttu-id="91fc9-142">**CommonEncryptionProtected** = **2** : spécifie si vous téléchargez des fichiers protégés par une méthode de chiffrement commune (comme PlayReady).</span><span class="sxs-lookup"><span data-stu-id="91fc9-142">**CommonEncryptionProtected** = **2**: Specify if you are uploading files protected with a common encryption method (such as PlayReady).</span></span> 
* <span data-ttu-id="91fc9-143">**EnvelopeEncryptionProtected** = **4** : indique si vous téléchargez un contenu au format HLS chiffré avec des fichiers AES.</span><span class="sxs-lookup"><span data-stu-id="91fc9-143">**EnvelopeEncryptionProtected** = **4**: Specify if you are uploading HLS encrypted with AES files.</span></span> <span data-ttu-id="91fc9-144">Notez que les fichiers doivent avoir été encodés et chiffrés par le gestionnaire de transformation Transform Manager.</span><span class="sxs-lookup"><span data-stu-id="91fc9-144">Note that the files must have been encoded and encrypted by Transform Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="91fc9-145">Si votre élément multimédia utilise le chiffrement, vous devez créer une **ContentKey** et la lier à votre élément multimédia, comme le décrit la rubrique suivante :[Création d’une ContentKey](media-services-rest-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="91fc9-145">If your asset will use encryption, you must create a **ContentKey** and link it to your asset as described in the following topic:[How to create a ContentKey](media-services-rest-create-contentkey.md).</span></span> <span data-ttu-id="91fc9-146">Notez qu’après avoir téléchargé les fichiers dans l’élément multimédia, vous devez mettre à jour les propriétés de chiffrement sur l’entité **AssetFile** avec les valeurs obtenues pendant le chiffrement **Asset**.</span><span class="sxs-lookup"><span data-stu-id="91fc9-146">Note that after you upload the files into the asset, you need to update the encryption properties on the **AssetFile** entity with the values you got during the **Asset** encryption.</span></span> <span data-ttu-id="91fc9-147">Pour ce faire, utilisez la demande HTTP **MERGE** .</span><span class="sxs-lookup"><span data-stu-id="91fc9-147">Do it by using the **MERGE** HTTP request.</span></span> 
> 
> 

<span data-ttu-id="91fc9-148">L’exemple suivant montre comment créer une ressource.</span><span class="sxs-lookup"><span data-stu-id="91fc9-148">The following example shows how to create an asset.</span></span>

<span data-ttu-id="91fc9-149">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="91fc9-149">**HTTP Request**</span></span>

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

<span data-ttu-id="91fc9-150">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="91fc9-150">**HTTP Response**</span></span>

<span data-ttu-id="91fc9-151">Si l’opération réussit, l’élément suivant est retourné :</span><span class="sxs-lookup"><span data-stu-id="91fc9-151">If successful, the following is returned:</span></span>

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

### <a name="create-an-assetfile"></a><span data-ttu-id="91fc9-152">Création d’un AssetFile</span><span class="sxs-lookup"><span data-stu-id="91fc9-152">Create an AssetFile</span></span>
<span data-ttu-id="91fc9-153">L’entité [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) représente un fichier audio ou vidéo stocké dans un conteneur d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="91fc9-153">The [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="91fc9-154">Un fichier de ressources est toujours associé à une ressource et une ressource peut contenir un ou plusieurs fichiers de ressources.</span><span class="sxs-lookup"><span data-stu-id="91fc9-154">An asset file is always associated with an asset, and an asset may contain one or many asset files.</span></span> <span data-ttu-id="91fc9-155">La tâche de Media Services Encoder échoue si un objet de fichier de ressources n’est pas associé à un fichier numérique dans un conteneur d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="91fc9-155">The Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="91fc9-156">Notez que l’instance **AssetFile** et le fichier multimédia réel sont deux objets distincts.</span><span class="sxs-lookup"><span data-stu-id="91fc9-156">Note that the **AssetFile** instance and the actual media file are two distinct objects.</span></span> <span data-ttu-id="91fc9-157">L’instance AssetFile contient des métadonnées concernant le fichier multimédia, tandis que le fichier multimédia contient le contenu multimédia réel.</span><span class="sxs-lookup"><span data-stu-id="91fc9-157">The AssetFile instance contains metadata about the media file, while the media file contains the actual media content.</span></span>

<span data-ttu-id="91fc9-158">Après avoir chargé votre fichier multimédia numérique dans un conteneur d’objets blob, vous utiliserez la demande HTTP **MERGE** pour mettre à jour AssetFile avec des informations sur votre fichier multimédia (comme l’indique plus loin cette rubrique).</span><span class="sxs-lookup"><span data-stu-id="91fc9-158">After you upload your digital media file into a blob container, you will use the **MERGE** HTTP request to update the AssetFile with information about your media file (as shown later in the topic).</span></span> 

<span data-ttu-id="91fc9-159">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="91fc9-159">**HTTP Request**</span></span>

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

<span data-ttu-id="91fc9-160">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="91fc9-160">**HTTP Response**</span></span>

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

### <a name="creating-the-accesspolicy-with-write-permission"></a><span data-ttu-id="91fc9-161">Création d’AccessPolicy avec autorisation d’écriture.</span><span class="sxs-lookup"><span data-stu-id="91fc9-161">Creating the AccessPolicy with write permission.</span></span>

>[!NOTE]
><span data-ttu-id="91fc9-162">Un nombre limite de 1 000 000 a été défini pour les différentes stratégies AMS (par exemple, pour la stratégie de localisateur ou pour ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="91fc9-162">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="91fc9-163">Vous devez utiliser le même ID de stratégie si vous utilisez toujours les mêmes jours / autorisations d’accès, par exemple, les stratégies pour les localisateurs destinées à demeurer en place pendant une longue période (stratégies sans chargement).</span><span class="sxs-lookup"><span data-stu-id="91fc9-163">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="91fc9-164">Pour plus d’informations, consultez [cette rubrique](media-services-dotnet-manage-entities.md#limit-access-policies) .</span><span class="sxs-lookup"><span data-stu-id="91fc9-164">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="91fc9-165">Avant de télécharger des fichiers dans le stockage blob, définissez les droits de la stratégie d’accès pour l’écriture sur une ressource.</span><span class="sxs-lookup"><span data-stu-id="91fc9-165">Before uploading any files into blob storage, set the access policy rights for writing to an asset.</span></span> <span data-ttu-id="91fc9-166">Pour ce faire, utilisez POST avec une demande HTTP sur le jeu d’entités AccessPolicies.</span><span class="sxs-lookup"><span data-stu-id="91fc9-166">To do that, POST an HTTP request to the AccessPolicies entity set.</span></span> <span data-ttu-id="91fc9-167">N’oubliez pas de définir une valeur DurationInMinutes après la création ou vous recevrez en réponse un message d’erreur interne de serveur 500.</span><span class="sxs-lookup"><span data-stu-id="91fc9-167">Define a DurationInMinutes value upon creation or you will receive a 500 Internal Server error message back in response.</span></span> <span data-ttu-id="91fc9-168">Pour plus d’informations sur AccessPolicies, consultez [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span><span class="sxs-lookup"><span data-stu-id="91fc9-168">For more information on AccessPolicies, see [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span></span>

<span data-ttu-id="91fc9-169">L’exemple suivant montre comment créer une stratégie AccessPolicy :</span><span class="sxs-lookup"><span data-stu-id="91fc9-169">The following example shows how to create an AccessPolicy:</span></span>

<span data-ttu-id="91fc9-170">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="91fc9-170">**HTTP Request**</span></span>

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

<span data-ttu-id="91fc9-171">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="91fc9-171">**HTTP Request**</span></span>

    If successful, the following response is returned:

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

### <a name="get-the-upload-url"></a><span data-ttu-id="91fc9-172">Obtention de l’URL de téléchargement</span><span class="sxs-lookup"><span data-stu-id="91fc9-172">Get the Upload URL</span></span>
<span data-ttu-id="91fc9-173">Pour recevoir l’URL de téléchargement réelle, créez un localisateur SAS.</span><span class="sxs-lookup"><span data-stu-id="91fc9-173">To receive the actual upload URL, create a SAS Locator.</span></span> <span data-ttu-id="91fc9-174">Les localisateurs définissent l’heure de début et le type de point de terminaison de connexion pour les clients qui souhaitent accéder aux fichiers d’une ressource.</span><span class="sxs-lookup"><span data-stu-id="91fc9-174">Locators define the start time and type of connection endpoint for clients that want to access Files in an Asset.</span></span> <span data-ttu-id="91fc9-175">Vous pouvez créer plusieurs entités de localisateurs pour une paire AccessPolicy et Asset donnée, afin de gérer les différentes demandes et besoins des clients.</span><span class="sxs-lookup"><span data-stu-id="91fc9-175">You can create multiple Locator entities for a given AccessPolicy and Asset pair to handle different client requests and needs.</span></span> <span data-ttu-id="91fc9-176">Chacun de ces localisateurs utilise la valeur StartTime et la valeur DurationInMinutes d’AccessPolicy pour déterminer la durée pendant laquelle une URL peut être utilisée.</span><span class="sxs-lookup"><span data-stu-id="91fc9-176">Each of these Locators use the StartTime value plus the DurationInMinutes value of the AccessPolicy to determine the length of time a URL can be used.</span></span> <span data-ttu-id="91fc9-177">Pour plus d’informations, consultez la rubrique [Localisateur](https://docs.microsoft.com/rest/api/media/operations/locator).</span><span class="sxs-lookup"><span data-stu-id="91fc9-177">For more information, see [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>

<span data-ttu-id="91fc9-178">Une URL SAS a le format suivant :</span><span class="sxs-lookup"><span data-stu-id="91fc9-178">A SAS URL has the following format:</span></span>

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

<span data-ttu-id="91fc9-179">Certaines considérations s’appliquent :</span><span class="sxs-lookup"><span data-stu-id="91fc9-179">Some considerations apply:</span></span>

* <span data-ttu-id="91fc9-180">Vous ne pouvez avoir plus de cinq localisateurs uniques associés à une ressource donnée.</span><span class="sxs-lookup"><span data-stu-id="91fc9-180">You cannot have more than five unique Locators associated with a given Asset at one time.</span></span> <span data-ttu-id="91fc9-181">Pour plus d’informations, consultez la rubrique Localisateur.</span><span class="sxs-lookup"><span data-stu-id="91fc9-181">For more information, see Locator.</span></span>
* <span data-ttu-id="91fc9-182">Si vous avez besoin de télécharger vos fichiers immédiatement, vous devez définir la valeur StartTime sur cinq minutes avant l’heure actuelle.</span><span class="sxs-lookup"><span data-stu-id="91fc9-182">If you need to upload your files immediately, you should set your StartTime value to five minutes before the current time.</span></span> <span data-ttu-id="91fc9-183">Cela vient du fait qu’il peut exister un décalage horaire entre votre ordinateur client et Media Services.</span><span class="sxs-lookup"><span data-stu-id="91fc9-183">This is because there may be clock skew between your client machine and Media Services.</span></span> <span data-ttu-id="91fc9-184">De même, la valeur de StartTime doit être au format DateTime suivant : AAAA-MM-JJTHH:mm:ssZ (par exemple, « 2014-05-23T17:53:50Z »).</span><span class="sxs-lookup"><span data-stu-id="91fc9-184">Also, your StartTime value must be in the following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>    
* <span data-ttu-id="91fc9-185">Il peut y avoir un délai de 30 à 40 secondes après la création d’un localisateur avant qu’il soit disponible.</span><span class="sxs-lookup"><span data-stu-id="91fc9-185">There may be a 30-40 second delay after a Locator is created to when it is available for use.</span></span> <span data-ttu-id="91fc9-186">Ce problème s’applique aux localisateurs d’URL SAS et d’origine.</span><span class="sxs-lookup"><span data-stu-id="91fc9-186">This issue applies to both SAS URL and Origin Locators.</span></span>

<span data-ttu-id="91fc9-187">L’exemple suivant montre comment créer un localisateur d’URL SAS, tel que défini par la propriété Type dans le corps de la demande (« 1 » pour un localisateur SAS et « 2 » pour un localisateur d’origine à la demande).</span><span class="sxs-lookup"><span data-stu-id="91fc9-187">The following example shows how to create a SAS URL Locator, as defined by the Type property in the request body ("1" for a SAS locator and "2" for an On-Demand origin locator).</span></span> <span data-ttu-id="91fc9-188">La propriété **Path** retournée contient l’URL que vous devez utiliser pour télécharger votre fichier.</span><span class="sxs-lookup"><span data-stu-id="91fc9-188">The **Path** property returned contains the URL that you must use to upload your file.</span></span>

<span data-ttu-id="91fc9-189">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="91fc9-189">**HTTP Request**</span></span>

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

<span data-ttu-id="91fc9-190">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="91fc9-190">**HTTP Response**</span></span>

<span data-ttu-id="91fc9-191">Si l’opération réussit, la réponse suivante est retournée :</span><span class="sxs-lookup"><span data-stu-id="91fc9-191">If successful, the following response is returned:</span></span>

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

### <a name="upload-a-file-into-a-blob-storage-container"></a><span data-ttu-id="91fc9-192">Téléchargement d’un fichier dans un conteneur de stockage d’objets blob</span><span class="sxs-lookup"><span data-stu-id="91fc9-192">Upload a file into a blob storage container</span></span>
<span data-ttu-id="91fc9-193">Après avoir défini AccessPolicy et Locator, le fichier réel est téléchargé vers un conteneur de stockage d’objets blob Microsoft Azure à l’aide des API REST Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="91fc9-193">Once you have the AccessPolicy and Locator set, the actual file is uploaded to an Azure Blob Storage container using the Azure Storage REST APIs.</span></span> <span data-ttu-id="91fc9-194">Vous devez télécharger les fichiers en tant qu’objets blob de blocs.</span><span class="sxs-lookup"><span data-stu-id="91fc9-194">You must upload the files as block blobs.</span></span> <span data-ttu-id="91fc9-195">Les objets blob de pages ne sont pas pris en charge par Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="91fc9-195">Page blobs are not supported by Azure Media Services.</span></span>  

> [!NOTE]
> <span data-ttu-id="91fc9-196">Vous devez ajouter le nom du fichier à télécharger dans la valeur **Path** du localisateur reçue dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="91fc9-196">You must add the file name for the file you want to upload to the Locator **Path** value received in the previous section.</span></span> <span data-ttu-id="91fc9-197">Par exemple, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="91fc9-197">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="91fc9-198">.</span><span class="sxs-lookup"><span data-stu-id="91fc9-198">.</span></span> <span data-ttu-id="91fc9-199">.</span><span class="sxs-lookup"><span data-stu-id="91fc9-199">.</span></span> <span data-ttu-id="91fc9-200">.</span><span class="sxs-lookup"><span data-stu-id="91fc9-200">.</span></span> 
> 
> 

<span data-ttu-id="91fc9-201">Pour plus d’informations sur l’utilisation d’objets blob de stockage Microsoft Azure, consultez [API REST du service BLOB](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="91fc9-201">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

### <a name="update-the-assetfile"></a><span data-ttu-id="91fc9-202">Mise à jour d’AssetFile</span><span class="sxs-lookup"><span data-stu-id="91fc9-202">Update the AssetFile</span></span>
<span data-ttu-id="91fc9-203">Maintenant que vous avez téléchargé votre fichier, mettez à jour les informations de taille FileAsset (et autres).</span><span class="sxs-lookup"><span data-stu-id="91fc9-203">Now that you've uploaded your file, update the FileAsset size (and other) information.</span></span> <span data-ttu-id="91fc9-204">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="91fc9-204">For example:</span></span>

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


<span data-ttu-id="91fc9-205">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="91fc9-205">**HTTP Response**</span></span>

<span data-ttu-id="91fc9-206">Si l’opération réussit, l’élément suivant est retourné : HTTP/1.1 204 No Content</span><span class="sxs-lookup"><span data-stu-id="91fc9-206">If successful, the following is returned: HTTP/1.1 204 No Content</span></span>

### <a name="delete-the-locator-and-accesspolicy"></a><span data-ttu-id="91fc9-207">Suppression du localisateur et d’AcessPolicy</span><span class="sxs-lookup"><span data-stu-id="91fc9-207">Delete the Locator and AccessPolicy</span></span>
<span data-ttu-id="91fc9-208">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="91fc9-208">**HTTP Request**</span></span>

    DELETE https://media.windows.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="91fc9-209">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="91fc9-209">**HTTP Response**</span></span>

<span data-ttu-id="91fc9-210">Si l’opération réussit, l’élément suivant est retourné :</span><span class="sxs-lookup"><span data-stu-id="91fc9-210">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content 
    ...

<span data-ttu-id="91fc9-211">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="91fc9-211">**HTTP Request**</span></span>

    DELETE https://media.windows.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="91fc9-212">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="91fc9-212">**HTTP Response**</span></span>

<span data-ttu-id="91fc9-213">Si l’opération réussit, l’élément suivant est retourné :</span><span class="sxs-lookup"><span data-stu-id="91fc9-213">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content 
    ...

## <span data-ttu-id="91fc9-214"><a id="upload_in_bulk"></a>Téléchargement de ressources en bloc</span><span class="sxs-lookup"><span data-stu-id="91fc9-214"><a id="upload_in_bulk"></a>Upload assets in bulk</span></span>
### <a name="create-the-ingestmanifest"></a><span data-ttu-id="91fc9-215">Création d’IngestManifest</span><span class="sxs-lookup"><span data-stu-id="91fc9-215">Create the IngestManifest</span></span>
<span data-ttu-id="91fc9-216">IngestManifest est un conteneur pour un ensemble de ressources, de fichiers de ressources et d’informations statistiques qui peuvent être utilisées pour déterminer la progression de la réception en bloc pour l’ensemble.</span><span class="sxs-lookup"><span data-stu-id="91fc9-216">The IngestManifest is a container for a set of assets, asset files, and statistic information that can be used to determine the progress of bulk ingesting for the set.</span></span>

<span data-ttu-id="91fc9-217">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="91fc9-217">**HTTP Request**</span></span>

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

### <a name="create-assets"></a><span data-ttu-id="91fc9-218">Création de ressources</span><span class="sxs-lookup"><span data-stu-id="91fc9-218">Create assets</span></span>
<span data-ttu-id="91fc9-219">Avant de créer IngestManifestAsset, vous devez créer la ressource qui sera finalisée avec la réception en bloc.</span><span class="sxs-lookup"><span data-stu-id="91fc9-219">Before creating the IngestManifestAsset, you need to create the Asset that will be completed using bulk ingesting.</span></span> <span data-ttu-id="91fc9-220">Une ressource est un conteneur pour plusieurs types ou ensembles d’objets dans Media Services, y compris des fichiers vidéo, audio, des images, des collections de miniatures, des pistes textuelles et des légendes.</span><span class="sxs-lookup"><span data-stu-id="91fc9-220">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="91fc9-221">Dans l’API REST, la création d’une ressource nécessite d’envoyer une demande HTTP POST vers Microsoft Azure Media Services et de placer les informations de propriété concernant votre ressource dans le corps de la demande. Dans cet exemple, la ressource est créée à l’aide de l’option StorageEncryption(1) incluse dans le corps de la demande.</span><span class="sxs-lookup"><span data-stu-id="91fc9-221">In the REST API, creating an Asset requires sending a HTTP POST request to Microsoft Azure Media Services and placing any property information about your asset in the request body.In this example, the Asset is created using the StorageEncrption(1) option included with the request body.</span></span>

<span data-ttu-id="91fc9-222">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="91fc9-222">**HTTP Response**</span></span>

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

### <a name="create-the-ingestmanifestassets"></a><span data-ttu-id="91fc9-223">Création d’IngestManifestAssets</span><span class="sxs-lookup"><span data-stu-id="91fc9-223">Create the IngestManifestAssets</span></span>
<span data-ttu-id="91fc9-224">IngestManifestAssets représente les ressources dans un IngestManifest qui sont utilisées avec la réception en bloc.</span><span class="sxs-lookup"><span data-stu-id="91fc9-224">IngestManifestAssets represent Assets within an IngestManifest that are used with bulk ingesting.</span></span> <span data-ttu-id="91fc9-225">Elles permettent essentiellement de lier la ressource au manifeste.</span><span class="sxs-lookup"><span data-stu-id="91fc9-225">The basically link the asset to the manifest.</span></span> <span data-ttu-id="91fc9-226">Azure Media Services surveille en interne le téléchargement du fichier en fonction de la collection IngestManifestFiles associée à IngestManifestAsset.</span><span class="sxs-lookup"><span data-stu-id="91fc9-226">Azure Media Services watches internally for the file upload based on IngestManifestFiles collection associated to the IngestManifestAsset.</span></span> <span data-ttu-id="91fc9-227">Une fois que ces fichiers sont chargés, la ressource est finalisée.</span><span class="sxs-lookup"><span data-stu-id="91fc9-227">Once these files are uploaded, the asset is completed.</span></span> <span data-ttu-id="91fc9-228">Vous pouvez créer un IngestManifestAsset avec une demande HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="91fc9-228">You can create a new IngestManifestAsset with a HTTP POST request.</span></span> <span data-ttu-id="91fc9-229">Dans le corps de la demande, indiquez l’ID d’IngestManifest et l’ID de la ressource qu’IngestManifestAsset doit lier ensemble pour la réception en bloc.</span><span class="sxs-lookup"><span data-stu-id="91fc9-229">In the request body, include the IngestManifest Id and the Asset Id that the IngestManifestAsset should link together for bulk ingesting.</span></span>

<span data-ttu-id="91fc9-230">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="91fc9-230">**HTTP Response**</span></span>

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


### <a name="create-the-ingestmanifestfiles-for-each-asset"></a><span data-ttu-id="91fc9-231">Création d’IngestManifestFiles pour chaque ressource</span><span class="sxs-lookup"><span data-stu-id="91fc9-231">Create the IngestManifestFiles for each Asset</span></span>
<span data-ttu-id="91fc9-232">Un IngestManifestFile représente un objet blob réel vidéo ou audio qui sera téléchargé dans le cadre de la réception en bloc pour une ressource.</span><span class="sxs-lookup"><span data-stu-id="91fc9-232">An IngestManifestFile represents an actual video or audio blob object that will be uploaded as part of bulk ingesting for an asset.</span></span> <span data-ttu-id="91fc9-233">Des propriétés liées au chiffrement ne sont pas requises, sauf si la ressource utilise une option de chiffrement.</span><span class="sxs-lookup"><span data-stu-id="91fc9-233">Encryption related properties are not required unless the asset is using an encryption option.</span></span> <span data-ttu-id="91fc9-234">L’exemple utilisé dans cette section illustre la création d’un IngestManifestFile qui fait appel à StorageEncryption pour la ressource créée précédemment.</span><span class="sxs-lookup"><span data-stu-id="91fc9-234">The example used in this section demonstrates creating an IngestManifestFile that uses StorageEncryption for the Asset previously created.</span></span>

<span data-ttu-id="91fc9-235">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="91fc9-235">**HTTP Response**</span></span>

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

### <a name="upload-the-files-to-blob-storage"></a><span data-ttu-id="91fc9-236">Téléchargement des fichiers vers le stockage d’objets blob</span><span class="sxs-lookup"><span data-stu-id="91fc9-236">Upload the Files to Blob Storage</span></span>
<span data-ttu-id="91fc9-237">Vous pouvez utiliser n’importe quelle application cliente rapide capable de télécharger les fichiers de ressources sur l’URI du conteneur de stockage d’objets blob fourni par la propriété BlobStorageUriForUpload d’IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="91fc9-237">You can use any high speed client application capable of uploading the asset files to the blob storage container Uri provided by the BlobStorageUriForUpload property of the IngestManifest.</span></span> <span data-ttu-id="91fc9-238">[Aspera On Demand pour l'Application Azure](http://go.microsoft.com/fwlink/?LinkId=272001)est un service de téléchargement à grande vitesse intéressant.</span><span class="sxs-lookup"><span data-stu-id="91fc9-238">One notable high speed upload service is [Aspera On Demand for Azure Application](http://go.microsoft.com/fwlink/?LinkId=272001).</span></span>

### <a name="monitor-bulk-ingest-progress"></a><span data-ttu-id="91fc9-239">Surveillance de la progression de la réception en bloc</span><span class="sxs-lookup"><span data-stu-id="91fc9-239">Monitor Bulk Ingest Progress</span></span>
<span data-ttu-id="91fc9-240">Vous pouvez surveiller la progression des opérations de réception en bloc pour un IngestManifest en interrogeant la propriété Statistics d’IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="91fc9-240">You can monitor the progress of bulk ingesting operations for an IngestManifest by polling the Statistics property of the IngestManifest.</span></span> <span data-ttu-id="91fc9-241">Cette propriété est de type complexe [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics).</span><span class="sxs-lookup"><span data-stu-id="91fc9-241">That property is a complex type, [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics).</span></span> <span data-ttu-id="91fc9-242">Pour interroger la propriété Statistics, envoyez une demande HTTP GET en transmettant l’ID d’IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="91fc9-242">To poll the Statistics property, submit a HTTP GET request passing the IngestManifest Id.</span></span>

## <a name="create-contentkeys-used-for-encryption"></a><span data-ttu-id="91fc9-243">Créer des ContentKeys utilisées pour le chiffrement</span><span class="sxs-lookup"><span data-stu-id="91fc9-243">Create ContentKeys used for encryption</span></span>
<span data-ttu-id="91fc9-244">Si votre ressource utilise le chiffrement, vous devez créer la ContentKey à utiliser pour le chiffrement avant de créer les fichiers de ressources.</span><span class="sxs-lookup"><span data-stu-id="91fc9-244">If your asset will use encryption, you must create the ContentKey to be used for encryption before creating the asset files.</span></span> <span data-ttu-id="91fc9-245">Pour le chiffrement du stockage, les propriétés suivantes doivent être incluses dans le corps de la demande.</span><span class="sxs-lookup"><span data-stu-id="91fc9-245">For storage encryption, the following properties should be included in the request body.</span></span>

| <span data-ttu-id="91fc9-246">Propriété du corps de la demande</span><span class="sxs-lookup"><span data-stu-id="91fc9-246">Request body property</span></span> | <span data-ttu-id="91fc9-247">Description</span><span class="sxs-lookup"><span data-stu-id="91fc9-247">Description</span></span> |
| --- | --- |
| <span data-ttu-id="91fc9-248">Id</span><span class="sxs-lookup"><span data-stu-id="91fc9-248">Id</span></span> |<span data-ttu-id="91fc9-249">ID de ContentKey que nous générons nous-mêmes en utilisant le format suivant : « nb:kid:UUID:<NEW GUID> ».</span><span class="sxs-lookup"><span data-stu-id="91fc9-249">The ContentKey Id which we generate ourselves using the following format, “nb:kid:UUID:<NEW GUID>”.</span></span> |
| <span data-ttu-id="91fc9-250">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="91fc9-250">ContentKeyType</span></span> |<span data-ttu-id="91fc9-251">Il s’agit du type de clé de contenu en tant qu’entier pour cette clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="91fc9-251">This is the content key type as an integer for this content key.</span></span> <span data-ttu-id="91fc9-252">Nous transmettons la valeur 1 pour le chiffrement du stockage.</span><span class="sxs-lookup"><span data-stu-id="91fc9-252">We pass the value 1 for storage encryption.</span></span> |
| <span data-ttu-id="91fc9-253">EncryptedContentKey</span><span class="sxs-lookup"><span data-stu-id="91fc9-253">EncryptedContentKey</span></span> |<span data-ttu-id="91fc9-254">Nous créons une valeur de clé de contenu qui est une valeur de 256 bits (32 octets).</span><span class="sxs-lookup"><span data-stu-id="91fc9-254">We create a new content key value which is a 256-bit (32 byte) value.</span></span> <span data-ttu-id="91fc9-255">La clé est chiffrée à l’aide du certificat X.509 de chiffrement du stockage que nous récupérons à partir de Microsoft Azure Media Services en exécutant une demande HTTP GET pour les méthodes GetProtectionKeyId et GetProtectionKey.</span><span class="sxs-lookup"><span data-stu-id="91fc9-255">The key is encrypted using the storage encryption X.509 certificate which we retrieve from Microsoft Azure Media Services by executing a HTTP GET request for the GetProtectionKeyId and GetProtectionKey Methods.</span></span> |
| <span data-ttu-id="91fc9-256">ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="91fc9-256">ProtectionKeyId</span></span> |<span data-ttu-id="91fc9-257">Il s’agit de l’ID de clé de protection pour le certificat X.509 de chiffrement de stockage qui a été utilisé pour chiffrer notre clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="91fc9-257">This is the protection key id for the storage encryption X.509 certificate that was used to encrypt our content key.</span></span> |
| <span data-ttu-id="91fc9-258">ProtectionKeyType</span><span class="sxs-lookup"><span data-stu-id="91fc9-258">ProtectionKeyType</span></span> |<span data-ttu-id="91fc9-259">Il s’agit du type de chiffrement de la clé de protection qui a été utilisé pour chiffrer la clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="91fc9-259">This is the encryption type for the protection key that was used to encrypt the content key.</span></span> <span data-ttu-id="91fc9-260">Cette valeur est StorageEncryption(1) dans notre exemple.</span><span class="sxs-lookup"><span data-stu-id="91fc9-260">This value is StorageEncryption(1) for our example.</span></span> |
| <span data-ttu-id="91fc9-261">Somme de contrôle</span><span class="sxs-lookup"><span data-stu-id="91fc9-261">Checksum</span></span> |<span data-ttu-id="91fc9-262">La somme de contrôle calculée MD5 pour la clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="91fc9-262">The MD5 calculated checksum for the content key.</span></span> <span data-ttu-id="91fc9-263">Elle est calculée en chiffrant l’ID de contenu avec la clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="91fc9-263">It is computed by encrypting the content Id with the content key.</span></span> <span data-ttu-id="91fc9-264">L’exemple de code montre comment calculer la somme de contrôle.</span><span class="sxs-lookup"><span data-stu-id="91fc9-264">The example code demonstrates how to calculate the checksum.</span></span> |

<span data-ttu-id="91fc9-265">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="91fc9-265">**HTTP Response**</span></span>

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

### <a name="link-the-contentkey-to-the-asset"></a><span data-ttu-id="91fc9-266">Liaison de ContentKey à la ressource</span><span class="sxs-lookup"><span data-stu-id="91fc9-266">Link the ContentKey to the Asset</span></span>
<span data-ttu-id="91fc9-267">La ContentKey est associée à une ou plusieurs ressources en envoyant une demande HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="91fc9-267">The ContentKey is associated to one or more assets by sending a HTTP POST request.</span></span> <span data-ttu-id="91fc9-268">La demande suivante illustre la liaison de la ContentKey en exemple à la ressource en exemple par ID.</span><span class="sxs-lookup"><span data-stu-id="91fc9-268">The following request is an example to link the example ContentKey to the example asset by Id.</span></span>

<span data-ttu-id="91fc9-269">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="91fc9-269">**HTTP Response**</span></span>

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

<span data-ttu-id="91fc9-270">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="91fc9-270">**HTTP Response**</span></span>

    GET https://media.windows.net/API/IngestManifests('nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net

## <a name="next-steps"></a><span data-ttu-id="91fc9-271">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="91fc9-271">Next steps</span></span>

<span data-ttu-id="91fc9-272">Vous pouvez désormais encoder vos éléments multimédias téléchargés.</span><span class="sxs-lookup"><span data-stu-id="91fc9-272">You can now encode your uploaded assets.</span></span> <span data-ttu-id="91fc9-273">Pour plus d'informations, consultez [Encode an asset using Media Encoder Standard with the Azure portal (Encoder un élément multimédia à l’aide de Media Encoder Standard avec le portail Azure)](media-services-portal-encode.md).</span><span class="sxs-lookup"><span data-stu-id="91fc9-273">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="91fc9-274">Vous pouvez également utiliser les fonctions Azure pour déclencher une tâche de codage à partir d’un fichier entrant dans le conteneur configuré.</span><span class="sxs-lookup"><span data-stu-id="91fc9-274">You can also use Azure Functions to trigger an encoding job based on a file arriving in the configured container.</span></span> <span data-ttu-id="91fc9-275">Pour plus d’informations, consultez [cet exemple](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span><span class="sxs-lookup"><span data-stu-id="91fc9-275">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="91fc9-276">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="91fc9-276">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="91fc9-277">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="91fc9-277">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[How to Get a Media Processor]: media-services-get-media-processor.md

