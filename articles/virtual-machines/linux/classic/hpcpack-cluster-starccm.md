---
title: "aaaRun en étoile-CCM + avec HPC Pack sur les machines virtuelles Linux | Documents Microsoft"
description: "Déployer un cluster Microsoft HPC Pack sur Azure et exécuter un travail Star-CCM+ sur plusieurs nœuds de calcul Linux d’un réseau RDMA."
services: virtual-machines-linux
documentationcenter: 
author: xpillons
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 75523406-d268-4623-ac3e-811c7b74de4b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 09/13/2016
ms.author: xpillons
ms.openlocfilehash: 8265013cb295f53d6d4354ab2f100ef20d9f4c8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-star-ccm-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a>Exécuter Star-CCM+ avec Microsoft HPC Pack sur un cluster Linux RDMA dans Azure
Cet article explique comment toodeploy un Microsoft HPC Pack cluster sur Azure, exécutez un [CD-adapco STAR-CCM +](http://www.cd-adapco.com/products/star-ccm%C2%AE) travail sur plusieurs nœuds de calcul Linux qui sont interconnectés avec InfiniBand.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

Microsoft HPC Pack fournit des fonctionnalités toorun divers HPC à grande échelle et des applications parallèles, y compris des applications MPI sur des clusters de machines virtuelles Microsoft Azure. HPC Pack prend également en charge l’exécution d’applications Linux HPC sur les machines virtuelles de nœuds de calcul Linux déployées dans un cluster HPC Pack. Pour une présentation de toousing Linux nœuds avec HPC Pack, consultez [prise en main des nœuds de calcul Linux dans un cluster HPC Pack dans Azure](hpcpack-cluster.md).

## <a name="set-up-an-hpc-pack-cluster"></a>Configurer un cluster HPC Pack
Télécharger les scripts de déploiement IaaS de HPC Pack hello de hello [centre de téléchargement](https://www.microsoft.com/en-us/download/details.aspx?id=44949) et extrayez-les localement.

Azure PowerShell doit être installé et configuré. Si PowerShell n’est pas configuré sur votre ordinateur local, consultez l’article de hello [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).

Au moment de hello de rédaction de cet article, les images Linux hello hello Azure Marketplace (qui contient les pilotes InfiniBand hello pour Azure) sont pour SLES 12, CentOS 6.5 et CentOS 7.1. Cet article est basé sur l’utilisation de hello de SLES 12. nom de hello tooretrieve de toutes les images Linux qui prennent en charge HPC Bonjour Marketplace, vous pouvez exécuter hello suivant de commande PowerShell :

```
    get-azurevmimage | ?{$_.ImageName.Contains("hpc") -and $_.OS -eq "Linux" }
```

le résultat de Hello affiche emplacement hello dans lequel ces images sont disponibles et nom de l’image de hello (**ImageName**) toobe utilisé dans le modèle de déploiement hello plus tard.

Avant de déployer les clusters hello, vous avez toobuild un fichier de modèle de déploiement de HPC Pack. Étant donné que nous avons ciblez un petit cluster, nœud de tête hello sera contrôleur de domaine hello et héberger la base de données SQL locale.

Hello modèle suivant sera déployer ce type d’un nœud principal, créez un fichier XML nommé **MyCluster.xml**et remplacez les valeurs hello de **SubscriptionId**, **StorageAccount**,  **Emplacement**, **VMName**, et **ServiceName** avec les vôtres.

    <?xml version="1.0" encoding="utf-8" ?>
    <IaaSClusterConfig>
      <Subscription>
        <SubscriptionId>99999999-9999-9999-9999-999999999999</SubscriptionId>
        <StorageAccount>mystorageaccount</StorageAccount>
      </Subscription>
      <Location>North Europe</Location>
      <VNet>
        <VNetName>hpcvnetne</VNetName>
        <SubnetName>subnet-hpc</SubnetName>
      </VNet>
      <Domain>
        <DCOption>HeadNodeAsDC</DCOption>
        <DomainFQDN>hpc.local</DomainFQDN>
      </Domain>
      <Database>
        <DBOption>LocalDB</DBOption>
      </Database>
      <HeadNode>
        <VMName>myhpchn</VMName>
        <ServiceName>myhpchn</ServiceName>
        <VMSize>Standard_D4</VMSize>
      </HeadNode>
      <LinuxComputeNodes>
        <VMNamePattern>lnxcn-%0001%</VMNamePattern>
        <ServiceNamePattern>mylnxcn%01%</ServiceNamePattern>
        <MaxNodeCountPerService>20</MaxNodeCountPerService>
        <StorageAccountNamePattern>mylnxstorage%01%</StorageAccountNamePattern>
        <VMSize>A9</VMSize>
        <NodeCount>0</NodeCount>
        <ImageName>b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-hpc-v20150708</ImageName>
      </LinuxComputeNodes>
    </IaaSClusterConfig>

Démarrer la création du nœud principal et hello en exécutant la commande PowerShell de hello dans une invite de commandes avec élévation de privilèges :

```
    .\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml
```

Après 20 minutes too30, du nœud principal hello devrait être prêt. Vous pouvez vous connecter tooit hello portail Azure en cliquant sur hello **Connect** icône de l’ordinateur virtuel de hello.

Vous pouvez éventuellement avoir redirecteur DNS de hello toofix. toodo, démarrez le Gestionnaire DNS.

1. Nom du serveur hello avec le bouton droit dans le Gestionnaire de DNS, sélectionnez **propriétés**, puis cliquez sur hello **redirecteurs** onglet.
2. Cliquez sur hello **modifier** bouton tooremove tous les redirecteurs, puis cliquez sur **OK**.
3. Vérifiez que hello **utiliser les indications de racine si aucune des redirecteurs ne sont disponibles** case à cocher est sélectionnée, puis cliquez sur **OK**.

## <a name="set-up-linux-compute-nodes"></a>Créer les nœuds de calcul Linux
Vous déployez des nœuds de calcul hello Linux à l’aide de hello même modèle de déploiement que vous avez utilisé le nœud principal de toocreate hello.

Copier le fichier hello **MyCluster.xml** depuis votre nœud principal de toohello ordinateur local et mise à jour hello **NodeCount** balise avec un nombre de hello de nœuds que vous souhaitez toodeploy (< = 20). Être prudent toohave assez de cœurs disponibles dans votre quota de Azure, car chaque instance A9 consommera 16 cœurs dans votre abonnement. Vous pouvez utiliser des instances de A8 (8 cœurs) au lieu de A9 si vous souhaitez toouse davantage d’ordinateurs virtuels dans hello même budget.

Sur le nœud principal de hello, copiez les scripts de déploiement IaaS de HPC Pack hello.

Exécutez hello suivant les commandes Azure PowerShell dans une invite de commandes avec élévation de privilèges :

1. Exécutez **Add-AzureAccount** tooconnect tooyour abonnement Azure.
2. Si vous avez plusieurs abonnements, exécutez **Get-AzureSubscription** toolist les.
3. Définir un abonnement par défaut en exécutant hello **Select-AzureSubscription - SubscriptionName xxxx-par défaut** commande.
4. Exécutez **.\New-HPCIaaSCluster.ps1 - ConfigFile MyCluster.xml** toostart déploiement de nœuds de calcul Linux.
   
   ![Déploiement d’un nœud principal en action][hndeploy]

Ouvrez l’outil de gestionnaire du Cluster HPC Pack hello. Après quelques minutes, des nœuds de calcul Linux apparaîtront régulièrement dans la liste. Avec le mode de déploiement classique de hello, les machines virtuelles IaaS sont créés de façon séquentielle. Par conséquent, si le nombre de hello de nœuds est important, obtention tous déployé peut prendre beaucoup de temps.

![Nœuds Linux dans le Gestionnaire de cluster de HPC Pack][clustermanager]

Maintenant que tous les nœuds sont en cours d’exécution dans un cluster de hello, il existe une infrastructure supplémentaire paramètres toomake.

## <a name="set-up-an-azure-file-share-for-windows-and-linux-nodes"></a>Configurer un partage Azure File pour les nœuds Windows et Linux
Vous pouvez utiliser des scripts de toostore hello Azure File service, les packages d’applications et fichiers de données. Azure File fournit des fonctionnalités CIFS en plus d’un stockage d’objets blob Azure comme magasin persistant. N’oubliez pas que cela n’est pas solution plus évolutive de hello, mais il est hello celle la plus simple et ne nécessite pas dédié de machines virtuelles.

Créer un partage de fichiers Azure en suivant les instructions de hello dans l’article de hello [prise en main avec un stockage de fichier Azure sur Windows](../../../storage/files/storage-dotnet-how-to-use-files.md).

Conservez votre compte de stockage en tant que nom hello **saname**, nom de partage de fichiers hello en tant que **nom_partage**et la clé de compte de stockage hello en tant que **sakey**.

### <a name="mount-hello-azure-file-share-on-hello-head-node"></a>Partage de fichiers Azure hello de montage sur le nœud principal de hello
Ouvrez une invite de commandes avec élévation de privilèges et exécutez hello suit les informations d’identification de commande toostore hello dans le coffre hello ordinateur local :

```
    cmdkey /add:<saname>.file.core.windows.net /user:<saname> /pass:<sakey>
```

Ensuite, toomount hello Azure partage de fichiers, exécutez :

```
    net use Z: \\<saname>.file.core.windows.net\<sharename> /persistent:yes
```

### <a name="mount-hello-azure-file-share-on-linux-compute-nodes"></a>Monter le partage de fichiers Azure hello sur les nœuds de calcul Linux
Un outil utile qui est fourni avec HPC Pack est outil de clusrun hello. Vous pouvez utiliser cette hello toorun d’outil de ligne de commande même commande simultanément sur un ensemble de nœuds de calcul. Dans notre cas, il utilise le partage de fichiers Azure hello toomount et rendre persistant toosurvive redémarrages.
Dans une invite de commandes avec élévation de privilèges sur le nœud principal de hello, exécutez hello suivant les commandes.

répertoire de montage toocreate hello :

```
    clusrun /nodegroup:LinuxNodes mkdir -p /hpcdata
```

hello toomount partage de fichiers Azure :

```
    clusrun /nodegroup:LinuxNodes mount -t cifs //<saname>.file.core.windows.net/<sharename> /hpcdata -o vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777
```

partage de montage toopersist hello :

```
    clusrun /nodegroup:LinuxNodes "echo //<saname>.file.core.windows.net/<sharename> /hpcdata cifs vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777 >> /etc/fstab"
```

## <a name="install-star-ccm"></a>Installer STAR-CCM+
Les instances A8 et A9 de machine virtuelle Azure prennent en charge InfiniBand et les fonctionnalités RDMA. les pilotes de noyau Hello qui permettent ces fonctionnalités sont disponibles pour Windows Server 2012 R2, SUSE 12, CentOS 6.5 et images CentOS 7.1 Bonjour Azure Marketplace. Microsoft MPI et Intel MPI (version 5.x) sont hello deux MPI bibliothèques qui prennent en charge les pilotes compris dans Azure.

CD-adapco STAR-CCM+ 11.x et version ultérieure est fourni avec Intel MPI version 5.x et prend donc en charge InfiniBand pour Azure.

Obtenir hello Linux64 étoile-package CCM + à partir de hello [CD-adapco portal](https://steve.cd-adapco.com). Dans notre cas, nous avons utilisé la version 11.02.010 en précision mixte.

Sur le nœud principal hello, Bonjour **/hpcdata** fichier Azure partage, créez un script shell intitulé **setupstarccm.sh** avec hello suivant le contenu. Ce script est exécuté sur chaque tooset de nœud de calcul des ÉTOILES-CCM + localement.

#### <a name="sample-setupstarcmsh-script"></a>Exemple de script setupstarcm.sh
```
    #!/bin/bash
    # setupstarcm.sh tooset up STAR-CCM+ locally

    # Create hello CD-adapco main directory
    mkdir -p /opt/CD-adapco

    # Copy hello STAR-CCM package from hello file share toohello local directory
    cp /hpcdata/StarCCM/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz /opt/CD-adapco/

    # Extract hello package
    tar -xzf /opt/CD-adapco/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz -C /opt/CD-adapco/

    # Start a silent installation of STAR-CCM without hello FLEXlm component
    /opt/CD-adapco/starccm+_11.02.010/STAR-CCM+11.02.010_01_linux-x86_64-2.5_gnu4.8.bin -i silent -DCOMPUTE_NODE=true -DNODOC=true -DINSTALLFLEX=false

    # Update memory limits
    echo "*               hard    memlock         unlimited" >> /etc/security/limits.conf
    echo "*               soft    memlock         unlimited" >> /etc/security/limits.conf
```
Maintenant, tooset d’étoile-CCM + sur tous vos Linux nœuds de calcul, ouvrez une invite de commandes avec élévation de privilèges et exécutez hello de commande suivante :

```
    clusrun /nodegroup:LinuxNodes bash /hpcdata/setupstarccm.sh
```

Pendant l’exécution de la commande hello, vous pouvez surveiller l’utilisation du processeur hello à l’aide de carte thermique hello du Gestionnaire du Cluster. Après quelques minutes, tous les nœuds devraient être correctement installés.

## <a name="run-star-ccm-jobs"></a>Exécuter des travaux STAR-CCM+
HPC Pack est utilisé pour ses fonctionnalités de planificateur de tâche dans l’ordre toorun étoile-CCM + travaux. toodo par conséquent, nous devons hello prise en charge de scripts certains travaux de hello toostart utilisés et exécutées en étoile-CCM +. les données d’entrée Hello sont conservées sur le partage de fichiers Azure hello premier par souci de simplicité.

Hello PowerShell script suivant est utilisé tooqueue une étoile-travail CCM +. Il tient compte de trois arguments :

* nom du modèle Hello
* nombre de Hello de toobe de nœuds utilisé
* nombre de Hello de cœurs sur chaque toobe nœud utilisé

Étant donné qu’étoile-CCM + peuvent remplir la bande passante de mémoire hello, ses généralement une meilleure toouse moins noyaux par les nœuds de calcul et ajouter de nouveaux nœuds. nombre exact de Hello de cœurs par nœud dépend de la famille de processeurs hello et la vitesse d’interconnexion hello.

les nœuds de Hello sont allouées exclusivement pour le travail de hello et ne peut pas être partagés avec d’autres tâches. travail de Hello n’est pas démarré directement comme un travail MPI. Hello **runstarccm.sh** script shell démarrera Lanceur MPI hello.

Hello d’entrée de modèle et hello **runstarccm.sh** script sont stockés dans hello **/hpcdata** partage a été précédemment chargé.

Les fichiers journaux sont nommés avec l’ID de tâche hello et sont stockées dans hello **/hpcdata partage**, ainsi que de hello étoile-CCM + fichiers de sortie.

#### <a name="sample-submitstarccmjobps1-script"></a>Exemple de script SubmitStarccmJob.ps1
```
    Add-PSSnapin Microsoft.HPC -ErrorAction silentlycontinue
    $scheduler="headnodename"
    $modelName=$args[0]
    $nbCoresPerNode=$args[2]
    $nbNodes=$args[1]

    #---------------------------------------------------------------------------------------------------------
    # Create a new job; this will give us hello job ID that's used tooidentify hello name of hello uploaded package in Azure
    #
    $job = New-HpcJob -Name "$modelName $nbNodes $nbCoresPerNode" -Scheduler $scheduler -NumNodes $nbNodes -NodeGroups "LinuxNodes" -FailOnTaskFailure $true -Exclusive $true
    $jobId = [String]$job.Id

    #---------------------------------------------------------------------------------------------------------
    # Submit hello job     
    $workdir =  "/hpcdata"
    $execName = "$nbCoresPerNode runner.java $modelName.sim"

    $job | Add-HpcTask -Scheduler $scheduler -Name "Compute" -stdout "$jobId.log" -stderr "$jobId.err" -Rerunnable $false -NumNodes $nbNodes -Command "runstarccm.sh $execName" -WorkDir "$workdir"


    Submit-HpcJob -Job $job -Scheduler $scheduler
```
Remplacez le **runner.java** par le lanceur de modèle Java STAR-CCM+ de votre choix et votre code de journalisation.

#### <a name="sample-runstarccmsh-script"></a>Exemple de script runstarccm.sh
```
    #!/bin/bash
    echo "start"
    # hello path of this script
    SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
    echo ${SCRIPT_PATH}
    # Set hello mpirun runtime environment
    export CDLMD_LICENSE_FILE=1999@flex.cd-adapco.com

    # mpirun command
    STARCCM=/opt/CD-adapco/STAR-CCM+11.02.010/star/bin/starccm+

    # Get node information from ENVs
    NODESCORES=(${CCP_NODES_CORES})
    COUNT=${#NODESCORES[@]}
    NBCORESPERNODE=$1

    # Create hello hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$
    echo ${NODELIST_PATH}

    # Get every node name and write into hello hostfile file
    I=1
    NBNODES=0
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
        let "NBNODES=${NBNODES}+1"
    done
    let "NBCORES=${NBNODES}*${NBCORESPERNODE}"

    # Run STAR-CCM with hello hostfile argument
    #  
    ${STARCCM} -np ${NBCORES} -machinefile ${NODELIST_PATH} \
        -power -podkey "<yourkey>" -rsh ssh \
        -mpi intel -fabric UDAPL -cpubind bandwidth,v \
        -mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0" \
        -batch $2 $3
    RTNSTS=$?
    rm -f ${NODELIST_PATH}

    exit ${RTNSTS}
```

Dans notre test, nous avons utilisé un jeton de licence Power-On-Demand, Pour ce jeton, vous avez tooset hello **$CDLMD_LICENSE_FILE** variable d’environnement trop **1999@flex.cd-adapco.com**  et la clé hello Bonjour **- podkey** option de ligne de commande hello .

Après une initialisation, le script de hello extrait--hello **$CCP_NODES_CORES** variables d’environnement HPC Pack définir--hello liste de toobuild nœuds un fichier d’hôte qui hello Lanceur de MPI utilise. Ce fichier d’hôte doit contenir une liste de hello des noms de nœud de calcul qui sont utilisés pour la tâche hello, un nom par ligne.

format Hello de **$CCP_NODES_CORES** suit ce modèle :

```
<Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
```

Où :

* `<Number of nodes>`est nombre hello de nœuds allouée toothis travail.
* `<Name of node_n_...>`est le nom hello de chaque nœud allouée toothis travail.
* `<Cores of node_n_...>`est nombre hello de cœurs sur le nœud hello allouée toothis travail.

Hello du nombre de cœurs (**$NBCORES**) est également calculée hello en fonction de nombre de nœuds (**$NBNODES**) et le nombre de hello de cœurs par nœud (fourni comme paramètre **$NBCORESPERNODE**).

Pour les options de MPI hello, hello ceux qui sont utilisés avec MPI Intel sur Azure sont :

* `-mpi intel`toospecify Intel MPI.
* `-fabric UDAPL`verbes toouse InfiniBand de Azure.
* `-cpubind bandwidth,v`la bande passante toooptimize pour MPI avec étoile-CCM +.
* `-mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0"`toomake Intel MPI fonctionnent avec Azure InfiniBand et tooset hello nécessaire le nombre de cœurs par nœud.
* `-batch`toostart en étoile-CCM + en mode batch sans interface utilisateur.

Enfin, toostart un travail, assurez-vous que vos nœuds sont en cours d’exécution et en ligne dans le Gestionnaire du Cluster. Puis, dans une invite de commandes PowerShell, exécutez la commande suivante :

```
    .\ SubmitStarccmJob.ps1 <model> <nbNodes> <nbCoresPerNode>
```

## <a name="stop-nodes"></a>Arrêter les nœuds
Une fois que vous avez terminé avec vos tests, vous pouvez utiliser hello suivant HPC Pack PowerShell commandes toostop et démarrer les nœuds :

```
    Stop-HPCIaaSNode.ps1 -Name <prefix>-00*
    Start-HPCIaaSNode.ps1 -Name <prefix>-00*
```

## <a name="next-steps"></a>Étapes suivantes
Essayez d’exécuter d’autres charges de travail Linux, par exemple :

* [Exécution de NAMD avec Microsoft HPC Pack sur des nœuds de calcul Linux dans Azure](hpcpack-cluster-namd.md)
* [Exécuter OpenFOAM avec Microsoft HPC Pack sur un cluster Linux RDMA dans Azure](hpcpack-cluster-openfoam.md)

<!--Image references-->
[hndeploy]:media/hpcpack-cluster-starccm/hndeploy.png
[clustermanager]:media/hpcpack-cluster-starccm/ClusterManager.png
