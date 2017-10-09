---
title: aaaProtect de contenu HLS avec Microsoft PlayReady ou Apple FairPlay - Azure | Documents Microsoft
description: "Cette rubrique donne une vue d’ensemble et montre comment toouse Azure Media Services toodynamically chiffrer votre contenu HTTP Live Streaming (HLS) avec Apple FairPlay. Il montre également comment la remise service toodeliver tooclients de licences FairPlay de licence toouse hello Media Services."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7c3b35d9-1269-4c83-8c91-490ae65b0817
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 91ca451e3e7bf0da1d74dac4c99180f08f39e4ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="protect-your-hls-content-with-apple-fairplay-or-microsoft-playready"></a><span data-ttu-id="09876-104">Protéger votre contenu HLS avec Apple FairPlay ou Microsoft PlayReady</span><span class="sxs-lookup"><span data-stu-id="09876-104">Protect your HLS content with Apple FairPlay or Microsoft PlayReady</span></span>
<span data-ttu-id="09876-105">Azure permet de Media Services vous toodynamically chiffrer votre contenu HTTP Live Streaming (HLS) à l’aide de hello suivant formats :</span><span class="sxs-lookup"><span data-stu-id="09876-105">Azure Media Services enables you toodynamically encrypt your HTTP Live Streaming (HLS) content by using hello following formats:</span></span>  

* <span data-ttu-id="09876-106">**Clé en clair de l’enveloppe AES-128**</span><span class="sxs-lookup"><span data-stu-id="09876-106">**AES-128 envelope clear key**</span></span>

    <span data-ttu-id="09876-107">Hello segment entier est chiffré à l’aide de hello **AES-128 CBC** mode.</span><span class="sxs-lookup"><span data-stu-id="09876-107">hello entire chunk is encrypted by using hello **AES-128 CBC** mode.</span></span> <span data-ttu-id="09876-108">déchiffrement Hello du flux de hello est pris en charge par iOS et le lecteur du système d’exploitation X en mode natif.</span><span class="sxs-lookup"><span data-stu-id="09876-108">hello decryption of hello stream is supported by iOS and OS X player natively.</span></span> <span data-ttu-id="09876-109">Pour plus d’informations, consultez la page [Utilisation du chiffrement dynamique AES-128 et du service de distribution des clés](media-services-protect-with-aes128.md).</span><span class="sxs-lookup"><span data-stu-id="09876-109">For more information, see [Using AES-128 dynamic encryption and key delivery service](media-services-protect-with-aes128.md).</span></span>
* <span data-ttu-id="09876-110">**Apple FairPlay**</span><span class="sxs-lookup"><span data-stu-id="09876-110">**Apple FairPlay**</span></span>

    <span data-ttu-id="09876-111">Hello individuel vidéo et audio échantillons sont chiffrées à l’aide de hello **AES-128 CBC** mode.</span><span class="sxs-lookup"><span data-stu-id="09876-111">hello individual video and audio samples are encrypted by using hello **AES-128 CBC** mode.</span></span> <span data-ttu-id="09876-112">**Diffusion en continu de FairPlay** (i/s) est intégré dans les systèmes d’exploitation pour appareils hello, avec prise en charge native sur iOS et Apple TV.</span><span class="sxs-lookup"><span data-stu-id="09876-112">**FairPlay Streaming** (FPS) is integrated into hello device operating systems, with native support on iOS and Apple TV.</span></span> <span data-ttu-id="09876-113">Safari sur OS X permet i/s à l’aide de prise en charge d’interface hello chiffrés Media Extensions (EME).</span><span class="sxs-lookup"><span data-stu-id="09876-113">Safari on OS X enables FPS by using hello Encrypted Media Extensions (EME) interface support.</span></span>
* <span data-ttu-id="09876-114">**Microsoft PlayReady**</span><span class="sxs-lookup"><span data-stu-id="09876-114">**Microsoft PlayReady**</span></span>

<span data-ttu-id="09876-115">Hello image suivante montre hello **HLS + FairPlay ou PlayReady chiffrement dynamique** flux de travail.</span><span class="sxs-lookup"><span data-stu-id="09876-115">hello following image shows hello **HLS + FairPlay or PlayReady dynamic encryption** workflow.</span></span>

![Diagramme de flux de travail de chiffrement dynamique](./media/media-services-content-protection-overview/media-services-content-protection-with-fairplay.png)

<span data-ttu-id="09876-117">Cette rubrique montre comment toouse Media Services toodynamically chiffrer votre contenu HLS avec FairPlay d’Apple.</span><span class="sxs-lookup"><span data-stu-id="09876-117">This topic demonstrates how toouse Media Services toodynamically encrypt your HLS content with Apple FairPlay.</span></span> <span data-ttu-id="09876-118">Il montre également comment la remise service toodeliver tooclients de licences FairPlay de licence toouse hello Media Services.</span><span class="sxs-lookup"><span data-stu-id="09876-118">It also shows how toouse hello Media Services license delivery service toodeliver FairPlay licenses tooclients.</span></span>

> [!NOTE]
> <span data-ttu-id="09876-119">Si vous voulez également tooencrypt votre contenu HLS avec PlayReady, vous devez toocreate une clé de contenu commune et l’associez à votre élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="09876-119">If you also want tooencrypt your HLS content with PlayReady, you need toocreate a common content key and associate it with your asset.</span></span> <span data-ttu-id="09876-120">Vous devez également stratégie d’autorisation de tooconfigure hello de clé du contenu, comme décrit dans [du chiffrement commun dynamique à l’aide de PlayReady](media-services-protect-with-drm.md).</span><span class="sxs-lookup"><span data-stu-id="09876-120">You also need tooconfigure hello content key’s authorization policy, as described in [Using PlayReady dynamic common encryption](media-services-protect-with-drm.md).</span></span>
>
>

## <a name="requirements-and-considerations"></a><span data-ttu-id="09876-121">Conditions requises et éléments à prendre en compte</span><span class="sxs-lookup"><span data-stu-id="09876-121">Requirements and considerations</span></span>

<span data-ttu-id="09876-122">Hello Voici requis lors de l’utilisation de toodeliver Media Services que HLS chiffré avec FairPlay et toodeliver FairPlay licences :</span><span class="sxs-lookup"><span data-stu-id="09876-122">hello following are required when using Media Services toodeliver HLS encrypted with FairPlay, and toodeliver FairPlay licenses:</span></span>

  * <span data-ttu-id="09876-123">Un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="09876-123">An Azure account.</span></span> <span data-ttu-id="09876-124">Pour plus d’informations, consultez la page [Version d’évaluation gratuite d’Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="09876-124">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
  * <span data-ttu-id="09876-125">Un compte Media Services.</span><span class="sxs-lookup"><span data-stu-id="09876-125">A Media Services account.</span></span> <span data-ttu-id="09876-126">toocreate, consultez [créer un compte Azure Media Services à l’aide de hello Azure portal](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="09876-126">toocreate one, see [Create an Azure Media Services account using hello Azure portal](media-services-portal-create-account.md).</span></span>
  * <span data-ttu-id="09876-127">S’inscrire au programme [Apple Developer Program](https://developer.apple.com/).</span><span class="sxs-lookup"><span data-stu-id="09876-127">Sign up with [Apple Development Program](https://developer.apple.com/).</span></span>
  * <span data-ttu-id="09876-128">Apple requiert hello de hello propriétaire du contenu tooobtain [package de déploiement](https://developer.apple.com/contact/fps/).</span><span class="sxs-lookup"><span data-stu-id="09876-128">Apple requires hello content owner tooobtain hello [deployment package](https://developer.apple.com/contact/fps/).</span></span> <span data-ttu-id="09876-129">L’état que vous déjà implémenté de Module de sécurité de clé (KSM) avec Media Services et que vous demandez le package d’images par seconde final hello.</span><span class="sxs-lookup"><span data-stu-id="09876-129">State that you already implemented Key Security Module (KSM) with Media Services, and that you are requesting hello final FPS package.</span></span> <span data-ttu-id="09876-130">Des instructions Bonjour i/s final toogenerate certification du package et obtenir hello clé de Secret d’Application (demandez).</span><span class="sxs-lookup"><span data-stu-id="09876-130">There are instructions in hello final FPS package toogenerate certification and obtain hello Application Secret Key (ASK).</span></span> <span data-ttu-id="09876-131">Vous utilisez ASK tooconfigure FairPlay.</span><span class="sxs-lookup"><span data-stu-id="09876-131">You use ASK tooconfigure FairPlay.</span></span>
  * <span data-ttu-id="09876-132">Kit de développement logiciel (SDK) .NET Azure Media Services version **3.6.0** ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="09876-132">Azure Media Services .NET SDK version **3.6.0** or later.</span></span>

<span data-ttu-id="09876-133">Hello suivant d’éléments doit être définie sur le côté de distribution de clés de Media Services :</span><span class="sxs-lookup"><span data-stu-id="09876-133">hello following things must be set on Media Services key delivery side:</span></span>

  * <span data-ttu-id="09876-134">**Application Cert (AC)**: il s’agit d’un fichier .pfx qui contient la clé privée de hello.</span><span class="sxs-lookup"><span data-stu-id="09876-134">**App Cert (AC)**: This is a .pfx file that contains hello private key.</span></span> <span data-ttu-id="09876-135">Vous devez créer ce fichier et le chiffrer avec un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="09876-135">You create this file and encrypt it with a password.</span></span>

       <span data-ttu-id="09876-136">Lorsque vous configurez une stratégie de distribution de clés, vous devez fournir ce fichier .pfx hello et le mot de passe au format Base64.</span><span class="sxs-lookup"><span data-stu-id="09876-136">When you configure a key delivery policy, you must provide that password and hello .pfx file in Base64 format.</span></span>

      <span data-ttu-id="09876-137">Hello suit décrire comment toogenerate un certificat .pfx du fichier pour FairPlay :</span><span class="sxs-lookup"><span data-stu-id="09876-137">hello following steps describe how toogenerate a .pfx certificate file for FairPlay:</span></span>

    1. <span data-ttu-id="09876-138">Installez OpenSSL à partir de https://slproweb.com/products/Win32OpenSSL.html.</span><span class="sxs-lookup"><span data-stu-id="09876-138">Install OpenSSL from https://slproweb.com/products/Win32OpenSSL.html.</span></span>

        <span data-ttu-id="09876-139">Accédez toohello dossier certificat FairPlay de hello et d’autres fichiers fournies par Apple.</span><span class="sxs-lookup"><span data-stu-id="09876-139">Go toohello folder where hello FairPlay certificate and other files delivered by Apple are.</span></span>
    2. <span data-ttu-id="09876-140">Exécutez hello de commande suivante à partir de la ligne de commande hello.</span><span class="sxs-lookup"><span data-stu-id="09876-140">Run hello following command from hello command line.</span></span> <span data-ttu-id="09876-141">Cela convertit le fichier .pem tooa hello .cer fichier.</span><span class="sxs-lookup"><span data-stu-id="09876-141">This converts hello .cer file tooa .pem file.</span></span>

        <span data-ttu-id="09876-142">"C:\OpenSSL-Win32\bin\openssl.exe" x509 -inform der -in fairplay.cer -out fairplay-out.pem</span><span class="sxs-lookup"><span data-stu-id="09876-142">"C:\OpenSSL-Win32\bin\openssl.exe" x509 -inform der -in fairplay.cer -out fairplay-out.pem</span></span>
    3. <span data-ttu-id="09876-143">Exécutez hello de commande suivante à partir de la ligne de commande hello.</span><span class="sxs-lookup"><span data-stu-id="09876-143">Run hello following command from hello command line.</span></span> <span data-ttu-id="09876-144">Cela convertit le fichier .pfx tooa hello .pem fichier avec une clé privée de hello.</span><span class="sxs-lookup"><span data-stu-id="09876-144">This converts hello .pem file tooa .pfx file with hello private key.</span></span> <span data-ttu-id="09876-145">mot de passe Hello pour le fichier .pfx de hello est alors invité par OpenSSL.</span><span class="sxs-lookup"><span data-stu-id="09876-145">hello password for hello .pfx file is then asked by OpenSSL.</span></span>

        <span data-ttu-id="09876-146">"C:\OpenSSL-Win32\bin\openssl.exe" pkcs12 -export -out fairplay-out.pfx -inkey privatekey.pem -in fairplay-out.pem -passin file:privatekey-pem-pass.txt</span><span class="sxs-lookup"><span data-stu-id="09876-146">"C:\OpenSSL-Win32\bin\openssl.exe" pkcs12 -export -out fairplay-out.pfx -inkey privatekey.pem -in fairplay-out.pem -passin file:privatekey-pem-pass.txt</span></span>
  * <span data-ttu-id="09876-147">**Mot de passe de certificat de l’application**: mot de passe hello pour la création du fichier .pfx de hello.</span><span class="sxs-lookup"><span data-stu-id="09876-147">**App Cert password**: hello password for creating hello .pfx file.</span></span>
  * <span data-ttu-id="09876-148">**ID de mot de passe d’application Cert**: vous devez télécharger le mot de passe hello, toohow similaires, ils téléchargent d’autres clés de Media Services.</span><span class="sxs-lookup"><span data-stu-id="09876-148">**App Cert password ID**: You must upload hello password, similar toohow they upload other Media Services keys.</span></span> <span data-ttu-id="09876-149">Hello d’utilisation **ContentKeyType.FairPlayPfxPassword** hello de tooget de valeur enum ID de Media Services</span><span class="sxs-lookup"><span data-stu-id="09876-149">Use hello **ContentKeyType.FairPlayPfxPassword** enum value tooget hello Media Services ID.</span></span> <span data-ttu-id="09876-150">C’est ce qu’ils doivent toouse au sein de l’option de stratégie de distribution de clés hello.</span><span class="sxs-lookup"><span data-stu-id="09876-150">This is what they need toouse inside hello key delivery policy option.</span></span>
  * <span data-ttu-id="09876-151">**iv** : valeur aléatoire de 16 octets.</span><span class="sxs-lookup"><span data-stu-id="09876-151">**iv**: This is a random value of 16 bytes.</span></span> <span data-ttu-id="09876-152">Il doit correspondre au hello du vecteur d’initialisation dans la stratégie de remise hello actif.</span><span class="sxs-lookup"><span data-stu-id="09876-152">It must match hello iv in hello asset delivery policy.</span></span> <span data-ttu-id="09876-153">Vous générez hello iv et le placer dans deux emplacements : stratégie de livraison des actifs hello et option de stratégie de distribution de clés hello.</span><span class="sxs-lookup"><span data-stu-id="09876-153">You generate hello iv, and put it in both places: hello asset delivery policy and hello key delivery policy option.</span></span>
  * <span data-ttu-id="09876-154">**Demandez à**: cette clé est reçue lors de la génération de la certification de hello à l’aide du portail des développeurs Apple hello.</span><span class="sxs-lookup"><span data-stu-id="09876-154">**ASK**: This key is received when you generate hello certification by using hello Apple Developer portal.</span></span> <span data-ttu-id="09876-155">Chaque équipe de développement recevra une ASK unique.</span><span class="sxs-lookup"><span data-stu-id="09876-155">Each development team will receive a unique ASK.</span></span> <span data-ttu-id="09876-156">Enregistrer une copie de hello ASK et stockez-le dans un endroit sûr.</span><span class="sxs-lookup"><span data-stu-id="09876-156">Save a copy of hello ASK, and store it in a safe place.</span></span> <span data-ttu-id="09876-157">Vous aurez besoin ultérieurement tooconfigure ASK en tant que FairPlayAsk tooMedia Services.</span><span class="sxs-lookup"><span data-stu-id="09876-157">You will need tooconfigure ASK as FairPlayAsk tooMedia Services later.</span></span>
  * <span data-ttu-id="09876-158">**ASK ID (ID de clé ASK)** : cet ID est obtenu lorsque vous chargez la clé ASK dans Media Services.</span><span class="sxs-lookup"><span data-stu-id="09876-158">**ASK ID**: This ID is obtained when you upload ASK into Media Services.</span></span> <span data-ttu-id="09876-159">Vous devez télécharger poser à l’aide de hello **ContentKeyType.FairPlayAsk** valeur enum.</span><span class="sxs-lookup"><span data-stu-id="09876-159">You must upload ASK by using hello **ContentKeyType.FairPlayAsk** enum value.</span></span> <span data-ttu-id="09876-160">En tant que résultat de hello, hello Media Services ID est retournée, et c’est celui qui doit être utilisé lors de la définition d’option de stratégie de distribution de clés hello.</span><span class="sxs-lookup"><span data-stu-id="09876-160">As hello result, hello Media Services ID is returned, and this is what should be used when setting hello key delivery policy option.</span></span>

<span data-ttu-id="09876-161">Hello ce qui suit doit être défini par hello côté client de fréquence d’images :</span><span class="sxs-lookup"><span data-stu-id="09876-161">hello following things must be set by hello FPS client side:</span></span>

  * <span data-ttu-id="09876-162">**Application Cert (AC)**: il s’agit d’un fichier.cer/.der contenant la clé publique hello, système d’exploitation hello utilise tooencrypt certains charge.</span><span class="sxs-lookup"><span data-stu-id="09876-162">**App Cert (AC)**: This is a .cer/.der file that contains hello public key, which hello operating system uses tooencrypt some payload.</span></span> <span data-ttu-id="09876-163">Media Services doit tooknow concernant car il est requis par le lecteur hello.</span><span class="sxs-lookup"><span data-stu-id="09876-163">Media Services needs tooknow about it because it is required by hello player.</span></span> <span data-ttu-id="09876-164">service de distribution de clés Hello déchiffre à l’aide de la clé privée correspondante de hello.</span><span class="sxs-lookup"><span data-stu-id="09876-164">hello key delivery service decrypts it using hello corresponding private key.</span></span>

<span data-ttu-id="09876-165">tooplay un flux chiffré FairPlay, obtenez un véritable demander d’abord, puis générer un certificat réel.</span><span class="sxs-lookup"><span data-stu-id="09876-165">tooplay back a FairPlay encrypted stream, get a real ASK first, and then generate a real certificate.</span></span> <span data-ttu-id="09876-166">Ce processus crée les trois composants suivants :</span><span class="sxs-lookup"><span data-stu-id="09876-166">That process creates all three parts:</span></span>

  * <span data-ttu-id="09876-167">Fichier .der</span><span class="sxs-lookup"><span data-stu-id="09876-167">.der file</span></span>
  * <span data-ttu-id="09876-168">Fichier .pfx</span><span class="sxs-lookup"><span data-stu-id="09876-168">.pfx file</span></span>
  * <span data-ttu-id="09876-169">mot de passe pour hello .pfx</span><span class="sxs-lookup"><span data-stu-id="09876-169">password for hello .pfx</span></span>

<span data-ttu-id="09876-170">Hello clients suivants prennent en charge HLS avec **AES-128 CBC** chiffrement : Safari sur OS X, Apple TV, iOS.</span><span class="sxs-lookup"><span data-stu-id="09876-170">hello following clients support HLS with **AES-128 CBC** encryption: Safari on OS X, Apple TV, iOS.</span></span>

## <a name="configure-fairplay-dynamic-encryption-and-license-delivery-services"></a><span data-ttu-id="09876-171">Configurer le chiffrement dynamique FairPlay et des services de remise de licences</span><span class="sxs-lookup"><span data-stu-id="09876-171">Configure FairPlay dynamic encryption and license delivery services</span></span>
<span data-ttu-id="09876-172">Hello Voici les étapes générales pour la protection de vos éléments multimédias avec FairPlay à l’aide du service de remise de licences de Media Services hello et également à l’aide du chiffrement dynamique.</span><span class="sxs-lookup"><span data-stu-id="09876-172">hello following are general steps for protecting your assets with FairPlay by using hello Media Services license delivery service, and also by using dynamic encryption.</span></span>

1. <span data-ttu-id="09876-173">Créer un élément multimédia et télécharger des fichiers dans l’élément multimédia de hello.</span><span class="sxs-lookup"><span data-stu-id="09876-173">Create an asset, and upload files into hello asset.</span></span>
2. <span data-ttu-id="09876-174">Encoder asset hello contenant hello fichier toohello adaptive bitrate que MP4 set.</span><span class="sxs-lookup"><span data-stu-id="09876-174">Encode hello asset that contains hello file toohello adaptive bitrate MP4 set.</span></span>
3. <span data-ttu-id="09876-175">Créer une clé de contenu et l’associer à asset de hello encodé.</span><span class="sxs-lookup"><span data-stu-id="09876-175">Create a content key, and associate it with hello encoded asset.</span></span>  
4. <span data-ttu-id="09876-176">Configurez la stratégie d’autorisation de la clé de contenu hello.</span><span class="sxs-lookup"><span data-stu-id="09876-176">Configure hello content key’s authorization policy.</span></span> <span data-ttu-id="09876-177">Spécifiez hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="09876-177">Specify hello following:</span></span>

   * <span data-ttu-id="09876-178">méthode de remise Hello (dans ce cas, FairPlay).</span><span class="sxs-lookup"><span data-stu-id="09876-178">hello delivery method (in this case, FairPlay).</span></span>
   * <span data-ttu-id="09876-179">la configuration des options de stratégie FairPlay.</span><span class="sxs-lookup"><span data-stu-id="09876-179">FairPlay policy options configuration.</span></span> <span data-ttu-id="09876-180">Pour plus d’informations sur la façon de tooconfigure FairPlay, consultez hello **ConfigureFairPlayPolicyOptions()** méthode dans l’exemple hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="09876-180">For details on how tooconfigure FairPlay, see hello **ConfigureFairPlayPolicyOptions()** method in hello sample below.</span></span>

     > [!NOTE]
     > <span data-ttu-id="09876-181">En règle générale, vous souhaiteriez tooconfigure FairPlay stratégie n'options qu’une seule fois, car vous aurez qu’un ensemble de certification et un demandez.</span><span class="sxs-lookup"><span data-stu-id="09876-181">Usually, you would want tooconfigure FairPlay policy options only once, because you will only have one set of a certification and an ASK.</span></span>
     >
     >
   * <span data-ttu-id="09876-182">Les restrictions (d’ouverture ou jeton).</span><span class="sxs-lookup"><span data-stu-id="09876-182">Restrictions (open or token).</span></span>
   * <span data-ttu-id="09876-183">Informations spécifiques toohello clé type de remise qui définit comment la clé de hello est remis toohello client.</span><span class="sxs-lookup"><span data-stu-id="09876-183">Information specific toohello key delivery type that defines how hello key is delivered toohello client.</span></span>
5. <span data-ttu-id="09876-184">Configurer la stratégie de remise hello actif.</span><span class="sxs-lookup"><span data-stu-id="09876-184">Configure hello asset delivery policy.</span></span> <span data-ttu-id="09876-185">configuration de stratégie de livraison Hello inclut :</span><span class="sxs-lookup"><span data-stu-id="09876-185">hello delivery policy configuration includes:</span></span>

   * <span data-ttu-id="09876-186">protocole de livraison Hello (TLS).</span><span class="sxs-lookup"><span data-stu-id="09876-186">hello delivery protocol (HLS).</span></span>
   * <span data-ttu-id="09876-187">type Hello du chiffrement dynamique (chiffrement CBC commun).</span><span class="sxs-lookup"><span data-stu-id="09876-187">hello type of dynamic encryption (common CBC encryption).</span></span>
   * <span data-ttu-id="09876-188">URL d’acquisition de licence Hello.</span><span class="sxs-lookup"><span data-stu-id="09876-188">hello license acquisition URL.</span></span>

     > [!NOTE]
     > <span data-ttu-id="09876-189">Si vous voulez toodeliver un flux qui est chiffré avec FairPlay et un autre système de gestion des droits numériques (DRM), vous disposez des stratégies de remise distinct tooconfigure :</span><span class="sxs-lookup"><span data-stu-id="09876-189">If you want toodeliver a stream that is encrypted with FairPlay and another Digital Rights Management (DRM) system, you have tooconfigure separate delivery policies:</span></span>
     >
     > * <span data-ttu-id="09876-190">Un IAssetDeliveryPolicy tooconfigure dynamique diffusion adaptative en continu via HTTP (tiret) avec courantes chiffrement (CENC) (PlayReady + Widevine) et Smooth Streaming avec PlayReady</span><span class="sxs-lookup"><span data-stu-id="09876-190">One IAssetDeliveryPolicy tooconfigure Dynamic Adaptive Streaming over HTTP (DASH) with Common Encryption (CENC) (PlayReady + Widevine), and Smooth with PlayReady</span></span>
     > * <span data-ttu-id="09876-191">Un autre IAssetDeliveryPolicy tooconfigure FairPlay pour TLS</span><span class="sxs-lookup"><span data-stu-id="09876-191">Another IAssetDeliveryPolicy tooconfigure FairPlay for HLS</span></span>
     >
     >
6. <span data-ttu-id="09876-192">Créer un tooget de localisateur OnDemand une URL de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="09876-192">Create an OnDemand locator tooget a streaming URL.</span></span>

## <a name="use-fairplay-key-delivery-by-player-apps"></a><span data-ttu-id="09876-193">Utiliser la remise de clé FairPlay des applications de lecteur</span><span class="sxs-lookup"><span data-stu-id="09876-193">Use FairPlay key delivery by player apps</span></span>
<span data-ttu-id="09876-194">Vous pouvez développer des applications de lecteur à l’aide de hello, iOS SDK.</span><span class="sxs-lookup"><span data-stu-id="09876-194">You can develop player apps by using hello iOS SDK.</span></span> <span data-ttu-id="09876-195">tooplay en mesure de toobe FairPlay contenu, vous disposez de protocole d’échange de licence tooimplement hello.</span><span class="sxs-lookup"><span data-stu-id="09876-195">toobe able tooplay FairPlay content, you have tooimplement hello license exchange protocol.</span></span> <span data-ttu-id="09876-196">Ce protocole n’est pas spécifié par Apple.</span><span class="sxs-lookup"><span data-stu-id="09876-196">This protocol is not specified by Apple.</span></span> <span data-ttu-id="09876-197">Il est de l’application tooeach la distribution de clés toosend demande.</span><span class="sxs-lookup"><span data-stu-id="09876-197">It is up tooeach app how toosend key delivery requests.</span></span> <span data-ttu-id="09876-198">Hello service de distribution de clés de Media Services FairPlay attend hello SPC toocome comme un message encodé post www-form-url, Bonjour suivant du formulaire :</span><span class="sxs-lookup"><span data-stu-id="09876-198">hello Media Services FairPlay key delivery service expects hello SPC toocome as a www-form-url encoded post message, in hello following form:</span></span>

    spc=<Base64 encoded SPC>

> [!NOTE]
> <span data-ttu-id="09876-199">Azure Media Player ne prend pas en charge la lecture de FairPlay prédéfinies hello.</span><span class="sxs-lookup"><span data-stu-id="09876-199">Azure Media Player doesn’t support FairPlay playback out of hello box.</span></span> <span data-ttu-id="09876-200">lecture de FairPlay tooget sur MAC OS X, obtenir le lecteur exemple hello de hello compte de développeur Apple.</span><span class="sxs-lookup"><span data-stu-id="09876-200">tooget FairPlay playback on MAC OS X, obtain hello sample player from hello Apple developer account.</span></span>
>
>

## <a name="streaming-urls"></a><span data-ttu-id="09876-201">URL de diffusion</span><span class="sxs-lookup"><span data-stu-id="09876-201">Streaming URLs</span></span>
<span data-ttu-id="09876-202">Si votre élément multimédia a été chiffré avec plusieurs DRM, vous devez utiliser une balise de chiffrement dans les URL de diffusion en continu de hello : (format = 'm3u8-aapl', chiffrement = 'xxx').</span><span class="sxs-lookup"><span data-stu-id="09876-202">If your asset was encrypted with more than one DRM, you should use an encryption tag in hello streaming URL: (format='m3u8-aapl', encryption='xxx').</span></span>

<span data-ttu-id="09876-203">Hello suivant considérations s’appliquent :</span><span class="sxs-lookup"><span data-stu-id="09876-203">hello following considerations apply:</span></span>

* <span data-ttu-id="09876-204">Seul zéro ou un type de chiffrement peut être spécifié.</span><span class="sxs-lookup"><span data-stu-id="09876-204">Only zero or one encryption type can be specified.</span></span>
* <span data-ttu-id="09876-205">type de chiffrement Hello ne toobe spécifié dans les URL de hello si seul un chiffrement a été appliqué toohello actif.</span><span class="sxs-lookup"><span data-stu-id="09876-205">hello encryption type doesn't have toobe specified in hello URL if only one encryption was applied toohello asset.</span></span>
* <span data-ttu-id="09876-206">type de chiffrement Hello respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="09876-206">hello encryption type is case insensitive.</span></span>
* <span data-ttu-id="09876-207">Hello, les types de chiffrement suivants peut être spécifié :</span><span class="sxs-lookup"><span data-stu-id="09876-207">hello following encryption types can be specified:</span></span>  
  * <span data-ttu-id="09876-208">**cenc** : chiffrement commun (Playready ou Widevine)</span><span class="sxs-lookup"><span data-stu-id="09876-208">**cenc**:  Common encryption (PlayReady or Widevine)</span></span>
  * <span data-ttu-id="09876-209">**cbcs-aapl** : Fairplay</span><span class="sxs-lookup"><span data-stu-id="09876-209">**cbcs-aapl**: FairPlay</span></span>
  * <span data-ttu-id="09876-210">**cbc** : chiffrement de l’enveloppe AES</span><span class="sxs-lookup"><span data-stu-id="09876-210">**cbc**: AES envelope encryption</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="09876-211">Créer et configurer un projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="09876-211">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="09876-212">Configurer votre environnement de développement et de remplir le fichier app.config de hello avec les informations de connexion, comme décrit dans [développement Media Services avec .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="09876-212">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="09876-213">Ajouter hello suivant éléments trop**appSettings** défini dans votre fichier app.config :</span><span class="sxs-lookup"><span data-stu-id="09876-213">Add hello following elements too**appSettings** defined in your app.config file:</span></span>

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a><span data-ttu-id="09876-214">Exemple</span><span class="sxs-lookup"><span data-stu-id="09876-214">Example</span></span>

<span data-ttu-id="09876-215">Hello suivant l’exemple montre hello capacité toouse Media Services toodeliver votre contenu chiffré avec FairPlay.</span><span class="sxs-lookup"><span data-stu-id="09876-215">hello following sample demonstrates hello ability toouse Media Services toodeliver your content encrypted with FairPlay.</span></span> <span data-ttu-id="09876-216">Cette fonctionnalité a été introduite dans hello Azure Media Services SDK pour .NET version 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="09876-216">This functionality was introduced in hello Azure Media Services SDK for .NET version 3.6.0.</span></span> 

<span data-ttu-id="09876-217">Remplacer le code hello dans votre fichier Program.cs avec le code hello présenté dans cette section.</span><span class="sxs-lookup"><span data-stu-id="09876-217">Overwrite hello code in your Program.cs file with hello code shown in this section.</span></span>

>[!NOTE]
><span data-ttu-id="09876-218">Un nombre limite de 1 000 000 a été défini pour les différentes stratégies AMS (par exemple, pour la stratégie de localisateur ou pour ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="09876-218">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="09876-219">Vous devez utiliser hello ID de stratégie même si vous utilisez toujours hello même jours / autorisations d’accès, par exemple, les stratégies pour les localisateurs sont tooremain prévue en place pendant une longue période (non-téléchargement stratégies).</span><span class="sxs-lookup"><span data-stu-id="09876-219">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="09876-220">Pour plus d’informations, consultez [cette rubrique](media-services-dotnet-manage-entities.md#limit-access-policies) .</span><span class="sxs-lookup"><span data-stu-id="09876-220">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="09876-221">Assurez-vous que tooupdate variables toopoint toofolders où se trouvent vos fichiers d’entrée.</span><span class="sxs-lookup"><span data-stu-id="09876-221">Make sure tooupdate variables toopoint toofolders where your input files are located.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Threading;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;
    using Microsoft.WindowsAzure.MediaServices.Client.FairPlay;
    using Newtonsoft.Json;
    using System.Security.Cryptography.X509Certificates;

    namespace DynamicEncryptionWithFairPlay
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

            IContentKey key = CreateCommonCBCTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
            Console.WriteLine("FairPlay License Key delivery URL: {0}", key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay));
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

            string url = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Encrypted HLS URL: {0}/manifest(format=m3u8-aapl)", url);

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

            IJob job = _context.Jobs.Create(String.Format("Encoding {0}", inputAsset.Name));

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

        static public IContentKey CreateCommonCBCTypeContentKey(IAsset asset)
        {
            // Create HLS SAMPLE AES encryption content key
            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                        keyId,
                        contentKey,
                        "ContentKey",
                        ContentKeyType.CommonEncryptionCbcs);

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


            // Configure FairPlay policy option.
            string FairPlayConfiguration = ConfigureFairPlayPolicyOptions();

            IContentKeyAuthorizationPolicyOption FairPlayPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
            ContentKeyDeliveryType.FairPlay,
            restrictions,
            FairPlayConfiguration);


            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common CBC Content Key with no restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(FairPlayPolicy);

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

            // Configure FairPlay policy option.
            string FairPlayConfiguration = ConfigureFairPlayPolicyOptions();


            IContentKeyAuthorizationPolicyOption FairPlayPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                   ContentKeyDeliveryType.FairPlay,
                   restrictions,
                   FairPlayConfiguration);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common CBC Content Key with token restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(FairPlayPolicy);

            // Associate hello content key authorization policy with hello content key
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;

            return tokenTemplateString;
        }

        private static string ConfigureFairPlayPolicyOptions()
        {
            // For testing you can provide all zeroes for ASK bytes together with hello cert from Apple FPS SDK.
            // However, for production you must use a real ASK from Apple bound tooa real prod certificate.
            byte[] askBytes = Guid.NewGuid().ToByteArray();
            var askId = Guid.NewGuid();
            // Key delivery retrieves askKey by askId and uses this key toogenerate hello response.
            IContentKey askKey = _context.ContentKeys.Create(
                        askId,
                        askBytes,
                        "askKey",
                        ContentKeyType.FairPlayASk);

            //Customer password for creating hello .pfx file.
            string pfxPassword = "<customer password for creating hello .pfx file>";
            // Key delivery retrieves pfxPasswordKey by pfxPasswordId and uses this key toogenerate hello response.
            var pfxPasswordId = Guid.NewGuid();
            byte[] pfxPasswordBytes = System.Text.Encoding.UTF8.GetBytes(pfxPassword);
            IContentKey pfxPasswordKey = _context.ContentKeys.Create(
                        pfxPasswordId,
                        pfxPasswordBytes,
                        "pfxPasswordKey",
                        ContentKeyType.FairPlayPfxPassword);

            // iv - 16 bytes random value, must match hello iv in hello asset delivery policy.
            byte[] iv = Guid.NewGuid().ToByteArray();

            //Specify hello .pfx file created by hello customer.
            var appCert = new X509Certificate2("path toohello .pfx file created by hello customer", pfxPassword, X509KeyStorageFlags.Exportable);

            string FairPlayConfiguration =
            Microsoft.WindowsAzure.MediaServices.Client.FairPlay.FairPlayConfiguration.CreateSerializedFairPlayOptionConfiguration(
                appCert,
                pfxPassword,
                pfxPasswordId,
                askId,
                iv);

            return FairPlayConfiguration;
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

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            var kdPolicy = _context.ContentKeyAuthorizationPolicies.Where(p => p.Id == key.AuthorizationPolicyId).Single();

            var kdOption = kdPolicy.Options.Single(o => o.KeyDeliveryType == ContentKeyDeliveryType.FairPlay);

            FairPlayConfiguration configFP = JsonConvert.DeserializeObject<FairPlayConfiguration>(kdOption.KeyDeliveryConfiguration);

            // Get hello FairPlay license service URL.
            Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay);

            // hello reason hello below code replaces "https://" with "skd://" is because
            // in hello IOS player sample code which you obtained in Apple developer account,
            // hello player only recognizes a Key URL that starts with skd://.
            // However, if you are using a customized player,
            // you can choose whatever protocol you want.
            // For example, "https".

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                    {AssetDeliveryPolicyConfigurationKey.FairPlayLicenseAcquisitionUrl, acquisitionUrl.ToString().Replace("https://", "skd://")},
                    {AssetDeliveryPolicyConfigurationKey.CommonEncryptionIVForCbcs, configFP.ContentEncryptionIV}
            };

            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryptionCbcs,
            AssetDeliveryProtocol.HLS,
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


## <a name="next-steps-media-services-learning-paths"></a><span data-ttu-id="09876-222">Étapes suivantes : Parcours d’apprentissage Media Services</span><span class="sxs-lookup"><span data-stu-id="09876-222">Next steps: Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="09876-223">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="09876-223">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
