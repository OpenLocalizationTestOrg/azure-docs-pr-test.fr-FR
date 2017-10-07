---
title: aaaResources pour batch et HPC Bonjour Azure cloud | Documents Microsoft
description: "Répertorie les toohelp de ressources techniques vous exécutez votre parallèles à grande échelle, le lot et le calcul intensif les charges de travail (HPC) dans Azure."
services: batch, cloud-services, virtual-machines
documentationcenter: 
author: dlepow
manager: timlt
editor: 
ms.assetid: 6f8be911-c841-41ae-88d3-3bcfc029eb7f
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: big-compute
ms.date: 03/17/2017
ms.author: danlep
ms.openlocfilehash: ab8ba24678bd7ec090306b501d29ca63c4fb83ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="big-compute-in-azure-technical-resources-for-batch-and-high-performance-computing"></a>Big Compute dans Azure : ressources techniques pour Batch et calcul haute performance
Il s’agit d’un toohelp de ressources tootechnical guide vous exécutez votre parallèles à grande échelle, traitement et les charges de travail (HPC) high-performance computing dans Azure. Étendre votre lot existant ou un toohello de charges de travail HPC cloud Azure, ou créer de nouvelles solutions Big Compute à l’aide d’une plage de Azure services.

## <a name="solutions-options"></a>Options de solutions
En savoir plus sur les options de Big Compute dans Azure et choisissez une approche hello aux besoins de votre charge de travail et d’entreprise.

* [Solutions HPC et Batch](batch-hpc-solutions.md)
* [Vidéo : Big Compute dans cloud hello avec Azure et HPC](https://azure.microsoft.com/documentation/videos/teched-europe-2014-big-compute-in-the-cloud-with-high-performance-computing-on-azure/)

## <a name="azure-batch"></a>Azure Batch
[Lot](https://azure.microsoft.com/services/batch/) est un service de plateforme qui permet de facilement toocloud-activer vos applications Linux et Windows et les tâches d’exécution sans la configuration et la gestion d’un planificateur de cluster et la tâche. Utiliser des applications clientes de hello SDK toointegrate avec Azure Batch via différentes langues, étape tooAzure de données et générer des pipelines de l’exécution du travail.

* [Documentation](https://azure.microsoft.com/documentation/services/batch/)
* [.NET](https://msdn.microsoft.com/library/azure/mt348682.aspx), [Python](http://azure-sdk-for-python.readthedocs.io/latest/), [Node.js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/), [Java](http://azure.github.io/azure-sdk-for-java/) et référence d’API [REST](https://msdn.microsoft.com/library/azure/dn820158.aspx)
* [bibliothèque .NET de gestion Batch](https://msdn.microsoft.com/library/mt463120.aspx)
* Didacticiels : Mise en route de [Bibliothèque Batch pour .NET](batch-dotnet-get-started.md) et [Client Batch Python](batch-python-tutorial.md)
* [Forum Azure Batch](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurebatch)
* [Vidéos sur Azure Batch](https://azure.microsoft.com/documentation/videos/index/?services=batch)

## <a name="hpc-cluster-solutions"></a>Solutions de cluster HPC
Déployer ou d’étendre votre toorun Windows ou Linux HPC cluster tooAzure existant vos charges de travail intensives.  

### <a name="microsoft-hpc-pack"></a>Microsoft HPC Pack
HPC Pack est la solution HPC gratuite de Microsoft construite autour des technologies Microsoft Azure et Windows Server, capable d'exécuter des charges de travail HPC Windows et Linux.  

* [Téléchargez HPC Pack 2016](https://www.microsoft.com/download/details.aspx?id=54507)
* [Téléchargez la mise à jour 3 de HPC Pack 2012 R2](https://www.microsoft.com/download/details.aspx?id=49922)
* [Documentation](https://technet.microsoft.com/library/jj899572.aspx)
* Options de cluster HPC Pack dans Azure : [Linux](../virtual-machines/linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) et [Windows](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 
* [Croissance des instances de travail tooAzure avec HPC Pack](https://technet.microsoft.com/library/gg481749.aspx)
* [Croissance tooAzure lot avec HPC Pack](https://technet.microsoft.com/library/mt612877.aspx)
* [Forums Windows HPC](https://social.microsoft.com/Forums/home?category=windowshpc)

### <a name="linux-and-oss-cluster-solutions"></a>Solutions de cluster Linux et OSS
Utilisez ces toodeploy modèles Azure Linux HPC clusters.

* [Spin up a SLURM cluster](https://azure.microsoft.com/documentation/templates/slurm/) et [billet de blog](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx)
* [Spin up a Torque cluster](https://azure.microsoft.com/documentation/templates/torque-cluster/)
* [Modèles de grille de calcul avec PBS Professionnel](https://github.com/xpillons/azure-hpc/tree/master/Compute-Grid-Infra)

## <a name="hpc-storage"></a>Stockage HPC
* [Systèmes de fichiers parallèles pour le stockage HPC sur Azure](https://blogs.msdn.microsoft.com/azurecat/2017/03/17/parallel-file-systems-for-hpc-storage-on-azure/)
* [Intel Cloud Edition for Lustre Software - Eval](https://azure.microsoft.com/marketplace/partners/intel/lustre-cloud-edition-evaleval-lustre-2-7/)
* [Modèle BeeGFS sur CentOS 7.2](https://github.com/smith1511/hpc/tree/master/beegfs-shared-on-centos7.2)




## <a name="microsoft-mpi"></a>Microsoft MPI
[Microsoft MPI](https://msdn.microsoft.com/library/bb524831.aspx) (MS-MPI) est une implémentation Microsoft de hello Message passant Interface standard pour développer et exécuter des applications parallèles sur une plateforme de Windows hello.

* [Télécharger MS-MPI](http://go.microsoft.com/FWLink/p/?LinkID=389556)
* [Informations de référence sur MS-MPI](https://msdn.microsoft.com/library/dn473458.aspx)
* [Forum MPI](https://social.microsoft.com/Forums/en-us/home?forum=windowshpcmpi)

## <a name="compute-intensive-instances"></a>Instances nécessitant beaucoup de ressources système
Azure offre une [tailles de plage de la machine virtuelle](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), y compris [H-série de calcul intensif](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) instances capables de se connecter tooa RDMA réseau, toorun vos charges de travail Linux et Windows HPC. 

* [Configurer une application MPI de Linux RDMA cluster toorun](../virtual-machines/linux/classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Configuration d’un cluster Windows RDMA avec des applications MPI Microsoft HPC Pack toorun](../virtual-machines/windows/classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

Pour les charges de travail exigeant beaucoup de ressources graphiques, consultez la page [Tailles CN et NV](https://azure.microsoft.com/blog/azure-n-series-general-availability-on-december-1/).

## <a name="samples-and-demos"></a>Exemples et démonstrations
* [Exemples de code C# et Python Azure Batch](https://github.com/Azure/azure-batch-samples)
* [Traitement par lots chantier](https://azure.github.io/batch-shipyard/) boîte à outils pour un déploiement simple de type batch Dockerized les charges de travail tooAzure lot
* Package R [doAzureParallel](http://www.github.com/Azure/doAzureParallel) basé sur Azure Batch
* [Test de SUSE Linux Enterprise Server pour HPC](https://azure.microsoft.com/marketplace/partners/suse/suselinuxenterpriseserver12optimizedforhighperformancecompute/)

## <a name="related-azure-services"></a>Services Azure connexes
* [Data Factory](https://azure.microsoft.com/documentation/services/data-factory/)
* [Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/)
* [HDInsight](https://azure.microsoft.com/documentation/services/hdinsight/)
* [Machines virtuelles](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [Jeux de mise à l’échelle de machine virtuelle](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/)
* [Cloud Services](https://azure.microsoft.com/documentation/services/cloud-services/)
* [App Service](https://azure.microsoft.com/documentation/services/app-service/)
* [Media Services](https://azure.microsoft.com/documentation/services/media-services/)
* [Fonctions](https://azure.microsoft.com/documentation/services/functions/)

## <a name="architecture-blueprints"></a>Plans d'architecture
* [HPC et orchestration de données à l’aide des services Azure Batch et Azure Data Factory](http://go.microsoft.com/fwlink/?linkid=717686) (PDF) et [article](../data-factory/data-factory-data-processing-using-batch.md)

## <a name="industry-solutions"></a>Solutions métier
* [Banques et marchés financiers](https://finance.azure.com/)
* [Simulations techniques](https://simulation.azure.com/) 

## <a name="customer-stories"></a>Témoignages client
* [ANEO](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=4168) 
* [d3View](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=22088)
* [Ludwig Institute of Cancer Research](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=5830)
* [Microsoft Research](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=15634)
* [Milliman](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=14967)
* [Mitsubishi UFJ Securities International](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=26266)
* [Schlumberger](http://azure.microsoft.com/blog/big-compute-for-large-engineering-simulations)
* [Towers Watson](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18222)
* [UberCloud](https://simulation.azure.com/casestudies/Team-182-ABB-UC-Final.pdf)

## <a name="next-steps"></a>Étapes suivantes
* Pour les annonces hello plus récente, consultez hello [blog de l’équipe Microsoft HPC et Batch](http://blogs.technet.com/b/windowshpc/) et hello [blog Azure](https://azure.microsoft.com/blog/tag/hpc/).
* Consultez également [quelles sont les nouveautés dans le lot](https://azure.microsoft.com/updates/?service=batch) ou s’y abonner toohello [flux RSS](https://azure.microsoft.com/updates/feed/?service=batch).

