---
title: "les applications aaaConditional accès local tooon - Azure AD | Documents Microsoft"
description: "Décrit comment tooset accès conditionnel pour les applications que vous publiez toobe accédé à distance à l’aide de Proxy d’Application Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 2e97722b-eb4e-4078-b607-9fed210d8a0f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 7bed25dd4ba17941e77d8c4b2b9ba4edcf0cf597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-conditional-access-in-azure-ad-application-proxy"></a>Utilisation de l’accès conditionnel dans le proxy d’application Azure AD

>[!NOTE]
>Cet article s’applique toohello portail Azure classic, ce qui a été supprimée. Nous vous recommandons d’utiliser hello [portail Azure](https://portal.azure.com). Bonjour portail Azure, les applications ont le Proxy d’Application hello mêmes fonctionnalités d’accès conditionnel comme toute autre application SaaS. toolearn en savoir plus sur l’accès conditionnel, consultez [prise en main avec un accès conditionnel dans Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).

Vous pouvez configurer l’accès tooapplications d’accès conditionnel règles toogrant publiée à l’aide de Proxy d’Application. Vous pouvez ainsi effectuer les opérations suivantes :

* Exiger l’authentification multifacteur par application.
* Exiger l’authentification multifacteur uniquement quand les utilisateurs se trouvent à l’extérieur de l’entreprise.
* Empêcher les utilisateurs d’accéder à application hello lorsqu’ils ne sont pas au travail

Ces règles peuvent être appliquées tooall utilisateurs et groupes ou uniquement toospecific utilisateurs et groupes. Par défaut, règle de hello applique tooall les utilisateurs qui ont accès toohello application. Toutefois les règle hello peuvent également être restreint toousers qui sont membres de groupes de sécurité spécifiés.  

Les règles d’accès sont évaluées lorsqu’un utilisateur accède à une application fédérée qui utilise OAuth 2.0, OpenID Connect, SAML ou WS-Federation. En outre, les règles d’accès sont évaluées avec OAuth 2.0 et OpenID Connect lorsqu’un jeton d’actualisation est tooacquire utilisé un jeton d’accès.

## <a name="conditional-access-prerequisites"></a>Conditions préalables d'accès conditionnel
* Abonnement tooAzure Active Directory Premium
* Un locataire Azure Active Directory fédéré ou géré
* Les clients fédérés requièrent l’authentification multifacteur (MFA)  
    ![Configurer des règles d’accès - imposer l’authentification multifacteur](./media/active-directory-application-proxy-conditional-access/application-proxy-conditional-access.png)

## <a name="configure-per-application-multi-factor-authentication"></a>Configurer l'authentification multifacteur pour chaque application
1. Connectez-vous en tant qu’administrateur Bonjour portail Azure classic.
2. TooActive active, sélectionnez le répertoire hello dans lequel vous souhaitez tooenable Proxy d’Application.
3. Cliquez sur **Applications** et faites défiler toohello **les règles d’accès** section. section de règles d’accès Hello s’affiche uniquement pour les applications publiées à l’aide du Proxy d’Application qui utilisent l’authentification fédérée.
4. Activer la règle de hello en sélectionnant **activer les règles d’accès** trop**sur**.
5. Spécifiez hello utilisateurs et groupes toowhom hello règles s’appliquent. Hello d’utilisation **ajouter un groupe** bouton tooselect un ou plusieurs groupes toowhich hello accès règle s’applique. Cette boîte de dialogue peut également être utilisé tooremove sélectionné groupes.  Lorsque les règles de hello sont toogroups de tooapply sélectionné, les règles d’accès hello sont appliquées uniquement pour les utilisateurs qui appartiennent tooone Hello spécifié les groupes de sécurité.  

   * tooexplicitly exclure les groupes de sécurité à partir de la règle de hello, vérifiez **sauf** et spécifiez un ou plusieurs groupes. Les utilisateurs qui sont membres d’un groupe Bonjour à l’exception de liste ne sont pas l’authentification multifacteur tooperform requis.  
   * Si un utilisateur a été configuré à l’aide de la fonctionnalité de l’authentification multifacteur hello par utilisateur, ce paramètre est prioritaire sur hello règles d’authentification multifacteur d’application. Un utilisateur qui a été configuré pour l’authentification multifacteur par utilisateur est l’authentification multifacteur tooperform requis, même si elles ont été exemptés de règles de l’authentification multifacteur de l’application hello. En savoir plus sur [l’authentification multifacteur et sur les paramètres pour chaque utilisateur](../multi-factor-authentication/multi-factor-authentication.md).
6. Sélectionnez hello accès règle tooset :

   * **Exiger l’authentification multifacteur**: utilisateurs d’appliquent des règles d’accès toowhom sont l’authentification multifacteur toocomplete requis avant l’accès aux hello application toowhich hello règle s’applique.
   * **Exiger une authentification multifacteur en déplacement**: les utilisateurs qui tentent d’application de hello tooaccess à partir d’une adresse IP approuvée ne sera pas l’authentification multifacteur tooperform requis. Hello approuvés de plages d’adresses IP peuvent être configurés sur la page Paramètres de l’authentification multifacteur hello.
   * **Bloquer l’accès à l’extérieur de travail**: les utilisateurs qui tentent de tooaccess hello application en dehors de votre réseau d’entreprise ne sera pas d’application de hello en mesure de tooaccess.

## <a name="configuring-mfa-for-federation-services"></a>Configuration de l'authentification multifacteur pour les services de fédération
Pour les clients fédérés, l’authentification multifacteur (MFA) peut être effectuée par Azure Active Directory ou par hello serveur AD FS local. Par défaut, l’authentification multifacteur (MFA) a lieu sur n’importe quelle page hébergée par Azure Active Directory. tooconfigure l’authentification Multifacteur en local, exécutez Windows PowerShell et utilisez hello – SupportsMFA propriété tooset hello module Azure AD.

Hello suivant montre comment tooenable localement l’authentification Multifacteur à l’aide de hello [applet de commande Set-MsolDomainFederationSettings](https://msdn.microsoft.com/library/azure/dn194088.aspx) sur le client de hello contoso.com :`Set-MsolDomainFederationSettings -DomainName contoso.com -SupportsMFA $true `

Dans Ajout toosetting cet indicateur, instance de client fédéré ADFS hello doit être configuré l’authentification multifacteur tooperform. Suivez les instructions de hello pour [déploiement Microsoft Azure multi-Factor authentication local](../multi-factor-authentication/multi-factor-authentication-get-started-server.md).

## <a name="see-also"></a>Voir aussi
* [Utiliser des applications utilisant les revendications](active-directory-application-proxy-claims-aware-apps.md)
* [Publiez des applications avec le proxy d’application](active-directory-application-proxy-publish.md)
* [Activer l’authentification unique](active-directory-application-proxy-sso-using-kcd.md)
* [Publier des applications avec votre propre nom de domaine](active-directory-application-proxy-custom-domains.md)

Pour les informations les plus récentes hello et mises à jour, consultez hello [blog de Proxy d’Application](http://blogs.technet.com/b/applicationproxyblog/)
