
1. <span data-ttu-id="3300d-101">Dans le panneau **Connexions hybrides**, cliquez sur la connexion hybride que vous avez créée, puis sur **Configuration de l’écouteur**.</span><span class="sxs-lookup"><span data-stu-id="3300d-101">In the **Hybrid connections** blade, click the hybrid connection you just created, then click **Listener Setup**.</span></span>
   
    ![Click Listener Setup](./media/app-service-hybrid-connections-manager-install/D04ClickListenerSetup.png)
2. <span data-ttu-id="3300d-103">Le volet **Propriétés de la connexion hybride** s'ouvre.</span><span class="sxs-lookup"><span data-stu-id="3300d-103">The **Hybrid connection properties** blade opens.</span></span> <span data-ttu-id="3300d-104">Sous **Gestionnaire de connexions hybrides locales**, choisissez **télécharger et configurer manuellement**, enregistrez le package HybridConnectionManager.msi téléchargé, puis copiez la chaîne de connexion de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="3300d-104">Under **On-premises Hybrid Connection Manager**, choose **download and configure manually**, save the downloaded HybridConnectionManager.msi package, and copy the gateway connection string.</span></span>
   
    ![Cliquez ici pour l'installer](./media/app-service-hybrid-connections-manager-install/D05ClickToInstallHCM.png)
3. <span data-ttu-id="3300d-106">À partir d'une invite de commandes administrateur, tapez la commande suivante pour démarrer le programme d'installation :</span><span class="sxs-lookup"><span data-stu-id="3300d-106">From an administrator command prompt, type the following command to start the installer:</span></span>
   
        start HybridConnectionManager.msi
4. <span data-ttu-id="3300d-107">Une fois le programme d’installation lancé, cliquez sur **Pas maintenant**, accédez au dossier %ProgramFiles%\Microsoft\HybridConnectionManager, exécutez HCMConfigWizard.exe, puis cliquez sur **Oui** dans la boîte de dialogue **Contrôle de compte d’utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="3300d-107">After the installer runs, click **Not now**, then browse to the %ProgramFiles%\Microsoft\HybridConnectionManager folder, run HCMConfigWizard.exe and click **Yes** in the **User Account Control** dialog.</span></span>
5. <span data-ttu-id="3300d-108">Collez la chaîne de connexion hybride copiée précédemment, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="3300d-108">Paste the hybrid connection string that you copied earlier and click **OK**.</span></span> 
   
    ![Installation](./media/app-service-hybrid-connections-manager-install/D08aHCMInstallManual.png)
6. <span data-ttu-id="3300d-110">Une fois l'installation terminée, cliquez sur **Fermer**.</span><span class="sxs-lookup"><span data-stu-id="3300d-110">When the install completes, click **Close**.</span></span>
   
    ![Click Close](./media/app-service-hybrid-connections-manager-install/D09HCMInstallComplete.png)
   
    <span data-ttu-id="3300d-112">Dans le panneau **Connexions hybrides**, la colonne **Statut** indique à présent **Connecté**.</span><span class="sxs-lookup"><span data-stu-id="3300d-112">On the **Hybrid connections** blade, the **Status** column now shows **Connected**.</span></span> 
   
    ![Connected Status](./media/app-service-hybrid-connections-manager-install/D10HCStatusConnected.png)

