---
title: aaaFrequently aux questions sur les machines virtuelles Linux dans Azure | Documents Microsoft
description: "Fournit des toosome réponses hello fréquemment posées sur les ordinateurs virtuels Linux créés avec le modèle de gestionnaire de ressources hello."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-management
ms.assetid: 3648e09c-1115-4818-93c6-688d7a54a353
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: cynthn
ms.openlocfilehash: 0afd08123dddc408851065c46deedc3146dbec20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-question-about-linux-virtual-machines"></a><span data-ttu-id="df4a1-103">Forum aux questions sur les machines virtuelles Linux</span><span class="sxs-lookup"><span data-stu-id="df4a1-103">Frequently asked question about Linux Virtual Machines</span></span>
<span data-ttu-id="df4a1-104">Cet article traite des questions courantes sur les ordinateurs virtuels Linux créés dans Azure à l’aide du modèle de déploiement du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="df4a1-104">This article addresses some common questions about Linux virtual machines created in Azure using hello Resource Manager deployment model.</span></span> <span data-ttu-id="df4a1-105">Pour la version de Windows hello de cette rubrique, consultez [Forum aux questions sur les Machines virtuelles Windows](../windows/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="df4a1-105">For hello Windows version of this topic, see [Frequently asked question about Windows Virtual Machines](../windows/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

## <a name="what-can-i-run-on-an-azure-vm"></a><span data-ttu-id="df4a1-106">Qu’est-il possible d’exécuter sur une machine virtuelle Azure ?</span><span class="sxs-lookup"><span data-stu-id="df4a1-106">What can I run on an Azure VM?</span></span>
<span data-ttu-id="df4a1-107">Tous les abonnés peuvent exécuter des logiciels serveur sur une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="df4a1-107">All subscribers can run server software on an Azure virtual machine.</span></span> <span data-ttu-id="df4a1-108">Pour plus d’informations, consultez [Linux dans des distributions prises en charge par Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="df4a1-108">For more information, see [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a><span data-ttu-id="df4a1-109">Quelle quantité de stockage puis-je utiliser avec une machine virtuelle ?</span><span class="sxs-lookup"><span data-stu-id="df4a1-109">How much storage can I use with a virtual machine?</span></span>
<span data-ttu-id="df4a1-110">Chaque disque de données peut être jusqu'à too1 to.</span><span class="sxs-lookup"><span data-stu-id="df4a1-110">Each data disk can be up too1 TB.</span></span> <span data-ttu-id="df4a1-111">nombre de Hello de disques de données que vous pouvez utiliser dépend de la taille de hello de machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="df4a1-111">hello number of data disks you can use depends on hello size of hello virtual machine.</span></span> <span data-ttu-id="df4a1-112">Pour en savoir plus, voir la rubrique [Tailles de machines virtuelles](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="df4a1-112">For details, see [Sizes for Virtual Machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="df4a1-113">Un compte de stockage Azure fournit le stockage de disque de système d’exploitation hello et les disques de données.</span><span class="sxs-lookup"><span data-stu-id="df4a1-113">An Azure storage account provides storage for hello operating system disk and any data disks.</span></span> <span data-ttu-id="df4a1-114">Chaque disque est un fichier .vhd stocké sous la forme d’un objet blob de pages.</span><span class="sxs-lookup"><span data-stu-id="df4a1-114">Each disk is a .vhd file stored as a page blob.</span></span> <span data-ttu-id="df4a1-115">Pour plus d’informations sur la tarification, voir [Tarification – Stockage](https://azure.microsoft.com/pricing/details/storage/).</span><span class="sxs-lookup"><span data-stu-id="df4a1-115">For pricing details, see [Storage Pricing Details](https://azure.microsoft.com/pricing/details/storage/).</span></span>

## <a name="how-can-i-access-my-virtual-machine"></a><span data-ttu-id="df4a1-116">Comment puis-je accéder à ma machine virtuelle ?</span><span class="sxs-lookup"><span data-stu-id="df4a1-116">How can I access my virtual machine?</span></span>
<span data-ttu-id="df4a1-117">Établir une toolog de connexion à distance sur l’ordinateur virtuel de toohello, à l’aide de Secure Shell (SSH).</span><span class="sxs-lookup"><span data-stu-id="df4a1-117">Establish a remote connection toolog on toohello virtual machine, using Secure Shell (SSH).</span></span> <span data-ttu-id="df4a1-118">Consultez les instructions de hello sur la façon de tooconnect [à partir de Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [de Linux et Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="df4a1-118">See hello instructions on how tooconnect [from Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [from Linux and Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="df4a1-119">Par défaut, SSH autorise un maximum de 10 connexions simultanées.</span><span class="sxs-lookup"><span data-stu-id="df4a1-119">By default, SSH allows a maximum of 10 concurrent connections.</span></span> <span data-ttu-id="df4a1-120">Vous pouvez augmenter ce nombre en modifiant le fichier de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="df4a1-120">You can increase this number by editing hello configuration file.</span></span>

<span data-ttu-id="df4a1-121">Si vous rencontrez des problèmes, consultez [Dépanner les connexions Secure Shell (SSH)](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="df4a1-121">If you’re having problems, check out [Troubleshoot Secure Shell (SSH) connections](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="can-i-use-hello-temporary-disk-devsdb1-toostore-data"></a><span data-ttu-id="df4a1-122">Puis-je utiliser des données de toostore hello disque temporaire (/ dev/sdb1) ?</span><span class="sxs-lookup"><span data-stu-id="df4a1-122">Can I use hello temporary disk (/dev/sdb1) toostore data?</span></span>
<span data-ttu-id="df4a1-123">N’utilisez pas les données de toostore salutation disque temporaire (/ dev/sdb1).</span><span class="sxs-lookup"><span data-stu-id="df4a1-123">Don't use hello temporary disk (/dev/sdb1) toostore data.</span></span> <span data-ttu-id="df4a1-124">Il s’agit uniquement d’un stockage temporaire.</span><span class="sxs-lookup"><span data-stu-id="df4a1-124">It is only there for temporary storage.</span></span> <span data-ttu-id="df4a1-125">Vous risquez de perdre des données qui ne pourront pas être récupérées.</span><span class="sxs-lookup"><span data-stu-id="df4a1-125">You risk losing data that can’t be recovered.</span></span>

## <a name="can-i-copy-or-clone-an-existing-azure-vm"></a><span data-ttu-id="df4a1-126">Puis-je copier ou cloner une machine virtuelle Azure ?</span><span class="sxs-lookup"><span data-stu-id="df4a1-126">Can I copy or clone an existing Azure VM?</span></span>
<span data-ttu-id="df4a1-127">Oui.</span><span class="sxs-lookup"><span data-stu-id="df4a1-127">Yes.</span></span> <span data-ttu-id="df4a1-128">Pour obtenir des instructions, consultez [comment toocreate une copie de la machine virtuelle Linux dans hello modèle de déploiement de gestionnaire de ressources](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="df4a1-128">For instructions, see [How toocreate a copy of a Linux virtual machine in hello Resource Manager deployment model](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="why-am-i-not-seeing-canada-central-and-canada-east-regions-through-azure-resource-manager"></a><span data-ttu-id="df4a1-129">Pourquoi ne vois-je pas les régions Centre et Est du Canada dans Azure Resource Manager ?</span><span class="sxs-lookup"><span data-stu-id="df4a1-129">Why am I not seeing Canada Central and Canada East regions through Azure Resource Manager?</span></span>
<span data-ttu-id="df4a1-130">Hello deux nouvelles régions du Canada Central et est du Canada ne sont pas automatiquement inscrits pour la création de la machine virtuelle pour les abonnements Azure existants.</span><span class="sxs-lookup"><span data-stu-id="df4a1-130">hello two new regions of Canada Central and Canada East are not automatically registered for virtual machine creation for existing Azure subscriptions.</span></span> <span data-ttu-id="df4a1-131">Cette inscription s’effectue automatiquement lorsqu’un ordinateur virtuel est déployé par le biais hello tooany portail Azure autre région à l’aide du Gestionnaire de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="df4a1-131">This registration is done automatically when a virtual machine is deployed through hello Azure portal tooany other region using Azure Resource Manager.</span></span> <span data-ttu-id="df4a1-132">Après un ordinateur virtuel est déployé tooany autre région Azure, les régions de nouveau hello doivent être disponibles pour les ordinateurs virtuels suivants.</span><span class="sxs-lookup"><span data-stu-id="df4a1-132">After a virtual machine is deployed tooany other Azure region, hello new regions should be available for subsequent virtual machines.</span></span>

## <a name="can-i-add-a-nic-toomy-vm-after-its-created"></a><span data-ttu-id="df4a1-133">Puis-je ajouter un toomy de carte réseau virtuelle après sa création ?</span><span class="sxs-lookup"><span data-stu-id="df4a1-133">Can I add a NIC toomy VM after it's created?</span></span>
<span data-ttu-id="df4a1-134">Oui, c’est maintenant possible.</span><span class="sxs-lookup"><span data-stu-id="df4a1-134">Yes, this is now possible.</span></span> <span data-ttu-id="df4a1-135">Hello VM première besoins toobe arrêtée désallouée.</span><span class="sxs-lookup"><span data-stu-id="df4a1-135">hello VM first needs toobe stopped deallocated.</span></span> <span data-ttu-id="df4a1-136">Vous pouvez ajouter ou supprimer une carte réseau (sauf s’il est hello dernière NIC sur hello machine virtuelle).</span><span class="sxs-lookup"><span data-stu-id="df4a1-136">Then you can add or remove a NIC (unless it's hello last NIC on hello VM).</span></span> 

## <a name="are-there-any-computer-name-requirements"></a><span data-ttu-id="df4a1-137">Existe-t-il des exigences en matière de nom d’ordinateur ?</span><span class="sxs-lookup"><span data-stu-id="df4a1-137">Are there any computer name requirements?</span></span>
<span data-ttu-id="df4a1-138">Oui.</span><span class="sxs-lookup"><span data-stu-id="df4a1-138">Yes.</span></span> <span data-ttu-id="df4a1-139">nom de l’ordinateur Hello peut être un maximum de 64 caractères.</span><span class="sxs-lookup"><span data-stu-id="df4a1-139">hello computer name can be a maximum of 64 characters in length.</span></span> <span data-ttu-id="df4a1-140">Consultez l’article [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Restrictions et règles de conventions d’affectation de noms) pour en savoir plus sur la dénomination de vos ressources.</span><span class="sxs-lookup"><span data-stu-id="df4a1-140">See [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information around naming your resources.</span></span>

## <a name="are-there-any-resource-group-name-requirements"></a><span data-ttu-id="df4a1-141">Existe-t-il des exigences pour le nom du groupe de ressources ?</span><span class="sxs-lookup"><span data-stu-id="df4a1-141">Are there any resource group name requirements?</span></span>
<span data-ttu-id="df4a1-142">Oui.</span><span class="sxs-lookup"><span data-stu-id="df4a1-142">Yes.</span></span> <span data-ttu-id="df4a1-143">nom de groupe de ressources Hello peut être un maximum de 90 caractères.</span><span class="sxs-lookup"><span data-stu-id="df4a1-143">hello resource group name can be a maximum of 90 characters in length.</span></span> <span data-ttu-id="df4a1-144">Consultez l’article [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Restrictions et règles de conventions d’affectation de noms) pour en savoir plus sur les groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="df4a1-144">See [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information about resource groups.</span></span>

## <a name="what-are-hello-username-requirements-when-creating-a-vm"></a><span data-ttu-id="df4a1-145">Quelles sont les exigences de nom d’utilisateur hello lors de la création d’une machine virtuelle ?</span><span class="sxs-lookup"><span data-stu-id="df4a1-145">What are hello username requirements when creating a VM?</span></span>
<span data-ttu-id="df4a1-146">Les noms d’utilisateur doivent avoir une longueur de 1 à 64 caractères.</span><span class="sxs-lookup"><span data-stu-id="df4a1-146">Usernames must be 1 - 64 characters in length.</span></span>

<span data-ttu-id="df4a1-147">Hello suivant des noms d’utilisateur n’est pas autorisé :</span><span class="sxs-lookup"><span data-stu-id="df4a1-147">hello following usernames are not allowed:</span></span>

<table>
    <tr>
        <td style="text-align:center"><span data-ttu-id="df4a1-148">administrator</span><span class="sxs-lookup"><span data-stu-id="df4a1-148">administrator</span></span> </td><td style="text-align:center"> <span data-ttu-id="df4a1-149">admin</span><span class="sxs-lookup"><span data-stu-id="df4a1-149">admin</span></span> </td><td style="text-align:center"> <span data-ttu-id="df4a1-150">user</span><span class="sxs-lookup"><span data-stu-id="df4a1-150">user</span></span> </td><td style="text-align:center"> <span data-ttu-id="df4a1-151">user1</span><span class="sxs-lookup"><span data-stu-id="df4a1-151">user1</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="df4a1-152">test</span><span class="sxs-lookup"><span data-stu-id="df4a1-152">test</span></span> </td><td style="text-align:center"> <span data-ttu-id="df4a1-153">user2</span><span class="sxs-lookup"><span data-stu-id="df4a1-153">user2</span></span> </td><td style="text-align:center"> <span data-ttu-id="df4a1-154">test1</span><span class="sxs-lookup"><span data-stu-id="df4a1-154">test1</span></span> </td><td style="text-align:center"> <span data-ttu-id="df4a1-155">user3</span><span class="sxs-lookup"><span data-stu-id="df4a1-155">user3</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="df4a1-156">admin1</span><span class="sxs-lookup"><span data-stu-id="df4a1-156">admin1</span></span> </td><td style="text-align:center"> <span data-ttu-id="df4a1-157">1</span><span class="sxs-lookup"><span data-stu-id="df4a1-157">1</span></span> </td><td style="text-align:center"> <span data-ttu-id="df4a1-158">123</span><span class="sxs-lookup"><span data-stu-id="df4a1-158">123</span></span> </td><td style="text-align:center"> <span data-ttu-id="df4a1-159">a</span><span class="sxs-lookup"><span data-stu-id="df4a1-159">a</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="df4a1-160">actuser</span><span class="sxs-lookup"><span data-stu-id="df4a1-160">actuser</span></span>  </td><td style="text-align:center"> <span data-ttu-id="df4a1-161">adm</span><span class="sxs-lookup"><span data-stu-id="df4a1-161">adm</span></span> </td><td style="text-align:center"> <span data-ttu-id="df4a1-162">admin2</span><span class="sxs-lookup"><span data-stu-id="df4a1-162">admin2</span></span> </td><td style="text-align:center"> <span data-ttu-id="df4a1-163">aspnet</span><span class="sxs-lookup"><span data-stu-id="df4a1-163">aspnet</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="df4a1-164">backup</span><span class="sxs-lookup"><span data-stu-id="df4a1-164">backup</span></span> </td><td style="text-align:center"> <span data-ttu-id="df4a1-165">console</span><span class="sxs-lookup"><span data-stu-id="df4a1-165">console</span></span> </td><td style="text-align:center"> <span data-ttu-id="df4a1-166">david</span><span class="sxs-lookup"><span data-stu-id="df4a1-166">david</span></span> </td><td style="text-align:center"> <span data-ttu-id="df4a1-167">guest</span><span class="sxs-lookup"><span data-stu-id="df4a1-167">guest</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="df4a1-168">john</span><span class="sxs-lookup"><span data-stu-id="df4a1-168">john</span></span> </td><td style="text-align:center"> <span data-ttu-id="df4a1-169">propriétaire</span><span class="sxs-lookup"><span data-stu-id="df4a1-169">owner</span></span> </td><td style="text-align:center"> <span data-ttu-id="df4a1-170">root</span><span class="sxs-lookup"><span data-stu-id="df4a1-170">root</span></span> </td><td style="text-align:center"> <span data-ttu-id="df4a1-171">server</span><span class="sxs-lookup"><span data-stu-id="df4a1-171">server</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="df4a1-172">sql</span><span class="sxs-lookup"><span data-stu-id="df4a1-172">sql</span></span> </td><td style="text-align:center"> <span data-ttu-id="df4a1-173">support</span><span class="sxs-lookup"><span data-stu-id="df4a1-173">support</span></span> </td><td style="text-align:center"> <span data-ttu-id="df4a1-174">support_388945a0</span><span class="sxs-lookup"><span data-stu-id="df4a1-174">support_388945a0</span></span> </td><td style="text-align:center"> <span data-ttu-id="df4a1-175">sys</span><span class="sxs-lookup"><span data-stu-id="df4a1-175">sys</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="df4a1-176">test2</span><span class="sxs-lookup"><span data-stu-id="df4a1-176">test2</span></span> </td><td style="text-align:center"> <span data-ttu-id="df4a1-177">test3</span><span class="sxs-lookup"><span data-stu-id="df4a1-177">test3</span></span> </td><td style="text-align:center"> <span data-ttu-id="df4a1-178">user4</span><span class="sxs-lookup"><span data-stu-id="df4a1-178">user4</span></span> </td><td style="text-align:center"> <span data-ttu-id="df4a1-179">user5</span><span class="sxs-lookup"><span data-stu-id="df4a1-179">user5</span></span></td>
    </tr>
</table>


## <a name="what-are-hello-password-requirements-when-creating-a-vm"></a><span data-ttu-id="df4a1-180">Quelles sont les exigences de mot de passe hello lors de la création d’une machine virtuelle ?</span><span class="sxs-lookup"><span data-stu-id="df4a1-180">What are hello password requirements when creating a VM?</span></span>
<span data-ttu-id="df4a1-181">Les mots de passe doivent comporter 6-72 caractères et répondre aux 3 hors hello suivant les exigences de complexité 4 :</span><span class="sxs-lookup"><span data-stu-id="df4a1-181">Passwords must be 6 - 72 characters in length and meet 3 out of hello following 4 complexity requirements:</span></span>

* <span data-ttu-id="df4a1-182">Avoir des minuscules</span><span class="sxs-lookup"><span data-stu-id="df4a1-182">Have lower characters</span></span>
* <span data-ttu-id="df4a1-183">Avoir des majuscules</span><span class="sxs-lookup"><span data-stu-id="df4a1-183">Have upper characters</span></span>
* <span data-ttu-id="df4a1-184">Avoir un chiffre</span><span class="sxs-lookup"><span data-stu-id="df4a1-184">Have a digit</span></span>
* <span data-ttu-id="df4a1-185">Avoir un caractère spécial (correspondances Regex [\W_])</span><span class="sxs-lookup"><span data-stu-id="df4a1-185">Have a special character (Regex match [\W_])</span></span>

<span data-ttu-id="df4a1-186">Hello après les mots de passe n’est pas autorisé :</span><span class="sxs-lookup"><span data-stu-id="df4a1-186">hello following passwords are not allowed:</span></span>

<table>
    <tr>
        <td style="text-align:center">abc@123</td>
        <td style="text-align:center"><span data-ttu-id="df4a1-187">P@$$w0rd</span><span class="sxs-lookup"><span data-stu-id="df4a1-187">P@$$w0rd</span></span></td>
        <td style="text-align:center">P@ssw0rd</td>
        <td style="text-align:center">P@ssword123</td>
        <td style="text-align:center"><span data-ttu-id="df4a1-188">Pa$$word</span><span class="sxs-lookup"><span data-stu-id="df4a1-188">Pa$$word</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center">pass@word1</td>
        <td style="text-align:center"><span data-ttu-id="df4a1-189">Password!</span><span class="sxs-lookup"><span data-stu-id="df4a1-189">Password!</span></span></td>
        <td style="text-align:center"><span data-ttu-id="df4a1-190">Password1</span><span class="sxs-lookup"><span data-stu-id="df4a1-190">Password1</span></span></td>
        <td style="text-align:center"><span data-ttu-id="df4a1-191">Password22</span><span class="sxs-lookup"><span data-stu-id="df4a1-191">Password22</span></span></td>
        <td style="text-align:center"><span data-ttu-id="df4a1-192">iloveyou!</span><span class="sxs-lookup"><span data-stu-id="df4a1-192">iloveyou!</span></span></td>
    </tr>
</table>
