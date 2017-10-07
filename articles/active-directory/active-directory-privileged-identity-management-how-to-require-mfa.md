---
title: "l’authentification multifacteur de toorequire aaaHow | Documents Microsoft"
description: "Découvrez comment toorequire l’authentification multifacteur (MFA) pour privilégié identités avec l’extension d’Azure Active Directory Privileged Identity Management hello."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 1e3dc4ad-3a6a-4a52-8417-3ca4f84ae05c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: c08fad9dc80c09a14a4bd7497da4942fa227c3ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorequire-mfa-in-azure-ad-privileged-identity-management"></a>Comment toorequire l’authentification Multifacteur dans Azure AD Privileged Identity Management
Il est vivement recommandé d’exiger l’application de la solution Multi-Factor Authentication (MFA) pour tous vos administrateurs. Cela réduit le risque de hello d’une attaque en raison d’un mot de passe tooa compromis.

Vous pouvez exiger que les utilisateurs se soumettent à une authentification MFA lors de leur connexion. billet de blog de Hello [MFA pour Office 365 et l’authentification Multifacteur pour Azure](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/) compare ce qui est inclus dans Office et les abonnements Azure, avec les fonctionnalités de hello contenues dans l’offre Microsoft Azure multi-Factor Authentication hello.

Vous pouvez également exiger que les utilisateurs effectuent une demande d'authentification MFA lorsqu’ils activent un rôle dans Azure AD PIM. De cette manière, si l’utilisateur de hello n’a pas terminé une stimulation d’authentification Multifacteur lorsqu’ils connecté, ils seront demandée toodo c’est le cas par PIM.

## <a name="requiring-mfa-in-azure-ad-privileged-identity-management"></a>Exigence d’application de la solution MFA dans Azure AD Privileged Identity Management
Quand vous gérez des identités dans PIM en tant qu’administrateur de rôle privilégié, vous pouvez voir des alertes qui recommandent l’authentification MFA pour des comptes privilégiés. Cliquez sur la sécurité hello alerte dans le tableau de bord PIM hello et un nouveau panneau s’ouvre avec une liste de comptes d’administrateur hello qui doit exiger l’authentification Multifacteur.  Vous pouvez exiger l’authentification Multifacteur en sélectionnant plusieurs rôles, puis sur hello **corriger** bouton, ou vous pouvez cliquez sur hello ellipses suivant tooindividual rôles, puis cliquez hello **corriger** bouton.

> [!IMPORTANT]
> Actuellement, l’authentification Multifacteur Azure ne fonctionne qu’avec un travail comptes professionnels ou scolaires, pas les comptes Microsoft (généralement un compte personnel qui a utilisé toosign dans tooMicrosoft des services tels que Skype, Xbox, Outlook.com, etc..). Pour cette raison, toute personne utilisant un compte Microsoft ne peut pas être un administrateur éligible, car ils ne peut pas utiliser l’authentification Multifacteur tooactivate leurs rôles. Si ces utilisateurs ont besoin toocontinue la gestion des charges de travail à l’aide d’un compte Microsoft, élever les toopermanent administrateurs pour l’instant.
> 
> 

En outre, vous pouvez modifier hello multifacteur pour un rôle spécifique en cliquant dessus dans hello section rôles du tableau de bord hello PIM. Ensuite, cliquez sur **paramètres** dans le panneau de rôle hello, puis en sélectionnant **activer** sous l’authentification multifacteur.

## <a name="how-azure-ad-pim-validates-mfa"></a>Validation de Multi-Factor Authentication (MFA) par Azure AD PIM
Il existe deux options pour valider l'authentification multifacteur lorsqu’un utilisateur active un rôle.

option la plus simple de Hello est toorely sur Azure MFA pour les utilisateurs qui sont activation d’un rôle privilégié. toodo, première vérification de ces utilisateurs sont concédés sous licence, si nécessaire et ont enregistré pour l’authentification Multifacteur Azure. Plus d’informations sur comment toodo il s’agit de [prise en main d’Azure multi-Factor Authentication dans le cloud de hello](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md). Il est recommandé, mais pas obligatoire, que vous configurez tooenforce Azure AD MFA pour ces utilisateurs quand ils se connectent. Il s’agit, car les vérifications de l’authentification Multifacteur hello seront effectuées par Azure AD PIM, lui-même.

Si les utilisateurs s’authentifient en local, vous pouvez également faire en sorte que votre fournisseur d’identité soit responsable de l’authentification MFA. Par exemple, si vous avez configuré Active Directory Federation Services l’authentification basée sur une carte à puce toorequire avant d’accéder à Azure AD, [sécurisation des ressources de cloud avec Azure multi-Factor Authentication et AD FS](../multi-factor-authentication/multi-factor-authentication-get-started-adfs-cloud.md) inclut des instructions Pour configurer les services AD FS toosend tooAzure de revendications AD. Quand un utilisateur tente de tooactivate un rôle, Azure AD PIM accepte que l’authentification Multifacteur a déjà été validée pour l’utilisateur de hello une fois qu’il reçoit les revendications appropriées hello.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Étapes suivantes
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

