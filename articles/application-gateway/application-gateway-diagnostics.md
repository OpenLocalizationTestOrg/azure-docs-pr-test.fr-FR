---
title: "aaaMonitor accéder aux journaux, des journaux de performances, d’intégrité du serveur principal et de mesures pour la passerelle d’Application | Documents Microsoft"
description: "Découvrez comment tooenable et gérer les journaux d’accès et des journaux de performances pour la passerelle d’Application"
services: application-gateway
documentationcenter: na
author: amitsriva
manager: rossort
editor: tysonn
tags: azure-resource-manager
ms.assetid: 300628b8-8e3d-40ab-b294-3ecc5e48ef98
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/17/2017
ms.author: amitsriva
ms.openlocfilehash: 36ebf15c28f776158350ef8e73d617ef68e09266
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="back-end-health-diagnostic-logs-and-metrics-for-application-gateway"></a>Intégrité du serveur principal, journaux de diagnostic et métriques pour la passerelle Application Gateway

À l’aide de passerelle d’Application Azure, vous pouvez surveiller les ressources Bonjour suivant des façons :

* [Contrôle d’intégrité du serveur principal](#back-end-health): passerelle d’Application fournit hello capacité toomonitor hello la santé des serveurs hello Bonjour pools principaux via le portail Azure de hello et PowerShell. Vous trouverez également la santé des pools de back-end hello via les journaux de diagnostic de performances hello hello.

* [Journaux](#diagnostic-logs): autoriser les journaux pour les performances, l’accès, et autres toobe données enregistré ou consommés à partir d’une ressource pour la surveillance.

* [Mesures](#metrics) : la passerelle Application Gateway possède actuellement une métrique. Cette mesure mesure débit hello de passerelle d’application hello en octets par seconde.

## <a name="back-end-health"></a>Intégrité du serveur principal

Passerelle d’application fournit l’intégrité hello capacité toomonitor hello des membres individuels des pools de back-end hello via le portail de hello, PowerShell et hello interface de ligne de commande (CLI). Vous pouvez également trouver l’état d’intégrité agrégé résumé des pools principaux via les journaux de diagnostic de performances hello. 

rapport de contrôle d’intégrité du serveur principal Hello reflète la sortie hello d’instances de hello Application Gateway intégrité sonde toohello principal. Lors de la détection a réussi et hello précédent fin peut recevoir du trafic, il est considéré comme sain. Sinon, il est considéré comme défaillant.

> [!IMPORTANT]
> S’il existe un groupe de sécurité réseau (NSG) sur un sous-réseau de passerelle d’Application, ouvrez les plages de ports 65503-65 534 sur le sous-réseau de passerelle d’Application hello pour le trafic entrant. Ces ports sont requis pour toowork d’API hello d’intégrité du serveur principal.


### <a name="view-back-end-health-through-hello-portal"></a>Afficher l’intégrité du serveur principal via le portail de hello

Dans le portail hello, contrôle d’intégrité du serveur principal est fourni automatiquement. Dans une passerelle Application Gateway existante, sélectionnez **Analyse** > **Intégrité du serveur principal**. 

Chaque membre dans le pool principal d’hello est répertorié dans cette page (si elle est une carte réseau, IP ou nom de domaine complet). Le nom du pool principal, le port, le nom et l’état d’intégrité des paramètres HTTP principaux sont affichés. Les valeurs valides de l’état d’intégrité sont **Healthy** (Intègre), **Unhealthy** (Défaillant) et **Unknown** (Inconnu).

> [!NOTE]
> Si vous voyez l’état d’intégrité du serveur principal **inconnu**, assurez-vous que principale toohello d’accès n’est pas bloqué par une règle de groupe de sécurité réseau, un itinéraire défini par l’utilisateur (UDR) ou un DNS personnalisé hello du réseau virtuel.

![Intégrité du serveur principal][10]

### <a name="view-back-end-health-through-powershell"></a>Affichage de l’intégrité du serveur principal via PowerShell

Hello suivant code PowerShell montre comment le contrôle d’intégrité du serveur principal tooview à l’aide de hello `Get-AzureRmApplicationGatewayBackendHealth` applet de commande :

```powershell
Get-AzureRmApplicationGatewayBackendHealth -Name ApplicationGateway1 -ResourceGroupName Contoso
```

### <a name="view-back-end-health-through-azure-cli-20"></a>Affichage de l’intégrité du serveur principal via Azure CLI 2.0

```azurecli
az network application-gateway show-backend-health --resource-group AdatumAppGatewayRG --name AdatumAppGateway
```

### <a name="results"></a>Résultats

Hello suivant extrait de code illustre un exemple de réponse de hello :

```json
{
"BackendAddressPool": {
    "Id": "/subscriptions/00000000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/appGatewayBackendPool"
},
"BackendHttpSettingsCollection": [
    {
    "BackendHttpSettings": {
        "Id": "/00000000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings"
    },
    "Servers": [
        {
        "Address": "hostname.westus.cloudapp.azure.com",
        "Health": "Healthy"
        },
        {
        "Address": "hostname.westus.cloudapp.azure.com",
        "Health": "Healthy"
        }
    ]
    }
]
}
```

## <a name="diagnostic-logging"></a>Journaux de diagnostic

Vous pouvez utiliser différents types de journaux dans Azure toomanage et résoudre les problèmes de passerelles d’application. Vous pouvez accéder à certaines de ces journaux via le portail de hello. Tous les journaux peuvent être extraits à partir d’un stockage Blob Azure et affichés dans différents outils, comme [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md), Excel et PowerBI. Pour plus d’informations sur hello différents types de journaux de hello suivant liste :

* **Journal d’activité**: vous pouvez utiliser [journaux d’activité Azure](../monitoring-and-diagnostics/insights-debugging-with-events.md) (précédemment appelés journaux des opérations et les journaux d’audit) tooview toutes les opérations qui sont soumis tooyour abonnement Azure, ainsi que leur état. Entrées de journal d’activité sont collectées par défaut, et vous pouvez les visualiser dans hello portail Azure.
* **Journal d’accès**: vous pouvez utiliser cette modèles d’accès journal tooview passerelle d’Application et analyser des informations importantes, l’appelant, y compris hello IP, URL demandée, latence de la réponse, code de retour et d’octets et l’extraction. Un journal d’accès est collecté toutes les 300 secondes. Ce journal contient un enregistrement par instance Application Gateway. instance de la passerelle d’Application Hello peut être identifiée par la propriété instanceId de hello.
* **Journal de performances**: vous pouvez utiliser cette tooview du journal des performances des instances de la passerelle d’Application. Ce journal capture des informations sur les performances de chaque instance, notamment le nombre total de requêtes traitées, le débit en octets, le nombre total de requêtes présentées, le nombre de requêtes ayant échoué, le nombre d’instances du serveur principal intègres et défectueuses. Le journal des performances est collecté toutes les 60 secondes.
* **Journal du pare-feu**: vous pouvez utiliser ce journal tooview hello les demandes qui sont enregistrés via le mode de détection ou de prévention d’une passerelle d’application qui est configuré avec un pare-feu d’applications web hello.

> [!NOTE]
> Les journaux sont disponibles uniquement pour les ressources déployées dans le modèle de déploiement du Gestionnaire de ressources Azure hello. Vous ne pouvez pas utiliser les journaux pour les ressources dans le modèle de déploiement classique hello. Pour mieux comprendre les modèles hello deux, consultez hello [déploiement du Gestionnaire de ressources de présentation et déploiement classique](../azure-resource-manager/resource-manager-deployment-model.md) l’article.

Pour stocker vos journaux, vous disposez de trois options :

* **Compte de stockage** : les comptes de stockage conviennent parfaitement aux journaux lorsqu’ils sont stockés pour une durée plus longue et consultés lorsque nécessaire.
* **Concentrateurs d’événements**: concentrateurs d’événements sont une option intéressante pour l’intégration avec d’autres informations de sécurité et des outils de gestion des événements (SEIM) tooget des alertes sur vos ressources.
* **Log Analytics** : Log Analytics convient parfaitement pour la surveillance en temps réel générale de votre application ou la recherche de tendances.

### <a name="enable-logging-through-powershell"></a>Activation de la journalisation avec PowerShell

La journalisation d’activité est automatiquement activée pour chaque ressource Resource Manager. Vous devez activer l’accès et toostart de journalisation de performances collecte des données hello ces journaux. tooenable journalisation, hello utilisation comme suit :

1. Notez l’ID de ressource de votre compte de stockage, où sont stockées les données de journal hello. Cette valeur se présente sous forme de hello : /subscriptions/\<subscriptionId\>/resourceGroups/\<nom de groupe de ressources\>/providers/Microsoft.Storage/storageAccounts/\<le nom de compte de stockage\>. Vous pouvez utiliser n’importe quel compte de stockage dans votre abonnement. Ces informations, vous pouvez utiliser hello toofind portail Azure.

    ![Portail : ID de ressource du compte de stockage](./media/application-gateway-diagnostics/diagnostics1.png)

2. Notez l’ID de ressource de votre passerelle Application Gateway pour laquelle la journalisation est activée. Cette valeur se présente sous forme de hello : /subscriptions/\<subscriptionId\>/resourceGroups/\<nom de groupe de ressources\>/providers/Microsoft.Network/applicationGateways/\<passerelle d’application nom\>. Vous pouvez utiliser les toofind portail hello ces informations.

    ![Portail : ID de ressource de la passerelle Application Gateway](./media/application-gateway-diagnostics/diagnostics2.png)

3. Activer la journalisation de diagnostic à l’aide de hello suivant l’applet de commande PowerShell :

    ```powershell
    Set-AzureRmDiagnosticSetting  -ResourceId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name> -StorageAccountId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Storage/storageAccounts/<storage account name> -Enabled $true     
    ```
    
> [!TIP] 
>Les journaux d’activité ne nécessitent pas de compte de stockage distinct. utilisation de Hello du stockage pour l’accès et l’enregistrement des performances entraîne des frais de service.

### <a name="enable-logging-through-hello-azure-portal"></a>Activer la journalisation via hello portail Azure

1. Hello portail Azure, votre ressource et cliquez sur **journaux de Diagnostic**.

   Pour Application Gateway, trois journaux d’audit sont disponibles :

   * Journal d’accès
   * Journal des performances
   * Journal du pare-feu

2. toostart la collecte de données, cliquez sur **activer les diagnostics**.

   ![Activation des diagnostics][1]

3. Hello **paramètres de diagnostic** panneau fournit les paramètres hello hello des journaux de diagnostic. Dans cet exemple, Analytique de journal stocke les journaux de hello. Cliquez sur **configurer** sous **Analytique de journal** tooconfigure votre espace de travail. Vous pouvez également utiliser des hubs d’événements et un stockage compte toosave hello diagnostic se connecte.

   ![Démarrage du processus de configuration hello][2]

4. Sélectionnez ou créez un espace de travail OMS (Operations Management Suite) existant. Cet exemple utilise un espace de travail existant.

   ![Options des espaces de travail OMS][3]

5. Confirmez les paramètres hello et cliquez sur **enregistrer**.

   ![Panneau des paramètres de diagnostic avec des sélections][4]

### <a name="activity-log"></a>Journal d’activité

Azure génère un journal d’activité hello par défaut. dans le magasin de journaux des événements Azure hello, Hello journaux sont conservées pendant 90 jours. En savoir plus sur ces journaux en lisant hello [afficher les événements et le journal d’activité](../monitoring-and-diagnostics/insights-debugging-with-events.md) l’article.

### <a name="access-log"></a>Journal d’accès

journal d’accès Hello est généré uniquement si vous l’avez activé sur chaque instance de la passerelle d’Application, comme expliqué dans les étapes précédentes de hello. les données de Hello sont stockées dans le compte de stockage hello que vous avez spécifié lorsque vous avez activé la journalisation hello. Chaque accès de la passerelle d’Application est enregistré au format JSON, comme indiqué dans hello l’exemple suivant :


|Valeur  |Description  |
|---------|---------|
|instanceId     | Cette demande hello servi d’instance de passerelle d’application.        |
|clientIP     | Adresse IP d’origine pour la demande de hello.        |
|clientPort     | Port de demande de hello d’origine.       |
|httpMethod     | Méthode HTTP utilisée par la demande de hello.       |
|requestUri     | URI de hello a reçu une demande.        |
|RequestQuery     | **Server avait acheminé**: instance de pool principal qui a été envoyé à la demande de hello. </br> **X-AzureApplicationGateway-journal-ID**: ID de corrélation utilisé pour la demande de hello. Il peut être utilisé tootroubleshoot les problèmes de trafic sur les serveurs principaux hello. </br>**ÉTAT du serveur**: code de réponse HTTP passerelle d’Application a reçu back-end hello.       |
|UserAgent     | Agent utilisateur à partir de l’en-tête de demande HTTP de hello.        |
|httpStatus     | Code d’état HTTP retourné toohello client à partir de la passerelle d’Application.       |
|httpVersion     | Version HTTP de la demande de hello.        |
|receivedBytes     | Taille du paquet reçu, en octets.        |
|sentBytes| Taille du paquet envoyé, en octets.|
|timeTaken| Durée (en millisecondes) nécessaire pour une toobe demande traités et son toobe de réponse envoyé. Elle est calculée comme intervalle hello de temps hello lorsque la passerelle d’Application reçoit hello premier octet d’une durée de toohello de demande HTTP lorsque la réponse de hello envoyez fin de l’opération. Il est important de toonote qui hello Time-Taken le champ généralement inclut le temps hello hello demande et réponse les paquets réseau hello. |
|sslEnabled| Indique si les pools de communication toohello principal utilisé SSL. Les valeurs valides sont On (Activé) et Off (Désactivé).|
```json
{
    "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/PEERINGTEST/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
    "operationName": "ApplicationGatewayAccess",
    "time": "2017-04-26T19:27:38Z",
    "category": "ApplicationGatewayAccessLog",
    "properties": {
        "instanceId": "ApplicationGatewayRole_IN_0",
        "clientIP": "191.96.249.97",
        "clientPort": 46886,
        "httpMethod": "GET",
        "requestUri": "/phpmyadmin/scripts/setup.php",
        "requestQuery": "X-AzureApplicationGateway-CACHE-HIT=0&SERVER-ROUTED=10.4.0.4&X-AzureApplicationGateway-LOG-ID=874f1f0f-6807-41c9-b7bc-f3cfa74aa0b1&SERVER-STATUS=404",
        "userAgent": "-",
        "httpStatus": 404,
        "httpVersion": "HTTP/1.0",
        "receivedBytes": 65,
        "sentBytes": 553,
        "timeTaken": 205,
        "sslEnabled": "off"
    }
}
```

### <a name="performance-log"></a>Journal des performances

journal de performances Hello est généré uniquement si vous l’avez activé sur chaque instance de la passerelle d’Application, comme expliqué dans les étapes précédentes de hello. les données de Hello sont stockées dans le compte de stockage hello que vous avez spécifié lorsque vous avez activé la journalisation hello. données de journal de performances Hello sont générées par intervalles de 1 minute. Hello données suivantes est journalisé :


|Valeur  |Description  |
|---------|---------|
|instanceId     |  Instance Application Gateway pour laquelle les données des performances sont générées. Pour une passerelle Application Gateway à plusieurs instances, il y a une ligne par instance.        |
|healthyHostCount     | Nombre d’hôtes intègres dans le pool principal d’hello.        |
|unHealthyHostCount     | Nombre d’hôtes défectueux dans le pool principal d’hello.        |
|requestCount     | Nombre de requêtes traitées.        |
|latency | Latence (en millisecondes) des demandes de hello instance toohello back-end qui sert les demandes hello. |
|failedRequestCount| Nombre d’échecs de requêtes.|
|throughput| Débit moyen depuis le dernier journal hello, mesurée en octets par seconde.|

```json
{
    "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
    "operationName": "ApplicationGatewayPerformance",
    "time": "2016-04-09T00:00:00Z",
    "category": "ApplicationGatewayPerformanceLog",
    "properties":
    {
        "instanceId":"ApplicationGatewayRole_IN_1",
        "healthyHostCount":"4",
        "unHealthyHostCount":"0",
        "requestCount":"185",
        "latency":"0",
        "failedRequestCount":"0",
        "throughput":"119427"
    }
}
```

> [!NOTE]
> La latence est calculée à partir de l’heure hello lorsque hello du premier octet de demande de hello HTTP est reçu toohello pendant laquelle hello dernier octet de réponse HTTP de hello est envoyée. Son hello somme de hello passerelle d’Application le temps de traitement plus hello toohello du coût du réseau précédent se terminer, plus le temps hello hello back-end prend tooprocess hello demande.

### <a name="firewall-log"></a>Journal du pare-feu

journal du pare-feu Hello est généré uniquement si vous l’avez activé pour chaque application gateway, comme expliqué dans les étapes précédentes de hello. Ce fichier journal nécessite également que hello web application le pare-feu est configuré sur une passerelle d’application. les données de Hello sont stockées dans le compte de stockage hello que vous avez spécifié lorsque vous avez activé la journalisation hello. Hello données suivantes est journalisé :


|Valeur  |Description  |
|---------|---------|
|instanceId     | Instance Application Gateway pour laquelle les données du pare-feu sont générées. Pour une passerelle Application Gateway à plusieurs instances, il y a une ligne par instance.         |
|clientIp     |   Adresse IP d’origine pour la demande de hello.      |
|clientPort     |  Port de demande de hello d’origine.       |
|requestUri     | URL de hello a reçu une demande.       |
|ruleSetType     | Type d’ensemble de règles. la valeur disponible Hello est OWASP avoir.        |
|ruleSetVersion     | Version d’ensemble de règles utilisée. Les valeurs disponibles sont 2.2.9 et 3.0.     |
|ruleId     | ID de règle de hello déclenchant l’événement.        |
|Message     | Message convivial pour hello déclenchant l’événement. Plus de détails sont fournis dans la section relative aux détails hello.        |
|action     |  Action effectuée sur la demande de hello. Les valeurs disponibles sont bloquées et autorisées.      |
|site     | Site pour le hello journal a été généré. Actuellement, seul Global est répertorié car les règles sont globales.|
|détails     | Détails de hello déclenchant l’événement.        |
|details.message     | Description de règle de hello.        |
|details.data     | Données spécifiques trouvé dans la demande de cette règle de mise en correspondance hello.         |
|details.file     | Fichier de configuration contenant une règle de hello.        |
|details.line     | Numéro de ligne dans le fichier de configuration hello ayant déclenché l’événement de hello.       |

```json
{
  "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
  "operationName": "ApplicationGatewayFirewall",
  "time": "2017-03-20T15:52:09.1494499Z",
  "category": "ApplicationGatewayFirewallLog",
  "properties": {
    "instanceId": "ApplicationGatewayRole_IN_0",
    "clientIp": "104.210.252.3",
    "clientPort": "4835",
    "requestUri": "/?a=%3Cscript%3Ealert(%22Hello%22);%3C/script%3E",
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "ruleId": "941320",
    "message": "Possible XSS Attack Detected - HTML Tag Handler",
    "action": "Blocked",
    "site": "Global",
    "details": {
      "message": "Warning. Pattern match \"<(a|abbr|acronym|address|applet|area|audioscope|b|base|basefront|bdo|bgsound|big|blackface|blink|blockquote|body|bq|br|button|caption|center|cite|code|col|colgroup|comment|dd|del|dfn|dir|div|dl|dt|em|embed|fieldset|fn|font|form|frame|frameset|h1|head|h ...\" at ARGS:a.",
      "data": "Matched Data: <script> found within ARGS:a: <script>alert(\\x22hello\\x22);</script>",
      "file": "rules/REQUEST-941-APPLICATION-ATTACK-XSS.conf",
      "line": "865"
    }
  }
} 

```

### <a name="view-and-analyze-hello-activity-log"></a>Afficher et analyser le journal d’activité hello

Vous pouvez afficher et analyser les données de journal d’activité à l’aide d’une des méthodes suivantes de hello :

* **Windows Azure tools**: extraire des informations du journal d’activité hello Azure PowerShell, hello CLI d’Azure, hello API REST de Azure, ou hello portail Azure. Des instructions détaillées pour chaque méthode sont détaillées dans hello [opérations de l’activité avec le Gestionnaire de ressources](../azure-resource-manager/resource-group-audit.md) l’article.
* **Power BI** : si vous n’avez pas encore de compte [Power BI](https://powerbi.microsoft.com/pricing) , vous pouvez l’essayer gratuitement. À l’aide de hello [journaux d’activité Azure pack de contenu pour Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), vous pouvez analyser vos données avec des tableaux de bord préconfigurés que vous pouvez utiliser ou personnaliser.

### <a name="view-and-analyze-hello-access-performance-and-firewall-logs"></a>Afficher et analyser les accès hello, les performances et les journaux de pare-feu

Azure [Analytique de journal](../log-analytics/log-analytics-azure-networking-analytics.md) peut collecter des fichiers de journal des événements et compteurs de hello à partir de votre compte de stockage d’objets Blob. Il inclut des visualisations et recherche de puissantes fonctionnalités tooanalyze vos journaux.

Vous pouvez également connecter le compte de stockage tooyour et récupérer les entrées de journal hello JSON pour les journaux de performances et d’accès. Après avoir téléchargé les fichiers au format JSON hello, vous pouvez convertir les tooCSV et les afficher dans Excel, Power BI ou tout autre outil de visualisation des données.

> [!TIP]
> Si vous êtes familiarisé avec Visual Studio et les concepts de base de la modification des valeurs de constantes et variables dans c#, vous pouvez utiliser hello [ouvrir une session outils de convertisseur](https://github.com/Azure-Samples/networking-dotnet-log-converter) disponible à partir de GitHub.
> 
> 

## <a name="metrics"></a>Mesures

Métriques sont une fonctionnalité de certaines ressources Azure où vous pouvez afficher les compteurs de performance dans le portail de hello. Pour Application Gateway, une métrique est désormais disponible. Cette mesure est le débit, et vous pouvez le voir dans le portail de hello. Parcourir la passerelle d’application tooan et cliquez sur **métriques**. les valeurs hello tooview, sélectionnez débit Bonjour **métriques disponibles** section. Dans hello suivant l’image, vous pouvez voir un exemple avec des filtres hello que vous pouvez utiliser les données de salutation toodisplay dans les plages de temps différent.

![Affichage de métriques avec des filtres][5]

toosee liste actuelle des métriques, consultez [prise en charge des métriques avec Azure analyse](../monitoring-and-diagnostics/monitoring-supported-metrics.md).

### <a name="alert-rules"></a>Règles d'alerte

Vous pouvez démarrer des règles d’alerte en fonction des métriques d’une ressource. Par exemple, une alerte peut appeler un webhook ou un administrateur de messagerie, si le débit de passerelle d’application hello hello est au-dessus, au-dessous ou à un seuil pour une période spécifiée.

Bonjour à l’exemple suivant vous guide tout au long de la création d’une règle d’alerte qui envoie un administrateur de la messagerie tooan après un seuil, les violations de débit :

1. Cliquez sur **ajouter une alerte métrique** tooopen hello **ajouter une règle** panneau. Vous pouvez également atteindre ce panneau à partir du Panneau de métriques hello.

   ![Bouton Ajouter une alerte Métrique][6]

2. Sur hello **ajouter une règle** panneau, renseignez le nom hello, condition et informer des sections, puis cliquez sur **OK**.

   * Bonjour **Condition** sélecteur, sélectionnez une des valeurs de hello quatre : **supérieur**, **égal ou supérieur**, **moins**, ou  **Inférieur ou égal à**.

   * Bonjour **période** sélecteur, sélectionnez une période de 5 minutes too6 heures.

   * Si vous sélectionnez **propriétaires, collaborateurs et les lecteurs de messagerie**, messagerie de hello peut être dynamique basées sur les utilisateurs de hello qui ont accès toothat ressource. Sinon, vous pouvez fournir une liste séparée par des virgules des utilisateurs dans hello **administrateur supplémentaire email(s)** boîte.

   ![Panneau Ajouter une règle][7]

Si le seuil de hello est dépassé, un message électronique qui est similaire toohello un Bonjour suivant image arrive :

![E-mail en cas de dépassement de seuil][8]

Une liste d’alertes apparaît une fois que vous avez créé une alerte Métrique. Il fournit une vue d’ensemble de toutes les règles d’alerte hello.

![Liste d’alertes et de règles][9]

toolearn en savoir plus sur les notifications d’alerte, consultez [recevoir des notifications d’alerte](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).

toounderstand en savoir plus sur le webhooks et comment vous pouvez les utiliser avec les alertes, visitez [configurer un webhook sur une alerte de métrique Azure](../monitoring-and-diagnostics/insights-webhooks-alerts.md).

## <a name="next-steps"></a>Étapes suivantes

* Visualisation du compteur et des journaux des événements à l’aide de [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md).
* Billet de blog sur la [visualisation de votre journal d’activité Azure avec Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx).
* Billet de blog sur [l’affichage et l’analyse des journaux d’activité Azure dans Power BI](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/).

[1]: ./media/application-gateway-diagnostics/figure1.png
[2]: ./media/application-gateway-diagnostics/figure2.png
[3]: ./media/application-gateway-diagnostics/figure3.png
[4]: ./media/application-gateway-diagnostics/figure4.png
[5]: ./media/application-gateway-diagnostics/figure5.png
[6]: ./media/application-gateway-diagnostics/figure6.png
[7]: ./media/application-gateway-diagnostics/figure7.png
[8]: ./media/application-gateway-diagnostics/figure8.png
[9]: ./media/application-gateway-diagnostics/figure9.png
[10]: ./media/application-gateway-diagnostics/figure10.png
