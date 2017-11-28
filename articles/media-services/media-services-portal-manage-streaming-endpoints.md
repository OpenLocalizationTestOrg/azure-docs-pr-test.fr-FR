---
title: aaaManage de diffusion en continu des points de terminaison avec hello portail Azure | Documents Microsoft
description: Cette rubrique montre comment les points de terminaison de diffusion en continu toomanage avec hello portail Azure.
services: media-services
documentationcenter: 
author: Juliako
writer: juliako
manager: cfowler
editor: 
ms.assetid: bb1aca25-d23a-4520-8c45-44ef3ecd5371
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: dfa9352894d37edb317a6334d7f109419deb362b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-streaming-endpoints-with-hello-azure-portal"></a><span data-ttu-id="ef65f-103">Gérer les points de terminaison de diffusion en continu avec hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="ef65f-103">Manage streaming endpoints with hello Azure portal</span></span>

<span data-ttu-id="ef65f-104">Cette rubrique montre comment toouse hello toomanage portail Azure les points de terminaison de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="ef65f-104">This topic shows  how toouse hello Azure portal toomanage streaming endpoints.</span></span> 

>[!NOTE]
><span data-ttu-id="ef65f-105">Assurez-vous que tooreview hello [vue d’ensemble](media-services-streaming-endpoints-overview.md) rubrique.</span><span class="sxs-lookup"><span data-stu-id="ef65f-105">Make sure tooreview hello [overview](media-services-streaming-endpoints-overview.md) topic.</span></span> 

<span data-ttu-id="ef65f-106">Pour plus d’informations sur la façon dont tooscale hello point de terminaison de diffusion en continu, consultez [cela](media-services-portal-scale-streaming-endpoints.md) rubrique.</span><span class="sxs-lookup"><span data-stu-id="ef65f-106">For information about how tooscale hello streaming endpoint, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <a name="start-managing-streaming-endpoints"></a><span data-ttu-id="ef65f-107">Commencer à gérer des points de terminaison de streaming</span><span class="sxs-lookup"><span data-stu-id="ef65f-107">Start managing streaming endpoints</span></span> 

<span data-ttu-id="ef65f-108">toostart la gestion des points de terminaison de diffusion en continu de votre compte, procédez comme hello suivant.</span><span class="sxs-lookup"><span data-stu-id="ef65f-108">toostart managing streaming endpoints for your account, do hello following.</span></span>

1. <span data-ttu-id="ef65f-109">Bonjour [portail Azure](https://portal.azure.com/), sélectionnez votre compte Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="ef65f-109">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="ef65f-110">Bonjour **paramètres** panneau, sélectionnez **points de terminaison de diffusion en continu**.</span><span class="sxs-lookup"><span data-stu-id="ef65f-110">In hello **Settings** blade, select **Streaming endpoints**.</span></span>
   
    ![point de terminaison de diffusion en continu](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints1.png)

> [!NOTE]
> <span data-ttu-id="ef65f-112">Vous êtes facturé uniquement lorsque votre point de terminaison de streaming est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="ef65f-112">You are only billed when your Streaming Endpoint is in running state.</span></span>

## <a name="adddelete-a-streaming-endpoint"></a><span data-ttu-id="ef65f-113">Ajouter/supprimer un point de terminaison de streaming</span><span class="sxs-lookup"><span data-stu-id="ef65f-113">Add/delete a streaming endpoint</span></span>

>[!NOTE]
><span data-ttu-id="ef65f-114">point de terminaison de diffusion en continu de la valeur par défaut Hello ne peut pas être supprimé.</span><span class="sxs-lookup"><span data-stu-id="ef65f-114">hello default streaming endpoint cannot be deleted.</span></span>

<span data-ttu-id="ef65f-115">à l’aide du point de terminaison de diffusion en continu tooadd/delete hello portail Azure, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="ef65f-115">tooadd/delete streaming endpoint using hello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="ef65f-116">tooadd un point de terminaison de diffusion en continu, cliquez sur hello **+ point de terminaison** en hello haut hello.</span><span class="sxs-lookup"><span data-stu-id="ef65f-116">tooadd a streaming endpoint, click hello **+ Endpoint** at hello top of hello page.</span></span> 

    <span data-ttu-id="ef65f-117">Vous pourriez plusieurs points de terminaison de diffusion en continu si vous envisagez de toohave CDN différents ou un CDN et un accès direct.</span><span class="sxs-lookup"><span data-stu-id="ef65f-117">You might want multiple Streaming Endpoints if you plan toohave different CDNs or a CDN and direct access.</span></span>

2. <span data-ttu-id="ef65f-118">toodelete un point de terminaison de diffusion en continu, appuyez sur **supprimer** bouton.</span><span class="sxs-lookup"><span data-stu-id="ef65f-118">toodelete a streaming endpoint, press **Delete** button.</span></span>      
3. <span data-ttu-id="ef65f-119">Cliquez sur hello **Démarrer** hello toostart de bouton point de terminaison de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="ef65f-119">Click hello **Start** button toostart hello streaming endpoint.</span></span>
   
    ![point de terminaison de diffusion en continu](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints2.png)


## <span data-ttu-id="ef65f-121"><a id="configure_streaming_endpoints"></a>Configuration de point de terminaison de diffusion en continu de hello</span><span class="sxs-lookup"><span data-stu-id="ef65f-121"><a id="configure_streaming_endpoints"></a>Configuring hello Streaming Endpoint</span></span>
<span data-ttu-id="ef65f-122">Point de terminaison de diffusion en continu vous permet de hello tooconfigure propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="ef65f-122">Streaming Endpoint enables you tooconfigure hello following properties:</span></span>

* <span data-ttu-id="ef65f-123">Contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="ef65f-123">Access control</span></span>
* <span data-ttu-id="ef65f-124">Contrôle de cache</span><span class="sxs-lookup"><span data-stu-id="ef65f-124">Cache control</span></span>
* <span data-ttu-id="ef65f-125">Stratégies d’accès intersite</span><span class="sxs-lookup"><span data-stu-id="ef65f-125">Cross site access policies</span></span>

<span data-ttu-id="ef65f-126">Pour plus d’informations sur ces propriétés, consultez la rubrique [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span><span class="sxs-lookup"><span data-stu-id="ef65f-126">For detailed information about these properties, see [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span></span>

<span data-ttu-id="ef65f-127">Vous pouvez configurer le point de terminaison de diffusion en continu de manière hello suivante :</span><span class="sxs-lookup"><span data-stu-id="ef65f-127">You can configure streaming endpoint by doing hello following:</span></span>

1. <span data-ttu-id="ef65f-128">Sélectionnez hello point de terminaison de tooconfigure de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="ef65f-128">Select hello streaming endpoint you want tooconfigure.</span></span>
2. <span data-ttu-id="ef65f-129">Cliquez sur **Settings**.</span><span class="sxs-lookup"><span data-stu-id="ef65f-129">Click **Settings**.</span></span>

<span data-ttu-id="ef65f-130">Une brève description des champs de hello suit.</span><span class="sxs-lookup"><span data-stu-id="ef65f-130">A brief description of hello fields follows.</span></span>

![point de terminaison de diffusion en continu](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints4.png)

1. <span data-ttu-id="ef65f-132">Stratégie de cache maximale : tooconfigure utilisés de vie du cache pour les ressources servies par ce point de terminaison de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="ef65f-132">Maximum cache policy: used tooconfigure cache lifetime for assets served through this streaming endpoint.</span></span> <span data-ttu-id="ef65f-133">Si aucune valeur n’est définie, la valeur par défaut hello est utilisé.</span><span class="sxs-lookup"><span data-stu-id="ef65f-133">If no value is set, hello default is used.</span></span> <span data-ttu-id="ef65f-134">valeurs par défaut de Hello peuvent également être définies directement dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="ef65f-134">hello default values can also be defined directly in Azure storage.</span></span> <span data-ttu-id="ef65f-135">Si Azure CDN est activé pour le point de terminaison de diffusion en continu de hello, vous ne devez pas définir accessible sans hello cache stratégie valeur de 600 secondes.</span><span class="sxs-lookup"><span data-stu-id="ef65f-135">If Azure CDN is enabled for hello streaming endpoint, you should not set hello cache policy value tooless than 600 seconds.</span></span>  
2. <span data-ttu-id="ef65f-136">Adresses IP autorisées : les adresses IP toospecify qui sont autorisées tooconnect toohello publié le point de terminaison de diffusion en continu utilisées.</span><span class="sxs-lookup"><span data-stu-id="ef65f-136">Allowed IP addresses: used toospecify IP addresses that would be allowed tooconnect toohello published streaming endpoint.</span></span> <span data-ttu-id="ef65f-137">Si aucune adresse IP n’est spécifié, n’importe quelle adresse IP est tooconnect en mesure de.</span><span class="sxs-lookup"><span data-stu-id="ef65f-137">If no IP addresses specified, any IP address would be able tooconnect.</span></span> <span data-ttu-id="ef65f-138">Les adresses IP peuvent être définies sous forme d’adresse IP unique (par exemple, « 10.0.0.1 »), de plage d’adresses IP constituée d’une adresse IP et d’un masque de sous-réseau CIDR (par exemple, « 10.0.0.1/22 ») ou de plage d’adresses IP constituée d’une adresse IP et d’un masque de sous-réseau au format décimal séparé par des points (par exemple, « 10.0.0.1(255.255.255.0) »).</span><span class="sxs-lookup"><span data-stu-id="ef65f-138">IP addresses can be specified as either a single IP address (for example, '10.0.0.1'), an IP range using an IP address and a CIDR subnet mask (for example, '10.0.0.1/22'), or an IP range using IP address and a dotted decimal subnet mask (for example, '10.0.0.1(255.255.255.0)').</span></span>
3. <span data-ttu-id="ef65f-139">Configuration pour l’authentification d’en-tête de signature Akamai : utilisé toospecify configuration de la demande d’authentification de signature en-tête à partir de serveurs Akamai.</span><span class="sxs-lookup"><span data-stu-id="ef65f-139">Configuration for Akamai signature header authentication: used toospecify how signature header authentication request from Akamai servers is configured.</span></span> <span data-ttu-id="ef65f-140">L’expiration est au format UTC.</span><span class="sxs-lookup"><span data-stu-id="ef65f-140">Expiration is in UTC.</span></span>

## <a name="scale-your-premium-streaming-endpoint"></a><span data-ttu-id="ef65f-141">Mise à l’échelle du point de terminaison de streaming Premium</span><span class="sxs-lookup"><span data-stu-id="ef65f-141">Scale your Premium streaming endpoint</span></span>

<span data-ttu-id="ef65f-142">Pour plus d’informations, consultez [cette rubrique](media-services-portal-scale-streaming-endpoints.md) .</span><span class="sxs-lookup"><span data-stu-id="ef65f-142">For more information, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <span data-ttu-id="ef65f-143"><a id="enable_cdn"></a>Activer l’intégration au CDN Azure</span><span class="sxs-lookup"><span data-stu-id="ef65f-143"><a id="enable_cdn"></a>Enable Azure CDN integration</span></span>

<span data-ttu-id="ef65f-144">Lorsque vous créez un compte, l’intégration CDN Azure du point de terminaison de streaming par défaut est activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="ef65f-144">When you create a new account, default Streaming Endpoint Azure CDN integration is enabled by default.</span></span>

<span data-ttu-id="ef65f-145">Si vous souhaitez ultérieurement toodisable/activer hello CDN, votre point de terminaison de diffusion en continu doit être Bonjour **arrêté** état.</span><span class="sxs-lookup"><span data-stu-id="ef65f-145">If you later want toodisable/enable hello CDN, your streaming endpoint must be in hello **stopped** state.</span></span> <span data-ttu-id="ef65f-146">Peut prendre les heures too2 pour tooget de l’intégration d’Azure CDN hello activé et hello toobe de modifications actif sur tous les hello POP du CDN.</span><span class="sxs-lookup"><span data-stu-id="ef65f-146">It could take up too2 hours for hello Azure CDN integration tooget enabled and for hello changes toobe active across all hello CDN POPs.</span></span> <span data-ttu-id="ef65f-147">Toutefois, vous pouvez démarrer votre point de terminaison et les flux sans interruptions de diffusion en continu à partir du point de terminaison de diffusion en continu de hello et une fois qu’integration de hello est terminée, les flux hello seront remis à partir de hello CDN.</span><span class="sxs-lookup"><span data-stu-id="ef65f-147">However, your can start your streaming endpoint and stream without interruptions from hello streaming endpoint and once hello integration is complete, hello stream will be delivered from hello CDN.</span></span> <span data-ttu-id="ef65f-148">Au cours de hello période de mise en service votre point de terminaison de diffusion en continu sera dans **démarrage** état et que vous pouvez observer les performances de degredad.</span><span class="sxs-lookup"><span data-stu-id="ef65f-148">During hello provisioning period your streaming endpoint will be in **starting** state and you might observe degredad performance.</span></span>

<span data-ttu-id="ef65f-149">Intégration de CDN est activée dans tous les execpt de centres de données Azure hello en Chine et régions du gouvernement fédéral.</span><span class="sxs-lookup"><span data-stu-id="ef65f-149">CDN integration is enabled in all hello Azure data centers execpt China and Federal Goverment regions.</span></span>

<span data-ttu-id="ef65f-150">Une fois qu’elle est activée, hello **le contrôle d’accès**, **nom d’hôte personnalisé** et **l’authentification de Akamai Signature** configuration obtient désactivée.</span><span class="sxs-lookup"><span data-stu-id="ef65f-150">Once it is enabled, hello **Access Control**, **Custom hostname** and **Akamai Signature authentication** configuration gets disabled.</span></span>
 
> [!IMPORTANT]
> <span data-ttu-id="ef65f-151">L’intégration d’Azure Media Services au CDN Azure est implémentée sur le **CDN Azure fourni par Verizon** pour les points de terminaison de streaming Standard.</span><span class="sxs-lookup"><span data-stu-id="ef65f-151">Azure Media Services integration with Azure CDN is implemented on **Azure CDN from Verizon** for standard streaming endpoints.</span></span> <span data-ttu-id="ef65f-152">Les points de terminaison de streaming Premium peuvent être configurés à l’aide de l’ensemble des **fournisseurs et niveaux de tarification Azure CDN**.</span><span class="sxs-lookup"><span data-stu-id="ef65f-152">Premium streaming endpoints can be configured using all **Azure CDN pricing tiers and providers**.</span></span> <span data-ttu-id="ef65f-153">Pour plus d’informations sur les fonctionnalités d’Azure CDN, consultez hello [vue d’ensemble CDN](../cdn/cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ef65f-153">For more information about Azure CDN features, see hello [CDN overview](../cdn/cdn-overview.md).</span></span>
 
### <a name="additional-considerations"></a><span data-ttu-id="ef65f-154">Considérations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="ef65f-154">Additional considerations</span></span>

* <span data-ttu-id="ef65f-155">Si le CDN est activé pour un point de terminaison de diffusion en continu, les clients ne peuvent pas demandent du contenu directement à partir de l’origine de hello.</span><span class="sxs-lookup"><span data-stu-id="ef65f-155">When CDN is enabled for a streaming endpoint, clients cannot request content directly from hello origin.</span></span> <span data-ttu-id="ef65f-156">Si vous devez hello capacité tootest votre contenu avec ou sans CDN, vous pouvez créer un autre point de terminaison diffusion en continu qui n’est pas de CDN activé.</span><span class="sxs-lookup"><span data-stu-id="ef65f-156">If you need hello ability tootest your content with or without CDN, you can create another streaming endpoint that isn't CDN enabled.</span></span>
* <span data-ttu-id="ef65f-157">Votre diffusion en continu reste de nom d’hôte de point de terminaison hello même après l’activation du CDN.</span><span class="sxs-lookup"><span data-stu-id="ef65f-157">Your streaming endpoint hostname remains hello same after enabling CDN.</span></span> <span data-ttu-id="ef65f-158">Vous n’avez pas besoin toomake n’importe quel flux de travail de modifications tooyour media services une fois que le CDN est activé.</span><span class="sxs-lookup"><span data-stu-id="ef65f-158">You don’t need toomake any changes tooyour media services workflow after CDN is enabled.</span></span> <span data-ttu-id="ef65f-159">Par exemple, si votre nom d’hôte du point de terminaison diffusion en continu est strasbourg.streaming.mediaservices.windows.net, après avoir activé le CDN, hello exacte même nom d’hôte est utilisé.</span><span class="sxs-lookup"><span data-stu-id="ef65f-159">For example, if your streaming endpoint hostname is strasbourg.streaming.mediaservices.windows.net, after enabling CDN, hello exact same hostname is used.</span></span>
* <span data-ttu-id="ef65f-160">Pour les nouveaux points de terminaison de diffusion en continu, vous pouvez activer CDN simplement par la création d’un point de terminaison ; pour les points de terminaison de diffusion en continu existants, vous avez besoin de point de terminaison hello toofirst arrêter, puis sur Activer/désactiver hello CDN.</span><span class="sxs-lookup"><span data-stu-id="ef65f-160">For new streaming endpoints, you can enable CDN simply by creating a new endpoint; for existing streaming endpoints, you need toofirst stop hello endpoint and then enable/disable hello CDN.</span></span>
* <span data-ttu-id="ef65f-161">Le point de terminaison de streaming Standard ne peut être configuré qu’à l’aide du **fournisseur CDN Standard Verizon** par le biais du portail de gestion Azure.</span><span class="sxs-lookup"><span data-stu-id="ef65f-161">Standard streaming endpoint can only be configured using **Verizon Standard CDN provider** using Azure management portal.</span></span> <span data-ttu-id="ef65f-162">Toutefois, vous pouvez activer d’autres fournisseurs Azure CDN à l’aide d’API REST.</span><span class="sxs-lookup"><span data-stu-id="ef65f-162">However, you can enable other Azure CDN providers using REST APIs.</span></span>

## <a name="configure-cdn-profile"></a><span data-ttu-id="ef65f-163">Configurer le profil CDN</span><span class="sxs-lookup"><span data-stu-id="ef65f-163">Configure CDN profile</span></span>

<span data-ttu-id="ef65f-164">Vous pouvez configurer le profil CDN hello en sélectionnant hello **gérer le CDN** bouton à partir du haut de hello.</span><span class="sxs-lookup"><span data-stu-id="ef65f-164">You can configure hello CDN profile by selecting hello **Manage CDN** button from hello top.</span></span>

![point de terminaison de diffusion en continu](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints6.png)

## <a name="next-steps"></a><span data-ttu-id="ef65f-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ef65f-166">Next steps</span></span>
<span data-ttu-id="ef65f-167">Consultez les parcours d’apprentissage de Media Services.</span><span class="sxs-lookup"><span data-stu-id="ef65f-167">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ef65f-168">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="ef65f-168">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

