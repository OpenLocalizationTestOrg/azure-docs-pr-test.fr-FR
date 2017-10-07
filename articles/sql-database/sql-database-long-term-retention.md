---
title: "aaaStore les sauvegardes de base de données SQL Azure pour les années de too10 | Documents Microsoft"
description: "Découvrez comment Azure SQL Database prend en charge le stockage des sauvegardes pour les années de too10."
keywords: 
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: 
ms.assetid: 66fdb8b8-5903-4d3a-802e-af08d204566e
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 12/22/2016
ms.author: sashan
ms.openlocfilehash: 5825ebd4e3bd66b59b13aea603d377ef814a1df3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="store-azure-sql-database-backups-for-up-too10-years"></a><span data-ttu-id="f2dd9-103">Stocker les sauvegardes de base de données SQL Azure pour les années de too10</span><span class="sxs-lookup"><span data-stu-id="f2dd9-103">Store Azure SQL Database backups for up too10 years</span></span>
<span data-ttu-id="f2dd9-104">De nombreuses applications ont réglementaires, de conformité ou autres activités à des fins qui nécessitent que des sauvegardes de base de données tooretain au-delà de hello jours 7-35 fournies par la base de données SQL Azure [sauvegardes automatiques](sql-database-automated-backups.md).</span><span class="sxs-lookup"><span data-stu-id="f2dd9-104">Many applications have regulatory, compliance, or other business purposes that require you tooretain database backups beyond hello 7-35 days provided by Azure SQL Database [automatic backups](sql-database-automated-backups.md).</span></span> <span data-ttu-id="f2dd9-105">En utilisant la fonctionnalité de rétention de sauvegarde à long terme hello, vous pouvez stocker vos sauvegardes de base de données SQL dans un coffre Azure Recovery Services pour les années de too10.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-105">By using hello long-term backup retention feature, you can store your SQL database backups in an Azure Recovery Services vault for up too10 years.</span></span> <span data-ttu-id="f2dd9-106">Vous pouvez de stocker jusqu'à too1, 000 bases de données par le coffre.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-106">You can store up too1,000 databases per vault.</span></span> <span data-ttu-id="f2dd9-107">Vous pouvez ensuite sélectionner n’importe quelle sauvegarde dans hello coffre toorestore sous la forme d’une base de données.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-107">You then can select any backup in hello vault toorestore it as a new database.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f2dd9-108">Rétention de sauvegarde à long terme est actuellement en version préliminaire et disponible dans hello suivant régions : est de l’Australie, Sud-est de l’Australie, sud du Brésil, du centre des États-Unis, Asie orientale, est des États-Unis, est des États-Unis 2, Inde centrale, sud de l’Inde, est du Japon, ouest du Japon, Amérique du Nord, du Nord Europe du Sud-Centre des États-Unis, Asie du Sud-est, Europe de l’ouest et ouest des États-Unis.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-108">Long-term backup retention is currently in preview and available in hello following regions: Australia East, Australia Southeast, Brazil South, Central US, East Asia, East US, East US 2, India Central, India South, Japan East, Japan West, North Central US, North Europe, South Central US, Southeast Asia, West Europe, and West US.</span></span>
>

> [!NOTE]
> <span data-ttu-id="f2dd9-109">Vous pouvez activer des bases de données too200 par coffre pendant une période de 24 heures.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-109">You can enable up too200 databases per vault during a 24-hour period.</span></span> <span data-ttu-id="f2dd9-110">Nous vous recommandons d’utiliser un coffre distinct pour chaque impact sur le serveur toominimize hello de cette limite.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-110">We recommend that you use a separate vault for each server toominimize hello impact of this limit.</span></span> 
> 

## <a name="how-sql-database-long-term-backup-retention-works"></a><span data-ttu-id="f2dd9-111">Comment fonctionne la rétention de sauvegarde SQL Database à long terme</span><span class="sxs-lookup"><span data-stu-id="f2dd9-111">How SQL Database long-term backup retention works</span></span>

<span data-ttu-id="f2dd9-112">Avec la rétention à long terme des sauvegardes, vous pouvez associer un serveur de base de données SQL à un coffre Azure Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-112">With long-term backup retention, you can associate a SQL database server with an Azure Recovery Services vault.</span></span> 

* <span data-ttu-id="f2dd9-113">Vous devez créer le coffre de hello en hello même abonnement Azure créé hello SQL serveur et dans hello même groupe de ressources et de la région géographique.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-113">You must create hello vault in hello same Azure subscription that created hello SQL server and in hello same geographic region and resource group.</span></span> 
* <span data-ttu-id="f2dd9-114">Vous configurez ensuite une stratégie de rétention pour une base de données quelconque.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-114">You then configure a retention policy for any database.</span></span> <span data-ttu-id="f2dd9-115">Hello stratégie causes hello hebdomadaire de la base de données complète des sauvegardes toobe copié le coffre Recovery Services toohello et conservées pendant la période de rétention spécifiée hello (haut too10 ans).</span><span class="sxs-lookup"><span data-stu-id="f2dd9-115">hello policy causes hello weekly full database backups toobe copied toohello Recovery Services vault and retained for hello specified retention period (up too10 years).</span></span> 
* <span data-ttu-id="f2dd9-116">Vous pouvez ensuite restaurer la base de données hello à partir d’un de ces sauvegardes tooa nouvelle base de données dans n’importe quel serveur dans l’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-116">You can then restore hello database from any of these backups tooa new database in any server in hello subscription.</span></span> <span data-ttu-id="f2dd9-117">Le stockage Azure crée une copie à partir de sauvegardes existants, et copie de hello n’a aucun impact sur les performances sur la base de données existante hello.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-117">Azure storage creates a copy from existing backups, and hello copy has no performance impact on hello existing database.</span></span>

> [!TIP]
> <span data-ttu-id="f2dd9-118">Pour une procédure-tooguide, consultez [configurer et restauration à partir de la rétention de sauvegarde à long terme de base de données SQL Azure](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f2dd9-118">For a how-tooguide, see [Configure and restore from Azure SQL Database long-term backup retention](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="enable-long-term-backup-retention"></a><span data-ttu-id="f2dd9-119">Activer la rétention des sauvegardes à long terme</span><span class="sxs-lookup"><span data-stu-id="f2dd9-119">Enable long-term backup retention</span></span>

<span data-ttu-id="f2dd9-120">rétention de sauvegarde à long terme tooconfigure pour une base de données :</span><span class="sxs-lookup"><span data-stu-id="f2dd9-120">tooconfigure long-term backup retention for a database:</span></span>

1. <span data-ttu-id="f2dd9-121">Créer un coffre Azure Recovery Services Bonjour même groupe de région, les abonnements et les ressources que votre serveur de base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-121">Create an Azure Recovery Services vault in hello same region, subscription, and resource group as your SQL database server.</span></span> 
2. <span data-ttu-id="f2dd9-122">Inscrire un coffre-fort toohello hello.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-122">Register hello server toohello vault.</span></span>
3. <span data-ttu-id="f2dd9-123">Créez une stratégie de protection Azure Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-123">Create an Azure Recovery Services protection policy.</span></span>
4. <span data-ttu-id="f2dd9-124">Appliquer hello protection stratégie toohello bases de données qui nécessitent la rétention de sauvegarde à long terme.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-124">Apply hello protection policy toohello databases that require long-term backup retention.</span></span>

<span data-ttu-id="f2dd9-125">tooconfigure, gérer et restaurer une base de données à partir de la rétention de sauvegarde à long terme des sauvegardes automatisées dans un coffre Azure Recovery Services, effectuez une des manières suivantes les hello :</span><span class="sxs-lookup"><span data-stu-id="f2dd9-125">tooconfigure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault, do either of hello following:</span></span>

* <span data-ttu-id="f2dd9-126">À l’aide de hello portail Azure : cliquez sur **rétention de sauvegarde à long terme**, sélectionnez une base de données, puis cliquez sur **configurer**.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-126">Using hello Azure portal: Click **Long-term backup retention**, select a database, and then click **Configure**.</span></span> 

   ![Sélectionner une base de données pour la rétention des sauvegardes à long terme](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

* <span data-ttu-id="f2dd9-128">À l’aide de PowerShell : Accédez trop[configurer et restauration à partir de la rétention de sauvegarde à long terme de base de données SQL Azure](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f2dd9-128">Using PowerShell: Go too[Configure and restore from Azure SQL Database long-term backup retention](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="restore-a-database-thats-stored-with-hello-long-term-backup-retention-feature"></a><span data-ttu-id="f2dd9-129">Restaurer une base de données qui est stockée avec la fonctionnalité de rétention de sauvegarde à long terme hello</span><span class="sxs-lookup"><span data-stu-id="f2dd9-129">Restore a database that's stored with hello long-term backup retention feature</span></span>

<span data-ttu-id="f2dd9-130">toorecover à partir d’une sauvegarde à long terme de la rétention de sauvegarde :</span><span class="sxs-lookup"><span data-stu-id="f2dd9-130">toorecover from a long-term backup retention backup:</span></span>

1. <span data-ttu-id="f2dd9-131">Coffre de hello liste où la sauvegarde de hello est stocké.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-131">List hello vault where hello backup is stored.</span></span>
2. <span data-ttu-id="f2dd9-132">Conteneur de hello de liste qui est mappé tooyour logique.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-132">List hello container that is mapped tooyour logical server.</span></span>
3. <span data-ttu-id="f2dd9-133">Source de données liste hello dans le coffre hello qui est mappé tooyour de base de données.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-133">List hello data source within hello vault that is mapped tooyour database.</span></span>
4. <span data-ttu-id="f2dd9-134">Liste hello points de récupération sont toorestore disponible.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-134">List hello recovery points that are available toorestore.</span></span>
5. <span data-ttu-id="f2dd9-135">Restaurer la base de données de hello à partir de serveur de cible de toohello de point de récupération hello dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-135">Restore hello database from hello recovery point toohello target server within your subscription.</span></span>

<span data-ttu-id="f2dd9-136">tooconfigure, gérer et restaurer une base de données à partir de la rétention de sauvegarde à long terme des sauvegardes automatisées dans un coffre Azure Recovery Services, effectuez une des manières suivantes les hello :</span><span class="sxs-lookup"><span data-stu-id="f2dd9-136">tooconfigure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault, do either of hello following:</span></span>

* <span data-ttu-id="f2dd9-137">À l’aide de hello portail Azure : accédez trop[gérer à long terme rétention de sauvegarde à l’aide de hello Azure portal](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f2dd9-137">Using hello Azure portal: Go too[Manage long-term backup retention using hello Azure portal](sql-database-long-term-backup-retention-configure.md).</span></span> 

* <span data-ttu-id="f2dd9-138">À l’aide de PowerShell : Accédez trop[gérer la rétention de sauvegarde à long terme à l’aide de PowerShell](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f2dd9-138">Using PowerShell: Go too[Manage long-term backup retention using PowerShell](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="get-pricing-for-long-term-backup-retention"></a><span data-ttu-id="f2dd9-139">Obtenir les prix de la rétention des sauvegardes à long terme</span><span class="sxs-lookup"><span data-stu-id="f2dd9-139">Get pricing for long-term backup retention</span></span>

<span data-ttu-id="f2dd9-140">Rétention à long terme des sauvegardes de base de données SQL est facturée en fonction de toohello [service sauvegarde Azure tarification taux](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="f2dd9-140">Long-term backup retention of a SQL database is charged according toohello [Azure backup services pricing rates](https://azure.microsoft.com/pricing/details/backup/).</span></span>

<span data-ttu-id="f2dd9-141">Une fois le serveur de base de données SQL hello toohello inscrits coffre, vous êtes facturé pour le stockage total hello qui est utilisé par les sauvegardes hebdomadaires hello stockées dans le coffre hello.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-141">After hello SQL database server is registered toohello vault, you are charged for hello total storage that's used by hello weekly backups stored in hello vault.</span></span>

## <a name="view-available-backups-that-are-stored-in-long-term-backup-retention"></a><span data-ttu-id="f2dd9-142">Afficher les sauvegardes disponibles qui sont stockées avec rétention à long terme</span><span class="sxs-lookup"><span data-stu-id="f2dd9-142">View available backups that are stored in long-term backup retention</span></span>

<span data-ttu-id="f2dd9-143">tooconfigure, gérer et restaurer une base de données à partir de la rétention de sauvegarde à long terme des sauvegardes automatisées dans un coffre Azure Recovery Services à l’aide de hello portail Azure, effectuez une des manières suivantes les hello :</span><span class="sxs-lookup"><span data-stu-id="f2dd9-143">tooconfigure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault by using hello Azure portal, do either of hello following:</span></span>

* <span data-ttu-id="f2dd9-144">À l’aide de hello portail Azure : accédez trop[gérer à long terme rétention de sauvegarde à l’aide de hello Azure portal](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f2dd9-144">Using hello Azure portal: Go too[Manage long-term backup retention using hello Azure portal](sql-database-long-term-backup-retention-configure.md).</span></span> 

* <span data-ttu-id="f2dd9-145">À l’aide de PowerShell : Accédez trop[gérer la rétention de sauvegarde à long terme à l’aide de PowerShell](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f2dd9-145">Using PowerShell: Go too[Manage long-term backup retention using PowerShell](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="disable-long-term-retention"></a><span data-ttu-id="f2dd9-146">Désactiver la rétention à long terme</span><span class="sxs-lookup"><span data-stu-id="f2dd9-146">Disable long-term retention</span></span>

<span data-ttu-id="f2dd9-147">le service de récupération Hello gère automatiquement le nettoyage hello de hello fourni la stratégie de rétention des sauvegardes.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-147">hello recovery service automatically handles hello cleanup of backups based on hello provided retention policy.</span></span> 

<span data-ttu-id="f2dd9-148">les sauvegardes hello envoi toostop pour un coffre toohello de la base de données spécifique, supprimer la stratégie de rétention de hello pour cette base de données.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-148">toostop sending hello backups for a specific database toohello vault, remove hello retention policy for that database.</span></span>
  
```
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName 'RG1' -ServerName 'Server1' -DatabaseName 'DB1' -State 'Disabled' -ResourceId $policy.Id
```

> [!NOTE]
> <span data-ttu-id="f2dd9-149">les sauvegardes Hello qui se trouvent déjà dans le coffre hello ne sont pas affectés.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-149">hello backups that are already in hello vault are unaffected.</span></span> <span data-ttu-id="f2dd9-150">Ils sont automatiquement supprimés par le service de récupération hello lorsque leur période de rétention expire.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-150">They are automatically deleted by hello recovery service when their retention period expires.</span></span>

## <a name="long-term-backup-retention-faq"></a><span data-ttu-id="f2dd9-151">Questions fréquentes (FAQ) sur la rétention des sauvegardes à long terme</span><span class="sxs-lookup"><span data-stu-id="f2dd9-151">Long-term backup retention FAQ</span></span>

<span data-ttu-id="f2dd9-152">**Puis-je supprimer manuellement des sauvegardes spécifiques dans le coffre hello ?**</span><span class="sxs-lookup"><span data-stu-id="f2dd9-152">**Can I manually delete specific backups in hello vault?**</span></span>

<span data-ttu-id="f2dd9-153">Pas actuellement.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-153">Not currently.</span></span> <span data-ttu-id="f2dd9-154">coffre de Hello nettoie automatiquement les sauvegardes lors de la période de rétention hello a expiré.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-154">hello vault automatically cleans up backups when hello retention period has expired.</span></span>

<span data-ttu-id="f2dd9-155">**Puis-je enregistrer mon toomore de sauvegardes toostore serveur à un coffre-fort ?**</span><span class="sxs-lookup"><span data-stu-id="f2dd9-155">**Can I register my server toostore backups toomore than one vault?**</span></span>

<span data-ttu-id="f2dd9-156">Non, vous pouvez stocker actuellement un coffre-fort de sauvegardes tooonly à la fois.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-156">No, you can currently store backups tooonly one vault at a time.</span></span>

<span data-ttu-id="f2dd9-157">**Puis-je avoir un serveur et un coffre dans différents abonnements ?**</span><span class="sxs-lookup"><span data-stu-id="f2dd9-157">**Can I have a vault and server in different subscriptions?**</span></span>

<span data-ttu-id="f2dd9-158">Non, actuellement le coffre hello et le serveur doivent être Bonjour même groupe d’abonnement et de ressources.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-158">No, currently hello vault and server must be in hello same subscription and resource group.</span></span>

<span data-ttu-id="f2dd9-159">**Puis-je utiliser un coffre que j’ai créé dans une région qui est différente de celle de mon serveur ?**</span><span class="sxs-lookup"><span data-stu-id="f2dd9-159">**Can I use a vault that I created in a region that's different from my server’s region?**</span></span>

<span data-ttu-id="f2dd9-160">Non, le coffre hello et le serveur doivent être Bonjour même région toominimize copier du temps et éviter les frais liés au trafic.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-160">No, hello vault and server must be in hello same region toominimize copy time and avoid traffic charges.</span></span>

<span data-ttu-id="f2dd9-161">**Combien de bases de données puis-je stocker dans un coffre ?**</span><span class="sxs-lookup"><span data-stu-id="f2dd9-161">**How many databases can I store in one vault?**</span></span>

<span data-ttu-id="f2dd9-162">Actuellement, nous prenons en charge des too1, 000 bases de données par le coffre.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-162">Currently, we support up too1,000 databases per vault.</span></span> 

<span data-ttu-id="f2dd9-163">**Combien de coffres puis-je créer par abonnement ?**</span><span class="sxs-lookup"><span data-stu-id="f2dd9-163">**How many vaults can I create per subscription?**</span></span>

<span data-ttu-id="f2dd9-164">Vous pouvez créer des coffres too25 par abonnement.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-164">You can create up too25 vaults per subscription.</span></span>

<span data-ttu-id="f2dd9-165">**Combien de bases de données puis-je configurer par jour par coffre ?**</span><span class="sxs-lookup"><span data-stu-id="f2dd9-165">**How many databases can I configure per day per vault?**</span></span>

<span data-ttu-id="f2dd9-166">Vous pouvez configurer jusqu’à 200 bases de données par jour par coffre.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-166">You can set up 200 databases per day per vault.</span></span>

<span data-ttu-id="f2dd9-167">**La rétention de sauvegarde à long terme fonctionne-t-elle avec des pools élastiques ?**</span><span class="sxs-lookup"><span data-stu-id="f2dd9-167">**Does long-term backup retention work with elastic pools?**</span></span>

<span data-ttu-id="f2dd9-168">Oui.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-168">Yes.</span></span> <span data-ttu-id="f2dd9-169">Une base de données dans le pool de hello peut être configuré avec la stratégie de rétention hello.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-169">Any database in hello pool can be configured with hello retention policy.</span></span>

<span data-ttu-id="f2dd9-170">**Puis-je choisir temps hello création de sauvegarde de hello ?**</span><span class="sxs-lookup"><span data-stu-id="f2dd9-170">**Can I choose hello time at which hello backup is created?**</span></span>

<span data-ttu-id="f2dd9-171">Non, la base de données SQL contrôle hello planification de sauvegarde toominimize hello impact sur les performances de vos bases de données.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-171">No, SQL Database controls hello backup schedule toominimize hello performance impact on your databases.</span></span>

<span data-ttu-id="f2dd9-172">**Transparent Data Encryption est activé pour ma base de données. Puis-je utiliser avec le coffre de hello ?**</span><span class="sxs-lookup"><span data-stu-id="f2dd9-172">**I have transparent data encryption enabled for my database. Can I use it with hello vault?**</span></span> 

<span data-ttu-id="f2dd9-173">Oui, Transparent Data Encryption est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-173">Yes, transparent data encryption is supported.</span></span> <span data-ttu-id="f2dd9-174">Vous pouvez restaurer la base de données hello du coffre de hello même si la base de données d’origine hello n’existe plus.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-174">You can restore hello database from hello vault even if hello original database no longer exists.</span></span>

<span data-ttu-id="f2dd9-175">**Que se passe-t-il avec des sauvegardes dans le coffre hello hello si mon abonnement est suspendu ?**</span><span class="sxs-lookup"><span data-stu-id="f2dd9-175">**What happens with hello backups in hello vault if my subscription is suspended?**</span></span> 

<span data-ttu-id="f2dd9-176">Si votre abonnement est suspendu, nous conserver les sauvegardes et les bases de données existantes hello.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-176">If your subscription is suspended, we retain hello existing databases and backups.</span></span> <span data-ttu-id="f2dd9-177">Nouvelles sauvegardes ne sont pas copiés toohello coffre.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-177">New backups are not copied toohello vault.</span></span> <span data-ttu-id="f2dd9-178">Après la réactivation d’abonnement de hello, service de hello reprend coffre toohello de sauvegardes de copie.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-178">After you reactivate hello subscription, hello service resumes copying backups toohello vault.</span></span> <span data-ttu-id="f2dd9-179">Votre archivage devenue accessible toohello les opérations de restauration à l’aide de sauvegardes hello qui ont été copiés il avant hello abonnement a été suspendu.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-179">Your vault becomes accessible toohello restore operations by using hello backups that were copied there before hello subscription was suspended.</span></span> 

<span data-ttu-id="f2dd9-180">**Puis-je accéder aux fichiers de sauvegarde de base de données SQL toohello donc je peux télécharger ou les restaurer toohello SQL server ?**</span><span class="sxs-lookup"><span data-stu-id="f2dd9-180">**Can I get access toohello SQL database backup files so I can download or restore them toohello SQL server?**</span></span>

<span data-ttu-id="f2dd9-181">Non, pas actuellement.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-181">No, not currently.</span></span>

<span data-ttu-id="f2dd9-182">**Il est possible de toohave plusieurs planifications (quotidienne, hebdomadaire, mensuelle, annuelle) au sein d’une stratégie de rétention SQL.**</span><span class="sxs-lookup"><span data-stu-id="f2dd9-182">**Is it possible toohave multiple schedules (daily, weekly, monthly, yearly) within a SQL retention policy.**</span></span>

<span data-ttu-id="f2dd9-183">Non. Les planifications multiples sont prises en charge uniquement pour les sauvegardes de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-183">No, multiple schedules are currently available only for virtual machine backups.</span></span>

<span data-ttu-id="f2dd9-184">**Que se passe-t-il si nous configurons la rétention à long terme de la sauvegarde sur une base de données qui est une base de données de géoréplication active secondaire ?**</span><span class="sxs-lookup"><span data-stu-id="f2dd9-184">**What if we set up long-term backup retention on a database that is an active geo-replication secondary database?**</span></span>

<span data-ttu-id="f2dd9-185">Comme nous ne prenons pas en charge les sauvegardes sur des réplicas, il n’existe aucune option de rétention de sauvegarde à long terme sur les bases de données secondaires.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-185">Because we don't take backups on replicas, there is currently no option for long-term backup retention on secondary databases.</span></span> <span data-ttu-id="f2dd9-186">Toutefois, il est important pour les utilisateurs des tooset de rétention de sauvegarde à long terme sur une base de données secondaires géo-réplication active pour ces raisons :</span><span class="sxs-lookup"><span data-stu-id="f2dd9-186">However, it is important for users tooset up long-term backup retention on an active geo-replication secondary database for these reasons:</span></span>
* <span data-ttu-id="f2dd9-187">Lorsqu’un basculement a lieu et base de données hello devient une base de données primaire, nous effectuer une sauvegarde complète, qui est téléchargé toovault.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-187">When a failover happens and hello database becomes a primary database, we take a full backup, which is uploaded toovault.</span></span>
* <span data-ttu-id="f2dd9-188">Il n’existe pas d’autres clients de toohello de coût pour configurer la rétention des sauvegardes à long terme sur une base de données secondaire.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-188">There is no extra cost toohello customer for setting up long-term backup retention on a secondary database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2dd9-189">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f2dd9-189">Next steps</span></span>
<span data-ttu-id="f2dd9-190">Dans la mesure où les sauvegardes de base de données protègent les données des corruptions et des suppressions accidentelles, elles sont une partie essentielle de toute stratégie de continuité d’activité ou de récupération d’urgence.</span><span class="sxs-lookup"><span data-stu-id="f2dd9-190">Because database backups protect data from accidental corruption or deletion, they're an essential part of any business continuity and disaster recovery strategy.</span></span> <span data-ttu-id="f2dd9-191">toolearn sur hello d’autres solutions de continuité d’activité de base de données SQL, consultez [vue d’ensemble de la continuité des activités métier](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="f2dd9-191">toolearn about hello other SQL Database business-continuity solutions, see [Business continuity overview](sql-database-business-continuity.md).</span></span>
