---
title: toowork aaaHow avec serveur principal de Node.js hello SDK pour applications mobiles | Documents Microsoft
description: "Découvrez comment toowork avec hello Node.js principal serveur SDK pour applications de Azure App Service Mobile."
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: e7d97d3b-356e-4fb3-ba88-38ecbda5ea50
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: node
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 2b1ea5fda6f6ca422b92fe29ff8d16bf035018d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-mobile-apps-nodejs-sdk"></a>Comment toouse hello Azure Mobile Apps Node.js SDK
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

Cet article fournit des informations détaillées et des exemples montrant comment toowork avec un service principal de Node.js dans Azure App Service Mobile Apps.

## <a name="Introduction"></a>Introduction
Azure App Service Mobile Apps permet un accès données hello capacité tooadd mobile-optimisé application web de tooa API Web.  Hello Kit de développement logiciel Azure App Service Mobile Apps est fournie pour les applications web ASP.NET et Node.js.  Hello SDK fournit hello opérations suivantes :

* Opérations de table (Read, Insert, Update, Delete) pour l’accès aux données
* Opérations d’API personnalisées

Les deux types d’opérations permettent une authentification entre tous les fournisseurs d’identité autorisés par Azure App Service, y compris les fournisseurs d’identité sociaux tels que Facebook, Twitter, Google et Microsoft, ainsi qu’Azure Active Directory pour les identités d’entreprise.

Vous trouverez des exemples pour chaque cas d’usage dans hello [répertoire d’exemples sur GitHub].

## <a name="supported-platforms"></a>Plateformes prises en charge
Bonjour Azure Mobile Apps nœud SDK prend en charge hello que LTS actuels de version de nœud et versions ultérieures.  Au moment de la rédaction, dernière version LTS hello est v4.5.0 de nœud.  Les autres versions de Node peuvent fonctionner, mais elles ne sont pas prises en charge.

Bonjour Azure Mobile Apps nœud SDK prend en charge deux pilotes de base de données - hello mssql de nœud pilote prend en charge SQL Azure et les instances locales de SQL Server.  pilote de sqlite3 Hello prend en charge les bases de données SQLite sur une seule instance.

### <a name="howto-cmdline-basicapp"></a>Comment : créer un service principal de base Node.js à l’aide de la ligne de commande de hello
Chaque serveur principal Node.js Azure App Service Mobile Apps démarre en tant qu’application ExpressJS.  ExpressJS est hello plus populaires infrastructure de service web disponible pour Node.js.  Vous pouvez créer une application [Express] de base de la manière suivante :

1. Dans une commande ou une fenêtre PowerShell, créez un répertoire pour votre projet.

        mkdir basicapp
2. Exécutez la structure du package npm init tooinitialize hello.

        cd basicapp
        npm init

    commande d’init Hello npm demande un ensemble d’un projet de questions tooinitialize hello.  Consultez la sortie de l’exemple hello :

    ![sortie d’init Hello npm][0]
3. Installer les bibliothèques d’express et applications azure-mobile de hello de dépôt de npm hello.

        npm install --save express azure-mobile-apps
4. Création d’un serveur app.js fichier tooimplement hello base mobile.

        var express = require('express'),
            azureMobileApps = require('azure-mobile-apps');

        var app = express(),
            mobile = azureMobileApps();

        // Define a TodoItem table
        mobile.tables.add('TodoItem');

        // Add hello mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);

Cette application crée un WebAPI mobile optimisé avec un seul point de terminaison (`/tables/TodoItem`) qui fournit des tooan accès non authentifié sous-jacent du magasin de données SQL à l’aide d’un schéma dynamique.  Cette API est adaptée pour les démarrages rapides de bibliothèques client suivants :

* [Android Client QuickStart]
* [Apache Cordova Client QuickStart]
* [iOS Client QuickStart]
* [Windows Store Client QuickStart]
* [Xamarin.iOS Client QuickStart]
* [Xamarin.Android Client QuickStart]
* [Xamarin.Forms Client QuickStart]

Vous pouvez trouver le code de hello pour cette application de base hello [exemple basicapp sur GitHub].

### <a name="howto-vs2015-basicapp"></a>Procédure : créer un serveur principal Node avec Visual Studio 2015
Visual Studio 2015 requiert une extension toodevelop Node.js les applications au sein de hello IDE.  toostart, installation hello [Node.js Tools 1.1 pour Visual Studio].  Une fois que hello Node.js Tools pour Visual Studio sont installés, créer une application de 4.x Express :

1. Ouvrez hello **nouveau projet** boîte de dialogue (à partir de **fichier** > **nouveau** > **projet...** ).
2. Développez **Modèles** > **JavaScript** > **Node.js**.
3. Sélectionnez hello **Basic Azure Node.js Express 4 Application**.
4. Renseignez le nom du projet hello.  Cliquez sur *OK*.

    ![Visual Studio 2015 Nouveau projet][1]
5. Avec le bouton hello **npm** nœud et sélectionnez **installer de nouveaux packages npm...** .
6. Vous devrez peut-être le catalogue de npm toorefresh hello sur la création de votre première application Node.js.  Cliquez sur **Actualiser** si nécessaire.
7. Entrez *azure-mobile-apps* dans la zone de recherche hello.  Cliquez sur hello **azure-mobile-apps 2.0.0** du package, puis cliquez sur **installer le Package**.

    ![Installer de nouveaux packages npm][2]
8. Cliquez sur **Fermer**.
9. Ouvrez hello *app.js* hello Azure Mobile Apps SDK tooadd prise en charge de fichiers.  À la ligne 6 at hello en bas de la bibliothèque de hello nécessitent des instructions, ajoutez les hello suivant de code :

        var bodyParser = require('body-parser');
        var azureMobileApps = require('azure-mobile-apps');

    À la ligne environ 27 après hello autres instructions app.use, ajoutez hello suivant de code :

        app.use('/users', users);

        // Azure Mobile Apps Initialization
        var mobile = azureMobileApps();
        mobile.tables.add('TodoItem');
        app.use(mobile);

    Enregistrez le fichier de hello.
10. Exécutez l’application hello localement (hello API est pris en charge sur http://localhost:3000) soit publier tooAzure.

### <a name="create-node-backend-portal"></a>Comment : créer un serveur Node.js principal à l’aide de hello portail Azure
Vous pouvez créer un droit de principal de l’application Mobile Bonjour [portail Azure]. Vous pouvez suivre soit hello en suivant les étapes ou créer un client et un serveur ensemble en suivant les hello [créer une application mobile](app-service-mobile-ios-get-started.md) didacticiel. didacticiel de Hello contient une version simplifiée de ces instructions et convient pour la preuve de projets de concept.

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

Dans hello *prise en main* panneau, sous **créer une table API**, choisissez **Node.js** en tant que votre **principal langage**.
Case de hello pour «**je reconnais que cette opération va remplacer tout contenu de site.**», puis cliquez sur **table TodoItem de créer**.

### <a name="download-quickstart"></a>Comment : télécharger hello Node.js principal quickstart projet de code à l’aide de Git
Lorsque vous créez un service principal de l’application Mobile Node.js à l’aide du portail de hello **démarrage rapide** panneau, un projet Node.js est créé pour vous et le site de tooyour déployé. Vous pouvez ajouter des tables et des API et modifier des fichiers de code pour le serveur principal de Node.js hello dans le portail de hello. Vous pouvez également utiliser le projet de service principal hello différents déploiement outils toodownload afin que vous pouvez ajouter ou modifier des tables et des API, puis republier le projet de hello. Pour plus d’informations, consultez le [Guide de déploiement d’Azure App Service]. Hello procédure suivante utilise un code de projet de démarrage rapide Git référentiel toodownload hello.

1. Si vous ne l’avez pas déjà fait, installez Git. tooinstall requis des étapes de Hello Git varient entre les systèmes d’exploitation. Consultez la rubrique [Installation de Git](http://git-scm.com/book/en/Getting-Started-Installing-Git) pour accéder aux distributions et consignes d'installation propres aux différents systèmes d'exploitation.
2. Suivez les étapes de hello dans [activer hello référentiel d’application de Service d’applications](../app-service-web/app-service-deploy-local-git.md#Step3) référentiel de Git tooenable hello pour votre site principal, une annotation de nom d’utilisateur du déploiement hello et le mot de passe.
3. Dans le panneau de hello pour votre serveur principal de l’application Mobile, prenez note de hello **URL de clone Git** paramètre.
4. Exécutez hello `git clone` commande à l’aide des URL de clone Git hello, entrer votre mot de passe à la demande, comme dans l’exemple suivant :

        $ git clone https://username@todolist.scm.azurewebsites.net:443/todolist.git
5. Parcourir toolocal répertoire Bonjour précédent exemple /todolist et notez que les fichiers de projet ont été téléchargés. Recherchez hello `todoitem.json` fichier Bonjour `/tables` active.  Ce fichier définit les autorisations sur la table.  Recherche également les hello `todoitem.js` fichier Bonjour même répertoire, qui définit les opérations CRUD sont effectuées de scripts pour la table de hello.
6. Une fois que vous avez apporté des modifications tooproject fichiers, exécutez hello suivant les commandes tooadd, valider, puis télécharger le site de toohello de modifications :

        $ git commit -m "updated hello table script"
        $ git push origin master

    Lorsque vous ajoutez de nouveau projet toohello de fichiers, vous devez tout d’abord tooexecute hello `git add .` commande.

site de Hello est republiée chaque fois qu’un nouvel ensemble de validation est transmise toohello site.

### <a name="howto-publish-to-azure"></a>Comment : publier votre tooAzure de back-end Node.js
Microsoft Azure fournit plusieurs mécanismes pour la publication de votre serveur principal d’Azure App Service Mobile applications Node.js pour hello service Azure.  En fonction du contrôle de la source, vous pouvez notamment utiliser les outils de déploiement intégrés à Visual Studio, les outils de ligne de commande et les options de déploiement continu.  Pour plus d’informations sur ce sujet, reportez-vous au [Guide de déploiement d’Azure App Service].

Avant le déploiement, vous devriez prendre connaissance des recommandations suivantes pour l’application Node.js avec Azure App Service :

* Comment trop[spécifier hello Version du nœud]
* Comment trop[utiliser des modules de nœud]

### <a name="howto-enable-homepage"></a>Procédure : activation d’une page d’accueil pour votre application
De nombreuses applications sont une combinaison d’applications web et mobiles et hello ExpressJS infrastructure permet de toocombine les deux facettes.  Dans certains cas, toutefois, vous pouvez choisir tooonly implémentent une interface mobile.  Il est utile tooprovide qu'un lancement page tooensure hello app service est en cours d’exécution.  Vous pouvez soit fournir votre propre page d’accueil, soit activer une page d’accueil temporaire.  tooenable une page d’accueil temporaire, utilisez hello suivant tooinstantiate Azure Mobile Apps :

    var mobile = azureMobileApps({ homePage: true });

Si vous ne souhaitez que cette option disponible lors du développement localement, vous pouvez ajouter cette tooyour paramètre `azureMobile.js` fichier.

## <a name="TableOperations"></a>Opérations de table
Bonjour azure-mobile-applications Node.js serveur SDK fournit des mécanismes tooexpose données tables stockées dans la base de données SQL Azure comme un WebAPI.  Cinq opérations sont fournies.

| Opération | Description |
| --- | --- |
| GET /tables/*tablename* |Obtenir tous les enregistrements dans la table de hello |
| GET /tables/*tablename*/:id |Obtenir un enregistrement spécifique dans la table de hello |
| POST /tables/*tablename* |Créer un enregistrement dans la table de hello |
| PATCH /tables/*tablename*/:id |Mettre à jour un enregistrement dans la table de hello |
| DELETE /tables/*tablename*/:id |Supprimer un enregistrement dans la table de hello |

Prend en charge de cette WebAPI [OData] et étend hello table schéma toosupport [synchronisation des données hors connexion].

### <a name="howto-dynamicschema"></a>Procédure : définir des tables à l’aide d’un schéma dynamique
Avant de pouvoir utiliser une table, vous devez la définir.  Les tables peuvent être définies avec un schéma statique (où les développeurs hello définit colonnes hello dans le schéma de hello) ou dynamique (où hello SDK contrôle schéma hello en fonction des demandes entrantes). En outre, développeur de hello peut contrôler des aspects spécifiques du hello WebAPI en ajoutant la définition toohello du code Javascript.

Comme meilleure pratique, vous devez définir chaque table dans un fichier Javascript dans le répertoire de tables hello, puis utiliser les tables de hello tables.import() méthode tooimport.  Extension basic-application hello, fichier de app.js hello seront ajusté :

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Define hello database schema that is exposed
    mobile.tables.import('./tables');

    // Provide initialization of any tables that are statically defined
    mobile.tables.initialize().then(function () {
        // Add hello mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);
    });

Définir la table hello dans. / tables/TodoItem.js :

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Additional configuration for hello table goes here

    module.exports = table;

Par défaut, les tables utilisent le schéma dynamique.  tooturn hors schéma dynamique définie globalement, hello paramètre d’application **MS_DynamicSchema** toofalse dans hello portail Azure.

Vous trouverez un exemple complet dans hello [exemple todo sur GitHub].

### <a name="howto-staticschema"></a>Procédure : définir des tables à l’aide d’un schéma statique
Vous pouvez définir explicitement tooexpose de colonnes hello via hello WebAPI.  Bonjour qu'azure-mobile-applications Node.js SDK ajoute automatiquement des colonnes supplémentaires requis pour la liste de toohello de synchronisation des données hors connexion que vous fournissez.  Par exemple, les applications clientes QuickStart requièrent une table à deux colonnes : une colonne texte (une chaîne) et une colonne complète (une valeur booléenne).  
table de Hello peut être défini dans hello tableau JavaScript fichier de définition (situé dans le répertoire de tables hello) comme suit :

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    module.exports = table;

Si vous définissez des tables statiquement, vous devez également appeler schéma de la base de données hello tables.initialize() méthode toocreate hello au démarrage.  Hello tables.initialize() méthode retourne un [promesse] afin que le service web de hello n’utilise pas les demandes avant l’initialisation de la base de données hello.

### <a name="howto-sqlexpress-setup"></a>Procédure : utiliser SQL Express comme datastore de développement sur votre ordinateur local
les applications mobiles Azure hello AzureMobile applications nœud SDK Hello offre trois options pour traiter les données en dehors de la zone de hello : Kit de développement logiciel offre trois options pour traiter les données en dehors de la zone de hello :

* Hello d’utilisation **mémoire** magasin pilote tooprovide non persistant
* Hello d’utilisation **mssql** pilote tooprovide un magasin de données SQL Express pour le développement
* Hello d’utilisation **mssql** pilote tooprovide une banque de données de base de données SQL Azure pour la production

Bonjour Azure Mobile Apps Node.js SDK utilise hello [mssql Node.js package] tooestablish et utiliser un tooboth de connexion SQL Express et la base de données SQL.  Ce package nécessite l’activation de connexions TCP sur votre instance SQL Express.

> [!TIP]
> pilote de la mémoire Hello ne fournit pas un ensemble complet des installations de test.  Si vous le souhaitez tootest votre serveur principal localement, nous vous recommandons d’utiliser un magasin de données SQL Express hello et hello mssql pilote.
>
>

1. Téléchargez et installez [Microsoft SQL Server 2014 Express].  Assurez-vous que vous installez hello SQL Server 2014 Express avec l’édition des outils.  Sauf si vous avez besoin explicitement la prise en charge 64 bits, version 32 bits de hello consomme moins de mémoire lors de l’exécution.
2. Exécutez hello Gestionnaire de Configuration SQL Server 2014.

   1. Développez hello **Configuration du réseau SQL Server** nœud dans le menu de gauche arborescence hello.
   2. Cliquez sur **Protocols for SQLEXPRESS**.
   3. Cliquez avec le bouton droit sur **TCP/IP**, puis sélectionnez **Enable**.  Cliquez sur **OK** dans la boîte de dialogue contextuelle hello.
   4. Cliquez avec le bouton droit sur **TCP/IP**, puis sélectionnez **Properties**.
   5. Cliquez sur hello **des adresses IP** onglet.
   6. Recherche hello **IPAll** nœud.  Bonjour **le Port TCP** , entrez **1433**.

          ![Configure SQL Express for TCP/IP][3]
   7. Cliquez sur **OK**.  Cliquez sur **OK** dans la boîte de dialogue contextuelle hello.
   8. Cliquez sur **Services SQL Server** dans le menu de gauche arborescence hello.
   9. Cliquez avec le bouton droit sur **SQL Server (SQLEXPRESS)**, puis sélectionnez **Restart**.
   10. Fermez hello Gestionnaire de Configuration SQL Server 2014.
3. Exécutez hello SQL Server 2014 Management Studio et se connecter à l’instance SQL Express local tooyour

   1. Avec le bouton droit de votre instance Bonjour l’Explorateur d’objets et sélectionnez **propriétés**
   2. Sélectionnez hello **sécurité** page.
   3. Assurez-vous de hello **mode d’authentification SQL Server et Windows** est sélectionné
   4. Cliquez sur **OK**

          ![Configure SQL Express Authentication][4]
   5. Développez **sécurité** > **connexions** Bonjour l’Explorateur d’objets
   6. Cliquez avec le bouton droit sur **Connexions** et sélectionnez **Nouvelle connexion...**.
   7. Entrez un nom de connexion.  Sélectionnez **Authentification SQL Server**.  Entrez un mot de passe, puis entrez hello dans le même mot de passe **confirmer le mot de passe**.  mot de passe Hello doit répondre aux exigences de complexité Windows.
   8. Cliquez sur **OK**

          ![Add a new user tooSQL Express][5]
   9. Cliquez avec le bouton droit sur votre nouveau compte de connexion et sélectionnez **Properties**
   10. Sélectionnez hello **rôles serveur** page
   11. Vérifiez toohello suivant de zone hello **dbcreator** rôle de serveur
   12. Cliquez sur **OK**
   13. Hello fermer SQL Server 2015 Management Studio

Vérifiez que vous vous avez sélectionné un mot de passe et de nom d’utilisateur de l’enregistrement hello.  Vous devrez peut-être tooassign des rôles serveur supplémentaires ou des autorisations en fonction de vos besoins spécifiques de la base de données.

Hello application Node.js lit hello **SQLCONNSTR_MS_TableConnectionString** variable d’environnement pour la chaîne de connexion hello pour cette base de données.  Vous pouvez définir cette variable dans votre environnement.  Par exemple, vous pouvez utiliser PowerShell tooset cette variable d’environnement :

    $env:SQLCONNSTR_MS_TableConnectionString = "Server=127.0.0.1; Database=mytestdatabase; User Id=azuremobile; Password=T3stPa55word;"

Hello d’accès via une connexion TCP/IP de base de données et fournir un nom d’utilisateur et un mot de passe de connexion de hello.

### <a name="howto-config-localdev"></a>Procédure : configurer votre projet pour un développement local
Azure Mobile Apps lit un fichier JavaScript nommé *azureMobile.js* hello de système de fichiers local.  Effectuer pas utiliser cette hello tooconfigure de fichier Azure Mobile Apps SDK en production, utiliser les paramètres de l’application au sein de hello [portail Azure] à la place.  Hello *azureMobile.js* fichier doit exporter un objet de configuration.  Hello plus courantes sont les suivantes :

* Paramètres de base de données
* Paramètres de journalisation des diagnostics
* Paramètres CORS de remplacement

Un exemple *azureMobile.js* fichier mettant en œuvre hello précédant suit les paramètres de base de données :

    module.exports = {
        cors: {
            origins: [ 'localhost' ]
        },
        data: {
            provider: 'mssql',
            server: '127.0.0.1',
            database: 'mytestdatabase',
            user: 'azuremobile',
            password: 'T3stPa55word'
        },
        logging: {
            level: 'verbose'
        }
    };

Nous vous conseillons *azureMobile.js* tooyour *.gitignore* fichier (ou un autre contrôle de code source ignorer le fichier) tooprevent les mots de passe d’être stockées dans le cloud de hello.  Configurez toujours les paramètres de production dans les paramètres de l’application au sein de hello [portail Azure].

### <a name="howto-appsettings"></a>Procédure : configuration des paramètres d’application pour votre application mobile
La plupart des paramètres hello *azureMobile.js* fichier a un paramètre d’application équivalent Bonjour [portail Azure].  Utilisez hello suivant liste tooconfigure votre application dans les paramètres de l’application :

| Paramètre d'application | *azureMobile.js* | Description | Valeurs valides |
|:--- |:--- |:--- |:--- |
| **MS_MobileAppName** |name |nom de l’application hello de Hello |string |
| **MS_MobileLoggingLevel** |logging.level |Niveau de journal minimal de messages toolog |error, warning, info, verbose, debug, silly |
| **MS_DebugMode** |debug |Activer ou désactiver le mode débogage |true, false |
| **MS_TableSchema** |data.schema |Nom de schéma par défaut pour les tables SQL |string (valeur par défaut : dbo) |
| **MS_DynamicSchema** |data.dynamicSchema |Activer ou désactiver le mode débogage |true, false |
| **MS_DisableVersionHeader** |version (jeu tooundefined) |Désactive l’en-tête de hello X-ZUMO-Server-Version |true, false |
| **MS_SkipVersionCheck** |skipversioncheck |Désactive la vérification de la version API client hello |true, false |

tooset un paramètre d’application :

1. Connectez-vous à toohello [portail Azure].
2. Sélectionnez **toutes les ressources** ou **des Services d’application** puis cliquez sur nom hello de votre application Mobile.
3. Panneau de paramètres Hello s’ouvre par défaut. Si ce n’est pas le cas, cliquez sur **Paramètres**.
4. Cliquez sur **paramètres de l’Application** menu général de hello.
5. Faites défiler toohello section de paramètres de l’application.
6. Si votre application de définir déjà existe, cliquez sur valeur hello valeur hello tooedit du paramètre d’application hello.
7. Si votre paramètre d’application n’existe pas, entrez hello paramètre d’application dans la boîte de clé hello et valeur hello dans la zone de valeur hello.
8. Une fois que vous avez terminé, cliquez sur **Enregistrer**.

La modification de la plupart des paramètres requiert le redémarrage du service.

### <a name="howto-use-sqlazure"></a>Procédure : utiliser la base de données SQL comme datastore de production
<!--- ALTERNATE INCLUDE - we can't use ../includes/app-service-mobile-dotnet-backend-create-new-service.md - slightly different semantics -->

L’utilisation de la base de données SQL Azure en tant que datastore est identique pour tous les types d’applications Azure App Service. Si vous n’avez pas déjà fait, suivez ces étapes de toocreate un service principal de l’application Mobile.

1. Connectez-vous à toohello [portail Azure].
2. Dans hello haut à gauche de la fenêtre hello, cliquez sur hello **+ nouveau** bouton > **Web + Mobile** > **l’application Mobile**, puis indiquez un nom pour votre serveur principal de l’application Mobile.
3. Bonjour **groupe de ressources** , entrez le même nom que celui de hello en tant que votre application.
4. plan de Service par défaut de l’application Hello est sélectionné.  Si vous le souhaitez toochange votre plan App Service, vous pouvez le faire en cliquant sur hello Plan App Service > **+ créer de nouveaux**.  Fournir un nom d’un nouveau plan de Service de l’application hello et sélectionnez un emplacement approprié.  Cliquez sur le niveau de tarification hello et sélectionnez un niveau de tarification approprié pour le service de hello. Sélectionnez **afficher toutes les** tooview plus tarification options, telles que **libre** et **partagé**.  Une fois que vous avez sélectionné le niveau de tarification, cliquez sur hello **sélectionnez** bouton.  Dans hello **plan App Service** panneau, cliquez sur **OK**.
5. Cliquez sur **Créer**. La configuration d’un serveur principal d’application mobile peut prendre quelques minutes.  Une fois que le serveur principal de l’application Mobile hello est configuré, le portail de hello ouvre hello **paramètres** panneau pour le serveur principal de l’application Mobile hello.

Une fois que le principal de l’application Mobile hello est créé, vous pouvez choisir tooeither se connecter à une base de données SQL existante principale de l’application Mobile tooyour ou créer une base de données SQL.  Dans cette section, nous créons une base de données SQL.

> [!NOTE]
> Si vous disposez déjà d’une base de données Bonjour même emplacement en tant que serveur principal d’application mobile hello, vous pouvez à la place choisir **utiliser une base de données** , puis sélectionnez la base de données. utilisation de Hello d’une base de données dans un autre emplacement n’est pas recommandée en raison des latences supérieures.
>
>

1. Dans le nouveau principal d’application Mobile hello, cliquez sur **paramètres** > **l’application Mobile** > **données** > **+ ajouter**.
2. Bonjour **ajouter une connexion de données** panneau, cliquez sur **base de données SQL - configurer les paramètres requis** > **créer une base de données**.  Entrez le nom hello de base de données hello Bonjour **nom** champ.
3. Cliquez sur **Serveur**.  Bonjour **nouveau serveur** panneau, entrez un nom de serveur unique Bonjour **nom du serveur** champ et fournir un approprié **ouverture de session de serveur admin** et **mot de passe**.  Vérifiez **server d’Autoriser les services azure tooaccess** est activée.  Cliquez sur **OK**.

    ![Création d’une base de données SQL Azure][6]
4. Sur hello **nouvelle base de données** panneau, cliquez sur **OK**.
5. Retour sur hello **ajouter une connexion de données** panneau, sélectionnez **chaîne de connexion**, entrez le compte de connexion hello et un mot de passe que vous avez fourni lors de la création de la base de données hello.  Si vous utilisez une base de données existante, fournissez les informations d’identification du compte de connexion de hello pour cette base de données.  Cliquez ensuite sur **OK**.
6. Retour sur hello **ajouter une connexion de données** panneau, cliquez sur **OK** base de données toocreate hello.

<!--- END OF ALTERNATE INCLUDE -->

La création de base de données hello peut prendre quelques minutes.  Hello d’utilisation **Notifications** progression de hello toomonitor zone du déploiement de hello.  Ne progressent pas jusqu'à ce que la base de données hello a été déployée avec succès.  Une fois déployée, une chaîne de connexion est créée pour l’instance de base de données SQL hello dans vos paramètres de l’application de service principal Mobile.  Vous pouvez voir ce paramètre d’application Bonjour **paramètres** > **paramètres de l’Application** > **les chaînes de connexion**.

### <a name="howto-tables-auth"></a>Comment : demander l’authentification pour accès tootables
Si vous le souhaitez toouse authentification de Service d’application avec un point de terminaison hello tables, vous devez configurer l’authentification du Service application Bonjour [portail Azure] première.  Pour plus d’informations sur la configuration de l’authentification dans un Service d’application Azure, passez en revue les hello Guide de Configuration pour le fournisseur d’identité hello vous avez l’intention de toouse :

* [Comment tooconfigure authentification Azure Active Directory]
* [Comment tooconfigure l’authentification Facebook]
* [Comment tooconfigure l’authentification Google]
* [Comment tooconfigure Microsoft Authentication]
* [Comment tooconfigure Twitter de l’authentification]

Chaque table possède une propriété d’accès qui peut être utilisé toocontrol accès toohello table.  Hello suivant l’exemple affiche un tableau défini de façon statique avec l’authentification requise.

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

propriété d’accès Hello peut prendre une des trois valeurs

* *anonyme* indique que hello client d’autorisation tooread des données sans authentification
* *authentifié* indique que hello doit envoyer un jeton d’authentification valide avec la demande de hello
* *disabled* indique que cette table est actuellement désactivée

Si la propriété d’accès hello n’est pas définie, l’accès non authentifié est autorisé.

### <a name="howto-tables-getidentity"></a>Procédure : utilisation des revendications d’authentification avec vos tables
Vous pouvez configurer différentes revendications qui sont demandées lors de la configuration de l'authentification.  Ces revendications ne sont pas normalement disponibles via hello `context.user` objet.  Toutefois, elles peuvent être récupérées à l’aide de hello `context.user.getIdentity()` (méthode).  Hello `getIdentity()` méthode retourne une promesse résolue tooan objet.  objet de Hello est indexé par la méthode d’authentification (facebook, google, twitter, microsoftaccount ou aad).

Par exemple, si vous configurez l’authentification de Microsoft Account et demande hello messagerie adresses revendication, vous pouvez ajouter enregistrement de toohello adresse hello par courrier électronique avec hello suivant du contrôleur de table :

    var azureMobileApps = require('azure-mobile-apps');

    // Create a new table definition
    var table = azureMobileApps.table();

    table.columns = {
        "emailAddress": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;
    table.access = 'authenticated';

    /**
    * Limit hello context query toothose records with hello authenticated user email address
    * @param {Context} context hello operation context
    * @returns {Promise} context execution Promise
    */
    function queryContextForEmail(context) {
        return context.user.getIdentity().then((data) => {
            context.query.where({ emailAddress: data.microsoftaccount.claims.emailaddress });
            return context.execute();
        });
    }

    /**
    * Adds hello email address from hello claims toohello context item - used for
    * insert operations
    * @param {Context} context hello operation context
    * @returns {Promise} context execution Promise
    */
    function addEmailToContext(context) {
        return context.user.getIdentity().then((data) => {
            context.item.emailAddress = data.microsoftaccount.claims.emailaddress;
            return context.execute();
        });
    }

    // Configure specific code when hello client does a request
    // READ - only return records belonging toohello authenticated user
    table.read(queryContextForEmail);

    // CREATE - add or overwrite hello userId based on hello authenticated user
    table.insert(addEmailToContext);

    // UPDATE - only allow updating of record belong toohello authenticated user
    table.update(queryContextForEmail);

    // DELETE - only allow deletion of records belong toohello authenticated uer
    table.delete(queryContextForEmail);

    module.exports = table;

toosee les revendications sont disponibles, utilisez un Bonjour tooview de navigateur web `/.auth/me` point de terminaison de votre site.

### <a name="howto-tables-disabled"></a>Comment : désactiver les opérations de table accès toospecific
Dans tooappearing d’ajout sur la table de hello, propriété d’accès hello peut être utilisé toocontrol des opérations individuelles.  Il existe quatre opérations :

* *lire* est hello RESTful une opération GET sur la table de hello
* *Insérer* est opération POST RESTful de hello sur la table de hello
* *mettre à jour* est hello correctif RESTful opération sur la table de hello
* *supprimer* est l’opération de suppression RESTful hello sur la table de hello

Par exemple, vous souhaiterez peut-être tooprovide une table non authentifiée en lecture seule :

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Read-Only table - only allow READ operations
    table.read.access = 'anonymous';
    table.insert.access = 'disabled';
    table.update.access = 'disabled';
    table.delete.access = 'disabled';

    module.exports = table;

### <a name="howto-tables-query"></a>Comment : régler requête hello qui est utilisé avec les opérations de table
Une exigence courante pour les opérations de table est tooprovide une vue restreinte des données de hello.  Par exemple, vous pouvez fournir une table qui est marquée avec hello authentifié ID d’utilisateur, telles que vous pouvez uniquement lire ou mettre à jour vos propres enregistrements.  Hello, suivant la définition de table fournit cette fonctionnalité :

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define a static schema for hello table
    table.columns = {
        "userId": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;

    // Require authentication for this table
    table.access = 'authenticated';

    // Ensure that only records for hello authenticated user are retrieved
    table.read(function (context) {
        context.query.where({ userId: context.user.id });
        return context.execute();
    });

    // When adding records, add or overwrite hello userId with hello authenticated user
    table.insert(function (context) {
        context.item.userId = context.user.id;
        return context.execute();
    });

    module.exports = table;

Les opérations qui exécutent normalement une requête ont une propriété de requête que vous pouvez ajuster avec une clause where. propriété de requête Hello est un [QueryJS] de l’objet qui est utilisé tooconvert un toosomething de requête OData qui hello de données principal peut traiter.  Pour les cas d’égalité simple (par exemple hello précédant un), une carte peut servir. Vous pouvez également ajouter des clauses SQL spécifiques :

    context.query.where('myfield eq ?', 'value');

### <a name="howto-tables-softdelete"></a>Procédure : configurer une suppression réversible sur une table
La suppression réversible (Soft Delete) ne supprime pas réellement les enregistrements.  À la place il les marque comme étant supprimées dans la base de données hello en définissant tootrue de colonne hello supprimé.  Bonjour Azure Mobile Apps SDK supprime automatiquement supprimé des enregistrements à partir des résultats, sauf si hello Mobile Client SDK utilise IncludeDeleted().  tooconfigure supprimer d’une table pour soft, définissez hello `softDelete` propriété dans le fichier de définition de table hello :

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Turn on Soft Delete
    table.softDelete = true;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

Vous devez établir un mécanisme pour purger les enregistrements, à partir d’une application cliente, via un WebJob, via une fonction Azure ou via une API personnalisée.

### <a name="howto-tables-seeding"></a>Procédure : alimenter votre base de données
Lorsque vous créez une nouvelle application, vous pouvez tooseed une table avec des données.  Cela est possible dans un fichier JavaScript de définition de table hello comme suit :

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };
    table.seed = [
        { text: 'Example 1', complete: false },
        { text: 'Example 2', complete: true }
    ];

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

L’amorçage de données s’effectue uniquement lors de la table de hello est créée par hello Azure Mobile Apps SDK.  Si hello existe déjà dans la base de données hello, aucune donnée n’est introduite dans un tableau de hello.  Si le schéma dynamique est activé, le schéma est déduit à partir des données de hello d’amorçage.

Nous recommandons d’appeler explicitement hello `tables.initialize()` table de hello toocreate mode de démarrage du service de hello en cours d’exécution.

### <a name="Swagger"></a>Procédure : activation de la prise en charge de Swagger
Azure App Service Mobile Apps prend nativement en charge l’interface [Swagger] .  tooenable prise en charge de Swagger, installez tout d’abord hello swagger interface utilisateur en tant que dépendance :

    npm install --save swagger-ui

Une fois installé, vous pouvez activer la prise en charge de Swagger dans le constructeur d’applications mobiles Azure hello :

    var mobile = azureMobileApps({ swagger: true });

Vous tooenable que vous souhaitez probablement uniquement prise en charge de Swagger dans les éditions de développement.  Pour ce faire, vous pouvez utiliser le paramètre d’application `NODE_ENV` :

    var mobile = azureMobileApps({ swagger: process.env.NODE_ENV !== 'production' });

Hello point de terminaison swagger se trouve à http://*yoursite*.azurewebsites.net/swagger.  Vous pouvez accéder à hello Swagger de l’interface utilisateur via hello `/swagger/ui` point de terminaison.  Si vous choisissez l’authentification de toorequire dans toute votre application, Swagger génère une erreur.  Pour de meilleurs résultats, choisissez demandes tooallow non authentifiée via Bonjour Azure App Service authentification / paramètres d’autorisation, puis contrôler l’authentification à l’aide de hello `table.access` propriété.

Vous pouvez également ajouter hello Swagger option tooyour `azureMobile.js` fichier si vous souhaitez uniquement prise en charge de Swagger lors du développement localement.

## <a name="a-namepushpush-notifications"></a><a name="push">Notifications Push
Applications mobiles s’intègre à Azure Notification Hubs tooenable vous toomillions de notifications push toosend ciblé d’appareils sur toutes les plateformes principales. À l’aide de concentrateurs de Notification, vous pouvez envoyer push notifications tooiOS, appareils Android et Windows. consultez des concentrateurs de Notification, toolearn plus que vous peuvent faire avec [vue d’ensemble des concentrateurs de Notification](../notification-hubs/notification-hubs-push-notification-overview.md).

### </a><a name="send-push"></a>Procédure : envoi de notifications Push
Hello suivant de code montre comment toouse hello push objet toosend une diffusion push des appareils iOS notification tooregistered :

    // Create an APNS payload.
    var payload = '{"aps": {"alert": "This is an APNS payload."}}';

    // Only do hello push if configured
    if (context.push) {
        // Send a push notification using APNS.
        context.push.apns.send(null, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }

En créant un enregistrement de push de modèle à partir du client de hello, vous pouvez à la place envoyer un toodevices de message push modèle sur toutes les plateformes prises en charge. Hello suivant de code montre comment toosend une notification de modèle :

    // Define hello template payload.
    var payload = '{"messageParam": "This is a template payload."}';

    // Only do hello push if configured
    if (context.push) {
        // Send a template notification.
        context.push.send(null, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }


### <a name="push-user"></a>Comment : envoi push notifications tooan authentifié l’utilisateur à l’aide de balises
Lorsqu’un utilisateur authentifié s’inscrit pour les notifications push, une balise d’ID utilisateur est automatiquement ajoutée l’enregistrement de toohello. À l’aide de cette balise, vous pouvez envoyer des périphériques de tooall notifications inscrits par un utilisateur spécifique par émission de données. Hello de code suivant obtient hello SID de l’utilisateur qui effectue la demande de hello et envoie une inscription de périphérique modèle push notification tooevery pour cet utilisateur :

    // Only do hello push if configured
    if (context.push) {
        // Send a notification toohello current user.
        context.push.send(context.user.id, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }

Quand vous vous inscrivez à des notifications Push à partir d’un client authentifié, assurez-vous au préalable que l’authentification est bien terminée.

## <a name="CustomAPI"></a> API personnalisées
### <a name="howto-customapi-basic"></a>Procédure : définition d'une API personnalisée
En outre toohello d’accès aux données API via le point de terminaison /tables hello, les applications mobiles Azure peut fournir une couverture API personnalisée.  API personnalisées sont définies dans une façon toohello table des définitions similaires et peuvent accéder à tous les hello mêmes installations, y compris l’authentification.

Si vous le souhaitez toouse authentification de Service d’application avec une API personnalisée, vous devez configurer l’authentification du Service application Bonjour [portail Azure] première.  Pour plus d’informations sur la configuration de l’authentification dans un Service d’application Azure, passez en revue les hello Guide de Configuration pour le fournisseur d’identité hello vous avez l’intention de toouse :

* [Comment tooconfigure authentification Azure Active Directory]
* [Comment tooconfigure l’authentification Facebook]
* [Comment tooconfigure l’authentification Google]
* [Comment tooconfigure Microsoft Authentication]
* [Comment tooconfigure Twitter de l’authentification]

Les API personnalisées sont définies à peu près comme hello API Tables hello.

1. Créez un répertoire **api** .
2. Créer un fichier JavaScript de définition API Bonjour **api** active.
3. Utilisez Bonjour importation méthode tooimport Bonjour **api** active.

Voici la définition de l’api prototype hello basée sur d’exemple hello basic-app utilisé précédemment.

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Import hello Custom API
    mobile.api.import('./api');

    // Add hello mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

Prenons un exemple API qui renvoie la date du serveur hello à l’aide de hello *Date.now()* (méthode).  Voici le fichier de api/date.js hello :

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };

    module.exports = api;

Chaque paramètre est un des hello RESTful verbes standard - GET, POST, PATCH ou DELETE.  méthode Hello est une norme [ExpressJS Middleware] fonction qui envoie la sortie de hello requis.

### <a name="howto-customapi-auth"></a>Comment : exiger l’authentification pour l’API personnalisée d’accès tooa
Kit de développement Azure Mobile Apps implémente l’authentification dans hello identique pour le point de terminaison hello tables et des API personnalisées.  Pour ajouter l’authentification toohello API est développé dans la section précédente de hello, ajoutez un **accès** propriété :

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };
    // All methods must be authenticated.
    api.access = 'authenticated';

    module.exports = api;

Vous pouvez également spécifier l’authentification sur des opérations spécifiques :

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        }
    };
    // hello GET methods must be authenticated.
    api.get.access = 'authenticated';

    module.exports = api;

Hello même jeton qui est utilisé pour le point de terminaison hello tables doit être utilisé pour les API personnalisées nécessitant une authentification.

### <a name="howto-customapi-auth"></a>Procédure : gestion des téléchargements de fichiers volumineux
Azure Mobile Apps SDK utilise hello [corps-analyseur intergiciel (middleware)](https://github.com/expressjs/body-parser) tooaccept et décoder le contenu du corps de votre demande.  Vous pouvez préconfigurer les téléchargements de fichiers plus volumineux corps-analyseur tooaccept :

    var express = require('express'),
        bodyParser = require('body-parser'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Set up large body content handling
    app.use(bodyParser.json({ limit: '50mb' }));
    app.use(bodyParser.urlencoded({ limit: '50mb', extended: true }));

    // Import hello Custom API
    mobile.api.import('./api');

    // Add hello mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

fichier de Hello est codée avant la transmission en base-64.  Cela augmente la taille hello de téléchargement réelle de hello (et donc hello taille, que vous devez prendre en compte).

### <a name="howto-customapi-sql"></a>Procédure : exécution d’instructions SQL personnalisées
Hello Azure Mobile Apps SDK permet l’accès toohello ensemble du contexte via l’objet de demande hello, ce qui vous tooexecute paramétrables fournisseur de données SQL instructions toohello facilement :

    var api = {
        get: function (request, response, next) {
            // Check for parameters - if not there, pass on tooa later API call
            if (typeof request.params.completed === 'undefined')
                return next();

            // Define hello query - anything that can be handled by hello mssql
            // driver is allowed.
            var query = {
                sql: 'UPDATE TodoItem SET complete=@completed',
                parameters: [{
                    completed: request.params.completed
                }]
            };

            // Execute hello query.  hello context for Azure Mobile Apps is available through
            // request.azureMobile - hello data object contains hello configured data provider.
            request.azureMobile.data.execute(query)
            .then(function (results) {
                response.json(results);
            });
        }
    };

    api.get.access = 'authenticated';
    module.exports = api;

## <a name="Debugging"></a>Débogage, Tables facile et API simples
### <a name="howto-diagnostic-logs"></a>Procédure : débogage, diagnostic et résolution des problèmes sur Azure Mobile Apps
Hello du Service d’applications Azure fournit plusieurs de débogage et de résolution des problèmes techniques pour les applications de Node.js.
Consultez toohello suivant tooget articles démarré dans Résolution des problèmes de votre serveur principal Node.js Mobile :

* [Surveiller les applications web dans Microsoft Azure App Service]
* [Activer la journalisation des diagnostics pour les applications web dans Azure App Service]
* [Dépanner un service Azure App dans Visual Studio]

Les applications Node.js ont accès tooa une large gamme d’outils de diagnostic de journal.  En interne, les hello Azure Mobile Apps Node.js SDK utilise [Winston] pour la journalisation des Diagnostics.  La journalisation est activée automatiquement en activant le mode de débogage ou en définissant un hello **MS_DebugMode** tootrue de paramètre d’application Bonjour [portail Azure]. Journaux générés s’affichent dans hello des journaux de Diagnostic sur hello [portail Azure].

### <a name="in-portal-editing"></a><a name="work-easy-tables"></a>Comment : utiliser des Tables facile Bonjour portail Azure
Tables facile dans le portail de hello vous permettent de créer et manipuler directement de tables dans le portail de hello. Vous pouvez modifier les opérations de table à l’aide de hello éditeur de Service d’applications.

Lorsque vous cliquez sur **Easy Tables** dans vos paramètres de site principal, vous pouvez ajouter, modifier ou supprimer une table. Vous pouvez également voir les données de table de hello.

![Utilisation de l’outil Easy Tables](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-tables.png)

Hello commandes suivantes sont disponibles sur la barre de commandes hello pour une table :

* **Modifier les autorisations** - modifier l’autorisation hello pour la lecture, insérer, mettre à jour et opérations delete sur la table de hello.
  Les options sont tooallow l’accès anonyme, une authentification toorequire ou toodisable tous les accès toohello opération.
* **Modifier le script** -fichier de script hello pour la table de hello est ouvert dans hello éditeur de Service d’applications.
* **Gérer le schéma** - ajouter ou supprimer des colonnes ou modifier des index de table hello.
* **Effacer le tableau** -tronque une table existante Supprimer toutes les lignes de données mais en laissant le schéma de hello reste la même.
* **Supprimer des lignes** : supprimer des lignes de données spécifiques.
* **Affichage des journaux de diffusion en continu** -vous connecte toohello service de journal de votre site de diffusion en continu.

### <a name="work-easy-apis"></a>Comment : travailler avec les API facile Bonjour portail Azure
Une API simple dans le portail de hello vous permettre de créer et manipuler le droit d’API personnalisé dans le portail de hello. Vous pouvez modifier les scripts d’API à l’aide de hello éditeur de Service d’applications.

Lorsque vous cliquez sur **Easy APIs** dans vos paramètres de site principal, vous pouvez ajouter modifier ou supprimer un point de terminaison API personnalisé.

![Utilisation de l’outil Easy APIs](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-apis.png)

Dans le portail hello, vous pouvez modifier les autorisations d’accès hello pour une action HTTP donnés, modifier le fichier de script d’API hello dans l’éditeur de Service application ou afficher les journaux de diffusion en continu hello.

### <a name="online-editor"></a>Comment : modifier le code dans hello éditeur de Service d’applications
Hello portail Azure vous permet de modifier vos fichiers de script principal Node.js Bonjour éditeur de Service d’applications sans avoir à télécharger l’ordinateur local de hello projet tooyour. tooedit des fichiers de script dans l’éditeur en ligne hello :

1. Dans le panneau de votre serveur principal d’application mobile, cliquez sur **Tous les paramètres** > **Tables faciles** ou **API faciles**, cliquez sur une table ou une API, puis cliquez sur **Modifier le script**. fichier de script Hello est ouvert dans hello éditeur de Service d’applications.

    ![Éditeur App Service](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-visual-studio-editor.png)
2. Vérifiez votre fichier de code toohello modifications dans l’éditeur en ligne hello. Les modifications sont enregistrées automatiquement au fil de la saisie.

<!-- Images -->
[0]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/npm-init.png
[1]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-new-project.png
[2]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-install-npm.png
[3]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-config.png
[4]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-authconfig.png
[5]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-newuser-1.png
[6]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/dotnet-backend-create-db.png

<!-- URLs -->
[Android Client QuickStart]: app-service-mobile-android-get-started.md
[Apache Cordova Client QuickStart]: app-service-mobile-cordova-get-started.md
[iOS Client QuickStart]: app-service-mobile-ios-get-started.md
[Xamarin.iOS Client QuickStart]: app-service-mobile-xamarin-ios-get-started.md
[Xamarin.Android Client QuickStart]: app-service-mobile-xamarin-android-get-started.md
[Xamarin.Forms Client QuickStart]: app-service-mobile-xamarin-forms-get-started.md
[Windows Store Client QuickStart]: app-service-mobile-windows-store-dotnet-get-started.md
[HTML/Javascript Client QuickStart]: app-service-html-get-started.md
[synchronisation des données hors connexion]: app-service-mobile-offline-data-sync.md
[Comment tooconfigure authentification Azure Active Directory]: app-service-mobile-how-to-configure-active-directory-authentication.md
[Comment tooconfigure l’authentification Facebook]: app-service-mobile-how-to-configure-facebook-authentication.md
[Comment tooconfigure l’authentification Google]: app-service-mobile-how-to-configure-google-authentication.md
[Comment tooconfigure Microsoft Authentication]: app-service-mobile-how-to-configure-microsoft-authentication.md
[Comment tooconfigure Twitter de l’authentification]: app-service-mobile-how-to-configure-twitter-authentication.md
[Guide de déploiement d’Azure App Service]: ../app-service-web/web-sites-deploy.md
[Surveiller les applications web dans Microsoft Azure App Service]: ../app-service-web/web-sites-monitor.md
[Activer la journalisation des diagnostics pour les applications web dans Azure App Service]: ../app-service-web/web-sites-enable-diagnostic-log.md
[Dépanner un service Azure App dans Visual Studio]: ../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md
[spécifier hello Version du nœud]: ../nodejs-specify-node-version-azure-apps.md
[utiliser des modules de nœud]: ../nodejs-use-node-modules-azure-apps.md
[Create a new Azure App Service]: ../app-service-web/
[azure-mobile-apps]: https://www.npmjs.com/package/azure-mobile-apps
[Express]: http://expressjs.com/
[Swagger]: http://swagger.io/

[portail Azure]: https://portal.azure.com/
[OData]: http://www.odata.org
[promesse]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
[exemple basicapp sur GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app
[exemple todo sur GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo
[répertoire d’exemples sur GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
[QueryJS]: https://github.com/Azure/queryjs
[Node.js Tools 1.1 pour Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1
[mssql Node.js package]: https://www.npmjs.com/package/mssql
[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx
[ExpressJS Middleware]: http://expressjs.com/guide/using-middleware.html
[Winston]: https://github.com/winstonjs/winston
