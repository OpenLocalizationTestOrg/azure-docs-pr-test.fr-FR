

Quand vous créez un projet d’application web pour Azure, vous pouvez approvisionner une machine virtuelle dans Azure. Vous pouvez ensuite configurer des hello virtual machine avec des logiciels supplémentaires, ou utiliser d’ordinateur virtuel de hello pour à des fins de diagnostic ou de débogage.

toocreate une machine virtuelle lorsque vous créez une application web, procédez comme suit :

1. Dans Visual Studio, cliquez sur **fichier** > **nouveau** > **projet** > **Web**, puis choisissez **Application Web ASP.NET** (sous hello **Visual C#** ou **Visual Basic** nœuds).
2. Bonjour **nouveau projet ASP.NET** boîte de dialogue, de type hello select de l’application web que vous souhaitez et Bonjour Azure section de la boîte de dialogue hello (dans le coin inférieur droit de hello), assurez-vous que hello **hôte hello cloud**case à cocher est activée (cette case à cocher **créer des ressources distantes** dans certaines installations).
   
    ![][0]
3. Pour cet exemple, dans la liste déroulante de hello sous Microsoft Azure, choisissez **l’ordinateur virtuel (v1)**, puis cliquez sur hello **OK** bouton.
4. Connectez-vous tooAzure si vous êtes invité. Hello **créer un ordinateur virtuel** boîte de dialogue s’affiche.
   
    ![][2]
5. Bonjour **nom DNS** , entrez un nom pour la machine virtuelle de hello. nom DNS de Hello doit être unique dans Azure. Si le nom hello que vous avez entré n’est pas disponible, un point d’exclamation rouge s’affiche.
6. Bonjour **Image** , choisissez hello image de machine virtuelle de hello toobase sur. Vous pouvez choisir une des images de machine virtuelle Azure standard hello ou votre image que vous avez téléchargé tooAzure.
7. Laissez hello **activer IIS et Web Deploy** case à cocher, sauf si vous prévoyez tooinstall un serveur web différent. Vous ne serez pas en mesure de toopublish à partir de Visual Studio si vous désactivez Web Deploy. Vous pouvez ajouter IIS et Web Deploy tooany d’images de Windows Server hello empaqueté, y compris vos images personnalisées.
8. Bonjour **taille** , choisissez la taille de hello de machine virtuelle de hello.
9. Spécifiez hello signe-informations d’identification pour cet ordinateur virtuel. Notez les, car vous en aurez besoin tooaccess hello ordinateur via Bureau à distance.
10. Bonjour **emplacement** , sélectionnez l’ordinateur virtuel de hello région toohost hello.
11. Cliquez sur hello **OK** toostart bouton Création d’ordinateur virtuel de hello. Vous pouvez suivre la progression hello d’opération hello Bonjour **sortie** fenêtre.
    
    ![][3]
12. Lors de la configuration de machine virtuelle de hello, scripts publiés sont créés dans un **PublishScripts** nœud dans votre solution. Hello publié script s’exécute et configure un ordinateur virtuel dans Azure. Hello **sortie** fenêtre affiche l’état de hello. script de Hello exécute hello suivant tooset actions hello virtual machine :
    
    * Crée la machine virtuelle de hello s’il n’existe pas.
    * Crée un compte de stockage avec un nom qui commence par `devtest`, mais uniquement si il n’est pas déjà un compte de stockage de ce type dans la région spécifiée du hello.
    * Crée un service cloud en tant que conteneur pour la machine virtuelle de hello et crée un rôle web pour l’application web de hello.
    * Configure Web Deploy sur l’ordinateur virtuel de hello.
    * Configure IIS et ASP.NET sur l’ordinateur virtuel de hello.
    
    ![][4]
13. (Facultatif) Vous pouvez vous connecter toohello machine virtuelle. Dans **l’Explorateur de serveurs**, développez hello **virtuels** nœud, choisissez le nœud hello pour la machine virtuelle de hello vous avez créé et dans le menu contextuel, choisissez **connexion Bureau à distance**. Vous pouvez également, dans **Cloud Explorer** vous pouvez choisir **ouvrir dans le portail** hello du menu contextuel et connecter la machine virtuelle de toohello il.
    
    ![][5]

## <a name="next-steps"></a>Étapes suivantes
Si vous souhaitez toocustomize hello publiées scripts que vous avez créé, lire des informations plus détaillées à [environnements de Test et à l’aide de Scripts Windows PowerShell tooPublish tooDev](http://msdn.microsoft.com/library/dn642480.aspx).

[0]: ./media/virtual-machines-common-classic-web-app-visual-studio/CreateVM_NewProject.PNG
[1]: ./media/dotnet-visual-studio-create-virtual-machine/CreateVM_SignIn.PNG
[2]: ./media/virtual-machines-common-classic-web-app-visual-studio/CreateVM_CreateVM.PNG
[3]: ./media/virtual-machines-common-classic-web-app-visual-studio/CreateVM_Provisioning.png
[4]: ./media/virtual-machines-common-classic-web-app-visual-studio/CreateVM_SolutionExplorer.png
[5]: ./media/virtual-machines-common-classic-web-app-visual-studio/VS_Create_VM_Connect.png
