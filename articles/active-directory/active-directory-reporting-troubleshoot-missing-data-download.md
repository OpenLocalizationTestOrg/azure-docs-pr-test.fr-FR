---
title: "Résolution des problèmes : Les données manquantes dans hello téléchargement les journaux d’activité Azure Active Directory | Documents Microsoft"
description: "Vous fournit des données toomissing résolution dans le journal d’activité de Azure Active Directory téléchargé."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ffce7eb1-99da-4ea7-9c4d-2322b755c8ce
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 027b70e6efc570f81d3c836f50ee52aaa89be71a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="i-cant-find-any-data-in-hello-azure-active-directory-activity-logs-i-have-downloaded"></a><span data-ttu-id="dae07-103">Impossible de trouver des données dans les journaux d’activité Azure Active Directory hello téléchargés</span><span class="sxs-lookup"><span data-stu-id="dae07-103">I can’t find any data in hello Azure Active Directory activity logs I have downloaded</span></span>


## <a name="symptoms"></a><span data-ttu-id="dae07-104">Symptômes</span><span class="sxs-lookup"><span data-stu-id="dae07-104">Symptoms</span></span>

<span data-ttu-id="dae07-105">Télécharger les journaux d’activité hello (audit ou connexions) et ne sont pas tous les enregistrements de hello pendant hello, que vous avez choisi.</span><span class="sxs-lookup"><span data-stu-id="dae07-105">I downloaded hello activity logs (audit or sign-ins) and I don’t see all hello records for hello time I chose.</span></span> <span data-ttu-id="dae07-106">Pourquoi ?</span><span class="sxs-lookup"><span data-stu-id="dae07-106">Why?</span></span> 

 ![Reporting](./media/active-directory-reporting-troubleshoot-missing-data-download/01.png)
 

## <a name="cause"></a><span data-ttu-id="dae07-108">Cause :</span><span class="sxs-lookup"><span data-stu-id="dae07-108">Cause</span></span>

<span data-ttu-id="dae07-109">Lorsque vous téléchargez les journaux d’activité Bonjour portail Azure, nous limitons enregistrements too120K hello échelle triés par la plupart des récentes.</span><span class="sxs-lookup"><span data-stu-id="dae07-109">When you download activity logs in hello Azure portal, we limit hello scale too120K records, sorted by most recent.</span></span> 

## <a name="resolution"></a><span data-ttu-id="dae07-110">Résolution :</span><span class="sxs-lookup"><span data-stu-id="dae07-110">Resolution</span></span>

<span data-ttu-id="dae07-111">Vous pouvez tirer parti de [API de création de rapports AD Azure](active-directory-reporting-api-getting-started.md) toofetch des enregistrements tooa millions à un moment donné.</span><span class="sxs-lookup"><span data-stu-id="dae07-111">You can leverage [Azure AD Reporting APIs](active-directory-reporting-api-getting-started.md) toofetch up tooa million records at any given point.</span></span> <span data-ttu-id="dae07-112">Notre approche recommandée est toorun un script selon une planification qui appelle hello reporting API toofetch enregistre de manière incrémentielle sur une période de temps (par exemple, quotidienne ou hebdomadaire).</span><span class="sxs-lookup"><span data-stu-id="dae07-112">Our recommended approach is toorun a script on a scheduled basis that calls hello reporting APIs toofetch records in an incremental fashion over a period of time (e.g., daily or weekly).</span></span>

## <a name="next-steps"></a><span data-ttu-id="dae07-113">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dae07-113">Next steps</span></span>
<span data-ttu-id="dae07-114">Consultez hello [Azure Active Directory reporting FAQ](active-directory-reporting-faq.md).</span><span class="sxs-lookup"><span data-stu-id="dae07-114">See hello [Azure Active Directory reporting FAQ](active-directory-reporting-faq.md).</span></span>

