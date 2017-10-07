---
titre : aaa « leçon du didacticiel Azure Analysis Services 10 : créer des partitions | Description de Microsoft Docs » : décrit comment toocreate partitions dans le projet du didacticiel hello Azure Analysis Services. Services : analysis services documentationcenter : '' auteur : minewiskan manager : erikre éditeur : '' balises : ».

MS.AssetId : ms.service : ms.devlang d’analysis services : NA ms.topic : get-started-article ms.tgt_pltfrm : NA ms.workload : na ms.date : 26/05/2017 ms.author : owend
---
# <a name="lesson-10-create-partitions"></a>Leçon 10 : Créer des partitions

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Dans cette leçon, vous créer la table FactInternetSales de partitions toodivide hello en parties logiques plus petites qui peuvent être traitée (actualisées) indépendamment d’autres partitions. Par défaut, chaque table que vous incluez dans votre modèle a une partition, qui inclut les colonnes et lignes de la table du hello. Pour la table FactInternetSales de hello, nous souhaitons les données de salutation toodivide par année ; une seule partition pour chacune des cinq années de la table hello. Chaque partition peut ensuite être traitée indépendamment. toolearn, voir [Partitions](https://docs.microsoft.com/sql/analysis-services/tabular-models/partitions-ssas-tabular). 
  
Estimé temps toocomplete cette leçon : **15 minutes**  
  
## <a name="prerequisites"></a>Composants requis  
Cette rubrique fait partie d’un didacticiel de modélisation tabulaire, qui doit être suivi dans l’ordre prévu. Avant d’effectuer les tâches de hello dans cette leçon, vous devez avoir terminé les leçon précédente hello : [leçon 9 : créer des hiérarchies](../tutorials/aas-lesson-9-create-hierarchies.md).  
  
## <a name="create-partitions"></a>Créer des partitions  
  
#### <a name="toocreate-partitions-in-hello-factinternetsales-table"></a>partitions toocreate dans la table FactInternetSales de hello  
  
1.  Dans l’Explorateur de modèles tabulaires, développez **Tables**, puis cliquez avec le bouton droit sur **FactInternetSales** > **Partitions**.  
  
2.  Dans le Gestionnaire de Partition, cliquez sur **copie**, puis modifiez le nom de hello trop**FactInternetSales2010**.
  
    Pour que vous puissiez hello partition tooinclude uniquement les lignes dans une période donnée, pour l’année hello 2010, vous devez modifier l’expression de requête hello.
  
4.  Cliquez sur **conception** tooopen éditeur de requête, puis cliquez sur hello **FactInternetSales2010** requête.

5.  Dans l’aperçu, cliquez sur hello bas Bonjour **OrderDate** en-tête de colonne, puis cliquez sur **filtres de Date/heure** > **entre**.

    ![aas-lesson10-query-editor](../tutorials/media/aas-lesson10-query-editor.png)

6.  Dans la boîte de dialogue Filtrer les lignes hello dans **afficher les lignes où : OrderDate**, laissez **est postérieur ou égal à**, puis dans le champ de date hello, entrez **1/1/2010**. Laissez hello **et** opérateur sélectionné, puis sélectionnez **avant**, puis, dans le champ de date hello, entrez **1/1/2011**, puis cliquez sur **OK**.

    ![aas-lesson10-filter-rows](../tutorials/media/aas-lesson10-filter-rows.png)
    
    Dans l’éditeur de requête, sous ÉTAPES APPLIQUÉES, vous voyez une autre étape nommée Lignes filtrées. Ce filtre est tooselect les dates de commande uniquement à partir de 2010.

8.  Cliquez sur **Importer**.

    Dans le Gestionnaire de Partition, notez que la requête hello expression maintenant comporte une clause de filtrer les lignes supplémentaire.

    ![aas-lesson10-query](../tutorials/media/aas-lesson10-query.png)
  
    Cette instruction spécifie que cette partition doit inclure uniquement les données hello dans les lignes où OrderDate de hello est Bonjour année 2010 comme spécifié dans la clause de lignes filtrées hello.  
  
  
#### <a name="toocreate-a-partition-for-hello-2011-year"></a>toocreate une partition pour hello année 2011  
  
1.  Dans la liste des partitions hello, cliquez sur hello **FactInternetSales2010** de partition que vous avez créé, puis cliquez sur **copie**.  Modifier le nom de la partition hello trop**FactInternetSales2011**. 

    Vous n’avez pas besoin de toouse toocreate de l’éditeur de requête une nouvelle clause de lignes filtrées. Étant donné que vous avez créé une copie de la requête de hello pour 2010, vous devez toodo est apporter une légère modification dans la requête de hello pour 2011.
  
2.  Dans **Expression de requête**, dans l’ordre pour ce tooinclude partition uniquement les lignes pour hello année 2011, la remplacer les années hello dans la clause de filtrer les lignes hello avec **2011** et **2012**, respectivement, telles que :  
  
    ```  
    let
        Source = #"SQL/localhost;AdventureWorksDW2014",
        dbo_FactInternetSales = Source{[Schema="dbo",Item="FactInternetSales"]}[Data],
        #"Removed Columns" = Table.RemoveColumns(dbo_FactInternetSales,{"OrderDateKey", "DueDateKey", "ShipDateKey"}),
        #"Filtered Rows" = Table.SelectRows(#"Removed Columns", each [OrderDate] >= #datetime(2011, 1, 1, 0, 0, 0) and [OrderDate] < #datetime(2012, 1, 1, 0, 0, 0))
    in
        #"Filtered Rows"
   
    ```  
  
#### <a name="toocreate-partitions-for-2012-2013-and-2014"></a>partitions toocreate pour 2012, 2013 et 2014.  
  
- Suivez les étapes précédentes hello, création de partitions pour 2014, la modification des années hello dans hello filtré lignes clause tooinclude uniquement les lignes pour l’année 2012 et 2013. 
  

## <a name="delete-hello-factinternetsales-partition"></a>Supprimer la partition de FactInternetSales hello
Maintenant que vous avez des partitions pour chaque année, vous pouvez supprimer la partition de FactInternetSales hello ; empêche le chevauchement lors du choix de traiter toutes les lors du traitement de partitions.

#### <a name="toodelete-hello-factinternetsales-partition"></a>toodelete hello FactInternetSales partition
-  Cliquez sur la partition FactInternetSales hello, puis cliquez sur **supprimer**.



## <a name="process-partitions"></a>Traiter les partitions  
Dans le Gestionnaire de Partition, notez hello **traités dernière** colonne pour chacune des partitions hello vous créées montre ces partitions n’ont jamais été traitées. Lorsque vous créez des partitions, vous devez exécuter un traiter les Partitions ou les données de traiter la Table opération toorefresh hello dans ces partitions.  
  
#### <a name="tooprocess-hello-factinternetsales-partitions"></a>partitions de FactInternetSales tooprocess hello  
  
1.  Cliquez sur **OK** tooclose le Gestionnaire de Partition.  
  
2.  Cliquez sur hello **FactInternetSales** , puis cliquez sur hello **modèle** menu > **processus** > **traiter les Partitions**.  
  
3.  Dans la boîte de dialogue traiter les Partitions hello, vérifiez **Mode** est défini trop**traiter par défaut**.  
  
4.  Sélectionnez la case à cocher hello Bonjour **processus** colonne pour chacune des hello cinq partitions que vous avez créé, puis cliquez sur **OK**.  

    ![aas-lesson10-process-partitions](../tutorials/media/aas-lesson10-process-partitions.png)
  
    Si vous êtes invité à entrer des informations d’identification d’emprunt d’identité, entrez le nom d’utilisateur Windows hello et le mot de passe spécifié dans la leçon 2.  
  
    Hello **le traitement des données** boîte de dialogue apparaît et affiche les détails du processus pour chaque partition. Notez que le nombre de lignes transférées est différent pour chaque partition. Chaque partition contient uniquement les lignes pour l’année hello spécifiée dans la clause WHERE dans l’instruction SQL de hello de hello. Lorsque le traitement est terminé, continuez et fermer la boîte de dialogue hello le traitement des données.  
  
    ![aas-lesson10-process-complete](../tutorials/media/aas-lesson10-process-complete.png)
  
 ## <a name="whats-next"></a>Et ensuite ?
Accédez toohello prochaine leçon : [leçon 11 : créer des rôles](../tutorials/aas-lesson-11-create-roles.md). 
