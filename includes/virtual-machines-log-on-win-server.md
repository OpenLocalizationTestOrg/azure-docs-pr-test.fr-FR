1. Un clic sur **Connecter** permet de créer et de télécharger un fichier de protocole Remote Desktop Protocol (fichier .rdp). Cliquez sur **ouvrir** toouse ce fichier.
2. Vous obtiendrez un avertissement qui .rdp hello est un serveur de publication inconnu. C’est normal. Dans la fenêtre du Bureau à distance hello, cliquez sur **Connect** toocontinue.
   
    ![Capture d’écran d’avertissement relatif à un éditeur inconnu.](./media/virtual-machines-log-on-win-server/rdp-warn.png)
3. Bonjour **sécurité Windows** fenêtre, informations d’identification de hello pour un compte sur l’ordinateur virtuel de hello puis tapez **OK**.
   
     **Compte local** -il s’agit généralement de nom d’utilisateur et mot de passe que vous avez spécifié lors de la création de machine virtuelle hello compte hello. Dans ce cas, domaine de hello est nom hello de machine virtuelle de hello et il est entré en tant que *vmname*&#92; *nom d’utilisateur*.  
   
    **Machine virtuelle d’un domaine** - si hello machine virtuelle appartient tooa domaine, entrez le nom d’utilisateur de hello au format de hello *domaine*&#92; *Nom d’utilisateur*. compte de Hello doit également tooeither soit hello administrateurs de groupe disposent des privilèges de l’accès à distance toohello machine virtuelle.
   
    **Contrôleur de domaine** - si hello machine virtuelle est un contrôleur de domaine, le nom d’utilisateur de type hello et le mot de passe d’un compte d’administrateur de domaine pour ce domaine.
4. Cliquez sur **Oui** tooverify hello l’identité de l’ordinateur virtuel de hello et terminer la session.
   
   ![Capture d’écran montrant un message à propos de vérification d’identité hello Hello machine virtuelle.](./media/virtual-machines-log-on-win-server/cert-warning.png)

