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
# <a name="introducing-sql-server-always-on-availability-groups-on-azure-virtual-machines"></a>Présentation des groupes de disponibilité SQL Server AlwaysOn sur des machines virtuelles Azure #

Cet article présente les groupes de disponibilité de SQL Server sur les machines virtuelles Azure. 

Toujours sur les groupes de disponibilité sur des Machines virtuelles Azure sont tooAlways similaires sur les groupes de disponibilité local. Pour plus d’informations, voir [Groupes de disponibilité AlwaysOn (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx). 

diagramme de Hello illustre les parties de hello d’un groupe de disponibilité de serveur dans les Machines virtuelles Azure SQL complète.

![Groupe de disponibilité](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

Hello différence essentielle pour un groupe de disponibilité dans des Machines virtuelles Azure est que hello des machines virtuelles, nécessitent un [l’équilibrage de charge](../../../load-balancer/load-balancer-overview.md). équilibrage de charge Hello conserve des adresses IP hello pour l’écouteur du groupe de disponibilité hello. Si vous avez plusieurs groupes de disponibilité, chacun requiert un écouteur. Un équilibrage de charge prend en charge plusieurs écouteurs.

Lorsque vous êtes prêt toobuild un aroup de disponibilité de SQL Server sur des Machines virtuelles Azure, consultez les didacticiels toothese.

## <a name="automatically-create-an-availability-group-from-a-template"></a>Créer automatiquement un groupe de disponibilité à l’aide d’un modèle

[Configurer automatiquement un groupe de disponibilité AlwaysOn dans une machine virtuelle Azure - Resource Manager](virtual-machines-windows-portal-sql-alwayson-availability-groups.md)

## <a name="manually-create-an-availability-group-in-azure-portal"></a>Créer manuellement un groupe de disponibilité dans le portail Azure

Vous pouvez également créer les ordinateurs virtuels hello vous-même sans modèle de hello. Tout d’abord, effectuer des conditions préalables de hello, puis créez le groupe de disponibilité hello. Consultez hello rubriques suivantes : 

- [Remplir les conditions requises pour les groupes de disponibilité AlwaysOn SQL Server sur les machines virtuelles Azure](virtual-machines-windows-portal-sql-availability-group-prereq.md)

- [Créer groupe de disponibilité AlwaysOn tooimprove disponibilité et récupération d’urgence](virtual-machines-windows-portal-sql-availability-group-tutorial.md)

## <a name="next-steps"></a>Étapes suivantes

[Configurer un groupe de disponibilité AlwaysOn SQL Server sur des machines virtuelles dans différentes régions](virtual-machines-windows-portal-sql-availability-group-dr.md).
