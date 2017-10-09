---
title: "aaaUse hello vue de l’exécution de sommets dans Data Lake Tools pour Visual Studio | Documents Microsoft"
description: "Découvrez comment toouse hello travaux de vue de l’exécution de sommets tooexam Analytique lac de données."
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 5366d852-e7d6-44cf-a88c-e9f52f15f7df
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/13/2016
ms.author: jgao
ms.openlocfilehash: fb54d2af8a32aa27a54ff50a73c1b4903677a21e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-vertex-execution-view-in-data-lake-tools-for-visual-studio"></a>Utilisez hello vue de l’exécution de sommets dans Data Lake Tools pour Visual Studio
Découvrez comment toouse hello travaux de vue de l’exécution de sommets tooexam Analytique lac de données.

## <a name="prerequisites"></a>Composants requis

Vous avez besoin d’une connaissance élémentaire à l’aide des outils lac de données pour le script toodevelop U-SQL de Visual Studio.  Consultez [Didacticiel : Développer des scripts U-SQL avec Data Lake Tools pour Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).

## <a name="open-hello-vertex-execution-view"></a>Ouvrez hello vue de l’exécution de sommets
Ouvrez une tâche U-SQL dans Data Lake Tools pour Visual Studio. Cliquez sur **vue de l’exécution de sommets** dans hello bas à gauche. Vous pouvez être invité à tooload profils tout d’abord, et elle peut prendre un certain temps en fonction de la connectivité réseau.

![Vue d’exécution du vertex Data Lake Analytics Tools](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-open-vertex-execution-view.png)

## <a name="understand-vertex-execution-view"></a>Présentation de la vue d’exécution du vertex
Hello, vue de l’exécution de sommets comprend trois parties :

![Vue d’exécution du vertex Data Lake Analytics Tools](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view.png)

Hello **sélecteur de sommets** sur permet de gauche hello vous sélectionnez les sommets par les fonctionnalités (telles que les premières 10 données lire, ou choisissez par étape). Un des filtres de hello plus couramment utilisées est toosee hello **sommets sur le chemin critique**. Hello **chemin d’accès critique** est hello plus longue séquence de sommets d’un travail U-SQL. Chemin d’accès critique de présentation hello est utile pour optimiser vos travaux en vérifiant les sommets prend plus longtemps hello.
  
![Vue d’exécution du vertex Data Lake Analytics Tools](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane2.png)

volet en haut au centre de Hello affiche hello **état de tous les sommets hello en cours d’exécution**.
  
![Vue d’exécution du vertex Data Lake Analytics Tools](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane3.png)

volet central de bas Hello affiche des informations sur chaque sommet :
* : Processus hello nom d’instance de sommets hello. Il est composé de différentes parties de StageName|VertexName|VertexRunInstance. Par exemple, sommet de .v1 [62] hello SV7_Split signifie hello deuxième instance d’exécution (.v1, index à partir de 0) du nombre de sommets 62 dans étape SV7_Split.
* Lecture de données total/écrit : les données de salutation a été lus/écrits par ce vertex.
* État de l’état/sortie : hello état final lorsque les sommets hello sont terminée.
* Type/Échec du Code de sortie : hello lors de sommet de hello a échoué.
* Raison de la création : Pourquoi les sommets hello a été créé.
* Temps de latence de file d’attente de ressources latence/processus latence/PN : hello durée de toowait de sommets hello pour les ressources, les données tooprocess et toostay dans la file d’attente hello.
* GUID du processus/créateur : GUID vertex en cours d’exécution actuel de hello ou son créateur.
* Version : instance de hello N-th Hello vertex en cours d’exécution (hello système peut-être planifier des instances d’un sommet pour nombreuses raisons, par exemple le basculement, de calcul redondance, etc..)
* Heure de création de la version.
* Créer début processus d’exécution en file d’attente/processus de l’heure début heure/processus terminé de traiter temps : lorsque le processus de sommets hello démarre la création ; début du processus de sommet de hello tooqueue ; Lorsque hello certains processus de sommets démarre ; Lorsque hello certains sommets est terminée.

## <a name="next-steps"></a>Étapes suivantes
* toolog des informations de diagnostic, consultez [l’accès aux journaux de diagnostic pour l’Analytique de LAC de données Azure](data-lake-analytics-diagnostic-logs.md)
* toosee une requête plus complexe, consultez [site Web d’analyse se connecte à l’aide d’Analytique de LAC de données Azure](data-lake-analytics-analyze-weblogs.md).
* Détails de la tâche tooview, consultez [navigateur de travail d’utilisation et de la vue des travaux pour les travaux de l’Analytique de LAC de données Azure](data-lake-analytics-data-lake-tools-view-jobs.md)
