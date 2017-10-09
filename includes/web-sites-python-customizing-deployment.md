<span data-ttu-id="af383-101">Azure détermine que votre application utilise Python **si les deux conditions suivantes sont remplies**:</span><span class="sxs-lookup"><span data-stu-id="af383-101">Azure will determine that your application uses Python **if both of these conditions are true**:</span></span>

* <span data-ttu-id="af383-102">fichier Requirements.txt dans le dossier racine de hello</span><span class="sxs-lookup"><span data-stu-id="af383-102">requirements.txt file in hello root folder</span></span>
* <span data-ttu-id="af383-103">n’importe quel fichier .py dans le dossier racine de hello ou un runtime.txt qui spécifie les python</span><span class="sxs-lookup"><span data-stu-id="af383-103">any .py file in hello root folder OR a runtime.txt that specifies python</span></span>

<span data-ttu-id="af383-104">Lorsque c’est le cas de hello, il utilise un script de déploiement spécifique Python qui effectue une synchronisation standard de hello de fichiers, ainsi que les opérations de Python supplémentaires telles que :</span><span class="sxs-lookup"><span data-stu-id="af383-104">When that's hello case, it will use a Python specific deployment script, which performs hello standard synchronization of files, as well as additional Python operations such as:</span></span>

* <span data-ttu-id="af383-105">Gestion automatique de l’environnement virtuel</span><span class="sxs-lookup"><span data-stu-id="af383-105">Automatic management of virtual environment</span></span>
* <span data-ttu-id="af383-106">Installation des packages répertoriés dans requirements.txt à l’aide de pip</span><span class="sxs-lookup"><span data-stu-id="af383-106">Installation of packages listed in requirements.txt using pip</span></span>
* <span data-ttu-id="af383-107">La création du fichier web.config approprié hello selon hello sélectionnés version Python.</span><span class="sxs-lookup"><span data-stu-id="af383-107">Creation of hello appropriate web.config based on hello selected Python version.</span></span>
* <span data-ttu-id="af383-108">Collecte des fichiers statiques pour les applications Django</span><span class="sxs-lookup"><span data-stu-id="af383-108">Collect static files for Django applications</span></span>

<span data-ttu-id="af383-109">Vous pouvez contrôler certains aspects des étapes de déploiement par défaut hello sans avoir de script de hello toocustomize.</span><span class="sxs-lookup"><span data-stu-id="af383-109">You can control certain aspects of hello default deployment steps without having toocustomize hello script.</span></span>

<span data-ttu-id="af383-110">Si vous souhaitez tooskip toutes les étapes de déploiement spécifique de Python, vous pouvez créer ce fichier vide :</span><span class="sxs-lookup"><span data-stu-id="af383-110">If you want tooskip all Python specific deployment steps, you can create this empty file:</span></span>

    \.skipPythonDeployment

<span data-ttu-id="af383-111">Pour mieux contrôler le déploiement, vous pouvez remplacer le script de déploiement par défaut hello en créant hello fichiers suivants :</span><span class="sxs-lookup"><span data-stu-id="af383-111">For more control over deployment, you can override hello default deployment script by creating hello following files:</span></span>

    \.deployment
    \deploy.cmd

<span data-ttu-id="af383-112">Vous pouvez utiliser hello [interface de ligne de commande Azure] [ Azure command-line interface] toocreate les fichiers hello.</span><span class="sxs-lookup"><span data-stu-id="af383-112">You can use hello [Azure command-line interface][Azure command-line interface] toocreate hello files.</span></span>  <span data-ttu-id="af383-113">Utilisez cette commande à partir de votre dossier de projet :</span><span class="sxs-lookup"><span data-stu-id="af383-113">Use this command from your project folder:</span></span>

    azure site deploymentscript --python

<span data-ttu-id="af383-114">Lorsque ces fichiers n’existent pas, Azure crée un script de déploiement temporaire et l’exécute.</span><span class="sxs-lookup"><span data-stu-id="af383-114">When these files don't exist, Azure creates a temporary deployment script and runs it.</span></span>  <span data-ttu-id="af383-115">Il est identique toohello vous l’avez créée avec la commande hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="af383-115">It is identical toohello one you create with hello command above.</span></span>

[Azure command-line interface]: http://azure.microsoft.com/downloads/
