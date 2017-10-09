### <a name="create-a-nodejs-application"></a>Création d’une application Node.js

Créez un fichier JavaScript appelé `listener.js`.

### <a name="add-hello-relay-npm-package"></a>Ajouter un package de relais NPM hello

Exécutez `npm install hyco-ws` à partir d’une invite de commandes de nœud dans votre dossier de projet.

### <a name="write-some-code-tooreceive-messages"></a>Écrivez du code tooreceive messages

1. Ajouter hello suivant top constante toohello Hello `listener.js` fichier.
   
    ```js
    const WebSocket = require('hyco-ws');
    ```
2. Ajouter hello suivant constantes toohello `listener.js` fichier hello hybride détails de connexion. Remplacez les espaces réservés de hello entre crochets avec les valeurs hello obtenues lors de la création de la connexion hybride hello.
   
   1. `const ns`-hello d’espace de noms de relais. Être toouse vraiment hello complet espace de noms ; par exemple, `{namespace}.servicebus.windows.net`.
   2. `const path`-nom hello de la connexion hybride hello.
   3. `const keyrule`-nom hello de la clé SAS hello.
   4. `const key`-valeur de la clé SAS de hello.

3. Ajouter hello suivant code toohello `listener.js` fichier :
   
    ```js
    var wss = WebSocket.createRelayedServer(
    {
        server : WebSocket.createRelayListenUri(ns, path),
        token: WebSocket.createRelayToken('http://' + ns, keyrule, key)
    }, 
    function (ws) {
        console.log('connection accepted');
        ws.onmessage = function (event) {
            console.log(event.data);
        };
        ws.on('close', function () {
            console.log('connection closed');
        });       
    });
   
    console.log('listening');
   
    wss.on('error', function(err) {
        console.log('error' + err);
    });
    ```
    Voici à quoi doit ressembler votre fichier listener.js :
   
    ```js
    const WebSocket = require('hyco-ws');
   
    const ns = "{RelayNamespace}";
    const path = "{HybridConnectionName}";
    const keyrule = "{SASKeyName}";
    const key = "{SASKeyValue}";
   
    var wss = WebSocket.createRelayedServer(
        {
            server : WebSocket.createRelayListenUri(ns, path),
            token: WebSocket.createRelayToken('http://' + ns, keyrule, key)
        }, 
        function (ws) {
            console.log('connection accepted');
            ws.onmessage = function (event) {
                console.log(event.data);
            };
            ws.on('close', function () {
                console.log('connection closed');
            });       
    });
   
    console.log('listening');
   
    wss.on('error', function(err) {
        console.log('error' + err);
    });
    ```

