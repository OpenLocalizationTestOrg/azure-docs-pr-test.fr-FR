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
# <a name="back-end-health-diagnostic-logs-and-metrics-for-application-gateway"></a><span data-ttu-id="67175-103">Intégrité du serveur principal, journaux de diagnostic et métriques pour la passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="67175-103">Back-end health, diagnostic logs, and metrics for Application Gateway</span></span>

<span data-ttu-id="67175-104">À l’aide de passerelle d’Application Azure, vous pouvez surveiller les ressources Bonjour suivant des façons :</span><span class="sxs-lookup"><span data-stu-id="67175-104">By using Azure Application Gateway, you can monitor resources in hello following ways:</span></span>

* <span data-ttu-id="67175-105">[Contrôle d’intégrité du serveur principal](#back-end-health): passerelle d’Application fournit hello capacité toomonitor hello la santé des serveurs hello Bonjour pools principaux via le portail Azure de hello et PowerShell.</span><span class="sxs-lookup"><span data-stu-id="67175-105">[Back-end health](#back-end-health): Application Gateway provides hello capability toomonitor hello health of hello servers in hello back-end pools through hello Azure portal and through PowerShell.</span></span> <span data-ttu-id="67175-106">Vous trouverez également la santé des pools de back-end hello via les journaux de diagnostic de performances hello hello.</span><span class="sxs-lookup"><span data-stu-id="67175-106">You can also find hello health of hello back-end pools through hello performance diagnostic logs.</span></span>

* <span data-ttu-id="67175-107">[Journaux](#diagnostic-logs): autoriser les journaux pour les performances, l’accès, et autres toobe données enregistré ou consommés à partir d’une ressource pour la surveillance.</span><span class="sxs-lookup"><span data-stu-id="67175-107">[Logs](#diagnostic-logs): Logs allow for performance, access, and other data toobe saved or consumed from a resource for monitoring purposes.</span></span>

* <span data-ttu-id="67175-108">[Mesures](#metrics) : la passerelle Application Gateway possède actuellement une métrique.</span><span class="sxs-lookup"><span data-stu-id="67175-108">[Metrics](#metrics): Application Gateway currently has one metric.</span></span> <span data-ttu-id="67175-109">Cette mesure mesure débit hello de passerelle d’application hello en octets par seconde.</span><span class="sxs-lookup"><span data-stu-id="67175-109">This metric measures hello throughput of hello application gateway in bytes per second.</span></span>

## <a name="back-end-health"></a><span data-ttu-id="67175-110">Intégrité du serveur principal</span><span class="sxs-lookup"><span data-stu-id="67175-110">Back-end health</span></span>

<span data-ttu-id="67175-111">Passerelle d’application fournit l’intégrité hello capacité toomonitor hello des membres individuels des pools de back-end hello via le portail de hello, PowerShell et hello interface de ligne de commande (CLI).</span><span class="sxs-lookup"><span data-stu-id="67175-111">Application Gateway provides hello capability toomonitor hello health of individual members of hello back-end pools through hello portal, PowerShell, and hello command-line interface (CLI).</span></span> <span data-ttu-id="67175-112">Vous pouvez également trouver l’état d’intégrité agrégé résumé des pools principaux via les journaux de diagnostic de performances hello.</span><span class="sxs-lookup"><span data-stu-id="67175-112">You can also find an aggregated health summary of back-end pools through hello performance diagnostic logs.</span></span> 

<span data-ttu-id="67175-113">rapport de contrôle d’intégrité du serveur principal Hello reflète la sortie hello d’instances de hello Application Gateway intégrité sonde toohello principal.</span><span class="sxs-lookup"><span data-stu-id="67175-113">hello back-end health report reflects hello output of hello Application Gateway health probe toohello back-end instances.</span></span> <span data-ttu-id="67175-114">Lors de la détection a réussi et hello précédent fin peut recevoir du trafic, il est considéré comme sain.</span><span class="sxs-lookup"><span data-stu-id="67175-114">When probing is successful and hello back end can receive traffic, it's considered healthy.</span></span> <span data-ttu-id="67175-115">Sinon, il est considéré comme défaillant.</span><span class="sxs-lookup"><span data-stu-id="67175-115">Otherwise, it's considered unhealthy.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="67175-116">S’il existe un groupe de sécurité réseau (NSG) sur un sous-réseau de passerelle d’Application, ouvrez les plages de ports 65503-65 534 sur le sous-réseau de passerelle d’Application hello pour le trafic entrant.</span><span class="sxs-lookup"><span data-stu-id="67175-116">If there is a network security group (NSG) on an Application Gateway subnet, open port ranges 65503-65534 on hello Application Gateway subnet for inbound traffic.</span></span> <span data-ttu-id="67175-117">Ces ports sont requis pour toowork d’API hello d’intégrité du serveur principal.</span><span class="sxs-lookup"><span data-stu-id="67175-117">These ports are required for hello back-end health API toowork.</span></span>


### <a name="view-back-end-health-through-hello-portal"></a><span data-ttu-id="67175-118">Afficher l’intégrité du serveur principal via le portail de hello</span><span class="sxs-lookup"><span data-stu-id="67175-118">View back-end health through hello portal</span></span>

<span data-ttu-id="67175-119">Dans le portail hello, contrôle d’intégrité du serveur principal est fourni automatiquement.</span><span class="sxs-lookup"><span data-stu-id="67175-119">In hello portal, back-end health is provided automatically.</span></span> <span data-ttu-id="67175-120">Dans une passerelle Application Gateway existante, sélectionnez **Analyse** > **Intégrité du serveur principal**.</span><span class="sxs-lookup"><span data-stu-id="67175-120">In an existing application gateway, select **Monitoring** > **Backend health**.</span></span> 

<span data-ttu-id="67175-121">Chaque membre dans le pool principal d’hello est répertorié dans cette page (si elle est une carte réseau, IP ou nom de domaine complet).</span><span class="sxs-lookup"><span data-stu-id="67175-121">Each member in hello back-end pool is listed on this page (whether it's a NIC, IP, or FQDN).</span></span> <span data-ttu-id="67175-122">Le nom du pool principal, le port, le nom et l’état d’intégrité des paramètres HTTP principaux sont affichés.</span><span class="sxs-lookup"><span data-stu-id="67175-122">Back-end pool name, port, back-end HTTP settings name, and health status are shown.</span></span> <span data-ttu-id="67175-123">Les valeurs valides de l’état d’intégrité sont **Healthy** (Intègre), **Unhealthy** (Défaillant) et **Unknown** (Inconnu).</span><span class="sxs-lookup"><span data-stu-id="67175-123">Valid values for health status are **Healthy**, **Unhealthy**, and **Unknown**.</span></span>

> [!NOTE]
> <span data-ttu-id="67175-124">Si vous voyez l’état d’intégrité du serveur principal **inconnu**, assurez-vous que principale toohello d’accès n’est pas bloqué par une règle de groupe de sécurité réseau, un itinéraire défini par l’utilisateur (UDR) ou un DNS personnalisé hello du réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="67175-124">If you see a back-end health status of **Unknown**, ensure that access toohello back end is not blocked by an NSG rule, a user-defined route (UDR), or a custom DNS in hello virtual network.</span></span>

![Intégrité du serveur principal][10]

### <a name="view-back-end-health-through-powershell"></a><span data-ttu-id="67175-126">Affichage de l’intégrité du serveur principal via PowerShell</span><span class="sxs-lookup"><span data-stu-id="67175-126">View back-end health through PowerShell</span></span>

<span data-ttu-id="67175-127">Hello suivant code PowerShell montre comment le contrôle d’intégrité du serveur principal tooview à l’aide de hello `Get-AzureRmApplicationGatewayBackendHealth` applet de commande :</span><span class="sxs-lookup"><span data-stu-id="67175-127">hello following PowerShell code shows how tooview back-end health by using hello `Get-AzureRmApplicationGatewayBackendHealth` cmdlet:</span></span>

```powershell
Get-AzureRmApplicationGatewayBackendHealth -Name ApplicationGateway1 -ResourceGroupName Contoso
```

### <a name="view-back-end-health-through-azure-cli-20"></a><span data-ttu-id="67175-128">Affichage de l’intégrité du serveur principal via Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="67175-128">View back-end health through Azure CLI 2.0</span></span>

```azurecli
az network application-gateway show-backend-health --resource-group AdatumAppGatewayRG --name AdatumAppGateway
```

### <a name="results"></a><span data-ttu-id="67175-129">Résultats</span><span class="sxs-lookup"><span data-stu-id="67175-129">Results</span></span>

<span data-ttu-id="67175-130">Hello suivant extrait de code illustre un exemple de réponse de hello :</span><span class="sxs-lookup"><span data-stu-id="67175-130">hello following snippet shows an example of hello response:</span></span>

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

## <span data-ttu-id="67175-131"><a name="diagnostic-logging"></a>Journaux de diagnostic</span><span class="sxs-lookup"><span data-stu-id="67175-131"><a name="diagnostic-logging"></a>Diagnostic logs</span></span>

<span data-ttu-id="67175-132">Vous pouvez utiliser différents types de journaux dans Azure toomanage et résoudre les problèmes de passerelles d’application.</span><span class="sxs-lookup"><span data-stu-id="67175-132">You can use different types of logs in Azure toomanage and troubleshoot application gateways.</span></span> <span data-ttu-id="67175-133">Vous pouvez accéder à certaines de ces journaux via le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="67175-133">You can access some of these logs through hello portal.</span></span> <span data-ttu-id="67175-134">Tous les journaux peuvent être extraits à partir d’un stockage Blob Azure et affichés dans différents outils, comme [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md), Excel et PowerBI.</span><span class="sxs-lookup"><span data-stu-id="67175-134">All logs can be extracted from Azure Blob storage and viewed in different tools, such as [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md), Excel, and Power BI.</span></span> <span data-ttu-id="67175-135">Pour plus d’informations sur hello différents types de journaux de hello suivant liste :</span><span class="sxs-lookup"><span data-stu-id="67175-135">You can learn more about hello different types of logs from hello following list:</span></span>

* <span data-ttu-id="67175-136">**Journal d’activité**: vous pouvez utiliser [journaux d’activité Azure](../monitoring-and-diagnostics/insights-debugging-with-events.md) (précédemment appelés journaux des opérations et les journaux d’audit) tooview toutes les opérations qui sont soumis tooyour abonnement Azure, ainsi que leur état.</span><span class="sxs-lookup"><span data-stu-id="67175-136">**Activity log**: You can use [Azure activity logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) (formerly known as operational logs and audit logs) tooview all operations that are submitted tooyour Azure subscription, and their status.</span></span> <span data-ttu-id="67175-137">Entrées de journal d’activité sont collectées par défaut, et vous pouvez les visualiser dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="67175-137">Activity log entries are collected by default, and you can view them in hello Azure portal.</span></span>
* <span data-ttu-id="67175-138">**Journal d’accès**: vous pouvez utiliser cette modèles d’accès journal tooview passerelle d’Application et analyser des informations importantes, l’appelant, y compris hello IP, URL demandée, latence de la réponse, code de retour et d’octets et l’extraction. Un journal d’accès est collecté toutes les 300 secondes.</span><span class="sxs-lookup"><span data-stu-id="67175-138">**Access log**: You can use this log tooview Application Gateway access patterns and analyze important information, including hello caller's IP, requested URL, response latency, return code, and bytes in and out. An access log is collected every 300 seconds.</span></span> <span data-ttu-id="67175-139">Ce journal contient un enregistrement par instance Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="67175-139">This log contains one record per instance of Application Gateway.</span></span> <span data-ttu-id="67175-140">instance de la passerelle d’Application Hello peut être identifiée par la propriété instanceId de hello.</span><span class="sxs-lookup"><span data-stu-id="67175-140">hello Application Gateway instance can be identified by hello instanceId property.</span></span>
* <span data-ttu-id="67175-141">**Journal de performances**: vous pouvez utiliser cette tooview du journal des performances des instances de la passerelle d’Application.</span><span class="sxs-lookup"><span data-stu-id="67175-141">**Performance log**: You can use this log tooview how Application Gateway instances are performing.</span></span> <span data-ttu-id="67175-142">Ce journal capture des informations sur les performances de chaque instance, notamment le nombre total de requêtes traitées, le débit en octets, le nombre total de requêtes présentées, le nombre de requêtes ayant échoué, le nombre d’instances du serveur principal intègres et défectueuses.</span><span class="sxs-lookup"><span data-stu-id="67175-142">This log captures performance information for each instance, including total requests served, throughput in bytes, total requests served, failed request count, and healthy and unhealthy back-end instance count.</span></span> <span data-ttu-id="67175-143">Le journal des performances est collecté toutes les 60 secondes.</span><span class="sxs-lookup"><span data-stu-id="67175-143">A performance log is collected every 60 seconds.</span></span>
* <span data-ttu-id="67175-144">**Journal du pare-feu**: vous pouvez utiliser ce journal tooview hello les demandes qui sont enregistrés via le mode de détection ou de prévention d’une passerelle d’application qui est configuré avec un pare-feu d’applications web hello.</span><span class="sxs-lookup"><span data-stu-id="67175-144">**Firewall log**: You can use this log tooview hello requests that are logged through either detection or prevention mode of an application gateway that is configured with hello web application firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="67175-145">Les journaux sont disponibles uniquement pour les ressources déployées dans le modèle de déploiement du Gestionnaire de ressources Azure hello.</span><span class="sxs-lookup"><span data-stu-id="67175-145">Logs are available only for resources deployed in hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="67175-146">Vous ne pouvez pas utiliser les journaux pour les ressources dans le modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="67175-146">You cannot use logs for resources in hello classic deployment model.</span></span> <span data-ttu-id="67175-147">Pour mieux comprendre les modèles hello deux, consultez hello [déploiement du Gestionnaire de ressources de présentation et déploiement classique](../azure-resource-manager/resource-manager-deployment-model.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="67175-147">For a better understanding of hello two models, see hello [Understanding Resource Manager deployment and classic deployment](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

<span data-ttu-id="67175-148">Pour stocker vos journaux, vous disposez de trois options :</span><span class="sxs-lookup"><span data-stu-id="67175-148">You have three options for storing your logs:</span></span>

* <span data-ttu-id="67175-149">**Compte de stockage** : les comptes de stockage conviennent parfaitement aux journaux lorsqu’ils sont stockés pour une durée plus longue et consultés lorsque nécessaire.</span><span class="sxs-lookup"><span data-stu-id="67175-149">**Storage account**: Storage accounts are best used for logs when logs are stored for a longer duration and reviewed when needed.</span></span>
* <span data-ttu-id="67175-150">**Concentrateurs d’événements**: concentrateurs d’événements sont une option intéressante pour l’intégration avec d’autres informations de sécurité et des outils de gestion des événements (SEIM) tooget des alertes sur vos ressources.</span><span class="sxs-lookup"><span data-stu-id="67175-150">**Event hubs**: Event hubs are a great option for integrating with other security information and event management (SEIM) tools tooget alerts on your resources.</span></span>
* <span data-ttu-id="67175-151">**Log Analytics** : Log Analytics convient parfaitement pour la surveillance en temps réel générale de votre application ou la recherche de tendances.</span><span class="sxs-lookup"><span data-stu-id="67175-151">**Log Analytics**: Log Analytics is best used for general real-time monitoring of your application or looking at trends.</span></span>

### <a name="enable-logging-through-powershell"></a><span data-ttu-id="67175-152">Activation de la journalisation avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="67175-152">Enable logging through PowerShell</span></span>

<span data-ttu-id="67175-153">La journalisation d’activité est automatiquement activée pour chaque ressource Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="67175-153">Activity logging is automatically enabled for every Resource Manager resource.</span></span> <span data-ttu-id="67175-154">Vous devez activer l’accès et toostart de journalisation de performances collecte des données hello ces journaux.</span><span class="sxs-lookup"><span data-stu-id="67175-154">You must enable access and performance logging toostart collecting hello data available through those logs.</span></span> <span data-ttu-id="67175-155">tooenable journalisation, hello utilisation comme suit :</span><span class="sxs-lookup"><span data-stu-id="67175-155">tooenable logging, use hello following steps:</span></span>

1. <span data-ttu-id="67175-156">Notez l’ID de ressource de votre compte de stockage, où sont stockées les données de journal hello.</span><span class="sxs-lookup"><span data-stu-id="67175-156">Note your storage account's resource ID, where hello log data is stored.</span></span> <span data-ttu-id="67175-157">Cette valeur se présente sous forme de hello : /subscriptions/\<subscriptionId\>/resourceGroups/\<nom de groupe de ressources\>/providers/Microsoft.Storage/storageAccounts/\<le nom de compte de stockage\>.</span><span class="sxs-lookup"><span data-stu-id="67175-157">This value is of hello form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Storage/storageAccounts/\<storage account name\>.</span></span> <span data-ttu-id="67175-158">Vous pouvez utiliser n’importe quel compte de stockage dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="67175-158">You can use any storage account in your subscription.</span></span> <span data-ttu-id="67175-159">Ces informations, vous pouvez utiliser hello toofind portail Azure.</span><span class="sxs-lookup"><span data-stu-id="67175-159">You can use hello Azure portal toofind this information.</span></span>

    ![Portail : ID de ressource du compte de stockage](./media/application-gateway-diagnostics/diagnostics1.png)

2. <span data-ttu-id="67175-161">Notez l’ID de ressource de votre passerelle Application Gateway pour laquelle la journalisation est activée.</span><span class="sxs-lookup"><span data-stu-id="67175-161">Note your application gateway's resource ID for which logging is enabled.</span></span> <span data-ttu-id="67175-162">Cette valeur se présente sous forme de hello : /subscriptions/\<subscriptionId\>/resourceGroups/\<nom de groupe de ressources\>/providers/Microsoft.Network/applicationGateways/\<passerelle d’application nom\>.</span><span class="sxs-lookup"><span data-stu-id="67175-162">This value is of hello form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Network/applicationGateways/\<application gateway name\>.</span></span> <span data-ttu-id="67175-163">Vous pouvez utiliser les toofind portail hello ces informations.</span><span class="sxs-lookup"><span data-stu-id="67175-163">You can use hello portal toofind this information.</span></span>

    ![Portail : ID de ressource de la passerelle Application Gateway](./media/application-gateway-diagnostics/diagnostics2.png)

3. <span data-ttu-id="67175-165">Activer la journalisation de diagnostic à l’aide de hello suivant l’applet de commande PowerShell :</span><span class="sxs-lookup"><span data-stu-id="67175-165">Enable diagnostic logging by using hello following PowerShell cmdlet:</span></span>

    ```powershell
    Set-AzureRmDiagnosticSetting  -ResourceId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name> -StorageAccountId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Storage/storageAccounts/<storage account name> -Enabled $true     
    ```
    
> [!TIP] 
><span data-ttu-id="67175-166">Les journaux d’activité ne nécessitent pas de compte de stockage distinct.</span><span class="sxs-lookup"><span data-stu-id="67175-166">Activity logs do not require a separate storage account.</span></span> <span data-ttu-id="67175-167">utilisation de Hello du stockage pour l’accès et l’enregistrement des performances entraîne des frais de service.</span><span class="sxs-lookup"><span data-stu-id="67175-167">hello use of storage for access and performance logging incurs service charges.</span></span>

### <a name="enable-logging-through-hello-azure-portal"></a><span data-ttu-id="67175-168">Activer la journalisation via hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="67175-168">Enable logging through hello Azure portal</span></span>

1. <span data-ttu-id="67175-169">Hello portail Azure, votre ressource et cliquez sur **journaux de Diagnostic**.</span><span class="sxs-lookup"><span data-stu-id="67175-169">In hello Azure portal, find your resource and click **Diagnostic logs**.</span></span>

   <span data-ttu-id="67175-170">Pour Application Gateway, trois journaux d’audit sont disponibles :</span><span class="sxs-lookup"><span data-stu-id="67175-170">For Application Gateway, three logs are available:</span></span>

   * <span data-ttu-id="67175-171">Journal d’accès</span><span class="sxs-lookup"><span data-stu-id="67175-171">Access log</span></span>
   * <span data-ttu-id="67175-172">Journal des performances</span><span class="sxs-lookup"><span data-stu-id="67175-172">Performance log</span></span>
   * <span data-ttu-id="67175-173">Journal du pare-feu</span><span class="sxs-lookup"><span data-stu-id="67175-173">Firewall log</span></span>

2. <span data-ttu-id="67175-174">toostart la collecte de données, cliquez sur **activer les diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="67175-174">toostart collecting data, click **Turn on diagnostics**.</span></span>

   ![Activation des diagnostics][1]

3. <span data-ttu-id="67175-176">Hello **paramètres de diagnostic** panneau fournit les paramètres hello hello des journaux de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="67175-176">hello **Diagnostics settings** blade provides hello settings for hello diagnostic logs.</span></span> <span data-ttu-id="67175-177">Dans cet exemple, Analytique de journal stocke les journaux de hello.</span><span class="sxs-lookup"><span data-stu-id="67175-177">In this example, Log Analytics stores hello logs.</span></span> <span data-ttu-id="67175-178">Cliquez sur **configurer** sous **Analytique de journal** tooconfigure votre espace de travail.</span><span class="sxs-lookup"><span data-stu-id="67175-178">Click **Configure** under **Log Analytics** tooconfigure your workspace.</span></span> <span data-ttu-id="67175-179">Vous pouvez également utiliser des hubs d’événements et un stockage compte toosave hello diagnostic se connecte.</span><span class="sxs-lookup"><span data-stu-id="67175-179">You can also use event hubs and a storage account toosave hello diagnostic logs.</span></span>

   ![Démarrage du processus de configuration hello][2]

4. <span data-ttu-id="67175-181">Sélectionnez ou créez un espace de travail OMS (Operations Management Suite) existant.</span><span class="sxs-lookup"><span data-stu-id="67175-181">Choose an existing Operations Management Suite (OMS) workspace or create a new one.</span></span> <span data-ttu-id="67175-182">Cet exemple utilise un espace de travail existant.</span><span class="sxs-lookup"><span data-stu-id="67175-182">This example uses an existing one.</span></span>

   ![Options des espaces de travail OMS][3]

5. <span data-ttu-id="67175-184">Confirmez les paramètres hello et cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="67175-184">Confirm hello settings and click **Save**.</span></span>

   ![Panneau des paramètres de diagnostic avec des sélections][4]

### <a name="activity-log"></a><span data-ttu-id="67175-186">Journal d’activité</span><span class="sxs-lookup"><span data-stu-id="67175-186">Activity log</span></span>

<span data-ttu-id="67175-187">Azure génère un journal d’activité hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="67175-187">Azure generates hello activity log by default.</span></span> <span data-ttu-id="67175-188">dans le magasin de journaux des événements Azure hello, Hello journaux sont conservées pendant 90 jours.</span><span class="sxs-lookup"><span data-stu-id="67175-188">hello logs are preserved for 90 days in hello Azure event logs store.</span></span> <span data-ttu-id="67175-189">En savoir plus sur ces journaux en lisant hello [afficher les événements et le journal d’activité](../monitoring-and-diagnostics/insights-debugging-with-events.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="67175-189">Learn more about these logs by reading hello [View events and activity log](../monitoring-and-diagnostics/insights-debugging-with-events.md) article.</span></span>

### <a name="access-log"></a><span data-ttu-id="67175-190">Journal d’accès</span><span class="sxs-lookup"><span data-stu-id="67175-190">Access log</span></span>

<span data-ttu-id="67175-191">journal d’accès Hello est généré uniquement si vous l’avez activé sur chaque instance de la passerelle d’Application, comme expliqué dans les étapes précédentes de hello.</span><span class="sxs-lookup"><span data-stu-id="67175-191">hello access log is generated only if you've enabled it on each Application Gateway instance, as detailed in hello preceding steps.</span></span> <span data-ttu-id="67175-192">les données de Hello sont stockées dans le compte de stockage hello que vous avez spécifié lorsque vous avez activé la journalisation hello.</span><span class="sxs-lookup"><span data-stu-id="67175-192">hello data is stored in hello storage account that you specified when you enabled hello logging.</span></span> <span data-ttu-id="67175-193">Chaque accès de la passerelle d’Application est enregistré au format JSON, comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="67175-193">Each access of Application Gateway is logged in JSON format, as shown in hello following example:</span></span>


|<span data-ttu-id="67175-194">Valeur</span><span class="sxs-lookup"><span data-stu-id="67175-194">Value</span></span>  |<span data-ttu-id="67175-195">Description</span><span class="sxs-lookup"><span data-stu-id="67175-195">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="67175-196">instanceId</span><span class="sxs-lookup"><span data-stu-id="67175-196">instanceId</span></span>     | <span data-ttu-id="67175-197">Cette demande hello servi d’instance de passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="67175-197">Application Gateway instance that served hello request.</span></span>        |
|<span data-ttu-id="67175-198">clientIP</span><span class="sxs-lookup"><span data-stu-id="67175-198">clientIP</span></span>     | <span data-ttu-id="67175-199">Adresse IP d’origine pour la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="67175-199">Originating IP for hello request.</span></span>        |
|<span data-ttu-id="67175-200">clientPort</span><span class="sxs-lookup"><span data-stu-id="67175-200">clientPort</span></span>     | <span data-ttu-id="67175-201">Port de demande de hello d’origine.</span><span class="sxs-lookup"><span data-stu-id="67175-201">Originating port for hello request.</span></span>       |
|<span data-ttu-id="67175-202">httpMethod</span><span class="sxs-lookup"><span data-stu-id="67175-202">httpMethod</span></span>     | <span data-ttu-id="67175-203">Méthode HTTP utilisée par la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="67175-203">HTTP method used by hello request.</span></span>       |
|<span data-ttu-id="67175-204">requestUri</span><span class="sxs-lookup"><span data-stu-id="67175-204">requestUri</span></span>     | <span data-ttu-id="67175-205">URI de hello a reçu une demande.</span><span class="sxs-lookup"><span data-stu-id="67175-205">URI of hello received request.</span></span>        |
|<span data-ttu-id="67175-206">RequestQuery</span><span class="sxs-lookup"><span data-stu-id="67175-206">RequestQuery</span></span>     | <span data-ttu-id="67175-207">**Server avait acheminé**: instance de pool principal qui a été envoyé à la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="67175-207">**Server-Routed**: Back-end pool instance that was sent hello request.</span></span> </br> <span data-ttu-id="67175-208">**X-AzureApplicationGateway-journal-ID**: ID de corrélation utilisé pour la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="67175-208">**X-AzureApplicationGateway-LOG-ID**: Correlation ID used for hello request.</span></span> <span data-ttu-id="67175-209">Il peut être utilisé tootroubleshoot les problèmes de trafic sur les serveurs principaux hello.</span><span class="sxs-lookup"><span data-stu-id="67175-209">It can be used tootroubleshoot traffic issues on hello back-end servers.</span></span> </br><span data-ttu-id="67175-210">**ÉTAT du serveur**: code de réponse HTTP passerelle d’Application a reçu back-end hello.</span><span class="sxs-lookup"><span data-stu-id="67175-210">**SERVER-STATUS**: HTTP response code that Application Gateway received from hello back end.</span></span>       |
|<span data-ttu-id="67175-211">UserAgent</span><span class="sxs-lookup"><span data-stu-id="67175-211">UserAgent</span></span>     | <span data-ttu-id="67175-212">Agent utilisateur à partir de l’en-tête de demande HTTP de hello.</span><span class="sxs-lookup"><span data-stu-id="67175-212">User agent from hello HTTP request header.</span></span>        |
|<span data-ttu-id="67175-213">httpStatus</span><span class="sxs-lookup"><span data-stu-id="67175-213">httpStatus</span></span>     | <span data-ttu-id="67175-214">Code d’état HTTP retourné toohello client à partir de la passerelle d’Application.</span><span class="sxs-lookup"><span data-stu-id="67175-214">HTTP status code returned toohello client from Application Gateway.</span></span>       |
|<span data-ttu-id="67175-215">httpVersion</span><span class="sxs-lookup"><span data-stu-id="67175-215">httpVersion</span></span>     | <span data-ttu-id="67175-216">Version HTTP de la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="67175-216">HTTP version of hello request.</span></span>        |
|<span data-ttu-id="67175-217">receivedBytes</span><span class="sxs-lookup"><span data-stu-id="67175-217">receivedBytes</span></span>     | <span data-ttu-id="67175-218">Taille du paquet reçu, en octets.</span><span class="sxs-lookup"><span data-stu-id="67175-218">Size of packet received, in bytes.</span></span>        |
|<span data-ttu-id="67175-219">sentBytes</span><span class="sxs-lookup"><span data-stu-id="67175-219">sentBytes</span></span>| <span data-ttu-id="67175-220">Taille du paquet envoyé, en octets.</span><span class="sxs-lookup"><span data-stu-id="67175-220">Size of packet sent, in bytes.</span></span>|
|<span data-ttu-id="67175-221">timeTaken</span><span class="sxs-lookup"><span data-stu-id="67175-221">timeTaken</span></span>| <span data-ttu-id="67175-222">Durée (en millisecondes) nécessaire pour une toobe demande traités et son toobe de réponse envoyé.</span><span class="sxs-lookup"><span data-stu-id="67175-222">Length of time (in milliseconds) that it takes for a request toobe processed and its response toobe sent.</span></span> <span data-ttu-id="67175-223">Elle est calculée comme intervalle hello de temps hello lorsque la passerelle d’Application reçoit hello premier octet d’une durée de toohello de demande HTTP lorsque la réponse de hello envoyez fin de l’opération.</span><span class="sxs-lookup"><span data-stu-id="67175-223">This is calculated as hello interval from hello time when Application Gateway receives hello first byte of an HTTP request toohello time when hello response send operation finishes.</span></span> <span data-ttu-id="67175-224">Il est important de toonote qui hello Time-Taken le champ généralement inclut le temps hello hello demande et réponse les paquets réseau hello.</span><span class="sxs-lookup"><span data-stu-id="67175-224">It's important toonote that hello Time-Taken field usually includes hello time that hello request and response packets are traveling over hello network.</span></span> |
|<span data-ttu-id="67175-225">sslEnabled</span><span class="sxs-lookup"><span data-stu-id="67175-225">sslEnabled</span></span>| <span data-ttu-id="67175-226">Indique si les pools de communication toohello principal utilisé SSL.</span><span class="sxs-lookup"><span data-stu-id="67175-226">Whether communication toohello back-end pools used SSL.</span></span> <span data-ttu-id="67175-227">Les valeurs valides sont On (Activé) et Off (Désactivé).</span><span class="sxs-lookup"><span data-stu-id="67175-227">Valid values are on and off.</span></span>|
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

### <a name="performance-log"></a><span data-ttu-id="67175-228">Journal des performances</span><span class="sxs-lookup"><span data-stu-id="67175-228">Performance log</span></span>

<span data-ttu-id="67175-229">journal de performances Hello est généré uniquement si vous l’avez activé sur chaque instance de la passerelle d’Application, comme expliqué dans les étapes précédentes de hello.</span><span class="sxs-lookup"><span data-stu-id="67175-229">hello performance log is generated only if you have enabled it on each Application Gateway instance, as detailed in hello preceding steps.</span></span> <span data-ttu-id="67175-230">les données de Hello sont stockées dans le compte de stockage hello que vous avez spécifié lorsque vous avez activé la journalisation hello.</span><span class="sxs-lookup"><span data-stu-id="67175-230">hello data is stored in hello storage account that you specified when you enabled hello logging.</span></span> <span data-ttu-id="67175-231">données de journal de performances Hello sont générées par intervalles de 1 minute.</span><span class="sxs-lookup"><span data-stu-id="67175-231">hello performance log data is generated in 1-minute intervals.</span></span> <span data-ttu-id="67175-232">Hello données suivantes est journalisé :</span><span class="sxs-lookup"><span data-stu-id="67175-232">hello following data is logged:</span></span>


|<span data-ttu-id="67175-233">Valeur</span><span class="sxs-lookup"><span data-stu-id="67175-233">Value</span></span>  |<span data-ttu-id="67175-234">Description</span><span class="sxs-lookup"><span data-stu-id="67175-234">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="67175-235">instanceId</span><span class="sxs-lookup"><span data-stu-id="67175-235">instanceId</span></span>     |  <span data-ttu-id="67175-236">Instance Application Gateway pour laquelle les données des performances sont générées.</span><span class="sxs-lookup"><span data-stu-id="67175-236">Application Gateway instance for which performance data is being generated.</span></span> <span data-ttu-id="67175-237">Pour une passerelle Application Gateway à plusieurs instances, il y a une ligne par instance.</span><span class="sxs-lookup"><span data-stu-id="67175-237">For a multiple-instance application gateway, there is one row per instance.</span></span>        |
|<span data-ttu-id="67175-238">healthyHostCount</span><span class="sxs-lookup"><span data-stu-id="67175-238">healthyHostCount</span></span>     | <span data-ttu-id="67175-239">Nombre d’hôtes intègres dans le pool principal d’hello.</span><span class="sxs-lookup"><span data-stu-id="67175-239">Number of healthy hosts in hello back-end pool.</span></span>        |
|<span data-ttu-id="67175-240">unHealthyHostCount</span><span class="sxs-lookup"><span data-stu-id="67175-240">unHealthyHostCount</span></span>     | <span data-ttu-id="67175-241">Nombre d’hôtes défectueux dans le pool principal d’hello.</span><span class="sxs-lookup"><span data-stu-id="67175-241">Number of unhealthy hosts in hello back-end pool.</span></span>        |
|<span data-ttu-id="67175-242">requestCount</span><span class="sxs-lookup"><span data-stu-id="67175-242">requestCount</span></span>     | <span data-ttu-id="67175-243">Nombre de requêtes traitées.</span><span class="sxs-lookup"><span data-stu-id="67175-243">Number of requests served.</span></span>        |
|<span data-ttu-id="67175-244">latency</span><span class="sxs-lookup"><span data-stu-id="67175-244">latency</span></span> | <span data-ttu-id="67175-245">Latence (en millisecondes) des demandes de hello instance toohello back-end qui sert les demandes hello.</span><span class="sxs-lookup"><span data-stu-id="67175-245">Latency (in milliseconds) of requests from hello instance toohello back end that serves hello requests.</span></span> |
|<span data-ttu-id="67175-246">failedRequestCount</span><span class="sxs-lookup"><span data-stu-id="67175-246">failedRequestCount</span></span>| <span data-ttu-id="67175-247">Nombre d’échecs de requêtes.</span><span class="sxs-lookup"><span data-stu-id="67175-247">Number of failed requests.</span></span>|
|<span data-ttu-id="67175-248">throughput</span><span class="sxs-lookup"><span data-stu-id="67175-248">throughput</span></span>| <span data-ttu-id="67175-249">Débit moyen depuis le dernier journal hello, mesurée en octets par seconde.</span><span class="sxs-lookup"><span data-stu-id="67175-249">Average throughput since hello last log, measured in bytes per second.</span></span>|

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
> <span data-ttu-id="67175-250">La latence est calculée à partir de l’heure hello lorsque hello du premier octet de demande de hello HTTP est reçu toohello pendant laquelle hello dernier octet de réponse HTTP de hello est envoyée.</span><span class="sxs-lookup"><span data-stu-id="67175-250">Latency is calculated from hello time when hello first byte of hello HTTP request is received toohello time when hello last byte of hello HTTP response is sent.</span></span> <span data-ttu-id="67175-251">Son hello somme de hello passerelle d’Application le temps de traitement plus hello toohello du coût du réseau précédent se terminer, plus le temps hello hello back-end prend tooprocess hello demande.</span><span class="sxs-lookup"><span data-stu-id="67175-251">It's hello sum of hello Application Gateway processing time plus hello network cost toohello back end, plus hello time that hello back end takes tooprocess hello request.</span></span>

### <a name="firewall-log"></a><span data-ttu-id="67175-252">Journal du pare-feu</span><span class="sxs-lookup"><span data-stu-id="67175-252">Firewall log</span></span>

<span data-ttu-id="67175-253">journal du pare-feu Hello est généré uniquement si vous l’avez activé pour chaque application gateway, comme expliqué dans les étapes précédentes de hello.</span><span class="sxs-lookup"><span data-stu-id="67175-253">hello firewall log is generated only if you have enabled it for each application gateway, as detailed in hello preceding steps.</span></span> <span data-ttu-id="67175-254">Ce fichier journal nécessite également que hello web application le pare-feu est configuré sur une passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="67175-254">This log also requires that hello web application firewall is configured on an application gateway.</span></span> <span data-ttu-id="67175-255">les données de Hello sont stockées dans le compte de stockage hello que vous avez spécifié lorsque vous avez activé la journalisation hello.</span><span class="sxs-lookup"><span data-stu-id="67175-255">hello data is stored in hello storage account that you specified when you enabled hello logging.</span></span> <span data-ttu-id="67175-256">Hello données suivantes est journalisé :</span><span class="sxs-lookup"><span data-stu-id="67175-256">hello following data is logged:</span></span>


|<span data-ttu-id="67175-257">Valeur</span><span class="sxs-lookup"><span data-stu-id="67175-257">Value</span></span>  |<span data-ttu-id="67175-258">Description</span><span class="sxs-lookup"><span data-stu-id="67175-258">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="67175-259">instanceId</span><span class="sxs-lookup"><span data-stu-id="67175-259">instanceId</span></span>     | <span data-ttu-id="67175-260">Instance Application Gateway pour laquelle les données du pare-feu sont générées.</span><span class="sxs-lookup"><span data-stu-id="67175-260">Application Gateway instance for which firewall data is being generated.</span></span> <span data-ttu-id="67175-261">Pour une passerelle Application Gateway à plusieurs instances, il y a une ligne par instance.</span><span class="sxs-lookup"><span data-stu-id="67175-261">For a multiple-instance application gateway, there is one row per instance.</span></span>         |
|<span data-ttu-id="67175-262">clientIp</span><span class="sxs-lookup"><span data-stu-id="67175-262">clientIp</span></span>     |   <span data-ttu-id="67175-263">Adresse IP d’origine pour la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="67175-263">Originating IP for hello request.</span></span>      |
|<span data-ttu-id="67175-264">clientPort</span><span class="sxs-lookup"><span data-stu-id="67175-264">clientPort</span></span>     |  <span data-ttu-id="67175-265">Port de demande de hello d’origine.</span><span class="sxs-lookup"><span data-stu-id="67175-265">Originating port for hello request.</span></span>       |
|<span data-ttu-id="67175-266">requestUri</span><span class="sxs-lookup"><span data-stu-id="67175-266">requestUri</span></span>     | <span data-ttu-id="67175-267">URL de hello a reçu une demande.</span><span class="sxs-lookup"><span data-stu-id="67175-267">URL of hello received request.</span></span>       |
|<span data-ttu-id="67175-268">ruleSetType</span><span class="sxs-lookup"><span data-stu-id="67175-268">ruleSetType</span></span>     | <span data-ttu-id="67175-269">Type d’ensemble de règles.</span><span class="sxs-lookup"><span data-stu-id="67175-269">Rule set type.</span></span> <span data-ttu-id="67175-270">la valeur disponible Hello est OWASP avoir.</span><span class="sxs-lookup"><span data-stu-id="67175-270">hello available value is OWASP.</span></span>        |
|<span data-ttu-id="67175-271">ruleSetVersion</span><span class="sxs-lookup"><span data-stu-id="67175-271">ruleSetVersion</span></span>     | <span data-ttu-id="67175-272">Version d’ensemble de règles utilisée.</span><span class="sxs-lookup"><span data-stu-id="67175-272">Rule set version used.</span></span> <span data-ttu-id="67175-273">Les valeurs disponibles sont 2.2.9 et 3.0.</span><span class="sxs-lookup"><span data-stu-id="67175-273">Available values are 2.2.9 and 3.0.</span></span>     |
|<span data-ttu-id="67175-274">ruleId</span><span class="sxs-lookup"><span data-stu-id="67175-274">ruleId</span></span>     | <span data-ttu-id="67175-275">ID de règle de hello déclenchant l’événement.</span><span class="sxs-lookup"><span data-stu-id="67175-275">Rule ID of hello triggering event.</span></span>        |
|<span data-ttu-id="67175-276">Message</span><span class="sxs-lookup"><span data-stu-id="67175-276">message</span></span>     | <span data-ttu-id="67175-277">Message convivial pour hello déclenchant l’événement.</span><span class="sxs-lookup"><span data-stu-id="67175-277">User-friendly message for hello triggering event.</span></span> <span data-ttu-id="67175-278">Plus de détails sont fournis dans la section relative aux détails hello.</span><span class="sxs-lookup"><span data-stu-id="67175-278">More details are provided in hello details section.</span></span>        |
|<span data-ttu-id="67175-279">action</span><span class="sxs-lookup"><span data-stu-id="67175-279">action</span></span>     |  <span data-ttu-id="67175-280">Action effectuée sur la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="67175-280">Action taken on hello request.</span></span> <span data-ttu-id="67175-281">Les valeurs disponibles sont bloquées et autorisées.</span><span class="sxs-lookup"><span data-stu-id="67175-281">Available values are Blocked and Allowed.</span></span>      |
|<span data-ttu-id="67175-282">site</span><span class="sxs-lookup"><span data-stu-id="67175-282">site</span></span>     | <span data-ttu-id="67175-283">Site pour le hello journal a été généré.</span><span class="sxs-lookup"><span data-stu-id="67175-283">Site for which hello log was generated.</span></span> <span data-ttu-id="67175-284">Actuellement, seul Global est répertorié car les règles sont globales.</span><span class="sxs-lookup"><span data-stu-id="67175-284">Currently, only Global is listed because rules are global.</span></span>|
|<span data-ttu-id="67175-285">détails</span><span class="sxs-lookup"><span data-stu-id="67175-285">details</span></span>     | <span data-ttu-id="67175-286">Détails de hello déclenchant l’événement.</span><span class="sxs-lookup"><span data-stu-id="67175-286">Details of hello triggering event.</span></span>        |
|<span data-ttu-id="67175-287">details.message</span><span class="sxs-lookup"><span data-stu-id="67175-287">details.message</span></span>     | <span data-ttu-id="67175-288">Description de règle de hello.</span><span class="sxs-lookup"><span data-stu-id="67175-288">Description of hello rule.</span></span>        |
|<span data-ttu-id="67175-289">details.data</span><span class="sxs-lookup"><span data-stu-id="67175-289">details.data</span></span>     | <span data-ttu-id="67175-290">Données spécifiques trouvé dans la demande de cette règle de mise en correspondance hello.</span><span class="sxs-lookup"><span data-stu-id="67175-290">Specific data found in request that matched hello rule.</span></span>         |
|<span data-ttu-id="67175-291">details.file</span><span class="sxs-lookup"><span data-stu-id="67175-291">details.file</span></span>     | <span data-ttu-id="67175-292">Fichier de configuration contenant une règle de hello.</span><span class="sxs-lookup"><span data-stu-id="67175-292">Configuration file that contained hello rule.</span></span>        |
|<span data-ttu-id="67175-293">details.line</span><span class="sxs-lookup"><span data-stu-id="67175-293">details.line</span></span>     | <span data-ttu-id="67175-294">Numéro de ligne dans le fichier de configuration hello ayant déclenché l’événement de hello.</span><span class="sxs-lookup"><span data-stu-id="67175-294">Line number in hello configuration file that triggered hello event.</span></span>       |

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

### <a name="view-and-analyze-hello-activity-log"></a><span data-ttu-id="67175-295">Afficher et analyser le journal d’activité hello</span><span class="sxs-lookup"><span data-stu-id="67175-295">View and analyze hello activity log</span></span>

<span data-ttu-id="67175-296">Vous pouvez afficher et analyser les données de journal d’activité à l’aide d’une des méthodes suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="67175-296">You can view and analyze activity log data by using any of hello following methods:</span></span>

* <span data-ttu-id="67175-297">**Windows Azure tools**: extraire des informations du journal d’activité hello Azure PowerShell, hello CLI d’Azure, hello API REST de Azure, ou hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="67175-297">**Azure tools**: Retrieve information from hello activity log through Azure PowerShell, hello Azure CLI, hello Azure REST API, or hello Azure portal.</span></span> <span data-ttu-id="67175-298">Des instructions détaillées pour chaque méthode sont détaillées dans hello [opérations de l’activité avec le Gestionnaire de ressources](../azure-resource-manager/resource-group-audit.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="67175-298">Step-by-step instructions for each method are detailed in hello [Activity operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.</span></span>
* <span data-ttu-id="67175-299">**Power BI** : si vous n’avez pas encore de compte [Power BI](https://powerbi.microsoft.com/pricing) , vous pouvez l’essayer gratuitement.</span><span class="sxs-lookup"><span data-stu-id="67175-299">**Power BI**: If you don't already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free.</span></span> <span data-ttu-id="67175-300">À l’aide de hello [journaux d’activité Azure pack de contenu pour Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), vous pouvez analyser vos données avec des tableaux de bord préconfigurés que vous pouvez utiliser ou personnaliser.</span><span class="sxs-lookup"><span data-stu-id="67175-300">By using hello [Azure Activity Logs content pack for Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), you can analyze your data with preconfigured dashboards that you can use as is or customize.</span></span>

### <a name="view-and-analyze-hello-access-performance-and-firewall-logs"></a><span data-ttu-id="67175-301">Afficher et analyser les accès hello, les performances et les journaux de pare-feu</span><span class="sxs-lookup"><span data-stu-id="67175-301">View and analyze hello access, performance, and firewall logs</span></span>

<span data-ttu-id="67175-302">Azure [Analytique de journal](../log-analytics/log-analytics-azure-networking-analytics.md) peut collecter des fichiers de journal des événements et compteurs de hello à partir de votre compte de stockage d’objets Blob.</span><span class="sxs-lookup"><span data-stu-id="67175-302">Azure [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md) can collect hello counter and event log files from your Blob storage account.</span></span> <span data-ttu-id="67175-303">Il inclut des visualisations et recherche de puissantes fonctionnalités tooanalyze vos journaux.</span><span class="sxs-lookup"><span data-stu-id="67175-303">It includes visualizations and powerful search capabilities tooanalyze your logs.</span></span>

<span data-ttu-id="67175-304">Vous pouvez également connecter le compte de stockage tooyour et récupérer les entrées de journal hello JSON pour les journaux de performances et d’accès.</span><span class="sxs-lookup"><span data-stu-id="67175-304">You can also connect tooyour storage account and retrieve hello JSON log entries for access and performance logs.</span></span> <span data-ttu-id="67175-305">Après avoir téléchargé les fichiers au format JSON hello, vous pouvez convertir les tooCSV et les afficher dans Excel, Power BI ou tout autre outil de visualisation des données.</span><span class="sxs-lookup"><span data-stu-id="67175-305">After you download hello JSON files, you can convert them tooCSV and view them in Excel, Power BI, or any other data-visualization tool.</span></span>

> [!TIP]
> <span data-ttu-id="67175-306">Si vous êtes familiarisé avec Visual Studio et les concepts de base de la modification des valeurs de constantes et variables dans c#, vous pouvez utiliser hello [ouvrir une session outils de convertisseur](https://github.com/Azure-Samples/networking-dotnet-log-converter) disponible à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="67175-306">If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use hello [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.</span></span>
> 
> 

## <a name="metrics"></a><span data-ttu-id="67175-307">Mesures</span><span class="sxs-lookup"><span data-stu-id="67175-307">Metrics</span></span>

<span data-ttu-id="67175-308">Métriques sont une fonctionnalité de certaines ressources Azure où vous pouvez afficher les compteurs de performance dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="67175-308">Metrics are a feature for certain Azure resources where you can view performance counters in hello portal.</span></span> <span data-ttu-id="67175-309">Pour Application Gateway, une métrique est désormais disponible.</span><span class="sxs-lookup"><span data-stu-id="67175-309">For Application Gateway, one metric is available now.</span></span> <span data-ttu-id="67175-310">Cette mesure est le débit, et vous pouvez le voir dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="67175-310">This metric is throughput, and you can see it in hello portal.</span></span> <span data-ttu-id="67175-311">Parcourir la passerelle d’application tooan et cliquez sur **métriques**.</span><span class="sxs-lookup"><span data-stu-id="67175-311">Browse tooan application gateway and click **Metrics**.</span></span> <span data-ttu-id="67175-312">les valeurs hello tooview, sélectionnez débit Bonjour **métriques disponibles** section.</span><span class="sxs-lookup"><span data-stu-id="67175-312">tooview hello values, select throughput in hello **Available metrics** section.</span></span> <span data-ttu-id="67175-313">Dans hello suivant l’image, vous pouvez voir un exemple avec des filtres hello que vous pouvez utiliser les données de salutation toodisplay dans les plages de temps différent.</span><span class="sxs-lookup"><span data-stu-id="67175-313">In hello following image, you can see an example with hello filters that you can use toodisplay hello data in different time ranges.</span></span>

![Affichage de métriques avec des filtres][5]

<span data-ttu-id="67175-315">toosee liste actuelle des métriques, consultez [prise en charge des métriques avec Azure analyse](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="67175-315">toosee a current list of metrics, see [Supported metrics with Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span></span>

### <a name="alert-rules"></a><span data-ttu-id="67175-316">Règles d'alerte</span><span class="sxs-lookup"><span data-stu-id="67175-316">Alert rules</span></span>

<span data-ttu-id="67175-317">Vous pouvez démarrer des règles d’alerte en fonction des métriques d’une ressource.</span><span class="sxs-lookup"><span data-stu-id="67175-317">You can start alert rules based on metrics for a resource.</span></span> <span data-ttu-id="67175-318">Par exemple, une alerte peut appeler un webhook ou un administrateur de messagerie, si le débit de passerelle d’application hello hello est au-dessus, au-dessous ou à un seuil pour une période spécifiée.</span><span class="sxs-lookup"><span data-stu-id="67175-318">For example, an alert can call a webhook or email an administrator if hello throughput of hello application gateway is above, below, or at a threshold for a specified period.</span></span>

<span data-ttu-id="67175-319">Bonjour à l’exemple suivant vous guide tout au long de la création d’une règle d’alerte qui envoie un administrateur de la messagerie tooan après un seuil, les violations de débit :</span><span class="sxs-lookup"><span data-stu-id="67175-319">hello following example walks you through creating an alert rule that sends an email tooan administrator after throughput breaches a threshold:</span></span>

1. <span data-ttu-id="67175-320">Cliquez sur **ajouter une alerte métrique** tooopen hello **ajouter une règle** panneau.</span><span class="sxs-lookup"><span data-stu-id="67175-320">Click **Add metric alert** tooopen hello **Add rule** blade.</span></span> <span data-ttu-id="67175-321">Vous pouvez également atteindre ce panneau à partir du Panneau de métriques hello.</span><span class="sxs-lookup"><span data-stu-id="67175-321">You can also reach this blade from hello metrics blade.</span></span>

   ![Bouton Ajouter une alerte Métrique][6]

2. <span data-ttu-id="67175-323">Sur hello **ajouter une règle** panneau, renseignez le nom hello, condition et informer des sections, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="67175-323">On hello **Add rule** blade, fill out hello name, condition, and notify sections, and click **OK**.</span></span>

   * <span data-ttu-id="67175-324">Bonjour **Condition** sélecteur, sélectionnez une des valeurs de hello quatre : **supérieur**, **égal ou supérieur**, **moins**, ou  **Inférieur ou égal à**.</span><span class="sxs-lookup"><span data-stu-id="67175-324">In hello **Condition** selector, select one of hello four values: **Greater than**, **Greater than or equal**, **Less than**, or **Less than or equal to**.</span></span>

   * <span data-ttu-id="67175-325">Bonjour **période** sélecteur, sélectionnez une période de 5 minutes too6 heures.</span><span class="sxs-lookup"><span data-stu-id="67175-325">In hello **Period** selector, select a period from 5 minutes too6 hours.</span></span>

   * <span data-ttu-id="67175-326">Si vous sélectionnez **propriétaires, collaborateurs et les lecteurs de messagerie**, messagerie de hello peut être dynamique basées sur les utilisateurs de hello qui ont accès toothat ressource.</span><span class="sxs-lookup"><span data-stu-id="67175-326">If you select **Email owners, contributors, and readers**, hello email can be dynamic based on hello users who have access toothat resource.</span></span> <span data-ttu-id="67175-327">Sinon, vous pouvez fournir une liste séparée par des virgules des utilisateurs dans hello **administrateur supplémentaire email(s)** boîte.</span><span class="sxs-lookup"><span data-stu-id="67175-327">Otherwise, you can provide a comma-separated list of users in hello **Additional administrator email(s)** box.</span></span>

   ![Panneau Ajouter une règle][7]

<span data-ttu-id="67175-329">Si le seuil de hello est dépassé, un message électronique qui est similaire toohello un Bonjour suivant image arrive :</span><span class="sxs-lookup"><span data-stu-id="67175-329">If hello threshold is breached, an email that's similar toohello one in hello following image arrives:</span></span>

![E-mail en cas de dépassement de seuil][8]

<span data-ttu-id="67175-331">Une liste d’alertes apparaît une fois que vous avez créé une alerte Métrique.</span><span class="sxs-lookup"><span data-stu-id="67175-331">A list of alerts appears after you create a metric alert.</span></span> <span data-ttu-id="67175-332">Il fournit une vue d’ensemble de toutes les règles d’alerte hello.</span><span class="sxs-lookup"><span data-stu-id="67175-332">It provides an overview of all hello alert rules.</span></span>

![Liste d’alertes et de règles][9]

<span data-ttu-id="67175-334">toolearn en savoir plus sur les notifications d’alerte, consultez [recevoir des notifications d’alerte](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="67175-334">toolearn more about alert notifications, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="67175-335">toounderstand en savoir plus sur le webhooks et comment vous pouvez les utiliser avec les alertes, visitez [configurer un webhook sur une alerte de métrique Azure](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="67175-335">toounderstand more about webhooks and how you can use them with alerts, visit [Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="67175-336">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="67175-336">Next steps</span></span>

* <span data-ttu-id="67175-337">Visualisation du compteur et des journaux des événements à l’aide de [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="67175-337">Visualize counter and event logs by using [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md).</span></span>
* <span data-ttu-id="67175-338">Billet de blog sur la [visualisation de votre journal d’activité Azure avec Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx).</span><span class="sxs-lookup"><span data-stu-id="67175-338">[Visualize your Azure activity log with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog post.</span></span>
* <span data-ttu-id="67175-339">Billet de blog sur [l’affichage et l’analyse des journaux d’activité Azure dans Power BI](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/).</span><span class="sxs-lookup"><span data-stu-id="67175-339">[View and analyze Azure activity logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.</span></span>

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
