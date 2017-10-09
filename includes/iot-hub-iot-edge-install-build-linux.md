## <a name="install-hello-prerequisites"></a><span data-ttu-id="8f14b-101">Installez les composants requis de hello</span><span class="sxs-lookup"><span data-stu-id="8f14b-101">Install hello prerequisites</span></span>

<span data-ttu-id="8f14b-102">Hello dans ce didacticiel suppose que vous utilisez Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="8f14b-102">hello steps in this tutorial assume you are running Ubuntu Linux.</span></span>

<span data-ttu-id="8f14b-103">Ouvrez un interpréteur de commandes et exécutez les hello suivant des packages de composants requis de commandes tooinstall hello :</span><span class="sxs-lookup"><span data-stu-id="8f14b-103">Open a shell and run hello following commands tooinstall hello prerequisite packages:</span></span>

```bash
sudo apt-get update
sudo apt-get install curl build-essential libcurl4-openssl-dev git cmake libssl-dev uuid-dev valgrind libglib2.0-dev libtool autoconf
```

<span data-ttu-id="8f14b-104">Dans l’interface de hello, exécutez hello suivant commande tooclone hello Azure IoT bord GitHub référentiel tooyour ordinateur local :</span><span class="sxs-lookup"><span data-stu-id="8f14b-104">In hello shell, run hello following command tooclone hello Azure IoT Edge GitHub repository tooyour local machine:</span></span>

```bash
git clone https://github.com/Azure/iot-edge.git
```

## <a name="how-toobuild-hello-sample"></a><span data-ttu-id="8f14b-105">Comment toobuild hello exemple</span><span class="sxs-lookup"><span data-stu-id="8f14b-105">How toobuild hello sample</span></span>

<span data-ttu-id="8f14b-106">Vous pouvez à présent générer hello IoT bord runtime et des exemples sur votre ordinateur local :</span><span class="sxs-lookup"><span data-stu-id="8f14b-106">You can now build hello IoT Edge runtime and samples on your local machine:</span></span>

1. <span data-ttu-id="8f14b-107">Ouvrez un interpréteur de commandes.</span><span class="sxs-lookup"><span data-stu-id="8f14b-107">Open a shell.</span></span>

1. <span data-ttu-id="8f14b-108">Exploration du dossier racine de toohello dans votre copie locale de hello **iot-bord** référentiel.</span><span class="sxs-lookup"><span data-stu-id="8f14b-108">Navigate toohello root folder in your local copy of hello **iot-edge** repository.</span></span>

1. <span data-ttu-id="8f14b-109">Exécutez le script de génération comme suit :</span><span class="sxs-lookup"><span data-stu-id="8f14b-109">Run the build script as follows:</span></span>

    ```sh
    tools/build.sh --disable-native-remote-modules
    ```

<span data-ttu-id="8f14b-110">Ce script utilise le **cmake** toocreate utilitaire un dossier appelé **générer** dans le dossier racine de hello de votre copie locale de la **iot-bord** référentiel et générer un makefile.</span><span class="sxs-lookup"><span data-stu-id="8f14b-110">This script uses the **cmake** utility toocreate a folder called **build** in hello root folder of your local copy of the **iot-edge** repository and generate a makefile.</span></span> <span data-ttu-id="8f14b-111">script de Hello génère alors solution hello, ignorer les tests unitaires et tests tooend de fin.</span><span class="sxs-lookup"><span data-stu-id="8f14b-111">hello script then builds hello solution, skipping unit tests and end tooend tests.</span></span> <span data-ttu-id="8f14b-112">Si vous souhaitez toobuild et exécutez des tests unitaires de hello, ajouter hello `--run-unittests` paramètre.</span><span class="sxs-lookup"><span data-stu-id="8f14b-112">If you want toobuild and run hello unit tests, add hello `--run-unittests` parameter.</span></span> <span data-ttu-id="8f14b-113">Si vous souhaitez toobuild et exécutez des tests de tooend fin hello, ajouter hello `--run-e2e-tests`.</span><span class="sxs-lookup"><span data-stu-id="8f14b-113">If you want toobuild and run hello end tooend tests, add hello `--run-e2e-tests`.</span></span>

> [!NOTE]
> <span data-ttu-id="8f14b-114">Chaque fois que vous exécutez hello **build.sh** script, il supprime et recrée ensuite hello **générer** dossier dans le dossier racine de hello de votre copie locale de hello **iot-bord** référentiel.</span><span class="sxs-lookup"><span data-stu-id="8f14b-114">Every time you run hello **build.sh** script, it deletes and then recreates hello **build** folder in hello root folder of your local copy of hello **iot-edge** repository.</span></span>
