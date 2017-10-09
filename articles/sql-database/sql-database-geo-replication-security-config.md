---
title: "sécurité de base de données SQL Azure pour la récupération d’urgence d’aaaConfigure | Documents Microsoft"
description: "Cette rubrique décrit les considérations de sécurité pour la configuration et la gestion de la sécurité après une restauration de base de données ou un serveur secondaire tooa de basculement en cas de hello de panne du centre de données ou d’autres d’urgence"
services: sql-database
documentationcenter: na
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: c7c898c9-69d4-4e16-8b7e-720bbb3353dd
ms.service: sql-database
ms.custom: business continuity
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 10/13/2016
ms.author: sashan
ms.openlocfilehash: c3172568e1b8ad2a53958200aa6cf19b4a9434ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-manage-azure-sql-database-security-for-geo-restore-or-failover"></a><span data-ttu-id="e55cf-103">Configurer et gérer la sécurité Azure SQL Database pour la géo-restauration ou le basculement</span><span class="sxs-lookup"><span data-stu-id="e55cf-103">Configure and manage Azure SQL Database security for geo-restore or failover</span></span> 

> [!NOTE]
> <span data-ttu-id="e55cf-104">La [géoréplication active](sql-database-geo-replication-overview.md) est désormais disponible pour toutes les bases de données de tous les niveaux de service.</span><span class="sxs-lookup"><span data-stu-id="e55cf-104">[Active geo-replication](sql-database-geo-replication-overview.md) is now available for all databases in all service tiers.</span></span>
>  

## <a name="overview-of-authentication-requirements-for-disaster-recovery"></a><span data-ttu-id="e55cf-105">Vue d’ensemble des exigences d’authentification pour la récupération d’urgence</span><span class="sxs-lookup"><span data-stu-id="e55cf-105">Overview of authentication requirements for disaster recovery</span></span>
<span data-ttu-id="e55cf-106">Cette rubrique décrit hello authentification exigences tooconfigure et contrôle [géo-réplication active](sql-database-geo-replication-overview.md) hello les étapes requise tooset haut de la base de données secondaire de toohello accès utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e55cf-106">This topic describes hello authentication requirements tooconfigure and control [active geo-replication](sql-database-geo-replication-overview.md) and hello steps required tooset up user access toohello secondary database.</span></span> <span data-ttu-id="e55cf-107">Elle décrit également comment activer l’accès toohello base de données récupérée après l’utilisation de [géo-restauration](sql-database-recovery-using-backups.md#geo-restore).</span><span class="sxs-lookup"><span data-stu-id="e55cf-107">It also describes how enable access toohello recovered database after using [geo-restore](sql-database-recovery-using-backups.md#geo-restore).</span></span> <span data-ttu-id="e55cf-108">Pour plus d’informations sur les options de récupération, consultez [Vue d’ensemble de la continuité des activités](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="e55cf-108">For more information on recovery options, see [Business Continuity Overview](sql-database-business-continuity.md).</span></span>

## <a name="disaster-recovery-with-contained-users"></a><span data-ttu-id="e55cf-109">Récupération d’urgence avec des utilisateurs contenus</span><span class="sxs-lookup"><span data-stu-id="e55cf-109">Disaster recovery with contained users</span></span>
<span data-ttu-id="e55cf-110">Contrairement aux utilisateurs traditionnels, qui doit être mappé à toologins dans la base de données master hello, un utilisateur contenu est entièrement géré par base de données hello lui-même.</span><span class="sxs-lookup"><span data-stu-id="e55cf-110">Unlike traditional users, which must be mapped toologins in hello master database, a contained user is managed completely by hello database itself.</span></span> <span data-ttu-id="e55cf-111">Cela a deux avantages.</span><span class="sxs-lookup"><span data-stu-id="e55cf-111">This has two benefits.</span></span> <span data-ttu-id="e55cf-112">Dans un scénario de récupération d’urgence hello, les utilisateurs de hello peuvent continuer tooconnect toohello nouvelle base de données primaire ou base de données hello récupéré à l’aide de géo-restauration sans configuration supplémentaire, car la base de données hello gère les utilisateurs de hello.</span><span class="sxs-lookup"><span data-stu-id="e55cf-112">In hello disaster recovery scenario, hello users can continue tooconnect toohello new primary database or hello database recovered using geo-restore without any additional configuration, because hello database manages hello users.</span></span> <span data-ttu-id="e55cf-113">Du point de vue de la connexion, cette configuration présente également des possibilités de mise à l’échelle et d’amélioration des performances.</span><span class="sxs-lookup"><span data-stu-id="e55cf-113">There are also potential scalability and performance benefits from this configuration from a login perspective.</span></span> <span data-ttu-id="e55cf-114">Pour plus d’informations, voir [Utilisateurs de base de données à relation contenant-contenu - Rendre votre base de données portable](https://msdn.microsoft.com/library/ff929188.aspx).</span><span class="sxs-lookup"><span data-stu-id="e55cf-114">For more information, see [Contained Database Users - Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx).</span></span> 

<span data-ttu-id="e55cf-115">les compromis principal Hello sont que la gestion des processus de récupération d’urgence hello à l’échelle sont plus difficile.</span><span class="sxs-lookup"><span data-stu-id="e55cf-115">hello main trade-off is that managing hello disaster recovery process at scale is more challenging.</span></span> <span data-ttu-id="e55cf-116">Lorsque vous disposez de plusieurs bases de données que hello utilisation contenue de la même connexion, en conservant les informations d’identification hello à l’aide les utilisateurs dans plusieurs bases de données peuvent anéantir les avantages de hello des utilisateurs contenus.</span><span class="sxs-lookup"><span data-stu-id="e55cf-116">When you have multiple databases that use hello same login, maintaining hello credentials using contained users in multiple databases may negate hello benefits of contained users.</span></span> <span data-ttu-id="e55cf-117">Par exemple, la stratégie de rotation de mot de passe hello nécessite qu’apporter des modifications régulièrement dans plusieurs bases de données plutôt que modifier mot de passe hello pour hello qu’une seule fois dans la base de données master hello.</span><span class="sxs-lookup"><span data-stu-id="e55cf-117">For example, hello password rotation policy requires that changes be made consistently in multiple databases rather than changing hello password for hello login once in hello master database.</span></span> <span data-ttu-id="e55cf-118">Pour cette raison, si vous disposez de plusieurs bases de données que hello utilisez même nom d’utilisateur et mot de passe, à l’aide les utilisateurs contenus n’est pas recommandée.</span><span class="sxs-lookup"><span data-stu-id="e55cf-118">For this reason, if you have multiple databases that use hello same user name and password, using contained users is not recommended.</span></span> 

## <a name="how-tooconfigure-logins-and-users"></a><span data-ttu-id="e55cf-119">Comment tooconfigure connexions et utilisateurs</span><span class="sxs-lookup"><span data-stu-id="e55cf-119">How tooconfigure logins and users</span></span>
<span data-ttu-id="e55cf-120">Si vous utilisez des connexions et les utilisateurs (et non les utilisateurs contenus), vous devez prendre des étapes supplémentaires tooinsure que hello mêmes connexions existent dans la base de données master hello.</span><span class="sxs-lookup"><span data-stu-id="e55cf-120">If you are using logins and users (rather than contained users), you must take extra steps tooinsure that hello same logins exist in hello master database.</span></span> <span data-ttu-id="e55cf-121">Hello sections ci-dessous présentent les considérations hello étapes impliquées et d’autres.</span><span class="sxs-lookup"><span data-stu-id="e55cf-121">hello following sections outline hello steps involved and additional considerations.</span></span>

### <a name="set-up-user-access-tooa-secondary-or-recovered-database"></a><span data-ttu-id="e55cf-122">Configurer les accès tooa secondaire récupéré ou de base de données utilisateur</span><span class="sxs-lookup"><span data-stu-id="e55cf-122">Set up user access tooa secondary or recovered database</span></span>
<span data-ttu-id="e55cf-123">Pour toobe de base de données secondaire hello utilisable comme une base de données secondaire en lecture seule et tooensure accès toohello hello ou base de données de base de données primaire récupéré à l’aide de géo-restauration hello master base de données du serveur cible de hello doit avoir hello configuration de sécurité appropriés en place avant la récupération de hello.</span><span class="sxs-lookup"><span data-stu-id="e55cf-123">In order for hello secondary database toobe usable as a read-only secondary database, and tooensure proper access toohello new primary database or hello database recovered using geo-restore, hello master database of hello target server must have hello appropriate security configuration in place before hello recovery.</span></span>

<span data-ttu-id="e55cf-124">Hello des autorisations spécifiques pour chaque étape sont décrites plus loin dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="e55cf-124">hello specific permissions for each step are described later in this topic.</span></span>

<span data-ttu-id="e55cf-125">Préparation de tooa des accès utilisateur géo-réplication secondaire doit être effectuée dans le cadre de la configuration de géo-réplication.</span><span class="sxs-lookup"><span data-stu-id="e55cf-125">Preparing user access tooa geo-replication secondary should be performed as part configuring geo-replication.</span></span> <span data-ttu-id="e55cf-126">Préparation des bases de données de géo-restauration toohello accès utilisateur doit être effectuée à tout moment lorsque le serveur d’origine de hello est en ligne (par exemple, dans le cadre de l’extraction de récupération d’urgence de hello).</span><span class="sxs-lookup"><span data-stu-id="e55cf-126">Preparing user access toohello geo-restored databases should be performed at any time when hello original server is online (e.g. as part of hello DR drill).</span></span>

> [!NOTE]
> <span data-ttu-id="e55cf-127">Si vous ne parvenez pas over ou géo-restauration serveur tooa qui n’a pas correctement configuré les connexions, accès tooit sera le compte d’administrateur de serveur de toohello limité.</span><span class="sxs-lookup"><span data-stu-id="e55cf-127">If you fail over or geo-restore tooa server that does not have properly configured logins, access tooit will be limited toohello server admin account.</span></span>
> 
> 

<span data-ttu-id="e55cf-128">Configuration des connexions sur le serveur cible de hello implique trois étapes décrites ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="e55cf-128">Setting up logins on hello target server involves three steps outlined below:</span></span>

#### <a name="1-determine-logins-with-access-toohello-primary-database"></a><span data-ttu-id="e55cf-129">1. Déterminer les connexions avec la base de données access toohello principal :</span><span class="sxs-lookup"><span data-stu-id="e55cf-129">1. Determine logins with access toohello primary database:</span></span>
<span data-ttu-id="e55cf-130">Hello première étape du processus de hello est toodetermine les connexions doivent être dupliquées sur le serveur cible de hello.</span><span class="sxs-lookup"><span data-stu-id="e55cf-130">hello first step of hello process is toodetermine which logins must be duplicated on hello target server.</span></span> <span data-ttu-id="e55cf-131">Pour cela, une paire d’instructions SELECT, une hello logique base de données master sur le serveur de source de hello et dans hello principal de base de données elle-même.</span><span class="sxs-lookup"><span data-stu-id="e55cf-131">This is accomplished with a pair of SELECT statements, one in hello logical master database on hello source server and one in hello primary database itself.</span></span>

<span data-ttu-id="e55cf-132">Uniquement hello administrateur du serveur ou un membre de hello **LoginManager** rôle de serveur peut déterminer les connexions de hello sur le serveur de source de hello avec hello après l’instruction SELECT.</span><span class="sxs-lookup"><span data-stu-id="e55cf-132">Only hello server admin or a member of hello **LoginManager** server role can determine hello logins on hello source server with hello following SELECT statement.</span></span> 

    SELECT [name], [sid] 
    FROM [sys].[sql_logins] 
    WHERE [type_desc] = 'SQL_Login'

<span data-ttu-id="e55cf-133">Seul un membre du rôle de base de données db_owner hello, un utilisateur dbo de hello ou administrateur du serveur, peut déterminer toutes les entités d’utilisateur de base de données hello dans la base de données primaire hello.</span><span class="sxs-lookup"><span data-stu-id="e55cf-133">Only a member of hello db_owner database role, hello dbo user, or server admin, can determine all of hello database user principals in hello primary database.</span></span>

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

#### <a name="2-find-hello-sid-for-hello-logins-identified-in-step-1"></a><span data-ttu-id="e55cf-134">2. Recherche hello SID pour les connexions hello identifiées à l’étape 1 :</span><span class="sxs-lookup"><span data-stu-id="e55cf-134">2. Find hello SID for hello logins identified in step 1:</span></span>
<span data-ttu-id="e55cf-135">En comparant la sortie hello de requêtes hello à partir de la section précédente de hello et correspondance hello SID, vous pouvez mapper hello serveur de connexion toodatabase utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e55cf-135">By comparing hello output of hello queries from hello previous section and matching hello SIDs, you can map hello server login toodatabase user.</span></span> <span data-ttu-id="e55cf-136">Connexions qui ont un utilisateur de base de données avec le SID correspondant ont toothat base de données access utilisateur en tant qu’utilisateur de base de données principal.</span><span class="sxs-lookup"><span data-stu-id="e55cf-136">Logins that have a database user with a matching SID have user access toothat database as that database user principal.</span></span> 

<span data-ttu-id="e55cf-137">Hello requête suivante peut être utilisé toosee tous les principaux d’utilisateur hello et leur SID dans une base de données.</span><span class="sxs-lookup"><span data-stu-id="e55cf-137">hello following query can be used toosee all of hello user principals and their SIDs in a database.</span></span> <span data-ttu-id="e55cf-138">Seul un membre de hello db_owner de base de données serveur ou du rôle administrateur peut exécuter cette requête.</span><span class="sxs-lookup"><span data-stu-id="e55cf-138">Only a member of hello db_owner database role or server admin can run this query.</span></span>

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

> [!NOTE]
> <span data-ttu-id="e55cf-139">Hello **INFORMATION_SCHEMA** et **sys** les utilisateurs ont *NULL* SID et hello **invité** possède un SID **0 x 00**.</span><span class="sxs-lookup"><span data-stu-id="e55cf-139">hello **INFORMATION_SCHEMA** and **sys** users have *NULL* SIDs, and hello **guest** SID is **0x00**.</span></span> <span data-ttu-id="e55cf-140">Hello **dbo** SID peut commencer par *0 x 01060000000001648000000000048454*, si le créateur de base de données hello était administrateur du serveur hello au lieu d’un membre de **DbManager**.</span><span class="sxs-lookup"><span data-stu-id="e55cf-140">hello **dbo** SID may start with *0x01060000000001648000000000048454*, if hello database creator was hello server admin instead of a member of **DbManager**.</span></span>
> 
> 

#### <a name="3-create-hello-logins-on-hello-target-server"></a><span data-ttu-id="e55cf-141">3. Permet de créer des connexions de hello sur le serveur cible de hello :</span><span class="sxs-lookup"><span data-stu-id="e55cf-141">3. Create hello logins on hello target server:</span></span>
<span data-ttu-id="e55cf-142">Hello dernière étape est toogo toohello cible, ou les serveurs et générer les connexions hello hello approprié SID.</span><span class="sxs-lookup"><span data-stu-id="e55cf-142">hello last step is toogo toohello target server, or servers, and generate hello logins with hello appropriate SIDs.</span></span> <span data-ttu-id="e55cf-143">syntaxe de base Hello est comme suit.</span><span class="sxs-lookup"><span data-stu-id="e55cf-143">hello basic syntax is as follows.</span></span>

    CREATE LOGIN [<login name>]
    WITH PASSWORD = <login password>,
    SID = <desired login SID>

> [!NOTE]
> <span data-ttu-id="e55cf-144">Si vous souhaitez toogrant utilisateur accès toohello secondaire, mais pas toohello principal, c’est également en modifiant la connexion de l’utilisateur sur le serveur principal de hello hello à l’aide de la syntaxe de hello.</span><span class="sxs-lookup"><span data-stu-id="e55cf-144">If you want toogrant user access toohello secondary, but not toohello primary, you can do that by altering hello user login on hello primary server by using hello following syntax.</span></span>
> 
> <span data-ttu-id="e55cf-145">ALTER LOGIN <login name> DISABLE</span><span class="sxs-lookup"><span data-stu-id="e55cf-145">ALTER LOGIN <login name> DISABLE</span></span>
> 
> <span data-ttu-id="e55cf-146">DISABLE ne modifie pas un mot de passe hello, donc vous pouvez toujours l’activer si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e55cf-146">DISABLE doesn’t change hello password, so you can always enable it if needed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="e55cf-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e55cf-147">Next steps</span></span>
* <span data-ttu-id="e55cf-148">Pour plus d’informations sur la gestion de l’accès aux bases de données et des identifiants de connexion, consultez [Sécurité SQL Database : gérer la sécurité d’accès et de connexion aux bases de données](sql-database-manage-logins.md).</span><span class="sxs-lookup"><span data-stu-id="e55cf-148">For more information on managing database access and logins, see [SQL Database security: Manage database access and login security](sql-database-manage-logins.md).</span></span>
* <span data-ttu-id="e55cf-149">Pour plus d’informations sur les utilisateurs de base de données à relation contenant-contenu, consultez [Utilisateurs de base de données à relation contenant-contenu - Rendre votre base de données portable](https://msdn.microsoft.com/library/ff929188.aspx).</span><span class="sxs-lookup"><span data-stu-id="e55cf-149">For more information on contained database users, see [Contained Database Users - Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx).</span></span>
* <span data-ttu-id="e55cf-150">Pour plus d’informations sur l’utilisation et la configuration de la géoréplication active, voir [Géoréplication active](sql-database-geo-replication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e55cf-150">For information about using and configuring active geo-replication, see [active geo-replication](sql-database-geo-replication-overview.md)</span></span>
* <span data-ttu-id="e55cf-151">Pour plus d’informations sur l’utilisation de la géorestauration, voir [Géorestauration](sql-database-recovery-using-backups.md#geo-restore).</span><span class="sxs-lookup"><span data-stu-id="e55cf-151">For information about using geo-restore, see [geo-restore](sql-database-recovery-using-backups.md#geo-restore)</span></span>

