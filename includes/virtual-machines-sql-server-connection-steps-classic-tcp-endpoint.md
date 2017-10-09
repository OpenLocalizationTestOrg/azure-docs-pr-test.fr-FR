### <a name="create-a-tcp-endpoint-for-hello-virtual-machine"></a>Créer un point de terminaison TCP pour la machine virtuelle de hello
Dans l’ordre tooaccess SQL Server à partir de hello internet, ordinateur virtuel de hello doit avoir un toolisten de point de terminaison pour les communications TCP entrantes. Cette étape de configuration Azure dirige TCP port trafic tooa le port TCP entrant qui est accessible toohello virtual machine.

> [!NOTE]
> Si vous vous connectez au sein de hello même service ou de réseau virtuel de cloud, vous n’avez pas toocreate un point de terminaison accessible publiquement. Dans ce cas, vous pouvez continuer toohello prochaine étape. Pour plus d'informations, consultez [Scénarios de connexion](../articles/virtual-machines/windows/sqlclassic/virtual-machines-windows-classic-sql-connect.md#connection-scenarios).
> 
> 

1. Sur hello portail Azure, sélectionnez **machines virtuelles (classiques)**.
2. Sélectionnez ensuite une machine virtuelle SQL Server.
3. Sélectionnez **points de terminaison**, puis cliquez sur hello **ajouter** bouton en haut de hello du panneau des points de terminaison hello.
   
    ![Étapes pour la création d’un point de terminaison sur le portail](./media/virtual-machines-sql-server-connection-steps/portal-endpoint-creation.png)
4. Sur hello **ajouter le point de terminaison** panneau, fournissez un **nom** tels que SQLEndpoint.
5. Sélectionnez **TCP** pour hello **protocole**.
6. Pour **Port public**, spécifiez un numéro de port comme **57500**.
7. Pour **port privé**, spécifiez le port d’écoute de SQL Server, qui utilise par défaut trop**1433**.
8. Cliquez sur **Ok** point de terminaison toocreate hello.

