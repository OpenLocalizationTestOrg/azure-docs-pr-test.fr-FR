---
title: aaaCreate une machine virtuelle dans hello portail Azure | Documents Microsoft
description: "Créer une machine virtuelle Windows dans hello portail Azure."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1871f823-ebd7-4eff-9a22-8e2411555595
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 3848a3d06a7ce377633db78ea385826ed40f94fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-running-windows-in-hello-azure-portal"></a>Créer une machine virtuelle exécutant Windows Bonjour portail Azure
> [!div class="op_single_selector"]
> * [Portail Azure](tutorial.md)
> * [PowerShell : Déploiement classique](create-powershell.md)
>
>

<br>

> [!IMPORTANT]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello. Découvrez comment trop[effectuer ces étapes à l’aide du modèle de déploiement du Gestionnaire de ressources hello](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) à l’aide de hello **portail Azure**.

Ce didacticiel vous montre comment toocreate Azure exécutant Windows Bonjour Azure portal de la machine virtuelle (VM). Nous allons utiliser une image Windows Server par exemple, mais qui est simplement l’une de hello plusieurs images offres Azure. Notez que votre choix en matière d’images dépend de votre abonnement. Par exemple, les images de bureau Windows peuvent être disponible tooMSDN abonnés.

Cette section vous montre comment toouse hello **tableau de bord** hello tooselect portail Azure et puis créer la machine virtuelle de hello.

Vous pouvez également créer des machines virtuelles en utilisant [vos propres images](createupload-vhd.md). toolearn à ce sujet et d’autres méthodes, consultez [toocreate de différentes manières une machine virtuelle Windows](../../virtual-machines-windows-creation-choices.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

<!-- 02/27/2017 Video removed as it was based on hello classic portal. -->

## <a id="createvirtualmachine"></a>Créer la machine virtuelle de hello
[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

## <a name="next-steps"></a>Étapes suivantes
* Découvrez comment trop[créer une machine virtuelle à l’aide du modèle de déploiement du Gestionnaire de ressources hello](../../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) Bonjour portail Azure.
* Ouvrez une session sur l’ordinateur virtuel de toohello. Pour obtenir des instructions, consultez [ouvrir une session sur l’ordinateur virtuel de tooa exécutant Windows Server](connect-logon.md).
* Attacher un toostore de données de disque. Vous pouvez attacher des disques, qu'ils soient vides ou non. Pour obtenir des instructions, consultez hello [attacher une machine virtuelle données disque tooa Windows créée avec le modèle de déploiement classique hello](attach-disk.md).
