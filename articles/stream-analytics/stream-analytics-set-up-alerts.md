---
title: "aaaSet des alertes pour les requêtes dans le flux de données Analytique | Documents Microsoft"
description: "Présentation des alertes Stream Analytics"
keywords: configurer des alertes
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9952e2cf-b335-4a5c-8f45-8d3e1eda2e20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/26/2017
ms.author: jeffstok
ms.openlocfilehash: 7b1d90d1468311186567c8518e0283ea6b88c3f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-alerts-for-azure-stream-analytics-jobs"></a><span data-ttu-id="f4514-104">Configuration d’alertes pour des tâches Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f4514-104">Set up alerts for Azure Stream Analytics jobs</span></span>
## <a name="introduction-monitor-page"></a><span data-ttu-id="f4514-105">Introduction : page de surveillance</span><span class="sxs-lookup"><span data-stu-id="f4514-105">Introduction: Monitor page</span></span>
<span data-ttu-id="f4514-106">Vous pouvez définir des alertes tootrigger une alerte lorsqu’un indicateur atteint une condition que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="f4514-106">You can set up alerts tootrigger an alert when a metric reaches a condition that you specify.</span></span> <span data-ttu-id="f4514-107">Par exemple, vous pouvez configurer une alerte pour une condition hello suivante :</span><span class="sxs-lookup"><span data-stu-id="f4514-107">For example, you might set up an alert for a condition like hello following:</span></span>

`If there are zero input events in hello last 5 minutes, send email notification toosa-admin@example.com`

<span data-ttu-id="f4514-108">Les règles peuvent être configurés sur des métriques via le portail de hello, ou peuvent être configurés [par programme](https://code.msdn.microsoft.com/windowsazure/Receive-Email-Notifications-199e2c9a) sur les données de journaux des opérations.</span><span class="sxs-lookup"><span data-stu-id="f4514-108">Rules can be set up on metrics through hello portal, or can be configured [programmatically](https://code.msdn.microsoft.com/windowsazure/Receive-Email-Notifications-199e2c9a) over Operation Logs data.</span></span>

## <a name="set-up-alerts-in-hello-azure-portal"></a><span data-ttu-id="f4514-109">Configurer des alertes dans hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="f4514-109">Set up alerts in hello Azure portal</span></span>
1. <span data-ttu-id="f4514-110">Bonjour portail Azure, ouvrez hello flux Analytique travail toocreate une alerte pour.</span><span class="sxs-lookup"><span data-stu-id="f4514-110">In hello Azure portal, open hello Stream Analytics job you want toocreate an alert for.</span></span> 

2. <span data-ttu-id="f4514-111">Bonjour **travail** panneau, cliquez sur hello **analyse** section.</span><span class="sxs-lookup"><span data-stu-id="f4514-111">In hello **Job** blade, click hello **Monitoring** section.</span></span>  

3. <span data-ttu-id="f4514-112">Bonjour **métrique** panneau, cliquez sur hello **ajouter une alerte** commande.</span><span class="sxs-lookup"><span data-stu-id="f4514-112">In hello **Metric** blade, click hello **Add alert** command.</span></span>

      ![Configuration du portail Azure](./media/stream-analytics-set-up-alerts/06-stream-analytics-set-up-alerts.png)  

4. <span data-ttu-id="f4514-114">Entrez un nom et une description.</span><span class="sxs-lookup"><span data-stu-id="f4514-114">Enter a name and a description.</span></span>

5. <span data-ttu-id="f4514-115">Utilisez hello sélecteurs toodefine hello condition sous le hello alerte est envoyée.</span><span class="sxs-lookup"><span data-stu-id="f4514-115">Use hello selectors toodefine hello condition under which hello alert will be sent.</span></span>

6. <span data-ttu-id="f4514-116">Fournissent des informations sur où l’alerte de hello doit accéder.</span><span class="sxs-lookup"><span data-stu-id="f4514-116">Provide information about where hello alert should go.</span></span>

      ![Configuration d’une alerte pour un travail Azure Stream Analytics](./media/stream-analytics-set-up-alerts/stream-analytics-add-alert.png)  

<span data-ttu-id="f4514-118">Pour plus d’informations sur la configuration des alertes dans hello portail Azure, consultez [recevoir des notifications d’alerte](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="f4514-118">For more detail on configuring alerts in hello Azure portal, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>  


## <a name="get-help"></a><span data-ttu-id="f4514-119">Obtenir de l’aide</span><span class="sxs-lookup"><span data-stu-id="f4514-119">Get help</span></span>
<span data-ttu-id="f4514-120">Pour obtenir une assistance, essayez notre [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="f4514-120">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4514-121">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f4514-121">Next steps</span></span>
* [<span data-ttu-id="f4514-122">Introduction tooAzure Analytique de flux de données</span><span class="sxs-lookup"><span data-stu-id="f4514-122">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="f4514-123">Prise en main d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f4514-123">Get started using Azure Stream Analytics</span></span>](stream-analytics-get-started.md)
* [<span data-ttu-id="f4514-124">Mise à l'échelle des travaux Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f4514-124">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="f4514-125">Références sur le langage des requêtes d'Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f4514-125">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="f4514-126">Références sur l’API REST de gestion d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f4514-126">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

