Vous pouvez maintenant utiliser outil Explorateur de données de hello Bonjour toocreate portail Azure une base de données de graphique. 

1. Bonjour portail Azure, dans le menu de navigation gauche hello, cliquez sur **Explorateur de données (version préliminaire)**. 
2. Bonjour **Explorateur de données (version préliminaire)** panneau, cliquez sur **nouveau graphique**, puis renseignez page hello à l’aide de hello informations suivantes.

    ![Explorateur de données Bonjour portail Azure](./media/cosmos-db-create-graph/azure-cosmosdb-data-explorer.png)

    Paramètre|Valeur suggérée|Description
    ---|---|---
    ID de base de données|sample-database|ID de Hello pour votre nouvelle base de données. Les noms de base de données doivent inclure entre 1 et 255 caractères et ne peuvent pas contenir `/ \ # ?` ni d’espace de fin.
    ID de graphique|sample-graph|ID de Hello pour votre nouveau graphique. Les noms de graphique ont hello même caractère spécifications en tant qu’ID de base de données.
    Capacité de stockage| 10 Go|Laissez la valeur par défaut de hello. Il s’agit de la capacité de stockage hello de base de données hello.
    Throughput|400 unités de requête|Laissez la valeur par défaut de hello. Vous pouvez monter le débit hello ultérieurement si vous souhaitez une latence tooreduce.
    Clé de partition|/userid|Une clé de partition qui distribue uniformément les données tooeach partition. En sélectionnant hello correct de clé de partition est importante pour la création d’un performants du graphique, en savoir plus sur dans [conception pour le partitionnement](../articles/cosmos-db/partition-data.md#designing-for-partitioning).

3. Une fois le formulaire de hello est rempli, cliquez sur **OK**.
