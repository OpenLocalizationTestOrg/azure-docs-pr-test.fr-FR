---
title: "aaaSingle l’authentification avec le Proxy d’Application | Documents Microsoft"
description: "Décrit comment tooprovide l’authentification unique à l’aide du Proxy d’Application Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: ded0d9c9-45f6-47d7-bd0f-3f7fd99ab621
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: H1Hack27Feb2017, it-pro
ms.openlocfilehash: 0047e834cd42e057a75ebc0c5dcf860734464a05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="kerberos-constrained-delegation-for-single-sign-on-tooyour-apps-with-application-proxy"></a>La délégation contrainte Kerberos pour les applications tooyour de l’authentification unique avec le Proxy d’Application

Vous pouvez fournir l’authentification unique pour les applications locales publiées via le proxy d’application et sécurisées avec l’authentification Windows intégrée. L’accès à ces applications nécessitent un ticket Kerberos. Le Proxy d’application utilise la délégation Kerberos (KCD) toosupport ces applications. 

Vous pouvez activer les applications tooyour de l’authentification unique à l’aide de l’authentification Windows (intégrée) en attribuant l’autorisation de connecteurs de Proxy d’Application dans Active Directory tooimpersonate users. les connecteurs Hello utilisent toosend de cette autorisation et recevoir des jetons en leur nom.

## <a name="how-single-sign-on-with-kcd-works"></a>Fonctionnement de l’authentification unique avec KCD
Ce diagramme explique le flux de hello lorsqu’un utilisateur tente de tooaccess une application locale qui utilise IWA.

![Diagramme de flux de l’authentification Microsoft AAD](./media/active-directory-application-proxy-sso-using-kcd/AuthDiagram.png)

1. utilisateur de Hello passe à l’application hello URL tooaccess hello local via le Proxy d’Application.
2. Le Proxy d’application redirige hello demande tooAzure AD authentication services toopreauthenticate. À ce stade, Azure AD applique les stratégies d’authentification et d’autorisation applicables, comme l’authentification multifacteur. Si l’utilisateur de hello est validé, Azure AD crée un jeton et l’envoie toohello utilisateur.
3. Hello passe tooApplication de jeton hello Proxy.
4. Le Proxy d’application valide le jeton de hello et récupère hello nom d’utilisateur Principal (UPN) à partir de celui-ci, et puis envoie hello demande hello UPN et hello toohello de nom de Principal du Service (SPN) connecteur via un canal sécurisé doublement authentifié.
5. Hello connecteur effectue une négociation de la délégation Kerberos (KCD) avec hello local AD, l’emprunt d’identité hello utilisateur tooget une application de toohello jeton Kerberos.
6. Active Directory envoie le jeton Kerberos de hello pour hello application toohello connecteur.
7. Hello connecteur envoie hello d’origine demande toohello serveur d’applications, à l’aide du jeton Kerberos de hello que provenant d’AD.
8. application Hello envoie hello réponse toohello connecteur, qui est renvoyée au service de Proxy d’Application toohello et enfin toohello utilisateur.

## <a name="prerequisites"></a>Composants requis
Avant de commencer avec l’authentification unique pour les applications IWA, assurez-vous que votre environnement est prêt à hello suivant les paramètres et les configurations :

* Vos applications, telles que les applications SharePoint Web, sont définies toouse l’authentification Windows intégrée. Pour plus d’informations, consultez [Activer la prise en charge de l’authentification Kerberos](https://technet.microsoft.com/library/dd759186.aspx) ou, pour SharePoint, consultez [Planifier l’authentification Kerberos dans SharePoint 2013](https://technet.microsoft.com/library/ee806870.aspx).
* Toutes vos applications disposent de [Noms de principal du service](https://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spns-setspn-syntax-setspn-exe.aspx).
* hello en cours d’exécution du serveur Hello connecteur et serveur hello application hello en cours d’exécution sont joints à un domaine et une partie de hello même domaine ou domaines autorisés à approuver. Pour plus d’informations sur la jonction de domaine, consultez [joindre un domaine de tooa ordinateur](https://technet.microsoft.com/library/dd807102.aspx).
* serveur Hello hello connecteur possède un attribut TokenGroupsGlobalAndUniversal hello de tooread d’accès pour les utilisateurs. Ce paramètre par défaut peut avoir affecté par l’environnement de hello de renforcement de la sécurité.

### <a name="configure-active-directory"></a>Configurer Active Directory
configuration d’Active Directory Hello varie, selon si votre connecteur de Proxy d’Application et le serveur d’applications hello sont dans hello même domaine ou non.

#### <a name="connector-and-application-server-in-hello-same-domain"></a>Connecteur et serveur d’applications Bonjour même domaine
1. Dans Active Directory, accédez trop**outils** > **utilisateurs et ordinateurs**.
2. Sélectionnez serveur hello connecteur de hello en cours d’exécution.
3. Cliquez avec le bouton droit, puis sélectionnez **Properties** > **Délégation**.
4. Sélectionnez **n’approuver cet ordinateur pour les services uniquement de délégation toospecified**. 
5. Sous **Services toowhich ce compte peut présenter des informations d’identification déléguées** Ajouter valeur hello pour hello identité SPN hello du serveur d’applications. Ainsi, hello connecteur Proxy d’Application tooimpersonate les utilisateurs dans Active Directory par rapport aux applications hello définies dans la liste de hello.

   ![Capture d’écran de la fenêtre Propriétés du connecteur-SVR](./media/active-directory-application-proxy-sso-using-kcd/Properties.jpg)

#### <a name="connector-and-application-server-in-different-domains"></a>Le connecteur et le serveur d’application sont dans des domaines différents
1. Pour obtenir la liste des conditions préalables à l’utilisation de la délégation Kerberos contrainte entre domaines, consultez [Délégation Kerberos contrainte entre domaines](https://technet.microsoft.com/library/hh831477.aspx).
2. Hello d’utilisation `principalsallowedtodelegateto` propriété sur le Proxy d’Application hello connecteur serveur tooenable hello toodelegate pour le serveur de connecteur hello. serveur d’applications Hello `sharepointserviceaccount` et hello délégation du serveur est `connectormachineaccount`. Pour Windows 2012 R2, utilisez ce code comme exemple :

        $connector= Get-ADComputer -Identity connectormachineaccount -server dc.connectordomain.com

        Set-ADComputer -Identity sharepointserviceaccount -PrincipalsAllowedToDelegateToAccount $connector

        Get-ADComputer sharepointserviceaccount -Properties PrincipalsAllowedToDelegateToAccount

Sharepointserviceaccount peut être un compte de service sous le hello SPS pool d’applications est en cours d’exécution ou de compte d’ordinateur hello SPS.

## <a name="configure-single-sign-on"></a>Configurer l’authentification unique 
1. Publier votre application en fonction des instructions toohello décrites dans [publier des applications avec Proxy d’Application](application-proxy-publish-azure-portal.md). Assurez-vous que tooselect **Azure Active Directory** comme hello **méthode de pré-authentification**.
2. Une fois que votre application s’affiche dans la liste hello d’applications d’entreprise, sélectionnez-la et cliquez sur **l’authentification unique**.
3. Définir hello seul mode d’authentification trop**l’authentification Windows intégrée**.  
4. Entrez hello **SPN d’Application interne** hello serveur d’applications. Dans cet exemple, hello SPN pour notre application publiée est http/www.contoso.com. Cette toobe de besoins SPN dans liste hello du connecteur de hello toowhich services peut présenter des informations d’identification déléguées. 
5. Choisissez hello **identité déléguée** pour toouse de connecteur hello pour le compte de vos utilisateurs. Pour plus d’informations, consultez [Utilisation d’identités cloud et locales différentes](#Working-with-different-on-premises-and-cloud-identities)

   ![Configuration avancée des applications](./media/active-directory-application-proxy-sso-using-kcd/cwap_auth2.png)  


## <a name="sso-for-non-windows-apps"></a>Authentification unique pour les applications non Windows
Hello flux de délégation contrainte Kerberos dans le Proxy d’Application Azure AD démarre lorsque Azure AD authentifie l’utilisateur hello dans le cloud de hello. Une fois la demande de hello arrive sur site, hello Proxy d’Application Azure Active Directory connector émet un ticket Kerberos pour le compte d’utilisateur de hello en interagissant avec hello Active Directory local. Ce processus est tooas auxquels la délégation Kerberos (KCD). Bonjour la phase suivante, une demande est envoyée toohello l’application principale avec ce ticket Kerberos. Il existe plusieurs protocoles qui définissent comment toosend ces demandes. La plupart des serveurs non Windows supposent qu’il s’agit de Negotiate/SPNego, qui est maintenant pris en charge sur le proxy d’application Azure AD.

Pour plus d’informations sur Kerberos, consultez [vous souhaitez tooknow sur la délégation Kerberos (KCD)](https://blogs.technet.microsoft.com/applicationproxyblog/2015/09/21/all-you-want-to-know-about-kerberos-constrained-delegation-kcd).

Les applications non Windows utilisent en général les noms d’utilisateur ou les noms de compte SAM au lieu des adresses e-mail de domaine. Si cette situation s’applique tooyour applications, vous devez tooconfigure hello déléguée connexion identité champ tooconnect vos identités d’application cloud identités tooyour. 

## <a name="working-with-different-on-premises-and-cloud-identities"></a>Utilisation d’identités cloud et locales différentes
Le Proxy d’application part du principe que les utilisateurs ont exactement hello même identité dans le cloud de hello et sur site. Si tel n’est pas le cas de hello, vous pouvez peuvent toujours utiliser KCD pour l’authentification unique. Configurer un **déléguée identité** pour chaque toospecify application quelle identité doit être utilisée lors de l’exécution de l’authentification unique.  

Cette fonctionnalité permet à de nombreuses organisations qui ont des différents locaux et cloud identités toohave l’authentification unique à partir d’applications de site tooon hello cloud sans nécessiter de hello utilisateurs tooenter différents noms d’utilisateur et mots de passe. Cela inclut les organisations qui :

* Disposent de plusieurs domaines en interne (joe@us.contoso.com, joe@eu.contoso.com) et un domaine unique dans le cloud de hello (joe@contoso.com).
* Avoir le nom de domaine non routable en interne (joe@contoso.usa) et un juridique dans le cloud de hello.
* n’utilisent pas de noms de domaine en interne (joe) ;
* Utilisez des alias différents localement et dans le cloud de hello. Par exemple, joe-johns@contoso.com et joej@contoso.com  

Proxy d’Application, vous pouvez sélectionner le hello de tooobtain toouse identité ticket Kerberos. Ce paramètre est à configurer application par application. Certaines de ces options sont adaptées pour les systèmes qui n’acceptent pas le format d’adresse de messagerie, tandis que d’autres sont conçues pour les connexions alternatives.

![Capture d’écran du paramètre Identité de connexion déléguée](./media/active-directory-application-proxy-sso-using-kcd/app_proxy_sso_diff_id_upn.png)

Si l’identité déléguée est utilisée, hello valeur ne peut pas être unique entre tous les domaines de hello ou les forêts de votre organisation. Vous pouvez éviter ce problème en publiant ces applications deux fois à l’aide de deux groupes de connecteurs différents. Étant donné que chaque application possède une audience utilisateur différent, vous pouvez joindre son domaine différent de tooa de connecteurs.

### <a name="configure-sso-for-different-identities"></a>Configuration de l’authentification unique pour différentes identités
1. Configurer les paramètres d’Azure AD Connect identité principale de hello est l’adresse de messagerie hello (messagerie). Cette opération s’effectue comme partie de hello personnaliser le processus, en modifiant hello **nom d’utilisateur Principal** champ dans les paramètres de synchronisation hello. Ces paramètres déterminent également comment les utilisateurs du journal dans tooOffice365, les appareils Windows 10 Professionnel et d’autres applications qui utilisent Azure AD en tant que leur magasin d’identités.  
   ![Capture d’écran de l’identification des utilisateurs : liste déroulante Nom d’utilisateur principal](./media/active-directory-application-proxy-sso-using-kcd/app_proxy_sso_diff_id_connect_settings.png)  
2. Dans les paramètres de Configuration de l’Application hello pour une application hello vous aimeriez toomodify, sélectionnez hello **identité déléguée** toobe utilisé :

   * Nom d’utilisateur principal (par exemple, joe@contoso.com)
   * Nom d’utilisateur principal alternatif (par exemple, joed@contoso.local)
   * Partie correspondant au nom d’utilisateur dans le nom d’utilisateur principal (par exemple, joe)
   * Partie correspondant au nom d’utilisateur dans le nom d’utilisateur principal alternatif (par exemple, joed)
   * Nom de compte SAM local (dépend de la configuration du contrôleur de domaine hello)

### <a name="troubleshooting-sso-for-different-identities"></a>Résolution des problèmes liés à l’authentification unique pour différentes identités
S’il existe une erreur dans hello processus d’authentification unique, il apparaît dans le journal des événements hello connecteur ordinateur comme expliqué dans [dépannage](application-proxy-back-end-kerberos-constrained-delegation-how-to.md).
Toutefois, dans certains cas, demande de hello est envoyée avec succès l’application principale toohello alors que cette application répond dans divers autres réponses HTTP. Résolution des problèmes de ces cas doivent commencer en examinant le numéro d’événement 24029 sur l’ordinateur de connecteur hello dans le journal des événements session hello Proxy d’Application. identité de l’utilisateur Hello qui a été utilisée pour la délégation s’affiche dans le champ « utilisateur » de hello dans les détails de l’événement hello. tooturn sur le journal de session, sélectionnez **afficher d’analyse et les journaux de débogage** dans le menu Affichage de hello événements Observateur.

## <a name="next-steps"></a>Étapes suivantes

* [Comment tooconfigure un toouse d’application de Proxy d’Application la délégation contrainte Kerberos](application-proxy-back-end-kerberos-constrained-delegation-how-to.md)
* [Résoudre les problèmes rencontrés avec le proxy d’application](active-directory-application-proxy-troubleshoot.md)


Pour les informations les plus récentes hello et mises à jour, consultez hello [blog de Proxy d’Application](http://blogs.technet.com/b/applicationproxyblog/)

