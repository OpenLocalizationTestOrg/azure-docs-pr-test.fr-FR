### <a name="determine-hello-dns-name-of-hello-virtual-machine"></a>Déterminer le nom DNS de hello de machine virtuelle de hello
tooconnect toohello du moteur de base de données SQL Server à partir d’un autre ordinateur, vous devez connaître hello système DNS (Domain Name) nom de l’ordinateur virtuel de hello. (Il s’agit d’ordinateur virtuel des hello tooidentify utilise hello nom hello internet. Vous pouvez utiliser des adresses IP de hello, mais l’adresse hello peut-être changer lorsque Azure déplace des ressources pour la redondance ou la maintenance. nom DNS de Hello sera stable, car elle peut être redirigé la nouvelle adresse IP de tooa.)  

1. Bonjour portail Azure (ou à partir de l’étape précédente de hello), sélectionnez **machines virtuelles (classiques)**.
2. Sélectionnez votre machine virtuelle SQL.
3. Sur hello **virtuels** panneau, hello de copie **nom DNS** pour la machine virtuelle de hello.
   
    ![Nom DNS](./media/virtual-machines-sql-server-connection-steps/sql-vm-dns-name.png)

### <a name="connect-toohello-database-engine-from-another-computer"></a>Se connecter toohello du moteur de base de données à partir d’un autre ordinateur
1. Sur un ordinateur connecté toohello internet, ouvrez SQL Server Management Studio.
2. Bonjour **connecter tooServer** ou **connecter tooDatabase moteur** la boîte de dialogue hello **nom du serveur** , entrez le nom DNS de hello de machine virtuelle de hello (déterminée Bonjour la tâche précédente) et un numéro de port de point de terminaison public au format hello de *NomDNS, numéro_port* comme **mysqlvm.cloudapp.net,57500**.
   
    ![Connexion en utilisant SSMS](./media/virtual-machines-sql-server-connection-steps/33Connect-SSMS.png)
   
    Si vous avez oublié le numéro de port du point de terminaison public hello que vous avez créé précédemment, vous pouvez le trouver dans hello **points de terminaison** zone Hello **machine virtuelle** panneau.
   
    ![Port public](./media/virtual-machines-sql-server-connection-steps/sql-vm-port-number.png)
3. Bonjour **authentification** boîte, sélectionnez **l’authentification SQL Server**.
4. Bonjour **connexion** zone, entrez un nom hello d’une connexion que vous avez créé dans une tâche précédente.
5. Bonjour **mot de passe** boîte, un mot de passe hello type de connexion hello que vous créez dans une tâche précédente.
6. Cliquez sur **Connecter**.

