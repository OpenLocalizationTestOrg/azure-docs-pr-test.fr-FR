---
title: "aaaAutomated mise à jour corrective pour les machines virtuelles (classiques) de SQL Server | Documents Microsoft"
description: "Explique les fonctionnalité de correctifs automatiques hello pour les Machines virtuelles SQL Server s’exécutant dans Azure à l’aide du mode de déploiement classique de hello."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 737b2f65-08b9-4f54-b867-e987730265a8
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 2ef06b95705fc457605d6eb2fbc0afd490321843
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-classic"></a><span data-ttu-id="d1c48-103">Mise à jour corrective automatisée pour SQL Server dans les machines virtuelles Azure (classiques)</span><span class="sxs-lookup"><span data-stu-id="d1c48-103">Automated Patching for SQL Server in Azure Virtual Machines (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d1c48-104">Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="d1c48-104">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-automated-patching.md)
> * [<span data-ttu-id="d1c48-105">Classique</span><span class="sxs-lookup"><span data-stu-id="d1c48-105">Classic</span></span>](../classic/sql-automated-patching.md)
> 
> 

<span data-ttu-id="d1c48-106">La mise à jour corrective automatisée établit une fenêtre de maintenance pour une machine virtuelle Azure exécutant SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d1c48-106">Automated Patching establishes a maintenance window for an Azure Virtual Machine running SQL Server.</span></span> <span data-ttu-id="d1c48-107">Les mises à jour automatisées ne peuvent être installées qu’au cours de cette fenêtre de maintenance.</span><span class="sxs-lookup"><span data-stu-id="d1c48-107">Automated Updates can only be installed during this maintenance window.</span></span> <span data-ttu-id="d1c48-108">Pour SQL Server, ainsi que les mises à jour système et les éventuels redémarrages associés se produisent au meilleur moment possible hello pour la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="d1c48-108">For SQL Server, this ensures that system updates and any associated restarts occur at hello best possible time for hello database.</span></span> <span data-ttu-id="d1c48-109">Mise à jour corrective automatisée dépend hello [Extension de l’Agent SQL Server IaaS](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="d1c48-109">Automated Patching depends on hello [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="d1c48-110">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d1c48-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d1c48-111">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="d1c48-111">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="d1c48-112">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="d1c48-112">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="d1c48-113">version de gestionnaire de ressources hello tooview de cet article, consultez [les correctifs automatiques pour SQL Server dans le Gestionnaire de ressources de Machines virtuelles Azure](../sql/virtual-machines-windows-sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="d1c48-113">tooview hello Resource Manager version of this article, see [Automated Patching for SQL Server in Azure Virtual Machines Resource Manager](../sql/virtual-machines-windows-sql-automated-patching.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d1c48-114">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d1c48-114">Prerequisites</span></span>
<span data-ttu-id="d1c48-115">toouse automatisée de mise à jour corrective, envisagez de hello suivant des conditions préalables :</span><span class="sxs-lookup"><span data-stu-id="d1c48-115">toouse Automated Patching, consider hello following prerequisites:</span></span>

<span data-ttu-id="d1c48-116">**Système d’exploitation**:</span><span class="sxs-lookup"><span data-stu-id="d1c48-116">**Operating System**:</span></span>

* <span data-ttu-id="d1c48-117">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="d1c48-117">Windows Server 2012</span></span>
* <span data-ttu-id="d1c48-118">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="d1c48-118">Windows Server 2012 R2</span></span>
* <span data-ttu-id="d1c48-119">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="d1c48-119">Windows Server 2016</span></span>

<span data-ttu-id="d1c48-120">**Version de SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="d1c48-120">**SQL Server version**:</span></span>

* <span data-ttu-id="d1c48-121">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="d1c48-121">SQL Server 2012</span></span>
* <span data-ttu-id="d1c48-122">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="d1c48-122">SQL Server 2014</span></span>
* <span data-ttu-id="d1c48-123">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="d1c48-123">SQL Server 2016</span></span>

<span data-ttu-id="d1c48-124">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="d1c48-124">**Azure PowerShell**:</span></span>

* <span data-ttu-id="d1c48-125">[Installez les commandes Azure PowerShell dernière hello](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d1c48-125">[Install hello latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="d1c48-126">**Extension IaaS SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="d1c48-126">**SQL Server IaaS Extension**:</span></span>

* <span data-ttu-id="d1c48-127">[Installer l’IaaS Extension de SQL Server de hello](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="d1c48-127">[Install hello SQL Server IaaS Extension](../classic/sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="d1c48-128">Paramètres</span><span class="sxs-lookup"><span data-stu-id="d1c48-128">Settings</span></span>
<span data-ttu-id="d1c48-129">Hello tableau suivant décrit les options de hello qui peuvent être configurées pour les correctifs automatiques.</span><span class="sxs-lookup"><span data-stu-id="d1c48-129">hello following table describes hello options that can be configured for Automated Patching.</span></span> <span data-ttu-id="d1c48-130">Pour les machines virtuelles classiques, vous devez utiliser PowerShell tooconfigure ces paramètres.</span><span class="sxs-lookup"><span data-stu-id="d1c48-130">For classic VMs, you must use PowerShell tooconfigure these settings.</span></span>

| <span data-ttu-id="d1c48-131">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d1c48-131">Setting</span></span> | <span data-ttu-id="d1c48-132">Valeurs possibles</span><span class="sxs-lookup"><span data-stu-id="d1c48-132">Possible values</span></span> | <span data-ttu-id="d1c48-133">Description</span><span class="sxs-lookup"><span data-stu-id="d1c48-133">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d1c48-134">**Mise à jour corrective automatisée**</span><span class="sxs-lookup"><span data-stu-id="d1c48-134">**Automated Patching**</span></span> |<span data-ttu-id="d1c48-135">Activer/Désactiver (désactivé)</span><span class="sxs-lookup"><span data-stu-id="d1c48-135">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="d1c48-136">Active ou désactive la mise à jour corrective automatisée pour une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="d1c48-136">Enables or disables Automated Patching for an Azure virtual machine.</span></span> |
| <span data-ttu-id="d1c48-137">**Planification de la maintenance**</span><span class="sxs-lookup"><span data-stu-id="d1c48-137">**Maintenance schedule**</span></span> |<span data-ttu-id="d1c48-138">Tous les jours, lundi, mardi, mercredi, jeudi, vendredi, samedi et dimanche</span><span class="sxs-lookup"><span data-stu-id="d1c48-138">Everyday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday</span></span> |<span data-ttu-id="d1c48-139">planification de Hello pour télécharger et installer les mises à jour Windows et Microsoft SQL Server pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d1c48-139">hello schedule for downloading and installing Windows, SQL Server, and Microsoft updates for your virtual machine.</span></span> |
| <span data-ttu-id="d1c48-140">**Heure de début de la maintenance**</span><span class="sxs-lookup"><span data-stu-id="d1c48-140">**Maintenance start hour**</span></span> |<span data-ttu-id="d1c48-141">0-24</span><span class="sxs-lookup"><span data-stu-id="d1c48-141">0-24</span></span> |<span data-ttu-id="d1c48-142">Hello Démarrer local temps tooupdate hello l’ordinateur virtuel</span><span class="sxs-lookup"><span data-stu-id="d1c48-142">hello local start time tooupdate hello virtual machine.</span></span> |
| <span data-ttu-id="d1c48-143">**Durée de la fenêtre de maintenance**</span><span class="sxs-lookup"><span data-stu-id="d1c48-143">**Maintenance window duration**</span></span> |<span data-ttu-id="d1c48-144">30 à 180</span><span class="sxs-lookup"><span data-stu-id="d1c48-144">30-180</span></span> |<span data-ttu-id="d1c48-145">nombre de Hello de minutes autorisées toocomplete hello télécharger et installer les mises à jour.</span><span class="sxs-lookup"><span data-stu-id="d1c48-145">hello number of minutes permitted toocomplete hello download and installation of updates.</span></span> |
| <span data-ttu-id="d1c48-146">**Catégorie de correctif**</span><span class="sxs-lookup"><span data-stu-id="d1c48-146">**Patch Category**</span></span> |<span data-ttu-id="d1c48-147">Important</span><span class="sxs-lookup"><span data-stu-id="d1c48-147">Important</span></span> |<span data-ttu-id="d1c48-148">catégorie de Hello de toodownload de mises à jour et les installer.</span><span class="sxs-lookup"><span data-stu-id="d1c48-148">hello category of updates toodownload and install.</span></span> |

## <a name="configuration-with-powershell"></a><span data-ttu-id="d1c48-149">Configuration avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="d1c48-149">Configuration with PowerShell</span></span>
<span data-ttu-id="d1c48-150">Dans l’exemple suivant de hello, PowerShell est utilisé tooconfigure correctifs automatiques sur une machine virtuelle de serveur SQL existant.</span><span class="sxs-lookup"><span data-stu-id="d1c48-150">In hello following example, PowerShell is used tooconfigure Automated Patching on an existing SQL Server VM.</span></span> <span data-ttu-id="d1c48-151">Hello **New-AzureVMSqlServerAutoPatchingConfig** commande configure une nouvelle fenêtre de maintenance pour les mises à jour automatiques.</span><span class="sxs-lookup"><span data-stu-id="d1c48-151">hello **New-AzureVMSqlServerAutoPatchingConfig** command configures a new maintenance window for automatic updates.</span></span>

    $aps = New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoPatchingSettings $aps | Update-AzureVM

<span data-ttu-id="d1c48-152">En fonction de cet exemple, hello tableau suivant décrit les effets pratiques de hello sur la machine virtuelle Azure cible de hello :</span><span class="sxs-lookup"><span data-stu-id="d1c48-152">Based on this example, hello following table describes hello practical effect on hello target Azure VM:</span></span>

| <span data-ttu-id="d1c48-153">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d1c48-153">Parameter</span></span> | <span data-ttu-id="d1c48-154">Résultat</span><span class="sxs-lookup"><span data-stu-id="d1c48-154">Effect</span></span> |
| --- | --- |
| <span data-ttu-id="d1c48-155">**DayOfWeek**</span><span class="sxs-lookup"><span data-stu-id="d1c48-155">**DayOfWeek**</span></span> |<span data-ttu-id="d1c48-156">Les correctifs sont installés tous les jeudis.</span><span class="sxs-lookup"><span data-stu-id="d1c48-156">Patches installed every Thursday.</span></span> |
| <span data-ttu-id="d1c48-157">**MaintenanceWindowStartingHour**</span><span class="sxs-lookup"><span data-stu-id="d1c48-157">**MaintenanceWindowStartingHour**</span></span> |<span data-ttu-id="d1c48-158">Les mises à jour démarrent à 11 h 00.</span><span class="sxs-lookup"><span data-stu-id="d1c48-158">Begin updates at 11:00am.</span></span> |
| <span data-ttu-id="d1c48-159">**MaintenanceWindowsDuration**</span><span class="sxs-lookup"><span data-stu-id="d1c48-159">**MaintenanceWindowsDuration**</span></span> |<span data-ttu-id="d1c48-160">Les correctifs doivent être installés dans les 120 minutes.</span><span class="sxs-lookup"><span data-stu-id="d1c48-160">Patches must be installed within 120 minutes.</span></span> <span data-ttu-id="d1c48-161">Selon l’heure de début hello, ils doivent effectuer par 1:00 pm.</span><span class="sxs-lookup"><span data-stu-id="d1c48-161">Based on hello start time, they must complete by 1:00pm.</span></span> |
| <span data-ttu-id="d1c48-162">**PatchCategory**</span><span class="sxs-lookup"><span data-stu-id="d1c48-162">**PatchCategory**</span></span> |<span data-ttu-id="d1c48-163">Hello uniquement possibles pour ce paramètre est « Important ».</span><span class="sxs-lookup"><span data-stu-id="d1c48-163">hello only possible setting for this parameter is “Important”.</span></span> |

<span data-ttu-id="d1c48-164">Il peut prendre plusieurs minutes tooinstall et configurer hello IaaS Agent SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d1c48-164">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span>

<span data-ttu-id="d1c48-165">toodisable correctifs automatiques, exécution hello même script sans hello - Enable paramètre toohello New-AzureVMSqlServerAutoPatchingConfig.</span><span class="sxs-lookup"><span data-stu-id="d1c48-165">toodisable Automated Patching, run hello same script without hello -Enable parameter toohello New-AzureVMSqlServerAutoPatchingConfig.</span></span> <span data-ttu-id="d1c48-166">Comme avec l’installation, il peut prendre plusieurs minutes toodisable correctifs automatiques.</span><span class="sxs-lookup"><span data-stu-id="d1c48-166">As with installation, it can take several minutes toodisable Automated Patching.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1c48-167">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d1c48-167">Next steps</span></span>
<span data-ttu-id="d1c48-168">Pour plus d’informations sur les autres tâches d’automatisation disponibles, voir [Extension de l’agent IaaS SQL Server](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="d1c48-168">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

<span data-ttu-id="d1c48-169">Pour plus d’informations sur l’exécution de SQL Server sur des machines virtuelles Azure, voir [Vue d’ensemble de SQL Server sur les machines virtuelles Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d1c48-169">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

