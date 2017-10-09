---
title: "aaaAutomate des tâches de gestion sur des machines virtuelles de SQL (classiques) | Documents Microsoft"
description: "Cette rubrique décrit comment toomanage hello extension de l’agent SQL Server, qui automatise les tâches d’administration SQL Server spécifiques. Celles-ci incluent Sauvegarde automatisée, Mise à jour corrective automatisée et Azure Key Vault Integration. Cette rubrique utilise le mode de déploiement classique hello."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a9bda2e7-cdba-427c-bc30-77cde4376f3a
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a1dc011e0526845701eaf0c365007938f9ee32ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-hello-sql-server-agent-extension-classic"></a><span data-ttu-id="ae70d-105">Automatiser les tâches de gestion sur des Machines virtuelles Azure avec hello Extension de l’Agent SQL Server (classique)</span><span class="sxs-lookup"><span data-stu-id="ae70d-105">Automate management tasks on Azure Virtual Machines with hello SQL Server Agent Extension (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ae70d-106">Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="ae70d-106">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-server-agent-extension.md)
> * [<span data-ttu-id="ae70d-107">Classique</span><span class="sxs-lookup"><span data-stu-id="ae70d-107">Classic</span></span>](../classic/sql-server-agent-extension.md)
> 
>
 
<span data-ttu-id="ae70d-108">Hello, Extension de l’Agent SQL Server IaaS (sqliaasagent n’est) s’exécute sur les machines virtuelles tooautomate les tâches d’administration.</span><span class="sxs-lookup"><span data-stu-id="ae70d-108">hello SQL Server IaaS Agent Extension (SQLIaaSAgent) runs on Azure virtual machines tooautomate administration tasks.</span></span> <span data-ttu-id="ae70d-109">Cette rubrique fournit une vue d’ensemble des services hello pris en charge par l’extension de hello ainsi que des instructions pour l’installation, l’état et la suppression.</span><span class="sxs-lookup"><span data-stu-id="ae70d-109">This topic provides an overview of hello services supported by hello extension as well as instructions for installation, status, and removal.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="ae70d-110">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ae70d-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ae70d-111">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="ae70d-111">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="ae70d-112">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="ae70d-112">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="ae70d-113">version de gestionnaire de ressources hello tooview de cet article, consultez [Extension de l’Agent SQL Server pour SQL Server machines virtuelles Resource Manager](../sql/virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="ae70d-113">tooview hello Resource Manager version of this article, see [SQL Server Agent Extension for SQL Server VMs Resource Manager](../sql/virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="supported-services"></a><span data-ttu-id="ae70d-114">Services pris en charge</span><span class="sxs-lookup"><span data-stu-id="ae70d-114">Supported services</span></span>
<span data-ttu-id="ae70d-115">Hello Extension de l’Agent IaaS SQL Server prend en charge hello tâches d’administration suivantes :</span><span class="sxs-lookup"><span data-stu-id="ae70d-115">hello SQL Server IaaS Agent Extension supports hello following administration tasks:</span></span>

| <span data-ttu-id="ae70d-116">Fonction d’administration</span><span class="sxs-lookup"><span data-stu-id="ae70d-116">Administration feature</span></span> | <span data-ttu-id="ae70d-117">Description</span><span class="sxs-lookup"><span data-stu-id="ae70d-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ae70d-118">**Sauvegarde automatisée SQL**</span><span class="sxs-lookup"><span data-stu-id="ae70d-118">**SQL Automated Backup**</span></span> |<span data-ttu-id="ae70d-119">Automatise hello planification des sauvegardes pour toutes les bases de données hello instance par défaut de SQL Server dans hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ae70d-119">Automates hello scheduling of backups for all databases for hello default instance of SQL Server in hello VM.</span></span> <span data-ttu-id="ae70d-120">Pour plus d’informations, consultez [Sauvegarde automatisée pour SQL Server dans les machines virtuelles Azure (Classic)](../classic/sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="ae70d-120">For more information, see [Automated backup for SQL Server in Azure Virtual Machines (Classic)](../classic/sql-automated-backup.md).</span></span> |
| <span data-ttu-id="ae70d-121">**Mise à jour corrective automatisée SQL**</span><span class="sxs-lookup"><span data-stu-id="ae70d-121">**SQL Automated Patching**</span></span> |<span data-ttu-id="ae70d-122">Configure une fenêtre de maintenance pendant les mises à jour tooyour machine virtuelle peut prendre place de, vous pouvez ainsi éviter les mises à jour pendant les pics de charge de travail.</span><span class="sxs-lookup"><span data-stu-id="ae70d-122">Configures a maintenance window during which updates tooyour VM can take place, so  you can avoid updates during peak times for your workload.</span></span> <span data-ttu-id="ae70d-123">Pour plus d’informations, consultez [Mise à jour corrective automatisée pour SQL Server dans les machines virtuelles Azure (Classic)](../classic/sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="ae70d-123">For more information, see [Automated patching for SQL Server in Azure Virtual Machines (Classic)](../classic/sql-automated-patching.md).</span></span> |
| <span data-ttu-id="ae70d-124">**Intégration du coffre de clés Azure**</span><span class="sxs-lookup"><span data-stu-id="ae70d-124">**Azure Key Vault Integration**</span></span> |<span data-ttu-id="ae70d-125">Permet de vous tooautomatically installer et configurer le coffre de clés Azure sur votre machine virtuelle SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ae70d-125">Enables you tooautomatically install and configure Azure Key Vault on your SQL Server VM.</span></span> <span data-ttu-id="ae70d-126">Pour plus d’informations, consultez [Configurer Azure Key Vault Integration (Intégration du coffre de clés Azure) pour SQL Server sur des machines virtuelles Azure (Classic)](../classic/ps-sql-keyvault.md).</span><span class="sxs-lookup"><span data-stu-id="ae70d-126">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs (Classic)](../classic/ps-sql-keyvault.md).</span></span> |

## <a name="prerequisites"></a><span data-ttu-id="ae70d-127">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ae70d-127">Prerequisites</span></span>
<span data-ttu-id="ae70d-128">Configuration requise hello de toouse Extension de l’Agent SQL Server IaaS sur votre machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="ae70d-128">Requirements toouse hello SQL Server IaaS Agent Extension on your VM:</span></span>

### <a name="operating-system"></a><span data-ttu-id="ae70d-129">Système d’exploitation :</span><span class="sxs-lookup"><span data-stu-id="ae70d-129">Operating System:</span></span>
* <span data-ttu-id="ae70d-130">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="ae70d-130">Windows Server 2012</span></span>
* <span data-ttu-id="ae70d-131">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="ae70d-131">Windows Server 2012 R2</span></span>
* <span data-ttu-id="ae70d-132">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="ae70d-132">Windows Server 2016</span></span>

### <a name="sql-server-versions"></a><span data-ttu-id="ae70d-133">Versions de SQL Server :</span><span class="sxs-lookup"><span data-stu-id="ae70d-133">SQL Server versions:</span></span>
* <span data-ttu-id="ae70d-134">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="ae70d-134">SQL Server 2012</span></span>
* <span data-ttu-id="ae70d-135">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="ae70d-135">SQL Server 2014</span></span>
* <span data-ttu-id="ae70d-136">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="ae70d-136">SQL Server 2016</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="ae70d-137">Azure PowerShell :</span><span class="sxs-lookup"><span data-stu-id="ae70d-137">Azure PowerShell:</span></span>
<span data-ttu-id="ae70d-138">[Télécharger et configurer les commandes Azure PowerShell dernière hello](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ae70d-138">[Download and configure hello latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="ae70d-139">Démarrez Windows PowerShell et le connecter tooyour abonnement Azure avec hello **Add-AzureAccount** commande.</span><span class="sxs-lookup"><span data-stu-id="ae70d-139">Start Windows PowerShell, and connect it tooyour Azure subscription with hello **Add-AzureAccount** command.</span></span>

    Add-AzureAccount

<span data-ttu-id="ae70d-140">Si vous avez plusieurs abonnements, utilisez **Select-AzureSubscription** abonnement hello tooselect qui contient la cible de machine virtuelle classique.</span><span class="sxs-lookup"><span data-stu-id="ae70d-140">If you have multiple subscriptions, use **Select-AzureSubscription** tooselect hello subscription that contains your target classic VM.</span></span>

    Select-AzureSubscription -SubscriptionName <subscriptionname>

<span data-ttu-id="ae70d-141">À ce stade, vous pouvez obtenir une liste de machines virtuelles classiques de hello et leurs noms de service associé avec hello **Get-AzureVM** commande.</span><span class="sxs-lookup"><span data-stu-id="ae70d-141">At this point, you can get a list of hello classic virtual machines and their associated service names with hello **Get-AzureVM** command.</span></span>

    Get-AzureVM

## <a name="installation"></a><span data-ttu-id="ae70d-142">Installation</span><span class="sxs-lookup"><span data-stu-id="ae70d-142">Installation</span></span>
<span data-ttu-id="ae70d-143">Pour les machines virtuelles classiques, vous devez utiliser PowerShell tooinstall hello Extension de l’Agent IaaS SQL Server et configurer ses services associés.</span><span class="sxs-lookup"><span data-stu-id="ae70d-143">For classic VMs, you must use PowerShell tooinstall hello SQL Server IaaS Agent Extension and configure its associated services.</span></span> <span data-ttu-id="ae70d-144">Hello d’utilisation **Set-AzureVMSqlServerExtension** extension de hello tooinstall PowerShell applet de commande.</span><span class="sxs-lookup"><span data-stu-id="ae70d-144">Use hello **Set-AzureVMSqlServerExtension** PowerShell cmdlet tooinstall hello extension.</span></span> <span data-ttu-id="ae70d-145">Par exemple, hello de commande suivante installe l’extension de hello sur une machine virtuelle (classique) de Windows Server et le nomme « SQLIaaSExtension ».</span><span class="sxs-lookup"><span data-stu-id="ae70d-145">For example, hello following command installs hello extension on a Windows Server VM (classic) and names it "SQLIaaSExtension".</span></span>

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -ReferenceName "SQLIaasExtension" -Version "1.2" | Update-AzureVM

<span data-ttu-id="ae70d-146">Si vous mettez à jour plus récent toohello hello Extension de l’Agent IaaS SQL, vous devez redémarrer votre machine virtuelle après la mise à jour hello extension.</span><span class="sxs-lookup"><span data-stu-id="ae70d-146">If you update toohello latest version of hello SQL IaaS Agent Extension, you must restart your virtual machine after updating hello extension.</span></span>

> [!NOTE]
> <span data-ttu-id="ae70d-147">Machines virtuelles classiques ne pas avoir un tooinstall option et configurer hello Extension de l’Agent IaaS SQL via le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="ae70d-147">Classic virtual machines do not have an option tooinstall and configure hello SQL IaaS Agent Extension through hello portal.</span></span>
> 
> 

## <a name="status"></a><span data-ttu-id="ae70d-148">État</span><span class="sxs-lookup"><span data-stu-id="ae70d-148">Status</span></span>
<span data-ttu-id="ae70d-149">Une façon tooverify que hello extension est installée est état de l’agent tooview hello Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ae70d-149">One way tooverify that hello extension is installed is tooview hello agent status in hello Azure Portal.</span></span> <span data-ttu-id="ae70d-150">Sélectionnez une machine virtuelle répertoriée dans le panneau de machine virtuelle hello, puis sur **Extensions**.</span><span class="sxs-lookup"><span data-stu-id="ae70d-150">Select a virtual machine listed in hello virtual machine blade, and then click on **Extensions**.</span></span> <span data-ttu-id="ae70d-151">Vous devez voir hello **sqliaasagent n’est** extension répertoriée.</span><span class="sxs-lookup"><span data-stu-id="ae70d-151">You should see hello **SQLIaaSAgent** extension listed.</span></span>

![Extension Agent IaaS SQL Server dans le portail Azure](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-portal.png)

<span data-ttu-id="ae70d-153">Vous pouvez également utiliser hello **Get-AzureVMSqlServerExtension** applet de commande Powershell de Azure.</span><span class="sxs-lookup"><span data-stu-id="ae70d-153">You can also use hello **Get-AzureVMSqlServerExtension** Azure Powershell cmdlet.</span></span>

    Get-AzureVM –ServiceName "service" –Name "vmname" | Get-AzureVMSqlServerExtension

## <a name="removal"></a><span data-ttu-id="ae70d-154">Suppression</span><span class="sxs-lookup"><span data-stu-id="ae70d-154">Removal</span></span>
<span data-ttu-id="ae70d-155">Bonjour portail Azure, vous pouvez désinstaller l’extension de hello en cliquant sur les points de suspension hello hello **Extensions** Panneau de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ae70d-155">In hello Azure Portal, you can uninstall hello extension by clicking hello ellipsis on hello **Extensions** blade of your virtual machine properties.</span></span> <span data-ttu-id="ae70d-156">Cliquez ensuite sur **Désinstaller**.</span><span class="sxs-lookup"><span data-stu-id="ae70d-156">Then click **Uninstall**.</span></span>

![Désinstaller hello Extension de l’Agent SQL Server IaaS dans le portail Azure](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-uninstall.png)

<span data-ttu-id="ae70d-158">Vous pouvez également utiliser hello **Remove-AzureVMSqlServerExtension** applet de commande Powershell.</span><span class="sxs-lookup"><span data-stu-id="ae70d-158">You can also use hello **Remove-AzureVMSqlServerExtension** Powershell cmdlet.</span></span>

    Get-AzureVM –ServiceName "service" –Name "vmname" | Remove-AzureVMSqlServerExtension | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="ae70d-159">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ae70d-159">Next Steps</span></span>
<span data-ttu-id="ae70d-160">Commencer à utiliser un des services hello pris en charge par l’extension de hello.</span><span class="sxs-lookup"><span data-stu-id="ae70d-160">Begin using one of hello services supported by hello extension.</span></span> <span data-ttu-id="ae70d-161">Pour plus d’informations, consultez les rubriques de hello référencées Bonjour [prise en charge des services](#supported-services) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="ae70d-161">For more details, see hello topics referenced in hello [Supported services](#supported-services) section of this article.</span></span>

<span data-ttu-id="ae70d-162">Pour plus d’informations sur l’exécution de SQL Server sur des machines virtuelles Azure, voir [SQL Server sur les machines virtuelles Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ae70d-162">For more information about running SQL Server on Azure Virtual Machines, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

