---
title: "aaaUsing toomanage de contrôle d’accès en fonction du rôle Azure Site Recovery | Documents Microsoft"
description: "Cet article décrit comment tooapply et l’utilisation en fonction du rôle de contrôle d’accès (RBAC) toomanage vos déploiements Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: mayanknayar
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: manayar
ms.openlocfilehash: 7b721090351e561b28317ccdcf0ff283e0b146ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-role-based-access-control-toomanage-azure-site-recovery-deployments"></a>Utilisez des déploiements Azure Site Recovery Role-Based Access Control toomanage

Le contrôle d’accès en fonction du rôle (RBAC) Azure permet une gestion précise de l’accès pour Azure. À l’aide de RBAC, vous pouvez séparer les responsabilités au sein de votre équipe et accorder uniquement accès spécifique toousers d’autorisations en tant que travaux tooperform nécessaires.

Azure Site Recovery fournit des opérations de gestion de Site Recovery toocontrol 3 rôles intégrés. En savoir plus sur les [rôles intégrés Azure RBAC](../active-directory/role-based-access-built-in-roles.md)

* [Collaborateurs de la récupération de site](../active-directory/role-based-access-built-in-roles.md#site-recovery-contributor) -ce rôle dispose de toutes les opérations de Azure Site Recovery autorisations toomanage requis dans un coffre Recovery Services. Un utilisateur disposant de ce rôle, toutefois, ne peut pas créer ou supprimer un coffre Recovery Services ni affecter des utilisateurs de tooother de droits d’accès. Ce rôle est parfaitement adapté pour les administrateurs de récupération d’urgence qui peuvent activer et gérer la récupération d’urgence pour les applications ou organisations, selon les cas de hello.
* [Opérateur de récupération de site](../active-directory/role-based-access-built-in-roles.md#site-recovery-operator) -ce rôle a des autorisations tooexecute et le Gestionnaire de basculement et restauration opérations. Un utilisateur disposant de ce rôle ne peut pas activer ou désactiver la réplication, créer ou supprimer des coffres, enregistrer la nouvelle infrastructure ou affecter des utilisateurs de tooother de droits d’accès. Ce rôle est tout indiqué pour un opérateur de récupération d’urgence, qui peut basculer des machines virtuelles ou des applications lorsqu’il en reçoit la demande des propriétaires et administrateurs informatiques, dans une situation d’urgence réelle ou simulée telle qu’un test de récupération d’urgence. Valider la résolution d’un incident de hello, opérateur de récupération d’urgence de hello peut protéger de nouveau et la restauration automatique hello des machines virtuelles.
* [Lecteur de la récupération de site](../active-directory/role-based-access-built-in-roles.md#site-recovery-reader) -ce rôle dispose des autorisations tooview toutes les opérations de gestion de Site Recovery. Ce rôle est parfaitement adapté pour un responsable analyse qui peut surveiller l’état actuel de hello de protection et de déclencher des tickets de support si nécessaire.

Si vous envisagez d’utiliser toodefine vos propres rôles pour encore plus de contrôle, consultez Comment trop[générer les rôles personnalisés](../active-directory/role-based-access-control-custom-roles.md) dans Azure.

## <a name="permissions-required-tooenable-replication-for-new-virtual-machines"></a>Autorisations requises tooEnable la réplication pour les nouvelles Machines virtuelles
Lorsqu’une Machine virtuelle est répliquée tooAzure à l’aide d’Azure Site Recovery, niveaux d’accès de l’utilisateur hello associée sont validée tooensure qui hello utilisateur hello exige des autorisations toouse hello ressources Azure fournis tooSite récupération.

réplication tooenable pour une machine virtuelle, un utilisateur doit disposer :
* Autorisation toocreate une machine virtuelle dans le groupe de ressources sélectionné hello
* Autorisation toocreate une machine virtuelle dans le réseau virtuel sélectionné de hello
* Autorisation toowrite toohello le compte de stockage sélectionné

Un utilisateur doit hello suivant réplication toocomplete des autorisations d’un nouvel ordinateur virtuel.

> [!IMPORTANT]
>Assurez-vous que les autorisations appropriées sont ajoutées par le modèle de déploiement hello (Gestionnaire de ressources / classique) utilisé pour le déploiement de ressources.

| **Type de ressource** | **Modèle de déploiement** | **Permission** |
| --- | --- | --- |
| Calcul | Gestionnaire de ressources | Microsoft.Compute/availabilitySets/read |
|  |  | Microsoft.Compute/virtualMachines/read |
|  |  | Microsoft.Compute/virtualMachines/write |
|  |  | Microsoft.Compute/virtualMachines/delete |
|  | Classique | Microsoft.ClassicCompute/domainNames/read |
|  |  | Microsoft.ClassicCompute/domainNames/write |
|  |  | Microsoft.ClassicCompute/domainNames/delete |
|  |  | Microsoft.ClassicCompute/virtualMachines/read |
|  |  | Microsoft.ClassicCompute/virtualMachines/write |
|  |  | Microsoft.ClassicCompute/virtualMachines/delete |
| Réseau | Gestionnaire de ressources | Microsoft.Network/networkInterfaces/read |
|  |  | Microsoft.Network/networkInterfaces/write |
|  |  | Microsoft.Network/networkInterfaces/delete |
|  |  | Microsoft.Network/networkInterfaces/join/action |
|  |  | Microsoft.Network/virtualNetworks/read |
|  |  | Microsoft.Network/virtualNetworks/subnets/read |
|  |  | Microsoft.Network/virtualNetworks/subnets/join/action |
|  | Classique | Microsoft.ClassicNetwork/virtualNetworks/read |
|  |  | Microsoft.ClassicNetwork/virtualNetworks/join/action |
| Storage | Gestionnaire de ressources | Microsoft.Storage/storageAccounts/read |
|  |  | Microsoft.Storage/storageAccounts/listkeys/action |
|  | Classique | Microsoft.ClassicStorage/storageAccounts/read |
|  |  | Microsoft.ClassicStorage/storageAccounts/listKeys/action |
| Groupe de ressources | Gestionnaire de ressources | Microsoft.Resources/deployments/* |
|  |  | Microsoft.Resources/subscriptions/resourceGroups/read |

Vous pouvez utiliser hello 'Contributeur de la Machine virtuelle' et 'Classic collaborateur de Machine virtuelle' [rôles intégrés](../active-directory/role-based-access-built-in-roles.md) modèles respectivement pour le déploiement de gestionnaire de ressources et classique.

## <a name="next-steps"></a>Étapes suivantes
* [Contrôle d’accès en fonction du rôle](../active-directory/role-based-access-control-configure.md): prise en main RBAC Bonjour portail Azure.
* Découvrez comment accéder à toomanage avec :
  * [PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md)
  * [Interface de ligne de commande Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md)
  * [API REST](../active-directory/role-based-access-control-manage-access-rest.md)
* [Résolution des problèmes de contrôle d’accès en fonction du rôle](../active-directory/role-based-access-control-troubleshooting.md): obtenez des suggestions pour résoudre les problèmes courants.
