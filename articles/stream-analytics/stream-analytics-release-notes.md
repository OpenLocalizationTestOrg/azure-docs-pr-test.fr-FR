---
title: Notes de publication de Stream Analytics | Microsoft Docs
description: Notes de publication de Stream Analytics
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 5e59f893-cd2c-43fb-9eca-c146ce637203
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 05/03/2017
ms.author: samacha
ms.openlocfilehash: 3251cd47bb917912d63330345dbf392e724448ea
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="stream-analytics-release-notes"></a>Notes de publication de Stream Analytics

## <a name="notes-for-06142017-update-of-stream-analytics-tools-for-visual-studio"></a>Notes relatives à la mise à jour du 14/06/2017 d’Azure Stream Analytics Tools pour Visual Studio
Cette mise à jour est destinée à nos outils Visual Studio Tools. Cette version contient les nouvelles fonctionnalités ci-dessous :

| Intitulé | Description |
| --- | --- |
| Prise en charge de l’éditeur de script Java |Vous pouvez profiter de l’expérience de l’éditeur de script Java natif après avoir créé vos fonctions de script Java.|
| Afficher un message d’erreur d’exécution du travail | En cas d’erreurs d’exécution pendant l’exécution du travail, vous pouvez les afficher dans l’onglet Erreurs en ajustant la fenêtre de temps d’affichage. Par défaut, elle affiche les messages d’erreur des 30 dernières minutes. |
| Prise en charge CSV et Avro du test local de l’entrée | Outre le format JSON, vous pouvez à présent utiliser les formats de fichiers CSV et Avro pour le test local de l’entrée.|

## <a name="notes-for-05032017-update-of-stream-analytics"></a>Notes relatives à la version du 03/05/2017 de Stream Analytics
Cette mise à jour concerne la publication de notre documentation de résolution des problèmes.

Le [guide de résolution des problèmes](stream-analytics-troubleshooting-guide.md) et d’autres documents ont été publiés. Nous vous invitons à les consulter et à nous faire part de vos commentaires.

## <a name="notes-for-04242017-update-of-stream-analytics-tools-for-visual-studio"></a>Notes relatives à la mise à jour du 24/04/2017 d’Azure Stream Analytics Tools pour Visual Studio
Cette mise à jour est destinée à nos outils Visual Studio Tools. Cette version contient les nouvelles fonctionnalités ci-dessous :

| Intitulé | Description |
| --- | --- |
| Afficher le résultat du test local dans Visual Studio | Pour afficher le résultat de la sortie du test local, il vous suffit d’appuyer sur Entrée dans la fenêtre de la console de sortie ou de la fermer. Le résultat s’affiche dans une fenêtre dans Visual Studio sous forme de tableau. |
| Résultat local de sortie au format JSON | Lorsqu’un test local est exécuté, le résultat de sortie est généré dans les formats de fichiers JSON et CSV. |
| Afficher un aperçu des données d’entrées/de sorties du stockage d’objets Blob/Table | En double-cliquant sur une entrée/sortie du stockage Table ou Blob dans la présentation Travail, vous pouvez facilement afficher un aperçu des données dans Visual Studio. |
| Afficher les messages d’erreur des entrées/sorties | Les éventuelles erreurs d’exécution liées aux entrées ou aux sorties du travail s’affichent sur le diagramme du travail ; placez le curseur dessus pour afficher le message d’erreur détaillé.|


## <a name="notes-for-02012017-release-of-stream-analytics"></a>Notes relatives à la version du 01/02/2017 de Stream Analytics
Cette version contient la mise à jour suivante :

| Intitulé | Description |
| --- | --- |
| Présentation des fonctions JavaScript définies par l’utilisateur |Des [fonctions Java définies par l’utilisateur](stream-analytics-javascript-user-defined-functions.md) sont désormais disponibles pour offrir davantage de souplesse lors de la création de requêtes. |
| Présentation des outils pour Visual Studio et Stream Analytics |Des [outils pour Visual Studio](stream-analytics-tools-for-visual-studio.md) sont désormais disponibles pour le débogage et d’autres fonctions utiles. |
| Présentation de la journalisation des diagnostics |La [journalisation des diagnostics](stream-analytics-job-diagnostic-logs.md) propose des options de dépannage supplémentaires. |
| Présentation des fonctions géospatiales |Des [fonctions géospatiales](http://msdn.microsoft.com/library/mt778980(Azure.100).aspx) sont désormais disponibles. |

## <a name="notes-for-04152016-release-of-stream-analytics"></a>Notes pour la version 04/15/2016 de Stream Analytics 
Cette version contient la mise à jour suivante :

| Intitulé | Description |
| --- | --- |
| Disponibilité générale pour les sorties Power BI |[sorties Power BI](stream-analytics-power-bi-dashboard.md) sont désormais mises à la disposition générale. L’expiration de l’autorisation de Power BI après 90 jours a été supprimée. Pour plus d’informations sur les scénarios dans lesquels l’autorisation doit être renouvelée, consultez la section [Renouveler une autorisation](stream-analytics-power-bi-dashboard.md#renew-authorization) de la page Créer un tableau de bord Power BI. |

## <a name="notes-for-03032016-release-of-stream-analytics"></a>Notes relatives à la version du 03/03/2016 de Stream Analytics
Cette version contient la mise à jour suivante :

| Intitulé | Description |
| --- | --- |
| Nouveaux éléments du langage de requête Stream Analytics |SAQL dispose désormais des expressions [GetType](https://msdn.microsoft.com/library/azure/mt643890.aspx "GetType MSDN Page"), [TRY_CAST](https://msdn.microsoft.com/library/azure/mt643735.aspx "TRY_CAST MSDN Page") et [REGEXMATCH](https://msdn.microsoft.com/library/azure/mt643891.aspx "REGEXMATCH MSDN Page"). |

## <a name="notes-for-12102015-release-of-stream-analytics"></a>Notes relatives à la version du 10/12/2015 de Stream Analytics
Cette version contient la mise à jour suivante :

| Intitulé | Description |
| --- | --- |
| Mise à jour de la version de l’API REST |L’API REST a été mise à jour vers la version suivante : 01-10-2015. Vous trouverez plus d’informations sur MSDN à l’adresse [Références d’API REST de gestion Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx) et [Intégration de Machine Learning dans Stream Analytics](stream-analytics-how-to-configure-azure-machine-learning-endpoints-in-stream-analytics.md). |
| Intégration d’Azure Machine Learning |Cette version s’accompagne de la prise en charge des fonctions Azure Machine Learning définies par l’utilisateur. Consultez le [didacticiel](stream-analytics-machine-learning-integration-tutorial.md) pour plus d’informations, ainsi que les [annonces générales sur le blog](http://blogs.technet.com/b/machinelearning/archive/2015/12/10/apply-azure-ml-as-a-function-in-azure-stream-analytics.aspx). |

## <a name="notes-for-11122015-release-of-stream-analytics"></a>Notes relatives à la version du 12/11/2015 de Stream Analytics
Cette version contient la mise à jour suivante :

| Intitulé | Description |
| --- | --- |
| Nouveau comportement de SELECT |Dans Stream Analytics, SELECT a été étendu pour autoriser * comme accesseur de propriété d’un enregistrement imbriqué. Pour plus d’informations, consultez la page [http://msdn.microsoft.com/library/mt622759.aspx](http://msdn.microsoft.com/library/mt622759.aspx "Types de données complexes"). |

## <a name="notes-for-10222015-release-of-stream-analytics"></a>Notes relatives à la version du 22/10/2015 de Stream Analytics
Cette version contient les mises à jour suivantes :

| Intitulé | Description |
| --- | --- |
| Fonctionnalités de langage de requête supplémentaires |Stream Analytics a étendu le langage de requête en incluant les fonctionnalités suivantes : [ABS](https://msdn.microsoft.com/library/azure/mt574054.aspx), [CEILING](https://msdn.microsoft.com/library/azure/mt605286.aspx), [EXP](https://msdn.microsoft.com/library/azure/mt605289.aspx), [FLOOR](https://msdn.microsoft.com/library/azure/mt605240.aspx), [POWER](https://msdn.microsoft.com/library/azure/mt605287.aspx), [SIGN](https://msdn.microsoft.com/library/azure/mt605290.aspx), [SQUARE](https://msdn.microsoft.com/library/azure/mt605288.aspx) et [SQRT](https://msdn.microsoft.com/library/azure/mt605238.aspx). |
| Limitations d’agrégation supprimées |Cette version supprime la limitation à 15 agrégats dans une requête. Il n’existe désormais aucune limite du nombre d’agrégats par requête. |
| Fonctionnalité GROUP BY System.Timestamp ajoutée |La fonction [GROUP BY](https://msdn.microsoft.com/library/azure/dn835023.aspx) autorise désormais window_type ou [System.Timestamp](https://msdn.microsoft.com/library/azure/mt598501.aspx). |
| Fonctionnalité OFFSET ajoutée pour les fenêtres bascule et récurrentes |Par défaut, la fenêtre [bascule](https://msdn.microsoft.com/library/azure/dn835055.aspx) et la fenêtre [récurrente](https://msdn.microsoft.com/library/azure/dn835041.aspx) sont alignées par rapport à l’heure zéro (1/1/0001 12:00:00 AM UTC). Le nouveau paramètre (facultatif) « offsetsize » permet de spécifier un décalage (ou alignement) personnalisé. |

## <a name="notes-for-09292015-release-of-stream-analytics"></a>Notes relatives à la version du 29/09/2015 de Stream Analytics
Cette version contient les mises à jour suivantes :

| Intitulé | Description |
| --- | --- |
| Version préliminaire publique d’IoT Azure Suite |Stream Analytics est inclus dans la version préliminaire publique d’IoT Azure Suite. |
| Intégration du Portail Azure |Stream Analytics, toujours présent sur le Portail Azure, est désormais intégré au [Portail Azure](https://azure.microsoft.com/overview/preview-portal/). Notez que la fonctionnalité Stream Analytics du portail en version préliminaire correspond actuellement à un sous-ensemble des fonctionnalités offertes par le Portail Azure, sans prise en charge du test de requête dans un navigateur, de la configuration des sorties Power BI et de la possibilité de créer ou d’accéder aux ressources d’entrée et de sortie des abonnements auxquels vous avez accès. |
| Prise en charge de la sortie d’Azure Cosmos DB |Les tâches Stream Analytics peuvent désormais générer une sortie dans [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/). |
| Prise en charge de l’entrée IoT Hub |Les tâches Stream Analytics peuvent à présent recevoir des données à partir d’IoT Hub. |
| TIMESTAMP BY pour les événements hétérogènes |Quand un flux de données unique contient plusieurs types d’événements ayant des horodatages dans différents champs, vous pouvez désormais utiliser [TIMESTAMP BY](http://msdn.microsoft.com/library/mt573293.aspx) avec des expressions pour spécifier différents champs d’horodatage pour chaque cas. |

## <a name="notes-for-09102015-release-of-stream-analytics"></a>Notes relatives à la version du 10/09/2015 de Stream Analytics
Cette version contient les mises à jour suivantes :

| Intitulé | Description |
| --- | --- |
| Prise en charge des groupes PowerBI |Pour permettre le partage de données avec d’autres utilisateurs de Power BI, les tâches Stream Analytics peuvent désormais écrire dans des [groupes PowerBI](stream-analytics-define-outputs.md#power-bi) appartenant à votre compte Power BI. |

## <a name="notes-for-08202015-release-of-stream-analytics"></a>Notes relatives à la version du 20/08/2015 de Stream Analytics
Cette version contient les mises à jour suivantes :

| Intitulé | Description |
| --- | --- |
| Ajout de la fonction LAST |La fonction [LAST](http://msdn.microsoft.com/library/mt421186.aspx) est désormais disponible dans les tâches Stream Analytics, ce qui vous permet de récupérer l’événement le plus récent d’un flux d’événements dans une période donnée. |
| Nouvelles fonctions de tableau |Les fonctions de tableau [GetArrayElement](http://msdn.microsoft.com/library/mt270218.aspx), [GetArrayElements](http://msdn.microsoft.com/library/mt298451.aspx) et [GetArrayLength](http://msdn.microsoft.com/library/mt270226.aspx) sont désormais disponibles. |
| Nouvelles fonctions d’enregistrement |Les fonctions d’enregistrement [GetRecordProperties](http://msdn.microsoft.com/library/mt270221.aspx) et [GetRecordPropertyValue](http://msdn.microsoft.com/library/mt270220.aspx) sont désormais disponibles. |

## <a name="notes-for-07302015-release-of-stream-analytics"></a>Notes relatives à la version du 30/07/2015 de Stream Analytics
Cette version contient les mises à jour suivantes :

| Intitulé | Description |
| --- | --- |
| ID d’organisation Power BI dissocié de l’ID Azure |Cette fonctionnalité permet une [sortie Power BI](stream-analytics-power-bi-dashboard.md) pour les tâches ASA dans tout type de compte Azure (Live ID ou ID d’organisation). En outre, vous pouvez avoir un ID d’organisation pour votre compte Azure et en utiliser un autre pour autoriser la sortie de Power BI. |
| Prise en charge de la sortie de files d’attente de Service Bus |Les sorties des [files d’attente Service Bus](stream-analytics-define-outputs.md#service-bus-queues) sont désormais disponibles dans les tâches Stream Analytics. |
| Prise en charge de la sortie de rubriques de Service Bus |Les sorties de [rubriques Service Bus](stream-analytics-define-outputs.md#service-bus-topics) sont désormais disponibles dans les tâches Stream Analytics. |

## <a name="notes-for-07092015-release-of-stream-analytics"></a>Notes relatives à la version du 09/07/2015 de Stream Analytics
Cette version contient les mises à jour suivantes :

| Intitulé | Description |
| --- | --- |
| Partitionnement personnalisé de la sortie des objets blob |Les sorties d’objets blob de stockage autorisent désormais une option pour spécifier la fréquence à laquelle les objets blob de sortie sont écrits ainsi que la structure et le format de la structure des dossiers du chemin d’accès des données de sortie. |

## <a name="notes-for-05032015-release-of-stream-analytics"></a>Notes relatives à la version du 03/05/2015 de Stream Analytics
Cette version contient les mises à jour suivantes :

| Intitulé | Description |
| --- | --- |
| Augmentation de la valeur maximale de la plage de tolérance pour les événements en désordre |La taille maximale de la plage de tolérance pour les événements en désordre est désormais définie sur 59:59 (mm:ss). |
| Format de sortie JSON : Séparé par une ligne ou tableau |Il existe désormais une option lors de la sortie vers le stockage d’objets blob ou le hub d’événements sous la forme d’un tableau d’objets JSON ou en séparant les objets JSON par une nouvelle ligne. |

## <a name="notes-for-04162015-release-of-stream-analytics"></a>Notes relatives à la version du 16/04/2015 de Stream Analytics
| Intitulé | Description |
| --- | --- |
| Retard dans la configuration du compte Azure Storage |Si c’est la première fois que vous créez un travail Stream Analytics dans une certaine région, vous devez créer un compte de stockage ou indiquer un compte existant pour surveiller les travaux Stream Analytics de cette région. En raison d’une latence dans la configuration du monitorage, la création d’un autre travail Stream Analytics dans la même région dans les 30 minutes invite à indiquer un second compte de stockage au lieu d’afficher celui que vous venez de configurer dans la liste déroulante Surveiller un compte de stockage. Pour éviter la création d'un compte de stockage inutile, attendez 30 minutes après votre première création de travail dans une région, puis procédez à la configuration des travaux supplémentaires dans cette région. |
| Mise à niveau d’un travail |Pour le moment, Stream Analytics ne prend pas en charge les modifications de définition ou de configuration en direct d’un travail en cours d’exécution. Pour modifier l’entrée, la sortie, la requête, l’échelle ou la configuration d’un travail en cours d’exécution, vous devez tout d’abord l’arrêter. |
| Types de données déduits de la source d’entrée |Si une instruction CRÉER UNE TABLE n’est pas utilisée, le type d’entrée est dérivé du format d’entrée, par exemple tous les champs du CSV sont des chaînes. Les champs doivent être explicitement convertis au type correct à l’aide de la fonction CAST pour éviter les erreurs d’incompatibilité des types. |
| Les champs manquants sont renvoyés comme valeurs nulles. |La référence à un champ absent de la source d’entrée génère des valeurs nulles dans l’événement de sortie. |
| Les instructions AVEC doivent précéder les instructions SÉLECTIONNER |Dans votre requête, les instructions SÉLECTIONNER doivent suivre les sous-requêtes définies dans les instructions AVEC. |
| Problème de mémoire insuffisante |Les travaux Streaming Analytics ayant une tolérance importante pour les événements arrivant en désordre et/ou les requêtes complexes tenant à jour un grand nombre d’états, cela peut entraîner un manque de mémoire et provoquer leur redémarrage. Les opérations de démarrage et d’arrêt sont visibles dans les journaux des opérations du travail. Pour éviter ce comportement, montez en charge la requête sur plusieurs partitions. Dans une version ultérieure, cette limitation sera traitée par la dégradation des performances des travaux affectés plutôt que par leur redémarrage. |
| Les entrées importantes d’objets blob sans horodatage de la charge utile peuvent provoquer un problème d’insuffisance de mémoire |L’absorption de fichiers volumineux depuis le stockage d’objets blob peut entraîner le blocage de Stream Analytics si un champ d’horodatage n’est pas spécifié via HORODATAGE PAR. Pour éviter ce problème, faites en sorte que la taille de chaque objet blob ne dépasse pas 10 Mo. |
| Limitation du volume d’événements de base de données SQL |Lorsque vous utilisez une base de données SQL comme cible de sortie, des volumes de données de sortie particulièrement importants peuvent provoquer une expiration du délai du travail Stream Analytics. Pour résoudre ce problème, réduisez le volume de sortie à l’aide d’opérateurs d’agrégation ou de filtrage, ou choisissez le service de stockage d’objets blob Azure ou Event Hubs comme cible de sortie. |
| Les jeux de données Power BI ne peuvent contenir qu’une seule table |Power BI ne peut pas prendre en charge plus d’une table dans un jeu de données. |

## <a name="get-help"></a>Obtenir de l’aide
Pour obtenir une assistance, essayez notre [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Étapes suivantes
* [Présentation d’Azure Stream Analytics](stream-analytics-introduction.md)
* [Prise en main d’Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Mise à l'échelle des travaux Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Références sur le langage des requêtes d'Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Références sur l’API REST de gestion d’Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
