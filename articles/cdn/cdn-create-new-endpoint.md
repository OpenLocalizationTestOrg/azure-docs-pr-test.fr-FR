---
title: "Prise en main d’Azure CDN | Microsoft Docs"
description: "Cette rubrique montre comment activer le réseau de distribution de contenu (CDN) Azure. Ce didacticiel décrit la création d'un profil CDN et d’un point de terminaison."
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
ms.openlocfilehash: d263e911d0d0b3cdc1e48e300a3c8a0994b38c39
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-azure-cdn"></a><span data-ttu-id="6af05-104">Prise en main d’Azure CDN</span><span class="sxs-lookup"><span data-stu-id="6af05-104">Getting started with Azure CDN</span></span>
<span data-ttu-id="6af05-105">Cette rubrique décrit l’activation d’Azure CDN en créant un nouveau profil CDN et un point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="6af05-105">This topic walks through enabling Azure CDN by creating a new CDN profile and endpoint.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6af05-106">Pour une présentation du fonctionnement du CDN, ainsi qu’une liste de fonctionnalités, consultez la [Présentation du CDN](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6af05-106">For an introduction to how CDN works, as well as a list of features, see the [CDN Overview](cdn-overview.md).</span></span>
> 
> 

## <a name="create-a-new-cdn-profile"></a><span data-ttu-id="6af05-107">Créer un profil CDN</span><span class="sxs-lookup"><span data-stu-id="6af05-107">Create a new CDN profile</span></span>
<span data-ttu-id="6af05-108">Un profil CDN est une collection de points de terminaison CDN.</span><span class="sxs-lookup"><span data-stu-id="6af05-108">A CDN profile is a collection of CDN endpoints.</span></span>  <span data-ttu-id="6af05-109">Chaque profil contient un ou plusieurs points de terminaison CDN.</span><span class="sxs-lookup"><span data-stu-id="6af05-109">Each profile contains one or more CDN endpoints.</span></span>  <span data-ttu-id="6af05-110">Vous pouvez utiliser plusieurs profils pour organiser vos points de terminaison CDN par domaine Internet, application web ou d'autres critères.</span><span class="sxs-lookup"><span data-stu-id="6af05-110">You may wish to use multiple profiles to organize your CDN endpoints by internet domain, web application, or some other criteria.</span></span>

> [!NOTE]
> <span data-ttu-id="6af05-111">Par défaut, un abonnement Azure unique est limité à huit profils CDN.</span><span class="sxs-lookup"><span data-stu-id="6af05-111">By default, a single Azure subscription is limited to eight CDN profiles.</span></span> <span data-ttu-id="6af05-112">Chaque profil CDN est limité à dix points de terminaison CDN.</span><span class="sxs-lookup"><span data-stu-id="6af05-112">Each CDN profile is limited to ten CDN endpoints.</span></span>
> 
> <span data-ttu-id="6af05-113">La tarification CDN est appliquée au niveau du profil CDN.</span><span class="sxs-lookup"><span data-stu-id="6af05-113">CDN pricing is applied at the CDN profile level.</span></span> <span data-ttu-id="6af05-114">Si vous souhaitez utiliser une combinaison de niveaux de tarification Azure CDN, vous aurez besoin de plusieurs profils CDN.</span><span class="sxs-lookup"><span data-stu-id="6af05-114">If you wish to use a mix of Azure CDN pricing tiers, you will need multiple CDN profiles.</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a><span data-ttu-id="6af05-115">Créer un point de terminaison CDN</span><span class="sxs-lookup"><span data-stu-id="6af05-115">Create a new CDN endpoint</span></span>
<span data-ttu-id="6af05-116">**Pour créer un point de terminaison CDN**</span><span class="sxs-lookup"><span data-stu-id="6af05-116">**To create a new CDN endpoint**</span></span>

1. <span data-ttu-id="6af05-117">Dans le [portail Azure](https://portal.azure.com), accédez à votre profil CDN.</span><span class="sxs-lookup"><span data-stu-id="6af05-117">In the [Azure Portal](https://portal.azure.com), navigate to your CDN profile.</span></span>  <span data-ttu-id="6af05-118">Vous l'avez peut-être épinglé au tableau de bord à l'étape précédente.</span><span class="sxs-lookup"><span data-stu-id="6af05-118">You may have pinned it to the dashboard in the previous step.</span></span>  <span data-ttu-id="6af05-119">Dans le cas contraire, vous le trouverez en cliquant sur **Parcourir**, puis **Profils CDN** et en cliquant sur le profil auquel vous voulez ajouter le point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="6af05-119">If you not, you can find it by clicking **Browse**, then **CDN profiles**, and clicking on the profile you plan to add your endpoint to.</span></span>
   
    <span data-ttu-id="6af05-120">Le panneau du profil CDN s'affiche.</span><span class="sxs-lookup"><span data-stu-id="6af05-120">The CDN profile blade appears.</span></span>
   
    ![Profil CDN][cdn-profile-settings]
2. <span data-ttu-id="6af05-122">Cliquez sur le bouton **Ajouter un point de terminaison** .</span><span class="sxs-lookup"><span data-stu-id="6af05-122">Click the **Add Endpoint** button.</span></span>
   
    ![Bouton Ajouter un point de terminaison][cdn-new-endpoint-button]
   
    <span data-ttu-id="6af05-124">Le panneau **Ajouter un point de terminaison** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="6af05-124">The **Add an endpoint** blade appears.</span></span>
   
    ![Panneau Ajouter un point de terminaison][cdn-add-endpoint]
3. <span data-ttu-id="6af05-126">Entrez un **nom** pour ce point de terminaison CDN.</span><span class="sxs-lookup"><span data-stu-id="6af05-126">Enter a **Name** for this CDN endpoint.</span></span>  <span data-ttu-id="6af05-127">Ce nom servira à accéder à vos ressources en cache au niveau du domaine `<endpointname>.azureedge.net`.</span><span class="sxs-lookup"><span data-stu-id="6af05-127">This name will be used to access your cached resources at the domain `<endpointname>.azureedge.net`.</span></span>
4. <span data-ttu-id="6af05-128">Dans la liste déroulante **Type d’origine** , sélectionnez votre type d’origine.</span><span class="sxs-lookup"><span data-stu-id="6af05-128">In the **Origin type** dropdown, select your origin type.</span></span>  <span data-ttu-id="6af05-129">Sélectionnez **Stockage** pour un compte de stockage Azure, **Service cloud** pour un service cloud Azure, **Application web** pour une application web Azure ou **Origine personnalisée** pour toute autre origine de serveur web accessible publiquement (hébergé dans Azure ou ailleurs).</span><span class="sxs-lookup"><span data-stu-id="6af05-129">Select **Storage** for an Azure Storage account, **Cloud service** for an Azure Cloud Service, **Web App** for an Azure Web App, or **Custom origin** for any other publicly accessible web server origin (hosted in Azure or elsewhere).</span></span>
   
    ![Type d'origine CDN](./media/cdn-create-new-endpoint/cdn-origin-type.png)
5. <span data-ttu-id="6af05-131">Dans la liste déroulante **Nom d’hôte d’origine** , sélectionnez ou tapez votre domaine d’origine.</span><span class="sxs-lookup"><span data-stu-id="6af05-131">In the **Origin hostname** dropdown, select or type your origin domain.</span></span>  <span data-ttu-id="6af05-132">La liste déroulante répertorie toutes les origines disponibles du type spécifié à l'étape 4.</span><span class="sxs-lookup"><span data-stu-id="6af05-132">The dropdown will list all available origins of the type you specified in step 4.</span></span>  <span data-ttu-id="6af05-133">Si vous avez sélectionné *Origine personnalisée* comme **type d’origine**, tapez le domaine de votre origine personnalisée.</span><span class="sxs-lookup"><span data-stu-id="6af05-133">If you selected *Custom origin* as your **Origin type**, you will type in the domain of your custom origin.</span></span>
6. <span data-ttu-id="6af05-134">Dans la zone de texte **Chemin d’accès d’origine** , entrez le chemin d’accès aux ressources que vous souhaitez mettre en cache ou laissez cette zone vide pour autoriser la mise en cache de n’importe quelle ressource au niveau du domaine spécifié à l’étape 5.</span><span class="sxs-lookup"><span data-stu-id="6af05-134">In the **Origin path** text box, enter the path to the resources you want to cache, or leave blank to allow cache any resource at the domain you specified in step 5.</span></span>
7. <span data-ttu-id="6af05-135">Dans **En-tête de l’hôte d’origine**, entrez l’en-tête de l’hôte que le CDN doit envoyer avec chaque requête ou conservez la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="6af05-135">In the **Origin host header**, enter the host header you want the CDN to send with each request, or leave the default.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="6af05-136">Certains types d’origine, tels que Azure Storage et Web Apps, nécessitent l’en-tête de l’hôte pour correspondre au domaine de l’origine.</span><span class="sxs-lookup"><span data-stu-id="6af05-136">Some types of origins, such as Azure Storage and Web Apps, require the host header to match the domain of the origin.</span></span> <span data-ttu-id="6af05-137">À moins d’avoir une origine nécessitant un en-tête d’hôte différent de son domaine, vous devriez laisser la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="6af05-137">Unless you have an origin that requires a host header different from its domain, you should leave the default value.</span></span>
   > 
   > 
8. <span data-ttu-id="6af05-138">Pour **Protocole** et **Port d’origine**, spécifiez les protocoles et les ports utilisés pour accéder à vos ressources à l’origine.</span><span class="sxs-lookup"><span data-stu-id="6af05-138">For **Protocol** and **Origin port**, specify the protocols and ports used to access your resources at the origin.</span></span>  <span data-ttu-id="6af05-139">Vous devez sélectionner au moins un protocole (HTTP ou HTTPS).</span><span class="sxs-lookup"><span data-stu-id="6af05-139">At least one protocol (HTTP or HTTPS) must be selected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6af05-140">Le **port d’origine** ne concerne que le port utilisé par le point de terminaison pour récupérer des informations à partir de l’origine.</span><span class="sxs-lookup"><span data-stu-id="6af05-140">The **Origin port** only affects what port the endpoint uses to retrieve information from the origin.</span></span>  <span data-ttu-id="6af05-141">Le point de terminaison ne sera disponible pour les clients que sur les ports HTTP et HTTPS par défaut (80 et 443), quel que soit le **port d’origine**.</span><span class="sxs-lookup"><span data-stu-id="6af05-141">The endpoint itself will only be available to end clients on the default HTTP and HTTPS ports (80 and 443), regardless of the **Origin port**.</span></span>  
   > 
   > <span data-ttu-id="6af05-142">**Azure CDN fourni par Akamai** n’autorisent pas la plage de ports TCP complète pour les origines.</span><span class="sxs-lookup"><span data-stu-id="6af05-142">**Azure CDN from Akamai** endpoints do not allow the full TCP port range for origins.</span></span>  <span data-ttu-id="6af05-143">Pour obtenir la liste des ports d’origine non autorisés, consultez l’article [Azure CDN from Akamai Allowed Origin Ports](https://msdn.microsoft.com/library/mt757337.aspx)(Ports d’origine autorisés du CDN Azure fourni par Akamai).</span><span class="sxs-lookup"><span data-stu-id="6af05-143">For a list of origin ports that are not allowed, see [Azure CDN from Akamai Allowed Origin Ports](https://msdn.microsoft.com/library/mt757337.aspx).</span></span>  
   > 
   > <span data-ttu-id="6af05-144">L'accès à du contenu CDN à l'aide du protocole HTTPS présente les contraintes suivantes :</span><span class="sxs-lookup"><span data-stu-id="6af05-144">Accessing CDN content using HTTPS has the following constraints:</span></span>
   > 
   > * <span data-ttu-id="6af05-145">Vous devez utiliser le certificat SSL fourni par le CDN.</span><span class="sxs-lookup"><span data-stu-id="6af05-145">You must use the SSL certificate provided by the CDN.</span></span> <span data-ttu-id="6af05-146">Les certificats tiers ne sont pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="6af05-146">Third party certificates are not supported.</span></span>
   > * <span data-ttu-id="6af05-147">Vous devez utiliser le domaine fourni par le CDN (`<endpointname>.azureedge.net`) pour accéder au contenu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="6af05-147">You must use the CDN-provided domain (`<endpointname>.azureedge.net`) to access HTTPS content.</span></span> <span data-ttu-id="6af05-148">La prise en charge du protocole HTTPS n'est pas disponible pour les noms de domaines personnalisés (enregistrements CNAME), car le CDN ne prend pas en charge les certificats personnalisés pour l'instant.</span><span class="sxs-lookup"><span data-stu-id="6af05-148">HTTPS support is not available for custom domain names (CNAMEs) since the CDN does not support custom certificates at this time.</span></span>
   > 
   > 
9. <span data-ttu-id="6af05-149">Cliquez sur le bouton **Ajouter** pour créer le point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="6af05-149">Click the **Add** button to create the new endpoint.</span></span>
10. <span data-ttu-id="6af05-150">Une fois le point de terminaison créé, il s'affiche dans la liste des points de terminaison pour le profil.</span><span class="sxs-lookup"><span data-stu-id="6af05-150">Once the endpoint is created, it appears in a list of endpoints for the profile.</span></span> <span data-ttu-id="6af05-151">L’affichage sous forme de liste montre l’URL à utiliser pour accéder au contenu mis en cache et le domaine d’origine.</span><span class="sxs-lookup"><span data-stu-id="6af05-151">The list view shows the URL to use to access cached content, as well as the origin domain.</span></span>
    
    ![Point de terminaison CDN][cdn-endpoint-success]
    
    > [!IMPORTANT]
    > <span data-ttu-id="6af05-153">Le point de terminaison ne sera pas disponible immédiatement, car la propagation de l’enregistrement dans le CDN peut prendre du temps.</span><span class="sxs-lookup"><span data-stu-id="6af05-153">The endpoint will not immediately be available for use, as it takes time for the registration to propagate through the CDN.</span></span>  <span data-ttu-id="6af05-154">Pour <b>Azure CDN fourni par Akamai</b> , la propagation s’effectue généralement dans un délai d’une minute.</span><span class="sxs-lookup"><span data-stu-id="6af05-154">For <b>Azure CDN from Akamai</b> profiles, propagation will usually complete within one minute.</span></span>  <span data-ttu-id="6af05-155">Pour les profils du <b>CDN Azure fourni par Verizon</b>, la propagation s’effectue généralement dans un délai de 90 minutes, mais elle peut prendre plus de temps dans certains cas.</span><span class="sxs-lookup"><span data-stu-id="6af05-155">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
    > 
    > <span data-ttu-id="6af05-156">Les utilisateurs qui tentent d’utiliser le nom de domaine CDN avant la propagation de la configuration du point de terminaison aux POP voient s’afficher des codes de réponse HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="6af05-156">Users who try to use the CDN domain name before the endpoint configuration has propagated to the POPs will receive HTTP 404 response codes.</span></span>  <span data-ttu-id="6af05-157">Si plusieurs heures se sont écoulées depuis la création de votre point de terminaison et que vous recevez toujours des réponses 404, consultez [Dépannage des points de terminaison de CDN renvoyant des états 404](cdn-troubleshoot-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="6af05-157">If it's been several hours since you created your endpoint and you're still receiving 404 responses, please see [Troubleshooting CDN endpoints returning 404 statuses](cdn-troubleshoot-endpoint.md).</span></span>
    > 
    > 

## <a name="see-also"></a><span data-ttu-id="6af05-158">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="6af05-158">See Also</span></span>
* [<span data-ttu-id="6af05-159">Contrôle du comportement de mise en cache des demandes avec des chaînes de requête</span><span class="sxs-lookup"><span data-stu-id="6af05-159">Controlling caching behavior of requests with query strings</span></span>](cdn-query-string.md)
* [<span data-ttu-id="6af05-160">Mappage du contenu CDN à un domaine personnalisé</span><span class="sxs-lookup"><span data-stu-id="6af05-160">How to Map CDN Content to a Custom Domain</span></span>](cdn-map-content-to-custom-domain.md)
* [<span data-ttu-id="6af05-161">Préchargement d’éléments multimédias sur un point de terminaison CDN Azure</span><span class="sxs-lookup"><span data-stu-id="6af05-161">Pre-load assets on an Azure CDN endpoint</span></span>](cdn-preload-endpoint.md)
* [<span data-ttu-id="6af05-162">Purger un point de terminaison CDN Azure</span><span class="sxs-lookup"><span data-stu-id="6af05-162">Purge an Azure CDN Endpoint</span></span>](cdn-purge-endpoint.md)
* [<span data-ttu-id="6af05-163">Dépannage des points de terminaison de CDN renvoyant des états 404</span><span class="sxs-lookup"><span data-stu-id="6af05-163">Troubleshooting CDN endpoints returning 404 statuses</span></span>](cdn-troubleshoot-endpoint.md)

[cdn-profile-settings]: ./media/cdn-create-new-endpoint/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-create-new-endpoint/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-create-new-endpoint/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-create-new-endpoint/cdn-endpoint-success.png
