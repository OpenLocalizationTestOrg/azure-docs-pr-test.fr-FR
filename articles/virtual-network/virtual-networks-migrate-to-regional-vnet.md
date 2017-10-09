---
title: "aaaMigrate un réseau virtuel Azure (classique) à partir d’une région de tooa groupe d’affinités | Documents Microsoft"
description: "Découvrez comment toomigrate un réseau virtuel (classique) à partir d’une affinité de groupe tooa région."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 84febcb9-bb8b-4e79-ab91-865ad9de41cb
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: e3a5c0f21e748912e29e2e8d03f4295720e63637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-a-virtual-network-classic-from-an-affinity-group-tooa-region"></a>Migrer un réseau virtuel (classiques) à partir d’une région de tooa groupe d’affinités

> [!IMPORTANT]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle de déploiement du Gestionnaire de ressources hello.

Groupes d’affinités vous assurer que les ressources créées au sein de hello même groupe d’affinités sont physiquement hébergés par des serveurs qui sont proches, l’activation de ces ressources toocommunicate plus rapide. Bonjour précédentes, les groupes d’affinités étaient requis pour créer des réseaux virtuels (classiques). À ce stade, service manager réseau hello géré des réseaux virtuels (classiques) ne pouvait fonctionner qu’au sein d’un ensemble de serveurs physiques ou unité d’échelle. Améliorations architecturales ont augmenté étendue hello de région de tooa de gestion de réseau.

Suite à ces améliorations architecturales, les groupes d’affinités ne sont plus recommandés ou requis pour les réseaux virtuels (classiques). Utilisez Hello de groupes d’affinités pour les réseaux virtuels (classiques) est remplacé par les régions. Les réseaux virtuels (classiques) qui sont associés à des régions sont appelés réseaux virtuels régionaux.

Nous vous recommandons de ne pas utiliser les groupes d’affinités en général. À l’exception de spécification de réseau virtuel hello, groupes d’affinités étaient également toouse important tooensure ressources, telles que le calcul (classiques) et de stockage (classique), soient proches les uns des autres. Toutefois, avec l’architecture de réseau Azure hello actuelle, ces exigences de la sélection élective ne sont plus nécessaires.

> [!IMPORTANT]
> Bien qu’il soit techniquement possible de toocreate un réseau virtuel est associé à un groupe d’affinités, n’existe donc aucune toodo raison attrayants. De nombreuses fonctionnalités de réseau virtuel, telles que les groupes de sécurité réseau, sont disponibles uniquement quand vous utilisez un réseau virtuel régional et ne sont pas disponibles pour les réseaux virtuels associés à des groupes d’affinités.
> 
> 

## <a name="edit-hello-network-configuration-file"></a>Modifier le fichier de configuration de réseau hello

1. Exporter le fichier de configuration de réseau hello. toolearn comment tooexport une configuration réseau de fichiers à l’aide de PowerShell ou hello Azure interface de ligne de commande (CLI) 1.0, consultez [configurer un réseau virtuel à l’aide d’un fichier de configuration réseau](virtual-networks-using-network-configuration-file.md#export).
2. Modifier le fichier de configuration de réseau hello, en remplaçant **AffinityGroup** avec **emplacement**. Spécifiez une [région](https://azure.microsoft.com/regions) Azure pour le paramètre **Location**.
   
   > [!NOTE]
   > Hello **emplacement** est hello région que vous avez spécifié pour le groupe d’affinités hello qui est associé à votre réseau virtuel (classique). Par exemple, si votre réseau virtuel (classiques) est associé à un groupe d’affinités qui se trouve dans l’ouest des États-Unis, lorsque vous migrez, votre **emplacement** doit pointer tooWest des États-Unis. 
   > 
   > 
   
    Modifiez hello lignes dans votre fichier de configuration de réseau suivantes, en remplaçant les valeurs hello par les vôtres : 
   
    **Ancienne valeur :**\<VirtualNetworkSitename="VNetUSWest" AffinityGroup="VNetDemoAG"\> 
   
    **Nouvelle valeur :**\<VirtualNetworkSitename="VNetUSWest" Location="West US"\>
3. Enregistrez vos modifications et [importer](virtual-networks-using-network-configuration-file.md#import) hello tooAzure de configuration réseau.

> [!NOTE]
> Cette migration n’entraîne pas de temps d’arrêt tooyour services.
> 
> 

## <a name="what-toodo-if-you-have-a-vm-classic-in-an-affinity-group"></a>Quelles toodo si vous avez une machine virtuelle (classique) dans un groupe d’affinités
Machines virtuelles (classiques) qui se trouvent actuellement dans un groupe d’affinités n’avez pas besoin de toobe supprimé du groupe d’affinité hello. Une fois qu’un ordinateur virtuel est déployé, il est déployé tooa seule unité d’échelle. Groupes d’affinités peuvent restreindre l’ensemble de hello de tailles de machine virtuelle disponibles pour un nouveau déploiement de machine virtuelle, mais toute machine virtuelle est déployée est déjà limitée jeu toohello de machine virtuelle des tailles disponibles dans l’unité d’échelle hello dans le hello l’ordinateur virtuel est déployé. Hello que machine virtuelle est déjà déployé l’unité d’échelle tooa, suppression d’une machine virtuelle à partir d’un groupe d’affinités n’a aucun effet sur la machine virtuelle de hello.
