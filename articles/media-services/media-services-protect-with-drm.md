---
title: aaaUsing PlayReady et/ou Widevine dynamique chiffrement commun | Documents Microsoft
description: "Microsoft Azure Media Services permet de vous toodeliver MPEG-DASH, Smooth Streaming et Http-Live-Streaming (HLS) flux protégés par Microsoft PlayReady DRM. Il vous permet également de toodelivery DASH chiffré avec Widevine DRM. Cette rubrique montre comment toodynamically chiffrer avec PlayReady et Widevine DRM."
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
ms.openlocfilehash: 0475e6ec80dcf39eb4e5c4ad4d17f821502951bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-playready-andor-widevine-dynamic-common-encryption"></a><span data-ttu-id="a20c2-105">Utilisation du chiffrement commun dynamique PlayReady et/ou Widevine</span><span class="sxs-lookup"><span data-stu-id="a20c2-105">Using PlayReady and/or Widevine dynamic common encryption</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a20c2-106">.NET</span><span class="sxs-lookup"><span data-stu-id="a20c2-106">.NET</span></span>](media-services-protect-with-drm.md)
> * [<span data-ttu-id="a20c2-107">Java</span><span class="sxs-lookup"><span data-stu-id="a20c2-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="a20c2-108">PHP</span><span class="sxs-lookup"><span data-stu-id="a20c2-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
>
>

<span data-ttu-id="a20c2-109">Microsoft Azure Media Services vous permet de toodeliver MPEG-DASH, Smooth Streaming et les flux HTTP Live Streaming (HLS) protégés avec [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span><span class="sxs-lookup"><span data-stu-id="a20c2-109">Microsoft Azure Media Services enables you toodeliver MPEG-DASH, Smooth Streaming, and HTTP-Live-Streaming (HLS) streams protected with [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span></span> <span data-ttu-id="a20c2-110">Il vous permet également de flux de tiret toodeliver chiffré avec licences Widevine DRM.</span><span class="sxs-lookup"><span data-stu-id="a20c2-110">It also enables you toodeliver encrypted DASH streams with Widevine DRM licenses.</span></span> <span data-ttu-id="a20c2-111">PlayReady et Widevine sont chiffrées par hello spécification de chiffrement commun (CENC 23001-7 de norme ISO/IEC).</span><span class="sxs-lookup"><span data-stu-id="a20c2-111">Both PlayReady and Widevine are encrypted per hello Common Encryption (ISO/IEC 23001-7 CENC) specification.</span></span> <span data-ttu-id="a20c2-112">Vous pouvez utiliser [AMS .NET SDK](https://www.nuget.org/packages/windowsazure.mediaservices/) (depuis la version de hello 3.5.1) ou REST API tooconfigure votre toouse AssetDeliveryConfiguration Widevine.</span><span class="sxs-lookup"><span data-stu-id="a20c2-112">You can use [AMS .NET SDK](https://www.nuget.org/packages/windowsazure.mediaservices/) (starting with hello version 3.5.1) or REST API tooconfigure your AssetDeliveryConfiguration toouse Widevine.</span></span>

<span data-ttu-id="a20c2-113">Media Services fournit un service de remise de licences DRM PlayReady et Widevine.</span><span class="sxs-lookup"><span data-stu-id="a20c2-113">Media Services provides a service for delivering PlayReady and Widevine DRM licenses.</span></span> <span data-ttu-id="a20c2-114">Media Services fournit également des API qui vous permettent de configurer les droits hello et restrictions que vous souhaitez pour hello PlayReady ou Widevine DRM runtime tooenforce lorsqu’un utilisateur lit le contenu protégé.</span><span class="sxs-lookup"><span data-stu-id="a20c2-114">Media Services also provides APIs that let you configure hello rights and restrictions that you want for hello PlayReady or Widevine DRM runtime tooenforce when a user plays back protected content.</span></span> <span data-ttu-id="a20c2-115">Lorsqu’un utilisateur demande un contenu protégé par DRM, application de lecteur hello demande une licence de service de licence hello AMS.</span><span class="sxs-lookup"><span data-stu-id="a20c2-115">When a user requests a DRM protected content, hello player application will request a license from hello AMS license service.</span></span> <span data-ttu-id="a20c2-116">service de licence Hello AMS émettra un lecteur toohello de licence s’il est autorisé.</span><span class="sxs-lookup"><span data-stu-id="a20c2-116">hello AMS license service will issue a license toohello player if it is authorized.</span></span> <span data-ttu-id="a20c2-117">Une licence PlayReady ou Widevine contient la clé de déchiffrement hello qui peut être utilisé par hello client toodecrypt et flux hello contenu du lecteur.</span><span class="sxs-lookup"><span data-stu-id="a20c2-117">A PlayReady or Widevine license contains hello decryption key that can be used by hello client player toodecrypt and stream hello content.</span></span>

<span data-ttu-id="a20c2-118">Vous pouvez également utiliser hello suivant toohelp de partenaires AMS vous fournir des licences Widevine : [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span><span class="sxs-lookup"><span data-stu-id="a20c2-118">You can also use hello following AMS partners toohelp you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span> <span data-ttu-id="a20c2-119">Pour plus d’informations, consultez : Intégration à [Axinom](media-services-axinom-integration.md) et [castLabs](media-services-castlabs-integration.md).</span><span class="sxs-lookup"><span data-stu-id="a20c2-119">For more information, see: integration with [Axinom](media-services-axinom-integration.md) and [castLabs](media-services-castlabs-integration.md).</span></span>

<span data-ttu-id="a20c2-120">Media Services prend en charge plusieurs méthodes d’autorisation des utilisateurs effectuant des demandes de clé.</span><span class="sxs-lookup"><span data-stu-id="a20c2-120">Media Services supports multiple ways of authorizing users who make key requests.</span></span> <span data-ttu-id="a20c2-121">Hello contenu clé peut avoir une ou plusieurs restrictions d’autorisation : ouvrir ou de restriction de jeton.</span><span class="sxs-lookup"><span data-stu-id="a20c2-121">hello content key authorization policy could have one or more authorization restrictions: open or token restriction.</span></span> <span data-ttu-id="a20c2-122">stratégie de restriction token Hello doit être accompagné d’un jeton émis par un Service (jeton de sécurité).</span><span class="sxs-lookup"><span data-stu-id="a20c2-122">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="a20c2-123">Media Services prend en charge les jetons Bonjour [des jetons Web simples](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) format de (SWT) et [jeton Web JSON](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) format (JWT).</span><span class="sxs-lookup"><span data-stu-id="a20c2-123">Media Services supports tokens in hello [Simple Web Tokens](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) (SWT) format and [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JWT) format.</span></span> <span data-ttu-id="a20c2-124">Pour plus d’informations, consultez la stratégie d’autorisation de configurer hello de clé du contenu.</span><span class="sxs-lookup"><span data-stu-id="a20c2-124">For more information, see Configure hello content key’s authorization policy.</span></span>

<span data-ttu-id="a20c2-125">tootake parti du chiffrement dynamique, vous devez toohave une ressource qui contient un ensemble de fichiers MP4 à plusieurs débits ou des fichiers sources de diffusion en continu lisse débits.</span><span class="sxs-lookup"><span data-stu-id="a20c2-125">tootake advantage of dynamic encryption, you need toohave an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="a20c2-126">Vous devez également les stratégies de remise tooconfigure hello pour un composant hello (décrite plus loin dans cette rubrique).</span><span class="sxs-lookup"><span data-stu-id="a20c2-126">You also need tooconfigure hello delivery policies for hello asset (described later in this topic).</span></span> <span data-ttu-id="a20c2-127">Ensuite, selon le format de hello spécifié dans l’URL de diffusion en continu de hello, serveur de diffusion en continu à la demande de hello s’assure que ce flux de données hello est remis dans le protocole hello que vous avez choisi.</span><span class="sxs-lookup"><span data-stu-id="a20c2-127">Then, based on hello format specified in hello streaming URL, hello On-Demand Streaming server will ensure that hello stream is delivered in hello protocol you have chosen.</span></span> <span data-ttu-id="a20c2-128">Par conséquent, vous devez uniquement toostore et payer pour les fichiers hello dans un seul format de stockage et les Services de support crée et fournit la réponse HTTP approprié de hello, en fonction de chaque demande d’un client.</span><span class="sxs-lookup"><span data-stu-id="a20c2-128">As a result, you only need toostore and pay for hello files in a single storage format and Media Services will build and serve hello appropriate HTTP response based on each request from a client.</span></span>

<span data-ttu-id="a20c2-129">Cette rubrique serait utile toodevelopers qui fonctionnent sur les applications qui fournissent du support protégé avec plusieurs DRMs, tels que PlayReady et Widevine.</span><span class="sxs-lookup"><span data-stu-id="a20c2-129">This topic would be useful toodevelopers that work on applications that deliver media protected with multiple DRMs, such as PlayReady and Widevine.</span></span> <span data-ttu-id="a20c2-130">rubrique de Hello vous montre comment tooconfigure hello service de fourniture de licence PlayReady avec les stratégies d’autorisation afin que seuls les clients autorisés puissent recevoir des licences PlayReady ou Widevine.</span><span class="sxs-lookup"><span data-stu-id="a20c2-130">hello topic shows you how tooconfigure hello PlayReady license delivery service with authorization policies so that only authorized clients could receive PlayReady or Widevine licenses.</span></span> <span data-ttu-id="a20c2-131">Il montre également comment le chiffrement de chiffrement dynamique toouse avec PlayReady ou DRM Widevine sur tiret.</span><span class="sxs-lookup"><span data-stu-id="a20c2-131">It also shows how toouse dynamic encryption encryption with PlayReady or Widevine DRM over DASH.</span></span>

>[!NOTE]
><span data-ttu-id="a20c2-132">Création de votre compte AMS un **par défaut** point de terminaison de diffusion en continu est ajoutée tooyour compte Bonjour **arrêté** état.</span><span class="sxs-lookup"><span data-stu-id="a20c2-132">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="a20c2-133">toostart de diffusion en continu de votre contenu et profitez de l’empaquetage dynamique et chiffrement dynamique, hello de point de terminaison de diffusion en continu à partir de laquelle vous souhaitez que le contenu toostream a toobe Bonjour **en cours d’exécution** état.</span><span class="sxs-lookup"><span data-stu-id="a20c2-133">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 

## <a name="download-sample"></a><span data-ttu-id="a20c2-134">Charger l’exemple</span><span class="sxs-lookup"><span data-stu-id="a20c2-134">Download sample</span></span>
<span data-ttu-id="a20c2-135">Vous pouvez télécharger des exemple hello décrit dans cet article à partir de [ici](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-drm).</span><span class="sxs-lookup"><span data-stu-id="a20c2-135">You can download hello sample described in this article from [here](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-drm).</span></span>

## <a name="configuring-dynamic-common-encryption-and-drm-license-delivery-services"></a><span data-ttu-id="a20c2-136">Configuration de Dynamic Common Encryption et services de distribution de licences DRM</span><span class="sxs-lookup"><span data-stu-id="a20c2-136">Configuring Dynamic Common Encryption and DRM License Delivery Services</span></span>

<span data-ttu-id="a20c2-137">Hello Voici les étapes générales que vous devez tooperform lors de la protection de vos éléments multimédias avec PlayReady, à l’aide du service de remise de licences de Media Services hello et utiliser le chiffrement dynamique.</span><span class="sxs-lookup"><span data-stu-id="a20c2-137">hello following are general steps that you would need tooperform when protecting your assets with PlayReady, using hello Media Services license delivery service, and also using dynamic encryption.</span></span>

1. <span data-ttu-id="a20c2-138">Créer un élément multimédia et télécharger des fichiers dans l’élément multimédia de hello.</span><span class="sxs-lookup"><span data-stu-id="a20c2-138">Create an asset and upload files into hello asset.</span></span>
2. <span data-ttu-id="a20c2-139">Encoder hello asset contenant hello fichier toohello ensemble à débit adaptatif MP4.</span><span class="sxs-lookup"><span data-stu-id="a20c2-139">Encode hello asset containing hello file toohello adaptive bitrate MP4 set.</span></span>
3. <span data-ttu-id="a20c2-140">Créer une clé de contenu et l’associer à asset de hello encodé.</span><span class="sxs-lookup"><span data-stu-id="a20c2-140">Create a content key and associate it with hello encoded asset.</span></span> <span data-ttu-id="a20c2-141">Dans Media Services, clé de contenu hello contient la clé de chiffrement de l’élément multimédia hello.</span><span class="sxs-lookup"><span data-stu-id="a20c2-141">In Media Services, hello content key contains hello asset’s encryption key.</span></span>
4. <span data-ttu-id="a20c2-142">Configurez la stratégie d’autorisation de la clé de contenu hello.</span><span class="sxs-lookup"><span data-stu-id="a20c2-142">Configure hello content key’s authorization policy.</span></span> <span data-ttu-id="a20c2-143">stratégie d’autorisation de clé contenu de Hello doit être configurée par vous et remplie par client hello pour hello toobe clé contenu livré toohello client.</span><span class="sxs-lookup"><span data-stu-id="a20c2-143">hello content key authorization policy must be configured by you and met by hello client in order for hello content key toobe delivered toohello client.</span></span>

    <span data-ttu-id="a20c2-144">Lorsque vous créez la stratégie d’autorisation de clé contenu de hello, toospecify, hello éléments suivants sont nécessaires : (méthode) (PlayReady ou Widevine), restrictions de remise (ouvertes ou jeton) et le type de distribution de clés de toohello spécifique d’informations qui définit le mode de remise de clé de hello client de toohello ([PlayReady](media-services-playready-license-template-overview.md) ou [Widevine](media-services-widevine-license-template-overview.md) modèle de licence).</span><span class="sxs-lookup"><span data-stu-id="a20c2-144">When creating hello content key authorization policy, you need toospecify hello following: delivery method (PlayReady or Widevine), restrictions (open or token), and information specific toohello key delivery type that defines how hello key is delivered toohello client ([PlayReady](media-services-playready-license-template-overview.md) or [Widevine](media-services-widevine-license-template-overview.md) license template).</span></span>

5. <span data-ttu-id="a20c2-145">Configurer la stratégie de livraison de hello pour un élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="a20c2-145">Configure hello delivery policy for an asset.</span></span> <span data-ttu-id="a20c2-146">configuration de la stratégie Hello livraison inclut : protocole de remise (par exemple, MPEG DASH, HLS, Smooth Streaming ou tous), hello type de chiffrement dynamique (par exemple, chiffrement commun), PlayReady ou l’URL d’acquisition de licences Widevine.</span><span class="sxs-lookup"><span data-stu-id="a20c2-146">hello delivery policy configuration includes: delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all), hello type of dynamic encryption (for example, Common Encryption), PlayReady or Widevine license acquisition URL.</span></span>

    <span data-ttu-id="a20c2-147">Vous pouvez appliquer le protocole de tooeach stratégie différente sur hello même actif.</span><span class="sxs-lookup"><span data-stu-id="a20c2-147">You could apply different policy tooeach protocol on hello same asset.</span></span> <span data-ttu-id="a20c2-148">Par exemple, vous pouvez appliquer tooSmooth de chiffrement PlayReady/DASH et tooHLS d’enveloppe AES.</span><span class="sxs-lookup"><span data-stu-id="a20c2-148">For example, you could apply PlayReady encryption tooSmooth/DASH and AES Envelope tooHLS.</span></span> <span data-ttu-id="a20c2-149">Tous les protocoles qui ne sont pas définis dans une stratégie de remise (par exemple, vous ajoutez une stratégie unique qui spécifie seulement le HLS en tant que protocole de hello) sera bloquée à partir de la diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="a20c2-149">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as hello protocol) will be blocked from streaming.</span></span> <span data-ttu-id="a20c2-150">Hello exception toothis est si vous ne disposez d’aucune stratégie de remise actif du tout défini.</span><span class="sxs-lookup"><span data-stu-id="a20c2-150">hello exception toothis is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="a20c2-151">Ensuite, tous les protocoles seront autorisés en hello clair.</span><span class="sxs-lookup"><span data-stu-id="a20c2-151">Then, all protocols will be allowed in hello clear.</span></span>

6. <span data-ttu-id="a20c2-152">Créer un localisateur OnDemand dans l’ordre tooget une URL de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="a20c2-152">Create an OnDemand locator in order tooget a streaming URL.</span></span>

<span data-ttu-id="a20c2-153">Vous trouverez un exemple complet de .NET à fin hello de rubrique de hello.</span><span class="sxs-lookup"><span data-stu-id="a20c2-153">You will find a complete .NET example at hello end of hello topic.</span></span>

<span data-ttu-id="a20c2-154">Hello suivant image montre workflow hello décrit ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="a20c2-154">hello following image demonstrates hello workflow described above.</span></span> <span data-ttu-id="a20c2-155">Ici, le jeton de hello est utilisé pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="a20c2-155">Here hello token is used for authentication.</span></span>

![Protéger avec PlayReady](./media/media-services-content-protection-overview/media-services-content-protection-with-drm.png)

<span data-ttu-id="a20c2-157">reste Hello de cette rubrique fournit des explications détaillées, des exemples de code et tootopics des liens qui vous montrent comment tooachieve hello les tâches décrites ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="a20c2-157">hello rest of this topic provides detailed explanations, code examples, and links tootopics that show you how tooachieve hello tasks described above.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="a20c2-158">Limitations actuelles</span><span class="sxs-lookup"><span data-stu-id="a20c2-158">Current limitations</span></span>
<span data-ttu-id="a20c2-159">Si vous ajoutez ou mettez à jour une stratégie de remise asset, vous devez supprimer le localisateur de hello associé (le cas échéant) et créer un nouveau.</span><span class="sxs-lookup"><span data-stu-id="a20c2-159">If you add or update an asset delivery policy, you must delete hello associated locator (if any) and create a new locator.</span></span>

<span data-ttu-id="a20c2-160">Limites lors du chiffrement Widevine avec Azure Media Services : actuellement, plusieurs clés de contenu ne sont pas prises en charge.</span><span class="sxs-lookup"><span data-stu-id="a20c2-160">Limitation when encrypting with Widevine with Azure Media Services: currently, multiple content keys are not supported.</span></span>

## <a name="create-an-asset-and-upload-files-into-hello-asset"></a><span data-ttu-id="a20c2-161">Créer un élément multimédia et télécharger des fichiers dans l’élément multimédia de hello</span><span class="sxs-lookup"><span data-stu-id="a20c2-161">Create an asset and upload files into hello asset</span></span>
<span data-ttu-id="a20c2-162">Dans l’ordre toomanage, encoder et diffuser en continu vos vidéos, vous devez d’abord télécharger votre contenu dans Microsoft Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="a20c2-162">In order toomanage, encode, and stream your videos, you must first upload your content into Microsoft Azure Media Services.</span></span> <span data-ttu-id="a20c2-163">Une fois téléchargé, votre contenu est stocké en toute sécurité dans le cloud hello pour poursuivre le traitement et la diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="a20c2-163">Once uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span>

<span data-ttu-id="a20c2-164">Pour plus d’informations, consultez [Charger des fichiers vers un compte Media Services](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="a20c2-164">For detailed information, see [Upload Files into a Media Services account](media-services-dotnet-upload-files.md).</span></span>

## <a name="encode-hello-asset-containing-hello-file-toohello-adaptive-bitrate-mp4-set"></a><span data-ttu-id="a20c2-165">Encoder hello asset contenant hello fichier toohello ensemble à débit adaptatif MP4</span><span class="sxs-lookup"><span data-stu-id="a20c2-165">Encode hello asset containing hello file toohello adaptive bitrate MP4 set</span></span>
<span data-ttu-id="a20c2-166">Avec le chiffrement dynamique, il vous suffit de toocreate un élément multimédia contenant un ensemble de fichiers MP4 à plusieurs débits ou des fichiers sources de diffusion en continu lisse débits.</span><span class="sxs-lookup"><span data-stu-id="a20c2-166">With dynamic encryption all you need is toocreate an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="a20c2-167">Ensuite, en fonction hello le format spécifié dans le manifeste de hello et demande de fragment, hello à la demande de diffusion en continu serveur garantit que vous recevez des flux de hello protocole hello que vous avez choisi.</span><span class="sxs-lookup"><span data-stu-id="a20c2-167">Then, based on hello specified format in hello manifest and fragment request, hello On-Demand Streaming server will ensure that you receive hello stream in hello protocol you have chosen.</span></span> <span data-ttu-id="a20c2-168">Par conséquent, vous devez uniquement toostore et payer pour les fichiers hello dans un seul format de stockage et le service Media Services pour la génération et fournit hello de réponse appropriée en fonction des demandes d’un client.</span><span class="sxs-lookup"><span data-stu-id="a20c2-168">As a result, you only need toostore and pay for hello files in single storage format and Media Services service will build and serve hello appropriate response based on requests from a client.</span></span> <span data-ttu-id="a20c2-169">Pour plus d’informations, consultez hello [présentation de la mise en package dynamique](media-services-dynamic-packaging-overview.md) rubrique.</span><span class="sxs-lookup"><span data-stu-id="a20c2-169">For more information, see hello [Dynamic Packaging Overview](media-services-dynamic-packaging-overview.md) topic.</span></span>

<span data-ttu-id="a20c2-170">Pour obtenir des instructions sur la façon de tooencode, consultez [comment tooencode un élément multimédia à l’aide de Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).</span><span class="sxs-lookup"><span data-stu-id="a20c2-170">For instructions on how tooencode, see [How tooencode an asset using Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).</span></span>

## <span data-ttu-id="a20c2-171"><a id="create_contentkey"></a>Créer une clé de contenu et l’associer à asset de hello codée</span><span class="sxs-lookup"><span data-stu-id="a20c2-171"><a id="create_contentkey"></a>Create a content key and associate it with hello encoded asset</span></span>
<span data-ttu-id="a20c2-172">Dans Media Services, clé de contenu hello contient la clé hello que vous souhaitez tooencrypt un élément multimédia avec.</span><span class="sxs-lookup"><span data-stu-id="a20c2-172">In Media Services, hello content key contains hello key that you want tooencrypt an asset with.</span></span>

<span data-ttu-id="a20c2-173">Pour plus d’informations, consultez [Créer une clé de contenu](media-services-dotnet-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="a20c2-173">For detailed information, see [Create content key](media-services-dotnet-create-contentkey.md).</span></span>

## <span data-ttu-id="a20c2-174"><a id="configure_key_auth_policy"></a>Configurer la stratégie d’autorisation de clé de contenu hello</span><span class="sxs-lookup"><span data-stu-id="a20c2-174"><a id="configure_key_auth_policy"></a>Configure hello content key’s authorization policy</span></span>
<span data-ttu-id="a20c2-175">Media Services prend en charge plusieurs méthodes d’authentification des utilisateurs effectuant des demandes de clé.</span><span class="sxs-lookup"><span data-stu-id="a20c2-175">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="a20c2-176">stratégie d’autorisation de clé contenu de Hello doit être configurée par vous et remplie par le client hello (lecteur) afin que les toobe clé hello remis toohello client.</span><span class="sxs-lookup"><span data-stu-id="a20c2-176">hello content key authorization policy must be configured by you and met by hello client (player) in order for hello key toobe delivered toohello client.</span></span> <span data-ttu-id="a20c2-177">Hello contenu clé peut avoir une ou plusieurs restrictions d’autorisation : ouvrir ou de restriction de jeton.</span><span class="sxs-lookup"><span data-stu-id="a20c2-177">hello content key authorization policy could have one or more authorization restrictions: open or token restriction.</span></span>

<span data-ttu-id="a20c2-178">Pour plus d’informations, consultez [Configurer la stratégie d’autorisation de clé de contenu](media-services-dotnet-configure-content-key-auth-policy.md#playready-dynamic-encryption).</span><span class="sxs-lookup"><span data-stu-id="a20c2-178">For detailed information, see [Configure Content Key Authorization Policy](media-services-dotnet-configure-content-key-auth-policy.md#playready-dynamic-encryption).</span></span>

## <span data-ttu-id="a20c2-179"><a id="configure_asset_delivery_policy"></a>Configurer la stratégie de distribution d’éléments multimédia</span><span class="sxs-lookup"><span data-stu-id="a20c2-179"><a id="configure_asset_delivery_policy"></a>Configure asset delivery policy</span></span>
<span data-ttu-id="a20c2-180">Configurer la stratégie de livraison de hello pour votre élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="a20c2-180">Configure hello delivery policy for your asset.</span></span> <span data-ttu-id="a20c2-181">Les éléments qui hello configuration actif de la stratégie de livraison inclut :</span><span class="sxs-lookup"><span data-stu-id="a20c2-181">Some things that hello asset delivery policy configuration includes:</span></span>

* <span data-ttu-id="a20c2-182">URL d’acquisition de licence DRM Hello.</span><span class="sxs-lookup"><span data-stu-id="a20c2-182">hello DRM license acquisition URL.</span></span>
* <span data-ttu-id="a20c2-183">protocole de la livraison d’asset Hello (par exemple, MPEG DASH, HLS, Smooth Streaming ou tous).</span><span class="sxs-lookup"><span data-stu-id="a20c2-183">hello asset delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all).</span></span>
* <span data-ttu-id="a20c2-184">type Hello du chiffrement dynamique (dans ce cas, le chiffrement commun).</span><span class="sxs-lookup"><span data-stu-id="a20c2-184">hello type of dynamic encryption (in this case, Common Encryption).</span></span>

<span data-ttu-id="a20c2-185">Pour plus d’informations, consultez [Configurer la stratégie de distribution d’éléments multimédia ](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="a20c2-185">For detailed information, see [Configure asset delivery policy ](media-services-rest-configure-asset-delivery-policy.md).</span></span>

## <span data-ttu-id="a20c2-186"><a id="create_locator"></a>Créer une recherche dans l’ordre tooget une URL de diffusion en continu de diffusion en continu à la demande</span><span class="sxs-lookup"><span data-stu-id="a20c2-186"><a id="create_locator"></a>Create an OnDemand streaming locator in order tooget a streaming URL</span></span>
<span data-ttu-id="a20c2-187">Vous devez tooprovide votre utilisateur avec hello URL pour Smooth, DASH ou HLS de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="a20c2-187">You will need tooprovide your user with hello streaming URL for Smooth, DASH or HLS.</span></span>

> [!NOTE]
> <span data-ttu-id="a20c2-188">Si vous ajoutez ou mettez à jour la stratégie de remise de votre ressource, vous devez supprimer le localisateur existant (le cas échéant) et en créer un nouveau.</span><span class="sxs-lookup"><span data-stu-id="a20c2-188">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
>
>

<span data-ttu-id="a20c2-189">Pour plus d’informations sur comment toopublish un élément multimédia et créer une URL de diffusion en continu, consultez [générer une URL de diffusion en continu](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="a20c2-189">For instructions on how toopublish an asset and build a streaming URL, see [Build a streaming URL](media-services-deliver-streaming-content.md).</span></span>

## <a name="get-a-test-token"></a><span data-ttu-id="a20c2-190">Obtenir un test de jeton</span><span class="sxs-lookup"><span data-stu-id="a20c2-190">Get a test token</span></span>
<span data-ttu-id="a20c2-191">Obtenez un test de jeton basé sur la restriction de type hello token qui a été utilisée pour la stratégie d’autorisation de clé de hello.</span><span class="sxs-lookup"><span data-stu-id="a20c2-191">Get a test token based on hello token restriction that was used for hello key authorization policy.</span></span>

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate =
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on hello data in hello given TokenRestrictionTemplate.
    //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
    //so you have tooadd it in front of hello token string.
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate);
    Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);


<span data-ttu-id="a20c2-192">Vous pouvez utiliser hello [AMS lecteur](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tootest votre flux de données.</span><span class="sxs-lookup"><span data-stu-id="a20c2-192">You can use hello [AMS Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tootest your stream.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="a20c2-193">Créer et configurer un projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a20c2-193">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="a20c2-194">Configurer votre environnement de développement et de remplir le fichier app.config de hello avec les informations de connexion, comme décrit dans [développement Media Services avec .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="a20c2-194">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="a20c2-195">Ajouter hello suivant éléments trop**appSettings** défini dans votre fichier app.config :</span><span class="sxs-lookup"><span data-stu-id="a20c2-195">Add hello following elements too**appSettings** defined in your app.config file:</span></span>

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a><span data-ttu-id="a20c2-196">Exemple</span><span class="sxs-lookup"><span data-stu-id="a20c2-196">Example</span></span>

<span data-ttu-id="a20c2-197">Hello exemple suivant illustre la fonctionnalité qui a été introduite dans Azure Media Services SDK pour .net-Version 3.5.2 (plus précisément, hello capacité toodefine un Widevine modèle de licence et demande une licence Widevine à partir d’Azure Media Services).</span><span class="sxs-lookup"><span data-stu-id="a20c2-197">hello following sample demonstrates functionality that was introduced in Azure Media Services SDK for .Net -Version 3.5.2 (specifically, hello ability toodefine a Widevine license template and request a Widevine license from Azure Media Services).</span></span>

<span data-ttu-id="a20c2-198">Remplacer le code hello dans votre fichier Program.cs avec le code hello présenté dans cette section.</span><span class="sxs-lookup"><span data-stu-id="a20c2-198">Overwrite hello code in your Program.cs file with hello code shown in this section.</span></span>

>[!NOTE]
><span data-ttu-id="a20c2-199">Un nombre limite de 1 000 000 a été défini pour les différentes stratégies AMS (par exemple, pour la stratégie de localisateur ou pour ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="a20c2-199">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="a20c2-200">Vous devez utiliser hello ID de stratégie même si vous utilisez toujours hello même jours / autorisations d’accès, par exemple, les stratégies pour les localisateurs sont tooremain prévue en place pendant une longue période (non-téléchargement stratégies).</span><span class="sxs-lookup"><span data-stu-id="a20c2-200">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="a20c2-201">Pour plus d’informations, consultez [cette rubrique](media-services-dotnet-manage-entities.md#limit-access-policies) .</span><span class="sxs-lookup"><span data-stu-id="a20c2-201">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="a20c2-202">Assurez-vous que tooupdate variables toopoint toofolders où se trouvent vos fichiers d’entrée.</span><span class="sxs-lookup"><span data-stu-id="a20c2-202">Make sure tooupdate variables toopoint toofolders where your input files are located.</span></span>

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
        // Read values from hello App.config file.
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
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
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

            // Generate a test token based on hello hello data in hello given TokenRestrictionTemplate.
            // Note, you need toopass hello key id Guid because we specified
            // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey,
                                        DateTime.UtcNow.AddDays(365));
            Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            // You can use hello http://amsplayer.azurewebsites.net/azuremediaplayer.html player tootest streams.
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

            IJob job = _context.Jobs.Create(String.Format("Encoding into Mp4 {0} too{1}",
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

            // Associate hello key with hello asset.
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
            // Associate hello content key authorization policy with hello content key.
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

            // Associate hello content key authorization policy with hello content key
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
            // hello following code configures PlayReady License Template using .NET classes
            // and returns hello XML string.

            //hello PlayReadyLicenseResponseTemplate class represents hello template for hello response sent back toohello end user.
            //It contains a field for a custom data string between hello license server and hello application
            //(may be useful for custom app logic) as well as a list of one or more license templates.
            PlayReadyLicenseResponseTemplate responseTemplate = new PlayReadyLicenseResponseTemplate();

            // hello PlayReadyLicenseTemplate class represents a license template for creating PlayReady licenses
            // toobe returned toohello end users.
            //It contains hello data on hello content key in hello license and any rights or restrictions toobe
            //enforced by hello PlayReady DRM runtime when using hello content key.
            PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();
            //Configure whether hello license is persistent (saved in persistent storage on hello client)
            //or non-persistent (only held in memory while hello player is using hello license).  
            licenseTemplate.LicenseType = PlayReadyLicenseType.Nonpersistent;

            // AllowTestDevices controls whether test devices can use hello license or not.  
            // If true, hello MinimumSecurityLevel property of hello license
            // is set too150.  If false (hello default), hello MinimumSecurityLevel property of hello license is set too2000.
            licenseTemplate.AllowTestDevices = true;

            // You can also configure hello Play Right in hello PlayReady license by using hello PlayReadyPlayRight class.
            // It grants hello user hello ability tooplayback hello content subject toohello zero or more restrictions
            // configured in hello license and on hello PlayRight itself (for playback specific policy).
            // Much of hello policy on hello PlayRight has toodo with output restrictions
            // which control hello types of outputs that hello content can be played over and
            // any restrictions that must be put in place when using a given output.
            // For example, if hello DigitalVideoOnlyContentRestriction is enabled,
            //then hello DRM runtime will only allow hello video toobe displayed over digital outputs
            //(analog video outputs won’t be allowed toopass hello content).

            //IMPORTANT: These types of restrictions can be very powerful but can also affect hello consumer experience.
            // If hello output protections are configured too restrictive,
            // hello content might be unplayable on some clients. For more information, see hello PlayReady Compliance Rules document.

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
            // Get hello PlayReady license service URL.
            Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);

            // GetKeyDeliveryUrl for Widevine attaches hello KID toohello URL.
            // For example: https://amsaccount1.keydelivery.mediaservices.windows.net/Widevine/?KID=268a6dcb-18c8-4648-8c95-f46429e4927c.  
            // hello WidevineBaseLicenseAcquisitionUrl (used below) also tells Dynamaic Encryption
            // tooappend /? KID =< keyId > toohello end of hello url when creating hello manifest.
            // As a result Widevine license acquisition URL will have KID appended twice,
            // so we need tooremove hello KID that in hello URL when we call GetKeyDeliveryUrl.

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

            // In this case we only specify Dash streaming protocol in hello delivery policy,
            // All other protocols will be blocked from streaming.
            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryption,
            AssetDeliveryProtocol.Dash,
            assetDeliveryPolicyConfiguration);


            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        }

        /// <summary>
        /// Gets hello streaming origin locator.
        /// </summary>
        /// <param name="assets"></param>
        /// <returns></returns>
        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference toohello streaming manifest file from hello  
            // collection of files in hello asset.

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                         EndsWith(".ism")).
                         FirstOrDefault();

            // Create a 30-day readonly access policy.
            IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

            // Create a locator toohello streaming content on an origin.
            ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

            // Create a URL toohello manifest file.
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


## <a name="next-step"></a><span data-ttu-id="a20c2-203">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="a20c2-203">Next step</span></span>
<span data-ttu-id="a20c2-204">Consultez les parcours d’apprentissage de Media Services.</span><span class="sxs-lookup"><span data-stu-id="a20c2-204">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a20c2-205">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="a20c2-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="a20c2-206">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="a20c2-206">See also</span></span>
[<span data-ttu-id="a20c2-207">CENC avec Multi-DRM et Access Control</span><span class="sxs-lookup"><span data-stu-id="a20c2-207">CENC with Multi-DRM and Access Control</span></span>](media-services-cenc-with-multidrm-access-control.md)

[<span data-ttu-id="a20c2-208">Configurer l’empaquetage Widevine avec AMS</span><span class="sxs-lookup"><span data-stu-id="a20c2-208">Configure Widevine packaging with AMS</span></span>](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services)

[<span data-ttu-id="a20c2-209">Annonce des services de distribution de licence Google Widevine dans Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="a20c2-209">Announcing Google Widevine license delivery services in Azure Media Services</span></span>](https://azure.microsoft.com/blog/announcing-general-availability-of-google-widevine-license-services/)
