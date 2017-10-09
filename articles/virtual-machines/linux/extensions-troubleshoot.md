---
title: "aaaTroubleshooting Linux VM échecs d’extension | Documents Microsoft"
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
ms.openlocfilehash: 29a0ca34207421e0014380000a313d3c44e7e594
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-linux-vm-extension-failures"></a><span data-ttu-id="40153-103">Dépannage des échecs d’extension de machine virtuelle Azure Linux</span><span class="sxs-lookup"><span data-stu-id="40153-103">Troubleshooting Azure Linux VM extension failures</span></span>
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a><span data-ttu-id="40153-104">Affichage de l’état de l’extension</span><span class="sxs-lookup"><span data-stu-id="40153-104">Viewing extension status</span></span>
<span data-ttu-id="40153-105">Les modèles de gestionnaire de ressources Azure peuvent être exécutés à partir de hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="40153-105">Azure Resource Manager templates can be executed from hello  Azure CLI.</span></span> <span data-ttu-id="40153-106">Une fois le modèle de hello est exécuté, l’état de l’extension hello peut être affiché à partir des outils de ligne de commande de l’Explorateur de ressources Azure ou hello.</span><span class="sxs-lookup"><span data-stu-id="40153-106">Once hello template is executed, hello extension status can be viewed from Azure Resource Explorer or hello command line tools.</span></span>

<span data-ttu-id="40153-107">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="40153-107">Here is an example:</span></span>

<span data-ttu-id="40153-108">Interface de ligne de commande Azure :</span><span class="sxs-lookup"><span data-stu-id="40153-108">Azure CLI:</span></span>

      azure vm get-instance-view


<span data-ttu-id="40153-109">Voici le résultat de l’exemple hello :</span><span class="sxs-lookup"><span data-stu-id="40153-109">Here is hello sample output:</span></span>

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
  <span data-ttu-id="40153-110">]</span><span class="sxs-lookup"><span data-stu-id="40153-110">]</span></span>

## <a name="troubleshooting-extenson-failures"></a><span data-ttu-id="40153-111">Dépannage des échecs d'extension :</span><span class="sxs-lookup"><span data-stu-id="40153-111">Troubleshooting Extenson failures:</span></span>
### <a name="re-running-hello-extension-on-hello-vm"></a><span data-ttu-id="40153-112">Extension de hello nouveau en cours d’exécution sur la machine virtuelle de hello</span><span class="sxs-lookup"><span data-stu-id="40153-112">Re-running hello extension on hello VM</span></span>
<span data-ttu-id="40153-113">Si vous exécutez des scripts sur hello machine virtuelle à l’aide d’Extension de Script personnalisé, vous pourriez parfois rencontrer une erreur dans lequel la machine virtuelle a été créé avec succès mais hello script a échoué.</span><span class="sxs-lookup"><span data-stu-id="40153-113">If you are running scripts on hello VM using Custom Script Extension, you could sometimes run into an error where VM was created successfully but hello script has failed.</span></span> <span data-ttu-id="40153-114">Dans ces conditions, hello recommandé toorecover de façon à partir de cette erreur est tooremove hello extension et le nouveau modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="40153-114">Under these conditons, hello recommended way toorecover from this error is tooremove hello extension and rerun hello template again.</span></span>
<span data-ttu-id="40153-115">Remarque : Dans le futur, cette fonctionnalité serait tooremove étendu hello besoin de désinstaller l’extension de hello.</span><span class="sxs-lookup"><span data-stu-id="40153-115">Note: In future, this functionality would be enhanced tooremove hello need for uninstalling hello extension.</span></span>

#### <a name="remove-hello-extension-from-azure-cli"></a><span data-ttu-id="40153-116">Supprimer une extension de hello de CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="40153-116">Remove hello extension from Azure CLI</span></span>
      azure vm extension set --resource-group "KPRG1" --vm-name "kundanapdemo" --publisher-name "Microsoft.Compute.CustomScriptExtension" --name "myCustomScriptExtension" --version 1.4 --uninstall

<span data-ttu-id="40153-117">Où « de Publisher-name » correspond toohello type d’extension à partir de la sortie de hello de « get-instance-view de la machine virtuelle azure » et est nom hello de ressource d’extension hello à partir du modèle de hello</span><span class="sxs-lookup"><span data-stu-id="40153-117">Where "publsher-name" corresponds toohello extension type from hello output of "azure vm get-instance-view" and name is hello name of hello extension resource from hello template</span></span>

<span data-ttu-id="40153-118">Une fois que l’extension de hello a été supprimée, modèle de hello peut être réexécuté toorun hello scripts hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="40153-118">Once hello extension has been removed, hello template can be re-executed toorun hello scripts on hello VM.</span></span>

