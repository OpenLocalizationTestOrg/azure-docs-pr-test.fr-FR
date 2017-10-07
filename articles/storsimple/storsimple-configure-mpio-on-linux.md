---
title: "aaaConfigure MPIO sur un hôte Linux de StorSimple | Documents Microsoft"
description: "Configurer MPIO sur l’ordinateur hôte Linux StorSimple connecté tooa CentOS 6.6 en cours d’exécution"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: tysonn
ms.assetid: ca289eed-12b7-4e2e-9117-adf7e2034f2f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/01/2016
ms.author: alkohli
ms.openlocfilehash: d9f7e02903243494c909313fb2c33ac690764274
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-mpio-on-a-storsimple-host-running-centos"></a>Configuration de MPIO sur un hôte StorSimple exécutant CentOS
Cet article explique hello étapes tooconfigure requis e/s de gestion multivoie (MPIO) sur un serveur hôte Centos 6.6. serveur hôte de Hello est un appareil de Microsoft Azure StorSimple tooyour connecté pour la haute disponibilité via des initiateurs iSCSI. Il décrit en détail hello la détection automatique des périphériques MPIO et hello spécifique le programme d’installation pour des volumes StorSimple.

Cette procédure est applicable tooall des modèles de hello d’unités StorSimple 8000 series.

> [!NOTE]
> Cette procédure ne peut pas être utilisée pour un appareil virtuel StorSimple. Pour plus d’informations, consultez Comment tooconfigure hébergent les serveurs pour votre appareil virtuel.
> 
> 

## <a name="about-multipathing"></a>À propos de la gestion multivoie
fonctionnalité de gestion multivoie Hello vous permet de tooconfigure plusieurs chemins d’accès d’e/s entre un serveur hôte et un périphérique de stockage. Ces chemins d’accès d’E/S sont des connexions SAN physiques pouvant inclure des câbles distincts, des commutateurs, des interfaces réseau et des contrôleurs. Chemins d’accès multiples agrège les chemins d’accès d’e/s hello, tooconfigure un nouveau périphérique qui est associé à tous les chemins d’accès hello agrégée.

objectif de Hello de chemins d’accès multiples est double :

* **Haute disponibilité**: il fournit un chemin alternatif en cas de n’importe quel élément du chemin d’accès de hello d’e/s (par exemple, un câble, un commutateur, une interface réseau ou un contrôleur).
* **L’équilibrage de charge**: selon la configuration de hello votre dispositif de stockage, elle peut améliorer les performances de hello en détectant des charges sur les chemins d’accès d’e/s de hello et dynamiquement rééquilibrer les charges.

### <a name="about-multipathing-components"></a>À propos des composants de la gestion multivoie
Sous Linux, la gestion multivoie comprend des composants du noyau et des composants de l’espace utilisateur comme présenté ci-dessous.

* **Noyau**: composant principal de hello est hello *mappeur de périphérique* qui redirige les e/s et prend en charge de basculement pour les chemins d’accès et les groupes de chemin d’accès.

* **Espace utilisateur**: il s’agit *multipath-tools* qui permettent de gérer complémentaires appareils en demandant le module de chemins d’accès multiples hello-mise en correspondance le toodo. outils de Hello se composent de :
   
   * **Multipath**: répertorie et configure les appareils à chemins d’accès multiples.
   * **Multipathd**: démon qui exécute des chemins d’accès de hello MPIO et des analyses.
   * **Nom de devmap**: fournit un tooudev nom du périphérique significative pour devmaps.
   * **Kpartx**: mappe devmaps linéaire toodevice partitions toomake MPIO maps avec partitions.
   * **Multipath.conf**: fichier de configuration de MPIO démon qui est utilisé toooverwrite hello configuration intégrée table.

### <a name="about-hello-multipathconf-configuration-file"></a>Sur le fichier de configuration multipath.conf hello
fichier de configuration Hello `/etc/multipath.conf` met un grand nombre de hello multivoie fonctionnalités configurables par l’utilisateur. Hello `multipath` démon de noyau de commande et hello `multipathd` utiliser des informations figurant dans ce fichier. fichier de Hello est consulté uniquement lors de la configuration de hello de périphériques de chemins d’accès multiples hello. Assurez-vous que toutes les modifications sont effectuées avant d’exécuter hello `multipath` commande. Si vous modifiez le fichier de hello par la suite, vous devez toostop et démarrer multipathd pour effet de tootake modifications hello.

Hello multipath.conf a cinq sections :

- **Valeurs par défaut au niveau système***(defaults)*: vous pouvez remplacer les valeurs par défaut au niveau système.
- **Sur liste noire les appareils** *(liste de blocage)*: vous pouvez spécifier la liste hello des appareils qui ne doivent pas être contrôlés par le mappeur de l’appareil.
- **Blocage des exceptions** *(blacklist_exceptions)*: vous pouvez identifier toobe des appareils spécifiques considéré comme des périphériques MPIO même si répertoriés dans la liste de blocage hello.
- **Paramètres spécifiques de contrôleur de stockage** *(appareils)*: vous pouvez spécifier des paramètres de configuration qui seront appliqués toodevices qui contiennent des informations de produit et de fournisseur.
- **Paramètres spécifiques d’appareil** *(multipaths)*: vous pouvez utiliser ce paramètres de configuration de section toofine ajuster hello pour les LUN individuelles.

## <a name="configure-multipathing-on-storsimple-connected-toolinux-host"></a>Configurer plusieurs chemins d’accès sur l’ordinateur hôte connecté tooLinux de StorSimple
Un appareil connecté StorSimple tooa même hôte Linux peut être configuré pour la haute disponibilité et l’équilibrage de charge. Par exemple, si le même hôte Linux hello possède deux interfaces toohello connecté les périphériques SAN et hello a deux interfaces connectées toohello SAN tels situés sur ces interfaces hello même sous-réseau, puis il y aura des chemins de 4 accès disponible. Toutefois, si chaque interface de données sur l’interface de périphérique et l’hôte hello est sur un sous-réseau IP différent (et non routables), puis les chemins d’accès seulement 2 sera disponibles. Vous pouvez configurer les chemins d’accès multiples tooautomatically découvrir tous les chemins d’accès disponibles hello, choisissez un algorithme d’équilibrage de charge pour les chemins d’accès, appliquer des paramètres de configuration spécifiques pour les volumes StorSimple uniquement, puis activer et vérifier les chemins d’accès multiples.

Hello procédure suivante décrit comment plusieurs chemins d’accès tooconfigure lorsqu’un appareil StorSimple avec deux interfaces réseau hôte connecté tooa avec deux interfaces réseau.

## <a name="prerequisites"></a>Composants requis
Cette section détaille hello configuration requise pour le serveur de CentOS et que votre appareil StorSimple.

### <a name="on-centos-host"></a>Sur l’hôte CentOS
1. Assurez-vous que votre hôte CentOS possède 2 interfaces réseau activées. Entrez :
   
    `ifconfig`
   
    Hello suivant montre la sortie de hello lorsque deux interfaces réseau (`eth0` et `eth1`) sont présents sur l’ordinateur hôte de hello.
   
        [root@centosSS ~]# ifconfig
        eth0  Link encap:Ethernet  HWaddr 00:15:5D:A2:33:41  
          inet addr:10.126.162.65  Bcast:10.126.163.255  Mask:255.255.252.0
          inet6 addr: 2001:4898:4010:3012:215:5dff:fea2:3341/64 Scope:Global
          inet6 addr: fe80::215:5dff:fea2:3341/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
         RX packets:36536 errors:0 dropped:0 overruns:0 frame:0
          TX packets:6312 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:13994127 (13.3 MiB)  TX bytes:645654 (630.5 KiB)
   
        eth1  Link encap:Ethernet  HWaddr 00:15:5D:A2:33:42  
          inet addr:10.126.162.66  Bcast:10.126.163.255  Mask:255.255.252.0
          inet6 addr: 2001:4898:4010:3012:215:5dff:fea2:3342/64 Scope:Global
          inet6 addr: fe80::215:5dff:fea2:3342/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:25962 errors:0 dropped:0 overruns:0 frame:0
          TX packets:11 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:2597350 (2.4 MiB)  TX bytes:754 (754.0 b)
   
        loLink encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:12 errors:0 dropped:0 overruns:0 frame:0
          TX packets:12 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:720 (720.0 b)  TX bytes:720 (720.0 b)
2. Installez *iSCSI-initiator-utils* sur votre serveur CentOS. Effectuer hello suivant les étapes tooinstall *iSCSI-initiateur-utils*.
   
   1. Connectez-vous en tant que `root` à votre hôte CentOS.
   2. Installer hello *iSCSI-initiateur-utils*. Entrez :
      
       `yum install iscsi-initiator-utils`
   3. Après avoir hello *iSCSI-initiateur-utils* est correctement installé, démarrez le service iSCSI hello. Entrez :
      
       `service iscsid start`
      
       Il arrive, `iscsid` ne peut pas démarrer et hello `--force` option peut être nécessaire.
   4. tooensure que votre initiateur iSCSI est activé lors du démarrage, utilisez hello `chkconfig` service de hello tooenable de commandes.
      
       `chkconfig iscsi on`
   5. tooverify qui il a été correctement le programme d’installation, exécutez la commande hello :
      
       `chkconfig --list | grep iscsi`
      
       Voici un exemple de sortie obtenue.
      
           iscsi   0:off   1:off   2:on3:on4:on5:on6:off
           iscsid  0:off   1:off   2:on3:on4:on5:on6:off
      
       À partir de hello exemple ci-dessus, vous pouvez voir que votre environnement iSCSI s’exécutera sur l’heure de démarrage sur les niveaux d’exécution 2, 3, 4 et 5.
3. Installez *device-mapper-multipath*. Entrez :
   
    `yum install device-mapper-multipath`
   
    installation de Hello démarre. Type **Y** toocontinue lorsque vous êtes invité à confirmer l’opération.

### <a name="on-storsimple-device"></a>Sur l’appareil StorSimple
Votre appareil StorSimple doit disposer des éléments suivants :

* Deux interfaces activées pour iSCSI minimum. tooverify que les deux interfaces sont compatible iSCSI sur votre appareil StorSimple, procédez hello Bonjour portail classique Azure pour votre appareil StorSimple comme suit :
  
  1. Vous connecter au portail classique de hello pour votre appareil StorSimple.
  2. Sélectionnez votre service StorSimple Manager, cliquez sur **périphériques** et choisissez l’appareil StorSimple spécifique hello. Cliquez sur **configurer** et vérifiez les paramètres d’interface réseau hello. Une capture d’écran avec deux interfaces réseau compatibles iSCSI est affichée ci-dessous. Ici, pour DATA 2 et DATA 3, les deux interfaces 10 Gigabit Ethernet sont activées pour iSCSI.
     
      ![Configuration de MPIO StorSimple DATA 2](./media/storsimple-configure-mpio-on-linux/IC761347.png)
     
      ![Configuration de MPIO StorSimple DATA 3](./media/storsimple-configure-mpio-on-linux/IC761348.png)
     
      Bonjour **configurer** page
     
     1. Assurez-vous que les deux interfaces réseau sont compatibles iSCSI. Hello **compatible iSCSI** champ doit être défini trop**Oui**.
     2. Assurez-vous que les interfaces réseau hello ont hello même vitesse, les deux doivent être de 1 GbE ou 10 GbE.
     3. Notez les adresses IPv4 de hello des interfaces de hello compatible iSCSI et enregistrer pour une utilisation ultérieure sur l’ordinateur hôte de hello.
* interfaces d’iSCSI Hello sur votre appareil StorSimple doivent être accessibles à partir du serveur de CentOS hello.
      tooverify, vous devez les adresses IP tooprovide hello des interfaces réseau iSCSI StorSimple sur votre serveur hôte. Hello commandes utilisées et hello sortie correspondante avec DATA2 (10.126.162.25) et DATA3 (10.126.162.26) est indiqué ci-dessous :
  
        [root@centosSS ~]# iscsiadm -m discovery -t sendtargets -p 10.126.162.25:3260
        10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target
        10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target

### <a name="hardware-configuration"></a>Configuration matérielle
Nous vous conseillons de vous connectez hello deux iSCSI interfaces réseau sur les chemins d’accès distincts pour assurer la redondance. figure Hello ci-dessous montre la configuration matérielle recommandée de hello pour la haute disponibilité et l’équilibrage de charge de gestion multivoie pour votre serveur de CentOS et l’appareil StorSimple.

![Configuration matérielle de MPIO pour StorSimple tooLinux hôte](./media/storsimple-configure-mpio-on-linux/MPIOHardwareConfigurationStorSimpleToLinuxHost2M.png)

Comme indiqué dans hello précédant figure :

* Votre appareil StorSimple est une configuration active/passive avec deux contrôleurs.
* Deux commutateurs SAN sont des contrôleurs de périphériques connectés tooyour.
* Deux initiateurs iSCSI sont activés sur votre appareil StorSimple.
* Deux interfaces réseau sont activées sur votre hôte CentOS.

Hello ci-dessus configuration produira 4 chemins d’accès distincts entre votre appareil et hello l’hôte si les interfaces hello hôte et les données sont routables.

> [!IMPORTANT]
> * Nous vous recommandons de ne pas mélanger les interfaces réseau 1 Gigabit Ethernet et 10 Gigabit Ethernet pour la gestion multivoie. Lorsque vous utilisez deux interfaces réseau, les deux interfaces hello doivent être de type identiques de hello.
> * Sur votre appareil StorSimple, DATA0, DATA1, DATA4 et DATA5 sont des interfaces 1 Gigabit Ethernet, alors que DATA2 et DATA3 sont des interfaces réseau 10 Gigabit Ethernet.|
> 
> 

## <a name="configuration-steps"></a>Configuration
les étapes de configuration Hello pour les chemins d’accès multiples impliquent la configuration de hello les chemins disponibles pour la détection automatique, en spécifiant toouse algorithme hello l’équilibrage de charge, l’activation de plusieurs chemins d’accès et enfin vérification de la configuration de hello. Chacune de ces étapes est décrite en détail dans les sections suivantes de hello.

### <a name="step-1-configure-multipathing-for-automatic-discovery"></a>Étape 1 : Configurer la gestion multivoie pour la détection automatique
les appareils pris en charge MPIO Hello peuvent être automatiquement détectés et configurés.

1. Initialisez le fichier `/etc/multipath.conf` . Entrez :
   
     `mpathconf --enable`
   
    Hello ci-dessus commande créera un `sample/etc/multipath.conf` fichier.
2. Démarrez le service de gestion multivoie. Entrez :
   
    `service multipathd start`
   
    Vous verrez hello suivant de sortie :
   
    `Starting multipathd daemon:`
3. Activez la détection automatique des chemins d’accès multiples. Entrez :
   
    `mpathconf --find_multipaths y`
   
    Cela modifiera la section de paramètres par défaut hello de votre `multipath.conf` comme indiqué ci-dessous :
   
        defaults {
        find_multipaths yes
        user_friendly_names yes
        path_grouping_policy multibus
        }

### <a name="step-2-configure-multipathing-for-storsimple-volumes"></a>Étape 2 : Configurer la gestion multivoie pour les volumes StorSimple
Par défaut, tous les appareils sont noirs répertoriés dans le fichier de multipath.conf hello et seront ignorés. Vous devez toocreate blacklist exceptions tooallow multivoie pour les volumes à partir d’appareils StorSimple.

1. Modifier hello `/etc/mulitpath.conf` fichier. Entrez :
   
    `vi /etc/multipath.conf`
2. Recherchez la section de blacklist_exceptions de hello dans le fichier de multipath.conf hello. Votre appareil StorSimple doit toobe répertorié comme une exception de la liste de blocage dans cette section. Vous pouvez ne pas commenter pertinentes de lignes dans cette toomodify fichier il comme indiqué ci-dessous (utilisez uniquement hello modèle spécifique de l’appareil que vous utilisez hello) :
   
        blacklist_exceptions {
            device {
                       vendor  "MSFT"
                       product "STORSIMPLE 8100*"
            }
            device {
                       vendor  "MSFT"
                       product "STORSIMPLE 8600*"
            }
           }

### <a name="step-3-configure-round-robin-multipathing"></a>Étape 3 : Configurer la gestion multivoie de tourniquet (round robin)
Cet algorithme d’équilibrage de charge utilise contrôleur actif de tous les hello toohello multipaths disponible de manière à charge équilibrée, tourniquet.

1. Modifier hello `/etc/multipath.conf` fichier. Entrez :
   
    `vi /etc/multipath.conf`
2. Sous hello `defaults` section, jeu hello `path_grouping_policy` trop`multibus`. Hello `path_grouping_policy` spécifie multipaths toounspecified tooapply de la stratégie hello par défaut chemin d’accès au regroupement. section des valeurs par défaut de Hello se présente comme indiqué ci-dessous.
   
        defaults {
                user_friendly_names yes
                path_grouping_policy multibus
        }

> [!NOTE]
> Hello les valeurs les plus courantes de `path_grouping_policy` incluent :
> 
> * basculement = 1 chemin d’accès par groupe de priorité
> * multibus = tous les chemins d’accès valides dans 1 groupe de priorité
> 
> 

### <a name="step-4-enable-multipathing"></a>Étape 4 : Activer la gestion multivoie
1. Redémarrez hello `multipathd` démon. Entrez :
   
    `service multipathd restart`
2. sortie de Hello sera comme indiqué ci-dessous :
   
        [root@centosSS ~]# service multipathd start
        Starting multipathd daemon:  [OK]

### <a name="step-5-verify-multipathing"></a>Étape 5 : Vérifier la gestion multivoie
1. D’abord vous assurer que connexion iSCSI est établie avec l’appareil StorSimple hello comme suit :
   
   a. Détectez votre appareil StorSimple. Entrez :
      
    ```
    iscsiadm -m discovery -t sendtargets -p  <IP address of network interface on hello device>:<iSCSI port on StorSimple device>
    ```
    
    sortie Hello lorsque l’adresse IP DATA0 est 10.126.162.25 et port 3260 est ouvert sur l’appareil StorSimple hello pour le trafic iSCSI sortant est comme indiqué ci-dessous :
    
    ```
    10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    ```

    Hello de copie IQN de votre appareil StorSimple, `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`, à partir de hello précédant la sortie.

   b. Connectez appareil toohello à l’aide de IQN cible. l’appareil StorSimple Hello est ici de cible iSCSI hello. Entrez :

    ```
    iscsiadm -m node --login -T <IQN of iSCSI target>
    ```

    Hello suivant montre la sortie avec une nom qualifié de la cible de `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`. sortie de Hello indique que vous avez correctement connecté deux interfaces réseau iSCSI de toohello sur votre appareil.

    ```
    Logging in too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Logging in too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Login too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    Login too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    ```

    Si vous voyez l’interface qu’un seul hôte et deux chemins d’accès ici, vous devez tooenable les deux interfaces hello sur l’ordinateur hôte iSCSI. Vous pouvez suivre hello [des instructions dans la documentation de Linux](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/iscsioffloadmain.html).

2. Un volume est un serveur de CentOS toohello exposé à partir de l’appareil StorSimple hello. Pour plus d’informations, consultez [étape 6 : création d’un volume](storsimple-deployment-walkthrough.md#step-6-create-a-volume) via hello portail classique Azure sur votre appareil StorSimple.

3. Vérifiez les chemins d’accès disponibles hello. Entrez :

      ```
      multipath –l
      ```

      Hello, l’exemple suivant montre la sortie hello pour les deux interfaces réseau sur une interface réseau StorSimple périphérique connecté tooa hôte unique, avec deux chemins d’accès disponibles.

        ```
        mpathb (36486fd20cc081f8dcd3fccb992d45a68) dm-3 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 7:0:0:1 sdc 8:32 active undef running
        `- 6:0:0:1 sdd 8:48 active undef running
        ```

        hello following example shows hello output for two network interfaces on a StorSimple device connected tootwo host network interfaces with four available paths.

        ```
        mpathb (36486fd27a23feba1b096226f11420f6b) dm-2 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 17:0:0:0 sdb 8:16 active undef running
        |- 15:0:0:0 sdd 8:48 active undef running
        |- 14:0:0:0 sdc 8:32 active undef running
        `- 16:0:0:0 sde 8:64 active undef running
        ```

        After hello paths are configured, refer toohello specific instructions on your host operating system (Centos 6.6) toomount and format this volume.

## <a name="troubleshoot-multipathing"></a>Résolution des problèmes de la gestion multivoie
Cette section fournit des conseils utiles si vous rencontrez des problèmes lors de la configuration de la gestion multivoie.

Q : Je ne vois pas les modifications de hello dans `multipath.conf` fichier prennent effet.

R : Si vous avez apporté les modifications de toohello `multipath.conf` fichier, vous devrez le service de gestion multivoie toorestart hello. Tapez hello de commande suivante :

    service multipathd restart

Q : J’ai activé un deux interfaces réseau sur l’appareil StorSimple hello et deux interfaces réseau sur l’ordinateur hôte de hello. Lorsque la liste de chemins d’accès disponibles de hello, je vois uniquement deux chemins d’accès. Chemins d’accès disponibles quatre toosee prévu.

R : Vérifiez que hello deux chemins sur hello même sous-réseau et routable. Si les interfaces réseau hello se trouvent sur différents réseaux locaux virtuels et non routables, vous verrez uniquement deux chemins d’accès. Une façon tooverify il s’agit de toomake assurer que vous pouvez joindre les deux interfaces d’hôte hello à partir d’une interface réseau sur l’appareil StorSimple hello. Vous devez trop[contactez le Support Microsoft](storsimple-contact-microsoft-support.md) que cette vérification peut uniquement être effectuée via une session de support.

Q : Lorsque je répertorie les chemins d’accès disponibles, je ne vois aucune sortie.

R : En règle générale, ne subit des chemins d’accès complémentaires suggère un problème avec le démon de chemins d’accès multiples hello et il est très probablement que n’importe quel problème ici se trouve dans hello `multipath.conf` fichier.

Il est également important de vérifier que vous permet de visualiser certains disques après la connexion toohello cible, car aucune réponse à partir des listes de chemins d’accès multiples hello ne peut aussi signifier que vous n’avez pas tous les disques.

* Utilisez hello suivant bus SCSI de commande toorescan hello :
  
    `$ rescan-scsi-bus.sh `(partie du package sg3_utils)
* Tapez hello suivant de commandes :
  
    `$ dmesg | grep sd*`
     
     Ou
  
    `$ fdisk –l`
  
    Celles-ci renverront les détails des disques récemment ajoutés.
* toodetermine s’il s’agit d’un disque StorSimple, utilisez hello suivant de commandes :
  
    `cat /sys/block/<DISK>/device/model`
  
    Cela renvoie une chaîne qui déterminera s’il s’agit d’un disque StorSimple.

Cause moins probable mais possible, la présence d’un PID iSCSI obsolète. Utilisez hello suivant commande toolog hors tension à partir des sessions iSCSI hello :

    iscsiadm -m node --logout -p <Target_IP>

Répétez cette commande pour toutes les interfaces réseau de hello connecté sur la cible iSCSI hello, qui est votre appareil StorSimple. Une fois que vous avez déconnecté de toutes les sessions iSCSI de hello, utilisez session iSCSI de hello iSCSI cible IQN tooreestablish hello. Tapez hello de commande suivante :

    iscsiadm -m node --login -T <TARGET_IQN>


Q : Je ne sais pas si mon appareil figure dans la liste approuvée.

R : tooverify si votre appareil est dans la liste approuvée, utilisez hello commande interactive dépannage suivante :

    multipathd –k
    multipathd> show devices
    available block devices:
    ram0 devnode blacklisted, unmonitored
    ram1 devnode blacklisted, unmonitored
    ram2 devnode blacklisted, unmonitored
    ram3 devnode blacklisted, unmonitored
    ram4 devnode blacklisted, unmonitored
    ram5 devnode blacklisted, unmonitored
    ram6 devnode blacklisted, unmonitored
    ram7 devnode blacklisted, unmonitored
    ram8 devnode blacklisted, unmonitored
    ram9 devnode blacklisted, unmonitored
    ram10 devnode blacklisted, unmonitored
    ram11 devnode blacklisted, unmonitored
    ram12 devnode blacklisted, unmonitored
    ram13 devnode blacklisted, unmonitored
    ram14 devnode blacklisted, unmonitored
    ram15 devnode blacklisted, unmonitored
    loop0 devnode blacklisted, unmonitored
    loop1 devnode blacklisted, unmonitored
    loop2 devnode blacklisted, unmonitored
    loop3 devnode blacklisted, unmonitored
    loop4 devnode blacklisted, unmonitored
    loop5 devnode blacklisted, unmonitored
    loop6 devnode blacklisted, unmonitored
    loop7 devnode blacklisted, unmonitored
    sr0 devnode blacklisted, unmonitored
    sda devnode whitelisted, monitored
    dm-0 devnode blacklisted, unmonitored
    dm-1 devnode blacklisted, unmonitored
    dm-2 devnode blacklisted, unmonitored
    sdb devnode whitelisted, monitored
    sdc devnode whitelisted, monitored
    dm-3 devnode blacklisted, unmonitored


Pour plus d’informations, consultez trop[utiliser la résolution des problèmes de commande interactive pour les chemins d’accès multiples](http://www.centos.org/docs/5/html/5.1/DM_Multipath/multipath_config_confirm.html).

## <a name="list-of-useful-commands"></a>Liste des commandes utiles
| Tapez  | Commande | Description |
| --- | --- | --- |
| **iSCSI** |`service iscsid start` |Démarrer le service iSCSI |
| &nbsp; |`service iscsid stop` |Arrêter le service iSCSI |
| &nbsp; |`service iscsid restart` |Redémarrer le service iSCSI |
| &nbsp; |`iscsiadm -m discovery -t sendtargets -p <TARGET_IP>` |Découvrir les cibles disponibles sur hello spécifié adresse |
| &nbsp; |`iscsiadm -m node --login -T <TARGET_IQN>` |Connectez-vous à toohello de cible iSCSI |
| &nbsp; |`iscsiadm -m node --logout -p <Target_IP>` |Se déconnecter du serveur cible iSCSI hello |
| &nbsp; |`cat /etc/iscsi/initiatorname.iscsi` |Imprimer le nom de l'initiateur iSCSI |
| &nbsp; |`iscsiadm –m session –s <sessionid> -P 3` |Vérifier l’état de hello de session iSCSI de hello et volume détectés sur l’ordinateur hôte de hello |
| &nbsp; |`iscsi –m session` |Affiche toutes les sessions iSCSI de hello établies entre l’appareil StorSimple hello et un hôte de hello |
|  | | |
| **Gestion multivoie** |`service multipathd start` |Démarrer le démon multivoie |
| &nbsp; |`service multipathd stop` |Arrêter le démon multivoie |
| &nbsp; |`service multipathd restart` |Redémarrer le démon multivoie |
| &nbsp; |`chkconfig multipathd on` </br> OU </br> `mpathconf –with_chkconfig y` |Activer les chemins d’accès multiples démon toostart au moment du démarrage |
| &nbsp; |`multipathd –k` |Démarrez la console interactive de hello pour la résolution des problèmes |
| &nbsp; |`multipath –l` |Lister les connexions et les périphériques multivoie |
| &nbsp; |`mpathconf --enable` |Créer un exemple de fichier mulitpath.conf dans `/etc/mulitpath.conf` |
|  | | |

## <a name="next-steps"></a>Étapes suivantes
Comme vous configurez MPIO sur un hôte Linux, vous devrez peut-être également toohello toorefer suivant CentoS 6.6 documents :

* [Configuration de MPIO sur CentOS](http://www.centos.org/docs/5/html/5.1/DM_Multipath/setup_procedure.html)
* [Guide de formation Linux](http://linux-training.be/files/books/LinuxAdm.pdf)

