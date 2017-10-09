Si votre machine virtuelle (VM) dans Azure rencontre une erreur de démarrage ou de disque, vous devrez peut-être tooperform étapes de dépannage sur le disque dur virtuel hello lui-même. Un exemple courant est une mise à jour d’application qui a échoué qui empêche les hello machine virtuelle de démarrer correctement. Cet article décrit comment toouse tooconnect portail Azure votre toofix de machine virtuelle de disque dur virtuel tooanother toutes les erreurs, puis recréer votre machine virtuelle d’origine.

## <a name="recovery-process-overview"></a>Vue d’ensemble du processus de récupération
Hello, résolution des problèmes de processus est la suivante :

1. Supprimer hello machine virtuelle qui rencontre des problèmes, mais conserver les disques durs virtuels hello.
2. Attacher et monter tooanother de disque dur virtuel hello machine virtuelle pour le dépannage.
3. Se connecter toohello résolution des problèmes de la machine virtuelle. Modifier des fichiers ou d’exécuter les outils toofix erreurs sur les disque dur virtuel d’origine hello.
4. Démontez et détacher le disque dur virtuel de hello de hello, résolution des problèmes de la machine virtuelle.
5. Créer une machine virtuelle à l’aide de hello d’origine disque dur.

## <a name="delete-hello-original-vm"></a>Supprimer hello d’ordinateur virtuel d’origine
Les disques durs virtuels et les machines virtuelles sont deux ressources distinctes dans Azure. Un disque dur virtuel consiste à stocker des configurations, des applications et système d’exploitation de hello. Hello machine virtuelle est simplement des métadonnées qui définit la taille de hello ou l’emplacement et qui fait référence à des ressources, tel qu’un disque dur virtuel ou d’une carte réseau virtuelle (NIC). Chaque disque dur virtuel Obtient un bail affecté lors de ce disque est attaché tooa machine virtuelle. Bien que les disques de données peuvent être attachées et détachées même pendant l’exécution de la machine virtuelle de hello, les disques du système d’exploitation hello ne peut pas être détachée tant que hello ressource d’ordinateur virtuel est supprimé. bail de Hello continue tooassociate hello du système d’exploitation disque tooa machine virtuelle, même lorsque l’ordinateur virtuel est dans un état arrêté et est libéré.

Hello première étape toorecovering votre machine virtuelle est la ressource d’ordinateur virtuel hello toodelete lui-même. Suppression hello VM laisse hello des disques durs virtuels dans votre compte de stockage. Après hello que machine virtuelle est supprimée, vous pouvez attacher hello disque dur virtuel tooanother VM tootroubleshoot et résoudre les erreurs de hello. 

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com). 
2. Dans le menu hello hello situé à gauche, cliquez sur **Machines virtuelles (classiques)**.
3. Cliquez sur la machine virtuelle qui possède le problème de hello, sélectionnez hello **disques**, puis identifiez le nom hello du disque dur virtuel de hello. 
4. Sélectionnez un disque dur virtuel hello du système d’exploitation et vérifier hello **emplacement** compte de stockage hello tooidentify qui contient ce disque dur virtuel. Dans l’exemple suivant de hello, hello chaîne immédiatement avant «. blob.core.windows.net » est le nom de compte de stockage hello.

    ```
    https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd
    ```

    ![image Hello sur l’emplacement de la machine virtuelle](./media/virtual-machines-classic-recovery-disks-portal/vm-location.png)

5. Avec le bouton droit hello machine virtuelle, puis sélectionnez **supprimer**. Assurez-vous que les disques de hello ne sont pas activées lorsque vous supprimez hello machine virtuelle.
6. Créez une nouvelle machine virtuelle de récupération. Cet ordinateur virtuel doit être Bonjour même région et ressource groupe (Service Cloud) en tant que le problème hello machine virtuelle.
7. Sélectionnez l’ordinateur virtuel de récupération hello et sélectionnez **disques** > **attacher existant**.
8. tooselect votre disque dur virtuel existant, cliquez sur **fichier de disque dur virtuel**:

    ![Rechercher le disque dur virtuel existant](./media/virtual-machines-classic-recovery-disks-portal/select-vhd-location.png)

9. Sélectionnez le compte de stockage hello > conteneur de disque dur virtuel > hello du disque dur virtuel, cliquez sur hello **sélectionnez** bouton tooconfirm votre choix.

    ![Sélectionner votre disque dur virtuel existant](./media/virtual-machines-classic-recovery-disks-portal/select-vhd.png)

10. Sélectionnez votre disque dur virtuel est maintenant sélectionné, **OK** tooattach hello disque dur virtuel existant.
11. Après quelques secondes, hello **disques** volet pour votre machine virtuelle affiche votre disque dur virtuel existant connecté en tant qu’un disque de données :

    ![Disque dur virtuel existant attaché en tant que disque de données](./media/virtual-machines-classic-recovery-disks-portal/attached-disk.png)

## <a name="fix-issues-on-hello-original-virtual-hard-disk"></a>Résoudre les problèmes sur les disque dur virtuel d’origine hello
Lorsque le disque dur virtuel existant hello est monté, vous pouvez désormais effectuer une maintenance et dépannage en fonction des besoins. Une fois que vous avez corrige les problèmes de hello, poursuivez hello comme suit.

## <a name="unmount-and-detach-hello-original-virtual-hard-disk"></a>Démontez et détacher les disque dur virtuel d’origine hello
Une fois toutes les erreurs résolues, démontez et détacher hello disque dur virtuel existant à partir de votre machine virtuelle de résolution des problèmes. Vous ne pouvez pas utiliser votre disque dur virtuel avec tout autre ordinateur virtuel jusqu'à ce que le bail hello qui relie des toohello de disque dur virtuel hello résolution des problèmes de la machine virtuelle est libéré.  

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com). 
2. Dans le menu hello hello situé à gauche, sélectionnez **Machines virtuelles (classiques)**.
3. Localisez l’ordinateur virtuel de récupération hello. Sélectionnez les disques, disque de hello avec le bouton droit, puis **détachement**.

## <a name="create-a-vm-from-hello-original-hard-disk"></a>Créer une machine virtuelle à partir du disque dur d’origine de hello

utilisation d’une machine virtuelle à partir de votre disque dur virtuel d’origine, toocreate [portail Azure classic](https://manage.windowsazure.com).

1. Connectez-vous au [portail Azure Classic](https://manage.windowsazure.com).
2. Au bas de hello du portail de hello, sélectionnez **nouveau** > **de calcul** > **Machine virtuelle** > **à partir de la galerie** .
3. Bonjour **choisir une Image** section, sélectionnez **mes disques**, et puis sélectionnez hello d’origine de disque dur virtuel. Vérifiez les informations d’emplacement hello. Il s’agit de région de hello où hello machine virtuelle doit être déployé. Sélectionnez le bouton suivant de hello.
4. Bonjour **configuration d’ordinateur virtuel** section, tapez le nom d’ordinateur virtuel hello et sélectionnez une taille pour hello machine virtuelle.
