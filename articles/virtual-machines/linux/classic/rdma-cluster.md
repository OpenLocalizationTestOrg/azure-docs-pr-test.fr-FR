---
title: aaaSet une applications MPI de Linux RDMA cluster toorun | Documents Microsoft
description: "Créer un cluster de Linux de la taille des toouse H16r, H16mr, A8 ou A9 VMs les applications MPI toorun hello RDMA Azure réseau"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 01834bad-c8e6-48a3-b066-7f1719047dd2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: danlep
ms.openlocfilehash: 3199317a37b095e80718d6724954687d30aea3a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-linux-rdma-cluster-toorun-mpi-applications"></a>Configurer une application MPI de Linux RDMA cluster toorun
Découvrez comment tooset d’un RDMA Linux cluster dans Azure avec [tailles de machine virtuelle de calcul haute performance](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toorun les applications Interface MPI (Message Passing) parallèles. Cet article fournit des étapes tooprepare un toorun d’image Linux HPC Intel MPI sur un cluster. Après la préparation, vous déployez un cluster d’ordinateurs virtuels à l’aide de cette image et l’une des tailles de machine virtuelle de Azure prend en charge RDMA hello (actuellement H16r, H16mr, A8 ou A9). Utilisez hello cluster toorun des applications MPI qui communiquent efficacement sur un réseau à faible latence, à débit élevé en fonction de la technologie direct à la mémoire à distance (RDMA) d’accès.

> [!IMPORTANT]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Azure Resource Manager](../../../resource-manager-deployment-model.md) et classique. Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.

## <a name="cluster-deployment-options"></a>Options de déploiement de cluster
Voici les méthodes toocreate un cluster Linux RDMA avec ou sans un planificateur de travaux.

* **Les scripts CLI Azure**: comme indiqué plus loin dans cet article, utilisez hello [interface de ligne de commande Azure](../../../cli-install-nodejs.md) déploiement de hello tooscript (CLI) d’un cluster d’ordinateurs virtuels prenant en charge RDMA. Hello CLI en mode de gestion de Service crée hello nœuds de cluster en série dans le modèle de déploiement classique de hello, afin de déployer plusieurs nœuds de calcul peut prendre plusieurs minutes. tooenable hello connexion de réseau RDMA lorsque vous utilisez le modèle de déploiement classique de hello, déployez des machines virtuelles hello Bonjour même service cloud.
* **Les modèles de gestionnaire de ressources Azure**: vous pouvez également utiliser hello Gestionnaire de ressources du déploiement modèle toodeploy un cluster d’ordinateurs virtuels prenant en charge RDMA qui relie toohello RDMA. Vous pouvez [créer votre propre modèle](../../../resource-group-authoring-templates.md), ou vérifiez hello [modèles de démarrage rapide Azure](https://azure.microsoft.com/documentation/templates/) pour les modèles fournis par Microsoft hello Communauté toodeploy hello solution ou souhaité. Modèles du Gestionnaire de ressources peuvent fournir un moyen rapide et fiable de toodeploy un cluster Linux. tooenable hello connexion de réseau RDMA lorsque vous utilisez le modèle de déploiement du Gestionnaire de ressources hello, déployer des machines virtuelles de hello Bonjour même groupe à haute disponibilité.
* **HPC Pack**: créer un cluster Microsoft HPC Pack dans Azure et ajouter des nœuds de calcul prenant en charge RDMA qui s’exécutent à un réseau RDMA hello de prise en charge Linux distribution tooaccess. Pour plus d’informations, consultez [Prise en main des nœuds de calcul Linux dans un cluster HPC Pack dans Azure](hpcpack-cluster.md).

## <a name="sample-deployment-steps-in-hello-classic-model"></a>Étapes de l’exemple de déploiement dans le modèle classique de hello
Hello étapes suivantes montrent comment toouse hello CLI d’Azure toodeploy une machine virtuelle de SUSE Linux Enterprise Server 12 (SLES) SP1 HPC de hello Azure Marketplace, personnaliser et créer une image de machine virtuelle personnalisée. Ensuite, vous pouvez utiliser déploiement de hello tooscript hello image d’un cluster d’ordinateurs virtuels prenant en charge RDMA.

> [!TIP]
> Utilisez similaire toodeploy comme un cluster d’ordinateurs virtuels prenant en charge RDMA basé sur des images HPC de base CentOS Bonjour Azure Marketplace. Certaines étapes diffèrent légèrement, comme indiqué. 
>
>

### <a name="prerequisites"></a>Composants requis
* **Ordinateur client**: vous avez besoin d’un toocommunicate d’ordinateur client Mac, Linux ou Windows Azure. Ces étapes supposent que vous utilisez un client Linux.
* **Abonnement Azure** : si vous n’en avez pas, vous pouvez créer un [compte gratuit](https://azure.microsoft.com/free/) en quelques minutes. Pour les clusters de grande taille, envisagez de souscrire un abonnement de paiement à l’utilisation ou d’autres options d’achat.
* **Disponibilité de taille de machine virtuelle**: hello suivant des tailles d’instance est compatible RDMA : H16r, H16mr, A8 et A9. Pour connaître la disponibilité dans les différentes régions Azure, voir [Disponibilité des produits par région](https://azure.microsoft.com/regions/services/) .
* **Quota de cœurs**: vous devrez peut-être le quota de hello tooincrease de cœurs toodeploy un cluster de machines virtuelles de calcul intensif. Par exemple, vous devez au moins 128 cœurs si vous souhaitez toodeploy 8 machines virtuelles de A9 comme indiqué dans cet article. Votre abonnement peut également limiter hello nombre de cœurs, que vous pouvez déployer dans certaines familles de taille de machine virtuelle, y compris hello H-series. un quota de toorequest augmenter, [ouvrir une demande de support client en ligne](../../../azure-supportability/how-to-create-azure-support-request.md) sans frais.
* **CLI Azure**: [installer](../../../cli-install-nodejs.md) hello CLI d’Azure et [connecter tooyour abonnement Azure](../../../xplat-cli-connect.md) à partir de l’ordinateur client de hello.

### <a name="provision-an-sles-12-sp1-hpc-vm"></a>Configurer une machine virtuelle SLES 12 SP1 HPC
Une fois connectés tooAzure avec hello CLI d’Azure, exécutez `azure config list` tooconfirm qui hello sortie montre le mode de gestion de Service. Si elle n’est pas le cas, définissez le mode hello en exécutant cette commande :

    azure config mode asm


Tapez hello suivant toolist tous les abonnements hello vous toouse autorisé sont :

    azure account list

abonnement actuel Hello est identifié avec `Current` défini trop`true`. Si cet abonnement n’est pas hello celui que vous souhaitez toouse toocreate hello cluster, définissez les ID de l’abonnement approprié hello en tant qu’abonnement hello :

    azure account set <subscription-Id>

toosee hello disponibles publiquement images SLES 12 SP1 HPC dans Azure, exécutez une commande telle que hello suivant, en supposant que votre environnement de shell prend en charge **grep**:

    azure vm image list | grep "suse.*hpc"

Configurer un ordinateur prenant en charge RDMA virtuel avec une image de SLES 12 SP1 HPC en exécutant une commande hello suivante :

    azure vm create -g <username> -p <password> -c <cloud-service-name> -l <location> -z A9 -n <vm-name> -e 22 b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824

Où :

* taille de Hello (A9 dans cet exemple) est une des tailles de machine virtuelle hello prenant en charge RDMA.
* numéro de port SSH externe Hello (22 dans cet exemple, qui est par défaut SSH de hello) est un numéro de port valide. numéro de port SSH Hello interne a la valeur too22.
* Un nouveau service cloud est créé dans hello région Azure spécifiée par l’emplacement de hello. Spécifiez un emplacement dans le machines virtuelles hello taille que vous choisissez est disponible.
* Pour un support de priorité SUSE (ce qui entraîne des frais supplémentaires), nom de l’image hello SLES 12 SP1 actuellement peut prendre l’une de ces deux options : 

 `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824`

  `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-priority-v20160824`


### <a name="customize-hello-vm"></a>Personnaliser hello machine virtuelle
Hello machine virtuelle après l’approvisionnement, SSH toohello machine virtuelle à l’aide de hello adresse IP externe de l’ordinateur virtuel (ou le nom DNS) et hello numéro de port externe que vous avez configuré et ensuite le personnaliser. Pour plus d’informations de connexion, consultez [comment toolog sur l’ordinateur virtuel de tooa exécutant Linux](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Exécuter des commandes en tant qu’utilisateur hello que vous avez configurés sur hello machine virtuelle, sauf si l’accès à la racine est une étape de toocomplete requis.

> [!IMPORTANT]
> Microsoft Azure ne fournit pas d’accès racine tooLinux VMs. un accès administratif toogain lorsqu’il est connecté en tant qu’un utilisateur de toohello machine virtuelle, exécuter des commandes à l’aide de `sudo`.
>
>

* **Mises à jour** : installez les mises à jour à l’aide de zypper. Vous pourriez également des utilitaires NFS tooinstall.

  > [!IMPORTANT]
  > Dans une machine de HPC virtuelle SLES 12 SP1, nous vous recommandons de ne pas appliquer les mises à jour du noyau, ce qui peuvent entraîner des problèmes avec hello Linux RDMA pilotes.
  >
  >
* **Intel MPI**: installer hello d’Intel sur hello SLES 12 SP1 HPC virtuelle en exécutant hello de commande suivante :

        sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
* **Verrouiller la mémoire**: MPI codes toolock hello mémoire disponible pour RDMA, ajouter ou modifier des hello suivant les paramètres dans le fichier de /etc/security/limits.conf hello. Vous devez tooedit d’accès racine de ce fichier.

    ```
    <User or group name> hard    memlock <memory required for your application in KB>

    <User or group name> soft    memlock <memory required for your application in KB>
    ```

  > [!NOTE]
  > À des fins de test, vous pouvez également définir memlock toounlimited. Par exemple : `<User or group name>    hard    memlock unlimited`. Pour plus d’informations, voir les [meilleures méthodes connues pour définir la taille de mémoire verrouillée](https://software.intel.com/en-us/blogs/2014/12/16/best-known-methods-for-setting-locked-memory-size).
  >
  >
* **Clés SSH pour les machines virtuelles SLES**: générer SSH clés tooestablish confiance pour votre compte d’utilisateur entre hello nœuds hello SLES cluster de calcul lors de l’exécution des travaux MPI. Si vous avez déployé une machine virtuelle HPC basée sur CentOS, ne suivez pas cette étape. Une fois que vous capturez l’image de hello et à déployez hello cluster, consultez les instructions plus loin dans cette tooset article passwordless SSH relation de confiance entre les nœuds de cluster hello.

    clés SSH toocreate, exécutez hello commande suivante. Lorsque vous êtes invité pour l’entrée, sélectionnez **entrée** toogenerate les clés de hello dans l’emplacement par défaut de hello sans définir un mot de passe.

        ssh-keygen

    Ajouter le fichier d’authorized_keys hello toohello de clé publique pour les clés publiques connus.

        cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys

    Dans le répertoire de ~/.ssh hello, modifier ou créer le fichier de configuration hello. Fournir plage d’adresses IP hello de réseau privé de hello que vous envisagez de toouse dans Azure (10.32.0.0/16 dans cet exemple) :

        host 10.32.0.*
        StrictHostKeyChecking no

    Vous pouvez également répertorier des adresse hello réseau privé de chaque machine virtuelle dans votre cluster comme suit :

    ```
    host 10.32.0.1
     StrictHostKeyChecking no
    host 10.32.0.2
     StrictHostKeyChecking no
    host 10.32.0.3
     StrictHostKeyChecking no
    ```

  > [!NOTE]
  > La configuration de `StrictHostKeyChecking no` peut créer un risque de sécurité potentiel si une adresse IP ou une plage d’adresses IP spécifiques ne sont pas spécifiées.
  >
  >
* **Applications**: installer des applications que vous avez besoin ou effectuez d’autres personnalisations avant de capturer l’image de hello.

### <a name="capture-hello-image"></a>Capturer l’image de hello
image de hello toocapture, exécutez d’abord hello suivant de commande de hello Linux VM. Cette commande arrête hello machine virtuelle mais conserve les comptes d’utilisateur et les clés SSH que vous avez configurée.

```
sudo waagent -deprovision
```

À partir de votre ordinateur client, exécutez hello suivant l’image de hello de toocapture de commandes CLI d’Azure. Pour plus d’informations, consultez [comment toocapture une machine virtuelle de Linux classique comme image](capture-image.md).  

```
azure vm shutdown <vm-name>

azure vm capture -t <vm-name> <image-name>

```

Après avoir exécuté ces commandes, image de machine virtuelle hello est capturé pour votre utilisation et hello machine virtuelle est supprimé. Vous disposez à présent votre toodeploy prêt image personnalisée un cluster.

### <a name="deploy-a-cluster-with-hello-image"></a>Déployer un cluster avec l’image de hello
Modifier hello script d’interpréteur de commandes avec les valeurs appropriées pour votre environnement suivant et exécutez-le à partir de votre ordinateur client. Étant donné que Azure déploie les machines virtuelles de hello en série dans le modèle de déploiement classique de hello, prend quelques minutes toodeploy hello huit machines virtuelles de A9 suggérés dans ce script.

```
#!/bin/bash -x
# Script toocreate a compute cluster without a scheduler in a VNet in Azure
# Create a custom private network in Azure
# Replace 10.32.0.0 with your virtual network address space
# Replace <network-name> with your network identifier
# Replace "West US" with an Azure region where hello VM size is available
# See Azure Pricing pages for prices and availability of compute-intensive VMs

azure network vnet create -l "West US" -e 10.32.0.0 -i 16 <network-name>

# Create a cloud service. All hello compute-intensive instances need toobe in hello same cloud service for Linux RDMA toowork across InfiniBand.
# Note: hello current maximum number of VMs in a cloud service is 50. If you need tooprovision more than 50 VMs in hello same cloud service in your cluster, contact Azure Support.

azure service create <cloud-service-name> --location "West US" –s <subscription-ID>

# Define a prefix naming scheme for compute nodes, e.g., cluster11, cluster12, etc.

vmname=cluster

# Define a prefix for external port numbers. If you want tooturn off external ports and use only internal ports toocommunicate between compute nodes via port 22, don’t use this option. Since port numbers up too10000 are reserved, use numbers after 10000. Leave external port on for rank 0 and head node.

portnumber=101

# In this cluster there will be 8 size A9 nodes, named cluster11 toocluster18. Specify your captured image in <image-name>. Specify hello username and password you used when creating hello SSH keys.

for (( i=11; i<19; i++ )); do
        azure vm create -g <username> -p <password> -c <cloud-service-name> -z A9 -n $vmname$i -e $portnumber$i -w <network-name> -b Subnet-1 <image-name>
done

# Save this script with a name like makecluster.sh and run it in your shell environment tooprovision your cluster
```

## <a name="considerations-for-a-centos-hpc-cluster"></a>Considérations pour un cluster HPC CentOS
Si vous souhaitez tooset configuration d’un cluster basé sur l’une des images HPC de base CentOS hello Bonjour Azure Marketplace, au lieu de SLES 12 pour HPC, procédez hello général hello précédant la section. Notez hello suivant différences lorsque vous configurez, configurez hello machine virtuelle :

- Intel MPI est déjà installé sur une machine virtuelle approvisionnée à partir d’une image de HPC basée sur CentOS.
- Verrouiller les paramètres de mémoire sont déjà ajoutés dans /etc/security/limits.conf fichier la machine virtuelle hello.
- Ne pas générer les clés SSH sur hello machine virtuelle que vous configurez pour la capture. Au lieu de cela, nous vous recommandons de configurer l’authentification basée sur l’utilisateur après le déploiement de cluster de hello. Pour plus d’informations, consultez hello suivant la section.  

### <a name="set-up-passwordless-ssh-trust-on-hello-cluster"></a>Configurez passwordless approbation SSH sur le cluster de hello
Sur un cluster HPC de base CentOS, il existe deux méthodes pour établir une approbation entre les nœuds de calcul hello : l’authentification basée sur l’hôte et l’authentification basée sur l’utilisateur. L’authentification basée sur l’hôte n’est pas décrite hello de cet article et doit généralement être effectuée via un script d’extension pendant le déploiement. L’authentification basée sur l’utilisateur est pratique pour établir une approbation après le déploiement et requiert la génération de hello et le partage des clés SSH hello parmi les nœuds de calcul dans le cluster de hello. Cette méthode est communément appelée connexion SSH sans mot de passe. Elle est requise lors de l’exécution de travaux MPI.

Un exemple de script obtenue à partir de la Communauté de hello est disponible sur [GitHub](https://github.com/tanewill/utils/blob/master/user_authentication.sh) tooenable l’authentification utilisateur simple sur un cluster HPC de base CentOS. Télécharger et utiliser ce script à l’aide de hello comme suit. Vous pouvez également modifier ce script, ou utiliser n’importe quel autre méthode tooestablish passwordless SSH authentification entre les nœuds de calcul hello.

    wget https://raw.githubusercontent.com/tanewill/utils/master/ user_authentication.sh

script de hello toorun, vous devez préfixe de hello tooknow pour vos adresses IP du sous-réseau. Obtient le préfixe de hello en exécutant la commande suivante sur l’un des nœuds de cluster hello de hello. Votre sortie doit ressembler à 10.1.3.5 et préfixe de hello est la partie de hello 10.1.3.

    ifconfig eth0 | grep -w inet | awk '{print $2}'

À présent exécuter script hello à l’aide de trois paramètres : hello utilisateur nom commun sur hello des nœuds de calcul, le mot de passe commun hello pour cet utilisateur hello sur les nœuds de calcul et du préfixe de sous-réseau de hello qui a été retourné à partir de la commande précédente hello.

    ./user_authentication.sh <myusername> <mypassword> 10.1.3

Ce script hello suivant :

* Crée un répertoire sur le nœud d’hôte hello nommé .ssh, qui est requis pour la connexion passwordless.
* Crée un fichier de configuration dans le répertoire .ssh hello qui indique la connexion de tooallow passwordless de connexion à partir de n’importe quel nœud dans le cluster de hello.
* Crée des fichiers contenant les noms de nœud hello et les adresses IP de nœud de tous les nœuds hello dans un cluster de hello. Ces fichiers sont conservés après l’exécution de script de hello pour référence ultérieure.
* Crée une paire de clés privée et publique pour chaque nœud de cluster (y compris le nœud de l’hôte hello) et crée des entrées dans le fichier d’authorized_keys hello.

> [!WARNING]
> L’exécution de ce script peut créer un risque de sécurité potentiel. Vérifiez que hello informations de clé publique ~/.ssh ne sont pas distribuées.
>
>

## <a name="configure-intel-mpi"></a>Configurer Intel MPI
toorun des applications MPI sur Azure Linux RDMA, vous devez tooconfigure certaine variables d’environnement spécifiques tooIntel MPI. Voici un toorun de variables nécessaires exemple Bash script tooconfigure hello une application. Modifiez toompivars.sh de chemin d’accès hello en fonction des besoins de votre installation de Intel MPI.

```
#!/bin/bash -x

# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh

export I_MPI_FABRICS=shm:dapl

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB
# Setting hello variable tooshm:dapl gives best performance for some applications
# If your application doesn’t take advantage of shared memory and MPI together, then set only dapl

export I_MPI_DAPL_PROVIDER=ofa-v2-ib0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

export I_MPI_DYNAMIC_CONNECTION=0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

# Command line toorun hello job

mpirun -n <number-of-cores> -ppn <core-per-node> -hostfile <hostfilename>  /path <path toohello application exe> <arguments specific toohello application>

#end
```

format Hello du fichier d’hôte hello est comme suit. Ajoutez une ligne pour chaque nœud de votre cluster. Spécifiez les adresses IP privées à partir du réseau virtuel de hello définie précédemment, pas les noms DNS. Par exemple, pour deux ordinateurs hôtes avec les adresses IP 10.32.0.1 et 10.32.0.2, fichier de hello contient suivant de hello :

```
10.32.0.1:16
10.32.0.2:16
```

## <a name="run-mpi-on-a-basic-two-node-cluster"></a>Exécuter MPI sur un cluster à deux nœuds de base
Si vous n’avez pas déjà fait, définissez tout d’abord les environnement hello pour Intel MPI.

```
# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh
```

### <a name="run-an-mpi-command"></a>Exécution d’une commande MPI
Exécuter une commande MPI sur l’un des tooshow de nœuds de calcul hello MPI est correctement installé et peut communiquer au moins deux nœuds de calcul. suivant de Hello **mpirun** commande exécute hello **nom d’hôte** commande sur deux nœuds.

```
mpirun -ppn 1 -n 2 -hosts <host1>,<host2> -env I_MPI_FABRICS=shm:dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 hostname
```
Votre sortie doit répertorier les noms de tous les nœuds hello que vous avez transmise en tant qu’entrée pour hello `-hosts`. Par exemple, un **mpirun** commande avec deux nœuds retourne une sortie semblable à hello suivante :

```
cluster11
cluster12
```

### <a name="run-an-mpi-benchmark"></a>Exécution d'un test d'évaluation MPI
Hello Intel MPI commande suivante exécute pingpong banc d’essai tooverify hello configuration et connexion toohello RDMA réseau du cluster.

```
mpirun -hosts <host1>,<host2> -ppn 1 -n 2 -env I_MPI_FABRICS=dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 IMB-MPI1 pingpong
```

Sur un cluster opérationnel avec deux nœuds, vous devez voir la sortie suivante de hello. Sur le réseau RDMA Azure de hello, la latence ou inférieure à 3 microsecondes pour les formats de message des octets de too512 devrait.

```
#------------------------------------------------------------
#    Intel (R) MPI Benchmarks 4.0 Update 1, MPI-1 part
#------------------------------------------------------------
# Date                  : Fri Jul 17 23:16:46 2015
# Machine               : x86_64
# System                : Linux
# Release               : 3.12.39-44-default
# Version               : #5 SMP Thu Jun 25 22:45:24 UTC 2015
# MPI Version           : 3.0
# MPI Thread Environment:
# New default behavior from Version 3.2 on:
# hello number of iterations per message size is cut down
# dynamically when a certain run time (per message size sample)
# is expected toobe exceeded. Time limit is defined by variable
# "SECS_PER_SAMPLE" (=> IMB_settings.h)
# or through hello flag => -time

# Calling sequence was:
# /opt/intel/impi_latest/bin64/IMB-MPI1 pingpong
# Minimum message length in bytes:   0
# Maximum message length in bytes:   4194304
#
# MPI_Datatype                   :   MPI_BYTE
# MPI_Datatype for reductions    :   MPI_FLOAT
# MPI_Op                         :   MPI_SUM
#
#
# List of Benchmarks toorun:
# PingPong
#---------------------------------------------------
# Benchmarking PingPong
# #processes = 2
#---------------------------------------------------
       #bytes #repetitions      t[usec]   Mbytes/sec
            0         1000         2.23         0.00
            1         1000         2.26         0.42
            2         1000         2.26         0.85
            4         1000         2.26         1.69
            8         1000         2.26         3.38
           16         1000         2.36         6.45
           32         1000         2.57        11.89
           64         1000         2.36        25.81
          128         1000         2.64        46.19
          256         1000         2.73        89.30
          512         1000         3.09       157.99
         1024         1000         3.60       271.53
         2048         1000         4.46       437.57
         4096         1000         6.11       639.23
         8192         1000         7.49      1043.47
        16384         1000         9.76      1600.76
        32768         1000        14.98      2085.77
        65536          640        25.99      2405.08
       131072          320        50.68      2466.64
       262144          160        80.62      3101.01
       524288           80       145.86      3427.91
      1048576           40       279.06      3583.42
      2097152           20       543.37      3680.71
      4194304           10      1082.94      3693.63

# All processes entering MPI_Finalize

```



## <a name="next-steps"></a>Étapes suivantes
* Déploiement et exécution de vos applications MPI Linux sur votre cluster Linux.
* Consultez hello [documentation de la bibliothèque de MPI Intel](https://software.intel.com/en-us/articles/intel-mpi-library-documentation/) pour obtenir des conseils sur Intel MPI.
* Essayez une [modèle de démarrage rapide](https://github.com/Azure/azure-quickstart-templates/tree/master/intel-lustre-clients-on-centos) toocreate un Lustre Intel cluster à l’aide d’une image basée sur CentOS HPC. Pour plus d’informations, consultez [Déploiement d’Intel Cloud Edition pour Lustre sur Microsoft Azure](https://blogs.msdn.microsoft.com/arsen/2015/10/29/deploying-intel-cloud-edition-for-lustre-on-microsoft-azure/).
