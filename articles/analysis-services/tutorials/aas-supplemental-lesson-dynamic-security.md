---
titre : aaa « leçon Azure Analysis Services supplémentaire du didacticiel : sécurité dynamique | Description de Microsoft Docs » : décrit comment toouse la sécurité dynamique à l’aide de ligne de filtre en hello Azure Analysis Services tutorial.
Services : analysis services documentationcenter : '' auteur : minewiskan manager : erikre éditeur : '' balises : ».

MS.AssetId : ms.service : ms.devlang d’analysis services : NA ms.topic : get-started-article ms.tgt_pltfrm : NA ms.workload : na ms.date : 26/05/2017 ms.author : owend
---
# <a name="supplemental-lesson---dynamic-security"></a>Leçon supplémentaire – Sécurité dynamique

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Dans cette leçon supplémentaire, vous allez créer un rôle supplémentaire qui implémente la sécurité dynamique. Sécurité dynamique offre une sécurité au niveau des lignes en fonction de hello name ou login id de hello utilisateur actuellement connecté. 
  
tooimplement la sécurité dynamique, vous ajoutez un modèle de tooyour table contenant les noms d’utilisateur hello des utilisateurs qui peuvent se connecter toohello modèle et parcourir les données et les objets de modèle. modèle Hello que vous créez à l’aide de ce didacticiel est dans le contexte de hello Adventure Works ; Toutefois, toocomplete cette leçon, vous devez ajouter une table qui contient les utilisateurs de votre propre domaine. Vous n’avez pas besoin de mots de passe hello hello les noms d’utilisateurs qui sont ajoutés. toocreate une table EmployeeSecurity, avec un petit groupe d’utilisateurs de votre propre domaine, vous utilisez la fonctionnalité Coller hello coller des données sur les employés à partir d’une feuille de calcul Excel. Dans un scénario réel, table hello contenant les noms d’utilisateur est en général pas une table à partir d’une base de données en tant que source de données. par exemple, une table DimEmployee réelle.  
  
tooimplement la sécurité dynamique, vous utilisez deux fonctions DAX : [nom d’utilisateur, fonction (DAX)](http://msdn.microsoft.com/22dddc4b-1648-4c89-8c93-f1151162b93f) et [LOOKUPVALUE, fonction (DAX)](http://msdn.microsoft.com/73a51c4d-131c-4c33-a139-b1342d10caab). Ces fonctions, appliquées dans une formule de filtre de lignes, sont définies dans un nouveau rôle. À l’aide de la fonction LOOKUPVALUE hello, formule de hello spécifie une valeur à partir de la table de EmployeeSecurity hello. formule de Hello transmet ensuite que fonction value toohello nom d’utilisateur, qui spécifie le nom d’utilisateur hello d’utilisateur hello connecté appartienne toothis rôle. Hello utilisateur peut ensuite parcourir uniquement les données spécifiées par les filtres de lignes du rôle hello. Dans ce scénario, vous spécifiez que les employés peuvent parcourir uniquement les données de ventes Internet pour les secteurs de vente hello dans lequel ils sont membres.  
  
Les tâches qui sont uniques toothis scénario de modèle tabulaire Adventure Works, mais sont appliquent pas nécessairement la réalité tooa sont identifiées comme telles. Chaque tâche inclut des informations supplémentaires décrivant l’objectif de hello de tâche hello.  
  
Estimé temps toocomplete cette leçon : **30 minutes**  
  
## <a name="prerequisites"></a>Composants requis  
Cette rubrique de leçon supplémentaire fait partie d’un didacticiel de modélisation tabulaire, qui doit être suivi dans l’ordre prévu. Avant d’effectuer les tâches de hello dans cette leçon supplémentaire, vous devez avoir terminé toutes les leçons précédentes.  
  
## <a name="add-hello-dimsalesterritory-table-toohello-aw-internet-sales-tabular-model-project"></a>Ajouter hello DimSalesTerritory table toohello le projet de modèle tabulaire AW Internet Sales  
tooimplement sécurité dynamique pour ce scénario Adventure Works, vous devez ajouter le modèle de tooyour deux tables supplémentaires. Hello première table que vous ajoutez est DimSalesTerritory (comme le secteur de vente) à partir de hello la même base de données AdventureWorksDW. Vous appliquez ultérieurement une table SalesTerritory toohello filtre ligne qui définit les données particulier hello hello l’utilisateur connecté peut parcourir.  
  
#### <a name="tooadd-hello-dimsalesterritory-table"></a>table de DimSalesTerritory tooadd hello  
  
1.  Dans l’Explorateur de modèles tabulaires > **Sources de données**, cliquez avec le bouton droit sur votre connexion, puis cliquez sur **Importer de nouvelles tables**.  

    Si la boîte de dialogue informations d’identification d’emprunt d’identité hello s’affiche, tapez les informations d’identification d’emprunt d’identité de hello vous avez utilisé dans la leçon 2 : ajouter des données.
  
2.  Dans le navigateur, sélectionnez hello **DimSalesTerritory** de table, puis cliquez sur **OK**.    
  
3.  Dans l’éditeur de requête, cliquez sur hello **DimSalesTerritory** de requête, puis supprimez **SalesTerritoryAlternateKey** colonne.  
  
7.  Cliquez sur **Importer**.  
  
    Hello nouvelle table est ajoutée toohello espace de travail modèle. Objets et données de table de DimSalesTerritory source hello sont ensuite importées dans votre modèle tabulaire AW Internet Sales.  
  
9. Une fois la table de hello a été importé avec succès, cliquez sur **fermer**.  

## <a name="add-a-table-with-user-name-data"></a>Ajouter une table avec des données de noms d’utilisateur  
table DimEmployee de Hello dans la base de données exemple hello AdventureWorksDW contient les utilisateurs de domaine de AdventureWorks hello. Ces noms d’utilisateur n’existent pas dans votre propre environnement. Vous devez donc créer dans votre modèle une table qui contient un petit échantillon (au moins trois) d’utilisateurs réels de votre organisation. Puis, vous ajoutez ces utilisateurs en tant que rôle de nouveaux membres toohello. Vous n’avez pas besoin des mots de passe hello hello exemple les noms d’utilisateurs, mais vous avez besoin des noms d’utilisateur Windows réels de votre propre domaine.  
  
#### <a name="tooadd-an-employeesecurity-table"></a>tooadd une table EmployeeSecurity  
  
1.  Ouvrez Microsoft Excel, ce qui crée une feuille de calcul.  
  
2.  Hello tableau, y compris la ligne d’en-tête hello, de copier et coller ensuite dans la feuille de calcul hello.  

    ```
      |EmployeeId|SalesTerritoryId|FirstName|LastName|LoginId|  
      |---------------|----------------------|--------------|-------------|------------|  
      |1|2|<user first name>|<user last name>|\<domain\username>|  
      |1|3|<user first name>|<user last name>|\<domain\username>|  
      |2|4|<user first name>|<user last name>|\<domain\username>|  
      |3|5|<user first name>|<user last name>|\<domain\username>|  
    ```

3.  Remplacez domaine\nom d’utilisateur, nom et prénom hello hello de noms et ID de connexion de trois utilisateurs de votre organisation. Placez hello même utilisateur sur hello deux premières lignes, pour 1 EmployeeId, affichant cet utilisateur appartient toomore à un secteur de vente. Renseignez hello EmployeeId et SalesTerritoryId comme ils le sont.  
  
4.  Enregistrez la feuille de calcul hello en tant que **SampleEmployee**.  
  
5.  Dans la feuille de calcul hello, sélectionner toutes les cellules de hello avec les données d’employé, y compris les en-têtes de hello, puis cliquez sur les données de salutation sélectionnée, puis cliquez sur **copie**.  
  
6.  Dans SSDT, cliquez sur hello **modifier** menu, puis sur **coller**.  
  
    Si coller est grisée, cliquez sur n’importe quelle colonne dans une table dans la fenêtre du Concepteur de modèles hello et recommencez l’opération.  
  
7.  Bonjour **Aperçu avant collage** boîte de dialogue **nom de la Table**, type **EmployeeSecurity**.  
  
8.  Dans **toobe données collée**, vérifiez que les données de salutation incluent toutes les données d’utilisateur hello et en-têtes à partir de la feuille de calcul SampleEmployee hello.  
  
9. Vérifiez que la case **Utiliser la première ligne comme en-têtes de colonne** est cochée, puis cliquez sur **OK**.  
  
    Une nouvelle table nommée EmployeeSecurity avec les données employé copiées à partir de la feuille de calcul SampleEmployee hello est créée.  
  
## <a name="create-relationships-between-factinternetsales-dimgeography-and-dimsalesterritory-table"></a>Créer des relations entre les tables FactInternetSales, DimGeography et DimSalesTerritory  
toutes les tables Hello FactInternetSales, DimGeography et DimSalesTerritory contiennent une colonne commune, SalesTerritoryId. Hello SalesTerritoryId colonne hello DimSalesTerritory table contient des valeurs avec un Id différent pour chaque secteur de vente.  
  
#### <a name="toocreate-relationships-between-hello-factinternetsales-dimgeography-and-hello-dimsalesterritory-table"></a>relations toocreate entre hello FactInternetSales DimGeography et la table DimSalesTerritory de hello  
  
1.  Dans la vue de diagramme, Bonjour **DimGeography** table, cliquez et maintenez la sélection hello **SalesTerritoryId** colonne, puis faites glisser hello curseur toohello **SalesTerritoryId** colonne Bonjour **DimSalesTerritory** table et relâchez.  
  
2.  Bonjour **FactInternetSales** table, cliquez et maintenez la sélection hello **SalesTerritoryId** colonne, puis faites glisser hello curseur toohello **SalesTerritoryId** colonne Bonjour  **DimSalesTerritory** de table et relâchez.  
  
    Hello d’avis propriété Active pour cette relation est False, ce qui signifie qu’il est inactif. table de FactInternetSales Hello a déjà une autre relation active.  
  
## <a name="hide-hello-employeesecurity-table-from-client-applications"></a>Masquer hello EmployeeSecurity Table à partir d’applications clientes  
Dans cette tâche, vous masquez la table de EmployeeSecurity hello, évitant qu’elles s’affichent dans la liste de champs d’une application cliente. N’oubliez pas que le fait de masquer une table ne garantit pas sa sécurité. Les utilisateurs peuvent toujours interroger les données de la table EmployeeSecurity s’ils savent comment procéder. toosecure hello des données de la table EmployeeSecurity, empêchant les utilisateurs d’être en mesure de tooquery un de ses données, vous appliquez un filtre dans une tâche ultérieure.  
  
#### <a name="toohide-hello-employeesecurity-table-from-client-applications"></a>table de EmployeeSecurity hello toohide des applications clientes  
  
-   Dans le Concepteur de modèle hello, dans la vue de diagramme, cliquez sur hello **employé** en-tête de la table, puis cliquez sur **masquer dans les outils clients**.  
  
## <a name="create-a-sales-employees-by-territory-user-role"></a>Créer un rôle d’utilisateur Sales Employees by Territory (Représentants commerciaux par secteur)  
Dans cette tâche, vous allez créer un rôle d’utilisateur. Ce rôle inclut un filtre de lignes définissant les lignes de la table DimSalesTerritory de hello sont toousers visible. Hello filtre est ensuite appliqué dans une relation de hello un-à-plusieurs sens tooall autres tables connexe tooDimSalesTerritory. Un filtre qui sécurise hello totalité EmployeeSecurity de la table d’être interrogée par tout utilisateur qui est membre du rôle de hello s’appliquent également.  
  
> [!NOTE]  
> Hello vendeurs par rôle Territory que vous créez dans cette leçon restreint toobrowse (ou requête) uniquement les données des membres pour hello toowhich de secteur de vente qu'auquel ils appartiennent. Si vous ajoutez un utilisateur comme un membre de toohello Sales Employees par rôle de territoire existe également comme un membre d’un rôle créé dans [leçon 11 : créer des rôles](../tutorials/aas-lesson-11-create-roles.md), vous obtenez une combinaison d’autorisations. Lorsqu’un utilisateur est membre de plusieurs rôles, les autorisations hello et les filtres de lignes définies pour chaque rôle se cumulent. Autrement dit, les utilisateurs hello a des autorisations supérieures de hello déterminées par la combinaison de hello de rôles.  
  
#### <a name="toocreate-a-sales-employees-by-territory-user-role"></a>toocreate un Sales Employees par rôle d’utilisateur de secteur de vente  
  
1.  Dans SSDT, cliquez sur hello **modèle** menu, puis sur **rôles**.  
  
2.  Dans le **Gestionnaire de rôles**, cliquez sur **Nouveau**.  
  
    Un nouveau rôle avec hello aucune autorisation est ajoutée toohello liste.  
  
3.  Cliquez sur Nouveau rôle de hello, puis dans hello **nom** colonne, renommez le rôle de hello trop**Sales Employees by Territory**.  
  
4.  Bonjour **autorisations** colonne, cliquez sur la liste déroulante hello et sélectionnez hello **en lecture** autorisation.  
  
5.  Cliquez sur hello **membres** onglet, puis cliquez sur **ajouter**.  
  
6.  Bonjour **sélectionner utilisateur ou groupe** boîte de dialogue **des objets hello nommé tooselect**, type hello premier exemple nom d’utilisateur utilisé lors de la création de table de EmployeeSecurity hello. Cliquez sur **vérifier les noms** nom d’utilisateur tooverify hello est valide, puis cliquez sur **Ok**.  
  
    Répétez cette étape, en ajoutant hello autres exemples de noms d’utilisateur que vous avez utilisé lors de la création de table de EmployeeSecurity hello.  
  
7.  Cliquez sur hello **les filtres de lignes** onglet.  
  
8.  Pourquoi **EmployeeSecurity** table, Bonjour **filtre DAX** colonne, hello type formule suivante :  
  
    ```
      =FALSE()  
    ```
  
    Cette formule indique que toutes les colonnes résolvent toohello condition booléenne false. Aucune colonne de table de EmployeeSecurity hello ne peut être interrogées par un membre de hello Sales Employees par rôle d’utilisateur de secteur de vente.  
  
9. Pourquoi **DimSalesTerritory** table, hello type formule suivante :  

    ```  
    ='Sales Territory'[Sales Territory Id]=LOOKUPVALUE('Employee Security'[Sales Territory Id], 
      'Employee Security'[Login Id], USERNAME(), 
      'Employee Security'[Sales Territory Id], 
      'Sales Territory'[Sales Territory Id]) 
    ```
  
    Dans cette formule, hello la fonction LOOKUPVALUE retourne toutes les valeurs de colonne de DimEmployeeSecurity [SalesTerritoryId] hello, où hello EmployeeSecurity [LoginId] est hello même comme hello actuel ouvert une session sur le nom d’utilisateur Windows et [[[EmployeeSecurity SalesTerritoryId] est hello identique hello DimSalesTerritory [SalesTerritoryId].  
  
    Hello jeu d’ID de secteur de vente retournées par LOOKUPVALUE est ensuite utilisé toorestrict hello lignes affichées dans la table DimSalesTerritory de hello. Seules les lignes où hello SalesTerritoryID pour la ligne de hello est dans le jeu de hello d’ID retournée par la fonction LOOKUPVALUE hello sont affichés.  
  
10. Dans le Gestionnaire de rôles, cliquez sur **OK**.  
  
## <a name="test-hello-sales-employees-by-territory-user-role"></a>Hello Sales Employees by Territory rôle d’utilisateur de test  
Dans cette tâche, vous utilisez hello analyser dans la fonctionnalité Excel dans SSDT tootest hello l’efficacité de hello Sales Employees par rôle d’utilisateur de secteur de vente. Vous spécifiez l’une des noms d’utilisateur hello, vous avez ajouté toohello EmployeeSecurity table et en tant que membre du rôle de hello. Ce nom d’utilisateur est ensuite utilisé en tant que nom d’utilisateur effectif hello dans connexion hello créée entre Excel et hello le modèle.  
  
#### <a name="tootest-hello-sales-employees-by-territory-user-role"></a>tootest hello Sales Employees par rôle d’utilisateur de secteur de vente  
  
1.  Dans SSDT, cliquez sur hello **modèle** menu, puis sur **analyser dans Excel**.  
  
2.  Bonjour **analyser dans Excel** boîte de dialogue **spécifiez hello modèle utilisateur de nom ou rôle toouse tooconnect toohello**, sélectionnez **autre utilisateur Windows**, puis cliquez sur **Parcourir**.  
  
3.  Bonjour **sélectionner utilisateur ou groupe** boîte de dialogue **entrez hello objet nom tooselect**, tapez un nom d’utilisateur que vous avez inclus dans la table de EmployeeSecurity hello, puis cliquez sur **vérifier les noms**.  
  
4.  Cliquez sur **Ok** tooclose hello **sélectionner utilisateur ou groupe** boîte de dialogue, puis cliquez sur **Ok** tooclose hello **analyser dans Excel** boîte de dialogue.  
  
    Excel s’ouvre avec un nouveau classeur. Un tableau croisé dynamique est automatiquement créé. Hello liste PivotTable Fields inclut la plupart des champs de données hello disponibles dans votre nouveau modèle.  
  
    Table de EmployeeSecurity avis hello n’est pas visible dans hello liste PivotTable Fields. En effet, vous avez masqué cette table dans les outils clients lors d’une tâche précédente.  
  
5.  Bonjour **champs** liste dans **∑ Internet Sales** (mesures), sélectionnez hello **InternetTotalSales** mesure. mesure de Hello est entré dans hello **valeurs** champs.  
  
6.  Sélectionnez hello **SalesTerritoryId** colonne hello **DimSalesTerritory** table. colonne de Hello est entré dans hello **étiquettes de ligne** champs.  
  
    Internet Notez les chiffres des ventes s’affichent uniquement pour hello une région toowhich hello efficace nom d’utilisateur utilisé appartient. Si vous sélectionnez une autre colonne, comme ville à partir de la table de DimGeography hello comme champ d’étiquette de ligne, les villes uniquement dans l’utilisateur en vigueur hello secteur de vente toowhich hello appartient sont affichées.  
  
    Cet utilisateur ne peut pas parcourir ou interroger les données des ventes Internet pour les secteurs autres que hello une qu'auquel ils appartiennent. Cette restriction est parce que le filtre de lignes défini pour la table DimSalesTerritory de hello, Bonjour vendeurs par rôle d’utilisateur territoire, hello sécurise les données pour toutes les données liées tooother des secteurs de vente.  
  
## <a name="see-also"></a>Voir aussi  
[USERNAME, fonction (DAX)](https://msdn.microsoft.com/library/hh230954.aspx)  
[LOOKUPVALUE, fonction (DAX)](https://msdn.microsoft.com/library/gg492170.aspx)  
[CUSTOMDATA, fonction (DAX)](https://msdn.microsoft.com/library/hh213140.aspx)  