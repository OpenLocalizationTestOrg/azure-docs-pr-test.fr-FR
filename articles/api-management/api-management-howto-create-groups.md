---
title: "Gérer des comptes de développeurs à l’aide de groupes dans Gestion des API Azure | Microsoft Docs"
description: "Apprenez à gérer des comptes de développeurs à l'aide de groupes dans Gestion des API Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 33660b45-442f-44be-9a4a-1899d7f699b0
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: b4d71cdfbab535b02542fbb26c7555265e5f9c37
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-use-groups-to-manage-developer-accounts-in-azure-api-management"></a><span data-ttu-id="91248-103">Création et utilisation de groupes pour gérer les comptes de développeurs dans Gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="91248-103">How to create and use groups to manage developer accounts in Azure API Management</span></span>
<span data-ttu-id="91248-104">Dans Gestion des API, les groupes permettent de gérer la visibilité des produits pour les développeurs.</span><span class="sxs-lookup"><span data-stu-id="91248-104">In API Management, groups are used to manage the visibility of products to developers.</span></span> <span data-ttu-id="91248-105">Les produits sont d'abord visibles pour les groupes. Les développeurs de ces groupes peuvent afficher les produits associés aux groupes et s'y abonner.</span><span class="sxs-lookup"><span data-stu-id="91248-105">Products are first made visible to groups, and then developers in those groups can view and subscribe to the products that are associated with the groups.</span></span> 

<span data-ttu-id="91248-106">Le service Gestion des API possède les groupes système suivants, qui ne sont pas modifiables.</span><span class="sxs-lookup"><span data-stu-id="91248-106">API Management has the following immutable system groups.</span></span>

* <span data-ttu-id="91248-107">**Administrateurs** : les administrateurs d’abonnements Azure sont membres de ce groupe.</span><span class="sxs-lookup"><span data-stu-id="91248-107">**Administrators** - Azure subscription administrators are members of this group.</span></span> <span data-ttu-id="91248-108">Les administrateurs gèrent les instances du service Gestion des API, créant les API, opérations et produits qui sont utilisés par les développeurs.</span><span class="sxs-lookup"><span data-stu-id="91248-108">Administrators manage API Management service instances, creating the APIs, operations, and products that are used by developers.</span></span>
* <span data-ttu-id="91248-109">**Développeurs** : les utilisateurs authentifiés du portail des développeurs appartiennent à ce groupe.</span><span class="sxs-lookup"><span data-stu-id="91248-109">**Developers** - Authenticated developer portal users fall into this group.</span></span> <span data-ttu-id="91248-110">Les développeurs sont les clients qui génèrent des applications grâce à vos API.</span><span class="sxs-lookup"><span data-stu-id="91248-110">Developers are the customers that build applications using your APIs.</span></span> <span data-ttu-id="91248-111">Les développeurs bénéficient d'un accès au portail des développeurs et génèrent des applications qui appellent les opérations d'une API.</span><span class="sxs-lookup"><span data-stu-id="91248-111">Developers are granted access to the developer portal and build applications that call the operations of an API.</span></span>
* <span data-ttu-id="91248-112">**Invités** : les utilisateurs non authentifiés du portail des développeurs, comme les prospects, qui consultent le portail des développeurs d’une instance d’API Management appartiennent à ce groupe.</span><span class="sxs-lookup"><span data-stu-id="91248-112">**Guests** - Unauthenticated developer portal users, such as prospective customers visiting the developer portal of an API Management instance fall into this group.</span></span> <span data-ttu-id="91248-113">Ils peuvent recevoir certains accès en lecture seule, comme la possibilité d'afficher les API, mais pas de les appeler.</span><span class="sxs-lookup"><span data-stu-id="91248-113">They can be granted certain read-only access, such as the ability to view APIs but not call them.</span></span>

<span data-ttu-id="91248-114">Outre ces groupes système, les administrateurs peuvent créer des groupes personnalisés ou [utiliser des groupes externes dans des locataires Azure Active Directory qui leur sont associés][leverage external groups in associated Azure Active Directory tenants].</span><span class="sxs-lookup"><span data-stu-id="91248-114">In addition to these system groups, administrators can create custom groups or [leverage external groups in associated Azure Active Directory tenants][leverage external groups in associated Azure Active Directory tenants].</span></span> <span data-ttu-id="91248-115">Des groupes externes et personnalisés peuvent être utilisés avec des groupes système offrant une certaine visibilité aux développeurs et un accès aux produits d’API.</span><span class="sxs-lookup"><span data-stu-id="91248-115">Custom and external groups can be used alongside system groups in giving developers visibility and access to API products.</span></span> <span data-ttu-id="91248-116">Vous pourriez, par exemple, créer un groupe personnalisé pour les développeurs affiliés à une organisation partenaire spécifique et leur permettre d’accéder aux API à partir d’un produit contenant uniquement des API pertinentes.</span><span class="sxs-lookup"><span data-stu-id="91248-116">For example, you could create one custom group for developers affiliated with a specific partner organization and allow them access to the APIs from a product containing relevant APIs only.</span></span> <span data-ttu-id="91248-117">Un utilisateur peut être membre de plusieurs groupes.</span><span class="sxs-lookup"><span data-stu-id="91248-117">A user can be a member of more than one group.</span></span>

<span data-ttu-id="91248-118">Ce guide explique comment les administrateurs de l'instance Gestion des API peuvent ajouter de nouveaux groupes et les associer à des produits et des développeurs.</span><span class="sxs-lookup"><span data-stu-id="91248-118">This guide shows how administrators of an API Management instance can add new groups and associate them with products and developers.</span></span>

> [!NOTE]
> <span data-ttu-id="91248-119">En plus de créer et gérer des groupes dans le portail de publication, vous pouvez créer et gérer vos groupes à l'aide de l’entité [Groupe](https://msdn.microsoft.com/library/azure/dn776329.aspx) de l’API REST de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="91248-119">In addition to creating and managing groups in the publisher portal, you can create and manage your groups using the API Management REST API [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) entity.</span></span>
> 
> 

## <span data-ttu-id="91248-120"><a name="create-group"> </a>Création d’un groupe</span><span class="sxs-lookup"><span data-stu-id="91248-120"><a name="create-group"> </a>Create a group</span></span>
<span data-ttu-id="91248-121">Pour créer un groupe, cliquez sur **Portail de publication** dans le portail Azure de votre service Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="91248-121">To create a new group, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="91248-122">Vous accédez au portail des éditeurs Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="91248-122">This takes you to the API Management publisher portal.</span></span>

![Portail des éditeurs][api-management-management-console]

> <span data-ttu-id="91248-124">Si vous n’avez pas encore créé une instance de service Gestion des API, consultez la page de [création d’une instance de service Gestion des API][Create an API Management service instance] dans le didacticiel de [prise en main de Gestion des API Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="91248-124">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="91248-125">Cliquez sur **Groupes** dans le menu **Gestion des API** à gauche, puis sur **Ajouter un groupe**.</span><span class="sxs-lookup"><span data-stu-id="91248-125">Click **Groups** from the **API Management** menu on the left, and then click **Add Group**.</span></span>

![Add new group][api-management-add-group]

<span data-ttu-id="91248-127">Entrez un nom unique pour le groupe, et éventuellement une description, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="91248-127">Enter a unique name for the group and an optional description, and click **Save**.</span></span>

![Add new group][api-management-add-group-window]

<span data-ttu-id="91248-129">Le nouveau groupe s'affiche dans l'onglet des groupes.</span><span class="sxs-lookup"><span data-stu-id="91248-129">The new group is displayed in the groups tab.</span></span> <span data-ttu-id="91248-130">Pour modifier le **nom** ou la **description** du groupe, cliquez sur le nom du groupe dans la liste.</span><span class="sxs-lookup"><span data-stu-id="91248-130">To edit the **Name** or **Description** of the group, click the name of the group in the list.</span></span> <span data-ttu-id="91248-131">Pour supprimer le groupe, cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="91248-131">To delete the group, click **Delete**.</span></span>

![Group added][api-management-new-group]

<span data-ttu-id="91248-133">Maintenant que le groupe est créé, il peut être associé à des produits et des développeurs.</span><span class="sxs-lookup"><span data-stu-id="91248-133">Now that the group is created, it can be associated with products and developers.</span></span>

## <span data-ttu-id="91248-134"><a name="associate-group-product"> </a>Association d’un groupe à un produit</span><span class="sxs-lookup"><span data-stu-id="91248-134"><a name="associate-group-product"> </a>Associate a group with a product</span></span>
<span data-ttu-id="91248-135">Pour associer un groupe à un produit, cliquez sur **Produits** dans le menu **Gestion des API** sur la gauche, puis cliquez sur le nom du produit souhaité.</span><span class="sxs-lookup"><span data-stu-id="91248-135">To associate a group with a product, click **Products** from the **API Management** menu on the left, and then click the name of the desired product.</span></span>

![Set visibility][api-management-add-group-to-product]

<span data-ttu-id="91248-137">Utilisez l'onglet **Visibilité** pour ajouter et supprimer des groupes et pour voir les groupes actuellement associés au produit.</span><span class="sxs-lookup"><span data-stu-id="91248-137">Select the **Visibility** tab to add and remove groups, and to view the current groups for the product.</span></span> <span data-ttu-id="91248-138">Pour ajouter ou supprimer des groupes, activez ou désactivez les cases à cocher des groupes voulus, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="91248-138">To add or remove groups, check or uncheck the checkboxes for the desired groups and click **Save**.</span></span>

![Set visibility][api-management-add-group-to-product-visibility]

> [!NOTE]
> <span data-ttu-id="91248-140">Pour ajouter des groupes Azure Active Directory, consultez la rubrique [Comment autoriser des comptes de développeur utilisant Azure Active Directory dans Gestion des API Azure](api-management-howto-aad.md).</span><span class="sxs-lookup"><span data-stu-id="91248-140">To add Azure Active Directory groups, see [How to authorize developer accounts using Azure Active Directory in Azure API Management](api-management-howto-aad.md).</span></span>
> 
> <span data-ttu-id="91248-141">Pour configurer les groupes depuis l’onglet**Visibilité** d’un produit, cliquez sur **Gérer des groupes**.</span><span class="sxs-lookup"><span data-stu-id="91248-141">To configure groups from the **Visibility** tab for a product, click **Manage Groups**.</span></span>
> 
> 

<span data-ttu-id="91248-142">Une fois le produit associé à un groupe, les développeurs de ce groupe peuvent le voir et s'y abonner.</span><span class="sxs-lookup"><span data-stu-id="91248-142">Once a product is associated with a group, developers in that group can view and subscribe to the product.</span></span>

## <span data-ttu-id="91248-143"><a name="associate-group-developer"> </a>Association des groupes aux développeurs</span><span class="sxs-lookup"><span data-stu-id="91248-143"><a name="associate-group-developer"> </a>Associate groups with developers</span></span>
<span data-ttu-id="91248-144">Pour associer des groupes aux développeurs, cliquez sur **Utilisateurs** dans le menu **Gestion des API** sur la gauche, puis activez la case à cocher à côté des développeurs à associer au groupe.</span><span class="sxs-lookup"><span data-stu-id="91248-144">To associate groups with developers, click **Users** from the **API Management** menu on the left, and then check the box beside the developers you wish to associate with a group.</span></span>

![Add developer to group][api-management-add-group-to-developer]

<span data-ttu-id="91248-146">Une fois que les développeurs souhaités sont sélectionnés, cliquez sur le groupe dans la liste déroulante **Ajouter au groupe** .</span><span class="sxs-lookup"><span data-stu-id="91248-146">Once the desired developers are checked, click the desired group in the **Add to Group** drop-down.</span></span> <span data-ttu-id="91248-147">Les développeurs peuvent être retirés des groupes via la liste déroulante **Supprimer du groupe** .</span><span class="sxs-lookup"><span data-stu-id="91248-147">Developers can be removed from groups by using the **Remove from Group** drop-down.</span></span> 

![Développeurs][api-management-add-group-to-developer-saved]

<span data-ttu-id="91248-149">Une fois l’association entre le développeur et le groupe ajoutée, vous pouvez la consulter dans l’onglet **Utilisateurs** .</span><span class="sxs-lookup"><span data-stu-id="91248-149">Once the association is added between the developer and the group, you can view it in the **Users** tab.</span></span>

## <span data-ttu-id="91248-150"><a name="next-steps"> </a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="91248-150"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="91248-151">Une fois le développeur ajouté à un groupe, il peut voir tous les produits associés à ce groupe et s'y abonner.</span><span class="sxs-lookup"><span data-stu-id="91248-151">Once a developer is added to a group, they can view and subscribe to the products associated with that group.</span></span> <span data-ttu-id="91248-152">Pour plus d’informations, consultez la page [Création et publication d’un produit dans Gestion des API Azure][How create and publish a product in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="91248-152">For more information, see [How create and publish a product in Azure API Management][How create and publish a product in Azure API Management],</span></span>
* <span data-ttu-id="91248-153">En plus de créer et gérer des groupes dans le portail de publication, vous pouvez créer et gérer vos groupes à l'aide de l’entité [Groupe](https://msdn.microsoft.com/library/azure/dn776329.aspx) de l’API REST de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="91248-153">In addition to creating and managing groups in the publisher portal, you can create and manage your groups using the API Management REST API [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) entity.</span></span>

[api-management-management-console]: ./media/api-management-howto-create-groups/api-management-management-console.png
[api-management-add-group]: ./media/api-management-howto-create-groups/api-management-add-group.png
[api-management-add-group-window]: ./media/api-management-howto-create-groups/api-management-add-group-window.png
[api-management-new-group]: ./media/api-management-howto-create-groups/api-management-new-group.png
[api-management-add-group-to-product]: ./media/api-management-howto-create-groups/api-management-add-group-to-product.png
[api-management-add-group-to-product-visibility]: ./media/api-management-howto-create-groups/api-management-add-group-to-product-visibility.png
[api-management-add-group-to-developer]: ./media/api-management-howto-create-groups/api-management-add-group-to-developer.png
[api-management-add-group-to-developer-saved]: ./media/api-management-howto-create-groups/api-management-add-group-to-developer-saved.png

[api-management-]: ./media/api-management-howto-create-groups/api-management-.png

[Create a group]: #create-group
[Associate a group with a product]: #associate-group-product
[Associate groups with developers]: #associate-group-developer
[Next steps]: #next-steps

[How create and publish a product in Azure API Management]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[leverage external groups in associated Azure Active Directory tenants]: api-management-howto-aad.md#how-to-add-an-external-azure-active-directory-group
