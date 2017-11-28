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
# <a name="how-toounlink-your-automation-account-from-a-log-analytics-workspace"></a><span data-ttu-id="4da92-103">Comment toounlink votre automatisation de compte à partir d’un espace de travail Analytique des journaux</span><span class="sxs-lookup"><span data-stu-id="4da92-103">How toounlink your Automation account from a Log Analytics workspace</span></span>

<span data-ttu-id="4da92-104">Azure Automation s’intègre à Analytique de journal toonot uniquement prise en charge une analyse proactive de vos travaux de runbook dans l’ensemble de vos comptes Automation, mais il est également requise lorsque vous importez hello suivant des solutions qui sont dépendantes de l’Analytique des journaux :</span><span class="sxs-lookup"><span data-stu-id="4da92-104">Azure Automation integrates with Log Analytics toonot only support proactive monitoring of your runbook jobs across all of your Automation accounts, but is also required when you import hello following solutions that are dependent on Log Analytics:</span></span>

* [<span data-ttu-id="4da92-105">Gestion des mises à jour</span><span class="sxs-lookup"><span data-stu-id="4da92-105">Update Management</span></span>](../operations-management-suite/oms-solution-update-management.md)
* [<span data-ttu-id="4da92-106">Suivi des modifications</span><span class="sxs-lookup"><span data-stu-id="4da92-106">Change Tracking</span></span>](../log-analytics/log-analytics-change-tracking.md)
* [<span data-ttu-id="4da92-107">Démarrer/arrêter des machines virtuelles pendant les heures creuses</span><span class="sxs-lookup"><span data-stu-id="4da92-107">Start/Stop VMs during off-hours</span></span>](automation-solution-vm-management.md)
 
<span data-ttu-id="4da92-108">Si vous décidez que vous ne souhaitez plus toointegrate votre compte Automation avec Analytique de journal, vous pouvez dissocier votre compte directement à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="4da92-108">If you decide you no longer wish toointegrate your Automation account with Log Analytics, you can unlink your account directly from hello Azure portal.</span></span>  <span data-ttu-id="4da92-109">Avant de continuer, vous devez tout d’abord les solutions de hello tooremove mentionnées précédemment, sinon ce processus ne pourra pas se poursuivre.</span><span class="sxs-lookup"><span data-stu-id="4da92-109">Before you proceed, you will first need tooremove hello solutions mentioned earlier, otherwise this process will be prevented from proceeding.</span></span>  <span data-ttu-id="4da92-110">Rubrique de hello révision pour une solution spécifique de hello vous avez importé des étapes hello toounderstand tooremove il.</span><span class="sxs-lookup"><span data-stu-id="4da92-110">Review hello topic for hello particular solution you have imported toounderstand hello steps required tooremove it.</span></span>  

<span data-ttu-id="4da92-111">Après la suppression de ces solutions vous pouvez effectuer hello suivant les étapes toounlink votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="4da92-111">After you remove these solutions you can perform hello following steps toounlink your Automation account.</span></span>

## <a name="unlink-workspace"></a><span data-ttu-id="4da92-112">Supprimer le lien de votre espace de travail</span><span class="sxs-lookup"><span data-stu-id="4da92-112">Unlink workspace</span></span>

1. <span data-ttu-id="4da92-113">À partir de hello portail Azure, ouvrez votre compte Automation et dans le panneau de compte Automation hello, dans le panneau de compte hello, sélectionnez **dissocier l’espace de travail**.</span><span class="sxs-lookup"><span data-stu-id="4da92-113">From hello Azure portal, open your Automation account, and in hello Automation account blade, in hello account blade, select **Unlink workspace**.</span></span><br><br> <span data-ttu-id="4da92-114">![Option Unlink workspace (Supprimer le lien de l’espace de travail)](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)</span><span class="sxs-lookup"><span data-stu-id="4da92-114">![Unlink workspace option](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)</span></span><br><br>  
2. <span data-ttu-id="4da92-115">Dans le panneau espace de travail de dissocier la hello, cliquez sur **dissocier l’espace de travail**.</span><span class="sxs-lookup"><span data-stu-id="4da92-115">On hello Unlink workspace blade, click **Unlink worksapce**.</span></span><br><br> <span data-ttu-id="4da92-116">![Panneau Unlink workspace (Supprimer le lien de l’espace de travail)](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).</span><span class="sxs-lookup"><span data-stu-id="4da92-116">![Unlink workspace blade](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).</span></span><br><br>  <span data-ttu-id="4da92-117">Vous recevez une invite de vérification que vous souhaitez tooproceed.</span><span class="sxs-lookup"><span data-stu-id="4da92-117">You will receive a prompt verifying you wish tooproceed.</span></span><br><br>
3. <span data-ttu-id="4da92-118">Alors que Azure Automation tente de compte de hello toounlink votre espace de travail Analytique des journaux, vous pouvez suivre la progression de hello sous **Notifications** à partir du menu de hello.</span><span class="sxs-lookup"><span data-stu-id="4da92-118">While Azure Automation attempts toounlink hello account your Log Analytics workspace, you can track hello progress under **Notifications** from hello menu.</span></span>

<span data-ttu-id="4da92-119">Si vous avez utilisé la solution de gestion de la mise à jour de hello, éventuellement vous souhaiterez hello tooremove les éléments qui ne sont plus nécessaires après la suppression de la solution de hello suivants.</span><span class="sxs-lookup"><span data-stu-id="4da92-119">If you used hello Update Management solution, optionally you may want tooremove hello following items that are no longer needed after you remove hello solution.</span></span>

* <span data-ttu-id="4da92-120">Planifications de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="4da92-120">Update schedules.</span></span>  <span data-ttu-id="4da92-121">Chacune aura des noms qui correspondent à des déploiements de mises à jour hello que vous avez créé)</span><span class="sxs-lookup"><span data-stu-id="4da92-121">Each will have names that match hello update deployments you created)</span></span>

* <span data-ttu-id="4da92-122">Groupes de travail hybride créés pour la solution de hello.</span><span class="sxs-lookup"><span data-stu-id="4da92-122">Hybrid worker groups created for hello solution.</span></span>  <span data-ttu-id="4da92-123">Chacun est nommé de la même façon trop machine1.contoso.com_9ceb8108 - 26 c 9-4051-b6b3-227600d715c8).</span><span class="sxs-lookup"><span data-stu-id="4da92-123">Each will be named similarly too machine1.contoso.com_9ceb8108-26c9-4051-b6b3-227600d715c8).</span></span>

<span data-ttu-id="4da92-124">Si vous avez utilisé des machines virtuelles de démarrage/arrêt hello au cours de la solution d’heures creuses, éventuellement vous souhaiterez hello tooremove les éléments qui ne sont plus nécessaires après la suppression de la solution de hello suivants.</span><span class="sxs-lookup"><span data-stu-id="4da92-124">If you used hello Start/Stop VMs during off-hours solution, optionally you may want tooremove hello following items that are no longer needed after you remove hello solution.</span></span>

* <span data-ttu-id="4da92-125">Start and stop VM runbook schedules (Démarrer et arrêter les planifications de Runbook de machine virtuelle)</span><span class="sxs-lookup"><span data-stu-id="4da92-125">Start and stop VM runbook schedules</span></span> 
* <span data-ttu-id="4da92-126">Start and stop VM runbooks (Démarrer et arrêter les Runbooks de machine virtuelle)</span><span class="sxs-lookup"><span data-stu-id="4da92-126">Start and stop VM runbooks</span></span>
* <span data-ttu-id="4da92-127">Variables</span><span class="sxs-lookup"><span data-stu-id="4da92-127">Variables</span></span>   

## <a name="next-steps"></a><span data-ttu-id="4da92-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4da92-128">Next steps</span></span>

<span data-ttu-id="4da92-129">reportez-vous à votre toointegrate de compte Automation avec Analytique de journal d’OMS, tooreconfigure [transférer l’état du travail et flux de travail à partir de l’Automation tooLog Analytique (OMS)](automation-manage-send-joblogs-log-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="4da92-129">tooreconfigure your Automation account toointegrate with OMS Log Analytics, see [Forward job status and job streams from Automation tooLog Analytics (OMS)](automation-manage-send-joblogs-log-analytics.md).</span></span> 
