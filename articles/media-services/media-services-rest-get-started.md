---
title: "aaaGet en main de diffusion de contenu sur demande à l’aide de REST | Documents Microsoft"
description: "Ce didacticiel vous guide tout au long des étapes hello d’implémentation d’une application de diffusion de contenu sur la demande avec Azure Media Services à l’aide des API REST."
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
ms.openlocfilehash: f270ed59e9ae9745e8403ec6e19d5c3533fc82b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-rest"></a><span data-ttu-id="b1583-103">Prendre en main la diffusion de contenus à la demande avec REST</span><span class="sxs-lookup"><span data-stu-id="b1583-103">Get started with delivering content on demand using REST</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="b1583-104">Ce démarrage rapide vous guide tout au long des étapes hello d’implémentation d’une application de diffusion de contenu vidéo à la demande (VoD) à l’aide des API REST de Azure Media Services (AMS).</span><span class="sxs-lookup"><span data-stu-id="b1583-104">This quickstart walks you through hello steps of implementing a Video-on-Demand (VoD) content delivery application using Azure Media Services (AMS) REST APIs.</span></span>

<span data-ttu-id="b1583-105">didacticiel de Hello présente des flux de travail Media Services hello et objets de programmation courants hello et tâches requises pour le développement de Media Services.</span><span class="sxs-lookup"><span data-stu-id="b1583-105">hello tutorial introduces hello basic Media Services workflow and hello most common programming objects and tasks required for Media Services development.</span></span> <span data-ttu-id="b1583-106">À l’achèvement de hello du didacticiel de hello, vous être en mesure de toostream ou télécharger progressivement un exemple de fichier de média que vous avez téléchargé, encodé, téléchargé.</span><span class="sxs-lookup"><span data-stu-id="b1583-106">At hello completion of hello tutorial, you will be able toostream or progressively download a sample media file that you uploaded, encoded, and downloaded.</span></span>

<span data-ttu-id="b1583-107">Hello image suivante montre certains des objets de hello couramment utilisé lors du développement d’applications VoD sur le modèle de Media Services OData hello.</span><span class="sxs-lookup"><span data-stu-id="b1583-107">hello following image shows some of hello most commonly used objects when developing VoD applications against hello Media Services OData model.</span></span>

<span data-ttu-id="b1583-108">Cliquez sur tooview d’image hello il plein écran.</span><span class="sxs-lookup"><span data-stu-id="b1583-108">Click hello image tooview it full size.</span></span>  

<a href="./media/media-services-rest-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-rest-get-started/media-services-overview-object-model-small.png"></a> 

## <a name="prerequisites"></a><span data-ttu-id="b1583-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b1583-109">Prerequisites</span></span>
<span data-ttu-id="b1583-110">Hello conditions préalables suivantes sont requise toostart développement avec Media Services avec l’API REST.</span><span class="sxs-lookup"><span data-stu-id="b1583-110">hello following prerequisites are required toostart developing with Media Services with REST APIs.</span></span>

* <span data-ttu-id="b1583-111">Un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="b1583-111">An Azure account.</span></span> <span data-ttu-id="b1583-112">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b1583-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="b1583-113">Un compte Media Services.</span><span class="sxs-lookup"><span data-stu-id="b1583-113">A Media Services account.</span></span> <span data-ttu-id="b1583-114">toocreate un compte Media Services, consultez [comment tooCreate un compte Media Services](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="b1583-114">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="b1583-115">Comprendre comment toodevelop avec l’API REST Media Services.</span><span class="sxs-lookup"><span data-stu-id="b1583-115">Understanding of how toodevelop with Media Services REST API.</span></span> <span data-ttu-id="b1583-116">Pour plus d’informations, consultez [Vue d’ensemble de l’API REST Media Services](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="b1583-116">For more information, see [Media Services REST API overview](media-services-rest-how-to-use.md).</span></span>
* <span data-ttu-id="b1583-117">Une application de votre choix qui peut envoyer des demandes et réponses HTTP.</span><span class="sxs-lookup"><span data-stu-id="b1583-117">An application of your choice that can send HTTP requests and responses.</span></span> <span data-ttu-id="b1583-118">Ce didacticiel utilise [Fiddler](http://www.telerik.com/download/fiddler).</span><span class="sxs-lookup"><span data-stu-id="b1583-118">This tutorial uses [Fiddler](http://www.telerik.com/download/fiddler).</span></span>

<span data-ttu-id="b1583-119">Bonjour tâches suivantes est affiché dans ce démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="b1583-119">hello following tasks are shown in this quickstart.</span></span>

1. <span data-ttu-id="b1583-120">Début de la diffusion en continu de point de terminaison (à l’aide de hello portail Azure).</span><span class="sxs-lookup"><span data-stu-id="b1583-120">Start streaming endpoint (using hello Azure portal).</span></span>
2. <span data-ttu-id="b1583-121">Connecter le compte de service de média toohello avec l’API REST.</span><span class="sxs-lookup"><span data-stu-id="b1583-121">Connect toohello Media Services account with REST API.</span></span>
3. <span data-ttu-id="b1583-122">Création d’une ressource et téléchargement d’un fichier vidéo à l’aide de l’API REST</span><span class="sxs-lookup"><span data-stu-id="b1583-122">Create a new asset and upload a video file with REST API.</span></span>
4. <span data-ttu-id="b1583-123">Encoder le fichier de source de hello en un ensemble de fichiers MP4 à débit adaptatif avec l’API REST.</span><span class="sxs-lookup"><span data-stu-id="b1583-123">Encode hello source file into a set of adaptive bitrate MP4 files with REST API.</span></span>
5. <span data-ttu-id="b1583-124">Publier les actifs hello et get de diffusion en continu et URL de téléchargement progressif avec l’API REST.</span><span class="sxs-lookup"><span data-stu-id="b1583-124">Publish hello asset and get streaming and progressive download URLs with REST API.</span></span>
6. <span data-ttu-id="b1583-125">Lire votre contenu.</span><span class="sxs-lookup"><span data-stu-id="b1583-125">Play your content.</span></span>

>[!NOTE]
><span data-ttu-id="b1583-126">Un nombre limite de 1 000 000 a été défini pour les différentes stratégies AMS (par exemple, pour la stratégie de localisateur ou pour ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="b1583-126">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="b1583-127">Vous devez utiliser hello ID de stratégie même si vous utilisez toujours hello même jours / autorisations d’accès, par exemple, les stratégies pour les localisateurs sont tooremain prévue en place pendant une longue période (non-téléchargement stratégies).</span><span class="sxs-lookup"><span data-stu-id="b1583-127">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="b1583-128">Pour plus d’informations, consultez [cette rubrique](media-services-dotnet-manage-entities.md#limit-access-policies) .</span><span class="sxs-lookup"><span data-stu-id="b1583-128">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="b1583-129">Pour plus d’informations sur les entités REST AMS utilisées dans cette rubrique, consultez [Informations de référence sur l’API REST de Media Services](/rest/api/media/services/azure-media-services-rest-api-reference).</span><span class="sxs-lookup"><span data-stu-id="b1583-129">For details about AMS REST entities used in this topic, see [Azure Media Services REST API Reference](/rest/api/media/services/azure-media-services-rest-api-reference).</span></span> <span data-ttu-id="b1583-130">Consultez également [Concepts Azure Media Services](media-services-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="b1583-130">Also, see [Azure Media Services concepts](media-services-concepts.md).</span></span>

>[!NOTE]
><span data-ttu-id="b1583-131">Lors de l’accès aux entités dans Media Services, vous devez définir les valeurs et les champs d’en-tête spécifiques dans vos requêtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="b1583-131">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="b1583-132">Pour plus d'informations, consultez [Installation pour le développement REST API de Media Services](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="b1583-132">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="start-streaming-endpoints-using-hello-azure-portal"></a><span data-ttu-id="b1583-133">Démarrer la diffusion en continu des points de terminaison à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="b1583-133">Start streaming endpoints using hello Azure portal</span></span>

<span data-ttu-id="b1583-134">Lorsque vous travaillez avec un des scénarios les plus courants de hello est diffusion vidéo via à débit adaptatif de diffusion en continu Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="b1583-134">When working with Azure Media Services one of hello most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="b1583-135">Media Services propose un empaquetage dynamique, ce qui vous permet de toodeliver votre vitesse de transmission adaptative MP4 encodés le contenu de diffusion en continu des formats pris en charge par Media Services (MPEG DASH, HLS, Smooth Streaming) juste-à-temps, sans que vous ayez toostore préconçue versions de chacune de ces formats de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="b1583-135">Media Services provides dynamic packaging, which allows you toodeliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having toostore pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="b1583-136">Création de votre compte AMS un **par défaut** point de terminaison de diffusion en continu est ajoutée tooyour compte Bonjour **arrêté** état.</span><span class="sxs-lookup"><span data-stu-id="b1583-136">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="b1583-137">toostart de diffusion en continu de votre contenu et profitez de l’empaquetage dynamique et chiffrement dynamique, hello de point de terminaison de diffusion en continu à partir de laquelle vous souhaitez que le contenu toostream a toobe Bonjour **en cours d’exécution** état.</span><span class="sxs-lookup"><span data-stu-id="b1583-137">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span>

<span data-ttu-id="b1583-138">toostart hello du point de terminaison de diffusion en continu, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="b1583-138">toostart hello streaming endpoint, do hello following:</span></span>

1. <span data-ttu-id="b1583-139">Connectez-vous à l’adresse hello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b1583-139">Log in at hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="b1583-140">Dans la fenêtre des paramètres hello, cliquez sur les points de terminaison de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="b1583-140">In hello Settings window, click Streaming endpoints.</span></span>
3. <span data-ttu-id="b1583-141">Cliquez sur le point de terminaison de diffusion en continu de la valeur par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="b1583-141">Click hello default streaming endpoint.</span></span>

    <span data-ttu-id="b1583-142">fenêtre de détails par défaut du point de terminaison de diffusion en continu Hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="b1583-142">hello DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="b1583-143">Cliquez sur l’icône Démarrer hello.</span><span class="sxs-lookup"><span data-stu-id="b1583-143">Click hello Start icon.</span></span>
5. <span data-ttu-id="b1583-144">Cliquez sur toosave de bouton hello enregistrer vos modifications.</span><span class="sxs-lookup"><span data-stu-id="b1583-144">Click hello Save button toosave your changes.</span></span>

## <span data-ttu-id="b1583-145"><a id="connect"></a>Connexion de compte de service de média toohello avec l’API REST</span><span class="sxs-lookup"><span data-stu-id="b1583-145"><a id="connect"></a>Connect toohello Media Services account with REST API</span></span>

<span data-ttu-id="b1583-146">Pour plus d’informations sur la façon dont tooconnect toohello AMS API, consultez [hello accès API Azure Media Services avec l’authentification Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="b1583-146">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="b1583-147">Après vous être connecté toohttps://media.windows.net, vous recevrez une redirection 301 spécifiant un autre URI de Media Services.</span><span class="sxs-lookup"><span data-stu-id="b1583-147">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="b1583-148">Vous devez effectuer les appels suivants toohello nouvel URI.</span><span class="sxs-lookup"><span data-stu-id="b1583-148">You must make subsequent calls toohello new URI.</span></span>

<span data-ttu-id="b1583-149">Par exemple, si, après la tentative de tooconnect, que vous avez obtenu suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="b1583-149">For example, if after trying tooconnect, you got hello following:</span></span>

    HTTP/1.1 301 Moved Permanently
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/

<span data-ttu-id="b1583-150">Vous devez enregistrer votre ultérieures API appels toohttps://wamsbayclus001rest-hs.cloudapp.net/api/.</span><span class="sxs-lookup"><span data-stu-id="b1583-150">You should post your subsequent API calls toohttps://wamsbayclus001rest-hs.cloudapp.net/api/.</span></span>

## <span data-ttu-id="b1583-151"><a id="upload"></a>Création d’une ressource et téléchargement d’un fichier vidéo à l’aide de l’API REST</span><span class="sxs-lookup"><span data-stu-id="b1583-151"><a id="upload"></a>Create a new asset and upload a video file with REST API</span></span>

<span data-ttu-id="b1583-152">Dans Media Services, vous téléchargez vos fichiers numériques dans une ressource.</span><span class="sxs-lookup"><span data-stu-id="b1583-152">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="b1583-153">Hello **Asset** entité peut contenir vidéo, audio, images, collections de miniatures, texte assure le suivi et sous-titres fichiers (et les métadonnées hello sur ces fichiers.)  Une fois que les fichiers de hello sont téléchargés en ressource de hello, votre contenu est stocké en toute sécurité dans le cloud hello pour le traitement et la diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="b1583-153">hello **Asset** entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.)  Once hello files are uploaded into hello asset, your content is stored securely in hello cloud for further processing and streaming.</span></span>

<span data-ttu-id="b1583-154">Une des valeurs hello que vous avez tooprovide lors de la création d’un élément multimédia est options de création d’élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="b1583-154">One of hello values that you have tooprovide when creating an asset is asset creation options.</span></span> <span data-ttu-id="b1583-155">Hello **Options** propriété est une valeur d’énumération qui décrit les options de chiffrement hello un élément multimédia peut être créé avec.</span><span class="sxs-lookup"><span data-stu-id="b1583-155">hello **Options** property is an enumeration value that describes hello encryption options that an Asset can be created with.</span></span> <span data-ttu-id="b1583-156">Une valeur valide est une des valeurs hello dans liste hello ci-dessous, pas une combinaison de valeurs à partir de cette liste :</span><span class="sxs-lookup"><span data-stu-id="b1583-156">A valid value is one of hello values from hello list below, not a combination of values from this list:</span></span>

* <span data-ttu-id="b1583-157">**None** = **0** : aucun chiffrement.</span><span class="sxs-lookup"><span data-stu-id="b1583-157">**None** = **0** - No encryption is used.</span></span> <span data-ttu-id="b1583-158">Quand vous utilisez cette option, votre contenu n'est pas protégé pendant le transit ou le repos dans le stockage.</span><span class="sxs-lookup"><span data-stu-id="b1583-158">When using this option your content is not protected in transit or at rest in storage.</span></span>
    <span data-ttu-id="b1583-159">Si vous envisagez de toodeliver un fichier MP4 à l’aide d’un téléchargement progressif, utilisez cette option.</span><span class="sxs-lookup"><span data-stu-id="b1583-159">If you plan toodeliver an MP4 using progressive download, use this option.</span></span>
* <span data-ttu-id="b1583-160">**StorageEncrypted** = **1** - chiffre votre contenu en clair localement à l’aide du chiffrement AES-256 bits, puis le télécharge tooAzure Storage où il est stocké et chiffré au repos.</span><span class="sxs-lookup"><span data-stu-id="b1583-160">**StorageEncrypted** = **1** - Encrypts your clear content locally using AES-256 bit encryption and then uploads it tooAzure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="b1583-161">Les éléments multimédias protégés par chiffrement de stockage sont automatiquement déchiffrés et placés dans un tooencoding préalable de système de fichiers chiffrés et éventuellement RE-chiffrée toouploading préalable comme un nouvel élément multimédia de sortie.</span><span class="sxs-lookup"><span data-stu-id="b1583-161">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior tooencoding, and optionally re-encrypted prior toouploading back as a new output asset.</span></span> <span data-ttu-id="b1583-162">Hello est principalement utilisé pour le chiffrement de stockage lorsque vous souhaitez toosecure vos fichiers multimédias d’entrée de haute qualité avec un chiffrement renforcé au repos sur le disque.</span><span class="sxs-lookup"><span data-stu-id="b1583-162">hello primary use case for Storage Encryption is when you want toosecure your high-quality input media files with strong encryption at rest on disk.</span></span>
* <span data-ttu-id="b1583-163">**CommonEncryptionProtected** = **2** : utilisez cette option quand vous chargez du contenu qui a déjà été chiffré et protégé avec la DRM Common Encryption ou PlayReady (par exemple Smooth Streaming protégé avec la DRM PlayReady).</span><span class="sxs-lookup"><span data-stu-id="b1583-163">**CommonEncryptionProtected** = **2** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="b1583-164">**EnvelopeEncryptionProtected** = **4** : utilisez cette option lorsque vous téléchargez un contenu au format TLS chiffré avec AES.</span><span class="sxs-lookup"><span data-stu-id="b1583-164">**EnvelopeEncryptionProtected** = **4** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="b1583-165">les fichiers Hello doivent encodés et chiffrés par Transform Manager.</span><span class="sxs-lookup"><span data-stu-id="b1583-165">hello files must have been encoded and encrypted by Transform Manager.</span></span>

### <a name="create-an-asset"></a><span data-ttu-id="b1583-166">Créer une ressource</span><span class="sxs-lookup"><span data-stu-id="b1583-166">Create an asset</span></span>
<span data-ttu-id="b1583-167">Une ressource est un conteneur pour plusieurs types ou ensembles d’objets dans Media Services, y compris des fichiers vidéo, audio, des images, des collections de miniatures, des pistes textuelles et des légendes.</span><span class="sxs-lookup"><span data-stu-id="b1583-167">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="b1583-168">Bonjour API REST, création d’un élément multimédia requiert l’envoi de POST solliciter des Services de tooMedia et placer toutes les informations de propriété concernant votre élément multimédia dans le corps de la demande hello.</span><span class="sxs-lookup"><span data-stu-id="b1583-168">In hello REST API, creating an Asset requires sending POST request tooMedia Services and placing any property information about your asset in hello request body.</span></span>

<span data-ttu-id="b1583-169">Hello suivant montre l’exemple de comment toocreate un élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="b1583-169">hello following example shows how toocreate an asset.</span></span>

<span data-ttu-id="b1583-170">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="b1583-170">**HTTP Request**</span></span>

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


<span data-ttu-id="b1583-171">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="b1583-171">**HTTP Response**</span></span>

<span data-ttu-id="b1583-172">En cas de réussite, suivant de hello est retournée :</span><span class="sxs-lookup"><span data-stu-id="b1583-172">If successful, hello following is returned:</span></span>

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

### <a name="create-an-assetfile"></a><span data-ttu-id="b1583-173">Création d’un AssetFile</span><span class="sxs-lookup"><span data-stu-id="b1583-173">Create an AssetFile</span></span>
<span data-ttu-id="b1583-174">Hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entité représente un fichier vidéo ou audio qui est stocké dans un conteneur d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="b1583-174">hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="b1583-175">Un fichier de ressources est toujours associé à une ressource et une ressource peut contenir un ou plusieurs AssetFiles.</span><span class="sxs-lookup"><span data-stu-id="b1583-175">An asset file is always associated with an asset, and an asset may contain one or many AssetFiles.</span></span> <span data-ttu-id="b1583-176">tâche d’encodeur Media Services Hello échoue si un objet de fichier actif n’est pas associé à un fichier numérique dans un conteneur d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="b1583-176">hello Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="b1583-177">Après avoir téléchargé votre fichier multimédia numérique sur un conteneur d’objets blob, vous utilisez hello **fusion** tooupdate hello AssetFile HTTP demande des informations sur votre fichier multimédia (comme indiqué plus loin dans la rubrique de hello).</span><span class="sxs-lookup"><span data-stu-id="b1583-177">After you upload your digital media file into a blob container, you use hello **MERGE** HTTP request tooupdate hello AssetFile with information about your media file (as shown later in hello topic).</span></span>

<span data-ttu-id="b1583-178">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="b1583-178">**HTTP Request**</span></span>

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


<span data-ttu-id="b1583-179">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="b1583-179">**HTTP Response**</span></span>

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


### <a name="creating-hello-accesspolicy-with-write-permission"></a><span data-ttu-id="b1583-180">Création de hello AccessPolicy avec autorisation d’écriture</span><span class="sxs-lookup"><span data-stu-id="b1583-180">Creating hello AccessPolicy with write permission</span></span>
<span data-ttu-id="b1583-181">Avant de télécharger des fichiers dans le stockage d’objets blob, définissez l’accès de hello droits de stratégie pour l’écriture de tooan actif.</span><span class="sxs-lookup"><span data-stu-id="b1583-181">Before uploading any files into blob storage, set hello access policy rights for writing tooan asset.</span></span> <span data-ttu-id="b1583-182">toodo que, VALIDEZ un toohello de demande HTTP entité de stratégies d’accès défini.</span><span class="sxs-lookup"><span data-stu-id="b1583-182">toodo that, POST an HTTP request toohello AccessPolicies entity set.</span></span> <span data-ttu-id="b1583-183">N’oubliez pas de définir une valeur DurationInMinutes après la création ou vous recevrez en réponse un message d’erreur interne de serveur 500.</span><span class="sxs-lookup"><span data-stu-id="b1583-183">Define a DurationInMinutes value upon creation or you receive a 500 Internal Server error message back in response.</span></span> <span data-ttu-id="b1583-184">Pour plus d’informations sur AccessPolicies, consultez [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span><span class="sxs-lookup"><span data-stu-id="b1583-184">For more information on AccessPolicies, see [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span></span>

<span data-ttu-id="b1583-185">Hello suivant montre l’exemple de comment toocreate une stratégie d’accès :</span><span class="sxs-lookup"><span data-stu-id="b1583-185">hello following example shows how toocreate an AccessPolicy:</span></span>

<span data-ttu-id="b1583-186">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="b1583-186">**HTTP Request**</span></span>

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

<span data-ttu-id="b1583-187">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="b1583-187">**HTTP Response**</span></span>

<span data-ttu-id="b1583-188">En cas de réussite, hello suivant la réponse est retournée :</span><span class="sxs-lookup"><span data-stu-id="b1583-188">If successful, hello following response is returned:</span></span>

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

### <a name="get-hello-upload-url"></a><span data-ttu-id="b1583-189">Obtenir hello télécharger l’URL</span><span class="sxs-lookup"><span data-stu-id="b1583-189">Get hello Upload URL</span></span>

<span data-ttu-id="b1583-190">tooreceive hello URL de téléchargement réelle, créer un localisateur SAS.</span><span class="sxs-lookup"><span data-stu-id="b1583-190">tooreceive hello actual upload URL, create a SAS Locator.</span></span> <span data-ttu-id="b1583-191">Les localisateurs définissent l’heure de début de hello et le type du point de terminaison de connexion pour les clients qui tooaccess des fichiers dans un élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="b1583-191">Locators define hello start time and type of connection endpoint for clients that want tooaccess Files in an Asset.</span></span> <span data-ttu-id="b1583-192">Vous pouvez créer plusieurs entités Locator pour une donnée AccessPolicy et Asset paire toohandle client différents besoins et demandes.</span><span class="sxs-lookup"><span data-stu-id="b1583-192">You can create multiple Locator entities for a given AccessPolicy and Asset pair toohandle different client requests and needs.</span></span> <span data-ttu-id="b1583-193">Chacun de ces localisateurs utilise la valeur de StartTime hello plus la valeur DurationInMinutes hello hello AccessPolicy toodetermine hello durée qu'une URL peut être utilisée.</span><span class="sxs-lookup"><span data-stu-id="b1583-193">Each of these Locators uses hello StartTime value plus hello DurationInMinutes value of hello AccessPolicy toodetermine hello length of time a URL can be used.</span></span> <span data-ttu-id="b1583-194">Pour plus d’informations, consultez la rubrique [Localisateur](https://docs.microsoft.com/rest/api/media/operations/locator).</span><span class="sxs-lookup"><span data-stu-id="b1583-194">For more information, see [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>

<span data-ttu-id="b1583-195">Une URL SAS a hello suivant le format :</span><span class="sxs-lookup"><span data-stu-id="b1583-195">A SAS URL has hello following format:</span></span>

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

<span data-ttu-id="b1583-196">Certaines considérations s’appliquent :</span><span class="sxs-lookup"><span data-stu-id="b1583-196">Some considerations apply:</span></span>

* <span data-ttu-id="b1583-197">Vous ne pouvez avoir plus de cinq localisateurs uniques associés à une ressource donnée.</span><span class="sxs-lookup"><span data-stu-id="b1583-197">You cannot have more than five unique Locators associated with a given Asset at one time.</span></span> <span data-ttu-id="b1583-198">Pour plus d’informations, consultez la rubrique Localisateur.</span><span class="sxs-lookup"><span data-stu-id="b1583-198">For more information, see Locator.</span></span>
* <span data-ttu-id="b1583-199">Si vous avez besoin de tooupload vos fichiers immédiatement, vous devez définir les minutes de toofive valeur StartTime avant hello heure actuelle.</span><span class="sxs-lookup"><span data-stu-id="b1583-199">If you need tooupload your files immediately, you should set your StartTime value toofive minutes before hello current time.</span></span> <span data-ttu-id="b1583-200">Cela vient du fait qu’il peut exister un décalage horaire entre votre ordinateur client et Media Services.</span><span class="sxs-lookup"><span data-stu-id="b1583-200">This is because there may be clock skew between your client machine and Media Services.</span></span> <span data-ttu-id="b1583-201">En outre, votre valeur StartTime doit être hello respectant le format de date/heure : AAAA-MM-JJThh (par exemple, « 2014-05-23T17:53:50Z »).</span><span class="sxs-lookup"><span data-stu-id="b1583-201">Also, your StartTime value must be in hello following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>    
* <span data-ttu-id="b1583-202">Il peut y avoir un 30 à 40 secondes après la création d’un localisateur toowhen, il est disponible pour une utilisation de retarder.</span><span class="sxs-lookup"><span data-stu-id="b1583-202">There may be a 30-40 second delay after a Locator is created toowhen it is available for use.</span></span> <span data-ttu-id="b1583-203">Ce problème s’applique tooboth URL SAS et les localisateurs d’origine.</span><span class="sxs-lookup"><span data-stu-id="b1583-203">This issue applies tooboth SAS URL and Origin Locators.</span></span>

<span data-ttu-id="b1583-204">Pour plus d’informations sur les localisateurs de SAP, consultez [ce](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span><span class="sxs-lookup"><span data-stu-id="b1583-204">For more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span></span>

<span data-ttu-id="b1583-205">Bonjour à l’exemple suivant montre comment toocreate un localisateur d’URL SAS, tel que défini par hello la propriété de Type dans le corps de la demande hello (« 1 » pour un localisateur SAS) et « 2 » pour un localisateur d’origine à la demande.</span><span class="sxs-lookup"><span data-stu-id="b1583-205">hello following example shows how toocreate a SAS URL Locator, as defined by hello Type property in hello request body ("1" for a SAS locator and "2" for an On-Demand origin locator).</span></span> <span data-ttu-id="b1583-206">Hello **chemin d’accès** propriété retournée contient les URL de hello que vous devez utiliser tooupload votre fichier.</span><span class="sxs-lookup"><span data-stu-id="b1583-206">hello **Path** property returned contains hello URL that you must use tooupload your file.</span></span>

<span data-ttu-id="b1583-207">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="b1583-207">**HTTP Request**</span></span>

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


<span data-ttu-id="b1583-208">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="b1583-208">**HTTP Response**</span></span>

<span data-ttu-id="b1583-209">En cas de réussite, hello suivant la réponse est retournée :</span><span class="sxs-lookup"><span data-stu-id="b1583-209">If successful, hello following response is returned:</span></span>

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

### <a name="upload-a-file-into-a-blob-storage-container"></a><span data-ttu-id="b1583-210">Téléchargement d’un fichier dans un conteneur de stockage d’objets blob</span><span class="sxs-lookup"><span data-stu-id="b1583-210">Upload a file into a blob storage container</span></span>
<span data-ttu-id="b1583-211">Une fois que vous avez hello AccessPolicy et l’ensemble de la recherche, le fichier hello est conteneur de stockage d’objets blob Azure tooan téléchargé à l’aide de hello API REST de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="b1583-211">Once you have hello AccessPolicy and Locator set, hello actual file is uploaded tooan Azure blob storage container using hello Azure Storage REST APIs.</span></span> <span data-ttu-id="b1583-212">Vous devez télécharger les fichiers hello en tant qu’objets BLOB de blocs.</span><span class="sxs-lookup"><span data-stu-id="b1583-212">You must upload hello files as block blobs.</span></span> <span data-ttu-id="b1583-213">Les objets blob de pages ne sont pas pris en charge par Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="b1583-213">Page blobs are not supported by Azure Media Services.</span></span>  

> [!NOTE]
> <span data-ttu-id="b1583-214">Vous devez ajouter le nom de fichier hello pour le fichier de hello souhaité tooupload toohello recherche **chemin d’accès** valeur reçue dans la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="b1583-214">You must add hello file name for hello file you want tooupload toohello Locator **Path** value received in hello previous section.</span></span> <span data-ttu-id="b1583-215">Par exemple, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="b1583-215">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="b1583-216">.</span><span class="sxs-lookup"><span data-stu-id="b1583-216">.</span></span> <span data-ttu-id="b1583-217">.</span><span class="sxs-lookup"><span data-stu-id="b1583-217">.</span></span> <span data-ttu-id="b1583-218">.</span><span class="sxs-lookup"><span data-stu-id="b1583-218">.</span></span>
>
>

<span data-ttu-id="b1583-219">Pour plus d’informations sur l’utilisation d’objets blob de stockage Microsoft Azure, consultez [API REST du service BLOB](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="b1583-219">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

### <a name="update-hello-assetfile"></a><span data-ttu-id="b1583-220">Mettre à jour hello AssetFile</span><span class="sxs-lookup"><span data-stu-id="b1583-220">Update hello AssetFile</span></span>
<span data-ttu-id="b1583-221">Maintenant que vous avez téléchargé votre fichier, mettre à jour des informations hello FileAsset taille (et autres).</span><span class="sxs-lookup"><span data-stu-id="b1583-221">Now that you've uploaded your file, update hello FileAsset size (and other) information.</span></span> <span data-ttu-id="b1583-222">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="b1583-222">For example:</span></span>

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


<span data-ttu-id="b1583-223">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="b1583-223">**HTTP Response**</span></span>

<span data-ttu-id="b1583-224">En cas de réussite, suivant de hello est retournée :</span><span class="sxs-lookup"><span data-stu-id="b1583-224">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

## <a name="delete-hello-locator-and-accesspolicy"></a><span data-ttu-id="b1583-225">Supprimer hello recherche et la stratégie d’accès</span><span class="sxs-lookup"><span data-stu-id="b1583-225">Delete hello Locator and AccessPolicy</span></span>
<span data-ttu-id="b1583-226">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="b1583-226">**HTTP Request**</span></span>

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="b1583-227">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="b1583-227">**HTTP Response**</span></span>

<span data-ttu-id="b1583-228">En cas de réussite, suivant de hello est retournée :</span><span class="sxs-lookup"><span data-stu-id="b1583-228">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

<span data-ttu-id="b1583-229">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="b1583-229">**HTTP Request**</span></span>

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net

<span data-ttu-id="b1583-230">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="b1583-230">**HTTP Response**</span></span>

<span data-ttu-id="b1583-231">En cas de réussite, suivant de hello est retournée :</span><span class="sxs-lookup"><span data-stu-id="b1583-231">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

## <span data-ttu-id="b1583-232"><a id="encode"></a>Encoder le fichier de source de hello en un ensemble de fichiers MP4 à débit adaptatif</span><span class="sxs-lookup"><span data-stu-id="b1583-232"><a id="encode"></a>Encode hello source file into a set of adaptive bitrate MP4 files</span></span>

<span data-ttu-id="b1583-233">Après réception d’éléments que multimédias dans Media Services, support peuvent être encodés, transmuxed, filigrane et ainsi de suite, avant qu’il est remis tooclients.</span><span class="sxs-lookup"><span data-stu-id="b1583-233">After ingesting Assets into Media Services, media can be encoded, transmuxed, watermarked, and so on, before it is delivered tooclients.</span></span> <span data-ttu-id="b1583-234">Ces activités sont planifiées et exécutées sur plusieurs arrière-plan rôle instances tooensure performances et la disponibilité.</span><span class="sxs-lookup"><span data-stu-id="b1583-234">These activities are scheduled and run against multiple background role instances tooensure high performance and availability.</span></span> <span data-ttu-id="b1583-235">Ces activités sont appellent des travaux et chaque tâche se compose de tâches atomiques qui hello travail réel dans le fichier d’élément multimédia hello (pour plus d’informations, consultez [travail](/rest/api/media/services/job), [tâche](/rest/api/media/services/task) descriptions).</span><span class="sxs-lookup"><span data-stu-id="b1583-235">These activities are called Jobs and each Job is composed of atomic Tasks that do hello actual work on hello Asset file (for more information, see [Job](/rest/api/media/services/job), [Task](/rest/api/media/services/task) descriptions).</span></span>

<span data-ttu-id="b1583-236">Comme indiqué précédemment, lorsque le travail avec Azure Media Services, un des scénarios les plus courants de hello est remise à débit adaptatif tooyour clients de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="b1583-236">As was mentioned earlier, when working with Azure Media Services one of hello most common scenarios is delivering adaptive bitrate streaming tooyour clients.</span></span> <span data-ttu-id="b1583-237">Media Services peut package dynamiquement un ensemble de fichiers MP4 à débit adaptatif dans une des hello suivant formats : HTTP Live Streaming (HLS), la diffusion en continu lisse, MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="b1583-237">Media Services can dynamically package a set of adaptive bitrate MP4 files into one of hello following formats: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span>

<span data-ttu-id="b1583-238">Hello après section montre comment toocreate tâches un travail qui contient un encodage.</span><span class="sxs-lookup"><span data-stu-id="b1583-238">hello following section shows how toocreate a job that contains one encoding task.</span></span> <span data-ttu-id="b1583-239">Hello tâche spécifie le fichier mezzanine de hello tootranscode dans un ensemble de l’utilisation de fichiers à débit adaptatif MP4s **Media Encoder Standard**.</span><span class="sxs-lookup"><span data-stu-id="b1583-239">hello task specifies tootranscode hello mezzanine file into a set of adaptive bitrate MP4s using **Media Encoder Standard**.</span></span> <span data-ttu-id="b1583-240">section de Hello montre également comment toomonitor hello la progression du traitement du travail.</span><span class="sxs-lookup"><span data-stu-id="b1583-240">hello section also shows how toomonitor hello job processing progress.</span></span> <span data-ttu-id="b1583-241">Lors de la tâche de hello est terminée, vous serez toocreate en mesure de localisateurs qui sont nécessaires tooget accès tooyour actifs.</span><span class="sxs-lookup"><span data-stu-id="b1583-241">When hello job is complete, you would be able toocreate locators that are needed tooget access tooyour assets.</span></span>

### <a name="get-a-media-processor"></a><span data-ttu-id="b1583-242">Obtention d’un processeur multimédia</span><span class="sxs-lookup"><span data-stu-id="b1583-242">Get a media processor</span></span>
<span data-ttu-id="b1583-243">Dans Media Services, un processeur multimédia est un composant qui gère une tâche de traitement spécifique, telle que l’encodage, la conversion de format, le chiffrement ou le déchiffrement de contenu multimédia.</span><span class="sxs-lookup"><span data-stu-id="b1583-243">In Media Services, a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="b1583-244">Hello encodage tâche que celle indiquée dans ce didacticiel, nous allons hello toouse Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="b1583-244">For hello encoding task shown in this tutorial, we are going toouse hello Media Encoder Standard.</span></span>

<span data-ttu-id="b1583-245">Hello id de l’encodeur hello code demandes suivant.</span><span class="sxs-lookup"><span data-stu-id="b1583-245">hello following code requests hello encoder's id.</span></span>

<span data-ttu-id="b1583-246">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="b1583-246">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=f7f09258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="b1583-247">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="b1583-247">**HTTP Response**</span></span>

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

### <a name="create-a-job"></a><span data-ttu-id="b1583-248">Création d’un travail</span><span class="sxs-lookup"><span data-stu-id="b1583-248">Create a job</span></span>
<span data-ttu-id="b1583-249">Chaque tâche peut avoir l’une ou plusieurs tâches en fonction de type hello de traitement que vous souhaitez tooaccomplish.</span><span class="sxs-lookup"><span data-stu-id="b1583-249">Each Job can have one or more Tasks depending on hello type of processing that you want tooaccomplish.</span></span> <span data-ttu-id="b1583-250">Via l’API REST de hello, vous pouvez créer des tâches et leurs tâches connexes de deux manières : tâches peuvent être définies inline via la propriété de navigation hello tâches sur des entités Job ou via le traitement par lots OData.</span><span class="sxs-lookup"><span data-stu-id="b1583-250">Through hello REST API, you can create Jobs and their related Tasks in one of two ways: Tasks can be defined inline through hello Tasks navigation property on Job entities, or through OData batch processing.</span></span> <span data-ttu-id="b1583-251">Hello SDK Media Services utilise le traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="b1583-251">hello Media Services SDK uses batch processing.</span></span> <span data-ttu-id="b1583-252">Toutefois, pour une meilleure lisibilité de hello hello des exemples de code dans cette rubrique, les tâches sont définies inline.</span><span class="sxs-lookup"><span data-stu-id="b1583-252">However, for hello readability of hello code examples in this topic, tasks are defined inline.</span></span> <span data-ttu-id="b1583-253">Pour plus d’informations sur le traitement par lots, consultez [Traitement par lots d’Open Data Protocol (OData)](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span><span class="sxs-lookup"><span data-stu-id="b1583-253">For information on batch processing, see [Open Data Protocol (OData) Batch Processing](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span></span>

<span data-ttu-id="b1583-254">Hello l’exemple suivant vous montre toocreate et valider un travail avec une seule tâche définition tooencode une vidéo à une résolution spécifique et la qualité.</span><span class="sxs-lookup"><span data-stu-id="b1583-254">hello following example shows you how toocreate and post a Job with one Task set tooencode a video at a specific resolution and quality.</span></span> <span data-ttu-id="b1583-255">Hello suivant la section de la documentation contient la liste hello Hello tous les [Présélections de tâches](http://msdn.microsoft.com/library/mt269960) pris en charge par le processeur hello Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="b1583-255">hello following documentation section contains hello list of all hello [task presets](http://msdn.microsoft.com/library/mt269960) supported by hello Media Encoder Standard processor.</span></span>  

<span data-ttu-id="b1583-256">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="b1583-256">**HTTP Request**</span></span>

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

<span data-ttu-id="b1583-257">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="b1583-257">**HTTP Response**</span></span>

<span data-ttu-id="b1583-258">En cas de réussite, hello suivant la réponse est retournée :</span><span class="sxs-lookup"><span data-stu-id="b1583-258">If successful, hello following response is returned:</span></span>

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


<span data-ttu-id="b1583-259">Il existe quelques points importants toonote dans toute demande de travail :</span><span class="sxs-lookup"><span data-stu-id="b1583-259">There are a few important things toonote in any Job request:</span></span>

* <span data-ttu-id="b1583-260">Propriétés TaskBody doivent utiliser le nombre de hello de toodefine littéral XML d’entrée ou des éléments multimédias de sortie qui sont utilisés par hello tâche.</span><span class="sxs-lookup"><span data-stu-id="b1583-260">TaskBody properties MUST use literal XML toodefine hello number of input, or output assets that are used by hello Task.</span></span> <span data-ttu-id="b1583-261">la rubrique Hello contient hello définition de schéma XML pour hello XML.</span><span class="sxs-lookup"><span data-stu-id="b1583-261">hello Task topic contains hello XML Schema Definition for hello XML.</span></span>
* <span data-ttu-id="b1583-262">Bonjour définition de TaskBody, chaque interne valeur <inputAsset> et <outputAsset> doit être définie en tant que JobInputAsset(value) ou JobOutputAsset(value).</span><span class="sxs-lookup"><span data-stu-id="b1583-262">In hello TaskBody definition, each inner value for <inputAsset> and <outputAsset> must be set as JobInputAsset(value) or JobOutputAsset(value).</span></span>
* <span data-ttu-id="b1583-263">Une tâche peut comporter plusieurs ressources de sortie.</span><span class="sxs-lookup"><span data-stu-id="b1583-263">A task can have multiple output assets.</span></span> <span data-ttu-id="b1583-264">Un JobOutputAsset(x) ne peut être utilisé qu’une fois en tant que résultat d’une tâche dans un travail.</span><span class="sxs-lookup"><span data-stu-id="b1583-264">One JobOutputAsset(x) can only be used once as an output of a task in a job.</span></span>
* <span data-ttu-id="b1583-265">Vous pouvez spécifier JobInputAsset ou JobOutputAsset en tant que ressource d’entrée d’une tâche.</span><span class="sxs-lookup"><span data-stu-id="b1583-265">You can specify JobInputAsset or JobOutputAsset as an input asset of a task.</span></span>
* <span data-ttu-id="b1583-266">Les tâches ne doivent pas former un cycle.</span><span class="sxs-lookup"><span data-stu-id="b1583-266">Tasks must not form a cycle.</span></span>
* <span data-ttu-id="b1583-267">paramètre de valeur Hello que vous passez tooJobInputAsset ou JobOutputAsset représente la valeur d’index hello pour un élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="b1583-267">hello value parameter that you pass tooJobInputAsset or JobOutputAsset represents hello index value for an Asset.</span></span> <span data-ttu-id="b1583-268">Hello éléments multimédias réels sont définis dans les propriétés hello InputMediaAssets et OutputMediaAssets de la navigation sur hello définition de l’entité tâche.</span><span class="sxs-lookup"><span data-stu-id="b1583-268">hello actual Assets are defined in hello InputMediaAssets and OutputMediaAssets navigation properties on hello Job entity definition.</span></span>

> [!NOTE]
> <span data-ttu-id="b1583-269">Comme Media Services repose sur OData v3, hello des éléments multimédias individuels dans InputMediaAssets et OutputMediaAssets des ensembles de propriétés de navigation sont référencés par un « __metadata : uri « paire nom-valeur.</span><span class="sxs-lookup"><span data-stu-id="b1583-269">Because Media Services is built on OData v3, hello individual assets in InputMediaAssets and OutputMediaAssets navigation property collections are referenced through a "__metadata : uri" name-value pair.</span></span>
>
>

* <span data-ttu-id="b1583-270">InputMediaAssets mappe tooone ou plus de ressources que vous avez créé dans Media Services.</span><span class="sxs-lookup"><span data-stu-id="b1583-270">InputMediaAssets maps tooone or more Assets you have created in Media Services.</span></span> <span data-ttu-id="b1583-271">Propriétés OutputMediaAssets sont créées par le système de hello.</span><span class="sxs-lookup"><span data-stu-id="b1583-271">OutputMediaAssets are created by hello system.</span></span> <span data-ttu-id="b1583-272">Ils ne font pas référence à une ressource existante.</span><span class="sxs-lookup"><span data-stu-id="b1583-272">They do not reference an existing asset.</span></span>
* <span data-ttu-id="b1583-273">OutputMediaAssets peut être nommé à l’aide des attributs d’assetName hello.</span><span class="sxs-lookup"><span data-stu-id="b1583-273">OutputMediaAssets can be named using hello assetName attribute.</span></span> <span data-ttu-id="b1583-274">Si cet attribut n’est pas présent, nom hello Hello OutputMediaAsset est la valeur de texte interne hello Hello <outputAsset> élément est avec un suffixe de valeur de nom de la tâche hello ou valeur d’Id de tâche hello (dans le cas de hello où la propriété de nom hello n’est pas définie).</span><span class="sxs-lookup"><span data-stu-id="b1583-274">If this attribute is not present, then hello name of hello OutputMediaAsset is whatever hello inner text value of hello <outputAsset> element is with a suffix of either hello Job Name value, or hello Job Id value (in hello case where hello Name property isn't defined).</span></span> <span data-ttu-id="b1583-275">Par exemple, si vous définissez une valeur pour assetName trop « Exemple », puis hello propriété a la valeur Name du OutputMediaAsset trop « Sample ».</span><span class="sxs-lookup"><span data-stu-id="b1583-275">For example, if you set a value for assetName too"Sample", then hello OutputMediaAsset Name property would be set too"Sample".</span></span> <span data-ttu-id="b1583-276">Toutefois, si vous n’avez pas défini une valeur pour assetName, mais qui définissez le nom de la tâche hello trop « NewJob », puis hello Name du OutputMediaAsset serait « JobOutputAsset (valeur) _NewJob ».</span><span class="sxs-lookup"><span data-stu-id="b1583-276">However, if you did not set a value for assetName, but did set hello job name too"NewJob", then hello OutputMediaAsset Name would be "JobOutputAsset(value)_NewJob".</span></span>

    <span data-ttu-id="b1583-277">Bonjour à l’exemple suivant montre comment tooset hello attribut assetName :</span><span class="sxs-lookup"><span data-stu-id="b1583-277">hello following example shows how tooset hello assetName attribute:</span></span>

        "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"
* <span data-ttu-id="b1583-278">tooenable chaînage des tâches :</span><span class="sxs-lookup"><span data-stu-id="b1583-278">tooenable task chaining:</span></span>

  * <span data-ttu-id="b1583-279">un travail doit comporter au moins deux tâches</span><span class="sxs-lookup"><span data-stu-id="b1583-279">A job must have at least two tasks</span></span>
  * <span data-ttu-id="b1583-280">Il doit exister au moins une tâche dont l’entrée est la sortie d’une autre tâche dans la tâche de hello.</span><span class="sxs-lookup"><span data-stu-id="b1583-280">There must be at least one task whose input is output of another task in hello job.</span></span>

<span data-ttu-id="b1583-281">Pour plus d’informations, consultez [création d’un travail d’encodage avec hello API REST Media Services](media-services-rest-encode-asset.md).</span><span class="sxs-lookup"><span data-stu-id="b1583-281">For more information see, [Creating an Encoding Job with hello Media Services REST API](media-services-rest-encode-asset.md).</span></span>

### <a name="monitor-processing-progress"></a><span data-ttu-id="b1583-282">Surveillance de la progression du traitement</span><span class="sxs-lookup"><span data-stu-id="b1583-282">Monitor Processing Progress</span></span>
<span data-ttu-id="b1583-283">Vous pouvez récupérer des état de la tâche hello en utilisant la propriété d’état hello, comme indiqué dans hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="b1583-283">You can retrieve hello Job status by using hello State property, as shown in hello following example.</span></span>

<span data-ttu-id="b1583-284">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="b1583-284">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/State HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=zf84471d-2233-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908022&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=RYXOraO6Z%2f7l9whWZQN%2bypeijgHwIk8XyikA01Kx1%2bk%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 0


<span data-ttu-id="b1583-285">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="b1583-285">**HTTP Response**</span></span>

<span data-ttu-id="b1583-286">En cas de réussite, hello suivant la réponse est retournée :</span><span class="sxs-lookup"><span data-stu-id="b1583-286">If successful, hello following response is returned:</span></span>

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


### <a name="cancel-a-job"></a><span data-ttu-id="b1583-287">Annulation d’une tâche</span><span class="sxs-lookup"><span data-stu-id="b1583-287">Cancel a job</span></span>
<span data-ttu-id="b1583-288">Media Services vous permet de toocancel travaux en cours d’exécution via hello fonction CancelJob.</span><span class="sxs-lookup"><span data-stu-id="b1583-288">Media Services allows you toocancel running jobs through hello CancelJob function.</span></span> <span data-ttu-id="b1583-289">Cet appel renvoie un code de 400 erreur si vous essayez de toocancel une tâche lorsque son état est annulé, l’annulation, l’erreur ou terminé.</span><span class="sxs-lookup"><span data-stu-id="b1583-289">This call returns a 400 error code if you try toocancel a Job when its state is canceled, canceling, error, or finished.</span></span>

<span data-ttu-id="b1583-290">Hello suivant montre l’exemple de comment toocall CancelJob.</span><span class="sxs-lookup"><span data-stu-id="b1583-290">hello following example shows how toocall CancelJob.</span></span>

<span data-ttu-id="b1583-291">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="b1583-291">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.net/API/CancelJob?jobid='nb%3ajid%3aUUID%3a71d2dd33-efdf-ec43-8ea1-136a110bd42c' HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.2
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908753&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=kolAgnFfbQIeRv4lWxKSFa4USyjWXRm15Kd%2bNd5g8eA%3d
    Host: wamsbayclus001rest-hs.net


<span data-ttu-id="b1583-292">Si l’opération réussit, un code de réponse 204 est retourné, sans corps de message.</span><span class="sxs-lookup"><span data-stu-id="b1583-292">If successful, a 204 response code is returned with no message body.</span></span>

> [!NOTE]
> <span data-ttu-id="b1583-293">Vous devez coder par URL des id de tâche hello (normalement jid : valeur) lorsque vous transmettez en tant qu’un tooCancelJob paramètre.</span><span class="sxs-lookup"><span data-stu-id="b1583-293">You must URL-encode hello job id (normally nb:jid:UUID: somevalue) when passing it in as a parameter tooCancelJob.</span></span>
>
>

### <a name="get-hello-output-asset"></a><span data-ttu-id="b1583-294">Obtenir l’élément multimédia de sortie hello</span><span class="sxs-lookup"><span data-stu-id="b1583-294">Get hello output asset</span></span>
<span data-ttu-id="b1583-295">Hello de code suivant montre comment toorequest hello identificateur d’élément multimédia de sortie</span><span class="sxs-lookup"><span data-stu-id="b1583-295">hello following code shows how toorequest hello output asset Id.</span></span>

<span data-ttu-id="b1583-296">**Demande HTTP**</span><span class="sxs-lookup"><span data-stu-id="b1583-296">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/OutputMediaAssets() HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="b1583-297">**Réponse HTTP**</span><span class="sxs-lookup"><span data-stu-id="b1583-297">**HTTP Response**</span></span>

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



## <span data-ttu-id="b1583-298"><a id="publish_get_urls"></a>Publier les actifs hello et get de diffusion en continu et URL de téléchargement progressif avec l’API REST</span><span class="sxs-lookup"><span data-stu-id="b1583-298"><a id="publish_get_urls"></a>Publish hello asset and get streaming and progressive download URLs with REST API</span></span>

<span data-ttu-id="b1583-299">toostream ou téléchargement d’un élément multimédia, vous tout d’abord besoin trop « publier » en créant un localisateur.</span><span class="sxs-lookup"><span data-stu-id="b1583-299">toostream or download an asset, you first need too"publish" it by creating a locator.</span></span> <span data-ttu-id="b1583-300">Les localisateurs offrent toofiles accès contenues dans l’élément multimédia de hello.</span><span class="sxs-lookup"><span data-stu-id="b1583-300">Locators provide access toofiles contained in hello asset.</span></span> <span data-ttu-id="b1583-301">Media Services prend en charge deux types de localisateurs : OnDemandOrigin localisateurs, support toostream utilisé (par exemple, MPEG DASH, HLS ou Smooth Streaming) et les localisateurs de Signature d’accès (SAS), les fichiers de support de toodownload utilisés.</span><span class="sxs-lookup"><span data-stu-id="b1583-301">Media Services supports two types of locators: OnDemandOrigin locators, used toostream media (for example, MPEG DASH, HLS, or Smooth Streaming) and Access Signature (SAS) locators, used toodownload media files.</span></span> <span data-ttu-id="b1583-302">Pour plus d’informations sur les localisateurs de SAP, consultez [ce](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span><span class="sxs-lookup"><span data-stu-id="b1583-302">For more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span></span>

<span data-ttu-id="b1583-303">Une fois que vous créez les localisateurs hello, vous pouvez générer des URL hello toostream utilisé ou téléchargement vos fichiers.</span><span class="sxs-lookup"><span data-stu-id="b1583-303">Once you create hello locators, you can build hello URLs that are used toostream or download your files.</span></span>

>[!NOTE]
><span data-ttu-id="b1583-304">Création de votre compte AMS un **par défaut** point de terminaison de diffusion en continu est ajoutée tooyour compte Bonjour **arrêté** état.</span><span class="sxs-lookup"><span data-stu-id="b1583-304">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="b1583-305">toostart de diffusion en continu de votre contenu et profitez de l’empaquetage dynamique et chiffrement dynamique, hello de point de terminaison de diffusion en continu à partir de laquelle vous souhaitez que le contenu toostream a toobe Bonjour **en cours d’exécution** état.</span><span class="sxs-lookup"><span data-stu-id="b1583-305">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span>

<span data-ttu-id="b1583-306">Une URL de diffusion pour Smooth Streaming a hello suivant le format :</span><span class="sxs-lookup"><span data-stu-id="b1583-306">A streaming URL for Smooth Streaming has hello following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="b1583-307">Une URL de diffusion en continu pour TLS a hello suivant le format :</span><span class="sxs-lookup"><span data-stu-id="b1583-307">A streaming URL for HLS has hello following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="b1583-308">Une URL de diffusion en continu pour MPEG DASH a hello suivant le format :</span><span class="sxs-lookup"><span data-stu-id="b1583-308">A streaming URL for MPEG DASH has hello following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


<span data-ttu-id="b1583-309">Une URL SAS utilisé des fichiers toodownload a hello suivant le format :</span><span class="sxs-lookup"><span data-stu-id="b1583-309">A SAS URL used toodownload files has hello following format:</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

<span data-ttu-id="b1583-310">Cette section montre comment tooperform hello tâches suivantes nécessaires trop « publier » vos éléments multimédias.</span><span class="sxs-lookup"><span data-stu-id="b1583-310">This section shows how tooperform hello following tasks necessary too"publish" your assets.</span></span>  

* <span data-ttu-id="b1583-311">Création d’hello AccessPolicy avec autorisation de lecture</span><span class="sxs-lookup"><span data-stu-id="b1583-311">Creating hello AccessPolicy with read permission</span></span>
* <span data-ttu-id="b1583-312">Création d’une URL SAS pour le téléchargement de contenu</span><span class="sxs-lookup"><span data-stu-id="b1583-312">Creating a SAS URL for downloading content</span></span>
* <span data-ttu-id="b1583-313">Création d’une URL d’origine pour la diffusion en continu de contenu</span><span class="sxs-lookup"><span data-stu-id="b1583-313">Creating an origin URL for streaming content</span></span>

### <a name="creating-hello-accesspolicy-with-read-permission"></a><span data-ttu-id="b1583-314">Création d’hello AccessPolicy avec autorisation de lecture</span><span class="sxs-lookup"><span data-stu-id="b1583-314">Creating hello AccessPolicy with read permission</span></span>
<span data-ttu-id="b1583-315">Avant de télécharger ou de diffusion en continu un contenu multimédia, tout d’abord définir une stratégie d’accès avec des autorisations de lecture et créer hello entité de localisateur appropriée qui spécifie le type de hello du mécanisme de remise que vous souhaitez tooenable pour vos clients.</span><span class="sxs-lookup"><span data-stu-id="b1583-315">Before downloading or streaming any media content, first define an AccessPolicy with read permissions and create hello appropriate Locator entity that specifies hello type of delivery mechanism you want tooenable for your clients.</span></span> <span data-ttu-id="b1583-316">Pour plus d’informations sur les propriétés de hello disponibles, consultez [propriétés de l’entité AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties).</span><span class="sxs-lookup"><span data-stu-id="b1583-316">For more information on hello properties available, see [AccessPolicy Entity Properties](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties).</span></span>

<span data-ttu-id="b1583-317">Bonjour à l’exemple suivant montre comment toospecify hello la stratégie d’accès pour les autorisations de lecture pour un élément multimédia donné.</span><span class="sxs-lookup"><span data-stu-id="b1583-317">hello following example shows how toospecify hello AccessPolicy for read permissions for a given Asset.</span></span>

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

<span data-ttu-id="b1583-318">En cas de réussite, un code de 201 réussite est renvoyé et décrit l’entité AccessPolicy hello que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="b1583-318">If successful, a 201 success code is returned describing hello AccessPolicy entity that you created.</span></span> <span data-ttu-id="b1583-319">Vous utilisez ensuite hello AccessPolicy Id avec hello Id de ressource hello qui contient le fichier hello entité de localisateur de hello toocreate toodeliver (par exemple, une ressource en sortie).</span><span class="sxs-lookup"><span data-stu-id="b1583-319">You then use hello AccessPolicy Id along with hello Asset Id of hello asset that contains hello file you want toodeliver(such as an output asset) toocreate hello Locator entity.</span></span>

> [!NOTE]
> <span data-ttu-id="b1583-320">Ce flux de travail est hello identique au téléchargement d’un fichier lors de la réception d’un élément multimédia (tel qu’il a été décrit précédemment dans cette rubrique).</span><span class="sxs-lookup"><span data-stu-id="b1583-320">This basic workflow is hello same as uploading a file when ingesting an Asset (as was discussed earlier in this topic).</span></span> <span data-ttu-id="b1583-321">En outre, comme le téléchargement de fichiers, si vous (ou vos clients) doivent tooaccess vos fichiers immédiatement, définir les minutes de toofive valeur StartTime avant hello heure actuelle.</span><span class="sxs-lookup"><span data-stu-id="b1583-321">Also, like uploading files, if you (or your clients) need tooaccess your files immediately, set your StartTime value toofive minutes before hello current time.</span></span> <span data-ttu-id="b1583-322">Cette action est nécessaire, car il peut exister une horloge maximal autorisé entre le client de hello et Media Services.</span><span class="sxs-lookup"><span data-stu-id="b1583-322">This action is necessary because there may be clock skew between hello client and Media Services.</span></span> <span data-ttu-id="b1583-323">Hello valeur StartTime doit être Bonjour respectant le format de date/heure : AAAA-MM-JJThh (par exemple, « 2014-05-23T17:53:50Z »).</span><span class="sxs-lookup"><span data-stu-id="b1583-323">hello StartTime value must be in hello following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>
>
>

### <a name="creating-a-sas-url-for-downloading-content"></a><span data-ttu-id="b1583-324">Création d’une URL SAS pour le téléchargement de contenu</span><span class="sxs-lookup"><span data-stu-id="b1583-324">Creating a SAS URL for downloading content</span></span>
<span data-ttu-id="b1583-325">Hello suivant de code montre comment tooget une URL qui peut être utilisé toodownload un fichier multimédia créé et téléchargé précédemment.</span><span class="sxs-lookup"><span data-stu-id="b1583-325">hello following code shows how tooget a URL that can be used toodownload a media file created and uploaded previously.</span></span> <span data-ttu-id="b1583-326">Hello AccessPolicy dispose d’autorisations en lecture et chemin d’accès du localisateur hello fait référence l’URL de téléchargement SAS tooa.</span><span class="sxs-lookup"><span data-stu-id="b1583-326">hello AccessPolicy has read permissions set and hello Locator path refers tooa SAS download URL.</span></span>

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

<span data-ttu-id="b1583-327">En cas de réussite, hello suivant la réponse est retournée :</span><span class="sxs-lookup"><span data-stu-id="b1583-327">If successful, hello following response is returned:</span></span>

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


<span data-ttu-id="b1583-328">Hello retourné **chemin d’accès** propriété contient hello URL SAS.</span><span class="sxs-lookup"><span data-stu-id="b1583-328">hello returned **Path** property contains hello SAS URL.</span></span>

> [!NOTE]
> <span data-ttu-id="b1583-329">Si vous téléchargez le contenu chiffré de stockage, vous devez le déchiffrer avant de le restituer manuellement ou utiliser hello MediaProcessor de déchiffrement du stockage dans un toooutput de tâche de traitement traité les fichiers dans tooan clair d’hello OutputAsset, puis téléchargez à partir de cet élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="b1583-329">If you download storage encrypted content, you must manually decrypt it before rendering it, or use hello Storage Decryption MediaProcessor in a processing task toooutput processed files in hello clear tooan OutputAsset and then download from that Asset.</span></span> <span data-ttu-id="b1583-330">Pour plus d’informations sur le traitement, consultez Création d’un travail d’encodage avec hello API REST Media Services.</span><span class="sxs-lookup"><span data-stu-id="b1583-330">For more information on processing, see Creating an Encoding Job with hello Media Services REST API.</span></span> <span data-ttu-id="b1583-331">En outre, les localisateurs d’URL SAS ne peuvent pas être mis à jour après leur création.</span><span class="sxs-lookup"><span data-stu-id="b1583-331">Also, SAS URL Locators cannot be updated after they have been created.</span></span> <span data-ttu-id="b1583-332">Par exemple, vous ne pouvez pas réutiliser hello même localisateur avec une valeur StartTime mise à jour.</span><span class="sxs-lookup"><span data-stu-id="b1583-332">For example, you cannot reuse hello same Locator with an updated StartTime value.</span></span> <span data-ttu-id="b1583-333">Il s’agit en raison de façon hello que des URL de SAP sont créés.</span><span class="sxs-lookup"><span data-stu-id="b1583-333">This is because of hello way SAS URLs are created.</span></span> <span data-ttu-id="b1583-334">Si vous voulez tooaccess un élément multimédia en téléchargement après qu’un localisateur a expiré, vous devez créer un nouveau avec une nouvelle heure de début.</span><span class="sxs-lookup"><span data-stu-id="b1583-334">If you want tooaccess an asset for download after a Locator has expired, then you must create a new one with a new StartTime.</span></span>
>
>

### <a name="download-files"></a><span data-ttu-id="b1583-335">Téléchargement de fichiers</span><span class="sxs-lookup"><span data-stu-id="b1583-335">Download files</span></span>
<span data-ttu-id="b1583-336">Une fois que vous avez hello AccessPolicy et l’ensemble de la recherche, vous pouvez télécharger des fichiers à l’aide de hello API REST de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="b1583-336">Once you have hello AccessPolicy and Locator set, you can download files using hello Azure Storage REST APIs.</span></span>  

> [!NOTE]
> <span data-ttu-id="b1583-337">Vous devez ajouter le nom de fichier hello pour le fichier de hello souhaité toodownload toohello recherche **chemin d’accès** valeur reçue dans la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="b1583-337">You must add hello file name for hello file you want toodownload toohello Locator **Path** value received in hello previous section.</span></span> <span data-ttu-id="b1583-338">Par exemple, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="b1583-338">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="b1583-339">.</span><span class="sxs-lookup"><span data-stu-id="b1583-339">.</span></span> <span data-ttu-id="b1583-340">.</span><span class="sxs-lookup"><span data-stu-id="b1583-340">.</span></span> <span data-ttu-id="b1583-341">.</span><span class="sxs-lookup"><span data-stu-id="b1583-341">.</span></span>
>
>

<span data-ttu-id="b1583-342">Pour plus d’informations sur l’utilisation d’objets blob de stockage Microsoft Azure, consultez [API REST du service BLOB](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="b1583-342">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

<span data-ttu-id="b1583-343">À la suite de hello encodage de travail que vous avez effectuées précédemment (encodage en ensemble de MP4 à débit adaptatif), vous avez plusieurs fichiers MP4 que vous pouvez télécharger progressivement.</span><span class="sxs-lookup"><span data-stu-id="b1583-343">As a result of hello encoding job that you performed earlier (encoding into Adaptive MP4 set), you have multiple MP4 files that you can progressively download.</span></span> <span data-ttu-id="b1583-344">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="b1583-344">For example:</span></span>    

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


### <a name="creating-a-streaming-url-for-streaming-content"></a><span data-ttu-id="b1583-345">Création d’une URL pour la diffusion en continu de contenu</span><span class="sxs-lookup"><span data-stu-id="b1583-345">Creating a streaming URL for streaming content</span></span>
<span data-ttu-id="b1583-346">Hello suivant de code montre comment toocreate un localisateur d’URL de diffusion en continu :</span><span class="sxs-lookup"><span data-stu-id="b1583-346">hello following code shows how toocreate a streaming URL Locator:</span></span>

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

<span data-ttu-id="b1583-347">En cas de réussite, hello suivant la réponse est retournée :</span><span class="sxs-lookup"><span data-stu-id="b1583-347">If successful, hello following response is returned:</span></span>

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

<span data-ttu-id="b1583-348">toostream une URL d’origine de diffusion en continu lisse dans un lecteur multimédia en continu, vous devez ajouter de propriété de chemin d’accès de hello portant le nom de hello Hello Smooth Streaming manifeste de fichier, suivi par « /manifest ».</span><span class="sxs-lookup"><span data-stu-id="b1583-348">toostream a Smooth Streaming origin URL in a streaming media player, you must append hello Path property with hello name of hello Smooth Streaming manifest file, followed by "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

<span data-ttu-id="b1583-349">toostream TLS, ajouter (format = m3u8-aapl) après hello « /manifest ».</span><span class="sxs-lookup"><span data-stu-id="b1583-349">toostream HLS, append (format=m3u8-aapl) after hello "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

<span data-ttu-id="b1583-350">toostream MPEG DASH, ajouter (format = mpd-heure-csf) après hello « /manifest ».</span><span class="sxs-lookup"><span data-stu-id="b1583-350">toostream MPEG DASH, append (format=mpd-time-csf) after hello "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)


## <span data-ttu-id="b1583-351"><a id="play"></a>Lecture de votre contenu</span><span class="sxs-lookup"><span data-stu-id="b1583-351"><a id="play"></a>Play your content</span></span>
<span data-ttu-id="b1583-352">toostream vidéo, vous utilisez [lecteur Azure Media Services](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="b1583-352">toostream you video, use [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

<span data-ttu-id="b1583-353">tootest progressif de téléchargement, collez une URL dans un navigateur (par exemple, Internet Explorer, Chrome, Safari).</span><span class="sxs-lookup"><span data-stu-id="b1583-353">tootest progressive download, paste a URL into a browser (for example, IE, Chrome, Safari).</span></span>

## <a name="next-steps-media-services-learning-paths"></a><span data-ttu-id="b1583-354">Étapes suivantes : Parcours d’apprentissage Media Services</span><span class="sxs-lookup"><span data-stu-id="b1583-354">Next Steps: Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b1583-355">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="b1583-355">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
