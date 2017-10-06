---
title: "comptes de développeur aaaManage à l’aide de groupes de gestion des API Azure | Documents Microsoft"
description: "Découvrez comment les développeurs toomanage comptes à l’aide groupes dans Gestion des API Azure"
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
ms.openlocfilehash: c46e010e41d9705ae161dcd60d734a76d19c9e93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-use-groups-toomanage-developer-accounts-in-azure-api-management"></a><span data-ttu-id="2fde0-103">Le mode développeur de toomanage groupes toocreate et l’utilisation de comptes dans Gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="2fde0-103">How toocreate and use groups toomanage developer accounts in Azure API Management</span></span>
<span data-ttu-id="2fde0-104">Gestion des API, les groupes sont visibilité de hello utilisé toomanage de toodevelopers de produits.</span><span class="sxs-lookup"><span data-stu-id="2fde0-104">In API Management, groups are used toomanage hello visibility of products toodevelopers.</span></span> <span data-ttu-id="2fde0-105">Produits sont premier toogroups de visible effectuées, et ensuite les développeurs dans ces groupes peuvent afficher et s’abonner toohello les produits qui sont associés aux groupes de hello.</span><span class="sxs-lookup"><span data-stu-id="2fde0-105">Products are first made visible toogroups, and then developers in those groups can view and subscribe toohello products that are associated with hello groups.</span></span> 

<span data-ttu-id="2fde0-106">Gestion des API a hello suivant groupes système immuables.</span><span class="sxs-lookup"><span data-stu-id="2fde0-106">API Management has hello following immutable system groups.</span></span>

* <span data-ttu-id="2fde0-107">**Administrateurs** : les administrateurs d’abonnements Azure sont membres de ce groupe.</span><span class="sxs-lookup"><span data-stu-id="2fde0-107">**Administrators** - Azure subscription administrators are members of this group.</span></span> <span data-ttu-id="2fde0-108">Administrateurs de gérer des instances de service de gestion des API, création hello API, opérations et produits qui sont utilisés par les développeurs.</span><span class="sxs-lookup"><span data-stu-id="2fde0-108">Administrators manage API Management service instances, creating hello APIs, operations, and products that are used by developers.</span></span>
* <span data-ttu-id="2fde0-109">**Développeurs** : les utilisateurs authentifiés du portail des développeurs appartiennent à ce groupe.</span><span class="sxs-lookup"><span data-stu-id="2fde0-109">**Developers** - Authenticated developer portal users fall into this group.</span></span> <span data-ttu-id="2fde0-110">Les développeurs sont des clients hello générer des applications à l’aide de votre API.</span><span class="sxs-lookup"><span data-stu-id="2fde0-110">Developers are hello customers that build applications using your APIs.</span></span> <span data-ttu-id="2fde0-111">Les développeurs sont accordées portail des développeurs accès toohello et générer des applications qui appellent des opérations d’une API hello.</span><span class="sxs-lookup"><span data-stu-id="2fde0-111">Developers are granted access toohello developer portal and build applications that call hello operations of an API.</span></span>
* <span data-ttu-id="2fde0-112">**Invités** -non authentifié utilisateurs du portail développeur, tels que les clients potentiels en visitant le portail des développeurs hello d’une baisse d’instance gestion des API dans ce groupe.</span><span class="sxs-lookup"><span data-stu-id="2fde0-112">**Guests** - Unauthenticated developer portal users, such as prospective customers visiting hello developer portal of an API Management instance fall into this group.</span></span> <span data-ttu-id="2fde0-113">Ils peuvent bénéficier de certain accès en lecture seule, par exemple, hello capacité tooview API mais pas de les appellent.</span><span class="sxs-lookup"><span data-stu-id="2fde0-113">They can be granted certain read-only access, such as hello ability tooview APIs but not call them.</span></span>

<span data-ttu-id="2fde0-114">Dans les groupes de système toothese plus, les administrateurs peuvent créer des groupes personnalisés ou [tirer parti des groupes externes dans les clients Azure Active Directory associés][leverage external groups in associated Azure Active Directory tenants].</span><span class="sxs-lookup"><span data-stu-id="2fde0-114">In addition toothese system groups, administrators can create custom groups or [leverage external groups in associated Azure Active Directory tenants][leverage external groups in associated Azure Active Directory tenants].</span></span> <span data-ttu-id="2fde0-115">Groupes personnalisés et externes peuvent être utilisés avec des groupes de systèmes en offrant aux développeurs une visibilité et accéder aux produits de tooAPI.</span><span class="sxs-lookup"><span data-stu-id="2fde0-115">Custom and external groups can be used alongside system groups in giving developers visibility and access tooAPI products.</span></span> <span data-ttu-id="2fde0-116">Par exemple, vous pouvez créer un groupe personnalisé pour les développeurs affiliés à spécifiques à une organisation partenaire et les autoriser à accéder toohello API à partir d’un produit contenant uniquement des API pertinentes.</span><span class="sxs-lookup"><span data-stu-id="2fde0-116">For example, you could create one custom group for developers affiliated with a specific partner organization and allow them access toohello APIs from a product containing relevant APIs only.</span></span> <span data-ttu-id="2fde0-117">Un utilisateur peut être membre de plusieurs groupes.</span><span class="sxs-lookup"><span data-stu-id="2fde0-117">A user can be a member of more than one group.</span></span>

<span data-ttu-id="2fde0-118">Ce guide explique comment les administrateurs de l'instance Gestion des API peuvent ajouter de nouveaux groupes et les associer à des produits et des développeurs.</span><span class="sxs-lookup"><span data-stu-id="2fde0-118">This guide shows how administrators of an API Management instance can add new groups and associate them with products and developers.</span></span>

> [!NOTE]
> <span data-ttu-id="2fde0-119">En outre toocreating et gérer des groupes dans le portail de publication hello, vous pouvez créer et gérer vos groupes à l’aide des API REST de gestion des API de hello [groupe](https://msdn.microsoft.com/library/azure/dn776329.aspx) entité.</span><span class="sxs-lookup"><span data-stu-id="2fde0-119">In addition toocreating and managing groups in hello publisher portal, you can create and manage your groups using hello API Management REST API [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) entity.</span></span>
> 
> 

## <span data-ttu-id="2fde0-120"><a name="create-group"></a>Création d’un groupe</span><span class="sxs-lookup"><span data-stu-id="2fde0-120"><a name="create-group"> </a>Create a group</span></span>
<span data-ttu-id="2fde0-121">toocreate un nouveau groupe, cliquez sur **portail de publication** Bonjour portail Azure pour votre service de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="2fde0-121">toocreate a new group, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="2fde0-122">Cela vous prend un portail de publication de gestion des API toohello.</span><span class="sxs-lookup"><span data-stu-id="2fde0-122">This takes you toohello API Management publisher portal.</span></span>

![Portail des éditeurs][api-management-management-console]

> <span data-ttu-id="2fde0-124">Si vous n’avez pas encore créé une instance de service de gestion des API, consultez [de créer une instance de service de gestion des API] [ Create an API Management service instance] Bonjour [prise en main Azure API Management] [ Get started with Azure API Management] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="2fde0-124">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="2fde0-125">Cliquez sur **groupes** de hello **gestion des API** menu sur hello gauche, puis cliquez sur **ajouter un groupe**.</span><span class="sxs-lookup"><span data-stu-id="2fde0-125">Click **Groups** from hello **API Management** menu on hello left, and then click **Add Group**.</span></span>

![Ajouter un nouveau groupe][api-management-add-group]

<span data-ttu-id="2fde0-127">Entrez un nom unique pour le groupe de hello et une description facultative, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="2fde0-127">Enter a unique name for hello group and an optional description, and click **Save**.</span></span>

![Ajouter un nouveau groupe][api-management-add-group-window]

<span data-ttu-id="2fde0-129">nouveau groupe de Hello s’affiche dans Bonjour groupes onglet tooedit Bonjour **nom** ou **Description** hello groupe de, cliquez sur nom hello du groupe hello dans la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="2fde0-129">hello new group is displayed in hello groups tab. tooedit hello **Name** or **Description** of hello group, click hello name of hello group in hello list.</span></span> <span data-ttu-id="2fde0-130">groupe de hello toodelete, cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="2fde0-130">toodelete hello group, click **Delete**.</span></span>

![Group added][api-management-new-group]

<span data-ttu-id="2fde0-132">Maintenant que hello groupe est créé, il peut être associé avec les produits et les développeurs.</span><span class="sxs-lookup"><span data-stu-id="2fde0-132">Now that hello group is created, it can be associated with products and developers.</span></span>

## <span data-ttu-id="2fde0-133"><a name="associate-group-product"></a>Association d’un groupe à un produit</span><span class="sxs-lookup"><span data-stu-id="2fde0-133"><a name="associate-group-product"> </a>Associate a group with a product</span></span>
<span data-ttu-id="2fde0-134">tooassociate un groupe avec un produit, cliquez sur **produits** de hello **gestion des API** hello menu gauche, puis cliquez sur nom hello de produit de votre choix hello.</span><span class="sxs-lookup"><span data-stu-id="2fde0-134">tooassociate a group with a product, click **Products** from hello **API Management** menu on hello left, and then click hello name of hello desired product.</span></span>

![Set visibility][api-management-add-group-to-product]

<span data-ttu-id="2fde0-136">Sélectionnez hello **visibilité** onglet tooadd et supprimer des groupes et des groupes en cours de tooview hello pour le produit de hello.</span><span class="sxs-lookup"><span data-stu-id="2fde0-136">Select hello **Visibility** tab tooadd and remove groups, and tooview hello current groups for hello product.</span></span> <span data-ttu-id="2fde0-137">tooadd ou supprimez des groupes, vérifiez ou désactivez les cases à cocher hello pour hello souhaitée des groupes et cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="2fde0-137">tooadd or remove groups, check or uncheck hello checkboxes for hello desired groups and click **Save**.</span></span>

![Set visibility][api-management-add-group-to-product-visibility]

> [!NOTE]
> <span data-ttu-id="2fde0-139">tooadd les groupes Azure Active Directory, consultez [comment tooauthorize développeur comptes à l’aide Azure Active Directory dans la gestion des API Azure](api-management-howto-aad.md).</span><span class="sxs-lookup"><span data-stu-id="2fde0-139">tooadd Azure Active Directory groups, see [How tooauthorize developer accounts using Azure Active Directory in Azure API Management](api-management-howto-aad.md).</span></span>
> 
> <span data-ttu-id="2fde0-140">groupes tooconfigure hello **visibilité** pour un produit, cliquez sur **gérer les groupes**.</span><span class="sxs-lookup"><span data-stu-id="2fde0-140">tooconfigure groups from hello **Visibility** tab for a product, click **Manage Groups**.</span></span>
> 
> 

<span data-ttu-id="2fde0-141">Une fois qu’un produit est associé à un groupe, les développeurs de ce groupe peuvent afficher et s’abonner toohello produit.</span><span class="sxs-lookup"><span data-stu-id="2fde0-141">Once a product is associated with a group, developers in that group can view and subscribe toohello product.</span></span>

## <span data-ttu-id="2fde0-142"><a name="associate-group-developer"></a>Association des groupes aux développeurs</span><span class="sxs-lookup"><span data-stu-id="2fde0-142"><a name="associate-group-developer"> </a>Associate groups with developers</span></span>
<span data-ttu-id="2fde0-143">groupes tooassociate avec les développeurs, cliquez sur **utilisateurs** de hello **gestion des API** menu hello gauche, puis hello case à cocher en regard des développeurs de hello vous souhaitez tooassociate avec un groupe.</span><span class="sxs-lookup"><span data-stu-id="2fde0-143">tooassociate groups with developers, click **Users** from hello **API Management** menu on hello left, and then check hello box beside hello developers you wish tooassociate with a group.</span></span>

![Ajouter le développeur toogroup][api-management-add-group-to-developer]

<span data-ttu-id="2fde0-145">Une fois que hello souhaité les développeurs sont vérifiées, cliquez sur groupe hello Bonjour **ajouter tooGroup** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="2fde0-145">Once hello desired developers are checked, click hello desired group in hello **Add tooGroup** drop-down.</span></span> <span data-ttu-id="2fde0-146">Les développeurs peuvent être supprimés des groupes à l’aide de hello **supprimer du groupe** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="2fde0-146">Developers can be removed from groups by using hello **Remove from Group** drop-down.</span></span> 

![Développeurs][api-management-add-group-to-developer-saved]

<span data-ttu-id="2fde0-148">Une fois que l’association de hello est ajoutée entre le développeur de hello et groupe de hello, vous pouvez les consulter dans hello **utilisateurs** onglet.</span><span class="sxs-lookup"><span data-stu-id="2fde0-148">Once hello association is added between hello developer and hello group, you can view it in hello **Users** tab.</span></span>

## <span data-ttu-id="2fde0-149"><a name="next-steps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2fde0-149"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="2fde0-150">Une fois qu’un développeur est ajouté tooa groupe, ils peuvent afficher et s’abonner produits toohello associés à ce groupe.</span><span class="sxs-lookup"><span data-stu-id="2fde0-150">Once a developer is added tooa group, they can view and subscribe toohello products associated with that group.</span></span> <span data-ttu-id="2fde0-151">Pour plus d’informations, consultez la page [Création et publication d’un produit dans Gestion des API Azure][How create and publish a product in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="2fde0-151">For more information, see [How create and publish a product in Azure API Management][How create and publish a product in Azure API Management],</span></span>
* <span data-ttu-id="2fde0-152">En outre toocreating et gérer des groupes dans le portail de publication hello, vous pouvez créer et gérer vos groupes à l’aide des API REST de gestion des API de hello [groupe](https://msdn.microsoft.com/library/azure/dn776329.aspx) entité.</span><span class="sxs-lookup"><span data-stu-id="2fde0-152">In addition toocreating and managing groups in hello publisher portal, you can create and manage your groups using hello API Management REST API [Group](https://msdn.microsoft.com/library/azure/dn776329.aspx) entity.</span></span>

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
