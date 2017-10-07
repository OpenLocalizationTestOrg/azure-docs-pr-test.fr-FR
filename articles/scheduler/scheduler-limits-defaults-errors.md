---
title: "aaaScheduler limites et des valeurs par défaut"
description: "Limites et valeurs par défaut de Scheduler"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 88f4a3e9-6dbd-4943-8543-f0649d423061
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 6fe0600d3ce3249d5aab1b877369b175316b5437
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-limits-and-defaults"></a><span data-ttu-id="a69a0-103">Limites et valeurs par défaut de Scheduler</span><span class="sxs-lookup"><span data-stu-id="a69a0-103">Scheduler Limits and Defaults</span></span>
## <a name="scheduler-quotas-limits-defaults-and-throttles"></a><span data-ttu-id="a69a0-104">Limitations, valeurs par défaut, limites et quotas de Scheduler</span><span class="sxs-lookup"><span data-stu-id="a69a0-104">Scheduler Quotas, Limits, Defaults, and Throttles</span></span>
[!INCLUDE [scheduler-limits-table](../../includes/scheduler-limits-table.md)]

## <a name="hello-x-ms-request-id-header"></a><span data-ttu-id="a69a0-105">Hello x-ms-request-id en-tête</span><span class="sxs-lookup"><span data-stu-id="a69a0-105">hello x-ms-request-id Header</span></span>
<span data-ttu-id="a69a0-106">Chaque demande adressée à hello service Planificateur renvoie un en-tête de réponse nommé**x-ms-request-id**. Cet en-tête contient une valeur opaque qui identifie de façon unique la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="a69a0-106">Every request made against hello Scheduler service returns a response header named**x-ms-request-id**. This header contains an opaque value that uniquely identifies hello request.</span></span>

<span data-ttu-id="a69a0-107">Si une demande est régulièrement défectueux et que vous avez vérifié que la demande de hello est correctement formulée, vous pouvez utiliser cette tooMicrosoft d’erreur valeur tooreport hello.</span><span class="sxs-lookup"><span data-stu-id="a69a0-107">If a request is consistently failing and you have verified that hello request is properly formulated, you may use this value tooreport hello error tooMicrosoft.</span></span> <span data-ttu-id="a69a0-108">Dans votre rapport, inclure la valeur de hello durée approximative de x-ms-request-id hello cette demande hello a été apportée, hello identificateur d’abonnement de hello, collection de travaux et/ou de travail, et hello du type d’opération hello a tenté de demande.</span><span class="sxs-lookup"><span data-stu-id="a69a0-108">In your report, include hello value of x-ms-request-id, hello approximate time that hello request was made, hello identifier of hello subscription, job collection, and/or job, and hello type of operation that hello request attempted.</span></span>

## <a name="see-also"></a><span data-ttu-id="a69a0-109">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="a69a0-109">See Also</span></span>
 [<span data-ttu-id="a69a0-110">Présentation d'Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="a69a0-110">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="a69a0-111">Concepts, terminologie et hiérarchie d’entités d’Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="a69a0-111">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="a69a0-112">Prise en main du planificateur Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="a69a0-112">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="a69a0-113">Plans et facturation dans Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="a69a0-113">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="a69a0-114">Informations de référence sur l’API REST d’Azure Scheluler</span><span class="sxs-lookup"><span data-stu-id="a69a0-114">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="a69a0-115">Informations de référence sur les applets de commande PowerShell d’Azure Scheluler</span><span class="sxs-lookup"><span data-stu-id="a69a0-115">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="a69a0-116">Haute disponibilité et fiabilité d’Azure Scheluler</span><span class="sxs-lookup"><span data-stu-id="a69a0-116">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="a69a0-117">Authentification sortante d’Azure Scheluler</span><span class="sxs-lookup"><span data-stu-id="a69a0-117">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

