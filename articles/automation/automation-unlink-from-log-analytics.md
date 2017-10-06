---
title: "aaaUnlink compte Azure Automation à partir de l’Analytique des journaux | Documents Microsoft"
description: "Cet article fournit une vue d’ensemble de toounlink comment votre Azure Automation compte à partir d’un espace de travail OMS."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: how-to-article
ms.date: 02/07/2017
ms.author: magoedte
ms.openlocfilehash: 3ec0745673f6a872538d33023a7a1d2bb1d18ec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toounlink-your-automation-account-from-a-log-analytics-workspace"></a>Comment toounlink votre automatisation de compte à partir d’un espace de travail Analytique des journaux

Azure Automation s’intègre à Analytique de journal toonot uniquement prise en charge une analyse proactive de vos travaux de runbook dans l’ensemble de vos comptes Automation, mais il est également requise lorsque vous importez hello suivant des solutions qui sont dépendantes de l’Analytique des journaux :

* [Gestion des mises à jour](../operations-management-suite/oms-solution-update-management.md)
* [Suivi des modifications](../log-analytics/log-analytics-change-tracking.md)
* [Démarrer/arrêter des machines virtuelles pendant les heures creuses](automation-solution-vm-management.md)
 
Si vous décidez que vous ne souhaitez plus toointegrate votre compte Automation avec Analytique de journal, vous pouvez dissocier votre compte directement à partir de hello portail Azure.  Avant de continuer, vous devez tout d’abord les solutions de hello tooremove mentionnées précédemment, sinon ce processus ne pourra pas se poursuivre.  Rubrique de hello révision pour une solution spécifique de hello vous avez importé des étapes hello toounderstand tooremove il.  

Après la suppression de ces solutions vous pouvez effectuer hello suivant les étapes toounlink votre compte Automation.

## <a name="unlink-workspace"></a>Supprimer le lien de votre espace de travail

1. À partir de hello portail Azure, ouvrez votre compte Automation et dans le panneau de compte Automation hello, dans le panneau de compte hello, sélectionnez **dissocier l’espace de travail**.<br><br> ![Option Unlink workspace (Supprimer le lien de l’espace de travail)](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)<br><br>  
2. Dans le panneau espace de travail de dissocier la hello, cliquez sur **dissocier l’espace de travail**.<br><br> ![Panneau Unlink workspace (Supprimer le lien de l’espace de travail)](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).<br><br>  Vous recevez une invite de vérification que vous souhaitez tooproceed.<br><br>
3. Alors que Azure Automation tente de compte de hello toounlink votre espace de travail Analytique des journaux, vous pouvez suivre la progression de hello sous **Notifications** à partir du menu de hello.

Si vous avez utilisé la solution de gestion de la mise à jour de hello, éventuellement vous souhaiterez hello tooremove les éléments qui ne sont plus nécessaires après la suppression de la solution de hello suivants.

* Planifications de mise à jour.  Chacune aura des noms qui correspondent à des déploiements de mises à jour hello que vous avez créé)

* Groupes de travail hybride créés pour la solution de hello.  Chacun est nommé de la même façon trop machine1.contoso.com_9ceb8108 - 26 c 9-4051-b6b3-227600d715c8).

Si vous avez utilisé des machines virtuelles de démarrage/arrêt hello au cours de la solution d’heures creuses, éventuellement vous souhaiterez hello tooremove les éléments qui ne sont plus nécessaires après la suppression de la solution de hello suivants.

* Start and stop VM runbook schedules (Démarrer et arrêter les planifications de Runbook de machine virtuelle) 
* Start and stop VM runbooks (Démarrer et arrêter les Runbooks de machine virtuelle)
* Variables   

## <a name="next-steps"></a>Étapes suivantes

reportez-vous à votre toointegrate de compte Automation avec Analytique de journal d’OMS, tooreconfigure [transférer l’état du travail et flux de travail à partir de l’Automation tooLog Analytique (OMS)](automation-manage-send-joblogs-log-analytics.md). 
