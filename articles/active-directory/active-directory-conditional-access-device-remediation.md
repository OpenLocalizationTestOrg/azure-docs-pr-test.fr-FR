---
title: "aaaYou ne peut pas y accéder à partir de maintenant hello portail Azure à partir d’un appareil Windows | Documents Microsoft"
description: "En savoir où vous ne pouvez pas get il à partir d’ici provient et ce que vous pourriez vérifier tooavoid en cours d’exécution dans cette boîte de dialogue."
services: active-directory
keywords: "accès conditionnel en fonction de l’appareil, inscription de l’appareil, activer l’inscription de l’appareil, inscription de l’appareil et GPM"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8ad0156c-0812-4855-8563-6fbff6194174
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: eda2aa10fbff5b3e515723219f61c1cb6f634e29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="you-cant-get-there-from-here-on-a-windows-device"></a>Problèmes d’accès aux ressources sur un appareil Windows

Par exemple, lors d’une tentative d’accès à l’intranet SharePoint Online de votre organisation, vous pouvez rencontrer une page indiquant que *vous ne pouvez pas y accéder à partir de votre emplacement*. Vous voyez cette page, car votre administrateur a configuré une stratégie d’accès conditionnel qui empêche les ressources de l’organisation accès tooyour sous certaines conditions. Bien qu’il soit nécessaire toocontact technique ou votre tooget administrateur résoudre ce problème, il existe quelques éléments, que vous pouvez essayer par vous-même, tout d’abord.

Si vous utilisez un **Windows** appareil, vous devez vérifier hello suivant :

- Le navigateur que vous utilisez est-il pris en charge ?

- Votre appareil exécute-t-il une version prise en charge de Windows ?

- Votre appareil est-il conforme ?






## <a name="supported-browser"></a>Navigateur pris en charge

Si votre administrateur a configuré une stratégie d’accès conditionnel, vous pouvez uniquement accéder aux ressources de votre organisation à l’aide d’un navigateur pris en charge. Sur un appareil Windows, seuls **Internet Explorer** et **Edge** sont pris en charge.

Vous pouvez facilement identifier si vous ne peut pas accéder à une ressource en raison de navigateur non pris en charge de tooan en consultant la section des détails de la page d’erreur hello hello :

![Messages d’accès refusé aux navigateurs non pris en charge](./media/active-directory-conditional-access-device-remediation/02.png "Scénario")

mise à jour de la seule Hello est toouse un navigateur qui prend en charge de l’application hello pour votre plateforme d’appareils. Pour obtenir une liste complète des navigateurs pris en charge, consultez la liste des [navigateurs pris en charge](active-directory-conditional-access-supported-apps.md#supported-browsers-for-device-based-policies).  


## <a name="supported-versions-of-windows"></a>Versions de Windows prises en charge

suivant de Hello doit être remplies sur le système de d’exploitation Windows hello sur votre appareil : 

- Si vous exécutez un système d’exploitation Windows sur votre appareil, il doit toobe Windows 7 ou version ultérieure.
- Si vous exécutez un système d’exploitation Windows sur votre appareil, il doit toobe Windows Server 2008 R2 ou version ultérieure. 


## <a name="compliant-device"></a>Conformité de l’appareil

Votre administrateur peut avoir configuré une stratégie d’accès conditionnel qui permet aux ressources de l’organisation de tooyour accès uniquement à partir d’appareils conformes. Active Directory local toobe conforme, que votre appareil doit être soit joint tooyour ou joint tooyour Azure Active Directory.

Vous pouvez facilement identifier si vous ne pouvez pas accéder à une ressource en raison de l’appareil tooa qui n’est pas conforme en examinant la section des détails de la page d’erreur hello hello :
 
![Messages d’accès refusé aux appareils non enregistrés](./media/active-directory-conditional-access-device-remediation/01.png "Scénario")


### <a name="is-your-device-joined-tooan-on-premises-active-directory"></a>Est votre tooan appareil joint sur le site Active Directory ?

**Si votre appareil est joint tooan locale Active Directory dans votre organisation :**

1. Assurez-vous que vous vous connectez tooWindows à l’aide de votre compte professionnel (votre compte Active Directory).
2. Se connecter tooyour de réseau d’entreprise via un réseau privé virtuel (VPN) ou un DirectAccess.
3. Une fois que vous êtes connecté, appuyez sur touche du logo Windows hello + toolock de clé hello L votre session Windows.
4. Déverrouillez votre session Windows en saisissant les informations d’identification de votre compte de travail.
5. Patientez une minute et réessayez tooaccess hello application ou service.
6. Si vous voyez hello même page, cliquez sur hello **plus de détails** lier, puis contactez votre administrateur avec des détails de hello.


### <a name="is-your-device-not-joined-tooan-on-premises-active-directory"></a>Est votre tooan appareil ne joint pas sur le site Active Directory ?

Si votre appareil n’est pas joint tooan Active Directory local et exécute Windows 10, vous avez deux options :

* Exécuter Azure AD Join
* Ajouter votre travail ou d’établissement scolaire tooWindows de compte

Pour plus d’informations sur les différences entre ces options, consultez la section [Utilisation d’appareils Windows 10 sur votre lieu de travail](active-directory-azureadjoin-windows10-devices.md).  
Ainsi :

- Appartient tooyour organisation, vous devez exécuter Azure AD Join.
- Est un périphérique personnel ou un appareil Windows phone, vous devez ajouter votre travail ou scolaire tooWindows de compte 



#### <a name="azure-ad-join-on-windows-10"></a>Exécution de l’option Azure AD Join sur Windows 10

Hello toojoin étapes votre tooAzure DISPOSITIF AD sont liés version hello de Windows 10 en cours d’exécution sur ce dernier. version de hello toodetermine de votre système d’exploitation Windows 10, exécutez hello **winver** commande : 

![Version de Windows](./media/active-directory-conditional-access-device-remediation/03.png )


**Mise à jour anniversaire Windows 10 (version 1607) :**

1. Ouvrez hello **paramètres** application.
2. Cliquez sur **Comptes** > **Access work or school** (Accès professionnel ou scolaire).
3. Cliquez sur **Connecter**.
4. Cliquez sur **joindre cette tooAzure appareil AD**.
5. Authentifier tooyour organisation, fournir une authentification multifacteur si vous y êtes invité, puis suivez les étapes de hello sont affichés.
6. Déconnectez-vous puis reconnectez-vous à l’aide de votre compte professionnel.
7. Essayez à nouveau l’application de hello tooaccess.

**Mise à jour Windows 10 de novembre 2015 (version 1511) :**

1. Ouvrez hello **paramètres** application.
2. Cliquez sur **Système** > **À propos de**.
3. Cliquez sur **Joindre Azure AD**.
4. Authentifier tooyour organisation, fournir une authentification multifacteur si vous y êtes invité, puis suivez les étapes de hello sont affichés.
5. Déconnectez-vous et reconnectez-vous à l’aide de votre compte professionnel (votre compte Azure AD).
6. Essayez à nouveau l’application de hello tooaccess.


#### <a name="workplace-join-on-windows-81"></a>Workplace Join pour Windows 8.1

Si votre appareil n’est pas joint au domaine et exécutant Windows 8.1, toodo une jonction et s’inscrire à Microsoft Intune, procédez comme hello comme suit :

1. Ouvrez **Paramètres du PC**.
2. Cliquez sur **Réseau** > **Espace de travail**.
3. Cliquez sur **Joindre**.
4. Authentifier tooyour organisation, fournir une authentification multifacteur si vous y êtes invité, puis suivez les étapes de hello sont affichés.
5. Cliquez sur **Activer**.
6. Essayez à nouveau l’application de hello tooaccess.



#### <a name="add-your-work-or-school-account-toowindows"></a>Ajouter votre travail ou d’établissement scolaire tooWindows de compte 


**Mise à jour anniversaire Windows 10 (version 1607) :**

1. Ouvrez hello **paramètres** application.
2. Cliquez sur **Comptes** > **Access work or school** (Accès professionnel ou scolaire).
3. Cliquez sur **Connecter**.
4. Authentifier tooyour organisation, fournir une authentification multifacteur si vous y êtes invité, puis suivez les étapes de hello sont affichés.
5. Essayez à nouveau l’application de hello tooaccess.


**Mise à jour Windows 10 de novembre 2015 (version 1511) :**

1. Ouvrez hello **paramètres** application.
2. Cliquez sur **Comptes** > **Vos comptes**.
3. Cliquez sur **Ajouter un compte professionnel ou scolaire**.
4. Authentifier tooyour organisation, fournir une authentification multifacteur si vous y êtes invité, puis suivez les étapes de hello sont affichés.
5. Essayez à nouveau l’application de hello tooaccess.





## <a name="next-steps"></a>Étapes suivantes
[Accès conditionnel Azure Active Directory](active-directory-conditional-access.md)

