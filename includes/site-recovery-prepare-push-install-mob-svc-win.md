### <a name="prepare-for-a-push-installation-on-a-windows-computer"></a>Préparer une installation push sur un ordinateur Windows

1. Assurez-vous qu’il existe une connectivité réseau entre l’ordinateur Windows hello et serveur de processus hello.
2. Créer un compte de qu'ordinateur de hello tooaccess permet de ce serveur de processus hello. compte de Hello doit disposer des droits d’administrateur (local ou domaine). (Utilisez ce compte uniquement pour l’installation push de hello et des mises à jour de l’agent).

   > [!NOTE]
   > Si vous n’utilisez pas un compte de domaine, désactivez le contrôle d’accès utilisateur à distance sur l’ordinateur local de hello. toodisable contrôle des accès utilisateur à distance, sous la clé de Registre HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System hello, ajoutez un nouveau DWORD : **LocalAccountTokenFilterPolicy**. La valeur hello trop**1**. toodo à une commande invite de, exécutez hello de commande suivante :  
   `REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1`
   >
   >
2. Dans le pare-feu Windows sur l’ordinateur de hello souhaité tooprotect, sélectionnez **autoriser une application ou une fonctionnalité via le pare-feu**. Activez **Partage de fichiers et d’imprimantes** et **Windows Management Instrumentation (WMI)**. Pour les ordinateurs qui appartiennent tooa domaine, vous pouvez configurer les paramètres du pare-feu hello à l’aide d’un objet de stratégie de groupe (GPO).

   ![Paramètres du pare-feu](./media/site-recovery-prepare-push-install-mob-svc-win/mobility1.png)

3. Ajoutez le compte hello que vous avez créé dans CSPSConfigtool.
    1.  Connectez-vous sur le serveur de configuration tooyour.
    2.  Ouvrez le fichier **cspsconfigtool.exe**. (Il est disponible comme un raccourci sur le bureau de hello et dans le dossier de %ProgramData%\home\svsystems\bin hello).
    3.  Sur hello **gérer les comptes** onglet, sélectionnez **ajouter un compte**.
    4.  Ajoutez le compte hello que vous avez créé.
    5.  Entrez les informations d’identification de l’hello que vous utilisez lorsque vous activez la réplication pour un ordinateur.
