---
title: aaaHow toocreate et publier un produit de gestion des API Azure
description: "Découvrez comment toocreate et publier des produits dans la gestion des API Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 31de55cb-9384-490b-a2f2-6dfcf83da764
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: f0a37f08b4e29ca68be9caec4c7604e3b4b6aaa6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-publish-a-product-in-azure-api-management"></a><span data-ttu-id="71150-103">Comment toocreate et publier un produit de gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="71150-103">How toocreate and publish a product in Azure API Management</span></span>
<span data-ttu-id="71150-104">Dans Gestion des API Azure, un produit contient une ou plusieurs API ainsi que les conditions hello et de quota d’utilisation d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="71150-104">In Azure API Management, a product contains one or more APIs as well as a usage quota and hello terms of use.</span></span> <span data-ttu-id="71150-105">Une fois qu’un produit est publié, les développeurs peuvent s’abonner toohello produit et commencer l’API du produit toouse hello.</span><span class="sxs-lookup"><span data-stu-id="71150-105">Once a product is published, developers can subscribe toohello product and begin toouse hello product's APIs.</span></span> <span data-ttu-id="71150-106">rubrique de Hello fournit un guide toocreating un produit, l’ajout d’une API et sa publication pour les développeurs.</span><span class="sxs-lookup"><span data-stu-id="71150-106">hello topic provides a guide toocreating a product, adding an API, and publishing it for developers.</span></span>

## <span data-ttu-id="71150-107"><a name="create-product"></a>Création d’un produit</span><span class="sxs-lookup"><span data-stu-id="71150-107"><a name="create-product"> </a>Create a product</span></span>
<span data-ttu-id="71150-108">Les opérations sont ajoutées et configurés tooan API dans le portail de publication hello.</span><span class="sxs-lookup"><span data-stu-id="71150-108">Operations are added and configured tooan API in hello publisher portal.</span></span> <span data-ttu-id="71150-109">tooaccess hello cliquez portail, du serveur de publication **portail de publication** Bonjour portail Azure pour votre service de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="71150-109">tooaccess hello publisher portal, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span>

![Portail des éditeurs][api-management-management-console]

> <span data-ttu-id="71150-111">Si vous n’avez pas encore créé une instance de service de gestion des API, consultez [de créer une instance de service de gestion des API] [ Create an API Management service instance] Bonjour [prise en main Azure API Management] [ Get started with Azure API Management] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="71150-111">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="71150-112">Cliquez sur **produits** dans menu hello Bonjour toodisplay gauche Bonjour **produits** page, puis cliquez sur **ajouter un produit**.</span><span class="sxs-lookup"><span data-stu-id="71150-112">Click on **Products** in hello menu on hello left toodisplay hello **Products** page, and click **Add Product**.</span></span>

![Produits][api-management-products]

![New product][api-management-add-new-product]

<span data-ttu-id="71150-115">Entrez un nom descriptif pour le produit de hello Bonjour **nom** champ et une description du produit de hello en hello **Description** champ.</span><span class="sxs-lookup"><span data-stu-id="71150-115">Enter a descriptive name for hello product in hello **Name** field and a description of hello product in hello **Description** field.</span></span>

<span data-ttu-id="71150-116">Les produits de Gestion des API peuvent être **Ouverts** ou **Protégés**.</span><span class="sxs-lookup"><span data-stu-id="71150-116">Products in API Management can be **Open** or **Protected**.</span></span> <span data-ttu-id="71150-117">Produits protégés doivent être souscrit toobefore ils peuvent être utilisés pendant l’ouverture produits peuvent être utilisés sans abonnement.</span><span class="sxs-lookup"><span data-stu-id="71150-117">Protected products must be subscribed toobefore they can be used, while open products can be used without a subscription.</span></span> <span data-ttu-id="71150-118">Vérifiez **abonnement** toocreate un produit protégé qui nécessite un abonnement.</span><span class="sxs-lookup"><span data-stu-id="71150-118">Check **Require subscription** toocreate a protected product that requires a subscription.</span></span> <span data-ttu-id="71150-119">Il s’agit de paramètre par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="71150-119">This is hello default setting.</span></span>

<span data-ttu-id="71150-120">Vérifiez **exiger l’approbation de l’abonnement** si vous souhaitez un tooreview administrateur et l’accepter ou rejeter abonnement tente toothis produit.</span><span class="sxs-lookup"><span data-stu-id="71150-120">Check **Require subscription approval** if you want an administrator tooreview and accept or reject subscription attempts toothis product.</span></span> <span data-ttu-id="71150-121">Si hello est désactivée, les tentatives d’abonnement sera approuvée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="71150-121">If hello box is unchecked, subscription attempts will be auto-approved.</span></span> <span data-ttu-id="71150-122">Pour plus d’informations sur les abonnements, consultez [afficher le produit abonnés tooa][View subscribers tooa product].</span><span class="sxs-lookup"><span data-stu-id="71150-122">For more information on subscriptions, see [View subscribers tooa product][View subscribers tooa product].</span></span>

<span data-ttu-id="71150-123">tooallow développeur comptes toosubscribe produit de toohello plusieurs fois, vérifiez hello **autoriser plusieurs abonnements** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="71150-123">tooallow developer accounts toosubscribe multiple times toohello product, check hello **Allow multiple subscriptions** check box.</span></span> <span data-ttu-id="71150-124">Si cette case n’est pas activée, chaque compte de développeur peut s’abonner à un produit toohello seule fois uniquement.</span><span class="sxs-lookup"><span data-stu-id="71150-124">If this box is not checked, each developer account can subscribe only a single time toohello product.</span></span>

![Abonnements multiples illimités][api-management-unlimited-multiple-subscriptions]

<span data-ttu-id="71150-126">nombre de hello toolimit de plusieurs abonnements simultanés, vérifiez hello **limiter le nombre d’abonnements simultanés à** case à cocher et entrez la limite d’abonnement hello.</span><span class="sxs-lookup"><span data-stu-id="71150-126">toolimit hello count of multiple simultaneous subscriptions, check hello **Limit number of simultaneous subscriptions to** check box and enter hello subscription limit.</span></span> <span data-ttu-id="71150-127">Dans l’exemple suivant de hello, abonnements simultanés sont toofour limitée par le compte de développeur.</span><span class="sxs-lookup"><span data-stu-id="71150-127">In hello following example, simultaneous subscriptions are limited toofour per developer account.</span></span>

![Quatre abonnements multiples][api-management-four-multiple-subscriptions]

<span data-ttu-id="71150-129">Une fois que toutes les nouvelles options de produit sont configurées, cliquez sur **enregistrer** produit toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="71150-129">Once all new product options are configured, click **Save** toocreate hello new product.</span></span>

![Produits][api-management-products-page]

> <span data-ttu-id="71150-131">Par défaut les nouveaux produits non publiés et sont visible toohello uniquement **administrateurs** groupe.</span><span class="sxs-lookup"><span data-stu-id="71150-131">By default new products are unpublished, and are visible only toohello  **Administrators** group.</span></span>
> 
> 

<span data-ttu-id="71150-132">tooconfigure un produit, cliquez sur le nom du produit hello Bonjour **produits** onglet.</span><span class="sxs-lookup"><span data-stu-id="71150-132">tooconfigure a product, click on hello product name in hello **Products** tab.</span></span>

## <span data-ttu-id="71150-133"><a name="add-apis"></a>Produit de tooa ajouter des API</span><span class="sxs-lookup"><span data-stu-id="71150-133"><a name="add-apis"> </a>Add APIs tooa product</span></span>
<span data-ttu-id="71150-134">Hello **produits** page contient quatre des liens pour la configuration : **Résumé**, **paramètres**, **visibilité**, et  **Les abonnés**.</span><span class="sxs-lookup"><span data-stu-id="71150-134">hello **Products** page contains four links for configuration: **Summary**, **Settings**, **Visibility**, and **Subscribers**.</span></span> <span data-ttu-id="71150-135">Hello **Résumé** onglet est où vous pouvez ajouter les API et publier ou annuler la publication d’un produit.</span><span class="sxs-lookup"><span data-stu-id="71150-135">hello **Summary** tab is where you can add APIs and publish or unpublish a product.</span></span>

![Résumé][api-management-new-product-summary]

<span data-ttu-id="71150-137">Avant de publier votre produit vous devez tooadd une ou plusieurs API.</span><span class="sxs-lookup"><span data-stu-id="71150-137">Before publishing your product you need tooadd one or more APIs.</span></span> <span data-ttu-id="71150-138">toodo, cliquez sur **tooproduct d’ajouter les API**.</span><span class="sxs-lookup"><span data-stu-id="71150-138">toodo this, click **Add API tooproduct**.</span></span>

![Add APIs][api-management-add-apis-to-product]

<span data-ttu-id="71150-140">Sélectionnez hello souhaité API et cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="71150-140">Select hello desired APIs and click **Save**.</span></span>

## <span data-ttu-id="71150-141"><a name="add-description"></a>Produit de tooa ajouter des informations descriptives</span><span class="sxs-lookup"><span data-stu-id="71150-141"><a name="add-description"> </a>Add descriptive information tooa product</span></span>
<span data-ttu-id="71150-142">Hello **paramètres** onglet vous permet de tooprovide des informations détaillées sur le produit hello comme son objectif, hello donne accès à des API et autres informations utiles.</span><span class="sxs-lookup"><span data-stu-id="71150-142">hello **Settings** tab allows you tooprovide detailed information about hello product such as its purpose, hello APIs it provides access to, and other useful information.</span></span> <span data-ttu-id="71150-143">contenu de Hello est destiné aux développeurs de hello en appelant l’API de hello et peuvent être écrits en texte brut ou un balisage HTML.</span><span class="sxs-lookup"><span data-stu-id="71150-143">hello content is targeted at hello developers that will be calling hello API and can be written in plain text or HTML markup.</span></span>

![Product settings][api-management-product-settings]

<span data-ttu-id="71150-145">Vérifiez **abonnement** toocreate un produit protégé qui nécessite une toobe d’abonnement utilisé, ou désactivez hello case à cocher toocreate un produit en cours qui peut être appelé sans un abonnement.</span><span class="sxs-lookup"><span data-stu-id="71150-145">Check **Require subscription** toocreate a protected product that requires a subscription toobe used, or clear hello checkbox toocreate an open product that can be called without a subscription.</span></span>

<span data-ttu-id="71150-146">Sélectionnez **exiger l’approbation de l’abonnement** si vous souhaitez toomanually approuver toutes les demandes d’abonnement de produit.</span><span class="sxs-lookup"><span data-stu-id="71150-146">Select **Require subscription approval** if you want toomanually approve all product subscription requests.</span></span> <span data-ttu-id="71150-147">Par défaut, tous les abonnements sont acceptés automatiquement.</span><span class="sxs-lookup"><span data-stu-id="71150-147">By default all product subscriptions are granted automatically.</span></span>

<span data-ttu-id="71150-148">tooallow développeur comptes toosubscribe produit de toohello plusieurs fois, vérifiez hello **autoriser plusieurs abonnements** case à cocher et si vous le souhaitez spécifier une limite.</span><span class="sxs-lookup"><span data-stu-id="71150-148">tooallow developer accounts toosubscribe multiple times toohello product, check hello **Allow multiple subscriptions** check box and optionally specify a limit.</span></span> <span data-ttu-id="71150-149">Si cette case n’est pas activée, chaque compte de développeur peut s’abonner à un produit toohello seule fois uniquement.</span><span class="sxs-lookup"><span data-stu-id="71150-149">If this box is not checked, each developer account can subscribe only a single time toohello product.</span></span>

<span data-ttu-id="71150-150">Si vous le souhaitez renseignez hello **conditions d’utilisation** champ décrivant les conditions d’utilisation de hello pour le produit hello que les abonnés doivent accepter dans le produit de commande toouse hello.</span><span class="sxs-lookup"><span data-stu-id="71150-150">Optionally fill in hello **Terms of use** field describing hello terms of use for hello product which subscribers must accept in order toouse hello product.</span></span>

## <span data-ttu-id="71150-151"><a name="publish-product"></a>Publication d’un produit</span><span class="sxs-lookup"><span data-stu-id="71150-151"><a name="publish-product"> </a>Publish a product</span></span>
<span data-ttu-id="71150-152">Avant de hello API dans un produit peut être appelée, produit de hello doit être publié.</span><span class="sxs-lookup"><span data-stu-id="71150-152">Before hello APIs in a product can be called, hello product must be published.</span></span> <span data-ttu-id="71150-153">Sur hello **Résumé** pour le produit de hello, cliquez sur **publier**, puis cliquez sur **Oui, publiez-le** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="71150-153">On hello **Summary** tab for hello product, click **Publish**, and then click **Yes, publish it** tooconfirm.</span></span> <span data-ttu-id="71150-154">toomake privé produit précédemment publiée, cliquez sur **annuler la publication**.</span><span class="sxs-lookup"><span data-stu-id="71150-154">toomake a previously published product private, click **Unpublish**.</span></span>

![Publish product][api-management-publish-product]

## <span data-ttu-id="71150-156"><a name="make-visible"></a>Rendre un toodevelopers visible du produit</span><span class="sxs-lookup"><span data-stu-id="71150-156"><a name="make-visible"> </a>Make a product visible toodevelopers</span></span>
<span data-ttu-id="71150-157">Hello **visibilité** onglet vous permet de toochoose les rôles sont le produit de hello en mesure de toosee sur le portail des développeurs hello et s’abonner toohello produit.</span><span class="sxs-lookup"><span data-stu-id="71150-157">hello **Visibility** tab allows you toochoose which roles are able toosee hello product on hello developer portal and subscribe toohello product.</span></span>

![Product visibility][api-management-product-visiblity]

<span data-ttu-id="71150-159">visibilité tooenable ou désactivation d’un produit pour les développeurs de hello dans un groupe, ou désactivez la case à cocher en regard du groupe de hello hello, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="71150-159">tooenable or disable visibility of a product for hello developers in a group, check or uncheck hello check box beside hello group and then click **Save**.</span></span>

> <span data-ttu-id="71150-160">Pour plus d’informations, consultez [mode développeur de toomanage groupes toocreate et l’utilisation de comptes dans Gestion des API Azure][How toocreate and use groups toomanage developer accounts in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="71150-160">For more information, see [How toocreate and use groups toomanage developer accounts in Azure API Management][How toocreate and use groups toomanage developer accounts in Azure API Management].</span></span>
> 
> 

## <span data-ttu-id="71150-161"><a name="view-subscribers"></a>Afficher le produit tooa abonnés</span><span class="sxs-lookup"><span data-stu-id="71150-161"><a name="view-subscribers"> </a>View subscribers tooa product</span></span>
<span data-ttu-id="71150-162">Hello **abonnés** onglet répertorie les développeurs hello qui se sont abonnés toohello produit.</span><span class="sxs-lookup"><span data-stu-id="71150-162">hello **Subscribers** tab lists hello developers who have subscribed toohello product.</span></span> <span data-ttu-id="71150-163">Hello détails et les paramètres pour chaque développeur peuvent être affichés en cliquant sur le nom du développeur hello.</span><span class="sxs-lookup"><span data-stu-id="71150-163">hello details and settings for each developer can be viewed by clicking on hello developer's name.</span></span> <span data-ttu-id="71150-164">Dans cet exemple sans les développeurs ont encore abonnés toohello produit.</span><span class="sxs-lookup"><span data-stu-id="71150-164">In this example no developers have yet subscribed toohello product.</span></span>

![Développeurs][api-management-developer-list]

## <span data-ttu-id="71150-166"><a name="next-steps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="71150-166"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="71150-167">Une fois hello souhaité API ont été ajoutées et hello produit publié, les développeurs peuvent s’abonner toohello produit et commencer toocall hello API.</span><span class="sxs-lookup"><span data-stu-id="71150-167">Once hello desired APIs are added and hello product published, developers can subscribe toohello product and begin toocall hello APIs.</span></span> <span data-ttu-id="71150-168">Pour suivre le didacticiel présentant comment configurer ces éléments, ainsi que certains paramètres de produit avancés, consultez la page [Création et configuration de paramètres de produit avancés dans Gestion des API Azure][How create and configure advanced product settings in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="71150-168">For a tutorial that demonstrates these items as well as advanced product configuration see [How create and configure advanced product settings in Azure API Management][How create and configure advanced product settings in Azure API Management].</span></span>

<span data-ttu-id="71150-169">Pour plus d’informations sur l’utilisation des produits, consultez hello suivant vidéo.</span><span class="sxs-lookup"><span data-stu-id="71150-169">For more information about working with products, see hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Using-Products/player]
> 
> 

[Create a product]: #create-product
[Add APIs tooa product]: #add-apis
[Add descriptive information tooa product]: #add-description
[Publish a product]: #publish-product
[Make a product visible toodevelopers]: #make-visible
[View subscribers tooa product]: #view-subscribers
[Next steps]: #next-steps

[api-management-management-console]: ./media/api-management-howto-add-products/api-management-management-console.png
[api-management-add-product]: ./media/api-management-howto-add-products/api-management-add-product.png
[api-management-add-new-product]: ./media/api-management-howto-add-products/api-management-add-new-product.png
[api-management-unlimited-multiple-subscriptions]: ./media/api-management-howto-add-products/api-management-unlimited-multiple-subscriptions.png
[api-management-four-multiple-subscriptions]: ./media/api-management-howto-add-products/api-management-four-multiple-subscriptions.png
[api-management-products-page]: ./media/api-management-howto-add-products/api-management-products-page.png
[api-management-new-product-summary]: ./media/api-management-howto-add-products/api-management-new-product-summary.png
[api-management-add-apis-to-product]: ./media/api-management-howto-add-products/api-management-add-apis-to-product.png
[api-management-product-settings]: ./media/api-management-howto-add-products/api-management-product-settings.png
[api-management-publish-product]: ./media/api-management-howto-add-products/api-management-publish-product.png
[api-management-product-visiblity]: ./media/api-management-howto-add-products/api-management-product-visibility.png
[api-management-developer-list]: ./media/api-management-howto-add-products/api-management-developer-list.png



[api-management-products]: ./media/api-management-howto-add-products/api-management-products.png
[api-management-]: ./media/api-management-howto-add-products/
[api-management-]: ./media/api-management-howto-add-products/


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps
[How toocreate and use groups toomanage developer accounts in Azure API Management]: api-management-howto-create-groups.md
[How create and configure advanced product settings in Azure API Management]: api-management-howto-product-with-rules.md 
