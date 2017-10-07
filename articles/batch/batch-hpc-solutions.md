---
title: "aaaBatch et solutions HPC dans Azure cloud : hello | Documents Microsoft"
description: "Découvrez les scénarios de Batch Computing et de calcul haute performance (HPC et Big Compute) et les solutions proposées dans Azure"
services: batch, virtual-machines, cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
ms.assetid: aab5401d-2baf-4cf2-bf20-ad224de33888
ms.service: batch
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c5a3c8859d1f95040bcdad15942a815d71eb4486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="batch-and-hpc-solutions-for-large-scale-computing-workloads"></a>Solutions Batch et HPC pour les charges de travail de calcul à grande échelle

Azure offre des solutions efficaces et évolutives pour le Batch Computing et le calcul haute performance (HPC), également désignés ensemble sous le terme de *Big Compute*. En savoir plus ici sur les charges de travail Big Compute et toosupport des services de Azure les, ou accéder directement trop[scénarios de solution](#scenarios) plus loin dans cet article. Cet article est principalement destiné aux décideurs techniques, les responsables informatiques et aux éditeurs de logiciels, mais les autres professionnels de l’informatique et développeurs peuvent utiliser informatique toofamiliarize eux-mêmes à ces solutions.

Les organisations ont des problèmes informatiques à grande échelle : analyse et conception d’ingénierie, rendu d’image, modélisation complexe, simulations Monte Carlo, calculs de risques financiers, etc. Azure permet aux organisations de résoudre ces problèmes avec les ressources hello, échelle et planification que dont ils ont besoin. Avec Azure, les entreprises peuvent :

* Créer des solutions hybrides, étendre un cloud de toohello local HPC cluster toooffload pointe les charges de travail
* Exécuter des outils de cluster HPC et des charges de travail entièrement dans Azure
* Utiliser les services Azure évolutifs et non managées telles que [lot](https://azure.microsoft.com/documentation/services/batch/) les charges de travail intensives toorun sans avoir toodeploy et gérer une infrastructure de calcul

Bien que dépasse hello de cet article, Azure fournit également aux développeurs et les partenaires un ensemble complet de fonctionnalités, les choix d’architecture et développement outils toobuild à grande échelle personnalisée Big Compute des workflows. Et un écosystème de partenaires croissante est prêt toohelp vous rendre vos charges de travail Big Compute productive dans hello cloud Azure.

## <a name="batch-and-hpc-applications"></a>Applications Batch et HPC
Contrairement aux applications Web et à de nombreuses applications métier, les applications Batch et HPC ont un début et une fin définis et elles peuvent s’exécuter selon une planification ou à la demande, parfois pendant des heures ou plus. La plupart sont classées en deux catégories principales : *intrinsèquement parallèles* (parfois appelé « embarrassingly parallel », car les problèmes de hello qu’ils résolvent prêtent toorunning en parallèle sur plusieurs ordinateurs ou des processeurs) et *étroitement couplées*. Consultez hello tableau suivant pour plus d’informations sur ces types d’applications. Certaines solutions Azure est proche de vos besoins pour un type ou hello autres.

> [!NOTE]
> Dans les solutions Batch et HPC, une instance en cours d’exécution d'une application est généralement appelée un *travail* et chaque travail peut être divisé en *tâches*. Et hello des ressources de calcul en cluster pour l’application hello sont souvent appelées *nœuds de calcul*.
> 
> 

| Type | Caractéristiques | Exemples |
| --- | --- | --- |
| **Intrinsèquement parallèles**<br/><br/>![Intrinsèquement parallèles][parallel] |• Les ordinateurs exécutent la logique applicative indépendamment<br/><br/> • Ajout ordinateurs permet hello application tooscale et réduire le temps de calcul<br/><br/>• L’application se compose d'exécutables séparés ou est divisée en un groupe de services appelés par un client (une application SOA ou une architecture orientée services) |• Modélisation de risques financiers<br/><br/>• Rendu et traitement d’images<br/><br/>• Encodage et transcodage multimédia<br/><br/>• Simulations Monte Carlo<br/><br/>• Tests de logiciels |
| **Tightly coupled**<br/><br/>![Tightly coupled][coupled] |• Application requiert le calcul nœuds exchange ou toointeract les résultats intermédiaires<br/><br/>• Nœuds peuvent communiquer à l’aide de compute hello Interface MPI (Message Passing), un protocole de communication commun pour le calcul parallèle<br/><br/>application de hello • est la bande passante et la latence toonetwork sensibles<br/><br/>• Les performances de l'application peuvent être améliorées en utilisant des technologies de réseau à haut débit comme InfiniBand et l'accès direct à la mémoire à distance (RDMA) |• Modélisation de réservoirs de pétrole et de gaz<br/><br/>• Analyse et conception technique, comme le calcul des dynamiques des fluides<br/><br/>• Simulations physiques comme des accidents de voiture et des réactions nucléaires<br/><br/>• Prévisions météorologiques |

### <a name="considerations-for-running-batch-and-hpc-applications-in-hello-cloud"></a>Considérations pour l’exécution du lot et les applications HPC dans le cloud de hello
Vous pouvez facilement migrer de nombreuses applications sont conçue toorun tooAzure de clusters HPC local ou tooa hybrides (entre sites) environnement. Toutefois, il peut y avoir des limitations ou des points à prendre en considération, notamment :

* **Disponibilité des ressources de cloud** -en fonction de type hello de ressources de calcul cloud vous utilisez, vous peut-être pas en mesure de toorely sur la disponibilité continue des machines pendant l’exécution d’un travail. Progression et la gestion d’état Vérifiez pointant est courantes techniques toohandle possibles erreurs temporaires et plus nécessaire lors de l’utilisation des ressources de cloud.
* **Accès aux données** -techniques d’accès aux données généralement disponibles dans les clusters de l’entreprise, tels que NFS, peuvent nécessiter une configuration spéciale dans le cloud de hello. Ou bien, vous devrez peut-être tooadopt différentes données accès pratiques et les modèles de cloud de hello.
* **Le déplacement des données** - pour les applications qui processus de grandes quantités de données, les stratégies de données de hello toomove nécessaires dans les ressources de stockage et toocompute cloud. Vous devrez peut-être utiliser un réseau haut débit intersite, par exemple [Azure ExpressRoute](https://azure.microsoft.com/services/expressroute/). Pensez également aux limites juridiques, réglementaires ou de politique pour le stockage ou l'accès à ces données.
* **Gestionnaire de licences** - Vérifiez auprès du fournisseur hello de toute application commerciale pour le Gestionnaire de licences ou autres restrictions pour l’exécution dans hello cloud. Tous les fournisseurs ne proposent pas le paiement à l'utilisation pour les licences. Que vous deviez tooplan pour un serveur de licences dans le cloud de hello pour votre solution, ou connecter le serveur de licences tooan local.

### <a name="big-compute-or-big-data"></a>Big Compute ou Big Data ?
Hello ligne entre les applications Big Compute et Big Data de séparation n’est pas toujours clair, et certaines applications peuvent avoir les caractéristiques des deux. Elles concernent toutes deux l'exécution de calculs à grande échelle, généralement sur des clusters d'ordinateurs. Mais les approches de solution hello et outils de prise en charge peuvent être différentes.

• **Big Compute** tend tooinvolve les applications qui s’appuient sur la puissance du processeur et mémoire, telles que des simulations d’ingénierie, des modélisations de risques financiers et des rendus numériques. infrastructure Hello pour une solution Big Compute peut-être inclure des ordinateurs avec des processeurs muliticœurs spécialisés tooperform des calculs bruts et spécialisées, haut débit réseau matériel tooconnect hello.

• Le **Big Data** résout les problèmes d’analyse de données qui impliquent de grandes quantités de données ne pouvant pas être gérées par un seul ordinateur ou un système de gestion de bases de données, par exemple les volumes importants de journaux web ou d’autres données décisionnelles. Big Data tend toorely plus d’informations sur la capacité du disque et les performances d’e/s que sur la puissance de l’UC. Il existe également des outils spécialisés comme Apache Hadoop toomanage hello cluster et pour partitionner les données de salutation Big Data. (Pour plus d’informations sur Azure HDInsight et d’autres solutions Azure Hadoop, consultez [Hadoop](https://azure.microsoft.com/solutions/hadoop/).)

## <a name="compute-management-and-job-scheduling"></a>Gestion des calculs et planification des travaux
En cours d’exécution des applications Batch et HPC souvent inclut un *Gestionnaire du cluster de* et un *planificateur* toohelp gérer les ressources de calcul en cluster et leur allouer toohello les applications qui exécutent des tâches de hello. Ces fonctions peuvent être exécutées par des outils distincts ou un outil ou service intégré.

* **Gestionnaire de cluster** : fournit, libère et administre les ressources de calcul (ou nœuds de calcul). Un gestionnaire de cluster peut automatiser l’installation des images de système d’exploitation et applications sur des nœuds de calcul, l’échelle des ressources de calcul en fonction de toodemands et surveiller les performances de hello de nœuds de hello.
* **Planificateur de travaux** -spécifie les ressources hello (tels que les processeurs ou mémoire) une application a besoin et hello conditions lorsqu’il s’exécute. Un planificateur de travaux gère une file d’attente des travaux et alloue toothem de ressources en fonction de la priorité assignée ou d’autres caractéristiques.

Clustering et planification des outils pour les clusters Windows et Linux peuvent migrer tooAzure bien. Par exemple, [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029), la solution de cluster de calcul gratuite de Microsoft pour les charges de travail HPC Windows et Linux, offre plusieurs options d'exécution dans Azure. Vous pouvez également générer des clusters Linux toorun des outils d’open source tels que couple et SLURM. Vous pouvez également faire tooAzure de solutions de grille commerciale, tels que [TIBCO DataSynapse GridServer](https://azure.microsoft.com/blog/tibco-datasynapse-comes-to-the-azure-marketplace/), [Symphony de gamme IBM et Symphony LSF](https://azure.microsoft.com/blog/ibm-and-microsoft-azure-support-spectrum-symphony-and-spectrum-lsf/), et [Univa grille moteur](http://www.univa.com/products/grid-engine).

Comme indiqué dans les sections suivantes de hello, vous pouvez également tirer parti des services Azure toomanage ressources de calcul et planifier des outils de gestion de cluster traditionnels travaux sans (ou en plus).

## <a name="scenarios"></a>Scénarios
Voici trois scénarios courants toorun les charges de travail Big Compute dans Azure à l’aide des solutions de cluster HPC existantes, les services Azure ou une combinaison de hello deux. Les points clés à prendre en compte pour choisir chaque scénario sont répertoriés mais ne sont pas exhaustifs. Plus sur les services Azure disponibles hello que vous pouvez utiliser dans votre solution sont plus loin dans l’article de hello.

| Scénario | Pourquoi choisir celui-ci ? |
| --- | --- | --- |
| **Croissance d’un tooAzure de cluster HPC**<br/><br/>[![Cluster burst][burst_cluster]](./media/batch-hpc-solutions/burst_cluster.png) <br/><br/> En savoir plus :<br/>• [Croître tooAzure des instances de travail avec HPC Pack](https://technet.microsoft.com/library/gg481749.aspx)<br/><br/>• [Configurer un cluster de calcul hybride avec HPC Pack](../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)<br/><br/>• [Croître tooAzure lot avec HPC Pack](https://technet.microsoft.com/library/mt612877.aspx)<br/><br/> |• Combinez votre [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) ou autre cluster local avec des ressources Azure supplémentaires dans une solution hybride.<br/><br/>• Étendre votre toorun les charges de travail Big Compute sur la plateforme en tant qu’instances de machine virtuelle un Service (PaaS) (actuellement Windows Server uniquement).<br/><br/>• Accédez à une banque de données ou à un serveur de licences local à l’aide d’un réseau virtuel Azure facultatif. |
| **Création d’un cluster HPC entièrement dans Azure**<br/><br/>[![Cluster in IaaS][iaas_cluster]](./media/batch-hpc-solutions/iaas_cluster.png)<br/><br/>En savoir plus :<br/>• [Solutions de cluster HPC dans Azure](big-compute-resources.md)<br/><br/> |• Déployez rapidement et uniformément vos applications et outils de cluster sur des machines virtuelles IaaS (infrastructure as a service) Windows ou Linux standard ou personnalisées.<br/><br/>• Exécutez différentes charges de travail Big Compute à l’aide de la solution de votre choix d’ordonnancement hello.<br/><br/>• Utiliser des services Azure supplémentaires, y compris réseau et stockage toocreate nuage solutions complètes. |
| **Montée en puissance parallèle un tooAzure application parallèle**<br/><br/>[![Azure Batch][batch_proc]](./media/batch-hpc-solutions/batch_proc.png)<br/><br/>En savoir plus :<br/>• [Notions de base d’Azure Batch](batch-technical-overview.md)<br/><br/>• [Démarrer avec la bibliothèque de traitement par lots Azure hello pour .NET](batch-dotnet-get-started.md) |• Développer avec [Azure Batch](https://azure.microsoft.com/documentation/services/batch/) tooscale les différentes toorun les charges de travail Big Compute sur les pools d’ordinateurs virtuels de Windows ou Linux.<br/><br/>• Utilisez un toomanage déploiement du service de plateforme Azure et l’échelle de machines virtuelles, une planification de travaux, la récupération d’urgence, le déplacement des données, gestion des dépendances et déploiement de l’application. |

## <a name="azure-services-for-big-compute"></a>Services Azure pour Big Compute
Voici plus d’informations sur le calcul de hello, données, mise en réseau et que vous pouvez combiner les services connexes pour des solutions Big Compute et le flux de travail. Pour des instructions détaillées sur les services Azure, consultez hello services Azure [documentation](https://azure.microsoft.com/documentation/). Hello [scénarios](#scenarios) plus haut dans cet article montrent quelques méthodes d’utilisation de ces services.

> [!NOTE]
> Azure lance régulièrement de nouveaux services qui pourraient être utiles dans votre scénario. Si vous avez des questions, contactez un [partenaire Azure](https://pinpoint.microsoft.com/en-US/search?keyword=azure) ou envoyez un e-mail à *bigcompute@microsoft.com*.
> 
> 

### <a name="compute-services"></a>Services de calcul
Services de calcul Azure sont core hello d’une solution Big Compute et les avantages d’offre de services de calcul différents hello pour différents scénarios. Au niveau de base, ces services offrent des modes différents pour toorun d’applications sur des instances de calcul basées sur une machine virtuelle Azure fournit à l’aide de la technologie Hyper-V de Windows Server. Ces instances peuvent exécuter des systèmes d’exploitation et des outils Linux et Windows standard et personnalisés. Azure vous propose un choix de [tailles d’instance](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) avec différentes configurations de cœurs d’UC, de mémoire, de capacité de disque et d’autres caractéristiques. Selon vos besoins, vous pouvez mettre à l’échelle toothousands d’instances hello de cœurs et ensuite à l’échelle lorsque vous avez besoin de moins de ressources.

> [!NOTE]
> Tirer parti de hello Azure [instances de calcul intensif telles que hello H-série](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooimprove hello les performances et l’évolutivité des charges de travail HPC. Ces instances prennent également en charge des applications MPI parallèles qui nécessitent un réseau d’application à faible latence et à débit élevé. Également disponible sont [série N](../virtual-machines/windows/sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) machines virtuelles avec NVIDIA GPU tooexpand hello différents scénarios de calcul et de visualisation dans Azure.  
> 
> 

| Service | Description |
| --- | --- |
| **[Machines virtuelles](https://azure.microsoft.com/documentation/services/virtual-machines/)**<br/><br/> |• Fournissent l’infrastructure de calcul en tant que service (IaaS) à l’aide de la technologie Microsoft Hyper-V.<br/><br/>• Vous tooflexibly configurer et gérer les ordinateurs de cloud persistants à partir d’images de Windows Server ou Linux standards à partir de hello [Azure Marketplace](https://azure.microsoft.com/marketplace/), ou les images et les données des disques vous fournissez<br/><br/>• Peut être déployé et géré en tant que [jeux de mise à l’échelle de machine virtuelle](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/) toobuild à grande échelle des services à partir de machines virtuelles identiques, avec une capacité échelle tooincrease ou diminue automatiquement<br/><br/>• Exécutés localement compute outils de cluster et les applications entièrement dans le cloud de hello<br/><br/> |
| **[Services cloud](https://azure.microsoft.com/documentation/services/cloud-services/)**<br/><br/> |• Peuvent exécuter des applications Big Compute dans des instances de rôle de travail, qui sont des machines virtuelles qui exécutent une version de Windows Server et sont entièrement gérées par Azure<br/><br/>• Activent des applications évolutives et fiables avec une charge administrative basse, exécutées dans un modèle de plateforme en tant que service (PaaS)<br/><br/>• Peut nécessiter des outils supplémentaires ou toointegrate du développement des solutions de cluster HPC local |
| **[Batch](https://azure.microsoft.com/documentation/services/batch/)**<br/><br/> |• Exécute des charges de travail à grande échelle parallèles et par lot dans un service entièrement géré.<br/><br/>• Fournit la planification des tâches et la mise à l’échelle automatique d’un pool géré de machines virtuelles<br/><br/>• Permet aux développeurs toobuild et exécuter des applications en tant que service ou cloud des applications existantes<br/> |

### <a name="storage-services"></a>Services de stockage
Une solution Big Compute fonctionne généralement sur un jeu de données d'entrée et génère des données pour ses résultats. Voici quelques-uns des services de stockage Azure hello utilisés dans des solutions Big Compute :

* [Stockage de file d’attente, table et blob](https://azure.microsoft.com/documentation/services/storage/) : gère de grandes quantités de données non structurées, de données NoSQL et de messages de flux de travail et de communication. Par exemple, vous pouvez utiliser le stockage d’objets blob pour les grands jeux de données techniques ou pour les images d’entrée de hello ou votre processus d’application des fichiers de support. Vous pouvez utiliser les files d'attente pour la communication asynchrone dans une solution. Consultez [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md).
* [Stockage de fichier Azure](https://azure.microsoft.com/services/storage/files/) -partages de fichiers courants et les données à l’aide d’Azure hello protocole SMB standard, qui est nécessaire pour certaines solutions de cluster HPC.
* [Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) -fournit une système de fichiers distribués d’Apache Hadoop démultipliée pour cloud hello, utile pour le traitement par lots, en temps réel et analytique interactif.

### <a name="data-and-analysis-services"></a>Services de données et d’analyse
Certains scénarios Big Compute impliquent des flux de données à grande échelle ou génèrent des données nécessitant un traitement ou une analyse supplémentaire. Azure propose plusieurs services de données et d’analyse, notamment :

* [Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) : génère des flux de travail (pipelines) pilotés par les données qui joignent, agrègent et transforment des données provenant de banques de données Internet, locales et basées sur le cloud.
* [Base de données SQL](https://azure.microsoft.com/documentation/services/sql-database/) -fournit hello des fonctionnalités clés d’un système de gestion de base de données relationnelle Microsoft SQL Server dans un service managé.
* [HDInsight](https://azure.microsoft.com/documentation/services/hdinsight/) - déploie et approvisionne les clusters Windows Server ou basés sur Linux Apache Hadoop Bonjour toomanage de cloud computing, l’analyse et de rapports sur les données volumineuses.
* [Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) : vous permet de créer, de tester, de faire fonctionner et de gérer des solutions analytiques prédictives dans un service entièrement administré.

### <a name="additional-services"></a>Services supplémentaires
Votre solution Big Compute peut-être des autres services Azure tooconnect tooresources localement ou dans d’autres environnements. Voici quelques exemples :

* [Réseau virtuel](https://azure.microsoft.com/documentation/services/virtual-network/) -crée une section logiquement isolée dans tooeach de ressources Azure de tooconnect Azure autres ou centre de données local tooyour. Avec un réseau virtuel intersite, les applications Big Compute peuvent accéder aux données, aux services Active Directory et aux serveurs de licences locaux.
* [ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/) : crée une connexion privée entre les centres de données Microsoft et une infrastructure locale ou dans un environnement de colocalisation. ExpressRoute fournit une sécurité accrue, plus de fiabilité, vitesses et des latences moindres rapport aux connexions classiques sur Internet de hello.
* [Service Bus](https://azure.microsoft.com/documentation/services/service-bus/) -fournit plusieurs mécanismes pour les applications toocommunicate ou échange des données, si elles se trouvent sur Azure, sur une autre plateforme cloud, ou dans un centre de données.

## <a name="next-steps"></a>Étapes suivantes
* Consultez [ressources techniques pour le traitement par lots et HPC](big-compute-resources.md) toofind des conseils techniques toobuild votre solution.
* Discutez de vos options Azure avec des partenaires, tels que Cycle Computing, Rescale et UberCloud.
* Découvrez les solutions Azure Big Compute fournies par [Towers Watson](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18222), [Altair](https://azure.microsoft.com/blog/availability-of-altair-radioss-rdma-on-microsoft-azure/), [ANSYS](https://azure.microsoft.com/blog/ansys-cfd-and-microsoft-azure-perform-the-best-hpc-scalability-in-the-cloud/) et [d3VIEW](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=22088).
* Pour les annonces hello plus récente, consultez hello [blog de l’équipe Microsoft HPC et Batch](http://blogs.technet.com/b/windowshpc/) et hello [blog Azure](https://azure.microsoft.com/blog/tag/hpc/).

<!--Image references-->
[parallel]: ./media/batch-hpc-solutions/parallel.png
[coupled]: ./media/batch-hpc-solutions/coupled.png
[iaas_cluster]: ./media/batch-hpc-solutions/iaas_cluster.png
[burst_cluster]: ./media/batch-hpc-solutions/burst_cluster.png
[batch_proc]: ./media/batch-hpc-solutions/batch_proc.png
