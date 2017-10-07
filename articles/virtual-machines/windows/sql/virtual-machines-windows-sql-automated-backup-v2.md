---
title: aaaAutomated v2 de sauvegarde pour les Machines virtuelles Azure 2016 SQL Server | Documents Microsoft
description: "Explique la fonctionnalité de sauvegarde automatisée hello pour SQL Server 2016 machines virtuelles s’exécutant dans Azure. Cet article est tooVMs spécifique à l’aide de hello Gestionnaire de ressources."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: ebd23868-821c-475b-b867-06d4a2e310c7
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 04/05/2017
ms.author: jroth
ms.openlocfilehash: a322792fb22c76bfa74fafb711b8b1927a6e2b3a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-v2-for-sql-server-2016-azure-virtual-machines-resource-manager"></a><span data-ttu-id="e0f16-104">Sauvegarde automatisée version 2 pour SQL Server 2016 dans des machines virtuelles Azure (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="e0f16-104">Automated Backup v2 for SQL Server 2016 Azure Virtual Machines (Resource Manager)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e0f16-105">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="e0f16-105">SQL Server 2014</span></span>](virtual-machines-windows-sql-automated-backup.md)
> * [<span data-ttu-id="e0f16-106">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="e0f16-106">SQL Server 2016</span></span>](virtual-machines-windows-sql-automated-backup-v2.md)

<span data-ttu-id="e0f16-107">V2 de sauvegarde automatisée configure automatiquement [tooMicrosoft de gestion de sauvegarde Azure](https://msdn.microsoft.com/library/dn449496.aspx) pour toutes les bases de données nouvelles et existantes sur une machine virtuelle de Azure exécutant les éditions de SQL Server 2016 : Standard, Enterprise ou Developer.</span><span class="sxs-lookup"><span data-stu-id="e0f16-107">Automated Backup v2 automatically configures [Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2016 Standard, Enterprise, or Developer editions.</span></span> <span data-ttu-id="e0f16-108">Cela vous permet de tooconfigure des sauvegardes régulières de la base de données qui utilisent le stockage d’objets blob Azure durable.</span><span class="sxs-lookup"><span data-stu-id="e0f16-108">This enables you tooconfigure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="e0f16-109">V2 de sauvegarde automatisée dépend hello [Extension de l’Agent SQL Server IaaS](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="e0f16-109">Automated Backup v2 depends on hello [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="e0f16-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e0f16-110">Prerequisites</span></span>
<span data-ttu-id="e0f16-111">toouse v2 de sauvegarde automatisée, passez en revue les hello suivant des conditions préalables :</span><span class="sxs-lookup"><span data-stu-id="e0f16-111">toouse Automated Backup v2, review hello following prerequisites:</span></span>

<span data-ttu-id="e0f16-112">**Système d’exploitation**:</span><span class="sxs-lookup"><span data-stu-id="e0f16-112">**Operating System**:</span></span>

- <span data-ttu-id="e0f16-113">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="e0f16-113">Windows Server 2012 R2</span></span>
- <span data-ttu-id="e0f16-114">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="e0f16-114">Windows Server 2016</span></span>

<span data-ttu-id="e0f16-115">**Édition/version de SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="e0f16-115">**SQL Server version/edition**:</span></span>

- <span data-ttu-id="e0f16-116">SQL Server 2016 Standard</span><span class="sxs-lookup"><span data-stu-id="e0f16-116">SQL Server 2016 Standard</span></span>
- <span data-ttu-id="e0f16-117">SQL Server 2016 Enterprise</span><span class="sxs-lookup"><span data-stu-id="e0f16-117">SQL Server 2016 Enterprise</span></span>
- <span data-ttu-id="e0f16-118">SQL Server 2016 Developer</span><span class="sxs-lookup"><span data-stu-id="e0f16-118">SQL Server 2016 Developer</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e0f16-119">La sauvegarde automatisée version 2 fonctionne avec SQL Server 2016.</span><span class="sxs-lookup"><span data-stu-id="e0f16-119">Automated Backup v2 works with SQL Server 2016.</span></span> <span data-ttu-id="e0f16-120">Si vous utilisez SQL Server 2014, vous pouvez utiliser la sauvegarde automatisée v1 tooback vos bases de données.</span><span class="sxs-lookup"><span data-stu-id="e0f16-120">If you are using SQL Server 2014, you can use Automated Backup v1 tooback up your databases.</span></span> <span data-ttu-id="e0f16-121">Pour plus d’informations, voir [Sauvegarde automatisée pour SQL Server 2014 dans les machines virtuelles Azure](virtual-machines-windows-sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="e0f16-121">For more information, see [Automated Backup for SQL Server 2014 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup.md).</span></span>

<span data-ttu-id="e0f16-122">**Configuration de la base de données**:</span><span class="sxs-lookup"><span data-stu-id="e0f16-122">**Database configuration**:</span></span>

- <span data-ttu-id="e0f16-123">Bases de données cible doivent utiliser le mode de récupération complète hello.</span><span class="sxs-lookup"><span data-stu-id="e0f16-123">Target databases must use hello full recovery model.</span></span> <span data-ttu-id="e0f16-124">Pour plus d’informations sur l’impact de hello hello complète du mode de récupération sur les sauvegardes, consultez [hello sauvegarde sous le mode de récupération complète](https://technet.microsoft.com/library/ms190217.aspx).</span><span class="sxs-lookup"><span data-stu-id="e0f16-124">For more information about hello impact of hello full recovery model on backups, see [Backup Under hello Full Recovery Model](https://technet.microsoft.com/library/ms190217.aspx).</span></span>
- <span data-ttu-id="e0f16-125">Bases de données système n’ont pas de mode de récupération complète toouse.</span><span class="sxs-lookup"><span data-stu-id="e0f16-125">System databases do not have toouse full recovery model.</span></span> <span data-ttu-id="e0f16-126">Toutefois, si vous avez besoin toobe de sauvegardes de journal nécessaire pour le modèle ou MSDB, vous devez utiliser le mode de récupération complète.</span><span class="sxs-lookup"><span data-stu-id="e0f16-126">However, if you require log backups toobe taken for Model or MSDB, you must use full recovery model.</span></span>
- <span data-ttu-id="e0f16-127">Bases de données cible doivent être sur une instance de SQL Server par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="e0f16-127">Target databases must be on hello default SQL Server instance.</span></span> <span data-ttu-id="e0f16-128">Hello IaaS Extension de SQL Server ne prend pas en charge les instances nommées.</span><span class="sxs-lookup"><span data-stu-id="e0f16-128">hello SQL Server IaaS Extension does not support named instances.</span></span>

<span data-ttu-id="e0f16-129">**Modèle de déploiement Azure** :</span><span class="sxs-lookup"><span data-stu-id="e0f16-129">**Azure deployment model**:</span></span>

- <span data-ttu-id="e0f16-130">Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="e0f16-130">Resource Manager</span></span>

> [!NOTE]
> <span data-ttu-id="e0f16-131">Sauvegarde automatisée s’appuie sur hello **Extension de l’Agent SQL Server IaaS**.</span><span class="sxs-lookup"><span data-stu-id="e0f16-131">Automated Backup relies on hello **SQL Server IaaS Agent Extension**.</span></span> <span data-ttu-id="e0f16-132">Les images actuelles de la galerie de machines virtuelles SQL ajoutent cette extension par défaut.</span><span class="sxs-lookup"><span data-stu-id="e0f16-132">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="e0f16-133">Pour plus d’informations, consultez [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md)(Extension de l’agent IaaS SQL Server).</span><span class="sxs-lookup"><span data-stu-id="e0f16-133">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="e0f16-134">Paramètres</span><span class="sxs-lookup"><span data-stu-id="e0f16-134">Settings</span></span>
<span data-ttu-id="e0f16-135">Hello tableau suivant décrit les options de hello qui peuvent être configurées pour la sauvegarde automatisée v2.</span><span class="sxs-lookup"><span data-stu-id="e0f16-135">hello following table describes hello options that can be configured for Automated Backup v2.</span></span> <span data-ttu-id="e0f16-136">étapes de configuration réelles Hello varient selon que vous utilisez hello portail Azure ou des commandes PowerShell de Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="e0f16-136">hello actual configuration steps vary depending on whether you use hello Azure portal or Azure Windows PowerShell commands.</span></span>

### <a name="basic-settings"></a><span data-ttu-id="e0f16-137">Paramètres de base</span><span class="sxs-lookup"><span data-stu-id="e0f16-137">Basic Settings</span></span>

| <span data-ttu-id="e0f16-138">Paramètre</span><span class="sxs-lookup"><span data-stu-id="e0f16-138">Setting</span></span> | <span data-ttu-id="e0f16-139">Plage (par défaut)</span><span class="sxs-lookup"><span data-stu-id="e0f16-139">Range (Default)</span></span> | <span data-ttu-id="e0f16-140">Description</span><span class="sxs-lookup"><span data-stu-id="e0f16-140">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e0f16-141">**Sauvegarde automatisée**</span><span class="sxs-lookup"><span data-stu-id="e0f16-141">**Automated Backup**</span></span> | <span data-ttu-id="e0f16-142">Activer/Désactiver (désactivé)</span><span class="sxs-lookup"><span data-stu-id="e0f16-142">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="e0f16-143">Active ou désactive la sauvegarde automatisée d’une machine virtuelle Azure exécutant SQL Server 2016 Standard ou Enterprise.</span><span class="sxs-lookup"><span data-stu-id="e0f16-143">Enables or disables Automated Backup for an Azure VM running SQL Server 2016 Standard or Enterprise.</span></span> |
| <span data-ttu-id="e0f16-144">**Période de rétention**</span><span class="sxs-lookup"><span data-stu-id="e0f16-144">**Retention Period**</span></span> | <span data-ttu-id="e0f16-145">1 à 30 jours (30 jours)</span><span class="sxs-lookup"><span data-stu-id="e0f16-145">1-30 days (30 days)</span></span> | <span data-ttu-id="e0f16-146">nombre de Hello de sauvegardes de tooretain jours.</span><span class="sxs-lookup"><span data-stu-id="e0f16-146">hello number of days tooretain backups.</span></span> |
| <span data-ttu-id="e0f16-147">**Compte de stockage**</span><span class="sxs-lookup"><span data-stu-id="e0f16-147">**Storage Account**</span></span> | <span data-ttu-id="e0f16-148">Compte Azure Storage</span><span class="sxs-lookup"><span data-stu-id="e0f16-148">Azure storage account</span></span> | <span data-ttu-id="e0f16-149">Un toouse de compte de stockage Azure pour stocker les fichiers de sauvegarde automatisée dans le stockage blob.</span><span class="sxs-lookup"><span data-stu-id="e0f16-149">An Azure storage account toouse for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="e0f16-150">Un conteneur est créé à cet emplacement toostore tous les fichiers de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="e0f16-150">A container is created at this location toostore all backup files.</span></span> <span data-ttu-id="e0f16-151">fichier de sauvegarde Hello convention d’affectation de noms inclut hello date, heure et la base de données GUID.</span><span class="sxs-lookup"><span data-stu-id="e0f16-151">hello backup file naming convention includes hello date, time, and database GUID.</span></span> |
| <span data-ttu-id="e0f16-152">**Chiffrement**</span><span class="sxs-lookup"><span data-stu-id="e0f16-152">**Encryption**</span></span> |<span data-ttu-id="e0f16-153">Activer/Désactiver (désactivé)</span><span class="sxs-lookup"><span data-stu-id="e0f16-153">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="e0f16-154">Active ou désactive le chiffrement.</span><span class="sxs-lookup"><span data-stu-id="e0f16-154">Enables or disables encryption.</span></span> <span data-ttu-id="e0f16-155">Lorsque le chiffrement est activé, hello certificats utilisés toorestore hello sauvegarde se trouvent dans hello spécifié du compte de stockage Bonjour même **automaticbackup** conteneur à l’aide de hello même convention d’affectation de noms.</span><span class="sxs-lookup"><span data-stu-id="e0f16-155">When encryption is enabled, hello certificates used toorestore hello backup are located in hello specified storage account in hello same **automaticbackup** container using hello same naming convention.</span></span> <span data-ttu-id="e0f16-156">Si le mot de passe hello change, un nouveau certificat est généré avec ce mot de passe, mais hello ancien certificat est conservé toorestore les sauvegardes antérieures.</span><span class="sxs-lookup"><span data-stu-id="e0f16-156">If hello password changes, a new certificate is generated with that password, but hello old certificate remains toorestore prior backups.</span></span> |
| <span data-ttu-id="e0f16-157">**Mot de passe**</span><span class="sxs-lookup"><span data-stu-id="e0f16-157">**Password**</span></span> |<span data-ttu-id="e0f16-158">Texte du mot de passe</span><span class="sxs-lookup"><span data-stu-id="e0f16-158">Password text</span></span> | <span data-ttu-id="e0f16-159">Mot de passe pour les clés de chiffrement.</span><span class="sxs-lookup"><span data-stu-id="e0f16-159">A password for encryption keys.</span></span> <span data-ttu-id="e0f16-160">Il est uniquement requis si le chiffrement est activé.</span><span class="sxs-lookup"><span data-stu-id="e0f16-160">This is only required if encryption is enabled.</span></span> <span data-ttu-id="e0f16-161">Dans l’ordre toorestore une sauvegarde chiffrée, vous devez avoir mot de passe correct hello et du certificat associé qui a été utilisé au moment de hello hello sauvegarde a été effectuée.</span><span class="sxs-lookup"><span data-stu-id="e0f16-161">In order toorestore an encrypted backup, you must have hello correct password and related certificate that was used at hello time hello backup was taken.</span></span> |

### <a name="advanced-settings"></a><span data-ttu-id="e0f16-162">Paramètres avancés</span><span class="sxs-lookup"><span data-stu-id="e0f16-162">Advanced Settings</span></span>

| <span data-ttu-id="e0f16-163">Paramètre</span><span class="sxs-lookup"><span data-stu-id="e0f16-163">Setting</span></span> | <span data-ttu-id="e0f16-164">Plage (par défaut)</span><span class="sxs-lookup"><span data-stu-id="e0f16-164">Range (Default)</span></span> | <span data-ttu-id="e0f16-165">Description</span><span class="sxs-lookup"><span data-stu-id="e0f16-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e0f16-166">**Sauvegardes de bases de données système**</span><span class="sxs-lookup"><span data-stu-id="e0f16-166">**System Database Backups**</span></span> | <span data-ttu-id="e0f16-167">Activer/Désactiver (désactivé)</span><span class="sxs-lookup"><span data-stu-id="e0f16-167">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="e0f16-168">Lorsque activé, cette fonctionnalité sera également sauvegarder les bases de données système hello : Master, MSDB et Model.</span><span class="sxs-lookup"><span data-stu-id="e0f16-168">When enabled, this feature will also back up hello system databases: Master, MSDB, and Model.</span></span> <span data-ttu-id="e0f16-169">Hello MSDB et des bases de données de modèle, vérifiez qu’ils sont en mode de récupération complète si vous souhaitez que toobe de sauvegardes de journal effectuée.</span><span class="sxs-lookup"><span data-stu-id="e0f16-169">For hello MSDB and Model databases, verify that they are in full recovery mode if you want log backups toobe taken.</span></span> <span data-ttu-id="e0f16-170">Les sauvegardes de journaux ne sont jamais effectuées pour Master.</span><span class="sxs-lookup"><span data-stu-id="e0f16-170">Log backups are never taken for Master.</span></span> <span data-ttu-id="e0f16-171">Et aucune sauvegarde n’est effectuée pour TempDB.</span><span class="sxs-lookup"><span data-stu-id="e0f16-171">And no backups are taken for TempDB.</span></span> |
| <span data-ttu-id="e0f16-172">**Planification de sauvegarde**</span><span class="sxs-lookup"><span data-stu-id="e0f16-172">**Backup Schedule**</span></span> | <span data-ttu-id="e0f16-173">Manuelle/automatisée (automatisée)</span><span class="sxs-lookup"><span data-stu-id="e0f16-173">Manual/Automated (Automated)</span></span> | <span data-ttu-id="e0f16-174">Par défaut, planification de sauvegarde hello est automatiquement déterminée en fonction de la croissance du journal hello.</span><span class="sxs-lookup"><span data-stu-id="e0f16-174">By default, hello backup schedule will be automatically determined based on hello log growth.</span></span> <span data-ttu-id="e0f16-175">Planification de la sauvegarde manuelle permet de fenêtre de temps hello utilisateur toospecify hello pour les sauvegardes.</span><span class="sxs-lookup"><span data-stu-id="e0f16-175">Manual backup schedule allows hello user toospecify hello time window for backups.</span></span> <span data-ttu-id="e0f16-176">Dans ce cas, les sauvegardes seront uniquement n’aient lieu au moment de hello spécifié fréquence et pendant hello fenêtre de temps d’un jour donné.</span><span class="sxs-lookup"><span data-stu-id="e0f16-176">In this case, backups will only ever take place at hello specified frequency and during hello specified time window of a given day.</span></span> |
| <span data-ttu-id="e0f16-177">**Fréquence de sauvegarde complète**</span><span class="sxs-lookup"><span data-stu-id="e0f16-177">**Full backup frequency**</span></span> | <span data-ttu-id="e0f16-178">Quotidienne/hebdomadaire</span><span class="sxs-lookup"><span data-stu-id="e0f16-178">Daily/Weekly</span></span> | <span data-ttu-id="e0f16-179">Fréquence des sauvegardes complètes.</span><span class="sxs-lookup"><span data-stu-id="e0f16-179">Frequency of full backups.</span></span> <span data-ttu-id="e0f16-180">Dans les deux cas, les sauvegardes complètes commence au cours de la fenêtre d’heure planifiée suivante hello.</span><span class="sxs-lookup"><span data-stu-id="e0f16-180">In both cases, full backups will begin during hello next scheduled time window.</span></span> <span data-ttu-id="e0f16-181">Si vous sélectionnez l’option Hebdomadaire, les sauvegardes peuvent s’étaler sur plusieurs jours jusqu'à ce que toutes les bases de données aient été sauvegardées avec succès.</span><span class="sxs-lookup"><span data-stu-id="e0f16-181">When weekly is selected, backups could span multiple days until all databases have successfully backed up.</span></span> |
| <span data-ttu-id="e0f16-182">**Heure de début de la sauvegarde complète**</span><span class="sxs-lookup"><span data-stu-id="e0f16-182">**Full backup start time**</span></span> | <span data-ttu-id="e0f16-183">00:00 – 23:00 (01:00)</span><span class="sxs-lookup"><span data-stu-id="e0f16-183">00:00 – 23:00 (01:00)</span></span> | <span data-ttu-id="e0f16-184">Heure de début d’un jour donné où des sauvegardes complètes peuvent être effectuées.</span><span class="sxs-lookup"><span data-stu-id="e0f16-184">Start time of a given day during which full backups can take place.</span></span> |
| <span data-ttu-id="e0f16-185">**Fenêtre de temps de la sauvegarde complète**</span><span class="sxs-lookup"><span data-stu-id="e0f16-185">**Full backup time window**</span></span> | <span data-ttu-id="e0f16-186">1 à 23 heures (1 heure)</span><span class="sxs-lookup"><span data-stu-id="e0f16-186">1 – 23 hours (1 hour)</span></span> | <span data-ttu-id="e0f16-187">Durée hello de fenêtre de temps d’un jour donné au cours de laquelle les sauvegardes complètes peuvent avoir lieu.</span><span class="sxs-lookup"><span data-stu-id="e0f16-187">Duration of hello time window of a given day during which full backups can take place.</span></span> |
| <span data-ttu-id="e0f16-188">**Fréquence de sauvegarde des journaux**</span><span class="sxs-lookup"><span data-stu-id="e0f16-188">**Log backup frequency**</span></span> | <span data-ttu-id="e0f16-189">5 à 60 minutes (60 minutes)</span><span class="sxs-lookup"><span data-stu-id="e0f16-189">5 – 60 minutes (60 minutes)</span></span> | <span data-ttu-id="e0f16-190">Fréquence des sauvegardes de journaux.</span><span class="sxs-lookup"><span data-stu-id="e0f16-190">Frequency of log backups.</span></span> |

## <a name="understanding-full-backup-frequency"></a><span data-ttu-id="e0f16-191">Présentation de la fréquence de sauvegarde complète</span><span class="sxs-lookup"><span data-stu-id="e0f16-191">Understanding full backup frequency</span></span>
<span data-ttu-id="e0f16-192">Il est la différence de hello toounderstand important entre les sauvegardes complètes quotidiennes ou hebdomadaires.</span><span class="sxs-lookup"><span data-stu-id="e0f16-192">It is important toounderstand hello difference between daily and weekly full backups.</span></span> <span data-ttu-id="e0f16-193">Ici, nous étudierons deux exemples de scénarios.</span><span class="sxs-lookup"><span data-stu-id="e0f16-193">In this effort, we will walk through two example scenarios.</span></span>

### <a name="scenario-1-weekly-backups"></a><span data-ttu-id="e0f16-194">Scénario 1 : Sauvegardes hebdomadaires</span><span class="sxs-lookup"><span data-stu-id="e0f16-194">Scenario 1: Weekly backups</span></span>
<span data-ttu-id="e0f16-195">Vous utilisez une machine virtuelle SQL Server qui contient plusieurs bases de données très volumineuses.</span><span class="sxs-lookup"><span data-stu-id="e0f16-195">You have a SQL Server VM which contains a number of very large databases.</span></span>

<span data-ttu-id="e0f16-196">Lundi, vous activez v2 de sauvegarde automatisée avec hello suivant les paramètres :</span><span class="sxs-lookup"><span data-stu-id="e0f16-196">On Monday, you enable Automated Backup v2 with hello following settings:</span></span>

- <span data-ttu-id="e0f16-197">Planification de sauvegarde : **Manuelle**</span><span class="sxs-lookup"><span data-stu-id="e0f16-197">Backup schedule: **Manual**</span></span>
- <span data-ttu-id="e0f16-198">Fréquence de sauvegarde complète : **Hebdomadaire**</span><span class="sxs-lookup"><span data-stu-id="e0f16-198">Full backup frequency: **Weekly**</span></span>
- <span data-ttu-id="e0f16-199">Heure de début de la sauvegarde complète : **01:00**</span><span class="sxs-lookup"><span data-stu-id="e0f16-199">Full backup start time: **01:00**</span></span>
- <span data-ttu-id="e0f16-200">Fenêtre de temps de la sauvegarde complète : **1 heure**</span><span class="sxs-lookup"><span data-stu-id="e0f16-200">Full backup time window: **1 hour**</span></span>

<span data-ttu-id="e0f16-201">Cela signifie que hello prochaine sauvegarde fenêtre disponible mardi à 1 h 00 pour 1 heure.</span><span class="sxs-lookup"><span data-stu-id="e0f16-201">This means that hello next available backup window is Tuesday at 1 AM for 1 hour.</span></span> <span data-ttu-id="e0f16-202">À ce stade, la sauvegarde automatisée commence à sauvegarder vos bases de données une par une.</span><span class="sxs-lookup"><span data-stu-id="e0f16-202">At that time, Automated Backup will begin backing up your databases one at a time.</span></span> <span data-ttu-id="e0f16-203">Dans ce scénario, vos bases de données sont suffisamment grands pour que les sauvegardes complètes va s’achever pour hello abord deux bases de données.</span><span class="sxs-lookup"><span data-stu-id="e0f16-203">In this scenario, your databases are large enough that full backups will complete for hello first couple databases.</span></span> <span data-ttu-id="e0f16-204">Toutefois, après une heure toutes les bases de données hello ont été sauvegardés.</span><span class="sxs-lookup"><span data-stu-id="e0f16-204">However, after one hour not all of hello databases have been backed up.</span></span>

<span data-ttu-id="e0f16-205">Dans ce cas, sauvegarde automatisée commencera sauvegarde hello restant hello de bases de données à jour suivant, le mercredi à 1 h 00 pour 1 heure.</span><span class="sxs-lookup"><span data-stu-id="e0f16-205">When this happens, Automated Backup will begin backing up hello remaining databases hello next day, Wednesday at 1 AM for 1 hour.</span></span> <span data-ttu-id="e0f16-206">Si pas toutes les bases de données ont été sauvegardés pendant cette période, il tentera à nouveau hello hello mise à jour même temps.</span><span class="sxs-lookup"><span data-stu-id="e0f16-206">If not all databases have been backed up in that time, it will try again hello next day at hello same time.</span></span> <span data-ttu-id="e0f16-207">Cette opération se poursuit jusqu'à ce que toutes les bases de données aient été correctement sauvegardées.</span><span class="sxs-lookup"><span data-stu-id="e0f16-207">This will continue until all databases have been successfully backed up.</span></span>

<span data-ttu-id="e0f16-208">Le mardi suivant, la sauvegarde automatisée recommencera à sauvegarder toutes les bases de données.</span><span class="sxs-lookup"><span data-stu-id="e0f16-208">Once it reaches Tuesday again, Automated Backup will begin backing up all databases once again.</span></span>

<span data-ttu-id="e0f16-209">Ce scénario montre que la sauvegarde automatisée ne fonctionnera que dans la fenêtre de temps spécifié hello, et chaque base de données est sauvegardé une fois par semaine.</span><span class="sxs-lookup"><span data-stu-id="e0f16-209">This scenario shows that Automated Backup will only operate within hello specified time window, and each database will be backed up once per week.</span></span> <span data-ttu-id="e0f16-210">Il montre également qu’il est possible pour les sauvegardes toospan plusieurs jours Bonjour cas où il n’est pas possible de toocomplete toutes les sauvegardes en un seul jour.</span><span class="sxs-lookup"><span data-stu-id="e0f16-210">This also shows that it is possible for backups toospan multiple days in hello case where it is not possible toocomplete all backups in a single day.</span></span>

### <a name="scenario-2-daily-backups"></a><span data-ttu-id="e0f16-211">Scénario 2 : Sauvegardes quotidiennes</span><span class="sxs-lookup"><span data-stu-id="e0f16-211">Scenario 2: Daily backups</span></span>
<span data-ttu-id="e0f16-212">Vous utilisez une machine virtuelle SQL Server qui contient plusieurs bases de données très volumineuses.</span><span class="sxs-lookup"><span data-stu-id="e0f16-212">You have a SQL Server VM which contains a number of very large databases.</span></span>

<span data-ttu-id="e0f16-213">Lundi, vous activez v2 de sauvegarde automatisée avec hello suivant les paramètres :</span><span class="sxs-lookup"><span data-stu-id="e0f16-213">On Monday, you enable Automated Backup v2 with hello following settings:</span></span>

- <span data-ttu-id="e0f16-214">Planification de sauvegarde : Manuelle</span><span class="sxs-lookup"><span data-stu-id="e0f16-214">Backup schedule: Manual</span></span>
- <span data-ttu-id="e0f16-215">Fréquence de sauvegarde complète : Quotidienne</span><span class="sxs-lookup"><span data-stu-id="e0f16-215">Full backup frequency: Daily</span></span>
- <span data-ttu-id="e0f16-216">Heure de début de la sauvegarde complète : 22:00</span><span class="sxs-lookup"><span data-stu-id="e0f16-216">Full backup start time: 22:00</span></span>
- <span data-ttu-id="e0f16-217">Fenêtre de temps de la sauvegarde complète : 6 heures</span><span class="sxs-lookup"><span data-stu-id="e0f16-217">Full backup time window: 6 hours</span></span>

<span data-ttu-id="e0f16-218">Cela signifie que Hello suivant disponible fenêtre de sauvegarde est le lundi à 22 h 00 pendant 6 heures.</span><span class="sxs-lookup"><span data-stu-id="e0f16-218">This means that hello next available backup window is Monday at 10 PM for 6 hours.</span></span> <span data-ttu-id="e0f16-219">À ce stade, la sauvegarde automatisée commence à sauvegarder vos bases de données une par une.</span><span class="sxs-lookup"><span data-stu-id="e0f16-219">At that time, Automated Backup will begin backing up your databases one at a time.</span></span>

<span data-ttu-id="e0f16-220">Puis des sauvegardes complètes de toutes les bases de données seront relancées mardi à 22 h 00 pendant 6 heures.</span><span class="sxs-lookup"><span data-stu-id="e0f16-220">Then, on Tuesday at 10 for 6 hours, full backups of all databases will start again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e0f16-221">Lors de la planification des sauvegardes quotidiennes, il est recommandé de planifier l’exécution d’une tooensure de fenêtre de temps large toutes les bases de données peuvent être sauvegardées dans ce délai.</span><span class="sxs-lookup"><span data-stu-id="e0f16-221">When scheduling daily backups, it is recommended that you schedule a wide time window tooensure all databases can be backed up within this time.</span></span> <span data-ttu-id="e0f16-222">Cela est particulièrement important dans le cas de hello si vous avez une grande quantité de données tooback des.</span><span class="sxs-lookup"><span data-stu-id="e0f16-222">This is especially important in hello case where you have a large amount of data tooback up.</span></span>

## <a name="configuration-in-hello-portal"></a><span data-ttu-id="e0f16-223">Configuration Bonjour portail</span><span class="sxs-lookup"><span data-stu-id="e0f16-223">Configuration in hello Portal</span></span>

<span data-ttu-id="e0f16-224">Vous pouvez utiliser v2 de sauvegarde automatisée tooconfigure portail Azure hello lors de la configuration ou de SQL Server 2016 des machines virtuelles existantes.</span><span class="sxs-lookup"><span data-stu-id="e0f16-224">You can use hello Azure portal tooconfigure Automated Backup v2 during provisioning or for existing SQL Server 2016 VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="e0f16-225">Nouvelles machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="e0f16-225">New VMs</span></span>

<span data-ttu-id="e0f16-226">Utilisez v2 de sauvegarde automatisée hello tooconfigure portail Azure lorsque vous créez une nouvelle Machine virtuelle SQL Server 2016 dans le modèle de déploiement du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="e0f16-226">Use hello Azure portal tooconfigure Automated Backup v2 when you create a new SQL Server 2016 Virtual Machine in hello Resource Manager deployment model.</span></span> 

<span data-ttu-id="e0f16-227">Bonjour **paramètres SQL Server** panneau, sélectionnez **sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="e0f16-227">In hello **SQL Server settings** blade, select **Automated backup**.</span></span> <span data-ttu-id="e0f16-228">Bonjour Azure portail montre hello **sauvegarde automatisée SQL** panneau.</span><span class="sxs-lookup"><span data-stu-id="e0f16-228">hello following Azure portal screenshot shows hello **SQL Automated Backup** blade.</span></span>

![Configuration d’une sauvegarde automatisée SQL dans le portail Azure](./media/virtual-machines-windows-sql-automated-backup-v2/automated-backup-blade.png)

> [!NOTE]
> <span data-ttu-id="e0f16-230">La sauvegarde automatisée version 2 est désactivée par défaut.</span><span class="sxs-lookup"><span data-stu-id="e0f16-230">Automated Backup v2 is disabled by default.</span></span>

<span data-ttu-id="e0f16-231">Pour le contexte, consultez la rubrique complète de hello relative [approvisionner un ordinateur virtuel de SQL Server dans Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="e0f16-231">For context, see hello complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="e0f16-232">Machines virtuelles existantes</span><span class="sxs-lookup"><span data-stu-id="e0f16-232">Existing VMs</span></span>

<span data-ttu-id="e0f16-233">Pour les machines virtuelles SQL Server existantes, sélectionnez votre machine virtuelle SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e0f16-233">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="e0f16-234">Puis sélectionnez hello **configuration de SQL Server** section Hello **paramètres** panneau.</span><span class="sxs-lookup"><span data-stu-id="e0f16-234">Then select hello **SQL Server configuration** section of hello **Settings** blade.</span></span>

![Sauvegarde automatisée SQL pour les machines virtuelles existantes](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration.png)

<span data-ttu-id="e0f16-236">Bonjour **configuration de SQL Server** panneau, cliquez sur hello **modifier** bouton Bonjour automatisée de section de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="e0f16-236">In hello **SQL Server configuration** blade, click hello **Edit** button in hello Automated backup section.</span></span>

![Configurer la sauvegarde automatisée SQL pour les machines virtuelles existantes](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration-edit.png)

<span data-ttu-id="e0f16-238">Lorsque vous avez terminé, cliquez sur hello **OK** bouton bas hello Hello **configuration de SQL Server** panneau toosave vos modifications.</span><span class="sxs-lookup"><span data-stu-id="e0f16-238">When finished, click hello **OK** button on hello bottom of hello **SQL Server configuration** blade toosave your changes.</span></span>

<span data-ttu-id="e0f16-239">Si vous activez le sauvegarde automatisée pour hello première fois, Azure configure hello Agent SQL Server IaaS en arrière-plan de hello.</span><span class="sxs-lookup"><span data-stu-id="e0f16-239">If you are enabling Automated Backup for hello first time, Azure configures hello SQL Server IaaS Agent in hello background.</span></span> <span data-ttu-id="e0f16-240">Pendant ce temps, hello portail Azure peut ne pas affiche que la sauvegarde automatisée est configurée.</span><span class="sxs-lookup"><span data-stu-id="e0f16-240">During this time, hello Azure portal might not show that Automated Backup is configured.</span></span> <span data-ttu-id="e0f16-241">Attendez quelques minutes pour hello toobe de l’agent installé, configuré.</span><span class="sxs-lookup"><span data-stu-id="e0f16-241">Wait several minutes for hello agent toobe installed, configured.</span></span> <span data-ttu-id="e0f16-242">Après ce hello Azure portal reflètent les nouveaux paramètres de hello.</span><span class="sxs-lookup"><span data-stu-id="e0f16-242">After that hello Azure portal will reflect hello new settings.</span></span>

## <a name="configuration-with-powershell"></a><span data-ttu-id="e0f16-243">Configuration avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="e0f16-243">Configuration with PowerShell</span></span>

<span data-ttu-id="e0f16-244">Vous pouvez utiliser PowerShell tooconfigure v2 de sauvegarde automatisée.</span><span class="sxs-lookup"><span data-stu-id="e0f16-244">You can use PowerShell tooconfigure Automated Backup v2.</span></span> <span data-ttu-id="e0f16-245">Avant de commencer, vous devez :</span><span class="sxs-lookup"><span data-stu-id="e0f16-245">Before you begin, you must:</span></span>

- <span data-ttu-id="e0f16-246">[Téléchargez et installez hello la dernière version d’Azure PowerShell](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="e0f16-246">[Download and install hello latest Azure PowerShell](http://aka.ms/webpi-azps).</span></span>
- <span data-ttu-id="e0f16-247">Ouvrir Windows PowerShell et l’associer à votre compte.</span><span class="sxs-lookup"><span data-stu-id="e0f16-247">Open Windows PowerShell and associate it with your account.</span></span> <span data-ttu-id="e0f16-248">Vous pouvez faire cela hello comme suit dans hello [configurer votre abonnement](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) section Hello rubrique de configuration.</span><span class="sxs-lookup"><span data-stu-id="e0f16-248">You can do this by following hello steps in hello [Configure your subscription](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) section of hello provisioning topic.</span></span>

### <a name="install-hello-sql-iaas-extension"></a><span data-ttu-id="e0f16-249">Installer hello IaaS Extension de SQL</span><span class="sxs-lookup"><span data-stu-id="e0f16-249">Install hello SQL IaaS Extension</span></span>
<span data-ttu-id="e0f16-250">Si vous avez configuré un ordinateur virtuel SQL Server hello portail Azure, hello IaaS Extension de SQL Server doit déjà être installé.</span><span class="sxs-lookup"><span data-stu-id="e0f16-250">If you provisioned a SQL Server virtual machine from hello Azure portal, hello SQL Server IaaS Extension should already be installed.</span></span> <span data-ttu-id="e0f16-251">Vous pouvez déterminer si elle est installée pour votre machine virtuelle en appelant **Get-AzureRmVM** commande et en examinant hello **Extensions** propriété.</span><span class="sxs-lookup"><span data-stu-id="e0f16-251">You can determine if it is installed for your VM by calling **Get-AzureRmVM** command and examining hello **Extensions** property.</span></span>

```powershell
$vmname = "vmname"
$resourcegroupname = "resourcegroupname"

(Get-AzureRmVM -Name $vmname -ResourceGroupName $resourcegroupname).Extensions 
```

<span data-ttu-id="e0f16-252">Si hello extension SQL Server IaaS Agent est installé, vous devez voir qu'il répertorié comme « Sqliaasagent n’est » ou « SQLIaaSExtension ».</span><span class="sxs-lookup"><span data-stu-id="e0f16-252">If hello SQL Server IaaS Agent extension is installed, you should see it listed as “SqlIaaSAgent” or “SQLIaaSExtension”.</span></span> <span data-ttu-id="e0f16-253">**ProvisioningState** pour l’extension de hello doit également indiquer « Réussi ».</span><span class="sxs-lookup"><span data-stu-id="e0f16-253">**ProvisioningState** for hello extension should also show “Succeeded”.</span></span> 

<span data-ttu-id="e0f16-254">S’il n’est pas installé ou a échoué toobe configuré, vous pouvez l’installer avec hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="e0f16-254">If it is not installed or failed toobe provisioned, you can install it with hello following command.</span></span> <span data-ttu-id="e0f16-255">Dans Ajout toohello nom et ressource groupe virtuelle, vous devez également spécifier la région de hello (**$region**) où se trouve votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e0f16-255">In addition toohello VM name and resource group, you must also specify hello region (**$region**) that your VM is located in.</span></span>

```powershell
$region = “EASTUS2”
Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region 
```

### <span data-ttu-id="e0f16-256"><a id="verifysettings"></a> Vérifier les paramètres actuels</span><span class="sxs-lookup"><span data-stu-id="e0f16-256"><a id="verifysettings"></a> Verify current settings</span></span>
<span data-ttu-id="e0f16-257">Si vous avez activé la sauvegarde automatisée lors de la configuration, vous pouvez utiliser PowerShell toocheck votre configuration actuelle.</span><span class="sxs-lookup"><span data-stu-id="e0f16-257">If you enabled automated backup during provisioning, you can use PowerShell toocheck your current configuration.</span></span> <span data-ttu-id="e0f16-258">Exécutez hello **Get-AzureRmVMSqlServerExtension** de commandes et examiner hello **AutoBackupSettings** propriété :</span><span class="sxs-lookup"><span data-stu-id="e0f16-258">Run hello **Get-AzureRmVMSqlServerExtension** command and examine hello **AutoBackupSettings** property:</span></span>

```powershell
(Get-AzureRmVMSqlServerExtension -VMName $vmname -ResourceGroupName $resourcegroupname).AutoBackupSettings
```

<span data-ttu-id="e0f16-259">Vous devez obtenir suivant toohello similaire de sortie :</span><span class="sxs-lookup"><span data-stu-id="e0f16-259">You should get output similar toohello following:</span></span>

```
Enable                      : True
EnableEncryption            : False
RetentionPeriod             : 30
StorageUrl                  : https://test.blob.core.windows.net/
StorageAccessKey            :  
Password                    : 
BackupSystemDbs             : False
BackupScheduleType          : Manual
FullBackupFrequency         : WEEKLY
FullBackupStartTime         : 2
FullBackupWindowHours       : 2
LogBackupFrequency          : 60
```

<span data-ttu-id="e0f16-260">Si votre sortie montre que **activer** est défini trop**False**, vous devez effectuer des sauvegardes automatiques tooenable.</span><span class="sxs-lookup"><span data-stu-id="e0f16-260">If your output shows that **Enable** is set too**False**, then you have tooenable automated backup.</span></span> <span data-ttu-id="e0f16-261">Bonjour excellente est activer et configurer la sauvegarde automatisée Bonjour identique.</span><span class="sxs-lookup"><span data-stu-id="e0f16-261">hello good news is that you enable and configure Automated Backup in hello same way.</span></span> <span data-ttu-id="e0f16-262">Consultez hello la section suivante pour obtenir des informations.</span><span class="sxs-lookup"><span data-stu-id="e0f16-262">See hello next section for this information.</span></span>

> [!NOTE] 
> <span data-ttu-id="e0f16-263">Si vous vérifiez les paramètres de hello immédiatement après une modification, il est possible que vous obtenez les valeurs de configuration anciennes hello.</span><span class="sxs-lookup"><span data-stu-id="e0f16-263">If you check hello settings immediately after making a change, it is possible that you will get back hello old configuration values.</span></span> <span data-ttu-id="e0f16-264">Attendez quelques minutes et vérifier les paramètres de hello à nouveau les toomake sûr que vos modifications ont été appliquées.</span><span class="sxs-lookup"><span data-stu-id="e0f16-264">Wait a few minutes and check hello settings again toomake sure that your changes were applied.</span></span>

### <a name="configure-automated-backup-v2"></a><span data-ttu-id="e0f16-265">Configurer une sauvegarde automatisée version 2</span><span class="sxs-lookup"><span data-stu-id="e0f16-265">Configure Automated Backup v2</span></span>
<span data-ttu-id="e0f16-266">Vous pouvez utiliser les PowerShell tooenable la sauvegarde, ainsi que toomodify sa configuration et son comportement à tout moment.</span><span class="sxs-lookup"><span data-stu-id="e0f16-266">You can use PowerShell tooenable Automated Backup as well as toomodify its configuration and behavior at any time.</span></span> 

<span data-ttu-id="e0f16-267">Tout d’abord, sélectionnez ou créez un compte de stockage hello pour les fichiers de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="e0f16-267">First, select or create a storage account for hello backup files.</span></span> <span data-ttu-id="e0f16-268">Hello script suivant sélectionne un compte de stockage ou la crée si elle n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="e0f16-268">hello following script selects a storage account or creates it if it does not exist.</span></span>

```powershell
$storage_accountname = “yourstorageaccount”
$storage_resourcegroupname = $resourcegroupname

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region } 
```

> [!NOTE]
> <span data-ttu-id="e0f16-269">La sauvegarde automatisée ne prend pas en charge le stockage des sauvegardes dans un stockage Premium, mais elle peut effectuer des sauvegardes à partir de disques de machines virtuelles qui utilisent le stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="e0f16-269">Automated Backup does not support storing backups in premium storage, but it can take backups from VM disks which use Premium Storage.</span></span>

<span data-ttu-id="e0f16-270">Utilisez ensuite hello **New-AzureRmVMSqlServerAutoBackupConfig** tooenable de commande et de configurer des sauvegardes de toostore paramètres hello v2 de sauvegarde automatisée dans le compte de stockage Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e0f16-270">Then use hello **New-AzureRmVMSqlServerAutoBackupConfig** command tooenable and configure hello Automated Backup v2 settings toostore backups in hello Azure storage account.</span></span> <span data-ttu-id="e0f16-271">Dans cet exemple, les sauvegardes de hello sont définies toobe conservée pendant 10 jours.</span><span class="sxs-lookup"><span data-stu-id="e0f16-271">In this example, hello backups are set toobe retained for 10 days.</span></span> <span data-ttu-id="e0f16-272">Les sauvegardes de bases de données système sont activées.</span><span class="sxs-lookup"><span data-stu-id="e0f16-272">System database backups are enabled.</span></span> <span data-ttu-id="e0f16-273">Les sauvegardes complètes sont planifiées pour être effectuées toutes les semaines, avec une fenêtre de temps commençant à 20 h 00 pendant deux heures.</span><span class="sxs-lookup"><span data-stu-id="e0f16-273">Full backups are scheduled for weekly with a time window starting at 20:00 for two hours.</span></span> <span data-ttu-id="e0f16-274">Les sauvegardes de journaux sont planifiées pour être effectuées toutes les 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="e0f16-274">Log backups are scheduled for every 30 minutes.</span></span> <span data-ttu-id="e0f16-275">Hello la deuxième commande, **Set-AzureRmVMSqlServerExtension**, hello de mises à jour spécifié de machine virtuelle Azure avec ces paramètres.</span><span class="sxs-lookup"><span data-stu-id="e0f16-275">hello second command, **Set-AzureRmVMSqlServerExtension**, updates hello specified Azure VM with these settings.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType Manual -FullBackupFrequency Weekly `
    -FullBackupStartHour 20 -FullBackupWindowInHours 2 `
    -LogBackupFrequencyInMinutes 30 

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname 
```

<span data-ttu-id="e0f16-276">Il peut prendre plusieurs minutes tooinstall et configurer hello IaaS Agent SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e0f16-276">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span> 

<span data-ttu-id="e0f16-277">le chiffrement tooenable, modifier hello toopass script précédent de hello **EnableEncryption** paramètre avec un mot de passe (chaîne sécurisée) hello **CertificatePassword** paramètre.</span><span class="sxs-lookup"><span data-stu-id="e0f16-277">tooenable encryption, modify hello previous script toopass hello **EnableEncryption** parameter along with a password (secure string) for hello **CertificatePassword** parameter.</span></span> <span data-ttu-id="e0f16-278">Hello script suivant active les paramètres de sauvegarde automatisée hello dans l’exemple précédent de hello et ajoute le chiffrement.</span><span class="sxs-lookup"><span data-stu-id="e0f16-278">hello following script enables hello Automated Backup settings in hello previous example and adds encryption.</span></span>

```powershell
$password = "P@ssw0rd"
$encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -EnableEncryption -CertificatePassword $encryptionpassword `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType Manual -FullBackupFrequency Weekly `
    -FullBackupStartHour 20 -FullBackupWindowInHours 2 `
    -LogBackupFrequencyInMinutes 30 

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

<span data-ttu-id="e0f16-279">tooconfirm vos paramètres sont appliqués, [vérifier la configuration de sauvegarde automatisée hello](#verifysettings).</span><span class="sxs-lookup"><span data-stu-id="e0f16-279">tooconfirm your settings are applied, [verify hello Automated Backup configuration](#verifysettings).</span></span>

### <a name="disable-automated-backup"></a><span data-ttu-id="e0f16-280">Désactiver la sauvegarde automatisée</span><span class="sxs-lookup"><span data-stu-id="e0f16-280">Disable Automated Backup</span></span>
<span data-ttu-id="e0f16-281">toodisable sauvegarde automatisée, exécution hello même script sans hello **-activer** paramètre toohello **New-AzureRmVMSqlServerAutoBackupConfig** commande.</span><span class="sxs-lookup"><span data-stu-id="e0f16-281">toodisable Automated Backup, run hello same script without hello **-Enable** parameter toohello **New-AzureRmVMSqlServerAutoBackupConfig** command.</span></span> <span data-ttu-id="e0f16-282">Hello absence de hello **-activer** fonctionnalité de paramètre signaux hello commande toodisable hello.</span><span class="sxs-lookup"><span data-stu-id="e0f16-282">hello absence of hello **-Enable** parameter signals hello command toodisable hello feature.</span></span> <span data-ttu-id="e0f16-283">Comme avec l’installation, il peut prendre plusieurs minutes toodisable la sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="e0f16-283">As with installation, it can take several minutes toodisable Automated Backup.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

### <a name="example-script"></a><span data-ttu-id="e0f16-284">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="e0f16-284">Example script</span></span>
<span data-ttu-id="e0f16-285">Hello script suivant fournit un ensemble de variables que vous pouvez personnaliser tooenable et configurer la sauvegarde automatisée pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e0f16-285">hello following script provides a set of variables that you can customize tooenable and configure Automated Backup for your VM.</span></span> <span data-ttu-id="e0f16-286">Dans ce cas, vous devrez peut-être le script de hello toocustomize selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="e0f16-286">In your case, you might need toocustomize hello script based on your requirements.</span></span> <span data-ttu-id="e0f16-287">Par exemple, vous auraient toomake modifications si vous souhaitez que la sauvegarde de hello toodisable de bases de données système ou activer le chiffrement.</span><span class="sxs-lookup"><span data-stu-id="e0f16-287">For example, you would have toomake changes if you wanted toodisable hello backup of system databases or enable encryption.</span></span>

```powershell
$vmname = "yourvmname"
$resourcegroupname = "vmresourcegroupname"
$region = “Azure region name such as EASTUS2”
$storage_accountname = “storageaccountname”
$storage_resourcegroupname = $resourcegroupname
$retentionperiod = 10
$backupscheduletype = "Manual"
$fullbackupfrequency = "Weekly"
$fullbackupstarthour = "20"
$fullbackupwindow = "2"
$logbackupfrequency = "30"

# ResourceGroupName is hello resource group which is hosting hello VM where you are deploying hello SQL IaaS Extension 

Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region

# Creates/use a storage account toostore hello backups

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region }

# Configure Automated Backup settings

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays $retentionperiod -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType $backupscheduletype -FullBackupFrequency $fullbackupfrequency `
    -FullBackupStartHour $fullbackupstarthour -FullBackupWindowInHours $fullbackupwindow `
    -LogBackupFrequencyInMinutes $logbackupfrequency

# Apply hello Automated Backup settings toohello VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="e0f16-288">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e0f16-288">Next steps</span></span>
<span data-ttu-id="e0f16-289">La sauvegarde automatisée v2 configure une sauvegarde managée sur les machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="e0f16-289">Automated Backup v2 configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="e0f16-290">Il est donc important trop[passez en revue la documentation hello pour la gestion de sauvegarde](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello comportement et les implications.</span><span class="sxs-lookup"><span data-stu-id="e0f16-290">So it is important too[review hello documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello behavior and implications.</span></span>

<span data-ttu-id="e0f16-291">Vous pouvez trouver de sauvegarde supplémentaire et restaurer des conseils pour SQL Server sur des machines virtuelles Azure dans la rubrique suivante de hello : [sauvegarde et de restauration pour SQL Server dans Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="e0f16-291">You can find additional backup and restore guidance for SQL Server on Azure VMs in hello following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).</span></span>

<span data-ttu-id="e0f16-292">Pour plus d’informations sur les autres tâches d’automatisation disponibles, voir [Extension de l’agent IaaS SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="e0f16-292">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="e0f16-293">Pour plus d’informations sur l’exécution de SQL Server sur des machines virtuelles Azure, voir [Vue d’ensemble de SQL Server sur les machines virtuelles Azure](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e0f16-293">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

