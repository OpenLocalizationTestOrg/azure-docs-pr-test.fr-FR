<span data-ttu-id="080a8-101">Il est possible que certains packages ne soient pas installés via pip sous Azure.</span><span class="sxs-lookup"><span data-stu-id="080a8-101">Some packages may not install using pip when run on Azure.</span></span>  <span data-ttu-id="080a8-102">Il peut être simplement que ce package hello n’est pas disponible sur hello Python Package Index.</span><span class="sxs-lookup"><span data-stu-id="080a8-102">It may simply be that hello package is not available on hello Python Package Index.</span></span>  <span data-ttu-id="080a8-103">Il peut être qu’un compilateur est requis (un compilateur n’est pas disponible sur l’ordinateur en cours d’exécution hello web application hello dans Azure App Service).</span><span class="sxs-lookup"><span data-stu-id="080a8-103">It could be that a compiler is required (a compiler is not available on hello machine running hello web app in Azure App Service).</span></span>

<span data-ttu-id="080a8-104">Dans cette section, nous allons examiner les façons toodeal avec ce problème.</span><span class="sxs-lookup"><span data-stu-id="080a8-104">In this section, we'll look at ways toodeal with this issue.</span></span>

### <a name="request-wheels"></a><span data-ttu-id="080a8-105">Demande de roues</span><span class="sxs-lookup"><span data-stu-id="080a8-105">Request wheels</span></span>
<span data-ttu-id="080a8-106">Si l’installation du package hello requiert un compilateur, vous devez essayer de contacter hello package propriétaire toorequest que roues être disponibles pour le package de hello.</span><span class="sxs-lookup"><span data-stu-id="080a8-106">If hello package installation requires a compiler, you should try contacting hello package owner toorequest that wheels be made available for hello package.</span></span>

<span data-ttu-id="080a8-107">Avec la disponibilité récente hello [compilateur Microsoft Visual C++ pour Python 2.7][Microsoft Visual C++ Compiler for Python 2.7], il est désormais plus faciles packages toobuild ayant le code natif pour Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="080a8-107">With hello recent availability of [Microsoft Visual C++ Compiler for Python 2.7][Microsoft Visual C++ Compiler for Python 2.7], it is now easier toobuild packages that have native code for Python 2.7.</span></span>

### <a name="build-wheels-requires-windows"></a><span data-ttu-id="080a8-108">Création de roues (Windows requis)</span><span class="sxs-lookup"><span data-stu-id="080a8-108">Build wheels (requires Windows)</span></span>
<span data-ttu-id="080a8-109">Remarque : Lorsque vous utilisez cette option, vérifiez que package de hello toocompile à l’aide d’un environnement de Python qui correspond aux hello/architecture/version de la plateforme qui est utilisée sur l’application web de hello dans Azure App Service (Windows/32-bit/2.7 ou 3.4).</span><span class="sxs-lookup"><span data-stu-id="080a8-109">Note: When using this option, make sure toocompile hello package using a Python environment that matches hello platform/architecture/version that is used on hello web app in Azure App Service (Windows/32-bit/2.7 or 3.4).</span></span>

<span data-ttu-id="080a8-110">Si le package de hello ne s’installe pas, car elle requiert un compilateur, vous pouvez installer le compilateur de hello sur votre ordinateur local et générer une roulette de package de hello, qui vous serez ensuite inclure dans votre référentiel.</span><span class="sxs-lookup"><span data-stu-id="080a8-110">If hello package doesn't install because it requires a compiler, you can install hello compiler on your local machine and build a wheel for hello package, which you will then include in your repository.</span></span>

<span data-ttu-id="080a8-111">Les utilisateurs Mac/Linux : Si vous n’avez pas machine virtuelle Windows tooa accès, consultez [créer une Machine virtuelle exécutant Windows] [ Create a Virtual Machine Running Windows] de façon toocreate une machine virtuelle sur Azure.</span><span class="sxs-lookup"><span data-stu-id="080a8-111">Mac/Linux Users: If you don't have access tooa Windows machine, see [Create a Virtual Machine Running Windows][Create a Virtual Machine Running Windows] for how toocreate a VM on Azure.</span></span>  <span data-ttu-id="080a8-112">Vous pouvez utiliser roues de hello toobuild, ajoutez-les toohello référentiel et ignorer hello machine virtuelle si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="080a8-112">You can use it toobuild hello wheels, add them toohello repository, and discard hello VM if you like.</span></span> 

<span data-ttu-id="080a8-113">Pour les Python 2.7, vous pouvez installer [compilateur Microsoft Visual C++ pour Python 2.7][Microsoft Visual C++ Compiler for Python 2.7].</span><span class="sxs-lookup"><span data-stu-id="080a8-113">For Python 2.7, you can install [Microsoft Visual C++ Compiler for Python 2.7][Microsoft Visual C++ Compiler for Python 2.7].</span></span>

<span data-ttu-id="080a8-114">Pour les Python 3.4, vous pouvez installer [Microsoft Visual C++ 2010 Express][Microsoft Visual C++ 2010 Express].</span><span class="sxs-lookup"><span data-stu-id="080a8-114">For Python 3.4, you can install [Microsoft Visual C++ 2010 Express][Microsoft Visual C++ 2010 Express].</span></span>

<span data-ttu-id="080a8-115">Vous devez toobuild roues, package de roulette hello :</span><span class="sxs-lookup"><span data-stu-id="080a8-115">toobuild wheels, you'll need hello wheel package:</span></span>

    env\scripts\pip install wheel

<span data-ttu-id="080a8-116">Vous allez utiliser `pip wheel` toocompile une dépendance :</span><span class="sxs-lookup"><span data-stu-id="080a8-116">You'll use `pip wheel` toocompile a dependency:</span></span>

    env\scripts\pip wheel azure==0.8.4

<span data-ttu-id="080a8-117">Cela crée un fichier de .whl dans le dossier de \wheelhouse hello.</span><span class="sxs-lookup"><span data-stu-id="080a8-117">This creates a .whl file in hello \wheelhouse folder.</span></span>  <span data-ttu-id="080a8-118">Ajouter le dossier de \wheelhouse hello et un référentiel de tooyour de fichiers de roulette.</span><span class="sxs-lookup"><span data-stu-id="080a8-118">Add hello \wheelhouse folder and wheel files tooyour repository.</span></span>

<span data-ttu-id="080a8-119">Modifier votre hello de tooadd requirements.txt `--find-links` option haut hello.</span><span class="sxs-lookup"><span data-stu-id="080a8-119">Edit your requirements.txt tooadd hello `--find-links` option at hello top.</span></span> <span data-ttu-id="080a8-120">Cela indique un pip toolook une correspondance exacte dans le dossier local de hello avant l’index de cours toohello python package.</span><span class="sxs-lookup"><span data-stu-id="080a8-120">This tells pip toolook for an exact match in hello local folder before going toohello python package index.</span></span>

    --find-links wheelhouse
    azure==0.8.4

<span data-ttu-id="080a8-121">Si vous souhaitez tooinclude toutes les dépendances de vos hello \wheelhouse dossier et n’utilise pas hello python package index du tout, vous pouvez forcer l’index du package pip tooignore hello en ajoutant `--no-index` haut toohello de votre requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="080a8-121">If you want tooinclude all your dependencies in hello \wheelhouse folder and not use hello python package index at all, you can force pip tooignore hello package index by adding `--no-index` toohello top of your requirements.txt.</span></span>

    --no-index

### <a name="customize-installation"></a><span data-ttu-id="080a8-122">Installation personnalisée</span><span class="sxs-lookup"><span data-stu-id="080a8-122">Customize installation</span></span>
<span data-ttu-id="080a8-123">Vous pouvez personnaliser tooinstall de script de déploiement hello un package dans hello environnement virtuel en utilisant un autre programme d’installation, tel que facile\_installer.</span><span class="sxs-lookup"><span data-stu-id="080a8-123">You can customize hello deployment script tooinstall a package in hello virtual environment using an alternate installer, such as easy\_install.</span></span>  <span data-ttu-id="080a8-124">Reportez-vous à deploy.cmd pour obtenir un exemple commenté.  Assurez-vous que ces packages ne sont pas répertoriés dans requirements.txt, pip tooprevent de les installer.</span><span class="sxs-lookup"><span data-stu-id="080a8-124">See deploy.cmd for an example that is commented out.  Make sure that such packages aren't listed in requirements.txt, tooprevent pip from installing them.</span></span>

<span data-ttu-id="080a8-125">Ajoutez ce script de déploiement toohello :</span><span class="sxs-lookup"><span data-stu-id="080a8-125">Add this toohello deployment script:</span></span>

    env\scripts\easy_install somepackage

<span data-ttu-id="080a8-126">Vous pouvez également être en mesure de toouse facile\_installer tooinstall à partir d’un programme d’installation de l’exe (certains sont zip compatible, facile\_installer les prend en charge).</span><span class="sxs-lookup"><span data-stu-id="080a8-126">You may also be able toouse easy\_install tooinstall from an exe installer (some are zip compatible, so easy\_install supports them).</span></span>  <span data-ttu-id="080a8-127">Ajoutez le référentiel de tooyour hello programme d’installation et appeler facilement\_installer en passant toohello de chemin d’accès hello exécutable.</span><span class="sxs-lookup"><span data-stu-id="080a8-127">Add hello installer tooyour repository, and invoke easy\_install by passing hello path toohello executable.</span></span>

<span data-ttu-id="080a8-128">Ajoutez ce script de déploiement toohello :</span><span class="sxs-lookup"><span data-stu-id="080a8-128">Add this toohello deployment script:</span></span>

    env\scripts\easy_install "%DEPLOYMENT_SOURCE%\installers\somepackage.exe"

### <a name="include-hello-virtual-environment-in-hello-repository-requires-windows"></a><span data-ttu-id="080a8-129">Inclure un environnement virtuel de hello dans le référentiel hello (nécessite Windows)</span><span class="sxs-lookup"><span data-stu-id="080a8-129">Include hello virtual environment in hello repository (requires Windows)</span></span>
<span data-ttu-id="080a8-130">Remarque : Lorsque vous utilisez cette option, assurez-vous que toouse un environnement virtuel qui correspond aux hello/architecture/version de la plateforme qui est utilisée sur l’application web de hello dans Azure App Service (Windows/32-bit/2.7 ou 3.4).</span><span class="sxs-lookup"><span data-stu-id="080a8-130">Note: When using this option, make sure toouse a virtual environment that matches hello platform/architecture/version that is used on hello web app in Azure App Service (Windows/32-bit/2.7 or 3.4).</span></span>

<span data-ttu-id="080a8-131">Si vous incluez un environnement virtuel de hello dans le référentiel de hello, vous pouvez empêcher le script de déploiement hello d’effectuer la gestion de l’environnement virtuel sur Azure en créant un fichier vide :</span><span class="sxs-lookup"><span data-stu-id="080a8-131">If you include hello virtual environment in hello repository, you can prevent hello deployment script from doing virtual environment management on Azure by creating an empty file:</span></span>

    .skipPythonDeployment

<span data-ttu-id="080a8-132">Nous vous recommandons de supprimer environnement virtuel existant de hello sur application hello, tooprevent les fichiers restants à partir de lors de l’environnement virtuel de hello était gérée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="080a8-132">We recommend that you delete hello existing virtual environment on hello app, tooprevent leftover files from when hello virtual environment was managed automatically.</span></span>

[Create a Virtual Machine Running Windows]: http://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/
[Microsoft Visual C++ Compiler for Python 2.7]: http://aka.ms/vcpython27
[Microsoft Visual C++ 2010 Express]: http://go.microsoft.com/?linkid=9709949
