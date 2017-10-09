
1. Bonjour **connexions hybrides** panneau, cliquez sur la connexion hybride hello vous venez de créer, puis cliquez sur **écouteur le programme d’installation**.
   
    ![Click Listener Setup](./media/app-service-hybrid-connections-manager-install/D04ClickListenerSetup.png)
2. Hello **propriétés de connexion hybride** panneau s’ouvre. Sous **Gestionnaire de connexions hybrides local**, choisissez **télécharger et configurer manuellement**enregistrer hello téléchargé HybridConnectionManager.msi package et copiez la chaîne de connexion de passerelle hello.
   
    ![Cliquez ici tooinstall](./media/app-service-hybrid-connections-manager-install/D05ClickToInstallHCM.png)
3. À partir d’une invite de commandes administrateur, tapez Bonjour suivant le programme d’installation de commande toostart hello :
   
        start HybridConnectionManager.msi
4. Après avoir hello s’exécute le programme d’installation, cliquez sur **pas maintenant**, puis recherchez le dossier de %ProgramFiles%\Microsoft\HybridConnectionManager toohello, exécutez HCMConfigWizard.exe et cliquez sur **Oui** Bonjour **utilisateur Contrôle de compte** boîte de dialogue.
5. Collez la chaîne de connexion hybride hello que vous avez copiés précédemment et cliquez sur **OK**. 
   
    ![Installation](./media/app-service-hybrid-connections-manager-install/D08aHCMInstallManual.png)
6. Fin de l’installation de hello, cliquez sur **fermer**.
   
    ![Click Close](./media/app-service-hybrid-connections-manager-install/D09HCMInstallComplete.png)
   
    Sur hello **connexions hybrides** panneau, hello **état** colonne affiche à présent **connecté**. 
   
    ![Connected Status](./media/app-service-hybrid-connections-manager-install/D10HCStatusConnected.png)

