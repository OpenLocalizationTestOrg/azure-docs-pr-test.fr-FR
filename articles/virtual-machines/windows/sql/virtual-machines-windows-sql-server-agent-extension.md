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
# <a name="automate-management-tasks-on-azure-virtual-machines-with-hello-sql-server-agent-extension-resource-manager"></a>Automatiser les tâches de gestion sur des Machines virtuelles Azure avec hello Extension de l’Agent SQL Server (Gestionnaire de ressources)
> [!div class="op_single_selector"]
> * [Gestionnaire de ressources](virtual-machines-windows-sql-server-agent-extension.md)
> * [Classique](../classic/sql-server-agent-extension.md)
> 
> 

Hello, Extension de l’Agent SQL Server IaaS (SQLIaaSExtension) s’exécute sur les machines virtuelles tooautomate les tâches d’administration. Cette rubrique fournit une vue d’ensemble des services hello pris en charge par l’extension de hello ainsi que des instructions pour l’installation, l’état et la suppression.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

version classique de hello tooview de cet article, consultez [Extension de l’Agent SQL Server pour SQL Server machines virtuelles Classic](../classic/sql-server-agent-extension.md).

## <a name="supported-services"></a>Services pris en charge
Hello Extension de l’Agent IaaS SQL Server prend en charge hello tâches d’administration suivantes :

| Fonction d’administration | Description |
| --- | --- |
| **Sauvegarde automatisée SQL** |Automatise hello planification des sauvegardes pour toutes les bases de données hello instance par défaut de SQL Server dans hello machine virtuelle. Pour plus d’informations, consultez [Sauvegarde automatisée pour SQL Server dans Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-backup.md). |
| **Mise à jour corrective automatisée SQL** |Configure une fenêtre de maintenance pendant les mises à jour tooyour machine virtuelle peut prendre place de, vous pouvez ainsi éviter les mises à jour pendant les pics de charge de travail. Pour plus d’informations, consultez [Mise à jour corrective automatisée pour SQL Server dans les machines virtuelles Azure (Resource Manager)](virtual-machines-windows-sql-automated-patching.md). |
| **Intégration du coffre de clés Azure** |Permet de vous tooautomatically installer et configurer le coffre de clés Azure sur votre machine virtuelle SQL Server. Pour plus d’informations, consultez [Configurer l’intégration du coffre de clés Azure SQL Server sur des machines virtuelles (Resource Manager)](virtual-machines-windows-ps-sql-keyvault.md). |

Une fois installé et en cours d’exécution, hello Extension de l’Agent SQL Server IaaS rend ces fonctionnalités d’administration disponibles sur Panneau de configuration hello SQL Server de hello machine virtuelle Bonjour portail Azure et Azure PowerShell pour les images de marketplace de SQL Server et par le biais Pour les installations manuelles d’extension de hello d’Azure PowerShell. 

## <a name="prerequisites"></a>Composants requis
Configuration requise hello de toouse Extension de l’Agent SQL Server IaaS sur votre machine virtuelle :

**Système d’exploitation**:

* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

**Versions de SQL Server**:

* SQL Server 2012
* SQL Server 2014
* SQL Server 2016

**Azure PowerShell**:

* [Télécharger et configurer les commandes Azure PowerShell dernière hello](/powershell/azure/overview)

## <a name="installation"></a>Installation
Hello, Extension de l’Agent IaaS SQL Server est installé automatiquement lorsque vous configurez une des images de la galerie de machine virtuelle SQL Server hello. Si vous avez besoin d’extension de hello tooreinstall manuellement sur l’un de ces machines virtuelles SQL Server, utilisez hello suivant de commande PowerShell :

```powershell
Set-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension" -Version "1.2" -Location "East US 2"
```

Il est également possible tooinstall hello Extension de l’Agent IaaS SQL Server sur une machine virtuelle d’uniquement par le système d’exploitation Windows Server. Cette opération est autorisée uniquement si vous avez installé manuellement SQL Server sur cette machine. Puis installer une extension hello manuellement à l’aide hello même **Set-AzureVMSqlServerExtension** applet de commande PowerShell.

> [!NOTE]
> Si vous installez manuellement hello Extension de l’Agent IaaS SQL Server sur un ordinateur uniquement par le système d’exploitation Windows Server, vous ne pouvez pas gérer les paramètres de configuration de SQL Server hello via hello portail Azure. Dans ce cas, vous devez utiliser PowerShell pour apporter toutes vos modifications.

## <a name="status"></a>État
Une façon tooverify que hello extension est installée est état de l’agent tooview hello Bonjour portail Azure. Sélectionnez **tous les paramètres** dans hello du Panneau de l’ordinateur virtuel, puis sur **Extensions**. Vous devez voir hello **SQLIaaSExtension** extension répertoriée.

![Extension Agent IaaS SQL Server dans le portail Azure](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-portal.png)

Vous pouvez également utiliser hello **Get-AzureVMSqlServerExtension** applet de commande Powershell de Azure.

    Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"

commande précédente Hello confirme que l’agent de hello est installé et fournit des informations d’état général. Vous pouvez également obtenir des informations d’état spécifiques de sauvegarde automatisée et de mise à jour corrective avec hello suivant les commandes.

    $sqlext = Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"
    $sqlext.AutoPatchingSettings
    $sqlext.AutoBackupSettings

## <a name="removal"></a>Suppression
Bonjour portail Azure, vous pouvez désinstaller l’extension de hello en cliquant sur les points de suspension hello hello **Extensions** Panneau de votre machine virtuelle. Ensuite, cliquez sur **Supprimer**.

![Désinstaller hello Extension de l’Agent SQL Server IaaS dans le portail Azure](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-uninstall.png)

Vous pouvez également utiliser hello **Remove-AzureRmVMSqlServerExtension** applet de commande Powershell.

    Remove-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension"

## <a name="next-steps"></a>Étapes suivantes
Commencer à utiliser un des services hello pris en charge par l’extension de hello. Pour plus d’informations, consultez les rubriques de hello référencées Bonjour [prise en charge des services](#supported-services) section de cet article.

Pour plus d’informations sur l’exécution de SQL Server sur des machines virtuelles Azure, voir [SQL Server sur les machines virtuelles Azure](virtual-machines-windows-sql-server-iaas-overview.md).

