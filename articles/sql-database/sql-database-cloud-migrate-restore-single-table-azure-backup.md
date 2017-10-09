---
title: "aaaRestore une seule table à partir de la sauvegarde de base de données SQL Azure | Documents Microsoft"
description: "Découvrez comment toorestore une seule table à partir de la sauvegarde de base de données SQL Azure."
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: 340b41bd-9df8-47fb-adfc-03216de38a5e
ms.service: sql-database
ms.custom: business continuity
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: 696d2ac87a70bccdf063bfecb8255723404aa5bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorestore-a-single-table-from-an-azure-sql-database-backup"></a>Comment toorestore une seule table à partir d’une sauvegarde de base de données SQL Azure
Vous pouvez rencontrer une situation dans laquelle vous avez modifié par inadvertance des données dans une base de données SQL, vous vous souhaitez toorecover hello seule affecté table. Cet article décrit comment toorestore une seule table dans une base de données à partir d’un de base de données SQL de hello [sauvegardes automatiques](sql-database-automated-backups.md).

## <a name="preparation-steps-rename-hello-table-and-restore-a-copy-of-hello-database"></a>Étapes de préparation : renommer la table de hello et restaurez une copie de base de données hello
1. Identifiez la table hello dans votre base de données SQL Azure que vous souhaitez tooreplace avec la copie de hello restaurée. Utilisez Microsoft SQL Management Studio toorename hello tableau. Par exemple, renommez la table hello en tant que &lt;nom de la table&gt;_old.
   
   > [!NOTE]
   > tooavoid bloqué, assurez-vous qu’il n’existe aucune activité en cours d’exécution sur la table hello que vous renommez. Si vous rencontrez des problèmes, veillez à effectuer cette procédure pendant une fenêtre de maintenance.
   >

2. Restaurer une sauvegarde de votre point de tooa de base de données dans le temps que vous souhaitez toorecover toousing hello [Point-In_Time restaurer](sql-database-recovery-using-backups.md#point-in-time-restore) étapes.
   
   > [!NOTE]
   > nom de Hello de base de données restaurée de hello doit être au format de DBName + TimeStamp hello ; par exemple, **Adventureworks2012_2016-01-01T22-12Z**. Nom de base de données existante hello sur le serveur de hello ne remplace pas cette étape. Il s’agit d’une mesure de sécurité, et il est envisagé tooallow hello de tooverify vous restauré la base de données avant de supprimer leur base de données actuelle et renommer la base de données hello restaurée pour la production.
   
## <a name="copying-hello-table-from-hello-restored-database-by-using-hello-sql-database-migration-tool"></a>Copie de la table à partir de hello hello restauré la base de données à l’aide de l’outil de Migration de base de données de SQL hello

1. Téléchargez et installez hello [l’Assistant Migration de base de données SQL](https://sqlazuremw.codeplex.com).
2. Ouvrez hello Assistant de Migration de base de données SQL, sur hello **sélectionner le processus** , sélectionnez **base de données dans les analyser/migrer**, puis cliquez sur **suivant**.

   ![Assistant Migration de la base de données SQL - Sélectionner un processus](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/1.png)

3. Bonjour **connecter tooServer** boîte de dialogue zone, appliquer hello suivant les paramètres :

   * Nom du serveur : **votre SQL server**
   * Authentification : **authentification SQL Server**
   * Connexion : **votre identifiant de connexion**
   * Mot de passe : **votre mot de passe**
   * Base de données : **Master DB (Liste toutes les bases de données)**
   
   > [!NOTE]
   > Assistant de hello enregistre vos informations de connexion par défaut. Si cela ne vous convient pas, sélectionnez **Oublier les informations de connexion**.
   >
   
     ![Assistant de Migration SQL Database - Sélectionner une source - étape 1](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/2.png)
4. Bonjour **sélectionner une Source** boîte de dialogue, le nom de base de données Sélectionnez hello restauré à partir de hello **étapes de préparation** section comme source, puis cliquez sur **suivant**.
   
    ![Assistant Migration de la base de données SQL - 	Sélectionner une source - étape 2](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/3.png)
5. Bonjour **choisir objets** boîte de dialogue, sélectionnez hello **sélectionner des objets de base de données spécifique** option et sélectionnez table(or tables) hello que vous souhaitez le serveur cible de toohello toomigrate.
   ![Assistant Migration de la base de données SQL - 	Sélectionner les objets](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)
6. Sur hello **résumé de l’Assistant Script** , cliquez sur **Oui** lorsque vous êtes invité à entrer indiquant si vous êtes prêt toogenerate un script SQL. Vous avez également toosave hello Script TSQL de hello option pour une utilisation ultérieure.
   ![Assistant Migration de la base de données SQL - 	Résumé de l’Assistant Script](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)
7. Sur hello **résumé des résultats** , cliquez sur **suivant**.
   ![Assistant Migration de la base de données SQL - 	Résumé des résultats](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)
8. Sur hello **connexion au serveur cible d’installation** , cliquez sur **connecter tooServer**, puis entrez les détails de hello comme suit :
   
   * **Nom du serveur**: instance de serveur cible
   * **Authentification** : **authentification SQL Server**. Entrez vos informations d’identification.
   * **Base de données** : **Master DB (Lister toutes les bases de données)**. Cette option répertorie toutes les bases de données hello sur le serveur cible de hello.
     
     ![Assistant Migration de la base de données SQL - 	Configurer la connexion au serveur cible](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/7.png)
9. Cliquez sur **Connect**, sélectionnez base de données hello cible que vous voulez toomove hello table, puis cliquez sur **suivant**. Cela doit terminer le script de hello généré précédemment en cours d’exécution, et vous devez voir hello vient d’être placé de base de données de table toohello copié cible.

## <a name="verification-step"></a>Étape de vérification

- Hello de requête et de test récemment copié toomake table assurant que les données de salutation sont intactes. Après confirmation, vous pouvez supprimer la forme de table hello renommé **étapes de préparation** section. (par exemple, &lt;nom de la table&gt;_old).

## <a name="next-steps"></a>Étapes suivantes
[Sauvegardes automatiques d’une base de données SQL](sql-database-automated-backups.md)

