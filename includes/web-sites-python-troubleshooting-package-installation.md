<span data-ttu-id="4d3fb-101">Il est possible que certains packages ne soient pas installés via pip sous Azure.</span><span class="sxs-lookup"><span data-stu-id="4d3fb-101">Some packages may not install using pip when run on Azure.</span></span>  <span data-ttu-id="4d3fb-102">Cela peut signifier simplement que le package n’est pas disponible dans l’index de packages Python.</span><span class="sxs-lookup"><span data-stu-id="4d3fb-102">It may simply be that the package is not available on the Python Package Index.</span></span>  <span data-ttu-id="4d3fb-103">Ou qu’un compilateur est nécessaire (aucun compilateur n’est disponible sur l’ordinateur exécutant l’application web dans Azure App Service).</span><span class="sxs-lookup"><span data-stu-id="4d3fb-103">It could be that a compiler is required (a compiler is not available on the machine running the web app in Azure App Service).</span></span>

<span data-ttu-id="4d3fb-104">Dans cette section, nous étudierons les différentes façons de résoudre ce problème.</span><span class="sxs-lookup"><span data-stu-id="4d3fb-104">In this section, we'll look at ways to deal with this issue.</span></span>

### <a name="request-wheels"></a><span data-ttu-id="4d3fb-105">Demande de roues</span><span class="sxs-lookup"><span data-stu-id="4d3fb-105">Request wheels</span></span>
<span data-ttu-id="4d3fb-106">Si l’installation du package nécessite un compilateur, tentez de contacter le propriétaire du package afin qu’il mette à disposition des roues pour le package.</span><span class="sxs-lookup"><span data-stu-id="4d3fb-106">If the package installation requires a compiler, you should try contacting the package owner to request that wheels be made available for the package.</span></span>

<span data-ttu-id="4d3fb-107">Avec la disponibilité récente [compilateur Microsoft Visual C++ pour Python 2.7][Microsoft Visual C++ Compiler for Python 2.7], il est désormais plus facile de générer des packages qui ont le code natif pour Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="4d3fb-107">With the recent availability of [Microsoft Visual C++ Compiler for Python 2.7][Microsoft Visual C++ Compiler for Python 2.7], it is now easier to build packages that have native code for Python 2.7.</span></span>

### <a name="build-wheels-requires-windows"></a><span data-ttu-id="4d3fb-108">Création de roues (Windows requis)</span><span class="sxs-lookup"><span data-stu-id="4d3fb-108">Build wheels (requires Windows)</span></span>
<span data-ttu-id="4d3fb-109">Remarque : lorsque vous utilisez cette option, veillez à compiler le package à l’aide d’un environnement Python correspondant à la plateforme/version/architecture utilisée sur l’application web dans Azure Web Service (Windows/32 bits/2.7 ou 3.4).</span><span class="sxs-lookup"><span data-stu-id="4d3fb-109">Note: When using this option, make sure to compile the package using a Python environment that matches the platform/architecture/version that is used on the web app in Azure App Service (Windows/32-bit/2.7 or 3.4).</span></span>

<span data-ttu-id="4d3fb-110">Si l’installation du package échoue car un compilateur est requis, vous pouvez installer le compilateur sur votre machine locale et créer une roue pour le package, que vous inclurez ensuite dans votre référentiel.</span><span class="sxs-lookup"><span data-stu-id="4d3fb-110">If the package doesn't install because it requires a compiler, you can install the compiler on your local machine and build a wheel for the package, which you will then include in your repository.</span></span>

<span data-ttu-id="4d3fb-111">Les utilisateurs Mac/Linux : Si vous n’avez pas accès à un ordinateur Windows, consultez [créer une Machine virtuelle exécutant Windows] [ Create a Virtual Machine Running Windows] pour savoir comment créer une machine virtuelle sur Azure.</span><span class="sxs-lookup"><span data-stu-id="4d3fb-111">Mac/Linux Users: If you don't have access to a Windows machine, see [Create a Virtual Machine Running Windows][Create a Virtual Machine Running Windows] for how to create a VM on Azure.</span></span>  <span data-ttu-id="4d3fb-112">Vous pouvez alors utiliser cette machine virtuelle pour générer des roues et les ajouter au référentiel, puis la supprimer si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="4d3fb-112">You can use it to build the wheels, add them to the repository, and discard the VM if you like.</span></span> 

<span data-ttu-id="4d3fb-113">Pour les Python 2.7, vous pouvez installer [compilateur Microsoft Visual C++ pour Python 2.7][Microsoft Visual C++ Compiler for Python 2.7].</span><span class="sxs-lookup"><span data-stu-id="4d3fb-113">For Python 2.7, you can install [Microsoft Visual C++ Compiler for Python 2.7][Microsoft Visual C++ Compiler for Python 2.7].</span></span>

<span data-ttu-id="4d3fb-114">Pour les Python 3.4, vous pouvez installer [Microsoft Visual C++ 2010 Express][Microsoft Visual C++ 2010 Express].</span><span class="sxs-lookup"><span data-stu-id="4d3fb-114">For Python 3.4, you can install [Microsoft Visual C++ 2010 Express][Microsoft Visual C++ 2010 Express].</span></span>

<span data-ttu-id="4d3fb-115">Pour générer des roues, vous aurez besoin du package de roue :</span><span class="sxs-lookup"><span data-stu-id="4d3fb-115">To build wheels, you'll need the wheel package:</span></span>

    env\scripts\pip install wheel

<span data-ttu-id="4d3fb-116">Vous allez utiliser `pip wheel` pour compiler une dépendance :</span><span class="sxs-lookup"><span data-stu-id="4d3fb-116">You'll use `pip wheel` to compile a dependency:</span></span>

    env\scripts\pip wheel azure==0.8.4

<span data-ttu-id="4d3fb-117">Cette commande crée un fichier .whl dans le dossier \wheelhouse.</span><span class="sxs-lookup"><span data-stu-id="4d3fb-117">This creates a .whl file in the \wheelhouse folder.</span></span>  <span data-ttu-id="4d3fb-118">Ajoutez les fichiers de roue et ceux du dossier \wheelhouse à votre référentiel.</span><span class="sxs-lookup"><span data-stu-id="4d3fb-118">Add the \wheelhouse folder and wheel files to your repository.</span></span>

<span data-ttu-id="4d3fb-119">Modifiez votre fichier requirements.txt en ajoutant l’option `--find-links` en haut.</span><span class="sxs-lookup"><span data-stu-id="4d3fb-119">Edit your requirements.txt to add the `--find-links` option at the top.</span></span> <span data-ttu-id="4d3fb-120">Ceci indique à pip de rechercher une correspondance exacte dans le dossier local, avant de passer à l’index de packages Python.</span><span class="sxs-lookup"><span data-stu-id="4d3fb-120">This tells pip to look for an exact match in the local folder before going to the python package index.</span></span>

    --find-links wheelhouse
    azure==0.8.4

<span data-ttu-id="4d3fb-121">Si vous souhaitez inclure toutes vos dépendances dans le dossier \wheelhouse et ne pas utiliser l’index de packages Python, forcez pip à ignorer l’index de packages en ajoutant `--no-index` en haut du fichier requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="4d3fb-121">If you want to include all your dependencies in the \wheelhouse folder and not use the python package index at all, you can force pip to ignore the package index by adding `--no-index` to the top of your requirements.txt.</span></span>

    --no-index

### <a name="customize-installation"></a><span data-ttu-id="4d3fb-122">Installation personnalisée</span><span class="sxs-lookup"><span data-stu-id="4d3fb-122">Customize installation</span></span>
<span data-ttu-id="4d3fb-123">Vous pouvez personnaliser le script de déploiement afin d’installer un package dans l’environnement virtuel, à l’aide d’un autre programme d’installation, comme easy\_install.</span><span class="sxs-lookup"><span data-stu-id="4d3fb-123">You can customize the deployment script to install a package in the virtual environment using an alternate installer, such as easy\_install.</span></span>  <span data-ttu-id="4d3fb-124">Reportez-vous à deploy.cmd pour obtenir un exemple commenté.</span><span class="sxs-lookup"><span data-stu-id="4d3fb-124">See deploy.cmd for an example that is commented out.</span></span>  <span data-ttu-id="4d3fb-125">Assurez-vous que ces packages ne sont pas répertoriés dans le fichier requirements.txt, pour empêcher pip de les installer.</span><span class="sxs-lookup"><span data-stu-id="4d3fb-125">Make sure that such packages aren't listed in requirements.txt, to prevent pip from installing them.</span></span>

<span data-ttu-id="4d3fb-126">Ajoutez cette instruction au script de déploiement :</span><span class="sxs-lookup"><span data-stu-id="4d3fb-126">Add this to the deployment script:</span></span>

    env\scripts\easy_install somepackage

<span data-ttu-id="4d3fb-127">Vous pouvez également utiliser easy\_install pour effectuer l’installation à partir d’un exécutable d’installation (certains sont compatibles zip et easy\_install les prend en charge).</span><span class="sxs-lookup"><span data-stu-id="4d3fb-127">You may also be able to use easy\_install to install from an exe installer (some are zip compatible, so easy\_install supports them).</span></span>  <span data-ttu-id="4d3fb-128">Ajoutez le programme d’installation à votre référentiel et appelez easy\_install en transmettant le chemin au fichier exécutable.</span><span class="sxs-lookup"><span data-stu-id="4d3fb-128">Add the installer to your repository, and invoke easy\_install by passing the path to the executable.</span></span>

<span data-ttu-id="4d3fb-129">Ajoutez cette instruction au script de déploiement :</span><span class="sxs-lookup"><span data-stu-id="4d3fb-129">Add this to the deployment script:</span></span>

    env\scripts\easy_install "%DEPLOYMENT_SOURCE%\installers\somepackage.exe"

### <a name="include-the-virtual-environment-in-the-repository-requires-windows"></a><span data-ttu-id="4d3fb-130">Inclure l’environnement virtuel dans le référentiel (Windows requis)</span><span class="sxs-lookup"><span data-stu-id="4d3fb-130">Include the virtual environment in the repository (requires Windows)</span></span>
<span data-ttu-id="4d3fb-131">Remarque : lorsque vous choisissez cette option, veillez à utiliser un environnement virtuel correspondant à la plateforme/version/architecture utilisée sur l’application web dans Azure App Service (Windows/32 bits/2.7 ou 3.4).</span><span class="sxs-lookup"><span data-stu-id="4d3fb-131">Note: When using this option, make sure to use a virtual environment that matches the platform/architecture/version that is used on the web app in Azure App Service (Windows/32-bit/2.7 or 3.4).</span></span>

<span data-ttu-id="4d3fb-132">Si vous incluez l’environnement virtuel dans le référentiel, vous pouvez empêcher le script de déploiement d’effectuer la gestion de l’environnement virtuel sur Azure en créant un fichier vide :</span><span class="sxs-lookup"><span data-stu-id="4d3fb-132">If you include the virtual environment in the repository, you can prevent the deployment script from doing virtual environment management on Azure by creating an empty file:</span></span>

    .skipPythonDeployment

<span data-ttu-id="4d3fb-133">Nous vous recommandons de supprimer l’environnement virtuel existant sur l’application, afin d’éviter que des fichiers soient conservés lorsque l’environnement virtuel était géré automatiquement.</span><span class="sxs-lookup"><span data-stu-id="4d3fb-133">We recommend that you delete the existing virtual environment on the app, to prevent leftover files from when the virtual environment was managed automatically.</span></span>

[Create a Virtual Machine Running Windows]: http://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/
[Microsoft Visual C++ Compiler for Python 2.7]: http://aka.ms/vcpython27
[Microsoft Visual C++ 2010 Express]: http://go.microsoft.com/?linkid=9709949
