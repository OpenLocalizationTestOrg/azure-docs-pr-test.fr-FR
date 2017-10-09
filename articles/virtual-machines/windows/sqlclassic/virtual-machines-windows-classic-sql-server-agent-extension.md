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
# <a name="automate-management-tasks-on-azure-virtual-machines-with-hello-sql-server-agent-extension-classic"></a>Automatiser les tâches de gestion sur des Machines virtuelles Azure avec hello Extension de l’Agent SQL Server (classique)
> [!div class="op_single_selector"]
> * [Gestionnaire de ressources](../sql/virtual-machines-windows-sql-server-agent-extension.md)
> * [Classique](../classic/sql-server-agent-extension.md)
> 
>
 
Hello, Extension de l’Agent SQL Server IaaS (sqliaasagent n’est) s’exécute sur les machines virtuelles tooautomate les tâches d’administration. Cette rubrique fournit une vue d’ensemble des services hello pris en charge par l’extension de hello ainsi que des instructions pour l’installation, l’état et la suppression.

> [!IMPORTANT] 
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../azure-resource-manager/resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello. version de gestionnaire de ressources hello tooview de cet article, consultez [Extension de l’Agent SQL Server pour SQL Server machines virtuelles Resource Manager](../sql/virtual-machines-windows-sql-server-agent-extension.md).

## <a name="supported-services"></a>Services pris en charge
Hello Extension de l’Agent IaaS SQL Server prend en charge hello tâches d’administration suivantes :

| Fonction d’administration | Description |
| --- | --- |
| **Sauvegarde automatisée SQL** |Automatise hello planification des sauvegardes pour toutes les bases de données hello instance par défaut de SQL Server dans hello machine virtuelle. Pour plus d’informations, consultez [Sauvegarde automatisée pour SQL Server dans les machines virtuelles Azure (Classic)](../classic/sql-automated-backup.md). |
| **Mise à jour corrective automatisée SQL** |Configure une fenêtre de maintenance pendant les mises à jour tooyour machine virtuelle peut prendre place de, vous pouvez ainsi éviter les mises à jour pendant les pics de charge de travail. Pour plus d’informations, consultez [Mise à jour corrective automatisée pour SQL Server dans les machines virtuelles Azure (Classic)](../classic/sql-automated-patching.md). |
| **Intégration du coffre de clés Azure** |Permet de vous tooautomatically installer et configurer le coffre de clés Azure sur votre machine virtuelle SQL Server. Pour plus d’informations, consultez [Configurer Azure Key Vault Integration (Intégration du coffre de clés Azure) pour SQL Server sur des machines virtuelles Azure (Classic)](../classic/ps-sql-keyvault.md). |

## <a name="prerequisites"></a>Composants requis
Configuration requise hello de toouse Extension de l’Agent SQL Server IaaS sur votre machine virtuelle :

### <a name="operating-system"></a>Système d’exploitation :
* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

### <a name="sql-server-versions"></a>Versions de SQL Server :
* SQL Server 2012
* SQL Server 2014
* SQL Server 2016

### <a name="azure-powershell"></a>Azure PowerShell :
[Télécharger et configurer les commandes Azure PowerShell dernière hello](/powershell/azure/overview).

Démarrez Windows PowerShell et le connecter tooyour abonnement Azure avec hello **Add-AzureAccount** commande.

    Add-AzureAccount

Si vous avez plusieurs abonnements, utilisez **Select-AzureSubscription** abonnement hello tooselect qui contient la cible de machine virtuelle classique.

    Select-AzureSubscription -SubscriptionName <subscriptionname>

À ce stade, vous pouvez obtenir une liste de machines virtuelles classiques de hello et leurs noms de service associé avec hello **Get-AzureVM** commande.

    Get-AzureVM

## <a name="installation"></a>Installation
Pour les machines virtuelles classiques, vous devez utiliser PowerShell tooinstall hello Extension de l’Agent IaaS SQL Server et configurer ses services associés. Hello d’utilisation **Set-AzureVMSqlServerExtension** extension de hello tooinstall PowerShell applet de commande. Par exemple, hello de commande suivante installe l’extension de hello sur une machine virtuelle (classique) de Windows Server et le nomme « SQLIaaSExtension ».

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -ReferenceName "SQLIaasExtension" -Version "1.2" | Update-AzureVM

Si vous mettez à jour plus récent toohello hello Extension de l’Agent IaaS SQL, vous devez redémarrer votre machine virtuelle après la mise à jour hello extension.

> [!NOTE]
> Machines virtuelles classiques ne pas avoir un tooinstall option et configurer hello Extension de l’Agent IaaS SQL via le portail de hello.
> 
> 

## <a name="status"></a>État
Une façon tooverify que hello extension est installée est état de l’agent tooview hello Bonjour portail Azure. Sélectionnez une machine virtuelle répertoriée dans le panneau de machine virtuelle hello, puis sur **Extensions**. Vous devez voir hello **sqliaasagent n’est** extension répertoriée.

![Extension Agent IaaS SQL Server dans le portail Azure](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-portal.png)

Vous pouvez également utiliser hello **Get-AzureVMSqlServerExtension** applet de commande Powershell de Azure.

    Get-AzureVM –ServiceName "service" –Name "vmname" | Get-AzureVMSqlServerExtension

## <a name="removal"></a>Suppression
Bonjour portail Azure, vous pouvez désinstaller l’extension de hello en cliquant sur les points de suspension hello hello **Extensions** Panneau de votre machine virtuelle. Cliquez ensuite sur **Désinstaller**.

![Désinstaller hello Extension de l’Agent SQL Server IaaS dans le portail Azure](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-uninstall.png)

Vous pouvez également utiliser hello **Remove-AzureVMSqlServerExtension** applet de commande Powershell.

    Get-AzureVM –ServiceName "service" –Name "vmname" | Remove-AzureVMSqlServerExtension | Update-AzureVM

## <a name="next-steps"></a>Étapes suivantes
Commencer à utiliser un des services hello pris en charge par l’extension de hello. Pour plus d’informations, consultez les rubriques de hello référencées Bonjour [prise en charge des services](#supported-services) section de cet article.

Pour plus d’informations sur l’exécution de SQL Server sur des machines virtuelles Azure, voir [SQL Server sur les machines virtuelles Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

