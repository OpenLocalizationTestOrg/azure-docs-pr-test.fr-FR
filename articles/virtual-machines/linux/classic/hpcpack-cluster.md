---
title: machines virtuelles de calcul aaaLinux dans un cluster HPC Pack | Documents Microsoft
description: "Découvrez comment toocreate et utilisez un HPC Pack du cluster dans Azure pour Linux à haute performance des charges de travail (HPC)"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 4d080fdd-5ffe-4f54-a78d-4c818f6eb3fb
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 10/12/2016
ms.author: danlep
ms.openlocfilehash: 9ed20d6cd69a6472a00666caf8965e9d022698a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-linux-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a>Prise en main des nœuds de calcul Linux dans un cluster HPC Pack dans Azure
Configurez un cluster [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029.aspx) dans Azure, contenant un nœud principal qui exécute Windows Server et plusieurs nœuds de calcul qui exécutent une distribution Linux. Explorer les options toomove des données entre les nœuds de Linux hello et nœud de cluster de hello tête de Windows hello. Découvrez comment toosubmit Linux HPC travaux toohello cluster.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

À un niveau élevé, hello diagramme suivant montre hello HPC Pack cluster vous créez et manipulez.

![Cluster HPC Pack avec nœuds Linux][scenario]

Pour les autres options de toorun Linux HPC les charges de travail dans Azure, consultez [ressources techniques pour le traitement et l’informatique hautes performances](../../../batch/big-compute-resources.md).

## <a name="deploy-an-hpc-pack-cluster-with-linux-compute-nodes"></a>Déployer un cluster HPC Pack avec des nœuds de calcul Linux
Cet article explique les toodeploy deux options vous un cluster HPC Pack dans Azure avec les nœuds de calcul Linux. Les deux méthodes utilisent une image de Marketplace de Windows Server avec du nœud principal HPC Pack toocreate hello. 

* **Modèle de gestionnaire de ressources Azure** -utiliser un modèle à partir de hello Azure Marketplace, ou un modèle de démarrage rapide de communauté hello, tooautomate la création du cluster hello dans le modèle de déploiement du Gestionnaire de ressources hello. Par exemple, hello [cluster HPC Pack pour les charges de travail Linux](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) modèle Bonjour Azure Marketplace permet de créer une infrastructure de cluster HPC Pack complète pour Linux HPC les charges de travail.
* **Script PowerShell** -hello d’utilisation [script de déploiement IaaS de Microsoft HPC Pack](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (**New-hpciaascluster.ps1**) tooautomate un déploiement de la création du cluster dans le modèle de déploiement classique hello. Ce script Azure PowerShell utilise une image de machine virtuelle HPC Pack Bonjour Azure Marketplace pour le déploiement rapide et fournit un ensemble complet de toodeploy des paramètres de configuration des nœuds de calcul Linux.

Pour plus d’informations sur les options de déploiement de cluster HPC Pack dans Azure, consultez [toocreate les Options et de gérer un cluster informatique de hautes performances (HPC) dans Azure avec Microsoft HPC Pack](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

### <a name="prerequisites"></a>Composants requis
* **Abonnement Azure** -vous pouvez utiliser un abonnement soit Bonjour service Global Azure ou Azure Chine. Si vous ne possédez pas de compte, vous pouvez créer un [compte gratuit](https://azure.microsoft.com/pricing/free-trial/) en quelques minutes.
* **Quota de cœurs** -vous devrez peut-être le quota de hello tooincrease de cœurs, en particulier si vous choisissez toodeploy plusieurs nœuds de cluster avec des tailles de machine virtuelle multicœurs. tooincrease un quota, ouvrez une demande de support technique en ligne sans frais.
* **Les distributions Linux** -actuellement HPC Pack prend en charge hello suivant des distributions de Linux pour les nœuds de calcul. Vous pouvez utiliser les versions Marketplace de ces distributions dans la mesure où elles sont disponibles, ou fournissez la vôtre.
  
  * **Basée sur centOS** : 6.5, 6.6, 6.7, 7.0, 7.1, 7.2, HPC 6.5, HPC 7.1
  * **Red Hat Enterprise Linux** : 6.7, 6.8, 7.2
  * **SUSE Linux Enterprise Server** : SLES 12, SLES 12 (Premium), SLES 12 SP1, SLES 12 SP1 (Premium), SLES 12 pour HPC, SLES 12 pour HPC (Premium)
  * **Ubuntu Server** : 14.04 LTS, 16.04 LTS
    
    > [!TIP]
    > réseau de RDMA Azure hello toouse avec l’une des tailles de machine virtuelle hello prenant en charge RDMA, spécifiez une image de SUSE Linux Enterprise Server 12 HPC ou HPC de base CentOS hello Azure Marketplace. Pour plus d’informations, consultez [Tailles de machine virtuelle de calcul haute performance](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
    > 
    > 

Cluster hello du toodeploy autres conditions préalables à l’aide du script de déploiement IaaS de HPC Pack hello :

* **Ordinateur client** -vous avez besoin d’un script de déploiement de clients basés sur Windows ordinateur toorun hello cluster.
* **Azure PowerShell** - [installez et configurez Azure PowerShell](/powershell/azure/overview) (version 0.8.10 ou ultérieure) sur votre ordinateur client.
* **Script de déploiement IaaS de HPC Pack** - Téléchargez et décompressez hello dernière version de script hello hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949). Vous pouvez vérifier la version hello du script de hello en exécutant `.\New-HPCIaaSCluster.ps1 –Version`. Cet article est basé sur la version 4.4.1 ou ultérieures du script de hello.

### <a name="deployment-option-1-use-a-resource-manager-template"></a>Option de déploiement 1. Utiliser un modèle Resource Manager
1. Accédez toohello [cluster HPC Pack pour les charges de travail Linux](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) modèle dans hello Azure Marketplace, puis cliquez sur **déployer**.
2. Hello portail Azure, passez en revue les informations hello et puis cliquez sur **créer**.
   
    ![Création de portail][portal]
3. Sur hello **notions de base** panneau, entrez un nom pour le cluster de hello, qui nomme également la machine virtuelle du nœud principal hello. Vous pouvez choisir un groupe de ressources existant ou créer un groupe pour le déploiement de hello dans un emplacement qui est tooyou disponible. emplacement Hello affecte disponibilité hello de certaines tailles de machine virtuelle et d’autres services Azure (consultez [produits disponibles par région](https://azure.microsoft.com/regions/services/)).
4. Sur hello **principal des paramètres de nœud** panneau, pour un premier déploiement, vous pouvez généralement accepter les paramètres par défaut de hello. 
   
   > [!NOTE]
   > Hello **l’URL du script de post-configuration** est facultative définissant toospecify un script Windows PowerShell disponible au public que vous souhaitez toorun sur la machine virtuelle du nœud principal hello quand il est en cours d’exécution. 
   > 
   > 
5. Sur hello **paramètres du nœud de calcul** panneau, sélectionnez un modèle d’affectation de noms pour les nœuds de hello, nombre de hello et taille des nœuds de hello et hello toodeploy de distribution de Linux.
6. Sur hello **paramètres d’Infrastructure** panneau, entrez les noms de réseau virtuel de hello et Active Directory domaine, le domaine et les informations d’identification d’administrateur de machine virtuelle et un modèle d’affectation de noms pour les comptes de stockage hello.
   
   > [!NOTE]
   > HPC Pack utilise hello les utilisateurs Active Directory domaine tooauthenticate cluster. 
   > 
   > 
7. Une fois l’exécution des tests de validation hello et que vous passez en revue les conditions d’utilisation de hello, cliquez sur **bon**.

### <a name="deployment-option-2-use-hello-iaas-deployment-script"></a>Option de déploiement 2. Utilisez le script de déploiement IaaS hello
Voici cluster de hello toodeploy autres conditions préalables à l’aide du script de déploiement IaaS de HPC Pack hello :

* **Ordinateur client** -vous avez besoin d’un script de déploiement de clients basés sur Windows ordinateur toorun hello cluster.
* **Azure PowerShell** - [installez et configurez Azure PowerShell](/powershell/azure/overview) (version 0.8.10 ou ultérieure) sur votre ordinateur client.
* **Script de déploiement IaaS de HPC Pack** - Téléchargez et décompressez hello dernière version de script hello hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949). Vous pouvez vérifier la version hello du script de hello en exécutant `.\New-HPCIaaSCluster.ps1 –Version`. Cet article est basé sur la version 4.4.1 ou ultérieures du script de hello.

**Fichier de configuration XML**

Hello script de déploiement IaaS de HPC Pack utilise un fichier de configuration XML en tant que cluster HPC de hello toodescribe d’entrée. Hello exemple de fichier de configuration suivant spécifie un petit cluster constitué d’un nœud principal HPC Pack et deux nœuds de calcul taille A7, CentOS Linux 7.0. 

Modifier le fichier de hello en fonction des besoins de votre environnement et la configuration de cluster souhaité et enregistrez-le sous un nom tel que HPCDemoConfig.xml. Par exemple, vous devez toosupply votre nom d’abonnement et un nom de compte de stockage unique et un nom de service cloud. En outre, vous pourriez toochoose une autre prise en charge Linux image pour les nœuds de calcul hello. Pour plus d’informations sur les éléments de hello dans le fichier de configuration hello, consultez fichier Manual.rtf de hello dans le dossier de scripts hello et [créer un cluster HPC avec hello script de déploiement IaaS de HPC Pack](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>allvhdsje</StorageAccount>
  </Subscription>
  <Location>Japan East</Location>  
  <VNet>
    <VNetName>centos7rdmavnetje</VNetName>
    <SubnetName>CentOS7RDMACluster</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>CentOS7RDMA-HN</VMName>
    <ServiceName>centos7rdma-je</ServiceName>
  <VMSize>ExtraLarge</VMSize>
  <EnableRESTAPI />
  <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>CentOS7RDMA-LN%1%</VMNamePattern>
    <ServiceName>centos7rdma-je</ServiceName>
    <VMSize>A7</VMSize>
    <NodeCount>2</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20150325</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```

**toorun hello script de déploiement IaaS de HPC Pack**

1. Ouvrez Windows PowerShell sur l’ordinateur client de hello en tant qu’administrateur.
2. Modification toohello du répertoire où le script de hello est installé (E:\IaaSClusterScript dans cet exemple).
   
    ```powershell
    cd E:\IaaSClusterScript
    ```
3. Exécutez hello suivant du cluster HPC Pack de commande toodeploy hello. Cet exemple suppose que ce fichier de configuration hello se trouve dans E:\HPCDemoConfig.xml
   
    ```powershell
    .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
    ```
   
    a. Étant donné que hello **AdminPassword** n’est pas spécifié dans hello précédant la commande, vous êtes invité à tooenter hello mot de passe utilisateur *MyAdminName*.
   
    b. script de Hello démarre ensuite le fichier de configuration toovalidate hello. Il peut prendre jusqu'à minutes tooseveral dépend de la connexion de réseau hello.
   
    ![Validation][validate]
   
    c. Une fois les validations passer, script de hello répertorie toocreate de ressources de cluster hello. Entrez *Y* toocontinue.
   
    ![Ressources][resources]
   
    d. script de Hello démarrage toodeploy hello HPC Pack cluster et termine la configuration hello sans davantage les étapes manuelles. script de Hello peut prendre plusieurs minutes.
   
    ![Déployer][deploy]
   
   > [!NOTE]
   > Dans cet exemple, hello script génère un fichier journal automatiquement depuis hello **- LogFile** paramètre n’est pas spécifié. Hello journaux ne sont pas écrites en temps réel, mais sont collectés à fin hello de validation de hello et de déploiement de hello. Si hello processus PowerShell est arrêté pendant l’exécution du script de hello, des journaux sont perdues.
   > 
   > 

## <a name="connect-toohello-head-node"></a>Se connecter toohello du nœud principal
Une fois que vous déployez un cluster HPC Pack hello dans Azure, [connexion Bureau à distance](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) à l’aide de machine virtuelle de nœud principal toohello hello des informations d’identification de domaine vous avez fourni lors du déploiement de cluster de hello (par exemple, *hpc\\ clusteradmin*). Vous gérez un cluster de hello à partir du nœud principal hello.

Sur le nœud principal de hello, démarrez état hello de HPC Cluster Manager toocheck de cluster HPC Pack de hello. Vous pouvez gérer et surveiller des nœuds de calcul Linux hello même façon que vous utilisez avec Windows nœuds de calcul. Par exemple, vous voyez les nœuds de Linux hello répertoriés dans **gestion des ressources** (ces nœuds sont déployés avec hello **LinuxNode** modèle).

![Gestion des nœuds][management]

Vous voyez également des nœuds Linux hello hello **thermique** vue.

![Carte thermique][heatmap]

## <a name="how-toomove-data-in-a-cluster-with-linux-nodes"></a>Comment toomove les données dans un cluster avec des nœuds Linux
Vous avez plusieurs données toomove de choix entre des nœuds Linux et le nœud principal de Windows hello du cluster de hello. Voici trois méthodes courantes, décrits plus en détail dans les sections suivantes de hello :

* **Fichier Azure** -expose une managé toostore données SMB fichier partage de fichiers dans le stockage Azure. Les nœuds de Windows et Linux peuvent monter un partage de fichiers Azure comme un lecteur ou dossier à hello même moment, même si elles sont déployées dans des réseaux virtuels différents.
* **Partager du nœud principal SMB** -monte un dossier partagé Windows standard de nœud principal de hello des nœuds Linux.
* **Head node NFS server** : fournit une solution de partage de fichiers pour un environnement mixte Windows et Linux.

### <a name="azure-file-storage"></a>Présentation du stockage de fichiers
Hello [fichier Azure](https://azure.microsoft.com/services/storage/files/) service expose les partages de fichiers à l’aide du protocole SMB 2.1 standard de hello. Machines virtuelles Azure et les services de cloud computing peuvent partager des données de fichier entre les composants d’application via des partages montés, et des applications locales peuvent accéder les données de fichier dans un partage via hello API de stockage de fichier. 

Pour obtenir des instructions détaillées toocreate un fichier Azure partager et montez-le sur le nœud principal de hello, consultez [prise en main avec un stockage de fichier Azure sur Windows](../../../storage/files/storage-how-to-use-files-windows.md). partage de fichiers Azure hello toomount des nœuds de Linux hello, consultez [comment toouse stockage Azure files avec Linux](../../../storage/files/storage-how-to-use-files-linux.md). tooset des connexions persistantes, consultez [Persisting connexions tooMicrosoft Azure Files](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx).

Dans l’exemple suivant de hello, créer un partage de fichiers Azure sur un compte de stockage. toomount hello partager sur hello du nœud principal, ouvrez une invite de commandes, puis entrez hello suivant de commandes :

```command
cmdkey /add:allvhdsje.file.core.windows.net /user:allvhdsje /pass:<storageaccountkey>

net use Z: \\allvhdje.file.core.windows.net\rdma /persistent:yes
```

Dans cet exemple, allvhdsje est le nom de votre compte de stockage, storageaccountkey est votre clé de compte de stockage et rdma est le nom de partage de fichiers Azure hello. partage de fichiers Azure Hello est monté en tant que Z: sur le nœud principal de hello.

partage de fichiers Azure hello toomount des nœuds Linux, exécutez un **clusrun** commande sur le nœud principal de hello. **[ClusRun](https://technet.microsoft.com/library/cc947685.aspx)**  est un toocarry d’outil HPC Pack utile des tâches d’administration sur plusieurs nœuds. (Voir aussi [Clusrun pour les nœuds Linux](#Clusrun-for-Linux-nodes) dans cet article.)

Ouvrez une fenêtre Windows PowerShell, puis entrez hello suivant de commandes :

```powershell
clusrun /nodegroup:LinuxNodes mkdir -p /rdma

clusrun /nodegroup:LinuxNodes mount -t cifs //allvhdsje.file.core.windows.net/rdma /rdma -o vers=2.1`,username=allvhdsje`,password=<storageaccountkey>'`,dir_mode=0777`,file_mode=0777
```

Hello première commande crée un dossier nommé /rdma sur tous les nœuds dans le groupe de LinuxNodes hello. commande deuxième Hello monte hello Azure fichier partage allvhdsjw.file.core.windows.net/rdma sur le dossier /rdma hello too777 de jeu de bits en mode dir et fichier. Dans la deuxième commande de hello, allvhdsje est le nom de votre compte de stockage et storageaccountkey est votre clé de compte de stockage.

> [!NOTE]
> Hello »\`« symbole dans la deuxième commande de hello est un symbole d’échappement pour PowerShell. «\`, « signifie que hello », » (virgule) est une partie de la commande hello.
> 
> 

### <a name="head-node-share"></a>Partage du nœud principal
Vous pouvez également monter un dossier partagé de nœud principal de hello des nœuds Linux. Fournit d’un partage de fichiers tooshare hello la plus simple, mais du nœud principal de hello et tous les nœuds de Linux doivent être déployés dans hello même réseau virtuel. Voici les étapes hello.

1. Créez un dossier sur le nœud principal de hello et tooEveryone le partager avec des autorisations en lecture/écriture. Par exemple, partager D:\OpenFOAM sur le nœud principal de hello en tant que \\CentOS7RDMA-HN\OpenFOAM. CentOS7RDMA-HN Voici hello les nom d’hôte de nœud principal de hello.
   
    ![Autorisations des partages de fichiers][fileshareperms]
   
    ![Partage de fichiers][filesharing]
2. Ouvrez une fenêtre Windows PowerShell et exécutez hello suivant de commandes :
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS7RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

Hello première commande crée un dossier nommé /openfoam sur tous les nœuds dans le groupe de LinuxNodes hello. commande deuxième Hello monte hello partagé dossier //CentOS7RDMA-HN/OpenFOAM sur le dossier hello avec too777 de jeu de bits en mode dir et fichier. Hello nom d’utilisateur et mot de passe dans la commande hello doivent être nom d’utilisateur hello et un mot de passe d’un utilisateur de cluster sur le nœud principal de hello. (Consultez la page [Add or Remove Cluster Users](https://technet.microsoft.com/library/ff919330.aspx)(Ajouter ou supprimer des utilisateurs du cluster).)

> [!NOTE]
> Hello »\`« symbole dans la deuxième commande de hello est un symbole d’échappement pour PowerShell. «\`, « signifie que hello », » (virgule) est une partie de la commande hello.
> 
> 

### <a name="nfs-server"></a>Serveur NFS
Hello service NFS vous permet de tooshare et migrer des fichiers entre les ordinateurs exécutant le système d’exploitation de hello Windows Server 2012 à l’aide du protocole SMB de hello et basés sur Linux à l’aide du protocole NFS de hello. Hello du serveur NFS et tous les autres nœuds ont toobe déployé Bonjour même réseau virtuel. Il offre une meilleure compatibilité avec les nœuds Linux en comparaison d’un partage SMB. Par exemple, il prend en charge les liaisons de fichiers.

1. tooinstall et configurer un serveur NFS, suivez les étapes de hello dans [serveur pour le partage premier du système de fichiers réseau de bout en bout](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx).
   
    Par exemple, créez un partage NFS nommé nfs avec hello propriétés suivantes :
   
    ![Autorisation NFS][nfsauth]
   
    ![Autorisations des partages NFS][nfsshare]
   
    ![Autorisations NTFS NFS][nfsperm]
   
    ![Propriétés de la gestion NFS][nfsmanage]
2. Ouvrez une fenêtre Windows PowerShell et exécutez hello suivant de commandes :
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /nfsshare
   
    clusrun /nodegroup:LinuxNodes mount CentOS7RDMA-HN:/nfs /nfsshared
    ```
   
   Hello première commande crée un dossier nommé /nfsshared sur tous les nœuds dans le groupe de LinuxNodes hello. deuxième commande hello de montage NFS Hello partager HN-CentOS7RDMA : / nfs sur hello dossier. Ici HN-CentOS7RDMA : / nfs hello un chemin d’accès à distance de votre partage NFS.

## <a name="how-toosubmit-jobs"></a>Comment les travaux toosubmit
Il existe des clusters de HPC Pack toohello plusieurs façons toosubmit travaux :

* Gestionnaire de cluster HPC ou interface graphique utilisateur du Gestionnaire de travaux HPC
* Portail web HPC
* API REST

Soumission de travaux de cluster toohello dans Azure via le portail web HPC hello et les outils de l’interface utilisateur graphique de HPC Pack sont hello même que pour les nœuds de calcul Windows. Consultez [Gestionnaire de travaux HPC Pack](https://technet.microsoft.com/library/ff919691.aspx) et [comment toosubmit travaux à partir d’un ordinateur de client local](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

travaux toosubmit via hello API REST, consultez trop[création et envoi de travaux à l’aide de l’API REST Microsoft HPC Pack hello](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx). travaux toosubmit à partir d’un client Linux, également faire référence exemple de Python toohello Bonjour [HPC Pack SDK](https://www.microsoft.com/download/details.aspx?id=47756).

## <a name="clusrun-for-linux-nodes"></a>Clusrun pour les nœuds Linux
Hello HPC Pack [clusrun](https://technet.microsoft.com/library/cc947685.aspx) outil peut être utilisé tooexecute les commandes des nœuds Linux via une invite de commandes ou d’un gestionnaire de Cluster HPC. Voici quelques exemples de base.

* Afficher les noms d’utilisateur en cours sur tous les nœuds de cluster de hello.
  
    ```command
    clusrun whoami
    ```
* Installer hello **gdb** outil de débogage avec **yum** sur tous les nœuds hello linuxnodes groupe et redémarrez les nœuds hello après 10 minutes.
  
    ```command
    clusrun /nodegroup:linuxnodes yum install gdb –y; shutdown –r 10
    ```
* Créer un script shell afficher chaque nombre entre 1 et 10 pour une seconde sur chaque nœud de Linux dans le cluster de hello, exécuter et afficher la sortie à partir des nœuds de hello immédiatement.
  
    ```command
    clusrun /interleaved /nodegroup:linuxnodes echo \"for i in {1..10}; do echo \\\"\$i\\\"; sleep 1; done\" ^> script.sh; chmod +x script.sh; ./script.sh
    ```

> [!NOTE]
> Vous devrez peut-être toouse certains caractères d’échappement dans **clusrun** commandes. Comme illustré dans cet exemple, utilisez ^ un Bonjour de tooescape d’invite de commandes » > « symbole.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
* Essayez la montée en puissance hello cluster tooa plus grand nombre de nœuds, ou une charge de travail Linux en cours d’exécution sur le cluster de hello. Pour trouver un exemple, consultez [Exécuter NAMD avec Microsoft HPC Pack sur des nœuds de calcul Linux dans Azure](hpcpack-cluster-namd.md).
* Essayez d’un cluster avec [prenant en charge RDMA, nécessitant de machines virtuelles](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toorun les charges de travail MPI. Pour trouver un exemple, consultez [Exécuter OpenFOAM avec Microsoft HPC Pack sur un cluster Linux RDMA dans Azure](hpcpack-cluster-openfoam.md).
* Si vous êtes intéressé par utilisation des nœuds Linux dans un cluster de HPC Pack sur site, consultez hello [conseils TechNet](https://technet.microsoft.com/library/mt595803.aspx).

<!--Image references-->
[scenario]:media/hpcpack-cluster/scenario.png
[portal]:media/hpcpack-cluster/portal.png
[validate]:media/hpcpack-cluster/validate.png
[resources]:media/hpcpack-cluster/resources.png
[deploy]:media/hpcpack-cluster/deploy.png
[management]:media/hpcpack-cluster/management.png
[heatmap]:media/hpcpack-cluster/heatmap.png
[fileshareperms]:media/hpcpack-cluster/fileshare1.png
[filesharing]:media/hpcpack-cluster/fileshare2.png
[nfsauth]:media/hpcpack-cluster/nfsauth.png
[nfsshare]:media/hpcpack-cluster/nfsshare.png
[nfsperm]:media/hpcpack-cluster/nfsperm.png
[nfsmanage]:media/hpcpack-cluster/nfsmanage.png
