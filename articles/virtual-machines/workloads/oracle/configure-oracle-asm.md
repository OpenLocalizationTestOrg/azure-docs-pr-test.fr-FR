---
title: "aaaSet d’Oracle ASM sur une machine virtuelle de Azure Linux | Documents Microsoft"
description: "Rendez Oracle ASM opérationnel rapidement dans votre environnement Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: RicksterCDN
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/19/2017
ms.author: rclaus
ms.openlocfilehash: d6a7046638e919876477d46943faabcb1872acac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-oracle-asm-on-an-azure-linux-virtual-machine"></a>Configurer Oracle ASM sur une machine virtuelle Linux Azure  

Les machines virtuelles fournissent un environnement informatique entièrement configurable et flexible. Ce didacticiel décrit le déploiement de base de machine virtuelle Azure combiné avec l’installation de hello et la configuration d’Oracle Automated Storage Management (ASM).  Vous allez apprendre à effectuer les actions suivantes :

> [!div class="checklist"]
> * Créer et connecter tooan machine virtuelle de base de données Oracle
> * Installer et configurer Oracle Automated Storage Management
> * Installer et configurer Oracle Grid Infrastructure
> * Initialiser une installation Oracle ASM
> * Créer une base de données Oracle gérée par ASM


[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

Si vous choisissez tooinstall et que vous utilisez hello CLI localement, ce didacticiel nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure. Exécutez `az --version` version de hello toofind. Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="prepare-hello-environment"></a>Préparer l’environnement de hello

### <a name="create-a-resource-group"></a>Créer un groupe de ressources

toocreate un groupe de ressources, utilisez hello [création de groupe de az](/cli/azure/group#create) commande. Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées. Dans cet exemple, un groupe de ressources nommé *myResourceGroup* Bonjour *eastus* région.

```azurecli-interactive
az group create --name myResourceGroup --location eastus
```

### <a name="create-a-vm"></a>Créer une machine virtuelle

toocreate un ordinateur virtuel basé sur l’image de base de données Oracle hello et configurez-le toouse Oracle ASM, utilisez hello [az vm créer](/cli/azure/vm#create) commande. 

Hello exemple suivant crée un ordinateur virtuel nommé myVM qui a une taille Standard_DS2_v2 avec quatre disques de données associés de 50 Go. Si elles n’existent pas déjà dans l’emplacement de la clé hello par défaut, il crée également des clés SSH.  toouse un ensemble spécifique de clés, utilisez hello `--ssh-key-value` option.  

   ```azurecli-interactive
   az vm create --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --generate-ssh-keys \
    --data-disk-sizes-gb 50 50 50 50
   ```

Après avoir créé la machine virtuelle de hello, CLI d’Azure affiche des informations similaires toohello est l’exemple suivant. Notez la valeur hello pour `publicIpAddress`. Vous utilisez cette hello de tooaccess adresse machine virtuelle.

   ```azurecli
   {
     "fqdns": "",
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
     "location": "eastus",
     "macAddress": "00-0D-3A-36-2F-56",
     "powerState": "VM running",
     "privateIpAddress": "10.0.0.4",
     "publicIpAddress": "13.64.104.241",
     "resourceGroup": "myResourceGroup"
   }
   ```

### <a name="connect-toohello-vm"></a>Se connecter toohello machine virtuelle

toocreate une session SSH avec hello de machine virtuelle et configurer des paramètres supplémentaires, utilisez hello commande suivante. Remplacer l’adresse IP de hello avec hello `publicIpAddress` valeur pour votre machine virtuelle.

```bash 
ssh <publicIpAddress>
```

## <a name="install-oracle-asm"></a>Installer Oracle ASM

tooinstall Oracle ASM, hello complète comme suit. 

Pour plus d’informations sur l’installation d’Oracle ASM, consultez [Oracle ASMLib Downloads for Oracle Linux 6](http://www.oracle.com/technetwork/server-storage/linux/asmlib/ol6-1709075.html).  

1. Vous devez toologin en tant que racine dans toocontinue d’ordre d’installation de ASM :

   ```bash
   sudo su -
   ```
   
2. Exécutez ces commandes supplémentaires des composants Oracle ASM tooinstall :

   ```bash
    yum list | grep oracleasm 
    yum -y install kmod-oracleasm.x86_64 
    yum -y install oracleasm-support.x86_64 
    wget http://download.oracle.com/otn_software/asmlib/oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    yum -y install oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    rm -f oracleasmlib-2.0.12-1.el6.x86_64.rpm
   ```

3. Vérifiez qu’Oracle ASM est installé :

   ```bash
   rpm -qa |grep oracleasm
   ```

    sortie Hello de cette commande doit répertorier hello suivant des composants :

    ```bash
   oracleasm-support-2.1.10-4.el6.x86_64
   kmod-oracleasm-2.0.8-15.el6_9.x86_64
   oracleasmlib-2.0.12-1.el6.x86_64
    ```

4. ASM requiert des utilisateurs spécifiques et les rôles dans l’ordre toofunction correctement. Hello suivant les commandes créer des groupes et comptes d’utilisateur requis hello : 

   ```bash
    groupadd -g 54345 asmadmin 
    groupadd -g 54346 asmdba 
    groupadd -g 54347 asmoper 
    useradd -u 3000 -g oinstall -G dba,asmadmin,asmdba,asmoper grid 
    usermod -g oinstall -G dba,asmdba,asmadmin oracle
   ```

5. Vérifiez que les utilisateurs et les groupes ont été créés correctement :

   ```bash
   id grid
   ```

    Hello sortie de cette commande doit répertorier les suivant hello utilisateurs et groupes :

    ```bash
    uid=3000(grid) gid=54321(oinstall) groups=54321(oinstall),54322(dba),54345(asmadmin),54346(asmdba),54347(asmoper)
    ```
 
6. Créez un dossier pour l’utilisateur *grille* et changer le propriétaire de hello :

   ```bash
   mkdir /u01/app/grid 
   chown grid:oinstall /u01/app/grid
   ```

## <a name="set-up-oracle-asm"></a>Configurer Oracle ASM

Pour ce didacticiel, hello utilisateur par défaut est *grille* et le groupe par défaut hello est *asmadmin*. Vérifiez que hello *oracle* utilisateur fait partie du groupe d’asmadmin hello. tooset votre installation Oracle ASM, hello complète comme suit :

1. Configuration d’un pilote de bibliothèque Oracle ASM hello implique la définition d’utilisateur par défaut de hello (grille) et le groupe par défaut (asmadmin), ainsi que la configuration hello lecteur toostart au démarrage du système (choisissez y) et tooscan de disques de démarrage (choisissez y). Vous avez besoin d’invites de hello tooanswer de hello de commande suivante :

   ```bash
   /usr/sbin/oracleasm configure -i
   ```

   sortie Hello de cette commande doit se présenter comme toohello suivant, l’arrêt avec toobe invites ayant obtenu une réponse.

    ```bash
   Configuring hello Oracle ASM library driver.

   This will configure hello on-boot properties of hello Oracle ASM library
   driver. hello following questions will determine whether hello driver is
   loaded on boot and what permissions it will have. hello current values
   will be shown in brackets ('[]'). Hitting <ENTER> without typing an
   answer will keep that current value. Ctrl-C will abort.

   Default user tooown hello driver interface []: grid
   Default group tooown hello driver interface []: asmadmin
   Start Oracle ASM library driver on boot (y/n) [n]: y
   Scan for Oracle ASM disks on boot (y/n) [y]: y
   Writing Oracle ASM library driver configuration: done
   ```

2. Afficher la configuration disque hello :
   ```bash
   cat /proc/partitions
   ```

   sortie Hello de cette commande doit ressembler similaire toohello suivant de la liste des disques disponibles

   ```bash
   8       16   14680064 sdb
   8       17   14678976 sdb1
   8        0   52428800 sda
   8        1     512000 sda1
   8        2   51915776 sda2
   8       48   52428800 sdd
   8       64   52428800 sde
   8       80   52428800 sdf
   8       32   52428800 sdc
   11       0       1152 sr0
   ```

3. Disque au format *sdc/dev/* en exécutant hello commande suivante et répondre aux hello invite avec :
   - *n* pour la nouvelle partition
   - *p* pour la partition principale
   - *1* première partition de hello tooselect
   - Appuyez sur `enter` pour le premier cylindre de hello par défaut
   - Appuyez sur `enter` pour le dernier cylindre de hello par défaut
   - Appuyez sur *w* table de partition toowrite hello modifications toohello  

   ```bash
   fdisk /dev/sdc
   ```
   
   Réponses hello fournis ci-dessus, sortie hello pour la commande de fdisk hello doit ressembler à celle de hello suivantes :

   ```bash
   Device contains not a valid DOS partition table, or Sun, SGI or OSF disklabel
   Building a new DOS disklabel with disk identifier 0xf865c6ca.
   Changes will remain in memory only, until you decide toowrite them.
   After that, of course, hello previous content won't be recoverable.

   Warning: invalid flag 0x0000 of partition table 4 will be corrected by w(rite)

   hello device presents a logical sector size that is smaller than
   hello physical sector size. Aligning tooa physical sector (or optimal
   I/O) size boundary is recommended, or performance may be impacted.

   WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
           switch off hello mode (command 'c') and change display units to
           sectors (command 'u').

   Command (m for help): n
   Command action
     e   extended
     p   primary partition (1-4)
   p
   Partition number (1-4): 1
   First cylinder (1-6527, default 1):
   Using default value 1
   Last cylinder, +cylinders or +size{K,M,G} (1-6527, default 6527):
   Using default value 6527

   Command (m for help): w
   hello partition table has been altered!

   Calling ioctl() toore-read partition table.
   Syncing disks.
   ```

4. Répétition hello précédant la commande fdisk pour `/dev/sdd`, `/dev/sde`, et `/dev/sdf`.

5. Vérifier la configuration de disque hello :

   ```bash
   cat /proc/partitions
   ```

   sortie Hello de commande hello doit ressembler à hello suivantes :

   ```bash
   major minor  #blocks  name

     8       16   14680064 sdb
     8       17   14678976 sdb1
     8       32   52428800 sdc
     8       33   52428096 sdc1
     8       48   52428800 sdd
     8       49   52428096 sdd1
     8       64   52428800 sde
     8       65   52428096 sde1
     8       80   52428800 sdf
     8       81   52428096 sdf1
     8        0   52428800 sda
     8        1     512000 sda1
     8        2   51915776 sda2
     11       0    1048575 sr0
   ```

6. Vérifiez l’état du service Oracle ASM hello et démarrer le service Oracle ASM hello :

   ```bash
   service oracleasm status 
   service oracleasm start
   ```

   sortie Hello de commande hello doit ressembler à hello suivantes :
   
   ```bash
   Checking if ASM is loaded: no
   Checking if /dev/oracleasm is mounted: no
   Initializing hello Oracle ASMLib driver:                     [  OK  ]
   Scanning hello system for Oracle ASMLib disks:               [  OK  ]
   ```

7. Créez les disques Oracle ASM :

   ```bash
   service oracleasm createdisk ASMSP /dev/sdc1 
   service oracleasm createdisk DATA /dev/sdd1 
   service oracleasm createdisk DATA1 /dev/sde1 
   service oracleasm createdisk FRA /dev/sdf1
   ```    

   sortie Hello de commande hello doit ressembler à hello suivantes :

   ```bash
   Marking disk "ASMSP" as an ASM disk:                       [  OK  ]
   Marking disk "DATA" as an ASM disk:                        [  OK  ]
   Marking disk "DATA1" as an ASM disk:                       [  OK  ]
   Marking disk "FRA" as an ASM disk:                         [  OK  ]
   ```

8. Répertoriez les disques Oracle ASM :

   ```bash
   service oracleasm listdisks
   ```   

   sortie Hello de commande hello doit répertorier off hello Oracle ASM disques suivants :

   ```bash
    ASMSP
    DATA
    DATA1
    FRA
   ```

9. Modifier les mots de passe hello pour les utilisateurs racine, oracle et grille hello. **Prenez note de ces nouveaux mots de passe** comme vous les utilisez plus tard pendant l’installation de hello.

   ```bash
   passwd oracle 
   passwd grid 
   passwd root
   ```

10. Modifier les autorisations de dossier hello :

   ```bash
   chmod -R 775 /opt 
   chown grid:oinstall /opt 
   chown oracle:oinstall /dev/sdc1 
   chown oracle:oinstall /dev/sdd1 
   chown oracle:oinstall /dev/sde1 
   chown oracle:oinstall /dev/sdf1 
   chmod 600 /dev/sdc1 
   chmod 600 /dev/sdd1 
   chmod 600 /dev/sde1 
   chmod 600 /dev/sdf1
   ```

## <a name="download-and-prepare-oracle-grid-infrastructure"></a>Télécharger et préparer Oracle Grid Infrastructure

toodownload et préparer des logiciels d’Infrastructure de grille Oracle hello, hello complète comme suit :

1. Télécharger l’Infrastructure de grille Oracle à partir de hello [page de téléchargement Oracle ASM](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/database12c-linux-download-2240591.html). 

   Sous Télécharger hello intitulée **Oracle Database 12C version 1 grille Infrastructure (12.1.0.2.0) pour Linux x86-64**, téléchargez les fichiers .zip hello deux.

2. Après avoir téléchargé hello .zip fichiers tooyour client ordinateur, vous pouvez utiliser Secure copie Protocol (SCP) toocopy hello fichiers tooyour machine virtuelle :

   ```bash
   scp *.zip <publicIpAddress>:.
   ```

3. SSH précédent dans votre machine virtuelle d’Oracle dans Azure dans les fichiers de commande toomove hello .zip dans hello / opt dossier. Ensuite, modifiez le propriétaire hello des fichiers de hello :

   ```bash
   ssh <publicIPAddress>
   sudo mv ./*.zip /opt
   cd /opt
   sudo chown grid:oinstall linuxamd64_12102_grid_1of2.zip
   sudo chown grid:oinstall linuxamd64_12102_grid_2of2.zip
   ```

4. Décompressez les fichiers hello. (Installation hello Linux décompressez outil s’il n’est pas déjà installé).
   
   ```bash
   sudo yum install unzip
   sudo unzip linuxamd64_12102_grid_1of2.zip
   sudo unzip linuxamd64_12102_grid_2of2.zip
   ```

5. Changez l’autorisation :
   
   ```bash
   sudo chown -R grid:oinstall /opt/grid
   ```

6. Mettez à jour l’espace d’échange configuré. Les composants de grille Oracle doivent au moins 6,8 Go d’espace de permutation tooinstall grille. taille de fichier d’échange Hello par défaut pour les images Oracle Linux dans Azure est uniquement 2 048 Mo. Vous devez tooincrease `ResourceDisk.SwapSizeMB` Bonjour `/etc/waagent.conf` de fichiers et de redémarrer hello WALinuxAgent service pour effet de tootake hello mis à jour les paramètres. S’agissant d’un fichier en lecture seule, vous avez besoin d’autorisations fichier toochange tooenable un accès en écriture.

   ```bash
   sudo chmod 777 /etc/waagent.conf  
   vi /etc/waagent.conf
   ```
   
   Recherchez `ResourceDisk.SwapSizeMB` et également de modifier la valeur de hello**8192**. Vous devez toopress `insert` tooenter en mode d’insertion, le type de valeur hello de **8192** , puis appuyez sur `esc` tooreturn toocommand mode. modifications de hello toowrite et quittez hello, type de fichier `:wq` et appuyez sur `enter`.
   
   > [!NOTE]
   > Il est vivement recommandé de toujours utiliser `WALinuxAgent` tooconfigure espace d’échange afin qu’il est toujours créé sur hello local éphémère disque temporaire pour de meilleures performances. Pour plus d’informations, consultez [comment tooadd un échange de fichiers dans des machines virtuelles Linux Azure](https://support.microsoft.com/en-us/help/4010058/how-to-add-a-swap-file-in-linux-azure-virtual-machines).

## <a name="prepare-your-local-client-and-vm-toorun-x11"></a>Préparer votre client local et la machine virtuelle toorun x11
Configuration d’Oracle ASM nécessite une interface graphique toocomplete hello installation et la configuration. Nous utilisons hello x11 protocole toofacilitate cette installation. Si vous utilisez un système client (Mac ou Linux) qui a déjà X11 fonctionnalités activé et configuré - vous pouvez ignorer cette configuration et le programme d’installation tooWindows exclusif machines. 

1. [Télécharger PuTTY](http://www.putty.org/) et [télécharger Xming](https://xming.en.softonic.com/) tooyour l’ordinateur Windows. Installation vous devez toocomplete hello de ces deux applications hello valeurs par défaut avant de continuer.

2. Après avoir installé PuTTY, ouvrez une invite de commandes en hello PuTTY dossier (par exemple, C:\Program Files\PuTTY) et modifier `puttygen.exe` commander toogenerate une clé.

3. Dans PuTTY Key Generator :
   
   1. Générer une clé en sélectionnant hello `Generate` bouton.
   2. Copier le contenu de hello de clé de hello (Ctrl + C).
   3. Sélectionnez hello `Save private key` bouton.
   4. Ignorer l’avertissement hello sur la sécurisation de clé hello avec un mot de passe, puis sélectionnez `OK`.

   ![Capture d’écran du générateur de clé PuTTY](./media/oracle-asm/puttykeygen.png)

4. Dans votre machine virtuelle, exécutez ces commandes :

   ```bash
   sudo su - grid
   mkdir .ssh 
   cd .ssh
   ```

5. Créez un fichier appelé `authorized_keys`. Collez le contenu hello de clé de hello dans ce fichier, puis enregistrez le fichier de hello.

   > [!NOTE]
   > clé de Hello doit contenir la chaîne de hello `ssh-rsa`. En outre, le contenu hello de clé de hello doit être une seule ligne de texte.
   >  

6. Sur votre système client, démarrez PuTTY. Bonjour **catégorie** volet, accédez trop**connexion** > **SSH** > **Auth**. Bonjour **fichier de clé privée pour l’authentification** , naviguez jusque toohello clé que vous avez créé précédemment.

   ![Capture d’écran des options d’authentification SSH hello](./media/oracle-asm/setprivatekey.png)

7. Bonjour **catégorie** volet, accédez trop**connexion** > **SSH** > **X11**. Sélectionnez hello **X11 d’activer le transfert** case à cocher.

   ![Capture d’écran de hello SSH X11 options de transfert](./media/oracle-asm/enablex11.png)

8. Bonjour **catégorie** volet, accédez trop**Session**. Entrez votre machine virtuelle ASM de Oracle `<publicIPaddress>` dans la boîte de dialogue Nom hôte hello renseigner un nouvel `Saved Session` nom, puis cliquez sur `Save`.  Une fois enregistré, cliquez sur `open` tooconnect tooyour Oracle ASM virtual machine.  Hello première connexion, vous recevez un avertissement système à distance de hello n’est pas mis en cache dans le Registre. Cliquez sur `yes` tooadd il et continuer.

   ![Capture d’écran des options de session PuTTY hello](./media/oracle-asm/puttysession.png)

## <a name="install-oracle-grid-infrastructure"></a>Installer Oracle Grid Infrastructure

tooinstall Infrastructure de grille Oracle, hello complète comme suit :

1. Connectez-vous en tant que **grid**. (Vous devez être en mesure de toosign dans sans être invité à entrer un mot de passe.) 

   > [!NOTE]
   > Si vous exécutez Windows, assurez-vous que vous avez démarré Xming avant de commencer l’installation de hello.

   ```bash
   cd /opt/grid
   ./runInstaller
   ```

   Le programme d’installation d’Oracle Grid Infrastructure 12c Release 1 s’ouvre. (Il peut prendre quelques minutes pour toostart du programme d’installation hello.)

2. Sur hello **sélectionner l’Option Installation** , sélectionnez **installez et configurez l’Infrastructure de grille Oracle pour un serveur autonome**.

   ![Capture d’écran de la page de sélectionner l’Option Installation hello du programme d’installation](./media/oracle-asm/install01.png)

3. Sur hello **sélectionner les langues de produits** , vérifiez **anglais** ou langue hello de votre choix est sélectionné.  Cliquez sur `next`.

4. Sur hello **créer un groupe de disques ASM** page :
   - Entrez un nom pour le groupe de disques hello.
   - Sous **Redundancy** (Redondance), sélectionnez **External** (Externe).
   - Sous **Allocation Unit Size** (Taille d’unité d’allocation), sélectionnez **4**.
   - Sous **Add Disks** (Ajouter des disques), sélectionnez **ORCLASMSP**.
   - Cliquez sur `next`.

5. Sur hello **spécifier le mot de passe ASM** page, sélectionnez hello **utiliser les mêmes mots de passe pour ces comptes** , puis entrez un mot de passe.

   ![Capture d’écran de la page de spécifier le mot de passe ASM hello du programme d’installation](./media/oracle-asm/install04.png)

6. Sur hello **spécifier les Options de gestion** page, vous avez hello option tooconfigure EM Cloud contrôle. Cette option est ignorée, cliquez `next` toocontinue. 

7. Sur hello **groupes privilégiés de système d’exploitation** page, les paramètres par défaut hello. Cliquez sur `next` toocontinue.

8. Sur hello **spécifier l’emplacement d’Installation** page, les paramètres par défaut hello. Cliquez sur `next` toocontinue.

9. Sur hello **créer un inventaire** , changez hello inventaire active trop`/u01/app/grid/oraInventory`. Cliquez sur `next` toocontinue.

   ![Capture d’écran de la page Créer un inventaire de hello du programme d’installation](./media/oracle-asm/install08.png)

10. Sur hello **configuration de l’exécution de script racine** page, sélectionnez hello **exécuter automatiquement les scripts de configuration** case à cocher. Ensuite, sélectionnez hello **utiliser les informations d’identification utilisateur de « root »** , puis entrez le mot de passe utilisateur hello racine.

    ![Capture d’écran de la page de configuration de l’exécution du programme d’installation hello racine script](./media/oracle-asm/install09.png)

11. Sur hello **effectuer Prerequisite Checks** la page, le programme d’installation en cours de hello échouera avec des erreurs. Ce comportement est normal. Sélectionnez `Fix & Check Again`.

12. Bonjour **Script de correction** boîte de dialogue, cliquez sur `OK`.

13. Sur hello **Résumé** page, passez en revue les paramètres sélectionnés, puis cliquez sur `Install`.

    ![Capture d’écran de la page de résumé hello du programme d’installation](./media/oracle-asm/install12.png)

14. Une boîte de dialogue d’avertissement s’affiche pour signaler les scripts de configuration vous devez toobe exécuter en tant qu’un utilisateur doté de privilèges. Cliquez sur `Yes` toocontinue.

15. Sur hello **Terminer** , cliquez sur `Close` installation de hello toofinish.

## <a name="set-up-your-oracle-asm-installation"></a>Configurer votre installation Oracle ASM

tooset votre installation Oracle ASM, hello complète comme suit :

1. Vérifiez que vous êtes toujours connecté en tant que **grid** à partir de votre session X11. Vous devrez peut-être toohit `enter` hello toorevive Terminal Server. Puis lancez hello Oracle automatisée stockage gestion Assistant de Configuration :

   ```bash
   cd /u01/app/grid/product/12.1.0/grid/bin
   ./asmca
   ```

   L’Assistant de configuration d’Oracle ASM s’ouvre.

2. Bonjour **configurer un ASM : groupes de disques** boîte de dialogue, cliquez sur hello `Create` bouton, puis cliquez sur `Show Advanced Options`.

3. Bonjour **créer un groupe de disques** boîte de dialogue :

   - Entrez le nom du groupe hello disque **données**.
   - Sous **Select Member Disks** (Sélectionner les disques membres), sélectionnez **ORCL_DATA** et **ORCL_DATA1**.
   - Sous **Allocation Unit Size** (Taille d’unité d’allocation), sélectionnez **4**.
   - Cliquez sur `ok` le groupe de disques toocreate hello.
   - Cliquez sur `ok` fenêtre de confirmation tooclose hello.

   ![Capture d’écran de la boîte de dialogue Créer un groupe de disques hello](./media/oracle-asm/asm02.png)

4. Bonjour **configurer un ASM : groupes de disques** boîte de dialogue, cliquez sur hello `Create` bouton, puis cliquez sur `Show Advanced Options`.

5. Bonjour **créer un groupe de disques** boîte de dialogue :

   - Entrez le nom du groupe hello disque **FRA**.
   - Sous **Redundancy** (Redondance), sélectionnez **External (none)** (Externe (aucun)).
   - Sous **Select Member Disks** (Sélectionner les disques membres), sélectionnez **ORCL_FRA**.
   - Sous **Allocation Unit Size** (Taille d’unité d’allocation), sélectionnez **4**.
   - Cliquez sur `ok` le groupe de disques toocreate hello.
   - Cliquez sur `ok` fenêtre de confirmation tooclose hello.

   ![Capture d’écran de la boîte de dialogue Créer un groupe de disques hello](./media/oracle-asm/asm04.png)

6. Sélectionnez **Exit** tooclose ASM l’Assistant Configuration.

   ![Capture d’écran de hello ASM de configurer : boîte de dialogue de groupes de disques avec le bouton Quitter](./media/oracle-asm/asm05.png)

## <a name="create-hello-database"></a>Créer la base de données hello

Hello logiciel de base de données Oracle est déjà installé sur l’image d’Azure Marketplace hello. toocreate une base de données, hello complète comme suit :

1. Basculez superutilisateur de Oracle toohello utilisateurs et puis initialisez écouteur hello pour l’enregistrement :

   ```bash
   su - oracle
   cd /u01/app/oracle/product/12.1.0/dbhome_1/bin
   ./dbca
   ```
   L’Assistant de configuration de base de données s’ouvre.

2. Sur hello **opération de base de données** , cliquez sur `Create Database`.

3. Sur hello **Mode de création de** page :

   - Entrez un nom pour la base de données hello.
   - Pour **Storage Type** (Type de stockage), assurez-vous que l’option **Automatic Storage Management (ASM)** est sélectionnée.
   - Pour **emplacement des fichiers de base de données**, utiliser la valeur par défaut hello ASM suggéré emplacement.
   - Pour **zone de récupération rapide**, utiliser la valeur par défaut hello ASM suggéré emplacement.
   - Saisissez un **mot de passe administrateur** et **confirmez le mot de passe**.
   - Vérifiez que l’option `create as container database` est sélectionnée.
   - Saisissez une valeur pour `pluggable database name`.

4. Sur hello **Résumé** page, passez en revue les paramètres sélectionnés, puis cliquez sur `Finish` base de données toocreate hello.

   ![Capture d’écran de la page de résumé hello](./media/oracle-asm/createdb03.png)

5. Hello de base de données a été créé. Sur hello **Terminer** page, vous avez hello option toounlock des comptes supplémentaires toouse cette base de données et modifier les mots de passe hello. Si vous souhaitez donc toodo, sélectionnez **gestion de mot de passe** -Cliquez sinon sur `close`.

## <a name="delete-hello-vm"></a>Supprimer hello machine virtuelle

Vous avez correctement configuré la gestion du stockage automatisé Oracle sur l’image de base de données Oracle hello de hello Azure Marketplace.  Lorsque vous ne devez plus cet ordinateur virtuel, vous pouvez utiliser hello suivant du groupe de ressources de commande tooremove hello, machine virtuelle et toutes les ressources :

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Étapes suivantes

[Didacticiel : Configurer Oracle DataGuard](configure-oracle-dataguard.md)

[Didacticiel : Configurer Oracle GoldenGate](Configure-oracle-golden-gate.md)

Revoir [Créer l’architecture d’une base de données Oracle](oracle-design.md)
