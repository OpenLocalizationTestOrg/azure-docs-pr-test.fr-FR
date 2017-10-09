Les solutions cloud Azure reposent sur des machines virtuelles (émulation de matériel informatique physique). Cela permet un conditionnement souple des déploiements logiciels et une meilleure consolidation des ressources par rapport au matériel physique. [Docker](https://www.docker.com) conteneurs et hello écosystème docker a façons hello considérablement développé vous pouvez développer, livrer et gérer la distribution des logiciels. Code d’application dans un conteneur est isolé à partir de la machine virtuelle d’hôte hello et autres conteneurs sur hello même machine virtuelle. Cette isolation vous confère une plus grande agilité de déploiement et de développement.

Azure offre hello Docker valeurs suivantes :

* [Nombreux](../articles/virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) [différents](../articles/virtual-machines/linux/dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) façons toocreate Docker héberge de conteneurs toosuit votre situation
* Hello [Service de conteneur Azure](https://azure.microsoft.com/documentation/services/container-service/) crée des clusters hôtes de conteneur à l’aide d’orchestrators comme **marathon** et **swarm**.
* [Le Gestionnaire de ressources Azure](../articles/azure-resource-manager/resource-group-overview.md) et [modèles de groupe de ressources](../articles/resource-group-authoring-templates.md) toosimplify déploiement et mise à jour des applications distribuées complexes
* Intégration avec un large éventail d’outils de gestion de configuration propriétaires et open source

Et parce que vous pouvez créer par programme des machines virtuelles et Linux conteneurs sur Azure, vous pouvez également utiliser les ordinateurs virtuels et le conteneur *orchestration* outils toocreate des groupes de Machines virtuelles (VM) et les applications toodeploy dans les deux Linux conteneurs et maintenant [les conteneurs Windows](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview).

Cet article présente non seulement ces concepts à un niveau élevé, il contient également des tonnes d’informations toomore de liens, des didacticiels, et produits liés à l’utilisation de toocontainer et cluster sur Azure. Si vous connaissez tout cela et que vous souhaitiez simplement les liens hello, ils sont directement au [outils permettant de travailler avec des conteneurs](#tools-for-working-with-azure-vms-and-containers).

## <a name="hello-difference-between-virtual-machines-and-containers"></a>différence Hello entre les conteneurs et les machines virtuelles
Les machines virtuelles s’exécutent dans un environnement isolé de virtualisation matérielle, fourni par un [hyperviseur](http://en.wikipedia.org/wiki/Hypervisor). Dans Azure, hello [virtuels](https://azure.microsoft.com/services/virtual-machines/) descripteurs de service que vous : créer des ordinateurs virtuels en choisissant le système d’exploitation de hello et en configurant &mdash;ou en chargeant une image de machine virtuelle personnalisée. Machines virtuelles sont une technologie éprouvée, « renforcé-nom », et il existe de nombreux outils disponibles toomanage hello du système d’exploitation et les applications qu’ils contiennent.  Les applications dans une machine virtuelle sont masquées à partir du système d’exploitation hôte de hello. Hello point de vue d’une application ou un utilisateur sur une machine virtuelle, hello machine virtuelle apparaît toobe un ordinateur physique autonome.

[Les conteneurs Linux](http://en.wikipedia.org/wiki/LXC) et ceux créés et hébergé à l’aide d’outils docker, n’utilisez pas un isolement de tooprovide hyperviseur. Avec des conteneurs, hôte de conteneur hello utilise, des processus et fonctionnalités de d’isolation de système de fichiers du conteneur de hello Linux noyau tooexpose toohello ses applications, certaines fonctionnalités de noyau et son propre système de fichiers isolés. Hello point de vue d’une application en cours d’exécution à l’intérieur d’un conteneur, le conteneur de hello apparaît toobe une instance unique de système d’exploitation. Une application à relation contenant-contenu ne peut pas voir les processus ou autres ressources en dehors de son conteneur.

Le nombre de ressources utilisées dans un conteneur Docker est beaucoup moins important que dans une machine virtuelle. Conteneurs docker employant un isolement et l’exécution de modèle d’application, qui ne partage pas de noyau hello de l’hôte Docker de hello. conteneur Hello est beaucoup plus faible encombrement du disque car elle n’inclut pas hello du système d’exploitation complet. Le temps de démarrage et l’espace disque requis sont considérablement inférieurs à ceux dans une machine virtuelle.
Conteneurs Windows offrent les mêmes avantages que les conteneurs Linux de hello pour les applications qui s’exécutent sur Windows. Les conteneurs Windows prennent en charge le format d’image hello Docker et les API Docker, mais ils peuvent également être gérés à l’aide de PowerShell. Deux runtimes de conteneur sont disponibles avec les conteneurs Windows, les conteneurs Windows Server et les conteneurs Hyper-V. Les conteneurs Hyper-V fournissent une couche supplémentaire d’isolation en hébergeant chaque conteneur dans une machine virtuelle très optimisée. toolearn d’informations sur les conteneurs Windows, consultez [sur les conteneurs Windows](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview). tooget main des conteneurs Windows dans Azure, découvrez comment trop[déployer un cluster du Service de conteneur Azure](../articles/container-service/dcos-swarm/container-service-deployment.md).

## <a name="what-are-containers-good-for"></a>Quels sont les avantages des conteneurs ?

Les conteneurs peuvent améliorer :

* code de l’application Hello vitesse peut être développé et partagé à grande échelle
* vitesse de Hello et une application peut être testée de confiance
* vitesse de Hello et peut être déployée une application de confiance

Les conteneurs s’exécutent sur un hôte conteneur&mdash;un système d’exploitation, et dans le cas d’Azure, une machine virtuelle Azure. Même si vous aimez déjà idée hello de conteneurs, vous aurez toujours tooneed une infrastructure de machine virtuelle héberge hello conteneurs, mais les avantages de hello sont les conteneurs ne se soucient pas sur les ordinateurs virtuels qu’ils sont en cours d’exécution (même si le conteneur de hello souhaite que Linux de Windows environnement d’exécution sera important, par exemple).


## <a name="what-are-containers-good-for"></a>Quels sont les avantages des conteneurs ?
Ils sont utiles dans de nombreux cas, mais ils encourageons&mdash;comme [Azure Cloud Services](https://azure.microsoft.com/services/cloud-services/) et [Azure Service Fabric](../articles/service-fabric/service-fabric-overview.md)&mdash;hello la création d’un service unique, orienté de microservice applications distribuées, dans une application qui repose sur plusieurs parties de petite taille, composables plutôt que sur les composants plus grandes et plus fortement couplées.

Cela est particulièrement vrai dans les environnements de cloud public comme Azure, dans lesquels vous louez des machines virtuelles quand et où vous le souhaitez. Non seulement vous bénéficiez de l’isolation, du déploiement rapide et des outils d’orchestration, mais vous pouvez prendre des décisions d’infrastructure des applications plus efficaces.

Par exemple, votre déploiement actuel est peut-être composé de 9 machines virtuelles Azure de grande taille pour une application distribuée et à haute disponibilité. Si les composants hello de cette application peuvent être déployés dans des conteneurs, vous pouvez être en mesure de toouse uniquement 4 machines virtuelles et déployer les composants de votre application à l’intérieur des 20 conteneurs pour la redondance et d’équilibrage de charge.

Il s’agit d’un exemple, bien entendu, mais pour cela, dans votre scénario, vous pouvez ajuster les pics toousage avec plusieurs conteneurs plutôt que davantage d’ordinateurs virtuels Azure et utiliser hello restant charge processeur globale beaucoup plus efficace qu’avant.

En outre, il existe de nombreux scénarios qui se prêtent pas les tooa microservices approche ; vous connaissez mieux que les conteneurs et les microservices vous aide.

### <a name="container-benefits-for-developers"></a>Avantages des conteneurs pour les développeurs
En règle générale, il est facile toosee que la technologie de conteneur est une étape suivante, mais il existe également des avantages plus spécifiques. Prenons l’exemple hello de conteneurs Docker. Cette rubrique ne sera pas aller plus loin dans Docker maintenant (lire [What ' s Docker ?](https://www.docker.com/whatisdocker/) de ce récit, ou [wikipedia](http://wikipedia.org/wiki/Docker_%28software%29)), mais Docker et son écosystème offrent des avantages considérables aux développeurs de tooboth et informatique professionnels de le.

Les développeurs prennent tooDocker conteneurs rapidement, car au-dessus de tous les rend à l’aide de conteneurs Windows et Linux simple :

* Ils peuvent utiliser des commandes simples, incrémentielle toocreate une image fixe toodeploy facile et que vous pouvant automatiser la création de ces images à l’aide d’un fichier dockerfile
* Ils peuvent partager ces images à l’aide de simples, [git](https://git-scm.com/)-style push et pull trop de commandes[public](https://registry.hub.docker.com/) ou [les registres privés docker](../articles/virtual-machines/virtual-machines-linux-docker-registry-in-blob-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Ils peuvent penser en termes de composants d’application isolés au lieu d’ordinateurs
* Ils peuvent utilisent un grand nombre d’outils qui comprennent les conteneurs Docker et différentes images de base

### <a name="container-benefits-for-operations-and-it-professionals"></a>Avantages des conteneurs pour les professionnels opérationnels et informatiques
INFORMATIQUE et aux professionnels de l’opérations également bénéficient de combinaison hello des conteneurs et des machines virtuelles.

* les services à relation contenant-contenu sont isolés de l’environnement d’exécution hôte de machines virtuelles ;
* le code à relation contenant-contenu est rigoureusement identique ;
* les services à relation contenant-contenu peuvent être démarrés, arrêtés et déplacés rapidement entre les environnements de développement, de test et de production.

Des fonctionnalités telles que ces&mdash;et qu’il existe plusieurs&mdash;excite entreprises établies, où les organisations de technologie des informations professionnelles ont travail hello des ressources de l’ajustement&mdash;, y compris la puissance de traitement pure&mdash; toonot requis de tâches toohello uniquement restent dans l’entreprise, mais augmenter la satisfaction des clients et atteindre. Petites entreprises, les éditeurs de logiciels indépendants et les démarrages ont exactement hello même exigence, mais ils peuvent décrire différemment.

## <a name="what-are-virtual-machines-good-for"></a>Quels sont les avantages des machines virtuelles ?
Les machines virtuelles fournissent backbone hello du cloud computing, et qui ne change pas. Si les ordinateurs virtuels démarrent plus lentement, ont un plus grand encombrement du disque et ne sont pas mappés directement tooa microservices architecture, ils ont très importants avantages :

1. Par défaut, elles offrent des protections de sécurité par défaut bien plus robustes pour l’ordinateur hôte.
2. Elles prennent en charge les principaux systèmes d’exploitation et les configurations d’applications
3. Elles disposent d’écosystèmes d’outils éprouvés pour le contrôle
4. Ils fournissent à l’exécution de hello conteneurs toohost d’environnement

Hello dernier élément est important, car une application de contenu requiert toujours un système d’exploitation et le type de processeur, en fonction d’appels hello permettront à application hello. Il est important tooremember installer les conteneurs sur des machines virtuelles, car ils contiennent des applications de hello souhaitées toodeploy ; conteneurs ne sont pas des remplacements pour les machines virtuelles ou des systèmes d’exploitation.

## <a name="high-level-feature-comparison-of-vms-and-containers"></a>Comparaison des fonctionnalités générales des machines virtuelles et des conteneurs
Hello tableau suivant décrit une très élevé des différences de type hello au niveau de fonctionnalité qui&mdash;, sans effort supplémentaire&mdash;existe entre les machines virtuelles Linux et les conteneurs. Notez que certaines fonctionnalités peut-être plus ou moins souhaitable selon votre propre application a besoin, et que comme avec tous les logiciels, un travail supplémentaire permet d’accroître la prise en charge des fonctionnalités, en particulier dans la zone hello de sécurité.

| Fonctionnalité | Machines virtuelles | Conteneurs |
|:--- | --- | --- |
| Prise en charge de la sécurité « par défaut » |tooa plus grande |tooa légèrement capitale |
| Mémoire nécessaire sur disque |Système d'exploitation complet, plus des applications |Conditions des applications uniquement |
| Temps nécessaire à le toostart |Nettement plus long : démarrage du système d’exploitation et chargement des applications |Sensiblement plus court : uniquement les applications doivent toostart, car le noyau est déjà en cours d’exécution |
| Portabilité |Portable avec une préparation adéquate |Portable dans le format d’image ; en général de format inférieur |
| Automatisation des images |Varie considérablement en fonction du système d'exploitation et des applications |[Registre Docker](https://registry.hub.docker.com/); autres |

## <a name="creating-and-managing-groups-of-vms-and-containers"></a>Création et gestion de groupes de machines virtuelles et de conteneurs
À ce stade, un architecte, développeur ou spécialiste des opérations informatiques pourrait penser : « Je peux automatiser TOUTES ces opérations ; le Data-Center-As-A-Service est une RÉALITÉ ! »

Vous avez raison, il peut être, et il existe de nombreux systèmes, nombre d'entre vous utilisez déjà, que vous pouvez gérer des groupes de machines virtuelles Azure et d’injecter du code personnalisé à l’aide de scripts, souvent avec hello [CustomScriptingExtension pour Windows](https://msdn.microsoft.com/library/azure/dn781373.aspx) ou Hello [CustomScriptingExtension pour Linux](https://azure.microsoft.com/blog/2014/08/20/automate-linux-vm-customization-tasks-using-customscript-extension/). Vous pouvez automatiser &mdash; vous l’avez peut-être déjà fait &mdash; vos déploiements Azure en utilisant PowerShell ou des scripts de l’interface de ligne de commande Azure.

Ces fonctionnalités sont souvent puis tootools migrés comme [Puppet](https://puppetlabs.com/) et [Chef](https://www.chef.io/) tooautomate hello création d’et de configuration pour les machines virtuelles à l’échelle. (Voici quelques liens trop[à l’aide de ces outils avec Azure](#tools-for-working-with-containers).)

### <a name="azure-resource-group-templates"></a>Modèles de groupes de ressources Azure
Plus, Azure ont été publiées récemment hello [gestion des ressources Azure](../articles/resource-manager-deployment-model.md) l’API REST et mis à jour toouse d’outils PowerShell et CLI d’Azure il facilement. Vous pouvez déployer, modifier ou redéployer les topologies d’ensemble de l’application à l’aide [modèles Azure Resource Manager](../articles/resource-group-authoring-templates.md) à l’aide des API de gestion de ressources Azure hello :

* Hello [portail Azure à l’aide de modèles](https://github.com/Azure/azure-quickstart-templates)&mdash;indicateur, utilisez le bouton de « DeployToAzure » hello
* Hello [CLI d’Azure](../articles/virtual-machines/linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="deployment-and-management-of-entire-groups-of-azure-vms-and-containers"></a>Déploiement et gestion de groupes entiers de machines virtuelles Azure et de conteneurs
Plusieurs systèmes courants peuvent déployer des groupes entiers de machines virtuelles et installer Docker (ou autres systèmes d’hébergement de conteneurs Linux ) comme un groupe automatisable. Pour obtenir des liens directs, consultez hello [conteneurs et les outils](#containers-and-vm-technologies) section ci-dessous. Il existe plusieurs systèmes qui effectuent cette tooa plus ou moins grande, et cette liste n’est pas exhaustive. En fonction de vos compétences et scénarios, ils peuvent se révéler utiles ou non

Docker possède son propre jeu d’outils de création de machines virtuelles ([docker-machine](../articles/virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)), ainsi qu’un outil de gestion des clusters, conteneur de Docker et à équilibrage de charge ([swarm](../articles/virtual-machines/virtual-machines-linux-docker-swarm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). En outre, hello [Extension de machine virtuelle Azure Docker](https://github.com/Azure/azure-docker-extension/blob/master/README.md) est fourni avec prise en charge par défaut de [ `docker-compose` ](https://docs.docker.com/compose/), qui peut déployer configuré des conteneurs d’applications sur plusieurs conteneurs.

En outre, vous pouvez essayer le [système d'exploitation de centre de données (Data Center Operating System, DCOS) de Mesosphere](http://docs.mesosphere.com). DCOS est basée sur hello open source [mesos](http://mesos.apache.org/) « noyau de systèmes distribués » qui permet de vous tootreat votre centre de données en tant qu’un seul service adressable. DCOS intègre des packages pour plusieurs systèmes importants tels que [Spark](http://spark.apache.org/), [Kafka](http://kafka.apache.org/) et d’autres, ainsi que des services intégrés tels que [Marathon](https://mesosphere.github.io/marathon/) (un système de contrôle de conteneurs) et [Chronos](https://mesos.github.io/chronos/) (un planificateur distribué). Mesos est un dérivé de leçons tirées de Twitter, d’AirBnb et autres entreprises web à grande échelle. Vous pouvez également utiliser **swarm** en tant que moteur d’orchestration hello.

En outre, [kubernetes](https://azure.microsoft.com/blog/2014/08/28/hackathon-with-kubernetes-on-azure/) est un système open source pour la gestion de groupes de machines virtuelles et de conteneurs, fondé sur les enseignements tirés de Google. Vous pouvez même utiliser [kubernetes avec entrelacé prise en charge de la mise en réseau tooprovide](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/getting-started-guides/coreos/azure/README.md#kubernetes-on-azure-with-coreos-and-weave).

[Deis](http://deis.io/overview/) est open source « Platform-as-a-Service » (PaaS) qui le rend facile toodeploy et gérer les applications sur vos serveurs. Deis s’appuie sur Docker et CoreOS tooprovide un léger PaaS un Heroku basées sur un flux de travail.

[CoreOS](https://coreos.com/os/docs/latest/booting-on-azure.html), une distribution Linux avec un encombrement optimisé, la prise en charge Docker et leur propre système de conteneurs appelé [rkt](https://github.com/coreos/rkt) disposent également d’un outil de gestion de groupes de conteneurs appelé [fleet](https://coreos.com/fleet/docs/latest/).

Ubuntu, une autre distribution Linux très populaire, prend très bien en charge Docker mais également les [clusters Linux (de type LXC)](https://help.ubuntu.com/lts/serverguide/lxc.html).

## <a name="tools-for-working-with-azure-vms-and-containers"></a>Outils de travail avec les machines virtuelles Azure et les conteneurs
Le travail avec les conteneurs et les machines virtuelles Azure requiert des outils. Cette section fournit une liste de quelques-unes des concepts plus utile ou importantes de hello et outils sur des conteneurs, des groupes et configuration de supérieure hello et orchestration utilisé avec les.

> [!NOTE]
> Cette zone change très rapidement, et pendant que nous ferons de notre tookeep meilleures cette rubrique et ses liens des toodate, il peut également être impossible, cette tâche. Assurez-vous que vous effectuez une recherche sur intéressantes tookeep sujets des toodate !
>
>

### <a name="containers-and-vm-technologies"></a>Technologies relatives aux conteneurs et aux machines virtuelles
Certaines technologies de conteneurs Linux :

* [Docker](https://www.docker.com)
* [LXC](https://linuxcontainers.org/)
* [CoreOS et rkt](https://github.com/coreos/rkt)
* [Open Container Project](http://opencontainers.org/)
* [RancherOS](http://rancher.com/rancher-os/)

Liens pour les conteneurs Windows :

* [Conteneurs Windows](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview)

Liens pour Docker pour Visual Studio :

* [Visual Studio Tools pour Docker](https://docs.microsoft.com/en-us/dotnet/core/docker/visual-studio-tools-for-docker)

Outils Docker :

* [Démon Docker](https://docs.docker.com/installation/#installation)
* Clients Docker
  * [Windows Docker Client pour Chocolatey](https://chocolatey.org/packages/docker)
  * [Instructions d’installation de Docker](https://docs.docker.com/installation/#installation)

Docker sur Microsoft Azure :

* [Extension Docker VM pour Linux dans Azure](../articles/virtual-machines/linux/dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Guide de l’utilisateur de l’extension Docker VM Azure](https://github.com/Azure/azure-docker-extension/blob/master/README.md)
* [À l’aide de hello Extension de machine virtuelle Docker à partir de hello Azure Interface de ligne (Azure)](../articles/virtual-machines/linux/classic/cli-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [À l’aide de hello Extension de machine virtuelle Docker à partir de hello portail Azure](../articles/virtual-machines/linux/classic/portal-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [La machine docker toouse sur Azure](../articles/virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Comment docker toouse avec essaim sur Azure](../articles/virtual-machines/virtual-machines-linux-docker-swarm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Prise en main de Docker et Compose sur Azure](../articles/virtual-machines/linux/docker-compose-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [À l’aide d’un toocreate de modèle de groupe de ressources Azure un hôte Docker sur Azure rapidement](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu)
* [Hello prise en charge intégrée pour `compose` ](https://github.com/Azure/azure-docker-extension#11-public-configuration-keys) pour les applications qu’il contient
* [Déploiement de votre propre registre Docker privé sur Azure](../articles/virtual-machines/virtual-machines-linux-docker-registry-in-blob-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Distributions Linux et exemples Azure :

* [CoreOS](https://coreos.com/os/docs/latest/booting-on-azure.html)

Configuration, gestion de clusters et orchestration de conteneurs :

* [Fleet sur CoreOS](https://coreos.com/fleet/docs/latest/)
* Deis

  * [Terminer le déploiement de cluster guide tooautomated Kubernetes avec CoreOS et tressé](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/getting-started-guides/coreos/azure/README.md#kubernetes-on-azure-with-coreos-and-weave)
  * [Visualiseur Kubernetes](https://azure.microsoft.com/blog/2014/08/28/hackathon-with-kubernetes-on-azure/)
* [Mesos](http://mesos.apache.org/)

  * [Système d’exploitation de centre de données (Data Center Operating System, DCOS) de Mesosphere](https://docs.mesosphere.com/1.7/overview/design/azure-container-service/)
* [Jenkins](https://jenkins.io/) et [Hudson](http://hudson-ci.org/)

  * [Plug-in Jenkins VM Agent pour Azure](https://wiki.jenkins.io/display/JENKINS/Azure+VM+Agents+plugin)
  * [Référentiel GitHub : Plug-in Jenkins Storage pour Azure](https://github.com/jenkinsci/windows-azure-storage-plugin)
  * [Tiers : Plug-in Hudson Slave pour Azure](http://wiki.hudson-ci.org/display/HUDSON/Azure+Slave+Plugin)
  * [Tiers : Plug-in Hudson Storage pour Azure](https://github.com/hudson3-plugins/windows-azure-storage-plugin)
* [Azure Automation](https://azure.microsoft.com/services/automation/)

  * [Vidéo : Comment tooUse Azure Automation avec les machines virtuelles Linux](http://channel9.msdn.com/Shows/Azure-Friday/Azure-Automation-104-managing-Linux-and-creating-Modules-with-Joe-Levy)
* Configuration d'état souhaité Powershell pour Linux

  * [Blog : Comment toodo DSC Powershell pour Linux](http://blogs.technet.com/b/privatecloud/archive/2014/05/19/powershell-dsc-for-linux-step-by-step.aspx)
  * [GitHub : Configuration d’état souhaité du client Docker](https://github.com/anweiss/DockerClientDSC)

## <a name="next-steps"></a>Étapes suivantes
Découvrez [Docker](https://www.docker.com) et les [conteneurs Windows](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview).

<!--Anchors-->
[microservices]: http://martinfowler.com/articles/microservices.html
[microservice]: http://martinfowler.com/articles/microservices.html
<!--Image references-->
