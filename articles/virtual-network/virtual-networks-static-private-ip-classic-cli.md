---
title: "les adresses IP privées aaaConfigure pour les machines virtuelles (classiques) - Azure CLI 1.0 | Documents Microsoft"
description: "Découvrez comment les adresses IP privées tooconfigure pour les machines virtuelles (classiques) à l’aide de hello Azure interface de ligne de commande (CLI) 1.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 17386acf-c708-4103-9b22-ff9bf04b778d
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 417a57181bcf5c2e6101bf3bdf63fc94ebc99df5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-hello-azure-cli-10"></a>Configurer des adresses IP privées pour une machine virtuelle (classique) à l’aide de hello Azure CLI 1.0

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Cet article décrit le modèle de déploiement classique hello. Vous pouvez également [gérer une adresse IP privée statique dans le modèle de déploiement du Gestionnaire de ressources hello](virtual-networks-static-private-ip-arm-cli.md).

commandes CLI d’Azure d’exemple Hello ci-dessous s’attendre à un environnement simple déjà créé. Si vous souhaitez que les commandes de hello toorun car elles sont affichées dans ce document, tout d’abord créer d’environnement de test hello décrit dans [créer un réseau virtuel](virtual-networks-create-vnet-classic-cli.md).

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a>Comment toospecify une adresse IP privée statique d’adresses lorsque vous créez une machine virtuelle
toocreate un nouvel ordinateur virtuel nommé *DNS01* dans un nouveau service cloud nommé *TestService* selon le scénario hello ci-dessus, procédez comme suit :

1. Si vous n’avez jamais utilisé CLI d’Azure, consultez [installer et configurer hello CLI d’Azure](../cli-install-nodejs.md) et suivez les instructions de hello point toohello où vous sélectionnez votre compte Azure et votre abonnement.
2. Exécutez hello **de création du service azure** commande du service de cloud toocreate hello.
   
        azure service create TestService --location uscentral
   
    Sortie attendue :
   
        info:    Executing command service create
        info:    Creating cloud service
        data:    Cloud service name TestService
        info:    service create command OK
3. Exécutez hello **créer une machine virtuelle azure** commande toocreate hello machine virtuelle. Notez la valeur hello pour une adresse IP privée statique. liste de Hello affiché après la sortie de hello explique paramètres hello utilisés.
   
        azure vm create -l centralus -n DNS01 -w TestVNet -S "192.168.1.101" TestService bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2 adminuser AdminP@ssw0rd
   
    Sortie attendue :
   
        info:    Executing command vm create
        warn:    --vm-size has not been specified. Defaulting too"Small".
        info:    Looking up image bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2
        info:    Looking up virtual network
        info:    Looking up cloud service
        warn:    --location option will be ignored
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Retrieving storage accounts
        info:    Creating VM
        info:    OK
        info:    vm create command OK
   
   * **-l (ou --location)**. Région Azure où hello machine virtuelle doit être créé. Pour notre scénario, *centralus*.
   * **-n (ou--vm-name)**. Nom de hello toobe de machine virtuelle créée.
   * **-w (ou --virtual-network-name)**. Nom de hello réseau virtuel où hello machine virtuelle doit être créé. 
   * **-S (ou --static-ip)**. Valeur adresse IP privée statique pour hello machine virtuelle.
   * **TestService**. Nom du service de cloud hello où hello machine virtuelle doit être créé.
   * **bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2**. Image utilisée toocreate hello machine virtuelle.
   * **adminuser**. Administrateur local pour hello machine virtuelle Windows.
   * **AdminP@ssw0rd**. Mot de passe administrateur local pour hello machine virtuelle Windows.

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a>Comment informations pour une machine virtuelle d’adresse IP privée statique de tooretrieve
adresse IP privée statique de tooview hello adresse hello pour les ordinateurs virtuels créés avec script hello ci-dessus, exécutez hello suivant commande CLI d’Azure et observez la valeur hello pour *réseau StaticIP*:

    azure vm static-ip show DNS01

Sortie attendue :

    info:    Executing command vm static-ip show
    info:    Getting virtual machines
    data:    Network StaticIP "192.168.1.101"
    info:    vm static-ip show command OK

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a>Comment tooremove une privée d’adresses IP statiques à partir d’une machine virtuelle
tooremove hello adresse IP privée statique ajouté toohello machine virtuelle dans le script hello ci-dessus, hello exécution suivant la commande CLI d’Azure :

    azure vm static-ip remove DNS01

Sortie attendue :

    info:    Executing command vm static-ip remove
    info:    Getting virtual machines
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip remove command OK

## <a name="how-tooadd-a-static-private-ip-tooan-existing-vm"></a>Comment tooadd un tooan d’IP privée statique machine virtuelle existante
tooadd un toohello d’adresse IP privée statique machine virtuelle créée à l’aide de script hello ci-dessus, exécutez commande suivante :

    azure vm static-ip set DNS01 192.168.1.101

Sortie attendue :

    info:    Executing command vm static-ip set
    info:    Getting virtual machines
    info:    Looking up virtual network
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip set command OK

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur les [adresses IP publiques réservées](virtual-networks-reserved-public-ip.md) .
* En savoir plus sur les [adresses IP publiques de niveau d’instance](virtual-networks-instance-level-public-ip.md) .
* Consultez hello [API REST de IP réservée](https://msdn.microsoft.com/library/azure/dn722420.aspx).

