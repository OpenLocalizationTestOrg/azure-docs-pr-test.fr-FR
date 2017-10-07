---
title: aaaUse de calcul intensif machines virtuelles de Azure avec le traitement par lots | Documents Microsoft
description: "Comment parti tootake de machine virtuelle prenant en charge RDMA ou GPU compatible tailles dans des pools d’Azure Batch"
services: batch
documentationcenter: 
author: dlepow
manager: timlt
editor: 
ms.assetid: 
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: danlep
ms.openlocfilehash: 6a462a5f2a44ddcec8bf4e5c200d444cac8fafe6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-rdma-capable-or-gpu-enabled-instances-in-batch-pools"></a>Utiliser des instances compatibles RDMA ou GPU dans les pools Batch

toorun certains traitements par lots, vous souhaiterez peut-être parti tootake des tailles de machine virtuelle Azure conçu pour le calcul à grande échelle. Par exemple, les instances multiples toorun [les charges de travail MPI](batch-mpi.md), vous pouvez choisir A8, A9, ou tailles H-série qui ont un réseau de l’interface d’accès à distance directe mémoire (RDMA). Ces tailles de connecter le réseau InfiniBand de tooan pour la communication entre les nœuds, ce qui peut accélérer les applications MPI. Pour les applications CUDA, vous pouvez choisir des tailles de série N qui incluent des cartes d’unité de traitement graphique (GPU) NVIDIA Tesla.

Cet article fournit des instructions et des exemples toouse quelques-uns des formats de spécialisées d’Azure dans les pools de lot. Pour obtenir des informations générales et en savoir plus sur les caractéristiques techniques, consultez :

* Tailles de machines virtuelles de calcul haute performance ([Linux](../virtual-machines/linux/sizes-hpc.md), [Windows](../virtual-machines/windows/sizes-hpc.md)) 

* Tailles de machines virtuelles Linux compatibles GPU ([Linux](../virtual-machines/linux/sizes-gpu.md), [Windows](../virtual-machines/windows/sizes-gpu.md)) 


## <a name="subscription-and-account-limits"></a>Limites de compte et d’abonnement

* **Quotas** -un ou plusieurs quotas Azure peuvent limiter hello nombre ou le type de nœuds, vous pouvez ajouter pool de traitement par lots tooa. Vous êtes toobe probablement limité lorsque vous choisissez prenant en charge RDMA, GPU compatible, ou autres tailles de machine virtuelle multicœurs. En fonction de type hello du compte de traitement par lots créé, les quotas de hello pourraient s’appliquent compte toohello lui-même ou tooyour abonnement.

    * Si vous avez créé votre compte Batch Bonjour **lot service** configuration, vous êtes limité par hello [quota de cœurs dédiés par compte Batch](batch-quota-limit.md#resource-quotas). Par défaut, ce quota est de 20 cœurs. Un quota distinct s’applique également[machines virtuelles de faible priorité](batch-low-pri-vms.md), si vous les utilisez. 

    * Si vous avez créé le compte de hello Bonjour **abonnement utilisateur** configuration, votre abonnement limite le nombre hello de cœurs de machine virtuelle par région. Consultez [Abonnement Azure et limites, quotas et contraintes de service](../azure-subscription-service-limits.md). Votre abonnement s’applique également à un quota régionaux toocertain tailles de machine virtuelle, notamment des instances HPC et du GPU. Dans la configuration d’un abonnement utilisateur hello, aucune des quotas supplémentaires s’appliquent toohello du compte Batch. 

  Vous devrez peut-être tooincrease un ou plusieurs quotas lors de l’utilisation d’une taille de machine virtuelle spécialisée dans le lot. toorequest une augmentation du quota, ouvrir une [demande de support technique en ligne](../azure-supportability/how-to-create-azure-support-request.md) sans frais.

* **Disponibilité de la région** - calcul intensif machines virtuelles ne soient pas disponibles dans les régions hello où vous créez des comptes de traitement par lots. toocheck qu’une taille n’est disponible, consultez [produits disponibles par région](https://azure.microsoft.com/regions/services/).


## <a name="dependencies"></a>Dépendances

Hello RDMA et les fonctionnalités GPU des tailles de calcul intensif sont pris en charge uniquement dans certains systèmes d’exploitation. Selon votre système d’exploitation, vous deviez tooinstall ou configurer des pilotes supplémentaires ou autres logiciels. Hello les tableaux suivants résument ces dépendances. Pour plus de détails, consultez les articles associés. Pour les pools de lot tooconfigure options, consultez plus loin dans cet article.


### <a name="linux-pools---virtual-machine-configuration"></a>Pools Linux - Configuration de machine virtuelle

| Taille | Fonctionnalité | Systèmes d’exploitation | Logiciels requis | Paramètres de pool |
| -------- | -------- | ----- |  -------- | ----- |
| [H16r, H16mr, A8, A9](../virtual-machines/linux/sizes-hpc.md#rdma-capable-instances) | RDMA | HPC SUSE Linux Enterprise Server 12 ou<br/>HPC basé sur CentOS<br/>(Place de marché Azure) | Intel MPI 5 | Activer la communication entre les nœuds, désactiver l’exécution simultanée des tâches |
| [Série NC*](../virtual-machines/linux/n-series-driver-setup.md#install-cuda-drivers-for-nc-vms) | GPU NVIDIA Tesla K80 | Ubuntu 16.04 LTS.<br/>Red Hat Enterprise Linux 7.3 ou<br/>Basé sur CentOS 7.3<br/>(Place de marché Azure) | Pilotes NVIDIA CUDA Toolkit 8.0 | N/A | 
| [Série NV](../virtual-machines/linux/n-series-driver-setup.md#install-grid-drivers-for-nv-vms) | GPU NVIDIA Tesla M60 | Ubuntu 16.04 LTS<br/>Red Hat Enterprise Linux 7.3<br/>Basé sur CentOS 7.3<br/>(Place de marché Azure) | Pilotes NVIDIA GRID 4.3 | N/A |

*La connectivité RDMA sur les machines virtuelles NC24r est prise en charge sur HPC basé sur CentOS 7.3 avec Intel MPI.



### <a name="windows-pools---virtual-machine-configuration"></a>Pools Windows - Configuration de machine virtuelle

| Taille | Fonctionnalité | Systèmes d’exploitation | Logiciels requis | Paramètres de pool |
| -------- | ------ | -------- | -------- | ----- |
| [H16r, H16mr, A8, A9](../virtual-machines/windows/sizes-hpc.md#rdma-capable-instances) | RDMA | Windows Server 2012 R2 ou<br/>Windows Server 2012 (Place de marché Azure) | Microsoft MPI 2012 R2 ou ultérieur, ou<br/> Intel MPI 5<br/><br/>Extension de machine virtuelle Azure HpcVMDrivers | Activer la communication entre les nœuds, désactiver l’exécution simultanée des tâches |
| [Série NC*](../virtual-machines/windows/n-series-driver-setup.md) | GPU NVIDIA Tesla K80 | Windows Server 2016 ou <br/>Windows Server 2012 R2 (Place de marché Azure) | Pilotes NVIDIA Tesla ou pilotes CUDA Toolkit 8.0| N/A | 
| [Série NV](../virtual-machines/windows/n-series-driver-setup.md) | GPU NVIDIA Tesla M60 | Windows Server 2016 ou<br/>Windows Server 2012 R2 (Place de marché Azure) | Pilotes NVIDIA GRID 4.3 | N/A |

*La connectivité RDMA sur les machines virtuelles NC24r est prise en charge sur Windows Server 2012 R2 avec l’extension HpcVMDrivers et Microsoft MPI ou Intel MPI.

### <a name="windows-pools---cloud-services-configuration"></a>Pools Windows - Configuration des services cloud

> [!NOTE]
> Pools de lot avec la configuration des services cloud hello ne prend pas en charge les tailles de N-series.
>

| Taille | Fonctionnalité | Systèmes d’exploitation | Logiciels requis | Paramètres de pool |
| -------- | ------- | -------- | -------- | ----- |
| [H16r, H16mr, A8, A9](../virtual-machines/windows/sizes-hpc.md#rdma-capable-instances) | RDMA | Windows Server 2012 R2,<br/>Windows Server 2012 ou<br/>Windows Server 2008 R2 (Famille de système d’exploitation invité) | Microsoft MPI 2012 R2 ou ultérieur, ou<br/>Intel MPI 5<br/><br/>Extension de machine virtuelle Azure HpcVMDrivers | Activer la communication entre les nœuds,<br/> désactiver l’exécution simultanée des tâches |





## <a name="pool-configuration-options"></a>Options de configuration de pool

tooconfigure une taille de machine virtuelle spécialisée pour votre pool de lot, hello API de lot et les outils fournissent plusieurs logiciels de tooinstall requis d’options ou les pilotes, y compris :

* [Démarrer la tâche](batch-api-basics.md#start-task) -télécharger un package d’installation comme un tooan de fichier de ressources compte de stockage Azure Bonjour même région que hello compte Batch. Créer un fichier de ressources hello tooinstall début tâche ligne de commande en mode silencieux au démarrage du pool de hello. Pour plus d’informations, consultez hello [documentation de l’API REST](/rest/api/batchservice/add-a-pool-to-an-account#bk_starttask).

  > [!NOTE] 
  > tâche de démarrage Hello doit s’exécuter avec des autorisations avec élévation de privilèges (administrateur), et il doit attendre pour la réussite.
  >

* [Package d’application](batch-application-packages.md) - ajouter un tooyour de package d’installation compressé compte Batch et configurer une référence de package dans le pool de hello. Ce paramètre télécharge et décompresse le package hello sur tous les nœuds dans le pool de hello. Si le package de hello est un programme d’installation, créer une application hello de démarrage tâche ligne de commande toosilently installation sur tous les nœuds de pool. Vous pouvez également installer hello lorsqu’une tâche est planifiée toorun sur un nœud.

* [Image de pool personnalisé](batch-api-basics.md#pool) - création d’un Windows personnalisé ou l’image Linux VM qui contient les pilotes, logiciels ou autres paramètres nécessaires pour hello taille de machine virtuelle. Si vous avez créé votre compte Batch dans la configuration d’un abonnement utilisateur hello, spécifiez l’image personnalisée de hello pour votre pool de traitement par lots. (Les images personnalisées ne sont pas pris en charge dans les comptes dans la configuration du service de traitement par lots hello.) Images personnalisées utilisable uniquement avec les pools dans la configuration d’ordinateur virtuel hello.

  > [!IMPORTANT]
  > Dans les pools Batch, vous ne pouvez pas utiliser une image personnalisée créée avec des disques gérés ou avec le stockage Premium pour l’instant.
  >



* [Traitement par lots chantier](https://github.com/Azure/batch-shipyard) configure automatiquement la toowork GPU et RDMA hello en toute transparence avec des charges de travail sur Azure Batch. Batch Shipyard est entièrement piloté par les fichiers de configuration. Il existe plusieurs exemples recette de configurations disponibles qui permettent les charges de travail GPU et RDMA telles que hello [CNTK GPU recette](https://github.com/Azure/batch-shipyard/tree/master/recipes/CNTK-GPU-OpenMPI) qui préconfigure les pilotes GPU sur des machines virtuelles de série N et charge les logiciels Microsoft cognitifs Toolkit comme une image Docker.


## <a name="example-microsoft-mpi-on-an-a8-vm-pool"></a>Exemple : Microsoft MPI sur un pool de machines virtuelles A8

toorun les applications MPI de Windows sur un pool de nœuds d’Azure A8, vous devez tooinstall une implémentation MPI prise en charge. Voici des exemples étapes tooinstall [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) sur un Windows du pool à l’aide d’un package d’application de traitement par lots.

1. Télécharger hello [le package d’installation](http://go.microsoft.com/FWLink/p/?LinkID=389556) (MSMpiSetup.exe) pour la version la plus récente de Microsoft MPI hello.
2. Créer un fichier zip de package de hello.
3. Téléchargez le compte de traitement par lots tooyour hello package. Pour obtenir des instructions, consultez hello [les packages d’applications](batch-application-packages.md) des conseils. Spécifiez un ID d’application (par exemple *MSMPI*) et une version (par exemple *8.1*). 
4. Hello API de lot ou le portail Azure, créez un pool dans configuration des services cloud hello avec numéro hello souhaité de nœuds et d’échelle. Hello tableau suivant montre tooset de paramètres d’échantillon des MPI en mode sans assistance à l’aide d’une tâche de démarrage :

| Paramètre | Valeur |
| ---- | ----- | 
| **Type d’image** | Services cloud |
| **Famille de système d’exploitation** | Windows Server 2012 R2 (famille de système d’exploitation 4) |
| **Taille du nœud** | A8 Standard |
| **Communication entre les nœuds activée** | true |
| **Nombre maximal de tâches par nœud** | 1 |
| **Références du package d’application** | MSMPI |
| **Tâche de démarrage activée** | true<br>**Ligne de commande** - `"cmd /c %AZ_BATCH_APP_PACKAGE_MSMPI#8.1%\\MSMpiSetup.exe -unattend -force"`<br/>**Identité de l’utilisateur** - Pool autouser, admin<br/>**Attente de la réussite** - True

## <a name="example-nvidia-tesla-drivers-on-nc-vm-pool"></a>Exemple : Pilotes NVIDIA Tesla sur un pool de machines virtuelles NC

applications de CUDA toorun sur un pool de nœuds de contexte de nommage de Linux, vous devez tooinstall CUDA Toolkit 8.0 sur les nœuds hello. Hello Toolkit installe des pilotes de NVIDIA Tesla GPU nécessaires hello. Voici un exemple suit toodeploy une image Ubuntu 16.04 LTS personnalisée avec les pilotes GPU hello :

1. Déployez une machine virtuelle Azure NC6 exécutant Ubuntu 16.04 LTS. Par exemple, créer hello machine virtuelle dans la région US Sud hello. Vérifiez que vous créez hello machine virtuelle avec un stockage standard, et *sans* des disques gérés.
2. Suivez hello étapes tooconnect toohello VM et [installer des pilotes CUDA](../virtual-machines/linux/n-series-driver-setup.md#install-cuda-drivers-for-nc-vms).
3. Annuler le déploiement de l’agent de hello Linux, puis vous capturez image Linux VM à l’aide des commandes hello Azure CLI 1.0. Pour connaître les étapes nécessaires, consultez [Capturer une machine virtuelle Linux exécutée sur Azure](../virtual-machines/linux/capture-image-nodejs.md). Prenez note de l’URI d’image hello.
  > [!IMPORTANT]
  > N’utilisez pas d’image de Azure CLI 2.0 commandes toocapture hello pour Azure Batch. Actuellement commandes hello CLI 2.0 ne capturer que les machines virtuelles créées à l’aide de disques gérés.
  >
4. Créez un compte Batch, avec configuration abonnement utilisateur hello, dans une région qui prend en charge des machines virtuelles de contexte de nommage.
5. Hello API de lot ou le portail Azure, créez un pool à l’aide d’image personnalisée de hello et par hello souhaité nombre de nœuds et l’échelle. Hello tableau suivant présente les paramètres de pool exemple pour l’image de hello :

| Paramètre | Valeur |
| ---- | ---- |
| **Type d’image** | Image personnalisée |
| **Image personnalisée** | URI du formulaire de hello d’image`https://yourstorageaccountdisks.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd` |
| **Référence de l’agent de nœud** | batch.node.ubuntu 16.04 |
| **Taille du nœud** | NC6 Standard |



## <a name="next-steps"></a>Étapes suivantes

* toorun des travaux MPI sur un pool de traitement par lots Azure, consultez hello [Windows](batch-mpi.md) ou [Linux](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/) exemples.

* Pour obtenir des exemples de charges de travail GPU sur le traitement par lots, consultez hello [lot chantier](https://github.com/Azure/batch-shipyard/) recettes.
