## <a name="install-hello-prerequisites"></a>Installez les composants requis de hello

1. Installez [Visual Studio 2015 ou 2017](https://www.visualstudio.com). Vous pouvez utiliser hello libre Community Edition si vous répondez aux conditions de licence hello. Être tooinclude que Visual C++ et le Gestionnaire de Package NuGet.

1. Installer [git](http://www.git-scm.com) et assurez-vous que vous pouvez exécuter git.exe à partir de la ligne de commande hello.

1. Installer [CMake](https://cmake.org/download/) et assurez-vous que vous pouvez exécuter cmake.exe à partir de la ligne de commande hello. CMake version 3.7.2 ou supérieure est recommandé. Hello **.msi** programme d’installation est l’option la plus simple hello sur Windows. Ajouter CMake toohello chemin d’accès pour hello au moins l’utilisateur actuel lorsque le programme d’installation hello vous invite.

1. Installez [Python 2.7](https://www.python.org/downloads/release/python-27). Assurez-vous que vous ajoutez Python tooyour `PATH` variable d’environnement dans **le panneau de configuration -> système -> Avancé paramètres système -> Variables d’environnement**.

1. À l’invite de commandes, exécutez hello suivant commande tooclone hello Azure IoT bord GitHub référentiel tooyour ordinateur local :

    ```cmd
    git clone https://github.com/Azure/iot-edge.git
    ```

## <a name="how-toobuild-hello-sample"></a>Comment toobuild hello exemple

Vous pouvez à présent générer hello IoT bord runtime et des exemples sur votre ordinateur local :

1. Ouvrez une **invite de commandes développeur pour VS 2015** ou une **invite de commandes développeur pour VS 2017**.

1. Exploration du dossier racine de toohello dans votre copie locale de hello **iot-bord** référentiel.

1. Exécutez le script de génération comme suit :

    ```cmd
    tools\build.cmd --disable-native-remote-modules
    ```

Ce script crée un fichier de solution Visual Studio et génère hello solution. Vous pouvez trouver des solutions de Visual Studio hello Bonjour **générer** dossier dans votre copie locale de hello **iot-bord** référentiel. Si vous souhaitez toobuild et exécutez des tests unitaires de hello, ajouter hello `--run-unittests` paramètre. Si vous souhaitez toobuild et exécutez des tests de tooend fin hello, ajouter hello `--run-e2e-tests`.

> [!NOTE]
> Chaque fois que vous exécutez hello **build.cmd** script, il supprime et recrée ensuite hello **générer** dossier dans le dossier racine de hello de votre copie locale de hello **iot-bord** référentiel.
