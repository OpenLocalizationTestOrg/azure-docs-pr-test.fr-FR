---
title: aaaBoot des diagnostics pour les ordinateurs virtuels Linux dans Azure | Documentation de Microsoft
description: "Vue d’ensemble des fonctionnalités de débogage deux hello pour les ordinateurs virtuels Linux dans Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: Deland-Han
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: delhan
ms.openlocfilehash: d355d512de09d2f1d7a2718e3db3fb99c9dd9e24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-boot-diagnostics-tootroubleshoot-linux-virtual-machines-in-azure"></a><span data-ttu-id="7ac5e-103">Comment toouse démarrer les ordinateurs virtuels Linux diagnostics tootroubleshoot dans Azure</span><span class="sxs-lookup"><span data-stu-id="7ac5e-103">How toouse boot diagnostics tootroubleshoot Linux virtual machines in Azure</span></span>

<span data-ttu-id="7ac5e-104">La prise en charge de deux fonctionnalités de débogage est désormais disponible dans Azure : les supports de Console Output et Screenshot pour le modèle de déploiement Azure Virtual Machines Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7ac5e-104">Support for two debugging features is now available in Azure: Console Output and Screenshot support for Azure Virtual Machines Resource Manager deployment model.</span></span> 

<span data-ttu-id="7ac5e-105">Lors de la prochaine tooAzure de votre propre image ou même initialisation d’une des images de plateforme hello, il peut y avoir plusieurs raisons pour lesquelles un ordinateur virtuel Obtient dans un état non démarrable.</span><span class="sxs-lookup"><span data-stu-id="7ac5e-105">When bringing your own image tooAzure or even booting one of hello platform images, there can be many reasons why a Virtual Machine gets into a non-bootable state.</span></span> <span data-ttu-id="7ac5e-106">Activation de ces fonctionnalités vous tooeasily diagnostiquer et récupérer vos Machines virtuelles des échecs de démarrage.</span><span class="sxs-lookup"><span data-stu-id="7ac5e-106">These features enable you tooeasily diagnose and recover your Virtual Machines from boot failures.</span></span>

<span data-ttu-id="7ac5e-107">Pour les Machines virtuelles Linux, vous pouvez facilement afficher sortie hello de votre journal de console à partir de hello portail :</span><span class="sxs-lookup"><span data-stu-id="7ac5e-107">For Linux Virtual Machines, you can easily view hello output of your console log from hello Portal:</span></span>

![Portail Azure](./media/boot-diagnostics/screenshot1.png)
 
<span data-ttu-id="7ac5e-109">Toutefois, pour Windows et les ordinateurs virtuels Linux, Azure permet également de toosee une capture d’écran de hello machine virtuelle à partir de l’hyperviseur de hello :</span><span class="sxs-lookup"><span data-stu-id="7ac5e-109">However, for both Windows and Linux Virtual Machines, Azure also enables you toosee a screenshot of hello VM from hello hypervisor:</span></span>

![Error](./media/boot-diagnostics/screenshot2.png)

<span data-ttu-id="7ac5e-111">Ces deux fonctionnalités sont prises en charge par les Machines Virtuelles Azure dans toutes les régions.</span><span class="sxs-lookup"><span data-stu-id="7ac5e-111">Both of these features are supported for Azure Virtual Machines in all regions.</span></span> <span data-ttu-id="7ac5e-112">Tooappear de minutes too10 dans votre compte de stockage peuvent prendre note des captures d’écran et la sortie.</span><span class="sxs-lookup"><span data-stu-id="7ac5e-112">Note, screenshots, and output can take up too10 minutes tooappear in your storage account.</span></span>

## <a name="common-boot-errors"></a><span data-ttu-id="7ac5e-113">Erreurs de démarrage courantes</span><span class="sxs-lookup"><span data-stu-id="7ac5e-113">Common boot errors</span></span>

- [<span data-ttu-id="7ac5e-114">Problèmes de système de fichiers</span><span class="sxs-lookup"><span data-stu-id="7ac5e-114">File system issues</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/09/13/linux-recovery-cannot-ssh-to-linux-vm-due-to-file-system-errors-fsck-inodes/)
- [<span data-ttu-id="7ac5e-115">Problèmes de noyau</span><span class="sxs-lookup"><span data-stu-id="7ac5e-115">Kernel Issues</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/10/09/linux-recovery-manually-fixing-non-boot-issues-related-to-kernel-problems/)
- [<span data-ttu-id="7ac5e-116">Erreurs FSTAB</span><span class="sxs-lookup"><span data-stu-id="7ac5e-116">FSTAB errors</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/ )

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a><span data-ttu-id="7ac5e-117">Activer la fonction de diagnostic sur une nouvelle machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="7ac5e-117">Enable diagnostics on a new virtual machine</span></span>
1. <span data-ttu-id="7ac5e-118">Lorsque vous créez une Machine virtuelle à partir de la version préliminaire du portail de hello, sélectionnez hello **Azure Resource Manager** à partir de la liste déroulante modèle de déploiement hello :</span><span class="sxs-lookup"><span data-stu-id="7ac5e-118">When creating a new Virtual Machine from hello Preview Portal, select hello **Azure Resource Manager** from hello deployment model dropdown:</span></span>
 
    ![Gestionnaire de ressources](./media/boot-diagnostics/screenshot3.jpg)

2. <span data-ttu-id="7ac5e-120">Configurer hello analyse option tooselect hello de stockage Azure où vous aimeriez tooplace ces fichiers de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="7ac5e-120">Configure hello Monitoring option tooselect hello storage account where you would like tooplace these diagnostic files.</span></span>
 
    ![Créer une machine virtuelle](./media/boot-diagnostics/screenshot4.jpg)

3. <span data-ttu-id="7ac5e-122">Si vous déployez un modèle Azure Resource Manager, accédez de ressource d’ordinateur virtuel tooyour et ajouter la section de profil de diagnostics hello.</span><span class="sxs-lookup"><span data-stu-id="7ac5e-122">If you are deploying from an Azure Resource Manager template, navigate tooyour Virtual Machine resource and append hello diagnostics profile section.</span></span> <span data-ttu-id="7ac5e-123">N’oubliez pas d’en-tête de version de l’API de toouse hello « 2015-06-15 ».</span><span class="sxs-lookup"><span data-stu-id="7ac5e-123">Remember toouse hello “2015-06-15” API version header.</span></span>

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. <span data-ttu-id="7ac5e-124">profil de diagnostic Hello vous permet de compte de stockage hello tooselect où vous souhaitez tooput ces journaux.</span><span class="sxs-lookup"><span data-stu-id="7ac5e-124">hello diagnostics profile enables you tooselect hello storage account where you want tooput these logs.</span></span>

    ```json
            "diagnosticsProfile": {
                "bootDiagnostics": {
                "enabled": true,
                "storageUri": "[concat('http://', parameters('newStorageAccountName'), '.blob.core.windows.net')]"
                }
            }
            }
        }
    ```

## <a name="update-an-existing-virtual-machine"></a><span data-ttu-id="7ac5e-125">Mettre à jour une machine virtuelle existante</span><span class="sxs-lookup"><span data-stu-id="7ac5e-125">Update an existing virtual machine</span></span>

<span data-ttu-id="7ac5e-126">diagnostics de démarrage tooenable via le portail de hello, vous pouvez également mettre à jour un ordinateur virtuel existant via le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="7ac5e-126">tooenable boot diagnostics through hello portal, you can also update an existing virtual machine through hello portal.</span></span> <span data-ttu-id="7ac5e-127">Sélectionnez hello option Diagnostics de démarrage et les enregistrer.</span><span class="sxs-lookup"><span data-stu-id="7ac5e-127">Select hello Boot Diagnostics option and Save.</span></span> <span data-ttu-id="7ac5e-128">Redémarrez l’effet de tootake hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7ac5e-128">Restart hello VM tootake effect.</span></span>

![Mettre à jour une machine virtuelle existante](./media/boot-diagnostics/screenshot5.png)