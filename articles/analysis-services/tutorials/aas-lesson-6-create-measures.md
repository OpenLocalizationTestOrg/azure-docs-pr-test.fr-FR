---
titre : aaa « leçon du didacticiel Azure Analysis Services 6 : créer des mesures | Description de Microsoft Docs » : décrit comment toocreate mesure dans le projet du didacticiel hello Azure Analysis Services. Services : analysis services documentationcenter : '' auteur : minewiskan manager : erikre éditeur : '' balises : ».

MS.AssetId : ms.service : ms.devlang d’analysis services : NA ms.topic : get-started-article ms.tgt_pltfrm : NA ms.workload : na ms.date : 01/06/2017 ms.author : owend
---
# <a name="lesson-6-create-measures"></a>Leçon 6 : Créer des mesures

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Dans cette leçon, vous créez toobe de mesures inclus dans votre modèle. Toohello similaire calculée des colonnes que vous avez créé, une mesure est un calcul créé à l’aide d’une formule DAX. Toutefois, contrairement aux colonnes calculées, les mesures sont évaluées sur la base d’un *filtre* sélectionné par l’utilisateur. Par exemple, une colonne particulière ou un segment ajoutée champ des étiquettes de ligne toohello dans un tableau croisé dynamique. Une valeur pour chaque cellule de filtre de hello est ensuite calculée par mesure de hello appliqué. Les mesures sont des calculs puissants et flexibles que vous souhaitez tooinclude dans presque tous les calculs dynamiques tooperform de modèles tabulaires sur des données numériques. toolearn, voir [mesures](https://docs.microsoft.com/sql/analysis-services/tabular-models/measures-ssas-tabular).
  
les mesures toocreate, vous utilisez hello *grille de mesures*. Par défaut, chaque table comprend une grille de mesures vide. Toutefois, la plupart du temps, vous n’êtes pas obligé de créer des mesures pour chaque table. grille de mesures Hello s’affiche sous une table dans le Générateur de modèles hello dans la vue de données. grille de mesures hello toohide ou afficher une table, cliquez sur hello **Table** menu, puis sur **afficher la grille de mesures**.  
  
Vous pouvez créer une mesure en cliquant sur une cellule vide dans la grille de mesures hello, puis en tapant une formule DAX dans la barre de formule hello. Lorsque vous cliquez sur entrer une formule hello toocomplete, les mesures hello puis apparaît dans la cellule de hello. Vous pouvez également créer des mesures à l’aide d’une fonction d’agrégation standard en cliquant sur une colonne, puis en cliquant sur hello bouton Somme automatique (**∑**) sur la barre d’outils hello. Les mesures créées à l’aide de la fonction de somme automatique hello apparaissent dans la cellule de grille de mesures hello directement sous la colonne de hello, mais peuvent être déplacés.  
  
Dans cette leçon, vous créez les mesures en entrant une formule DAX dans la barre de formule hello et en utilisant la fonction de somme automatique hello.  
  
Estimé temps toocomplete cette leçon : **30 minutes**  
  
## <a name="prerequisites"></a>Composants requis  
Cette rubrique fait partie d’un didacticiel de modélisation tabulaire, qui doit être suivi dans l’ordre prévu. Avant d’effectuer les tâches de hello dans cette leçon, vous devez avoir terminé les leçon précédente hello : [leçon 5 : créer des colonnes calculées](../tutorials/aas-lesson-5-create-calculated-columns.md).  
  
## <a name="create-measures"></a>Créer des mesures  
  
#### <a name="toocreate-a-dayscurrentquartertodate-measure-in-hello-dimdate-table"></a>toocreate une mesure DaysCurrentQuarterToDate dans la table DimDate de hello  
  
1.  Dans le Concepteur de modèle hello, cliquez sur hello **DimDate** table.  
  
2.  Dans la grille de mesures hello, cliquez sur cellule vide en haut à gauche de hello.  
  
3.  Dans la barre de formule hello, tapez hello formule suivante :  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    Avis hello supérieur gauche de la cellule contient désormais un nom de mesure, **DaysCurrentQuarterToDate**, suivi par le résultat de hello, **92**.
    
      ![aas-lesson6-newmeasure](../tutorials/media/aas-lesson6-newmeasure.png) 
    
    Contrairement aux colonnes calculées, des formules de mesure vous pouvez taper un nom de la mesure hello, suivie du signe deux-points, suivi d’une expression de la formule hello.

  
#### <a name="toocreate-a-daysincurrentquarter-measure-in-hello-dimdate-table"></a>toocreate une mesure DaysInCurrentQuarter dans la table DimDate de hello  
  
1.  Avec hello **DimDate** toujours active dans le Concepteur de modèle hello, dans la grille de mesures hello, cliquez sur la cellule vide de hello sous mesure hello que vous avez créé.  
  
2.  Dans la barre de formule hello, tapez hello formule suivante :  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    Lorsque vous créez un rapport de comparaison entre une période incomplète et hello période précédente. formule de Hello doit calculer la proportion de hello de période hello qui s’est écoulée et comparez-la toohello même proportion Bonjour période précédente. Dans ce cas, [DaysCurrentQuarterToDate] / [DaysInCurrentQuarter] donne hello proportion écoulé Bonjour période en cours.  
  
#### <a name="toocreate-an-internetdistinctcountsalesorder-measure-in-hello-factinternetsales-table"></a>toocreate une mesure de InternetDistinctCountSalesOrder dans la table FactInternetSales de hello  
  
1.  Cliquez sur hello **FactInternetSales** table.   
  
2.  Cliquez sur hello **SalesOrderNumber** en-tête de colonne.  
  
3.  Barre d’outils hello, cliquez sur hello flèche toohello suivant Somme automatique (**∑**), puis **DistinctCount**.  
  
    fonction de somme automatique Hello crée automatiquement une mesure pour la colonne sélectionnée de hello à l’aide de la formule de regroupement standard DistinctCount hello.  
    
       ![aas-lesson6-newmeasure2](../tutorials/media/aas-lesson6-newmeasure2.png)
  
4.  Dans la grille de mesures hello, cliquez sur Nouvelle mesure de hello, puis dans hello **propriétés** fenêtre, dans **nom de la mesure**, renommez les mesures hello trop**InternetDistinctCountSalesOrder**. 
 
  
#### <a name="toocreate-additional-measures-in-hello-factinternetsales-table"></a>toocreate des mesures supplémentaires dans la table FactInternetSales de hello  
  
1.  En utilisant la fonction de somme automatique hello, créez et nommez les hello suivant de mesures :  

    |Colonne|Nom de la mesure|Somme automatique (∑)|Formule|  
    |----------------|----------|-----------------|-----------|  
    |SalesOrderLineNumber|InternetOrderLinesCount|Nombre|=COUNTA([SalesOrderLineNumber])|  
    |OrderQuantity|InternetTotalUnits|Somme|=SUM([OrderQuantity])|  
    |DiscountAmount|InternetTotalDiscountAmount|Somme|=SUM([DiscountAmount])|  
    |TotalProductCost|InternetTotalProductCost|Somme|=SUM([TotalProductCost])|  
    |SalesAmount|InternetTotalSales|Somme|=SUM([SalesAmount])|  
    |Margin|InternetTotalMargin|Somme|=SUM([Margin])|  
    |TaxAmt|InternetTotalTaxAmt|Somme|=SUM([TaxAmt])|  
    |Freight|InternetTotalFreight|Somme|=SUM([Freight])|  
  
2.  En cliquant sur une cellule vide dans la grille de mesures hello et à l’aide de barre de formule hello, créer et les mesures suivantes hello de nom dans l’ordre :  
  
      ```
      InternetPreviousQuarterMargin:=CALCULATE([InternetTotalMargin],PREVIOUSQUARTER('DimDate'[Date]))
      ```
      
      ```
      InternetCurrentQuarterMargin:=TOTALQTD([InternetTotalMargin],'DimDate'[Date])
      ```
  
      ```
      InternetPreviousQuarterMarginProportionToQTD:=[InternetPreviousQuarterMargin]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
      ```
      InternetPreviousQuarterSales:=CALCULATE([InternetTotalSales],PREVIOUSQUARTER('DimDate'[Date]))
      ```
  
      ```
      InternetCurrentQuarterSales:=TOTALQTD([InternetTotalSales],'DimDate'[Date])
      ```
      
      ```
      InternetPreviousQuarterSalesProportionToQTD:=[InternetPreviousQuarterSales]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
Les mesures créées pour la table FactInternetSales de hello peuvent être utilisé tooanalyze des données financières critiques telles que les ventes et les coûts, marge bénéficiaire des éléments définis par le filtre de hello utilisateur sélectionné.  
  
## <a name="whats-next"></a>Et ensuite ?
[Leçon 7 : Afficher les indicateurs de performance clés](../tutorials/aas-lesson-7-create-key-performance-indicators.md).  

  
