---
title: aaaRun OpenFOAM avec HPC Pack sur les machines virtuelles Linux | Documents Microsoft
description: "Déployer un cluster Microsoft HPC Pack sur Azure et exécuter un travail OpenFOAM sur plusieurs nœuds de calcul RDMA."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: c0bb1637-bb19-48f1-adaa-491808d3441f
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 07/22/2016
ms.author: danlep
ms.openlocfilehash: 1a51ffe6804abb5156f01d580c9b7a4a9649377a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-openfoam-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a>Exécuter OpenFoam avec Microsoft HPC Pack sur un cluster Linux RDMA dans Azure
Cet article vous montre une façon toorun OpenFoam dans des machines virtuelles. Ici, vous déployez un cluster Microsoft HPC Pack avec des nœuds de calcul Linux sur Azure, et exécutez une tâche [OpenFoam](http://openfoam.com/) avec Intel MPI. Vous pouvez utiliser des machines virtuelles de Azure prend en charge RDMA pour les nœuds de calcul hello, afin que les nœuds de calcul hello communiquent sur le réseau RDMA Azure de hello. Autres toorun options OpenFoam dans Azure sont entièrement configuré commerciales images disponibles dans hello Marketplace, tels que de UberCloud [2.3 OpenFoam CentOS 6](https://azure.microsoft.com/marketplace/partners/ubercloud/openfoam-v2dot3-centos-v6/)et en exécutant sur [Azure Batch](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/). 

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

OpenFOAM (acronyme d’Open Field Operation and Manipulation) est un logiciel open source de calcul de mécanique des fluides numérique largement utilisé en ingénierie et en sciences, tant au sein d’organisations commerciales que d’instituts universitaires. Il comprend des outils de maillage, notamment snappyHexMesh, un meilleur parallélisé pour les géométries de CAO complexes et de pré et post-traitement. Presque tous les processus s’exécutent en parallèle, l’activation des utilisateurs tootake pleinement parti du matériel informatique à leur disposition.  

Microsoft HPC Pack fournit des fonctionnalités toorun HPC à grande échelle et des applications parallèles, y compris des applications MPI sur des clusters de machines virtuelles Microsoft Azure. HPC Pack prend également en charge l’exécution d’applications Linux HPC sur les machines virtuelles de nœuds de calcul Linux déployées dans un cluster HPC Pack. Consultez [prise en main des nœuds de calcul Linux dans un cluster HPC Pack dans Azure](hpcpack-cluster.md) pour une présentation toousing Linux de calcul des nœuds avec HPC Pack.

> [!NOTE]
> Cet article explique comment toorun une charge de travail Linux MPI avec HPC Pack. Il suppose que vous êtes familiarisé avec l’administration du système Linux et l’exécution de charges de travail MPI sur des clusters Linux. Si vous utilisez des versions de MPI et OpenFOAM différent de ceux indiqués dans cet article de hello, vous pouvez avoir toomodify certaines étapes d’installation et de configuration. 
> 
> 

## <a name="prerequisites"></a>Composants requis
* **Cluster HPC Pack avec nœuds de calcul Linux prenant en charge RDMA** : déployez un cluster HPC Pack avec des nœuds de calcul Linux de taille A8, A9, H16r ou H16rm à l’aide d’un [modèle Azure Resource Manager](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) ou d’un [script Azure PowerShell](hpcpack-cluster-powershell-script.md). Consultez [prise en main des nœuds de calcul Linux dans un cluster HPC Pack dans Azure](hpcpack-cluster.md) pour les conditions préalables de hello et étapes dans les deux cas. Si vous choisissez hello option de déploiement de script PowerShell, consultez le fichier de configuration d’exemple hello dans les fichiers d’exemple hello à fin hello de cet article. Utilisez ce cluster de HPC Pack configuration toodeploy basé sur un Azure consistant en un nœud principal de taille A8 Windows Server 2012 R2 et les nœuds de calcul de taille de 2 A8 SUSE Linux Enterprise Server 12. Remplacez les valeurs appropriées pour les noms de vos abonnement et service. 
  
  **Autres informations tooknow**
  
  * Pour connaître les conditions préalables à la mise en réseau RDMA Linux dans Azure, consultez [Tailles de machines virtuelles de calcul haute performance](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
  * Si vous utilisez hello option de déploiement de script Powershell, déployer tous les nœuds de calcul Linux hello au sein de la connexion de réseau d’un cloud service toouse hello RDMA.
  * Après le déploiement de nœuds de Linux hello, connectez-vous à SSH tooperform les tâches d’administration supplémentaires. Trouver les détails de la connexion SSH hello pour chaque VM Linux Bonjour portail Azure.  
* **Intel MPI** -toorun OpenFOAM SLES 12 HPC sur les nœuds de calcul dans Azure, vous devez tooinstall hello Intel MPI bibliothèque 5 runtime hello [Intel.com site](https://software.intel.com/en-us/intel-mpi-library/). (Intel MPI 5 est préinstallé sur des images HPC basées sur CentOS.)  Si nécessaire, vous devez ensuite installer Intel MPI sur vos nœuds de calcul Linux. tooprepare pour cette étape, après avoir inscrit avec Intel, procédez comme lien hello hello confirmation par courrier électronique toohello connexes des pages web. Ensuite, hello de copie télécharger le lien pour la version appropriée de hello d’Intel sur le fichier .tgz hello. Cet article est basé sur Intel MPI version 5.0.3.048.
* **Pack de Source OpenFOAM** -télécharger le logiciel de OpenFOAM Source Pack hello pour Linux à partir de hello [site OpenFOAM Foundation](http://openfoam.org/download/2-3-1-source/). Cet article est basé sur la version du Pack Source 2.3.1, disponible en téléchargement en tant que OpenFOAM 2.3.1.tgz. Suivez les instructions de hello plus loin dans cet article de toounpack et OpenFOAM se compiler sur les nœuds de calcul Linux hello.
* **EnSight** (facultatif) : résultats de hello toosee de votre simulation OpenFOAM, télécharger et installer hello [EnSight](https://www.ceisoftware.com/download/) programme de visualisation et d’analyse. Informations de licence et de téléchargement sont sur le site de EnSight hello.

## <a name="set-up-mutual-trust-between-compute-nodes"></a>Configuration de l’approbation mutuelle entre les nœuds de calcul
L’exécution d’une tâche entre nœuds sur plusieurs nœuds Linux requiert hello nœuds tootrust eux (par **rsh** ou **ssh**). Lorsque vous créez un cluster HPC Pack de hello avec hello script de déploiement Microsoft HPC Pack IaaS, script de hello configure automatiquement permanente confiance mutuelle pour le compte administrateur hello que vous spécifiez. Pour les utilisateurs non-administrateurs que vous créez dans le domaine de ce cluster hello, vous avez tooset temporaire approbation mutuelle entre les nœuds de hello quand un travail est alloué toothem et détruire la relation de hello après que hello tâche est terminée. approbation tooestablish pour chaque utilisateur, fournissez un cluster de toohello de paire de clés RSA HPC Pack utilise pour la relation d’approbation hello.

### <a name="generate-an-rsa-key-pair"></a>Génération d’une paire de clés RSA
Il est facile toogenerate une paire de clés RSA, qui contient une clé publique et une clé privée, en exécutant hello Linux **ssh-keygen** commande.

1. Ouvrez une session tooa ordinateur Linux.
2. Exécutez hello de commande suivante :
   
   ```
   ssh-keygen -t rsa
   ```
   
   > [!NOTE]
   > Appuyez sur **entrée** toouse hello paramètres jusqu'à ce que la commande hello est terminée. N'entrez pas de phrase secrète ici ; à l'invite de mot de passe, appuyez simplement sur **Entrée**.
   > 
   > 
   
   ![Génération d’une paire de clés RSA][keygen]
3. Modification toohello ~/.ssh répertoire. clé privée de Hello est stockée dans la clé publique id_rsa et hello dans id_rsa.pub.
   
   ![Clés publiques et privées][keys]

### <a name="add-hello-key-pair-toohello-hpc-pack-cluster"></a>Ajouter un cluster de HPC Pack toohello hello paire de clés
1. Rendre un nœud de tête du tooyour de connexion Bureau à distance avec votre compte d’administrateur de HPC Pack (compte d’administrateur hello configuré lors de l’exécution du script de déploiement hello).
2. Utilisez toocreate de procédures standard Windows Server un compte d’utilisateur de domaine dans le domaine d’Active Directory du cluster hello. Par exemple, utiliser hello utilisateur Active Directory et outil d’ordinateurs sur le nœud principal de hello. les exemples de Hello dans cet article supposent que vous créez un utilisateur de domaine nommé hpclab\hpcuser.
3. Créez un fichier nommé C:\cred.xml et copier hello RSA clé des données dans celui-ci. Un exemple de fichier cred.xml est à la fin de hello de cet article.
   
   ```
   <ExtendedData>
     <PrivateKey>Copy hello contents of private key here</PrivateKey>
     <PublicKey>Copy hello contents of public key here</PublicKey>
   </ExtendedData>
   ```
4. Ouvrez une invite de commandes et entrez hello tooset hello données hello hpclab\hpcuser compte les informations d’identification de commande suivante. Vous utilisez hello **extendeddata** toopass de paramètre hello nom de fichier C:\cred.xml que vous avez créé pour les données de clé hello.
   
   ```
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   Cette commande se termine correctement sans sortie. Après avoir défini les informations d’identification hello pour les comptes d’utilisateur hello que vous devez toorun travaux, stockez le fichier de cred.xml de hello dans un emplacement sécurisé ou supprimez-le.
5. Si vous avez généré hello paire de clés RSA sur l’un de vos nœuds de Linux, n’oubliez pas les clés hello toodelete après avoir terminé leur utilisation. HPC Pack recherche un fichier id_rsa ou id_rsa.pub existant. Il ne configure pas d’approbation mutuelle.

> [!IMPORTANT]
> Nous ne recommandons l’exécution d’un travail de Linux en tant qu’un administrateur de cluster sur un cluster partagé, car une tâche envoyée par un administrateur s’exécute sous un compte de racine hello des nœuds de Linux hello. Toutefois, une tâche envoyée par un utilisateur non administrateur s’exécute sous un compte d’utilisateur local Linux avec hello même nom en tant qu’utilisateur de tâche hello. Dans ce cas, HPC Pack définit confiance mutuelle pour cet utilisateur Linux sur les nœuds hello allouées toohello travail. Vous pouvez configurer des utilisateurs de Linux hello manuellement sur les nœuds de Linux hello avant d’exécuter le travail de hello ou HPC Pack crée automatiquement les utilisateur hello lorsque le travail de hello est envoyé. Si HPC Pack crée un utilisateur de hello, HPC Pack supprime une fois hello travail terminé. menaces de sécurité tooreduce, HPC Pack supprime les clés de hello après l’achèvement du travail.
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a>Configuration d’un partage de fichiers pour les nœuds Linux
Maintenant configurer un partage SMB standard sur un dossier sur le nœud principal de hello. tooallow hello Linux nœuds tooaccess fichiers d’application avec un chemin d’accès commun, montage hello dossier partagé sur les nœuds de Linux hello. Si vous le souhaitez, vous pouvez utiliser une autre option de partage de fichier telle que le partage de fichiers Azure (recommandé dans de nombreux scénarios) ou un partage NFS. Consultez le fichier hello partager des informations et des instructions détaillées dans [prise en main des nœuds de calcul Linux dans un Cluster HPC Pack dans Azure](hpcpack-cluster.md).

1. Créez un dossier sur le nœud principal de hello et partagez-le tooEveryone en définissant des privilèges de lecture/écriture. Par exemple, partager C:\OpenFOAM sur le nœud principal de hello en tant que \\ \\SUSE12RDMA-HN\OpenFOAM. Ici, *SUSE12RDMA-HN* est le nom d’hôte hello de nœud principal de hello.
2. Ouvrez une fenêtre Windows PowerShell et exécutez hello suivant de commandes :
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
   clusrun /nodegroup:LinuxNodes mount -t cifs //SUSE12RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
   ```

Hello première commande crée un dossier nommé /openfoam sur tous les nœuds dans le groupe de LinuxNodes hello. commande deuxième Hello monte hello partagé dossier //SUSE12RDMA-HN/OpenFOAM des nœuds de Linux hello avec dir_mode et file_mode too777 d’ensemble de bits. Hello *nom d’utilisateur* et *mot de passe* Bonjour commande doit-elle être des informations d’identification de hello d’un utilisateur sur le nœud principal de hello.

> [!NOTE]
> Hello »\`« symbole dans la deuxième commande de hello est un symbole d’échappement pour PowerShell. «\`, « signifie hello », » (virgule) est une partie de la commande hello.
> 
> 

## <a name="install-mpi-and-openfoam"></a>Installer MPI et OpenFOAM
toorun OpenFOAM comme un travail MPI sur le réseau de hello RDMA, vous devez toocompile OpenFOAM avec les bibliothèques Intel MPI hello. 

Tout d’abord, exécuter plusieurs **clusrun** des commandes telles que les bibliothèques Intel MPI tooinstall (le cas échéant) et OpenFOAM sur vos nœuds Linux. Partage de nœud principal Utilisez hello configuré précédemment fichiers d’installation hello tooshare entre les nœuds de Linux hello.

> [!IMPORTANT]
> Ces étapes d’installation et de compilation sont des exemples. Vous devez avoir quelques connaissances de Linux système administration tooensure que les bibliothèques et les compilateurs dépendants sont installés correctement. Vous devrez peut-être toomodify certaines variables d’environnement ou d’autres paramètres pour les versions de Intel MPI et OpenFOAM. Pour plus de détails, voir [Guide d’installation de la bibliothèque Intel MPI pour Linux](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html) et [Installation du pack source d’OpenFOAM](http://openfoam.org/download/2-3-1-source/) pour votre environnement.
> 
> 

### <a name="install-intel-mpi"></a>Installer Intel MPI
Enregistrer package d’installation téléchargé hello pour Intel MPI (l_mpi_p_5.0.3.048.tgz dans cet exemple) dans C:\OpenFoam sur le nœud principal de hello afin que les nœuds de Linux hello peuvent accéder à ce fichier à partir de /openfoam. Puis exécutez **clusrun** bibliothèque d’Intel MPI tooinstall sur tous les nœuds de Linux hello.

1. Voici de Hello commandes package d’installation copie hello, extrayez-le trop/opt/intel sur chaque nœud.
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/intel
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/l_mpi_p_5.0.3.048.tgz /opt/intel/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/intel/l_mpi_p_5.0.3.048.tgz -C /opt/intel/
   ```
2. tooinstall Intel MPI bibliothèque utilisez en mode silencieux, un fichier silent.cfg. Vous trouverez un exemple Bonjour exemples de fichiers à la fin de hello de cet article. Place ce fichier dans hello partagé /openfoam du dossier. Pour plus d’informations sur le fichier de silent.cfg hello, consultez [Intel MPI Library for Linux Installation Guide - Installation sans assistance](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall).
   
   > [!TIP]
   > Assurez-vous que vous enregistrez votre fichier .cfg silencieux en tant que fichier texte avec des fins de ligne Linux (LF uniquement, et non CR LF). Cette étape permet de s’assurer qu’elle s’exécute correctement sur les nœuds de Linux hello.
   > 
   > 
3. Installez la bibliothèque MPI Intel en mode silencieux.
   
   ```
   clusrun /nodegroup:LinuxNodes bash /opt/intel/l_mpi_p_5.0.3.048/install.sh --silent /openfoam/silent.cfg
   ```

### <a name="configure-mpi"></a>Configuration de MPI
Pour le test, vous devez ajouter hello suivant des lignes toohello /etc/security/limits.conf sur chacun des nœuds de Linux hello :

    clusrun /nodegroup:LinuxNodes echo "*               hard    memlock         unlimited" `>`> /etc/security/limits.conf
    clusrun /nodegroup:LinuxNodes echo "*               soft    memlock         unlimited" `>`> /etc/security/limits.conf


Redémarrez les nœuds de Linux hello une fois que vous mettez à jour le fichier de limits.conf hello. Par exemple, utilisez hello qui suit **clusrun** commande :

```
clusrun /nodegroup:LinuxNodes systemctl reboot
```

Après avoir redémarré, vérifiez que ce dossier partagé hello est monté en tant que /openfoam.

### <a name="compile-and-install-openfoam"></a>Compiler et installer OpenFOAM
Enregistrez le package d’installation téléchargé hello pour hello tooC:\OpenFoam de OpenFOAM Source Pack (OpenFOAM 2.3.1.tgz dans cet exemple) sur le nœud principal de hello afin que les nœuds de Linux hello peuvent accéder à ce fichier à partir de /openfoam. Puis exécutez **clusrun** commandes toocompile OpenFOAM sur tous les hello des nœuds Linux.

1. Créer un dossier /opt/OpenFOAM sur chaque nœud de Linux, copier hello source package toothis le dossier et il l’extraire.
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/OpenFOAM
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/OpenFOAM-2.3.1.tgz /opt/OpenFOAM/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/OpenFOAM/OpenFOAM-2.3.1.tgz -C /opt/OpenFOAM/
   ```
2. toocompile OpenFOAM avec hello Intel MPI bibliothèque, définissez tout d’abord certaines variables d’environnement pour Intel MPI et OpenFOAM. Utiliser un script d’interpréteur de commandes appelé settings.sh tooset hello variables. Vous trouverez un exemple Bonjour exemples de fichiers à la fin de hello de cet article. Place ce fichier (à des fins de ligne Linux) Bonjour partagé /openfoam du dossier. Ce fichier contient également des paramètres pour hello MPI OpenFOAM composants d’exécution et que vous utilisez ultérieure toorun un travail OpenFOAM.
3. Installer des packages dépendants nécessités toocompile OpenFOAM. En fonction de votre distribution Linux, vous devrez tout d’abord tooadd un référentiel. Exécutez **clusrun** commandes similaires toohello suivantes :
   
    ```
    clusrun /nodegroup:LinuxNodes zypper ar http://download.opensuse.org/distribution/13.2/repo/oss/suse/ opensuse
   
    clusrun /nodegroup:LinuxNodes zypper -n --gpg-auto-import-keys install --repo opensuse --force-resolution -t pattern devel_C_C++
    ```
   
    Si nécessaire, hello toorun SSH tooeach Linux nœud commandes tooconfirm qu’ils s’exécutent correctement.
4. Exécutez hello suivant commande toocompile OpenFOAM. processus de compilation Hello prend quelques toocomplete de temps et génère une grande quantité de sortie toostandard informations du journal, par conséquent, utilisez hello **/ entrelacées** option de sortie de hello toodisplay entrelacée.
   
   ```
   clusrun /nodegroup:LinuxNodes /interleaved source /openfoam/settings.sh `&`& /opt/OpenFOAM/OpenFOAM-2.3.1/Allwmake
   ```
   
   > [!NOTE]
   > Hello »\`« symbole dans la commande hello est un symbole d’échappement pour PowerShell. «\`& » signifie hello « & » fait partie de la commande hello.
   > 
   > 

## <a name="prepare-toorun-an-openfoam-job"></a>Préparer toorun une tâche de OpenFOAM
Maintenant get prêt toorun un travail MPI appelée sloshingTank3D, qui est un des exemples de OpenFoam hello, sur les deux nœuds Linux. 

### <a name="set-up-hello-runtime-environment"></a>Configurer l’environnement d’exécution hello
tooset des environnements d’exécution hello pour MPI et OpenFOAM des nœuds de Linux hello, exécutez hello suivant de commande dans une fenêtre Windows PowerShell sur le nœud principal de hello. (Cette commande est valide pour SUSE Linux uniquement.)

```
clusrun /nodegroup:LinuxNodes cp /openfoam/settings.sh /etc/profile.d/
```

### <a name="prepare-sample-data"></a>Préparer l’exemple de données
Partage de nœud principal Utilisez hello configurées précédemment tooshare des fichiers entre les nœuds de Linux hello (montés en tant que /openfoam).

1. Nœuds de calcul tooone SSH de votre Linux.
2. Exécutez hello suivant tooset de commande d’environnement d’exécution hello OpenFOAM si vous n’avez pas déjà fait.
   
   ```
   $ source /openfoam/settings.sh
   ```
3. Copier le dossier partagé du toohello exemple sloshingTank3D hello et accédez tooit.
   
   ```
   $ cp -r $FOAM_TUTORIALS/multiphase/interDyMFoam/ras/sloshingTank3D /openfoam/
   
   $ cd /openfoam/sloshingTank3D
   ```
4. Lorsque vous utilisez les paramètres par défaut de hello de cet exemple, il peut prendre des dizaines de minutes toorun, vous pouvez donc toomodify certains toomake paramètres il s’exécuter plus rapidement. Un choix simple est toomodify hello temps étape variables deltaT et writeInterval dans le fichier du système/controlDict hello. Ce fichier stocke toutes les données d’entrée relatives contrôle toohello de temps et de la lecture et l’écriture des données de la solution. Par exemple, vous pouvez modifier la valeur hello deltaT de 0,05 too0.5 et valeur hello writeInterval de 0,05 too0.5.
   
   ![Modifier les variables d’étape][step_variables]
5. Spécifiez les valeurs souhaitées pour les variables de hello dans le fichier du système/decomposeParDict hello. Cet exemple utilise deux nœuds Linux chaque avec 8 cœurs, définissez donc numberOfSubdomains too16 et n de hierarchicalCoeffs too(1 1 16), ce qui signifie qu’exécuter OpenFOAM en parallèle avec les 16 processus. Pour plus d’informations, consultez [Guide de l’utilisateur OpenFOAM : 3.4 Exécution d’applications en parallèle](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4).
   
   ![Décomposer les processus][decompose]
6. Exécutez hello suivant les commandes à partir de hello sloshingTank3D Active tooprepare hello exemples de données.
   
   ```
   $ . $WM_PROJECT_DIR/bin/tools/RunFunctions
   
   $ m4 constant/polyMesh/blockMeshDict.m4 > constant/polyMesh/blockMeshDict
   
   $ runApplication blockMesh
   
   $ cp 0/alpha.water.org 0/alpha.water
   
   $ runApplication setFields  
   ```
7. Sur le nœud principal de hello, vous devez voir des fichiers de données exemple hello sont copiés dans C:\OpenFoam\sloshingTank3D. (C:\OpenFoam est dossier partagé de hello sur le nœud principal de hello).
   
   ![Fichiers de données sur le nœud principal de hello][data_files]

### <a name="host-file-for-mpirun"></a>Fichier hôte pour mpirun
Dans cette étape, vous créez un fichier d’hôte (il s’agit d’une liste de nœuds de calcul) qui hello **mpirun** commande utilise.

1. Sur l’un des nœuds de Linux hello, créez un fichier nommé fichier hôte sous /openfoam, donc ce fichier peut être atteint à /openfoam/hostfile sur tous les nœuds Linux.
2. Écrivez vos noms de nœud Linux dans ce fichier. Dans cet exemple, les fichiers hello contient hello nom :
   
   ```       
   SUSE12RDMA-LN1
   SUSE12RDMA-LN2
   ```
   
   > [!TIP]
   > Vous pouvez également créer ce fichier à C:\OpenFoam\hostfile sur le nœud principal de hello. Si vous optez pour cette solution, enregistrez le fichier au format texte avec des fins de lignes Linux (LF uniquement, pas CR LF). Cela garantit qu’elle s’exécute correctement sur les nœuds de Linux hello.
   > 
   > 
   
   **Wrapper de script d’interpréteur de commandes**
   
   Si vous disposez de nombreux nœuds Linux et vous souhaitez que votre toorun de travail uniquement sur certaines d'entre elles, il n’est pas un toouse conseillé de fichiers, un hôte fixe, car vous ne connaissez pas les nœuds qui seront allouées tooyour travail. Dans ce cas, écrire un wrapper un interpréteur de commandes de script pour **mpirun** toocreate hello automatiquement les fichiers de l’ordinateur hôte. Vous pouvez trouver un wrapper de script exemple un interpréteur de commandes appelé hpcimpirun.sh à fin hello de cet article et l’enregistrer en tant que /openfoam/hpcimpirun.sh. Cet exemple de script hello suivant :
   
   1. Définit les variables d’environnement hello pour **mpirun**et certains travail MPI addition commande paramètres toorun hello via réseau RDMA de hello. Dans ce cas, il définit hello suivant variables :
      
      * I_MPI_FABRICS=shm:dapl
      * I_MPI_DAPL_PROVIDER=ofa-v2-ib0
      * I_MPI_DYNAMIC_CONNECTION=0
   2. Crée un fichier d’hôte en fonction de toohello $ variable d’environnement CCP_NODES_CORES, qui est définie par le nœud principal HPC de hello lors de la tâche de hello est activé.
      
      format Hello $CCP_NODES_CORES suit ce modèle :
      
      ```
      <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
      ```
      
      où
      
      * `<Number of nodes>`-nombre de hello de nœuds allouée toothis travail.  
      * `<Name of node_n_...>`-nom hello de chaque nœud allouée toothis travail.
      * `<Cores of node_n_...>`-hello du nombre de cœurs sur le travail de hello nœud toothis alloué.
      
      Par exemple, si le travail de hello a besoin de deux nœuds toorun, $CCP_NODES_CORES est similaire à
      
      ```
      2 SUSE12RDMA-LN1 8 SUSE12RDMA-LN2 8
      ```
   3. Hello d’appels **mpirun** commande et ajoute la ligne de commande de deux paramètres toohello.
      
      * `--hostfile <hostfilepath>: <hostfilepath>`-chemin d’accès de hello du script de hello du fichier hôte hello crée
      * `-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}`-une variable d’environnement définie par hello nœud principal HPC Pack, qui stocke le nombre de hello de cœurs total alloué toothis travail. Dans ce cas, il spécifie le nombre de hello de processus pour **mpirun**.

## <a name="submit-an-openfoam-job"></a>Envoi d’un travail OpenFOAM
Maintenant, vous pouvez envoyer un travail dans HPC Cluster Manager. Vous devez toopass hello script hpcimpirun.sh dans les lignes de commande hello pour certaines des tâches hello.

1. Se connecter tooyour nœud principal du cluster et démarrez le Gestionnaire du Cluster HPC.
2. **Dans la gestion des ressources**, assurez-vous que les nœuds de calcul Linux hello sont Bonjour **Online** état. Si ce n’est pas le cas, sélectionnez-les et cliquez sur **Mettre en ligne**.
3. Dans **Gestion des tâches**, cliquez sur **Nouveau travail**.
4. Entrez un nom pour le travail, par exemple *sloshingTank3D*.
   
   ![Détails du travail][job_details]
5. Dans **ressources de projet**, choisissez de type hello de ressource en tant que « Nœud » et définir hello Minimum too2. Cette configuration s’exécute le travail de hello sur deux nœuds de Linux, chacun d’eux a huit cœurs dans cet exemple.
   
   ![ressources de la tâche][job_resources]
6. Cliquez sur **modifier des tâches** dans hello du volet de navigation gauche, puis cliquez sur **ajouter** tooadd un travail de toohello de tâches. Ajouter quatre travail toohello de tâches avec hello suivant des lignes de commande et les paramètres.
   
   > [!NOTE]
   > En cours d’exécution `source /openfoam/settings.sh` configure hello OpenFOAM et MPI environnements d’exécution, si bien que chacun des hello tâches suivantes l’appelle avant hello OpenFOAM commande.
   > 
   > 
   
   * **Tâche 1**. Exécutez **decomposePar** toogenerate des fichiers de données pour exécuter **interDyMFoam** en parallèle.
     
     * Affecter une tâche toohello de nœud
     * **Ligne de commande** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`
     * **Répertoire de travail** - /openfoam/sloshingTank3D
     
     Consultez hello figure suivante. Vous configurez les tâches restantes hello de la même façon.
     
     ![Détails de la tâche 1][task_details1]
   * **Tâche 2**. Exécutez **interDyMFoam** dans toocompute parallèle hello exemple.
     
     * Affecter des tâches de toohello deux nœuds
     * **Ligne de commande** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`
     * **Répertoire de travail** - /openfoam/sloshingTank3D
   * **Tâche 3**. Exécutez **reconstructPar** toomerge hello définit des répertoires de temps à partir de chaque répertoire processor_N_ en un seul ensemble.
     
     * Affecter une tâche toohello de nœud
     * **Ligne de commande** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`
     * **Répertoire de travail** - /openfoam/sloshingTank3D
   * **Tâche 4**. Exécutez **foamToEnsight** dans tooconvert parallèle fichiers de résultats OpenFOAM hello dans EnSight mettre en forme et hello EnSight fichiers dans un répertoire nommé Ensight dans le répertoire de cas hello.
     
     * Affecter des tâches de toohello deux nœuds
     * **Ligne de commande** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`
     * **Répertoire de travail** - /openfoam/sloshingTank3D
7. Ajouter des tâches de toothese de dépendances dans l’ordre croissant de l’ordre des tâches.
   
   ![Dépendances de la tâche][task_dependencies]
8. Cliquez sur **Submit** toorun ce travail.
   
   Par défaut, HPC Pack soumet le travail hello que votre compte d’utilisateur connecté actuel. Après avoir cliqué sur **envoyer**, vous pouvez voir une boîte de dialogue vous invitant à nom d’utilisateur tooenter hello et le mot de passe.
   
   ![Informations d’identification de la tâche][creds]
   
   Sous certaines conditions, HPC Pack mémorise les informations d’utilisateur hello d’entrée avant et de ne plus afficher cette boîte de dialogue. toomake HPC Pack afficher à nouveau, entrez hello commande à l’invite de commande suivante et l’envoi de la tâche de hello puis.
   
   ```
   hpccred delcreds
   ```
9. travail de Hello prend de dizaines de minutes tooseveral heures en fonction des paramètres toohello que vous avez défini pour l’exemple hello. Dans la carte thermique hello, vous voyez travail hello en cours d’exécution sur les nœuds de Linux hello. 
   
   ![Carte thermique][heat_map]
   
   Sur chaque nœud, huit processus sont démarrés.
   
   ![Processus Linux][linux_processes]
10. Lors de la fin du travail de hello, trouver les résultats de la tâche hello dans les dossiers C:\OpenFoam\sloshingTank3D et des fichiers journaux hello C:\OpenFoam.

## <a name="view-results-in-ensight"></a>Afficher les résultats dans EnSight
Vous pouvez également utiliser [EnSight](https://www.ceisoftware.com/) toovisualize et analyser les résultats hello du travail de OpenFOAM hello. Pour plus d’informations sur la visualisation et l’animation dans EnSight, consultez le [guide vidéo](http://www.ceisoftware.com/wp-content/uploads/screencasts/vof_visualization/vof_visualization.html).

1. Après avoir installé EnSight sur le nœud principal de hello, démarrez-le.
2. Ouvrez C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case.
   
   Vous voyez un réservoir dans l’Observateur hello.
   
   ![Réservoir dans EnSight][tank]
3. Créer un **Isosurface** de **internalMesh**, puis choisissez la variable de hello **alpha_water**.
   
   ![Créer une isosurface][isosurface]
4. Définir la couleur de hello pour **Isosurface_part** créé à l’étape précédente de hello. Par exemple, définissez-le toowater bleu.
   
   ![Modifier la couleur de l’isosurface][isosurface_color]
5. Créer un **Iso-volume** de **murs** en sélectionnant **murs** Bonjour **parties** volet et cliquez sur hello **Isosurfaces**  bouton dans la barre d’outils hello.
6. Dans la boîte de dialogue hello, sélectionnez **Type** en tant que **Isovolume** et définissez hello Min. de **Isovolume plage** too0.5. toocreate hello isovolume, cliquez sur **créer avec les parties sélectionnées**.
7. Définir la couleur de hello pour **Iso_volume_part** créé à l’étape précédente de hello. Par exemple, définissez-le toodeep eau bleu.
8. Définir la couleur de hello pour **murs**. Par exemple, définissez-le tootransparent blanc.
9. Maintenant, cliquez sur **lire** toosee les résultats de hello de simulation de hello.
   
    ![Résultat du réservoir][tank_result]

## <a name="sample-files"></a>Exemple de fichiers
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a>Exemple de fichier de configuration XML pour le déploiement de clusters par script PowerShell
 ```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>allvhdsje</StorageAccount>
  </Subscription>
  <Location>Japan East</Location>  
  <VNet>
    <VNetName>suse12rdmavnet</VNetName>
    <SubnetName>SUSE12RDMACluster</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpclab.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>SUSE12RDMA-HN</VMName>
    <ServiceName>suse12rdma-je</ServiceName>
    <VMSize>A8</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>SUSE12RDMA-LN%1%</VMNamePattern>
    <ServiceName>suse12rdma-je</ServiceName>
    <VMSize>A8</VMSize>
    <NodeCount>2</NodeCount>
      <ImageName>b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-hpc-v20150708</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```

### <a name="sample-credxml-file"></a>Exemple de fichier cred.xml
```
<ExtendedData>
  <PrivateKey>-----BEGIN RSA PRIVATE KEY-----
MIIEpQIBAAKCAQEAxJKBABhnOsE9eneGHvsjdoXKooHUxpTHI1JVunAJkVmFy8JC
qFt1pV98QCtKEHTC6kQ7tj1UT2N6nx1EY9BBHpZacnXmknpKdX4Nu0cNlSphLpru
lscKPR3XVzkTwEF00OMiNJVknq8qXJF1T3lYx3rW5EnItn6C3nQm3gQPXP0ckYCF
Jdtu/6SSgzV9kaapctLGPNp1Vjf9KeDQMrJXsQNHxnQcfiICp21NiUCiXosDqJrR
AfzePdl0XwsNngouy8t0fPlNSngZvsx+kPGh/AKakKIYS0cO9W3FmdYNW8Xehzkc
VzrtJhU8x21hXGfSC7V0ZeD7dMeTL3tQCVxCmwIDAQABAoIBAQCve8Jh3Wc6koxZ
qh43xicwhdwSGyliZisoozYZDC/ebDb/Ydq0BYIPMiDwADVMX5AqJuPPmwyLGtm6
9hu5p46aycrQ5+QA299g6DlF+PZtNbowKuvX+rRvPxagrTmupkCswjglDUEYUHPW
05wQaNoSqtzwS9Y85M/b24FfLeyxK0n8zjKFErJaHdhVxI6cxw7RdVlSmM9UHmah
wTkW8HkblbOArilAHi6SlRTNZG4gTGeDzPb7fYZo3hzJyLbcaNfJscUuqnAJ+6pT
iY6NNp1E8PQgjvHe21yv3DRoVRM4egqQvNZgUbYAMUgr30T1UoxnUXwk2vqJMfg2
Nzw0ESGRAoGBAPkfXjjGfc4HryqPkdx0kjXs0bXC3js2g4IXItK9YUFeZzf+476y
OTMQg/8DUbqd5rLv7PITIAqpGs39pkfnyohPjOe2zZzeoyaXurYIPV98hhH880uH
ZUhOxJYnlqHGxGT7p2PmmnAlmY4TSJrp12VnuiQVVVsXWOGPqHx4S4f9AoGBAMn/
vuea7hsCgwIE25MJJ55FYCJodLkioQy6aGP4NgB89Azzg527WsQ6H5xhgVMKHWyu
Q1snp+q8LyzD0i1veEvWb8EYifsMyTIPXOUTwZgzaTTCeJNHdc4gw1U22vd7OBYy
nZCU7Tn8Pe6eIMNztnVduiv+2QHuiNPgN7M73/x3AoGBAOL0IcmFgy0EsR8MBq0Z
ge4gnniBXCYDptEINNBaeVStJUnNKzwab6PGwwm6w2VI3thbXbi3lbRAlMve7fKK
B2ghWNPsJOtppKbPCek2Hnt0HUwb7qX7Zlj2cX/99uvRAjChVsDbYA0VJAxcIwQG
TxXx5pFi4g0HexCa6LrkeKMdAoGAcvRIACX7OwPC6nM5QgQDt95jRzGKu5EpdcTf
g4TNtplliblLPYhRrzokoyoaHteyxxak3ktDFCLj9eW6xoCZRQ9Tqd/9JhGwrfxw
MS19DtCzHoNNewM/135tqyD8m7pTwM4tPQqDtmwGErWKj7BaNZARUlhFxwOoemsv
R6DbZyECgYEAhjL2N3Pc+WW+8x2bbIBN3rJcMjBBIivB62AwgYZnA2D5wk5o0DKD
eesGSKS5l22ZMXJNShgzPKmv3HpH22CSVpO0sNZ6R+iG8a3oq4QkU61MT1CfGoMI
a8lxTKnZCsRXU1HexqZs+DSc+30tz50bNqLdido/l5B4EJnQP03ciO0=
-----END RSA PRIVATE KEY-----</PrivateKey>
  <PublicKey>ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDEkoEAGGc6wT16d4Ye+yN2hcqigdTGlMcjUlW6cAmRWYXLwkKoW3WlX3xAK0oQdMLqRDu2PVRPY3qfHURj0EEellpydeaSekp1fg27Rw2VKmEumu6Wxwo9HddXORPAQXTQ4yI0lWSerypckXVPeVjHetbkSci2foLedCbeBA9c/RyRgIUl227/pJKDNX2Rpqly0sY82nVWN/0p4NAyslexA0fGdBx+IgKnbU2JQKJeiwOomtEB/N492XRfCw2eCi7Ly3R8+U1KeBm+zH6Q8aH8ApqQohhLRw71bcWZ1g1bxd6HORxXOu0mFTzHbWFcZ9ILtXRl4Pt0x5Mve1AJXEKb username@servername;</PublicKey>
</ExtendedData>
```
### <a name="sample-silentcfg-file-tooinstall-mpi"></a>Exemple silent.cfg fichier tooinstall MPI
```
# Patterns used toocheck silent configuration file
#
# anythingpat - any string
# filepat     - hello file location pattern (/file/location/to/license.lic)
# lspat       - hello license server address pattern (0123@hostname)
# snpat       - hello serial number pattern (ABCD-01234567)

# accept EULA, valid values are: {accept, decline}
ACCEPT_EULA=accept

# optional error behavior, valid values are: {yes, no}
CONTINUE_WITH_OPTIONAL_ERROR=yes

# install location, valid values are: {/opt/intel, filepat}
PSET_INSTALL_DIR=/opt/intel

# continue with overwrite of existing installation directory, valid values are: {yes, no}
CONTINUE_WITH_INSTALLDIR_OVERWRITE=yes

# list of components tooinstall, valid values are: {ALL, DEFAULTS, anythingpat}
COMPONENTS=DEFAULTS

# installation mode, valid values are: {install, modify, repair, uninstall}
PSET_MODE=install

# directory for non-RPM database, valid values are: {filepat}
#NONRPM_DB_DIR=filepat

# Serial number, valid values are: {snpat}
#ACTIVATION_SERIAL_NUMBER=snpat

# License file or license server, valid values are: {lspat, filepat}
#ACTIVATION_LICENSE_FILE=

# Activation type, valid values are: {exist_lic, license_server, license_file, trial_lic, serial_number}
ACTIVATION_TYPE=trial_lic

# Path toohello cluster description file, valid values are: {filepat}
#CLUSTER_INSTALL_MACHINES_FILE=filepat

# Intel(R) Software Improvement Program opt-in, valid values are: {yes, no}
PHONEHOME_SEND_USAGE_DATA=no

# Perform validation of digital signatures of RPM files, valid values are: {yes, no}
SIGNING_ENABLED=yes

# Select yes tooenable mpi-selector integration, valid values are: {yes, no}
ENVIRONMENT_REG_MPI_ENV=no

# Select yes tooupdate ld.so.conf, valid values are: {yes, no}
ENVIRONMENT_LD_SO_CONF=no


```

### <a name="sample-settingssh-script"></a>Exemple de script settings.sh
```
#!/bin/bash

# impi
source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh
export MPI_ROOT=$I_MPI_ROOT
export I_MPI_FABRICS=shm:dapl
export I_MPI_DAPL_PROVIDER=ofa-v2-ib0
export I_MPI_DYNAMIC_CONNECTION=0

# openfoam
export FOAM_INST_DIR=/opt/OpenFOAM
source /opt/OpenFOAM/OpenFOAM-2.3.1/etc/bashrc
export WM_MPLIB=INTELMPI
```


### <a name="sample-hpcimpirunsh-script"></a>Exemple de script hpcimpirun.sh
```
#!/bin/bash

# hello path of this script
SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"

# Set mpirun runtime evironment
source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh
export MPI_ROOT=$I_MPI_ROOT
export I_MPI_FABRICS=shm:dapl
export I_MPI_DAPL_PROVIDER=ofa-v2-ib0
export I_MPI_DYNAMIC_CONNECTION=0

# mpirun command
MPIRUN=mpirun
# Argument of "--hostfile"
NODELIST_OPT="--hostfile"
# Argument of "-np"
NUMPROCESS_OPT="-np"

# Get node information from ENVs
NODESCORES=(${CCP_NODES_CORES})
COUNT=${#NODESCORES[@]}

if [ ${COUNT} -eq 0 ]
then
    # CCP_NODES_CORES is not found or is empty, just run hello mpirun without hostfile arg.
    ${MPIRUN} $*
else
    # Create hello hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$

    # Get every node name and write into hello hostfile file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run hello mpirun with hostfile arg
    ${MPIRUN} ${NUMPROCESS_OPT} ${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*

    RTNSTS=$?
    rm -f ${NODELIST_PATH}
fi

exit ${RTNSTS}

```





<!--Image references-->
[keygen]:media/hpcpack-cluster-openfoam/keygen.png
[keys]:media/hpcpack-cluster-openfoam/keys.png
[step_variables]:media/hpcpack-cluster-openfoam/step_variables.png
[data_files]:media/hpcpack-cluster-openfoam/data_files.png
[decompose]:media/hpcpack-cluster-openfoam/decompose.png
[job_details]:media/hpcpack-cluster-openfoam/job_details.png
[job_resources]:media/hpcpack-cluster-openfoam/job_resources.png
[task_details1]:media/hpcpack-cluster-openfoam/task_details1.png
[task_dependencies]:media/hpcpack-cluster-openfoam/task_dependencies.png
[creds]:media/hpcpack-cluster-openfoam/creds.png
[heat_map]:media/hpcpack-cluster-openfoam/heat_map.png
[tank]:media/hpcpack-cluster-openfoam/tank.png
[tank_result]:media/hpcpack-cluster-openfoam/tank_result.png
[isosurface]:media/hpcpack-cluster-openfoam/isosurface.png
[isosurface_color]:media/hpcpack-cluster-openfoam/isosurface_color.png
[linux_processes]:media/hpcpack-cluster-openfoam/linux_processes.png
