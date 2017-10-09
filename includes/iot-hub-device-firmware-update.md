## <a name="create-a-simulated-device-app"></a>Création d’une application de périphérique simulé
Dans cette section, vous allez :

* Créer une application de console Node.js qui répond tooa de méthode directe appelé par le cloud de hello
* Déclencher une mise à jour du microprogramme simulé
* Hello d’utilisation signalées propriétés tooenable double requêtes tooidentify périphériques et quand ils fin une mise à jour du microprogramme

Étape 1 : Créez un dossier vide nommé **manageddevice**.  Bonjour **manageddevice** dossier, créez un fichier package.json à l’aide de hello, la commande suivante à l’invite suivante. Acceptez les valeurs par défaut hello :
   
    ```
    npm init
    ```

Étape 2 : À l’invite de commandes Bonjour **manageddevice** dossier, exécutez hello suivant commande tooinstall hello **azure iot-appareil** et **azure-iot-périphérique-mqtt** périphérique Packages du Kit de développement logiciel :
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

Étape 3 : À l’aide d’un éditeur de texte, créez un **dmpatterns_fwupdate_device.js** fichier Bonjour **manageddevice** dossier.

Étape 4 : Ajouter des instructions au début de hello Hello suivant de hello « exiger » **dmpatterns_fwupdate_device.js** fichier :
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
Étape 5 : Ajouter un **connectionString** variable et l’utiliser toocreate un **Client** instance. Remplacez hello `{yourdeviceconnectionstring}` espace réservé avec la chaîne de connexion hello vous avez effectuées précédemment note de dans la section « Créer une identité d’appareil » de hello précédemment :
   
    ```
    var connectionString = '{yourdeviceconnectionstring}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

Étape 6 : Ajouter des éléments suivants de hello fonction qui est utilisé tooupdate a signalé des propriétés :
   
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

Étape 7 : Ajouter hello suivant des fonctions qui simulent le téléchargement et l’application d’image de microprogramme hello :
   
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

Étape 8 : Ajouter hello suivant qu’état de mise à jour de microprogramme de hello mises à jour via hello signalés trop de propriétés de fonction**attente**. En règle générale, les périphériques sont informés d’une mise à jour disponible et définies par l’administrateur stratégie provoque hello appareil toostart téléchargement et l’application de mise à jour hello. Cette fonction est hello où tooenable logique que la stratégie doit s’exécuter. Par souci de simplicité, exemple hello attend que les quatre secondes avant l’image de microprogramme continuer toodownload hello :
   
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

Étape 9 : Ajouter hello suivant qu’état de mise à jour de microprogramme de hello mises à jour via hello signalés trop de propriétés de fonction**téléchargement**. Hello fonction puis simule un téléchargement de microprogramme et enfin les mises à jour hello tooeither de statut de mise à jour de microprogramme **downloadFailed** ou **downloadComplete**:
   
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

Étape 10 : Ajouter hello suivant qu’état de mise à jour de microprogramme de hello mises à jour via hello signalés trop de propriétés de fonction**application**. Hello fonction puis simule l’image de microprogramme application hello et enfin les mises à jour hello tooeither de statut de mise à jour de microprogramme **applyFailed** ou **applyComplete**:
    
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

Étape 11 : Ajouter hello fonction suivante que hello handles **firmwareUpdate** méthode directe et lance hello en plusieurs étapes microprogramme des mises à jour :
    
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

Étape 12 : Enfin, ajoutez hello suivant le code qui se connecte tooyour IoT hub :
    
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
> tookeep les choses simples, ce didacticiel n’implémente pas de toute stratégie de nouvelle tentative. Dans le code de production, vous devez implémenter des stratégies de nouvelle tentative (par exemple, une interruption exponentielle), comme indiqué dans l’article hello [gestion des pannes temporaires](https://msdn.microsoft.com/library/hh675232.aspx).
> 
> 