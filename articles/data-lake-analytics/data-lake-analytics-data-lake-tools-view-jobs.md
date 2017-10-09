---
title: "aaaUse navigateur de travail et de la vue des travaux pour les travaux de l’Analytique de LAC de données Azure | Documents Microsoft"
description: "Découvrez comment toouse navigateur de travail et de la vue des travaux pour les travaux de l’Analytique de LAC de données Azure. "
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: bdf27b4d-6f58-4093-ab83-4fa3a99b5650
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/02/2017
ms.author: jgao
ms.openlocfilehash: c45e618426808349ca380b1bcfaefd4c947ce7ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-job-browser-and-job-view-for-azure-data-lake-analytics-jobs"></a>Utilisation de l’Explorateur de travaux et la Vue des travaux pour les travaux Azure Data Lake Analytics
Analytique de LAC de données Azure service archives Hello soumis des travaux dans un [magasin de requêtes](#query-store). Dans cet article, vous découvrez comment toouse navigateur de projet et affichage du travail dans Azure Data Lake Tools pour hello de toofind Visual Studio historique de la tâche d’informations. 

Par défaut, hello service de données Lake Analytique archive les travaux hello pendant 30 jours. période d’expiration de Hello peut être configuré à partir de hello portail Azure en configurant la stratégie d’expiration de hello personnalisé. Vous ne serez pas en mesure de tooaccess informations sur les travaux hello après expiration. 

## <a name="prerequisites"></a>Composants requis
Voir [Data Lake Tools for Visual Studio - Composants requis](data-lake-analytics-data-lake-tools-get-started.md#prerequisites).

## <a name="open-hello-job-browser"></a>Ouvrez hello navigateur de travail
Accès hello navigateur travail via **l’Explorateur de serveurs > Azure > Analytique lac de données > travaux** dans Visual Studio.  Hello navigateur de travail, vous pouvez accéder aux magasin de requêtes hello d’un compte Analytique lac de données. Navigateur de travail affiche le magasin de requêtes sur hello gauche, informations sur les travaux de base et vue des travaux sur l’affichage de droite hello détaillées des informations sur les travaux.

## <a name="job-view"></a>Vue des travaux
Vue montre hello des informations détaillées d’un travail de la tâche. tooopen un travail, vous pouvez double-cliquez sur une tâche Bonjour navigateur de projet ou ouvrez à partir du menu de Data Lake hello en cliquant sur la vue des travaux. Vous devez voir une boîte de dialogue renseignée avec l’URL de tâche hello.

![Data Lake Tools pour Visual Studio - Explorateur de travaux](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-view.png)

La Vue des travaux contient les éléments suivants :

* Résumé des tâches
  
    Hello vue des travaux d’actualisation toosee hello les informations les plus récentes des travaux en cours d’exécution.
  
  * Statut de tâche (graphique) :
    
      État de la tâche présente les phases de travail hello :
    
      ![Azure Data Lake Analytics - Statut des phases du travail](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-phases.png)
    
    * Préparation : Téléchargez votre cloud toohello de script, la compilation et l’optimisation de script hello à l’aide du service de compilation hello.
    * En attente : Les travaux sont en file d’attente lactosérum qu’ils sont en attente suffisamment de ressources ou les travaux hello dépassent travaux simultanés de hello max par limitation de votre compte. paramètre de priorité Hello détermine la séquence hello des travaux en file d’attente - hello hello inférieure, une priorité plus élevée hello hello.
    * En cours d’exécution : tâche de hello est réellement en cours d’exécution dans votre compte Analytique lac de données.
    * Finalisation : fin du travail de hello (par exemple, la finalisation de fichier de hello).
      
      travail de Hello peut échouer dans chaque phase. Par exemple, les erreurs de compilation dans la phase de préparation hello, erreurs de délai d’attente dans la phase de hello en file d’attente et les erreurs d’exécution dans la phase en cours d’exécution de hello, etc..
  * Informations de base
    
      informations de base de tâche Hello s’affiche dans la partie inférieure de hello du Panneau de résumé de la tâche hello.
    
      ![Azure Data Lake Analytics - Statut des phases du travail](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-info.png)
    
    * Résultat du travail : A réussi ou a échoué. tâche de Hello peut échouer dans chaque phase.
    * Durée totale : temps écoulé (durée) entre l’heure de soumission et l’heure de fin.
    * Durée totale de calcul : somme hello chaque sommet de durée d’exécution, vous pouvez envisager qu'il est exécuté comme hello heure à laquelle cette tâche hello dans uniquement un sommet. Consultez tooTotal sommets toofind plus d’informations sur les sommets.
    * Heure de soumission/début/fin : heure hello lorsque hello service de données Lake Analytique reçoit hello de toorun/démarrage de l’envoi de travail/Fin travail de hello correctement ou non.
    * Compilation en file d’attente/en cours d’exécution : Durée totale d’exécution est passée au cours de la phase de préparation en file d’attente/en cours d’exécution hello.
    * : Hello Analytique lac de données compte utilisé pour exécuter le travail de hello.
    * Auteur : hello utilisateur envoyé hello travail, il peut être le compte d’une personne réelle ou un compte système.
    * Priorité : priorité de hello du travail de hello. Hello hello numéro inférieur, une priorité plus élevée hello hello. Il affecte uniquement la séquence hello de travaux de hello dans la file d’attente hello. Définir une priorité plus élevée n’accélère pas les travaux en cours d’exécution.
    * Parallélisme : hello a demandé un nombre maximal simultanées Azure Lake Analytique des unités de données (ADLAUs), également appelé sommets. Actuellement, un sommet est égal tooone machine virtuelle avec deux cœurs virtuels et six Go de RAM, bien que cela peut être mis à niveau dans les futures Analytique lac de données mises à jour.
    * Octets de gauche : Des octets toobe traité tant que hello tâche se termine.
    * Octets lus/écrits : octets qui ont été lus/écrits depuis le démarrage en cours d’exécution du travail de hello.
    * Nombre total de sommets : tâche de hello est divisé en plusieurs éléments de travail, chaque élément de travail est appelé un sommet. Cette valeur décrit le travail de hello combien éléments de travail se compose de. Vous pouvez considérer un vertex comme une unité de processus de base, également appelée Azure Data Lake Analytics Unit (ADLAU), et les vertex peuvent être exécutés dans un parallélisme. 
    * S’est terminée en cours d’exécution/Échec : hello nombre de sommets de terminée ou d’en cours d’exécution/échec. Sommets peuvent échouer en raison de pannes du système et de code utilisateur tooboth, mais échec de tentatives de système hello sommets automatiquement plusieurs fois. Si les sommets hello sont toujours en échec après une nouvelle tentative, l’ensemble du projet hello échoue.
* Graphique du travail
  
    Un script U-SQL représente hello une logique de transformation des données toooutput de données d’entrée. script de Hello est compilée et optimisée du plan d’exécution physique tooa au niveau de la phase de préparation hello. Graphique de travail est un plan d’exécution physique tooshow hello.  Hello suivant schéma illustre les processus hello :
  
    ![Azure Data Lake Analytics - Statut des phases du travail](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-logical-to-physical-plan.png)
  
    Un travail est divisé en plusieurs éléments. Chaque élément est appelé un vertex. les sommets Hello sont regroupés en tant que Super sommets (également appelé phase) et affichées sous la forme graphique du travail. plaquettes de scène vert Hello dans le graphique de travail hello indiquent les étapes hello.
  
    Chaque sommet d’une étape fait hello même type de travailler avec des différents éléments de hello même données. Par exemple, si vous disposez d’un fichier contenant un To de données et des centaines de vertex à lire, chaque vertex lit un bloc de données. Ces derniers sont regroupés dans hello même étape et faire de même fonctionnent sur différentes parties du même fichier d’entrée.
  
  * <a name="state-information"></a>Informations sur la phase
    
      Dans une étape spécifique, des nombres sont affichés dans le résumé de hello.
    
      ![Azure Data Lake Analytics - Phase du graphique du travail](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-graph-stage.png)
    
    * SV1 Extraire : nom hello d’une étape, nommée par une méthode d’opération numéro et hello.
    * 84 sommets : hello nombre total de sommets dans cette étape. la figure Hello indique le nombre d’éléments de travail est divisé dans cette étape.
    * 12.90 de vertex/s : hello des temps d’exécution moyen de sommets pour cette étape. Ce chiffre est calculé à l’aide de la fonction SUM (temps d’exécution de chaque vertex)/(nombre de vertex). Ce qui signifie que si vous pouvez attribuer tous les sommets hello exécutées dans le parallélisme, hello entière est terminé dans 12.90 s. Cela signifie également que si tous les hello travail dans cette étape est effectuée en série, hello coût serait #vertices * temps de réponse moyen.
    * 850 895 lignes écrites : nombre total de lignes écrites au cours de cette phase.
    * R/W : quantité de données lues/écrites au cours de cette phase, en octets.
    * Couleurs : Les couleurs sont utilisées dans l’état de différents sommets tooindicate l’étape hello.
      
      * Vert indique les sommets hello sont réussi.
      * Orange indique les sommets hello sont retentée. les sommets Hello retentée a échoué, mais sont tentée à nouveau automatiquement et correctement par hello système hello global est terminé avec succès. Si les sommets hello retenté mais échoue encore, couleur de hello devient rouge et hello ensemble du projet a échoué.
      * Rouge indique un échec, ce qui signifie que certaines un sommet avait été retentée plusieurs fois par le système de hello mais toujours a échoué. Ce scénario provoque toofail d’ensemble du projet hello.
      * Bleu signifie qu’un vertex est en cours d’exécution.
      * Blanc indique hello sommet est en attente. les sommets Hello peuvent être toobe en attente planifiée une fois qu’un ADLAU est disponible, ou elle peut être en attente pour l’entrée, car ses données d’entrée n’est peut-être pas prêtes.
      
      Vous trouverez plus de détails pour l’étape de hello en plaçant le curseur de la souris par un état :
      
      ![Azure Data Lake Analytics - Détails de la phase du graphique du travail](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-graph-stage-details.png)
  * Sommets : Décrit les hello sommets plus d’informations, par exemple, le nombre de sommets au total, le nombre de sommets ont été effectuées, sont elles a échoué ou est toujours en attente en cours d’exécution, etc..
  * Lecture des données dans un ou plusieurs pods : les fichiers et les données sont stockés dans plusieurs pods dans un système de fichiers distribués. valeur Hello ici décrit la quantité de données a été lue hello même les zones ou cross-pod.
  * Nombre total de temps de calcul : somme de hello de chaque exécution de sommets dans la phase de hello, vous pouvez le considérer comme hello temps si tout le travail dans la phase de hello est exécuté dans uniquement un sommet.
  * Données et les lignes écrites/lecture : indique la quantité données ou les lignes ont été lus/écrits, ou doivent toobe lire.
  * Échecs de lecture de vertex : indique le nombre de vertex qui ont échoué lors de la lecture de données.
  * Ignore les sommets en double : si un sommet s’exécute trop lentement, système de hello peut planifier plusieurs sommets toorun hello même élément de travail. Les sommets reductant seront supprimées une fois les sommets hello se terminent avec succès. Sommet en double ignore le nombre de hello d’enregistrements de sommets sont ignorées en tant que doublons dans la phase de hello.
  * Révocations de sommets : les sommets hello a réussi, mais obtenir réexécuter ultérieurement en raison des raisons de toosome. Par exemple, si en aval sommet perd des données d’entrée intermédiaire, il demandera hello vertex en amont toorerun.
  * Exécutions de planification de sommets : durée totale hello les sommets hello ont été planifiées.
  * Lecture de données moyenne/Min/Max sommets : hello minimale/moyenne/maximale de chaque sommet lire les données.
  * Durée : hello durée totale d’exécution que prend d’une étape, vous devez tooload profil toosee cette valeur.
  * Lecture de travail
    
      Analytique de LAC de données exécute les travaux et les archives hello sommets en cours d’exécution d’informations de travaux hello, par exemple lorsque les sommets hello sont démarrés, arrêtés, a échoué et comment ils sont retentées, etc.. Toutes les informations de hello est automatiquement enregistré dans le magasin de requêtes hello et stockée dans son profil de travail. Vous pouvez télécharger hello profil de travail via « Profil de charge » dans la vue des travaux, et vous pouvez afficher hello lecture de la tâche après avoir téléchargé hello profil de travail.
    
      Lecture de la tâche est une visualisation parfaite illustration des sites, ce qui est arrivé dans le cluster de hello. Elle vous permet de surveiller la progression de l'exécution du travail et de détecter visuellement les anomalies de performance et les goulots d'étranglement très rapidement (moins de 30 s généralement).
  * Affichage du tableau (Heat Map) du travail 
    
      Carte thermique des travaux peut être sélectionné via la liste déroulante hello affichage graphique de la tâche. 
    
      ![Azure Data Lake Analytics - Tableau du graphique du travail](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-graph-heat-map-display.png)
    
      Il affiche la carte de chaleur hello d’e/s, temps et le débit d’une tâche, par le biais duquel vous pouvez rechercher où le travail de hello consacre à la plupart du temps de hello, ou si votre projet est un travail de la limite d’e/s et ainsi de suite.
    
      ![Azure Data Lake Analytics - Exemple de tableau du graphique du travail](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-graph-heat-map-example.png)
    
    * Progression : hello la progression de l’exécution de travaux, voir les informations de [plus d’informations à l’étape](#stage-information).
    * Les données en lecture/écriture : carte thermique hello du total des données en lecture/écriture à chaque étape.
    * Temps de calcul : hello carte thermique de somme (heure de l’exécution chaque sommet), vous pouvez considérer ceci la durée pendant laquelle il faudrait si tout le travail dans la phase de hello est exécuté avec les 1 uniquement sommets.
    * Durée moyenne d’exécution par nœud : carte thermique hello de somme (heure de l’exécution chaque sommet) / (nombre de sommets). Ce qui signifie que si vous pouvez attribuer tous les sommets hello exécutées dans le parallélisme, ensemble de la scène hello est effectuée dans ce laps de temps.
    * Débit d’entrée/sortie : hello carte thermique de débit d’entrée/sortie de chaque étape, vous pouvez vérifier si votre travail est une tâche liée d’e/s via ce.
* Opérations sur les métadonnées
  
    Vous pouvez effectuer certaines opérations sur les métadonnées dans votre script SQL-U, notamment créer une base de données, supprimer une table, etc. Ces opérations sont affichées dans Opération sur les métadonnées après compilation. Vous pouvez rechercher des assertions, créer des entités, ou déposer ici des entités.
  
    ![Azure Data Lake Analytics - Opérations sur les métadonnées dans la Vue des travaux](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-view-metadata-operations.png)
* Historique de l'état
  
    Hello historique de l’état est également affichée dans le résumé de la tâche, mais vous pouvez obtenir plus de détails ici. Vous pouvez trouver hello détaillée des informations telles que lorsque le travail de hello a été préparé, en file d’attente, démarré, s’est terminée. Vous pouvez également rechercher combien de fois le travail de hello a été compilé (hello CcsAttempts : 1), lorsque est réellement cluster de hello travail distribué toohello (hello détail : la distribution toocluster de travail), etc..
  
    ![Azure Data Lake Analytics - Historique de l’état dans la Vue des travaux](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-view-state-history.png)
* Diagnostics
  
    outil de Hello permet de diagnostiquer automatiquement l’exécution du travail. Vous recevrez des alertes lorsqu'il y a des erreurs ou des problèmes de performances dans vos travaux. Notez que vous devez toodownload profil tooget complètes informations ici. 
  
    ![Azure Data Lake Analytics - Diagnostics dans la Vue des travaux](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-view-diagnostics.png)
  
  * Avertissement : une alerte apparaît ici avec un avertissement du compilateur. Vous pouvez cliquer sur « x ou les problèmes » lien toohave plus de détails une fois hello alerte s’affiche.
  * Exécution trop longue du vertex : si un vertex expire (par exemple, après 5 heures), les problèmes sont décrits ici.
  * Utilisation des ressources : si vous avez alloué trop ou pas assez de parallélisme que nécessaire, les problèmes sont décrits ici. Également vous pouvez cliquez sur toosee de l’utilisation des ressources plus d’informations et effectuer des scénarios toofind une meilleure allocation de ressources (pour plus d’informations, consultez ce guide).
  * Vérification de la mémoire : si un vertex utilise plus de 5 Go de mémoire, les problèmes sont décrits ici. L’exécution du travail peut être annulée par le système s’il utilise davantage de mémoire que la limitation du système.

## <a name="job-detail"></a>Détail du travail
Détail du travail affiche hello des informations détaillées de tâche hello, y compris la vue de l’exécution de sommets, de ressources et de Script.

![Azure Data Lake Analytics - Détail du travail](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-details.png)

* Script
  
    Hello script U-SQL de la tâche de hello est stocké dans le magasin de requêtes hello. Vous pouvez afficher le script U-SQL d’origine de hello et nouveau il si nécessaire.
* Ressources
  
    Vous pouvez trouver des sorties de compilation hello travail stockés dans le magasin de requêtes hello via des ressources. Par exemple, vous pouvez rechercher « algebra.xml » est utilisé tooshow hello travail graphique, les assemblys hello que vous vous êtes inscrit, etc. ici.
* Vue d’exécution du vertex
  
    Affiche des détails sur l’exécution des vertex. chaque journal d’exécution de sommets, telles que les données total en lecture/écriture, exécution, état, etc. les archives Hello profil de travail. Dans cette vue, vous pouvez obtenir plus d’informations sur la façon dont un travail a été exécuté. Pour plus d’informations, consultez [hello d’utilisation vue de l’exécution de sommets dans Data Lake Tools pour Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).

## <a name="next-steps"></a>Étapes suivantes
* toolog des informations de diagnostic, consultez [l’accès aux journaux de diagnostic pour l’Analytique de LAC de données Azure](data-lake-analytics-diagnostic-logs.md)
* toosee une requête plus complexe, consultez [site Web d’analyse se connecte à l’aide d’Analytique de LAC de données Azure](data-lake-analytics-analyze-weblogs.md).
* vue de l’exécution de sommets toouse, consultez [hello d’utilisation vue de l’exécution de sommets dans Data Lake Tools pour Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md)

