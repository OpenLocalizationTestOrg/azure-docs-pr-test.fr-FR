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
# <a name="troubleshooting-azure-linux-vm-extension-failures"></a>Dépannage des échecs d’extension de machine virtuelle Azure Linux
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a>Affichage de l’état de l’extension
Les modèles de gestionnaire de ressources Azure peuvent être exécutés à partir de hello CLI d’Azure. Une fois le modèle de hello est exécuté, l’état de l’extension hello peut être affiché à partir des outils de ligne de commande de l’Explorateur de ressources Azure ou hello.

Voici un exemple :

Interface de ligne de commande Azure :

      azure vm get-instance-view


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

## <a name="troubleshooting-extenson-failures"></a>Dépannage des échecs d'extension :
### <a name="re-running-hello-extension-on-hello-vm"></a>Extension de hello nouveau en cours d’exécution sur la machine virtuelle de hello
Si vous exécutez des scripts sur hello machine virtuelle à l’aide d’Extension de Script personnalisé, vous pourriez parfois rencontrer une erreur dans lequel la machine virtuelle a été créé avec succès mais hello script a échoué. Dans ces conditions, hello recommandé toorecover de façon à partir de cette erreur est tooremove hello extension et le nouveau modèle de hello.
Remarque : Dans le futur, cette fonctionnalité serait tooremove étendu hello besoin de désinstaller l’extension de hello.

#### <a name="remove-hello-extension-from-azure-cli"></a>Supprimer une extension de hello de CLI d’Azure
      azure vm extension set --resource-group "KPRG1" --vm-name "kundanapdemo" --publisher-name "Microsoft.Compute.CustomScriptExtension" --name "myCustomScriptExtension" --version 1.4 --uninstall

Où « de Publisher-name » correspond toohello type d’extension à partir de la sortie de hello de « get-instance-view de la machine virtuelle azure » et est nom hello de ressource d’extension hello à partir du modèle de hello

Une fois que l’extension de hello a été supprimée, modèle de hello peut être réexécuté toorun hello scripts hello machine virtuelle.

