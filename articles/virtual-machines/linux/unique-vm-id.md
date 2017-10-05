---
title: Obtenir un ID de machine virtuelle Linux Azure | Microsoft Docs
description: "Décrit comment obtenir et utiliser un ID de machine virtuelle Linux Azure unique."
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
ms.openlocfilehash: 258ce425d5692730011cf2f4468dc0ba77f4cb79
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="accessing-and-using-azure-vm-unique-id"></a><span data-ttu-id="093ad-103">Accès et utilisation de l’ID unique de machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="093ad-103">Accessing and Using Azure VM Unique ID</span></span>
<span data-ttu-id="093ad-104">L’ID unique de machine virtuelle Azure est un identificateur 128 bits codé et stocké dans le SMBIOS de la machine virtuelle IaaS Azure et qui peut être lu simultanément à l’aide des commandes du BIOS de la plate-forme.</span><span class="sxs-lookup"><span data-stu-id="093ad-104">Azure VM unique ID is a 128bits identifier encoded and stored in all Azure IaaS VM’s SMBIOS and can currently be read using platform BIOS commands.</span></span>

<span data-ttu-id="093ad-105">L’ID unique de machine virtuelle Azure est une propriété en lecture seule.</span><span class="sxs-lookup"><span data-stu-id="093ad-105">Azure VM unique ID is a Read-only property.</span></span> <span data-ttu-id="093ad-106">L’ID unique de machine virtuelle Azure ne sera pas modifié lors de l’arrêt pour redémarrage (planifié ou non planifié), lors du démarrage ou de l’arrêt pour désallouer, lors d’une réparation de service ou de la restauration en place.</span><span class="sxs-lookup"><span data-stu-id="093ad-106">Azure Unique VM ID won’t change upon reboot shutdown (either planned for unplanned), Start/Stop de-allocate, service healing or restore in place.</span></span> <span data-ttu-id="093ad-107">Toutefois, si la machine virtuelle est un instantané copié pour créer une nouvelle instance, un nouvel ID de machine virtuelle Azure est configuré.</span><span class="sxs-lookup"><span data-stu-id="093ad-107">However, if the VM is a snapshot and copied to create a new instance, new Azure VM ID is configured.</span></span>

> [!NOTE]
> <span data-ttu-id="093ad-108">Si vous avez des machines virtuelles plus anciennes créées et en cours d’exécution depuis que cette nouvelle fonctionnalité a été déployée (18 septembre 2014), veuillez redémarrer votre machine virtuelle pour obtenir automatiquement un ID unique Azure.</span><span class="sxs-lookup"><span data-stu-id="093ad-108">If you have older VMs created and running since this new feature got rolled out (September 18, 2014), please restart your VM to automatically get an Azure unique ID.</span></span>
> 
> 

<span data-ttu-id="093ad-109">Pour accéder à l’ID unique de machine virtuelle Azure à partir de la machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="093ad-109">To access Azure Unique VM ID from within the VM:</span></span>

## <a name="create-a-vm"></a><span data-ttu-id="093ad-110">Créer une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="093ad-110">Create a VM</span></span>
<span data-ttu-id="093ad-111">Pour plus d’informations, consultez [Création d’une machine virtuelle](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="093ad-111">For more information, see [Create a Virtual Machine](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="connect-to-the-vm"></a><span data-ttu-id="093ad-112">Connexion à la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="093ad-112">Connect to the VM</span></span>
<span data-ttu-id="093ad-113">Pour plus d’informations, consultez [SSH à partir de Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="093ad-113">For more information, see [SSH from Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="query-vm-unique-id"></a><span data-ttu-id="093ad-114">Interrogation de l’ID unique de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="093ad-114">Query VM Unique ID</span></span>
<span data-ttu-id="093ad-115">Commande (l’exemple utilise **Ubuntu**) :</span><span class="sxs-lookup"><span data-stu-id="093ad-115">Command (example uses **Ubuntu**):</span></span>

```bash
sudo dmidecode | grep UUID
```

<span data-ttu-id="093ad-116">Résultats attendus de l’exemple :</span><span class="sxs-lookup"><span data-stu-id="093ad-116">Example Expected Results:</span></span>

```bash
UUID: 090556DA-D4FA-764F-A9F1-63614EDA019A
```

<span data-ttu-id="093ad-117">En raison du classement de bit Big Endian, l’ID unique de machine virtuelle réel dans ce cas sera :</span><span class="sxs-lookup"><span data-stu-id="093ad-117">Due to Big Endian bit ordering, the actual Unique VM ID in this case will be:</span></span>

```bash
DA 56 05 09 – FA D4 – 4f 76 - A9F1-63614EDA019A
```

<span data-ttu-id="093ad-118">L’ID unique de machine virtuelle Azure peut être utilisé dans différents scénarios selon si la machine virtuelle s’exécute sur Azure ou en local, et il peut vous aider avec vos exigences en matière de licence, de création de rapports ou de suivi général sur vos déploiements IaaS Azure.</span><span class="sxs-lookup"><span data-stu-id="093ad-118">Azure VM unique ID can be used in different scenarios whether the VM is running on Azure or on-premises and can help your licensing, reporting or general tracking requirements you may have on your Azure IaaS deployments.</span></span> <span data-ttu-id="093ad-119">Plusieurs éditeurs de logiciels indépendants créant des applications et les certifiant sur Azure peuvent avoir besoin d’identifier une machine virtuelle Azure tout au long de son cycle de vie et pour savoir si la machine virtuelle s’exécute sur Azure, en local ou sur d’autres fournisseurs de cloud.</span><span class="sxs-lookup"><span data-stu-id="093ad-119">Many independent software vendors building applications and certifying them on Azure may require to identify an Azure VM throughout its lifecycle and to tell if the VM is running on Azure, on-Premises or on other cloud providers.</span></span> <span data-ttu-id="093ad-120">Cet identificateur de plate-forme peut par exemple aider à détecter si le logiciel est concédé sous licence correctement ou il peut vous aider à mettre en corrélation des données de machine virtuelle avec la source, afin de vous permettre de définir les mesures correctes pour la bonne plate-forme, ainsi que suivre et mettre en corrélation ces mesures avec d’autres utilisations.</span><span class="sxs-lookup"><span data-stu-id="093ad-120">This platform identifier can for example help detect if the software is properly licensed or help to correlate any VM data to its source such as to assist on setting the right metrics for the right platform and to track and correlate these metrics amongst other uses.</span></span>

