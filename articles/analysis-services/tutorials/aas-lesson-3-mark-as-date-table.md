---
titre : aaa « leçon du didacticiel Azure Analysis Services 3 : marquer en tant que Table de dates | Description de Microsoft Docs » : décrit comment toomark une date de la table dans le projet du didacticiel hello Azure Analysis Services. Services : analysis services documentationcenter : '' auteur : minewiskan manager : erikre éditeur : '' balises : ».

MS.AssetId : ms.service : ms.devlang d’analysis services : NA ms.topic : get-started-article ms.tgt_pltfrm : NA ms.workload : na ms.date : 01/06/2017 ms.author : owend
---
# <a name="lesson-3-mark-as-date-table"></a>Leçon 3 : Marquer en tant que Table de dates

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Dans Leçon 2 : Obtenir les données, vous avez importé une table de dimension nommée DimDate. Dans votre modèle, cette table se nomme DimDate. Toutefois, elle peut également être appelée *Table de dates*, car elle contient des données de date et d’heure.  
  
Chaque fois que vous utilisez les fonctions Time Intelligence DAX (comme lorsque vous allez créer des mesures), vous devez spécifier des propriétés qui correspondent à une *table de dates* et à sa *colonne de date* à identificateur unique.
  
Dans cette leçon, vous marquez la table DimDate hello hello *table de dates* et la colonne de Date de hello (dans la table de dates hello) comme hello *colonne de Date* (identificateur unique).  

Avant de vous marquez la colonne de table et la date de la date hello, il est un toodo de temps un peu de ménage toomake votre toounderstand plus facile de modèle. Notez que, dans la table DimDate de hello, une colonne nommée **FullDateAlternateKey**. Cette colonne contient une ligne pour chaque jour de l’année civile incluse dans la table de hello. Cette colonne est très souvent utilisée dans les formules de mesure et dans les rapports. Cependant, FullDateAlternateKey n’est pas vraiment un bon identificateur pour cette colonne. Renommez-le trop**Date**, rendant tooidentify plus facile et les inclure dans les formules. Chaque fois que possible, il s’agit d’une bonne idée toorename objets tels que tables et colonnes toomake les tooidentify plus facile dans SSDT et les applications telles que Power BI et Excel de création de rapports. 
  
Estimé temps toocomplete cette leçon : **trois minutes**  
  
## <a name="prerequisites"></a>Composants requis  
Cette rubrique fait partie d’un didacticiel de modélisation tabulaire, qui doit être suivi dans l’ordre prévu. Avant d’effectuer les tâches de hello dans cette leçon, vous devez avoir terminé les leçon précédente hello : [leçon 2 : obtenir des données](../tutorials/aas-lesson-2-get-data.md). 

### <a name="toorename-hello-fulldatealternatekey-column"></a>colonne de toorename hello FullDateAlternateKey

1.  Dans le Concepteur de modèle hello, cliquez sur hello **DimDate** table.

2.  Double-cliquez sur en-tête hello pour hello **FullDateAlternateKey** colonne, puis renommez-le trop**Date**.

  
### <a name="tooset-mark-as-date-table"></a>tooset marquer en tant que Table de dates  
  
1.  Sélectionnez hello **Date** colonne, puis dans hello **propriétés** fenêtre, sous **Type de données**, assurez-vous que **Date** est sélectionné.  
  
2.  Cliquez sur hello **Table** menu, puis cliquez sur **Date**, puis cliquez sur **marquer en tant que Table de dates**.  
  
3.  Bonjour **marquer en tant que Table de dates** la boîte de dialogue hello **Date** zone de liste, sélectionnez hello **Date** colonne comme identificateur unique de hello. Elle est généralement sélectionnée par défaut. Cliquez sur **OK**. 

    ![aas-lesson3-date-table](../tutorials/media/aas-lesson3-date-table.png)
  

## <a name="whats-next"></a>Et ensuite ?
[Leçon 4 : Créer des relations](../tutorials/aas-lesson-4-create-relationships.md).
  
