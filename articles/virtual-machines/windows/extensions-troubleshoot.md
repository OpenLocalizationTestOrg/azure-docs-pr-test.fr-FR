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
# <a name="troubleshooting-azure-windows-vm-extension-failures"></a><span data-ttu-id="c4e62-103">Dépannage des échecs d’extension de machine virtuelle Windows dans Azure</span><span class="sxs-lookup"><span data-stu-id="c4e62-103">Troubleshooting Azure Windows VM extension failures</span></span>
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a><span data-ttu-id="c4e62-104">Affichage de l’état de l’extension</span><span class="sxs-lookup"><span data-stu-id="c4e62-104">Viewing extension status</span></span>
<span data-ttu-id="c4e62-105">Les modèles Azure Resource Manager sont exécutables à partir d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c4e62-105">Azure Resource Manager templates can be executed from Azure PowerShell.</span></span> <span data-ttu-id="c4e62-106">Une fois le modèle de hello est exécuté, l’état de l’extension hello peut être affiché à partir des outils de ligne de commande de l’Explorateur de ressources Azure ou hello.</span><span class="sxs-lookup"><span data-stu-id="c4e62-106">Once hello template is executed, hello extension status can be viewed from Azure Resource Explorer or hello command line tools.</span></span>

<span data-ttu-id="c4e62-107">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="c4e62-107">Here is an example:</span></span>

<span data-ttu-id="c4e62-108">Azure PowerShell :</span><span class="sxs-lookup"><span data-stu-id="c4e62-108">Azure PowerShell:</span></span>

      Get-AzureRmVM -ResourceGroupName $RGName -Name $vmName -Status

<span data-ttu-id="c4e62-109">Voici le résultat de l’exemple hello :</span><span class="sxs-lookup"><span data-stu-id="c4e62-109">Here is hello sample output:</span></span>

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
  <span data-ttu-id="c4e62-110">]</span><span class="sxs-lookup"><span data-stu-id="c4e62-110">]</span></span>

## <a name="troubleshooting-extension-failures"></a><span data-ttu-id="c4e62-111">Dépannage des échecs d’extension</span><span class="sxs-lookup"><span data-stu-id="c4e62-111">Troubleshooting extension failures</span></span>
### <a name="re-running-hello-extension-on-hello-vm"></a><span data-ttu-id="c4e62-112">Extension de hello nouveau en cours d’exécution sur la machine virtuelle de hello</span><span class="sxs-lookup"><span data-stu-id="c4e62-112">Re-running hello extension on hello VM</span></span>
<span data-ttu-id="c4e62-113">Si vous exécutez des scripts sur hello machine virtuelle à l’aide d’Extension de Script personnalisé, vous pourriez parfois rencontrer une erreur dans lequel la machine virtuelle a été créé avec succès mais hello script a échoué.</span><span class="sxs-lookup"><span data-stu-id="c4e62-113">If you are running scripts on hello VM using Custom Script Extension, you could sometimes run into an error where VM was created successfully but hello script has failed.</span></span> <span data-ttu-id="c4e62-114">Dans ces conditions, hello recommandé toorecover de façon à partir de cette erreur est tooremove hello extension et le nouveau modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="c4e62-114">Under these conditons, hello recommended way toorecover from this error is tooremove hello extension and rerun hello template again.</span></span>
<span data-ttu-id="c4e62-115">Remarque : Dans le futur, cette fonctionnalité serait tooremove étendu hello besoin de désinstaller l’extension de hello.</span><span class="sxs-lookup"><span data-stu-id="c4e62-115">Note: In future, this functionality would be enhanced tooremove hello need for uninstalling hello extension.</span></span>

#### <a name="remove-hello-extension-from-azure-powershell"></a><span data-ttu-id="c4e62-116">Supprimer une extension de hello d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c4e62-116">Remove hello extension from Azure PowerShell</span></span>
    Remove-AzureRmVMExtension -ResourceGroupName $RGName -VMName $vmName -Name "myCustomScriptExtension"

<span data-ttu-id="c4e62-117">Une fois que l’extension de hello a été supprimée, modèle de hello peut être réexécuté toorun hello scripts hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c4e62-117">Once hello extension has been removed, hello template can be re-executed toorun hello scripts on hello VM.</span></span>

