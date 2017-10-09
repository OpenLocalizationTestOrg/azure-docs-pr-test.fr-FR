---
title: "aaaAutomate des tâches de gestion sur des machines virtuelles de SQL (Resource Manager) | Documents Microsoft"
description: "Cette rubrique décrit comment toomanage hello extension de l’agent SQL Server, qui automatise les tâches d’administration SQL Server spécifiques. Celles-ci incluent Sauvegarde automatisée, Mise à jour corrective automatisée et Azure Key Vault Integration. Cette rubrique utilise le mode de déploiement du Gestionnaire de ressources hello."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: effe4e2f-35b5-490a-b5ef-b06746083da4
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ae917612c4af59f12c0b083440673bdc555e9d56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-hello-sql-server-agent-extension-resource-manager"></a><span data-ttu-id="51b80-105">Automatiser les tâches de gestion sur des Machines virtuelles Azure avec hello Extension de l’Agent SQL Server (Gestionnaire de ressources)</span><span class="sxs-lookup"><span data-stu-id="51b80-105">Automate management tasks on Azure Virtual Machines with hello SQL Server Agent Extension (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="51b80-106">Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="51b80-106">Resource Manager</span></span>](virtual-machines-windows-sql-server-agent-extension.md)
> * [<span data-ttu-id="51b80-107">Classique</span><span class="sxs-lookup"><span data-stu-id="51b80-107">Classic</span></span>](../classic/sql-server-agent-extension.md)
> 
> 

<span data-ttu-id="51b80-108">Hello, Extension de l’Agent SQL Server IaaS (SQLIaaSExtension) s’exécute sur les machines virtuelles tooautomate les tâches d’administration.</span><span class="sxs-lookup"><span data-stu-id="51b80-108">hello SQL Server IaaS Agent Extension (SQLIaaSExtension) runs on Azure virtual machines tooautomate administration tasks.</span></span> <span data-ttu-id="51b80-109">Cette rubrique fournit une vue d’ensemble des services hello pris en charge par l’extension de hello ainsi que des instructions pour l’installation, l’état et la suppression.</span><span class="sxs-lookup"><span data-stu-id="51b80-109">This topic provides an overview of hello services supported by hello extension as well as instructions for installation, status, and removal.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="51b80-110">version classique de hello tooview de cet article, consultez [Extension de l’Agent SQL Server pour SQL Server machines virtuelles Classic](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="51b80-110">tooview hello classic version of this article, see [SQL Server Agent Extension for SQL Server VMs Classic](../classic/sql-server-agent-extension.md).</span></span>

## <a name="supported-services"></a><span data-ttu-id="51b80-111">Services pris en charge</span><span class="sxs-lookup"><span data-stu-id="51b80-111">Supported services</span></span>
<span data-ttu-id="51b80-112">Hello Extension de l’Agent IaaS SQL Server prend en charge hello tâches d’administration suivantes :</span><span class="sxs-lookup"><span data-stu-id="51b80-112">hello SQL Server IaaS Agent Extension supports hello following administration tasks:</span></span>

| <span data-ttu-id="51b80-113">Fonction d’administration</span><span class="sxs-lookup"><span data-stu-id="51b80-113">Administration feature</span></span> | <span data-ttu-id="51b80-114">Description</span><span class="sxs-lookup"><span data-stu-id="51b80-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="51b80-115">**Sauvegarde automatisée SQL**</span><span class="sxs-lookup"><span data-stu-id="51b80-115">**SQL Automated Backup**</span></span> |<span data-ttu-id="51b80-116">Automatise hello planification des sauvegardes pour toutes les bases de données hello instance par défaut de SQL Server dans hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="51b80-116">Automates hello scheduling of backups for all databases for hello default instance of SQL Server in hello VM.</span></span> <span data-ttu-id="51b80-117">Pour plus d’informations, consultez [Sauvegarde automatisée pour SQL Server dans Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="51b80-117">For more information, see [Automated backup for SQL Server in Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-backup.md).</span></span> |
| <span data-ttu-id="51b80-118">**Mise à jour corrective automatisée SQL**</span><span class="sxs-lookup"><span data-stu-id="51b80-118">**SQL Automated Patching**</span></span> |<span data-ttu-id="51b80-119">Configure une fenêtre de maintenance pendant les mises à jour tooyour machine virtuelle peut prendre place de, vous pouvez ainsi éviter les mises à jour pendant les pics de charge de travail.</span><span class="sxs-lookup"><span data-stu-id="51b80-119">Configures a maintenance window during which updates tooyour VM can take place, so  you can avoid updates during peak times for your workload.</span></span> <span data-ttu-id="51b80-120">Pour plus d’informations, consultez [Mise à jour corrective automatisée pour SQL Server dans les machines virtuelles Azure (Resource Manager)](virtual-machines-windows-sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="51b80-120">For more information, see [Automated patching for SQL Server in Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-patching.md).</span></span> |
| <span data-ttu-id="51b80-121">**Intégration du coffre de clés Azure**</span><span class="sxs-lookup"><span data-stu-id="51b80-121">**Azure Key Vault Integration**</span></span> |<span data-ttu-id="51b80-122">Permet de vous tooautomatically installer et configurer le coffre de clés Azure sur votre machine virtuelle SQL Server.</span><span class="sxs-lookup"><span data-stu-id="51b80-122">Enables you tooautomatically install and configure Azure Key Vault on your SQL Server VM.</span></span> <span data-ttu-id="51b80-123">Pour plus d’informations, consultez [Configurer l’intégration du coffre de clés Azure SQL Server sur des machines virtuelles (Resource Manager)](virtual-machines-windows-ps-sql-keyvault.md).</span><span class="sxs-lookup"><span data-stu-id="51b80-123">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs (Resource Manager)](virtual-machines-windows-ps-sql-keyvault.md).</span></span> |

<span data-ttu-id="51b80-124">Une fois installé et en cours d’exécution, hello Extension de l’Agent SQL Server IaaS rend ces fonctionnalités d’administration disponibles sur Panneau de configuration hello SQL Server de hello machine virtuelle Bonjour portail Azure et Azure PowerShell pour les images de marketplace de SQL Server et par le biais Pour les installations manuelles d’extension de hello d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="51b80-124">Once installed and running, hello SQL Server IaaS Agent Extension makes these administration features available on hello SQL Server panel of hello virtual machine in hello Azure Portal and through Azure PowerShell for SQL Server marketplace images, and through Azure PowerShell for manual installations of hello extension.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="51b80-125">Composants requis</span><span class="sxs-lookup"><span data-stu-id="51b80-125">Prerequisites</span></span>
<span data-ttu-id="51b80-126">Configuration requise hello de toouse Extension de l’Agent SQL Server IaaS sur votre machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="51b80-126">Requirements toouse hello SQL Server IaaS Agent Extension on your VM:</span></span>

<span data-ttu-id="51b80-127">**Système d’exploitation**:</span><span class="sxs-lookup"><span data-stu-id="51b80-127">**Operating System**:</span></span>

* <span data-ttu-id="51b80-128">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="51b80-128">Windows Server 2012</span></span>
* <span data-ttu-id="51b80-129">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="51b80-129">Windows Server 2012 R2</span></span>
* <span data-ttu-id="51b80-130">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="51b80-130">Windows Server 2016</span></span>

<span data-ttu-id="51b80-131">**Versions de SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="51b80-131">**SQL Server versions**:</span></span>

* <span data-ttu-id="51b80-132">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="51b80-132">SQL Server 2012</span></span>
* <span data-ttu-id="51b80-133">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="51b80-133">SQL Server 2014</span></span>
* <span data-ttu-id="51b80-134">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="51b80-134">SQL Server 2016</span></span>

<span data-ttu-id="51b80-135">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="51b80-135">**Azure PowerShell**:</span></span>

* [<span data-ttu-id="51b80-136">Télécharger et configurer les commandes Azure PowerShell dernière hello</span><span class="sxs-lookup"><span data-stu-id="51b80-136">Download and configure hello latest Azure PowerShell commands</span></span>](/powershell/azure/overview)

## <a name="installation"></a><span data-ttu-id="51b80-137">Installation</span><span class="sxs-lookup"><span data-stu-id="51b80-137">Installation</span></span>
<span data-ttu-id="51b80-138">Hello, Extension de l’Agent IaaS SQL Server est installé automatiquement lorsque vous configurez une des images de la galerie de machine virtuelle SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="51b80-138">hello SQL Server IaaS Agent Extension is automatically installed when you provision one of hello SQL Server virtual machine gallery images.</span></span> <span data-ttu-id="51b80-139">Si vous avez besoin d’extension de hello tooreinstall manuellement sur l’un de ces machines virtuelles SQL Server, utilisez hello suivant de commande PowerShell :</span><span class="sxs-lookup"><span data-stu-id="51b80-139">If you need tooreinstall hello extension manually on one of these SQL Server VMs, use hello following PowerShell command:</span></span>

```powershell
Set-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension" -Version "1.2" -Location "East US 2"
```

<span data-ttu-id="51b80-140">Il est également possible tooinstall hello Extension de l’Agent IaaS SQL Server sur une machine virtuelle d’uniquement par le système d’exploitation Windows Server.</span><span class="sxs-lookup"><span data-stu-id="51b80-140">It is also possible tooinstall hello SQL Server IaaS Agent Extension on an OS-only Windows Server virtual machine.</span></span> <span data-ttu-id="51b80-141">Cette opération est autorisée uniquement si vous avez installé manuellement SQL Server sur cette machine.</span><span class="sxs-lookup"><span data-stu-id="51b80-141">This is only supported if you have also manually installed SQL Server on that machine.</span></span> <span data-ttu-id="51b80-142">Puis installer une extension hello manuellement à l’aide hello même **Set-AzureVMSqlServerExtension** applet de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="51b80-142">Then install hello extension manually by using hello same **Set-AzureVMSqlServerExtension** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="51b80-143">Si vous installez manuellement hello Extension de l’Agent IaaS SQL Server sur un ordinateur uniquement par le système d’exploitation Windows Server, vous ne pouvez pas gérer les paramètres de configuration de SQL Server hello via hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="51b80-143">If you manually install hello SQL Server IaaS Agent Extension on an OS-only Windows Server VM, you can not manage hello SQL Server configuration settings through hello Azure portal.</span></span> <span data-ttu-id="51b80-144">Dans ce cas, vous devez utiliser PowerShell pour apporter toutes vos modifications.</span><span class="sxs-lookup"><span data-stu-id="51b80-144">In this scenario, you must make all changes with PowerShell.</span></span>

## <a name="status"></a><span data-ttu-id="51b80-145">État</span><span class="sxs-lookup"><span data-stu-id="51b80-145">Status</span></span>
<span data-ttu-id="51b80-146">Une façon tooverify que hello extension est installée est état de l’agent tooview hello Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="51b80-146">One way tooverify that hello extension is installed is tooview hello agent status in hello Azure Portal.</span></span> <span data-ttu-id="51b80-147">Sélectionnez **tous les paramètres** dans hello du Panneau de l’ordinateur virtuel, puis sur **Extensions**.</span><span class="sxs-lookup"><span data-stu-id="51b80-147">Select **All settings** in hello virtual machine blade, and then click on **Extensions**.</span></span> <span data-ttu-id="51b80-148">Vous devez voir hello **SQLIaaSExtension** extension répertoriée.</span><span class="sxs-lookup"><span data-stu-id="51b80-148">You should see hello **SQLIaaSExtension** extension listed.</span></span>

![Extension Agent IaaS SQL Server dans le portail Azure](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-portal.png)

<span data-ttu-id="51b80-150">Vous pouvez également utiliser hello **Get-AzureVMSqlServerExtension** applet de commande Powershell de Azure.</span><span class="sxs-lookup"><span data-stu-id="51b80-150">You can also use hello **Get-AzureVMSqlServerExtension** Azure Powershell cmdlet.</span></span>

    Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"

<span data-ttu-id="51b80-151">commande précédente Hello confirme que l’agent de hello est installé et fournit des informations d’état général.</span><span class="sxs-lookup"><span data-stu-id="51b80-151">hello previous command confirms hello agent is installed and provides general status information.</span></span> <span data-ttu-id="51b80-152">Vous pouvez également obtenir des informations d’état spécifiques de sauvegarde automatisée et de mise à jour corrective avec hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="51b80-152">You can also get specific status information about Automated Backup and Patching with hello following commands.</span></span>

    $sqlext = Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"
    $sqlext.AutoPatchingSettings
    $sqlext.AutoBackupSettings

## <a name="removal"></a><span data-ttu-id="51b80-153">Suppression</span><span class="sxs-lookup"><span data-stu-id="51b80-153">Removal</span></span>
<span data-ttu-id="51b80-154">Bonjour portail Azure, vous pouvez désinstaller l’extension de hello en cliquant sur les points de suspension hello hello **Extensions** Panneau de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="51b80-154">In hello Azure Portal, you can uninstall hello extension by clicking hello ellipsis on hello **Extensions** blade of your virtual machine properties.</span></span> <span data-ttu-id="51b80-155">Ensuite, cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="51b80-155">Then click **Delete**.</span></span>

![Désinstaller hello Extension de l’Agent SQL Server IaaS dans le portail Azure](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-uninstall.png)

<span data-ttu-id="51b80-157">Vous pouvez également utiliser hello **Remove-AzureRmVMSqlServerExtension** applet de commande Powershell.</span><span class="sxs-lookup"><span data-stu-id="51b80-157">You can also use hello **Remove-AzureRmVMSqlServerExtension** Powershell cmdlet.</span></span>

    Remove-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension"

## <a name="next-steps"></a><span data-ttu-id="51b80-158">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="51b80-158">Next Steps</span></span>
<span data-ttu-id="51b80-159">Commencer à utiliser un des services hello pris en charge par l’extension de hello.</span><span class="sxs-lookup"><span data-stu-id="51b80-159">Begin using one of hello services supported by hello extension.</span></span> <span data-ttu-id="51b80-160">Pour plus d’informations, consultez les rubriques de hello référencées Bonjour [prise en charge des services](#supported-services) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="51b80-160">For more details, see hello topics referenced in hello [Supported services](#supported-services) section of this article.</span></span>

<span data-ttu-id="51b80-161">Pour plus d’informations sur l’exécution de SQL Server sur des machines virtuelles Azure, voir [SQL Server sur les machines virtuelles Azure](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="51b80-161">For more information about running SQL Server on Azure Virtual Machines, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

