---
title: "aaaAzure l’authentification basée sur certificat Active Directory sur iOS | Documents Microsoft"
description: "En savoir plus sur les scénarios de hello pris en charge et les exigences de hello pour la configuration de l’authentification basée sur certificat dans les solutions avec les appareils iOS"
services: active-directory
author: MarkusVi
documentationcenter: na
manager: femila
ms.assetid: 26a6fc54-0153-44fb-b970-9b432c99e9f9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 4486ff5239c2897b3bc187053f31d74807430301
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-certificate-based-authentication-on-ios"></a>Authentification par certificat Azure Active Directory sur iOS

Authentification par certificat (Services) vous permet de toobe authentifié par Azure Active Directory avec un certificat client sur un appareil Windows, Android ou iOS lors de la connexion de votre compte en ligne Exchange pour : 

* Des applications mobiles Office, telles que Microsoft Outlook et Microsoft Word ;   
* Des clients Exchange ActiveSync (EAS). 

La configuration de cette fonctionnalité évite hello besoin tooenter un nom d’utilisateur et mot de passe dans certaines applications de Microsoft Office sur votre appareil mobile et de messagerie. 

Cette rubrique vous fournit des exigences de hello et les scénarios de hello pris en charge pour la configuration des services sur un appareil iOS(Android) pour les utilisateurs de clients dans Office 365 entreprise, entreprise, éducation, du gouvernement, Chine, et plans de l’Allemagne.

Cette fonctionnalité est disponible en version préliminaire dans les plans Office 365 US Government Defense et US Government Federal.




## <a name="office-mobile-applications-support"></a>Prise en charge des applications mobiles Office

| Applications | Support |
| --- | --- |
| Application Azure Information Protection |![Vérification][1] |
| Microsoft Teams |![Vérification][1] |
| OneNote |![Vérification][1] |
| OneDrive |![Vérification][1] |
| Outlook |![Vérification][1] |
| Applications mobiles Power BI |![Vérification][1] |
| Skype Entreprise |![Vérification][1] |
| Word / Excel / PowerPoint |![Vérification][1] |
| Yammer |![Vérification][1] |


## <a name="requirements"></a>Configuration requise 

Hello version du système d’exploitation de périphérique doit être iOS 9 et versions ultérieures 

Un serveur de fédération doit être configuré.  

Microsoft Authenticator est requis pour les applications Office sur iOS.  

Pour Azure Active Directory toorevoke un certificat client, jeton d’ADFS hello doit avoir hello suivant revendications :  

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/<serialnumber>`  
  (hello le numéro de série du certificat de client hello) 
* `http://schemas.microsoft.com/2012/12/certificatecontext/field/<issuer>`  
  (chaîne hello pour émetteur hello du certificat de client hello) 

Azure Active Directory ajoute ces revendications toohello actualiser le jeton si elles sont disponibles dans le jeton d’ADFS hello (ou tout autre jeton SAML). Lorsque le jeton d’actualisation hello doit toobe validé, ces informations sont utilisées toocheck hello révocation. 

Comme meilleure pratique, mettez à jour les pages d’erreurs hello ADFS avec les éléments suivants de hello :

* spécification de Hello pour l’installation de hello Microsoft Authenticator sur iOS
* Obtenir des instructions sur la façon de tooget un certificat utilisateur. 

Pour plus d’informations, consultez [personnalisation des Pages de hello AD FS Sign-in](https://technet.microsoft.com/library/dn280950.aspx).

Certaines applications Office (avec l’authentification moderne activée) envoyer '*prompt = connexion*' tooAzure AD dans sa demande. Par défaut, Azure AD convertit ce dans hello demande tooADFS trop '*wauth = usernamepassworduri*» (demande d’authentification ADFS toodo U/P) et «*wfresh = 0*» (demande d’état de l’authentification AD FS tooignore et effectuez une nouvelle authentification) . Si vous souhaitez que l’authentification basée sur certificat tooenable pour ces applications, vous devez toomodify hello Azure AD par défaut. Simplement ensemble hello '*PromptLoginBehavior*' dans les paramètres de votre domaine fédéré trop '*désactivé*'. Vous pouvez utiliser hello [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) tooperform de l’applet de commande cette tâche :

`Set-MSOLDomainFederationSettings -domainname <domain> -PromptLoginBehavior Disabled`
  

## <a name="exchange-activesync-clients-support"></a>Prise en charge des clients Exchange ActiveSync
Sur iOS 9 ou version ultérieure, client de messagerie iOS natif hello est pris en charge. Pour toutes les autres applications Exchange ActiveSync, toodetermine si cette fonctionnalité est prise en charge, contactez le développeur de votre application.  


## <a name="next-steps"></a>Étapes suivantes

Si vous souhaitez que l’authentification par certificat tooconfigure dans votre environnement, consultez [prise en main l’authentification basée sur le certificat sur Android](active-directory-certificate-based-authentication-get-started.md) pour obtenir des instructions.


<!--Image references-->
[1]: ./media/active-directory-certificate-based-authentication-ios/ic195031.png
