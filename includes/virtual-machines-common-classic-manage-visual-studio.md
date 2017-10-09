Vous pouvez créer des machines virtuelles dans Azure à l’aide de l’Explorateur de serveurs de Visual Studio.

## <a name="create-an-azure-virtual-machine-in-server-explorer"></a>Créer une machine virtuelle Azure dans l’Explorateur de serveurs
Si vous pouvez créer une machine virtuelle Bonjour [portail de gestion Azure](http://go.microsoft.com/fwlink/?LinkID=253103), vous pouvez également créer une machine virtuelle dans Azure à l’aide des commandes dans l’Explorateur de serveurs. Machines virtuelles peuvent être utilisées, par exemple, tooprovide devant se terminer derrière un équilibrage de charge public point de terminaison commun.

### <a name="toocreate-a-new-virtual-machine"></a>toocreate un nouvel ordinateur virtuel
1. Dans l’Explorateur de serveurs, ouvrez hello **Azure** nœud et cliquez sur **virtuels**.
2. Dans le menu contextuel de hello, cliquez sur **créer un ordinateur virtuel**.
   
    Hello **créer une Machine virtuelle** Assistant s’affiche.
   
    ![Hello commande de créer un ordinateur virtuel](./media/virtual-machines-common-classic-create-manage-visual-studio/IC718342.png)
3. Sur hello **choisir un abonnement** page, sélectionnez un abonnement toouse lors de la création d’ordinateur virtuel de hello, puis sur **suivant**.
   
    Si vous n’êtes pas connecté dans tooAzure, cliquez sur **connexion** toosign dans. Ensuite, sélectionnez votre abonnement Azure dans la zone de liste déroulante hello s’il n’est pas déjà sélectionné.
4. Sur hello **sélectionner une Image de Machine virtuelle** , sélectionnez un type d’image Bonjour **type d’Image** déroulante zone de liste, puis sélectionnez un images de machine virtuelle Bonjour **nom de l’Image** zone de liste. Quand vous avez terminé, cliquez sur **Suivant**.
   
    ![Page Sélectionner une image de machine virtuelle](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744137.png)
   
    Vous pouvez choisir hello les types d’image suivants.
   
   * **Images publiques** : images de machines virtuelles des systèmes d’exploitation et des logiciels serveurs, tels que Windows Server et SQL Server.
   * **Images MSDN** répertorie les images de machine virtuelle d’abonnés tooMSDN disponible de logiciels, tels que Visual Studio et Microsoft Dynamics.
   * **Images privées** : images de machines virtuelles spécialisées et généralisées que vous avez créées.
     
     toolearn sur spécialisées et généralisées des machines virtuelles, consultez [Image de machine virtuelle](https://azure.microsoft.com/blog/2014/04/14/vm-image-blog-post/). Consultez [comment tooCapture un tooUse de Machine virtuelle Windows en tant que modèle](https://azure.microsoft.com/documentation/articles/virtual-machines-capture-image-windows-server/) pour plus d’informations sur la tooturn créer un ordinateur virtuel dans un modèle que vous pouvez utiliser tooquickly configuration des machines virtuelles.
     
     Vous pouvez cliquer sur une machine virtuelle image nom toosee informations sur hello image sur hello droite de la page de hello.
     
     > [!NOTE]
     > Vous ne pouvez pas ajouter toohello des images de machine virtuelle **Images publiques** ou **Images MSDN** répertorie parce qu’ils sont en lecture seule. Tous les ordinateurs virtuels que vous créez sont ajoutés toohello **Images privées** liste.
     > 
     > 
     
     Si vous êtes un abonné MSDN avec un abonnement de niveau Visual Studio, vous pouvez créer une machine virtuelle Azure préconfigurée contenant Visual Studio, ainsi que plusieurs autres images. Pour plus d’informations, consultez l’article concernant la [création d’une machine virtuelle dans Visual Studio à l’aide de la galerie d’images Visual Studio 2013 pour les abonnés MSDN](http://visualstudio2013msdngalleryimage.azurewebsites.net) et le site relatif aux [abonnements MSDN](https://www.visualstudio.com/products/msdn-subscriptions-vs).|
5. Sur hello **les paramètres de base de Machine virtuelle** page, entrez un nom d’ordinateur et ajoutez ensuite des spécifications hello pour l’ordinateur virtuel de hello, y compris la taille de hello et un nom d’utilisateur et le mot de passe. Quand vous avez terminé, cliquez sur **Suivant**.
   
    Vous allez utiliser le nouveau nom de hello et toolog de mot de passe dans la machine hello à l’aide du Bureau à distance, afin qu’il soit un toowrite conseillé les vers le bas dans le cas où vous avez oublié. Après avoir créé une machine virtuelle Azure dans Visual Studio, vous pouvez modifier sa taille et autres paramètres Bonjour [portail de gestion Azure](http://go.microsoft.com/fwlink/?LinkID=253103).
   
   > [!NOTE]
   > Si vous choisissez des tailles plus importantes pour la machine virtuelle de hello, des frais supplémentaires peuvent s’appliquer. Pour plus d’informations, consultez [Tarification des machines virtuelles](https://azure.microsoft.com/pricing/details/virtual-machines/) .
   > 
   > 
6. Les machines virtuelles créées dans Visual Studio nécessitent un service cloud. Sur hello **paramètres du Service Cloud** page, sélectionnez un service cloud pour la machine virtuelle de hello ou cliquez sur **< nouveau... >** dans la liste déroulante de hello si vous n’avez pas encore un cloud service ou souhaitez toouse une nouvelle une. Un compte de stockage est également requis, par conséquent, choisissez un compte de stockage (ou créer un nouveau compte de stockage) Bonjour **compte de stockage** zone de liste déroulante. Consultez [Introduction tooMicrosoft Azure Storage](../articles/storage/common/storage-introduction.md) pour plus d’informations.
7. Si vous voulez toospecify un réseau virtuel (qui est facultatif), sélectionnez-le dans les zones de liste déroulante réseau virtuel et sous-réseau des hello.
   
    Les ordinateurs virtuels qui sont membres d’un ensemble de disponibilité sont déployées toodifferent domaines d’erreur. Pour plus d’informations, consultez [Azure Virtual Network](https://azure.microsoft.com/services/virtual-network/) .
8. Si vous souhaitez que votre ensemble de disponibilité des machines virtuelles toobelong tooan (également facultatif), sélectionnez hello **spécifier un ensemble de disponibilité** case à cocher, puis choisissez un groupe à haute disponibilité dans la zone de liste déroulante hello. Lorsque vous avez terminé, choisissez hello **suivant** bouton.
   
    Ajout de votre tooan d’ordinateur virtuel à haute disponibilité permet à votre application rester disponibles lors de problèmes réseau, de défaillance matérielle du disque local et de tout temps d’arrêt planifié. Vous devez toouse hello [portail de gestion Azure](http://go.microsoft.com/fwlink/?LinkID=253103) toocreate des réseaux virtuels, des sous-réseaux et disponibilité définit. Consultez [gérer hello disponibilité des Machines virtuelles](https://azure.microsoft.com/documentation/articles/manage-availability-virtual-machines/) pour plus d’informations.
9. Sur hello **points de terminaison** , spécifiez les points de terminaison publics hello que vous souhaitez toousers disponibles de votre machine virtuelle. Par exemple, vous pouvez choisir tooenable HTTP (Port 80) en outre toohello Bureau à distance et PowerShell points de terminaison qui sont activées par défaut. tooadd un point de terminaison, sélectionnez-en un dans hello **nom de Port** zone de liste de liste déroulante et choisissez hello **ajouter** bouton. tooremove un point de terminaison, choisissez hello rouge **X** nom toohello suivant dans la liste de points de terminaison hello.
   
    ![page points de terminaison de Hello dans l’Assistant de machines virtuelles hello.](./media/virtual-machines-common-classic-create-manage-visual-studio/IC718351.png)
   
    les points de terminaison Hello disponibles dépendent du service de cloud computing hello que vous avez sélectionné pour votre machine virtuelle. Pour plus d’informations, consultez [Points de terminaison de service Azure](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/) .
   
   > [!NOTE]
   > L’activation des points de terminaison publics rend les services sur votre toohello disponible de machine virtuelle internet. Être tooinstall sûr et configurer correctement les services et les points de terminaison hello sur votre machine virtuelle, tel comme les listes de contrôle d’accès (ACL) pour les points de terminaison hello. Consultez [comment tooSet des points de terminaison tooa Machine virtuelle](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/) pour plus d’informations.
   > 
   > 
10. Une fois que vous avez terminé de configurer les paramètres de machine virtuelle hello, choisissez hello **créer** bouton toocreate hello virtual machine.
    
     Comme Azure crée un ordinateur virtuel de hello, hello **journal des activités Azure** affiche hello la progression de l’opération de création d’ordinateur virtuel hello.
    
     ![Journal des activités de la machine virtuelle – En cours](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744138.png)
    
     informations de machine virtuelle uniquement tooview, choisissez hello **virtuels** onglet Bonjour **journal des activités Azure**.
    
     ![Journal des activités de la machine virtuelle – Terminé](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744139.png)
    
     Si l’opération de hello est correctement exécutée, hello machine virtuelle apparaît sous hello **virtuels** nœud dans l’Explorateur de serveurs. Vous pouvez vous y connecter en cliquant sur hello **se connecter à l’aide du Bureau à distance** contextuel.
    
     ![Machine virtuelle affichée dans l’Explorateur de serveurs](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744140.png)

## <a name="manage-your-virtual-machines"></a>Gérer vos machines virtuelles
Sur la page de configuration de machine virtuelle hello, en outre tooshutting vers le bas, la connexion, l’actualisation et ajouter des points de contrôle toohello sélectionné la machine virtuelle, vous pouvez également afficher ou modifier les paramètres pour la machine virtuelle de hello. Vous pouvez :

* Modifier la taille de machine virtuelle hello.
* Toouse avec l’ordinateur virtuel de hello à haute disponibilité de hello SELECT.
* ajouter, supprimer et modifier les paramètres des points de terminaison publics ;
* ajouter, supprimer et configurer les extensions des machines virtuelles ;
* Afficher des informations sur les disques hello associé avec l’ordinateur virtuel de hello.

### <a name="view-or-change-virtual-machine-settings"></a>Afficher ou modifier les paramètres des machines virtuelles
1. Dans l’Explorateur de serveurs, choisissez votre machine virtuelle dans hello **des Machines virtuelles Azure** nœud.
2. Dans le menu contextuel de hello, choisissez **configurer** page de configuration de machine virtuelle tooview hello.
   
    ![page de configuration de machine virtuelle Azure Hello](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744141.png)
3. Afficher les informations de machine virtuelle hello ou la modifier.

### <a name="save-or-restore-hello-status-of-your-virtual-machine"></a>Enregistrer ou restaurer l’état hello de votre machine virtuelle
Quand vous configurez votre machine virtuelle et installez des logiciels sur ce dernier, il est un tooregularly conseillé enregistrer votre progression en créant des points de contrôle de machine virtuelle. Un point de contrôle est un instantané ou une image, de l’état actuel de hello de votre machine virtuelle. Si une erreur survient avec l’ordinateur virtuel de hello, ou que vous souhaitez tooreconfigure hello virtual machine, vous pouvez gagner du temps en la restaurant état de point de contrôle précédent tooa plutôt que de recommencer à partir de zéro.

### <a name="toocreate-a-virtual-machine-checkpoint"></a>toocreate un point de contrôle de machine virtuelle
1. Dans l’Explorateur de serveurs, choisissez votre machine virtuelle dans hello **des Machines virtuelles Azure** nœud.
2. Dans le menu contextuel de hello, choisissez **configurer** page de configuration de machine virtuelle tooview hello.
3. Dans la page de configuration hello, choisissez hello **capturer l’Image** bouton.
   
    ![Bouton Capturer de la page de configuration Azure](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744142.png)
   
    Hello **capturer une Machine virtuelle** boîte de dialogue s’affiche.
   
    ![Boîte de dialogue Capturer la machine virtuelle](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744143.png)
4. Fournissez une étiquette et une description pour l’image. Une étiquette et une description par défaut sont fournies, mais vous pouvez les remplacer par les vôtres si vous le voulez.
5. Si vous avez déjà exécuté Sysprep sur cet ordinateur virtuel, sélectionnez hello **j’ai exécuté Sysprep sur l’ordinateur virtuel de hello** boîte.
   
    Sysprep est un outil qui, entre autres choses, supprime les données propres au système de version de l’ordinateur virtuel de hello de Windows, et le modèle d’autres peuvent utiliser. Consultez [comment tooCapture un tooUse de Machine virtuelle Windows en tant que modèle](https://azure.microsoft.com/documentation/articles/virtual-machines-capture-image-windows-server/) pour plus d’informations. Sauvegardez hello machine virtuelle avant d’exécuter Sysprep.
6. Une fois que vous avez terminé de configurer les paramètres de capture hello, choisissez hello **Capture** point de contrôle de bouton toocreate hello.
   
    Comme Azure crée un point de contrôle hello, hello **journal des activités Azure** affiche hello la progression de l’opération de hello.
   
    ![Capture d’un point de contrôle de machine virtuelle](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744144.png)
   
    Lors de l’opération de point de contrôle hello est terminée, vous le verrez Bonjour **journal des activités Azure**.
   
    ![Création de point de contrôle terminée](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744145.png)

## <a name="toomanage-virtual-machine-checkpoints"></a>points de contrôle de machine virtuelle toomanage
### <a name="toorestore-a-virtual-machine-tooa-previously-saved-state"></a>l’état précédemment enregistré toorestore un tooa de machine virtuelle
* Suivez les étapes de hello décrites dans [pas à pas : effectuer Cloud restaure des Machines virtuelles Microsoft Azure à l’aide de PowerShell - partie 2](http://blogs.technet.com/b/keithmayer/archive/2014/02/04/step-by-step-perform-cloud-restores-of-windows-azure-virtual-machines-using-powershell-part-2.aspx).

### <a name="toodelete-a-checkpoint"></a>toodelete un point de contrôle
1. Accédez toohello [portail de gestion Azure](http://go.microsoft.com/fwlink/?LinkID=253103).
2. Dans la page de configuration de machine virtuelle hello, choisissez hello **Images** onglet en hello haut hello.
3. Choisissez le point de contrôle hello vous souhaitez toodelete, puis choisissez hello **supprimer** bouton bas hello de page de hello.

## <a name="shut-down-your-virtual-machine"></a>Arrêter une machine virtuelle
1. Dans l’Explorateur de serveurs, choisissez hello machine virtuelle tooshut vers le bas dans hello **des Machines virtuelles Azure** nœud.
2. Dans le menu contextuel de hello, choisissez hello **arrêt** de commande, ou choisissez **configurer** tooview hello page de configuration d’ordinateur virtuel, puis choisissez hello **arrêt**bouton.

## <a name="next-steps"></a>Étapes suivantes
toolearn savoir plus sur la création d’ordinateurs virtuels, consultez [créer une Machine virtuelle exécutant Linux](../articles/virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) et [créer une machine virtuelle exécutant Windows dans le portail Azure en version préliminaire de hello](../articles/virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

