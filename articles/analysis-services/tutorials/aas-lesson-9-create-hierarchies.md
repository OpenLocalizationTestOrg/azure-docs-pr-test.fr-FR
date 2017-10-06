---
titre : aaa « leçon du didacticiel Azure Analysis Services 9 : créer des hiérarchies | Description de Microsoft Docs » : services : analysis services documentationcenter : '' auteur : minewiskan manager : erikre éditeur : '' balises : ».

MS.AssetId : ms.service : ms.devlang d’analysis services : NA ms.topic : get-started-article ms.tgt_pltfrm : NA ms.workload : na ms.date : 26/05/2017 ms.author : owend
---
# <a name="lesson-9-create-hierarchies"></a>Leçon 9 : Créer des hiérarchies

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Dans cette leçon, vous allez créer des hiérarchies. Les hiérarchies sont des groupes de colonnes organisées en niveaux. Par exemple, la hiérarchie Géographie peut comporter des sous-niveaux correspondant à des pays, des régions, des départements et des villes. Les hiérarchies peuvent apparaître séparément des autres colonnes dans une liste de champs à application client de création de rapports, ce qui les rend plus facile pour les clients utilisateurs toonavigate et inclure dans un rapport. toolearn, voir [hiérarchies](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular)
  
toocreate hiérarchies, utilisez le Générateur de modèles hello dans *vue de diagramme*. La création et la gestion des hiérarchies ne sont pas prises en charge dans la vue de données.  
  
Estimé temps toocomplete cette leçon : **20 minutes**  
  
## <a name="prerequisites"></a>Composants requis  
Cette rubrique fait partie d’un didacticiel de modélisation tabulaire, qui doit être suivi dans l’ordre prévu. Avant d’effectuer les tâches de hello dans cette leçon, vous devez avoir terminé les leçon précédente hello : [leçon 8 : créer des perspectives](../tutorials/aas-lesson-8-create-perspectives.md).  
  
## <a name="create-hierarchies"></a>Créer des hiérarchies  
  
#### <a name="toocreate-a-category-hierarchy-in-hello-dimproduct-table"></a>toocreate une hiérarchie de catégorie dans la table DimProduct de hello  
  
1.  Dans le Concepteur de modèle hello (vue de diagramme), avec le bouton droit hello **DimProduct** table > **créer une hiérarchie**. Une nouvelle hiérarchie apparaît au bas de hello de fenêtre de la table hello. Renommer la hiérarchie de hello **catégorie**.  
  
2.  Cliquez et faites glisser hello **ProductCategoryName** toohello colonne nouvelle **catégorie** hiérarchie.  
  
3.  Bonjour **catégorie** hiérarchie, avec le bouton hello **ProductCategoryName** > **renommer**, puis tapez **catégorie**.  
  
    > [!NOTE]  
    > Si vous renommez une colonne dans une hiérarchie ne renomme pas cette colonne dans la table de hello. Une colonne dans une hiérarchie est simplement une représentation sous forme de colonne hello dans la table de hello.  
  
4.  Cliquez et faites glisser hello **ProductSubcategoryName** colonne toohello **catégorie** hiérarchie. Renommez cette colonne **Sous-catégorie**. 
  
5.  Avec le bouton hello **ModelName** colonne > **ajouter toohierarchy**, puis sélectionnez **catégorie**. Renommez cette colonne **Modèle**.

6.  Enfin, ajoutez **EnglishProductName** toohello hiérarchie de catégorie. Renommez cette colonne **Produit**.  

    ![aas-lesson9-category](../tutorials/media/aas-lesson9-category.png)
  
#### <a name="toocreate-hierarchies-in-hello-dimdate-table"></a>hiérarchies toocreate dans la table DimDate de hello  
  
1.  Bonjour **DimDate** table, créer une hiérarchie nommée **calendrier**.  
  
3.  Ajoutez hello suivant des colonnes dans l’ordre :

    *  CalendarYear
    *  CalendarSemester
    *  CalendarQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
    
4.  Bonjour **DimDate** table, créez un **Fiscal** hiérarchie. Inclure hello suivant des colonnes dans l’ordre :  
  
    *  FiscalYear
    *  FiscalSemester
    *  FiscalQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
  
5.  Enfin, dans hello **DimDate** table, créez un **ProductionCalendar** hiérarchie. Inclure hello suivant des colonnes dans l’ordre :  
    *  CalendarYear
    *  WeekNumberOfYear
    *  DayNumberOfWeek
  
 ## <a name="whats-next"></a>Et ensuite ?
[Leçon 10 : Créer des partitions](../tutorials/aas-lesson-10-create-partitions.md). 
  
  
