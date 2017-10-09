# <a name="scale-agent-nodes-in-a-container-service-cluster"></a><span data-ttu-id="395b6-101">Mettre à l’échelle des nœuds d’agent dans un cluster Container Service</span><span class="sxs-lookup"><span data-stu-id="395b6-101">Scale agent nodes in a Container Service cluster</span></span>
<span data-ttu-id="395b6-102">Après avoir [déploiement d’un cluster du Service de conteneur Azure](../articles/container-service/dcos-swarm/container-service-deployment.md), vous devrez peut-être le nombre de hello toochange de nœuds de l’agent.</span><span class="sxs-lookup"><span data-stu-id="395b6-102">After [deploying an Azure Container Service cluster](../articles/container-service/dcos-swarm/container-service-deployment.md), you might need toochange hello number of agent nodes.</span></span> <span data-ttu-id="395b6-103">Vous risquez par exemple d’avoir besoin de davantage d’agents afin de pouvoir exécuter davantage d’instances ou d’applications de conteneur.</span><span class="sxs-lookup"><span data-stu-id="395b6-103">For example, you might need more agents so you can run more container applications or instances.</span></span> 

<span data-ttu-id="395b6-104">Vous pouvez modifier nombre hello de nœuds de l’agent dans un cluster de contrôleur de domaine/système d’exploitation, Docker Swarm ou Kubernetes à l’aide de hello portail Azure ou hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="395b6-104">You can change hello number of agent nodes in a DC/OS, Docker Swarm, or Kubernetes cluster by using hello Azure portal or hello Azure CLI 2.0.</span></span> 

## <a name="scale-with-hello-azure-portal"></a><span data-ttu-id="395b6-105">Mettre à l’échelle par hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="395b6-105">Scale with hello Azure portal</span></span>

1. <span data-ttu-id="395b6-106">Bonjour [portail Azure](https://portal.azure.com), recherchez **services de conteneur**, puis cliquez sur le service de conteneur hello que vous souhaitez toomodify.</span><span class="sxs-lookup"><span data-stu-id="395b6-106">In hello [Azure portal](https://portal.azure.com), browse for **Container services**, and then click hello container service that you want toomodify.</span></span>
2. <span data-ttu-id="395b6-107">Bonjour **service de conteneur** panneau, cliquez sur **Agents**.</span><span class="sxs-lookup"><span data-stu-id="395b6-107">In hello **Container service** blade, click **Agents**.</span></span>
3. <span data-ttu-id="395b6-108">Dans **nombre d’ordinateurs virtuels**, entrez nombre hello souhaité de nœuds d’agents.</span><span class="sxs-lookup"><span data-stu-id="395b6-108">In **VM Count**, enter hello desired number of agents nodes.</span></span>

    ![Mettre à l’échelle d’un pool dans le portail de hello](./media/container-service-scale/container-service-scale-portal.png)

4. <span data-ttu-id="395b6-110">configuration de hello toosave, cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="395b6-110">toosave hello configuration, click **Save**.</span></span>

## <a name="scale-with-hello-azure-cli-20"></a><span data-ttu-id="395b6-111">Mettre à l’échelle par hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="395b6-111">Scale with hello Azure CLI 2.0</span></span>

<span data-ttu-id="395b6-112">Assurez-vous que vous [installé](/cli/azure/install-az-cli2) hello dernière Azure CLI 2.0 et consigné dans tooan compte azure (`az login`).</span><span class="sxs-lookup"><span data-stu-id="395b6-112">Make sure that you [installed](/cli/azure/install-az-cli2) hello latest Azure CLI 2.0 and logged in tooan azure account (`az login`).</span></span>

### <a name="see-hello-current-agent-count"></a><span data-ttu-id="395b6-113">Voir le nombre actuel de l’agent de hello</span><span class="sxs-lookup"><span data-stu-id="395b6-113">See hello current agent count</span></span>
<span data-ttu-id="395b6-114">nombre de hello toosee d’agents actuellement dans un cluster de hello, exécutez hello `az acs show` commande.</span><span class="sxs-lookup"><span data-stu-id="395b6-114">toosee hello number of agents currently in hello cluster, run hello `az acs show` command.</span></span> <span data-ttu-id="395b6-115">Configuration de cluster hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="395b6-115">This shows hello cluster configuration.</span></span> <span data-ttu-id="395b6-116">Hello, par exemple, la commande affiche hello configuration du service de conteneur hello nommé suivante `containerservice-myACSName` dans le groupe de ressources hello `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="395b6-116">For example, hello following command shows hello configuration of hello container service named `containerservice-myACSName` in hello resource group `myResourceGroup`:</span></span>

```azurecli
az acs show -g myResourceGroup -n containerservice-myACSName
```

<span data-ttu-id="395b6-117">commande Hello retourne le nombre de hello d’agents Bonjour `Count` valeur sous `AgentPoolProfiles`.</span><span class="sxs-lookup"><span data-stu-id="395b6-117">hello command returns hello number of agents in hello `Count` value under `AgentPoolProfiles`.</span></span>

### <a name="use-hello-az-acs-scale-command"></a><span data-ttu-id="395b6-118">Utilisez hello az commande de mise à l’échelle des services acs</span><span class="sxs-lookup"><span data-stu-id="395b6-118">Use hello az acs scale command</span></span>
<span data-ttu-id="395b6-119">nombre de hello toochange de nœuds de l’agent, exécutez hello `az acs scale` hello de commande et fournissez **groupe de ressources**, **nom de service de conteneur**et hello souhaité **nouveau nombre d’agents**.</span><span class="sxs-lookup"><span data-stu-id="395b6-119">toochange hello number of agent nodes, run hello `az acs scale` command and supply hello **resource group**, **container service name**, and hello desired **new agent count**.</span></span> <span data-ttu-id="395b6-120">Si vous utilisez un nombre inférieur ou supérieur, vous descendez ou montez en puissance, respectivement.</span><span class="sxs-lookup"><span data-stu-id="395b6-120">By using a smaller or higher number, you can scale down or up, respectively.</span></span>

<span data-ttu-id="395b6-121">Par exemple, le nombre de hello toochange d’agents dans hello précédente too10 de cluster, tapez Bonjour de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="395b6-121">For example, toochange hello number of agents in hello previous cluster too10, type hello following command:</span></span>

```azurecli
az acs scale -g myResourceGroup -n containerservice-myACSName --new-agent-count 10
```

<span data-ttu-id="395b6-122">Bonjour Azure CLI 2.0 retourne une chaîne JSON représentant la nouvelle configuration du service de conteneur hello, y compris le nombre de l’agent de nouveau hello de hello.</span><span class="sxs-lookup"><span data-stu-id="395b6-122">hello Azure CLI 2.0 returns a JSON string representing hello new configuration of hello container service, including hello new agent count.</span></span>

<span data-ttu-id="395b6-123">Pour plus d’options de commande, exécutez `az acs scale --help`.</span><span class="sxs-lookup"><span data-stu-id="395b6-123">For more command options, run `az acs scale --help`.</span></span>

## <a name="scaling-considerations"></a><span data-ttu-id="395b6-124">Mise à l'échelle - Éléments à prendre en compte</span><span class="sxs-lookup"><span data-stu-id="395b6-124">Scaling considerations</span></span>

* <span data-ttu-id="395b6-125">nombre de Hello de nœuds de l’agent doit être compris entre 1 et 100 (inclus).</span><span class="sxs-lookup"><span data-stu-id="395b6-125">hello number of agent nodes must be between 1 and 100, inclusive.</span></span> 

* <span data-ttu-id="395b6-126">Votre quota de cœurs peut limiter le nombre de hello de nœuds de l’agent dans un cluster.</span><span class="sxs-lookup"><span data-stu-id="395b6-126">Your cores quota can limit hello number of agent nodes in a cluster.</span></span>

* <span data-ttu-id="395b6-127">Opérations de mise à l’échelle de nœud de l’agent sont un ensemble d’échelle de machine virtuelle Azure tooan appliqué qui contient le pool d’agents hello.</span><span class="sxs-lookup"><span data-stu-id="395b6-127">Agent node scaling operations are applied tooan Azure virtual machine scale set that contains hello agent pool.</span></span> <span data-ttu-id="395b6-128">Dans un cluster de contrôleur de domaine/système d’exploitation, seuls les nœuds de l’agent dans le pool privé de hello à l’échelle par les opérations hello illustrées dans cet article.</span><span class="sxs-lookup"><span data-stu-id="395b6-128">In a DC/OS cluster, only agent nodes in hello private pool are scaled by hello operations shown in this article.</span></span>

* <span data-ttu-id="395b6-129">En fonction d’orchestrator hello que vous déployez dans votre cluster, vous pouvez faire évoluer séparément nombre hello d’instances d’un conteneur en cours d’exécution sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="395b6-129">Depending on hello orchestrator you deploy in your cluster, you can separately scale hello number of instances of a container running on hello cluster.</span></span> <span data-ttu-id="395b6-130">Par exemple, dans un cluster de contrôleur de domaine/système d’exploitation, utilisez hello [Marathon UI](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) toochange hello quantité, pour les instances d’une application conteneur.</span><span class="sxs-lookup"><span data-stu-id="395b6-130">For example, in a DC/OS cluster, use hello [Marathon UI](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) toochange hello number of instances of a container application.</span></span>

* <span data-ttu-id="395b6-131">Actuellement, la mise à l’échelle automatique de nœuds d’agent dans un cluster du service de conteneur n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="395b6-131">Currently, autoscaling of agent nodes in a container service cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="395b6-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="395b6-132">Next steps</span></span>
* <span data-ttu-id="395b6-133">Consultez [d’autres exemples](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) d’utilisation des commandes de la CLI Azure 2.0 avec Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="395b6-133">See [more examples](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) of using Azure CLI 2.0 commands with Azure Container Service.</span></span>
* <span data-ttu-id="395b6-134">En savoir plus sur les [pools d’agents contrôleur de domaine/système d’exploitation](../articles/container-service/dcos-swarm/container-service-dcos-agents.md) d’Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="395b6-134">Learn more about [DC/OS agent pools](../articles/container-service/dcos-swarm/container-service-dcos-agents.md) in Azure Container Service.</span></span>

