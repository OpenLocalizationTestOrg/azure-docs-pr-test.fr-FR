---
title: Azure Batch Analytics | Microsoft Docs
description: "Référence pour Azure Batch Analytics."
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: 7d634e1bb595a84b8af339e5bc5a483a7849e7f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="batch-analytics"></a><span data-ttu-id="1acee-103">Analyse en mode batch</span><span class="sxs-lookup"><span data-stu-id="1acee-103">Batch Analytics</span></span>
<span data-ttu-id="1acee-104">Les rubriques relatives à l’analyse en mode batch contiennent des informations de référence concernant les événements et alertes disponibles pour les ressources de service Batch.</span><span class="sxs-lookup"><span data-stu-id="1acee-104">The topics in Batch Analytics contain reference information for the events and alerts available for Batch service resources.</span></span>

<span data-ttu-id="1acee-105">Pour plus d’informations sur l’activation et l’utilisation des journaux de diagnostic de Batch, voir [Journalisation des diagnostics Azure Batch](https://azure.microsoft.com/documentation/articles/batch-diagnostics/).</span><span class="sxs-lookup"><span data-stu-id="1acee-105">See [Azure Batch diagnostic logging](https://azure.microsoft.com/documentation/articles/batch-diagnostics/) for more information on enabling and consuming Batch diagnostic logs.</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="1acee-106">Journaux de diagnostic</span><span class="sxs-lookup"><span data-stu-id="1acee-106">Diagnostic logs</span></span>

<span data-ttu-id="1acee-107">Le service Microsoft Azure Batch émet les événements de journal de diagnostic suivants pendant la durée de vie de certaines ressources Batch.</span><span class="sxs-lookup"><span data-stu-id="1acee-107">The Azure Batch service emits the following diagnostic log events during the lifetime of certain Batch resources.</span></span>

<span data-ttu-id="1acee-108">**Événements du journal de service**</span><span class="sxs-lookup"><span data-stu-id="1acee-108">**Service Log events**</span></span>
* [<span data-ttu-id="1acee-109">Création de pool</span><span class="sxs-lookup"><span data-stu-id="1acee-109">Pool create</span></span>](batch-pool-create-event.md)
* [<span data-ttu-id="1acee-110">Début de suppression de pool</span><span class="sxs-lookup"><span data-stu-id="1acee-110">Pool delete start</span></span>](batch-pool-delete-start-event.md)
* [<span data-ttu-id="1acee-111">Fin de suppression de pool</span><span class="sxs-lookup"><span data-stu-id="1acee-111">Pool delete complete</span></span>](batch-pool-delete-complete-event.md)
* [<span data-ttu-id="1acee-112">Début de redimensionnement de pool</span><span class="sxs-lookup"><span data-stu-id="1acee-112">Pool resize start</span></span>](batch-pool-resize-start-event.md)
* [<span data-ttu-id="1acee-113">Fin de redimensionnement de pool</span><span class="sxs-lookup"><span data-stu-id="1acee-113">Pool resize complete</span></span>](batch-pool-resize-complete-event.md)
* [<span data-ttu-id="1acee-114">Début de tâche</span><span class="sxs-lookup"><span data-stu-id="1acee-114">Task start</span></span>](batch-task-start-event.md)
* [<span data-ttu-id="1acee-115">Fin de tâche</span><span class="sxs-lookup"><span data-stu-id="1acee-115">Task complete</span></span>](batch-task-complete-event.md)
* [<span data-ttu-id="1acee-116">Échec de tâche</span><span class="sxs-lookup"><span data-stu-id="1acee-116">Task fail</span></span>](batch-task-fail-event.md)