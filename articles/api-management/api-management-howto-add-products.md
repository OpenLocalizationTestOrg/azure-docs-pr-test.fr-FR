---
title: "Création et publication d'un produit dans Gestion des API Azure"
description: "Apprenez à créer et à publier des produits dans Gestion des API Azure."
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
ms.openlocfilehash: 73bf4451ba1b71807e22440beecc73a7e8045c5e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-publish-a-product-in-azure-api-management"></a><span data-ttu-id="c798f-103">Création et publication d'un produit dans Gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="c798f-103">How to create and publish a product in Azure API Management</span></span>
<span data-ttu-id="c798f-104">Dans Gestion des API Azure, un produit contient une ou plusieurs API, ainsi qu’un quota et des conditions d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="c798f-104">In Azure API Management, a product contains one or more APIs as well as a usage quota and the terms of use.</span></span> <span data-ttu-id="c798f-105">Une fois le produit publié, les développeurs peuvent s'y abonner et commencer à utiliser ses API.</span><span class="sxs-lookup"><span data-stu-id="c798f-105">Once a product is published, developers can subscribe to the product and begin to use the product's APIs.</span></span> <span data-ttu-id="c798f-106">Cette rubrique constitue un guide pour créer un produit, ajouter une API et le publier pour les développeurs.</span><span class="sxs-lookup"><span data-stu-id="c798f-106">The topic provides a guide to creating a product, adding an API, and publishing it for developers.</span></span>

## <span data-ttu-id="c798f-107"><a name="create-product"> </a>Création d’un produit</span><span class="sxs-lookup"><span data-stu-id="c798f-107"><a name="create-product"> </a>Create a product</span></span>
<span data-ttu-id="c798f-108">Les opérations sont ajoutées et configurées dans une API sur le portail des éditeurs.</span><span class="sxs-lookup"><span data-stu-id="c798f-108">Operations are added and configured to an API in the publisher portal.</span></span> <span data-ttu-id="c798f-109">Pour accéder au portail des éditeurs, cliquez sur **Portail des éditeurs** dans le portail Azure de votre service Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="c798f-109">To access the publisher portal, click **Publisher portal** in the Azure Portal for your API Management service.</span></span>

![Portail des éditeurs][api-management-management-console]

> <span data-ttu-id="c798f-111">Si vous n’avez pas encore créé une instance de service Gestion des API, consultez la page de [création d’une instance de service Gestion des API][Create an API Management service instance] dans le didacticiel de [prise en main de Gestion des API Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="c798f-111">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="c798f-112">Cliquez sur **Produits** dans le menu à gauche pour afficher la page **Produits**, puis cliquez sur **Ajouter un produit**.</span><span class="sxs-lookup"><span data-stu-id="c798f-112">Click on **Products** in the menu on the left to display the **Products** page, and click **Add Product**.</span></span>

![Produits][api-management-products]

![New product][api-management-add-new-product]

<span data-ttu-id="c798f-115">Entrez un nom décrivant le produit dans le champ **Nom**, ainsi qu’une description du produit dans le champ **Description**.</span><span class="sxs-lookup"><span data-stu-id="c798f-115">Enter a descriptive name for the product in the **Name** field and a description of the product in the **Description** field.</span></span>

<span data-ttu-id="c798f-116">Les produits de Gestion des API peuvent être **Ouverts** ou **Protégés**.</span><span class="sxs-lookup"><span data-stu-id="c798f-116">Products in API Management can be **Open** or **Protected**.</span></span> <span data-ttu-id="c798f-117">Les produits protégés doivent faire l’objet d’un abonnement avant de pouvoir être utilisés, alors que les produits ouverts peuvent être utilisés sans abonnement.</span><span class="sxs-lookup"><span data-stu-id="c798f-117">Protected products must be subscribed to before they can be used, while open products can be used without a subscription.</span></span> <span data-ttu-id="c798f-118">Cochez la case **Demander une approbation d’abonnement** pour créer un produit protégé qui requiert un abonnement.</span><span class="sxs-lookup"><span data-stu-id="c798f-118">Check **Require subscription** to create a protected product that requires a subscription.</span></span> <span data-ttu-id="c798f-119">Il s’agit du paramètre par défaut.</span><span class="sxs-lookup"><span data-stu-id="c798f-119">This is the default setting.</span></span>

<span data-ttu-id="c798f-120">Cochez **Demander une approbation d'abonnement** si vous souhaitez qu'un administrateur révise et accepte ou refuse les tentatives d'abonnement à ce produit.</span><span class="sxs-lookup"><span data-stu-id="c798f-120">Check **Require subscription approval** if you want an administrator to review and accept or reject subscription attempts to this product.</span></span> <span data-ttu-id="c798f-121">Si la case n'est pas cochée, les tentatives d'abonnement seront automatiquement approuvées.</span><span class="sxs-lookup"><span data-stu-id="c798f-121">If the box is unchecked, subscription attempts will be auto-approved.</span></span> <span data-ttu-id="c798f-122">Pour plus d’informations sur les abonnements, consultez la section [Affichage des abonnés à un produit][View subscribers to a product].</span><span class="sxs-lookup"><span data-stu-id="c798f-122">For more information on subscriptions, see [View subscribers to a product][View subscribers to a product].</span></span>

<span data-ttu-id="c798f-123">Pour autoriser les comptes de développeur à s’abonner plusieurs fois au produit, cochez la case **Autoriser plusieurs abonnements** .</span><span class="sxs-lookup"><span data-stu-id="c798f-123">To allow developer accounts to subscribe multiple times to the product, check the **Allow multiple subscriptions** check box.</span></span> <span data-ttu-id="c798f-124">Si cette case n’est pas cochée, chaque compte de développeur ne peut s’abonner qu’une seule fois pour le produit.</span><span class="sxs-lookup"><span data-stu-id="c798f-124">If this box is not checked, each developer account can subscribe only a single time to the product.</span></span>

![Abonnements multiples illimités][api-management-unlimited-multiple-subscriptions]

<span data-ttu-id="c798f-126">Pour limiter le nombre d’abonnements simultanés, cochez la case **Limiter le nombre d’abonnements simultanés à** et entrez le nombre limite d’abonnements.</span><span class="sxs-lookup"><span data-stu-id="c798f-126">To limit the count of multiple simultaneous subscriptions, check the **Limit number of simultaneous subscriptions to** check box and enter the subscription limit.</span></span> <span data-ttu-id="c798f-127">Dans l’exemple suivant, les abonnements simultanés sont limités à quatre par compte de développeur.</span><span class="sxs-lookup"><span data-stu-id="c798f-127">In the following example, simultaneous subscriptions are limited to four per developer account.</span></span>

![Quatre abonnements multiples][api-management-four-multiple-subscriptions]

<span data-ttu-id="c798f-129">Une fois que toutes les nouvelles options du produit sont configurées, cliquez sur **Enregistrer** pour créer ce dernier.</span><span class="sxs-lookup"><span data-stu-id="c798f-129">Once all new product options are configured, click **Save** to create the new product.</span></span>

![Produits][api-management-products-page]

> <span data-ttu-id="c798f-131">Par défaut, les nouveaux produits ne sont pas publiés et ne sont visibles que pour les utilisateurs du groupe **Administrateurs** .</span><span class="sxs-lookup"><span data-stu-id="c798f-131">By default new products are unpublished, and are visible only to the  **Administrators** group.</span></span>
> 
> 

<span data-ttu-id="c798f-132">Pour configurer un produit, cliquez sur son nom dans l'onglet **Produits** .</span><span class="sxs-lookup"><span data-stu-id="c798f-132">To configure a product, click on the product name in the **Products** tab.</span></span>

## <span data-ttu-id="c798f-133"><a name="add-apis"> </a>Ajout d’API à un produit</span><span class="sxs-lookup"><span data-stu-id="c798f-133"><a name="add-apis"> </a>Add APIs to a product</span></span>
<span data-ttu-id="c798f-134">La page **Produits** contient quatre liens de configuration : **Résumé**, **Paramètres**, **Visibilité** et **Abonnés**.</span><span class="sxs-lookup"><span data-stu-id="c798f-134">The **Products** page contains four links for configuration: **Summary**, **Settings**, **Visibility**, and **Subscribers**.</span></span> <span data-ttu-id="c798f-135">L’onglet **Résumé** est celui dans lequel vous pouvez ajouter des API et publier un produit, ou en annuler la publication.</span><span class="sxs-lookup"><span data-stu-id="c798f-135">The **Summary** tab is where you can add APIs and publish or unpublish a product.</span></span>

![Résumé][api-management-new-product-summary]

<span data-ttu-id="c798f-137">Avant de publier votre produit, vous devez ajouter une ou plusieurs API.</span><span class="sxs-lookup"><span data-stu-id="c798f-137">Before publishing your product you need to add one or more APIs.</span></span> <span data-ttu-id="c798f-138">Pour cela, cliquez sur **Ajouter l'API au produit**.</span><span class="sxs-lookup"><span data-stu-id="c798f-138">To do this, click **Add API to product**.</span></span>

![Add APIs][api-management-add-apis-to-product]

<span data-ttu-id="c798f-140">Sélectionnez les API voulues, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="c798f-140">Select the desired APIs and click **Save**.</span></span>

## <span data-ttu-id="c798f-141"><a name="add-description"> </a>Ajout d’informations descriptives à un produit</span><span class="sxs-lookup"><span data-stu-id="c798f-141"><a name="add-description"> </a>Add descriptive information to a product</span></span>
<span data-ttu-id="c798f-142">L’onglet **Paramètres** vous permet d’ajouter des informations détaillées sur le produit, comme son objectif, les API auxquelles il permet l’accès, ainsi que d’autres informations utiles.</span><span class="sxs-lookup"><span data-stu-id="c798f-142">The **Settings** tab allows you to provide detailed information about the product such as its purpose, the APIs it provides access to, and other useful information.</span></span> <span data-ttu-id="c798f-143">Le contenu est destiné aux développeurs qui appelleront l'API. Il peut être sous forme de texte brut ou au format HTML.</span><span class="sxs-lookup"><span data-stu-id="c798f-143">The content is targeted at the developers that will be calling the API and can be written in plain text or HTML markup.</span></span>

![Product settings][api-management-product-settings]

<span data-ttu-id="c798f-145">Cochez **Demander une approbation d’abonnement** pour créer un produit protégé dont l’utilisation requiert un abonnement, ou décochez la case à cocher pour créer un produit ouvert qui peut être appelé sans abonnement.</span><span class="sxs-lookup"><span data-stu-id="c798f-145">Check **Require subscription** to create a protected product that requires a subscription to be used, or clear the checkbox to create an open product that can be called without a subscription.</span></span>

<span data-ttu-id="c798f-146">Sélectionnez **Demander une approbation d'abonnement** si vous souhaitez approuver manuellement toutes les demandes d'abonnement au produit.</span><span class="sxs-lookup"><span data-stu-id="c798f-146">Select **Require subscription approval** if you want to manually approve all product subscription requests.</span></span> <span data-ttu-id="c798f-147">Par défaut, tous les abonnements sont acceptés automatiquement.</span><span class="sxs-lookup"><span data-stu-id="c798f-147">By default all product subscriptions are granted automatically.</span></span>

<span data-ttu-id="c798f-148">Pour autoriser les comptes de développeur à s’abonner plusieurs fois au produit, cochez la case **Autoriser plusieurs abonnements** et définissez une limite si besoin.</span><span class="sxs-lookup"><span data-stu-id="c798f-148">To allow developer accounts to subscribe multiple times to the product, check the **Allow multiple subscriptions** check box and optionally specify a limit.</span></span> <span data-ttu-id="c798f-149">Si cette case n’est pas cochée, chaque compte de développeur ne peut s’abonner qu’une seule fois pour le produit.</span><span class="sxs-lookup"><span data-stu-id="c798f-149">If this box is not checked, each developer account can subscribe only a single time to the product.</span></span>

<span data-ttu-id="c798f-150">Vous pouvez si vous le souhaitez remplir le champ **Conditions d'utilisation** qui décrit les conditions d'utilisation que les abonnés doivent accepter pour pouvoir utiliser le produit.</span><span class="sxs-lookup"><span data-stu-id="c798f-150">Optionally fill in the **Terms of use** field describing the terms of use for the product which subscribers must accept in order to use the product.</span></span>

## <span data-ttu-id="c798f-151"><a name="publish-product"> </a>Publication d’un produit</span><span class="sxs-lookup"><span data-stu-id="c798f-151"><a name="publish-product"> </a>Publish a product</span></span>
<span data-ttu-id="c798f-152">Avant de pouvoir appeler les API dans un produit, ce produit doit être publié.</span><span class="sxs-lookup"><span data-stu-id="c798f-152">Before the APIs in a product can be called, the product must be published.</span></span> <span data-ttu-id="c798f-153">Dans l’onglet **Résumé** du produit, cliquez sur **Publier**, puis sur **Oui, publier** pour confirmer.</span><span class="sxs-lookup"><span data-stu-id="c798f-153">On the **Summary** tab for the product, click **Publish**, and then click **Yes, publish it** to confirm.</span></span> <span data-ttu-id="c798f-154">Pour rendre privé un produit préalablement publié, cliquez sur **Annuler la publication**.</span><span class="sxs-lookup"><span data-stu-id="c798f-154">To make a previously published product private, click **Unpublish**.</span></span>

![Publish product][api-management-publish-product]

## <span data-ttu-id="c798f-156"><a name="make-visible"> </a>Rendre un produit visible pour les développeurs</span><span class="sxs-lookup"><span data-stu-id="c798f-156"><a name="make-visible"> </a>Make a product visible to developers</span></span>
<span data-ttu-id="c798f-157">L'onglet **Visibilité** vous permet de choisir quels rôles sont en mesure de voir le produit sur le portail des développeurs et de s'abonner à ce produit.</span><span class="sxs-lookup"><span data-stu-id="c798f-157">The **Visibility** tab allows you to choose which roles are able to see the product on the developer portal and subscribe to the product.</span></span>

![Product visibility][api-management-product-visiblity]

<span data-ttu-id="c798f-159">Pour activer ou désactiver la visibilité d'un produit pour les développeurs d'un groupe, cochez ou décochez la case à côté du groupe, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="c798f-159">To enable or disable visibility of a product for the developers in a group, check or uncheck the check box beside the group and then click **Save**.</span></span>

> <span data-ttu-id="c798f-160">Pour plus d’informations, consultez la page [Création et utilisation de groupes pour gérer les comptes de développeurs dans Gestion des API Azure][How to create and use groups to manage developer accounts in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="c798f-160">For more information, see [How to create and use groups to manage developer accounts in Azure API Management][How to create and use groups to manage developer accounts in Azure API Management].</span></span>
> 
> 

## <span data-ttu-id="c798f-161"><a name="view-subscribers"> </a>Affichage des abonnés à un produit</span><span class="sxs-lookup"><span data-stu-id="c798f-161"><a name="view-subscribers"> </a>View subscribers to a product</span></span>
<span data-ttu-id="c798f-162">L’onglet **Abonnés** présente la liste des développeurs qui se sont abonnés au produit.</span><span class="sxs-lookup"><span data-stu-id="c798f-162">The **Subscribers** tab lists the developers who have subscribed to the product.</span></span> <span data-ttu-id="c798f-163">Les détails et les paramètres de chaque développeur peuvent être consultés en cliquant sur le nom du développeur.</span><span class="sxs-lookup"><span data-stu-id="c798f-163">The details and settings for each developer can be viewed by clicking on the developer's name.</span></span> <span data-ttu-id="c798f-164">Dans cet exemple, aucun développeur ne s'est encore abonné au produit.</span><span class="sxs-lookup"><span data-stu-id="c798f-164">In this example no developers have yet subscribed to the product.</span></span>

![Développeurs][api-management-developer-list]

## <span data-ttu-id="c798f-166"><a name="next-steps"> </a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c798f-166"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="c798f-167">Une fois les API souhaitées ajoutées et le produit publié, les développeurs peuvent s'abonner au produit et commencer à appeler les API.</span><span class="sxs-lookup"><span data-stu-id="c798f-167">Once the desired APIs are added and the product published, developers can subscribe to the product and begin to call the APIs.</span></span> <span data-ttu-id="c798f-168">Pour suivre le didacticiel présentant comment configurer ces éléments, ainsi que certains paramètres de produit avancés, consultez la page [Création et configuration de paramètres de produit avancés dans Gestion des API Azure][How create and configure advanced product settings in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="c798f-168">For a tutorial that demonstrates these items as well as advanced product configuration see [How create and configure advanced product settings in Azure API Management][How create and configure advanced product settings in Azure API Management].</span></span>

<span data-ttu-id="c798f-169">Pour plus d’informations sur l’utilisation des produits, consultez la vidéo suivante.</span><span class="sxs-lookup"><span data-stu-id="c798f-169">For more information about working with products, see the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Using-Products/player]
> 
> 

[Create a product]: #create-product
[Add APIs to a product]: #add-apis
[Add descriptive information to a product]: #add-description
[Publish a product]: #publish-product
[Make a product visible to developers]: #make-visible
[View subscribers to a product]: #view-subscribers
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


[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps
[How to create and use groups to manage developer accounts in Azure API Management]: api-management-howto-create-groups.md
[How create and configure advanced product settings in Azure API Management]: api-management-howto-product-with-rules.md 
