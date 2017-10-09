---
title: "aaaProtect un principal de l’API Web avec Azure Active Directory et gestion des API | Documents Microsoft"
description: "Découvrez comment tooprotect un principal de l’API Web avec Azure Active Directory et gestion des API."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: f856ff03-64a1-4548-9ec4-c0ec4cc1600f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: f4b323034354aa09579c643bade47257fbf1e5c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprotect-a-web-api-backend-with-azure-active-directory-and-api-management"></a>Comment tooprotect un principal de l’API Web avec Azure Active Directory et gestion des API
Hello suivant vidéo montre comment toobuild un principal de l’API Web et le protéger à l’aide du protocole OAuth 2.0 avec Azure Active Directory et gestion des API.  Cet article fournit une vue d’ensemble et des informations supplémentaires pour hello les étapes dans la vidéo de hello. Cette vidéo 24 minutes vous montre comment faire pour :

* générer un serveur principal d’API Web et le protéger avec AAD (début à 1:30) ;
* Importer hello API de gestion des API - commençant à 7:10
* Configurer hello développeur toocall portail hello API - commençant à 9:09
* Configurer un Bonjour de toocall d’application de bureau API - commençant à 18:08
* Configurer un toopre de stratégie de validation de jetons Web JSON-autoriser les demandes - en commençant à 20:47

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

## <a name="create-an-azure-ad-directory"></a>Création d’un répertoire Azure AD
toosecure votre API Web sauvegardé à l’aide d’Azure Active Directory vous devez avoir un un locataire AAD. Dans cette vidéo, on utilise un client nommé **APIMDemo** . toocreate un locataire AAD, connectez-vous toohello [portail classique Azure](https://manage.windowsazure.com) et cliquez sur **nouveau**->**des Services d’application**->**Active Répertoire**->**active**->**création personnalisée**. 

![Azure Active Directory][api-management-create-aad-menu]

Dans cet exemple, on crée un répertoire nommé **APIMDemo** avec un domaine par défaut nommé **DemoAPIM.onmicrosoft.com**. Ce répertoire est utilisé dans l’ensemble de vidéo de hello.

![Azure Active Directory][api-management-create-aad]

## <a name="create-a-web-api-service-secured-by-azure-active-directory"></a>Création d’un service API web protégé par Azure Active Directory
Dans cette étape, un serveur principal d’API web est créé à l’aide de Visual Studio 2013. Cette étape de hello vidéo démarre à 1 h 30. projet de service principal d’API Web toocreate dans, cliquez sur Visual Studio **fichier**->**nouveau**->**projet**, puis choisissez **Web ASP.NET Application** de hello **Web** liste de modèles. Dans cette vidéo hello projet se nomme **APIMAADDemo**. Cliquez sur **OK** projet hello de toocreate. 

![Visual Studio][api-management-new-web-app]

Cliquez sur **API Web** de hello **, sélectionnez un modèle de liste** toocreate un projet d’API Web. Cliquez sur le tooconfigure Azure Active Authentication **modifier l’authentification**.

![Nouveau projet][api-management-new-project]

Cliquez sur **comptes professionnels**et spécifiez hello **domaine** de votre locataire AAD. Bonjour de cet exemple est domaine **DemoAPIM.onmicrosoft.com**. domaine hello de votre annuaire peut être obtenue à partir de hello **domaines** onglet de votre annuaire.

![Domaines][api-management-aad-domains]

Configurer les paramètres de hello souhaité Bonjour **modifier l’authentification** boîte de dialogue et cliquez sur **OK**.

![Modifier l’authentification][api-management-change-authentication]

Lorsque vous cliquez sur **OK** Visual Studio va tenter de tooregister votre application avec votre annuaire Azure AD et vous pouvez être invité à toosign dans par Visual Studio. Connectez-vous à l’aide d’un compte administrateur de votre répertoire.

![Connectez-vous à tooVisual Studio][api-management-sign-in-vidual-studio]

zone de ce projet en tant qu’un hello de vérification Azure Web API tooconfigure pour **hôte hello cloud** puis cliquez sur **OK**.

![Nouveau projet][api-management-new-project-cloud]

Vous pouvez être invité à toosign dans tooAzure, et vous pouvez ensuite configurer hello Web App.

![Configuration][api-management-configure-web-app]

Dans cet exemple, on spécifie un nouveau **Plan App Service** nommé **APIMAADDemo**.

Cliquez sur **OK** tooconfigure hello Web App et créer le projet de hello.

## <a name="add-hello-code-toohello-web-api-project"></a>Ajouter le projet d’API Web hello code toohello
étape suivante Hello vidéo de hello ajoute le projet d’API Web toohello hello code. Cette étape démarre à 4’35’’.

Hello API Web dans cet exemple implémente un service de calculatrice de base à l’aide d’un modèle et un contrôleur. avec le bouton droit de modèle de hello tooadd pour service de hello, **modèles** dans **l’Explorateur de solutions** et choisissez **ajouter**, **classe**. Nom de classe hello `CalcInput` et cliquez sur **ajouter**.

Ajoutez hello suivant `using` haut de toohello d’instruction de hello `CalcInput.cs` fichier.

```c#
using Newtonsoft.Json;
```

Remplacez classe hello généré par hello suivant de code.

```c#
public class CalcInput
{
    [JsonProperty(PropertyName = "a")]
    public int a;

    [JsonProperty(PropertyName = "b")]
    public int b;
}
```

Cliquez droit sur **Contrôleurs** dans l’**Explorateur de solutions** et choisissez **Ajouter**->**Contrôleur**. Choisissez **Contrôleur API 2 web - Vide**, puis cliquez sur **Ajouter**. Type **CalcController** pour hello contrôleur nom, cliquez sur **ajouter**.

![Ajouter un contrôleur][api-management-add-controller]

Ajoutez hello suivant `using` haut de toohello d’instruction de hello `CalcController.cs` fichier.

```c#
using System.IO;
using System.Web;
using APIMAADDemo.Models;
```

Remplacez classe de contrôleur hello généré par hello suivant de code. Ce code implémente hello `Add`, `Subtract`, `Multiply`, et `Divide` opérations Hello API de calculatrice de base.

```c#
[Authorize]
public class CalcController : ApiController
{
    [Route("api/add")]
    [HttpGet]
    public HttpResponseMessage GetSum([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a + b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/sub")]
    [HttpGet]
    public HttpResponseMessage GetDiff([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a - b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/mul")]
    [HttpGet]
    public HttpResponseMessage GetProduct([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a * b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/div")]
    [HttpGet]
    public HttpResponseMessage GetDiv([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a / b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }
}
```

Appuyez sur **F6** toobuild et vérifiez la solution de hello.

## <a name="publish-hello-project-tooazure"></a>Publier hello projet tooAzure
Projet est publié tooAzure cette hello étape Visual Studio. Cette étape de hello vidéo commence à 5 h 45.

toopublish hello tooAzure du projet, avec le bouton droit hello **APIMAADDemo** de projet dans Visual Studio et choisissez **publier**. Conserver les paramètres par défaut de hello Bonjour **publier le site Web** boîte de dialogue et cliquez sur **publier**.

![Publier un site web][api-management-web-publish]

## <a name="grant-permissions-toohello-azure-ad-backend-service-application"></a>Autoriser l’application de service principal toohello Azure AD
Une nouvelle application de service principal de hello est créée dans votre annuaire Azure AD en tant que partie de la configuration de hello et processus de publication de votre projet d’API Web. Dans cette étape de hello vidéo, en commençant à 6:13, autorisations sont accordées de toohello API Web principal.

![Application][api-management-aad-backend-app]

Cliquez sur nom hello hello autorisations des applications tooconfigure hello requis. Accédez toohello **configurer** onglet et faites défiler toohello **autorisations tooother applications** section. Cliquez sur hello **autorisations d’Application** liste déroulante en regard de **Windows** **Azure Active Directory**, la case hello pour **lire les données d’annuaire**, puis cliquez sur **enregistrer**.

![Ajout d’autorisations][api-management-aad-add-permissions]

> [!NOTE]
> Si **Windows** **Azure Active Directory** est ne pas répertorié sous autorisations tooother applications, cliquez sur **ajouter application** et l’ajouter à partir de la liste de hello.
> 
> 

Prenez note de hello **URI Id d’application** pour une utilisation dans une étape ultérieure lorsqu’une application Azure AD est configurée pour le portail des développeurs gestion des API hello.

![URI ID d’application][api-management-aad-sso-uri]

## <a name="import-hello-web-api-into-api-management"></a>Importer hello Web API de gestion des API
API est configurés à partir du portail de publication d’API hello, qui est accessible via hello portail Azure. tooreach, cliquez sur **portail de publication** à partir de la barre d’outils hello de votre service de gestion des API. Si vous n’avez pas encore créé une instance de service de gestion des API, consultez [de créer une instance de service de gestion des API] [ Create an API Management service instance] Bonjour [gérer votre première API] [ Manage your first API] didacticiel.

![Portail des éditeurs][api-management-management-console]

Les opérations peuvent être [ajoutés manuellement les tooAPIs](api-management-howto-add-operations.md), ou elles peuvent être importées. Dans cette vidéo, à partir de 6’40’’, les opérations sont importées au format Swagger.

Créez un fichier nommé `calcapi.json` avec suivant le contenu et l’enregistrer tooyour ordinateur. Vérifiez que hello `host` attribut pointe tooyour API Web principal. Dans cet exemple, on utilise `"host": "apimaaddemo.azurewebsites.net"` .

```json
{
  "swagger": "2.0",
  "info": {
    "title": "Calculator",
    "description": "Arithmetics over HTTP!",
    "version": "1.0"
  },
  "host": "apimaaddemo.azurewebsites.net",
  "basePath": "/api",
  "schemes": [
    "http"
  ],
  "paths": {
    "/add?a={a}&b={b}": {
      "get": {
        "description": "Responds with a sum of two numbers.",
        "operationId": "Add two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>51</code>.",
            "required": true,
            "type": "string",
            "default": "51",
            "enum": [
              "51"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>49</code>.",
            "required": true,
            "type": "string",
            "default": "49",
            "enum": [
              "49"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/sub?a={a}&b={b}": {
      "get": {
        "description": "Responds with a difference between two numbers.",
        "operationId": "Subtract two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>100</code>.",
            "required": true,
            "type": "string",
            "default": "100",
            "enum": [
              "100"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>50</code>.",
            "required": true,
            "type": "string",
            "default": "50",
            "enum": [
              "50"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/div?a={a}&b={b}": {
      "get": {
        "description": "Responds with a quotient of two numbers.",
        "operationId": "Divide two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>100</code>.",
            "required": true,
            "type": "string",
            "default": "100",
            "enum": [
              "100"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>20</code>.",
            "required": true,
            "type": "string",
            "default": "20",
            "enum": [
              "20"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/mul?a={a}&b={b}": {
      "get": {
        "description": "Responds with a product of two numbers.",
        "operationId": "Multiply two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>20</code>.",
            "required": true,
            "type": "string",
            "default": "20",
            "enum": [
              "20"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>5</code>.",
            "required": true,
            "type": "string",
            "default": "5",
            "enum": [
              "5"
            ]
          }
        ],
        "responses": { }
      }
    }
  }
}
```

calcul de hello tooimport API, cliquez sur **API** de hello **gestion des API** menu sur hello gauche, puis cliquez sur **API d’importation**.

![Bouton Importer l’API][api-management-import-api]

Effectuer hello suivant les étapes tooconfigure hello calculatrice API.

1. Cliquez sur **à partir du fichier**, parcourir toohello `calculator.json` fichier que vous avez enregistré, puis cliquez sur hello **Swagger** case d’option.
2. Type **calc** dans hello **suffixe d’URL d’API Web** zone de texte.
3. Cliquez sur Bonjour **produits (facultatifs)** et sélectionnez **Starter**.
4. Cliquez sur **enregistrer** tooimport hello API.

![Ajouter une nouvelle API][api-management-import-new-api]

Une fois les API hello est importé, hello page Résumé pour l’API de hello s’affiche dans le portail de publication hello.

## <a name="call-hello-api-unsuccessfully-from-hello-developer-portal"></a>Appeler les API hello sans succès à partir du portail des développeurs hello
À ce stade, hello API a été importé dans la gestion des API, mais ne peut pas encore être appelée avec succès à partir du portail des développeurs hello, car le service principal de hello est protégé par l’authentification Azure AD. Cela est illustré dans la vidéo hello commençant à 7:40 à l’aide de hello comme suit.

Cliquez sur **portail des développeurs** de hello en haut à droite du portail de publication hello.

![Portail des développeurs][api-management-developer-portal-menu]

Cliquez sur **API** et cliquez sur hello **calculatrice** API.

![Portail des développeurs][api-management-dev-portal-apis]

Cliquez sur **Essayer**.

![Essayer][api-management-dev-portal-try-it]

Cliquez sur **envoyer** et notez l’état de réponse hello de **401 non autorisé**.

![Envoyer][api-management-dev-portal-send-401]

demande de Hello n’est pas autorisé, car les API de service principal hello est protégé par Azure Active Directory. Avant d’appeler correctement les API de hello portail des développeurs hello doit être développeurs tooauthorize configuré à l’aide d’OAuth 2.0. Ce processus est décrit dans les sections suivantes de hello.

## <a name="register-hello-developer-portal-as-an-aad-application"></a>Portail des développeurs hello inscrire comme une application AAD
Hello première étape de configuration aux développeurs tooauthorize portail hello développeur à l’aide d’OAuth 2.0 est un portail des développeurs hello tooregister comme une application AAD. Cela est illustré en commençant à 8:27 vidéo de hello.

Accédez locataire toohello Azure AD à partir de la première étape de hello de cette vidéo, dans cet exemple **APIMDemo** et accédez toohello **Applications** onglet.

![Nouvelle application][api-management-aad-new-application-devportal]

Cliquez sur hello **ajouter** bouton toocreate une application Azure Active Directory, puis choisissez **ajouter une application développée par mon organisation**.

![Nouvelle application][api-management-new-aad-application-menu]

Choisissez **Web application et/ou API Web**, entrez un nom et cliquez sur la flèche suivant de hello. Dans cet exemple, on utilise **APIMDeveloperPortal** .

![Nouvelle application][api-management-aad-new-application-devportal-1]

Pour **URL de connexion** entrez hello les URL de votre service de gestion des API et ajoutez `/signin`. Dans cet exemple, on utilise `https://contoso5.portal.azure-api.net/signin` .

Pour **URL Id d’application** entrez hello les URL de votre service de gestion des API et l’ajout de caractères uniques. Il peut s’agir des caractères de votre choix. Dans cet exemple, on utilise `https://contoso5.portal.azure-api.net/dp`. Lorsque hello souhaité **propriétés de l’application** sont configurées, cliquez sur application de hello toocreate hello case à cocher.

![Nouvelle application][api-management-aad-new-application-devportal-2]

## <a name="configure-an-api-management-oauth-20-authorization-server"></a>Configuration du serveur d’autorisation OAuth 2.0 dans Gestion des API
étape suivante de Hello est tooconfigure un serveur d’autorisation OAuth 2.0 dans Gestion des API. Cette étape est illustrée dans hello vidéo en commençant à 9:43.

Cliquez sur **sécurité** à partir du menu Gestion des API hello hello gauche, cliquez sur **OAuth 2.0**, puis cliquez sur **ajouter une autorisation** server.

![Ajouter un serveur d’autorisation][api-management-add-authorization-server]

Entrez un nom et une description facultative dans hello **nom** et **Description** champs. Ces champs sont le serveur de d’autorisation hello OAuth 2.0 tooidentify utilisés au sein de l’instance de service de gestion des API hello. Dans cet exemple, on utilise **Démonstration de serveur d’autorisation** . Plus tard lorsque vous spécifiez une toobe de serveur OAuth 2.0 utilisé pour l’authentification d’API, vous allez sélectionner ce nom.

Pourquoi **URL de la page d’inscription Client** Entrez une valeur d’espace réservé tel que `http://localhost`.  Hello **URL de la page d’inscription Client** points toohello page que les utilisateurs peuvent utiliser toocreate et configurer leurs propres comptes pour les fournisseurs OAuth 2.0 qui prennent en charge la gestion des comptes d’utilisateur. Dans cet exemple, les utilisateurs ne peuvent pas créer et configurer leurs propres comptes. Ainsi, on utilise un espace réservé.

![Ajouter un serveur d’autorisation][api-management-add-authorization-server-1]

Ensuite, spécifiez l’**URL de point de terminaison d’autorisation** et l’**URL de point de terminaison de jeton**.

![Serveur d’autorisation][api-management-add-authorization-server-1a]

Ces valeurs peuvent être récupérées à partir de hello **points de terminaison** page Hello application AAD que vous avez créé pour le portail des développeurs hello. points de terminaison tooaccess hello accédez toohello **configurer** onglet pour l’application de AAD hello et cliquez sur **afficher les points de terminaison**.

![Application][api-management-aad-devportal-application]

![Afficher les points de terminaison][api-management-aad-view-endpoints]

Hello de copie **point de terminaison d’autorisation OAuth 2.0** et collez-le dans hello **URL de point de terminaison d’autorisation** zone de texte.

![Ajouter un serveur d’autorisation][api-management-add-authorization-server-2]

Hello de copie **point de terminaison de jeton OAuth 2.0** et collez-le dans hello **URL de point de terminaison de jeton** zone de texte.

![Ajouter un serveur d’autorisation][api-management-add-authorization-server-2a]

En outre toopasting dans le point de terminaison de jeton hello, ajouter un paramètre de corps supplémentaire nommé **ressource** et pour la valeur de hello utiliser hello **URI Id d’application** de hello application AAD pour service hello principal qui a été créé lors de la publication de projet de Visual Studio hello.

![URI ID d’application][api-management-aad-sso-uri]

Ensuite, spécifiez les informations d’identification du client hello. Ceux-ci sont des informations d’identification de hello pour la ressource hello tooaccess, hello dans ce cas le portail des développeurs.

![Informations d'identification du client][api-management-client-credentials]

tooget hello **Id Client**, accédez toohello **configurer** onglet Hello application AAD pour hello portal et la copie du développeur hello **Id Client**.

tooget hello **clé secrète Client** cliquez sur hello **sélectionner une durée** déroulante Bonjour **clés** section et spécifiez un intervalle. Dans cet exemple, on utilise la valeur 1 an.

![ID client][api-management-aad-client-id]

Cliquez sur **enregistrer** clé hello toosave hello configuration et l’affichage. 

> [!IMPORTANT]
> Notez sa valeur. Une fois que vous fermez la fenêtre de configuration d’Azure Active Directory hello, clé de hello Impossible d’afficher à nouveau.
> 
> 

Copie hello toohello clé coller depuis le Presse-papiers, portail de publication commutateur toohello arrière, clé de hello en hello **clé secrète Client** zone de texte, puis cliquez sur **enregistrer**.

![Ajouter un serveur d’autorisation][api-management-add-authorization-server-3]

Immédiatement après les informations d’identification du client hello est un octroi de code d’autorisation. Copiez le code d’autorisation et tooyour arrière du commutateur application du portail Azure AD développeur page, ainsi coller d’octroi de hello hello **URL de réponse** champ, puis cliquez sur **enregistrer** à nouveau.

![URL de réponse][api-management-aad-reply-url]

étape suivante de Hello est tooconfigure les autorisations de hello pour le portail des développeurs hello application AAD. Cliquez sur **autorisations d’Application** et hello la case pour **lire les données d’annuaire**. Cliquez sur **enregistrer** toosave cette modification, puis cliquez sur **ajouter application**.

![Ajout d’autorisations][api-management-add-devportal-permissions]

Cliquez sur icône de recherche hello, type **APIM** dans hello commençant par, sélectionnez **APIMAADDemo**, puis cliquez sur toosave de case à cocher hello.

![Ajout d’autorisations][api-management-aad-add-app-permissions]

Cliquez sur **autorisations déléguées** pour **APIMAADDemo** et hello la case pour **accès APIMAADDemo**, puis cliquez sur **enregistrer**. Ainsi, développeur de hello service principal d’application de portail tooaccess hello.

![Ajout d’autorisations][api-management-aad-add-delegated-permissions]

## <a name="enable-oauth-20-user-authorization-for-hello-calculator-api"></a>Activer l’autorisation de l’utilisateur OAuth 2.0 pour hello calculatrice API
Maintenant que hello serveur OAuth 2.0 est configuré, vous pouvez le spécifier dans les paramètres de sécurité hello pour votre API. Cette étape est illustrée dans hello vidéo en commençant à 14:30.

Cliquez sur **API** dans hello du menu de gauche, puis cliquez sur **calculatrice** tooview et configurer ses paramètres.

![API de calcul][api-management-calc-api]

Accédez toohello **sécurité** onglet, vérifiez hello **OAuth 2.0** case à cocher, le serveur de l’autorisation souhaitée de hello sélectionnez à partir de hello **serveur d’autorisation** liste déroulante, puis cliquez sur **Enregistrer**.

![API de calcul][api-management-enable-aad-calculator]

## <a name="successfully-call-hello-calculator-api-from-hello-developer-portal"></a>Appeler à partir du portail des développeurs hello hello calculatrice API
Maintenant que l’autorisation de hello OAuth 2.0 est configurée sur hello API, ses opérations peuvent être appelées avec succès à partir du centre de développement hello. Cette étape est illustrée dans hello vidéo en commençant à 15:00.

Accédez arrière toohello **ajouter deux entiers** opération du service de calculatrice hello dans le portail des développeurs hello et cliquez sur **essayez-la**. Remarque hello nouvel élément Bonjour **autorisation** section serveur d’autorisation toohello correspondant vous venez d’ajouter.

![API de calcul][api-management-calc-authorization-server]

Sélectionnez **code d’autorisation** à partir de l’autorisation hello déroulante liste, puis entrez les informations d’identification hello de hello compte toouse. Si vous êtes déjà connecté avec hello compte, vous ne pouvez pas invité.

![API de calcul][api-management-devportal-authorization-code]

Cliquez sur **envoyer** et Remarque Bonjour **état de la réponse** de **200 OK** et des résultats d’opération hello dans le contenu de la réponse hello hello.

![API de calcul][api-management-devportal-response]

## <a name="configure-a-desktop-application-toocall-hello-api"></a>Configurer un Bonjour de toocall API application de bureau
procédure suivante de Hello Bonjour vidéo démarre à 16 h 30 et configure un Bonjour de toocall API simple application de bureau. première étape de Hello est l’application de bureau tooregister hello dans Azure AD et lui donner accès toohello directory et toohello principal du service. À 18:25, il existe une démonstration d’application de bureau hello appel d’opération de calculatrice de hello API.

## <a name="configure-a-jwt-validation-policy-toopre-authorize-requests"></a>Configurer un toopre de stratégie de validation de jetons Web JSON-autoriser les demandes
commence à 20:48 Hello procédure finale dans la vidéo de hello et vous montre comment toouse hello [valider les jetons Web JSON](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT) stratégie toopre-autoriser les demandes en validant les jetons d’accès hello de chaque demande entrante. Si la demande de hello n’est pas validé par hello stratégie de valider les jetons Web JSON, demande de hello est bloquée par la gestion des API et n’est pas passé toohello principal.

```xml
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">
    <openid-config url="https://login.microsoftonline.com/DemoAPIM.onmicrosoft.com/.well-known/openid-configuration" />
    <required-claims>
        <claim name="aud">
            <value>https://DemoAPIM.NOTonmicrosoft.com/APIMAADDemo</value>
        </claim>
    </required-claims>
</validate-jwt>
```

Pour une autre démonstration de configuration et l’utilisation de cette stratégie, consultez [Cloud couvrent épisode 177 : fonctionnalités de gestion des API plus](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) et avançons too13:50. Avance rapide too15:00 les stratégies de hello toosee configurées dans l’éditeur de stratégie hello et puis too18:50 pour une démonstration de l’appel d’une opération à partir du portail des développeurs hello avec et sans hello requis jeton d’autorisation.

## <a name="next-steps"></a>Étapes suivantes
* Découvrez plus de [vidéos](https://azure.microsoft.com/documentation/videos/index/?services=api-management) sur Gestion des API.
* Pour les autres façons toosecure votre service principal, consultez [authentification mutuelle des certificats](api-management-howto-mutual-certificates.md).

[api-management-management-console]: ./media/api-management-howto-protect-backend-with-aad/api-management-management-console.png

[api-management-import-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-import-api.png
[api-management-import-new-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-import-new-api.png
[api-management-create-aad-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-create-aad-menu.png
[api-management-create-aad]: ./media/api-management-howto-protect-backend-with-aad/api-management-create-aad.png
[api-management-new-web-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-web-app.png
[api-management-new-project]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-project.png
[api-management-new-project-cloud]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-project-cloud.png
[api-management-change-authentication]: ./media/api-management-howto-protect-backend-with-aad/api-management-change-authentication.png
[api-management-sign-in-vidual-studio]: ./media/api-management-howto-protect-backend-with-aad/api-management-sign-in-vidual-studio.png
[api-management-configure-web-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-configure-web-app.png
[api-management-aad-domains]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-domains.png
[api-management-add-controller]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-controller.png
[api-management-web-publish]: ./media/api-management-howto-protect-backend-with-aad/api-management-web-publish.png
[api-management-aad-backend-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-backend-app.png
[api-management-aad-add-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-permissions.png
[api-management-developer-portal-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-developer-portal-menu.png
[api-management-dev-portal-apis]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-apis.png
[api-management-dev-portal-try-it]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-try-it.png
[api-management-dev-portal-send-401]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-send-401.png
[api-management-aad-new-application-devportal]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal.png
[api-management-aad-new-application-devportal-1]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal-1.png
[api-management-aad-new-application-devportal-2]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal-2.png
[api-management-aad-devportal-application]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-devportal-application.png
[api-management-add-authorization-server]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server.png
[api-management-aad-sso-uri]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-sso-uri.png
[api-management-aad-view-endpoints]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-view-endpoints.png
[api-management-aad-client-id]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-client-id.png
[api-management-add-authorization-server-1]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-1.png
[api-management-add-authorization-server-2]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-2.png
[api-management-add-authorization-server-2a]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-2a.png
[api-management-add-authorization-server-3]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-3.png
[api-management-aad-reply-url]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-reply-url.png
[api-management-add-devportal-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-devportal-permissions.png
[api-management-aad-add-app-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-app-permissions.png
[api-management-aad-add-delegated-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-delegated-permissions.png
[api-management-calc-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-calc-api.png
[api-management-enable-aad-calculator]: ./media/api-management-howto-protect-backend-with-aad/api-management-enable-aad-calculator.png
[api-management-devportal-authorization-code]: ./media/api-management-howto-protect-backend-with-aad/api-management-devportal-authorization-code.png
[api-management-devportal-response]: ./media/api-management-howto-protect-backend-with-aad/api-management-devportal-response.png
[api-management-calc-authorization-server]: ./media/api-management-howto-protect-backend-with-aad/api-management-calc-authorization-server.png
[api-management-add-authorization-server-1a]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-1a.png
[api-management-client-credentials]: ./media/api-management-howto-protect-backend-with-aad/api-management-client-credentials.png
[api-management-new-aad-application-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-aad-application-menu.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Manage your first API]: api-management-get-started.md
