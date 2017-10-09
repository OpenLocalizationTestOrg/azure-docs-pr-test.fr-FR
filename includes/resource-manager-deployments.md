## <a name="incremental-and-complete-deployments"></a><span data-ttu-id="f0701-101">Déploiements incrémentiels et complets</span><span class="sxs-lookup"><span data-stu-id="f0701-101">Incremental and complete deployments</span></span>
<span data-ttu-id="f0701-102">Lors du déploiement de vos ressources, vous spécifiez que le déploiement de hello est une mise à jour incrémentielle ou une mise à jour terminée.</span><span class="sxs-lookup"><span data-stu-id="f0701-102">When deploying your resources, you specify that hello deployment is either an incremental update or a complete update.</span></span> <span data-ttu-id="f0701-103">Hello principale différence entre ces deux modes est comment le Gestionnaire de ressources gère les ressources existantes dans le groupe de ressources hello qui ne sont pas dans le modèle de hello :</span><span class="sxs-lookup"><span data-stu-id="f0701-103">hello primary difference between these two modes is how Resource Manager handles existing resources in hello resource group that are not in hello template:</span></span>

* <span data-ttu-id="f0701-104">En mode complet, le Gestionnaire de ressources **supprime** ressources qui existent dans le groupe de ressources hello mais qui ne sont pas spécifiés dans le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="f0701-104">In complete mode, Resource Manager **deletes** resources that exist in hello resource group but are not specified in hello template.</span></span> 
* <span data-ttu-id="f0701-105">En mode incrémentiel, le Gestionnaire de ressources **laisse inchangée** ressources qui existent dans le groupe de ressources hello mais qui ne sont pas spécifiés dans le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="f0701-105">In incremental mode, Resource Manager **leaves unchanged** resources that exist in hello resource group but are not specified in hello template.</span></span>

<span data-ttu-id="f0701-106">Pour les deux modes, le Gestionnaire de ressources tente tooprovision toutes les ressources spécifiées dans le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="f0701-106">For both modes, Resource Manager attempts tooprovision all resources specified in hello template.</span></span> <span data-ttu-id="f0701-107">Si les ressources hello existant déjà dans le groupe de ressources hello et ses paramètres sont identiques, hello opération entraîne aucune modification.</span><span class="sxs-lookup"><span data-stu-id="f0701-107">If hello resource already exists in hello resource group and its settings are unchanged, hello operation results in no change.</span></span> <span data-ttu-id="f0701-108">Si vous modifiez les paramètres de hello pour une ressource, les ressources hello sont configuré avec ces nouveaux paramètres.</span><span class="sxs-lookup"><span data-stu-id="f0701-108">If you change hello settings for a resource, hello resource is provisioned with those new settings.</span></span> <span data-ttu-id="f0701-109">Si vous essayez d’emplacement de hello tooupdate ou le type d’une ressource existante, le déploiement de hello échoue avec une erreur.</span><span class="sxs-lookup"><span data-stu-id="f0701-109">If you attempt tooupdate hello location or type of an existing resource, hello deployment fails with an error.</span></span> <span data-ttu-id="f0701-110">Au lieu de cela, déployer une nouvelle ressource avec l’emplacement de hello ou type que vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="f0701-110">Instead, deploy a new resource with hello location or type that you need.</span></span>

<span data-ttu-id="f0701-111">Par défaut, le Gestionnaire de ressources utilise le mode incrémentiel de hello.</span><span class="sxs-lookup"><span data-stu-id="f0701-111">By default, Resource Manager uses hello incremental mode.</span></span>

<span data-ttu-id="f0701-112">différence de hello tooillustrate entre les modes incrémentielles et complètes, envisagez de hello scénario.</span><span class="sxs-lookup"><span data-stu-id="f0701-112">tooillustrate hello difference between incremental and complete modes, consider hello following scenario.</span></span>

<span data-ttu-id="f0701-113">Un **groupe de ressources existant** contient :</span><span class="sxs-lookup"><span data-stu-id="f0701-113">**Existing Resource Group** contains:</span></span>

* <span data-ttu-id="f0701-114">Ressource A</span><span class="sxs-lookup"><span data-stu-id="f0701-114">Resource A</span></span>
* <span data-ttu-id="f0701-115">Ressource B</span><span class="sxs-lookup"><span data-stu-id="f0701-115">Resource B</span></span>
* <span data-ttu-id="f0701-116">Ressource C</span><span class="sxs-lookup"><span data-stu-id="f0701-116">Resource C</span></span>

<span data-ttu-id="f0701-117">Un **modèle** définit :</span><span class="sxs-lookup"><span data-stu-id="f0701-117">**Template** defines:</span></span>

* <span data-ttu-id="f0701-118">Ressource A</span><span class="sxs-lookup"><span data-stu-id="f0701-118">Resource A</span></span>
* <span data-ttu-id="f0701-119">Ressource B</span><span class="sxs-lookup"><span data-stu-id="f0701-119">Resource B</span></span>
* <span data-ttu-id="f0701-120">Ressource D</span><span class="sxs-lookup"><span data-stu-id="f0701-120">Resource D</span></span>

<span data-ttu-id="f0701-121">Lors du déploiement dans **incrémentielle** mode, le groupe de ressources hello contient :</span><span class="sxs-lookup"><span data-stu-id="f0701-121">When deployed in **incremental** mode, hello resource group contains:</span></span>

* <span data-ttu-id="f0701-122">Ressource A</span><span class="sxs-lookup"><span data-stu-id="f0701-122">Resource A</span></span>
* <span data-ttu-id="f0701-123">Ressource B</span><span class="sxs-lookup"><span data-stu-id="f0701-123">Resource B</span></span>
* <span data-ttu-id="f0701-124">Ressource C</span><span class="sxs-lookup"><span data-stu-id="f0701-124">Resource C</span></span>
* <span data-ttu-id="f0701-125">Ressource D</span><span class="sxs-lookup"><span data-stu-id="f0701-125">Resource D</span></span>

<span data-ttu-id="f0701-126">Lors du déploiement en mode **complet**, la ressource C est supprimée.</span><span class="sxs-lookup"><span data-stu-id="f0701-126">When deployed in **complete** mode, Resource C is deleted.</span></span> <span data-ttu-id="f0701-127">groupe de ressources Hello contient :</span><span class="sxs-lookup"><span data-stu-id="f0701-127">hello resource group contains:</span></span>

* <span data-ttu-id="f0701-128">Ressource A</span><span class="sxs-lookup"><span data-stu-id="f0701-128">Resource A</span></span>
* <span data-ttu-id="f0701-129">Ressource B</span><span class="sxs-lookup"><span data-stu-id="f0701-129">Resource B</span></span>
* <span data-ttu-id="f0701-130">Ressource D</span><span class="sxs-lookup"><span data-stu-id="f0701-130">Resource D</span></span>
