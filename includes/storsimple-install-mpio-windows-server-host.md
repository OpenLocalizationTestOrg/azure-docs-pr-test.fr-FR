#### <a name="tooinstall-mpio-on-hello-host"></a>tooinstall MPIO sur l’ordinateur hôte de hello
1. Ouvrez le Gestionnaire de serveur sur votre hôte Windows Server. Par défaut, le Gestionnaire de serveur démarre lorsqu’un membre du groupe des administrateurs de hello ouvre une session sur l’ordinateur tooa qui exécute Windows Server 2012 R2 ou Windows Server 2012. Si hello Gestionnaire de serveur n’est pas déjà ouvert, cliquez sur **Démarrer > Gestionnaire de serveur**.
   
    ![Gestionnaire de serveur](./media/storsimple-install-mpio-windows-server/IC740997.png)
2. Cliquez sur **Gestionnaire de serveur > Tableau de bord > Ajouter des rôles et fonctionnalités**. Cela démarre hello **Ajout de rôles et fonctionnalités** Assistant.
   
    ![Assistant Ajouter des rôles et fonctionnalités 1](./media/storsimple-install-mpio-windows-server/IC740998.png)
3. Bonjour **Ajout de rôles et fonctionnalités** Assistant, hello suivant :
   
   * Sur hello **avant de commencer** , cliquez sur **suivant**.
   * Sur hello **sélectionner le type d’installation** page, acceptez le paramètre par défaut hello **en fonction du rôle ou une fonctionnalité** installation. Cliquez sur **Suivant**.
     
       ![Assistant Ajouter des rôles et fonctionnalités 2](./media/storsimple-install-mpio-windows-server/IC740999.png)
   * Sur hello **serveur de destination sélectionnez** choisissez **sélectionner un serveur de pool de serveurs hello**. Votre serveur hôte doit être détecté automatiquement. Cliquez sur **Suivant**.
   * Sur hello **sélectionner des rôles de serveur** , cliquez sur **suivant**.
   * Sur hello **sélectionner des fonctionnalités** , sélectionnez **MPIO**, puis cliquez sur **suivant**.
     
       ![Assistant Ajouter des rôles et fonctionnalités 5](./media/storsimple-install-mpio-windows-server/IC741000.png)
   * Sur hello **confirmer les sélections d’installation** page, confirmer la sélection de hello, puis sélectionnez **redémarrez le serveur de destination hello automatiquement si nécessaire**, comme illustré ci-dessous. Cliquez sur **Installer**.
     
       ![Assistant Ajouter des rôles et fonctionnalités 8](./media/storsimple-install-mpio-windows-server/IC741001.png)
   * Vous serez notifiées hello l’installation est terminée. Cliquez sur **fermer** Assistant de hello tooclose.
     
       ![Assistant Ajouter des rôles et fonctionnalités 9](./media/storsimple-install-mpio-windows-server/IC741002.png)

