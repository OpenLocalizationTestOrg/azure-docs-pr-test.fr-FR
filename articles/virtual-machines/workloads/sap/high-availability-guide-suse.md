---
title: "aaaAzure Machines virtuelles de haute disponibilité pour SAP NetWeaver sur SUSE Linux Enterprise Server, pour les applications SAP | Documents Microsoft"
description: "Guide de haute disponibilité pour SAP NetWeaver sur SUSE Linux Enterprise Server pour les applications SAP"
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: mssedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 5e514964-c907-4324-b659-16dd825f6f87
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 04/27/2017
ms.author: sedusch
ms.openlocfilehash: e944103df92d5ffec9196189f138e25972bea79f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-for-sap-netweaver-on-azure-vms-on-suse-linux-enterprise-server-for-sap-applications"></a>Haute disponibilité pour SAP NetWeaver sur les machines virtuelles Azure sur SUSE Linux Enterprise Server pour les applications SAP

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
[1410736]:https://launchpad.support.sap.com/#/notes/1410736

[sap-swcenter]:https://support.sap.com/en/my-support/software-downloads.html

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[suse-drbd-guide]:https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha_techguides/book_sleha_techguides.html

[template-multisid-xscs]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs-md%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged-md%2Fazuredeploy.json
[template-file-server]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-file-server-md%2Fazuredeploy.json

[sap-hana-ha]:sap-hana-high-availability.md

Cet article décrit comment les machines virtuelles toodeploy hello, configurer des machines virtuelles de hello, installer hello cluster framework et installer un système SAP NetWeaver 7.50 hautement disponible.
Dans les configurations d’exemple hello, etc. des commandes d’installation. nous utilisons le numéro d’instance ASCS 00, le numéro d’instance ERS 02 et l’ID de système SAP NWS. Hello noms de ressources hello (par exemple les machines virtuelles, les réseaux virtuels) dans l’exemple de hello supposent que vous avez utilisé hello [convergé modèle] [ template-converged] avec les ressources SAP système ID NWS toocreate hello.

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
* [SAP HANA SR Performance Optimized Scenario][suse-hana-ha-guide] (Scénario d’optimisation des performances de réplication système de SAP HANA)  
  guide de Hello contient toutes les informations requises tooset, réplication du système SAP HANA en local. Utilisez ce guide comme référence.
* [Hautement disponible stockage NFS avec DRBD et STIMULATEUR] [ suse-drbd-guide] guide de hello contient toutes les informations requises tooset, d’un serveur NFS à haute disponibilité. Utilisez ce guide comme référence.


## <a name="overview"></a>Vue d'ensemble

tooachieve haute disponibilité, SAP NetWeaver requiert un serveur NFS. serveur NFS de Hello est configuré dans un cluster distinct et peut être utilisé par plusieurs systèmes SAP.

![Vue d’ensemble de la haute disponibilité SAP NetWeaver](./media/high-availability-guide-suse/img_001.png)

Hello serveur NFS, SAP NetWeaver ASC, SAP NetWeaver SCS, SAP NetWeaver ERS et base de données SAP HANA hello utiliser le nom d’hôte virtuel et les adresses IP virtuelles. Sur Azure, un équilibreur de charge est requis toouse une adresse IP virtuelle. Hello liste suivante présente configuration hello d’équilibrage de charge hello.

### <a name="nfs-server"></a>Serveur NFS
* Configuration du frontend
  * Adresse IP 10.0.0.4
* Configuration du backend
  * Connecté tooprimary les interfaces de réseau de tous les ordinateurs virtuels qui doivent faire partie du cluster NFS hello
* Port de la sonde
  * Port 61000
* Règles d’équilibrage de charge
  * TCP 2049 
  * UDP 2049

### <a name="ascs"></a>(A)SCS
* Configuration du frontend
  * Adresse IP 10.0.0.10
* Configuration du backend
  * Interfaces de réseau connecté tooprimary de tous les ordinateurs virtuels qui doivent faire partie du cluster SCS/ERS hello (A)
* Port de la sonde
  * Port 620**&lt;nr&gt;**
* Règles d’équilibrage de charge
  * TCP 32**&lt;nr&gt;**
  * TCP 36**&lt;nr&gt;**
  * TCP 39**&lt;nr&gt;**
  * TCP 81**&lt;nr&gt;**
  * TCP 5**&lt;nr&gt;**13
  * TCP 5**&lt;nr&gt;**14
  * TCP 5**&lt;nr&gt;**16

### <a name="ers"></a>ERS
* Configuration du frontend
  * Adresse IP 10.0.0.11
* Configuration du backend
  * Interfaces de réseau connecté tooprimary de tous les ordinateurs virtuels qui doivent faire partie du cluster SCS/ERS hello (A)
* Port de la sonde
  * Port 621**&lt;nr&gt;**
* Règles d’équilibrage de charge
  * TCP 33**&lt;nr&gt;**
  * TCP 5**&lt;nr&gt;**13
  * TCP 5**&lt;nr&gt;**14
  * TCP 5**&lt;nr&gt;**16

### <a name="sap-hana"></a>SAP HANA
* Configuration du frontend
  * Adresse IP 10.0.0.12
* Configuration du backend
  * Connecté tooprimary les interfaces de réseau de tous les ordinateurs virtuels qui doivent faire partie du cluster HANA hello
* Port de la sonde
  * Port 625**&lt;nr&gt;**
* Règles d’équilibrage de charge
  * TCP 3**&lt;nr&gt;**15
  * TCP 3**&lt;nr&gt;**17

## <a name="setting-up-a-highly-available-nfs-server"></a>Configuration d’un serveur NFS à haute disponibilité

### <a name="deploying-linux"></a>Déploiement de Linux

Bonjour Azure Marketplace contient une image pour SUSE Linux Enterprise Server 12 d’Applications SAP que vous pouvez utiliser les nouveaux ordinateurs virtuels de toodeploy.
Vous pouvez utiliser un des modèles de démarrage rapide de hello sur github toodeploy toutes les ressources requises. modèle de Hello déploie les machines virtuelles de hello, équilibrage de charge hello, haute disponibilité etc.. Suivez ces modèles de hello toodeploy comme suit :

1. Ouvrez hello [modèle de serveur de fichiers SAP] [ template-file-server] Bonjour portail Azure   
1. Entrez les paramètres suivants de hello
   1. Préfixe de ressource  
      Entrez le préfixe hello toouse. valeur de Hello est utilisé en tant que préfixe pour les ressources hello qui sont déployés.
   2. Type de système d’exploitation  
      Sélectionnez une des distributions de Linux hello. Dans cet exemple, sélectionnez SLES 12.
   3. Nom d’utilisateur et mot de passe d’administrateur  
      Création d’un utilisateur qui peut être utilisé toolog sur l’ordinateur de toohello.
   4. ID du sous-réseau  
      ID de Hello d’ordinateurs virtuels hello sous-réseau toowhich hello doit être connecté à. Laissez vide si vous voulez toocreate un nouveau réseau virtuel ou sélectionnez sous-réseau hello de votre VPN ou Express Route réseau virtuel tooconnect hello tooyour local réseau d’ordinateurs virtuels. ID de Hello ressemble généralement à /subscriptions/**&lt;id d’abonnement&gt;**/resourceGroups/**&lt;nom de groupe de ressources&gt;**/providers/ Microsoft.Network/virtualNetworks/**&lt;nom de réseau virtuel&gt;**/subnets/**&lt;nom de sous-réseau&gt;**

### <a name="installation"></a>Installation

Hello éléments suivants portent le préfixe soit **[A]** -tooall applicable nœuds, **[1]** -uniquement applicable toonode 1 ou **[2]** -uniquement applicable toonode 2.

1. **[A]** Mettre à jour SLES

   <pre><code>
   sudo zypper update
   </code></pre>

1. **[1]** Activer l’accès SSH

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. **[2**] Activer l’accès SSH

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. **[1]** Activer l’accès SSH

   <pre><code>
   # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. **[A]** Installer l’extension de haute disponibilité
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. **[A]** Configurer la résolution de nom d’hôte   

   Vous pouvez utiliser un serveur DNS ou modifier/etc/hosts de hello sur tous les nœuds. Cet exemple montre comment toouse hello les fichier/etc/hosts.
   Remplacez l’adresse IP de hello et un nom d’hôte hello Bonjour suivant les commandes

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   Insérez hello suivant lignes trop/etc/hosts. Modifiez les toomatch hello IP adresse et le nom d’hôte de votre environnement   
   
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   </code></pre>

1. **[1]** Installer le cluster
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want toocontinue anyway? [y/N] -> y
   # Network address toobind too(for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish toouse SBD? [y/N] -> N
   # Do you wish tooconfigure an administration IP? [y/N] -> N
   </code></pre>

1. **[2]**  Ajouter toocluster de nœud
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured toostart at system boot.
   # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
   # Do you want toocontinue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. **[A]**  Toohello de mot de passe de modification hacluster même mot de passe

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. **[A]**  Configurer corosync toouse autre transport et ajouter la liste de nœuds. Le cluster ne fonctionnera pas dans le cas contraire.
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

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
      # IP address of <b>prod-nfs-0</b>
      ring0_addr:10.0.0.5
     }
     node {
      # IP address of <b>prod-nfs-1</b>
      ring0_addr:10.0.0.6
     } 
   }</b>
   logging {
     [...]
   </code></pre>

   Ensuite, redémarrez le service corosync hello

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. **[A]** Installer les composants drbd

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. **[A]**  Créer une partition pour appareil de drbd hello

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. **[A]** Créer des configurations LVM

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_NFS /dev/sdc1
   sudo lvcreate -l 100%FREE -n <b>NWS</b> vg_NFS
   </code></pre>

1. **[A]**  Dispositif de drbd créer hello NFS

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_nfs.res
   </code></pre>

   Insérer configuration hello pour le nouveau périphérique de drbd hello et quitter

   <pre><code>
   resource <b>NWS</b>_nfs {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>prod-nfs-0</b> {
         address   <b>10.0.0.5</b>:7790;
         device    /dev/drbd0;
         disk      /dev/vg_NFS/NWS;
         meta-disk internal;
      }
      on <b>prod-nfs-1</b> {
         address   <b>10.0.0.6</b>:7790;
         device    /dev/drbd0;
         disk      /dev/vg_NFS/NWS;
         meta-disk internal;
      }
   }
   </code></pre>

   Créer un appareil drbd hello et démarrez-le

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_nfs
   sudo drbdadm up <b>NWS</b>_nfs
   </code></pre>

1. **[1]** Ignorer la synchronisation initiale

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_nfs
   </code></pre>

1. **[1]**  Nœud principal de l’ensemble hello

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_nfs
   </code></pre>

1. **[1]**  Patienter jusqu'à ce que les nouveaux appareils de drbd hello sont synchronisés

   <pre><code>
   sudo cat /proc/drbd

   # version: 8.4.6 (api:1/proto:86-101)
   # GIT-hash: 833d830e0152d1e457fa7856e71e11248ccf3f70 build by abuild@sheep14, 2016-05-09 23:14:56
   # 0: cs:Connected ro:Primary/Secondary ds:UpToDate/UpToDate C r-----
   #    ns:0 nr:0 dw:0 dr:912 al:8 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   </code></pre>

1. **[1]**  Créer des systèmes de fichiers sur hello drbd périphériques

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   </code></pre>


### <a name="configure-cluster-framework"></a>Configurer le framework du cluster

1. **[1]**  Modifier les paramètres par défaut de hello

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. **[1]**  Configuration du cluster ajouter hello NFS drbd périphérique toohello

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_nfs \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_nfs" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_nfs drbd_<b>NWS</b>_nfs \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true" interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. **[1]**  Du serveur NFS hello créer

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive nfsserver \
     systemd:nfs-server \
     op monitor interval="30s"

   crm(live)configure# clone cl-nfsserver nfsserver interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. **[1]**  Créer des ressources de système de fichiers NFS hello

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive fs_<b>NWS</b>_sapmnt \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd0 \
     directory=/srv/nfs/<b>NWS</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# group g-<b>NWS</b>_nfs fs_<b>NWS</b>_sapmnt

   crm(live)configure# order o-<b>NWS</b>_drbd_before_nfs inf: \
     ms-drbd_<b>NWS</b>_nfs:promote g-<b>NWS</b>_nfs:start
   
   crm(live)configure# colocation col-<b>NWS</b>_nfs_on_drbd inf: \
     g-<b>NWS</b>_nfs ms-drbd_<b>NWS</b>_nfs:Master

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. **[1]**  Créer hello NFS exports

   <pre><code>
   sudo mkdir /srv/nfs/<b>NWS</b>/sidsys
   sudo mkdir /srv/nfs/<b>NWS</b>/sapmntsid
   sudo mkdir /srv/nfs/<b>NWS</b>/trans

   sudo crm configure

   crm(live)configure# primitive exportfs_<b>NWS</b> \
     ocf:heartbeat:exportfs \
     params directory="/srv/nfs/<b>NWS</b>" \
     options="rw,no_root_squash" \
     clientspec="*" fsid=0 \
     wait_for_leasetime_on_stop=true \
     op monitor interval="30s"

   crm(live)configure# modgroup g-<b>NWS</b>_nfs add exportfs_<b>NWS</b>

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. **[1]**  Créer une ressource IP virtuel et un contrôle d’intégrité-sonde d’équilibreur de charge interne hello

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive vip_<b>NWS</b>_nfs IPaddr2 \
     params ip=<b>10.0.0.4</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_nfs anything \
     params binfile="/usr/bin/nc" cmdline_options="-l -k 610<b>00</b>" \
     op monitor timeout=20s interval=10 depth=0

   crm(live)configure# modgroup g-<b>NWS</b>_nfs add nc_<b>NWS</b>_nfs
   crm(live)configure# modgroup g-<b>NWS</b>_nfs add vip_<b>NWS</b>_nfs

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

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

#### <a name="1-create-hello-stonith-devices"></a>**[1]**  Créer des unités de STONITH hello

Une fois que vous avez modifié les autorisations hello pour les ordinateurs virtuels de hello, vous pouvez configurer les appareils STONITH hello dans un cluster de hello.

<pre><code>
sudo crm configure

# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-hello-use-of-a-stonith-device"></a>**[1]**  Activer l’utilisation de hello d’un périphérique STONITH

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="setting-up-ascs"></a>Configuration de (A)SCS

### <a name="deploying-linux"></a>Déploiement de Linux

Bonjour Azure Marketplace contient une image pour SUSE Linux Enterprise Server 12 d’Applications SAP que vous pouvez utiliser les nouveaux ordinateurs virtuels de toodeploy. image de marketplace Hello contient un agent de ressource de hello pour SAP NetWeaver.

Vous pouvez utiliser un des modèles de démarrage rapide de hello sur github toodeploy toutes les ressources requises. modèle de Hello déploie les machines virtuelles de hello, équilibrage de charge hello, haute disponibilité etc.. Suivez ces modèles de hello toodeploy comme suit :

1. Ouvrez hello [modèle du SID de multiples ASCS/SCS] [ template-multisid-xscs] ou hello [convergé modèle] [ template-converged] sur le modèle hello Azure hello portail ASCS/SCS uniquement crée des règles de l’équilibrage de charge de hello pour hello SAP NetWeaver ASCS/SCS et les instances ERS (Linux uniquement) alors que le modèle de convergé hello crée également des règles d’équilibrage de charge hello pour une base de données (par exemple Microsoft SQL Server ou SAP HANA). Si vous prévoyez d’un système SAP NetWeaver en fonction de tooinstall et que vous souhaitez également de base de données de tooinstall hello en hello les mêmes ordinateurs, utilisez hello [convergé modèle][template-converged].
1. Entrez les paramètres suivants de hello
   1. Préfixe de ressource (modèle ASCS/SCS Multi SID uniquement)  
      Entrez le préfixe hello toouse. valeur de Hello est utilisé en tant que préfixe pour les ressources hello qui sont déployés.
   3. ID du système SAP (modèle convergé uniquement)  
      Entrez le système hello SAP Id Hello système SAP tooinstall. Hello Id est utilisé en tant que préfixe pour les ressources hello qui sont déployés.
   4. Type de pile  
      Sélectionnez le type de pile hello SAP NetWeaver
   5. Type de système d’exploitation  
      Sélectionnez une des distributions de Linux hello. Dans cet exemple, sélectionnez SLES 12 BYOS
   6. Type de base de données  
      Sélectionnez HANA
   7. Taille du système SAP  
      quantité Hello du nouveau système SAP hello fournit. Si vous n’êtes pas sûr du système de hello combien SAP, veuillez demander à votre partenaire technologique SAP ou l’intégrateur système
   8. Disponibilité du système  
      Sélectionnez la haute disponibilité (HA).
   9. Nom d’utilisateur et mot de passe d’administrateur  
      Création d’un utilisateur qui peut être utilisé toolog sur l’ordinateur de toohello.
   10. ID du sous-réseau  
   ID de Hello d’ordinateurs virtuels hello sous-réseau toowhich hello doit être connecté à.  Laissez vide si vous voulez toocreate un nouveau réseau virtuel ou sélectionnez hello même sous-réseau que vous utilisés ou créés dans le cadre du déploiement de serveur NFS hello. ID de Hello ressemble généralement à /subscriptions/**&lt;id d’abonnement&gt;**/resourceGroups/**&lt;nom de groupe de ressources&gt;**/providers/ Microsoft.Network/virtualNetworks/**&lt;nom de réseau virtuel&gt;**/subnets/**&lt;nom de sous-réseau&gt;**

### <a name="installation"></a>Installation

Hello éléments suivants portent le préfixe soit **[A]** -tooall applicable nœuds, **[1]** -uniquement applicable toonode 1 ou **[2]** -uniquement applicable toonode 2.

1. **[A]** Mettre à jour SLES

   <pre><code>
   sudo zypper update
   </code></pre>

1. **[1]** Activer l’accès SSH

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. **[2**] Activer l’accès SSH

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. **[1]** Activer l’accès SSH

   <pre><code>
   # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. **[A]** Installer l’extension de haute disponibilité
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. **[A]** Mettre à jour les agents de ressources SAP  
   
   Un correctif pour hello agents de la ressource est obligatoire toouse hello nouvelle configuration, qui est décrite dans cet article. Vous pouvez vérifier si hello correctif est déjà installé avec hello commande suivante

   <pre><code>
   sudo grep 'parameter name="IS_ERS"' /usr/lib/ocf/resource.d/heartbeat/SAPInstance
   </code></pre>

   sortie de Hello doit être similaire à

   <pre><code>
   &lt;parameter name="IS_ERS" unique="0" required="0"&gt;
   </code></pre>

   Si la commande grep de hello ne trouve pas de paramètre IS_ERS hello, vous avez besoin de correctifs de hello tooinstall répertoriées sur [hello SUSE page de téléchargement](https://download.suse.com/patch/finder/#bu=suse&familyId=&productId=&dateRange=&startDate=&endDate=&priority=&architecture=&keywords=resource-agents)

   <pre><code>
   # example for patch for SLES 12 SP1
   sudo zypper in -t patch SUSE-SLE-HA-12-SP1-2017-885=1
   # example for patch for SLES 12 SP2
   sudo zypper in -t patch SUSE-SLE-HA-12-SP2-2017-886=1
   </code></pre>

1. **[A]** Configurer la résolution de nom d’hôte   

   Vous pouvez utiliser un serveur DNS ou modifier/etc/hosts de hello sur tous les nœuds. Cet exemple montre comment toouse hello les fichier/etc/hosts.
   Remplacez l’adresse IP de hello et un nom d’hôte hello Bonjour suivant les commandes

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   Insérez hello suivant lignes trop/etc/hosts. Modifiez les toomatch hello IP adresse et le nom d’hôte de votre environnement   
   
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of hello load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   </code></pre>

1. **[1]** Installer le cluster
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want toocontinue anyway? [y/N] -> y
   # Network address toobind too(for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish toouse SBD? [y/N] -> N
   # Do you wish tooconfigure an administration IP? [y/N] -> N
   </code></pre>

1. **[2]**  Ajouter toocluster de nœud
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured toostart at system boot.
   # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
   # Do you want toocontinue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. **[A]**  Toohello de mot de passe de modification hacluster même mot de passe

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. **[A]**  Configurer corosync toouse autre transport et ajouter la liste de nœuds. Le cluster ne fonctionnera pas dans le cas contraire.
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

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
      # IP address of <b>nws-cl-0</b>
      ring0_addr:     10.0.0.14
     }
     node {
      # IP address of <b>nws-cl-1</b>
      ring0_addr:     10.0.0.13
     } 
   }</b>
   logging {
     [...]
   </code></pre>

   Ensuite, redémarrez le service corosync hello

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. **[A]** Installer les composants drbd

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. **[A]**  Créer une partition pour appareil de drbd hello

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. **[A]** Créer des configurations LVM

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_<b>NWS</b> /dev/sdc1
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ASCS vg_<b>NWS</b>
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ERS vg_<b>NWS</b>
   </code></pre>

1. **[A]**  Dispositif de drbd créer hello SCS

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ascs.res
   </code></pre>

   Insérer configuration hello pour le nouveau périphérique de drbd hello et quitter

   <pre><code>
   resource <b>NWS</b>_ascs {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>nws-cl-0</b> {
         address   <b>10.0.0.14</b>:7791;
         device    /dev/drbd0;
         disk      /dev/vg_NWS/NWS_ASCS;
         meta-disk internal;
      }
      on <b>nws-cl-1</b> {
         address   <b>10.0.0.13</b>:7791;
         device    /dev/drbd0;
         disk      /dev/vg_NWS/NWS_ASCS;
         meta-disk internal;
      }
   }
   </code></pre>

   Créer un appareil drbd hello et démarrez-le

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ascs
   sudo drbdadm up <b>NWS</b>_ascs
   </code></pre>

1. **[A]**  Dispositif de drbd créer hello ERS

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ers.res
   </code></pre>

   Insérer configuration hello pour le nouveau périphérique de drbd hello et quitter

   <pre><code>
   resource <b>NWS</b>_ers {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>nws-cl-0</b> {
         address   <b>10.0.0.14</b>:7792;
         device    /dev/drbd1;
         disk      /dev/vg_NWS/NWS_ERS;
         meta-disk internal;
      }
      on <b>nws-cl-1</b> {
         address   <b>10.0.0.13</b>:7792;
         device    /dev/drbd1;
         disk      /dev/vg_NWS/NWS_ERS;
         meta-disk internal;
      }
   }
   </code></pre>

   Créer un appareil drbd hello et démarrez-le

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ers
   sudo drbdadm up <b>NWS</b>_ers
   </code></pre>

1. **[1]** Ignorer la synchronisation initiale

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ascs
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ers
   </code></pre>

1. **[1]**  Nœud principal de l’ensemble hello

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_ascs
   sudo drbdadm primary --force <b>NWS</b>_ers
   </code></pre>

1. **[1]**  Patienter jusqu'à ce que les nouveaux appareils de drbd hello sont synchronisés

   <pre><code>
   sudo cat /proc/drbd

   # version: 8.4.6 (api:1/proto:86-101)
   # GIT-hash: 833d830e0152d1e457fa7856e71e11248ccf3f70 build by abuild@sheep14, 2016-05-09 23:14:56
   # 0: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:93991268 nr:0 dw:93991268 dr:93944920 al:383 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   # 1: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:6047920 nr:0 dw:6047920 dr:6039112 al:34 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   # 2: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:5142732 nr:0 dw:5142732 dr:5133924 al:30 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   </code></pre>

1. **[1]**  Créer des systèmes de fichiers sur hello drbd périphériques

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   sudo mkfs.xfs /dev/drbd1
   </code></pre>


### <a name="configure-cluster-framework"></a>Configurer le framework du cluster

**[1]**  Modifier les paramètres par défaut de hello

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

## <a name="prepare-for-sap-netweaver-installation"></a>Préparer l’installation de SAP NetWeaver

1. **[A]**  Hello de créer les répertoires partagés

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans
   sudo mkdir -p /usr/sap/<b>NWS</b>/SYS

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   sudo chattr +i /usr/sap/<b>NWS</b>/SYS
   </code></pre>

1. **[A]** Configurer autofs
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add hello following line toohello file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   Créer un fichier avec

   <pre><code>
   sudo vi /etc/auto.direct

   # Add hello following lines toohello file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   /usr/sap/<b>NWS</b>/SYS -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sidsys
   </code></pre>

   Redémarrez les nouveaux partages autofs toomount hello

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. **[A]** Configurer le fichier SWAP
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set hello property ResourceDisk.EnableSwap tooy
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set hello size of hello SWAP file with property ResourceDisk.SwapSizeMB
   # hello free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check hello SWAP space with command swapon
   # Size of hello swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   Redémarrez le changement d’hello hello Agent tooactivate

   <pre><code>
   sudo service waagent restart
   </code></pre>

### <a name="installing-sap-netweaver-ascsers"></a>Installation de SAP NetWeaver ASC/ERS

1. **[1]**  Créer une ressource IP virtuel et un contrôle d’intégrité-sonde d’équilibreur de charge interne hello

   <pre><code>
   sudo crm node standby <b>nws-cl-1</b>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_ASCS \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_ascs" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_ASCS drbd_<b>NWS</b>_ASCS \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true"

   crm(live)configure# primitive fs_<b>NWS</b>_ASCS \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd0 \
     directory=/usr/sap/<b>NWS</b>/ASCS<b>00</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# primitive vip_<b>NWS</b>_ASCS IPaddr2 \
     params ip=<b>10.0.0.10</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_ASCS anything \
     params binfile="/usr/bin/nc" cmdline_options="-l -k 620<b>00</b>" \
     op monitor timeout=20s interval=10 depth=0
   
   crm(live)configure# group g-<b>NWS</b>_ASCS nc_<b>NWS</b>_ASCS vip_<b>NWS</b>_ASCS fs_<b>NWS</b>_ASCS \
      meta resource-stickiness=3000

   crm(live)configure# order o-<b>NWS</b>_drbd_before_ASCS inf: \
     ms-drbd_<b>NWS</b>_ASCS:promote g-<b>NWS</b>_ASCS:start
   
   crm(live)configure# colocation col-<b>NWS</b>_ASCS_on_drbd inf: \
     ms-drbd_<b>NWS</b>_ASCS:Master g-<b>NWS</b>_ASCS
   
   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

   Assurez-vous que l’état du cluster hello est OK et que toutes les ressources sont démarrés. Il n’est pas important sur les ressources de hello de nœud sont en cours d’exécution.

   <pre><code>
   sudo crm_mon -r

   # Node nws-cl-1: standby
   # <b>Online: [ nws-cl-0 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      Stopped: [ nws-cl-1 ]
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   </code></pre>

1. **[1]** Installer SAP NetWeaver ASCS  

   Installation de SAP NetWeaver ASC en tant que racine sur hello premier nœud à l’aide d’un nom d’hôte virtuel qui mappe les adresses IP de toohello de configuration de serveur frontal d’équilibrage de charge de hello pour hello ASC par exemple <b>nws-ASC</b>, <b>10.0.0.10</b>et numéro d’instance hello que vous avez utilisé pour la sonde hello d’équilibrage de charge hello, par exemple <b>00</b>.

   Vous pouvez utiliser hello sapinst paramètre SAPINST_REMOTE_ACCESS_USER tooallow un toosapinst de tooconnect utilisateur non racine.

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. **[1]**  Créer une ressource IP virtuel et un contrôle d’intégrité-sonde d’équilibreur de charge interne hello

   <pre><code>
   sudo crm node standby <b>nws-cl-0</b>
   sudo crm node online <b>nws-cl-1</b>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_ERS \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_ers" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_ERS drbd_<b>NWS</b>_ERS \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true"

   crm(live)configure# primitive fs_<b>NWS</b>_ERS \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd1 \
     directory=/usr/sap/<b>NWS</b>/ERS<b>02</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# primitive vip_<b>NWS</b>_ERS IPaddr2 \
     params ip=<b>10.0.0.11</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_ERS anything \
    params binfile="/usr/bin/nc" cmdline_options="-l -k 621<b>02</b>" \
    op monitor timeout=20s interval=10 depth=0

   crm(live)configure# group g-<b>NWS</b>_ERS nc_<b>NWS</b>_ERS vip_<b>NWS</b>_ERS fs_<b>NWS</b>_ERS

   crm(live)configure# order o-<b>NWS</b>_drbd_before_ERS inf: \
     ms-drbd_<b>NWS</b>_ERS:promote g-<b>NWS</b>_ERS:start
   
   crm(live)configure# colocation col-<b>NWS</b>_ERS_on_drbd inf: \
     ms-drbd_<b>NWS</b>_ERS:Master g-<b>NWS</b>_ERS
   
   crm(live)configure# commit
   # WARNING: Resources nc_NWS_ASCS,nc_NWS_ERS,nc_NWS_nfs violate uniqueness for parameter "binfile": "/usr/bin/nc"
   # Do you still want toocommit (y/n)? y

   crm(live)configure# exit
   
   </code></pre>
 
   Assurez-vous que l’état du cluster hello est OK et que toutes les ressources sont démarrés. Il n’est pas important sur les ressources de hello de nœud sont en cours d’exécution.

   <pre><code>
   sudo crm_mon -r

   # Node <b>nws-cl-0: standby</b>
   # <b>Online: [ nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      Stopped: [ nws-cl-0 ]
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      Stopped: [ nws-cl-0 ]
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   </code></pre>

1. **[2]** Installer SAP NetWeaver ERS  

   Installation de SAP NetWeaver ERS en tant que racine sur le nœud de deuxième hello à l’aide d’un nom d’hôte virtuel qui mappe les adresses IP de toohello de configuration de serveur frontal d’équilibrage de charge de hello pour hello ERS par exemple <b>nws-ers</b>, <b>10.0.0.11</b> et le numéro d’instance hello que vous avez utilisé pour la sonde hello d’équilibrage de charge hello, par exemple <b>02</b>.

   Vous pouvez utiliser hello sapinst paramètre SAPINST_REMOTE_ACCESS_USER tooallow un toosapinst de tooconnect utilisateur non racine.

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

   > [!NOTE]
   > Utilisez SWPM SP 20 PL 05 ou ultérieur. Versions inférieures ne définissez pas correctement les autorisations de hello et hello installation échouera.
   > 

1. **[1]**  Adapter hello ASCS/SCS et ERS instance des profils
 
   * Profil ASCS/SCS

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_<b>ASCS00</b>_<b>nws-ascs</b>

   # Change hello restart command tooa start command
   #Restart_Program_01 = local $(_EN) pf=$(_PF)
   Start_Program_01 = local $(_EN) pf=$(_PF)

   # Add hello following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector

   # Add hello keep alive parameter
   enque/encni/set_so_keepalive = true
   </code></pre>

   * Profil ERS

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b>

   # Add hello following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector
   </code></pre>


1. **[A]** Configurer Keep Alive

   communication Hello entre le serveur d’applications SAP NetWeaver hello et hello ASCS/SCS est routée via un équilibrage de charge du logiciel. équilibrage de charge Hello déconnecte les connexions inactives après un délai configurable. tooprevent vous devez tooset un paramètre dans le profil de SAP NetWeaver ASCS/SCS de hello et modifiez les paramètres de système de Linux hello. Pour plus d’informations, consultez la [Note SAP 1410736][1410736].
   
   Hello ASCS/SCS profil paramètre terminer/encni/set_so_keepalive a déjà été ajoutée dans la dernière étape de hello.

   <pre><code> 
   # Change hello Linux system configuration
   sudo sysctl net.ipv4.tcp_keepalive_time=120
   </code></pre>

1. **[A]**  Configurer des utilisateurs SAP hello après l’installation de hello
 
   <pre><code>
   # Add sidadm toohello haclient group
   sudo usermod -aG haclient <b>nws</b>adm   
   </code></pre>

1. **[1]**  Ajouter hello ASC et ERS SAP toohello sapservice fichier services

   Ajouter hello ASC service entrée toohello second nœud et copie hello ERS service toohello premier nœud d’entrée.

   <pre><code>
   cat /usr/sap/sapservices | grep ASCS<b>00</b> | sudo ssh <b>nws-cl-1</b> "cat >>/usr/sap/sapservices"
   sudo ssh <b>nws-cl-1</b> "cat /usr/sap/sapservices" | grep ERS<b>02</b> | sudo tee -a /usr/sap/sapservices
   </code></pre>

1. **[1]**  Créer des ressources de cluster hello SAP

   <pre><code>
   sudo crm configure property maintenance-mode="true"

   sudo crm configure

   crm(live)configure# primitive rsc_sap_<b>NWS</b>_ASCS<b>00</b> SAPInstance \
    operations $id=rsc_sap_<b>NWS</b>_ASCS<b>00</b>-operations \
    op monitor interval=11 timeout=60 on_fail=restart \
    params InstanceName=<b>NWS</b>_ASCS<b>00</b>_<b>nws-ascs</b> START_PROFILE="/sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ASCS<b>00</b>_<b>nws-ascs</b>" \
    AUTOMATIC_RECOVER=false \
    meta resource-stickiness=5000 failure-timeout=60 migration-threshold=1 priority=10

   crm(live)configure# primitive rsc_sap_<b>NWS</b>_ERS<b>02</b> SAPInstance \
    operations $id=rsc_sap_<b>NWS</b>_ERS<b>02</b>-operations \
    op monitor interval=11 timeout=60 on_fail=restart \
    params InstanceName=<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b> START_PROFILE="/sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b>" AUTOMATIC_RECOVER=false IS_ERS=true \
    meta priority=1000

   crm(live)configure# modgroup g-<b>NWS</b>_ASCS add rsc_sap_<b>NWS</b>_ASCS<b>00</b>
   crm(live)configure# modgroup g-<b>NWS</b>_ERS add rsc_sap_<b>NWS</b>_ERS<b>02</b>

   crm(live)configure# colocation col_sap_<b>NWS</b>_no_both -5000: g-<b>NWS</b>_ERS g-<b>NWS</b>_ASCS
   crm(live)configure# location loc_sap_<b>NWS</b>_failover_to_ers rsc_sap_<b>NWS</b>_ASCS<b>00</b> rule 2000: runs_ers_<b>NWS</b> eq 1
   crm(live)configure# order ord_sap_<b>NWS</b>_first_start_ascs Optional: rsc_sap_<b>NWS</b>_ASCS<b>00</b>:start rsc_sap_<b>NWS</b>_ERS<b>02</b>:stop symmetrical=false

   crm(live)configure# commit
   crm(live)configure# exit

   sudo crm configure property maintenance-mode="false"
   sudo crm node online <b>nws-cl-0</b>
   </code></pre>

   Assurez-vous que l’état du cluster hello est OK et que toutes les ressources sont démarrés. Il n’est pas important sur les ressources de hello de nœud sont en cours d’exécution.

   <pre><code>
   sudo crm_mon -r

   # Online: <b>[ nws-cl-0 nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   #      rsc_sap_NWS_ASCS00 (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-0</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      <b>Slaves: [ nws-cl-0 ]</b>
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #      rsc_sap_NWS_ERS02  (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-1</b>
   </code></pre>

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

#### <a name="1-create-hello-stonith-devices"></a>**[1]**  Créer des unités de STONITH hello

Une fois que vous avez modifié les autorisations hello pour les ordinateurs virtuels de hello, vous pouvez configurer les appareils STONITH hello dans un cluster de hello.

<pre><code>
sudo crm configure

# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-hello-use-of-a-stonith-device"></a>**[1]**  Activer l’utilisation de hello d’un périphérique STONITH

Activer l’utilisation de hello d’un périphérique STONITH

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="install-database"></a>Installer la base de données

Dans cet exemple, une réplication du système SAP HANA est installée et configurée. SAP HANA s’exécute dans le même cluster comme hello SAP NetWeaver ASCS/SCS et ERS de hello. Vous pouvez également installer SAP HANA dans un cluster dédié. Consultez [Haute disponibilité de SAP HANA sur des machines virtuelles Azure][sap-hana-ha].

### <a name="prepare-for-sap-hana-installation"></a>Préparer l’installation de SAP HANA

En général, nous recommandons d’utiliser LVM pour les volumes qui stockent des données et des fichiers journaux. À des fins de test, vous pouvez également choisir toostore hello données et le fichier journal directement sur un disque brut.

1. **[A]** LVM  
   exemple Hello ci-dessous suppose que les ordinateurs virtuels hello avez quatre disques de données attachés doivent être utilisé toocreate deux volumes.
   
   Créer des volumes physiques de tous les disques que vous souhaitez toouse.
   
   <pre><code>
   sudo pvcreate /dev/sdd
   sudo pvcreate /dev/sde
   sudo pvcreate /dev/sdf
   sudo pvcreate /dev/sdg
   </code></pre>
   
   Créer un groupe de volumes pour les fichiers de données hello, un groupe de volumes pour les fichiers de journaux hello et un pour le répertoire partagé de hello de SAP HANA
   
   <pre><code>
   sudo vgcreate vg_hana_data /dev/sdd /dev/sde
   sudo vgcreate vg_hana_log /dev/sdf
   sudo vgcreate vg_hana_shared /dev/sdg
   </code></pre>
   
   Créer des volumes logiques hello
   
   <pre><code>
   sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
   sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
   sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
   sudo mkfs.xfs /dev/vg_hana_data/hana_data
   sudo mkfs.xfs /dev/vg_hana_log/hana_log
   sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
   </code></pre>
   
   Créer des répertoires de montage hello et copiez hello UUID de tous les volumes logiques
   
   <pre><code>
   sudo mkdir -p /hana/data
   sudo mkdir -p /hana/log
   sudo mkdir -p /hana/shared
   sudo chattr +i /hana/data
   sudo chattr +i /hana/log
   sudo chattr +i /hana/shared
   # write down hello id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
   sudo blkid
   </code></pre>
   
   Créer des volumes logiques trois entrées autofs pour hello
   
   <pre><code>
   sudo vi /etc/auto.direct
   </code></pre>
   
   Insérer cette ligne toosudo vi /etc/auto.direct
   
   <pre><code>
   /hana/data -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b>
   /hana/log -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b>
   /hana/shared -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b>
   </code></pre>
   
   Monter des volumes de nouveau hello
   
   <pre><code>
   sudo service autofs restart 
   </code></pre>

1. **[A]** Disques simples  

   Pour les petits systèmes ou les systèmes de démonstration, vous pouvez placer vos données et fichiers journaux HANA sur un disque. Hello commandes suivantes créent une partition sur /dev/sdc puis formater xfs.
   ```bash
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdd'
   sudo mkfs.xfs /dev/sdd1
   
   # write down hello id of /dev/sdd1
   sudo /sbin/blkid
   sudo vi /etc/auto.direct
   ```
   
   Insérer cette ligne de too/etc/auto.direct
   <pre><code>
   /hana -fstype=xfs :UUID=<b>&lt;UUID&gt;</b>
   </code></pre>
   
   Créer le répertoire cible de hello et monter le disque de hello.
   
   <pre><code>
   sudo mkdir /hana
   sudo chattr +i /hana
   sudo service autofs restart
   </code></pre>

### <a name="installing-sap-hana"></a>Installation de SAP HANA

étapes suivantes Hello sont basées sur le chapitre 4 Hello [SAP HANA SR performances optimisées Scenario guide] [ suse-hana-ha-guide] tooinstall réplication du système SAP HANA. Veuillez lire avant de poursuivre hello.

1. **[A]**  Exécuter hdblcm à partir de hello HANA DVD
   
   <pre><code>
   sudo hdblcm --sid=<b>HDB</b> --number=<b>03</b> --action=install --batch --password=<b>&lt;password&gt;</b> --system_user_password=<b>&lt;password for system user&gt;</b>

   sudo /hana/shared/<b>HDB</b>/hdblcm/hdblcm --action=configure_internal_network --listen_interface=internal --internal_network=<b>10.0.0/24</b> --password=<b>&lt;password for system user&gt;</b> --batch
   </code></pre>

1. **[A]** Mettre à niveau l’agent hôte SAP

   Télécharger des archives de l’Agent hôte SAP hello plus récente à partir de hello [SAP Softwarecenter] [ sap-swcenter] et exécution hello après la commande tooupgrade hello agent. Remplacez hello chemin d’accès toohello toopoint toohello fichier d’archive que vous avez téléchargé.
   <pre><code>
   sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <b>&lt;path tooSAP Host Agent SAR&gt;</b> 
   </code></pre>

1. **[1]** Créer la réplication HANA (en tant que racine)  

   Exécutez hello commande suivante. Assurez-vous que tooreplace chaînes en gras (HANA système ID HDB et numéro d’instance 03) avec des valeurs de votre installation de SAP HANA hello.
   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
   hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN too<b>hdb</b>hasync' 
   hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
   </code></pre>

1. **[A]** Créer l’entrée keystore (en tant que racine)

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>&lt;passwd&gt;</b>
   </code></pre>

1. **[1]** Sauvegarder la base de données (en tant que racine)

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
   </code></pre>

1. **[1]**  Permuter toohello HANA sapsid utilisateur et créer un site principal de hello.

   <pre><code>
   su - <b>hdb</b>adm
   hdbnsutil -sr_enable –-name=<b>SITE1</b>
   </code></pre>

1. **[2]**  Permuter toohello HANA sapsid utilisateur et créer un site secondaire de hello.

   <pre><code>
   su - <b>hdb</b>adm
   sapcontrol -nr <b>03</b> -function StopWait 600 10
   hdbnsutil -sr_register --remoteHost=<b>nws-cl-0</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
   </code></pre>

1. **[1]** Créer les ressources de cluster SAP HANA

   Commencez par créer la topologie de hello.
   
   <pre><code>
   sudo crm configure

   # replace hello bold string with your instance number and HANA system id
   
   crm(live)configure# primitive rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b>   ocf:suse:SAPHanaTopology \
     operations $id="rsc_sap2_<b>HDB</b>_HDB<b>03</b>-operations" \
     op monitor interval="10" timeout="600" \
     op start interval="0" timeout="600" \
     op stop interval="0" timeout="300" \
     params SID="<b>HDB</b>" InstanceNumber="<b>03</b>"
    
   crm(live)configure# clone cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \
     meta is-managed="true" clone-node-max="1" target-role="Started" interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>
   
   Créez ensuite les ressources HANA hello
   
   <pre><code>
   sudo crm configure

   # replace hello bold string with your instance number, HANA system id and hello frontend IP address of hello Azure load balancer. 
    
   crm(live)configure# primitive rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHana \
     operations $id="rsc_sap_<b>HDB</b>_HDB<b>03</b>-operations" \
     op start interval="0" timeout="3600" \
     op stop interval="0" timeout="3600" \
     op promote interval="0" timeout="3600" \
     op monitor interval="60" role="Master" timeout="700" \
     op monitor interval="61" role="Slave" timeout="700" \
     params SID="<b>HDB</b>" InstanceNumber="<b>03</b>" PREFER_SITE_TAKEOVER="true" \
     DUPLICATE_PRIMARY_TIMEOUT="7200" AUTOMATED_REGISTER="false"
    
   crm(live)configure# ms msl_SAPHana_<b>HDB</b>_HDB<b>03</b> rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> \
     meta is-managed="true" notify="true" clone-max="2" clone-node-max="1" \
     target-role="Started" interleave="true"
    
   crm(live)configure# primitive rsc_ip_<b>HDB</b>_HDB<b>03</b> ocf:heartbeat:IPaddr2 \ 
     meta target-role="Started" is-managed="true" \ 
     operations $id="rsc_ip_<b>HDB</b>_HDB<b>03</b>-operations" \ 
     op monitor interval="10s" timeout="20s" \ 
     params ip="<b>10.0.0.12</b>" 

   crm(live)configure# primitive rsc_nc_<b>HDB</b>_HDB<b>03</b> anything \ 
     params binfile="/usr/bin/nc" cmdline_options="-l -k 625<b>03</b>" \ 
     op monitor timeout=20s interval=10 depth=0 

   crm(live)configure# group g_ip_<b>HDB</b>_HDB<b>03</b> rsc_ip_<b>HDB</b>_HDB<b>03</b> rsc_nc_<b>HDB</b>_HDB<b>03</b>
    
   crm(live)configure# colocation col_saphana_ip_<b>HDB</b>_HDB<b>03</b> 2000: g_ip_<b>HDB</b>_HDB<b>03</b>:Started \ 
     msl_SAPHana_<b>HDB</b>_HDB<b>03</b>:Master  

   crm(live)configure# order ord_SAPHana_<b>HDB</b>_HDB<b>03</b> 2000: cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \ 
     msl_SAPHana_<b>HDB</b>_HDB<b>03</b>
    
   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

   Assurez-vous que l’état du cluster hello est OK et que toutes les ressources sont démarrés. Il n’est pas important sur les ressources de hello de nœud sont en cours d’exécution.

   <pre><code>
   sudo crm_mon -r

   # <b>Online: [ nws-cl-0 nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      <b>Slaves: [ nws-cl-0 ]</b>
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #      rsc_sap_NWS_ASCS00 (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-1</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   #      rsc_sap_NWS_ERS02  (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-0</b>
   #  Clone Set: cln_SAPHanaTopology_HDB_HDB03 [rsc_SAPHanaTopology_HDB_HDB03]
   #      <b>Started: [ nws-cl-0 nws-cl-1 ]</b>
   #  Master/Slave Set: msl_SAPHana_HDB_HDB03 [rsc_SAPHana_HDB_HDB03]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g_ip_HDB_HDB03
   #      rsc_ip_HDB_HDB03   (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      rsc_nc_HDB_HDB03   (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   # rsc_st_azure_1  (stonith:fence_azure_arm):      <b>Started nws-cl-0</b>
   # rsc_st_azure_2  (stonith:fence_azure_arm):      <b>Started nws-cl-1</b>
   </code></pre>

1. **[1]**  Instance de base de données SAP NetWeaver installation Bonjour

   Instance de base de données SAP NetWeaver installation hello en tant que racine à l’aide d’un nom d’hôte virtuel qui mappe les adresses IP de toohello de configuration de serveur frontal d’équilibrage de charge de hello pour la base de données hello par exemple <b>nws-db</b> et <b>10.0.0.12</b>.

   Vous pouvez utiliser hello sapinst paramètre SAPINST_REMOTE_ACCESS_USER tooallow un toosapinst de tooconnect utilisateur non racine.

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

## <a name="sap-netweaver-application-server-installation"></a>Installation de serveur d’applications SAP NetWeaver

Suivez ces étapes de tooinstall un serveur d’applications SAP. Hello étapes ci-dessous supposent que vous installez un serveur d’applications hello sur un serveur différent de hello ASCS/SCS et les serveurs HANA. Sinon, certaines des étapes hello ci-dessous (par exemple, la configuration de la résolution de nom d’hôte) ne sont pas nécessaires.

1. Configurer la résolution de nom d’hôte    
   Vous pouvez utiliser un serveur DNS ou modifier/etc/hosts de hello sur tous les nœuds. Cet exemple montre comment toouse hello les fichier/etc/hosts.
   Remplacez l’adresse IP de hello et un nom d’hôte hello Bonjour suivant les commandes
   ```bash
   sudo vi /etc/hosts
   ```
   Insérez hello suivant lignes trop/etc/hosts. Modifiez les toomatch hello IP adresse et le nom d’hôte de votre environnement    
    
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of hello load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   # IP address of hello application server
   <b>10.0.0.8 nws-di-0</b>
   </code></pre>

1. Créer le répertoire de sapmnt hello

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   </code></pre>

1. Configurer autofs
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add hello following line toohello file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   Créer un fichier avec

   <pre><code>
   sudo vi /etc/auto.direct

   # Add hello following lines toohello file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   </code></pre>

   Redémarrez les nouveaux partages autofs toomount hello

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. Configurer le fichier SWAP
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set hello property ResourceDisk.EnableSwap tooy
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set hello size of hello SWAP file with property ResourceDisk.SwapSizeMB
   # hello free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check hello SWAP space with command swapon
   # Size of hello swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   Redémarrez le changement d’hello hello Agent tooactivate

   <pre><code>
   sudo service waagent restart
   </code></pre>

1. Installer le serveur d’applications SAP NetWeaver

   Installer un serveur d’applications SAP NetWeaver principal ou supplémentaire.

   Vous pouvez utiliser hello sapinst paramètre SAPINST_REMOTE_ACCESS_USER tooallow un toosapinst de tooconnect utilisateur non racine.

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. Mettre à jour la banque d’informations sécurisée SAP HANA

   Hello de mise à jour sécurisée à SAP HANA stocker le nom virtuel de toopoint toohello du programme d’installation de la réplication du système SAP HANA hello.
   <pre><code>
   su - <b>nws</b>adm
   hdbuserstore SET DEFAULT <b>nws-db</b>:3<b>03</b>15 <b>SAPABAP1</b> <b>&lt;password of ABAP schema&gt;</b>
   </code></pre>

## <a name="next-steps"></a>Étapes suivantes
* [Planification et implémentation de machines virtuelles Azure pour SAP][planning-guide]
* [Déploiement de machines virtuelles Azure pour SAP][deployment-guide]
* [Déploiement SGBD de machines virtuelles Azure pour SAP][dbms-guide]
* toolearn comment tooestablish haute disponibilité et le plan de récupération d’urgence de SAP HANA sur Azure (instances de grande taille), consultez [SAP HANA (instances de grande taille) haute disponibilité et récupération d’urgence sur Azure](hana-overview-high-availability-disaster-recovery.md).
* toolearn comment tooestablish haute disponibilité et le plan de récupération d’urgence de SAP HANA sur des machines virtuelles Azure, consultez [disponibilité élevée de SAP HANA sur Azure des Machines virtuelles (VM)][sap-hana-ha]
