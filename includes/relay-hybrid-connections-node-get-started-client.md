### <a name="create-a-nodejs-application"></a>Création d’une application Node.js

Créez un fichier JavaScript appelé `sender.js`.

### <a name="add-hello-relay-npm-package"></a>Ajouter un package de relais NPM hello

Exécutez `npm install hyco-ws` à partir d’une invite de commandes de nœud dans votre dossier de projet.

### <a name="write-some-code-toosend-messages"></a>Écrivez du code toosend messages

1. Ajoutez hello suivant `constants` haut toohello Hello `sender.js` fichier.
   
    ```js
    const WebSocket = require('hyco-ws');
    const readline = require('readline')
        .createInterface({
            input: process.stdin,
            output: process.stdout
        });;
    ```
2. Ajouter hello suivant constantes toohello `sender.js` fichier hello hybride détails de connexion. Remplacez les espaces réservés de hello entre crochets avec les valeurs hello obtenues lors de la création de la connexion hybride hello.
   
   1. `const ns`-hello d’espace de noms de relais. Être toouse vraiment hello complet espace de noms ; par exemple, `{namespace}.servicebus.windows.net`.
   2. `const path`-nom hello de la connexion hybride hello.
   3. `const keyrule`-nom hello de la clé SAS hello.
   4. `const key`-valeur de la clé SAS de hello.

3. Ajouter hello suivant code toohello `sender.js` fichier :
   
    ```js
    WebSocket.relayedConnect(
        WebSocket.createRelaySendUri(ns, path),
        WebSocket.createRelayToken('http://'+ns, keyrule, key),
        function (wss) {
            readline.on('line', (input) => {
                wss.send(input, null);
            });
   
            console.log('Started client interval.');
            wss.on('close', function () {
                console.log('stopping client interval');
                process.exit();
            });
        }
    );
    ```
    Voici à quoi doit ressembler votre fichier sender.js :
   
    ```js
    const WebSocket = require('hyco-ws');
    const readline = require('readline')
        .createInterface({
            input: process.stdin,
            output: process.stdout
        });;
   
    const ns = "{RelayNamespace}";
    const path = "{HybridConnectionName}";
    const keyrule = "{SASKeyName}";
    const key = "{SASKeyValue}";
   
    WebSocket.relayedConnect(
        WebSocket.createRelaySendUri(ns, path),
        WebSocket.createRelayToken('http://'+ns, keyrule, key),
        function (wss) {
            readline.on('line', (input) => {
                wss.send(input, null);
            });
   
            console.log('Started client interval.');
            wss.on('close', function () {
                console.log('stopping client interval');
                process.exit();
            });
        }
    );
    ```

