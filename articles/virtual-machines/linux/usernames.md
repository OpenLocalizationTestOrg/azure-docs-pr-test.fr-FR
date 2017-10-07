---
title: "aaaSelecting noms d’utilisateur pour Linux | Documents Microsoft"
description: "Découvrez comment des noms tooselect utilisateur pour un ordinateur virtuel de Linux dans Azure."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 33b50c97-92f1-46c9-a623-e37f67459c5c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: c65e2ac46f40bb8c9d74cccbaf248a070c0fa6cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="selecting-user-names-for-linux-on-azure"></a>Sélection de noms d'utilisateur pour Linux dans Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Lorsque vous configurez un ordinateur virtuel de Linux sur Azure, vous devez spécifier nom hello d’un utilisateur non racine que vous pouvez utiliser ultérieurement toolog dans hello machine virtuelle. Vous pouvez choisir le nom hello du nouvel utilisateur de hello, ou si la configuration via hello portail Azure classic accepter par défaut de hello nom « azureuser ».

Dans la plupart des cas, cet utilisateur n’existe pas sur l’image de base hello et sera créé pendant le processus d’approvisionnement de hello. Si l’utilisateur hello existe sur l’image de machine virtuelle base hello, puis hello Azure Linux agent simplement configure un mot de passe hello et/ou une clé SSH pour cet utilisateur en fonction des informations hello que vous avez spécifié lors de la création de hello machine virtuelle.

**Toutefois**, Linux définit un ensemble de noms d’utilisateur à ne pas utiliser pour la création de nouveaux utilisateurs. Hello mise en service du processus sera **échouer** si vous essayez de tooprovision une VM Linux à l’aide d’un utilisateur système existant, qui est défini en tant qu’utilisateur avec UID 0 et 99. Un exemple classique est hello `root` utilisateur, ce qui a des UID 0.

* Voir aussi [Base standard Linux : plages d’ID utilisateur](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)

Hello Voici une liste des utilisateurs système intégré commun CentOS et Ubuntu que vous devez éviter d’utiliser lors de la configuration d’un ordinateur virtuel de Linux sur Azure. Cette liste est juste un exemple, consultez toohello documentation pour votre tooensure distribution username hello que vous choisissez ne sont pas en conflit avec un utilisateur système existant.

## <a name="centos"></a>CentOS
* abrt
* adm
* audio
* bin
* cdrom
* cgred
* daemon
* dbus
* dialout
* dip
* disk
* floppy
* ftp
* ftp
* games
* gopher
* haldaemon
* halt
* kmem
* lock
* lp
* mail
* man
* mem
* nfsnobody
* nobody
* ntp
* operator
* oprofile
* postdrop
* postfix
* qpidd
* root
* rpc
* rpcuser
* saslauth
* shutdown
* slocate
* sshd
* stapdev
* stapusr
* sync
* sys
* tape
* test
* tcpdump
* tty
* users
* utempter
* utmp
* uucp
* vcsa
* video
* wheel

## <a name="ubuntu"></a>Ubuntu
* adm
* admin
* audio
* backup
* bin
* cdrom
* crontab
* daemon
* dialout
* dip
* disk
* fax
* floppy
* fuse
* games
* gnats
* irc
* kmem
* landscape
* libuuid
* list
* lp
* mail
* man
* messagebus
* mlocate
* netdev
* news
* nobody
* nogroup
* operator
* plugdev
* proxy
* root
* sasl
* shadow
* src
* ssh
* sshd
* staff
* sudo
* sync
* sys
* syslog
* tape
* tty
* users
* utmp
* uucp
* video
* voice
* whoopsie
* www-data

