---
title: "Comparaison entre les images personnalisées et les formules dans DevTest Labs | Microsoft Docs"
description: "Découvrez les différences entre les images personnalisées et les formules comme bases de machine virtuelle afin de déterminer laquelle correspond le mieux à votre environnement."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: a3cb259a-7d80-40ec-8ee8-45105704d589
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: tarcher
ms.openlocfilehash: ff771abc26c08f0adb977c29739d2f5c91924b21
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="comparing-custom-images-and-formulas-in-devtest-labs"></a><span data-ttu-id="859ec-103">Comparaison entre les images personnalisées et les formules dans DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="859ec-103">Comparing custom images and formulas in DevTest Labs</span></span>
<span data-ttu-id="859ec-104">Les [images personnalisées](devtest-lab-create-template.md) et les [formules](devtest-lab-manage-formulas.md) peuvent toutes deux être utilisées comme bases pour [créer des machines virtuelles](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="859ec-104">Both [custom images](devtest-lab-create-template.md) and [formulas](devtest-lab-manage-formulas.md) can be used as bases for [created new VMs](devtest-lab-add-vm-with-artifacts.md).</span></span> <span data-ttu-id="859ec-105">Cependant, la différence principale entre les images personnalisées et les formules est qu’une image personnalisée est simplement une image basée sur un disque dur virtuel, alors qu’une formule correspond à une image basée sur un disque dur virtuel *en plus* de paramètres préconfigurés, comme la taille de la machine virtuelle, le réseau virtuel, le sous-réseau et les artefacts.</span><span class="sxs-lookup"><span data-stu-id="859ec-105">However, the key distinction between custom images and formulas is that a custom image is simply an image based on a VHD, while a formula is an image based on a VHD *in addition to* preconfigured settings - such as VM Size, virtual network, subnet, and artifacts.</span></span> <span data-ttu-id="859ec-106">Ces paramètres préconfigurés sont définis avec les valeurs par défaut. Celles-ci peuvent être remplacées au moment de la création de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="859ec-106">These preconfigured settings are set up with default values that can be overridden at the time of VM creation.</span></span> <span data-ttu-id="859ec-107">Cet article explique quelques-uns des avantages et des inconvénients de l’utilisation des images personnalisées et des formules.</span><span class="sxs-lookup"><span data-stu-id="859ec-107">This article explains some of the advantages (pros) and disadvantages (cons) to using custom images versus using formulas.</span></span>

## <a name="custom-image-pros-and-cons"></a><span data-ttu-id="859ec-108">Avantages et inconvénients des images personnalisées</span><span class="sxs-lookup"><span data-stu-id="859ec-108">Custom image pros and cons</span></span>
<span data-ttu-id="859ec-109">Les images personnalisées représentent un moyen statique et immuable de créer des machines virtuelles dans un environnement de votre choix.</span><span class="sxs-lookup"><span data-stu-id="859ec-109">Custom images provide a static, immutable way to create VMs from a desired environment.</span></span> 

<span data-ttu-id="859ec-110">**Avantages**</span><span class="sxs-lookup"><span data-stu-id="859ec-110">**Pros**</span></span>

* <span data-ttu-id="859ec-111">L’approvisionnement de machines virtuelles à partir d’une image personnalisée est rapide car rien ne change une fois que la machine virtuelle est lancée à partir de l’image.</span><span class="sxs-lookup"><span data-stu-id="859ec-111">VM provisioning from a custom image is fast as nothing changes after the VM is spun up from the image.</span></span> <span data-ttu-id="859ec-112">En d’autres termes, il n’existe aucun paramètre à appliquer, car l’image personnalisée est simplement une image sans paramètres.</span><span class="sxs-lookup"><span data-stu-id="859ec-112">In other words, there are no settings to apply as the custom image is just an image without settings.</span></span> 
* <span data-ttu-id="859ec-113">Les machines virtuelles créées à partir d’une même image personnalisée sont identiques.</span><span class="sxs-lookup"><span data-stu-id="859ec-113">VMs created from a single custom image are identical.</span></span>

<span data-ttu-id="859ec-114">**Inconvénients**</span><span class="sxs-lookup"><span data-stu-id="859ec-114">**Cons**</span></span>

* <span data-ttu-id="859ec-115">Si vous avez besoin de mettre à jour certains aspects de l’image personnalisée, l’image doit être recréée.</span><span class="sxs-lookup"><span data-stu-id="859ec-115">If you need to update some aspect of the custom image, the image must be recreated.</span></span>  

## <a name="formula-pros-and-cons"></a><span data-ttu-id="859ec-116">Avantages et inconvénients des formules</span><span class="sxs-lookup"><span data-stu-id="859ec-116">Formula pros and cons</span></span>
<span data-ttu-id="859ec-117">Les formules représentent un moyen dynamique de créer des machines virtuelles à partir de la configuration/des paramètres souhaités.</span><span class="sxs-lookup"><span data-stu-id="859ec-117">Formulas provide a dynamic way to create VMs from the desired configuration/settings.</span></span>

<span data-ttu-id="859ec-118">**Avantages**</span><span class="sxs-lookup"><span data-stu-id="859ec-118">**Pros**</span></span>

* <span data-ttu-id="859ec-119">Les modifications de l'environnement peuvent être capturées à la volée au moyen d’artefacts.</span><span class="sxs-lookup"><span data-stu-id="859ec-119">Changes in the environment can be captured on the fly via artifacts.</span></span> <span data-ttu-id="859ec-120">Par exemple, si vous voulez installer une machine virtuelle avec les derniers éléments de votre pipeline de mise en production ou inscrire les lignes de code les plus récentes de votre dépôt, vous pouvez simplement spécifier un artefact qui déploie les derniers éléments ou inscrit les lignes de code les plus récentes dans la formule avec l’image de base cible.</span><span class="sxs-lookup"><span data-stu-id="859ec-120">For example, if you want a VM installed with the latest bits from your release pipeline or enlist the latest code from your repository, you can simply specify an artifact that deploys the latest bits or enlists the latest code in the formula together with a target base image.</span></span> <span data-ttu-id="859ec-121">Chaque fois que cette formule sera utilisée pour créer des machines virtuelles, les derniers éléments/lignes de code seront déployés/inscrites sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="859ec-121">Whenever this formula is used to create VMs, the latest bits/code are deployed/enlisted to the VM.</span></span> 
* <span data-ttu-id="859ec-122">Les formules, à la différence des images personnalisées, peuvent définir des paramètres par défaut, par exemple la taille des machines virtuelles et les paramètres de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="859ec-122">Formulas can define default settings that custom images cannot provide - such as VM sizes and virtual network settings.</span></span> 
* <span data-ttu-id="859ec-123">Les paramètres enregistrés dans une formule apparaissent comme valeurs par défaut, mais peuvent être modifiés à la création de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="859ec-123">The settings saved in a formula are shown as default values, but can be modified when the VM is created.</span></span> 

<span data-ttu-id="859ec-124">**Inconvénients**</span><span class="sxs-lookup"><span data-stu-id="859ec-124">**Cons**</span></span>

* <span data-ttu-id="859ec-125">La création d’une machine virtuelle à partir d’une formule peut prendre plus de temps qu’à partir d’une image personnalisée.</span><span class="sxs-lookup"><span data-stu-id="859ec-125">Creating a VM from a formula can take more time than creating a VM from a custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="859ec-126">Billets de blog connexes</span><span class="sxs-lookup"><span data-stu-id="859ec-126">Related blog posts</span></span>
* [<span data-ttu-id="859ec-127">Images personnalisées ou formules ?</span><span class="sxs-lookup"><span data-stu-id="859ec-127">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a><span data-ttu-id="859ec-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="859ec-128">Next steps</span></span>
- [<span data-ttu-id="859ec-129">FAQ DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="859ec-129">DevTest Labs FAQ</span></span>](devtest-lab-faq.md)