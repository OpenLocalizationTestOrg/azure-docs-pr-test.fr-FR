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
# <a name="how-tootag-a-windows-virtual-machine-in-azure"></a>Comment tootag une machine virtuelle de Windows dans Azure
Cet article décrit les différentes façons tootag une machine virtuelle de Windows dans Azure via le modèle de déploiement du Gestionnaire de ressources hello. Les balises sont des paires clé/valeur définies par l’utilisateur, qui peuvent être placées directement sur une ressource ou sur un groupe de ressources. Azure prend actuellement en charge des balises de too15 par la ressource et le groupe de ressources. Balises peuvent être placées sur une ressource au moment de la création de hello ou ajouté tooan les ressources existantes. Notez que les balises sont prises en charge pour les ressources créées via le modèle de déploiement Resource Manager hello uniquement. Si vous souhaitez tootag une machine virtuelle Linux, consultez [comment tootag une machine virtuelle de Linux dans Azure](../linux/tag.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-powershell"></a>Balisage avec PowerShell
toocreate, ajouter et supprimer des balises via PowerShell, vous devez tout d’abord tooset de votre [l’environnement PowerShell avec Azure Resource Manager][PowerShell environment with Azure Resource Manager]. Une fois que vous avez terminé le programme d’installation hello, vous pouvez placer des étiquettes sur les ressources de calcul, réseau et de stockage lors de la création ou après la création de ressources de hello via PowerShell. Cet article se concentre sur l’affichage et la modification des balises placées sur des machines virtuelles.

Accédez d’abord, tooa Machine virtuelle via hello `Get-AzureRmVM` applet de commande.

        PS C:\> Get-AzureRmVM -ResourceGroupName "MyResourceGroup" -Name "MyTestVM"

Si votre Machine virtuelle contient déjà des balises, vous verrez ensuite toutes les balises hello sur votre ressource :

        Tags : {
                "Application": "MyApp1",
                "Created By": "MyName",
                "Department": "MyDepartment",
                "Environment": "Production"
               }

Si vous souhaitez que les balises tooadd via PowerShell, vous pouvez utiliser hello `Set-AzureRmResource` commande. Notez que lors de la mise à jour des balises via PowerShell, les balises sont mises à jour comme un tout. Par conséquent, si vous ajoutez une ressource de tooa de balise qui comporte déjà des balises, vous devez tooinclude toutes les balises hello toobe placé sur la ressource de hello souhaitées. Voici un exemple de comment tooadd supplémentaire les balises tooa des ressources via les PowerShell Cmdlets.

Cette applet de commande premier définit toutes les balises hello placés sur *MyTestVM* toohello *$tags* variable, à l’aide de hello `Get-AzureRmResource` et `Tags` propriété.

        PS C:\> $tags = (Get-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM).Tags

Hello deuxième commande affiche des balises hello pour hello donné variable.

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

Hello troisième commande ajoute une balise supplémentaires de toohello *$tags* variable. Notez que hello hello  **+=**  tooappend hello nouvelle toohello de paire clé/valeur *$tags* liste.

        PS C:\> $tags += @{Name="Location";Value="MyLocation"}

commande quatrième Hello définit toutes les balises hello définis dans hello *$tags* toohello variable donné de ressources. Dans ce cas, il s’agit de MyTestVM.

        PS C:\> Set-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM -ResourceType "Microsoft.Compute/VirtualMachines" -Tag $tags

commande cinquième Hello affiche toutes les balises hello sur la ressource de hello. Comme vous pouvez le voir, *emplacement* est maintenant définie en tant que balise *MyLocation* en tant que valeur de hello.

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

toolearn en savoir plus sur le balisage via PowerShell, consultez hello [applets de commande Resource Azure][Azure Resource Cmdlets].

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a>Étapes suivantes
* toolearn en savoir plus sur le marquage de vos ressources Azure, consultez [vue d’ensemble du Gestionnaire de ressources Azure] [ Azure Resource Manager Overview] et [à l’aide de balises tooorganize vos ressources Azure] [ Using Tags tooorganize your Azure Resources].
* toosee balises peuvent vous aider à gérer votre utilisation des ressources Azure, voir [comprendre votre facture Azure] [ Understanding your Azure Bill] et [obtenir votre consommation de ressources Microsoft Azure] [Gain insights into your Microsoft Azure resource consumption].

[PowerShell environment with Azure Resource Manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
[Azure Resource Cmdlets]: https://msdn.microsoft.com/library/azure/dn757692.aspx
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags tooorganize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
