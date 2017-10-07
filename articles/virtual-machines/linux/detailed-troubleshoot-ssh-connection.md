---
title: "résolution des problèmes d’aaaDetailed SSH pour une machine virtuelle Azure | Documents Microsoft"
description: "Plus SSH dépannage de problèmes de connexion tooan machine virtuelle Azure"
keywords: "refus de la connexion ssh,erreur ssh,ssh azure,échec de la connexion ssh"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: b8e8be5f-e8a6-489d-9922-9df8de32e839
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: support-article
ms.date: 07/06/2017
ms.author: iainfou
ms.openlocfilehash: 3f711e53a8251f8c06dbb589a258222566a4ae1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="detailed-ssh-troubleshooting-steps-for-issues-connecting-tooa-linux-vm-in-azure"></a>SSH détaillée dépannage de problèmes de connexion tooa VM Linux dans Azure
Il existe plusieurs raisons, que le client SSH hello peut ne pas être en mesure de tooreach le service SSH hello sur hello machine virtuelle. Si vous avez suivi via hello plus [SSH générale des étapes de dépannage](troubleshoot-ssh-connection.md), vous devez toofurther résoudre les problème de connexion hello. Cet article vous guide à travers toodetermine d’étapes de dépannage détaillées où hello connexion SSH est défectueux et comment tooresolve il.

## <a name="take-preliminary-steps"></a>Commencer par les étapes préliminaires
Hello diagramme ci-après illustre les composants hello impliqués.

![Diagramme qui affiche les composants d’un service SSH](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot1.png)

Hello suit vous aider à isoler la source de hello de défaillance de hello et déterminer les solutions.

1. Vérifier l’état de hello Hello machine virtuelle dans le portail de hello.
   Bonjour [portail Azure](https://portal.azure.com), sélectionnez **virtuels** > *nom d’ordinateur virtuel*.

   Hello volet d’état pour hello machine virtuelle doit afficher **en cours d’exécution**. Faites défiler tooshow des activités récentes pour le calcul, stockage et ressources réseau.

2. Sélectionnez **paramètres** tooexamine points de terminaison, les adresses IP, les groupes de sécurité réseau et les autres paramètres.

   Hello machine virtuelle doit avoir un point de terminaison défini pour le trafic SSH que vous pouvez consulter dans **points de terminaison** ou  **[groupe de sécurité réseau](../../virtual-network/virtual-networks-nsg.md)**. Les points de terminaison pour les machines virtuelles créées à l’aide de Resource Manager sont stockés dans un groupe de sécurité réseau. En outre, vérifiez que les règles hello ont été appliqués toohello groupe de sécurité réseau et que celles-ci ne soient référencées dans un sous-réseau de hello.

connectivité de réseau tooverify, vérifiez les points de terminaison hello configuré et voir si vous pouvez atteindre hello machine virtuelle via un autre protocole, tels que HTTP ou un autre service.

Après ces étapes, essayez à nouveau la connexion SSH hello.

## <a name="find-hello-source-of-hello-issue"></a>Rechercher la source de hello du problème de hello
client SSH Hello sur votre ordinateur risque d’échouer tooreach le service SSH hello sur hello Azure VM tooissues ou des erreurs de configuration Bonjour suivant de zones :

* [Ordinateur client SSH](#source-1-ssh-client-computer)
* [Appareil du périmètre de l’organisation](#source-2-organization-edge-device)
* [point de terminaison de service cloud et liste de contrôle d’accès (ACL) ;](#source-3-cloud-service-endpoint-and-acl)
* [Groupes de sécurité réseau](#source-4-network-security-groups)
* [Machine virtuelle Linux Azure](#source-5-linux-based-azure-virtual-machine)

## <a name="source-1-ssh-client-computer"></a>Source 1 : ordinateur client SSH
tooeliminate votre ordinateur en tant que source de hello de défaillance de hello, vérifiez qu’il peut SSH connexions tooanother localement, ordinateur Linux.

![Diagramme qui indique les composants de l’ordinateur client SSH](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot2.png)

Si la connexion de hello échoue, recherchez hello suivants sur votre ordinateur :

* un paramètre de pare-feu local qui bloque le trafic SSH entrant ou sortant (TCP 22) ;
* un logiciel de proxy client installé localement qui empêche les connexions SSH ;
* un logiciel de surveillance réseau installé localement qui empêche les connexions SSH ;
* d’autres types de logiciels de sécurité qui surveillent le trafic ou autorisent/interdisent des types spécifiques de trafic.

Si une des conditions suivantes s’appliquent, temporairement désactiver le logiciel de hello et essayez une toofind ordinateur locales de tooan de connexion SSH out raison hello hello connexion soit bloquée sur votre ordinateur. Puis fonctionne avec vos connexions réseau administrateur toocorrect hello logiciel paramètres tooallow SSH.

Si vous utilisez l’authentification par certificat, vérifiez que vous avez ces autorisations toohello .ssh dossier dans votre répertoire de base :

* Chmod 700 ~/.ssh
* Chmod 644 ~/.ssh/\*.pub
* Chmod 600 ~/.ssh/id_rsa (ou tout autre fichier contenant vos clés privées)
* Chmod 644 ~/.ssh/known_hosts (contient des ordinateurs hôtes que vous avez connecté toovia SSH)

## <a name="source-2-organization-edge-device"></a>Source 2 : appareil du périmètre de l’organisation
tooeliminate votre appareil de périphérie d’entreprise en tant que source de hello de défaillance de hello, vérifiez qu’un ordinateur qui est connecté directement toohello Internet peut créer un tooyour des connexions SSH machine virtuelle Azure. Si vous accédez à hello machine virtuelle via un VPN de site à site ou une connexion Azure ExpressRoute, ignorez trop[Source 4 : groupes de sécurité réseau](#nsg).

![Diagramme qui met en évidence un appareil du périmètre de l’organisation](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot3.png)

Si vous n’avez pas un ordinateur qui est directement connecté toohello Internet, créez une machine virtuelle Azure dans son propre service de cloud ou le groupe de ressources et l’utiliser. Pour plus d’informations, consultez [Créer une machine virtuelle exécutant Linux dans Azure](quick-create-cli.md). Supprimer hello ressource groupe ou ordinateur virtuel et un service cloud lorsque vous avez terminé avec votre test.

Si vous pouvez créer une connexion SSH avec un ordinateur qui est connecté directement toohello Internet, vérifiez votre appareil de périphérie d’entreprise pour :

* Un pare-feu qui bloque le trafic SSH avec hello Internet
* un serveur proxy qui empêche les connexions SSH ;
* un logiciel de détection d’intrusion ou de surveillance réseau s’exécutant sur les appareils de votre réseau de périmètre qui empêche les connexions SSH.

Fonctionne avec vos paramètres de hello de toocorrect d’administrateur réseau de votre trafic SSH organisation bord appareils tooallow avec hello Internet.

## <a name="source-3-cloud-service-endpoint-and-acl"></a>Source 3 : Point de terminaison de service cloud et liste de contrôle d’accès
> [!NOTE]
> Cette source s’applique uniquement aux tooVMs qui ont été créés à l’aide du modèle de déploiement classique hello. Pour les ordinateurs virtuels qui ont été créés à l’aide du Gestionnaire de ressources, ignorez trop[source 4 : groupes de sécurité réseau](#nsg).

point de terminaison du service de cloud tooeliminate hello et la liste ACL en tant que source de hello de défaillance de hello, vérifiez qu’une autre machine virtuelle Azure dans hello même réseau virtuel peut rendre tooyour des connexions SSH machine virtuelle.

![Diagramme qui met en évidence un point de terminaison de service cloud et une liste de contrôle d’accès](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot4.png)

Si vous n’avez pas une autre machine virtuelle Bonjour même réseau virtuel, vous pouvez facilement en créer un. Pour plus d’informations, consultez [créer un VM Linux sur Azure à l’aide de hello CLI](quick-create-cli.md). Supprimer hello machine virtuelle supplémentaire lorsque vous avez terminé avec votre test.

Si vous pouvez créer une connexion SSH avec une machine virtuelle dans hello virtuel même réseau, vérifiez hello suivant de zones :

* **configuration de point de terminaison Hello pour le trafic de SSH sur la cible de hello machine virtuelle.** le port TCP privé Hello du point de terminaison hello doit correspondre à quels hello SSH service sur hello machine virtuelle écoute le port TCP hello. (le port par défaut de hello est 22). Vérifiez le numéro de port TCP SSH hello Bonjour portail Azure en sélectionnant **virtuels** > *nom de machine virtuelle* > **paramètres**  >  **Points de terminaison**.
* **Hello ACL pour point de terminaison du trafic hello SSH sur la machine virtuelle cible hello.** Une liste ACL permet toospecify autorisés ou non le trafic entrant à partir de hello Internet, en fonction de son adresse IP de source. ACL mal configurée peut empêcher le point de terminaison toohello entrant SSH du trafic. Vérifiez votre tooensure ACL que le trafic entrant à partir d’adresses IP publiques de hello de votre serveur proxy ou un autre serveur edge est autorisé. Pour plus d'informations, consultez [À propos des listes de contrôle d'accès (ACL) réseau](../../virtual-network/virtual-networks-acl.md).

point de terminaison tooeliminate hello en tant que source du problème de hello, supprimer le point de terminaison actuel hello, créer un autre point de terminaison et spécifier le nom SSH hello (port TCP 22 pour le numéro de port public et privé hello). Pour plus d’informations, consultez [Configuration des points de terminaison sur une machine virtuelle dans Azure](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

<a id="nsg"></a>

## <a name="source-4-network-security-groups"></a>Source 4 : groupes de sécurité réseau
Les groupes de sécurité réseau permettent toohave un contrôle plus précis du trafic autorisé de trafic entrant et sortant. Vous pouvez créer des règles qui s’étendent aux sous-réseaux et aux services cloud d’un réseau virtuel Azure. Vérifiez votre tooensure de règles de groupe de sécurité réseau qui tooand de trafic SSH à partir de hello Qu'internet est autorisée.
Pour plus d'informations, consultez [À propos des groupes de sécurité réseau](../../virtual-network/virtual-networks-nsg.md).

Vous pouvez également utiliser IP vérifier toovalidate hello NSG la configuration. Pour plus d’informations, consultez [Vue d’ensemble de la surveillance réseau Azure](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview). 

## <a name="source-5-linux-based-azure-virtual-machine"></a>Source 5 : machine virtuelle Azure Linux
Hello dernière source d’identifier les problèmes éventuels est hello machine virtuelle Azure lui-même.

![Diagramme qui met en évidence une machine virtuelle Azure Linux](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot5.png)

Si vous n’avez pas déjà fait, suivez les instructions de hello [tooreset un mot de passe ou de SSH pour les ordinateurs virtuels basés sur Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

Essayez une nouvelle fois de vous connecter à partir de votre ordinateur. Si elle échoue toujours, hello Voici quelques-uns des problèmes possibles de hello :

* Hello service SSH n’est pas exécuté sur la machine virtuelle cible hello.
* Hello SSH service n’écoute pas sur le port TCP 22. tootest, installez un client telnet sur votre ordinateur local et exécutez « telnet *cloudServiceName*. cloudapp.net 22 ». Cette étape détermine si hello virtuels permet de point de terminaison de communications entrantes et sortantes toohello SSH.
* le pare-feu local Hello sur la machine virtuelle cible hello possède des règles qui empêchent le trafic SSH entrant ou sortant.
* Détection d’intrusion ou un logiciel qui s’exécute sur une machine virtuelle Azure de hello de surveillance empêche les connexions SSH.

## <a name="additional-resources"></a>Ressources supplémentaires
Pour plus d’informations sur la résolution des problèmes d’accès aux applications, consultez [application tooan de résoudre les accès en cours d’exécution sur une machine virtuelle Azure](troubleshoot-app-connection.md)
