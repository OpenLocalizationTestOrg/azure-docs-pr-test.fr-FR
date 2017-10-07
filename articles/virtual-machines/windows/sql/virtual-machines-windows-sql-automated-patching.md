---
title: "aaaAutomated mise à jour corrective pour les machines virtuelles SQL Server (Gestionnaire de ressources) | Documents Microsoft"
description: "Explique les fonctionnalité de correctifs automatiques hello pour les Machines virtuelles SQL Server s’exécutant dans Azure à l’aide du Gestionnaire de ressources."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 58232e92-318f-456b-8f0a-2201a541e08d
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 8bb8d0fb265e69d7bbf1fa047f5ceef02e7c56fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-resource-manager"></a><span data-ttu-id="2e09f-103">Mise à jour corrective automatisée pour SQL Server dans Azure Virtual Machines (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="2e09f-103">Automated Patching for SQL Server in Azure Virtual Machines (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2e09f-104">Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="2e09f-104">Resource Manager</span></span>](virtual-machines-windows-sql-automated-patching.md)
> * [<span data-ttu-id="2e09f-105">Classique</span><span class="sxs-lookup"><span data-stu-id="2e09f-105">Classic</span></span>](../classic/sql-automated-patching.md)
> 
> 

<span data-ttu-id="2e09f-106">La mise à jour corrective automatisée établit une fenêtre de maintenance pour une machine virtuelle Azure exécutant SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2e09f-106">Automated Patching establishes a maintenance window for an Azure Virtual Machine running SQL Server.</span></span> <span data-ttu-id="2e09f-107">Les mises à jour automatisées ne peuvent être installées qu’au cours de cette fenêtre de maintenance.</span><span class="sxs-lookup"><span data-stu-id="2e09f-107">Automated Updates can only be installed during this maintenance window.</span></span> <span data-ttu-id="2e09f-108">Pour SQL Server, cette rescriction garantit que les mises à jour système et les éventuels redémarrages associés se produisent au meilleur moment possible hello pour la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="2e09f-108">For SQL Server, this rescriction ensures that system updates and any associated restarts occur at hello best possible time for hello database.</span></span> <span data-ttu-id="2e09f-109">Mise à jour corrective automatisée dépend hello [Extension de l’Agent SQL Server IaaS](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="2e09f-109">Automated Patching depends on hello [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="2e09f-110">version classique de hello tooview de cet article, consultez [automatisée mise à jour corrective de SQL Server dans les Machines virtuelles Azure Classic](../classic/sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="2e09f-110">tooview hello classic version of this article, see [Automated Patching for SQL Server in Azure Virtual Machines Classic](../classic/sql-automated-patching.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2e09f-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="2e09f-111">Prerequisites</span></span>
<span data-ttu-id="2e09f-112">toouse automatisée de mise à jour corrective, envisagez de hello suivant des conditions préalables :</span><span class="sxs-lookup"><span data-stu-id="2e09f-112">toouse Automated Patching, consider hello following prerequisites:</span></span>

<span data-ttu-id="2e09f-113">**Système d’exploitation**:</span><span class="sxs-lookup"><span data-stu-id="2e09f-113">**Operating System**:</span></span>

* <span data-ttu-id="2e09f-114">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="2e09f-114">Windows Server 2012</span></span>
* <span data-ttu-id="2e09f-115">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="2e09f-115">Windows Server 2012 R2</span></span>
* <span data-ttu-id="2e09f-116">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="2e09f-116">Windows Server 2016</span></span>

<span data-ttu-id="2e09f-117">**Version de SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="2e09f-117">**SQL Server version**:</span></span>

* <span data-ttu-id="2e09f-118">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="2e09f-118">SQL Server 2012</span></span>
* <span data-ttu-id="2e09f-119">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="2e09f-119">SQL Server 2014</span></span>
* <span data-ttu-id="2e09f-120">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="2e09f-120">SQL Server 2016</span></span>

<span data-ttu-id="2e09f-121">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="2e09f-121">**Azure PowerShell**:</span></span>

* <span data-ttu-id="2e09f-122">[Installez les commandes Azure PowerShell dernière hello](/powershell/azure/overview) si vous envisagez de tooconfigure les correctifs automatiques avec PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2e09f-122">[Install hello latest Azure PowerShell commands](/powershell/azure/overview) if you plan tooconfigure Automated Patching with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="2e09f-123">Mise à jour corrective automatisée s’appuie sur hello Extension de l’Agent SQL Server IaaS.</span><span class="sxs-lookup"><span data-stu-id="2e09f-123">Automated Patching relies on hello SQL Server IaaS Agent Extension.</span></span> <span data-ttu-id="2e09f-124">Les images actuelles de la galerie de machines virtuelles SQL ajoutent cette extension par défaut.</span><span class="sxs-lookup"><span data-stu-id="2e09f-124">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="2e09f-125">Pour plus d’informations, consultez [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md)(Extension de l’agent IaaS SQL Server).</span><span class="sxs-lookup"><span data-stu-id="2e09f-125">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>
> 
> 

## <a name="settings"></a><span data-ttu-id="2e09f-126">Paramètres</span><span class="sxs-lookup"><span data-stu-id="2e09f-126">Settings</span></span>
<span data-ttu-id="2e09f-127">Hello tableau suivant décrit les options de hello qui peuvent être configurées pour les correctifs automatiques.</span><span class="sxs-lookup"><span data-stu-id="2e09f-127">hello following table describes hello options that can be configured for Automated Patching.</span></span> <span data-ttu-id="2e09f-128">étapes de configuration réelles Hello varient selon que vous utilisez hello portail Azure ou des commandes PowerShell de Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="2e09f-128">hello actual configuration steps vary depending on whether you use hello Azure portal or Azure Windows PowerShell commands.</span></span>

| <span data-ttu-id="2e09f-129">Paramètre</span><span class="sxs-lookup"><span data-stu-id="2e09f-129">Setting</span></span> | <span data-ttu-id="2e09f-130">Valeurs possibles</span><span class="sxs-lookup"><span data-stu-id="2e09f-130">Possible values</span></span> | <span data-ttu-id="2e09f-131">Description</span><span class="sxs-lookup"><span data-stu-id="2e09f-131">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2e09f-132">**Mise à jour corrective automatisée**</span><span class="sxs-lookup"><span data-stu-id="2e09f-132">**Automated Patching**</span></span> |<span data-ttu-id="2e09f-133">Activer/Désactiver (désactivé)</span><span class="sxs-lookup"><span data-stu-id="2e09f-133">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="2e09f-134">Active ou désactive la mise à jour corrective automatisée pour une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="2e09f-134">Enables or disables Automated Patching for an Azure virtual machine.</span></span> |
| <span data-ttu-id="2e09f-135">**Planification de la maintenance**</span><span class="sxs-lookup"><span data-stu-id="2e09f-135">**Maintenance schedule**</span></span> |<span data-ttu-id="2e09f-136">Tous les jours, lundi, mardi, mercredi, jeudi, vendredi, samedi et dimanche</span><span class="sxs-lookup"><span data-stu-id="2e09f-136">Everyday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday</span></span> |<span data-ttu-id="2e09f-137">planification de Hello pour télécharger et installer les mises à jour Windows et Microsoft SQL Server pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2e09f-137">hello schedule for downloading and installing Windows, SQL Server, and Microsoft updates for your virtual machine.</span></span> |
| <span data-ttu-id="2e09f-138">**Heure de début de la maintenance**</span><span class="sxs-lookup"><span data-stu-id="2e09f-138">**Maintenance start hour**</span></span> |<span data-ttu-id="2e09f-139">0-24</span><span class="sxs-lookup"><span data-stu-id="2e09f-139">0-24</span></span> |<span data-ttu-id="2e09f-140">Hello Démarrer local temps tooupdate hello l’ordinateur virtuel</span><span class="sxs-lookup"><span data-stu-id="2e09f-140">hello local start time tooupdate hello virtual machine.</span></span> |
| <span data-ttu-id="2e09f-141">**Durée de la fenêtre de maintenance**</span><span class="sxs-lookup"><span data-stu-id="2e09f-141">**Maintenance window duration**</span></span> |<span data-ttu-id="2e09f-142">30 à 180</span><span class="sxs-lookup"><span data-stu-id="2e09f-142">30-180</span></span> |<span data-ttu-id="2e09f-143">nombre de Hello de minutes autorisées toocomplete hello télécharger et installer les mises à jour.</span><span class="sxs-lookup"><span data-stu-id="2e09f-143">hello number of minutes permitted toocomplete hello download and installation of updates.</span></span> |
| <span data-ttu-id="2e09f-144">**Catégorie de correctif**</span><span class="sxs-lookup"><span data-stu-id="2e09f-144">**Patch Category**</span></span> |<span data-ttu-id="2e09f-145">Important</span><span class="sxs-lookup"><span data-stu-id="2e09f-145">Important</span></span> |<span data-ttu-id="2e09f-146">catégorie de Hello de toodownload de mises à jour et les installer.</span><span class="sxs-lookup"><span data-stu-id="2e09f-146">hello category of updates toodownload and install.</span></span> |

## <a name="configuration-in-hello-portal"></a><span data-ttu-id="2e09f-147">Configuration Bonjour portail</span><span class="sxs-lookup"><span data-stu-id="2e09f-147">Configuration in hello Portal</span></span>
<span data-ttu-id="2e09f-148">Vous pouvez utiliser hello tooconfigure portail Azure correctifs automatiques lors de la configuration ou pour des machines virtuelles existantes.</span><span class="sxs-lookup"><span data-stu-id="2e09f-148">You can use hello Azure portal tooconfigure Automated Patching during provisioning or for existing VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="2e09f-149">Nouvelles machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="2e09f-149">New VMs</span></span>
<span data-ttu-id="2e09f-150">Hello d’utilisation tooconfigure portail Azure lorsque vous créez une Machine virtuelle de nouveau SQL Server dans le modèle de déploiement du Gestionnaire de ressources hello les correctifs automatiques.</span><span class="sxs-lookup"><span data-stu-id="2e09f-150">Use hello Azure portal tooconfigure Automated Patching when you create a new SQL Server Virtual Machine in hello Resource Manager deployment model.</span></span>

<span data-ttu-id="2e09f-151">Bonjour **paramètres SQL Server** panneau, sélectionnez **mise à jour corrective automatisée**.</span><span class="sxs-lookup"><span data-stu-id="2e09f-151">In hello **SQL Server settings** blade, select **Automated patching**.</span></span> <span data-ttu-id="2e09f-152">Bonjour Azure portail montre hello **les correctifs automatiques SQL** panneau.</span><span class="sxs-lookup"><span data-stu-id="2e09f-152">hello following Azure portal screenshot shows hello **SQL Automated Patching** blade.</span></span>

![Mise à jour corrective automatisée SQL dans le portail Azure](./media/virtual-machines-windows-sql-automated-patching/azure-sql-arm-patching.png)

<span data-ttu-id="2e09f-154">Pour le contexte, consultez la rubrique complète de hello relative [approvisionner un ordinateur virtuel de SQL Server dans Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="2e09f-154">For context, see hello complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="2e09f-155">Machines virtuelles existantes</span><span class="sxs-lookup"><span data-stu-id="2e09f-155">Existing VMs</span></span>
<span data-ttu-id="2e09f-156">Pour les machines virtuelles SQL Server existantes, sélectionnez votre machine virtuelle SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2e09f-156">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="2e09f-157">Puis sélectionnez hello **configuration de SQL Server** section Hello **paramètres** panneau.</span><span class="sxs-lookup"><span data-stu-id="2e09f-157">Then select hello **SQL Server configuration** section of hello **Settings** blade.</span></span>

![Mise à jour corrective automatisée SQL pour les machines virtuelles existantes](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-existing-vms.png)

<span data-ttu-id="2e09f-159">Bonjour **configuration de SQL Server** panneau, cliquez sur hello **modifier** bouton Bonjour automatisée section mise à jour corrective.</span><span class="sxs-lookup"><span data-stu-id="2e09f-159">In hello **SQL Server configuration** blade, click hello **Edit** button in hello Automated patching section.</span></span>

![Configurer la mise à jour corrective automatisée SQL pour les machines virtuelles existantes](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-configuration.png)

<span data-ttu-id="2e09f-161">Lorsque vous avez terminé, cliquez sur hello **OK** bouton bas hello Hello **configuration de SQL Server** panneau toosave vos modifications.</span><span class="sxs-lookup"><span data-stu-id="2e09f-161">When finished, click hello **OK** button on hello bottom of hello **SQL Server configuration** blade toosave your changes.</span></span>

<span data-ttu-id="2e09f-162">Si vous activez les correctifs automatiques pour hello première fois, Azure configure hello Agent SQL Server IaaS en arrière-plan de hello.</span><span class="sxs-lookup"><span data-stu-id="2e09f-162">If you are enabling Automated Patching for hello first time, Azure configures hello SQL Server IaaS Agent in hello background.</span></span> <span data-ttu-id="2e09f-163">Pendant ce temps, hello portail Azure peut ne pas affiche que les correctifs automatiques est configuré.</span><span class="sxs-lookup"><span data-stu-id="2e09f-163">During this time, hello Azure portal might not show that Automated Patching is configured.</span></span> <span data-ttu-id="2e09f-164">Attendez quelques minutes pour hello toobe de l’agent installé, configuré.</span><span class="sxs-lookup"><span data-stu-id="2e09f-164">Wait several minutes for hello agent toobe installed, configured.</span></span> <span data-ttu-id="2e09f-165">Après que Azure hello portail reflète les nouveaux paramètres de hello.</span><span class="sxs-lookup"><span data-stu-id="2e09f-165">After that hello Azure portal reflects hello new settings.</span></span>

> [!NOTE]
> <span data-ttu-id="2e09f-166">Vous pouvez également configurer la mise à jour corrective automatisée à l’aide d’un modèle.</span><span class="sxs-lookup"><span data-stu-id="2e09f-166">You can also configure Automated Patching using a template.</span></span> <span data-ttu-id="2e09f-167">Pour plus d’informations, consultez l’article [Azure quickstart template for Automated Patching](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autopatching-update)(Modèle de démarrage rapide d’Azure pour la mise à jour corrective automatisée).</span><span class="sxs-lookup"><span data-stu-id="2e09f-167">For more information, see [Azure quickstart template for Automated Patching](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autopatching-update).</span></span>
> 
> 

## <a name="configuration-with-powershell"></a><span data-ttu-id="2e09f-168">Configuration avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="2e09f-168">Configuration with PowerShell</span></span>
<span data-ttu-id="2e09f-169">Après avoir déployé votre VM SQL, utilisez PowerShell tooconfigure correctifs automatiques.</span><span class="sxs-lookup"><span data-stu-id="2e09f-169">After provisioning your SQL VM, use PowerShell tooconfigure Automated Patching.</span></span>

<span data-ttu-id="2e09f-170">Dans l’exemple suivant de hello, PowerShell est utilisé tooconfigure correctifs automatiques sur une machine virtuelle de serveur SQL existant.</span><span class="sxs-lookup"><span data-stu-id="2e09f-170">In hello following example, PowerShell is used tooconfigure Automated Patching on an existing SQL Server VM.</span></span> <span data-ttu-id="2e09f-171">Hello **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig** commande configure une nouvelle fenêtre de maintenance pour les mises à jour automatiques.</span><span class="sxs-lookup"><span data-stu-id="2e09f-171">hello **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig** command configures a new maintenance window for automatic updates.</span></span>

    $vmname = "vmname"
    $resourcegroupname = "resourcegroupname"
    $aps = AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Set-AzureRmVMSqlServerExtension -AutoPatchingSettings $aps -VMName $vmname -ResourceGroupName $resourcegroupname

<span data-ttu-id="2e09f-172">En fonction de cet exemple, hello tableau suivant décrit les effets pratiques de hello sur la machine virtuelle Azure cible de hello :</span><span class="sxs-lookup"><span data-stu-id="2e09f-172">Based on this example, hello following table describes hello practical effect on hello target Azure VM:</span></span>

| <span data-ttu-id="2e09f-173">Paramètre</span><span class="sxs-lookup"><span data-stu-id="2e09f-173">Parameter</span></span> | <span data-ttu-id="2e09f-174">Résultat</span><span class="sxs-lookup"><span data-stu-id="2e09f-174">Effect</span></span> |
| --- | --- |
| <span data-ttu-id="2e09f-175">**DayOfWeek**</span><span class="sxs-lookup"><span data-stu-id="2e09f-175">**DayOfWeek**</span></span> |<span data-ttu-id="2e09f-176">Les correctifs sont installés tous les jeudis.</span><span class="sxs-lookup"><span data-stu-id="2e09f-176">Patches installed every Thursday.</span></span> |
| <span data-ttu-id="2e09f-177">**MaintenanceWindowStartingHour**</span><span class="sxs-lookup"><span data-stu-id="2e09f-177">**MaintenanceWindowStartingHour**</span></span> |<span data-ttu-id="2e09f-178">Les mises à jour démarrent à 11 h 00.</span><span class="sxs-lookup"><span data-stu-id="2e09f-178">Begin updates at 11:00am.</span></span> |
| <span data-ttu-id="2e09f-179">**MaintenanceWindowsDuration**</span><span class="sxs-lookup"><span data-stu-id="2e09f-179">**MaintenanceWindowsDuration**</span></span> |<span data-ttu-id="2e09f-180">Les correctifs doivent être installés dans les 120 minutes.</span><span class="sxs-lookup"><span data-stu-id="2e09f-180">Patches must be installed within 120 minutes.</span></span> <span data-ttu-id="2e09f-181">Selon l’heure de début hello, ils doivent effectuer par 1:00 pm.</span><span class="sxs-lookup"><span data-stu-id="2e09f-181">Based on hello start time, they must complete by 1:00pm.</span></span> |
| <span data-ttu-id="2e09f-182">**PatchCategory**</span><span class="sxs-lookup"><span data-stu-id="2e09f-182">**PatchCategory**</span></span> |<span data-ttu-id="2e09f-183">Hello seul réglage possible pour ce paramètre est **Important**.</span><span class="sxs-lookup"><span data-stu-id="2e09f-183">hello only possible setting for this parameter is **Important**.</span></span> |

<span data-ttu-id="2e09f-184">Il peut prendre plusieurs minutes tooinstall et configurer hello IaaS Agent SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2e09f-184">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span>

<span data-ttu-id="2e09f-185">toodisable correctifs automatiques, exécution hello même script sans hello **-activer** paramètre toohello **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig**.</span><span class="sxs-lookup"><span data-stu-id="2e09f-185">toodisable Automated Patching, run hello same script without hello **-Enable** parameter toohello **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig**.</span></span> <span data-ttu-id="2e09f-186">Hello absence de hello **-activer** fonctionnalité de paramètre signaux hello commande toodisable hello.</span><span class="sxs-lookup"><span data-stu-id="2e09f-186">hello absence of hello **-Enable** parameter signals hello command toodisable hello feature.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e09f-187">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2e09f-187">Next steps</span></span>
<span data-ttu-id="2e09f-188">Pour plus d’informations sur les autres tâches d’automatisation disponibles, voir [Extension de l’agent IaaS SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="2e09f-188">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="2e09f-189">Pour plus d’informations sur l’exécution de SQL Server sur des machines virtuelles Azure, voir [Vue d’ensemble de SQL Server sur les machines virtuelles Azure](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2e09f-189">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

