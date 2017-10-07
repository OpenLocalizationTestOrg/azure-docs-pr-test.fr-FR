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
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-resource-manager"></a>Mise à jour corrective automatisée pour SQL Server dans Azure Virtual Machines (Resource Manager)
> [!div class="op_single_selector"]
> * [Gestionnaire de ressources](virtual-machines-windows-sql-automated-patching.md)
> * [Classique](../classic/sql-automated-patching.md)
> 
> 

La mise à jour corrective automatisée établit une fenêtre de maintenance pour une machine virtuelle Azure exécutant SQL Server. Les mises à jour automatisées ne peuvent être installées qu’au cours de cette fenêtre de maintenance. Pour SQL Server, cette rescriction garantit que les mises à jour système et les éventuels redémarrages associés se produisent au meilleur moment possible hello pour la base de données hello. Mise à jour corrective automatisée dépend hello [Extension de l’Agent SQL Server IaaS](virtual-machines-windows-sql-server-agent-extension.md).

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

version classique de hello tooview de cet article, consultez [automatisée mise à jour corrective de SQL Server dans les Machines virtuelles Azure Classic](../classic/sql-automated-patching.md).

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

* [Installez les commandes Azure PowerShell dernière hello](/powershell/azure/overview) si vous envisagez de tooconfigure les correctifs automatiques avec PowerShell.

> [!NOTE]
> Mise à jour corrective automatisée s’appuie sur hello Extension de l’Agent SQL Server IaaS. Les images actuelles de la galerie de machines virtuelles SQL ajoutent cette extension par défaut. Pour plus d’informations, consultez [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md)(Extension de l’agent IaaS SQL Server).
> 
> 

## <a name="settings"></a>Paramètres
Hello tableau suivant décrit les options de hello qui peuvent être configurées pour les correctifs automatiques. étapes de configuration réelles Hello varient selon que vous utilisez hello portail Azure ou des commandes PowerShell de Windows Azure.

| Paramètre | Valeurs possibles | Description |
| --- | --- | --- |
| **Mise à jour corrective automatisée** |Activer/Désactiver (désactivé) |Active ou désactive la mise à jour corrective automatisée pour une machine virtuelle Azure. |
| **Planification de la maintenance** |Tous les jours, lundi, mardi, mercredi, jeudi, vendredi, samedi et dimanche |planification de Hello pour télécharger et installer les mises à jour Windows et Microsoft SQL Server pour votre machine virtuelle. |
| **Heure de début de la maintenance** |0-24 |Hello Démarrer local temps tooupdate hello l’ordinateur virtuel |
| **Durée de la fenêtre de maintenance** |30 à 180 |nombre de Hello de minutes autorisées toocomplete hello télécharger et installer les mises à jour. |
| **Catégorie de correctif** |Important |catégorie de Hello de toodownload de mises à jour et les installer. |

## <a name="configuration-in-hello-portal"></a>Configuration Bonjour portail
Vous pouvez utiliser hello tooconfigure portail Azure correctifs automatiques lors de la configuration ou pour des machines virtuelles existantes.

### <a name="new-vms"></a>Nouvelles machines virtuelles
Hello d’utilisation tooconfigure portail Azure lorsque vous créez une Machine virtuelle de nouveau SQL Server dans le modèle de déploiement du Gestionnaire de ressources hello les correctifs automatiques.

Bonjour **paramètres SQL Server** panneau, sélectionnez **mise à jour corrective automatisée**. Bonjour Azure portail montre hello **les correctifs automatiques SQL** panneau.

![Mise à jour corrective automatisée SQL dans le portail Azure](./media/virtual-machines-windows-sql-automated-patching/azure-sql-arm-patching.png)

Pour le contexte, consultez la rubrique complète de hello relative [approvisionner un ordinateur virtuel de SQL Server dans Azure](virtual-machines-windows-portal-sql-server-provision.md).

### <a name="existing-vms"></a>Machines virtuelles existantes
Pour les machines virtuelles SQL Server existantes, sélectionnez votre machine virtuelle SQL Server. Puis sélectionnez hello **configuration de SQL Server** section Hello **paramètres** panneau.

![Mise à jour corrective automatisée SQL pour les machines virtuelles existantes](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-existing-vms.png)

Bonjour **configuration de SQL Server** panneau, cliquez sur hello **modifier** bouton Bonjour automatisée section mise à jour corrective.

![Configurer la mise à jour corrective automatisée SQL pour les machines virtuelles existantes](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-configuration.png)

Lorsque vous avez terminé, cliquez sur hello **OK** bouton bas hello Hello **configuration de SQL Server** panneau toosave vos modifications.

Si vous activez les correctifs automatiques pour hello première fois, Azure configure hello Agent SQL Server IaaS en arrière-plan de hello. Pendant ce temps, hello portail Azure peut ne pas affiche que les correctifs automatiques est configuré. Attendez quelques minutes pour hello toobe de l’agent installé, configuré. Après que Azure hello portail reflète les nouveaux paramètres de hello.

> [!NOTE]
> Vous pouvez également configurer la mise à jour corrective automatisée à l’aide d’un modèle. Pour plus d’informations, consultez l’article [Azure quickstart template for Automated Patching](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autopatching-update)(Modèle de démarrage rapide d’Azure pour la mise à jour corrective automatisée).
> 
> 

## <a name="configuration-with-powershell"></a>Configuration avec PowerShell
Après avoir déployé votre VM SQL, utilisez PowerShell tooconfigure correctifs automatiques.

Dans l’exemple suivant de hello, PowerShell est utilisé tooconfigure correctifs automatiques sur une machine virtuelle de serveur SQL existant. Hello **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig** commande configure une nouvelle fenêtre de maintenance pour les mises à jour automatiques.

    $vmname = "vmname"
    $resourcegroupname = "resourcegroupname"
    $aps = AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Set-AzureRmVMSqlServerExtension -AutoPatchingSettings $aps -VMName $vmname -ResourceGroupName $resourcegroupname

En fonction de cet exemple, hello tableau suivant décrit les effets pratiques de hello sur la machine virtuelle Azure cible de hello :

| Paramètre | Résultat |
| --- | --- |
| **DayOfWeek** |Les correctifs sont installés tous les jeudis. |
| **MaintenanceWindowStartingHour** |Les mises à jour démarrent à 11 h 00. |
| **MaintenanceWindowsDuration** |Les correctifs doivent être installés dans les 120 minutes. Selon l’heure de début hello, ils doivent effectuer par 1:00 pm. |
| **PatchCategory** |Hello seul réglage possible pour ce paramètre est **Important**. |

Il peut prendre plusieurs minutes tooinstall et configurer hello IaaS Agent SQL Server.

toodisable correctifs automatiques, exécution hello même script sans hello **-activer** paramètre toohello **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig**. Hello absence de hello **-activer** fonctionnalité de paramètre signaux hello commande toodisable hello.

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur les autres tâches d’automatisation disponibles, voir [Extension de l’agent IaaS SQL Server](virtual-machines-windows-sql-server-agent-extension.md).

Pour plus d’informations sur l’exécution de SQL Server sur des machines virtuelles Azure, voir [Vue d’ensemble de SQL Server sur les machines virtuelles Azure](virtual-machines-windows-sql-server-iaas-overview.md).

