---
title: "aaaHigh disponibilité de SAP HANA sur Azure des Machines virtuelles (VM) | Documents Microsoft"
description: "Créer une haute disponibilité de SAP HANA sur des machines virtuelles Azure."
services: virtual-machines-linux
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 04/25/2017
ms.author: sedusch
ms.openlocfilehash: dcb9bb70594f9d97f8a888cec76300bcbe0bf1ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-of-sap-hana-on-azure-virtual-machines-vms"></a>Haute disponibilité de SAP HANA sur des machines virtuelles Azure

[dbms-guide]:dbms-guide.md
[deployment-guide]:deployment-guide.md
[planning-guide]:planning-guide.md

[2205917]:https://launchpad.support.sap.com/#/notes/2205917
[1944799]:https://launchpad.support.sap.com/#/notes/1944799
[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2191498]:https://launchpad.support.sap.com/#/notes/2191498
[2243692]:https://launchpad.support.sap.com/#/notes/2243692
[1984787]:https://launchpad.support.sap.com/#/notes/1984787
[1999351]:https://launchpad.support.sap.com/#/notes/1999351

[hana-ha-guide-replication]:sap-hana-high-availability.md#14c19f65-b5aa-4856-9594-b81c7e4df73d
[hana-ha-guide-shared-storage]:sap-hana-high-availability.md#498de331-fa04-490b-997c-b078de457c9d

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[sap-swcenter]:https://launchpad.support.sap.com/#/softwarecenter
[template-multisid-db]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged%2Fazuredeploy.json

Locale, vous pouvez utiliser la réplication du système soit HANA ou utiliser un stockage partagé tooestablish haute disponibilité pour SAP HANA.
Azure ne prend en charge actuellement que la configuration de la réplication système HANA. La réplication SAP HANA se compose d’un nœud principal et d’au moins un nœud subordonné. Toohello de modifications de données sur le nœud principal de hello sont répliquées de nœuds d’esclave toohello synchrone ou asynchrone.

Cet article décrit comment toodeploy hello des machines virtuelles, configurer des machines virtuelles de hello installer hello cluster framework, installer et configurer la réplication du système SAP HANA.
Dans les configurations d’exemple hello, numéro d’instance etc. 03 commandes d’installation et HANA système ID HDB est utilisé.

Lire hello suivant tout d’abord les Notes SAP et livres

* Note SAP [1928533], qui contient :
  * Liste des tailles de machine virtuelle Azure qui sont pris en charge pour le déploiement de hello de logiciels SAP
  * des informations importantes sur la capacité en fonction de la taille des machines virtuelles Azure
  * les logiciels SAP pris en charge et les combinaisons entre système d’exploitation et base de données
  * la version du noyau SAP requise pour Windows et Linux sur Microsoft Azure
* La note SAP [2015553] répertorie les conditions préalables au déploiement de logiciels SAP pris en charge par SAP sur Azure.
* La note SAP [2205917] contient des paramètres de système d’exploitation recommandés pour SUSE Linux Enterprise Server pour les applications SAP
* La note SAP [1944799] contient des instructions SAP HANA pour SUSE Linux Enterprise Server pour les applications SAP
* La note SAP [2178632] contient des informations détaillées sur toutes les métriques de surveillance rapportées pour SAP sur Azure.
* La Note SAP [2191498] hello requise version de l’Agent hôte SAP pour Linux dans Azure.
* La note SAP [2243692] contient des informations sur les licences SAP sur Linux dans Azure.
* La note SAP [1984787] contient des informations sur SUSE Linux Enterprise Server 12.
* La Note SAP [1999351] a des informations de dépannage supplémentaires pour hello améliorée Extension de surveillance Azure pour SAP.
* Le [WIKI de la communauté SAP](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) contient toutes les notes SAP requises pour Linux.
* [Planification et implémentation de Machines virtuelles Azure pour SAP sur Linux][planning-guide]
* [Déploiement de Machines virtuelles Azure pour SAP sur Linux (cet article)][deployment-guide]
* [Déploiement SGBD de Machines virtuelles Azure pour SAP sur Linux][dbms-guide]
* [Scénario d’optimisé de performances SAP HANA SR] [ suse-hana-ha-guide] guide de hello contient toutes les informations requises tooset, réplication du système SAP HANA en local. Utilisez ce guide comme référence.

## <a name="deploying-linux"></a>Déploiement de Linux

l’agent de ressource Hello pour SAP HANA est inclus dans SUSE Linux Enterprise Server pour les Applications SAP.
Bonjour Azure Marketplace contient une image pour SUSE Linux Enterprise Server 12 d’Applications SAP avec BYOS (apportez votre propre abonnement) que vous pouvez utiliser les nouveaux ordinateurs virtuels de toodeploy.

### <a name="manual-deployment"></a>Déploiement manuel

1. Création d’un groupe de ressources
1. Création d'un réseau virtuel
1. Créer deux comptes de stockage
1. Créer un groupe à haute disponibilité  
   Définir un domaine de mise à jour maximal
1. Créer un équilibrage de charge (interne)  
   Sélectionner le réseau virtuel de l’étape précédente
1. Créer la machine virtuelle 1  
   https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1  
   SLES For SAP Applications 12 SP1 (BYOS)  
   Sélectionner le compte de stockage 1  
   Sélectionner le groupe à haute disponibilité  
1. Créer la machine virtuelle 2  
   https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1  
   SLES For SAP Applications 12 SP1 (BYOS)  
   Sélectionner le compte de stockage 2   
   Sélectionner le groupe à haute disponibilité  
1. Ajouter des disques de données
1. Configurer l’équilibrage de charge hello
    1. Créer un pool d’adresse IP frontal
        1. Ouvrez hello l’équilibrage de charge, sélectionnez le pool d’adresses IP de serveur frontal et cliquez sur Ajouter
        1. Entrez le nom hello de hello nouveau serveur frontal pool IP (par exemple hana-frontend)
       1. Cliquez sur OK
        1. Une fois le nouveau pool d’IP frontale hello est créé, notez son adresse IP
    1. Créer un pool principal
        1. Ouvrez l’équilibrage de charge hello, pools principaux, cliquez sur Ajouter
        1. Entrez hello nom hello nouveau serveur principal du pool de (par exemple hana principal)
        1. Cliquer sur Ajouter une machine virtuelle
        1. Sélectionnez hello que vous avez créé précédemment à haute disponibilité
        1. Sélectionner des machines virtuelles hello du cluster de SAP HANA hello
        1. Cliquez sur OK
    1. Créer une sonde d’intégrité
       1. Ouvrez l’équilibrage de charge hello, sondes d’intégrité, cliquez sur Ajouter
        1. Entrez le nom hello de sonde d’intégrité nouvelle hello (par exemple hana hp)
        1. Sélectionner le protocole TCP et le port 625**03**, et conserver un intervalle de 5 et un seuil de défaillance de 2
        1. Click OK
    1. Créer des règles d’équilibrage de charge
        1. Ouvrez l’équilibrage de charge hello, règles d’équilibrage de charge, cliquez sur Ajouter
        1. Entrez le nom hello de nouvelle règle d’équilibrage de charge hello (par exemple hana-lb-3**03**15)
        1. Adresse IP de serveur frontal sélectionnez hello, pool principal et l’intégrité de sonde vous avez créé précédemment (par exemple hana-frontend)
        1. Conserver le protocole TCP et choisir le port 3**03**15
        1. Augmenter le délai d’inactivité too30 minutes
       1. **Assurez-vous que tooenable IP flottante**
        1. Cliquez sur OK
        1. Répétez les étapes de hello ci-dessus pour le port 3**03**17

### <a name="deploy-with-template"></a>Déployer avec un modèle
Vous pouvez utiliser un des modèles de démarrage rapide de hello sur github toodeploy toutes les ressources requises. modèle de Hello déploie les machines virtuelles de hello, équilibrage de charge hello, haute disponibilité etc.. Suivez ces modèles de hello toodeploy comme suit :

1. Ouvrez hello [modèle de base de données] [ template-multisid-db] ou hello [convergé modèle] [ template-converged] sur hello Azure Portal modèle de base de données hello crée uniquement hello règles d’équilibrage de charge pour une base de données alors que le modèle de convergé hello crée également hello règles d’équilibrage de charge pour un ASCS/SCS et une instance ERS (Linux uniquement). Si vous prévoyez d’un système SAP NetWeaver en fonction de tooinstall et que vous souhaitez également tooinstall hello ASCS/SCS d’instance sur hello mêmes ordinateurs, utilisez hello [convergé modèle][template-converged].
1. Entrez les paramètres suivants de hello
    1. ID du système SAP  
       Entrez le système hello SAP Id Hello système SAP tooinstall. Hello Id sera utilisé en tant que préfixe pour les ressources hello qui sont déployés.
    1. Type de la pile (applicable uniquement si vous utilisez le modèle de convergé hello)  
       Sélectionnez le type de pile hello SAP NetWeaver
    1. Type de système d’exploitation  
       Sélectionnez une des distributions de Linux hello. Dans cet exemple, sélectionnez SLES 12 BYOS
    1. Type de base de données  
       Sélectionnez HANA
    1. Taille du système SAP  
       quantité Hello du nouveau système SAP hello fournissent. Si vous n’êtes pas sûr du système de hello SAP combien nécessitera, veuillez demander à votre partenaire technologique SAP ou l’intégrateur système
    1. Disponibilité du système  
       Sélectionnez la haute disponibilité (HA).
    1. Nom d’utilisateur et mot de passe d’administrateur  
       Création d’un utilisateur qui peut être utilisé toolog sur l’ordinateur de toohello.
    1. Sous-réseau nouveau ou existant  
       Détermine s’il faut créer un réseau virtuel et un sous-réseau, ou utiliser un sous-réseau existant. Si vous disposez déjà d’un réseau virtuel qui est le réseau local de tooyour connecté, sélectionnez existante.
    1. ID du sous-réseau  
    ID de Hello d’ordinateurs virtuels hello sous-réseau toowhich hello doit être connecté à. Sélectionnez sous-réseau hello de votre VPN ou Express Route réseau virtuel tooconnect hello tooyour local réseau d’ordinateurs virtuels. ID de Hello ressemble généralement à /subscriptions/`<subscription id`> /resourceGroups/`<resource group name`> /providers/Microsoft.Network/virtualNetworks/`<virtual network name`> /subnets/`<subnet name`>

## <a name="setting-up-linux-ha"></a>Configuration de la haute disponibilité Linux

Hello éléments suivants est préfixé avec l’option [A] - les nœuds tooall applicable, [1] - applicable uniquement toonode 1 ou [2] - le toonode s’applique seulement 2.

1. [A] SLES pour SAP BYOS uniquement - inscrire les SLES toobe toouse en mesure de hello des référentiels
1. [A] SLES for SAP BYOS uniquement : ajouter un module de cloud public
1. [A] Mettre à jour SLES
    ```bash
    sudo zypper update

    ```

1. [1] Activer l’accès SSH
    ```bash
    sudo ssh-keygen -tdsa
    
    # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy hello public key
    sudo cat /root/.ssh/id_dsa.pub
    ```

2. [2] Activer l’accès SSH
    ```bash
    sudo ssh-keygen -tdsa

    # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
    sudo vi /root/.ssh/authorized_keys
    
    # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy hello public key    
    sudo cat /root/.ssh/id_dsa.pub
    ```

1. [1] Activer l’accès SSH
    ```bash
    # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
    sudo vi /root/.ssh/authorized_keys
    
    ```

1. [A] installer l’extension de haute disponibilité
    ```bash
    sudo zypper install sle-ha-release fence-agents
    
    ```

1. [A] Configurer la disposition du disque
    1. LVM  
    Nous déconseillons généralement de toouse Gestionnaire de volume logique pour les volumes qui stockent les données et fichiers journaux. exemple Hello ci-dessous suppose que les ordinateurs virtuels hello avez quatre disques de données attachés doivent être utilisé toocreate deux volumes.
        * Créer des volumes physiques de tous les disques que vous souhaitez toouse.
    <pre><code>
    sudo pvcreate /dev/sdc
    sudo pvcreate /dev/sdd
    sudo pvcreate /dev/sde
    sudo pvcreate /dev/sdf
    </code></pre>
        * Créer un groupe de volumes pour les fichiers de données hello, un groupe de volumes pour les fichiers de journaux hello et un pour le répertoire partagé de hello de SAP HANA
    <pre><code>
    sudo vgcreate vg_hana_data /dev/sdc /dev/sdd
    sudo vgcreate vg_hana_log /dev/sde
    sudo vgcreate vg_hana_shared /dev/sdf
    </code></pre>
        * Créer des volumes logiques hello
    <pre><code>
    sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
    sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
    sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
    sudo mkfs.xfs /dev/vg_hana_data/hana_data
    sudo mkfs.xfs /dev/vg_hana_log/hana_log
    sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
    </code></pre>
        * Créer des répertoires de montage hello et copiez hello UUID de tous les volumes logiques
    <pre><code>
    sudo mkdir -p /hana/data
    sudo mkdir -p /hana/log
    sudo mkdir -p /hana/shared
    # write down hello id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
    sudo blkid
    </code></pre>
        * Créer des volumes logiques trois entrées fstab pour hello
    <pre><code>
    sudo vi /etc/fstab
    </code></pre>
    Insérer cette ligne trop/etc/fstab
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b> /hana/data xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b> /hana/log xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b> /hana/shared xfs  defaults,nofail  0  2
    </code></pre>
        * Monter des volumes de nouveau hello
    <pre><code>
    sudo mount -a
    </code></pre>
    1. Disques simples  
       Pour les petits systèmes ou les systèmes de démonstration, vous pouvez placer vos données et fichiers journaux HANA sur un disque. Hello commandes suivantes créent une partition sur /dev/sdc puis formater xfs.
    ```bash
    sudo fdisk /dev/sdc
    sudo mkfs.xfs /dev/sdc1
    
    # <a name="write-down-hello-id-of-devsdc1"></a>Notez les id hello de /dev/sdc1
    sudo /sbin/blkid  sudo vi /etc/fstab
    ```

    Insert this line too/etc/fstab
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID&gt;</b> /hana xfs  defaults,nofail  0  2
    </code></pre>

    Create hello target directory and mount hello disk.

    ```bash
    sudo mkdir /hana
    sudo mount -a
    ```

1. [A] Configurer la résolution de nom d’hôte pour tous les hôtes  
    Vous pouvez utiliser un serveur DNS ou modifier/etc/hosts de hello sur tous les nœuds. Cet exemple montre comment toouse hello les fichier/etc/hosts.
   Remplacez l’adresse IP de hello et un nom d’hôte hello Bonjour suivant les commandes
    ```bash
    sudo vi /etc/hosts
    ```
    Insérez hello suivant lignes trop/etc/hosts. Modifiez les toomatch hello IP adresse et le nom d’hôte de votre environnement    
    
    <pre><code>
    <b>&lt;IP address of host 1&gt; &lt;hostname of host 1&gt;</b>
    <b>&lt;IP address of host 2&gt; &lt;hostname of host 2&gt;</b>
    </code></pre>

1. [1] Installer le cluster
    ```bash
    sudo ha-cluster-init
    
    # Do you want toocontinue anyway? [y/N] -> y
    # Network address toobind too(e.g.: 192.168.1.0) [10.79.227.0] -> ENTER
    # Multicast address (e.g.: 239.x.x.x) [239.174.218.125] -> ENTER
    # Multicast port [5405] -> ENTER
    # Do you wish toouse SBD? [y/N] -> N
    # Do you wish tooconfigure an administration IP? [y/N] -> N
    ```
        
1. [2] Ajout de nœud toocluster
    ```bash
    sudo ha-cluster-join
        
    # WARNING: NTP is not configured toostart at system boot.
    # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
    # Do you want toocontinue anyway? [y/N] -> y
    # IP address or hostname of existing node (e.g.: 192.168.1.1) [] -> IP address of node 1 e.g. 10.0.0.5
    # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
    ```

1. [A] toohello de mot de passe de modification hacluster même mot de passe
    ```bash
    sudo passwd hacluster
    
    ```

1. [A] configurer corosync toouse autre transport et ajouter la liste de nœuds. Le cluster ne fonctionnera pas dans le cas contraire.
    ```bash
    sudo vi /etc/corosync/corosync.conf    
    
    ```

    Ajoutez hello toohello contenu gras le fichier suivant.
    
    <pre><code> 
    [...]
      interface { 
          [...] 
      }
      <b>transport:      udpu</b>
    } 
    <b>nodelist {
      node {
        ring0_addr:     < ip address of node 1 >
      }
      node {
        ring0_addr:     < ip address of node 2 > 
      } 
    }</b>
    logging {
      [...]
    </code></pre>

    Ensuite, redémarrez le service corosync hello

    ```bash
    sudo service corosync restart
    
    ```

1. [A] Installer les packages haute disponibilité HANA  
    ```bash
    sudo zypper install SAPHanaSR
    
    ```

## <a name="installing-sap-hana"></a>Installation de SAP HANA

Chapitre 4 Hello [SAP HANA SR performances optimisées Scenario guide] [ suse-hana-ha-guide] tooinstall réplication du système SAP HANA.

1. [A] exécuter hdblcm à partir de hello HANA DVD
    * Choose installation -> 1
    * Select additional components for installation -> 1
    * Enter Installation Path [/hana/shared]: -> ENTRÉE
    * Enter Local Host Name [..]: -> ENTRÉE
    * Voulez-vous que le système de toohello tooadd hôtes supplémentaires ? (y/n) [n] : -> ENTRÉE
    * Enter SAP HANA System ID : <SID of HANA e.g. HDB>
    * Enter Instance Number [00] :   
  Numéro d’instance HANA. Utilisée 03 utilisé hello modèle Azure ou pour suivre l’exemple hello ci-dessus
    * Select Database Mode / Enter Index [1] : -> ENTRÉE
    * Select System Usage / Enter Index [4] :  
  Sélectionnez le système hello d’utilisation
    * Enter Location of Data Volumes [/hana/data/HDB] : -> ENTRÉE
    * Enter Location of Log Volumes [/hana/log/HDB] : -> ENTRÉE
    * Restrict maximum memory allocation? [n] : -> ENTRÉE
    * Entrez le nom d’hôte de certificat pour l’hôte '...' [...] : -> Entrée
    * Enter SAP Host Agent User (sapadm) Password:
    * Confirm SAP Host Agent User (sapadm) Password:
    * Enter System Administrator (hdbadm) Password:
    * Confirm System Administrator (hdbadm) Password:
    * Enter System Administrator Home Directory [/usr/sap/HDB/home] : -> ENTRÉE
    * Enter System Administrator Login Shell [/bin/sh] : -> ENTRÉE
    * Enter System Administrator User ID [1001] : -> ENTRÉE
    * Enter ID of User Group (sapsys) [79] : -> ENTRÉE
    * Enter Database User (SYSTEM) Password:
    * Confirm Database User (SYSTEM) Password:
    * Restart system after machine reboot? [n] : -> ENTRÉE
    * Voulez-vous toocontinue ? (y/n) :  
  Valider hello résumé et entrez y toocontinue
1. [A] Mettre à niveau l’agent hôte SAP  
  Télécharger des archives de l’Agent hôte SAP hello plus récente à partir de hello [SAP Softwarecenter] [ sap-swcenter] et exécution hello après la commande tooupgrade hello agent. Remplacez hello chemin d’accès toohello toopoint toohello fichier d’archive que vous avez téléchargé.
    ```bash
    sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <path tooSAP Host Agent SAR>
    ```

1. [1] Créer la réplication HANA (en tant que root)  
    Exécutez hello commande suivante. Assurez-vous que tooreplace chaînes en gras (HANA système ID HDB et numéro d’instance 03) avec des valeurs de votre installation de SAP HANA hello.
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
    hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN too<b>hdb</b>hasync' 
    hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
    </code></pre>

1. [A] Créer l’entrée keystore (en tout que root)
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>passwd</b>
    </code></pre>
1. [1] Sauvegarder la base de données (en tant que root)
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
    </code></pre>
1. [1] commutateur toohello sapsid utilisateur (par exemple hdbadm) et créer un site principal de hello.
    <pre><code>
    su - <b>hdb</b>adm
    hdbnsutil -sr_enable –-name=<b>SITE1</b>
    </code></pre>
1. [2] commutateur toohello sapsid utilisateur (par exemple hdbadm) et créer un site secondaire de hello.
    <pre><code>
    su - <b>hdb</b>adm
    sapcontrol -nr <b>03</b> -function StopWait 600 10
    hdbnsutil -sr_register --remoteHost=<b>saphanavm1</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
    </code></pre>

## <a name="configure-cluster-framework"></a>Configurer le framework du cluster

Modifier les paramètres par défaut hello

<pre>
sudo vi crm-defaults.txt
# enter hello following toocrm-defaults.txt
<code>
property $id="cib-bootstrap-options" \
  no-quorum-policy="ignore" \
  stonith-enabled="true" \
  stonith-action="reboot" \
  stonith-timeout="150s"
rsc_defaults $id="rsc-options" \
  resource-stickiness="1000" \
  migration-threshold="5000"
op_defaults $id="op-options" \
  timeout="600"
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a>maintenant que nous charger toohello de fichiers hello
sudo crm configure load update crm-defaults.txt
</pre>

### <a name="create-stonith-device"></a>Créer l’appareil STONITH

APPAREIL STONITH Hello utilise un tooauthorize de Principal du Service par rapport à Microsoft Azure. Suivez ces étapes de toocreate un Principal de Service.

1. Accédez trop<https://portal.azure.com>
1. Panneau d’Azure Active Directory hello ouvert  
   Accédez tooProperties et écrivez hello ID de répertoire. Il s’agit de hello **id client**.
1. Cliquez sur Inscriptions d’applications
1. Cliquez sur Ajouter.
1. Entrez un nom, sélectionnez le type d’application « Application web/API », entrez une URL de connexion (par exemple, http://localhost) et cliquez sur Créer
1. URL de connexion Hello n’est pas utilisé et peut être une URL valide
1. Sélectionnez hello nouvelle application et cliquez sur les clés dans l’onglet Paramètres de hello
1. Entrez une description pour la nouvelle clé, sélectionnez « N’expire jamais » et cliquez sur Enregistrer
1. Écrivez hello valeur. Il est utilisé comme hello **mot de passe** pour hello Principal du Service
1. Écrivez hello ID d’Application. Il est utilisé comme nom d’utilisateur de hello (**id de connexion** dans suit hello) de hello Principal du Service

Hello Principal du Service n’a pas les autorisations tooaccess vos ressources Azure par défaut. Vous devez toostart d’autorisations toogive hello Principal du Service et arrêter (désallouer) tous les ordinateurs virtuels du cluster de hello.

1. Accédez toohttps://portal.azure.com
1. Ouvrez hello toutes les lames de ressources
1. Sélectionnez l’ordinateur virtuel de hello
1. Cliquez sur Contrôle d’accès (IAM)
1. Cliquez sur Ajouter.
1. Sélectionnez le rôle hello propriétaire
1. Entrez les nom hello d’application hello créé ci-dessus
1. Cliquez sur OK

Une fois que vous avez modifié les autorisations hello pour les ordinateurs virtuels de hello, vous pouvez configurer les appareils STONITH hello dans un cluster de hello.

<pre>
sudo vi crm-fencing.txt
# enter hello following toocrm-fencing.txt
# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password
<code>
primitive rsc_st_azure_1 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

primitive rsc_st_azure_2 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a>maintenant que nous charger toohello de fichiers hello
sudo crm configure load update crm-fencing.txt
</pre>

### <a name="create-sap-hana-resources"></a>Créer des ressources SAP HANA

<pre>
sudo vi crm-saphanatop.txt
# enter hello following toocrm-saphana.txt
# replace hello bold string with your instance number and HANA system id
<code>
primitive rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHanaTopology \
    operations $id="rsc_sap2_<b>HDB</b>_HDB<b>03</b>-operations" \
    op monitor interval="10" timeout="600" \
    op start interval="0" timeout="600" \
    op stop interval="0" timeout="300" \
    params SID="<b>HDB</b>" InstanceNumber="<b>03</b>"

clone cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \
    meta is-managed="true" clone-node-max="1" target-role="Started" interleave="true"
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a>maintenant que nous charger toohello de fichiers hello
sudo crm configure load update crm-saphanatop.txt
</pre>

<pre>
sudo vi crm-saphana.txt
# enter hello following toocrm-saphana.txt
# replace hello bold string with your instance number, HANA system id and hello frontend IP address of hello Azure load balancer. 
<code>
primitive rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHana \
    operations $id="rsc_sap_<b>HDB</b>_HDB<b>03</b>-operations" \
    op start interval="0" timeout="3600" \
    op stop interval="0" timeout="3600" \
    op promote interval="0" timeout="3600" \
    op monitor interval="60" role="Master" timeout="700" \
    op monitor interval="61" role="Slave" timeout="700" \
    params SID="<b>HDB</b>" InstanceNumber="<b>03</b>" PREFER_SITE_TAKEOVER="true" \
    DUPLICATE_PRIMARY_TIMEOUT="7200" AUTOMATED_REGISTER="false"

ms msl_SAPHana_<b>HDB</b>_HDB<b>03</b> rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> \
    meta is-managed="true" notify="true" clone-max="2" clone-node-max="1" \
    target-role="Started" interleave="true"

primitive rsc_ip_<b>HDB</b>_HDB<b>03</b> ocf:heartbeat:IPaddr2 \ 
    meta target-role="Started" is-managed="true" \ 
    operations $id="rsc_ip_<b>HDB</b>_HDB<b>03</b>-operations" \ 
    op monitor interval="10s" timeout="20s" \ 
    params ip="<b>10.0.0.21</b>" 
primitive rsc_nc_<b>HDB</b>_HDB<b>03</b> anything \ 
    params binfile="/usr/bin/nc" cmdline_options="-l -k 625<b>03</b>" \ 
    op monitor timeout=20s interval=10 depth=0 
group g_ip_<b>HDB</b>_HDB<b>03</b> rsc_ip_<b>HDB</b>_HDB<b>03</b> rsc_nc_<b>HDB</b>_HDB<b>03</b>
 
colocation col_saphana_ip_<b>HDB</b>_HDB<b>03</b> 2000: g_ip_<b>HDB</b>_HDB<b>03</b>:Started \ 
    msl_SAPHana_<b>HDB</b>_HDB<b>03</b>:Master  
order ord_SAPHana_<b>HDB</b>_HDB<b>03</b> 2000: cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \ 
    msl_SAPHana_<b>HDB</b>_HDB<b>03</b>
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a>maintenant que nous charger toohello de fichiers hello
sudo crm configure load update crm-saphana.txt
</pre>

### <a name="test-cluster-setup"></a>Tester la configuration du cluster
Hello chapitre décrire comment vous pouvez tester votre configuration. Chaque test suppose que vous êtes racine principale de SAP HANA hello s’exécute sur saphanavm1 de machine virtuelle hello.

#### <a name="fencing-test"></a>Test de délimitation

Vous pouvez tester le programme d’installation de hello de l’agent de délimitation hello en désactivant l’interface réseau hello sur saphanavm1 de nœud.

<pre><code>
sudo ifdown eth0
</code></pre>

Hello machine virtuelle doit désormais obtenir redémarré ou arrêté, selon votre configuration de cluster.
Si vous définissez hello stonith-action toooff, hello virtual machine va être arrêté, et les ressources de hello sont migré toohello machine virtuelle en cours d’exécution.

Une fois que vous démarrez à nouveau hello virtual machine, hello ressource de SAP HANA échoue toostart en tant que base de données secondaire si vous définissez AUTOMATED_REGISTER = « false ». Dans ce cas, vous avez besoin d’instance HANA de hello tooconfigure secondaire en exécutant hello de commande suivante :

<pre><code>
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b>

# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-manual-failover"></a>Tester un basculement manuel

Vous pouvez tester un basculement manuel en arrêtant le service de STIMULATEUR hello sur le nœud saphanavm1.
<pre><code>
service pacemaker stop
</code></pre>

Après le basculement de hello, vous pouvez démarrer le service de hello à nouveau. Hello ressources SAP HANA sur saphanavm1 échoue toostart en tant que base de données secondaire si vous définissez AUTOMATED_REGISTER = « false ». Dans ce cas, vous avez besoin d’instance HANA de hello tooconfigure secondaire en exécutant hello de commande suivante :

<pre><code>
service pacemaker start
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 


# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-migration"></a>Tester une migration

Vous pouvez migrer le nœud principal de SAP HANA hello en exécutant hello commande suivante
<pre><code>
crm resource migrate msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
crm resource migrate g_ip_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
</code></pre>

Cette migration nœud maître de SAP HANA hello et groupe hello contenant toosaphanavm2 adresse IP virtuelle de hello.
Hello ressources SAP HANA sur saphanavm1 échoue toostart en tant que base de données secondaire si vous définissez AUTOMATED_REGISTER = « false ». Dans ce cas, vous avez besoin d’instance HANA de hello tooconfigure secondaire en exécutant hello de commande suivante :

<pre><code>
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 
</code></pre>

migration de Hello crée des contraintes d’emplacement qui doivent toobe supprimé à nouveau.

<pre><code>
crm configure edited

# delete location contraints that are named like hello following contraint. You should have two contraints, one for hello SAP HANA resource and one for hello IP address group.
location cli-prefer-g_ip_<b>HDB</b>_HDB<b>03</b> g_ip_<b>HDB</b>_HDB<b>03</b> role=Started inf: <b>saphanavm2</b>
</code></pre>

Vous devez également l’état de hello toocleanup de ressource du nœud secondaire hello

<pre><code>
# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

## <a name="next-steps"></a>Étapes suivantes
* [Planification et implémentation de machines virtuelles Azure pour SAP][planning-guide]
* [Déploiement de machines virtuelles Azure pour SAP][deployment-guide]
* [Déploiement SGBD de machines virtuelles Azure pour SAP][dbms-guide]
* toolearn comment tooestablish haute disponibilité et le plan de récupération d’urgence de SAP HANA sur Azure (instances de grande taille), consultez [SAP HANA (instances de grande taille) haute disponibilité et récupération d’urgence sur Azure](hana-overview-high-availability-disaster-recovery.md). 
