---
title: "Création de rapports aaaAccess - Azure RBAC. | Documents Microsoft"
description: "Générer un rapport que répertorie toutes les modifications dans tooyour d’accès abonnements Azure, avec contrôle d’accès basée sur hello 90 derniers jours."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 2bc68595-145e-4de3-8b71-3a21890d13d9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/17/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9ad85d3d8e66ce167032638a35e4afffb46d3892
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-access-report-for-role-based-access-control"></a>Créer un rapport d’accès pour le contrôle d’accès en fonction du rôle
Chaque fois qu’un utilisateur accorde ou révoque l’accès au sein de vos abonnements, les modifications de hello sont consignées dans les événements de Azure. Vous pouvez créer accès modifier l’historique des rapports toosee toutes les modifications pour hello 90 derniers jours.

## <a name="create-a-report-with-azure-powershell"></a>Créer un rapport avec Azure PowerShell
toocreate un accès à modifier le rapport d’historique dans PowerShell, utilisez hello [Get-AzureRMAuthorizationChangeLog](/powershell/module/azurerm.resources/get-azurermauthorizationchangelog) commande.

Lorsque vous appelez cette commande, vous pouvez spécifier la propriété hello aux affectations de répertoriées, y compris les hello suivant :

| Propriété | Description |
| --- | --- |
| **Action** |Si l’accès a été autorisé ou interdit |
| **Appelant** |le propriétaire de Hello responsable de l’accès hello modifier |
| **PrincipalId** | Identificateur unique de l’application qui a été attribuée le rôle de hello, groupe ou utilisateur de hello de Hello |
| **PrincipalName** |Hello nom d’utilisateur de hello, groupe ou application |
| **PrincipalType** |Indique si l’attribution de hello a pour un utilisateur, un groupe ou une application |
| **RoleDefinitionId** |Hello GUID du rôle hello qui a été accordé ou révoqué |
| **RoleName** |rôle Hello qui a été accordé ou révoqué |
| **Portée** | Identificateur unique de Hello d’abonnement de hello, groupe de ressources ou ressource hello assignation s’applique également| 
| **ScopeName** |Hello nom d’abonnement de hello, groupe de ressources ou ressource |
| **ScopeType** |Indique si l’attribution de hello a à portée de la ressource, groupe de ressources ou abonnement de hello |
| **Timestamp** |hello date et l’heure que l’accès a été modifié. |

Cet exemple de commande répertorie toutes les modifications d’accès dans l’abonnement hello pour hello sept derniers jours :

```
Get-AzureRMAuthorizationChangeLog -StartTime ([DateTime]::Now - [TimeSpan]::FromDays(7)) | FT Caller,Action,RoleName,PrincipalType,PrincipalName,ScopeType,ScopeName
```

![PowerShell Get-AzureRMAuthorizationChangeLog - capture d’écran](./media/role-based-access-control-configure/access-change-history.png)

## <a name="create-a-report-with-azure-cli"></a>Créer un rapport avec l’interface de ligne de commande Azure
toocreate un rapport historique des modifications accès Bonjour Azure interface de ligne de commande (CLI), utilisez hello `azure role assignment changelog list` commande.

## <a name="export-tooa-spreadsheet"></a>Exporter la feuille de calcul tooa
toosave hello rapport ou manipuler des données de hello, exportation hello accès se transforme en un fichier .csv. Vous pouvez ensuite afficher les rapports hello dans une feuille de calcul pour la révision.

![ChangeLog affiché en tant que feuille de calcul - capture d’écran](./media/role-based-access-control-configure/change-history-spreadsheet.png)

## <a name="next-steps"></a>Étapes suivantes
* Utilisation des [rôles personnalisés dans le contrôle d’accès en fonction du rôle (RBAC) Azure](role-based-access-control-custom-roles.md)
* Découvrez comment toomanage [RBAC Azure avec powershell](role-based-access-control-manage-access-powershell.md)

