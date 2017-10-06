---
titre : aaa « leçon du didacticiel Azure Analysis Services 11 : créer des rôles | Description de Microsoft Docs » : décrit comment les rôles toocreate dans hello projet du didacticiel Azure Analysis Services. Services : analysis services documentationcenter : '' auteur : minewiskan manager : erikre éditeur : '' balises : ».

MS.AssetId : ms.service : ms.devlang d’analysis services : NA ms.topic : get-started-article ms.tgt_pltfrm : NA ms.workload : na ms.date : 26/05/2017 ms.author : owend
---
# <a name="lesson-11-create-roles"></a>Leçon 11 : Créer des rôles

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Dans cette leçon, vous allez créer des rôles. Les rôles fournissent la sécurité de données et l’objet de base de données de modèle en limitant l’accès tooonly les utilisateurs qui sont membres du rôle. Chaque rôle est défini avec une autorisation unique : aucune autorisation, autorisation de lecture, autorisation de lecture et de traitement, autorisation de traitement ou autorisation d’administrateur. Les rôles peuvent être définis lors de la création des modèles à l’aide du Gestionnaire de rôles. Une fois un modèle déployé, vous pouvez gérer des rôles à l’aide de SQL Server Management Studio (SSMS). toolearn, voir [rôles](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular).
  
> [!NOTE]  
> Création de rôles est toocomplete n’est pas nécessaire de ce didacticiel. Par défaut, compte hello que vous êtes actuellement connecté dispose des privilèges d’administrateur sur le modèle de hello. Toutefois, pour les autres utilisateurs toobrowse de votre organisation à l’aide d’un client de création de rapports, vous devez créer au moins un rôle avec la lecture des autorisations et ajouter ces utilisateurs en tant que membres.  
  
Vous devez créer trois rôles :  
  
-   **Responsable des ventes** – ce rôle peut inclure des utilisateurs de votre organisation pour lequel vous souhaitez que les données et les objets de modèle toohave tooall de l’autorisation en lecture.  
  
-   **Analyste des ventes aux États-Unis** – ce rôle peut inclure des utilisateurs de votre organisation pour lequel vous ne souhaitez que les données en mesure de toobrowse toobe liés toosales Bonjour États-Unis. Pour ce rôle, vous utilisez un toodefine de formule DAX un *filtre de lignes*, qui limite les membres toobrowse uniquement les données hello États-Unis.  
  
-   **Administrateur** – ce rôle peut inclure des utilisateurs pour lesquels vous souhaitez toohave les autorisations d’administrateur, ce qui permet un accès illimité et autorisations tooperform des tâches d’administration sur la base de données model hello.  
  
Étant donné que les comptes d’utilisateur et de groupe Windows dans votre organisation sont uniques, vous pouvez ajouter des comptes à partir de toomembers de votre organisation. Toutefois, pour ce didacticiel, vous pouvez également laisser les membres hello vide. Test d’effet hello de chaque rôle plus tard dans la leçon 12 : analyser dans Excel.  
  
Estimé temps toocomplete cette leçon : **15 minutes**  
  
## <a name="prerequisites"></a>Composants requis  
Cette rubrique fait partie d’un didacticiel de modélisation tabulaire, qui doit être suivi dans l’ordre prévu. Avant d’effectuer les tâches de hello dans cette leçon, vous devez avoir terminé les leçon précédente hello : [leçon 10 : créer des partitions](../tutorials/aas-lesson-10-create-partitions.md).  
  
## <a name="create-roles"></a>Créer des rôles  
  
#### <a name="toocreate-a-sales-manager-user-role"></a>toocreate un rôle d’utilisateur Sales Manager  
  
1.  Dans l’Explorateur de modèle tabulaire, cliquez avec le bouton droit sur **Rôles** > **Rôles**.  
  
2.  Dans le Gestionnaire de rôles, cliquez sur **Nouveau**.  
  
3.  Cliquez sur Nouveau rôle de hello, puis dans hello **nom** colonne, renommez le rôle de hello trop**responsable des ventes**.  
  
4.  Bonjour **autorisations** colonne, cliquez sur la liste déroulante hello et sélectionnez hello **en lecture** autorisation. 

    ![aas-lesson11-new-role](../tutorials/media/aas-lesson11-new-role.png) 
  
5.  Facultatif : Cliquez sur hello **membres** onglet, puis cliquez sur **ajouter**. Bonjour **sélectionner des utilisateurs ou groupes** boîte de dialogue, entrez hello utilisateurs ou groupes Windows à partir de votre organisation, vous souhaitez tooinclude dans le rôle de hello.  
  
#### <a name="toocreate-a-sales-analyst-us-user-role"></a>toocreate un rôle d’utilisateur Sales Analyst US  
  
1.  Dans le Gestionnaire de rôles, cliquez sur **Nouveau**.    
  
2.  Renommer le rôle de hello trop**Sales Analyst US**.  
  
3.  Attribuez à ce rôle l’autorisation **Lecture**.  
  
4.  Cliquez sur hello onglet Filtres de lignes, puis pour hello **DimGeography** table uniquement, dans la colonne de filtre DAX hello, hello type formule suivante :  
  
    ```Administrator
    =DimGeography[CountryRegionCode] = "US" 
    ```
    
    Formule de filtre de lignes d’une valeur booléenne (TRUE/FALSE) de tooa doit être résolue. Avec cette formule, vous spécifiez que seules les lignes avec hello valeur Country Region Code « US » sont visibles toohello utilisateur.  
    ![aas-lesson11-role-filter](../tutorials/media/aas-lesson11-role-filter.png) 
  
6.  Facultatif : Cliquez sur hello **membres** onglet, puis cliquez sur **ajouter**. Bonjour **sélectionner des utilisateurs ou groupes** boîte de dialogue, entrez hello utilisateurs ou groupes Windows à partir de votre organisation, vous souhaitez tooinclude dans le rôle de hello.  
  
#### <a name="toocreate-an-administrator-user-role"></a>toocreate un rôle d’utilisateur administrateur  
  
1.  Cliquez sur **Nouveau**.  
  
2.  Renommer le rôle de hello trop**administrateur**.  
  
3.  Attribuez à ce rôle l’autorisation **Administrateur**.  
  
4.  Facultatif : Cliquez sur hello **membres** onglet, puis cliquez sur **ajouter**. Bonjour **sélectionner des utilisateurs ou groupes** boîte de dialogue, entrez hello utilisateurs ou groupes Windows à partir de votre organisation, vous souhaitez tooinclude dans le rôle de hello. 
  
  
## <a name="whats-next"></a>Et ensuite ?
[Leçon 12 : Analyser dans Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).

  
  
