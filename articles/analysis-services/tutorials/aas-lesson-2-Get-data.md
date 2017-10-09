---
titre : aaa « leçon du didacticiel Azure Analysis Services 2 : obtenir les données | Description de Microsoft Docs » : décrit comment tooget et importer des données dans hello projet du didacticiel Azure Analysis Services. Services : analysis services documentationcenter : '' auteur : minewiskan manager : erikre éditeur : '' balises : ».

MS.AssetId : ms.service : ms.devlang d’analysis services : NA ms.topic : get-started-article ms.tgt_pltfrm : NA ms.workload : na ms.date : 01/06/2017 ms.author : owend
---

# <a name="lesson-2-get-data"></a>Leçon 2 : Obtenir des données

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Dans cette leçon, vous utilisez obtenir des données dans la base de données exemple tooconnect toohello AdventureWorksDW2014 SSDT, sélectionnez les données, aperçu et filtrer et ensuite importerez dans votre espace de travail modèle.  
  
L’option Obtenir des données vous permet d’importer des données à partir d’une grande variété de sources : Azure SQL Database, Oracle, Sybase, flux OData, bases de données Teradata, fichiers, entre autres. Les données peuvent également être interrogées à l’aide d’une expression de formule M Power Query.
  
Estimé temps toocomplete cette leçon : **10 minutes**  
  
## <a name="prerequisites"></a>Composants requis  
Cette rubrique fait partie d’un didacticiel de modélisation tabulaire, qui doit être suivi dans l’ordre prévu. Avant d’effectuer les tâches de hello dans cette leçon, vous devez avoir terminé les leçon précédente hello : [leçon 1 : créer un projet de modèle tabulaire](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).  
  
## <a name="create-a-connection"></a>Créer une connexion  
  
#### <a name="toocreate-a-connection-toohello-adventureworksdw2014-database"></a>toocreate une base de données toohello AdventureWorksDW2014 de connexion  
  
1.  Dans l’Explorateur de modèles tabulaires, cliquez avec le bouton droit sur **Sources de données** > **Importer à partir de la source de données**.  
  
    Obtenir des données, qui vous guide tout au long de source de données tooa connexion démarre. Si vous ne voyez pas dans l’Explorateur de modèles tabulaires, **l’Explorateur de solutions**, double-cliquez sur **Model.bim** modèle de hello tooopen dans le Concepteur de hello. 
    
    ![aas-lesson2-getdata](../tutorials/media/aas-lesson2-getdata.png)
  
2.  Dans l’option Obtenir des données, cliquez sur **Base de données** > **Base de données SQL Server** > **Connecter**.  
  
3.  Bonjour **base de données SQL Server** boîte de dialogue, dans **Server**, tapez nom hello du serveur hello où vous avez installé la base de données hello AdventureWorksDW2014, puis cliquez sur **connexion**.  

4.  Lorsque vous y êtes invité informations d’identification de tooenter, vous avez besoin d’informations d’identification de hello toospecify Analysis Services utilise la source de données toohello tooconnect lors de l’importation et le traitement des données. Dans **Mode d’emprunt d’identité**, sélectionnez **Emprunter l’identité du compte**, entrez les informations d’identification, puis cliquez sur **Connecter**. Il est recommandé de qu'utiliser un compte dans lequel le mot de passe hello n’expire jamais.

    ![aas-lesson2-account](../tutorials/media/aas-lesson2-account.png)
  
    > [!NOTE]  
    > À l’aide d’un compte d’utilisateur Windows et un mot de passe fournit la méthode la plus sûre de hello connexion tooa de source de données.
  
5.  Dans le navigateur, sélectionnez hello **AdventureWorksDW2014** de base de données, puis cliquez sur **OK**. Cela crée la base de données toohello hello connexion. 
  
6.  Dans le navigateur, sélectionnez hello case à cocher pour hello les tableaux suivants : **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**,  **DimProductCategory**, **DimProductSubcategory**, et **FactInternetSales**.  

    ![aas-lesson2-select-tables](../tutorials/media/aas-lesson2-select-tables.png)
  
Après que vous avez cliqué sur OK, l’éditeur de requête s’ouvre. Dans la section suivante de hello, vous sélectionnez uniquement hello données tooimport.

  
## <a name="filter-hello-table-data"></a>Filtrer les données de table hello  
Tables dans la base de données exemple hello AdventureWorksDW2014 contiennent des données qui n’est pas nécessaire tooinclude dans votre modèle. Lorsque cela est possible, vous souhaitez toofilter l’espace de mémoire des données inutiles toosave utilisé par le modèle de hello. Filtrer certaines des colonnes hello à partir des tables afin de n'être pas importés dans la base de données hello espace de travail ou base de données model hello après que qu’il a été déployé. 
  
#### <a name="toofilter-hello-table-data-before-importing"></a>données de la table hello toofilter avant l’importation  
  
1.  Dans l’éditeur de requête, sélectionnez hello **DimCustomer** table. Une vue de la table DimCustomer hello datasource de hello (votre base de données exemple AdventureWorksDWQ2014) s’affiche. 
  
2.  Effectuez une sélection multiple (Ctrl + clic) de **SpanishEducation**, **FrenchEducation**, **SpanishOccupation** et **FrenchOccupation**. Cliquez avec le bouton droit, puis cliquez sur **Supprimer les colonnes**. 

    ![aas-lesson2-remove-columns](../tutorials/media/aas-lesson2-remove-columns.png)
  
    Valeurs hello pour ces colonnes ne sont pas pertinentes tooInternet analyse des ventes, n’est pas tooimport besoin de ces colonnes. L’élimination des colonnes inutiles permet de réduire la taille de votre modèle et de le rendre plus efficace.  
  
4.  Filtrer hello restant des tables en supprimant hello suivant des colonnes dans chaque table :  
    
    **DimDate**
    
      |Colonne|  
      |--------|  
      |DateKey|  
      |**SpanishDayNameOfWeek**|  
      |**FrenchDayNameOfWeek**|  
      |**SpanishMonthName**|  
      |**FrenchMonthName**|  
  
    **DimGeography**
  
      |Colonne|  
      |-------------|  
      |**SpanishCountryRegionName**|  
      |**FrenchCountryRegionName**|  
      |**IpAddressLocator**|  
  
    **DimProduct**
  
      |Colonne|  
      |-----------|  
      |**SpanishProductName**|  
      |**FrenchProductName**|  
      |**FrenchDescription**|  
      |**ChineseDescription**|  
      |**ArabicDescription**|  
      |**HebrewDescription**|  
      |**ThaiDescription**|  
      |**GermanDescription**|  
      |**JapaneseDescription**|  
      |**TurkishDescription**|  
  
    **DimProductCategory**
  
      |Colonne|  
      |--------------------|  
      |**SpanishProductCategoryName**|  
      |**FrenchProductCategoryName**|  
  
    **DimProductSubcategory**
  
      |Colonne|  
      |-----------------------|  
      |**SpanishProductSubcategoryName**|  
      |**FrenchProductSubcategoryName**|  
  
    **FactInternetSales**
  
      |Colonne|  
      |------------------|  
      |**OrderDateKey**|  
      |**DueDateKey**|  
      |**ShipDateKey**|   
  
## <a name="Import"></a>Importer les tables de hello sélectionnée et les données de la colonne  
Maintenant que vous avez prévisualisé et filtré les données inutiles, vous pouvez importer reste hello de données hello souhaités. Assistant de Hello importe des données de la table hello avec toutes les relations entre les tables. Nouvelles tables et colonnes sont créés dans le modèle de hello et les données filtrées n’est pas importé.  
  
#### <a name="tooimport-hello-selected-tables-and-column-data"></a>tooimport hello sélectionné les tables et les données de colonne  
  
1.  Passez en revue vos sélections. Si tout semble correct, cliquez sur **Importer**. boîte de dialogue de traitement des données Hello affiche état hello des données importées à partir de votre source de données dans votre base de données de l’espace de travail.
  
    ![aas-lesson2-success](../tutorials/media/aas-lesson2-success.png) 
  
2.  Cliquez sur **Fermer**.  

  
## <a name="save-your-model-project"></a>Enregistrer votre projet de modèle  
Il est important, elles sonttrop enregistrer votre projet de modèle.  
  
#### <a name="toosave-hello-model-project"></a>projet de modèle hello toosave  
  
-   Cliquez sur **Fichier** > **Enregistrer tout**.  
  
## <a name="whats-next"></a>Et ensuite ?
[Leçon 3 : Marquer en tant que Table de dates](../tutorials/aas-lesson-3-mark-as-date-table.md).

  
  
