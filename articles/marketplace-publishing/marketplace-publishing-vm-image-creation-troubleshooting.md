---
title: "Comment résoudre les problèmes courants lors de la création du disque dur virtuel | Microsoft Docs"
description: "Réponses aux questions courantes de dépannage et aux problèmes rencontrés lors de la création du disque dur virtuel."
services: Azure Marketplace
documentationcenter: 
author: HannibalSII
manager: 
editor: 
ms.assetid: e39563d8-8646-4cb7-b078-8b10ac35b494
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 09/26/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: c4e88a9fbb15dd90d619b159ae1065dfacc1907f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-troubleshoot-common-issues-encountered-during-vhd-creation"></a><span data-ttu-id="bcb2b-103">Comment résoudre les problèmes courants rencontrés lors de la création du disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="bcb2b-103">How to troubleshoot common issues encountered during VHD creation</span></span>
<span data-ttu-id="bcb2b-104">Cet article aide les éditeurs et/ou coadministrateurs Azure Marketplace qui peuvent rencontrer un problème ou avoir des questions courantes lors de la publication ou de la gestion de leurs solutions de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="bcb2b-104">This article is provided to help an Azure Marketplace publisher and/or co-administrator that may experience an issue or have common questions while publishing or managing their virtual machine solution(s).</span></span>

1. <span data-ttu-id="bcb2b-105">Comment modifier le nom de l’hôte ?</span><span class="sxs-lookup"><span data-stu-id="bcb2b-105">How do I change the name of the host?</span></span>
   
    <span data-ttu-id="bcb2b-106">Une fois que la machine virtuelle est créée, il est impossible pour les utilisateurs de mettre à jour le nom de l’hôte.</span><span class="sxs-lookup"><span data-stu-id="bcb2b-106">Once VM is created, users can’t update the name of the host.</span></span>
2. <span data-ttu-id="bcb2b-107">Comment réinitialiser le service Bureau à distance ou son mot de passe de connexion ?</span><span class="sxs-lookup"><span data-stu-id="bcb2b-107">How to reset the Remote Desktop service or its login password?</span></span>
   
   * [<span data-ttu-id="bcb2b-108">Référence pour les machines virtuelles Windows</span><span class="sxs-lookup"><span data-stu-id="bcb2b-108">Reference for Windows VM</span></span>](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-reset-rdp/)
   * [<span data-ttu-id="bcb2b-109">Référence pour les machines virtuelles Linux</span><span class="sxs-lookup"><span data-stu-id="bcb2b-109">Reference for Linux VM</span></span>](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/)
3. <span data-ttu-id="bcb2b-110">Comment générer de nouveaux certificats ssh ?</span><span class="sxs-lookup"><span data-stu-id="bcb2b-110">How to generate new ssh certificates?</span></span>
   
   <span data-ttu-id="bcb2b-111">Reportez-vous au lien : [https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/)</span><span class="sxs-lookup"><span data-stu-id="bcb2b-111">Please refer to the link: [https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/)</span></span>
4. <span data-ttu-id="bcb2b-112">Comment configurer un certificat VPN ouvert ?</span><span class="sxs-lookup"><span data-stu-id="bcb2b-112">How to configure an open VPN certificate?</span></span>
   
   <span data-ttu-id="bcb2b-113">Reportez-vous au lien : [https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/](https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/)</span><span class="sxs-lookup"><span data-stu-id="bcb2b-113">Please refer to the link: [https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/](https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/)</span></span>
5. <span data-ttu-id="bcb2b-114">Quelle est la stratégie de prise en charge pour l’exécution de logiciels serveur Microsoft dans un environnement de machine virtuelle Microsoft Azure (infrastructure en tant que service) ?</span><span class="sxs-lookup"><span data-stu-id="bcb2b-114">What is the support policy for running Microsoft server software in the Microsoft Azure virtual machine environment (infrastructure-as-a-service)?</span></span>
   
   <span data-ttu-id="bcb2b-115">Reportez-vous au lien : [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)</span><span class="sxs-lookup"><span data-stu-id="bcb2b-115">Please refer to the link: [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)</span></span>
6. <span data-ttu-id="bcb2b-116">Les machines virtuelles ont-elles un identificateur unique ?</span><span class="sxs-lookup"><span data-stu-id="bcb2b-116">Do Virtual Machines have any unique identifier?</span></span>
   
   <span data-ttu-id="bcb2b-117">Azure encode l’ID unique de machine virtuelle Azure dans chaque machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="bcb2b-117">Azure encodes Azure VM Unique ID in every VM.</span></span> <span data-ttu-id="bcb2b-118">Pour plus d’informations, consultez le blog et la documentation.</span><span class="sxs-lookup"><span data-stu-id="bcb2b-118">See details in this blog and documentation.</span></span>
7. <span data-ttu-id="bcb2b-119">Dans une machine virtuelle, comment puis-je gérer l’extension de script personnalisé lors de la tâche de démarrage ?</span><span class="sxs-lookup"><span data-stu-id="bcb2b-119">In a VM how can I manage the custom script extension in the startup task?</span></span>
   
   <span data-ttu-id="bcb2b-120">Reportez-vous au lien : [https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/)</span><span class="sxs-lookup"><span data-stu-id="bcb2b-120">Please refer to the link: [https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/)</span></span>
8. <span data-ttu-id="bcb2b-121">Comment créer une machine virtuelle à partir du portail Azure à l’aide du disque dur virtuel qui est téléchargé vers le stockage Premium ?</span><span class="sxs-lookup"><span data-stu-id="bcb2b-121">How to create a VM from the Azure portal using the VHD that is uploaded to premium storage?</span></span>
   
   <span data-ttu-id="bcb2b-122">Nous ne prenons pas encore en charge cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="bcb2b-122">We do not support this feature yet.</span></span>
9. <span data-ttu-id="bcb2b-123">Les applications 32 bits sont-elles prises en charge dans Azure Marketplace ?</span><span class="sxs-lookup"><span data-stu-id="bcb2b-123">Is a 32-bit app supported in the Azure Marketplace?</span></span>
   
   <span data-ttu-id="bcb2b-124">Reportez-vous au lien suivant pour plus d’informations sur la stratégie de prise en charge : [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)</span><span class="sxs-lookup"><span data-stu-id="bcb2b-124">Please refer to the link for details on the support policy: [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)</span></span>
10. <span data-ttu-id="bcb2b-125">Chaque fois que j’essaie de créer une image à partir de mes disques durs virtuels, j’obtiens l’erreur « .VHD is already registered with image repository as the resource » (Le disque dur virtuel est déjà enregistré avec le référentiel d’image en tant que ressource) dans PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bcb2b-125">Every time I am trying to create an image from my VHDs, I get the error “.VHD is already registered with image repository as the resource” in PowerShell.</span></span> <span data-ttu-id="bcb2b-126">Je n’ai pas créé d’image au préalable et je n’ai trouvé aucune image portant ce nom dans Azure.</span><span class="sxs-lookup"><span data-stu-id="bcb2b-126">I did not create any image before nor did I find any image with this name in Azure.</span></span> <span data-ttu-id="bcb2b-127">Comment résoudre ce problème ?</span><span class="sxs-lookup"><span data-stu-id="bcb2b-127">How do I resolve this?</span></span>
    
    <span data-ttu-id="bcb2b-128">Cela se produit généralement si l’utilisateur a provisionné une machine virtuelle à partir de ce disque dur virtuel et si le disque dur virtuel est verrouillé.</span><span class="sxs-lookup"><span data-stu-id="bcb2b-128">This usually happen if the user provisioned a VM from this VHD and there is a lock on that VHD.</span></span> <span data-ttu-id="bcb2b-129">Vérifiez qu’aucune machine virtuelle n’est allouée à partir de ce disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="bcb2b-129">Please check that there is no VM allocated from this VHD.</span></span> <span data-ttu-id="bcb2b-130">Si l’erreur persiste, ouvrez un ticket de support à l’aide de ce lien ou du portail de publication (toutes les informations sont fournies dans la réponse à la question 11).</span><span class="sxs-lookup"><span data-stu-id="bcb2b-130">If the error still persist , then please raise a support ticket using this link or from the Publishing portal regarding this (details are given in the answer of question 11).</span></span>