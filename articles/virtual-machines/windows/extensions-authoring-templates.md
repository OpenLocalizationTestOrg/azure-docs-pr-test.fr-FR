---
title: "aaaAuthoring modèles avec des extensions de machine virtuelle Windows | Documents Microsoft"
description: "En savoir plus sur la création de modèles Azure Resource Manager avec des extensions de machine virtuelle Windows"
services: virtual-machines-windows
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 418dd1f7-ded8-45ab-9a5a-a59d245e2555
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: c5156cb3859f7ff86bebda942150d268e57d6486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="authoring-azure-resource-manager-templates-with-windows-vm-extensions"></a>Création de modèles Azure Resource Manager avec des extensions de machine virtuelle Windows
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

À partir de Azure PowerShell, exécutez hello suivant l’applet de commande PowerShell de Azure :

      Get-AzureVMAvailableExtension


Cette applet de commande retourne la version, nom d’extension et nom de l’éditeur hello comme suit :

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

Ces trois propriétés mappent trop « éditeur », « type » et « typeHandlerVersion » respectivement dans hello ci-dessus extrait de modèle.

> [!NOTE]
> Il est toujours recommandée toouse hello dernière extension version tooget hello plus mis à jour des fonctionnalités.
> 
> 

## <a name="identifying-hello-schema-for-hello-extension-configuration-parameters"></a>Identification de schéma hello pour les paramètres de configuration d’extension hello
étape suivante de Hello par la création d’un modèle d’extension est format de hello tooidentify pour fournir des paramètres de configuration. Chaque extension prend en charge son propre ensemble de paramètres.

toolook à des exemples de configurations pour les extensions Windows, consultez [exemples d’extensions Windows](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Reportez-vous toohello suivant tooget un modèle entièrement terminé avec des extensions de machine virtuelle.

[Extension de script personnalisé sur une machine virtuelle Windows](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/201-list-storage-keys-windows-vm/azuredeploy.json/)

Après la création de modèle de hello, vous pouvez déployer à l’aide d’Azure PowerShell.

