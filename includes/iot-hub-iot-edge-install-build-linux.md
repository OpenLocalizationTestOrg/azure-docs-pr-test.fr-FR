## <a name="install-hello-prerequisites"></a>Installez les composants requis de hello

Hello dans ce didacticiel suppose que vous utilisez Ubuntu Linux.

Ouvrez un interpréteur de commandes et exécutez les hello suivant des packages de composants requis de commandes tooinstall hello :

```bash
sudo apt-get update
sudo apt-get install curl build-essential libcurl4-openssl-dev git cmake libssl-dev uuid-dev valgrind libglib2.0-dev libtool autoconf
```

Dans l’interface de hello, exécutez hello suivant commande tooclone hello Azure IoT bord GitHub référentiel tooyour ordinateur local :

```bash
git clone https://github.com/Azure/iot-edge.git
```

## <a name="how-toobuild-hello-sample"></a>Comment toobuild hello exemple

Vous pouvez à présent générer hello IoT bord runtime et des exemples sur votre ordinateur local :

1. Ouvrez un interpréteur de commandes.

1. Exploration du dossier racine de toohello dans votre copie locale de hello **iot-bord** référentiel.

1. Exécutez le script de génération comme suit :

    ```sh
    tools/build.sh --disable-native-remote-modules
    ```

Ce script utilise le **cmake** toocreate utilitaire un dossier appelé **générer** dans le dossier racine de hello de votre copie locale de la **iot-bord** référentiel et générer un makefile. script de Hello génère alors solution hello, ignorer les tests unitaires et tests tooend de fin. Si vous souhaitez toobuild et exécutez des tests unitaires de hello, ajouter hello `--run-unittests` paramètre. Si vous souhaitez toobuild et exécutez des tests de tooend fin hello, ajouter hello `--run-e2e-tests`.

> [!NOTE]
> Chaque fois que vous exécutez hello **build.sh** script, il supprime et recrée ensuite hello **générer** dossier dans le dossier racine de hello de votre copie locale de hello **iot-bord** référentiel.
