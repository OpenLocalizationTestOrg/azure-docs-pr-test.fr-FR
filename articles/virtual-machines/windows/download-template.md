---
title: "modèle de hello aaaDownload pour une machine virtuelle Azure | Documents Microsoft"
description: "Télécharger hello templatefor un toohelp de machine virtuelle avec l’automatisation des déploiements dans le modèle de déploiement du Gestionnaire de ressources hello"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 51ef4f51-0942-4249-afea-4a3f87ce1ff8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 86fd05f67409019b5e5c9023881745047860eee1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="download-hello-template-for-a-vm"></a>Téléchargez le modèle de hello pour une machine virtuelle
Lorsque vous créez une machine virtuelle dans Azure à l’aide du portail de hello ou de PowerShell, un gestionnaire de ressources du modèle est automatiquement créé pour vous. Vous pouvez utiliser cette copie de tooquickly un déploiement de modèle. modèle de Hello contient des informations sur toutes les ressources hello dans un groupe de ressources. Pour un ordinateur virtuel, cela signifie que le modèle de hello contient tout ce qui est créé pour prendre en charge hello VM dans ce groupe de ressources, y compris des ressources de mise en réseau hello.

## <a name="download-hello-template-using-hello-portal"></a>Téléchargez le modèle de hello à l’aide du portail de hello
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).
2. Menu d’un hello concentrateur, sélectionnez **virtuels**.
3. Sélectionnez hello virtuels à partir de la liste de hello.
4. Sélectionnez **Script Automation**.
5. Sélectionnez **télécharger** et enregistrez l’ordinateur local du tooyour fichier .zip hello.
6. Ouvrez le fichier .zip de hello et extraire le dossier de tooa fichiers hello. fichier .zip de Hello contient :
   
   * deploy.ps1
   * deploy.sh 
   * deployer.rb
   * DeploymentHelper.cs
   * parameters.json
   * template.json

fichier de template.json Hello est le modèle de hello.

## <a name="download-hello-template-using-powershell"></a>Téléchargez le modèle de hello à l’aide de PowerShell
Vous pouvez également télécharger le fichier de modèle .json hello à l’aide de hello [Export-AzureRMResourceGroup](https://msdn.microsoft.com/library/mt715427.aspx) applet de commande. Vous pouvez utiliser hello `-path` paramètre tooprovide hello nom de fichier et chemin d’accès de fichier .json de hello. Cet exemple montre comment le modèle de hello de toodownload pour le groupe de ressources hello nommé **myResourceGroup** toohello **C:\users\public\downloads** dossier sur votre ordinateur local.

```powershell
    Export-AzureRmResourceGroup -ResourceGroupName "myResourceGroup" -Path "C:\users\public\downloads"
```

## <a name="next-steps"></a>Étapes suivantes
toolearn plus sur le déploiement de ressources à l’aide de modèles, consultez [procédure pas à pas de gestionnaire de ressources du modèle](../../azure-resource-manager/resource-manager-template-walkthrough.md).

