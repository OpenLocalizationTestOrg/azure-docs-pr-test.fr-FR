---
title: "Déplacer des ressources d’application web vers un autre groupe de ressources"
description: "Décrit les scénarios dans lesquels vous pouvez déplacer des applications web et services d’application d’un groupe de ressources vers un autre."
services: app-service
documentationcenter: 
author: ZainRizvi
manager: erikre
editor: 
ms.assetid: 22f97607-072e-4d1f-a46f-8d500420c33c
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: zarizvi
ms.openlocfilehash: 1b5059dc052005b6079f70ecf6771a3771df8d87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="supported-move-configurations"></a><span data-ttu-id="5d606-103">Configurations de déplacement prises en charge</span><span class="sxs-lookup"><span data-stu-id="5d606-103">Supported Move Configurations</span></span>
<span data-ttu-id="5d606-104">Vous pouvez déplacer des ressources d’application web Azure à l’aide de l’[API de déplacement des ressources Azure Manager](../azure-resource-manager/resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="5d606-104">You can move Azure Web App resources using the [Resource Manager Move Resources API](../azure-resource-manager/resource-group-move-resources.md).</span></span>

<span data-ttu-id="5d606-105">Les applications web Azure prennent actuellement en charge les scénarios de déplacement suivants :</span><span class="sxs-lookup"><span data-stu-id="5d606-105">Azure Web Apps currently supports the following move scenarios:</span></span>

* <span data-ttu-id="5d606-106">Déplacez tout le contenu d’un groupe de ressources (applications web, plans de service d’application et certificats) vers un autre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="5d606-106">Move the entire contents of a resource group (web apps, app service plans, and certificates) to another resource group.</span></span> 
   > [!Note]
   > <span data-ttu-id="5d606-107">Le groupe de ressources de destination ne peut pas contenir de ressources Microsoft.Web dans ce scénario.</span><span class="sxs-lookup"><span data-stu-id="5d606-107">The destination resource group can not contain any Microsoft.Web resources in this scenario.</span></span>

* <span data-ttu-id="5d606-108">Déplacez des applications web individuelles vers un groupe de ressources différent, tout en les hébergeant toujours dans leur plan de service d’application actuel (le plan de service d’application reste dans l’ancien groupe de ressources).</span><span class="sxs-lookup"><span data-stu-id="5d606-108">Move individual web apps to a different resource group, while still hosting them in their current app service plan (the app service plan stays in the old resource group).</span></span>


