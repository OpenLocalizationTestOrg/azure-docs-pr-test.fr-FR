---
title: aaaAzure AD Android prise en main | Documents Microsoft
description: "Comment toobuild une application Android qui s’intègre à Azure AD pour se connecter et d’appels Azure AD protégé API à l’aide d’OAuth."
services: active-directory
documentationcenter: android
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: da1ee39f-89d3-4d36-96f1-4eabbc662343
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 01/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 1aedc8ff60874b405a182a4ccbfb2c8b4d9d3704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-an-android-app"></a>Intégration d’Azure AD dans une application Android
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> Un aperçu de hello de notre nouveau [portail des développeurs](https://identity.microsoft.com/Docs/Android), ce qui vous aidera à obtenir en cours d’exécution auprès d’Azure AD en quelques minutes. portail des développeurs Hello vous guidera tout au long des processus hello l’inscription d’une application et l’intégration d’Azure AD dans votre code. Une fois que vous aurez terminé, vous disposerez d’une application simple capable d’authentifier les utilisateurs dans votre client et d’un serveur principal qui peut accepter les jetons et effectuer la validation.
>
>

Si vous développez une application de bureau, Azure Active Directory (Azure AD) rend très simple pour vous tooauthenticate vos utilisateurs à l’aide de leurs comptes d’Active Directory local. Il permet également de votre application toosecurely consommer n’importe quel web API protégée par Azure AD, comme la hello API Office 365 ou hello API Azure.

Pour les clients Android qui ont besoin de ressources de tooaccess protégé, Azure AD fournit hello Active Directory Authentication Library (ADAL). Hello seul but de la bibliothèque ADAL est toomake plus facile pour les jetons d’accès tooget votre application. toodemonstrate facilement il s’agit, nous allons créer une application Android liste de tâches :

* Obtient les jetons pour l’appel d’une API de la liste des tâches à l’aide de hello d’accès [protocole d’authentification OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* obtention de la liste des tâches d’un utilisateur ;
* déconnexion des utilisateurs.

tooget démarré, vous devez un locataire Azure AD, dans laquelle vous pouvez créer des utilisateurs et inscrire une application. Si vous n’avez pas encore un client, [apprendre comment tooget un](active-directory-howto-tenant.md).

## <a name="step-1-download-and-run-hello-nodejs-rest-api-todo-sample-server"></a>Étape 1 : Télécharger et exécuter l’exemple de serveur hello Node.js REST API TODO
exemple de Node.js REST API TODO Hello est écrit spécifiquement toowork par rapport à notre exemple existant pour la création d’un locataire unique action REST API pour Azure AD. Il s’agit d’une condition préalable pour hello démarrage rapide.

Pour plus d’informations sur comment tooset cette installation, consultez nos exemples existants dans [Service Microsoft Azure Active Directory exemple REST API pour Node.js](active-directory-devquickstarts-webapi-nodejs.md).


## <a name="step-2-register-your-web-api-with-your-azure-ad-tenant"></a>Étape 2 : Inscription de votre API web auprès de votre client Azure AD
Active Directory prend en charge l’ajout de deux types d’application :

- API qui offrent des toousers de services Web
- Applications (en cours d’exécution sur le web de hello ou sur un appareil) qui accèdent à ceux des API web

Dans cette étape, vous êtes enregistré hello web API que vous exécutez localement pour tester cet exemple. Normalement, cette API web est un service REST offre les fonctionnalités que vous souhaitez une tooaccess de l’application. Azure AD peut contribuer à protéger n’importe quel point de terminaison.

Nous supposons que vous êtes inscrit hello API REST de tâches mentionnée précédemment. Mais cela fonctionne pour n’importe quel site web API Azure Active Directory toohelp protéger.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Sur la barre supérieure de hello, cliquez sur votre compte. Bonjour **répertoire** , choisissez locataire hello AD Azure où vous souhaitez tooregister votre application.
3. Cliquez sur **plus Services** dans hello du volet gauche, puis sélectionnez **Azure Active Directory**.
4. Cliquez sur **Inscriptions des applications**, puis sélectionnez **Ajouter**.
5. Entrez un nom convivial pour l’application hello (par exemple, **TodoListService**), sélectionnez **Application Web et/ou API Web**, puis cliquez sur **suivant**.
6. Pour l’URL de connexion hello, entrez les URL de base de hello pour exemple hello. (`https://localhost:8080` par défaut).
7. Cliquez sur **OK** l’inscription de toocomplete hello.
8. Dans hello portail Azure, atteindre la page d’application tooyour, recherchez la valeur d’ID application hello et copiez-le. Vous en aurez besoin plus tard lors de la configuration de votre application.
9. À partir de hello **paramètres** -> **propriétés** page, mettre à jour d’URI ID d’application hello - entrez `https://<your_tenant_name>/TodoListService`. Remplacez `<your_tenant_name>` par nom de hello de votre client Azure AD.

## <a name="step-3-register-hello-sample-android-native-client-application"></a>Étape 3 : Inscrire hello exemple Android Native d’application cliente
Vous devez inscrire votre application web dans cet exemple. Cela permet de toocommunicate de votre application avec hello inscrit juste API web. Azure AD refusera tooeven autoriser tooask de votre application pour la connexion, sauf si elle est inscrite. Qui est la partie de la sécurité hello du modèle de hello.

Nous supposons que vous êtes l’inscription d’application d’exemple hello mentionnée précédemment. Cependant, cette procédure fonctionne pour n’importe quelle application que vous développez.

> [!NOTE]
> Vous vous demandez peut-être pourquoi nous incorporons à la fois une application et une API web dans un seul client. Comme vous l’avez peut-être deviné, vous pouvez générer une application qui accède à une API externe inscrite dans Azure AD à partir d’un autre client. Si vous procédez ainsi, vos clients seront vous y êtes invité à utiliser toohello tooconsent hello API dans l’application hello. La bibliothèque d’authentification Active Directory pour iOS s’occupe de cette autorisation pour vous. Lors de l’exploration des fonctionnalités plus avancées, vous verrez qu’il s’agit d’une partie importante de la suite de hello hello travail tooaccess nécessaires de Microsoft APIs d’Azure et Office, ainsi que tout autre fournisseur de service. Pour l’instant, car vous avez inscrit votre API web et votre application sous hello même locataire, vous ne voyez pas les invites de consentement. C’est généralement hello cas si vous développez une application simplement pour votre propre toouse d’entreprise.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Sur la barre supérieure de hello, cliquez sur votre compte. Bonjour **répertoire** , choisissez locataire hello AD Azure où vous souhaitez tooregister votre application.
3. Cliquez sur **plus Services** dans hello du volet gauche, puis sélectionnez **Azure Active Directory**.
4. Cliquez sur **Inscriptions des applications**, puis sélectionnez **Ajouter**.
5. Entrez un nom convivial pour l’application hello (par exemple, **TodoListClient-Android**), sélectionnez **Application cliente Native**, puis cliquez sur **suivant**.
6. Pourquoi les URI de redirection, entrez `http://TodoListClient`. Cliquez sur **Terminer**.
7. À partir de la page d’application hello, recherchez la valeur d’ID application hello et copiez-la. Vous en aurez besoin plus tard lors de la configuration de votre application.
8. À partir de hello **paramètres** page, sélectionnez **autorisations requises** et sélectionnez **ajouter**.  Recherchez et sélectionnez TodoListService, ajouter hello **accès TodoListService** autorisation sous **autorisations déléguées**, puis cliquez sur **fait**.

toobuild avec Maven, vous pouvez utiliser pom.xml hello premier niveau :

1. Clonez ce référentiel dans le répertoire de votre choix :

  `$ git clone git@github.com:AzureADSamples/NativeClient-Android.git`  
2. Suivez les étapes de hello Bonjour [tooset des conditions préalables de votre environnement de Maven pour Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).
3. Configurer l’émulateur hello avec le Kit de développement logiciel 19.
4. Atteindre le dossier racine de toohello où vous avez cloné le dépôt de hello.
5. Exécutez cette commande : `mvn clean install`.
6. Modifier l’exemple de démarrage rapide de toohello hello active :`cd samples\hello`
7. Exécutez cette commande : `mvn android:deploy android:run`.

   Vous devez voir le démarrage d’application hello.
8. Entrez tootry d’informations d’identification utilisateur de test.

Les packages JAR seront soumis à côté de package de AAR hello.

## <a name="step-4-download-hello-android-adal-and-add-it-tooyour-eclipse-workspace"></a>Étape 4 : Télécharger hello Android ADAL et ajoutez-le tooyour espace de travail Eclipse
Nous avons simplifié pour vous toohave plusieurs options toouse ADAL dans votre projet Android :

* Vous pouvez utiliser tooimport de code source hello cette bibliothèque dans des application tooyour Eclipse et lien.
* Si vous utilisez Android Studio, vous pouvez utiliser hello AAR package format référence hello binaires et.

### <a name="option-1-source-zip"></a>Option 1 : code source dans un fichier ZIP
toodownload une copie du code source de hello, cliquez sur **ZIP de téléchargement** sur le côté droit de hello de page de hello. Vous pouvez également [effectuer le téléchargement à partir de GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).

### <a name="option-2-source-via-git"></a>Option 2:  code Source via Git
code de source tooget hello Hello SDK via Git, tapez :

    git clone git@github.com:AzureAD/azure-activedirectory-library-for-android.git
    cd ./azure-activedirectory-library-for-android/src

### <a name="option-3-binaries-via-gradle"></a>Option 3: fichiers binaires via Gradle
Vous pouvez obtenir les fichiers binaires de hello référentiel central de Maven hello. package de AAR Hello peut être inclus comme suit dans votre projet dans Android Studio :

```gradle
repositories {
    mavenCentral()
    flatDir {
        dirs 'libs'
    }
    maven {
        url "YourLocalMavenRepoPath\\.m2\\repository"
    }
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile('com.microsoft.aad:adal:1.1.1') {
        exclude group: 'com.android.support'
    } // Recent version is 1.1.1
}
```

### <a name="option-4-aar-via-maven"></a>Option 4: AAR via Maven
Si vous utilisez hello M2Eclipse plug-in, vous pouvez spécifier la dépendance de hello dans votre fichier pom.xml :

```xml
<dependency>
    <groupId>com.microsoft.aad</groupId>
    <artifactId>adal</artifactId>
    <version>1.1.1</version>
    <type>aar</type>
</dependency>
```


### <a name="option-5-jar-package-inside-hello-libs-folder"></a>Option 5 : Package du fichier JAR à l’intérieur du dossier de bibliothèques hello
Vous pouvez obtenir le fichier JAR hello à partir du référentiel de Maven hello et déposez-le dans hello **libs** dossier dans votre projet. Vous devez toocopy hello ressources requises tooyour projet ainsi, car les packages JAR hello ne les incluent pas.

## <a name="step-5-add-references-tooandroid-adal-tooyour-project"></a>Étape 5 : Ajouter le projet de références tooAndroid tooyour ADAL
1. Ajouter une référence de projet tooyour et spécifiez-le sous la forme d’une bibliothèque Android. Si vous n’êtes pas sûr comment toodo cela, vous pouvez obtenir plus d’informations sur hello [site Android Studio](http://developer.android.com/tools/projects/projects-eclipse.html).
2. Ajouter une dépendance de projet hello pour le débogage dans les paramètres de votre projet.
3. Mettre à jour tooinclude de fichier AndroidManifest.xml de votre projet :

        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <application
            android:allowBackup="true"
            android:debuggable="true"
            android:icon="@drawable/ic_launcher"
            android:label="@string/app_name"
            android:theme="@style/AppTheme" >

            <activity
                android:name="com.microsoft.aad.adal.AuthenticationActivity"
                android:label="@string/title_login_hello_app" >
            </activity>
            ....
        <application/>

4. Créez une instance d’AuthenticationContext pour votre activité principale. Détails de Hello de cet appel sont traitées par cette rubrique hello, mais vous pouvez obtenir un bon début en examinant hello [exemple d’Android Native Client](https://github.com/AzureADSamples/NativeClient-Android). Bonjour l’exemple suivant, SharedPreferences est cache par défaut de hello et autorité est de forme hello `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:

    `mContext = new AuthenticationContext(MainActivity.this, authority, true); // mContext is a field in your activity`

5. Copiez le code bloc toohandle hello parvenir de AuthenticationActivity une fois que l’utilisateur de hello entre des informations d’identification et qu’il reçoit un code d’autorisation :

        @Override
         protected void onActivityResult(int requestCode, int resultCode, Intent data) {
             super.onActivityResult(requestCode, resultCode, data);
             if (mContext != null) {
                mContext.onActivityResult(requestCode, resultCode, data);
             }
         }

6. tooask pour un jeton, définissez un rappel :

        private AuthenticationCallback<AuthenticationResult> callback = new AuthenticationCallback<AuthenticationResult>() {

            @Override
            public void onError(Exception exc) {
                if (exc instanceof AuthenticationException) {
                    textViewStatus.setText("Cancelled");
                    Log.d(TAG, "Cancelled");
                } else {
                    textViewStatus.setText("Authentication error:" + exc.getMessage());
                    Log.d(TAG, "Authentication error:" + exc.getMessage());
                }
            }

            @Override
            public void onSuccess(AuthenticationResult result) {
                mResult = result;

                if (result == null || result.getAccessToken() == null
                        || result.getAccessToken().isEmpty()) {
                    textViewStatus.setText("Token is empty");
                    Log.d(TAG, "Token is empty");
                } else {
                    // request is successful
                    Log.d(TAG, "Status:" + result.getStatus() + " Expired:"
                            + result.getExpiresOn().toString());
                    textViewStatus.setText(PASSED);
                }
            }
        };

7. Enfin, demandez un jeton à l’aide de ce rappel :

    `mContext.acquireToken(MainActivity.this, resource, clientId, redirect, user_loginhint, PromptBehavior.Auto, "",
                   callback);`

Voici une explication des paramètres de hello :

* *ressource* est requise et que vous essayez de tooaccess de ressources hello.
* *clientid* est obligatoire et provient d’Azure AD.
* *RedirectUri* n’est pas requis toobe fourni pour l’appel d’acquireToken hello. Vous pouvez définir ce paramètre sur le nom de votre package.
* *PromptBehavior* vous aide à tooask pour la mémoire cache tooskip hello et un cookie.
* *rappel* est appelé après que le code d’autorisation de hello est échangé pour un jeton. Ce paramètre présente un objet AuthenticationResult avec jeton d’accès, date d’expiration et informations de jeton d’ID.
* *acquireTokenSilent* est facultatif. Vous pouvez l’appeler toohandle mise en cache et l’actualisation de jeton. Il fournit également la version de synchronisation hello. Il accepte *userId* comme paramètre.

        mContext.acquireTokenSilent(resource, clientid, userId, callback );

À l’aide de cette procédure pas à pas, vous devez disposer de ce que vous devez intégrer toosuccessfully avec Azure Active Directory. Pour plus d’exemples de ce travail, visitez hello AzureADSamples / référentiel sur GitHub.

## <a name="important-information"></a>Informations importantes
### <a name="customization"></a>Personnalisation
Les ressources de votre application peuvent remplacer celles du projet de bibliothèque. Cela se produit lors de la création de votre application. Pour cette raison, vous pouvez personnaliser l’authentification activité disposition hello librement. Code de hello tookeep que des contrôles de hello que la bibliothèque ADAL utilise (WebView).

### <a name="broker"></a>Service Broker
application de portail d’entreprise Microsoft Intune Hello fournit un composant de service broker hello. compte de Hello est créé dans AccountManager. type de compte Hello est « com.microsoft.workaccount ». AccountManager autorise un seul compte d’authentification unique. Il crée un cookie d’authentification unique pour l’utilisateur de hello après avoir effectué la demande de périphérique hello pour l’une des applications de hello.

La bibliothèque ADAL utilise le compte de service broker hello si un compte d’utilisateur est créé à cet authentificateur et que vous choisissez tooskip pas il. Vous pouvez ignorer l’utilisateur du service broker hello avec :

   `AuthenticationSettings.Instance.setSkipBroker(true);`

Vous devez tooregister une RedirectUri spécial pour l’utilisation de service broker. RedirectUri est au format hello de `msauth://packagename/Base64UrlencodedSignature`. Vous pouvez obtenir votre RedirectUri pour votre application à l’aide de hello script brokerRedirectPrint.ps1 ou hello API appel mContext.getBrokerRedirectUri. signature de Hello est connexe tooyour certificats de signature.

modèle de service broker actif Hello est pour un utilisateur. AuthenticationContext fournit un utilisateur de service broker hello API méthode tooget hello.

   `String brokerAccount =  mContext.getBrokerUser(); //Broker user is returned if account is valid.`

Votre manifeste d’application doit avoir hello suivant autorisations toouse AccountManager des comptes. Pour plus d’informations, consultez hello [AccountManager plus d’informations sur le site de Android hello](http://developer.android.com/reference/android/accounts/AccountManager.html).

* GET_ACCOUNTS
* USE_CREDENTIALS
* MANAGE_ACCOUNTS

### <a name="authority-url-and-ad-fs"></a>AD FS et URL de l’autorité
Services de fédération Active Directory (AD FS) n’est pas reconnu en tant que STS, de production, afin que vous avez besoin tooturn de découverte d’instance et passez la valeur false au constructeur de classe AuthenticationContext hello.

URL d’autorité Hello a besoin d’une instance de STS et une [nom_client](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).

### <a name="querying-cache-items"></a>Interrogation des éléments de cache
ADAL fournit un cache par défaut dans SharedPreferences avec quelques fonctions simples de requête de cache. Vous pouvez obtenir de cache actuelle hello de AuthenticationContext à l’aide de :

    ITokenCacheStore cache = mContext.getCache();

Vous pouvez également fournir votre implémentation de cache, si vous souhaitez toocustomize il.

    mContext = new AuthenticationContext(MainActivity.this, authority, true, yourCache);

### <a name="prompt-behavior"></a>Comportement d’invite
ADAL fournit un comportement de toospecify l’option invite. PromptBehavior.Auto affiche hello l’interface utilisateur si le jeton d’actualisation hello n’est pas valide et les informations d’identification utilisateur sont requises. PromptBehavior.Always ignore l’utilisation du cache de hello et toujours afficher hello l’interface utilisateur.

### <a name="silent-token-request-from-cache-and-refresh"></a>Demande de jeton en mode silencieux à partir du cache et actualisation
Une demande de jeton en mode silencieux n’utilise pas de hello indépendante de l’interface utilisateur et ne nécessite pas une activité. Il retourne un jeton à partir du cache de hello s’il est disponible. Si le jeton de hello a expiré, cette méthode essaie de toorefresh il. Si le jeton d’actualisation hello est expiré ou a échoué, elle retourne AuthenticationException.

    Future<AuthenticationResult> result = mContext.acquireTokenSilent(resource, clientid, userId, callback );

Vous pouvez également effectuer un appel de synchronisation à l’aide de cette méthode. Vous pouvez définir toocallback null ou utiliser acquireTokenSilentSync.

### <a name="diagnostics"></a>Diagnostics
Il s’agit de hello principales sources d’informations pour diagnostiquer les problèmes :

* Exceptions
* Journaux
* Suivis réseau

Notez que les ID de corrélation sont diagnostics toohello central dans la bibliothèque de hello. Si vous voulez toocorrelate une ADAL demander avec d’autres opérations dans votre code, vous pouvez définir votre ID de corrélation sur la base de chaque demande. Si vous ne définissez aucun ID de corrélation, la bibliothèque ADAL génère un ID aléatoire. Tous les messages du journal et les appels réseau seront ensuite marqués avec l’ID de corrélation hello. modifications Hello générées automatiquement ID à chaque demande.

#### <a name="exceptions"></a>Exceptions
Les exceptions sont tout d’abord hello diagnostic. Nous essayons de messages d’erreur utiles tooprovide. Si vous en trouvez un qui n’est pas utile, faites-le-nous savoir en signalant un problème. Incluez des informations sur l’appareil, notamment le modèle et le numéro du Kit de développement logiciel (SDK).

#### <a name="logs"></a>Journaux
Vous pouvez configurer hello bibliothèque toogenerate des messages de journal que vous pouvez utiliser toohelp diagnostiquer les problèmes. Vous configurez la journalisation en rendant hello suivant appeler tooconfigure un rappel que la bibliothèque ADAL utilisera toohand chaque message du journal car il est généré.

    Logger.getInstance().setExternalLogger(new ILogger() {
        @Override
        public void Log(String tag, String message, String additionalMessage, LogLevel level, ADALError errorCode) {
        ...
        // You can write this toolog file depending on level or error code.
        writeToLogFile(getApplicationContext(), tag +":" + message + "-" + additionalMessage);
        }
    }

Les messages peuvent être écrits tooa fichier de journal personnalisé, comme indiqué dans hello suivant de code. Malheureusement, il n’existe aucun moyen standard d’obtenir les journaux d’un appareil. Il existe des services qui peuvent vous y aider. Vous pouvez également inventer votre propre, tels que serveur de tooa fichier hello émetteur.

    private syncronized void writeToLogFile(Context ctx, String msg) {
       File directory = ctx.getDir(ctx.getPackageName(), Context.MODE_PRIVATE);
       File logFile = new File(directory, "logfile");
       FileOutputStream outputStream = new FileOutputStream(logFile, true);
       OutputStreamWriter osw = new OutputStreamWriter(outputStream);
       osw.write(msg);
       osw.flush();
       osw.close();
    }

Il s’agit des niveaux de journalisation hello :
* Error (exceptions)
* Warn (avertissement)
* Info (informations)
* Verbose (détails supplémentaires)

Vous définissez le niveau de journal hello comme suit :

    Logger.getInstance().setLogLevel(Logger.LogLevel.Verbose);

 Tous les messages de journal sont envoyés toologcat, dans les rappels de journal personnalisé tooany Ajout.
Vous pouvez obtenir un fichier journal de tooa de logcat comme suit :

    adb logcat > "C:\logmsg\logfile.txt"

 Pour plus d’informations sur les commandes d’adb, consultez hello [logcat plus d’informations sur le site de Android hello](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).

#### <a name="network-traces"></a>Suivis réseau
Vous pouvez utiliser divers outils toocapture hello le trafic HTTP qui génère de la bibliothèque ADAL.  Cela est particulièrement utile si vous êtes familiarisé avec hello protocole OAuth ou si vous devez tooprovide des informations de diagnostic tooMicrosoft ou autres canaux de support.

Fiddler est un outil de suivi HTTP hello plus simple. Tooset des liens de suivants de hello d’utilisation de l’enregistrement toocorrectly ADAL trafic réseau. Pour un outil de suivi comme toobe Fiddler ou Charles utile, vous devez le configurer le trafic SSL toorecord non chiffré.  

> [!NOTE]
> Les suivis générés de cette manière peuvent contenir des informations hautement privilégiées (jetons d’accès, noms d’utilisateur, mots de passe, etc.). Si vous utilisez des comptes de production, ne partagez pas ces suivis avec des tiers. Si vous avez besoin de toosupply un toosomeone de trace dans la prise en charge de commande tooget, reproduisez le problème d’hello à l’aide d’un compte temporaire avec les noms d’utilisateur et mots de passe que vous êtes prêt à partager.

* À partir du site Web de Telerik hello : [paramètre de Fiddler pour Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)
* À partir de GitHub : [Configuration des règles de Fiddler pour la bibliothèque ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler)

### <a name="dialog-mode"></a>Mode de la boîte de dialogue
méthode d’acquireToken Hello sans activité prend en charge une invite de la boîte de dialogue.

### <a name="encryption"></a>Chiffrement
La bibliothèque ADAL chiffre les jetons hello et magasin dans SharedPreferences par défaut. Vous pouvez examiner les détails de hello StorageHelper classe toosee hello. Android a introduit Android Keydtore pour le stockage sécurisé des clés privées de la version 4.3 (API 18). La bibliothèque ADAL utilise ces informations pour l’API 18 et versions ultérieures. Si vous souhaitez toouse ADAL pour les versions inférieures de kit de développement logiciel, vous devez tooprovide une clé secrète à AuthenticationSettings.INSTANCE.setSecretKey.

### <a name="oauth2-bearer-challenge"></a>Demande de support OAuth2
Hello AuthenticationParameters classe fournit authorization_uri tooget de fonctionnalités à partir de hello défi de support OAuth2.

### <a name="session-cookies-in-webview"></a>Cookies de session dans WebView
Android WebView n’efface pas les cookies de session une fois l’application hello est fermée. Vous pouvez gérer cela à l’aide de l’exemple de code suivant :

    CookieSyncManager.createInstance(getApplicationContext());
    CookieManager cookieManager = CookieManager.getInstance();
    cookieManager.removeSessionCookie();
    CookieSyncManager.getInstance().sync();

Pour plus d’informations sur les cookies, consultez hello [CookieSyncManager plus d’informations sur le site de Android hello](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).

### <a name="resource-overrides"></a>Remplacements de ressources
bibliothèque ADAL de Hello inclut des chaînes en anglais pour les messages ProgressDialog. Votre application doit les remplacer si vous voulez des chaînes localisées.

     <string name="app_loading">Loading...</string>
     <string name="broker_processing">Broker is processing</string>
     <string name="http_auth_dialog_username">Username</string>
     <string name="http_auth_dialog_password">Password</string>
     <string name="http_auth_dialog_title">Sign In</string>
     <string name="http_auth_dialog_login">Login</string>
     <string name="http_auth_dialog_cancel">Cancel</string>

### <a name="ntlm-dialog-box"></a>Boîte de dialogue NTLM
ADAL version 1.1.0 prend en charge une boîte de dialogue NTLM qui est traitée via un événement onReceivedHttpAuthRequest hello WebViewClient. Vous pouvez personnaliser la disposition de hello et les chaînes de boîte de dialogue hello.

### <a name="cross-app-sso"></a>Authentification unique entre applications
En savoir plus [comment tooenable SSO inter-applications sur Android à l’aide de la bibliothèque ADAL](active-directory-sso-android.md).  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
