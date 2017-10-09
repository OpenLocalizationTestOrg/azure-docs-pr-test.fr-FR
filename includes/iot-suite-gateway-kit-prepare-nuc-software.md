## <a name="build-iot-edge"></a>Générer IoT Edge

Ce didacticiel utilise toocommunicate de modules personnalisé IoT Edge avec hello solution préconfigurée de surveillance à distance. Par conséquent, vous devez les modules toobuild hello IoT bord à partir du code source personnalisée. Hello les sections suivantes décrire comment tooinstall IoT Edge et build hello module IoT bord personnalisé.

### <a name="install-iot-edge"></a>Installer IoT Edge

Hello étapes suivantes décrivent comment tooinstall hello compilé préalable logiciel IoT Edge sur hello Intel NUC :

1. Configurez les référentiels de package actives hello requis en exécutant les hello suivant de commandes de hello Intel NUC :

    ```bash
    smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
    smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
    ```

    Entrez `y` lorsque hello commande vous demande trop**inclure ce canal ?**.

1. Mise à jour hello actives Gestionnaire de package en exécutant hello de commande suivante :

    ```bash
    smart update
    ```

1. Installer le package de Azure IoT Edge de hello en exécutant hello de commande suivante :

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```

1. Vérifier l’installation de hello par exemple hello « Hello world ». Cet exemple écrit un fichier de hello world message toohello log.txT toutes les cinq secondes. Hello exécuter les commandes suivantes hello, exemple « Hello world » :

    ```bash
    cd /usr/share/azureiotgatewaysdk/samples/hello_world/
    ./hello_world hello_world.json
    ```

    Ignorer les **argument non valide** lorsque vous arrêtez l’exemple hello des messages.

    Utilisez hello suivant le contenu de hello tooview de commande du fichier journal de hello :

    ```bash
    cat log.txt | more
    ```

### <a name="troubleshooting"></a>Résolution des problèmes

Si vous recevez une erreur de hello « aucun package ne fournit util-linux-dev », essayez de redémarrer hello NUC d’Intel.
