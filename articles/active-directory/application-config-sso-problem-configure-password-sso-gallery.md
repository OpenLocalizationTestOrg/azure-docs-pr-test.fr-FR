---
title: "aaaProblem configuration de mot de passe l’authentification unique pour une application Azure AD galerie | Documents Microsoft"
description: "Comprendre le cadran de personnes hello courantes des problèmes lors de la configuration de mot de passe Single Sign-on pour les applications qui figurent déjà dans hello Galerie d’applications Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 78c37c52453c375bf7ccbca6df5c9008be4ce642
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-password-single-sign-on-for-an-azure-ad-gallery-application"></a>Problème de configuration de l’authentification unique avec mot de passe pour une application de la galerie Azure AD

Cet article vous a-t-il face de personnes toounderstand hello courantes des problèmes lors de la configuration **mot de passe Single Sign-on** avec une application de la galerie d’Azure AD.

## <a name="credentials-are-filled-in-but-hello-extension-does-not-submit-them"></a>Informations d’identification sont renseignées, mais les extension hello ne présente pas les

Cela se produit généralement si le fournisseur de l’application hello a changé sa connexion dans la page récemment tooadd un champ, modifier un identificateur sous-jacent que nous utilisons des champs de nom d’utilisateur et mot de passe de hello toodetect ou modifier la connexion hello fonctionnement de l’expérience d’application. Heureusement, dans de nombreux cas, Microsoft peut travailler avec application fournisseurs toorapidly résoudre ces problèmes.

Alors que Microsoft a technologies tooautomatically détecter lorsque ces intégrations interrompre, mais parfois, nous ne sommes pas en mesure de toofind ces problèmes droite absent ou prendre un certain temps toofix. Dans le cas de hello lorsqu’une de ces intégrations ne fonctionne pas correctement, nous souhaiterions si vous avez ouvert un cas de support afin de pouvoir le corriger aussi rapidement que possible.

En outre toothis, **si vous êtes en contact avec le fournisseur de l’application,** **les envoyer notre comme** afin de nous pouvons utiliser toonatively intégrer leurs applications avec Azure Active Directory. Vous pouvez envoyer hello fournisseur toohello [répertorier votre application dans la galerie d’applications Azure Active Directory hello](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) tooget les a démarré.

## <a name="credentials-are-filled-in-and-submitted-but-hello-page-indicates-hello-credentials-are-incorrect"></a>Informations d’identification sont remplies et soumises, mais la page de hello indique hello sont incorrectes

tooresolve ce problème, premier suivant hello de vérification :

-   Avoir les utilisateur hello commencent par essayer de trop**vous connecter directement dans le site Web d’applications toohello** avec informations d’identification hello stockées pour les.

  * Si cela fonctionne, puis demandez à hello utilisateur cliquez sur hello **mettre à jour les informations d’identification** bouton sur hello **vignette** Bonjour **applications** section Hello [Application Accéder au panneau](https://myapps.microsoft.com/) tooupdate les toohello connu de dernière utilisation du nom d’utilisateur et mot de passe.

   * Si vous, ou un autre administrateur affecté hello pour cet utilisateur, trouver les utilisateur hello ou assignation d’application du groupe en naviguant toohello **utilisateurs et groupes** onglet de l’application hello, en sélectionnant l’attribution hello et en cliquant sur hello **informations d’identification de la mise à jour** bouton.

-   Si les utilisateurs hello attribué leurs propres informations d’identification, disposent d’utilisateur de hello **vérifier toobe assurer que leur mot de passe n’a pas expiré dans l’application hello** et dans ce cas, **mettre à jour le mot de passe expiré** en vous connectant toohello application directement.

   * Une fois le mot de passe hello a été mis à jour dans l’application hello, demander hello de hello utilisateur tooclick **mettre à jour les informations d’identification** bouton sur hello **vignette** Bonjour **applications** section de hello [volet d’accès Application](https://myapps.microsoft.com/) tooupdate les toohello connu de dernière utilisation du nom d’utilisateur et mot de passe.

   * Si vous, ou un autre administrateur affecté hello pour cet utilisateur, trouver les utilisateur hello ou assignation d’application du groupe en naviguant toohello **utilisateurs et groupes** onglet de l’application hello, en sélectionnant l’attribution hello et en cliquant sur hello **informations d’identification de la mise à jour** bouton.

-   Avoir hello mise à jour de hello utilisateur accès panneau une extension de navigateur en suivant les étapes de hello ci-dessous Bonjour [comment tooinstall hello extension du navigateur de panneau d’accès](#how-to-install-the-access-panel-browser-extension) section.

-   Assurez-vous que l’extension du navigateur hello accès Panneau de configuration est en cours d’exécution et activés dans votre navigateur.

-   Assurez-vous que vos utilisateurs n’essaient pas de toosign dans l’application toohello à partir du panneau d’accès hello lors de **mode privé, inPrivate ou incognito**. extension de panneau d’accès Hello n’est pas pris en charge dans ces modes.

Dans le cas où cela ne fonctionne pas, il peut être cas hello qu’une modification a été côté hello application qui a été temporairement endommagé d’intégration de l’application hello à Azure AD. Par exemple, cela peut se produire lorsque le fournisseur de l’application hello introduit un script dans leur page qui se comporte différemment de recalcul manuel et automatisé d’entrée, ce qui entraîne l’automatisée d’intégration, telles que notre propre, toobreak. Heureusement, dans de nombreux cas, Microsoft peut travailler avec application fournisseurs toorapidly résoudre ces problèmes.

Alors que Microsoft a technologies tooautomatically détecter lorsque ces intégrations interrompre, mais parfois, nous ne sommes pas en mesure de toofind ces problèmes droite absent ou prendre un certain temps toofix. Dans le cas de hello lorsqu’une de ces intégrations ne fonctionne pas correctement, nous souhaiterions si vous avez ouvert un cas de support afin de pouvoir le corriger aussi rapidement que possible.

En outre toothis, **si vous êtes en contact avec le fournisseur de l’application,** **les envoyer notre comme** afin de nous pouvons utiliser toonatively intégrer leurs applications avec Azure Active Directory. Vous pouvez envoyer hello fournisseur toohello [répertorier votre application dans la galerie d’applications Azure Active Directory hello](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) tooget les a démarré.

## <a name="hello-extension-works-in-chrome-and-firefox-but-not-in-internet-explorer"></a>extension de Hello fonctionne dans Chrome et Firefox, mais pas dans Internet Explorer

Il existe deux causes principales toothis problème :

-   En fonction des paramètres de sécurité hello activés dans Internet Explorer, si le site Web de hello n’est pas dans le cadre d’un **approuvés**, parfois notre script bloquée à partir de l’exécution pour une application hello.

  *  tooresolve, demander à utilisateur de hello trop**ajouter le site Web de l’application hello** toohello **Sites de confiance** liste au sein de leurs **les paramètres de sécurité Internet Explorer**. Vous pouvez envoyer votre toohello utilisateurs [comment tooadd un toomy site approuvé sites liste](https://answers.microsoft.com/en-us/ie/forum/ie9-windows_7/how-do-i-add-a-site-to-my-trusted-sites-list/98cc77c8-b364-e011-8dfc-68b599b31bf5) article pour obtenir des instructions détaillées.

-   Dans de rares circonstances, validation de la sécurité d’Internet Explorer peut parfois provoquer tooload de page hello plus lentement que l’exécution de hello de notre script.

   * Malheureusement, cette situation peut varier selon la version du navigateur hello, vitesse de votre ordinateur ou site visité. Dans ce cas, nous vous suggérons de que vous contactez le support technique afin que nous corrigions intégration hello pour cette application spécifique.

En outre toothis, **si vous êtes en contact avec le fournisseur de l’application,** **les envoyer notre comme** afin de nous pouvons utiliser toonatively intégrer leurs applications avec Azure Active Directory. Vous pouvez envoyer hello fournisseur toohello [répertorier votre application dans la galerie d’applications Azure Active Directory hello](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) tooget les a démarré.

## <a name="check-if-hello-applications-login-page-has-changed-recently-or-requires-an-additional-field"></a>Vérifiez si hello page de connexion de l’application a été modifié récemment ou requiert un champ supplémentaire

Si la page de connexion de l’application hello a changé considérablement, cela entraîne parfois notre toobreak intégrations. Un exemple est un fournisseur de l’application ajoute une connexion dans le champ, un test captcha, ou l’authentification multifacteur tootheir rencontre. Heureusement, dans de nombreux cas, Microsoft peut travailler avec application fournisseurs toorapidly résoudre ces problèmes.

Alors que Microsoft a technologies tooautomatically détecter lorsque ces intégrations interrompre, mais parfois, nous ne sommes pas en mesure de toofind ces problèmes immédiatement. Dans le cas contraire, ils prennent certains toofix de temps. Dans le cas de hello lorsqu’une de ces intégrations ne fonctionne pas correctement, nous souhaiterions ouverture d’un cas de support afin de pouvoir le corriger aussi rapidement que possible.

En outre toothis, **si vous êtes en contact avec le fournisseur de l’application,** **les envoyer notre comme** afin de nous pouvons utiliser toonatively intégrer leurs applications avec Azure Active Directory. Vous pouvez envoyer hello fournisseur toohello [répertorier votre application dans la galerie d’applications Azure Active Directory hello](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) tooget les a démarré.

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a>Comment tooinstall hello extension du navigateur de panneau d’accès

tooinstall hello extension du navigateur de panneau d’accès, suivez les étapes de hello ci-dessous :

1.  Ouvrez hello [volet d’accès](https://myapps.microsoft.com) dans un des navigateurs de hello pris en charge et vous connecter en tant qu’un **utilisateur** dans Azure AD.

2.  Cliquez sur un **application d’authentification unique du mot de passe** Bonjour panneau d’accès.

3.  Dans hello invite vous demandant tooinstall hello logiciel, sélectionnez **installer maintenant**.

4.  En fonction de votre navigateur vous être lien de téléchargement toohello dirigée. **Ajouter** navigateur de tooyour extension hello.

5.  Si votre navigateur vous invite à sélectionner tooeither **activer** ou **autoriser** hello extension.

6.  Une fois l’extension installée, **redémarrez** votre session de navigateur.

7.  Connectez-vous en hello volet d’accès et de voir si vous pouvez **lancer** vos applications SSO de mot de passe

Vous pouvez également télécharger l’extension de hello pour Chrome et Firefox à partir de liens directs de hello ci-dessous :

-   [Extension du volet d’accès pour Chrome](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Extension du volet d’accès pour Firefox](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="next-steps"></a>Étapes suivantes
[Fournissent des applications de tooyour de l’authentification unique avec le Proxy d’Application](active-directory-application-proxy-sso-using-kcd.md)

