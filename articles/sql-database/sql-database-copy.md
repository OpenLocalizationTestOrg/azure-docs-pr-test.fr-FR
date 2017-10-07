---
title: "aaaCopy une base de données SQL Azure | Documents Microsoft"
description: "Création d'une copie d'une base de données SQL Azure"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 5aaf6bcd-3839-49b5-8c77-cbdf786e359b
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.date: 06/15/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 64a297d819d6da89600fda60abe8394ae405abfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-an-azure-sql-database"></a>Copie d'une base de données SQL Azure

Base de données SQL Azure fournit plusieurs méthodes pour la création d’une copie cohérente de SQL Azure existantes de base de données sur deux hello même serveur ou un autre serveur. Vous pouvez copier une base de données SQL à l’aide de T-SQL, PowerShell ou hello portail Azure. 

## <a name="overview"></a>Vue d'ensemble

Une copie de la base de données est un instantané de base de données source hello sien hello de demande de copie hello. Vous pouvez sélectionner hello même serveur ou un autre serveur, son niveau de performances et de la couche de service ou un niveau de performance différents au sein de hello même niveau de service (édition). Une fois hello copie terminée, elle devient une base de données totalement opérationnelle et indépendante. À ce stade, vous pouvez mettre à niveau ou rétrograder le tooany edition. les autorisations, les utilisateurs et les connexions de hello peuvent être gérées indépendamment.  

## <a name="logins-in-hello-database-copy"></a>Connexions dans la copie de base de données hello

Lorsque vous copiez une base de données toohello même serveur logique, hello mêmes connexions peuvent être utilisées sur les deux bases de données. Hello principal de sécurité que vous utilisez base de données toocopy hello devient propriétaire de base de données hello sur la nouvelle base de données hello. Tous les utilisateurs de base de données, leurs autorisations et leur sécurité (SID) les identificateurs sont copiés de copie de base de données toohello.  

Lorsque vous copiez un base de données tooa autre serveur logique, la sécurité de hello principale sur le nouveau serveur de hello devient propriétaire de base de données hello sur la nouvelle base de données hello. Si vous utilisez [contenait des utilisateurs de base de données](sql-database-manage-logins.md) pour accéder aux données, vérifiez que les deux hello principal et bases de données secondaires ont toujours hello mêmes informations d’identification utilisateur, afin qu’après hello copie est terminée, vous peuvent accéder immédiatement à hello même informations d’identification. 

Si vous utilisez [Azure Active Directory](../active-directory/active-directory-whatis.md), vous pouvez éliminer entièrement besoin hello pour la gestion des informations d’identification dans la copie de hello. Toutefois, lorsque vous copiez le nouveau serveur hello de base de données tooa, accès en fonction du compte de connexion de hello pas fonctionnent, car les connexions hello n’existent pas sur le nouveau serveur de hello. toolearn sur la gestion des connexions lorsque vous copiez un base de données tooa autre serveur logique, consultez [toomanage SQL Azure base de sécurité après la récupération d’urgence](sql-database-geo-replication-security-config.md). 

Une fois la copie hello et avant les autres utilisateurs soient remappés, uniquement hello connexion qui a initié hello copie, propriétaire de base de données hello, peut se connecter toohello nouvelle base de données. connexions tooresolve après hello opération de copie est terminée, consultez [résoudre connexions](#resolve-logins).

## <a name="copy-a-database-by-using-hello-azure-portal"></a>Copier une base de données à l’aide de hello portail Azure

toocopy une base de données à l’aide de hello portail Azure, page hello ouvert pour votre base de données, puis cliquez sur **copie**. 

   ![Copie de base de données](./media/sql-database-copy/database-copy.png)

## <a name="copy-a-database-by-using-powershell"></a>Copier une base de données à l’aide de PowerShell

toocopy une base de données à l’aide de PowerShell, utilisez hello [New-AzureRmSqlDatabaseCopy](/powershell/module/azurerm.sql/new-azurermsqldatabasecopy) applet de commande. 

```PowerShell
New-AzureRmSqlDatabaseCopy -ResourceGroupName "myResourceGroup" `
    -ServerName $sourceserver `
    -DatabaseName "MySampleDatabase" `
    -CopyResourceGroupName "myResourceGroup" `
    -CopyServerName $targetserver `
    -CopyDatabaseName "CopyOfMySampleDatabase"
```

Pour un exemple complet de script, consultez [copier un tooa nouveau serveur de base de données](scripts/sql-database-copy-database-to-new-server-powershell.md).

## <a name="copy-a-database-by-using-transact-sql"></a>Copier une base de données à l’aide de Transact-SQL

Ouvrez une session toohello principale de base de données avec connexion du principal au niveau du serveur hello ou connexion hello créer hello base de données toocopy. Pour la base de données copie toosucceed, les connexions qui ne sont pas hello au niveau du serveur principal doivent être membres du rôle dbmanager de hello. Pour plus d’informations sur les connexions et connexion toohello server, consultez [gérer des connexions](sql-database-manage-logins.md).

Commencer la copie de base de données source hello avec hello [CREATE DATABASE](https://msdn.microsoft.com/library/ms176061.aspx) instruction. L’exécution de cette instruction de lance le processus de copie de la base de données hello. Étant donné que la copie d’une base de données est un processus asynchrone, hello instruction CREATE DATABASE retourne avant que la copie de base de données hello est terminée.

### <a name="copy-a-sql-database-toohello-same-server"></a>Copier un toohello de la base de données SQL server même
Ouvrez une session toohello principale de base de données avec connexion du principal au niveau du serveur hello ou connexion hello créer hello base de données toocopy. Pour la base de données copie toosucceed, les connexions qui ne sont pas hello au niveau du serveur principal doivent être membres du rôle dbmanager de hello.

Cette commande copie Database1 tooa nouvelle base de données nommée Database2 sur hello même serveur. Selon la taille de hello de votre base de données, hello opération de copie peut prendre quelques toocomplete de temps.

    -- Execute on hello master database.
    -- Start copying.
    CREATE DATABASE Database1_copy AS COPY OF Database1;

### <a name="copy-a-sql-database-tooa-different-server"></a>Copier un serveur de différents tooa de base de données SQL

Connectez-vous toohello principale de base de données du serveur de destination hello, serveur de base de données SQL hello où la nouvelle base de données hello est toobe créé. Utilisez une connexion qui a hello même nom et le mot de passe en tant que propriétaire de base de données hello de base de données source hello sur le serveur de base de données SQL hello source. Hello connexion sur le serveur de destination hello doit également être membre du rôle dbmanager de hello ou être hello connexion du principal au niveau du serveur.

Cette commande copie Database1 sur server1 tooa nouvelle base de données nommée Database2 sur server2. Selon la taille de hello de votre base de données, hello opération de copie peut prendre quelques toocomplete de temps.

    -- Execute on hello master database of hello target server (server2)
    -- Start copying from Server1 tooServer2
    CREATE DATABASE Database1_copy AS COPY OF server1.Database1;


### <a name="monitor-hello-progress-of-hello-copying-operation"></a>Surveiller la progression hello Hello opération de copie

Surveiller le processus de copie hello en interrogeant les vues sys.databases et sys.dm_database_copies hello. Lors de la copie de hello est en cours, hello **state_desc** le jeu de colonnes de vue de sys.databases hello pour la nouvelle base de données hello est trop**copie**.

* Si hello copie échoue, hello **state_desc** le jeu de colonnes de vue de sys.databases hello pour la nouvelle base de données hello est trop**SOUPÇONNER**. Exécutez hello instruction DROP sur la nouvelle base de données hello et réessayez plus tard.
* Si hello copie réussit, hello **state_desc** le jeu de colonnes de vue de sys.databases hello pour la nouvelle base de données hello est trop**ONLINE**. Hello la copie est terminée et nouvelle base de données hello est une base de données normale qui peut être modifié indépendamment de la base de données source hello.

> [!NOTE]
> Si vous décidez de toocancel hello copie alors qu’il est en cours d’exécution, exécutez hello [DROP DATABASE](https://msdn.microsoft.com/library/ms178613.aspx) instruction sur la nouvelle base de données hello. Vous pouvez également l’exécution d’instruction DROP DATABASE de hello sur la base de données source hello annule également hello processus de copie.
> 

## <a name="resolve-logins"></a>Résolution des connexions

Une fois la nouvelle base de données hello en ligne sur le serveur de destination hello, utilisez hello [ALTER USER](https://msdn.microsoft.com/library/ms176060.aspx) instruction tooremap hello les utilisateurs de hello nouvelle base de données toologins sur le serveur de destination hello. les utilisateurs tooresolve orphelin, voir [dépanner des utilisateurs orphelins](https://msdn.microsoft.com/library/ms175475.aspx). Voir aussi [toomanage SQL Azure base de sécurité après la récupération d’urgence](sql-database-geo-replication-security-config.md).

Tous les utilisateurs de base de données hello conservent les autorisations de hello qu’ils avaient dans la base de données source hello. Hello l’utilisateur qui a initié la copie de base de données hello devient propriétaire de base de données hello de base de données hello et reçoit un nouvel identificateur de sécurité (SID). Une fois la copie hello et avant les autres utilisateurs soient remappés, uniquement hello connexion qui a initié hello copie, propriétaire de base de données hello, peut se connecter toohello nouvelle base de données.

toolearn sur la gestion des connexions et les utilisateurs lorsque vous copiez un base de données tooa autre serveur logique, consultez [toomanage SQL Azure base de sécurité après la récupération d’urgence](sql-database-geo-replication-security-config.md).

## <a name="next-steps"></a>Étapes suivantes

* Pour plus d’informations sur les connexions, consultez [gérer des connexions](sql-database-manage-logins.md) et [toomanage SQL Azure base de sécurité après la récupération d’urgence](sql-database-geo-replication-security-config.md).
* tooexport une base de données, consultez [exporter hello de base de données tooa BACPAC](sql-database-export.md).
