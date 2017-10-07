---
title: "aaaCollect Azure du service Journaux et des mesures pour l’Analytique de journal | Documents Microsoft"
description: "Configurer les diagnostics sur les ressources Azure toowrite métriques et journaux tooLog Analytique."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 84105740-3697-4109-bc59-2452c1131bfe
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1cede9a94ec83c4e3a95853dc2ec355d8df06d6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-azure-service-logs-and-metrics-for-use-in-log-analytics"></a>Collecte des journaux et des métriques des services Azure à utiliser dans Log Analytics

Il existe quatre façons différentes de collecter des journaux et des métriques pour les services Azure :

1. Diagnostics Azure directe tooLog Analytique (*Diagnostics* Bonjour tableau suivant)
2. Diagnostics Azure tooAzure stockage tooLog Analytique (*stockage* Bonjour tableau suivant)
3. Connecteurs pour les services Azure (*connecteurs* Bonjour tableau suivant)
4. Scripts toocollect, puis les données de publication dans le journal Analytique (vides Bonjour tableau suivant et pour les services qui ne sont pas répertoriées)


| Service                 | Type de ressource                           | Journaux        | Mesures     | Solution |
| --- | --- | --- | --- | --- |
| Passerelles d’application    | Microsoft.Network/applicationGateways   | Diagnostics | Diagnostics | [Azure Application Gateway Analytics](log-analytics-azure-networking-analytics.md#azure-application-gateway-analytics-solution-in-log-analytics) |
| Application Insights    |                                         | Connecteur   | Connecteur   | [Connecteur Application Insights](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/) (version préliminaire) |
| Comptes Automation     | Microsoft.Automation/AutomationAccounts | Diagnostics |             | [Plus d’informations](../automation/automation-manage-send-joblogs-log-analytics.md)|
| Comptes Batch          | Microsoft.Batch/batchAccounts           | Diagnostics | Diagnostics | |
| Services cloud classiques  |                                         | Storage     |             | [Plus d’informations](log-analytics-azure-storage-iis-table.md) |
| Cognitive services      | Microsoft.CognitiveServices/accounts    |             | Diagnostics | |
| Data Lake analytics     | Microsoft.DataLakeAnalytics/accounts    | Diagnostics |             | |
| Data Lake Store         | Microsoft.DataLakeStore/accounts        | Diagnostics |             | |
| Espace de noms Event Hub     | Microsoft.EventHub/namespaces           | Diagnostics | Diagnostics | |
| IoT Hubs                | Microsoft.Devices/IotHubs               |             | Diagnostics | |
| Key Vault               | Microsoft.KeyVault/vaults               | Diagnostics |             | [KeyVault Analytics](log-analytics-azure-key-vault.md) |
| Équilibreurs de charge          | Microsoft.Network/loadBalancers         | Diagnostics |             |  |
| Logic Apps              | Microsoft.Logic/workflows <br> Microsoft.Logic/integrationAccounts | Diagnostics | Diagnostics | |
| Groupes de sécurité réseau | Microsoft.Network/networksecuritygroups | Diagnostics |             | [Azure Network Security Group Analytics](log-analytics-azure-networking-analytics.md#azure-network-security-group-analytics-solution-in-log-analytics) |
| Coffres de récupération         | Microsoft.RecoveryServices/vaults       |             |             | [Azure Recovery Services Analytics (version préliminaire)](https://github.com/krnese/AzureDeploy/blob/master/OMS/MSOMS/Solutions/recoveryservices/)|
| Services de recherche         | Microsoft.Search/searchServices         | Diagnostics | Diagnostics | |
| Espace de noms Service Bus   | Microsoft.ServiceBus/namespaces         | Diagnostics | Diagnostics | [Service Bus Analytics (version préliminaire)](https://github.com/Azure/azure-quickstart-templates/tree/master/oms-servicebus-solution)|
| Service Fabric          |                                         | Storage     |             | [Service Fabric Analytics (version préliminaire)](log-analytics-service-fabric.md) |
| SQL (v12)               | Microsoft.Sql/servers/databases <br> Microsoft.Sql/servers/elasticPools |             | Diagnostics | [Azure SQL Analytics (version préliminaire)](log-analytics-azure-sql.md) |
| Storage                 |                                         |             | Script      | [Azure Storage Analytics (version préliminaire)](https://github.com/Azure/azure-quickstart-templates/tree/master/oms-azure-storage-analytics-solution) |
| Machines virtuelles        | Microsoft.Compute/virtualMachines       | Extension   | Extension <br> Diagnostics  | |
| Groupes de machines virtuelles identiques | Microsoft.Compute/virtualMachines <br> Microsoft.Compute/virtualMachineScaleSets/virtualMachines |             | Diagnostics | |
| Batteries de serveurs web        | Microsoft.Web/serverfarms               |             | Diagnostics | |
| Sites web               | Microsoft.Web/sites <br> Microsoft.Web/sites/slots |             | Diagnostics | [Azure Web Apps Analytics (version préliminaire)](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureWebAppsAnalyticsOMS?tab=Overview) |


> [!NOTE]
> Pour la surveillance des machines virtuelles Azure (Linux et Windows), nous vous recommandons d’installer hello [extension de machine virtuelle Analytique de journal](log-analytics-azure-vm-extension.md). l’agent de Hello vous fournit les informations collectées à partir de vos machines virtuelles. Vous pouvez également utiliser l’extension de hello pour les machines virtuelles identiques.
>
>

## <a name="azure-diagnostics-direct-toolog-analytics"></a>Diagnostics Azure directe tooLog Analytique
Beaucoup de ressources Azure est des mesures et des journaux de diagnostic toowrite en mesure de directement tooLog Analytique, ce qui est moyen hello préféré de la collecte de données hello pour l’analyse. Lors de l’utilisation des diagnostics Azure, données sont immédiatement écrit tooLog Analytique et il n’existe aucun toostorage de données nécessaire toofirst écriture hello.

Les ressources Azure qui prennent en charge [moniteur Azure](../monitoring-and-diagnostics/monitoring-overview.md) peut envoyer les journaux et les métriques directement tooLog Analytique.

* Pour plus d’informations hello de métriques disponibles de hello, consultez trop[prise en charge des métriques avec Azure analyse](../monitoring-and-diagnostics/monitoring-supported-metrics.md).
* Pour plus d’informations hello de journaux disponibles de hello, consultez trop[prise en charge des services et schéma pour les journaux de diagnostic](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).

### <a name="enable-diagnostics-with-powershell"></a>Activer les diagnostics avec PowerShell
Vous avez besoin hello novembre 2016 (v2.3.0) ou une version plus récente de [Azure PowerShell](/powershell/azure/overview).

Hello suivant montre l’exemple PowerShell comment toouse [Set-AzureRmDiagnosticSetting](/powershell/module/azurerm.insights/set-azurermdiagnosticsetting) tooenable des diagnostics sur un groupe de sécurité réseau. Hello même approche fonctionne pour toutes les ressources prises en charge - définir `$resourceId` toohello id de ressource de ressource hello diagnostics tooenable pour.

```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$resourceId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/DEMO"

Set-AzureRmDiagnosticSetting -ResourceId $ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="enable-diagnostics-with-resource-manager-templates"></a>Activer les diagnostics avec des modèles Resource Manager

tooenable des diagnostics sur une ressource lorsqu’il est créé, et ont les diagnostics hello envoyés espace de travail Analytique de journal tooyour que vous pouvez utiliser un modèle toohello similaire un ci-dessous. Cet exemple est destiné à un compte Automation, mais fonctionne pour tous les types de ressources pris en charge.

```json
        {
            "type": "Microsoft.Automation/automationAccounts/providers/diagnosticSettings",
            "name": "[concat(parameters('omsAutomationAccountName'), '/', 'Microsoft.Insights/service')]",
            "apiVersion": "2015-07-01",
            "dependsOn": [
                "[concat('Microsoft.Automation/automationAccounts/', parameters('omsAutomationAccountName'))]",
                "[concat('Microsoft.OperationalInsights/workspaces/', parameters('omsWorkspaceName'))]"
            ],
            "properties": {
                "workspaceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('omsWorkspaceName'))]",
                "logs": [
                    {
                        "category": "JobLogs",
                        "enabled": true
                    },
                    {
                        "category": "JobStreams",
                        "enabled": true
                    }
                ]
            }
        }
```

[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="azure-diagnostics-toostorage-then-toolog-analytics"></a>Diagnostics Azure toostorage puis tooLog Analytique

Pour collecter les journaux à partir de certaines ressources, il est possible toosend hello journaux tooAzure stockage et puis configurer les journaux de hello tooread Analytique de journal à partir du stockage.

Analytique de journal permet de ce test de diagnostic toocollect approche du stockage Azure hello suivant des ressources et les journaux :

| Ressource | Journaux |
| --- | --- |
| Service Fabric |ETWEvent <br> Événement opérationnel <br> Événement Reliable Actor <br> Événement de service fiable |
| Machines virtuelles |Syslog Linux <br> Événement Windows <br> Journal IIS <br> ETWEvent Windows |
| Rôles web <br> Rôles de travail |Syslog Linux <br> Événement Windows <br> Journal IIS <br> ETWEvent Windows |

> [!NOTE]
> Vous payez un taux de données Azure normal pour le stockage et les transactions lorsque vous envoyez des diagnostics compte de stockage tooa et quand Analytique de journal lit les données de hello à partir de votre compte de stockage.
>
>

Consultez [stockage d’objets blob utilisé pour le stockage IIS et de table pour les événements](log-analytics-azure-storage-iis-table.md) toolearn plus en détail comment Analytique de journal peuvent collecter ces journaux.

## <a name="connectors-for-azure-services"></a>Connecteurs pour les services Azure

Il existe un connecteur pour Application Insights, qui permet aux données collectées par toobe Application Insights envoyé tooLog Analytique.

En savoir plus sur hello [connecteur Application Insights](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/).

## <a name="scripts-toocollect-and-post-data-toolog-analytics"></a>Scripts toocollect et post tooLog données Analytique

Pour les services Azure qui ne fournissent pas un moyen direct toosend les tooLog journaux et des métriques Analytique, vous pouvez utiliser un toocollect de script Azure Automation hello journal et des mesures. Hello script peut alors envoyer hello données tooLog Analytique à l’aide de hello [API du collecteur de données](log-analytics-data-collector-api.md)

la galerie de modèle Azure Hello a [exemples d’utilisation d’Azure Automation](https://azure.microsoft.com/en-us/resources/templates/?term=OMS) toocollect des données à partir des services et en l’envoyant tooLog Analytique.

## <a name="next-steps"></a>Étapes suivantes

* [Utiliser le stockage d’objets blob pour le stockage IIS et de table pour les événements](log-analytics-azure-storage-iis-table.md) tooread les journaux hello pour les services Azure qui écrivent des diagnostics tootable stockage ou IIS consigne écrite tooblob stockage.
* [Activer des Solutions](log-analytics-add-solutions.md) tooprovide comprendre les données de hello.
* [Utiliser des requêtes de recherche](log-analytics-log-searches.md) tooanalyze les données de salutation.
