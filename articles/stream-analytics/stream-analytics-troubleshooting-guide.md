---
title: "guide d’aaaTroubleshooting pour l’Analytique des flux de données Azure | Documents Microsoft"
description: "Comment tootroubleshoot votre tâche de flux de données Analytique"
keywords: "Guide de dépannage"
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 4add48054e06a7d8eb617a08595c1be4555c59d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-azure-stream-analytics"></a>Guide de dépannage pour Azure Stream Analytics

Résolution des problèmes du flux de données Analytique Azure peuvent s’afficher toobe un effort complex à première vue. Après avoir travaillé avec de nombreux utilisateurs, nous avoir créé ce guide de processus de hello toohelp simplifiée et supprimer le hasard hello sur vos entrées, les sorties, les requêtes et les fonctions.

## <a name="troubleshoot-your-stream-analytics-job"></a>Résoudre les problèmes liés à votre travail Stream Analytics

Pour de meilleurs résultats dans votre tâche de flux de données Analytique de résolution des problèmes, utilisez hello instructions :

1.  Testez votre connectivité :
    - Vérifiez tooinputs de connectivité et des sorties à l’aide de hello **tester la connexion** bouton pour chaque entrée et sortie.

2.  Examinez vos données d’entrée :
    - tooverify que les données d’entrée est transférée dans le concentrateur d’événements, utilisez [Explorateur Service Bus](https://code.msdn.microsoft.com/windowsapps/Service-Bus-Explorer-f2abca5a) tooconnect tooAzure concentrateur d’événements (si l’entrée de concentrateur d’événements est utilisée).  
    - Hello d’utilisation [ **Sample Data** ](stream-analytics-sample-data-input.md) bouton pour chaque entrée et télécharger les données d’exemple d’entrée de hello.
    - Inspecter hello exemple données toounderstand hello forme des données de salutation : hello schéma et hello [des types de données](https://msdn.microsoft.com/library/azure/dn835065.aspx).

3.  Testez votre requête :
    - Sur hello **requête** utiliser hello, onglet **Test** bouton requête de hello tootest et utiliser les données d’exemple hello téléchargé trop[tester la requête hello](stream-analytics-test-query.md). Examinez les erreurs et tenter de toocorrect les.
    - Si vous utilisez [ **Timestamp By**](https://msdn.microsoft.com/library/azure/mt573293.aspx), vérifiez que les événements hello horodateurs supérieur hello [heure de début de la tâche](stream-analytics-out-of-order-and-late-events.md).

4.  Déboguez votre requête :
    - Reconstruire la requête hello progressivement à partir d’agrégats complexes de toomore instruction select simple à l’aide des étapes. toobuild logique de requête hello étape par étape, utilisez [WITH](https://msdn.microsoft.com/library/azure/dn835049.aspx) clauses.
    - Utilisez [SELECT INTO](stream-analytics-select-into.md) toodebug étapes de la requête.

5.  Éliminez les pièges les plus courants, comme par exemple :
    - A [ **où** ](https://msdn.microsoft.com/library/azure/dn835048.aspx) clause de la requête de hello filtrées de tous les événements, empêchant toute sortie d’être générée.
    - Lorsque vous utilisez des fonctions de fenêtre, attendez toosee de durée de fenêtre entière hello une sortie à partir de la requête de hello.
    - horodatage Hello pour les événements précède l’heure de début de tâche hello et, par conséquent, les événements sont en cours de suppression.

6.  Utilisez l’ordre des événements :
    - Si tous les hello fonctionnés des étapes précédentes, accédez à toohello **paramètres** panneau et sélectionnez [ **l’ordre des événements**](stream-analytics-out-of-order-and-late-events.md). Vérifiez que cette stratégie est configurée pour s’intégrer logiquement à votre scénario. stratégie de Hello est *pas* appliqué lorsque vous utilisez hello **Test** requête de bouton tootest hello. Le résultat est une différence entre le test dans un navigateur et en cours d’exécution des travaux de hello en production.

7.  Déboguez la requête à l’aide de métriques :
    - Si vous ne disposez d’aucune sortie après que hello attendu (basée sur la requête de hello) de durée, essayez suivante de hello :
        - Examinez [ **mesures de surveillance** ](stream-analytics-monitoring.md) sur hello **moniteur** onglet. Étant donné que les valeurs hello sont agrégées, les métriques de hello sont retardés en quelques minutes.
            - Si les événements d’entrée > 0, la tâche de hello est en mesure de tooread des données d’entrée. Si le nombre d’événements d’entrée est nul, alors :
                - toosee si la source de données hello comporte des données valides, intégrez-le à l’aide de [Explorateur Service Bus](https://code.msdn.microsoft.com/windowsapps/Service-Bus-Explorer-f2abca5a). Cette vérification s’applique si le travail de hello est à l’aide de concentrateur d’événements en tant qu’entrée.
                - Vérifiez toosee si le format de sérialisation des données hello et codage de données sont normalement.
                - Si le travail de hello est à l’aide d’un concentrateur d’événements, vérifiez toosee si le corps de message de type hello hello est *Null*.
            - Si des erreurs de Conversion de données > 0 et escalade, suivant de hello peut être vrai :
                - travail de Hello peut ne pas être en mesure de toode-sérialiser les événements hello.
                - Hello schéma d’événement peut ne pas correspondre au hello défini ou schéma attendu d’événements hello dans la requête de hello.
                - Hello des types de données de certains champs hello dans les événements hello ne peut pas correspondre aux attentes.
            - Si des erreurs d’exécution > 0, cela signifie que le travail hello peut recevoir des données de hello mais génère des erreurs lors du traitement de requête de hello.
                - erreurs de hello toofind, accédez toohello [les journaux d’Audit](../azure-resource-manager/resource-group-audit.md) et filtrer sur *n’a pas pu* état.
            - Si InputEvents > 0 et OutputEvents = 0, cela signifie que hello suivantes est vraie :
                - Le traitement de la requête a abouti à un nombre nul d’événements de sortie.
                - Les événements ou leurs champs peuvent être formés de manière inappropriée et n’entraîner aucune sortie après le traitement des requêtes.
                - tâche de Hello était impossible toopush données toohello [récepteur de sortie](stream-analytics-select-into.md) pour des raisons de connectivité ou d’authentification.
        - Dans tous les hello mentionné précédemment cas d’erreur, les opérations des messages de journal décrivent d’autres aspects (y compris ce qui se passe), sauf dans les cas où la logique de requête hello filtrée tous les événements. Si le traitement de plusieurs événements hello génère des erreurs, Analytique de flux de journaux hello trois premiers messages d’erreur de hello même type dans les 10 minutes tooOperations se connecte. Il supprime ensuite toutes les autres erreurs identiques avec un message indiquant que les erreurs survenant trop rapidement sont supprimées.

8. Débogage à l’aide des journaux de diagnostic et d’audit :
    - Utilisez [les journaux d’Audit](../azure-resource-manager/resource-group-audit.md)et les erreurs du filtre de tooidentify et de débogage.
    - Utilisez [journaux de diagnostic de la tâche](stream-analytics-job-diagnostic-logs.md) tooidentify et débogage des erreurs.

9. Examinez les sorties hello :
    - Lorsque le statut de la tâche hello est *en cours d’exécution*, selon la durée hello stipulée dans la requête de hello, vous pouvez voir la sortie de hello dans la source de données récepteur hello.
    - Si vous ne voyez pas les sorties qui vont type de sortie spécifique de tooa, rediriger les type de sortie tooan qui est moins complexe, par exemple un objet Blob Azure. À l’aide de l’Explorateur de stockage, vérifiez toosee si la sortie de hello peut être consulté. En outre, vérifiez si des limites de limitation à la sortie de hello empêchent les données reçues.

10. Utilisez l’analyse de flux de données avec les métriques du diagramme de travail :
    - flux de données de la tooanalyze et identifier les problèmes, utilisez hello [diagramme de travail avec les mesures](stream-analytics-job-diagram-with-metrics.md).

11. Créez une demande de support :
    - Enfin, si tout le reste échoue, ouvrez une demande de support Microsoft à l’aide de hello SubscriptionID qui contient votre travail.

## <a name="get-help"></a>Obtenir de l’aide

Pour obtenir une assistance, consultez le [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Étapes suivantes

* [Introduction tooAzure Analytique de flux de données](stream-analytics-introduction.md)
* [Prise en main d’Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Mise à l'échelle des travaux Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Références sur le langage des requêtes d'Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Références sur l’API REST de gestion d’Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
