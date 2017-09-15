### <a name="create-a-nodejs-application"></a><span data-ttu-id="c4521-101">Création d’une application Node.js</span><span class="sxs-lookup"><span data-stu-id="c4521-101">Create a Node.js application</span></span>

<span data-ttu-id="c4521-102">Créez un fichier JavaScript appelé `sender.js`.</span><span class="sxs-lookup"><span data-stu-id="c4521-102">Create a new JavaScript file called `sender.js`.</span></span>

### <a name="add-the-relay-npm-package"></a><span data-ttu-id="c4521-103">Ajout du package NPM de relais</span><span class="sxs-lookup"><span data-stu-id="c4521-103">Add the Relay NPM package</span></span>

<span data-ttu-id="c4521-104">Exécutez `npm install hyco-ws` à partir d’une invite de commandes de nœud dans votre dossier de projet.</span><span class="sxs-lookup"><span data-stu-id="c4521-104">Run `npm install hyco-ws` from a Node command prompt in your project folder.</span></span>

### <a name="write-some-code-to-send-messages"></a><span data-ttu-id="c4521-105">Écriture de code pour envoyer des messages</span><span class="sxs-lookup"><span data-stu-id="c4521-105">Write some code to send messages</span></span>

1. <span data-ttu-id="c4521-106">Ajoutez le `constants` suivant au début du fichier `sender.js`.</span><span class="sxs-lookup"><span data-stu-id="c4521-106">Add the following `constants` to the top of the `sender.js` file.</span></span>
   
    ```js
    const WebSocket = require('hyco-ws');
    const readline = require('readline')
        .createInterface({
            input: process.stdin,
            output: process.stdout
        });;
    ```
2. <span data-ttu-id="c4521-107">Ajoutez les constantes suivantes au fichier `sender.js` pour les détails de la connexion hybride.</span><span class="sxs-lookup"><span data-stu-id="c4521-107">Add the following constants to the `sender.js` file for the hybrid connection details.</span></span> <span data-ttu-id="c4521-108">Remplacez les espaces réservés entre crochets par les valeurs obtenues lors de la création de la connexion hybride.</span><span class="sxs-lookup"><span data-stu-id="c4521-108">Replace the placeholders in brackets with the values you obtained when you created the hybrid connection.</span></span>
   
   1. <span data-ttu-id="c4521-109">`const ns` - L’espace de noms du relais.</span><span class="sxs-lookup"><span data-stu-id="c4521-109">`const ns` - The Relay namespace.</span></span> <span data-ttu-id="c4521-110">Veillez à utiliser le nom de l’espace de noms complet, par exemple `{namespace}.servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="c4521-110">Be sure to use the fully qualified namespace name; for example, `{namespace}.servicebus.windows.net`.</span></span>
   2. <span data-ttu-id="c4521-111">`const path` - Le nom de la connexion hybride.</span><span class="sxs-lookup"><span data-stu-id="c4521-111">`const path` - The name of the hybrid connection.</span></span>
   3. <span data-ttu-id="c4521-112">`const keyrule` - Le nom de la clé SAS.</span><span class="sxs-lookup"><span data-stu-id="c4521-112">`const keyrule` - The name of the SAS key.</span></span>
   4. <span data-ttu-id="c4521-113">`const key` - La valeur de la clé SAS.</span><span class="sxs-lookup"><span data-stu-id="c4521-113">`const key` - The SAS key value.</span></span>

3. <span data-ttu-id="c4521-114">Ajoutez le code suivant au fichier `sender.js` :</span><span class="sxs-lookup"><span data-stu-id="c4521-114">Add the following code to the `sender.js` file:</span></span>
   
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
    <span data-ttu-id="c4521-115">Voici à quoi doit ressembler votre fichier sender.js :</span><span class="sxs-lookup"><span data-stu-id="c4521-115">Here is what your sender.js file should look like:</span></span>
   
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

