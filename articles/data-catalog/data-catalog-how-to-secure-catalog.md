---
title: "aaaHow toosecure accès tooAzure Data Catalog | Documents Microsoft"
description: "Cet article explique comment toosecure data catalog et ses ressources de données."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/17/2017
ms.author: maroche
ms.openlocfilehash: d7c35fd57d8add1cdc152b75f111879288e1548f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosecure-access-toodata-catalog-and-data-assets"></a><span data-ttu-id="a3d76-103">Comment toosecure accéder aux ressources de catalogue et les données toodata</span><span class="sxs-lookup"><span data-stu-id="a3d76-103">How toosecure access toodata catalog and data assets</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a3d76-104">Cette fonctionnalité est disponible uniquement dans l’édition standard de hello d’Azure Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="a3d76-104">This feature is available only in hello standard edition of Azure Data Catalog.</span></span>

<span data-ttu-id="a3d76-105">Azure Data Catalog vous permet de toospecify qui peut accéder au catalogue de données hello et les opérations (inscrire, annoter, prendre possession) qu’ils peuvent effectuer sur les métadonnées de catalogue de hello.</span><span class="sxs-lookup"><span data-stu-id="a3d76-105">Azure Data Catalog allows you toospecify who can access hello data catalog and what operations (register, annotate, take ownership) they can perform on metadata in hello catalog.</span></span> 

## <a name="catalog-users-and-permissions"></a><span data-ttu-id="a3d76-106">Utilisateurs du catalogue et autorisations</span><span class="sxs-lookup"><span data-stu-id="a3d76-106">Catalog users and permissions</span></span>
<span data-ttu-id="a3d76-107">toogive un utilisateur ou un Bonjour groupe accéder au catalogue de données tooa et définir des autorisations :</span><span class="sxs-lookup"><span data-stu-id="a3d76-107">toogive a user or a group hello access tooa data catalog and set permissions:</span></span>

1. <span data-ttu-id="a3d76-108">Sur hello [page d’accueil de votre catalogue de données](http://www.azuredatacatalog.com), cliquez sur **paramètres** sur la barre d’outils hello.</span><span class="sxs-lookup"><span data-stu-id="a3d76-108">On hello [home page of your data catalog](http://www.azuredatacatalog.com),  click **Settings** on hello toolbar.</span></span>

    ![catalogue de données - paramètres](media/data-catalog-how-to-secure-catalog/data-catalog-settings.png)
2. <span data-ttu-id="a3d76-110">Dans la page Paramètres de hello, développez hello **utilisateurs catalogue** section.</span><span class="sxs-lookup"><span data-stu-id="a3d76-110">In hello settings page, expand hello **Catalog Users** section.</span></span>
    <span data-ttu-id="a3d76-111">![Utilisateurs du catalogue - Ajouter](media/data-catalog-how-to-secure-catalog/data-catalog-add-button.png)</span><span class="sxs-lookup"><span data-stu-id="a3d76-111">![Catalog Users - Add](media/data-catalog-how-to-secure-catalog/data-catalog-add-button.png)</span></span>
3. <span data-ttu-id="a3d76-112">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="a3d76-112">Click **Add**.</span></span>
4. <span data-ttu-id="a3d76-113">Entrez hello complet **nom d’utilisateur** ou le nom de hello **groupe de sécurité** Bonjour Azure Active Directory (AAD) associés au catalogue de hello.</span><span class="sxs-lookup"><span data-stu-id="a3d76-113">Enter hello fully qualified **user name** or name of hello **security group** in hello Azure Active Directory (AAD) associated with hello catalog.</span></span> <span data-ttu-id="a3d76-114">Utilisez une virgule (« , ») comme séparateur si vous ajoutez plusieurs utilisateurs ou groupes.</span><span class="sxs-lookup"><span data-stu-id="a3d76-114">Use comma (\`,’) as a separator if you are adding more than one user or group.</span></span>
    <span data-ttu-id="a3d76-115">![Utilisateurs du catalogue - utilisateurs ou groupes](media/data-catalog-how-to-secure-catalog/data-catalog-users-groups.png)</span><span class="sxs-lookup"><span data-stu-id="a3d76-115">![Catalog Users - users or groups](media/data-catalog-how-to-secure-catalog/data-catalog-users-groups.png)</span></span>
5. <span data-ttu-id="a3d76-116">Appuyez sur **entrée** ou **onglet** en dehors de la zone de texte hello.</span><span class="sxs-lookup"><span data-stu-id="a3d76-116">Press **ENTER** or **TAB** out of hello text box.</span></span> 
6.  <span data-ttu-id="a3d76-117">Vérifiez que toutes les autorisations (**annoter**, **inscrire**, et **Take Ownership**) sont affectés toothese utilisateurs ou des groupes par défaut.</span><span class="sxs-lookup"><span data-stu-id="a3d76-117">Confirm that all permissions (**Annotate**, **Register**, and **Take Ownership**) are assigned toothese users or groups by default.</span></span> <span data-ttu-id="a3d76-118">Autrement dit, hello utilisateur ou un groupe peut [inscrire les ressources de données]( data-catalog-how-to-register.md), [annoter les ressources de données]( data-catalog-how-to-annotate.md), et [s’approprier les ressources de données]( data-catalog-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="a3d76-118">That is, hello user or group can [register data assets]( data-catalog-how-to-register.md), [annotate data assets]( data-catalog-how-to-annotate.md), and [take ownership of data assets]( data-catalog-how-to-manage.md).</span></span> 
    <span data-ttu-id="a3d76-119">![Utilisateurs du catalogue - autorisations par défaut](media/data-catalog-how-to-secure-catalog/data-catalog-default-permissions.png)</span><span class="sxs-lookup"><span data-stu-id="a3d76-119">![Catalog Users - default permissions](media/data-catalog-how-to-secure-catalog/data-catalog-default-permissions.png)</span></span>
7.  <span data-ttu-id="a3d76-120">toogive un utilisateur ou groupe uniquement hello lire accès toohello catalogue, désactivez hello **annoter** option pour cet utilisateur ou groupe.</span><span class="sxs-lookup"><span data-stu-id="a3d76-120">toogive a user or group only hello read access toohello catalog, clear hello **annotate** option for that user or group.</span></span> <span data-ttu-id="a3d76-121">Lorsque vous procédez ainsi, hello utilisateur ou un groupe ne peut pas annoter les ressources de données dans le catalogue de hello, mais ils peuvent les afficher.</span><span class="sxs-lookup"><span data-stu-id="a3d76-121">When you do so, hello user or group cannot annotate data assets in hello catalog but they can view them.</span></span> 
8.  <span data-ttu-id="a3d76-122">toodeny un utilisateur ou un groupe de l’inscription de vos données, désactivez hello **inscrire** option pour cet utilisateur ou groupe.</span><span class="sxs-lookup"><span data-stu-id="a3d76-122">toodeny a user or group from registering data assets, clear hello **register** option for that user or group.</span></span>
9.  <span data-ttu-id="a3d76-123">toodeny un utilisateur de prendre possession d’une ressource de données, désactivez hello **prendre possession** option pour cet utilisateur ou groupe.</span><span class="sxs-lookup"><span data-stu-id="a3d76-123">toodeny a user from taking ownership of a data asset, clear hello **take ownership** option for that user or group.</span></span> 
10. <span data-ttu-id="a3d76-124">toodelete un utilisateur/groupe d’utilisateurs du catalogue, cliquez sur **x** pour un utilisateur/groupe hello bas hello de liste de hello.</span><span class="sxs-lookup"><span data-stu-id="a3d76-124">toodelete a user/group from catalog users, click **x** for hello user/group at hello bottom of hello list.</span></span> 
    <span data-ttu-id="a3d76-125">![Utilisateurs du catalogue - supprimer un utilisateur](media/data-catalog-how-to-secure-catalog/data-catalog-delete-user.png)</span><span class="sxs-lookup"><span data-stu-id="a3d76-125">![Catalog Users - delete user](media/data-catalog-how-to-secure-catalog/data-catalog-delete-user.png)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="a3d76-126">Nous vous recommandons de vous ajoutez directement des utilisateurs de toocatalog de groupes de sécurité plutôt que d’ajouter des utilisateurs et affectez des autorisations.</span><span class="sxs-lookup"><span data-stu-id="a3d76-126">We recommend that you add security groups toocatalog users rather than adding users directly and assign permissions.</span></span> <span data-ttu-id="a3d76-127">Ensuite, ajoutez les utilisateurs toohello des groupes de sécurité qui correspondent à leurs rôles et leur catalogue toohello d’accès requis.</span><span class="sxs-lookup"><span data-stu-id="a3d76-127">Then, add users toohello security groups that match their roles and their required access toohello catalog.</span></span>

## <a name="special-considerations"></a><span data-ttu-id="a3d76-128">Considérations spéciales</span><span class="sxs-lookup"><span data-stu-id="a3d76-128">Special considerations</span></span>

- <span data-ttu-id="a3d76-129">toosecurity groupes affectés aux autorisations de Hello sont additives.</span><span class="sxs-lookup"><span data-stu-id="a3d76-129">hello permissions assigned toosecurity groups are additive.</span></span> <span data-ttu-id="a3d76-130">Imaginez par exemple qu’un utilisateur appartient à deux groupes.</span><span class="sxs-lookup"><span data-stu-id="a3d76-130">Say, a user is in two groups.</span></span> <span data-ttu-id="a3d76-131">L’un des groupes a des autorisations d’annotation, tandis que l’autre n’en a pas.</span><span class="sxs-lookup"><span data-stu-id="a3d76-131">One group has annotate permissions and other group does not have annotate permissions.</span></span> <span data-ttu-id="a3d76-132">Dans ce cas de figure, l’utilisateur a des autorisations d’annotation.</span><span class="sxs-lookup"><span data-stu-id="a3d76-132">Then, user has annotate permissions.</span></span> 
- <span data-ttu-id="a3d76-133">Hello autorisations affectées explicitement hello de remplacement tooa utilisateur les autorisations affectées toogroups toowhich hello utilisateur appartient.</span><span class="sxs-lookup"><span data-stu-id="a3d76-133">hello permissions assigned explicitly tooa user override hello permissions assigned toogroups toowhich hello user belongs.</span></span> <span data-ttu-id="a3d76-134">Dans l’exemple précédent de hello, par exemple, vous avez ajouté explicitement les utilisateurs de toocatalog hello et n’affectez pas d’annoter les autorisations.</span><span class="sxs-lookup"><span data-stu-id="a3d76-134">In hello previous example, say, you explicitly added hello user toocatalog users and do not assign annotate permissions.</span></span> <span data-ttu-id="a3d76-135">utilisateur de Hello ne peut pas annoter les ressources de données même si l’utilisateur de hello est un membre d’un groupe qui possède annoter les autorisations.</span><span class="sxs-lookup"><span data-stu-id="a3d76-135">hello user cannot annotate data assets even though hello user is a member of a group that does have annotate permissions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3d76-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a3d76-136">Next steps</span></span>
- [<span data-ttu-id="a3d76-137">Prise en main d’Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="a3d76-137">Get started with Azure Data Catalog</span></span>](data-catalog-get-started.md)

