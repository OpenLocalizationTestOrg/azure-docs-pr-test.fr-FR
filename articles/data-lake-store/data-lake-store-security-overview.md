---
title: "aaaOverview de la sécurité dans Data Lake Store | Documents Microsoft"
description: "Comprendre en quoi Azure Data Lake Store est un magasin de Big Data plus sécurisé"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ebd5b2ac-c5cc-46d4-9cfd-1a1ee70024c2
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 69e20bd046a9427202074baf59bff13f5b6a83ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="security-in-azure-data-lake-store"></a><span data-ttu-id="ce055-103">Sécurité dans Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ce055-103">Security in Azure Data Lake Store</span></span>
<span data-ttu-id="ce055-104">De nombreuses entreprises Tirez profit de l’analytique des données volumineuses pour business toohelp d’insights que les rendre actives décisions.</span><span class="sxs-lookup"><span data-stu-id="ce055-104">Many enterprises are taking advantage of big data analytics for business insights toohelp them make smart decisions.</span></span> <span data-ttu-id="ce055-105">Une organisation peut évoluer dans un environnement complexe et réglementé, avec un nombre croissant d’utilisateurs divers.</span><span class="sxs-lookup"><span data-stu-id="ce055-105">An organization might have a complex and regulated environment, with an increasing number of diverse users.</span></span> <span data-ttu-id="ce055-106">Il est essentiel pour une entreprise toomake assurer que les données critiques sont stockées en toute sécurité, avec le niveau approprié de hello d’accès accordé aux utilisateurs de tooindividual.</span><span class="sxs-lookup"><span data-stu-id="ce055-106">It is vital for an enterprise toomake sure that critical business data is stored more securely, with hello correct level of access granted tooindividual users.</span></span> <span data-ttu-id="ce055-107">Azure Data Lake Store est conçu toohelp respecter ces exigences de sécurité.</span><span class="sxs-lookup"><span data-stu-id="ce055-107">Azure Data Lake Store is designed toohelp meet these security requirements.</span></span> <span data-ttu-id="ce055-108">Dans cet article, Découvrez les fonctionnalités de sécurité hello Lake du magasin de données, y compris :</span><span class="sxs-lookup"><span data-stu-id="ce055-108">In this article, learn about hello security capabilities of Data Lake Store, including:</span></span>

* <span data-ttu-id="ce055-109">Authentification</span><span class="sxs-lookup"><span data-stu-id="ce055-109">Authentication</span></span>
* <span data-ttu-id="ce055-110">Autorisation</span><span class="sxs-lookup"><span data-stu-id="ce055-110">Authorization</span></span>
* <span data-ttu-id="ce055-111">Isolement réseau</span><span class="sxs-lookup"><span data-stu-id="ce055-111">Network isolation</span></span>
* <span data-ttu-id="ce055-112">Protection des données</span><span class="sxs-lookup"><span data-stu-id="ce055-112">Data protection</span></span>
* <span data-ttu-id="ce055-113">Audit</span><span class="sxs-lookup"><span data-stu-id="ce055-113">Auditing</span></span>

## <a name="authentication-and-identity-management"></a><span data-ttu-id="ce055-114">Authentification et gestion des identités</span><span class="sxs-lookup"><span data-stu-id="ce055-114">Authentication and identity management</span></span>
<span data-ttu-id="ce055-115">L’authentification consiste à hello par lequel l’identité d’un utilisateur est vérifiée lorsque l’utilisateur de hello interagit avec Data Lake Store ou tout service qui se connecte tooData Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ce055-115">Authentication is hello process by which a user's identity is verified when hello user interacts with Data Lake Store or with any service that connects tooData Lake Store.</span></span> <span data-ttu-id="ce055-116">Pour l’authentification et de gestion des identités, Data Lake Store utilise [Azure Active Directory](../active-directory/active-directory-whatis.md), une identité et accès management solution cloud complète qui simplifie la gestion des utilisateurs et groupes hello.</span><span class="sxs-lookup"><span data-stu-id="ce055-116">For identity management and authentication, Data Lake Store uses [Azure Active Directory](../active-directory/active-directory-whatis.md), a comprehensive identity and access management cloud solution that simplifies hello management of users and groups.</span></span>

<span data-ttu-id="ce055-117">Chaque abonnement Azure peut être associé à une instance d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ce055-117">Each Azure subscription can be associated with an instance of Azure Active Directory.</span></span> <span data-ttu-id="ce055-118">Seuls les utilisateurs et les identités de service qui sont définies dans votre service Azure Active Directory peuvent accéder à votre compte Data Lake Store, à l’aide de hello portail Azure, les outils de ligne de commande, ou via des applications client que génère de votre organisation à l’aide de hello Azure Data Kit de développement logiciel Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ce055-118">Only users and service identities that are defined in your Azure Active Directory service can access your Data Lake Store account, by using hello Azure portal, command-line tools, or through client applications your organization builds by using hello Azure Data Lake Store SDK.</span></span> <span data-ttu-id="ce055-119">Les principaux avantages de l’utilisation d’Azure Active Directory en tant que mécanisme de contrôle d’accès centralisé sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="ce055-119">Key advantages of using Azure Active Directory as a centralized access control mechanism are:</span></span>

* <span data-ttu-id="ce055-120">Gestion du cycle de vie des identités simplifiée.</span><span class="sxs-lookup"><span data-stu-id="ce055-120">Simplified identity lifecycle management.</span></span> <span data-ttu-id="ce055-121">identité Hello d’un utilisateur ou un service (une identité principale du service) peut être rapidement créée et rapidement révoquée par simplement la suppression ou la désactivation du compte hello dans le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="ce055-121">hello identity of a user or a service (a service principal identity) can be quickly created and quickly revoked by simply deleting or disabling hello account in hello directory.</span></span>
* <span data-ttu-id="ce055-122">Authentification multifacteur</span><span class="sxs-lookup"><span data-stu-id="ce055-122">Multi-factor authentication.</span></span> <span data-ttu-id="ce055-123">[L’authentification multifacteur](../multi-factor-authentication/multi-factor-authentication.md) fournit une couche supplémentaire de sécurité pour les connexions et les transactions utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ce055-123">[Multi-factor authentication](../multi-factor-authentication/multi-factor-authentication.md) provides an additional layer of security for user sign-ins and transactions.</span></span>
* <span data-ttu-id="ce055-124">Authentification à partir de n’importe quel client via un protocole ouvert standard, tel qu’OAuth ou OpenID.</span><span class="sxs-lookup"><span data-stu-id="ce055-124">Authentication from any client through a standard open protocol, such as OAuth or OpenID.</span></span>
* <span data-ttu-id="ce055-125">Fédération avec les services de répertoire d’entreprise et les fournisseurs d’identité cloud.</span><span class="sxs-lookup"><span data-stu-id="ce055-125">Federation with enterprise directory services and cloud identity providers.</span></span>

## <a name="authorization-and-access-control"></a><span data-ttu-id="ce055-126">Autorisation et contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="ce055-126">Authorization and access control</span></span>
<span data-ttu-id="ce055-127">Une fois Azure Active Directory authentifie un utilisateur afin que hello utilisateur peut accéder à Azure Data Lake Store, contrôles d’autorisation d’accès nécessaires pour Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ce055-127">After Azure Active Directory authenticates a user so that hello user can access Azure Data Lake Store, authorization controls access permissions for Data Lake Store.</span></span> <span data-ttu-id="ce055-128">Data Lake Store sépare d’autorisation pour les activités relatives aux comptes et liées aux données Bonjour suivant de manière :</span><span class="sxs-lookup"><span data-stu-id="ce055-128">Data Lake Store separates authorization for account-related and data-related activities in hello following manner:</span></span>

* <span data-ttu-id="ce055-129">[Le contrôle d’accès en fonction du rôle](../active-directory/role-based-access-control-what-is.md) (RBAC) fournit par Azure pour la gestion des comptes ;</span><span class="sxs-lookup"><span data-stu-id="ce055-129">[Role-based access control](../active-directory/role-based-access-control-what-is.md) (RBAC) provided by Azure for account management</span></span>
* <span data-ttu-id="ce055-130">POSIX ACL pour l’accès aux données dans le magasin de hello</span><span class="sxs-lookup"><span data-stu-id="ce055-130">POSIX ACL for accessing data in hello store</span></span>

### <a name="rbac-for-account-management"></a><span data-ttu-id="ce055-131">RBAC pour la gestion des comptes</span><span class="sxs-lookup"><span data-stu-id="ce055-131">RBAC for account management</span></span>
<span data-ttu-id="ce055-132">Par défaut, quatre rôles de base sont définis pour Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ce055-132">Four basic roles are defined for Data Lake Store by default.</span></span> <span data-ttu-id="ce055-133">les rôles Hello autorisent différentes opérations sur un compte Data Lake Store via hello portail Azure, les applets de commande PowerShell et les API REST.</span><span class="sxs-lookup"><span data-stu-id="ce055-133">hello roles permit different operations on a Data Lake Store account via hello Azure portal, PowerShell cmdlets, and REST APIs.</span></span> <span data-ttu-id="ce055-134">Hello propriétaire et les rôles de collaborateur peuvent effectuer diverses fonctions d’administration sur le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="ce055-134">hello Owner and Contributor roles can perform a variety of administration functions on hello account.</span></span> <span data-ttu-id="ce055-135">Vous pouvez affecter toousers de rôle de lecteur hello qui peuvent interagir uniquement avec les données.</span><span class="sxs-lookup"><span data-stu-id="ce055-135">You can assign hello Reader role toousers who only interact with data.</span></span>

<span data-ttu-id="ce055-136">![Rôles RBAC](./media/data-lake-store-security-overview/rbac-roles.png "Rôles RBAC")</span><span class="sxs-lookup"><span data-stu-id="ce055-136">![RBAC roles](./media/data-lake-store-security-overview/rbac-roles.png "RBAC roles")</span></span>

<span data-ttu-id="ce055-137">Notez que, bien que les rôles sont attribués pour la gestion de compte, certains rôles affectent toodata d’accès.</span><span class="sxs-lookup"><span data-stu-id="ce055-137">Note that although roles are assigned for account management, some roles affect access toodata.</span></span> <span data-ttu-id="ce055-138">Vous devez toouse ACL toocontrol accès toooperations qu’un utilisateur peut effectuer sur le système de fichiers hello.</span><span class="sxs-lookup"><span data-stu-id="ce055-138">You need toouse ACLs toocontrol access toooperations that a user can perform on hello file system.</span></span> <span data-ttu-id="ce055-139">Hello tableau suivant montre un résumé des droits et de gestion des droits d’accès pour hello rôles par défaut.</span><span class="sxs-lookup"><span data-stu-id="ce055-139">hello following table shows a summary of management rights and data access rights for hello default roles.</span></span>

| <span data-ttu-id="ce055-140">contrôleur</span><span class="sxs-lookup"><span data-stu-id="ce055-140">Roles</span></span> | <span data-ttu-id="ce055-141">Droits de gestion</span><span class="sxs-lookup"><span data-stu-id="ce055-141">Management rights</span></span> | <span data-ttu-id="ce055-142">Droits d’accès aux données</span><span class="sxs-lookup"><span data-stu-id="ce055-142">Data access rights</span></span> | <span data-ttu-id="ce055-143">Explication</span><span class="sxs-lookup"><span data-stu-id="ce055-143">Explanation</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ce055-144">Aucun rôle affecté</span><span class="sxs-lookup"><span data-stu-id="ce055-144">No role assigned</span></span> |<span data-ttu-id="ce055-145">Aucun</span><span class="sxs-lookup"><span data-stu-id="ce055-145">None</span></span> |<span data-ttu-id="ce055-146">Régi par ACL</span><span class="sxs-lookup"><span data-stu-id="ce055-146">Governed by ACL</span></span> |<span data-ttu-id="ce055-147">utilisateur de Hello ne peut pas utiliser hello Azure portal ou Azure PowerShell cmdlets toobrowse Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ce055-147">hello user cannot use hello Azure portal or Azure PowerShell cmdlets toobrowse Data Lake Store.</span></span> <span data-ttu-id="ce055-148">utilisateur de Hello peut utiliser des outils de ligne de commande uniquement.</span><span class="sxs-lookup"><span data-stu-id="ce055-148">hello user can use command-line tools only.</span></span> |
| <span data-ttu-id="ce055-149">Propriétaire</span><span class="sxs-lookup"><span data-stu-id="ce055-149">Owner</span></span> |<span data-ttu-id="ce055-150">Tout</span><span class="sxs-lookup"><span data-stu-id="ce055-150">All</span></span> |<span data-ttu-id="ce055-151">Tout</span><span class="sxs-lookup"><span data-stu-id="ce055-151">All</span></span> |<span data-ttu-id="ce055-152">rôle de propriétaire Hello est un super utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ce055-152">hello Owner role is a superuser.</span></span> <span data-ttu-id="ce055-153">Ce rôle peut tout gérer et a un accès complet toodata.</span><span class="sxs-lookup"><span data-stu-id="ce055-153">This role can manage everything and has full access toodata.</span></span> |
| <span data-ttu-id="ce055-154">Lecteur</span><span class="sxs-lookup"><span data-stu-id="ce055-154">Reader</span></span> |<span data-ttu-id="ce055-155">Lecture seule</span><span class="sxs-lookup"><span data-stu-id="ce055-155">Read-only</span></span> |<span data-ttu-id="ce055-156">Régi par ACL</span><span class="sxs-lookup"><span data-stu-id="ce055-156">Governed by ACL</span></span> |<span data-ttu-id="ce055-157">rôle de lecteur Hello peut tout afficher concernant la gestion des comptes, par exemple quels utilisateur rôle toowhich.</span><span class="sxs-lookup"><span data-stu-id="ce055-157">hello Reader role can view everything regarding account management, such as which user is assigned toowhich role.</span></span> <span data-ttu-id="ce055-158">rôle de lecteur Hello ne peut pas apporter des modifications.</span><span class="sxs-lookup"><span data-stu-id="ce055-158">hello Reader role can't make any changes.</span></span> |
| <span data-ttu-id="ce055-159">Collaborateur</span><span class="sxs-lookup"><span data-stu-id="ce055-159">Contributor</span></span> |<span data-ttu-id="ce055-160">Tout, sauf ajouter et supprimer des rôles</span><span class="sxs-lookup"><span data-stu-id="ce055-160">All except add and remove roles</span></span> |<span data-ttu-id="ce055-161">Régi par ACL</span><span class="sxs-lookup"><span data-stu-id="ce055-161">Governed by ACL</span></span> |<span data-ttu-id="ce055-162">rôle de collaborateur Hello peut gérer certains aspects d’un compte, tels que les déploiements et la création et la gestion des alertes.</span><span class="sxs-lookup"><span data-stu-id="ce055-162">hello Contributor role can manage some aspects of an account, such as deployments and creating and managing alerts.</span></span> <span data-ttu-id="ce055-163">rôle de collaborateur Hello ne peut pas ajouter ou supprimer des rôles.</span><span class="sxs-lookup"><span data-stu-id="ce055-163">hello Contributor role cannot add or remove roles.</span></span> |
| <span data-ttu-id="ce055-164">Administrateur de l'accès utilisateur</span><span class="sxs-lookup"><span data-stu-id="ce055-164">User Access Administrator</span></span> |<span data-ttu-id="ce055-165">Ajouter et supprimer des rôles</span><span class="sxs-lookup"><span data-stu-id="ce055-165">Add and remove roles</span></span> |<span data-ttu-id="ce055-166">Régi par ACL</span><span class="sxs-lookup"><span data-stu-id="ce055-166">Governed by ACL</span></span> |<span data-ttu-id="ce055-167">rôle d’administrateur de l’accès utilisateur Hello peut gérer tooaccounts des accès utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ce055-167">hello User Access Administrator role can manage user access tooaccounts.</span></span> |

<span data-ttu-id="ce055-168">Pour obtenir des instructions, consultez [affecter des utilisateurs ou des groupes de sécurité des comptes de tooData Lake Store](data-lake-store-secure-data.md#assign-users-or-security-groups-to-azure-data-lake-store-accounts).</span><span class="sxs-lookup"><span data-stu-id="ce055-168">For instructions, see [Assign users or security groups tooData Lake Store accounts](data-lake-store-secure-data.md#assign-users-or-security-groups-to-azure-data-lake-store-accounts).</span></span>

### <a name="using-acls-for-operations-on-file-systems"></a><span data-ttu-id="ce055-169">Utilisation des ACL pour les opérations sur les systèmes de fichiers</span><span class="sxs-lookup"><span data-stu-id="ce055-169">Using ACLs for operations on file systems</span></span>
<span data-ttu-id="ce055-170">Data Lake Store est un système de fichiers hiérarchique comme Hadoop HDFS Distributed File System (HDFS), et il prend en charge les [ACL POSIX](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html#ACLs_Access_Control_Lists).</span><span class="sxs-lookup"><span data-stu-id="ce055-170">Data Lake Store is a hierarchical file system like Hadoop Distributed File System (HDFS), and it supports [POSIX ACLs](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html#ACLs_Access_Control_Lists).</span></span> <span data-ttu-id="ce055-171">Elle contrôle en lecture (r), écriture (w) et exécuter (tooresources d’autorisations pour le rôle de propriétaire hello, pour le groupe de propriétaires hello et pour d’autres utilisateurs et groupes x).</span><span class="sxs-lookup"><span data-stu-id="ce055-171">It controls read (r), write (w), and execute (x) permissions tooresources for hello Owner role, for hello Owners group, and for other users and groups.</span></span> <span data-ttu-id="ce055-172">Bonjour Data Lake Store Public Preview (version actuelle de hello), les ACL peuvent être activées sur le dossier racine de hello, dans les sous-dossiers et sur des fichiers individuels.</span><span class="sxs-lookup"><span data-stu-id="ce055-172">In hello Data Lake Store Public Preview (hello current release), ACLs can be enabled on hello root folder, on subfolders, and on individual files.</span></span> <span data-ttu-id="ce055-173">Pour plus d’informations sur le fonctionnement des ACL dans le contexte de Data Lake Store, consultez [Contrôle d’accès dans Data Lake Store](data-lake-store-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="ce055-173">For more information on how ACLs work in context of Data Lake Store, see [Access control in Data Lake Store](data-lake-store-access-control.md).</span></span>

<span data-ttu-id="ce055-174">Nous vous recommandons de définir des ACL pour plusieurs utilisateurs à l’aide des [groupes de sécurité](../active-directory/active-directory-accessmanagement-manage-groups.md).</span><span class="sxs-lookup"><span data-stu-id="ce055-174">We recommend that you define ACLs for multiple users by using [security groups](../active-directory/active-directory-accessmanagement-manage-groups.md).</span></span> <span data-ttu-id="ce055-175">Ajouter le groupe de sécurité utilisateurs tooa, puis attribuez les ACL hello pour un groupe de sécurité toothat fichier ou dossier.</span><span class="sxs-lookup"><span data-stu-id="ce055-175">Add users tooa security group, and then assign hello ACLs for a file or folder toothat security group.</span></span> <span data-ttu-id="ce055-176">Cela est utile lorsque vous souhaitez que les accès personnalisé tooprovide, car vous êtes limité tooadding un maximum de neuf entrées pour un accès personnalisé.</span><span class="sxs-lookup"><span data-stu-id="ce055-176">This is useful when you want tooprovide custom access, because you are limited tooadding a maximum of nine entries for custom access.</span></span> <span data-ttu-id="ce055-177">Pour plus d’informations sur la façon dont les toobetter sécuriser les données stockées dans Data Lake Store à l’aide de groupes de sécurité Azure Active Directory, consultez [affecter des utilisateurs ou groupe de sécurité comme les ACL toohello système de fichiers Azure Data Lake Store](data-lake-store-secure-data.md#filepermissions).</span><span class="sxs-lookup"><span data-stu-id="ce055-177">For more information about how toobetter secure data stored in Data Lake Store by using Azure Active Directory security groups, see [Assign users or security group as ACLs toohello Azure Data Lake Store file system](data-lake-store-secure-data.md#filepermissions).</span></span>

<span data-ttu-id="ce055-178">![Lister les accès standard et personnalisés](./media/data-lake-store-security-overview/adl.acl.2.png "Lister les accès standard et personnalisés")</span><span class="sxs-lookup"><span data-stu-id="ce055-178">![List standard and custom access](./media/data-lake-store-security-overview/adl.acl.2.png "List standard and custom access")</span></span>

## <a name="network-isolation"></a><span data-ttu-id="ce055-179">Isolement réseau</span><span class="sxs-lookup"><span data-stu-id="ce055-179">Network isolation</span></span>
<span data-ttu-id="ce055-180">Stocker des données tooyour d’utilisez Data Lake Store toohelp contrôle l’accès au niveau du réseau hello.</span><span class="sxs-lookup"><span data-stu-id="ce055-180">Use Data Lake Store toohelp control access tooyour data store at hello network level.</span></span> <span data-ttu-id="ce055-181">Vous pouvez activer des pare-feu et définir une plage d’adresses IP pour vos clients approuvés.</span><span class="sxs-lookup"><span data-stu-id="ce055-181">You can establish firewalls and define an IP address range for your trusted clients.</span></span> <span data-ttu-id="ce055-182">Une plage d’adresses IP, seuls les clients qui ont une adresse IP au sein de la plage de hello défini peuvent se connecter tooData Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ce055-182">With an IP address range, only clients that have an IP address within hello defined range can connect tooData Lake Store.</span></span>

<span data-ttu-id="ce055-183">![Paramètres de pare-feu et accès IP](./media/data-lake-store-security-overview/firewall-ip-access.png "Paramètres de pare-feu et accès IP")</span><span class="sxs-lookup"><span data-stu-id="ce055-183">![Firewall settings and IP access](./media/data-lake-store-security-overview/firewall-ip-access.png "Firewall settings and IP address")</span></span>

## <a name="data-protection"></a><span data-ttu-id="ce055-184">Protection des données</span><span class="sxs-lookup"><span data-stu-id="ce055-184">Data protection</span></span>
<span data-ttu-id="ce055-185">Azure Data Lake Store protège vos données tout au long de leur cycle de vie.</span><span class="sxs-lookup"><span data-stu-id="ce055-185">Azure Data Lake Store protects your data throughout its life cycle.</span></span> <span data-ttu-id="ce055-186">Pour les données en transit, Data Lake Store utilise les données toosecure du protocole de sécurité TLS (Transport Layer) hello normalisées réseau hello.</span><span class="sxs-lookup"><span data-stu-id="ce055-186">For data in transit, Data Lake Store uses hello industry-standard Transport Layer Security (TLS) protocol toosecure data over hello network.</span></span>

<span data-ttu-id="ce055-187">![Chiffrement dans Data Lake Store](./media/data-lake-store-security-overview/adls-encryption.png "Chiffrement dans Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="ce055-187">![Encryption in Data Lake Store](./media/data-lake-store-security-overview/adls-encryption.png "Encryption in Data Lake Store")</span></span>

<span data-ttu-id="ce055-188">Data Lake Store fournit également le chiffrement de données qui sont stockés dans le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="ce055-188">Data Lake Store also provides encryption for data that is stored in hello account.</span></span> <span data-ttu-id="ce055-189">Vous pouvez choisir toohave vos données chiffrées ou optez pour aucun chiffrement.</span><span class="sxs-lookup"><span data-stu-id="ce055-189">You can chose toohave your data encrypted or opt for no encryption.</span></span> <span data-ttu-id="ce055-190">Si vous choisissez cette option pour le chiffrement, les données stockées dans Data Lake Store sont chiffrée toostoring préalable sur un support permanent.</span><span class="sxs-lookup"><span data-stu-id="ce055-190">If you opt in for encryption, data stored in Data Lake Store is encrypted prior toostoring on persistent media.</span></span> <span data-ttu-id="ce055-191">Dans ce cas, Data Lake Store toopersisting préalable des données de chiffre et déchiffre tooretrieval préalable de données, afin qu’il soit client toohello totalement transparente l’accès aux données de hello automatiquement.</span><span class="sxs-lookup"><span data-stu-id="ce055-191">In such a case, Data Lake Store automatically encrypts data prior toopersisting and decrypts data prior tooretrieval, so it is completely transparent toohello client accessing hello data.</span></span> <span data-ttu-id="ce055-192">Il n’existe aucune modification du code requise sur les données hello client côté tooencrypt/decrypt.</span><span class="sxs-lookup"><span data-stu-id="ce055-192">There is no code change required on hello client side tooencrypt/decrypt data.</span></span>

<span data-ttu-id="ce055-193">Gestion de clés, Data Lake Store propose deux modes de gestion de vos clés de chiffrement principale (MEKs), qui sont requis pour le déchiffrement des données qui sont stockées dans hello Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ce055-193">For key management, Data Lake Store provides two modes for managing your master encryption keys (MEKs), which are required for decrypting any data that is stored in hello Data Lake Store.</span></span> <span data-ttu-id="ce055-194">Vous pouvez laisser Data Lake Store gérer hello MEKs pour vous, ou choisissez tooretain approprier MEKs hello à l’aide de votre compte Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="ce055-194">You can either let Data Lake Store manage hello MEKs for you, or choose tooretain ownership of hello MEKs using your Azure Key Vault account.</span></span> <span data-ttu-id="ce055-195">Vous spécifiez le mode de gestion de clés hello tandis que lors de la création d’un compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ce055-195">You specify hello mode of key management while while creating a Data Lake Store account.</span></span> <span data-ttu-id="ce055-196">Pour plus d’informations sur la façon de configuration relatives au chiffrement de tooprovide, consultez [prise en main Azure Data Lake Store à l’aide de hello Azure Portal](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ce055-196">For more information on how tooprovide encryption-related configuration, see [Get started with Azure Data Lake Store using hello Azure Portal](data-lake-store-get-started-portal.md).</span></span>

## <a name="auditing-and-diagnostic-logs"></a><span data-ttu-id="ce055-197">Journaux d’audit et de diagnostic</span><span class="sxs-lookup"><span data-stu-id="ce055-197">Auditing and diagnostic logs</span></span>
<span data-ttu-id="ce055-198">Vous pouvez utiliser les journaux d’audit ou de diagnostic selon si vous recherchez des journaux sur des activités liées à la gestion ou des activités liées aux données.</span><span class="sxs-lookup"><span data-stu-id="ce055-198">You can use auditing or diagnostic logs, depending on whether you are looking for logs for management-related activities or data-related activities.</span></span>

* <span data-ttu-id="ce055-199">Activités de gestion utilisent les API du Gestionnaire de ressources Azure et sont signalées dans hello portail Azure via les journaux d’audit.</span><span class="sxs-lookup"><span data-stu-id="ce055-199">Management-related activities use Azure Resource Manager APIs and are surfaced in hello Azure portal via audit logs.</span></span>
* <span data-ttu-id="ce055-200">Les activités liées aux données utilisent les API REST de WebHDFS et sont signalées dans hello portail Azure via les journaux de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="ce055-200">Data-related activities use WebHDFS REST APIs and are surfaced in hello Azure portal via diagnostic logs.</span></span>

### <a name="auditing-logs"></a><span data-ttu-id="ce055-201">Journaux d’audit</span><span class="sxs-lookup"><span data-stu-id="ce055-201">Auditing logs</span></span>
<span data-ttu-id="ce055-202">toocomply avec les réglementations, une organisation peut nécessiter des pistes d’audit appropriées si elle a besoin toodig dans des incidents spécifiques.</span><span class="sxs-lookup"><span data-stu-id="ce055-202">toocomply with regulations, an organization might require adequate audit trails if it needs toodig into specific incidents.</span></span> <span data-ttu-id="ce055-203">Data Lake Store est doté de fonctionnalités intégrées de surveillance et d’audit et journalise toutes les activités de gestion des comptes.</span><span class="sxs-lookup"><span data-stu-id="ce055-203">Data Lake Store has built-in monitoring and auditing, and it logs all account management activities.</span></span>

<span data-ttu-id="ce055-204">Compte gestion des journaux d’audit, afficher et sélectionner des colonnes de hello que vous souhaitez toolog.</span><span class="sxs-lookup"><span data-stu-id="ce055-204">For account management audit trails, view and choose hello columns that you want toolog.</span></span> <span data-ttu-id="ce055-205">Vous pouvez également exporter tooAzure de journaux d’audit stockage.</span><span class="sxs-lookup"><span data-stu-id="ce055-205">You also can export audit logs tooAzure Storage.</span></span>

<span data-ttu-id="ce055-206">![Journaux d’audit](./media/data-lake-store-security-overview/audit-logs.png "Journaux d’Audit")</span><span class="sxs-lookup"><span data-stu-id="ce055-206">![Audit logs](./media/data-lake-store-security-overview/audit-logs.png "Audit logs")</span></span>

### <a name="diagnostic-logs"></a><span data-ttu-id="ce055-207">Journaux de diagnostic</span><span class="sxs-lookup"><span data-stu-id="ce055-207">Diagnostic logs</span></span>
<span data-ttu-id="ce055-208">Vous pouvez définir des pistes d’audit de l’accès aux données dans le portail Azure (dans les paramètres de Diagnostic) de hello et créer un compte de stockage d’objets Blob Azure sur lequel sont enregistrés les journaux de hello.</span><span class="sxs-lookup"><span data-stu-id="ce055-208">You can set data access audit trails in hello Azure portal (in Diagnostic Settings) and create an Azure Blob storage account where hello logs are stored.</span></span>

<span data-ttu-id="ce055-209">![Journaux de diagnostic](./media/data-lake-store-security-overview/diagnostic-logs.png "Journaux de diagnostic")</span><span class="sxs-lookup"><span data-stu-id="ce055-209">![Diagnostic logs](./media/data-lake-store-security-overview/diagnostic-logs.png "Diagnostic logs")</span></span>

<span data-ttu-id="ce055-210">Après avoir configuré les paramètres de diagnostic, vous pouvez afficher des journaux de hello sur hello **journaux de Diagnostic** onglet.</span><span class="sxs-lookup"><span data-stu-id="ce055-210">After you configure diagnostic settings, you can view hello logs on hello **Diagnostic Logs** tab.</span></span>

<span data-ttu-id="ce055-211">Pour plus d’informations sur l’utilisation des journaux de diagnostic avec Azure Data Lake Store, consultez [Accès aux journaux de diagnostic d’Azure Data Lake Store](data-lake-store-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="ce055-211">For more information on working with diagnostic logs with Azure Data Lake Store, see [Access diagnostic logs for Data Lake Store](data-lake-store-diagnostic-logs.md).</span></span>

## <a name="summary"></a><span data-ttu-id="ce055-212">Résumé</span><span class="sxs-lookup"><span data-stu-id="ce055-212">Summary</span></span>
<span data-ttu-id="ce055-213">Les clients d’entreprise exigent une plateforme cloud données analytique est toouse simple et sécurisée.</span><span class="sxs-lookup"><span data-stu-id="ce055-213">Enterprise customers demand a data analytics cloud platform that is secure and easy toouse.</span></span> <span data-ttu-id="ce055-214">Azure Data Lake Store est conçu toohelp surmonter ces difficultés via la gestion des identités et l’authentification via l’intégration d’Azure Active Directory, d’autorisation basée sur les ACL, l’isolement réseau, le chiffrement des données en transit et au repos (entrants hello ultérieures) et l’audit.</span><span class="sxs-lookup"><span data-stu-id="ce055-214">Azure Data Lake Store is designed toohelp address these requirements through identity management and authentication via Azure Active Directory integration, ACL-based authorization, network isolation, data encryption in transit and at rest (coming in hello future), and auditing.</span></span>

<span data-ttu-id="ce055-215">Si vous souhaitez toosee les nouvelles fonctionnalités de Data Lake Store, nous envoyer vos commentaires Bonjour [UserVoice de magasin de données Lake forum](https://feedback.azure.com/forums/327234-data-lake).</span><span class="sxs-lookup"><span data-stu-id="ce055-215">If you want toosee new features in Data Lake Store, send us your feedback in hello [Data Lake Store UserVoice forum](https://feedback.azure.com/forums/327234-data-lake).</span></span>

## <a name="see-also"></a><span data-ttu-id="ce055-216">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="ce055-216">See also</span></span>
* [<span data-ttu-id="ce055-217">Présentation d’Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ce055-217">Overview of Azure Data Lake Store</span></span>](data-lake-store-overview.md)
* [<span data-ttu-id="ce055-218">Prise en main d’Azure Data Lake Store avec le portail Azure</span><span class="sxs-lookup"><span data-stu-id="ce055-218">Get started with Data Lake Store</span></span>](data-lake-store-get-started-portal.md)
* [<span data-ttu-id="ce055-219">Sécuriser les données dans Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ce055-219">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
