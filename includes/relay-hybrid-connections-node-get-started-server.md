### <a name="create-a-nodejs-application"></a><span data-ttu-id="21af1-101">Création d’une application Node.js</span><span class="sxs-lookup"><span data-stu-id="21af1-101">Create a Node.js application</span></span>

<span data-ttu-id="21af1-102">Créez un fichier JavaScript appelé `listener.js`.</span><span class="sxs-lookup"><span data-stu-id="21af1-102">Create a new JavaScript file called `listener.js`.</span></span>

### <a name="add-hello-relay-npm-package"></a><span data-ttu-id="21af1-103">Ajouter un package de relais NPM hello</span><span class="sxs-lookup"><span data-stu-id="21af1-103">Add hello Relay NPM package</span></span>

<span data-ttu-id="21af1-104">Exécutez `npm install hyco-ws` à partir d’une invite de commandes de nœud dans votre dossier de projet.</span><span class="sxs-lookup"><span data-stu-id="21af1-104">Run `npm install hyco-ws` from a Node command prompt in your project folder.</span></span>

### <a name="write-some-code-tooreceive-messages"></a><span data-ttu-id="21af1-105">Écrivez du code tooreceive messages</span><span class="sxs-lookup"><span data-stu-id="21af1-105">Write some code tooreceive messages</span></span>

1. <span data-ttu-id="21af1-106">Ajouter hello suivant top constante toohello Hello `listener.js` fichier.</span><span class="sxs-lookup"><span data-stu-id="21af1-106">Add hello following constant toohello top of hello `listener.js` file.</span></span>
   
    ```js
    const WebSocket = require('hyco-ws');
    ```
2. <span data-ttu-id="21af1-107">Ajouter hello suivant constantes toohello `listener.js` fichier hello hybride détails de connexion.</span><span class="sxs-lookup"><span data-stu-id="21af1-107">Add hello following constants toohello `listener.js` file for hello hybrid connection details.</span></span> <span data-ttu-id="21af1-108">Remplacez les espaces réservés de hello entre crochets avec les valeurs hello obtenues lors de la création de la connexion hybride hello.</span><span class="sxs-lookup"><span data-stu-id="21af1-108">Replace hello placeholders in brackets with hello values you obtained when you created hello hybrid connection.</span></span>
   
   1. <span data-ttu-id="21af1-109">`const ns`-hello d’espace de noms de relais.</span><span class="sxs-lookup"><span data-stu-id="21af1-109">`const ns` - hello Relay namespace.</span></span> <span data-ttu-id="21af1-110">Être toouse vraiment hello complet espace de noms ; par exemple, `{namespace}.servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="21af1-110">Be sure toouse hello fully qualified namespace name; for example, `{namespace}.servicebus.windows.net`.</span></span>
   2. <span data-ttu-id="21af1-111">`const path`-nom hello de la connexion hybride hello.</span><span class="sxs-lookup"><span data-stu-id="21af1-111">`const path` - hello name of hello hybrid connection.</span></span>
   3. <span data-ttu-id="21af1-112">`const keyrule`-nom hello de la clé SAS hello.</span><span class="sxs-lookup"><span data-stu-id="21af1-112">`const keyrule` - hello name of hello SAS key.</span></span>
   4. <span data-ttu-id="21af1-113">`const key`-valeur de la clé SAS de hello.</span><span class="sxs-lookup"><span data-stu-id="21af1-113">`const key` - hello SAS key value.</span></span>

3. <span data-ttu-id="21af1-114">Ajouter hello suivant code toohello `listener.js` fichier :</span><span class="sxs-lookup"><span data-stu-id="21af1-114">Add hello following code toohello `listener.js` file:</span></span>
   
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
    <span data-ttu-id="21af1-115">Voici à quoi doit ressembler votre fichier listener.js :</span><span class="sxs-lookup"><span data-stu-id="21af1-115">Here is what your listener.js file should look like:</span></span>
   
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

