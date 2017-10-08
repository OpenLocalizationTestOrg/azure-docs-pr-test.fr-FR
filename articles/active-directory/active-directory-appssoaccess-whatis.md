---
title: "aaaWhat est l’accès à l’application et l’authentification unique avec Azure Active Directory ? | Microsoft Docs"
description: "Utilisez Azure Active Directory tooenable unique authentification tooall de hello SaaS et les applications web dont vous avez besoin pour l’entreprise."
services: active-directory
documentationcenter: 
author: asmalser-msft
manager: femila
editor: 
ms.assetid: 75d1a3fd-b3c5-4495-a5c8-c4c24145ff00
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: curyand
ms.openlocfilehash: 429522cbd570ab27359c4630c5a6d7b25b692ec5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-application-access-and-single-sign-on-with-azure-active-directory"></a>Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?
L’authentification unique sur signifie être en mesure de tooaccess toutes les applications de hello et de ressources que vous avez besoin de toodo entreprise, en vous connectant une seule fois à l’aide d’un compte d’utilisateur. Une fois connecté, vous pouvez accéder à toutes les applications hello vous devez sans être tooauthenticate requis (par exemple, tapez un mot de passe) une deuxième fois.

De nombreuses entreprises s’appuient sur des applications SaaS comme Office 365, Box et Salesforce pour accroître la productivité des utilisateurs finaux. Historiquement, le personnel informatique doit tooindividually créer et mettre à jour des comptes d’utilisateur de chaque application SaaS, et que les utilisateurs ont tooremember un mot de passe pour chaque application SaaS.

Azure Active Directory s’étend sur site Active Directory dans le cloud de hello, l’activation des utilisateurs toouse leur compte professionnel principal toonot uniquement de connexion des appareils joints au domaine tootheir et ressources de l’entreprise, mais aussi tous hello applications web et SaaS nécessaire pour leur travail.

Par conséquent, non seulement les utilisateurs aient toomanage plusieurs ensembles de noms d’utilisateur et des mots de passe, leurs applications d’accès peut être mis en service ou annuler configuré automatiquement en fonction de leurs membres de groupe d’organisation, ainsi que leur état en tant qu’un employés. Azure Active Directory présente la sécurité et les contrôles de gouvernance d’accès qui permettent de vous toocentrally gérer l’accès des utilisateurs entre les applications SaaS.

Azure AD permet de réduire une intégration facile des applications SaaS populaires aujourd'hui ; Il fournit la gestion des identités et des accès et permet aux utilisateurs toosingle authentification tooapplications directement, ou découvre et les lancer à partir d’un portail tels que Office 365 ou hello volet d’accès Azure AD.

architecture de Hello d’intégration de hello est constituée de hello suivant quatre blocs de construction principaux :

* L’authentification unique permet aux utilisateurs tooaccess leurs applications SaaS avec leur compte professionnel dans Azure AD. L’authentification unique est ce qui permet des utilisateurs tooauthenticate tooan application à l’aide de leur compte d’organisation unique.
* L’approvisionnement de l’utilisateur et l’annulation de l’approvisionnement dans le SaaS cible en fonction des modifications apportées dans Windows Server Active Directory et/ou Azure AD. Un compte configuré est ce qui permet un toouse de toobe autorisé utilisateur une application, une fois qu’ils ont authentifiés via l’authentification unique.
* Gestion de l’accès centralisé application Bonjour portail de gestion Azure permet un accès application unique point de SaaS et gestion, avec hello capacité toodelegate application accès décision fabrication et approbations tooanyone dans l’organisation de hello
* Rapports unifiés et surveillance de l’activité utilisateur dans Azure AD

## <a name="how-does-single-sign-on-with-azure-active-directory-work"></a>Fonctionnement de l’authentification unique avec Azure Active Directory
Lorsqu’une application utilisateur « se connecte » tooan, ils accéder via un processus d’authentification là où ils sont requis tooprove qu’ils sont ceux qu’ils prétendent qu'être. Sans l’authentification unique, il suffit généralement un mot de passe qui est stockée au niveau de l’application hello et utilisateur de hello est requis tooknow ce mot de passe.

Azure AD prend en charge trois façons différentes toosign tooapplications :

* **L’authentification unique fédérée** active des applications tooredirect tooAzure AD pour l’authentification utilisateur au lieu de demander son propre mot de passe. Cela est pris en charge pour les applications qui prise en charge des protocoles tels que SAML 2.0, WS-Federation ou OpenID Connect et mode de hello plus riche de l’authentification unique.
* **L’authentification unique par mot de passe** permet de sécuriser le stockage et la lecture des mots de passe des applications à l’aide d’une extension de navigateur web ou d’une application mobile. Cela tire parti de hello existant processus de connexion fourni par l’application hello, mais permet à un mots de passe administrateur toomanage hello et ne nécessite pas de mot de passe hello utilisateur tooknow hello.
* **Existant Single Sign-On** permet à Azure AD tooleverage tout existant l’authentification unique qui a été configuré pour l’application hello, mais ces applications toobe lié toohello Office 365 ou les portails de panneau d’accès Azure AD et permet également de des rapports supplémentaires dans Azure AD lorsque les applications de hello sont lancées il.

Une fois qu’un utilisateur a authentifié avec une application, ils doivent également être toohave un enregistrement de compte est configuré au niveau de l’application hello qui indique l’application hello où il autorisations et les niveaux d’accès sont à l’intérieur d’application hello. Hello de configuration de cet enregistrement de compte peut se produire automatiquement, ou il peut se produire manuellement par un administrateur avant que l’accès de l’authentification unique est fourni par l’utilisateur de hello.

 Plus d’informations sur ces modes d’authentification unique et sur l’approvisionnement sont disponibles ci-dessous.

### <a name="federated-single-sign-on"></a>Authentification unique fédérée
Fédérés Single Sign-On permet aux utilisateurs de hello de session active dans votre toobe organisation automatiquement connecté dans l’application de SaaS tooa tierce par Azure AD à l’aide des informations de compte d’utilisateur hello d’Azure AD.

Dans ce scénario, lorsque vous avez déjà été connecté à Azure AD et que vous souhaitez tooaccess les ressources qui sont contrôlés par une application SaaS tierce, fédération évite hello pour un toobe utilisateur authentifié de nouveau.

Azure AD peut prendre en charge fédérée authentification unique avec les applications qui prennent en charge hello SAML 2.0, WS-Federation, ou OpenID connect protocoles.

Voir aussi : [Gestion des certificats pour l’authentification unique fédérée](active-directory-sso-certs.md)

### <a name="password-based-single-sign-on"></a>L’authentification unique par mot de passe
La configuration de mot de passe de session unique permet utilisateurs hello dans votre toobe organisation automatiquement connecté dans l’application de SaaS tooa tierce par Azure AD à l’aide des informations de compte d’utilisateur hello à partir de l’application de SaaS tiers hello. Lorsque vous activez cette fonctionnalité, Azure AD recueille et stocke en toute sécurité les informations de compte d’utilisateur hello et le mot de passe associé hello.

Azure AD prend en charge l’authentification unique par mot de passe pour toutes les applications cloud qui possèdent une page de connexion HTML. En utilisant un plug-in de navigateur personnalisé, AAD automatise le processus récupérant en toute sécurité les informations d’identification de l’application comme nom d’utilisateur hello et un mot de passe hello à partir du répertoire de hello de connexion de l’utilisateur hello et insère ces informations d’identification dans la page de connexion de l’application hello compte d’utilisateur de hello. Il existe deux cas d’utilisation :

1. **Administrateur gère les informations d’identification** – les administrateurs peuvent créer et gérer des informations d’identification de l’application et affecter ces toousers des informations d’identification ou des groupes qui doivent accéder aux toohello application. Dans ces cas, hello utilisateur n’a pas besoin d’informations d’identification de tooknow hello, mais obtient malgré tout application de toohello d’accès de l’authentification unique simplement en cliquant dessus dans leur volet d’accès ou via un lien fourni. Cela permet à la fois, gestion du cycle de vie des informations d’identification hello par l’administrateur de hello, ainsi que des raisons de commodité pour les utilisateurs finaux dans laquelle ils ne doivent tooremember ni gérer les mots de passe spécifiques de l’application. informations d’identification Hello obscurcies à partir de l’utilisateur final de hello lors de l’inscription automatique de hello dans le processus ; Toutefois, elles sont techniquement détectables par utilisateur hello à l’aide de web-débogage outils et les utilisateurs et les administrateurs doivent suivre hello mêmes stratégies de sécurité comme si hello les informations d’identification ont été présentées directement par l’utilisateur de hello. Les informations d’identification fournies par l’administrateur sont très utiles lorsqu’un compte d’accès est partagé entre plusieurs utilisateurs, par exemple pour les applications de médias sociaux ou de partage de documents.
2. **Gère les informations d’identification utilisateur** – les administrateurs peuvent affecter les applications tooend utilisateurs ou des groupes et autoriser hello fin utilisateurs tooenter leurs propres informations d’identification directement lors de l’accès à application hello pour hello première fois dans leur volet d’accès. Ceci s’avère pratique pour les utilisateurs finaux dans laquelle ils n’ont pas besoin toocontinually, entrez les mots de passe spécifiques de l’application hello chaque fois qu’ils accèdent à application hello. Ce cas de figure peut également servir gestion Pierre tooadministrative pas à pas d’informations d’identification de hello, dans laquelle administrateur de hello peut définir les nouvelles informations d’identification pour l’application hello à une date ultérieure sans modifier l’expérience d’accès application hello de l’utilisateur final de hello.

Dans les deux cas, les informations d’identification sont stockées dans un état chiffré dans le répertoire de hello et sont transmises uniquement via HTTPS au cours du processus de connexion hello automatisée. Avec l’authentification unique par mot de passe, Azure AD offre une solution de gestion d’accès pratique pour les applications qui ne peuvent pas prendre en charge les protocoles de fédération.

Mot de passe de l’authentification unique s’appuie sur un navigateur extension toosecurely récupérer hello utilisateur et applications des informations spécifiques à partir d’Azure AD et l’applique toohello service. La plupart des applications SaaS tierces prises en charge par Azure AD prennent en charge cette fonctionnalité.

Pour l’authentification unique basée sur le mot de passe, hello navigateurs des utilisateurs finaux peuvent être :

* Internet Explorer 8, 9, 10, 11 -- sous Windows 7 ou version ultérieure (voir également [Guide de déploiement extension IE](active-directory-saas-ie-group-policy.md))
* Chrome -- sur Windows 7 ou ultérieur, et sur Mac OS X ou ultérieur
* Firefox 26.0 ou ultérieur -- sur Windows XP SP2 ou ultérieur, et sur Mac OS X 10.6 ou ultérieur

**Remarque :** hello mot de passe SSO d’extension devient disponible pour Edge dans Windows 10 lorsque les extensions du navigateur sont pris en charge pour la session.

### <a name="existing-single-sign-on"></a>Authentification unique existante
Lorsque vous configurez l’authentification unique pour une application, le portail de gestion Azure hello fournit une troisième option de « existant Single Sign-On ». Cette option permet à une application de tooan lien hello administrateur toocreate simplement et placez-le sur le volet d’accès hello pour les utilisateurs sélectionnés.

Par exemple, s’il existe une application qui est configuré tooauthenticate les utilisateurs à l’aide d’Active Directory Federation Services 2.0, un administrateur peut utiliser hello « existante Single Sign-On » option toocreate un tooit lien sur le volet d’accès hello. Lorsque les utilisateurs accèdent de lien de hello, ils sont authentifiés à l’aide d’Active Directory Federation Services 2.0 ou toute solution unique existante authentification fournie par l’application hello.

### <a name="user-provisioning"></a>Approvisionnement de l’utilisateur
Pour sélectionner des applications, Azure AD permet l’approvisionnement automatique des utilisateurs et l’annulation du déploiement de comptes dans les applications SaaS tierces depuis hello portail de gestion Azure, à l’aide de vos informations d’identité Windows Server Active Directory ou Azure AD. Lorsqu’un utilisateur se voit accorder des autorisations dans Azure AD pour l’une de ces applications, un compte peut être créé automatiquement (configuré) dans une application SaaS cible de hello.

Lorsqu’un utilisateur est supprimé ou ses informations sont modifiées dans Azure AD, ces modifications sont également répercutées dans hello application SaaS. Cela signifie, configuration de la gestion du cycle de vie automatique des identités permet aux administrateurs toocontrol et fournir une configuration automatisée et de l’annulation du déploiement d’applications SaaS. Dans Azure AD, cette automatisation de la gestion du cycle de vie des identités se fait via l’approvisionnement de l’utilisateur.

toolearn, voir [automatisée l’approvisionnement des utilisateurs et Deprovisioning tooSaaS Applications](active-directory-saas-app-provisioning.md)

## <a name="get-started-with-hello-azure-ad-application-gallery"></a>Prise en main Galerie d’applications Azure AD hello
Prêt tooget démarré ? toodeploy l’authentification unique entre Azure AD et les applications SaaS utilisées par votre organisation, suivez ces instructions.

### <a name="using-hello-azure-ad-application-gallery"></a>À l’aide de la galerie d’applications Azure AD hello
Hello [Galerie d’applications Azure Active Directory](https://azure.microsoft.com/marketplace/active-directory/all/) fournit une liste des applications qui sont connues toosupport un formulaire de l’authentification unique avec Azure Active Directory.

![][1]

Voici quelques conseils pour trouver des applications en fonction des fonctionnalités qu’elles prennent en charge :

* Azure AD prend en charge la configuration automatique et de l’annulation du déploiement pour toutes les applications « Par défaut » Bonjour [Galerie d’applications Azure Active Directory](https://azure.microsoft.com/marketplace/active-directory/all/).
* Une liste d'applications fédérées qui prennent en charge l'authentification unique fédérée à l'aide d'un protocole comme SAML, WS-Federation ou OpenID Connect est disponible [ici](http://social.technet.microsoft.com/wiki/contents/articles/20235.azure-active-directory-application-gallery-federated-saas-apps.aspx).

Une fois que vous avez trouvé votre application, vous pouvez commencer par suivez hello pas à pas les instructions présentées dans la galerie d’applications hello et dans tooenable portail de gestion Azure hello sur l’authentification unique.

### <a name="application-not-in-hello-gallery"></a>Application pas dans la galerie de hello ?
Si votre application est introuvable dans la galerie d’applications Azure AD hello, vous disposez des options suivantes :

* **Ajouter une application non répertoriée que vous utilisez** -une catégorie personnalisée hello utilisation dans la galerie d’applications hello dans tooconnect portail de gestion Azure hello une application non répertoriée à l’aide de votre organisation. Vous pouvez ajouter n’importe quelle application qui prend en charge SAML 2.0 comme application fédérée, ou bien toute application qui possède une page de connexion HTML comme étape d’authentification unique avec mot de passe. Pour plus d’informations, consultez cet article sur l’ [ajout de votre propre application](active-directory-saas-custom-apps.md).
* **Ajouter votre propre application que vous développez** : Si vous avez développé application hello vous-même, suivez les instructions de hello Bonjour Azure AD developer documentation tooimplement fédéré l’authentification unique ou à l’aide de l’approvisionnement hello API Azure AD graph. Pour plus d’informations, consultez ces ressources :
  
  * [Scénarios d’authentification pour Azure AD](active-directory-authentication-scenarios.md)
  * [https://github.com/AzureADSamples/WebApp-MultiTenant-OpenIdConnect-DotNet](https://github.com/AzureADSamples/WebApp-MultiTenant-OpenIdConnect-DotNet)
  * [https://github.com/AzureADSamples/WebApp-WebAPI-MultiTenant-OpenIdConnect-DotNet](https://github.com/AzureADSamples/WebApp-WebAPI-MultiTenant-OpenIdConnect-DotNet)
  * [https://github.com/AzureADSamples/NativeClient-WebAPI-MultiTenant-WindowsStore](https://github.com/AzureADSamples/NativeClient-WebAPI-MultiTenant-WindowsStore)
* **Demander une intégration d’application** -demande de support pour l’application hello que vous avez besoin à l’aide de hello [forum de commentaires d’Azure AD](https://feedback.azure.com/forums/169401-azure-active-directory/).

### <a name="using-hello-azure-management-portal"></a>À l’aide du portail de gestion Azure hello
Vous pouvez utiliser hello extension Active Directory Bonjour portail de gestion Azure tooconfigure hello application SSO. Dans un premier temps, vous devez tooselect un répertoire à partir de la section Active Directory dans le portail de hello de hello :

![][2]

toomanage vos applications SaaS tierces, vous pouvez basculer dans l’onglet Applications de hello du répertoire sélectionné de hello. Cette vue permet aux administrateurs d’effectuer les opérations suivantes :

* Ajouter de nouvelles applications à partir de la galerie d’Azure AD hello, ainsi que des applications que vous développez
* Supprimer les applications intégrées
* Gérer les applications hello que déjà intégrées.

Les tâches administratives standard pour une application SaaS tierce sont :

* Activer l’authentification unique avec Azure AD, à l’aide du mot de passe SSO ou, s’il est disponible pour la cible de hello SaaS, de l’authentification unique fédérée
* Le cas échéant, l’activation de l’approvisionnement pour l’approvisionnement et l’annulation de l’approvisionnement de l’utilisateur (gestion du cycle de vie des identités).
* Pour les applications où la configuration de l’utilisateur est activée, sélectionnez les utilisateurs qui ont accès toothat application

Pour les applications de la galerie qui prennent en charge fédérée l’authentification unique, configuration nécessite généralement vous tooprovide des paramètres de configuration supplémentaires tels que les certificats et les métadonnées toocreate une approbation fédérée entre l’application tierce de hello et Azure AD. Assistant de configuration de Hello vous guide à travers les détails hello et fournit des accès facile toohello données propres aux applications SaaS et obtenir des instructions.

Pour les applications de la galerie qui prennent en charge la configuration automatique d’utilisateurs, cela nécessite vous toogive Azure AD autorisations toomanage vos comptes dans l’application SaaS de hello. Au minimum, vous devez tooprovide informations d’identification Azure AD doivent utiliser lors de l’authentification sur toohello d’application cible. Si les paramètres de configuration supplémentaires doivent toobe fourni dépend des exigences hello de l’application hello.

## <a name="deploying-azure-ad-integrated-applications-toousers"></a>Déploiement d’Azure AD intégré toousers d’applications
Azure AD fournit plusieurs façons personnalisables toodeploy applications tooend-les utilisateurs de votre organisation :

* Panneau d’accès Azure AD
* Lanceur d’applications Office 365
* Applications toofederated l’authentification directe
* Des liens profonds toofederated, basé sur le mot de passe, ou les applications existantes

Les méthodes que vous choisissez toodeploy dans votre organisation est à votre convenance.

### <a name="azure-ad-access-panel"></a>Panneau d’accès Azure AD
Hello volet d’accès à https://myapps.microsoft.com est un portail web qui permet à un utilisateur final avec un compte professionnel dans Azure Active Directory tooview et lancer les applications cloud toowhich est qu’ils ont été accordé l’accès par hello Azure AD administrateur. Si vous êtes un utilisateur final ayant [Azure Active Directory Premium](https://azure.microsoft.com/pricing/details/active-directory/), vous pouvez également utiliser les fonctionnalités de gestion de groupes libre-service via hello panneau d’accès.

![][3]

Hello volet d’accès est séparé hello portail de gestion Azure et ne nécessite pas d’utilisateurs toohave un abonnement Azure ou Office 365.

Pour plus d’informations sur le volet d’accès hello Azure AD, consultez hello [volet d’accès toohello introduction](active-directory-saas-access-panel-introduction.md).

### <a name="office-365-application-launcher"></a>Lanceur d’applications Office 365
Pour les organisations qui ont déployé Office 365, applications assignées toousers via Azure AD apparaîtra également dans le portail de hello Office 365 à l’adresse https://portal.office.com/myapps. Il est ainsi facile et pratique pour les utilisateurs dans une organisation toolaunch leurs applications sans avoir à toouse un deuxième portail et hello est recommandé d’application de lancement de la solution pour les organisations à l’aide d’Office 365.

![][4]

Pour plus d’informations sur le Lanceur d’applications hello Office 365, consultez [afficher votre application dans le Lanceur d’applications hello Office 365](https://msdn.microsoft.com/office/office365/howto/connect-your-app-to-o365-app-launcher).

### <a name="direct-sign-on-toofederated-apps"></a>Applications toofederated l’authentification directe
La plupart des applications fédérées qui prennent en charge d’OpenID, WS-Federation ou SAML 2.0 connectez-vous également capacité hello de prise en charge pour toostart les utilisateurs à l’application hello et puis obtient connectées via Azure AD par redirection automatique ou en cliquant sur un toosign lien dans. Il s’agit en tant que fournisseur de service-authentification unique initiée par, et la plupart des applications fédérées dans la galerie d’applications hello Azure AD prend en charge cette (voir la documentation de hello liée à partir de l’Assistant de configuration de l’authentification unique de l’application hello dans le portail de gestion Azure hello pour Détails).

![][5]

### <a name="direct-sign-on-links-for-federated-password-based-or-existing-apps"></a>Liens d’authentification directs pour les applications fédérées, par mot de passe ou des applications existantes
Azure AD prend également en charge les applications tooindividual unique authentification liens directs qui prennent en charge basée sur mot de passe l’authentification unique sur existant l’authentification unique et toutes les formes de fédérée l’authentification unique.

Ces liens sont spécifiquement conçus URL qui envoient un utilisateur via hello Azure AD se connecte à une application spécifique sans exiger de hello utilisateur les lancer à partir de panneau d’accès hello Azure AD ou Office 365. Ces URL de l’authentification unique sont accessibles sous l’onglet tableau de bord de hello de toute application pré-intégrées Bonjour section Active Directory du portail de gestion Azure hello, comme indiqué dans la capture d’écran hello ci-dessous.

![][6]

Ces liens peuvent être copiées et collées partout où que vous souhaitez tooprovide un signe de lien toohello sélectionné application. Cela peut être dans un message électronique ou dans n’importe quel portail web personnalisé que vous avez configuré pour l’accès. Voici un exemple d’URL d’authentification unique Azure AD pour Twitter :

`https://myapps.microsoft.com/signin/Twitter/230848d52c8745d4b05a60d29a40fced`

URL spécifique tooorganization similaire pour le volet d’accès hello, vous pouvez personnaliser davantage cette URL en ajoutant un des domaines de hello actif ou vérifié pour votre annuaire du domaine myapps.microsoft.com hello. Cela garantit qu'un logo de l’entreprise est immédiatement chargée sur la page de connexion hello sans hello utilisateur tooenter leur ID utilisateur tout d’abord :

`https://myapps.microsoft.com/contosobuild.com/signin/Twitter/230848d52c8745d4b05a60d29a40fced`

Lorsqu’un utilisateur autorisé clique sur un de ces liens spécifiques à l’application, ils tout d’abord voir leur organisation-page de connexion (en supposant qu’ils ne sont pas connectés) et après la connexion sont application tootheir redirigé sans arrêter tout d’abord au volet d’accès hello. Si les conditions préalables tooaccess hello application, comme l’extension du navigateur hello authentification unique basée sur le mot de passe, est manquant pour l’utilisateur de hello lien de hello invitera l’extension manquante hello utilisateur tooinstall hello. URL du lien Hello reste constante si hello seule configuration d’authentification pour l’application hello change.

Ces liens utilisent hello mêmes mécanismes de contrôle d’accès que hello accéder au panneau de configuration et d’Office 365, et seuls ces utilisateurs ou groupes qui ont été attribuées application toohello dans le portail de gestion Azure hello pourront toosuccessfully s’authentifier. Toutefois, un message qui explique qu’ils n’ont pas reçus d’accès et reçoivent un lien tooload hello accès panneau tooview applications disponibles pour laquelle ils ont accès s’affiche pour tout utilisateur qui n’est pas autorisé.

## <a name="related-articles"></a>Articles connexes
* [Index d’articles pour la gestion des applications dans Azure Active Directory](active-directory-apps-index.md)
* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Détection des applications cloud non approuvées avec Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md)
* [Introduction tooManaging tooApps d’accès](active-directory-managing-access-to-apps.md)
* [Comparaison des capacités de gestion des identités externes dans Azure AD](active-directory-b2b-compare-external-identities.md)

<!--Image references-->
[1]: ./media/active-directory-appssoaccess-whatis/onlineappgallery.png
[2]: ./media/active-directory-appssoaccess-whatis/azuremgmtportal.png
[3]: ./media/active-directory-appssoaccess-whatis/accesspanel.png
[4]: ./media/active-directory-appssoaccess-whatis/officeapphub.png
[5]: ./media/active-directory-appssoaccess-whatis/workdaymobile.png
[6]: ./media/active-directory-appssoaccess-whatis/deeplink.png
