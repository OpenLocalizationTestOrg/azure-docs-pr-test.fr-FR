---
title: aaaConfigure Azure AD SSO pour les applications | Documents Microsoft
description: "Découvrez comment tooself service vous connecter tooAzure d’applications Active Directory à l’aide de SAML et mot de passe de l’authentification unique"
services: active-directory
author: asmalser-msft
documentationcenter: na
manager: femila
ms.assetid: 0d42eb0c-6d3f-4557-9030-e88e86709a19
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: asmalser
ms.reviewer: luleon
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 002a19a6c7ad25ea2f3b9c6a7c7874ed2be23cce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-single-sign-on-tooapplications-that-are-not-in-hello-azure-active-directory-application-gallery"></a>Configuration uniques tooapplications ouverture de session qui ne sont pas dans la galerie d’applications Azure Active Directory hello
Cet article porte sur une fonctionnalité qui permet aux administrateurs tooconfigure unique authentification tooapplications ne figure pas dans la galerie d’applications Azure Active Directory hello *sans écrire de code*. Cette fonctionnalité a été publiée à partir de la version d’évaluation technique le 18 novembre 2015 et est incluse dans [Azure Active Directory Premium](active-directory-editions.md). Si vous cherchez à la place pour le Guide du développeur sur la façon de toointegrate des applications personnalisées avec Azure AD via le code, consultez [scénarios d’authentification pour Azure AD](active-directory-authentication-scenarios.md).

Hello Galerie d’applications Azure Active Directory fournit une liste des applications qui sont connues toosupport un formulaire de l’authentification unique avec Azure Active Directory, comme décrit dans [cet article](active-directory-appssoaccess-whatis.md). Une fois que vous (en tant qu’informatique spécialiste ou système intégrateur de votre organisation) avez trouvé application hello souhaitée tooconnect, vous pouvez commencer par des instructions détaillées hello suivez présentées Bonjour Azure management tooenable portail de l’authentification unique.

Les clients disposant de licences [Azure Active Directory Premium](active-directory-editions.md) licences obtiennent également ces fonctionnalités supplémentaires :

* Intégration libre-service de toute application prenant en charge les fournisseurs d’identité SAML 2.0 (Initiée par le fournisseur de services ou par le fournisseur d’identité fédérée)
* Intégration libre-service de toute application Web dont la page de connexion est basée sur le HTML et utilise une [authentification unique par mot de passe](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)
* Libre service de connexion des applications qui utilisent le protocole SCIM hello pour l’approvisionnement des utilisateurs ([décrites ici](active-directory-scim-provisioning.md))
* Capacité tooadd lie application tooany Bonjour [Lanceur d’applications Office 365](https://blogs.office.com/2014/10/16/organize-office-365-new-app-launcher-2/) ou hello [volet d’accès Azure AD](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)

Cela peut inclure non seulement les applications SaaS que vous utilisez, mais n’avez pas encore été toohello embarquée Galerie d’applications Azure AD, mais les applications web tiers que votre organisation a déployé tooservers que contrôler, soit dans le cloud de hello ou localement.

Ces fonctionnalités, également appelées *modèles d’intégration d’application*, fournissent des points de connexion basés sur des normes pour les applications prenant en charge l’authentification SCIM, SAML ou par formulaire, et incluent des paramètres et options flexibles pour la compatibilité avec un grand nombre d’applications. 

## <a name="adding-an-unlisted-application"></a>Ajout d’une application non répertoriée
tooconnect une application à l’aide d’un modèle de l’intégration d’application, connectez-vous au portail de gestion Azure hello à l’aide de votre compte d’administrateur Azure Active Directory et parcourir toohello **Active Directory > [répertoire] > Applications**section, sélectionnez **ajouter**, puis **ajouter une application à partir de la galerie de hello**. 

![][1]

Dans la galerie d’applications hello, vous pouvez ajouter une application non répertoriée à l’aide de hello **personnalisé** catégorie hello gauche, ou en sélectionnant hello **ajouter une application non répertoriée que** lien qui figure dans la recherche de hello résultats si votre application de votre choix n’a pas été trouvé. Après avoir entré un nom pour votre application, vous pouvez configurer le comportement et les options d’authentification unique hello. 

**Astuce**: il est recommandé d’utiliser hello recherche fonction toocheck toosee si hello application existe déjà dans la galerie d’applications hello. Si l’application hello et sa description mentionne « l’authentification unique », puis application hello sont déjà pris en charge pour seule l’authentification fédérée. 

![][2]

Ajout d’une application de cette manière fournit un toohello expérience très similaire disponible pour les applications pré-intégrées. toostart, sélectionnez **configurer l’authentification unique sur**. écran suivant de Hello présente hello suivant trois options de configuration de l’authentification unique, qui sont décrites dans les sections suivantes de hello.

![][3]

## <a name="azure-ad-single-sign-on"></a>Authentification unique Azure AD
Sélectionnez cette option tooconfigure SAML-l’authentification pour application hello. Ceci nécessite que hello prise en charge des applications SAML 2.0, et vous devez collecter des informations sur comment toouse hello fonctionnalités SAML de l’application hello avant de continuer. Après avoir sélectionné **suivant**, vous seront demandées tooenter trois différentes URL correspondantes des points de terminaison toohello SAML pour l’application hello. 

![][4]

Ces composants sont les suivants :

* **URL de connexion (initialisée par SP uniquement)** – où l’utilisateur de hello accède dans toosign toothis application. Si l’application hello est configurée unique d’initiée par le fournisseur de service tooperform se connecter, puis lorsqu’un utilisateur navigue toothis URL, fournisseur de services hello sera hello redirection nécessaire tooAzure AD tooauthenticate et utilisateur hello dans une session. Si ce champ est renseigné, Azure AD utilisera cette application de hello toolaunch URL à partir d’Office 365 et hello panneau d’accès Azure AD. Si ce champ est ommited, Azure AD va effectuer le fournisseur d’identité-authentification lorsque hello application est lancée à partir d’Office 365, hello panneau d’accès Azure AD, ou à partir de hello Azure AD unique initiée par l’authentification URL (copiable à partir de l’onglet du tableau de bord hello).
* **URL de l’émetteur** -hello URL de l’émetteur doit identifier de façon unique application hello pour le simple ouverture de session est configurée. Valeur hello que Azure AD envoie tooapplication arrière comme hello **public** paramètre de jeton SAML de hello et application hello est attendu toovalidate il. Cette valeur apparaît également comme hello **ID d’entité** dans toutes les métadonnées SAML fournie par l’application hello. Consultez la documentation SAML de l’application hello pour plus d’informations sur ce qu’il s’agit de l’entité ou la valeur de l’Audience est. Voici un exemple de comment hello Audience URL apparaît dans l’application de toohello retourné jeton SAML hello :

```
    <Subject>
    <NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:unspecificed">chad.smith@example.com</NameID>
        <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer" />
      </Subject>
      <Conditions NotBefore="2014-12-19T01:03:14.278Z" NotOnOrAfter="2014-12-19T02:03:14.278Z">
        <AudienceRestriction>
          <Audience>https://tenant.example.com</Audience>
        </AudienceRestriction>
      </Conditions>
```

* **URL de réponse** -URL de réponse hello est alors application hello attend le jeton SAML de hello tooreceive. Cela est également référencé tooas hello **URL du Service ACS (Assertion Consumer)**. Consultez la documentation SAML de l’application hello pour plus d’informations sur ce qui est son URL de réponse de jeton SAML ou ACS.
  Une fois que ceux-ci ont été entrées, cliquez sur **suivant** écran suivant de tooproceed toohello. Cet écran fournit des informations sur le besoins de toobe configuré sur tooenable de côté application hello tooaccept un jeton SAML à partir d’Azure AD. 

![][5]

Les valeurs qui sont requis pour varient en fonction de l’application hello, par conséquent, consultez la documentation de SAML de l’application hello pour plus d’informations. Hello **Sign-On** et **déconnexion** toohello résoudre les URL de service même point de terminaison, qui est le point de terminaison de gestion des demandes hello SAML pour votre instance d’Azure AD. URL de l’émetteur de Hello est la valeur hello apparaît sous la forme hello « Issuer » à l’intérieur de hello application de toohello émis jeton SAML. 

Une fois votre application a été configurée, cliquez sur **suivant** bouton et puis hello **Complete** boîte de dialogue tooclose hello. 

## <a name="assigning-users-and-groups-tooyour-saml-application"></a>Affecter des utilisateurs et les applications de groupes tooyour SAML
Une fois que votre application a été configurée toouse Azure AD en tant qu’un fournisseur d’identité SAML, il est presque prêt tootest. Comme un contrôle de sécurité, Azure AD n’émettra pas un jeton qui permet de les toosign dans l’application hello, sauf si elles ont été accordés l’accès à l’aide d’Azure AD. Les utilisateurs peuvent bénéficier d'un accès direct ou via un groupe dont ils sont membres. 

tooassign une application de tooyour utilisateur ou groupe, cliquez sur hello **affecter des utilisateurs** bouton. Sélectionnez hello utilisateur ou un groupe à votre convenance tooassign, puis sélectionnez hello **affecter** bouton. 

![][6]

Affectation d’un utilisateur permettra tooissue d’Azure AD un jeton pour l’utilisateur de hello, mais aussi à l’origine d’une vignette pour tooappear de cette application dans le volet d’accès de l’utilisateur hello. Une vignette d’application apparaît également dans le Lanceur d’applications hello Office 365 si hello utilisateur utilise Office 365. 

Vous pouvez charger un logo de vignette pour l’application hello utilisant hello **charger un Logo** bouton sur hello **configurer** onglet pour l’application hello. 

### <a name="customizing-hello-claims-issued-in-hello-saml-token"></a>Personnalisation des revendications hello émises dans un jeton SAML de hello
Lorsqu’un utilisateur s’authentifie toohello application, Azure AD émettra une application toohello jeton SAML qui contient des informations (ou les revendications) sur l’utilisateur hello qui identifie de façon unique les. Par défaut, cela inclut les nom d’utilisateur, adresse de messagerie, prénom et nom d’utilisateur hello. 

Vous pouvez afficher ou modifier des revendications hello envoyées Bonjour application toohello jeton SAML hello **attributs** onglet. 

![][7]

Il existe deux raisons pour lesquelles vous devrez peut-être les revendications de hello tooedit émises dans un jeton SAML de hello : •hello application a été écrit toorequire un autre ensemble d’URI de demande ou de la revendication application •Your de valeurs a été déployée dans une manière requérant hello Transmet la revendication toobe autre chose qu’un nom d’utilisateur de hello (AKA nom d’utilisateur principal) stockées dans Azure Active Directory. 

Pour plus d’informations sur la façon dont tooadd et modifier des revendications pour ces scénarios, consultez ce [l’article sur la personnalisation des revendications](active-directory-saml-claims-customization.md). 

### <a name="testing-hello-saml-application"></a>Test de hello SAML application
Après ont configuré les URL SAML hello et le certificat dans Azure AD et dans l’application hello, utilisateurs ou groupes ont reçu application toohello dans Azure, hello revendications ont été examinées et modifiées si nécessaire, puis l’utilisateur hello est prêt toosign dans hello application. 

tootest, simplement se connectent à hello volet d’accès Azure AD à https://myapps.microsoft.com à l’aide d’un compte d’utilisateur que vous avez affecté toohello application, puis cliquez sur la vignette hello pour tookick d’application hello hors processus d’authentification unique hello. Ou bien, vous pouvez parcourir directement toohello URL de connexion pour l’application hello et connectez-vous à partir de là. 

Conseils de débogage, consultez ce [l’article sur la façon de toodebug basé sur SAML uniques authentification tooapplications](active-directory-saml-debugging.md) 

## <a name="password-single-sign-on"></a>Authentification unique basée sur un mot de passe
Sélectionnez cette option tooconfigure [mot de passe l’authentification unique sur](active-directory-appssoaccess-whatis.md) pour une application web qui a une page de connexion HTML. Mot de passe SSO, également désignée tooas un mot de passe de stockage, vous permet de toomanage accès et mots de passe tooweb applications utilisateur qui ne prennent pas en charge la fédération d’identité. Il est également utile pour les scénarios où plusieurs utilisateurs doivent tooshare un seul compte, tels que des comptes d’application tooyour organisation sociaux. 

Après avoir sélectionné **suivant**, vous serez invité à tooenter des URL de hello de basée sur le web-page de connexion l’application hello. Notez que cela doit être page hello qui inclut les champs d’entrée hello nom d’utilisateur et mot de passe. Une fois entrée, Azure AD démarre une processus tooparse hello-page de connexion pour une entrée de nom d’utilisateur et un mot de passe entré. Si le processus de hello ne réussit pas, il vous guide ensuite dans un autre processus d’installation d’une extension du navigateur (nécessite Internet Explorer, Chrome ou Firefox) qui vous permettra de champs de hello toomanually capture.

Une fois hello-page de connexion est capturée, les utilisateurs et les groupes peuvent être affectés et les stratégies d’informations d’identification peuvent être définies uniquement à l’instar des [applications SSO de mot de passe](active-directory-appssoaccess-whatis.md).

Remarque : Vous pouvez télécharger un logo de vignette pour l’application hello utilisant hello **charger un Logo** bouton sur hello **configurer** onglet pour l’application hello. 

## <a name="existing-single-sign-on"></a>Authentification unique existante
Sélectionnez cette option tooadd un lien tooan application tooyour portail d’entreprise du panneau d’accès Azure AD ou Office 365. Vous pouvez utiliser cette tooadd liens toocustom web apps qui utilisent actuellement Azure Active Directory Federation Services (ou un autre service de fédération) au lieu d’Azure AD pour l’authentification. Ou bien, vous pouvez ajouter des liens profonds toospecific SharePoint pages ou autres que vous souhaitiez tooappear sur des panneaux d’accès de vos utilisateurs. 

Après avoir sélectionné **suivant**, vous seront demandées tooenter hello une URL de toolink d’application hello pour. Une fois terminé, les utilisateurs et les groupes peuvent être affectés toohello application, ce qui amène hello application tooappear Bonjour [Lanceur d’applications Office 365](https://blogs.office.com/2014/10/16/organize-office-365-new-app-launcher-2/) ou hello [volet d’accès Azure AD](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users) pour ces utilisateurs.

Remarque : Vous pouvez télécharger un logo de vignette pour l’application hello utilisant hello **charger un Logo** bouton sur hello **configurer** onglet pour l’application hello.

## <a name="related-articles"></a>Articles connexes
* [Index d’articles pour la gestion des applications dans Azure Active Directory](active-directory-apps-index.md)
* [Comment tooCustomize les revendications émises dans hello du jeton SAML pour les applications Pre-Integrated](active-directory-saml-claims-customization.md)
* [Dépannage de l’authentification unique basée sur SAML](active-directory-saml-debugging.md)

<!--Image references-->
[1]: ./media/active-directory-saas-custom-apps/customapp1.png
[2]: ./media/active-directory-saas-custom-apps/customapp2.png
[3]: ./media/active-directory-saas-custom-apps/customapp3.png
[4]: ./media/active-directory-saas-custom-apps/customapp4.png
[5]: ./media/active-directory-saas-custom-apps/customapp5.png
[6]: ./media/active-directory-saas-custom-apps/customapp6.png
[7]: ./media/active-directory-saas-custom-apps/customapp7.png
