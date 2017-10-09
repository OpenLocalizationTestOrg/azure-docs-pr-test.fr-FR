---
title: "échecs d’extension de machine virtuelle Windows aaaTroubleshooting | Documents Microsoft"
description: "En savoir plus sur la résolution des problèmes pour les échecs d’extension de machine virtuelle Windows dans Azure"
services: virtual-machines-windows
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: top-support-issue,azure-resource-manager
ms.assetid: 878ab9b6-c3e6-40be-82d4-d77fecd5030f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: d24544743d9e0cb1a68ec9ab7718716f918054f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-windows-vm-extension-failures"></a>Dépannage des échecs d’extension de machine virtuelle Windows dans Azure
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a>Affichage de l’état de l’extension
Les modèles Azure Resource Manager sont exécutables à partir d’Azure PowerShell. Une fois le modèle de hello est exécuté, l’état de l’extension hello peut être affiché à partir des outils de ligne de commande de l’Explorateur de ressources Azure ou hello.

Voici un exemple :

Azure PowerShell :

      Get-AzureRmVM -ResourceGroupName $RGName -Name $vmName -Status

Voici le résultat de l’exemple hello :

      Extensions:  {
      "ExtensionType": "Microsoft.Compute.CustomScriptExtension",
      "Name": "myCustomScriptExtension",
      "SubStatuses": [
        {
          "Code": "ComponentStatus/StdOut/succeeded",
          "DisplayStatus": "Provisioning succeeded",
          "Level": "Info",
          "Message": "    Directory: C:\\temp\\n\\n\\nMode                LastWriteTime     Length Name
              \\n----                -------------     ------ ----                              \\n-a---          9/1/2015   2:03 AM         11
              test.txt                          \\n\\n",
                      "Time": null
          },
        {
          "Code": "ComponentStatus/StdErr/succeeded",
          "DisplayStatus": "Provisioning succeeded",
          "Level": "Info",
          "Message": "",
          "Time": null
        }
    }
  ]

## <a name="troubleshooting-extension-failures"></a>Dépannage des échecs d’extension
### <a name="re-running-hello-extension-on-hello-vm"></a>Extension de hello nouveau en cours d’exécution sur la machine virtuelle de hello
Si vous exécutez des scripts sur hello machine virtuelle à l’aide d’Extension de Script personnalisé, vous pourriez parfois rencontrer une erreur dans lequel la machine virtuelle a été créé avec succès mais hello script a échoué. Dans ces conditions, hello recommandé toorecover de façon à partir de cette erreur est tooremove hello extension et le nouveau modèle de hello.
Remarque : Dans le futur, cette fonctionnalité serait tooremove étendu hello besoin de désinstaller l’extension de hello.

#### <a name="remove-hello-extension-from-azure-powershell"></a>Supprimer une extension de hello d’Azure PowerShell
    Remove-AzureRmVMExtension -ResourceGroupName $RGName -VMName $vmName -Name "myCustomScriptExtension"

Une fois que l’extension de hello a été supprimée, modèle de hello peut être réexécuté toorun hello scripts hello machine virtuelle.

