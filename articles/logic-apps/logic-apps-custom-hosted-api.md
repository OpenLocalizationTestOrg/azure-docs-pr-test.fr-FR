---
title: "aaaDeploy, appeler et s’authentifier web API et les API REST pour Azure Logic Apps | Documents Microsoft"
description: "Déployer, authentifier et appeler des API web et REST dans les flux de travail d’intégration système avec Azure Logic Apps"
keywords: "API web, API REST, connecteurs, flux de travail, intégration système, authentifier"
services: logic-apps
author: stepsic-microsoft-com
manager: anneta
editor: 
documentationcenter: 
ms.assetid: f113005d-0ba6-496b-8230-c1eadbd6dbb9
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: LADocs; stepsic
ms.openlocfilehash: ca1e4f28196b21f43b7c9ab94029684121e36f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-call-and-authenticate-custom-apis-as-connectors-for-logic-apps"></a>Déployer, appeler et authentifier des API personnalisées en tant que connecteurs pour les applications logiques

Après avoir [créer des API personnalisées](./logic-apps-create-api-app.md) qui fournissent des actions ou des déclencheurs toouse dans la logique de flux de travail applications, vous devez déployer votre API avant de les appeler. Bien que vous pouvez appeler une API à partir d’une application logique, pour une meilleure expérience de hello, ajoutez [Swagger métadonnées](http://swagger.io/specification/) qui décrit les opérations et les paramètres de votre API. Ce fichier Swagger améliore le fonctionnent de votre API et simplifie son intégration aux applications logiques.

Vous pouvez déployer votre API comme [les applications web](../app-service-web/app-service-web-overview.md), mais envisagez de déployer votre API comme [applications API](../app-service-api/app-service-api-apps-why-best-platform.md), qui peut simplifier votre travail lorsque vous générez, hébergez et consommer des API dans le cloud de hello et localement. Vous n’avez pas de code toochange dans votre API--simplement déployer votre application API de tooan code. Vous pouvez héberger votre API sur [Azure App Service](../app-service/app-service-value-prop-what-is.md), un platform-as-a-service (PaaS) qui fournit une des manières de meilleures, plus simple et plus évolutive hello pour l’hébergement de l’API de l’offre.

tooauthenticate les appels d’applications de logique tooyour API, vous pouvez configurer Azure Active Directory Bonjour portail Azure, vous n’avez tooupdate votre code. Vous pouvez également exiger et appliquer une authentification par le biais du code de votre API.

## <a name="deploy-your-api-as-a-web-app-or-api-app"></a>Déployer votre API en tant qu’application web ou application API

Avant de pouvoir appeler votre API personnalisée à partir d’une application logique, déployez votre API comme une application web ou l’API application tooAzure du Service d’applications. En outre, toomake votre document Swagger lisible par hello Concepteur d’application logique, définition des propriétés de définition de hello API et activer [ressources cross-origin (CORS) de partage](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) pour votre application web ou d’une application API.

1. Bonjour portail Azure, sélectionnez votre application web ou une application API.

2. Dans le panneau hello qui s’ouvre, sous **API**, choisissez **définition d’API**. Ensemble hello **emplacement de définition d’API** toohello des URL pour votre fichier swagger.json.

   En règle générale, hello URL s’affiche dans ce format :`https://{name}.azurewebsites.net/swagger/docs/v1)`

   ![Fichier tooSwagger de lien de votre API personnalisée](media/logic-apps-custom-hosted-api/custom-api-swagger-url.png)

3. Sous **API**, choisissez **CORS**. Définir la stratégie CORS hello pour **autorisée origines** trop**'*'** (tous les autoriser).

   Ce paramètre autorise les demandes à partir du concepteur d’application logique.

   ![Autoriser les demandes à partir de l’API de concepteur d’application logique tooyour personnalisée](media/logic-apps-custom-hosted-api/custom-api-cors.png)

Pour plus d’informations, voir les articles suivants :

* [Utiliser l’interface utilisateur et les métadonnées d’API Swagger](../app-service-api/app-service-api-dotnet-get-started.md#use-swagger-api-metadata-and-ui)
* [Déployer ASP.NET web API tooAzure du Service d’applications](../app-service-api/app-service-api-dotnet-get-started.md)

## <a name="call-your-custom-api-from-logic-app-workflows"></a>Appeler votre API personnalisée à partir de flux de travail d’application logique

Après avoir défini les propriétés de la définition hello API et CORS, déclencheurs et les actions de votre API personnalisée doivent être accessible pour vous tooinclude dans votre workflow d’application logique. 

*  tooview hello des sites Web ayant des URL de Swagger, vous pouvez parcourir vos sites Web d’abonnement Bonjour logique de concepteur d’applications.

*  tooview les actions disponibles et les entrées en pointant sur un document Swagger, utilisez hello [HTTP + Swagger action](../connectors/connectors-native-http-swagger.md).

*  toocall toute API, y compris les API qui n’ont ou exposer un document Swagger, vous pouvez toujours créer une demande avec hello [action HTTP](../connectors/connectors-native-http.md).

## <a name="authenticate-calls-tooyour-custom-api"></a>Authentifier les API d’appels tooyour personnalisée

Vous pouvez sécuriser les appels tooyour API personnalisée des façons suivantes :

* [Aucune modification de code](#no-code): protéger votre API avec [Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) via hello portail Azure, par conséquent, vous n’avez tooupdate votre code ou redéployer votre API.

  > [!NOTE]
  > Par défaut, d’authentification Azure AD hello que vous activez dans hello portail Azure ne fournit pas d’autorisations affinées. Par exemple, cette authentification verrouille votre toojust API un client spécifique, pas tooa utilisateur ou application. 

* [Mise à jour du code de votre API](#update-code) : protégez votre API en appliquant [l’authentification par certificat](#certificate), [l’authentification de base](#basic) ou [l’authentification Azure AD](#azure-ad-code) par le biais du code.

<a name="no-code"></a>

### <a name="authenticate-calls-tooyour-api-without-changing-code"></a>Authentifier les appels tooyour API sans modifier le code

Voici les étapes générales de hello pour cette méthode :

1. Créez deux [identités d’application Azure Active Directory (Azure AD)](../app-service-api/app-service-api-dotnet-service-principal-auth.md) : une pour votre application logique et l’autre pour votre application web (ou application API).

2. tooauthenticate appelle tooyour API, utilisez des informations d’identification de hello (ID client et secret) pour hello [principal du service](../app-service-api/app-service-api-dotnet-service-principal-auth.md) associé hello identité Azure AD de votre application logique.

3. Inclure les ID des applications hello dans votre définition de la logique d’application.

#### <a name="part-1-create-an-azure-ad-application-identity-for-your-logic-app"></a>Partie 1 : Créer une identité d’application Azure AD pour votre application logique

Votre application logique utilise cette tooauthenticate d’identité d’application Azure AD auprès d’Azure AD. Il vous suffit tooset cette identité une fois pour votre annuaire. Par exemple, vous pouvez choisir toouse hello même identité pour toutes vos applications logique, même si vous pouvez créer des identités uniques pour chaque application logique. Vous pouvez configurer ces identités Bonjour portail Azure, [portail Azure classic](#app-identity-logic-classic), ou utilisez [PowerShell](#powershell).

**Créer l’identité de l’application hello pour votre application logique Bonjour portail Azure**

1. Bonjour [portail Azure](https://portal.azure.com "https://portal.azure.com"), choisissez **Azure Active Directory**. 

2. Confirmez que vous êtes dans hello même répertoire que votre application web ou d’une application API.

   > [!TIP]
   > répertoires de tooswitch, cliquez sur votre profil et sélectionnez un autre répertoire. Vous pouvez également sélectionner **Présentation** > **Changer de répertoire**.

3. Dans le menu du répertoire hello, sous **gérer**, choisissez **inscriptions d’application** > **nouvelle inscription de l’application**.

   > [!TIP]
   > Par défaut, liste des enregistrements de l’application hello affiche toutes les inscriptions d’application dans votre annuaire. Sélectionnez des seules votre application les inscriptions, zone de recherche suivant toohello, tooview **mes applications**. 

   ![Créer une inscription d’application](./media/logic-apps-custom-hosted-api/new-app-registration-azure-portal.png)

4. Donnez un nom à votre identité de l’application, laissez **type d’Application** défini trop**application Web / API**, fournir une valeur unique chaîne mise en forme en tant que domaine pour **URL de connexion**, puis choisissez  **Créer**.

   ![Indication d’un nom et d’une URL de connexion pour l’identité de l’application](./media/logic-apps-custom-hosted-api/logic-app-identity-azure-portal.png)

   identité d’application Hello que vous avez créé pour votre application logique maintenant s’affiche dans la liste des enregistrements de l’application hello.

   ![Identité d’application pour votre application logique](./media/logic-apps-custom-hosted-api/logic-app-identity-created.png)

5. Dans la liste des enregistrements de l’application hello, sélectionnez votre nouvelle identité de l’application. Copiez et enregistrez hello **ID d’Application** toouse comme hello « ID de client » pour votre application de la logique dans la partie 3.

   ![Copie et enregistrement de l’ID de l’application pour l’application logique](./media/logic-apps-custom-hosted-api/logic-app-application-id.png)

6. Si vos paramètres d’identité d’application ne sont pas visibles, choisissez **Paramètres** ou **Tous les paramètres**.

7. Sous **Accès d’API**, choisissez **Clés**. Sous **Description**, indiquez le nom de votre clé. Sous **Date d’expiration**, sélectionnez la durée de votre clé.

   clé Hello que vous créez joue le rôle de l’identité d’application hello « secret » ou mot de passe pour votre application logique.

   ![Création d’une clé pour l’identité de l’application logique](./media/logic-apps-custom-hosted-api/create-logic-app-identity-key-secret-password.png)

8. Dans la barre d’outils de hello, choisissez **enregistrer**. Votre clé apparaît maintenant sous **Valeur**. 
**Assurez-vous que toocopy et enregistrer votre clé de** pour une utilisation ultérieure, car la clé de hello est masqué lorsque vous laissez les lames clé hello.

   Lorsque vous configurez votre application de la logique dans la partie 3, vous spécifiez cette clé comme hello « secret » ou le mot de passe.

   ![Copie et enregistrement de la clé pour une utilisation ultérieure](./media/logic-apps-custom-hosted-api/logic-app-copy-key-secret-password.png)

<a name="app-identity-logic-classic"></a>

**Créer l’identité de l’application hello pour votre application logique Bonjour portail Azure classic**

1. Dans les hello portail Azure classic, choisissez [ **Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).

2. Sélectionnez hello même répertoire que vous utilisez pour votre application web ou d’une application API.

3. Sur hello **Applications** , onglet choisir **ajouter** bas hello de page de hello.

4. Donnez un nom à votre identité d’application, puis cliquez sur **Suivant** (flèche droite).

5. Sous **Propriétés de l’application**, indiquez une chaîne unique sous forme de domaine sous **URL de connexion** et **URI ID d’application**, puis choisissez **Terminer** (coche).

6. Sur hello **configurer** onglet, copiez et enregistrez hello **ID Client** pour votre toouse d’application logique dans la partie 3.

7. Sous **clés**, ouvrez hello **sélectionner une durée** liste. Sélectionnez la durée de votre clé.

   clé Hello que vous créez joue le rôle de l’identité d’application hello « secret » ou mot de passe pour votre application logique.

8. Au bas de hello de page de hello, choisissez **enregistrer**. Vous pouvez avoir toowait quelques secondes.

9. Sous **clés**, assurez-vous que toocopy et enregistrer la clé hello qui apparaît à présent. 

   Lorsque vous configurez votre application de la logique dans la partie 3, vous spécifiez cette clé comme hello « secret » ou le mot de passe.

Pour plus d’informations, découvrez comment trop [configurer votre connexion de Service d’applications application toouse Azure Active Directory](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).

<a name="powershell"></a>

**Créer l’identité de l’application hello pour votre application logique dans PowerShell**

Vous pouvez effectuer cette tâche par le biais d’Azure Resource Manager avec PowerShell. Dans PowerShell, exécutez ces commandes :

1. `Switch-AzureMode AzureResourceManager`

2. `Add-AzureAccount`

3. `New-AzureADApplication -DisplayName "MyLogicAppID" -HomePage "http://mydomain.tld" -IdentifierUris "http://mydomain.tld" -Password "identity-password"`

4. Assurez-vous que toocopy hello **ID client** hello de (GUID de votre client Azure AD), **ID de l’Application**et le mot de passe hello que vous avez utilisé.

Pour plus d’informations, découvrez comment trop [créer un principal de service avec PowerShell tooaccess ressources](../azure-resource-manager/resource-group-authenticate-service-principal.md).

#### <a name="part-2-create-an-azure-ad-application-identity-for-your-web-app-or-api-app"></a>Partie 2 : Créer une identité d’application Azure AD pour votre application web ou votre application API

Si votre application web ou une application API est déjà déployée, vous pouvez activer l’authentification et créer l’identité de l’application hello Bonjour portail Azure. Sinon, vous pouvez [activer l’authentification lorsque vous effectuez un déploiement avec un modèle Azure Resource Manager](#authen-deploy). 

**Créer l’identité de l’application hello et activer l’authentification Bonjour portail Azure pour les applications déployées**

1. Bonjour [portail Azure](https://portal.azure.com "https://portal.azure.com"), recherchez et sélectionnez votre application web ou une application API. 

2. Sous **Paramètres**, choisissez **Authentification/Autorisation**. Sous **Authentification App Service**, activez **l’authentification**. Sous **Fournisseurs d’authentification**, sélectionnez **Azure Active Directory**.

   ![Activer l’authentification](./media/logic-apps-custom-hosted-api/custom-web-api-app-authentication.png)

3. À présent, créez une identité d’application pour votre application web ou votre application API comme indiqué ici. Sur hello **paramètres Azure Active Directory** panneau, définissez **mode de gestion** trop**Express**. Choisissez **Créer une application AD**. Donnez un nom à votre identité d’application, puis cliquez sur **OK**. 

   ![Créer une identité d’application pour votre application web ou votre application API](./media/logic-apps-custom-hosted-api/custom-api-application-identity.png)

4. Sur hello **l’authentification / panneau d’autorisation**, choisissez **enregistrer**.

Vous devez maintenant trouver l’ID de client hello et ID de locataire pour l’identité d’application hello qui est associé à votre application web ou d’une application API. Vous utiliserez ces ID dans la partie 3. Donc continuer avec ces étapes pour hello portail Azure ou [portail Azure classic](#find-id-classic).

**Rechercher l’ID de client de l’identité de l’application et l’ID de locataire pour votre application web ou d’une application API Bonjour portail Azure**

1. Sous **Fournisseurs d’authentification**, sélectionnez **Azure Active Directory**. 

   ![Sélectionner « Azure Active Directory »](./media/logic-apps-custom-hosted-api/custom-api-app-identity-client-id-tenant-id.png)

2. Sur hello **paramètres Azure Active Directory** panneau, définissez **mode de gestion** trop**avancé**.

3. Hello de copie **ID Client**et enregistrez ce GUID pour une utilisation dans la partie 3.

   > [!TIP] 
   > Si **ID Client** et **Url de l’émetteur** ne s’affichent, essayez d’actualiser hello portail Azure, et répétez l’étape 1.

4. Sous **Url de l’émetteur**, copiez et enregistrez simplement hello GUID pour la partie 3. Vous pouvez également utiliser ce GUID dans le modèle de déploiement de votre application web ou de votre application API si nécessaire.

   Ce GUID est celui de votre locataire spécifique (« ID de locataire ») et doit apparaître dans cette URL :`https://sts.windows.net/{GUID}`

5. Sans enregistrer vos modifications, fermez hello **paramètres Azure Active Directory** panneau.

<a name="find-id-classic"></a>

**Rechercher l’ID de client de l’identité de l’application et l’ID de locataire pour votre application web ou d’une application API Bonjour portail Azure classic**

1. Dans les hello portail Azure classic, choisissez [ **Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).

2.  Sélectionnez le répertoire hello que vous utilisez pour votre application web ou d’une application API.

3. Bonjour **recherche** zone, recherchez et sélectionnez l’identité de l’application hello pour votre application web ou d’une application API.

4. Sur hello **configurer** hello de copie, onglet **ID Client**et enregistrez ce GUID pour une utilisation dans la partie 3.

5. Une fois que vous obtenez l’ID de client hello, bas hello hello **configurer** , onglet choisir **afficher les points de terminaison**.

6. Copier l’URL de hello pour **Document de métadonnées de fédération**et de parcourir les URL toothat.

7. Dans le document de métadonnées hello qui s’ouvre, trouver la racine de hello **EntityDescriptor ID** élément, ce qui a un **entityID** attribut sous cette forme :`https://sts.windows.net/{GUID}` 

      Hello GUID dans cet attribut est le GUID de votre locataire spécifique (ID client).

8. Copier l’ID de client hello et enregistrer cet ID pour une utilisation dans la partie 3 et également toouse dans votre application web ou un modèle de déploiement de l’application API, le cas échéant.

Pour plus d’informations, consultez les rubriques suivantes :

* [Authentification utilisateur pour les applications API dans Azure App Service](../app-service-api/app-service-api-dotnet-user-principal-auth.md)
* [Authentification et autorisation dans Azure App Service](../app-service/app-service-authentication-overview.md)

<a name="authen-deploy"></a>

**Activer l’authentification lorsque vous effectuez un déploiement avec un modèle Azure Resource Manager**

Vous devez toujours créer une identité d’application Azure AD de votre application web ou d’une application API qui diffère d’identité d’application hello pour votre application logique. identité de l’application hello toocreate, hello suivez précédentes étapes dans la partie 2 pour hello portail Azure. Vous pouvez également suivre les étapes de hello dans la partie 1 et rendre toouse que votre application web ou l’application API réel `https://{URL}` pour **URL de connexion** et **URI ID d’application**. À partir de ces étapes, vous avez toosave client hello ID et l’ID de client pour une utilisation dans le modèle de déploiement de votre application, ainsi que pour la partie 3.

> [!NOTE]
> Lorsque vous créez d’identité de l’application hello Azure AD de votre application web ou d’une application API, vous devez utiliser hello portail Azure ou portail Azure classic, plutôt que PowerShell. applet de commande PowerShell Hello ne configurer les autorisations de hello requis toosign des utilisateurs dans un site Web.

Une fois que vous obtenez l’ID de client hello et l’ID de client, inclure ces ID comme un subresource de votre application web ou d’une application API dans votre modèle de déploiement :

   ```
   "resources": [
       {
           "apiVersion": "2015-08-01",
           "name": "web",
           "type": "config",
           "dependsOn": ["[concat('Microsoft.Web/sites/','parameters('webAppName'))]"],
           "properties": {
               "siteAuthEnabled": true,
               "siteAuthSettings": {
                 "clientId": "{client-ID}",
                 "issuer": "https://sts.windows.net/{tenant-ID}/",
               }
           }
       }
   ]
   ```

tooautomatically déployer une application web vide et une application logique avec l’authentification Azure Active Directory, [afficher hello complète le modèle ici](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json), ou cliquez sur **déployer tooAzure** ici :

[![Déployer tooAzure](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)

#### <a name="part-3-populate-hello-authorization-section-in-your-logic-app"></a>Partie 3 : Remplir la section d’autorisation hello dans votre logique d’application

modèle précédent de Hello possède déjà cette section d’autorisation configurée, mais si vous créez directement hello logique application, vous devez inclure la section complète d’autorisation de hello.

Ouvrez votre définition de la logique d’application dans la vue code, accédez toohello **HTTP** section Actions, rechercher hello **autorisation** section et ajoutez cette ligne :

`{"tenant": "{tenant-ID}", "audience": "{client-ID-from-Part-2-web-app-or-API app}", "clientId": "{client-ID-from-Part-1-logic-app}", "secret": "{key-from-Part-1-logic-app}", "type": "ActiveDirectoryOAuth" }`

| Élément | Description |
| ------- | ----------- |
| locataire |Hello GUID pour le client de hello Azure AD |
| audience |Obligatoire. Hello GUID pour la ressource cible de hello que vous souhaitez tooaccess - hello des ID de client à partir de l’identité de l’application hello pour votre application web ou d’une application API |
| clientId |Hello GUID pour le client hello qui demandent l’accès - hello des ID de client à partir de l’identité de l’application hello pour votre application logique |
| secret |Obligatoire. clé de Hello ou un mot de passe à partir de l’identité de l’application hello pour client hello qui demande le jeton d’accès hello |
| type |type d’authentification Hello. Pour l’authentification ActiveDirectoryOAuth, valeur de hello est `ActiveDirectoryOAuth`. |

Par exemple :

```
{
   ...
   "actions": {
      "some-action": {
         "conditions": [],
         "inputs": {
            "method": "post",
            "uri": "https://your-api-azurewebsites.net/api/your-method",
            "authentication": {
               "tenant": "tenant-ID",
               "audience": "client-ID-from-azure-ad-app-for-web-app-or-api-app",
               "clientId": "client-ID-from-azure-ad-app-for-logic-app",
               "secret": "key-from-azure-ad-app-for-logic-app",
               "type": "ActiveDirectoryOAuth"
            }
         },
      }
   }
}
```

<a name="update-code"></a>

### <a name="secure-api-calls-through-code"></a>Sécuriser les appels à l’API avec le code

<a name="certificate"></a>

#### <a name="certificate-authentication"></a>Authentification par certificat

toovalidate hello les demandes entrantes à partir de votre application web de logique application tooyour ou API, vous pouvez utiliser des certificats clients. tooset votre code, en savoir plus [comment l’authentification mutuelle tooconfigure TLS](../app-service-web/app-service-web-configure-tls-mutual-auth.md).

Bonjour **autorisation** section, ajoutez cette ligne : 

`{"type": "clientcertificate", "password": "password", "pfx": "long-pfx-key"}`

| Élément | Description |
| ------- | ----------- |
| type |Obligatoire. type d’authentification Hello. Pour les certificats clients SSL, la valeur de hello doit être `ClientCertificate`. |
| password |Obligatoire. mot de passe Hello pour accéder au certificat de client hello (fichier PFX) |
| pfx |Obligatoire. Contenu de codée en Base64 du certificat de client hello (fichier PFX) |

<a name="basic"></a>

#### <a name="basic-authentication"></a>Authentification de base

toovalidate les demandes entrantes à partir de votre application web de logique application tooyour ou API, vous pouvez utiliser l’authentification de base, telles qu’un nom d’utilisateur et le mot de passe. L’authentification de base est un modèle commun, et vous pouvez utiliser cette authentification dans n’importe quel toobuild langage utilisé votre application web ou une application API.

Bonjour **autorisation** section, ajoutez cette ligne :

`{"type": "basic", "username": "username", "password": "password"}`.

| Élément | Description |
| --- | --- |
| type |Obligatoire. type d’authentification Hello. L’authentification de base, la valeur de hello doit être `Basic`. |
| username |Obligatoire. nom d’utilisateur Hello pour l’authentification |
| password |Obligatoire. mot de passe Hello pour l’authentification |

<a name="azure-ad-code"></a>

#### <a name="azure-active-directory-authentication-through-code"></a>Authentification Azure Active Directory avec le code

Par défaut, d’authentification Azure AD hello que vous activez dans hello portail Azure ne fournit pas d’autorisations affinées. Par exemple, cette authentification verrouille votre toojust API un client spécifique, pas tooa utilisateur ou application. 

application de logique tooyour toorestrict API accès via le code, extrayez en-tête hello qui comporte hello un jeton web JSON (JWT). Vérifier l’identité de l’appelant hello et rejeter les demandes qui ne correspondent pas.

Aller plus loin, tooimplement cette authentification entièrement dans votre propre code et pas l’utilisation hello portail Azure, découvrez comment trop [s’authentifier auprès d’Active Directory locale dans votre application Azure](../app-service-web/web-sites-authentication-authorization.md).

toocreate une identité pour votre application de la logique d’application et utiliser ce toocall identité votre API, vous devez suivre les étapes précédentes hello.

## <a name="next-steps"></a>Étapes suivantes

* [Vérifier les performances de l’application logique avec des alertes et des journaux de diagnostic](logic-apps-monitor-your-logic-apps.md)