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
# <a name="how-toorestore-a-single-table-from-an-azure-sql-database-backup"></a><span data-ttu-id="80915-103">Comment toorestore une seule table à partir d’une sauvegarde de base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="80915-103">How toorestore a single table from an Azure SQL Database backup</span></span>
<span data-ttu-id="80915-104">Vous pouvez rencontrer une situation dans laquelle vous avez modifié par inadvertance des données dans une base de données SQL, vous vous souhaitez toorecover hello seule affecté table.</span><span class="sxs-lookup"><span data-stu-id="80915-104">You may encounter a situation in which you accidentally modified some data in a SQL database and now you want toorecover hello single affected table.</span></span> <span data-ttu-id="80915-105">Cet article décrit comment toorestore une seule table dans une base de données à partir d’un de base de données SQL de hello [sauvegardes automatiques](sql-database-automated-backups.md).</span><span class="sxs-lookup"><span data-stu-id="80915-105">This article describes how toorestore a single table in a database from one of hello SQL Database [automatic backups](sql-database-automated-backups.md).</span></span>

## <a name="preparation-steps-rename-hello-table-and-restore-a-copy-of-hello-database"></a><span data-ttu-id="80915-106">Étapes de préparation : renommer la table de hello et restaurez une copie de base de données hello</span><span class="sxs-lookup"><span data-stu-id="80915-106">Preparation steps: Rename hello table and restore a copy of hello database</span></span>
1. <span data-ttu-id="80915-107">Identifiez la table hello dans votre base de données SQL Azure que vous souhaitez tooreplace avec la copie de hello restaurée.</span><span class="sxs-lookup"><span data-stu-id="80915-107">Identify hello table in your Azure SQL database that you want tooreplace with hello restored copy.</span></span> <span data-ttu-id="80915-108">Utilisez Microsoft SQL Management Studio toorename hello tableau.</span><span class="sxs-lookup"><span data-stu-id="80915-108">Use Microsoft SQL Management Studio toorename hello table.</span></span> <span data-ttu-id="80915-109">Par exemple, renommez la table hello en tant que &lt;nom de la table&gt;_old.</span><span class="sxs-lookup"><span data-stu-id="80915-109">For example, rename hello table as &lt;table name&gt;_old.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="80915-110">tooavoid bloqué, assurez-vous qu’il n’existe aucune activité en cours d’exécution sur la table hello que vous renommez.</span><span class="sxs-lookup"><span data-stu-id="80915-110">tooavoid being blocked, make sure that there's no activity running on hello table that you are renaming.</span></span> <span data-ttu-id="80915-111">Si vous rencontrez des problèmes, veillez à effectuer cette procédure pendant une fenêtre de maintenance.</span><span class="sxs-lookup"><span data-stu-id="80915-111">If you encounter issues, make sure that perform this procedure during a maintenance window.</span></span>
   >

2. <span data-ttu-id="80915-112">Restaurer une sauvegarde de votre point de tooa de base de données dans le temps que vous souhaitez toorecover toousing hello [Point-In_Time restaurer](sql-database-recovery-using-backups.md#point-in-time-restore) étapes.</span><span class="sxs-lookup"><span data-stu-id="80915-112">Restore a backup of your database tooa point in time that you want toorecover toousing hello [Point-In_Time Restore](sql-database-recovery-using-backups.md#point-in-time-restore) steps.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="80915-113">nom de Hello de base de données restaurée de hello doit être au format de DBName + TimeStamp hello ; par exemple, **Adventureworks2012_2016-01-01T22-12Z**.</span><span class="sxs-lookup"><span data-stu-id="80915-113">hello name of hello restored database will be in hello DBName+TimeStamp format; for example, **Adventureworks2012_2016-01-01T22-12Z**.</span></span> <span data-ttu-id="80915-114">Nom de base de données existante hello sur le serveur de hello ne remplace pas cette étape.</span><span class="sxs-lookup"><span data-stu-id="80915-114">This step doesn't overwrite hello existing database name on hello server.</span></span> <span data-ttu-id="80915-115">Il s’agit d’une mesure de sécurité, et il est envisagé tooallow hello de tooverify vous restauré la base de données avant de supprimer leur base de données actuelle et renommer la base de données hello restaurée pour la production.</span><span class="sxs-lookup"><span data-stu-id="80915-115">This is a safety measure, and it's intended tooallow you tooverify hello restored database before they drop their current database and rename hello restored database for production use.</span></span>
   
## <a name="copying-hello-table-from-hello-restored-database-by-using-hello-sql-database-migration-tool"></a><span data-ttu-id="80915-116">Copie de la table à partir de hello hello restauré la base de données à l’aide de l’outil de Migration de base de données de SQL hello</span><span class="sxs-lookup"><span data-stu-id="80915-116">Copying hello table from hello restored database by using hello SQL Database Migration tool</span></span>

1. <span data-ttu-id="80915-117">Téléchargez et installez hello [l’Assistant Migration de base de données SQL](https://sqlazuremw.codeplex.com).</span><span class="sxs-lookup"><span data-stu-id="80915-117">Download and install hello [SQL Database Migration Wizard](https://sqlazuremw.codeplex.com).</span></span>
2. <span data-ttu-id="80915-118">Ouvrez hello Assistant de Migration de base de données SQL, sur hello **sélectionner le processus** , sélectionnez **base de données dans les analyser/migrer**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="80915-118">Open hello SQL Database Migration Wizard, on hello **Select Process** page, select **Database under Analyze/Migrate**, and then click **Next**.</span></span>

   ![Assistant Migration de la base de données SQL - Sélectionner un processus](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/1.png)

3. <span data-ttu-id="80915-120">Bonjour **connecter tooServer** boîte de dialogue zone, appliquer hello suivant les paramètres :</span><span class="sxs-lookup"><span data-stu-id="80915-120">In hello **Connect tooServer** dialog box, apply hello following settings:</span></span>

   * <span data-ttu-id="80915-121">Nom du serveur : **votre SQL server**</span><span class="sxs-lookup"><span data-stu-id="80915-121">Server name: **Your SQL server**</span></span>
   * <span data-ttu-id="80915-122">Authentification : **authentification SQL Server**</span><span class="sxs-lookup"><span data-stu-id="80915-122">Authentication: **SQL Server Authentication**</span></span>
   * <span data-ttu-id="80915-123">Connexion : **votre identifiant de connexion**</span><span class="sxs-lookup"><span data-stu-id="80915-123">Login: **Your login**</span></span>
   * <span data-ttu-id="80915-124">Mot de passe : **votre mot de passe**</span><span class="sxs-lookup"><span data-stu-id="80915-124">Password: **Your password**</span></span>
   * <span data-ttu-id="80915-125">Base de données : **Master DB (Liste toutes les bases de données)**</span><span class="sxs-lookup"><span data-stu-id="80915-125">Database: **Master DB (List all databases)**</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="80915-126">Assistant de hello enregistre vos informations de connexion par défaut.</span><span class="sxs-lookup"><span data-stu-id="80915-126">By default hello wizard saves your login information.</span></span> <span data-ttu-id="80915-127">Si cela ne vous convient pas, sélectionnez **Oublier les informations de connexion**.</span><span class="sxs-lookup"><span data-stu-id="80915-127">If you don't want it to, select **Forget Login Information**.</span></span>
   >
   
     ![Assistant de Migration SQL Database - Sélectionner une source - étape 1](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/2.png)
4. <span data-ttu-id="80915-129">Bonjour **sélectionner une Source** boîte de dialogue, le nom de base de données Sélectionnez hello restauré à partir de hello **étapes de préparation** section comme source, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="80915-129">In hello **Select Source** dialog box, select hello restored database name from hello **Preparation steps** section as your source, and then click **Next**.</span></span>
   
    ![Assistant Migration de la base de données SQL - 	Sélectionner une source - étape 2](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/3.png)
5. <span data-ttu-id="80915-131">Bonjour **choisir objets** boîte de dialogue, sélectionnez hello **sélectionner des objets de base de données spécifique** option et sélectionnez table(or tables) hello que vous souhaitez le serveur cible de toohello toomigrate.</span><span class="sxs-lookup"><span data-stu-id="80915-131">In hello **Choose Objects** dialog box, select hello **Select specific database objects** option, and then select hello table(or tables) that you want toomigrate toohello target server.</span></span>
   <span data-ttu-id="80915-132">![Assistant Migration de la base de données SQL - 	Sélectionner les objets](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)</span><span class="sxs-lookup"><span data-stu-id="80915-132">![SQL Database Migration wizard - Choose Objects](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)</span></span>
6. <span data-ttu-id="80915-133">Sur hello **résumé de l’Assistant Script** , cliquez sur **Oui** lorsque vous êtes invité à entrer indiquant si vous êtes prêt toogenerate un script SQL.</span><span class="sxs-lookup"><span data-stu-id="80915-133">On hello **Script Wizard Summary** page, click **Yes** when you’re prompted about whether you’re ready toogenerate a SQL script.</span></span> <span data-ttu-id="80915-134">Vous avez également toosave hello Script TSQL de hello option pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="80915-134">You also have hello option toosave hello TSQL Script for later use.</span></span>
   <span data-ttu-id="80915-135">![Assistant Migration de la base de données SQL - 	Résumé de l’Assistant Script](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)</span><span class="sxs-lookup"><span data-stu-id="80915-135">![SQL Database Migration wizard - Script Wizard Summary](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)</span></span>
7. <span data-ttu-id="80915-136">Sur hello **résumé des résultats** , cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="80915-136">On hello **Results Summary** page, click **Next**.</span></span>
   <span data-ttu-id="80915-137">![Assistant Migration de la base de données SQL - 	Résumé des résultats](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)</span><span class="sxs-lookup"><span data-stu-id="80915-137">![SQL Database Migration wizard - Results Summary](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)</span></span>
8. <span data-ttu-id="80915-138">Sur hello **connexion au serveur cible d’installation** , cliquez sur **connecter tooServer**, puis entrez les détails de hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="80915-138">On hello **Setup Target Server Connection** page, click **Connect tooServer**, and then enter hello details as follows:</span></span>
   
   * <span data-ttu-id="80915-139">**Nom du serveur**: instance de serveur cible</span><span class="sxs-lookup"><span data-stu-id="80915-139">**Server Name**: Target server instance</span></span>
   * <span data-ttu-id="80915-140">**Authentification** : **authentification SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="80915-140">**Authentication**: **SQL Server authentication**.</span></span> <span data-ttu-id="80915-141">Entrez vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="80915-141">Enter your login credentials.</span></span>
   * <span data-ttu-id="80915-142">**Base de données** : **Master DB (Lister toutes les bases de données)**.</span><span class="sxs-lookup"><span data-stu-id="80915-142">**Database**: **Master DB (List all databases)**.</span></span> <span data-ttu-id="80915-143">Cette option répertorie toutes les bases de données hello sur le serveur cible de hello.</span><span class="sxs-lookup"><span data-stu-id="80915-143">This option lists all hello databases on hello target server.</span></span>
     
     ![Assistant Migration de la base de données SQL - 	Configurer la connexion au serveur cible](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/7.png)
9. <span data-ttu-id="80915-145">Cliquez sur **Connect**, sélectionnez base de données hello cible que vous voulez toomove hello table, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="80915-145">Click **Connect**, select hello target database that you want toomove hello table to, and then click **Next**.</span></span> <span data-ttu-id="80915-146">Cela doit terminer le script de hello généré précédemment en cours d’exécution, et vous devez voir hello vient d’être placé de base de données de table toohello copié cible.</span><span class="sxs-lookup"><span data-stu-id="80915-146">This should finish running hello previously generated script, and you should see hello newly moved table copied toohello target database.</span></span>

## <a name="verification-step"></a><span data-ttu-id="80915-147">Étape de vérification</span><span class="sxs-lookup"><span data-stu-id="80915-147">Verification step</span></span>

- <span data-ttu-id="80915-148">Hello de requête et de test récemment copié toomake table assurant que les données de salutation sont intactes.</span><span class="sxs-lookup"><span data-stu-id="80915-148">Query and test hello newly copied table toomake sure that hello data is intact.</span></span> <span data-ttu-id="80915-149">Après confirmation, vous pouvez supprimer la forme de table hello renommé **étapes de préparation** section.</span><span class="sxs-lookup"><span data-stu-id="80915-149">Upon confirmation, you can drop hello renamed table form **Preparation steps** section.</span></span> <span data-ttu-id="80915-150">(par exemple, &lt;nom de la table&gt;_old).</span><span class="sxs-lookup"><span data-stu-id="80915-150">(for example, &lt;table name&gt;_old).</span></span>

## <a name="next-steps"></a><span data-ttu-id="80915-151">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="80915-151">Next steps</span></span>
[<span data-ttu-id="80915-152">Sauvegardes automatiques d’une base de données SQL</span><span class="sxs-lookup"><span data-stu-id="80915-152">SQL Database automatic backups</span></span>](sql-database-automated-backups.md)

