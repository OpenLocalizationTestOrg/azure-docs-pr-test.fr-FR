---
title: aaaCreate nom de domaine complet pour un ordinateur virtuel Windows hello portail Azure | Documents Microsoft
description: "Découvrez comment toocreate un nom de domaine complet ou le nom de domaine complet pour un gestionnaire de ressources en fonction de machine virtuelle dans hello portail Azure."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a2ae5887-76df-485e-ae19-0efd96df8600
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 67c817ec97073803e513bc41ebde67b75ced565e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-qualified-domain-name-in-hello-azure-portal-for-a-windows-vm"></a>Créer un nom de domaine complet dans hello portail Azure pour une machine virtuelle Windows

Lorsque vous créez un ordinateur virtuel (VM) Bonjour [portail Azure](https://portal.azure.com), une ressource IP publique pour l’ordinateur virtuel de hello est automatiquement créée. Vous utilisez cette hello d’accès IP adresse tooremotely machine virtuelle. Bien que le portail de hello ne crée pas une [nom de domaine complet](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), ou nom de domaine complet, vous pouvez créer un fois hello machine virtuelle est créée. Cet article explique hello étapes toocreate un nom DNS ou le nom de domaine complet.

## <a name="create-a-fqdn"></a>Créer un nom de domaine complet
Cet article suppose que vous avez déjà créé une machine virtuelle. Si nécessaire, vous pouvez [créer une machine virtuelle dans le portail de hello](quick-create-portal.md) ou [avec Azure PowerShell](quick-create-powershell.md). Une fois que votre machine virtuelle est en cours d’exécution, procédez comme suit :

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

Vous pouvez maintenant vous connecter à distance toohello machine virtuelle en utilisant ce nom DNS, tel que de protocole RDP (Remote Desktop).

## <a name="next-steps"></a>Étapes suivantes
Maintenant que votre machine virtuelle a un nom DNS et une IP publique, vous pouvez déployer des infrastructures d’applications courantes ou des services tels qu’IIS, SQL ou SharePoint.

Vous pouvez également lire un autre article sur [l’utilisation de Resource Manager](../../azure-resource-manager/resource-group-overview.md) pour obtenir des conseils sur la création de vos déploiements Azure.

