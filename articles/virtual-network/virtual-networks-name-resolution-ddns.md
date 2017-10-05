---
title: "Utilisation de DNS dynamique pour inscrire les noms d’hôte"
description: "Cette page fournit des détails sur la configuration du DNS dynamique pour enregistrer les noms d’hôte sur vos propres serveurs DNS."
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
ms.openlocfilehash: 440a062e5fff73526b2d77d7d0a7c52ca72a66f1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="using-dynamic-dns-to-register-hostnames-in-your-own-dns-server"></a><span data-ttu-id="47df3-103">Utilisation de DNS dynamique pour inscrire les noms d’hôte sur votre propre serveur DNS</span><span class="sxs-lookup"><span data-stu-id="47df3-103">Using Dynamic DNS to register hostnames in your own DNS server</span></span>
<span data-ttu-id="47df3-104">[Azure fournit la résolution de noms](virtual-networks-name-resolution-for-vms-and-role-instances.md) pour les machines virtuelles et les instances de rôle.</span><span class="sxs-lookup"><span data-stu-id="47df3-104">[Azure provides name resolution](virtual-networks-name-resolution-for-vms-and-role-instances.md) for virtual machines (VMs) and role instances.</span></span> <span data-ttu-id="47df3-105">Cependant, lorsque votre résolution de noms doit aller au-delà de ceux fournis par Azure, vous pouvez fournir vos propres serveurs DNS.</span><span class="sxs-lookup"><span data-stu-id="47df3-105">However, when your name resolution needs go beyond those provided by Azure, you can provide your own DNS servers.</span></span> <span data-ttu-id="47df3-106">Cela vous permet de personnaliser votre solution DNS pour l’adapter à vos propres besoins.</span><span class="sxs-lookup"><span data-stu-id="47df3-106">This gives you the power to tailor your DNS solution to suit your own specific needs.</span></span> <span data-ttu-id="47df3-107">Par exemple, vous pouvez avoir besoin d’accéder à des ressources locales avec votre contrôleur de domaine Active Directory.</span><span class="sxs-lookup"><span data-stu-id="47df3-107">For example, you may need to access on-premises resources via your Active Directory domain controller.</span></span>

<span data-ttu-id="47df3-108">Lorsque vos serveurs DNS personnalisés sont hébergés en tant que machines virtuelles Azure, vous pouvez transférer les requêtes de nom d’hôte (pour le même réseau virtuel) vers Azure pour résoudre les noms d’hôte.</span><span class="sxs-lookup"><span data-stu-id="47df3-108">When your custom DNS servers are hosted as Azure VMs you can forward hostname queries for the same vnet to Azure to resolve hostnames.</span></span> <span data-ttu-id="47df3-109">Si vous ne souhaitez pas utiliser cet itinéraire, vous pouvez enregistrer les noms d’hôte de vos machines virtuelles dans votre serveur DNS à l’aide du DNS dynamique.</span><span class="sxs-lookup"><span data-stu-id="47df3-109">If you do not wish to use this route, you can register your VM hostnames in your DNS server using Dynamic DNS.</span></span>  <span data-ttu-id="47df3-110">Comme Azure n’a pas la possibilité (informations d’identification, par exemple) de créer directement des enregistrements dans vos serveurs DNS, d’autres mécanismes sont souvent nécessaires.</span><span class="sxs-lookup"><span data-stu-id="47df3-110">Azure doesn't have the ability (e.g. credentials) to directly create records in your DNS servers, so alternative arrangements are often needed.</span></span> <span data-ttu-id="47df3-111">Voici quelques scénarios courants avec des solutions alternatives.</span><span class="sxs-lookup"><span data-stu-id="47df3-111">Here are some common scenarios with alternatives.</span></span>

## <a name="windows-clients"></a><span data-ttu-id="47df3-112">Clients Windows</span><span class="sxs-lookup"><span data-stu-id="47df3-112">Windows clients</span></span>
<span data-ttu-id="47df3-113">Les clients Windows non joints à un domaine tentent des mises à jour DNS dynamiques non sécurisées lors du démarrage ou de la modifications de leurs adresses IP.</span><span class="sxs-lookup"><span data-stu-id="47df3-113">Non-domain-joined Windows clients attempt unsecured Dynamic DNS (DDNS) updates when they boot or when their IP address changes.</span></span> <span data-ttu-id="47df3-114">Le nom DNS se compose du nom d’hôte et du suffixe DNS principal.</span><span class="sxs-lookup"><span data-stu-id="47df3-114">The DNS name is the hostname plus the primary DNS suffix.</span></span> <span data-ttu-id="47df3-115">Azure laisse le suffixe DNS principal vide, mais ce dernier peut être défini dans la machine virtuelle, via l’[interface utilisateur](https://technet.microsoft.com/library/cc794784.aspx) ou avec [Automation](https://social.technet.microsoft.com/forums/windowsserver/3720415a-6a9a-4bca-aa2a-6df58a1a47d7/change-primary-dns-suffix).</span><span class="sxs-lookup"><span data-stu-id="47df3-115">Azure leaves the primary DNS suffix blank, but you can set this in the VM, via the [UI](https://technet.microsoft.com/library/cc794784.aspx) or [by using automation](https://social.technet.microsoft.com/forums/windowsserver/3720415a-6a9a-4bca-aa2a-6df58a1a47d7/change-primary-dns-suffix).</span></span>

<span data-ttu-id="47df3-116">Les clients Windows joints à un domaine inscrivent leurs adresses IP auprès du contrôleur de domaine à l’aide de la mise à jour DNS dynamique sécurisée.</span><span class="sxs-lookup"><span data-stu-id="47df3-116">Domain-joined Windows clients register their IP addresses with the domain controller by using secure Dynamic DNS.</span></span> <span data-ttu-id="47df3-117">Le processus de jonction de domaine définit le suffixe DNS principal sur le client, puis crée et gère la relation d’approbation.</span><span class="sxs-lookup"><span data-stu-id="47df3-117">The domain-join process sets the primary DNS suffix on the client and creates and maintains the trust relationship.</span></span>

## <a name="linux-clients"></a><span data-ttu-id="47df3-118">Clients Linux</span><span class="sxs-lookup"><span data-stu-id="47df3-118">Linux clients</span></span>
<span data-ttu-id="47df3-119">En général, les clients Linux ne s’inscrivent pas eux-mêmes auprès du serveur DNS au démarrage et présument que ce dernier le fait à leur place.</span><span class="sxs-lookup"><span data-stu-id="47df3-119">Linux clients generally don't register themselves with the DNS server on startup, they assume the DHCP server does it.</span></span> <span data-ttu-id="47df3-120">Les serveurs DHCP d’Azure n’ont pas la capacité ou les informations d’identification pour stocker des enregistrements dans votre serveur DNS.</span><span class="sxs-lookup"><span data-stu-id="47df3-120">Azure's DHCP servers do not have the ability or credentials to register records in your DNS server.</span></span>  <span data-ttu-id="47df3-121">Vous pouvez utiliser un outil appelé *nsupdate*, qui est inclus dans le package Bind, pour envoyer des mises à jour DNS dynamiques.</span><span class="sxs-lookup"><span data-stu-id="47df3-121">You can use a tool called *nsupdate*, which is included in the Bind package, to send Dynamic DNS updates.</span></span> <span data-ttu-id="47df3-122">Comme le protocole DNS dynamique est normalisé, vous pouvez utiliser *nsupdate* même quand vous n’utilisez pas Bind sur le serveur DNS.</span><span class="sxs-lookup"><span data-stu-id="47df3-122">Because the Dynamic DNS protocol is standardized, you can use *nsupdate* even when you're not using Bind on the DNS server.</span></span>

<span data-ttu-id="47df3-123">Vous pouvez utiliser les raccordements fournis par le client DHCP pour créer et gérer l’entrée du nom d’hôte sur le serveur DNS.</span><span class="sxs-lookup"><span data-stu-id="47df3-123">You can use the hooks that are provided by the DHCP client to create and maintain the hostname entry in the DNS server.</span></span> <span data-ttu-id="47df3-124">Au cours du cycle DHCP, le client exécute les scripts dans */etc/dhcp/dhclient-exit-hooks.d/*.</span><span class="sxs-lookup"><span data-stu-id="47df3-124">During the DHCP cycle, the client executes the scripts in */etc/dhcp/dhclient-exit-hooks.d/*.</span></span> <span data-ttu-id="47df3-125">Vous pouvez l’utiliser pour inscrire la nouvelle adresse IP à l’aide de *nsupdate*.</span><span class="sxs-lookup"><span data-stu-id="47df3-125">This can be used to register the new IP address by using *nsupdate*.</span></span> <span data-ttu-id="47df3-126">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="47df3-126">For example:</span></span>

        #!/bin/sh
        requireddomain=mydomain.local

        # only execute on the primary nic
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

        
        

<span data-ttu-id="47df3-127">Vous pouvez également utiliser la commande *nsupdate* pour effectuer des mises à jour DNS dynamiques sécurisées.</span><span class="sxs-lookup"><span data-stu-id="47df3-127">You can also use the *nsupdate* command to perform secure Dynamic DNS updates.</span></span> <span data-ttu-id="47df3-128">Par exemple, quand vous utilisez un serveur DNS Bind, une paire de clés publique/privée est [générée](http://linux.yyz.us/nsupdate/).</span><span class="sxs-lookup"><span data-stu-id="47df3-128">For example, when you're using a Bind DNS server, a public-private key pair is [generated](http://linux.yyz.us/nsupdate/).</span></span>  <span data-ttu-id="47df3-129">Le serveur DNS est [configuré](http://linux.yyz.us/dns/ddns-server.html) avec la partie publique de la clé, ce qui lui permet de vérifier la signature sur la demande.</span><span class="sxs-lookup"><span data-stu-id="47df3-129">The DNS server is [configured](http://linux.yyz.us/dns/ddns-server.html) with the public part of the key so that it can verify the signature on the request.</span></span> <span data-ttu-id="47df3-130">Vous devez utiliser l’option *-k* pour fournir la paire de clés à *nsupdate* afin de signer la demande de mise à jour DNS dynamique.</span><span class="sxs-lookup"><span data-stu-id="47df3-130">You must use the *-k* option to provide the key-pair to *nsupdate* in order for the Dynamic DNS update request to be signed.</span></span>

<span data-ttu-id="47df3-131">Quand vous utilisez un serveur DNS Windows, l’authentification Kerberos peut être associée au paramètre *-g* dans *nsupdate* (non disponible dans la version Windows de *nsupdate*).</span><span class="sxs-lookup"><span data-stu-id="47df3-131">When you're using a Windows DNS server, you can use Kerberos authentication with the *-g* parameter in *nsupdate* (not available in the Windows version of *nsupdate*).</span></span> <span data-ttu-id="47df3-132">Pour ce faire, utilisez *kinit* pour charger les informations d’identification (par exemple, depuis un [fichier keytab](http://www.itadmintools.com/2011/07/creating-kerberos-keytab-files.html)).</span><span class="sxs-lookup"><span data-stu-id="47df3-132">To do this, use *kinit* to load the credentials (e.g. from a [keytab file](http://www.itadmintools.com/2011/07/creating-kerberos-keytab-files.html)).</span></span> <span data-ttu-id="47df3-133">*nsupdate -g* sélectionnera ensuite les informations d’identification à partir du cache.</span><span class="sxs-lookup"><span data-stu-id="47df3-133">Then *nsupdate -g* will pick up the credentials from the cache.</span></span>

<span data-ttu-id="47df3-134">Si nécessaire, vous pouvez ajouter un suffixe de recherche DNS à vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="47df3-134">If needed, you can add a DNS search suffix to your VMs.</span></span> <span data-ttu-id="47df3-135">Le suffixe DNS est spécifié dans le fichier */etc/resolv.conf* .</span><span class="sxs-lookup"><span data-stu-id="47df3-135">The DNS suffix is specified in the */etc/resolv.conf* file.</span></span> <span data-ttu-id="47df3-136">Comme la plupart des distributions Linux gèrent automatiquement le contenu de ce fichier, il ne peut généralement pas être modifié.</span><span class="sxs-lookup"><span data-stu-id="47df3-136">Most Linux distros automatically manage the content of this file, so usually you can't edit it.</span></span> <span data-ttu-id="47df3-137">Toutefois, vous pouvez remplacer le suffixe à l’aide de la commande *supersede* du client DHCP.</span><span class="sxs-lookup"><span data-stu-id="47df3-137">However, you can override the suffix by using the DHCP client's *supersede* command.</span></span> <span data-ttu-id="47df3-138">Pour ce faire, dans */etc/dhcp/dhclient.conf*, ajoutez :</span><span class="sxs-lookup"><span data-stu-id="47df3-138">To do this, in */etc/dhcp/dhclient.conf*, add:</span></span>

        supersede domain-name <required-dns-suffix>;

