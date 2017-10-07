---
titre : aaa « leçon du didacticiel Azure Analysis Services 12 : analyser dans Excel | Description de Microsoft Docs » : décrit comment toouse analyser dans Excel Bonjour Azure Analysis Services projet du didacticiel. Services : analysis services documentationcenter : '' auteur : minewiskan manager : erikre éditeur : '' balises : ».

MS.AssetId : ms.service : ms.devlang d’analysis services : NA ms.topic : get-started-article ms.tgt_pltfrm : NA ms.workload : na ms.date : 26/05/2017 ms.author : owend
---
# <a name="lesson-12-analyze-in-excel"></a>Leçon 12 : Analyser dans Excel

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Dans cette leçon, vous utilisez hello analyser dans Excel fonctionnalité tooopen Microsoft Excel, créez automatiquement un espace de travail du modèle toohello connexion et ajoutez automatiquement une feuille de calcul de toohello de tableau croisé dynamique. Hello analyser dans la fonctionnalité Excel vise tooprovide une efficacité de hello tootest moyen simple et rapide de votre modèle de conception toodeploying préalable votre modèle. Vous n’exécutez aucune analyse de données dans cette leçon. objectif Hello de cette leçon est toofamiliarize, créez le modèle de hello, avec les outils hello vous pouvez utiliser tootest à la conception du modèle.   
  
toocomplete cette leçon, Excel doit être installée sur hello même ordinateur en tant que SSDT.
  
Estimé temps toocomplete cette leçon : **cinq minutes**  
  
## <a name="prerequisites"></a>Composants requis  
Cette rubrique fait partie d’un didacticiel de modélisation tabulaire, qui doit être suivi dans l’ordre prévu. Avant d’effectuer les tâches de hello dans cette leçon, vous devez avoir terminé les leçon précédente hello : [leçon 11 : créer des rôles](../tutorials/aas-lesson-11-create-roles.md).  
  
## <a name="browse-using-hello-default-and-internet-sales-perspectives"></a>Accédez à l’aide des perspectives de valeur par défaut et Internet Sales hello  
Dans ces premières tâches, vous parcourez votre modèle à l’aide de deux perspective par défaut hello, qui inclut tous les objets de modèle, et également à l’aide de perspective Internet Sales de hello vous précédemment. Hello perspective Internet Sales exclut l’objet de table Customer hello.  
  
#### <a name="toobrowse-by-using-hello-default-perspective"></a>toobrowse à l’aide du point de vue par défaut hello  
  
1.  Cliquez sur hello **modèle** menu > **analyser dans Excel**.  
  
2.  Bonjour **analyser dans Excel** boîte de dialogue, cliquez sur **OK**.  
  
    Excel s’ouvre avec un nouveau classeur. Une connexion de source de données est créée à l’aide du compte d’utilisateur actuel hello et hello perspective par défaut est utilisé toodefine les champs visibles. Un tableau croisé dynamique est automatiquement ajouté toohello la feuille de calcul.  
  
3.  Dans Excel, Bonjour **liste de champs de tableau croisé dynamique**, avis hello **DimDate** et **FactInternetSales** groupes de mesures s’affichent. Hello **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, et **FactInternetSales** tables avec leurs colonnes respectives apparaissent également.  
  
4.  Fermez Excel sans enregistrer le classeur de hello.  
  
#### <a name="toobrowse-by-using-hello-internet-sales-perspective"></a>toobrowse à l’aide du point de vue hello ventes sur Internet  
  
1.  Cliquez sur hello **modèle** menu, puis sur **analyser dans Excel**.  
  
2.  Bonjour **analyser dans Excel** boîte de dialogue, laissez le champ **utilisateur Windows actuel** sélectionné, puis dans hello **Perspective** zone de liste déroulante, sélectionnez **Internet Sales** , puis cliquez sur **OK**. 
    
    ![aas-lesson12-perspective](../tutorials/media/aas-lesson12-perspective.png)
    
3.  Dans Excel, dans **PivotTable Fields**, notez la table DimCustomer de hello est exclu de la liste de champs hello.  
    
    ![aas-lesson12-fields](../tutorials/media/aas-lesson12-fields.png)
    
4.  Fermez Excel sans enregistrer le classeur de hello.  
  
## <a name="browse-by-using-roles"></a>Parcourir les données à l’aide de rôles  
Les rôles sont importants dans n’importe quel modèle tabulaire. Au moins un rôle toowhich utilisateurs sont ajoutés en tant que membres, les utilisateurs ne peuvent pas accéder et analyser les données à l’aide de votre modèle. Hello analyser dans la fonctionnalité Excel offre un moyen pour vous les rôles de hello tootest que vous avez définis.  
  
#### <a name="toobrowse-by-using-hello-sales-manager-user-role"></a>toobrowse à l’aide du rôle d’utilisateur Sales Manager hello  
  
1.  Dans SSDT, cliquez sur hello **modèle** menu, puis sur **analyser dans Excel**.  
  
2.  Dans **spécifiez hello modèle utilisateur de nom ou rôle toouse tooconnect toohello**, sélectionnez **rôle**, puis, dans la zone de liste déroulante hello, sélectionnez **responsable des ventes**, puis cliquez sur  **OK**.  
  
    Excel s’ouvre avec un nouveau classeur. Un tableau croisé dynamique est automatiquement créé. Hello liste de champs de tableau croisé dynamique inclut tous les champs de données hello disponibles dans votre nouveau modèle.  
      
3.  Fermez Excel sans enregistrer le classeur de hello.  
  
## <a name="whats-next"></a>Et ensuite ?
Accédez toohello prochaine leçon : [leçon 13 : déployer](../tutorials/aas-lesson-13-deploy.md).

  
  
  
