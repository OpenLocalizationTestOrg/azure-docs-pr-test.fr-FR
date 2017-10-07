---
titre : aaa « leçon du didacticiel Azure Analysis Services 7 : créer des indicateurs de Performance clés | Description de Microsoft Docs » : décrit comment toocreate des indicateurs de Performance clés dans hello projet du didacticiel Azure Analysis Services. Services : analysis services documentationcenter : '' auteur : minewiskan manager : erikre éditeur : '' balises : ».

MS.AssetId : ms.service : ms.devlang d’analysis services : NA ms.topic : get-started-article ms.tgt_pltfrm : NA ms.workload : na ms.date : 26/05/2017 ms.author : owend
---
# <a name="lesson-7-create-key-performance-indicators"></a>Leçon 7 : Créer des indicateurs de performance clés

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Dans cette leçon, vous allez créer des indicateurs de performance clés (KPI). Indicateurs de performance clés sont utilisées toogauge les performances d’une valeur définie par un *Base* mesure, par rapport à un *cible* valeur également définie par une mesure ou par une valeur absolue. Dans les applications clientes de création de rapports, indicateurs de performance clés offrent aux professionnels un toounderstand rapidement et facilement un résumé des tendances de réussite ou tooidentify business. toolearn, voir [indicateurs de performance clés](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular)
  
Estimé temps toocomplete cette leçon : **15 minutes**  
  
## <a name="prerequisites"></a>Composants requis  
Cette rubrique fait partie d’un didacticiel de modélisation tabulaire, qui doit être suivi dans l’ordre prévu. Avant d’effectuer les tâches de hello dans cette leçon, vous devez avoir terminé les leçon précédente hello : [Leçon 6 : créer des mesures](../tutorials/aas-lesson-6-create-measures.md).   
  
## <a name="create-key-performance-indicators"></a>Créer des indicateurs de performance clés (KPI)  
  
#### <a name="toocreate-an-internetcurrentquartersalesperformance-kpi"></a>toocreate un KPI InternetCurrentQuarterSalesPerformance  
  
1.  Dans le Concepteur de modèle hello, cliquez sur hello **FactInternetSales** table.  
  
2.  Dans la grille de mesures hello, cliquez sur une cellule vide.  
  
3.  Dans la barre de formule hello, au-dessus de table de hello, tapez hello formule suivante : 
 
    ```  
    InternetCurrentQuarterSalesPerformance :=DIVIDE([InternetCurrentQuarterSales]/[InternetPreviousQuarterSalesProportionToQTD],BLANK())  
    ```

    Cette mesure sert de mesure de Base hello pour hello indicateur de performance clé.  
  
4.  Cliquez avec le bouton droit sur **InternetCurrentQuarterSalesPerformance** > **Créer un KPI**.   
  
5.  Dans la boîte de dialogue indicateur de Performance clé (KPI) hello dans **cible** sélectionnez **valeur absolue**, puis tapez **1.1**.  
  
7.  Dans le champ de gauche (bas) du curseur hello, tapez **1**, puis dans le curseur de hello droit (élevé), tapez **1.07**.  
  
8.  Dans **sélectionner le Style d’icône**, sélectionnez le triangle de losange (rouge), hello (jaune), cercle de type d’icône (vert).
  
    ![aas-lesson7-kpi](../tutorials/media/aas-lesson7-kpi.png)
    
    > [!TIP]  
    > Hello avis extensible **Descriptions** étiquette au-dessous des styles d’icône disponibles hello. Utilisez les descriptions de hello toomake d’éléments différents indicateurs de performance clés les plus identifiable dans les applications clientes.  
  
9. Cliquez sur **OK** toocomplete hello indicateur de performance clé.  
  
    Dans la grille de mesures hello, notez toohello suivante icône de hello **InternetCurrentQuarterSalesPerformance** mesure. Cette icône indique que cette mesure sert de valeur de base pour un indicateur KPI.  
  
#### <a name="toocreate-an-internetcurrentquartermarginperformance-kpi"></a>toocreate un KPI InternetCurrentQuarterMarginPerformance  
  
1.  Dans la grille de mesures hello pour hello **FactInternetSales** , cliquez sur une cellule vide.  
  
2.  Dans la barre de formule hello, au-dessus de table de hello, tapez hello formule suivante :  

    ```
    InternetCurrentQuarterMarginPerformance :=IF([InternetPreviousQuarterMarginProportionToQTD]<>0,([InternetCurrentQuarterMargin]-[InternetPreviousQuarterMarginProportionToQTD])/[InternetPreviousQuarterMarginProportionToQTD],BLANK())  
    ```
 
3.  Cliquez avec le bouton droit sur **InternetCurrentQuarterMarginPerformance** > **Créer un KPI**.  
  
4.  Dans la boîte de dialogue indicateur de Performance clé (KPI) hello dans **cible** sélectionnez **valeur absolue**, puis tapez **1.25**.   
  
5.  Dans le champ de gauche (bas) du curseur hello, faites glisser jusqu'à ce que le champ de hello affiche **0,8**, et puis hello de diapositive avec le bouton droit champ de curseur (élevé), jusqu'à ce que le champ de hello affiche **1.03**.  
  
6.  Dans **sélectionner le Style d’icône**, sélectionnez losange hello (rouge), triangle (jaune), type d’icône de cercle (vert), puis cliquez sur **OK**.  
  
## <a name="whats-next"></a>Et ensuite ?
[Leçon 8 : Créer des perspectives](../tutorials/aas-lesson-8-create-perspectives.md).
  
  
