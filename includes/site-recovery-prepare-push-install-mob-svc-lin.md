### <a name="prepare-for-a-push-installation-on-a-linux-server"></a>Préparer une installation push sur un serveur Linux

1. Assurez-vous qu’il existe une connectivité réseau entre l’ordinateur Linux hello et serveur de processus hello.
2. Créer un compte de qu'ordinateur de hello tooaccess permet de ce serveur de processus hello. Hello compte doit être un **racine** utilisateur sur le serveur de Linux hello source. (Utilisez ce compte uniquement pour l’installation push de hello et des mises à jour.)
3. Vérifiez le fichier/etc/hosts hello sur la source de hello Linux server possède des entrées qui mappent des adresses de tooIP hello nom d’hôte local associés à toutes les cartes réseau.
4. Installer des packages d’openssh et openssl openssh-serveur plus récente de hello sur ordinateur hello que vous souhaitez tooreplicate.
5. Vérifiez que le protocole Secure Shell (SSH) est activé et s’exécute sur le port 22.
6. Activer l’authentification sous-système et le mot de passe SFTP dans le fichier de sshd_config hello :
  1.  Connectez-vous en tant qu’utilisateur **racine**.
  2.  Dans hello fichier/etc/ssh/fichier sshd_config, rechercher la ligne hello qui commence par **PasswordAuthentication**.
  3.  Supprimez les commentaires de la ligne de hello et également de modifier la valeur de hello**Oui**.
  4.  Ligne hello rechercher qui commence par **sous-système** et supprimez les commentaires de la ligne de hello.

     ![Linux](./media/site-recovery-prepare-push-install-mob-svc-lin/mobility2.png)
  5. Redémarrez hello **sshd** service.

7. Ajoutez le compte hello que vous avez créé dans CSPSConfigtool.
    1.  Connectez-vous sur le serveur de configuration tooyour.
    2.  Ouvrez le fichier **cspsconfigtool.exe**. (Il est disponible comme un raccourci sur le bureau de hello et dans le dossier de %ProgramData%\home\svsystems\bin hello).
    3.  Sur hello **gérer les comptes** , cliquez sur **ajouter un compte**.
    4.  Ajoutez le compte hello que vous avez créé. 
    5.  Entrez les informations d’identification de l’hello que vous utilisez lorsque vous activez la réplication pour un ordinateur.
