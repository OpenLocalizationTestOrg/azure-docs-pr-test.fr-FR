---
title: "Définir et gérer l’état dans les microservices Azure | Microsoft Docs"
description: "Comment définir et gérer l'état de service dans Service Fabric"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: f5e618a5-3ea3-4404-94af-122278f91652
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 2f7835fab175bdb7ef7ce3894cab9e09a39457f3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="service-state"></a><span data-ttu-id="a88cb-103">État du service</span><span class="sxs-lookup"><span data-stu-id="a88cb-103">Service state</span></span>
<span data-ttu-id="a88cb-104">**L’état du service** correspond aux données en mémoire ou sur disque nécessaires au bon fonctionnement du service.</span><span class="sxs-lookup"><span data-stu-id="a88cb-104">**Service state** refers to the in-memory or on disk data that a service requires to function.</span></span> <span data-ttu-id="a88cb-105">Il comprend, par exemple, les variables membres et les structures de données que le service lit et écrit afin d’effectuer des tâches.</span><span class="sxs-lookup"><span data-stu-id="a88cb-105">It includes, for example, the data structures and member variables that the service reads and writes to do work.</span></span> <span data-ttu-id="a88cb-106">Selon l’architecture du service, il peut aussi inclure des fichiers ou d’autres ressources stockés sur le disque,</span><span class="sxs-lookup"><span data-stu-id="a88cb-106">Depending on how the service is architected, it could also include files or other resources that are stored on disk.</span></span> <span data-ttu-id="a88cb-107">par exemple, les fichiers qu’utiliserait une base de données pour stocker les journaux des transactions et des données.</span><span class="sxs-lookup"><span data-stu-id="a88cb-107">For example, the files a database would use to store data and transaction logs.</span></span>

<span data-ttu-id="a88cb-108">Prenons l’exemple d’une calculatrice.</span><span class="sxs-lookup"><span data-stu-id="a88cb-108">As an example service, let's consider a calculator.</span></span> <span data-ttu-id="a88cb-109">Un service de calculatrice de base accepte deux nombres et retourne leur somme.</span><span class="sxs-lookup"><span data-stu-id="a88cb-109">A basic calculator service takes two numbers and returns their sum.</span></span> <span data-ttu-id="a88cb-110">Ce calcul n’implique aucune variable membre ni aucune autre information.</span><span class="sxs-lookup"><span data-stu-id="a88cb-110">Performing this calculation involves no member variables or other information.</span></span>

<span data-ttu-id="a88cb-111">À présent, considérons cette même calculatrice, mais avec une méthode supplémentaire permettant de stocker et de retourner la dernière somme calculée.</span><span class="sxs-lookup"><span data-stu-id="a88cb-111">Now consider the same calculator, but with an additional method for storing and returning the last sum it has computed.</span></span> <span data-ttu-id="a88cb-112">Il s’agit à présent d’un service avec état,</span><span class="sxs-lookup"><span data-stu-id="a88cb-112">This service is now stateful.</span></span> <span data-ttu-id="a88cb-113">c’est-à-dire qu’il contient un certain état dans lequel il écrit quand il calcule une nouvelle somme et qu’il lit quand on lui demande de retourner la dernière somme calculée.</span><span class="sxs-lookup"><span data-stu-id="a88cb-113">Stateful means it contains some state that it writes to when it computes a new sum and reads from when you ask it to return the last computed sum.</span></span>

<span data-ttu-id="a88cb-114">Dans Service Fabric Azure, le premier service porte le nom de « service sans état ».</span><span class="sxs-lookup"><span data-stu-id="a88cb-114">In Azure Service Fabric, the first service is called a stateless service.</span></span> <span data-ttu-id="a88cb-115">Le second service est appelé « service avec état ».</span><span class="sxs-lookup"><span data-stu-id="a88cb-115">The second service is called a stateful service.</span></span>

## <a name="storing-service-state"></a><span data-ttu-id="a88cb-116">Stockage de l’état du service</span><span class="sxs-lookup"><span data-stu-id="a88cb-116">Storing service state</span></span>
<span data-ttu-id="a88cb-117">L’état peut être externalisé ou colocalisé avec le code qui le manipule.</span><span class="sxs-lookup"><span data-stu-id="a88cb-117">State can be either externalized or co-located with the code that is manipulating the state.</span></span> <span data-ttu-id="a88cb-118">L’externalisation d’état s’effectue généralement à l’aide d’une base de données externe ou autre magasin de données, qui s’exécute sur différents ordinateurs du réseau ou en dehors du processus sur le même ordinateur.</span><span class="sxs-lookup"><span data-stu-id="a88cb-118">Externalization of state is typically done by using an external database or other data store that runs on different machines over the network or out of process on the same machine.</span></span> <span data-ttu-id="a88cb-119">Dans notre exemple de calculatrice, le magasin de données pourrait être une base de données SQL ou une instance de magasin de tables Azure.</span><span class="sxs-lookup"><span data-stu-id="a88cb-119">In our calculator example, the data store could be a SQL database or instance of Azure Table Store.</span></span> <span data-ttu-id="a88cb-120">Chaque requête de calcul de la somme effectue une mise à jour de ces données et demande au service de retourner en résultat la valeur actuelle récupérée à partir du magasin.</span><span class="sxs-lookup"><span data-stu-id="a88cb-120">Every request to compute the sum performs an update on this data, and requests to the service to return the value result in the current value being fetched from the store.</span></span> 

<span data-ttu-id="a88cb-121">L’état peut également être colocalisé avec le code qui manipule l’état.</span><span class="sxs-lookup"><span data-stu-id="a88cb-121">State can also be co-located with the code that manipulates the state.</span></span> <span data-ttu-id="a88cb-122">Les services avec état de Service Fabric sont majoritairement générés suivant ce modèle.</span><span class="sxs-lookup"><span data-stu-id="a88cb-122">Stateful services in Service Fabric are typically built using this model.</span></span> <span data-ttu-id="a88cb-123">Service Fabric fournit l’infrastructure permettant de s’assurer que cet état est hautement disponible, cohérent et durable, et que les services générés de cette façon peuvent facilement évoluer.</span><span class="sxs-lookup"><span data-stu-id="a88cb-123">Service Fabric provides the infrastructure to ensure that this state is highly available, consistent, and durable, and that the services built this way can easily scale.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a88cb-124">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a88cb-124">Next steps</span></span>
<span data-ttu-id="a88cb-125">Pour plus d’informations sur les concepts propres à Service Fabric, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="a88cb-125">For more information on Service Fabric concepts, see the following articles:</span></span>

* [<span data-ttu-id="a88cb-126">Disponibilité des services Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a88cb-126">Availability of Service Fabric services</span></span>](service-fabric-availability-services.md)
* [<span data-ttu-id="a88cb-127">Extensibilité des services Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a88cb-127">Scalability of Service Fabric services</span></span>](service-fabric-concepts-scalability.md)
* [<span data-ttu-id="a88cb-128">Partitionnement des services Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a88cb-128">Partitioning Service Fabric services</span></span>](service-fabric-concepts-partitioning.md)
* [<span data-ttu-id="a88cb-129">Modèle Reliable Services de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a88cb-129">Service Fabric Reliable Services</span></span>](service-fabric-reliable-services-introduction.md)
