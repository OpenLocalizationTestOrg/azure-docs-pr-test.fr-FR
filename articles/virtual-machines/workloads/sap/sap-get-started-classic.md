---
title: aaaUsing SAP sur les ordinateurs virtuels Linux | Documents Microsoft
description: "En savoir plus sur l’utilisation de SAP sur des machines virtuelles Linux dans Microsoft Azure"
services: virtual-machines-linux,virtual-network,storage
documentationcenter: saponazure
author: MSSedusch
manager: timlt
editor: 
tags: azure-service-management
keywords: 
ms.assetid: f9cd93dc-71ad-48a4-8778-4e48aec484a6
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: campaign-page
ms.tgt_pltfrm: vm-linux
ms.workload: na
ms.date: 10/04/2016
ms.author: sedusch
ms.openlocfilehash: fd4aad83d99ef5286488aaab6552fd67a5e35a4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-sap-on-linux-virtual-machines-in-azure"></a><span data-ttu-id="1ca75-103">Utilisation de SAP sur des machines virtuelles Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="1ca75-103">Using SAP on Linux virtual machines in Azure</span></span>
<span data-ttu-id="1ca75-104">Le Cloud Computing est un terme couramment utilisé qui prend de plus en plus d’importance dans hello secteur informatique, des petites entreprises, les sociétés toolarge et multinationale.</span><span class="sxs-lookup"><span data-stu-id="1ca75-104">Cloud Computing is a widely used term which is gaining more and more importance within hello IT industry, from small companies up toolarge and multinational corporations.</span></span> <span data-ttu-id="1ca75-105">Microsoft Azure est la plateforme de Services de Cloud de Microsoft, qui offre un large éventail de nouvelles possibilités de hello.</span><span class="sxs-lookup"><span data-stu-id="1ca75-105">Microsoft Azure is hello Cloud Services Platform from Microsoft which offers a wide spectrum of new possibilities.</span></span> <span data-ttu-id="1ca75-106">Maintenant les clients sont des applications d’approvisionner et configurer des toorapidly en mesure d’en tant que Services de cloud computing, afin qu’ils ne sont pas tootechnical limité ou restrictions budgétisation.</span><span class="sxs-lookup"><span data-stu-id="1ca75-106">Now customers are able toorapidly provision and de-provision applications as Cloud-Services, so they are not limited tootechnical or budgeting restrictions.</span></span> <span data-ttu-id="1ca75-107">Au lieu de consacrer du temps et budget à l’infrastructure matérielle, les entreprises peuvent se concentrer sur l’application hello, des processus d’entreprise et ses avantages pour les clients et les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="1ca75-107">Instead of investing time and budget into hardware infrastructure, companies can focus on hello application, business processes and its benefits for customers and users.</span></span>

<span data-ttu-id="1ca75-108">Avec Microsoft Azure Virtual Machines, Microsoft propose une plateforme IaaS (Infrastructure as a Service) complète.</span><span class="sxs-lookup"><span data-stu-id="1ca75-108">With Microsoft Azure virtual machines, Microsoft offers a comprehensive Infrastructure as a Service (IaaS) platform.</span></span> <span data-ttu-id="1ca75-109">Les applications basées sur SAP NetWeaver sont prises en charge sur Machines virtuelles Azure (IaaS).</span><span class="sxs-lookup"><span data-stu-id="1ca75-109">SAP NetWeaver based applications are supported on Azure Virtual Machines (IaaS).</span></span> <span data-ttu-id="1ca75-110">livres blancs de Hello ci-dessous décrivent comment tooplan implémentez SAP NetWeaver applications basées sur et sur les machines virtuelles Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="1ca75-110">hello whitepapers below describe how tooplan and implement SAP NetWeaver based applications on Windows virtual machines in Azure.</span></span> <span data-ttu-id="1ca75-111">Vous pouvez également implémenter des applications basées sur SAP NetWeaver sur des [machines virtuelles Windows](../../virtual-machines-windows-classic-sap-get-started.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1ca75-111">You can also implement SAP NetWeaver based applications on [Windows virtual machines](../../virtual-machines-windows-classic-sap-get-started.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-sap-get-started](../../../../includes/virtual-machines-common-classic-sap-get-started.md)]

## <a name="sap-netweaver-on-azure-suse-linux-virtual-machines"></a><span data-ttu-id="1ca75-112">SAP NetWeaver sur les machines virtuelles Azure SUSE Linux</span><span class="sxs-lookup"><span data-stu-id="1ca75-112">SAP NetWeaver on Azure SUSE Linux Virtual Machines</span></span>
<span data-ttu-id="1ca75-113">titre : aaaTesting SAP NetWeaver sur machines virtuelles de Microsoft Azure SUSE Linux</span><span class="sxs-lookup"><span data-stu-id="1ca75-113">title: aaaTesting SAP NetWeaver on Microsoft Azure SUSE Linux VMs</span></span>

<span data-ttu-id="1ca75-114">Résumé : à ce stade, il n’existe aucune prise en charge SAP officielle pour l’exécution de SAP NetWeaver sur les machines virtuelles Linux Azure.</span><span class="sxs-lookup"><span data-stu-id="1ca75-114">Summary: There is no official SAP support for running SAP NetWeaver on Azure Linux VMs at this point in time.</span></span> <span data-ttu-id="1ca75-115">Néanmoins clients peuvent toodo des tests ou envisagez de toorun systèmes de démonstration ou de formations SAP sur les machines virtuelles Linux Azure tant qu’il n’est pas nécessaire pour contacter le support SAP.</span><span class="sxs-lookup"><span data-stu-id="1ca75-115">Nevertheless customers might want toodo some testing or might consider toorun SAP demo or training systems on Azure Linux VMs as long as there is no need for contacting SAP support.</span></span> <span data-ttu-id="1ca75-116">Cet article doit aider à configurer les machines virtuelles Linux SUSE Azure pour SAP en cours d’exécution et fournit quelques conseils de base dans l’ordre tooavoid pièges potentiels.</span><span class="sxs-lookup"><span data-stu-id="1ca75-116">This article should help setting up Azure SUSE Linux VMs for running SAP and gives some basic hints in order tooavoid common potential pitfalls.</span></span>

<span data-ttu-id="1ca75-117">Mise à jour : décembre 2015</span><span class="sxs-lookup"><span data-stu-id="1ca75-117">Updated: December 2015</span></span>

[<span data-ttu-id="1ca75-118">Cet article est disponible ici</span><span class="sxs-lookup"><span data-stu-id="1ca75-118">This article can be found here</span></span>](suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

