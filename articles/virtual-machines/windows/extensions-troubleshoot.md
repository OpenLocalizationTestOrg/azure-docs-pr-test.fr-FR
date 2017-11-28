---
title: "Résolution des problèmes d’extension de machines virtuelles Windows | Microsoft Docs"
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
ms.openlocfilehash: 4dba196e1b838f2092b30972fb070514bd2a4b25
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-azure-windows-vm-extension-failures"></a><span data-ttu-id="49135-103">Dépannage des échecs d’extension de machine virtuelle Windows dans Azure</span><span class="sxs-lookup"><span data-stu-id="49135-103">Troubleshooting Azure Windows VM extension failures</span></span>
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a><span data-ttu-id="49135-104">Affichage de l’état de l’extension</span><span class="sxs-lookup"><span data-stu-id="49135-104">Viewing extension status</span></span>
<span data-ttu-id="49135-105">Les modèles Azure Resource Manager sont exécutables à partir d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="49135-105">Azure Resource Manager templates can be executed from Azure PowerShell.</span></span> <span data-ttu-id="49135-106">Une fois que le modèle est exécuté, l'état de l'extension peut être affiché à partir d'Azure Resource Explorer ou des outils de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="49135-106">Once the template is executed, the extension status can be viewed from Azure Resource Explorer or the command line tools.</span></span>

<span data-ttu-id="49135-107">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="49135-107">Here is an example:</span></span>

<span data-ttu-id="49135-108">Azure PowerShell :</span><span class="sxs-lookup"><span data-stu-id="49135-108">Azure PowerShell:</span></span>

      Get-AzureRmVM -ResourceGroupName $RGName -Name $vmName -Status

<span data-ttu-id="49135-109">Voici l'exemple de sortie :</span><span class="sxs-lookup"><span data-stu-id="49135-109">Here is the sample output:</span></span>

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
  <span data-ttu-id="49135-110">]</span><span class="sxs-lookup"><span data-stu-id="49135-110">]</span></span>

## <a name="troubleshooting-extension-failures"></a><span data-ttu-id="49135-111">Dépannage des échecs d’extension</span><span class="sxs-lookup"><span data-stu-id="49135-111">Troubleshooting extension failures</span></span>
### <a name="re-running-the-extension-on-the-vm"></a><span data-ttu-id="49135-112">Réexécution de l’extension sur la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="49135-112">Re-running the extension on the VM</span></span>
<span data-ttu-id="49135-113">Si vous exécutez des scripts sur la machine virtuelle à l’aide de l’extension de script personnalisé, cela peut générer une erreur indiquant que la machine virtuelle a été créée avec succès mais que le script a échoué.</span><span class="sxs-lookup"><span data-stu-id="49135-113">If you are running scripts on the VM using Custom Script Extension, you could sometimes run into an error where VM was created successfully but the script has failed.</span></span> <span data-ttu-id="49135-114">Dans ces conditions, la méthode recommandée pour corriger cette erreur consiste à supprimer l'extension et exécuter le modèle à nouveau.</span><span class="sxs-lookup"><span data-stu-id="49135-114">Under these conditons, the recommended way to recover from this error is to remove the extension and rerun the template again.</span></span>
<span data-ttu-id="49135-115">Remarque : à l'avenir, cette fonctionnalité sera améliorée pour supprimer le besoin de désinstaller l'extension.</span><span class="sxs-lookup"><span data-stu-id="49135-115">Note: In future, this functionality would be enhanced to remove the need for uninstalling the extension.</span></span>

#### <a name="remove-the-extension-from-azure-powershell"></a><span data-ttu-id="49135-116">Suppression de l’extension d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="49135-116">Remove the extension from Azure PowerShell</span></span>
    Remove-AzureRmVMExtension -ResourceGroupName $RGName -VMName $vmName -Name "myCustomScriptExtension"

<span data-ttu-id="49135-117">Une fois que l'extension a été supprimée, le modèle peut être réexécuté pour exécuter les scripts sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="49135-117">Once the extension has been removed, the template can be re-executed to run the scripts on the VM.</span></span>

