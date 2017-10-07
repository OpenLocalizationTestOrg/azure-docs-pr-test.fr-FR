---
title: "aaaGetting main d’Azure CDN | Documents Microsoft"
description: "Cette rubrique montre comment tooenable hello Azure réseau CDN (Content Delivery). didacticiel de Hello Guide de création de hello d’un nouveau profil CDN et du point de terminaison."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 4ca51224-5423-419b-98cf-89860ef516d2
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 0ce9802bfd7b60e70a9a62330f5593fc17ea07d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-cdn"></a><span data-ttu-id="a491c-104">Prise en main d’Azure CDN</span><span class="sxs-lookup"><span data-stu-id="a491c-104">Getting started with Azure CDN</span></span>
<span data-ttu-id="a491c-105">Cette rubrique décrit l’activation d’Azure CDN en créant un nouveau profil CDN et un point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="a491c-105">This topic walks through enabling Azure CDN by creating a new CDN profile and endpoint.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a491c-106">Pour un fonctionnement du CDN toohow introduction, ainsi que d’une liste des fonctionnalités, consultez hello [vue d’ensemble du CDN](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a491c-106">For an introduction toohow CDN works, as well as a list of features, see hello [CDN Overview](cdn-overview.md).</span></span>
> 
> 

## <a name="create-a-new-cdn-profile"></a><span data-ttu-id="a491c-107">Créer un profil CDN</span><span class="sxs-lookup"><span data-stu-id="a491c-107">Create a new CDN profile</span></span>
<span data-ttu-id="a491c-108">Un profil CDN est une collection de points de terminaison CDN.</span><span class="sxs-lookup"><span data-stu-id="a491c-108">A CDN profile is a collection of CDN endpoints.</span></span>  <span data-ttu-id="a491c-109">Chaque profil contient un ou plusieurs points de terminaison CDN.</span><span class="sxs-lookup"><span data-stu-id="a491c-109">Each profile contains one or more CDN endpoints.</span></span>  <span data-ttu-id="a491c-110">Vous souhaiterez peut-être toouse plusieurs profils tooorganize vos points de terminaison CDN par domaine internet, application web ou d’autres critères.</span><span class="sxs-lookup"><span data-stu-id="a491c-110">You may wish toouse multiple profiles tooorganize your CDN endpoints by internet domain, web application, or some other criteria.</span></span>

> [!NOTE]
> <span data-ttu-id="a491c-111">Par défaut, un seul abonnement Azure est profils CDN tooeight limité.</span><span class="sxs-lookup"><span data-stu-id="a491c-111">By default, a single Azure subscription is limited tooeight CDN profiles.</span></span> <span data-ttu-id="a491c-112">Chaque profil CDN est limitée tooten points de terminaison CDN.</span><span class="sxs-lookup"><span data-stu-id="a491c-112">Each CDN profile is limited tooten CDN endpoints.</span></span>
> 
> <span data-ttu-id="a491c-113">Tarification du CDN est appliquée au niveau de profil CDN hello.</span><span class="sxs-lookup"><span data-stu-id="a491c-113">CDN pricing is applied at hello CDN profile level.</span></span> <span data-ttu-id="a491c-114">Si vous souhaitez toouse un mélange d’Azure CDN niveaux tarifaires, vous devez plusieurs profils CDN.</span><span class="sxs-lookup"><span data-stu-id="a491c-114">If you wish toouse a mix of Azure CDN pricing tiers, you will need multiple CDN profiles.</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a><span data-ttu-id="a491c-115">Créer un point de terminaison CDN</span><span class="sxs-lookup"><span data-stu-id="a491c-115">Create a new CDN endpoint</span></span>
<span data-ttu-id="a491c-116">**toocreate un nouveau point de terminaison CDN**</span><span class="sxs-lookup"><span data-stu-id="a491c-116">**toocreate a new CDN endpoint**</span></span>

1. <span data-ttu-id="a491c-117">Bonjour [Azure Portal](https://portal.azure.com), accédez tooyour le profil CDN.</span><span class="sxs-lookup"><span data-stu-id="a491c-117">In hello [Azure Portal](https://portal.azure.com), navigate tooyour CDN profile.</span></span>  <span data-ttu-id="a491c-118">Vous pouvez avoir épinglée toohello le tableau de bord à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="a491c-118">You may have pinned it toohello dashboard in hello previous step.</span></span>  <span data-ttu-id="a491c-119">Si vous ne vous le trouverez en cliquant sur **Parcourir**, puis **profils CDN**, et en cliquant sur le profil de hello vous prévoyez de tooadd votre point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="a491c-119">If you not, you can find it by clicking **Browse**, then **CDN profiles**, and clicking on hello profile you plan tooadd your endpoint to.</span></span>
   
    <span data-ttu-id="a491c-120">Panneau de profil CDN Hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="a491c-120">hello CDN profile blade appears.</span></span>
   
    ![Profil CDN][cdn-profile-settings]
2. <span data-ttu-id="a491c-122">Cliquez sur hello **ajouter le point de terminaison** bouton.</span><span class="sxs-lookup"><span data-stu-id="a491c-122">Click hello **Add Endpoint** button.</span></span>
   
    ![Bouton Ajouter un point de terminaison][cdn-new-endpoint-button]
   
    <span data-ttu-id="a491c-124">Hello **ajouter un point de terminaison** panneau s’affiche.</span><span class="sxs-lookup"><span data-stu-id="a491c-124">hello **Add an endpoint** blade appears.</span></span>
   
    ![Panneau Ajouter un point de terminaison][cdn-add-endpoint]
3. <span data-ttu-id="a491c-126">Entrez un **nom** pour ce point de terminaison CDN.</span><span class="sxs-lookup"><span data-stu-id="a491c-126">Enter a **Name** for this CDN endpoint.</span></span>  <span data-ttu-id="a491c-127">Ce nom sera utilisé tooaccess vos ressources mises en cache au niveau du domaine de hello `<endpointname>.azureedge.net`.</span><span class="sxs-lookup"><span data-stu-id="a491c-127">This name will be used tooaccess your cached resources at hello domain `<endpointname>.azureedge.net`.</span></span>
4. <span data-ttu-id="a491c-128">Bonjour **type d’origine** liste déroulante, sélectionnez votre type d’origine.</span><span class="sxs-lookup"><span data-stu-id="a491c-128">In hello **Origin type** dropdown, select your origin type.</span></span>  <span data-ttu-id="a491c-129">Sélectionnez **Stockage** pour un compte de stockage Azure, **Service cloud** pour un service cloud Azure, **Application web** pour une application web Azure ou **Origine personnalisée** pour toute autre origine de serveur web accessible publiquement (hébergé dans Azure ou ailleurs).</span><span class="sxs-lookup"><span data-stu-id="a491c-129">Select **Storage** for an Azure Storage account, **Cloud service** for an Azure Cloud Service, **Web App** for an Azure Web App, or **Custom origin** for any other publicly accessible web server origin (hosted in Azure or elsewhere).</span></span>
   
    ![Type d'origine CDN](./media/cdn-create-new-endpoint/cdn-origin-type.png)
5. <span data-ttu-id="a491c-131">Bonjour **nom d’hôte d’origine** liste déroulante, sélectionnez ou tapez votre domaine d’origine.</span><span class="sxs-lookup"><span data-stu-id="a491c-131">In hello **Origin hostname** dropdown, select or type your origin domain.</span></span>  <span data-ttu-id="a491c-132">liste déroulante de Hello répertorie toutes les origines disponibles de type hello spécifié à l’étape 4.</span><span class="sxs-lookup"><span data-stu-id="a491c-132">hello dropdown will list all available origins of hello type you specified in step 4.</span></span>  <span data-ttu-id="a491c-133">Si vous avez sélectionné *origine du personnalisé* en tant que votre **type d’origine**, vous allez taper dans le domaine hello de votre origine personnalisée.</span><span class="sxs-lookup"><span data-stu-id="a491c-133">If you selected *Custom origin* as your **Origin type**, you will type in hello domain of your custom origin.</span></span>
6. <span data-ttu-id="a491c-134">Bonjour **chemin d’origine** texte, entrez hello chemin d’accès toohello ressources toocache, ou laissez vide tooallow cache n’importe quelle ressource au niveau domaine hello spécifié à l’étape 5.</span><span class="sxs-lookup"><span data-stu-id="a491c-134">In hello **Origin path** text box, enter hello path toohello resources you want toocache, or leave blank tooallow cache any resource at hello domain you specified in step 5.</span></span>
7. <span data-ttu-id="a491c-135">Bonjour **en-tête hôte d’origine**, entrez l’en-tête d’hôte hello souhaité hello toosend CDN avec chaque demande, ou laissez hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="a491c-135">In hello **Origin host header**, enter hello host header you want hello CDN toosend with each request, or leave hello default.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="a491c-136">Certains types d’origines, telles que le stockage Azure et les applications Web requièrent hello hôte en-tête toomatch hello domaine d’origine de hello.</span><span class="sxs-lookup"><span data-stu-id="a491c-136">Some types of origins, such as Azure Storage and Web Apps, require hello host header toomatch hello domain of hello origin.</span></span> <span data-ttu-id="a491c-137">À moins d’avoir une origine nécessitant un en-tête d’hôte différent de son domaine, vous devez laisser la valeur par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="a491c-137">Unless you have an origin that requires a host header different from its domain, you should leave hello default value.</span></span>
   > 
   > 
8. <span data-ttu-id="a491c-138">Pour **protocole** et **port d’origine**, spécifier hello protocoles et ports utilisés tooaccess vos ressources à l’origine de hello.</span><span class="sxs-lookup"><span data-stu-id="a491c-138">For **Protocol** and **Origin port**, specify hello protocols and ports used tooaccess your resources at hello origin.</span></span>  <span data-ttu-id="a491c-139">Vous devez sélectionner au moins un protocole (HTTP ou HTTPS).</span><span class="sxs-lookup"><span data-stu-id="a491c-139">At least one protocol (HTTP or HTTPS) must be selected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a491c-140">Hello **port d’origine** affecte uniquement le point de terminaison hello port utilise les informations de tooretrieve à partir de l’origine de hello.</span><span class="sxs-lookup"><span data-stu-id="a491c-140">hello **Origin port** only affects what port hello endpoint uses tooretrieve information from hello origin.</span></span>  <span data-ttu-id="a491c-141">Hello point de terminaison lui-même sera disponible tooend clients hello par défaut ports HTTP et HTTPS (80 et 443), quel que soit hello **port d’origine**.</span><span class="sxs-lookup"><span data-stu-id="a491c-141">hello endpoint itself will only be available tooend clients on hello default HTTP and HTTPS ports (80 and 443), regardless of hello **Origin port**.</span></span>  
   > 
   > <span data-ttu-id="a491c-142">**CDN Azure à partir d’Akamai** points de terminaison n’autorisent pas de plage de ports TCP complète hello pour les origines.</span><span class="sxs-lookup"><span data-stu-id="a491c-142">**Azure CDN from Akamai** endpoints do not allow hello full TCP port range for origins.</span></span>  <span data-ttu-id="a491c-143">Pour obtenir la liste des ports d’origine non autorisés, consultez l’article [Azure CDN from Akamai Allowed Origin Ports](https://msdn.microsoft.com/library/mt757337.aspx)(Ports d’origine autorisés du CDN Azure fourni par Akamai).</span><span class="sxs-lookup"><span data-stu-id="a491c-143">For a list of origin ports that are not allowed, see [Azure CDN from Akamai Allowed Origin Ports](https://msdn.microsoft.com/library/mt757337.aspx).</span></span>  
   > 
   > <span data-ttu-id="a491c-144">L’accès à CDN contenu à l’aide de HTTPS a hello suivant des contraintes :</span><span class="sxs-lookup"><span data-stu-id="a491c-144">Accessing CDN content using HTTPS has hello following constraints:</span></span>
   > 
   > * <span data-ttu-id="a491c-145">Vous devez utiliser le certificat SSL de hello fournie par hello CDN.</span><span class="sxs-lookup"><span data-stu-id="a491c-145">You must use hello SSL certificate provided by hello CDN.</span></span> <span data-ttu-id="a491c-146">Les certificats tiers ne sont pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="a491c-146">Third party certificates are not supported.</span></span>
   > * <span data-ttu-id="a491c-147">Vous devez utiliser le domaine CDN autant de hello (`<endpointname>.azureedge.net`) le contenu tooaccess HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a491c-147">You must use hello CDN-provided domain (`<endpointname>.azureedge.net`) tooaccess HTTPS content.</span></span> <span data-ttu-id="a491c-148">Prise en charge HTTPS n’est pas disponible pour les noms de domaines personnalisés (enregistrements CNAME) hello CDN ne prenant pas en charge les certificats personnalisés pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="a491c-148">HTTPS support is not available for custom domain names (CNAMEs) since hello CDN does not support custom certificates at this time.</span></span>
   > 
   > 
9. <span data-ttu-id="a491c-149">Cliquez sur hello **ajouter** bouton toocreate hello nouveau point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="a491c-149">Click hello **Add** button toocreate hello new endpoint.</span></span>
10. <span data-ttu-id="a491c-150">Une fois que le point de terminaison hello est créé, il apparaît dans une liste de points de terminaison pour le profil de hello.</span><span class="sxs-lookup"><span data-stu-id="a491c-150">Once hello endpoint is created, it appears in a list of endpoints for hello profile.</span></span> <span data-ttu-id="a491c-151">Hello liste affiche hello URL toouse tooaccess mis en cache le contenu, ainsi que le domaine d’origine hello.</span><span class="sxs-lookup"><span data-stu-id="a491c-151">hello list view shows hello URL toouse tooaccess cached content, as well as hello origin domain.</span></span>
    
    ![Point de terminaison CDN][cdn-endpoint-success]
    
    > [!IMPORTANT]
    > <span data-ttu-id="a491c-153">point de terminaison Hello pas immédiatement sera disponible pour une utilisation, comme le temps requis pour toopropagate d’inscription hello via hello CDN.</span><span class="sxs-lookup"><span data-stu-id="a491c-153">hello endpoint will not immediately be available for use, as it takes time for hello registration toopropagate through hello CDN.</span></span>  <span data-ttu-id="a491c-154">Pour <b>Azure CDN fourni par Akamai</b> , la propagation s’effectue généralement dans un délai d’une minute.</span><span class="sxs-lookup"><span data-stu-id="a491c-154">For <b>Azure CDN from Akamai</b> profiles, propagation will usually complete within one minute.</span></span>  <span data-ttu-id="a491c-155">Pour les profils du <b>CDN Azure fourni par Verizon</b>, la propagation s’effectue généralement dans un délai de 90 minutes, mais elle peut prendre plus de temps dans certains cas.</span><span class="sxs-lookup"><span data-stu-id="a491c-155">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
    > 
    > <span data-ttu-id="a491c-156">Les utilisateurs qui essaient de nom de domaine CDN toouse hello avant la configuration de point de terminaison hello a propagé toohello POP recevront des codes de réponse HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="a491c-156">Users who try toouse hello CDN domain name before hello endpoint configuration has propagated toohello POPs will receive HTTP 404 response codes.</span></span>  <span data-ttu-id="a491c-157">Si plusieurs heures se sont écoulées depuis la création de votre point de terminaison et que vous recevez toujours des réponses 404, consultez [Dépannage des points de terminaison de CDN renvoyant des états 404](cdn-troubleshoot-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="a491c-157">If it's been several hours since you created your endpoint and you're still receiving 404 responses, please see [Troubleshooting CDN endpoints returning 404 statuses](cdn-troubleshoot-endpoint.md).</span></span>
    > 
    > 

## <a name="see-also"></a><span data-ttu-id="a491c-158">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="a491c-158">See Also</span></span>
* [<span data-ttu-id="a491c-159">Contrôle du comportement de mise en cache des demandes avec des chaînes de requête</span><span class="sxs-lookup"><span data-stu-id="a491c-159">Controlling caching behavior of requests with query strings</span></span>](cdn-query-string.md)
* [<span data-ttu-id="a491c-160">Comment tooa de contenu CDN tooMap un domaine personnalisé</span><span class="sxs-lookup"><span data-stu-id="a491c-160">How tooMap CDN Content tooa Custom Domain</span></span>](cdn-map-content-to-custom-domain.md)
* [<span data-ttu-id="a491c-161">Préchargement d’éléments multimédias sur un point de terminaison CDN Azure</span><span class="sxs-lookup"><span data-stu-id="a491c-161">Pre-load assets on an Azure CDN endpoint</span></span>](cdn-preload-endpoint.md)
* [<span data-ttu-id="a491c-162">Purger un point de terminaison CDN Azure</span><span class="sxs-lookup"><span data-stu-id="a491c-162">Purge an Azure CDN Endpoint</span></span>](cdn-purge-endpoint.md)
* [<span data-ttu-id="a491c-163">Dépannage des points de terminaison de CDN renvoyant des états 404</span><span class="sxs-lookup"><span data-stu-id="a491c-163">Troubleshooting CDN endpoints returning 404 statuses</span></span>](cdn-troubleshoot-endpoint.md)

[cdn-profile-settings]: ./media/cdn-create-new-endpoint/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-create-new-endpoint/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-create-new-endpoint/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-create-new-endpoint/cdn-endpoint-success.png
