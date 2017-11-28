---
title: "tâches de base de données élastique aaaInstalling | Documents Microsoft"
description: "Suivez les étapes de fonction de travail élastique hello."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: cbe0aa2b-17e3-4b6f-a16f-6ebc1f5a66af
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 0349f66a4428f81d00d43681d7f2177f273ec032
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="installing-elastic-database-jobs-overview"></a><span data-ttu-id="8752d-103">Vue d’ensemble de l’installation de Tâches de bases de données élastiques</span><span class="sxs-lookup"><span data-stu-id="8752d-103">Installing Elastic Database jobs overview</span></span>
<span data-ttu-id="8752d-104">[**Les travaux de base de données élastiques** ](sql-database-elastic-jobs-overview.md) peut être installé via PowerShell ou via hello Portal.You classique de Azure peuvent avoir accès toocreate et gérer des travaux à l’aide des API PowerShell de hello uniquement si vous installez le package de PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="8752d-104">[**Elastic Database jobs**](sql-database-elastic-jobs-overview.md) can be installed via PowerShell or through hello Azure Classic Portal.You can gain access toocreate and manage jobs using hello PowerShell API only if you install hello PowerShell package.</span></span> <span data-ttu-id="8752d-105">En outre, hello PowerShell APIs fournir beaucoup plus de fonctionnalités que le portail de hello à ce stade.</span><span class="sxs-lookup"><span data-stu-id="8752d-105">Additionally, hello PowerShell APIs provide significantly more functionality than hello portal at this point in time.</span></span>

<span data-ttu-id="8752d-106">Si vous avez déjà installé **des travaux de base de données élastique** via hello portail à partir d’un fichier **pool élastique**, préliminaire Powershell hello inclut des scripts tooupgrade votre installation existante.</span><span class="sxs-lookup"><span data-stu-id="8752d-106">If you have already installed **Elastic Database jobs** through hello Portal from an existing **elastic pool**, hello latest Powershell preview includes scripts tooupgrade your existing installation.</span></span> <span data-ttu-id="8752d-107">Il est fortement recommandé, tooupgrade toohello de votre installation dernières **des travaux de base de données élastique** parti de tootake d’ordre de nouvelles fonctionnalités exposées par le biais des composants hello APIs PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8752d-107">It is highly recommended tooupgrade your installation toohello latest **Elastic Database jobs** components in order tootake advantage of new functionality exposed via hello PowerShell APIs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8752d-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8752d-108">Prerequisites</span></span>
* <span data-ttu-id="8752d-109">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="8752d-109">An Azure subscription.</span></span> <span data-ttu-id="8752d-110">Pour un essai gratuit, consultez [Version d'évaluation gratuite](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8752d-110">For a free trial, see [Free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="8752d-111">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8752d-111">Azure PowerShell.</span></span> <span data-ttu-id="8752d-112">Installer la version la plus récente hello à l’aide de hello [Web Platform Installer](http://go.microsoft.com/fwlink/p/?linkid=320376).</span><span class="sxs-lookup"><span data-stu-id="8752d-112">Install hello latest version using hello [Web Platform Installer](http://go.microsoft.com/fwlink/p/?linkid=320376).</span></span> <span data-ttu-id="8752d-113">Pour plus d’informations, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8752d-113">For detailed information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="8752d-114">[L’utilitaire de ligne de commande NuGet](https://nuget.org/nuget.exe) est utilisé tooinstall hello élastique de base de données du package travaux.</span><span class="sxs-lookup"><span data-stu-id="8752d-114">[NuGet Command-line Utility](https://nuget.org/nuget.exe) is used tooinstall hello Elastic Database jobs package.</span></span> <span data-ttu-id="8752d-115">Pour plus d’informations, consultez http://docs.nuget.org/docs/start-here/installing-nuget.</span><span class="sxs-lookup"><span data-stu-id="8752d-115">For more information, see http://docs.nuget.org/docs/start-here/installing-nuget.</span></span>

## <a name="download-and-import-hello-elastic-database-jobs-powershell-package"></a><span data-ttu-id="8752d-116">Téléchargez et importez le package de PowerShell travaux hello élastique de base de données</span><span class="sxs-lookup"><span data-stu-id="8752d-116">Download and import hello Elastic Database jobs PowerShell package</span></span>
1. <span data-ttu-id="8752d-117">Lancer la fenêtre de commande PowerShell de Microsoft Azure et accédez répertoire toohello où vous avez téléchargé l’utilitaire de ligne de commande NuGet (nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="8752d-117">Launch Microsoft Azure PowerShell command window and navigate toohello directory where you downloaded NuGet Command-line Utility (nuget.exe).</span></span>
2. <span data-ttu-id="8752d-118">Téléchargez et importez **des travaux de base de données élastique** package dans le répertoire en cours de hello avec hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="8752d-118">Download and import **Elastic Database jobs** package into hello current directory with hello following command:</span></span>
   
        PS C:\>.\nuget install Microsoft.Azure.SqlDatabase.Jobs -prerelease
   
    <span data-ttu-id="8752d-119">Hello **des travaux de base de données élastique** fichiers sont placés dans le répertoire local de hello dans un dossier nommé **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x** où *x.x.xxxx.x* reflète le numéro de version hello.</span><span class="sxs-lookup"><span data-stu-id="8752d-119">hello **Elastic Database jobs** files are placed in hello local directory in a folder named **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x** where *x.x.xxxx.x* reflects hello version number.</span></span> <span data-ttu-id="8752d-120">applets de commande PowerShell Hello (y compris les fichiers .dll du client requis) se trouvent dans hello **tools\ElasticDatabaseJobs** sous-répertoire et hello tooinstall de scripts PowerShell, la mise à niveau et désinstaller également résider dans hello  **outils** sous-répertoire.</span><span class="sxs-lookup"><span data-stu-id="8752d-120">hello PowerShell cmdlets (including required client .dlls) are located in hello **tools\ElasticDatabaseJobs** sub-directory and hello PowerShell scripts tooinstall, upgrade and uninstall also reside in hello **tools** sub-directory.</span></span>
3. <span data-ttu-id="8752d-121">Accédez toohello outils sous-répertoire sous hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x dossier en tapant cd outils, par exemple :</span><span class="sxs-lookup"><span data-stu-id="8752d-121">Navigate toohello tools sub-directory under hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x folder by typing cd tools, for example:</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

4. <span data-ttu-id="8752d-122">Exécutez Active ElasticDatabaseJobs de hello.\InstallElasticDatabaseJobsCmdlets.ps1 script toocopy hello dans $home\Documents\WindowsPowerShell\Modules.</span><span class="sxs-lookup"><span data-stu-id="8752d-122">Execute hello .\InstallElasticDatabaseJobsCmdlets.ps1 script toocopy hello ElasticDatabaseJobs directory into $home\Documents\WindowsPowerShell\Modules.</span></span> <span data-ttu-id="8752d-123">Cette opération va automatiquement importer le module hello pour l’utilisation, par exemple :</span><span class="sxs-lookup"><span data-stu-id="8752d-123">This will also automatically import hello module for use, for example:</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobsCmdlets.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobsCmdlets.ps1

## <a name="install-hello-elastic-database-jobs-components-using-powershell"></a><span data-ttu-id="8752d-124">Installer les composants de travaux hello élastique de base de données à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="8752d-124">Install hello Elastic Database jobs components using PowerShell</span></span>
1. <span data-ttu-id="8752d-125">Lancez une fenêtre de commande PowerShell de Microsoft Azure et accédez toohello \tools sous-répertoire sous le dossier de Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x hello : tapez cd \tools</span><span class="sxs-lookup"><span data-stu-id="8752d-125">Launch a Microsoft Azure PowerShell command window and navigate toohello \tools sub-directory under hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x folder: Type cd \tools</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

2. <span data-ttu-id="8752d-126">Exécutez le script PowerShell de.\InstallElasticDatabaseJobs.ps1 hello et fournir des valeurs pour ses variables demandées.</span><span class="sxs-lookup"><span data-stu-id="8752d-126">Execute hello .\InstallElasticDatabaseJobs.ps1 PowerShell script and supply values for its requested variables.</span></span> <span data-ttu-id="8752d-127">Ce script crée les composants hello décrits dans [composants et la tarification des travaux de base de données élastique](sql-database-elastic-jobs-overview.md#components-and-pricing) configuration hello Azure Cloud Service tooappropriately qui l’utilisent les composants dépendants hello.</span><span class="sxs-lookup"><span data-stu-id="8752d-127">This script will create hello components described in [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing) along with configuring hello Azure Cloud Service tooappropriately use hello dependent components.</span></span>

        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobs.ps1

<span data-ttu-id="8752d-128">Lorsque vous exécutez cette commande, une fenêtre s’ouvre dans laquelle vous devez entrer un **nom d’utilisateur** et un **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="8752d-128">When you run this command a window opens asking for a **user name** and **password**.</span></span> <span data-ttu-id="8752d-129">Ce n’est pas vos informations d’identification Azure, entrez le nom d’utilisateur hello et le mot de passe administrateur hello toocreate souhaité pour le nouveau serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="8752d-129">This is not your Azure credentials, enter hello user name and password that will be hello administrator credentials you want toocreate for hello new server.</span></span>

<span data-ttu-id="8752d-130">paramètres Hello fournis dans cet exemple d’appel peuvent être modifiées pour les paramètres de votre choix.</span><span class="sxs-lookup"><span data-stu-id="8752d-130">hello parameters provided on this sample invocation can be modified for your desired settings.</span></span> <span data-ttu-id="8752d-131">suivant de Hello fournit plus d’informations sur le comportement de hello de chaque paramètre :</span><span class="sxs-lookup"><span data-stu-id="8752d-131">hello following provides more information on hello behavior of each parameter:</span></span>

<table style="width:100%">
  <tr>
    <th><span data-ttu-id="8752d-132">Paramètre</span><span class="sxs-lookup"><span data-stu-id="8752d-132">Parameter</span></span></th>
    <th><span data-ttu-id="8752d-133">Description</span><span class="sxs-lookup"><span data-stu-id="8752d-133">Description</span></span></th>
  </tr>

<tr>
    <td><span data-ttu-id="8752d-134">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="8752d-134">ResourceGroupName</span></span></td>
    <td><span data-ttu-id="8752d-135">Fournit le nom de groupe de ressources Azure hello créé hello toocontain nouvellement créé les composants Azure.</span><span class="sxs-lookup"><span data-stu-id="8752d-135">Provides hello Azure resource group name created toocontain hello newly created Azure components.</span></span> <span data-ttu-id="8752d-136">Ce paramètre par défaut est trop « __ElasticDatabaseJob ».</span><span class="sxs-lookup"><span data-stu-id="8752d-136">This parameter defaults too“__ElasticDatabaseJob”.</span></span> <span data-ttu-id="8752d-137">Il n’est pas recommandé toochange cette valeur.</span><span class="sxs-lookup"><span data-stu-id="8752d-137">It is not recommended toochange this value.</span></span></td>
    </tr>

</tr>

    <tr>
    <td><span data-ttu-id="8752d-138">ResourceGroupLocation</span><span class="sxs-lookup"><span data-stu-id="8752d-138">ResourceGroupLocation</span></span></td>
    <td><span data-ttu-id="8752d-139">Fournit des toobe d’emplacement Azure hello utilisé pour hello nouvellement créé les composants Azure.</span><span class="sxs-lookup"><span data-stu-id="8752d-139">Provides hello Azure location toobe used for hello newly created Azure components.</span></span> <span data-ttu-id="8752d-140">Ce paramètre par défaut est toohello emplacement du centre des États-Unis.</span><span class="sxs-lookup"><span data-stu-id="8752d-140">This parameter defaults toohello Central US location.</span></span></td>
</tr>

<tr>
    <td><span data-ttu-id="8752d-141">ServiceWorkerCount</span><span class="sxs-lookup"><span data-stu-id="8752d-141">ServiceWorkerCount</span></span></td>
    <td><span data-ttu-id="8752d-142">Offre plusieurs hello tooinstall de threads de travail de service.</span><span class="sxs-lookup"><span data-stu-id="8752d-142">Provides hello number of service workers tooinstall.</span></span> <span data-ttu-id="8752d-143">Ce paramètre par défaut est too1.</span><span class="sxs-lookup"><span data-stu-id="8752d-143">This parameter defaults too1.</span></span> <span data-ttu-id="8752d-144">Un plus grand nombre de threads de travail peut être utilisé tooscale out hello service tooprovide haute disponibilité et.</span><span class="sxs-lookup"><span data-stu-id="8752d-144">A higher number of workers can be used tooscale out hello service and tooprovide high availability.</span></span> <span data-ttu-id="8752d-145">Il est recommandé de toouse « 2 » pour les déploiements qui nécessitent une haute disponibilité du service de hello.</span><span class="sxs-lookup"><span data-stu-id="8752d-145">It is recommended toouse “2” for deployments that require high availability of hello service.</span></span></td>
    </tr>

</tr>
    <tr>
    <td><span data-ttu-id="8752d-146">ServiceVmSize</span><span class="sxs-lookup"><span data-stu-id="8752d-146">ServiceVmSize</span></span></td>
    <td><span data-ttu-id="8752d-147">Fournit la taille de machine virtuelle hello pour une utilisation dans hello Service Cloud.</span><span class="sxs-lookup"><span data-stu-id="8752d-147">Provides hello VM size for usage within hello Cloud Service.</span></span> <span data-ttu-id="8752d-148">Ce paramètre par défaut est tooA0.</span><span class="sxs-lookup"><span data-stu-id="8752d-148">This parameter defaults tooA0.</span></span> <span data-ttu-id="8752d-149">Les valeurs de paramètres d’A0/A1/A2/A3 sont acceptées obligeant les processus de travail hello rôle toouse une taille ExtraSmall/petit/moyen/grand, respectivement.</span><span class="sxs-lookup"><span data-stu-id="8752d-149">Parameters values of A0/A1/A2/A3 are accepted which cause hello worker role toouse an ExtraSmall/Small/Medium/Large size, respectively.</span></span> <span data-ttu-id="8752d-150">Pour plus d’informations sur les tailles de rôle de travail, consultez [Composants et tarification des tâches de bases de données élastiques](sql-database-elastic-jobs-overview.md#components-and-pricing).</span><span class="sxs-lookup"><span data-stu-id="8752d-150">Fo more information on worker role sizes, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="8752d-151">SqlServerDatabaseSlo</span><span class="sxs-lookup"><span data-stu-id="8752d-151">SqlServerDatabaseSlo</span></span></td>
    <td><span data-ttu-id="8752d-152">Fournit l’objectif de niveau de service hello pour une édition Standard.</span><span class="sxs-lookup"><span data-stu-id="8752d-152">Provides hello service level objective for a Standard edition.</span></span> <span data-ttu-id="8752d-153">Ce paramètre par défaut est tooS0.</span><span class="sxs-lookup"><span data-stu-id="8752d-153">This parameter defaults tooS0.</span></span> <span data-ttu-id="8752d-154">Les valeurs de paramètre de S0/S1/S2/S3 sont acceptées obligeant hello de base de données SQL Azure toouse hello SLO respectif.</span><span class="sxs-lookup"><span data-stu-id="8752d-154">Parameter values of S0/S1/S2/S3 are accepted which cause hello Azure SQL Database toouse hello respective SLO.</span></span> <span data-ttu-id="8752d-155">Pour plus d’informations sur les objectifs de niveau de service SQL Database, consultez [Composants et tarification des tâches de bases de données élastiques](sql-database-elastic-jobs-overview.md#components-and-pricing).</span><span class="sxs-lookup"><span data-stu-id="8752d-155">For more information on SQL Database SLOs, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="8752d-156">SqlServerAdministratorUserName</span><span class="sxs-lookup"><span data-stu-id="8752d-156">SqlServerAdministratorUserName</span></span></td>
    <td><span data-ttu-id="8752d-157">Fournit le nom d’utilisateur admin hello pour hello créé sur le serveur de base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="8752d-157">Provides hello admin user name for hello newly created Azure SQL Database server.</span></span> <span data-ttu-id="8752d-158">Lorsque ne pas spécifié, une fenêtre d’informations d’identification PowerShell s’ouvre tooprompt pour des informations d’identification hello.</span><span class="sxs-lookup"><span data-stu-id="8752d-158">When not specified, a PowerShell credentials window will open tooprompt for hello credentials.</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="8752d-159">SqlServerAdministratorPassword</span><span class="sxs-lookup"><span data-stu-id="8752d-159">SqlServerAdministratorPassword</span></span></td>
    <td><span data-ttu-id="8752d-160">Fournit un mot de passe administrateur hello pour hello créé sur le serveur de base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="8752d-160">Provides hello admin password for hello newly created Azure SQL Database server.</span></span> <span data-ttu-id="8752d-161">Quand il est ne pas fourni, une fenêtre d’informations d’identification PowerShell s’ouvre tooprompt pour des informations d’identification hello.</span><span class="sxs-lookup"><span data-stu-id="8752d-161">When not provided, a PowerShell credentials window will open tooprompt for hello credentials.</span></span></td>
</tr>
</table>

<span data-ttu-id="8752d-162">Pour les systèmes qui ciblent de très nombreux de travaux en cours d’exécution en parallèle sur un grand nombre de bases de données, il est recommandé de toospecify paramètres tels que : - ServiceWorkerCount 2 - ServiceVmSize A2 - SqlServerDatabaseSlo S2.</span><span class="sxs-lookup"><span data-stu-id="8752d-162">For systems that target having large numbers of jobs running in parallel against a large number of databases, it is recommended toospecify parameters such as: -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2.</span></span>

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\InstallElasticDatabaseJobs.ps1 -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2

## <a name="update-an-existing-elastic-database-jobs-components-installation-using-powershell"></a><span data-ttu-id="8752d-163">Mettez à jour une installation de composants de Tâches de bases de données élastiques existante à l'aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="8752d-163">Update an existing Elastic Database jobs components installation using PowerShell</span></span>
<span data-ttu-id="8752d-164">**Tâches de bases de données élastiques** peut être mis à jour dans une installation existante pour assurer la mise à l'échelle et la haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="8752d-164">**Elastic Database jobs** can be updated within an existing installation for scale and high-availability.</span></span> <span data-ttu-id="8752d-165">Ce processus permet de futures mises à niveau du code de service sans avoir toodrop et recréer la base de données de contrôle hello.</span><span class="sxs-lookup"><span data-stu-id="8752d-165">This process allows for future upgrades of service code without having toodrop and recreate hello control database.</span></span> <span data-ttu-id="8752d-166">Ce processus peut également être utilisé au sein de hello même version toomodify hello service taille ou hello serveur worker nombre d’ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="8752d-166">This process can also be used within hello same version toomodify hello service VM size or hello server worker count.</span></span>

<span data-ttu-id="8752d-167">taille de machine virtuelle tooupdate hello d’une installation, hello exécution suivante du script avec les paramètres mis à jour toohello les valeurs de votre choix.</span><span class="sxs-lookup"><span data-stu-id="8752d-167">tooupdate hello VM size of an installation, run hello following script with parameters updated toohello values of your choice.</span></span>

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\UpdateElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\UpdateElasticDatabaseJobs.ps1 -ServiceVmSize A1 -ServiceWorkerCount 2

<table style="width:100%">
  <tr>
  <th><span data-ttu-id="8752d-168">Paramètre</span><span class="sxs-lookup"><span data-stu-id="8752d-168">Parameter</span></span></th>
  <th><span data-ttu-id="8752d-169">Description</span><span class="sxs-lookup"><span data-stu-id="8752d-169">Description</span></span></th>
</tr>

  <tr>
    <td><span data-ttu-id="8752d-170">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="8752d-170">ResourceGroupName</span></span></td>
    <td><span data-ttu-id="8752d-171">Identifie le nom de groupe de ressources Azure hello utilisé lorsque les composants de tâche hello élastique de base de données ont été installés initialement.</span><span class="sxs-lookup"><span data-stu-id="8752d-171">Identifies hello Azure resource group name used when hello Elastic Database job components were initially installed.</span></span> <span data-ttu-id="8752d-172">Ce paramètre par défaut est trop « __ElasticDatabaseJob ».</span><span class="sxs-lookup"><span data-stu-id="8752d-172">This parameter defaults too“__ElasticDatabaseJob”.</span></span> <span data-ttu-id="8752d-173">Dans la mesure où il n’est pas recommandé toochange cette valeur, vous ne devez pas avoir toospecify ce paramètre.</span><span class="sxs-lookup"><span data-stu-id="8752d-173">Since it is not recommended toochange this value, you shouldn't have toospecify this parameter.</span></span></td>
    </tr>
</tr>

</tr>

  <tr>
    <td><span data-ttu-id="8752d-174">ServiceWorkerCount</span><span class="sxs-lookup"><span data-stu-id="8752d-174">ServiceWorkerCount</span></span></td>
    <td><span data-ttu-id="8752d-175">Offre plusieurs hello tooinstall de threads de travail de service.</span><span class="sxs-lookup"><span data-stu-id="8752d-175">Provides hello number of service workers tooinstall.</span></span>  <span data-ttu-id="8752d-176">Ce paramètre par défaut est too1.</span><span class="sxs-lookup"><span data-stu-id="8752d-176">This parameter defaults too1.</span></span>  <span data-ttu-id="8752d-177">Un plus grand nombre de threads de travail peut être utilisé tooscale out hello service tooprovide haute disponibilité et.</span><span class="sxs-lookup"><span data-stu-id="8752d-177">A higher number of workers can be used tooscale out hello service and tooprovide high availability.</span></span>  <span data-ttu-id="8752d-178">Il est recommandé de toouse « 2 » pour les déploiements qui nécessitent une haute disponibilité du service de hello.</span><span class="sxs-lookup"><span data-stu-id="8752d-178">It is recommended toouse “2” for deployments that require high availability of hello service.</span></span></td>
</tr>

</tr>

    <tr>
    <td><span data-ttu-id="8752d-179">ServiceVmSize</span><span class="sxs-lookup"><span data-stu-id="8752d-179">ServiceVmSize</span></span></td>
    <td><span data-ttu-id="8752d-180">Fournit la taille de machine virtuelle hello pour une utilisation dans hello Service Cloud.</span><span class="sxs-lookup"><span data-stu-id="8752d-180">Provides hello VM size for usage within hello Cloud Service.</span></span> <span data-ttu-id="8752d-181">Ce paramètre par défaut est tooA0.</span><span class="sxs-lookup"><span data-stu-id="8752d-181">This parameter defaults tooA0.</span></span> <span data-ttu-id="8752d-182">Les valeurs de paramètres d’A0/A1/A2/A3 sont acceptées obligeant les processus de travail hello rôle toouse une taille ExtraSmall/petit/moyen/grand, respectivement.</span><span class="sxs-lookup"><span data-stu-id="8752d-182">Parameters values of A0/A1/A2/A3 are accepted which cause hello worker role toouse an ExtraSmall/Small/Medium/Large size, respectively.</span></span> <span data-ttu-id="8752d-183">Pour plus d’informations sur les tailles de rôle de travail, consultez [Composants et tarification des tâches de bases de données élastiques](sql-database-elastic-jobs-overview.md#components-and-pricing).</span><span class="sxs-lookup"><span data-stu-id="8752d-183">Fo more information on worker role sizes, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</table>

## <a name="install-hello-elastic-database-jobs-components-using-hello-portal"></a><span data-ttu-id="8752d-184">Installer les composants de travaux hello élastique de base de données à l’aide de hello portail</span><span class="sxs-lookup"><span data-stu-id="8752d-184">Install hello Elastic Database jobs components using hello Portal</span></span>
<span data-ttu-id="8752d-185">Une fois que vous avez [créé un pool élastique](sql-database-elastic-pool-manage-portal.md), vous pouvez installer **des travaux de base de données élastique** l’exécution de tooenable composants des tâches d’administration sur chaque base de données dans le pool élastique de hello.</span><span class="sxs-lookup"><span data-stu-id="8752d-185">Once you have [created an elastic pool](sql-database-elastic-pool-manage-portal.md), you can install **Elastic Database jobs** components tooenable execution of administrative tasks against each database in hello elastic pool.</span></span> <span data-ttu-id="8752d-186">Contrairement aux lorsque à l’aide de hello **des travaux de base de données élastique** PowerShell APIs, interface du portail hello est actuellement restreint tooonly l’exécution par rapport à un pool existant.</span><span class="sxs-lookup"><span data-stu-id="8752d-186">Unlike when using hello **Elastic Database jobs** PowerShell APIs, hello portal interface is currently restricted tooonly executing against an existing pool.</span></span>

<span data-ttu-id="8752d-187">**Estimation du temps toocomplete :** 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="8752d-187">**Estimated time toocomplete:** 10 minutes.</span></span>

1. <span data-ttu-id="8752d-188">À partir de l’affichage de tableau de bord hello du pool élastique de hello via hello [Azure Portal](https://portal.azure.com/#) , cliquez sur **travail de création de**.</span><span class="sxs-lookup"><span data-stu-id="8752d-188">From hello dashboard view of hello elastic pool via hello [Azure Portal](https://portal.azure.com/#) , click **Create job**.</span></span>
2. <span data-ttu-id="8752d-189">Si vous créez un travail pour hello première fois, vous devez installer **des travaux de base de données élastique** en cliquant sur **les termes du contrat de l’aperçu**.</span><span class="sxs-lookup"><span data-stu-id="8752d-189">If you are creating a job for hello first time, you must install **Elastic Database jobs** by clicking **PREVIEW TERMS**.</span></span>
3. <span data-ttu-id="8752d-190">Accepter les termes du contrat de hello en cliquant sur hello case à cocher.</span><span class="sxs-lookup"><span data-stu-id="8752d-190">Accept hello terms by clicking hello checkbox.</span></span>
4. <span data-ttu-id="8752d-191">Dans la vue de hello « installer les services », cliquez sur **informations d’identification du travail**.</span><span class="sxs-lookup"><span data-stu-id="8752d-191">In hello "Install services" view, click **JOB CREDENTIALS**.</span></span>
   
    ![L’installation des services de hello][1]
5. <span data-ttu-id="8752d-193">Tapez un nom d'utilisateur et un mot de passe d'administrateur de base de données. Dans le cadre de l’installation de hello, un nouveau serveur de base de données SQL Azure est créé.</span><span class="sxs-lookup"><span data-stu-id="8752d-193">Type a user name and password for a database admin. As part of hello installation, a new Azure SQL Database server is created.</span></span> <span data-ttu-id="8752d-194">Dans ce nouveau serveur, une base de données, appelé base de données du contrôle hello, est créé et utilisé des métadonnées de toocontain hello pour les travaux de la base de données élastique.</span><span class="sxs-lookup"><span data-stu-id="8752d-194">Within this new server, a new database, known as hello control database, is created and used toocontain hello meta data for Elastic Database jobs.</span></span> <span data-ttu-id="8752d-195">nom d’utilisateur Hello et mot de passe créés ici sont utilisés à des fins de hello de la journalisation dans la base de données de contrôle toohello.</span><span class="sxs-lookup"><span data-stu-id="8752d-195">hello user name and password created here are used for hello purpose of logging in toohello control database.</span></span> <span data-ttu-id="8752d-196">Informations d’identification distincte sont utilisée pour l’exécution du script par rapport aux bases de données hello dans le pool de hello.</span><span class="sxs-lookup"><span data-stu-id="8752d-196">A separate credential is used for script execution against hello databases within hello pool.</span></span>
   
    ![Créer le nom d'utilisateur et le mot de passe][2]
6. <span data-ttu-id="8752d-198">Cliquez sur le bouton OK de hello.</span><span class="sxs-lookup"><span data-stu-id="8752d-198">Click hello OK button.</span></span> <span data-ttu-id="8752d-199">composants de Hello sont créés pour vous dans quelques minutes dans un nouveau [groupe de ressources](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8752d-199">hello components are created for you in a few minutes in a new [Resource group](../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="8752d-200">nouveau groupe de ressources Hello est épinglé toohello démarrer le tableau, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="8752d-200">hello new resource group is pinned toohello start board, as shown below.</span></span> <span data-ttu-id="8752d-201">Les travaux de base de données une fois créés, élastique (Service de cloud computing, de la base de données SQL, Service Bus et stockage) sont créés dans le groupe de hello.</span><span class="sxs-lookup"><span data-stu-id="8752d-201">Once created, elastic database jobs (Cloud Service, SQL Database, Service Bus, and Storage) are all created in hello group.</span></span>
   
    ![groupe de ressources dans le panneau de démarrage][3]
7. <span data-ttu-id="8752d-203">Si vous essayez de toocreate ou gérer un travail pendant que les tâches de base de données élastique s’installe lorsque vous fournissez **informations d’identification** hello message suivant s’affiche.</span><span class="sxs-lookup"><span data-stu-id="8752d-203">If you attempt toocreate or manage a job while elastic database jobs is installing, when providing **Credentials** you will see hello following message.</span></span>
   
    ![Déploiement en cours][4]

<span data-ttu-id="8752d-205">Si la désinstallation est nécessaire, supprimer le groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="8752d-205">If uninstallation is required, delete hello resource group.</span></span> <span data-ttu-id="8752d-206">Consultez [comment toouninstall hello élastique de base de données de la tâche composants](sql-database-elastic-jobs-uninstall.md).</span><span class="sxs-lookup"><span data-stu-id="8752d-206">See [How toouninstall hello Elastic Database job components](sql-database-elastic-jobs-uninstall.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8752d-207">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8752d-207">Next steps</span></span>
<span data-ttu-id="8752d-208">Vérifiez les informations d’identification avec les droits appropriés hello pour l’exécution du script est créée sur chaque base de données dans le groupe de hello, pour plus d’informations, consultez [sécurisation de votre base de données SQL](sql-database-manage-logins.md).</span><span class="sxs-lookup"><span data-stu-id="8752d-208">Ensure a credential with hello appropriate rights for script execution is created on each database in hello group, for more information see [Securing your SQL Database](sql-database-manage-logins.md).</span></span>
<span data-ttu-id="8752d-209">Consultez [création et gestion des travaux d’une base de données élastique](sql-database-elastic-jobs-create-and-manage.md) tooget a démarré.</span><span class="sxs-lookup"><span data-stu-id="8752d-209">See [Creating and managing an Elastic Database jobs](sql-database-elastic-jobs-create-and-manage.md) tooget started.</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-service-installation/screen-1.png
[2]: ./media/sql-database-elastic-jobs-service-installation/credentials.png
[3]: ./media/sql-database-elastic-jobs-service-installation/start-board.png
[4]: ./media/sql-database-elastic-jobs-service-installation/not-done.png
