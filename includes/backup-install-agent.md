## <a name="download-install-and-register-hello-azure-backup-agent"></a>Télécharger, installer et inscrire l’agent de sauvegarde Azure hello
Après avoir créé le coffre de sauvegarde Azure hello, un agent doit être installé sur chacun de vos ordinateurs Windows (Windows Server, Windows client, serveur de System Center Data Protection Manager ou ordinateur du serveur de sauvegarde Azure) qui permet de sauvegarder des données et applications tooAzure.

1. Connectez-vous à toohello [portail de gestion](https://manage.windowsazure.com/)
2. Cliquez sur **Services de récupération**, puis sélectionnez le coffre de sauvegarde hello que vous souhaitez tooregister avec un serveur. page de démarrage rapide de Hello ce coffre de sauvegarde s’affiche.
   
    ![Démarrage rapide](./media/backup-install-agent/quickstart.png)
3. Sur la page de démarrage rapide de hello, cliquez sur hello **pour Windows Server ou System Center Data Protection Manager ou Windows client** sous **télécharger l’Agent**. Cliquez sur **enregistrer** toocopy il toohello les ordinateur local.
   
    ![Enregistrer l’agent](./media/backup-install-agent/agent.png)
4. Une fois que l’agent de hello est installé, double-cliquez sur MARSAgentInstaller.exe toolaunch hello l’installation de hello Azure Backup agent. Choisissez le dossier d’installation hello et le dossier de travail requis pour l’agent de hello. emplacement de cache de Hello spécifié doit disposer de l’espace libre qui est au moins 5 % des données de sauvegarde hello.
5. Si vous utilisez un toohello tooconnect du serveur proxy internet, Bonjour **configuration Proxy** écran, entrez les détails du serveur proxy hello. Si vous utilisez un proxy authentifié, entrez les détails de nom et mot de passe utilisateur hello dans cet écran.
6. agent de sauvegarde Azure Hello installe .NET Framework 4.5 et Windows PowerShell (si elle n’est disponible) installation de hello toocomplete.
7. Une fois que l’agent de hello est installé, cliquez sur hello **continuer tooRegistration** toocontinue bouton avec les flux de travail hello.
   
   ![S’inscrire](./media/backup-install-agent/register.png)
8. Dans l’écran informations d’identification de coffre hello, accédez à fichier tooand hello sélectionnez coffre informations d’identification qui a été téléchargée antérieurement.
   
    ![Informations d’identification du coffre](./media/backup-install-agent/vc.png)
   
    fichier d’informations d’identification de coffre Hello est valide uniquement pour 48 heures (après l’avoir téléchargée à partir du portail de hello). Si vous rencontrez une erreur dans cet écran (par exemple « coffre informations d’identification de fichier fourni a expiré »), connexion toohello portail Azure et informations d’identification de coffre de hello téléchargement de fichiers à nouveau.
   
    Vérifiez que ce fichier d’informations d’identification de coffre hello est disponible dans un emplacement qui est accessible par l’application d’installation de hello. Si vous rencontrez des erreurs connexes d’accès, informations d’identification du coffre copie hello tooa temporaire sur cet ordinateur et de recommencer l’opération de hello.
   
    Si vous rencontrez une erreur d’informations d’identification de coffre non valide (par exemple « non valide de coffre informations d’identification fournies ») soit hello fichier est endommagé ou ne pas avoir hello dernières informations d’identification associées service de récupération hello. Recommencez l’opération hello après avoir téléchargé un nouveau fichier d’informations d’identification de coffre à partir du portail de hello. Cette erreur se produit généralement si l’utilisateur de hello clique sur hello **informations d’identification du coffre de téléchargement** option Bonjour portail Azure, de suite. Dans ce cas, uniquement hello deuxième coffre informations d’identification du fichier est valide.
9. Bonjour **paramètre de chiffrement** écran, vous pouvez générer un mot de passe ou fournissez une phrase secrète (16 caractères au minimum). N’oubliez pas de mot de passe toosave hello dans un emplacement sécurisé.
   
    ![Chiffrement](./media/backup-install-agent/encryption.png)
   
   > [!WARNING]
   > Si hello le mot de passe est perdu ou oublié ; L’aide de Microsoft ne peut pas récupérer les données de sauvegarde hello. utilisateur final de Hello possède la phrase secrète de chiffrement hello et Microsoft n’a pas de visibilité hello de mot de passe utilisé par l’utilisateur final de hello. Enregistrez les fichiers hello dans un emplacement sécurisé comme requis pendant une opération de récupération.
   > 
   > 
10. Une fois que vous cliquez sur hello **Terminer** bouton, hello est inscrit correctement toohello coffre et que vous êtes maintenant prêt toostart sauvegarde tooMicrosoft Azure.
11. Lorsque vous utilisez Microsoft Azure Backup autonome vous pouvez modifier les paramètres de hello spécifiés au cours de flux de travail de l’inscription hello en cliquant sur hello **modifier les propriétés** option dans le composant logiciel enfichable de mmc de sauvegarde Azure hello dans.
    
    ![Modifier les propriétés](./media/backup-install-agent/change.png)
    
    Ou bien, lors de l’utilisation de Data Protection Manager, vous pouvez modifier les paramètres de hello spécifiées pendant le flux de travail de l’inscription hello en cliquant sur hello **configurer** option en sélectionnant **Online** sous hello **Gestion** onglet.
    
    ![Configurer la sauvegarde Azure](./media/backup-install-agent/configure.png)

