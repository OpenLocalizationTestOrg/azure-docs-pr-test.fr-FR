---
title: aaaIntegrating Applications avec Azure Active Directory | Documents Microsoft
description: "Détails sur la manière tooadd, mettre à jour ou supprimer une application dans Azure Active Directory (Azure AD)."
services: active-directory
documentationcenter: 
author: lnalepa
manager: mbaldwin
editor: mbaldwin
ms.assetid: ae637be5-0b71-4b1e-b1fe-b83df3eb4845
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: lenalepa
ms.custom: aaddev
ms.reviewer: luleon
ms.openlocfilehash: c6bf1123bb3a4d78b55c1c55558e684fb844e687
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-applications-with-azure-active-directory"></a>Intégration d’applications dans Azure Active Directory
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Les développeurs d’entreprise et les fournisseurs de logiciels-as-a-service (SaaS) peuvent développer des services cloud commerciaux ou des applications métier qui peut être intégré à Azure Active Directory tooprovide (Azure AD) sécurisé se connecter et d’autorisation pour leurs Services. toointegrate une application ou un service auprès d’Azure AD, un développeur doit inscrire tout d’abord hello plus d’informations sur leur application auprès d’Azure AD via hello portail Azure classic.

Cet article vous explique comment tooadd, mettre à jour ou supprimer une application dans Azure AD. Vous allez découvrir hello différents types d’applications qui peuvent être intégrées à Azure AD, comment tooconfigure votre tooaccess applications autres ressources telles que les API web et bien plus encore.

toolearn savoir plus sur les objets Azure AD deux hello qui représentent une application inscrite et la relation hello entre elles, consultez [les objets de Principal du Service et Application](active-directory-application-objects.md); toolearn plus d’informations sur les instructions de personnalisation de hello vous doit utiliser lors du développement d’applications avec Azure Active Directory, consultez [instructions de personnalisation pour les applications intégrées](active-directory-branding-guidelines.md).

## <a name="adding-an-application"></a>Ajout d'une application
Toute application qui souhaite que les fonctionnalités de hello toouse d’Azure AD doit d’abord être enregistrée dans un locataire Azure AD. Ce processus d’inscription implique la fourniture à Azure AD de détails sur votre application, par exemple, les URL hello où il est situé, hello URL toosend réponses après qu’un utilisateur est authentifié, hello URI qui identifie l’application hello et ainsi de suite.

Si vous créez une application web qui doit juste toosupport connectez-vous pour les utilisateurs dans Azure AD, vous pouvez simplement suivre les instructions hello ci-dessous. Si votre application a besoin d’informations d’identification ou des autorisations tooaccess tooa web API ou doit tooallow les utilisateurs à partir d’autres les locataires Azure AD tooaccess, consultez [mise à jour d’une Application](#updating-an-application) toocontinue section Configuration de votre application.

### <a name="tooregister-a-new-application-in-hello-azure-portal"></a>tooregister une nouvelle application Bonjour portail Azure
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Choisissez votre locataire Azure AD en sélectionnant votre compte dans hello coin supérieur droit de la page de hello.
3. Dans le volet de navigation gauche hello, choisissez **plus Services**, cliquez sur **inscriptions d’application**, puis cliquez sur **ajouter**.
4. Suivez les invites hello et créez une nouvelle application. Si vous souhaitez des exemples spécifiques pour les applications web ou natives, consultez les [Démarrages rapides](active-directory-developers-guide.md).
  * Pour les Applications Web, indiquez hello **URL de connexion**, qui est hello les URL de base de votre application, où les utilisateurs peuvent se connecter par exemple `http://localhost:12345`.
<!--TODO: add once App ID URI is configurable: hello **App ID URI** is a unique identifier for your application. hello convention is toouse `https://<tenant-domain>/<app-name>`, e.g. `https://contoso.onmicrosoft.com/my-first-aad-app`-->
  * Pour les Applications natives, vous devez fournir un **URI de redirection**, quels Azure AD utilise des réponses de jeton tooreturn. Entrez une application tooyour spécifique de la valeur,. exemple :`http://MyFirstAADApp`
5. Une fois que vous avez terminé l’inscription, Azure AD assigne à votre application un identificateur client unique, hello ID d’Application. Votre application a été ajoutée, et vous serez dirigé toohello la page de démarrage rapide pour votre application. Selon que votre application est un rôle web ou application native, vous verrez des différentes options sur l’application de tooyour tooadd des fonctionnalités supplémentaires. Une fois que votre application a été ajoutée, vous pouvez mettre à jour votre toosign d’utilisateurs tooenable application dans web access API dans d’autres applications, ou configurer l’application mutualisée (ce qui permet à votre application autres tooaccess organisations).

> [!NOTE]
> Par défaut, inscription d’application hello nouvellement créé est tooallow configuré des utilisateurs à partir de votre toosign active dans tooyour application.
> 
> 

## <a name="updating-an-application"></a>Mise à jour d’une application
Une fois que votre application a été inscrit auprès d’Azure AD, elle peut avoir besoin toobe mis à jour tooprovide tooweb API d’accès, être disponible dans d’autres organisations et bien plus encore. Cette section décrit les différentes façons dans lesquelles vous devrez peut-être tooconfigure davantage votre application. Tout d’abord, nous allons commencer avec une vue d’ensemble de hello infrastructure de consentement, qui est toounderstand important si vous générez des applications API des ressources qui seront utilisées par les applications clientes générées par les développeurs de votre organisation ou une autre organisation.

Pour plus d’informations sur hello d’authentification fonctionne dans Azure AD, consultez [scénarios d’authentification pour Azure AD](active-directory-authentication-scenarios.md).

### <a name="overview-of-hello-consent-framework"></a>Vue d’ensemble de l’infrastructure de consentement hello
Infrastructure de consentement d’Azure AD rend facile toodevelop web à plusieurs locataires et les applications clientes natives qui doivent tooaccess web API sécurisés par un locataire Azure AD, différent de hello où l’application cliente de hello est inscrit. Ces API web incluent hello Microsoft Graph API (tooaccess Azure Active Directory, Intune et services Office 365) et autres API des services Microsoft, en outre tooyour propre API web. infrastructure de Hello est basée sur un utilisateur ou un administrateur fournissant consentement tooan application demandant toobe inscrites dans leur annuaire, ce qui peut impliquer l’accès aux données d’annuaire.

Par exemple, si une application cliente web doit tooread Calendrier informations hello utilisateur à partir d’Office 365, cet utilisateur sera requis tooconsent toohello client application. Une fois le consentement reçu, hello client application être en mesure de toocall hello Microsoft Graph API pour le compte d’utilisateur de hello et utiliser les informations relatives au calendrier hello en fonction des besoins. Hello [Microsoft Graph API](https://graph.microsoft.io) fournit toodata d’accès dans Office 365 (par exemple, les calendriers et les messages à partir d’Exchange, des sites et des listes SharePoint, les documents à partir de OneDrive, les ordinateurs portables à partir de OneNote, tâches du planificateur, les classeurs à partir de Excel, etc.), ainsi que les utilisateurs et groupes d’Azure AD et autres objets de données à partir de plusieurs services de cloud de Microsoft. 

infrastructure de consentement Hello repose sur OAuth 2.0 et ses différents flux, telles que du code d’autorisation accordez des informations d’identification client et d’accorder, à l’aide des clients publics ou confidentiels. En utilisant OAuth 2.0, Azure AD rend possible toobuild nombreux différents types d’applications clientes, comme sur un téléphone, tablette, serveur ou une application web et accéder à des ressources de toohello requis.

Pour plus d’informations sur l’infrastructure de consentement hello, consultez [OAuth 2.0 dans Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx), [scénarios d’authentification pour Azure AD](active-directory-authentication-scenarios.md)et pour plus d’informations sur l’obtention d’un accès autorisé tooOffice 365 via Microsoft Graph, consultez [authentification de l’application avec Microsoft Graph](https://graph.microsoft.io/docs/authorization/auth_overview).

#### <a name="example-of-hello-consent-experience"></a>Exemple d’expérience de consentement hello
Hello suivants étapes vont vous montrer le fonctionnement de consentement hello pour développeur d’applications hello et utilisateur.

1. Sur la page configuration de votre application cliente web hello portail Azure, définir des autorisations de hello que requiert de votre application à l’aide des menus de hello Bonjour section des autorisations requises.
   
    ![Autorisations tooother applications](./media/active-directory-integrating-applications/requiredpermissions.png)
2. Considérez que les autorisations de votre application ont été mis à jour, application hello est en cours d’exécution et un utilisateur est-il sur toouse pour hello première fois. Si l’application hello n’a pas encore acquis une application hello jeton, d’accès ou d’actualisation doit tooobtain de point de terminaison d’autorisation toogo tooAzure d’AD un code d’autorisation qui peut être utilisé tooacquire un nouvel accès et un jeton d’actualisation.
3. Si l’utilisateur de hello n’est pas déjà authentifié, elles sont demandées toosign dans tooAzure AD.
   
    ![Connexion utilisateur ou un administrateur tooAzure AD](./media/active-directory-integrating-applications/usersignin.png)
4. Une fois hello utilisateur connecté, Azure AD déterminent si les utilisateur hello doit toobe indiqué une page de consentement. Ce choix est basé sur indique si les utilisateurs de hello (ou l’administrateur de leur organisation) a déjà accordé consentement d’application hello. Si le consentement n’a pas déjà été accordé, Azure AD invite utilisateur hello à donner son consentement et affiche les autorisations hello requis dont il a besoin toofunction. jeu de Hello d’autorisations qui s’affiche dans la boîte de dialogue de consentement hello sont hello identique à ce qui a été sélectionné dans hello des autorisations déléguées Bonjour portail Azure.
   
    ![Expérience de consentement de l'utilisateur](./media/active-directory-integrating-applications/consent.png)
5. Une fois que l’utilisateur de hello donne son consentement, un code d’autorisation est retourné tooyour application, ce qui peut être échangé tooacquire un jeton d’accès et jeton d’actualisation. Pour plus d’informations sur ce flux, consultez hello [web section tooweb API d’Application](active-directory-authentication-scenarios.md#web-application-to-web-api) section [scénarios d’authentification pour Azure AD](active-directory-authentication-scenarios.md).

6. En tant qu’administrateur, vous pouvez également donner son consentement autorisations déléguées de l’application tooan pour le compte de tous les utilisateurs de hello dans votre client. Cela empêchera la boîte de dialogue de consentement hello d’apparaître pour chaque utilisateur de client de hello. Vous pouvez les spécifier cela via hello [portail Azure](https://portal.azure.com) à partir de votre page d’application. À partir de hello **paramètres** panneau pour votre application, cliquez sur **autorisations requises** , puis cliquez sur hello **accorder des autorisations** bouton. 

    ![Accorder des autorisations pour un consentement administrateur explicite](./media/active-directory-integrating-applications/grantpermissions.png)
    
> [!NOTE]
> L’octroi de consentement explicite à l’aide de hello **accorder des autorisations** bouton est actuellement requis pour les applications à page unique (SPA) à l’aide de ADAL.js, comme le jeton d’accès hello est demandé sans une invite de consentement, échoue si un accord n’est pas déjà accordée.   

### <a name="configuring-a-client-application-tooaccess-web-apis"></a>Configuration d’un ordinateur client application tooaccess web API
Dans l’ordre pour un web/confidentielles client application toobe en mesure de tooparticipate dans un flux d’octroi d’autorisation qui requiert l’authentification (et obtenir un jeton d’accès), il doit établir les informations d’identification sécurisées. méthode d’authentification par défaut Hello pris en charge par hello portail Azure est l’ID de Client + clé symétrique. Cette section couvre hello configuration étapes tooprovide requis hello une clé secrète informations d’identification de votre client.

En outre, avant d’un client pouvant accès une API web exposées par une application de ressource (ie : l’API Microsoft Graph), infrastructure de consentement hello permettra de client de la hello obtient hello autorisation autorisations requis, en fonction de hello demandées. Par défaut, toutes les applications peuvent choisir des autorisations à partir d’Azure Active Directory (API graphique) et les API de Service Management Azure, avec l’autorisation « activer l’authentification et profil de la lecture de l’utilisateur » hello Azure AD déjà sélectionnée par défaut. Si votre application cliente est en cours d’enregistrement dans un locataire Azure AD Office 365, vous aurez également la possibilité de sélectionner les API web et les autorisations pour Exchange Online et SharePoint. Vous pouvez sélectionner à partir de [deux types d’autorisations](active-directory-dev-glossary.md#permissions) Bonjour déroulants toohello suivant souhaité web API :

* Autorisations d’application : Votre application cliente doit tooaccess hello web API directement en tant que telle (sans contexte utilisateur). Ce type d'autorisation requiert le consentement de l'administrateur et n'est également pas disponible pour les applications clientes natives.
* Autorisations déléguées : Votre application cliente doit tooaccess hello web API en tant qu’utilisateur connecté hello, mais avec un accès limité par l’autorisation de hello sélectionné. Ce type d’autorisation peut être accordé par un utilisateur, sauf si l’autorisation de hello est configurée comme nécessitant le consentement de l’administrateur. 

> [!NOTE]
> Ajout d’une application de tooan d’autorisation déléguée n’accorde pas automatiquement les utilisateurs toohello de consentement dans le locataire de hello, comme il le faisait Bonjour portail classique Azure. Hello utilisateurs doivent exécuter manuellement donner son accord pour hello ajouté délégué des autorisations lors de l’exécution, à moins que l’administrateur de hello clique hello **accorder des autorisations** bouton hello **autorisations requises** section de la page d’application hello Bonjour portail Azure. 

#### <a name="tooadd-credentials-or-permissions-tooaccess-web-apis"></a>informations d’identification tooadd ou tooaccess des autorisations web API
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Choisissez votre locataire Azure AD en sélectionnant votre compte dans hello coin supérieur droit de la page de hello.
3. Dans le menu supérieur de hello, choisissez **Azure Active Directory**, cliquez sur **inscriptions d’application**et puis cliquez sur application hello tooconfigure. Cela sera vous prendre la page de démarrage rapide de l’application toohello, ainsi qu’ouvrir le panneau des paramètres pour l’application hello hello.
4. tooadd une clé secrète pour les informations d’identification de votre application web, cliquez sur la section « Clés » de hello à partir du Panneau de paramètres hello.  
   
   * Ajoutez une description pour votre clé et sélectionnez une durée de 1 ou 2 ans. 
   * colonne la plus à droite de Hello contiendra la valeur de clé hello, après avoir enregistré les modifications de configuration hello. Toocome que retour toothis section et copie il après avoir appuyé sur Enregistrer, vous devrez pour utilisent dans votre application cliente lors de l’authentification au moment de l’exécution.
5. tooadd autorisations tooaccess les API de ressources à partir de votre client, cliquez sur la section « Autorisations requises » de hello à partir du Panneau de paramètres hello. 
   
   * Tout d’abord, cliquez sur le bouton « Ajouter » de hello.
   * Cliquez sur « Sélectionner un API » tooselect hello souhaité toopick à partir de ressources.
   * Parcourir la liste hello des API disponibles ou utilisez tooselect de zone de recherche hello à partir d’applications de ressource disponible hello dans votre annuaire qui exposent une API web. Cliquez sur la ressource hello vous intéressez, puis cliquez sur **sélectionnez**.
   * Une fois sélectionné, vous pouvez déplacer toohello **autorisations Select** menu, où vous pouvez sélectionner hello « autorisations d’Application » et « Autorisations déléguées » pour votre application.
   
6. Lorsque vous avez terminé, cliquez sur hello **fait** bouton.

> [!NOTE]
> En cliquant sur hello **fait** bouton définit aussi automatiquement les autorisations hello pour votre application dans votre annuaire selon les autorisations hello tooother les applications que vous avez configuré.  Vous pouvez afficher ces autorisations de l’application en examinant application hello **paramètres** panneau.
> 
> 

### <a name="configuring-a-resource-application-tooexpose-web-apis"></a>Configuration d’un site web tooexpose d’application de ressource API
Vous pouvez développer une API web et rendre les applications disponibles tooclient en exposant accès [étendues](active-directory-dev-glossary.md#scopes) et [rôles](active-directory-dev-glossary.md#roles). Une API web correctement configurée est rendue disponible comme hello autres API web Microsoft, y compris hello API Graph et hello API Office 365. Les étendues d’accès sont exposées par le biais du [manifeste de votre application](active-directory-dev-glossary.md#application-manifest), c’est-à-dire un fichier JSON représentant la configuration d’identité de votre application.  

Hello après section va vous montrer comment tooexpose accès étendues, en modifiant le manifeste de l’application de ressource hello.

#### <a name="adding-access-scopes-tooyour-resource-application"></a>Ajout d’application de ressource d’accès étendues tooyour
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Choisissez votre locataire Azure AD en sélectionnant votre compte dans hello coin supérieur droit de la page de hello.
3. Dans le menu supérieur de hello, choisissez **Azure Active Directory**, cliquez sur **inscriptions d’application**et puis cliquez sur application hello tooconfigure. Cela sera vous prendre la page de démarrage rapide de l’application toohello, ainsi qu’ouvrir le panneau des paramètres pour l’application hello hello.
4. Cliquez sur **manifeste** de hello application page tooopen hello manifeste éditeur inline. 
5. Remplacez « oauth2Permissions » nœud hello suivant extrait de code JSON. Cet extrait de code est un exemple de comment tooexpose une étendue connue en tant que « emprunt d’identité », qui permet un toogive du propriétaire de la ressource à une application cliente, un type de délégué accès tooa ressource. Assurez-vous de modifier les valeurs et le texte de hello pour votre propre application :
   
        "oauth2Permissions": [
        {
            "adminConsentDescription": "Allow hello application full access toohello Todo List service on behalf of hello signed-in     user",
            "adminConsentDisplayName": "Have full access toohello Todo List service",
            "id": "b69ee3c9-c40d-4f2a-ac80-961cd1534e40",
            "isEnabled": true,
            "type": "User",
            "userConsentDescription": "Allow hello application full access toohello todo service on your behalf",
            "userConsentDisplayName": "Have full access toohello todo service",
            "value": "user_impersonation"
            }
        ],
   
    valeur d’id Hello doit être un nouveau GUID généré que vous créez en utilisant un [outil de génération de GUID](https://msdn.microsoft.com/library/ms241442%28v=vs.80%29.aspx) ou par programme. Il représente un identificateur unique pour l’autorisation de hello qui est exposé par l’API web de hello. Une fois que votre client est configuré correctement API toorequest tooyour web à l’accès et les appels hello API web, il présente un jeton OAuth 2.0 JWT a hello étendue (scp) revendication toohello valeur définie ci-dessus, qui dans ce cas est user_impersonation.
   
   > [!NOTE]
   > Vous pouvez exposer des étendues supplémentaires ultérieurement si nécessaire. Considérez que votre API web peut exposer plusieurs étendues associées à un éventail de fonctions différentes. Vous pouvez désormais contrôler les accès toohello API web à l’aide hello étendue (scp) revendication dans le jeton OAuth 2.0 JWT de salutation reçu.
   > 
   > 
6. Cliquez sur **enregistrer** manifeste de hello toosave. Votre site web QU'API est désormais configuré toobe utilisé par d’autres applications dans votre annuaire.

#### <a name="tooverify-hello-web-api-is-exposed-tooother-applications-in-your-directory"></a>API web de hello tooverify est exposé tooother des applications dans votre annuaire
1. Dans le menu supérieur de hello, cliquez sur **inscriptions d’application**, sélectionnez hello souhaité application client tooconfigure accès toohello web API et accédez toohello panneau des paramètres.
2. À partir de hello **autorisations requises** , sélectionnez hello web API que vous venez d’exposer une autorisation. À partir du menu déroulant d’autorisations déléguées hello, sélectionnez une nouvelle autorisation hello.

![Les autorisations de la liste des tâches sont affichées.](./media/active-directory-integrating-applications/todolistpermissions.png)

#### <a name="more-on-hello-application-manifest"></a>Plus d’informations sur le manifeste de l’application hello
manifeste de l’application Hello sert en fait un mécanisme de mise à jour d’entité d’Application hello, qui définit tous les attributs de la configuration d’identité d’une application Azure AD, y compris les étendues d’accès API hello évoqué. Pour plus d’informations sur hello entité d’Application, consultez hello [documentation d’entité Application d’API Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity). Dans, vous trouverez des informations de référence complètes sur les autorisations de toospecify hello Application entité membres utilisés pour votre API :  

* membre d’appRoles Hello, qui est une collection de [AppRole](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#approle-type) les entités qui peuvent être utilisés toodefine hello **autorisations d’Application** pour une API web  
* membre d’oauth2Permissions Hello, qui est une collection de [OAuth2Permission](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permission-type) les entités qui peuvent être utilisés toodefine hello **autorisations déléguées** pour une API web

Pour plus d’informations sur l’application des concepts manifestes en général, consultez trop[manifeste d’application Azure Active Directory compréhension hello](active-directory-application-manifest.md).

### <a name="accessing-hello-azure-ad-graph-and-office-365-via-microsoft-graph-apis"></a>L’accès aux hello Azure AD Graph et Office 365 via Microsoft Graph API  
Comme mentionnées précédemment, en outre tooexposing / l’accès aux API sur vos propres applications de la ressource, vous pouvez également mettre à jour votre tooaccess d’application client API exposées par les ressources de Microsoft.  Bonjour API Microsoft Graph, qui est appelée « Microsoft Graph » dans la liste de hello d’autorisations tooother applications, n’est disponible ou toutes les applications qui sont inscrits auprès d’Azure AD. Si vous inscrivez votre application cliente dans un locataire Azure AD qui a été configuré par Office 365, vous pouvez également accéder toutes les autorisations hello exposées par hello Microsoft Graph API toovarious ressources Office 365.

Pour obtenir une présentation complète des étendues d’accès exposé par l’API Graph, consultez hello [étendues d’autorisation | Concepts de l’API Microsoft Graph](https://graph.microsoft.io/docs/authorization/permission_scopes) l’article.

> [!NOTE]
> En raison de la limite actuelle de tooa, les applications clientes natives peuvent uniquement appeler hello API Azure AD Graph s’ils utilisent l’autorisation « Accéder à l’annuaire de votre organisation » de hello.  Cette restriction ne s'applique pas aux applications web.
> 
> 

### <a name="configuring-multi-tenant-applications"></a>Configuration d'applications multilocataires
Lorsque vous ajoutez un tooAzure application Active Directory, vous pouvez mettre votre toobe application accessible uniquement par les utilisateurs de votre organisation. Vous pouvez également votre toobe application accessible aux utilisateurs des organisations externes. Ces deux types d’applications sont appelés applications à locataire unique et applications multilocataires. Vous pouvez modifier la configuration hello d’un toomake d’application mono-utilisateur il une application mutualisée, cette section décrit ci-dessous.

Il est important toonote hello différences à locataire unique et une application mutualisée :  

* Une application à locataire unique est prévue pour une utilisation dans une seule organisation. Il s’agit généralement d’une application métier écrite par un développeur de l’entreprise. Une application à locataire unique doit uniquement toobe accessible aux utilisateurs dans un répertoire, et par conséquent, il doit uniquement toobe configuré dans un répertoire.
* Une application multilocataire est prévue pour une utilisation dans plusieurs organisations. Il s’agit d’une application SaaS (software-as-a-service) web généralement écrite par un éditeur de logiciels indépendant. Applications mutualisées doivent toobe configuré dans chaque répertoire dans lequel ils seront utilisés, ce qui nécessite tooregister de consentement utilisateur ou un administrateur, les prises en charge via l’infrastructure de consentement hello Azure AD. Notez que toutes les applications clientes natives sont mutualisées par défaut qu’ils sont installés sur les appareils du propriétaire des ressources hello. Consultez hello vue d’ensemble de hello infrastructure de consentement ci-dessus pour plus d’informations sur l’infrastructure de consentement hello.

#### <a name="enabling-external-users-toogrant-your-application-access-tootheir-resources"></a>L’activation des utilisateurs externes toogrant vos ressources d’application accès tootheir
Si vous écrivez une application que vous souhaitez toomake tooyour disponible clients ou partenaires en dehors de votre organisation, vous devez la définition de l’application hello tooupdate Bonjour portail Azure.

> [!NOTE]
> Lorsque vous rendez une application multilocataire, vous devez vous assurer que l’URI ID de votre application appartient à un domaine vérifié. En outre, les URL de renvoi de hello doit commencer par https://. Pour plus d’informations, voir [Objets principal du service et application](active-directory-application-objects.md).
> 
> 

accès tooenable tooyour l’application pour les utilisateurs externes : 

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Choisissez votre locataire Azure AD en sélectionnant votre compte dans hello coin supérieur droit de la page de hello.
3. Dans le menu supérieur de hello, choisissez **Azure Active Directory**, cliquez sur **inscriptions d’application**et puis cliquez sur application hello tooconfigure. Cela sera vous prendre la page de démarrage rapide de l’application toohello, ainsi qu’ouvrir le panneau des paramètres pour l’application hello hello.
4. Dans le panneau des paramètres de hello, cliquez sur **propriétés** et hello retournement **avec clients Multi** basculer trop**Oui**.

Une fois que vous avez modifié hello ci-dessus, les utilisateurs et les administrateurs dans d’autres organisations sera en mesure de toogrant le répertoire tootheir accès de votre application et d’autres données.

#### <a name="triggering-hello-azure-ad-consent-framework-at-runtime"></a>Infrastructure de consentement hello Azure AD lors de l’exécution de déclenchement
infrastructure de consentement toouse hello, applications mutualisées client doivent demander une autorisation à l’aide d’OAuth 2.0. [Exemples de code](https://azure.microsoft.com/documentation/samples/?service=active-directory&term=multi-tenant) sont disponible tooshow comment une application web, une application native ou une autorisation de demandes d’application démon/serveur codes et accéder aux jetons toocall web API.

Votre application web peut peut-être offrir également une expérience d’inscription aux utilisateurs. Si vous offrez une expérience d’inscription, il est probable que l’utilisateur hello cliquer sur un bouton d’inscription que redirection hello navigateur toohello OAuth2.0 AD Azure permettra point de terminaison ou un point de terminaison userinfo OpenID Connect. Ces points de terminaison autorisent hello application tooget plus d’informations sur le nouvel utilisateur de hello en inspectant hello id_token. Après la phase d’abonnement de hello utilisateur de hello s’affiche avec un toohello similaire invite consentement celui affiché ci-dessus dans hello vue d’ensemble de la section de l’infrastructure de consentement de hello.

Vous pouvez également votre application web peut également offrir une expérience qui permet aux administrateurs trop « inscrire de ma société ». Cette expérience redirige également hello utilisateur toohello Azure AD OAuth 2.0 de point de terminaison authorize. Dans ce cas, vous passez à une invite de commandes = admin_consent toohello de paramètre Autoriser le point de terminaison tooforce hello administrateur expérience de consentement, où hello administrateur donne son consentement pour le compte de leur organisation. Seul l’utilisateur qui s’authentifie avec un compte auquel appartient le rôle d’administrateur général toohello peut fournir son consentement ; d’autres utilisateurs recevront une erreur. Consentement est correct, réponse de hello contiendra admin_consent = true. En échangeant un jeton d’accès, vous recevrez un id_token qui fournit des informations sur l’organisation de hello et un administrateur de hello inscrit pour votre application.

### <a name="enabling-oauth-20-implicit-grant-for-single-page-applications"></a>Activation de l’accord implicite OAuth 2.0 pour les applications à page unique
Application à Page unique (ZPS) sont généralement structurée avec un frontal lourdes JavaScript qui s’exécute dans le navigateur hello, qui appelle tooperform de back-end de l’application hello web API sa logique métier. Pour SPAs hébergés dans Azure AD, vous utilisez utilisateur de OAuth 2.0 Implicit Grant tooauthenticate hello avec Azure AD et obtenir un jeton que vous pouvez utiliser toosecure rappelle de tooits de client JavaScript de l’application hello API web de fin. Une fois que l’utilisateur de hello a donné son consentement, ce même protocole d’authentification peut être utilisé tooobtain jetons toosecure appels entre un client de hello et d’autres ressources de l’API web configurés pour l’application hello. toolearn en savoir plus sur l’octroi d’autorisation implicite hello et déterminer s’il est adapté à votre scénario d’application, consultez [hello de présentation OAuth2 implicite accorder des flux dans Azure Active Directory ](active-directory-dev-understanding-oauth2-implicit-grant.md).

Par défaut, l’accord implicite OAuth 2.0 est désactivé pour les applications. Vous pouvez activer OAuth 2.0 Implicit Grant pour votre application en définissant les hello `oauth2AllowImplicitFlow` valeur dans sa [manifeste d’application](active-directory-application-manifest.md), qui est un fichier JSON qui représente la configuration d’identité de votre application.

#### <a name="tooenable-oauth-20-implicit-grant"></a>Octroi implicite de tooenable OAuth 2.0
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Choisissez votre locataire Azure AD en sélectionnant votre compte dans hello coin supérieur droit de la page de hello.
3. Dans le menu supérieur de hello, choisissez **Azure Active Directory**, cliquez sur **inscriptions d’application**et puis cliquez sur application hello tooconfigure. Cela sera vous prendre la page de démarrage rapide de l’application toohello, ainsi qu’ouvrir le panneau des paramètres pour l’application hello hello.
4. À partir de la page d’application hello, cliquez sur **manifeste** éditeur de manifeste tooopen hello inline.
   Recherchez et définir la valeur « oauth2AllowImplicitFlow » de hello trop « true ». La valeur par défaut est « false ».
   
    `"oauth2AllowImplicitFlow": true,`
5. Enregistrer le manifeste de hello mis à jour. Une fois enregistré, votre site web QU'API est maintenant configuré les utilisateurs de tooauthenticate toouse OAuth 2.0 Implicit Grant.


## <a name="removing-an-application"></a>Suppression d'une application
Cette section décrit comment tooremove locataire une application à partir de votre annuaire Azure AD.

### <a name="removing-an-application-authored-by-your-organization"></a>Suppression d’une application créée par votre organisation
Il s’agit d’applications hello qui présentent sous hello « Applications que ma société possède » filtre sur la page « Applications » de la principale hello pour votre locataire Azure AD. En termes techniques, ceux-ci sont des applications que vous avez inscrit manuellement via le portail Azure classic de hello, ou par programme via PowerShell ou hello API Graph. Plus précisément, ces applications sont représentées dans votre locataire par des objets Application et Principal du service. Pour plus d’informations, consultez [Objets principal du service et application](active-directory-application-objects.md) .

#### <a name="tooremove-a-single-tenant-application-from-your-directory"></a>tooremove une application à locataire unique à partir de votre annuaire
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Choisissez votre locataire Azure AD en sélectionnant votre compte dans hello coin supérieur droit de la page de hello.
3. Dans le menu supérieur de hello, choisissez **Azure Active Directory**, cliquez sur **inscriptions d’application**et puis cliquez sur application hello tooconfigure. Cela sera vous prendre la page de démarrage rapide de l’application toohello, ainsi qu’ouvrir le panneau des paramètres pour l’application hello hello.
4. À partir de la page d’application hello, cliquez sur **supprimer**.
5. Cliquez sur **Oui** dans le message de confirmation hello.

#### <a name="tooremove-a-multi-tenant-application-from-your-directory"></a>tooremove une application mutualisée de votre annuaire
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Choisissez votre locataire Azure AD en sélectionnant votre compte dans hello coin supérieur droit de la page de hello.
3. Dans le menu supérieur de hello, choisissez **Azure Active Directory**, cliquez sur **inscriptions d’application**et puis cliquez sur application hello tooconfigure. Cela sera vous prendre la page de démarrage rapide de l’application toohello, ainsi qu’ouvrir le panneau des paramètres pour l’application hello hello.
4. Dans le panneau des paramètres de hello, choisissez **propriétés** et hello retournement **avec clients Multi** basculer trop**non**. Cela convertit votre application toobe un seul locataire, mais l’application hello reste dans une organisation qui a déjà consenti tooit.
5. Cliquez sur hello **supprimer** bouton à partir de la page de l’application hello.
6. Cliquez sur **Oui** dans le message de confirmation hello.

### <a name="removing-a-multi-tenant-application-authorized-by-another-organization"></a>Suppression d’une application multilocataire autorisée par une autre organisation
Il s’agit d’un sous-ensemble des applications hello qui présentent sous hello « Applications que ma société utilise » filtre sur la page du principal « Applications » hello pour votre locataire Azure AD, en particulier hello ceux qui ne sont pas répertoriés sous la liste des « Applications que ma société possède » hello. En termes techniques, il s’agit d’applications mutualisées inscrites pendant le processus de consentement hello. Ces applications sont représentées dans votre locataire par un objet Principal du service. Pour plus d’informations, consultez [Objets principal du service et application](active-directory-application-objects.md) .

Dans commande tooremove répertoire de l’application d’une architecture mutualisée access tooyour (après avoir donné son consentement), l’administrateur de la société hello doit avoir un abonnement Azure tooremove l’accès via hello portail Azure. Administrateur de la société hello pouvez également utiliser hello [applets de commande PowerShell Azure AD](http://go.microsoft.com/fwlink/?LinkId=294151) tooremove accès.

## <a name="next-steps"></a>Étapes suivantes
* Consultez hello [instructions de personnalisation pour les applications intégrées](active-directory-branding-guidelines.md) pour obtenir des conseils sur l’aide visuelle pour votre application.
* Pour plus d’informations sur la relation hello entre les objets d’Application et de Principal du Service d’une application, consultez [les objets de Principal du Service et Application](active-directory-application-objects.md).
* toolearn en savoir plus sur hello rôle hello application manifeste est lu, consultez [le manifeste d’application de présentation hello Azure Active Directory](active-directory-application-manifest.md)
* Consultez hello [glossaire du développeur Azure AD](active-directory-dev-glossary.md) pour les définitions de certains des concepts de développement hello core Azure Active Directory (AD).
* Visitez hello [guide du développeur Active Directory](active-directory-developers-guide.md) pour une vue d’ensemble de tous les développeur de contenu associé.

