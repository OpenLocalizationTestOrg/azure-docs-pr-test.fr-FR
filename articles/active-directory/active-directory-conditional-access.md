---
title: "accès aaaConditional Bonjour portail classique Azure | Documents Microsoft"
description: "Utilisez le contrôle d’accès conditionnel dans hello toocheck de portail classique Azure pour des conditions spécifiques lors de l’authentification pour accès tooapplications."
services: active-directory
keywords: "tooapps d’accès conditionnel, l’accès conditionnel avec Azure AD, sécuriser l’accès aux ressources toocompany, les stratégies d’accès conditionnel"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: da3f0a44-1399-4e0b-aefb-03a826ae4ead
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/07/2017
ms.author: markvi
ms.reviewer: calebb
ms.custom: oldportal
ms.openlocfilehash: 049bd3f6ec9e35479319ee7608b007b9a1e16647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-in-hello-azure-classic-portal"></a>Accès conditionnel dans hello portail Azure classic

Cette rubrique concerne l’accès conditionnel dans hello portail Azure classic. Pour hello toutes dernières informations sur l’accès conditionnel Bonjour Azure Active Directory, consultez [accès conditionnel dans Azure Active Directory](active-directory-conditional-access-azure-portal.md).


fonctionnalités de contrôle Hello l’accès conditionnel Azure Active Directory (Azure AD) offrent des moyens simples toohelp des ressources sécurisées dans le cloud de hello et sur site. Stratégies d’accès conditionnel telles que l’authentification multifacteur peut vous protéger contre les risques de hello de vol et les informations d’identification récoltées. D’autres stratégies d’accès conditionnel peuvent vous aider à protéger les données de votre organisation. Par exemple, en outre les informations d’identification toorequiring vous peut-être une stratégie que seuls les appareils qui sont inscrits dans un système de gestion des appareils mobiles tels que Microsoft Intune peut accéder aux services sensibles de votre organisation.

## <a name="prerequisites"></a>Composants requis
L’accès conditionnel Azure AD est une fonctionnalité [Azure Active Directory Premium](http://www.microsoft.com/identity). Tous les utilisateurs accédant à une application limitée par des stratégies d’accès conditionnel doivent disposer d’une licence Azure AD Premium. Pour en savoir plus sur les conditions requises de licence, consultez l’article [Rapport d’utilisation sans licence](https://aka.ms/utc5ix).

## <a name="how-is-conditional-access-control-enforced"></a>Comment est appliqué le contrôle d’accès conditionnel ?
Avec le contrôle d’accès conditionnel en place, Azure AD vérifie pour des conditions spécifiques hello que vous définissez pour un utilisateur tooaccess une application. Une fois que les conditions d’accès sont remplies, utilisateur de hello est authentifié et peut accéder à application hello.  

![Présentation de l’accès conditionnel](./media/active-directory-conditional-access/conditionalaccess-overview.png)

## <a name="conditions"></a>Conditions
Voici les conditions que vous pouvez inclure dans une stratégie d’accès conditionnel :

* **Appartenance au groupe**. Contrôlez l’accès d’un utilisateur selon l’appartenance à un groupe.
* **Emplacement**. Utilisez emplacement hello hello tootrigger multi-Factor d’authentification des utilisateurs et les contrôles de bloc lorsqu’un utilisateur n’est pas sur un réseau approuvé.
* **Plate-forme d’appareil**. Utiliser la plateforme d’appareil hello, telles qu’iOS, Android, Windows Mobile ou Windows, comme condition pour appliquer la stratégie.
* **Appareil activé**. Le statut de l’appareil, activé ou désactivé, est validé au cours de l’évaluation de la stratégie d’appareil. Si vous désactivez un appareil perdu ou volé dans le répertoire de hello, il peut n’est plus satisfaire les exigences de la stratégie.
* **Risque utilisateur et à la connexion**. Vous pouvez utiliser [Azure AD Identity Protection](active-directory-identityprotection.md) pour les stratégies de risque d’accès conditionnel. Les stratégies de risque d’accès conditionnel permettent d’offrir à votre organisation une protection avancée, en fonction des évènements à risque et des activités de connexion inhabituelles.

## <a name="controls"></a>Commandes
Il s’agit des contrôles que vous pouvez utiliser une stratégie d’accès conditionnel de tooenforce :

* **Authentification multifacteur**. Grâce à l’authentification multifacteur, vous pouvez appliquer une authentification renforcée. Vous pouvez utiliser l’authentification multifacteur avec Azure Multi-Factor Authentication ou via un fournisseur d’authentification multifacteur local, combiné aux services de fédération Active Directory (AD FS). À l’aide de l’authentification multifacteur permet de protéger des ressources soit accessible par un utilisateur non autorisé peut avoir accédé toohello les informations d’identification d’un utilisateur valide.
* **Bloquer**. Vous pouvez appliquer des conditions telles que l’accès utilisateur emplacement tooblock utilisateur. Vous pouvez, par exemple, bloquer l’accès à un utilisateur qui ne se trouve pas sur un réseau approuvé.
* **Appareils conformes**. Vous pouvez définir des stratégies d’accès conditionnel au niveau du périphérique hello. Vous pouvez définir une stratégie de façon que seuls les ordinateurs joints à un domaine ou seuls les appareils mobiles inscrits dans une application de gestion des appareils mobiles puissent accéder aux ressources de votre organisation. Par exemple, vous pourrez utiliser la conformité des appareils Intune toocheck et puis signaler tooAzure AD pour l’application lors de l’utilisateur de hello tente tooaccess une application. Pour obtenir des instructions détaillées sur comment les applications tooprotect toouse Intune et les données, consultez [protéger les données avec Microsoft Intune et les applications](https://docs.microsoft.com/intune/deploy-use/protect-apps-and-data-with-microsoft-intune). Vous pouvez également utiliser protection des données tooenforce Intune pour les appareils perdus ou volés. Pour plus d’informations, consultez [Protection de vos données avec effacement complet ou sélectif à l’aide de Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/use-remote-wipe-to-help-protect-data-using-microsoft-intune).

## <a name="applications"></a>Applications
Vous pouvez appliquer une stratégie d’accès conditionnel au niveau de l’application hello. Définir les niveaux d’accès pour les applications et services dans le cloud de hello ou localement. stratégie de Hello est appliquée directement toohello site ou service. stratégie de Hello est appliquée pour l’accès toohello navigateur et tooapplications qui accèdent aux services de hello.

## <a name="device-based-conditional-access"></a>Accès conditionnel basé sur les appareils
Vous pouvez restreindre l’accès tooapplications à partir d’appareils qui sont inscrits auprès d’Azure AD, et qui remplissent des conditions spécifiques. Accès conditionnel basés sur l’appareil protège les ressources d’une organisation d’utilisateurs qui essaient de ressources de hello tooaccess à partir de :

* Appareils inconnus ou non gérés.
* Appareils qui ne répondent pas aux stratégies de sécurité hello votre organisation à configurer.

Vous pouvez définir des stratégies en fonction des exigences suivantes :

* **Appareils joints à un domaine**. Définir un toodevices d’accès de toorestrict stratégie qui appartiennent à un domaine d’Active Directory tooan jointes localement, et qui sont également inscrits auprès d’Azure AD. Cette stratégie s’applique tooWindows bureaux, ordinateurs portables et tablettes de l’entreprise.
  Pour plus d’informations sur la façon tooset d’inscription automatique des appareils de joints à un domaine auprès d’Azure AD, consultez [configurer l’inscription automatique des périphériques joints au domaine de Windows avec Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).
* **Appareils conformes**. Définir un toodevices d’accès toorestrict stratégie marqués **conforme** dans le répertoire du système de gestion hello. Cette stratégie garantit que seuls les appareils qui répondent aux stratégies de sécurité, comme le chiffrement des fichiers sur l’appareil, ont droit à l’accès. Vous pouvez utiliser cet accès toorestrict de stratégie à partir de hello suivant des appareils :
  
  * **Appareils Windows joints à un domaine**. Géré par System Center Configuration Manager (dans la branche active de hello) déployé dans une configuration hybride.
  * **Appareils personnels ou professionnels Windows 10 Mobile**. Appareils gérés par Intune ou par un système de gestion d’appareils mobiles tiers pris en charge.
  * **Appareils iOS et Android**. Appareils gérés par Intune.

Les utilisateurs qui accèdent aux applications qui sont protégées par basée sur un appareil, stratégie d’autorité de certification doit accéder à application hello à partir d’un appareil qui répond aux critères de cette stratégie. L’accès est refusé s’il a été effectué sur un appareil qui ne respecte pas les conditions requises de la stratégie.

Pour plus d’informations sur comment tooconfigure des périphériques, stratégie d’autorité de certification dans Azure AD, consultez [définir la stratégie d’accès conditionnel basés sur un appareil pour applications connectées Azure Active Directory](active-directory-conditional-access-policy-connected-applications.md).

## <a name="resources"></a>Ressources
Consultez hello suivant ressource catégories et les articles toolearn plus sur la définition de l’accès conditionnel pour votre organisation.

### <a name="multi-factor-authentication-and-location-policies"></a>Stratégies basées sur l’emplacement et l’authentification multifacteur
* [Prise en main avec les applications d’AD connectés tooAzure accès conditionnel basées sur le groupe, l’emplacement et les stratégies d’authentification multifacteur](active-directory-conditional-access-azuread-connected-apps.md)
* [Applications et navigateurs pris en charge](active-directory-conditional-access-supported-apps.md)

### <a name="device-based-conditional-access"></a>Accès conditionnel basé sur les appareils
* [Définir la stratégie d’accès conditionnel basés sur l’appareil pour l’accès contrôle tooAzure connecté à Active Directory applications](active-directory-conditional-access-policy-connected-applications.md)
* [Configuration de l’inscription automatique auprès d’Azure Active Directory d’appareils Windows joints à un domaine](active-directory-conditional-access-automatic-device-registration-setup.md)
* [Résolution des problèmes d’accès Azure Active Directory](active-directory-conditional-access-device-remediation.md)
* [Protégez vos données avec la réinitialisation complète ou sélective à l’aide de Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/use-remote-wipe-to-help-protect-data-using-microsoft-intune)

### <a name="protect-resources-based-on-sign-in-risk"></a>Protection des ressources en fonction d’un risque à la connexion
* [Azure AD Identity Protection](active-directory-identityprotection.md)

### <a name="next-steps"></a>Étapes suivantes
* [Conditional access FAQs (Forums Aux Questions sur l’accès conditionnel)](active-directory-conditional-faqs.md)
* [Référence technique](active-directory-conditional-access-technical-reference.md)

