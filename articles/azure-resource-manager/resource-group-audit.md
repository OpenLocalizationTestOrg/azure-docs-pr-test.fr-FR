---
title: "aaaView activités Windows Azure consigne les ressources toomonitor | Documents Microsoft"
description: "Utilisez hello activité enregistre les erreurs et les actions de l’utilisateur tooreview. Affiche le portail Azure, PowerShell, l’interface CLI Azure et REST."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: fcdb3125-13ce-4c3b-9087-f514c5e41e73
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: tomfitz
ms.openlocfilehash: 8430ed2a9c1dfe5f13423a55d358e590b0facb22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="view-activity-logs-tooaudit-actions-on-resources"></a><span data-ttu-id="282c1-104">Afficher l’activité enregistre les actions de tooaudit sur les ressources</span><span class="sxs-lookup"><span data-stu-id="282c1-104">View activity logs tooaudit actions on resources</span></span>
<span data-ttu-id="282c1-105">Les journaux d’activité vous permettent de déterminer :</span><span class="sxs-lookup"><span data-stu-id="282c1-105">Through activity logs, you can determine:</span></span>

* <span data-ttu-id="282c1-106">les opérations effectuées sur les ressources hello dans votre abonnement</span><span class="sxs-lookup"><span data-stu-id="282c1-106">what operations were taken on hello resources in your subscription</span></span>
* <span data-ttu-id="282c1-107">qui a lancé une opération hello (bien que les opérations générées par un service principal ne retournent pas d’un utilisateur en tant que l’appelant de hello)</span><span class="sxs-lookup"><span data-stu-id="282c1-107">who initiated hello operation (although operations initiated by a backend service do not return a user as hello caller)</span></span>
* <span data-ttu-id="282c1-108">Lorsque l’opération de hello s’est produite</span><span class="sxs-lookup"><span data-stu-id="282c1-108">when hello operation occurred</span></span>
* <span data-ttu-id="282c1-109">état Hello d’opération de hello</span><span class="sxs-lookup"><span data-stu-id="282c1-109">hello status of hello operation</span></span>
* <span data-ttu-id="282c1-110">les valeurs Hello d’autres propriétés qui peuvent vous aider à effectuer des recherches sur les opération hello</span><span class="sxs-lookup"><span data-stu-id="282c1-110">hello values of other properties that might help you research hello operation</span></span>

[!INCLUDE [resource-manager-audit-limitations](../../includes/resource-manager-audit-limitations.md)]

<span data-ttu-id="282c1-111">Vous pouvez récupérer des informations à partir des journaux d’activité hello via le portail hello, PowerShell, CLI d’Azure, API REST de Insights, ou [Insights .NET bibliothèque](https://www.nuget.org/packages/Microsoft.Azure.Insights/).</span><span class="sxs-lookup"><span data-stu-id="282c1-111">You can retrieve information from hello activity logs through hello portal, PowerShell, Azure CLI, Insights REST API, or [Insights .NET Library](https://www.nuget.org/packages/Microsoft.Azure.Insights/).</span></span>

## <a name="portal"></a><span data-ttu-id="282c1-112">Portail</span><span class="sxs-lookup"><span data-stu-id="282c1-112">Portal</span></span>
1. <span data-ttu-id="282c1-113">journaux d’activité hello tooview via le portail de hello, sélectionnez **analyse**.</span><span class="sxs-lookup"><span data-stu-id="282c1-113">tooview hello activity logs through hello portal, select **Monitor**.</span></span>
   
    ![sélectionner les journaux d’activité](./media/resource-group-audit/select-monitor.png)

   <span data-ttu-id="282c1-115">Ou, tooautomatically filtrer le journal d’activité hello pour une ressource particulière ou d’un groupe de ressources, sélectionnez **le journal d’activité** à partir de ce panneau des ressources.</span><span class="sxs-lookup"><span data-stu-id="282c1-115">Or, tooautomatically filter hello activity log for a particular resource or resource group, select **Activity log** from that resource blade.</span></span> <span data-ttu-id="282c1-116">Notez que ce journal d’activité hello est filtré automatiquement par la ressource de hello sélectionné.</span><span class="sxs-lookup"><span data-stu-id="282c1-116">Notice that hello activity log is automatically filtered by hello selected resource.</span></span>
   
    ![filtrer par ressource](./media/resource-group-audit/filtered-by-resource.png)
2. <span data-ttu-id="282c1-118">Bonjour **le journal d’activité** panneau, vous voyez un résumé des dernières opérations.</span><span class="sxs-lookup"><span data-stu-id="282c1-118">In hello **Activity Log** blade, you see a summary of recent operations.</span></span>
   
    ![afficher des actions](./media/resource-group-audit/audit-summary.png)
3. <span data-ttu-id="282c1-120">nombre de hello toorestrict d’opérations affichée, sélectionnez différentes conditions.</span><span class="sxs-lookup"><span data-stu-id="282c1-120">toorestrict hello number of operations displayed, select different conditions.</span></span> <span data-ttu-id="282c1-121">Par exemple, hello image suivante montre hello **Timespan** et **événement déclenché par** champs modifiés tooview hello mesures par un utilisateur particulier ou d’une application pour hello du mois passé.</span><span class="sxs-lookup"><span data-stu-id="282c1-121">For example, hello following image shows hello **Timespan** and **Event initiated by** fields changed tooview hello actions taken by a particular user or application for hello past month.</span></span> <span data-ttu-id="282c1-122">Sélectionnez **appliquer** tooview les résultats de hello de votre requête.</span><span class="sxs-lookup"><span data-stu-id="282c1-122">Select **Apply** tooview hello results of your query.</span></span>
   
    ![définir des options de filtre](./media/resource-group-audit/set-filter.png)

4. <span data-ttu-id="282c1-124">Si vous avez besoin de requête de hello toorun plus tard, sélectionnez **enregistrer** et donnez un nom à des requêtes de hello.</span><span class="sxs-lookup"><span data-stu-id="282c1-124">If you need toorun hello query again later, select **Save** and give hello query a name.</span></span>
   
    ![enregistrer la requête](./media/resource-group-audit/save-query.png)
5. <span data-ttu-id="282c1-126">tooquickly exécuter une requête, vous pouvez sélectionner une requêtes de hello intégrées, telles que de déploiement a échoué.</span><span class="sxs-lookup"><span data-stu-id="282c1-126">tooquickly run a query, you can select one of hello built-in queries, such as failed deployments.</span></span>

    ![sélectionner la requête](./media/resource-group-audit/select-quick-query.png)

   <span data-ttu-id="282c1-128">requête Hello définit automatiquement les valeurs de filtre hello requis.</span><span class="sxs-lookup"><span data-stu-id="282c1-128">hello selected query automatically sets hello required filter values.</span></span>

    ![afficher les erreurs de déploiement](./media/resource-group-audit/view-failed-deployment.png)   

6. <span data-ttu-id="282c1-130">Sélectionnez une des hello operations toosee un résumé des événements de hello.</span><span class="sxs-lookup"><span data-stu-id="282c1-130">Select one of hello operations toosee a summary of hello event.</span></span>

    ![afficher l’opération](./media/resource-group-audit/view-operation.png)  

## <a name="powershell"></a><span data-ttu-id="282c1-132">PowerShell</span><span class="sxs-lookup"><span data-stu-id="282c1-132">PowerShell</span></span>
1. <span data-ttu-id="282c1-133">les entrées de journal tooretrieve, exécutez hello **Get-AzureRmLog** commande.</span><span class="sxs-lookup"><span data-stu-id="282c1-133">tooretrieve log entries, run hello **Get-AzureRmLog** command.</span></span> <span data-ttu-id="282c1-134">Vous fournissez des paramètres supplémentaires toofilter hello liste d’entrées.</span><span class="sxs-lookup"><span data-stu-id="282c1-134">You provide additional parameters toofilter hello list of entries.</span></span> <span data-ttu-id="282c1-135">Si vous ne spécifiez pas une heure de début et de fin, les entrées pour hello dernière heure sont retournées.</span><span class="sxs-lookup"><span data-stu-id="282c1-135">If you do not specify a start and end time, entries for hello last hour are returned.</span></span> <span data-ttu-id="282c1-136">Par exemple, les opérations de hello tooretrieve pour un groupe de ressources au cours de la dernière heure de hello exécutent :</span><span class="sxs-lookup"><span data-stu-id="282c1-136">For example, tooretrieve hello operations for a resource group during hello past hour run:</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup
  ```
   
    <span data-ttu-id="282c1-137">Bonjour à l’exemple suivant montre comment l’activité de hello toouse du journal tooresearch les opérations effectuées pendant une durée spécifiée.</span><span class="sxs-lookup"><span data-stu-id="282c1-137">hello following example shows how toouse hello activity log tooresearch operations taken during a specified time.</span></span> <span data-ttu-id="282c1-138">Hello les dates de début et de fin sont spécifiées dans un format de date.</span><span class="sxs-lookup"><span data-stu-id="282c1-138">hello start and end dates are specified in a date format.</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime 2015-08-28T06:00 -EndTime 2015-09-10T06:00
  ```

    <span data-ttu-id="282c1-139">Ou bien, vous pouvez utiliser les fonctions toospecify hello date plage de dates, par exemple hello 14 derniers jours.</span><span class="sxs-lookup"><span data-stu-id="282c1-139">Or, you can use date functions toospecify hello date range, such as hello last 14 days.</span></span>
   
  ```powershell 
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14)
  ```

2. <span data-ttu-id="282c1-140">En fonction de l’heure de début hello que vous spécifiez, les commandes précédentes hello peuvent retourner une longue liste des opérations de groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="282c1-140">Depending on hello start time you specify, hello previous commands can return a long list of operations for hello resource group.</span></span> <span data-ttu-id="282c1-141">Vous pouvez filtrer les résultats de hello pour ce que vous recherchez en fournissant des critères de recherche.</span><span class="sxs-lookup"><span data-stu-id="282c1-141">You can filter hello results for what you are looking for by providing search criteria.</span></span> <span data-ttu-id="282c1-142">Par exemple, si vous essayez de tooresearch comment une application web a été arrêtée, vous pouvez exécuter hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="282c1-142">For example, if you are trying tooresearch how a web app was stopped, you could run hello following command:</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14) | Where-Object OperationName -eq Microsoft.Web/sites/stop/action
  ```

    <span data-ttu-id="282c1-143">Dans cet exemple, elle montre qu’une action d’arrêt a été effectuée par someone@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="282c1-143">Which for this example shows that a stop action was performed by someone@contoso.com.</span></span> 

  ```powershell 
  Authorization     :
  Scope     : /subscriptions/xxxxx/resourcegroups/ExampleGroup/providers/Microsoft.Web/sites/ExampleSite
  Action    : Microsoft.Web/sites/stop/action
  Role      : Subscription Admin
  Condition :
  Caller            : someone@contoso.com
  CorrelationId     : 84beae59-92aa-4662-a6fc-b6fecc0ff8da
  EventSource       : Administrative
  EventTimestamp    : 8/28/2015 4:08:18 PM
  OperationName     : Microsoft.Web/sites/stop/action
  ResourceGroupName : ExampleGroup
  ResourceId        : /subscriptions/xxxxx/resourcegroups/ExampleGroup/providers/Microsoft.Web/sites/ExampleSite
  Status            : Succeeded
  SubscriptionId    : xxxxx
  SubStatus         : OK
  ```

3. <span data-ttu-id="282c1-144">Vous pouvez rechercher des actions de hello effectuées par un utilisateur particulier, même pour un groupe de ressources qui n’existe plus.</span><span class="sxs-lookup"><span data-stu-id="282c1-144">You can look up hello actions taken by a particular user, even for a resource group that no longer exists.</span></span>

  ```powershell 
  Get-AzureRmLog -ResourceGroup deletedgroup -StartTime (Get-Date).AddDays(-14) -Caller someone@contoso.com
  ```

4. <span data-ttu-id="282c1-145">Vous pouvez filtrer les résultats sur les opérations ayant échoué.</span><span class="sxs-lookup"><span data-stu-id="282c1-145">You can filter for failed operations.</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -Status Failed
  ```

5. <span data-ttu-id="282c1-146">Vous concentrer sur une erreur en examinant le message d’état hello pour cette entrée.</span><span class="sxs-lookup"><span data-stu-id="282c1-146">You can focus on one error by looking at hello status message for that entry.</span></span>
   
        ((Get-AzureRmLog -Status Failed -ResourceGroup ExampleGroup -DetailedOutput).Properties[1].Content["statusMessage"] | ConvertFrom-Json).error
   
    <span data-ttu-id="282c1-147">Résultat :</span><span class="sxs-lookup"><span data-stu-id="282c1-147">Which returns:</span></span>
   
        code           message                                                                        
        ----           -------                                                                        
        DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. 


## <a name="azure-cli"></a><span data-ttu-id="282c1-148">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="282c1-148">Azure CLI</span></span>
* <span data-ttu-id="282c1-149">les entrées de journal tooretrieve, que vous exécutez hello **groupe azure journal afficher** commande.</span><span class="sxs-lookup"><span data-stu-id="282c1-149">tooretrieve log entries, you run hello **azure group log show** command.</span></span>

  ```azurecli
  azure group log show ExampleGroup --json
  ```


## <a name="rest-api"></a><span data-ttu-id="282c1-150">API REST</span><span class="sxs-lookup"><span data-stu-id="282c1-150">REST API</span></span>
<span data-ttu-id="282c1-151">opérations de REST Hello pour travailler avec le journal d’activité hello font partie de hello [Insights REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="282c1-151">hello REST operations for working with hello activity log are part of hello [Insights REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span> <span data-ttu-id="282c1-152">les événements de journal d’activité tooretrieve, consultez [liste des événements de gestion hello dans un abonnement](https://msdn.microsoft.com/library/azure/dn931934.aspx).</span><span class="sxs-lookup"><span data-stu-id="282c1-152">tooretrieve activity log events, see [List hello management events in a subscription](https://msdn.microsoft.com/library/azure/dn931934.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="282c1-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="282c1-153">Next steps</span></span>
* <span data-ttu-id="282c1-154">Journaux d’activité Azure sont utilisables avec Power BI toogain supérieur perspectives détaillées sur les actions hello dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="282c1-154">Azure Activity logs can be used with Power BI toogain greater insights about hello actions in your subscription.</span></span> <span data-ttu-id="282c1-155">Consultez le billet de blog sur [l’affichage et l’analyse des journaux d’activité Azure dans Power BI](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/).</span><span class="sxs-lookup"><span data-stu-id="282c1-155">See [View and analyze Azure Activity Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/).</span></span>
* <span data-ttu-id="282c1-156">toolearn sur la définition des stratégies de sécurité, consultez [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="282c1-156">toolearn about setting security policies, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>
* <span data-ttu-id="282c1-157">toolearn sur les commandes hello pour l’affichage des opérations de déploiement, consultez [afficher les opérations de déploiement](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="282c1-157">toolearn about hello commands for viewing deployment operations, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="282c1-158">toolearn tooprevent des suppressions sur une ressource pour tous les utilisateurs, voir [verrouiller les ressources avec Azure Resource Manager](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="282c1-158">toolearn how tooprevent deletions on a resource for all users, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

