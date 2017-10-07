---
title: aaaGet un ID de machine virtuelle Azure Linux | Documents Microsoft
description: "Décrit comment tooget et utilisez un Unique de machine virtuelle Azure Linux ID."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: kmouss
manager: timlt
editor: 
ms.assetid: 136c5d28-ff6b-4466-b27f-7a29785b5d27
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 01/23/2017
ms.author: kmouss
ms.openlocfilehash: 4c8ddfc2e892824581e77649285ee8adbccd5def
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-and-using-azure-vm-unique-id"></a>Accès et utilisation de l’ID unique de machine virtuelle Azure
L’ID unique de machine virtuelle Azure est un identificateur 128 bits codé et stocké dans le SMBIOS de la machine virtuelle IaaS Azure et qui peut être lu simultanément à l’aide des commandes du BIOS de la plate-forme.

L’ID unique de machine virtuelle Azure est une propriété en lecture seule. L’ID unique de machine virtuelle Azure ne sera pas modifié lors de l’arrêt pour redémarrage (planifié ou non planifié), lors du démarrage ou de l’arrêt pour désallouer, lors d’une réparation de service ou de la restauration en place. Toutefois, si hello machine virtuelle est un toocreate de capture instantanée et à copier une nouvelle instance, le nouvel ID de machine virtuelle Azure est configuré.

> [!NOTE]
> Si vous avez des machines virtuelles plus anciennes et que vous en cours d’exécution, car cette nouvelle fonctionnalité a été transférée (18 septembre 2014), redémarrez votre machine virtuelle tooautomatically obtenir un ID unique de Azure.
> 
> 

tooaccess Unique ID de machine virtuelle Azure à partir de hello machine virtuelle :

## <a name="create-a-vm"></a>Créer une machine virtuelle
Pour plus d’informations, consultez [Création d’une machine virtuelle](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="connect-toohello-vm"></a>Se connecter toohello machine virtuelle
Pour plus d’informations, consultez [SSH à partir de Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="query-vm-unique-id"></a>Interrogation de l’ID unique de machine virtuelle
Commande (l’exemple utilise **Ubuntu**) :

```bash
sudo dmidecode | grep UUID
```

Résultats attendus de l’exemple :

```bash
UUID: 090556DA-D4FA-764F-A9F1-63614EDA019A
```

En raison de tooBig Endian ordre des bits, hello ID de machine virtuelle Unique réel dans ce cas sera :

```bash
DA 56 05 09 – FA D4 – 4f 76 - A9F1-63614EDA019A
```

ID unique d’ordinateur virtuel Azure peut servir dans différents scénarios si hello machine virtuelle s’exécute sur Azure ou sur site et peut aider à vos spécifications de suivi de licence, création de rapports ou générales que peut avoir sur vos déploiements Azure IaaS. Éditeurs de logiciels de création d’applications et de les certifier sur Azure peuvent nécessiter tooidentify une machine virtuelle de Azure tout au long de son cycle de vie et le tootell si hello machine virtuelle s’exécute sur Azure, localement ou sur d’autres fournisseurs cloud. Cet identificateur de la plateforme peut par exemple permettent de détecter si hello logiciel est correctement concédé sous licence ou aider à n’importe quelle source de tooits de données de machine virtuelle comme tooassist sur la définition des métriques de droite hello pour la plate-forme hello et tootrack toocorrelate et mettre en corrélation ces mesures dans la liste autres utilisations.

