---
title: "Gérer les points de terminaison de streaming avec le Portail Azure | Microsoft Docs"
description: "Cette rubrique montre comment gérer les points de terminaison de streaming avec le Portail Azure."
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
ms.openlocfilehash: 797dced6c3e2525730afa29987259cb9b435ba66
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-streaming-endpoints-with-the-azure-portal"></a><span data-ttu-id="b3c9a-103">Gérer les points de terminaison de streaming avec le Portail Azure</span><span class="sxs-lookup"><span data-stu-id="b3c9a-103">Manage streaming endpoints with the Azure portal</span></span>

<span data-ttu-id="b3c9a-104">Cette rubrique explique comment utiliser le portail Azure pour gérer les points de terminaison de streaming.</span><span class="sxs-lookup"><span data-stu-id="b3c9a-104">This topic shows  how to use the Azure portal to manage streaming endpoints.</span></span> 

>[!NOTE]
><span data-ttu-id="b3c9a-105">Consultez la rubrique de [présentation](media-services-streaming-endpoints-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b3c9a-105">Make sure to review the [overview](media-services-streaming-endpoints-overview.md) topic.</span></span> 

<span data-ttu-id="b3c9a-106">Pour plus d’informations sur la mise à l’échelle du point de terminaison de streaming, consultez [cette](media-services-portal-scale-streaming-endpoints.md) rubrique.</span><span class="sxs-lookup"><span data-stu-id="b3c9a-106">For information about how to scale the streaming endpoint, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <a name="start-managing-streaming-endpoints"></a><span data-ttu-id="b3c9a-107">Commencer à gérer des points de terminaison de streaming</span><span class="sxs-lookup"><span data-stu-id="b3c9a-107">Start managing streaming endpoints</span></span> 

<span data-ttu-id="b3c9a-108">Pour commencer à gérer les points de terminaison de streaming de votre compte, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="b3c9a-108">To start managing streaming endpoints for your account, do the following.</span></span>

1. <span data-ttu-id="b3c9a-109">Dans le [portail Azure](https://portal.azure.com/), sélectionnez votre compte Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="b3c9a-109">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="b3c9a-110">Dans le panneau **Paramètres**, sélectionnez **Points de terminaison de streaming**.</span><span class="sxs-lookup"><span data-stu-id="b3c9a-110">In the **Settings** blade, select **Streaming endpoints**.</span></span>
   
    ![point de terminaison de diffusion en continu](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints1.png)

> [!NOTE]
> <span data-ttu-id="b3c9a-112">Vous êtes facturé uniquement lorsque votre point de terminaison de streaming est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="b3c9a-112">You are only billed when your Streaming Endpoint is in running state.</span></span>

## <a name="adddelete-a-streaming-endpoint"></a><span data-ttu-id="b3c9a-113">Ajouter/supprimer un point de terminaison de streaming</span><span class="sxs-lookup"><span data-stu-id="b3c9a-113">Add/delete a streaming endpoint</span></span>

>[!NOTE]
><span data-ttu-id="b3c9a-114">Il n’est pas possible de supprimer le point de terminaison de streaming par défaut.</span><span class="sxs-lookup"><span data-stu-id="b3c9a-114">The default streaming endpoint cannot be deleted.</span></span>

<span data-ttu-id="b3c9a-115">Pour ajouter/supprimer un point de terminaison de streaming à l’aide du Portail Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="b3c9a-115">To add/delete streaming endpoint using the Azure portal, do the following:</span></span>

1. <span data-ttu-id="b3c9a-116">Pour ajouter un point de terminaison de streaming, cliquez sur le **+ Point de terminaison** en haut de la page.</span><span class="sxs-lookup"><span data-stu-id="b3c9a-116">To add a streaming endpoint, click the **+ Endpoint** at the top of the page.</span></span> 

    <span data-ttu-id="b3c9a-117">Vous pouvez également disposer de plusieurs points de terminaison de streaming si vous prévoyez d’avoir différents CDN ou bien un CDN et un accès direct.</span><span class="sxs-lookup"><span data-stu-id="b3c9a-117">You might want multiple Streaming Endpoints if you plan to have different CDNs or a CDN and direct access.</span></span>

2. <span data-ttu-id="b3c9a-118">Pour supprimer un point de terminaison de streaming, appuyez sur le bouton **Supprimer** .</span><span class="sxs-lookup"><span data-stu-id="b3c9a-118">To delete a streaming endpoint, press **Delete** button.</span></span>      
3. <span data-ttu-id="b3c9a-119">Cliquez sur le bouton **Démarrer** pour démarrer le point de terminaison de streaming.</span><span class="sxs-lookup"><span data-stu-id="b3c9a-119">Click the **Start** button to start the streaming endpoint.</span></span>
   
    ![point de terminaison de diffusion en continu](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints2.png)


## <span data-ttu-id="b3c9a-121"><a id="configure_streaming_endpoints"></a>Configuration du point de terminaison de diffusion en continu</span><span class="sxs-lookup"><span data-stu-id="b3c9a-121"><a id="configure_streaming_endpoints"></a>Configuring the Streaming Endpoint</span></span>
<span data-ttu-id="b3c9a-122">Le point de terminaison de streaming vous permet de configurer les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="b3c9a-122">Streaming Endpoint enables you to configure the following properties:</span></span>

* <span data-ttu-id="b3c9a-123">Contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="b3c9a-123">Access control</span></span>
* <span data-ttu-id="b3c9a-124">Contrôle de cache</span><span class="sxs-lookup"><span data-stu-id="b3c9a-124">Cache control</span></span>
* <span data-ttu-id="b3c9a-125">Stratégies d’accès intersite</span><span class="sxs-lookup"><span data-stu-id="b3c9a-125">Cross site access policies</span></span>

<span data-ttu-id="b3c9a-126">Pour plus d’informations sur ces propriétés, consultez la rubrique [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span><span class="sxs-lookup"><span data-stu-id="b3c9a-126">For detailed information about these properties, see [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span></span>

<span data-ttu-id="b3c9a-127">Vous pouvez configurer le point de terminaison de streaming en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="b3c9a-127">You can configure streaming endpoint by doing the following:</span></span>

1. <span data-ttu-id="b3c9a-128">Sélectionnez le point de terminaison de streaming que vous souhaitez configurer.</span><span class="sxs-lookup"><span data-stu-id="b3c9a-128">Select the streaming endpoint you want to configure.</span></span>
2. <span data-ttu-id="b3c9a-129">Cliquez sur **Settings**.</span><span class="sxs-lookup"><span data-stu-id="b3c9a-129">Click **Settings**.</span></span>

<span data-ttu-id="b3c9a-130">Vous trouverez une brève description des champs ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="b3c9a-130">A brief description of the fields follows.</span></span>

![point de terminaison de diffusion en continu](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints4.png)

1. <span data-ttu-id="b3c9a-132">Stratégie de cache maximale : permet de configurer la durée de vie du cache pour les ressources traitées par le biais de ce point de terminaison de streaming.</span><span class="sxs-lookup"><span data-stu-id="b3c9a-132">Maximum cache policy: used to configure cache lifetime for assets served through this streaming endpoint.</span></span> <span data-ttu-id="b3c9a-133">Si aucune valeur n’est définie, la valeur par défaut est utilisée.</span><span class="sxs-lookup"><span data-stu-id="b3c9a-133">If no value is set, the default is used.</span></span> <span data-ttu-id="b3c9a-134">Les valeurs par défaut peuvent également être définies directement dans Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="b3c9a-134">The default values can also be defined directly in Azure storage.</span></span> <span data-ttu-id="b3c9a-135">Si Azure CDN est activé pour le point de terminaison de streaming, ne définissez pas une valeur de stratégie de cache inférieure à 600 secondes.</span><span class="sxs-lookup"><span data-stu-id="b3c9a-135">If Azure CDN is enabled for the streaming endpoint, you should not set the cache policy value to less than 600 seconds.</span></span>  
2. <span data-ttu-id="b3c9a-136">Adresses IP autorisées : permet de définir les adresses IP autorisées à se connecter au point de terminaison de streaming publié.</span><span class="sxs-lookup"><span data-stu-id="b3c9a-136">Allowed IP addresses: used to specify IP addresses that would be allowed to connect to the published streaming endpoint.</span></span> <span data-ttu-id="b3c9a-137">Si aucune adresse IP n'est spécifiée, toutes les adresses IP peuvent se connecter.</span><span class="sxs-lookup"><span data-stu-id="b3c9a-137">If no IP addresses specified, any IP address would be able to connect.</span></span> <span data-ttu-id="b3c9a-138">Les adresses IP peuvent être définies sous forme d’adresse IP unique (par exemple, « 10.0.0.1 »), de plage d’adresses IP constituée d’une adresse IP et d’un masque de sous-réseau CIDR (par exemple, « 10.0.0.1/22 ») ou de plage d’adresses IP constituée d’une adresse IP et d’un masque de sous-réseau au format décimal séparé par des points (par exemple, « 10.0.0.1(255.255.255.0) »).</span><span class="sxs-lookup"><span data-stu-id="b3c9a-138">IP addresses can be specified as either a single IP address (for example, '10.0.0.1'), an IP range using an IP address and a CIDR subnet mask (for example, '10.0.0.1/22'), or an IP range using IP address and a dotted decimal subnet mask (for example, '10.0.0.1(255.255.255.0)').</span></span>
3. <span data-ttu-id="b3c9a-139">Configuration de l’authentification de l’en-tête de signature Akamai : permet de spécifier la configuration de la demande d’authentification de l’en-tête de signature à partir de serveurs Akamai.</span><span class="sxs-lookup"><span data-stu-id="b3c9a-139">Configuration for Akamai signature header authentication: used to specify how signature header authentication request from Akamai servers is configured.</span></span> <span data-ttu-id="b3c9a-140">L’expiration est au format UTC.</span><span class="sxs-lookup"><span data-stu-id="b3c9a-140">Expiration is in UTC.</span></span>

## <a name="scale-your-premium-streaming-endpoint"></a><span data-ttu-id="b3c9a-141">Mise à l’échelle du point de terminaison de streaming Premium</span><span class="sxs-lookup"><span data-stu-id="b3c9a-141">Scale your Premium streaming endpoint</span></span>

<span data-ttu-id="b3c9a-142">Pour plus d’informations, consultez [cette rubrique](media-services-portal-scale-streaming-endpoints.md) .</span><span class="sxs-lookup"><span data-stu-id="b3c9a-142">For more information, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <span data-ttu-id="b3c9a-143"><a id="enable_cdn"></a>Activer l’intégration au CDN Azure</span><span class="sxs-lookup"><span data-stu-id="b3c9a-143"><a id="enable_cdn"></a>Enable Azure CDN integration</span></span>

<span data-ttu-id="b3c9a-144">Lorsque vous créez un compte, l’intégration CDN Azure du point de terminaison de streaming par défaut est activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="b3c9a-144">When you create a new account, default Streaming Endpoint Azure CDN integration is enabled by default.</span></span>

<span data-ttu-id="b3c9a-145">Si vous souhaitez activer/désactiver le CDN ultérieurement, votre point de terminaison de streaming doit avoir l’état **Arrêté**.</span><span class="sxs-lookup"><span data-stu-id="b3c9a-145">If you later want to disable/enable the CDN, your streaming endpoint must be in the **stopped** state.</span></span> <span data-ttu-id="b3c9a-146">Il peut s’écouler jusqu’à deux heures pour que l’intégration d’Azure CDN soit active et pour que les modifications soient actives sur tous les comptes POP CDN.</span><span class="sxs-lookup"><span data-stu-id="b3c9a-146">It could take up to 2 hours for the Azure CDN integration to get enabled and for the changes to be active across all the CDN POPs.</span></span> <span data-ttu-id="b3c9a-147">Toutefois, vous pouvez démarrer votre point de terminaison de streaming et le flux sans interruptions à partir du point de terminaison de streaming. Une fois l’intégration terminée, le flux est émis à partir du CDN.</span><span class="sxs-lookup"><span data-stu-id="b3c9a-147">However, your can start your streaming endpoint and stream without interruptions from the streaming endpoint and once the integration is complete, the stream will be delivered from the CDN.</span></span> <span data-ttu-id="b3c9a-148">Pendant la durée de l’approvisionnement, votre point de terminaison de streaming est en état de **démarrage** et vous pouvez observer une dégradation des performances.</span><span class="sxs-lookup"><span data-stu-id="b3c9a-148">During the provisioning period your streaming endpoint will be in **starting** state and you might observe degredad performance.</span></span>

<span data-ttu-id="b3c9a-149">L’intégration du CDN est activée dans tous les centres de données Azure, sauf dans les régions Gouvernement fédéral et Chine.</span><span class="sxs-lookup"><span data-stu-id="b3c9a-149">CDN integration is enabled in all the Azure data centers execpt China and Federal Goverment regions.</span></span>

<span data-ttu-id="b3c9a-150">Une fois qu’elle est activée, la configuration d’**Access Control**, du **nom d’hôte personnalisé** et de l’**authentification de signature Akamai** est désactivée.</span><span class="sxs-lookup"><span data-stu-id="b3c9a-150">Once it is enabled, the **Access Control**, **Custom hostname** and **Akamai Signature authentication** configuration gets disabled.</span></span>
 
> [!IMPORTANT]
> <span data-ttu-id="b3c9a-151">L’intégration d’Azure Media Services au CDN Azure est implémentée sur le **CDN Azure fourni par Verizon** pour les points de terminaison de streaming Standard.</span><span class="sxs-lookup"><span data-stu-id="b3c9a-151">Azure Media Services integration with Azure CDN is implemented on **Azure CDN from Verizon** for standard streaming endpoints.</span></span> <span data-ttu-id="b3c9a-152">Les points de terminaison de streaming Premium peuvent être configurés à l’aide de l’ensemble des **fournisseurs et niveaux de tarification Azure CDN**.</span><span class="sxs-lookup"><span data-stu-id="b3c9a-152">Premium streaming endpoints can be configured using all **Azure CDN pricing tiers and providers**.</span></span> <span data-ttu-id="b3c9a-153">Pour plus d’informations sur les fonctionnalités du CDN Azure, consultez [Vue d’ensemble du réseau de distribution de contenu (CDN)](../cdn/cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b3c9a-153">For more information about Azure CDN features, see the [CDN overview](../cdn/cdn-overview.md).</span></span>
 
### <a name="additional-considerations"></a><span data-ttu-id="b3c9a-154">Considérations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="b3c9a-154">Additional considerations</span></span>

* <span data-ttu-id="b3c9a-155">Lorsque le CDN est activé pour un point de terminaison de diffusion en continu, les clients ne peuvent pas demander directement le contenu à partir de l’origine.</span><span class="sxs-lookup"><span data-stu-id="b3c9a-155">When CDN is enabled for a streaming endpoint, clients cannot request content directly from the origin.</span></span> <span data-ttu-id="b3c9a-156">Si vous avez besoin de tester votre contenu avec ou sans CDN, vous pouvez créer un autre point de terminaison de streaming qui n’est pas activé pour le CDN.</span><span class="sxs-lookup"><span data-stu-id="b3c9a-156">If you need the ability to test your content with or without CDN, you can create another streaming endpoint that isn't CDN enabled.</span></span>
* <span data-ttu-id="b3c9a-157">Le nom d’hôte de votre point de terminaison reste le même une fois le CDN activé.</span><span class="sxs-lookup"><span data-stu-id="b3c9a-157">Your streaming endpoint hostname remains the same after enabling CDN.</span></span> <span data-ttu-id="b3c9a-158">Vous n’avez pas besoin d’apporter de modifications à votre flux de travail Media Services une fois le CDN activé.</span><span class="sxs-lookup"><span data-stu-id="b3c9a-158">You don’t need to make any changes to your media services workflow after CDN is enabled.</span></span> <span data-ttu-id="b3c9a-159">Par exemple, si le nom d’hôte de votre point de terminaison en continu est strasbourg.streaming.mediaservices.windows.net, après avoir activé le CDN, le même nom d’hôte est utilisé.</span><span class="sxs-lookup"><span data-stu-id="b3c9a-159">For example, if your streaming endpoint hostname is strasbourg.streaming.mediaservices.windows.net, after enabling CDN, the exact same hostname is used.</span></span>
* <span data-ttu-id="b3c9a-160">Pour les nouveaux points de terminaison de streaming, vous pouvez simplement activer le CDN en créant un point de terminaison. Pour les points de terminaison de streaming existants, vous devez d’abord arrêter le point de terminaison, puis activer/désactiver le CDN.</span><span class="sxs-lookup"><span data-stu-id="b3c9a-160">For new streaming endpoints, you can enable CDN simply by creating a new endpoint; for existing streaming endpoints, you need to first stop the endpoint and then enable/disable the CDN.</span></span>
* <span data-ttu-id="b3c9a-161">Le point de terminaison de streaming Standard ne peut être configuré qu’à l’aide du **fournisseur CDN Standard Verizon** par le biais du portail de gestion Azure.</span><span class="sxs-lookup"><span data-stu-id="b3c9a-161">Standard streaming endpoint can only be configured using **Verizon Standard CDN provider** using Azure management portal.</span></span> <span data-ttu-id="b3c9a-162">Toutefois, vous pouvez activer d’autres fournisseurs Azure CDN à l’aide d’API REST.</span><span class="sxs-lookup"><span data-stu-id="b3c9a-162">However, you can enable other Azure CDN providers using REST APIs.</span></span>

## <a name="configure-cdn-profile"></a><span data-ttu-id="b3c9a-163">Configurer le profil CDN</span><span class="sxs-lookup"><span data-stu-id="b3c9a-163">Configure CDN profile</span></span>

<span data-ttu-id="b3c9a-164">Vous pouvez configurer le profil CDN en sélectionnant le bouton **Gérer le CDN** en haut.</span><span class="sxs-lookup"><span data-stu-id="b3c9a-164">You can configure the CDN profile by selecting the **Manage CDN** button from the top.</span></span>

![point de terminaison de diffusion en continu](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints6.png)

## <a name="next-steps"></a><span data-ttu-id="b3c9a-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b3c9a-166">Next steps</span></span>
<span data-ttu-id="b3c9a-167">Consultez les parcours d’apprentissage de Media Services.</span><span class="sxs-lookup"><span data-stu-id="b3c9a-167">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b3c9a-168">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="b3c9a-168">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

