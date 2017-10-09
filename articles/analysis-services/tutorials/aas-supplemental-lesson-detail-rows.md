---
titre : aaa « leçon supplémentaire du didacticiel Azure Analysis Services : les lignes de détails | Description de Microsoft Docs » : décrit comment toocreate une Expression de lignes de détail dans hello didacticiel Azure Analysis Services.
Services : analysis services documentationcenter : '' auteur : minewiskan manager : erikre éditeur : '' balises : ».

MS.AssetId : ms.service : ms.devlang d’analysis services : NA ms.topic : get-started-article ms.tgt_pltfrm : NA ms.workload : na ms.date : 26/05/2017 ms.author : owend
---
# <a name="supplemental-lesson---detail-rows"></a>Leçon supplémentaire – Lignes de détails

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Dans cette leçon supplémentaire, vous utilisez une Expression de lignes de détail personnalisée hello éditeur DAX toodefine. Une Expression de lignes de détail est une propriété sur une mesure, en fournissant aux utilisateurs plus d’informations sur les résultats hello agrégée d’une mesure. 
  
Estimé temps toocomplete cette leçon : **10 minutes**  
  
## <a name="prerequisites"></a>Composants requis  
Cette rubrique de leçon supplémentaire fait partie d’un didacticiel de modélisation tabulaire. Avant d’effectuer les tâches de hello dans cette leçon supplémentaire, vous devez avoir terminé toutes les leçons précédentes ou avoir un projet de modèle d’exemple Adventure Works Internet Sales terminé.  
  
## <a name="what-do-we-need-toosolve"></a>Comment nous avons besoin de toosolve ?
Examinez les détails hello de votre mesure InternetTotalSales, avant d’ajouter une Expression de lignes de détail.

1.  Dans SSDT, cliquez sur hello **modèle** menu > **analyser dans Excel** tooopen Excel et créer un tableau croisé dynamique vide.
  
2.  Dans **PivotTable Fields**, ajouter hello **InternetTotalSales** trop de mesures à partir de la table FactInternetSales de hello**valeurs**, **CalendarYear**à partir de hello DimDate table trop**colonnes**, et **EnglishCountryRegionName** trop**lignes**. Notre tableau croisé dynamique permet à présent nous des résultats agrégés à partir de la mesure de InternetTotalSales hello en régions et l’année. 

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-pivottable.png)

3. Bonjour tableau croisé dynamique, double-cliquez sur une valeur agrégée pour une année et un nom de région. Nous avons double-cliqué valeur hello pour l’Australie et hello ici année 2014. Cette opération affiche une nouvelle feuille contenant des données dont nous n’avons pas l’utilité.

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-sheet.png)
  
Ce que nous veut toosee ici est une table contenant des colonnes et lignes de données qui contribuent le résultat toohello agrégée de votre mesure InternetTotalSales. toodo que, nous pouvons ajouter une Expression de lignes de détail en tant que propriété de mesure de hello.

## <a name="add-a-detail-rows-expression"></a>Ajouter une expression de lignes de détail

#### <a name="toocreate-a-detail-rows-expression"></a>toocreate une Expression de lignes de détail 
  
1. Dans SSDT, dans la grille de mesures de la table hello FactInternetSales, cliquez sur hello **InternetTotalSales** mesure. 

2. Dans **propriétés** > **Expression de lignes de détail**, cliquez sur Bonjour éditeur bouton tooopen Bonjour éditeur DAX.

    ![aas-lesson-detail-rows-ellipse](../tutorials/media/aas-lesson-detail-rows-ellipse.png)

3. Dans l’éditeur DAX, entrez hello expression suivante :

    ```
    SELECTCOLUMNS(
    FactInternetSales,
    "Sales Order Number", FactInternetSales[SalesOrderNumber],
    "Customer First Name", RELATED(DimCustomer[FirstName]),
    "Customer Last Name", RELATED(DimCustomer[LastName]),
    "City", RELATED(DimGeography[City]),
    "Order Date", FactInternetSales[OrderDate],
    "Internet Total Sales", [InternetTotalSales]
    )

    ```

    Cette expression spécifie les noms de colonnes, et les résultats de mesure à partir de la table FactInternetSales de hello et les tables associées sont retournés lorsqu’un utilisateur double-clique sur un résultat agrégé dans un tableau croisé dynamique ou un rapport.

4. Dans Excel, supprimer une feuille hello créé à l’étape 3, puis double-cliquez sur une valeur agrégée. Cette fois, avec une propriété Expression de lignes de détail définie pour la mesure de hello, une nouvelle feuille s’ouvre contenant des données beaucoup plus utiles.

    ![aas-lesson-detail-rows-detailsheet](../tutorials/media/aas-lesson-detail-rows-detailsheet.png)

5. Redéployez votre modèle.

  
## <a name="see-also"></a>Voir aussi  
[SELECTCOLUMNS, fonction (DAX)](https://msdn.microsoft.com/library/mt761759.aspx)   
[Leçon supplémentaire – Sécurité dynamique](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[Leçon supplémentaire – Hiérarchies déséquilibrées](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)  
