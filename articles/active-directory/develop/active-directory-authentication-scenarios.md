---
title: "Scénarios pour Azure AD d’aaaAuthentication | Documents Microsoft"
description: "Vue d’ensemble de scénarios d’authentification les plus courants hello cinq pour Azure Active Directory (AAD)"
services: active-directory
documentationcenter: dev-center-name
author: skwan
manager: mbaldwin
editor: 
ms.assetid: 0c84e7d0-16aa-4897-82f2-f53c6c990fd9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: skwan
ms.custom: aaddev
ms.openlocfilehash: 5b391e3f096fcb52934c4a8aff08688352bfd3dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-scenarios-for-azure-ad"></a>Scénarios d’authentification pour Azure AD
Azure Active Directory (Azure AD) simplifie l’authentification pour les développeurs en fournissant l’identité en tant que service, avec prise en charge pour les normes des protocoles tels que OAuth 2.0 et OpenID Connect, ainsi que les bibliothèques open source pour différentes plateformes toohelp vous commencer à coder rapidement. Ce document vous aide comprendre hello prend en charge de différents scénarios Azure AD et vous montrera comment tooget a démarré. Il est divisé en hello les sections suivantes :

* [Principes fondamentaux de l’authentification dans Azure AD](#basics-of-authentication-in-azure-ad)
* [Revendications des jetons de sécurité Azure AD](#claims-in-azure-ad-security-tokens)
* [Principes fondamentaux de l’inscription d’une application dans Azure AD](#basics-of-registering-an-application-in-azure-ad)
* [Types d’application et scénarios](#application-types-and-scenarios)
  
  * [TooWeb de navigateur Web Application](#web-browser-to-web-application)
  * [Application à page unique (SPA)](#single-page-application-spa)
  * [TooWeb Application native API](#native-application-to-web-api)
  * [TooWeb d’Application Web API](#web-application-to-web-api)
  * [Application démon ou serveur tooWeb API](#daemon-or-server-application-to-web-api)

## <a name="basics-of-authentication-in-azure-ad"></a>Principes fondamentaux de l’authentification dans Azure AD
Si vous ne connaissez pas les concepts de base de l’authentification dans Azure AD, lisez cette section. Dans le cas contraire, vous souhaiterez peut-être tooskip bas trop[Types d’applications et scénarios](#application-types-and-scenarios).

Prenons le scénario le plus élémentaire hello où l’identité est requise : application web de tooa tooauthenticate a besoin d’un utilisateur dans un navigateur web. Ce scénario est décrit en détail dans hello [tooWeb de navigateur Web Application](#web-browser-to-web-application) section, mais un démarrage point tooillustrate hello des fonctionnalités d’Azure AD et conceptualiser le fonctionne du scénario de hello. Tenez compte des hello suivant le schéma pour ce scénario :

![Vue d’ensemble de l’application d’authentification tooweb](./media/active-directory-authentication-scenarios/basics_of_auth_in_aad.png)

Diagramme hello ci-dessus à l’esprit, voici ce que vous devez tooknow sur ses différents composants :

* Azure AD est un fournisseur d’identité hello, responsable de la vérification d’identité hello des utilisateurs et des applications qui existent dans le répertoire de l’organisation et de l’émission des jetons de sécurité après une authentification réussie de ces applications et les utilisateurs.
* Une application qui veut toooutsource tooAzure de l’authentification Active Directory doit être inscrit dans Azure AD, qui inscrit et identifie les application hello dans le répertoire de hello.
* Les développeurs peuvent utiliser hello open source Azure AD bibliothèques toomake authentification simple en gérant les détails de protocole hello pour vous. Pour plus d’informations, consultez la rubrique [Bibliothèques d’authentification d’Azure Active Directory](active-directory-authentication-libraries.md) .

• Une fois un utilisateur a été authentifié, l’application hello doit valider tooensure de jeton de sécurité de l’utilisateur hello que l’authentification a réussi de hello conçues tiers. Les développeurs peuvent utiliser hello fourni de validation de toohandle bibliothèques d’authentification d’un jeton d’Azure AD, y compris les jetons Web JSON (JWT) ou SAML 2.0. Si vous souhaitez que la validation de tooperform manuellement, consultez hello [Gestionnaire de jetons JWT](https://msdn.microsoft.com/library/dn205065.aspx) documentation.

> [!IMPORTANT]
> Azure AD utilise des jetons toosign de chiffrement à clé publique et vérifiez qu’ils sont valides. Consultez [Important d’informations sur la signature de substitution des clés dans Azure AD](active-directory-signing-key-rollover.md) pour plus d’informations sur la logique nécessaire de hello, vous devez disposer dans votre application tooensure il est toujours mis à jour avec les dernières clés de hello.
> 
> 

flux de hello • des demandes et réponses hello processus d’authentification est déterminée par le protocole d’authentification hello qui a été utilisé, tel qu’OAuth 2.0, OpenID Connect, WS-Federation ou SAML 2.0. Ces protocoles sont présentés plus en détail dans hello [protocoles d’authentification Azure Active Directory](active-directory-authentication-protocols.md) rubrique et dans les sections hello ci-dessous.

> [!NOTE]
> Azure AD prend en charge hello OAuth 2.0 et les normes OpenID Connect qui font une large utilisent des jetons de support, y compris les jetons de support représentés comme jetons Web JSON. Un jeton de support est un jeton de sécurité léger qu’accorde hello tooa d’accès « support » une ressource protégée. Dans ce sens, hello « support » est une partie capable de présenter le jeton de hello. Si un tiers doit s’authentifier avec un jeton de support pour Azure AD tooreceive hello, si nécessaire de hello étapes ne sont pas prises jeton de hello toosecure de transmission et de stockage, il peut être interceptée et utilisée par une partie indésirable. Bien que certains jetons de sécurité intègrent un mécanisme de protection contre l’utilisation par des parties non autorisées, les jetons porteurs n’en sont pas dotés et doivent donc être acheminés sur un canal sécurisé, par exemple à l’aide du protocole TLS (HTTPS). Si un jeton de support est transmis en clair de hello, une attaque hello man-in peut être utilisé par un jeton de hello tooacquire partie malveillante et l’utiliser pour une ressource tooa protégée de tout accès non autorisé. Bonjour les mêmes principes de sécurité s’appliquent lors du stockage ou la mise en cache des jetons de support pour une utilisation ultérieure. Veillez systématiquement à ce que votre application transmette et stocke les jetons porteurs de manière sécurisée. Pour en savoir plus sur les aspects de sécurité des jetons porteurs, consultez [RFC 6750 Section 5](http://tools.ietf.org/html/rfc6750).
> 
> 

Maintenant que vous avez une vue d’ensemble des concepts de base hello et lisez les sections hello ci-dessous toounderstand comment l’approvisionnement fonctionne dans Azure AD et prend en charge des scénarios courants de hello Azure AD.

## <a name="claims-in-azure-ad-security-tokens"></a>Revendications des jetons de sécurité Azure AD
Les jetons de sécurité émis par Azure AD contiennent des revendications, ou assertions d’informations sur l’objet hello qui a été authentifié. Ces revendications peuvent être utilisées par l’application hello pour différentes tâches. Par exemple, ils peuvent toovalidate utilisées hello jeton, identifier le locataire d’annuaire du sujet hello, afficher des informations utilisateur, déterminer l’autorisation du sujet hello et ainsi de suite. Hello revendications présentes dans un jeton de sécurité donné sont dépendantes de type hello de jeton, de type hello d’informations d’identification utilisées tooauthenticate hello utilisateur et configuration de l’application hello. Une brève description de chaque type de revendication émise par Azure AD est fournie dans le tableau hello ci-dessous. Pour plus d’informations, consultez trop[prise en charge du jeton et Types de revendications](active-directory-token-and-claims.md).

| Revendication | Description |
| --- | --- |
| ID de l'application |Identifie l’application hello qui utilise un jeton hello. |
| Public ciblé |Identifie la ressource de destinataire hello hello jeton est destiné. |
| Référence de classe du contexte d’authentification de l’application |Indique comment hello client a été authentifié (client public ou client confidentiel). |
| Moment d’authentification |Enregistrements hello date et heure de l’authentification de hello. |
| Méthode d'authentification |Indique comment le sujet hello du jeton de hello a été authentifié (mot de passe, certificat, etc.). |
| Prénom |Fournit des hello le prénom de l’utilisateur de hello dans Azure AD en tant qu’ensemble. |
| Groupes |Contient les groupes de codes d’Azure AD objet hello utilisateur est un membre. |
| Fournisseur d’identité |Enregistrements hello fournisseur d’identité qui a authentifié le sujet hello du jeton de hello. |
| Émis à |Heure de hello enregistrements à quels hello jeton a été émis, souvent utilisés pour l’actualisation du jeton. |
| Émetteur |Identifie le STS hello qui a émis le jeton de hello ainsi que de locataire Azure AD de hello. |
| Nom |Fournit des surname hello d’utilisateur de hello dans Azure AD en tant qu’ensemble. |
| Nom |Fournit une valeur contrôlable de visu qui identifie le sujet hello du jeton de hello. |
| ID objet |Contient un identificateur unique et immuable du sujet de hello dans Azure AD. |
| contrôleur |Contient les noms conviviaux des rôles d’Application Azure AD dispose cet utilisateur hello. |
| Scope |Indique hello autorisations accordées toohello client application. |
| Objet |Indique le principal de hello sur quel hello jeton déclare les informations. |
| ID client |Contient un identificateur unique et immuable du locataire d’annuaire hello qui a émis le jeton de hello. |
| Durée de vie du jeton |Définit l’intervalle de temps hello dans lequel un jeton est valide. |
| Nom d’utilisateur principal |Contient le nom d’utilisateur hello principal de l’objet de hello. |
| Version |Contient le numéro de version de hello du jeton de hello. |

## <a name="basics-of-registering-an-application-in-azure-ad"></a>Principes fondamentaux de l’inscription d’une application dans Azure AD
Toute application qui sous-traite tooAzure d’authentification qu'active Directory doit être enregistré dans un répertoire. Cette étape consiste à indiquer à Azure AD sur votre application, y compris les URL hello où il est situé, hello URL toosend réponses après authentification, hello URI tooidentify votre application et bien plus encore. Ces informations sont obligatoires pour les raisons principales suivantes :

* Azure AD doit toocommunicate coordonnées avec l’application hello lors de la gestion des jetons d’authentification ou de l’échange. Ces hello suivants :
  
  * URI ID d’application : hello identificateur pour une application. Cette valeur est envoyée tooAzure AD au cours de tooindicate d’authentification qui appelant de hello application souhaite un jeton. En outre, cette valeur est incluse dans le jeton de hello afin que l’application hello sait qu’il a été hello destiné cible.
  * Réponse URL et l’URI de redirection : hello les cas d’une API web ou d’application web, hello URL de réponse est toowhich d’emplacement hello Azure AD envoie la réponse d’authentification hello, y compris un jeton si l’authentification a réussi. Dans le cas de hello d’une application native, hello URI de redirection est qu'un identificateur unique de toowhich Azure AD redirigera hello user-agent dans une requête OAuth 2.0.
  * ID d’application : hello ID pour une application, qui est générée par Azure AD quand l’application hello est enregistrée. Lors de la demande d’un code d’autorisation ou un jeton, hello ID d’Application et la clé sont envoyés tooAzure AD lors de l’authentification.
  * : Hello clé envoyée avec un ID d’Application lors de l’authentification tooAzure AD toocall une API web.
* Les besoins AD Azure tooensure hello application a hello tooaccess des autorisations requises à vos données d’annuaire, les autres applications de votre organisation et ainsi de suite

L’approvisionnement devient plus clair lorsque vous comprenez qu’il existe deux catégories d’applications que vous pouvez développer et intégrer avec Azure AD :

* Application à client unique : une application à client unique est  prévue pour une utilisation dans une organisation. Il s’agit généralement d’applications métiers écrites par un développeur d’entreprise. Une application à locataire unique doit uniquement toobe accessible aux utilisateurs dans un répertoire, et par conséquent, il doit uniquement toobe configuré dans un répertoire. Ces applications sont généralement inscrites par un développeur d’organisation de hello.
* Application mutualisée : une application mutualisée est prévue pour une utilisation dans plusieurs organisations, pas une seule. Il s’agit généralement d’applications SaaS (software-as-a-service) écrites par un éditeur de logiciels indépendant. Applications mutualisées doivent toobe configuré dans chaque répertoire dans lequel ils seront utilisés, ce qui nécessite tooregister de consentement utilisateur ou un administrateur les. Ce processus de consentement démarre lorsqu’une application a été enregistrée dans le répertoire de hello et bénéficie de l’API Graph accès toohello ou peut-être une autre API web. Quand un utilisateur ou un administrateur à partir d’une autre organisation s’inscrit à application hello de toouse, elles sont présentées avec une boîte de dialogue qui affiche les autorisations hello requiert l’application hello. Hello utilisateur ou un administrateur peut alors consentement toohello application, ce qui donne hello application accès toohello indiqué les données, et enfin les registres hello application dans leur annuaire. Pour plus d’informations, consultez [vue d’ensemble de l’infrastructure de consentement de hello](active-directory-integrating-applications.md#overview-of-the-consent-framework).

Vous devez tenir compte d’autres éléments lorsque vous choisissez de développer une application mutualisée plutôt qu’une application à client unique. Par exemple, si vous effectuez votre toousers disponible application dans plusieurs annuaires, vous avez besoin d’un mécanisme toodetermine quel locataire ils se trouvent dans. Une application à locataire unique suffit toolook dans son propre annuaire pour un utilisateur, tandis que tooidentify un utilisateur spécifique à partir de tous les répertoires hello a besoin d’une application mutualisée dans Azure AD. tooaccomplish cette tâche, Azure AD fournit un point de terminaison d’authentification commun, où toute application mutualisée peut diriger les demandes de connexion, au lieu d’un point de terminaison spécifiques du client. Ce point de terminaison est https://login.microsoftonline.com/common pour tous les répertoires dans Azure AD, alors qu’un point de terminaison spécifiques du client peut être https://login.microsoftonline.com/contoso.onmicrosoft.com. point de terminaison commun Hello est particulièrement important tooconsider lorsque vous développez votre application, car vous devez hello logique nécessaire toohandle plusieurs clients pendant la connexion, déconnexion et la validation du jeton.

Si vous développez actuellement une application à locataire unique, mais souhaitez toomake il organisations de réduire disponibles, vous pouvez facilement apporter modifications toohello application et sa configuration dans Azure AD toomake il mutualisée compatible. En outre, Azure AD utilise hello même clé pour tous les jetons dans tous les répertoires de signature, si vous fournissez l’authentification dans un seul client ou une application mutualisée.

Chaque scénario répertorié dans ce document inclut une sous-section décrivant les exigences d’approvisionnement associées. Pour plus d’informations sur la configuration d’une application dans Azure AD et hello les différences entre les applications uniques et plusieurs locataires, consultez [intégration d’Applications avec Azure Active Directory](active-directory-integrating-applications.md) pour plus d’informations. Poursuivez la lecture des scénarios d’application courants hello toounderstand dans Azure AD.

## <a name="application-types-and-scenarios"></a>Types d’application et scénarios
Chacun des scénarios de hello décrits dans ce document peut être développée à l’aide de différents langages et plateformes. Ils bénéficient tous des exemples de code qui sont disponibles dans notre [exemples de Code guide](active-directory-code-samples.md), ou directement à partir de hello correspondant [des référentiels GitHub exemple](https://github.com/Azure-Samples?utf8=%E2%9C%93&query=active-directory). De plus, si votre application nécessite un élément ou segment spécifique d’un scénario de bout en bout, vous pouvez ajouter cette fonctionnalité séparément dans la plupart des cas. Par exemple, si vous avez une application native qui appelle une API web, vous pouvez facilement ajouter une application web qui appelle également hello web API. Hello diagramme suivant illustre ces scénarios et les types d’applications, et comment les différents composants peuvent être ajoutés :

![Types d’application et scénarios](./media/active-directory-authentication-scenarios/application_types_and_scenarios.png)

Il s’agit de hello cinq principaux scénarios d’application pris en charge par Azure AD :

* [Web Browser tooWeb Application](#web-browser-to-web-application): toosign dans l’application web tooa sécurisée par Azure AD a besoin d’un utilisateur.
* [Single Page Application (SPA)](#single-page-application-spa): toosign dans tooa application à page unique sécurisée par Azure AD a besoin d’un utilisateur.
* [TooWeb Application native API](#native-application-to-web-api): une application native qui s’exécute sur un téléphone, tablette ou un PC besoins tooauthenticate un tooget utilisateur ressources à partir d’une API web sécurisée par Azure AD.
* [Web Application tooWeb API](#web-application-to-web-api): tooget des ressources à partir d’une API web sécurisée par Azure AD a besoin d’une application web.
* [Application démon ou serveur tooWeb API](#daemon-or-server-application-to-web-api): tooget des ressources à partir d’une API web sécurisée par Azure AD a besoin d’une application démon ou une application serveur sans aucune interface utilisateur web.

### <a name="web-browser-tooweb-application"></a>TooWeb de navigateur Web Application
Cette section décrit une application qui authentifie un utilisateur dans une application web de tooa de navigateur web. Dans ce scénario, application web de hello dirige toosign de navigateur de l’utilisateur hello dans tooAzure AD. Azure AD renvoie une réponse de connexion via le navigateur de l’utilisateur de hello, qui contient les revendications relatives à utilisateur hello dans un jeton de sécurité. Ce scénario prend en charge l’authentification à l’aide des protocoles WS-Federation, SAML 2.0 et OpenID Connect de hello.

#### <a name="diagram"></a>Diagramme
![Flux d’authentification pour l’application de navigateur tooweb](./media/active-directory-authentication-scenarios/web_browser_to_web_api.png)

#### <a name="description-of-protocol-flow"></a>Description du flux du protocole
1. Lorsqu’un utilisateur visite l’application hello et doit toosign dans, il est redirigé via un point de terminaison de demande de connexion toohello d’authentification dans Azure AD.
2. Hello utilisateur se connecte sur hello-page de connexion.
3. Si l’authentification réussit, Azure AD crée un jeton d’authentification et retourne l’URL de réponse d’une application toohello de réponse de connexion qui a été configuré dans hello portail Azure. Pour une application de production, cette URL de réponse doit être au format HTTPS. Hello renvoyé un jeton inclut des revendications sur utilisateur de hello et Azure AD qui sont requises par le jeton de hello application toovalidate hello.
4. application Hello valide le jeton de hello à l’aide d’une clé de signature publique et les informations de l’émetteur disponibles au niveau du document de métadonnées de fédération hello pour Azure AD. Une fois l’application hello valide le jeton de hello, Azure AD démarre une nouvelle session avec l’utilisateur de hello. Cette session permet de hello utilisateur tooaccess application hello jusqu'à son expiration.

#### <a name="code-samples"></a>Exemples de code
Consultez les exemples de code hello pour les scénarios d’Application de navigateur Web tooWeb. Et consultez régulièrement, car que nous ajoutons de nouveaux exemples tout temps hello. [Web Browser tooWeb Application](active-directory-code-samples.md#web-browser-to-web-application).

#### <a name="registering"></a>Inscription
* Client unique : Si vous générez une application simplement pour votre organisation, elle doit être inscrite dans le répertoire de votre entreprise à l’aide de hello portail Azure.
* Architecture mutualisée : Si vous générez une application qui peut être utilisée par les utilisateurs extérieurs à votre organisation, il doit être enregistré dans le répertoire de votre entreprise, mais également doit être inscrit dans le répertoire de chaque organisation qui utiliseront application hello. toomake votre application disponible dans leur annuaire, vous pouvez inclure un processus d’inscription pour les clients qui leur permet de tooconsent tooyour application. Lors de leur inscription pour votre application, ils seront affiche une boîte de dialogue qui affiche hello autorisations hello application ainsi puis hello option tooconsent. Selon les autorisations hello requis, un administrateur Bonjour autre organisation peut être requis toogive consentement. Quand hello utilisateur ou un administrateur a consenti, l’application hello est inscrit dans leur annuaire. Pour plus d’informations, consultez [Intégration d’applications dans Azure Active Directory](active-directory-integrating-applications.md).

#### <a name="token-expiration"></a>Expiration du jeton
Hello session utilisateur expire lorsque hello de durée de vie du jeton hello émis par Azure AD expire. Votre application peut raccourcir cette durée au besoin, par exemple en déconnectant les utilisateurs suite à une période d’inactivité. Lors de l’expiration de la session de hello, utilisateur de hello sera à nouveau invité à toosign dans.

### <a name="single-page-application-spa"></a>Application à page unique (SPA)
Cette section décrit les paramètres d’authentification pour une Application à Page unique, qui utilise Azure AD et autorisation implicite de OAuth 2.0 hello accorder toosecure mettre fin à son API web. Applications à Page unique sont généralement structurées sous la forme d’une couche de présentation JavaScript (frontale) qui s’exécute dans le navigateur de hello et API Web principale qui s’exécute sur un serveur et implémente hello logique métier de l’application. toolearn en savoir plus sur l’octroi d’autorisation implicite hello et déterminer s’il est adapté à votre scénario d’application, consultez [hello de présentation OAuth2 implicite accorder des flux dans Azure Active Directory](active-directory-dev-understanding-oauth2-implicit-grant.md).

Dans ce scénario, lorsque l’utilisateur de hello se connecte, hello JavaScript front end utilise [bibliothèque d’authentification Active Directory pour JavaScript (ADAL. JS)](https://github.com/AzureAD/azure-activedirectory-library-for-js/tree/dev) et autorisation implicite de hello accorder tooobtain un jeton d’ID (id_token) d’Azure AD. jeton de Hello est mis en cache et hello client le joint toohello demande en tant que jeton de support hello lors d’appels tooits API Web principale, qui est sécurisé à l’aide de l’intergiciel OWIN hello. 

#### <a name="diagram"></a>Diagramme
![Diagramme Application à page unique (SPA)](./media/active-directory-authentication-scenarios/single_page_app.png)

#### <a name="description-of-protocol-flow"></a>Description du flux du protocole
1. utilisateur de Hello accède l’application web de toohello.
2. application Hello retourne le navigateur de toohello hello JavaScript frontal (couche présentation).
3. utilisateur de Hello établit une connexion, par exemple en cliquant sur un lien de connexion. navigateur de Hello envoie un jeton d’ID à un toorequest de point de terminaison d’autorisation de GET toohello Azure AD. Cette demande inclut l’URL d’application hello ID et de réponse dans les paramètres de requête hello.
4. Azure AD valide hello QU'URL de réponse par rapport à hello inscrit les URL de réponse a été configuré dans hello portail Azure.
5. Hello utilisateur se connecte sur hello-page de connexion.
6. Si l’authentification réussit, Azure AD crée un jeton d’ID et le retourne en tant qu’URL de réponse d’URL fragment (#) toohello d’une application. Pour une application de production, cette URL de réponse doit être au format HTTPS. Hello renvoyé un jeton inclut des revendications sur utilisateur de hello et Azure AD qui sont requises par le jeton de hello application toovalidate hello.
7. Hello client du code JavaScript exécuté dans le navigateur de hello extrait le jeton de hello toouse de réponse hello dans sécuriser les appels d’API web de l’application toohello se terminer.
8. Bonjour à API web l’application hello navigateur appels principale avec le jeton d’accès hello dans l’en-tête d’autorisation hello.

#### <a name="code-samples"></a>Exemples de code
Consultez les exemples de code hello pour les scénarios d’Application de Page unique (SPA). Être toocheck vraiment arrière régulièrement, car nous ajoutons de nouveaux exemples tout temps hello. [Application à page unique (SPA)](active-directory-code-samples.md#single-page-application-spa).

#### <a name="registering"></a>Inscription
* Client unique : Si vous générez une application simplement pour votre organisation, elle doit être inscrite dans le répertoire de votre entreprise à l’aide de hello portail Azure.
* Architecture mutualisée : Si vous générez une application qui peut être utilisée par les utilisateurs extérieurs à votre organisation, il doit être enregistré dans le répertoire de votre entreprise, mais également doit être inscrit dans le répertoire de chaque organisation qui utiliseront application hello. toomake votre application disponible dans leur annuaire, vous pouvez inclure un processus d’inscription pour les clients qui leur permet de tooconsent tooyour application. Lors de leur inscription pour votre application, ils seront affiche une boîte de dialogue qui affiche hello autorisations hello application ainsi puis hello option tooconsent. Selon les autorisations hello requis, un administrateur Bonjour autre organisation peut être requis toogive consentement. Quand hello utilisateur ou un administrateur a consenti, l’application hello est inscrit dans leur annuaire. Pour plus d’informations, consultez [Intégration d’applications dans Azure Active Directory](active-directory-integrating-applications.md).

Après avoir inscrit l’application hello, il doit être configuré toouse protocole OAuth 2.0 Implicit Grant. Par défaut, ce protocole est désactivé pour les applications. tooenable hello protocole OAuth2 Implicit Grant pour votre application, modifier son manifeste d’application à partir de hello portail Azure et définir tootrue de valeur « oauth2AllowImplicitFlow » hello. Pour obtenir des instructions détaillées, consultez la rubrique [Activation de l’octroi implicite OAuth 2.0 pour les applications à page unique](active-directory-integrating-applications.md).

#### <a name="token-expiration"></a>Expiration du jeton
Lorsque vous utilisez ADAL.js toomanage authentification avec Azure AD, vous bénéficiez de plusieurs fonctionnalités qui facilitent l’actualisation d’un jeton expiré, ainsi que d’obtention de jetons pour les ressources d’API web supplémentaires qui peuvent être appelés par une application hello. Lorsque l’utilisateur de hello est correctement authentifié auprès d’Azure AD, une session sécurisée par un cookie est établie pour l’utilisateur hello entre le navigateur de hello et Azure AD. Il est important toonote que la session de hello existe entre l’utilisateur de hello et Azure AD et pas entre l’utilisateur de hello et application web de hello en cours d’exécution sur le serveur de hello. Lorsqu’un jeton arrive à expiration, ADAL.js utilise cette session toosilently obtenir un autre jeton. Il fait cela en utilisant un iFrame masqué de toosend et de réception de demande hello à l’aide du protocole OAuth Implicit Grant de hello. ADAL.js peut également utiliser ce même mécanisme toosilently obtenir des jetons d’accès d’Azure AD pour les autres web ressources d’API que hello application appelle tant que ces ressources prennent en charge des ressources cross-origin (CORS), de partage est enregistrés dans le répertoire de l’utilisateur hello, et tout consentement nécessaire a été spécifié par l’utilisateur de hello pendant la connexion.

### <a name="native-application-tooweb-api"></a>TooWeb Application native API
Cette section décrit l’appel d’une API web par une application native au nom d’un utilisateur. Ce scénario repose sur le type d’autorisation de grant code hello OAuth 2.0 avec un client public, comme décrit dans la section 4.1 de hello [spécification OAuth 2.0](http://tools.ietf.org/html/rfc6749). application native Hello Obtient un jeton d’accès pour l’utilisateur de hello à l’aide du protocole de hello OAuth 2.0. Ce jeton d’accès est ensuite envoyé dans hello demande toohello API web, qui autorise l’utilisateur de hello et retourne les ressources hello souhaité.

#### <a name="diagram"></a>Diagramme
![TooWeb Application native API diagramme](./media/active-directory-authentication-scenarios/native_app_to_web_api.png)

#### <a name="authentication-flow-for-native-application-tooapi"></a>Flux d’authentification de l’application native tooAPI
#### <a name="description-of-protocol-flow"></a>Description du flux du protocole
Si vous utilisez des bibliothèques d’authentification hello AD, la plupart des détails sur le protocole hello décrites ci-dessous est gérée pour vous, telles que la fenêtre contextuelle du navigateur hello, mise en cache de jeton et la gestion des jetons d’actualisation.

1. À l’aide d’un fenêtre contextuelle du navigateur, application native hello rend un point de terminaison d’autorisation de toohello demande dans Azure AD. Cette demande inclut hello ID d’Application et l’URI de l’application native hello de redirection de hello comme indiqué dans hello portail Azure et l’application hello URI ID d’API web de hello. Si l’utilisateur de hello n’a pas déjà connecté, ils sont à nouveau toosign demandée dans
2. Azure AD authentifie l’utilisateur de hello. Si c’est une application mutualisée et consentement est requis toouse hello application, utilisateur de hello sera tooconsent requis s’ils ne l’avez pas déjà fait. Après l’octroi de consentement et après une authentification réussie, Azure AD émet l’URI de redirection d’autorisation code réponse toohello précédent client d’une application.
3. Lorsque Azure AD émet une réponse de code d’autorisation précédent toohello URI de redirection, hello cesse de navigateur interaction et extraits hello d’autorisation code d’application cliente à partir de la réponse de hello. À l’aide de ce code d’autorisation, application cliente de hello envoie une demande de tooAzure d’AD jeton point de terminaison inclut le code d’autorisation de hello, plus d’informations sur hello application cliente (ID d’Application et l’URI de redirection) et hello ressource souhaitée (ID d’application URI pour l’API web de hello).
4. code d’autorisation de Hello et plus d’informations sur l’application cliente de hello et API web sont validés par Azure AD. Si la validation réussit, Azure AD renvoie deux jetons : un jeton d’accès JWT et un jeton d’actualisation JWT. En outre, Azure AD renvoie des informations de base sur l’utilisateur hello, telles que leur nom et le client l’ID complet.
5. Sur HTTPS, hello d’application cliente utilise hello retourné hello de tooadd jeton d’accès JWT chaîne JWT avec une désignation « Support » dans l’en-tête d’autorisation de hello d’API web toohello demande de hello. API web de Hello valide ensuite un jeton JWT hello, et si la validation est réussie, retourne hello souhaitée des ressources.
6. Expiration du jeton d’accès hello, hello client application reçoit une erreur indiquant que l’utilisateur hello doit tooauthenticate à nouveau. Si l’application hello possède un jeton d’actualisation valide, il peut être utilisé tooacquire un nouveau jeton d’accès sans demander confirmation hello toosign utilisateur dans une nouvelle fois. Si le jeton d’actualisation hello expire, application hello devez toointeractively s’authentifier à nouveau les utilisateur hello.

> [!NOTE]
> jeton d’actualisation Hello émis par Azure AD, tooaccess utilisé peut être plusieurs ressources. Par exemple, si vous avez une application cliente qui a des API web de toocall deux autorisations, jeton d’actualisation hello peut être utilisé également tooget une accès toohello jeton autres API web.
> 
> 

#### <a name="code-samples"></a>Exemples de code
Consultez les exemples de code hello pour les scénarios d’Application Native tooWeb API. Et consultez régulièrement, car que nous ajoutons de nouveaux exemples tout temps hello. [TooWeb Application native API](active-directory-code-samples.md#native-application-to-web-api).

#### <a name="registering"></a>Inscription
* Client unique : Les deux hello application native et l’API web de hello doit être inscrit dans hello même annuaire dans Azure AD. API web de Hello peut être configuré tooexpose un jeu d’autorisations, qui sont des ressources de tooits accès toolimit utilisé hello native de l’application. Hello application cliente sélectionne ensuite les autorisations hello souhaité à partir du menu hello déroulant « Autorisations tooOther Applications » Bonjour portail Azure.
* Architecture mutualisée : Tout d’abord, hello native application uniquement jamais inscrite dans hello développeur ou un répertoire du serveur de publication. En second lieu, application native hello est tooindicate configuré des autorisations hello unième toobe fonctionnel. Cette liste des autorisations requises s’affiche dans une boîte de dialogue lorsqu’un utilisateur ou un administrateur dans le répertoire de destination hello donne son consentement toohello application, ce qui le rend disponible tootheir organisation. Certaines applications requièrent des autorisations uniquement au niveau utilisateur, ce qui n’importe quel utilisateur dans l’organisation de hello peut accepter. Autres applications nécessitent des autorisations de niveau administrateur, auxquelles un utilisateur d’organisation de hello ne peut pas donner son consentement à. Un administrateur d’annuaire peut donner le consentement tooapplications qui requièrent ce niveau d’autorisations. Lorsque l’utilisateur de hello ou un administrateur a consenti, API web d’hello uniquement est inscrite dans leur annuaire. Pour plus d’informations, consultez [Intégration d’applications dans Azure Active Directory](active-directory-integrating-applications.md).

#### <a name="token-expiration"></a>Expiration du jeton
Lors de l’application native hello utilise son tooget de code d’autorisation un jeton d’accès JWT, elle reçoit aussi un jeton d’actualisation JWT. Expiration du jeton d’accès hello, jeton d’actualisation hello peut être utilisé toore-authentifier un utilisateur de hello sans qu’ils aient toosign de nouveau. Ce jeton d’actualisation est utilisé tooauthenticate hello utilisateur, ce qui aboutit à un nouvel accès des jetons et actualiser jeton.

### <a name="web-application-tooweb-api"></a>TooWeb d’Application Web API
Cette section décrit une application web qui a besoin de ressources tooget à partir d’une API web. Dans ce scénario, il existe deux types d’identité que hello application web peuvent utiliser tooauthenticate et appeler l’API web hello : une identité d’application ou une identité de l’utilisateur délégué.

*Identité de l’application :* ce utilise scénario tooauthenticate accordant des informations d’identification du client OAuth 2.0 en tant qu’application hello et hello d’accès web API. Lors de l’utilisation d’une identité d’application web hello API peut uniquement détecter que hello application web l’appelle, en tant que hello API web ne reçoit pas toutes les informations concernant l’utilisateur de hello. Si l’application hello reçoit des informations sur l’utilisateur de hello, il sera envoyé via le protocole d’application hello et il n’est pas signé par Azure AD. API web de Hello suppose qu’application web de hello authentifié utilisateur de hello. C’est pour cette raison que ce modèle est appelé « sous-système approuvé ».

*Identité d’utilisateur délégué* : ce scénario peut être obtenu de deux façons : OpenID Connect et octroi de code d’autorisation OAuth 2.0 avec un client confidentiel. application web de Hello Obtient un jeton d’accès pour l’utilisateur hello, qui s’avère toohello web API application web toohello hello utilisateur authentifié avec succès et que l’application web de hello a été en mesure de tooobtain un utilisateur délégué identité toocall hello API web. Ce jeton d’accès est envoyé dans hello demande toohello API web, qui autorise l’utilisateur de hello et retourne les ressources hello souhaité.

#### <a name="diagram"></a>Diagramme
![Diagramme d’Application tooWeb API de Web](./media/active-directory-authentication-scenarios/web_app_to_web_api.png)

#### <a name="description-of-protocol-flow"></a>Description du flux du protocole
Les deux hello l’identité de l’application et les types d’identité de l’utilisateur délégué sont décrits dans les flux hello ci-dessous. Hello leur principale différence est que hello déléguée identité de l’utilisateur doit acquérir tout d’abord un code d’autorisation avant que l’utilisateur de hello peut connectez-vous et avoir accès toohello web API.

##### <a name="application-identity-with-oauth-20-client-credentials-grant"></a>Identité d’application avec octroi d’informations d’identification client OAuth 2.0
1. Un utilisateur est connecté dans tooAzure AD dans l’application web de hello (voir hello [tooWeb de navigateur Web Application](#web-browser-to-web-application) ci-dessus).
2. application web de Hello doit tooacquire un jeton d’accès pour qu’il peut s’authentifier toohello web API et récupération de la ressource de hello souhaité. Il rend le point de terminaison token un tooAzure de demande d’AD, en fournissant des informations d’identification hello, ID d’Application et URI de l’ID d’application de l’API web.
3. Azure AD authentifie l’application hello et retourne un jeton d’accès JWT est utilisé toocall hello web API.
4. Sur HTTPS, application web de hello utilise hello retourné hello de tooadd jeton d’accès JWT chaîne JWT avec une désignation « Support » dans l’en-tête d’autorisation de hello d’API web toohello demande de hello. API web de Hello valide ensuite un jeton JWT hello, et si la validation est réussie, retourne hello souhaitée des ressources.

##### <a name="delegated-user-identity-with-openid-connect"></a>Identité d’utilisateur délégué avec OpenID Connect
1. Un utilisateur est connecté dans l’application web de tooa à l’aide d’Azure AD (voir hello [tooWeb de navigateur Web Application](#web-browser-to-web-application) section ci-dessus). Si l’utilisateur hello d’application web de hello n’a pas encore consenti tooallowing hello web toocall hello web application API sur son nom, l’utilisateur de hello doit tooconsent. application Hello affiche les autorisations hello que requises, et s’il une de ces autorisations de niveau administrateur, un utilisateur normal dans le répertoire de hello ne sera pas en mesure de tooconsent. Ce processus de consentement s’applique uniquement le locataire toomulti les applications, pas un seul locataire, comme application hello ont déjà les autorisations nécessaires de hello. Lorsque hello utilisateur connecté, application web de hello a reçu un jeton d’ID des informations sur l’utilisateur de hello, ainsi que d’un code d’autorisation.
2. À l’aide du code d’autorisation de hello émis par Azure AD, application web de hello envoie une demande de tooAzure d’AD jeton point de terminaison inclut le code d’autorisation de hello, plus d’informations sur l’application de client hello (ID d’Application et l’URI de redirection) et hello souhaitée (de ressources application URI d’ID pour hello web API).
3. code d’autorisation de Hello et plus d’informations sur l’application web de hello et API web sont validés par Azure AD. Si la validation réussit, Azure AD renvoie deux jetons : un jeton d’accès JWT et un jeton d’actualisation JWT.
4. Sur HTTPS, application web de hello utilise hello retourné hello de tooadd jeton d’accès JWT chaîne JWT avec une désignation « Support » dans l’en-tête d’autorisation de hello d’API web toohello demande de hello. API web de Hello valide ensuite un jeton JWT hello, et si la validation est réussie, retourne hello souhaitée des ressources.

##### <a name="delegated-user-identity-with-oauth-20-authorization-code-grant"></a>Identité d’utilisateur délégué avec octroi du code d’autorisation OAuth 2.0
1. Un utilisateur est déjà connecté dans l’application web de tooa, dont le mécanisme d’authentification est indépendant d’Azure AD.
2. Hello application web nécessite une autorisation code tooacquire un jeton d’accès, elle émet une demande via le point de terminaison hello navigateur tooAzure d’AD d’autorisation, en fournissant hello ID d’Application et l’URI de redirection de l’application web de hello après avoir réussi authentification. Hello utilisateur se connecte tooAzure AD.
3. Si l’utilisateur hello d’application web de hello n’a pas encore consenti tooallowing hello web toocall hello web application API sur son nom, l’utilisateur de hello doit tooconsent. application Hello affiche les autorisations hello que requises, et s’il une de ces autorisations de niveau administrateur, un utilisateur normal dans le répertoire de hello ne sera pas en mesure de tooconsent. Ce consentement s’applique tooboth unique et plusieurs locataires de l’application.  Dans les cas d’un seul locataire hello, un administrateur peut effectuer tooconsent de consentement d’administration pour le compte de leurs utilisateurs.  Cela est possible à l’aide de hello `Grant Permissions` bouton Bonjour [Azure Portal](https://portal.azure.com). 
4. Une fois hello utilisateur a consenti, application web de hello reçoit code d’autorisation de hello qu’il doit tooacquire un jeton d’accès.
5. À l’aide du code d’autorisation de hello émis par Azure AD, application web de hello envoie une demande de tooAzure d’AD jeton point de terminaison inclut le code d’autorisation de hello, plus d’informations sur l’application de client hello (ID d’Application et l’URI de redirection) et hello souhaitée (de ressources application URI d’ID pour hello web API).
6. code d’autorisation de Hello et plus d’informations sur l’application web de hello et API web sont validés par Azure AD. Si la validation réussit, Azure AD renvoie deux jetons : un jeton d’accès JWT et un jeton d’actualisation JWT.
7. Sur HTTPS, application web de hello utilise hello retourné hello de tooadd jeton d’accès JWT chaîne JWT avec une désignation « Support » dans l’en-tête d’autorisation de hello d’API web toohello demande de hello. API web de Hello valide ensuite un jeton JWT hello, et si la validation est réussie, retourne hello souhaitée des ressources.

#### <a name="code-samples"></a>Exemples de code
Consultez les exemples de code hello pour les scénarios d’Application Web tooWeb API. Et consultez régulièrement, car que nous ajoutons de nouveaux exemples tout temps hello. Web [tooWeb de l’Application API](active-directory-code-samples.md#web-application-to-web-api).

#### <a name="registering"></a>Inscription
* Client unique : Hello pour l’identité de l’application hello et cas d’identité de l’utilisateur délégué, application web et l’API web de hello doit être inscrit dans hello même annuaire dans Azure AD. API web de Hello peut être configuré tooexpose un jeu d’autorisations, qui sont des ressources de l’application web toolimit utilisé hello accès tooits. Si un type d’identité de l’utilisateur délégué est utilisé, application web de hello doit tooselect les autorisations de hello souhaité à partir du menu hello déroulant « Autorisations tooOther Applications » Bonjour portail Azure. Cette étape n’est pas requise si le type d’identité application hello est utilisé.
* Architecture mutualisée : Tout d’abord, application web de hello tooindicate configuré hello autorisations est unième toobe fonctionnel. Cette liste des autorisations requises s’affiche dans une boîte de dialogue lorsqu’un utilisateur ou un administrateur dans le répertoire de destination hello donne son consentement toohello application, ce qui le rend disponible tootheir organisation. Certaines applications requièrent des autorisations uniquement au niveau utilisateur, ce qui n’importe quel utilisateur dans l’organisation de hello peut accepter. Autres applications nécessitent des autorisations de niveau administrateur, auxquelles un utilisateur d’organisation de hello ne peut pas donner son consentement à. Un administrateur d’annuaire peut donner le consentement tooapplications qui requièrent ce niveau d’autorisations. Lorsque des autorisations utilisateur ou un administrateur, hello hello web API web d’application et de hello sont inscrits dans leur annuaire.

#### <a name="token-expiration"></a>Expiration du jeton
Lors de l’application web de hello utilise son tooget de code d’autorisation un jeton d’accès JWT, elle reçoit aussi un jeton d’actualisation JWT. Expiration du jeton d’accès hello, jeton d’actualisation hello peut être utilisé toore-authentifier un utilisateur de hello sans qu’ils aient toosign de nouveau. Ce jeton d’actualisation est utilisé tooauthenticate hello utilisateur, ce qui aboutit à un nouvel accès des jetons et actualiser jeton.

### <a name="daemon-or-server-application-tooweb-api"></a>Application démon ou serveur tooWeb API
Cette section décrit une application démon ou serveur qui a besoin de ressources tooget à partir d’une API web. Il existe deux scénarios secondaire qui s’appliquent toothis section : un démon qui doit toocall une API web, basée sur le type d’octroi d’informations d’identification du client OAuth 2.0 ; et une application serveur (par exemple, une API web) qui doit toocall une API web, généré sur le projet de spécification OAuth 2.0 On-Behalf-Of.

Pour le scénario de hello lorsqu’une application démon doit toocall une API web, il est important toounderstand quelques éléments. Tout d’abord, l’intervention de l’utilisateur n’est pas possible avec une application démon, ce qui nécessite hello application toohave sa propre identité. Un exemple d’application démon est un traitement par lots ou un service de système d’exploitation en cours d’exécution en arrière-plan de hello. Ce type d’application demande un jeton d’accès à l’aide de son identité d’application et présentant son ID d’Application, les informations d’identification (mot de passe ou certificat) et tooAzure URI ID d’application AD. Après une authentification réussie, démon de hello reçoit un jeton d’accès à partir d’Azure AD, qui est alors utilisé toocall hello API web.

Pour le scénario de hello lorsqu’une application serveur doit toocall une API web, il est utile toouse un exemple. Imaginez qu’un utilisateur authentifié sur une application native et que cette application native doit toocall une API web. Azure AD émet un jeton Web JSON accès toocall jeton hello API web. Si l’API web de hello doit toocall une autre API web en aval, il peut utiliser hello sur à la place de flux toodelegate hello l’identité d’utilisateur et authentifier des API web de deuxième niveau toohello.

#### <a name="diagram"></a>Diagramme
![Diagramme de tooWeb API Application démon ou serveur](./media/active-directory-authentication-scenarios/daemon_server_app_to_web_api.png)

#### <a name="description-of-protocol-flow"></a>Description du flux du protocole
##### <a name="application-identity-with-oauth-20-client-credentials-grant"></a>Identité d’application avec octroi d’informations d’identification client OAuth 2.0
1. Application de serveur hello doit tout d’abord, tooauthenticate avec Azure AD en tant que telle, sans intervention humaine, par exemple une boîte de dialogue Ouverture de session interactive. Il rend le point de terminaison token un tooAzure de demande d’AD, en fournissant des informations d’identification hello, ID d’Application et l’URI de l’ID d’application.
2. Azure AD authentifie l’application hello et retourne un jeton d’accès JWT est utilisé toocall hello web API.
3. Sur HTTPS, application web de hello utilise hello retourné hello de tooadd jeton d’accès JWT chaîne JWT avec une désignation « Support » dans l’en-tête d’autorisation de hello d’API web toohello demande de hello. API web de Hello valide ensuite un jeton JWT hello, et si la validation est réussie, retourne hello souhaitée des ressources.

##### <a name="delegated-user-identity-with-oauth-20-on-behalf-of-draft-specification"></a>Identité d’utilisateur délégué avec spécification préliminaire « Au nom de » OAuth 2.0
flux de Hello présenté ci-après présume qu’un utilisateur a été authentifié sur une autre application (par exemple, une application native), et que leur identité d’utilisateur a été utilisé tooacquire une API web de premier niveau du jeton toohello accès.

1. application native Hello envoie web de premier niveau jeton toohello hello accès API.
2. API web de premier niveau Hello envoie le point de terminaison token un tooAzure de demande d’AD, en fournissant son ID d’Application et les informations d’identification, ainsi que les hello jeton d’accès utilisateur. En outre, la demande de hello est envoyée avec un on_behalf_of paramètre indiquant hello web API demande nouveaux jetons toocall une API web en aval pour le compte d’utilisateur d’origine de hello.
3. Azure AD vérifie que web de premier niveau hello API dispose d’autorisations tooaccess hello web de deuxième niveau API et valide la demande de hello, retournant qu'un jeton d’accès JWT et un jeton Web JSON actualiser toohello jeton web de premier niveau API.
4. Sur HTTPS, web de premier niveau hello puis d’appels d’API hello API web de deuxième niveau en ajoutant la chaîne de jeton hello dans l’en-tête d’autorisation hello dans la demande hello. API web de premier niveau Hello peut continuer web de deuxième niveau hello toocall API tant que le jeton d’accès hello et jetons d’actualisation sont valides.

#### <a name="code-samples"></a>Exemples de code
Consultez les exemples de code hello pour les scénarios de tooWeb API Application démon ou serveur. Et consultez régulièrement, car que nous ajoutons de nouveaux exemples tout temps hello. [Application serveur ou démon tooWeb API](active-directory-code-samples.md#server-or-daemon-application-to-web-api)

#### <a name="registering"></a>Inscription
* Client unique : Pour l’identité de l’application hello et cas d’identité de l’utilisateur délégué, hello démon ou une application serveur doit être inscrit Bonjour même annuaire dans Azure AD. API web de Hello peut être configuré tooexpose un jeu d’autorisations qui sont le démon de hello toolimit utilisé ou les ressources de tooits d’accès du serveur. Si un type d’identité de l’utilisateur délégué est utilisé, application de serveur hello doit tooselect les autorisations de hello souhaité à partir du menu hello déroulant « Autorisations tooOther Applications » Bonjour portail Azure. Cette étape n’est pas requise si le type d’identité application hello est utilisé.
* Architecture mutualisée : Tout d’abord, application démon ou serveur de hello tooindicate configuré hello autorisations est unième toobe fonctionnel. Cette liste des autorisations requises s’affiche dans une boîte de dialogue lorsqu’un utilisateur ou un administrateur dans le répertoire de destination hello donne son consentement toohello application, ce qui le rend disponible tootheir organisation. Certaines applications requièrent des autorisations uniquement au niveau utilisateur, ce qui n’importe quel utilisateur dans l’organisation de hello peut accepter. Autres applications nécessitent des autorisations de niveau administrateur, auxquelles un utilisateur d’organisation de hello ne peut pas donner son consentement à. Un administrateur d’annuaire peut donner le consentement tooapplications qui requièrent ce niveau d’autorisations. Lorsque l’utilisateur de hello ou un administrateur a consenti, les deux API web de hello sont inscrits dans leur annuaire.

#### <a name="token-expiration"></a>Expiration du jeton
Lors de la première application de hello utilise son tooget de code d’autorisation un jeton d’accès JWT, elle reçoit aussi un jeton d’actualisation JWT. Expiration du jeton d’accès hello, jeton d’actualisation hello peut être utilisé toore-authentifier un utilisateur de hello sans demander les informations d’identification. Ce jeton d’actualisation est utilisé tooauthenticate hello utilisateur, ce qui aboutit à un nouvel accès des jetons et actualiser jeton.

## <a name="see-also"></a>Voir aussi
[Guide du développeur Azure Active Directory](active-directory-developers-guide.md)

[Exemples de code Azure Active Directory](active-directory-code-samples.md)

[Informations importantes sur la substitution des clés de signature dans Azure AD](active-directory-signing-key-rollover.md)

[OAuth 2.0 dans Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx)

