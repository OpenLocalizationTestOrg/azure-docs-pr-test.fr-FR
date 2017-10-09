---
title: "intégration de flux de données Analytique et l’apprentissage d’aaaAzure | Documents Microsoft"
description: "Comment toouse un apprentissage automatique dans une tâche de flux de données Analytique et la fonction définie par l’utilisateur"
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: cfced01f-ccaa-4bc6-81e2-c03d1470a7a2
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 07/06/2017
ms.author: jeffstok
ms.openlocfilehash: e1ba7ab51ece80719839793e1320a7666cfc4181
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="performing-sentiment-analysis-by-using-azure-stream-analytics-and-azure-machine-learning"></a>Analyse des sentiments à l’aide d’Azure Stream Analytics et Azure Machine Learning
Cet article décrit comment tooquickly configurer une tâche Analytique de flux de données Azure simple qui s’intègre à Azure Machine Learning. Vous utilisez un modèle d’analytique sentiment Machine Learning à partir de hello données texte diffusion en continu de la galerie de Cortana Intelligence tooanalyze et déterminez le score d’opinion hello en temps réel. Hello Cortana Intelligence Suite vous permet de procéder sans vous soucier des complexités hello de la création d’un modèle d’analytique sentiments.

Vous pouvez appliquer ce que vous apprenez à partir de cette tooscenarios article telles que celles-ci :

* Analyse des sentiments en temps réel sur la diffusion de données Twitter en continu.
* Analyse des enregistrements de conversations de clients avec le personnel de support.
* Évaluation des commentaires sur les forums, blogs et vidéos. 
* Nombreux autres scénarios de notation prédictive en temps réel.

Dans un scénario réel, vous pourriez obtenir des données de salutation directement à partir d’un flux de données Twitter. toosimplify hello didacticiel, nous avons écrit il afin que hello Analytique de diffusion en continu travail obtient tweet à partir d’un fichier CSV dans le stockage d’objets Blob Azure. Vous pouvez créer votre propre fichier CSV, ou vous pouvez utiliser un exemple de fichier CSV, comme indiqué dans hello suivant image :

![exemples de tweets dans un fichier CSV](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-2.png)  

travail de diffusion en continu d’Analytique Hello que vous créez s’applique modèle d’analytique hello sentiment comme une fonction définie par l’utilisateur (UDF) sur les données texte hello à partir du magasin d’objets blob hello. sortie de Hello (résultat hello d’analyse des sentiments hello) est écrit toohello même magasin d’objets blob dans un autre fichier CSV. 

Hello figure suivante illustre cette configuration. Comme nous l’avons indiqué, pour un scénario plus réaliste, vous pouvez remplacer le stockage d’objets blob par la diffusion de données Twitter en continu à partir d’une entrée Event Hub Azure. En outre, vous pouvez générer un [Microsoft Power BI](https://powerbi.microsoft.com/) visualisation en temps réel de sentiment d’agrégation de hello.    

![Vue d’ensemble de l’intégration de Machine Learning dans Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-1.png)  

## <a name="prerequisites"></a>Composants requis
Avant de commencer, assurez-vous que vous avez hello suivantes :

* Un abonnement Azure actif.
* Un fichier CSV contenant des données. Vous pouvez télécharger le fichier hello présentée précédemment à partir de [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv), ou vous pouvez créer votre propre fichier. Pour cet article, nous supposons que vous utilisez le fichier hello à partir de GitHub.

À un niveau élevé, les tâches hello toocomplete présentés dans cet article, vous hello suivant :

1. Créer un compte de stockage Azure et un conteneur de stockage d’objets blob et télécharger un conteneur de toohello du fichier d’entrée au format CSV.
3. Ajouter un modèle d’analytique sentiment à partir de l’espace de travail Azure Machine Learning hello Cortana Intelligence galerie tooyour et déployer ce modèle en tant qu’un service web dans l’espace de travail Machine Learning hello.
5. Créer une tâche de flux de données Analytique qui appelle ce service web en fonction de l’opinion de toodetermine de commande pour l’entrée de texte hello.
6. Démarrer la tâche de flux de données Analytique hello et vérifier la sortie de hello.

## <a name="create-a-storage-container-and-upload-hello-csv-input-file"></a>Créer un conteneur de stockage et de télécharger un fichier d’entrée CSV hello
Pour cette étape, vous pouvez utiliser n’importe quel fichier CSV, par exemple hello disponible à partir de GitHub.

1. Bonjour portail Azure, cliquez sur **nouveau** &gt; **stockage** &gt; **compte de stockage**.

   ![créer un compte de stockage](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-create-storage-account.png)

2. Fournissez un nom (`samldemo` dans l’exemple de hello). nom de Hello peut utiliser que des lettres minuscules et des chiffres, et il doit être unique dans Azure. 

3. Spécifiez un groupe de ressources existant et un emplacement. Pour l’emplacement, nous recommandons que toutes les ressources hello créés dans ce didacticiel, utilisez hello même emplacement.

    ![indiquer les détails du compte de stockage](./media/stream-analytics-machine-learning-integration-tutorial/create-sa1.png)

4. Bonjour portail Azure, sélectionnez le compte de stockage hello. Dans le panneau de compte de stockage hello, cliquez sur **conteneurs** puis cliquez sur  **+ &nbsp;conteneur** toocreate stockage d’objets blob.

    ![créer un conteneur d’objets blob](./media/stream-analytics-machine-learning-integration-tutorial/create-sa2.png)

5. Fournissez un nom pour le conteneur de hello (`azuresamldemoblob` dans l’exemple de hello) et vérifiez que **type d’accès** est défini trop**Blob**. Quand vous avez terminé, cliquez sur **OK**.

    ![spécifier les détails du conteneur d’objets blob](./media/stream-analytics-machine-learning-integration-tutorial/create-sa3.png)

6. Bonjour **conteneurs** panneau, sélectionnez hello nouveau conteneur, qui ouvre le panneau hello pour ce conteneur.

7. Cliquez sur **Télécharger**.

    ![Bouton ’Télécharger’ d’un conteneur](./media/stream-analytics-machine-learning-integration-tutorial/create-sa-upload-button.png)

8. Bonjour **téléchargement blob** panneau, spécifiez le fichier CSV de hello que vous souhaitez toouse pour ce didacticiel. Pour **type d’objets Blob**, sélectionnez **objet blob de blocs** et ensemble hello bloc taille too4 Mo, ce qui est suffisant pour ce didacticiel.

    ![charger le fichier blob](./media/stream-analytics-machine-learning-integration-tutorial/create-sa4.png)

9. Cliquez sur hello **télécharger** bouton bas hello du Panneau de hello.

## <a name="add-hello-sentiment-analytics-model-from-hello-cortana-intelligence-gallery"></a>Ajouter un modèle d’analytique de sentiment hello de hello Cortana Intelligence galerie

Maintenant que les données d’exemple hello sont dans un objet blob, vous pouvez activer le modèle d’analyse de sentiments hello dans Cortana Intelligence galerie.

1. Accédez toohello [modèle analytique de sentiment prédictive](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) page Bonjour Cortana Intelligence galerie.  

2. Cliquez sur **Ouvrir dans Studio**.  
   
   ![Stream Analytics Machine Learning, ouvrir Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-open-ml-studio.png)  

3. Espace de travail toogo toohello vous connecter. Sélectionnez un emplacement.

4. Cliquez sur **exécuter** bas hello de page de hello. processus de Hello s’exécute, ce qui dure environ une minute.

   ![exécuter une expérience dans Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-run-experiment.png)  

5. Une fois le processus de hello s’est exécutée correctement, sélectionnez **déployer le Service Web** bas hello de page de hello.

   ![déployer l’expérience dans Machine Learning Studio en tant que service web](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-deploy-web-service.png)  

6. toovalidate qui hello sentiment modèle d’analytique est toouse prêt, cliquez sur hello **Test** bouton. Entrez du texte, par exemple « I love Microsoft ». 

   ![tester une expérience dans Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test.png)  

    Si le test de hello fonctionne, vous consultez un toohello comme résultat l’exemple suivant :

   ![résultats du test dans Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test-results.png)  

7. Bonjour **applications** colonne, cliquez sur hello **Excel 2010 ou classeur antérieur** toodownload de lien un classeur Excel. classeur de Hello contient clé de hello une API et l’URL de hello que vous avez besoin tooset ultérieure de la tâche de flux de données Analytique hello.

    ![Stream Analytics Machine Learning, aperçu rapide](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-quick-glance.png)  


## <a name="create-a-stream-analytics-job-that-uses-hello-machine-learning-model"></a>Créer une tâche de flux de données Analytique qui utilise le modèle d’apprentissage hello

Vous pouvez maintenant créer une tâche de flux Analytique qui lit hello exemple tweets d’un fichier CSV hello dans le stockage blob. 

### <a name="create-hello-job"></a>Créer le travail de hello

1. Accédez toohello [portail Azure](https://portal.azure.com).  

2. Dans le portail Azure, cliquez sur **Nouveau** > **Internet des objets** > **Travail Stream Analytics**. 

   ![Chemin d’accès au portail Azure pour obtenir la nouvelle tâche de flux de données Analytique tooa](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-new-iot-sa-job.png)
   
3. Nom du travail hello `azure-sa-ml-demo`, spécifiez un abonnement, spécifiez un groupe de ressources existant ou créez-en un et sélectionnez hello emplacement pour le travail de hello.

   ![spécifier les paramètres du nouveau travail Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-job-1.png)
   

### <a name="configure-hello-job-input"></a>Configurer l’entrée de tâche hello
travail de Hello obtient son entrée d’un fichier CSV hello que vous avez téléchargé antérieures tooblob stockage.

1. Une fois le travail de hello a été créé, sous **travail topologie** dans le panneau de tâche hello, cliquez sur hello **entrées** boîte.  
   
   ![zone 'Entrées' du panneau du travail dans Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input.png)  

2. Bonjour **entrées** panneau, cliquez sur **+ ajouter**.

   !['Add' bouton pour ajouter une tâche de flux de données Analytique toohello d’entrée](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input-button.png)  

3. Remplir hello **nouvelle entrée** panneau avec ces valeurs :

    * **Alias d’entrée**: utiliser le nom hello `datainput`.
    * **Type de source** : sélectionnez **Flux de données**.
    * **Source** : sélectionnez **Stockage d’objets blob**.
    * **Option d’importation** : sélectionnez **Utiliser l’objet blob de stockage de l’abonnement actuel**. 
    * **Compte de stockage**. Sélectionnez le compte de stockage hello que vous avez créé précédemment.
    * **Conteneur** : Conteneur de sélection hello vous avez créé précédemment (`azuresamldemoblob`).
    * **Format de sérialisation de l’événement**. Sélectionnez **CSV**.

    ![Paramètres de la nouvelle entrée de travail](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-create-sa-input-new-portal.png)

4. Cliquez sur **Créer**.

### <a name="configure-hello-job-output"></a>Configurer la sortie de tâche hello
Bonjour toohello de résultats de la tâche envoie même lorsqu’il obtient une entrée de stockage d’objets blob. 

1. Sous **travail topologie** dans le panneau de tâche hello, cliquez sur hello **sorties** boîte.  
  
   ![Créer une sortie pour le travail Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-output.png)  

2. Bonjour **sorties** panneau, cliquez sur **+ ajouter**, puis ajoutez une sortie avec l’alias de hello `datamloutput`. 

3. Au niveau du paramètre **Récepteur**, sélectionnez **Stockage d’objets blob**. Puis renseignez reste hello Hello de sortie à l’aide des paramètres hello les mêmes valeurs que vous avez utilisé pour le stockage d’objets blob hello pour l’entrée :

    * **Compte de stockage**. Sélectionnez le compte de stockage hello que vous avez créé précédemment.
    * **Conteneur** : Conteneur de sélection hello vous avez créé précédemment (`azuresamldemoblob`).
    * **Format de sérialisation de l’événement**. Sélectionnez **CSV**.

   ![Paramètres de la nouvelle sortie de travail](./media/stream-analytics-machine-learning-integration-tutorial/create-output2.png) 

4. Cliquez sur **Créer**.   


### <a name="add-hello-machine-learning-function"></a>Ajouter une fonction d’apprentissage hello 
Précédemment, vous avez publié un service web de Machine Learning modèle tooa. Dans notre scénario, lorsque la tâche d’analyse de flux de hello s’exécute, il envoie chaque tweet exemple hello toohello d’entrée web service pour l’analyse de sentiments. Hello service web Machine Learning retourne un sentiments (`positive`, `neutral`, ou `negative`) et une probabilité de tweet hello positif. 

Dans cette section du didacticiel de hello, vous définissez une fonction dans la tâche de flux de données analyse hello. fonction Hello peut être appelée toosend un service web de toohello tweet et revenir réponse de hello. 

1. Assurez-vous que vous avez hello web service URL et la clé API que vous avez téléchargé précédemment dans le classeur Excel de hello.

2. Panneau de vue d’ensemble du travail toohello retour.

3. Sous **Paramètres**, sélectionnez **Fonctions**, puis cliquez sur **+ Ajouter**.

   ![Ajouter une tâche de flux de données Analytique toohello (fonction)](./media/stream-analytics-machine-learning-integration-tutorial/create-function1.png) 

4. Entrez `sentiment` comme hello fonction alias et remplissez les autres hello du panneau hello à l’aide de ces valeurs :

    * **Type de fonction** : sélectionnez **Azure ML**.
    * **Option d’importation** : sélectionnez **Importer à partir d’un autre abonnement**. Cela vous donne une occasion tooenter hello URL et une clé.
    * **URL**: coller dans l’URL du service web hello.
    * **Clé**: coller dans la clé de l’API de hello.
  
    ![Paramètres pour l’ajout d’une tâche de flux de données Analytique toohello Machine Learning (fonction)](./media/stream-analytics-machine-learning-integration-tutorial/add-function.png)  
    
5. Cliquez sur **Créer**.

### <a name="create-a-query-tootransform-hello-data"></a>Créer une requête de données hello tootransform

Flux de données Analytique utilise une entrée de hello tooexamine requête déclarative basé sur SQL et le traiter. Dans cette section, vous créez une requête qui lit chaque tweet d’entrée, puis appelle analyse des sentiments tooperform hello Machine Learning (fonction). requête de Hello envoie ensuite hello résultat toohello de sortie que vous avez définies (stockage d’objets blob).

1. Panneau de vue d’ensemble du travail toohello retour.

2.  Sous **travail topologie**, cliquez sur hello **requête** boîte.

    ![Créer une requête pour le travail Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-query.png)  

3. Entrez hello suivant la requête :

    ```
    WITH sentiment AS (  
    SELECT text, sentiment(text) as result from datainput  
    )  

    Select text, result.[Score]  
    Into datamloutput
    From sentiment  
    ```    

    requête de Hello appelle la fonction hello que vous avez créé précédemment (`sentiment`) dans l’analyse des sentiments tooperform commande sur chaque tweet dans l’entrée de hello. 

4. Cliquez sur **enregistrer** requête de hello toosave.


## <a name="start-hello-stream-analytics-job-and-check-hello-output"></a>Démarrer la tâche de flux de données Analytique hello et vérifier la sortie de hello

Vous pouvez maintenant démarrer la tâche de flux de données Analytique hello.

### <a name="start-hello-job"></a>Démarrer le travail de hello
1. Panneau de vue d’ensemble du travail toohello retour.

2. Cliquez sur **Démarrer** haut hello du Panneau de hello.

    ![Créer une requête pour le travail Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/start-job.png)  

3. Bonjour **Start job**, sélectionnez **personnalisé**, puis sélectionnez toowhen préalable à un jour vous avez téléchargé un stockage tooblob fichier CSV hello. Quand vous avez terminé, cliquez sur **Démarrer**.  


### <a name="check-hello-output"></a>Vérifier la sortie de hello
1. Tâche hello laisser s’exécutée pendant quelques minutes jusqu'à ce que vous voyiez activité Bonjour **analyse** boîte. 

2. Si vous disposez d’un outil que vous utilisez normalement contenu de hello tooexamine de stockage d’objets blob, utilisez ce hello de tooexamine outil `azuresamldemoblob` conteneur. Vous pouvez également le hello Bonjour portail Azure comme suit :

    1. Dans le portail de hello, recherchez hello `samldemo` stockage compte et dans le compte de hello, recherche hello `azuresamldemoblob` conteneur. Vous voyez deux fichiers dans le conteneur de hello : hello du fichier qui contient des tweets d’exemple hello et un fichier CSV généré par la tâche de flux de données Analytique hello.
    2. Fichier de hello généré de droit et sélectionnez **télécharger**. 

   ![Télécharger la sortie CSV du travail à partir du stockage d’objets blob](./media/stream-analytics-machine-learning-integration-tutorial/download-output-csv-file.png)  

3. Ouvrez hello généré un fichier CSV. Vous voyez quelque chose comme hello l’exemple suivant :  
   
   ![Stream Analytics Machine Learning, vue CSV](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-csv-view.png)  


### <a name="view-metrics"></a>Afficher les mesures
Vous pouvez également afficher les mesures liées à la fonction Azure Machine Learning. Hello suit les mesures associées à la fonction est affiché dans hello **analyse** zone dans le panneau de tâche hello :

* **Demandes de fonction** indique le nombre de hello de demandes envoyées tooa service web Machine Learning.  
* **Événements de la fonction** indique le nombre de hello d’événements dans la demande de hello. Par défaut, chaque demande de tooa service web Machine Learning contient too1, 000 événements.  


## <a name="next-steps"></a>Étapes suivantes

* [Introduction tooAzure Analytique de flux de données](stream-analytics-introduction.md)
* [Références sur le langage des requêtes d'Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Intégrer l’API REST et le service Machine Learning](stream-analytics-how-to-configure-azure-machine-learning-endpoints-in-stream-analytics.md)
* [Références sur l’API REST de gestion d’Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)



