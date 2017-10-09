Vous pouvez maintenant utiliser l’outil d’Explorateur de données de hello Bonjour toocreate portail Azure une base de données et de la collection. 

1. Bonjour portail Azure, dans le menu de navigation gauche hello, cliquez sur **Explorateur de données (version préliminaire)**. 

2. Sur hello **Explorateur de données (version préliminaire)** panneau, cliquez sur **nouvelle Collection**, puis fournissez hello informations suivantes :

    ![Bonjour Azure portail Panneau de l’Explorateur de données](./media/cosmos-db-create-collection/azure-cosmosdb-data-explorer.png)

    Paramètre|Valeur suggérée|Description
    ---|---|---
    ID de base de données|Tâches|nom Hello pour votre nouvelle base de données. Les noms de base de données doivent comporter entre 1 et 255 caractères, et ne peuvent pas contenir les caractères /, \\, # ou ?, ni d’espace de fin.
    ID de la collection|Éléments|nom Hello pour votre nouvelle collection. Les noms de collection ont hello même exigences telles que l’ID de base de données de caractères.
    Capacité de stockage| Fixe (10 Go)|Utilisez la valeur par défaut de hello. Cette valeur est la capacité de stockage hello de base de données hello.
    Throughput|400 RU|Utilisez la valeur par défaut de hello. Si vous souhaitez une latence tooreduce, vous pouvez monter le débit hello plus tard.
    Clé de partition|/category|Une clé de partition qui distribue uniformément les données tooeach partition. Clé de partition correct en sélectionnant hello est important pour la création d’une collection performant. toolearn, voir [conception pour le partitionnement](../articles/cosmos-db/partition-data.md#designing-for-partitioning).    
3. Une fois le formulaire de hello terminé, cliquez sur **OK**.

L’Explorateur de données affiche hello nouvelle base de données et une collection. 
