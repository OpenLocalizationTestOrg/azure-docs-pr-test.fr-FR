---
title: "Utilisation du chiffrement dynamique AES-128 et du service de distribution des clés | Microsoft Docs"
description: "Microsoft Azure Media Services vous permet de transmettre du contenu chiffré à l'aide de clés de chiffrement AES 128 bits. Media Services assure également le service de distribution des clés qui fournit des clés de chiffrement aux utilisateurs autorisés. Cette rubrique montre comment chiffrer dynamiquement avec AES-128 et utiliser le service de distribution des clés."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 4d2c10af-9ee0-408f-899b-33fa4c1d89b9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: juliako
ms.openlocfilehash: ae1b36c26e688e74eb8fcc1a4cdbd3be0c014c08
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="using-aes-128-dynamic-encryption-and-key-delivery-service"></a><span data-ttu-id="8301c-105">Utilisation du chiffrement dynamique AES-128 et du service de distribution des clés</span><span class="sxs-lookup"><span data-stu-id="8301c-105">Using AES-128 dynamic encryption and key delivery service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8301c-106">.NET</span><span class="sxs-lookup"><span data-stu-id="8301c-106">.NET</span></span>](media-services-protect-with-aes128.md)
> * [<span data-ttu-id="8301c-107">Java</span><span class="sxs-lookup"><span data-stu-id="8301c-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="8301c-108">PHP</span><span class="sxs-lookup"><span data-stu-id="8301c-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="8301c-109">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="8301c-109">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="8301c-110">Consultez [cette](https://channel9.msdn.com/Shows/Azure-Friday/Azure-Media-Services-Protecting-your-Media-Content-with-AES-Encryption) vidéo pour une vue d’ensemble sur la façon de protéger votre contenu multimédia avec le chiffrement AES.</span><span class="sxs-lookup"><span data-stu-id="8301c-110">See [this](https://channel9.msdn.com/Shows/Azure-Friday/Azure-Media-Services-Protecting-your-Media-Content-with-AES-Encryption) video for an overview of how to protect your Media Content with AES encryption.</span></span>
> 
> 

<span data-ttu-id="8301c-111">Microsoft Azure Media Services permet de transmettre du contenu HLS (Http-Live-Streaming) et des flux lisses (Smooth Streams) chiffrés avec la norme AES (Advanced Encryption Standard) (à l’aide de clés de chiffrement 128 bits).</span><span class="sxs-lookup"><span data-stu-id="8301c-111">Microsoft Azure Media Services enables you to deliver Http-Live-Streaming (HLS) and Smooth Streams encrypted with Advanced Encryption Standard (AES) (using 128-bit encryption keys).</span></span> <span data-ttu-id="8301c-112">Media Services assure également le service de distribution des clés qui fournit des clés de chiffrement aux utilisateurs autorisés.</span><span class="sxs-lookup"><span data-stu-id="8301c-112">Media Services also provides the Key Delivery service that delivers encryption keys to authorized users.</span></span> <span data-ttu-id="8301c-113">Si vous souhaitez que Media Services chiffre un élément multimédia, vous devez associer une clé de chiffrement à l'élément multimédia et configurer des stratégies d'autorisation pour la clé.</span><span class="sxs-lookup"><span data-stu-id="8301c-113">If you want for Media Services to encrypt an asset, you need to associate an encryption key with the asset and also configure authorization policies for the key.</span></span> <span data-ttu-id="8301c-114">Lorsqu’un lecteur demande un flux de données, Media Services utilise la clé spécifiée pour chiffrer dynamiquement votre contenu à l’aide du chiffrement AES.</span><span class="sxs-lookup"><span data-stu-id="8301c-114">When a stream is requested by a player, Media Services uses the specified key to dynamically encrypt your content using AES encryption.</span></span> <span data-ttu-id="8301c-115">Pour déchiffrer le flux de données, le lecteur demande la clé au service de remise de clé.</span><span class="sxs-lookup"><span data-stu-id="8301c-115">To decrypt the stream, the player will request the key from the key delivery service.</span></span> <span data-ttu-id="8301c-116">Pour déterminer si l’utilisateur est autorisé à obtenir la clé, le service évalue les stratégies d’autorisation que vous avez spécifiées pour la clé.</span><span class="sxs-lookup"><span data-stu-id="8301c-116">To decide whether or not the user is authorized to get the key, the service evaluates the authorization policies that you specified for the key.</span></span>

<span data-ttu-id="8301c-117">Media Services prend en charge plusieurs méthodes d’authentification des utilisateurs effectuant des demandes de clé.</span><span class="sxs-lookup"><span data-stu-id="8301c-117">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="8301c-118">La stratégie d’autorisation des clés de contenu peut comporter une ou plusieurs restrictions d’autorisation : ouverte ou restriction à jeton.</span><span class="sxs-lookup"><span data-stu-id="8301c-118">The content key authorization policy could have one or more authorization restrictions: open or token restriction.</span></span> <span data-ttu-id="8301c-119">La stratégie de restriction à jeton doit être accompagnée d’un jeton émis par un service de jeton sécurisé (STS).</span><span class="sxs-lookup"><span data-stu-id="8301c-119">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="8301c-120">Media Services prend en charge les jetons aux formats [SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) (Simple Web Tokens) et [JWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JSON Web Token).</span><span class="sxs-lookup"><span data-stu-id="8301c-120">Media Services supports tokens in the [Simple Web Tokens](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) (SWT) format and [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JWT) format.</span></span> <span data-ttu-id="8301c-121">Pour plus d’informations, consultez [Configurer la stratégie d’autorisation de clé de contenu](media-services-protect-with-aes128.md#configure_key_auth_policy).</span><span class="sxs-lookup"><span data-stu-id="8301c-121">For more information, see [Configure the content key’s authorization policy](media-services-protect-with-aes128.md#configure_key_auth_policy).</span></span>

<span data-ttu-id="8301c-122">Pour tirer parti du chiffrement dynamique, vous devez avoir un élément multimédia qui contient un ensemble de fichiers MP4 à débit binaire multiple ou de fichiers sources de diffusion en continu lisse (Smooth Streaming) à débit binaire multiple.</span><span class="sxs-lookup"><span data-stu-id="8301c-122">To take advantage of dynamic encryption, you need to have an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="8301c-123">Vous devez également configurer la stratégie de remise pour l'élément multimédia (décrite plus loin dans cette rubrique).</span><span class="sxs-lookup"><span data-stu-id="8301c-123">You also need to configure the delivery policy for the asset (described later in this topic).</span></span> <span data-ttu-id="8301c-124">Ensuite, en fonction du format spécifié dans l'URL de diffusion, le serveur de streaming à la demande s'assure que le flux est livré conformément au protocole choisi.</span><span class="sxs-lookup"><span data-stu-id="8301c-124">Then, based on the format specified in the streaming URL, the On-Demand Streaming server will ensure that the stream is delivered in the protocol you have chosen.</span></span> <span data-ttu-id="8301c-125">Par conséquent, il vous suffit de stocker et de payer les fichiers dans un seul format de stockage. Le service Media Services se charge de créer et de fournir la réponse appropriée en fonction des demandes des clients.</span><span class="sxs-lookup"><span data-stu-id="8301c-125">As a result, you only need to store and pay for the files in single storage format and Media Services service will build and serve the appropriate response based on requests from a client.</span></span>

<span data-ttu-id="8301c-126">Cette rubrique peut être utile pour les développeurs travaillant sur des applications qui fournissent du contenu multimédia protégé.</span><span class="sxs-lookup"><span data-stu-id="8301c-126">This topic would be useful to developers that work on applications that deliver protected media.</span></span> <span data-ttu-id="8301c-127">La rubrique vous montre comment configurer le service de distribution des clés avec des stratégies d'autorisation, afin que seuls les clients autorisés puissent recevoir les clés de chiffrement.</span><span class="sxs-lookup"><span data-stu-id="8301c-127">The topic shows you how to configure the key delivery service with authorization policies so that only authorized clients could receive the encryption keys.</span></span> <span data-ttu-id="8301c-128">Elle vous montre également comment utiliser le chiffrement dynamique.</span><span class="sxs-lookup"><span data-stu-id="8301c-128">It also shows how to use dynamic encryption.</span></span>


## <a name="aes-128-dynamic-encryption-and-key-delivery-service-workflow"></a><span data-ttu-id="8301c-129">Flux de travail du chiffrement dynamique AES-128 et du service de distribution des clés</span><span class="sxs-lookup"><span data-stu-id="8301c-129">AES-128 Dynamic Encryption and Key Delivery Service Workflow</span></span>

<span data-ttu-id="8301c-130">Voici les étapes générales que vous aurez à exécuter lors du chiffrement de vos éléments multimédias avec AES, en utilisant le service de distribution des clés Media Services, ainsi que le chiffrement dynamique.</span><span class="sxs-lookup"><span data-stu-id="8301c-130">The following are general steps that you would need to perform when encrypting your assets with AES, using the Media Services key delivery service, and also using dynamic encryption.</span></span>

1. <span data-ttu-id="8301c-131">[Créer un élément multimédia et télécharger des fichiers dans l’élément multimédia](media-services-protect-with-aes128.md#create_asset).</span><span class="sxs-lookup"><span data-stu-id="8301c-131">[Create an asset and upload files into the asset](media-services-protect-with-aes128.md#create_asset).</span></span>
2. <span data-ttu-id="8301c-132">[Encoder l'élément multimédia contenant le fichier selon le débit binaire MP4 défini](media-services-protect-with-aes128.md#encode_asset).</span><span class="sxs-lookup"><span data-stu-id="8301c-132">[Encode the asset containing the file to the adaptive bitrate MP4 set](media-services-protect-with-aes128.md#encode_asset).</span></span>
3. <span data-ttu-id="8301c-133">[Créer une clé de contenu et l’associer à l’élément multimédia encodé](media-services-protect-with-aes128.md#create_contentkey).</span><span class="sxs-lookup"><span data-stu-id="8301c-133">[Create a content key and associate it with the encoded asset](media-services-protect-with-aes128.md#create_contentkey).</span></span> <span data-ttu-id="8301c-134">Dans Media Services, la clé de contenu contient la clé de chiffrement de l'élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="8301c-134">In Media Services, the content key contains the asset’s encryption key.</span></span>
4. <span data-ttu-id="8301c-135">[Configurer la stratégie d’autorisation de la clé de contenu](media-services-protect-with-aes128.md#configure_key_auth_policy).</span><span class="sxs-lookup"><span data-stu-id="8301c-135">[Configure the content key’s authorization policy](media-services-protect-with-aes128.md#configure_key_auth_policy).</span></span> <span data-ttu-id="8301c-136">La stratégie d'autorisation de la clé de contenu doit être configurée par vous et respectée par le client afin que la clé de contenu soit remise au client.</span><span class="sxs-lookup"><span data-stu-id="8301c-136">The content key authorization policy must be configured by you and met by the client in order for the content key to be delivered to the client.</span></span>
5. <span data-ttu-id="8301c-137">[Configurer la stratégie de remise pour un élément multimédia](media-services-protect-with-aes128.md#configure_asset_delivery_policy).</span><span class="sxs-lookup"><span data-stu-id="8301c-137">[Configure the delivery policy for an asset](media-services-protect-with-aes128.md#configure_asset_delivery_policy).</span></span> <span data-ttu-id="8301c-138">La configuration de la stratégie de remise inclut : l’URL d’acquisition de clé et le vecteur d’initialisation (IV) (AES 128 nécessite que le vecteur d’initialisation fourni pour le chiffrement et le déchiffrement soit similaire), le protocole de remise (par exemple, MPEG DASH, HLS, Smooth Streaming ou tous), le type de chiffrement dynamique (par exemple, enveloppe ou aucun chiffrement dynamique).</span><span class="sxs-lookup"><span data-stu-id="8301c-138">The delivery policy configuration includes: key acquisition URL and Initialization Vector (IV) (AES 128 requires the same IV to be supplied when encrypting and decrypting), delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all), the type of dynamic encryption (for example, envelope or no dynamic encryption).</span></span>

    <span data-ttu-id="8301c-139">Vous pouvez appliquer des stratégies différentes à chaque protocole dans le même élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="8301c-139">You could apply different policy to each protocol on the same asset.</span></span> <span data-ttu-id="8301c-140">Par exemple, vous pouvez appliquer le chiffrement PlayReady à Smooth/DASH et AES Envelope à HLS.</span><span class="sxs-lookup"><span data-stu-id="8301c-140">For example, you could apply PlayReady encryption to Smooth/DASH and AES Envelope to HLS.</span></span> <span data-ttu-id="8301c-141">Tous les protocoles qui ne sont pas définis dans une stratégie de remise (par exemple, en cas d’ajout d’une stratégie unique qui spécifie uniquement TLS comme protocole) seront bloqués de la diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="8301c-141">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as the protocol) will be blocked from streaming.</span></span> <span data-ttu-id="8301c-142">Cela ne s’applique toutefois pas si vous n’avez défini aucune stratégie de remise de ressources.</span><span class="sxs-lookup"><span data-stu-id="8301c-142">The exception to this is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="8301c-143">Tous les protocoles seront alors autorisés.</span><span class="sxs-lookup"><span data-stu-id="8301c-143">Then, all protocols will be allowed in the clear.</span></span>

6. <span data-ttu-id="8301c-144">[Créer un localisateur à la demande](media-services-protect-with-aes128.md#create_locator) afin d’obtenir une URL de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="8301c-144">[Create an OnDemand locator](media-services-protect-with-aes128.md#create_locator) in order to get a streaming URL.</span></span>

<span data-ttu-id="8301c-145">La rubrique présente également [comment une application cliente peut demander une clé au service de distribution des clés](media-services-protect-with-aes128.md#client_request).</span><span class="sxs-lookup"><span data-stu-id="8301c-145">The topic also shows [how a client application can request a key from the key delivery service](media-services-protect-with-aes128.md#client_request).</span></span>

<span data-ttu-id="8301c-146">Vous trouverez un [exemple](media-services-protect-with-aes128.md#example) .NET complet à la fin de la rubrique.</span><span class="sxs-lookup"><span data-stu-id="8301c-146">You will find a complete .NET [example](media-services-protect-with-aes128.md#example) at the end of the topic.</span></span>

<span data-ttu-id="8301c-147">L'illustration suivante montre le flux de travail décrit ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="8301c-147">The following image demonstrates the workflow described above.</span></span> <span data-ttu-id="8301c-148">Ici, le jeton est utilisé pour l'authentification.</span><span class="sxs-lookup"><span data-stu-id="8301c-148">Here the token is used for authentication.</span></span>

![Protéger avec AES-128](./media/media-services-content-protection-overview/media-services-content-protection-with-aes.png)

<span data-ttu-id="8301c-150">Le reste de cette rubrique fournit des explications détaillées, des exemples de code et des liens vers des rubriques qui vous expliquent comment réaliser les tâches décrites ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="8301c-150">The rest of this topic provides detailed explanations, code examples, and links to topics that show you how to achieve the tasks described above.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="8301c-151">Limitations actuelles</span><span class="sxs-lookup"><span data-stu-id="8301c-151">Current limitations</span></span>
<span data-ttu-id="8301c-152">Si vous ajoutez ou mettez à jour la stratégie de remise de votre ressource, vous devez supprimer le localisateur existant (le cas échéant) et en créer un nouveau.</span><span class="sxs-lookup"><span data-stu-id="8301c-152">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>

## <span data-ttu-id="8301c-153"><a id="create_asset"></a>Créer un élément multimédia et télécharger des fichiers dans l’élément multimédia</span><span class="sxs-lookup"><span data-stu-id="8301c-153"><a id="create_asset"></a>Create an asset and upload files into the asset</span></span>
<span data-ttu-id="8301c-154">Pour gérer, encoder et diffuser vos vidéos, vous devez d'abord télécharger votre contenu dans Microsoft Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="8301c-154">In order to manage, encode, and stream your videos, you must first upload your content into Microsoft Azure Media Services.</span></span> <span data-ttu-id="8301c-155">Une fois téléchargé, votre contenu est stocké en toute sécurité dans le cloud et peut faire l’objet d’un traitement et d’une diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="8301c-155">Once uploaded, your content is stored securely in the cloud for further processing and streaming.</span></span> 

<span data-ttu-id="8301c-156">Pour plus d’informations, consultez [Charger des fichiers vers un compte Media Services](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="8301c-156">For detailed information, see [Upload Files into a Media Services account](media-services-dotnet-upload-files.md).</span></span>

## <span data-ttu-id="8301c-157"><a id="encode_asset"></a>Encoder l’élément multimédia contenant le fichier selon le débit binaire MP4 défini</span><span class="sxs-lookup"><span data-stu-id="8301c-157"><a id="encode_asset"></a>Encode the asset containing the file to the adaptive bitrate MP4 set</span></span>
<span data-ttu-id="8301c-158">Avec le chiffrement dynamique, il vous suffit de créer un élément multimédia qui contient un ensemble de fichiers MP4 à débit binaire multiple ou de fichiers sources de diffusion en continu lisse à débit binaire multiple.</span><span class="sxs-lookup"><span data-stu-id="8301c-158">With dynamic encryption all you need is to create an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="8301c-159">Ensuite, en fonction du format spécifié dans le manifeste ou la demande de fragment, le serveur de diffusion en continu à la demande s'assure que vous recevez le flux conforme au protocole choisi.</span><span class="sxs-lookup"><span data-stu-id="8301c-159">Then, based on the specified format in the manifest or fragment request, the On-Demand Streaming server will ensure that you receive the stream in the protocol you have chosen.</span></span> <span data-ttu-id="8301c-160">Par conséquent, il vous suffit de stocker et de payer les fichiers dans un seul format de stockage. Le service Media Services se charge de créer et de fournir la réponse appropriée en fonction des demandes des clients.</span><span class="sxs-lookup"><span data-stu-id="8301c-160">As a result, you only need to store and pay for the files in single storage format and Media Services service will build and serve the appropriate response based on requests from a client.</span></span> <span data-ttu-id="8301c-161">Pour plus d’informations, consultez la rubrique [Vue d’ensemble de l’empaquetage dynamique](media-services-dynamic-packaging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8301c-161">For more information, see the [Dynamic Packaging Overview](media-services-dynamic-packaging-overview.md) topic.</span></span>

>[!NOTE]
><span data-ttu-id="8301c-162">Une fois votre compte AMS créé, un point de terminaison de streaming **par défaut** est ajouté à votre compte à l’état **Arrêté**.</span><span class="sxs-lookup"><span data-stu-id="8301c-162">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="8301c-163">Pour démarrer la diffusion en continu de votre contenu et tirer parti de l’empaquetage et du chiffrement dynamiques, le point de terminaison de streaming à partir duquel vous souhaitez diffuser du contenu doit se trouver à l’état **En cours d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="8301c-163">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> 
>
><span data-ttu-id="8301c-164">De plus, pour pouvoir utiliser l’empaquetage et le chiffrement dynamiques, votre ressource doit contenir un ensemble de MP4 à débit adaptatif ou des fichiers de diffusion en continu lisse à débit adaptatif.</span><span class="sxs-lookup"><span data-stu-id="8301c-164">Also, to be able to use dynamic packaging and dynamic encryption your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span>

<span data-ttu-id="8301c-165">Pour savoir comment encoder, consultez [Encodage d’un élément multimédia à l’aide de Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).</span><span class="sxs-lookup"><span data-stu-id="8301c-165">For instructions on how to encode, see [How to encode an asset using Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).</span></span>

## <span data-ttu-id="8301c-166"><a id="create_contentkey"></a>Créer une clé de contenu et l’associer à l’élément multimédia encodé</span><span class="sxs-lookup"><span data-stu-id="8301c-166"><a id="create_contentkey"></a>Create a content key and associate it with the encoded asset</span></span>
<span data-ttu-id="8301c-167">Dans Media Services, la clé de contenu contient la clé que vous souhaitez utiliser pour chiffrer un élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="8301c-167">In Media Services, the content key contains the key that you want to encrypt an asset with.</span></span>

<span data-ttu-id="8301c-168">Pour plus d’informations, consultez [Créer une clé de contenu](media-services-dotnet-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="8301c-168">For detailed information, see [Create content key](media-services-dotnet-create-contentkey.md).</span></span>

## <span data-ttu-id="8301c-169"><a id="configure_key_auth_policy"></a>Configurez la stratégie d’autorisation de la clé de contenu.</span><span class="sxs-lookup"><span data-stu-id="8301c-169"><a id="configure_key_auth_policy"></a>Configure the content key’s authorization policy</span></span>
<span data-ttu-id="8301c-170">Media Services prend en charge plusieurs méthodes d’authentification des utilisateurs effectuant des demandes de clé.</span><span class="sxs-lookup"><span data-stu-id="8301c-170">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="8301c-171">La stratégie d'autorisation de la clé de contenu doit être configurée par vous et respectée par le client (lecteur) afin que la clé soit remise au client.</span><span class="sxs-lookup"><span data-stu-id="8301c-171">The content key authorization policy must be configured by you and met by the client (player) in order for the key to be delivered to the client.</span></span> <span data-ttu-id="8301c-172">La stratégie d’autorisation des clés de contenu peut avoir une ou plusieurs restrictions d’autorisations : ouvert, restriction par jeton ou restriction IP.</span><span class="sxs-lookup"><span data-stu-id="8301c-172">The content key authorization policy could have one or more authorization restrictions: open, token restriction, or IP restriction.</span></span>

<span data-ttu-id="8301c-173">Pour plus d’informations, consultez [Configurer la stratégie d’autorisation de clé de contenu](media-services-dotnet-configure-content-key-auth-policy.md).</span><span class="sxs-lookup"><span data-stu-id="8301c-173">For detailed information, see [Configure Content Key Authorization Policy](media-services-dotnet-configure-content-key-auth-policy.md).</span></span>

## <span data-ttu-id="8301c-174"><a id="configure_asset_delivery_policy"></a>Configurer la stratégie de distribution d’éléments multimédia</span><span class="sxs-lookup"><span data-stu-id="8301c-174"><a id="configure_asset_delivery_policy"></a>Configure asset delivery policy</span></span>
<span data-ttu-id="8301c-175">Configurez la stratégie de remise pour votre élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="8301c-175">Configure the delivery policy for your asset.</span></span> <span data-ttu-id="8301c-176">Certains éléments que la configuration de la stratégie de remise de l'élément multimédia inclut :</span><span class="sxs-lookup"><span data-stu-id="8301c-176">Some things that the asset delivery policy configuration includes:</span></span>

* <span data-ttu-id="8301c-177">L'URL d'acquisition de la clé.</span><span class="sxs-lookup"><span data-stu-id="8301c-177">The Key acquisition URL.</span></span> 
* <span data-ttu-id="8301c-178">Le vecteur d'initialisation (IV) à utiliser pour le chiffrement d'enveloppe.</span><span class="sxs-lookup"><span data-stu-id="8301c-178">The Initialization Vector (IV) to use for the envelope encryption.</span></span> <span data-ttu-id="8301c-179">AES 128 nécessite que le vecteur d'initialisation fourni pour le chiffrement et le déchiffrement soit similaire.</span><span class="sxs-lookup"><span data-stu-id="8301c-179">AES 128 requires the same IV to be supplied when encrypting and decrypting.</span></span> 
* <span data-ttu-id="8301c-180">Le protocole de remise de l’élément multimédia (par exemple, MPEG DASH, HLS, Smooth Streaming ou tous).</span><span class="sxs-lookup"><span data-stu-id="8301c-180">The asset delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all).</span></span>
* <span data-ttu-id="8301c-181">Le type de chiffrement dynamique (par exemple, AES Envelope) ou aucun chiffrement dynamique.</span><span class="sxs-lookup"><span data-stu-id="8301c-181">The type of dynamic encryption (for example, AES envelope) or no dynamic encryption.</span></span> 

<span data-ttu-id="8301c-182">Pour plus d’informations, consultez [Configurer la stratégie de distribution d’éléments multimédia ](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="8301c-182">For detailed information, see [Configure asset delivery policy ](media-services-rest-configure-asset-delivery-policy.md).</span></span>

## <span data-ttu-id="8301c-183"><a id="create_locator"></a>Créer un localisateur de diffusion en continu à la demande afin d’obtenir une URL de diffusion en continu</span><span class="sxs-lookup"><span data-stu-id="8301c-183"><a id="create_locator"></a>Create an OnDemand streaming locator in order to get a streaming URL</span></span>
<span data-ttu-id="8301c-184">Vous devrez fournir aux utilisateurs l'URL de diffusion en continu pour Smooth, DASH ou HLS.</span><span class="sxs-lookup"><span data-stu-id="8301c-184">You will need to provide your user with the streaming URL for Smooth, DASH or HLS.</span></span>

> [!NOTE]
> <span data-ttu-id="8301c-185">Si vous ajoutez ou mettez à jour la stratégie de remise de votre ressource, vous devez supprimer le localisateur existant (le cas échéant) et en créer un nouveau.</span><span class="sxs-lookup"><span data-stu-id="8301c-185">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
> 
> 

<span data-ttu-id="8301c-186">Pour savoir comment publier une ressource et générer une URL de diffusion en continu, consultez [Générer une URL de diffusion en continu](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="8301c-186">For instructions on how to publish an asset and build a streaming URL, see [Build a streaming URL](media-services-deliver-streaming-content.md).</span></span>

## <a name="get-a-test-token"></a><span data-ttu-id="8301c-187">Obtenir un test de jeton</span><span class="sxs-lookup"><span data-stu-id="8301c-187">Get a test token</span></span>
<span data-ttu-id="8301c-188">Obtenez un jeton de test basé sur la restriction par jeton utilisée pour la stratégie d’autorisation de clé.</span><span class="sxs-lookup"><span data-stu-id="8301c-188">Get a test token based on the token restriction that was used for the key authorization policy.</span></span>

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate = 
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on the data in the given TokenRestrictionTemplate.
    //The GenerateTestToken method returns the token without the word “Bearer” in front
    //so you have to add it in front of the token string. 
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate);
    Console.WriteLine("The authorization token is:\nBearer {0}", testToken);

<span data-ttu-id="8301c-189">Vous pouvez utiliser le [lecteur AMS](http://amsplayer.azurewebsites.net/azuremediaplayer.html) pour tester votre flux.</span><span class="sxs-lookup"><span data-stu-id="8301c-189">You can use the [AMS Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) to test your stream.</span></span>

## <span data-ttu-id="8301c-190"><a id="client_request"></a>Comment votre client peut-il demander une clé à partir du service de distribution des clés ?</span><span class="sxs-lookup"><span data-stu-id="8301c-190"><a id="client_request"></a>How can your client request a key from the key delivery service?</span></span>
<span data-ttu-id="8301c-191">Dans l'étape précédente, vous avez construit l'URL qui pointe vers un fichier manifeste.</span><span class="sxs-lookup"><span data-stu-id="8301c-191">In the previous step, you constructed the URL that points to a manifest file.</span></span> <span data-ttu-id="8301c-192">Votre client doit extraire les informations nécessaires à partir des fichiers manifeste de diffusion en continu afin d'effectuer une demande au service de distribution des clés.</span><span class="sxs-lookup"><span data-stu-id="8301c-192">Your client needs to extract the necessary information from the streaming manifest files in order to make a request to the key delivery service.</span></span>

### <a name="manifest-files"></a><span data-ttu-id="8301c-193">Fichiers manifeste</span><span class="sxs-lookup"><span data-stu-id="8301c-193">Manifest files</span></span>
<span data-ttu-id="8301c-194">Le client doit extraire la valeur de l'URL (qui contient également l'ID de la clé de contenu (kid)) à partir du fichier manifeste.</span><span class="sxs-lookup"><span data-stu-id="8301c-194">The client needs to extract the URL (that also contains content key Id (kid)) value from the manifest file.</span></span> <span data-ttu-id="8301c-195">Ensuite, le client doit essayer d'obtenir la clé de chiffrement à partir du service de distribution des clés.</span><span class="sxs-lookup"><span data-stu-id="8301c-195">The client will then try to get the encryption key from the key delivery service.</span></span> <span data-ttu-id="8301c-196">Le client doit également extraire la valeur IV et l’utiliser pour déchiffrer le flux. L’extrait de code suivant montre l’élément <Protection> du manifeste Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="8301c-196">The client also needs to extract the IV value and use it do decrypt the stream.The following snippet shows the <Protection> element of the Smooth Streaming manifest.</span></span>

    <Protection>
      <ProtectionHeader SystemID="B47B251A-2409-4B42-958E-08DBAE7B4EE9">
        <ContentProtection xmlns:sea="urn:mpeg:dash:schema:sea:2012" schemeIdUri="urn:mpeg:dash:sea:2012">
          <sea:SegmentEncryption schemeIdUri="urn:mpeg:dash:sea:aes128-cbc:2013"/>
          <sea:KeySystem keySystemUri="urn:mpeg:dash:sea:keysys:http:2013"/>
          <sea:CryptoPeriod IV="0xD7D7D7D7D7D7D7D7D7D7D7D7D7D7D7D7" 
                            keyUriTemplate="https://wamsbayclus001kd-hs.cloudapp.net/HlsHandler.ashx?
                                            kid=da3813af-55e6-48e7-aa9f-a4d6031f7b4d"/>
        </ContentProtection>
      </ProtectionHeader>
    </Protection>

<span data-ttu-id="8301c-197">Dans le cas de HLS, le manifeste racine est divisé en fichiers de segment.</span><span class="sxs-lookup"><span data-stu-id="8301c-197">In the case of HLS, the root manifest is broken into segment files.</span></span> 

<span data-ttu-id="8301c-198">Par exemple, le manifeste racine est : http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/manifest(format=m3u8-aapl) et il contient une liste de noms de fichiers de segment.</span><span class="sxs-lookup"><span data-stu-id="8301c-198">For example, the root manifest is: http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/manifest(format=m3u8-aapl) and it contains a list of segment file names.</span></span>

    . . . 
    #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=630133,RESOLUTION=424x240,CODECS="avc1.4d4015,mp4a.40.2",AUDIO="audio"
    QualityLevels(514369)/Manifest(video,format=m3u8-aapl)
    #EXT-X-STREAM-INF:PROGRAM-ID=1,BANDWIDTH=965441,RESOLUTION=636x356,CODECS="avc1.4d401e,mp4a.40.2",AUDIO="audio"
    QualityLevels(842459)/Manifest(video,format=m3u8-aapl)
    …

<span data-ttu-id="8301c-199">Si vous ouvrez l’un des fichiers de segment dans l’éditeur de texte (par exemple, http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/QualityLevels(514369)/Manifest(video,format=m3u8-aapl), il doit contenir #EXT-X-KEY qui indique que le fichier est chiffré.</span><span class="sxs-lookup"><span data-stu-id="8301c-199">If you open one of the segment files in text editor (for example, http://test001.origin.mediaservices.windows.net/8bfe7d6f-34e3-4d1a-b289-3e48a8762490/BigBuckBunny.ism/QualityLevels(514369)/Manifest(video,format=m3u8-aapl), it should contain #EXT-X-KEY which indicates that the file is encrypted.</span></span>

    #EXTM3U
    #EXT-X-VERSION:4
    #EXT-X-ALLOW-CACHE:NO
    #EXT-X-MEDIA-SEQUENCE:0
    #EXT-X-TARGETDURATION:9
    #EXT-X-KEY:METHOD=AES-128,
    URI="https://wamsbayclus001kd-hs.cloudapp.net/HlsHandler.ashx?
         kid=da3813af-55e6-48e7-aa9f-a4d6031f7b4d",
            IV=0XD7D7D7D7D7D7D7D7D7D7D7D7D7D7D7D7
    #EXT-X-PROGRAM-DATE-TIME:1970-01-01T00:00:00.000+00:00
    #EXTINF:8.425708,no-desc
    Fragments(video=0,format=m3u8-aapl)
    #EXT-X-ENDLIST

>[!NOTE] 
><span data-ttu-id="8301c-200">Si vous envisagez de lire un flux HLS chiffré par AES dans Safari, consultez [ce billet de blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span><span class="sxs-lookup"><span data-stu-id="8301c-200">If you are planning to play an AES encrypted HLS in Safari, see [this blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span></span>

### <a name="request-the-key-from-the-key-delivery-service"></a><span data-ttu-id="8301c-201">Demander la clé au service de distribution des clés</span><span class="sxs-lookup"><span data-stu-id="8301c-201">Request the key from the key delivery service</span></span>

<span data-ttu-id="8301c-202">Le code suivant montre comment envoyer une requête au service de distribution des clés Media Services à l'aide d'un Uri (extrait du manifeste) de remise de clé et d'un jeton (cette rubrique ne traite pas de l'obtention de jetons Simple Web à partir d'un service de jeton sécurisé).</span><span class="sxs-lookup"><span data-stu-id="8301c-202">The following code shows how to send a request to the Media Services key delivery service using a key delivery Uri (that was extracted from the manifest) and a token (this topic does not talk about how to get Simple Web Tokens from a Secure Token Service).</span></span>

    private byte[] GetDeliveryKey(Uri keyDeliveryUri, string token)
    {
        HttpWebRequest request = (HttpWebRequest)WebRequest.Create(keyDeliveryUri);

        request.Method = "POST";
        request.ContentType = "text/xml";
        if (!string.IsNullOrEmpty(token))
        {
            request.Headers[AuthorizationHeader] = token;
        }
        request.ContentLength = 0;

        var response = request.GetResponse();

        var stream = response.GetResponseStream();
        if (stream == null)
        {
            throw new NullReferenceException("Response stream is null");
        }

        var buffer = new byte[256];
        var length = 0;
        while (stream.CanRead && length <= buffer.Length)
        {
            var nexByte = stream.ReadByte();
            if (nexByte == -1)
            {
                break;
            }
            buffer[length] = (byte)nexByte;
            length++;
        }
        response.Close();

        // AES keys must be exactly 16 bytes (128 bits).
        var key = new byte[length];
        Array.Copy(buffer, key, length);
        return key;
    }

## <a name="protect-your-content-with-aes-128-using-net"></a><span data-ttu-id="8301c-203">Protéger votre contenu avec AES-128 en utilisant .NET</span><span class="sxs-lookup"><span data-stu-id="8301c-203">Protect your content with AES-128 using .NET</span></span>

### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="8301c-204">Créer et configurer un projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8301c-204">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="8301c-205">Configurez votre environnement de développement et ajoutez des informations de connexion au fichier app.config selon la procédure décrite dans l’article [Développement Media Services avec .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="8301c-205">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="8301c-206">Ajoutez les éléments suivants aux **appSettings** définis dans votre fichier app.config :</span><span class="sxs-lookup"><span data-stu-id="8301c-206">Add the following elements to **appSettings** defined in your app.config file:</span></span>

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

### <span data-ttu-id="8301c-207"><a id="example"></a>Exemple</span><span class="sxs-lookup"><span data-stu-id="8301c-207"><a id="example"></a>Example</span></span>

<span data-ttu-id="8301c-208">Remplacez le code dans votre fichier Program.cs par le code présenté dans cette section.</span><span class="sxs-lookup"><span data-stu-id="8301c-208">Overwrite the code in your Program.cs file with the code shown in this section.</span></span>
 
>[!NOTE]
><span data-ttu-id="8301c-209">Un nombre limite de 1 000 000 a été défini pour les différentes stratégies AMS (par exemple, pour la stratégie de localisateur ou pour ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="8301c-209">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="8301c-210">Vous devez utiliser le même ID de stratégie si vous utilisez toujours les mêmes jours / autorisations d’accès, par exemple, les stratégies pour les localisateurs destinées à demeurer en place pendant une longue période (stratégies sans chargement).</span><span class="sxs-lookup"><span data-stu-id="8301c-210">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="8301c-211">Pour plus d’informations, consultez [cette rubrique](media-services-dotnet-manage-entities.md#limit-access-policies) .</span><span class="sxs-lookup"><span data-stu-id="8301c-211">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="8301c-212">Veillez à mettre à jour les variables pour pointer vers les dossiers où se trouvent vos fichiers d'entrée.</span><span class="sxs-lookup"><span data-stu-id="8301c-212">Make sure to update variables to point to folders where your input files are located.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Security.Cryptography;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;

    namespace AESDynamicEncryptionAndKeyDeliverySvc
    {
        class Program
        {
        // Read values from the App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // A Uri describing the issuer of the token.  
        // Must match the value in the token for the token to be considered valid.
        private static readonly Uri _sampleIssuer =
            new Uri(ConfigurationManager.AppSettings["Issuer"]);
        // The Audience or Scope of the token.  
        // Must match the value in the token for the token to be considered valid.
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

            IContentKey key = CreateEnvelopeTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for the asset {1} ", key.Id, encodedAsset.Id);
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

            // Generate a test token based on the data in the given TokenRestrictionTemplate.
            // Note, you need to pass the key id Guid because we specified 
            // TokenClaim.ContentKeyIdentifierClaim in during the creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);

            //The GenerateTestToken method returns the token without the word “Bearer” in front
            //so you have to add it in front of the token string. 
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey);
            Console.WriteLine("The authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            // You can use the bit.ly/aesplayer Flash player to test the URL 
            // (with open authorization policy). 
            // Paste the URL and click the Update button to play the video. 
            //
            string URL = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Smooth Streaming Url: {0}/manifest", URL);
            Console.WriteLine();
            Console.WriteLine("HLS Url: {0}/manifest(format=m3u8-aapl)", URL);
            Console.WriteLine();

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
            IAsset inputAsset = _context.Assets.Create(assetName, AssetCreationOptions.StorageEncrypted);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Created assetFile {0}", assetFile.Name);


            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset asset)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("Media Encoder Standard Job");
            // Get a media processor reference, and pass to it the name of the 
            // processor to use for the specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task with the encoding details, using a string preset.
            // In this case "Adaptive Streaming" preset is used.
            ITask task = job.Tasks.AddNew("My encoding task",
            processor,
            "Adaptive Streaming",
            TaskOptions.None);

            // Specify the input asset to be encoded.
            task.InputAssets.Add(asset);
            // Add an output asset to contain the results of the job. 
            // This output is specified as AssetCreationOptions.None, which 
            // means the output asset is not encrypted. 
            task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.StorageEncrypted);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }

        private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
        {
            var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
            ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

            if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

            return processor;
        }

        static public IContentKey CreateEnvelopeTypeContentKey(IAsset asset)
        {
            // Create envelope encryption content key
            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                keyId,
                contentKey,
                "ContentKey",
                ContentKeyType.EnvelopeEncryption);

            // Associate the key with the asset.
            asset.ContentKeys.Add(key);

            return key;
        }

        static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
        {
            // Create ContentKeyAuthorizationPolicy with Open restrictions 
            // and create authorization policy             
            IContentKeyAuthorizationPolicy policy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Open Authorization Policy").Result;

            List<ContentKeyAuthorizationPolicyRestriction> restrictions =
            new List<ContentKeyAuthorizationPolicyRestriction>();

            ContentKeyAuthorizationPolicyRestriction restriction =
            new ContentKeyAuthorizationPolicyRestriction
            {
            Name = "HLS Open Authorization Policy",
            KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
            Requirements = null // no requirements needed for HLS
        };

            restrictions.Add(restriction);

            IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create(
            "policy",
            ContentKeyDeliveryType.BaselineHttp,
            restrictions,
            "");

            policy.Options.Add(policyOption);

            // Add ContentKeyAutorizationPolicy to ContentKey
            contentKey.AuthorizationPolicyId = policy.Id;
            IContentKey updatedKey = contentKey.UpdateAsync().Result;
            Console.WriteLine("Adding Key to Asset: Key ID is " + updatedKey.Id);
        }

        public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
        {
            string tokenTemplateString = GenerateTokenRequirements();

            IContentKeyAuthorizationPolicy policy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("HLS token restricted authorization policy").Result;

            List<ContentKeyAuthorizationPolicyRestriction> restrictions =
            new List<ContentKeyAuthorizationPolicyRestriction>();

            ContentKeyAuthorizationPolicyRestriction restriction =
            new ContentKeyAuthorizationPolicyRestriction
            {
                Name = "Token Authorization Policy",
                KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                Requirements = tokenTemplateString
            };

            restrictions.Add(restriction);

            //You could have multiple options 
            IContentKeyAuthorizationPolicyOption policyOption =
            _context.ContentKeyAuthorizationPolicyOptions.Create(
            "Token option for HLS",
            ContentKeyDeliveryType.BaselineHttp,
            restrictions,
            null  // no key delivery data is needed for HLS
            );

            policy.Options.Add(policyOption);

            // Add ContentKeyAutorizationPolicy to ContentKey
            contentKey.AuthorizationPolicyId = policy.Id;
            IContentKey updatedKey = contentKey.UpdateAsync().Result;
            Console.WriteLine("Adding Key to Asset: Key ID is " + updatedKey.Id);

            return tokenTemplateString;
        }

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            Uri keyAcquisitionUri = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.BaselineHttp);

            string envelopeEncryptionIV = Convert.ToBase64String(GetRandomBuffer(16));

            // When configuring delivery policy, you can choose to associate it
            // with a key acquisition URL that has a KID appended or
            // or a key acquisition URL that does not have a KID appended  
            // in which case a content key can be reused. 

            // EnvelopeKeyAcquisitionUrl:  contains a key ID in the key URL.
            // EnvelopeBaseKeyAcquisitionUrl:  the URL does not contains a key ID

            // The following policy configuration specifies: 
            // key url that will have KID=<Guid> appended to the envelope and
            // the Initialization Vector (IV) to use for the envelope encryption.

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
            {AssetDeliveryPolicyConfigurationKey.EnvelopeKeyAcquisitionUrl, keyAcquisitionUri.ToString()}
            };

            IAssetDeliveryPolicy assetDeliveryPolicy =
            _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
                AssetDeliveryPolicyType.DynamicEnvelopeEncryption,
                AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.Dash,
                assetDeliveryPolicyConfiguration);

            // Add AssetDelivery Policy to the asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);
            Console.WriteLine();
            Console.WriteLine("Adding Asset Delivery Policy: " +
            assetDeliveryPolicy.AssetDeliveryPolicyType);
        }

        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference to the streaming manifest file from the  
            // collection of files in the asset. 

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                EndsWith(".ism")).
                FirstOrDefault();

            // Create a 30-day readonly access policy. 
            // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.            
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

        static private void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine(string.Format("{0}\n  State: {1}\n  Time: {2}\n\n",
            ((IJob)sender).Name,
            e.CurrentState,
            DateTime.UtcNow.ToString(@"yyyy_M_d__hh_mm_ss")));
        }

        static private byte[] GetRandomBuffer(int size)
        {
            byte[] randomBytes = new byte[size];
            using (RNGCryptoServiceProvider rng = new RNGCryptoServiceProvider())
            {
            rng.GetBytes(randomBytes);
            }

            return randomBytes;
        }
        }
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="8301c-213">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="8301c-213">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="8301c-214">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="8301c-214">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

