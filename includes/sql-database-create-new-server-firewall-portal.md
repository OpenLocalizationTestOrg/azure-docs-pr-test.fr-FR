
<!--
includes/sql-database-create-new-server-firewall-portal.md

Latest Freshness check:  2016-11-28 , rickbyh.

As of circa 2016-04-11, hello following topics might include this include:
articles/sql-database/sql-database-get-started.md
articles/sql-database/sql-database-configure-firewall-settings
articles/sql-data-warehouse-get-started-provision.md

-->
### <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a>Créer une règle de pare-feu de niveau serveur dans hello portail Azure

1. Dans le panneau de serveur SQL hello, sous Paramètres, cliquez sur **pare-feu** Panneau de pare-feu tooopen hello pour SQL server de hello.

    <!-- ![sql server firewall](../articles/sql-database/media/sql-database-get-started/sql-server-firewall.png) -->

2. Vérifiez l’adresse IP du client hello affiché et valider qu’il s’agit de votre adresse IP sur Internet à l’aide d’un navigateur de votre choix de hello (demandez « quel est mon adresse IP). Parfois, elles ne correspondent pas pour diverses raisons.

    <!-- ![your IP address](../articles/sql-database/media/sql-database-get-started/your-ip-address.png) -->

3. En supposant que les adresses IP de hello correspondent, cliquez sur **ajouter l’adresse IP du client** sur la barre d’outils hello.

    ![add client IP](../articles/sql-data-warehouse/media/sql-data-warehouse-get-started-provision/add-client-ip.png)

    > [!NOTE]
    > Vous pouvez ouvrir le pare-feu de base de données SQL hello hello tooa unique adresse IP de serveur ou d’une plage entière d’adresses. Ouverture hello pare-feu permet aux administrateurs SQL et les utilisateurs toologin tooany base de données sur hello toowhich serveur comportant des informations d’identification valides.
    >

4. Cliquez sur **enregistrer** dans hello toosave de barre d’outils de cette règle de pare-feu de niveau serveur, puis sur **OK**.

    ![add client IP](../articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule.png)

> [!Tip]
> Pour trouver un didacticiel, consultez [Didacticiel sur la base de données SQL : création d’un serveur, d’une règle de pare-feu de niveau serveur, d’un exemple de base de données, d’une règle de pare-feu de niveau base de données et connexion à SQL Server](../articles/sql-database/sql-database-get-started.md).    
>
