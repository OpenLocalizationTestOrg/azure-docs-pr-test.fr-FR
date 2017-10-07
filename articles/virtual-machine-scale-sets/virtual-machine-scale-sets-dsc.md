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
# <a name="using-virtual-machine-scale-sets-with-hello-azure-dsc-extension"></a>À l’aide de machines virtuelles identiques avec hello extensions Azure DSC
[Machines virtuelles identiques](virtual-machine-scale-sets-overview.md) peut être utilisé avec hello [Configuration d’état souhaité (DSC) Azure](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) Gestionnaire d’extensions. Machines virtuelles identiques fournissent un moyen toodeploy et gérer un grand nombre d’ordinateurs virtuels et peuvent être distribuées configurées et l’extraction de tooload de réponse. DSC est utilisé tooconfigure hello machines virtuelles lorsqu’elles s’en ligne afin qu’ils exécutent un logiciel production hello.

## <a name="differences-between-deploying-toovirtual-machines-and-virtual-machine-scale-sets"></a>Différences entre le déploiement d’ordinateurs de tooVirtual et des machines virtuelles identiques
structure de modèle sous-jacent Hello pour un ensemble d’échelle de machine virtuelle est légèrement différente à partir d’une seule machine virtuelle. Plus précisément, une seule machine virtuelle déploie les extensions sous le nœud de « machines virtuelles » hello. Il existe une entrée de type « extensions » où DSC est ajouté toohello modèle

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

Un nœud de jeu de mise à l’échelle machine virtuelle a une section « Propriétés » par « VirtualMachineProfile », « extensionProfile » attribut de hello. La configuration DSC est ajoutée sous « extensions »

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

## <a name="behavior-for-a-virtual-machine-scale-set"></a>Comportement d’un groupe identique de machines virtuelles
comportement Hello pour un ensemble d’échelle de machine virtuelle est le comportement toohello identiques pour une seule machine virtuelle. Lorsqu’un nouvel ordinateur virtuel est créé, il est configuré automatiquement par hello extension DSC. Si une version plus récente de hello que WMF est requis par l’extension de hello, hello machine virtuelle redémarre avant la mise en ligne. Une fois qu’il est en ligne, il les télécharge hello DSC configuration .zip et mettre en service sur hello machine virtuelle. Vous trouverez plus de détails dans [hello vue d’ensemble des extensions Azure DSC](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="next-steps"></a>Étapes suivantes
Examinez hello [modèle Azure Resource Manager pour l’extension de hello DSC](../virtual-machines/windows/extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Découvrez comment hello [extension DSC gère en toute sécurité les informations d’identification](../virtual-machines/windows/extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Pour plus d’informations sur le Gestionnaire d’extensions Azure DSC hello, consultez [Gestionnaire d’extensions Azure DSC Introduction toohello](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Pour plus d’informations sur PowerShell DSC, [visitez le centre de documentation PowerShell hello](https://msdn.microsoft.com/powershell/dsc/overview). 

