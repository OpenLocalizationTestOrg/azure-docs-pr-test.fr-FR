1. Lors de la machine virtuelle toohello connecté de bureau à distance, recherchez **Configuration Manager**:

    ![Ouvrir le gestionnaire de configuration SQL Server](./media/virtual-machines-sql-server-connection-tcp-protocol/sql-server-configuration-manager.png)

1. Dans le Gestionnaire de Configuration SQL Server, dans le volet de console hello, développez **Configuration du réseau SQL Server**.

1. Dans le volet de console hello, cliquez sur **protocoles pour MSSQLSERVER** (nom d’instance par défaut hello). Dans le volet d’informations hello, cliquez sur **TCP** et cliquez sur **activer** s’il n’est pas déjà activé.

    ![Activer TCP](./media/virtual-machines-sql-server-connection-tcp-protocol/enable-tcp.png)

1. Dans le volet de console hello, cliquez sur **SQL Server Services**. Dans le volet d’informations hello, cliquez sur  **SQL Server (*nom de l’instance*) ** (instance par défaut de hello est **SQL Server (MSSQLSERVER)**), puis cliquez sur **redémarrer** , instance de hello toostop et redémarrage de SQL Server.

    ![Redémarrer le moteur de base de données](./media/virtual-machines-sql-server-connection-tcp-protocol/restart-sql-server.png)

1. Fermez le Gestionnaire de configuration de SQL Server.

Pour plus d’informations sur l’activation des protocoles pour hello du moteur de base de données SQL Server, consultez [activer ou désactiver un protocole réseau serveur](http://msdn.microsoft.com/library/ms191294.aspx).
