---
title: "aaaUsing les noms d’hôte DNS dynamique tooregister"
description: "Cette page fournit des détails sur la façon de tooset des noms d’hôtes de tooregister DNS dynamiques dans vos propres serveurs DNS."
services: dns
documentationcenter: na
author: GarethBradshawMSFT
manager: timlt
editor: 
ms.assetid: c315961a-fa33-45cf-82b9-4551e70d32dd
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2017
ms.author: garbrad
ms.openlocfilehash: 8d4b44265714e6976f26bfb3446e8101aa70996a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-dynamic-dns-tooregister-hostnames-in-your-own-dns-server"></a>À l’aide de noms d’hôtes de tooregister DNS dynamique dans votre propre serveur DNS
[Azure fournit la résolution de noms](virtual-networks-name-resolution-for-vms-and-role-instances.md) pour les machines virtuelles et les instances de rôle. Cependant, lorsque votre résolution de noms doit aller au-delà de ceux fournis par Azure, vous pouvez fournir vos propres serveurs DNS. Cette offre vous hello power tootailor votre toosuit de solution DNS vos propres besoins. Par exemple, vous devrez peut-être tooaccess des ressources locales via votre contrôleur de domaine Active Directory.

Quand vos serveurs DNS personnalisés sont hébergés en tant que machines virtuelles de Azure vous pouvez transférer le nom d’hôte demande hello même réseau virtuel tooAzure tooresolve les noms d’hôte. Si vous ne souhaitez pas toouse cet itinéraire, vous pouvez inscrire les noms d’hôte de votre machine virtuelle dans votre serveur DNS à l’aide de DNS dynamique.  Azure n’hello capacité (par exemple, informations d’identification) toodirectly à créer des enregistrements dans vos serveurs DNS, afin d’autres mécanismes sont souvent nécessaires. Voici quelques scénarios courants avec des solutions alternatives.

## <a name="windows-clients"></a>Clients Windows
Les clients Windows non joints à un domaine tentent des mises à jour DNS dynamiques non sécurisées lors du démarrage ou de la modifications de leurs adresses IP. nom DNS de Hello est le nom d’hôte hello plus le suffixe DNS principal de hello. Azure laisse le suffixe DNS principal de hello vide, mais vous pouvez définir cette option Bonjour machine virtuelle, via hello [UI](https://technet.microsoft.com/library/cc794784.aspx) ou [à l’aide d’automation](https://social.technet.microsoft.com/forums/windowsserver/3720415a-6a9a-4bca-aa2a-6df58a1a47d7/change-primary-dns-suffix).

Les clients appartenant au domaine Windows inscrivent leurs adresses IP avec le contrôleur de domaine hello à l’aide de DNS dynamique sécurisée. processus de jonction de domaine Hello définit le suffixe DNS principal de hello sur le client de hello, crée et gère la relation d’approbation hello.

## <a name="linux-clients"></a>Clients Linux
Clients Linux généralement ne s’inscrire avec le serveur DNS de hello au démarrage, ils supposent que le serveur DHCP hello le fait. Les serveurs DHCP d’Azure n’ont pas de possibilité de hello ou les enregistrements de tooregister d’informations d’identification dans votre serveur DNS.  Vous pouvez utiliser un outil appelé *nsupdate*, qui est inclus dans le package de liaison hello, met à jour des DNS dynamiques toosend. Étant donné que le protocole DNS dynamique de hello est normalisé, vous pouvez utiliser *nsupdate* même lorsque vous utilisez pas liaison sur le serveur DNS de hello.

Vous pouvez utiliser des crochets hello fournis par toocreate de client DHCP hello et conserver l’entrée de nom d’hôte hello dans le serveur DNS hello. Cycle hello DHCP, les clients hello exécute des scripts de hello dans */etc/dhcp/dhclient-exit-hooks.d/*. Cela peut être utilisé tooregister hello nouvelle adresse IP à l’aide de *nsupdate*. Par exemple :

        #!/bin/sh
        requireddomain=mydomain.local

        # only execute on hello primary nic
        if [ "$interface" != "eth0" ]
        then
            return
        fi

        # when we have a new IP, perform nsupdate
        if [ "$reason" = BOUND ] || [ "$reason" = RENEW ] ||
           [ "$reason" = REBIND ] || [ "$reason" = REBOOT ]
        then
            host=`hostname`
            nsupdatecmds=/var/tmp/nsupdatecmds
              echo "update delete $host.$requireddomain a" > $nsupdatecmds
              echo "update add $host.$requireddomain 3600 a $new_ip_address" >> $nsupdatecmds
              echo "send" >> $nsupdatecmds

              nsupdate $nsupdatecmds
        fi

        
        

Vous pouvez également utiliser hello *nsupdate* tooperform de commande des mises à jour DNS dynamique sécurisée. Par exemple, quand vous utilisez un serveur DNS Bind, une paire de clés publique/privée est [générée](http://linux.yyz.us/nsupdate/).  le serveur DNS Hello est [configuré](http://linux.yyz.us/dns/ddns-server.html) avec la partie publique de hello de clé hello afin qu’il puisse vérifier la signature hello sur demande de hello. Vous devez utiliser hello *-k* option tooprovide hello paire de clés trop*nsupdate* par ordre de hello toobe demande signé de la mise à jour des DNS dynamique.

Lorsque vous utilisez un serveur DNS Windows, vous pouvez utiliser l’authentification Kerberos avec hello *-g* paramètre dans *nsupdate* (non disponible dans la version de Windows hello de *nsupdate* ). toodo cela, utilisez *kinit* informations d’identification de hello tooload (par exemple un [fichier keytab](http://www.itadmintools.com/2011/07/creating-kerberos-keytab-files.html)). Puis *nsupdate -g* collectera des informations d’identification hello à partir du cache de hello.

Si nécessaire, vous pouvez ajouter un tooyour de suffixe de recherche DNS machines virtuelles. suffixe DNS de Hello est spécifié dans hello */etc/resolv.conf* fichier. La plupart des distributions Linux prises gérer automatiquement le contenu de hello de ce fichier, généralement pas les modifier. Toutefois, vous pouvez remplacer le suffixe de hello à l’aide du client hello DHCP *remplacent* commande. toodo cela, dans */etc/dhcp/dhclient.conf*, ajoutez :

        supersede domain-name <required-dns-suffix>;

