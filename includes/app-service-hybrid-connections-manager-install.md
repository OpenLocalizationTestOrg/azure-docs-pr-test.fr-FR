
1. <span data-ttu-id="c6d69-101">Bonjour **connexions hybrides** panneau, cliquez sur la connexion hybride hello vous venez de créer, puis cliquez sur **écouteur le programme d’installation**.</span><span class="sxs-lookup"><span data-stu-id="c6d69-101">In hello **Hybrid connections** blade, click hello hybrid connection you just created, then click **Listener Setup**.</span></span>
   
    ![Click Listener Setup](./media/app-service-hybrid-connections-manager-install/D04ClickListenerSetup.png)
2. <span data-ttu-id="c6d69-103">Hello **propriétés de connexion hybride** panneau s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="c6d69-103">hello **Hybrid connection properties** blade opens.</span></span> <span data-ttu-id="c6d69-104">Sous **Gestionnaire de connexions hybrides local**, choisissez **télécharger et configurer manuellement**enregistrer hello téléchargé HybridConnectionManager.msi package et copiez la chaîne de connexion de passerelle hello.</span><span class="sxs-lookup"><span data-stu-id="c6d69-104">Under **On-premises Hybrid Connection Manager**, choose **download and configure manually**, save hello downloaded HybridConnectionManager.msi package, and copy hello gateway connection string.</span></span>
   
    ![Cliquez ici tooinstall](./media/app-service-hybrid-connections-manager-install/D05ClickToInstallHCM.png)
3. <span data-ttu-id="c6d69-106">À partir d’une invite de commandes administrateur, tapez Bonjour suivant le programme d’installation de commande toostart hello :</span><span class="sxs-lookup"><span data-stu-id="c6d69-106">From an administrator command prompt, type hello following command toostart hello installer:</span></span>
   
        start HybridConnectionManager.msi
4. <span data-ttu-id="c6d69-107">Après avoir hello s’exécute le programme d’installation, cliquez sur **pas maintenant**, puis recherchez le dossier de %ProgramFiles%\Microsoft\HybridConnectionManager toohello, exécutez HCMConfigWizard.exe et cliquez sur **Oui** Bonjour **utilisateur Contrôle de compte** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="c6d69-107">After hello installer runs, click **Not now**, then browse toohello %ProgramFiles%\Microsoft\HybridConnectionManager folder, run HCMConfigWizard.exe and click **Yes** in hello **User Account Control** dialog.</span></span>
5. <span data-ttu-id="c6d69-108">Collez la chaîne de connexion hybride hello que vous avez copiés précédemment et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="c6d69-108">Paste hello hybrid connection string that you copied earlier and click **OK**.</span></span> 
   
    ![Installation](./media/app-service-hybrid-connections-manager-install/D08aHCMInstallManual.png)
6. <span data-ttu-id="c6d69-110">Fin de l’installation de hello, cliquez sur **fermer**.</span><span class="sxs-lookup"><span data-stu-id="c6d69-110">When hello install completes, click **Close**.</span></span>
   
    ![Click Close](./media/app-service-hybrid-connections-manager-install/D09HCMInstallComplete.png)
   
    <span data-ttu-id="c6d69-112">Sur hello **connexions hybrides** panneau, hello **état** colonne affiche à présent **connecté**.</span><span class="sxs-lookup"><span data-stu-id="c6d69-112">On hello **Hybrid connections** blade, hello **Status** column now shows **Connected**.</span></span> 
   
    ![Connected Status](./media/app-service-hybrid-connections-manager-install/D10HCStatusConnected.png)

