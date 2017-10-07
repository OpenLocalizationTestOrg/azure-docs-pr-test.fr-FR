---
title: "aaaAnalyze des données dans Data Lake Store à l’aide de Power BI | Documents Microsoft"
description: "Utiliser des données de tooanalyze de Power BI stockées dans Azure Data Lake Store"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 57d19d27-e135-49d9-a7ea-46c48ef4e3bd
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 6a1bfa80fd1b0dda59b7eaaae9ca1585ba42783e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-data-in-data-lake-store-by-using-power-bi"></a>Analyse des données dans Data Lake Store à l’aide de Power BI
Dans cet article, vous allez apprendre comment toouse Power BI Desktop tooanalyze et visualiser les données stockées dans Azure Data Lake Store.

## <a name="prerequisites"></a>Composants requis
Avant de commencer ce didacticiel, vous devez disposer de hello :

* **Un abonnement Azure**. Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Compte Azure Data Lake Store**. Suivez les instructions de hello à [prise en main Azure Data Lake Store à l’aide de hello Azure Portal](data-lake-store-get-started-portal.md). Cet article suppose que vous avez déjà créé un compte Data Lake Store appelé **mybidatalakestore**et téléchargé un fichier de données (**Drivers.txt**) tooit. Cet exemple de fichier est disponible au téléchargement à partir du [référentiel Git d’Azure Data Lake](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).
* **Power BI Desktop**. Vous pouvez le télécharger à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=45331). 

## <a name="create-a-report-in-power-bi-desktop"></a>Création d’un rapport dans Power BI Desktop
1. Lancez Power BI Desktop sur votre ordinateur.
2. À partir de hello **accueil** du ruban, cliquez sur **obtenir des données**, puis cliquez sur plus d’informations. Bonjour **obtenir des données** boîte de dialogue, cliquez sur **Azure**, cliquez sur **Azure Data Lake Store**, puis cliquez sur **connexion**.
   
    ![Se connecter tooData Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account.png "Connect tooData Lake Store")
3. Si vous voyez une boîte de dialogue à propos de connecteur hello en cours d’une phase de développement, s’abonner toocontinue.
4. Bonjour **Microsoft Azure Data Lake Store** boîte de dialogue, fournissez hello URL tooyour Data Lake Store compte, puis cliquez sur **OK**.
   
    ![URL de Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-url.png "URL de Data Lake Store")
5. Dans la boîte de dialogue suivante hello, cliquez sur **connectez-vous** toosign dans le compte Data Lake Store. Vous serez redirigé page de connexion tooyour de l’organisation. Suivez hello invites toosign considération hello.
   
    ![Se connecter à Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-signin.png "Se connecter à Data Lake Store")
6. Une fois que vous vous êtes connecté, cliquez sur **Connexion**.
   
    ![Se connecter tooData Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-connect.png "Connect tooData Lake Store")
7. boîte de dialogue Hello suivante montre les fichier hello que vous avez téléchargé le compte Data Lake Store de tooyour. Vérifiez les informations de hello et puis cliquez sur **charge**.
   
    ![Charger des données à partir de Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-load.png "Charger des données à partir de Data Lake Store")
8. Une fois que les données de salutation a été correctement chargées dans Power BI, vous verrez hello suivant champs Bonjour **champs** onglet.
   
    ![Champs importés](./media/data-lake-store-power-bi/imported-fields.png "Champs importés")
   
    Toutefois, toovisualize et analyser les données de hello, nous préférons hello toobe de données disponible par hello suivant des champs
   
    ![Champs souhaités](./media/data-lake-store-power-bi/desired-fields.png "Champs souhaités")
   
    Dans les étapes suivantes hello, nous mettrons à jour hello interroger tooconvert hello importé des données dans le format désiré de hello.
9. À partir de hello **accueil** du ruban, cliquez sur **modifier les requêtes**.
   
    ![Modifier des requêtes](./media/data-lake-store-power-bi/edit-queries.png "Modifier des requêtes")
10. Bonjour, l’éditeur de requête sous hello **contenu** colonne, cliquez sur **binaire**.
    
    ![Modifier des requêtes](./media/data-lake-store-power-bi/convert-query1.png "Modifier des requêtes")
11. Vous verrez une icône de fichier, qui représente le hello **Drivers.txt** fichier que vous avez téléchargé. Fichier de hello d’avec le bouton droit, puis cliquez sur **CSV**.    
    
    ![Modifier des requêtes](./media/data-lake-store-power-bi/convert-query2.png "Modifier des requêtes")
12. Une sortie comme celle illustrée ci-dessous doit s’afficher. Vos données sont maintenant disponibles dans un format que vous pouvez utiliser les visualisations toocreate.
    
    ![Modifier des requêtes](./media/data-lake-store-power-bi/convert-query3.png "Modifier des requêtes")
13. À partir de hello **accueil** du ruban, cliquez sur **fermer et appliquer**, puis cliquez sur **fermer et appliquer**.
    
    ![Modifier des requêtes](./media/data-lake-store-power-bi/load-edited-query.png "Modifier des requêtes")
14. Une fois la requête de hello est mise à jour, hello **champs** onglet affiche hello nouveaux champs disponibles pour la visualisation.
    
    ![Champs mis à jour](./media/data-lake-store-power-bi/updated-query-fields.png "Champs mis à jour")
15. Nous créer d’un graphique à secteurs de toorepresent hello pilotes dans chaque ville d’un pays donné. toodo par conséquent, assurez-vous que les choix suivants de hello.
    
    1. À partir de l’onglet de visualisations hello, cliquez sur le symbole hello pour un graphique à secteurs.
       
        ![Créer un graphique à secteurs](./media/data-lake-store-power-bi/create-pie-chart.png "Créer un graphique à secteurs")
    2. colonnes Hello que nous allons toouse sont **colonne 4** (nom de ville de hello) et **colonne 7** (nom du pays de hello). Faites glisser ces colonnes de **champs** onglet trop**visualisations** onglet comme indiqué ci-dessous.
       
        ![Créer des visualisations](./media/data-lake-store-power-bi/create-visualizations.png "Créer des visualisations")
    3. graphique à secteurs de Hello doit maintenant ressembler à hello illustré ci-dessous.
       
        ![Graphique à secteurs](./media/data-lake-store-power-bi/pie-chart.png "Créer des visualisations")
16. En sélectionnant un pays spécifique à partir de filtres au niveau de la page hello, vous pouvez maintenant voir le nombre de hello de pilotes dans chaque ville de pays de hello sélectionné. Par exemple, sous hello **visualisations** sous l’onglet sous **filtres au niveau de la Page**, sélectionnez **Brésil**.
    
    ![Sélectionner un pays](./media/data-lake-store-power-bi/select-country.png "Sélectionner un pays")
17. graphique à secteurs de Hello est toodisplay mis à jour automatiquement les pilotes de hello dans les villes hello du Brésil.
    
    ![Pilotes dans un pays](./media/data-lake-store-power-bi/driver-per-country.png "Pilotes par pays")
18. À partir de hello **fichier** menu, cliquez sur **enregistrer** visualisation de hello toosave sous forme de fichier Power BI Desktop.

## <a name="publish-report-toopower-bi-service"></a>Publier le service de rapport tooPower BI
Une fois que vous avez créé des visualisations hello dans Power BI Desktop, vous pouvez le partager avec d’autres utilisateurs en le publiant un service de toohello Power BI. Pour obtenir des instructions sur la façon de toodo qui, consultez [publier à partir de Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-upload-desktop-files/).

## <a name="see-also"></a>Voir aussi
* [Analyse des données dans Data Lake Store à l’aide de Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md)

