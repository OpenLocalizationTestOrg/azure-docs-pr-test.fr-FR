---
title: "Afficher les journaux d’activité Azure pour surveiller les ressources | Microsoft Docs"
description: "Utilisez les journaux d’activité pour passer en revue les actions et les erreurs des utilisateurs. Affiche le portail Azure, PowerShell, l’interface CLI Azure et REST."
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
ms.openlocfilehash: 9f90bc80c146c6c2da04aacbc110f7d389c0baa2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="view-activity-logs-to-audit-actions-on-resources"></a><span data-ttu-id="b372a-104">Afficher les journaux d’activité pour auditer les actions sur les ressources</span><span class="sxs-lookup"><span data-stu-id="b372a-104">View activity logs to audit actions on resources</span></span>
<span data-ttu-id="b372a-105">Les journaux d’activité vous permettent de déterminer :</span><span class="sxs-lookup"><span data-stu-id="b372a-105">Through activity logs, you can determine:</span></span>

* <span data-ttu-id="b372a-106">Les opérations qui ont été effectuées sur les ressources de votre abonnement</span><span class="sxs-lookup"><span data-stu-id="b372a-106">what operations were taken on the resources in your subscription</span></span>
* <span data-ttu-id="b372a-107">Les utilisateurs qui ont lancé l’opération (même si les opérations lancées par un service principal ne retournent pas d’utilisateur en tant qu’appelant)</span><span class="sxs-lookup"><span data-stu-id="b372a-107">who initiated the operation (although operations initiated by a backend service do not return a user as the caller)</span></span>
* <span data-ttu-id="b372a-108">Le moment où a eu lieu l’opération</span><span class="sxs-lookup"><span data-stu-id="b372a-108">when the operation occurred</span></span>
* <span data-ttu-id="b372a-109">L’état de l’opération</span><span class="sxs-lookup"><span data-stu-id="b372a-109">the status of the operation</span></span>
* <span data-ttu-id="b372a-110">Les valeurs d’autres propriétés qui peuvent vous aider à effectuer des recherches sur l’opération</span><span class="sxs-lookup"><span data-stu-id="b372a-110">the values of other properties that might help you research the operation</span></span>

[!INCLUDE [resource-manager-audit-limitations](../../includes/resource-manager-audit-limitations.md)]

<span data-ttu-id="b372a-111">Vous pouvez récupérer des informations dans les journaux d’activité par le biais du portail, de PowerShell, de l’interface de ligne de commande Azure, de l’API REST Insights ou de [Insights .NET Library](https://www.nuget.org/packages/Microsoft.Azure.Insights/).</span><span class="sxs-lookup"><span data-stu-id="b372a-111">You can retrieve information from the activity logs through the portal, PowerShell, Azure CLI, Insights REST API, or [Insights .NET Library](https://www.nuget.org/packages/Microsoft.Azure.Insights/).</span></span>

## <a name="portal"></a><span data-ttu-id="b372a-112">Portail</span><span class="sxs-lookup"><span data-stu-id="b372a-112">Portal</span></span>
1. <span data-ttu-id="b372a-113">Pour afficher les journaux d’activité via le portail, sélectionnez **Surveiller**.</span><span class="sxs-lookup"><span data-stu-id="b372a-113">To view the activity logs through the portal, select **Monitor**.</span></span>
   
    ![sélectionner les journaux d’activité](./media/resource-group-audit/select-monitor.png)

   <span data-ttu-id="b372a-115">Pour afficher automatiquement le journal d’activité d’une ressource ou d’un groupe de ressources en particulier, sélectionnez **Journal d’activité** à partir du panneau correspondant.</span><span class="sxs-lookup"><span data-stu-id="b372a-115">Or, to automatically filter the activity log for a particular resource or resource group, select **Activity log** from that resource blade.</span></span> <span data-ttu-id="b372a-116">Notez que le journal d’activité est automatiquement filtré sur la dernière ressource sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="b372a-116">Notice that the activity log is automatically filtered by the selected resource.</span></span>
   
    ![filtrer par ressource](./media/resource-group-audit/filtered-by-resource.png)
2. <span data-ttu-id="b372a-118">Le panneau **Journal d’activité** affiche un résumé des opérations récentes.</span><span class="sxs-lookup"><span data-stu-id="b372a-118">In the **Activity Log** blade, you see a summary of recent operations.</span></span>
   
    ![afficher des actions](./media/resource-group-audit/audit-summary.png)
3. <span data-ttu-id="b372a-120">Pour limiter le nombre d’opérations affichées, sélectionnez d’autres conditions.</span><span class="sxs-lookup"><span data-stu-id="b372a-120">To restrict the number of operations displayed, select different conditions.</span></span> <span data-ttu-id="b372a-121">Par exemple, l’illustration suivante indique les champs **Intervalle de temps** et **Événement lancé par** modifiés pour afficher les actions effectuées par un utilisateur ou une application au cours du mois passé.</span><span class="sxs-lookup"><span data-stu-id="b372a-121">For example, the following image shows the **Timespan** and **Event initiated by** fields changed to view the actions taken by a particular user or application for the past month.</span></span> <span data-ttu-id="b372a-122">Sélectionnez **Appliquer** pour afficher les résultats de votre requête.</span><span class="sxs-lookup"><span data-stu-id="b372a-122">Select **Apply** to view the results of your query.</span></span>
   
    ![définir des options de filtre](./media/resource-group-audit/set-filter.png)

4. <span data-ttu-id="b372a-124">Si vous avez besoin d’exécuter la requête ultérieurement, sélectionnez **Enregistrer** et attribuez un nom à votre requête.</span><span class="sxs-lookup"><span data-stu-id="b372a-124">If you need to run the query again later, select **Save** and give the query a name.</span></span>
   
    ![enregistrer la requête](./media/resource-group-audit/save-query.png)
5. <span data-ttu-id="b372a-126">Pour exécuter rapidement une requête, vous pouvez sélectionner une des requêtes intégrées, telles que les déploiements ayant échoué.</span><span class="sxs-lookup"><span data-stu-id="b372a-126">To quickly run a query, you can select one of the built-in queries, such as failed deployments.</span></span>

    ![sélectionner la requête](./media/resource-group-audit/select-quick-query.png)

   <span data-ttu-id="b372a-128">La requête sélectionnée définit automatiquement les valeurs de filtre requis.</span><span class="sxs-lookup"><span data-stu-id="b372a-128">The selected query automatically sets the required filter values.</span></span>

    ![afficher les erreurs de déploiement](./media/resource-group-audit/view-failed-deployment.png)   

6. <span data-ttu-id="b372a-130">Sélectionnez l’une des opérations pour afficher un résumé de l’événement.</span><span class="sxs-lookup"><span data-stu-id="b372a-130">Select one of the operations to see a summary of the event.</span></span>

    ![afficher l’opération](./media/resource-group-audit/view-operation.png)  

## <a name="powershell"></a><span data-ttu-id="b372a-132">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b372a-132">PowerShell</span></span>
1. <span data-ttu-id="b372a-133">Pour récupérer les entrées de journal, exécutez la commande **Get-AzureRmLog** .</span><span class="sxs-lookup"><span data-stu-id="b372a-133">To retrieve log entries, run the **Get-AzureRmLog** command.</span></span> <span data-ttu-id="b372a-134">Vous spécifiez des paramètres supplémentaires pour filtrer la liste des entrées.</span><span class="sxs-lookup"><span data-stu-id="b372a-134">You provide additional parameters to filter the list of entries.</span></span> <span data-ttu-id="b372a-135">Si vous ne spécifiez pas une heure de début et de fin, les entrées de la dernière heure sont retournées.</span><span class="sxs-lookup"><span data-stu-id="b372a-135">If you do not specify a start and end time, entries for the last hour are returned.</span></span> <span data-ttu-id="b372a-136">Par exemple, pour récupérer les opérations d’un groupe de ressources pendant la dernière heure d’exécution :</span><span class="sxs-lookup"><span data-stu-id="b372a-136">For example, to retrieve the operations for a resource group during the past hour run:</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup
  ```
   
    <span data-ttu-id="b372a-137">L’exemple suivant montre comment utiliser le journal d’activité pour rechercher les opérations effectuées pendant une période spécifique.</span><span class="sxs-lookup"><span data-stu-id="b372a-137">The following example shows how to use the activity log to research operations taken during a specified time.</span></span> <span data-ttu-id="b372a-138">Les dates de début et de fin sont indiquées dans un format de date.</span><span class="sxs-lookup"><span data-stu-id="b372a-138">The start and end dates are specified in a date format.</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime 2015-08-28T06:00 -EndTime 2015-09-10T06:00
  ```

    <span data-ttu-id="b372a-139">Vous pouvez également utiliser les fonctions de date pour spécifier la plage de dates, par exemple, les 14 derniers jours.</span><span class="sxs-lookup"><span data-stu-id="b372a-139">Or, you can use date functions to specify the date range, such as the last 14 days.</span></span>
   
  ```powershell 
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14)
  ```

2. <span data-ttu-id="b372a-140">En fonction de l’heure de début que vous spécifiez, les commandes précédentes peuvent retourner une longue liste d’opérations pour le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="b372a-140">Depending on the start time you specify, the previous commands can return a long list of operations for the resource group.</span></span> <span data-ttu-id="b372a-141">Vous pouvez filtrer les résultats de votre recherche en fournissant des critères de recherche.</span><span class="sxs-lookup"><span data-stu-id="b372a-141">You can filter the results for what you are looking for by providing search criteria.</span></span> <span data-ttu-id="b372a-142">Par exemple, si vous recherchez la manière dont une application web a été arrêtée, vous pouvez exécuter la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b372a-142">For example, if you are trying to research how a web app was stopped, you could run the following command:</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14) | Where-Object OperationName -eq Microsoft.Web/sites/stop/action
  ```

    <span data-ttu-id="b372a-143">Dans cet exemple, elle montre qu’une action d’arrêt a été effectuée par someone@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="b372a-143">Which for this example shows that a stop action was performed by someone@contoso.com.</span></span> 

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

3. <span data-ttu-id="b372a-144">Vous pouvez rechercher les actions effectuées par un utilisateur particulier, même pour un groupe de ressources qui n’existe plus.</span><span class="sxs-lookup"><span data-stu-id="b372a-144">You can look up the actions taken by a particular user, even for a resource group that no longer exists.</span></span>

  ```powershell 
  Get-AzureRmLog -ResourceGroup deletedgroup -StartTime (Get-Date).AddDays(-14) -Caller someone@contoso.com
  ```

4. <span data-ttu-id="b372a-145">Vous pouvez filtrer les résultats sur les opérations ayant échoué.</span><span class="sxs-lookup"><span data-stu-id="b372a-145">You can filter for failed operations.</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -Status Failed
  ```

5. <span data-ttu-id="b372a-146">Vous pouvez vous focaliser sur une erreur en examinant le message d’état pour cette entrée.</span><span class="sxs-lookup"><span data-stu-id="b372a-146">You can focus on one error by looking at the status message for that entry.</span></span>
   
        ((Get-AzureRmLog -Status Failed -ResourceGroup ExampleGroup -DetailedOutput).Properties[1].Content["statusMessage"] | ConvertFrom-Json).error
   
    <span data-ttu-id="b372a-147">Résultat :</span><span class="sxs-lookup"><span data-stu-id="b372a-147">Which returns:</span></span>
   
        code           message                                                                        
        ----           -------                                                                        
        DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. 


## <a name="azure-cli"></a><span data-ttu-id="b372a-148">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="b372a-148">Azure CLI</span></span>
* <span data-ttu-id="b372a-149">Pour récupérer les entrées de journal, exécutez la commande **azure group log show** .</span><span class="sxs-lookup"><span data-stu-id="b372a-149">To retrieve log entries, you run the **azure group log show** command.</span></span>

  ```azurecli
  azure group log show ExampleGroup --json
  ```


## <a name="rest-api"></a><span data-ttu-id="b372a-150">API REST</span><span class="sxs-lookup"><span data-stu-id="b372a-150">REST API</span></span>
<span data-ttu-id="b372a-151">Les opérations REST à utiliser avec le journal d’activité font partie de l’ [API REST Insights](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="b372a-151">The REST operations for working with the activity log are part of the [Insights REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span> <span data-ttu-id="b372a-152">Pour récupérer les événements du journal d’activité, consultez [Liste des événements de gestion dans un abonnement](https://msdn.microsoft.com/library/azure/dn931934.aspx).</span><span class="sxs-lookup"><span data-stu-id="b372a-152">To retrieve activity log events, see [List the management events in a subscription](https://msdn.microsoft.com/library/azure/dn931934.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b372a-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b372a-153">Next steps</span></span>
* <span data-ttu-id="b372a-154">Les journaux d’activité Azure sont utilisables avec Power BI pour obtenir des informations plus détaillées sur les actions de votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="b372a-154">Azure Activity logs can be used with Power BI to gain greater insights about the actions in your subscription.</span></span> <span data-ttu-id="b372a-155">Consultez le billet de blog sur [l’affichage et l’analyse des journaux d’activité Azure dans Power BI](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/).</span><span class="sxs-lookup"><span data-stu-id="b372a-155">See [View and analyze Azure Activity Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/).</span></span>
* <span data-ttu-id="b372a-156">Pour en savoir plus sur la définition de stratégies de sécurité, consultez [Contrôle d’accès en fonction du rôle Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="b372a-156">To learn about setting security policies, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>
* <span data-ttu-id="b372a-157">Pour en savoir plus sur les commandes permettant d’afficher les opérations de déploiement, consultez [Voir les opérations de déploiement](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="b372a-157">To learn about the commands for viewing deployment operations, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="b372a-158">Pour savoir comment empêcher des suppressions sur une ressource pour tous les utilisateurs, consultez [Verrouiller des ressources avec Azure Resource Manager](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="b372a-158">To learn how to prevent deletions on a resource for all users, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

