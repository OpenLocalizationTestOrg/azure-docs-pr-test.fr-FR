---
title: "Créer des alertes pour les services Azure - Portail Azure | Microsoft Docs"
description: "Déclenchez des e-mails et des notifications, appelez des URL de sites web (webhooks) ou déclenchez une automatisation lorsque les conditions spécifiées sont remplies."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: f7457655-ced6-4102-a9dd-7ddf2265c0e2
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/23/2016
ms.author: robb
ms.openlocfilehash: 745a9c016bd037f1051025a2c5a468c3935e4550
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---azure-portal"></a><span data-ttu-id="1f867-103">Créer des alertes dans Azure Monitor pour les services Azure - Portail Azure</span><span class="sxs-lookup"><span data-stu-id="1f867-103">Create metric alerts in Azure Monitor for Azure services - Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1f867-104">Portail</span><span class="sxs-lookup"><span data-stu-id="1f867-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="1f867-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1f867-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="1f867-106">INTERFACE DE LIGNE DE COMMANDE</span><span class="sxs-lookup"><span data-stu-id="1f867-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="1f867-107">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="1f867-107">Overview</span></span>
<span data-ttu-id="1f867-108">Cet article vous montre comment configurer des alertes de métrique Azure avec le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1f867-108">This article shows you how to set up Azure metric alerts using the Azure portal.</span></span>   

<span data-ttu-id="1f867-109">Vous pouvez recevoir une alerte en fonction de métriques de surveillance pour vos services Azure ou d'événements sur ces derniers.</span><span class="sxs-lookup"><span data-stu-id="1f867-109">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="1f867-110">**Valeurs de métriques** : l’alerte se déclenche lorsque la valeur d’une métrique spécifiée dépasse un seuil que vous affectez dans un des deux sens.</span><span class="sxs-lookup"><span data-stu-id="1f867-110">**Metric values** - The alert triggers when the value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="1f867-111">C’est-à-dire que le déclenchement se fait à la fois lorsque la condition est remplie et par la suite une fois que la condition n’est plus remplie.</span><span class="sxs-lookup"><span data-stu-id="1f867-111">That is, it triggers both when the condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="1f867-112">**Événements du journal d’activité** : une alerte peut se déclencher sur *chaque* événement ou seulement quand un certain événement se produit.</span><span class="sxs-lookup"><span data-stu-id="1f867-112">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="1f867-113">Pour plus d’informations sur les alertes du journal d’activité, [cliquez ici](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="1f867-113">To learn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="1f867-114">Vous pouvez configurer une alerte de métrique pour effectuer les opérations suivantes lors de son déclenchement :</span><span class="sxs-lookup"><span data-stu-id="1f867-114">You can configure a metric alert to do the following when it triggers:</span></span>

* <span data-ttu-id="1f867-115">envoyer des notifications par courrier électronique à l’administrateur du service et aux coadministrateurs</span><span class="sxs-lookup"><span data-stu-id="1f867-115">send email notifications to the service administrator and co-administrators</span></span>
* <span data-ttu-id="1f867-116">envoyer un courrier électronique à d’autres adresses que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="1f867-116">send email to additional emails that you specify.</span></span>
* <span data-ttu-id="1f867-117">appeler un webhook</span><span class="sxs-lookup"><span data-stu-id="1f867-117">call a webhook</span></span>
* <span data-ttu-id="1f867-118">démarrer l’exécution d’un runbook Azure (uniquement à partir du Portail Azure)</span><span class="sxs-lookup"><span data-stu-id="1f867-118">start execution of an Azure runbook (only from the Azure portal)</span></span>

<span data-ttu-id="1f867-119">Vous pouvez configurer et obtenir des informations sur les règles d’alerte de métrique via</span><span class="sxs-lookup"><span data-stu-id="1f867-119">You can configure and get information about metric alert rules using</span></span>

* [<span data-ttu-id="1f867-120">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="1f867-120">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="1f867-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1f867-121">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="1f867-122">interface de ligne de commande (CLI)</span><span class="sxs-lookup"><span data-stu-id="1f867-122">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="1f867-123">API REST Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="1f867-123">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

## <a name="create-an-alert-rule-on-a-metric-with-the-azure-portal"></a><span data-ttu-id="1f867-124">Créer une règle d’alerte sur une métrique avec le Portail Azure</span><span class="sxs-lookup"><span data-stu-id="1f867-124">Create an alert rule on a metric with the Azure portal</span></span>
1. <span data-ttu-id="1f867-125">Sur le [portail](https://portal.azure.com/), localisez la ressource que vous souhaitez surveiller et sélectionnez-la.</span><span class="sxs-lookup"><span data-stu-id="1f867-125">In the [portal](https://portal.azure.com/), locate the resource you are interested in monitoring and select it.</span></span>

2. <span data-ttu-id="1f867-126">Sélectionnez **Alertes** ou **Règles d’alerte** dans la section SURVEILLANCE.</span><span class="sxs-lookup"><span data-stu-id="1f867-126">Select **Alerts** or **Alert rules** under the MONITORING section.</span></span> <span data-ttu-id="1f867-127">Le texte et l’icône peuvent varier légèrement pour les différentes ressources.</span><span class="sxs-lookup"><span data-stu-id="1f867-127">The text and icon may vary slightly for different resources.</span></span>  

    ![Analyse](./media/insights-alerts-portal/AlertRulesButton.png)

3. <span data-ttu-id="1f867-129">Sélectionnez la commande **Ajouter une alerte** et renseignez les champs.</span><span class="sxs-lookup"><span data-stu-id="1f867-129">Select the **Add alert** command and fill in the fields.</span></span>

    ![Ajouter une alerte](./media/insights-alerts-portal/AddAlertOnlyParamsPage.png)

4. <span data-ttu-id="1f867-131">**Nommez** votre règle d’alerte, puis choisissez une **Description** qui indique également les adresses électroniques de notification.</span><span class="sxs-lookup"><span data-stu-id="1f867-131">**Name** your alert rule, and choose a **Description**, which also shows in notification emails.</span></span>

5. <span data-ttu-id="1f867-132">Sélectionnez la **Métrique** que vous souhaitez surveiller, puis choisissez une **Condition** et une valeur de **Seuil** pour la métrique.</span><span class="sxs-lookup"><span data-stu-id="1f867-132">Select the **Metric** you want to monitor, then choose a **Condition** and **Threshold** value for the metric.</span></span> <span data-ttu-id="1f867-133">Choisissez également la **Période** de temps pendant laquelle la règle de métrique doit être satisfaite pour que l’alerte se déclenche.</span><span class="sxs-lookup"><span data-stu-id="1f867-133">Also chose the **Period** of time that the metric rule must be satisfied before the alert triggers.</span></span> <span data-ttu-id="1f867-134">Par exemple, si vous utilisez la période « PT5M » et que vous alerte recherche l’UC au-dessus de 80 %, elle se déclenche quand l’UC a été constamment au-dessus de 80 % pendant cinq minutes.</span><span class="sxs-lookup"><span data-stu-id="1f867-134">So for example, if you use the period "PT5M" and your alert looks for CPU above 80%, the alert triggers when the CPU has been consistently above 80% for 5 minutes.</span></span> <span data-ttu-id="1f867-135">Après le premier déclenchement, elle se déclenche à nouveau lorsque l’UC reste au-dessous de 80 % pendant cinq minutes.</span><span class="sxs-lookup"><span data-stu-id="1f867-135">Once the first trigger occurs, it again triggers when the CPU stays below 80% for 5 minutes.</span></span> <span data-ttu-id="1f867-136">La mesure de l’UC se produit toutes les minutes.</span><span class="sxs-lookup"><span data-stu-id="1f867-136">The CPU measurement occurs every 1 minute.</span></span>   

6. <span data-ttu-id="1f867-137">Cochez **Propriétaires de messagerie...** si vous souhaitez que les administrateurs et les coadministrateurs reçoivent un courrier électronique lorsque l’alerte se déclenche.</span><span class="sxs-lookup"><span data-stu-id="1f867-137">Check **Email owners...** if you want administrators and co-administrators to be emailed when the alert fires.</span></span>

7. <span data-ttu-id="1f867-138">Si vous souhaitez que d’autres adresses électroniques reçoivent une notification lorsque l’alerte se déclenche, ajoutez-les dans le champ **Adresse(s) de messagerie d’administrateur(s) supplémentaire(s)** .</span><span class="sxs-lookup"><span data-stu-id="1f867-138">If you want additional emails to receive a notification when the alert fires, add them in the **Additional Administrator email(s)** field.</span></span> <span data-ttu-id="1f867-139">Séparez les adresses e-mails par des points-virgules : *email@contoso.com;email2@contoso.com*</span><span class="sxs-lookup"><span data-stu-id="1f867-139">Separate multiple emails with semi-colons - *email@contoso.com;email2@contoso.com*</span></span>

8. <span data-ttu-id="1f867-140">Insérez un URI valide dans le champ **Webhook** si vous souhaitez qu’il soit appelé lorsque l’alerte se déclenche.</span><span class="sxs-lookup"><span data-stu-id="1f867-140">Put in a valid URI in the **Webhook** field if you want it called when the alert fires.</span></span>

9. <span data-ttu-id="1f867-141">Si vous utilisez Azure Automation, vous pouvez sélectionner un Runbook à exécuter lorsque l’alerte se déclenche.</span><span class="sxs-lookup"><span data-stu-id="1f867-141">If you use Azure Automation, you can select a Runbook to be run when the alert fires.</span></span>

10. <span data-ttu-id="1f867-142">Quand vous avez terminé, sélectionnez **OK** pour créer l’alerte.</span><span class="sxs-lookup"><span data-stu-id="1f867-142">Select **OK** when done to create the alert.</span></span>   

<span data-ttu-id="1f867-143">Après quelques minutes, l’alerte est active et se déclenche comme décrit précédemment.</span><span class="sxs-lookup"><span data-stu-id="1f867-143">Within a few minutes, the alert is active and triggers as previously described.</span></span>

## <a name="managing-your-alerts"></a><span data-ttu-id="1f867-144">Gestion de vos alertes</span><span class="sxs-lookup"><span data-stu-id="1f867-144">Managing your alerts</span></span>
<span data-ttu-id="1f867-145">Une fois que vous avez créé une alerte, vous pouvez la sélectionner et :</span><span class="sxs-lookup"><span data-stu-id="1f867-145">Once you have created an alert, you can select it and:</span></span>

* <span data-ttu-id="1f867-146">Afficher un graphique indiquant le seuil de la métrique et les valeurs réelles du jour précédent.</span><span class="sxs-lookup"><span data-stu-id="1f867-146">View a graph showing the metric threshold and the actual values from the previous day.</span></span>
* <span data-ttu-id="1f867-147">La modifier ou la supprimer.</span><span class="sxs-lookup"><span data-stu-id="1f867-147">Edit or delete it.</span></span>
* <span data-ttu-id="1f867-148">La **Désactiver** ou l’**Activer** si vous voulez arrêter temporairement ou reprendre l’envoi de notifications pour cette alerte.</span><span class="sxs-lookup"><span data-stu-id="1f867-148">**Disable** or **Enable** it if you want to temporarily stop or resume receiving notifications for that alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f867-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1f867-149">Next steps</span></span>
* <span data-ttu-id="1f867-150">[Consultez une vue d’ensemble de la surveillance Azure](monitoring-overview.md) , notamment les types d’informations que vous pouvez collecter et surveiller.</span><span class="sxs-lookup"><span data-stu-id="1f867-150">[Get an overview of Azure monitoring](monitoring-overview.md) including the types of information you can collect and monitor.</span></span>
* <span data-ttu-id="1f867-151">Découvrez plus en détail la [configuration des webhooks dans les alertes](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="1f867-151">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="1f867-152">Découvrez plus d’informations sur la [configuration des alertes sur les événements de journal d’activité](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="1f867-152">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="1f867-153">Découvrez plus en détails les [runbooks Azure Automation](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="1f867-153">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="1f867-154">Consultez une [vue d’ensemble des journaux de diagnostic](monitoring-overview-of-diagnostic-logs.md) et collecter des métriques détaillées à fréquence élevée sur votre service.</span><span class="sxs-lookup"><span data-stu-id="1f867-154">Get an [overview of diagnostic logs](monitoring-overview-of-diagnostic-logs.md) and collect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="1f867-155">Consultez une [vue d’ensemble de la collecte des métriques](insights-how-to-customize-monitoring.md) pour vous assurer que votre service est disponible et réactif.</span><span class="sxs-lookup"><span data-stu-id="1f867-155">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span></span>
