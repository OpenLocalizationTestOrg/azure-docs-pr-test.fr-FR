---
title: "aaaUsing souhaité état Configuration avec des machines virtuelles identiques | Documents Microsoft"
description: "À l’aide de machines virtuelles identiques avec hello extensions Azure DSC"
services: virtual-machine-scale-sets
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: c8f047b5-0e6c-4ef3-8a47-f1b284d32942
ms.service: virtual-machine-scale-sets
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 04/05/2017
ms.author: zachal
ms.openlocfilehash: a35f1ca6700aa4889978032aa512882db50d6573
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-virtual-machine-scale-sets-with-hello-azure-dsc-extension"></a><span data-ttu-id="1d480-103">À l’aide de machines virtuelles identiques avec hello extensions Azure DSC</span><span class="sxs-lookup"><span data-stu-id="1d480-103">Using Virtual Machine Scale Sets with hello Azure DSC Extension</span></span>
<span data-ttu-id="1d480-104">[Machines virtuelles identiques](virtual-machine-scale-sets-overview.md) peut être utilisé avec hello [Configuration d’état souhaité (DSC) Azure](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) Gestionnaire d’extensions.</span><span class="sxs-lookup"><span data-stu-id="1d480-104">[Virtual Machine Scale Sets](virtual-machine-scale-sets-overview.md) can be used with hello [Azure Desired State Configuration (DSC)](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) extension handler.</span></span> <span data-ttu-id="1d480-105">Machines virtuelles identiques fournissent un moyen toodeploy et gérer un grand nombre d’ordinateurs virtuels et peuvent être distribuées configurées et l’extraction de tooload de réponse.</span><span class="sxs-lookup"><span data-stu-id="1d480-105">Virtual machine scale sets provide a way toodeploy and manage large numbers of virtual machines, and can elastically scale in and out in response tooload.</span></span> <span data-ttu-id="1d480-106">DSC est utilisé tooconfigure hello machines virtuelles lorsqu’elles s’en ligne afin qu’ils exécutent un logiciel production hello.</span><span class="sxs-lookup"><span data-stu-id="1d480-106">DSC is used tooconfigure hello VMs as they come online so they are running hello production software.</span></span>

## <a name="differences-between-deploying-toovirtual-machines-and-virtual-machine-scale-sets"></a><span data-ttu-id="1d480-107">Différences entre le déploiement d’ordinateurs de tooVirtual et des machines virtuelles identiques</span><span class="sxs-lookup"><span data-stu-id="1d480-107">Differences between deploying tooVirtual Machines and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="1d480-108">structure de modèle sous-jacent Hello pour un ensemble d’échelle de machine virtuelle est légèrement différente à partir d’une seule machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1d480-108">hello underlying template structure for a virtual machine scale set is slightly different from a single VM.</span></span> <span data-ttu-id="1d480-109">Plus précisément, une seule machine virtuelle déploie les extensions sous le nœud de « machines virtuelles » hello.</span><span class="sxs-lookup"><span data-stu-id="1d480-109">Specifically, a single VM deploys extensions under hello "virtualMachines" node.</span></span> <span data-ttu-id="1d480-110">Il existe une entrée de type « extensions » où DSC est ajouté toohello modèle</span><span class="sxs-lookup"><span data-stu-id="1d480-110">There is an entry of type "extensions" where DSC is added toohello template</span></span>

```
"resources": [
          {
              "name": "Microsoft.Powershell.DSC",
              "type": "extensions",
              "location": "[resourceGroup().location]",
              "apiVersion": "2015-06-15",
              "dependsOn": [
                  "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
              ],
              "tags": {
                  "displayName": "dscExtension"
              },
              "properties": {
                  "publisher": "Microsoft.Powershell",
                  "type": "DSC",
                  "typeHandlerVersion": "2.20",
                  "autoUpgradeMinorVersion": false,
                  "forceUpdateTag": "[parameters('dscExtensionUpdateTagVersion')]",
                  "settings": {
                      "configuration": {
                          "url": "[concat(parameters('_artifactsLocation'), '/', variables('dscExtensionArchiveFolder'), '/', variables('dscExtensionArchiveFileName'))]",
                          "script": "DscExtension.ps1",
                          "function": "Main"
                      },
                      "configurationArguments": {
                          "nodeName": "[variables('vmName')]"
                      }
                  },
                  "protectedSettings": {
                      "configurationUrlSasToken": "[parameters('_artifactsLocationSasToken')]"
                  }
              }
          }
      ]
```

<span data-ttu-id="1d480-111">Un nœud de jeu de mise à l’échelle machine virtuelle a une section « Propriétés » par « VirtualMachineProfile », « extensionProfile » attribut de hello.</span><span class="sxs-lookup"><span data-stu-id="1d480-111">A virtual machine scale set node has a "properties" section with hello "VirtualMachineProfile", "extensionProfile" attribute.</span></span> <span data-ttu-id="1d480-112">La configuration DSC est ajoutée sous « extensions »</span><span class="sxs-lookup"><span data-stu-id="1d480-112">DSC is added under "extensions"</span></span>

```
"extensionProfile": {
            "extensions": [
                {
                    "name": "Microsoft.Powershell.DSC",
                    "properties": {
                        "publisher": "Microsoft.Powershell",
                        "type": "DSC",
                        "typeHandlerVersion": "2.20",
                        "autoUpgradeMinorVersion": false,
                        "forceUpdateTag": "[parameters('DscExtensionUpdateTagVersion')]",
                        "settings": {
                            "configuration": {
                                "url": "[concat(parameters('_artifactsLocation'), '/', variables('DscExtensionArchiveFolder'), '/', variables('DscExtensionArchiveFileName'))]",
                                "script": "DscExtension.ps1",
                                "function": "Main"
                            },
                            "configurationArguments": {
                                "nodeName": "localhost"
                            }
                        },
                        "protectedSettings": {
                            "configurationUrlSasToken": "[parameters('_artifactsLocationSasToken')]"
                        }
                    }
                }
            ]
```

## <a name="behavior-for-a-virtual-machine-scale-set"></a><span data-ttu-id="1d480-113">Comportement d’un groupe identique de machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="1d480-113">Behavior for a Virtual Machine Scale Set</span></span>
<span data-ttu-id="1d480-114">comportement Hello pour un ensemble d’échelle de machine virtuelle est le comportement toohello identiques pour une seule machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1d480-114">hello behavior for a virtual machine scale set is identical toohello behavior for a single VM.</span></span> <span data-ttu-id="1d480-115">Lorsqu’un nouvel ordinateur virtuel est créé, il est configuré automatiquement par hello extension DSC.</span><span class="sxs-lookup"><span data-stu-id="1d480-115">When a new VM is created, it is automatically provisioned with hello DSC extension.</span></span> <span data-ttu-id="1d480-116">Si une version plus récente de hello que WMF est requis par l’extension de hello, hello machine virtuelle redémarre avant la mise en ligne.</span><span class="sxs-lookup"><span data-stu-id="1d480-116">If a newer version of hello WMF is required by hello extension, hello VM reboots before coming online.</span></span> <span data-ttu-id="1d480-117">Une fois qu’il est en ligne, il les télécharge hello DSC configuration .zip et mettre en service sur hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1d480-117">Once it is online, it downloads hello DSC configuration .zip and provision it on hello VM.</span></span> <span data-ttu-id="1d480-118">Vous trouverez plus de détails dans [hello vue d’ensemble des extensions Azure DSC](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1d480-118">More details can be found in [hello Azure DSC Extension Overview](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1d480-119">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1d480-119">Next steps</span></span>
<span data-ttu-id="1d480-120">Examinez hello [modèle Azure Resource Manager pour l’extension de hello DSC](../virtual-machines/windows/extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1d480-120">Examine hello [Azure Resource Manager template for hello DSC extension](../virtual-machines/windows/extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="1d480-121">Découvrez comment hello [extension DSC gère en toute sécurité les informations d’identification](../virtual-machines/windows/extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1d480-121">Learn how hello [DSC extension securely handles credentials](../virtual-machines/windows/extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="1d480-122">Pour plus d’informations sur le Gestionnaire d’extensions Azure DSC hello, consultez [Gestionnaire d’extensions Azure DSC Introduction toohello](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1d480-122">For more information on hello Azure DSC extension handler, see [Introduction toohello Azure Desired State Configuration extension handler](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="1d480-123">Pour plus d’informations sur PowerShell DSC, [visitez le centre de documentation PowerShell hello](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="1d480-123">For more information about PowerShell DSC, [visit hello PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

