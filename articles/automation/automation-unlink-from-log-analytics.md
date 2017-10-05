---
title: "Supprimer le lien d’un compte Azure Automation dans Log Analytics | Microsoft Docs"
description: "Cet article décrit comment supprimer le lien votre compte Azure Automation dans un espace de travail OMS."
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
ms.openlocfilehash: 56b09c2cfc14813b5efcb364c580787fec1bf639
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-unlink-your-automation-account-from-a-log-analytics-workspace"></a><span data-ttu-id="c775f-103">Comment supprimer le lien de votre compte Automation dans un espace de travail Log Analytics</span><span class="sxs-lookup"><span data-stu-id="c775f-103">How to unlink your Automation account from a Log Analytics workspace</span></span>

<span data-ttu-id="c775f-104">Azure Automation s’intègre dans Log Analytics non seulement pour assurer une surveillance proactive de vos travaux de Runbook sur l’ensemble de vos comptes Automation, mais il est indispensable lorsque vous importez les solutions suivantes qui dépendent de Log Analytics :</span><span class="sxs-lookup"><span data-stu-id="c775f-104">Azure Automation integrates with Log Analytics to not only support proactive monitoring of your runbook jobs across all of your Automation accounts, but is also required when you import the following solutions that are dependent on Log Analytics:</span></span>

* [<span data-ttu-id="c775f-105">Gestion des mises à jour</span><span class="sxs-lookup"><span data-stu-id="c775f-105">Update Management</span></span>](../operations-management-suite/oms-solution-update-management.md)
* [<span data-ttu-id="c775f-106">Suivi des modifications</span><span class="sxs-lookup"><span data-stu-id="c775f-106">Change Tracking</span></span>](../log-analytics/log-analytics-change-tracking.md)
* [<span data-ttu-id="c775f-107">Démarrer/arrêter des machines virtuelles pendant les heures creuses</span><span class="sxs-lookup"><span data-stu-id="c775f-107">Start/Stop VMs during off-hours</span></span>](automation-solution-vm-management.md)
 
<span data-ttu-id="c775f-108">Si vous ne souhaitez plus intégrer votre compte Automation dans Log Analytics, vous pouvez supprimer son lien directement dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c775f-108">If you decide you no longer wish to integrate your Automation account with Log Analytics, you can unlink your account directly from the Azure portal.</span></span>  <span data-ttu-id="c775f-109">Avant toute chose, vous devez supprimer les solutions mentionnées précédemment. Sinon, la procédure ne pourra pas aboutir.</span><span class="sxs-lookup"><span data-stu-id="c775f-109">Before you proceed, you will first need to remove the solutions mentioned earlier, otherwise this process will be prevented from proceeding.</span></span>  <span data-ttu-id="c775f-110">Consultez la rubrique relative à la solution que vous avez importée pour comprendre sa procédure de suppression.</span><span class="sxs-lookup"><span data-stu-id="c775f-110">Review the topic for the particular solution you have imported to understand the steps required to remove it.</span></span>  

<span data-ttu-id="c775f-111">Après avoir supprimé ces solutions, vous pouvez effectuer les étapes suivantes pour supprimer le lien de votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="c775f-111">After you remove these solutions you can perform the following steps to unlink your Automation account.</span></span>

## <a name="unlink-workspace"></a><span data-ttu-id="c775f-112">Supprimer le lien de votre espace de travail</span><span class="sxs-lookup"><span data-stu-id="c775f-112">Unlink workspace</span></span>

1. <span data-ttu-id="c775f-113">Dans le portail Azure, ouvrez votre compte Automation puis, dans le panneau de ce dernier, sélectionnez **Unlink workspace (Supprimer le lien de l’espace de travail)**.</span><span class="sxs-lookup"><span data-stu-id="c775f-113">From the Azure portal, open your Automation account, and in the Automation account blade, in the account blade, select **Unlink workspace**.</span></span><br><br> <span data-ttu-id="c775f-114">![Option Unlink workspace (Supprimer le lien de l’espace de travail)](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)</span><span class="sxs-lookup"><span data-stu-id="c775f-114">![Unlink workspace option](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)</span></span><br><br>  
2. <span data-ttu-id="c775f-115">Dans le panneau Unlink workspace (Supprimer le lien de l’espace de travail), cliquez sur **Unlink workspace (Supprimer le lien de l’espace de travail)**.</span><span class="sxs-lookup"><span data-stu-id="c775f-115">On the Unlink workspace blade, click **Unlink worksapce**.</span></span><br><br> <span data-ttu-id="c775f-116">![Panneau Unlink workspace (Supprimer le lien de l’espace de travail)](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).</span><span class="sxs-lookup"><span data-stu-id="c775f-116">![Unlink workspace blade](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).</span></span><br><br>  <span data-ttu-id="c775f-117">Vous recevez une invite de confirmation de la suppression.</span><span class="sxs-lookup"><span data-stu-id="c775f-117">You will receive a prompt verifying you wish to proceed.</span></span><br><br>
3. <span data-ttu-id="c775f-118">Pour suivre la progression de la suppression du lien de votre espace de travail Log Analytics dans Azure Automation, sélectionnez **Notifications** dans le menu.</span><span class="sxs-lookup"><span data-stu-id="c775f-118">While Azure Automation attempts to unlink the account your Log Analytics workspace, you can track the progress under **Notifications** from the menu.</span></span>

<span data-ttu-id="c775f-119">Si vous avez utilisé la solution de gestion de la mise à jour, vous pouvez (si vous le souhaitez) supprimer les éléments suivants qui ne sont plus nécessaires après la suppression de la solution.</span><span class="sxs-lookup"><span data-stu-id="c775f-119">If you used the Update Management solution, optionally you may want to remove the following items that are no longer needed after you remove the solution.</span></span>

* <span data-ttu-id="c775f-120">Planifications de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="c775f-120">Update schedules.</span></span>  <span data-ttu-id="c775f-121">Chacune aura un nom correspondant aux déploiements de mise à jour que vous avez créés.</span><span class="sxs-lookup"><span data-stu-id="c775f-121">Each will have names that match the update deployments you created)</span></span>

* <span data-ttu-id="c775f-122">Groupes de travail hybrides créés pour la solution.</span><span class="sxs-lookup"><span data-stu-id="c775f-122">Hybrid worker groups created for the solution.</span></span>  <span data-ttu-id="c775f-123">Chacun a un nom similaire à machine1.contoso.com_9ceb8108-26c9-4051-b6b3-227600d715c8.</span><span class="sxs-lookup"><span data-stu-id="c775f-123">Each will be named similarly to  machine1.contoso.com_9ceb8108-26c9-4051-b6b3-227600d715c8).</span></span>

<span data-ttu-id="c775f-124">Si vous avez utilisé la solution Démarrer/arrêter des machines virtuelles pendant les heures creuses, vous pouvez (si vous le souhaitez) supprimer les éléments suivants qui ne sont plus nécessaires après la suppression de la solution.</span><span class="sxs-lookup"><span data-stu-id="c775f-124">If you used the Start/Stop VMs during off-hours solution, optionally you may want to remove the following items that are no longer needed after you remove the solution.</span></span>

* <span data-ttu-id="c775f-125">Start and stop VM runbook schedules (Démarrer et arrêter les planifications de Runbook de machine virtuelle)</span><span class="sxs-lookup"><span data-stu-id="c775f-125">Start and stop VM runbook schedules</span></span> 
* <span data-ttu-id="c775f-126">Start and stop VM runbooks (Démarrer et arrêter les Runbooks de machine virtuelle)</span><span class="sxs-lookup"><span data-stu-id="c775f-126">Start and stop VM runbooks</span></span>
* <span data-ttu-id="c775f-127">Variables</span><span class="sxs-lookup"><span data-stu-id="c775f-127">Variables</span></span>   

## <a name="next-steps"></a><span data-ttu-id="c775f-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c775f-128">Next steps</span></span>

<span data-ttu-id="c775f-129">Pour reconfigurer votre compte Automation et l’intégrer dans OMS Log Analytics, consultez [Transférer l’état d’un travail et des flux de travail d’Automation vers Log Analytics (OMS)](automation-manage-send-joblogs-log-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="c775f-129">To reconfigure your Automation account to integrate with OMS Log Analytics, see [Forward job status and job streams from Automation to Log Analytics (OMS)](automation-manage-send-joblogs-log-analytics.md).</span></span> 