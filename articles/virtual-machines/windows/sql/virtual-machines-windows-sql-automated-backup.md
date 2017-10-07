---
title: aaaAutomated sauvegarde pour les Machines virtuelles Azure 2014 SQL Server | Documents Microsoft
description: "Explique la fonctionnalité de sauvegarde automatisée hello pour SQL Server 2014 machines virtuelles s’exécutant dans Azure. Cet article est tooVMs spécifique à l’aide de hello Gestionnaire de ressources."
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
ms.openlocfilehash: c6803d8ef9f80e44a2f87918d87e099f1b562483
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-for-sql-server-2014-virtual-machines-resource-manager"></a><span data-ttu-id="38054-104">Sauvegarde automatisée pour les machines virtuelles SQL Server 2014 (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="38054-104">Automated Backup for SQL Server 2014 Virtual Machines (Resource Manager)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="38054-105">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="38054-105">SQL Server 2014</span></span>](virtual-machines-windows-sql-automated-backup.md)
> * [<span data-ttu-id="38054-106">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="38054-106">SQL Server 2016</span></span>](virtual-machines-windows-sql-automated-backup-v2.md)

<span data-ttu-id="38054-107">Sauvegarde automatisée configure automatiquement [tooMicrosoft de gestion de sauvegarde Azure](https://msdn.microsoft.com/library/dn449496.aspx) pour toutes les bases de données nouvelles et existantes sur une machine virtuelle de Azure exécutant SQL Server 2014 Standard ou Enterprise.</span><span class="sxs-lookup"><span data-stu-id="38054-107">Automated Backup automatically configures [Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> <span data-ttu-id="38054-108">Cela vous permet de tooconfigure des sauvegardes régulières de la base de données qui utilisent le stockage d’objets blob Azure durable.</span><span class="sxs-lookup"><span data-stu-id="38054-108">This enables you tooconfigure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="38054-109">Sauvegarde automatisée dépend hello [Extension de l’Agent SQL Server IaaS](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="38054-109">Automated Backup depends on hello [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="38054-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="38054-110">Prerequisites</span></span>
<span data-ttu-id="38054-111">toouse la sauvegarde, tenez compte des hello suivant des conditions préalables :</span><span class="sxs-lookup"><span data-stu-id="38054-111">toouse Automated Backup, consider hello following prerequisites:</span></span>

<span data-ttu-id="38054-112">**Système d’exploitation**:</span><span class="sxs-lookup"><span data-stu-id="38054-112">**Operating System**:</span></span>

- <span data-ttu-id="38054-113">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="38054-113">Windows Server 2012</span></span>
- <span data-ttu-id="38054-114">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="38054-114">Windows Server 2012 R2</span></span>
- <span data-ttu-id="38054-115">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="38054-115">Windows Server 2016</span></span>

<span data-ttu-id="38054-116">**Édition/version de SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="38054-116">**SQL Server version/edition**:</span></span>

- <span data-ttu-id="38054-117">SQL Server 2014 Standard</span><span class="sxs-lookup"><span data-stu-id="38054-117">SQL Server 2014 Standard</span></span>
- <span data-ttu-id="38054-118">SQL Server 2014 Enterprise</span><span class="sxs-lookup"><span data-stu-id="38054-118">SQL Server 2014 Enterprise</span></span>

> [!IMPORTANT]
> <span data-ttu-id="38054-119">La sauvegarde automatisée fonctionne avec SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="38054-119">Automated Backup works with SQL Server 2014.</span></span> <span data-ttu-id="38054-120">Si vous utilisez SQL Server 2016, vous pouvez utiliser la sauvegarde automatisée v2 tooback vos bases de données.</span><span class="sxs-lookup"><span data-stu-id="38054-120">If you are using SQL Server 2016, you can use Automated Backup v2 tooback up your databases.</span></span> <span data-ttu-id="38054-121">Pour plus d’informations, consultez [Sauvegarde automatisée en version 2 pour les machines virtuelles Azure SQL Server 2016](virtual-machines-windows-sql-automated-backup-v2.md).</span><span class="sxs-lookup"><span data-stu-id="38054-121">For more information, see [Automated Backup v2 for SQL Server 2016 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).</span></span>

<span data-ttu-id="38054-122">**Configuration de la base de données**:</span><span class="sxs-lookup"><span data-stu-id="38054-122">**Database configuration**:</span></span>

- <span data-ttu-id="38054-123">Bases de données cible doivent utiliser le mode de récupération complète hello.</span><span class="sxs-lookup"><span data-stu-id="38054-123">Target databases must use hello full recovery model.</span></span> <span data-ttu-id="38054-124">Pour plus d’informations sur l’impact de hello hello complète du mode de récupération sur les sauvegardes, consultez [hello sauvegarde sous le mode de récupération complète](https://technet.microsoft.com/library/ms190217.aspx).</span><span class="sxs-lookup"><span data-stu-id="38054-124">For more information about hello impact of hello full recovery model on backups, see [Backup Under hello Full Recovery Model](https://technet.microsoft.com/library/ms190217.aspx).</span></span>
- <span data-ttu-id="38054-125">Bases de données cible doivent être sur une instance de SQL Server par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="38054-125">Target databases must be on hello default SQL Server instance.</span></span> <span data-ttu-id="38054-126">Hello IaaS Extension de SQL Server ne prend pas en charge les instances nommées.</span><span class="sxs-lookup"><span data-stu-id="38054-126">hello SQL Server IaaS Extension does not support named instances.</span></span>

<span data-ttu-id="38054-127">**Modèle de déploiement Azure** :</span><span class="sxs-lookup"><span data-stu-id="38054-127">**Azure deployment model**:</span></span>

- <span data-ttu-id="38054-128">Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="38054-128">Resource Manager</span></span>

<span data-ttu-id="38054-129">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="38054-129">**Azure PowerShell**:</span></span>

- <span data-ttu-id="38054-130">[Installez les commandes Azure PowerShell dernière hello](/powershell/azure/overview) si vous envisagez de tooconfigure sauvegarde automatisée avec PowerShell.</span><span class="sxs-lookup"><span data-stu-id="38054-130">[Install hello latest Azure PowerShell commands](/powershell/azure/overview) if you plan tooconfigure Automated Backup with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="38054-131">Sauvegarde automatisée s’appuie sur hello Extension de l’Agent SQL Server IaaS.</span><span class="sxs-lookup"><span data-stu-id="38054-131">Automated Backup relies on hello SQL Server IaaS Agent Extension.</span></span> <span data-ttu-id="38054-132">Les images actuelles de la galerie de machines virtuelles SQL ajoutent cette extension par défaut.</span><span class="sxs-lookup"><span data-stu-id="38054-132">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="38054-133">Pour plus d’informations, consultez [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md)(Extension de l’agent IaaS SQL Server).</span><span class="sxs-lookup"><span data-stu-id="38054-133">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="38054-134">Paramètres</span><span class="sxs-lookup"><span data-stu-id="38054-134">Settings</span></span>

<span data-ttu-id="38054-135">Hello tableau suivant décrit les options de hello qui peuvent être configurées pour la sauvegarde automatisée.</span><span class="sxs-lookup"><span data-stu-id="38054-135">hello following table describes hello options that can be configured for Automated Backup.</span></span> <span data-ttu-id="38054-136">étapes de configuration réelles Hello varient selon que vous utilisez hello portail Azure ou des commandes PowerShell de Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="38054-136">hello actual configuration steps vary depending on whether you use hello Azure portal or Azure Windows PowerShell commands.</span></span>

| <span data-ttu-id="38054-137">Paramètre</span><span class="sxs-lookup"><span data-stu-id="38054-137">Setting</span></span> | <span data-ttu-id="38054-138">Plage (par défaut)</span><span class="sxs-lookup"><span data-stu-id="38054-138">Range (Default)</span></span> | <span data-ttu-id="38054-139">Description</span><span class="sxs-lookup"><span data-stu-id="38054-139">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38054-140">**Sauvegarde automatisée**</span><span class="sxs-lookup"><span data-stu-id="38054-140">**Automated Backup**</span></span> | <span data-ttu-id="38054-141">Activer/Désactiver (désactivé)</span><span class="sxs-lookup"><span data-stu-id="38054-141">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="38054-142">Active ou désactive la sauvegarde automatisée d’une machine virtuelle Azure exécutant SQL Server 2014 Standard ou Enterprise.</span><span class="sxs-lookup"><span data-stu-id="38054-142">Enables or disables Automated Backup for an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> |
| <span data-ttu-id="38054-143">**Période de rétention**</span><span class="sxs-lookup"><span data-stu-id="38054-143">**Retention Period**</span></span> | <span data-ttu-id="38054-144">1 à 30 jours (30 jours)</span><span class="sxs-lookup"><span data-stu-id="38054-144">1-30 days (30 days)</span></span> | <span data-ttu-id="38054-145">nombre de Hello de jours tooretain une sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="38054-145">hello number of days tooretain a backup.</span></span> |
| <span data-ttu-id="38054-146">**Compte de stockage**</span><span class="sxs-lookup"><span data-stu-id="38054-146">**Storage Account**</span></span> | <span data-ttu-id="38054-147">Compte Azure Storage</span><span class="sxs-lookup"><span data-stu-id="38054-147">Azure storage account</span></span> | <span data-ttu-id="38054-148">Un toouse de compte de stockage Azure pour stocker les fichiers de sauvegarde automatisée dans le stockage blob.</span><span class="sxs-lookup"><span data-stu-id="38054-148">An Azure storage account toouse for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="38054-149">Un conteneur est créé à cet emplacement toostore tous les fichiers de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="38054-149">A container is created at this location toostore all backup files.</span></span> <span data-ttu-id="38054-150">fichier de sauvegarde Hello convention d’affectation de noms inclut hello date, heure et nom de l’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="38054-150">hello backup file naming convention includes hello date, time, and machine name.</span></span> |
| <span data-ttu-id="38054-151">**Chiffrement**</span><span class="sxs-lookup"><span data-stu-id="38054-151">**Encryption**</span></span> | <span data-ttu-id="38054-152">Activer/Désactiver (désactivé)</span><span class="sxs-lookup"><span data-stu-id="38054-152">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="38054-153">Active ou désactive le chiffrement.</span><span class="sxs-lookup"><span data-stu-id="38054-153">Enables or disables encryption.</span></span> <span data-ttu-id="38054-154">Lorsque le chiffrement est activé, hello certificats utilisés toorestore hello sauvegarde se trouvent dans hello spécifié du compte de stockage Bonjour même `automaticbackup` conteneur à l’aide de hello même convention d’affectation de noms.</span><span class="sxs-lookup"><span data-stu-id="38054-154">When encryption is enabled, hello certificates used toorestore hello backup are located in hello specified storage account in hello same `automaticbackup` container using hello same naming convention.</span></span> <span data-ttu-id="38054-155">Si le mot de passe hello change, un nouveau certificat est généré avec ce mot de passe, mais hello ancien certificat est conservé toorestore les sauvegardes antérieures.</span><span class="sxs-lookup"><span data-stu-id="38054-155">If hello password changes, a new certificate is generated with that password, but hello old certificate remains toorestore prior backups.</span></span> |
| <span data-ttu-id="38054-156">**Mot de passe**</span><span class="sxs-lookup"><span data-stu-id="38054-156">**Password**</span></span> | <span data-ttu-id="38054-157">Texte du mot de passe</span><span class="sxs-lookup"><span data-stu-id="38054-157">Password text</span></span> | <span data-ttu-id="38054-158">Mot de passe pour les clés de chiffrement.</span><span class="sxs-lookup"><span data-stu-id="38054-158">A password for encryption keys.</span></span> <span data-ttu-id="38054-159">Il est uniquement requis si le chiffrement est activé.</span><span class="sxs-lookup"><span data-stu-id="38054-159">This is only required if encryption is enabled.</span></span> <span data-ttu-id="38054-160">Dans l’ordre toorestore une sauvegarde chiffrée, vous devez avoir mot de passe correct hello et du certificat associé qui a été utilisé au moment de hello hello sauvegarde a été effectuée.</span><span class="sxs-lookup"><span data-stu-id="38054-160">In order toorestore an encrypted backup, you must have hello correct password and related certificate that was used at hello time hello backup was taken.</span></span> |

## <a name="configuration-in-hello-portal"></a><span data-ttu-id="38054-161">Configuration Bonjour portail</span><span class="sxs-lookup"><span data-stu-id="38054-161">Configuration in hello Portal</span></span>

<span data-ttu-id="38054-162">Vous pouvez utiliser hello tooconfigure portail Azure la sauvegarde lors de la configuration ou de machines virtuelles SQL Server 2014 existantes.</span><span class="sxs-lookup"><span data-stu-id="38054-162">You can use hello Azure portal tooconfigure Automated Backup during provisioning or for existing SQL Server 2014 VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="38054-163">Nouvelles machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="38054-163">New VMs</span></span>

<span data-ttu-id="38054-164">Utilisez hello tooconfigure portail Azure la sauvegarde lorsque vous créez une nouvelle Machine virtuelle SQL Server 2014 dans le modèle de déploiement du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="38054-164">Use hello Azure portal tooconfigure Automated Backup when you create a new SQL Server 2014 Virtual Machine in hello Resource Manager deployment model.</span></span>

<span data-ttu-id="38054-165">Bonjour **paramètres SQL Server** panneau, sélectionnez **sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="38054-165">In hello **SQL Server settings** blade, select **Automated backup**.</span></span> <span data-ttu-id="38054-166">Bonjour Azure portail montre hello **sauvegarde automatisée SQL** panneau.</span><span class="sxs-lookup"><span data-stu-id="38054-166">hello following Azure portal screenshot shows hello **SQL Automated Backup** blade.</span></span>

![Configuration d’une sauvegarde automatisée SQL dans le portail Azure](./media/virtual-machines-windows-sql-automated-backup/azure-sql-arm-autobackup.png)

<span data-ttu-id="38054-168">Pour le contexte, consultez la rubrique complète de hello relative [approvisionner un ordinateur virtuel de SQL Server dans Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="38054-168">For context, see hello complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="38054-169">Machines virtuelles existantes</span><span class="sxs-lookup"><span data-stu-id="38054-169">Existing VMs</span></span>

<span data-ttu-id="38054-170">Pour les machines virtuelles SQL Server existantes, sélectionnez votre machine virtuelle SQL Server.</span><span class="sxs-lookup"><span data-stu-id="38054-170">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="38054-171">Puis sélectionnez hello **configuration de SQL Server** section Hello **paramètres** panneau.</span><span class="sxs-lookup"><span data-stu-id="38054-171">Then select hello **SQL Server configuration** section of hello **Settings** blade.</span></span>

![Sauvegarde automatisée SQL pour les machines virtuelles existantes](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-existing-vms.png)

<span data-ttu-id="38054-173">Bonjour **configuration de SQL Server** panneau, cliquez sur hello **modifier** bouton Bonjour automatisée de section de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="38054-173">In hello **SQL Server configuration** blade, click hello **Edit** button in hello Automated backup section.</span></span>

![Configurer la sauvegarde automatisée SQL pour les machines virtuelles existantes](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-configuration.png)

<span data-ttu-id="38054-175">Lorsque vous avez terminé, cliquez sur hello **OK** bouton bas hello Hello **configuration de SQL Server** panneau toosave vos modifications.</span><span class="sxs-lookup"><span data-stu-id="38054-175">When finished, click hello **OK** button on hello bottom of hello **SQL Server configuration** blade toosave your changes.</span></span>

<span data-ttu-id="38054-176">Si vous activez le sauvegarde automatisée pour hello première fois, Azure configure hello Agent SQL Server IaaS en arrière-plan de hello.</span><span class="sxs-lookup"><span data-stu-id="38054-176">If you are enabling Automated Backup for hello first time, Azure configures hello SQL Server IaaS Agent in hello background.</span></span> <span data-ttu-id="38054-177">Pendant ce temps, hello portail Azure peut ne pas affiche que la sauvegarde automatisée est configurée.</span><span class="sxs-lookup"><span data-stu-id="38054-177">During this time, hello Azure portal might not show that Automated Backup is configured.</span></span> <span data-ttu-id="38054-178">Attendez quelques minutes pour hello toobe de l’agent installé, configuré.</span><span class="sxs-lookup"><span data-stu-id="38054-178">Wait several minutes for hello agent toobe installed, configured.</span></span> <span data-ttu-id="38054-179">Après ce hello Azure portal reflètent les nouveaux paramètres de hello.</span><span class="sxs-lookup"><span data-stu-id="38054-179">After that hello Azure portal will reflect hello new settings.</span></span>

> [!NOTE]
> <span data-ttu-id="38054-180">Vous pouvez également configurer la sauvegarde automatisée à l’aide d’un modèle.</span><span class="sxs-lookup"><span data-stu-id="38054-180">You can also configure Automated Backup using a template.</span></span> <span data-ttu-id="38054-181">Pour plus d’informations, consultez l’article [Azure quickstart template for Automated Backup](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update)(Modèle de démarrage rapide d’Azure pour la sauvegarde automatisée).</span><span class="sxs-lookup"><span data-stu-id="38054-181">For more information, see [Azure quickstart template for Automated Backup](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update).</span></span>

## <a name="configuration-with-powershell"></a><span data-ttu-id="38054-182">Configuration avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="38054-182">Configuration with PowerShell</span></span>

<span data-ttu-id="38054-183">Vous pouvez utiliser PowerShell tooconfigure la sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="38054-183">You can use PowerShell tooconfigure Automated Backup.</span></span> <span data-ttu-id="38054-184">Avant de commencer, vous devez :</span><span class="sxs-lookup"><span data-stu-id="38054-184">Before you begin, you must:</span></span>

- <span data-ttu-id="38054-185">[Téléchargez et installez hello la dernière version d’Azure PowerShell](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="38054-185">[Download and install hello latest Azure PowerShell](http://aka.ms/webpi-azps).</span></span>
- <span data-ttu-id="38054-186">Ouvrir Windows PowerShell et l’associer à votre compte.</span><span class="sxs-lookup"><span data-stu-id="38054-186">Open Windows PowerShell and associate it with your account.</span></span> <span data-ttu-id="38054-187">Vous pouvez faire cela hello comme suit dans hello [configurer votre abonnement](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) section Hello rubrique de configuration.</span><span class="sxs-lookup"><span data-stu-id="38054-187">You can do this by following hello steps in hello [Configure your subscription](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) section of hello provisioning topic.</span></span>

### <a name="install-hello-sql-iaas-extension"></a><span data-ttu-id="38054-188">Installer hello IaaS Extension de SQL</span><span class="sxs-lookup"><span data-stu-id="38054-188">Install hello SQL IaaS Extension</span></span>
<span data-ttu-id="38054-189">Si vous avez configuré un ordinateur virtuel SQL Server hello portail Azure, hello IaaS Extension de SQL Server doit déjà être installé.</span><span class="sxs-lookup"><span data-stu-id="38054-189">If you provisioned a SQL Server virtual machine from hello Azure portal, hello SQL Server IaaS Extension should already be installed.</span></span> <span data-ttu-id="38054-190">Vous pouvez déterminer si elle est installée pour votre machine virtuelle en appelant **Get-AzureRmVM** commande et en examinant hello **Extensions** propriété.</span><span class="sxs-lookup"><span data-stu-id="38054-190">You can determine if it is installed for your VM by calling **Get-AzureRmVM** command and examining hello **Extensions** property.</span></span>

```powershell
$vmname = "vmname"
$resourcegroupname = "resourcegroupname"

(Get-AzureRmVM -Name $vmname -ResourceGroupName $resourcegroupname).Extensions
```

<span data-ttu-id="38054-191">Si hello extension SQL Server IaaS Agent est installé, vous devez voir qu'il répertorié comme « Sqliaasagent n’est » ou « SQLIaaSExtension ».</span><span class="sxs-lookup"><span data-stu-id="38054-191">If hello SQL Server IaaS Agent extension is installed, you should see it listed as “SqlIaaSAgent” or “SQLIaaSExtension”.</span></span> <span data-ttu-id="38054-192">**ProvisioningState** pour l’extension de hello doit également indiquer « Réussi ».</span><span class="sxs-lookup"><span data-stu-id="38054-192">**ProvisioningState** for hello extension should also show “Succeeded”.</span></span>

<span data-ttu-id="38054-193">S’il n’est pas installé ou a échoué toobe configuré, vous pouvez l’installer avec hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="38054-193">If it is not installed or failed toobe provisioned, you can install it with hello following command.</span></span> <span data-ttu-id="38054-194">Dans Ajout toohello nom et ressource groupe virtuelle, vous devez également spécifier la région de hello (**$region**) où se trouve votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="38054-194">In addition toohello VM name and resource group, you must also specify hello region (**$region**) that your VM is located in.</span></span>

```powershell
$region = “EASTUS2”
Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region
```

### <span data-ttu-id="38054-195"><a id="verifysettings"></a> Vérifier les paramètres actuels</span><span class="sxs-lookup"><span data-stu-id="38054-195"><a id="verifysettings"></a> Verify current settings</span></span>

<span data-ttu-id="38054-196">Si vous avez activé la sauvegarde automatisée lors de la configuration, vous pouvez utiliser PowerShell toocheck votre configuration actuelle.</span><span class="sxs-lookup"><span data-stu-id="38054-196">If you enabled automated backup during provisioning, you can use PowerShell toocheck your current configuration.</span></span> <span data-ttu-id="38054-197">Exécutez hello **Get-AzureRmVMSqlServerExtension** de commandes et examiner hello **AutoBackupSettings** propriété :</span><span class="sxs-lookup"><span data-stu-id="38054-197">Run hello **Get-AzureRmVMSqlServerExtension** command and examine hello **AutoBackupSettings** property:</span></span>

```powershell
(Get-AzureRmVMSqlServerExtension -VMName $vmname -ResourceGroupName $resourcegroupname).AutoBackupSettings
```

<span data-ttu-id="38054-198">Vous devez obtenir suivant toohello similaire de sortie :</span><span class="sxs-lookup"><span data-stu-id="38054-198">You should get output similar toohello following:</span></span>

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

<span data-ttu-id="38054-199">Si votre sortie montre que **activer** est défini trop**False**, vous devez effectuer des sauvegardes automatiques tooenable.</span><span class="sxs-lookup"><span data-stu-id="38054-199">If your output shows that **Enable** is set too**False**, then you have tooenable automated backup.</span></span> <span data-ttu-id="38054-200">Bonjour excellente est activer et configurer la sauvegarde automatisée Bonjour identique.</span><span class="sxs-lookup"><span data-stu-id="38054-200">hello good news is that you enable and configure Automated Backup in hello same way.</span></span> <span data-ttu-id="38054-201">Consultez hello la section suivante pour obtenir des informations.</span><span class="sxs-lookup"><span data-stu-id="38054-201">See hello next section for this information.</span></span>

> [!NOTE] 
> <span data-ttu-id="38054-202">Si vous vérifiez les paramètres de hello immédiatement après une modification, il est possible que vous obtenez les valeurs de configuration anciennes hello.</span><span class="sxs-lookup"><span data-stu-id="38054-202">If you check hello settings immediately after making a change, it is possible that you will get back hello old configuration values.</span></span> <span data-ttu-id="38054-203">Attendez quelques minutes et vérifier les paramètres de hello à nouveau les toomake sûr que vos modifications ont été appliquées.</span><span class="sxs-lookup"><span data-stu-id="38054-203">Wait a few minutes and check hello settings again toomake sure that your changes were applied.</span></span>

### <a name="configure-automated-backup"></a><span data-ttu-id="38054-204">Configurer une sauvegarde automatisée</span><span class="sxs-lookup"><span data-stu-id="38054-204">Configure Automated Backup</span></span>
<span data-ttu-id="38054-205">Vous pouvez utiliser les PowerShell tooenable la sauvegarde, ainsi que toomodify sa configuration et son comportement à tout moment.</span><span class="sxs-lookup"><span data-stu-id="38054-205">You can use PowerShell tooenable Automated Backup as well as toomodify its configuration and behavior at any time.</span></span>

<span data-ttu-id="38054-206">Tout d’abord, sélectionnez ou créez un compte de stockage hello pour les fichiers de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="38054-206">First, select or create a storage account for hello backup files.</span></span> <span data-ttu-id="38054-207">Hello script suivant sélectionne un compte de stockage ou la crée si elle n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="38054-207">hello following script selects a storage account or creates it if it does not exist.</span></span>

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
> <span data-ttu-id="38054-208">La sauvegarde automatisée ne prend pas en charge le stockage des sauvegardes dans un stockage Premium, mais elle peut effectuer des sauvegardes à partir de disques de machines virtuelles qui utilisent le stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="38054-208">Automated Backup does not support storing backups in premium storage, but it can take backups from VM disks which use Premium Storage.</span></span>

<span data-ttu-id="38054-209">Utilisez ensuite hello **New-AzureRmVMSqlServerAutoBackupConfig** tooenable de commande et de configurer des sauvegardes de toostore de paramètres de sauvegarde automatisée hello Bonjour compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="38054-209">Then use hello **New-AzureRmVMSqlServerAutoBackupConfig** command tooenable and configure hello Automated Backup settings toostore backups in hello Azure storage account.</span></span> <span data-ttu-id="38054-210">Dans cet exemple, les sauvegardes de hello sont définies toobe conservée pendant 10 jours.</span><span class="sxs-lookup"><span data-stu-id="38054-210">In this example, hello backups are set toobe retained for 10 days.</span></span> <span data-ttu-id="38054-211">Hello la deuxième commande, **Set-AzureRmVMSqlServerExtension**, hello de mises à jour spécifié de machine virtuelle Azure avec ces paramètres.</span><span class="sxs-lookup"><span data-stu-id="38054-211">hello second command, **Set-AzureRmVMSqlServerExtension**, updates hello specified Azure VM with these settings.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

<span data-ttu-id="38054-212">Il peut prendre plusieurs minutes tooinstall et configurer hello IaaS Agent SQL Server.</span><span class="sxs-lookup"><span data-stu-id="38054-212">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span>

> [!NOTE]
> <span data-ttu-id="38054-213">Autres paramètres pour **New-AzureRmVMSqlServerAutoBackupConfig** qui s’appliquent uniquement tooSQL Server 2016 et v2 de sauvegarde automatisée.</span><span class="sxs-lookup"><span data-stu-id="38054-213">There are other settings for **New-AzureRmVMSqlServerAutoBackupConfig** that apply only tooSQL Server 2016 and Automated Backup v2.</span></span> <span data-ttu-id="38054-214">SQL Server 2014 ne prend pas en charge hello suivant paramètres : **BackupSystemDbs**, **BackupScheduleType**, **FullBackupFrequency**,  **FullBackupStartHour**, **FullBackupWindowInHours**, et **LogBackupFrequencyInMinutes**.</span><span class="sxs-lookup"><span data-stu-id="38054-214">SQL Server 2014 does not support hello following settings: **BackupSystemDbs**, **BackupScheduleType**, **FullBackupFrequency**, **FullBackupStartHour**, **FullBackupWindowInHours**, and **LogBackupFrequencyInMinutes**.</span></span> <span data-ttu-id="38054-215">Si vous essayez de tooconfigure ces paramètres sur un ordinateur virtuel de SQL Server 2014, il n’existe aucune erreur, mais les paramètres hello ne sont pas appliquées.</span><span class="sxs-lookup"><span data-stu-id="38054-215">If you attempt tooconfigure these settings on a SQL Server 2014 virtual machine, there is no error, but hello settings do not get applied.</span></span> <span data-ttu-id="38054-216">Si vous souhaitez que ces paramètres sur un ordinateur virtuel de SQL Server 2016 toouse, consultez [v2 de sauvegarde automatisée pour les Machines virtuelles Azure 2016 SQL Server](virtual-machines-windows-sql-automated-backup-v2.md).</span><span class="sxs-lookup"><span data-stu-id="38054-216">If you want toouse these settings on a SQL Server 2016 virtual machine, see [Automated Backup v2 for SQL Server 2016 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).</span></span>

<span data-ttu-id="38054-217">le chiffrement tooenable, modifier hello toopass script précédent de hello **EnableEncryption** paramètre avec un mot de passe (chaîne sécurisée) hello **CertificatePassword** paramètre.</span><span class="sxs-lookup"><span data-stu-id="38054-217">tooenable encryption, modify hello previous script toopass hello **EnableEncryption** parameter along with a password (secure string) for hello **CertificatePassword** parameter.</span></span> <span data-ttu-id="38054-218">Hello script suivant active les paramètres de sauvegarde automatisée hello dans l’exemple précédent de hello et ajoute le chiffrement.</span><span class="sxs-lookup"><span data-stu-id="38054-218">hello following script enables hello Automated Backup settings in hello previous example and adds encryption.</span></span>

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

<span data-ttu-id="38054-219">tooconfirm vos paramètres sont appliqués, [vérifier la configuration de sauvegarde automatisée hello](#verifysettings).</span><span class="sxs-lookup"><span data-stu-id="38054-219">tooconfirm your settings are applied, [verify hello Automated Backup configuration](#verifysettings).</span></span>

### <a name="disable-automated-backup"></a><span data-ttu-id="38054-220">Désactiver la sauvegarde automatisée</span><span class="sxs-lookup"><span data-stu-id="38054-220">Disable Automated Backup</span></span>

<span data-ttu-id="38054-221">toodisable sauvegarde automatisée, exécution hello même script sans hello **-activer** paramètre toohello **New-AzureRmVMSqlServerAutoBackupConfig** commande.</span><span class="sxs-lookup"><span data-stu-id="38054-221">toodisable Automated Backup, run hello same script without hello **-Enable** parameter toohello **New-AzureRmVMSqlServerAutoBackupConfig** command.</span></span> <span data-ttu-id="38054-222">Hello absence de hello **-activer** fonctionnalité de paramètre signaux hello commande toodisable hello.</span><span class="sxs-lookup"><span data-stu-id="38054-222">hello absence of hello **-Enable** parameter signals hello command toodisable hello feature.</span></span> <span data-ttu-id="38054-223">Comme avec l’installation, il peut prendre plusieurs minutes toodisable la sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="38054-223">As with installation, it can take several minutes toodisable Automated Backup.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

### <a name="example-script"></a><span data-ttu-id="38054-224">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="38054-224">Example script</span></span>

<span data-ttu-id="38054-225">Hello script suivant fournit un ensemble de variables que vous pouvez personnaliser tooenable et configurer la sauvegarde automatisée pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="38054-225">hello following script provides a set of variables that you can customize tooenable and configure Automated Backup for your VM.</span></span> <span data-ttu-id="38054-226">Dans ce cas, vous devrez peut-être le script de hello toocustomize selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="38054-226">In your case, you might need toocustomize hello script based on your requirements.</span></span> <span data-ttu-id="38054-227">Par exemple, vous auraient toomake modifications si vous souhaitez que la sauvegarde de hello toodisable de bases de données système ou activer le chiffrement.</span><span class="sxs-lookup"><span data-stu-id="38054-227">For example, you would have toomake changes if you wanted toodisable hello backup of system databases or enable encryption.</span></span>

```powershell
$vmname = "yourvmname"
$resourcegroupname = "vmresourcegroupname"
$region = “Azure region name such as EASTUS2”
$storage_accountname = “storageaccountname”
$storage_resourcegroupname = $resourcegroupname
$retentionperiod = 10

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
    -ResourceGroupName $storage_resourcegroupname

# Apply hello Automated Backup settings toohello VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="38054-228">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="38054-228">Next steps</span></span>

<span data-ttu-id="38054-229">La sauvegarde automatisée configure une sauvegarde managée sur les machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="38054-229">Automated Backup configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="38054-230">Il est donc important trop[passez en revue la documentation hello pour la gestion de sauvegarde](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello comportement et les implications.</span><span class="sxs-lookup"><span data-stu-id="38054-230">So it is important too[review hello documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello behavior and implications.</span></span>

<span data-ttu-id="38054-231">Vous pouvez trouver de sauvegarde supplémentaire et restaurer des conseils pour SQL Server sur des machines virtuelles Azure dans la rubrique suivante de hello : [sauvegarde et de restauration pour SQL Server dans Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="38054-231">You can find additional backup and restore guidance for SQL Server on Azure VMs in hello following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).</span></span>

<span data-ttu-id="38054-232">Pour plus d’informations sur les autres tâches d’automatisation disponibles, voir [Extension de l’agent IaaS SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="38054-232">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="38054-233">Pour plus d’informations sur l’exécution de SQL Server sur des machines virtuelles Azure, voir [Vue d’ensemble de SQL Server sur les machines virtuelles Azure](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="38054-233">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

