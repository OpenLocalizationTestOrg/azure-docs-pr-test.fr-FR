---
title: aaaBack de votre application dans Azure
description: "Découvrez comment toocreate les sauvegardes de vos applications dans Azure App Service."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 6223b6bd-84ec-48df-943f-461d84605694
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: e41d93d322bbc48b45b28eeaa817928d83c2b9d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-your-app-in-azure"></a><span data-ttu-id="07fc8-103">Sauvegarde de votre application dans Azure</span><span class="sxs-lookup"><span data-stu-id="07fc8-103">Back up your app in Azure</span></span>
<span data-ttu-id="07fc8-104">Hello sauvegarder et restaurer la fonctionnalité de [Azure App Service](../app-service/app-service-value-prop-what-is.md) vous permet de créer facilement des sauvegardes de l’application manuellement ou selon une planification.</span><span class="sxs-lookup"><span data-stu-id="07fc8-104">hello Back up and Restore feature in [Azure App Service](../app-service/app-service-value-prop-what-is.md) lets you easily create app backups manually or on a schedule.</span></span> <span data-ttu-id="07fc8-105">Vous pouvez restaurer l’instantané de tooa hello application d’un état antérieur par remplacement hello application ou existante restauration tooanother.</span><span class="sxs-lookup"><span data-stu-id="07fc8-105">You can restore hello app tooa snapshot of a previous state by overwriting hello existing app or restoring tooanother app.</span></span> 

<span data-ttu-id="07fc8-106">Pour plus d’informations sur la restauration d’une application à partir d’une sauvegarde, consultez [Restauration d’une application dans Azure](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="07fc8-106">For information on restoring an app from backup, see [Restore an app in Azure](web-sites-restore.md).</span></span>

<a name="whatsbackedup"></a>

## <a name="what-gets-backed-up"></a><span data-ttu-id="07fc8-107">Éléments sauvegardés</span><span class="sxs-lookup"><span data-stu-id="07fc8-107">What gets backed up</span></span>
<span data-ttu-id="07fc8-108">Service de l’application peut effectuer des sauvegardes suivantes de hello compte de stockage Azure informations tooan et conteneur que vous avez configuré votre toouse d’application.</span><span class="sxs-lookup"><span data-stu-id="07fc8-108">App Service can backup hello following information tooan Azure storage account and container that you have configured your app toouse.</span></span> 

* <span data-ttu-id="07fc8-109">la configuration d’une application ;</span><span class="sxs-lookup"><span data-stu-id="07fc8-109">App configuration</span></span>
* <span data-ttu-id="07fc8-110">le contenu d’un fichier ;</span><span class="sxs-lookup"><span data-stu-id="07fc8-110">File content</span></span>
* <span data-ttu-id="07fc8-111">Base de données connectée tooyour application</span><span class="sxs-lookup"><span data-stu-id="07fc8-111">Database connected tooyour app</span></span>

<span data-ttu-id="07fc8-112">Hello suivant des solutions de base de données est pris en charge avec la fonctionnalité de sauvegarde :</span><span class="sxs-lookup"><span data-stu-id="07fc8-112">hello following database solutions are supported with backup feature:</span></span> 
   - [<span data-ttu-id="07fc8-113">Base de données SQL</span><span class="sxs-lookup"><span data-stu-id="07fc8-113">SQL Database</span></span>](https://azure.microsoft.com/en-us/services/sql-database/)
   - [<span data-ttu-id="07fc8-114">Azure Database pour MySQL (Version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="07fc8-114">Azure Database for MySQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/mysql)
   - [<span data-ttu-id="07fc8-115">Azure Database pour PostgreSQL (Version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="07fc8-115">Azure Database for PostgreSQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/postgres)
   - [<span data-ttu-id="07fc8-116">ClearDB MySQL</span><span class="sxs-lookup"><span data-stu-id="07fc8-116">ClearDB MySQL</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
   - [<span data-ttu-id="07fc8-117">MySQL dans l’application</span><span class="sxs-lookup"><span data-stu-id="07fc8-117">MySQL in-app</span></span>](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)
 

> [!NOTE]
>  <span data-ttu-id="07fc8-118">Chaque sauvegarde représente une copie hors connexion complète de votre application et non une mise à jour incrémentielle.</span><span class="sxs-lookup"><span data-stu-id="07fc8-118">Each backup is a complete offline copy of your app, not an incremental update.</span></span>
>  

<a name="requirements"></a>

## <a name="requirements-and-restrictions"></a><span data-ttu-id="07fc8-119">Exigences et restrictions</span><span class="sxs-lookup"><span data-stu-id="07fc8-119">Requirements and restrictions</span></span>
* <span data-ttu-id="07fc8-120">Hello sauvegarder et de la fonctionnalité de restauration requiert hello toobe du plan App Service Bonjour **Standard** couche ou **Premium** couche.</span><span class="sxs-lookup"><span data-stu-id="07fc8-120">hello Back up and Restore feature requires hello App Service plan toobe in hello **Standard** tier or **Premium** tier.</span></span> <span data-ttu-id="07fc8-121">Pour plus d’informations sur la mise à l’échelle votre toouse de plan de Service de l’application un niveau supérieur, consultez [évoluer une application dans Azure](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="07fc8-121">For more information about scaling your App Service plan toouse a higher tier, see [Scale up an app in Azure](web-sites-scale.md).</span></span>  
  <span data-ttu-id="07fc8-122">Le niveau **Premium** permet un plus grand nombre de sauvegardes quotidiennes que le niveau **Standard**.</span><span class="sxs-lookup"><span data-stu-id="07fc8-122">**Premium** tier allows a greater number of daily back ups than **Standard** tier.</span></span>
* <span data-ttu-id="07fc8-123">Vous avez besoin d’un compte de stockage Azure et un conteneur dans hello même abonnement que l’application hello que vous souhaitez toobackup.</span><span class="sxs-lookup"><span data-stu-id="07fc8-123">You need an Azure storage account and container in hello same subscription as hello app that you want toobackup.</span></span> <span data-ttu-id="07fc8-124">Pour plus d’informations sur les comptes de stockage Azure, consultez hello [liens](#moreaboutstorage) à fin hello de cet article.</span><span class="sxs-lookup"><span data-stu-id="07fc8-124">For more information on Azure storage accounts, see hello [links](#moreaboutstorage) at hello end of this article.</span></span>
* <span data-ttu-id="07fc8-125">Les sauvegardes peuvent être des Go too10 du contenu d’application et de la base de données.</span><span class="sxs-lookup"><span data-stu-id="07fc8-125">Backups can be up too10 GB of app and database content.</span></span> <span data-ttu-id="07fc8-126">Si la taille de la sauvegarde hello dépasse cette limite, vous obtenez une erreur.</span><span class="sxs-lookup"><span data-stu-id="07fc8-126">If hello backup size exceeds this limit, you get an error .</span></span>

<a name="manualbackup"></a>

## <a name="create-a-manual-backup"></a><span data-ttu-id="07fc8-127">Création d’une sauvegarde manuelle</span><span class="sxs-lookup"><span data-stu-id="07fc8-127">Create a manual backup</span></span>
1. <span data-ttu-id="07fc8-128">Bonjour [Azure Portal](https://portal.azure.com), accédez Panneau de l’application tooyour, sélectionnez **sauvegardes**.</span><span class="sxs-lookup"><span data-stu-id="07fc8-128">In hello [Azure Portal](https://portal.azure.com), navigate tooyour app's blade, select **Backups**.</span></span> <span data-ttu-id="07fc8-129">Hello **sauvegardes** panneau s’affiche.</span><span class="sxs-lookup"><span data-stu-id="07fc8-129">hello **Backups** blade will be displayed.</span></span>
   
    ![Page Sauvegardes][ChooseBackupsPage]
   
   > [!NOTE]
   > <span data-ttu-id="07fc8-131">Si vous voyez le message de type hello ci-dessous, cliquez dessus tooupgrade votre plan App Service avant de peut continuer avec les sauvegardes.</span><span class="sxs-lookup"><span data-stu-id="07fc8-131">If you see hello message below, click it tooupgrade your App Service plan before you can proceed with backups.</span></span>
   > <span data-ttu-id="07fc8-132">Consultez la page [Mise à l’échelle d’une application web dans Microsoft Azure App Service](web-sites-scale.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="07fc8-132">See [Scale up an app in Azure](web-sites-scale.md) for more information.</span></span>  
   > <span data-ttu-id="07fc8-133">![Sélection d'un compte de stockage](./media/web-sites-backup/01UpgradePlan1.png)</span><span class="sxs-lookup"><span data-stu-id="07fc8-133">![Choose storage account](./media/web-sites-backup/01UpgradePlan1.png)</span></span>
   > 
   > 

2. <span data-ttu-id="07fc8-134">Bonjour **sauvegarde** panneau, cliquez sur **configurer**
![cliquez sur Configurer](./media/web-sites-backup/ClickConfigure1.png)</span><span class="sxs-lookup"><span data-stu-id="07fc8-134">In hello **Backup** blade, Click **Configure**
![Click Configure](./media/web-sites-backup/ClickConfigure1.png)</span></span>
3. <span data-ttu-id="07fc8-135">Bonjour **Configuration de la sauvegarde** panneau, cliquez sur **stockage : non configuré** tooconfigure un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="07fc8-135">In hello **Backup Configuration** blade, click **Storage: Not configured** tooconfigure a storage account.</span></span>
   
    ![Sélection d'un compte de stockage][ChooseStorageAccount]
4. <span data-ttu-id="07fc8-137">Choisissez la destination de sauvegarde en sélectionnant un **Compte de stockage** et un **Conteneur**.</span><span class="sxs-lookup"><span data-stu-id="07fc8-137">Choose your backup destination by selecting a **Storage Account** and **Container**.</span></span> <span data-ttu-id="07fc8-138">compte de stockage Hello doit appartenir toohello même abonnement que hello application tooback des.</span><span class="sxs-lookup"><span data-stu-id="07fc8-138">hello storage account must belong toohello same subscription as hello app you want tooback up.</span></span> <span data-ttu-id="07fc8-139">Si vous le souhaitez, vous pouvez créer un compte de stockage ou un nouveau conteneur dans les panneaux respectifs hello.</span><span class="sxs-lookup"><span data-stu-id="07fc8-139">If you wish, you can create a new storage account or a new container in hello respective blades.</span></span> <span data-ttu-id="07fc8-140">Quand vous avez terminé, cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="07fc8-140">When you're done, click **Select**.</span></span>
   
    ![Sélection d'un compte de stockage](./media/web-sites-backup/02ChooseStorageAccount1-1.png)
5. <span data-ttu-id="07fc8-142">Bonjour **Configuration de la sauvegarde** panneau qui reste ouvert, vous pouvez configurer **sauvegarde de base de données**, puis sélectionnez les bases de données hello souhaité tooinclude dans les sauvegardes hello (base de données SQL ou MySQL), puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="07fc8-142">In hello **Backup Configuration** blade that is still left open, you can configure **Backup Database**, then select hello databases you want tooinclude in hello backups (SQL database or MySQL), then click **OK**.</span></span>  
   
    ![Sélection d'un compte de stockage](./media/web-sites-backup/03ConfigureDatabase1.png)
   
   > [!NOTE]
   > <span data-ttu-id="07fc8-144">Pour une base de données tooappear dans cette liste, sa chaîne de connexion doit exister dans hello **les chaînes de connexion** section Hello **paramètres de l’Application** panneau pour votre application.</span><span class="sxs-lookup"><span data-stu-id="07fc8-144">For a database tooappear in this list, its connection string must exist in hello **Connection strings** section of hello **Application settings** blade for your app.</span></span>
   > 
   > 
6. <span data-ttu-id="07fc8-145">Bonjour **Configuration de la sauvegarde** panneau, cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="07fc8-145">In hello **Backup Configuration** blade, click **Save**.</span></span>    
7. <span data-ttu-id="07fc8-146">Bonjour **sauvegardes** panneau, cliquez sur **sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="07fc8-146">In hello  **Backups** blade, click **Backup**.</span></span>
   
    ![Bouton Backup Now][BackUpNow]
   
    <span data-ttu-id="07fc8-148">Vous voyez un message de progression pendant le processus de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="07fc8-148">You see a progress message during hello backup process.</span></span>

<span data-ttu-id="07fc8-149">Une fois que le compte de stockage hello et un conteneur est configuré, vous pouvez lancer une sauvegarde manuelle à tout moment.</span><span class="sxs-lookup"><span data-stu-id="07fc8-149">Once hello storage account and container is configured you can initiate a manual backup at any time.</span></span>  

<a name="automatedbackups"></a>

## <a name="configure-automated-backups"></a><span data-ttu-id="07fc8-150">Configuration de sauvegardes automatisées</span><span class="sxs-lookup"><span data-stu-id="07fc8-150">Configure automated backups</span></span>
1. <span data-ttu-id="07fc8-151">Bonjour **Configuration de la sauvegarde** panneau, définissez **planifiée sauvegarde** trop**sur**.</span><span class="sxs-lookup"><span data-stu-id="07fc8-151">In hello **Backup Configuration** blade, set **Scheduled backup** too**On**.</span></span> 
   
    ![Sélection d'un compte de stockage](./media/web-sites-backup/05ScheduleBackup1.png)
2. <span data-ttu-id="07fc8-153">Planification de sauvegarde seront afficheront les options définie **planifiée sauvegarde** trop**sur**, configurez la planification de sauvegarde hello selon vos besoins, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="07fc8-153">Backup schedule options will show up, set **Scheduled Backup** too**On**, then configure hello backup schedule as desired and click **OK**.</span></span>
   
    ![Activation des sauvegardes automatisées][SetAutomatedBackupOn]

<a name="partialbackups"></a>

## <a name="configure-partial-backups"></a><span data-ttu-id="07fc8-155">Configurer des sauvegardes partielles</span><span class="sxs-lookup"><span data-stu-id="07fc8-155">Configure Partial Backups</span></span>
<span data-ttu-id="07fc8-156">Parfois, vous ne souhaitez toobackup tous les éléments sur votre application.</span><span class="sxs-lookup"><span data-stu-id="07fc8-156">Sometimes you don't want toobackup everything on your app.</span></span> <span data-ttu-id="07fc8-157">Voici quelques exemples :</span><span class="sxs-lookup"><span data-stu-id="07fc8-157">Here are a few examples:</span></span>

* <span data-ttu-id="07fc8-158">Vous [configurez une sauvegarde hebdomadaire](web-sites-backup.md#configure-automated-backups) de votre application qui contient du contenu statique qui ne change jamais, comme des anciens billets de blog ou des images.</span><span class="sxs-lookup"><span data-stu-id="07fc8-158">You [set up weekly backups](web-sites-backup.md#configure-automated-backups) of your app that contains static content that never changes, such as old blog posts or images.</span></span>
* <span data-ttu-id="07fc8-159">Votre application dispose de plus de 10 Go de contenu (ce qui est la quantité maximale de hello que vous pouvez sauvegarder à la fois).</span><span class="sxs-lookup"><span data-stu-id="07fc8-159">Your app has over 10 GB of content (that's hello max amount you can backup at a time).</span></span>
* <span data-ttu-id="07fc8-160">Vous ne souhaitez pas les fichiers journaux toobackup hello.</span><span class="sxs-lookup"><span data-stu-id="07fc8-160">You don't want toobackup hello log files.</span></span>

<span data-ttu-id="07fc8-161">Sauvegardes partielles vous permet de choisir exactement les fichiers auxquels vous souhaitez toobackup.</span><span class="sxs-lookup"><span data-stu-id="07fc8-161">Partial backups allows you choose exactly which files you want toobackup.</span></span>

### <a name="exclude-files-from-your-backup"></a><span data-ttu-id="07fc8-162">Exclusion de fichiers de votre sauvegarde</span><span class="sxs-lookup"><span data-stu-id="07fc8-162">Exclude files from your backup</span></span>
<span data-ttu-id="07fc8-163">Supposons que vous disposez d’une application qui contient les fichiers journaux et des images statiques qui ont été sauvegarde qu’une seule fois et ne vont pas toochange.</span><span class="sxs-lookup"><span data-stu-id="07fc8-163">Suppose you have an app that contains log files and static images that have been backup once and are not going toochange.</span></span> <span data-ttu-id="07fc8-164">Dans ce cas, vous pouvez exclure ces fichiers et dossiers du stockage lors de vos sauvegardes futures.</span><span class="sxs-lookup"><span data-stu-id="07fc8-164">In such cases you can exclude those folders and files from being stored in your future backups.</span></span> <span data-ttu-id="07fc8-165">tooexclude fichiers et dossiers à partir des sauvegardes, créer un `_backup.filter` fichier Bonjour `D:\home\site\wwwroot` dossier de votre application.</span><span class="sxs-lookup"><span data-stu-id="07fc8-165">tooexclude files and folders from your backups, create a `_backup.filter` file in hello `D:\home\site\wwwroot` folder of your app.</span></span> <span data-ttu-id="07fc8-166">Spécifiez la liste hello des fichiers et dossiers que vous souhaitez tooexclude dans ce fichier.</span><span class="sxs-lookup"><span data-stu-id="07fc8-166">Specify hello list of files and folders you want tooexclude in this file.</span></span> 

<span data-ttu-id="07fc8-167">Un tooaccess facilement vos fichiers est toouse Kudu.</span><span class="sxs-lookup"><span data-stu-id="07fc8-167">An easy way tooaccess your files is toouse Kudu .</span></span> <span data-ttu-id="07fc8-168">Cliquez sur **outils avancés -> accédez** définition pour votre tooaccess d’application web Kudu.</span><span class="sxs-lookup"><span data-stu-id="07fc8-168">Click **Advanced Tools -> Go** setting for your web app tooaccess Kudu.</span></span>

![Utilisation du portail par Kudu][kudu-portal]

<span data-ttu-id="07fc8-170">Identifiez les dossiers hello que vous souhaitez tooexclude à partir de vos sauvegardes.</span><span class="sxs-lookup"><span data-stu-id="07fc8-170">Identify hello folders that you want tooexclude from your backups.</span></span>  <span data-ttu-id="07fc8-171">Par exemple, vous souhaitez toofilter dossier de mise en surbrillance de hello et fichiers de sortie.</span><span class="sxs-lookup"><span data-stu-id="07fc8-171">For example , you want toofilter out hello highlighted folder and files.</span></span>

![Dossier images][ImagesFolder]

<span data-ttu-id="07fc8-173">Créez un fichier appelé `_backup.filter` et placer la liste hello ci-dessus dans le fichier de hello, mais supprimer `D:\home`.</span><span class="sxs-lookup"><span data-stu-id="07fc8-173">Create a file called `_backup.filter` and put hello list above in hello file, but remove `D:\home`.</span></span> <span data-ttu-id="07fc8-174">Listez un répertoire ou fichier par ligne.</span><span class="sxs-lookup"><span data-stu-id="07fc8-174">List one directory or file per line.</span></span> <span data-ttu-id="07fc8-175">Par conséquent, le contenu du fichier de hello hello doit être :</span><span class="sxs-lookup"><span data-stu-id="07fc8-175">So hello content of hello file should be:</span></span>
 ```bash
    \site\wwwroot\Images\brand.png
    \site\wwwroot\Images\2014
    \site\wwwroot\Images\2013
```

<span data-ttu-id="07fc8-176">Télécharger `_backup.filter` toohello de fichiers `D:\home\site\wwwroot\` répertoire de votre site à l’aide de [ftp](web-sites-deploy.md#ftp) ou toute autre méthode.</span><span class="sxs-lookup"><span data-stu-id="07fc8-176">Upload `_backup.filter` file toohello `D:\home\site\wwwroot\` directory of your site using [ftp](web-sites-deploy.md#ftp) or any other method.</span></span> <span data-ttu-id="07fc8-177">Si vous le souhaitez, vous pouvez créer le fichier hello directement à l’aide de Kudu `DebugConsole` et insérez le contenu hello il.</span><span class="sxs-lookup"><span data-stu-id="07fc8-177">If you wish, you can create hello file directly using Kudu  `DebugConsole` and insert hello content there.</span></span>

<span data-ttu-id="07fc8-178">Exécution de sauvegardes hello la même façon que vous feriez normalement, [manuellement](#create-a-manual-backup) ou [automatiquement](#configure-automated-backups).</span><span class="sxs-lookup"><span data-stu-id="07fc8-178">Run backups hello same way you would normally do it, [manually](#create-a-manual-backup) or [automatically](#configure-automated-backups).</span></span> <span data-ttu-id="07fc8-179">Maintenant, tous les fichiers et dossiers qui sont spécifiés dans `_backup.filter` est exclu de hello futures sauvegardes planifiées ou lancées manuellement.</span><span class="sxs-lookup"><span data-stu-id="07fc8-179">Now, any files and folders that are specified in `_backup.filter` is excluded from hello future backups scheduled or manually initiated.</span></span> 

> [!NOTE]
> <span data-ttu-id="07fc8-180">Vous restaurez les sauvegardes partielles de votre hello site manière [restaurer une sauvegarde régulière](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="07fc8-180">You restore partial backups of your site hello same way you would [restore a regular backup](web-sites-restore.md).</span></span> <span data-ttu-id="07fc8-181">processus de restauration Hello hello qu’il faut.</span><span class="sxs-lookup"><span data-stu-id="07fc8-181">hello restore process does hello right thing.</span></span>
> 
> <span data-ttu-id="07fc8-182">Lorsqu’une sauvegarde complète est restaurée, tout le contenu sur le site de hello est remplacé par tout ce qui est dans la sauvegarde de hello.</span><span class="sxs-lookup"><span data-stu-id="07fc8-182">When a full backup is restored, all content on hello site is replaced with whatever is in hello backup.</span></span> <span data-ttu-id="07fc8-183">Si un fichier se trouve sur le site de hello, mais pas dans la sauvegarde de hello, il est supprimé.</span><span class="sxs-lookup"><span data-stu-id="07fc8-183">If a file is on hello site, but not in hello backup it gets deleted.</span></span> <span data-ttu-id="07fc8-184">Mais lors de la restauration d’une sauvegarde partielle, tout contenu qui se trouve dans un des répertoires de hello sur liste noire ou n’importe quel fichier sur liste noire, demeure en l’état.</span><span class="sxs-lookup"><span data-stu-id="07fc8-184">But when a partial backup is restored, any content that is located in one of hello blacklisted directories, or any blacklisted file, is left as is.</span></span>
> 


<a name="aboutbackups"></a>

## <a name="how-backups-are-stored"></a><span data-ttu-id="07fc8-185">Mode de stockage des sauvegardes</span><span class="sxs-lookup"><span data-stu-id="07fc8-185">How backups are stored</span></span>
<span data-ttu-id="07fc8-186">Après avoir effectué une ou plusieurs sauvegardes de votre application, les sauvegardes hello sont visibles sur hello **conteneurs** Panneau de votre compte de stockage et de votre application.</span><span class="sxs-lookup"><span data-stu-id="07fc8-186">After you have made one or more backups for your app, hello backups are visible on hello **Containers** blade of your storage account, and your app.</span></span> <span data-ttu-id="07fc8-187">Dans le compte de stockage hello, chaque sauvegarde se compose d’un`.zip` fichier qui contient les données de sauvegarde hello et un `.xml` fichier qui contient un manifeste de hello `.zip` le contenu du fichier.</span><span class="sxs-lookup"><span data-stu-id="07fc8-187">In hello storage account, each backup consists of a`.zip` file that contains hello backup data and an `.xml` file that contains a manifest of hello `.zip` file contents.</span></span> <span data-ttu-id="07fc8-188">Vous pouvez décompresser et parcourir ces fichiers si vous souhaitez tooaccess vos sauvegardes sans réellement effectuer une restauration d’une application.</span><span class="sxs-lookup"><span data-stu-id="07fc8-188">You can unzip and browse these files if you want tooaccess your backups without actually performing an app restore.</span></span>

<span data-ttu-id="07fc8-189">sauvegarde de base de données Hello pour une application hello est stocké dans la racine hello 100Ko fichier.</span><span class="sxs-lookup"><span data-stu-id="07fc8-189">hello database backup for hello app is stored in hello root of the.zip file.</span></span> <span data-ttu-id="07fc8-190">Pour une base de données SQL, il s'agit d'un fichier BACPAC (pas d'extension de fichier) qui peut être importé.</span><span class="sxs-lookup"><span data-stu-id="07fc8-190">For a SQL database, this is a BACPAC file (no file extension) and can be imported.</span></span> <span data-ttu-id="07fc8-191">en fonction de base de données SQL toocreate de hello exportation de BACPAC, consultez [importer un fichier BACPAC de tooCreate une base de données utilisateur](http://technet.microsoft.com/library/hh710052.aspx).</span><span class="sxs-lookup"><span data-stu-id="07fc8-191">toocreate a SQL database based on hello BACPAC export, see [Import a BACPAC File tooCreate a New User Database](http://technet.microsoft.com/library/hh710052.aspx).</span></span>

> [!WARNING]
> <span data-ttu-id="07fc8-192">Modification des fichiers hello dans votre **websitebackups** conteneur peut entraîner des toobecome de sauvegarde hello non valide et par conséquent non récupérable.</span><span class="sxs-lookup"><span data-stu-id="07fc8-192">Altering any of hello files in your **websitebackups** container can cause hello backup toobecome invalid and therefore non-restorable.</span></span>
> 
> 

<a name="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="07fc8-193">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="07fc8-193">Next Steps</span></span>
<span data-ttu-id="07fc8-194">Pour plus d’informations sur la restauration d’une application à partir d’une sauvegarde, consultez [Restauration d’une application dans Azure](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="07fc8-194">For information on restoring an app from a backup, see [Restore an app in Azure](web-sites-restore.md).</span></span> <span data-ttu-id="07fc8-195">Vous pouvez également sauvegarder et restaurer des applications de Service d’applications à l’aide des API REST (voir [utilisation reste toobackup et la restauration d’applications de Service d’applications](websites-csm-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="07fc8-195">You can also backup and restore App Service apps using REST API (see [Use REST toobackup and restore App Service apps](websites-csm-backup.md)).</span></span>


<!-- IMAGES -->
[ChooseBackupsPage]: ./media/web-sites-backup/01ChooseBackupsPage1.png
[ChooseStorageAccount]: ./media/web-sites-backup/02ChooseStorageAccount-1.png
[IncludedDatabases]: ./media/web-sites-backup/03IncludedDatabases.png
[BackUpNow]: ./media/web-sites-backup/04BackUpNow1.png
[BackupProgress]: ./media/web-sites-backup/05BackupProgress.png
[SetAutomatedBackupOn]: ./media/web-sites-backup/06SetAutomatedBackupOn1.png
[Frequency]: ./media/web-sites-backup/07Frequency.png
[StartDate]: ./media/web-sites-backup/08StartDate.png
[StartTime]: ./media/web-sites-backup/09StartTime.png
[SaveIcon]: ./media/web-sites-backup/10SaveIcon.png
[ImagesFolder]: ./media/web-sites-backup/11Images.png
[LogsFolder]: ./media/web-sites-backup/12Logs.png
[GhostUpgradeWarning]: ./media/web-sites-backup/13GhostUpgradeWarning.png
[kudu-portal]:./media/web-sites-backup/kudu-portal.PNG

