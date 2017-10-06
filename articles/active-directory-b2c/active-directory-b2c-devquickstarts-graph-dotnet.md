---
title: "Azure B2C Active Directory : Hello d’utiliser API Graph | Documents Microsoft"
description: "Comment toocall hello API Graph pour un locataire B2C à l’aide d’un processus identité tooautomate hello."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f9904516-d9f7-43b1-ae4f-e4d9eb1c67a0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/07/2017
ms.author: parakhj
ms.openlocfilehash: a17cdc4adf57dbf22592d99ef8ecde41652763fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-use-hello-graph-api"></a>Azure AD B2C : Utilisez hello API Graph
Les clients Azure Active Directory (Azure AD) B2C ont tendance à toobe très volumineux. Cela signifie que plusieurs tâches courantes de gestion client doivent toobe effectuée par programme. La gestion des utilisateurs en est un parfait exemple. Vous devrez peut-être toomigrate un client utilisateur magasin tooa B2C. Vous pouvez souhaitez toohost d’inscription des utilisateurs sur votre page et créer des comptes d’utilisateur dans votre annuaire Azure AD B2C coulisses hello. Ces types de tâches nécessitent hello capacité toocreate, lecture, mise à jour et supprimer des comptes d’utilisateur. Vous pouvez effectuer ces tâches à l’aide des API d’Azure AD Graph hello.

Pour les locataires B2C, il existe deux modes de communication avec l’API Graph de hello.

* Pour les tâches interactives, exécution unique, vous devez agir comme un compte d’administrateur de client de B2C hello lorsque vous effectuez des tâches de hello. Ce mode requiert une toosign administrateur avec informations d’identification avant de l’administrateur peut effectuer n’importe quel toohello appelle l’API Graph.
* Pour les tâches automatisés en continu, vous devez utiliser un type de compte de service que vous fournissez avec les tâches de gestion tooperform hello des privilèges nécessaires. Dans Azure AD, cela par enregistrez une application et l’authentification tooAzure AD. Cela en utilisant un **ID d’Application** qui utilise hello [accorder des informations d’identification du client OAuth 2.0](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api). Dans ce cas, application hello joue le rôle lui-même, pas en tant qu’utilisateur, toocall hello API Graph.

Dans cet article, nous expliquerons comment tooperform hello cas d’usage automatisée. toodemonstrate, nous allons construire un .NET 4.5 `B2CGraphClient` qui effectue l’utilisateur créer, lire, mettre à jour et suppression (CRUD). client de Hello aura une interface de ligne de commande de Windows (CLI) qui vous permet de tooinvoke différentes méthodes. Cependant, le code de hello est écrite toobehave de manière non interactive et automatisée.

## <a name="get-an-azure-ad-b2c-tenant"></a>Obtention d’un client Azure AD B2C
Avant de pouvoir créer des applications ou utilisateurs, ou interagir avec Azure AD du tout, vous devez un locataire Azure AD B2C et un compte d’administrateur général dans le locataire de hello. Si vous n’avez pas encore de client, suivez le guide de [prise en main d’Azure AD B2C](active-directory-b2c-get-started.md).

## <a name="register-your-application-in-your-tenant"></a>Inscrire votre application dans votre locataire
Une fois que vous avez un locataire B2C, vous devez tooregister votre application via hello [Azure Portal](https://portal.azure.com).

> [!IMPORTANT]
> API de Graph toouse hello avec votre client B2C, vous devez tooregister une application dédiée à l’aide de hello générique *inscriptions d’application* panneau Bonjour Azure Portal, **pas** de B2C Azure AD  *Applications* panneau. Vous ne pouvez pas réutiliser hello existante B2C applications que vous avez enregistré dans hello du B2C Azure AD *Applications* panneau.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Choisissez votre locataire Azure AD B2C en sélectionnant votre compte dans hello coin supérieur droit de la page de hello.
3. Dans le volet de navigation gauche hello, choisissez **plus Services**, cliquez sur **inscriptions d’application**, puis cliquez sur **ajouter**.
4. Suivez les invites hello et créez une nouvelle application. 
    1. Sélectionnez **application Web / API** comme hello du Type d’Application.    
    2. Fournissez **les URI de redirection** (par exemple, https://B2CGraphAPI) dans la mesure où cela n’est pas pertinent pour cet exemple.  
5. Hello application va maintenant s’affichent dans la liste de hello des applications, cliquez sur cette tooobtain hello **ID de l’Application** (également appelé ID de Client). Copiez-le, car vous en aurez besoin dans une section ultérieure.
6. Dans le panneau des paramètres de hello, cliquez sur **clés** et ajoutez une nouvelle clé (également appelé clé secrète du client). Copiez-la également pour une utilisation dans une section ultérieure.

## <a name="configure-create-read-and-update-permissions-for-your-application"></a>Configurer les autorisations Créer, Lire et Mettre à jour pour votre application
Maintenant vous devez tooconfigure votre tooget application que tous hello requis toocreate d’autorisations, lire, mettre à jour et supprimer des utilisateurs.

1. Continuer dans hello panneau d’inscriptions d’application du portail Azure, sélectionnez votre application.
2. Dans le panneau des paramètres de hello, cliquez sur **autorisations requises**.
3. Dans le panneau des autorisations requises hello, cliquez sur **Windows Azure Active Directory**.
4. Dans le panneau d’activer l’accès hello, sélectionnez hello **les données d’annuaire en lecture et écriture** autorisation **autorisations d’Application** et cliquez sur **enregistrer**.
5. Enfin, dans le panneau des autorisations requises hello, cliquez sur hello **accorder des autorisations** bouton.

Vous avez maintenant une application qui a l’autorisation toocreate, lecture et mise à jour les utilisateurs de votre client B2C.

## <a name="configure-delete-permissions-for-your-application"></a>Configurer les autorisations de suppression pour votre application
Actuellement, hello *les données d’annuaire en lecture et écriture* autorisation est **pas** inclure hello capacité toodo toutes les suppressions, telles que la suppression des utilisateurs. Si vous souhaitez toogive vos utilisateurs de toodelete application hello possibilité, vous devez toodo ces étapes supplémentaires qui impliquent de PowerShell, dans le cas contraire, vous pouvez ignorer la section suivante de toohello.

Tout d’abord, téléchargez et installez hello [Assistant Microsoft Online Services Sign-In](http://go.microsoft.com/fwlink/?LinkID=286152). Puis téléchargez et installez hello [64 bits du module Active Directory de Azure pour Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).

Après avoir installé le module PowerShell de hello, ouvrez PowerShell et se connecter tooyour B2C locataire. Après avoir exécuté `Get-Credential`, être invité à entrer un nom d’utilisateur et mot de passe, entrée hello nom d’utilisateur et mot de passe de votre compte d’administrateur client B2C.

> [!IMPORTANT]
> Vous devez le compte d’administrateur de client toouse un B2C est **local** toohello B2C locataire. Ces comptes se présentent comme suit : myusername@myb2ctenant.onmicrosoft.com.

```powershell
Connect-MsolService
```

Maintenant, nous allons utiliser hello **ID d’Application** dans le script hello ci-dessous tooassign hello application hello compte administrateur rôle d’utilisateur qui lui permettront de toodelete utilisateurs. Ces rôles ont des identificateurs connus, donc vous devez toodo est entrée votre **ID d’Application** dans le script hello ci-dessous.

```powershell
$applicationId = "<YOUR_APPLICATION_ID>"
$sp = Get-MsolServicePrincipal -AppPrincipalId $applicationId
Add-MsolRoleMember -RoleObjectId fe930be7-5e62-47db-91af-98c3a49a38b1 -RoleMemberObjectId $sp.ObjectId -RoleMemberType servicePrincipal
```

Votre application maintenant possède également des autorisations accordées aux utilisateurs de toodelete à partir de votre client B2C.

## <a name="download-configure-and-build-hello-sample-code"></a>Télécharger, configurer et générer l’exemple de code hello
Tout d’abord, téléchargez l’exemple de code hello et pouvoir l’exécuter. Nous l’examinerons ensuite plus en détail.  Vous pouvez [télécharger l’exemple de code hello sous forme de fichier .zip](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip). Vous pouvez également le cloner dans un répertoire de votre choix :

```
git clone https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet.git
```

Ouvrez hello `B2CGraphClient\B2CGraphClient.sln` solution Visual Studio dans Visual Studio. Bonjour `B2CGraphClient` projet, les fichiers ouverts hello `App.config`. Remplacez les trois paramètres d’application hello par vos propres valeurs :

```
<appSettings>
    <add key="b2c:Tenant" value="{Your Tenant Name}" />
    <add key="b2c:ClientId" value="{hello ApplicationID from above}" />
    <add key="b2c:ClientSecret" value="{hello Key from above}" />
</appSettings>
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

Ensuite, avec le bouton droit sur hello `B2CGraphClient` hello, exemple solution et de reconstruction. Si l’opération aboutit, vous devez maintenant disposer d’un fichier exécutable `B2C.exe` dans le répertoire `B2CGraphClient\bin\Debug`.

## <a name="build-user-crud-operations-by-using-hello-graph-api"></a>Générer des opérations CRUD de l’utilisateur à l’aide de l’API Graph de hello
toouse hello B2CGraphClient, ouvrez un `cmd` de commande Windows invite de commandes et modifiez votre toohello active `Debug` active. Puis exécutez hello `B2C Help` commande.

```
> cd B2CGraphClient\bin\Debug
> B2C Help
```

Ceci affiche une brève description de chaque commande. Chaque fois que vous appelez une de ces commandes, `B2CGraphClient` rend un toohello demande API Azure AD Graph.

### <a name="get-an-access-token"></a>Obtention d’un jeton d’accès
N’importe quel toohello demande API Graph nécessite un jeton d’accès pour l’authentification. `B2CGraphClient`utilise hello open source Active Directory Authentication Library (ADAL) toohelp d’acquisition de jetons d’accès. La bibliothèque ADAL facilite l’acquisition des jetons en fournissant une API simple et en prenant soin de certains détails importants, tels que la mise en cache des jetons d’accès. Vous n’avez toouse tooget ADAL jetons, cependant. Vous pouvez également en obtenir en créant des requêtes HTTP.

> [!NOTE]
> Cet exemple de code utilise la bibliothèque ADAL v2 dans toocommunicate ordre avec hello API Graph.  Vous devez utiliser la bibliothèque ADAL v2 ou v3 dans les jetons d’accès ordre tooget qui peuvent être utilisés avec hello API Azure AD Graph.
> 
> 

Lorsque `B2CGraphClient` s’exécute, il crée une instance de hello `B2CGraphClient` classe. constructeur Hello pour cette classe définit une structure de l’authentification ADAL :

```C#
public B2CGraphClient(string clientId, string clientSecret, string tenant)
{
    // hello client_id, client_secret, and tenant are provided in Program.cs, which pulls hello values from App.config
    this.clientId = clientId;
    this.clientSecret = clientSecret;
    this.tenant = tenant;

    // hello AuthenticationContext is ADAL's primary class, in which you indicate hello tenant toouse.
    this.authContext = new AuthenticationContext("https://login.microsoftonline.com/" + tenant);

    // hello ClientCredential is where you pass in your client_id and client_secret, which are
    // provided tooAzure AD in order tooreceive an access_token by using hello app's identity.
    this.credential = new ClientCredential(clientId, clientSecret);
}
```

Nous allons utiliser hello `B2C Get-User` commande par exemple. Lorsque `B2C Get-User` est appelé sans des entrées supplémentaires, hello CLI appels hello `B2CGraphClient.GetAllUsers(...)` (méthode). Cette méthode appelle `B2CGraphClient.SendGraphGetRequest(...)`, qui envoie une API Graph toohello de demande HTTP GET. Avant de `B2CGraphClient.SendGraphGetRequest(...)` envoie hello demande GET, il tout d’abord Obtient un jeton d’accès à l’aide de la bibliothèque ADAL :

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    // First, use ADAL tooacquire a token by using hello app's identity (hello credential)
    // hello first parameter is hello resource we want an access_token for; in this case, hello Graph API.
    AuthenticationResult result = authContext.AcquireToken("https://graph.windows.net", credential);

    ...

```

Vous pouvez obtenir un jeton accès pour hello API Graph en appelant hello ADAL `AuthenticationContext.AcquireToken(...)` (méthode). La bibliothèque ADAL retourne ensuite un `access_token` qui représente l’identité de l’application hello.

### <a name="read-users"></a>Lecture des utilisateurs
Lorsque vous souhaitez tooget une liste d’utilisateurs ou obtenez un utilisateur particulier de hello API Graph, vous pouvez envoyer un HTTP `GET` demande toohello `/users` point de terminaison. Une demande pour tous les utilisateurs de hello dans un locataire ressemble à ceci :

```
GET https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

toosee cette requête, exécutez :

 ```
 > B2C Get-User
 ```

Il existe deux éléments importants toonote :

* Hello jeton d’accès obtenu via la bibliothèque ADAL est ajouté toohello `Authorization` en-tête à l’aide de hello `Bearer` schéma.
* Pour les locataires B2C, vous devez utiliser le paramètre de requête hello `api-version=1.6`.

Les deux de ces informations sont gérées dans hello `B2CGraphClient.SendGraphGetRequest(...)` méthode :

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    ...

    // For B2C user management, be sure toouse hello 1.6 Graph API version.
    HttpClient http = new HttpClient();
    string url = "https://graph.windows.net/" + tenant + api + "?" + "api-version=1.6";
    if (!string.IsNullOrEmpty(query))
    {
        url += "&" + query;
    }

    // Append hello access token for hello Graph API toohello Authorization header of hello request by using hello Bearer scheme.
    HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, url);
    request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
    HttpResponseMessage response = await http.SendAsync(request);

    ...
```

### <a name="create-consumer-user-accounts"></a>Création de comptes d’utilisateurs clients
Lorsque vous créez des comptes d’utilisateur dans votre client B2C, vous pouvez envoyer un HTTP `POST` demande toohello `/users` point de terminaison :

```
POST https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 338

{
    // All of these properties are required toocreate consumer users.

    "accountEnabled": true,
    "signInNames": [                            // controls which identifier hello user uses toosign in toohello account
        {
            "type": "emailAddress",             // can be 'emailAddress' or 'userName'
            "value": "joeconsumer@gmail.com"
        }
    ],
    "creationType": "LocalAccount",            // always set too'LocalAccount'
    "displayName": "Joe Consumer",                // a value that can be used for displaying toohello end user
    "mailNickname": "joec",                        // an email alias for hello user
    "passwordProfile": {
        "password": "P@ssword!",
        "forceChangePasswordNextLogin": false   // always set toofalse
    },
    "passwordPolicies": "DisablePasswordExpiration"
}
```

La plupart de ces propriétés dans cette demande est des utilisateurs de consommateur toocreate requis. est de plus, cliquez sur toolearn [ici](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser). Notez que hello `//` commentaires ont été ajoutés à titre d’illustration. Ne les incluez pas dans une requête réelle.

demande de hello toosee, exécutez une des hello suivant de commandes :

```
> B2C Create-User ..\..\..\usertemplate-email.json
> B2C Create-User ..\..\..\usertemplate-username.json
```

Hello `Create-User` commande accepte un fichier .json comme paramètre d’entrée. Celui-ci contient une représentation JSON d’un objet utilisateur. Il existe deux exemples de fichiers .json dans l’exemple de code hello : `usertemplate-email.json` et `usertemplate-username.json`. Vous pouvez modifier ces toosuit de fichiers à vos besoins. En outre toohello requis des champs ci-dessus, plusieurs champs facultatifs que vous pouvez utiliser sont inclus dans ces fichiers. Vous trouverez plus d’informations sur les champs facultatifs hello Bonjour [référence d’entité API Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity).

Vous pouvez voir comment la requête POST de hello est construit dans `B2CGraphClient.SendGraphPostRequest(...)`.

* Attache un toohello de jeton d’accès `Authorization` en-tête de demande de hello.
* définit le paramètre `api-version=1.6`;
* Il inclut objet utilisateur JSON hello dans les corps de hello de demande de hello.

> [!NOTE]
> Si hello comptes que vous souhaitez toomigrate à partir d’un magasin d’utilisateur existant a le niveau inférieur de mot de passe que hello [force du mot de passe fort appliquée par Azure AD B2C](https://msdn.microsoft.com/library/azure/jj943764.aspx), vous pouvez désactiver l’exigence de mot de passe fort hello à l’aide de hello `DisableStrongPassword`valeur Bonjour `passwordPolicies` propriété. Par exemple, vous pouvez modifier hello créer une demande d’utilisateur fourni ci-dessus comme suit : `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`.
> 
> 

### <a name="update-consumer-user-accounts"></a>Mise à jour de comptes d’utilisateurs clients
Lorsque vous mettez à jour les objets utilisateur, les processus de hello est similaire toohello celui que vous utilisez des objets de l’utilisateur toocreate. Mais ce processus utilise hello HTTP `PATCH` méthode :

```
PATCH https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 37

{
    "displayName": "Joe Consumer",                // this request updates only hello user's displayName
}
```

Essayez de tooupdate un utilisateur en mettant à jour vos fichiers JSON avec de nouvelles données. Vous pouvez ensuite utiliser `B2CGraphClient` toorun une des commandes suivantes :

```
> B2C Update-User <user-object-id> ..\..\..\usertemplate-email.json
> B2C Update-User <user-object-id> ..\..\..\usertemplate-username.json
```

Inspecter hello `B2CGraphClient.SendGraphPatchRequest(...)` méthode pour plus d’informations sur la façon de toosend cette demande.

### <a name="search-users"></a>Rechercher des utilisateurs
Vous pouvez rechercher des utilisateurs dans votre client B2C de deux façons. Un, à l’aide des ID d’objet ou les deux, à l’aide de connectez-vous identificateur l’utilisateur hello de l’utilisateur hello (c'est-à-dire hello `signInNames` propriété).

Exécutez une des hello suivant toosearch de commandes pour un utilisateur spécifique :

```
> B2C Get-User <user-object-id>
> B2C Get-User <filter-query-expression>
```

Voici quelques exemples :

```
> B2C Get-User 2bcf1067-90b6-4253-9991-7f16449c2d91
> B2C Get-User $filter=signInNames/any(x:x/value%20eq%20%27joeconsumer@gmail.com%27)
```

### <a name="delete-users"></a>Suppression d’utilisateurs
processus Hello pour la suppression d’un utilisateur est simple. Hello d’utiliser HTTP `DELETE` méthode et la construction des URL de hello avec hello corriger l’ID d’objet :

```
DELETE https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

toosee un exemple, entrez cette commande et vue hello supprimer chaque requête qui est imprimée toohello console :

```
> B2C Delete-User <object-id-of-user>
```

Inspecter hello `B2CGraphClient.SendGraphDeleteRequest(...)` méthode pour plus d’informations sur la façon de toosend cette demande.

Vous pouvez effectuer beaucoup d’autres actions avec hello API Azure AD Graph dans la gestion de toouser Ajout. La [référence de l’API Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) fournit des informations détaillées sur chaque action, ainsi que des exemples de demande.

## <a name="use-custom-attributes"></a>Utilisation d’attributs personnalisés
La plupart des applications consommateur devez toostore tout type d’informations de profil utilisateur personnalisée. Pour ce faire consiste toodefine un attribut personnalisé dans votre client B2C. Vous pouvez ensuite traiter ce hello attribut identique à traiter de toute autre propriété sur un objet utilisateur. Vous pouvez mettre à jour les attributs de hello, supprimer l’attribut hello, requête par attribut de hello, envoyer les attributs hello comme revendication dans les jetons d’authentification et bien plus encore.

toodefine un attribut personnalisé dans votre locataire B2C, consultez hello [référence de l’attribut personnalisé B2C](active-directory-b2c-reference-custom-attr.md).

Vous pouvez afficher les attributs personnalisés de hello définis dans votre client B2C à l’aide de `B2CGraphClient`:

```
> B2C Get-B2C-Application
> B2C Get-Extension-Attribute <object-id-in-the-output-of-the-above-command>
```

sortie Hello de ces fonctions révèle détails hello de chaque attribut personnalisé, tel que :

```JSON
{
      "odata.type": "Microsoft.DirectoryServices.ExtensionProperty",
      "objectType": "ExtensionProperty",
      "objectId": "cec6391b-204d-42fe-8f7c-89c2b1964fca",
      "deletionTimestamp": null,
      "appDisplayName": "",
      "name": "extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number",
      "dataType": "Integer",
      "isSyncedFromOnPremises": false,
      "targetObjects": [
        "User"
      ]
}
```

Vous pouvez utiliser hello nom complet, comme `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`, en tant que propriété sur vos objets de l’utilisateur.  Mettre à jour votre fichier .json avec la nouvelle propriété de hello et une valeur pour la propriété de hello, puis exécutez :

```
> B2C Update-User <object-id-of-user> <path-to-json-file>
```

Avec `B2CGraphClient`, vous disposez d’une application de service capable de gérer les utilisateurs de votre client B2C par programmation. `B2CGraphClient`utilise son propre toohello de tooauthenticate d’identité application API Azure AD Graph. et acquiert des jetons à l’aide d’une clé secrète client. Lorsque vous intégrez cette fonctionnalité dans votre application, prenez en considération les quelques points clés suivants pour les applications B2C :

* Vous devez toogrant hello application hello autorisations appropriées dans le locataire de hello.
* Pour l’instant, vous devez les jetons d’accès tooget toouse ADAL (pas MSAL). (vous pouvez également envoyer des messages de protocole directement, sans utiliser de bibliothèque).
* Lorsque vous appelez hello API Graph, utilisez `api-version=1.6`.
* Lorsque vous créez et mettez à jour des utilisateurs clients, certaines propriétés sont requises, comme décrit plus haut.

Si vous avez des questions ou des demandes pour les actions que vous aimeriez tooperform à l’aide de hello API Graph sur votre client B2C, laissez un commentaire sur cet article ou un problème de fichier dans le dépôt d’exemples code hello GitHub.

