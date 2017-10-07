---
title: "aaaTroubleshoot Analytique de flux de données Azure avec des journaux de diagnostics | Documents Microsoft"
description: "Découvrez comment tooanalyze journaux de diagnostics à partir de l’Analytique des flux de travaux dans Microsoft Azure."
keywords: 
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
ms.openlocfilehash: 600fce73636dd137f8f3a137f1d77b59b4a88801
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-stream-analytics-by-using-diagnostics-logs"></a>Résoudre les problèmes liés à Azure Stream Analytics à l’aide des journaux de diagnostic

Il arrive parfois qu’un travail Azure Stream Analytics s’arrête de manière inattendue. Il est important toobe le tootroubleshoot en mesure de ce type d’événement. événement de Hello peut être provoqué par un résultat de requête inattendue, par toodevices de connectivité ou par un arrêt inattendu du service. Hello dans le flux de données Analytique des journaux de diagnostic peuvent vous aider à identifier la cause hello des problèmes lorsqu’ils se produisent et réduisent les temps de récupération.

## <a name="log-types"></a>Types de journaux

Stream Analytics fournit deux types de journaux : 
* Les [journaux d’activité](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) (activés en permanence). Les journaux d’activité fournissent des détails sur les opérations effectuées sur les travaux.
* Les [journaux de diagnostic](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs) (configurables). Les journaux de diagnostic offrent des informations plus détaillées sur tous les événements liés à un travail. Diagnostics les journaux lors de la création du travail de hello de début et fin hello travail est supprimé. Elles décrivent les événements lors de la tâche de hello est mise à jour et il est en cours d’exécution.

> [!NOTE]
> Vous pouvez utiliser des services tels que le stockage Azure Azure Event Hubs, données et Analytique de journal Azure tooanalyze non conformes. Vous êtes facturé en fonction de hello tarification pour ces services.
>

## <a name="turn-on-diagnostics-logs"></a>Activer les journaux de diagnostic

Les journaux de diagnostic sont **désactivés** par défaut. tooturn sur les journaux de diagnostics, procédez comme suit :

1.  Connectez-vous à toohello portail Azure, puis accédez toohello Panneau de tâche de diffusion en continu. Sous **Surveillance**, sélectionnez **Journaux de diagnostic**.

    ![Panneau navigation toodiagnostics journaux](./media/stream-analytics-job-diagnostic-logs/image1.png)  

2.  Sélectionnez **Activer les diagnostics**.

    ![Activer les journaux de diagnostic](./media/stream-analytics-job-diagnostic-logs/image2.png)

3.  Sur hello **paramètres de diagnostic** page, pour **état**, sélectionnez **sur**.

    ![Modifier l’état pour les journaux de diagnostic](./media/stream-analytics-job-diagnostic-logs/image3.png)

4.  Configurer la cible d’archivage hello (compte de stockage, concentrateur d’événements, Analytique de journal) que vous souhaitez. Ensuite, sélectionnez les catégories de hello de journaux que vous souhaitez toocollect (d’exécution, création). 

5.  Enregistrer la nouvelle configuration de diagnostics hello.

configuration des diagnostics Hello en vigueur environ 10 minutes tootake. Après cela, hello consigne début figurant dans la cible d’archivage hello configuré (vous pouvez voir ces derniers sur hello **les journaux de diagnostic** page) :

![Journaux de toodiagnostics panneau navigation - cibles d’archivage](./media/stream-analytics-job-diagnostic-logs/image4.png)

Pour en savoir plus sur la configuration de diagnostic, consultez l’article [Collecte et utilisation des données de diagnostic à partir de vos ressources Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs).

## <a name="diagnostics-log-categories"></a>Catégories de journaux de diagnostic

Deux catégories de journaux de diagnostic sont actuellement disponibles :

* **Création** : Capture les événements qui sont associée toojob opérations de création : la création du travail, ajout et suppression d’entrées et sorties, ajout et la mise à jour de la requête de hello, le démarrage et la tâche hello de l’arrêt.
* **Exécution** : capture les événements qui se produisent pendant l’exécution du travail :
    * Erreurs de connectivité
    * Erreurs de traitement des données, notamment :
        * Les événements qui ne sont pas conformes toohello définition (types de champs ne correspondent pas et les valeurs, les champs manquants, etc.) de la requête
        * Erreurs d’évaluation d’expression
    * Autres erreurs et événements

## <a name="diagnostics-logs-schema"></a>Schéma des journaux de diagnostic

Tous les journaux sont stockés au format JSON. Chaque entrée a hello suivant des champs de chaîne courants :

Nom | Description
------- | -------
time | Horodateur (au format UTC) de journal de hello.
resourceId | ID de ressource hello hello opération a eu lieu, en majuscules. Il inclut l’ID d’abonnement hello, groupe de ressources hello et nom de la tâche hello. Par exemple, **/SUBSCRIPTIONS/6503D296-DAC1-4449-9B03-609A1F4A1C87/RESOURCEGROUPS/MY-RESOURCE-GROUP/PROVIDERS/MICROSOFT.STREAMANALYTICS/STREAMINGJOBS/MYSTREAMINGJOB**.
category | La catégorie de journal, **Exécution** ou **Création**.
operationName | Nom de l’opération hello est connectée. Par exemple, **envoyer des événements : échec toomysqloutput d’écriture de sortie SQL**.
status | État de l’opération de hello. Par exemple, **Échec** ou **Réussite**.
minimal | Le niveau du journal. Par exemple, **Erreur**, **Avertissement** ou **Informations**.
properties | Détail spécifique de l’entrée du journal, sérialisé comme chaîne JSON. Pour plus d’informations, consultez les sections suivantes de hello.

### <a name="execution-log-properties-schema"></a>Schéma de propriétés des journaux d’exécution

Les journaux d’exécution contiennent des informations sur les événements qui se sont produits pendant l’exécution du travail Stream Analytics. schéma Hello des propriétés varie en fonction de type hello d’événement. Actuellement, nous avons hello les types de journaux d’exécution suivants :

### <a name="data-errors"></a>Erreurs de données

Toute erreur qui se produit lors du traitement de données de travail de hello est dans cette catégorie de journaux. La plupart du temps, ces journaux sont créés au cours des opérations de lecture, de sérialisation et d’écriture des données. Ces journaux n’incluent pas les erreurs de connectivité. Les erreurs de connectivité sont traitées comme des événements génériques.

Nom | Description
------- | -------
Source | Nom du travail de hello d’entrée ou de sortie où hello s’est produite.
Message | Message associé à hello erreur.
Type | Le type d’erreur. Par exemple, **DataConversionError**, **CsvParserError** ou **ServiceBusPropertyColumnMissingError**.
Données | Contient des données qui sont utiles tooaccurately localiser la source de hello d’erreur de hello. Objet tootruncation, en fonction de la taille.

En fonction de hello **NomOpération** valeur, les erreurs de données ont hello suivant le schéma :
* **Événements de sérialisation** : les événements de sérialisation se produisent pendant les opérations de lecture d’événements, Elles se produisent lorsque hello données dans l’entrée de hello ne satisfait pas aux schémas de requête hello pour l’une des raisons suivantes :
    * *Incompatibilité de type au cours de l’événement (de) sérialiser*: identifie le champ hello qui provoque l’erreur de hello.
    * *Impossible de lire un événement, la sérialisation non valide*: répertorie des informations sur l’emplacement hello dans les données d’entrée hello où hello s’est produite. Inclut le nom d’objet blob pour l’entrée de l’objet blob, décalage et un exemple de données de hello.
* **Événements d’envoi** : les événements d’envoi se produisent pendant les opérations d’écriture. Ils identifient hello événement ayant provoqué l’erreur de hello de diffusion en continu.

### <a name="generic-events"></a>Événements génériques

Les événements génériques couvrent tout le reste.

Nom | Description
-------- | --------
Error | (facultatif) Informations sur l’erreur, en général des informations sur l’exception si celles-ci sont disponibles.
Message| Message de journal.
Type | Type de message, Mappe la catégorisation toointernal d’erreurs. Par exemple, **JobValidationError** ou **BlobOutputAdapterInitializationFailure**.
ID de corrélation : | [GUID](https://en.wikipedia.org/wiki/Universally_unique_identifier) qui identifie de façon unique l’exécution du travail hello. Toutes les entrées de journal d’exécution à partir de hello de temps hello démarre la tâche jusqu'à ce que hello tâche s’arrête ont hello même **ID de corrélation** valeur.

## <a name="next-steps"></a>Étapes suivantes

* [Introduction tooStream Analytique](stream-analytics-introduction.md)
* [Prise en main de Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Mise à l’échelle des travaux Stream Analytics](stream-analytics-scale-jobs.md)
* [Informations de référence sur le langage de requête Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Références sur l’API REST de gestion de Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
