---
title: "journaux de diagnostic aaaViewing pour Analytique de LAC de données Azure | Documents Microsoft"
description: "Comprendre comment toosetup et diagnostic d’accès des journaux de données Azure analytique de LAC "
services: data-lake-analytics
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: cf5633d4-bc43-444e-90fc-f90fbd0b7935
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 4cd1eb6f585c1ef96c358340232ef85721a972b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-analytics"></a>Accès aux journaux de diagnostic d’Azure Data Lake Analytics

Journalisation des diagnostics vous permet de pistes d’audit de toocollect données access. Ces journaux fournissent des informations comme :

* Une liste d’utilisateurs qui ont accédé à des données de hello.
* La fréquence à laquelle les données de salutation sont accessible.
* La quantité de données est stockée dans le compte de hello.

## <a name="enable-logging"></a>Activation de la journalisation

1. Ouverture de session toohello [portail Azure](https://portal.azure.com).

2. Ouvrez votre compte Analytique lac de données et sélectionnez **journaux de Diagnostic** de hello __moniteur__ section. Ensuite, sélectionnez __Activer les diagnostics__.

    ![Activer les diagnostics toocollect audit et les journaux de demandes](./media/data-lake-analytics-diagnostic-logs/turn-on-logging.png)

3. À partir de __paramètres de diagnostic__, définir hello état too__On__ et sélectionnez les options de journalisation.

    ![Activer les diagnostics toocollect audit et les journaux de demandes](./media/data-lake-analytics-diagnostic-logs/enable-diagnostic-logs.png "activer les journaux de diagnostic")

   * Définissez **état** trop**sur** tooenable journalisation des Diagnostics.

   * Vous pouvez choisir les données toostore/processus hello de trois façons différentes.

     * Sélectionnez __archiver le compte de stockage tooa__ toostore enregistre dans un compte de stockage Azure. Utilisez cette option si vous souhaitez que les données de salutation tooarchive. Si vous sélectionnez cette option, vous devez fournir un stockage Azure compte toosave hello se connecte à.

     * Sélectionnez **tooan concentrateur d’événements de flux** tooan de données de journal toostream concentrateur d’événements Azure. Utilisez cette option si vous disposez d’un pipeline de traitement en aval qui analyse les journaux entrants en temps réel. Si vous sélectionnez cette option, vous devez fournir les détails de hello pour hello concentrateur d’événements Azure vous souhaitez toouse.

     * Sélectionnez __envoyer tooLog Analytique__ toosend hello données toohello service d’Analytique de journal. Utilisez cette option si vous souhaitez toouse Analytique de journal toogather et analysez les journaux.
   * Spécifiez si vous souhaitez que les journaux d’audit de tooget ou les journaux des requêtes ou les deux.  Un journal des requêtes capture chaque demande d’API. Un journal d’audit enregistre toutes les opérations qui sont déclenchées par cette demande d’API.

   * Pour __archiver le compte de stockage tooa__, spécifiez nombre hello de données de hello tooretain jours.

   * Cliquez sur __Enregistrer__.

        > [!NOTE]
        > Vous devez sélectionner __archiver le compte de stockage tooa__, __tooan concentrateur d’événements de flux__ ou __envoyer tooLog Analytique__ avant de cliquer sur hello __enregistrer__bouton.

Une fois que vous avez activé les paramètres de diagnostic, vous pouvez retourner toohello __les journaux de diagnostic__ panneau tooview hello journaux.

## <a name="view-logs"></a>Consulter les journaux

### <a name="use-hello-data-lake-analytics-view"></a>Utiliser le mode de données Lake Analytique hello

1. À partir de votre Analytique lac de données compte un panneau, sous **analyse**, sélectionnez **journaux de Diagnostic** et puis sélectionnez une entrée toodisplay ouvre une session.

    ![Afficher la journalisation des diagnostics](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs.png "Afficher les journaux de diagnostic")

2. journaux Hello sont classés par **les journaux d’Audit** et **les journaux de demandes**.

    ![entrées de journal](./media/data-lake-analytics-diagnostic-logs/diagnostic-log-entries.png)

   * Les journaux de demandes de capture chaque demande d’API sur hello compte d’Analytique lac de données.
   * Journaux d’audit sont les journaux toorequest similaire, mais fournissent une analyse beaucoup plus détaillée des opérations de hello. Par exemple, un simple appel d’API de chargement dans un journal de demande peut entraîner plusieurs opérations « Ajouter » dans son journal d’audit.

3. Cliquez sur hello **télécharger** lien pour une toodownload d’entrée de journal du journal.

### <a name="use-hello-azure-storage-account-that-contains-log-data"></a>Utiliser le compte de stockage Azure hello qui contient les données du journal

1. Ouvrir le panneau de compte de stockage Azure hello associé Analytique lac de données pour la journalisation, puis cliquez sur __BLOB__. Hello **service Blob** panneau répertorie deux conteneurs.

    ![Afficher la journalisation des diagnostics](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs-storage-account.png "Afficher les journaux de diagnostic")

   * conteneur de Hello **insights-journaux-audit** contient les journaux d’audit de hello.
   * conteneur de Hello **demandes de journaux insights** contient les journaux de demandes hello.
2. Ces conteneurs, hello journaux sont stockés sous hello suivant structure :

        resourceId=/
          SUBSCRIPTIONS/
            <<SUBSCRIPTION_ID>>/
              RESOURCEGROUPS/
                <<RESOURCE_GRP_NAME>>/
                  PROVIDERS/
                    MICROSOFT.DATALAKEANALYTICS/
                      ACCOUNTS/
                        <DATA_LAKE_ANALYTICS_NAME>>/
                          y=####/
                            m=##/
                              d=##/
                                h=##/
                                  m=00/
                                    PT1H.json

   > [!NOTE]
   > Hello `##` contiennent des entrées dans le chemin d’accès hello hello year, month, day et les heures dans le hello journal a été créé. Data Lake Analytics crée un fichier toutes les heures, par conséquent, `m=` contient toujours une valeur de `00`.

    Par exemple, le chemin d’accès complet de hello tooan log peut être :

        https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=04/m=00/PT1H.json

    De même, le journal des demandes tooa hello chemin d’accès complet peut être :

        https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=14/m=00/PT1H.json

## <a name="log-structure"></a>Structure journal

Hello journaux d’audit et de la demande sont dans un format JSON structuré.

### <a name="request-logs"></a>journaux de demande

Voici un exemple d’entrée dans le journal au format JSON de demande de hello. Chaque objet blob a un objet racine appelé **enregistrements** qui contient un tableau d’objets du journal.

    {
    "records":
      [        
        . . . .
        ,
        {
             "time": "2016-07-07T21:02:53.456Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/<data_lake_analytics_account_name>",
             "category": "Requests",
             "operationName": "GetAggregatedJobHistory",
             "resultType": "200",
             "callerIpAddress": "::ffff:1.1.1.1",
             "correlationId": "4a11c709-05f5-417c-a98d-6e81b3e29c58",
             "identity": "1808bd5f-62af-45f4-89d8-03c5e81bac30",
             "properties": {
                 "HttpMethod":"POST",
                 "Path":"/JobAggregatedHistory",
                 "RequestContentLength":122,
                 "ClientRequestId":"3b7adbd9-3519-4f28-a61c-bd89506163b8",
                 "StartTime":"2016-07-07T21:02:52.472Z",
                 "EndTime":"2016-07-07T21:02:53.456Z"
                 }
        }
        ,
        . . . .
      ]
    }

#### <a name="request-log-schema"></a>Schéma du journal de requête

| Name | Type | Description |
| --- | --- | --- |
| time |String |Hello horodateur (UTC) du journal de hello |
| resourceId |String |Identificateur Hello de ressource de hello opération placer sur |
| category |String |catégorie de journal Hello. Par exemple, **Demandes**. |
| operationName |String |Nom de l’opération hello est connectée. Par exemple, GetAggregatedJobHistory. |
| resultType |String |état Hello d’opération hello, par exemple, 200. |
| callerIpAddress |String |adresse IP de Hello du client hello hello demande |
| correlationId |String |Identificateur Hello du journal de hello. Cette valeur peut être utilisé toogroup un ensemble d’entrées de journal connexes. |
| identité |Object |identité Hello qui a généré hello journal |
| properties |JSON |Voir section suivante hello (schéma de propriétés d’un journal de demande) pour plus d’informations |

#### <a name="request-log-properties-schema"></a>Schéma des propriétés de journal de demande

| Name | Type | Description |
| --- | --- | --- |
| HttpMethod |String |Hello méthode HTTP utilisée pour l’opération de hello. Par exemple, GET. |
| Chemin |String |opération hello Hello a été effectuée sur |
| RequestContentLength |int |longueur du contenu de la demande de hello HTTP Hello |
| ClientRequestId |String |Identificateur Hello qui identifie de façon unique cette demande |
| StartTime |String |heure Hello qui demande hello du serveur reçues hello |
| EndTime |String |temps de Hello à quels hello serveur a envoyé une réponse |

### <a name="audit-logs"></a>Journaux d’audit

Voici un exemple d’entrée dans le journal d’audit d’au format JSON hello. Chaque objet blob a un objet racine appelé **enregistrements** qui contient un tableau d’objets du journal.

    {
    "records":
      [        
        . . . .
        ,
        {
             "time": "2016-07-28T19:15:16.245Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/<data_lake_ANALYTICS_account_name>",
             "category": "Audit",
             "operationName": "JobSubmitted",
             "identity": "user@somewhere.com",
             "properties": {
                 "JobId":"D74B928F-5194-4E6C-971F-C27026C290E6",
                 "JobName": "New Job",
                 "JobRuntimeName": "default",
                 "SubmitTime": "7/28/2016 7:14:57 PM"
                 }
        }
        ,
        . . . .
      ]
    }

#### <a name="audit-log-schema"></a>Schéma du journal d’audit

| Name | Type | Description |
| --- | --- | --- |
| time |String |Hello horodateur (UTC) du journal de hello |
| resourceId |String |Identificateur Hello de ressource de hello opération placer sur |
| category |String |catégorie de journal Hello. Par exemple, **Audit**. |
| operationName |String |Nom de l’opération hello est connectée. Par exemple, JobSubmitted. |
| resultType |String |Un sous-état pour l’état de la tâche hello (NomOpération). |
| resultSignature |String |Plus d’informations sur l’état du travail hello (NomOpération). |
| identité |String |utilisateur Hello hello l’opération demandée. Par exemple, susan@contoso.com. |
| properties |JSON |Voir section suivante hello (schéma des propriétés du journal d’Audit) pour plus d’informations |

> [!NOTE]
> **resultType** et **resultSignature** fournissent des informations sur le résultat de hello d’une opération et contenir uniquement une valeur si une opération est terminée. Par exemple, ils contiennent uniquement une valeur quand **operationName** contient la valeur **JobStarted** ou **JobEnded**.
>
>

#### <a name="audit-log-properties-schema"></a>Schéma des propriétés de journal d’audit

| Name | Type | Description |
| --- | --- | --- |
| JobId |String |travail de Hello ID toohello attribué |
| JobName |String |nom Hello qui a été fournie pour le travail de hello |
| JobRunTime |String |Hello runtime utilisé la tâche de hello tooprocess |
| SubmitTime |String |temps de Hello (au format UTC) que le travail hello a été soumis |
| StartTime |String |Hello temps hello tâche de démarrage en cours d’exécution après l’envoi (au format UTC) |
| EndTime |String |Hello temps hello tâche s’est terminée |
| Parallélisme |String |nombre de Hello d’unités Analytique lac de données demandé pour ce travail lors de l’envoi |

> [!NOTE]
> **SubmitTime**, **StartTime**, **EndTime** et **Parallélisme** fournissent des informations sur une opération. Ces entrées ne contiennent une valeur que si cette opération a démarré ou est terminée. Par exemple, **SubmitTime** contient uniquement une valeur après **NomOpération** a la valeur de hello **JobSubmitted**.

## <a name="process-hello-log-data"></a>Données de journal hello de processus

Analytique de LAC de données Azure fournit un exemple sur la façon de tooprocess et analyser les données de journal hello. Vous trouverez un exemple hello à [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).

## <a name="next-steps"></a>Étapes suivantes
* [Présentation d’Azure Data Lake Analytics](data-lake-analytics-overview.md)
