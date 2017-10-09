## <a name="install-hello-prerequisites"></a><span data-ttu-id="854a0-101">Installez les composants requis de hello</span><span class="sxs-lookup"><span data-stu-id="854a0-101">Install hello prerequisites</span></span>

1. <span data-ttu-id="854a0-102">Installez [Visual Studio 2015 ou 2017](https://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="854a0-102">Install [Visual Studio 2015 or 2017](https://www.visualstudio.com).</span></span> <span data-ttu-id="854a0-103">Vous pouvez utiliser hello libre Community Edition si vous répondez aux conditions de licence hello.</span><span class="sxs-lookup"><span data-stu-id="854a0-103">You can use hello free Community Edition if you meet hello licensing requirements.</span></span> <span data-ttu-id="854a0-104">Être tooinclude que Visual C++ et le Gestionnaire de Package NuGet.</span><span class="sxs-lookup"><span data-stu-id="854a0-104">Be sure tooinclude Visual C++ and NuGet Package Manager.</span></span>

1. <span data-ttu-id="854a0-105">Installer [git](http://www.git-scm.com) et assurez-vous que vous pouvez exécuter git.exe à partir de la ligne de commande hello.</span><span class="sxs-lookup"><span data-stu-id="854a0-105">Install [git](http://www.git-scm.com) and make sure you can run git.exe from hello command line.</span></span>

1. <span data-ttu-id="854a0-106">Installer [CMake](https://cmake.org/download/) et assurez-vous que vous pouvez exécuter cmake.exe à partir de la ligne de commande hello.</span><span class="sxs-lookup"><span data-stu-id="854a0-106">Install [CMake](https://cmake.org/download/) and make sure you can run cmake.exe from hello command line.</span></span> <span data-ttu-id="854a0-107">CMake version 3.7.2 ou supérieure est recommandé.</span><span class="sxs-lookup"><span data-stu-id="854a0-107">CMake version 3.7.2 or later is recommended.</span></span> <span data-ttu-id="854a0-108">Hello **.msi** programme d’installation est l’option la plus simple hello sur Windows.</span><span class="sxs-lookup"><span data-stu-id="854a0-108">hello **.msi** installer is hello easiest option on Windows.</span></span> <span data-ttu-id="854a0-109">Ajouter CMake toohello chemin d’accès pour hello au moins l’utilisateur actuel lorsque le programme d’installation hello vous invite.</span><span class="sxs-lookup"><span data-stu-id="854a0-109">Add CMake toohello PATH for at least hello current user when hello installer prompts you.</span></span>

1. <span data-ttu-id="854a0-110">Installez [Python 2.7](https://www.python.org/downloads/release/python-27).</span><span class="sxs-lookup"><span data-stu-id="854a0-110">Install [Python 2.7](https://www.python.org/downloads/release/python-27).</span></span> <span data-ttu-id="854a0-111">Assurez-vous que vous ajoutez Python tooyour `PATH` variable d’environnement dans **le panneau de configuration -> système -> Avancé paramètres système -> Variables d’environnement**.</span><span class="sxs-lookup"><span data-stu-id="854a0-111">Make sure you add Python tooyour `PATH` environment variable in **Control Panel -> System -> Advanced system settings -> Environment Variables**.</span></span>

1. <span data-ttu-id="854a0-112">À l’invite de commandes, exécutez hello suivant commande tooclone hello Azure IoT bord GitHub référentiel tooyour ordinateur local :</span><span class="sxs-lookup"><span data-stu-id="854a0-112">At a command prompt, run hello following command tooclone hello Azure IoT Edge GitHub repository tooyour local machine:</span></span>

    ```cmd
    git clone https://github.com/Azure/iot-edge.git
    ```

## <a name="how-toobuild-hello-sample"></a><span data-ttu-id="854a0-113">Comment toobuild hello exemple</span><span class="sxs-lookup"><span data-stu-id="854a0-113">How toobuild hello sample</span></span>

<span data-ttu-id="854a0-114">Vous pouvez à présent générer hello IoT bord runtime et des exemples sur votre ordinateur local :</span><span class="sxs-lookup"><span data-stu-id="854a0-114">You can now build hello IoT Edge runtime and samples on your local machine:</span></span>

1. <span data-ttu-id="854a0-115">Ouvrez une **invite de commandes développeur pour VS 2015** ou une **invite de commandes développeur pour VS 2017**.</span><span class="sxs-lookup"><span data-stu-id="854a0-115">Open a **Developer Command Prompt for VS 2015** or **Developer Command Prompt for VS 2017** command prompt.</span></span>

1. <span data-ttu-id="854a0-116">Exploration du dossier racine de toohello dans votre copie locale de hello **iot-bord** référentiel.</span><span class="sxs-lookup"><span data-stu-id="854a0-116">Navigate toohello root folder in your local copy of hello **iot-edge** repository.</span></span>

1. <span data-ttu-id="854a0-117">Exécutez le script de génération comme suit :</span><span class="sxs-lookup"><span data-stu-id="854a0-117">Run the build script as follows:</span></span>

    ```cmd
    tools\build.cmd --disable-native-remote-modules
    ```

<span data-ttu-id="854a0-118">Ce script crée un fichier de solution Visual Studio et génère hello solution.</span><span class="sxs-lookup"><span data-stu-id="854a0-118">This script creates a Visual Studio solution file and builds hello solution.</span></span> <span data-ttu-id="854a0-119">Vous pouvez trouver des solutions de Visual Studio hello Bonjour **générer** dossier dans votre copie locale de hello **iot-bord** référentiel.</span><span class="sxs-lookup"><span data-stu-id="854a0-119">You can find hello Visual Studio solution in hello **build** folder in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="854a0-120">Si vous souhaitez toobuild et exécutez des tests unitaires de hello, ajouter hello `--run-unittests` paramètre.</span><span class="sxs-lookup"><span data-stu-id="854a0-120">If you want toobuild and run hello unit tests, add hello `--run-unittests` parameter.</span></span> <span data-ttu-id="854a0-121">Si vous souhaitez toobuild et exécutez des tests de tooend fin hello, ajouter hello `--run-e2e-tests`.</span><span class="sxs-lookup"><span data-stu-id="854a0-121">If you want toobuild and run hello end tooend tests, add hello `--run-e2e-tests`.</span></span>

> [!NOTE]
> <span data-ttu-id="854a0-122">Chaque fois que vous exécutez hello **build.cmd** script, il supprime et recrée ensuite hello **générer** dossier dans le dossier racine de hello de votre copie locale de hello **iot-bord** référentiel.</span><span class="sxs-lookup"><span data-stu-id="854a0-122">Every time you run hello **build.cmd** script, it deletes and then recreates hello **build** folder in hello root folder of your local copy of hello **iot-edge** repository.</span></span>
