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
# <a name="create-an-alert-webhook-action-in-oms-log-analytics-toosend-message-tooslack"></a>Créer une action de l’alerte de webhook dans tooSlack de message toosend Analytique des journaux OMS
Une des actions hello vous pouvez exécuter dans la réponse tooa [alerte d’Analytique de journal](log-analytics-alerts.md) est un *webhook*, qui vous permet de tooinvoke un processus externe via une requête HTTP unique.  Vous pouvez consulter les détails des alertes et des webhooks dans [Alertes dans Log Analytics](log-analytics-alerts.md)

Dans cet article, nous allons découvrir un exemple de création d’une action de webhook dans une alerte Log Analytics à l’aide du service de messagerie Slack.

> [!NOTE]
> Cet exemple, vous devez avoir un toocomplete compte Slack.  Vous pouvez ouvrir un compte gratuit à l’adresse [slack.com](http://slack.com).
> 
> 

## <a name="step-1---enable-webhooks-in-slack"></a>Étape 1 : Activer les webhooks dans Slack
1. Connectez-vous à tooSlack à [slack.com](http://slack.com).
2. Sélectionnez un canal Bonjour **canaux** section dans le volet gauche de hello.  C’est hello canal vous recevrez ce message de type hello pour.  Vous pouvez sélectionner un des canaux de hello par défaut telles que **général** ou **aléatoire**.  Dans un scénario de production, vous créeriez probablement un canal spécial tel que **alertes_service_critiques**. <br>
   
   ![Canaux Slack](media/log-analytics-alerts-webhooks/oms-webhooks01.png)
3. Cliquez sur **ajouter une application ou intégration personnalisés** tooopen hello active de l’application.
4. Type *webhooks* dans la zone de recherche hello, puis sélectionnez **WebHooks entrant**. <br>
   
   ![Canaux Slack](media/log-analytics-alerts-webhooks/oms-webhooks02.png)
5. Cliquez sur **installer** nom d’équipe tooyour suivant.
6. Cliquez sur **Ajouter une configuration**.
7. Canal de hello hello SELECT que vous allez toouse pour cet exemple, puis cliquez sur **ajouter le WebHooks entrant intégration**.  
8. Hello de copie **URL du Webhook**.  Vous allez coller ce dans configuration d’alerte hello. <br>
   
    ![Canaux Slack](media/log-analytics-alerts-webhooks/oms-webhooks05.png)

## <a name="step-2---create-alert-rule-in-log-analytics"></a>Étape 2 : Créer une règle d’alerte dans Log Analytics
1. [Créer une règle d’alerte](log-analytics-alerts.md) avec hello suivant les paramètres.
   * Requête : ```    Type=Event EventLevelName=error ```
   * Vérifier cette alerte toutes les : 5 minutes
   * nombre de Hello de résultats est : supérieur à 10
   * Over this time window (Pendant cette fenêtre de temps) : 60 minutes
   * Sélectionnez **Oui** pour **Webhook** et **non** pour hello autres actions.
2. Hello coller Slack URL dans hello **URL du Webhook** champ.
3. L’option hello trop**incluent une charge utile JSON personnalisée**.
4. Slack attend une charge utile au format JSON avec un paramètre nommé *text*.  Il s’agit de texte hello elle s’affichera dans le message de type hello qu'il crée.  Vous pouvez utiliser une ou plusieurs des paramètres d’alerte hello à l’aide de hello  *#*  ces symboles comme hello l’exemple suivant.
   
    ```
    {
    "text":"#alertrulename fired with #searchresultcount records which exceeds hello over threshold of #thresholdvalue ."
    }
    ```
   
    ![exemple de charge utile JSON](media/log-analytics-alerts-webhooks/oms-webhooks07.png)
5. Cliquez sur **enregistrer** règle d’alerte toosave hello.
6. Temps d’attente suffisant pour une alerte toobe créé, puis vérifiez la marge d’un message qui sera similaire toohello suivant.
   
   ![exemple de webhook dans Slack](media/log-analytics-alerts-webhooks/oms-webhooks08.png)

### <a name="advanced-webhook-payload-for-slack"></a>Charge utile de webhook avancée pour Slack
Vous disposez d’une marge de manœuvre importante pour personnaliser les messages entrants avec Slack. Pour plus d’informations, consultez [Webhooks entrant](https://api.slack.com/incoming-webhooks) sur le site Web de la marge de hello. Voici un toocreate plus complexe de la charge utile un message complet avec mise en forme :

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


Cela génère un message dans la marge suivant toohello similaire.

![exemple de message dans Slack](media/log-analytics-alerts-webhooks/oms-webhooks09.png)

## <a name="summary"></a>Résumé
Avec cette règle d’alerte en place, vous aurez un tooSlack message envoyé chaque fois que les critères de hello est remplie.  

Cela n'est qu’un exemple d’une action que vous pouvez créer dans l’alerte tooan de réponse.  Vous pouvez créer une action webhook qui appelle un autre service externe, un toostart d’action de runbook un runbook dans Azure Automation ou une toosend d’action de courrier électronique un tooyourself de messagerie ou d’autres destinataires.   

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur les autres [actions d’alerte dans Log Analytics](log-analytics-alerts-actions.md).


