---
title: "Résolution des défaillances des extensions de machine virtuelle Linux | Microsoft Docs"
description: "En savoir plus sur la résolution des défaillances des extensions de machine virtuelle Azure Linux"
services: virtual-machines-linux
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: top-support-issue,azure-resource-manager
ms.assetid: f05d93f3-42fc-4a09-9798-d92f7929c417
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: 589890de379d0b729de1f1ba9e604e0ec0496f50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-azure-linux-vm-extension-failures"></a><span data-ttu-id="b6c6d-103">Dépannage des échecs d’extension de machine virtuelle Azure Linux</span><span class="sxs-lookup"><span data-stu-id="b6c6d-103">Troubleshooting Azure Linux VM extension failures</span></span>
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a><span data-ttu-id="b6c6d-104">Affichage de l’état de l’extension</span><span class="sxs-lookup"><span data-stu-id="b6c6d-104">Viewing extension status</span></span>
<span data-ttu-id="b6c6d-105">Les modèles Azure Resource Manager peuvent être exécutés à partir de l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="b6c6d-105">Azure Resource Manager templates can be executed from the  Azure CLI.</span></span> <span data-ttu-id="b6c6d-106">Une fois que le modèle est exécuté, l'état de l'extension peut être affiché à partir d'Azure Resource Explorer ou des outils de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="b6c6d-106">Once the template is executed, the extension status can be viewed from Azure Resource Explorer or the command line tools.</span></span>

<span data-ttu-id="b6c6d-107">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="b6c6d-107">Here is an example:</span></span>

<span data-ttu-id="b6c6d-108">Interface de ligne de commande Azure :</span><span class="sxs-lookup"><span data-stu-id="b6c6d-108">Azure CLI:</span></span>

      azure vm get-instance-view


<span data-ttu-id="b6c6d-109">Voici l'exemple de sortie :</span><span class="sxs-lookup"><span data-stu-id="b6c6d-109">Here is the sample output:</span></span>

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
  <span data-ttu-id="b6c6d-110">]</span><span class="sxs-lookup"><span data-stu-id="b6c6d-110">]</span></span>

## <a name="troubleshooting-extenson-failures"></a><span data-ttu-id="b6c6d-111">Dépannage des échecs d'extension :</span><span class="sxs-lookup"><span data-stu-id="b6c6d-111">Troubleshooting Extenson failures:</span></span>
### <a name="re-running-the-extension-on-the-vm"></a><span data-ttu-id="b6c6d-112">Réexécution de l’extension sur la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="b6c6d-112">Re-running the extension on the VM</span></span>
<span data-ttu-id="b6c6d-113">Si vous exécutez des scripts sur la machine virtuelle à l’aide de l’extension de script personnalisé, cela peut générer une erreur indiquant que la machine virtuelle a été créée avec succès mais que le script a échoué.</span><span class="sxs-lookup"><span data-stu-id="b6c6d-113">If you are running scripts on the VM using Custom Script Extension, you could sometimes run into an error where VM was created successfully but the script has failed.</span></span> <span data-ttu-id="b6c6d-114">Dans ces conditions, la méthode recommandée pour corriger cette erreur consiste à supprimer l'extension et exécuter le modèle à nouveau.</span><span class="sxs-lookup"><span data-stu-id="b6c6d-114">Under these conditons, the recommended way to recover from this error is to remove the extension and rerun the template again.</span></span>
<span data-ttu-id="b6c6d-115">Remarque : à l'avenir, cette fonctionnalité sera améliorée pour supprimer le besoin de désinstaller l'extension.</span><span class="sxs-lookup"><span data-stu-id="b6c6d-115">Note: In future, this functionality would be enhanced to remove the need for uninstalling the extension.</span></span>

#### <a name="remove-the-extension-from-azure-cli"></a><span data-ttu-id="b6c6d-116">Suppression de l’extension de l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="b6c6d-116">Remove the extension from Azure CLI</span></span>
      azure vm extension set --resource-group "KPRG1" --vm-name "kundanapdemo" --publisher-name "Microsoft.Compute.CustomScriptExtension" --name "myCustomScriptExtension" --version 1.4 --uninstall

<span data-ttu-id="b6c6d-117">Où « publsher-name » correspond au type d'extension à partir de la sortie de « azure vm get-instance-view » et name est le nom de la ressource d'extension à partir du modèle</span><span class="sxs-lookup"><span data-stu-id="b6c6d-117">Where "publsher-name" corresponds to the extension type from the output of "azure vm get-instance-view" and name is the name of the extension resource from the template</span></span>

<span data-ttu-id="b6c6d-118">Une fois que l'extension a été supprimée, le modèle peut être réexécuté pour exécuter les scripts sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b6c6d-118">Once the extension has been removed, the template can be re-executed to run the scripts on the VM.</span></span>

