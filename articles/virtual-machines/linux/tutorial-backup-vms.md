---
title: Sauvegarder des machines virtuelles Linux Azure | Microsoft Docs
description: "Protégez vos machines virtuelles Linux en les sauvegardant à l’aide d’Azure Backup."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/27/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 7c00392d5185a2f067f2ee2717529dcbde1e71f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-linux--virtual-machines-in-azure"></a>Sauvegarder des machines virtuelles Linux dans Azure

Vous pouvez protéger vos données en effectuant des sauvegardes à intervalles réguliers. Azure Backup crée des points de récupération stockés dans des coffres de récupération géoredondants. Lorsque vous restaurez à partir d’un point de récupération, vous pouvez restaurer hello toute machine virtuelle ou des fichiers spécifiques. Cet article explique comment toorestore un seul fichier tooa nginx en cours d’exécution de Linux VM. Si vous n’avez pas encore un toouse de machine virtuelle, vous pouvez en créer un à l’aide de hello [Linux quickstart](quick-create-cli.md). Ce didacticiel vous explique comment effectuer les opérations suivantes :

> [!div class="checklist"]
> * Créer une sauvegarde de machine virtuelle
> * Planifier une sauvegarde quotidienne
> * Restaurer un fichier à partir d’une sauvegarde



## <a name="backup-overview"></a>Présentation de la sauvegarde

Hello service Azure Backup lorsqu’une sauvegarde, il déclenche hello extension de sauvegarde tootake un instantané de point-à-temps. Hello service Azure Backup utilise hello _VMSnapshotLinux_ extension dans Linux. extension de Hello est installée au cours de la première sauvegarde de machine virtuelle hello si hello machine virtuelle est en cours d’exécution. Si hello machine virtuelle ne fonctionne pas, hello service de sauvegarde prend un instantané de hello stockage sous-jacent (dans la mesure où aucune écriture de l’application se produire lors de la machine virtuelle est arrêtée de hello).

Par défaut, Azure Backup prend une sauvegarde cohérente de système de fichiers pour Linux VM, mais il peut être configuré tootake [sauvegarde cohérente d’application à l’aide du script avant et après script framework](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent). Une fois que hello service Azure Backup prend un instantané de hello, données de hello sont transférées toohello coffre. l’efficacité toomaximize, hello service identifie et transfère uniquement les blocs de hello de données qui ont été modifiés depuis la sauvegarde précédente de hello.

Lorsque le transfert de données hello est terminé, les instantanés hello sont supprimé et un point de récupération est créé.


## <a name="create-a-backup"></a>Création d'une sauvegarde
Créer une simple planifiée quotidienne sauvegarde tooa coffre Recovery Services. 

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).
2. Dans le menu hello hello gauche, sélectionnez **virtuels**. 
3. À partir de la liste de hello, sélectionnez un tooback de machine virtuelle.
4. Dans Panneau de machine virtuelle hello, Bonjour **paramètres** , cliquez sur **sauvegarde**. Hello **Active la sauvegarde** panneau s’ouvre.
5. Dans **de coffre Recovery Services**, cliquez sur **nouvel** et fournir le nom hello pour le coffre hello. Un nouvel archivage est créé dans hello même groupe de ressources et l’emplacement en tant que machine virtuelle de hello.
6. Cliquez sur **Stratégie de sauvegarde**. Pour cet exemple, conservez les valeurs par défaut hello et cliquez sur **OK**.
7. Sur hello **Active la sauvegarde** panneau, cliquez sur **activez la sauvegarde**. Cette opération crée une sauvegarde quotidienne selon une planification par défaut hello.
10. toocreate un point de récupération initial sur hello **sauvegarde** cliquez sur le panneau **sauvegarder maintenant**.
11. Sur hello **sauvegarde maintenant** panneau, cliquez sur icône du calendrier hello, utilisez Bonjour calendrier contrôle tooselect Bonjour dernier jour de ce point de récupération est conservé, puis cliquez sur **sauvegarde**.
12. Bonjour **sauvegarde** panneau pour votre machine virtuelle, vous verrez nombre hello de points de récupération qui sont terminées.

    ![Points de récupération](./media/tutorial-backup-vms/backup-complete.png)

première sauvegarde de Hello prend environ 20 minutes. Continuer toohello la partie suivante de ce didacticiel, une fois la sauvegarde terminée.

## <a name="restore-a-file"></a>Restaurer un fichier

Si vous supprimez ou rendre le fichier tooa des modifications, vous pouvez utiliser le fichier de récupération de fichier toorecover hello votre coffre de sauvegarde. Récupération de fichiers utilise un script qui s’exécute sur hello machine virtuelle, point de récupération toomount hello en tant que lecteur local. Ces lecteurs restera montés pendant 12 heures, afin que vous pouvez copier les fichiers de point de récupération hello et restaurez-les toohello machine virtuelle.  

Dans cet exemple, nous montrons comment toorecover hello par défaut nginx page web /var/www/html/index.nginx-debian.html. Hello une adresse IP publique de votre machine virtuelle dans cet exemple est *13.69.75.209*. Vous pouvez trouver l’adresse IP de hello de votre machine virtuelle à l’aide :

 ```bash 
 az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
 ```

 
1. Sur votre ordinateur local, ouvrez un navigateur et tapez dans hello adresse IP publique de votre page web de machine virtuelle toosee hello par défaut nginx.

    ![Page web nginx par défaut](./media/tutorial-backup-vms/nginx-working.png)

1. Connectez-vous avec SSH à votre machine virtuelle.

    ```bash
    ssh 13.69.75.209
    ```
2. Supprimez /var/www/html/index.nginx-debian.html.

    ```bash
    sudo rm /var/www/html/index.nginx-debian.html
    ```
    
4. Sur votre ordinateur local, actualisez le navigateur de hello en appuyant sur CTRL + F5 toosee qui nginx page par défaut a disparu.

    ![Page web nginx par défaut](./media/tutorial-backup-vms/nginx-broken.png)
    
1. Sur votre ordinateur local, connectez-vous en toohello [portail Azure](https://portal.azure.com/).
6. Dans le menu hello hello gauche, sélectionnez **virtuels**. 
7. Dans la liste hello, sélectionnez hello machine virtuelle.
8. Dans Panneau de machine virtuelle hello, Bonjour **paramètres** , cliquez sur **sauvegarde**. Hello **sauvegarde** panneau s’ouvre. 
9. Dans le menu hello haut hello du Panneau de hello, sélectionnez **récupération de fichier**. Hello **récupération de fichier** panneau s’ouvre.
10. Dans **étape 1 : sélectionnez le point de récupération**, sélectionnez un point de récupération à partir de hello de liste déroulante.
11. Dans **étape 2 : télécharger le script toobrowse et récupérer les fichiers**, cliquez sur hello **télécharger le fichier exécutable** bouton. Enregistrer l’ordinateur local du tooyour hello fichier téléchargé.
7. Cliquez sur **télécharger le script** fichier de script hello toodownload localement.
8. Ouvrez un Bonjour Bash invite et le type suivant, en remplaçant *Linux_myVM_05-05-2017.sh* avec hello corriger le chemin d’accès et nom de fichier de script hello que vous avez téléchargé, *azureuser* UserName hello pour hello machine virtuelle et *13.69.75.209* avec l’adresse IP publique de hello pour votre machine virtuelle.
    
    ```bash
    scp Linux_myVM_05-05-2017.sh azureuser@13.69.75.209:
    ```
    
9. Sur votre ordinateur local, ouvrez un toohello de connexion SSH machine virtuelle.

    ```bash
    ssh 13.69.75.209
    ```
    
10. Sur votre machine virtuelle, ajoutez d’exécuter le fichier de script toohello autorisations.

    ```bash
    chmod +x Linux_myVM_05-05-2017.sh
    ```
    
11. Sur votre machine virtuelle, exécutez le point de récupération hello hello script toomount comme un système de fichiers.

    ```bash
    ./Linux_myVM_05-05-2017.sh
    ```
    
12. Hello de sortie à partir de l’offre de script hello que Hello de chemin d’accès pour le point de montage hello. sortie de Hello ressemble toothis similaire :

    ```bash
    Microsoft Azure VM Backup - File Recovery
    ______________________________________________
                          
    Connecting toorecovery point using ISCSI service...
    
    Connection succeeded!
    
    Please wait while we attach volumes of hello recovery point toothis machine...
                         
    ************ Volumes of hello recovery point and their mount paths on this machine ************

    Sr.No.  |  Disk  |  Volume  |  MountPath 

    1)  | /dev/sdc  |  /dev/sdc1  |  /home/azureuser/myVM-20170505191055/Volume1

    ************ Open File Explorer toobrowse for files. ************

    After recovery, tooremove hello disks and close hello connection toohello recovery point, please click 'Unmount Disks' in step 3 of hello portal.

    Please enter 'q/Q' tooexit...
    ```

12. Sur votre machine virtuelle, copiez la page web de hello nginx par défaut à partir de toowhere arrière du point de montage hello vous avez supprimé les fichier hello.

    ```bash
    sudo cp ~/myVM-20170505191055/Volume1/var/www/html/index.nginx-debian.html /var/www/html/
    ```
    
17. Sur votre ordinateur local, ouvrez l’onglet de navigateur hello où vous êtes connecté adresse toohello de hello VM écran hello nginx par défaut de la page. Appuyez sur CTRL + F5 page du navigateur toorefresh hello. Vous devez maintenant voir que hello page par défaut fonctionne à nouveau.

    ![Page web nginx par défaut](./media/tutorial-backup-vms/nginx-working.png)

18. Sur votre ordinateur local, revenir en arrière toohello onglet du navigateur pour hello portail Azure et dans **étape 3 : démontage de disques de hello après la récupération** cliquez sur hello **démontage de disques** bouton. Si vous oubliez toodo cette étape, point de montage toohello hello connexion est automatiquement fermée après 12 heures. Après les 12 heures, vous devez toodownload une nouvelle toocreate de script un nouveau point de montage.


## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez appris à :

> [!div class="checklist"]
> * Créer une sauvegarde de machine virtuelle
> * Planifier une sauvegarde quotidienne
> * Restaurer un fichier à partir d’une sauvegarde

Avance toohello toolearn de didacticiel suivant sur l’analyse des ordinateurs virtuels.

> [!div class="nextstepaction"]
> [Surveiller les machines virtuelles](tutorial-monitoring.md)

