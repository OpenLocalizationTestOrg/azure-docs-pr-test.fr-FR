---
title: Utilisation du chiffrement commun dynamique PlayReady et/ou Widevine | Microsoft Docs
description: "Microsoft Azure Media Services vous permet de fournir des flux MPEG-DASH, Smooth Streaming et HLS (Http-Live-Streaming) protégés par Microsoft PlayReady DRM. Vous pouvez également l’utiliser pour diffuser du contenu DASH chiffré avec Widevine DRM. Cette rubrique montre comment chiffrer dynamiquement avec PlayReady et Widevine DRM."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 548d1a12-e2cb-45fe-9307-4ec0320567a2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 6cfb7b558b8dce511d517e69c022765feae245fa
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="using-playready-andor-widevine-dynamic-common-encryption"></a><span data-ttu-id="0fdb4-105">Utilisation du chiffrement commun dynamique PlayReady et/ou Widevine</span><span class="sxs-lookup"><span data-stu-id="0fdb4-105">Using PlayReady and/or Widevine dynamic common encryption</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0fdb4-106">.NET</span><span class="sxs-lookup"><span data-stu-id="0fdb4-106">.NET</span></span>](media-services-protect-with-drm.md)
> * [<span data-ttu-id="0fdb4-107">Java</span><span class="sxs-lookup"><span data-stu-id="0fdb4-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="0fdb4-108">PHP</span><span class="sxs-lookup"><span data-stu-id="0fdb4-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
>
>

<span data-ttu-id="0fdb4-109">Microsoft Azure Media Services vous permet de fournir des flux MPEG-DASH, Smooth Streaming et HLS (HTTP-Live-Streaming) protégés par [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span><span class="sxs-lookup"><span data-stu-id="0fdb4-109">Microsoft Azure Media Services enables you to deliver MPEG-DASH, Smooth Streaming, and HTTP-Live-Streaming (HLS) streams protected with [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span></span> <span data-ttu-id="0fdb4-110">Vous pouvez également l’utiliser pour diffuser du contenu DASH chiffré avec des licences Widevine DRM.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-110">It also enables you to deliver encrypted DASH streams with Widevine DRM licenses.</span></span> <span data-ttu-id="0fdb4-111">PlayReady et Widewine sont chiffrés conformément à la spécification de chiffrement commun (ISO/IEC 23001-7 CENC).</span><span class="sxs-lookup"><span data-stu-id="0fdb4-111">Both PlayReady and Widevine are encrypted per the Common Encryption (ISO/IEC 23001-7 CENC) specification.</span></span> <span data-ttu-id="0fdb4-112">Vous pouvez utiliser [AMS .NET SDK](https://www.nuget.org/packages/windowsazure.mediaservices/) (en commençant par la version 3.5.1) ou une API REST pour configurer votre AssetDeliveryConfiguration afin d’utiliser Widevine.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-112">You can use [AMS .NET SDK](https://www.nuget.org/packages/windowsazure.mediaservices/) (starting with the version 3.5.1) or REST API to configure your AssetDeliveryConfiguration to use Widevine.</span></span>

<span data-ttu-id="0fdb4-113">Media Services fournit un service de remise de licences DRM PlayReady et Widevine.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-113">Media Services provides a service for delivering PlayReady and Widevine DRM licenses.</span></span> <span data-ttu-id="0fdb4-114">Media Services fournit également des API qui vous permettent de configurer les droits et les restrictions que vous souhaitez pour le runtime DRM PlayReady ou Widevine, qui s’appliquent lorsqu’un utilisateur lit un contenu protégé.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-114">Media Services also provides APIs that let you configure the rights and restrictions that you want for the PlayReady or Widevine DRM runtime to enforce when a user plays back protected content.</span></span> <span data-ttu-id="0fdb4-115">Lorsqu’un utilisateur demande un contenu DRM protégé, l’application de lecteur demande une licence du service de licence AMS.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-115">When a user requests a DRM protected content, the player application will request a license from the AMS license service.</span></span> <span data-ttu-id="0fdb4-116">Le service de licence AMS émet une licence pour le lecteur s’il est autorisé.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-116">The AMS license service will issue a license to the player if it is authorized.</span></span> <span data-ttu-id="0fdb4-117">Une licence PlayReady ou Widevine contient la clé de déchiffrement qui peut être utilisée par le lecteur client pour déchiffrer et diffuser le contenu.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-117">A PlayReady or Widevine license contains the decryption key that can be used by the client player to decrypt and stream the content.</span></span>

<span data-ttu-id="0fdb4-118">Vous pouvez également utiliser les partenaires AMS suivants pour vous aider à distribuer des licences Widevine : [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span><span class="sxs-lookup"><span data-stu-id="0fdb4-118">You can also use the following AMS partners to help you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span> <span data-ttu-id="0fdb4-119">Pour plus d’informations, consultez : Intégration à [Axinom](media-services-axinom-integration.md) et [castLabs](media-services-castlabs-integration.md).</span><span class="sxs-lookup"><span data-stu-id="0fdb4-119">For more information, see: integration with [Axinom](media-services-axinom-integration.md) and [castLabs](media-services-castlabs-integration.md).</span></span>

<span data-ttu-id="0fdb4-120">Media Services prend en charge plusieurs méthodes d’autorisation des utilisateurs effectuant des demandes de clé.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-120">Media Services supports multiple ways of authorizing users who make key requests.</span></span> <span data-ttu-id="0fdb4-121">La stratégie d’autorisation des clés de contenu peut comporter une ou plusieurs restrictions d’autorisation : ouverte ou restriction à jeton.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-121">The content key authorization policy could have one or more authorization restrictions: open or token restriction.</span></span> <span data-ttu-id="0fdb4-122">La stratégie de restriction à jeton doit être accompagnée d’un jeton émis par un service de jeton sécurisé (STS).</span><span class="sxs-lookup"><span data-stu-id="0fdb4-122">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="0fdb4-123">Media Services prend en charge les jetons aux formats [SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) (Simple Web Tokens) et [JWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JSON Web Token).</span><span class="sxs-lookup"><span data-stu-id="0fdb4-123">Media Services supports tokens in the [Simple Web Tokens](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) (SWT) format and [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JWT) format.</span></span> <span data-ttu-id="0fdb4-124">Pour plus d'informations, consultez Configurer la stratégie d'autorisation de la clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-124">For more information, see Configure the content key’s authorization policy.</span></span>

<span data-ttu-id="0fdb4-125">Pour tirer parti du chiffrement dynamique, vous devez avoir un élément multimédia qui contient un ensemble de fichiers MP4 à débit binaire multiple ou de fichiers sources de diffusion en continu lisse (Smooth Streaming) à débit binaire multiple.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-125">To take advantage of dynamic encryption, you need to have an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="0fdb4-126">Vous devez également configurer les stratégies de remise pour l’élément multimédia (décrites plus loin dans cette rubrique).</span><span class="sxs-lookup"><span data-stu-id="0fdb4-126">You also need to configure the delivery policies for the asset (described later in this topic).</span></span> <span data-ttu-id="0fdb4-127">Ensuite, en fonction du format spécifié dans l'URL de diffusion, le serveur de streaming à la demande s'assure que le flux est livré conformément au protocole choisi.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-127">Then, based on the format specified in the streaming URL, the On-Demand Streaming server will ensure that the stream is delivered in the protocol you have chosen.</span></span> <span data-ttu-id="0fdb4-128">Par conséquent, il vous suffit de stocker et de payer les fichiers dans un seul format de stockage. Media Services se charge de créer et de fournir la réponse HTTP appropriée à chaque demande des clients.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-128">As a result, you only need to store and pay for the files in a single storage format and Media Services will build and serve the appropriate HTTP response based on each request from a client.</span></span>

<span data-ttu-id="0fdb4-129">Cette rubrique peut être utile aux développeurs travaillant sur des applications qui fournissent un support protégé avec plusieurs DRM comme PlayReady et Widevine.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-129">This topic would be useful to developers that work on applications that deliver media protected with multiple DRMs, such as PlayReady and Widevine.</span></span> <span data-ttu-id="0fdb4-130">La rubrique vous montre comment configurer le service de distribution des licences PlayReady avec des stratégies d’autorisation, afin que seuls les clients autorisés puissent recevoir les licences PlayReady ou Widevine.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-130">The topic shows you how to configure the PlayReady license delivery service with authorization policies so that only authorized clients could receive PlayReady or Widevine licenses.</span></span> <span data-ttu-id="0fdb4-131">Il indique également comment utiliser le chiffrement de cryptage dynamique avec PlayReady ou Widevine DRM sur DASH.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-131">It also shows how to use dynamic encryption encryption with PlayReady or Widevine DRM over DASH.</span></span>

>[!NOTE]
><span data-ttu-id="0fdb4-132">Une fois votre compte AMS créé, un point de terminaison de streaming **par défaut** est ajouté à votre compte à l’état **Arrêté**.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-132">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="0fdb4-133">Pour démarrer la diffusion en continu de votre contenu et tirer parti de l’empaquetage et du chiffrement dynamiques, le point de terminaison de streaming à partir duquel vous souhaitez diffuser du contenu doit se trouver à l’état **En cours d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-133">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> 

## <a name="download-sample"></a><span data-ttu-id="0fdb4-134">Charger l’exemple</span><span class="sxs-lookup"><span data-stu-id="0fdb4-134">Download sample</span></span>
<span data-ttu-id="0fdb4-135">Vous pouvez télécharger l’exemple décrit dans cet article à partir d’ [ici](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-drm).</span><span class="sxs-lookup"><span data-stu-id="0fdb4-135">You can download the sample described in this article from [here](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-drm).</span></span>

## <a name="configuring-dynamic-common-encryption-and-drm-license-delivery-services"></a><span data-ttu-id="0fdb4-136">Configuration de Dynamic Common Encryption et services de distribution de licences DRM</span><span class="sxs-lookup"><span data-stu-id="0fdb4-136">Configuring Dynamic Common Encryption and DRM License Delivery Services</span></span>

<span data-ttu-id="0fdb4-137">Voici les étapes générales que vous aurez à exécuter lors de la protection de vos éléments multimédias avec PlayReady, en utilisant le service de distribution des licences Media Services, ainsi que le chiffrement dynamique.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-137">The following are general steps that you would need to perform when protecting your assets with PlayReady, using the Media Services license delivery service, and also using dynamic encryption.</span></span>

1. <span data-ttu-id="0fdb4-138">Créer un élément multimédia et télécharger des fichiers dans l'élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-138">Create an asset and upload files into the asset.</span></span>
2. <span data-ttu-id="0fdb4-139">Encoder l'élément multimédia contenant le fichier selon le débit binaire MP4 défini.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-139">Encode the asset containing the file to the adaptive bitrate MP4 set.</span></span>
3. <span data-ttu-id="0fdb4-140">Créer une clé de contenu et l'associer à l'élément multimédia encodé.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-140">Create a content key and associate it with the encoded asset.</span></span> <span data-ttu-id="0fdb4-141">Dans Media Services, la clé de contenu contient la clé de chiffrement de l'élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-141">In Media Services, the content key contains the asset’s encryption key.</span></span>
4. <span data-ttu-id="0fdb4-142">Configurer la stratégie d'autorisation de la clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-142">Configure the content key’s authorization policy.</span></span> <span data-ttu-id="0fdb4-143">La stratégie d'autorisation de la clé de contenu doit être configurée par vous et respectée par le client afin que la clé de contenu soit remise au client.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-143">The content key authorization policy must be configured by you and met by the client in order for the content key to be delivered to the client.</span></span>

    <span data-ttu-id="0fdb4-144">Lorsque vous créez la stratégie d’autorisation de clé de contenu, vous devez spécifier les éléments suivants : méthode de livraison (PlayReady ou Widevine), restrictions de remise (ouvertes ou jeton) et informations spécifiques au type de remise de clé qui définit comment la clé est fournie au client (modèle de licence [PlayReady](media-services-playready-license-template-overview.md) ou [Widevine](media-services-widevine-license-template-overview.md)).</span><span class="sxs-lookup"><span data-stu-id="0fdb4-144">When creating the content key authorization policy, you need to specify the following: delivery method (PlayReady or Widevine), restrictions (open or token), and information specific to the key delivery type that defines how the key is delivered to the client ([PlayReady](media-services-playready-license-template-overview.md) or [Widevine](media-services-widevine-license-template-overview.md) license template).</span></span>

5. <span data-ttu-id="0fdb4-145">Configurer la stratégie de remise pour un élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-145">Configure the delivery policy for an asset.</span></span> <span data-ttu-id="0fdb4-146">La configuration de la stratégie de remise inclut : le protocole de remise (par exemple, MPEG DASH, HLS, Smooth Streaming ou tous), le type de chiffrement dynamique (par exemple, chiffrement commun), l’URL d’acquisition de licence PlayReady ou Widevine.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-146">The delivery policy configuration includes: delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all), the type of dynamic encryption (for example, Common Encryption), PlayReady or Widevine license acquisition URL.</span></span>

    <span data-ttu-id="0fdb4-147">Vous pouvez appliquer des stratégies différentes à chaque protocole dans le même élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-147">You could apply different policy to each protocol on the same asset.</span></span> <span data-ttu-id="0fdb4-148">Par exemple, vous pouvez appliquer le chiffrement PlayReady à Smooth/DASH et AES Envelope à HLS.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-148">For example, you could apply PlayReady encryption to Smooth/DASH and AES Envelope to HLS.</span></span> <span data-ttu-id="0fdb4-149">Tous les protocoles qui ne sont pas définis dans une stratégie de remise (par exemple, en cas d’ajout d’une stratégie unique qui spécifie uniquement TLS comme protocole) seront bloqués de la diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-149">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as the protocol) will be blocked from streaming.</span></span> <span data-ttu-id="0fdb4-150">Cela ne s’applique toutefois pas si vous n’avez défini aucune stratégie de remise de ressources.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-150">The exception to this is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="0fdb4-151">Tous les protocoles seront alors autorisés.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-151">Then, all protocols will be allowed in the clear.</span></span>

6. <span data-ttu-id="0fdb4-152">Créer un localisateur à la demande afin d'obtenir une URL de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-152">Create an OnDemand locator in order to get a streaming URL.</span></span>

<span data-ttu-id="0fdb4-153">Vous trouverez un exemple .NET complet à la fin de la rubrique.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-153">You will find a complete .NET example at the end of the topic.</span></span>

<span data-ttu-id="0fdb4-154">L'illustration suivante montre le flux de travail décrit ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-154">The following image demonstrates the workflow described above.</span></span> <span data-ttu-id="0fdb4-155">Ici, le jeton est utilisé pour l'authentification.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-155">Here the token is used for authentication.</span></span>

![Protéger avec PlayReady](./media/media-services-content-protection-overview/media-services-content-protection-with-drm.png)

<span data-ttu-id="0fdb4-157">Le reste de cette rubrique fournit des explications détaillées, des exemples de code et des liens vers des rubriques qui vous expliquent comment réaliser les tâches décrites ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-157">The rest of this topic provides detailed explanations, code examples, and links to topics that show you how to achieve the tasks described above.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="0fdb4-158">Limitations actuelles</span><span class="sxs-lookup"><span data-stu-id="0fdb4-158">Current limitations</span></span>
<span data-ttu-id="0fdb4-159">Si vous ajoutez ou mettez à jour une stratégie de remise de ressource, vous devez supprimer le localisateur associé (le cas échéant) et en créer un nouveau.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-159">If you add or update an asset delivery policy, you must delete the associated locator (if any) and create a new locator.</span></span>

<span data-ttu-id="0fdb4-160">Limites lors du chiffrement Widevine avec Azure Media Services : actuellement, plusieurs clés de contenu ne sont pas prises en charge.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-160">Limitation when encrypting with Widevine with Azure Media Services: currently, multiple content keys are not supported.</span></span>

## <a name="create-an-asset-and-upload-files-into-the-asset"></a><span data-ttu-id="0fdb4-161">Créer un élément multimédia et télécharger des fichiers dans l'élément multimédia</span><span class="sxs-lookup"><span data-stu-id="0fdb4-161">Create an asset and upload files into the asset</span></span>
<span data-ttu-id="0fdb4-162">Pour gérer, encoder et diffuser vos vidéos, vous devez d'abord télécharger votre contenu dans Microsoft Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-162">In order to manage, encode, and stream your videos, you must first upload your content into Microsoft Azure Media Services.</span></span> <span data-ttu-id="0fdb4-163">Une fois téléchargé, votre contenu est stocké en toute sécurité dans le cloud et peut faire l’objet d’un traitement et d’une diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-163">Once uploaded, your content is stored securely in the cloud for further processing and streaming.</span></span>

<span data-ttu-id="0fdb4-164">Pour plus d’informations, consultez [Charger des fichiers vers un compte Media Services](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="0fdb4-164">For detailed information, see [Upload Files into a Media Services account](media-services-dotnet-upload-files.md).</span></span>

## <a name="encode-the-asset-containing-the-file-to-the-adaptive-bitrate-mp4-set"></a><span data-ttu-id="0fdb4-165">Encoder l'élément multimédia contenant le fichier selon le débit binaire MP4 défini</span><span class="sxs-lookup"><span data-stu-id="0fdb4-165">Encode the asset containing the file to the adaptive bitrate MP4 set</span></span>
<span data-ttu-id="0fdb4-166">Avec le chiffrement dynamique, il vous suffit de créer un élément multimédia qui contient un ensemble de fichiers MP4 à débit binaire multiple ou de fichiers sources de diffusion en continu lisse à débit binaire multiple.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-166">With dynamic encryption all you need is to create an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="0fdb4-167">Ensuite, en fonction du format spécifié dans le manifeste et la demande de fragment, le serveur de diffusion en continu à la demande s’assure que vous recevez le flux conforme au protocole choisi.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-167">Then, based on the specified format in the manifest and fragment request, the On-Demand Streaming server will ensure that you receive the stream in the protocol you have chosen.</span></span> <span data-ttu-id="0fdb4-168">Par conséquent, il vous suffit de stocker et de payer les fichiers dans un seul format de stockage. Le service Media Services se charge de créer et de fournir la réponse appropriée en fonction des demandes des clients.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-168">As a result, you only need to store and pay for the files in single storage format and Media Services service will build and serve the appropriate response based on requests from a client.</span></span> <span data-ttu-id="0fdb4-169">Pour plus d’informations, consultez la rubrique [Vue d’ensemble de l’empaquetage dynamique](media-services-dynamic-packaging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0fdb4-169">For more information, see the [Dynamic Packaging Overview](media-services-dynamic-packaging-overview.md) topic.</span></span>

<span data-ttu-id="0fdb4-170">Pour savoir comment encoder, consultez [Encodage d’un élément multimédia à l’aide de Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).</span><span class="sxs-lookup"><span data-stu-id="0fdb4-170">For instructions on how to encode, see [How to encode an asset using Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).</span></span>

## <span data-ttu-id="0fdb4-171"><a id="create_contentkey"></a>Créer une clé de contenu et l’associer à l’élément multimédia encodé</span><span class="sxs-lookup"><span data-stu-id="0fdb4-171"><a id="create_contentkey"></a>Create a content key and associate it with the encoded asset</span></span>
<span data-ttu-id="0fdb4-172">Dans Media Services, la clé de contenu contient la clé que vous souhaitez utiliser pour chiffrer un élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-172">In Media Services, the content key contains the key that you want to encrypt an asset with.</span></span>

<span data-ttu-id="0fdb4-173">Pour plus d’informations, consultez [Créer une clé de contenu](media-services-dotnet-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="0fdb4-173">For detailed information, see [Create content key](media-services-dotnet-create-contentkey.md).</span></span>

## <span data-ttu-id="0fdb4-174"><a id="configure_key_auth_policy"></a>Configurez la stratégie d’autorisation de la clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-174"><a id="configure_key_auth_policy"></a>Configure the content key’s authorization policy</span></span>
<span data-ttu-id="0fdb4-175">Media Services prend en charge plusieurs méthodes d’authentification des utilisateurs effectuant des demandes de clé.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-175">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="0fdb4-176">La stratégie d'autorisation de la clé de contenu doit être configurée par vous et respectée par le client (lecteur) afin que la clé soit remise au client.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-176">The content key authorization policy must be configured by you and met by the client (player) in order for the key to be delivered to the client.</span></span> <span data-ttu-id="0fdb4-177">La stratégie d’autorisation des clés de contenu peut comporter une ou plusieurs restrictions d’autorisation : ouverte ou restriction à jeton.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-177">The content key authorization policy could have one or more authorization restrictions: open or token restriction.</span></span>

<span data-ttu-id="0fdb4-178">Pour plus d’informations, consultez [Configurer la stratégie d’autorisation de clé de contenu](media-services-dotnet-configure-content-key-auth-policy.md#playready-dynamic-encryption).</span><span class="sxs-lookup"><span data-stu-id="0fdb4-178">For detailed information, see [Configure Content Key Authorization Policy](media-services-dotnet-configure-content-key-auth-policy.md#playready-dynamic-encryption).</span></span>

## <span data-ttu-id="0fdb4-179"><a id="configure_asset_delivery_policy"></a>Configurer la stratégie de distribution d’éléments multimédia</span><span class="sxs-lookup"><span data-stu-id="0fdb4-179"><a id="configure_asset_delivery_policy"></a>Configure asset delivery policy</span></span>
<span data-ttu-id="0fdb4-180">Configurez la stratégie de remise pour votre élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-180">Configure the delivery policy for your asset.</span></span> <span data-ttu-id="0fdb4-181">Certains éléments que la configuration de la stratégie de remise de l'élément multimédia inclut :</span><span class="sxs-lookup"><span data-stu-id="0fdb4-181">Some things that the asset delivery policy configuration includes:</span></span>

* <span data-ttu-id="0fdb4-182">L’URL d’acquisition de licence PlayReady.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-182">The DRM license acquisition URL.</span></span>
* <span data-ttu-id="0fdb4-183">Le protocole de remise de l’élément multimédia (par exemple, MPEG DASH, HLS, Smooth Streaming ou tous).</span><span class="sxs-lookup"><span data-stu-id="0fdb4-183">The asset delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all).</span></span>
* <span data-ttu-id="0fdb4-184">Le type de chiffrement dynamique (dans ce cas, Common Encryption).</span><span class="sxs-lookup"><span data-stu-id="0fdb4-184">The type of dynamic encryption (in this case, Common Encryption).</span></span>

<span data-ttu-id="0fdb4-185">Pour plus d’informations, consultez [Configurer la stratégie de distribution d’éléments multimédia ](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="0fdb4-185">For detailed information, see [Configure asset delivery policy ](media-services-rest-configure-asset-delivery-policy.md).</span></span>

## <span data-ttu-id="0fdb4-186"><a id="create_locator"></a>Créer un localisateur de diffusion en continu à la demande afin d’obtenir une URL de diffusion en continu</span><span class="sxs-lookup"><span data-stu-id="0fdb4-186"><a id="create_locator"></a>Create an OnDemand streaming locator in order to get a streaming URL</span></span>
<span data-ttu-id="0fdb4-187">Vous devrez fournir aux utilisateurs l'URL de diffusion en continu pour Smooth, DASH ou HLS.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-187">You will need to provide your user with the streaming URL for Smooth, DASH or HLS.</span></span>

> [!NOTE]
> <span data-ttu-id="0fdb4-188">Si vous ajoutez ou mettez à jour la stratégie de remise de votre ressource, vous devez supprimer le localisateur existant (le cas échéant) et en créer un nouveau.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-188">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
>
>

<span data-ttu-id="0fdb4-189">Pour savoir comment publier une ressource et générer une URL de diffusion en continu, consultez [Générer une URL de diffusion en continu](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="0fdb4-189">For instructions on how to publish an asset and build a streaming URL, see [Build a streaming URL](media-services-deliver-streaming-content.md).</span></span>

## <a name="get-a-test-token"></a><span data-ttu-id="0fdb4-190">Obtenir un test de jeton</span><span class="sxs-lookup"><span data-stu-id="0fdb4-190">Get a test token</span></span>
<span data-ttu-id="0fdb4-191">Obtenez un jeton de test basé sur la restriction par jeton utilisée pour la stratégie d’autorisation de clé.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-191">Get a test token based on the token restriction that was used for the key authorization policy.</span></span>

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate =
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on the data in the given TokenRestrictionTemplate.
    //The GenerateTestToken method returns the token without the word “Bearer” in front
    //so you have to add it in front of the token string.
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate);
    Console.WriteLine("The authorization token is:\nBearer {0}", testToken);


<span data-ttu-id="0fdb4-192">Vous pouvez utiliser le [lecteur AMS](http://amsplayer.azurewebsites.net/azuremediaplayer.html) pour tester votre flux.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-192">You can use the [AMS Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) to test your stream.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="0fdb4-193">Créer et configurer un projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0fdb4-193">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="0fdb4-194">Configurez votre environnement de développement et ajoutez des informations de connexion au fichier app.config selon la procédure décrite dans l’article [Développement Media Services avec .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="0fdb4-194">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="0fdb4-195">Ajoutez les éléments suivants aux **appSettings** définis dans votre fichier app.config :</span><span class="sxs-lookup"><span data-stu-id="0fdb4-195">Add the following elements to **appSettings** defined in your app.config file:</span></span>

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a><span data-ttu-id="0fdb4-196">Exemple</span><span class="sxs-lookup"><span data-stu-id="0fdb4-196">Example</span></span>

<span data-ttu-id="0fdb4-197">L’exemple suivant illustre la fonctionnalité présentée dans le kit de développement logiciel Azure Media Services pour .Net-Version 3.5.2 (en particulier, la possibilité de définir un modèle de licence Widevine et de demander une licence Widevine Azure Media Services).</span><span class="sxs-lookup"><span data-stu-id="0fdb4-197">The following sample demonstrates functionality that was introduced in Azure Media Services SDK for .Net -Version 3.5.2 (specifically, the ability to define a Widevine license template and request a Widevine license from Azure Media Services).</span></span>

<span data-ttu-id="0fdb4-198">Remplacez le code dans votre fichier Program.cs par le code présenté dans cette section.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-198">Overwrite the code in your Program.cs file with the code shown in this section.</span></span>

>[!NOTE]
><span data-ttu-id="0fdb4-199">Un nombre limite de 1 000 000 a été défini pour les différentes stratégies AMS (par exemple, pour la stratégie de localisateur ou pour ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="0fdb4-199">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="0fdb4-200">Vous devez utiliser le même ID de stratégie si vous utilisez toujours les mêmes jours / autorisations d’accès, par exemple, les stratégies pour les localisateurs destinées à demeurer en place pendant une longue période (stratégies sans chargement).</span><span class="sxs-lookup"><span data-stu-id="0fdb4-200">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="0fdb4-201">Pour plus d’informations, consultez [cette rubrique](media-services-dotnet-manage-entities.md#limit-access-policies) .</span><span class="sxs-lookup"><span data-stu-id="0fdb4-201">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="0fdb4-202">Veillez à mettre à jour les variables pour pointer vers les dossiers où se trouvent vos fichiers d'entrée.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-202">Make sure to update variables to point to folders where your input files are located.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Threading;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;
    using Microsoft.WindowsAzure.MediaServices.Client.Widevine;
    using Newtonsoft.Json;

    namespace DynamicEncryptionWithDRM
    {
        class Program
        {
        // Read values from the App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static readonly Uri _sampleIssuer =
            new Uri(ConfigurationManager.AppSettings["Issuer"]);
        private static readonly Uri _sampleAudience =
            new Uri(ConfigurationManager.AppSettings["Audience"]);

        // Field for service context.
        private static CloudMediaContext _context = null;

        private static readonly string _mediaFiles =
            Path.GetFullPath(@"../..\Media");

        private static readonly string _singleMP4File =
            Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            bool tokenRestriction = false;
            string tokenTemplateString = null;

            IAsset asset = UploadFileAndCreateAsset(_singleMP4File);
            Console.WriteLine("Uploaded asset: {0}", asset.Id);

            IAsset encodedAsset = EncodeToAdaptiveBitrateMP4Set(asset);
            Console.WriteLine("Encoded asset: {0}", encodedAsset.Id);

            IContentKey key = CreateCommonTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for the asset {1} ", key.Id, encodedAsset.Id);
            Console.WriteLine("PlayReady License Key delivery URL: {0}", key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense));
            Console.WriteLine();

            if (tokenRestriction)
            tokenTemplateString = AddTokenRestrictedAuthorizationPolicy(key);
            else
            AddOpenAuthorizationPolicy(key);

            Console.WriteLine("Added authorization policy: {0}", key.AuthorizationPolicyId);
            Console.WriteLine();

            CreateAssetDeliveryPolicy(encodedAsset, key);
            Console.WriteLine("Created asset delivery policy. \n");
            Console.WriteLine();

            if (tokenRestriction && !String.IsNullOrEmpty(tokenTemplateString))
            {
            // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
            // back into a TokenRestrictionTemplate class instance.
            TokenRestrictionTemplate tokenTemplate =
                TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

            // Generate a test token based on the the data in the given TokenRestrictionTemplate.
            // Note, you need to pass the key id Guid because we specified
            // TokenClaim.ContentKeyIdentifierClaim in during the creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey,
                                        DateTime.UtcNow.AddDays(365));
            Console.WriteLine("The authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            // You can use the http://amsplayer.azurewebsites.net/azuremediaplayer.html player to test streams.
            // Note that DASH works on IE 11 (via PlayReady), Edge (via PlayReady), Chrome (via Widevine).

            string url = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Encrypted DASH URL: {0}/manifest(format=mpd-time-csf)", url);

            Console.ReadLine();
        }

        static public IAsset UploadFileAndCreateAsset(string singleFilePath)
        {
            if (!File.Exists(singleFilePath))
            {
            Console.WriteLine("File does not exist.");
            return null;
            }

            var assetName = Path.GetFileNameWithoutExtension(singleFilePath);
            IAsset inputAsset = _context.Assets.Create(assetName, AssetCreationOptions.None);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Created assetFile {0}", assetFile.Name);

            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset inputAsset)
        {
            var encodingPreset = "Adaptive Streaming";

            IJob job = _context.Jobs.Create(String.Format("Encoding into Mp4 {0} to {1}",
                        inputAsset.Name,
                        encodingPreset));

            var mediaProcessors =
            _context.MediaProcessors.Where(p => p.Name.Contains("Media Encoder Standard")).ToList();

            var latestMediaProcessor =
            mediaProcessors.OrderBy(mp => new Version(mp.Version)).LastOrDefault();

            ITask encodeTask = job.Tasks.AddNew("Encoding", latestMediaProcessor, encodingPreset, TaskOptions.None);
            encodeTask.InputAssets.Add(inputAsset);
            encodeTask.OutputAssets.AddNew(String.Format("{0} as {1}", inputAsset.Name, encodingPreset), AssetCreationOptions.StorageEncrypted);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }


        static public IContentKey CreateCommonTypeContentKey(IAsset asset)
        {

            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                        keyId,
                        contentKey,
                        "ContentKey",
                        ContentKeyType.CommonEncryption);

            // Associate the key with the asset.
            asset.ContentKeys.Add(key);

            return key;
        }

        static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
        {

            // Create ContentKeyAuthorizationPolicy with Open restrictions
            // and create authorization policy          

            List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                {
                new ContentKeyAuthorizationPolicyRestriction
                {
                    Name = "Open",
                    KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
                    Requirements = null
                }
                };

            // Configure PlayReady and Widevine license templates.
            string PlayReadyLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

            string WidevineLicenseTemplate = ConfigureWidevineLicenseTemplate();

            IContentKeyAuthorizationPolicyOption PlayReadyPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
                ContentKeyDeliveryType.PlayReadyLicense,
                restrictions, PlayReadyLicenseTemplate);

            IContentKeyAuthorizationPolicyOption WidevinePolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
                ContentKeyDeliveryType.Widevine,
                restrictions, WidevineLicenseTemplate);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common Content Key with no restrictions").
                Result;


            contentKeyAuthorizationPolicy.Options.Add(PlayReadyPolicy);
            contentKeyAuthorizationPolicy.Options.Add(WidevinePolicy);
            // Associate the content key authorization policy with the content key.
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;
        }

        public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
        {
            string tokenTemplateString = GenerateTokenRequirements();

            List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                {
                new ContentKeyAuthorizationPolicyRestriction
                {
                    Name = "Token Authorization Policy",
                    KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                    Requirements = tokenTemplateString,
                }
                };

            // Configure PlayReady and Widevine license templates.
            string PlayReadyLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

            string WidevineLicenseTemplate = ConfigureWidevineLicenseTemplate();

            IContentKeyAuthorizationPolicyOption PlayReadyPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                ContentKeyDeliveryType.PlayReadyLicense,
                restrictions, PlayReadyLicenseTemplate);

            IContentKeyAuthorizationPolicyOption WidevinePolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                ContentKeyDeliveryType.Widevine,
                restrictions, WidevineLicenseTemplate);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common Content Key with token restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(PlayReadyPolicy);
            contentKeyAuthorizationPolicy.Options.Add(WidevinePolicy);

            // Associate the content key authorization policy with the content key
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;

            return tokenTemplateString;
        }

        static private string GenerateTokenRequirements()
        {
            TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);

            template.PrimaryVerificationKey = new SymmetricVerificationKey();
            template.AlternateVerificationKeys.Add(new SymmetricVerificationKey());
            template.Audience = _sampleAudience.ToString();
            template.Issuer = _sampleIssuer.ToString();
            template.RequiredClaims.Add(TokenClaim.ContentKeyIdentifierClaim);

            return TokenRestrictionTemplateSerializer.Serialize(template);
        }

        static private string ConfigurePlayReadyLicenseTemplate()
        {
            // The following code configures PlayReady License Template using .NET classes
            // and returns the XML string.

            //The PlayReadyLicenseResponseTemplate class represents the template for the response sent back to the end user.
            //It contains a field for a custom data string between the license server and the application
            //(may be useful for custom app logic) as well as a list of one or more license templates.
            PlayReadyLicenseResponseTemplate responseTemplate = new PlayReadyLicenseResponseTemplate();

            // The PlayReadyLicenseTemplate class represents a license template for creating PlayReady licenses
            // to be returned to the end users.
            //It contains the data on the content key in the license and any rights or restrictions to be
            //enforced by the PlayReady DRM runtime when using the content key.
            PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();
            //Configure whether the license is persistent (saved in persistent storage on the client)
            //or non-persistent (only held in memory while the player is using the license).  
            licenseTemplate.LicenseType = PlayReadyLicenseType.Nonpersistent;

            // AllowTestDevices controls whether test devices can use the license or not.  
            // If true, the MinimumSecurityLevel property of the license
            // is set to 150.  If false (the default), the MinimumSecurityLevel property of the license is set to 2000.
            licenseTemplate.AllowTestDevices = true;

            // You can also configure the Play Right in the PlayReady license by using the PlayReadyPlayRight class.
            // It grants the user the ability to playback the content subject to the zero or more restrictions
            // configured in the license and on the PlayRight itself (for playback specific policy).
            // Much of the policy on the PlayRight has to do with output restrictions
            // which control the types of outputs that the content can be played over and
            // any restrictions that must be put in place when using a given output.
            // For example, if the DigitalVideoOnlyContentRestriction is enabled,
            //then the DRM runtime will only allow the video to be displayed over digital outputs
            //(analog video outputs won’t be allowed to pass the content).

            //IMPORTANT: These types of restrictions can be very powerful but can also affect the consumer experience.
            // If the output protections are configured too restrictive,
            // the content might be unplayable on some clients. For more information, see the PlayReady Compliance Rules document.

            // For example:
            //licenseTemplate.PlayRight.AgcAndColorStripeRestriction = new AgcAndColorStripeRestriction(1);

            responseTemplate.LicenseTemplates.Add(licenseTemplate);

            return MediaServicesLicenseTemplateSerializer.Serialize(responseTemplate);
        }

        private static string ConfigureWidevineLicenseTemplate()
        {
            var template = new WidevineMessage
            {
            allowed_track_types = AllowedTrackTypes.SD_HD,
            content_key_specs = new[]
            {
                    new ContentKeySpecs
                    {
                    required_output_protection = new RequiredOutputProtection { hdcp = Hdcp.HDCP_NONE},
                    security_level = 1,
                    track_type = "SD"
                    }
                },
            policy_overrides = new
            {
                can_play = true,
                can_persist = true,
                can_renew = false
            }
            };

            string configuration = JsonConvert.SerializeObject(template);
            return configuration;
        }

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            // Get the PlayReady license service URL.
            Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);

            // GetKeyDeliveryUrl for Widevine attaches the KID to the URL.
            // For example: https://amsaccount1.keydelivery.mediaservices.windows.net/Widevine/?KID=268a6dcb-18c8-4648-8c95-f46429e4927c.  
            // The WidevineBaseLicenseAcquisitionUrl (used below) also tells Dynamaic Encryption
            // to append /? KID =< keyId > to the end of the url when creating the manifest.
            // As a result Widevine license acquisition URL will have KID appended twice,
            // so we need to remove the KID that in the URL when we call GetKeyDeliveryUrl.

            Uri widevineUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.Widevine);
            UriBuilder uriBuilder = new UriBuilder(widevineUrl);
            uriBuilder.Query = String.Empty;
            widevineUrl = uriBuilder.Uri;

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                    {AssetDeliveryPolicyConfigurationKey.PlayReadyLicenseAcquisitionUrl, acquisitionUrl.ToString()},
                    {AssetDeliveryPolicyConfigurationKey.WidevineBaseLicenseAcquisitionUrl, widevineUrl.ToString()}

            };

            // In this case we only specify Dash streaming protocol in the delivery policy,
            // All other protocols will be blocked from streaming.
            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryption,
            AssetDeliveryProtocol.Dash,
            assetDeliveryPolicyConfiguration);


            // Add AssetDelivery Policy to the asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        }

        /// <summary>
        /// Gets the streaming origin locator.
        /// </summary>
        /// <param name="assets"></param>
        /// <returns></returns>
        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference to the streaming manifest file from the  
            // collection of files in the asset.

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                         EndsWith(".ism")).
                         FirstOrDefault();

            // Create a 30-day readonly access policy.
            IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

            // Create a locator to the streaming content on an origin.
            ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

            // Create a URL to the manifest file.
            return originLocator.Path + assetFile.Name;
        }

        static private void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine(string.Format("{0}\n  State: {1}\n  Time: {2}\n\n",
            ((IJob)sender).Name,
            e.CurrentState,
            DateTime.UtcNow.ToString(@"yyyy_M_d__hh_mm_ss")));
        }

        static private byte[] GetRandomBuffer(int length)
        {
            var returnValue = new byte[length];

            using (var rng =
            new System.Security.Cryptography.RNGCryptoServiceProvider())
            {
            rng.GetBytes(returnValue);
            }

            return returnValue;
        }
        }
    }


## <a name="next-step"></a><span data-ttu-id="0fdb4-203">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="0fdb4-203">Next step</span></span>
<span data-ttu-id="0fdb4-204">Consultez les parcours d’apprentissage de Media Services.</span><span class="sxs-lookup"><span data-stu-id="0fdb4-204">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="0fdb4-205">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="0fdb4-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="0fdb4-206">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="0fdb4-206">See also</span></span>
[<span data-ttu-id="0fdb4-207">CENC avec Multi-DRM et Access Control</span><span class="sxs-lookup"><span data-stu-id="0fdb4-207">CENC with Multi-DRM and Access Control</span></span>](media-services-cenc-with-multidrm-access-control.md)

[<span data-ttu-id="0fdb4-208">Configurer l’empaquetage Widevine avec AMS</span><span class="sxs-lookup"><span data-stu-id="0fdb4-208">Configure Widevine packaging with AMS</span></span>](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services)

[<span data-ttu-id="0fdb4-209">Annonce des services de distribution de licence Google Widevine dans Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="0fdb4-209">Announcing Google Widevine license delivery services in Azure Media Services</span></span>](https://azure.microsoft.com/blog/announcing-general-availability-of-google-widevine-license-services/)
