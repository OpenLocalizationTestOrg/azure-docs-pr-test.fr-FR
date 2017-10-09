---
title: "pratiques aaaBest pour l’accès conditionnel dans Azure Active Directory | Documents Microsoft"
description: "Découvrez-en davantage sur les éléments à connaître ce que vous devez évite lors de la configuration des stratégies d’accès conditionnel."
services: active-directory
keywords: "tooapps d’accès conditionnel, l’accès conditionnel avec Azure AD, sécuriser l’accès aux ressources toocompany, les stratégies d’accès conditionnel"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8c1d978f-e80b-420e-853a-8bbddc4bcdad
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 4952f8746a2e583380b3bb99cfe2fbdae1c07b08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-conditional-access-in-azure-active-directory"></a>Meilleures pratiques l’accès conditionnel dans Azure Active Directory

Cette rubrique vous fournit des informations sur les éléments à connaître ce que vous devez évite lors de la configuration des stratégies d’accès conditionnel. Avant de lire cette rubrique, vous devez vous familiariser avec les concepts de hello et la terminologie de hello décrites dans [accès conditionnel dans Azure Active Directory](active-directory-conditional-access-azure-portal.md)

## <a name="what-you-should-know"></a>Ce que vous devez savoir

### <a name="whats-required-toomake-a-policy-work"></a>Les étapes nécessaires toomake un travail de la stratégie ?

Lorsque vous créez une stratégie, aucun utilisateur, groupe, application ou contrôle d’accès n’est sélectionné.

![Applications cloud](./media/active-directory-conditional-access-best-practices/02.png)


toomake votre stratégie fonctionne, vous devez configurer les éléments suivants de hello :


|Quoi           | Comment                                  | Pourquoi|
|:--            | :--                                  | :-- |
|**Applications cloud** |Vous devez tooselect une ou plusieurs applications.  | Hello une stratégie d’accès conditionnel vise tooenable toofine ajuster comment les utilisateurs autorisés peuvent accéder à vos applications.|
| **Utilisateurs et groupes** | Vous devez tooselect au moins un utilisateur ou un groupe qui est autorisé que vous avez sélectionné les applications cloud hello tooaccess. | Une stratégie d’accès conditionnel, à laquelle aucun utilisateur ou groupe n’est affecté, n’est jamais déclenchée. |
| **Contrôles d’accès** | Vous devez tooselect au moins un contrôle d’accès. | Votre stratégie processeur a besoin tooknow quel toodo si vos conditions sont remplies.|


En outre toothese conditions de base, dans de nombreux cas, vous devez également configurer une condition. Une stratégie serait également fonctionner sans condition configurée, les conditions sont un facteur déterminant pour le paramétrage d’accès tooyour applications hello.


![Applications cloud](./media/active-directory-conditional-access-best-practices/04.png)



### <a name="how-are-assignments-evaluated"></a>Comment les affectations sont-elles évaluées ?

Toutes les attributions sont reliées par l’opérateur logique **AND**. Si vous avez plusieurs attribution configurée, tootrigger une stratégie, toutes les attributions doivent être respectées.  

Si vous devez tooconfigure une condition d’emplacement qui applique des connexions tooall sur en dehors du réseau de votre organisation, vous pouvez le faire par :

- inclure **tous les emplacements**,
- exclure **toutes les adresses IP approuvées**.

### <a name="what-happens-if-you-have-policies-in-hello-azure-classic-portal-and-azure-portal-configured"></a>Que se passe-t-il si vous avez des stratégies dans hello portail Azure classic et le portail Azure configuré ?  
Les deux stratégies sont appliquées par Azure Active Directory et hello utilisateur accès uniquement lorsque toutes les conditions requises sont remplies.

### <a name="what-happens-if-you-have-policies-in-hello-intune-silverlight-portal-and-hello-azure-portal"></a>Que se passe-t-il si vous avez des stratégies dans hello portail Intune Silverlight et hello portail Azure ?
Les deux stratégies sont appliquées par Azure Active Directory et hello utilisateur accès uniquement lorsque toutes les conditions requises sont remplies.

### <a name="what-happens-if-i-have-multiple-policies-for-hello-same-user-configured"></a>Que se passe-t-il si j’ai plusieurs stratégies pour hello même utilisateur configuré ?  
Pour chaque connexion, Azure Active Directory évalue toutes les stratégies et garantit que toutes les conditions requises sont remplies avant que l’utilisateur de toohello accès accordé.


### <a name="does-conditional-access-work-with-exchange-activesync"></a>L’accès conditionnel fonctionne-t-il avec Exchange ActiveSync ?

Oui, vous pouvez utiliser Exchange ActiveSync dans une stratégie d’accès conditionnel.


## <a name="what-you-should-avoid-doing"></a>Ce que vous devez éviter

infrastructure d’accès conditionnel Hello vous offre une flexibilité de configuration excellent. Toutefois, une grande souplesse signifie également que vous devez lire soigneusement chaque tooreleasing préalable de stratégie de configuration il tooavoid des résultats indésirables. Dans ce contexte, vous devez prêter tooassignments une attention particulière affecter tels que les jeux complets **tous les utilisateurs / groupes / applications cloud**.

Dans votre environnement, vous devez éviter hello suivant configurations :


**Pour tous les utilisateurs, toutes les applications cloud :**

- **Bloquer l’accès** : cette configuration bloque toute votre organisation, ce qui n’est pas une bonne idée.

- **Exiger un appareil conforme** - pour les utilisateurs qui n’ont inscrit leurs appareils encore, cette stratégie bloque tout accès, y compris l’accès toohello Intune portail. Si vous êtes un administrateur sans un appareil inscrit, cette stratégie bloque le retour à la stratégie de hello hello toochange portail Azure.

- **Exiger la jonction de domaine** - ce bloc de stratégie accès a également hello potentiels tooblock accès pour tous les utilisateurs de votre organisation si vous n’avez pas encore un appareil appartenant à un domaine.


**Pour tous les utilisateurs, toutes les applications cloud, toutes les plates-formes d’appareils :**

- **Bloquer l’accès** : cette configuration bloque toute votre organisation, ce qui n’est pas une bonne idée.


## <a name="common-scenarios"></a>Scénarios courants

### <a name="requiring-multi-factor-authentication-for-apps"></a>Exiger l’authentification multifacteur pour les applications

De nombreux environnements disposent d’applications nécessitant un niveau de protection supérieur hello d’autres.
C’est, par exemple, les cas de hello pour les applications qui ont accès aux données de toosensitive.
Si vous souhaitez tooadd une autre couche de protection toothese applications, vous pouvez configurer une stratégie d’accès conditionnel qui requiert l’authentification multifacteur lorsque les utilisateurs accèdent à ces applications.


### <a name="requiring-multi-factor-authentication-for-access-from-networks-that-are-not-trusted"></a>Exiger l’authentification multifacteur pour l’accès à partir de réseaux non approuvés

Ce scénario est le scénario précédent de toohello similaire, car elle ajoute la configuration requise pour l’authentification multifacteur.
Toutefois, hello principale différence est condition hello pour cette spécification.  
Lors de focus hello du scénario précédent de hello est sur les applications avec des données access toosensitve, hello ce scénario se concentre sur des emplacements approuvés.  
En d’autres termes, l’authentification multifacteur peut être requise si un utilisateur accède à une application à partir d’un réseau que vous n’avez pas approuvé.


### <a name="only-trusted-devices-can-access-office-365-services"></a>Seuls les appareils approuvés ont accès aux services Office 365

Si vous utilisez Intune dans votre environnement, vous pouvez commencer immédiatement à l’aide d’interface de stratégie d’accès conditionnel hello Bonjour console Azure.

De nombreux clients Intune utilisent tooensure d’accès conditionnel qu’uniquement les appareils de confiance peuvent accéder aux services Office 365. Cela signifie que les appareils mobiles sont inscrits avec Intune et répondre aux exigences de stratégie de conformité, et que les PC Windows appartiennent à un domaine local de tooan jointes. Une amélioration importante est que vous n’avez pas tooset hello même stratégie pour chacun des services de hello Office 365.  Lorsque vous créez une nouvelle stratégie, configurez hello Cloud applications tooinclude chaque des applications hello O365 que vous souhaitez tooprotect avec l’accès conditionnel.

## <a name="next-steps"></a>Étapes suivantes

Si vous souhaitez tooknow tooconfigure une stratégie d’accès conditionnel, voir [prise en main avec un accès conditionnel dans Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).
