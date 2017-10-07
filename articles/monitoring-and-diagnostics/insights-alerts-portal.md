---
title: aaaCreate des alertes pour les services Azure - portail Azure | Documents Microsoft
description: "Déclencher des messages électroniques, les notifications, les URL de sites Web d’appel (webhooks) ou automation lorsque les conditions hello spécifiées sont remplies."
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
ms.openlocfilehash: 78d862d25255cda9fdfe347329e908a471c39846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---azure-portal"></a><span data-ttu-id="5ad1f-103">Créer des alertes dans Azure Monitor pour les services Azure - Portail Azure</span><span class="sxs-lookup"><span data-stu-id="5ad1f-103">Create metric alerts in Azure Monitor for Azure services - Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5ad1f-104">Portail</span><span class="sxs-lookup"><span data-stu-id="5ad1f-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="5ad1f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5ad1f-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="5ad1f-106">INTERFACE DE LIGNE DE COMMANDE</span><span class="sxs-lookup"><span data-stu-id="5ad1f-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="5ad1f-107">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="5ad1f-107">Overview</span></span>
<span data-ttu-id="5ad1f-108">Cet article vous explique comment tooset des alertes de métrique Azure à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5ad1f-108">This article shows you how tooset up Azure metric alerts using hello Azure portal.</span></span>   

<span data-ttu-id="5ad1f-109">Vous pouvez recevoir une alerte en fonction de métriques de surveillance pour vos services Azure ou d'événements sur ces derniers.</span><span class="sxs-lookup"><span data-stu-id="5ad1f-109">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="5ad1f-110">**Valeurs de mesure** - hello déclencheurs d’alerte lorsque la valeur de hello d’une métrique spécifique dépasse un seuil que vous affectez dans les deux sens.</span><span class="sxs-lookup"><span data-stu-id="5ad1f-110">**Metric values** - hello alert triggers when hello value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="5ad1f-111">Autrement dit, elle déclenche à la fois lorsque hello condition est tout d’abord remplie et puis par la suite que lorsque la condition est n’est plus remplie.</span><span class="sxs-lookup"><span data-stu-id="5ad1f-111">That is, it triggers both when hello condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="5ad1f-112">**Événements du journal d’activité** : une alerte peut se déclencher sur *chaque* événement ou seulement quand un certain événement se produit.</span><span class="sxs-lookup"><span data-stu-id="5ad1f-112">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="5ad1f-113">toolearn plus d’informations sur les alertes de journal d’activité [cliquez ici](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="5ad1f-113">toolearn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="5ad1f-114">Vous pouvez configurer un hello métrique toodo alerte suivant lorsqu’il déclenche :</span><span class="sxs-lookup"><span data-stu-id="5ad1f-114">You can configure a metric alert toodo hello following when it triggers:</span></span>

* <span data-ttu-id="5ad1f-115">envoyer l’administrateur de service de messagerie des notifications toohello et coadministrateurs</span><span class="sxs-lookup"><span data-stu-id="5ad1f-115">send email notifications toohello service administrator and co-administrators</span></span>
* <span data-ttu-id="5ad1f-116">envoyer des e-mails tooadditional que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="5ad1f-116">send email tooadditional emails that you specify.</span></span>
* <span data-ttu-id="5ad1f-117">appeler un webhook</span><span class="sxs-lookup"><span data-stu-id="5ad1f-117">call a webhook</span></span>
* <span data-ttu-id="5ad1f-118">Démarrer l’exécution d’un runbook Azure (uniquement à partir de hello portail Azure)</span><span class="sxs-lookup"><span data-stu-id="5ad1f-118">start execution of an Azure runbook (only from hello Azure portal)</span></span>

<span data-ttu-id="5ad1f-119">Vous pouvez configurer et obtenir des informations sur les règles d’alerte de métrique via</span><span class="sxs-lookup"><span data-stu-id="5ad1f-119">You can configure and get information about metric alert rules using</span></span>

* [<span data-ttu-id="5ad1f-120">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="5ad1f-120">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="5ad1f-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5ad1f-121">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="5ad1f-122">interface de ligne de commande (CLI)</span><span class="sxs-lookup"><span data-stu-id="5ad1f-122">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="5ad1f-123">API REST Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="5ad1f-123">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

## <a name="create-an-alert-rule-on-a-metric-with-hello-azure-portal"></a><span data-ttu-id="5ad1f-124">Créer une règle d’alerte sur une mesure avec hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="5ad1f-124">Create an alert rule on a metric with hello Azure portal</span></span>
1. <span data-ttu-id="5ad1f-125">Bonjour [portal](https://portal.azure.com/), recherchez des ressources hello vous intéressez dans l’analyse et sélectionnez-le.</span><span class="sxs-lookup"><span data-stu-id="5ad1f-125">In hello [portal](https://portal.azure.com/), locate hello resource you are interested in monitoring and select it.</span></span>

2. <span data-ttu-id="5ad1f-126">Sélectionnez **alertes** ou **règles d’alerte** sous la section analyse de hello.</span><span class="sxs-lookup"><span data-stu-id="5ad1f-126">Select **Alerts** or **Alert rules** under hello MONITORING section.</span></span> <span data-ttu-id="5ad1f-127">icône et texte hello peuvent varier légèrement en fonction des ressources différentes.</span><span class="sxs-lookup"><span data-stu-id="5ad1f-127">hello text and icon may vary slightly for different resources.</span></span>  

    ![Surveillance](./media/insights-alerts-portal/AlertRulesButton.png)

3. <span data-ttu-id="5ad1f-129">Sélectionnez hello **ajouter une alerte** commande et renseignez les champs hello.</span><span class="sxs-lookup"><span data-stu-id="5ad1f-129">Select hello **Add alert** command and fill in hello fields.</span></span>

    ![Ajouter une alerte](./media/insights-alerts-portal/AddAlertOnlyParamsPage.png)

4. <span data-ttu-id="5ad1f-131">**Nommez** votre règle d’alerte, puis choisissez une **Description** qui indique également les adresses électroniques de notification.</span><span class="sxs-lookup"><span data-stu-id="5ad1f-131">**Name** your alert rule, and choose a **Description**, which also shows in notification emails.</span></span>

5. <span data-ttu-id="5ad1f-132">Sélectionnez hello **métrique** toomonitor de souhaité, puis choisissez un **Condition** et **seuil** valeur pour métrique de hello.</span><span class="sxs-lookup"><span data-stu-id="5ad1f-132">Select hello **Metric** you want toomonitor, then choose a **Condition** and **Threshold** value for hello metric.</span></span> <span data-ttu-id="5ad1f-133">Sélectionnez également l’option hello **période** de temps qui hello métrique règle doit être satisfaite avant de déclencheurs d’alerte hello.</span><span class="sxs-lookup"><span data-stu-id="5ad1f-133">Also chose hello **Period** of time that hello metric rule must be satisfied before hello alert triggers.</span></span> <span data-ttu-id="5ad1f-134">Par exemple, si vous utilisez hello point « PT5M », votre alerte recherche du processeur supérieure à 80 %, hello alerte se déclenche lorsque hello du processeur a été constamment ci-dessus 80 % pendant 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="5ad1f-134">So for example, if you use hello period "PT5M" and your alert looks for CPU above 80%, hello alert triggers when hello CPU has been consistently above 80% for 5 minutes.</span></span> <span data-ttu-id="5ad1f-135">Une fois le premier déclencheur de hello se produit, elle déclenche à nouveau lorsque hello UC reste inférieur à 80 % pendant 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="5ad1f-135">Once hello first trigger occurs, it again triggers when hello CPU stays below 80% for 5 minutes.</span></span> <span data-ttu-id="5ad1f-136">mesure du processeur de Hello se produit toutes les minutes.</span><span class="sxs-lookup"><span data-stu-id="5ad1f-136">hello CPU measurement occurs every 1 minute.</span></span>   

6. <span data-ttu-id="5ad1f-137">Vérifiez **propriétaires de messagerie...**  si vous souhaitez que les administrateurs et coadministrateurs toobe envoyé par courrier électronique lorsque hello alerte se déclenche.</span><span class="sxs-lookup"><span data-stu-id="5ad1f-137">Check **Email owners...** if you want administrators and co-administrators toobe emailed when hello alert fires.</span></span>

7. <span data-ttu-id="5ad1f-138">Si vous souhaitez que les messages électroniques supplémentaires tooreceive une notification lorsque hello l’alerte se déclenche, ajoutez-les dans hello **administrateur supplémentaire email(s)** champ.</span><span class="sxs-lookup"><span data-stu-id="5ad1f-138">If you want additional emails tooreceive a notification when hello alert fires, add them in hello **Additional Administrator email(s)** field.</span></span> <span data-ttu-id="5ad1f-139">Séparez les adresses e-mails par des points-virgules : *email@contoso.com;email2@contoso.com*</span><span class="sxs-lookup"><span data-stu-id="5ad1f-139">Separate multiple emails with semi-colons - *email@contoso.com;email2@contoso.com*</span></span>

8. <span data-ttu-id="5ad1f-140">Placez dans un URI valide Bonjour **Webhook** champ si vous souhaitez qu’il est appelé lorsque hello alerte se déclenche.</span><span class="sxs-lookup"><span data-stu-id="5ad1f-140">Put in a valid URI in hello **Webhook** field if you want it called when hello alert fires.</span></span>

9. <span data-ttu-id="5ad1f-141">Si vous utilisez Azure Automation, vous pouvez sélectionner un toobe Runbook exécuter lors du déclenche de l’alerte de hello.</span><span class="sxs-lookup"><span data-stu-id="5ad1f-141">If you use Azure Automation, you can select a Runbook toobe run when hello alert fires.</span></span>

10. <span data-ttu-id="5ad1f-142">Sélectionnez **OK** lorsque toocreate terminé hello alerte.</span><span class="sxs-lookup"><span data-stu-id="5ad1f-142">Select **OK** when done toocreate hello alert.</span></span>   

<span data-ttu-id="5ad1f-143">Dans quelques minutes, alerte de hello est actif et déclenche comme décrit précédemment.</span><span class="sxs-lookup"><span data-stu-id="5ad1f-143">Within a few minutes, hello alert is active and triggers as previously described.</span></span>

## <a name="managing-your-alerts"></a><span data-ttu-id="5ad1f-144">Gestion de vos alertes</span><span class="sxs-lookup"><span data-stu-id="5ad1f-144">Managing your alerts</span></span>
<span data-ttu-id="5ad1f-145">Une fois que vous avez créé une alerte, vous pouvez la sélectionner et :</span><span class="sxs-lookup"><span data-stu-id="5ad1f-145">Once you have created an alert, you can select it and:</span></span>

* <span data-ttu-id="5ad1f-146">Permet d’afficher un graphique indiquant de seuil de métrique hello et les valeurs actuelles hello hello jour précédent.</span><span class="sxs-lookup"><span data-stu-id="5ad1f-146">View a graph showing hello metric threshold and hello actual values from hello previous day.</span></span>
* <span data-ttu-id="5ad1f-147">La modifier ou la supprimer.</span><span class="sxs-lookup"><span data-stu-id="5ad1f-147">Edit or delete it.</span></span>
* <span data-ttu-id="5ad1f-148">**Désactiver** ou **activer** si vous souhaitez tootemporarily arrêter ou reprenez la réception de notifications qui.</span><span class="sxs-lookup"><span data-stu-id="5ad1f-148">**Disable** or **Enable** it if you want tootemporarily stop or resume receiving notifications for that alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ad1f-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5ad1f-149">Next steps</span></span>
* <span data-ttu-id="5ad1f-150">[Obtenir une vue d’ensemble de la surveillance Azure](monitoring-overview.md) y compris les types d’informations, vous pouvez collecter et analyser hello.</span><span class="sxs-lookup"><span data-stu-id="5ad1f-150">[Get an overview of Azure monitoring](monitoring-overview.md) including hello types of information you can collect and monitor.</span></span>
* <span data-ttu-id="5ad1f-151">Découvrez plus en détail la [configuration des webhooks dans les alertes](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="5ad1f-151">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="5ad1f-152">Découvrez plus d’informations sur la [configuration des alertes sur les événements de journal d’activité](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="5ad1f-152">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="5ad1f-153">Découvrez plus en détails les [runbooks Azure Automation](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="5ad1f-153">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="5ad1f-154">Consultez une [vue d’ensemble des journaux de diagnostic](monitoring-overview-of-diagnostic-logs.md) et collecter des métriques détaillées à fréquence élevée sur votre service.</span><span class="sxs-lookup"><span data-stu-id="5ad1f-154">Get an [overview of diagnostic logs](monitoring-overview-of-diagnostic-logs.md) and collect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="5ad1f-155">Obtenir un [vue d’ensemble de la collecte de métriques](insights-how-to-customize-monitoring.md) toomake que votre service est disponible et réactive.</span><span class="sxs-lookup"><span data-stu-id="5ad1f-155">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>
