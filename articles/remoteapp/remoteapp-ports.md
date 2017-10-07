---
title: "aaaList de toowhitelist de Ports et les URL pour le déploiement de Azure RemoteApp dans le réseau virtuel du client | Documents Microsoft"
description: "Découvrez les ports et les URL que vous devez tooconfigure pour la communication via Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: mghosh1616
manager: mbaldwin
ms.assetid: 5a001ff7-14c9-47fa-9b39-78fd5a5f0250
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 039866f7b64ac763ca833d66031ade3def1d3543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="list-of-ports-and-urls-toopermit-access-for-azure-remoteapp-deployed-in-customer-virtual-network"></a><span data-ttu-id="89893-103">Liste d’URL et les Ports d’accès de toopermit pour le déploiement de RemoteApp Azure client réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="89893-103">List of Ports and URLs toopermit access for Azure RemoteApp Deployed in customer Virtual Network</span></span>
> [!IMPORTANT]
> <span data-ttu-id="89893-104">Azure RemoteApp ne sera plus disponible à partir du 31 août 2017.</span><span class="sxs-lookup"><span data-stu-id="89893-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="89893-105">Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="89893-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="89893-106">Si vous déployez une collection de cloud ou hybride Azure RemoteApp dans un réseau virtuel (VNET), passez en revue hello suivant des informations sur le port.</span><span class="sxs-lookup"><span data-stu-id="89893-106">If you are deploying an Azure RemoteApp cloud or hybrid collection in a virtual network (VNET), review hello following port information.</span></span> <span data-ttu-id="89893-107">Pour plus d’informations sur les réseaux virtuels, consultez [Présentation du réseau virtuel](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="89893-107">For more information on virtual networks, read [Virtual Network Overview](../virtual-network/virtual-networks-overview.md).</span></span> <span data-ttu-id="89893-108">Si vous avez créé un groupe de sécurité réseau (NSG) limitant le trafic toohello réseau virtuel ressources dans votre collection, assurez-vous que hello suivant ports est accessibles et autorisées par le biais des stratégies de sécurité hello sur le réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="89893-108">If you have created a network security group (NSG) restricting traffic toohello virtual network resources in your collection, make sure hello following ports are accessible and allowed through hello security policies on hello virtual network.</span></span> <span data-ttu-id="89893-109">Pour plus d’informations sur les groupes de sécurité réseau, consultez [Qu’est qu’un groupe de sécurité réseau ?](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="89893-109">For more information on network security groups, read [What is a Network Security Group? (NSG)](../virtual-network/virtual-networks-nsg.md).</span></span>

## <a name="azure-remoteapp-subnet-needs-access-toothese-endpoints-and-urls"></a><span data-ttu-id="89893-110">Azure RemoteApp sous-réseau a besoin de points de terminaison toothese accès et les URL :</span><span class="sxs-lookup"><span data-stu-id="89893-110">Azure RemoteApp subnet needs access toothese endpoints and URLs:</span></span>
* <span data-ttu-id="89893-111">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="89893-111">*.servicebus.windows.net</span></span>
* <span data-ttu-id="89893-112">*.servicebus.net</span><span class="sxs-lookup"><span data-stu-id="89893-112">*.servicebus.net</span></span>
* <span data-ttu-id="89893-113">https://*.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="89893-113">https://*.remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="89893-114">https://www.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="89893-114">https://www.remoteapp.windowsazure.com</span></span> 
* <span data-ttu-id="89893-115">https://*remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="89893-115">https://*remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="89893-116">https://*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="89893-116">https://*.core.windows.net</span></span>  
* <span data-ttu-id="89893-117">Sortant : TCP : TCP : 443, 9351, 9352, 10101-10175</span><span class="sxs-lookup"><span data-stu-id="89893-117">Outbound: TCP: TCP: 443, 9351, 9352, 10101-10175</span></span> 
* <span data-ttu-id="89893-118">Facultatif – UDP : 10201-10275</span><span class="sxs-lookup"><span data-stu-id="89893-118">Optional – UDP: 10201-10275</span></span>  

## <a name="azure-remoteapp-clients-need-access-toothese-endpoints-and-urls"></a><span data-ttu-id="89893-119">Azure RemoteApp clients doivent accéder aux points de terminaison toothese et les URL :</span><span class="sxs-lookup"><span data-stu-id="89893-119">Azure RemoteApp clients need access toothese endpoints and URLs:</span></span>
<span data-ttu-id="89893-120">Par les clients, que je veux dire, hello de postes de travail, les périphériques que les utilisateurs etc. Utilisez tooconnect toohello applications déploiement Bonjour collection Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="89893-120">By clients I mean hello desktops, devices etc. that people use tooconnect toohello apps deployed in hello Azure RemoteApp collection.</span></span>

* <span data-ttu-id="89893-121">https://telemetry.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="89893-121">https://telemetry.remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="89893-122">https://*.RemoteApp.windowsazure.com (les ports UDP facultatif hello sont pour cette adresse)</span><span class="sxs-lookup"><span data-stu-id="89893-122">https://*.remoteapp.windowsazure.com (hello optional UDP ports are for this address)</span></span> 
* <span data-ttu-id="89893-123">https://login.windows.net</span><span class="sxs-lookup"><span data-stu-id="89893-123">https://login.windows.net</span></span>  
* <span data-ttu-id="89893-124">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="89893-124">https://login.microsoftonline.com</span></span>  
* <span data-ttu-id="89893-125">https://www.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="89893-125">https://www.remoteapp.windowsazure.com</span></span> 
* <span data-ttu-id="89893-126">https://*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="89893-126">https://*.core.windows.net</span></span>  
* <span data-ttu-id="89893-127">Sortant : TCP : 443</span><span class="sxs-lookup"><span data-stu-id="89893-127">Outbound: TCP: 443</span></span>  
* <span data-ttu-id="89893-128">Facultatif - UDP : 3391</span><span class="sxs-lookup"><span data-stu-id="89893-128">Optional - UDP: 3391</span></span> 

