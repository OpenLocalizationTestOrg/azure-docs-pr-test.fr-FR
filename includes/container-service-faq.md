# <a name="container-service-frequently-asked-questions"></a>Forum aux questions : Container Service

## <a name="orchestrators"></a>Orchestrators

### <a name="which-container-orchestrators-do-you-support-on-azure-container-service"></a>Quels orchestrators de conteneur sont pris en charge sur Azure Container Service ? 

Une prise en charge est disponible pour CD/OS open source, Docker Swarm et Kubernetes. Pour plus d’informations, consultez hello [vue d’ensemble](../articles/container-service/kubernetes/container-service-intro-kubernetes.md).
 
### <a name="do-you-support-docker-swarm-mode"></a>Le mode Docker Swarm est-il pris en charge ? 

Actuellement essaim mode n’est pas pris en charge, mais il est prévu de service hello. 

### <a name="does-azure-container-service-support-windows-containers"></a>Azure Container Service prend-il en charge les conteneurs Windows ?  

Les conteneurs Linux sont actuellement pris en charge par tous les orchestrators. La prise en charge des conteneurs Windows avec Kubernetes est en version préliminaire.

### <a name="do-you-recommend-a-specific-orchestrator-in-azure-container-service"></a>Recommandez-vous un orchestrator spécifique dans Azure Container Service ? 
Nous ne recommandons généralement pas un orchestrator spécifique. Si vous avez aucune expérience avec l’un des orchestrators de hello pris en charge, vous pouvez appliquer cette expérience dans le Service de conteneur Azure. Les tendances des données suggère toutefois que DC/OS est éprouvé en production pour les charges de travail Big Data et IoT, que Kubernetes est adapté aux charges de travail natif de cloud, et que Docker Swarm est connu pour son intégration aux outils Docker et sa simplicité de prise en main.

En fonction de votre scénario, vous pouvez également créer et gérer des solutions de conteneur personnalisé avec d’autres services Azure. Ces services incluent les [machines virtuelles](../articles/virtual-machines/linux/overview.md), [Service Fabric](../articles/service-fabric/service-fabric-overview.md), [Web Apps](../articles/app-service-web/app-service-web-overview.md) et [lot](../articles/batch/batch-technical-overview.md).  

### <a name="what-is-hello-difference-between-azure-container-service-and-acs-engine"></a>Qu’est la différence hello entre le Service de conteneur Azure et des services ACS moteur ? 
Service de conteneur Azure est un service Azure reposant sur le contrat SLA avec les fonctionnalités de l’API Azure hello portail Azure et les outils de ligne de commande Azure. service de Hello permet que vous tooquickly implémenter et gérer des clusters en cours d’exécution d’outils standard de conteneur d’orchestration avec un nombre relativement restreint d’options de configuration. 

[Moteur d’ACS](http://github.com/Azure/acs-engine) est un projet open source qui permet la configuration de cluster power utilisateurs toocustomize hello à tous les niveaux. Cette configuration de hello tooalter capacité d’infrastructure et de logiciels signifie que nous ne proposons aucun contrat SLA pour le moteur d’ACS. Prise en charge est gérée via le projet open source de hello sur GitHub, plutôt que via des canaux Microsoft officiels. 

## <a name="cluster-management"></a>Gestion de cluster

### <a name="how-do-i-create-ssh-keys-for-my-cluster"></a>Comment créer des clés SSH pour mon cluster ?

Vous pouvez utiliser les outils standard sur votre système d’exploitation de toocreate une paire de clés SSH RSA publique et privée pour l’authentification sur les ordinateurs virtuels Linux hello pour votre cluster. Pour obtenir des instructions, consultez hello [OS X et Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) ou [Windows](../articles/virtual-machines/linux/ssh-from-windows.md) des conseils. 

Si vous utilisez [Azure CLI 2.0 commandes](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) toodeploy un conteneur de service de cluster, SSH clés peuvent être générées automatiquement pour votre cluster.

### <a name="how-do-i-create-a-service-principal-for-my-kubernetes-cluster"></a>Comment créer un principal du service pour mon cluster Kubernetes ?

Un ID de principal de service Azure Active Directory et le mot de passe sont également nécessaire toocreate un cluster Kubernetes dans le Service de conteneur Azure. Pour plus d’informations, consultez [sur le principal du service pour un cluster Kubernetes hello](../articles/container-service/kubernetes/container-service-kubernetes-service-principal.md).

Si vous utilisez [Azure CLI 2.0 commandes](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) toodeploy un Kubernetes service de cluster, les informations d’identification principales peuvent être générées automatiquement pour votre cluster.

### <a name="how-large-a-cluster-can-i-create"></a>Si je crée un cluster, quelle doit être sa taille maximale ?
Vous pouvez créer un cluster incluant 1, 3 ou 5 nœuds principaux. Vous pouvez choisir des nœuds de l’agent too100.

> [!IMPORTANT]
> Pour les clusters de grande taille et en fonction de la taille de machine virtuelle que vous choisissez pour vos nœuds de hello, vous devrez peut-être le quota de cœurs tooincrease hello dans votre abonnement. toorequest une augmentation du quota, ouvrir une [demande de support technique en ligne](../articles/azure-supportability/how-to-create-azure-support-request.md) sans frais. Si vous utilisez un [compte gratuit Azure](https://azure.microsoft.com/free/), vous pouvez seulement utiliser un nombre limité de cœurs de calcul Azure.
> 

### <a name="how-do-i-increase-hello-number-of-masters-after-a-cluster-is-created"></a>Comment augmenter nombre hello des maîtres d’après la création d’un cluster ? 
Une fois que le cluster de hello est créé, nombre hello de masques est fixe et ne peut pas être modifié. Dans l’idéal, lors de la création de hello du cluster de hello, sélectionnez plusieurs maîtres pour la haute disponibilité.

### <a name="how-do-i-increase-hello-number-of-agents-after-a-cluster-is-created"></a>Comment augmenter nombre hello d’agents après la création d’un cluster ? 
Vous pouvez adapter le nombre hello d’agents dans le cluster de hello à l’aide de hello portail Azure ou les outils de ligne de commande. Consultez [Mise à l’échelle d’un cluster Azure Container Service](../articles/container-service/kubernetes/container-service-scale.md).

### <a name="what-are-hello-urls-of-my-masters-and-agents"></a>Quelles sont les URL hello Mes formes de base et les agents ? 
URL Hello du cluster de ressources dans le Service de conteneur Azure reposent sur hello vous fournissez et hello nom Hello région Azure que vous avez choisi pour le déploiement de préfixe de nom DNS. Par exemple, le nom de domaine complet (FQDN) hello du nœud principal de hello est de ce formulaire :

``` 
DNSnamePrefix.AzureRegion.cloudapp.azure.net
```

Vous pouvez trouver des URL utilisées pour votre cluster dans hello portail Azure, hello Explorateur de ressources Azure ou d’autres outils Azure.

### <a name="how-do-i-tell-which-orchestrator-version-is-running-in-my-cluster"></a>Comment savoir quelle version d’Orchestrator est en cours d’exécution dans mon cluster ?

* Contrôleur de domaine/système d’exploitation : Consultez hello [documentation de mésosphère](https://support.mesosphere.com/hc/en-us/articles/207719793-How-to-get-the-DCOS-version-from-the-command-line-)
* Docker Swarm : Exécuter `docker version`
* Kubernetes : Exécuter `kubectl version`

### <a name="how-do-i-upgrade-hello-orchestrator-after-deployment"></a>Comment mettre à niveau hello orchestrator après le déploiement ?

Actuellement, Service de conteneur Azure ne fournit pas version hello tooupgrade des outils d’orchestrator hello que vous avez déployé sur votre cluster. Si Container Service prend en charge une version ultérieure, vous pouvez déployer un nouveau cluster. Une autre option consiste outils orchestrator spécifiques de toouse s’ils sont disponible tooupgrade un cluster en place. Par exemple, consultez [mise à niveau DC/OS](https://dcos.io/docs/1.8/administration/upgrading/).
 
### <a name="where-do-i-find-hello-ssh-connection-string-toomy-cluster"></a>Où trouver le cluster de toomy chaîne hello SSH connexion ?

Vous trouverez la chaîne de connexion hello Bonjour portail Azure, ou à l’aide des outils de ligne de commande Azure. 

1. Dans le portail de hello, accédez toohello groupe de ressources pour le déploiement de cluster hello.  

2. Cliquez sur **vue d’ensemble** et cliquez sur le lien hello pour **déploiements** sous **Essentials**. 

3. Bonjour **l’historique de déploiement** panneau, cliquez sur déploiement hello qui a un nom commençant par **microsoft-acs** suivie d’une date de déploiement. Exemple : microsoft-acs-201701310000.  

4. Sur hello **Résumé** sous **sorties**, vous trouverez plusieurs liens de cluster. **SSHMaster0** fournit un SSH connexion chaîne toohello première maître dans votre cluster de service de conteneur. 

Comme indiqué précédemment, vous pouvez également utiliser Windows Azure tools toofind hello nom de domaine complet du principal de hello. Ils établissent une connexion SSH master toohello à l’aide de hello FQDN du maître de hello et nom d’utilisateur hello que vous avez spécifié lors de la création du cluster de hello. Par exemple :

```bash
ssh userName@masterFQDN –A –p 22 
```

Pour plus d’informations, consultez [cluster de Service de conteneur Azure Connect tooan](../articles/container-service/kubernetes/container-service-connect.md).

## <a name="next-steps"></a>Étapes suivantes

* [En savoir plus](../articles/container-service/kubernetes/container-service-intro-kubernetes.md) sur Azure Container Service.
* Déployer un cluster du service de conteneur à l’aide de hello [portal](../articles/container-service/dcos-swarm/container-service-deployment.md) ou [Azure CLI 2.0](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md).
