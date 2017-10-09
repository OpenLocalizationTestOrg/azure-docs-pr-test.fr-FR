# <a name="scale-agent-nodes-in-a-container-service-cluster"></a>Mettre à l’échelle des nœuds d’agent dans un cluster Container Service
Après avoir [déploiement d’un cluster du Service de conteneur Azure](../articles/container-service/dcos-swarm/container-service-deployment.md), vous devrez peut-être le nombre de hello toochange de nœuds de l’agent. Vous risquez par exemple d’avoir besoin de davantage d’agents afin de pouvoir exécuter davantage d’instances ou d’applications de conteneur. 

Vous pouvez modifier nombre hello de nœuds de l’agent dans un cluster de contrôleur de domaine/système d’exploitation, Docker Swarm ou Kubernetes à l’aide de hello portail Azure ou hello Azure CLI 2.0. 

## <a name="scale-with-hello-azure-portal"></a>Mettre à l’échelle par hello portail Azure

1. Bonjour [portail Azure](https://portal.azure.com), recherchez **services de conteneur**, puis cliquez sur le service de conteneur hello que vous souhaitez toomodify.
2. Bonjour **service de conteneur** panneau, cliquez sur **Agents**.
3. Dans **nombre d’ordinateurs virtuels**, entrez nombre hello souhaité de nœuds d’agents.

    ![Mettre à l’échelle d’un pool dans le portail de hello](./media/container-service-scale/container-service-scale-portal.png)

4. configuration de hello toosave, cliquez sur **enregistrer**.

## <a name="scale-with-hello-azure-cli-20"></a>Mettre à l’échelle par hello Azure CLI 2.0

Assurez-vous que vous [installé](/cli/azure/install-az-cli2) hello dernière Azure CLI 2.0 et consigné dans tooan compte azure (`az login`).

### <a name="see-hello-current-agent-count"></a>Voir le nombre actuel de l’agent de hello
nombre de hello toosee d’agents actuellement dans un cluster de hello, exécutez hello `az acs show` commande. Configuration de cluster hello s’affiche. Hello, par exemple, la commande affiche hello configuration du service de conteneur hello nommé suivante `containerservice-myACSName` dans le groupe de ressources hello `myResourceGroup`:

```azurecli
az acs show -g myResourceGroup -n containerservice-myACSName
```

commande Hello retourne le nombre de hello d’agents Bonjour `Count` valeur sous `AgentPoolProfiles`.

### <a name="use-hello-az-acs-scale-command"></a>Utilisez hello az commande de mise à l’échelle des services acs
nombre de hello toochange de nœuds de l’agent, exécutez hello `az acs scale` hello de commande et fournissez **groupe de ressources**, **nom de service de conteneur**et hello souhaité **nouveau nombre d’agents**. Si vous utilisez un nombre inférieur ou supérieur, vous descendez ou montez en puissance, respectivement.

Par exemple, le nombre de hello toochange d’agents dans hello précédente too10 de cluster, tapez Bonjour de commande suivante :

```azurecli
az acs scale -g myResourceGroup -n containerservice-myACSName --new-agent-count 10
```

Bonjour Azure CLI 2.0 retourne une chaîne JSON représentant la nouvelle configuration du service de conteneur hello, y compris le nombre de l’agent de nouveau hello de hello.

Pour plus d’options de commande, exécutez `az acs scale --help`.

## <a name="scaling-considerations"></a>Mise à l'échelle - Éléments à prendre en compte

* nombre de Hello de nœuds de l’agent doit être compris entre 1 et 100 (inclus). 

* Votre quota de cœurs peut limiter le nombre de hello de nœuds de l’agent dans un cluster.

* Opérations de mise à l’échelle de nœud de l’agent sont un ensemble d’échelle de machine virtuelle Azure tooan appliqué qui contient le pool d’agents hello. Dans un cluster de contrôleur de domaine/système d’exploitation, seuls les nœuds de l’agent dans le pool privé de hello à l’échelle par les opérations hello illustrées dans cet article.

* En fonction d’orchestrator hello que vous déployez dans votre cluster, vous pouvez faire évoluer séparément nombre hello d’instances d’un conteneur en cours d’exécution sur le cluster de hello. Par exemple, dans un cluster de contrôleur de domaine/système d’exploitation, utilisez hello [Marathon UI](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) toochange hello quantité, pour les instances d’une application conteneur.

* Actuellement, la mise à l’échelle automatique de nœuds d’agent dans un cluster du service de conteneur n’est pas prise en charge.

## <a name="next-steps"></a>Étapes suivantes
* Consultez [d’autres exemples](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) d’utilisation des commandes de la CLI Azure 2.0 avec Azure Container Service.
* En savoir plus sur les [pools d’agents contrôleur de domaine/système d’exploitation](../articles/container-service/dcos-swarm/container-service-dcos-agents.md) d’Azure Container Service.

