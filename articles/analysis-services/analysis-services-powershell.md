---
title: aaaManage Azure Analysis Services avec PowerShell | Documents Microsoft
description: "Gestion d’Azure Analysis Services avec PowerShell."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: owend
ms.openlocfilehash: bc4250bf77b5a0d86c1049ee57493bcf2a1f0c1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-analysis-services-with-powershell"></a>Gérer Azure Analysis Services avec PowerShell

Cet article décrit PowerShell applets de commande utilisées tooperform Azure Analysis Services serveur et base de données de tâches de gestion. 

Tâches de gestion de serveur comme la création ou suppression d’un serveur, la suspension ou la reprise des opérations de serveur ou la modification du niveau de service hello (niveau) utilisent les applets de commande Azure Resource Manager (Azure Resource Manager). Autres tâches de gestion des bases de données telles qu’ajouter ou supprimer les membres du rôle, le traitement ou le partitionnement applets inclus dans hello même module SQL Server en tant que SQL Server Analysis Services.

## <a name="permissions"></a>Autorisations
La plupart des tâches PowerShell nécessitent que vous disposez des privilèges d’administrateur sur le serveur Analysis Services hello que vous gérez. Les tâches PowerShell planifiées s’exécutent sans assistance. compte de Hello en cours d’exécution du Planificateur de hello doit disposer des privilèges d’administrateur sur le serveur Analysis Services de hello. 

Pour les opérations de serveur à l’aide des applets de commande Azure Resource Manager, votre compte ou le compte hello du planificateur en cours d’exécution doit également appartenir toohello propriétaire de la ressource hello dans [du contrôle d’accès (RBAC)](../active-directory/role-based-access-control-what-is.md). 

## <a name="server-operations"></a>Opérations de serveur 
Applets de commande Azure Analysis Services sont inclus dans hello [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices) module de composant. modules d’applet de commande tooinstall Azure Resource Manager, consultez [applets de commande Azure Resource Manager](/powershell/azure/overview) Bonjour PowerShell Gallery.

|Applet de commande|Description| 
|------------|-----------------| 
|[Export-AzureAnalysisServicesInstance](/powershell/module/azurerm.analysisservices/export-azureanalysisservicesinstancelog)|Exportations journal toofile.| 
|[Get-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/get-azurermanalysisservicesserver)|Obtient les détails d’une instance de serveur.|  
|[New-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver)|Crée une instance de serveur.|
|[Remove-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/remove-azurermanalysisservicesserver)|Supprime une instance de serveur.|  
|[Suspend-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/suspend-azurermanalysisservicesserver)|Interrompt une instance de serveur.| 
|[Resume-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/resume-azurermanalysisservicesserver)|Reprend une instance de serveur.|  
|[Set-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/set-azurermanalysisservicesserver)|Modifie une instance de serveur.|   
|[Test-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/test-azurermanalysisservicesserver)|Tests hello l’existence d’une instance de serveur.| 

## <a name="database-operations"></a>Opérations de base de données

Azure Analysis Services, les opérations de base de données utiliser hello même [SqlServer](https://www.powershellgallery.com/packages/SqlServer) module en tant que SQL Server Analysis Services. Toutefois, certaines applets de commande ne sont pas prises en charge par Azure Analysis Services. 

module de SqlServer Hello fournit des applets de commande de gestion de base de données spécifiques à une tâche ainsi que l’applet de commande hello usage général Invoke-ASCmd qui accepte un script langage TMSL (Tabular Model) de requête ou de script. Hello applets de commande suivantes dans le module SqlServer de hello sont pris en charge pour Azure Analysis Services.

  
|Applet de commande|Description|
|------------|-----------------| 
|[Add-RoleMember](https://msdn.microsoft.com/library/hh510167.aspx)|Ajouter un rôle de base de données de membre tooa.| 
|[Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet)|Sauvegarde une base de données Analysis Services.|  
|[Remove-RoleMember](https://msdn.microsoft.com/library/hh510173.aspx)|Supprime un membre d’un rôle de base de données.|   
|[Invoke-ASCmd](https://msdn.microsoft.com/library/hh479579.aspx)|Exécute un script TMSL.|
|[Invoke-ProcessASDatabase](https://msdn.microsoft.com/library/mt651773.aspx)|Traite une base de données.|  
|[Invoke-ProcessPartition](https://msdn.microsoft.com/library/hh510164.aspx)|Traite une partition.| 
|[Invoke-ProcessTable](https://msdn.microsoft.com/library/mt651774.aspx)|Traiter une table.|  
|[Merge-Partition](https://msdn.microsoft.com/library/hh479576.aspx)|Fusionne une partition.|  
|[Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet)|Restaurer une base de données Analysis Services.| 
  

## <a name="related-information"></a>Informations connexes

* [Télécharger le module SQL Server PowerShell](https://docs.microsoft.com/sql/ssms/download-sql-server-ps-module)   
* [Télécharger SSMS](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)   
* [Module SqlServer dans PowerShell Gallery](https://www.powershellgallery.com/packages/SqlServer)    
* [Programmation de modèle tabulaire pour le niveau de compatibilité 1200 et ultérieur](https://msdn.microsoft.com/library/mt712541.aspx)
