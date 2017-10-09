---
title: "Assistant de sécurité aaaThe Azure AD Privileged Identity Management"
description: "Hello première fois que vous utilisez extension d’Azure Active Directory Privileged Identity Management hello, s’affiche avec un Assistant de sécurité. Cet article décrit les étapes de hello pour utiliser l’Assistant de hello."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: a53a3719-8cc7-4fc7-8164-aafca192871b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/27/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: 0b3019134d3c7cfac33b3acfcf430b4d4f67b119
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-security-wizard-in-azure-ad-privileged-identity-management"></a>À l’aide de l’Assistant sécurité hello dans Azure AD Privileged Identity Management 
Si vous êtes hello première personne toorun Azure Privileged Identity Management (PIM) pour votre organisation, un Assistant s’affiche. Assistant de Hello vous permet de comprendre les risques de sécurité hello d’identités privilégiées et comment toouse PIM tooreduce ces risques. Vous n’avez pas besoin toomake les attributions de rôle tooexisting modifications dans l’Assistant de hello, si vous préférez toodo plus tard.

## <a name="what-tooexpect"></a>Quel tooexpect
Avant le démarrage de votre organisation à l’aide de PIM, toutes les attributions de rôle sont permanentes : hello utilisateurs sont toujours à ces rôles même si elles ne doivent pas actuellement de leurs privilèges.  Hello première étape de hello Assistant vous présente une liste des rôles de privilèges élevés et le nombre d’utilisateurs actuellement dans ces rôles. Vous pouvez Explorer toolearn de rôle particulier tooa savoir plus sur les utilisateurs si une ou plusieurs d'entre eux sont inconnues.

Hello deuxième étape de hello Assistant vous donne les attributions de rôles d’administrateur toochange opportunité.  

> [!WARNING]
> Il est important de disposer d’au moins un administrateur général et plusieurs administrateurs de rôle privilégié avec un compte professionnel ou scolaire (et non un compte Microsoft). S’il n'existe qu’un seul administrateur du rôle privilégié, organisation de hello ne seront pas en mesure de toomanage PIM si ce compte est supprimé.
> En outre, conserver les attributions de rôles permanente si un utilisateur possède un compte Microsoft (compte qu’ils utilisent toosign dans tooMicrosoft des services tels que Skype et Outlook.com). Si vous envisagez de toorequire l’authentification Multifacteur pour l’activation de ce rôle, cet utilisateur sera verrouillé.
> 
> 

Une fois que vous avez apporté des modifications, Assistant de hello n’affiche plus. Hello prochaine fois que vous ou un autre administrateur de rôle privilégié utilisez PIM, vous verrez hello PIM tableau de bord.  

* Si vous souhaitez tooadd ou supprimer des utilisateurs des rôles ou modifier les affectations de tooeligible permanente, en savoir plus sur [comment tooadd ou supprimer le rôle d’un utilisateur](active-directory-privileged-identity-management-how-to-add-role-to-user.md).
* Si vous souhaitez que toogive davantage d’utilisateurs accès toomanage PIM, en savoir plus sur [comment toogive aux toomanage dans PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).

## <a name="next-steps"></a>Étapes suivantes
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

