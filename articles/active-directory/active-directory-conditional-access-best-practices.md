---
title: "Meilleures pratiques l’accès conditionnel dans Azure Active Directory | Microsoft Docs"
description: "Découvrez-en davantage sur les éléments à connaître ce que vous devez évite lors de la configuration des stratégies d’accès conditionnel."
services: active-directory
keywords: "accès conditionnel aux applications, accès conditionnel à Azure AD, accès sécurisé aux ressources d’entreprise, stratégies d’accès conditionnel"
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
ms.openlocfilehash: 3e524c116479c1af6eb6a601c9b57d27a697c5a2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="best-practices-for-conditional-access-in-azure-active-directory"></a>Meilleures pratiques l’accès conditionnel dans Azure Active Directory

Cette rubrique vous fournit des informations sur les éléments à connaître ce que vous devez évite lors de la configuration des stratégies d’accès conditionnel. Avant de lire cette rubrique, vous devez vous familiariser avec les concepts et la terminologie décrits dans [Accès conditionnel dans Azure Active Directory](active-directory-conditional-access-azure-portal.md)

## <a name="what-you-should-know"></a>Ce que vous devez savoir

### <a name="whats-required-to-make-a-policy-work"></a>Qu’est-ce qui est nécessaire pour faire fonctionner une stratégie ?

Lorsque vous créez une stratégie, aucun utilisateur, groupe, application ou contrôle d’accès n’est sélectionné.

![Applications cloud](./media/active-directory-conditional-access-best-practices/02.png)


Pour que votre stratégie fonctionne, vous devez configurer ce qui suit :


|Quoi           | Comment                                  | Pourquoi|
|:--            | :--                                  | :-- |
|**Applications cloud** |Vous devez sélectionner une ou plusieurs applications.  | L’objectif d’une stratégie d’accès conditionnel est de vous permettre d’ajuster la manière dont les utilisateurs autorisés peuvent accéder à vos applications.|
| **Utilisateurs et groupes** | Vous devez sélectionner au moins un utilisateur ou groupe autorisé à accéder aux applications cloud sélectionnées. | Une stratégie d’accès conditionnel, à laquelle aucun utilisateur ou groupe n’est affecté, n’est jamais déclenchée. |
| **Contrôles d’accès** | Vous devez sélectionner au moins un contrôle d'accès. | Votre processeur de stratégies doit savoir que faire si vos conditions sont remplies.|


En plus de ces exigences de base, dans de nombreux cas, vous devez également configurer une condition. Si une stratégie peut fonctionner sans condition configurée, les conditions constituent un facteur déterminant pour l’ajustement précis de l’accès à vos applications.


![Applications cloud](./media/active-directory-conditional-access-best-practices/04.png)



### <a name="how-are-assignments-evaluated"></a>Comment les affectations sont-elles évaluées ?

Toutes les attributions sont reliées par l’opérateur logique **AND**. Si vous configurez plusieurs affectations, elles doivent toutes être satisfaites pour que la stratégie soit déclenchée.  

Pour configurer une condition d’emplacement applicable à toutes les connexions non établies depuis le réseau de votre organisation, vous devez :

- inclure **tous les emplacements**,
- exclure **toutes les adresses IP approuvées**.

### <a name="what-happens-if-you-have-policies-in-the-azure-classic-portal-and-azure-portal-configured"></a>Que se passe-t-il si vous avez configuré des stratégies dans le portail Azure Classic et le portail Azure ?  
Azure Active Directory applique les deux stratégies et l’utilisateur n’obtient l’accès que si toutes les conditions requises sont remplies.

### <a name="what-happens-if-you-have-policies-in-the-intune-silverlight-portal-and-the-azure-portal"></a>Que se passe-t-il si vous avez des stratégies dans le portail Intune Silverlight et le portail Azure ?
Azure Active Directory applique les deux stratégies et l’utilisateur n’obtient l’accès que si toutes les conditions requises sont remplies.

### <a name="what-happens-if-i-have-multiple-policies-for-the-same-user-configured"></a>Que se passe-t-il si j’ai configuré plusieurs stratégies pour le même utilisateur ?  
À chaque connexion, Azure Active Directory évalue toutes les stratégies et vérifie que toutes les conditions requises sont remplies avant d’accorder l’accès à l’utilisateur.


### <a name="does-conditional-access-work-with-exchange-activesync"></a>L’accès conditionnel fonctionne-t-il avec Exchange ActiveSync ?

Oui, vous pouvez utiliser Exchange ActiveSync dans une stratégie d’accès conditionnel.


## <a name="what-you-should-avoid-doing"></a>Ce que vous devez éviter

L’infrastructure d’accès conditionnel vous offre une souplesse de configuration exceptionnelle. Toutefois, une grande souplesse signifie également que vous devez examiner chaque stratégie de configuration avant de la mettre en œuvre afin d’éviter des résultats indésirables. Dans ce contexte, prêtez une attention particulière à l’affectation de jeux complets comme par exemple **tous les utilisateurs / groupes / applications cloud**.

Dans votre environnement, vous devez éviter les configurations suivantes :


**Pour tous les utilisateurs, toutes les applications cloud :**

- **Bloquer l’accès** : cette configuration bloque toute votre organisation, ce qui n’est pas une bonne idée.

- **Exiger un appareil conforme** : pour les utilisateurs qui n’ont pas encore inscrit leurs appareils, cette stratégie bloque tout accès, notamment l’accès au portail Intune. Si vous êtes un administrateur sans appareil inscrit, cette stratégie vous bloque et vous ne pouvez pas retourner dans le portail Azure pour modifier la stratégie.

- **Exiger la jonction de domaine** : ce blocage d’accès par stratégie peut également bloquer l’accès pour tous les utilisateurs de votre organisation si vous n’avez pas encore d’appareil joint à un domaine.


**Pour tous les utilisateurs, toutes les applications cloud, toutes les plates-formes d’appareils :**

- **Bloquer l’accès** : cette configuration bloque toute votre organisation, ce qui n’est pas une bonne idée.


## <a name="common-scenarios"></a>Scénarios courants

### <a name="requiring-multi-factor-authentication-for-apps"></a>Exiger l’authentification multifacteur pour les applications

Dans de nombreux environnements, certaines applications nécessitent un niveau de protection plus élevé que d’autres.
C’est le cas des applications qui ont accès à des données sensibles.
Si vous souhaitez ajouter une couche de protection supplémentaire pour ces applications, vous pouvez configurer une stratégie d’accès conditionnel qui requiert l’authentification multifacteur lorsque les utilisateurs accèdent à ces applications.


### <a name="requiring-multi-factor-authentication-for-access-from-networks-that-are-not-trusted"></a>Exiger l’authentification multifacteur pour l’accès à partir de réseaux non approuvés

Ce scénario est semblable au précédent, car il ajoute une exigence pour l’authentification multifacteur.
Toutefois, la principale différence réside dans la condition de cette exigence.  
Tandis que le scénario précédent se concentre sur les applications ayant accès à des données sensibles, ce scénario concerne les emplacements approuvés.  
En d’autres termes, l’authentification multifacteur peut être requise si un utilisateur accède à une application à partir d’un réseau que vous n’avez pas approuvé.


### <a name="only-trusted-devices-can-access-office-365-services"></a>Seuls les appareils approuvés ont accès aux services Office 365

Si vous utilisez Intune dans votre environnement, vous pouvez utiliser d’emblée l’interface de stratégie d’accès conditionnel dans la console Azure.

De nombreux clients Intune utilisent l’accès conditionnel pour vérifier que seuls les appareils approuvés ont accès aux services Office 365. Cela signifie que les appareils mobiles sont inscrits dans Intune, qu’ils répondent aux critères de la stratégie de conformité et que des PC Windows sont joints à un domaine local. L’avantage, c’est que vous n’avez pas à définir la même stratégie pour chacun des services Office 365.  Lorsque vous créez une stratégie, configurez les applications cloud pour inclure chacune des applications Office 365 que vous souhaitez protéger avec l’accès conditionnel.

## <a name="next-steps"></a>Étapes suivantes

Pour savoir comment configurer une stratégie d’accès conditionnel, consultez [Prise en main de l’accès conditionnel dans Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).
