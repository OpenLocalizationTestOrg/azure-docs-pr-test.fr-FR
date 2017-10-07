---
title: aaaAzure Analytique de traitement par lots | Documents Microsoft
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
ms.openlocfilehash: 462fbad1ac522b485ae18c1e8891b9d2cabd45e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="batch-analytics"></a><span data-ttu-id="16416-103">Analyse en mode batch</span><span class="sxs-lookup"><span data-stu-id="16416-103">Batch Analytics</span></span>
<span data-ttu-id="16416-104">les rubriques de Hello de traitement Analytique contiennent des informations de référence pour les événements de hello et alertes disponibles pour les ressources de service de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="16416-104">hello topics in Batch Analytics contain reference information for hello events and alerts available for Batch service resources.</span></span>

<span data-ttu-id="16416-105">Pour plus d’informations sur l’activation et l’utilisation des journaux de diagnostic de Batch, voir [Journalisation des diagnostics Azure Batch](https://azure.microsoft.com/documentation/articles/batch-diagnostics/).</span><span class="sxs-lookup"><span data-stu-id="16416-105">See [Azure Batch diagnostic logging](https://azure.microsoft.com/documentation/articles/batch-diagnostics/) for more information on enabling and consuming Batch diagnostic logs.</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="16416-106">Journaux de diagnostic</span><span class="sxs-lookup"><span data-stu-id="16416-106">Diagnostic logs</span></span>

<span data-ttu-id="16416-107">Hello service Azure Batch émet hello suivant des événements du journal de diagnostic pendant la durée de vie hello de certaines ressources de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="16416-107">hello Azure Batch service emits hello following diagnostic log events during hello lifetime of certain Batch resources.</span></span>

<span data-ttu-id="16416-108">**Événements du journal de service**</span><span class="sxs-lookup"><span data-stu-id="16416-108">**Service Log events**</span></span>
* [<span data-ttu-id="16416-109">Création de pool</span><span class="sxs-lookup"><span data-stu-id="16416-109">Pool create</span></span>](batch-pool-create-event.md)
* [<span data-ttu-id="16416-110">Début de suppression de pool</span><span class="sxs-lookup"><span data-stu-id="16416-110">Pool delete start</span></span>](batch-pool-delete-start-event.md)
* [<span data-ttu-id="16416-111">Fin de suppression de pool</span><span class="sxs-lookup"><span data-stu-id="16416-111">Pool delete complete</span></span>](batch-pool-delete-complete-event.md)
* [<span data-ttu-id="16416-112">Début de redimensionnement de pool</span><span class="sxs-lookup"><span data-stu-id="16416-112">Pool resize start</span></span>](batch-pool-resize-start-event.md)
* [<span data-ttu-id="16416-113">Fin de redimensionnement de pool</span><span class="sxs-lookup"><span data-stu-id="16416-113">Pool resize complete</span></span>](batch-pool-resize-complete-event.md)
* [<span data-ttu-id="16416-114">Début de tâche</span><span class="sxs-lookup"><span data-stu-id="16416-114">Task start</span></span>](batch-task-start-event.md)
* [<span data-ttu-id="16416-115">Fin de tâche</span><span class="sxs-lookup"><span data-stu-id="16416-115">Task complete</span></span>](batch-task-complete-event.md)
* [<span data-ttu-id="16416-116">Échec de tâche</span><span class="sxs-lookup"><span data-stu-id="16416-116">Task fail</span></span>](batch-task-fail-event.md)