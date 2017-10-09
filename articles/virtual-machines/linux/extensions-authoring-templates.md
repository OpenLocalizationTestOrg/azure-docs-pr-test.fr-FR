---
title: "modèles d’aaaAuthoring avec les extensions de Linux VM | Documents Microsoft"
description: "En savoir plus sur la création de modèles Azure Resource Manager avec des extensions de machine virtuelle Linux"
services: virtual-machines-linux
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 322f8f0b-6697-4acb-b5f3-b3f58d28358b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: b797e442d8706956bbc06c5be611a2b0119055d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="authoring-azure-resource-manager-templates-with-linux-vm-extensions"></a>Création de modèles Azure Resource Manager avec des extensions de machine virtuelle Linux
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

À partir de l’interface CLI d’Azure, exécutez hello suivant de commande :

      Azure VM extension list

Cette commande retourne hello, nom de serveur de publication, le nom de l’extension et la version comme suit :

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

toolook à des exemples de configurations pour les extensions de Linux, cliquez sur documentation hello pour voir [Linux eExtensions exemples](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Reportez-vous toohello suivant tooget un modèle entièrement terminé avec des Extensions de machine virtuelle.

[Extension de script personnalisé sur une machine virtuelle Linux](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/mongodb-on-ubuntu/azuredeploy.json/)

Après la création de modèle de hello, vous pouvez déployer à l’aide de hello CLI d’Azure.

