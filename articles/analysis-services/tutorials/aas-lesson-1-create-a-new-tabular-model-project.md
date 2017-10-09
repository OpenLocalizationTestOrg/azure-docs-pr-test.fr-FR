---
titre : aaa « leçon du didacticiel Azure Analysis Services 1 : créer un projet de modèle tabulaire | Description de Microsoft Docs » : décrit comment toocreate une nouvelle analyse Azure Services projet du didacticiel. Services : analysis services documentationcenter : '' auteur : minewiskan manager : erikre éditeur : '' balises : ».

MS.AssetId : ms.service : ms.devlang d’analysis services : NA ms.topic : get-started-article ms.tgt_pltfrm : NA ms.workload : na ms.date : 01/06/2017 ms.author : owend
---
# <a name="lesson-1-create-a-tabular-model-project"></a>Leçon 1 : Créer un projet de modèle tabulaire

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Dans cette leçon, vous utilisez SQL Server Data Tools (SSDT) toocreate un nouveau projet de modèle tabulaire au niveau de compatibilité 1400 hello. Une fois votre nouveau projet créé, vous pouvez commencer à ajouter des données et à créer votre modèle. Cette leçon vous donne une brève introduction toohello création de modèles tabulaires environnement dans SSDT.  
  
Estimé temps toocomplete cette leçon : **10 minutes**  
  
## <a name="prerequisites"></a>Composants requis  
Cette rubrique est hello première leçon du didacticiel de conception de modèle tabulaire. toocomplete de cette leçon, vous devez toohave in situ de plusieurs conditions préalables. toolearn, voir [Azure Analysis Services - didacticiel Adventure Works](../tutorials/aas-adventure-works-tutorial.md).  
  
## <a name="create-a-new-tabular-model-project"></a>Créer un projet de modèle tabulaire  
  
#### <a name="toocreate-a-new-tabular-model-project"></a>toocreate un nouveau projet de modèle tabulaire  
  
1.  Dans SSDT, sur hello **fichier** menu, cliquez sur **nouveau** > **projet**.  
  
2.  Bonjour **nouveau projet** boîte de dialogue, développez **installé** > **Business Intelligence** > **Analysis Services**, puis cliquez sur **projet tabulaire Analysis Services**.  
  
3.  Dans **nom**, type **AW Internet Sales**, puis spécifiez un emplacement pour les fichiers de projet hello.  
  
    Par défaut, **nom de la Solution** est même hello comme nom de projet hello ; Toutefois, vous pouvez taper un nom de l’autre solution.  
  
4.  Cliquez sur **OK**.  
  
5.  Bonjour **Générateur de modèles tabulaires** boîte de dialogue, sélectionnez **espace de travail intégré**.  
  
    espace de travail Hello héberge une base de données de modèle tabulaire avec hello même nom en tant que projet de hello pendant la création du modèle. Espace de travail intégré signifie que SSDT utilise une instance intégrée, éliminant hello besoin tooinstall une instance distincte de serveur Analysis Services uniquement pour la création d’un modèle.
      
6.  Dans **Niveau de compatibilité**, sélectionnez **SQL Server 2017/Azure Analysis Services (1400)**.   
 
    ![aas-lesson1-tmd](../tutorials/media/aas-lesson1-tmd.png)
      
    Si vous ne voyez pas SQL Server 2017 / Azure Analysis Services (1400) dans la zone de liste au niveau de compatibilité de hello, vous n’utilisez pas de version la plus récente de SQL Server Data Tools hello. version la plus récente tooget hello, consultez [installer SQL Server Data tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt).  
      
  
## <a name="understanding-hello-ssdt-tabular-model-authoring-environment"></a>Comprendre l’environnement de création de modèles tabulaires SSDT hello  
Maintenant que vous avez créé un nouveau projet de modèle tabulaire, prenons un modèle tabulaire hello tooexplore moment environnement de création dans SSDT.  
  
Une fois votre projet créé, il s’ouvre dans SSDT. Sur hello côté droit, dans **l’Explorateur de modèles tabulaires**, vous voyez une arborescence d’objets de hello dans votre modèle. Étant donné que vous n’avez pas encore importé des données, les dossiers hello sont vides. Vous pouvez cliquer sur un objet actions tooperform du dossier, la barre de menus toohello similaire. À mesure que vous parcourez ce didacticiel, vous utilisez hello Explorateur de modèles tabulaires toonavigate différents objets dans votre projet de modèle.

![aas-lesson1-tme](../tutorials/media/aas-lesson1-tme.png)

Cliquez sur hello **l’Explorateur de solutions** onglet. Le fichier **Model.bim** s’y trouve. Si vous ne voyez pas hello fenêtre du concepteur toohello gauche (hello fenêtre vide avec onglet Model.bim de hello), dans **l’Explorateur de solutions**, sous **projet AW Internet Sales**, double-cliquez sur hello  **Model.BIM** fichier. fichier de Model.bim Hello contient des métadonnées de hello pour votre projet de modèle. 

![aas-lesson1-se](../tutorials/media/aas-lesson1-se.png)
  
Cliquez sur **Model.bim**. Bonjour **propriétés** fenêtre, vous consultez les propriétés du modèle hello, qui est hello plus importantes **DirectQuery Mode** propriété. Cette propriété spécifie si le modèle de hello est déployé en mode In-Memory (désactivé) ou en mode DirectQuery (activé). Pour ce didacticiel, vous créez et déployez votre modèle en mode In-Memory.

![aas-lesson1-properties](../tutorials/media/aas-lesson1-properties.png)
  
Lorsque vous créez un projet de modèle, certaines de ses propriétés sont définies automatiquement en fonction toohello des paramètres de modélisation des données qui peuvent être spécifiés dans hello **outils** menu > **Options** boîte de dialogue. Sauvegarde de données, la rétention de l’espace de travail et serveur d’espace de travail propriétés spécifient comment et où hello base de données (votre mode de création de base de données) est sauvegardée, conservée en mémoire et généré. Vous pouvez modifier ces paramètres ultérieurement si nécessaire, mais pour l’instant, laissez ces propriétés en l’état.  

Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur le projet **AW Internet Sales**, puis cliquez sur **Propriétés**. Hello **Pages de propriétés de AW Internet Sales** boîte de dialogue s’affiche. Vous allez définir certaines de ces propriétés ultérieurement lors du déploiement de votre modèle.  
  
Lorsque vous avez installé SSDT, plusieurs nouveaux éléments de menu ont été ajoutés environnement de Visual Studio toohello. Cliquez sur hello **modèle** menu. À ce stade, vous pouvez importer des données, actualiser les données de l’espace de travail, parcourir votre modèle dans Excel, créer des perspectives et des rôles, la vue du modèle, sélectionnez hello et définir les options de calcul. Cliquez sur hello **Table** menu. À ce stade vous pouvez créer et gérer les relations, spécifier les paramètres de la table de dates, créer des partitions et modifier les propriétés de la table. Si vous cliquez sur hello **colonne** menu, vous pouvez ajouter et supprimer des colonnes dans une table, figer des colonnes et spécifier l’ordre de tri. SSDT ajoute également certains barre toohello de boutons. Plus utile est toocreate de fonctionnalité de somme automatique hello une mesure d’agrégation standard pour une colonne sélectionnée. Autres boutons de barre d’outils fournissent elles sonttrop d’accès rapide utilisé les fonctionnalités et les commandes.  
  
Explorez les boîtes de dialogue hello et les emplacements pour les modèles tabulaires différentes fonctionnalités tooauthoring spécifique. Alors que certains éléments ne sont pas encore actives, vous pouvez obtenir une bonne idée de l’environnement de création du modèle tabulaire hello.  
  

## <a name="whats-next"></a>Et ensuite ?
[Leçon 2 : Obtenir des données](../tutorials/aas-lesson-2-get-data.md).

  
  
  
