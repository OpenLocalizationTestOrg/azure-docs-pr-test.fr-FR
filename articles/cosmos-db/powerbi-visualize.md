---
title: "didacticiel de BI aaaPower pour le connecteur de base de données Azure Cosmos | Documents Microsoft"
description: "Utilisez cette tooimport de didacticiel Power BI JSON, créer des rapports détaillés et visualiser les données à l’aide du connecteur de base de données Azure Cosmos et Power BI hello."
keywords: "didacticiel power BI, visualiser les données, connecteur Power BI"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: cd1b7f70-ef99-40b7-ab1c-f5f3e97641f7
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: mimig
ms.openlocfilehash: ca0bb8b76db8ef2ec936722b682af6a9488a3501
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="power-bi-tutorial-for-azure-cosmos-db-visualize-data-using-hello-power-bi-connector"></a>Didacticiel de BI de puissance pour la base de données Azure Cosmos : visualiser des données à l’aide du connecteur Power BI de hello
[PowerBI.com](https://powerbi.microsoft.com/) est un service en ligne dans laquelle vous pouvez créer et partager des tableaux de bord et rapports avec des données qui sont important tooyou et votre organisation.  Power BI Desktop est dédiée outil qui vous permet de tooretrieve des données de rapport à partir de diverses sources de données, fusionner et transformer des données de hello, créer des visualisations et des rapports puissants et publier des rapports de hello tooPower BI.  Avec la version la plus récente hello de Power BI Desktop, vous pouvez désormais connecter compte de base de données Cosmos tooyour via le connecteur de base de données Cosmos hello pour Power BI.   

Dans ce didacticiel Power BI, nous guider hello étapes tooconnect tooa compte Cosmos DB dans Power BI Desktop, accédez collection tooa que nous voulons les données de hello tooextract à l’aide de hello navigateur, de transformer les données JSON dans un format tabulaire à l’aide de la requête de Power BI Desktop L’éditeur et générer et publier un rapport tooPowerBI.com.

Quand ils auront terminé ce didacticiel Power BI, vous serez hello en mesure de tooanswer suivant questions :  

* Comment générer des rapports avec des données issues de Cosmos DB à l’aide de Power BI Desktop ?
* Comment puis-je connecter le compte de base de données Cosmos tooa dans Power BI Desktop ?
* Comment récupérer des données d’une collection dans Power BI Desktop ?
* Comment transformer des données JSON imbriquées dans Power BI Desktop ?
* Comment publier et partager mes rapports dans PowerBI.com ?

> [!NOTE]
> connecteur de Power BI Hello pour la base de données Azure Cosmos connecte tooPower BI Desktop pour l’extraction et de transformation de données. Les rapports créés dans Power BI Desktop peuvent ensuite être publié tooPowerBI.com. L’extraction et la transformation directes des données Azure Cosmos DB ne peuvent pas être effectuées sur PowerBI.com. 

## <a name="prerequisites"></a>Composants requis
Avant de suivre les instructions de hello dans ce didacticiel Power BI, vérifiez que vous avez toohello accès suivant de ressources :

* [version la plus récente de Power BI Desktop Hello](https://powerbi.microsoft.com/desktop).
* Compte d’accès tooour démonstration ou de données dans votre compte de base de données Cosmos.
  * compte de démonstration Hello est remplie avec les données d’îles hello indiquées dans ce didacticiel. Ce compte de démonstration n’est lié à aucun contrat de niveau de service et est réservé uniquement à des fins de démonstration.  Nous nous réservons hello toomake droite modifications toothis démonstration compte, y compris mais non limité à, arrêt hello compte, la modification de clé hello, de restreindre l’accès, la modification, de supprimer hello, à tout moment sans préavis ou raison.
    * URL : https://analytics.documents.azure.com
    * Clé en lecture seule : MSr6kt7Gn0YRQbjd6RbTnTt7VHc5ohaAFu7osF0HdyQmfR + YhwCH2D2jcczVIR1LNK3nMPNBD31losN7lQ/fkw ==
  * Ou, toocreate votre propre compte, consultez [créer un compte de base de données de base de données Azure Cosmos à l’aide de hello portail Azure](https://azure.microsoft.com/documentation/articles/create-account/). Ensuite, tooget exemples îles de données sont similaire de toowhat utilisé dans ce didacticiel (ne contient pas de blocs de GeoJSON hello), voir hello [site de NOAA](https://www.ngdc.noaa.gov/nndc/struts/form?t=102557&s=5&d=5) , puis importer les données hello à l’aide de hello [migration des données de base de données Azure Cosmos outil](import-data.md).

tooshare vos rapports dans PowerBI.com, vous devez avoir un compte sur PowerBI.com.  toolearn en savoir plus sur Power BI pour gratuit et Power BI Pro, visitez [https://powerbi.microsoft.com/pricing](https://powerbi.microsoft.com/pricing).

## <a name="lets-get-started"></a>Prise en main
Dans ce didacticiel, imaginons que vous êtes un geologist étudiant tableaux monde hello.  données îles de Hello sont stockées dans un compte de base de données Cosmos et des documents JSON hello ressembler hello suivant l’exemple de document.

    {
        "Volcano Name": "Rainier",
           "Country": "United States",
          "Region": "US-Washington",
          "Location": {
            "type": "Point",
            "coordinates": [
              -121.758,
              46.87
            ]
          },
          "Elevation": 4392,
          "Type": "Stratovolcano",
          "Status": "Dendrochronology",
          "Last Known Eruption": "Last known eruption from 1800-1899, inclusive"
    }

Vous souhaitez données îles tooretrieve hello hello Cosmos DB compte et visualiser les données dans un rapport Power BI interactive comme hello suivant le rapport.

![Ils auront terminé ce didacticiel Power BI avec le connecteur Power BI de hello, vous serez toovisualize en mesure des données avec hello rapport îles de Power BI Desktop](./media/powerbi-visualize/power_bi_connector_pbireportfinal.png)

Prêt toogive informatique a try ? Allons-y.

1. Exécutez Power BI Desktop sur votre station de travail.
2. Après le démarrage de Power BI Desktop, un écran d’ *accueil* s’affiche.
   
    ![Power BI Desktop - Écran d’accueil - Connecteur Power BI](./media/powerbi-visualize/power_bi_connector_welcome.png)
3. Vous pouvez **obtenir des données**, consultez **Sources récentes**, ou **ouvrir d’autres rapports** directement à partir de hello *Bienvenue* écran.  Cliquez sur hello X à l’écran de hello tooclose hello coin supérieur droit. Hello **rapport** de Power BI Desktop s’affiche.
   
    ![Power BI Desktop - Vue Rapport - Connecteur Power BI](./media/powerbi-visualize/power_bi_connector_pbireportview.png)
4. Sélectionnez hello **accueil** du ruban, puis cliquez sur **obtenir des données**.  Hello **obtenir des données** fenêtre doit s’afficher.
5. Cliquez sur **Azure**, sélectionnez **Microsoft Azure DocumentDB (Beta)**, puis cliquez sur **Se connecter**. 

    ![Power BI Desktop - Obtenir des données - Connecteur Power BI](./media/powerbi-visualize/power_bi_connector_pbigetdata.png)   
6. Sur hello **aperçu connecteur** , cliquez sur **continuer**. Hello **Microsoft Azure DocumentDB Connect** fenêtre s’affiche.
7. Spécifiez l’URL du point de terminaison hello Cosmos DB compte vous serez comme données hello tooretrieve comme indiqué ci-dessous, puis cliquez sur **OK**. toouse votre propre compte, vous pouvez récupérer hello URL à partir de l’URI de hello zone hello  **[clés](manage-account.md#keys)**  Panneau de hello portail Azure. toouse hello compte de démonstration, entrez `https://analytics.documents.azure.com` pour hello URL. 
   
    Ne renseignez nom de base de données hello, nom de la collection et d’instruction SQL que ces champs sont facultatifs.  Au lieu de cela, nous allons utiliser hello Navigator tooselect hello de base de données et de la Collection tooidentify d'où proviennent les données hello.
   
    ![Didacticiel Power BI pour le connecteur Microsoft Azure Cosmos DB et Power BI - Fenêtre de connexion](./media/powerbi-visualize/power_bi_connector_pbiconnectwindow.png)
8. Si vous vous connectez à toothis de point de terminaison pour hello première fois, vous êtes invité pour la clé de compte hello. Pour votre propre compte, extraire la clé de hello hello **clé primaire** zone hello  **[clés en lecture seule](manage-account.md#keys)**  Panneau de hello portail Azure. Pour le compte de démonstration hello, clé de hello est `MSr6kt7Gn0YRQbjd6RbTnTt7VHc5ohaAFu7osF0HdyQmfR+YhwCH2D2jcczVIR1LNK3nMPNBD31losN7lQ/fkw==`. Entrez la clé appropriée de hello et puis cliquez sur **connexion**.
   
    Nous vous recommandons d’utiliser clé en lecture seule de hello lors de la création de rapports.  Cela empêchera toute exposition inutile hello clé principale toopotential des risques de sécurité. clé de Hello en lecture seule est disponible à partir de hello [clés](manage-account.md#keys) Panneau de hello portail Azure, ou vous pouvez utiliser les informations de compte de démonstration hello fournies ci-dessus.
   
    ![Didacticiel Power BI pour le connecteur Microsoft Azure Cosmos DB et Power BI - Clé du compte](./media/powerbi-visualize/power_bi_connector_pbidocumentdbkey.png)
    
    > [!NOTE] 
    > Si vous obtenez une erreur indiquant que « base de données hello spécifiée est introuvable. » consultez les étapes de cette solution de contournement hello [problème de Power BI](https://community.powerbi.com/t5/Issues/Document-DB-Power-BI/idi-p/208200).
    
9. Lorsque le compte de hello est correctement connecté, hello **Navigator** s’affiche.  Hello **Navigator** affiche une liste des bases de données sous le compte de hello.
10. Développez sur base de données hello où les données hello pour les rapports hello proviennent, si vous utilisez un compte de démonstration hello, sélectionnez **volcanodb**.   
11. À présent, sélectionnez le regroupement qui vous permettra de récupérer les données de hello à partir de. Si vous utilisez un compte de démonstration hello, sélectionnez **volcano1**.
    
    volet de visualisation Hello affiche une liste de **enregistrement** éléments.  Dans Power BI, un Document est représenté sous la forme d’un type d’ **enregistrement** . De même, un bloc JSON imbriqué à l’intérieur d’un document est également considéré comme un **enregistrement**.
    
    ![Didacticiel Power BI pour le connecteur Microsoft Azure Cosmos DB et Power BI - Fenêtre de Navigateur](./media/powerbi-visualize/power_bi_connector_pbinavigator.png)
12. Cliquez sur **modifier** toolaunch hello éditeur de requête dans les données de salutation une nouvelle fenêtre tootransform.

## <a name="flattening-and-transforming-json-documents"></a>Mise à plat et transformation de documents JSON
1. Basculer la fenêtre de l’éditeur de requête de Power BI toohello, où hello **Document** colonne dans le volet central de hello.
   ![Power BI Desktop - Éditeur de requête](./media/powerbi-visualize/power_bi_connector_pbiqueryeditor.png)
2. Cliquez sur un expander hello à droite hello Hello **Document** en-tête de colonne.  menu contextuel de Hello avec une liste de champs s’affiche.  Sélectionnez les champs hello vous avez besoin pour votre rapport, par exemple, îles nom, pays, région, emplacement, élévation, Type, état et dernière création de savoir, puis cliquez sur **OK**.
   
    ![Didacticiel Power BI pour le connecteur Microsoft Azure Cosmos DB et Power BI - Développement des documents](./media/powerbi-visualize/power_bi_connector_pbiqueryeditorexpander.png)
3. volet central de Hello affiche un aperçu du résultat de hello avec champs hello sélectionnés.
   
    ![Didacticiel Power BI pour le connecteur Microsoft Azure Cosmos DB et Power BI - Résultats aplatis](./media/powerbi-visualize/power_bi_connector_pbiresultflatten.png)
4. Dans notre exemple, hello propriété d’emplacement est un bloc de GeoJSON dans un document.  Comme vous pouvez le constater, l’emplacement est représenté en tant que type d’ **enregistrement** dans Power BI Desktop.  
5. Cliquez sur un expander hello à droite hello d’en-tête de colonne emplacement hello.  menu contextuel de Hello avec des champs de type et les coordonnées s’affiche.  Nous allons sélectionner le champ de coordonnées hello et cliquez sur **OK**.
   
    ![Didacticiel Power BI pour le connecteur Microsoft Azure Cosmos DB et Power BI - Enregistrement emplacement](./media/powerbi-visualize/power_bi_connector_pbilocationrecord.png)
6. Hello volet central affiche maintenant une colonne de coordonnées de **liste** type.  Comme indiqué au début de hello du didacticiel de hello, hello données GeoJSON dans ce didacticiel est de type Point avec les valeurs de Latitude et Longitude enregistrés dans le tableau de coordonnées hello.
   
    élément de coordonnées [0] Hello représente Longitude tandis que les coordonnées [1] représente la Latitude.
    ![Didacticiel Power BI pour le connecteur Microsoft Azure Cosmos DB et Power BI - Liste des coordonnées](./media/powerbi-visualize/power_bi_connector_pbiresultflattenlist.png)
7. tableau des coordonnées tooflatten hello, nous allons créer un **une colonne personnalisée** appelé LatLong.  Sélectionnez hello **ajouter une colonne** du ruban, puis cliquez sur **ajouter une colonne personnalisée**.  Hello **ajouter une colonne personnalisée** fenêtre doit s’afficher.
8. Fournissez un nom pour la nouvelle colonne hello, par exemple, LatLong.
9. Spécifiez ensuite la formule personnalisée de hello pour la nouvelle colonne de hello.  Dans notre exemple, nous concaténer des valeurs de Latitude et de Longitude hello séparées par une virgule, comme illustré ci-dessous à l’aide de la formule suivante de hello : `Text.From([coordinates]{1})&","&Text.From([coordinates]{0})`. Cliquez sur **OK**.
   
    Pour plus d’informations sur le langage DAX (Data Analysis Expressions) et notamment sur les fonctions DAX, consultez la page [DAX Basic in Power BI Desktop (Dax de base dans Power BI Desktop)](https://support.powerbi.com/knowledgebase/articles/554619-dax-basics-in-power-bi-desktop).
   
    ![Didacticiel Power BI pour le connecteur Microsoft Azure Cosmos DB et Power BI - Ajout d’une colonne personnalisée](./media/powerbi-visualize/power_bi_connector_pbicustomlatlong.png)
10. Maintenant, hello center volet affiche hello LatLong colonne renseignée avec hello Latitude et des valeurs de Longitude séparés par une virgule.
    
    ![Didacticiel Power BI pour le connecteur Microsoft Azure Cosmos DB et Power BI - Colonne personnalisée LatLong](./media/powerbi-visualize/power_bi_connector_pbicolumnlatlong.png)
    
    Si vous recevez une erreur dans la nouvelle colonne de hello, assurez-vous que les étapes de hello appliqué sous les paramètres de la requête correspondent au hello figure suivante :
    
    ![Les étapes appliquées doivent être Source, Navigation, Expanded Document, Expanded Document.Location, Added Custom](./media/powerbi-visualize/power-bi-applied-steps.png)
    
    Si vos étapes sont différentes, supprimer des étapes supplémentaires de hello et essayez à nouveau d’ajouter une colonne personnalisée hello. 
11. Nous avons terminé les données de salutation mise à plat au format tabulaire.  Vous pouvez tirer parti de toutes les fonctionnalités hello hello tooshape de l’éditeur de requête et transformer des données dans la base de données Cosmos.  Si vous utilisez l’exemple hello, type de données hello élévation également modifier**nombre entier** en modifiant hello **Type de données** sur hello **accueil** ruban.
    
    ![Didacticiel Power BI pour le connecteur Microsoft Azure Cosmos DB et Power BI - Modification du type de colonne](./media/powerbi-visualize/power_bi_connector_pbichangetype.png)
12. Cliquez sur **fermer et appliquer** modèle de données toosave hello.
    
    ![Didacticiel Power BI pour le connecteur Microsoft Azure Cosmos DB et Power BI - Fermer et appliquer](./media/powerbi-visualize/power_bi_connector_pbicloseapply.png)

<a id="build-the-reports"></a>
## <a name="build-hello-reports"></a>Générer des rapports de hello
Vue de Power BI Desktop rapport est où vous pouvez commencer la création de rapports toovisualize données.  Vous pouvez créer des rapports en faisant glisser les champs dans hello **rapport** canevas.

![Power BI Desktop - Vue Rapport - Connecteur Power BI](./media/powerbi-visualize/power_bi_connector_pbireportview2.png)

Bonjour vue rapport, vous devez rechercher :

1. Hello **champs** volet, il s’agit où vous verrez une liste de modèles de données avec des champs que vous pouvez utiliser pour vos rapports.
2. Hello **visualisations** volet. Un rapport peut contenir une ou plusieurs visualisations.  Choisir les types d’éléments visuels hello raccord vos besoins de hello **visualisations** volet.
3. Hello **rapport** zone de dessin, il s’agit d’où vous allez créer des éléments visuels de hello pour votre rapport.
4. Hello **rapport** page. Vous pouvez ajouter plusieurs pages de rapport dans Power BI Desktop.

Hello Voici hello principales étapes de création d’un rapport de vue cartographique interactif simple.

1. Dans notre exemple, nous allons créer une vue cartographique montrant emplacement hello de chaque îles.  Bonjour **visualisations** volet, cliquez sur le type d’élément visuel hello carte mise en évidence dans la capture d’écran hello ci-dessus.  Vous devez voir hello carte type d’élément visuel peinte sur hello **rapport** canevas.  Hello **visualisation** volet doit afficher également un ensemble de toohello de propriétés connexes type visual de carte.
2. Maintenant, faites glisser des champs de LatLong hello de hello **champs** volet toohello **emplacement** propriété dans **visualisations** volet.
3. Ensuite, faites glisser hello îles nom champ toohello **légende** propriété.  
4. Ensuite, faites glisser hello élévation champ toohello **taille** propriété.  
5. Vous devez maintenant voir hello mappage visual contenant un ensemble de bulles indiquant l’emplacement hello de chaque îles avec une taille de bulle hello corrélation élévation toohello d’îles de hello hello.
6. Vous avez maintenant créé un rapport de base.  Vous pouvez personnaliser davantage les rapports hello en ajoutant davantage de visualisations.  Dans notre cas, nous avons ajouté un rapport de hello îles Type segment toomake interactif.  
   
    ![Capture d’écran de rapport de Power BI Desktop final hello à la fin du didacticiel de Power BI hello pour la base de données Azure Cosmos](./media/powerbi-visualize/power_bi_connector_pbireportfinal.png)

## <a name="publish-and-share-your-report"></a>Publier et partager votre rapport
tooshare votre rapport, vous devez posséder un compte sur PowerBI.com.

1. Bonjour Power BI Desktop, cliquez sur hello **accueil** ruban.
2. Cliquez sur **Publier**.  Vous serez invité à tooenter hello mot de passe pour votre compte PowerBI.com.
3. Une fois que les informations d’identification hello a été authentifiée, les rapports hello sont destination publiée tooyour que vous avez sélectionné.
4. Cliquez sur **'PowerBITutorial.pbix' ouvrir dans Power BI** toosee et partager votre rapport sur PowerBI.com.
   
    ![Publication tooPower BI succès ! Ouvrir le didacticiel dans Power BI](./media/powerbi-visualize/power_bi_connector_open_in_powerbi.png)

## <a name="create-a-dashboard-in-powerbicom"></a>Créer un tableau de bord dans PowerBI.com
Maintenant que vous disposez d’un rapport, partageons-le dans PowerBI.com.

Lorsque vous publiez votre rapport à partir de Power BI Desktop tooPowerBI.com, il génère une **rapport** et un **Dataset** dans votre client PowerBI.com. Par exemple, une fois que vous avez publié un rapport appelé **PowerBITutorial** tooPowerBI.com, vous verrez PowerBITutorial dans les deux hello **rapports** et **Datasets** sections sur PowerBI.com.

   ![Capture d’écran de hello nouveau rapport et un Dataset dans PowerBI.com](./media/powerbi-visualize/powerbi-reports-datasets.png)

toocreate un tableau de bord partageable, cliquez sur hello **épingler une Page dynamique** bouton sur votre rapport PowerBI.com.

   ![Capture d’écran de hello nouveau rapport et un Dataset dans PowerBI.com](./media/powerbi-visualize/power-bi-pin-live-tile.png)

Puis suivez les instructions de hello dans [épingler une vignette à partir d’un rapport](https://powerbi.microsoft.com/documentation/powerbi-service-pin-a-tile-to-a-dashboard-from-a-report/#pin-a-tile-from-a-report) toocreate un tableau de bord. 

Vous pouvez également effectuer des modifications ad hoc tooreport avant de créer un tableau de bord. Toutefois, il est recommandé que vous utilisez des modifications de Power BI Desktop tooperform hello et republiez hello rapport tooPowerBI.com.

## <a name="refresh-data-in-powerbicom"></a>Actualiser les données dans PowerBI.com
Il existe deux façons de données toorefresh, ad hoc et planifiées.

Pour une actualisation ad hoc, cliquez simplement sur l’eclipses hello (...) en hello **Dataset**, par exemple, PowerBITutorial. Une liste d’actions doit s’afficher, comprenant notamment **Actualiser maintenant**. Cliquez sur **Actualiser maintenant** toorefresh les données de salutation.

![Capture d’écran de la fenêtre Actualiser maintenant dans PowerBI.com](./media/powerbi-visualize/power-bi-refresh-now.png)

Pour une actualisation planifiée, procédez comme hello suivant.

1. Cliquez sur **planifier l’actualisation** dans la liste des actions hello. 

    ![Capture d’écran de hello planifier l’actualisation dans PowerBI.com](./media/powerbi-visualize/power-bi-schedule-refresh.png)
2. Bonjour **paramètres** page, développez **informations d’identification de source de données**. 
3. Cliquez sur **Modifier les informations d’identification**. 
   
    menu contextuel de configurer Hello s’affiche. 
4. Entrez le compte de Cosmos DB toohello hello tooconnect clé pour ce jeu de données, puis cliquez sur **connectez-vous**. 
5. Développez **planifier l’actualisation** et configurer la planification de hello toorefresh hello dataset. 
6. Cliquez sur **appliquer** et que vous avez terminé de configurer l’actualisation planifiée de hello.

## <a name="next-steps"></a>Étapes suivantes
* toolearn en savoir plus sur Power BI, consultez [prise en main de Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/).
* toolearn savoir plus sur Cosmos DB, consultez hello [page d’accueil de documentation de base de données Azure Cosmos](https://azure.microsoft.com/documentation/services/documentdb/).

