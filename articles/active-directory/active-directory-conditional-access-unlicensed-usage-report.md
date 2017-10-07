---
title: "Rapport d’utilisation d’aaaUnlicensed | Documents Microsoft"
description: "Bonjour rapport sans licence d’utilisation vous permet de de qu'identifier les utilisateurs sans licence qui sont à l’aide payer les fonctionnalités Azure AD."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 92138f43-9528-4c8a-b834-66a47da476e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: c44d1756b4641d7ca88434017eedb6c5e2567cb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="unlicensed-usage-report"></a>Rapport d’utilisation sans licence
Bonjour rapport sans licence d’utilisation vous permet de de qu'identifier les utilisateurs sans licence qui sont à l’aide payer les fonctionnalités Azure AD. Cela vous permet de toomake améliore l’utilisation des licences que vous avez achetées et tooidentify vous savez que vous ayez besoin de licences supplémentaires. 

rapport de Hello montre active l’utilisation de hello fonctionnalités payée hello 30 derniers jours. 

## <a name="report-structure"></a>Structure du rapport
| Nom de la colonne | Description |
|:--- |:--- |
| Utilisateur sans licence |Nom d’utilisateur de hello |
| Fonctionnalité |nom de la fonction Hello. Par exemple : accès conditionnel |
| Application utilisée |nom Hello d’application hello qui est accessible avec la fonctionnalité de hello. Par exemple : Office 365 SharePoint Online |

> [!NOTE]
> Si un compte d’utilisateur a été supprimé hello 'Sans licence utilisateur' colonne sera remplie avec un ID, comme 1003000090D8B285
> 
> 

## <a name="conditional-access-feature"></a>Fonctionnalité d’accès conditionnel
Les utilisateurs sans licence seront signalés lorsqu’ils accèdent à un service limité par une stratégie d’accès conditionnel s’ils ne disposent pas d’une licence Azure AD Premium. 

Cela s’applique tooMFA / stratégies de l’emplacement ainsi que les appareils des stratégies qui utilisent Intune.

## <a name="see-also"></a>Voir aussi
* [Utilisation de l’accès conditionnel avec Office 365 et les autres applications connectées à Azure Active Directory](active-directory-conditional-access.md)
* [Prise en main de l’accès conditionnel tooAzure AD](active-directory-conditional-access-azuread-connected-apps.md) 

