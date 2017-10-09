---
title: "un classique de machine virtuelle Linux à l’aide d’aaaCreate hello Azure CLI 1.0 | Documents Microsoft"
description: "Découvrez comment toocreate une machine virtuelle Linux à l’aide de hello Azure CLI 1.0 hello modèle de déploiement classique"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: f8071a2e-ed91-4f77-87d9-519a37e5364f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 5c3c54e5d1444a79e8e609c76d04a3a621c8d03f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-classic-linux-vm-with-hello-azure-cli-10"></a>Comment tooCreate un classique de machine virtuelle Linux avec hello Azure CLI 1.0
> [!IMPORTANT] 
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello. Pour la version du Gestionnaire de ressources hello, consultez [ici](../create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Cette rubrique décrit comment toocreate une machine virtuelle de Linux (VM) à l’aide de hello Azure CLI 1.0 hello modèle de déploiement classique. Nous utilisons une image Linux à partir de hello disponible **IMAGES** sur Azure. commandes Hello Azure CLI 1.0 donnent hello suivant les choix de configuration, entre autres :

* Connexion hello tooa virtuel réseau d’ordinateurs virtuels
* Ajout de service cloud existant de hello VM tooan
* Ajouter le compte de stockage existant hello VM tooan
* Ajout de machine virtuelle hello tooan à haute disponibilité ou l’emplacement

> [!IMPORTANT]
> Si vous souhaitez que votre toouse de machine virtuelle un réseau virtuel pour pouvoir vous connecter tooit directement par nom d’hôte ou configurer des connexions entre différents locaux, assurez-vous que vous spécifiez le réseau virtuel de hello lorsque vous créez hello machine virtuelle. Une machine virtuelle peut être configurée toojoin un réseau virtuel uniquement lorsque vous créez hello machine virtuelle. Pour plus d’informations sur les réseaux virtuels, consultez la page [Présentation du réseau virtuel Azure](http://go.microsoft.com/fwlink/p/?LinkID=294063).
> 
> 

## <a name="how-toocreate-a-linux-vm-using-hello-classic-deployment-model"></a>Comment toocreate un VM Linux à l’aide de hello modèle de déploiement classique
[!INCLUDE [virtual-machines-create-LinuxVM](../../../../includes/virtual-machines-create-linuxvm.md)]

