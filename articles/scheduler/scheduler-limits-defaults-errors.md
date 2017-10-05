---
title: "Limites et valeurs par défaut de Scheduler"
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
ms.openlocfilehash: db6b1c196cb468f41c7a7ce34758de346b522abb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="scheduler-limits-and-defaults"></a><span data-ttu-id="b084d-103">Limites et valeurs par défaut de Scheduler</span><span class="sxs-lookup"><span data-stu-id="b084d-103">Scheduler Limits and Defaults</span></span>
## <a name="scheduler-quotas-limits-defaults-and-throttles"></a><span data-ttu-id="b084d-104">Limitations, valeurs par défaut, limites et quotas de Scheduler</span><span class="sxs-lookup"><span data-stu-id="b084d-104">Scheduler Quotas, Limits, Defaults, and Throttles</span></span>
[!INCLUDE [scheduler-limits-table](../../includes/scheduler-limits-table.md)]

## <a name="the-x-ms-request-id-header"></a><span data-ttu-id="b084d-105">L'en-tête x-ms-request-id</span><span class="sxs-lookup"><span data-stu-id="b084d-105">The x-ms-request-id Header</span></span>
<span data-ttu-id="b084d-106">Chaque requête adressée au service de Scheduler retourne un en-tête de réponse nommé**x-ms-request-id**.</span><span class="sxs-lookup"><span data-stu-id="b084d-106">Every request made against the Scheduler service returns a response header named**x-ms-request-id**.</span></span> <span data-ttu-id="b084d-107">Cet en-tête contient une valeur opaque qui identifie de façon unique la requête.</span><span class="sxs-lookup"><span data-stu-id="b084d-107">This header contains an opaque value that uniquely identifies the request.</span></span>

<span data-ttu-id="b084d-108">Si une requête échoue constamment et que vous avez vérifié qu'elle est formulée correctement, vous pouvez utiliser cette valeur pour signaler l'erreur à Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b084d-108">If a request is consistently failing and you have verified that the request is properly formulated, you may use this value to report the error to Microsoft.</span></span> <span data-ttu-id="b084d-109">Dans votre rapport, incluez la valeur de x-ms-request-id, l’heure approximative de la requête, l’identificateur de l’abonnement, la collection de travaux et/ou la tâche et le type d’opération tenté par la requête.</span><span class="sxs-lookup"><span data-stu-id="b084d-109">In your report, include the value of x-ms-request-id, the approximate time that the request was made, the identifier of the subscription, job collection, and/or job, and the type of operation that the request attempted.</span></span>

## <a name="see-also"></a><span data-ttu-id="b084d-110">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="b084d-110">See Also</span></span>
 [<span data-ttu-id="b084d-111">Présentation d'Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="b084d-111">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="b084d-112">Concepts, terminologie et hiérarchie d’entités d’Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="b084d-112">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="b084d-113">Prise en main de Scheduler dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="b084d-113">Get started using Scheduler in the Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="b084d-114">Plans et facturation dans Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="b084d-114">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="b084d-115">Informations de référence sur l’API REST d’Azure Scheluler</span><span class="sxs-lookup"><span data-stu-id="b084d-115">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="b084d-116">Informations de référence sur les applets de commande PowerShell d’Azure Scheluler</span><span class="sxs-lookup"><span data-stu-id="b084d-116">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="b084d-117">Haute disponibilité et fiabilité d’Azure Scheluler</span><span class="sxs-lookup"><span data-stu-id="b084d-117">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="b084d-118">Authentification sortante d’Azure Scheluler</span><span class="sxs-lookup"><span data-stu-id="b084d-118">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

