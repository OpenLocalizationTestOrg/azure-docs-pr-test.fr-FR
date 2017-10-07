---
title: "aaaCalling un Runbook Azure Automation à partir d’une alerte Analytique de journal | Documents Microsoft"
description: "Cet article fournit une vue d’ensemble de la manière tooinvoke un runbook Automation à partir d’une alerte Microsoft OMS journal Analytique."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/31/2017
ms.author: magoedte
ms.openlocfilehash: 8b745d6e6c2b0294d676e010f52855cd51741cf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="calling-an-azure-automation-runbook-from-an-oms-log-analytics-alert"></a>Appel d’un runbook Azure Automation à partir d’une alerte OMS Log Analytics

Lorsqu’une alerte est configurée dans le journal Analytique toocreate un enregistrement d’alerte si les résultats correspondent aux critères particuliers, tels qu’un pic prolongé dans l’utilisation du processeur ou une application particulière processus toohello critiques des fonctionnalités d’une application métier échoue et écrit un événement correspondant dans le journal des événements Windows hello, cette alerte peut exécuter automatiquement un runbook Automation dans un tooauto tentative-corriger le problème de hello.  

Il y a deux options toocall un runbook pour la configuration d’alerte de hello.  Plus précisément :

1. Utilisation d’un webhook.
   * Il s’agit de hello seule option si votre espace de travail OMS n’est pas lié tooan compte Automation.
   * Si vous disposez déjà d’un espace de travail Automation compte lié tooan OMS, cette option est toujours disponible.  

2. Sélection directe d’un runbook.
   * Cette option est disponible uniquement lorsque l’espace de travail OMS hello est lié tooan compte Automation.  

## <a name="calling-a-runbook-using-a-webhook"></a>Appel d’un runbook à l’aide d’un webhook

Un webhook vous permet de toostart un runbook donné dans Azure Automation via une requête HTTP unique.  Avant de configurer hello [alerte d’Analytique de journal](../log-analytics/log-analytics-alerts.md#alert-rules) runbook de hello toocall à l’aide d’un webhook comme une action d’alerte, vous devez toofirst créer un webhook pour runbook hello qui sera appelée à l’aide de cette méthode.  Passez en revue et suivez les étapes de hello Bonjour [créer un webhook](automation-webhooks.md#creating-a-webhook) l’article et n’oubliez pas de l’URL du webhook toorecord hello afin que vous pouvez référencer lors de la configuration de règle d’alerte hello.   

## <a name="calling-a-runbook-directly"></a>Appel direct d’un runbook

Si vous avez hello Automation & offre de contrôle installé et configuré dans votre espace de travail OMS, lorsque vous configurez l’option d’actions hello Runbook d’alerte de hello, vous pouvez afficher tous les runbooks à partir de hello **sélectionnez un runbook** liste déroulante et sélectionnez hello spécifique de runbook vous souhaitez toorun dans alerte toohello de réponse.  Hello sélectionné runbook peut s’exécuter dans un espace de travail dans hello cloud Azure ou sur un runbook worker hybride.  Lors de l’alerte de hello est créé à l’aide d’option de runbook hello, un webhook va être créé pour hello runbook.  Vous pouvez voir hello webhook si vous accédez compte Automation de toohello et accédez lame de webhook toohello de runbook de hello sélectionné.  Si vous supprimez hello alerte, hello webhook n’est pas supprimé, mais hello l’utilisateur peut supprimer des hello webhook manuellement.  Il n’est pas un problème si hello webhook n’est pas supprimé, il est simplement un élément orphelin qui devra finalement toobe supprimé dans l’ordre toomaintain un compte Automation sont organisé.  

## <a name="characteristics-of-a-runbook-for-both-options"></a>Caractéristiques d’un runbook (pour les deux méthodes)

Les deux méthodes d’appel de hello runbook d’alerte d’Analytique de journal hello présentent les caractéristiques de comportement différent qui doivent toobe compris avant de configurer vos règles d’alerte.  

* Vous devez disposer d’un paramètre d’entrée de runbook appelé **WebhookData** qui est de type **objet**.  Il peut être obligatoire ou facultatif.  alerte de Hello passe hello recherche résultats toohello runbook à l’aide de ce paramètre d’entrée.

        param  
         (  
          [Parameter (Mandatory=$true)]  
          [object] $WebhookData  
         )

*  Vous devez avoir l’objet de code tooconvert hello WebhookData tooa PowerShell.

    `$SearchResults = (ConvertFrom-Json $WebhookData.RequestBody).SearchResults.value`

    *$SearchResults* est un tableau d’objets ; chaque objet contient des champs de hello avec des valeurs à partir d’un résultat de recherche

### <a name="webhookdata-inconsistencies-between-hello-webhook-option-and-runbook-option"></a>WebhookData les incohérences entre l’option de webhook hello et option de runbook

* Lorsque vous configurez une alerte toocall un Webhook, entrez une URL webhook que vous avez créé pour un runbook, cliquez sur hello **Test Webhook** bouton.  Hello WebhookData résultant envoyé toohello runbook ne contient pas *. Résultats de la recherche* ou *. SearchResults*.

*  Si vous enregistrez cette alerte, lors de l’alerte de hello déclenche et appelle hello webhook, hello WebhookData envoyé toohello runbook contient *. Résultats de la recherche*.
* Si vous créez une alerte et le configurez toocall un runbook (qui crée également un webhook), lorsque hello il envoie WebhookData toohello runbook qui contient les déclencheurs alerte *. SearchResults*.

Par conséquent, dans l’exemple de code hello ci-dessus, vous devez tooget *. Résultats de la recherche* si l’alerte de hello appelle un webhook et devez tooget *. SearchResults* si l’alerte de hello appelle un runbook directement.

## <a name="example-walkthrough"></a>Exemple de procédure pas à pas

Nous allons vous montrer comment cela fonctionne à l’aide de hello suivant l’exemple de runbook graphique, ce qui démarre un service Windows.<br><br> ![Démarrer le runbook graphique d’un service Windows](media/automation-invoke-runbook-from-omsla-alert/automation-runbook-restartservice.png)<br>

Hello runbook possède un paramètre d’entrée de type **objet** appelé **WebhookData** et inclut des données de webhook hello passées à partir de hello alerte contenant *. SearchResults*.<br><br> ![Paramètres d’entrée de runbook](media/automation-invoke-runbook-from-omsla-alert/automation-runbook-restartservice-inputparameter.png)<br>

Pour cet exemple, dans le journal Analytique nous avons créé deux champs personnalisés, *SvcDisplayName_CF* et *SvcState_CF*, tooextract hello service hello nom et l’état d’affichage du service de hello (autrement dit, en cours d’exécution ou arrêté) à partir de l’événement de hello écrites toohello journal des événements système.  Ensuite, nous créons une règle d’alerte avec hello suivant la requête de recherche : `Type=Event SvcDisplayName_CF="Print Spooler" SvcState_CF="stopped"` afin que nous pouvons détecter lorsque hello service Spouleur d’impression est arrêté sur hello système Windows.  Il peut être n’importe quel service qui vous intéresse, mais pour cet exemple nous référençons un des services préexistant hello qui sont incluses avec hello du système d’exploitation Windows.  action d’alerte Hello est configuré tooexecute notre runbook utilisé dans cet exemple et exécuter sur hello Runbook Worker hybride, qui sont activé sur les systèmes cibles de hello.   

Hello d’activité de code runbook **obtenir un nom de Service à partir de LA** convertira la chaîne JSON de hello dans un type d’objet et un filtre sur l’élément de hello *SvcDisplayName_CF* nom d’affichage tooextract hello Hello Windows service et passer cette activité suivante de hello qui vérifiera hello est arrêté avant d’essayer de toorestart il.  *SvcDisplayName_CF* est un [champ personnalisé](../log-analytics/log-analytics-custom-fields.md) créé dans le journal Analytique toodemonstrate cet exemple.

    $SearchResults = (ConvertFrom-Json $WebhookData.RequestBody).SearchResults.value
    $SearchResults.SvcDisplayName_CF  

Lorsque hello service s’arrête, règle d’alerte dans le journal Analytique hello détecte une correspondance et déclencher hello runbook et envoyer hello contexte de l’alerte toohello runbook. Hello runbook effectuera une action tooverify hello service est arrêté, et si donc tentative toorestart hello service et vérifiez que l’opération a démarré correctement et hello de sortie des résultats.     

Vous pouvez également si vous n’avez pas votre espace de travail Automation compte lié tooyour OMS, configurer la règle d’alerte hello avec un runbook de webhook action tootrigger hello et configurer une chaîne JSON hello runbook tooconvert hello et filtre sur *. Résultats de la recherche* suivant les instructions hello mentionnée précédemment.    

## <a name="next-steps"></a>Étapes suivantes

* toolearn plus d’informations sur les alertes dans le journal Analytique et toocreate, voir [alertes dans le journal Analytique](../log-analytics/log-analytics-alerts.md).

* toounderstand runbooks tootrigger à l’aide d’un webhook, voir [Azure Automation webhooks](automation-webhooks.md).
