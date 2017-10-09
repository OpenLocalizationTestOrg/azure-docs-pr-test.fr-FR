---
title: aaaCreate une application de conversation Node.js avec Socket.IO dans Azure App Service
description: "Didacticiel démontrant l’utilisation de socket.io dans une application web node.js hébergée sur Azure."
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: c4c4af36-3ecf-4619-b586-ca90d53ce35b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 3bd7867ccc297dc0a21c7a00cc9db06358877f5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-nodejs-chat-application-with-socketio-in-azure-app-service"></a>Créer une application de conversation instantanée Node.js avec Socket.IO dans Azure App Service
Socket.IO offre une communication en temps réel entre votre serveur node.js et vos clients à l'aide de WebSockets. Il prend également en charge les transports de secours tooother (par exemple, d’interrogation longue) qui fonctionnent avec les navigateurs plus anciens. Ce didacticiel vous guide hébergeant une application de conversation Socket.IO basé sous forme d’application web Azure et vous montrent comment tooscale hello à l’aide de l’application [Cache Redis Azure]. Pour plus d’informations sur Socket.IO, consultez le site <http://socket.io/>.

> [!NOTE]
> les procédures dans cette tâche Hello appliquent trop[App Service Web Apps]; pour les Services de cloud computing, consultez [générer une Application de Chat Node.js avec Socket.IO sur un Service Cloud Azure].
> 
> 

## <a name="download-hello-chat-example"></a>Télécharger l’exemple de conversation hello
Pour ce projet, nous allons utiliser exemple hello conversation hello [référentiel GitHub de Socket.IO]. Effectuer hello étapes toodownload hello exemple suivant et l’ajouter projet toohello créé précédemment.

1. Télécharger un [ZIP ou GZ archivé version] du projet de Socket.IO hello (version 1.3.5 a été utilisée pour ce document)
2. Extraire hello de copie et d’archivage hello **exemples\\chat** nouvel emplacement de répertoire tooa. Par exemple, **\\node\\chat**.

## <a name="modify-appjs-and-install-modules"></a>Modifier le fichier app.js et installer les modules
1. Renommer hello **index.js** trop de fichiers**app.js**. Cela permet à Azure toodetect qu’il s’agit d’une application Node.js.
2. Ouvrez hello **app.js** fichier dans un éditeur de texte. Qui contient la ligne hello modification `var io = require('../..')(server);` comme indiqué ci-dessous :
   
       var express = require('express');
       var app = express();
       var server = require('http').createServer(app);
       // var io = require('../..')(server);
       // New:
       var io = require('socket.io')(server);
       var port = process.env.PORT || 3000;
3. Ouvrez hello **package.json** et ajoutez un toosocket.io référence sous `dependencies`, comme indiqué ci-dessous :
   
        "dependencies": {
          "express": "3.4.8",
          "socket.io": "1.3.5"
        }
4. Hello de ligne de commande, de modifier toohello  **\\nœud\\chat** active et l’utilisation tooinstall hello des modules npm requis par cette application :
   
        npm install
   
    Les modules hello va être installé dans un sous-dossier nommé **node_modules**.

## <a name="create-an-azure-web-app"></a>Créer une application web Azure
Suivez ces étapes de toocreate une application web Azure, activer la publication Git et activer la prise en charge de WebSocket pour l’application web de hello.

> [!NOTE]
> toocomplete ce didacticiel, vous avez besoin d’un compte Azure. Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes. Pour plus d'informations, consultez la page <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Version d'évaluation gratuite d'Azure</a>.
> 
> 

1. Installer hello Azure Interface de ligne (Azure) et se connecter tooyour abonnement Azure. Consultez [installer et configurer hello CLI d’Azure](../cli-install-nodejs.md).
2. S’il s’agit de votre premier paramètre de temps un référentiel dans Azure, vous avez besoin des informations d’identification de connexion toocreate. À partir de hello CLI d’Azure, entrez hello de commande suivante :
   
        azure site deployment user set [username] [password]
3. Modifier toohello  **\\node\chat** active et suit de hello utilisez commande toocreate une nouvelle application web Azure et un référentiel Git local. Cette commande crée également un Git distant nommé ’azure’.
   
        azure site create mysitename --git
   
    Vous devez remplacer ’mysitename’ par le nom unique de votre application web.
4. Valider le référentiel local hello existant fichiers toohello à l’aide de hello suivant de commandes :
   
        git add .
        git commit -m "Initial commit"
5. Push référentiel des applications Web Azure hello fichiers toohello avec hello de commande suivante :
   
        git push azure master
   
    Lorsque vous y êtes invité, entrez vos informations d'identification de l'étape 2. Vous recevez des messages d’état comme les modules sont importés sur le serveur de hello. Une fois ce processus terminé, application hello sera hébergée sur votre application web Azure.
   
   > [!NOTE]
   > Pendant l’installation du module, vous remarquerez peut-être des erreurs qui « hello projet importé... n’a été trouvé ». Vous pouvez les ignorer sans problème.
   > 
   > 
6. Socket.IO utilise WebSockets, qui n'est pas activé par défaut sur Azure. tooenable WebSocket, utilisez hello de commande suivante :
   
        azure site set -w
   
    Si vous y êtes invité, entrez le nom hello de hello web app.
   
   > [!NOTE]
   > Bonjour va de commande 'site azure set -w' fonctionnent uniquement avec la version 0.7.4 ou une version ultérieure de hello Interface de ligne de commande de Azure. Vous pouvez également activer la prise en charge de WebSocket à l’aide de hello [Azure Portal](https://portal.azure.com).
   > 
   > à l’aide du protocole WebSocket tooenable hello portail Azure, cliquez sur l’application web à partir du panneau des applications Web hello hello **tous les paramètres** > **paramètres de l’Application**. Sous **WebSockets**, cliquez sur **Activé**. Cliquez ensuite sur **Enregistrer**.
   > 
   > 
7. tooview hello web application Azure, suivant le hello utilisez commande toolaunch votre navigateur web et accédez toohello hébergé l’application web :
   
        azure site browse

Votre application s’exécute à présent sur Azure et peut relayer des messages de conversation instantanée entre différents clients en utilisant Socket.IO.

## <a name="scale-out"></a>Montée en charge
Les applications Socket.IO peuvent être monté en charge à l’aide un **carte** toodistribute messages et les événements entre plusieurs instances d’application. Lorsqu’il existe plusieurs adaptateurs disponibles, hello [socket.io-redis] adaptateur peut être facilement utilisé avec la fonctionnalité de Cache Redis Azure hello.

> [!NOTE]
> Une autre condition requise par la montée en charge d’une solution Socket.IO est la prise en charge des sessions rémanentes. Celles-ci sont activées par défaut pour Azure Web Apps par l’intermédiaire d’Azure Request Routing. Pour plus d'informations, consultez [Affinité d'instance dans Sites Web Azure].
> 
> 

### <a name="create-a-redis-cache"></a>Création d'un cache Redis
Effectuez les étapes de hello dans [créer un cache dans le Cache Redis Azure] toocreate un nouveau cache.

> [!NOTE]
> Enregistrer hello **nom d’hôte** et **clé primaire** pour votre cache, car elles seront nécessaires dans hello étapes suivantes.
> 
> 

### <a name="add-hello-redis-and-socketio-redis-modules"></a>Ajouter les redis hello et les modules de socket.io-redis
1. À partir d’une ligne de commande, modifiez toohello  **\\nœud\\chat** active et l’utilisation hello commande suivante.
   
        npm install socket.io-redis@0.1.4 redis@0.12.1 --save
   
   > [!NOTE]
   > les versions de Hello spécifiées dans cette commande sont des versions de hello utilisées lors du test de cet article.
   > 
   > 
2. Modifier hello **app.js** suivant de fichier tooadd hello lignes immédiatement après`var io = require('socket.io')(server);`
   
        var pub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
        var sub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
   
        var redis = require('socket.io-redis');
        io.adapter(redis({pubClient: pub, subClient: sub}));
   
    Remplacez **redishostname** et **rediskey** avec le nom d’hôte hello et clé de votre cache Redis.
   
    Cela créera une publication et abonnement client toohello cache Redis créé précédemment. les clients de Hello sont ensuite utilisés avec hello adaptateur tooconfigure cache Redis de Socket.IO toouse hello pour le transfert des messages et les événements entre instances de votre application
   
   > [!NOTE]
   > Lors de hello **socket.io-redis** adaptateur peut communiquer directement tooRedis, la version actuelle de hello ne prend pas en charge l’authentification hello requise par le cache Azure Redis. Pour la connexion initiale hello est créée à l’aide de hello **redis** module, puis client de hello est passé toohello **socket.io-redis** carte.
   > 
   > Cache Redis Azure prend en charge les connexions sécurisées à l’aide du port 6380, modules hello utilisés dans cet exemple ne prennent pas en charge les connexions sécurisées à compter du 14/7/2014. Hello au-dessus de code utilise par défaut hello, un port non sécurisé de 6379.
   > 
   > 
3. Hello enregistrer modifié **app.js**

### <a name="commit-changes-and-redeploy"></a>Validation des modifications et redéploiement
À partir de hello de ligne de commande Bonjour  **\\nœud\\chat** active, utilisez hello commandes toocommit modifications suivantes et redéployer l’application hello.

    git add .
    git commit -m "implementing scale out"
    git push azure master

Une fois les modifications hello ont été déplacées toohello serveur, vous pouvez faire évoluer votre site sur plusieurs instances à l’aide de hello commande suivante.

    azure site scale instances --instances #

Où  **#**  est le nombre de hello d’instances toocreate.

Vous pouvez vous connecter à l’application web tooyour à partir de plusieurs tooverify de navigateurs ou les ordinateurs qui sont correctement envoyés tooall clients.

## <a name="troubleshooting"></a>Résolution des problèmes
### <a name="connection-limits"></a>Limites de connexions
Les applications Web Azure est disponible dans plusieurs SKU, qui déterminent le site de hello ressources tooyour disponibles. Cela inclut le nombre de hello de WebSocket de connexions autorisées. Pour plus d’informations, consultez hello [page de tarification des applications Web].

### <a name="messages-arent-being-sent-using-websockets"></a>Les messages ne sont pas envoyés avec WebSockets
Si les navigateurs clients conservent revenir toolong d’interrogation au lieu d’utiliser le protocole WebSocket, il peut être en raison d’une des manières suivantes les hello.

* **Essayez en limitant hello transport toojust WebSockets**
  
    Dans l’ordre pour Socket.IO toouse WebSocket en tant que hello transport de messagerie, hello serveur et le client doivent prendre en charge WebSocket. Si un ou hello autres n’existe pas, Socket.IO va négocier un autre transport, telles que l’interrogation longue. liste des transports utilisés par Socket.IO par défaut de Hello est ` websocket, htmlfile, xhr-polling, jsonp-polling`. Vous pouvez forcer il tooonly utiliser WebSocket en ajoutant hello suivant code toohello **app.js** fichier, après la ligne contenant de hello `, nicknames = {};`.
  
        io.configure(function() {
          io.set('transports', ['websocket']);
        });
  
  > [!NOTE]
  > Notez que les navigateurs plus anciens qui ne prennent pas en charge les WebSockets ne seront pas en mesure de tooconnect toohello site alors que hello au-dessus de code est actif, il restreint uniquement tooWebSockets de communication.
  > 
  > 
* **Utilisation du protocole SSL**
  
    Protocole WebSocket s’appuie sur certains en-têtes HTTP utilisés moindre, par exemple hello **mise à niveau** en-tête. Certains périphériques réseau intermédiaires, tels que les proxys web, peuvent supprimer ces en-têtes. tooavoid ce problème, vous pouvez établir la connexion WebSocket hello via le protocole SSL.
  
    Un moyen simple de tooaccomplish Voici tooconfigure Socket.IO trop`match origin protocol`. Cela indique hello de communication Socket.IO toosecure WebSockets identique hello origine HTTP/HTTPS demande de page web de hello. Si un navigateur utilise un toovisit URL HTTPS à votre site Web, les communications ultérieures WebSocket via Socket.IO seront sécurisées via le protocole SSL.
  
    toomodify tooenable de cet exemple montre comment cette configuration, ajoutez hello suivant code toohello **app.js** fichier après hello ligne contenant `, nicknames = {};`.
  
        io.configure(function() {
          io.set('match origin protocol', true);
        });
* **Vérification des paramètres de web.config**
  
    Les applications web Azure qui hébergent des applications Node.js utilisent hello **web.config** tooroute fichier entrant demande toohello Node.js application. Pour toofunction WebSockets correctement avec les applications Node.js, hello **web.config** doit contenir hello entrée suivante.
  
        <webSocket enabled="false"/>
  
    Cela désactive le module WebSockets IIS hello, qui inclut sa propre implémentation de WebSocket et est en conflit avec les modules Node.js de WebSocket spécifiques telles que Socket.IO. Si cette ligne n’est pas présente ou est définie trop`true`, cela peut être la raison de hello transport WebSocket de hello ne fonctionne pas pour votre application.
  
    Normalement, les applications Node.js n’incluent pas de fichier **web.config**. Par conséquent, l’offre Sites Web Azure en génère un automatiquement pour les applications Node.js lors de leur déploiement. Étant donné que ce fichier est généré automatiquement sur le serveur de hello, vous devez utiliser hello FTP ou FTPS une URL pour votre site Web tooview de ce fichier. Vous pouvez trouver hello FTP et FTPS des URL de votre site dans le portail classique de hello en sélectionnant votre application web et puis hello **tableau de bord** lien. Hello URL sont affichés dans hello **coup de œil rapide** section.
  
  > [!NOTE]
  > Hello **web.config** fichier est généré uniquement par les sites Web Azure si votre application n’en fournit pas. Si vous fournissez un **web.config** fichier racine hello de votre projet d’application, il sera utilisé par les applications Web Azure.
  > 
  > 
  
    Si les entrée hello n’est pas présente ou a la valeur tooa de `true`, vous devez créer un **web.config** hello racine de votre application Node.js et spécifiez la valeur `false`.  Pour référence, hello ci-dessous est une valeur par défaut **web.config** pour une application qui utilise **app.js** en tant que point d’entrée hello.
  
        <?xml version="1.0" encoding="utf-8"?>
        <!--
             This configuration file is required if iisnode is used toorun node processes behind
             IIS or IIS Express.  For more information, visit:
  
             https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config
        -->
  
        <configuration>
          <system.webServer>
            <!-- Visit http://blogs.msdn.com/b/windowsazure/archive/2013/11/14/introduction-to-websockets-on-windows-azure-web-sites.aspx for more information on WebSocket support -->
            <webSocket enabled="false" />
            <handlers>
              <!-- Indicates that hello server.js file is a node.js web app toobe handled by hello iisnode module -->
              <add name="iisnode" path="app.js" verb="*" modules="iisnode"/>
            </handlers>
            <rewrite>
              <rules>
                <!-- Do not interfere with requests for node-inspector debugging -->
                <rule name="NodeInspector" patternSyntax="ECMAScript" stopProcessing="true">
                  <match url="^app.js\/debug[\/]?" />
                </rule>
  
                <!-- First we consider whether hello incoming URL matches a physical file in hello /public folder -->
                <rule name="StaticContent">
                  <action type="Rewrite" url="public{REQUEST_URI}"/>
                </rule>
  
                <!-- All other URLs are mapped toohello node.js web app entry point -->
                <rule name="DynamicContent">
                  <conditions>
                    <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="True"/>
                  </conditions>
                  <action type="Rewrite" url="app.js"/>
                </rule>
              </rules>
            </rewrite>
            <!--
              You can control how Node is hosted within IIS using hello following options:
                * watchedFiles: semi-colon separated list of files that will be watched for changes toorestart hello server
                * node_env: will be propagated toonode as NODE_ENV environment variable
                * debuggingEnabled - controls whether hello built-in debugger is enabled
  
              See https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config for a full list of options
            -->
            <!--<iisnode watchedFiles="web.config;*.js"/>-->
          </system.webServer>
        </configuration>
  
    Si votre application utilise un point d’entrée autre que **app.js**, vous devez remplacer toutes les occurrences de **app.js** avec hello corriger le point d’entrée. Par exemple, vous devez remplacer **app.js** par **server.js**.

> [!NOTE]
> Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications], où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications. Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous avez appris comment toocreate une application de conversation hébergé dans une application web Azure. Vous pouvez également héberger cette application dans le service cloud Azure. Pour obtenir des instructions sur la façon de tooaccomplish, consultez [générer une Application de Chat Node.js avec Socket.IO sur un Service Cloud Azure].

Pour plus d’informations, consultez également hello [centre de développement Node.js].

## <a name="whats-changed"></a>Changements apportés
* Pour un toohello guide voir changer à partir de sites Web tooApp Service : [Azure App Service et son Impact sur les Services Azure existants].

<!-- URL List -->

[Cache Redis Azure]: /documentation/services/redis-cache/
[App Service Web Apps]: http://go.microsoft.com/fwlink/?LinkId=529714
[page de tarification des applications Web]: http://go.microsoft.com/fwlink/?LinkId=511643
[générer une Application de Chat Node.js avec Socket.IO sur un Service Cloud Azure]: ../cloud-services/cloud-services-nodejs-chat-app-socketio.md
[Install and Configure hello Azure CLI]: ../cli-install-nodejs.md
[Azure App Service et son Impact sur les Services Azure existants]: http://go.microsoft.com/fwlink/?LinkId=529714
[centre de développement Node.js]: /develop/nodejs/
[essayez du Service d’applications]: https://azure.microsoft.com/try/app-service/
[Affinité d'instance dans Sites Web Azure]: https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/
[créer un cache dans le Cache Redis Azure]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md

[socket.io-redis]: https://github.com/socketio/socket.io-redis
[référentiel GitHub de Socket.IO]: https://github.com/socketio/socket.io
[ZIP ou GZ archivé version]: https://github.com/socketio/socket.io/releases

<!-- IMG List -->

[chat-example-view]: ./media/web-sites-nodejs-chat-app-socketio/socketio-2.png
[npm-output]: ./media/web-sites-nodejs-chat-app-socketio/socketio-7.png
[completed-app]: ./media/web-sites-nodejs-chat-app-socketio/websitesocketcomplete.png
