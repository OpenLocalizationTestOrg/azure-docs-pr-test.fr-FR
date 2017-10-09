---
titre : aaa « leçon du didacticiel Azure Analysis Services 4 : créer des relations | Description de Microsoft Docs » : décrit la façon dont les relations toocreate dans hello projet du didacticiel Azure Analysis Services. Services : analysis services documentationcenter : '' auteur : minewiskan manager : erikre éditeur : '' balises : ».

MS.AssetId : ms.service : ms.devlang d’analysis services : NA ms.topic : get-started-article ms.tgt_pltfrm : NA ms.workload : na ms.date : 26/05/2017 ms.author : owend
---
# <a name="lesson-4-create-relationships"></a>Leçon 4 : Créer des relations

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Dans cette leçon, vous vérifiez les relations hello qui ont été créées automatiquement lorsque vous avez importé des données et ajoutez de nouvelles relations entre les différentes tables. Une relation est une connexion entre deux tables qui établit la corrélation des données hello dans ces tables. Par exemple, table de hello DimProduct et DimProductSubcategory hello ont une relation basée sur des faits hello que chaque produit appartienne tooa sous-catégorie. toolearn, voir [relations](https://docs.microsoft.com/sql/analysis-services/tabular-models/relationships-ssas-tabular).
  
Estimé temps toocomplete cette leçon : **10 minutes**  
  
## <a name="prerequisites"></a>Composants requis  
Cette rubrique fait partie d’un didacticiel de modélisation tabulaire, qui doit être suivi dans l’ordre prévu. Avant d’effectuer les tâches de hello dans cette leçon, vous devez avoir terminé les leçon précédente hello : [leçon 3 : marquer en tant que Table de dates](../tutorials/aas-lesson-3-mark-as-date-table.md). 
  
## <a name="review-existing-relationships-and-add-new-relationships"></a>Vérifier les relations existantes et ajouter de nouvelles relations  
Lorsque vous avez importé des données à l’aide d’obtenir des données, que vous avez obtenu sept tables de base de données AdventureWorksDW2014 hello. En règle générale, lorsque vous importez des données à partir d’une source relationnelle, les relations existantes sont importées automatiquement avec les données de salutation. Toutefois, avant de poursuivre avec la création de votre modèle, vous devez vérifier que les relations entre les tables ont été créées correctement. Pour ce didacticiel, vous ajoutez trois nouvelles relations.  
  
#### <a name="tooreview-existing-relationships"></a>relations existantes tooreview  
  
1.  Cliquez sur hello **modèle** menu > **vue de modèle** > **vue de diagramme**.  

    Hello Générateur de modèles apparaît maintenant dans la vue de diagramme, un format graphique affichant toutes les tables hello que vous importées et les lignes entre eux. lignes Hello entre les tables indiquent les relations de hello qui ont été créées automatiquement lorsque vous avez importé les données de salutation.
    
    ![aas-lesson4-diagram](../tutorials/media/aas-lesson4-diagram.png)
  
    Inclure autant de tables hello que possible à l’aide de contrôles de la minicarte dans le coin inférieur droit de hello du Générateur de modèles hello. Vous pouvez également cliquez et faites glisser d’emplacements toodifferent de tables, regrouper les tables plus proche ou en les plaçant dans un ordre particulier. Déplacement de tables n’affecte pas les relations hello déjà entre les tables de hello. tooview toutes les colonnes hello dans une table particulière, cliquez et faites glisser sur un tooexpand de bord de table ou réduire sa taille.  
  
2.  Sur la ligne pleine entre hello hello **DimCustomer** table et hello **DimGeography** table. trait plein de Hello entre ces deux tables indique que cette relation est active, autrement dit, qu'il est utilisé par défaut lors du calcul des formules DAX.  
  
    Hello d’avis **GeographyKey** colonne Bonjour **DimCustomer** table et hello **GeographyKey** colonne Bonjour **DimGeography** table apparaissent maintenant chacune dans une zone. Ces colonnes sont utilisées dans la relation de hello. Hello propriétés de la relation apparaissent maintenant aussi Bonjour **propriétés** fenêtre.  
  
    > [!TIP]  
    > En outre toousing hello Générateur de modèles dans la vue de diagramme, vous pouvez également utiliser hello gérer les relations boîte de dialogue zone tooshow hello des relations entre toutes les tables dans un format de table. Dans l’Explorateur de modèles tabulaires, cliquez sur **Relations** > **Gérer les relations**.
  
3.  Vérifiez que hello suit les relations ont été créée lorsque chacune des tables de hello ont été importées à partir de la base de données AdventureWorksDW hello :  
  
    |Actif|Table|Table de recherche associée|  
    |----------|---------|------------------------|  
    |Oui|**DimCustomer [GeographyKey]**|**DimGeography [GeographyKey]**|  
    |Oui|**DimProduct [ProductSubcategoryKey]**|**DimProductSubcategory [ProductSubcategoryKey]**|  
    |Oui|**DimProductSubcategory [ProductCategoryKey]**|**DimProductCategory [ProductCategoryKey]**|  
    |Oui|**FactInternetSales [CustomerKey]**|**DimCustomer [CustomerKey]**|  
    |Oui|**FactInternetSales [ProductKey]**|**DimProduct [ProductKey]**|  
  
    Si une des relations de hello sont manquante, vérifiez que votre modèle inclut les tableaux suivants de hello : DimCustomer, DimDate, DimGeography, DimProduct, DimProductCategory, DimProductSubcategory et FactInternetSales. Si les tables à partir de hello même connexion de source de données sont importées à séparent les heures, toutes les relations entre ces tables ne sont pas créées et doivent être créées manuellement.  

### <a name="take-a-closer-look"></a>Examen approfondi
Dans la vue de diagramme, notez une flèche, un astérisque et un nombre de lignes hello qui montrent la relation hello entre les tables.

![aas-lesson4-line](../tutorials/media/aas-lesson4-line.png)

flèche de Hello indique la direction du filtrage hello. astérisque de Hello montre que cette table est hello côté « plusieurs » de la cardinalité de la relation hello et hello un élément indique cette table est hello côté « un » de la relation de hello. Si vous avez besoin de tooedit une relation ; par exemple, modifiez la direction du filtrage ou la cardinalité de la relation hello, double-cliquez sur hello ligne tooopen hello modifier la relation boîte de dialogue relation.

![aas-lesson4-edit](../tutorials/media/aas-lesson4-edit.png)

Ces fonctionnalités sont destinées à la modélisation des données avancées et étendue de hello en dehors de ce didacticiel. toolearn, voir [bidirectionnelles entre les filtres pour les modèles tabulaires dans Analysis Services](https://docs.microsoft.com/sql/analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services).

Dans certains cas, vous devrez peut-être toocreate des relations supplémentaires entre les tables dans votre modèle de toosupport certaine logique métier. Pour ce didacticiel, vous devez toocreate trois relations supplémentaires entre les tables de FactInternetSales hello et hello DimDate.  
  
#### <a name="tooadd-new-relationships-between-tables"></a>relations entre les tables tooadd  
  
1.  Dans le Concepteur de modèle hello, Bonjour **FactInternetSales** table, cliquez et maintenez la sélection hello **OrderDate** colonne, puis faites glisser hello curseur toohello **Date** colonne Bonjour  **DimDate** de table et relâchez.  

    Une ligne pleine apparaît et indique que vous avez créé une relation active entre hello **OrderDate** colonne Bonjour **Internet Sales** table et hello **Date** colonne Bonjour **Date** table. 
  
      ![aas-lesson4-new](../tutorials/media/aas-lesson4-new.png) 
  
    > [!NOTE]  
    > Lors de la création de relations, la direction de cardinalité et filtre hello entre la table primaire de hello et de la table de recherche associée hello est sélectionnée automatiquement.  
  
2.  Bonjour **FactInternetSales** table, cliquez sur et maintenez la sélection hello **DueDate** colonne, puis faites glisser hello curseur toohello **Date** colonne Bonjour **DimDate** de table et relâchez.  
  
    Une ligne pointillée apparaît indique que vous avez créé une relation inactive entre hello **DueDate** colonne Bonjour **FactInternetSales** table et hello **Date** colonne Hello **DimDate** table. Vous pouvez avoir plusieurs relations entre les tables, mais une seule relation peut être active à la fois. Les relations inactives peuvent être effectuées tooperform active les agrégations spéciale dans les expressions DAX personnalisées.  
  
3.  Pour finir, créez une dernière relation. Bonjour **FactInternetSales** table, cliquez sur et maintenez la sélection hello **ShipDate** colonne, puis faites glisser hello curseur toohello **Date** colonne Bonjour **DimDate** de table et relâchez.  
    
     ![aas-lesson4-newinactive](../tutorials/media/aas-lesson4-newinactive.png)
  
## <a name="whats-next"></a>Et ensuite ?
[Leçon 5 : Créer des colonnes calculées](../tutorials/aas-lesson-5-create-calculated-columns.md).
  
  
  
