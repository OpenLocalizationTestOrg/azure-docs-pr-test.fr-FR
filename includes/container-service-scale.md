# <a name="scale-agent-nodes-in-a-container-service-cluster"></a><span data-ttu-id="f972f-101">Mettre à l’échelle des nœuds d’agent dans un cluster Container Service</span><span class="sxs-lookup"><span data-stu-id="f972f-101">Scale agent nodes in a Container Service cluster</span></span>
<span data-ttu-id="f972f-102">Après le [déploiement d’un cluster Azure Container Service](../articles/container-service/dcos-swarm/container-service-deployment.md), vous devez peut-être modifier le nombre de nœuds de l’agent.</span><span class="sxs-lookup"><span data-stu-id="f972f-102">After [deploying an Azure Container Service cluster](../articles/container-service/dcos-swarm/container-service-deployment.md), you might need to change the number of agent nodes.</span></span> <span data-ttu-id="f972f-103">Vous risquez par exemple d’avoir besoin de davantage d’agents afin de pouvoir exécuter davantage d’instances ou d’applications de conteneur.</span><span class="sxs-lookup"><span data-stu-id="f972f-103">For example, you might need more agents so you can run more container applications or instances.</span></span> 

<span data-ttu-id="f972f-104">Vous pouvez modifier le nombre de nœuds de l’agent dans un cluster DC/OS, Docker Swarm ou Kubernetes à l’aide du portail Azure ou d’Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="f972f-104">You can change the number of agent nodes in a DC/OS, Docker Swarm, or Kubernetes cluster by using the Azure portal or the Azure CLI 2.0.</span></span> 

## <a name="scale-with-the-azure-portal"></a><span data-ttu-id="f972f-105">Mise à l’échelle avec le portail Azure</span><span class="sxs-lookup"><span data-stu-id="f972f-105">Scale with the Azure portal</span></span>

1. <span data-ttu-id="f972f-106">Dans le [portail Azure](https://portal.azure.com), recherchez les **services de conteneur**, puis cliquez sur le service de conteneur que vous souhaitez modifier.</span><span class="sxs-lookup"><span data-stu-id="f972f-106">In the [Azure portal](https://portal.azure.com), browse for **Container services**, and then click the container service that you want to modify.</span></span>
2. <span data-ttu-id="f972f-107">Dans le panneau **Service de conteneur**, cliquez sur **Agents**.</span><span class="sxs-lookup"><span data-stu-id="f972f-107">In the **Container service** blade, click **Agents**.</span></span>
3. <span data-ttu-id="f972f-108">Dans **Nombre de machines virtuelles**, entrez le nombre souhaité de nœuds d’agent.</span><span class="sxs-lookup"><span data-stu-id="f972f-108">In **VM Count**, enter the desired number of agents nodes.</span></span>

    ![Mise à l’échelle d’un pool dans le portail](./media/container-service-scale/container-service-scale-portal.png)

4. <span data-ttu-id="f972f-110">Pour enregistrer la configuration, cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="f972f-110">To save the configuration, click **Save**.</span></span>

## <a name="scale-with-the-azure-cli-20"></a><span data-ttu-id="f972f-111">Mise à l’échelle avec la CLI Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="f972f-111">Scale with the Azure CLI 2.0</span></span>

<span data-ttu-id="f972f-112">Assurez-vous d’avoir [installé](/cli/azure/install-az-cli2) la dernière version de la CLI Azure 2.0 et d’être connecté à un compte Azure (`az login`).</span><span class="sxs-lookup"><span data-stu-id="f972f-112">Make sure that you [installed](/cli/azure/install-az-cli2) the latest Azure CLI 2.0 and logged in to an azure account (`az login`).</span></span>

### <a name="see-the-current-agent-count"></a><span data-ttu-id="f972f-113">Affichage du nombre actuel d’agents</span><span class="sxs-lookup"><span data-stu-id="f972f-113">See the current agent count</span></span>
<span data-ttu-id="f972f-114">Pour afficher le nombre d’agents actuellement dans le cluster, exécutez la commande `az acs show`.</span><span class="sxs-lookup"><span data-stu-id="f972f-114">To see the number of agents currently in the cluster, run the `az acs show` command.</span></span> <span data-ttu-id="f972f-115">Elle permet d’afficher la configuration du cluster.</span><span class="sxs-lookup"><span data-stu-id="f972f-115">This shows the cluster configuration.</span></span> <span data-ttu-id="f972f-116">Par exemple, la commande suivante affiche la configuration du service de conteneur nommé `containerservice-myACSName` dans le groupe de ressources `myResourceGroup` :</span><span class="sxs-lookup"><span data-stu-id="f972f-116">For example, the following command shows the configuration of the container service named `containerservice-myACSName` in the resource group `myResourceGroup`:</span></span>

```azurecli
az acs show -g myResourceGroup -n containerservice-myACSName
```

<span data-ttu-id="f972f-117">La commande renvoie le nombre d’agents dans la valeur `Count` sous `AgentPoolProfiles`.</span><span class="sxs-lookup"><span data-stu-id="f972f-117">The command returns the number of agents in the `Count` value under `AgentPoolProfiles`.</span></span>

### <a name="use-the-az-acs-scale-command"></a><span data-ttu-id="f972f-118">Utilisation de la commande az acs scale</span><span class="sxs-lookup"><span data-stu-id="f972f-118">Use the az acs scale command</span></span>
<span data-ttu-id="f972f-119">Pour modifier le nombre de nœuds de l’agent, exécutez la commande `az acs scale` et indiquez le **groupe de ressources**, le **nom du service de conteneur** et le **nombre de nouveaux agents**.</span><span class="sxs-lookup"><span data-stu-id="f972f-119">To change the number of agent nodes, run the `az acs scale` command and supply the **resource group**, **container service name**, and the desired **new agent count**.</span></span> <span data-ttu-id="f972f-120">Si vous utilisez un nombre inférieur ou supérieur, vous descendez ou montez en puissance, respectivement.</span><span class="sxs-lookup"><span data-stu-id="f972f-120">By using a smaller or higher number, you can scale down or up, respectively.</span></span>

<span data-ttu-id="f972f-121">Par exemple, pour modifier le nombre d’agents dans le précédent cluster en 10, tapez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f972f-121">For example, to change the number of agents in the previous cluster to 10, type the following command:</span></span>

```azurecli
az acs scale -g myResourceGroup -n containerservice-myACSName --new-agent-count 10
```

<span data-ttu-id="f972f-122">L’interface Azure CLI 2.0 renvoie une chaîne JSON représentant la nouvelle configuration du service de conteneur, avec notamment le nouveau nombre d’agents.</span><span class="sxs-lookup"><span data-stu-id="f972f-122">The Azure CLI 2.0 returns a JSON string representing the new configuration of the container service, including the new agent count.</span></span>

<span data-ttu-id="f972f-123">Pour plus d’options de commande, exécutez `az acs scale --help`.</span><span class="sxs-lookup"><span data-stu-id="f972f-123">For more command options, run `az acs scale --help`.</span></span>

## <a name="scaling-considerations"></a><span data-ttu-id="f972f-124">Mise à l'échelle - Éléments à prendre en compte</span><span class="sxs-lookup"><span data-stu-id="f972f-124">Scaling considerations</span></span>

* <span data-ttu-id="f972f-125">Le nombre de nœuds de l’agent doit être compris entre 1 et 100 (inclus).</span><span class="sxs-lookup"><span data-stu-id="f972f-125">The number of agent nodes must be between 1 and 100, inclusive.</span></span> 

* <span data-ttu-id="f972f-126">Votre quota de cœurs peut limiter le nombre de nœuds de l’agent dans un cluster.</span><span class="sxs-lookup"><span data-stu-id="f972f-126">Your cores quota can limit the number of agent nodes in a cluster.</span></span>

* <span data-ttu-id="f972f-127">Les opérations de mise à l’échelle de nœud de l’agent sont appliquées à un groupe de machines virtuelles Azure identiques qui contient le pool de l’agent.</span><span class="sxs-lookup"><span data-stu-id="f972f-127">Agent node scaling operations are applied to an Azure virtual machine scale set that contains the agent pool.</span></span> <span data-ttu-id="f972f-128">Dans un cluster de contrôleur de domaine/système d’exploitation, seuls les nœuds de l’agent dans le pool privé sont mis à l’échelle par les opérations indiquées dans cet article.</span><span class="sxs-lookup"><span data-stu-id="f972f-128">In a DC/OS cluster, only agent nodes in the private pool are scaled by the operations shown in this article.</span></span>

* <span data-ttu-id="f972f-129">Selon l’orchestrateur que vous déployez dans votre cluster, vous pouvez mettre à l’échelle séparément le nombre d’instances d’un conteneur en cours d’exécution sur le cluster.</span><span class="sxs-lookup"><span data-stu-id="f972f-129">Depending on the orchestrator you deploy in your cluster, you can separately scale the number of instances of a container running on the cluster.</span></span> <span data-ttu-id="f972f-130">Par exemple, dans un cluster de contrôleur de domaine/système d’exploitation, utilisez l’[interface utilisateur Marathon](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) pour modifier le nombre d’instances d’une application conteneur.</span><span class="sxs-lookup"><span data-stu-id="f972f-130">For example, in a DC/OS cluster, use the [Marathon UI](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) to change the number of instances of a container application.</span></span>

* <span data-ttu-id="f972f-131">Actuellement, la mise à l’échelle automatique de nœuds d’agent dans un cluster du service de conteneur n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="f972f-131">Currently, autoscaling of agent nodes in a container service cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f972f-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f972f-132">Next steps</span></span>
* <span data-ttu-id="f972f-133">Consultez [d’autres exemples](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) d’utilisation des commandes de la CLI Azure 2.0 avec Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="f972f-133">See [more examples](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) of using Azure CLI 2.0 commands with Azure Container Service.</span></span>
* <span data-ttu-id="f972f-134">En savoir plus sur les [pools d’agents contrôleur de domaine/système d’exploitation](../articles/container-service/dcos-swarm/container-service-dcos-agents.md) d’Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="f972f-134">Learn more about [DC/OS agent pools](../articles/container-service/dcos-swarm/container-service-dcos-agents.md) in Azure Container Service.</span></span>

