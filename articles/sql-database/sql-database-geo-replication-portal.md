---
title: "Portail Azure : géoréplication SQL Database | Microsoft Docs"
description: "Configurer les géo-réplication pour la base de données SQL Azure dans hello portail Azure et de basculement de lancement"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: d0b29822-714f-4633-a5ab-fb1a09d43ced
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/06/2016
ms.author: carlrab
ms.openlocfilehash: 09cbbdb040f36c42593e3be87ce6db2238f36656
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-in-hello-azure-portal-and-initiate-failover"></a>Configurer géo-réplication active pour base de données SQL Azure hello portail Azure et de basculement de lancement

Cet article vous montre comment tooconfigure géo-réplication active pour la base de données SQL dans hello [portail Azure](http://portal.azure.com) et tooinitiate le basculement.

basculement tooinitiate avec hello portail Azure, consultez [initier un basculement planifié ou non planifié pour la base de données SQL Azure avec hello portail Azure](sql-database-geo-replication-portal.md).

tooconfigure géo-réplication active à l’aide de hello portail Azure, vous devez hello suivant de ressource :

* Une base de données SQL Azure : base de données primaire hello que vous souhaitez tooa tooreplicate autre région géographique.

> [!Note]
Géo-réplication Active doit être entre bases de données Bonjour même abonnement.

## <a name="add-a-secondary-database"></a>Ajout d'une base de données secondaire
Hello étapes suivantes créent une nouvelle base de données secondaire dans un partenariat de géo-réplication.  

tooadd une base de données secondaire, vous devez être propriétaire de l’abonnement hello ou copropriétaire.

base de données secondaire Hello a hello même nom qu’une base de données primaire hello et a, par défaut, hello même niveau de service. base de données secondaire Hello peut être une base de données ou d’une base de données dans un pool élastique. Pour en savoir plus, consultez [Niveaux de service](sql-database-service-tiers.md).
Une fois hello secondaire est créée et amorcée, données commencent à se répliquer à partir de hello base de données primaire toohello nouvelle base de données secondaire.

> [!NOTE]
> Si la base de données partenaire hello existe déjà (par exemple, suite à l’arrêt d’une relation de géo-réplication précédente) commande hello échoue.
> 

1. Bonjour [portail Azure](http://portal.azure.com), parcourir toohello de base de données que vous souhaitez tooset pour géo-réplication.
2. Sur la page de base de données SQL hello, sélectionnez **géo-réplication**, puis sélectionnez hello région toocreate hello base de données secondaire. Vous pouvez sélectionner n’importe quelle région autre que de la région de hello hébergeant la base de données primaire hello, mais nous vous recommandons de hello [région associée](../best-practices-availability-paired-regions.md).
   
    ![Configuration de la géo-réplication](./media/sql-database-geo-replication-portal/configure-geo-replication.png)
3. Sélectionnez ou configurer le serveur de hello et niveau de tarification pour la base de données secondaire hello.
   
    ![Configuration de la base de données secondaire](./media/sql-database-geo-replication-portal/create-secondary.png)
4. Si vous le souhaitez, vous pouvez ajouter un pool élastique de base de données secondaire tooan. base de données secondaire toocreate hello dans un pool, cliquez sur **pool élastique** et sélectionnez un pool sur le serveur cible de hello. Un pool doit déjà exister sur le serveur cible de hello. Ce workflow ne crée pas un pool.
5. Cliquez sur **créer** hello tooadd secondaire.
6. base de données secondaire Hello est créé et hello amorçage processus commence.
   
    ![Configuration de la base de données secondaire](./media/sql-database-geo-replication-portal/seeding0.png)
7. Lorsque hello amorçage le processus est terminé, la base de données secondaire hello affiche son état.
   
    ![Amorçage terminé](./media/sql-database-geo-replication-portal/seeding-complete.png)

## <a name="initiate-a-failover"></a>Initialisation d’un basculement

base de données secondaire Hello peut être hello toobecome commuté principal.  

1. Bonjour [portail Azure](http://portal.azure.com), parcourir la base de données primaire toohello en partenariat de géo-réplication hello.
2. Dans le panneau de la base de données SQL hello, sélectionnez **tous les paramètres** > **géo-réplication**.
3. Bonjour **secondaires** liste, sélectionnez hello base de données toobecome hello nouveau réplica principal et cliquez sur **basculement**.
   
    ![Basculement](./media/sql-database-geo-replication-failover-portal/secondaries.png)
4. Cliquez sur **Oui** toobegin hello basculement.

commande Hello bascule immédiatement la base de données secondaire hello dans le rôle principal de hello. 

Il existe une courte période pendant laquelle les deux bases de données ne sont pas disponibles (dans l’ordre hello de 0 seconde too25) pendant le basculement des rôles de hello. Si la base de données primaire hello a plusieurs bases de données secondaires, commande hello automatiquement reconfigure hello autres bases de données secondaires tooconnect toohello nouveau réplica principal. toute l’opération Hello doit prendre moins d’une minute toocomplete dans des circonstances normales. 

> [!NOTE]
> Cette commande est conçue pour une récupération rapide de base de données hello en cas de panne. Elle déclenche un basculement sans synchronisation des données (basculement forcé).  Si hello principal est en ligne et la validation des transactions lors de la commande hello est émise une perte de données peut se produire. 
> 
> 

## <a name="remove-secondary-database"></a>Supprimer une base de données secondaire
Cette opération arrête définitivement de la base de données secondaire de toohello réplication hello et modifications hello le rôle de base de données en lecture-écriture régulière hello tooa secondaire. Si la base de données secondaire hello connectivité toohello est rompue, commande hello réussit mais hello est secondaire ne devient en lecture-écriture jusqu'à une fois que la connectivité est rétablie.  

1. Bonjour [portail Azure](http://portal.azure.com), parcourir la base de données primaire toohello en partenariat de géo-réplication hello.
2. Sur la page de base de données SQL hello, sélectionnez **géo-réplication**.
3. Bonjour **secondaires** liste, sélectionnez hello base de données tooremove à partir du partenariat de géo-réplication hello.
4. Cliquez sur **Arrêter la réplication**.
   
    ![Suppression de la base de données secondaire](./media/sql-database-geo-replication-portal/remove-secondary.png)
5. Une fenêtre de confirmation s’ouvre. Cliquez sur **Oui** tooremove hello base de données partenariat de géo-réplication hello. (Définissez la propriété en lecture-écriture de base de données ne fait pas partie de toute réplication tooa.)

## <a name="next-steps"></a>Étapes suivantes
* toolearn en savoir plus sur la géo-réplication active, consultez [géo-réplication active](sql-database-geo-replication-overview.md).
* Pour une vue d’ensemble de la continuité des activités et des scénarios, consultez [Vue d’ensemble de la continuité des activités](sql-database-business-continuity.md).

