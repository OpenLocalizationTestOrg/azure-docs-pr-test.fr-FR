---
title: "aaaHow tooinstall serveur cible maître Linux pour basculement à partir d’Azure site tooon | Documents Microsoft"
description: "Pour reprotéger une machine virtuelle Linux, vous avez besoin d’un serveur cible maître Linux. Découvrez comment tooinstall une."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: d7c55d115712b9862414979f89efb1f177c5f0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-linux-master-target-server"></a>Installer un serveur cible maître Linux
Après avoir effectué sur vos ordinateurs virtuels, vous pouvez échouer hello arrière machines virtuelles toohello sur site local. toofail précédent, vous devez tooreprotect hello virtual machine à partir du site local de toohello Azure. Pour ce processus, vous avez besoin d’un trafic de hello tooreceive local du serveur de cible maître. 

Si votre machine virtuelle protégée est de type Windows, vous avez besoin d’un serveur cible maître Windows. Si vous avez une machine virtuelle Linux, vous avez besoin d’un serveur cible maître Linux. Toolearn les étapes suivantes de hello en lecture comment toocreate et installer une Linux maître cible.

> [!IMPORTANT]
> À partir de la version du serveur cible maître de hello 9.10.0, serveur cible maître de la dernière hello peut être uniquement installé sur un serveur d’Ubuntu 16.04. Les nouvelles installations ne sont pas autorisées sur les serveurs de CentOS6.6. Toutefois, vous pouvez continuer tooupgrade vos serveurs de la cible principale ancienne aide hello 9.10.0 version.

## <a name="overview"></a>Vue d'ensemble
Cet article fournit des instructions pour la tooinstall une Linux maître cible.

Valider des commentaires ou des questions à fin hello de cet article ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="prerequisites"></a>Composants requis

* hôte de hello toochoose sur le toodeploy hello serveur cible maître, déterminer si la restauration automatique hello va toobe tooan existante sur site ordinateur virtuel ou la machine virtuelle tooa. 
    * Pour un ordinateur virtuel existant, hôte hello du serveur cible maître hello doit avoir accès aux banques de données toohello de la machine virtuelle de hello.
    * Si l’ordinateur virtuel local, hello n’existe pas, la machine virtuelle de la restauration automatique hello est créé sur le même hôte que le serveur cible maître hello de hello. Vous pouvez choisir n’importe quel hôte ESXi tooinstall serveur cible maître hello.
* serveur cible maître Hello doit être sur un réseau qui peut communiquer avec le serveur de processus hello et serveur de configuration hello.
* version de Hello du serveur cible maître hello doit être égal tooor précédemment que dans les versions de serveur de processus hello et serveur de configuration hello hello. Par exemple, si la version hello hello du serveur de configuration est 9.4, version hello du serveur cible maître hello peut être 9.4 ou 9.3 mais pas 9.5.
* serveur cible maître Hello ne peut être un ordinateur virtuel VMware et non à un serveur physique.

## <a name="create-hello-master-target-according-toohello-sizing-guidelines"></a>Créer le serveur cible maître hello en fonction des instructions de dimensionnement de toohello

Créer un serveur cible maître hello conformément aux hello suivant les instructions de dimensionnement :
- **RAM** : 6 Go ou plus
- **Taille du disque du système d’exploitation**: 100 Go ou plus (tooinstall CentOS6.6)
- **Taille du disque supplémentaire pour le lecteur de conservation** : 1 To
- **Cœurs d’UC** : 4 cœurs ou plus

Ubuntu noyaux sont prises en charge de charge Hello qui suit.


|Série de noyau  |Prend en charge des trop |
|---------|---------|
|4.4      |4.4.0-81-generic         |
|4.8      |4.8.0-56-generic         |
|4.10     |4.10.0-24-generic        |


## <a name="deploy-hello-master-target-server"></a>Déployer le serveur cible maître de hello

### <a name="install-ubuntu-16042-minimal"></a>Installer Ubuntu version 16.04.2 Minimal

Prendre hello suivant le système d’exploitation de hello étapes tooinstall hello Ubuntu 16.04.2 64 bits.

**Étape 1 :** accédez toohello [lien de téléchargement](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64) et choisissez le miroir le plus proche de hello à partir de laquelle télécharger un fichier ISO du Ubuntu 16.04.2 minimale 64 bits.

Conserver un fichier ISO du Ubuntu 16.04.2 minimale 64 bits dans le lecteur de DVD de hello et démarrer hello système.

**Étape 2 :** sélectionnez **French** (Français) comme langue par défaut, puis appuyez sur **Entrée**.

![Sélectionner une langue](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image1.png)

**Étape 3 :** sélectionnez **Install Ubuntu Server** (Installer le serveur Ubuntu), puis appuyez sur **Entrée**.

![Sélectionner l’option d’installation du serveur Ubuntu](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image2.png)

**Étape 4 :** sélectionnez **French** (Français) comme langue par défaut, puis appuyez sur **Entrée**.

![Sélectionner French (Français) comme langue par défaut](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image3.png)

**Étape 5 :** sélectionnez hello option appropriée dans hello **fuseau horaire** liste d’options et sélectionnez **entrée**.

![Sélectionnez le fuseau horaire correct de hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image4.png)

**Étape 6 :** sélectionnez **non** (hello option par défaut), puis sélectionnez **entrée**.


![Configurer hello clavier](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image5.png)

**Étape 7 :** sélectionnez **anglais (États-Unis)** comme hello pays d’origine pour le clavier de hello et sélectionnez **entrée**.

![Sélectionnez des États-Unis comme pays hello d’origine](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image6.png)

**Étape 8 :** sélectionnez **anglais (États-Unis)** comme disposition du clavier hello, puis sélectionnez **entrée**.

![Sélectionnez l’anglais (États-Unis) en tant que la disposition du clavier hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image7.png)

**Étape 9 :** entrer de nom d’hôte hello pour votre serveur Bonjour **nom d’hôte** zone, puis sélectionnez **continuer**.

![Entrez le nom d’hôte hello pour votre serveur](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image8.png)

**Étape 10 :** toocreate un compte d’utilisateur, entrez le nom d’utilisateur hello et sélectionnez **continuer**.

![Création d'un compte d'utilisateur](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image9.png)

**Étape 11 :** mot de passe hello hello nouveau compte d’utilisateur, puis sélectionnez **continuer**.

![Entrez le mot de passe hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image10.png)

**Étape 12 :** confirmer hello mot de passe utilisateur hello et sélectionnez **continuer**.

![Confirmer les mots de passe hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image11.png)

**Étape 13 :** sélectionnez **non** (hello option par défaut), puis sélectionnez **entrée**.

![Configurer des utilisateurs et des mots de passe](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image12.png)

**Étape 14 :** si le fuseau horaire hello affichée est correcte, sélectionnez **Oui** (hello option par défaut), puis sélectionnez **entrée**.

tooreconfigure votre fuseau horaire, sélectionnez **non**.

![Configurer l’horloge hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image13.png)

**Étape 15 :** hello options de la méthode de partitionnement, sélectionnez **guidée - utiliser l’intégralité du disque**, puis sélectionnez **entrée**.

![Sélectionnez hello option de méthode de partitionnement](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image14.png)

**Étape 16 :** sélectionnez hello disque approprié à partir de hello **sélectionnez disque toopartition** options, puis sélectionnez **entrée**.


![Sélectionnez le disque hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image15.png)

**Étape 17 :** sélectionnez **Oui** toowrite hello toodisk de modifications, puis sélectionnez **entrée**.

![Écrire hello modifications toodisk](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image16.png)

**Étape 18 :** sélectionnez l’option par défaut de hello, sélectionnez **continuer**, puis sélectionnez **entrée**.

![Sélectionnez l’option par défaut de hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image17.png)

**Étape 19 :** l’option hello approprié pour la gestion des mises à niveau sur votre système, puis **entrée**.

![Sélectionnez comment toomanage mises à niveau](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image18.png)

> [!WARNING]
> Étant donné que le serveur cible maître de Azure Site Recovery hello requiert une version spécifique de hello Ubuntu, vous devez tooensure ce noyau hello mises à niveau sont désactivés pour la machine virtuelle de hello. Si elles sont activées, les mises à niveau régulières provoquent toomalfunction de serveur cible maître hello. Veillez à sélectionner hello **aucune mise à jour automatique** option.


**Étape 20 :** sélectionnez les options par défaut. Si vous souhaitez openSSH pour établir une connexion SSH, sélectionnez hello **OpenSSH server** option et sélectionnez **continuer**.

![Sélectionner les logiciels](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image19.png)

**Étape 21 :** sélectionnez **Yes** (Oui), puis appuyez sur **Entrée**.

![Chargeur de démarrage de l’installation n’hello GRUB](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image20.png)

**Étape 22 :** sélectionnez hello appareil approprié pour l’installation de chargeur de démarrage de hello (de préférence **/dev/sda**), puis sélectionnez **entrée**.

![Sélectionner un appareil pour l’installation du chargeur de démarrage](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image21.png)

**Étape 23 :** sélectionnez **continuer**, puis sélectionnez **entrée** installation de hello toofinish.

![Terminer l’installation de hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image22.png)

Une fois l’installation de hello est terminée, connectez-vous toohello machine virtuelle avec les informations d’identification d’utilisateur nouveau hello. (Consultez trop**étape 10** pour plus d’informations.)

Étapes hello décrits dans hello suivant capture d’écran tooset hello racine mot de passe utilisateur. Ensuite, connectez-vous en tant qu’utilisateur ROOT.

![Mot de passe utilisateur ensemble hello racine](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image23.png)


### <a name="prepare-hello-machine-for-configuration-as-a-master-target-server"></a>Préparer l’ordinateur hello pour la configuration comme un serveur cible maître
Ensuite, préparez l’ordinateur hello pour la configuration comme un serveur cible maître.

ID de hello tooget pour chaque disque SCSI dans une machine virtuelle Linux, activer hello **disque. EnableUUID = TRUE** paramètre.

tooenable étapes de ce paramètre, hello take suivant :

1. Arrêtez votre machine virtuelle.

2. Entrée hello pour l’ordinateur virtuel de hello dans le volet gauche de hello d’avec le bouton droit et sélectionnez **modifier les paramètres**.

3. Sélectionnez hello **Options** onglet.

4. Dans le volet gauche de hello, sélectionnez **avancé** > **général**, puis sélectionnez hello **les paramètres de Configuration** bouton dans la partie inférieure droite de hello d’écran hello.

    ![Onglets Options](./media/site-recovery-how-to-install-linux-master-target/media/image20.png)

    Hello **les paramètres de Configuration** option n’est pas disponible lors de la machine de hello est en cours d’exécution. toomake cet onglet actif, arrêter la machine virtuelle de hello.

5. Vérifiez si une ligne comportant **disk.EnableUUID** existe.

    - Si la valeur de hello existe et qu’il est défini trop**False**, modifiez la valeur de hello trop**True**. (les valeurs hello ne respectent pas la casse).

    - Si la valeur de hello existe et qu’il est défini trop**True**, sélectionnez **Annuler**.

    - Si la valeur de hello n’existe pas, sélectionnez **ajouter une ligne**.

    - Dans la colonne de nom hello, ajoutez **disque. EnableUUID**, puis définissez la valeur de hello trop**TRUE**.

    ![Vérification de la présence de disk.EnableUUID](./media/site-recovery-how-to-install-linux-master-target/media/image21.png)

#### <a name="disable-kernel-upgrades"></a>Désactiver les mises à niveau du noyau

Azure serveur cible maître de récupération de Site requiert une version spécifique de hello Ubuntu, assurez-vous que les mises à niveau du noyau hello sont désactivées pour l’ordinateur virtuel de hello.

Si les mises à niveau du noyau sont activés, les mises à niveau régulières provoquent toomalfunction de serveur cible maître hello.

#### <a name="download-and-install-additional-packages"></a>Télécharger et installer les packages supplémentaires

> [!NOTE]
> Assurez-vous que vous avez toodownload de connectivité Internet et installez des packages supplémentaires. Si vous n’avez pas connecté à Internet, vous devez toomanually rechercher ces packages RPM et de les installer.

```
apt-get install -y multipath-tools lsscsi python-pyasn1 lvm2 kpartx
```

### <a name="get-hello-installer-for-setup"></a>Obtenir le programme d’installation hello pour le programme d’installation

Si votre serveur cible maître possède une connexion Internet, vous pouvez utiliser hello suivant le programme d’installation d’étapes toodownload hello. Dans le cas contraire, vous pouvez copier le programme d’installation hello hello serveur de processus et l’installer.

#### <a name="download-hello-master-target-installation-packages"></a>Télécharger les packages d’installation du serveur cible maître hello

[Télécharger hello dernière Linux cible maître installation](https://aka.ms/latestlinuxmobsvc).

toodownload à l’aide de Linux, type :

```
wget https://aka.ms/latestlinuxmobsvc -O latestlinuxmobsvc.tar.gz
```

Assurez-vous que vous téléchargez et décompressez le programme d’installation hello dans votre répertoire de base. Si vous décompressez trop**/usr/Local**, puis hello installation échoue.


#### <a name="access-hello-installer-from-hello-process-server"></a>Programme d’installation d’accès hello hello du serveur de processus

1. Sur le serveur de processus hello, accédez trop**C:\Program Files (x86) \Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**.

2. Copiez le fichier du programme d’installation requis hello hello serveur de processus et l’enregistrer en tant que **latestlinuxmobsvc.tar.gz** dans votre répertoire de base.


### <a name="apply-custom-configuration-changes"></a>Appliquer des modifications de configuration personnalisées

modifications de configuration personnalisée tooapply, utilisez hello comme suit :


1. Exécutez hello suivant binaire de commande toountar hello.
    ```
    tar -zxvf latestlinuxmobsvc.tar.gz
    ```
    ![Capture d’écran de hello commande toorun](./media/site-recovery-how-to-install-linux-master-target/image16.png)

2. La commande suivante d’exécution hello toogive autorisation.
    ```
    chmod 755 ./ApplyCustomChanges.sh
    ```

3. Exécutez hello commande toorun hello script suivant.
    ```
    ./ApplyCustomChanges.sh
    ```
> [!NOTE]
> Exécuter le script hello qu’une seule fois sur le serveur de hello. Hello serveur arrêté. Redémarrez hello serveur après avoir ajouté un disque, comme décrit dans la section suivante de hello.

### <a name="add-a-retention-disk-toohello-linux-master-target-virtual-machine"></a>Ajouter une machine virtuelle de rétention disque toohello Linux cible maître

Utilisez hello suivant les étapes toocreate un disque de rétention :

1. Attacher une disque de 1 to toohello Linux cible maître machine virtuelle et ensuite démarrer hello ordinateur.

2. Hello d’utilisation **multipath -ll** ID de commande toolearn hello MPIO du disque de rétention hello.

    ```
    multipath -ll
    ```
    ![ID de chemins d’accès multiples Hello du disque de rétention de hello](./media/site-recovery-how-to-install-linux-master-target/media/image22.png)

3. Formater le lecteur hello et créer un système de fichiers sur le nouveau lecteur de hello.

    ```
    mkfs.ext4 /dev/mapper/<Retention disk's multipath id>
    ```
    ![Création d’un système de fichiers sur le lecteur de hello](./media/site-recovery-how-to-install-linux-master-target/media/image23.png)

4. Après avoir créé le système de fichiers hello, montez le disque de rétention hello.
    ```
    mkdir /mnt/retention
    mount /dev/mapper/<Retention disk's multipath id> /mnt/retention
    ```
    ![Disque de rétention de montage hello](./media/site-recovery-how-to-install-linux-master-target/media/image24.png)

5. Créer hello **fstab** lecteur de rétention entrée toomount hello chaque fois hello système démarre.
    ```
    vi /etc/fstab
    ```
    Sélectionnez **insérer** toobegin modification hello fichier. Créer une nouvelle ligne, puis insérez hello après le texte. Modifier l’ID de plusieurs chemins de disque hello basé sur les ID de chemins d’accès multiples hello mis en surbrillance à partir de la commande précédente hello.

    **/dev/mapper/<Retention disks multipath id> /mnt/retention ext4 rw 0 0**

    Sélectionnez **ÉCHAP**, puis tapez **: wq** (écrire et quittez) fenêtre de l’éditeur tooclose hello.

### <a name="install-hello-master-target"></a>Installer le serveur cible maître hello

> [!IMPORTANT]
> version de Hello du serveur cible maître de hello doit être égal tooor précédemment que dans les versions de serveur de processus hello et serveur de configuration hello hello. Si cette condition n’est pas remplie, la reprotection aboutit, mais la réplication échoue.


> [!NOTE]
> Avant d’installer de serveur cible maître de hello, vérifiez que hello **/etc/hosts** fichier sur l’ordinateur virtuel de hello contient des entrées qui mappent hello nom d’hôte local toohello adresses IP qui sont associés à toutes les cartes réseau.

1. Copier la phrase secrète de hello à partir de **C:\ProgramData\Microsoft Azure Site Recovery\private\connection.passphrase** sur le serveur de configuration hello. Puis l’enregistrer en tant que **passphrase.txt** Bonjour même répertoire local en exécutant hello la commande suivante :

    ```
    echo <passphrase> >passphrase.txt
    ```
    Exemple : 
    
    ```
    echo itUx70I47uxDuUVY >passphrase.txt
    ```

2. Notez l’adresse IP du serveur de configuration hello. Vous en avez besoin dans l’étape suivante de hello.

3. Exécutez hello suivant du serveur cible maître de commande tooinstall hello et inscrire le serveur de hello avec le serveur de configuration hello.

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```

    Exemple : 
    
    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

    Attendez la fin du script de hello. Si le serveur cible maître hello inscrit avec succès, serveur cible maître hello est répertorié sur hello **Infrastructure Site Recovery** page du portail de hello.


#### <a name="install-hello-master-target-by-using-interactive-installation"></a>Installer le serveur cible maître hello à l’aide d’une installation interactive

1. Exécutez hello suivant cible de commande tooinstall hello maître. Pour le rôle de l’agent hello, choisissez **cible maître**.

    ```
    ./install
    ```

2. Choisissez l’emplacement par défaut de hello pour l’installation, puis sélectionnez **entrée** toocontinue.

    ![Choix d’un emplacement par défaut pour l’installation du serveur cible maître](./media/site-recovery-how-to-install-linux-master-target/image17.png)

Une fois l’installation de hello est terminée, inscrire le serveur de configuration de hello en utilisant la ligne de commande hello.

1. Notez l’adresse IP de hello hello du serveur de configuration. Vous en avez besoin dans l’étape suivante de hello.

2. Exécutez hello suivant du serveur cible maître de commande tooinstall hello et inscrire le serveur de hello avec le serveur de configuration hello.

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```
    Exemple : 

    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

   Attendez la fin du script de hello. Si le serveur cible maître hello est correctement inscrit, serveur cible maître hello est répertorié sur hello **Infrastructure Site Recovery** page du portail de hello.


### <a name="upgrade-hello-master-target"></a>Mettre à niveau le serveur cible maître hello

Exécutez le programme d’installation hello. Il détecte automatiquement que l’agent hello est installé sur le serveur cible maître hello. tooupgrade, sélectionnez **Y**.  Après avoir hello le programme d’installation est terminée, vérifiez la version de hello du serveur cible maître hello installé à l’aide de hello commande suivante.

    ```
    cat /usr/local/.vx_version
    ```

Vous pouvez voir que hello **Version** champ indique le numéro de version de hello du serveur cible maître hello.

### <a name="install-vmware-tools-on-hello-master-target-server"></a>Installer les outils VMware sur le serveur cible maître de hello

Vous devez tooinstall les outils VMware sur le serveur cible maître hello afin qu’il peut découvrir des magasins de données hello. Si les outils hello ne sont pas installés, écran de reprotection hello n’est pas répertorié dans les magasins de données hello. Après l’installation des outils de hello VMware, vous devez toorestart.

## <a name="next-steps"></a>Étapes suivantes
Une fois l’installation de hello et l’inscription du serveur cible maître hello a finsihed, vous pouvez voir serveur cible maître hello apparaissent sur hello **cible maître** section **Infrastructure Site Recovery**, sous hello vue d’ensemble du serveur de configuration.

Vous pouvez maintenant procéder à la [reprotection](site-recovery-how-to-reprotect.md), puis à la restauration automatique.

## <a name="common-issues"></a>Problèmes courants

* Veillez à ne pas activer Storage vMotion sur des composants de gestion tels qu’un serveur cible maître. Si le serveur cible maître hello déplace après une reprotection réussie, les disques de machine virtuelle hello (VMDK) ne peut pas être détachées. Dans ce cas, la restauration automatique échoue.

* serveur cible maître Hello ne doit pas posséder de toutes les captures instantanées sur l’ordinateur virtuel de hello. Si des instantanés sont présents, la restauration automatique échoue.

* En raison des configurations de carte réseau de personnalisée toosome à certains clients, interface de réseau hello est désactivée lors du démarrage et l’agent de hello cible maître ne peut pas initialiser. Vérifiez que hello propriétés suivantes sont définies correctement. Vérifiez ces propriétés Bonjour Ethernet de carte /etc/sysconfig/network-scripts/ifcfg du fichier-eth *.
    * BOOTPROTO=dhcp
    * ONBOOT=yes
