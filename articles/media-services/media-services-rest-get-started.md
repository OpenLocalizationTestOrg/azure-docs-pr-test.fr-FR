---
title: "Prendre en main la diffusion de contenus à la demande avec REST | Microsoft Docs"
description: "Ce didacticiel vous présente les étapes d’implémentation d’une application de diffusion de contenu à la demande avec Azure Media Services au moyen de l’API REST."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 88194b59-e479-43ac-b179-af4f295e3780
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: f304f7671465862123f64c8b0f9af95a7c828cc2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-rest"></a><span data-ttu-id="6afe9-103">Prendre en main la diffusion de contenus à la demande avec REST</span><span class="sxs-lookup"><span data-stu-id="6afe9-103">Get started with delivering content on demand using REST</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="6afe9-104">Ce document de démarrage rapide vous guide à travers les étapes d’implémentation d’une application de diffusion de contenu vidéo à la demande (VoD) avec les API REST Azure Media Services (AMS).</span><span class="sxs-lookup"><span data-stu-id="6afe9-104">This quickstart walks you through the steps of implementing a Video-on-Demand (VoD) content delivery application using Azure Media Services (AMS) REST APIs.</span></span>

<span data-ttu-id="6afe9-105">Il présente le workflow Media Services de base et les objets et tâches de programmation les plus courants requis pour le développement Media Services.</span><span class="sxs-lookup"><span data-stu-id="6afe9-105">The tutorial introduces the basic Media Services workflow and the most common programming objects and tasks required for Media Services development.</span></span> <span data-ttu-id="6afe9-106">À la fin de ce didacticiel, vous pourrez lire en continu ou télécharger de façon progressive un exemple de fichier multimédia que vous aurez chargé, encodé et téléchargé.</span><span class="sxs-lookup"><span data-stu-id="6afe9-106">At the completion of the tutorial, you will be able to stream or progressively download a sample media file that you uploaded, encoded, and downloaded.</span></span>

<span data-ttu-id="6afe9-107">L’image suivante illustre certains des objets couramment utilisés lors du développement d’applications VoD par rapport au modèle OData de Media Services.</span><span class="sxs-lookup"><span data-stu-id="6afe9-107">The following image shows some of the most commonly used objects when developing VoD applications against the Media Services OData model.</span></span>

<span data-ttu-id="6afe9-108">Cliquez sur l’image pour l’afficher en plein écran.</span><span class="sxs-lookup"><span data-stu-id="6afe9-108">Click the image to view it full size.</span></span>  

<a href="./media/media-services-rest-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-rest-get-started/media-services-overview-object-model-small.png"></a> 

## <a name="prerequisites"></a><span data-ttu-id="6afe9-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="6afe9-109">Prerequisites</span></span>
<span data-ttu-id="6afe9-110">Les conditions préalables suivantes sont requises pour commencer à développer avec les API REST et Media Services.</span><span class="sxs-lookup"><span data-stu-id="6afe9-110">The following prerequisites are required to start developing with Media Services with REST APIs.</span></span>

* <span data-ttu-id="6afe9-111">Un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="6afe9-111">An Azure account.</span></span> <span data-ttu-id="6afe9-112">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6afe9-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="6afe9-113">Un compte Media Services.</span><span class="sxs-lookup"><span data-stu-id="6afe9-113">A Media Services account.</span></span> <span data-ttu-id="6afe9-114">Pour créer un compte Media Services, consultez [Création d’un compte Media Services](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="6afe9-114">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="6afe9-115">Présentation du développement avec l’API REST Media Services.</span><span class="sxs-lookup"><span data-stu-id="6afe9-115">Understanding of how to develop with Media Services REST API.</span></span> <span data-ttu-id="6afe9-116">Pour plus d’informations, consultez [Vue d’ensemble de l’API REST Media Services](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="6afe9-116">For more information, see [Media Services REST API overview](media-services-rest-how-to-use.md).</span></span>
* <span data-ttu-id="6afe9-117">Une application de votre choix qui peut envoyer des demandes et réponses HTTP.</span><span class="sxs-lookup"><span data-stu-id="6afe9-117">An application of your choice that can send HTTP requests and responses.</span></span> <span data-ttu-id="6afe9-118">Ce didacticiel utilise [Fiddler](http://www.telerik.com/download/fiddler).</span><span class="sxs-lookup"><span data-stu-id="6afe9-118">This tutorial uses [Fiddler](http://www.telerik.com/download/fiddler).</span></span>

<span data-ttu-id="6afe9-119">Ce document de démarrage rapide présente les tâches suivantes.</span><span class="sxs-lookup"><span data-stu-id="6afe9-119">The following tasks are shown in this quickstart.</span></span>

1. <span data-ttu-id="6afe9-120">Démarrer les points de terminaison de streaming (à l’aide du portail Azure).</span><span class="sxs-lookup"><span data-stu-id="6afe9-120">Start streaming endpoint (using the Azure portal).</span></span>
2. <span data-ttu-id="6afe9-121">Connexion à un compte Media Services à l’aide de l’API REST</span><span class="sxs-lookup"><span data-stu-id="6afe9-121">Connect to the Media Services account with REST API.</span></span>
3. <span data-ttu-id="6afe9-122">Création d’une ressource et téléchargement d’un fichier vidéo à l’aide de l’API REST</span><span class="sxs-lookup"><span data-stu-id="6afe9-122">Create a new asset and upload a video file with REST API.</span></span>
4. <span data-ttu-id="6afe9-123">Encodage du fichier source en un ensemble de fichiers MP4 à débit adaptatif avec l’API REST</span><span class="sxs-lookup"><span data-stu-id="6afe9-123">Encode the source file into a set of adaptive bitrate MP4 files with REST API.</span></span>
5. <span data-ttu-id="6afe9-124">Publication des éléments et obtention des URL de diffusion et de téléchargement progressif avec l’API REST</span><span class="sxs-lookup"><span data-stu-id="6afe9-124">Publish the asset and get streaming and progressive download URLs with REST API.</span></span>
6. <span data-ttu-id="6afe9-125">Lire votre contenu.</span><span class="sxs-lookup"><span data-stu-id="6afe9-125">Play your content.</span></span>

>[!NOTE]
><span data-ttu-id="6afe9-126">Un nombre limite de 1 000 000 a été défini pour les différentes stratégies AMS (par exemple, pour la stratégie de localisateur ou pour ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="6afe9-126">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="6afe9-127">Vous devez utiliser le même ID de stratégie si vous utilisez toujours les mêmes jours / autorisations d’accès, par exemple, les stratégies pour les localisateurs destinées à demeurer en place pendant une longue période (stratégies sans chargement).</span><span class="sxs-lookup"><span data-stu-id="6afe9-127">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="6afe9-128">Pour plus d’informations, consultez [cette rubrique](media-services-dotnet-manage-entities.md#limit-access-policies) .</span><span class="sxs-lookup"><span data-stu-id="6afe9-128">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="6afe9-129">Pour plus d’informations sur les entités REST AMS utilisées dans cette rubrique, consultez [Informations de référence sur l’API REST de Media Services](/rest/api/media/services/azure-media-services-rest-api-reference).</span><span class="sxs-lookup"><span data-stu-id="6afe9-129">For details about AMS REST entities used in this topic, see [Azure Media Services REST API Reference](/rest/api/media/services/azure-media-services-rest-api-reference).</span></span> <span data-ttu-id="6afe9-130">Consultez également [Concepts Azure Media Services](media-services-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="6afe9-130">Also, see [Azure Media Services concepts](media-services-concepts.md).</span></span>

>[!NOTE]
><span data-ttu-id="6afe9-131">Lors de l’accès aux entités dans Media Services, vous devez définir les valeurs et les champs d’en-tête spécifiques dans vos requêtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="6afe9-131">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="6afe9-132">Pour plus d'informations, consultez [Installation pour le développement REST API de Media Services](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="6afe9-132">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="start-streaming-endpoints-using-the-azure-portal"></a><span data-ttu-id="6afe9-133">Démarrer les points de terminaison de streaming à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="6afe9-133">Start streaming endpoints using the Azure portal</span></span>

<span data-ttu-id="6afe9-134">Lorsque vous utilisez Azure Media Services, la diffusion de vidéos en continu à débit binaire adaptatif constitue l’un des scénarios les plus courants.</span><span class="sxs-lookup"><span data-stu-id="6afe9-134">When working with Azure Media Services one of the most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="6afe9-135">Media Services assure l’empaquetage dynamique, qui vous permet de distribuer juste-à-temps un contenu encodé en MP4 à débit adaptatif dans un format de diffusion en continu pris en charge par Media Services (MPEG DASH, HLS, Smooth Streaming), sans qu’il vous soit nécessaire de stocker des versions pré-empaquetées de chacun de ces formats.</span><span class="sxs-lookup"><span data-stu-id="6afe9-135">Media Services provides dynamic packaging, which allows you to deliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having to store pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="6afe9-136">Une fois votre compte AMS créé, un point de terminaison de streaming **par défaut** est ajouté à votre compte à l’état **Arrêté**.</span><span class="sxs-lookup"><span data-stu-id="6afe9-136">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="6afe9-137">Pour démarrer la diffusion en continu de votre contenu et tirer parti de l’empaquetage et du chiffrement dynamiques, le point de terminaison de streaming à partir duquel vous souhaitez diffuser du contenu doit se trouver à l’état **En cours d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="6afe9-137">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span>

<span data-ttu-id="6afe9-138">Pour démarrer le point de terminaison de streaming, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="6afe9-138">To start the streaming endpoint, do the following:</span></span>

1. <span data-ttu-id="6afe9-139">Connectez-vous au [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="6afe9-139">Log in at the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="6afe9-140">Dans la fenêtre Paramètres, cliquez sur Points de terminaison de streaming.</span><span class="sxs-lookup"><span data-stu-id="6afe9-140">In the Settings window, click Streaming endpoints.</span></span>
3. <span data-ttu-id="6afe9-141">Cliquez sur le point de terminaison de diffusion en continu par défaut.</span><span class="sxs-lookup"><span data-stu-id="6afe9-141">Click the default streaming endpoint.</span></span>

    <span data-ttu-id="6afe9-142">La fenêtre DEFAULT STREAMING ENDPOINT DETAILS (DÉTAILS DU POINT DE TERMINAISON DE STREAMING PAR DÉFAUT) s’affiche.</span><span class="sxs-lookup"><span data-stu-id="6afe9-142">The DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="6afe9-143">Cliquez sur l’icône de démarrage.</span><span class="sxs-lookup"><span data-stu-id="6afe9-143">Click the Start icon.</span></span>
5. <span data-ttu-id="6afe9-144">Cliquez sur le bouton Enregistrer pour enregistrer vos modifications.</span><span class="sxs-lookup"><span data-stu-id="6afe9-144">Click the Save button to save your changes.</span></span>

## <span data-ttu-id="6afe9-145"><a id="connect"></a>Connexion à un compte Media Services à l’aide de l’API REST</span><span class="sxs-lookup"><span data-stu-id="6afe9-145"><a id="connect"></a>Connect to the Media Services account with REST API</span></span>

<span data-ttu-id="6afe9-146">Pour savoir comment vous connecter à l’API AMS, consultez [Accéder à l’API Azure Media Services avec l’authentification Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="6afe9-146">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="6afe9-147">Après vous être connecté à https://media.windows.net, vous recevrez une redirection 301 spécifiant un autre URI Media Services.</span><span class="sxs-lookup"><span data-stu-id="6afe9-147">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="6afe9-148">Vous devez faire d’autres appels au nouvel URI.</span><span class="sxs-lookup"><span data-stu-id="6afe9-148">You must make subsequent calls to the new URI.</span></span>

<span data-ttu-id="6afe9-149">Par exemple, si après avoir essayé de vous connecter, vous avez les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="6afe9-149">For example, if after trying to connect, you got the following:</span></span>

    HTTP/1.1 301 Moved Permanently
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/

<span data-ttu-id="6afe9-150">Vous devez enregistrer vos appels d’API suivants à https://wamsbayclus001rest-hs.cloudapp.net/api/.</span><span class="sxs-lookup"><span data-stu-id="6afe9-150">You should post your subsequent API calls to https://wamsbayclus001rest-hs.cloudapp.net/api/.</span></span>

## <span data-ttu-id="6afe9-151"><a id="upload"></a>Création d’une ressource et téléchargement d’un fichier vidéo à l’aide de l’API REST</span><span class="sxs-lookup"><span data-stu-id="6afe9-151"><a id="upload"></a>Create a new asset and upload a video file with REST API</span></span>

<span data-ttu-id="6afe9-152">Dans Media Services, vous téléchargez vos fichiers numériques dans une ressource.</span><span class="sxs-lookup"><span data-stu-id="6afe9-152">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="6afe9-153">L’entité **Asset** peut contenir des fichiers vidéo et audio, des images, des collections de miniatures, des pistes textuelles et des légendes (et les métadonnées concernant ces fichiers).  Une fois les fichiers téléchargés dans la ressource, votre contenu est stocké en toute sécurité dans le cloud et peut faire l’objet d’un traitement et d’une diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="6afe9-153">The **Asset** entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files.)  Once the files are uploaded into the asset, your content is stored securely in the cloud for further processing and streaming.</span></span>

<span data-ttu-id="6afe9-154">Les options de création de ressources sont une des valeurs que vous devez fournir lors de la création d’une ressource.</span><span class="sxs-lookup"><span data-stu-id="6afe9-154">One of the values that you have to provide when creating an asset is asset creation options.</span></span> <span data-ttu-id="6afe9-155">La propriété **Options** est une valeur d’énumération qui décrit les options de chiffrement permettant de créer une ressource.</span><span class="sxs-lookup"><span data-stu-id="6afe9-155">The **Options** property is an enumeration value that describes the encryption options that an Asset can be created with.</span></span> <span data-ttu-id="6afe9-156">Une valeur valide est une des valeurs de la liste ci-dessous, et non une combinaison de valeurs de cette liste :</span><span class="sxs-lookup"><span data-stu-id="6afe9-156">A valid value is one of the values from the list below, not a combination of values from this list:</span></span>

* <span data-ttu-id="6afe9-157">**None** = **0** : aucun chiffrement.</span><span class="sxs-lookup"><span data-stu-id="6afe9-157">**None** = **0** - No encryption is used.</span></span> <span data-ttu-id="6afe9-158">Quand vous utilisez cette option, votre contenu n'est pas protégé pendant le transit ou le repos dans le stockage.</span><span class="sxs-lookup"><span data-stu-id="6afe9-158">When using this option your content is not protected in transit or at rest in storage.</span></span>
    <span data-ttu-id="6afe9-159">Si vous prévoyez de fournir un MP4 sous forme de téléchargement progressif, utilisez cette option.</span><span class="sxs-lookup"><span data-stu-id="6afe9-159">If you plan to deliver an MP4 using progressive download, use this option.</span></span>
* <span data-ttu-id="6afe9-160">**StorageEncrypted** = **1** : permet de chiffrer votre contenu en clair localement en utilisant le chiffrement AES-256 bits, puis de le télécharger vers le Stockage Azure où il est chiffré pour le stockage, au repos.</span><span class="sxs-lookup"><span data-stu-id="6afe9-160">**StorageEncrypted** = **1** - Encrypts your clear content locally using AES-256 bit encryption and then uploads it to Azure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="6afe9-161">Les éléments multimédias protégés par le chiffrement de stockage sont automatiquement déchiffrés et placés dans un système de fichiers chiffré avant d’être encodés, puis éventuellement rechiffrés avant d’être rechargés sous la forme d’un nouvel élément multimédia de sortie.</span><span class="sxs-lookup"><span data-stu-id="6afe9-161">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior to encoding, and optionally re-encrypted prior to uploading back as a new output asset.</span></span> <span data-ttu-id="6afe9-162">Le principal cas d'utilisation du chiffrement de stockage concerne la sécurisation de fichiers multimédias d'entrée de haute qualité avec un chiffrement renforcé au repos sur le disque.</span><span class="sxs-lookup"><span data-stu-id="6afe9-162">The primary use case for Storage Encryption is when you want to secure your high-quality input media files with strong encryption at rest on disk.</span></span>
* <span data-ttu-id="6afe9-163">**CommonEncryptionProtected** = **2** : utilisez cette option quand vous chargez du contenu qui a déjà été chiffré et protégé avec la DRM Common Encryption ou PlayReady (par exemple Smooth Streaming protégé avec la DRM PlayReady).</span><span class="sxs-lookup"><span data-stu-id="6afe9-163">**CommonEncryptionProtected** = **2** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="6afe9-164">**EnvelopeEncryptionProtected** = **4** : utilisez cette option lorsque vous téléchargez un contenu au format TLS chiffré avec AES.</span><span class="sxs-lookup"><span data-stu-id="6afe9-164">**EnvelopeEncryptionProtected** = **4** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="6afe9-165">Les fichiers doivent avoir été encodés et chiffrés par le gestionnaire de transformation Transform Manager.</span><span class="sxs-lookup"><span data-stu-id="6afe9-165">The files must have been encoded and encrypted by Transform Manager.</span></span>

### <a name="create-an-asset"></a><span data-ttu-id="6afe9-166">Création d’une ressource</span><span class="sxs-lookup"><span data-stu-id="6afe9-166">Create an asset</span></span>
<span data-ttu-id="6afe9-167">Une ressource est un conteneur pour plusieurs types ou ensembles d’objets dans Media Services, y compris des fichiers vidéo, audio, des images, des collections de miniatures, des pistes textuelles et des légendes.</span><span class="sxs-lookup"><span data-stu-id="6afe9-167">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="6afe9-168">Dans l’API REST, la création d’une ressource nécessite d’envoyer une demande POST vers Media Services et de placer les informations de propriété concernant votre ressource dans le corps de la demande.</span><span class="sxs-lookup"><span data-stu-id="6afe9-168">In the REST API, creating an Asset requires sending POST request to Media Services and placing any property information about your asset in the request body.</span></span>

<span data-ttu-id="6afe9-169">L’exemple suivant montre comment créer une ressource.</span><span class="sxs-lookup"><span data-stu-id="6afe9-169">The following example shows how to create an asset.</span></span>

<span data-ttu-id="6afe9-170">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="6afe9-170">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Assets HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    x-ms-client-request-id: c59de965-bc89-4295-9a57-75d897e5221e
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 45

    {"Name":"BigBuckBunny.mp4", "Options":"0"}


<span data-ttu-id="6afe9-171">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="6afe9-171">**HTTP Response**</span></span>

<span data-ttu-id="6afe9-172">Si l’opération réussit, l’élément suivant est retourné :</span><span class="sxs-lookup"><span data-stu-id="6afe9-172">If successful, the following is returned:</span></span>

    HTTP/1.1 201 Created
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
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:06:40 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets/@Element",
       "Id":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "State":0,
       "Created":"2015-01-18T22:06:40.6010903Z",
       "LastModified":"2015-01-18T22:06:40.6010903Z",
       "AlternateId":null,
       "Name":"BigBuckBunny2.mp4",
       "Options":0,
       "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StorageAccountName":"storagetestaccount001"
    }

### <a name="create-an-assetfile"></a><span data-ttu-id="6afe9-173">Création d’un AssetFile</span><span class="sxs-lookup"><span data-stu-id="6afe9-173">Create an AssetFile</span></span>
<span data-ttu-id="6afe9-174">L’entité [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) représente un fichier audio ou vidéo stocké dans un conteneur d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="6afe9-174">The [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="6afe9-175">Un fichier de ressources est toujours associé à une ressource et une ressource peut contenir un ou plusieurs AssetFiles.</span><span class="sxs-lookup"><span data-stu-id="6afe9-175">An asset file is always associated with an asset, and an asset may contain one or many AssetFiles.</span></span> <span data-ttu-id="6afe9-176">La tâche de Media Services Encoder échoue si un objet de fichier de ressources n’est pas associé à un fichier numérique dans un conteneur d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="6afe9-176">The Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="6afe9-177">Après avoir téléchargé le fichier de ressource numérique dans un conteneur d’objets blob, vous utilisez la requête HTTP **MERGE** pour mettre à jour AssetFile avec des informations sur votre fichier multimédia (comme indiqué ultérieurement dans cette rubrique).</span><span class="sxs-lookup"><span data-stu-id="6afe9-177">After you upload your digital media file into a blob container, you use the **MERGE** HTTP request to update the AssetFile with information about your media file (as shown later in the topic).</span></span>

<span data-ttu-id="6afe9-178">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="6afe9-178">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Files HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 164

    {  
       "IsEncrypted":"false",
       "IsPrimary":"false",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


<span data-ttu-id="6afe9-179">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="6afe9-179">**HTTP Response**</span></span>

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


### <a name="creating-the-accesspolicy-with-write-permission"></a><span data-ttu-id="6afe9-180">Création d’AccessPolicy avec autorisation d’écriture</span><span class="sxs-lookup"><span data-stu-id="6afe9-180">Creating the AccessPolicy with write permission</span></span>
<span data-ttu-id="6afe9-181">Avant de télécharger des fichiers dans le stockage blob, définissez les droits de la stratégie d’accès pour l’écriture sur une ressource.</span><span class="sxs-lookup"><span data-stu-id="6afe9-181">Before uploading any files into blob storage, set the access policy rights for writing to an asset.</span></span> <span data-ttu-id="6afe9-182">Pour ce faire, utilisez POST avec une demande HTTP sur le jeu d’entités AccessPolicies.</span><span class="sxs-lookup"><span data-stu-id="6afe9-182">To do that, POST an HTTP request to the AccessPolicies entity set.</span></span> <span data-ttu-id="6afe9-183">N’oubliez pas de définir une valeur DurationInMinutes après la création ou vous recevrez en réponse un message d’erreur interne de serveur 500.</span><span class="sxs-lookup"><span data-stu-id="6afe9-183">Define a DurationInMinutes value upon creation or you receive a 500 Internal Server error message back in response.</span></span> <span data-ttu-id="6afe9-184">Pour plus d’informations sur AccessPolicies, consultez [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span><span class="sxs-lookup"><span data-stu-id="6afe9-184">For more information on AccessPolicies, see [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span></span>

<span data-ttu-id="6afe9-185">L’exemple suivant montre comment créer une stratégie AccessPolicy :</span><span class="sxs-lookup"><span data-stu-id="6afe9-185">The following example shows how to create an AccessPolicy:</span></span>

<span data-ttu-id="6afe9-186">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="6afe9-186">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 74

    {"Name":"NewUploadPolicy", "DurationInMinutes":"440", "Permissions":"2"}

<span data-ttu-id="6afe9-187">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="6afe9-187">**HTTP Response**</span></span>

<span data-ttu-id="6afe9-188">Si l’opération réussit, la réponse suivante est retournée :</span><span class="sxs-lookup"><span data-stu-id="6afe9-188">If successful, the following response is returned:</span></span>

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
    X-Powered-By: ASP.NET
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

### <a name="get-the-upload-url"></a><span data-ttu-id="6afe9-189">Obtention de l’URL de téléchargement</span><span class="sxs-lookup"><span data-stu-id="6afe9-189">Get the Upload URL</span></span>

<span data-ttu-id="6afe9-190">Pour recevoir l’URL de téléchargement réelle, créez un localisateur SAS.</span><span class="sxs-lookup"><span data-stu-id="6afe9-190">To receive the actual upload URL, create a SAS Locator.</span></span> <span data-ttu-id="6afe9-191">Les localisateurs définissent l’heure de début et le type de point de terminaison de connexion pour les clients qui souhaitent accéder aux fichiers d’une ressource.</span><span class="sxs-lookup"><span data-stu-id="6afe9-191">Locators define the start time and type of connection endpoint for clients that want to access Files in an Asset.</span></span> <span data-ttu-id="6afe9-192">Vous pouvez créer plusieurs entités de localisateurs pour une paire AccessPolicy et Asset donnée, afin de gérer les différentes demandes et besoins des clients.</span><span class="sxs-lookup"><span data-stu-id="6afe9-192">You can create multiple Locator entities for a given AccessPolicy and Asset pair to handle different client requests and needs.</span></span> <span data-ttu-id="6afe9-193">Chacun de ces localisateurs utilise la valeur StartTime et la valeur DurationInMinutes d’AccessPolicy pour déterminer la durée pendant laquelle une URL peut être utilisée.</span><span class="sxs-lookup"><span data-stu-id="6afe9-193">Each of these Locators uses the StartTime value plus the DurationInMinutes value of the AccessPolicy to determine the length of time a URL can be used.</span></span> <span data-ttu-id="6afe9-194">Pour plus d’informations, consultez la rubrique [Localisateur](https://docs.microsoft.com/rest/api/media/operations/locator).</span><span class="sxs-lookup"><span data-stu-id="6afe9-194">For more information, see [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>

<span data-ttu-id="6afe9-195">Une URL SAS a le format suivant :</span><span class="sxs-lookup"><span data-stu-id="6afe9-195">A SAS URL has the following format:</span></span>

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

<span data-ttu-id="6afe9-196">Certaines considérations s’appliquent :</span><span class="sxs-lookup"><span data-stu-id="6afe9-196">Some considerations apply:</span></span>

* <span data-ttu-id="6afe9-197">Vous ne pouvez avoir plus de cinq localisateurs uniques associés à une ressource donnée.</span><span class="sxs-lookup"><span data-stu-id="6afe9-197">You cannot have more than five unique Locators associated with a given Asset at one time.</span></span> <span data-ttu-id="6afe9-198">Pour plus d’informations, consultez la rubrique Localisateur.</span><span class="sxs-lookup"><span data-stu-id="6afe9-198">For more information, see Locator.</span></span>
* <span data-ttu-id="6afe9-199">Si vous avez besoin de télécharger vos fichiers immédiatement, vous devez définir la valeur StartTime sur cinq minutes avant l’heure actuelle.</span><span class="sxs-lookup"><span data-stu-id="6afe9-199">If you need to upload your files immediately, you should set your StartTime value to five minutes before the current time.</span></span> <span data-ttu-id="6afe9-200">Cela vient du fait qu’il peut exister un décalage horaire entre votre ordinateur client et Media Services.</span><span class="sxs-lookup"><span data-stu-id="6afe9-200">This is because there may be clock skew between your client machine and Media Services.</span></span> <span data-ttu-id="6afe9-201">De même, la valeur de StartTime doit être au format DateTime suivant : AAAA-MM-JJTHH:mm:ssZ (par exemple, « 2014-05-23T17:53:50Z »).</span><span class="sxs-lookup"><span data-stu-id="6afe9-201">Also, your StartTime value must be in the following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>    
* <span data-ttu-id="6afe9-202">Il peut y avoir un délai de 30 à 40 secondes après la création d’un localisateur avant qu’il soit disponible.</span><span class="sxs-lookup"><span data-stu-id="6afe9-202">There may be a 30-40 second delay after a Locator is created to when it is available for use.</span></span> <span data-ttu-id="6afe9-203">Ce problème s’applique aux localisateurs d’URL SAS et d’origine.</span><span class="sxs-lookup"><span data-stu-id="6afe9-203">This issue applies to both SAS URL and Origin Locators.</span></span>

<span data-ttu-id="6afe9-204">Pour plus d’informations sur les localisateurs de SAP, consultez [ce](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span><span class="sxs-lookup"><span data-stu-id="6afe9-204">For more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span></span>

<span data-ttu-id="6afe9-205">L’exemple suivant montre comment créer un localisateur d’URL SAS, tel que défini par la propriété Type dans le corps de la demande (« 1 » pour un localisateur SAS et « 2 » pour un localisateur d’origine à la demande).</span><span class="sxs-lookup"><span data-stu-id="6afe9-205">The following example shows how to create a SAS URL Locator, as defined by the Type property in the request body ("1" for a SAS locator and "2" for an On-Demand origin locator).</span></span> <span data-ttu-id="6afe9-206">La propriété **Path** retournée contient l’URL que vous devez utiliser pour télécharger votre fichier.</span><span class="sxs-lookup"><span data-stu-id="6afe9-206">The **Path** property returned contains the URL that you must use to upload your file.</span></span>

<span data-ttu-id="6afe9-207">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="6afe9-207">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Locators HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=f7f09258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 178

    {  
       "AccessPolicyId":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "AssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StartTime":"2015-02-18T16:45:53",
       "Type":1
    }


<span data-ttu-id="6afe9-208">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="6afe9-208">**HTTP Response**</span></span>

<span data-ttu-id="6afe9-209">Si l’opération réussit, la réponse suivante est retournée :</span><span class="sxs-lookup"><span data-stu-id="6afe9-209">If successful, the following response is returned:</span></span>

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

### <a name="upload-a-file-into-a-blob-storage-container"></a><span data-ttu-id="6afe9-210">Téléchargement d’un fichier dans un conteneur de stockage d’objets blob</span><span class="sxs-lookup"><span data-stu-id="6afe9-210">Upload a file into a blob storage container</span></span>
<span data-ttu-id="6afe9-211">Après avoir défini AccessPolicy et Locator, le fichier réel est téléchargé vers un conteneur de stockage d’objets blob Microsoft Azure à l’aide des API REST Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="6afe9-211">Once you have the AccessPolicy and Locator set, the actual file is uploaded to an Azure blob storage container using the Azure Storage REST APIs.</span></span> <span data-ttu-id="6afe9-212">Vous devez télécharger les fichiers en tant qu’objets blob de blocs.</span><span class="sxs-lookup"><span data-stu-id="6afe9-212">You must upload the files as block blobs.</span></span> <span data-ttu-id="6afe9-213">Les objets blob de pages ne sont pas pris en charge par Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="6afe9-213">Page blobs are not supported by Azure Media Services.</span></span>  

> [!NOTE]
> <span data-ttu-id="6afe9-214">Vous devez ajouter le nom du fichier à télécharger dans la valeur **Path** du localisateur reçue dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="6afe9-214">You must add the file name for the file you want to upload to the Locator **Path** value received in the previous section.</span></span> <span data-ttu-id="6afe9-215">Par exemple, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="6afe9-215">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="6afe9-216">.</span><span class="sxs-lookup"><span data-stu-id="6afe9-216">.</span></span> <span data-ttu-id="6afe9-217">.</span><span class="sxs-lookup"><span data-stu-id="6afe9-217">.</span></span> <span data-ttu-id="6afe9-218">.</span><span class="sxs-lookup"><span data-stu-id="6afe9-218">.</span></span>
>
>

<span data-ttu-id="6afe9-219">Pour plus d’informations sur l’utilisation d’objets blob de stockage Microsoft Azure, consultez [API REST du service BLOB](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="6afe9-219">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

### <a name="update-the-assetfile"></a><span data-ttu-id="6afe9-220">Mise à jour d’AssetFile</span><span class="sxs-lookup"><span data-stu-id="6afe9-220">Update the AssetFile</span></span>
<span data-ttu-id="6afe9-221">Maintenant que vous avez téléchargé votre fichier, mettez à jour les informations de taille FileAsset (et autres).</span><span class="sxs-lookup"><span data-stu-id="6afe9-221">Now that you've uploaded your file, update the FileAsset size (and other) information.</span></span> <span data-ttu-id="6afe9-222">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="6afe9-222">For example:</span></span>

    MERGE https://wamsbayclus001rest-hs.cloudapp.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5') HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net

    {  
       "ContentFileSize":"1186540",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


<span data-ttu-id="6afe9-223">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="6afe9-223">**HTTP Response**</span></span>

<span data-ttu-id="6afe9-224">Si l’opération réussit, l’élément suivant est retourné :</span><span class="sxs-lookup"><span data-stu-id="6afe9-224">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

## <a name="delete-the-locator-and-accesspolicy"></a><span data-ttu-id="6afe9-225">Suppression du localisateur et d’AcessPolicy</span><span class="sxs-lookup"><span data-stu-id="6afe9-225">Delete the Locator and AccessPolicy</span></span>
<span data-ttu-id="6afe9-226">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="6afe9-226">**HTTP Request**</span></span>

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="6afe9-227">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="6afe9-227">**HTTP Response**</span></span>

<span data-ttu-id="6afe9-228">Si l’opération réussit, l’élément suivant est retourné :</span><span class="sxs-lookup"><span data-stu-id="6afe9-228">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

<span data-ttu-id="6afe9-229">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="6afe9-229">**HTTP Request**</span></span>

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net

<span data-ttu-id="6afe9-230">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="6afe9-230">**HTTP Response**</span></span>

<span data-ttu-id="6afe9-231">Si l’opération réussit, l’élément suivant est retourné :</span><span class="sxs-lookup"><span data-stu-id="6afe9-231">If successful, the following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

## <span data-ttu-id="6afe9-232"><a id="encode"></a>Encoder le fichier source en un ensemble de fichiers MP4 à débit adaptatif</span><span class="sxs-lookup"><span data-stu-id="6afe9-232"><a id="encode"></a>Encode the source file into a set of adaptive bitrate MP4 files</span></span>

<span data-ttu-id="6afe9-233">Après avoir reçu des éléments multimédias dans Media Services, vous pouvez encoder un média, modifier le format de ce dernier, lui appliquer un filigrane, etc. avant de le livrer à des clients.</span><span class="sxs-lookup"><span data-stu-id="6afe9-233">After ingesting Assets into Media Services, media can be encoded, transmuxed, watermarked, and so on, before it is delivered to clients.</span></span> <span data-ttu-id="6afe9-234">Afin de garantir des performances et une disponibilité optimales, ces activités sont planifiées et exécutées dans de nombreuses instances de rôle en arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="6afe9-234">These activities are scheduled and run against multiple background role instances to ensure high performance and availability.</span></span> <span data-ttu-id="6afe9-235">Ces activités s’appellent des travaux et chaque Travail se compose de tâches atomiques qui effectuent le travail à proprement parler sur le fichier de ressource (pour plus d’informations, consultez les descriptions de [Travail](/rest/api/media/services/job) et [Tâche](/rest/api/media/services/task)).</span><span class="sxs-lookup"><span data-stu-id="6afe9-235">These activities are called Jobs and each Job is composed of atomic Tasks that do the actual work on the Asset file (for more information, see [Job](/rest/api/media/services/job), [Task](/rest/api/media/services/task) descriptions).</span></span>

<span data-ttu-id="6afe9-236">Comme mentionné précédemment, lorsque vous travaillez avec Azure Media Services, un des scénarios les plus courants est la diffusion de contenu à débit adaptatif à vos clients.</span><span class="sxs-lookup"><span data-stu-id="6afe9-236">As was mentioned earlier, when working with Azure Media Services one of the most common scenarios is delivering adaptive bitrate streaming to your clients.</span></span> <span data-ttu-id="6afe9-237">Media Services peut empaqueter de façon dynamique un ensemble de fichiers MP4 à débit adaptatif dans l’un des formats suivants : HTTP Live Streaming (HLS), Smooth Streaming et MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="6afe9-237">Media Services can dynamically package a set of adaptive bitrate MP4 files into one of the following formats: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span>

<span data-ttu-id="6afe9-238">La section suivante montre comment créer un travail contenant une tâche d’encodage.</span><span class="sxs-lookup"><span data-stu-id="6afe9-238">The following section shows how to create a job that contains one encoding task.</span></span> <span data-ttu-id="6afe9-239">La tâche spécifie de transcoder le fichier mezzanine en un ensemble de MP4 à débit adaptatif à l’aide de **Media Encoder Standard**.</span><span class="sxs-lookup"><span data-stu-id="6afe9-239">The task specifies to transcode the mezzanine file into a set of adaptive bitrate MP4s using **Media Encoder Standard**.</span></span> <span data-ttu-id="6afe9-240">La section indique également comment surveiller la progression du traitement du travail.</span><span class="sxs-lookup"><span data-stu-id="6afe9-240">The section also shows how to monitor the job processing progress.</span></span> <span data-ttu-id="6afe9-241">Une fois le travail terminé, vous pourrez créer les localisateurs nécessaires pour accéder à vos ressources.</span><span class="sxs-lookup"><span data-stu-id="6afe9-241">When the job is complete, you would be able to create locators that are needed to get access to your assets.</span></span>

### <a name="get-a-media-processor"></a><span data-ttu-id="6afe9-242">Obtention d’un processeur multimédia</span><span class="sxs-lookup"><span data-stu-id="6afe9-242">Get a media processor</span></span>
<span data-ttu-id="6afe9-243">Dans Media Services, un processeur multimédia est un composant qui gère une tâche de traitement spécifique, telle que l’encodage, la conversion de format, le chiffrement ou le déchiffrement de contenu multimédia.</span><span class="sxs-lookup"><span data-stu-id="6afe9-243">In Media Services, a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="6afe9-244">Pour la tâche d’encodage indiquée dans ce didacticiel, nous allons utiliser Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="6afe9-244">For the encoding task shown in this tutorial, we are going to use the Media Encoder Standard.</span></span>

<span data-ttu-id="6afe9-245">Le code suivant demande l’ID de l’encodeur.</span><span class="sxs-lookup"><span data-stu-id="6afe9-245">The following code requests the encoder's id.</span></span>

<span data-ttu-id="6afe9-246">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="6afe9-246">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=f7f09258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="6afe9-247">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="6afe9-247">**HTTP Response**</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 273
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 6beb04b4-55a7-480d-8aa8-e5c5d59ffa1f
    x-ms-request-id: 6beb04b4-55a7-480d-8aa8-e5c5d59ffa1f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 07:54:09 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "Description":"Media Encoder Standard",
             "Name":"Media Encoder Standard",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }

### <a name="create-a-job"></a><span data-ttu-id="6afe9-248">Création d’un travail</span><span class="sxs-lookup"><span data-stu-id="6afe9-248">Create a job</span></span>
<span data-ttu-id="6afe9-249">Chaque travail peut comporter une ou plusieurs tâches, en fonction du type de traitement que vous souhaitez accomplir.</span><span class="sxs-lookup"><span data-stu-id="6afe9-249">Each Job can have one or more Tasks depending on the type of processing that you want to accomplish.</span></span> <span data-ttu-id="6afe9-250">Via l’API REST, vous pouvez créer des travaux et leurs tâches associées de deux manières : les tâches peuvent être définies en ligne via la propriété de navigation de tâches sur les entités de travail ou via le traitement par lots OData.</span><span class="sxs-lookup"><span data-stu-id="6afe9-250">Through the REST API, you can create Jobs and their related Tasks in one of two ways: Tasks can be defined inline through the Tasks navigation property on Job entities, or through OData batch processing.</span></span> <span data-ttu-id="6afe9-251">Le Kit de développement logiciel (SDK) Media Services utilise le traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="6afe9-251">The Media Services SDK uses batch processing.</span></span> <span data-ttu-id="6afe9-252">Toutefois, pour une meilleure lisibilité des exemples de code dans cette rubrique, les tâches sont définies inline.</span><span class="sxs-lookup"><span data-stu-id="6afe9-252">However, for the readability of the code examples in this topic, tasks are defined inline.</span></span> <span data-ttu-id="6afe9-253">Pour plus d’informations sur le traitement par lots, consultez [Traitement par lots d’Open Data Protocol (OData)](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span><span class="sxs-lookup"><span data-stu-id="6afe9-253">For information on batch processing, see [Open Data Protocol (OData) Batch Processing](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span></span>

<span data-ttu-id="6afe9-254">L’exemple suivant montre comment créer et publier un projet avec une tâche visant à encoder une vidéo en une résolution et une qualité spécifiques.</span><span class="sxs-lookup"><span data-stu-id="6afe9-254">The following example shows you how to create and post a Job with one Task set to encode a video at a specific resolution and quality.</span></span> <span data-ttu-id="6afe9-255">La section suivante de la documentation contient la liste de toutes les [présélections de tâches](http://msdn.microsoft.com/library/mt269960) prises en charge par Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="6afe9-255">The following documentation section contains the list of all the [task presets](http://msdn.microsoft.com/library/mt269960) supported by the Media Encoder Standard processor.</span></span>  

<span data-ttu-id="6afe9-256">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="6afe9-256">**HTTP Request**</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Content-Type: application/json
    Accept: application/json;odata=verbose
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 482

    {  
       "Name":"NewTestJob",
       "InputMediaAssets":[  
          {  
             "__metadata":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Assets('nb%3Acid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')"
             }
          }
       ],
       "Tasks":[  
          {  
             "Configuration":"Adaptive Streaming",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset>
                <outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"
          }
       ]
    }

<span data-ttu-id="6afe9-257">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="6afe9-257">**HTTP Response**</span></span>

<span data-ttu-id="6afe9-258">Si l’opération réussit, la réponse suivante est retournée :</span><span class="sxs-lookup"><span data-stu-id="6afe9-258">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1215
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')
    Server: Microsoft-IIS/8.5
    request-id: 532ac1ec-a475-4dce-b2d5-7c8ce94ac87c
    x-ms-request-id: 532ac1ec-a475-4dce-b2d5-7c8ce94ac87c
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 08:04:35 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')",
             "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Job"
          },
          "Tasks":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/Tasks"
             }
          },
          "OutputMediaAssets":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/OutputMediaAssets"
             }
          },
          "InputMediaAssets":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')/InputMediaAssets"
             }
          },
          "Id":"nb:jid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
          "Name":"NewTestJob",
          "Created":"2015-01-19T08:04:34.3287057Z",
          "LastModified":"2015-01-19T08:04:34.3287057Z",
          "EndTime":null,
          "Priority":0,
          "RunningDuration":0,
          "StartTime":null,
          "State":0,
          "TemplateId":null,
          "JobNotificationSubscriptions":{  
             "__metadata":{  
                "type":"Collection(Microsoft.Cloud.Media.Vod.Rest.Data.Models.JobNotificationSubscription)"
             },
             "results":[  

             ]
          }
       }
    }


<span data-ttu-id="6afe9-259">Il convient de noter quelques points importants concernant les demandes de travail :</span><span class="sxs-lookup"><span data-stu-id="6afe9-259">There are a few important things to note in any Job request:</span></span>

* <span data-ttu-id="6afe9-260">les propriétés TaskBody DOIVENT utiliser un XML littéral pour définir le nombre de ressources d’entrée ou de sortie qui sont utilisées par la tâche.</span><span class="sxs-lookup"><span data-stu-id="6afe9-260">TaskBody properties MUST use literal XML to define the number of input, or output assets that are used by the Task.</span></span> <span data-ttu-id="6afe9-261">La rubrique Tâche contient la définition du schéma XML pour le XML.</span><span class="sxs-lookup"><span data-stu-id="6afe9-261">The Task topic contains the XML Schema Definition for the XML.</span></span>
* <span data-ttu-id="6afe9-262">Dans la définition TaskBody, chaque valeur interne de <inputAsset> et <outputAsset> doit être définie en tant que JobInputAsset(valeur) ou JobOutputAsset(valeur).</span><span class="sxs-lookup"><span data-stu-id="6afe9-262">In the TaskBody definition, each inner value for <inputAsset> and <outputAsset> must be set as JobInputAsset(value) or JobOutputAsset(value).</span></span>
* <span data-ttu-id="6afe9-263">Une tâche peut comporter plusieurs ressources de sortie.</span><span class="sxs-lookup"><span data-stu-id="6afe9-263">A task can have multiple output assets.</span></span> <span data-ttu-id="6afe9-264">Un JobOutputAsset(x) ne peut être utilisé qu’une fois en tant que résultat d’une tâche dans un travail.</span><span class="sxs-lookup"><span data-stu-id="6afe9-264">One JobOutputAsset(x) can only be used once as an output of a task in a job.</span></span>
* <span data-ttu-id="6afe9-265">Vous pouvez spécifier JobInputAsset ou JobOutputAsset en tant que ressource d’entrée d’une tâche.</span><span class="sxs-lookup"><span data-stu-id="6afe9-265">You can specify JobInputAsset or JobOutputAsset as an input asset of a task.</span></span>
* <span data-ttu-id="6afe9-266">Les tâches ne doivent pas former un cycle.</span><span class="sxs-lookup"><span data-stu-id="6afe9-266">Tasks must not form a cycle.</span></span>
* <span data-ttu-id="6afe9-267">Le paramètre de valeur que vous transmettez à JobInputAsset ou à JobOutputAsset représente la valeur d’index pour une ressource.</span><span class="sxs-lookup"><span data-stu-id="6afe9-267">The value parameter that you pass to JobInputAsset or JobOutputAsset represents the index value for an Asset.</span></span> <span data-ttu-id="6afe9-268">Les ressources réelles sont définies dans les propriétés de navigation InputMediaAssets et OutputMediaAssets de la définition d’entité de travail.</span><span class="sxs-lookup"><span data-stu-id="6afe9-268">The actual Assets are defined in the InputMediaAssets and OutputMediaAssets navigation properties on the Job entity definition.</span></span>

> [!NOTE]
> <span data-ttu-id="6afe9-269">Étant donné que Media Services est basé sur OData v3, les ressources dans les collections de propriétés de navigation InputMediaAssets et OutputMediaAssets sont référencées par une paire nom de valeur « __metadata : uri ».</span><span class="sxs-lookup"><span data-stu-id="6afe9-269">Because Media Services is built on OData v3, the individual assets in InputMediaAssets and OutputMediaAssets navigation property collections are referenced through a "__metadata : uri" name-value pair.</span></span>
>
>

* <span data-ttu-id="6afe9-270">InputMediaAssets mappe vers une ou plusieurs ressources que vous avez créées dans Media Services.</span><span class="sxs-lookup"><span data-stu-id="6afe9-270">InputMediaAssets maps to one or more Assets you have created in Media Services.</span></span> <span data-ttu-id="6afe9-271">Les OutputMediaAssets sont créés par le système.</span><span class="sxs-lookup"><span data-stu-id="6afe9-271">OutputMediaAssets are created by the system.</span></span> <span data-ttu-id="6afe9-272">Ils ne font pas référence à une ressource existante.</span><span class="sxs-lookup"><span data-stu-id="6afe9-272">They do not reference an existing asset.</span></span>
* <span data-ttu-id="6afe9-273">OutputMediaAssets peut être nommé à l’aide de l’attribut assetName.</span><span class="sxs-lookup"><span data-stu-id="6afe9-273">OutputMediaAssets can be named using the assetName attribute.</span></span> <span data-ttu-id="6afe9-274">Si cet attribut n’est pas présent, le nom d’OutputMediaAsset est la valeur de texte interne de l’élément <outputAsset> avec le suffixe de la valeur du nom du travail ou de l’ID de travail (dans le cas où la propriété Name n’est pas définie).</span><span class="sxs-lookup"><span data-stu-id="6afe9-274">If this attribute is not present, then the name of the OutputMediaAsset is whatever the inner text value of the <outputAsset> element is with a suffix of either the Job Name value, or the Job Id value (in the case where the Name property isn't defined).</span></span> <span data-ttu-id="6afe9-275">Par exemple, si vous affectez à assetName la valeur « Sample », la propriété de Nom d’OutputMediaAsset est définie sur « Sample ».</span><span class="sxs-lookup"><span data-stu-id="6afe9-275">For example, if you set a value for assetName to "Sample", then the OutputMediaAsset Name property would be set to "Sample".</span></span> <span data-ttu-id="6afe9-276">Toutefois, si vous n’avez pas défini de valeur pour assetName, mais avez défini le nom du travail comme « NewJob », le nom d’OutputMediaAsset est « JobOutputAsset(value)_NewJob ».</span><span class="sxs-lookup"><span data-stu-id="6afe9-276">However, if you did not set a value for assetName, but did set the job name to "NewJob", then the OutputMediaAsset Name would be "JobOutputAsset(value)_NewJob".</span></span>

    <span data-ttu-id="6afe9-277">L’exemple suivant montre comment définir l’attribut assetName :</span><span class="sxs-lookup"><span data-stu-id="6afe9-277">The following example shows how to set the assetName attribute:</span></span>

        "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"
* <span data-ttu-id="6afe9-278">Pour activer le chaînage des tâches :</span><span class="sxs-lookup"><span data-stu-id="6afe9-278">To enable task chaining:</span></span>

  * <span data-ttu-id="6afe9-279">un travail doit comporter au moins deux tâches</span><span class="sxs-lookup"><span data-stu-id="6afe9-279">A job must have at least two tasks</span></span>
  * <span data-ttu-id="6afe9-280">Il doit y avoir au moins une tâche dont l’entrée correspond à la sortie d’une autre tâche du travail.</span><span class="sxs-lookup"><span data-stu-id="6afe9-280">There must be at least one task whose input is output of another task in the job.</span></span>

<span data-ttu-id="6afe9-281">Pour plus d’informations, consultez la page [Création d’une tâche d’encodage avec l’API REST Media Services](media-services-rest-encode-asset.md).</span><span class="sxs-lookup"><span data-stu-id="6afe9-281">For more information see, [Creating an Encoding Job with the Media Services REST API](media-services-rest-encode-asset.md).</span></span>

### <a name="monitor-processing-progress"></a><span data-ttu-id="6afe9-282">Surveillance de la progression du traitement</span><span class="sxs-lookup"><span data-stu-id="6afe9-282">Monitor Processing Progress</span></span>
<span data-ttu-id="6afe9-283">Vous pouvez récupérer l’état du travail à l’aide de la propriété State, comme l’illustre l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="6afe9-283">You can retrieve the Job status by using the State property, as shown in the following example.</span></span>

<span data-ttu-id="6afe9-284">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="6afe9-284">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/State HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=zf84471d-2233-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908022&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=RYXOraO6Z%2f7l9whWZQN%2bypeijgHwIk8XyikA01Kx1%2bk%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 0


<span data-ttu-id="6afe9-285">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="6afe9-285">**HTTP Response**</span></span>

<span data-ttu-id="6afe9-286">Si l’opération réussit, la réponse suivante est retournée :</span><span class="sxs-lookup"><span data-stu-id="6afe9-286">If successful, the following response is returned:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 17
    Content-Type: application/json;odata=verbose;charset=utf-8
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 01324d81-18e2-4493-a3e5-c6186209f0c8
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Sun, 13 May 2012 05:16:53 GMT

    {"d":{"State":2}}


### <a name="cancel-a-job"></a><span data-ttu-id="6afe9-287">Annulation d’une tâche</span><span class="sxs-lookup"><span data-stu-id="6afe9-287">Cancel a job</span></span>
<span data-ttu-id="6afe9-288">Media Services vous permet d’annuler les travaux en cours d’exécution via la fonction CancelJob.</span><span class="sxs-lookup"><span data-stu-id="6afe9-288">Media Services allows you to cancel running jobs through the CancelJob function.</span></span> <span data-ttu-id="6afe9-289">Cet appel renvoie un code d’erreur 400 si vous essayez d’annuler un Travail dont l’état est annulé, en cours d’annulation, erreur ou terminé.</span><span class="sxs-lookup"><span data-stu-id="6afe9-289">This call returns a 400 error code if you try to cancel a Job when its state is canceled, canceling, error, or finished.</span></span>

<span data-ttu-id="6afe9-290">L’exemple suivant montre comment appeler CancelJob.</span><span class="sxs-lookup"><span data-stu-id="6afe9-290">The following example shows how to call CancelJob.</span></span>

<span data-ttu-id="6afe9-291">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="6afe9-291">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.net/API/CancelJob?jobid='nb%3ajid%3aUUID%3a71d2dd33-efdf-ec43-8ea1-136a110bd42c' HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.2
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908753&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=kolAgnFfbQIeRv4lWxKSFa4USyjWXRm15Kd%2bNd5g8eA%3d
    Host: wamsbayclus001rest-hs.net


<span data-ttu-id="6afe9-292">Si l’opération réussit, un code de réponse 204 est retourné, sans corps de message.</span><span class="sxs-lookup"><span data-stu-id="6afe9-292">If successful, a 204 response code is returned with no message body.</span></span>

> [!NOTE]
> <span data-ttu-id="6afe9-293">Vous devez encoder par l’URL l’ID de travail (normalement nb:jid:UUID: valeur) lorsque vous la transmettez en tant que paramètre à la fonction CancelJob.</span><span class="sxs-lookup"><span data-stu-id="6afe9-293">You must URL-encode the job id (normally nb:jid:UUID: somevalue) when passing it in as a parameter to CancelJob.</span></span>
>
>

### <a name="get-the-output-asset"></a><span data-ttu-id="6afe9-294">Obtention de la ressource de sortie</span><span class="sxs-lookup"><span data-stu-id="6afe9-294">Get the output asset</span></span>
<span data-ttu-id="6afe9-295">Le code suivant montre comment demander l’ID de la ressource de sortie</span><span class="sxs-lookup"><span data-stu-id="6afe9-295">The following code shows how to request the output asset Id.</span></span>

<span data-ttu-id="6afe9-296">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="6afe9-296">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/OutputMediaAssets() HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="6afe9-297">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="6afe9-297">**HTTP Response**</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 445
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 73cd605d-066a-46f1-8358-f4bd25a9220a
    x-ms-request-id: 73cd605d-066a-46f1-8358-f4bd25a9220a
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 08:28:13 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets",
       "value":[  
          {  
             "Id":"nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
             "State":0,
             "Created":"2015-01-19T07:52:15.603",
             "LastModified":"2015-01-19T07:52:15.603",
             "AlternateId":null,
             "Name":"Multibitrate MP4s",
             "Options":0,
             "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-71d2dd33-efdf-ec43-8ea1-136a110bd42c",
             "StorageAccountName":"storagetestaccount001"
          }
       ]
    }



## <span data-ttu-id="6afe9-298"><a id="publish_get_urls"></a>Publication des éléments et obtention des URL de diffusion et de téléchargement progressif avec l’API REST</span><span class="sxs-lookup"><span data-stu-id="6afe9-298"><a id="publish_get_urls"></a>Publish the asset and get streaming and progressive download URLs with REST API</span></span>

<span data-ttu-id="6afe9-299">Pour diffuser en continu ou télécharger un élément multimédia, vous devez tout d'abord le « publier » en créant un localisateur.</span><span class="sxs-lookup"><span data-stu-id="6afe9-299">To stream or download an asset, you first need to "publish" it by creating a locator.</span></span> <span data-ttu-id="6afe9-300">Les localisateurs assurent l’accès aux fichiers contenus dans l’élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="6afe9-300">Locators provide access to files contained in the asset.</span></span> <span data-ttu-id="6afe9-301">Media Services prend en charge deux types de localisateurs : les localisateurs OnDemandOrigin, utilisés pour diffuser du contenu multimédia (par exemple, MPEG DASH, HLS ou Smooth Streaming) et les localisateurs d’URL SAS (signature d’accès partagé), utilisés pour télécharger des fichiers multimédias.</span><span class="sxs-lookup"><span data-stu-id="6afe9-301">Media Services supports two types of locators: OnDemandOrigin locators, used to stream media (for example, MPEG DASH, HLS, or Smooth Streaming) and Access Signature (SAS) locators, used to download media files.</span></span> <span data-ttu-id="6afe9-302">Pour plus d’informations sur les localisateurs de SAP, consultez [ce](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span><span class="sxs-lookup"><span data-stu-id="6afe9-302">For more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span></span>

<span data-ttu-id="6afe9-303">Une fois que vous avez créé les localisateurs, vous pouvez générer les URL utilisées pour transmettre en continu ou télécharger les fichiers.</span><span class="sxs-lookup"><span data-stu-id="6afe9-303">Once you create the locators, you can build the URLs that are used to stream or download your files.</span></span>

>[!NOTE]
><span data-ttu-id="6afe9-304">Une fois votre compte AMS créé, un point de terminaison de streaming **par défaut** est ajouté à votre compte à l’état **Arrêté**.</span><span class="sxs-lookup"><span data-stu-id="6afe9-304">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="6afe9-305">Pour démarrer la diffusion en continu de votre contenu et tirer parti de l’empaquetage et du chiffrement dynamiques, le point de terminaison de streaming à partir duquel vous souhaitez diffuser du contenu doit se trouver à l’état **En cours d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="6afe9-305">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span>

<span data-ttu-id="6afe9-306">Les URL de diffusion en continu pour Smooth Streaming ont le format suivant :</span><span class="sxs-lookup"><span data-stu-id="6afe9-306">A streaming URL for Smooth Streaming has the following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="6afe9-307">Les URL de diffusion en continu pour HLS ont le format suivant :</span><span class="sxs-lookup"><span data-stu-id="6afe9-307">A streaming URL for HLS has the following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="6afe9-308">Les URL de diffusion en continu pour MPEG DASH ont le format suivant :</span><span class="sxs-lookup"><span data-stu-id="6afe9-308">A streaming URL for MPEG DASH has the following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


<span data-ttu-id="6afe9-309">Les URL SAS permettant de télécharger les fichiers ont le format suivant :</span><span class="sxs-lookup"><span data-stu-id="6afe9-309">A SAS URL used to download files has the following format:</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

<span data-ttu-id="6afe9-310">Cette section montre comment effectuer les tâches suivantes, nécessaires pour « publier » vos ressources.</span><span class="sxs-lookup"><span data-stu-id="6afe9-310">This section shows how to perform the following tasks necessary to "publish" your assets.</span></span>  

* <span data-ttu-id="6afe9-311">Création d’AccessPolicy avec autorisation de lecture</span><span class="sxs-lookup"><span data-stu-id="6afe9-311">Creating the AccessPolicy with read permission</span></span>
* <span data-ttu-id="6afe9-312">Création d’une URL SAS pour le téléchargement de contenu</span><span class="sxs-lookup"><span data-stu-id="6afe9-312">Creating a SAS URL for downloading content</span></span>
* <span data-ttu-id="6afe9-313">Création d’une URL d’origine pour la diffusion en continu de contenu</span><span class="sxs-lookup"><span data-stu-id="6afe9-313">Creating an origin URL for streaming content</span></span>

### <a name="creating-the-accesspolicy-with-read-permission"></a><span data-ttu-id="6afe9-314">Création d’AccessPolicy avec autorisation de lecture</span><span class="sxs-lookup"><span data-stu-id="6afe9-314">Creating the AccessPolicy with read permission</span></span>
<span data-ttu-id="6afe9-315">Avant de télécharger ou de diffuser en continu du contenu multimédia, il convient tout d’abord de définir une AccessPolicy avec des autorisations de lecture et de créer l’entité de localisateur appropriée, qui spécifie le type de mécanisme de remise que vous souhaitez activer pour vos clients.</span><span class="sxs-lookup"><span data-stu-id="6afe9-315">Before downloading or streaming any media content, first define an AccessPolicy with read permissions and create the appropriate Locator entity that specifies the type of delivery mechanism you want to enable for your clients.</span></span> <span data-ttu-id="6afe9-316">Pour plus d’informations sur les propriétés disponibles, consultez [Propriétés de l’entité AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties).</span><span class="sxs-lookup"><span data-stu-id="6afe9-316">For more information on the properties available, see [AccessPolicy Entity Properties](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties).</span></span>

<span data-ttu-id="6afe9-317">L’exemple suivant montre comment spécifier AccessPolicy pour les autorisations de lecture d’une ressource donnée.</span><span class="sxs-lookup"><span data-stu-id="6afe9-317">The following example shows how to specify the AccessPolicy for read permissions for a given Asset.</span></span>

    POST https://wamsbayclus001rest-hs.net/API/AccessPolicies HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 74
    Expect: 100-continue

    {"Name": "DownloadPolicy", "DurationInMinutes" : "300", "Permissions" : 1}

<span data-ttu-id="6afe9-318">Si l’opération réussit, un code de succès 201 est renvoyé et décrit l’entité AccessPolicy que vous avez créée.</span><span class="sxs-lookup"><span data-stu-id="6afe9-318">If successful, a 201 success code is returned describing the AccessPolicy entity that you created.</span></span> <span data-ttu-id="6afe9-319">Vous utilisez ensuite l’ID de l’AccessPolicy et l’ID de la ressource contenant le fichier que vous souhaitez remettre (par exemple, une ressource de sortie) pour créer l’entité de localisateur.</span><span class="sxs-lookup"><span data-stu-id="6afe9-319">You then use the AccessPolicy Id along with the Asset Id of the asset that contains the file you want to deliver(such as an output asset) to create the Locator entity.</span></span>

> [!NOTE]
> <span data-ttu-id="6afe9-320">Ce flux de travail de base est le même que pour le téléchargement d’un fichier lors de la réception d’une ressource (comme expliqué précédemment dans cette rubrique).</span><span class="sxs-lookup"><span data-stu-id="6afe9-320">This basic workflow is the same as uploading a file when ingesting an Asset (as was discussed earlier in this topic).</span></span> <span data-ttu-id="6afe9-321">En outre, comme pour le téléchargement de fichiers, si vous (ou vos clients) devez accéder à vos fichiers immédiatement, définissez la valeur StartTime cinq minutes avant l’heure actuelle.</span><span class="sxs-lookup"><span data-stu-id="6afe9-321">Also, like uploading files, if you (or your clients) need to access your files immediately, set your StartTime value to five minutes before the current time.</span></span> <span data-ttu-id="6afe9-322">Cela vient du fait qu’il peut exister un décalage horaire entre le client et Media Services.</span><span class="sxs-lookup"><span data-stu-id="6afe9-322">This action is necessary because there may be clock skew between the client and Media Services.</span></span> <span data-ttu-id="6afe9-323">La valeur de StartTime doit être au format DateTime suivant : AAAA-MM-JJTHH:mm:ssZ (par exemple, « 2014-05-23T17:53:50Z »).</span><span class="sxs-lookup"><span data-stu-id="6afe9-323">The StartTime value must be in the following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>
>
>

### <a name="creating-a-sas-url-for-downloading-content"></a><span data-ttu-id="6afe9-324">Création d’une URL SAS pour le téléchargement de contenu</span><span class="sxs-lookup"><span data-stu-id="6afe9-324">Creating a SAS URL for downloading content</span></span>
<span data-ttu-id="6afe9-325">Le code suivant montre comment obtenir une URL qui peut être utilisée pour télécharger une ressource créée et téléchargée précédemment.</span><span class="sxs-lookup"><span data-stu-id="6afe9-325">The following code shows how to get a URL that can be used to download a media file created and uploaded previously.</span></span> <span data-ttu-id="6afe9-326">AccessPolicy dispose d’autorisations en lecture et le chemin d’accès du localisateur fait référence à une URL de téléchargement SAS.</span><span class="sxs-lookup"><span data-stu-id="6afe9-326">The AccessPolicy has read permissions set and the Locator path refers to a SAS download URL.</span></span>

    POST https://wamsbayclus001rest-hs.net/API/Locators HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=zf84471d-b1ae-2233-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 182
    Expect: 100-continue

    {"AccessPolicyId": "nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8", "AssetId" : "nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c", "StartTime" : "2014-05-17T16:45:53", "Type":1}

<span data-ttu-id="6afe9-327">Si l’opération réussit, la réponse suivante est retournée :</span><span class="sxs-lookup"><span data-stu-id="6afe9-327">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1150
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 8cfd8556-3064-416a-97f2-67d9e35f0911
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Mon, 14 May 2012 21:41:32 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')",
             "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Locator"
          },
          "AccessPolicy":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')/AccessPolicy"
             }
          },
          "Asset":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/Asset"
             }
          },
          "Id":"nb:lid:UUID:8e5a821d-2194-4d00-8884-adf979856874",
          "ExpirationDateTime":"\/Date(1337049393000)\/",
          "Type":1,
          "Path":"https://storagetestaccount001.blob.core.windows.net/asset-71d2dd33-efdf-ec43-8ea1-136a110bd42c?st=2012-05-14T21%3A36%3A33Z&se=2012-05-15T02%3A36%3A33Z&sr=c&si=8e5a821d-2194-4d00-8884-adf979856874&sig=y75dViDpC5V8WutrXM%2B%2FGpR3uOtqmlISiNlHU1YUBOg%3D",
          "AccessPolicyId":"nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8",
          "AssetId":"nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
          "StartTime":"\/Date(1337031393000)\/"
       }
    }


<span data-ttu-id="6afe9-328">La propriété **Path** retournée contient l’URL SAS.</span><span class="sxs-lookup"><span data-stu-id="6afe9-328">The returned **Path** property contains the SAS URL.</span></span>

> [!NOTE]
> <span data-ttu-id="6afe9-329">Si vous téléchargez du contenu avec chiffrement de stockage, vous devez le déchiffrer manuellement avant de le restituer ou utiliser le processeur multimédia de déchiffrement de stockage dans une tâche de traitement pour obtenir une sortie de fichiers traités en clair vers un OutputAsset et le télécharger à partir de cette ressource.</span><span class="sxs-lookup"><span data-stu-id="6afe9-329">If you download storage encrypted content, you must manually decrypt it before rendering it, or use the Storage Decryption MediaProcessor in a processing task to output processed files in the clear to an OutputAsset and then download from that Asset.</span></span> <span data-ttu-id="6afe9-330">Pour plus d’informations sur le traitement, consultez la page Création d’une tâche d’encodage avec l’API REST Media Services</span><span class="sxs-lookup"><span data-stu-id="6afe9-330">For more information on processing, see Creating an Encoding Job with the Media Services REST API.</span></span> <span data-ttu-id="6afe9-331">En outre, les localisateurs d’URL SAS ne peuvent pas être mis à jour après leur création.</span><span class="sxs-lookup"><span data-stu-id="6afe9-331">Also, SAS URL Locators cannot be updated after they have been created.</span></span> <span data-ttu-id="6afe9-332">Par exemple, vous ne pouvez pas réutiliser le même localisateur avec une valeur StartTime mise à jour.</span><span class="sxs-lookup"><span data-stu-id="6afe9-332">For example, you cannot reuse the same Locator with an updated StartTime value.</span></span> <span data-ttu-id="6afe9-333">Cela est dû au mode de création des URL SAS.</span><span class="sxs-lookup"><span data-stu-id="6afe9-333">This is because of the way SAS URLs are created.</span></span> <span data-ttu-id="6afe9-334">Si vous souhaitez accéder à une ressource pour la télécharger après l’expiration d’un localisateur, vous devez en créer un nouveau, avec une nouvelle valeur StartTime.</span><span class="sxs-lookup"><span data-stu-id="6afe9-334">If you want to access an asset for download after a Locator has expired, then you must create a new one with a new StartTime.</span></span>
>
>

### <a name="download-files"></a><span data-ttu-id="6afe9-335">Téléchargement de fichiers</span><span class="sxs-lookup"><span data-stu-id="6afe9-335">Download files</span></span>
<span data-ttu-id="6afe9-336">Après avoir défini AccessPolicy et le localisateur, vous pouvez télécharger des fichiers à l’aide des API REST Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="6afe9-336">Once you have the AccessPolicy and Locator set, you can download files using the Azure Storage REST APIs.</span></span>  

> [!NOTE]
> <span data-ttu-id="6afe9-337">Vous devez ajouter le nom de fichier du fichier à télécharger à la valeur **Path** du Localisateur, obtenue dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="6afe9-337">You must add the file name for the file you want to download to the Locator **Path** value received in the previous section.</span></span> <span data-ttu-id="6afe9-338">Par exemple, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="6afe9-338">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="6afe9-339">.</span><span class="sxs-lookup"><span data-stu-id="6afe9-339">.</span></span> <span data-ttu-id="6afe9-340">.</span><span class="sxs-lookup"><span data-stu-id="6afe9-340">.</span></span> <span data-ttu-id="6afe9-341">.</span><span class="sxs-lookup"><span data-stu-id="6afe9-341">.</span></span>
>
>

<span data-ttu-id="6afe9-342">Pour plus d’informations sur l’utilisation d’objets blob de stockage Microsoft Azure, consultez [API REST du service BLOB](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="6afe9-342">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

<span data-ttu-id="6afe9-343">Suite à la tâche de codage que vous avez exécutée antérieurement (encodage vers un jeu de MP4 adaptatifs), vous disposez de plusieurs fichiers MP4 que vous pouvez télécharger progressivement.</span><span class="sxs-lookup"><span data-stu-id="6afe9-343">As a result of the encoding job that you performed earlier (encoding into Adaptive MP4 set), you have multiple MP4 files that you can progressively download.</span></span> <span data-ttu-id="6afe9-344">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="6afe9-344">For example:</span></span>    

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


### <a name="creating-a-streaming-url-for-streaming-content"></a><span data-ttu-id="6afe9-345">Création d’une URL pour la diffusion en continu de contenu</span><span class="sxs-lookup"><span data-stu-id="6afe9-345">Creating a streaming URL for streaming content</span></span>
<span data-ttu-id="6afe9-346">Le code suivant montre comment créer un localisateur d’URL de diffusion en continu  :</span><span class="sxs-lookup"><span data-stu-id="6afe9-346">The following code shows how to create a streaming URL Locator:</span></span>

    POST https://wamsbayclus001rest-hs/API/Locators HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: wamsbayclus001rest-hs
    Content-Length: 182
    Expect: 100-continue

    {"AccessPolicyId": "nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8", "AssetId" : "nb:cid:UUID:eb5540a2-116e-4d36-b084-7e9958f7f3c3", "StartTime" : "2014-05-17T16:45:53",, "Type":2}

<span data-ttu-id="6afe9-347">Si l’opération réussit, la réponse suivante est retournée :</span><span class="sxs-lookup"><span data-stu-id="6afe9-347">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 981
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 2eac4158-fc78-4fa2-81ee-c9f582dc385f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Mon, 14 May 2012 21:41:39 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')",
             "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Locator"
          },
          "AccessPolicy":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')/AccessPolicy"
             }
          },
          "Asset":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')/Asset"
             }
          },
          "Id":"nb:lid:UUID:52034bf6-dfae-4d83-aad3-3bd87dcb1a5d",
          "ExpirationDateTime":"\/Date(1337049395000)\/",
          "Type":2,
          "Path":"http://wamsbayclus001rest-hs.net/52034bf6-dfae-4d83-aad3-3bd87dcb1a5d/",
          "AccessPolicyId":"nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8",
          "AssetId":"nb:cid:UUID:eb5540a2-116e-4d36-b084-7e9958f7f3c3",
          "StartTime":"\/Date(1337031395000)\/"
       }
    }

<span data-ttu-id="6afe9-348">Pour diffuser une URL d’origine de diffusion en continu lisse dans un lecteur multimédia de diffusion en continu, vous devez ajouter la propriété de chemin d’accès avec le nom du fichier manifeste de diffusion en continu lisse, suivie de « /manifest ».</span><span class="sxs-lookup"><span data-stu-id="6afe9-348">To stream a Smooth Streaming origin URL in a streaming media player, you must append the Path property with the name of the Smooth Streaming manifest file, followed by "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

<span data-ttu-id="6afe9-349">Pour la diffusion en continu HLS, ajoutez (format=m3u8-aapl) après « /manifest ».</span><span class="sxs-lookup"><span data-stu-id="6afe9-349">To stream HLS, append (format=m3u8-aapl) after the "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

<span data-ttu-id="6afe9-350">Pour la diffusion en continu MPEG DASH, ajoutez (format=mpd-time-csf) après « /manifest ».</span><span class="sxs-lookup"><span data-stu-id="6afe9-350">To stream MPEG DASH, append (format=mpd-time-csf) after the "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)


## <span data-ttu-id="6afe9-351"><a id="play"></a>Lecture de votre contenu</span><span class="sxs-lookup"><span data-stu-id="6afe9-351"><a id="play"></a>Play your content</span></span>
<span data-ttu-id="6afe9-352">Pour tester votre vidéo, utilisez le [lecteur Azure Media Services](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="6afe9-352">To stream you video, use [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

<span data-ttu-id="6afe9-353">Pour tester le téléchargement progressif, collez l’URL dans un navigateur (par exemple, Internet Explorer, Chrome ou Safari).</span><span class="sxs-lookup"><span data-stu-id="6afe9-353">To test progressive download, paste a URL into a browser (for example, IE, Chrome, Safari).</span></span>

## <a name="next-steps-media-services-learning-paths"></a><span data-ttu-id="6afe9-354">Étapes suivantes : Parcours d’apprentissage Media Services</span><span class="sxs-lookup"><span data-stu-id="6afe9-354">Next Steps: Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="6afe9-355">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="6afe9-355">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
