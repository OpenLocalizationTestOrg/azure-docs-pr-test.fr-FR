---
title: "aaaUsing hello CLI d’Azure sur Windows | Documents Microsoft"
description: "À l’aide de hello CLI d’Azure sur Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/14/2017
ms.author: nepeters
ms.openlocfilehash: edca4a2701a7dfc0fc54df5649e8a5e7afc95490
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-on-windows"></a>À l’aide de hello CLI d’Azure sur Windows

Bonjour Azure Interface de ligne de commande (CLI) fournit une ligne de commande et l’environnement de script pour créer et gérer des ressources Azure. Hello CLI d’Azure est disponible pour les systèmes d’exploitation Windows, Linux et macOS. Dans ces systèmes d’exploitation, les commandes CLI hello sont identiques, mais la syntaxe de script spécifique de système d’exploitation peut être différentes.

Ce document détails hello manières hello CLI d’Azure peut être installé et exécuté sur Windows et les détails des considérations syntaxiques pour chaque. Pour en savoir plus sur Azure CLI, voir la [documentation Azure CLI]( https://docs.microsoft.com/en-us/cli/azure/overview).

## <a name="windows-subsystem-for-linux"></a>Sous-système Windows pour Linux

Hello le sous-système Windows pour Linux (WSL) fournit un environnement de Ubuntu Linux sur anniversaire Windows 10 et versions ultérieures. Une fois activé, le sous-système Windows pour Linux offre une expérience Bash native qui permet de créer et d’exécuter des scripts Azure CLI. Étant donné que le sous-système Windows pour Linux offre une expérience Bash native, les scripts Azure CLI peuvent être partagés par Mac OS, Linux et Windows sans nécessiter de modification.

toouse hello CLI d’Azure dans WSL, effectuer des opérations suivantes de hello.

|Task | Instructions |
|---|---|
| Activer le sous-système Windows pour Linux | [Documentation d’installation du sous-système Windows pour Linux](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide) |
| Installer hello CLI d’Azure |[Installer hello CLI sur WSL/Ubuntu 14.04](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#ubuntu)|

## <a name="powershell"></a>PowerShell

Hello CLI d’Azure peut être exécuté en mode natif dans Windows. Dans cette configuration, package de CLI d’Azure hello est installé sur le système d’exploitation de Windows hello et commandes peuvent être exécutées à partir de PowerShell. Dans cette configuration, les scripts et les commandes CLI Azure peuvent être exécutés sur n’importe quelle version prise en charge de Windows. Cependant, une syntaxe de script spécifique à la plateforme est nécessaire. C’est pourquoi les scripts ne peuvent pas toujours être partagés par Mac OS, Linux et Windows sans nécessiter de modification.

toouse hello CLI d’Azure sur Windows, installer le package hello à l’aide de ces instructions, [installation hello CLI sur Windows](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows).

## <a name="docker-image"></a>Image Docker

Lors de l’utilisation de Docker pour Windows, une image Docker qui inclut hello CLI d’Azure peut démarrer. Cette image est basée sur Linux et inclut une expérience Bash native.  Lors de l’utilisation de Docker pour Windows et image de CLI d’Azure hello, toobe scripts partagés entre macOS, Linux et Windows. 

toouse hello CLI d’Azure sur Docker pour Windows, assurez-vous que Docker pour Windows est en cours d’exécution et exécutez hello commande suivante.

```bash
docker run -it azuresdk/azure-cli-python:latest bash
```

Une fois terminé, une session démarre qui est un interpréteur de commandes préchargée avec des outils de CLI d’Azure hello.

## <a name="next-steps"></a>Étapes suivantes

[Exemple de commande pour les machines virtuelles Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Exemples de commande pour Azure Web Apps](../../app-service-web/app-service-cli-samples.md)

[Exemples de commande pour Azure SQL](../../sql-database/sql-database-cli-samples.md)
