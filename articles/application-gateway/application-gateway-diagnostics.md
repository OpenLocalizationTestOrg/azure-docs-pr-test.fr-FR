---
title: "Surveiller les journaux d’accès, les journaux des performances, l’intégrité du serveur principal, ainsi que les métriques d’Application Gateway | Microsoft Docs"
description: "Découvrez comment activer et gérer les journaux d’accès et les journaux des performances pour Application Gateway"
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
ms.openlocfilehash: 12c252340b82aba5ee69b12db83353750782e7c5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="back-end-health-diagnostic-logs-and-metrics-for-application-gateway"></a><span data-ttu-id="e1c49-103">Intégrité du serveur principal, journaux de diagnostic et métriques pour la passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="e1c49-103">Back-end health, diagnostic logs, and metrics for Application Gateway</span></span>

<span data-ttu-id="e1c49-104">À l’aide de la passerelle Azure Application Gateway, vous pouvez surveiller les ressources des manières suivantes :</span><span class="sxs-lookup"><span data-stu-id="e1c49-104">By using Azure Application Gateway, you can monitor resources in the following ways:</span></span>

* <span data-ttu-id="e1c49-105">[Intégrité du serveur principal](#back-end-health) : Application Gateway permet de surveiller l’intégrité des serveurs dans les pools principaux au moyen du portail Azure et de Powershell.</span><span class="sxs-lookup"><span data-stu-id="e1c49-105">[Back-end health](#back-end-health): Application Gateway provides the capability to monitor the health of the servers in the back-end pools through the Azure portal and through PowerShell.</span></span> <span data-ttu-id="e1c49-106">Vous pouvez également accéder à l’intégrité des pools principaux via les journaux de diagnostic des performances.</span><span class="sxs-lookup"><span data-stu-id="e1c49-106">You can also find the health of the back-end pools through the performance diagnostic logs.</span></span>

* <span data-ttu-id="e1c49-107">[Journaux](#diagnostic-logs) : les journaux permettent d’enregistrer ou d’utiliser les performances, les accès et les autres données à partir d’une ressource à des fins de surveillance.</span><span class="sxs-lookup"><span data-stu-id="e1c49-107">[Logs](#diagnostic-logs): Logs allow for performance, access, and other data to be saved or consumed from a resource for monitoring purposes.</span></span>

* <span data-ttu-id="e1c49-108">[Mesures](#metrics) : la passerelle Application Gateway possède actuellement une métrique.</span><span class="sxs-lookup"><span data-stu-id="e1c49-108">[Metrics](#metrics): Application Gateway currently has one metric.</span></span> <span data-ttu-id="e1c49-109">Cette métrique mesure le débit de la passerelle Application Gateway en octets par seconde.</span><span class="sxs-lookup"><span data-stu-id="e1c49-109">This metric measures the throughput of the application gateway in bytes per second.</span></span>

## <a name="back-end-health"></a><span data-ttu-id="e1c49-110">Intégrité du serveur principal</span><span class="sxs-lookup"><span data-stu-id="e1c49-110">Back-end health</span></span>

<span data-ttu-id="e1c49-111">La passerelle Application Gateway permet de surveiller l’intégrité des membres individuels des pools principaux au moyen du portail, de PowerShell et de l’interface de ligne de commande (CLI).</span><span class="sxs-lookup"><span data-stu-id="e1c49-111">Application Gateway provides the capability to monitor the health of individual members of the back-end pools through the portal, PowerShell, and the command-line interface (CLI).</span></span> <span data-ttu-id="e1c49-112">Une synthèse de l’intégrité agrégée des pools principaux est également accessible via les journaux de diagnostic des performances.</span><span class="sxs-lookup"><span data-stu-id="e1c49-112">You can also find an aggregated health summary of back-end pools through the performance diagnostic logs.</span></span> 

<span data-ttu-id="e1c49-113">Le rapport d’intégrité du serveur principal reflète les résultats de la sonde d’intégrité de la passerelle Application Gateway sur les instances de serveur principal.</span><span class="sxs-lookup"><span data-stu-id="e1c49-113">The back-end health report reflects the output of the Application Gateway health probe to the back-end instances.</span></span> <span data-ttu-id="e1c49-114">Si la détection réussit et que le trafic peut être orienté vers le serveur principal, ce dernier est considéré comme intègre.</span><span class="sxs-lookup"><span data-stu-id="e1c49-114">When probing is successful and the back end can receive traffic, it's considered healthy.</span></span> <span data-ttu-id="e1c49-115">Sinon, il est considéré comme défaillant.</span><span class="sxs-lookup"><span data-stu-id="e1c49-115">Otherwise, it's considered unhealthy.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e1c49-116">Si le sous-réseau Application Gateway comporte un groupe de sécurité réseau (NSG), ouvrez les plages de ports 65503-65534 sur ce sous-réseau pour permettre l’arrivée du trafic entrant.</span><span class="sxs-lookup"><span data-stu-id="e1c49-116">If there is a network security group (NSG) on an Application Gateway subnet, open port ranges 65503-65534 on the Application Gateway subnet for inbound traffic.</span></span> <span data-ttu-id="e1c49-117">Ces ports sont requis pour permettre à l’API relative à l’intégrité du serveur principal de fonctionner correctement.</span><span class="sxs-lookup"><span data-stu-id="e1c49-117">These ports are required for the back-end health API to work.</span></span>


### <a name="view-back-end-health-through-the-portal"></a><span data-ttu-id="e1c49-118">Affichage de l’intégrité du serveur principal via le portail</span><span class="sxs-lookup"><span data-stu-id="e1c49-118">View back-end health through the portal</span></span>

<span data-ttu-id="e1c49-119">Dans le portail, l’intégrité du serveur principal est indiquée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="e1c49-119">In the portal, back-end health is provided automatically.</span></span> <span data-ttu-id="e1c49-120">Dans une passerelle Application Gateway existante, sélectionnez **Analyse** > **Intégrité du serveur principal**.</span><span class="sxs-lookup"><span data-stu-id="e1c49-120">In an existing application gateway, select **Monitoring** > **Backend health**.</span></span> 

<span data-ttu-id="e1c49-121">Chaque membre du pool principal est répertorié sur cette page (qu’il s’agisse d’une carte réseau, d’un IP ou d’un nom de domaine complet).</span><span class="sxs-lookup"><span data-stu-id="e1c49-121">Each member in the back-end pool is listed on this page (whether it's a NIC, IP, or FQDN).</span></span> <span data-ttu-id="e1c49-122">Le nom du pool principal, le port, le nom et l’état d’intégrité des paramètres HTTP principaux sont affichés.</span><span class="sxs-lookup"><span data-stu-id="e1c49-122">Back-end pool name, port, back-end HTTP settings name, and health status are shown.</span></span> <span data-ttu-id="e1c49-123">Les valeurs valides de l’état d’intégrité sont **Healthy** (Intègre), **Unhealthy** (Défaillant) et **Unknown** (Inconnu).</span><span class="sxs-lookup"><span data-stu-id="e1c49-123">Valid values for health status are **Healthy**, **Unhealthy**, and **Unknown**.</span></span>

> [!NOTE]
> <span data-ttu-id="e1c49-124">Si l’état d’intégrité du serveur principal affiché est **Unknown** (Inconnu), assurez-vous que l’accès au serveur principal n’est pas bloqué par une règle de groupe de sécurité réseau, un itinéraire défini par l’utilisateur ou un DNS personnalisé dans le réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="e1c49-124">If you see a back-end health status of **Unknown**, ensure that access to the back end is not blocked by an NSG rule, a user-defined route (UDR), or a custom DNS in the virtual network.</span></span>

![Intégrité du serveur principal][10]

### <a name="view-back-end-health-through-powershell"></a><span data-ttu-id="e1c49-126">Affichage de l’intégrité du serveur principal via PowerShell</span><span class="sxs-lookup"><span data-stu-id="e1c49-126">View back-end health through PowerShell</span></span>

<span data-ttu-id="e1c49-127">Le code PowerShell suivant montre comment afficher l’intégrité du serveur principal en utilisant l’applet de commande `Get-AzureRmApplicationGatewayBackendHealth` :</span><span class="sxs-lookup"><span data-stu-id="e1c49-127">The following PowerShell code shows how to view back-end health by using the `Get-AzureRmApplicationGatewayBackendHealth` cmdlet:</span></span>

```powershell
Get-AzureRmApplicationGatewayBackendHealth -Name ApplicationGateway1 -ResourceGroupName Contoso
```

### <a name="view-back-end-health-through-azure-cli-20"></a><span data-ttu-id="e1c49-128">Affichage de l’intégrité du serveur principal via Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e1c49-128">View back-end health through Azure CLI 2.0</span></span>

```azurecli
az network application-gateway show-backend-health --resource-group AdatumAppGatewayRG --name AdatumAppGateway
```

### <a name="results"></a><span data-ttu-id="e1c49-129">Résultats</span><span class="sxs-lookup"><span data-stu-id="e1c49-129">Results</span></span>

<span data-ttu-id="e1c49-130">L’extrait de code suivant montre un exemple de la réponse :</span><span class="sxs-lookup"><span data-stu-id="e1c49-130">The following snippet shows an example of the response:</span></span>

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

## <span data-ttu-id="e1c49-131"><a name="diagnostic-logging"></a>Journaux de diagnostic</span><span class="sxs-lookup"><span data-stu-id="e1c49-131"><a name="diagnostic-logging"></a>Diagnostic logs</span></span>

<span data-ttu-id="e1c49-132">Vous pouvez utiliser différents types de journaux dans Azure pour gérer les passerelles Application Gateway et résoudre les problèmes associés.</span><span class="sxs-lookup"><span data-stu-id="e1c49-132">You can use different types of logs in Azure to manage and troubleshoot application gateways.</span></span> <span data-ttu-id="e1c49-133">Vous pouvez accéder à certains de ces journaux via le portail.</span><span class="sxs-lookup"><span data-stu-id="e1c49-133">You can access some of these logs through the portal.</span></span> <span data-ttu-id="e1c49-134">Tous les journaux peuvent être extraits à partir d’un stockage Blob Azure et affichés dans différents outils, comme [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md), Excel et PowerBI.</span><span class="sxs-lookup"><span data-stu-id="e1c49-134">All logs can be extracted from Azure Blob storage and viewed in different tools, such as [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md), Excel, and Power BI.</span></span> <span data-ttu-id="e1c49-135">Pour en savoir plus sur les différents types de journaux, consultez la liste suivante :</span><span class="sxs-lookup"><span data-stu-id="e1c49-135">You can learn more about the different types of logs from the following list:</span></span>

* <span data-ttu-id="e1c49-136">**Journal d’activité** : vous pouvez utiliser le [Journal d’activité Azure](../monitoring-and-diagnostics/insights-debugging-with-events.md) (anciennement journaux des opérations et journaux d’audit) pour afficher toutes les opérations soumises à votre abonnement Azure, ainsi que leur état.</span><span class="sxs-lookup"><span data-stu-id="e1c49-136">**Activity log**: You can use [Azure activity logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) (formerly known as operational logs and audit logs) to view all operations that are submitted to your Azure subscription, and their status.</span></span> <span data-ttu-id="e1c49-137">Les entrées du journal d’activité sont recueillies par défaut et vous pouvez les afficher dans le Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e1c49-137">Activity log entries are collected by default, and you can view them in the Azure portal.</span></span>
* <span data-ttu-id="e1c49-138">**Journaux d’accès** : vous pouvez utiliser ce journal pour afficher les modèles d’accès Application Gateway et analyser des informations importantes, notamment l’adresse IP de l’appelant, l’URL demandée, la latence de réponse, le code de retour, les octets d’entrée et de sortie. Un journal d’accès est collecté toutes les 300 secondes.</span><span class="sxs-lookup"><span data-stu-id="e1c49-138">**Access log**: You can use this log to view Application Gateway access patterns and analyze important information, including the caller's IP, requested URL, response latency, return code, and bytes in and out. An access log is collected every 300 seconds.</span></span> <span data-ttu-id="e1c49-139">Ce journal contient un enregistrement par instance Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="e1c49-139">This log contains one record per instance of Application Gateway.</span></span> <span data-ttu-id="e1c49-140">L’instance de la passerelle Application Gateway peut être identifiée par la propriété instanceId.</span><span class="sxs-lookup"><span data-stu-id="e1c49-140">The Application Gateway instance can be identified by the instanceId property.</span></span>
* <span data-ttu-id="e1c49-141">**Journaux de performances** : vous pouvez utiliser ce journal pour afficher les performances des instances de la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="e1c49-141">**Performance log**: You can use this log to view how Application Gateway instances are performing.</span></span> <span data-ttu-id="e1c49-142">Ce journal capture des informations sur les performances de chaque instance, notamment le nombre total de requêtes traitées, le débit en octets, le nombre total de requêtes présentées, le nombre de requêtes ayant échoué, le nombre d’instances du serveur principal intègres et défectueuses.</span><span class="sxs-lookup"><span data-stu-id="e1c49-142">This log captures performance information for each instance, including total requests served, throughput in bytes, total requests served, failed request count, and healthy and unhealthy back-end instance count.</span></span> <span data-ttu-id="e1c49-143">Le journal des performances est collecté toutes les 60 secondes.</span><span class="sxs-lookup"><span data-stu-id="e1c49-143">A performance log is collected every 60 seconds.</span></span>
* <span data-ttu-id="e1c49-144">**Journaux du pare-feu** : vous pouvez utiliser ce journal pour afficher les requêtes consignées via le mode de détection ou de prévention d’une passerelle Application Gateway configuré avec un pare-feu d’applications web.</span><span class="sxs-lookup"><span data-stu-id="e1c49-144">**Firewall log**: You can use this log to view the requests that are logged through either detection or prevention mode of an application gateway that is configured with the web application firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="e1c49-145">Les journaux ne sont disponibles que pour les ressources déployées dans le modèle de déploiement Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e1c49-145">Logs are available only for resources deployed in the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="e1c49-146">Vous ne pouvez pas les utiliser pour les ressources utilisant le modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="e1c49-146">You cannot use logs for resources in the classic deployment model.</span></span> <span data-ttu-id="e1c49-147">Pour mieux comprendre ces deux modèles, consultez l’article [Présentation du déploiement de Resource Manager et du déploiement classique](../azure-resource-manager/resource-manager-deployment-model.md) .</span><span class="sxs-lookup"><span data-stu-id="e1c49-147">For a better understanding of the two models, see the [Understanding Resource Manager deployment and classic deployment](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

<span data-ttu-id="e1c49-148">Pour stocker vos journaux, vous disposez de trois options :</span><span class="sxs-lookup"><span data-stu-id="e1c49-148">You have three options for storing your logs:</span></span>

* <span data-ttu-id="e1c49-149">**Compte de stockage** : les comptes de stockage conviennent parfaitement aux journaux lorsqu’ils sont stockés pour une durée plus longue et consultés lorsque nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e1c49-149">**Storage account**: Storage accounts are best used for logs when logs are stored for a longer duration and reviewed when needed.</span></span>
* <span data-ttu-id="e1c49-150">**Concentrateurs d’événements** : les concentrateurs d’événements constituent une excellente solution pour l’intégration avec d’autres outils SEIM (Security Information and Event Management) afin de recevoir des alertes sur vos ressources.</span><span class="sxs-lookup"><span data-stu-id="e1c49-150">**Event hubs**: Event hubs are a great option for integrating with other security information and event management (SEIM) tools to get alerts on your resources.</span></span>
* <span data-ttu-id="e1c49-151">**Log Analytics** : Log Analytics convient parfaitement pour la surveillance en temps réel générale de votre application ou la recherche de tendances.</span><span class="sxs-lookup"><span data-stu-id="e1c49-151">**Log Analytics**: Log Analytics is best used for general real-time monitoring of your application or looking at trends.</span></span>

### <a name="enable-logging-through-powershell"></a><span data-ttu-id="e1c49-152">Activation de la journalisation avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="e1c49-152">Enable logging through PowerShell</span></span>

<span data-ttu-id="e1c49-153">La journalisation d’activité est automatiquement activée pour chaque ressource Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e1c49-153">Activity logging is automatically enabled for every Resource Manager resource.</span></span> <span data-ttu-id="e1c49-154">Vous devez activer la journalisation de l’accès et des performances pour commencer à collecter les données disponibles dans ces journaux.</span><span class="sxs-lookup"><span data-stu-id="e1c49-154">You must enable access and performance logging to start collecting the data available through those logs.</span></span> <span data-ttu-id="e1c49-155">Pour activer la journalisation, utilisez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="e1c49-155">To enable logging, use the following steps:</span></span>

1. <span data-ttu-id="e1c49-156">Notez l’ID de ressource de votre compte de stockage, où les données de journalisation sont stockées.</span><span class="sxs-lookup"><span data-stu-id="e1c49-156">Note your storage account's resource ID, where the log data is stored.</span></span> <span data-ttu-id="e1c49-157">Cette valeur a le format suivant : /abonnements/\<subscriptionId\>/resourceGroups/\<nom du groupe de ressources\>/providers/Microsoft.Storage/storageAccounts/\<nom du compte de stockage\>.</span><span class="sxs-lookup"><span data-stu-id="e1c49-157">This value is of the form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Storage/storageAccounts/\<storage account name\>.</span></span> <span data-ttu-id="e1c49-158">Vous pouvez utiliser n’importe quel compte de stockage dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="e1c49-158">You can use any storage account in your subscription.</span></span> <span data-ttu-id="e1c49-159">Vous pouvez utiliser le portail Azure pour rechercher ces informations.</span><span class="sxs-lookup"><span data-stu-id="e1c49-159">You can use the Azure portal to find this information.</span></span>

    ![Portail : ID de ressource du compte de stockage](./media/application-gateway-diagnostics/diagnostics1.png)

2. <span data-ttu-id="e1c49-161">Notez l’ID de ressource de votre passerelle Application Gateway pour laquelle la journalisation est activée.</span><span class="sxs-lookup"><span data-stu-id="e1c49-161">Note your application gateway's resource ID for which logging is enabled.</span></span> <span data-ttu-id="e1c49-162">Cette valeur a le format suivant : /abonnements/\<subscriptionId\>/resourceGroups/\<nom du groupe de ressources\>/providers/Microsoft.Network/applicationGateways/\<nom de la passerelle Application Gateway\>.</span><span class="sxs-lookup"><span data-stu-id="e1c49-162">This value is of the form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Network/applicationGateways/\<application gateway name\>.</span></span> <span data-ttu-id="e1c49-163">Vous pouvez utiliser le portail pour rechercher ces informations.</span><span class="sxs-lookup"><span data-stu-id="e1c49-163">You can use the portal to find this information.</span></span>

    ![Portail : ID de ressource de la passerelle Application Gateway](./media/application-gateway-diagnostics/diagnostics2.png)

3. <span data-ttu-id="e1c49-165">Activez la journalisation des diagnostics à l’aide de l’applet de commande PowerShell suivante :</span><span class="sxs-lookup"><span data-stu-id="e1c49-165">Enable diagnostic logging by using the following PowerShell cmdlet:</span></span>

    ```powershell
    Set-AzureRmDiagnosticSetting  -ResourceId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name> -StorageAccountId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Storage/storageAccounts/<storage account name> -Enabled $true     
    ```
    
> [!TIP] 
><span data-ttu-id="e1c49-166">Les journaux d’activité ne nécessitent pas de compte de stockage distinct.</span><span class="sxs-lookup"><span data-stu-id="e1c49-166">Activity logs do not require a separate storage account.</span></span> <span data-ttu-id="e1c49-167">L’utilisation du stockage pour la journalisation de l’accès et des performances occasionne des frais de service.</span><span class="sxs-lookup"><span data-stu-id="e1c49-167">The use of storage for access and performance logging incurs service charges.</span></span>

### <a name="enable-logging-through-the-azure-portal"></a><span data-ttu-id="e1c49-168">Activation de la journalisation avec le portail Azure</span><span class="sxs-lookup"><span data-stu-id="e1c49-168">Enable logging through the Azure portal</span></span>

1. <span data-ttu-id="e1c49-169">Dans le portail Azure, recherchez votre ressource, puis cliquez sur **Journaux de diagnostic**.</span><span class="sxs-lookup"><span data-stu-id="e1c49-169">In the Azure portal, find your resource and click **Diagnostic logs**.</span></span>

   <span data-ttu-id="e1c49-170">Pour Application Gateway, trois journaux d’audit sont disponibles :</span><span class="sxs-lookup"><span data-stu-id="e1c49-170">For Application Gateway, three logs are available:</span></span>

   * <span data-ttu-id="e1c49-171">Journal d’accès</span><span class="sxs-lookup"><span data-stu-id="e1c49-171">Access log</span></span>
   * <span data-ttu-id="e1c49-172">Journal des performances</span><span class="sxs-lookup"><span data-stu-id="e1c49-172">Performance log</span></span>
   * <span data-ttu-id="e1c49-173">Journal du pare-feu</span><span class="sxs-lookup"><span data-stu-id="e1c49-173">Firewall log</span></span>

2. <span data-ttu-id="e1c49-174">Cliquez sur **Activer les diagnostics** pour démarrer la collecte de données.</span><span class="sxs-lookup"><span data-stu-id="e1c49-174">To start collecting data, click **Turn on diagnostics**.</span></span>

   ![Activation des diagnostics][1]

3. <span data-ttu-id="e1c49-176">Le panneau **Paramètres de diagnostic** contient les paramètres des journaux de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="e1c49-176">The **Diagnostics settings** blade provides the settings for the diagnostic logs.</span></span> <span data-ttu-id="e1c49-177">Dans cet exemple, Log Analytics stocke les journaux.</span><span class="sxs-lookup"><span data-stu-id="e1c49-177">In this example, Log Analytics stores the logs.</span></span> <span data-ttu-id="e1c49-178">Cliquez sur **Configurer** sous **Log Analytics** pour configurer votre espace de travail.</span><span class="sxs-lookup"><span data-stu-id="e1c49-178">Click **Configure** under **Log Analytics** to configure your workspace.</span></span> <span data-ttu-id="e1c49-179">Vous pouvez également utiliser des concentrateurs d’événements et un compte de stockage pour enregistrer les journaux de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="e1c49-179">You can also use event hubs and a storage account to save the diagnostic logs.</span></span>

   ![Démarrage du processus de configuration][2]

4. <span data-ttu-id="e1c49-181">Sélectionnez ou créez un espace de travail OMS (Operations Management Suite) existant.</span><span class="sxs-lookup"><span data-stu-id="e1c49-181">Choose an existing Operations Management Suite (OMS) workspace or create a new one.</span></span> <span data-ttu-id="e1c49-182">Cet exemple utilise un espace de travail existant.</span><span class="sxs-lookup"><span data-stu-id="e1c49-182">This example uses an existing one.</span></span>

   ![Options des espaces de travail OMS][3]

5. <span data-ttu-id="e1c49-184">Confirmez les paramètres et cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="e1c49-184">Confirm the settings and click **Save**.</span></span>

   ![Panneau des paramètres de diagnostic avec des sélections][4]

### <a name="activity-log"></a><span data-ttu-id="e1c49-186">Journal d’activité</span><span class="sxs-lookup"><span data-stu-id="e1c49-186">Activity log</span></span>

<span data-ttu-id="e1c49-187">Par défaut, Azure génère le journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="e1c49-187">Azure generates the activity log by default.</span></span> <span data-ttu-id="e1c49-188">Les journaux sont conservés pendant 90 jours dans la banque de journaux d’événements d’Azure.</span><span class="sxs-lookup"><span data-stu-id="e1c49-188">The logs are preserved for 90 days in the Azure event logs store.</span></span> <span data-ttu-id="e1c49-189">Pour en savoir plus sur ces journaux, lisez l’article [Affichage des événements et du journal d’activité](../monitoring-and-diagnostics/insights-debugging-with-events.md).</span><span class="sxs-lookup"><span data-stu-id="e1c49-189">Learn more about these logs by reading the [View events and activity log](../monitoring-and-diagnostics/insights-debugging-with-events.md) article.</span></span>

### <a name="access-log"></a><span data-ttu-id="e1c49-190">Journal d’accès</span><span class="sxs-lookup"><span data-stu-id="e1c49-190">Access log</span></span>

<span data-ttu-id="e1c49-191">Le journal d’accès n’est généré que si vous l’avez activé sur chaque instance Application Gateway, comme détaillé dans les étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="e1c49-191">The access log is generated only if you've enabled it on each Application Gateway instance, as detailed in the preceding steps.</span></span> <span data-ttu-id="e1c49-192">Les données sont stockées dans le compte de stockage spécifié lors de l’activation de la journalisation.</span><span class="sxs-lookup"><span data-stu-id="e1c49-192">The data is stored in the storage account that you specified when you enabled the logging.</span></span> <span data-ttu-id="e1c49-193">Chaque accès à la passerelle Application Gateway est journalisé au format JSON, comme indiqué dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="e1c49-193">Each access of Application Gateway is logged in JSON format, as shown in the following example:</span></span>


|<span data-ttu-id="e1c49-194">Valeur</span><span class="sxs-lookup"><span data-stu-id="e1c49-194">Value</span></span>  |<span data-ttu-id="e1c49-195">Description</span><span class="sxs-lookup"><span data-stu-id="e1c49-195">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="e1c49-196">instanceId</span><span class="sxs-lookup"><span data-stu-id="e1c49-196">instanceId</span></span>     | <span data-ttu-id="e1c49-197">Instance Application Gateway ayant traité la requête.</span><span class="sxs-lookup"><span data-stu-id="e1c49-197">Application Gateway instance that served the request.</span></span>        |
|<span data-ttu-id="e1c49-198">clientIP</span><span class="sxs-lookup"><span data-stu-id="e1c49-198">clientIP</span></span>     | <span data-ttu-id="e1c49-199">Adresse IP d’origine de la requête.</span><span class="sxs-lookup"><span data-stu-id="e1c49-199">Originating IP for the request.</span></span>        |
|<span data-ttu-id="e1c49-200">clientPort</span><span class="sxs-lookup"><span data-stu-id="e1c49-200">clientPort</span></span>     | <span data-ttu-id="e1c49-201">Port d’origine de la requête.</span><span class="sxs-lookup"><span data-stu-id="e1c49-201">Originating port for the request.</span></span>       |
|<span data-ttu-id="e1c49-202">httpMethod</span><span class="sxs-lookup"><span data-stu-id="e1c49-202">httpMethod</span></span>     | <span data-ttu-id="e1c49-203">Méthode HTTP utilisée par la requête.</span><span class="sxs-lookup"><span data-stu-id="e1c49-203">HTTP method used by the request.</span></span>       |
|<span data-ttu-id="e1c49-204">requestUri</span><span class="sxs-lookup"><span data-stu-id="e1c49-204">requestUri</span></span>     | <span data-ttu-id="e1c49-205">URI de la requête reçue.</span><span class="sxs-lookup"><span data-stu-id="e1c49-205">URI of the received request.</span></span>        |
|<span data-ttu-id="e1c49-206">RequestQuery</span><span class="sxs-lookup"><span data-stu-id="e1c49-206">RequestQuery</span></span>     | <span data-ttu-id="e1c49-207">**Acheminée par le serveur** : instance de pool principal à laquelle la requête a été envoyée.</span><span class="sxs-lookup"><span data-stu-id="e1c49-207">**Server-Routed**: Back-end pool instance that was sent the request.</span></span> </br> <span data-ttu-id="e1c49-208">**X-AzureApplicationGateway-journal-ID** : ID de corrélation utilisé pour la requête.</span><span class="sxs-lookup"><span data-stu-id="e1c49-208">**X-AzureApplicationGateway-LOG-ID**: Correlation ID used for the request.</span></span> <span data-ttu-id="e1c49-209">Peut être utilisée pour résoudre les problèmes de trafic sur les serveurs principaux.</span><span class="sxs-lookup"><span data-stu-id="e1c49-209">It can be used to troubleshoot traffic issues on the back-end servers.</span></span> </br><span data-ttu-id="e1c49-210">**ÉTAT DU SERVEUR** : code de réponse HTTP reçu par Application Gateway à partir du serveur principal.</span><span class="sxs-lookup"><span data-stu-id="e1c49-210">**SERVER-STATUS**: HTTP response code that Application Gateway received from the back end.</span></span>       |
|<span data-ttu-id="e1c49-211">UserAgent</span><span class="sxs-lookup"><span data-stu-id="e1c49-211">UserAgent</span></span>     | <span data-ttu-id="e1c49-212">Agent utilisateur de l’en-tête de requête HTTP.</span><span class="sxs-lookup"><span data-stu-id="e1c49-212">User agent from the HTTP request header.</span></span>        |
|<span data-ttu-id="e1c49-213">httpStatus</span><span class="sxs-lookup"><span data-stu-id="e1c49-213">httpStatus</span></span>     | <span data-ttu-id="e1c49-214">Code d’état HTTP renvoyé au client à partir de d’Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="e1c49-214">HTTP status code returned to the client from Application Gateway.</span></span>       |
|<span data-ttu-id="e1c49-215">httpVersion</span><span class="sxs-lookup"><span data-stu-id="e1c49-215">httpVersion</span></span>     | <span data-ttu-id="e1c49-216">Version HTTP de la requête.</span><span class="sxs-lookup"><span data-stu-id="e1c49-216">HTTP version of the request.</span></span>        |
|<span data-ttu-id="e1c49-217">receivedBytes</span><span class="sxs-lookup"><span data-stu-id="e1c49-217">receivedBytes</span></span>     | <span data-ttu-id="e1c49-218">Taille du paquet reçu, en octets.</span><span class="sxs-lookup"><span data-stu-id="e1c49-218">Size of packet received, in bytes.</span></span>        |
|<span data-ttu-id="e1c49-219">sentBytes</span><span class="sxs-lookup"><span data-stu-id="e1c49-219">sentBytes</span></span>| <span data-ttu-id="e1c49-220">Taille du paquet envoyé, en octets.</span><span class="sxs-lookup"><span data-stu-id="e1c49-220">Size of packet sent, in bytes.</span></span>|
|<span data-ttu-id="e1c49-221">timeTaken</span><span class="sxs-lookup"><span data-stu-id="e1c49-221">timeTaken</span></span>| <span data-ttu-id="e1c49-222">Durée (en millisecondes) nécessaire pour le traitement d’une requête et l’envoi de la réponse.</span><span class="sxs-lookup"><span data-stu-id="e1c49-222">Length of time (in milliseconds) that it takes for a request to be processed and its response to be sent.</span></span> <span data-ttu-id="e1c49-223">Elle est calculée en fonction de l’intervalle entre le moment où Application Gateway reçoit le premier octet d’une requête HTTP et le moment où l’opération d’envoi d’une réponse se termine.</span><span class="sxs-lookup"><span data-stu-id="e1c49-223">This is calculated as the interval from the time when Application Gateway receives the first byte of an HTTP request to the time when the response send operation finishes.</span></span> <span data-ttu-id="e1c49-224">Il est important de noter que le champ Time-Taken inclut généralement l’heure à laquelle la requête et les paquets de réponse circulent sur le réseau.</span><span class="sxs-lookup"><span data-stu-id="e1c49-224">It's important to note that the Time-Taken field usually includes the time that the request and response packets are traveling over the network.</span></span> |
|<span data-ttu-id="e1c49-225">sslEnabled</span><span class="sxs-lookup"><span data-stu-id="e1c49-225">sslEnabled</span></span>| <span data-ttu-id="e1c49-226">Détermine si la communication avec les pools principaux utilisait SSL.</span><span class="sxs-lookup"><span data-stu-id="e1c49-226">Whether communication to the back-end pools used SSL.</span></span> <span data-ttu-id="e1c49-227">Les valeurs valides sont On (Activé) et Off (Désactivé).</span><span class="sxs-lookup"><span data-stu-id="e1c49-227">Valid values are on and off.</span></span>|
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

### <a name="performance-log"></a><span data-ttu-id="e1c49-228">Journal des performances</span><span class="sxs-lookup"><span data-stu-id="e1c49-228">Performance log</span></span>

<span data-ttu-id="e1c49-229">Le journal des performances n’est généré que si vous l’avez activé sur chaque instance Application Gateway, comme détaillé dans les étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="e1c49-229">The performance log is generated only if you have enabled it on each Application Gateway instance, as detailed in the preceding steps.</span></span> <span data-ttu-id="e1c49-230">Les données sont stockées dans le compte de stockage spécifié lors de l’activation de la journalisation.</span><span class="sxs-lookup"><span data-stu-id="e1c49-230">The data is stored in the storage account that you specified when you enabled the logging.</span></span> <span data-ttu-id="e1c49-231">Les données du journal des performances sont générées par intervalles d’1 minute.</span><span class="sxs-lookup"><span data-stu-id="e1c49-231">The performance log data is generated in 1-minute intervals.</span></span> <span data-ttu-id="e1c49-232">Les données suivantes sont enregistrées :</span><span class="sxs-lookup"><span data-stu-id="e1c49-232">The following data is logged:</span></span>


|<span data-ttu-id="e1c49-233">Valeur</span><span class="sxs-lookup"><span data-stu-id="e1c49-233">Value</span></span>  |<span data-ttu-id="e1c49-234">Description</span><span class="sxs-lookup"><span data-stu-id="e1c49-234">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="e1c49-235">instanceId</span><span class="sxs-lookup"><span data-stu-id="e1c49-235">instanceId</span></span>     |  <span data-ttu-id="e1c49-236">Instance Application Gateway pour laquelle les données des performances sont générées.</span><span class="sxs-lookup"><span data-stu-id="e1c49-236">Application Gateway instance for which performance data is being generated.</span></span> <span data-ttu-id="e1c49-237">Pour une passerelle Application Gateway à plusieurs instances, il y a une ligne par instance.</span><span class="sxs-lookup"><span data-stu-id="e1c49-237">For a multiple-instance application gateway, there is one row per instance.</span></span>        |
|<span data-ttu-id="e1c49-238">healthyHostCount</span><span class="sxs-lookup"><span data-stu-id="e1c49-238">healthyHostCount</span></span>     | <span data-ttu-id="e1c49-239">Nombre d’hôtes intègres dans le pool principal.</span><span class="sxs-lookup"><span data-stu-id="e1c49-239">Number of healthy hosts in the back-end pool.</span></span>        |
|<span data-ttu-id="e1c49-240">unHealthyHostCount</span><span class="sxs-lookup"><span data-stu-id="e1c49-240">unHealthyHostCount</span></span>     | <span data-ttu-id="e1c49-241">Nombre d’hôtes défaillants dans le pool principal.</span><span class="sxs-lookup"><span data-stu-id="e1c49-241">Number of unhealthy hosts in the back-end pool.</span></span>        |
|<span data-ttu-id="e1c49-242">requestCount</span><span class="sxs-lookup"><span data-stu-id="e1c49-242">requestCount</span></span>     | <span data-ttu-id="e1c49-243">Nombre de requêtes traitées.</span><span class="sxs-lookup"><span data-stu-id="e1c49-243">Number of requests served.</span></span>        |
|<span data-ttu-id="e1c49-244">latency</span><span class="sxs-lookup"><span data-stu-id="e1c49-244">latency</span></span> | <span data-ttu-id="e1c49-245">Latence (en millisecondes) des requêtes à partir de l’instance vers le serveur principal qui traite les requêtes.</span><span class="sxs-lookup"><span data-stu-id="e1c49-245">Latency (in milliseconds) of requests from the instance to the back end that serves the requests.</span></span> |
|<span data-ttu-id="e1c49-246">failedRequestCount</span><span class="sxs-lookup"><span data-stu-id="e1c49-246">failedRequestCount</span></span>| <span data-ttu-id="e1c49-247">Nombre d’échecs de requêtes.</span><span class="sxs-lookup"><span data-stu-id="e1c49-247">Number of failed requests.</span></span>|
|<span data-ttu-id="e1c49-248">throughput</span><span class="sxs-lookup"><span data-stu-id="e1c49-248">throughput</span></span>| <span data-ttu-id="e1c49-249">Débit moyen depuis le dernier journal, mesuré en octets par seconde.</span><span class="sxs-lookup"><span data-stu-id="e1c49-249">Average throughput since the last log, measured in bytes per second.</span></span>|

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
> <span data-ttu-id="e1c49-250">La latence est calculée à partir de l’heure de la réception du premier octet de la requête HTTP jusqu’à l’heure de l'envoi du dernier octet de la réponse HTTP.</span><span class="sxs-lookup"><span data-stu-id="e1c49-250">Latency is calculated from the time when the first byte of the HTTP request is received to the time when the last byte of the HTTP response is sent.</span></span> <span data-ttu-id="e1c49-251">Il s’agit de la somme du temps de traitement d’Application Gateway et du coût du réseau pour le serveur principal, ainsi que le temps pris par le serveur principal pour traiter la requête.</span><span class="sxs-lookup"><span data-stu-id="e1c49-251">It's the sum of the Application Gateway processing time plus the network cost to the back end, plus the time that the back end takes to process the request.</span></span>

### <a name="firewall-log"></a><span data-ttu-id="e1c49-252">Journal du pare-feu</span><span class="sxs-lookup"><span data-stu-id="e1c49-252">Firewall log</span></span>

<span data-ttu-id="e1c49-253">Le journal du pare-feu n’est généré que si vous l’avez activé sur chaque passerelle Application Gateway, comme détaillé dans les étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="e1c49-253">The firewall log is generated only if you have enabled it for each application gateway, as detailed in the preceding steps.</span></span> <span data-ttu-id="e1c49-254">Ce fichier journal nécessite également que ce pare-feu d’applications web soit configuré sur une passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="e1c49-254">This log also requires that the web application firewall is configured on an application gateway.</span></span> <span data-ttu-id="e1c49-255">Les données sont stockées dans le compte de stockage spécifié lors de l’activation de la journalisation.</span><span class="sxs-lookup"><span data-stu-id="e1c49-255">The data is stored in the storage account that you specified when you enabled the logging.</span></span> <span data-ttu-id="e1c49-256">Les données suivantes sont enregistrées :</span><span class="sxs-lookup"><span data-stu-id="e1c49-256">The following data is logged:</span></span>


|<span data-ttu-id="e1c49-257">Valeur</span><span class="sxs-lookup"><span data-stu-id="e1c49-257">Value</span></span>  |<span data-ttu-id="e1c49-258">Description</span><span class="sxs-lookup"><span data-stu-id="e1c49-258">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="e1c49-259">instanceId</span><span class="sxs-lookup"><span data-stu-id="e1c49-259">instanceId</span></span>     | <span data-ttu-id="e1c49-260">Instance Application Gateway pour laquelle les données du pare-feu sont générées.</span><span class="sxs-lookup"><span data-stu-id="e1c49-260">Application Gateway instance for which firewall data is being generated.</span></span> <span data-ttu-id="e1c49-261">Pour une passerelle Application Gateway à plusieurs instances, il y a une ligne par instance.</span><span class="sxs-lookup"><span data-stu-id="e1c49-261">For a multiple-instance application gateway, there is one row per instance.</span></span>         |
|<span data-ttu-id="e1c49-262">clientIp</span><span class="sxs-lookup"><span data-stu-id="e1c49-262">clientIp</span></span>     |   <span data-ttu-id="e1c49-263">Adresse IP d’origine de la requête.</span><span class="sxs-lookup"><span data-stu-id="e1c49-263">Originating IP for the request.</span></span>      |
|<span data-ttu-id="e1c49-264">clientPort</span><span class="sxs-lookup"><span data-stu-id="e1c49-264">clientPort</span></span>     |  <span data-ttu-id="e1c49-265">Port d’origine de la requête.</span><span class="sxs-lookup"><span data-stu-id="e1c49-265">Originating port for the request.</span></span>       |
|<span data-ttu-id="e1c49-266">requestUri</span><span class="sxs-lookup"><span data-stu-id="e1c49-266">requestUri</span></span>     | <span data-ttu-id="e1c49-267">URL de la requête reçue.</span><span class="sxs-lookup"><span data-stu-id="e1c49-267">URL of the received request.</span></span>       |
|<span data-ttu-id="e1c49-268">ruleSetType</span><span class="sxs-lookup"><span data-stu-id="e1c49-268">ruleSetType</span></span>     | <span data-ttu-id="e1c49-269">Type d’ensemble de règles.</span><span class="sxs-lookup"><span data-stu-id="e1c49-269">Rule set type.</span></span> <span data-ttu-id="e1c49-270">La valeur disponible est OWASP.</span><span class="sxs-lookup"><span data-stu-id="e1c49-270">The available value is OWASP.</span></span>        |
|<span data-ttu-id="e1c49-271">ruleSetVersion</span><span class="sxs-lookup"><span data-stu-id="e1c49-271">ruleSetVersion</span></span>     | <span data-ttu-id="e1c49-272">Version d’ensemble de règles utilisée.</span><span class="sxs-lookup"><span data-stu-id="e1c49-272">Rule set version used.</span></span> <span data-ttu-id="e1c49-273">Les valeurs disponibles sont 2.2.9 et 3.0.</span><span class="sxs-lookup"><span data-stu-id="e1c49-273">Available values are 2.2.9 and 3.0.</span></span>     |
|<span data-ttu-id="e1c49-274">ruleId</span><span class="sxs-lookup"><span data-stu-id="e1c49-274">ruleId</span></span>     | <span data-ttu-id="e1c49-275">ID de règle de l’événement de déclenchement.</span><span class="sxs-lookup"><span data-stu-id="e1c49-275">Rule ID of the triggering event.</span></span>        |
|<span data-ttu-id="e1c49-276">Message</span><span class="sxs-lookup"><span data-stu-id="e1c49-276">message</span></span>     | <span data-ttu-id="e1c49-277">Message convivial pour l’événement de déclenchement.</span><span class="sxs-lookup"><span data-stu-id="e1c49-277">User-friendly message for the triggering event.</span></span> <span data-ttu-id="e1c49-278">La section Détails vous fournit plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="e1c49-278">More details are provided in the details section.</span></span>        |
|<span data-ttu-id="e1c49-279">action</span><span class="sxs-lookup"><span data-stu-id="e1c49-279">action</span></span>     |  <span data-ttu-id="e1c49-280">Action effectuée sur la requête.</span><span class="sxs-lookup"><span data-stu-id="e1c49-280">Action taken on the request.</span></span> <span data-ttu-id="e1c49-281">Les valeurs disponibles sont bloquées et autorisées.</span><span class="sxs-lookup"><span data-stu-id="e1c49-281">Available values are Blocked and Allowed.</span></span>      |
|<span data-ttu-id="e1c49-282">site</span><span class="sxs-lookup"><span data-stu-id="e1c49-282">site</span></span>     | <span data-ttu-id="e1c49-283">Site pour lequel le journal a été généré.</span><span class="sxs-lookup"><span data-stu-id="e1c49-283">Site for which the log was generated.</span></span> <span data-ttu-id="e1c49-284">Actuellement, seul Global est répertorié car les règles sont globales.</span><span class="sxs-lookup"><span data-stu-id="e1c49-284">Currently, only Global is listed because rules are global.</span></span>|
|<span data-ttu-id="e1c49-285">détails</span><span class="sxs-lookup"><span data-stu-id="e1c49-285">details</span></span>     | <span data-ttu-id="e1c49-286">Détails de l’événement de déclenchement.</span><span class="sxs-lookup"><span data-stu-id="e1c49-286">Details of the triggering event.</span></span>        |
|<span data-ttu-id="e1c49-287">details.message</span><span class="sxs-lookup"><span data-stu-id="e1c49-287">details.message</span></span>     | <span data-ttu-id="e1c49-288">Description de la règle.</span><span class="sxs-lookup"><span data-stu-id="e1c49-288">Description of the rule.</span></span>        |
|<span data-ttu-id="e1c49-289">details.data</span><span class="sxs-lookup"><span data-stu-id="e1c49-289">details.data</span></span>     | <span data-ttu-id="e1c49-290">Données spécifiques trouvées dans la requête correspondant à la règle.</span><span class="sxs-lookup"><span data-stu-id="e1c49-290">Specific data found in request that matched the rule.</span></span>         |
|<span data-ttu-id="e1c49-291">details.file</span><span class="sxs-lookup"><span data-stu-id="e1c49-291">details.file</span></span>     | <span data-ttu-id="e1c49-292">Fichier de configuration qui contenait la règle.</span><span class="sxs-lookup"><span data-stu-id="e1c49-292">Configuration file that contained the rule.</span></span>        |
|<span data-ttu-id="e1c49-293">details.line</span><span class="sxs-lookup"><span data-stu-id="e1c49-293">details.line</span></span>     | <span data-ttu-id="e1c49-294">Numéro de ligne dans le fichier de configuration ayant déclenché l’événement.</span><span class="sxs-lookup"><span data-stu-id="e1c49-294">Line number in the configuration file that triggered the event.</span></span>       |

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

### <a name="view-and-analyze-the-activity-log"></a><span data-ttu-id="e1c49-295">Afficher et analyser le journal d’activité</span><span class="sxs-lookup"><span data-stu-id="e1c49-295">View and analyze the activity log</span></span>

<span data-ttu-id="e1c49-296">Vous pouvez afficher et analyser les données du journal d’activité en utilisant l’une des méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="e1c49-296">You can view and analyze activity log data by using any of the following methods:</span></span>

* <span data-ttu-id="e1c49-297">**Outils Azure** : récupérez les informations à partir du journal d’activité au moyen d’Azure PowerShell, d’Azure CLI, de l’API REST Azure ou du Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e1c49-297">**Azure tools**: Retrieve information from the activity log through Azure PowerShell, the Azure CLI, the Azure REST API, or the Azure portal.</span></span> <span data-ttu-id="e1c49-298">Des instructions pas à pas pour chaque méthode sont détaillées dans l’article [Opérations d’activité avec Resource Manager](../azure-resource-manager/resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="e1c49-298">Step-by-step instructions for each method are detailed in the [Activity operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.</span></span>
* <span data-ttu-id="e1c49-299">**Power BI** : si vous n’avez pas encore de compte [Power BI](https://powerbi.microsoft.com/pricing) , vous pouvez l’essayer gratuitement.</span><span class="sxs-lookup"><span data-stu-id="e1c49-299">**Power BI**: If you don't already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free.</span></span> <span data-ttu-id="e1c49-300">À l’aide du [pack de contenus des journaux d’activité Azure pour Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), vous pouvez analyser vos données avec des tableaux de bord préconfigurés à utiliser en l’état ou à personnaliser.</span><span class="sxs-lookup"><span data-stu-id="e1c49-300">By using the [Azure Activity Logs content pack for Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), you can analyze your data with preconfigured dashboards that you can use as is or customize.</span></span>

### <a name="view-and-analyze-the-access-performance-and-firewall-logs"></a><span data-ttu-id="e1c49-301">Affichage et analyse des journaux d’accès, des performances et du pare-feu</span><span class="sxs-lookup"><span data-stu-id="e1c49-301">View and analyze the access, performance, and firewall logs</span></span>

<span data-ttu-id="e1c49-302">Azure [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md) peut collecter les fichiers du compteur et du journal d’événements à partir de votre compte de stockage d’objets Blob.</span><span class="sxs-lookup"><span data-stu-id="e1c49-302">Azure [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md) can collect the counter and event log files from your Blob storage account.</span></span> <span data-ttu-id="e1c49-303">Il inclut des visualisations et des fonctionnalités puissantes de recherche pour analyser vos journaux.</span><span class="sxs-lookup"><span data-stu-id="e1c49-303">It includes visualizations and powerful search capabilities to analyze your logs.</span></span>

<span data-ttu-id="e1c49-304">Vous pouvez également vous connecter à votre compte de stockage et récupérer les entrées de journal JSON pour les journaux d’accès et des performances.</span><span class="sxs-lookup"><span data-stu-id="e1c49-304">You can also connect to your storage account and retrieve the JSON log entries for access and performance logs.</span></span> <span data-ttu-id="e1c49-305">Après avoir téléchargé les fichiers JSON, vous pouvez les convertir en CSV et les afficher dans Excel, PowerBI ou tout autre outil de visualisation de données.</span><span class="sxs-lookup"><span data-stu-id="e1c49-305">After you download the JSON files, you can convert them to CSV and view them in Excel, Power BI, or any other data-visualization tool.</span></span>

> [!TIP]
> <span data-ttu-id="e1c49-306">Si vous savez utiliser Visual Studio et les concepts de base de la modification des valeurs de constantes et variables en C#, vous pouvez utiliser les [outils de convertisseur de journaux](https://github.com/Azure-Samples/networking-dotnet-log-converter) disponibles dans GitHub.</span><span class="sxs-lookup"><span data-stu-id="e1c49-306">If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use the [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.</span></span>
> 
> 

## <a name="metrics"></a><span data-ttu-id="e1c49-307">Mesures</span><span class="sxs-lookup"><span data-stu-id="e1c49-307">Metrics</span></span>

<span data-ttu-id="e1c49-308">Les mesures représentent une fonctionnalité de certaines ressources Azure, vous permettant d’afficher les compteurs de performances dans le portail.</span><span class="sxs-lookup"><span data-stu-id="e1c49-308">Metrics are a feature for certain Azure resources where you can view performance counters in the portal.</span></span> <span data-ttu-id="e1c49-309">Pour Application Gateway, une métrique est désormais disponible.</span><span class="sxs-lookup"><span data-stu-id="e1c49-309">For Application Gateway, one metric is available now.</span></span> <span data-ttu-id="e1c49-310">Vous pouvez afficher cette métrique, le débit, dans le portail.</span><span class="sxs-lookup"><span data-stu-id="e1c49-310">This metric is throughput, and you can see it in the portal.</span></span> <span data-ttu-id="e1c49-311">Accédez à une passerelle Application Gateway et cliquez sur **Métriques**.</span><span class="sxs-lookup"><span data-stu-id="e1c49-311">Browse to an application gateway and click **Metrics**.</span></span> <span data-ttu-id="e1c49-312">Sélectionnez Débit dans la section **Mesures disponibles** pour afficher les valeurs.</span><span class="sxs-lookup"><span data-stu-id="e1c49-312">To view the values, select throughput in the **Available metrics** section.</span></span> <span data-ttu-id="e1c49-313">L’image suivante montre un exemple avec les filtres que vous pouvez utiliser pour afficher les données dans différentes périodes.</span><span class="sxs-lookup"><span data-stu-id="e1c49-313">In the following image, you can see an example with the filters that you can use to display the data in different time ranges.</span></span>

![Affichage de métriques avec des filtres][5]

<span data-ttu-id="e1c49-315">Pour afficher une liste actuelle des métriques, consultez [Mesures prises en charge avec Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="e1c49-315">To see a current list of metrics, see [Supported metrics with Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span></span>

### <a name="alert-rules"></a><span data-ttu-id="e1c49-316">Règles d'alerte</span><span class="sxs-lookup"><span data-stu-id="e1c49-316">Alert rules</span></span>

<span data-ttu-id="e1c49-317">Vous pouvez démarrer des règles d’alerte en fonction des métriques d’une ressource.</span><span class="sxs-lookup"><span data-stu-id="e1c49-317">You can start alert rules based on metrics for a resource.</span></span> <span data-ttu-id="e1c49-318">Par exemple, une alerte peut appeler un webhook ou envoyer un e-mail à un administrateur si le débit de la passerelle Application Gateway est au-dessus ou en dessous d’un seuil pour une période spécifiée.</span><span class="sxs-lookup"><span data-stu-id="e1c49-318">For example, an alert can call a webhook or email an administrator if the throughput of the application gateway is above, below, or at a threshold for a specified period.</span></span>

<span data-ttu-id="e1c49-319">L’exemple suivant vous guide dans la création d’une règle d’alerte qui envoie un e-mail à un administrateur lorsqu’un seuil de débit est dépassé :</span><span class="sxs-lookup"><span data-stu-id="e1c49-319">The following example walks you through creating an alert rule that sends an email to an administrator after throughput breaches a threshold:</span></span>

1. <span data-ttu-id="e1c49-320">Cliquez sur **Ajouter une alerte Métrique** pour ouvrir le panneau **Ajouter une règle**.</span><span class="sxs-lookup"><span data-stu-id="e1c49-320">Click **Add metric alert** to open the **Add rule** blade.</span></span> <span data-ttu-id="e1c49-321">Ce panneau est également accessible à partir du panneau Métriques.</span><span class="sxs-lookup"><span data-stu-id="e1c49-321">You can also reach this blade from the metrics blade.</span></span>

   ![Bouton Ajouter une alerte Métrique][6]

2. <span data-ttu-id="e1c49-323">Dans le panneau **Ajouter une règle**, remplissez les sections Nom, Condition et Notifier, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="e1c49-323">On the **Add rule** blade, fill out the name, condition, and notify sections, and click **OK**.</span></span>

   * <span data-ttu-id="e1c49-324">Dans le sélecteur **Condition**, sélectionnez une des 4 valeurs : **Supérieur à**, **Supérieur ou égal à**, **Inférieur à** ou **Inférieur ou égal à**.</span><span class="sxs-lookup"><span data-stu-id="e1c49-324">In the **Condition** selector, select one of the four values: **Greater than**, **Greater than or equal**, **Less than**, or **Less than or equal to**.</span></span>

   * <span data-ttu-id="e1c49-325">Dans le sélecteur **Période**, sélectionnez une période allant de 5 minutes à 6 heures.</span><span class="sxs-lookup"><span data-stu-id="e1c49-325">In the **Period** selector, select a period from 5 minutes to 6 hours.</span></span>

   * <span data-ttu-id="e1c49-326">Si vous sélectionnez **Envoyer des e-mails aux propriétaires, contributeurs et lecteurs** , l’e-mail peut être dynamiquement basé sur les utilisateurs qui ont accès à cette ressource.</span><span class="sxs-lookup"><span data-stu-id="e1c49-326">If you select **Email owners, contributors, and readers**, the email can be dynamic based on the users who have access to that resource.</span></span> <span data-ttu-id="e1c49-327">Dans le cas contraire, vous pouvez fournir une liste d’utilisateurs séparée par des virgules dans la zone **Adresse(s) de messagerie d’administrateur(s) supplémentaire(s)** .</span><span class="sxs-lookup"><span data-stu-id="e1c49-327">Otherwise, you can provide a comma-separated list of users in the **Additional administrator email(s)** box.</span></span>

   ![Panneau Ajouter une règle][7]

<span data-ttu-id="e1c49-329">Si le seuil est dépassé, un e-mail similaire à celui de l’image suivante vous est envoyé :</span><span class="sxs-lookup"><span data-stu-id="e1c49-329">If the threshold is breached, an email that's similar to the one in the following image arrives:</span></span>

![E-mail en cas de dépassement de seuil][8]

<span data-ttu-id="e1c49-331">Une liste d’alertes apparaît une fois que vous avez créé une alerte Métrique.</span><span class="sxs-lookup"><span data-stu-id="e1c49-331">A list of alerts appears after you create a metric alert.</span></span> <span data-ttu-id="e1c49-332">Elle fournit une vue d’ensemble de toutes les règles d’alerte.</span><span class="sxs-lookup"><span data-stu-id="e1c49-332">It provides an overview of all the alert rules.</span></span>

![Liste d’alertes et de règles][9]

<span data-ttu-id="e1c49-334">Pour en savoir plus sur les notifications d’alerte, consultez [Réception de notifications d’alerte](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="e1c49-334">To learn more about alert notifications, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="e1c49-335">Pour en savoir plus sur les webhooks et sur la façon de les utiliser avec des alertes, consultez [Configurer un webhook sur une alerte de métrique Azure](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="e1c49-335">To understand more about webhooks and how you can use them with alerts, visit [Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1c49-336">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e1c49-336">Next steps</span></span>

* <span data-ttu-id="e1c49-337">Visualisation du compteur et des journaux des événements à l’aide de [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="e1c49-337">Visualize counter and event logs by using [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md).</span></span>
* <span data-ttu-id="e1c49-338">Billet de blog sur la [visualisation de votre journal d’activité Azure avec Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx).</span><span class="sxs-lookup"><span data-stu-id="e1c49-338">[Visualize your Azure activity log with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog post.</span></span>
* <span data-ttu-id="e1c49-339">Billet de blog sur [l’affichage et l’analyse des journaux d’activité Azure dans Power BI](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/).</span><span class="sxs-lookup"><span data-stu-id="e1c49-339">[View and analyze Azure activity logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.</span></span>

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
