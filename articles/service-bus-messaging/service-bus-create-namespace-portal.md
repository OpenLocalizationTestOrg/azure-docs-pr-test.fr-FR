---
title: aaaHow toocreate un espace de noms Service Bus hello portail Azure | Documents Microsoft
description: "Créer un espace de noms Service Bus à l’aide de hello portail Azure."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: fbb10e62-b133-4851-9d27-40bd844db3ba
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: d8907e7e4a804056f6d66d5a177d9ace967ed2ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-using-hello-azure-portal"></a><span data-ttu-id="48f7d-103">Créer un espace de noms Service Bus à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="48f7d-103">Create a Service Bus namespace using hello Azure portal</span></span>

<span data-ttu-id="48f7d-104">Un espace de noms est un conteneur d’étendue pour tous les composants de messagerie.</span><span class="sxs-lookup"><span data-stu-id="48f7d-104">A namespace is a scoping container for all messaging components.</span></span> <span data-ttu-id="48f7d-105">Plusieurs files d’attente et rubriques peuvent résider dans un seul espace de noms, et les espaces de noms servent souvent de conteneurs d’applications.</span><span class="sxs-lookup"><span data-stu-id="48f7d-105">Multiple queues and topics can reside within a single namespace, and namespaces often serve as application containers.</span></span> <span data-ttu-id="48f7d-106">Il existe deux façons différentes toocreate un espace de noms Service Bus :</span><span class="sxs-lookup"><span data-stu-id="48f7d-106">There are two different ways toocreate a Service Bus namespace:</span></span>

1. <span data-ttu-id="48f7d-107">Portail Azure (cet article)</span><span class="sxs-lookup"><span data-stu-id="48f7d-107">Azure portal (this article)</span></span>
2. <span data-ttu-id="48f7d-108">[Modèles Microsoft Azure Resource Manager][create-namespace-using-arm]</span><span class="sxs-lookup"><span data-stu-id="48f7d-108">[Resource Manager templates][create-namespace-using-arm]</span></span>

## <a name="create-a-namespace-in-hello-azure-portal"></a><span data-ttu-id="48f7d-109">Créer un espace de noms Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="48f7d-109">Create a namespace in hello Azure portal</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

<span data-ttu-id="48f7d-110">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="48f7d-110">Congratulations!</span></span> <span data-ttu-id="48f7d-111">Vous venez de créer un espace de noms de messagerie Service Bus.</span><span class="sxs-lookup"><span data-stu-id="48f7d-111">You have now created a Service Bus Messaging namespace.</span></span>

## <a name="next-steps"></a><span data-ttu-id="48f7d-112">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="48f7d-112">Next steps</span></span>

<span data-ttu-id="48f7d-113">Découvrez notre [GitHub exemples][github-samples], qui présentent certaines Hello plus avancés des fonctionnalités de messagerie Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="48f7d-113">Check out our [GitHub samples][github-samples], which show some of hello more advanced features of Azure Service Bus Messaging.</span></span>

[create-namespace-using-arm]: service-bus-resource-manager-overview.md
[github-samples]: https://github.com/Azure/azure-service-bus/tree/master/samples
