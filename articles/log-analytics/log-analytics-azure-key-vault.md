---
title: "aaaAzure solution de coffre de clés dans le journal Analytique | Documents Microsoft"
description: "Vous pouvez utiliser la solution de coffre de clés Azure hello dans tooreview Analytique de journal que coffre de clés Azure se connecte."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: jochan
editor: 
ms.assetid: 5e25e6d6-dd20-4528-9820-6e2958a40dae
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: richrund
ms.openlocfilehash: 1c6eae26ded7ad55b0159a3be09cdc9901596298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-analytics-solution-in-log-analytics"></a>Solution Azure Key Vault Analytics dans Log Analytics

![Symbole de Key Vault](./media/log-analytics-azure-keyvault/key-vault-analytics-symbol.png)

Vous pouvez utiliser la solution de coffre de clés Azure hello dans tooreview Analytique de journal Qu'azure Key Vault AuditEvent se connecte.

solution de hello toouse, vous devez tooenable la journalisation des diagnostics d’Azure Key Vault et l’espace de travail Analytique de journal direct hello diagnostics tooa. Il n’est pas le stockage Blob tooAzure toowrite nécessaire hello journaux.

> [!NOTE]
> En janvier 2017, hello pris en charge la façon d’envoi de journaux tooLog de coffre de clés que Analytique modifié. Si la solution de coffre de clés hello que vous utilisez affiche *(déconseillée)* au titre de hello, consultez trop[migration à partir de l’ancienne solution de coffre de clés hello](#migrating-from-the-old-key-vault-solution) pour connaître les étapes, vous devez toofollow.
>
>

## <a name="install-and-configure-hello-solution"></a>Installer et configurer une solution de hello
Utilisez hello suivant les instructions tooinstall et configurer une solution de coffre de clés Azure hello :

1. Activer la solution Azure Key Vault hello [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview) ou à l’aide de hello est décrite dans [solutions Analytique de journal ajouter à partir de la galerie des Solutions de hello](log-analytics-add-solutions.md).
2. Activer les diagnostics de journalisation pour toomonitor de ressources de coffre de clés hello, à l’aide soit hello [portal](#enable-key-vault-diagnostics-in-the-portal) ou [PowerShell](#enable-key-vault-diagnostics-using-powershell)

### <a name="enable-key-vault-diagnostics-in-hello-portal"></a>Activer les diagnostics de coffre de clés dans le portail de hello

1. Bonjour portail Azure, accédez à toomonitor de ressource de coffre de clés toohello
2. Sélectionnez *les journaux de diagnostic* hello tooopen suivant page

   ![Image de la vignette Azure Key Vault](./media/log-analytics-azure-keyvault/log-analytics-keyvault-enable-diagnostics01.png)
3. Cliquez sur *activer les diagnostics* hello tooopen suivant page

   ![Image de la vignette Azure Key Vault](./media/log-analytics-azure-keyvault/log-analytics-keyvault-enable-diagnostics02.png)
4. tooturn des diagnostics, cliquez sur *sur* sous *état*
5. Cliquez sur la case à cocher hello *envoyer tooLog Analytique*
6. Sélectionnez un espace de travail Log Analytics existant ou créez-en un.
7. tooenable *AuditEvent* journaux, cochez hello sous journal
8. Cliquez sur *enregistrer* tooenable la journalisation hello de diagnostics tooLog Analytique

### <a name="enable-key-vault-diagnostics-using-powershell"></a>Activer les diagnostics Key Vault avec PowerShell
Hello PowerShell script suivant fournit un exemple de procédure toouse `Set-AzureRmDiagnosticSetting` tooenable journalisation des diagnostics pour le coffre de clés :
```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'

Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```



## <a name="review-azure-key-vault-data-collection-details"></a>Examiner les détails de la collecte de données par Azure Key Vault
Solution de coffre de clés Azure collecte des journaux de diagnostics directement à partir de hello coffre de clés.
Il n’est pas nécessaire de toowrite hello journaux tooAzure stockage d’objets Blob et aucun agent n’est requise pour la collection de données.

Hello tableau suivant présente les méthodes de collecte de données et d’autres détails sur la façon dont les données sont collectées pour Azure Key Vault.

| Plateforme | Agent direct | Agent Systems Center Operations Manager | Microsoft Azure | Operations Manager requis ? | Données de l’agent Operations Manager envoyées via un groupe d’administration | Fréquence de collecte |
| --- | --- | --- | --- | --- | --- | --- |
| Microsoft Azure |  |  |&#8226; |  |  | à l'arrivée |

## <a name="use-azure-key-vault"></a>Utiliser Azure Key Vault
Après avoir [installer hello solution](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview), afficher des données du coffre de clés hello en cliquant sur hello **Azure Key Vault** vignette à partir de hello **vue d’ensemble** page d’Analytique de journal.

![Image de la vignette Azure Key Vault](./media/log-analytics-azure-keyvault/log-analytics-keyvault-tile.png)

Après avoir cliqué sur hello **vue d’ensemble** vignette, vous pouvez afficher des résumés de vos journaux ensuite dans toodetails pour hello suivant des catégories :

* Volume de toutes les opérations de Key Vault dans le temps
* Volumes des opérations en échec dans le temps
* Latence opérationnelle moyenne par opération
* Qualité de service pour les opérations avec le nombre de hello d’opérations qui prennent plus de 1 000 ms et une liste des opérations qui prennent plus de 1 000 ms

![Image du tableau de bord d’Azure Key Vault](./media/log-analytics-azure-keyvault/log-analytics-keyvault01.png)

![Image du tableau de bord d’Azure Key Vault](./media/log-analytics-azure-keyvault/log-analytics-keyvault02.png)

### <a name="tooview-details-for-any-operation"></a>Détails tooview pour toute opération
1. Sur hello **vue d’ensemble** , cliquez sur hello **Azure Key Vault** vignette.
2. Sur hello **Azure Key Vault** tableau de bord, passez en revue les informations de résumé hello dans un des panneaux de hello, puis cliquez sur une tooview des informations détaillées sur elle dans la page de recherche de journal hello.

    Sur les pages de recherche de journal hello, vous pouvez afficher les résultats par heure, les résultats détaillés et votre historique de recherche de journal. Vous pouvez également filtrer selon les résultats de facettes toonarrow hello.

## <a name="log-analytics-records"></a>Enregistrements Log Analytics
Hello solution d’Azure Key Vault analyse les enregistrements qui ont un type de **KeyVaults** qui sont collectées à partir de [AuditEvent journaux](../key-vault/key-vault-logging.md) dans les Diagnostics Azure.  Propriétés de ces enregistrements sont Bonjour tableau suivant :  

| Propriété | Description |
|:--- |:--- |
| Type |*AzureDiagnostics* |
| SourceSystem |*Microsoft Azure* |
| callerIpAddress |Adresse IP du client hello qui a effectué la demande de hello |
| Catégorie | *AuditEvent* |
| CorrelationId |Un GUID facultatif qui hello client peut passer toocorrelate des côté service (le coffre de clés), les journaux côté client. |
| DurationMs |Durée tooservice demande l’API REST hello, en millisecondes. Cette durée n’inclut pas de latence du réseau, hello décrivant côté client de hello peut correspond pas à ce stade. |
| httpStatusCode_d |Code d’état HTTP retourné par la demande de hello (par exemple, *200*) |
| id_s |ID unique de la demande de hello |
| identity_claim_appid_g | GUID de l’id de l’application hello |
| Nom d'opération |Nom de l’opération de hello, comme décrit dans [journalisation d’Azure Key Vault](../key-vault/key-vault-logging.md) |
| operationVersion |Version de l’API REST demandée par hello client (par exemple *2015-06-01*) |
| requestUri_s |URI de demande de hello |
| Ressource |Nom de coffre de clés hello |
| ResourceGroup |Groupe de ressources de coffre de clés hello |
| ResourceId |ID de ressource Azure Resource Manager Pour les journaux de coffre de clés, il s’agit d’un ID de ressource de coffre de clés hello. |
| ResourceProvider |*MICROSOFT.KEYVAULT* |
| ResourceType | *VAULTS* |
| ResultSignature |État HTTP (par exemple *OK*) |
| ResultType |Résultat de la demande de l’API REST (par exemple, *Réussite*) |
| SubscriptionId |ID d’abonnement hello contenant hello coffre de clés d’abonnement Azure |

## <a name="migrating-from-hello-old-key-vault-solution"></a>Migration à partir de l’ancienne solution de coffre de clés hello
En janvier 2017, hello pris en charge la façon d’envoi de journaux tooLog de coffre de clés que Analytique modifié. Ces modifications permettent de hello suivant avantages :
+ Les journaux sont écrits directement tooLog Analytique sans hello devez toouse un compte de stockage
+ Latence est faible à partir de l’heure hello lorsque les journaux sont générés toothem soient disponibles dans le journal Analytique
+ Le nombre d’étapes de configuration est réduit.
+ Tous les types de diagnostics Azure sont au même format.

solution de mise à jour de hello toouse :

1. [Configurer toobe diagnostics provenant directement tooLog Analytique le coffre de clés](#enable-key-vault-diagnostics-in-the-portal)  
2. Activer la solution de coffre de clés Azure hello à l’aide de hello est décrite dans [solutions Analytique de journal ajouter à partir de la galerie des Solutions de hello](log-analytics-add-solutions.md)
3. Mettre à jour toutes les requêtes enregistrées, les tableaux de bord ou les alertes toouse hello nouveau type de données
  + Le type est déconnecté : KeyVaults tooAzureDiagnostics. Vous pouvez utiliser hello ResourceType toofilter tooKey journaux du coffre.
  - Au lieu de `Type=KeyVaults`, utilisez `Type=AzureDiagnostics ResourceType=VAULTS`.
  + Champs : (les noms de champs respectent la casse)
  - Pour un champ qui comporte un suffixe de \_s, \_d, ou \_g dans nom hello, modification hello premier caractère toolower cas
  - Pour un champ qui comporte un suffixe de \_o dans nom, les données de salutation est divisé en champs individuels en fonction du nom de champ hello imbriqué. Par exemple, hello UPN de l’appelant de hello est stocké dans un champ`identity_claim_http_schemas_xmlsoap_org_ws_2005_05_identity_claims_upn_s`
   - CallerIpAddress champ modifié tooCallerIPAddress
   - Le champ RemoteIPCountry n’est plus présent
4. Supprimer hello *Analytique de coffre de clé (obsolète)* solution. Avec PowerShell, utilisez `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "KeyVault" -Enabled $false`.

Les données collectées avant la modification de hello n’est pas visible dans une nouvelle solution hello. Vous pouvez continuer tooquery pour cette à l’aide de données hello ancien Type et les noms de champs.

## <a name="troubleshooting"></a>Résolution des problèmes
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a>Étapes suivantes
* Utilisez [connecter recherche Analytique de journal](log-analytics-log-searches.md) tooview détaillé les données de coffre de clés Azure.
