---
title: "Résolution des problèmes : Données manquantes dans les journaux d’activité Azure Active Directory téléchargés | Microsoft Docs"
description: "Fournit une résolution au problème de données manquantes dans les journaux d’activité Azure Active Directory téléchargés."
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
ms.openlocfilehash: 3d56f89035da4d1a0074256b165663f81fc2b01e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="i-cant-find-any-data-in-the-azure-active-directory-activity-logs-i-have-downloaded"></a><span data-ttu-id="606dd-103">Aucune donnée n’apparaît dans les journaux d’activité Azure Active Directory que j’ai téléchargés</span><span class="sxs-lookup"><span data-stu-id="606dd-103">I can’t find any data in the Azure Active Directory activity logs I have downloaded</span></span>


## <a name="symptoms"></a><span data-ttu-id="606dd-104">Symptômes</span><span class="sxs-lookup"><span data-stu-id="606dd-104">Symptoms</span></span>

<span data-ttu-id="606dd-105">J’ai téléchargé les journaux d’activité (d’audit ou de connexion) et tous les enregistrements correspondant à la période choisie n’apparaissent pas.</span><span class="sxs-lookup"><span data-stu-id="606dd-105">I downloaded the activity logs (audit or sign-ins) and I don’t see all the records for the time I chose.</span></span> <span data-ttu-id="606dd-106">Pourquoi ?</span><span class="sxs-lookup"><span data-stu-id="606dd-106">Why?</span></span> 

 ![Reporting](./media/active-directory-reporting-troubleshoot-missing-data-download/01.png)
 

## <a name="cause"></a><span data-ttu-id="606dd-108">Cause :</span><span class="sxs-lookup"><span data-stu-id="606dd-108">Cause</span></span>

<span data-ttu-id="606dd-109">Lorsque vous téléchargez des journaux d’activité dans le portail Azure, nous limitons l’échelle à des enregistrements de 120 Ko, triés du plus récent au moins récent.</span><span class="sxs-lookup"><span data-stu-id="606dd-109">When you download activity logs in the Azure portal, we limit the scale to 120K records, sorted by most recent.</span></span> 

## <a name="resolution"></a><span data-ttu-id="606dd-110">Résolution :</span><span class="sxs-lookup"><span data-stu-id="606dd-110">Resolution</span></span>

<span data-ttu-id="606dd-111">Vous pouvez tirer parti des [API de création de rapports Azure AD](active-directory-reporting-api-getting-started.md) pour extraire jusqu’à un million d’enregistrements pour un point donné.</span><span class="sxs-lookup"><span data-stu-id="606dd-111">You can leverage [Azure AD Reporting APIs](active-directory-reporting-api-getting-started.md) to fetch up to a million records at any given point.</span></span> <span data-ttu-id="606dd-112">Nous vous recommandons d’exécuter un script de façon planifiée qui appelle les API de création de rapports pour extraire des enregistrements de manière incrémentielle sur une période donnée (par exemple, quotidienne ou hebdomadaire).</span><span class="sxs-lookup"><span data-stu-id="606dd-112">Our recommended approach is to run a script on a scheduled basis that calls the reporting APIs to fetch records in an incremental fashion over a period of time (e.g., daily or weekly).</span></span>

## <a name="next-steps"></a><span data-ttu-id="606dd-113">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="606dd-113">Next steps</span></span>
<span data-ttu-id="606dd-114">Consultez le [FAQ sur les rapports Azure Active Directory](active-directory-reporting-faq.md).</span><span class="sxs-lookup"><span data-stu-id="606dd-114">See the [Azure Active Directory reporting FAQ](active-directory-reporting-faq.md).</span></span>

