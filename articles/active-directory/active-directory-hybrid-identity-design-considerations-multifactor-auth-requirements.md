---
title: "Considérations de conception pour les identités hybrides aaaAzure Active Directory - déterminer les besoins de l’authentification multifacteur"
description: "Avec le contrôle d’accès conditionnel, Azure Active Directory vérifie les conditions spécifiques hello que vous choisissez lors de l’authentification utilisateur de hello et avant d’autoriser l’accès toohello application. Lorsque ces conditions sont réunies, hello utilisateur authentifié et autorisé accès toohello application."
documentationcenter: 
services: active-directory
author: femila
manager: billmath
editor: 
ms.assetid: 9c59fda9-47d0-4c7e-b3e7-3575c29beabe
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 49fa7b43772fb3a2d6664747477c60a34cddde2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="determine-multi-factor-authentication-requirements-for-your-hybrid-identity-solution"></a>Déterminer les besoins d'authentification multifacteur (Multi-Factor Authentication) pour votre solution d'identités hybrides
Dans ce monde de mobilité, avec les utilisateurs qui accèdent aux données et des applications dans le cloud de hello et à partir de n’importe quel appareil, sécuriser ces informations jouent un rôle essentiel.  On entend parler chaque jour de nouvelles failles de sécurité.  Bien qu’il n’existe aucune garantie contre ces violations, l’authentification multifacteur, fournit une couche supplémentaire de sécurité toohelp empêcher les violations.
Commencez par l’évaluation des besoins des entreprises hello pour l’authentification multifacteur. Autrement dit, ce qui est toosecure lors de la tentative de hello entreprise.  Cette évaluation est important toodefine hello technique configuration requise pour installer et activer les utilisateurs des organisations hello pour l’authentification multifacteur.

> [!NOTE]
> Si vous n’êtes pas familiarisé avec l’authentification Multifacteur et ce qu’il fait, il est fortement recommandé de lire l’article de hello [Nouveautés d’Azure multi-Factor Authentication ?](../multi-factor-authentication/multi-factor-authentication.md) toocontinue préalable lire cette section.
> 
> 

Rendre suivant de hello tooanswer que :

* Votre entreprise tente d’applications de Microsoft toosecure ? 
* Comment ces applications sont-elles publiées ?
* Votre entreprise fournit l’accès à distance tooallow employés tooaccess local applications ?

Si Oui, quel type d’accès à distance ? Vous devez également tooevaluate où les utilisateurs hello qui accèdent à ces applications se trouve. Cette évaluation est une autre stratégie de l’authentification multifacteur appropriée hello toodefine étape importante. Vérifiez que hello tooanswer suivant questions :

* Où sont situés les utilisateurs hello va toobe ?
* Peuvent-ils se trouver à un endroit quelconque ?
* Votre entreprise souhaite-t-elle restrictions tooestablish selon l’emplacement de l’utilisateur toohello ?

Une fois que vous avez compris ces exigences, il est important de tooalso évaluer les besoins de l’utilisateur hello pour l’authentification multifacteur. Cette évaluation est importante, car elle définit les exigences de hello pour le déploiement de l’authentification multifacteur. Vérifiez que hello tooanswer suivant questions :

* Sont les utilisateurs de hello familiarisé avec l’authentification multifacteur ?
* Certaines utilisations sera une authentification supplémentaire tooprovide requis ?  
  * Si Oui, toutes les hello moment, provenant des réseaux externes, ou l’accès aux applications spécifiques, ou dans d’autres conditions ?
* Les utilisateurs hello besoin d’une formation sur la façon de toosetup et implémenter l’authentification multifacteur ?
* Quels sont les scénarios clés hello que votre entreprise souhaite tooenable l’authentification multifacteur pour les utilisateurs ?

Après avoir répondu aux questions précédentes de hello, vous serez en mesure de toounderstand s’il y a déjà mis en œuvre l’authentification multifacteur localement. Cette évaluation est important toodefine hello technique configuration requise pour installer et activer les utilisateurs des organisations hello pour l’authentification multifacteur. Vérifiez que hello tooanswer suivant questions :

* Votre entreprise a-t-elle besoin de comptes tooprotect privilégié avec l’authentification Multifacteur ?
* Votre entreprise a-t-elle besoin tooenable l’authentification Multifacteur pour certaines applications pour des raisons de conformité ?
* Votre entreprise a-t-elle besoin tooenable l’authentification Multifacteur pour tous les utilisateurs de ces applications ou les seuls les administrateurs ?
* Peut-être avez-vous MFA toujours activée ou uniquement lorsque les utilisateurs de hello sont enregistrés en dehors de votre réseau d’entreprise ?

## <a name="next-steps"></a>Étapes suivantes
[Définir une stratégie d’adoption des identités hybrides](active-directory-hybrid-identity-design-considerations-identity-adoption-strategy.md)

## <a name="see-also"></a>Voir aussi
[Présentation des considérations relatives à la conception](active-directory-hybrid-identity-design-considerations-overview.md)

