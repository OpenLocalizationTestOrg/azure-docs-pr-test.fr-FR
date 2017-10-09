---
title: "à l’aide des stratégies de protection du contenu aaaConfiguring hello portail Azure | Documents Microsoft"
description: "Cet article explique comment toouse hello des stratégies de protection du contenu tooconfigure portail Azure. Hello article également montre comment le chiffrement dynamique tooenable pour vos ressources."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 270b3272-7411-40a9-ad42-5acdbba31154
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: juliako
ms.openlocfilehash: 3e7ce6ddaa0e738b5a1e26dafe9eef2df221f039
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-content-protection-policies-using-hello-azure-portal"></a><span data-ttu-id="16998-104">Configuration des stratégies de protection du contenu à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="16998-104">Configuring content protection policies using hello Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="16998-105">toocomplete ce didacticiel, vous avez besoin d’un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="16998-105">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="16998-106">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="16998-106">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="16998-107">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="16998-107">Overview</span></span>
<span data-ttu-id="16998-108">Microsoft Azure Media Services (AMS) permet de vous toosecure votre média à partir de l’heure hello qu'il quitte votre ordinateur via le stockage, le traitement et la remise.</span><span class="sxs-lookup"><span data-stu-id="16998-108">Microsoft Azure Media Services (AMS) enables you toosecure your media from hello time it leaves your computer through storage, processing, and delivery.</span></span> <span data-ttu-id="16998-109">Media Services vous permet de toodeliver votre contenu chiffré dynamiquement avec Advanced Encryption Standard (AES) (à l’aide de clés de chiffrement 128 bits), chiffrement commun (CENC) à l’aide de PlayReady et/ou Widevine DRM et FairPlay d’Apple.</span><span class="sxs-lookup"><span data-stu-id="16998-109">Media Services allows you toodeliver your content encrypted dynamically with Advanced Encryption Standard (AES) (using 128-bit encryption keys), common encryption (CENC) using PlayReady and/or Widevine DRM, and Apple FairPlay.</span></span> 

<span data-ttu-id="16998-110">AMS fournit un service de fourniture de licences DRM et les clients tooauthorized de clés en clair AES.</span><span class="sxs-lookup"><span data-stu-id="16998-110">AMS provides a service for delivering DRM licenses and AES clear keys tooauthorized clients.</span></span> <span data-ttu-id="16998-111">Hello portail Azure vous permet de toocreate un **stratégie d’autorisation de clé/licence** pour tous les types de chiffrements.</span><span class="sxs-lookup"><span data-stu-id="16998-111">hello Azure portal enables you toocreate one **key/license authorization policy** for all types of encryptions.</span></span>

<span data-ttu-id="16998-112">Cet article explique comment tooconfigure avec hello portail Azure, les stratégies de protection de contenu.</span><span class="sxs-lookup"><span data-stu-id="16998-112">This article demonstrates how tooconfigure content protection policies with hello Azure portal.</span></span> <span data-ttu-id="16998-113">Hello article également montre comment actifs de tooyour tooapply chiffrement dynamique.</span><span class="sxs-lookup"><span data-stu-id="16998-113">hello article also shows how tooapply dynamic encryption tooyour assets.</span></span>


> [!NOTE]
> <span data-ttu-id="16998-114">Si vous avez utilisé des stratégies de protection toocreate de portail classique Azure hello, les stratégies de hello ne peuvent pas apparaître dans hello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="16998-114">If you used hello Azure classic portal toocreate protection policies, hello policies may not appear in hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="16998-115">Toutefois, hello toutes les anciennes stratégies toujours existe.</span><span class="sxs-lookup"><span data-stu-id="16998-115">However, all hello old polices still exist.</span></span> <span data-ttu-id="16998-116">Vous pouvez les examiner à l’aide de hello Azure Media Services .NET SDK ou hello [-Media--Explorateur des Services Azure](https://github.com/Azure/Azure-Media-Services-Explorer/releases) outil (stratégies de hello toosee, avec le bouton droit sur l’élément multimédia de hello -> Affichage des informations (F4) -> cliquez sur l’onglet -> clés de contenu Cliquez sur la clé de hello).</span><span class="sxs-lookup"><span data-stu-id="16998-116">You can examine them using hello Azure Media Services .NET SDK or hello [Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer/releases) tool (toosee hello policies, right-click on hello asset -> Display information (F4)->click on Content keys tab-> click on hello key).</span></span> 
> 
> <span data-ttu-id="16998-117">Si vous souhaitez tooencrypt votre élément multimédia à l’aide des nouvelles stratégies, configurez-les avec hello portail Azure, cliquez sur Enregistrer et appliquer le chiffrement dynamique.</span><span class="sxs-lookup"><span data-stu-id="16998-117">If you want tooencrypt your asset using new policies, configure them with hello Azure portal, click save, and reapply dynamic encryption.</span></span> 
> 
> 

## <a name="start-configuring-content-protection"></a><span data-ttu-id="16998-118">Commencer à configurer la protection de contenu</span><span class="sxs-lookup"><span data-stu-id="16998-118">Start configuring content protection</span></span>
<span data-ttu-id="16998-119">les toostart portail hello toouse configuration de la protection de contenu, tooyour global AMS compte, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="16998-119">toouse hello portal toostart configuring content protection, global tooyour AMS account, do hello following:</span></span>

1. <span data-ttu-id="16998-120">Bonjour [portail Azure](https://portal.azure.com/), sélectionnez votre compte Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="16998-120">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="16998-121">Sélectionnez **Paramètres** > **Protection du contenu**.</span><span class="sxs-lookup"><span data-stu-id="16998-121">Select **Settings** > **Content protection**.</span></span>

![Protéger du contenu](./media/media-services-portal-content-protection/media-services-content-protection001.png)

## <a name="keylicense-authorization-policy"></a><span data-ttu-id="16998-123">stratégie d’autorisation de clé/licence</span><span class="sxs-lookup"><span data-stu-id="16998-123">Key/license authorization policy</span></span>
<span data-ttu-id="16998-124">AMS prend en charge plusieurs méthodes d’authentification des utilisateurs effectuant des demandes de clé ou de licence.</span><span class="sxs-lookup"><span data-stu-id="16998-124">AMS supports multiple ways of authenticating users who make key or license requests.</span></span> <span data-ttu-id="16998-125">stratégie d’autorisation de clé contenu de Hello doit être configurée par vous et appliquée par votre client pour hello clé/licence toobe toohello delived client.</span><span class="sxs-lookup"><span data-stu-id="16998-125">hello content key authorization policy must be configured by you and met by your client in order for hello key/license toobe delived toohello client.</span></span> <span data-ttu-id="16998-126">Hello contenu clé peut avoir une ou plusieurs restrictions d’autorisation : **ouvrir** ou **jeton** restriction.</span><span class="sxs-lookup"><span data-stu-id="16998-126">hello content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span>

<span data-ttu-id="16998-127">Hello portail Azure vous permet de toocreate un **stratégie d’autorisation de clé/licence** pour tous les types de chiffrements.</span><span class="sxs-lookup"><span data-stu-id="16998-127">hello Azure portal enables you toocreate one **key/license authorization policy** for all types of encryptions.</span></span>

### <a name="open"></a><span data-ttu-id="16998-128">Ouverts</span><span class="sxs-lookup"><span data-stu-id="16998-128">Open</span></span>
<span data-ttu-id="16998-129">Restriction Open signifie que hello système fournit des tooanyone clé hello qui fait la demande.</span><span class="sxs-lookup"><span data-stu-id="16998-129">Open restriction means that hello system will deliver hello key tooanyone who makes a key request.</span></span> <span data-ttu-id="16998-130">Cette restriction peut être utile à des fins de test.</span><span class="sxs-lookup"><span data-stu-id="16998-130">This restriction might be useful for test purposes.</span></span> 

### <a name="token"></a><span data-ttu-id="16998-131">Jeton</span><span class="sxs-lookup"><span data-stu-id="16998-131">Token</span></span>
<span data-ttu-id="16998-132">stratégie de restriction token Hello doit être accompagné d’un jeton émis par un Service (jeton de sécurité).</span><span class="sxs-lookup"><span data-stu-id="16998-132">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="16998-133">Media Services prend en charge les jetons dans les formats de jetons SWT (Simple Web Tokens) hello et JSON Web Token (JWT).</span><span class="sxs-lookup"><span data-stu-id="16998-133">Media Services supports tokens in hello Simple Web Tokens (SWT) format and JSON Web Token (JWT) format.</span></span> <span data-ttu-id="16998-134">Media Services ne fournit pas de services de jeton sécurisé.</span><span class="sxs-lookup"><span data-stu-id="16998-134">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="16998-135">Vous pouvez créer un STS personnalisé ou tirer parti des jetons de tooissue Microsoft Azure ACS.</span><span class="sxs-lookup"><span data-stu-id="16998-135">You can create a custom STS or leverage Microsoft Azure ACS tooissue tokens.</span></span> <span data-ttu-id="16998-136">Hello STS doit être configuré toocreate un jeton signé avec hello spécifié clé et émettre les revendications que vous avez spécifié dans la configuration de restriction token hello.</span><span class="sxs-lookup"><span data-stu-id="16998-136">hello STS must be configured toocreate a token signed with hello specified key and issue claims that you specified in hello token restriction configuration.</span></span> <span data-ttu-id="16998-137">les revendications Hello Media Services, service de distribution de clés renvoie hello demandé hello et clé (ou licence) client toohello si hello jeton est valide dans hello jeton correspondent à celles configurées pour la clé de hello (ou licence).</span><span class="sxs-lookup"><span data-stu-id="16998-137">hello Media Services key delivery service will return hello requested key (or license) toohello client if hello token is valid and hello claims in hello token match those configured for hello key (or license).</span></span>

<span data-ttu-id="16998-138">Lorsque vous configurez la stratégie de restriction token hello, vous devez spécifier la clé de vérification principale hello, l’émetteur et des paramètres de l’audience.</span><span class="sxs-lookup"><span data-stu-id="16998-138">When configuring hello token restricted policy, you must specify hello primary verification key, issuer, and audience parameters.</span></span> <span data-ttu-id="16998-139">clé de vérification principale Hello contient hello clé que le jeton de hello a été signé avec, l’émetteur est hello sécurisé STS qui émet le jeton de hello.</span><span class="sxs-lookup"><span data-stu-id="16998-139">hello primary verification key contains hello key that hello token was signed with, issuer is hello secure token service that issues hello token.</span></span> <span data-ttu-id="16998-140">audience Hello (parfois appelé étendue) décrit l’intention de hello du jeton de hello ou autorise l’accès au jeton de hello ressource hello.</span><span class="sxs-lookup"><span data-stu-id="16998-140">hello audience (sometimes called scope) describes hello intent of hello token or hello resource hello token authorizes access to.</span></span> <span data-ttu-id="16998-141">Hello service de distribution de clés de Media Services valide que ces valeurs dans le jeton de hello correspondent aux valeurs hello modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="16998-141">hello Media Services key delivery service validates that these values in hello token match hello values in hello template.</span></span>

![Protéger du contenu](./media/media-services-portal-content-protection/media-services-content-protection002.png)

## <a name="playready-rights-template"></a><span data-ttu-id="16998-143">Modèle de droits PlayReady</span><span class="sxs-lookup"><span data-stu-id="16998-143">PlayReady rights template</span></span>
<span data-ttu-id="16998-144">Pour obtenir des informations détaillées sur le modèle de droits hello PlayReady, consultez [vue d’ensemble du modèle de licence PlayReady Media Services](media-services-playready-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="16998-144">For detailed information about hello PlayReady rights template, see [Media Services PlayReady License Template Overview](media-services-playready-license-template-overview.md).</span></span>

### <a name="non-persistent"></a><span data-ttu-id="16998-145">Non persistante</span><span class="sxs-lookup"><span data-stu-id="16998-145">Non persistent</span></span>
<span data-ttu-id="16998-146">Si vous configurez la licence comme non persistant, il est uniquement conservée en mémoire pendant que le lecteur hello est à l’aide de licence de hello.</span><span class="sxs-lookup"><span data-stu-id="16998-146">If you configure license as non-persistent, it is only held in memory while hello player is using hello license.</span></span>  

![Protéger du contenu](./media/media-services-portal-content-protection/media-services-content-protection003.png)

### <a name="persistent"></a><span data-ttu-id="16998-148">Persistante</span><span class="sxs-lookup"><span data-stu-id="16998-148">Persistent</span></span>
<span data-ttu-id="16998-149">Si vous configurez la licence de hello comme persistant, il est enregistré dans un stockage persistant sur le client de hello.</span><span class="sxs-lookup"><span data-stu-id="16998-149">If you configure hello license  as persistent, it is saved in persistent storage on hello client.</span></span>

![Protéger du contenu](./media/media-services-portal-content-protection/media-services-content-protection004.png)

## <a name="widevine-rights-template"></a><span data-ttu-id="16998-151">Modèle de droits Widevine</span><span class="sxs-lookup"><span data-stu-id="16998-151">Widevine rights template</span></span>
<span data-ttu-id="16998-152">Pour obtenir des informations détaillées sur le modèle de droits Widevine hello, consultez [vue d’ensemble des modèles de licence Widevine](media-services-widevine-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="16998-152">For detailed information about hello Widevine rights template, see [Widevine License Template Overview](media-services-widevine-license-template-overview.md).</span></span>

### <a name="basic"></a><span data-ttu-id="16998-153">De base</span><span class="sxs-lookup"><span data-stu-id="16998-153">Basic</span></span>
<span data-ttu-id="16998-154">Lorsque vous sélectionnez **base**, hello modèle sera créé avec toutes les valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="16998-154">When you select **Basic**, hello template will be created with all defaults values.</span></span>

### <a name="advanced"></a><span data-ttu-id="16998-155">Avancé</span><span class="sxs-lookup"><span data-stu-id="16998-155">Advanced</span></span>
<span data-ttu-id="16998-156">Pour obtenir une explication détaillée sur l’option avancée des configurations Widevine, consultez [cette](media-services-widevine-license-template-overview.md) rubrique.</span><span class="sxs-lookup"><span data-stu-id="16998-156">For detailed explanation about advance option of Widevine configurations, see [this](media-services-widevine-license-template-overview.md) topic.</span></span>

![Protéger du contenu](./media/media-services-portal-content-protection/media-services-content-protection005.png)

## <a name="fairplay-configuration"></a><span data-ttu-id="16998-158">Configuration de FairPlay</span><span class="sxs-lookup"><span data-stu-id="16998-158">FairPlay configuration</span></span>
<span data-ttu-id="16998-159">le chiffrement FairPlay tooenable, vous avez besoin tooprovide hello certificat de l’application et la clé de Secret d’Application (demandez) via hello option de Configuration de FairPlay.</span><span class="sxs-lookup"><span data-stu-id="16998-159">tooenable FairPlay encryption, you need tooprovide hello App Certificate and Application Secret Key (ASK) through hello FairPlay Configuration option.</span></span> <span data-ttu-id="16998-160">Pour obtenir des informations détaillées sur la configuration de FairPlay et de la configuration requise, consultez [cet](media-services-protect-hls-with-fairplay.md) article.</span><span class="sxs-lookup"><span data-stu-id="16998-160">For detailed information about FairPlay configuration and requirements, see [this](media-services-protect-hls-with-fairplay.md) article.</span></span>

![Protéger du contenu](./media/media-services-portal-content-protection/media-services-content-protection006.png)

## <a name="apply-dynamic-encryption-tooyour-asset"></a><span data-ttu-id="16998-162">Appliquer asset tooyour de chiffrement dynamique</span><span class="sxs-lookup"><span data-stu-id="16998-162">Apply dynamic encryption tooyour asset</span></span>
<span data-ttu-id="16998-163">tootake parti du chiffrement dynamique, vous devez tooencode votre fichier source en un ensemble de fichiers MP4 à débit adaptatif.</span><span class="sxs-lookup"><span data-stu-id="16998-163">tootake advantage of dynamic encryption, you need tooencode your source file into a set of adaptive-bitrate MP4 files.</span></span>

### <a name="select-an-asset-that-you-want-tooencrypt"></a><span data-ttu-id="16998-164">Sélectionnez un élément multimédia que vous souhaitez tooencrypt</span><span class="sxs-lookup"><span data-stu-id="16998-164">Select an asset that you want tooencrypt</span></span>
<span data-ttu-id="16998-165">sélectionner de tous vos actifs, toosee **paramètres** > **actifs**.</span><span class="sxs-lookup"><span data-stu-id="16998-165">toosee all your assets, select **Settings** > **Assets**.</span></span>

![Protéger du contenu](./media/media-services-portal-content-protection/media-services-content-protection007.png)

### <a name="encrypt-with-aes-or-drm"></a><span data-ttu-id="16998-167">Chiffrer avec AES ou DRM</span><span class="sxs-lookup"><span data-stu-id="16998-167">Encrypt with AES or DRM</span></span>
<span data-ttu-id="16998-168">Quand vous appuyez sur **Chiffrer** sur un élément multimédia, deux options s’offrent à vous : **AES** ou **DRM**.</span><span class="sxs-lookup"><span data-stu-id="16998-168">Once you press **Encrypt** on an asset, you are presented wtih two choices: **AES** or **DRM**.</span></span> 

#### <a name="aes"></a><span data-ttu-id="16998-169">AES</span><span class="sxs-lookup"><span data-stu-id="16998-169">AES</span></span>
<span data-ttu-id="16998-170">Le chiffrement de clé en clair est activé sur tous les protocoles de diffusion en continu : Smooth Streaming, HLS et MPEG-DASH.</span><span class="sxs-lookup"><span data-stu-id="16998-170">AES clear key encryption will be enabled on all streaming protocols: Smooth Streaming, HLS, and MPEG-DASH.</span></span>

![Protéger du contenu](./media/media-services-portal-content-protection/media-services-content-protection008.png)

#### <a name="drm"></a><span data-ttu-id="16998-172">DRM</span><span class="sxs-lookup"><span data-stu-id="16998-172">DRM</span></span>
<span data-ttu-id="16998-173">Lorsque vous sélectionnez hello DRM onglet, vous sont présentées avec différents choix de stratégies de protection du contenu (qui, vous devez configurer à ce stade) + d’un ensemble de protocoles de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="16998-173">When you select hello DRM tab, you are presented with different choices of content protection policies (which you must have configured by now) + a set of streaming protocols.</span></span>

* <span data-ttu-id="16998-174">**PlayReady et Widevine avec MPEG-DASH** : chiffre dynamiquement votre flux MPEG-DASH avec les DRM PlayReady et Widevine.</span><span class="sxs-lookup"><span data-stu-id="16998-174">**PlayReady and Widevine with MPEG-DASH** - will dynamically encrypt your MPEG-DASH stream with PlayReady and Widevine DRMs.</span></span>
* <span data-ttu-id="16998-175">**PlayReady et Widevine avec MPEG-DASH+ FairPlay avec HLS** : chiffre dynamiquement votre flux MPEG-DASH avec les DRM PlayReady et Widevine.</span><span class="sxs-lookup"><span data-stu-id="16998-175">**PlayReady and Widevine with MPEG-DASH + FairPlay with HLS** - will dynamically encrypt you MPEG-DASH stream with PlayReady and Widevine DRMs.</span></span> <span data-ttu-id="16998-176">Chiffre également vos flux HLS avec FairPlay.</span><span class="sxs-lookup"><span data-stu-id="16998-176">Will also encrypt your HLS streams with FairPlay.</span></span>
* <span data-ttu-id="16998-177">**PlayReady uniquement avec Smooth Streaming, HLS et MPEG-DASH** : chiffre dynamiquement les flux Smooth Streaming, HLS, MPEG-DASH avec la DRM PlayReady.</span><span class="sxs-lookup"><span data-stu-id="16998-177">**PlayReady only with Smooth Streaming, HLS and MPEG-DASH** - will dynamically encrypt Smooth Streaming, HLS, MPEG-DASH streams with PlayReady DRM.</span></span>
* <span data-ttu-id="16998-178">**Widevine uniquement avec MPEG-DASH** : chiffre dynamiquement votre MPEG-DASH avec la DRM Widevine.</span><span class="sxs-lookup"><span data-stu-id="16998-178">**Widevine only with MPEG-DASH** - will dynamically encrypt you MPEG-DASH with Widevine DRM.</span></span>
* <span data-ttu-id="16998-179">**FairPlay uniquement avec HLS** : chiffre dynamiquement votre flux HLS avec FairPlay.</span><span class="sxs-lookup"><span data-stu-id="16998-179">**FairPlay only with HLS** - will dynamically encrypt your HLS stream with FairPlay.</span></span>

<span data-ttu-id="16998-180">le chiffrement FairPlay tooenable, vous avez besoin tooprovide hello certificat de l’application et la clé de Secret d’Application (demandez) via hello option FairPlay Configuration du Panneau de paramètres de Protection du contenu hello.</span><span class="sxs-lookup"><span data-stu-id="16998-180">tooenable FairPlay encryption, you need tooprovide hello App Certificate and Application Secret Key (ASK) through hello FairPlay Configuration option of hello Content Protection settings blade.</span></span>

![Protéger du contenu](./media/media-services-portal-content-protection/media-services-content-protection009.png)

<span data-ttu-id="16998-182">Une fois votre sélection du chiffrement hello, appuyez sur **appliquer**.</span><span class="sxs-lookup"><span data-stu-id="16998-182">Once you make hello encryption selection, press **Apply**.</span></span>

>[!NOTE] 
><span data-ttu-id="16998-183">Si vous envisagez de tooplay une AES chiffrée TLS dans Safari, consultez [ce billet de blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span><span class="sxs-lookup"><span data-stu-id="16998-183">If you are planning tooplay an AES encrypted HLS in Safari, see [this blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="16998-184">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="16998-184">Next steps</span></span>
<span data-ttu-id="16998-185">Consultez les parcours d’apprentissage de Media Services.</span><span class="sxs-lookup"><span data-stu-id="16998-185">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="16998-186">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="16998-186">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

