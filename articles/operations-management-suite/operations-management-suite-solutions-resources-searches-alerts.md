---
title: aaaSaved recherches et les alertes dans les solutions OMS | Documents Microsoft
description: "Solutions dans OMS inclut généralement les recherches enregistrées dans Analytique de journal tooanalyze collectées par les solutions hello.  Ils peuvent également définir l’utilisateur d’alertes toonotify hello ou agir automatiquement en problème critique tooa de réponse.  Cet article décrit comment toodefine Analytique de journal enregistrées recherches et les alertes dans un modèle ARM afin qu’ils peuvent être inclus dans les solutions de gestion."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 93d7c5bbf061473833ca6c0a8e4d8e10d923f3ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-log-analytics-saved-searches-and-alerts-toooms-management-solution-preview"></a><span data-ttu-id="fc423-105">Ajout d’Analytique de journal enregistré tooOMS recherches et les alertes solution de gestion (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="fc423-105">Adding Log Analytics saved searches and alerts tooOMS management solution (Preview)</span></span>

> [!NOTE]
> <span data-ttu-id="fc423-106">Il s’agit d’une documentation préliminaire pour la création de solutions de gestion dans OMS qui sont actuellement en préversion.</span><span class="sxs-lookup"><span data-stu-id="fc423-106">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="fc423-107">N’importe quel schéma décrit ci-dessous est un objet toochange.</span><span class="sxs-lookup"><span data-stu-id="fc423-107">Any schema described below is subject toochange.</span></span>   


<span data-ttu-id="fc423-108">[Solutions de gestion OMS](operations-management-suite-solutions.md) inclut généralement [recherches enregistrées](../log-analytics/log-analytics-log-searches.md) dans Analytique de journal tooanalyze collectées par les solutions hello.</span><span class="sxs-lookup"><span data-stu-id="fc423-108">[Management solutions in OMS](operations-management-suite-solutions.md) will typically include [saved searches](../log-analytics/log-analytics-log-searches.md) in Log Analytics tooanalyze data collected by hello solution.</span></span>  <span data-ttu-id="fc423-109">Ils peuvent également définir [alertes](../log-analytics/log-analytics-alerts.md) toonotify hello utilisateur ou agir automatiquement en problème critique tooa de réponse.</span><span class="sxs-lookup"><span data-stu-id="fc423-109">They may also define [alerts](../log-analytics/log-analytics-alerts.md) toonotify hello user or automatically take action in response tooa critical issue.</span></span>  <span data-ttu-id="fc423-110">Cet article décrit comment toodefine Analytique de journal enregistrées recherches et les alertes dans un [modèle de gestion des ressources](../resource-manager-template-walkthrough.md) afin qu’ils peuvent être inclus dans [solutions de gestion](operations-management-suite-solutions-creating.md).</span><span class="sxs-lookup"><span data-stu-id="fc423-110">This article describes how toodefine Log Analytics saved searches and alerts in a [Resource Management template](../resource-manager-template-walkthrough.md) so they can be included in [management solutions](operations-management-suite-solutions-creating.md).</span></span>

> [!NOTE]
> <span data-ttu-id="fc423-111">Hello exemples dans cet article utilisent les paramètres et les variables qui sont deux solutions toomanagement requises ou courantes et décrites dans [création de solutions de gestion Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="fc423-111">hello samples in this article use parameters and variables that are either required or common toomanagement solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="fc423-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="fc423-112">Prerequisites</span></span>
<span data-ttu-id="fc423-113">Cet article suppose que vous êtes déjà familiarisé avec le trop[créer une solution de gestion](operations-management-suite-solutions-creating.md) et la structure hello d’un [modèle ARM](../resource-group-authoring-templates.md) et le fichier de solution.</span><span class="sxs-lookup"><span data-stu-id="fc423-113">This article assumes that you're already familiar with how too[create a management solution](operations-management-suite-solutions-creating.md) and hello structure of an [ARM template](../resource-group-authoring-templates.md) and solution file.</span></span>


## <a name="log-analytics-workspace"></a><span data-ttu-id="fc423-114">Espace de travail Log Analytics</span><span class="sxs-lookup"><span data-stu-id="fc423-114">Log Analytics Workspace</span></span>
<span data-ttu-id="fc423-115">Toutes les ressources dans Log Analytics sont contenues dans un [espace de travail](../log-analytics/log-analytics-manage-access.md).</span><span class="sxs-lookup"><span data-stu-id="fc423-115">All resources in Log Analytics are contained in a [workspace](../log-analytics/log-analytics-manage-access.md).</span></span>  <span data-ttu-id="fc423-116">Comme décrit dans [OMS espace de travail et le compte Automation](operations-management-suite-solutions.md#oms-workspace-and-automation-account) espace de travail hello n’est pas inclus dans la solution de gestion hello mais doit exister pour que la solution de hello est installée.</span><span class="sxs-lookup"><span data-stu-id="fc423-116">As described in [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) hello workspace isn't included in hello management solution but must exist before hello solution is installed.</span></span>  <span data-ttu-id="fc423-117">Si elle n’est pas disponible, hello solution installation échouera.</span><span class="sxs-lookup"><span data-stu-id="fc423-117">If it isn't available, then hello solution install will fail.</span></span>

<span data-ttu-id="fc423-118">nom Hello d’espace de travail hello est nom hello de chaque ressource Analytique de journal.</span><span class="sxs-lookup"><span data-stu-id="fc423-118">hello name of hello workspace is in hello name of each Log Analytics resource.</span></span>  <span data-ttu-id="fc423-119">Cette opération est effectuée dans la solution hello avec hello **espace de travail** paramètre comme hello d’une ressource savedsearch l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="fc423-119">This is done in hello solution with hello **workspace** parameter as in hello following example of a savedsearch resource.</span></span>

    "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearchId'))]"


## <a name="saved-searches"></a><span data-ttu-id="fc423-120">Recherches enregistrées</span><span class="sxs-lookup"><span data-stu-id="fc423-120">Saved Searches</span></span>
<span data-ttu-id="fc423-121">Inclure [recherches enregistrées](../log-analytics/log-analytics-log-searches.md) dans une solution tooallow utilisateurs tooquery de données collecté par votre solution.</span><span class="sxs-lookup"><span data-stu-id="fc423-121">Include [saved searches](../log-analytics/log-analytics-log-searches.md) in a solution tooallow users tooquery data collected by your solution.</span></span>  <span data-ttu-id="fc423-122">Recherches enregistrées seront affiche sous **favoris** dans portail OMS : hello et **recherches enregistrées** Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="fc423-122">Saved searches will appear under **Favorites** in hello OMS portal and **Saved Searches** in hello Azure portal .</span></span>  <span data-ttu-id="fc423-123">Une recherche enregistrée est également requise pour chaque alerte.</span><span class="sxs-lookup"><span data-stu-id="fc423-123">A saved search is also required for each alert.</span></span>   

<span data-ttu-id="fc423-124">[Recherche de journal Analytique enregistrée](../log-analytics/log-analytics-log-searches.md) ressources ont un type de `Microsoft.OperationalInsights/workspaces/savedSearches` et avoir hello suivant la structure.</span><span class="sxs-lookup"><span data-stu-id="fc423-124">[Log Analytics saved search](../log-analytics/log-analytics-log-searches.md) resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches` and have hello following structure.</span></span>  <span data-ttu-id="fc423-125">Cela inclut des variables et des paramètres courants afin que vous pouvez copier et coller cet extrait de code dans votre fichier de solution et modifier les noms de paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="fc423-125">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
        ],
        "tags": { },
        "properties": {
            "etag": "*",
            "query": "[variables('SavedSearch').Query]",
            "displayName": "[variables('SavedSearch').DisplayName]",
            "category": "[variables('SavedSearch').Category]"
        }
    }



<span data-ttu-id="fc423-126">Chacune des propriétés hello d’une recherche enregistrée sont décrits dans hello tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="fc423-126">Each of hello properties of a saved search are described in hello following table.</span></span> 

| <span data-ttu-id="fc423-127">Propriété</span><span class="sxs-lookup"><span data-stu-id="fc423-127">Property</span></span> | <span data-ttu-id="fc423-128">Description</span><span class="sxs-lookup"><span data-stu-id="fc423-128">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="fc423-129">category</span><span class="sxs-lookup"><span data-stu-id="fc423-129">category</span></span> | <span data-ttu-id="fc423-130">catégorie Hello pour la recherche enregistrée hello.</span><span class="sxs-lookup"><span data-stu-id="fc423-130">hello category for hello saved search.</span></span>  <span data-ttu-id="fc423-131">Les recherches enregistrement Bonjour même solution souvent partagent une même catégorie afin qu’ils sont regroupés dans la console de hello.</span><span class="sxs-lookup"><span data-stu-id="fc423-131">Any saved searches in hello same solution will often share a single category so they are grouped together in hello console.</span></span> |
| <span data-ttu-id="fc423-132">displayname</span><span class="sxs-lookup"><span data-stu-id="fc423-132">displayname</span></span> | <span data-ttu-id="fc423-133">Toodisplay de nom pour hello recherche enregistrée dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="fc423-133">Name toodisplay for hello saved search in hello portal.</span></span> |
| <span data-ttu-id="fc423-134">query</span><span class="sxs-lookup"><span data-stu-id="fc423-134">query</span></span> | <span data-ttu-id="fc423-135">Toorun de la requête.</span><span class="sxs-lookup"><span data-stu-id="fc423-135">Query toorun.</span></span> |

> [!NOTE]
> <span data-ttu-id="fc423-136">Vous devrez peut-être toouse des caractères d’échappement dans la requête de hello si elle inclut des caractères qui peuvent être interprétés en tant que JSON.</span><span class="sxs-lookup"><span data-stu-id="fc423-136">You may need toouse escape characters in hello query if it includes characters that could be interpreted as JSON.</span></span>  <span data-ttu-id="fc423-137">Par exemple, si votre requête a été **Type : AzureActivity OperationName:"Microsoft.Compute/virtualMachines/write »**, il doit être écrit dans le fichier de solution hello en tant que **OperationName de Type : AzureActivity :\" Microsoft.Compute/virtualMachines/write\"**.</span><span class="sxs-lookup"><span data-stu-id="fc423-137">For example, if your query was **Type:AzureActivity OperationName:"Microsoft.Compute/virtualMachines/write"**, it should be written in hello solution file as **Type:AzureActivity OperationName:\"Microsoft.Compute/virtualMachines/write\"**.</span></span>

## <a name="alerts"></a><span data-ttu-id="fc423-138">Alertes</span><span class="sxs-lookup"><span data-stu-id="fc423-138">Alerts</span></span>
<span data-ttu-id="fc423-139">Les [alertes Log Analytics](../log-analytics/log-analytics-alerts.md) sont créées par le biais de règles d’alerte exécutant une recherche enregistrée à intervalles réguliers.</span><span class="sxs-lookup"><span data-stu-id="fc423-139">[Log Analytics alerts](../log-analytics/log-analytics-alerts.md) are created by alert rules that run a saved search on a regular interval.</span></span>  <span data-ttu-id="fc423-140">Si des résultats de requête de hello hello correspondent aux critères spécifiés, un enregistrement d’alerte est créé et une ou plusieurs actions sont exécutées.</span><span class="sxs-lookup"><span data-stu-id="fc423-140">If hello results of hello query match specified criteria, an alert record is created and one or more actions are run.</span></span>  

<span data-ttu-id="fc423-141">Règles d’alerte dans une solution de gestion sont constituées de hello suivant trois différentes ressources.</span><span class="sxs-lookup"><span data-stu-id="fc423-141">Alert rules in a management solution are made up of hello following three different resources.</span></span>

- <span data-ttu-id="fc423-142">**Recherche enregistrée.**</span><span class="sxs-lookup"><span data-stu-id="fc423-142">**Saved search.**</span></span>  <span data-ttu-id="fc423-143">Définit la recherche de journal hello qui est exécutée.</span><span class="sxs-lookup"><span data-stu-id="fc423-143">Defines hello log search that will be run.</span></span>  <span data-ttu-id="fc423-144">Plusieurs règles d’alerte peuvent partager une même recherche enregistrée.</span><span class="sxs-lookup"><span data-stu-id="fc423-144">Multiple alert rules can share a single saved search.</span></span>
- <span data-ttu-id="fc423-145">**Planification.**</span><span class="sxs-lookup"><span data-stu-id="fc423-145">**Schedule.**</span></span>  <span data-ttu-id="fc423-146">Définit la fréquence à laquelle hello recherche de journal sera exécuté.</span><span class="sxs-lookup"><span data-stu-id="fc423-146">Defines how often hello log search will be run.</span></span>  <span data-ttu-id="fc423-147">Chaque règle d’alerte est associée à une planification unique.</span><span class="sxs-lookup"><span data-stu-id="fc423-147">Each alert rule will have one and only one schedule.</span></span>
- <span data-ttu-id="fc423-148">**Action d’alerte.**</span><span class="sxs-lookup"><span data-stu-id="fc423-148">**Alert action.**</span></span>  <span data-ttu-id="fc423-149">Chaque règle d’alerte aura une ressource d’action avec un type de **alerte** qui définit les détails de hello d’alerte de hello telles que les critères de hello lorsqu’un enregistrement d’alerte sera créé puis hello la gravité de l’alerte.</span><span class="sxs-lookup"><span data-stu-id="fc423-149">Each alert rule will have one action resource with a type of **Alert** that defines hello details of hello alert such as hello criteria for when an alert record will be created and hello alert's severity.</span></span>  <span data-ttu-id="fc423-150">ressource d’action Hello sera éventuellement définir une réponse de la messagerie et le runbook.</span><span class="sxs-lookup"><span data-stu-id="fc423-150">hello action resource will optionally define a mail and runbook response.</span></span>
- <span data-ttu-id="fc423-151">**Action webhook (facultative).**</span><span class="sxs-lookup"><span data-stu-id="fc423-151">**Webhook action (optional).**</span></span>  <span data-ttu-id="fc423-152">Si une règle d’alerte hello appelle un webhook, il requiert une ressource d’une action avec un type de **Webhook**.</span><span class="sxs-lookup"><span data-stu-id="fc423-152">If hello alert rule will call a webhook, then it requires an additional action resource with a type of **Webhook**.</span></span>    

<span data-ttu-id="fc423-153">Les ressources de recherche enregistrée sont décrites ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="fc423-153">Saved search resources are described above.</span></span>  <span data-ttu-id="fc423-154">Hello autres ressources sont décrits ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="fc423-154">hello other resources are described below.</span></span>


### <a name="schedule-resource"></a><span data-ttu-id="fc423-155">Ressource de planification</span><span class="sxs-lookup"><span data-stu-id="fc423-155">Schedule resource</span></span>

<span data-ttu-id="fc423-156">Une recherche enregistrée peut avoir une ou plusieurs planifications, chacune d’entre elles représentant une règle d’alerte distincte.</span><span class="sxs-lookup"><span data-stu-id="fc423-156">A saved search can have one or more schedules with each schedule representing a separate alert rule.</span></span> <span data-ttu-id="fc423-157">Hello planification définit la fréquence à laquelle hello recherche est exécutée et hello intervalle de temps sur le hello les données sont récupérées.</span><span class="sxs-lookup"><span data-stu-id="fc423-157">hello schedule defines how often hello search is run and hello time interval over which hello data is retrieved.</span></span>  <span data-ttu-id="fc423-158">Planifier des ressources ont un type de `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` et avoir hello suivant la structure.</span><span class="sxs-lookup"><span data-stu-id="fc423-158">Schedule resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` and have hello following structure.</span></span> <span data-ttu-id="fc423-159">Cela inclut des variables et des paramètres courants afin que vous pouvez copier et coller cet extrait de code dans votre fichier de solution et modifier les noms de paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="fc423-159">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 


    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name)]"
        ],
        "properties": {
            "etag": "*",
            "interval": "[variables('Schedule').Interval]",
            "queryTimeSpan": "[variables('Schedule').TimeSpan]",
            "enabled": "[variables('Schedule').Enabled]"
        }
    }



<span data-ttu-id="fc423-160">Décrit les propriétés de Hello pour planifier des ressources Bonjour tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="fc423-160">hello properties for schedule resources are described in hello following table.</span></span>

| <span data-ttu-id="fc423-161">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="fc423-161">Element name</span></span> | <span data-ttu-id="fc423-162">Requis</span><span class="sxs-lookup"><span data-stu-id="fc423-162">Required</span></span> | <span data-ttu-id="fc423-163">Description</span><span class="sxs-lookup"><span data-stu-id="fc423-163">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="fc423-164">Activé</span><span class="sxs-lookup"><span data-stu-id="fc423-164">enabled</span></span>       | <span data-ttu-id="fc423-165">Oui</span><span class="sxs-lookup"><span data-stu-id="fc423-165">Yes</span></span> | <span data-ttu-id="fc423-166">Spécifie si l’alerte de hello est activée lors de sa création.</span><span class="sxs-lookup"><span data-stu-id="fc423-166">Specifies whether hello alert is enabled when it's created.</span></span> |
| <span data-ttu-id="fc423-167">interval</span><span class="sxs-lookup"><span data-stu-id="fc423-167">interval</span></span>      | <span data-ttu-id="fc423-168">Oui</span><span class="sxs-lookup"><span data-stu-id="fc423-168">Yes</span></span> | <span data-ttu-id="fc423-169">La fréquence à laquelle hello requête s’exécute en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="fc423-169">How often hello query runs in minutes.</span></span> |
| <span data-ttu-id="fc423-170">queryTimeSpan</span><span class="sxs-lookup"><span data-stu-id="fc423-170">queryTimeSpan</span></span> | <span data-ttu-id="fc423-171">Oui</span><span class="sxs-lookup"><span data-stu-id="fc423-171">Yes</span></span> | <span data-ttu-id="fc423-172">Durée en minutes sur les résultats tooevaluate.</span><span class="sxs-lookup"><span data-stu-id="fc423-172">Length of time in minutes over which tooevaluate results.</span></span> |

<span data-ttu-id="fc423-173">ressource de planification Hello doit s’appuyer sur hello recherche enregistrée afin qu’elle est créée avant la planification de hello.</span><span class="sxs-lookup"><span data-stu-id="fc423-173">hello schedule resource should depend on hello saved search so that it's created before hello schedule.</span></span>


### <a name="actions"></a><span data-ttu-id="fc423-174">Actions</span><span class="sxs-lookup"><span data-stu-id="fc423-174">Actions</span></span>
<span data-ttu-id="fc423-175">Il existe deux types de ressource d’action spécifié par hello **Type** propriété.</span><span class="sxs-lookup"><span data-stu-id="fc423-175">There are two types of action resource specified by hello **Type** property.</span></span>  <span data-ttu-id="fc423-176">Une planification requiert un **alerte** action qui définit les détails de hello de règle d’alerte hello et les actions prises lors de la création d’une alerte.</span><span class="sxs-lookup"><span data-stu-id="fc423-176">A schedule requires one **Alert** action which defines hello details of hello alert rule and what actions are taken when an alert is created.</span></span>  <span data-ttu-id="fc423-177">Il peut également inclure un **Webhook** action si un webhook doit être appelé à partir de l’alerte de hello.</span><span class="sxs-lookup"><span data-stu-id="fc423-177">It may also include a **Webhook** action if a webhook should be called from hello alert.</span></span>  

<span data-ttu-id="fc423-178">Les ressources d’action ont un type `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.</span><span class="sxs-lookup"><span data-stu-id="fc423-178">Action resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.</span></span>  

#### <a name="alert-actions"></a><span data-ttu-id="fc423-179">Actions d’alerte</span><span class="sxs-lookup"><span data-stu-id="fc423-179">Alert actions</span></span>

<span data-ttu-id="fc423-180">Chaque planification est associée à une action **Alert**.</span><span class="sxs-lookup"><span data-stu-id="fc423-180">Every schedule will have one **Alert** action.</span></span>  <span data-ttu-id="fc423-181">Définit les détails de hello d’alerte de hello et, éventuellement, les actions de notification et de correction.</span><span class="sxs-lookup"><span data-stu-id="fc423-181">This defines hello details of hello alert and optionally notification and remediation actions.</span></span>  <span data-ttu-id="fc423-182">Une notification envoie un e-mail tooone ou de plusieurs adresses.</span><span class="sxs-lookup"><span data-stu-id="fc423-182">A notification sends an email tooone or more addresses.</span></span>  <span data-ttu-id="fc423-183">Une mise à jour démarre un runbook problème de Azure Automation tooattempt tooremediate hello détecté.</span><span class="sxs-lookup"><span data-stu-id="fc423-183">A remediation starts a runbook in Azure Automation tooattempt tooremediate hello detected issue.</span></span>

<span data-ttu-id="fc423-184">Actions d’alerte ont hello suivant la structure.</span><span class="sxs-lookup"><span data-stu-id="fc423-184">Alert actions have hello following structure.</span></span>  <span data-ttu-id="fc423-185">Cela inclut des variables et des paramètres courants afin que vous pouvez copier et coller cet extrait de code dans votre fichier de solution et modifier les noms de paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="fc423-185">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 



    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name, '/', variables('Alert').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name, '/schedules/', variables('Schedule').Name)]"
        ],
        "properties": {
            "etag": "*",
            "type": "Alert",
            "name": "[variables('Alert').Name]",
            "description": "[variables('Alert').Description]",
            "severity": "[variables('Alert').Severity]",
            "threshold": {
                "operator": "[variables('Alert').Threshold.Operator]",
                "value": "[variables('Alert').Threshold.Value]",
                "metricsTrigger": {
                    "triggerCondition": "[variables('Alert').Threshold.Trigger.Condition]",
                    "operator": "[variables('Alert').Trigger.Operator]",
                    "value": "[variables('Alert').Trigger.Value]"
                },
            },
            "emailNotification": {
                "recipients": [
                    "[variables('Alert').Recipients]"
                ],
                "subject": "[variables('Alert').Subject]"
            },
            "remediation": {
                "runbookName": "[variables('Alert').Remedition.RunbookName]",
                "webhookUri": "[variables('Alert').Remedition.WebhookUri]"
            }
        }
    }

<span data-ttu-id="fc423-186">propriétés Hello pour les ressources de l’action d’alerte sont décrits dans les tableaux suivants de hello.</span><span class="sxs-lookup"><span data-stu-id="fc423-186">hello properties for Alert action resources are described in hello following tables.</span></span>

| <span data-ttu-id="fc423-187">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="fc423-187">Element name</span></span> | <span data-ttu-id="fc423-188">Requis</span><span class="sxs-lookup"><span data-stu-id="fc423-188">Required</span></span> | <span data-ttu-id="fc423-189">Description</span><span class="sxs-lookup"><span data-stu-id="fc423-189">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="fc423-190">Type</span><span class="sxs-lookup"><span data-stu-id="fc423-190">Type</span></span> | <span data-ttu-id="fc423-191">Oui</span><span class="sxs-lookup"><span data-stu-id="fc423-191">Yes</span></span> | <span data-ttu-id="fc423-192">Type d’action de hello.</span><span class="sxs-lookup"><span data-stu-id="fc423-192">Type of hello action.</span></span>  <span data-ttu-id="fc423-193">Ce type sera **Alert** pour les actions d’alerte.</span><span class="sxs-lookup"><span data-stu-id="fc423-193">This will be **Alert** for alert actions.</span></span> |
| <span data-ttu-id="fc423-194">Nom</span><span class="sxs-lookup"><span data-stu-id="fc423-194">Name</span></span> | <span data-ttu-id="fc423-195">Oui</span><span class="sxs-lookup"><span data-stu-id="fc423-195">Yes</span></span> | <span data-ttu-id="fc423-196">Nom complet de l’alerte de hello.</span><span class="sxs-lookup"><span data-stu-id="fc423-196">Display name for hello alert.</span></span>  <span data-ttu-id="fc423-197">Il s’agit de nom hello qui s’affiche dans la console pour la règle d’alerte hello hello.</span><span class="sxs-lookup"><span data-stu-id="fc423-197">This is hello name that's displayed in hello console for hello alert rule.</span></span> |
| <span data-ttu-id="fc423-198">Description</span><span class="sxs-lookup"><span data-stu-id="fc423-198">Description</span></span> | <span data-ttu-id="fc423-199">Non</span><span class="sxs-lookup"><span data-stu-id="fc423-199">No</span></span> | <span data-ttu-id="fc423-200">Description facultative de l’alerte de hello.</span><span class="sxs-lookup"><span data-stu-id="fc423-200">Optional description of hello alert.</span></span> |
| <span data-ttu-id="fc423-201">Severity</span><span class="sxs-lookup"><span data-stu-id="fc423-201">Severity</span></span> | <span data-ttu-id="fc423-202">Oui</span><span class="sxs-lookup"><span data-stu-id="fc423-202">Yes</span></span> | <span data-ttu-id="fc423-203">Gravité d’enregistrements alerte hello hello valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="fc423-203">Severity of hello alert record from hello following values:</span></span><br><br> <span data-ttu-id="fc423-204">**Critical**</span><span class="sxs-lookup"><span data-stu-id="fc423-204">**Critical**</span></span><br><span data-ttu-id="fc423-205">**Avertissement**</span><span class="sxs-lookup"><span data-stu-id="fc423-205">**Warning**</span></span><br><span data-ttu-id="fc423-206">**Informational**</span><span class="sxs-lookup"><span data-stu-id="fc423-206">**Informational**</span></span> |


##### <a name="threshold"></a><span data-ttu-id="fc423-207">Seuil</span><span class="sxs-lookup"><span data-stu-id="fc423-207">Threshold</span></span>
<span data-ttu-id="fc423-208">Cette section est obligatoire.</span><span class="sxs-lookup"><span data-stu-id="fc423-208">This section is required.</span></span>  <span data-ttu-id="fc423-209">Il définit les propriétés de hello pour le seuil d’alerte hello.</span><span class="sxs-lookup"><span data-stu-id="fc423-209">It defines hello properties for hello alert threshold.</span></span>

| <span data-ttu-id="fc423-210">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="fc423-210">Element name</span></span> | <span data-ttu-id="fc423-211">Requis</span><span class="sxs-lookup"><span data-stu-id="fc423-211">Required</span></span> | <span data-ttu-id="fc423-212">Description</span><span class="sxs-lookup"><span data-stu-id="fc423-212">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="fc423-213">Opérateur </span><span class="sxs-lookup"><span data-stu-id="fc423-213">Operator</span></span> | <span data-ttu-id="fc423-214">Oui</span><span class="sxs-lookup"><span data-stu-id="fc423-214">Yes</span></span> | <span data-ttu-id="fc423-215">Opérateur de comparaison hello de hello valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="fc423-215">Operator for hello comparison from hello following values:</span></span><br><br><span data-ttu-id="fc423-216">**gt = supérieur à<br>lt = inférieur à**</span><span class="sxs-lookup"><span data-stu-id="fc423-216">**gt = greater than<br>lt = less than**</span></span> |
| <span data-ttu-id="fc423-217">Valeur</span><span class="sxs-lookup"><span data-stu-id="fc423-217">Value</span></span> | <span data-ttu-id="fc423-218">Oui</span><span class="sxs-lookup"><span data-stu-id="fc423-218">Yes</span></span> | <span data-ttu-id="fc423-219">résultats de hello valeur toocompare Hello.</span><span class="sxs-lookup"><span data-stu-id="fc423-219">hello value toocompare hello results.</span></span> |


##### <a name="metricstrigger"></a><span data-ttu-id="fc423-220">MetricsTrigger</span><span class="sxs-lookup"><span data-stu-id="fc423-220">MetricsTrigger</span></span>
<span data-ttu-id="fc423-221">Cette section est facultative.</span><span class="sxs-lookup"><span data-stu-id="fc423-221">This section is optional.</span></span>  <span data-ttu-id="fc423-222">Vous devez l’inclure pour une alerte relative aux mesures métriques.</span><span class="sxs-lookup"><span data-stu-id="fc423-222">Include it for a metric measurement alert.</span></span>

> [!NOTE]
> <span data-ttu-id="fc423-223">Les alertes relatives aux mesures métriques sont actuellement en version préliminaire publique.</span><span class="sxs-lookup"><span data-stu-id="fc423-223">Metric measurement alerts are currently in public preview.</span></span> 

| <span data-ttu-id="fc423-224">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="fc423-224">Element name</span></span> | <span data-ttu-id="fc423-225">Requis</span><span class="sxs-lookup"><span data-stu-id="fc423-225">Required</span></span> | <span data-ttu-id="fc423-226">Description</span><span class="sxs-lookup"><span data-stu-id="fc423-226">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="fc423-227">TriggerCondition</span><span class="sxs-lookup"><span data-stu-id="fc423-227">TriggerCondition</span></span> | <span data-ttu-id="fc423-228">Oui</span><span class="sxs-lookup"><span data-stu-id="fc423-228">Yes</span></span> | <span data-ttu-id="fc423-229">Spécifie si le seuil de hello est pour le nombre total de violations ou consécutifs violations de hello valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="fc423-229">Specifies whether hello threshold is for total number of breaches or consecutive breaches from hello following values:</span></span><br><br><span data-ttu-id="fc423-230">**Total<br>Consecutive**</span><span class="sxs-lookup"><span data-stu-id="fc423-230">**Total<br>Consecutive**</span></span> |
| <span data-ttu-id="fc423-231">Opérateur </span><span class="sxs-lookup"><span data-stu-id="fc423-231">Operator</span></span> | <span data-ttu-id="fc423-232">Oui</span><span class="sxs-lookup"><span data-stu-id="fc423-232">Yes</span></span> | <span data-ttu-id="fc423-233">Opérateur de comparaison hello de hello valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="fc423-233">Operator for hello comparison from hello following values:</span></span><br><br><span data-ttu-id="fc423-234">**gt = supérieur à<br>lt = inférieur à**</span><span class="sxs-lookup"><span data-stu-id="fc423-234">**gt = greater than<br>lt = less than**</span></span> |
| <span data-ttu-id="fc423-235">Valeur</span><span class="sxs-lookup"><span data-stu-id="fc423-235">Value</span></span> | <span data-ttu-id="fc423-236">Oui</span><span class="sxs-lookup"><span data-stu-id="fc423-236">Yes</span></span> | <span data-ttu-id="fc423-237">Nombre de hello heures hello critères doit être alerte de hello tootrigger rempli.</span><span class="sxs-lookup"><span data-stu-id="fc423-237">Number of hello times hello criteria must be met tootrigger hello alert.</span></span> |

##### <a name="throttling"></a><span data-ttu-id="fc423-238">Limitation</span><span class="sxs-lookup"><span data-stu-id="fc423-238">Throttling</span></span>
<span data-ttu-id="fc423-239">Cette section est facultative.</span><span class="sxs-lookup"><span data-stu-id="fc423-239">This section is optional.</span></span>  <span data-ttu-id="fc423-240">Incluez cette section si vous souhaitez recevoir des alertes toosuppress de hello même règle pour une certaine quantité de temps après qu’une alerte est créée.</span><span class="sxs-lookup"><span data-stu-id="fc423-240">Include this section if you want toosuppress alerts from hello same rule for some amount of time after an alert is created.</span></span>

| <span data-ttu-id="fc423-241">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="fc423-241">Element name</span></span> | <span data-ttu-id="fc423-242">Requis</span><span class="sxs-lookup"><span data-stu-id="fc423-242">Required</span></span> | <span data-ttu-id="fc423-243">Description</span><span class="sxs-lookup"><span data-stu-id="fc423-243">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="fc423-244">DurationInMinutes</span><span class="sxs-lookup"><span data-stu-id="fc423-244">DurationInMinutes</span></span> | <span data-ttu-id="fc423-245">Oui, si l’élément Throttling est inclus</span><span class="sxs-lookup"><span data-stu-id="fc423-245">Yes if Throttling element included</span></span> | <span data-ttu-id="fc423-246">Nombre de minutes toosuppress des alertes après une à partir de hello même règle d’alerte est créée.</span><span class="sxs-lookup"><span data-stu-id="fc423-246">Number of minutes toosuppress alerts after one from hello same alert rule is created.</span></span> |

##### <a name="emailnotification"></a><span data-ttu-id="fc423-247">EmailNotification</span><span class="sxs-lookup"><span data-stu-id="fc423-247">EmailNotification</span></span>
 <span data-ttu-id="fc423-248">Cette section est facultative inclure si vous souhaitez hello tooone de messagerie toosend alerte ou des destinataires.</span><span class="sxs-lookup"><span data-stu-id="fc423-248">This section is optional  Include it if you want hello alert toosend mail tooone or more recipients.</span></span>

| <span data-ttu-id="fc423-249">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="fc423-249">Element name</span></span> | <span data-ttu-id="fc423-250">Requis</span><span class="sxs-lookup"><span data-stu-id="fc423-250">Required</span></span> | <span data-ttu-id="fc423-251">Description</span><span class="sxs-lookup"><span data-stu-id="fc423-251">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="fc423-252">Destinataires</span><span class="sxs-lookup"><span data-stu-id="fc423-252">Recipients</span></span> | <span data-ttu-id="fc423-253">Oui</span><span class="sxs-lookup"><span data-stu-id="fc423-253">Yes</span></span> | <span data-ttu-id="fc423-254">Liste séparée par des virgules de courrier électronique adresses toosend notification lorsqu’une alerte est créée comme Bonjour l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="fc423-254">Comma delimited list of email addresses toosend notification when an alert is created such as in hello following example.</span></span><br><br><span data-ttu-id="fc423-255">**[ "recipient1@contoso.com", "recipient2@contoso.com" ]**</span><span class="sxs-lookup"><span data-stu-id="fc423-255">**[ "recipient1@contoso.com", "recipient2@contoso.com" ]**</span></span> |
| <span data-ttu-id="fc423-256">Objet</span><span class="sxs-lookup"><span data-stu-id="fc423-256">Subject</span></span> | <span data-ttu-id="fc423-257">Oui</span><span class="sxs-lookup"><span data-stu-id="fc423-257">Yes</span></span> | <span data-ttu-id="fc423-258">Ligne objet de messagerie de hello.</span><span class="sxs-lookup"><span data-stu-id="fc423-258">Subject line of hello mail.</span></span> |
| <span data-ttu-id="fc423-259">Pièce jointe</span><span class="sxs-lookup"><span data-stu-id="fc423-259">Attachment</span></span> | <span data-ttu-id="fc423-260">Non</span><span class="sxs-lookup"><span data-stu-id="fc423-260">No</span></span> | <span data-ttu-id="fc423-261">Actuellement, les pièces jointes ne sont pas prises en charge.</span><span class="sxs-lookup"><span data-stu-id="fc423-261">Attachments are not currently supported.</span></span>  <span data-ttu-id="fc423-262">Si cet élément est inclus, il doit avoir la valeur **None**.</span><span class="sxs-lookup"><span data-stu-id="fc423-262">If this element is included, it should be **None**.</span></span> |


##### <a name="remediation"></a><span data-ttu-id="fc423-263">Correction</span><span class="sxs-lookup"><span data-stu-id="fc423-263">Remediation</span></span>
<span data-ttu-id="fc423-264">Cette section est facultative inclure si vous souhaitez un toostart de runbook dans l’alerte toohello de réponse.</span><span class="sxs-lookup"><span data-stu-id="fc423-264">This section is optional  Include it if you want a runbook toostart in response toohello alert.</span></span> |

| <span data-ttu-id="fc423-265">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="fc423-265">Element name</span></span> | <span data-ttu-id="fc423-266">Requis</span><span class="sxs-lookup"><span data-stu-id="fc423-266">Required</span></span> | <span data-ttu-id="fc423-267">Description</span><span class="sxs-lookup"><span data-stu-id="fc423-267">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="fc423-268">RunbookName</span><span class="sxs-lookup"><span data-stu-id="fc423-268">RunbookName</span></span> | <span data-ttu-id="fc423-269">Oui</span><span class="sxs-lookup"><span data-stu-id="fc423-269">Yes</span></span> | <span data-ttu-id="fc423-270">Nom de hello runbook toostart.</span><span class="sxs-lookup"><span data-stu-id="fc423-270">Name of hello runbook toostart.</span></span> |
| <span data-ttu-id="fc423-271">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="fc423-271">WebhookUri</span></span> | <span data-ttu-id="fc423-272">Oui</span><span class="sxs-lookup"><span data-stu-id="fc423-272">Yes</span></span> | <span data-ttu-id="fc423-273">URI du webhook hello pour hello runbook.</span><span class="sxs-lookup"><span data-stu-id="fc423-273">Uri of hello webhook for hello runbook.</span></span> |
| <span data-ttu-id="fc423-274">Expiry</span><span class="sxs-lookup"><span data-stu-id="fc423-274">Expiry</span></span> | <span data-ttu-id="fc423-275">Non</span><span class="sxs-lookup"><span data-stu-id="fc423-275">No</span></span> | <span data-ttu-id="fc423-276">Date et heure de mise à jour de hello expire.</span><span class="sxs-lookup"><span data-stu-id="fc423-276">Date and time that hello remediation expires.</span></span> |

#### <a name="webhook-actions"></a><span data-ttu-id="fc423-277">Actions de webhook</span><span class="sxs-lookup"><span data-stu-id="fc423-277">Webhook actions</span></span>

<span data-ttu-id="fc423-278">Les actions Webhook démarrer un processus en appelant une URL et éventuellement en fournissant un toobe de charge utile envoyée.</span><span class="sxs-lookup"><span data-stu-id="fc423-278">Webhook actions start a process by calling a URL and optionally providing a payload toobe sent.</span></span> <span data-ttu-id="fc423-279">Ils sont des actions tooRemediation similaires à ceci près qu’ils sont destinés à webhooks qui peut appeler des processus autres que les runbooks Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="fc423-279">They are similar tooRemediation actions except they are meant for webhooks that may invoke processes other than Azure Automation runbooks.</span></span> <span data-ttu-id="fc423-280">Elles fournissent également hello option supplémentaire permettant de fournir un processus à distance de charge utile toobe remis toohello.</span><span class="sxs-lookup"><span data-stu-id="fc423-280">They also provide hello additional option of providing a payload toobe delivered toohello remote process.</span></span>

<span data-ttu-id="fc423-281">Si votre alerte appelle un webhook, vous devez une ressource d’action avec un type de **Webhook** dans Ajout toohello **alerte** ressource d’action.</span><span class="sxs-lookup"><span data-stu-id="fc423-281">If your alert will call a webhook, then it will need an action resource with a type of **Webhook** in addition toohello **Alert** action resource.</span></span>  

    {
      "name": "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name, '/', variables('Webhook').Name)]",
      "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions/",
      "apiVersion": "[variables('LogAnalyticsApiVersion')]",
      "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name, '/schedules/', variables('Schedule').Name)]"
      ],
      "properties": {
        "etag": "*",
        "type": "[variables('Alert').Webhook.Type]",
        "name": "[variables('Alert').Webhook.Name]",
        "webhookUri": "[variables('Alert').Webhook.webhookUri]",
        "customPayload": "[variables('Alert').Webhook.CustomPayLoad]"
      }
    }

<span data-ttu-id="fc423-282">Décrit les propriétés de Hello pour ressources d’action Webhook Bonjour les tableaux suivants.</span><span class="sxs-lookup"><span data-stu-id="fc423-282">hello properties for Webhook action resources are described in hello following tables.</span></span>

| <span data-ttu-id="fc423-283">Nom de l'élément</span><span class="sxs-lookup"><span data-stu-id="fc423-283">Element name</span></span> | <span data-ttu-id="fc423-284">Requis</span><span class="sxs-lookup"><span data-stu-id="fc423-284">Required</span></span> | <span data-ttu-id="fc423-285">Description</span><span class="sxs-lookup"><span data-stu-id="fc423-285">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="fc423-286">type</span><span class="sxs-lookup"><span data-stu-id="fc423-286">type</span></span> | <span data-ttu-id="fc423-287">Oui</span><span class="sxs-lookup"><span data-stu-id="fc423-287">Yes</span></span> | <span data-ttu-id="fc423-288">Type d’action de hello.</span><span class="sxs-lookup"><span data-stu-id="fc423-288">Type of hello action.</span></span>  <span data-ttu-id="fc423-289">Il s’agit de **Webhook** pour les actions de webhook.</span><span class="sxs-lookup"><span data-stu-id="fc423-289">This will be **Webhook** for webhook actions.</span></span> |
| <span data-ttu-id="fc423-290">name</span><span class="sxs-lookup"><span data-stu-id="fc423-290">name</span></span> | <span data-ttu-id="fc423-291">Oui</span><span class="sxs-lookup"><span data-stu-id="fc423-291">Yes</span></span> | <span data-ttu-id="fc423-292">Nom complet de l’action de hello.</span><span class="sxs-lookup"><span data-stu-id="fc423-292">Display name for hello action.</span></span>  <span data-ttu-id="fc423-293">Cela n’est pas affiché dans la console de hello.</span><span class="sxs-lookup"><span data-stu-id="fc423-293">This is not displayed in hello console.</span></span> |
| <span data-ttu-id="fc423-294">wehookUri</span><span class="sxs-lookup"><span data-stu-id="fc423-294">wehookUri</span></span> | <span data-ttu-id="fc423-295">Oui</span><span class="sxs-lookup"><span data-stu-id="fc423-295">Yes</span></span> | <span data-ttu-id="fc423-296">URI pour hello webhook.</span><span class="sxs-lookup"><span data-stu-id="fc423-296">Uri for hello webhook.</span></span> |
| <span data-ttu-id="fc423-297">customPayload</span><span class="sxs-lookup"><span data-stu-id="fc423-297">customPayload</span></span> | <span data-ttu-id="fc423-298">Non</span><span class="sxs-lookup"><span data-stu-id="fc423-298">No</span></span> | <span data-ttu-id="fc423-299">Charge utile personnalisée toobe envoyé toohello webhook.</span><span class="sxs-lookup"><span data-stu-id="fc423-299">Custom payload toobe sent toohello webhook.</span></span> <span data-ttu-id="fc423-300">format de Hello dépend de quelles webhook hello est attendu.</span><span class="sxs-lookup"><span data-stu-id="fc423-300">hello format will depend on what hello webhook is expecting.</span></span> |




## <a name="sample"></a><span data-ttu-id="fc423-301">Exemple</span><span class="sxs-lookup"><span data-stu-id="fc423-301">Sample</span></span>

<span data-ttu-id="fc423-302">Voici un exemple d’une solution qui incluent ce qui inclut hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="fc423-302">Following is a sample of a solution that include that includes hello following resources:</span></span>

- <span data-ttu-id="fc423-303">Recherche enregistrée</span><span class="sxs-lookup"><span data-stu-id="fc423-303">Saved search</span></span>
- <span data-ttu-id="fc423-304">Planification</span><span class="sxs-lookup"><span data-stu-id="fc423-304">Schedule</span></span>
- <span data-ttu-id="fc423-305">Action d’alerte</span><span class="sxs-lookup"><span data-stu-id="fc423-305">Alert action</span></span>
- <span data-ttu-id="fc423-306">Action webhook</span><span class="sxs-lookup"><span data-stu-id="fc423-306">Webhook action</span></span>

<span data-ttu-id="fc423-307">exemples d’utilisation de Hello [paramètres de solution standard](operations-management-suite-solutions-solution-file.md#parameters) variables sont communément utilisées dans une solution en opposition toohardcoding des valeurs dans les définitions de ressource hello.</span><span class="sxs-lookup"><span data-stu-id="fc423-307">hello sample uses [standard solution parameters](operations-management-suite-solutions-solution-file.md#parameters) variables that would commonly be used in a solution as opposed toohardcoding values in hello resource definitions.</span></span>

    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0",
        "parameters": {
          "workspaceName": {
            "type": "string",
            "metadata": {
              "Description": "Name of Log Analytics workspace"
            }
          },
          "accountName": {
            "type": "string",
            "metadata": {
              "Description": "Name of Automation account"
            }
          },
          "workspaceregionId": {
            "type": "string",
            "metadata": {
              "Description": "Region of Log Analytics workspace"
            }
          },
          "regionId": {
            "type": "string",
            "metadata": {
              "Description": "Region of Automation account"
            }
          },
          "pricingTier": {
            "type": "string",
            "metadata": {
              "Description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
          },
          "recipients": {
            "type": "string",
            "metadata": {
              "Description": "List of recipients for hello email alert separated by semicolon"
            }
          }
        },
        "variables": {
          "SolutionName": "MySolution",
          "SolutionVersion": "1.0",
          "SolutionPublisher": "Contoso",
          "ProductName": "SampleSolution",
    
          "LogAnalyticsApiVersion": "2015-11-01-preview",
    
          "MySearch": {
            "displayName": "Error records by hour",
            "query": "Type=MyRecord_CL | measure avg(Rating_d) by Instance_s interval 60minutes",
            "category": "Samples",
            "name": "Samples-Count of data"
          },
          "MyAlert": {
            "Name": "[toLower(concat('myalert-',uniqueString(resourceGroup().id, deployment().name)))]",
            "DisplayName": "My alert rule",
            "Description": "Sample alert.  Fires when 3 error records found over hour interval.",
            "Severity": "Critical",
            "ThresholdOperator": "gt",
            "ThresholdValue": 3,
            "Schedule": {
              "Name": "[toLower(concat('myschedule-',uniqueString(resourceGroup().id, deployment().name)))]",
              "Interval": 15,
              "TimeSpan": 60
            },
            "MetricsTrigger": {
              "TriggerCondition": "Consecutive",
              "Operator": "gt",
              "Value": 3
            },
            "ThrottleMinutes": 60,
            "Notification": {
              "Recipients": [
                "[parameters('recipients')]"
              ],
              "Subject": "Sample alert"
            },
            "Remediation": {
              "RunbookName": "MyRemediationRunbook",
              "WebhookUri": "https://s1events.azure-automation.net/webhooks?token=TluBFH3GpX4IEAnFoImoAWLTULkjD%2bTS0yscyrr7ogw%3d"
            },
            "Webhook": {
              "Name": "MyWebhook",
              "Uri": "https://MyService.com/webhook",
              "Payload": "{\"field1\":\"value1\",\"field2\":\"value2\"}"
            }
          }
        },
        "resources": [
          {
            "name": "[concat(variables('SolutionName'), '[' ,parameters('workspacename'), ']')]",
            "location": "[parameters('workspaceRegionId')]",
            "tags": { },
            "type": "Microsoft.OperationsManagement/solutions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches', parameters('workspacename'), variables('MySearch').Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Webhook.Name)]"
            ],
            "properties": {
              "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
              "referencedResources": [
              ],
              "containedResources": [
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches', parameters('workspacename'), variables('MySearch').Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Webhook.Name)]"
              ]
            },
            "plan": {
              "name": "[concat(variables('SolutionName'), '[' ,parameters('workspaceName'), ']')]",
              "Version": "[variables('SolutionVersion')]",
              "product": "[variables('ProductName')]",
              "publisher": "[variables('SolutionPublisher')]",
              "promotionCode": ""
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [ ],
            "tags": { },
            "properties": {
              "etag": "*",
              "query": "[variables('MySearch').query]",
              "displayName": "[variables('MySearch').displayName]",
              "category": "[variables('MySearch').category]"
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/', variables('MyAlert').Schedule.Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name)]"
            ],
            "properties": {
              "etag": "*",
              "interval": "[variables('MyAlert').Schedule.Interval]",
              "queryTimeSpan": "[variables('MyAlert').Schedule.TimeSpan]",
              "enabled": true
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/',  variables('MyAlert').Schedule.Name, '/',  variables('MyAlert').Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/',  variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name)]"
            ],
            "properties": {
              "etag": "*",
              "Type": "Alert",
              "Name": "[variables('MyAlert').DisplayName]",
              "Description": "[variables('MyAlert').Description]",
              "Severity": "[variables('MyAlert').Severity]",
              "Threshold": {
                "Operator": "[variables('MyAlert').ThresholdOperator]",
                "Value": "[variables('MyAlert').ThresholdValue]",
                "MetricsTrigger": {
                  "TriggerCondition": "[variables('MyAlert').MetricsTrigger.TriggerCondition]",
                  "Operator": "[variables('MyAlert').MetricsTrigger.Operator]",
                  "Value": "[variables('MyAlert').MetricsTrigger.Value]"
                }
              },
              "Throttling": {
                "DurationInMinutes": "[variables('MyAlert').ThrottleMinutes]"
              },
              "EmailNotification": {
                "Recipients": "[variables('MyAlert').Notification.Recipients]",
                "Subject": "[variables('MyAlert').Notification.Subject]",
                "Attachment": "None"
              },
              "Remediation": {
                "RunbookName": "[variables('MyAlert').Remediation.RunbookName]",
                "WebhookUri": "[variables('MyAlert').Remediation.WebhookUri]"
              }
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/', variables('MyAlert').Schedule.Name, '/', variables('MyAlert').Webhook.Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name)]",
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name, '/actions/',variables('MyAlert').Name)]"
            ],
            "properties": {
              "etag": "*",
              "Type": "Webhook",
              "Name": "[variables('MyAlert').Webhook.Name]",
              "WebhookUri": "[variables('MyAlert').Webhook.Uri]",
              "CustomPayload": "[variables('MyAlert').Webhook.Payload]"
            }
          }
        ]
    }


<span data-ttu-id="fc423-308">Hello suivant du fichier de paramètres fournit des valeurs d’exemples pour cette solution.</span><span class="sxs-lookup"><span data-stu-id="fc423-308">hello following parameter file provides samples values for this solution.</span></span>

    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "workspacename": {
                "value": "myWorkspace"
            },
            "accountName": {
                "value": "myAccount"
            },
            "workspaceregionId": {
                "value": "East US"
            },
            "regionId": {
                "value": "East US 2"
            },
            "pricingTier": {
                "value": "Free"
            },
            "recipients": {
                "value": "recipient1@contoso.com;recipient2@contoso.com"
            }
        }
    }


## <a name="next-steps"></a><span data-ttu-id="fc423-309">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fc423-309">Next steps</span></span>
* <span data-ttu-id="fc423-310">[Ajouter des vues](operations-management-suite-solutions-resources-views.md) solution de gestion tooyour.</span><span class="sxs-lookup"><span data-stu-id="fc423-310">[Add views](operations-management-suite-solutions-resources-views.md) tooyour management solution.</span></span>
* <span data-ttu-id="fc423-311">[Ajouter des runbooks Automation et autres ressources](operations-management-suite-solutions-resources-automation.md) solution de gestion tooyour.</span><span class="sxs-lookup"><span data-stu-id="fc423-311">[Add Automation runbooks and other resources](operations-management-suite-solutions-resources-automation.md) tooyour management solution.</span></span>

