---
title: journaux de diagnostic aaaViewing pour Azure Data Lake Store | Documents Microsoft
description: "Comprendre comment les journaux de diagnostic toosetup et l’accès à Azure Data Lake Store "
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: f6e75eb1-d0ae-47cf-bdb8-06684b7c0a94
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 11fbf7f517f97abdcaf809c1ebeeb51424ab2c1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-store"></a>Accès aux journaux de diagnostic d’Azure Data Lake Store
En savoir plus sur la journalisation des diagnostics pour votre compte Data Lake Store et le mode de journalisation des tooview hello tooenable collectées pour votre compte.

Les organisations peuvent activer la journalisation des diagnostics pour leur compte toocollect données accès pistes d’audit qui fournit des informations telles que liste d’utilisateurs qui accèdent aux données de hello, la fréquence à laquelle les données de salutation sont accessible, la quantité de données est stocké dans hello Azure Data Lake Store compte, etc.

## <a name="prerequisites"></a>Composants requis
* **Un abonnement Azure**. Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Compte Azure Data Lake Store**. Suivez les instructions de hello à [prise en main Azure Data Lake Store à l’aide de hello Azure Portal](data-lake-store-get-started-portal.md).

## <a name="enable-diagnostic-logging-for-your-data-lake-store-account"></a>Activer la journalisation de diagnostic pour votre compte Data Lake Store
1. Ouverture de session toohello nouvelle [Azure Portal](https://portal.azure.com).
2. Ouvrez votre compte Data Lake Store et, dans le panneau de votre compte Data Lake Store, cliquez sur **Paramètres** puis sur **Paramètres de diagnostic**.
3. Bonjour **les journaux de diagnostic** panneau, cliquez sur **activer les diagnostics**.

    ![Activer la journalisation des diagnostics](./media/data-lake-store-diagnostic-logs/turn-on-diagnostics.png "Activer les journaux de diagnostic")

3. Bonjour **Diagnostic** panneau, rendre hello après la journalisation des diagnostics tooconfigure modifications.
   
    ![Activer la journalisation des diagnostics](./media/data-lake-store-diagnostic-logs/enable-diagnostic-logs.png "Activer les journaux de diagnostic")
   
   * Définissez **état** trop**sur** tooenable journalisation des Diagnostics.
   * Vous pouvez choisir les données toostore/processus hello de différentes façons.
     
        * L’option hello trop**archiver le compte de stockage tooa** toostore enregistre le compte de stockage Azure tooan. Vous utilisez cette option si vous souhaitez que les données de hello tooarchive qui seront lot traité à une date ultérieure. Si vous sélectionnez cette option vous devez fournir un compte Azure Storage toosave journaux hello.
        
        * L’option hello trop**concentrateur d’événements de flux tooan** tooan de données de journal toostream concentrateur d’événements Azure. Très probablement vous utiliserez cette option si vous disposez d’un traitement en aval pipeline tooanalyze les journaux entrant en temps réel. Si vous sélectionnez cette option, vous devez fournir les détails de hello pour hello concentrateur d’événements Azure vous souhaitez toouse.

        * L’option hello trop**envoyer tooLog Analytique** toouse hello données du journal Analytique de journal Azure service tooanalyze hello généré. Si vous sélectionnez cette option, vous devez fournir hello détails pour l’espace de travail Operations Management Suite hello que vous utilisez hello effectue l’analyse du journal.
     
   * Spécifiez si vous souhaitez que les journaux d’audit de tooget ou les journaux des requêtes ou les deux.
   * Spécifiez les nombre hello de jours pour lequel les données de salutation doivent être conservées. Rétention s’applique uniquement si vous utilisez des données de journal de tooarchive de compte de stockage Azure.
   * Cliquez sur **Enregistrer**.

Une fois que vous avez activé les paramètres de diagnostic, vous pouvez regarder hello se connecte hello **journaux de Diagnostic** onglet.

## <a name="view-diagnostic-logs-for-your-data-lake-store-account"></a>Afficher les journaux de diagnostic de votre compte Data Lake Store
Il existe deux façons de données du journal tooview hello pour votre compte Data Lake Store.

* Afficher les paramètres de compte Data Lake Store de hello
* À partir du compte de stockage Azure hello où sont stockées les données hello

### <a name="using-hello-data-lake-store-settings-view"></a>Afficher les paramètres de magasin de LAC de données à l’aide de hello
1. Dans le panneau **Paramètres** de votre compte Data Lake Store, cliquez sur **Journaux de diagnostic**.
   
    ![Afficher la journalisation des diagnostics](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs.png "Afficher les journaux de diagnostic") 
2. Bonjour **journaux de Diagnostic** panneau, vous devez voir les journaux hello classés par **les journaux d’Audit** et **les journaux de demandes**.
   
   * Les journaux de demandes de capture chaque demande d’API effectué sur hello compte Data Lake Store.
   * Journaux d’audit sont les journaux toorequest similaire, mais fournissent une analyse beaucoup plus détaillée des opérations hello en cours d’exécution sur le compte Data Lake Store de hello. Par exemple, un appel d’API téléchargement unique dans les journaux de demandes peut entraîner plusieurs opérations « Ajouter » dans les journaux d’audit de hello.
3. Cliquez sur hello **télécharger** lien sur chaque journal journaux toodownload hello.

### <a name="from-hello-azure-storage-account-that-contains-log-data"></a>À partir de hello compte de stockage Azure qui contient les données du journal
1. Ouvrir le panneau de compte de stockage Azure hello associé Data Lake Store pour la journalisation, puis cliquez sur objets BLOB. Hello **service Blob** panneau répertorie deux conteneurs.
   
    ![Afficher la journalisation des diagnostics](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account.png "Afficher les journaux de diagnostic")
   
   * conteneur de Hello **insights-journaux-audit** contient les journaux d’audit de hello.
   * conteneur de Hello **demandes de journaux insights** contient les journaux de demandes hello.
2. Ces conteneurs, les journaux de hello sont stockés sous hello suivant la structure.
   
    ![Afficher la journalisation des diagnostics](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account-structure.png "Afficher les journaux de diagnostic")
   
    Par exemple, le chemin d’accès complet de hello tooan log peut être`https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=04/m=00/PT1H.json`
   
    De même, journal des demandes tooa hello chemin d’accès complet peut être`https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=14/m=00/PT1H.json`

## <a name="understand-hello-structure-of-hello-log-data"></a>Comprendre la structure de hello hello des données de journaux
Hello journaux d’audit et de la demande sont dans un format JSON. Dans cette section, nous examiner la structure hello de JSON pour la demande et journaux d’audit.

### <a name="request-logs"></a>journaux de demande
Voici un exemple d’entrée dans le journal au format JSON de demande de hello. Chaque objet blob a un objet racine appelé **enregistrements** qui contient un tableau d’objets du journal.

    {
    "records": 
      [        
        . . . .
        ,
        {
             "time": "2016-07-07T21:02:53.456Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/<data_lake_store_account_name>",
             "category": "Requests",
             "operationName": "GETCustomerIngressEgress",
             "resultType": "200",
             "callerIpAddress": "::ffff:1.1.1.1",
             "correlationId": "4a11c709-05f5-417c-a98d-6e81b3e29c58",
             "identity": "1808bd5f-62af-45f4-89d8-03c5e81bac30",
             "properties": {"HttpMethod":"GET","Path":"/webhdfs/v1/Samples/Outputs/Drivers.csv","RequestContentLength":0,"ClientRequestId":"3b7adbd9-3519-4f28-a61c-bd89506163b8","StartTime":"2016-07-07T21:02:52.472Z","EndTime":"2016-07-07T21:02:53.456Z"}
        }
        ,
        . . . .
      ]
    }

#### <a name="request-log-schema"></a>Schéma du journal de requête
| Name | Type | Description |
| --- | --- | --- |
| time |String |Hello horodateur (UTC) du journal de hello |
| resourceId |String |ID de Hello de ressource hello opération placer sur |
| category |String |catégorie de journal Hello. Par exemple, **Demandes**. |
| operationName |String |Nom de l’opération hello est connectée. Par exemple, getfilestatus. |
| resultType |String |état Hello d’opération hello, par exemple, 200. |
| callerIpAddress |String |adresse IP de Hello du client hello hello demande |
| correlationId |String |id de Hello du journal hello qui permet de toogroup ensemble un ensemble d’entrées de journal connexes |
| identité |Object |identité Hello qui a généré hello journal |
| properties |JSON |Voir les détails ci-dessous. |

#### <a name="request-log-properties-schema"></a>Schéma des propriétés de journal de demande
| Name | Type | Description |
| --- | --- | --- |
| HttpMethod |String |Hello méthode HTTP utilisée pour l’opération de hello. Par exemple, GET. |
| Chemin |String |opération hello Hello a été effectuée sur |
| RequestContentLength |int |longueur du contenu de la demande de hello HTTP Hello |
| ClientRequestId |String |Hello Id qui identifie cette demande |
| StartTime |String |heure Hello qui demande hello du serveur reçues hello |
| EndTime |String |temps de Hello à quels hello serveur a envoyé une réponse |

### <a name="audit-logs"></a>Journaux d’audit
Voici un exemple d’entrée dans le journal d’audit d’au format JSON hello. Chaque objet blob a un objet racine appelé **records** qui contient un tableau d’objets du journal

    {
    "records": 
      [        
        . . . .
        ,
        {
             "time": "2016-07-08T19:08:59.359Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/<data_lake_store_account_name>",
             "category": "Audit",
             "operationName": "SeOpenStream",
             "resultType": "0",
             "correlationId": "381110fc03534e1cb99ec52376ceebdf;Append_BrEKAmg;25.66.9.145",
             "identity": "A9DAFFAF-FFEE-4BB5-A4A0-1B6CBBF24355",
             "properties": {"StreamName":"adl://<data_lake_store_account_name>.azuredatalakestore.net/logs.csv"}
        }
        ,
        . . . .
      ]
    }

#### <a name="audit-log-schema"></a>Schéma du journal d’audit
| Name | Type | Description |
| --- | --- | --- |
| time |String |Hello horodateur (UTC) du journal de hello |
| resourceId |String |ID de Hello de ressource hello opération placer sur |
| category |String |catégorie de journal Hello. Par exemple, **Audit**. |
| operationName |String |Nom de l’opération hello est connectée. Par exemple, getfilestatus. |
| resultType |String |état Hello d’opération hello, par exemple, 200. |
| correlationId |String |id de Hello du journal hello qui permet de toogroup ensemble un ensemble d’entrées de journal connexes |
| identité |Object |identité Hello qui a généré hello journal |
| properties |JSON |Voir les détails ci-dessous. |

#### <a name="audit-log-properties-schema"></a>Schéma des propriétés de journal d’audit
| Name | Type | Description |
| --- | --- | --- |
| StreamName |String |opération hello Hello a été effectuée sur |

## <a name="samples-tooprocess-hello-log-data"></a>Données du journal hello exemples tooprocess
Azure Data Lake Store fournit un exemple sur la façon de tooprocess et analyser les données de journal hello. Vous trouverez un exemple hello à [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample). 

## <a name="see-also"></a>Voir aussi
* [Présentation d'Azure Data Lake Store](data-lake-store-overview.md)
* [Sécuriser les données dans Data Lake Store](data-lake-store-secure-data.md)

