---
titre : aaa « leçon supplémentaire du didacticiel Azure Analysis Services : les hiérarchies irrégulières | Description de Microsoft Docs » : décrit comment toofix les hiérarchies déséquilibrées dans hello Azure Analysis Services tutorial.
Services : analysis services documentationcenter : '' auteur : minewiskan manager : erikre éditeur : '' balises : ».

MS.AssetId : ms.service : ms.devlang d’analysis services : NA ms.topic : get-started-article ms.tgt_pltfrm : NA ms.workload : na ms.date : 26/05/2017 ms.author : owend
---
# <a name="supplemental-lesson---ragged-hierarchies"></a>Leçon supplémentaire – Hiérarchies déséquilibrées

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Dans cette leçon supplémentaire, vous allez résoudre un problème courant se produisant lors de l’ajout d’un tableau croisé dynamique sur des hiérarchies qui contiennent des valeurs vides (membres) à différents niveaux. Par exemple, une organisation où un cadre a à la fois des responsables de département et des non-cadres comme collaborateurs. Ou bien des hiérarchies géographiques composées des éléments Pays-Région-Ville, où certaines villes n’ont pas d’état ou de région parent, par exemple Washington D.C. ou la Cité du Vatican. Lorsqu’une hiérarchie possède des membres vides, il souvent descend toodifferent ou déséquilibrée, les niveaux.

![aas-lesson-detail-ragged-hierarchies-table](../tutorials/media/aas-lesson-detail-ragged-hierarchies-table.png)

Les modèles tabulaires au niveau de compatibilité hello 1400 possèdent un autre **masquer les membres** propriété pour les hiérarchies. Hello **par défaut** paramètre qu’il n’y aucun membre vide n’importe quel niveau. Hello **masquer les membres vides** paramètre exclut vides à partir de la hiérarchie hello lors de l’ajout tooa tableau croisé dynamique ou un rapport.  
  
Estimé temps toocomplete cette leçon : **20 minutes**  
  
## <a name="prerequisites"></a>Composants requis  
Cette rubrique de leçon supplémentaire fait partie d’un didacticiel de modélisation tabulaire. Avant d’effectuer les tâches de hello dans cette leçon supplémentaire, vous devez avoir terminé toutes les leçons précédentes ou avoir un projet de modèle d’exemple Adventure Works Internet Sales terminé. 

Si vous avez créé le projet de AW Internet Sales hello dans le cadre du didacticiel de hello, votre modèle ne contient pas encore toutes les données ou les hiérarchies irrégulières. toocomplete cette leçon supplémentaire, vous devez toocreate hello problème en ajoutant des tables supplémentaires, créez des relations, les colonnes calculées, une mesure et une hiérarchie d’organisation. Cette partie prend environ 15 minutes. Ensuite, vous obtenez toosolve dans quelques minutes.  

## <a name="add-tables-and-objects"></a>Ajouter des tables et des objets
  
### <a name="tooadd-new-tables-tooyour-model"></a>nouveau modèle de tooyour tables tooadd
  
1.  Dans l’Explorateur de modèles tabulaires, développez **Sources de données**, puis cliquez avec le bouton droit sur votre connexion > **Importer de nouvelles tables**.
  
2.  Dans le navigateur, sélectionnez **DimEmployee** et **FactResellerSales**, puis cliquez sur **OK**.

3.  Dans l’éditeur de requête, cliquez sur **Importer**.

4.  Créer hello [relations](../tutorials/aas-lesson-4-create-relationships.md):

    | Table 1           | Colonne       | Direction du filtre   | Table 2     | Colonne      | Actif |
    |-------------------|--------------|--------------------|-------------|-------------|--------|
    | FactResellerSales | OrderDateKey | Par défaut            | DimDate     | Date        | Oui    |
    | FactResellerSales | DueDate      | Par défaut            | DimDate     | Date        | Non     |
    | FactResellerSales | ShipDateKey  | Par défaut            | DimDate     | Date        | Non     |
    | FactResellerSales | ProductKey   | Par défaut            | DimProduct  | ProductKey  | Oui    |
    | FactResellerSales | EmployeeKey  | Tables tooBoth | DimEmployee | EmployeeKey | Oui    |

5. Bonjour **DimEmployee** table, créer hello [des colonnes calculées](../tutorials/aas-lesson-5-create-calculated-columns.md): 

    **Chemin d’accès** 
    ```
    =PATH([EmployeeKey],[ParentEmployeeKey])
    ```

    **FullName** 
    ```
    =[FirstName] & " " & [MiddleName] & " " & [LastName]
    ```

    **Level1** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,1)) 
    ```

    **Level2** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,2)) 
    ```

    **Level3** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,3)) 
    ```

    **Level4** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,4)) 
    ```

    **Level5** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,5)) 
    ```

6.  Bonjour **DimEmployee** table, créez un [hiérarchie](../tutorials/aas-lesson-9-create-hierarchies.md) nommé **organisation**. Ajouter hello suivant des colonnes dans l’ordre : **Level1**, **Level2**, **Level3**, **Level4**, **Level5**.

7.  Bonjour **FactResellerSales** table, créer hello [mesure](../tutorials/aas-lesson-6-create-measures.md):

    ```
    ResellerTotalSales:=SUM([SalesAmount])
    ```

8.  Utilisez [analyser dans Excel](../tutorials/aas-lesson-12-analyze-in-excel.md) tooopen Excel et de créer automatiquement un tableau croisé dynamique.

9.  Dans **PivotTable Fields**, ajouter hello **organisation** hiérarchie à partir de hello **DimEmployee** table trop**lignes**et hello **ResellerTotalSales** mesure hello **FactResellerSales** table trop**valeurs**.

    ![aas-lesson-detail-ragged-hierarchies-pivottable](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable.png)

    Comme vous pouvez le voir dans le tableau croisé dynamique de hello, hiérarchie de hello affiche les lignes qui sont décalés. Il y a de nombreuses lignes où des membres vides sont affichés.

## <a name="toofix-hello-ragged-hierarchy-by-setting-hello-hide-members-property"></a>hiérarchie irrégulière de toofix hello en définissant les membres de masquer hello propriété

1.  Dans l’**Explorateur de modèles tabulaires**, développez **Tables** > **DimEmployee** > **Hiérarchies** > **Organization**.

2.  Dans **Propriétés** > **Masquer les membres**, sélectionnez **Masquer les membres vides**. 

    ![aas-lesson-detail-ragged-hierarchies-hidemembers](../tutorials/media/aas-lesson-detail-ragged-hierarchies-hidemembers.png)

3.  Dans Excel, actualiser hello tableau croisé dynamique. 

    ![aas-lesson-detail-ragged-hierarchies-pivottable-refresh](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable-refresh.png)

    Voilà qui est beaucoup mieux !

## <a name="see-also"></a>Voir aussi   
[Leçon 9 : Créer des hiérarchies](../tutorials/aas-lesson-9-create-hierarchies.md)  
[Leçon supplémentaire – Sécurité dynamique](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[Leçon supplémentaire – Lignes de détails](../tutorials/aas-supplemental-lesson-detail-rows.md)  