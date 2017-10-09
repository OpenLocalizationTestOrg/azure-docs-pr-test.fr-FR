### <a name="create-a-nodejs-application"></a><span data-ttu-id="e2843-101">Création d’une application Node.js</span><span class="sxs-lookup"><span data-stu-id="e2843-101">Create a Node.js application</span></span>

<span data-ttu-id="e2843-102">Créez un fichier JavaScript appelé `sender.js`.</span><span class="sxs-lookup"><span data-stu-id="e2843-102">Create a new JavaScript file called `sender.js`.</span></span>

### <a name="add-hello-relay-npm-package"></a><span data-ttu-id="e2843-103">Ajouter un package de relais NPM hello</span><span class="sxs-lookup"><span data-stu-id="e2843-103">Add hello Relay NPM package</span></span>

<span data-ttu-id="e2843-104">Exécutez `npm install hyco-ws` à partir d’une invite de commandes de nœud dans votre dossier de projet.</span><span class="sxs-lookup"><span data-stu-id="e2843-104">Run `npm install hyco-ws` from a Node command prompt in your project folder.</span></span>

### <a name="write-some-code-toosend-messages"></a><span data-ttu-id="e2843-105">Écrivez du code toosend messages</span><span class="sxs-lookup"><span data-stu-id="e2843-105">Write some code toosend messages</span></span>

1. <span data-ttu-id="e2843-106">Ajoutez hello suivant `constants` haut toohello Hello `sender.js` fichier.</span><span class="sxs-lookup"><span data-stu-id="e2843-106">Add hello following `constants` toohello top of hello `sender.js` file.</span></span>
   
    ```js
    const WebSocket = require('hyco-ws');
    const readline = require('readline')
        .createInterface({
            input: process.stdin,
            output: process.stdout
        });;
    ```
2. <span data-ttu-id="e2843-107">Ajouter hello suivant constantes toohello `sender.js` fichier hello hybride détails de connexion.</span><span class="sxs-lookup"><span data-stu-id="e2843-107">Add hello following constants toohello `sender.js` file for hello hybrid connection details.</span></span> <span data-ttu-id="e2843-108">Remplacez les espaces réservés de hello entre crochets avec les valeurs hello obtenues lors de la création de la connexion hybride hello.</span><span class="sxs-lookup"><span data-stu-id="e2843-108">Replace hello placeholders in brackets with hello values you obtained when you created hello hybrid connection.</span></span>
   
   1. <span data-ttu-id="e2843-109">`const ns`-hello d’espace de noms de relais.</span><span class="sxs-lookup"><span data-stu-id="e2843-109">`const ns` - hello Relay namespace.</span></span> <span data-ttu-id="e2843-110">Être toouse vraiment hello complet espace de noms ; par exemple, `{namespace}.servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="e2843-110">Be sure toouse hello fully qualified namespace name; for example, `{namespace}.servicebus.windows.net`.</span></span>
   2. <span data-ttu-id="e2843-111">`const path`-nom hello de la connexion hybride hello.</span><span class="sxs-lookup"><span data-stu-id="e2843-111">`const path` - hello name of hello hybrid connection.</span></span>
   3. <span data-ttu-id="e2843-112">`const keyrule`-nom hello de la clé SAS hello.</span><span class="sxs-lookup"><span data-stu-id="e2843-112">`const keyrule` - hello name of hello SAS key.</span></span>
   4. <span data-ttu-id="e2843-113">`const key`-valeur de la clé SAS de hello.</span><span class="sxs-lookup"><span data-stu-id="e2843-113">`const key` - hello SAS key value.</span></span>

3. <span data-ttu-id="e2843-114">Ajouter hello suivant code toohello `sender.js` fichier :</span><span class="sxs-lookup"><span data-stu-id="e2843-114">Add hello following code toohello `sender.js` file:</span></span>
   
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
    <span data-ttu-id="e2843-115">Voici à quoi doit ressembler votre fichier sender.js :</span><span class="sxs-lookup"><span data-stu-id="e2843-115">Here is what your sender.js file should look like:</span></span>
   
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

