---
title: "aaaAzure solution Analytique de mise en réseau dans le journal Analytique | Documents Microsoft"
description: "Vous pouvez utiliser hello solution Analytique de mise en réseau Azure dans les journaux du groupe de sécurité Analytique de journal tooreview réseau Azure et les journaux de la passerelle d’Application Azure."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: ewinner
editor: 
ms.assetid: 66a3b8a1-6c55-4533-9538-cad60c18f28b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: richrund
ms.openlocfilehash: 3674189786bacccc82e6708e78f14c92178e6676
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-networking-monitoring-solutions-in-log-analytics"></a>Solutions d’analyse réseaux Azure dans Log Analytics

Analytique de journal offre hello suivant des solutions pour l’analyse de vos réseaux :
* Analyseur de performances réseau (NPM) pour
 * Surveiller la santé de votre réseau hello
* Azure tooreview analytique de passerelle d’Application
 * Journaux Azure Application Gateway
 * Mesures Azure Application Gateway
* Groupe de sécurité réseau Azure analytique tooreview
 * Journaux Azure Network Security Group

## <a name="network-performance-monitor-npm"></a>Analyseur de performances réseau (NPM)

Hello [analyse des performances réseau](log-analytics-network-performance-monitor.md) solution de gestion est un solution, qui surveille l’intégrité de hello, la disponibilité et l’accessibilité des réseaux d’analyse de réseau.  Il existe une connectivité toomonitor utilisé entre :

* le cloud public et le site local ;
* les centres de données et les emplacements des utilisateurs (filiales) ;
* les sous-réseaux hébergeant différents niveaux d’une application multiniveau.

Pour plus d’informations, consultez l’[Analyseur de performances réseau](log-analytics-network-performance-monitor.md).

## <a name="azure-application-gateway-and-network-security-group-analytics"></a>Azure Application Gateway et Network Security Group Analytics
solutions de hello toouse :
1. Ajouter tooLog de solution de gestion hello Analytique, et
2. Activer les diagnostics toodirect hello diagnostics tooa Analytique de journal espace de travail. Il n’est pas le stockage Blob tooAzure toowrite nécessaire hello journaux.

Vous pouvez activer les diagnostics et les solutions correspondantes hello pour un ou deux de la passerelle d’Application et les groupes de sécurité réseau.

Si vous n’activez pas la journalisation des diagnostics pour un type particulier, mais que vous installez hello solution, panneaux de tableau de bord hello pour cette ressource est vides et affiche un message d’erreur.

> [!NOTE]
> En janvier 2017, hello pris en charge la façon d’envoi de journaux à partir des passerelles d’Application et les groupes de sécurité réseau tooLog que Analytique modifié. Si vous voyez hello **Analytique de mise en réseau Azure (déconseillée)** solution, consultez trop[migration à partir de l’ancienne solution de mise en réseau d’Analytique hello](#migrating-from-the-old-networking-analytics-solution) pour connaître les étapes, vous devez toofollow.
>
>

## <a name="review-azure-networking-data-collection-details"></a>Consulter les détails de la collecte de données réseaux Azure
analytique de passerelle d’Application Azure Hello et solutions de gestion d’analytique de groupe de sécurité réseau hello collecter les journaux de diagnostics directement à partir des passerelles d’Application Azure et les groupes de sécurité réseau. Il n’est pas nécessaire de toowrite hello journaux tooAzure stockage d’objets Blob et aucun agent n’est requise pour la collection de données.

Hello tableau suivant présente les méthodes de collecte de données et d’autres détails sur la façon dont les données sont collectées pour l’analytique de la passerelle d’Application Azure et analytique de groupe de sécurité réseau hello.

| Plateforme | Agent direct | Agent Systems Center Operations Manager | Microsoft Azure | Operations Manager requis ? | Données de l’agent Operations Manager envoyées via un groupe d’administration | Fréquence de collecte |
| --- | --- | --- | --- | --- | --- | --- |
| Microsoft Azure |  |  |&#8226; |  |  |si connecté |


## <a name="azure-application-gateway-analytics-solution-in-log-analytics"></a>Solution d’analytique Azure Application Gateway dans Log Analytics

![Symbole d’Azure Application Gateway Analytics](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

Hello suivant les journaux est pris en charge pour les passerelles d’Application :

* ApplicationGatewayAccessLog
* ApplicationGatewayPerformanceLog
* ApplicationGatewayFirewallLog

Hello suit les mesures est prises en charge pour les passerelles d’Application :

* Débit de 5 minutes

### <a name="install-and-configure-hello-solution"></a>Installer et configurer une solution de hello
Utilisez hello suivant les instructions tooinstall et configurer une solution d’analytique hello passerelle d’Application Azure :

1. Activer la solution d’analytique de passerelle d’Application Azure hello à partir de [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) ou à l’aide de hello est décrite dans [solutions Analytique de journal ajouter à partir de la galerie des Solutions de hello](log-analytics-add-solutions.md).
2. Activer la journalisation des diagnostics pour hello [passerelles d’Application](../application-gateway/application-gateway-diagnostics.md) vous souhaitez toomonitor.

#### <a name="enable-azure-application-gateway-diagnostics-in-hello-portal"></a>Activer les diagnostics de passerelle d’Application Azure dans le portail de hello

1. Bonjour portail Azure, accédez à toomonitor de ressources toohello Application Gateway
2. Sélectionnez *les journaux de diagnostic* hello tooopen suivant page

   ![Image de la ressource Azure Application Gateway](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics01.png)
3. Cliquez sur *activer les diagnostics* hello tooopen suivant page

   ![Image de la ressource Azure Application Gateway](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics02.png)
4. tooturn des diagnostics, cliquez sur *sur* sous *état*
5. Cliquez sur la case à cocher hello *envoyer tooLog Analytique*
6. Sélectionnez un espace de travail Log Analytics existant ou créez-en un.
7. Cliquez sur la case à cocher hello sous **journal** pour chacun des toocollect de types hello journal
8. Cliquez sur *enregistrer* tooenable la journalisation hello de diagnostics tooLog Analytique

#### <a name="enable-azure-network-diagnostics-using-powershell"></a>Activez les diagnostics de réseau Azure avec PowerShell

Hello PowerShell script suivant fournit un exemple de procédure tooenable journalisation des diagnostics pour les passerelles d’application.

```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$gateway = Get-AzureRmApplicationGateway -Name 'ContosoGateway'

Set-AzureRmDiagnosticSetting -ResourceId $gateway.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-application-gateway-analytics"></a>Utiliser l’analytique Azure Application Gateway
![Image de la mosaïque d’analytique Azure Application Gateway](./media/log-analytics-azure-networking/log-analytics-appgateway-tile.png)

Après avoir cliqué sur hello **analytique de la passerelle d’Application Azure** vignette sur hello vue d’ensemble, vous pouvez afficher des synthèses de vos journaux et procéder dans toodetails pour hello suivant des catégories :

* Journaux d’accès à la passerelle d’application
  * Erreurs client et serveur pour les journaux d’accès à la passerelle d’application
  * Nombre de demandes par heure pour chaque passerelle d’application
  * Nombre d’échecs de demande par heure pour chaque passerelle d’application
  * Erreurs de l’agent utilisateur pour les passerelles d’application
* Performances de la passerelle d’application
  * Intégrité de l’hôte pour la passerelle d’application
  * Nombre maximal et 95e centile pour les échecs de demande de passerelle d’application

![Image du tableau de bord d’analytique Azure Application Gateway](./media/log-analytics-azure-networking/log-analytics-appgateway01.png)

![Image du tableau de bord d’analytique Azure Application Gateway](./media/log-analytics-azure-networking/log-analytics-appgateway02.png)

Sur hello **analytique de la passerelle d’Application Azure** tableau de bord, passez en revue les informations de résumé hello dans un des panneaux de hello, puis cliquez sur une tooview des informations détaillées sur page de recherche de journal hello.

Sur les pages de recherche de journal hello, vous pouvez afficher les résultats par heure, les résultats détaillés et votre historique de recherche de journal. Vous pouvez également filtrer selon les résultats de facettes toonarrow hello.


## <a name="azure-network-security-group-analytics-solution-in-log-analytics"></a>Solution d’analytique Azure Network Security Group dans Log Analytics

![Symbole d’Azure Network Security Group Analytics](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

Hello suivant des journaux est pris en charge pour les groupes de sécurité réseau :

* NetworkSecurityGroupEvent
* NetworkSecurityGroupRuleCounter

### <a name="install-and-configure-hello-solution"></a>Installer et configurer une solution de hello
Utilisez hello suivant les instructions tooinstall et configurer une solution d’Analytique de mise en réseau Azure hello :

1. Activer la solution d’analytique de groupe de sécurité réseau Azure hello à partir de [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) ou à l’aide de hello est décrite dans [solutions Analytique de journal ajouter à partir de la galerie des Solutions de hello](log-analytics-add-solutions.md).
2. Activer la journalisation des diagnostics pour hello [groupe de sécurité réseau](../virtual-network/virtual-network-nsg-manage-log.md) ressources toomonitor.

### <a name="enable-azure-network-security-group-diagnostics-in-hello-portal"></a>Activer les diagnostics de groupe de sécurité réseau Azure dans le portail de hello

1. Bonjour portail Azure, accédez à toomonitor de ressource de groupe de sécurité réseau toohello
2. Sélectionnez *les journaux de diagnostic* hello tooopen suivant page

   ![Image de la ressource Azure Network Security Group](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics01.png)
3. Cliquez sur *activer les diagnostics* hello tooopen suivant page

   ![Image de la ressource Azure Network Security Group](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics02.png)
4. tooturn des diagnostics, cliquez sur *sur* sous *état*
5. Cliquez sur la case à cocher hello *envoyer tooLog Analytique*
6. Sélectionnez un espace de travail Log Analytics existant ou créez-en un.
7. Cliquez sur la case à cocher hello sous **journal** pour chacun des toocollect de types hello journal
8. Cliquez sur *enregistrer* tooenable la journalisation hello de diagnostics tooLog Analytique

### <a name="enable-azure-network-diagnostics-using-powershell"></a>Activez les diagnostics de réseau Azure avec PowerShell

Hello PowerShell script suivant fournit un exemple de procédure tooenable journalisation des diagnostics pour les groupes de sécurité réseau
```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$nsg = Get-AzureRmNetworkSecurityGroup -Name 'ContosoNSG'

Set-AzureRmDiagnosticSetting -ResourceId $nsg.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-network-security-group-analytics"></a>Utiliser l’analytique Azure Network Security Group
Après avoir cliqué sur hello **analytique de groupe de sécurité réseau Azure** vignette sur hello vue d’ensemble, vous pouvez afficher des synthèses de vos journaux et procéder dans toodetails pour hello suivant des catégories :

* Flux bloqués de groupe de sécurité réseau
  * Règles de groupe de sécurité réseau avec flux bloqués
  * Adresses MAC avec flux bloqués
* Flux autorisés de groupe de sécurité réseau
  * Règles de groupe de sécurité réseau avec flux autorisés
  * Adresses MAC avec flux autorisés

![Image du tableau de bord d’analytique Azure Network Security Group](./media/log-analytics-azure-networking/log-analytics-nsg01.png)

![Image du tableau de bord d’analytique Azure Network Security Group](./media/log-analytics-azure-networking/log-analytics-nsg02.png)

Sur hello **analytique de groupe de sécurité réseau Azure** tableau de bord, passez en revue les informations de résumé hello dans un des panneaux de hello, puis cliquez sur une tooview des informations détaillées sur page de recherche de journal hello.

Sur les pages de recherche de journal hello, vous pouvez afficher les résultats par heure, les résultats détaillés et votre historique de recherche de journal. Vous pouvez également filtrer selon les résultats de facettes toonarrow hello.

## <a name="migrating-from-hello-old-networking-analytics-solution"></a>Migration à partir de l’ancienne solution de mise en réseau d’Analytique hello
En janvier 2017, hello pris en charge la façon d’envoi de journaux à partir des passerelles d’Application Azure et les groupes de sécurité de réseau Azure tooLog que Analytique modifié. Ces modifications permettent de hello suivant avantages :
+ Les journaux sont écrits directement tooLog Analytique sans hello devez toouse un compte de stockage
+ Latence est faible à partir de l’heure hello lorsque les journaux sont générés toothem soient disponibles dans le journal Analytique
+ Le nombre d’étapes de configuration est réduit.
+ Tous les types de diagnostics Azure sont au même format.

solutions toouse hello mis à jour :

1. [Configurer toobe diagnostics provenant directement tooLog Analytique passerelles d’Application Azure](#enable-azure-application-gateway-diagnostics-in-the-portal)
2. [Configurer toobe diagnostics envoyé des tooLog Analytique directement à partir de groupes de sécurité réseau Azure](#enable-azure-network-security-group-diagnostics-in-the-portal)
2. Activer hello *Analytique de passerelle d’Application Azure* et hello *Analytique de groupe de sécurité de réseau Azure* solution à l’aide du processus de hello décrit dans [solutions Analytique de journal ajouter à partir de Hello galerie de Solutions](log-analytics-add-solutions.md)
3. Mettre à jour toutes les requêtes enregistrées, les tableaux de bord ou les alertes toouse hello nouveau type de données
  + Le type est tooAzureDiagnostics. Vous pouvez utiliser hello ResourceType toofilter tooAzure mise en réseau des journaux.

    | Au lieu du paramètre... | Utilisez : |
    | --- | --- |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayAccess`| `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayAccess` |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayPerformance` | `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayPerformance` |
    | `Type=NetworkSecuritygroups` | `Type=AzureDiagnostics ResourceType=NETWORKSECURITYGROUPS` |

   + Pour un champ qui comporte un suffixe de \_s, \_d, ou \_g dans nom hello, modification hello premier caractère toolower cas
   + Pour un champ qui comporte un suffixe de \_o dans nom, les données de salutation est divisé en champs individuels en fonction du nom de champ hello imbriqué.
4. Supprimer hello *Analytique de mise en réseau Azure (obsolète)* solution.
  + Avec PowerShell, utilisez `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`.

Les données collectées avant la modification de hello n’est pas visible dans une nouvelle solution hello. Vous pouvez continuer tooquery pour cette à l’aide de données hello ancien Type et les noms de champs.

## <a name="troubleshooting"></a>Résolution des problèmes
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a>Étapes suivantes
* Utilisez [connecter recherche Analytique de journal](log-analytics-log-searches.md) tooview détaillées des données de diagnostic Azure.
