---
title: "Sauvegarde automatisée pour les machines virtuelles Azure SQL Server 2014 | Microsoft Docs"
description: "Décrit la fonctionnalité de sauvegarde automatisée pour les machines virtuelles exécutant SQL Server 2014 dans Azure. Cet article est spécifique aux machines virtuelles utilisant Resource Manager."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: bdc63fd1-db49-4e76-87d5-b5c6a890e53c
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 91aab896dd5f06c950ee0ed8f36cc6a953d91611
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="automated-backup-for-sql-server-2014-virtual-machines-resource-manager"></a><span data-ttu-id="8bf8e-104">Sauvegarde automatisée pour les machines virtuelles SQL Server 2014 (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="8bf8e-104">Automated Backup for SQL Server 2014 Virtual Machines (Resource Manager)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8bf8e-105">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="8bf8e-105">SQL Server 2014</span></span>](virtual-machines-windows-sql-automated-backup.md)
> * [<span data-ttu-id="8bf8e-106">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="8bf8e-106">SQL Server 2016</span></span>](virtual-machines-windows-sql-automated-backup-v2.md)

<span data-ttu-id="8bf8e-107">La sauvegarde automatisée configure automatiquement une [sauvegarde managée sur Microsoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) pour toutes les bases de données nouvelles et existantes sur une machine virtuelle Azure exécutant SQL Server 2014 Standard ou Enterprise.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-107">Automated Backup automatically configures [Managed Backup to Microsoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> <span data-ttu-id="8bf8e-108">Cela vous permet de configurer des sauvegardes régulières de base de données utilisant le stockage d’objets blob Azure durable.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-108">This enables you to configure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="8bf8e-109">La sauvegarde automatisée dépend l’ [extension de l’agent IaaS de SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="8bf8e-109">Automated Backup depends on the [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="8bf8e-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8bf8e-110">Prerequisites</span></span>
<span data-ttu-id="8bf8e-111">Pour utiliser la sauvegarde automatisée, prenez en compte les conditions préalables suivantes :</span><span class="sxs-lookup"><span data-stu-id="8bf8e-111">To use Automated Backup, consider the following prerequisites:</span></span>

<span data-ttu-id="8bf8e-112">**Système d’exploitation**:</span><span class="sxs-lookup"><span data-stu-id="8bf8e-112">**Operating System**:</span></span>

- <span data-ttu-id="8bf8e-113">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="8bf8e-113">Windows Server 2012</span></span>
- <span data-ttu-id="8bf8e-114">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="8bf8e-114">Windows Server 2012 R2</span></span>
- <span data-ttu-id="8bf8e-115">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="8bf8e-115">Windows Server 2016</span></span>

<span data-ttu-id="8bf8e-116">**Édition/version de SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="8bf8e-116">**SQL Server version/edition**:</span></span>

- <span data-ttu-id="8bf8e-117">SQL Server 2014 Standard</span><span class="sxs-lookup"><span data-stu-id="8bf8e-117">SQL Server 2014 Standard</span></span>
- <span data-ttu-id="8bf8e-118">SQL Server 2014 Enterprise</span><span class="sxs-lookup"><span data-stu-id="8bf8e-118">SQL Server 2014 Enterprise</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8bf8e-119">La sauvegarde automatisée fonctionne avec SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-119">Automated Backup works with SQL Server 2014.</span></span> <span data-ttu-id="8bf8e-120">Si vous utilisez SQL Server 2016, vous pouvez utiliser la sauvegarde automatisée en version 2 pour sauvegarder vos bases de données.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-120">If you are using SQL Server 2016, you can use Automated Backup v2 to back up your databases.</span></span> <span data-ttu-id="8bf8e-121">Pour plus d’informations, consultez [Sauvegarde automatisée en version 2 pour les machines virtuelles Azure SQL Server 2016](virtual-machines-windows-sql-automated-backup-v2.md).</span><span class="sxs-lookup"><span data-stu-id="8bf8e-121">For more information, see [Automated Backup v2 for SQL Server 2016 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).</span></span>

<span data-ttu-id="8bf8e-122">**Configuration de la base de données**:</span><span class="sxs-lookup"><span data-stu-id="8bf8e-122">**Database configuration**:</span></span>

- <span data-ttu-id="8bf8e-123">Les bases de données cibles doivent utiliser le modèle de récupération complète.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-123">Target databases must use the full recovery model.</span></span> <span data-ttu-id="8bf8e-124">Pour plus d’informations sur l’impact du modèle de récupération complète sur les sauvegardes, consultez [Sauvegarde en mode de récupération complète](https://technet.microsoft.com/library/ms190217.aspx).</span><span class="sxs-lookup"><span data-stu-id="8bf8e-124">For more information about the impact of the full recovery model on backups, see [Backup Under the Full Recovery Model](https://technet.microsoft.com/library/ms190217.aspx).</span></span>
- <span data-ttu-id="8bf8e-125">Les bases de données cibles doivent se trouver sur l’instance SQL Server par défaut.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-125">Target databases must be on the default SQL Server instance.</span></span> <span data-ttu-id="8bf8e-126">L’extension IaaS SQL Server ne prend pas en charge les instances nommées.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-126">The SQL Server IaaS Extension does not support named instances.</span></span>

<span data-ttu-id="8bf8e-127">**Modèle de déploiement Azure** :</span><span class="sxs-lookup"><span data-stu-id="8bf8e-127">**Azure deployment model**:</span></span>

- <span data-ttu-id="8bf8e-128">Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="8bf8e-128">Resource Manager</span></span>

<span data-ttu-id="8bf8e-129">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="8bf8e-129">**Azure PowerShell**:</span></span>

- <span data-ttu-id="8bf8e-130">[Installez les dernières commandes Azure PowerShell](/powershell/azure/overview) si vous projetez de configurer la sauvegarde automatisée avec PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-130">[Install the latest Azure PowerShell commands](/powershell/azure/overview) if you plan to configure Automated Backup with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="8bf8e-131">La sauvegarde automatisée utilise l’extension de l’agent IaaS de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-131">Automated Backup relies on the SQL Server IaaS Agent Extension.</span></span> <span data-ttu-id="8bf8e-132">Les images actuelles de la galerie de machines virtuelles SQL ajoutent cette extension par défaut.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-132">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="8bf8e-133">Pour plus d’informations, consultez [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md)(Extension de l’agent IaaS SQL Server).</span><span class="sxs-lookup"><span data-stu-id="8bf8e-133">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="8bf8e-134">Paramètres</span><span class="sxs-lookup"><span data-stu-id="8bf8e-134">Settings</span></span>

<span data-ttu-id="8bf8e-135">Le tableau suivant décrit les options qui peuvent être configurées pour une sauvegarde automatisée.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-135">The following table describes the options that can be configured for Automated Backup.</span></span> <span data-ttu-id="8bf8e-136">Les étapes de la configuration varient selon que vous utilisez les commandes du portail Azure ou Azure Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-136">The actual configuration steps vary depending on whether you use the Azure portal or Azure Windows PowerShell commands.</span></span>

| <span data-ttu-id="8bf8e-137">Paramètre</span><span class="sxs-lookup"><span data-stu-id="8bf8e-137">Setting</span></span> | <span data-ttu-id="8bf8e-138">Plage (par défaut)</span><span class="sxs-lookup"><span data-stu-id="8bf8e-138">Range (Default)</span></span> | <span data-ttu-id="8bf8e-139">Description</span><span class="sxs-lookup"><span data-stu-id="8bf8e-139">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8bf8e-140">**Sauvegarde automatisée**</span><span class="sxs-lookup"><span data-stu-id="8bf8e-140">**Automated Backup**</span></span> | <span data-ttu-id="8bf8e-141">Activer/Désactiver (désactivé)</span><span class="sxs-lookup"><span data-stu-id="8bf8e-141">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="8bf8e-142">Active ou désactive la sauvegarde automatisée d’une machine virtuelle Azure exécutant SQL Server 2014 Standard ou Enterprise.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-142">Enables or disables Automated Backup for an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> |
| <span data-ttu-id="8bf8e-143">**Période de rétention**</span><span class="sxs-lookup"><span data-stu-id="8bf8e-143">**Retention Period**</span></span> | <span data-ttu-id="8bf8e-144">1 à 30 jours (30 jours)</span><span class="sxs-lookup"><span data-stu-id="8bf8e-144">1-30 days (30 days)</span></span> | <span data-ttu-id="8bf8e-145">Nombre de jours durant lesquels une sauvegarde est conservée.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-145">The number of days to retain a backup.</span></span> |
| <span data-ttu-id="8bf8e-146">**Compte de stockage**</span><span class="sxs-lookup"><span data-stu-id="8bf8e-146">**Storage Account**</span></span> | <span data-ttu-id="8bf8e-147">Compte Azure Storage</span><span class="sxs-lookup"><span data-stu-id="8bf8e-147">Azure storage account</span></span> | <span data-ttu-id="8bf8e-148">Compte de stockage Azure à utiliser pour stocker les fichiers de sauvegarde automatisée dans le stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-148">An Azure storage account to use for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="8bf8e-149">Un conteneur est créé à cet emplacement pour stocker tous les fichiers de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-149">A container is created at this location to store all backup files.</span></span> <span data-ttu-id="8bf8e-150">La convention de dénomination des fichiers de sauvegarde inclut la date, l’heure et le nom de la machine.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-150">The backup file naming convention includes the date, time, and machine name.</span></span> |
| <span data-ttu-id="8bf8e-151">**Chiffrement**</span><span class="sxs-lookup"><span data-stu-id="8bf8e-151">**Encryption**</span></span> | <span data-ttu-id="8bf8e-152">Activer/Désactiver (désactivé)</span><span class="sxs-lookup"><span data-stu-id="8bf8e-152">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="8bf8e-153">Active ou désactive le chiffrement.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-153">Enables or disables encryption.</span></span> <span data-ttu-id="8bf8e-154">Quand le chiffrement est activé, les certificats utilisés pour restaurer la sauvegarde se trouvent dans le compte de stockage spécifié dans le même conteneur `automaticbackup` avec la même convention de dénomination.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-154">When encryption is enabled, the certificates used to restore the backup are located in the specified storage account in the same `automaticbackup` container using the same naming convention.</span></span> <span data-ttu-id="8bf8e-155">Si le mot de passe change, un nouveau certificat est généré avec ce mot de passe, mais l’ancien certificat est conservé pour restaurer les sauvegardes antérieures.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-155">If the password changes, a new certificate is generated with that password, but the old certificate remains to restore prior backups.</span></span> |
| <span data-ttu-id="8bf8e-156">**Mot de passe**</span><span class="sxs-lookup"><span data-stu-id="8bf8e-156">**Password**</span></span> | <span data-ttu-id="8bf8e-157">Texte du mot de passe</span><span class="sxs-lookup"><span data-stu-id="8bf8e-157">Password text</span></span> | <span data-ttu-id="8bf8e-158">Mot de passe pour les clés de chiffrement.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-158">A password for encryption keys.</span></span> <span data-ttu-id="8bf8e-159">Il est uniquement requis si le chiffrement est activé.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-159">This is only required if encryption is enabled.</span></span> <span data-ttu-id="8bf8e-160">Pour restaurer une sauvegarde chiffrée, vous devez disposer du mot de passe correct et du certificat associé qui a été utilisé lorsque la sauvegarde a été effectuée.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-160">In order to restore an encrypted backup, you must have the correct password and related certificate that was used at the time the backup was taken.</span></span> |

## <a name="configuration-in-the-portal"></a><span data-ttu-id="8bf8e-161">Configuration dans le portail</span><span class="sxs-lookup"><span data-stu-id="8bf8e-161">Configuration in the Portal</span></span>

<span data-ttu-id="8bf8e-162">Vous pouvez utiliser le portail Azure pour configurer la sauvegarde automatisée lors de l’approvisionnement ou pour des machines virtuelles SQL Server 2014 existantes.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-162">You can use the Azure portal to configure Automated Backup during provisioning or for existing SQL Server 2014 VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="8bf8e-163">Nouvelles machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="8bf8e-163">New VMs</span></span>

<span data-ttu-id="8bf8e-164">Utilisez le portail Azure pour configurer la sauvegarde automatisée quand vous créez une machine virtuelle SQL Server 2014 dans le modèle de déploiement Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-164">Use the Azure portal to configure Automated Backup when you create a new SQL Server 2014 Virtual Machine in the Resource Manager deployment model.</span></span>

<span data-ttu-id="8bf8e-165">Dans le panneau **Paramètres SQL Server**, sélectionnez **Sauvegarde automatisée**.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-165">In the **SQL Server settings** blade, select **Automated backup**.</span></span> <span data-ttu-id="8bf8e-166">La capture d’écran suivante du portail Azure illustre le panneau **Sauvegarde automatisée SQL** .</span><span class="sxs-lookup"><span data-stu-id="8bf8e-166">The following Azure portal screenshot shows the **SQL Automated Backup** blade.</span></span>

![Configuration d’une sauvegarde automatisée SQL dans le portail Azure](./media/virtual-machines-windows-sql-automated-backup/azure-sql-arm-autobackup.png)

<span data-ttu-id="8bf8e-168">Pour plus de contexte, voir la rubrique complète intitulée [Configuration d’une machine virtuelle SQL Server dans Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="8bf8e-168">For context, see the complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="8bf8e-169">Machines virtuelles existantes</span><span class="sxs-lookup"><span data-stu-id="8bf8e-169">Existing VMs</span></span>

<span data-ttu-id="8bf8e-170">Pour les machines virtuelles SQL Server existantes, sélectionnez votre machine virtuelle SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-170">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="8bf8e-171">Puis sélectionnez la section **Configuration de SQL Server** du panneau **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-171">Then select the **SQL Server configuration** section of the **Settings** blade.</span></span>

![Sauvegarde automatisée SQL pour les machines virtuelles existantes](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-existing-vms.png)

<span data-ttu-id="8bf8e-173">Dans le panneau **Configuration de SQL Server**, cliquez sur le bouton **Modifier** dans la section de sauvegarde automatisée.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-173">In the **SQL Server configuration** blade, click the **Edit** button in the Automated backup section.</span></span>

![Configurer la sauvegarde automatisée SQL pour les machines virtuelles existantes](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-configuration.png)

<span data-ttu-id="8bf8e-175">Lorsque vous avez terminé, cliquez sur le bouton **OK** au bas du panneau **Configuration de SQL Server** pour enregistrer vos modifications.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-175">When finished, click the **OK** button on the bottom of the **SQL Server configuration** blade to save your changes.</span></span>

<span data-ttu-id="8bf8e-176">Si vous activez la sauvegarde automatisée pour la première fois, Azure configure l’agent IaaS de SQL Server en arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-176">If you are enabling Automated Backup for the first time, Azure configures the SQL Server IaaS Agent in the background.</span></span> <span data-ttu-id="8bf8e-177">Pendant ce temps, le portail Azure n’indiquera peut-être pas que la sauvegarde automatisée est configurée.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-177">During this time, the Azure portal might not show that Automated Backup is configured.</span></span> <span data-ttu-id="8bf8e-178">Patientez quelques minutes jusqu’à ce que l’agent soit installé et configuré.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-178">Wait several minutes for the agent to be installed, configured.</span></span> <span data-ttu-id="8bf8e-179">Le portail Azure reflète alors les nouveaux paramètres.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-179">After that the Azure portal will reflect the new settings.</span></span>

> [!NOTE]
> <span data-ttu-id="8bf8e-180">Vous pouvez également configurer la sauvegarde automatisée à l’aide d’un modèle.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-180">You can also configure Automated Backup using a template.</span></span> <span data-ttu-id="8bf8e-181">Pour plus d’informations, consultez l’article [Azure quickstart template for Automated Backup](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update)(Modèle de démarrage rapide d’Azure pour la sauvegarde automatisée).</span><span class="sxs-lookup"><span data-stu-id="8bf8e-181">For more information, see [Azure quickstart template for Automated Backup](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update).</span></span>

## <a name="configuration-with-powershell"></a><span data-ttu-id="8bf8e-182">Configuration avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="8bf8e-182">Configuration with PowerShell</span></span>

<span data-ttu-id="8bf8e-183">Vous pouvez utiliser PowerShell pour configurer une sauvegarde automatisée.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-183">You can use PowerShell to configure Automated Backup.</span></span> <span data-ttu-id="8bf8e-184">Avant de commencer, vous devez :</span><span class="sxs-lookup"><span data-stu-id="8bf8e-184">Before you begin, you must:</span></span>

- <span data-ttu-id="8bf8e-185">[Télécharger et installer la version la plus récente d’Azure PowerShell](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="8bf8e-185">[Download and install the latest Azure PowerShell](http://aka.ms/webpi-azps).</span></span>
- <span data-ttu-id="8bf8e-186">Ouvrir Windows PowerShell et l’associer à votre compte.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-186">Open Windows PowerShell and associate it with your account.</span></span> <span data-ttu-id="8bf8e-187">Pour cela, procédez selon les étapes de la section [Configurer votre abonnement](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) de la rubrique consacrée à l’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-187">You can do this by following the steps in the [Configure your subscription](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) section of the provisioning topic.</span></span>

### <a name="install-the-sql-iaas-extension"></a><span data-ttu-id="8bf8e-188">Installer l’extension IaaS SQL</span><span class="sxs-lookup"><span data-stu-id="8bf8e-188">Install the SQL IaaS Extension</span></span>
<span data-ttu-id="8bf8e-189">Si vous avez configuré une machine virtuelle SQL Server à partir du portail Azure, l’extension IaaS SQL Server devrait déjà être installée.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-189">If you provisioned a SQL Server virtual machine from the Azure portal, the SQL Server IaaS Extension should already be installed.</span></span> <span data-ttu-id="8bf8e-190">Vous pouvez déterminer si cette extension est installée pour votre machine virtuelle en appelant la commande **Get-AzureRmVM** puis en examinant la propriété **Extensions**.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-190">You can determine if it is installed for your VM by calling **Get-AzureRmVM** command and examining the **Extensions** property.</span></span>

```powershell
$vmname = "vmname"
$resourcegroupname = "resourcegroupname"

(Get-AzureRmVM -Name $vmname -ResourceGroupName $resourcegroupname).Extensions
```

<span data-ttu-id="8bf8e-191">Si l’extension de l’agent IaaS SQL Server est installée, elle devrait s’afficher sous la forme « SqlIaaSAgent » ou « SQLIaaSExtension ».</span><span class="sxs-lookup"><span data-stu-id="8bf8e-191">If the SQL Server IaaS Agent extension is installed, you should see it listed as “SqlIaaSAgent” or “SQLIaaSExtension”.</span></span> <span data-ttu-id="8bf8e-192">La propriété **ProvisioningState** de l’extension devrait également indiquer « Succeeded » (Réussie).</span><span class="sxs-lookup"><span data-stu-id="8bf8e-192">**ProvisioningState** for the extension should also show “Succeeded”.</span></span>

<span data-ttu-id="8bf8e-193">Si elle n’est pas installée ou n’a pas pu être configurée, vous pouvez l’installer avec la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-193">If it is not installed or failed to be provisioned, you can install it with the following command.</span></span> <span data-ttu-id="8bf8e-194">Outre le nom de la machine virtuelle et le groupe de ressources, vous devez également spécifier la région (**$region**) où se trouve votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-194">In addition to the VM name and resource group, you must also specify the region (**$region**) that your VM is located in.</span></span>

```powershell
$region = “EASTUS2”
Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region
```

### <span data-ttu-id="8bf8e-195"><a id="verifysettings"></a> Vérifier les paramètres actuels</span><span class="sxs-lookup"><span data-stu-id="8bf8e-195"><a id="verifysettings"></a> Verify current settings</span></span>

<span data-ttu-id="8bf8e-196">Si vous avez activé la sauvegarde automatisée lors de la configuration, vous pouvez utiliser PowerShell pour vérifier votre configuration actuelle.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-196">If you enabled automated backup during provisioning, you can use PowerShell to check your current configuration.</span></span> <span data-ttu-id="8bf8e-197">Exécutez la commande **Get-AzureRmVMSqlServerExtension** et examinez la propriété **AutoBackupSettings** :</span><span class="sxs-lookup"><span data-stu-id="8bf8e-197">Run the **Get-AzureRmVMSqlServerExtension** command and examine the **AutoBackupSettings** property:</span></span>

```powershell
(Get-AzureRmVMSqlServerExtension -VMName $vmname -ResourceGroupName $resourcegroupname).AutoBackupSettings
```

<span data-ttu-id="8bf8e-198">La sortie doit ressembler à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="8bf8e-198">You should get output similar to the following:</span></span>

```
Enable                      : False
EnableEncryption            : False
RetentionPeriod             : -1
StorageUrl                  : NOTSET
StorageAccessKey            : 
Password                    : 
BackupSystemDbs             : False
BackupScheduleType          : 
FullBackupFrequency         : 
FullBackupStartTime         : 
FullBackupWindowHours       : 
LogBackupFrequency          : 
```

<span data-ttu-id="8bf8e-199">Si votre sortie montre que l’option **Enable** (Activer) est définie sur **False**, vous devez activer la sauvegarde automatisée.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-199">If your output shows that **Enable** is set to **False**, then you have to enable automated backup.</span></span> <span data-ttu-id="8bf8e-200">La bonne nouvelle est que vous activez et configurez la sauvegarde automatisée de la même façon.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-200">The good news is that you enable and configure Automated Backup in the same way.</span></span> <span data-ttu-id="8bf8e-201">Pour en savoir plus, consultez la section suivante.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-201">See the next section for this information.</span></span>

> [!NOTE] 
> <span data-ttu-id="8bf8e-202">Si vous vérifiez les paramètres immédiatement après une modification, les anciennes valeurs de configuration peuvent s’afficher.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-202">If you check the settings immediately after making a change, it is possible that you will get back the old configuration values.</span></span> <span data-ttu-id="8bf8e-203">Patientez quelques minutes et revérifiez les paramètres pour vous assurer que vos modifications ont bien été appliquées.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-203">Wait a few minutes and check the settings again to make sure that your changes were applied.</span></span>

### <a name="configure-automated-backup"></a><span data-ttu-id="8bf8e-204">Configurer une sauvegarde automatisée</span><span class="sxs-lookup"><span data-stu-id="8bf8e-204">Configure Automated Backup</span></span>
<span data-ttu-id="8bf8e-205">Vous pouvez utiliser PowerShell pour activer la sauvegarde automatisée ainsi que pour modifier sa configuration et son comportement à tout moment.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-205">You can use PowerShell to enable Automated Backup as well as to modify its configuration and behavior at any time.</span></span>

<span data-ttu-id="8bf8e-206">Tout d’abord, sélectionnez ou créez un compte de stockage pour les fichiers de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-206">First, select or create a storage account for the backup files.</span></span> <span data-ttu-id="8bf8e-207">Le script suivant sélectionne un compte de stockage ou le crée s’il n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-207">The following script selects a storage account or creates it if it does not exist.</span></span>

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
> <span data-ttu-id="8bf8e-208">La sauvegarde automatisée ne prend pas en charge le stockage des sauvegardes dans un stockage Premium, mais elle peut effectuer des sauvegardes à partir de disques de machines virtuelles qui utilisent le stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-208">Automated Backup does not support storing backups in premium storage, but it can take backups from VM disks which use Premium Storage.</span></span>

<span data-ttu-id="8bf8e-209">Utilisez ensuite la commande **New-AzureRmVMSqlServerAutoBackupConfig** pour activer et configurer les paramètres de sauvegarde automatisée afin de stocker les sauvegardes dans le compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-209">Then use the **New-AzureRmVMSqlServerAutoBackupConfig** command to enable and configure the Automated Backup settings to store backups in the Azure storage account.</span></span> <span data-ttu-id="8bf8e-210">Dans cet exemple, les sauvegardes sont définies pour être conservées pendant 10 jours.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-210">In this example, the backups are set to be retained for 10 days.</span></span> <span data-ttu-id="8bf8e-211">La seconde commande **Set-AzureRmVMSqlServerExtension** met à jour la machine virtuelle Azure spécifiée avec ces paramètres.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-211">The second command, **Set-AzureRmVMSqlServerExtension**, updates the specified Azure VM with these settings.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

<span data-ttu-id="8bf8e-212">L’installation et la configuration de l’agent IaaS de SQL Server peuvent prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-212">It could take several minutes to install and configure the SQL Server IaaS Agent.</span></span>

> [!NOTE]
> <span data-ttu-id="8bf8e-213">Il existe d’autres paramètres pour **New-AzureRmVMSqlServerAutoBackupConfig** qui s’appliquent uniquement à SQL Server 2016 et à la sauvegarde automatisée version 2.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-213">There are other settings for **New-AzureRmVMSqlServerAutoBackupConfig** that apply only to SQL Server 2016 and Automated Backup v2.</span></span> <span data-ttu-id="8bf8e-214">SQL Server 2014 ne prend pas en charge les paramètres suivants : **BackupSystemDbs**, **BackupScheduleType**, **FullBackupFrequency**, **FullBackupStartHour**, **FullBackupWindowInHours** et **LogBackupFrequencyInMinutes**.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-214">SQL Server 2014 does not support the following settings: **BackupSystemDbs**, **BackupScheduleType**, **FullBackupFrequency**, **FullBackupStartHour**, **FullBackupWindowInHours**, and **LogBackupFrequencyInMinutes**.</span></span> <span data-ttu-id="8bf8e-215">Si vous essayez de configurer ces paramètres sur une machine virtuelle SQL Server 2014, aucune erreur n’apparaît, mais les paramètres ne sont pas appliqués.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-215">If you attempt to configure these settings on a SQL Server 2014 virtual machine, there is no error, but the settings do not get applied.</span></span> <span data-ttu-id="8bf8e-216">Si vous souhaitez utiliser ces paramètres sur une machine virtuelle SQL Server 2016, consultez [Sauvegarde automatisée version 2 pour SQL Server 2016 dans des machines virtuelles Azure](virtual-machines-windows-sql-automated-backup-v2.md).</span><span class="sxs-lookup"><span data-stu-id="8bf8e-216">If you want to use these settings on a SQL Server 2016 virtual machine, see [Automated Backup v2 for SQL Server 2016 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).</span></span>

<span data-ttu-id="8bf8e-217">Pour activer le chiffrement, modifiez le script précédent pour transmettre le paramètre **EnableEncryption** avec un mot de passe (chaîne sécurisée) pour le paramètre **CertificatePassword**.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-217">To enable encryption, modify the previous script to pass the **EnableEncryption** parameter along with a password (secure string) for the **CertificatePassword** parameter.</span></span> <span data-ttu-id="8bf8e-218">Le script suivant active les paramètres de sauvegarde automatisée dans l’exemple précédent et ajoute le chiffrement.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-218">The following script enables the Automated Backup settings in the previous example and adds encryption.</span></span>

```powershell
$password = "P@ssw0rd"
$encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -EnableEncryption -CertificatePassword $encryptionpassword `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

<span data-ttu-id="8bf8e-219">Pour confirmer que vos paramètres ont été appliqués, [vérifiez la configuration de la sauvegarde automatisée](#verifysettings).</span><span class="sxs-lookup"><span data-stu-id="8bf8e-219">To confirm your settings are applied, [verify the Automated Backup configuration](#verifysettings).</span></span>

### <a name="disable-automated-backup"></a><span data-ttu-id="8bf8e-220">Désactiver la sauvegarde automatisée</span><span class="sxs-lookup"><span data-stu-id="8bf8e-220">Disable Automated Backup</span></span>

<span data-ttu-id="8bf8e-221">Pour désactiver la sauvegarde automatisée, exécutez le même script sans le paramètre **-Enable** pour la commande **New-AzureRmVMSqlServerAutoBackupConfig**.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-221">To disable Automated Backup, run the same script without the **-Enable** parameter to the **New-AzureRmVMSqlServerAutoBackupConfig** command.</span></span> <span data-ttu-id="8bf8e-222">L’absence du paramètre **-Enable** indique à la commande de désactiver la fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-222">The absence of the **-Enable** parameter signals the command to disable the feature.</span></span> <span data-ttu-id="8bf8e-223">À l’instar de l’installation, la désactivation de la sauvegarde automatisée peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-223">As with installation, it can take several minutes to disable Automated Backup.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

### <a name="example-script"></a><span data-ttu-id="8bf8e-224">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="8bf8e-224">Example script</span></span>

<span data-ttu-id="8bf8e-225">Le script suivant fournit un ensemble de variables que vous pouvez personnaliser afin d’activer et de configurer la sauvegarde automatisée pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-225">The following script provides a set of variables that you can customize to enable and configure Automated Backup for your VM.</span></span> <span data-ttu-id="8bf8e-226">Dans votre cas, vous devrez peut-être personnaliser le script selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-226">In your case, you might need to customize the script based on your requirements.</span></span> <span data-ttu-id="8bf8e-227">Par exemple, vous devrez apporter des modifications si vous souhaitez désactiver la sauvegarde des bases de données système ou activer le chiffrement.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-227">For example, you would have to make changes if you wanted to disable the backup of system databases or enable encryption.</span></span>

```powershell
$vmname = "yourvmname"
$resourcegroupname = "vmresourcegroupname"
$region = “Azure region name such as EASTUS2”
$storage_accountname = “storageaccountname”
$storage_resourcegroupname = $resourcegroupname
$retentionperiod = 10

# ResourceGroupName is the resource group which is hosting the VM where you are deploying the SQL IaaS Extension

Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region

# Creates/use a storage account to store the backups

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region }

# Configure Automated Backup settings

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays $retentionperiod -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

# Apply the Automated Backup settings to the VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="8bf8e-228">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8bf8e-228">Next steps</span></span>

<span data-ttu-id="8bf8e-229">La sauvegarde automatisée configure une sauvegarde managée sur les machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-229">Automated Backup configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="8bf8e-230">Il est donc important de [lire la documentation relative à la sauvegarde gérée](https://msdn.microsoft.com/library/dn449496.aspx) pour comprendre son comportement et ses implications.</span><span class="sxs-lookup"><span data-stu-id="8bf8e-230">So it is important to [review the documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) to understand the behavior and implications.</span></span>

<span data-ttu-id="8bf8e-231">Vous trouverez des conseils supplémentaires pour la sauvegarde et la restauration de SQL Server sur les machines virtuelles Azure dans la rubrique suivante : [Sauvegarde et restauration de SQL Server dans les machines virtuelles Azure](virtual-machines-windows-sql-backup-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="8bf8e-231">You can find additional backup and restore guidance for SQL Server on Azure VMs in the following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).</span></span>

<span data-ttu-id="8bf8e-232">Pour plus d’informations sur les autres tâches d’automatisation disponibles, voir [Extension de l’agent IaaS SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="8bf8e-232">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="8bf8e-233">Pour plus d’informations sur l’exécution de SQL Server sur des machines virtuelles Azure, voir [Vue d’ensemble de SQL Server sur les machines virtuelles Azure](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8bf8e-233">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

