---
title: "aaaSQL vue d’ensemble des groupes de disponibilité de serveur - des Machines virtuelles Azure - | Documents Microsoft"
description: "Cet article présente les groupes de disponibilité de SQL Server sur les machines virtuelles Azure."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 601eebb1-fc2c-4f5b-9c05-0e6ffd0e5334
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/13/2017
ms.author: mikeray
ms.openlocfilehash: ecac8b8c5073021af2aa22a05490bb8c4c20ed17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-sql-server-always-on-availability-groups-on-azure-virtual-machines"></a><span data-ttu-id="1a6bc-103">Présentation des groupes de disponibilité SQL Server AlwaysOn sur des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="1a6bc-103">Introducing SQL Server Always On availability groups on Azure virtual machines</span></span> #

<span data-ttu-id="1a6bc-104">Cet article présente les groupes de disponibilité de SQL Server sur les machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="1a6bc-104">This article introduces SQL Server availability groups on Azure Virtual Machines.</span></span> 

<span data-ttu-id="1a6bc-105">Toujours sur les groupes de disponibilité sur des Machines virtuelles Azure sont tooAlways similaires sur les groupes de disponibilité local.</span><span class="sxs-lookup"><span data-stu-id="1a6bc-105">Always On availability groups on Azure Virtual Machines are similar tooAlways On availability groups on premises.</span></span> <span data-ttu-id="1a6bc-106">Pour plus d’informations, voir [Groupes de disponibilité AlwaysOn (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx).</span><span class="sxs-lookup"><span data-stu-id="1a6bc-106">For more information, see [Always On Availability Groups (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx).</span></span> 

<span data-ttu-id="1a6bc-107">diagramme de Hello illustre les parties de hello d’un groupe de disponibilité de serveur dans les Machines virtuelles Azure SQL complète.</span><span class="sxs-lookup"><span data-stu-id="1a6bc-107">hello diagram illustrates hello parts of a complete SQL Server Availability Group in Azure Virtual Machines.</span></span>

![Groupe de disponibilité](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

<span data-ttu-id="1a6bc-109">Hello différence essentielle pour un groupe de disponibilité dans des Machines virtuelles Azure est que hello des machines virtuelles, nécessitent un [l’équilibrage de charge](../../../load-balancer/load-balancer-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1a6bc-109">hello key difference for an Availability Group in Azure Virtual Machines is that hello Azure virtual machines, require a [load balancer](../../../load-balancer/load-balancer-overview.md).</span></span> <span data-ttu-id="1a6bc-110">équilibrage de charge Hello conserve des adresses IP hello pour l’écouteur du groupe de disponibilité hello.</span><span class="sxs-lookup"><span data-stu-id="1a6bc-110">hello load balancer holds hello IP addresses for hello availability group listener.</span></span> <span data-ttu-id="1a6bc-111">Si vous avez plusieurs groupes de disponibilité, chacun requiert un écouteur.</span><span class="sxs-lookup"><span data-stu-id="1a6bc-111">If you have more than one availability group each group requires a listener.</span></span> <span data-ttu-id="1a6bc-112">Un équilibrage de charge prend en charge plusieurs écouteurs.</span><span class="sxs-lookup"><span data-stu-id="1a6bc-112">One load balancer can support multiple listeners.</span></span>

<span data-ttu-id="1a6bc-113">Lorsque vous êtes prêt toobuild un aroup de disponibilité de SQL Server sur des Machines virtuelles Azure, consultez les didacticiels toothese.</span><span class="sxs-lookup"><span data-stu-id="1a6bc-113">When you are ready toobuild a SQL Server availability aroup on Azure Virtual Machines, refer toothese tutorials.</span></span>

## <a name="automatically-create-an-availability-group-from-a-template"></a><span data-ttu-id="1a6bc-114">Créer automatiquement un groupe de disponibilité à l’aide d’un modèle</span><span class="sxs-lookup"><span data-stu-id="1a6bc-114">Automatically create an availability group from a template</span></span>

[<span data-ttu-id="1a6bc-115">Configurer automatiquement un groupe de disponibilité AlwaysOn dans une machine virtuelle Azure - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1a6bc-115">Configure Always On availability group in Azure VM automatically - Resource Manager</span></span>](virtual-machines-windows-portal-sql-alwayson-availability-groups.md)

## <a name="manually-create-an-availability-group-in-azure-portal"></a><span data-ttu-id="1a6bc-116">Créer manuellement un groupe de disponibilité dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="1a6bc-116">Manually create an availability group in Azure portal</span></span>

<span data-ttu-id="1a6bc-117">Vous pouvez également créer les ordinateurs virtuels hello vous-même sans modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="1a6bc-117">You can also create hello virtual machines yourself without hello template.</span></span> <span data-ttu-id="1a6bc-118">Tout d’abord, effectuer des conditions préalables de hello, puis créez le groupe de disponibilité hello.</span><span class="sxs-lookup"><span data-stu-id="1a6bc-118">First, complete hello prerequisites, then create hello availability group.</span></span> <span data-ttu-id="1a6bc-119">Consultez hello rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="1a6bc-119">See hello following topics:</span></span> 

- [<span data-ttu-id="1a6bc-120">Remplir les conditions requises pour les groupes de disponibilité AlwaysOn SQL Server sur les machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="1a6bc-120">Configure prerequisites for SQL Server Always On availability groups on Azure Virtual Machines</span></span>](virtual-machines-windows-portal-sql-availability-group-prereq.md)

- [<span data-ttu-id="1a6bc-121">Créer groupe de disponibilité AlwaysOn tooimprove disponibilité et récupération d’urgence</span><span class="sxs-lookup"><span data-stu-id="1a6bc-121">Create Always On Availability Group tooimprove availability and disaster recovery</span></span>](virtual-machines-windows-portal-sql-availability-group-tutorial.md)

## <a name="next-steps"></a><span data-ttu-id="1a6bc-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1a6bc-122">Next steps</span></span>

<span data-ttu-id="1a6bc-123">[Configurer un groupe de disponibilité AlwaysOn SQL Server sur des machines virtuelles dans différentes régions](virtual-machines-windows-portal-sql-availability-group-dr.md).</span><span class="sxs-lookup"><span data-stu-id="1a6bc-123">[Configure a SQL Server Always On Availability Group on Azure Virtual Machines in Different Regions](virtual-machines-windows-portal-sql-availability-group-dr.md).</span></span>
