---
title: "Gérer des sauvegardes avec le contrôle d’accès en fonction du rôle | Microsoft Docs"
description: "Utilisez les opérations de gestion de contrôle d’accès en fonction du rôle toomanage accès toobackup dans le coffre Recovery Services."
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 3bd46b97-4b29-47a5-b5ac-ac174dd36760
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/22/2017
ms.author: trinadhk;markgal
ms.openlocfilehash: 26d034d152f9b77fc6d5b2ffd5ef2648b1797f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-role-based-access-control-toomanage-azure-backup-recovery-points"></a>Utiliser des points de récupération de contrôle d’accès en fonction du rôle toomanage Azure Backup
Le contrôle d’accès en fonction du rôle (RBAC) Azure permet une gestion précise de l’accès pour Azure. À l’aide de RBAC, vous pouvez séparer les droits au sein de votre équipe et accorder uniquement hello quantité toousers d’accès dont ils ont besoin tooperform leur travail.

> [!IMPORTANT]
> Rôles fournis par Azure Backup sont tooactions limitées qui peuvent être effectuées dans le portail Azure ou les applets de commande PowerShell de coffre de Services de récupération. Les actions effectuées dans l’interface cliente de l’agent Azure Backup, l’interface System Center Data Protection Manager ou l’interface de serveur de sauvegarde Azure ne sont pas contrôlées par ces rôles.

Azure Backup offre des opérations de gestion de sauvegarde toocontrol 3 rôles intégrés. En savoir plus sur les [rôles intégrés Azure RBAC](../active-directory/role-based-access-built-in-roles.md)

* [Sauvegarde collaborateur](../active-directory/role-based-access-built-in-roles.md#backup-contributor) -ce rôle a toutes les autorisations toocreate et gérer la sauvegarde, à l’exception de la création du coffre Recovery Services et donnant accès tooothers. Imaginez ce rôle comme un administrateur de gestion des sauvegardes qui peut exécuter chaque opération de gestion des sauvegardes.
* [Opérateur de sauvegarde](../active-directory/role-based-access-built-in-roles.md#backup-operator) -ce rôle a tooeverything autorisations un contributeur à l’exception de la suppression de sauvegarde et la gestion des stratégies de sauvegarde. Ce rôle est toocontributor équivalente, sauf qu’il ne peut pas effectuer des opérations de destructeurs comme arrêter la sauvegarde avec suppression des données ou supprimer l’enregistrement de ressources locales.
* [Lecteur de sauvegarde](../active-directory/role-based-access-built-in-roles.md#backup-reader) -ce rôle dispose des autorisations tooview toutes les opérations de gestion de sauvegarde. Imaginez que ce rôle de toobe une personne de surveillance.

Si vous envisagez d’utiliser toodefine vos propres rôles pour encore plus de contrôle, consultez Comment trop[générer les rôles personnalisés](../active-directory/role-based-access-control-custom-roles.md) dans Azure RBAC.



## <a name="mapping-backup-built-in-roles-toobackup-management-actions"></a>Mappage des actions de gestion de sauvegarde rôles intégrés toobackup
Hello tableau suivant conserve les actions de gestion de sauvegarde hello et correspondant rôle RBAC minimal nécessaire tooperform cette opération.

| Opération de gestion | Rôle RBAC minimum nécessaire |
| --- | --- |
| Créer un coffre Recovery Services | Contributeur sur le groupe de ressources de coffre |
| Activer la sauvegarde des machines virtuelles Azure | Opérateur de sauvegarde sur le coffre, contributeur de machine virtuelle sur des machines virtuelles |
| Sauvegarde de machine virtuelle à la demande | Opérateur de sauvegarde |
| Restaurer une machine virtuelle | Opérateur de sauvegarde, les collaborateurs de groupe de ressources dans lequel les ordinateurs virtuels et des réseaux virtuels sont tooget continu déployé |
| Restaurer des disques et des fichiers individuels à partir d’une sauvegarde de machine virtuelle | Opérateur de sauvegarde |
| Créer une stratégie de sauvegarde pour la sauvegarde de machine virtuelle Azure | Contributeur de sauvegarde |
| Modifier une stratégie de sauvegarde pour la sauvegarde de machine virtuelle Azure | Contributeur de sauvegarde |
| Supprimer une stratégie de sauvegarde pour la sauvegarde de machine virtuelle Azure | Contributeur de sauvegarde |
| Arrêt de la sauvegarde (avec conservation ou suppression des données) lors la sauvegarde d’une machine virtuelle | Contributeur de sauvegarde |
| Inscrire un Windows Server/client/SCDPM ou un serveur de sauvegarde Azure | Opérateur de sauvegarde |
| Supprimer un Windows Server/client/SCDPM inscrit ou un serveur de sauvegarde Azure | Contributeur de sauvegarde |

## <a name="next-steps"></a>Étapes suivantes
* [Contrôle d’accès basé sur rôle](../active-directory/role-based-access-control-configure.md): prise en main RBAC Bonjour portail Azure.
* Découvrez comment accéder à toomanage avec :
  * [PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md)
  * [Interface de ligne de commande Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md)
  * [API REST](../active-directory/role-based-access-control-manage-access-rest.md)
* [Résolution des problèmes de contrôle d’accès en fonction du rôle](../active-directory/role-based-access-control-troubleshooting.md): obtenez des suggestions pour résoudre les problèmes courants.
