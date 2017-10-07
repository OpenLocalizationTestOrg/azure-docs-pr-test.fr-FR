---
title: aaaCreate nom de domaine complet pour un VM Linux Bonjour portail Azure | Documents Microsoft
description: "Découvrez comment toocreate un nom de domaine complet ou le nom de domaine complet pour un gestionnaire de ressources en fonction de machine virtuelle dans hello portail Azure."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 2cd6c249-a737-4a0a-b5ba-e1c09e551b30
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1494a0cb1caa62069c72096a739aee111ac8b383
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-qualified-domain-name-in-hello-azure-portal-for-a-linux-vm"></a>Créer un nom de domaine complet dans hello portail Azure pour un VM Linux

Lorsque vous créez un ordinateur virtuel (VM) Bonjour [portail Azure](https://portal.azure.com), une ressource IP publique pour l’ordinateur virtuel de hello est automatiquement créée. Vous utilisez cette hello d’accès IP adresse tooremotely machine virtuelle. Bien que le portail de hello ne crée pas une [nom de domaine complet](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), ou nom de domaine complet, vous pouvez ajouter un fois hello machine virtuelle est créée. Cet article explique hello étapes toocreate un nom DNS ou le nom de domaine complet.

## <a name="create-a-fqdn"></a>Créer un nom de domaine complet
Cet article suppose que vous avez déjà créé une machine virtuelle. Si nécessaire, vous pouvez [créer une machine virtuelle dans le portail de hello](quick-create-portal.md) ou [avec hello CLI d’Azure](quick-create-cli.md). Une fois que votre machine virtuelle est en cours d’exécution, procédez comme suit :

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

Vous pouvez maintenant vous connecter à distance toohello nom d’ordinateur virtuel à l’aide de ce serveur DNS comme des `ssh azureuser@mydns.westus.cloudapp.azure.com`.

## <a name="next-steps"></a>Étapes suivantes
Maintenant que votre machine virtuelle a un nom DNS et une IP publique, vous pouvez déployer des services ou des infrastructures d’applications tels que nginx, MongoDB, Docker, etc.

Vous pouvez également lire un autre article sur [l’utilisation de Resource Manager](../../azure-resource-manager/resource-group-overview.md) pour obtenir des conseils sur la création de vos déploiements Azure.

