---
title: Sauvegarde de votre application dans Azure
description: "Apprenez à créer des sauvegardes de vos applications Web dans Azure App Service."
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
ms.openlocfilehash: 77e983afaaba8e944ab1f337e1c28ced83b63205
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="back-up-your-app-in-azure"></a><span data-ttu-id="01378-103">Sauvegarde de votre application dans Azure</span><span class="sxs-lookup"><span data-stu-id="01378-103">Back up your app in Azure</span></span>
<span data-ttu-id="01378-104">La fonctionnalité de sauvegarde et de restauration d’[Azure App Service](../app-service/app-service-value-prop-what-is.md) vous permet de créer facilement des sauvegardes d’applications manuelles ou planifiées.</span><span class="sxs-lookup"><span data-stu-id="01378-104">The Back up and Restore feature in [Azure App Service](../app-service/app-service-value-prop-what-is.md) lets you easily create app backups manually or on a schedule.</span></span> <span data-ttu-id="01378-105">Vous pouvez restaurer l’application d’après la capture instantanée d’un état précédent en remplaçant l’application existante ou en restaurant sur une autre application.</span><span class="sxs-lookup"><span data-stu-id="01378-105">You can restore the app to a snapshot of a previous state by overwriting the existing app or restoring to another app.</span></span> 

<span data-ttu-id="01378-106">Pour plus d’informations sur la restauration d’une application à partir d’une sauvegarde, consultez [Restauration d’une application dans Azure](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="01378-106">For information on restoring an app from backup, see [Restore an app in Azure](web-sites-restore.md).</span></span>

<a name="whatsbackedup"></a>

## <a name="what-gets-backed-up"></a><span data-ttu-id="01378-107">Éléments sauvegardés</span><span class="sxs-lookup"><span data-stu-id="01378-107">What gets backed up</span></span>
<span data-ttu-id="01378-108">App Service peut sauvegarder les informations suivantes sur un compte de stockage Azure et un conteneur que votre application à été configurée pour utiliser.</span><span class="sxs-lookup"><span data-stu-id="01378-108">App Service can backup the following information to an Azure storage account and container that you have configured your app to use.</span></span> 

* <span data-ttu-id="01378-109">la configuration d’une application ;</span><span class="sxs-lookup"><span data-stu-id="01378-109">App configuration</span></span>
* <span data-ttu-id="01378-110">le contenu d’un fichier ;</span><span class="sxs-lookup"><span data-stu-id="01378-110">File content</span></span>
* <span data-ttu-id="01378-111">la base de données connectée à votre application.</span><span class="sxs-lookup"><span data-stu-id="01378-111">Database connected to your app</span></span>

<span data-ttu-id="01378-112">Les solutions de base de données suivantes sont prises en charge par la fonctionnalité de sauvegarde :</span><span class="sxs-lookup"><span data-stu-id="01378-112">The following database solutions are supported with backup feature:</span></span> 
   - [<span data-ttu-id="01378-113">Base de données SQL</span><span class="sxs-lookup"><span data-stu-id="01378-113">SQL Database</span></span>](https://azure.microsoft.com/en-us/services/sql-database/)
   - [<span data-ttu-id="01378-114">Azure Database pour MySQL (Version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="01378-114">Azure Database for MySQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/mysql)
   - [<span data-ttu-id="01378-115">Azure Database pour PostgreSQL (Version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="01378-115">Azure Database for PostgreSQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/postgres)
   - [<span data-ttu-id="01378-116">ClearDB MySQL</span><span class="sxs-lookup"><span data-stu-id="01378-116">ClearDB MySQL</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
   - [<span data-ttu-id="01378-117">MySQL dans l’application</span><span class="sxs-lookup"><span data-stu-id="01378-117">MySQL in-app</span></span>](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)
 

> [!NOTE]
>  <span data-ttu-id="01378-118">Chaque sauvegarde représente une copie hors connexion complète de votre application et non une mise à jour incrémentielle.</span><span class="sxs-lookup"><span data-stu-id="01378-118">Each backup is a complete offline copy of your app, not an incremental update.</span></span>
>  

<a name="requirements"></a>

## <a name="requirements-and-restrictions"></a><span data-ttu-id="01378-119">Exigences et restrictions</span><span class="sxs-lookup"><span data-stu-id="01378-119">Requirements and restrictions</span></span>
* <span data-ttu-id="01378-120">La fonctionnalité de sauvegarde et de restauration implique que le plan App Service soit de type **Standard** ou **Premium**.</span><span class="sxs-lookup"><span data-stu-id="01378-120">The Back up and Restore feature requires the App Service plan to be in the **Standard** tier or **Premium** tier.</span></span> <span data-ttu-id="01378-121">Pour plus d'informations sur la mise à l’échelle de votre plan App Service en vue d'utiliser un niveau plus élevé, consultez [Mise à l’échelle d’une application web dans Microsoft Azure App Service](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="01378-121">For more information about scaling your App Service plan to use a higher tier, see [Scale up an app in Azure](web-sites-scale.md).</span></span>  
  <span data-ttu-id="01378-122">Le niveau **Premium** permet un plus grand nombre de sauvegardes quotidiennes que le niveau **Standard**.</span><span class="sxs-lookup"><span data-stu-id="01378-122">**Premium** tier allows a greater number of daily back ups than **Standard** tier.</span></span>
* <span data-ttu-id="01378-123">Vous avez besoin d’un compte de stockage Azure et d’un conteneur dans le même abonnement que l’application que vous souhaitez sauvegarder.</span><span class="sxs-lookup"><span data-stu-id="01378-123">You need an Azure storage account and container in the same subscription as the app that you want to backup.</span></span> <span data-ttu-id="01378-124">Pour plus d'informations sur les comptes de stockage Azure, consultez les [liens](#moreaboutstorage) situés en bas de cet article.</span><span class="sxs-lookup"><span data-stu-id="01378-124">For more information on Azure storage accounts, see the [links](#moreaboutstorage) at the end of this article.</span></span>
* <span data-ttu-id="01378-125">Les sauvegardes peuvent contenir jusqu’à 10 Go de contenu d’applications et de bases de données.</span><span class="sxs-lookup"><span data-stu-id="01378-125">Backups can be up to 10 GB of app and database content.</span></span> <span data-ttu-id="01378-126">Une erreur se produit si la taille de la sauvegarde dépasse cette limite.</span><span class="sxs-lookup"><span data-stu-id="01378-126">If the backup size exceeds this limit, you get an error .</span></span>

<a name="manualbackup"></a>

## <a name="create-a-manual-backup"></a><span data-ttu-id="01378-127">Création d’une sauvegarde manuelle</span><span class="sxs-lookup"><span data-stu-id="01378-127">Create a manual backup</span></span>
1. <span data-ttu-id="01378-128">Sur le [Portail Azure](https://portal.azure.com), accédez au panneau de votre application et sélectionnez **Sauvegardes**.</span><span class="sxs-lookup"><span data-stu-id="01378-128">In the [Azure Portal](https://portal.azure.com), navigate to your app's blade, select **Backups**.</span></span> <span data-ttu-id="01378-129">Le panneau **Sauvegardes** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="01378-129">The **Backups** blade will be displayed.</span></span>
   
    ![Page Sauvegardes][ChooseBackupsPage]
   
   > [!NOTE]
   > <span data-ttu-id="01378-131">Si le message ci-dessous s’affiche, cliquez dessus pour mettre à niveau votre plan App Service avant de pouvoir poursuivre avec les sauvegardes.</span><span class="sxs-lookup"><span data-stu-id="01378-131">If you see the message below, click it to upgrade your App Service plan before you can proceed with backups.</span></span>
   > <span data-ttu-id="01378-132">Consultez la page [Mise à l’échelle d’une application web dans Microsoft Azure App Service](web-sites-scale.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="01378-132">See [Scale up an app in Azure](web-sites-scale.md) for more information.</span></span>  
   > <span data-ttu-id="01378-133">![Sélection d'un compte de stockage](./media/web-sites-backup/01UpgradePlan1.png)</span><span class="sxs-lookup"><span data-stu-id="01378-133">![Choose storage account](./media/web-sites-backup/01UpgradePlan1.png)</span></span>
   > 
   > 

2. <span data-ttu-id="01378-134">Dans le panneau **Sauvegarde**, cliquez sur **Configurer**
![Cliquer sur Configurer](./media/web-sites-backup/ClickConfigure1.png).</span><span class="sxs-lookup"><span data-stu-id="01378-134">In the **Backup** blade, Click **Configure**
![Click Configure](./media/web-sites-backup/ClickConfigure1.png)</span></span>
3. <span data-ttu-id="01378-135">Dans le panneau **Configuration de la sauvegarde**, cliquez sur **Stockage : Non configuré** pour configurer un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="01378-135">In the **Backup Configuration** blade, click **Storage: Not configured** to configure a storage account.</span></span>
   
    ![Sélection d'un compte de stockage][ChooseStorageAccount]
4. <span data-ttu-id="01378-137">Choisissez la destination de sauvegarde en sélectionnant un **Compte de stockage** et un **Conteneur**.</span><span class="sxs-lookup"><span data-stu-id="01378-137">Choose your backup destination by selecting a **Storage Account** and **Container**.</span></span> <span data-ttu-id="01378-138">Ce compte de stockage doit relever du même abonnement que l’application que vous souhaitez sauvegarder.</span><span class="sxs-lookup"><span data-stu-id="01378-138">The storage account must belong to the same subscription as the app you want to back up.</span></span> <span data-ttu-id="01378-139">Si vous le souhaitez, vous pouvez créer un compte de stockage ou un conteneur dans les panneaux respectifs.</span><span class="sxs-lookup"><span data-stu-id="01378-139">If you wish, you can create a new storage account or a new container in the respective blades.</span></span> <span data-ttu-id="01378-140">Quand vous avez terminé, cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="01378-140">When you're done, click **Select**.</span></span>
   
    ![Sélection d'un compte de stockage](./media/web-sites-backup/02ChooseStorageAccount1-1.png)
5. <span data-ttu-id="01378-142">Dans le panneau **Configuration de la sauvegarde**, toujours ouvert, vous pouvez configurer **Base de données de sauvegarde**, puis sélectionner les bases de données que vous souhaitez inclure dans les sauvegardes (base de données SQL ou MySQL) et enfin cliquer sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="01378-142">In the **Backup Configuration** blade that is still left open, you can configure **Backup Database**, then select the databases you want to include in the backups (SQL database or MySQL), then click **OK**.</span></span>  
   
    ![Sélection d'un compte de stockage](./media/web-sites-backup/03ConfigureDatabase1.png)
   
   > [!NOTE]
   > <span data-ttu-id="01378-144">Pour qu’une base de données apparaisse dans cette liste, sa chaîne de connexion doit figurer dans la section **Chaînes de connexion** du panneau **Paramètres d’application** de votre application.</span><span class="sxs-lookup"><span data-stu-id="01378-144">For a database to appear in this list, its connection string must exist in the **Connection strings** section of the **Application settings** blade for your app.</span></span>
   > 
   > 
6. <span data-ttu-id="01378-145">Dans le panneau **Configuration de la sauvegarde**, cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="01378-145">In the **Backup Configuration** blade, click **Save**.</span></span>    
7. <span data-ttu-id="01378-146">Dans le panneau **Sauvegardes**, cliquez sur **Sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="01378-146">In the  **Backups** blade, click **Backup**.</span></span>
   
    ![Bouton Backup Now][BackUpNow]
   
    <span data-ttu-id="01378-148">Un message de progression s’affiche au cours du processus de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="01378-148">You see a progress message during the backup process.</span></span>

<span data-ttu-id="01378-149">Une fois que le compte de stockage et le conteneur configurés, vous pouvez lancer une sauvegarde manuelle à tout moment.</span><span class="sxs-lookup"><span data-stu-id="01378-149">Once the storage account and container is configured you can initiate a manual backup at any time.</span></span>  

<a name="automatedbackups"></a>

## <a name="configure-automated-backups"></a><span data-ttu-id="01378-150">Configuration de sauvegardes automatisées</span><span class="sxs-lookup"><span data-stu-id="01378-150">Configure automated backups</span></span>
1. <span data-ttu-id="01378-151">Dans le panneau **Configuration de la sauvegarde**, **activez** la **Sauvegarde planifiée**.</span><span class="sxs-lookup"><span data-stu-id="01378-151">In the **Backup Configuration** blade, set **Scheduled backup** to **On**.</span></span> 
   
    ![Sélection d'un compte de stockage](./media/web-sites-backup/05ScheduleBackup1.png)
2. <span data-ttu-id="01378-153">Les options de planification de la sauvegarde apparaissent : **activez** la **Sauvegarde planifiée**, puis configurez la planification de sauvegarde comme vous le souhaitez et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="01378-153">Backup schedule options will show up, set **Scheduled Backup** to **On**, then configure the backup schedule as desired and click **OK**.</span></span>
   
    ![Activation des sauvegardes automatisées][SetAutomatedBackupOn]

<a name="partialbackups"></a>

## <a name="configure-partial-backups"></a><span data-ttu-id="01378-155">Configurer des sauvegardes partielles</span><span class="sxs-lookup"><span data-stu-id="01378-155">Configure Partial Backups</span></span>
<span data-ttu-id="01378-156">Parfois, vous ne souhaitez pas sauvegarder tout le contenu de votre application.</span><span class="sxs-lookup"><span data-stu-id="01378-156">Sometimes you don't want to backup everything on your app.</span></span> <span data-ttu-id="01378-157">Voici quelques exemples :</span><span class="sxs-lookup"><span data-stu-id="01378-157">Here are a few examples:</span></span>

* <span data-ttu-id="01378-158">Vous [configurez une sauvegarde hebdomadaire](web-sites-backup.md#configure-automated-backups) de votre application qui contient du contenu statique qui ne change jamais, comme des anciens billets de blog ou des images.</span><span class="sxs-lookup"><span data-stu-id="01378-158">You [set up weekly backups](web-sites-backup.md#configure-automated-backups) of your app that contains static content that never changes, such as old blog posts or images.</span></span>
* <span data-ttu-id="01378-159">Votre application a plus de 10 Go de contenu (qui est la quantité maximale que vous pouvez sauvegarder à la fois).</span><span class="sxs-lookup"><span data-stu-id="01378-159">Your app has over 10 GB of content (that's the max amount you can backup at a time).</span></span>
* <span data-ttu-id="01378-160">Vous ne souhaitez pas sauvegarder les fichiers journaux.</span><span class="sxs-lookup"><span data-stu-id="01378-160">You don't want to backup the log files.</span></span>

<span data-ttu-id="01378-161">Les sauvegardes partielles vous permettent de choisir exactement les fichiers à sauvegarder.</span><span class="sxs-lookup"><span data-stu-id="01378-161">Partial backups allows you choose exactly which files you want to backup.</span></span>

### <a name="exclude-files-from-your-backup"></a><span data-ttu-id="01378-162">Exclusion de fichiers de votre sauvegarde</span><span class="sxs-lookup"><span data-stu-id="01378-162">Exclude files from your backup</span></span>
<span data-ttu-id="01378-163">Supposons que vous avez une application qui contient des fichiers journaux et des images statiques créés à un moment donné et qui ne seront jamais modifiés.</span><span class="sxs-lookup"><span data-stu-id="01378-163">Suppose you have an app that contains log files and static images that have been backup once and are not going to change.</span></span> <span data-ttu-id="01378-164">Dans ce cas, vous pouvez exclure ces fichiers et dossiers du stockage lors de vos sauvegardes futures.</span><span class="sxs-lookup"><span data-stu-id="01378-164">In such cases you can exclude those folders and files from being stored in your future backups.</span></span> <span data-ttu-id="01378-165">Pour exclure des fichiers et dossiers de vos sauvegardes, créez un fichier `_backup.filter` dans le dossier `D:\home\site\wwwroot` de votre application.</span><span class="sxs-lookup"><span data-stu-id="01378-165">To exclude files and folders from your backups, create a `_backup.filter` file in the `D:\home\site\wwwroot` folder of your app.</span></span> <span data-ttu-id="01378-166">Spécifiez la liste des fichiers et dossiers à exclure de ce fichier.</span><span class="sxs-lookup"><span data-stu-id="01378-166">Specify the list of files and folders you want to exclude in this file.</span></span> 

<span data-ttu-id="01378-167">L’utilisation de Kudu permet d’accéder facilement à vos fichiers.</span><span class="sxs-lookup"><span data-stu-id="01378-167">An easy way to access your files is to use Kudu .</span></span> <span data-ttu-id="01378-168">Cliquez sur le paramètre **Outils avancés -> Accéder** de votre application web pour accéder aux Kudu.</span><span class="sxs-lookup"><span data-stu-id="01378-168">Click **Advanced Tools -> Go** setting for your web app to access Kudu.</span></span>

![Utilisation du portail par Kudu][kudu-portal]

<span data-ttu-id="01378-170">Identifiez les dossiers que vous souhaitez exclure de vos sauvegardes.</span><span class="sxs-lookup"><span data-stu-id="01378-170">Identify the folders that you want to exclude from your backups.</span></span>  <span data-ttu-id="01378-171">Par exemple, si vous souhaitez exclure les fichiers et dossiers en surbrillance.</span><span class="sxs-lookup"><span data-stu-id="01378-171">For example , you want to filter out the highlighted folder and files.</span></span>

![Dossier images][ImagesFolder]

<span data-ttu-id="01378-173">Créez un fichier sous le nom `_backup.filter` et placez la liste précédente dans le fichier, mais supprimez `D:\home`.</span><span class="sxs-lookup"><span data-stu-id="01378-173">Create a file called `_backup.filter` and put the list above in the file, but remove `D:\home`.</span></span> <span data-ttu-id="01378-174">Listez un répertoire ou fichier par ligne.</span><span class="sxs-lookup"><span data-stu-id="01378-174">List one directory or file per line.</span></span> <span data-ttu-id="01378-175">Par conséquent, le contenu du fichier doit ressembler à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="01378-175">So the content of the file should be:</span></span>
 ```bash
    \site\wwwroot\Images\brand.png
    \site\wwwroot\Images\2014
    \site\wwwroot\Images\2013
```

<span data-ttu-id="01378-176">Téléchargez le fichier `_backup.filter` vers le répertoire `D:\home\site\wwwroot\` de votre site en utilisant [ftp](web-sites-deploy.md#ftp) ou toute autre méthode.</span><span class="sxs-lookup"><span data-stu-id="01378-176">Upload `_backup.filter` file to the `D:\home\site\wwwroot\` directory of your site using [ftp](web-sites-deploy.md#ftp) or any other method.</span></span> <span data-ttu-id="01378-177">Si vous le souhaitez, vous pouvez créer le fichier directement à l’aide de Kudu `DebugConsole` et y insérer le contenu.</span><span class="sxs-lookup"><span data-stu-id="01378-177">If you wish, you can create the file directly using Kudu  `DebugConsole` and insert the content there.</span></span>

<span data-ttu-id="01378-178">Exécutez des sauvegardes comme vous le faites normalement, [manuellement](#create-a-manual-backup) ou [automatiquement](#configure-automated-backups).</span><span class="sxs-lookup"><span data-stu-id="01378-178">Run backups the same way you would normally do it, [manually](#create-a-manual-backup) or [automatically](#configure-automated-backups).</span></span> <span data-ttu-id="01378-179">Maintenant, tous les fichiers et dossiers spécifiés dans `_backup.filter` sont exclus des futures sauvegardes planifiées ou lancées manuellement.</span><span class="sxs-lookup"><span data-stu-id="01378-179">Now, any files and folders that are specified in `_backup.filter` is excluded from the future backups scheduled or manually initiated.</span></span> 

> [!NOTE]
> <span data-ttu-id="01378-180">Pour restaurer les sauvegardes partielles de votre site, procédez de la même façon que pour [restaurer une sauvegarde régulière](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="01378-180">You restore partial backups of your site the same way you would [restore a regular backup](web-sites-restore.md).</span></span> <span data-ttu-id="01378-181">Le processus de restauration fait ce qu’il faut.</span><span class="sxs-lookup"><span data-stu-id="01378-181">The restore process does the right thing.</span></span>
> 
> <span data-ttu-id="01378-182">Lorsqu'une sauvegarde complète est restaurée, tout le contenu sur le site est remplacé par tout ce qui se trouve dans la sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="01378-182">When a full backup is restored, all content on the site is replaced with whatever is in the backup.</span></span> <span data-ttu-id="01378-183">Si un fichier se trouve sur le site, mais pas dans la sauvegarde, il est supprimé.</span><span class="sxs-lookup"><span data-stu-id="01378-183">If a file is on the site, but not in the backup it gets deleted.</span></span> <span data-ttu-id="01378-184">Mais lorsqu'une sauvegarde partielle est restaurée, tout contenu qui se trouve dans l'un des répertoires exclus, ou n'importe quel fichier exclu, est conservé tel quel.</span><span class="sxs-lookup"><span data-stu-id="01378-184">But when a partial backup is restored, any content that is located in one of the blacklisted directories, or any blacklisted file, is left as is.</span></span>
> 


<a name="aboutbackups"></a>

## <a name="how-backups-are-stored"></a><span data-ttu-id="01378-185">Mode de stockage des sauvegardes</span><span class="sxs-lookup"><span data-stu-id="01378-185">How backups are stored</span></span>
<span data-ttu-id="01378-186">Dès lors que vous avez effectué une ou plusieurs sauvegardes de votre application, celles-ci apparaissent dans le panneau **Conteneurs** de votre compte de stockage, et votre application.</span><span class="sxs-lookup"><span data-stu-id="01378-186">After you have made one or more backups for your app, the backups are visible on the **Containers** blade of your storage account, and your app.</span></span> <span data-ttu-id="01378-187">Dans le compte de stockage, chaque sauvegarde se compose d’un fichier `.zip` et d’un fichier `.xml` contenant respectivement les données sauvegardées et un manifeste du contenu du fichier `.zip`.</span><span class="sxs-lookup"><span data-stu-id="01378-187">In the storage account, each backup consists of a`.zip` file that contains the backup data and an `.xml` file that contains a manifest of the `.zip` file contents.</span></span> <span data-ttu-id="01378-188">Vous pouvez décompresser et parcourir ces fichiers si vous souhaitez accéder à vos sauvegardes sans réellement effectuer une restauration d'application.</span><span class="sxs-lookup"><span data-stu-id="01378-188">You can unzip and browse these files if you want to access your backups without actually performing an app restore.</span></span>

<span data-ttu-id="01378-189">La sauvegarde de base de données pour l’application est stockée dans la racine du fichier .zip.</span><span class="sxs-lookup"><span data-stu-id="01378-189">The database backup for the app is stored in the root of the.zip file.</span></span> <span data-ttu-id="01378-190">Pour une base de données SQL, il s'agit d'un fichier BACPAC (pas d'extension de fichier) qui peut être importé.</span><span class="sxs-lookup"><span data-stu-id="01378-190">For a SQL database, this is a BACPAC file (no file extension) and can be imported.</span></span> <span data-ttu-id="01378-191">Pour créer une base de données SQL en fonction de l’exportation de BACPAC, consultez [Importer un fichier BACPAC pour créer une nouvelle base de données utilisateur](http://technet.microsoft.com/library/hh710052.aspx).</span><span class="sxs-lookup"><span data-stu-id="01378-191">To create a SQL database based on the BACPAC export, see [Import a BACPAC File to Create a New User Database](http://technet.microsoft.com/library/hh710052.aspx).</span></span>

> [!WARNING]
> <span data-ttu-id="01378-192">Toute modification apportée aux fichiers de votre conteneur **websitebackups** peut invalider la sauvegarde et la rendre impossible à restaurer.</span><span class="sxs-lookup"><span data-stu-id="01378-192">Altering any of the files in your **websitebackups** container can cause the backup to become invalid and therefore non-restorable.</span></span>
> 
> 

<a name="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="01378-193">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="01378-193">Next Steps</span></span>
<span data-ttu-id="01378-194">Pour plus d’informations sur la restauration d’une application à partir d’une sauvegarde, consultez [Restauration d’une application dans Azure](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="01378-194">For information on restoring an app from a backup, see [Restore an app in Azure](web-sites-restore.md).</span></span> <span data-ttu-id="01378-195">Vous pouvez également sauvegarder et restaurer des applications App Service à l’aide de l’API REST. Pour cela, consultez [Utilisation de REST pour sauvegarder et restaurer des applications App Service](websites-csm-backup.md).</span><span class="sxs-lookup"><span data-stu-id="01378-195">You can also backup and restore App Service apps using REST API (see [Use REST to backup and restore App Service apps](websites-csm-backup.md)).</span></span>


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

