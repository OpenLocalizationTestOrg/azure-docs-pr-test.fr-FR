---
title: "Créer un nom de domaine complet pour une machine virtuelle Windows dans le portail Azure | Microsoft Docs"
description: "Apprenez à créer un nom de domaine complet pour une machine virtuelle Resource Manager dans le portail Azure."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a2ae5887-76df-485e-ae19-0efd96df8600
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2d5a555cd873222efcdb29e8eb3aaf128a24414b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-fully-qualified-domain-name-in-the-azure-portal-for-a-windows-vm"></a><span data-ttu-id="090a5-103">Créer un nom de domaine complet dans le portail Azure pour une machine virtuelle Windows</span><span class="sxs-lookup"><span data-stu-id="090a5-103">Create a fully qualified domain name in the Azure portal for a Windows VM</span></span>

<span data-ttu-id="090a5-104">Lorsque vous créez une machine virtuelle dans le [portail Azure](https://portal.azure.com), une ressource d’adresse IP publique est créée automatiquement pour la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="090a5-104">When you create a virtual machine (VM) in the [Azure portal](https://portal.azure.com), a public IP resource for the virtual machine is automatically created.</span></span> <span data-ttu-id="090a5-105">Vous utilisez cette adresse IP pour accéder à distance à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="090a5-105">You use this IP address to remotely access the VM.</span></span> <span data-ttu-id="090a5-106">Bien que le portail ne crée pas de [nom de domaine complet](https://en.wikipedia.org/wiki/Fully_qualified_domain_name) (FQDN), vous pouvez en créer un une fois la machine virtuelle créée.</span><span class="sxs-lookup"><span data-stu-id="090a5-106">Although the portal does not create a [fully qualified domain name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), or FQDN, you can create one once the VM is created.</span></span> <span data-ttu-id="090a5-107">Cet article explique les étapes pour créer un nom DNS ou un nom de domaine complet.</span><span class="sxs-lookup"><span data-stu-id="090a5-107">This article demonstrates the steps to create a DNS name or FQDN.</span></span>

## <a name="create-a-fqdn"></a><span data-ttu-id="090a5-108">Créer un nom de domaine complet</span><span class="sxs-lookup"><span data-stu-id="090a5-108">Create a FQDN</span></span>
<span data-ttu-id="090a5-109">Cet article suppose que vous avez déjà créé une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="090a5-109">This article assumes that you have already created a VM.</span></span> <span data-ttu-id="090a5-110">Si nécessaire, vous pouvez [créer une machine virtuelle dans le portail](quick-create-portal.md) ou [avec Azure PowerShell](quick-create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="090a5-110">If needed, you can [create a VM in the portal](quick-create-portal.md) or [with Azure PowerShell](quick-create-powershell.md).</span></span> <span data-ttu-id="090a5-111">Une fois que votre machine virtuelle est en cours d’exécution, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="090a5-111">Follow these steps once your VM is up and running:</span></span>

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

<span data-ttu-id="090a5-112">Vous pouvez maintenant vous connecter à distance à la machine virtuelle à l’aide de ce nom DNS comme pour Remote Desktop Protocol (RDP).</span><span class="sxs-lookup"><span data-stu-id="090a5-112">You can now connect remotely to the VM using this DNS name such as for Remote Desktop Protocol (RDP).</span></span>

## <a name="next-steps"></a><span data-ttu-id="090a5-113">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="090a5-113">Next steps</span></span>
<span data-ttu-id="090a5-114">Maintenant que votre machine virtuelle a un nom DNS et une IP publique, vous pouvez déployer des infrastructures d’applications courantes ou des services tels qu’IIS, SQL ou SharePoint.</span><span class="sxs-lookup"><span data-stu-id="090a5-114">Now that your VM has a public IP and DNS name, you can deploy common application frameworks or services such as IIS, SQL, or SharePoint.</span></span>

<span data-ttu-id="090a5-115">Vous pouvez également lire un autre article sur [l’utilisation de Resource Manager](../../azure-resource-manager/resource-group-overview.md) pour obtenir des conseils sur la création de vos déploiements Azure.</span><span class="sxs-lookup"><span data-stu-id="090a5-115">You can also read more about [using Resource Manager](../../azure-resource-manager/resource-group-overview.md) for tips on building your Azure deployments.</span></span>

