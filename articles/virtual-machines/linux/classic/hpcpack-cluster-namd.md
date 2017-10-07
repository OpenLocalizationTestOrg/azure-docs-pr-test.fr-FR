---
title: aaaNAMD avec Microsoft HPC Pack sur les machines virtuelles Linux | Documents Microsoft
description: "Déployer un cluster Microsoft HPC Pack sur Azure et exécuter une simulation NAMD avec charmrun sur plusieurs nœuds de calcul Linux"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 76072c6b-ac35-4729-ba67-0d16f9443bd7
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 10/13/2016
ms.author: danlep
ms.openlocfilehash: 90c722f66b494335a62c0613079366ae99002076
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-namd-with-microsoft-hpc-pack-on-linux-compute-nodes-in-azure"></a>Exécution de NAMD avec Microsoft HPC Pack sur des nœuds de calcul Linux dans Azure
Cet article explique monodirectionnelle toorun une charge de travail informatique de hautes performances (HPC) Linux sur les machines virtuelles. Ici, vous configurez un [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) de cluster avec les nœuds de calcul Linux sur Azure et exécuter un [NAMD](http://www.ks.uiuc.edu/Research/namd/) toocalculate de simulation et de visualiser la structure hello d’un système BIOMOLÉCULAIRE volumineux.  

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

* **NAMD** (pour le programme de Dynamics moléculaire d’a) est un package parallèle dynamics moléculaire conçu pour la simulation de hautes performances des systèmes de BIOMOLÉCULAIRE volumineux contenant des toomillions des atomes. Ces systèmes sont par exemple les virus, les structures de cellule et les grandes protéines. NAMD ajuste toohundreds de cœurs pour les simulations classiques et toomore à 500 000 cœurs pour les simulations de plus grande hello.
* **Microsoft HPC Pack** fournit les fonctionnalités toorun HPC à grande échelle et des applications parallèles dans les clusters d’ordinateurs locaux ou des machines virtuelles. Développée à l’origine comme solution pour les charges de travail Windows HPC, HPC Pack prend désormais en charge l’exécution d’applications HPC Linux sur les machines virtuelles de nœuds de calcul Linux déployées dans un cluster HPC Pack. Consultez la présentation [Prise en main des nœuds de calcul Linux dans un cluster HPC Pack dans Azure](hpcpack-cluster.md) .

Pour les autres options de toorun Linux HPC les charges de travail dans Azure, consultez [ressources techniques pour le traitement et l’informatique hautes performances](../../../batch/batch-hpc-solutions.md).

## <a name="prerequisites"></a>Composants requis
* **Cluster HPC Pack avec nœuds de calcul Linux** : déployez un cluster HPC Pack avec des nœuds de calcul Linux dans Azure à l’aide d’un [modèle Azure Resource Manager](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) ou d’un [script Azure PowerShell](hpcpack-cluster-powershell-script.md). Consultez [prise en main des nœuds de calcul Linux dans un cluster HPC Pack dans Azure](hpcpack-cluster.md) pour les conditions préalables de hello et étapes dans les deux cas. Si vous choisissez hello option de déploiement de script PowerShell, consultez le fichier de configuration d’exemple hello dans les fichiers d’exemple hello à fin hello de cet article. Ce fichier configure un cluster HPC Pack basé sur Azure comportant un nœud principal Windows Server 2012 R2 et quatre nœuds de calcul de grande taille CentOS 6.6. Personnalisez ce fichier comme il convient pour votre environnement.
* **Fichiers de logiciel et didacticiel NAMD** -logiciel NAMD de téléchargement pour Linux à partir de hello [NAMD](http://www.ks.uiuc.edu/Research/namd/) site (inscription requise). Cet article est basé sur la version 2.10 de NAMD et utilise hello [Linux-x86_64 (64 bits Intel/AMD avec Ethernet)](http://www.ks.uiuc.edu/Development/Download/download.cgi?UserID=&AccessCode=&ArchiveID=1310) archive. Téléchargez également hello [de fichiers de didacticiel NAMD](http://www.ks.uiuc.edu/Training/Tutorials/#namd). Hello téléchargements sont les fichiers .tar, et vous avez besoin d’un Windows outil tooextract hello les fichiers sur le nœud principal du cluster hello. fichiers de hello tooextract, suivez les instructions de hello plus loin dans cet article. 
* **VMD** (facultatif) - toosee les résultats de hello de votre travail NAMD, télécharger et installer le programme de visualisation moléculaire hello [VMD](http://www.ks.uiuc.edu/Research/vmd/) sur un ordinateur de votre choix. version actuelle de Hello est 1.9.2. Consultez hello VDM télécharger tooget de site a démarré.  

## <a name="set-up-mutual-trust-between-compute-nodes"></a>Configuration de l’approbation mutuelle entre les nœuds de calcul
L’exécution d’une tâche entre nœuds sur plusieurs nœuds Linux requiert hello nœuds tootrust eux (par **rsh** ou **ssh**). Lorsque vous créez un cluster HPC Pack de hello avec hello script de déploiement Microsoft HPC Pack IaaS, script de hello configure automatiquement permanente confiance mutuelle pour le compte administrateur hello que vous spécifiez. Pour les utilisateurs non-administrateurs que vous créez dans le domaine de ce cluster hello, vous avez tooset temporaire approbation mutuelle entre les nœuds de hello lorsqu’un travail est alloué toothem. Ensuite, détruisez relation de hello hello tâche est terminée. toodo cela pour chaque utilisateur, de fournir un cluster toohello de paire de clés RSA les HPC Pack utilise la relation d’approbation tooestablish hello. Instructions ci-dessous.

### <a name="generate-an-rsa-key-pair"></a>Génération d’une paire de clés RSA
Il est facile toogenerate une paire de clés RSA, qui contient une clé publique et une clé privée, en exécutant hello Linux **ssh-keygen** commande.

1. Ouvrez une session tooa ordinateur Linux.
2. Exécutez hello de commande suivante :
   
   ```bash
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
1. [Connexion Bureau à distance](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) à l’aide de machine virtuelle de nœud principal toohello hello des informations d’identification de domaine vous avez fourni lorsque vous avez déployé le cluster hello (par exemple, hpc\clusteradmin). Vous gérez un cluster de hello à partir du nœud principal hello.
2. Utilisez toocreate de procédures standard Windows Server un compte d’utilisateur de domaine dans le domaine d’Active Directory du cluster hello. Par exemple, utiliser hello utilisateur Active Directory et outil d’ordinateurs sur le nœud principal de hello. les exemples de Hello dans cet article supposent que vous créez un utilisateur de domaine nommé hpcuser dans le domaine de hpclab hello (hpclab\hpcuser).
3. Ajoutez le cluster HPC Pack toohello hello domaine utilisateur en tant qu’un utilisateur de cluster. Pour obtenir des instructions, consultez [Ajouter ou supprimer des utilisateurs du cluster](https://technet.microsoft.com/library/ff919330.aspx).
4. Créez un fichier nommé C:\cred.xml et copier hello RSA clé des données dans celui-ci. Vous trouverez un exemple Bonjour exemples de fichiers à la fin de hello de cet article.
   
   ```
   <ExtendedData>
     <PrivateKey>Copy hello contents of private key here</PrivateKey>
     <PublicKey>Copy hello contents of public key here</PublicKey>
   </ExtendedData>
   ```
5. Ouvrez une invite de commandes et entrez hello tooset hello données hello hpclab\hpcuser compte les informations d’identification de commande suivante. Vous utilisez hello **extendeddata** toopass de paramètre hello nom du fichier de C:\cred.xml hello vous avez créé pour les données de clé hello.
   
   ```command
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   Cette commande se termine correctement sans sortie. Après avoir défini les informations d’identification hello pour les comptes d’utilisateur hello que vous devez toorun travaux, stockez le fichier de cred.xml de hello dans un emplacement sécurisé ou supprimez-le.
6. Si vous avez généré hello paire de clés RSA sur l’un de vos nœuds de Linux, n’oubliez pas les clés hello toodelete après avoir terminé leur utilisation. HPC Pack ne configure pas l’approbation mutuelle s’il trouve des fichiers id_rsa ou id_rsa.pub existants.

> [!IMPORTANT]
> Nous ne recommandons l’exécution d’un travail de Linux en tant qu’un administrateur de cluster sur un cluster partagé, car une tâche envoyée par un administrateur s’exécute sous un compte de racine hello des nœuds de Linux hello. Une tâche envoyée par un utilisateur non administrateur s’exécute sous un compte d’utilisateur local Linux avec hello même nom en tant qu’utilisateur de tâche hello. Dans ce cas, HPC Pack définit confiance mutuelle pour cet utilisateur Linux sur tous les nœuds hello allouées toohello travail. Vous pouvez configurer des utilisateurs de Linux hello manuellement sur les nœuds de Linux hello avant d’exécuter le travail de hello ou HPC Pack crée automatiquement les utilisateur hello lorsque le travail de hello est envoyé. Si HPC Pack crée un utilisateur de hello, HPC Pack supprime une fois hello travail terminé. tooreduce menace pour la sécurité, hello clés sont supprimées après la fin de la tâche de hello sur les nœuds hello.
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a>Configuration d’un partage de fichiers pour les nœuds Linux
Maintenant configurer un partage de fichiers SMB et monter le dossier partagé de hello sur tous les nœuds tooallow hello Linux nœuds tooaccess NAMD fichiers Linux avec un chemin d’accès commun. Voici les étapes toomount un dossier partagé sur le nœud principal de hello. Un partage est recommandé pour les distributions tels que CentOS 6.6 actuellement ne prend en charge les services de fichiers Azure hello. Si vos nœuds Linux prend en charge un partage de fichiers Azure, consultez [comment toouse stockage Azure files avec Linux](../../../storage/files/storage-how-to-use-files-linux.md). Pour des options supplémentaires de partage des fichiers avec HPC Pack, consultez [Prise en main des nœuds de calcul Linux dans un cluster HPC Pack dans Azure](hpcpack-cluster.md).

1. Créez un dossier sur le nœud principal de hello et partagez-le tooEveryone en définissant des privilèges de lecture/écriture. Dans cet exemple, \\ \\CentOS66HN\Namd est le nom hello du dossier hello, où CentOS66HN est le nom d’hôte hello de nœud principal de hello.
2. Créer un sous-dossier nommé namd2 dans le dossier partagé de hello. Créez un autre sous-dossier nommé namdsample dans namd2.
3. Extraire hello NAMD fichiers hello dossier à l’aide d’une version Windows de **tar** ou un autre utilitaire de Windows qui fonctionne sur les archives .tar. 
   
   * Extraire archive tar NAMD hello trop\\\\CentOS66HN\Namd\namd2.
   * Extraire les fichiers du didacticiel hello sous \\ \\CentOS66HN\Namd\namd2\namdsample.
4. Ouvrez une fenêtre Windows PowerShell et exécutez hello suivant les commandes toomount hello dossier partagé sur les nœuds de Linux hello.
   
    ```command
    clusrun /nodegroup:LinuxNodes mkdir -p /namd2
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS66HN/Namd/namd2 /namd2 -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

Hello première commande crée un dossier nommé /namd2 sur tous les nœuds dans le groupe de LinuxNodes hello. commande deuxième Hello monte hello partagé dossier //CentOS66HN/Namd/namd2 sur le dossier hello avec dir_mode et file_mode too777 d’ensemble de bits. Hello *nom d’utilisateur* et *mot de passe* Bonjour commande doit-elle être des informations d’identification de hello d’un utilisateur sur le nœud principal de hello.

> [!NOTE]
> Hello »\`« symbole dans la deuxième commande de hello est un symbole d’échappement pour PowerShell. «\`, « signifie hello », » (virgule) est une partie de la commande hello.
> 
> 

## <a name="create-a-bash-script-toorun-a-namd-job"></a>Créer un toorun de script Bash un travail NAMD
Votre travail NAMD un *nodelist* de fichiers pour **charmrun** toodetermine hello quantité, nœuds toouse lors du démarrage du processus NAMD. Vous utilisez un script d’interpréteur de commandes qui génère le fichier de liste de nœuds hello et exécute **charmrun** avec ce fichier de liste de nœuds. Vous pouvez ensuite envoyer une tâche NAMD dans HPC Cluster Manager qui appelle ce script.

À l’aide d’un éditeur de texte de votre choix, créez un script d’interpréteur de commandes dans le dossier de /namd2 hello contenant les fichiers de programme NAMD hello et nommez-le hpccharmrun.sh. Pour obtenir une rapide preuve de concept, copiez hello exemple hpccharmrun.sh de script fourni à fin hello de cet article, puis accédez trop[soumettre un travail NAMD](#submit-a-namd-job).

> [!TIP]
> Enregistrez votre script en tant que fichier texte avec des fins de ligne Linux (LF uniquement, pas CR LF). Cela garantit qu’elle s’exécute correctement sur les nœuds de Linux hello.
> 
> 

Voici les détails des actions du script Bash. 

1. Définir des variables.
   
   ```bash
   #!/bin/bash
   
   # hello path of this script
   SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
   # Charmrun command
   CHARMRUN=${SCRIPT_PATH}/charmrun
   # Argument of ++nodelist
   NODELIST_OPT="++nodelist"
   # Argument of ++p
   NUMPROCESS="+p"
   ```
2. Obtenir des informations sur les nœuds à partir de variables d’environnement hello. $NODESCORES stocke une liste de mots de fractionnement à partir de $CCP_NODES_CORES. $COUNT n’hello taille $NODESCORES.
   
   ```
   # Get node information from hello environment variables
   NODESCORES=(${CCP_NODES_CORES})
   COUNT=${#NODESCORES[@]}
   ```    
   
   format Hello pour la variable CCP_NODES_CORES $ hello est comme suit :
   
   ```
   <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>…
   ```
   
   Cette variable répertorie le nombre total de hello de nœuds, les noms de nœud et nombre de cœurs sur chaque nœud qui sont alloués toohello travail. Par exemple, si le travail de hello doit 10 cœurs toorun, valeur hello $CCP_NODES_CORES est similaire à :
   
   ```
   3 CENTOS66LN-00 4 CENTOS66LN-01 4 CENTOS66LN-03 2
   ```
3. Si la variable CCP_NODES_CORES $ hello n’est pas définie, démarrez **charmrun** directement. (Cela doit uniquement se produire lorsque vous exécutez ce script directement sur vos nœuds Linux.)
   
   ```
   if [ ${COUNT} -eq 0 ]
   then
     # CCP_NODES is_CORES is not found or is empty, so just run charmrun without nodelist arg.
     #echo ${CHARMRUN} $*
     ${CHARMRUN} $*
   ```
4. Ou créer un fichier de liste de nœuds pour **charmrun**.
   
   ```
   else
     # Create hello nodelist file
     NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$
   
     # Write hello head line
     echo "group main" > ${NODELIST_PATH}
   
     # Get every node name and number of cores and write into hello nodelist file
     I=1
     while [ ${I} -lt ${COUNT} ]
     do
         echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
         let "I=${I}+2"
     done
   ```
5. Exécutez **charmrun** avec le fichier de liste de nœuds hello, obtenir son état de retour et supprimer le fichier de liste de nœuds hello à fin de hello.
   
   ${CCP_NUMCPUS} est une autre variable d’environnement définie par le nœud principal HPC Pack de hello. Il stocke le nombre hello de cœurs total alloué toothis travail. Nous utiliserons pas toospecify hello sur différents processus à charmrun.
   
   ```
   # Run charmrun with nodelist arg
   #echo ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   
   RTNSTS=$?
   rm -f ${NODELIST_PATH}
   fi
   
   ```
6. Sortie avec hello **charmrun** état de retour.
   
   ```
   exit ${RTNSTS}
   ```

Voici quelques informations hello dans fichier de liste de nœuds hello, le script de hello génère :

```
group main
host <Name of node1> ++cpus <Cores of node1>
host <Name of node2> ++cpus <Cores of node2>
…
```

Par exemple :

```
group main
host CENTOS66LN-00 ++cpus 4
host CENTOS66LN-01 ++cpus 4
host CENTOS66LN-03 ++cpus 2
```

## <a name="submit-a-namd-job"></a>Envoi d’une tâche NAMD
Vous êtes maintenant prêt toosubmit un travail NAMD dans HPC Cluster Manager.

1. Se connecter tooyour nœud principal du cluster et démarrez le Gestionnaire du Cluster HPC.
2. Dans **gestion des ressources**, assurez-vous que les nœuds de calcul Linux hello sont Bonjour **Online** état. Si ce n’est pas le cas, sélectionnez-les et cliquez sur **Mettre en ligne**.
3. Dans **Gestion des tâches**, cliquez sur **Nouveau travail**.
4. Entrez un nom pour la tâche, par exemple *hpccharmrun*.
   
   ![Nouvelle tâche HPC][namd_job]
5. Sur hello **détails de la tâche** sous **des ressources de travail**, sélectionner le type de hello de ressource en tant que **nœud** et ensemble hello **Minimum** too3. , nous exécutons les travaux hello sur trois nœuds Linux, et chaque nœud possède quatre cœurs.
   
   ![ressources de la tâche][job_resources]
6. Cliquez sur **modifier des tâches** dans hello du volet de navigation gauche, puis cliquez sur **ajouter** tooadd un travail de toohello de tâches.    
7. Sur hello **détails de la tâche et la Redirection des e/s** page hello du jeu de valeurs suivantes :
   
   * **Ligne de commande**-
     `/namd2/hpccharmrun.sh ++remote-shell ssh /namd2/namd2 /namd2/namdsample/1-2-sphere/ubq_ws_eq.conf > /namd2/namd2_hpccharmrun.log`
     
     > [!TIP]
     > Hello ligne de commande précédente est une commande unique sans saut de ligne. Elle encapsule tooappear sur plusieurs lignes sous **ligne de commande**.
     > 
     > 
   * **Répertoire de travail** : /namd2
   * **Minimum** : 3
     
     ![Détails de la tâche][task_details]
     
     > [!NOTE]
     > Vous définissez répertoire de travail hello ici car **charmrun** tente toonavigate toohello même répertoire de travail sur chaque nœud. Si le répertoire de travail hello n’est pas défini, HPC Pack démarre la commande hello dans un dossier nommé de façon aléatoire créé sur l’un des nœuds de Linux hello. Cela provoque des autres nœuds hello l’erreur suivante sur hello : `/bin/bash: line 37: cd: /tmp/nodemanager_task_94_0.mFlQSN: No such file or directory.` tooavoid ce problème, spécifiez un chemin d’accès du dossier qui est accessible par tous les nœuds en tant que répertoire de travail hello.
     > 
     > 
8. Cliquez sur **OK** puis cliquez sur **Submit** toorun ce travail.
   
   Par défaut, HPC Pack soumet le travail hello que votre compte d’utilisateur connecté actuel. Une boîte de dialogue peut vous demander nom d’utilisateur tooenter hello et le mot de passe après avoir cliqué sur **Submit**.
   
   ![Informations d’identification de la tâche][creds]
   
   Sous certaines conditions, HPC Pack mémorise les informations d’utilisateur hello d’entrée avant et de ne plus afficher cette boîte de dialogue. toomake HPC Pack afficher à nouveau, entrez hello commande à l’invite de commande suivante et l’envoi de la tâche de hello puis.
   
   ```command
   hpccred delcreds
   ```
9. travail de Hello prend plusieurs minutes toofinish.
10. Rechercher le journal des travaux hello à \\ <headnodeName>\Namd\namd2\namd2_hpccharmrun.log et hello dans les fichiers de sortie \\ <headnodeName>\Namd\namd2\namdsample\1-2-sphere\.
11. Vous pouvez également démarrer VDM tooview vos résultats de la tâche. étapes de Hello pour visualiser des fichiers de sortie hello NAMD (dans ce cas, une molecule de PROTEINE UBIQUITINE dans une sphère d’eau) sont abordée dans cet article hello. Voir [Didacticiel NAMD](http://www.life.illinois.edu/emad/biop590c/namd-tutorial-unix-590C.pdf) pour plus d'informations.
    
    ![Résultats de la tâche][vmd_view]

## <a name="sample-files"></a>Exemple de fichiers
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a>Exemple de fichier de configuration XML pour le déploiement de clusters par script PowerShell
```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
      <Location>West US</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpclab.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>CentOS66HN</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>Large</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>CentOS66LN-%00%</VMNamePattern>
    <ServiceName>MyLnxCNService</ServiceName>
     <VMSize>Large</VMSize>
     <NodeCount>4</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-66-20150325</ImageName>
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

### <a name="sample-hpccharmrunsh-script"></a>Exemple de script hpccharmrun.sh
```
#!/bin/bash

# hello path of this script
SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
# Charmrun command
CHARMRUN=${SCRIPT_PATH}/charmrun
# Argument of ++nodelist
NODELIST_OPT="++nodelist"
# Argument of ++p
NUMPROCESS="+p"

# Get node information from ENVs
# CCP_NODES_CORES=3 CENTOS66LN-00 4 CENTOS66LN-01 4 CENTOS66LN-03 4
NODESCORES=(${CCP_NODES_CORES})
COUNT=${#NODESCORES[@]}

if [ ${COUNT} -eq 0 ]
then
    # If CCP_NODES_CORES is not found or is empty, just run hello charmrun without nodelist arg.
    #echo ${CHARMRUN} $*
    ${CHARMRUN} $*
else
    # Create hello nodelist file
    NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$

    # Write hello head line
    echo "group main" > ${NODELIST_PATH}

    # Get every node name & cores and write into hello nodelist file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run hello charmrun with nodelist arg
    #echo ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
    ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*

    RTNSTS=$?
    rm -f ${NODELIST_PATH}
fi

exit ${RTNSTS}
```

 

<!--Image references-->
[keygen]:media/hpcpack-cluster-namd/keygen.png
[keys]:media/hpcpack-cluster-namd/keys.png
[namd_job]:media/hpcpack-cluster-namd/namd_job.png
[job_resources]:media/hpcpack-cluster-namd/job_resources.png
[creds]:media/hpcpack-cluster-namd/creds.png
[task_details]:media/hpcpack-cluster-namd/task_details.png
[vmd_view]:media/hpcpack-cluster-namd/vmd_view.png
