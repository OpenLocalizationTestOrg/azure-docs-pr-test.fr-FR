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
# <a name="using-dynamic-dns-tooregister-hostnames-in-your-own-dns-server"></a><span data-ttu-id="5fac0-103">À l’aide de noms d’hôtes de tooregister DNS dynamique dans votre propre serveur DNS</span><span class="sxs-lookup"><span data-stu-id="5fac0-103">Using Dynamic DNS tooregister hostnames in your own DNS server</span></span>
<span data-ttu-id="5fac0-104">[Azure fournit la résolution de noms](virtual-networks-name-resolution-for-vms-and-role-instances.md) pour les machines virtuelles et les instances de rôle.</span><span class="sxs-lookup"><span data-stu-id="5fac0-104">[Azure provides name resolution](virtual-networks-name-resolution-for-vms-and-role-instances.md) for virtual machines (VMs) and role instances.</span></span> <span data-ttu-id="5fac0-105">Cependant, lorsque votre résolution de noms doit aller au-delà de ceux fournis par Azure, vous pouvez fournir vos propres serveurs DNS.</span><span class="sxs-lookup"><span data-stu-id="5fac0-105">However, when your name resolution needs go beyond those provided by Azure, you can provide your own DNS servers.</span></span> <span data-ttu-id="5fac0-106">Cette offre vous hello power tootailor votre toosuit de solution DNS vos propres besoins.</span><span class="sxs-lookup"><span data-stu-id="5fac0-106">This gives you hello power tootailor your DNS solution toosuit your own specific needs.</span></span> <span data-ttu-id="5fac0-107">Par exemple, vous devrez peut-être tooaccess des ressources locales via votre contrôleur de domaine Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5fac0-107">For example, you may need tooaccess on-premises resources via your Active Directory domain controller.</span></span>

<span data-ttu-id="5fac0-108">Quand vos serveurs DNS personnalisés sont hébergés en tant que machines virtuelles de Azure vous pouvez transférer le nom d’hôte demande hello même réseau virtuel tooAzure tooresolve les noms d’hôte.</span><span class="sxs-lookup"><span data-stu-id="5fac0-108">When your custom DNS servers are hosted as Azure VMs you can forward hostname queries for hello same vnet tooAzure tooresolve hostnames.</span></span> <span data-ttu-id="5fac0-109">Si vous ne souhaitez pas toouse cet itinéraire, vous pouvez inscrire les noms d’hôte de votre machine virtuelle dans votre serveur DNS à l’aide de DNS dynamique.</span><span class="sxs-lookup"><span data-stu-id="5fac0-109">If you do not wish toouse this route, you can register your VM hostnames in your DNS server using Dynamic DNS.</span></span>  <span data-ttu-id="5fac0-110">Azure n’hello capacité (par exemple, informations d’identification) toodirectly à créer des enregistrements dans vos serveurs DNS, afin d’autres mécanismes sont souvent nécessaires.</span><span class="sxs-lookup"><span data-stu-id="5fac0-110">Azure doesn't have hello ability (e.g. credentials) toodirectly create records in your DNS servers, so alternative arrangements are often needed.</span></span> <span data-ttu-id="5fac0-111">Voici quelques scénarios courants avec des solutions alternatives.</span><span class="sxs-lookup"><span data-stu-id="5fac0-111">Here are some common scenarios with alternatives.</span></span>

## <a name="windows-clients"></a><span data-ttu-id="5fac0-112">Clients Windows</span><span class="sxs-lookup"><span data-stu-id="5fac0-112">Windows clients</span></span>
<span data-ttu-id="5fac0-113">Les clients Windows non joints à un domaine tentent des mises à jour DNS dynamiques non sécurisées lors du démarrage ou de la modifications de leurs adresses IP.</span><span class="sxs-lookup"><span data-stu-id="5fac0-113">Non-domain-joined Windows clients attempt unsecured Dynamic DNS (DDNS) updates when they boot or when their IP address changes.</span></span> <span data-ttu-id="5fac0-114">nom DNS de Hello est le nom d’hôte hello plus le suffixe DNS principal de hello.</span><span class="sxs-lookup"><span data-stu-id="5fac0-114">hello DNS name is hello hostname plus hello primary DNS suffix.</span></span> <span data-ttu-id="5fac0-115">Azure laisse le suffixe DNS principal de hello vide, mais vous pouvez définir cette option Bonjour machine virtuelle, via hello [UI](https://technet.microsoft.com/library/cc794784.aspx) ou [à l’aide d’automation](https://social.technet.microsoft.com/forums/windowsserver/3720415a-6a9a-4bca-aa2a-6df58a1a47d7/change-primary-dns-suffix).</span><span class="sxs-lookup"><span data-stu-id="5fac0-115">Azure leaves hello primary DNS suffix blank, but you can set this in hello VM, via hello [UI](https://technet.microsoft.com/library/cc794784.aspx) or [by using automation](https://social.technet.microsoft.com/forums/windowsserver/3720415a-6a9a-4bca-aa2a-6df58a1a47d7/change-primary-dns-suffix).</span></span>

<span data-ttu-id="5fac0-116">Les clients appartenant au domaine Windows inscrivent leurs adresses IP avec le contrôleur de domaine hello à l’aide de DNS dynamique sécurisée.</span><span class="sxs-lookup"><span data-stu-id="5fac0-116">Domain-joined Windows clients register their IP addresses with hello domain controller by using secure Dynamic DNS.</span></span> <span data-ttu-id="5fac0-117">processus de jonction de domaine Hello définit le suffixe DNS principal de hello sur le client de hello, crée et gère la relation d’approbation hello.</span><span class="sxs-lookup"><span data-stu-id="5fac0-117">hello domain-join process sets hello primary DNS suffix on hello client and creates and maintains hello trust relationship.</span></span>

## <a name="linux-clients"></a><span data-ttu-id="5fac0-118">Clients Linux</span><span class="sxs-lookup"><span data-stu-id="5fac0-118">Linux clients</span></span>
<span data-ttu-id="5fac0-119">Clients Linux généralement ne s’inscrire avec le serveur DNS de hello au démarrage, ils supposent que le serveur DHCP hello le fait.</span><span class="sxs-lookup"><span data-stu-id="5fac0-119">Linux clients generally don't register themselves with hello DNS server on startup, they assume hello DHCP server does it.</span></span> <span data-ttu-id="5fac0-120">Les serveurs DHCP d’Azure n’ont pas de possibilité de hello ou les enregistrements de tooregister d’informations d’identification dans votre serveur DNS.</span><span class="sxs-lookup"><span data-stu-id="5fac0-120">Azure's DHCP servers do not have hello ability or credentials tooregister records in your DNS server.</span></span>  <span data-ttu-id="5fac0-121">Vous pouvez utiliser un outil appelé *nsupdate*, qui est inclus dans le package de liaison hello, met à jour des DNS dynamiques toosend.</span><span class="sxs-lookup"><span data-stu-id="5fac0-121">You can use a tool called *nsupdate*, which is included in hello Bind package, toosend Dynamic DNS updates.</span></span> <span data-ttu-id="5fac0-122">Étant donné que le protocole DNS dynamique de hello est normalisé, vous pouvez utiliser *nsupdate* même lorsque vous utilisez pas liaison sur le serveur DNS de hello.</span><span class="sxs-lookup"><span data-stu-id="5fac0-122">Because hello Dynamic DNS protocol is standardized, you can use *nsupdate* even when you're not using Bind on hello DNS server.</span></span>

<span data-ttu-id="5fac0-123">Vous pouvez utiliser des crochets hello fournis par toocreate de client DHCP hello et conserver l’entrée de nom d’hôte hello dans le serveur DNS hello.</span><span class="sxs-lookup"><span data-stu-id="5fac0-123">You can use hello hooks that are provided by hello DHCP client toocreate and maintain hello hostname entry in hello DNS server.</span></span> <span data-ttu-id="5fac0-124">Cycle hello DHCP, les clients hello exécute des scripts de hello dans */etc/dhcp/dhclient-exit-hooks.d/*.</span><span class="sxs-lookup"><span data-stu-id="5fac0-124">During hello DHCP cycle, hello client executes hello scripts in */etc/dhcp/dhclient-exit-hooks.d/*.</span></span> <span data-ttu-id="5fac0-125">Cela peut être utilisé tooregister hello nouvelle adresse IP à l’aide de *nsupdate*.</span><span class="sxs-lookup"><span data-stu-id="5fac0-125">This can be used tooregister hello new IP address by using *nsupdate*.</span></span> <span data-ttu-id="5fac0-126">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="5fac0-126">For example:</span></span>

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

        
        

<span data-ttu-id="5fac0-127">Vous pouvez également utiliser hello *nsupdate* tooperform de commande des mises à jour DNS dynamique sécurisée.</span><span class="sxs-lookup"><span data-stu-id="5fac0-127">You can also use hello *nsupdate* command tooperform secure Dynamic DNS updates.</span></span> <span data-ttu-id="5fac0-128">Par exemple, quand vous utilisez un serveur DNS Bind, une paire de clés publique/privée est [générée](http://linux.yyz.us/nsupdate/).</span><span class="sxs-lookup"><span data-stu-id="5fac0-128">For example, when you're using a Bind DNS server, a public-private key pair is [generated](http://linux.yyz.us/nsupdate/).</span></span>  <span data-ttu-id="5fac0-129">le serveur DNS Hello est [configuré](http://linux.yyz.us/dns/ddns-server.html) avec la partie publique de hello de clé hello afin qu’il puisse vérifier la signature hello sur demande de hello.</span><span class="sxs-lookup"><span data-stu-id="5fac0-129">hello DNS server is [configured](http://linux.yyz.us/dns/ddns-server.html) with hello public part of hello key so that it can verify hello signature on hello request.</span></span> <span data-ttu-id="5fac0-130">Vous devez utiliser hello *-k* option tooprovide hello paire de clés trop*nsupdate* par ordre de hello toobe demande signé de la mise à jour des DNS dynamique.</span><span class="sxs-lookup"><span data-stu-id="5fac0-130">You must use hello *-k* option tooprovide hello key-pair too*nsupdate* in order for hello Dynamic DNS update request toobe signed.</span></span>

<span data-ttu-id="5fac0-131">Lorsque vous utilisez un serveur DNS Windows, vous pouvez utiliser l’authentification Kerberos avec hello *-g* paramètre dans *nsupdate* (non disponible dans la version de Windows hello de *nsupdate* ).</span><span class="sxs-lookup"><span data-stu-id="5fac0-131">When you're using a Windows DNS server, you can use Kerberos authentication with hello *-g* parameter in *nsupdate* (not available in hello Windows version of *nsupdate*).</span></span> <span data-ttu-id="5fac0-132">toodo cela, utilisez *kinit* informations d’identification de hello tooload (par exemple un [fichier keytab](http://www.itadmintools.com/2011/07/creating-kerberos-keytab-files.html)).</span><span class="sxs-lookup"><span data-stu-id="5fac0-132">toodo this, use *kinit* tooload hello credentials (e.g. from a [keytab file](http://www.itadmintools.com/2011/07/creating-kerberos-keytab-files.html)).</span></span> <span data-ttu-id="5fac0-133">Puis *nsupdate -g* collectera des informations d’identification hello à partir du cache de hello.</span><span class="sxs-lookup"><span data-stu-id="5fac0-133">Then *nsupdate -g* will pick up hello credentials from hello cache.</span></span>

<span data-ttu-id="5fac0-134">Si nécessaire, vous pouvez ajouter un tooyour de suffixe de recherche DNS machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="5fac0-134">If needed, you can add a DNS search suffix tooyour VMs.</span></span> <span data-ttu-id="5fac0-135">suffixe DNS de Hello est spécifié dans hello */etc/resolv.conf* fichier.</span><span class="sxs-lookup"><span data-stu-id="5fac0-135">hello DNS suffix is specified in hello */etc/resolv.conf* file.</span></span> <span data-ttu-id="5fac0-136">La plupart des distributions Linux prises gérer automatiquement le contenu de hello de ce fichier, généralement pas les modifier.</span><span class="sxs-lookup"><span data-stu-id="5fac0-136">Most Linux distros automatically manage hello content of this file, so usually you can't edit it.</span></span> <span data-ttu-id="5fac0-137">Toutefois, vous pouvez remplacer le suffixe de hello à l’aide du client hello DHCP *remplacent* commande.</span><span class="sxs-lookup"><span data-stu-id="5fac0-137">However, you can override hello suffix by using hello DHCP client's *supersede* command.</span></span> <span data-ttu-id="5fac0-138">toodo cela, dans */etc/dhcp/dhclient.conf*, ajoutez :</span><span class="sxs-lookup"><span data-stu-id="5fac0-138">toodo this, in */etc/dhcp/dhclient.conf*, add:</span></span>

        supersede domain-name <required-dns-suffix>;

