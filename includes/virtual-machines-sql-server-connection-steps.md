### <a name="open-tcp-ports-in-hello-windows-firewall-for-hello-default-instance-of-hello-database-engine"></a>Ouvrez les ports TCP dans le pare-feu Windows hello hello instance par défaut de hello du moteur de base de données
1. Se connecter toohello virtuels avec le Bureau à distance. Pour obtenir des instructions détaillées sur la connexion toohello machine virtuelle, consultez [ouvrir une VM SQL avec le Bureau à distance](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md#open-the-vm-with-remote-desktop).
2. Une fois connecté, à l’écran d’accueil hello, tapez **WF.msc**, puis appuyez sur ENTRÉE.
   
    ![Démarrer hello programme de pare-feu](./media/virtual-machines-sql-server-connection-steps/12Open-WF.png)
3. Bonjour **pare-feu Windows avec fonctions avancées de sécurité**, dans hello du volet gauche, cliquez sur **règles de trafic entrant**, puis cliquez sur **nouvelle règle** dans le volet d’actions hello.
   
    ![Nouvelle règle](./media/virtual-machines-sql-server-connection-steps/13New-FW-Rule.png)
4. Bonjour **Assistant Nouvelle règle de trafic entrant** boîte de dialogue **le Type de règle**, sélectionnez **Port**, puis cliquez sur **suivant**.
5. Bonjour **protocole et Ports** boîte de dialogue, par défaut hello **TCP**. Bonjour **ports locaux spécifiques** zone, puis hello de type numéro de port d’instance hello Hello du moteur de base de données (**1433** pour l’instance par défaut de hello ou de votre choix pour un port privé à l’étape de point de terminaison hello hello).
   
    ![Port TCP 1433](./media/virtual-machines-sql-server-connection-steps/14Port-1433.png)
6. Cliquez sur **Suivant**.
7. Bonjour **Action** boîte de dialogue, sélectionnez **autoriser la connexion hello**, puis cliquez sur **suivant**.
   
    **Note de sécurité :** sélection **autoriser la connexion de hello si elle est sécurisée** peut fournir une sécurité supplémentaire. Sélectionnez cette option si vous souhaitez que les options de sécurité supplémentaires tooconfigure dans votre environnement.
   
    ![Autoriser les connexions](./media/virtual-machines-sql-server-connection-steps/15Allow-Connection.png)
8. Bonjour **profil** boîte de dialogue, sélectionnez **Public**, **privé**, et **domaine**. Cliquez ensuite sur **Suivant**.
   
    **Note de sécurité :** sélection **Public** autorise l’accès via internet de hello. Lorsque cela est possible, sélectionnez un profil plus restrictif.
   
    ![Profil public](./media/virtual-machines-sql-server-connection-steps/16Public-Private-Domain-Profile.png)
9. Bonjour **nom** boîte de dialogue, tapez un nom et une description pour cette règle, puis cliquez sur **Terminer**.
   
    ![Nom de la règle](./media/virtual-machines-sql-server-connection-steps/17Rule-Name.png)

Le cas échéant, ouvrez des ports supplémentaires pour les autres composants. Pour plus d’informations, consultez [tooAllow de pare-feu Windows hello accès à SQL Server de configuration](http://msdn.microsoft.com/library/cc646023.aspx).

### <a name="configure-sql-server-toolisten-on-hello-tcp-protocol"></a>Configurer SQL Server toolisten sur hello protocole TCP

[!INCLUDE [Enable TCP](virtual-machines-sql-server-connection-tcp-protocol.md)]

### <a name="configure-sql-server-for-mixed-mode-authentication"></a>Configuration de SQL Server pour l'authentification en mode mixte
Hello du moteur de base de données SQL Server ne peut pas utiliser l’authentification Windows sans environnement de domaine. tooconnect toohello du moteur de base de données à partir d’un autre ordinateur, configurez SQL Server pour l’authentification en mode mixte. qui permet l'authentification SQL Server et l'authentification Windows

> [!NOTE]
> (il n’est pas nécessaire de configurer l’authentification en mode mixte si vous avez configuré un réseau virtuel Azure avec un environnement de domaine configuré).
> 
> 

1. Lors de la machine virtuelle toohello connecté, sur la page de démarrage hello, tapez **SQL Server Management Studio** et cliquez sur icône sélectionnée de hello.
   
    Hello la première fois que vous ouvrez Management Studio, il doit créer des environnement de Management Studio utilisateurs hello. Cette opération peut prendre du temps.
2. Management Studio présente hello **connecter tooServer** boîte de dialogue. Bonjour **nom du serveur** zone, entrez un nom hello de hello machine virtuelle tooconnect toohello du moteur de base de données avec l’Explorateur d’objets de hello (au lieu du nom d’ordinateur virtuel hello vous pouvez également utiliser **(local)** ou un période unique comme hello **nom du serveur**). Sélectionnez **l’authentification Windows**et laisser  ***your_VM_name*\your_local_administrator** Bonjour **nom d’utilisateur** boîte. Cliquez sur **Connecter**.
   
    ![Se connecter tooServer](./media/virtual-machines-sql-server-connection-steps/19Connect-to-Server.png)
3. Dans l’Explorateur d’objets SQL Server Management Studio, le bouton droit sur hello instance hello de SQL Server (nom de machine virtuelle hello), puis cliquez sur **propriétés**.
   
    ![Propriétés de serveur](./media/virtual-machines-sql-server-connection-steps/20Server-Properties.png)
4. Sur hello **sécurité** sous **l’authentification du serveur**, sélectionnez **mode d’authentification SQL Server et Windows**, puis cliquez sur **OK** .
   
    ![Sélectionner le mode d'authentification](./media/virtual-machines-sql-server-connection-steps/21Mixed-Mode.png)
5. Dans la boîte de dialogue hello SQL Server Management Studio, cliquez sur **OK** tooacknowledge hello exigence toorestart SQL Server.
6. Dans l’Explorateur d’objets, cliquez avec le bouton droit sur votre serveur, puis cliquez sur **Redémarrer**. (si SQL Server Agent est exécuté, il doit également être redémarré).
   
    ![Redémarrer](./media/virtual-machines-sql-server-connection-steps/22Restart2.png)
7. Dans la boîte de dialogue hello SQL Server Management Studio, cliquez sur **Oui** tooagree que vous souhaitez toorestart SQL Server.

### <a name="create-sql-server-authentication-logins"></a>Création de connexions d'authentification SQL Server
tooconnect toohello du moteur de base de données à partir d’un autre ordinateur, vous devez créer au moins une connexion d’authentification SQL Server.

1. Dans l’Explorateur d’objets SQL Server Management Studio, développez le dossier hello d’instance de serveur hello dans lequel vous souhaitez toocreate hello nouveau compte de connexion.
2. Avec le bouton hello **sécurité** dossier, pointez trop**nouveau**, puis sélectionnez **connexion...** .
   
    ![Nouvelle connexion](./media/virtual-machines-sql-server-connection-steps/23New-Login.png)
3. Bonjour **nouvelle connexion** la boîte de dialogue hello **général** , entrez le nom hello du nouvel utilisateur de hello Bonjour **nom de connexion** boîte.
4. Sélectionnez **Authentification SQL Server**.
5. Bonjour **mot de passe** , entrez un mot de passe pour le nouvel utilisateur de hello. Entrez de nouveau ce mot de passe dans hello **confirmer le mot de passe** boîte.
6. Sélectionnez les options de mise en œuvre de mot de passe hello requis (**appliquer la stratégie de mot de passe**, **appliquer l’expiration du mot de passe**, et **utilisateur doit changer de mot de passe à la prochaine connexion**). Si vous utilisez cette connexion pour vous-même, il est inutile toorequire modification d’un mot de passe à la prochaine connexion de hello.
7. À partir de hello **base de données par défaut** , sélectionnez une base de données par défaut pour la connexion de hello. **maître** est par défaut de hello pour cette option. Si vous n’avez pas encore créé une base de données utilisateur, laissez ce paramètre défini trop**master**.
   
    ![Propriétés de connexion](./media/virtual-machines-sql-server-connection-steps/24Test-Login.png)
8. Si c’est la première ouverture de session hello que vous créez, vous souhaiterez toodesignate cette connexion en tant qu’un administrateur SQL Server. Si tel est le cas, hello **rôles serveur** page, vérifiez **sysadmin**.
   
   > [!NOTE]
   > Les membres du rôle serveur fixe sysadmin de hello disposent du contrôle total hello du moteur de base de données. Vous devez limiter soigneusement l'appartenance à ce rôle.
   > 
   > 
   
   ![administrateur système](./media/virtual-machines-sql-server-connection-steps/25sysadmin.png)
9. Cliquez sur OK.

Pour plus d'informations sur les connexions SQL Server, consultez la page [Créer un compte de connexion](http://msdn.microsoft.com/library/aa337562.aspx).

