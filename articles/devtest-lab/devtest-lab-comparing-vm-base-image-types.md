---
title: "aaaComparing des images personnalisées et les formules de DevTest Labs | Documents Microsoft"
description: "En savoir plus sur les différences de hello entre des images personnalisées et les formules comme base la machine virtuelle afin de décider laquelle correspond le mieux à votre environnement."
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
ms.openlocfilehash: 3c1d88dfe0ff94b8e825bb7a0b4aca3341c9330d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="comparing-custom-images-and-formulas-in-devtest-labs"></a><span data-ttu-id="98d47-103">Comparaison entre les images personnalisées et les formules dans DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="98d47-103">Comparing custom images and formulas in DevTest Labs</span></span>
<span data-ttu-id="98d47-104">Les [images personnalisées](devtest-lab-create-template.md) et les [formules](devtest-lab-manage-formulas.md) peuvent toutes deux être utilisées comme bases pour [créer des machines virtuelles](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="98d47-104">Both [custom images](devtest-lab-create-template.md) and [formulas](devtest-lab-manage-formulas.md) can be used as bases for [created new VMs](devtest-lab-add-vm-with-artifacts.md).</span></span> <span data-ttu-id="98d47-105">Toutefois, hello différence majeure entre des images personnalisées et les formules est qu’une image personnalisée est simplement une image basée sur un disque dur virtuel, tandis que la formule est une image basée sur un disque dur virtuel *à* préconfiguré paramètres - telles que la taille de machine virtuelle, un réseau virtuel, sous-réseau et les artefacts.</span><span class="sxs-lookup"><span data-stu-id="98d47-105">However, hello key distinction between custom images and formulas is that a custom image is simply an image based on a VHD, while a formula is an image based on a VHD *in addition to* preconfigured settings - such as VM Size, virtual network, subnet, and artifacts.</span></span> <span data-ttu-id="98d47-106">Ces paramètres préconfigurés sont configurés avec les valeurs par défaut qui peuvent être remplacées au moment de hello de création d’ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="98d47-106">These preconfigured settings are set up with default values that can be overridden at hello time of VM creation.</span></span> <span data-ttu-id="98d47-107">Cet article décrit certains des avantages de hello (pros) et inconvénients (cons) toousing des images et à l’aide de formules personnalisées.</span><span class="sxs-lookup"><span data-stu-id="98d47-107">This article explains some of hello advantages (pros) and disadvantages (cons) toousing custom images versus using formulas.</span></span>

## <a name="custom-image-pros-and-cons"></a><span data-ttu-id="98d47-108">Avantages et inconvénients des images personnalisées</span><span class="sxs-lookup"><span data-stu-id="98d47-108">Custom image pros and cons</span></span>
<span data-ttu-id="98d47-109">Images personnalisées fournissent un toocreate de façon statique, immuable machines virtuelles à partir d’un environnement de votre choix.</span><span class="sxs-lookup"><span data-stu-id="98d47-109">Custom images provide a static, immutable way toocreate VMs from a desired environment.</span></span> 

<span data-ttu-id="98d47-110">**Avantages**</span><span class="sxs-lookup"><span data-stu-id="98d47-110">**Pros**</span></span>

* <span data-ttu-id="98d47-111">Machine virtuelle à partir d’une image personnalisée de configuration est rapide que rien ne change après hello que machine virtuelle est lancé à partir de l’image de hello.</span><span class="sxs-lookup"><span data-stu-id="98d47-111">VM provisioning from a custom image is fast as nothing changes after hello VM is spun up from hello image.</span></span> <span data-ttu-id="98d47-112">En d’autres termes, il n’existe aucune tooapply paramètres comme image personnalisée de hello est simplement une image sans paramètres.</span><span class="sxs-lookup"><span data-stu-id="98d47-112">In other words, there are no settings tooapply as hello custom image is just an image without settings.</span></span> 
* <span data-ttu-id="98d47-113">Les machines virtuelles créées à partir d’une même image personnalisée sont identiques.</span><span class="sxs-lookup"><span data-stu-id="98d47-113">VMs created from a single custom image are identical.</span></span>

<span data-ttu-id="98d47-114">**Inconvénients**</span><span class="sxs-lookup"><span data-stu-id="98d47-114">**Cons**</span></span>

* <span data-ttu-id="98d47-115">Si vous devez tooupdate certains aspects de l’image personnalisée de hello, image de hello doit être recréé.</span><span class="sxs-lookup"><span data-stu-id="98d47-115">If you need tooupdate some aspect of hello custom image, hello image must be recreated.</span></span>  

## <a name="formula-pros-and-cons"></a><span data-ttu-id="98d47-116">Avantages et inconvénients des formules</span><span class="sxs-lookup"><span data-stu-id="98d47-116">Formula pros and cons</span></span>
<span data-ttu-id="98d47-117">Les formules fournissent des machines virtuelles un toocreate de façon dynamique à partir des paramètres de la configuration souhaitée de hello.</span><span class="sxs-lookup"><span data-stu-id="98d47-117">Formulas provide a dynamic way toocreate VMs from hello desired configuration/settings.</span></span>

<span data-ttu-id="98d47-118">**Avantages**</span><span class="sxs-lookup"><span data-stu-id="98d47-118">**Pros**</span></span>

* <span data-ttu-id="98d47-119">Modifications dans l’environnement de hello peuvent être capturées à volée hello via les artefacts.</span><span class="sxs-lookup"><span data-stu-id="98d47-119">Changes in hello environment can be captured on hello fly via artifacts.</span></span> <span data-ttu-id="98d47-120">Par exemple, si vous souhaitez une machine virtuelle installée avec les éléments les plus récents à partir de votre version de pipeline hello ou inscrivez le dernier code de hello à partir de votre référentiel, vous pouvez spécifier simplement un artefact qui déploie les éléments les plus récents hello ou inscrit le dernier code de hello dans la formule hello avec un image de base cible.</span><span class="sxs-lookup"><span data-stu-id="98d47-120">For example, if you want a VM installed with hello latest bits from your release pipeline or enlist hello latest code from your repository, you can simply specify an artifact that deploys hello latest bits or enlists hello latest code in hello formula together with a target base image.</span></span> <span data-ttu-id="98d47-121">Chaque fois que cette formule est utilisée toocreate VMs, hello derniers bits/code sont déployés/inscrite toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="98d47-121">Whenever this formula is used toocreate VMs, hello latest bits/code are deployed/enlisted toohello VM.</span></span> 
* <span data-ttu-id="98d47-122">Les formules, à la différence des images personnalisées, peuvent définir des paramètres par défaut, par exemple la taille des machines virtuelles et les paramètres de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="98d47-122">Formulas can define default settings that custom images cannot provide - such as VM sizes and virtual network settings.</span></span> 
* <span data-ttu-id="98d47-123">paramètres de Hello enregistrés dans une formule sont affichés sous forme de valeurs par défaut, mais peuvent être modifiées lors de la création de hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="98d47-123">hello settings saved in a formula are shown as default values, but can be modified when hello VM is created.</span></span> 

<span data-ttu-id="98d47-124">**Inconvénients**</span><span class="sxs-lookup"><span data-stu-id="98d47-124">**Cons**</span></span>

* <span data-ttu-id="98d47-125">La création d’une machine virtuelle à partir d’une formule peut prendre plus de temps qu’à partir d’une image personnalisée.</span><span class="sxs-lookup"><span data-stu-id="98d47-125">Creating a VM from a formula can take more time than creating a VM from a custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="98d47-126">Billets de blog connexes</span><span class="sxs-lookup"><span data-stu-id="98d47-126">Related blog posts</span></span>
* [<span data-ttu-id="98d47-127">Images personnalisées ou formules ?</span><span class="sxs-lookup"><span data-stu-id="98d47-127">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a><span data-ttu-id="98d47-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="98d47-128">Next steps</span></span>
- [<span data-ttu-id="98d47-129">FAQ DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="98d47-129">DevTest Labs FAQ</span></span>](devtest-lab-faq.md)