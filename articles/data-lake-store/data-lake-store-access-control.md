---
title: "aaaOverview de contrôle d’accès dans Data Lake Store | Documents Microsoft"
description: "Comprendre le fonctionnement du contrôle d’accès dans Azure Data Lake Store"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: d16f8c09-c954-40d3-afab-c86ffa8c353d
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 1cc5d578f22ef0a123a1547abebfb4795ea09139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="access-control-in-azure-data-lake-store"></a><span data-ttu-id="784cc-103">Contrôle d’accès dans Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="784cc-103">Access control in Azure Data Lake Store</span></span>

<span data-ttu-id="784cc-104">Azure Data Lake Store implémente un modèle de contrôle d’accès qui dérive de HDFS, qui dérive à son tour de modèle de contrôle d’accès POSIX hello.</span><span class="sxs-lookup"><span data-stu-id="784cc-104">Azure Data Lake Store implements an access control model that derives from HDFS, which in turn derives from hello POSIX access control model.</span></span> <span data-ttu-id="784cc-105">Cet article résume les principes fondamentaux de hello de modèle de contrôle d’accès hello pour Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="784cc-105">This article summarizes hello basics of hello access control model for Data Lake Store.</span></span> <span data-ttu-id="784cc-106">toolearn en savoir plus sur le modèle de contrôle d’accès hello HDFS, consultez [HDFS autorisations Guide](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html).</span><span class="sxs-lookup"><span data-stu-id="784cc-106">toolearn more about hello HDFS access control model, see [HDFS Permissions Guide](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html).</span></span>

## <a name="access-control-lists-on-files-and-folders"></a><span data-ttu-id="784cc-107">Listes de contrôle d’accès sur les fichiers et dossiers</span><span class="sxs-lookup"><span data-stu-id="784cc-107">Access control lists on files and folders</span></span>

<span data-ttu-id="784cc-108">Il existe deux types de listes de contrôle d’accès (ACL) : les **ACL d’accès** et les **ACL par défaut**.</span><span class="sxs-lookup"><span data-stu-id="784cc-108">There are two kinds of access control lists (ACLs), **Access ACLs** and **Default ACLs**.</span></span>

* <span data-ttu-id="784cc-109">**Accès ACL**: ces objets de tooan contrôle l’accès.</span><span class="sxs-lookup"><span data-stu-id="784cc-109">**Access ACLs**: These control access tooan object.</span></span> <span data-ttu-id="784cc-110">Les fichiers et les dossiers ont tous des ACL d’accès.</span><span class="sxs-lookup"><span data-stu-id="784cc-110">Files and folders both have Access ACLs.</span></span>

* <span data-ttu-id="784cc-111">**ACL par défaut**: un « modèle » des ACL associé à un dossier qui déterminent les listes d’accès hello ACL pour tous les éléments enfants qui sont créés sous ce dossier.</span><span class="sxs-lookup"><span data-stu-id="784cc-111">**Default ACLs**: A "template" of ACLs associated with a folder that determine hello Access ACLs for any child items that are created under that folder.</span></span> <span data-ttu-id="784cc-112">Les fichiers n’ont pas d’ACL par défaut.</span><span class="sxs-lookup"><span data-stu-id="784cc-112">Files do not have Default ACLs.</span></span>

![ACL Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-1.png)

<span data-ttu-id="784cc-114">Accès ACL et par défaut des ACL ont hello même structure.</span><span class="sxs-lookup"><span data-stu-id="784cc-114">Both Access ACLs and Default ACLs have hello same structure.</span></span>

![ACL Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-2.png)



> [!NOTE]
> <span data-ttu-id="784cc-116">Modification hello ACL par défaut d’un parent n’affecte pas hello accès ou ACL par défaut des éléments enfants qui existent déjà.</span><span class="sxs-lookup"><span data-stu-id="784cc-116">Changing hello Default ACL on a parent does not affect hello Access ACL or Default ACL of child items that already exist.</span></span>
>
>

## <a name="users-and-identities"></a><span data-ttu-id="784cc-117">Utilisateurs et identités</span><span class="sxs-lookup"><span data-stu-id="784cc-117">Users and identities</span></span>

<span data-ttu-id="784cc-118">Chaque fichier et dossier dispose d’autorisations distinctes pour ces identités :</span><span class="sxs-lookup"><span data-stu-id="784cc-118">Every file and folder has distinct permissions for these identities:</span></span>

* <span data-ttu-id="784cc-119">Hello utilisateur du fichier de hello propriétaire</span><span class="sxs-lookup"><span data-stu-id="784cc-119">hello owning user of hello file</span></span>
* <span data-ttu-id="784cc-120">groupe propriétaire de Hello</span><span class="sxs-lookup"><span data-stu-id="784cc-120">hello owning group</span></span>
* <span data-ttu-id="784cc-121">Les utilisateurs nommés</span><span class="sxs-lookup"><span data-stu-id="784cc-121">Named users</span></span>
* <span data-ttu-id="784cc-122">Les groupes nommés</span><span class="sxs-lookup"><span data-stu-id="784cc-122">Named groups</span></span>
* <span data-ttu-id="784cc-123">Tous les autres utilisateurs</span><span class="sxs-lookup"><span data-stu-id="784cc-123">All other users</span></span>

<span data-ttu-id="784cc-124">les identités des utilisateurs et groupes Hello sont les identités Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="784cc-124">hello identities of users and groups are Azure Active Directory (Azure AD) identities.</span></span> <span data-ttu-id="784cc-125">Ainsi sauf indication contraire, un « utilisateur, » dans le contexte de hello Lake du magasin de données, permettant une signifie un utilisateur Azure AD ou un groupe de sécurité Azure AD.</span><span class="sxs-lookup"><span data-stu-id="784cc-125">So unless otherwise noted, a "user," in hello context of Data Lake Store, can either mean an Azure AD user or an Azure AD security group.</span></span>

## <a name="permissions"></a><span data-ttu-id="784cc-126">Autorisations</span><span class="sxs-lookup"><span data-stu-id="784cc-126">Permissions</span></span>

<span data-ttu-id="784cc-127">Hello les autorisations sur un objet de système de fichiers sont **en lecture**, **écrire**, et **Execute**, et ils peuvent être utilisés sur les fichiers et dossiers comme indiqué dans hello tableau suivant :</span><span class="sxs-lookup"><span data-stu-id="784cc-127">hello permissions on a filesystem object are **Read**, **Write**, and **Execute**, and they can be used on files and folders as shown in hello following table:</span></span>

|            |    <span data-ttu-id="784cc-128">Fichier</span><span class="sxs-lookup"><span data-stu-id="784cc-128">File</span></span>     |   <span data-ttu-id="784cc-129">Dossier</span><span class="sxs-lookup"><span data-stu-id="784cc-129">Folder</span></span> |
|------------|-------------|----------|
| <span data-ttu-id="784cc-130">**Lecture (R)**</span><span class="sxs-lookup"><span data-stu-id="784cc-130">**Read (R)**</span></span> | <span data-ttu-id="784cc-131">Peut lire contenu hello d’un fichier</span><span class="sxs-lookup"><span data-stu-id="784cc-131">Can read hello contents of a file</span></span> | <span data-ttu-id="784cc-132">Requiert **en lecture** et **Execute** contenu de hello toolist du dossier de hello</span><span class="sxs-lookup"><span data-stu-id="784cc-132">Requires **Read** and **Execute** toolist hello contents of hello folder</span></span>|
| <span data-ttu-id="784cc-133">**Écriture (W)**</span><span class="sxs-lookup"><span data-stu-id="784cc-133">**Write (W)**</span></span> | <span data-ttu-id="784cc-134">Écrire ou ajouter le fichier de tooa</span><span class="sxs-lookup"><span data-stu-id="784cc-134">Can write or append tooa file</span></span> | <span data-ttu-id="784cc-135">Requiert **écrire** et **Execute** toocreate des éléments enfants dans un dossier</span><span class="sxs-lookup"><span data-stu-id="784cc-135">Requires **Write** and **Execute** toocreate child items in a folder</span></span> |
| <span data-ttu-id="784cc-136">**Exécution (X)**</span><span class="sxs-lookup"><span data-stu-id="784cc-136">**Execute (X)**</span></span> | <span data-ttu-id="784cc-137">Ne signifie pas que n’importe où dans le contexte de hello de Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="784cc-137">Does not mean anything in hello context of Data Lake Store</span></span> | <span data-ttu-id="784cc-138">Éléments requis tootraverse hello enfant d’un dossier</span><span class="sxs-lookup"><span data-stu-id="784cc-138">Required tootraverse hello child items of a folder</span></span> |

### <a name="short-forms-for-permissions"></a><span data-ttu-id="784cc-139">Formes abrégées des autorisations</span><span class="sxs-lookup"><span data-stu-id="784cc-139">Short forms for permissions</span></span>

<span data-ttu-id="784cc-140">**RWX** est utilisé tooindicate **lecture + écriture + exécuter**.</span><span class="sxs-lookup"><span data-stu-id="784cc-140">**RWX** is used tooindicate **Read + Write + Execute**.</span></span> <span data-ttu-id="784cc-141">Il existe une forme numérique plus condensée dans lequel **lecture = 4**, **écrire = 2**, et **Execute = 1**, somme hello qui représente les autorisations hello.</span><span class="sxs-lookup"><span data-stu-id="784cc-141">A more condensed numeric form exists in which **Read=4**, **Write=2**, and **Execute=1**, hello sum of which represents hello permissions.</span></span> <span data-ttu-id="784cc-142">Voici quelques exemples.</span><span class="sxs-lookup"><span data-stu-id="784cc-142">Following are some examples.</span></span>

| <span data-ttu-id="784cc-143">Forme numérique</span><span class="sxs-lookup"><span data-stu-id="784cc-143">Numeric form</span></span> | <span data-ttu-id="784cc-144">Forme abrégée</span><span class="sxs-lookup"><span data-stu-id="784cc-144">Short form</span></span> |      <span data-ttu-id="784cc-145">Signification</span><span class="sxs-lookup"><span data-stu-id="784cc-145">What it means</span></span>     |
|--------------|------------|------------------------|
| <span data-ttu-id="784cc-146">7</span><span class="sxs-lookup"><span data-stu-id="784cc-146">7</span></span>            | <span data-ttu-id="784cc-147">RWX</span><span class="sxs-lookup"><span data-stu-id="784cc-147">RWX</span></span>        | <span data-ttu-id="784cc-148">Lecture + Écriture + Exécution</span><span class="sxs-lookup"><span data-stu-id="784cc-148">Read + Write + Execute</span></span> |
| <span data-ttu-id="784cc-149">5</span><span class="sxs-lookup"><span data-stu-id="784cc-149">5</span></span>            | <span data-ttu-id="784cc-150">R-X</span><span class="sxs-lookup"><span data-stu-id="784cc-150">R-X</span></span>        | <span data-ttu-id="784cc-151">Lecture + Exécution</span><span class="sxs-lookup"><span data-stu-id="784cc-151">Read + Execute</span></span>         |
| <span data-ttu-id="784cc-152">4</span><span class="sxs-lookup"><span data-stu-id="784cc-152">4</span></span>            | <span data-ttu-id="784cc-153">R--</span><span class="sxs-lookup"><span data-stu-id="784cc-153">R--</span></span>        | <span data-ttu-id="784cc-154">Lire</span><span class="sxs-lookup"><span data-stu-id="784cc-154">Read</span></span>                   |
| <span data-ttu-id="784cc-155">0</span><span class="sxs-lookup"><span data-stu-id="784cc-155">0</span></span>            | ---        | <span data-ttu-id="784cc-156">| Aucune autorisation</span><span class="sxs-lookup"><span data-stu-id="784cc-156">No permissions</span></span>         |


### <a name="permissions-do-not-inherit"></a><span data-ttu-id="784cc-157">Les autorisations ne se transmettent pas en héritage</span><span class="sxs-lookup"><span data-stu-id="784cc-157">Permissions do not inherit</span></span>

<span data-ttu-id="784cc-158">Modèle de style POSIX hello qui est utilisé par Data Lake Store, autorisations pour un élément sont stockées sur élément hello proprement dit.</span><span class="sxs-lookup"><span data-stu-id="784cc-158">In hello POSIX-style model that's used by Data Lake Store, permissions for an item are stored on hello item itself.</span></span> <span data-ttu-id="784cc-159">En d’autres termes, les autorisations pour un élément ne peut pas être héritées hello des éléments de parents.</span><span class="sxs-lookup"><span data-stu-id="784cc-159">In other words, permissions for an item cannot be inherited from hello parent items.</span></span>

## <a name="common-scenarios-related-toopermissions"></a><span data-ttu-id="784cc-160">Toopermissions connexes des scénarios courants</span><span class="sxs-lookup"><span data-stu-id="784cc-160">Common scenarios related toopermissions</span></span>

<span data-ttu-id="784cc-161">Voici certaines toohelp de scénarios courants vous comprenez quelles autorisations sont nécessaires tooperform certaines opérations sur un compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="784cc-161">Following are some common scenarios toohelp you understand which permissions are needed tooperform certain operations on a Data Lake Store account.</span></span>

### <a name="permissions-needed-tooread-a-file"></a><span data-ttu-id="784cc-162">Autorisations nécessaires tooread un fichier</span><span class="sxs-lookup"><span data-stu-id="784cc-162">Permissions needed tooread a file</span></span>

![ACL Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-3.png)

* <span data-ttu-id="784cc-164">Pour hello toobe de fichier en lecture, hello appelant besoins **en lecture** autorisations.</span><span class="sxs-lookup"><span data-stu-id="784cc-164">For hello file toobe read, hello caller needs **Read** permissions.</span></span>
* <span data-ttu-id="784cc-165">Pour tous les hello dans la structure de dossiers hello des dossiers qui contiennent les fichiers hello, hello appelant besoins **Execute** autorisations.</span><span class="sxs-lookup"><span data-stu-id="784cc-165">For all hello folders in hello folder structure that contain hello file, hello caller needs **Execute** permissions.</span></span>

### <a name="permissions-needed-tooappend-tooa-file"></a><span data-ttu-id="784cc-166">Autorisations nécessaires tooappend tooa fichier</span><span class="sxs-lookup"><span data-stu-id="784cc-166">Permissions needed tooappend tooa file</span></span>

![ACL Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-4.png)

* <span data-ttu-id="784cc-168">Pour hello fichier toobe ajoutée, hello appelant besoins **écrire** autorisations.</span><span class="sxs-lookup"><span data-stu-id="784cc-168">For hello file toobe appended to, hello caller needs **Write** permissions.</span></span>
* <span data-ttu-id="784cc-169">Pour tous les hello dossiers qui contiennent les fichiers hello, hello appelant besoins **Execute** autorisations.</span><span class="sxs-lookup"><span data-stu-id="784cc-169">For all hello folders that contain hello file, hello caller needs **Execute** permissions.</span></span>

### <a name="permissions-needed-toodelete-a-file"></a><span data-ttu-id="784cc-170">Autorisations nécessaires toodelete un fichier</span><span class="sxs-lookup"><span data-stu-id="784cc-170">Permissions needed toodelete a file</span></span>

![ACL Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-5.png)

* <span data-ttu-id="784cc-172">Dossier parent de hello, hello appelant besoins **écrire + exécuter** autorisations.</span><span class="sxs-lookup"><span data-stu-id="784cc-172">For hello parent folder, hello caller needs **Write + Execute** permissions.</span></span>
* <span data-ttu-id="784cc-173">Pour tous les hello autres dossiers dans le chemin d’accès du fichier hello, hello appelant besoins **Execute** autorisations.</span><span class="sxs-lookup"><span data-stu-id="784cc-173">For all hello other folders in hello file’s path, hello caller needs **Execute** permissions.</span></span>



> [!NOTE]
> <span data-ttu-id="784cc-174">Écrire des autorisations sur le fichier de hello ne sont pas requis toodelete il tant que hello deux conditions précédentes sont remplies.</span><span class="sxs-lookup"><span data-stu-id="784cc-174">Write permissions on hello file are not required toodelete it as long as hello previous two conditions are true.</span></span>
>
>

### <a name="permissions-needed-tooenumerate-a-folder"></a><span data-ttu-id="784cc-175">Autorisations nécessaires tooenumerate un dossier</span><span class="sxs-lookup"><span data-stu-id="784cc-175">Permissions needed tooenumerate a folder</span></span>

![ACL Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-6.png)

* <span data-ttu-id="784cc-177">Pour hello dossier tooenumerate, hello appelant besoins **lecture + Execute** autorisations.</span><span class="sxs-lookup"><span data-stu-id="784cc-177">For hello folder tooenumerate, hello caller needs **Read + Execute** permissions.</span></span>
* <span data-ttu-id="784cc-178">Pour tous les hello dossiers de niveau supérieur, les besoins de l’appelant de hello **Execute** autorisations.</span><span class="sxs-lookup"><span data-stu-id="784cc-178">For all hello ancestor folders, hello caller needs **Execute** permissions.</span></span>

## <a name="viewing-permissions-in-hello-azure-portal"></a><span data-ttu-id="784cc-179">Autorisations d’affichage Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="784cc-179">Viewing permissions in hello Azure portal</span></span>

<span data-ttu-id="784cc-180">À partir de hello **Explorateur de données** Panneau de hello compte Data Lake Store, cliquez sur **accès** toosee hello ACL pour un fichier ou un dossier.</span><span class="sxs-lookup"><span data-stu-id="784cc-180">From hello **Data Explorer** blade of hello Data Lake Store account, click **Access** toosee hello ACLs for a file or a folder.</span></span> <span data-ttu-id="784cc-181">Cliquez sur **accès** toosee hello ACL pour hello **catalogue** dossier sous hello **mydatastore** compte.</span><span class="sxs-lookup"><span data-stu-id="784cc-181">Click **Access** toosee hello ACLs for hello **catalog** folder under hello **mydatastore** account.</span></span>

![ACL Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-1.png)

<span data-ttu-id="784cc-183">Dans ce panneau, section supérieure de hello montre une vue d’ensemble d’autorisations hello dont vous disposez.</span><span class="sxs-lookup"><span data-stu-id="784cc-183">On this blade, hello top section shows an overview of hello permissions that you have.</span></span> <span data-ttu-id="784cc-184">(Dans la capture d’écran de hello, hello se Bob.) Après cela, les autorisations d’accès hello sont affichées.</span><span class="sxs-lookup"><span data-stu-id="784cc-184">(In hello screenshot, hello user is Bob.) Following that, hello access permissions are shown.</span></span> <span data-ttu-id="784cc-185">Après cela, à partir de hello **accès** panneau, cliquez sur **vue Simple** toosee hello vue plus simple.</span><span class="sxs-lookup"><span data-stu-id="784cc-185">After that, from hello **Access** blade, click **Simple View** toosee hello simpler view.</span></span>

![ACL Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-simple-view.png)

<span data-ttu-id="784cc-187">Cliquez sur **vue avancée** toosee hello plus vue avancée, où les concepts hello de super utilisateur, le masque et par défaut des ACL sont affichés.</span><span class="sxs-lookup"><span data-stu-id="784cc-187">Click **Advanced View** toosee hello more advanced view, where hello concepts of Default ACLs, mask, and super-user are shown.</span></span>

![ACL Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-advance-view.png)

## <a name="hello-super-user"></a><span data-ttu-id="784cc-189">super utilisateur de Hello</span><span class="sxs-lookup"><span data-stu-id="784cc-189">hello super-user</span></span>

<span data-ttu-id="784cc-190">Un super utilisateur a hello la plupart des droits de tous les utilisateurs de hello Bonjour Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="784cc-190">A super-user has hello most rights of all hello users in hello Data Lake Store.</span></span> <span data-ttu-id="784cc-191">Un super utilisateur :</span><span class="sxs-lookup"><span data-stu-id="784cc-191">A super-user:</span></span>

* <span data-ttu-id="784cc-192">A les autorisations RWX trop**tous les** fichiers et dossiers.</span><span class="sxs-lookup"><span data-stu-id="784cc-192">Has RWX Permissions too**all** files and folders.</span></span>
* <span data-ttu-id="784cc-193">Peut modifier les autorisations de hello sur n’importe quel fichier ou un dossier.</span><span class="sxs-lookup"><span data-stu-id="784cc-193">Can change hello permissions on any file or folder.</span></span>
* <span data-ttu-id="784cc-194">Peut modifier hello utilisateur propriétaire ou le propriétaire de groupe de tout fichier ou dossier.</span><span class="sxs-lookup"><span data-stu-id="784cc-194">Can change hello owning user or owning group of any file or folder.</span></span>

<span data-ttu-id="784cc-195">Dans Azure, un compte Data Lake Store possède plusieurs rôles Azure :</span><span class="sxs-lookup"><span data-stu-id="784cc-195">In Azure, a Data Lake Store account has several Azure roles, including:</span></span>

* <span data-ttu-id="784cc-196">Propriétaires</span><span class="sxs-lookup"><span data-stu-id="784cc-196">Owners</span></span>
* <span data-ttu-id="784cc-197">Contributeurs</span><span class="sxs-lookup"><span data-stu-id="784cc-197">Contributors</span></span>
* <span data-ttu-id="784cc-198">Lecteurs</span><span class="sxs-lookup"><span data-stu-id="784cc-198">Readers</span></span>

<span data-ttu-id="784cc-199">Tout le monde Bonjour **propriétaires** rôle pour un compte Data Lake Store est automatiquement un super utilisateur pour ce compte.</span><span class="sxs-lookup"><span data-stu-id="784cc-199">Everyone in hello **Owners** role for a Data Lake Store account is automatically a super-user for that account.</span></span> <span data-ttu-id="784cc-200">toolearn, voir [contrôle d’accès basé sur le rôle](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="784cc-200">toolearn more, see [Role-based access control](../active-directory/role-based-access-control-configure.md).</span></span>
<span data-ttu-id="784cc-201">Si vous voulez toocreate un rôle personnalisé contrôle d’accès en fonction du rôle (RBAC) qui dispose des autorisations de super utilisateur, il doit hello toohave les autorisations suivantes :</span><span class="sxs-lookup"><span data-stu-id="784cc-201">If you want toocreate a custom role-based-access control (RBAC) role that has super-user permissions, it needs toohave hello following permissions:</span></span>
- <span data-ttu-id="784cc-202">Microsoft.DataLakeStore/accounts/Superuser/action</span><span class="sxs-lookup"><span data-stu-id="784cc-202">Microsoft.DataLakeStore/accounts/Superuser/action</span></span>
- <span data-ttu-id="784cc-203">Microsoft.Authorization/roleAssignments/write</span><span class="sxs-lookup"><span data-stu-id="784cc-203">Microsoft.Authorization/roleAssignments/write</span></span>


## <a name="hello-owning-user"></a><span data-ttu-id="784cc-204">utilisateur propriétaire de Hello</span><span class="sxs-lookup"><span data-stu-id="784cc-204">hello owning user</span></span>

<span data-ttu-id="784cc-205">Hello utilisateur qui a créé l’élément de hello est automatiquement hello utilisateur de l’élément de hello propriétaire.</span><span class="sxs-lookup"><span data-stu-id="784cc-205">hello user who created hello item is automatically hello owning user of hello item.</span></span> <span data-ttu-id="784cc-206">Les utilisateurs propriétaires peuvent :</span><span class="sxs-lookup"><span data-stu-id="784cc-206">An owning user can:</span></span>

* <span data-ttu-id="784cc-207">Modifier les autorisations de hello d’un fichier qui est la propriété.</span><span class="sxs-lookup"><span data-stu-id="784cc-207">Change hello permissions of a file that is owned.</span></span>
* <span data-ttu-id="784cc-208">Modifier hello propriétaire de groupe d’un fichier qui appartient, tant que l’utilisateur propriétaire de hello est également un membre du groupe cible de hello.</span><span class="sxs-lookup"><span data-stu-id="784cc-208">Change hello owning group of a file that is owned, as long as hello owning user is also a member of hello target group.</span></span>

> [!NOTE]
> <span data-ttu-id="784cc-209">Hello utilisateur propriétaire *ne peut pas* modifier hello utilisateur du fichier appartenant à un autre propriétaire.</span><span class="sxs-lookup"><span data-stu-id="784cc-209">hello owning user *cannot* change hello owning user of another owned file.</span></span> <span data-ttu-id="784cc-210">Seuls les super utilisateurs peuvent modifier hello propriétaire l’utilisateur d’un fichier ou un dossier.</span><span class="sxs-lookup"><span data-stu-id="784cc-210">Only super-users can change hello owning user of a file or folder.</span></span>
>
>

## <a name="hello-owning-group"></a><span data-ttu-id="784cc-211">groupe propriétaire de Hello</span><span class="sxs-lookup"><span data-stu-id="784cc-211">hello owning group</span></span>

<span data-ttu-id="784cc-212">Bonjour POSIX ACL, chaque utilisateur est associé à un « groupe principal ».</span><span class="sxs-lookup"><span data-stu-id="784cc-212">In hello POSIX ACLs, every user is associated with a "primary group."</span></span> <span data-ttu-id="784cc-213">Par exemple, l’utilisateur « alice » peut appartenir au groupe « finance » toohello.</span><span class="sxs-lookup"><span data-stu-id="784cc-213">For example, user "alice" might belong toohello "finance" group.</span></span> <span data-ttu-id="784cc-214">Alice peut également appartenir toomultiple groupes, mais un seul groupe est toujours désigné comme son groupe principal.</span><span class="sxs-lookup"><span data-stu-id="784cc-214">Alice might also belong toomultiple groups, but one group is always designated as her primary group.</span></span> <span data-ttu-id="784cc-215">Dans POSIX, lorsqu’Alice crée un fichier, hello propriétaire de groupe de ce fichier a la valeur tooher groupe principal, qui dans ce cas est « Finances ».</span><span class="sxs-lookup"><span data-stu-id="784cc-215">In POSIX, when Alice creates a file, hello owning group of that file is set tooher primary group, which in this case is "finance."</span></span>

<span data-ttu-id="784cc-216">Lorsqu’un nouvel élément de système de fichiers est créé, Data Lake Store assigne un toohello valeur groupe propriétaire.</span><span class="sxs-lookup"><span data-stu-id="784cc-216">When a new filesystem item is created, Data Lake Store assigns a value toohello owning group.</span></span>

* <span data-ttu-id="784cc-217">**Cas n° 1**: dossier racine de hello « / ».</span><span class="sxs-lookup"><span data-stu-id="784cc-217">**Case 1**: hello root folder "/".</span></span> <span data-ttu-id="784cc-218">Ce dossier est créé lors de la création d’un compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="784cc-218">This folder is created when a Data Lake Store account is created.</span></span> <span data-ttu-id="784cc-219">Dans ce cas, le groupe propriétaire de hello est définie utilisateur toohello qui a créé le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="784cc-219">In this case, hello owning group is set toohello user who created hello account.</span></span>
* <span data-ttu-id="784cc-220">**Cas n° 2** (tous les autres cas) : lorsqu’un nouvel élément est créé, le groupe propriétaire de hello est copié à partir du dossier parent hello.</span><span class="sxs-lookup"><span data-stu-id="784cc-220">**Case 2** (Every other case): When a new item is created, hello owning group is copied from hello parent folder.</span></span>

<span data-ttu-id="784cc-221">groupe propriétaire de Hello peut être modifié par :</span><span class="sxs-lookup"><span data-stu-id="784cc-221">hello owning group can be changed by:</span></span>
* <span data-ttu-id="784cc-222">un super utilisateur ;</span><span class="sxs-lookup"><span data-stu-id="784cc-222">Any super-users.</span></span>
* <span data-ttu-id="784cc-223">Hello propriétaire l’utilisateur, si l’utilisateur propriétaire de hello est également un membre du groupe cible de hello.</span><span class="sxs-lookup"><span data-stu-id="784cc-223">hello owning user, if hello owning user is also a member of hello target group.</span></span>

## <a name="access-check-algorithm"></a><span data-ttu-id="784cc-224">Algorithme de vérification des accès</span><span class="sxs-lookup"><span data-stu-id="784cc-224">Access check algorithm</span></span>

<span data-ttu-id="784cc-225">Hello suivant illustration représente l’algorithme de vérification d’accès hello pour les comptes Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="784cc-225">hello following illustration represents hello access check algorithm for Data Lake Store accounts.</span></span>

![Algorithme d’ACL Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-algorithm.png)


## <a name="hello-mask-and-effective-permissions"></a><span data-ttu-id="784cc-227">masque de Hello et « autorisations effectives »</span><span class="sxs-lookup"><span data-stu-id="784cc-227">hello mask and "effective permissions"</span></span>

<span data-ttu-id="784cc-228">Hello **masque** est un RWX valeur accès toolimit utilisés pour **des utilisateurs nommés**, hello **groupe propriétaire**, et **groupes nommés** lorsque vous êtes exécution d’algorithme de vérification d’accès hello.</span><span class="sxs-lookup"><span data-stu-id="784cc-228">hello **mask** is an RWX value that is used toolimit access for **named users**, hello **owning group**, and **named groups** when you're performing hello access check algorithm.</span></span> <span data-ttu-id="784cc-229">Vous trouverez ici les concepts clés de hello pour le masque de hello.</span><span class="sxs-lookup"><span data-stu-id="784cc-229">Here are hello key concepts for hello mask.</span></span>

* <span data-ttu-id="784cc-230">masque de Hello crée « autorisations effectives ».</span><span class="sxs-lookup"><span data-stu-id="784cc-230">hello mask creates "effective permissions."</span></span> <span data-ttu-id="784cc-231">Autrement dit, il modifie les autorisations de hello au moment de hello de vérification d’accès.</span><span class="sxs-lookup"><span data-stu-id="784cc-231">That is, it modifies hello permissions at hello time of access check.</span></span>
* <span data-ttu-id="784cc-232">masque de Hello peut être modifié directement par le propriétaire du fichier hello et tous les super utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="784cc-232">hello mask can be directly edited by hello file owner and any super-users.</span></span>
* <span data-ttu-id="784cc-233">masque de Hello peut supprimer l’autorisation effective d’autorisations toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="784cc-233">hello mask can remove permissions toocreate hello effective permission.</span></span> <span data-ttu-id="784cc-234">masque de Hello *ne peut pas* ajouter l’autorisation effective de toohello autorisations.</span><span class="sxs-lookup"><span data-stu-id="784cc-234">hello mask *cannot* add permissions toohello effective permission.</span></span>

<span data-ttu-id="784cc-235">Prenons quelques exemples.</span><span class="sxs-lookup"><span data-stu-id="784cc-235">Let's look at some examples.</span></span> <span data-ttu-id="784cc-236">Dans l’exemple suivant de hello, masque de hello est défini trop**RWX**, ce qui signifie que le masque hello ne supprime pas les autorisations.</span><span class="sxs-lookup"><span data-stu-id="784cc-236">In hello following example, hello mask is set too**RWX**, which means that hello mask does not remove any permissions.</span></span> <span data-ttu-id="784cc-237">les autorisations effectives Hello pour hello nommé utilisateur, le groupe propriétaire et groupe nommé ne sont pas modifiées au cours de la vérification d’accès hello.</span><span class="sxs-lookup"><span data-stu-id="784cc-237">hello effective permissions for hello named user, owning group, and named group are not altered during hello access check.</span></span>

![ACL Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-mask-1.png)

<span data-ttu-id="784cc-239">Dans l’exemple suivant de hello, masque de hello est défini trop**R-X**.</span><span class="sxs-lookup"><span data-stu-id="784cc-239">In hello following example, hello mask is set too**R-X**.</span></span> <span data-ttu-id="784cc-240">Cela signifie qu’il **désactive les autorisations d’écriture hello** pour **utilisateur nommé**, **groupe propriétaire**, et **groupe nommé** au moment de hello d’accès vérification.</span><span class="sxs-lookup"><span data-stu-id="784cc-240">This means that it **turns off hello Write permissions** for **named user**, **owning group**, and **named group** at hello time of access check.</span></span>

![ACL Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-mask-2.png)

<span data-ttu-id="784cc-242">Pour référence, voici où masque hello pour un fichier ou un dossier s’affiche dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="784cc-242">For reference, here is where hello mask for a file or folder appears in hello Azure portal.</span></span>

![ACL Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-mask-view.png)

> [!NOTE]
> <span data-ttu-id="784cc-244">Un nouveau compte Data Lake Store, hello et masque de pour hello accès ACL par défaut de la racine de hello dossier (« / ») par défaut est tooRWX.</span><span class="sxs-lookup"><span data-stu-id="784cc-244">For a new Data Lake Store account, hello mask for hello Access ACL and Default ACL of hello root folder ("/") defaults tooRWX.</span></span>
>
>

## <a name="permissions-on-new-files-and-folders"></a><span data-ttu-id="784cc-245">Autorisations sur les nouveaux fichiers et dossiers</span><span class="sxs-lookup"><span data-stu-id="784cc-245">Permissions on new files and folders</span></span>

<span data-ttu-id="784cc-246">Lorsqu’un nouveau fichier ou dossier est créé dans un dossier existant, hello ACL par défaut sur le dossier parent de hello détermine :</span><span class="sxs-lookup"><span data-stu-id="784cc-246">When a new file or folder is created under an existing folder, hello Default ACL on hello parent folder determines:</span></span>

- <span data-ttu-id="784cc-247">L’ACL par défaut et l’ACL d’accès d’un dossier enfant</span><span class="sxs-lookup"><span data-stu-id="784cc-247">A child folder’s Default ACL and Access ACL.</span></span>
- <span data-ttu-id="784cc-248">L’ACL d’accès d’un fichier enfant (les fichiers n’ont pas d’ACL par défaut)</span><span class="sxs-lookup"><span data-stu-id="784cc-248">A child file's Access ACL (files do not have a Default ACL).</span></span>

### <a name="hello-access-acl-of-a-child-file-or-folder"></a><span data-ttu-id="784cc-249">Hello d’accès d’un fichier enfant ou un dossier</span><span class="sxs-lookup"><span data-stu-id="784cc-249">hello Access ACL of a child file or folder</span></span>

<span data-ttu-id="784cc-250">Lorsqu’un fichier enfant ou un dossier est créé, ACL par défaut de hello parent est copié en tant que hello d’accès du fichier d’enfant hello ou du dossier.</span><span class="sxs-lookup"><span data-stu-id="784cc-250">When a child file or folder is created, hello parent's Default ACL is copied as hello Access ACL of hello child file or folder.</span></span> <span data-ttu-id="784cc-251">En outre, si **autres** utilisateur dispose d’autorisations de RWX dans l’ACL par défaut du parent hello, il est supprimé d’accès l’élément enfant de hello.</span><span class="sxs-lookup"><span data-stu-id="784cc-251">Also, if **other** user has RWX permissions in hello parent's default ACL, it is removed from hello child item's Access ACL.</span></span>

![ACL Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-child-items-1.png)

<span data-ttu-id="784cc-253">Dans la plupart des scénarios, les informations précédentes hello sont tous les tooknow sur la manière dont l’accès d’un élément enfant est déterminé.</span><span class="sxs-lookup"><span data-stu-id="784cc-253">In most scenarios, hello previous information is all you need tooknow about how a child item’s Access ACL is determined.</span></span> <span data-ttu-id="784cc-254">Toutefois, si vous êtes familiarisé avec les systèmes POSIX et que vous souhaitez toounderstand détaillée la réalisation de cette transformation, consultez la section de hello [rôle du Umask lors de la création de hello accès pour les nouveaux fichiers et dossiers](#umasks-role-in-creating-the-access-acl-for-new-files-and-folders) plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="784cc-254">However, if you are familiar with POSIX systems and want toounderstand in-depth how this transformation is achieved, see hello section [Umask’s role in creating hello Access ACL for new files and folders](#umasks-role-in-creating-the-access-acl-for-new-files-and-folders) later in this article.</span></span>


### <a name="a-child-folders-default-acl"></a><span data-ttu-id="784cc-255">ACL par défaut pour un dossier enfant</span><span class="sxs-lookup"><span data-stu-id="784cc-255">A child folder's Default ACL</span></span>

<span data-ttu-id="784cc-256">Création d’un dossier enfant sous un dossier parent, par défaut de liste ACL du dossier hello parent est copiée via comme l’ACL du dossier toohello enfant par défaut est.</span><span class="sxs-lookup"><span data-stu-id="784cc-256">When a child folder is created under a parent folder, hello parent folder's Default ACL is copied over as is toohello child folder's Default ACL.</span></span>

![ACL Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-child-items-2.png)

## <a name="advanced-topics-for-understanding-acls-in-data-lake-store"></a><span data-ttu-id="784cc-258">Rubriques avancées permettant de comprendre les ACL dans Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="784cc-258">Advanced topics for understanding ACLs in Data Lake Store</span></span>

<span data-ttu-id="784cc-259">Voici certains toohelp rubriques avancées que vous comprenez comment les ACL sont déterminées pour Data Lake Store fichiers ou dossiers.</span><span class="sxs-lookup"><span data-stu-id="784cc-259">Following are some advanced topics toohelp you understand how ACLs are determined for Data Lake Store files or folders.</span></span>

### <a name="umasks-role-in-creating-hello-access-acl-for-new-files-and-folders"></a><span data-ttu-id="784cc-260">Rôle du umask lors de la création de hello accès pour les nouveaux fichiers et dossiers</span><span class="sxs-lookup"><span data-stu-id="784cc-260">Umask’s role in creating hello Access ACL for new files and folders</span></span>

<span data-ttu-id="784cc-261">Dans un système compatible POSIX, concept général de hello est qu’umask est une valeur de bit 9 sur le dossier parent hello qui a utilisé l’autorisation de hello tootransform pour **utilisateur propriétaire**, **groupe propriétaire**, et  **autres** sur hello accès d’un nouveau fichier enfant ou un dossier.</span><span class="sxs-lookup"><span data-stu-id="784cc-261">In a POSIX-compliant system, hello general concept is that umask is a 9-bit value on hello parent folder that's used tootransform hello permission for **owning user**, **owning group**, and **other** on hello Access ACL of a new child file or folder.</span></span> <span data-ttu-id="784cc-262">bits Hello d’un umask identifient quels tooturn bits hors tension dans accès l’élément enfant de hello.</span><span class="sxs-lookup"><span data-stu-id="784cc-262">hello bits of a umask identify which bits tooturn off in hello child item’s Access ACL.</span></span> <span data-ttu-id="784cc-263">Par conséquent, il est utilisé tooselectively empêcher la propagation des autorisations pour hello **utilisateur propriétaire**, **groupe propriétaire**, et **autres**.</span><span class="sxs-lookup"><span data-stu-id="784cc-263">Thus it is used tooselectively prevent hello propagation of permissions for **owning user**, **owning group**, and **other**.</span></span>

<span data-ttu-id="784cc-264">Dans un système HDFS, hello umask est généralement une option de configuration au niveau du site qui est contrôlée par les administrateurs.</span><span class="sxs-lookup"><span data-stu-id="784cc-264">In an HDFS system, hello umask is typically a sitewide configuration option that is controlled by administrators.</span></span> <span data-ttu-id="784cc-265">Data Lake Store utilise un **umask à l’échelle du compte** qui ne peut pas être modifié.</span><span class="sxs-lookup"><span data-stu-id="784cc-265">Data Lake Store uses an **account-wide umask** that cannot be changed.</span></span> <span data-ttu-id="784cc-266">Hello suivant table affiche hello Démasquez à Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="784cc-266">hello following table shows hello unmask for Data Lake Store.</span></span>

| <span data-ttu-id="784cc-267">Groupe d'utilisateurs</span><span class="sxs-lookup"><span data-stu-id="784cc-267">User group</span></span>  | <span data-ttu-id="784cc-268">Paramètre</span><span class="sxs-lookup"><span data-stu-id="784cc-268">Setting</span></span> | <span data-ttu-id="784cc-269">Effet sur l’ACL d’accès du nouvel élément enfant</span><span class="sxs-lookup"><span data-stu-id="784cc-269">Effect on new child item's Access ACL</span></span> |
|------------ |---------|---------------------------------------|
| <span data-ttu-id="784cc-270">utilisateur propriétaire</span><span class="sxs-lookup"><span data-stu-id="784cc-270">Owning user</span></span> | ---     | <span data-ttu-id="784cc-271">Aucun effet</span><span class="sxs-lookup"><span data-stu-id="784cc-271">No effect</span></span>                             |
| <span data-ttu-id="784cc-272">groupe propriétaire</span><span class="sxs-lookup"><span data-stu-id="784cc-272">Owning group</span></span>| ---     | <span data-ttu-id="784cc-273">Aucun effet</span><span class="sxs-lookup"><span data-stu-id="784cc-273">No effect</span></span>                             |
| <span data-ttu-id="784cc-274">autre</span><span class="sxs-lookup"><span data-stu-id="784cc-274">Other</span></span>       | <span data-ttu-id="784cc-275">RWX</span><span class="sxs-lookup"><span data-stu-id="784cc-275">RWX</span></span>     | <span data-ttu-id="784cc-276">Supprimer les autorisations Lecture + Écriture + Exécution</span><span class="sxs-lookup"><span data-stu-id="784cc-276">Remove Read + Write + Execute</span></span>         |

<span data-ttu-id="784cc-277">Hello après l’illustration montre cette umask en action.</span><span class="sxs-lookup"><span data-stu-id="784cc-277">hello following illustration shows this umask in action.</span></span> <span data-ttu-id="784cc-278">effet net de Hello est tooremove **lecture + écriture + exécuter** pour **autres** utilisateur.</span><span class="sxs-lookup"><span data-stu-id="784cc-278">hello net effect is tooremove **Read + Write + Execute** for **other** user.</span></span> <span data-ttu-id="784cc-279">Étant donné que hello umask n’a pas spécifié de bits pour **utilisateur propriétaire** et **groupe propriétaire**, ces autorisations ne sont pas transformées.</span><span class="sxs-lookup"><span data-stu-id="784cc-279">Because hello umask did not specify bits for **owning user** and **owning group**, those permissions are not transformed.</span></span>

![ACL Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-umask.png)

### <a name="hello-sticky-bit"></a><span data-ttu-id="784cc-281">bit de pense-bête Hello</span><span class="sxs-lookup"><span data-stu-id="784cc-281">hello sticky bit</span></span>

<span data-ttu-id="784cc-282">bit de pense-bête Hello est une fonctionnalité plus avancée d’un système de fichiers POSIX.</span><span class="sxs-lookup"><span data-stu-id="784cc-282">hello sticky bit is a more advanced feature of a POSIX filesystem.</span></span> <span data-ttu-id="784cc-283">Dans le contexte de hello Lake du magasin de données, il est peu probable que le bit rémanentes hello est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="784cc-283">In hello context of Data Lake Store, it is unlikely that hello sticky bit will be needed.</span></span>

<span data-ttu-id="784cc-284">Hello tableau suivant présente le fonctionnement des bits de pense-bête hello dans Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="784cc-284">hello following table shows how hello sticky bit works in Data Lake Store.</span></span>

| <span data-ttu-id="784cc-285">Groupe d'utilisateurs</span><span class="sxs-lookup"><span data-stu-id="784cc-285">User group</span></span>         | <span data-ttu-id="784cc-286">Fichier</span><span class="sxs-lookup"><span data-stu-id="784cc-286">File</span></span>    | <span data-ttu-id="784cc-287">Dossier</span><span class="sxs-lookup"><span data-stu-id="784cc-287">Folder</span></span> |
|--------------------|---------|-------------------------|
| <span data-ttu-id="784cc-288">Sticky bit **DÉSACTIVÉ**</span><span class="sxs-lookup"><span data-stu-id="784cc-288">Sticky bit **OFF**</span></span> | <span data-ttu-id="784cc-289">Aucun effet</span><span class="sxs-lookup"><span data-stu-id="784cc-289">No effect</span></span>   | <span data-ttu-id="784cc-290">Aucun effet</span><span class="sxs-lookup"><span data-stu-id="784cc-290">No effect.</span></span>           |
| <span data-ttu-id="784cc-291">Sticky bit **ACTIVÉ**</span><span class="sxs-lookup"><span data-stu-id="784cc-291">Sticky bit **ON**</span></span>  | <span data-ttu-id="784cc-292">Aucun effet</span><span class="sxs-lookup"><span data-stu-id="784cc-292">No effect</span></span>   | <span data-ttu-id="784cc-293">Empêche une personne d’autre que **super utilisateurs** et hello **utilisateur propriétaire** d’un élément enfant à partir de la supprimer ou renommer cet élément enfant.</span><span class="sxs-lookup"><span data-stu-id="784cc-293">Prevents anyone except **super-users** and hello **owning user** of a child item from deleting or renaming that child item.</span></span>               |

<span data-ttu-id="784cc-294">bit de pense-bête Hello n’est pas affiché dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="784cc-294">hello sticky bit is not shown in hello Azure portal.</span></span>

## <a name="common-questions-about-acls-in-data-lake-store"></a><span data-ttu-id="784cc-295">Questions les plus fréquentes sur les ACL dans Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="784cc-295">Common questions about ACLs in Data Lake Store</span></span>

<span data-ttu-id="784cc-296">Voici quelques questions fréquentes concernant les ACL dans Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="784cc-296">Here are some questions that come up often about ACLs in Data Lake Store.</span></span>

### <a name="do-i-have-tooenable-support-for-acls"></a><span data-ttu-id="784cc-297">Prise en charge de tooenable des ACL ai-je besoin ?</span><span class="sxs-lookup"><span data-stu-id="784cc-297">Do I have tooenable support for ACLs?</span></span>

<span data-ttu-id="784cc-298">Non.</span><span class="sxs-lookup"><span data-stu-id="784cc-298">No.</span></span> <span data-ttu-id="784cc-299">Le contrôle d’accès via les ACL est toujours activé pour les comptes Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="784cc-299">Access control via ACLs is always on for a Data Lake Store account.</span></span>

### <a name="which-permissions-are-required-toorecursively-delete-a-folder-and-its-contents"></a><span data-ttu-id="784cc-300">Les autorisations qui sont requis toorecursively les supprimer un dossier et son contenu ?</span><span class="sxs-lookup"><span data-stu-id="784cc-300">Which permissions are required toorecursively delete a folder and its contents?</span></span>

* <span data-ttu-id="784cc-301">le dossier parent Hello doit avoir **écrire + exécuter** autorisations.</span><span class="sxs-lookup"><span data-stu-id="784cc-301">hello parent folder must have **Write + Execute** permissions.</span></span>
* <span data-ttu-id="784cc-302">Hello toobe dossier supprimé et tous les dossiers qu’il contient, nécessite **lecture + écriture + exécuter** autorisations.</span><span class="sxs-lookup"><span data-stu-id="784cc-302">hello folder toobe deleted, and every folder within it, requires **Read + Write + Execute** permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="784cc-303">Il est inutile d’autorisations d’écriture toodelete fichiers dans des dossiers.</span><span class="sxs-lookup"><span data-stu-id="784cc-303">You do not need Write permissions toodelete files in folders.</span></span> <span data-ttu-id="784cc-304">En outre, hello du dossier racine « / » peut **jamais** être supprimé.</span><span class="sxs-lookup"><span data-stu-id="784cc-304">Also, hello root folder "/" can **never** be deleted.</span></span>
>
>

### <a name="who-is-hello-owner-of-a-file-or-folder"></a><span data-ttu-id="784cc-305">Qui est propriétaire de hello d’un fichier ou un dossier ?</span><span class="sxs-lookup"><span data-stu-id="784cc-305">Who is hello owner of a file or folder?</span></span>

<span data-ttu-id="784cc-306">créateur de Hello d’un fichier ou dossier devient propriétaire de hello.</span><span class="sxs-lookup"><span data-stu-id="784cc-306">hello creator of a file or folder becomes hello owner.</span></span>

### <a name="which-group-is-set-as-hello-owning-group-of-a-file-or-folder-at-creation"></a><span data-ttu-id="784cc-307">Le groupe est défini comme propriétaire de groupe d’un fichier ou dossier lors de la création de hello ?</span><span class="sxs-lookup"><span data-stu-id="784cc-307">Which group is set as hello owning group of a file or folder at creation?</span></span>

<span data-ttu-id="784cc-308">groupe propriétaire de Hello est copié à partir de hello propriétaire de groupe du dossier parent de hello sous le hello nouveau fichier ou dossier est créé.</span><span class="sxs-lookup"><span data-stu-id="784cc-308">hello owning group is copied from hello owning group of hello parent folder under which hello new file or folder is created.</span></span>

### <a name="i-am-hello-owning-user-of-a-file-but-i-dont-have-hello-rwx-permissions-i-need-what-do-i-do"></a><span data-ttu-id="784cc-309">Je suis hello propriétaire de l’utilisateur d’un fichier, mais je n’ai pas les autorisations de RWX hello qu'ai-je besoin.</span><span class="sxs-lookup"><span data-stu-id="784cc-309">I am hello owning user of a file but I don’t have hello RWX permissions I need.</span></span> <span data-ttu-id="784cc-310">Que faire ?</span><span class="sxs-lookup"><span data-stu-id="784cc-310">What do I do?</span></span>

<span data-ttu-id="784cc-311">Hello propriétaire utilisateur peut modifier les autorisations hello de hello fichier toogive eux-mêmes des autorisations RWX que dont ils ont besoin.</span><span class="sxs-lookup"><span data-stu-id="784cc-311">hello owning user can change hello permissions of hello file toogive themselves any RWX permissions they need.</span></span>

### <a name="when-i-look-at-acls-in-hello-azure-portal-i-see-user-names-but-through-apis-i-see-guids-why-is-that"></a><span data-ttu-id="784cc-312">Lorsque j’examine les ACL Bonjour Azure portal je vois des noms d’utilisateur mais via des API, je vois GUID, pourquoi est-ce ?</span><span class="sxs-lookup"><span data-stu-id="784cc-312">When I look at ACLs in hello Azure portal I see user names but through APIs, I see GUIDs, why is that?</span></span>

<span data-ttu-id="784cc-313">Entrées dans les listes ACL de hello sont stockées sous forme de GUID qui correspondent toousers dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="784cc-313">Entries in hello ACLs are stored as GUIDs that correspond toousers in Azure AD.</span></span> <span data-ttu-id="784cc-314">Hello API retournent hello GUID en l’état.</span><span class="sxs-lookup"><span data-stu-id="784cc-314">hello APIs return hello GUIDs as is.</span></span> <span data-ttu-id="784cc-315">Hello portail Azure tente toouse plus facile de toomake ACL par traduction hello GUID en noms conviviaux lorsque cela est possible.</span><span class="sxs-lookup"><span data-stu-id="784cc-315">hello Azure portal tries toomake ACLs easier toouse by translating hello GUIDs into friendly names when possible.</span></span>

### <a name="why-do-i-sometimes-see-guids-in-hello-acls-when-im-using-hello-azure-portal"></a><span data-ttu-id="784cc-316">Parfois, pourquoi GUID dans les listes ACL de hello lorsque j’utilise hello portail Azure ?</span><span class="sxs-lookup"><span data-stu-id="784cc-316">Why do I sometimes see GUIDs in hello ACLs when I'm using hello Azure portal?</span></span>

<span data-ttu-id="784cc-317">Un GUID est affiché lorsque l’utilisateur de hello n’existe pas dans Azure AD plus.</span><span class="sxs-lookup"><span data-stu-id="784cc-317">A GUID is shown when hello user doesn't exist in Azure AD anymore.</span></span> <span data-ttu-id="784cc-318">Cela se produit généralement lorsque l’utilisateur de hello a quitté l’entreprise de hello ou si son compte a été supprimé dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="784cc-318">Usually this happens when hello user has left hello company or if their account has been deleted in Azure AD.</span></span>

### <a name="does-data-lake-store-support-inheritance-of-acls"></a><span data-ttu-id="784cc-319">Data Lake Store prend-il en charge l’héritage des ACL ?</span><span class="sxs-lookup"><span data-stu-id="784cc-319">Does Data Lake Store support inheritance of ACLs?</span></span>

<span data-ttu-id="784cc-320">Non.</span><span class="sxs-lookup"><span data-stu-id="784cc-320">No.</span></span>

### <a name="what-is-hello-difference-between-mask-and-umask"></a><span data-ttu-id="784cc-321">Qu’est hello différencie masque umask ?</span><span class="sxs-lookup"><span data-stu-id="784cc-321">What is hello difference between mask and umask?</span></span>

| <span data-ttu-id="784cc-322">masque</span><span class="sxs-lookup"><span data-stu-id="784cc-322">mask</span></span> | <span data-ttu-id="784cc-323">umask</span><span class="sxs-lookup"><span data-stu-id="784cc-323">umask</span></span>|
|------|------|
| <span data-ttu-id="784cc-324">Hello **masque** propriété n’est disponible sur chaque fichier et dossier.</span><span class="sxs-lookup"><span data-stu-id="784cc-324">hello **mask** property is available on every file and folder.</span></span> | <span data-ttu-id="784cc-325">Hello **umask** est une propriété de hello compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="784cc-325">hello **umask** is a property of hello Data Lake Store account.</span></span> <span data-ttu-id="784cc-326">Il est donc uniquement un seul umask Bonjour Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="784cc-326">So there is only a single umask in hello Data Lake Store.</span></span>    |
| <span data-ttu-id="784cc-327">propriété du masque Hello sur un fichier ou un dossier peut être modifiée par hello propriétaire l’utilisateur ou le groupe d’un fichier ou un super utilisateur propriétaire.</span><span class="sxs-lookup"><span data-stu-id="784cc-327">hello mask property on a file or folder can be altered by hello owning user or owning group of a file or a super-user.</span></span> | <span data-ttu-id="784cc-328">propriété umask de Hello ne peut pas être modifiée par n’importe quel utilisateur, même un super utilisateur.</span><span class="sxs-lookup"><span data-stu-id="784cc-328">hello umask property cannot be modified by any user, even a super-user.</span></span> <span data-ttu-id="784cc-329">Il s’agit d’une valeur constante non modifiable.</span><span class="sxs-lookup"><span data-stu-id="784cc-329">It is an unchangeable, constant value.</span></span>|
| <span data-ttu-id="784cc-330">propriété du masque Hello est utilisée au cours de l’algorithme de vérification d’accès hello au runtime toodetermine si l’utilisateur dispose de tooperform de droite hello des opérations sur un fichier ou dossier.</span><span class="sxs-lookup"><span data-stu-id="784cc-330">hello mask property is used during hello access check algorithm at runtime toodetermine whether a user has hello right tooperform on operation on a file or folder.</span></span> <span data-ttu-id="784cc-331">rôle Hello du masque de hello est toocreate « autorisations effectives » au moment de hello de vérification d’accès.</span><span class="sxs-lookup"><span data-stu-id="784cc-331">hello role of hello mask is toocreate "effective permissions" at hello time of access check.</span></span> | <span data-ttu-id="784cc-332">Hello umask n’est pas utilisé lors de la vérification d’accès du tout.</span><span class="sxs-lookup"><span data-stu-id="784cc-332">hello umask is not used during access check at all.</span></span> <span data-ttu-id="784cc-333">Hello umask est utilisé toodetermine hello accès ACL de nouveaux éléments enfants d’un dossier.</span><span class="sxs-lookup"><span data-stu-id="784cc-333">hello umask is used toodetermine hello Access ACL of new child items of a folder.</span></span> |
| <span data-ttu-id="784cc-334">masque de Hello est une valeur RWX de 3 bits qui s’applique utilisateur propriétaire, groupe nommé et toonamed utilisateur au moment de hello de vérification d’accès.</span><span class="sxs-lookup"><span data-stu-id="784cc-334">hello mask is a 3-bit RWX value that applies toonamed user, named group, and owning user at hello time of access check.</span></span>| <span data-ttu-id="784cc-335">umask Hello est une valeur de 9 bits qui s’applique toohello utilisateur, groupe, propriétaire propriétaire et **autres** d’un nouvel enfant.</span><span class="sxs-lookup"><span data-stu-id="784cc-335">hello umask is a 9-bit value that applies toohello owning user, owning group, and **other** of a new child.</span></span>|

### <a name="where-can-i-learn-more-about-posix-access-control-model"></a><span data-ttu-id="784cc-336">Comment en savoir plus sur le modèle de contrôle d’accès POSIX ?</span><span class="sxs-lookup"><span data-stu-id="784cc-336">Where can I learn more about POSIX access control model?</span></span>

* [<span data-ttu-id="784cc-337">Listes de contrôle d’accès (ACL) POSIX sur Linux</span><span class="sxs-lookup"><span data-stu-id="784cc-337">POSIX Access Control Lists on Linux</span></span>](http://www.vanemery.com/Linux/ACL/POSIX_ACL_on_Linux.html)

* [<span data-ttu-id="784cc-338">HDFS Permission Guide (Guide des autorisations HDFS)</span><span class="sxs-lookup"><span data-stu-id="784cc-338">HDFS permission guide</span></span>](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html)

* [<span data-ttu-id="784cc-339">Forum aux questions POSIX</span><span class="sxs-lookup"><span data-stu-id="784cc-339">POSIX FAQ</span></span>](http://www.opengroup.org/austin/papers/posix_faq.html)

* [<span data-ttu-id="784cc-340">POSIX 1003.1 2008</span><span class="sxs-lookup"><span data-stu-id="784cc-340">POSIX 1003.1 2008</span></span>](http://standards.ieee.org/findstds/standard/1003.1-2008.html)

* [<span data-ttu-id="784cc-341">POSIX 1003.1 2013</span><span class="sxs-lookup"><span data-stu-id="784cc-341">POSIX 1003.1 2013</span></span>](http://pubs.opengroup.org/onlinepubs/9699919799.2013edition/)

* [<span data-ttu-id="784cc-342">POSIX 1003.1 2016</span><span class="sxs-lookup"><span data-stu-id="784cc-342">POSIX 1003.1 2016</span></span>](http://pubs.opengroup.org/onlinepubs/9699919799.2016edition/)

* [<span data-ttu-id="784cc-343">ACL POSIX sous Ubuntu</span><span class="sxs-lookup"><span data-stu-id="784cc-343">POSIX ACL on Ubuntu</span></span>](https://help.ubuntu.com/community/FilePermissionsACLs)

* [<span data-ttu-id="784cc-344">ACL using access control lists on Linux (ACL utilisant des listes de contrôle d’accès sous Linux)</span><span class="sxs-lookup"><span data-stu-id="784cc-344">ACL using access control lists on Linux</span></span>](http://bencane.com/2012/05/27/acl-using-access-control-lists-on-linux/)

## <a name="see-also"></a><span data-ttu-id="784cc-345">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="784cc-345">See also</span></span>

* [<span data-ttu-id="784cc-346">Présentation d’Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="784cc-346">Overview of Azure Data Lake Store</span></span>](data-lake-store-overview.md)
