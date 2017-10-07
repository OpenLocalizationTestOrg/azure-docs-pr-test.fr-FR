---
title: "aaaUse des privilèges de racine sur les ordinateurs virtuels Linux | Documents Microsoft"
description: "Découvrez comment toouse racine des privilèges sur un ordinateur virtuel de Linux dans Azure."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: a2c106a2-dceb-43a3-9dd1-50ed77685952
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 9411588c5fd0c86c4c73b3e44fbb56ab150013d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-root-privileges-on-linux-virtual-machines-in-azure"></a>Utilisation des privilèges root sur les machines virtuelles Linux dans Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Par défaut, hello `root` utilisateur est désactivé sur les ordinateurs virtuels Linux dans Azure. Les utilisateurs peuvent exécuter des commandes avec des privilèges élevés à l’aide de hello `sudo` commande. Toutefois, l’expérience de hello peut-être varier en fonction du mode de configuration de système de hello.

1. **Clé SSH et le mot de passe ou uniquement** -hello virtual machine a été configurée avec un certificat de soit (`.CER` fichier) ou clé SSH ainsi un mot de passe, ou simplement un nom d’utilisateur et mot de passe. Dans ce cas `sudo` demandera hello mot de passe utilisateur avant d’exécuter la commande hello.
2. **Uniquement la clé SSH** -hello virtual machine a été configurée avec un certificat (`.cer`, `.pem`, ou `.pub` fichier) ou la clé SSH, mais aucun mot de passe.  Dans ce cas `sudo` **ne seront pas** demander hello mot de passe utilisateur avant d’exécuter la commande hello.

## <a name="ssh-key-and-password-or-password-only"></a>Clé SSH et mot de passe ou mot de passe uniquement
Se connecter à la machine virtuelle de hello Linux à l’aide de l’authentification par mot de passe ou clé SSH, puis exécuter des commandes à l’aide de `sudo`, par exemple :

    # sudo <command>
    [sudo] password for azureuser:

Dans ce cas les utilisateur hello demandera un mot de passe. Après avoir entré un mot de passe hello `sudo` exécutera commande hello avec `root` des privilèges.

Vous pouvez également activer sudo passwordless en modifiant hello `/etc/sudoers.d/waagent` de fichiers, par exemple :

    #/etc/sudoers.d/waagent
    azureuser ALL = (ALL) NOPASSWD: ALL

Cette modification permettra sudo passwordless par l’utilisateur hello « azureuser ».

## <a name="ssh-key-only"></a>Clé SSH uniquement
Se connecter à la machine virtuelle de hello Linux à l’aide de l’authentification par clé SSH, puis exécuter des commandes à l’aide de `sudo`, par exemple :

    # sudo <command>

Dans ce cas les utilisateur hello seront **pas** être invité à entrer un mot de passe. Après avoir appuyé sur `<enter>`, `sudo` exécutera commande hello avec `root` des privilèges.

