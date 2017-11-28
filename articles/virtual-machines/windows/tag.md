---
title: "aaaHow tootag une ressource d’ordinateur virtuel Windows dans Azure | Documents Microsoft"
description: "En savoir plus sur le marquage d’une machine virtuelle de Windows créée dans Azure à l’aide du modèle de déploiement du Gestionnaire de ressources hello"
services: virtual-machines-windows
documentationcenter: 
author: mmccrory
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 56d17f45-e4a7-4d84-8022-b40334ae49d2
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2016
ms.author: memccror
ms.openlocfilehash: 160416ddc35998b3c98c6e579668a6a5eb6de6e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootag-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="1d227-103">Comment tootag une machine virtuelle de Windows dans Azure</span><span class="sxs-lookup"><span data-stu-id="1d227-103">How tootag a Windows virtual machine in Azure</span></span>
<span data-ttu-id="1d227-104">Cet article décrit les différentes façons tootag une machine virtuelle de Windows dans Azure via le modèle de déploiement du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="1d227-104">This article describes different ways tootag a Windows virtual machine in Azure through hello Resource Manager deployment model.</span></span> <span data-ttu-id="1d227-105">Les balises sont des paires clé/valeur définies par l’utilisateur, qui peuvent être placées directement sur une ressource ou sur un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="1d227-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span></span> <span data-ttu-id="1d227-106">Azure prend actuellement en charge des balises de too15 par la ressource et le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="1d227-106">Azure currently supports up too15 tags per resource and resource group.</span></span> <span data-ttu-id="1d227-107">Balises peuvent être placées sur une ressource au moment de la création de hello ou ajouté tooan les ressources existantes.</span><span class="sxs-lookup"><span data-stu-id="1d227-107">Tags may be placed on a resource at hello time of creation or added tooan existing resource.</span></span> <span data-ttu-id="1d227-108">Notez que les balises sont prises en charge pour les ressources créées via le modèle de déploiement Resource Manager hello uniquement.</span><span class="sxs-lookup"><span data-stu-id="1d227-108">Please note that tags are supported for resources created via hello Resource Manager deployment model only.</span></span> <span data-ttu-id="1d227-109">Si vous souhaitez tootag une machine virtuelle Linux, consultez [comment tootag une machine virtuelle de Linux dans Azure](../linux/tag.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1d227-109">If you want tootag a Linux virtual machine, see [How tootag a Linux virtual machine in Azure](../linux/tag.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-powershell"></a><span data-ttu-id="1d227-110">Balisage avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="1d227-110">Tagging with PowerShell</span></span>
<span data-ttu-id="1d227-111">toocreate, ajouter et supprimer des balises via PowerShell, vous devez tout d’abord tooset de votre [l’environnement PowerShell avec Azure Resource Manager][PowerShell environment with Azure Resource Manager].</span><span class="sxs-lookup"><span data-stu-id="1d227-111">toocreate, add, and delete tags through PowerShell, you first need tooset up your [PowerShell environment with Azure Resource Manager][PowerShell environment with Azure Resource Manager].</span></span> <span data-ttu-id="1d227-112">Une fois que vous avez terminé le programme d’installation hello, vous pouvez placer des étiquettes sur les ressources de calcul, réseau et de stockage lors de la création ou après la création de ressources de hello via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1d227-112">Once you have completed hello setup, you can place tags on Compute, Network, and Storage resources at creation or after hello resource is created via PowerShell.</span></span> <span data-ttu-id="1d227-113">Cet article se concentre sur l’affichage et la modification des balises placées sur des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="1d227-113">This article will concentrate on viewing/editing tags placed on Virtual Machines.</span></span>

<span data-ttu-id="1d227-114">Accédez d’abord, tooa Machine virtuelle via hello `Get-AzureRmVM` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="1d227-114">First, navigate tooa Virtual Machine through hello `Get-AzureRmVM` cmdlet.</span></span>

        PS C:\> Get-AzureRmVM -ResourceGroupName "MyResourceGroup" -Name "MyTestVM"

<span data-ttu-id="1d227-115">Si votre Machine virtuelle contient déjà des balises, vous verrez ensuite toutes les balises hello sur votre ressource :</span><span class="sxs-lookup"><span data-stu-id="1d227-115">If your Virtual Machine already contains tags, you will then see all hello tags on your resource:</span></span>

        Tags : {
                "Application": "MyApp1",
                "Created By": "MyName",
                "Department": "MyDepartment",
                "Environment": "Production"
               }

<span data-ttu-id="1d227-116">Si vous souhaitez que les balises tooadd via PowerShell, vous pouvez utiliser hello `Set-AzureRmResource` commande.</span><span class="sxs-lookup"><span data-stu-id="1d227-116">If you would like tooadd tags through PowerShell, you can use hello `Set-AzureRmResource` command.</span></span> <span data-ttu-id="1d227-117">Notez que lors de la mise à jour des balises via PowerShell, les balises sont mises à jour comme un tout.</span><span class="sxs-lookup"><span data-stu-id="1d227-117">Note when updating tags through PowerShell, tags are updated as a whole.</span></span> <span data-ttu-id="1d227-118">Par conséquent, si vous ajoutez une ressource de tooa de balise qui comporte déjà des balises, vous devez tooinclude toutes les balises hello toobe placé sur la ressource de hello souhaitées.</span><span class="sxs-lookup"><span data-stu-id="1d227-118">So if you are adding one tag tooa resource that already has tags, you will need tooinclude all hello tags that you want toobe placed on hello resource.</span></span> <span data-ttu-id="1d227-119">Voici un exemple de comment tooadd supplémentaire les balises tooa des ressources via les PowerShell Cmdlets.</span><span class="sxs-lookup"><span data-stu-id="1d227-119">Below is an example of how tooadd additional tags tooa resource through PowerShell Cmdlets.</span></span>

<span data-ttu-id="1d227-120">Cette applet de commande premier définit toutes les balises hello placés sur *MyTestVM* toohello *$tags* variable, à l’aide de hello `Get-AzureRmResource` et `Tags` propriété.</span><span class="sxs-lookup"><span data-stu-id="1d227-120">This first cmdlet sets all of hello tags placed on *MyTestVM* toohello *$tags* variable, using hello `Get-AzureRmResource` and `Tags` property.</span></span>

        PS C:\> $tags = (Get-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM).Tags

<span data-ttu-id="1d227-121">Hello deuxième commande affiche des balises hello pour hello donné variable.</span><span class="sxs-lookup"><span data-stu-id="1d227-121">hello second command displays hello tags for hello given variable.</span></span>

        PS C:\> $tags

        Name        Value
        ----                           -----
        Value        MyDepartment
        Name        Department
        Value        MyApp1
        Name        Application
        Value        MyName
        Name        Created By
        Value        Production
        Name        Environment

<span data-ttu-id="1d227-122">Hello troisième commande ajoute une balise supplémentaires de toohello *$tags* variable.</span><span class="sxs-lookup"><span data-stu-id="1d227-122">hello third command adds an additional tag toohello *$tags* variable.</span></span> <span data-ttu-id="1d227-123">Notez que hello hello  **+=**  tooappend hello nouvelle toohello de paire clé/valeur *$tags* liste.</span><span class="sxs-lookup"><span data-stu-id="1d227-123">Note hello use of hello **+=** tooappend hello new key/value pair toohello *$tags* list.</span></span>

        PS C:\> $tags += @{Name="Location";Value="MyLocation"}

<span data-ttu-id="1d227-124">commande quatrième Hello définit toutes les balises hello définis dans hello *$tags* toohello variable donné de ressources.</span><span class="sxs-lookup"><span data-stu-id="1d227-124">hello fourth command sets all of hello tags defined in hello *$tags* variable toohello given resource.</span></span> <span data-ttu-id="1d227-125">Dans ce cas, il s’agit de MyTestVM.</span><span class="sxs-lookup"><span data-stu-id="1d227-125">In this case, it is MyTestVM.</span></span>

        PS C:\> Set-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM -ResourceType "Microsoft.Compute/VirtualMachines" -Tag $tags

<span data-ttu-id="1d227-126">commande cinquième Hello affiche toutes les balises hello sur la ressource de hello.</span><span class="sxs-lookup"><span data-stu-id="1d227-126">hello fifth command displays all of hello tags on hello resource.</span></span> <span data-ttu-id="1d227-127">Comme vous pouvez le voir, *emplacement* est maintenant définie en tant que balise *MyLocation* en tant que valeur de hello.</span><span class="sxs-lookup"><span data-stu-id="1d227-127">As you can see, *Location* is now defined as a tag with *MyLocation* as hello value.</span></span>

        PS C:\> (Get-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM).Tags

        Name        Value
        ----                           -----
        Value        MyDepartment
        Name        Department
        Value        MyApp1
        Name        Application
        Value        MyName
        Name        Created By
        Value        Production
        Name        Environment
        Value        MyLocation
        Name        Location

<span data-ttu-id="1d227-128">toolearn en savoir plus sur le balisage via PowerShell, consultez hello [applets de commande Resource Azure][Azure Resource Cmdlets].</span><span class="sxs-lookup"><span data-stu-id="1d227-128">toolearn more about tagging through PowerShell, check out hello [Azure Resource Cmdlets][Azure Resource Cmdlets].</span></span>

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a><span data-ttu-id="1d227-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1d227-129">Next steps</span></span>
* <span data-ttu-id="1d227-130">toolearn en savoir plus sur le marquage de vos ressources Azure, consultez [vue d’ensemble du Gestionnaire de ressources Azure] [ Azure Resource Manager Overview] et [à l’aide de balises tooorganize vos ressources Azure] [ Using Tags tooorganize your Azure Resources].</span><span class="sxs-lookup"><span data-stu-id="1d227-130">toolearn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags tooorganize your Azure Resources][Using Tags tooorganize your Azure Resources].</span></span>
* <span data-ttu-id="1d227-131">toosee balises peuvent vous aider à gérer votre utilisation des ressources Azure, voir [comprendre votre facture Azure] [ Understanding your Azure Bill] et [obtenir votre consommation de ressources Microsoft Azure] [Gain insights into your Microsoft Azure resource consumption].</span><span class="sxs-lookup"><span data-stu-id="1d227-131">toosee how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span></span>

[PowerShell environment with Azure Resource Manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
[Azure Resource Cmdlets]: https://msdn.microsoft.com/library/azure/dn757692.aspx
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags tooorganize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
