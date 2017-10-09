---
title: "Ressources d’application Web d’aaaMove tooanother groupe de ressources"
description: "Décrit des scénarios hello où vous pouvez déplacer des applications Web et les Services d’application à partir d’un groupe de ressources tooanother."
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
ms.openlocfilehash: 931012fee656b7f8a4b2c225c38739a9171d3b2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="supported-move-configurations"></a><span data-ttu-id="5496f-103">Configurations de déplacement prises en charge</span><span class="sxs-lookup"><span data-stu-id="5496f-103">Supported Move Configurations</span></span>
<span data-ttu-id="5496f-104">Vous pouvez déplacer des ressources de l’application Web Azure à l’aide de hello [API ressources déplacer du Gestionnaire de ressources](../azure-resource-manager/resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="5496f-104">You can move Azure Web App resources using hello [Resource Manager Move Resources API](../azure-resource-manager/resource-group-move-resources.md).</span></span>

<span data-ttu-id="5496f-105">Les applications Web Azure prend actuellement en charge hello déplacer les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="5496f-105">Azure Web Apps currently supports hello following move scenarios:</span></span>

* <span data-ttu-id="5496f-106">Déplacer hello tout le contenu d’un groupe de ressources (les applications web, les plans de service d’application et les certificats) groupe de ressources tooanother.</span><span class="sxs-lookup"><span data-stu-id="5496f-106">Move hello entire contents of a resource group (web apps, app service plans, and certificates) tooanother resource group.</span></span> 
   > [!Note]
   > <span data-ttu-id="5496f-107">groupe de ressources Hello destination ne peut pas contenir toutes les ressources Microsoft.Web dans ce scénario.</span><span class="sxs-lookup"><span data-stu-id="5496f-107">hello destination resource group can not contain any Microsoft.Web resources in this scenario.</span></span>

* <span data-ttu-id="5496f-108">Déplacer le groupe de ressources différent de tooa des applications web individuelles, tout en hébergeant les dans leur plan app service en cours (hello app service plan reste dans le groupe de ressources ancien hello).</span><span class="sxs-lookup"><span data-stu-id="5496f-108">Move individual web apps tooa different resource group, while still hosting them in their current app service plan (hello app service plan stays in hello old resource group).</span></span>


