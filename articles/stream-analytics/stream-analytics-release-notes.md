---
title: aaaStream Notes de publication Analytique | Documents Microsoft
description: Notes de publication de Stream Analytics
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 5e59f893-cd2c-43fb-9eca-c146ce637203
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 05/03/2017
ms.author: jeffstok
ms.openlocfilehash: 1426ebc260be19fbde60518b25501fe53d908d46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-release-notes"></a>Notes de publication de Stream Analytics

## <a name="notes-for-06142017-update-of-stream-analytics-tools-for-visual-studio"></a>Notes relatives à la mise à jour du 14/06/2017 d’Azure Stream Analytics Tools pour Visual Studio
Cette mise à jour est destinée à nos outils Visual Studio Tools. Cette version contient hello nouvelles fonctions suivantes.

| Intitulé | Description |
| --- | --- |
| Prise en charge de l’éditeur de script Java |Vous pouvez profiter hello java natif script editor après avoir créé votre java de fonctions de script.|
| Afficher un message d’erreur d’exécution du travail | S’il existe des erreurs d’exécution pendant l’exécution du travail, vous pouvez les afficher dans l’onglet erreurs de hello en ajustant la fenêtre de temps d’affichage hello. Par défaut, il affiche les messages d’erreur hello pour les 30 dernières minutes. |
| Prise en charge CSV et Avro du test local de l’entrée | Outre le format JSON, vous pouvez à présent utiliser les formats de fichiers CSV et Avro pour le test local de l’entrée.|

## <a name="notes-for-05032017-update-of-stream-analytics"></a>Notes relatives à la version du 03/05/2017 de Stream Analytics
Cette mise à jour concerne la publication de notre documentation de résolution des problèmes.

Hello [guide de dépannage](stream-analytics-troubleshooting-guide.md) et autres documents ont été publiées. Nous vous invitons à les consulter et à nous faire part de vos commentaires.

## <a name="notes-for-04242017-update-of-stream-analytics-tools-for-visual-studio"></a>Notes relatives à la mise à jour du 24/04/2017 d’Azure Stream Analytics Tools pour Visual Studio
Cette mise à jour est destinée à nos outils Visual Studio Tools. Cette version contient hello nouvelles fonctions suivantes.

| Intitulé | Description |
| --- | --- |
| Afficher le résultat du test local dans Visual Studio | résultat de sortie tooview hello Hello local de test, appuyez sur entrée dans la fenêtre de console hello sortie ou de le fermer. résultat de Hello s’affichera dans une fenêtre dans Visual Studio dans un tableau. |
| Résultat local de sortie au format JSON | Lorsque vous exécutez un test local, le résultat de sortie hello sera généré comme JSON et CSV des formats de fichier. |
| Afficher un aperçu des données d’entrées/de sorties du stockage d’objets Blob/Table | En double-cliquant sur un stockage blob ou une table d’entrée/sortie dans la vue de tâche hello, vous pouvez afficher un aperçu données hello dans Visual Studio très facilement. |
| Afficher les messages d’erreur des entrées/sorties | S’il existe une tâche de runtime erreurs connexes tooyou entrées ou des sorties, il sera affiché sur le diagramme de travail hello où vous pouvez pointer dessus message d’erreur détaillé toosee hello.|


## <a name="notes-for-02012017-release-of-stream-analytics"></a>Notes relatives à la version du 01/02/2017 de Stream Analytics
Cette version contient hello mise à jour suivante.

| Intitulé | Description |
| --- | --- |
| Présentation des fonctions JavaScript définies par l’utilisateur |Des [fonctions Java définies par l’utilisateur](stream-analytics-javascript-user-defined-functions.md) sont désormais disponibles pour offrir davantage de souplesse lors de la création de requêtes. |
| Présentation des outils pour Visual Studio et Stream Analytics |Des [outils pour Visual Studio](stream-analytics-tools-for-visual-studio.md) sont désormais disponibles pour le débogage et d’autres fonctions utiles. |
| Présentation de la journalisation des diagnostics |La [journalisation des diagnostics](stream-analytics-job-diagnostic-logs.md) propose des options de dépannage supplémentaires. |
| Présentation des fonctions géospatiales |Des [fonctions géospatiales](http://msdn.microsoft.com/library/mt778980(Azure.100).aspx) sont désormais disponibles. |

## <a name="notes-for-04152016-release-of-stream-analytics"></a>Notes pour la version 04/15/2016 de Stream Analytics 
Cette version contient hello mise à jour suivante.

| Intitulé | Description |
| --- | --- |
| Disponibilité générale pour les sorties Power BI |[sorties Power BI](stream-analytics-power-bi-dashboard.md) sont désormais mises à la disposition générale. expiration de l’autorisation de 90 jours Hello pour Power BI a été supprimée. Pour plus d’informations sur les scénarios où l’autorisation doit toobe renouvelé voir hello [renouveler l’autorisation](stream-analytics-power-bi-dashboard.md#renew-authorization) section de la création d’un tableau de bord Power BI. |

## <a name="notes-for-03032016-release-of-stream-analytics"></a>Notes relatives à la version du 03/03/2016 de Stream Analytics
Cette version contient hello mise à jour suivante.

| Intitulé | Description |
| --- | --- |
| Nouveaux éléments du langage de requête Stream Analytics |SAQL dispose désormais des expressions [GetType](https://msdn.microsoft.com/library/azure/mt643890.aspx "GetType MSDN Page"), [TRY_CAST](https://msdn.microsoft.com/library/azure/mt643735.aspx "TRY_CAST MSDN Page") et [REGEXMATCH](https://msdn.microsoft.com/library/azure/mt643891.aspx "REGEXMATCH MSDN Page"). |

## <a name="notes-for-12102015-release-of-stream-analytics"></a>Notes relatives à la version du 10/12/2015 de Stream Analytics
Cette version contient hello mise à jour suivante.

| Intitulé | Description |
| --- | --- |
| Mise à jour de la version de l’API REST |version d’API REST Hello a été mis à jour too2015-10-01. Vous trouverez plus d’informations sur MSDN à l’adresse [Références d’API REST de gestion Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx) et [Intégration de Machine Learning dans Stream Analytics](stream-analytics-how-to-configure-azure-machine-learning-endpoints-in-stream-analytics.md). |
| Intégration d’Azure Machine Learning |Cette version s’accompagne de la prise en charge des fonctions Azure Machine Learning définies par l’utilisateur. Consultez hello [didacticiel](stream-analytics-machine-learning-integration-tutorial.md) pour plus d’informations ainsi hello [annonce du blog général](http://blogs.technet.com/b/machinelearning/archive/2015/12/10/apply-azure-ml-as-a-function-in-azure-stream-analytics.aspx). |

## <a name="notes-for-11122015-release-of-stream-analytics"></a>Notes relatives à la version du 12/11/2015 de Stream Analytics
Cette version contient hello mise à jour suivante.

| Intitulé | Description |
| --- | --- |
| Nouveau comportement de SELECT |Sélectionnez dans le flux de données Analytique a été étendue tooallow * en tant qu’un accesseur de propriété d’un enregistrement imbriqué. Pour plus d’informations, voir [http://msdn.microsoft.com/library/mt622759.aspx](http://msdn.microsoft.com/library/mt622759.aspx "Types de données complexes"). |

## <a name="notes-for-10222015-release-of-stream-analytics"></a>Notes relatives à la version du 22/10/2015 de Stream Analytics
Cette version contient hello après les mises à jour.

| Intitulé | Description |
| --- | --- |
| Fonctionnalités de langage de requête supplémentaires |Flux de données Analytique a développée langage de requête hello en insérant hello suivant des fonctionnalités : [ABS](https://msdn.microsoft.com/library/azure/mt574054.aspx), [plafond](https://msdn.microsoft.com/library/azure/mt605286.aspx), [EXP](https://msdn.microsoft.com/library/azure/mt605289.aspx), [FLOOR](https://msdn.microsoft.com/library/azure/mt605240.aspx), [POWER](https://msdn.microsoft.com/library/azure/mt605287.aspx), [signe](https://msdn.microsoft.com/library/azure/mt605290.aspx), [carré](https://msdn.microsoft.com/library/azure/mt605288.aspx), et [SQRT](https://msdn.microsoft.com/library/azure/mt605238.aspx). |
| Limitations d’agrégation supprimées |Cette version supprime la limite de hello de 15 agrégats dans une requête. Il n’existe désormais toohello aucun limiter le nombre d’agrégats par requête. |
| Fonctionnalité GROUP BY System.Timestamp ajoutée |Hello [GROUP BY](https://msdn.microsoft.com/library/azure/dn835023.aspx) permet désormais de fonction pour soit window_type ou [System.Timestamp](https://msdn.microsoft.com/library/azure/mt598501.aspx). |
| Fonctionnalité OFFSET ajoutée pour les fenêtres bascule et récurrentes |Par défaut, la fenêtre [bascule](https://msdn.microsoft.com/library/azure/dn835055.aspx) et la fenêtre [récurrente](https://msdn.microsoft.com/library/azure/dn835041.aspx) sont alignées par rapport à l’heure zéro (1/1/0001 12:00:00 AM UTC). Hello nouveau (facultatif) 'offsetsize' permet de spécifier un offset (ou un alignement) personnalisé. |

## <a name="notes-for-09292015-release-of-stream-analytics"></a>Notes relatives à la version du 29/09/2015 de Stream Analytics
Cette version contient hello après les mises à jour.

| Intitulé | Description |
| --- | --- |
| Version préliminaire publique d’IoT Azure Suite |Flux de données Analytique est inclus dans hello version préliminaire publique de hello Azure IoT Suite. |
| Intégration du portail Azure |En présence de toocontinued ajout dans le portail de gestion Azure hello, flux de données Analytique est maintenant intégré dans hello [Azure Portal](https://azure.microsoft.com/overview/preview-portal/). Notez que la fonctionnalité de flux de données Analytique dans le portail en version préliminaire hello est actuellement disponible un sous-ensemble de fonctionnalités de hello proposés dans le portail de gestion Azure hello, sans prise en charge pour le test de la requête de dans un navigateur, que Power BI de configuration et navigation tooor création d’une nouvelle sortie ressources d’entrée et de sortie dans les abonnements que vous avez accès. |
| Prise en charge de la sortie d’Azure Cosmos DB |Tâches de flux de données Analytique peuvent à présent sortir trop[base de données Azure Cosmos](https://azure.microsoft.com/services/documentdb/). |
| Prise en charge de l’entrée IoT Hub |Les tâches Stream Analytics peuvent à présent recevoir des données à partir d’IoT Hub. |
| TIMESTAMP BY pour les événements hétérogènes |Lorsqu’un flux de données contient plusieurs types d’événements ayant des horodatages dans différents domaines, vous pouvez maintenant utiliser [TIMESTAMP BY](http://msdn.microsoft.com/library/mt573293.aspx) avec des champs d’horodatage différent de toospecify d’expressions pour chaque cas. |

## <a name="notes-for-09102015-release-of-stream-analytics"></a>Notes relatives à la version du 10/09/2015 de Stream Analytics
Cette version contient hello après les mises à jour.

| Intitulé | Description |
| --- | --- |
| Prise en charge des groupes PowerBI |partage des données avec d’autres utilisateurs de Power BI, Analytique de flux de travaux, peuvent désormais écrire trop de tooenable[PowerBI groupes](stream-analytics-define-outputs.md#power-bi) à l’intérieur de votre compte Power BI. |

## <a name="notes-for-08202015-release-of-stream-analytics"></a>Notes relatives à la version du 20/08/2015 de Stream Analytics
Cette version contient hello après les mises à jour.

| Intitulé | Description |
| --- | --- |
| Ajout de la fonction LAST |Hello [dernière](http://msdn.microsoft.com/library/mt421186.aspx) fonction est désormais disponible dans les tâches de flux de données Analytique, vous permettant d’événement le plus récent tooretrieve hello dans un flux d’événements pendant un laps de temps donné. |
| Nouvelles fonctions de tableau |Les fonctions de tableau [GetArrayElement](http://msdn.microsoft.com/library/mt270218.aspx), [GetArrayElements](http://msdn.microsoft.com/library/mt298451.aspx) et [GetArrayLength](http://msdn.microsoft.com/library/mt270226.aspx) sont désormais disponibles. |
| Nouvelles fonctions d’enregistrement |Les fonctions d’enregistrement [GetRecordProperties](http://msdn.microsoft.com/library/mt270221.aspx) et [GetRecordPropertyValue](http://msdn.microsoft.com/library/mt270220.aspx) sont désormais disponibles. |

## <a name="notes-for-07302015-release-of-stream-analytics"></a>Notes relatives à la version du 30/07/2015 de Stream Analytics
Cette version contient hello après les mises à jour.

| Intitulé | Description |
| --- | --- |
| ID d’organisation Power BI dissocié de l’ID Azure |Cette fonctionnalité permet une [sortie Power BI](stream-analytics-power-bi-dashboard.md) pour les tâches ASA dans tout type de compte Azure (Live ID ou ID d’organisation). En outre, vous pouvez avoir un ID d’organisation pour votre compte Azure et en utiliser un autre pour autoriser la sortie de Power BI. |
| Prise en charge de la sortie de files d’attente de Service Bus |Les sorties des [files d’attente Service Bus](stream-analytics-define-outputs.md#service-bus-queues) sont désormais disponibles dans les tâches Stream Analytics. |
| Prise en charge de la sortie de rubriques de Service Bus |Les sorties de [rubriques Service Bus](stream-analytics-define-outputs.md#service-bus-topics) sont désormais disponibles dans les tâches Stream Analytics. |

## <a name="notes-for-07092015-release-of-stream-analytics"></a>Notes relatives à la version du 09/07/2015 de Stream Analytics
Cette version contient hello après les mises à jour.

| Intitulé | Description |
| --- | --- |
| Partitionnement personnalisé de la sortie des objets blob |Sorties de stockage d’objets BLOB permettent à présent une fréquence de hello toospecify option produisant en sortie des objets BLOB sont écrites et structure de hello et le format de hello de structure de données chemin d’accès au dossier de sortie. |

## <a name="notes-for-05032015-release-of-stream-analytics"></a>Notes relatives à la version du 03/05/2015 de Stream Analytics
Cette version contient hello après les mises à jour.

| Intitulé | Description |
| --- | --- |
| Augmentation de la valeur maximale de la plage de tolérance pour les événements en désordre |Hello taille maximale de hello de plage de tolérance est désormais 59:59 (mm : ss) |
| Format de sortie JSON : Séparé par une ligne ou tableau |Il existe désormais une option lors de la sortie tooBlob stockage ou toooutput du concentrateur d’événements comme un tableau d’objets JSON ou en séparant les objets JSON avec une nouvelle ligne. |

## <a name="notes-for-04162015-release-of-stream-analytics"></a>Notes relatives à la version du 16/04/2015 de Stream Analytics
| Intitulé | Description |
| --- | --- |
| Retard dans la configuration du compte Azure Storage |Lorsque vous créez une tâche de flux de données Analytique dans une région de hello première fois, vous être invité à toocreate un compte de stockage ou spécifiez un compte existant pour l’analyse des tâches de flux de données Analytique dans cette région. Échéance toolatency dans la configuration de la surveillance, la création d’une autre tâche de flux de données Analytique Bonjour même région dans les 30 minutes demandera hello spécification d’un deuxième compte de stockage au lieu de hello récemment configuré un Bonjour stockage de surveillance Liste déroulante du compte. tooavoid création d’un compte de stockage inutile, attendez 30 minutes après la création d’un travail dans une région de hello première avant la configuration des travaux supplémentaires dans cette région. |
| Mise à niveau d’un travail |À ce stade, Analytique de flux ne prend pas en charge modifications dynamique toohello définition ou la configuration d’un travail en cours d’exécution. Dans l’ordre toochange hello entrée, sortie, requête, l’échelle ou configuration d’un travail en cours d’exécution, vous devez arrêter les travaux hello. |
| Types de données déduits de la source d’entrée |Si une instruction CREATE TABLE n’est pas utilisée, un type d’entrée hello est dérivé de format d’entrée, par exemple tous les champs de volumes partagés de cluster sont la chaîne. Champs besoin toobe converti explicitement toohello type approprié à l’aide de la fonction CAST de hello dans les erreurs d’incompatibilité de type order tooavoid. |
| Les champs manquants sont renvoyés comme valeurs nulles. |Faisant référence à un champ qui n’est pas présent dans la source d’entrée de hello génère des valeurs null dans l’événement de sortie hello. |
| Les instructions AVEC doivent précéder les instructions SÉLECTIONNER |Dans votre requête, les instructions SÉLECTIONNER doivent suivre les sous-requêtes définies dans les instructions AVEC. |
| Problème de mémoire insuffisante |Diffusion en continu de travaux Analytique avec une grande tolérance pour les événements non ordonnés et/ou des requêtes complexes en conservant qu'une grande quantité d’état peut provoquer toorun de travail hello en dehors de la mémoire, ce qui entraîne un travail de redémarrer. Hello démarrer et arrêter les opérations sont visibles dans les journaux des opérations de la tâche hello. tooavoid ce comportement, la mise à l’échelle de requête de hello expire sur plusieurs partitions. Dans une version ultérieure, cette limitation sera traitée par la dégradation des performances des travaux affectés plutôt que par leur redémarrage. |
| Les entrées importantes d’objets blob sans horodatage de la charge utile peuvent provoquer un problème d’insuffisance de mémoire |Utilisation de fichiers volumineux depuis le stockage Blob risque de toocrash des tâches de flux de données Analytique si un champ d’horodatage n’est pas spécifié via TIMESTAMP BY. tooavoid ce problème, conserver chaque objet blob sous 10 Mo la taille. |
| Limitation du volume d’événements de base de données SQL |Lors de l’utilisation de base de données SQL comme une cible de sortie, très grands volumes de données de sortie risque de hello tootime de travail Analytique de flux sortant. tooresolve ce problème, soit réduire le volume de sortie hello à l’aide des opérateurs de filtre ou des agrégats ou choisissez stockage d’objets Blob Azure ou les concentrateurs d’événements en tant qu’une cible de sortie. |
| Les jeux de données Power BI ne peuvent contenir qu’une seule table |Power BI ne peut pas prendre en charge plus d’une table dans un jeu de données. |

## <a name="get-help"></a>Obtenir de l’aide
Pour obtenir une assistance, essayez notre [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Étapes suivantes
* [Introduction tooAzure Analytique de flux de données](stream-analytics-introduction.md)
* [Prise en main d’Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Mise à l'échelle des travaux Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Références sur le langage des requêtes d'Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Références sur l’API REST de gestion d’Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
