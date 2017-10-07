---
title: "conditions préalables pour ExpressRoute d’aaaQoS | Documents Microsoft"
description: "Cette page fournit des informations détaillées sur la configuration et la gestion de QoS pour des circuits ExpressRoute."
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: db1c1447-0283-4a09-907b-ae481adc40c7
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: cherylmc
ms.openlocfilehash: 46cc81bd38ff50dd9e7a1bfdd0faa457ff7b2fa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-qos-requirements"></a><span data-ttu-id="4c262-103">Configuration requise pour ExpressRoute QoS</span><span class="sxs-lookup"><span data-stu-id="4c262-103">ExpressRoute QoS requirements</span></span>
<span data-ttu-id="4c262-104">Skype Entreprise a différentes charges de travail nécessitant un traitement QoS différencié.</span><span class="sxs-lookup"><span data-stu-id="4c262-104">Skype for Business has various workloads that require differentiated QoS treatment.</span></span> <span data-ttu-id="4c262-105">Si vous envisagez de services de téléphonie tooconsume via ExpressRoute, vous devez respecter les exigences de toohello décrites ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="4c262-105">If you plan tooconsume voice services through ExpressRoute, you should adhere toohello requirements described below.</span></span>

![](./media/expressroute-qos/expressroute-qos.png)

> [!NOTE]
> <span data-ttu-id="4c262-106">Exigences de qualité de service s’appliquent toohello Microsoft d’homologation uniquement.</span><span class="sxs-lookup"><span data-stu-id="4c262-106">QoS requirements apply toohello Microsoft peering only.</span></span> <span data-ttu-id="4c262-107">les valeurs DSCP Hello dans votre trafic réseau reçu sur l’homologation publique Azure et de l’homologation privée Azure sera too0 de réinitialisation.</span><span class="sxs-lookup"><span data-stu-id="4c262-107">hello DSCP values in your network traffic received on Azure public peering and Azure private peering will be reset too0.</span></span> 
> 
> 

<span data-ttu-id="4c262-108">Hello tableau suivant fournit une liste des marquages de DSCP utilisé par Skype pour entreprises.</span><span class="sxs-lookup"><span data-stu-id="4c262-108">hello following table provides a list of DSCP markings used by Skype for Business.</span></span> <span data-ttu-id="4c262-109">Consultez trop[la gestion de la qualité de service pour Skype pour entreprises](https://technet.microsoft.com/library/gg405409.aspx) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="4c262-109">Refer too[Managing QoS for Skype for Business](https://technet.microsoft.com/library/gg405409.aspx) for more information.</span></span>

| <span data-ttu-id="4c262-110">**Classe de trafic**</span><span class="sxs-lookup"><span data-stu-id="4c262-110">**Traffic Class**</span></span> | <span data-ttu-id="4c262-111">**Traitement (marquage DSCP)**</span><span class="sxs-lookup"><span data-stu-id="4c262-111">**Treatment (DSCP Marking)**</span></span> | <span data-ttu-id="4c262-112">**Skype for Business Workloads**</span><span class="sxs-lookup"><span data-stu-id="4c262-112">**Skype for Business Workloads**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4c262-113">**Voice**</span><span class="sxs-lookup"><span data-stu-id="4c262-113">**Voice**</span></span> |<span data-ttu-id="4c262-114">EF (46)</span><span class="sxs-lookup"><span data-stu-id="4c262-114">EF (46)</span></span> |<span data-ttu-id="4c262-115">Skype / Lync voice</span><span class="sxs-lookup"><span data-stu-id="4c262-115">Skype / Lync voice</span></span> |
| <span data-ttu-id="4c262-116">**Interactive**</span><span class="sxs-lookup"><span data-stu-id="4c262-116">**Interactive**</span></span> |<span data-ttu-id="4c262-117">AF41 (34)</span><span class="sxs-lookup"><span data-stu-id="4c262-117">AF41 (34)</span></span> |<span data-ttu-id="4c262-118">Vidéo, VBSS</span><span class="sxs-lookup"><span data-stu-id="4c262-118">Video, VBSS</span></span> |
| <span data-ttu-id="4c262-119">AF21 (18)</span><span class="sxs-lookup"><span data-stu-id="4c262-119">AF21 (18)</span></span> |<span data-ttu-id="4c262-120">Partage d’application</span><span class="sxs-lookup"><span data-stu-id="4c262-120">App sharing</span></span> | |
| <span data-ttu-id="4c262-121">**Par défaut**</span><span class="sxs-lookup"><span data-stu-id="4c262-121">**Default**</span></span> |<span data-ttu-id="4c262-122">AF11 (10)</span><span class="sxs-lookup"><span data-stu-id="4c262-122">AF11 (10)</span></span> |<span data-ttu-id="4c262-123">Transfert de fichiers</span><span class="sxs-lookup"><span data-stu-id="4c262-123">File transfer</span></span> |
| <span data-ttu-id="4c262-124">CS0 (0)</span><span class="sxs-lookup"><span data-stu-id="4c262-124">CS0 (0)</span></span> |<span data-ttu-id="4c262-125">Tout autre élément</span><span class="sxs-lookup"><span data-stu-id="4c262-125">Anything else</span></span> | |

* <span data-ttu-id="4c262-126">Vous devez classer les charges de travail hello et marquer les valeurs DSCP hello.</span><span class="sxs-lookup"><span data-stu-id="4c262-126">You should classify hello workloads and mark hello right DSCP values.</span></span> <span data-ttu-id="4c262-127">Suivez les instructions de hello fournies [ici](https://technet.microsoft.com/library/gg405409.aspx) sur la façon de marquages de DSCP tooset dans votre réseau.</span><span class="sxs-lookup"><span data-stu-id="4c262-127">Follow hello guidance provided [here](https://technet.microsoft.com/library/gg405409.aspx) on how tooset DSCP markings in your network.</span></span>
* <span data-ttu-id="4c262-128">Vous devez configurer et prendre en charge plusieurs files d’attente QoS au sein de votre réseau.</span><span class="sxs-lookup"><span data-stu-id="4c262-128">You should configure and support multiple QoS queues within your network.</span></span> <span data-ttu-id="4c262-129">Voix doit être une classe autonome et reçoivent un traitement EF de hello spécifié dans la RFC 3246.</span><span class="sxs-lookup"><span data-stu-id="4c262-129">Voice must be a standalone class and receive hello EF treatment specified in RFC 3246.</span></span> 
* <span data-ttu-id="4c262-130">Vous pouvez décider hello queuing mécanisme, la stratégie de détection de congestion et allocation de bande passante par la classe de trafic.</span><span class="sxs-lookup"><span data-stu-id="4c262-130">You can decide hello queuing mechanism, congestion detection policy, and bandwidth allocation per traffic class.</span></span> <span data-ttu-id="4c262-131">Toutefois, hello marquage DSCP pour Skype pour les charges de travail métier doit être conservé.</span><span class="sxs-lookup"><span data-stu-id="4c262-131">But, hello DSCP marking for Skype for Business workloads must be preserved.</span></span> <span data-ttu-id="4c262-132">Si vous utilisez des marquages de DSCP non répertoriées ci-dessus, par exemple, AF31 (26), vous devez réécrire cette too0 de valeur DSCP avant d’envoyer tooMicrosoft de paquets hello.</span><span class="sxs-lookup"><span data-stu-id="4c262-132">If you are using DSCP markings not listed above, e.g. AF31 (26), you must rewrite this DSCP value too0 before sending hello packet tooMicrosoft.</span></span> <span data-ttu-id="4c262-133">Microsoft envoie uniquement les paquets marqués avec hello valeur DSCP hello au-dessus de table.</span><span class="sxs-lookup"><span data-stu-id="4c262-133">Microsoft only sends packets marked with hello DSCP value shown in hello above table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="4c262-134">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4c262-134">Next steps</span></span>
* <span data-ttu-id="4c262-135">Consultez Configuration requise de toohello pour [routage](expressroute-routing.md) et [NAT](expressroute-nat.md).</span><span class="sxs-lookup"><span data-stu-id="4c262-135">Refer toohello requirements for [Routing](expressroute-routing.md) and [NAT](expressroute-nat.md).</span></span>
* <span data-ttu-id="4c262-136">Voir les liens suivants de hello de tooconfigure de votre connexion ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="4c262-136">See hello following links tooconfigure your ExpressRoute connection.</span></span>
  
  * [<span data-ttu-id="4c262-137">Création d’un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="4c262-137">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-classic.md)
  * [<span data-ttu-id="4c262-138">Configuration du routage</span><span class="sxs-lookup"><span data-stu-id="4c262-138">Configure routing</span></span>](expressroute-howto-routing-classic.md)
  * [<span data-ttu-id="4c262-139">Lier un circuit ExpressRoute de tooan réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="4c262-139">Link a VNet tooan ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-classic.md)

