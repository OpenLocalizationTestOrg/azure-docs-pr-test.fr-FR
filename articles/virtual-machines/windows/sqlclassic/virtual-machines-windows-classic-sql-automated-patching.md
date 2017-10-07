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
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-classic"></a>Mise à jour corrective automatisée pour SQL Server dans les machines virtuelles Azure (classiques)
> [!div class="op_single_selector"]
> * [Gestionnaire de ressources](../sql/virtual-machines-windows-sql-automated-patching.md)
> * [Classique](../classic/sql-automated-patching.md)
> 
> 

La mise à jour corrective automatisée établit une fenêtre de maintenance pour une machine virtuelle Azure exécutant SQL Server. Les mises à jour automatisées ne peuvent être installées qu’au cours de cette fenêtre de maintenance. Pour SQL Server, ainsi que les mises à jour système et les éventuels redémarrages associés se produisent au meilleur moment possible hello pour la base de données hello. Mise à jour corrective automatisée dépend hello [Extension de l’Agent SQL Server IaaS](../classic/sql-server-agent-extension.md).

> [!IMPORTANT] 
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../azure-resource-manager/resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello. version de gestionnaire de ressources hello tooview de cet article, consultez [les correctifs automatiques pour SQL Server dans le Gestionnaire de ressources de Machines virtuelles Azure](../sql/virtual-machines-windows-sql-automated-patching.md).

## <a name="prerequisites"></a>Composants requis
toouse automatisée de mise à jour corrective, envisagez de hello suivant des conditions préalables :

**Système d’exploitation**:

* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

**Version de SQL Server**:

* SQL Server 2012
* SQL Server 2014
* SQL Server 2016

**Azure PowerShell**:

* [Installez les commandes Azure PowerShell dernière hello](/powershell/azure/overview).

**Extension IaaS SQL Server**:

* [Installer l’IaaS Extension de SQL Server de hello](../classic/sql-server-agent-extension.md).

## <a name="settings"></a>Paramètres
Hello tableau suivant décrit les options de hello qui peuvent être configurées pour les correctifs automatiques. Pour les machines virtuelles classiques, vous devez utiliser PowerShell tooconfigure ces paramètres.

| Paramètre | Valeurs possibles | Description |
| --- | --- | --- |
| **Mise à jour corrective automatisée** |Activer/Désactiver (désactivé) |Active ou désactive la mise à jour corrective automatisée pour une machine virtuelle Azure. |
| **Planification de la maintenance** |Tous les jours, lundi, mardi, mercredi, jeudi, vendredi, samedi et dimanche |planification de Hello pour télécharger et installer les mises à jour Windows et Microsoft SQL Server pour votre machine virtuelle. |
| **Heure de début de la maintenance** |0-24 |Hello Démarrer local temps tooupdate hello l’ordinateur virtuel |
| **Durée de la fenêtre de maintenance** |30 à 180 |nombre de Hello de minutes autorisées toocomplete hello télécharger et installer les mises à jour. |
| **Catégorie de correctif** |Important |catégorie de Hello de toodownload de mises à jour et les installer. |

## <a name="configuration-with-powershell"></a>Configuration avec PowerShell
Dans l’exemple suivant de hello, PowerShell est utilisé tooconfigure correctifs automatiques sur une machine virtuelle de serveur SQL existant. Hello **New-AzureVMSqlServerAutoPatchingConfig** commande configure une nouvelle fenêtre de maintenance pour les mises à jour automatiques.

    $aps = New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoPatchingSettings $aps | Update-AzureVM

En fonction de cet exemple, hello tableau suivant décrit les effets pratiques de hello sur la machine virtuelle Azure cible de hello :

| Paramètre | Résultat |
| --- | --- |
| **DayOfWeek** |Les correctifs sont installés tous les jeudis. |
| **MaintenanceWindowStartingHour** |Les mises à jour démarrent à 11 h 00. |
| **MaintenanceWindowsDuration** |Les correctifs doivent être installés dans les 120 minutes. Selon l’heure de début hello, ils doivent effectuer par 1:00 pm. |
| **PatchCategory** |Hello uniquement possibles pour ce paramètre est « Important ». |

Il peut prendre plusieurs minutes tooinstall et configurer hello IaaS Agent SQL Server.

toodisable correctifs automatiques, exécution hello même script sans hello - Enable paramètre toohello New-AzureVMSqlServerAutoPatchingConfig. Comme avec l’installation, il peut prendre plusieurs minutes toodisable correctifs automatiques.

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur les autres tâches d’automatisation disponibles, voir [Extension de l’agent IaaS SQL Server](../classic/sql-server-agent-extension.md).

Pour plus d’informations sur l’exécution de SQL Server sur des machines virtuelles Azure, voir [Vue d’ensemble de SQL Server sur les machines virtuelles Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

