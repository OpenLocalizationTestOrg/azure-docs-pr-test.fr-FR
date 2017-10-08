---
title: "groupe aaaRestore un supprimé Office 365 dans Azure Active Directory | Documents Microsoft"
description: "Comment toorestore un groupe supprimé, afficher les groupes qui peuvent être restaurés et permamnently supprimer un groupe dans Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cc5f232a-1e77-45c2-b28b-1fcb4621725c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: curtand
ms.openlocfilehash: 4e6650d64aa19f0c909f1c511f48681de8032f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-deleted-office-365-group-in-azure-active-directory"></a>Restaurer un groupe Office 365 supprimé dans Azure Active Directory

Lorsque vous supprimez un groupe Office 365 Bonjour Azure Active Directory (Azure AD), groupe de hello supprimé est conservée, mais n’est pas visible pendant 30 jours à partir de la date de suppression hello. Il s’agit afin que le groupe de hello et son contenu peut être restaurées si nécessaire. Cette fonctionnalité est limitée exclusivement tooOffice 365 groupes dans Azure AD. Elle n’est pas disponible pour les groupes de sécurité et les groupes de distribution.

> [!NOTE] 
> N’utilisez pas `Remove-MsolGroup` , car il implique l’élimination de groupe de hello définitivement. Toujours utiliser `Remove-AzureADMSGroup` toodelete un O365 groupe. 

les autorisations de Hello requises toorestore un groupe peut être hello suivants :

Rôle  | Autorisations 
--------- | ---------
Administrateur de la société, Prise en charge du partenaire de niveau 2 et Administrateurs de services InTune | Peut restaurer n’importe quel groupe Office 365 supprimé 
Administrateur de compte d’utilisateur et Prise en charge du partenaire de niveau 2 | Peut restaurer n’importe quel groupe Office 365 supprimé à l’exception de ces toohello attribué de rôle d’administrateur d’entreprise 
Utilisateur | Peut restaurer n’importe quel groupe Office 365 supprimé dont il est propriétaire 


## <a name="view-hello-deleted-office-365-groups-that-are-available-toorestore"></a>Hello d’affichage supprimé les groupes Office 365 qui sont disponible toorestore
Hello suivant d’applets de commande peut être utilisé tooview hello supprimé groupes tooverify qui hello une ou ceux que vous êtes intéressé n'ont pas encore été définitivement supprimés. Ces applets de commande font partie de hello [module PowerShell Azure AD](https://www.powershellgallery.com/packages/AzureAD/). Vous trouverez plus d’informations sur ce module Bonjour [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0) l’article.

1.  Exécutez hello suivant l’applet de commande toodisplay toutes les supprimer les groupes Office 365 dans votre client qui sont toujours disponible toorestore.
  ```
  Get-AzureADMSDeletedGroup
  ```

2.  Ou bien, si vous savez objectID hello d’un groupe spécifique (et vous pouvez l’obtenir à partir de l’applet de commande hello à l’étape 1), hello exécution suivant tooverify applet de commande qui hello groupe supprimé spécifique n'a pas encore été définitivement supprimé.
  ```
  Get-AzureADMSDeletedGroup –Id <objectId>
  ```



## <a name="how-toorestore-your-deleted-office-365-group"></a>Comment toorestore votre groupe Office 365 supprimé
Une fois que vous avez vérifié que hello ce groupe est toujours disponible toorestore, restauration hello a supprimé le groupe avec l’un des hello comme suit. Si le groupe de hello contient des documents, des sites de Service Pack ou d’autres objets persistants, elle peut prendre too24 heures toofully restaurer un groupe et son contenu.

1.  Exécution hello après le groupe de hello toorestore applet de commande et son contenu.
  
  ```
  Restore-AzureADMSDeletedDirectoryObject –Id <objectId>
  ``` 

Vous pouvez également hello applet de commande suivante peut être exécuté toopermanently supprimer le groupe hello supprimé.
  ```
  Remove-AzureADMSDeletedDirectoryObject –Id <objectId>
  ```

## <a name="how-do-you-know-this-worked"></a>Comment savez-vous si l’opération a fonctionné ?
tooverify que vous avez restauré un groupe Office 365, exécutez hello `Get-AzureADGroup –ObjectId <objectId>` applet de commande toodisplay plus d’informations sur le groupe de hello. Après la restauration de hello demande est terminée :
- groupe de Hello s’affiche dans la barre de navigation gauche de hello sur Exchange
- plan Hello pour le groupe de hello s’affiche dans le planificateur
- Les sites Sharepoint et tout leur contenu sont disponibles.
- groupe de Hello est accessible à partir d’un des points de terminaison Exchange hello et autres charges de travail Office 365 qui prennent en charge les groupes Office 365


## <a name="next-steps"></a>Étapes suivantes
Ces articles fournissent des informations supplémentaires sur les groupes Azure Active Directory.

* [Consulter les groupes existants](active-directory-groups-view-azure-portal.md)
* [Gérer les paramètres d’un groupe](active-directory-groups-settings-azure-portal.md)
* [Gérer les membres d’un groupe](active-directory-groups-members-azure-portal.md)
* [Gérer l’appartenance à un groupe](active-directory-groups-membership-azure-portal.md)
* [Gérer les règles dynamiques pour les utilisateurs dans un groupe](active-directory-groups-dynamic-membership-azure-portal.md)
