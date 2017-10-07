---
title: "aaaUser Action initiée par Azure Automation Runbook dans le journal Analytique | Documents Microsoft"
description: "Cet article décrit comment toorun un runbook Automation à partir d’un Analytique de journal recherche le résultat à la demande."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/04/2017
ms.author: magoedte
ms.openlocfilehash: 53c25431572babd5fd54bf964e4683077e2a4c2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="take-action-with-an-automation-runbook-from-a-log-analytics-log-search-result"></a>Utilisation d’un runbook Automation sur un résultat de recherche dans les journaux Log Analytics

À partir d’un résultat de recherche de journal dans l’Analytique des journaux Azure, vous pouvez maintenant sélectionner **prendre des mesures** toorun un runbook Automation.  Hello runbook peut être utilisé tooremediate hello problème ou effectuer d’autres actions telles que de collecter des informations de dépannage, envoyer un courrier électronique ou créer une demande de service. 

## <a name="components-and-features-used"></a>Composants et fonctionnalités utilisés
* [Compte Azure Automation](../automation/automation-offering-get-started.md)
* [Espace de travail Log Analytics](../log-analytics/log-analytics-overview.md)

## <a name="tooinitiate-runbook-from-log-search"></a>runbook tooinitiate à partir de la recherche de journal

action tootake sur un événement et le lancement d’un runbook à partir de vos résultats de recherche de journal, commencez par créer une recherche de journal et à partir des résultats de hello, vous pouvez appeler une runbook à la demande.  Cela peut être obtenue à partir de la fonctionnalité de recherche de journal hello Bonjour Azure ou [portail OMS](../log-analytics/log-analytics-log-searches.md).  Dans cet exemple, nous effectuons une recherche de journal à partir de hello portail Azure avec une démonstration de base de cette fonctionnalité.

1. Dans hello portail Azure, cliquez sur le menu du Hub hello **davantage de services** et sélectionnez **Analytique de journal**.  
2. Dans Panneau de journal Analytique hello, sélectionnez votre espace de travail Analytique de journal puis sur Panneau espace de travail de hello **recherche de journal**.  
3. Dans Panneau de recherche de journal hello, effectuer une recherche de journal.  
4. À partir des résultats de recherche de journal hello, cliquez sur la gauche de toohello hello ellipse de l’un des champs de hello et à partir de la fenêtre contextuelle hello, sélectionnez **agissent sur**.<br><br> ![Sélectionner Agir à partir des résultats de recherche](./media/log-analytics-log-search-takeaction/log-search-takeaction-menuoption.png) 
5. Dans le panneau de hello Take action, sélectionnez **exécuter un runbook**et sur hello **exécuter un runbook** panneau que vous pouvez sélectionner un toorun runbook.  Vous pouvez sélectionner n’importe quel runbook Bonjour compte Automation qui est l’espace de travail lié toohello Analytique de journal.  Notez hello suivantes :

    * Les runbooks sont organisés par balise
    * Les valeurs de paramètre d’entrée de Runbook peuvent être sélectionnés directement à partir de champs hello du résultat de la recherche hello.  Une liste déroulante apparaît affichant tous les champs disponibles hello de tooselect de résultat hello à partir de.  
    * Vous pouvez choisir toorun hello runbook sur un [runbook worker hybride](../automation/automation-hybrid-runbook-worker.md) que vous avez installé sur l’ordinateur hello qui a le problème de hello si vous avez un groupe de travail de Runbook hybride correspondant qui ne contient que cet ordinateur en tant que membre.  Si le nom hello du groupe de travail hybride hello correspond au nom hello d’ordinateur hello en résultat de recherche de journal hello, groupe de hello est sélectionné automatiquement.    

6. Après avoir cliqué sur **exécuter**, hello runbook travail panneau tooallow vous tooreview hello état du travail de hello.   

Si vous sélectionnez un runbook qui a été configuré toobe [appelée à partir d’une alerte d’Analytique de journal](../automation/automation-invoke-runbook-from-omsla-alert.md), il a un paramètre d’entrée appelé **WebhookData** qui est **objet** type.  Si le paramètre d’entrée hello est obligatoire, vous devez toopass hello recherche résultats toohello runbook et il peut convertir la chaîne JSON de hello dans un type d’objet qui vous toofilter sur des éléments spécifiques que vous allez référencer dans les activités de runbook.  Pour cela, sélectionnez **(objet) de résultat de la recherche** à partir de la liste déroulante de hello.<br><br> ![Sélectionner un objet de données Webhook pour le paramètre de runbook](media/log-analytics-log-search-takeaction/select-runbook-and-properties.png)   
    
## <a name="next-steps"></a>Étapes suivantes

* Hello de révision [Analytique de journal journal référence de recherche](log-analytics-search-reference.md) tooview tous les Hello recherche des champs et facettes disponibles dans le journal Analytique.
* toolearn comment tooinvoke un runbook Automation automatiquement, consultez [appeler un runbook Azure Automation à partir d’une alerte de l’Analytique des journaux OMS](../automation/automation-invoke-runbook-from-omsla-alert.md).  
