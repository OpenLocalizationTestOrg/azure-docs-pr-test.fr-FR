---
title: "Créer une identité professionnelle ou scolaire dans AAD pour Windows | Microsoft Docs"
description: "Découvrez comment créer une identité professionnelle ou scolaire dans Azure Active Directory à utiliser avec vos machines virtuelles Windows."
services: virtual-machines-windows
documentationcenter: 
author: squillace
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: d07dca34-618a-48aa-9971-03d9c1210f4a
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/23/2016
ms.author: rasquill
ms.openlocfilehash: 7694b959a384aaed213adc31e02debca31b7c131
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="creating-a-work-or-school-identity-in-azure-active-directory-to-use-with-windows-vms"></a><span data-ttu-id="c256d-103">Création d’une identité professionnelle ou scolaire dans Azure Active Directory à utiliser avec des machines virtuelles Windows</span><span class="sxs-lookup"><span data-stu-id="c256d-103">Creating a Work or School identity in Azure Active Directory to use with Windows VMs</span></span>
<span data-ttu-id="c256d-104">Si vous avez créé un compte Azure personnel ou si vous disposez d’un abonnement MSDN personnel et avez créé le compte Azure pour profiter des crédits Azure MSDN, cela signifie que vous avez utilisé une identité de *compte Microsoft* pour le créer.</span><span class="sxs-lookup"><span data-stu-id="c256d-104">If you created a personal Azure account or have a personal MSDN subscription and created the Azure account to take advantage of the MSDN Azure credits -- you used a *Microsoft account* identity to create it.</span></span> <span data-ttu-id="c256d-105">Pour fonctionner correctement, de nombreuses fonctionnalités d'Azure, parmi lesquelles les [modèles de groupes de ressources](../../azure-resource-manager/resource-group-overview.md) , nécessitent un compte professionnel ou scolaire (une identité gérée par Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="c256d-105">Many great features of Azure -- [resource group templates](../../azure-resource-manager/resource-group-overview.md) is one example -- require a work or school account (an identity managed by Azure Active Directory) to work.</span></span> <span data-ttu-id="c256d-106">Vous pouvez suivre les instructions ci-dessous pour créer un compte professionnel ou scolaire car, heureusement, l’un des atouts de votre compte personnel Azure est qu'il est fourni avec un domaine Azure Active Directory par défaut que vous pouvez utiliser pour créer un nouveau compte professionnel ou scolaire à utiliser avec les fonctionnalités Azure qui le nécessitent.</span><span class="sxs-lookup"><span data-stu-id="c256d-106">You can follow the instructions below to create a new work or school account because fortunately, one of the best things about your personal Azure account is that it comes with a default Azure Active Directory domain that you can use to create a new work or school account that you can use with Azure features that require it.</span></span>

<span data-ttu-id="c256d-107">Toutefois, de récentes modifications permettent de gérer votre abonnement avec n’importe quel type de compte Azure grâce à la `azure login` méthode de connexion interactive décrite [ici](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="c256d-107">However, recent changes make it possible to manage your subscription with any type of Azure account using the `azure login` interactive login method described [here](../../xplat-cli-connect.md).</span></span> <span data-ttu-id="c256d-108">Vous pouvez utiliser ce mécanisme ou suivre les instructions ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="c256d-108">You can either use that mechanism, or you can follow the instructions that follow.</span></span> <span data-ttu-id="c256d-109">Vous pouvez également [créer une identité professionnelle ou scolaire dans Azure Active Directory à utiliser avec des machines virtuelles Linux](../linux/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c256d-109">You can also [create a work or school identity in Azure Active Directory to use with Linux VMs](../linux/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

[!INCLUDE [virtual-machines-common-create-aad-work-id](../../../includes/virtual-machines-common-create-aad-work-id.md)]

