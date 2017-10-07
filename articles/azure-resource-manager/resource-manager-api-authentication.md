---
title: "aaaAzure Active l’authentification et le Gestionnaire de ressources | Documents Microsoft"
description: "Tooauthentication de guide du développeur avec hello API Azure Resource Manager et Azure Active Directory pour l’intégration d’une application avec d’autres abonnements Azure."
services: azure-resource-manager,active-directory
documentationcenter: na
author: dushyantgill
manager: timlt
editor: tysonn
ms.assetid: 17b2b40d-bf42-4c7d-9a88-9938409c5088
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/27/2016
ms.author: dugill;tomfitz
ms.openlocfilehash: 757e45fdb28488b45de70647746461888bf35a56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-resource-manager-authentication-api-tooaccess-subscriptions"></a>Utiliser le Gestionnaire de ressources des API d’authentification abonnements tooaccess
## <a name="introduction"></a>Introduction
Si vous êtes un développeur de logiciels ayant besoin de toocreate une application qui gère les ressources Azure du client, cette rubrique vous montre comment tooauthenticate avec hello API du Gestionnaire de ressources Azure et obtenir tooresources d’accès dans les autres abonnements.

Votre application peut accéder aux hello API du Gestionnaire de ressources de deux manières :

1. **Accès de l’utilisateur et de l’application**: pour les applications qui accèdent aux ressources pour le compte d’un utilisateur connecté. Cette approche fonctionne pour les applications, telles que les applications web et les outils en ligne de commande, qui n’assurent que la « gestion interactive » des ressources Azure.
2. **Accès de l’application uniquement**: pour les applications qui exécutent des services démons et des tâches planifiées. identité de l’application Hello bénéficie des ressources de toohello un accès direct. Cette approche fonctionne pour les applications nécessitant des tooAzure l’accès contrôlé à distance (sans assistance) à long terme.

Cette rubrique fournit des instructions détaillées toocreate une application qui utilise ces deux méthodes d’autorisation. Il montre comment tooperform chaque étape avec les API REST ou c#. les applications ASP.NET MVC complete Hello est disponible à l’adresse [https://github.com/dushyantgill/VipSwapper/tree/master/CloudSense](https://github.com/dushyantgill/VipSwapper/tree/master/CloudSense).

## <a name="what-hello-web-app-does"></a>Quelle application web de hello est
application Hello web :

1. Connecte un utilisateur Azure.
2. Demande utilisateur toogrant hello web application accès tooResource Manager.
3. Se procure le jeton d’accès de l’utilisateur et de l’application pour accéder à Resource Manager.
4. Utilise toocall jeton (à l’étape 3) le Gestionnaire de ressources et le rôle de tooa principal du service de l’application assign hello abonnement hello, ce qui donne l’abonnement de la toohello hello application de l’accès à long terme.
5. Obtient le jeton d’accès de l’application uniquement.
6. Utilise les ressources de jeton (à l’étape 5) toomanage dans l’abonnement hello via le Gestionnaire de ressources.

Voici le flux de bout en bout hello d’application web de hello.

![Flux d’authentification de Resource Manager](./media/resource-manager-api-authentication/Auth-Swim-Lane.png)

En tant qu’utilisateur, vous fournissez l’id d’abonnement hello pour l’abonnement de hello souhaité toouse :

![indiquer l’identifiant de l’abonnement](./media/resource-manager-api-authentication/sample-ux-1.png)

Sélectionnez toouse de compte hello pour la connexion.

![sélectionner le compte](./media/resource-manager-api-authentication/sample-ux-2.png)

Indiquez vos informations d’identification.

![Fournir des informations d’identification](./media/resource-manager-api-authentication/sample-ux-3.png)

Accorder des abonnements Azure hello application accès tooyour :

![Accorder l'accès](./media/resource-manager-api-authentication/sample-ux-4.png)

Gérez vos abonnements connectés :

![Connecter un abonnement](./media/resource-manager-api-authentication/sample-ux-7.png)

## <a name="register-application"></a>Inscription de l’application
Avant de commencer l’écriture du code, inscrivez votre application web à Azure Active Directory (AD). inscription d’une application Hello crée une identité centrale pour votre application dans Azure AD. Elle contient des informations de base relatives à votre application comme ID de Client OAuth, URL de réponse et les informations d’identification que votre application utilise tooauthenticate et l’accès aux API du Gestionnaire de ressources Azure. inscription d’une application Hello enregistre également hello différents délégué des autorisations dont votre application a besoin lors de l’accès APIs Microsoft pour le compte d’utilisateur de hello.

Votre application ayant accès à plusieurs abonnements, vous devez la configurer comme une application mutualisée. validation de toopass, fournir un domaine associé à votre Azure Active Directory. les domaines de hello toosee associés à votre Azure Active Directory, ouvrez une session toohello [portail classic](https://manage.windowsazure.com). Sélectionnez votre annuaire Azure Active Directory, puis **Domaines**.

Bonjour à l’exemple suivant montre comment tooregister hello application à l’aide d’Azure PowerShell. Vous devez disposer de hello version la plus récente (août 2016) d’Azure PowerShell pour toowork de cette commande.

    $app = New-AzureRmADApplication -DisplayName "{app name}" -HomePage "https://{your domain}/{app name}" -IdentifierUris "https://{your domain}/{app name}" -Password "{your password}" -AvailableToOtherTenants $true

toolog dans en tant que hello application AD, vous devez mot de passe et l’id de l’application hello. toosee hello id de l’application qui est retourné à partir de la commande précédente hello, utilisez :

    $app.ApplicationId

Bonjour à l’exemple suivant montre comment tooregister hello application à l’aide de CLI d’Azure.

    azure ad app create --name {app name} --home-page https://{your domain}/{app name} --identifier-uris https://{your domain}/{app name} --password {your password} --available true

les résultats de Hello incluent hello AppId, dont vous aurez besoin lors de l’authentification en tant qu’application hello.

### <a name="optional-configuration---certificate-credential"></a>Configuration facultative : informations d’identification des certificats
Azure AD prend également en charge les informations d’identification de certificat pour les applications : vous créez un certificat auto-signé, conserver la clé privée de hello et ajouter l’inscription d’application hello tooyour clé publique Azure AD. Pour l’authentification, votre application envoie un tooAzure de charge utile de petits AD signé à l’aide de votre clé privée et Azure AD valide la signature hello à l’aide de la clé publique hello que vous avez enregistré.

Pour plus d’informations sur la création d’une application AD avec un certificat, consultez [utiliser Azure PowerShell toocreate un principal de service des ressources de tooaccess](resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority) ou [CLI d’Azure utilisation toocreate un principal de service tooaccess ressources](resource-group-authenticate-service-principal-cli.md#create-service-principal-with-certificate).

## <a name="get-tenant-id-from-subscription-id"></a>Obtention de l’ID du client à partir de l’ID d’abonnement
toorequest un jeton qui peut être utilisé toocall Gestionnaire de ressources, votre application doit ID tooknow hello du hello Azure AD qui héberge hello abonnement Azure client. Vos utilisateurs connaissent sûrement leurs ID d’abonnement, mais pas nécessairement leurs ID de client Azure Active Directory. tooget hello id de l’utilisateur client, demandez à utilisateur de hello hello id d’abonnement. Fournir cet id d’abonnement lors de l’envoi d’une demande sur l’abonnement de hello :

    https://management.azure.com/subscriptions/{subscription-id}?api-version=2015-01-01

demande de Hello échoue, car l’utilisateur de hello n’a pas encore connecté, mais vous pouvez récupérer l’id de client hello de réponse de hello. Dans cette exception, extraire l’id de client hello à partir de la valeur d’en-tête de réponse hello pour **WWW-Authenticate**. Vous voyez cette implémentation Bonjour [GetDirectoryForSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L20) (méthode).

## <a name="get-user--app-access-token"></a>Obtention du jeton de l’utilisateur et de l’application
Votre application redirige l’utilisateur de hello tooAzure AD avec un OAuth 2.0 autoriser demande - informations d’identification de l’utilisateur tooauthenticate hello et obtenir un code d’autorisation. Votre application utilise tooget de code d’autorisation hello un jeton d’accès pour le Gestionnaire de ressources. Hello [ConnectSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/Controllers/HomeController.cs#L42) méthode crée la demande d’autorisation de hello.

Cette rubrique montre à hello API REST demandes tooauthenticate hello utilisateur. Vous pouvez également utiliser l’authentification tooperform de bibliothèques d’assistance dans votre code. Pour plus d’informations sur ces bibliothèques, consultez [Bibliothèques d’authentification d’Azure Active Directory](../active-directory/active-directory-authentication-libraries.md). Pour des conseils sur l’intégration de la gestion de l’identité dans une application, consultez le [Guide du développeur Azure Active Directory](../active-directory/active-directory-developers-guide.md).

### <a name="auth-request-oauth-20"></a>Demande d’autorisation (OAuth 2.0)
Émettre un point de terminaison de Authorize d’ouvrir Connect/OAuth2.0 autoriser les demandes d’ID de toohello Azure AD :

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Authorize

les paramètres de chaîne de requête de Hello qui sont disponibles pour cette demande sont décrits dans hello [demander un code d’autorisation](../active-directory/develop/active-directory-protocols-oauth-code.md#request-an-authorization-code) rubrique.

Hello suivant montre l’exemple de comment toorequest OAuth2.0 autorisation :

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Authorize?client_id=a0448380-c346-4f9f-b897-c18733de9394&response_mode=query&response_type=code&redirect_uri=http%3a%2f%2fwww.vipswapper.com%2fcloudsense%2fAccount%2fSignIn&resource=https%3a%2f%2fgraph.windows.net%2f&domain_hint=live.com

Azure AD authentifie l’utilisateur de hello et, si nécessaire, demande hello utilisateur toogrant autorisation toohello application. Il retourne toohello de code d’autorisation hello URL de réponse de votre application. En fonction de hello demandé response_mode, Azure AD soit renvoie un hello des données dans la chaîne de requête ou en tant que données de publication.

    code=AAABAAAAiL****FDMZBUwZ8eCAA&session_state=2d16bbce-d5d1-443f-acdf-75f6b0ce8850

### <a name="auth-request-open-id-connect"></a>Demande d’autorisation (Open ID Connect)
Si vous seulement souhaitez tooaccess Azure Resource Manager pour le compte d’utilisateur de hello, mais également autoriser hello utilisateur toosign dans l’application de tooyour à l’aide de leur compte Azure AD, émettre une Open ID autoriser demande de connexion. Avec Open ID de connexion, votre application reçoit également une id_token d’Azure AD que votre application peut utiliser toosign utilisateur de hello.

les paramètres de chaîne de requête de Hello qui sont disponibles pour cette demande sont décrits dans hello [envoi hello connectez-vous demande](../active-directory/develop/active-directory-protocols-openid-connect-code.md#send-the-sign-in-request) rubrique.

Exemple de demande Open ID Connect :

     https://login.microsoftonline.com/{tenant-id}/OAuth2/Authorize?client_id=a0448380-c346-4f9f-b897-c18733de9394&response_mode=form_post&response_type=code+id_token&redirect_uri=http%3a%2f%2fwww.vipswapper.com%2fcloudsense%2fAccount%2fSignIn&resource=https%3a%2f%2fgraph.windows.net%2f&scope=openid+profile&nonce=63567Dc4MDAw&domain_hint=live.com&state=M_12tMyKaM8

Azure AD authentifie l’utilisateur de hello et, si nécessaire, demande hello utilisateur toogrant autorisation toohello application. Il retourne toohello de code d’autorisation hello URL de réponse de votre application. En fonction de hello demandé response_mode, Azure AD soit renvoie un hello des données dans la chaîne de requête ou en tant que données de publication.

Exemple de réponse Open ID Connect :

    code=AAABAAAAiL*****I4rDWd7zXsH6WUjlkIEQxIAA&id_token=eyJ0eXAiOiJKV1Q*****T3GrzzSFxg&state=M_12tMyKaM8&session_state=2d16bbce-d5d1-443f-acdf-75f6b0ce8850

### <a name="token-request-oauth20-code-grant-flow"></a>Demande de jeton (flux d’octroi d’un code d’autorisation OAuth2.0)
Maintenant que votre application a reçu le code d’autorisation de hello d’Azure AD, il est le jeton d’accès de temps tooget hello pour le Gestionnaire de ressources Azure.  Valider une demande jeton d’OAuth2.0 Code Grant toohello Azure AD point de terminaison Token :

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Token

les paramètres de chaîne de requête de Hello qui sont disponibles pour cette demande sont décrits dans hello [utiliser du code d’autorisation hello](../active-directory/develop/active-directory-protocols-oauth-code.md#use-the-authorization-code-to-request-an-access-token) rubrique.

Bonjour à l’exemple suivant illustre une demande de jeton d’octroi de code avec les informations d’identification de mot de passe :

    POST https://login.microsoftonline.com/7fe877e6-a150-4992-bbfe-f517e304dfa0/oauth2/token HTTP/1.1

    Content-Type: application/x-www-form-urlencoded
    Content-Length: 1012

    grant_type=authorization_code&code=AAABAAAAiL9Kn2Z*****L1nVMH3Z5ESiAA&redirect_uri=http%3A%2F%2Flocalhost%3A62080%2FAccount%2FSignIn&client_id=a0448380-c346-4f9f-b897-c18733de9394&client_secret=olna84E8*****goScOg%3D

Lorsque vous travaillez avec les informations d’identification de certificat, créez un JSON Web Token (JWT) et le signe (RSA SHA256) à l’aide de la clé privée de hello des informations d’identification du certificat de votre application. types de revendications de jeton de hello Hello sont affichés dans [les revendications de jeton JWT](../active-directory/develop/active-directory-protocols-oauth-code.md#jwt-token-claims). Pour référence, consultez hello [code de bibliothèque d’Active Directory d’authentification (.NET)](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet/blob/dev/src/ADAL.PCL.Desktop/CryptographyHelper.cs) toosign des jetons JWT d’Assertion de Client.

Consultez hello [spécification de connexion d’ID ouvrir](http://openid.net/specs/openid-connect-core-1_0.html#ClientAuthentication) pour plus d’informations sur l’authentification du client.

Hello, l’exemple suivant illustre une demande de jeton d’octroi de code avec les informations d’identification de certificat :

    POST https://login.microsoftonline.com/7fe877e6-a150-4992-bbfe-f517e304dfa0/oauth2/token HTTP/1.1

    Content-Type: application/x-www-form-urlencoded
    Content-Length: 1012

    grant_type=authorization_code&code=AAABAAAAiL9Kn2Z*****L1nVMH3Z5ESiAA&redirect_uri=http%3A%2F%2Flocalhost%3A62080%2FAccount%2FSignIn&client_id=a0448380-c346-4f9f-b897-c18733de9394&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&client_assertion=eyJhbG*****Y9cYo8nEjMyA

Exemple de réponse de jeton d’octroi de code :

    HTTP/1.1 200 OK

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1432039858","not_before":"1432035958","resource":"https://management.core.windows.net/","access_token":"eyJ0eXAiOiJKV1Q****M7Cw6JWtfY2lGc5A","refresh_token":"AAABAAAAiL9Kn2Z****55j-sjnyYgAA","scope":"user_impersonation","id_token":"eyJ0eXAiOiJKV*****-drP1J3P-HnHi9Rr46kGZnukEBH4dsg"}

#### <a name="handle-code-grant-token-response"></a>Gérer la réponse de jeton d’octroi de code
Une réponse correcte de jeton contient de jeton d’accès hello (utilisateur + app) pour le Gestionnaire de ressources Azure. Votre application utilise cette tooaccess de jeton d’accès Gestionnaire de ressources pour le compte d’utilisateur de hello. durée de vie Hello des jetons d’accès émis par Azure AD est d’une heure. Il est peu probable que votre application web a besoin de jeton d’accès toorenew hello (utilisateur + application). Si elle a besoin de jeton d’accès toorenew hello, utilisez le jeton d’actualisation hello que votre application reçoit dans la réponse du jeton hello. Valider une demande de jeton OAuth2.0 toohello Azure AD point de terminaison Token :

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Token

Hello toouse de paramètres avec la demande d’actualisation hello sont décrites dans [jeton d’accès de l’actualisation hello](../active-directory/develop/active-directory-protocols-oauth-code.md#refreshing-the-access-tokens).

Hello suivant montre comment actualiser le jeton toouse hello :

    POST https://login.microsoftonline.com/7fe877e6-a150-4992-bbfe-f517e304dfa0/oauth2/token HTTP/1.1

    Content-Type: application/x-www-form-urlencoded
    Content-Length: 1012

    grant_type=refresh_token&refresh_token=AAABAAAAiL9Kn2Z****55j-sjnyYgAA&client_id=a0448380-c346-4f9f-b897-c18733de9394&client_secret=olna84E8*****goScOg%3D

Bien que les jetons d’actualisation peuvent être utilisé tooget nouveaux jetons d’accès pour le Gestionnaire de ressources Azure, ils ne conviennent pas pour l’accès hors connexion par votre application. durée de vie des jetons actualisation Hello est limitée, et des jetons d’actualisation sont liées toohello utilisateur. Si l’utilisateur de hello quitte l’organisation de hello, application hello à l’aide du jeton d’actualisation hello perd l’accès. Cette approche n’est pas appropriée pour les applications qui sont utilisés par les équipes toomanage leurs ressources Azure.

## <a name="check-if-user-can-assign-access-toosubscription"></a>Vérifiez si utilisateur peut assigner toosubscription d’accès
Votre application dispose maintenant d’un jeton tooaccess Azure Resource Manager pour le compte d’utilisateur de hello. étape suivante de Hello est tooconnect votre abonnement de toohello d’application. Une fois connecté, votre application peut gérer les abonnements, même lorsque l’utilisateur de hello n’est pas présent (accès hors connexion à long terme).

Pour chaque abonnement tooconnect, appelez hello [les autorisations de liste de gestionnaire de ressources](https://docs.microsoft.com/rest/api/authorization/permissions) API toodetermine si utilisateur de hello possède les droits de gestion d’accès pour l’abonnement de hello.

Hello [UserCanManagerAccessForSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L44) méthode Hello, exemple d’application ASP.NET MVC implémente cet appel.

Hello suivant montre l’exemple de comment toorequest les autorisations d’un utilisateur sur un abonnement. 83cfe939-2402-4581-b761-4f59b0a041e4 est l’id hello d’abonnement de hello.

    GET https://management.azure.com/subscriptions/83cfe939-2402-4581-b761-4f59b0a041e4/providers/microsoft.authorization/permissions?api-version=2015-07-01 HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJKV1QiLC***lwO1mM7Cw6JWtfY2lGc5A

Un exemple d’autorisations de l’utilisateur tooget hello réponse lors de l’abonnement est :

    HTTP/1.1 200 OK

    {"value":[{"actions":["*"],"notActions":["Microsoft.Authorization/*/Write","Microsoft.Authorization/*/Delete"]},{"actions":["*/read"],"notActions":[]}]}

autorisations de Hello API retourne plusieurs autorisations. Chaque autorisation est constituée d’actions autorisées (paramètre Actions) et interdites (paramètre NotActions). Si une action est présente dans hello liste d’actions de n’importe quelle autorisation autorisée et non présent dans la liste de notactions hello de cette autorisation, l’utilisateur hello est autorisée tooperform cette action. **Microsoft.Authorization/RoleAssignments/Write** est action hello que qui accorde l’accès de gestion. Votre application doit analyser hello autorisations résultat toolook pour une correspondance d’expression régulière sur cette chaîne d’action dans les actions hello et notactions de chaque autorisation.

## <a name="get-app-only-access-token"></a>Obtention du jeton d’accès de l’application uniquement
Vous savez maintenant, si l’utilisateur hello peut attribuer des accès toohello abonnement Azure. les étapes suivantes Hello sont :

1. Affecter hello approprié RBAC rôle tooyour identité de l’application sur l’abonnement de hello.
2. Valider l’assignation d’accès hello en demandant l’autorisation de l’Application hello sur les abonnement hello ou en accédant au Gestionnaire de ressources à l’aide du jeton d’application uniquement.
3. Connexion d’enregistrement hello dans votre structure de données d’applications « abonnements connectés » - persistance id hello d’abonnement de hello.

Examinons de plus près à la première étape de hello. tooassign hello approprié RBAC rôle toohello identité de l’application, vous devez déterminer :

* id d’objet Hello d’identité de votre application dans Azure Active Directory l’utilisateur hello
* Identificateur Hello du rôle RBAC hello requis par votre application sur un abonnement de hello

Lorsque votre application authentifie un utilisateur à partir d’une instance d’Azure AD, elle crée un objet principal du service pour votre application dans cette instance. Azure permet de RBAC rôles toobe affecté tooservice principaux applications de toocorresponding toogrant un accès direct sur les ressources Azure. Cette action est exactement ce que nous souhaitons toodo. Requête les identificateurs de principal du service de votre application dans l’utilisateur connecté hello hello hello de la toodetermine de l’API Graph de hello Azure Active Directory de Azure AD.

Il vous suffit un jeton d’accès pour le Gestionnaire de ressources Azure, vous avez besoin d’un nouveau Bonjour de jeton toocall accès API Azure AD Graph. Chaque application dans Azure AD a tooquery d’autorisation à son propre objet principal de service, par conséquent, un jeton d’accès d’application uniquement est suffisant.

<a id="app-azure-ad-graph" />

### <a name="get-app-only-access-token-for-azure-ad-graph-api"></a>Obtenir un jeton d’accès d’application uniquement pour l’API Microsoft Azure AD Graph
tooauthenticate votre application et obtenir un jeton tooAzure AD Graph API, émettre un Client d’informations d’identification Grant OAuth2.0 flux demande de jeton tooAzure AD point de terminaison token (**https://login.microsoftonline.com/ {directory_domain_name} / OAuth2/jeton**).

Hello [GetObjectIdOfServicePrincipalInOrganization](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureADGraphAPIUtil.cs) méthode Hello, exemple d’application ASP.net MVC Obtient un accès de l’application uniquement jeton pour l’utilisation de l’API Graph hello bibliothèque d’authentification Active Directory pour .NET.

les paramètres de chaîne de requête de Hello qui sont disponibles pour cette demande sont décrits dans hello [demande un jeton d’accès](../active-directory/develop/active-directory-protocols-oauth-service-to-service.md#request-an-access-token) rubrique.

Voici un exemple de demande de jeton d’octroi d’informations d’identification du client :

    POST https://login.microsoftonline.com/62e173e9-301e-423e-bcd4-29121ec1aa24/oauth2/token HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Content-Length: 187</pre>
    <pre>grant_type=client_credentials&client_id=a0448380-c346-4f9f-b897-c18733de9394&resource=https%3A%2F%2Fgraph.windows.net%2F &client_secret=olna8C*****Og%3D

Voici un exemple de réponse à une demande de jeton d’octroi d’informations d’identification du client :

    HTTP/1.1 200 OK

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1432039862","not_before":"1432035962","resource":"https://graph.windows.net/","access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiJodHRwczovL2dyYXBoLndpbmRv****G5gUTV-kKorR-pg"}

### <a name="get-objectid-of-application-service-principal-in-user-azure-ad"></a>Obtenir le principal de service d’application ObjectId dans l’instance Azure AD de l’utilisateur
À présent, utiliser hello de jeton tooquery accès uniquement par l’application hello [principaux du Service Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity) hello de toodetermine API Id d’objet de principal du service de l’application hello dans le répertoire de hello.

Hello [GetObjectIdOfServicePrincipalInOrganization](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureADGraphAPIUtil.cs#) méthode Hello, exemple d’application ASP.net MVC implémente cet appel.

Hello suivant montre l’exemple de comment toorequest principal du service d’une application. a0448380-c346-4f9f-b897-c18733de9394 est l’id de client hello de l’application hello.

    GET https://graph.windows.net/62e173e9-301e-423e-bcd4-29121ec1aa24/servicePrincipals?api-version=1.5&$filter=appId%20eq%20'a0448380-c346-4f9f-b897-c18733de9394' HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJK*****-kKorR-pg

Hello exemple suivant illustre une réponse toohello demande pour le service de l’application principale

    HTTP/1.1 200 OK

    {"odata.metadata":"https://graph.windows.net/62e173e9-301e-423e-bcd4-29121ec1aa24/$metadata#directoryObjects/Microsoft.DirectoryServices.ServicePrincipal","value":[{"odata.type":"Microsoft.DirectoryServices.ServicePrincipal","objectType":"ServicePrincipal","objectId":"9b5018d4-6951-42ed-8a92-f11ec283ccec","deletionTimestamp":null,"accountEnabled":true,"appDisplayName":"CloudSense","appId":"a0448380-c346-4f9f-b897-c18733de9394","appOwnerTenantId":"62e173e9-301e-423e-bcd4-29121ec1aa24","appRoleAssignmentRequired":false,"appRoles":[],"displayName":"CloudSense","errorUrl":null,"homepage":"http://www.vipswapper.com/cloudsense","keyCredentials":[],"logoutUrl":null,"oauth2Permissions":[{"adminConsentDescription":"Allow hello application tooaccess CloudSense on behalf of hello signed-in user.","adminConsentDisplayName":"Access CloudSense","id":"b7b7338e-683a-4796-b95e-60c10380de1c","isEnabled":true,"type":"User","userConsentDescription":"Allow hello application tooaccess CloudSense on your behalf.","userConsentDisplayName":"Access CloudSense","value":"user_impersonation"}],"passwordCredentials":[],"preferredTokenSigningKeyThumbprint":null,"publisherName":"vipswapper"quot;,"replyUrls":["http://www.vipswapper.com/cloudsense","http://www.vipswapper.com","http://vipswapper.com","http://vipswapper.azurewebsites.net","http://localhost:62080"],"samlMetadataUrl":null,"servicePrincipalNames":["http://www.vipswapper.com/cloudsense","a0448380-c346-4f9f-b897-c18733de9394"],"tags":["WindowsAzureActiveDirectoryIntegratedApp"]}]}

### <a name="get-azure-rbac-role-identifier"></a>Obtenir l’identificateur du rôle Azure RBAC
tooassign hello approprié RBAC tooyour service de rôle principal, vous devez déterminer l’identificateur hello du rôle de Azure RBAC hello.

Hello RBAC rôle qui correspond à votre application :

* Si votre application surveille uniquement les abonnement hello, sans apporter de modifications, il requiert uniquement des autorisations de lecteur sur les abonnement hello. Affecter hello **lecteur** rôle.
* Si votre application gère l’abonnement Azure hello, création/modification/suppression d’entités, elle nécessite une des autorisations de collaborateur hello.
  * toomanage un type particulier de ressource, attribuer des rôles de propres à la ressource collaborateur hello (contributeur de l’ordinateur virtuel, les collaborateurs de réseau virtuel, collaborateur de compte de stockage, etc.)
  * toomanage n’importe quel type de ressource, l’affectation hello **collaborateur** rôle.

attribution de rôle Hello pour votre application étant toousers visible, sélectionnez hello requis de moins de privilèges.

Appelez hello [définition de rôle Gestionnaire de ressources API](https://docs.microsoft.com/rest/api/authorization/roledefinitions) toolist tous les rôles Azure RBAC et recherche ensuite parcourir hello de toofind hello résultat souhaité de définition de rôle par nom.

Hello [GetRoleId](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L246) méthode Hello, exemple d’application ASP.net MVC implémente cet appel.

montre l’exemple de la requête suivante de Hello comment identificateur de rôle Azure RBAC tooget. 09cbd307-aa71-4aca-b346-5f253e6e3ebb est l’id hello d’abonnement de hello.

    GET https://management.azure.com/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions?api-version=2015-07-01 HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJKV*****fY2lGc5

réponse de Hello est Bonjour suivant le format :

    HTTP/1.1 200 OK

    {"value":[{"properties":{"roleName":"API Management Service Contributor","type":"BuiltInRole","description":"Lets you manage API Management services, but not access toothem.","scope":"/","permissions":[{"actions":["Microsoft.ApiManagement/Services/*","Microsoft.Authorization/*/read","Microsoft.Resources/subscriptions/resources/read","Microsoft.Resources/subscriptions/resourceGroups/read","Microsoft.Resources/subscriptions/resourceGroups/resources/read","Microsoft.Resources/subscriptions/resourceGroups/deployments/*","Microsoft.Insights/alertRules/*","Microsoft.Support/*"],"notActions":[]}]},"id":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/312a565d-c81f-4fd8-895a-4e21e48d571c","type":"Microsoft.Authorization/roleDefinitions","name":"312a565d-c81f-4fd8-895a-4e21e48d571c"},{"properties":{"roleName":"Application Insights Component Contributor","type":"BuiltInRole","description":"Lets you manage Application Insights components, but not access toothem.","scope":"/","permissions":[{"actions":["Microsoft.Insights/components/*","Microsoft.Insights/webtests/*","Microsoft.Authorization/*/read","Microsoft.Resources/subscriptions/resources/read","Microsoft.Resources/subscriptions/resourceGroups/read","Microsoft.Resources/subscriptions/resourceGroups/resources/read","Microsoft.Resources/subscriptions/resourceGroups/deployments/*","Microsoft.Insights/alertRules/*","Microsoft.Support/*"],"notActions":[]}]},"id":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/ae349356-3a1b-4a5e-921d-050484c6347e","type":"Microsoft.Authorization/roleDefinitions","name":"ae349356-3a1b-4a5e-921d-050484c6347e"}]}

Il est inutile toocall cette API en continu. Une fois que vous avez déterminé hello GUID connu de définition de rôle hello, vous pouvez construire des id de définition de rôle hello en tant que :

    /subscriptions/{subscription_id}/providers/Microsoft.Authorization/roleDefinitions/{well-known-role-guid}

Voici hello des GUID bien connu des rôles intégrés couramment utilisées :

| Rôle | Guid |
| --- | --- |
| Lecteur |acdd72a7-3385-48ef-bd42-f606fba81ae7 |
| Contributeur |b24988ac-6180-42a0-ab88-20f7382dd24c |
| Collaborateur de machine virtuelle |d73bb868-a0df-4d4d-bd69-98a00b01fccb |
| Collaborateur de réseau virtuel |b34d265f-36f7-4a0d-a4d4-e158ca92e90f |
| Collaborateur de compte de stockage |86e8f5dc-a6e9-4c67-9d15-de283e8eac25 |
| Collaborateur de site web |de139f84-1756-47ae-9be6-808fbbe84772 |
| Collaborateur de plan web |2cc479cb-7b4d-49a8-b449-8c00fd0f0a4b |
| Collaborateur SQL Server |6d8ee4ec-f05a-4a1d-8b00-a9b17e38b437 |
| Collaborateur de base de données SQL |9b7fa17d-e63e-47b0-bb0a-15c516ac86ec |

### <a name="assign-rbac-role-tooapplication"></a>Affecter le RBAC rôle tooapplication
Vous disposez de tous les éléments nécessaires tooassign hello approprié RBAC rôle tooyour principal du service à l’aide de hello [le Gestionnaire de ressources créez l’attribution de rôle](https://docs.microsoft.com/rest/api/authorization/roleassignments) API.

Hello [GrantRoleToServicePrincipalOnSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L170) méthode Hello, exemple d’application ASP.net MVC implémente cet appel.

Une tooapplication exemple demande tooassign RBAC rôle :

    PUT https://management.azure.com/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/microsoft.authorization/roleassignments/4f87261d-2816-465d-8311-70a27558df4c?api-version=2015-07-01 HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJKV1QiL*****FlwO1mM7Cw6JWtfY2lGc5
    Content-Type: application/json
    Content-Length: 230

    {"properties": {"roleDefinitionId":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7","principalId":"c3097b31-7309-4c59-b4e3-770f8406bad2"}}

Dans la demande hello, hello valeurs suivantes est utilisée :

| Guid | Description |
| --- | --- |
| 09cbd307-aa71-4aca-b346-5f253e6e3ebb |id de Hello d’abonnement de hello |
| c3097b31-7309-4c59-b4e3-770f8406bad2 |id de l’objet de principal du service de l’application hello hello Hello |
| acdd72a7-3385-48ef-bd42-f606fba81ae7 |id de Hello du rôle de lecteur hello |
| 4f87261d-2816-465d-8311-70a27558df4c |un nouveau guid créé pour la nouvelle attribution de rôle hello |

réponse de Hello est Bonjour suivant le format :

    HTTP/1.1 201 Created

    {"properties":{"roleDefinitionId":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7","principalId":"c3097b31-7309-4c59-b4e3-770f8406bad2","scope":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb"},"id":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleAssignments/4f87261d-2816-465d-8311-70a27558df4c","type":"Microsoft.Authorization/roleAssignments","name":"4f87261d-2816-465d-8311-70a27558df4c"}

### <a name="get-app-only-access-token-for-azure-resource-manager"></a>Obtenir un jeton d’accès d’application uniquement pour Azure Resource Manager
toovalidate cette application accède hello souhaitée sur l’abonnement de hello, effectuer une tâche de test sur abonnement hello à l’aide d’un jeton d’application uniquement.

tooget un jeton d’accès d’application uniquement, suivez les instructions à partir de la section [obtenir d’un jeton d’accès application uniquement pour l’API Azure AD Graph](#app-azure-ad-graph), avec une valeur différente pour le paramètre de ressource hello :

    https://management.core.windows.net/

Hello [ServicePrincipalHasReadAccessToSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L110) méthode Hello, exemple d’application ASP.NET MVC Obtient un accès de l’application uniquement jeton pour à l’aide du Gestionnaire de ressources Azure hello bibliothèque d’authentification Active Directory pour .net.

#### <a name="get-applications-permissions-on-subscription"></a>Obtention des autorisations de l’application sur l’abonnement
toocheck votre application a hello souhaité d’accès sur un abonnement Azure, vous pouvez également appeler hello [les autorisations de gestionnaire de ressources](https://docs.microsoft.com/rest/api/authorization/permissions) API. Cette approche est semblable toohow vous de déterminer si les utilisateurs hello dispose des droits de gestion de l’accès pour l’abonnement de hello. Toutefois, cette fois-ci, appeler des API d’autorisations de hello avec le jeton d’accès d’application uniquement hello que vous avez reçu dans l’étape précédente de hello.

Hello [ServicePrincipalHasReadAccessToSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L110) méthode Hello, exemple d’application ASP.NET MVC implémente cet appel.

## <a name="manage-connected-subscriptions"></a>Gestion des abonnements connectés
Lorsque le rôle RBAC approprié hello est assigné principal du service de l’application tooyour lors de l’abonnement de hello, votre application peut conserver d’analyse et la gestion à l’aide des jetons d’accès d’application uniquement pour le Gestionnaire de ressources Azure.

Si un propriétaire d’abonnement Supprime l’attribution de rôle de votre application à l’aide du portail classique de hello ou les outils de ligne de commande, votre application est tooaccess n’est plus en mesure de cet abonnement. Dans ce cas, vous devez notifier les utilisateurs hello que connexion hello abonnement de hello a été interrompue à partir de l’extérieur application hello et leur donner une option trop « réparer » les connexion hello. « Réparer » créerait simplement nouvelle attribution de rôle hello qui a été supprimée en mode hors connexion.

Tout comme vous avez activé l’application hello utilisateur tooconnect abonnements tooyour, vous devez autoriser les abonnements de toodisconnect utilisateur hello trop. À partir d’un point de gestion des accès, de vue déconnecter consiste à effacer l’attribution de rôle hello principal du service de l’application hello vis-à-vis d’abonnement de hello. Si vous le souhaitez, un état de l’application hello pour l’abonnement de hello peut également supprimé.
Seuls les utilisateurs disposant des autorisations de gestion de l’accès sur l’abonnement de hello sont abonnement de hello en mesure de toodisconnect.

Hello [RevokeRoleFromServicePrincipalOnSubscription méthode](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L200) Hello ASP.net MVC, exemple d’application implémente cet appel.

Et voilà ! Les utilisateurs peuvent maintenant se connecter et gérer facilement leurs abonnements Azure avec votre application.
