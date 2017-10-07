---
title: "un ensemble d’échelle de Machine virtuelle à l’aide d’aaaCreate hello portail Azure | Documents Microsoft"
description: "Déployez des jeux de mise à l’échelle à l’aide du portail Azure."
keywords: "Jeux de mise à l’échelle de machine virtuelle"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: madhana
editor: tysonn
tags: azure-resource-manager
ms.assetid: 9c1583f0-bcc7-4b51-9d64-84da76de1fda
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: negat
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 23c88f4b1ba99994a38f8886f60735da74e5c17e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-virtual-machine-scale-set-with-hello-azure-portal"></a>Comment toocreate un ensemble d’échelle de Machine virtuelle avec hello portail Azure
Ce didacticiel vous montre combien il est facile toocreate un ensemble d’échelle de machines virtuelles en quelques minutes, à l’aide de hello portail Azure. Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/) avant de commencer.

## <a name="choose-hello-vm-image-from-hello-marketplace"></a>Choisissez l’image de machine virtuelle hello Marketplace de hello
À partir du portail de hello, vous pouvez facilement déployer une échelle avec CentOS, CoreOS, Debian, Open Suse, Red Hat Enterprise Linux, SUSE Linux Enterprise Server, Ubuntu Server ou les images de Windows Server.

Accédez d’abord, toohello [portail Azure](https://portal.azure.com) dans un navigateur web. Cliquez sur `New`, recherchez `scale set`, puis sélectionnez hello `Virtual machine scale set` entrée :

![ScaleSetPortalOverview](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalOverview.PNG)

## <a name="create-hello-scale-set"></a>Créer un ensemble d’échelle hello
Vous pouvez désormais utiliser les paramètres par défaut hello et créer rapidement un ensemble d’échelle hello.

* Sur hello `Basics` panneau, entrez un nom pour l’ensemble d’échelle hello. Ce nom devient hello base Hello nom de domaine complet d’équilibrage de charge hello devant un ensemble d’échelle hello, par conséquent, vérifiez hello nom est unique sur Azure toutes les.
* Sélectionnez le type de système d’exploitation souhaité, entrez le nom d’utilisateur de votre choix, puis sélectionnez le type d’authentification que vous préférez. Si vous choisissez un mot de passe, il doit être au moins 12 caractères et répondre aux trois des exigences de complexité suivant quatre hello : une lettre minuscule, une lettre majuscule, un chiffre et un caractère spécial. En savoir plus sur les [conditions requises pour les noms d’utilisateur et les mots de passe](../virtual-machines/windows/faq.md#what-are-the-username-requirements-when-creating-a-vm). Si vous choisissez `SSH public key`, être tooonly vraiment coller dans votre clé publique, pas votre clé privée :

![ScaleSetPortalBasics](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalBasics.PNG)

* Choisissez si vous le feriez comme ensemble d’échelle de hello toolimit de groupe de la sélection élective unique tooa ou si elle doit s’étendre sur plusieurs groupes de la sélection élective. Autoriser l’ensemble d’échelle de hello toospan groupes de la sélection élective permet échelle définit plus de 100 machines virtuelles de capacité (haut too1, 000), avec certaines limitations. Pour plus d’informations, consultez [cette documentation](./virtual-machine-scale-sets-placement-groups.md).
* Entrez le nom de groupe de ressources et l’emplacement de votre choix, puis cliquez sur `OK`.
* Sur hello `Virtual machine scale set service settings` panneau : entrez votre étiquette de nom de domaine de votre choix (base hello Hello nom de domaine complet pour l’équilibrage de charge hello devant un ensemble d’échelle hello). Cette étiquette doit être unique dans Azure.
* Choisissez l’image de disque du système d’exploitation, le nombre d’instances et la taille de machine que vous souhaitez.
* Choisissez votre type de disque souhaité : géré ou non géré. Pour plus d’informations, consultez [cette documentation](./virtual-machine-scale-sets-managed-disks.md). Si vous avez choisi un ensemble d’échelle toohave hello s’étendre sur plusieurs groupes de la sélection élective, cette option ne sera pas disponible, car le disque géré est requis pour la sélection élective toospan jeux de groupes.
* Activez ou désactivez la mise à l’échelle automatique et configurez-la si elle est activée :

![ScaleSetPortalService](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalService.PNG)

* Sur hello `Summary` panneau, lorsque la validation est effectuée, cliquez sur `OK` ensemble d’échelle de hello toostart de déploiement.


## <a name="connect-tooa-vm-in-hello-scale-set"></a>Se connecter tooa machine virtuelle dans un ensemble d’échelle hello
Si vous avez choisi toolimit votre échelle définie tooa de groupe de positionnement unique, puis un ensemble d’échelle hello est déployé avec toolet de règles configurées NAT vous vous connectez à l’échelle de toohello définir facilement (si non, virtuels tooconnect toohello dans l’échelle de hello définie, vous devez probablement toocreate un jumpbox Bonjour même réseau virtuel en tant qu’ensemble d’échelle hello). toosee, accédez à toohello `Inbound NAT Rules` onglet d’équilibrage de charge hello pour un ensemble d’échelle hello :

![ScaleSetPortalNatRules](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalNatRules.PNG)

Vous pouvez vous connecter tooeach machine virtuelle dans l’échelle de hello définies à l’aide de ces règles NAT. Par exemple, pour un ensemble d’échelle de Windows, s’il existe une règle NAT sur 50 000, le port entrant vous pourriez connecter toothat machine via RDP sur `<load-balancer-ip-address>:50000`. Pour un ensemble d’échelle Linux, vous va se connecter à l’aide de la commande hello `ssh -p 50000 <username>@<load-balancer-ip-address>`.

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur la mise à l’échelle toodeploy définit de hello CLI, consultez [cette documentation](virtual-machine-scale-sets-cli-quick-create.md).

Pour plus d’informations sur la mise à l’échelle toodeploy définit à partir de PowerShell, consultez [cette documentation](virtual-machine-scale-sets-windows-create.md).

Pour plus d’informations sur la mise à l’échelle toodeploy définit à partir de Visual Studio, consultez [cette documentation](virtual-machine-scale-sets-vs-create.md).

Pour plus d’informations générales, consultez hello [page de vue d’ensemble de documentation pour les jeux de mise à l’échelle](virtual-machine-scale-sets-overview.md).

Pour plus d’informations, consultez hello [page d’accueil pour les jeux de mise à l’échelle](https://azure.microsoft.com/services/virtual-machine-scale-sets/).

