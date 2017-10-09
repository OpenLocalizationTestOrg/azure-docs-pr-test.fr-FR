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
# <a name="configure-and-manage-azure-sql-database-security-for-geo-restore-or-failover"></a>Configurer et gérer la sécurité Azure SQL Database pour la géo-restauration ou le basculement 

> [!NOTE]
> La [géoréplication active](sql-database-geo-replication-overview.md) est désormais disponible pour toutes les bases de données de tous les niveaux de service.
>  

## <a name="overview-of-authentication-requirements-for-disaster-recovery"></a>Vue d’ensemble des exigences d’authentification pour la récupération d’urgence
Cette rubrique décrit hello authentification exigences tooconfigure et contrôle [géo-réplication active](sql-database-geo-replication-overview.md) hello les étapes requise tooset haut de la base de données secondaire de toohello accès utilisateur. Elle décrit également comment activer l’accès toohello base de données récupérée après l’utilisation de [géo-restauration](sql-database-recovery-using-backups.md#geo-restore). Pour plus d’informations sur les options de récupération, consultez [Vue d’ensemble de la continuité des activités](sql-database-business-continuity.md).

## <a name="disaster-recovery-with-contained-users"></a>Récupération d’urgence avec des utilisateurs contenus
Contrairement aux utilisateurs traditionnels, qui doit être mappé à toologins dans la base de données master hello, un utilisateur contenu est entièrement géré par base de données hello lui-même. Cela a deux avantages. Dans un scénario de récupération d’urgence hello, les utilisateurs de hello peuvent continuer tooconnect toohello nouvelle base de données primaire ou base de données hello récupéré à l’aide de géo-restauration sans configuration supplémentaire, car la base de données hello gère les utilisateurs de hello. Du point de vue de la connexion, cette configuration présente également des possibilités de mise à l’échelle et d’amélioration des performances. Pour plus d’informations, voir [Utilisateurs de base de données à relation contenant-contenu - Rendre votre base de données portable](https://msdn.microsoft.com/library/ff929188.aspx). 

les compromis principal Hello sont que la gestion des processus de récupération d’urgence hello à l’échelle sont plus difficile. Lorsque vous disposez de plusieurs bases de données que hello utilisation contenue de la même connexion, en conservant les informations d’identification hello à l’aide les utilisateurs dans plusieurs bases de données peuvent anéantir les avantages de hello des utilisateurs contenus. Par exemple, la stratégie de rotation de mot de passe hello nécessite qu’apporter des modifications régulièrement dans plusieurs bases de données plutôt que modifier mot de passe hello pour hello qu’une seule fois dans la base de données master hello. Pour cette raison, si vous disposez de plusieurs bases de données que hello utilisez même nom d’utilisateur et mot de passe, à l’aide les utilisateurs contenus n’est pas recommandée. 

## <a name="how-tooconfigure-logins-and-users"></a>Comment tooconfigure connexions et utilisateurs
Si vous utilisez des connexions et les utilisateurs (et non les utilisateurs contenus), vous devez prendre des étapes supplémentaires tooinsure que hello mêmes connexions existent dans la base de données master hello. Hello sections ci-dessous présentent les considérations hello étapes impliquées et d’autres.

### <a name="set-up-user-access-tooa-secondary-or-recovered-database"></a>Configurer les accès tooa secondaire récupéré ou de base de données utilisateur
Pour toobe de base de données secondaire hello utilisable comme une base de données secondaire en lecture seule et tooensure accès toohello hello ou base de données de base de données primaire récupéré à l’aide de géo-restauration hello master base de données du serveur cible de hello doit avoir hello configuration de sécurité appropriés en place avant la récupération de hello.

Hello des autorisations spécifiques pour chaque étape sont décrites plus loin dans cette rubrique.

Préparation de tooa des accès utilisateur géo-réplication secondaire doit être effectuée dans le cadre de la configuration de géo-réplication. Préparation des bases de données de géo-restauration toohello accès utilisateur doit être effectuée à tout moment lorsque le serveur d’origine de hello est en ligne (par exemple, dans le cadre de l’extraction de récupération d’urgence de hello).

> [!NOTE]
> Si vous ne parvenez pas over ou géo-restauration serveur tooa qui n’a pas correctement configuré les connexions, accès tooit sera le compte d’administrateur de serveur de toohello limité.
> 
> 

Configuration des connexions sur le serveur cible de hello implique trois étapes décrites ci-dessous :

#### <a name="1-determine-logins-with-access-toohello-primary-database"></a>1. Déterminer les connexions avec la base de données access toohello principal :
Hello première étape du processus de hello est toodetermine les connexions doivent être dupliquées sur le serveur cible de hello. Pour cela, une paire d’instructions SELECT, une hello logique base de données master sur le serveur de source de hello et dans hello principal de base de données elle-même.

Uniquement hello administrateur du serveur ou un membre de hello **LoginManager** rôle de serveur peut déterminer les connexions de hello sur le serveur de source de hello avec hello après l’instruction SELECT. 

    SELECT [name], [sid] 
    FROM [sys].[sql_logins] 
    WHERE [type_desc] = 'SQL_Login'

Seul un membre du rôle de base de données db_owner hello, un utilisateur dbo de hello ou administrateur du serveur, peut déterminer toutes les entités d’utilisateur de base de données hello dans la base de données primaire hello.

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

#### <a name="2-find-hello-sid-for-hello-logins-identified-in-step-1"></a>2. Recherche hello SID pour les connexions hello identifiées à l’étape 1 :
En comparant la sortie hello de requêtes hello à partir de la section précédente de hello et correspondance hello SID, vous pouvez mapper hello serveur de connexion toodatabase utilisateur. Connexions qui ont un utilisateur de base de données avec le SID correspondant ont toothat base de données access utilisateur en tant qu’utilisateur de base de données principal. 

Hello requête suivante peut être utilisé toosee tous les principaux d’utilisateur hello et leur SID dans une base de données. Seul un membre de hello db_owner de base de données serveur ou du rôle administrateur peut exécuter cette requête.

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

> [!NOTE]
> Hello **INFORMATION_SCHEMA** et **sys** les utilisateurs ont *NULL* SID et hello **invité** possède un SID **0 x 00**. Hello **dbo** SID peut commencer par *0 x 01060000000001648000000000048454*, si le créateur de base de données hello était administrateur du serveur hello au lieu d’un membre de **DbManager**.
> 
> 

#### <a name="3-create-hello-logins-on-hello-target-server"></a>3. Permet de créer des connexions de hello sur le serveur cible de hello :
Hello dernière étape est toogo toohello cible, ou les serveurs et générer les connexions hello hello approprié SID. syntaxe de base Hello est comme suit.

    CREATE LOGIN [<login name>]
    WITH PASSWORD = <login password>,
    SID = <desired login SID>

> [!NOTE]
> Si vous souhaitez toogrant utilisateur accès toohello secondaire, mais pas toohello principal, c’est également en modifiant la connexion de l’utilisateur sur le serveur principal de hello hello à l’aide de la syntaxe de hello.
> 
> ALTER LOGIN <login name> DISABLE
> 
> DISABLE ne modifie pas un mot de passe hello, donc vous pouvez toujours l’activer si nécessaire.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
* Pour plus d’informations sur la gestion de l’accès aux bases de données et des identifiants de connexion, consultez [Sécurité SQL Database : gérer la sécurité d’accès et de connexion aux bases de données](sql-database-manage-logins.md).
* Pour plus d’informations sur les utilisateurs de base de données à relation contenant-contenu, consultez [Utilisateurs de base de données à relation contenant-contenu - Rendre votre base de données portable](https://msdn.microsoft.com/library/ff929188.aspx).
* Pour plus d’informations sur l’utilisation et la configuration de la géoréplication active, voir [Géoréplication active](sql-database-geo-replication-overview.md).
* Pour plus d’informations sur l’utilisation de la géorestauration, voir [Géorestauration](sql-database-recovery-using-backups.md#geo-restore).

