---
title: "aaaCreate une identité ou d’établissement scolaire dans AAD pour Linux | Documents Microsoft"
description: "Découvrez comment toocreate une identité ou d’établissement scolaire dans toouse Azure Active Directory avec vos machines virtuelles de Linux."
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: b0f86d77-c669-4aa1-a095-c2aa4d9105fe
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/23/2016
ms.author: rasquill
ms.openlocfilehash: 54c3d0b0e89fe1b2d6a9b58a46776fe446ed72b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-a-work-or-school-identity-in-azure-active-directory-toouse-with-linux-vms"></a><span data-ttu-id="d69dc-103">Création d’une identité d’entreprise ou école dans toouse Azure Active Directory avec les machines virtuelles Linux</span><span class="sxs-lookup"><span data-stu-id="d69dc-103">Creating a Work or School identity in Azure Active Directory toouse with Linux VMs</span></span>
<span data-ttu-id="d69dc-104">Si vous avez créé un compte Azure personnel ou que vous disposer d’un abonnement MSDN personnel créé parti de tootake compte Azure hello de crédits de MSDN Azure hello--que vous avez utilisé un *compte Microsoft* identité toocreate il.</span><span class="sxs-lookup"><span data-stu-id="d69dc-104">If you created a personal Azure account or have a personal MSDN subscription and created hello Azure account tootake advantage of hello MSDN Azure credits -- you used a *Microsoft account* identity toocreate it.</span></span> <span data-ttu-id="d69dc-105">Nombreuses fonctionnalités d’Azure-- [modèles de groupe de ressources](../../azure-resource-manager/resource-group-overview.md) est un exemple--requièrent un compte professionnel ou scolaire (une identité géré par Azure Active Directory) toowork.</span><span class="sxs-lookup"><span data-stu-id="d69dc-105">Many great features of Azure -- [resource group templates](../../azure-resource-manager/resource-group-overview.md) is one example -- require a work or school account (an identity managed by Azure Active Directory) toowork.</span></span> <span data-ttu-id="d69dc-106">Vous pouvez suivre les instructions hello ci-dessous toocreate nouveau Professionnel ou scolaire compte étant Heureusement, un des principaux avantages de votre compte Azure personnel hello qui l’accompagne un domaine d’Azure Active Directory par défaut que vous pouvez utiliser toocreate nouveau Professionnel ou scolaire compte que vous pouvez utiliser avec les fonctionnalités Azure qui en ont besoin.</span><span class="sxs-lookup"><span data-stu-id="d69dc-106">You can follow hello instructions below toocreate a new work or school account because fortunately, one of hello best things about your personal Azure account is that it comes with a default Azure Active Directory domain that you can use toocreate a new work or school account that you can use with Azure features that require it.</span></span>

<span data-ttu-id="d69dc-107">Toutefois, les modifications récentes rendent possible toomanage votre abonnement avec n’importe quel type de compte Azure à l’aide de hello `azure login` méthode de connexion interactive décrite [ici](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="d69dc-107">However, recent changes make it possible toomanage your subscription with any type of Azure account using hello `azure login` interactive login method described [here](../../xplat-cli-connect.md).</span></span> <span data-ttu-id="d69dc-108">Vous pouvez utiliser ce mécanisme, ou vous pouvez suivre les instructions hello qui suivent.</span><span class="sxs-lookup"><span data-stu-id="d69dc-108">You can either use that mechanism, or you can follow hello instructions that follow.</span></span> <span data-ttu-id="d69dc-109">Vous pouvez également [créer une identité ou d’établissement scolaire dans toouse Azure Active Directory avec les machines virtuelles Windows](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d69dc-109">You can also [create a work or school identity in Azure Active Directory toouse with Windows VMs](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

[!INCLUDE [virtual-machines-common-create-aad-work-id](../../../includes/virtual-machines-common-create-aad-work-id.md)]

