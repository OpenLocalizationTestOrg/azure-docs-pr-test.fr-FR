## <a name="install-the-prerequisites"></a><span data-ttu-id="85923-101">Installer les composants requis</span><span class="sxs-lookup"><span data-stu-id="85923-101">Install the prerequisites</span></span>

1. <span data-ttu-id="85923-102">Installez [Visual Studio 2015 ou 2017](https://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="85923-102">Install [Visual Studio 2015 or 2017](https://www.visualstudio.com).</span></span> <span data-ttu-id="85923-103">Vous pouvez utiliser l’édition Community gratuite si vous remplissez les conditions de licence.</span><span class="sxs-lookup"><span data-stu-id="85923-103">You can use the free Community Edition if you meet the licensing requirements.</span></span> <span data-ttu-id="85923-104">Veillez à inclure Visual C++ et le gestionnaire de package NuGet.</span><span class="sxs-lookup"><span data-stu-id="85923-104">Be sure to include Visual C++ and NuGet Package Manager.</span></span>

1. <span data-ttu-id="85923-105">Installez [git](http://www.git-scm.com) et vérifiez que vous pouvez exécuter le fichier git.exe à partir de la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="85923-105">Install [git](http://www.git-scm.com) and make sure you can run git.exe from the command line.</span></span>

1. <span data-ttu-id="85923-106">Installez [CMake](https://cmake.org/download/) et vérifiez que vous pouvez exécuter le fichier cmake.exe à partir de la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="85923-106">Install [CMake](https://cmake.org/download/) and make sure you can run cmake.exe from the command line.</span></span> <span data-ttu-id="85923-107">CMake version 3.7.2 ou supérieure est recommandé.</span><span class="sxs-lookup"><span data-stu-id="85923-107">CMake version 3.7.2 or later is recommended.</span></span> <span data-ttu-id="85923-108">Le programme d’installation **.msi** est l’option la plus simple sous Windows.</span><span class="sxs-lookup"><span data-stu-id="85923-108">The **.msi** installer is the easiest option on Windows.</span></span> <span data-ttu-id="85923-109">Ajoutez CMake au chemin d’accès au moins pour l’utilisateur actif lorsque le programme d’installation vous y invite.</span><span class="sxs-lookup"><span data-stu-id="85923-109">Add CMake to the PATH for at least the current user when the installer prompts you.</span></span>

1. <span data-ttu-id="85923-110">Installez [Python 2.7](https://www.python.org/downloads/release/python-27).</span><span class="sxs-lookup"><span data-stu-id="85923-110">Install [Python 2.7](https://www.python.org/downloads/release/python-27).</span></span> <span data-ttu-id="85923-111">Veillez à ajouter Python à votre variable d’environnement `PATH` dans **Panneau de configuration -> Système -> Paramètres système avancés -> Variables d’environnement**.</span><span class="sxs-lookup"><span data-stu-id="85923-111">Make sure you add Python to your `PATH` environment variable in **Control Panel -> System -> Advanced system settings -> Environment Variables**.</span></span>

1. <span data-ttu-id="85923-112">À l’invite de commande, exécutez la commande suivante pour cloner le référentiel GitHub d’Azure IoT Edge sur l’ordinateur local :</span><span class="sxs-lookup"><span data-stu-id="85923-112">At a command prompt, run the following command to clone the Azure IoT Edge GitHub repository to your local machine:</span></span>

    ```cmd
    git clone https://github.com/Azure/iot-edge.git
    ```

## <a name="how-to-build-the-sample"></a><span data-ttu-id="85923-113">Comment créer l'exemple</span><span class="sxs-lookup"><span data-stu-id="85923-113">How to build the sample</span></span>

<span data-ttu-id="85923-114">Vous pouvez désormais créer le runtime et les exemples IoT Edge sur l’ordinateur local :</span><span class="sxs-lookup"><span data-stu-id="85923-114">You can now build the IoT Edge runtime and samples on your local machine:</span></span>

1. <span data-ttu-id="85923-115">Ouvrez une **invite de commandes développeur pour VS 2015** ou une **invite de commandes développeur pour VS 2017**.</span><span class="sxs-lookup"><span data-stu-id="85923-115">Open a **Developer Command Prompt for VS 2015** or **Developer Command Prompt for VS 2017** command prompt.</span></span>

1. <span data-ttu-id="85923-116">Accédez au dossier racine de votre copie locale du référentiel **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="85923-116">Navigate to the root folder in your local copy of the **iot-edge** repository.</span></span>

1. <span data-ttu-id="85923-117">Exécutez le script de génération comme suit :</span><span class="sxs-lookup"><span data-stu-id="85923-117">Run the build script as follows:</span></span>

    ```cmd
    tools\build.cmd --disable-native-remote-modules
    ```

<span data-ttu-id="85923-118">Ce script crée un fichier de solution Visual Studio et génère la solution.</span><span class="sxs-lookup"><span data-stu-id="85923-118">This script creates a Visual Studio solution file and builds the solution.</span></span> <span data-ttu-id="85923-119">Vous trouverez la solution Visual Studio dans le dossier **build** de votre copie locale du référentiel **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="85923-119">You can find the Visual Studio solution in the **build** folder in your local copy of the **iot-edge** repository.</span></span> <span data-ttu-id="85923-120">Pour générer et exécuter les tests unitaires, ajoutez le paramètre `--run-unittests`.</span><span class="sxs-lookup"><span data-stu-id="85923-120">If you want to build and run the unit tests, add the `--run-unittests` parameter.</span></span> <span data-ttu-id="85923-121">Pour générer et exécuter les tests de bout en bout, ajoutez le paramètre `--run-e2e-tests`.</span><span class="sxs-lookup"><span data-stu-id="85923-121">If you want to build and run the end to end tests, add the `--run-e2e-tests`.</span></span>

> [!NOTE]
> <span data-ttu-id="85923-122">Chaque fois que vous exécutez le script **build.cmd**, celui-ci supprime et recrée le dossier **build** dans le dossier racine de votre copie locale du référentiel **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="85923-122">Every time you run the **build.cmd** script, it deletes and then recreates the **build** folder in the root folder of your local copy of the **iot-edge** repository.</span></span>