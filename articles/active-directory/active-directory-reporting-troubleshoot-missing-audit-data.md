---
title: "Résolution des problèmes : Données manquantes dans le journal d’activité Azure Active Directory | Microsoft Docs"
description: "Répertorie les différents rapports disponibles pour Azure Active Directory"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 7cbe4337-bb77-4ee0-b254-3e368be06db7
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 47617f8f727027de113a0f503308c8accc58859e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="i-cant-find-some-actions-that-i-performed-in-the-azure-active-directory-activity-log"></a><span data-ttu-id="af4c6-103">Je ne trouve pas certaines actions que j’ai réalisées dans le journal d’activité d’Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="af4c6-103">I can’t find some actions that I performed in the Azure Active Directory activity log</span></span>


## <a name="symptoms"></a><span data-ttu-id="af4c6-104">Symptômes</span><span class="sxs-lookup"><span data-stu-id="af4c6-104">Symptoms</span></span>

<span data-ttu-id="af4c6-105">J’ai réalisé certaines actions dans le portail Azure et je pensais pouvoir consulter les journaux d’audit associés dans le panneau `Activity logs > Audit Logs`, mais je ne les trouve pas.</span><span class="sxs-lookup"><span data-stu-id="af4c6-105">I performed some actions in the Azure portal and expected to see the audit logs for those actions in the `Activity logs > Audit Logs` blade, but I can’t find them.</span></span>

 ![Reporting](./media/active-directory-reporting-troubleshoot-missing-audit-data/01.png)
 

## <a name="cause"></a><span data-ttu-id="af4c6-107">Cause :</span><span class="sxs-lookup"><span data-stu-id="af4c6-107">Cause</span></span>

<span data-ttu-id="af4c6-108">Les actions n’apparaissent pas immédiatement dans le journal d’audit des activités.</span><span class="sxs-lookup"><span data-stu-id="af4c6-108">Actions don’t appear immediately in the Activity Audit log.</span></span> <span data-ttu-id="af4c6-109">Entre 15 minutes et 1 heure peuvent être nécessaires pour que les journaux d’audit s’affichent dans le portail après l’exécution de l’opération.</span><span class="sxs-lookup"><span data-stu-id="af4c6-109">It can take anywhere from 15 minutes to an hour to see the audit logs in the portal from the time the operation is performed.</span></span>

## <a name="resolution"></a><span data-ttu-id="af4c6-110">Résolution :</span><span class="sxs-lookup"><span data-stu-id="af4c6-110">Resolution</span></span>

<span data-ttu-id="af4c6-111">Attendez entre 15 minutes et 1 heure pour voir si les actions apparaissent dans le journal.</span><span class="sxs-lookup"><span data-stu-id="af4c6-111">Wait for 15 minutes to an hour and see if the actions appear in the log.</span></span> <span data-ttu-id="af4c6-112">Si elles n’apparaissent toujours pas, veuillez créer un ticket de support pour que nous résolvions le problème.</span><span class="sxs-lookup"><span data-stu-id="af4c6-112">If you still don’t see them, please raise a support ticket with us and we will look into it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="af4c6-113">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="af4c6-113">Next steps</span></span>
<span data-ttu-id="af4c6-114">Consultez le [FAQ sur les rapports Azure Active Directory](active-directory-reporting-faq.md).</span><span class="sxs-lookup"><span data-stu-id="af4c6-114">See the [Azure Active Directory reporting FAQ](active-directory-reporting-faq.md).</span></span>

