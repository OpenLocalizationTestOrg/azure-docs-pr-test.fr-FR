1. Connectez-vous à toohello [portail Azure classic](http://manage.windowsazure.com).  
2. Dans la barre de commandes hello bas hello de fenêtre hello, cliquez sur **nouveau**.
3. Sous **Calculer**, cliquez sur **Machine virtuelle**, puis sur **À partir de la galerie**.
   
    ![Créer une machine virtuelle][Image1]
4. Sous hello **SUSE** de groupe, sélectionnez une image de machine virtuelle OpenSUSE, puis cliquez sur hello flèche toocontinue.
5. Sur hello première **configuration d’ordinateur virtuel** page :
   
   * Entrez le **Nom de la machine virtuelle**, par exemple, « testlinuxvm ». Hello doit contenir entre 3 et 15 caractères, peut contenir uniquement des lettres, des chiffres et des traits d’union et doit commencer par une lettre et se terminer par une lettre ou un chiffre.
   * Vérifiez que hello **couche** et choisir un **taille**. couche de Hello détermine que vous pouvez choisir parmi des tailles de hello. Hello taille affecte hello coût d’utilisation, ainsi que des options de configuration telles que le nombre de disques de données vous pouvez attacher. Pour en savoir plus, voir la rubrique [Tailles de machines virtuelles](../articles/virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
   * Tapez un **nouveau nom d’utilisateur**, ou acceptez la valeur par défaut de hello, **azureuser**. Ce nom est ajouté le fichier de liste de programmes sudo toohello.
   * Décider quel type de **authentification** toouse. Pour obtenir des instructions générales sur les mots de passe, consultez la rubrique [Mots de passe forts](http://msdn.microsoft.com/library/ms161962.aspx).
6. Sur hello suivant **configuration d’ordinateur virtuel** page :
   
   * Utiliser la valeur par défaut hello **créer un service cloud**.
   * Bonjour **nom DNS** , tapez un toouse de nom DNS unique dans le cadre de l’adresse hello, tels que « testlinuxvm ».
   * Bonjour **régions ou d’affinités groupe/réseau virtuel** , sélectionnez une région où cette image virtuelle sera hébergée.
   * Sous **points de terminaison**, conservez le point de terminaison SSH hello. Vous pouvez ajouter d’autres à présent, ajouter, modifier ou les supprimer après la création d’ordinateur virtuel de hello.
     
     > [!NOTE]
     > Si vous souhaitez un toouse de machine virtuelle un réseau virtuel, vous **doit** spécifier le réseau virtuel de hello lorsque vous créez la machine virtuelle de hello. Vous ne pouvez pas ajouter un réseau virtuel de machine virtuelle tooa après avoir créé l’ordinateur virtuel de hello. Pour en savoir plus, consultez [Vue d’ensemble d’Azure Virtual Network](../articles/virtual-network/virtual-networks-overview.md).
     > 
     > 
7. Sur hello dernière **configuration d’ordinateur virtuel** page, conservez les paramètres par défaut de hello et puis cliquez sur toofinish de case à cocher hello.

portail Hello répertorie hello machine virtuelle sous **virtuels**. Alors que l’état de hello est signalée comme **(approvisionnement)**, ordinateur virtuel de hello est configuré. Lorsque l’état de hello est signalée comme **en cours d’exécution**, vous pouvez déplacer sur l’étape suivante de toohello.

## <a name="connect-toohello-virtual-machine"></a>Se connecter toohello Machine virtuelle
Vous allez utiliser SSH ou PuTTY tooconnect toohello machine virtuelle, en fonction du système d’exploitation de hello sur ordinateur hello de que vous vous connectez à partir :

* À partir d'un ordinateur exécutant Linux, utilisez SSH. À l’invite de commandes hello, tapez :
  
    `$ ssh newuser@testlinuxvm.cloudapp.net -o ServerAliveInterval=180`
  
    Tapez le mot de passe de l’utilisateur hello.
* À partir d'un ordinateur exécutant Windows, utilisez PuTTY. Si vous n’avez pas installé, le télécharger à partir de hello [Page de téléchargement de PuTTY][PuTTYDownload].
  
    Enregistrer **putty.exe** répertoire tooa sur votre ordinateur. Ouvrez une invite de commandes, accédez toothat dossier et exécuter **putty.exe**.
  
    Tapez le nom d’hôte hello, tels que « testlinuxvm.cloudapp.net » et « 22 » pour hello **Port**.
  
    ![Écran PuTTY][Image6]  

## <a name="update-hello-virtual-machine-optional"></a>Mettre à jour hello ordinateur virtuel (facultatif)
1. Une fois que vous êtes connecté toohello virtual machine, vous pouvez éventuellement installer les correctifs et mises à jour du système. toorun hello mise à jour, type :
   
    `$ sudo zypper update`
2. Sélectionnez **logiciel**, puis **mise à jour en ligne** mises à jour toolist. Sélectionnez **accepter** toostart hello installation et tous les correctifs disponibles nouveau (sauf hello arguments facultatifs).
3. Une fois l’installation terminée, sélectionnez **Terminer**.  Votre système est désormais toodate.

[PuTTYDownload]: http://www.puttyssh.org/download.html

[Image1]: ./media/create-and-configure-opensuse-vm-in-portal/CreateVM.png

[Image6]: ./media/create-and-configure-opensuse-vm-in-portal/putty.png
