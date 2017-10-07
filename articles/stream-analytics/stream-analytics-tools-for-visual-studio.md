---
title: aaaUse Azure flux Analytique Tools pour Visual Studio | Documents Microsoft
description: Didacticiel de mise en route pour hello Azure flux Analytique Tools pour Visual Studio
keywords: visual studio
documentationcenter: 
services: stream-analytics
author: 
manager: 
editor: 
ms.assetid: a473ea0a-3eaa-4e5b-aaa1-fec7e9069f20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 
ms.author: 
ms.openlocfilehash: bda8e548040509a6f29f1b713268bc38f73228fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-stream-analytics-tools-for-visual-studio"></a>Utilisation d’outils Azure Stream Analytics pour Visual Studio
## <a name="introduction"></a>Introduction
Dans ce didacticiel, vous découvrez comment l’Analytique du flux toouse Azure Tools pour Visual Studio toocreate, créer, tester localement, gérer et déboguer vos tâches de flux de données Analytique. 

Après avoir effectué ce didacticiel, vous pourrez :
* bien connaître les outils Stream Analytics pour Visual Studio ;
* configurer et déployer un travail Stream Analytics ;
* tester votre travail en local avec des exemples de données locaux ;
* Analyse des problèmes de tootroubleshoot à utiliser.
* Exporter tooprojects de travaux existants.

## <a name="prerequisites"></a>Composants requis
toocomplete ce didacticiel, vous devez hello suivant des conditions préalables :
* Terminer les étapes hello qui précèdent « Créer une tâche de flux de données Analytique » Bonjour [générer une solution IoT à l’aide du didacticiel de flux de données Analytique](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics). 
* Utilisez Visual Studio 2015, Visual Studio 2013 mise à jour 4 ou Visual Studio 2012. Les éditions Enterprise (Ultimate/Premium), Professional et Community sont prises en charge. L’édition Express n’est pas prise en charge. Visual Studio 2017 n’est pas pris en charge. 
* Hello d’utiliser Azure SDK pour .NET version 2.7.1 ou version ultérieure. Installez-le à l’aide de hello [le programme d’installation de Web platform](http://www.microsoft.com/web/downloads/platform.aspx).
* Installer hello [outils Analytique de flux de données pour Visual Studio](http://aka.ms/asatoolsvs).

## <a name="create-a-stream-analytics-project"></a>Créer un projet Stream Analytics
1. Dans Visual Studio, cliquez sur hello **fichier** menu et sélectionnez **nouveau projet**. 

2. Dans la liste des modèles hello sur hello gauche, sélectionnez **flux Analytique** puis cliquez sur **Application Analytique de flux de données Azure**.

3. Entrez le projet de hello **nom**, **emplacement**, et **nom de la Solution** comme vous le feriez pour d’autres projets.

    ![Fenêtre Nouveau projet](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-01.png)

    Un projet **Toll** est généré dans l’**Explorateur de solutions**.

    ![Projet Toll généré dans l’Explorateur de solutions](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-02.png)

## <a name="choose-hello-correct-subscription"></a>Choisissez l’abonnement approprié de hello
1. Dans Visual Studio, cliquez sur hello **vue** menu et ouvrez **l’Explorateur de serveurs**.

2. Connectez-vous à votre compte Azure. 

## <a name="define-hello-input-sources"></a>Définir des sources d’entrée hello
1.  Dans **l’Explorateur de solutions**, développez hello **entrées** nœud et renommer **Input.json** trop**EntryStream.json**. Double-cliquez sur **EntryStream.json**.
2.  Hello **Alias d’entrée** est désormais **EntryStream**. alias de Hello d’entrée est utilisé dans le script de requête hello. 
3.  Dans **Type de source**, sélectionnez **Data Stream**.
4.  Dans **Source**, sélectionnez **Event Hub**.
5.  Dans **Service Bus Namespace**, sélectionnez hello **TollData** option.
6.  Dans **Nom du hub d’événements**, sélectionnez **entry**.
7.  Dans **nom de la stratégie concentrateur d’événements**, sélectionnez **RootManageSharedAccessKey** (valeur par défaut de hello).
8.  Dans **Format de sérialisation de l’événement**, sélectionnez **Json**. 
9.  Dans **Encodage**, sélectionnez **UTF8**. Vos paramètres doivent ressembler à hello suivant capture d’écran :

    ![Fenêtre Entrée](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-01.png)
 
10. Assistant de hello toofinish, cliquez sur **enregistrer**. Vous pouvez maintenant ajouter un autre flux de sortie hello toocreate source d’entrée. Avec le bouton hello **entrées** nœud et sélectionnez **un nouvel élément**.

    ![Nouvel élément](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-02.png)
 
11. Dans la fenêtre hello, sélectionnez **Azure flux Analytique Entrée**et modifier hello **nom** trop**ExitStream.json**. Cliquez sur **Add**.

    ![Fenêtre Ajouter un nouvel élément](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-03.png)
 
12. Double-cliquez sur **ExitStream.json** hello projet et hello suivent même étapes comme vous l’avez fait pour le flux d’entrée hello. Être vraiment tooenter **quitter** pour hello **nom de Hub d’événements** comme indiqué dans hello suivant capture d’écran :

    ![Fenêtre ExitStream](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-04.png)

    Vous avez maintenant défini deux flux d’entrée de données :

    ![Flux d’entrée et de sortie](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-05.png)
 
    Ensuite, ajoutez des entrées de données de référence pour le fichier blob hello qui contient les données d’inscription de voiture.

13. Avec le bouton hello **entrées** nœud dans le projet de hello, puis hello suivent même étapes comme vous l’avez fait pour les entrées de flux hello. Dans **Alias d’entrée**, entrez **Registration**, et dans **Type de Source**, sélectionnez **Reference data**.

    ![Fenêtre Inscription](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-06.png)

14. Dans **compte de stockage**, sélectionnez hello **tolldata** option. Dans **Conteneur**, sélectionnez **tolldata**, et dans **Modèle de chemin d’accès**, entrez **registration.json**. Ce nom de fichier respecte la casse et doit être en minuscules.
15. Assistant de hello toofinish, cliquez sur **enregistrer**.

Maintenant, toutes les entrées de hello sont définies.

## <a name="define-hello-output"></a>Définir la sortie de hello
1.  Dans **l’Explorateur de solutions**, développez hello **entrées** nœud et double-cliquez sur **Output.json**.

2.  Dans **Alias de sortie**, entrez **output**. 
3.  Dans **Récepteur**, sélectionnez **SQL Database**.
4.  Dans **Base de données**, sélectionnez **TollDataDB**.
5.  Dans **Nom d’utilisateur**, entrez **tolladmin**. 
6.  Dans **Mot de passe**, entrez **123toll!**.
7.  Dans **Table**, entrez **TollDataRefJoin**.
8.  Cliquez sur **Save**.

    ![Fenêtre Sortie](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-output-01.png)
 
## <a name="create-a-stream-analytics-query"></a>Créer une requête Stream Analytics
Ce didacticiel tentatives tooanswer plusieurs questions qui sont des données de tootoll connexes. Il crée également des requêtes de flux de données Analytique qui peuvent être utilisés dans les réponses correspondantes de flux de données Analytique tooprovide.
Avant de commencer votre premier travail Analytique des flux de données, examinons une syntaxe de requête simple scénario et hello.

### <a name="introduction-toohello-stream-analytics-query-language"></a>Introduction toohello langage de requête Analytique de flux de données
Supposons que vous devez toocount hello de véhicules qui permet d’entrer une gare de péage. Cet exemple est un flux continu d’événements, vous devez toodefine une période de temps. Modifier hello toobe de question « Combien de véhicules entrer une gare de péage toutes les trois minutes » ? Cette toocount de manière les données sont souvent appelée tooas hello bascule count.

Examinez la requête de flux de données Analytique hello qui répond à cette question :

        SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count 
        FROM EntryStream TIMESTAMP BY EntryTime 
        GROUP BY TUMBLINGWINDOW(minute, 3), TollId 

Flux de données Analytique utilise un langage de requête tel que SQL et ajoute quelques extensions toospecify liées au temps aspects de hello requête.

Pour plus d’informations, consultez [gestion du temps](https://msdn.microsoft.com/library/azure/mt582045.aspx) et [fenêtrage](https://msdn.microsoft.com/library/azure/dn835019.aspx) constructions utilisées dans la requête hello à partir de MSDN.

Maintenant que vous avez écrit votre première requête Analytique de flux de données, il est temps tootest il. Utilisez les fichiers de données d’exemple hello situés dans le dossier TollApp hello suivant le chemin d’accès :

..\TollApp\TollApp\Data

Ce dossier contient les fichiers suivants de hello :
*   Entry.json
*   Exit.json
*   registration.json

## <a name="count-hello-number-of-vehicles-entering-a-toll-booth"></a>Nombre hello véhicules entrant une gare de péage
Dans le projet de hello, double-cliquez sur **Script.asaql** script hello tooopen hello **l’éditeur de requête**. Copiez et collez le script de hello dans la section précédente de hello dans l’éditeur de hello. Hello éditeur de requête prend en charge IntelliSense, la coloration de syntaxe et erroné hello.

![Éditeur de requête](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-query-01.png)
 
### <a name="test-stream-analytics-queries-locally"></a>Tester localement les requêtes Stream Analytics

1. toocompile hello requête toosee s’il existe une erreur de syntaxe, droit hello projet, puis sélectionnez **Build**. 

2. toovalidate cette requête par rapport à des exemples de données, vous pouvez utiliser les données local. Entrée de hello d’avec le bouton droit, puis sélectionnez **Ajouter entrée locale**.

    ![Ajouter une entrée locale](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-01.png)
 
3. Dans la fenêtre contextuelle de hello, sélectionnez les données d’exemple hello à partir de votre chemin d’accès local. Cliquez sur **Enregistrer**.

    ![Fenêtre Ajouter une entrée locale](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-02.png)
 
    Un fichier nommé **local_EntryStream.json** est automatiquement ajouté le dossier d’entrées tooyour.

    ![Dossier ajouté tooinputs de fichier](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-03.png)
 
4. Bonjour **l’éditeur de requête**, cliquez sur **exécuter localement**. Ou vous pouvez appuyer hello F5.

    ![Exécution locale](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-01.png)

    ![Sortie de l’exécution locale](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-02.png)

    Appuyez sur la touche de sortie de hello tooview clé Bonjour **résultat d’exécution Local ASA** fenêtre dans Visual Studio. 

    ![Fenêtre Résultats de l’exécution locale ASA](./media/stream-analytics-tools-for-vs/local-testing-output.png)

5. Cliquez sur **ouvrir le dossier résultat** des fichiers de sortie de hello toocheck tous deux au format CSV et JSON.

    ![Sortie Ouvrir le dossier des résultats](./media/stream-analytics-tools-for-vs/local-testing-files.png)
 

### <a name="sample-hello-input-data"></a>Exemples de données d’entrée hello
Vous pouvez également des exemples de données d’entrée à partir du fichier local tooa de sources d’entrée. 
1. Cliquez sur le fichier de configuration d’entrée hello, puis sélectionnez **Sample Data**. 

   ![Exemple de données](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-01.png)

    Pour l’instant, vous pouvez uniquement échantillonner le hub d’événements ou le hub IoT. Les autres sources d’entrée ne sont pas prises en charge.

2. Dans la fenêtre contextuelle de hello, entrez hello chemin d’accès local utilisé toosave hello exemples de données. Cliquez sur **Exemple**.

    ![Fenêtre Exemples de données](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-02.png)
 
    Vous pouvez voir la progression hello Bonjour **sortie** fenêtre. 

    ![Fenêtre Sortie](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-03.png)
 
### <a name="submit-a-stream-analytics-query-tooazure"></a>Envoyer un tooAzure de requête Analytique de flux de données
1. Bonjour **l’éditeur de requête**, cliquez sur **envoyer tooAzure** dans l’éditeur de script hello.

    ![Envoyer tooAzure](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-01.png)
 
2. Sélectionnez **Créer une tâche Azure Stream Analytics**. Entrez hello **nom de la tâche**et sélectionnez hello correct **abonnement**. Cliquez sur **Envoyer**.

    ![Fenêtre Envoyer la tâche](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-02.png)

 
### <a name="start-a-job"></a>Démarrer une tâche
Maintenant que votre travail est créé, vue de tâche hello est ouvert automatiquement. 
1. toostart hello des tâches, cliquez sur hello **flèche verte** bouton.

    ![Démarrer une tâche](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-01.png)
 
2. Sélectionnez le paramètre par défaut de hello, puis cliquez sur **Démarrer**.
 
    ![Fenêtre Démarrer une tâche](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-02.png)

    travail de Hello **état** change également**en cours d’exécution**, et **événements d’entrée** et **événements de sortie** s’affichent.

    ![État en cours d’exécution dans Résumé de la tâche](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-03.png)

## <a name="check-hello-results-in-visual-studio"></a>Vérifier les résultats de hello dans Visual Studio
1. Dans Visual Studio, ouvrez **l’Explorateur de serveurs** et avec le bouton hello **TollDataRefJoin** table.
2. Sélectionnez **afficher les données de Table** sortie de hello toosee de votre travail.
   
    ![Sélection de l’option Afficher les données de la table dans l’Explorateur de serveurs](media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-check-results.jpg)


### <a name="view-hello-job-metrics"></a>Métriques de travail vue hello
Certaines statistiques des tâches de base se trouvent dans **Métriques de tâche**. 

![Fenêtre Métriques de tâche](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-metrics-01.png)

 
## <a name="list-hello-job-in-server-explorer"></a>Tâche hello de liste dans l’Explorateur de serveurs
Dans l’**Explorateur de serveurs**, cliquez sur **Tâches Stream Analytics**, puis sur **Actualiser**. travail de Hello apparaît sous **des tâches de flux de données Analytique**.

![Tâches Stream Analytics répertoriées dans l’Explorateur de serveurs](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-list-jobs-01.png)


## <a name="open-hello-job-view"></a>Vue du travail hello ouvert
mode de travail tooopen hello, développez le nœud de votre travail et double-cliquez sur hello **vue des travaux** nœud.

![Nœud Vue de la tâche](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-view-01.png)


## <a name="export-an-existing-job-tooa-project"></a>Exporter un projet tooa de travail existant
Il existe deux façons, vous pouvez exporter un projet tooa de travail existant.

Dans **l’Explorateur de serveurs**, nœud de travail avec le bouton hello Bonjour **des travaux Stream Analytique** nœud et sélectionnez **exporter tooNew flux Analytique projet**.

![Exportation tooNew projet Analytique de flux de données](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-01.png)

projet de Hello est généré dans **l’Explorateur de solutions**.

![Projet généré dans l’Explorateur de solutions](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-02.png)
 
Vous également pourrez utiliser le mode de travail hello, puis cliquez sur **générer le projet**.

![Générer le projet](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-03.png)

## <a name="known-issues-and-limitations"></a>Problèmes connus et limitations
 
- Il n’existe aucune prise en charge pour la sortie Power BI et la sortie d’Azure Date Lake Store.
- Il n’existe aucune prise en charge de l’éditeur pour l’ajout ou la modification de fonctions JavaScript définies par l’utilisateur.

## <a name="next-steps"></a>Étapes suivantes
* [Introduction tooAzure Analytique de flux de données](stream-analytics-introduction.md)
* [Bien démarrer avec Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Mise à l'échelle des travaux Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Références sur le langage des requêtes d'Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Références sur l’API REST de gestion d’Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
