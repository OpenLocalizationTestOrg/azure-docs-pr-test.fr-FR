---
title: aaaGet un ID de machine virtuelle Azure Linux | Documents Microsoft
description: "Décrit comment tooget et utilisez un Unique de machine virtuelle Azure Linux ID."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: kmouss
manager: timlt
editor: 
ms.assetid: 136c5d28-ff6b-4466-b27f-7a29785b5d27
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 01/23/2017
ms.author: kmouss
ms.openlocfilehash: 4c8ddfc2e892824581e77649285ee8adbccd5def
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-and-using-azure-vm-unique-id"></a><span data-ttu-id="e1f00-103">Accès et utilisation de l’ID unique de machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="e1f00-103">Accessing and Using Azure VM Unique ID</span></span>
<span data-ttu-id="e1f00-104">L’ID unique de machine virtuelle Azure est un identificateur 128 bits codé et stocké dans le SMBIOS de la machine virtuelle IaaS Azure et qui peut être lu simultanément à l’aide des commandes du BIOS de la plate-forme.</span><span class="sxs-lookup"><span data-stu-id="e1f00-104">Azure VM unique ID is a 128bits identifier encoded and stored in all Azure IaaS VM’s SMBIOS and can currently be read using platform BIOS commands.</span></span>

<span data-ttu-id="e1f00-105">L’ID unique de machine virtuelle Azure est une propriété en lecture seule.</span><span class="sxs-lookup"><span data-stu-id="e1f00-105">Azure VM unique ID is a Read-only property.</span></span> <span data-ttu-id="e1f00-106">L’ID unique de machine virtuelle Azure ne sera pas modifié lors de l’arrêt pour redémarrage (planifié ou non planifié), lors du démarrage ou de l’arrêt pour désallouer, lors d’une réparation de service ou de la restauration en place.</span><span class="sxs-lookup"><span data-stu-id="e1f00-106">Azure Unique VM ID won’t change upon reboot shutdown (either planned for unplanned), Start/Stop de-allocate, service healing or restore in place.</span></span> <span data-ttu-id="e1f00-107">Toutefois, si hello machine virtuelle est un toocreate de capture instantanée et à copier une nouvelle instance, le nouvel ID de machine virtuelle Azure est configuré.</span><span class="sxs-lookup"><span data-stu-id="e1f00-107">However, if hello VM is a snapshot and copied toocreate a new instance, new Azure VM ID is configured.</span></span>

> [!NOTE]
> <span data-ttu-id="e1f00-108">Si vous avez des machines virtuelles plus anciennes et que vous en cours d’exécution, car cette nouvelle fonctionnalité a été transférée (18 septembre 2014), redémarrez votre machine virtuelle tooautomatically obtenir un ID unique de Azure.</span><span class="sxs-lookup"><span data-stu-id="e1f00-108">If you have older VMs created and running since this new feature got rolled out (September 18, 2014), please restart your VM tooautomatically get an Azure unique ID.</span></span>
> 
> 

<span data-ttu-id="e1f00-109">tooaccess Unique ID de machine virtuelle Azure à partir de hello machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="e1f00-109">tooaccess Azure Unique VM ID from within hello VM:</span></span>

## <a name="create-a-vm"></a><span data-ttu-id="e1f00-110">Créer une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e1f00-110">Create a VM</span></span>
<span data-ttu-id="e1f00-111">Pour plus d’informations, consultez [Création d’une machine virtuelle](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="e1f00-111">For more information, see [Create a Virtual Machine](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="connect-toohello-vm"></a><span data-ttu-id="e1f00-112">Se connecter toohello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e1f00-112">Connect toohello VM</span></span>
<span data-ttu-id="e1f00-113">Pour plus d’informations, consultez [SSH à partir de Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="e1f00-113">For more information, see [SSH from Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="query-vm-unique-id"></a><span data-ttu-id="e1f00-114">Interrogation de l’ID unique de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e1f00-114">Query VM Unique ID</span></span>
<span data-ttu-id="e1f00-115">Commande (l’exemple utilise **Ubuntu**) :</span><span class="sxs-lookup"><span data-stu-id="e1f00-115">Command (example uses **Ubuntu**):</span></span>

```bash
sudo dmidecode | grep UUID
```

<span data-ttu-id="e1f00-116">Résultats attendus de l’exemple :</span><span class="sxs-lookup"><span data-stu-id="e1f00-116">Example Expected Results:</span></span>

```bash
UUID: 090556DA-D4FA-764F-A9F1-63614EDA019A
```

<span data-ttu-id="e1f00-117">En raison de tooBig Endian ordre des bits, hello ID de machine virtuelle Unique réel dans ce cas sera :</span><span class="sxs-lookup"><span data-stu-id="e1f00-117">Due tooBig Endian bit ordering, hello actual Unique VM ID in this case will be:</span></span>

```bash
DA 56 05 09 – FA D4 – 4f 76 - A9F1-63614EDA019A
```

<span data-ttu-id="e1f00-118">ID unique d’ordinateur virtuel Azure peut servir dans différents scénarios si hello machine virtuelle s’exécute sur Azure ou sur site et peut aider à vos spécifications de suivi de licence, création de rapports ou générales que peut avoir sur vos déploiements Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="e1f00-118">Azure VM unique ID can be used in different scenarios whether hello VM is running on Azure or on-premises and can help your licensing, reporting or general tracking requirements you may have on your Azure IaaS deployments.</span></span> <span data-ttu-id="e1f00-119">Éditeurs de logiciels de création d’applications et de les certifier sur Azure peuvent nécessiter tooidentify une machine virtuelle de Azure tout au long de son cycle de vie et le tootell si hello machine virtuelle s’exécute sur Azure, localement ou sur d’autres fournisseurs cloud.</span><span class="sxs-lookup"><span data-stu-id="e1f00-119">Many independent software vendors building applications and certifying them on Azure may require tooidentify an Azure VM throughout its lifecycle and tootell if hello VM is running on Azure, on-Premises or on other cloud providers.</span></span> <span data-ttu-id="e1f00-120">Cet identificateur de la plateforme peut par exemple permettent de détecter si hello logiciel est correctement concédé sous licence ou aider à n’importe quelle source de tooits de données de machine virtuelle comme tooassist sur la définition des métriques de droite hello pour la plate-forme hello et tootrack toocorrelate et mettre en corrélation ces mesures dans la liste autres utilisations.</span><span class="sxs-lookup"><span data-stu-id="e1f00-120">This platform identifier can for example help detect if hello software is properly licensed or help toocorrelate any VM data tooits source such as tooassist on setting hello right metrics for hello right platform and tootrack and correlate these metrics amongst other uses.</span></span>

