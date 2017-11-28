---
title: aaaCreate nom de domaine complet pour un VM Linux Bonjour portail Azure | Documents Microsoft
description: "Découvrez comment toocreate un nom de domaine complet ou le nom de domaine complet pour un gestionnaire de ressources en fonction de machine virtuelle dans hello portail Azure."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 2cd6c249-a737-4a0a-b5ba-e1c09e551b30
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1494a0cb1caa62069c72096a739aee111ac8b383
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-qualified-domain-name-in-hello-azure-portal-for-a-linux-vm"></a><span data-ttu-id="28af2-103">Créer un nom de domaine complet dans hello portail Azure pour un VM Linux</span><span class="sxs-lookup"><span data-stu-id="28af2-103">Create a fully qualified domain name in hello Azure portal for a Linux VM</span></span>

<span data-ttu-id="28af2-104">Lorsque vous créez un ordinateur virtuel (VM) Bonjour [portail Azure](https://portal.azure.com), une ressource IP publique pour l’ordinateur virtuel de hello est automatiquement créée.</span><span class="sxs-lookup"><span data-stu-id="28af2-104">When you create a virtual machine (VM) in hello [Azure portal](https://portal.azure.com), a public IP resource for hello virtual machine is automatically created.</span></span> <span data-ttu-id="28af2-105">Vous utilisez cette hello d’accès IP adresse tooremotely machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="28af2-105">You use this IP address tooremotely access hello VM.</span></span> <span data-ttu-id="28af2-106">Bien que le portail de hello ne crée pas une [nom de domaine complet](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), ou nom de domaine complet, vous pouvez ajouter un fois hello machine virtuelle est créée.</span><span class="sxs-lookup"><span data-stu-id="28af2-106">Although hello portal does not create a [fully qualified domain name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), or FQDN, you can add one once hello VM is created.</span></span> <span data-ttu-id="28af2-107">Cet article explique hello étapes toocreate un nom DNS ou le nom de domaine complet.</span><span class="sxs-lookup"><span data-stu-id="28af2-107">This article demonstrates hello steps toocreate a DNS name or FQDN.</span></span>

## <a name="create-a-fqdn"></a><span data-ttu-id="28af2-108">Créer un nom de domaine complet</span><span class="sxs-lookup"><span data-stu-id="28af2-108">Create a FQDN</span></span>
<span data-ttu-id="28af2-109">Cet article suppose que vous avez déjà créé une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="28af2-109">This article assumes that you have already created a VM.</span></span> <span data-ttu-id="28af2-110">Si nécessaire, vous pouvez [créer une machine virtuelle dans le portail de hello](quick-create-portal.md) ou [avec hello CLI d’Azure](quick-create-cli.md).</span><span class="sxs-lookup"><span data-stu-id="28af2-110">If needed, you can [create a VM in hello portal](quick-create-portal.md) or [with hello Azure CLI](quick-create-cli.md).</span></span> <span data-ttu-id="28af2-111">Une fois que votre machine virtuelle est en cours d’exécution, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="28af2-111">Follow these steps once your VM is up and running:</span></span>

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

<span data-ttu-id="28af2-112">Vous pouvez maintenant vous connecter à distance toohello nom d’ordinateur virtuel à l’aide de ce serveur DNS comme des `ssh azureuser@mydns.westus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="28af2-112">You can now connect remotely toohello VM using this DNS name such as with `ssh azureuser@mydns.westus.cloudapp.azure.com`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="28af2-113">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="28af2-113">Next steps</span></span>
<span data-ttu-id="28af2-114">Maintenant que votre machine virtuelle a un nom DNS et une IP publique, vous pouvez déployer des services ou des infrastructures d’applications tels que nginx, MongoDB, Docker, etc.</span><span class="sxs-lookup"><span data-stu-id="28af2-114">Now that your VM has a public IP and DNS name, you can deploy common application frameworks or services such as nginx, MongoDB, Docker, etc.</span></span>

<span data-ttu-id="28af2-115">Vous pouvez également lire un autre article sur [l’utilisation de Resource Manager](../../azure-resource-manager/resource-group-overview.md) pour obtenir des conseils sur la création de vos déploiements Azure.</span><span class="sxs-lookup"><span data-stu-id="28af2-115">You can also read more about [using Resource Manager](../../azure-resource-manager/resource-group-overview.md) for tips on building your Azure deployments.</span></span>

