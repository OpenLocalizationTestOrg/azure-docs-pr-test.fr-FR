
<!--
includes/sql-database-include-connection-string-20-portalshots.md

Latest Freshness check:  2015-09-02 , GeneMi.

## Connection string
-->


### <a name="obtain-hello-connection-string-from-hello-azure-portal"></a>Obtenir la chaîne de connexion hello de hello portail Azure
Hello d’utilisation [portail Azure](https://portal.azure.com/) chaîne de connexion tooobtain hello nécessaire pour votre toointeract de programme client avec la base de données SQL Azure : 

1. Cliquez sur **PARCOURIR** > **Bases de données SQL**.
2. Entrez les nom de hello de votre base de données dans la zone de texte filtre hello près hello coin supérieur gauche de hello **bases de données SQL** panneau.
3. Cliquez sur ligne hello pour votre base de données.
4. Une fois le panneau de hello apparaît pour votre base de données, pour des raisons de commodité visuelle vous pouvez cliquer sur hello standard réduire les panneaux de hello toocollapse contrôles vous permet d’atteindre et de filtrage de la base de données. 
   
    ![Filtrer tooisolate votre base de données][10-FilterDatabase]
5. Dans le panneau de hello pour votre base de données, cliquez sur **afficher les chaînes de connexion de base de données**.
6. Si vous avez l’intention de bibliothèque de connexions ADO.NET toouse hello, copiez la chaîne hello étiqueté **ADO**. 
   
    ![Copier la chaîne de connexion ADO hello pour votre base de données][20-CopyAdoConnectionString]
7. Dans un format ou un autre, collez les informations de chaîne de connexion hello dans votre code de programme client.

Pour plus d'informations, consultez les pages suivantes :<br/>[Chaînes de connexion et fichiers de configuration](http://msdn.microsoft.com/library/ms254494.aspx).

<!-- Image references. -->

[10-FilterDatabase]: ./media/sql-database-include-connection-string-20-portalshots/connqry-connstr-a.png

[20-CopyAdoConnectionString]: ./media/sql-database-include-connection-string-20-portalshots/connqry-connstr-b.png


<!--
These three includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-connection-string-20-portalshots.md
includes/sql-database-include-connection-string-30-compare.md
includes/sql-database-include-connection-string-40-config.md
-->
