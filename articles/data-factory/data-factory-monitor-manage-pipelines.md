---
title: "aaaMonitor et gérer des pipelines à l’aide de hello portail Azure et PowerShell | Documents Microsoft"
description: "Découvrez comment toouse hello portail Azure et Azure PowerShell toomonitor et gérer des fabriques de données Azure hello et pipelines que vous avez créés."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 9b0fdc59-5bbe-44d1-9ebc-8be14d44def9
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: spelluru
ms.openlocfilehash: a8d3c7943e79450895ff754f06a37fdad1cbef92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-hello-azure-portal-and-powershell"></a>Surveiller et gérer les pipelines Azure Data Factory à l’aide de hello portail Azure et PowerShell
> [!div class="op_single_selector"]
> * [Utilisation du portail Azure/d’Azure PowerShell](data-factory-monitor-manage-pipelines.md)
> * [Utilisation de l’application de surveillance et gestion](data-factory-monitor-manage-app.md)


> [!IMPORTANT]
> application de gestion et d’analyse Hello fournit une meilleure prise en charge pour l’analyse et la gestion de vos pipelines de données et les problèmes de résolution des problèmes. Pour plus d’informations sur l’utilisation d’application hello, consultez [surveiller et gérer des pipelines de fabrique de données à l’aide d’application de gestion et de surveillance hello](data-factory-monitor-manage-app.md). 


Cet article décrit comment toomonitor, gérer et déboguer vos pipelines à l’aide de PowerShell et le portail Azure. Hello fournit également des informations sur les alertes toocreate et obtenir informées des échecs.

## <a name="understand-pipelines-and-activity-states"></a>Présentation des pipelines et des états d’activité
À l’aide de hello portail Azure, vous pouvez :

* Afficher votre fabrique de données sous forme de schéma.
* Afficher les activités à l’intérieur d’un pipeline.
* Afficher des jeux de données d’entrée et de sortie.

Cette section décrit également comment une tranche du jeu de données passe à partir d’un état de tooanother.   

### <a name="navigate-tooyour-data-factory"></a>Accédez de fabrique de données tooyour
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Cliquez sur **fabriques de données** dans menu hello hello gauche. Si vous ne le voyez pas, cliquez sur **davantage de services >**, puis cliquez sur **fabriques de données** sous hello **INTELLIGENCE + ANALYTICS** catégorie.

   ![Parcourir tout > Fabriques de données](./media/data-factory-monitor-manage-pipelines/browseall-data-factories.png)
3. Sur hello **fabriques de données** panneau, la fabrique de données Sélectionnez hello qui vous intéressent.

    ![Sélectionner une fabrique de données](./media/data-factory-monitor-manage-pipelines/select-data-factory.png)

   Vous devez voir la page d’accueil hello de fabrique de données hello.

   ![Panneau Data Factory](./media/data-factory-monitor-manage-pipelines/data-factory-blade.png)

#### <a name="diagram-view-of-your-data-factory"></a>Vue schématique de votre fabrique de données
Hello **diagramme** vue d’une fabrique de données fournit un volet de verre toomonitor et gérer hello data factory et ses composants. toosee hello **diagramme** afficher votre fabrique de données, cliquez sur **diagramme** sur la page d’accueil hello de fabrique de données hello.

![Vue schématique](./media/data-factory-monitor-manage-pipelines/diagram-view.png)

Vous pouvez faire un zoom, effectuer un zoom arrière, zoom toofit, zoom too100 %, disposition de hello de verrou de schéma de hello et positionnez automatiquement les pipelines et les jeux de données. Vous pouvez également voir les informations de lignage des données hello (autrement dit, afficher les éléments en amont et en aval des éléments sélectionnés).

### <a name="activities-inside-a-pipeline"></a>Activités à l'intérieur d'un pipeline
1. Pipeline de hello d’avec le bouton droit, puis cliquez sur **ouvrir pipeline** toosee toutes les activités de hello de pipeline, ainsi que des jeux de données d’entrée et de sortie pour les activités de hello. Cette fonctionnalité est utile lorsque votre pipeline inclut plusieurs activités et que vous souhaitez lignage opérationnelle de hello toounderstand d’un pipeline unique.

    ![Menu Ouvrir un pipeline](./media/data-factory-monitor-manage-pipelines/open-pipeline-menu.png)     
2. Dans l’exemple suivant de hello, vous voyez une activité de copie dans le pipeline hello avec une entrée et une sortie. 

    ![Activités à l'intérieur d'un pipeline](./media/data-factory-monitor-manage-pipelines/activities-inside-pipeline.png)
3. Vous pouvez naviguer de page d’accueil toohello arrière hello fabrique de données en cliquant sur hello **Data factory** lien dans la barre de navigation hello en haut à gauche de hello.

    ![Accédez toodata arrière fabrique](./media/data-factory-monitor-manage-pipelines/navigate-back-to-data-factory.png)

### <a name="view-hello-state-of-each-activity-inside-a-pipeline"></a>État d’affichage hello de chaque activité à l’intérieur d’un pipeline
Vous pouvez afficher l’état actuel de hello d’une activité en consultant l’état hello de hello des jeux de données qui est produites par l’activité hello.

En double-cliquant sur hello **OutputBlobTable** Bonjour **diagramme**, vous pouvez voir toutes les tranches hello produites par les exécutions d’activité différente à l’intérieur d’un pipeline. Vous pouvez voir que l’activité de copie hello a été correctement exécuté pour hello huit dernières heures et produits tranches hello Bonjour **prêt** état.  

![État du pipeline de hello](./media/data-factory-monitor-manage-pipelines/state-of-pipeline.png)

tranches de dataset Hello dans la fabrique de données hello peuvent prendre de hello suivant des États :

<table>
<tr>
    <th align="left">State</th><th align="left">Sous-état</th><th align="left">Description</th>
</tr>
<tr>
    <td rowspan="8">En attente</td><td>ScheduleTime</td><td>temps de Hello n’a pas encore être motivée par de hello tranche toorun.</td>
</tr>
<tr>
<td>DatasetDependencies</td><td>les dépendances en amont Hello ne sont pas prêts.</td>
</tr>
<tr>
<td>ComputeResources</td><td>ressources de calcul Hello ne sont pas disponibles.</td>
</tr>
<tr>
<td>ConcurrencyLimit</td> <td>Toutes les instances d’activité hello sont occupés à exécuter d’autres tranches.</td>
</tr>
<tr>
<td>ActivityResume</td><td>activité Hello est suspendue et ne peut pas exécuter les tranches hello jusqu'à ce que l’activité hello est reprise.</td>
</tr>
<tr>
<td>Retry</td><td>L’exécution de l’activité est retentée.</td>
</tr>
<tr>
<td>Validation</td><td>La validation n’a pas encore démarré.</td>
</tr>
<tr>
<td>ValidationRetry</td><td>La validation est toobe en attente une nouvelle tentée.</td>
</tr>
<tr>
<tr>
<td rowspan="2">InProgress</td><td>Validation</td><td>La validation est en cours.</td>
</tr>
<td>-</td>
<td>la tranche de Hello est en cours de traitement.</td>
</tr>
<tr>
<td rowspan="4">Échec</td><td>TimedOut</td><td>exécution de l’activité Hello a pris plus de temps que ce qui est autorisé par activité hello.</td>
</tr>
<tr>
<td>Canceled</td><td>la tranche de Hello a été annulée par l’utilisateur.</td>
</tr>
<tr>
<td>Validation</td><td>La validation a échoué.</td>
</tr>
<tr>
<td>-</td><td>Échec de la tranche de Hello toobe généré et/ou validé.</td>
</tr>
<td>Ready</td><td>-</td><td>tranche de Hello est prêt à être utilisé.</td>
</tr>
<tr>
<td>Ignoré</td><td>Aucun</td><td>la tranche de Hello n’est pas en cours de traitement.</td>
</tr>
<tr>
<td>Aucun</td><td>-</td><td>Une tranche utilisé tooexist avec un état différent, mais il a été réinitialisé.</td>
</tr>
</table>



Vous pouvez afficher les détails de hello sur une section en cliquant sur une entrée de la tranche sur hello **récemment mis à jour les tranches** panneau.

![Détails de la tranche](./media/data-factory-monitor-manage-pipelines/slice-details.png)

Si la tranche de hello a été exécutée plusieurs fois, vous voyez plusieurs lignes Bonjour **activité s’exécute** liste. Vous pouvez afficher des détails sur une activité à exécuter en cliquant sur entrée hello exécuter Bonjour **activité s’exécute** liste. liste de Hello montre tous les fichiers journaux hello, ainsi que d’un message d’erreur si elle existe. Cette fonctionnalité est utiles journaux tooview et de débogage sans avoir tooleave votre fabrique de données.

![Détails de l'exécution d'activité](./media/data-factory-monitor-manage-pipelines/activity-run-details.png)

Si la tranche de hello n’est pas Bonjour **prêt** état, vous pouvez voir les tranches en amont hello qui ne sont pas prêts et bloquent tranche à partir de l’exécution dans hello hello **tranches en amont qui ne sont pas prêtes** liste. Cette fonctionnalité est utile lorsque votre tranche est dans **attente** état et que vous souhaitez toounderstand hello en amont dépendances hello tranche est en attente.

![Tranches en amont qui ne sont pas prêtes](./media/data-factory-monitor-manage-pipelines/upstream-slices-not-ready.png)

### <a name="dataset-state-diagram"></a>Schéma d’état de jeux de données
Une fois que vous déployez une fabrique de données et les pipelines hello ont une période active valide, hello dataset tranches transition à partir d’un état tooanother. Actuellement, état de la tranche hello suit hello suivant le diagramme d’état :

![Schéma d'état](./media/data-factory-monitor-manage-pipelines/state-diagram.png)

jeu de données des flux de transition d’état dans la fabrique de données Hello sont suivant de hello : en attente -> en cours/en cours (validation) -> Échec prêt.

la tranche de Hello démarre dans un **en attente** état, en attente de toobe les conditions préalables remplie avant qu’elle s’exécute. Ensuite, activité hello commence à s’exécuter et tranche de hello sont placées dans un **en cours d’exécution** état. exécution de l’activité Hello peut réussissent ou échouent. la tranche de Hello est marquée comme **prêt** ou **n’a pas pu**, en fonction de résultats de l’exécution de hello hello.

Vous pouvez réinitialiser toogo de tranche hello de hello **prêt** ou **n’a pas pu** état toohello **attente** état. Vous pouvez également marquer l’état de tranche hello trop**ignorer**, ce qui empêche l’activité hello à partir de l’exécution et ne traite ne pas les tranches hello.

## <a name="pause-and-resume-pipelines"></a>Suspension et reprise des pipelines
Vous pouvez gérer vos pipelines à l’aide d’Azure PowerShell. Par exemple, vous pouvez suspendre et reprendre les pipelines en exécutant les applets de commande Azure PowerShell. 

> [!NOTE] 
> affichage des diagrammes Hello ne prend pas en charge la suspension et reprise des pipelines. Si vous souhaitez toouse une interface utilisateur, utilisez hello analyse et la gestion d’application. Pour plus d’informations sur l’utilisation d’application hello, consultez [surveiller et gérer des pipelines de fabrique de données à l’aide d’application de gestion et de surveillance hello](data-factory-monitor-manage-app.md) l’article. 

Vous pouvez suspendre/suspendre pipelines à l’aide de hello **Suspend-AzureRmDataFactoryPipeline** applet de commande PowerShell. Cette applet de commande est utile lorsque vous ne souhaitez pas que toorun vos pipelines jusqu'à ce qu’un problème est résolu. 

```powershell
Suspend-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
Par exemple :

```powershell
Suspend-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

Après que hello problème résolu avec le pipeline de hello, vous pouvez reprendre le pipeline de hello suspendu en exécutant hello suivant de commande PowerShell :

```powershell
Resume-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
Par exemple :

```powershell
Resume-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

## <a name="debug-pipelines"></a>Débogage de pipelines
Azure Data Factory fournit des fonctionnalités enrichies vous toodebug et résoudre les problèmes de pipelines à l’aide de hello portail Azure et Azure PowerShell.

> [! Notez} il est beaucoup plus facile tootroubleshot erreurs à l’aide de hello analyse & application de gestion. Pour plus d’informations sur l’utilisation d’application hello, consultez [surveiller et gérer des pipelines de fabrique de données à l’aide d’application de gestion et de surveillance hello](data-factory-monitor-manage-app.md) l’article. 

### <a name="find-errors-in-a-pipeline"></a>Recherche d’erreurs dans un pipeline
En cas d’exécution de l’activité hello dans un pipeline, hello de jeu de données qui est généré par le pipeline de hello est dans un état d’erreur en raison de l’échec de hello. Vous pouvez déboguer et résoudre les erreurs dans Azure Data Factory à l’aide des méthodes suivantes de hello.

#### <a name="use-hello-azure-portal-toodebug-an-error"></a>Utilisez hello toodebug portail Azure une erreur
1. Sur hello **Table** panneau, cliquez sur le secteur problème hello a hello **état** défini trop**n’a pas pu**.

   ![Panneau de table avec tranche problématique](./media/data-factory-monitor-manage-pipelines/table-blade-with-error.png)
2. Sur hello **tranche de données** panneau, cliquez sur activité hello qui a échoué.

   ![Tranche de données avec une erreur](./media/data-factory-monitor-manage-pipelines/dataslice-with-error.png)
3. Sur hello **détails de l’exécution activité** panneau, vous pouvez télécharger les fichiers de hello qui sont associés au traitement de HDInsight hello. Cliquez sur **télécharger** état/stderr toodownload hello fichier journal des erreurs qui contient des détails sur l’erreur de hello.

   ![Panneau de détails sur l’exécution d’activité](./media/data-factory-monitor-manage-pipelines/activity-run-details-with-error.png)     

#### <a name="use-powershell-toodebug-an-error"></a>Utilisez PowerShell toodebug une erreur
1. Lancez **PowerShell**.
2. Exécutez hello **Get-AzureRmDataFactorySlice** commande tranches de hello toosee et leurs États. Vous devez voir une tranche dont l’état hello **n’a pas pu**.        

    ```powershell   
    Get-AzureRmDataFactorySlice [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime] <DateTime> [[-EndDateTime] <DateTime> ] [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```   
   Par exemple :

    ```powershell   
    Get-AzureRmDataFactorySlice -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime 2014-05-04 20:00:00
    ```

   Remplacez **StartDateTime** par l’heure de début de votre pipeline. 
3. Exécutez maintenant hello **Get-AzureRmDataFactoryRun** tooget détails sur l’activité hello exécuter de la tranche de hello.

    ```powershell   
    Get-AzureRmDataFactoryRun [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime]
    <DateTime> [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```

    Par exemple :

    ```powershell   
    Get-AzureRmDataFactoryRun -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime "5/5/2014 12:00:00 AM"
    ```

    valeur Hello %StartDateTime;) est heure de début hello pour tranche d’erreur/problème hello que vous avez noté à l’étape précédente de hello. Hello date-heure doit être entourée de guillemets doubles.
4. Sortie avec des détails sur l’erreur de hello est similaire toohello suivant doit s’afficher :

    ```   
    Id                      : 841b77c9-d56c-48d1-99a3-8c16c3e77d39
    ResourceGroupName       : ADF
    DataFactoryName         : LogProcessingFactory3
    DatasetName               : EnrichedGameEventsTable
    ProcessingStartTime     : 10/10/2014 3:04:52 AM
    ProcessingEndTime       : 10/10/2014 3:06:49 AM
    PercentComplete         : 0
    DataSliceStart          : 5/5/2014 12:00:00 AM
    DataSliceEnd            : 5/6/2014 12:00:00 AM
    Status                  : FailedExecution
    Timestamp               : 10/10/2014 3:04:52 AM
    RetryAttempt            : 0
    Properties              : {}
    ErrorMessage            : Pig script failed with exit code '5'. See wasb://        adfjobs@spestore.blob.core.windows.net/PigQuery
                                    Jobs/841b77c9-d56c-48d1-99a3-
                8c16c3e77d39/10_10_2014_03_04_53_277/Status/stderr' for
                more details.
    ActivityName            : PigEnrichLogs
    PipelineName            : EnrichGameLogsPipeline
    Type                    :
    ```
5. Vous pouvez exécuter hello **Save-AzureRmDataFactoryLog** applet de commande avec hello valeur d’Id que vous consultez à partir de la sortie de hello et téléchargez les fichiers de journaux hello à l’aide de hello **- DownloadLogsoption** pour l’applet de commande hello.

    ```powershell
    Save-AzureRmDataFactoryLog -ResourceGroupName "ADF" -DataFactoryName "LogProcessingFactory" -Id "841b77c9-d56c-48d1-99a3-8c16c3e77d39" -DownloadLogs -Output "C:\Test"
    ```

## <a name="rerun-failures-in-a-pipeline"></a>Réexécuter des échecs dans un pipeline

> [!IMPORTANT]
> Il est plus facile tootroubleshoot erreurs et réexécuter tranches ayant échouées à l’aide de hello analyse & application de gestion. Pour plus d’informations sur l’utilisation d’application hello, consultez [surveiller et gérer des pipelines de fabrique de données à l’aide d’application de gestion et de surveillance hello](data-factory-monitor-manage-app.md). 

### <a name="use-hello-azure-portal"></a>Utilisez hello portail Azure
Après avoir résoudre les problèmes et déboguer les erreurs dans un pipeline, vous pouvez réexécuter des échecs par tranche d’erreur toohello en cliquant sur hello **exécuter** bouton de barre de commandes hello.

![Réexécuter une tranche de données ayant échoué](./media/data-factory-monitor-manage-pipelines/rerun-slice.png)

Dans le cas de tranche de hello Échec de la validation en raison d’un échec de la stratégie (par exemple, si des données n’est pas disponibles), vous pouvez corriger l’échec de hello et valider de nouveau en cliquant sur hello **Validate** bouton de barre de commandes hello.

![Corriger les erreurs et valider](./media/data-factory-monitor-manage-pipelines/fix-error-and-validate.png)

### <a name="use-azure-powershell"></a>Utilisation d'Azure PowerShell
Vous pouvez réexécuter les défaillances à l’aide de hello **Set-AzureRmDataFactorySliceStatus** applet de commande. Consultez hello [Set-AzureRmDataFactorySliceStatus](https://msdn.microsoft.com/library/mt603522.aspx) rubrique pour la syntaxe et d’autres détails sur l’applet de commande hello.

**Exemple :**

exemple Hello définit état hello de toutes les tranches pour hello table 'DAWikiAggregatedData' too'Waiting' dans la fabrique de données Azure hello 'WikiADF'.

Hello 'Type' a la valeur too'UpstreamInPipeline ', ce qui signifie que les États de chaque secteur pour la table de hello et toutes les tables (en amont) dépendants hello sont définies too'Waiting'. Bonjour autre valeur possible pour ce paramètre est « Individuel ».

```powershell
Set-AzureRmDataFactorySliceStatus -ResourceGroupName ADF -DataFactoryName WikiADF -DatasetName DAWikiAggregatedData -Status Waiting -UpdateType UpstreamInPipeline -StartDateTime 2014-05-21T16:00:00 -EndDateTime 2014-05-21T20:00:00
```

## <a name="create-alerts"></a>Créez des alertes
Azure consigne les événements utilisateur lorsqu'une ressource Azure (par exemple, une fabrique de données) est créée, mise à jour ou supprimée. Vous pouvez créer des alertes relatives à ces événements. Vous pouvez utiliser Data Factory toocapture diverses métriques et créer des alertes sur des métriques. Nous vous recommandons d’utiliser les événements pour obtenir une surveillance en temps réel et les mesures à des fins d’historique.

### <a name="alerts-on-events"></a>Alertes relatives à des événements
Les événements Azure fournissent des explications utiles sur ce qui se passe dans vos ressources Azure. Lorsque vous utilisez Azure Data Factory, les événements sont générés quand :

* Une fabrique de données est créée, mise à jour ou supprimée.
* Le traitement des données (les « exécutions ») est démarré ou terminé.
* Un cluster HDInsight à la demande est créé ou supprimé.

Vous pouvez créer des alertes sur ces événements utilisateur et les configurer à l’administrateur de toohello toosend par courrier électronique des notifications et coadministrators d’abonnement de hello. En outre, vous pouvez spécifier des adresses de messagerie supplémentaires des utilisateurs qui ont besoin de notifications par courrier électronique de tooreceive lorsque hello conditions sont remplies. Cette fonctionnalité est utile quand vous voulez tooget informé sur les échecs et que vous ne souhaitez pas que toocontinuously analyse votre fabrique de données.

> [!NOTE]
> Actuellement, le portail de hello n’affiche pas les alertes sur les événements. Hello d’utilisation [analyse et gestion d’application](data-factory-monitor-manage-app.md) toosee toutes les alertes.


#### <a name="specify-an-alert-definition"></a>Spécifier une définition d’alerte
toospecify une définition d’alerte, vous créez un fichier JSON qui décrit les opérations hello toobe alerté sur souhaitées. Dans l’exemple suivant de hello, alerte de hello envoie une notification par courrier électronique pour hello RunFinished opération. toobe spécifique, une notification par courrier électronique est envoyée lorsqu’une exécution dans la fabrique de données hello est terminée et hello exécuter a échoué (état = FailedExecution).

```JSON
{
    "contentVersion": "1.0.0.0",
     "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "parameters": {},
    "resources":
    [
        {
            "name": "ADFAlertsSlice",
            "type": "microsoft.insights/alertrules",
            "apiVersion": "2014-04-01",
            "location": "East US",
            "properties":
            {
                "name": "ADFAlertsSlice",
                "description": "One or more of hello data slices for hello Azure Data Factory has failed processing.",
                "isEnabled": true,
                "condition":
                {
                    "odata.type": "Microsoft.Azure.Management.Insights.Models.ManagementEventRuleCondition",
                    "dataSource":
                    {
                        "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleManagementEventDataSource",
                        "operationName": "RunFinished",
                        "status": "Failed",
                        "subStatus": "FailedExecution"   
                    }
                },
                "action":
                {
                    "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
                    "customEmails": [ "<your alias>@contoso.com" ]
                }
            }
        }
    ]
}
```

Vous pouvez supprimer **sous-état** de hello définition JSON si vous ne souhaitez pas toobe averti en cas d’échec spécifique.

Cet exemple configure alerte hello pour toutes les fabriques de données dans votre abonnement. Si vous souhaitez hello alerte toobe est défini pour une fabrique de données particulière, vous pouvez spécifier la fabrique de données **resourceUri** Bonjour **source de données**:

```JSON
"resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>"
```

Hello tableau suivant fournit hello liste des opérations disponibles et les États (sous-états).

| Nom d’opération | État | État secondaire |
| --- | --- | --- |
| RunStarted |Démarré |Starting |
| RunFinished |Failed / Succeeded |FailedResourceAllocation<br/><br/>Succeeded<br/><br/>FailedExecution<br/><br/>TimedOut<br/><br/><Canceled<br/><br/>FailedValidation<br/><br/>Abandonné |
| OnDemandClusterCreateStarted |Démarré | |
| OnDemandClusterCreateSuccessful |Réussi | |
| OnDemandClusterDeleted |Réussi | |

Consultez [créer une règle d’alerte](https://msdn.microsoft.com/library/azure/dn510366.aspx) pour plus d’informations sur les éléments JSON hello qui sont utilisés dans l’exemple de hello.

#### <a name="deploy-hello-alert"></a>Déployer l’alerte de hello
alerte de hello toodeploy, applet de commande Azure PowerShell utilisez hello **New-AzureRmResourceGroupDeployment**, comme indiqué dans hello l’exemple suivant :

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\ADFAlertFailedSlice.json  
```

Une fois le déploiement de groupe de ressources hello terminée avec succès, vous voyez hello suivant des messages :

```
VERBOSE: 7:00:48 PM - Template is valid.
WARNING: 7:00:48 PM - hello StorageAccountName parameter is no longer used and will be removed in a future release.
Please update scripts tooremove this parameter.
VERBOSE: 7:00:49 PM - Create template deployment 'ADFAlertFailedSlice'.
VERBOSE: 7:00:57 PM - Resource microsoft.insights/alertrules 'ADFAlertsSlice' provisioning status is succeeded

DeploymentName    : ADFAlertFailedSlice
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 10/11/2014 2:01:00 AM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           :
```

> [!NOTE]
> Vous pouvez utiliser hello [créer une règle d’alerte](https://msdn.microsoft.com/library/azure/dn510366.aspx) API REST toocreate une règle d’alerte. charge utile JSON de Hello est un exemple JSON toohello similaire.  


#### <a name="retrieve-hello-list-of-azure-resource-group-deployments"></a>Récupérer la liste de hello de déploiements de groupes de ressources Azure
liste de hello tooretrieve des déployé des déploiements de groupes de ressources Azure, utilisez l’applet de commande hello **Get-AzureRmResourceGroupDeployment**, comme indiqué dans hello l’exemple suivant :

```powershell
Get-AzureRmResourceGroupDeployment -ResourceGroupName adf
```

```
DeploymentName    : ADFAlertFailedSlice
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 10/11/2014 2:01:00 AM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           :
```

#### <a name="troubleshoot-user-events"></a>Résoudre les problèmes relatifs aux événements utilisateur
1. Vous pouvez voir tous les événements de hello qui sont générés après avoir cliqué sur hello **métriques et les opérations** vignette.

    ![Vignette Mesures et opérations](./media/data-factory-monitor-manage-pipelines/metrics-and-operations-tile.png)
2. Cliquez sur hello **événements** vignette événements de hello toosee.

    ![Vignette d'événements](./media/data-factory-monitor-manage-pipelines/events-tile.png)
3. Sur hello **événements** panneau, vous pouvez voir les détails sur les événements, événements filtrés et ainsi de suite.

    ![Panneau Événements](./media/data-factory-monitor-manage-pipelines/events-blade.png)
4. Cliquez sur un **opération** dans la liste des opérations hello qui provoque une erreur.

    ![Sélectionner une opération](./media/data-factory-monitor-manage-pipelines/select-operation.png)
5. Cliquez sur un **erreur** toosee détails de l’événement sur l’erreur de hello.

    ![Événement erreur](./media/data-factory-monitor-manage-pipelines/operation-error-event.png)

Consultez [applets de commande Azure Insight](https://msdn.microsoft.com/library/mt282452.aspx) pour les applets de commande PowerShell que vous pouvez utiliser tooadd, obtenir ou supprimer des alertes. Voici quelques exemples d’utilisation de hello **Get-AlertRule** applet de commande :

```powershell
get-alertrule -res $resourceGroup -n ADFAlertsSlice -det
```

```
Properties :
Action      : Microsoft.Azure.Management.Insights.Models.RuleEmailAction
Condition   :
DataSource :
EventName             :
Category              :
Level                 :
OperationName         : RunFinished
ResourceGroupName     :
ResourceProviderName  :
ResourceId            :
Status                : Failed
SubStatus             : FailedExecution
Claims                : Microsoft.Azure.Management.Insights.Models.RuleManagementEventClaimsDataSource
Condition      :
Description : One or more of hello data slices for hello Azure Data Factory has failed processing.
Status      : Enabled
Name:       : ADFAlertsSlice
Tags       :
$type          : Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage
Id: /subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/ADFAlertsSlice
Location   : West US
Name       : ADFAlertsSlice
```

```powershell
Get-AlertRule -res $resourceGroup
```
```
Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest0
Location   : West US
Name       : FailedExecutionRunsWest0

Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest3
Location   : West US
Name       : FailedExecutionRunsWest3
```

```powershell
Get-AlertRule -res $resourceGroup -Name FailedExecutionRunsWest0
```

```
Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest0
Location   : West US
Name       : FailedExecutionRunsWest0
```

Exécutez hello suivant get-help commandes toosee détails et des exemples d’applet de commande Get-AlertRule hello.

```powershell
get-help Get-AlertRule -detailed
```

```powershell
get-help Get-AlertRule -examples
```


Si vous voyez des événements de génération d’alertes de hello sur hello panneau portail, mais vous ne recevez pas de notifications par courrier électronique, vérifier si l’adresse de messagerie hello est spécifié a des messages électroniques tooreceive des expéditeurs externes. Il se peuvent que des messages d’alerte Hello ont été bloqués par vos paramètres de messagerie.

### <a name="alerts-on-metrics"></a>Alertes relatives à des mesures
Dans Data Factory, vous pouvez capturer différentes mesures et créer des alertes associées. Vous pouvez analyser et créer des alertes sur hello suivant métriques pour les tranches hello dans votre fabrique de données :

* **Exécutions échouées**
* **Exécutions réussies**

Ces mesures sont utiles et vous aider à tooget qu'une vue d’ensemble de globale ayant réussi et s’exécute dans la fabrique de données hello. Des mesures sont émises lors de chaque exécution de tranche de données. Au début de hello d’heure de hello, ces mesures sont agrégées et placé le compte de stockage tooyour. mesures tooenable, configurer un compte de stockage.

#### <a name="enable-metrics"></a>Activer les mesures
tooenable des mesures, cliquez sur suivant hello de hello **Data Factory** panneau :

**Analyse** > **Mesures** > **Paramètres de diagnostic** > **Diagnostics**

![Lien Diagnostics](./media/data-factory-monitor-manage-pipelines/diagnostics-link.png)

Sur hello **Diagnostics** panneau, cliquez sur **sur**, sélectionnez le compte de stockage hello, puis cliquez sur **enregistrer**.

![Panneau Diagnostics](./media/data-factory-monitor-manage-pipelines/diagnostics-blade.png)

Elle peut prendre heure tooone toobe de métriques hello visible sur hello **analyse** panneau parce que l’agrégation de mesures se produit toutes les heures.

### <a name="set-up-an-alert-on-metrics"></a>Configurer une alerte relative à des mesures
Cliquez sur hello **les métriques de Data Factory** vignette :

![Vignette Mesures de fabrique de données](./media/data-factory-monitor-manage-pipelines/data-factory-metrics-tile.png)

Sur hello **métrique** panneau, cliquez sur **+ ajouter une alerte** sur la barre d’outils hello.
![Panneau Mesures de fabrique de données &gt; Ajouter une alerte](./media/data-factory-monitor-manage-pipelines/add-alert.png)

Sur hello **ajouter une règle d’alerte** page, procédez comme hello comme suit, puis cliquez sur **OK**.

* Entrez un nom pour l’alerte de hello (exemple : « Échec de l’alerte »).
* Entrez une description de l’alerte de hello (exemple : « envoyer un courrier électronique lorsqu’une défaillance se produit »).
* Sélectionnez une mesure (« exécutions échouées » ou « exécutions réussies »).
* Spécifiez une condition et une valeur de seuil.   
* Spécifier la période hello.
* Spécifiez si un message électronique doit être envoyé tooowners, les collaborateurs et les lecteurs.

![Panneau Mesures de fabrique de données > Ajouter une règle d’alerte](./media/data-factory-monitor-manage-pipelines/add-an-alert-rule.png)

Une fois que la règle d’alerte hello est ajoutée avec succès, panneau de hello se ferme et vous voyez nouvelle alerte de hello sur hello **métrique** panneau.

![Panneau Mesures de fabrique de données > Nouvelle alerte ajoutée](./media/data-factory-monitor-manage-pipelines/failed-alert-in-metric-blade.png)

Vous devez également voir le nombre de hello d’alertes hello **règles d’alerte** vignette. Cliquez sur hello **règles d’alerte** vignette.

![Panneau Mesures de fabrique de données - Règles d’alerte](./media/data-factory-monitor-manage-pipelines/alert-rules-tile-rules.png)

Sur hello **alertes règles** panneau, vous voyez les alertes existantes. tooadd une alerte, cliquez sur **ajouter une alerte** sur la barre d’outils hello.

![Panneau Règles d’alerte](./media/data-factory-monitor-manage-pipelines/alert-rules-blade.png)

### <a name="alert-notifications"></a>Notifications d’alerte
Une fois que la règle d’alerte hello correspond à la condition de hello, vous devez obtenir un message électronique indiquant que l’alerte de hello est activée. Une fois résolu hello et condition d’alerte hello ne correspond pas à plus, vous obtenez un message électronique indiquant que hello alerte est résolue.

Ce comportement se distingue des événements donnant lieu à l’envoi d’une notification dès qu’un échec correspondant à une règle d’alerte a lieu.

### <a name="deploy-alerts-by-using-powershell"></a>Déployer des alertes à l’aide de PowerShell
Vous pouvez déployer des alertes pour les métriques hello même manière que pour les événements.

**Définition d’alerte**

```JSON
{
    "contentVersion" : "1.0.0.0",
    "$schema" : "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "parameters" : {},
    "resources" : [
    {
            "name" : "FailedRunsGreaterThan5",
            "type" : "microsoft.insights/alertrules",
            "apiVersion" : "2014-04-01",
            "location" : "East US",
            "properties" : {
                "name" : "FailedRunsGreaterThan5",
                "description" : "Failed Runs greater than 5",
                "isEnabled" : true,
                "condition" : {
                    "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.ThresholdRuleCondition, Microsoft.WindowsAzure.Management.Mon.Client",
                    "odata.type" : "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
                    "dataSource" : {
                        "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleMetricDataSource, Microsoft.WindowsAzure.Management.Mon.Client",
                        "odata.type" : "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
                        "resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName
>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>",
                        "metricName" : "FailedRuns"
                    },
                    "threshold" : 5.0,
                    "windowSize" : "PT3H",
                    "timeAggregation" : "Total"
                },
                "action" : {
                    "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleEmailAction, Microsoft.WindowsAzure.Management.Mon.Client",
                    "odata.type" : "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
                    "customEmails" : ["abhinav.gpt@live.com"]
                }
            }
        }
    ]
}
```

Remplacez *subscriptionId*, *resourceGroupName*, et *dataFactoryName* dans l’exemple hello avec les valeurs appropriées.

*metricName* prend actuellement en charge deux valeurs :

* FailedRuns
* SuccessfulRuns

**Déployer l’alerte de hello**

alerte de hello toodeploy, applet de commande Azure PowerShell utilisez hello **New-AzureRmResourceGroupDeployment**, comme indiqué dans hello l’exemple suivant :

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\FailedRunsGreaterThan5.json
```

Le message suivant devrait s’afficher après la réussite du déploiement :

```
VERBOSE: 12:52:47 PM - Template is valid.
VERBOSE: 12:52:48 PM - Create template deployment 'FailedRunsGreaterThan5'.
VERBOSE: 12:52:55 PM - Resource microsoft.insights/alertrules 'FailedRunsGreaterThan5' provisioning status is succeeded


DeploymentName    : FailedRunsGreaterThan5
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 7/27/2015 7:52:56 PM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           
```

Vous pouvez également utiliser hello **Add-AlertRule** toodeploy de l’applet de commande une règle d’alerte. Consultez hello [Add-AlertRule](https://msdn.microsoft.com/library/mt282468.aspx) rubrique pour plus d’informations et des exemples.  

## <a name="move-a-data-factory-tooa-different-resource-group-or-subscription"></a>Déplacer un groupe de ressources différent de données fabrique tooa ou un abonnement
Vous pouvez déplacer un groupe de ressources différent de données fabrique tooa ou un autre abonnement à l’aide de hello **déplacer** barre bouton sur la page d’accueil hello votre fabrique de données de commandes.

![Déplacer la fabrique de données](./media/data-factory-monitor-manage-pipelines/MoveDataFactory.png)

Vous pouvez également déplacer toutes les ressources associées (tels que les alertes associées à la fabrique de données hello), ainsi que de la fabrique de données hello.

![Boîte de dialogue Déplacer des ressources](./media/data-factory-monitor-manage-pipelines/MoveResources.png)
