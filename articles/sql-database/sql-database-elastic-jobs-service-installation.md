---
title: "Installation de Tâches de bases de données élastiques | Microsoft Docs"
description: "Passez en revue l'installation de la fonctionnalité de tâche élastique."
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
ms.openlocfilehash: e7a2d6dbcefbb31d76257eaf96ccc235d7a29416
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="installing-elastic-database-jobs-overview"></a><span data-ttu-id="b5a4f-103">Vue d’ensemble de l’installation de Tâches de bases de données élastiques</span><span class="sxs-lookup"><span data-stu-id="b5a4f-103">Installing Elastic Database jobs overview</span></span>
<span data-ttu-id="b5a4f-104">Une [**tâche de base de données élastique**](sql-database-elastic-jobs-overview.md) peut être installée à l’aide de PowerShell ou du portail Azure Classic. Vous pouvez y accéder pour créer et gérer des tâches à l’aide de l’API PowerShell uniquement si vous installez le package PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-104">[**Elastic Database jobs**](sql-database-elastic-jobs-overview.md) can be installed via PowerShell or through the Azure Classic Portal.You can gain access to create and manage jobs using the PowerShell API only if you install the PowerShell package.</span></span> <span data-ttu-id="b5a4f-105">En outre, les API PowerShell fournissent, à ce stade, beaucoup plus de fonctionnalités que le portail.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-105">Additionally, the PowerShell APIs provide significantly more functionality than the portal at this point in time.</span></span>

<span data-ttu-id="b5a4f-106">Si vous avez déjà installé **Tâche de base de données élastique** via le portail à partir d’un **pool élastique** existant, la dernière version préliminaire de Powershell inclut des scripts pour mettre à niveau votre installation existante.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-106">If you have already installed **Elastic Database jobs** through the Portal from an existing **elastic pool**, the latest Powershell preview includes scripts to upgrade your existing installation.</span></span> <span data-ttu-id="b5a4f-107">Il est vivement recommandé de mettre à niveau votre installation vers la dernière version des composants de **Tâches de bases de données élastiques** pour tirer parti des nouvelles fonctionnalités exposées via l'API PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-107">It is highly recommended to upgrade your installation to the latest **Elastic Database jobs** components in order to take advantage of new functionality exposed via the PowerShell APIs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b5a4f-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b5a4f-108">Prerequisites</span></span>
* <span data-ttu-id="b5a4f-109">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-109">An Azure subscription.</span></span> <span data-ttu-id="b5a4f-110">Pour un essai gratuit, consultez [Version d'évaluation gratuite](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b5a4f-110">For a free trial, see [Free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="b5a4f-111">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-111">Azure PowerShell.</span></span> <span data-ttu-id="b5a4f-112">Installez la dernière version via [Web Platform Installer](http://go.microsoft.com/fwlink/p/?linkid=320376).</span><span class="sxs-lookup"><span data-stu-id="b5a4f-112">Install the latest version using the [Web Platform Installer](http://go.microsoft.com/fwlink/p/?linkid=320376).</span></span> <span data-ttu-id="b5a4f-113">Pour plus de détails, consultez la rubrique [Installation et configuration d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b5a4f-113">For detailed information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="b5a4f-114">[utilitaire de ligne de commande NuGet](https://nuget.org/nuget.exe) est utilisé pour installer le package Tâches de bases de données élastiques.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-114">[NuGet Command-line Utility](https://nuget.org/nuget.exe) is used to install the Elastic Database jobs package.</span></span> <span data-ttu-id="b5a4f-115">Pour plus d’informations, consultez http://docs.nuget.org/docs/start-here/installing-nuget.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-115">For more information, see http://docs.nuget.org/docs/start-here/installing-nuget.</span></span>

## <a name="download-and-import-the-elastic-database-jobs-powershell-package"></a><span data-ttu-id="b5a4f-116">Téléchargez et importez le package Tâches de bases de données élastiques PowerShell</span><span class="sxs-lookup"><span data-stu-id="b5a4f-116">Download and import the Elastic Database jobs PowerShell package</span></span>
1. <span data-ttu-id="b5a4f-117">Lancez la fenêtre de commande Microsoft Azure PowerShell et accédez au répertoire où vous avez téléchargé l’utilitaire de ligne de commande NuGet (nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="b5a4f-117">Launch Microsoft Azure PowerShell command window and navigate to the directory where you downloaded NuGet Command-line Utility (nuget.exe).</span></span>
2. <span data-ttu-id="b5a4f-118">Téléchargez et importez le package **Tâches de bases de données élastiques** dans le répertoire actuel à l'aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b5a4f-118">Download and import **Elastic Database jobs** package into the current directory with the following command:</span></span>
   
        PS C:\>.\nuget install Microsoft.Azure.SqlDatabase.Jobs -prerelease
   
    <span data-ttu-id="b5a4f-119">Les fichiers **Tâche de base de données élastique** sont placés dans un dossier du répertoire local nommé **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x** où *x.x.xxxx.x* correspond au numéro de version.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-119">The **Elastic Database jobs** files are placed in the local directory in a folder named **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x** where *x.x.xxxx.x* reflects the version number.</span></span> <span data-ttu-id="b5a4f-120">Les applets de commande PowerShell (y compris les .dll clients requis) se trouvent dans le sous-répertoire **tools\ElasticDatabaseJobs** et les scripts PowerShell d’installation, de mise à niveau et de désinstallation résident également dans le sous-répertoire **tools**.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-120">The PowerShell cmdlets (including required client .dlls) are located in the **tools\ElasticDatabaseJobs** sub-directory and the PowerShell scripts to install, upgrade and uninstall also reside in the **tools** sub-directory.</span></span>
3. <span data-ttu-id="b5a4f-121">Accédez au sous-répertoire tools sous le dossier Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x en tapant cd tools, par exemple :</span><span class="sxs-lookup"><span data-stu-id="b5a4f-121">Navigate to the tools sub-directory under the Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x folder by typing cd tools, for example:</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

4. <span data-ttu-id="b5a4f-122">Exécutez le script .\InstallElasticDatabaseJobsCmdlets.ps1 pour copier le répertoire ElasticDatabaseJobs dans $home\Documents\WindowsPowerShell\Modules.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-122">Execute the .\InstallElasticDatabaseJobsCmdlets.ps1 script to copy the ElasticDatabaseJobs directory into $home\Documents\WindowsPowerShell\Modules.</span></span> <span data-ttu-id="b5a4f-123">Ceci importera automatiquement le module à utiliser, par exemple :</span><span class="sxs-lookup"><span data-stu-id="b5a4f-123">This will also automatically import the module for use, for example:</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobsCmdlets.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobsCmdlets.ps1

## <a name="install-the-elastic-database-jobs-components-using-powershell"></a><span data-ttu-id="b5a4f-124">Installez les composants de Tâches de bases de données élastiques à l'aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="b5a4f-124">Install the Elastic Database jobs components using PowerShell</span></span>
1. <span data-ttu-id="b5a4f-125">Lancez une fenêtre de commande Microsoft Azure PowerShell et accédez au sous-répertoire \tools sous le dossier Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x : tapez cd \tools</span><span class="sxs-lookup"><span data-stu-id="b5a4f-125">Launch a Microsoft Azure PowerShell command window and navigate to the \tools sub-directory under the Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x folder: Type cd \tools</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

2. <span data-ttu-id="b5a4f-126">Exécutez le script PowerShell .\InstallElasticDatabaseJobs.ps1 et fournissez des valeurs pour ses variables requises.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-126">Execute the .\InstallElasticDatabaseJobs.ps1 PowerShell script and supply values for its requested variables.</span></span> <span data-ttu-id="b5a4f-127">Ce script crée les composants décrits dans [Composants et tarification de Tâches de bases de données élastiques](sql-database-elastic-jobs-overview.md#components-and-pricing) , ainsi que la configuration du service cloud Azure, pour utiliser correctement les composants dépendants.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-127">This script will create the components described in [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing) along with configuring the Azure Cloud Service to appropriately use the dependent components.</span></span>

        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobs.ps1

<span data-ttu-id="b5a4f-128">Lorsque vous exécutez cette commande, une fenêtre s’ouvre dans laquelle vous devez entrer un **nom d’utilisateur** et un **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-128">When you run this command a window opens asking for a **user name** and **password**.</span></span> <span data-ttu-id="b5a4f-129">Il ne s'agit pas de vos informations d'identification Azure. Entrez le nom d'utilisateur et le mot de passe qui seront les informations d'identification d'administrateur que vous souhaitez créer pour le nouveau serveur.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-129">This is not your Azure credentials, enter the user name and password that will be the administrator credentials you want to create for the new server.</span></span>

<span data-ttu-id="b5a4f-130">Les paramètres fournis dans cet exemple d'appel peuvent être remplacés par les paramètres souhaités.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-130">The parameters provided on this sample invocation can be modified for your desired settings.</span></span> <span data-ttu-id="b5a4f-131">La liste suivante vous fournit plus d'informations sur le comportement de chaque paramètre :</span><span class="sxs-lookup"><span data-stu-id="b5a4f-131">The following provides more information on the behavior of each parameter:</span></span>

<table style="width:100%">
  <tr>
    <th><span data-ttu-id="b5a4f-132">Paramètre</span><span class="sxs-lookup"><span data-stu-id="b5a4f-132">Parameter</span></span></th>
    <th><span data-ttu-id="b5a4f-133">Description</span><span class="sxs-lookup"><span data-stu-id="b5a4f-133">Description</span></span></th>
  </tr>

<tr>
    <td><span data-ttu-id="b5a4f-134">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="b5a4f-134">ResourceGroupName</span></span></td>
    <td><span data-ttu-id="b5a4f-135">Fournit le nom du groupe de ressources Azure créé pour contenir les composants Azure nouvellement créés.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-135">Provides the Azure resource group name created to contain the newly created Azure components.</span></span> <span data-ttu-id="b5a4f-136">Ce paramètre est défini par défaut sur la valeur «&#160;__ElasticDatabaseJob&#160;».</span><span class="sxs-lookup"><span data-stu-id="b5a4f-136">This parameter defaults to “__ElasticDatabaseJob”.</span></span> <span data-ttu-id="b5a4f-137">Il n'est pas recommandé de modifier cette valeur.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-137">It is not recommended to change this value.</span></span></td>
    </tr>

</tr>

    <tr>
    <td><span data-ttu-id="b5a4f-138">ResourceGroupLocation</span><span class="sxs-lookup"><span data-stu-id="b5a4f-138">ResourceGroupLocation</span></span></td>
    <td><span data-ttu-id="b5a4f-139">Fournit l'emplacement Azure à utiliser pour les composants Azure nouvellement créés.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-139">Provides the Azure location to be used for the newly created Azure components.</span></span> <span data-ttu-id="b5a4f-140">Ce paramètre est défini par défaut sur  l'emplacement du centre des États-Unis.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-140">This parameter defaults to the Central US location.</span></span></td>
</tr>

<tr>
    <td><span data-ttu-id="b5a4f-141">ServiceWorkerCount</span><span class="sxs-lookup"><span data-stu-id="b5a4f-141">ServiceWorkerCount</span></span></td>
    <td><span data-ttu-id="b5a4f-142">Fournit le nombre de travaux de service à installer.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-142">Provides the number of service workers to install.</span></span> <span data-ttu-id="b5a4f-143">Ce paramètre est défini par défaut sur la valeur 1.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-143">This parameter defaults to 1.</span></span> <span data-ttu-id="b5a4f-144">Un nombre plus élevé de travaux peut permettre de faire évoluer le service et de fournir une haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-144">A higher number of workers can be used to scale out the service and to provide high availability.</span></span> <span data-ttu-id="b5a4f-145">Il est recommandé d'utiliser la valeur « 2 » pour les déploiements qui nécessitent une haute disponibilité du service.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-145">It is recommended to use “2” for deployments that require high availability of the service.</span></span></td>
    </tr>

</tr>
    <tr>
    <td><span data-ttu-id="b5a4f-146">ServiceVmSize</span><span class="sxs-lookup"><span data-stu-id="b5a4f-146">ServiceVmSize</span></span></td>
    <td><span data-ttu-id="b5a4f-147">Fournit la taille de machine virtuelle pour une utilisation dans le service cloud.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-147">Provides the VM size for usage within the Cloud Service.</span></span> <span data-ttu-id="b5a4f-148">Ce paramètre est défini par défaut sur la valeur A0.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-148">This parameter defaults to A0.</span></span> <span data-ttu-id="b5a4f-149">Les valeurs de paramètres A0/A1/A2/A3 sont acceptées, ce qui amène le rôle de travail à utiliser, respectivement, une très petite/petite/moyenne/grande taille.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-149">Parameters values of A0/A1/A2/A3 are accepted which cause the worker role to use an ExtraSmall/Small/Medium/Large size, respectively.</span></span> <span data-ttu-id="b5a4f-150">Pour plus d’informations sur les tailles de rôle de travail, consultez [Composants et tarification des tâches de bases de données élastiques](sql-database-elastic-jobs-overview.md#components-and-pricing).</span><span class="sxs-lookup"><span data-stu-id="b5a4f-150">Fo more information on worker role sizes, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="b5a4f-151">SqlServerDatabaseSlo</span><span class="sxs-lookup"><span data-stu-id="b5a4f-151">SqlServerDatabaseSlo</span></span></td>
    <td><span data-ttu-id="b5a4f-152">Fournit l'objectif de niveau de service d’une édition standard.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-152">Provides the service level objective for a Standard edition.</span></span> <span data-ttu-id="b5a4f-153">Ce paramètre est défini par défaut sur la valeur S0.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-153">This parameter defaults to S0.</span></span> <span data-ttu-id="b5a4f-154">Les valeurs de paramètres S0/S1/S2/S3 sont acceptées, ce qui amène la base de données SQL&#160;Azure à utiliser l’objectif de niveau de service correspondant.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-154">Parameter values of S0/S1/S2/S3 are accepted which cause the Azure SQL Database to use the respective SLO.</span></span> <span data-ttu-id="b5a4f-155">Pour plus d’informations sur les objectifs de niveau de service SQL Database, consultez [Composants et tarification des tâches de bases de données élastiques](sql-database-elastic-jobs-overview.md#components-and-pricing).</span><span class="sxs-lookup"><span data-stu-id="b5a4f-155">For more information on SQL Database SLOs, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="b5a4f-156">SqlServerAdministratorUserName</span><span class="sxs-lookup"><span data-stu-id="b5a4f-156">SqlServerAdministratorUserName</span></span></td>
    <td><span data-ttu-id="b5a4f-157">Fournit le nom d'utilisateur administrateur du serveur de base de données SQL Azure nouvellement créé.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-157">Provides the admin user name for the newly created Azure SQL Database server.</span></span> <span data-ttu-id="b5a4f-158">S’il n’est pas spécifié, une fenêtre d'informations d'identification PowerShell apparaît et vous demande de fournir les informations d'identification.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-158">When not specified, a PowerShell credentials window will open to prompt for the credentials.</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="b5a4f-159">SqlServerAdministratorPassword</span><span class="sxs-lookup"><span data-stu-id="b5a4f-159">SqlServerAdministratorPassword</span></span></td>
    <td><span data-ttu-id="b5a4f-160">Fournit le mot de passe administrateur du serveur de base de données SQL Azure nouvellement créé.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-160">Provides the admin password for the newly created Azure SQL Database server.</span></span> <span data-ttu-id="b5a4f-161">S’il n’est pas fourni, une fenêtre d'informations d'identification PowerShell apparaît et vous demande de fournir les informations d'identification.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-161">When not provided, a PowerShell credentials window will open to prompt for the credentials.</span></span></td>
</tr>
</table>

<span data-ttu-id="b5a4f-162">Pour les systèmes qui ciblent un très grand nombre de tâches s’exécutant en parallèle sur de nombreuses bases de données, il est vivement recommandé de spécifier des paramètres tels que : - ServiceWorkerCount 2 - ServiceVmSize A2 - SqlServerDatabaseSlo S2.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-162">For systems that target having large numbers of jobs running in parallel against a large number of databases, it is recommended to specify parameters such as: -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2.</span></span>

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\InstallElasticDatabaseJobs.ps1 -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2

## <a name="update-an-existing-elastic-database-jobs-components-installation-using-powershell"></a><span data-ttu-id="b5a4f-163">Mettez à jour une installation de composants de Tâches de bases de données élastiques existante à l'aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="b5a4f-163">Update an existing Elastic Database jobs components installation using PowerShell</span></span>
<span data-ttu-id="b5a4f-164">**Tâches de bases de données élastiques** peut être mis à jour dans une installation existante pour assurer la mise à l'échelle et la haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-164">**Elastic Database jobs** can be updated within an existing installation for scale and high-availability.</span></span> <span data-ttu-id="b5a4f-165">Ce processus permet d’effectuer ultérieurement des mises à niveau du code de service sans avoir à supprimer et recréer la base de données de contrôle.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-165">This process allows for future upgrades of service code without having to drop and recreate the control database.</span></span> <span data-ttu-id="b5a4f-166">Il peut également être utilisé sur la même version pour modifier la taille de la machine virtuelle du service ou le nombre de travaux de serveur.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-166">This process can also be used within the same version to modify the service VM size or the server worker count.</span></span>

<span data-ttu-id="b5a4f-167">Pour mettre à jour la taille de la machine virtuelle d’une installation, exécutez le script suivant via les paramètres mis à jour avec les valeurs de votre choix.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-167">To update the VM size of an installation, run the following script with parameters updated to the values of your choice.</span></span>

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\UpdateElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\UpdateElasticDatabaseJobs.ps1 -ServiceVmSize A1 -ServiceWorkerCount 2

<table style="width:100%">
  <tr>
  <th><span data-ttu-id="b5a4f-168">Paramètre</span><span class="sxs-lookup"><span data-stu-id="b5a4f-168">Parameter</span></span></th>
  <th><span data-ttu-id="b5a4f-169">Description</span><span class="sxs-lookup"><span data-stu-id="b5a4f-169">Description</span></span></th>
</tr>

  <tr>
    <td><span data-ttu-id="b5a4f-170">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="b5a4f-170">ResourceGroupName</span></span></td>
    <td><span data-ttu-id="b5a4f-171">Identifie le nom du groupe de ressources Azure utilisé lorsque les composants de Tâches de bases de données élastiques ont été initialement installés.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-171">Identifies the Azure resource group name used when the Elastic Database job components were initially installed.</span></span> <span data-ttu-id="b5a4f-172">Ce paramètre est défini par défaut sur la valeur « __ElasticDatabaseJob ».</span><span class="sxs-lookup"><span data-stu-id="b5a4f-172">This parameter defaults to “__ElasticDatabaseJob”.</span></span> <span data-ttu-id="b5a4f-173">Puisqu’il n'est pas recommandé de modifier cette valeur, vous ne devriez pas spécifier ce paramètre.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-173">Since it is not recommended to change this value, you shouldn't have to specify this parameter.</span></span></td>
    </tr>
</tr>

</tr>

  <tr>
    <td><span data-ttu-id="b5a4f-174">ServiceWorkerCount</span><span class="sxs-lookup"><span data-stu-id="b5a4f-174">ServiceWorkerCount</span></span></td>
    <td><span data-ttu-id="b5a4f-175">Fournit le nombre de travaux de service à installer.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-175">Provides the number of service workers to install.</span></span>  <span data-ttu-id="b5a4f-176">Ce paramètre est défini par défaut sur la valeur 1.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-176">This parameter defaults to 1.</span></span>  <span data-ttu-id="b5a4f-177">Un nombre plus élevé de travaux peut permettre de faire évoluer le service et de fournir une haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-177">A higher number of workers can be used to scale out the service and to provide high availability.</span></span>  <span data-ttu-id="b5a4f-178">Il est recommandé d'utiliser la valeur « 2 » pour les déploiements qui nécessitent une haute disponibilité du service.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-178">It is recommended to use “2” for deployments that require high availability of the service.</span></span></td>
</tr>

</tr>

    <tr>
    <td><span data-ttu-id="b5a4f-179">ServiceVmSize</span><span class="sxs-lookup"><span data-stu-id="b5a4f-179">ServiceVmSize</span></span></td>
    <td><span data-ttu-id="b5a4f-180">Fournit la taille de machine virtuelle pour une utilisation dans le service cloud.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-180">Provides the VM size for usage within the Cloud Service.</span></span> <span data-ttu-id="b5a4f-181">Ce paramètre est défini par défaut sur la valeur A0.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-181">This parameter defaults to A0.</span></span> <span data-ttu-id="b5a4f-182">Les valeurs de paramètres A0/A1/A2/A3 sont acceptées, ce qui amène le rôle de travail à utiliser, respectivement, une très petite/petite/moyenne/grande taille.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-182">Parameters values of A0/A1/A2/A3 are accepted which cause the worker role to use an ExtraSmall/Small/Medium/Large size, respectively.</span></span> <span data-ttu-id="b5a4f-183">Pour plus d’informations sur les tailles de rôle de travail, consultez [Composants et tarification des tâches de bases de données élastiques](sql-database-elastic-jobs-overview.md#components-and-pricing).</span><span class="sxs-lookup"><span data-stu-id="b5a4f-183">Fo more information on worker role sizes, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</table>

## <a name="install-the-elastic-database-jobs-components-using-the-portal"></a><span data-ttu-id="b5a4f-184">Installez les composants de Tâches de bases de données élastiques à l'aide du portail</span><span class="sxs-lookup"><span data-stu-id="b5a4f-184">Install the Elastic Database jobs components using the Portal</span></span>
<span data-ttu-id="b5a4f-185">Une fois que vous avez [créé un pool élastique](sql-database-elastic-pool-manage-portal.md), vous pouvez installer les composants de **Tâches de bases de données élastiques** pour activer l'exécution des tâches d'administration dans chaque base de données du pool élastique.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-185">Once you have [created an elastic pool](sql-database-elastic-pool-manage-portal.md), you can install **Elastic Database jobs** components to enable execution of administrative tasks against each database in the elastic pool.</span></span> <span data-ttu-id="b5a4f-186">Contrairement aux API PowerShell de **Tâches de bases de données élastiques** , l'interface du portail ne peut être exécuté que sur un pool existant.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-186">Unlike when using the **Elastic Database jobs** PowerShell APIs, the portal interface is currently restricted to only executing against an existing pool.</span></span>

<span data-ttu-id="b5a4f-187">**Durée estimée :** 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-187">**Estimated time to complete:** 10 minutes.</span></span>

1. <span data-ttu-id="b5a4f-188">Dans la vue du tableau de bord du pool élastique via le [portail Azure](https://portal.azure.com/#), cliquez sur **Créer une tâche**.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-188">From the dashboard view of the elastic pool via the [Azure Portal](https://portal.azure.com/#) , click **Create job**.</span></span>
2. <span data-ttu-id="b5a4f-189">Si vous créez une tâche pour la première fois, vous devez installer **Tâche de base de données élastique** en cliquant sur **CONDITIONS D’UTILISATION DE LA VERSION PREVIEW**.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-189">If you are creating a job for the first time, you must install **Elastic Database jobs** by clicking **PREVIEW TERMS**.</span></span>
3. <span data-ttu-id="b5a4f-190">Acceptez les termes en cliquant sur la case à cocher.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-190">Accept the terms by clicking the checkbox.</span></span>
4. <span data-ttu-id="b5a4f-191">Dans la vue « Installer les services », cliquez sur **JOB CREDENTIALS**.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-191">In the "Install services" view, click **JOB CREDENTIALS**.</span></span>
   
    ![Installation des serveurs][1]
5. <span data-ttu-id="b5a4f-193">Tapez un nom d'utilisateur et un mot de passe d'administrateur de base de données.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-193">Type a user name and password for a database admin.</span></span> <span data-ttu-id="b5a4f-194">Dans le cadre de l'installation, un nouveau serveur de base de données SQL Azure est créé.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-194">As part of the installation, a new Azure SQL Database server is created.</span></span> <span data-ttu-id="b5a4f-195">Sur ce nouveau serveur, une nouvelle base de données, appelée base de données de contrôle, est créée et utilisée pour contenir les métadonnées des tâches de bases de données élastiques.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-195">Within this new server, a new database, known as the control database, is created and used to contain the meta data for Elastic Database jobs.</span></span> <span data-ttu-id="b5a4f-196">Le nom d'utilisateur et le mot de passe créés ici sont utilisés pour se connecter à la base de données de contrôle.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-196">The user name and password created here are used for the purpose of logging in to the control database.</span></span> <span data-ttu-id="b5a4f-197">Une information d'identification distincte est utilisée pour l'exécution du script sur les bases de données du pool.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-197">A separate credential is used for script execution against the databases within the pool.</span></span>
   
    ![Créer le nom d'utilisateur et le mot de passe][2]
6. <span data-ttu-id="b5a4f-199">Cliquez sur le bouton OK.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-199">Click the OK button.</span></span> <span data-ttu-id="b5a4f-200">Les composants sont créés pour vous en quelques minutes dans un nouveau [groupe de ressources](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b5a4f-200">The components are created for you in a few minutes in a new [Resource group](../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="b5a4f-201">Le nouveau groupe de ressources est épinglé au panneau de démarrage, comme illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-201">The new resource group is pinned to the start board, as shown below.</span></span> <span data-ttu-id="b5a4f-202">Les tâches de bases de données élastiques (Service Cloud, Base de données SQL, Service Bus et Storage) sont toutes créées dans le groupe.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-202">Once created, elastic database jobs (Cloud Service, SQL Database, Service Bus, and Storage) are all created in the group.</span></span>
   
    ![groupe de ressources dans le panneau de démarrage][3]
7. <span data-ttu-id="b5a4f-204">Si vous tentez de créer ou de gérer une tâche pendant l’installation de tâches de bases de données élastiques, le message suivant apparaît lorsque vous fournissez les **informations d'identification** .</span><span class="sxs-lookup"><span data-stu-id="b5a4f-204">If you attempt to create or manage a job while elastic database jobs is installing, when providing **Credentials** you will see the following message.</span></span>
   
    ![Déploiement en cours][4]

<span data-ttu-id="b5a4f-206">Si la désinstallation est nécessaire, supprimez le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-206">If uninstallation is required, delete the resource group.</span></span> <span data-ttu-id="b5a4f-207">Consultez [Désinstaller les composants de Tâches de bases de données élastiques](sql-database-elastic-jobs-uninstall.md).</span><span class="sxs-lookup"><span data-stu-id="b5a4f-207">See [How to uninstall the Elastic Database job components](sql-database-elastic-jobs-uninstall.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b5a4f-208">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b5a4f-208">Next steps</span></span>
<span data-ttu-id="b5a4f-209">Vérifiez que les informations d’identification disposant des droits appropriés pour l’exécution du script sont créées sur chaque base de données du groupe. Pour plus d’informations, consultez [Sécurisation de votre base de données SQL](sql-database-manage-logins.md).</span><span class="sxs-lookup"><span data-stu-id="b5a4f-209">Ensure a credential with the appropriate rights for script execution is created on each database in the group, for more information see [Securing your SQL Database](sql-database-manage-logins.md).</span></span>
<span data-ttu-id="b5a4f-210">Pour plus d’informations, consultez [Création et gestion de Tâches de bases de données élastiques](sql-database-elastic-jobs-create-and-manage.md) pour commencer.</span><span class="sxs-lookup"><span data-stu-id="b5a4f-210">See [Creating and managing an Elastic Database jobs](sql-database-elastic-jobs-create-and-manage.md) to get started.</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-service-installation/screen-1.png
[2]: ./media/sql-database-elastic-jobs-service-installation/credentials.png
[3]: ./media/sql-database-elastic-jobs-service-installation/start-board.png
[4]: ./media/sql-database-elastic-jobs-service-installation/not-done.png
