## <a name="create-a-simulated-device-app"></a><span data-ttu-id="df956-101">Création d’une application de périphérique simulé</span><span class="sxs-lookup"><span data-stu-id="df956-101">Create a simulated device app</span></span>
<span data-ttu-id="df956-102">Dans cette section, vous allez :</span><span class="sxs-lookup"><span data-stu-id="df956-102">In this section, you:</span></span>

* <span data-ttu-id="df956-103">Créer une application de console Node.js qui répond tooa de méthode directe appelé par le cloud de hello</span><span class="sxs-lookup"><span data-stu-id="df956-103">Create a Node.js console app that responds tooa direct method called by hello cloud</span></span>
* <span data-ttu-id="df956-104">Déclencher une mise à jour du microprogramme simulé</span><span class="sxs-lookup"><span data-stu-id="df956-104">Trigger a simulated firmware update</span></span>
* <span data-ttu-id="df956-105">Hello d’utilisation signalées propriétés tooenable double requêtes tooidentify périphériques et quand ils fin une mise à jour du microprogramme</span><span class="sxs-lookup"><span data-stu-id="df956-105">Use hello reported properties tooenable device twin queries tooidentify devices and when they last completed a firmware update</span></span>

<span data-ttu-id="df956-106">Étape 1 : Créez un dossier vide nommé **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="df956-106">Step 1: Create an empty folder called **manageddevice**.</span></span>  <span data-ttu-id="df956-107">Bonjour **manageddevice** dossier, créez un fichier package.json à l’aide de hello, la commande suivante à l’invite suivante.</span><span class="sxs-lookup"><span data-stu-id="df956-107">In hello **manageddevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="df956-108">Acceptez les valeurs par défaut hello :</span><span class="sxs-lookup"><span data-stu-id="df956-108">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```

<span data-ttu-id="df956-109">Étape 2 : À l’invite de commandes Bonjour **manageddevice** dossier, exécutez hello suivant commande tooinstall hello **azure iot-appareil** et **azure-iot-périphérique-mqtt** périphérique Packages du Kit de développement logiciel :</span><span class="sxs-lookup"><span data-stu-id="df956-109">Step 2: At your command prompt in hello **manageddevice** folder, run hello following command tooinstall hello **azure-iot-device** and **azure-iot-device-mqtt** Device SDK packages:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

<span data-ttu-id="df956-110">Étape 3 : À l’aide d’un éditeur de texte, créez un **dmpatterns_fwupdate_device.js** fichier Bonjour **manageddevice** dossier.</span><span class="sxs-lookup"><span data-stu-id="df956-110">Step 3: Using a text editor, create a **dmpatterns_fwupdate_device.js** file in hello **manageddevice** folder.</span></span>

<span data-ttu-id="df956-111">Étape 4 : Ajouter des instructions au début de hello Hello suivant de hello « exiger » **dmpatterns_fwupdate_device.js** fichier :</span><span class="sxs-lookup"><span data-stu-id="df956-111">Step 4: Add hello following 'require' statements at hello start of hello **dmpatterns_fwupdate_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
<span data-ttu-id="df956-112">Étape 5 : Ajouter un **connectionString** variable et l’utiliser toocreate un **Client** instance.</span><span class="sxs-lookup"><span data-stu-id="df956-112">Step 5: Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span> <span data-ttu-id="df956-113">Remplacez hello `{yourdeviceconnectionstring}` espace réservé avec la chaîne de connexion hello vous avez effectuées précédemment note de dans la section « Créer une identité d’appareil » de hello précédemment :</span><span class="sxs-lookup"><span data-stu-id="df956-113">Replace hello `{yourdeviceconnectionstring}` placeholder with hello connection string you previously made a note of in hello "Create a device identity" section previously:</span></span>
   
    ```
    var connectionString = '{yourdeviceconnectionstring}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

<span data-ttu-id="df956-114">Étape 6 : Ajouter des éléments suivants de hello fonction qui est utilisé tooupdate a signalé des propriétés :</span><span class="sxs-lookup"><span data-stu-id="df956-114">Step 6: Add hello following function that is used tooupdate reported properties:</span></span>
   
    ```
    var reportFWUpdateThroughTwin = function(twin, firmwareUpdateValue) {
      var patch = {
          iothubDM : {
            firmwareUpdate : firmwareUpdateValue
          }
      };
   
      twin.properties.reported.update(patch, function(err) {
        if (err) throw err;
        console.log('twin state reported: ' + firmwareUpdateValue.status);
      });
    };
    ```

<span data-ttu-id="df956-115">Étape 7 : Ajouter hello suivant des fonctions qui simulent le téléchargement et l’application d’image de microprogramme hello :</span><span class="sxs-lookup"><span data-stu-id="df956-115">Step 7: Add hello following functions that simulate downloading and applying hello firmware image:</span></span>
   
    ```
    var simulateDownloadImage = function(imageUrl, callback) {
      var error = null;
      var image = "[fake image data]";
   
      console.log("Downloading image from " + imageUrl);
   
      callback(error, image);
    }
   
    var simulateApplyImage = function(imageData, callback) {
      var error = null;
   
      if (!imageData) {
        error = {message: 'Apply image failed because of missing image data.'};
      }
   
      callback(error);
    }
    ```

<span data-ttu-id="df956-116">Étape 8 : Ajouter hello suivant qu’état de mise à jour de microprogramme de hello mises à jour via hello signalés trop de propriétés de fonction**attente**.</span><span class="sxs-lookup"><span data-stu-id="df956-116">Step 8: Add hello following function that updates hello firmware update status through hello reported properties too**waiting**.</span></span> <span data-ttu-id="df956-117">En règle générale, les périphériques sont informés d’une mise à jour disponible et définies par l’administrateur stratégie provoque hello appareil toostart téléchargement et l’application de mise à jour hello.</span><span class="sxs-lookup"><span data-stu-id="df956-117">Typically, devices are informed of an available update and an administrator defined policy causes hello device toostart downloading and applying hello update.</span></span> <span data-ttu-id="df956-118">Cette fonction est hello où tooenable logique que la stratégie doit s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="df956-118">This function is where hello logic tooenable that policy should run.</span></span> <span data-ttu-id="df956-119">Par souci de simplicité, exemple hello attend que les quatre secondes avant l’image de microprogramme continuer toodownload hello :</span><span class="sxs-lookup"><span data-stu-id="df956-119">For simplicity, hello sample waits for four seconds before proceeding toodownload hello firmware image:</span></span>
   
    ```
    var waitToDownload = function(twin, fwPackageUriVal, callback) {
      var now = new Date();
   
      reportFWUpdateThroughTwin(twin, {
        fwPackageUri: fwPackageUriVal,
        status: 'waiting',
        error : null,
        startedWaitingTime : now.toISOString()
      });
      setTimeout(callback, 4000);
    };
    ```

<span data-ttu-id="df956-120">Étape 9 : Ajouter hello suivant qu’état de mise à jour de microprogramme de hello mises à jour via hello signalés trop de propriétés de fonction**téléchargement**.</span><span class="sxs-lookup"><span data-stu-id="df956-120">Step 9: Add hello following function that updates hello firmware update status through hello reported properties too**downloading**.</span></span> <span data-ttu-id="df956-121">Hello fonction puis simule un téléchargement de microprogramme et enfin les mises à jour hello tooeither de statut de mise à jour de microprogramme **downloadFailed** ou **downloadComplete**:</span><span class="sxs-lookup"><span data-stu-id="df956-121">hello function then simulates a firmware download and finally updates hello firmware update status tooeither **downloadFailed** or **downloadComplete**:</span></span>
   
    ```
    var downloadImage = function(twin, fwPackageUriVal, callback) {
      var now = new Date();   
   
      reportFWUpdateThroughTwin(twin, {
        status: 'downloading',
      });
   
      setTimeout(function() {
        // Simulate download
        simulateDownloadImage(fwPackageUriVal, function(err, image) {
   
          if (err)
          {
            reportFWUpdateThroughTwin(twin, {
              status: 'downloadfailed',
              error: {
                code: error_code,
                message: error_message,
              }
            });
          }
          else {        
            reportFWUpdateThroughTwin(twin, {
              status: 'downloadComplete',
              downloadCompleteTime: now.toISOString(),
            });
   
            setTimeout(function() { callback(image); }, 4000);   
          }
        });
   
      }, 4000);
    }
    ```

<span data-ttu-id="df956-122">Étape 10 : Ajouter hello suivant qu’état de mise à jour de microprogramme de hello mises à jour via hello signalés trop de propriétés de fonction**application**.</span><span class="sxs-lookup"><span data-stu-id="df956-122">Step 10: Add hello following function that updates hello firmware update status through hello reported properties too**applying**.</span></span> <span data-ttu-id="df956-123">Hello fonction puis simule l’image de microprogramme application hello et enfin les mises à jour hello tooeither de statut de mise à jour de microprogramme **applyFailed** ou **applyComplete**:</span><span class="sxs-lookup"><span data-stu-id="df956-123">hello function then simulates applying hello firmware image and finally updates hello firmware update status tooeither **applyFailed** or **applyComplete**:</span></span>
    
    ```
    var applyImage = function(twin, imageData, callback) {
      var now = new Date();   
    
      reportFWUpdateThroughTwin(twin, {
        status: 'applying',
        startedApplyingImage : now.toISOString()
      });
    
      setTimeout(function() {
    
        // Simulate apply firmware image
        simulateApplyImage(imageData, function(err) {
          if (err) {
            reportFWUpdateThroughTwin(twin, {
              status: 'applyFailed',
              error: {
                code: err.error_code,
                message: err.error_message,
              }
            });
          } else { 
            reportFWUpdateThroughTwin(twin, {
              status: 'applyComplete',
              lastFirmwareUpdate: now.toISOString()
            });    
    
          }
        });
    
        setTimeout(callback, 4000);
    
      }, 4000);
    }
    ```

<span data-ttu-id="df956-124">Étape 11 : Ajouter hello fonction suivante que hello handles **firmwareUpdate** méthode directe et lance hello en plusieurs étapes microprogramme des mises à jour :</span><span class="sxs-lookup"><span data-stu-id="df956-124">Step 11: Add hello following function that handles hello **firmwareUpdate** direct method and initiates hello multi-stage firmware update process:</span></span>
    
    ```
    var onFirmwareUpdate = function(request, response) {
    
      // Respond hello cloud app for hello direct method
      response.send(200, 'FirmwareUpdate started', function(err) {
        if (!err) {
          console.error('An error occured when sending a method response:\n' + err.toString());
        } else {
          console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
        }
      });
    
      // Get hello parameter from hello body of hello method request
      var fwPackageUri = request.payload.fwPackageUri;
    
      // Obtain hello device twin
      client.getTwin(function(err, twin) {
        if (err) {
          console.error('Could not get device twin.');
        } else {
          console.log('Device twin acquired.');
    
          // Start hello multi-stage firmware update
          waitToDownload(twin, fwPackageUri, function() {
            downloadImage(twin, fwPackageUri, function(imageData) {
              applyImage(twin, imageData, function() {});    
            });  
          });
    
        }
      });
    }
    ```

<span data-ttu-id="df956-125">Étape 12 : Enfin, ajoutez hello suivant le code qui se connecte tooyour IoT hub :</span><span class="sxs-lookup"><span data-stu-id="df956-125">Step 12: Finally, add hello following code that connects tooyour IoT hub:</span></span>
    
    ```
    client.open(function(err) {
      if (err) {
        console.error('Could not connect tooIotHub client');
      }  else {
        console.log('Client connected tooIoT Hub.  Waiting for firmwareUpdate direct method.');
      }
    
      client.onDeviceMethod('firmwareUpdate', onFirmwareUpdate);
    });
    ```

> [!NOTE]
> <span data-ttu-id="df956-126">tookeep les choses simples, ce didacticiel n’implémente pas de toute stratégie de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="df956-126">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="df956-127">Dans le code de production, vous devez implémenter des stratégies de nouvelle tentative (par exemple, une interruption exponentielle), comme indiqué dans l’article hello [gestion des pannes temporaires](https://msdn.microsoft.com/library/hh675232.aspx).</span><span class="sxs-lookup"><span data-stu-id="df956-127">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling](https://msdn.microsoft.com/library/hh675232.aspx).</span></span>
> 
> 