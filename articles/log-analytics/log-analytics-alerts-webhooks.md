---
title: "exemple d’action d’alerte aaaWebhook dans Analytique des journaux OMS | Documents Microsoft"
description: "Une des actions hello vous pouvez exécuter dans tooa réponse Analytique de journal alerte est un * webhook *, qui vous permet de tooinvoke un processus externe via une requête HTTP unique. Cet article décrit un exemple de création d’une action de webhook dans une alerte Log Analytics à l’aide de Slack."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 13c39f0f-fd3c-472d-8324-ddf7538be45e
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: bwren
ms.openlocfilehash: e60bdc4922347073d572c2e4719461b13e8e7d1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-alert-webhook-action-in-oms-log-analytics-toosend-message-tooslack"></a><span data-ttu-id="0d3bf-104">Créer une action de l’alerte de webhook dans tooSlack de message toosend Analytique des journaux OMS</span><span class="sxs-lookup"><span data-stu-id="0d3bf-104">Create an alert webhook action in OMS Log Analytics toosend message tooSlack</span></span>
<span data-ttu-id="0d3bf-105">Une des actions hello vous pouvez exécuter dans la réponse tooa [alerte d’Analytique de journal](log-analytics-alerts.md) est un *webhook*, qui vous permet de tooinvoke un processus externe via une requête HTTP unique.</span><span class="sxs-lookup"><span data-stu-id="0d3bf-105">One of hello actions you can run in response tooa [Log Analytics alert](log-analytics-alerts.md) is a *webhook*, which allows you tooinvoke an external process through a single HTTP request.</span></span>  <span data-ttu-id="0d3bf-106">Vous pouvez consulter les détails des alertes et des webhooks dans [Alertes dans Log Analytics](log-analytics-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="0d3bf-106">You can read about details of alerts and webhooks in [Alerts in Log Analytics](log-analytics-alerts.md)</span></span>

<span data-ttu-id="0d3bf-107">Dans cet article, nous allons découvrir un exemple de création d’une action de webhook dans une alerte Log Analytics à l’aide du service de messagerie Slack.</span><span class="sxs-lookup"><span data-stu-id="0d3bf-107">In this article, we’ll walk through an example of creating a webhook action in a Log Analytics alert using Slack which is a messaging service.</span></span>

> [!NOTE]
> <span data-ttu-id="0d3bf-108">Cet exemple, vous devez avoir un toocomplete compte Slack.</span><span class="sxs-lookup"><span data-stu-id="0d3bf-108">You must have a Slack account toocomplete this sample.</span></span>  <span data-ttu-id="0d3bf-109">Vous pouvez ouvrir un compte gratuit à l’adresse [slack.com](http://slack.com).</span><span class="sxs-lookup"><span data-stu-id="0d3bf-109">You can sign up for a free account at [slack.com](http://slack.com).</span></span>
> 
> 

## <a name="step-1---enable-webhooks-in-slack"></a><span data-ttu-id="0d3bf-110">Étape 1 : Activer les webhooks dans Slack</span><span class="sxs-lookup"><span data-stu-id="0d3bf-110">Step 1 - Enable webhooks in Slack</span></span>
1. <span data-ttu-id="0d3bf-111">Connectez-vous à tooSlack à [slack.com](http://slack.com).</span><span class="sxs-lookup"><span data-stu-id="0d3bf-111">Sign in tooSlack at [slack.com](http://slack.com).</span></span>
2. <span data-ttu-id="0d3bf-112">Sélectionnez un canal Bonjour **canaux** section dans le volet gauche de hello.</span><span class="sxs-lookup"><span data-stu-id="0d3bf-112">Select a channel in hello **Channels** section in hello left pane.</span></span>  <span data-ttu-id="0d3bf-113">C’est hello canal vous recevrez ce message de type hello pour.</span><span class="sxs-lookup"><span data-stu-id="0d3bf-113">This is hello channel that hello message will be sent to.</span></span>  <span data-ttu-id="0d3bf-114">Vous pouvez sélectionner un des canaux de hello par défaut telles que **général** ou **aléatoire**.</span><span class="sxs-lookup"><span data-stu-id="0d3bf-114">You can select one of hello default channels such as **general** or **random**.</span></span>  <span data-ttu-id="0d3bf-115">Dans un scénario de production, vous créeriez probablement un canal spécial tel que **alertes_service_critiques**.</span><span class="sxs-lookup"><span data-stu-id="0d3bf-115">In a production scenario, you would most likely create a special channel such as **criticalservicealerts**.</span></span> <br>
   
   ![Canaux Slack](media/log-analytics-alerts-webhooks/oms-webhooks01.png)
3. <span data-ttu-id="0d3bf-117">Cliquez sur **ajouter une application ou intégration personnalisés** tooopen hello active de l’application.</span><span class="sxs-lookup"><span data-stu-id="0d3bf-117">Click **Add an app or custom integration** tooopen hello App Directory.</span></span>
4. <span data-ttu-id="0d3bf-118">Type *webhooks* dans la zone de recherche hello, puis sélectionnez **WebHooks entrant**.</span><span class="sxs-lookup"><span data-stu-id="0d3bf-118">Type *webhooks* into hello search box and then select **Incoming WebHooks**.</span></span> <br>
   
   ![Canaux Slack](media/log-analytics-alerts-webhooks/oms-webhooks02.png)
5. <span data-ttu-id="0d3bf-120">Cliquez sur **installer** nom d’équipe tooyour suivant.</span><span class="sxs-lookup"><span data-stu-id="0d3bf-120">Click **Install** next tooyour team name.</span></span>
6. <span data-ttu-id="0d3bf-121">Cliquez sur **Ajouter une configuration**.</span><span class="sxs-lookup"><span data-stu-id="0d3bf-121">Click **Add Configuration**.</span></span>
7. <span data-ttu-id="0d3bf-122">Canal de hello hello SELECT que vous allez toouse pour cet exemple, puis cliquez sur **ajouter le WebHooks entrant intégration**.</span><span class="sxs-lookup"><span data-stu-id="0d3bf-122">Select hello hello channel that you're going toouse for this example, and then click **Add Incoming WebHooks integration**.</span></span>  
8. <span data-ttu-id="0d3bf-123">Hello de copie **URL du Webhook**.</span><span class="sxs-lookup"><span data-stu-id="0d3bf-123">Copy hello **Webhook URL**.</span></span>  <span data-ttu-id="0d3bf-124">Vous allez coller ce dans configuration d’alerte hello.</span><span class="sxs-lookup"><span data-stu-id="0d3bf-124">You'll be pasting this into hello Alert configuration.</span></span> <br>
   
    ![Canaux Slack](media/log-analytics-alerts-webhooks/oms-webhooks05.png)

## <a name="step-2---create-alert-rule-in-log-analytics"></a><span data-ttu-id="0d3bf-126">Étape 2 : Créer une règle d’alerte dans Log Analytics</span><span class="sxs-lookup"><span data-stu-id="0d3bf-126">Step 2 - Create alert rule in Log Analytics</span></span>
1. <span data-ttu-id="0d3bf-127">[Créer une règle d’alerte](log-analytics-alerts.md) avec hello suivant les paramètres.</span><span class="sxs-lookup"><span data-stu-id="0d3bf-127">[Create an alert rule](log-analytics-alerts.md) with hello following settings.</span></span>
   * <span data-ttu-id="0d3bf-128">Requête : ```    Type=Event EventLevelName=error ```</span><span class="sxs-lookup"><span data-stu-id="0d3bf-128">Query: ```    Type=Event EventLevelName=error ```</span></span>
   * <span data-ttu-id="0d3bf-129">Vérifier cette alerte toutes les : 5 minutes</span><span class="sxs-lookup"><span data-stu-id="0d3bf-129">Check for this alert every: 5 minutes</span></span>
   * <span data-ttu-id="0d3bf-130">nombre de Hello de résultats est : supérieur à 10</span><span class="sxs-lookup"><span data-stu-id="0d3bf-130">hello number of results is: greater than 10</span></span>
   * <span data-ttu-id="0d3bf-131">Over this time window (Pendant cette fenêtre de temps) : 60 minutes</span><span class="sxs-lookup"><span data-stu-id="0d3bf-131">Over this time window: 60 minutes</span></span>
   * <span data-ttu-id="0d3bf-132">Sélectionnez **Oui** pour **Webhook** et **non** pour hello autres actions.</span><span class="sxs-lookup"><span data-stu-id="0d3bf-132">Select **Yes** for **Webhook** and **No** for hello other actions.</span></span>
2. <span data-ttu-id="0d3bf-133">Hello coller Slack URL dans hello **URL du Webhook** champ.</span><span class="sxs-lookup"><span data-stu-id="0d3bf-133">Paste hello Slack URL into hello **Webhook URL** field.</span></span>
3. <span data-ttu-id="0d3bf-134">L’option hello trop**incluent une charge utile JSON personnalisée**.</span><span class="sxs-lookup"><span data-stu-id="0d3bf-134">Select hello option too**include a custom JSON payload**.</span></span>
4. <span data-ttu-id="0d3bf-135">Slack attend une charge utile au format JSON avec un paramètre nommé *text*.</span><span class="sxs-lookup"><span data-stu-id="0d3bf-135">Slack expects a payload formatted in JSON with a parameter named *text*.</span></span>  <span data-ttu-id="0d3bf-136">Il s’agit de texte hello elle s’affichera dans le message de type hello qu'il crée.</span><span class="sxs-lookup"><span data-stu-id="0d3bf-136">This is hello text that it will display in hello message it creates.</span></span>  <span data-ttu-id="0d3bf-137">Vous pouvez utiliser une ou plusieurs des paramètres d’alerte hello à l’aide de hello  *#*  ces symboles comme hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="0d3bf-137">You can use one or more of hello alert parameters using hello *#* symbol such as in hello following example.</span></span>
   
    ```
    {
    "text":"#alertrulename fired with #searchresultcount records which exceeds hello over threshold of #thresholdvalue ."
    }
    ```
   
    ![exemple de charge utile JSON](media/log-analytics-alerts-webhooks/oms-webhooks07.png)
5. <span data-ttu-id="0d3bf-139">Cliquez sur **enregistrer** règle d’alerte toosave hello.</span><span class="sxs-lookup"><span data-stu-id="0d3bf-139">Click **Save** toosave hello alert rule.</span></span>
6. <span data-ttu-id="0d3bf-140">Temps d’attente suffisant pour une alerte toobe créé, puis vérifiez la marge d’un message qui sera similaire toohello suivant.</span><span class="sxs-lookup"><span data-stu-id="0d3bf-140">Wait sufficient time for an alert toobe created and then check Slack for a message which will be similar toohello following.</span></span>
   
   ![exemple de webhook dans Slack](media/log-analytics-alerts-webhooks/oms-webhooks08.png)

### <a name="advanced-webhook-payload-for-slack"></a><span data-ttu-id="0d3bf-142">Charge utile de webhook avancée pour Slack</span><span class="sxs-lookup"><span data-stu-id="0d3bf-142">Advanced webhook payload for Slack</span></span>
<span data-ttu-id="0d3bf-143">Vous disposez d’une marge de manœuvre importante pour personnaliser les messages entrants avec Slack.</span><span class="sxs-lookup"><span data-stu-id="0d3bf-143">You can extensively customize inbound messages with Slack.</span></span> <span data-ttu-id="0d3bf-144">Pour plus d’informations, consultez [Webhooks entrant](https://api.slack.com/incoming-webhooks) sur le site Web de la marge de hello.</span><span class="sxs-lookup"><span data-stu-id="0d3bf-144">For more information, see [Incoming Webhooks](https://api.slack.com/incoming-webhooks) on hello Slack website.</span></span> <span data-ttu-id="0d3bf-145">Voici un toocreate plus complexe de la charge utile un message complet avec mise en forme :</span><span class="sxs-lookup"><span data-stu-id="0d3bf-145">Following is a more complex payload toocreate a rich message with formatting:</span></span>

    {
        "attachments": [
            {
                "title":"OMS Alerts Custom Payload",
                "fields": [
                    {
                        "title": "Alert Rule Name",
                        "value": "#alertrulename"},
                    {
                        "title": "Link tooSearchResults",
                        "value": "<#linktosearchresults|OMS Search Results>"},
                    {
                        "title": "Search Interval",
                        "value": "#searchinterval"},
                    {
                        "title": "Threshold Operator",
                        "value": "#thresholdoperator"},
                    {
                        "title": "Threshold Value",
                        "value": "#thresholdvalue"}
                ],
                "color": "#F35A00"
            }
        ]
    }


<span data-ttu-id="0d3bf-146">Cela génère un message dans la marge suivant toohello similaire.</span><span class="sxs-lookup"><span data-stu-id="0d3bf-146">This would generate a message in Slack similar toohello following.</span></span>

![exemple de message dans Slack](media/log-analytics-alerts-webhooks/oms-webhooks09.png)

## <a name="summary"></a><span data-ttu-id="0d3bf-148">Résumé</span><span class="sxs-lookup"><span data-stu-id="0d3bf-148">Summary</span></span>
<span data-ttu-id="0d3bf-149">Avec cette règle d’alerte en place, vous aurez un tooSlack message envoyé chaque fois que les critères de hello est remplie.</span><span class="sxs-lookup"><span data-stu-id="0d3bf-149">With this alert rule in place, you would have a message sent tooSlack every time hello criteria is met.</span></span>  

<span data-ttu-id="0d3bf-150">Cela n'est qu’un exemple d’une action que vous pouvez créer dans l’alerte tooan de réponse.</span><span class="sxs-lookup"><span data-stu-id="0d3bf-150">This is only one example of an action that you can create in response tooan alert.</span></span>  <span data-ttu-id="0d3bf-151">Vous pouvez créer une action webhook qui appelle un autre service externe, un toostart d’action de runbook un runbook dans Azure Automation ou une toosend d’action de courrier électronique un tooyourself de messagerie ou d’autres destinataires.</span><span class="sxs-lookup"><span data-stu-id="0d3bf-151">You could create a webhook action that calls another external service, a runbook action toostart a runbook in Azure Automation, or an email action toosend a mail tooyourself or other recipients.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="0d3bf-152">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0d3bf-152">Next Steps</span></span>
* <span data-ttu-id="0d3bf-153">En savoir plus sur les autres [actions d’alerte dans Log Analytics](log-analytics-alerts-actions.md).</span><span class="sxs-lookup"><span data-stu-id="0d3bf-153">Learn about other [alert actions in Log Analytics](log-analytics-alerts-actions.md) including other actions.</span></span>


