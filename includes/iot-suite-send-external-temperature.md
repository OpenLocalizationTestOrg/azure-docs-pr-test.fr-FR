## <a name="configure-hello-nodejs-simulated-device"></a>Configurer l’appareil simulé de hello Node.js
1. Tableau de bord de surveillance à distance hello, cliquez sur **+ ajouter un périphérique** , puis ajoutez un *périphérique personnalisé*. Prenez note de hello IoT Hub nom d’hôte, l’id et clé de périphérique. Vous avez besoin plus loin dans ce didacticiel lorsque vous préparez l’application de client de périphérique de remote_monitoring.js hello.
2. Assurez-vous que Node.js version 0.12.x ou ultérieure est installé sur votre ordinateur de développement. Exécutez `node --version` à une invite de commandes ou dans une version de hello toocheck shell. Pour plus d’informations sur l’utilisation d’un tooinstall de gestionnaire de package Node.js sur Linux, consultez [l’installation de Node.js via le Gestionnaire de package][node-linux].
3. Lorsque vous avez installé Node.js, cloner la version la plus récente de hello hello [azure iot-sdk-nœud] [ lnk-github-repo] ordinateur de développement tooyour de référentiel. Utilisez toujours hello **master** branche pour la version la plus récente des bibliothèques de hello et des exemples hello.
4. À partir de votre copie locale de hello [azure iot-sdk-nœud] [ lnk-github-repo] référentiel, hello copie suivant de deux fichiers à partir du dossier vide hello dossier nœud/périphérique/samples tooan sur votre ordinateur de développement :
   
   * packages.json
   * remote_monitoring.js
5. Ouvrir le fichier de remote_monitoring.js hello et recherchez hello après la définition de la variable :
   
    ```
    var connectionString = "[IoT Hub device connection string]";
    ```
6. Remplacez **[chaîne de connexion d’un périphérique de IoT Hub]** par votre chaîne de connexion de périphérique. Utilisez les valeurs hello pour votre nom d’hôte IoT Hub, id de périphérique et la clé de périphérique que vous avez notée à l’étape 1. Une chaîne de connexion de périphérique a hello suivant le format :
   
    ```
    HostName={your IoT Hub hostname};DeviceId={your device id};SharedAccessKey={your device key}
    ```
   
    Si votre nom d’hôte du IoT Hub est **contoso** et id de votre appareil est **mydevice**, votre chaîne de connexion ressemble à hello suivant extrait de code :
   
    ```
    var connectionString = "HostName=contoso.azure-devices.net;DeviceId=mydevice;SharedAccessKey=2s ... =="
    ```
7. Enregistrez le fichier de hello. Exécutez hello suivant les commandes dans un interpréteur de commandes ou d’une invite de commandes dans le dossier hello contenant ces fichiers tooinstall hello les packages, puis exécutez exemple d’application hello :
   
    ```
    npm install
    node remote_monitoring.js
    ```

## <a name="observe-dynamic-telemetry-in-action"></a>Observer la télémétrie dynamique en action
tableau de bord de Hello affiche la télémétrie de température et humidité hello à partir d’appareils simulée de hello existant :

![tableau de bord par défaut Hello][image1]

Si vous sélectionnez les appareil simulé Node.js hello que vous avez exécuté dans la section précédente de hello, vous consultez température et humidité télémétrie de température externe :

![Ajouter le tableau de bord toohello température externe][image2]

solution de surveillance à distance Hello détecte le type de données de télémétrie de température externe supplémentaire hello automatiquement et l’ajoute toohello graphique sur le tableau de bord hello.

[node-linux]: https://github.com/nodejs/node-v0.x-archive/wiki/Installing-Node.js-via-package-manager
[lnk-github-repo]: https://github.com/Azure/azure-iot-sdk-node
[image1]: media/iot-suite-send-external-temperature/image1.png
[image2]: media/iot-suite-send-external-temperature/image2.png