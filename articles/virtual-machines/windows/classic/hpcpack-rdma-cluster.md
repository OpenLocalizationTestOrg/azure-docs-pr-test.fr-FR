---
title: aaaSet une applications MPI de Windows RDMA cluster toorun | Documents Microsoft
description: "Découvrez comment toocreate un cluster Windows HPC Pack avec toouse H16r, H16mr, A8 ou A9 VMs de taille hello RDMA Azure réseau toorun MPI applications."
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 7d9f5bc8-012f-48dd-b290-db81c7592215
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/01/2017
ms.author: danlep
ms.openlocfilehash: 23bc8740dbd05a7c7ab3f998489a41d0df4520a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-windows-rdma-cluster-with-hpc-pack-toorun-mpi-applications"></a>Configuration d’un cluster Windows RDMA avec des applications MPI HPC Pack toorun
Configuration d’un cluster Windows RDMA dans Azure avec [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) et [tailles de machine virtuelle de calcul haute performance](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toorun les applications Interface MPI (Message Passing) parallèles. Lorsque vous configurez des nœuds Windows Server compatibles RDMA dans un cluster HPC Pack, les applications MPI communiquent efficacement sur un réseau à latence faible et à débit élevé dans Azure, reposant sur la technologie d’accès direct à la mémoire à distance (RDMA).

Si vous souhaitez que les charges de travail MPI toorun sur les machines virtuelles Linux réseau RDMA Azure hello accès, consultez [configurer une application MPI de Linux RDMA cluster toorun](../../linux/classic/rdma-cluster.md).

## <a name="hpc-pack-cluster-deployment-options"></a>Options de déploiement de cluster HPC Pack
Microsoft HPC Pack est un outil fourni à aucune toocreate coût supplémentaire des clusters HPC local ou dans les toorun Azure Windows ou Linux HPC. HPC Pack comprend un environnement d’exécution pour l’implémentation Microsoft hello hello Message passant Interface pour Windows (MS-MPI). Lorsqu’il est utilisé avec des instances en charge RDMA exécutant un système d’exploitation de Windows Server pris en charge, HPC Pack fournit un option efficace toorun Windows MPI des applications réseau RDMA Azure hello accès. 

Cet article présente deux scénarios et des liens tooset de conseils toodetailed configuration d’un cluster Windows RDMA avec Microsoft HPC Pack. 

* Scénario 1 Déployer des instances de rôle de travail nécessitant beaucoup de ressources système (PaaS)
* Scénario 2 Déployer des nœuds de calcul sur des machines virtuelles nécessitant beaucoup de ressources système (IaaS)

Pour les instances de calcul intensif préalables toouse avec Windows, consultez [tailles de machine virtuelle de calcul haute performance](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="scenario-1-deploy-compute-intensive-worker-role-instances-paas"></a>Scénario 1 : Déployer des instances de rôle de travail nécessitant beaucoup de ressources système (PaaS)
À partir d’un cluster HPC Pack existant, ajoutez des ressources de calcul supplémentaires dans les instances de rôle de travail Azure (nœuds Azure) en cours d’exécution dans un service cloud (PaaS). Cette fonctionnalité, également appelée « rafale tooAzure » à partir de HPC Pack, prend en charge une plage de tailles pour les instances de rôle de travail hello. Lors de l’ajout de hello nœuds Azure, spécifiez une des tailles de hello prenant en charge RDMA.

Voici les considérations et la procédure tooburst compatible tooRDMA instances Azure à partir d’un fichier (généralement local) cluster. Utilisez similaire procédures tooadd travail rôle instances tooan nœud principal HPC Pack déployé dans une machine virtuelle Azure.

> [!NOTE]
> Pour un didacticiel tooburst tooAzure avec HPC Pack, consultez [configurer un cluster hybride avec HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md). Notez les considérations de hello Bonjour suivant les étapes qui s’appliquent spécifiquement les nœuds Azure tooRDMA compatibles.
> 
> 

![Croissance tooAzure][burst]

### <a name="steps"></a>Étapes
1. **Déployer et configurer un nœud principal HPC Pack 2012 R2**
   
    Télécharger le package d’installation de HPC Pack dernière hello de hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=49922). Pour tooprepare configuration requise et des instructions pour un déploiement de croissance Azure, consultez [croître tooAzure des Instances de travail avec Microsoft HPC Pack](https://technet.microsoft.com/library/gg481749.aspx).
2. **Configurer un certificat de gestion Bonjour abonnement Azure**
   
    Configurer une connexion de hello toosecure certificat entre le nœud principal de hello et Azure. Pour plus d’options et les procédures, consultez [hello tooConfigure de scénarios le certificat de gestion Azure pour HPC Pack](http://technet.microsoft.com/library/gg481759.aspx). Pour les déploiements de test, HPC Pack installe un certificat par défaut Microsoft HPC Azure gestion vous pouvez télécharger rapidement tooyour abonnement Azure.
3. **Créer un nouveau service cloud et un compte de stockage**
   
    Utilisez hello toocreate portail Azure, un service cloud et un compte de stockage pour le déploiement de hello dans une région où les instances hello prenant en charge RDMA sont disponibles.
4. **Créer un modèle de nœud Azure**
   
    Utilisez l’Assistant Création d’un modèle de nœud de hello dans HPC Cluster Manager. Pour obtenir des instructions, consultez [créer un modèle de nœud Azure](http://technet.microsoft.com/library/gg481758.aspx#BKMK_Templ) dans « Étapes tooDeploy des nœuds Azure avec Microsoft HPC Pack ».
   
    Pour les premiers tests, nous vous suggérons de configuration d’une stratégie de disponibilité manuelle dans le modèle de hello.
5. **Ajouter toohello nœuds du cluster**
   
    Utilisez hello Assistant Ajout d’un nœud dans HPC Cluster Manager. Pour plus d’informations, consultez [toohello d’ajouter des nœuds Azure Cluster Windows HPC](http://technet.microsoft.com/library/gg481758.aspx#BKMK_Add).
   
    Lorsque vous spécifiez la taille hello de nœuds de hello, sélectionnez une des tailles d’instance prenant en charge RDMA hello.
   
   > [!NOTE]
   > Dans chaque déploiement de tooAzure croissance avec des instances de calcul intensif hello, HPC Pack déploie automatiquement un minimum de deux instances prenant en charge RDMA (telles que A8) en tant que nœuds de proxy, en outre les instances de rôle de travail Azure toohello vous spécifiez. nœuds de proxy Hello utilisent des cœurs qui sont alloués toohello abonnement et occasionnent des frais avec les instances de rôle de travail Azure hello.
   > 
   > 
6. **Démarrer (approvisionner) les nœuds de hello et les mettre en ligne toorun travaux**
   
    Sélectionnez les nœuds hello et utiliser hello **Démarrer** action dans HPC Cluster Manager. Lors de la configuration est terminée, sélectionnez les nœuds hello et utiliser hello **mettre en ligne** action dans HPC Cluster Manager. les nœuds de Hello sont prêt toorun travaux.
7. **Soumettre le cluster toohello de travaux**
   
   Utiliser des travaux de cluster HPC Pack travail soumission outils toorun. Consultez [Microsoft HPC Pack : gestion des travaux](http://technet.microsoft.com/library/jj899585.aspx).
8. **Arrêter les nœuds de hello (annuler le déploiement)**
   
   Lorsque vous avez terminé les tâches en cours d’exécution, mettez les nœuds hello hors connexion et utilisez hello **arrêter** action dans HPC Cluster Manager.

## <a name="scenario-2-deploy-compute-nodes-in-compute-intensive-vms-iaas"></a>Scénario 2 : Déployer des nœuds de calcul sur des machines virtuelles nécessitant beaucoup de ressources système (IaaS)
Dans ce scénario, vous déployez du nœud principal HPC Pack hello et les nœuds de calcul sur des machines virtuelles dans un réseau virtuel Azure. HPC Pack fournit un certain nombre [d’options de déploiement sur les machines virtuelles Azure](../../linux/hpcpack-cluster-options.md), y compris les scripts de déploiement automatisé et les modèles de démarrage rapide Azure. Par exemple, hello considérations relatives à la suite et étapes vous guide toouse hello [script de déploiement IaaS de HPC Pack](hpcpack-cluster-powershell-script.md) pour automatiser le déploiement d’un cluster HPC Pack 2012 R2 dans Azure hello.

![Cluster sur les machines virtuelles Azure][iaas]

### <a name="steps"></a>Étapes
1. **Créer un nœud principal du cluster et les machines virtuelles de nœud de calcul en exécutant le script de déploiement IaaS de HPC Pack hello sur un ordinateur client**
   
    Télécharger le package de Script de déploiement IaaS de HPC Pack hello de hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=49922).
   
    ordinateur client de hello tooprepare, créer le fichier de configuration hello et exécution hello script, consultez [créer un Cluster HPC avec hello script de déploiement IaaS de HPC Pack](hpcpack-cluster-powershell-script.md). 
   
    nœuds de calcul toodeploy prenant en charge RDMA, hello Remarque suivant des considérations supplémentaires :
   
   * **Réseau virtuel**: spécifiez un réseau virtuel dans une région qui Bonjour prenant en charge RDMA taille d’instance que vous souhaitez toouse est disponible.
   * **Système d’exploitation Windows Server**: toosupport la connectivité RDMA, spécifiez un système d’exploitation Windows Server 2012 R2 ou Windows Server 2012 pour les machines virtuelles de nœud de calcul hello.
   * **Services cloud** : nous vous recommandons de déployer votre nœud principal dans un service cloud et vos nœuds de calcul dans un autre service cloud.
   * **Taille du nœud principal**: pour ce scénario, envisagez une taille d’au moins A4 (très grande) pour le nœud principal de hello.
   * **Extension HpcVmDrivers**: script de déploiement hello installe hello Agent de machine virtuelle Azure et hello extension HpcVmDrivers automatiquement lorsque vous déployez des nœuds de calcul taille A8 ou A9 avec un système d’exploitation Windows. HpcVmDrivers installe des pilotes sur des machines virtuelles de nœud de calcul hello afin qu’ils peuvent se connecter réseau RDMA de toohello. Sur les machines virtuelles de série H prenant en charge RDMA, vous devez installer manuellement extension HpcVmDrivers de hello. Consultez [Tailles de machines virtuelles de calcul haute performance](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
   * **Configuration réseau du cluster**: script de déploiement hello configure automatiquement le cluster HPC Pack de hello dans la topologie 5 (tous les nœuds sur le réseau d’entreprise hello). Cette topologie est requise pour tous les déploiements de cluster HPC Pack dans les machines virtuelles. Ne modifiez pas topologie réseau du cluster hello plus tard.
2. **Mettre des nœuds de calcul hello toorun en ligne de travaux**
   
    Sélectionnez les nœuds hello et utiliser hello **mettre en ligne** action dans HPC Cluster Manager. les nœuds de Hello sont prêt toorun travaux.
3. **Soumettre le cluster toohello de travaux**
   
    Connecter des travaux de toosubmit toohello du nœud principal, ou configurer un toodo d’ordinateur local, cela. Pour plus d’informations, consultez [tooan d’envoyer des travaux HPC cluster dans Azure](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
4. **Take hello nœuds hors connexion et arrêter (libérer)**
   
    Lorsque vous avez terminé les tâches en cours d’exécution, vous pouvez prendre nœuds hello hors connexion dans HPC Cluster Manager. Ensuite, utilisez tooshut des outils de gestion Azure leur vers le bas.

## <a name="run-mpi-applications-on-hello-cluster"></a>Exécuter des applications MPI sur le cluster de hello
### <a name="example-run-mpipingpong-on-an-hpc-pack-cluster"></a>Exemple : Exécuter mpipingpong sur un cluster HPC Pack
tooverify un déploiement de HPC Pack des instances hello prenant en charge RDMA, exécutez hello HPC Pack **mpipingpong** commande sur le cluster de hello. **MPIPingPong** envoie les paquets de données entre des nœuds appariés de mesurer le débit et de latence toocalculate à plusieurs reprises et les statistiques de réseau applicatif RDMA de hello. Cet exemple montre un modèle par défaut pour l’exécution d’un travail MPI (dans ce cas, **mpipingpong**) à l’aide de cluster de hello **mpiexec** commande.

Cet exemple suppose que vous avez ajouté des nœuds Azure dans une configuration « croître tooAzure » ([scénario 1](#scenario-1.-deploy-compute-intensive-worker-role-instances-\(PaaS\) in this article). Si vous avez déployé HPC Pack sur un cluster de machines virtuelles Azure, vous devez toomodify hello commande syntaxe toospecify un autre groupe de nœuds et définir l’environnement supplémentaires variables toodirect trafic toohello RDMA réseau.

mpipingpong toorun sur le cluster de hello :

1. Sur le nœud principal de hello ou sur un ordinateur client correctement configuré, ouvrez une invite de commandes.
2. latence tooestimate entre les paires de nœuds dans un déploiement de croissance Azure de quatre nœuds, hello du type suivant de commande toosubmit un mpipingpong toorun de travail avec une petite taille de paquet et le nombre d’itérations :
   
    ```Command
    job submit /nodegroup:azurenodes /numnodes:4 mpiexec -c 1 -affinity mpipingpong -p 1:100000 -op -s nul
    ```
   
    commande Hello retourne ID hello du travail de hello est envoyé.
   
    Si vous avez déployé le cluster HPC Pack de hello déployé sur des machines virtuelles Azure, spécifiez un groupe de nœuds contenant déployés dans un seul service cloud de machines virtuelles de nœud de calcul et modifier hello **mpiexec** commande comme suit :
   
    ```Command
    job submit /nodegroup:vmcomputenodes /numnodes:4 mpiexec -c 1 -affinity -env MSMPI_DISABLE_SOCK 1 -env MSMPI_PRECONNECT all -env MPICH_NETMASK 172.16.0.0/255.255.0.0 mpipingpong -p 1:100000 -op -s nul
    ```
3. En cas de hello est terminée, tooview hello sortie (dans ce cas, sortie hello de la tâche 1 du travail de hello), hello du type suivant
   
    ```Command
    task view <JobID>.1
    ```
   
    où &lt; *JobID* &gt; hello des ID de tâche hello qui a été soumis.
   
    sortie de Hello inclut latence des résultats similaires toohello éléments suivants.
   
    ![Latence ping pong][pingpong1]
4. nœuds de croissance de débit tooestimate entre les paires de Azure, tapez ce qui suit hello commande toosubmit un toorun travail **mpipingpong** avec une grande taille de paquet et quelques itérations :
   
    ```Command
    job submit /nodegroup:azurenodes /numnodes:4 mpiexec -c 1 -affinity mpipingpong -p 4000000:1000 -op -s nul
    ```
   
    commande Hello retourne ID hello du travail de hello est envoyé.
   
    Sur un cluster HPC Pack déployé sur les machines virtuelles Azure, modifiez la commande hello comme indiqué à l’étape 2.
5. En cas de hello est terminée, tooview hello sortie (dans ce cas, sortie hello de la tâche 1 du travail de hello), hello du type suivant :
   
    ```Command
    task view <JobID>.1
    ```
   
   sortie de Hello inclut le débit des résultats similaires toohello après.
   
   ![Débit ping pong][pingpong2]

### <a name="mpi-application-considerations"></a>Considérations sur les applications MPI
Vous trouverez ci-dessous des considérations relatives à l’exécution d’applications MPI avec le HPC Pack dans Azure. Certains s’appliquent uniquement aux toodeployments de nœuds Azure (instances de rôle de travail ajoutés dans une configuration de « croissance tooAzure »).

* Les instances de rôle de travail dans un service cloud sont régulièrement réapprovisionnées sans préavis par Azure (par exemple, pour la maintenance du système ou en cas d’échec d’une instance). Si une instance est remise en service en cours d’exécution d’un travail MPI, instance de hello perd ses données et retourne l’état de toohello lors de son premier déploiement, ce qui peut entraîner des toofail de travail MPI hello. Hello plus de nœuds que vous utilisez pour un seul travail MPI, hello plus hello travail s’exécute, hello plus probable qu’une des instances de hello est remise en service pendant l’exécution d’un travail. Considérer ceci si vous désignez un seul nœud dans le déploiement de hello comme un serveur de fichiers.
* toorun des travaux MPI dans Azure, vous ne disposez d’instances de toouse hello prenant en charge RDMA. Vous pouvez utiliser n’importe quelle taille d’instance prise en charge par HPC Pack. Toutefois, les instances de prenant en charge RDMA hello sont recommandées pour l’exécution des travaux MPI à relativement grande échelle qui sont sensibles toohello latence et bande passante réseau hello qui connecte les nœuds hello hello. Si vous utilisez d’autres travaux MPI de tailles toorun sensibles et de la bande passante, nous vous recommandons d’exécuter de petits travaux, dans lequel une seule tâche s’exécute sur plusieurs nœuds.
* Les applications déployées tooAzure instances sont toohello sujet associé application hello de contrat de licence. Vérifiez auprès du fournisseur de hello de toute application commerciale pour le Gestionnaire de licences ou d’autres restrictions pour l’exécution dans le cloud de hello. Tous les fournisseurs ne proposent pas le paiement à l'utilisation pour les licences.
* Instances Azure vous doivent installer autres nœuds de tooaccess locaux, les partages et les serveurs de licences. Par exemple, tooenable hello nœuds Azure tooaccess un serveur de licences sur site, vous pouvez configurer un réseau virtuel Azure de site à site.
* toorun des applications MPI sur des instances Azure, inscrire chaque application MPI avec le pare-feu Windows sur les instances de hello en exécutant hello **hpcfwutil** commande. Cela permet de MPI communications tootake sur place sur un port affecté dynamiquement par le pare-feu hello.
  
  > [!NOTE]
  > Pour les déploiements en rafale tooAzure, vous pouvez également configurer un toorun de commande d’exception pare-feu automatiquement tous les nouveaux nœuds Azure ajoutés tooyour cluster. Une fois que vous exécutez hello **hpcfwutil** de commandes et vérifiez que votre application fonctionne, ajoutez le script de démarrage hello commande tooa pour vos nœuds Azure. Pour plus d'informations, consultez [Utiliser un script de démarrage pour les nœuds Azure](https://technet.microsoft.com/library/jj899632.aspx).
  > 
  > 
* HPC Pack utilise hello CCP_MPI_NETMASK cluster environnement variable toospecify une plage d’adresses acceptables pour la communication MPI. À compter de HPC Pack 2012 R2, variable d’environnement de cluster CCP_MPI_NETMASK hello affecte uniquement communication MPI entre les nœuds de calcul joints au domaine (localement ou dans des machines virtuelles Azure). variable de Hello est ignorée par les nœuds ajoutés dans une configuration de tooAzure de croissance.
* Impossible d’exécuter des travaux MPI entre des instances Azure déployées dans différents services cloud (par exemple, dans les déploiements de tooAzure croissance avec différents modèles de nœud ou les nœuds de calcul de machine virtuelle Azure déployées dans plusieurs services cloud). Si vous avez plusieurs déploiements de nœuds Azure démarrés avec différents modèles de nœud, hello MPI doit s’exécuter sur un seul jeu de nœuds Azure.
* Lorsque vous ajoutez des nœuds Azure tooyour cluster et les mettez en ligne, hello Service Planificateur de travaux HPC immédiatement tente toostart les travaux sur les nœuds hello. Si seule une partie de votre charge de travail peut exécuter sur Azure, assurez-vous de mettre à jour ou de créer toodefine des modèles de projet quel travail types peuvent s’exécuter sur Azure. Par exemple, tooensure que les travaux soumis avec un modèle de travail uniquement s’exécuter sur des nœuds Azure, ajouter un modèle de tâche hello nœud groupes propriété toohello et sélectionnez AzureNodes hello valeur requise. toocreate des groupes personnalisés pour vos nœuds Azure, utilisez l’applet de commande Add-HpcGroup HPC PowerShell hello.

## <a name="next-steps"></a>Étapes suivantes
* Comme un toousing autre HPC Pack, développer des applications MPI sur des pools gérés de nœuds de calcul dans Azure avec toorun de service de traitement par lots Azure hello. Consultez [multi-instance utilisez tâches toorun les applications d’Interface MPI (Message Passing) dans Azure Batch](../../../batch/batch-mpi.md).
* Si vous souhaitez toorun Linux MPI les applications qui accèdent au réseau RDMA Azure de hello, consultez [configurer une application MPI de Linux RDMA cluster toorun](../../linux/classic/rdma-cluster.md).

<!--Image references-->
[burst]:media/hpcpack-rdma-cluster/burst.png
[iaas]:media/hpcpack-rdma-cluster/iaas.png
[pingpong1]:media/hpcpack-rdma-cluster/pingpong1.png
[pingpong2]:media/hpcpack-rdma-cluster/pingpong2.png
