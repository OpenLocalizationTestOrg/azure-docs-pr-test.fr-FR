---
title: "aaaWhat est Azure Scheduler ? | Microsoft Docs"
description: "Azure Scheduler vous permet de toodeclaratively décrivent toorun actions dans le cloud de hello. Ensuite, il planifie et exécute ces actions automatiquement."
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 52aa6ae1-4c3d-43fb-81b0-6792c84bcfae
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 062e25ae473510264dc0038198c05e7ac1e86210
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-scheduler"></a><span data-ttu-id="6cc74-105">Présentation d’Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="6cc74-105">What is Azure Scheduler?</span></span>
<span data-ttu-id="6cc74-106">Azure Scheduler vous permet de toodeclaratively décrivent toorun actions dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="6cc74-106">Azure Scheduler allows you toodeclaratively describe actions toorun in hello cloud.</span></span> <span data-ttu-id="6cc74-107">Ensuite, il planifie et exécute ces actions automatiquement.</span><span class="sxs-lookup"><span data-stu-id="6cc74-107">It then schedules and runs those actions automatically.</span></span>  <span data-ttu-id="6cc74-108">Planificateur de parvenir à l’aide de [hello portail Azure](scheduler-get-started-portal.md), code, [API REST](https://msdn.microsoft.com/library/mt629143.aspx), ou Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6cc74-108">Scheduler does this by using [hello Azure portal](scheduler-get-started-portal.md), code, [REST API](https://msdn.microsoft.com/library/mt629143.aspx), or Azure PowerShell.</span></span>

<span data-ttu-id="6cc74-109">Le scheduler crée, gère et appelle le travail planifié.</span><span class="sxs-lookup"><span data-stu-id="6cc74-109">Scheduler creates, maintains, and invokes scheduled work.</span></span>  <span data-ttu-id="6cc74-110">Scheduler n’héberge pas de charge de travail et n’exécute pas de code.</span><span class="sxs-lookup"><span data-stu-id="6cc74-110">Scheduler does not host any workloads or run any code.</span></span> <span data-ttu-id="6cc74-111">Il se contente d’ *appeler* du code qui est hébergé ailleurs, par exemple, dans Azure, localement ou auprès d’un autre fournisseur.</span><span class="sxs-lookup"><span data-stu-id="6cc74-111">It only *invokes* code hosted elsewhere—in Azure, on-premises, or with another provider.</span></span> <span data-ttu-id="6cc74-112">Il effectue des appels via HTTP, HTTPS, une file d’attente de stockage, une file d’attente Service Bus ou une rubrique Service Bus.</span><span class="sxs-lookup"><span data-stu-id="6cc74-112">It invokes via HTTP, HTTPS, a storage queue, a service bus queue, or a service bus topic.</span></span>

<span data-ttu-id="6cc74-113">Les planifications de planificateur [travaux](scheduler-concepts-terms.md), conserve un historique des résultats de l’exécution du travail qu’un peut examiner et de façon déterministe et fiable toobe de charges de travail de planifications exécuter.</span><span class="sxs-lookup"><span data-stu-id="6cc74-113">Scheduler schedules [jobs](scheduler-concepts-terms.md), keeps a history of job execution results that one can review, and deterministically and reliably schedules workloads toobe run.</span></span> <span data-ttu-id="6cc74-114">Les tâches Web Azure (partie de la fonctionnalité d’applications Web hello dans Azure App Service) et autres fonctionnalités de planification Azure utilisent le planificateur en arrière-plan de hello.</span><span class="sxs-lookup"><span data-stu-id="6cc74-114">Azure WebJobs (part of hello Web Apps feature in Azure App Service) and other Azure scheduling capabilities use Scheduler in hello background.</span></span> <span data-ttu-id="6cc74-115">Hello [API REST de Scheduler](https://msdn.microsoft.com/library/mt629143.aspx) permet de gérer la communication hello pour ces actions.</span><span class="sxs-lookup"><span data-stu-id="6cc74-115">hello [Scheduler REST API](https://msdn.microsoft.com/library/mt629143.aspx) helps manage hello communication for these actions.</span></span> <span data-ttu-id="6cc74-116">Ainsi, Scheduler prend en charge les [planifications complexes et la périodicité avancée facilement](scheduler-advanced-complexity.md) .</span><span class="sxs-lookup"><span data-stu-id="6cc74-116">As such, Scheduler supports [complex schedules and advanced recurrence](scheduler-advanced-complexity.md) easily.</span></span>

<span data-ttu-id="6cc74-117">Il existe plusieurs scénarios qui se prêtent à l’utilisation de toohello du planificateur.</span><span class="sxs-lookup"><span data-stu-id="6cc74-117">There are several scenarios that lend themselves toohello usage of Scheduler.</span></span> <span data-ttu-id="6cc74-118">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="6cc74-118">For example:</span></span>

* <span data-ttu-id="6cc74-119">*Actions d’application périodiques* : collecte régulière de données à partir de Twitter dans un flux.</span><span class="sxs-lookup"><span data-stu-id="6cc74-119">*Recurring application actions:* Periodically gathering data from Twitter into a feed.</span></span>
* <span data-ttu-id="6cc74-120">*Maintenance quotidienne :* nettoyages quotidiens des journaux en exécutant des sauvegardes et autres tâches de maintenance.</span><span class="sxs-lookup"><span data-stu-id="6cc74-120">*Daily maintenance:* Daily pruning of logs, performing backups, and other maintenance tasks.</span></span> <span data-ttu-id="6cc74-121">Par exemple, un administrateur peut choisir tooback base de données hello à 01:00.</span><span class="sxs-lookup"><span data-stu-id="6cc74-121">For example, an administrator may choose tooback up hello database at 1:00 A.M.</span></span> <span data-ttu-id="6cc74-122">tous les jours hello prochains mois neuf.</span><span class="sxs-lookup"><span data-stu-id="6cc74-122">every day for hello next nine months.</span></span>

<span data-ttu-id="6cc74-123">Scheduler vous permet de toocreate mettre à jour, supprimer, afficher et gérer des travaux et [les collections de travaux](scheduler-concepts-terms.md) par programme, à l’aide de scripts et dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="6cc74-123">Scheduler allows you toocreate, update, delete, view, and manage jobs and [job collections](scheduler-concepts-terms.md) programmatically, by using scripts, and in hello portal.</span></span>

## <a name="see-also"></a><span data-ttu-id="6cc74-124">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="6cc74-124">See also</span></span>
 [<span data-ttu-id="6cc74-125">Concepts, terminologie et hiérarchie d’entités d’Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="6cc74-125">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="6cc74-126">Prise en main du planificateur Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="6cc74-126">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="6cc74-127">Plans et facturation dans Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="6cc74-127">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="6cc74-128">Comment toobuild complexe planifie et périodicité avancée avec Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="6cc74-128">How toobuild complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="6cc74-129">Informations de référence sur l’API REST d’Azure Scheluler</span><span class="sxs-lookup"><span data-stu-id="6cc74-129">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="6cc74-130">Informations de référence sur les applets de commande PowerShell d’Azure Scheluler</span><span class="sxs-lookup"><span data-stu-id="6cc74-130">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="6cc74-131">Haute disponibilité et fiabilité d’Azure Scheluler</span><span class="sxs-lookup"><span data-stu-id="6cc74-131">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="6cc74-132">Limites, valeurs par défaut et codes d’erreur d’Azure Scheluler</span><span class="sxs-lookup"><span data-stu-id="6cc74-132">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="6cc74-133">Authentification sortante d’Azure Scheluler</span><span class="sxs-lookup"><span data-stu-id="6cc74-133">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

