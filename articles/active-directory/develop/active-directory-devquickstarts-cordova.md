---
title: aaaAzure AD Cordova prise en main | Documents Microsoft
description: "Comment toobuild une application Cordova s’intègre à Azure AD pour la connexion et appelle les API de protégé par AD Azure à l’aide d’OAuth."
services: active-directory
documentationcenter: 
author: vibronet
manager: mbaldwin
editor: 
ms.assetid: b1a8d7bd-7ad6-44d5-8ccb-5255bb623345
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: vittorib
ms.custom: aaddev
ms.openlocfilehash: 573ed638c2180c5231648bcb8c49ceb6f53296f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-an-apache-cordova-app"></a>Intégration d’Azure AD avec une application Apache Cordova
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Vous pouvez utiliser les applications Apache Cordova toodevelop HTML5/JavaScript pouvant s’exécuter sur des appareils mobiles en tant qu’applications natives à part entière. Avec Azure Active Directory (Azure AD), vous pouvez ajouter les applications Cordova tooyour Professionnel authentification fonctionnalités.

Un plug-in Cordova encapsule des kits de développement logiciels (SDK) natifs Azure AD sur iOS, Android, Windows Store et Windows Phone. À l’aide de plug-in, vous pouvez améliorer votre application toosupport connectez-vous avec les comptes de vos utilisateurs Active Directory Windows Server, obtenir accès tooOffice 365 ainsi que des API Azure et même aider à protéger les appels tooyour propre personnalisé API web.

Dans ce didacticiel, nous allons utiliser hello Apache Cordova plug-in pour Active Directory Authentication Library (ADAL) tooimprove une application simple en ajoutant hello suivant de fonctionnalités :

* Avec quelques lignes de code seulement, authentifier un utilisateur et obtenir un jeton.
* Utilisez ce tooquery de l’API Graph hello jeton tooinvoke ce répertoire et afficher les résultats de hello.  
* Utiliser l’authentification toominimize cache de jeton ADAL hello demande utilisateur de hello.

toomake ces améliorations, vous devez :

1. inscrivez une application auprès d’Azure AD ;
2. Ajoutez des jetons de code tooyour application toorequest.
3. Ajouter un jeton hello toouse du code pour l’interrogation hello API Graph et afficher les résultats.
4. Créer un projet de déploiement Cordova hello avec toutes les plateformes hello vous souhaitez tootarget, ajouter hello plug-in Cordova ADAL et tester des solutions de hello dans les émulateurs.

## <a name="prerequisites"></a>Composants requis
toocomplete ce didacticiel, vous devez :

* Un client Azure AD où vous avez un compte disposant de droits de développement d’application.
* Un environnement de développement qui a configuré toouse Apache Cordova.  

Si vous les avez déjà configuré, passez directement toostep 1.

Si vous n’avez pas un locataire Azure AD, utilisez hello [obtenir des instructions sur la façon de tooget un](active-directory-howto-tenant.md).

Si vous n’avez pas Apache Cordova sur votre ordinateur, installez des éléments suivants de hello :

* [Git](http://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* [Node.JS](https://nodejs.org/download/)
* [Cordova CLI](https://cordova.apache.org/) (peut être installé facilement via le Gestionnaire de package NPM : `npm install -g cordova`)

Hello précédentes installations doit fonctionner sur hello PC et sur hello Mac.

Chaque plateforme cible présente une configuration requise différente :

* toobuild et exécuter une application pour Tablet PC/PC Windows ou Windows Phone :
  * Installez [Visual Studio 2013 pour Windows Update 2 ou version ultérieure](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express ou autre version) ou [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).

* toobuild et exécuter une application pour iOS :

  * Installez Xcode 6.x ou version ultérieure. Téléchargez-le à partir de hello [site Apple Developer](http://developer.apple.com/downloads) ou hello [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).
  * Installez [ios-sim](https://www.npmjs.org/package/ios-sim). Vous pouvez l’utiliser des applications iOS toostart dans iOS Simulator depuis la ligne de commande hello. (Vous pouvez l’installer facilement via hello Terminal Server : `npm install -g ios-sim`.)
* toobuild et exécuter une application pour Android :

  * Installez le [Kit de développement Java (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) ou ultérieur. Assurez-vous que `JAVA_HOME` (variable d’environnement) est correctement définie selon le chemin d’installation de JDK toohello (par exemple, C:\Program Files\Java\jdk1.7.0_75).
  * Installer [du SDK Android](http://developer.android.com/sdk/installing/index.html?pkg=tools) et ajoutez hello `<android-sdk-location>\tools` emplacement (par exemple, C:\tools\Android\android-sdk\tools) tooyour `PATH` variable d’environnement.
  * Ouvrez le Gestionnaire de SDK Android (via hello Terminal Server, par exemple : `android`) et l’installer :
    * *Android 5.0.1 (API 21)*
    * *Android SDK Build Tools* version 19.1.0 ou ultérieure
    * *Android Support Repository* (modules complémentaires)

  Hello du SDK Android ne fournit pas une instance d’émulateur par défaut. En exécutant `android avd` de hello Terminal Server, puis en sélectionnant **créer**, si vous souhaitez toorun hello des applications Android sur un émulateur. Nous recommandons un niveau d’API de 19 ou plus. Pour plus d’informations sur les options de création et d’émulateur Android hello, consultez [Gestionnaire AVD](http://developer.android.com/tools/help/avd-manager.html) sur le site de Android hello.

## <a name="step-1-register-an-application-with-azure-ad"></a>Étape 1 : Inscrire une application auprès d’Azure AD
Cette étape est facultative. Ce didacticiel fournit des valeurs préconfigurés, que vous pouvez utiliser toosee hello exemple en action sans effectuer toute mise en service dans votre propre locataire. Toutefois, nous vous recommandons de réaliser cette étape et vous familiariser avec les processus hello, car elle sera nécessaire lorsque vous créez vos propres applications.

Azure AD émet tooonly jetons connu des applications. Avant de pouvoir utiliser Azure AD à partir de votre application, vous devez toocreate une entrée pour celle-ci dans votre client. tooregister une nouvelle application dans votre client :

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Sur la barre supérieure de hello, cliquez sur votre compte. Bonjour **répertoire** , choisissez locataire hello AD Azure où vous souhaitez tooregister votre application.
3. Cliquez sur **plus Services** dans hello du volet gauche, puis sélectionnez **Azure Active Directory**.
4. Cliquez sur **Inscriptions des applications**, puis sélectionnez **Ajouter**.
5. Suivez les invites hello et créer un **Application cliente Native**. (Bien que les applications Cordova soient basées sur le langage HTML, nous créons ici une application cliente native. Hello **Application cliente Native** doit être activée ou l’application hello ne fonctionne pas.)
  * **Nom** décrit toousers de votre application.
  * **URI de redirection** est hello URI qui a utilisé tooreturn jetons tooyour application. Entrez **http://MyDirectorySearcherApp**.

Une fois que vous avez terminé l’inscription, Azure AD assigne une application de tooyour ID unique d’application. Vous aurez besoin de cette valeur dans les sections suivantes hello. Vous pouvez le trouver sur l’onglet de l’application hello Hello l’application nouvellement créée.

toorun `DirSearchClient Sample`, accorder hello nouvellement créé application autorisation tooquery hello Azure AD Graph API :

1. À partir de hello **paramètres** page, sélectionnez **autorisations requises**, puis sélectionnez **ajouter**.  
2. Pour hello application Azure Active Directory, sélectionnez **Microsoft Graph** comme hello API et ajouter hello **répertoire de hello Access en tant qu’utilisateur connecté hello** autorisation sous **délégués Autorisations**.  Cela permet à votre hello de tooquery d’application API Graph pour les utilisateurs.

## <a name="step-2-clone-hello-sample-app-repository"></a>Étape 2 : Cloner le référentiel d’application exemple hello
À partir de votre environnement ou de la ligne de commande, tapez hello de commande suivante :

    git clone -b skeleton https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova.git

## <a name="step-3-create-hello-cordova-app"></a>Étape 3 : Créer l’application de Cordova hello
Il existe plusieurs façons toocreate Cordova applications. Dans ce didacticiel, nous allons utiliser l’interface de ligne de commande de Cordova hello (CLI).

1. À partir de votre environnement ou de la ligne de commande, tapez hello de commande suivante :

        cordova create DirSearchClient

   Cette commande crée la structure de dossiers hello et génération de modèles automatique pour le projet de Cordova hello.

2. Déplacer le dossier DirSearchClient toohello :

        cd .\DirSearchClient

3. Copier le contenu de hello du projet de démarrage hello dans le sous-dossier de www hello à l’aide d’un gestionnaire de fichiers ou le hello commande dans votre interpréteur de commandes suivante :

  * Windows : `xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`
  * Mac : `cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`

4. Ajouter un plug-in de la liste d’autorisation hello. Cela est nécessaire pour l’appel d’API Graph de hello.

        cordova plugin add cordova-plugin-whitelist

5. Ajoutez toutes les plateformes hello que vous souhaitez toosupport. toohave un exemple fonctionnel, vous devez tooexecute au moins l’un de hello suivant les commandes. Notez que vous ne seront pas être iOS en mesure de tooemulate sur Windows ou émuler Windows sur un Mac.

        cordova platform add android
        cordova platform add ios
        cordova platform add windows

6. Ajoutez hello ADAL pour le projet de tooyour plug-in Cordova :

        cordova plugin add cordova-plugin-ms-adal

## <a name="step-4-add-code-tooauthenticate-users-and-obtain-tokens-from-azure-ad"></a>Étape 4 : Ajouter des utilisateurs tooauthenticate de code et obtenir des jetons d’Azure AD
application Hello que vous développez dans ce didacticiel fournit une fonctionnalité de recherche de répertoire simple. Hello utilisateur peut taper alias hello de n’importe quel utilisateur dans le répertoire de hello et visualiser certains attributs de base. projet de démarrage Hello contient la définition hello d’interface utilisateur de base de hello de l’application hello (dans www/index.html) et la structure hello qui relie des événements d’application de base, les liaisons d’interface utilisateur, cycles et les résultats de logique d’affichage (dans www/js/index.js). Hello seule tâche pour vous est tooadd hello logique qui implémente les tâches d’identité.

Hello première chose toodo dans votre code est de présenter les valeurs de protocole hello Azure AD utilise pour identifier votre application et hello ressources que vous ciblez. Ces valeurs seront ultérieurement sur les demandes de jeton de hello tooconstruct utilisé. Insérez hello suivant extrait haut hello du fichier de index.js hello :

```javascript
var authority = "https://login.microsoftonline.com/common",
    redirectUri = "http://MyDirectorySearcherApp",
    resourceUri = "https://graph.windows.net",
    clientId = "a5d92493-ae5a-4a9f-bcbf-9f1d354067d3",
    graphApiVersion = "2013-11-08";
```

Hello `redirectUri` et `clientId` valeurs doivent correspondre les valeurs hello qui décrivent votre application dans Azure AD. Vous pouvez trouver ceux de hello **configurer** onglet hello portail Azure, comme décrit à l’étape 1, plus haut dans ce didacticiel.

> [!NOTE]
> Si vous avez choisi pour ne pas l’inscription d’une nouvelle application dans votre propre client, vous pouvez coller simplement les valeurs hello préconfiguré en l’état. Vous pouvez ensuite voir en cours d’exécution exemple hello, bien que vous devez toujours créer votre propre entrée pour vos applications sont destinées à la production.

Ensuite, ajoutez le code de demande de jeton hello. Insérer hello suivant extrait entre hello `search` et `renderData` définitions :

```javascript
    // Shows hello user authentication dialog box if required
    authenticate: function (authCompletedCallback) {

        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
            // Attempt tooauthorize hello user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers hello authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed tooauthenticate: " + err);
                });
            });
        });

    },
```
Examinons cette fonction en la décomposant en deux parties principales.
Cet exemple est conçu toowork avec n’importe quel client, comme toobeing opposé liée tooa d'entre eux. Il utilise hello « / common » point de terminaison, qui permet de n’importe quel compte hello utilisateur tooenter au moment de l’authentification et dirige les client de toohello hello demande à laquelle il appartient.

La première partie de la méthode hello inspecte hello cache ADAL toosee si un jeton est déjà stocké. Dans ce cas, méthode hello utilise les locataires hello d'où provenance le jeton de hello pour la réinitialisation de la bibliothèque ADAL. Cela est nécessaire tooavoid invites supplémentaires, car hello utilisation de « / courantes » toujours demandant hello utilisateur tooenter un nouveau compte.

```javascript
        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
```
Hello deuxième partie de méthode hello effectue la demande de jeton correcte hello. Hello `acquireTokenSilentAsync` méthode demande tooreturn ADAL un jeton hello spécifié ressource sans affichage de n’importe quel UX. Cela peut se produire si le cache de hello a déjà un jeton d’accès stocké, ou si un jeton d’actualisation peut être utilisé tooget un nouveau jeton d’accès sans affichage d’une invite. Si cette tentative échoue, nous revenir `acquireTokenAsync`--ce qui invite visiblement hello utilisateur tooauthenticate.

```javascript
            // Attempt tooauthorize hello user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers hello authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed tooauthenticate: " + err);
                });
            });
```
Maintenant que nous avons le jeton de hello, nous pouvons enfin appeler hello API Graph et d’effectuer la requête de recherche hello que nous voulons. Insérer hello suivant extrait de code ci-dessous hello `authenticate` définition :

```javascript
// Makes an API call tooreceive hello user list
    requestData: function (authResult, searchText) {
        var req = new XMLHttpRequest();
        var url = resourceUri + "/" + authResult.tenantId + "/users?api-version=" + graphApiVersion;
        url = searchText ? url + "&$filter=mailNickname eq '" + searchText + "'" : url + "&$top=10";

        req.open("GET", url, true);
        req.setRequestHeader('Authorization', 'Bearer ' + authResult.accessToken);

        req.onload = function(e) {
            if (e.target.status >= 200 && e.target.status < 300) {
                app.renderData(JSON.parse(e.target.response));
                return;
            }
            app.error('Data request failed: ' + e.target.response);
        };
        req.onerror = function(e) {
            app.error('Data request failed: ' + e.error);
        }

        req.send();
    },

```
fichiers de point de départ Hello fourni une expérience utilisateur simple pour l’entrée d’un alias de l’utilisateur dans une zone de texte. Cette méthode utilise la valeur tooconstruct une requête, combiner avec le jeton d’accès hello, envoyer tooMicrosoft graphique et analyser les résultats hello. Hello `renderData` (méthode), déjà présente dans le fichier de point de départ de hello, prend en charge de visualisation des résultats de hello.

## <a name="step-5-run-hello-app"></a>Étape 5 : Exécuter l’application hello
Votre application est maintenant prête toorun. Il fonctionne est simple : au démarrage de l’application hello, entrez l’alias hello de hello utilisateur toolook des, puis cliquez sur le bouton de hello. Vous êtes invité à vous authentifier. Lors de l’authentification réussie et la recherche réussit, les attributs hello de hello recherché utilisateur sont affichés.

Les exécutions suivantes effectuera hello recherche sans affichage d’une invite, grâce présence toohello Hello précédemment acquis jeton dans le cache.

étapes de concrète Hello pour exécuter l’application hello varient selon la plateforme.

### <a name="windows-10"></a>Windows 10
   Tablette/PC : `cordova run windows --archs=x64 -- --appx=uap`

   Mobile (nécessite un tooa de périphérique connecté PC Windows 10 Mobile) :`cordova run windows --archs=arm -- --appx=uap --phone`

   > [!NOTE]
   > Au cours de hello exécutez d’abord, vous pouvez être invité toosign dans une licence de développeur. Pour plus d’informations, consultez [Obtenir une licence de développeur](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).

### <a name="windows-81-tabletpc"></a>Tablette/PC Windows 8.1
   `cordova run windows`

   > [!NOTE]
   > Au cours de hello exécutez d’abord, vous pouvez être invité toosign dans une licence de développeur. Pour plus d’informations, consultez [Obtenir une licence de développeur](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).

### <a name="windows-phone-81"></a>Windows Phone 8.1
   toorun sur un appareil connecté :`cordova run windows --device -- --phone`

   toorun sur l’émulateur par défaut de hello :`cordova emulate windows -- --phone`

   Utilisez `cordova run windows --list -- --phone` toosee toutes les cibles disponibles et `cordova run windows --target=<target_name> -- --phone` application hello de toorun sur un émulateur ou un périphérique spécifique (par exemple, `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).

### <a name="android"></a>Android
   toorun sur un appareil connecté :`cordova run android --device`

   toorun sur l’émulateur par défaut de hello :`cordova emulate android`

   Assurez-vous que vous avez créé une instance de l’émulateur à l’aide du gestionnaire AVD, comme décrit précédemment dans la section « Conditions préalables » de hello.

   Utilisez `cordova run android --list` toosee toutes les cibles disponibles et `cordova run android --target=<target_name>` application hello de toorun sur un émulateur ou un périphérique spécifique (par exemple, `cordova run android --target="Nexus4_emulator"`).

### <a name="ios"></a>iOS
   toorun sur un appareil connecté :`cordova run ios --device`

   toorun sur l’émulateur par défaut de hello :`cordova emulate ios`

   > [!NOTE]
   > Assurez-vous que vous avez hello `ios-sim` toorun package installé sur l’émulateur de hello. Pour plus d’informations, consultez hello « conditions préalables » section.

    Use `cordova run ios --list` toosee all available targets and `cordova run ios --target=<target_name>` toorun hello application on specific device or emulator (for example, `cordova run android --target="iPhone-6"`).

    Use `cordova run --help` toosee additional build and run options.

## <a name="next-steps"></a>Étapes suivantes
Pour référence, l’exemple hello terminée (sans les valeurs de configuration) est disponible dans [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).

Vous pouvez maintenant les scénarios de transfert sur toomore avancé (et plus intéressantes). Vous souhaiterez peut-être tootry : [sécuriser une API Web de Node.js avec Azure AD](active-directory-devquickstarts-webapi-nodejs.md).

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
