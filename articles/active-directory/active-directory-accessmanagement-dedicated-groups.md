---
title: groupes aaaDedicated dans Azure Active Directory | Documents Microsoft
description: "Vue d’ensemble du fonctionnement et de la création des groupes dédiés dans Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 86158909-083a-41fe-8090-955e96ad1865
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: 8feec6e1a4e6b384470392d3043caeeec2b03dd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="dedicated-groups-in-azure-active-directory"></a>Groupes dédiés dans Azure Active Directory
Dans Azure Active Directory (Azure AD), fonctionnalité de groupes dédiés hello crée et remplit l’appartenance des groupes Azure Active Directory prédéfini automatiquement. Les membres des groupes dédiés ne peut pas être ajoutés ou supprimé à l’aide de hello Azure classic portail, les cmdlets Windows PowerShell, ou par programme.

> [!NOTE]
> Les groupes dédiés nécessitent qu’une licence Azure AD Premium soit affectée à
>
> * administrateur Hello qui gère la règle hello sur un groupe
> * tous les utilisateurs qui sont sélectionnées par hello règle toobe un membre du groupe de hello
>
>

**groupes de tooenable dédié**

1. Bonjour [portail Azure classic](https://manage.windowsazure.com), sélectionnez **Active Directory**, puis ouvrez le répertoire de votre organisation.
2. Sélectionnez hello **groupes** onglet et groupe hello puis ouvrez tooedit.
3. Sélectionnez hello **configurer** onglet, puis définissez **activer les groupes dédiés** trop**Oui**.

Une fois que hello activer les groupes dédiés commutateur est défini trop**Oui**, vous pouvez activer davantage hello Active tooautomatically créer groupe dédié de tous les utilisateurs de hello en hello de définition **activer « Tous les utilisateurs » groupe** basculer trop**Oui**. Vous pouvez modifier puis également nom hello de ce groupe dédié en le tapant dans hello **nom d’affichage pour « Tous les utilisateurs » groupe** champ.

groupe de tous les utilisateurs Hello peut être utilisé tooassign hello aux mêmes autorisations tooall hello utilisateurs dans votre annuaire. Par exemple, vous pouvez accorder tous les utilisateurs dans votre tooa d’accès de répertoire application SaaS en attribuant l’accès pour hello tous les utilisateurs groupe dédié toothis application.

groupe de tous les utilisateurs Hello dédié inclut tous les utilisateurs dans le répertoire hello, y compris les invités et les utilisateurs externes. Si vous avez besoin d’un groupe qui exclut les utilisateurs externes, puis procéder à la création d’un groupe avec une règle dynamique basée sur les attributs tels que les suivants hello :

                (user.userPrincipalName -notContains "#EXT#@")

Pour un groupe qui exclut tous les invités, utilisez une règle, tels que les suivants hello :

                (user.userType -ne "Guest")

toolearn comment toocreate *avancées* règles (qui peut contenir plusieurs comparaisons) pour l’appartenance au groupe dynamique, consultez [à l’aide des attributs toocreate des règles avancées](active-directory-accessmanagement-groups-with-advanced-rules.md).

### <a name="next-steps"></a>Étapes suivantes
Ces articles fournissent des informations supplémentaires sur Azure Active Directory.

* [La gestion des accès tooresources avec les groupes Azure Active Directory](active-directory-manage-groups.md)
* [Index d’articles pour la gestion des applications dans Azure Active Directory](active-directory-apps-index.md)
* [Qu’est-ce qu’Azure Active Directory ?](active-directory-whatis.md)
* [Intégration des identités locales dans Azure Active Directory](active-directory-aadconnect.md)
