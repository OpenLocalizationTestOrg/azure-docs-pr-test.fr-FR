---
title: "aaaEnable ou la désactivation de surveillance de machine virtuelle Azure"
description: "Décrit comment tooEnable ou désactiver l’analyse machine virtuelle Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: kmouss
manager: timlt
editor: 
ms.assetid: 6ce366d2-bd4c-4fef-a8f5-a3ae2374abcc
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/08/2016
ms.author: kmouss
ms.openlocfilehash: 39c2211e4e5f3ad364513b52c5acc70c00b432fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-or-disable-azure-vm-monitoring"></a>Activation ou désactivation de l’analyse de machine virtuelle Azure

Cette section décrit comment tooenable ou la désactivation de la surveillance sur Virtual machines en cours d’exécution sur Azure. Vous pouvez activer ou désactiver l’analyse à l’aide de portail de hello ou une Interface de ligne de commande de Azure pour Mac, Linux et Windows (hello CLI d’Azure).

> [!IMPORTANT]
> Ce document décrit la version 2.3 de hello Extension Diagnostics Linux, ce qui a été déconseillée. La version 2.3 sera prise en charge jusqu’au 30 juin 2018.
>
> La version 3.0 de hello Extension Diagnostics Linux peut être activée à la place. Pour plus d’informations, consultez [hello documentation](./diagnostic-extension.md).

## <a name="enable--disable-monitoring-through-hello-azure-portal"></a>Activer / désactiver l’analyse hello par le biais du portail Azure

Vous pouvez activer l’analyse de votre machine virtuelle Azure, qui fournit les données relatives à votre instance par périodes d’une minute. (des modifications du stockage s’appliquent). Les données de diagnostic détaillées seront ensuite disponibles pour hello machine virtuelle dans les graphiques portail hello ou via l’API de hello. Par défaut, le portail Azure active l’analyse basée sur l’hôte d’un ensemble limité d’indicateurs de performance. Vous pouvez activer l’analyse des métriques à partir d’une machine virtuelle lors de hello que machine virtuelle est en cours d’exécution ou arrêté.

* Ouvrez hello Azure portail à [https://portal.azure.com](https://portal.azure.com).
* Bonjour barre de navigation gauche, cliquez sur les ordinateurs virtuels.
* Dans hello répertorier les machines virtuelles, sélectionnez une instance en cours d’exécution ou arrêtée. Panneau de « Ordinateur virtuel » Hello s’ouvre.
* Cliquez sur Tous les paramètres.
* Cliquez sur Diagnostics.
* Modifier l’état tooOn ou désactivé. Vous pouvez également choisir dans ce niveau de hello Panneau de détails que vous aimeriez tooenable pour votre machine virtuelle de l’analyse.

![Activer ou désactiver l’analyse via hello portail Azure.][1]

## <a name="enable--disable-monitoring-with-azure-cli"></a>Activation et désactivation de l’analyse avec l’interface de ligne de commande (CLI) Azure

tooenable d’analyse pour une machine virtuelle Azure.

* Créez un fichier (nommé PrivateConfig.json, par exemple) :

```json
{
        "storageAccountName":"hello storage account tooreceive data",
        "storageAccountKey":"hello key of hello account"
}
```

* Activez l’extension hello via l’interface CLI d’Azure.

```azurecli
azure vm extension set myvm LinuxDiagnostic Microsoft.OSTCExtensions 2.3 --private-config-path PrivateConfig.json
```

Pour plus d’informations, consultez [performances et les données de diagnostic de Linux VM utilisation de l’Extension Diagnostics Linux tooMonitor](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

<!--Image references-->
[1]: ./media/vm-monitoring/portal-enable-disable.png
