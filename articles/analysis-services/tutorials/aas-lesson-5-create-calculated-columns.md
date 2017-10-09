---
titre : aaa « leçon du didacticiel Azure Analysis Services 5 : créer des colonnes calculées | Description de Microsoft Docs » : décrit comment toocreate calculées des colonnes dans le projet du didacticiel hello Azure Analysis Services. Services : analysis services documentationcenter : '' auteur : minewiskan manager : erikre éditeur : '' balises : ».

MS.AssetId : ms.service : ms.devlang d’analysis services : NA ms.topic : get-started-article ms.tgt_pltfrm : NA ms.workload : na ms.date : 01/06/2017 ms.author : owend
---
# <a name="lesson-5-create-calculated-columns"></a>Leçon 5 : Créer des colonnes calculées

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Dans le cadre de cette leçon, vous créez des données dans votre modèle en ajoutant des colonnes calculées. Vous pouvez créer des colonnes calculées (en tant que colonnes personnalisées) lorsque vous utilisez obtenir des données, à l’aide de l’éditeur de requête hello ou plus loin dans le type de Concepteur de modèle hello suivre ici. toolearn, voir [des colonnes calculées](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns).
  
Vous créez cinq colonnes calculées dans trois tables différentes. Hello étapes sont légèrement différentes pour chaque tâche indiquant de plusieurs manières toocreate colonnes, les renommer et les placer à différents emplacements dans une table.  

Cette leçon vous permet également d’utiliser pour la première fois le langage DAX (Data Analysis Expressions). DAX est un langage spécial permettant de créer des expressions de formule hautement personnalisables pour les modèles tabulaires. Dans ce didacticiel, vous utilisez les colonnes calculée de toocreate DAX, les mesures et les filtres de rôle. toolearn, voir [DAX dans les modèles tabulaires](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular). 
  
Estimé temps toocomplete cette leçon : **15 minutes**  
  
## <a name="prerequisites"></a>Composants requis  
Cette rubrique fait partie d’un didacticiel de modélisation tabulaire, qui doit être suivi dans l’ordre prévu. Avant d’effectuer les tâches de hello dans cette leçon, vous devez avoir terminé les leçon précédente hello : [leçon 4 : créer des relations](../tutorials/aas-lesson-4-create-relationships.md). 
  
## <a name="create-calculated-columns"></a>Créer des colonnes calculées  
  
#### <a name="create-a-monthcalendar-calculated-column-in-hello-dimdate-table"></a>Créer une colonne calculée MonthCalendar dans la table DimDate de hello  
  
1.  Cliquez sur hello **modèle** menu > **vue de modèle** > **vue données**.  
  
    Les colonnes calculées peuvent uniquement être créées à l’aide du Générateur de modèles hello dans la vue de données.  
  
2.  Dans le Concepteur de modèle hello, cliquez sur hello **DimDate** table (onglet).  
  
3.  Avec le bouton hello **CalendarQuarter** en-tête de colonne, puis cliquez sur **insérer une colonne**.  
  
    Une nouvelle colonne nommée **1 de colonne calculée** est inséré toohello gauche hello **trimestre** colonne.  
  
4.  Dans la barre de formule hello au-dessus de table de hello, tapez Bonjour DAX formule suivante : vous aide à la saisie semi-automatique vous tapez hello des noms complets des colonnes et tables et listes hello des fonctions qui sont disponibles.  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    Des valeurs remplissent ensuite toutes les lignes hello dans la colonne calculée de hello. Si vous faites défiler la table de hello, vous consultez lignes peuvent avoir des valeurs différentes pour cette colonne, en fonction des données hello dans chaque ligne.    
  
5.  Renommer cette colonne trop**MonthCalendar**. 

    ![aas-lesson5-newcolumn](../tutorials/media/aas-lesson5-newcolumn.png) 
  
colonne calculée de MonthCalendar Hello fournit un nom triable pour le mois.  
  
#### <a name="create-a-dayofweek-calculated-column-in-hello-dimdate-table"></a>Créer une colonne calculée DayOfWeek dans la table DimDate de hello  
  
1.  Avec hello **DimDate** toujours active, cliquez sur hello **colonne** menu, puis sur **ajouter une colonne**.  
  
2.  Dans la barre de formule hello, tapez hello formule suivante :  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    Lorsque vous avez terminé de créer la formule de hello, appuyez sur ENTRÉE. Hello nouvelle colonne est ajoutée toohello plus à droite de la table de hello.  
  
3.  Renommer les colonnes hello trop**DayOfWeek**.  
  
4.  Cliquez sur l’en-tête de colonne hello, puis faites glisser les colonnes hello entre hello **EnglishDayNameOfWeek** colonne et hello **DayNumberOfMonth** colonne.  
  
    > [!TIP]  
    > Déplacer les colonnes dans votre table rend toonavigate plus facile.  
  
colonne calculée de Hello DayOfWeek fournit un nom triable pour le jour hello de la semaine.  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-hello-dimproduct-table"></a>Créer une colonne calculée ProductSubcategoryName dans la table DimProduct de hello  
  
  
1.  Bonjour **DimProduct** table, faites défiler toohello plus à droite de la table de hello. Colonne de notification hello plus à droite est nommée **ajouter une colonne** (en italique), cliquez sur l’en-tête de colonne hello.  
  
2.  Dans la barre de formule hello, tapez hello formule suivante :  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  Renommer les colonnes hello trop**ProductSubcategoryName**.  
  
colonne calculée de Hello ProductSubcategoryName est toocreate utilisé une hiérarchie dans la table DimProduct hello, qui inclut des données à partir de la colonne de EnglishProductSubcategoryName hello dans la table DimProductSubcategory de hello. Les hiérarchies ne peuvent pas couvrir plusieurs tables. Vous créerez des hiérarchies ultérieurement, dans le cadre de la Leçon 9.  
  
#### <a name="create-a-productcategoryname-calculated-column-in-hello-dimproduct-table"></a>Créer une colonne calculée ProductCategoryName dans la table DimProduct de hello  
  
1.  Avec hello **DimProduct** toujours active, cliquez sur hello **colonne** menu, puis sur **ajouter une colonne**.  
  
2.  Dans la barre de formule hello, tapez hello formule suivante :  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  Renommer les colonnes hello trop**ProductCategoryName**.  
  
colonne calculée de ProductCategoryName Hello est toocreate utilisé une hiérarchie dans la table DimProduct hello, qui inclut des données à partir de la colonne de EnglishProductCategoryName hello dans la table de DimProductCategory hello. Les hiérarchies ne peuvent pas couvrir plusieurs tables.  
  
#### <a name="create-a-margin-calculated-column-in-hello-factinternetsales-table"></a>Créer une colonne calculée de marge dans la table FactInternetSales de hello  
  
1.  Dans le Concepteur de modèle hello, sélectionnez hello **FactInternetSales** table.  
  
2.  Créer une nouvelle colonne calculée entre hello **SalesAmount** colonne et hello **TaxAmt** colonne.  
  
3.  Dans la barre de formule hello, tapez hello formule suivante :  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  Renommer les colonnes hello trop**marge**.  
 
      ![aas-lesson5-newmargin](../tutorials/media/aas-lesson5-newmargin.png)
      
    colonne calculée de marge Hello est marges tooanalyze utilisés pour chaque vente.  
  
## <a name="whats-next"></a>Et ensuite ?
[Leçon 6 : Créer des mesures](../tutorials/aas-lesson-6-create-measures.md).
  
  
  
