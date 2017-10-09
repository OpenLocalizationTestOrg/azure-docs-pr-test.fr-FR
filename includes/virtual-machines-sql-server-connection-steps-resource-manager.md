### <a name="configure-a-dns-label-for-hello-public-ip-address"></a>Configurer un nom DNS pour l’adresse IP publique de hello

tooconnect toohello du moteur de base de données SQL Server à partir de hello Internet, créez un nom DNS pour votre adresse IP publique. Vous pouvez vous connecter à l’adresse IP, mais hello nom DNS crée un enregistrement A qui est plus facile tooidentify et des résumés hello sous-jacent adresse IP publique.

> [!NOTE]
> Étiquettes de DNS ne sont pas requises si plan tooonly connecter toohello SQL Server de l’instance dans hello même réseau virtuel ou que localement.

toocreate un nom DNS, sélectionnez d’abord **virtuels** dans le portail de hello. Sélectionnez votre toobring de machine virtuelle SQL Server ses propriétés.

1. Dans la vue d’ensemble de la machine virtuelle hello, sélectionnez votre **adresse IP publique**.

    ![adresse IP publique](./media/virtual-machines-sql-server-connection-steps/rm-public-ip-address.png)

1. Dans Propriétés hello pour votre adresse IP publique, développez **Configuration**.

1. Entrez un nom DNS. Ce nom est un enregistrement A qui peut être utilisé tooconnect tooyour machine virtuelle SQL Server par un nom à la place de l’adresse IP directement.

1. Cliquez sur hello **enregistrer** bouton.

    ![nom dns](./media/virtual-machines-sql-server-connection-steps/rm-dns-label.png)

### <a name="connect-toohello-database-engine-from-another-computer"></a>Se connecter toohello du moteur de base de données à partir d’un autre ordinateur

1. Sur un ordinateur connecté toohello internet, ouvrez SQL Server Management Studio (SSMS). Si vous n’avez pas SQL Server Management Studio, vous pouvez le télécharger [ici](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

1. Bonjour **connecter tooServer** ou **connecter tooDatabase moteur** boîte de dialogue, modifier hello **nom du serveur** valeur. Entrez l’adresse IP de hello ou un nom DNS complet de l’ordinateur virtuel de hello (déterminée dans la tâche précédente hello). Vous pouvez également ajouter une virgule et indiquer le port TCP du serveur SQL. Par exemple, `mysqlvmlabel.eastus.cloudapp.azure.com,1433`.

1. Bonjour **authentification** boîte, sélectionnez **l’authentification SQL Server**.

1. Bonjour **connexion** zone, entrez un nom hello d’une connexion SQL valide.

1. Bonjour **mot de passe** boîte, un mot de passe hello type de connexion de hello.

1. Cliquez sur **Connecter**.

    ![connecter ssms](./media/virtual-machines-sql-server-connection-steps/rm-ssms-connect.png)