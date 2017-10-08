---
title: aaaAzure Active Directory Identity Protection - comment les utilisateurs toounblock | Documents Microsoft
description: "Découvrez comment débloquer les utilisateurs bloqués par une stratégie Azure Active Directory Identity Protection."
services: active-directory
keywords: "azure active directory identity protection, déblocage des utilisateurs"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: a953d425-a3ef-41f8-a55d-0202c3f250a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: cdda2808822888f76aa75cf46478738c94df51a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection---how-toounblock-users"></a>Azure Active Directory Identity Protection - comment toounblock utilisateurs
Avec la Protection d’identité Azure Active Directory, vous pouvez configurer des stratégies tooblock utilisateurs si hello configuré les conditions sont remplies. En règle générale, un utilisateur bloqué contacts help desk toobecome débloqué. Cette rubrique décrit les étapes de hello vous pouvez effectuer toounblock un utilisateur bloqué.

## <a name="determine-hello-reason-for-blocking"></a>Déterminer la raison du blocage hello
Comme une première étape toounblock un utilisateur, vous avez besoin d’un type de hello toodetermine de stratégie qui a bloqué l’utilisateur de hello, car les étapes suivantes sont associées.
Avec Azure Active Directory Identity Protection, un utilisateur peut être bloqué par une stratégie en matière de risque à la connexion ou par une stratégie de risque d’utilisateur.

Vous pouvez obtenir le type de hello de stratégie qui a bloqué un utilisateur à partir de l’en-tête de hello dans la boîte de dialogue hello qui a été présenté toohello utilisateur lors d’une tentative de connexion :

| Stratégie | Boîte de dialogue utilisateur |
| --- | --- |
| Risque à la connexion |![Connexion bloquée](./media/active-directory-identityprotection-unblock-howto/02.png) |
| Risque de l’utilisateur |![Compte bloqué](./media/active-directory-identityprotection-unblock-howto/104.png) |

Un utilisateur qui est bloqué par :

* Une stratégie en matière de risque à la connexion, également appelée connexion suspecte
* Une stratégie de risque d’utilisateur, également appelé compte à risque

## <a name="unblocking-suspicious-sign-ins"></a>Déblocage des connexions suspectes
toounblock une connexion suspect sign-in, vous avez hello options suivantes :

1. **Connexion à partir d’un emplacement ou d’un appareil connu** : les connexions suspectes bloquées sont généralement des tentatives de connexion effectuées à partir d’un emplacement ou d’un appareil inconnu. Les utilisateurs peuvent déterminer rapidement s’il s’agit de hello raison de blocage en essayant de toosign depuis un appareil ou un emplacement de votre choix.
2. **Exclure de la stratégie** : Si vous pensez que configuration actuelle de hello de votre stratégie d’authentification pose des problèmes des utilisateurs spécifiques, vous pouvez exclure des utilisateurs de hello à partir de celui-ci. Consultez [Azure Active Directory Identity Protection](active-directory-identityprotection.md) pour plus de détails.
3. **Désactiver la stratégie** : Si vous pensez que votre configuration de la stratégie pose des problèmes pour tous vos utilisateurs, vous pouvez désactiver la stratégie de hello. Consultez [Azure Active Directory Identity Protection](active-directory-identityprotection.md) pour plus de détails.

## <a name="unblocking-accounts-at-risk"></a>Déblocage des comptes à risque
toounblock un compte à risque, vous avez hello options suivantes :

1. **Réinitialisation du mot de passe** -vous pouvez réinitialiser le mot de passe de l’utilisateur hello. Pour plus d’informations, consultez la page [Réinitialisation manuelle et sécurisée du mot de passe](active-directory-identityprotection.md#manual-secure-password-reset) .
2. **Fermer tous les événements à risque** -stratégie des risques hello utilisateur empêche un utilisateur si le niveau de risque utilisateur hello configuré pour bloquer l’accès a été atteint. Vous pouvez réduire le niveau de risque d’un utilisateur en fermant manuellement les événements à risque signalés. Pour plus d’informations, consultez la page [Fermeture manuelle des événements à risque](active-directory-identityprotection.md#closing-risk-events-manually).
3. **Exclure de la stratégie** : Si vous pensez que configuration actuelle de hello de votre stratégie d’authentification pose des problèmes des utilisateurs spécifiques, vous pouvez exclure des utilisateurs de hello à partir de celui-ci. Consultez [Azure Active Directory Identity Protection](active-directory-identityprotection.md) pour plus de détails.
4. **Désactiver la stratégie** : Si vous pensez que votre configuration de la stratégie pose des problèmes pour tous vos utilisateurs, vous pouvez désactiver la stratégie de hello. Consultez [Azure Active Directory Identity Protection](active-directory-identityprotection.md) pour plus de détails.

## <a name="next-steps"></a>Étapes suivantes
 Voulez-vous tooknow plus d’informations sur Azure AD Identity Protection ? Consultez la rubrique [Azure Active Directory Identity Protection](active-directory-identityprotection.md).
