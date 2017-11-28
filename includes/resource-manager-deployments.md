## <a name="incremental-and-complete-deployments"></a><span data-ttu-id="a726e-101">Déploiements incrémentiels et complets</span><span class="sxs-lookup"><span data-stu-id="a726e-101">Incremental and complete deployments</span></span>
<span data-ttu-id="a726e-102">Lorsque vous déployez vos ressources, vous spécifiez que le déploiement est soit une mise à jour incrémentielle, soit une mise à jour complète.</span><span class="sxs-lookup"><span data-stu-id="a726e-102">When deploying your resources, you specify that the deployment is either an incremental update or a complete update.</span></span> <span data-ttu-id="a726e-103">La principale différence entre ces deux modes réside dans la manière dont Resource Manager gère les ressources existantes dans le groupe de ressources qui ne se trouvent pas dans le modèle :</span><span class="sxs-lookup"><span data-stu-id="a726e-103">The primary difference between these two modes is how Resource Manager handles existing resources in the resource group that are not in the template:</span></span>

* <span data-ttu-id="a726e-104">En mode complet, Resource Manager **supprime** les ressources qui existent dans le groupe de ressources, mais qui ne sont pas spécifiées dans le modèle.</span><span class="sxs-lookup"><span data-stu-id="a726e-104">In complete mode, Resource Manager **deletes** resources that exist in the resource group but are not specified in the template.</span></span> 
* <span data-ttu-id="a726e-105">En mode incrémentiel, Resource Manager **conserve telles quelles** les ressources qui existent dans le groupe de ressources, mais qui ne sont pas spécifiées dans le modèle.</span><span class="sxs-lookup"><span data-stu-id="a726e-105">In incremental mode, Resource Manager **leaves unchanged** resources that exist in the resource group but are not specified in the template.</span></span>

<span data-ttu-id="a726e-106">Pour les deux modes, Resource Manager tente de configurer toutes les ressources spécifiées dans le modèle.</span><span class="sxs-lookup"><span data-stu-id="a726e-106">For both modes, Resource Manager attempts to provision all resources specified in the template.</span></span> <span data-ttu-id="a726e-107">Si la ressource existe déjà dans le groupe de ressources et si ses paramètres sont conservés, l’opération n’entraîne aucune modification.</span><span class="sxs-lookup"><span data-stu-id="a726e-107">If the resource already exists in the resource group and its settings are unchanged, the operation results in no change.</span></span> <span data-ttu-id="a726e-108">Si vous modifiez les paramètres d’une ressource, la ressource est configurée avec ces nouveaux paramètres.</span><span class="sxs-lookup"><span data-stu-id="a726e-108">If you change the settings for a resource, the resource is provisioned with those new settings.</span></span> <span data-ttu-id="a726e-109">Si vous tentez de mettre à jour l’emplacement ou le type d’une ressource existante, le déploiement échoue avec une erreur.</span><span class="sxs-lookup"><span data-stu-id="a726e-109">If you attempt to update the location or type of an existing resource, the deployment fails with an error.</span></span> <span data-ttu-id="a726e-110">Vous devez dans ce cas déployer une nouvelle ressource avec l’emplacement ou le type dont vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="a726e-110">Instead, deploy a new resource with the location or type that you need.</span></span>

<span data-ttu-id="a726e-111">Par défaut, Resource Manager utilise le mode incrémentiel.</span><span class="sxs-lookup"><span data-stu-id="a726e-111">By default, Resource Manager uses the incremental mode.</span></span>

<span data-ttu-id="a726e-112">Pour illustrer la différence entre les modes incrémentiel et complet, examinez le scénario suivant.</span><span class="sxs-lookup"><span data-stu-id="a726e-112">To illustrate the difference between incremental and complete modes, consider the following scenario.</span></span>

<span data-ttu-id="a726e-113">Un **groupe de ressources existant** contient :</span><span class="sxs-lookup"><span data-stu-id="a726e-113">**Existing Resource Group** contains:</span></span>

* <span data-ttu-id="a726e-114">Ressource A</span><span class="sxs-lookup"><span data-stu-id="a726e-114">Resource A</span></span>
* <span data-ttu-id="a726e-115">Ressource B</span><span class="sxs-lookup"><span data-stu-id="a726e-115">Resource B</span></span>
* <span data-ttu-id="a726e-116">Ressource C</span><span class="sxs-lookup"><span data-stu-id="a726e-116">Resource C</span></span>

<span data-ttu-id="a726e-117">Un **modèle** définit :</span><span class="sxs-lookup"><span data-stu-id="a726e-117">**Template** defines:</span></span>

* <span data-ttu-id="a726e-118">Ressource A</span><span class="sxs-lookup"><span data-stu-id="a726e-118">Resource A</span></span>
* <span data-ttu-id="a726e-119">Ressource B</span><span class="sxs-lookup"><span data-stu-id="a726e-119">Resource B</span></span>
* <span data-ttu-id="a726e-120">Ressource D</span><span class="sxs-lookup"><span data-stu-id="a726e-120">Resource D</span></span>

<span data-ttu-id="a726e-121">Lors du déploiement en mode **incrémentiel**, le groupe de ressources contient :</span><span class="sxs-lookup"><span data-stu-id="a726e-121">When deployed in **incremental** mode, the resource group contains:</span></span>

* <span data-ttu-id="a726e-122">Ressource A</span><span class="sxs-lookup"><span data-stu-id="a726e-122">Resource A</span></span>
* <span data-ttu-id="a726e-123">Ressource B</span><span class="sxs-lookup"><span data-stu-id="a726e-123">Resource B</span></span>
* <span data-ttu-id="a726e-124">Ressource C</span><span class="sxs-lookup"><span data-stu-id="a726e-124">Resource C</span></span>
* <span data-ttu-id="a726e-125">Ressource D</span><span class="sxs-lookup"><span data-stu-id="a726e-125">Resource D</span></span>

<span data-ttu-id="a726e-126">Lors du déploiement en mode **complet**, la ressource C est supprimée.</span><span class="sxs-lookup"><span data-stu-id="a726e-126">When deployed in **complete** mode, Resource C is deleted.</span></span> <span data-ttu-id="a726e-127">Le groupe de ressources contient :</span><span class="sxs-lookup"><span data-stu-id="a726e-127">The resource group contains:</span></span>

* <span data-ttu-id="a726e-128">Ressource A</span><span class="sxs-lookup"><span data-stu-id="a726e-128">Resource A</span></span>
* <span data-ttu-id="a726e-129">Ressource B</span><span class="sxs-lookup"><span data-stu-id="a726e-129">Resource B</span></span>
* <span data-ttu-id="a726e-130">Ressource D</span><span class="sxs-lookup"><span data-stu-id="a726e-130">Resource D</span></span>
