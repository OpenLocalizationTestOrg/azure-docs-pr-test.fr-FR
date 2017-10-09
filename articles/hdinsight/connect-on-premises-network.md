---
title: "réseau local de tooyour Microsoft aaaConnect HDInsight - Azure HDInsight | Documents Microsoft"
description: "Découvrez comment toocreate un HDInsight de cluster dans un réseau virtuel Azure et connectez-la tooyour sur réseau local. Découvrez comment tooconfigure la résolution de noms entre HDInsight et votre réseau local à l’aide d’un serveur DNS personnalisé."
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: larryfr
ms.openlocfilehash: 8a3adf0e3df7726d8e6566d723700506baaf89a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-hdinsight-tooyour-on-premise-network"></a><span data-ttu-id="c933a-104">Connexion réseau locale de tooyour HDInsight</span><span class="sxs-lookup"><span data-stu-id="c933a-104">Connect HDInsight tooyour on-premise network</span></span>

<span data-ttu-id="c933a-105">Découvrez comment tooconnect HDInsight tooyour local réseau à l’aide de réseaux virtuels Azure et une passerelle VPN.</span><span class="sxs-lookup"><span data-stu-id="c933a-105">Learn how tooconnect HDInsight tooyour on-premises network by using Azure Virtual Networks and a VPN gateway.</span></span> <span data-ttu-id="c933a-106">Ce document fournit des informations de planification concernant :</span><span class="sxs-lookup"><span data-stu-id="c933a-106">This document provides planning information on:</span></span>

* <span data-ttu-id="c933a-107">À l’aide de HDInsight dans un réseau virtuel Azure qui se connecte tooyour sur site réseau.</span><span class="sxs-lookup"><span data-stu-id="c933a-107">Using HDInsight in an Azure Virtual Network that connects tooyour on-premises network.</span></span>

* <span data-ttu-id="c933a-108">Configuration de la résolution de nom DNS entre le réseau virtuel de hello et votre réseau local.</span><span class="sxs-lookup"><span data-stu-id="c933a-108">Configuring DNS name resolution between hello virtual network and your on-premises network.</span></span>

* <span data-ttu-id="c933a-109">Configuration réseau sécurité groupes toorestrict internet access tooHDInsight.</span><span class="sxs-lookup"><span data-stu-id="c933a-109">Configuring network security groups toorestrict internet access tooHDInsight.</span></span>

* <span data-ttu-id="c933a-110">Ports fournis par HDInsight sur un réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="c933a-110">Ports provided by HDInsight on hello virtual network.</span></span>

## <a name="create-hello-virtual-network-configuration"></a><span data-ttu-id="c933a-111">Créer la configuration du réseau virtuel hello</span><span class="sxs-lookup"><span data-stu-id="c933a-111">Create hello Virtual network configuration</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c933a-112">Si vous recherchez des instructions étape par étape sur la connexion HDInsight tooyour locale réseau à l’aide d’un réseau virtuel Azure, consultez hello [réseau de se connecter de HDInsight tooyour locale](connect-on-premises-network.md) document.</span><span class="sxs-lookup"><span data-stu-id="c933a-112">If you are looking for step by step guidance on connecting HDInsight tooyour on-premises network using an Azure Virtual Network, see hello [Connect HDInsight tooyour on-premise network](connect-on-premises-network.md) document.</span></span>

<span data-ttu-id="c933a-113">Toolearn les documents suivants de hello utilisation comment toocreate un réseau virtuel Azure qui est connecté tooyour local réseau :</span><span class="sxs-lookup"><span data-stu-id="c933a-113">Use hello following documents toolearn how toocreate an Azure Virtual Network that is connected tooyour on-premises network:</span></span>
    
* [<span data-ttu-id="c933a-114">À l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="c933a-114">Using hello Azure portal</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)

* [<span data-ttu-id="c933a-115">Utilisation de Microsoft Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c933a-115">Using Azure PowerShell</span></span>](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

* [<span data-ttu-id="c933a-116">Utilisation de l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="c933a-116">Using Azure CLI</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli.md)

## <a name="configure-name-resolution"></a><span data-ttu-id="c933a-117">Configurer la résolution de noms</span><span class="sxs-lookup"><span data-stu-id="c933a-117">Configure name resolution</span></span>

<span data-ttu-id="c933a-118">tooallow HDInsight et les ressources dans toocommunicate de réseau hello joint par nom, vous devez effectuer hello suivant des actions :</span><span class="sxs-lookup"><span data-stu-id="c933a-118">tooallow HDInsight and resources in hello joined network toocommunicate by name, you must perform hello following actions:</span></span>

* <span data-ttu-id="c933a-119">Créer un serveur DNS personnalisé Bonjour réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="c933a-119">Create a custom DNS server in hello Azure Virtual Network.</span></span>

* <span data-ttu-id="c933a-120">Configurer hello réseau virtuel toouse hello serveur DNS personnalisé au lieu de la valeur par défaut de hello Azure récursive résolveur.</span><span class="sxs-lookup"><span data-stu-id="c933a-120">Configure hello virtual network toouse hello custom DNS server instead of hello default Azure Recursive Resolver.</span></span>

* <span data-ttu-id="c933a-121">Configurer le transfert entre un serveur DNS personnalisé hello et votre serveur DNS sur local.</span><span class="sxs-lookup"><span data-stu-id="c933a-121">Configure forwarding between hello custom DNS server and your on-premises DNS server.</span></span>

<span data-ttu-id="c933a-122">Cette configuration permet de hello suivant de comportement :</span><span class="sxs-lookup"><span data-stu-id="c933a-122">This configuration enables hello following behavior:</span></span>

* <span data-ttu-id="c933a-123">Les requêtes de noms de domaine complet qui ont le suffixe DNS de hello __pour le réseau virtuel de hello__ sont transférés à un serveur DNS personnalisé toohello.</span><span class="sxs-lookup"><span data-stu-id="c933a-123">Requests for fully qualified domain names that have hello DNS suffix __for hello virtual network__ are forwarded toohello custom DNS server.</span></span> <span data-ttu-id="c933a-124">un serveur DNS personnalisé Hello transfère ensuite ces toohello demandes Azure récursive programme de résolution, qui retourne l’adresse IP de hello.</span><span class="sxs-lookup"><span data-stu-id="c933a-124">hello custom DNS server then forwards these requests toohello Azure Recursive Resolver, which returns hello IP address.</span></span>

* <span data-ttu-id="c933a-125">Toutes les autres demandes sont transférés de serveur DNS de local toohello.</span><span class="sxs-lookup"><span data-stu-id="c933a-125">All other requests are forwarded toohello on-premises DNS server.</span></span> <span data-ttu-id="c933a-126">Y compris les requêtes pour les ressources internet publics tels que microsoft.com sont transférés serveurDNS toohello local pour la résolution de nom.</span><span class="sxs-lookup"><span data-stu-id="c933a-126">Even requests for public internet resources such as microsoft.com are forwarded toohello on-premises DNS server for name resolution.</span></span>

<span data-ttu-id="c933a-127">Bonjour suivant schéma, lignes vertes sont des requêtes pour les ressources qui se terminent par le suffixe DNS de hello du réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="c933a-127">In hello following diagram, green lines are requests for resources that end in hello DNS suffix of hello virtual network.</span></span> <span data-ttu-id="c933a-128">Lignes bleues sont des requêtes pour les ressources d’un réseau local de hello ou hello internet public.</span><span class="sxs-lookup"><span data-stu-id="c933a-128">Blue lines are requests for resources in hello on-premises network or on hello public internet.</span></span>

![Diagramme de résolution des requêtes DNS dans configuration hello utilisée dans ce document](./media/connect-on-premises-network/on-premises-to-cloud-dns.png)

### <a name="create-a-custom-dns-server"></a><span data-ttu-id="c933a-130">Créer un serveur DNS personnalisé</span><span class="sxs-lookup"><span data-stu-id="c933a-130">Create a custom DNS server</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c933a-131">Vous devez créer et configurer le serveur DNS de hello avant d’installer HDInsight dans le réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="c933a-131">You must create and configure hello DNS server before installing HDInsight into hello virtual network.</span></span>

<span data-ttu-id="c933a-132">toocreate un VM Linux qui utilise hello [lier](https://www.isc.org/downloads/bind/) logiciel DNS, hello utilisation comme suit :</span><span class="sxs-lookup"><span data-stu-id="c933a-132">toocreate a Linux VM that uses hello [Bind](https://www.isc.org/downloads/bind/) DNS software, use hello following steps:</span></span>

> [!NOTE]
> <span data-ttu-id="c933a-133">Hello étapes suivantes utilisent hello [portail Azure](https://portal.azure.com) toocreate une Machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="c933a-133">hello following steps use hello [Azure portal](https://portal.azure.com) toocreate an Azure Virtual Machine.</span></span> <span data-ttu-id="c933a-134">Pour les autres façons toocreate une machine virtuelle, consultez hello [créer un ordinateur virtuel - CLI d’Azure](../virtual-machines/linux/quick-create-cli.md) et [créer un ordinateur virtuel - Azure PowerShell](../virtual-machines/linux/quick-create-portal.md) documents.</span><span class="sxs-lookup"><span data-stu-id="c933a-134">For other ways toocreate a virtual machine, see hello [Create VM - Azure CLI](../virtual-machines/linux/quick-create-cli.md) and [Create VM - Azure PowerShell](../virtual-machines/linux/quick-create-portal.md) documents.</span></span>

1. <span data-ttu-id="c933a-135">À partir de hello [portail Azure](https://portal.azure.com), sélectionnez  __+__ , __de calcul__, et __Ubuntu Server 16.04 LTS__.</span><span class="sxs-lookup"><span data-stu-id="c933a-135">From hello [Azure portal](https://portal.azure.com), select __+__, __Compute__, and __Ubuntu Server 16.04 LTS__.</span></span>

    ![Créer une machine virtuelle Ubuntu](./media/connect-on-premises-network/create-ubuntu-vm.png)

2. <span data-ttu-id="c933a-137">À partir de hello __notions de base__ section, entrez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="c933a-137">From hello __Basics__ section, enter hello following information:</span></span>

    * <span data-ttu-id="c933a-138">__Nom__ : nom convivial identifiant cette machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c933a-138">__Name__: A friendly name that identifies this virtual machine.</span></span> <span data-ttu-id="c933a-139">Par exemple, __DNSProxy__.</span><span class="sxs-lookup"><span data-stu-id="c933a-139">For example, __DNSProxy__.</span></span>
    * <span data-ttu-id="c933a-140">__Nom d’utilisateur__: nom hello Hello SSH compte.</span><span class="sxs-lookup"><span data-stu-id="c933a-140">__User name__: hello name of hello SSH account.</span></span>
    * <span data-ttu-id="c933a-141">__La clé publique SSH__ ou __mot de passe__: hello la méthode d’authentification pour hello SSH compte.</span><span class="sxs-lookup"><span data-stu-id="c933a-141">__SSH public key__ or __Password__: hello authentication method for hello SSH account.</span></span> <span data-ttu-id="c933a-142">Nous recommandons d’utiliser des clés publiques, car elles sont plus sécurisées.</span><span class="sxs-lookup"><span data-stu-id="c933a-142">We recommend using public keys, as they are more secure.</span></span> <span data-ttu-id="c933a-143">Pour plus d’informations, consultez hello [créer et utiliser des clés SSH pour les machines virtuelles Linux](../virtual-machines/linux/mac-create-ssh-keys.md) document.</span><span class="sxs-lookup"><span data-stu-id="c933a-143">For more information, see hello [Create and use SSH keys for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md) document.</span></span>
    * <span data-ttu-id="c933a-144">__Groupe de ressources__: sélectionnez __utiliser l’existante__, puis sélectionnez le groupe de ressources hello contient hello de réseau virtuel créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="c933a-144">__Resource group__: Select __Use existing__, and then select hello resource group that contains hello virtual network created earlier.</span></span>
    * <span data-ttu-id="c933a-145">__Emplacement__: sélectionnez hello même emplacement que le réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="c933a-145">__Location__: Select hello same location as hello virtual network.</span></span>

    ![Configuration de base de machine virtuelle](./media/connect-on-premises-network/vm-basics.png)

    <span data-ttu-id="c933a-147">Conservez les autres entrées de hello valeurs par défaut, puis sélectionnez __OK__.</span><span class="sxs-lookup"><span data-stu-id="c933a-147">Leave other entries at hello default values and then select __OK__.</span></span>

3. <span data-ttu-id="c933a-148">À partir de hello __choisir une taille__ section, la taille de machine virtuelle sélectionnez hello.</span><span class="sxs-lookup"><span data-stu-id="c933a-148">From hello __Choose a size__ section, select hello VM size.</span></span> <span data-ttu-id="c933a-149">Pour ce didacticiel, sélectionnez hello plus petit et plus bas coût option.</span><span class="sxs-lookup"><span data-stu-id="c933a-149">For this tutorial, select hello smallest and lowest cost option.</span></span> <span data-ttu-id="c933a-150">toocontinue, utilisez hello __sélectionnez__ bouton.</span><span class="sxs-lookup"><span data-stu-id="c933a-150">toocontinue, use hello __Select__ button.</span></span>

4. <span data-ttu-id="c933a-151">À partir de hello __paramètres__ section, entrez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="c933a-151">From hello __Settings__ section, enter hello following information:</span></span>

    * <span data-ttu-id="c933a-152">__Réseau virtuel__: sélectionnez hello réseau virtuel que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="c933a-152">__Virtual network__: Select hello virtual network that you created earlier.</span></span>

    * <span data-ttu-id="c933a-153">__Sous-réseau__: sélectionnez le sous-réseau hello par défaut pour le réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="c933a-153">__Subnet__: Select hello default subnet for hello virtual network.</span></span> <span data-ttu-id="c933a-154">Faire __pas__ sélectionnez hello sous-réseau utilisé par la passerelle VPN de hello.</span><span class="sxs-lookup"><span data-stu-id="c933a-154">Do __not__ select hello subnet used by hello VPN gateway.</span></span>

    * <span data-ttu-id="c933a-155">__Compte de stockage des diagnostics__ : sélectionnez ou créez un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="c933a-155">__Diagnostics storage account__: Either select an existing storage account or create a new one.</span></span>

    ![Paramètres de réseau virtuel](./media/connect-on-premises-network/virtual-network-settings.png)

    <span data-ttu-id="c933a-157">Conservez hello autres entrées hello valeur par défaut, puis sélectionnez __OK__ toocontinue.</span><span class="sxs-lookup"><span data-stu-id="c933a-157">Leave hello other entries at hello default value, then select __OK__ toocontinue.</span></span>

5. <span data-ttu-id="c933a-158">À partir de hello __achat__ section, sélectionnez hello __achat__ bouton toocreate hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="c933a-158">From hello __Purchase__ section, select hello __Purchase__ button toocreate hello virtual machine.</span></span>

6. <span data-ttu-id="c933a-159">Une fois que l’ordinateur virtuel de hello a été créé, son __vue d’ensemble__ s’affiche.</span><span class="sxs-lookup"><span data-stu-id="c933a-159">Once hello virtual machine has been created, its __Overview__ section is displayed.</span></span> <span data-ttu-id="c933a-160">Dans la liste hello hello gauche, sélectionnez __propriétés__.</span><span class="sxs-lookup"><span data-stu-id="c933a-160">From hello list on hello left, select __Properties__.</span></span> <span data-ttu-id="c933a-161">Enregistrer hello __adresse IP publique__ et __adresse IP privée__ valeurs.</span><span class="sxs-lookup"><span data-stu-id="c933a-161">Save hello __Public IP address__ and __Private IP address__ values.</span></span> <span data-ttu-id="c933a-162">Il va être utilisé dans la section suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="c933a-162">It will be used in hello next section.</span></span>

    ![Adresses IP publique et privée](./media/connect-on-premises-network/vm-ip-addresses.png)

### <a name="install-and-configure-bind-dns-software"></a><span data-ttu-id="c933a-164">Installer et configurer Bind (logiciel DNS)</span><span class="sxs-lookup"><span data-stu-id="c933a-164">Install and configure Bind (DNS software)</span></span>

1. <span data-ttu-id="c933a-165">Utiliser SSH tooconnect toohello __adresse IP publique__ de machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="c933a-165">Use SSH tooconnect toohello __public IP address__ of hello virtual machine.</span></span> <span data-ttu-id="c933a-166">Bonjour à l’exemple suivant établit une connexion virtuels tooa à 40.68.254.142 :</span><span class="sxs-lookup"><span data-stu-id="c933a-166">hello following example connects tooa virtual machine at 40.68.254.142:</span></span>

    ```bash
    ssh sshuser@40.68.254.142
    ```

    <span data-ttu-id="c933a-167">Remplacez `sshuser` par hello SSH compte d’utilisateur que vous avez spécifié lors de la création du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="c933a-167">Replace `sshuser` with hello SSH user account you specified when creating hello cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c933a-168">Il existe une multitude de hello tooobtain de façons `ssh` utilitaire.</span><span class="sxs-lookup"><span data-stu-id="c933a-168">There are a variety of ways tooobtain hello `ssh` utility.</span></span> <span data-ttu-id="c933a-169">Sur Linux, Unix et macOS, il est fourni en tant que partie du système d’exploitation de hello.</span><span class="sxs-lookup"><span data-stu-id="c933a-169">On Linux, Unix, and macOS, it is provided as part of hello operating system.</span></span> <span data-ttu-id="c933a-170">Si vous utilisez Windows, considérez l’une des options suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="c933a-170">If you are using Windows, consider one of hello following options:</span></span>
    >
    > * [<span data-ttu-id="c933a-171">Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="c933a-171">Azure Cloud Shell</span></span>](../cloud-shell/quickstart.md)
    > * [<span data-ttu-id="c933a-172">Bash sur Ubuntu sur Windows 10</span><span class="sxs-lookup"><span data-stu-id="c933a-172">Bash on Ubuntu on Windows 10</span></span>](https://msdn.microsoft.com/commandline/wsl/about)
    > * [<span data-ttu-id="c933a-173">Git (https://git-scm.com/)</span><span class="sxs-lookup"><span data-stu-id="c933a-173">Git (https://git-scm.com/)</span></span>](https://git-scm.com/)
    > * [<span data-ttu-id="c933a-174">OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)</span><span class="sxs-lookup"><span data-stu-id="c933a-174">OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)</span></span>](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)

2. <span data-ttu-id="c933a-175">tooinstall Bind, utilisez hello suivant les commandes à partir de la session SSH hello :</span><span class="sxs-lookup"><span data-stu-id="c933a-175">tooinstall Bind, use hello following commands from hello SSH session:</span></span>

    ```bash
    sudo apt-get update -y
    sudo apt-get install bind9 -y
    ```

3. <span data-ttu-id="c933a-176">tooconfigure liaison tooforward nom résolution demandes tooyour local serveur DNS, utilisez hello après le texte en tant que contenu hello Hello `/etc/bind/named.conf.options` fichier :</span><span class="sxs-lookup"><span data-stu-id="c933a-176">tooconfigure Bind tooforward name resolution requests tooyour on-prem DNS server, use hello following text as hello contents of hello `/etc/bind/named.conf.options` file:</span></span>

        acl goodclients {
            10.0.0.0/16; # Replace with hello IP address range of hello virtual network
            10.1.0.0/16; # Replace with hello IP address range of hello on-premises network
            localhost;
            localnets;
        };

        options {
                directory "/var/cache/bind";

                recursion yes;

                allow-query { goodclients; };

                forwarders {
                192.168.0.1; # Replace with hello IP address of hello on-premises DNS server
                };

                dnssec-validation auto;

                auth-nxdomain no;    # conform tooRFC1035
                listen-on { any; };
        };

    > [!IMPORTANT]
    > <span data-ttu-id="c933a-177">Remplacez les valeurs de hello en hello `goodclients` section avec une plage d’adresses IP hello du réseau virtuel de hello et réseau local.</span><span class="sxs-lookup"><span data-stu-id="c933a-177">Replace hello values in hello `goodclients` section with hello IP address range of hello virtual network and on-premises network.</span></span> <span data-ttu-id="c933a-178">Cette section définit les adresses hello qui accepte les demandes de ce serveur DNS.</span><span class="sxs-lookup"><span data-stu-id="c933a-178">This section defines hello addresses that this DNS server accepts requests from.</span></span>
    >
    > <span data-ttu-id="c933a-179">Remplacez hello `192.168.0.1` entrée Bonjour `forwarders` section avec l’adresse IP de hello du serveur DNS local.</span><span class="sxs-lookup"><span data-stu-id="c933a-179">Replace hello `192.168.0.1` entry in hello `forwarders` section with hello IP address of your on-premises DNS server.</span></span> <span data-ttu-id="c933a-180">Cette tooyour de demandes DNS entrée itinéraires locaux serveur DNS pour la résolution.</span><span class="sxs-lookup"><span data-stu-id="c933a-180">This entry routes DNS requests tooyour on-premises DNS server for resolution.</span></span>

    <span data-ttu-id="c933a-181">tooedit ce fichier, hello utilisez commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c933a-181">tooedit this file, use hello following command:</span></span>

    ```bash
    sudo nano /etc/bind/named.conf.options
    ```

    <span data-ttu-id="c933a-182">fichier de hello toosave, utilisez __Ctrl + X__, __Y__, puis __entrée__.</span><span class="sxs-lookup"><span data-stu-id="c933a-182">toosave hello file, use __Ctrl+X__, __Y__, and then __Enter__.</span></span>

4. <span data-ttu-id="c933a-183">À partir de la session SSH hello, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c933a-183">From hello SSH session, use hello following command:</span></span>

    ```bash
    hostname -f
    ```

    <span data-ttu-id="c933a-184">Cette commande retourne un toohello similaire valeur suit texte :</span><span class="sxs-lookup"><span data-stu-id="c933a-184">This command returns a value similar toohello following text:</span></span>

        dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net

    <span data-ttu-id="c933a-185">Hello `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` texte est hello __suffixe DNS__ pour ce réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="c933a-185">hello `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` text is hello __DNS suffix__ for this virtual network.</span></span> <span data-ttu-id="c933a-186">Enregistrez cette valeur, car vous l’utiliserez plus tard.</span><span class="sxs-lookup"><span data-stu-id="c933a-186">Save this value, as it is used later.</span></span>

5. <span data-ttu-id="c933a-187">Liaison tooconfigure tooresolve les noms DNS pour les ressources réseau virtuel de hello, utilisez hello après le texte en tant que contenu hello Hello `/etc/bind/named.conf.local` fichier :</span><span class="sxs-lookup"><span data-stu-id="c933a-187">tooconfigure Bind tooresolve DNS names for resources within hello virtual network, use hello following text as hello contents of hello `/etc/bind/named.conf.local` file:</span></span>

        // Replace hello following with hello DNS suffix for your virtual network
        zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
            type forward;
            forwarders {168.63.129.16;}; # hello Azure recursive resolver
        };

    > [!IMPORTANT]
    > <span data-ttu-id="c933a-188">Vous devez remplacer hello `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` avec le suffixe DNS de hello vous extrait précédemment.</span><span class="sxs-lookup"><span data-stu-id="c933a-188">You must replace hello `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` with hello DNS suffix you retrieved earlier.</span></span>

    <span data-ttu-id="c933a-189">tooedit ce fichier, hello utilisez commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c933a-189">tooedit this file, use hello following command:</span></span>

    ```bash
    sudo nano /etc/bind/named.conf.local
    ```

    <span data-ttu-id="c933a-190">fichier de hello toosave, utilisez __Ctrl + X__, __Y__, puis __entrée__.</span><span class="sxs-lookup"><span data-stu-id="c933a-190">toosave hello file, use __Ctrl+X__, __Y__, and then __Enter__.</span></span>

6. <span data-ttu-id="c933a-191">toostart Bind, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c933a-191">toostart Bind, use hello following command:</span></span>

    ```bash
    sudo service bind9 restart
    ```

7. <span data-ttu-id="c933a-192">tooverify lier peut résoudre les noms de hello de ressources de votre réseau local, hello utilisation suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="c933a-192">tooverify that bind can resolve hello names of resources in your on-premises network, use hello following commands:</span></span>

    ```bash
    sudo apt install dnsutils
    nslookup dns.mynetwork.net 10.0.0.4
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="c933a-193">Remplacez `dns.mynetwork.net` avec le nom de domaine complet (FQDN) hello d’une ressource de votre réseau local.</span><span class="sxs-lookup"><span data-stu-id="c933a-193">Replace `dns.mynetwork.net` with hello fully qualified domain name (FQDN) of a resource in your on-premises network.</span></span>
    >
    > <span data-ttu-id="c933a-194">Remplacez `10.0.0.4` avec hello __adresse IP interne__ de votre serveur DNS personnalisé dans le réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="c933a-194">Replace `10.0.0.4` with hello __internal IP address__ of your custom DNS server in hello virtual network.</span></span>

    <span data-ttu-id="c933a-195">réponse de Hello apparaît toohello similaire après le texte :</span><span class="sxs-lookup"><span data-stu-id="c933a-195">hello response appears similar toohello following text:</span></span>

        Server:         10.0.0.4
        Address:        10.0.0.4#53

        Non-authoritative answer:
        Name:   dns.mynetwork.net
        Address: 192.168.0.4

### <a name="configure-hello-virtual-network-toouse-hello-custom-dns-server"></a><span data-ttu-id="c933a-196">Configurer hello réseau virtuel toouse hello serveur DNS personnalisé</span><span class="sxs-lookup"><span data-stu-id="c933a-196">Configure hello virtual network toouse hello custom DNS server</span></span>

<span data-ttu-id="c933a-197">tooconfigure hello réseau virtuel toouse hello serveur DNS personnalisé au lieu de hello Azure récursive, programme de résolution, utiliser hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c933a-197">tooconfigure hello virtual network toouse hello custom DNS server instead of hello Azure recursive resolver, use hello following steps:</span></span>

1. <span data-ttu-id="c933a-198">Bonjour [portail Azure](https://portal.azure.com), sélectionnez le réseau virtuel de hello, puis sélectionnez __serveurs DNS__.</span><span class="sxs-lookup"><span data-stu-id="c933a-198">In hello [Azure portal](https://portal.azure.com), select hello virtual network, and then select __DNS Servers__.</span></span>

2. <span data-ttu-id="c933a-199">Sélectionnez __personnalisé__, puis entrez hello __adresse IP interne__ d’un serveur DNS personnalisé hello.</span><span class="sxs-lookup"><span data-stu-id="c933a-199">Select __Custom__, and enter hello __internal IP address__ of hello custom DNS server.</span></span> <span data-ttu-id="c933a-200">Enfin, sélectionnez __Enregistrer__.</span><span class="sxs-lookup"><span data-stu-id="c933a-200">Finally, select __Save__.</span></span>

    ![Définir un serveur DNS personnalisé hello pour le réseau de hello](./media/connect-on-premises-network/configure-custom-dns.png)

### <a name="configure-hello-on-premises-dns-server"></a><span data-ttu-id="c933a-202">Configurer hello locale DNS server</span><span class="sxs-lookup"><span data-stu-id="c933a-202">Configure hello on-premises DNS server</span></span>

<span data-ttu-id="c933a-203">Dans la section précédente de hello, vous configuré hello personnalisé DNS server tooforward demandes toohello sur serveur DNS local.</span><span class="sxs-lookup"><span data-stu-id="c933a-203">In hello previous section, you configured hello custom DNS server tooforward requests toohello on-premises DNS server.</span></span> <span data-ttu-id="c933a-204">Ensuite, vous devez configurer hello locale DNS tooforward demandes toohello personnalisé serveur DNS.</span><span class="sxs-lookup"><span data-stu-id="c933a-204">Next, you must configure hello on-premises DNS server tooforward requests toohello custom DNS server.</span></span>

<span data-ttu-id="c933a-205">Pour savoir comment tooconfigure votre serveur DNS, consultez la documentation de votre logiciel de serveur DNS hello.</span><span class="sxs-lookup"><span data-stu-id="c933a-205">For specific steps on how tooconfigure your DNS server, consult hello documentation for your DNS server software.</span></span> <span data-ttu-id="c933a-206">Recherchez la procédure hello tooconfigure un __redirecteur conditionnel__.</span><span class="sxs-lookup"><span data-stu-id="c933a-206">Look for hello steps on how tooconfigure a __conditional forwarder__.</span></span>

<span data-ttu-id="c933a-207">Un redirecteur conditionnel transfère uniquement les demandes relatives à un suffixe DNS spécifique.</span><span class="sxs-lookup"><span data-stu-id="c933a-207">A conditional forward only forwards requests for a specific DNS suffix.</span></span> <span data-ttu-id="c933a-208">Dans ce cas, vous devez configurer un redirecteur le suffixe DNS du réseau virtuel de hello hello.</span><span class="sxs-lookup"><span data-stu-id="c933a-208">In this case, you must configure a forwarder for hello DNS suffix of hello virtual network.</span></span> <span data-ttu-id="c933a-209">Demandes de ce suffixe doivent être transférés à adresse IP de toohello d’un serveur DNS personnalisé hello.</span><span class="sxs-lookup"><span data-stu-id="c933a-209">Requests for this suffix should be forwarded toohello IP address of hello custom DNS server.</span></span> 

<span data-ttu-id="c933a-210">Hello texte suivant est un exemple de configuration de redirecteur conditionnel pour hello **lier** logiciel DNS :</span><span class="sxs-lookup"><span data-stu-id="c933a-210">hello following text is an example of a conditional forwarder configuration for hello **Bind** DNS software:</span></span>

    zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # hello custom DNS server's internal IP address
    };

<span data-ttu-id="c933a-211">Pour plus d’informations sur l’utilisation de DNS sur **Windows Server 2016**, consultez hello [Add-DnsServerConditionalForwarderZone](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone) documentation...</span><span class="sxs-lookup"><span data-stu-id="c933a-211">For information on using DNS on **Windows Server 2016**, see hello [Add-DnsServerConditionalForwarderZone](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone) documentation...</span></span>

<span data-ttu-id="c933a-212">Une fois que vous avez configuré le serveur DNS de local hello, vous pouvez utiliser `nslookup` de tooverify de réseau local hello que vous pouvez résoudre les noms dans le réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="c933a-212">Once you have configured hello on-premises DNS server, you can use `nslookup` from hello on-premises network tooverify that you can resolve names in hello virtual network.</span></span> <span data-ttu-id="c933a-213">l’exemple suivant de Hello</span><span class="sxs-lookup"><span data-stu-id="c933a-213">hello following example</span></span> 

```bash
nslookup dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net 196.168.0.4
```

<span data-ttu-id="c933a-214">Cet exemple utilise hello serveur DNS local 196.168.0.4 nom de hello tooresolve d’un serveur DNS personnalisé hello.</span><span class="sxs-lookup"><span data-stu-id="c933a-214">This example uses hello on-premises DNS server at 196.168.0.4 tooresolve hello name of hello custom DNS server.</span></span> <span data-ttu-id="c933a-215">Remplacez adresse hello hello un pour le serveur DNS de local hello.</span><span class="sxs-lookup"><span data-stu-id="c933a-215">Replace hello IP address with hello one for hello on-premises DNS server.</span></span> <span data-ttu-id="c933a-216">Remplacez hello `dnsproxy` adresse avec le nom de domaine complet de hello du serveur DNS personnalisé de hello.</span><span class="sxs-lookup"><span data-stu-id="c933a-216">Replace hello `dnsproxy` address with hello fully qualified domain name of hello custom DNS server.</span></span>

## <a name="optional-control-network-traffic"></a><span data-ttu-id="c933a-217">Facultatif : contrôler le trafic réseau</span><span class="sxs-lookup"><span data-stu-id="c933a-217">Optional: Control network traffic</span></span>

<span data-ttu-id="c933a-218">Vous pouvez utiliser des groupes de sécurité réseau (NSG) ou le trafic réseau de toocontrol itinéraires définis par l’utilisateur (UDR).</span><span class="sxs-lookup"><span data-stu-id="c933a-218">You can use network security groups (NSG) or user-defined routes (UDR) toocontrol network traffic.</span></span> <span data-ttu-id="c933a-219">Groupes de sécurité réseau permettent de toofilter entrant et sortant du trafic et autoriser ou refuser le trafic de hello.</span><span class="sxs-lookup"><span data-stu-id="c933a-219">NSGs allow you toofilter inbound and outbound traffic, and allow or deny hello traffic.</span></span> <span data-ttu-id="c933a-220">UDRs vous toocontrol le flux de trafic entre les ressources de réseau virtuel de hello, hello internet et hello réseau local.</span><span class="sxs-lookup"><span data-stu-id="c933a-220">UDRs allow you toocontrol how traffic flows between resources in hello virtual network, hello internet, and hello on-premises network.</span></span>

> [!WARNING]
> <span data-ttu-id="c933a-221">HDInsight requiert un accès entrant à partir d’adresses IP spécifiques Bonjour Azure cloud et un accès sortant non restreint.</span><span class="sxs-lookup"><span data-stu-id="c933a-221">HDInsight requires inbound access from specific IP addresses in hello Azure cloud, and unrestricted outbound access.</span></span> <span data-ttu-id="c933a-222">Lorsque vous utilisez des groupes de sécurité réseau ou UDRs toocontrol du trafic, vous devez effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c933a-222">When using NSGs or UDRs toocontrol traffic, you must perform hello following steps:</span></span>
>
> 1. <span data-ttu-id="c933a-223">Recherche des adresses IP hello pour l’emplacement hello qui contient votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="c933a-223">Find hello IP addresses for hello location that contains your virtual network.</span></span> <span data-ttu-id="c933a-224">Pour obtenir la liste des adresses IP requises par emplacement, consultez [Adresses IP requises](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip).</span><span class="sxs-lookup"><span data-stu-id="c933a-224">For a list of required IPs by location, see [Required IP addresses](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip).</span></span>
>
> 2. <span data-ttu-id="c933a-225">Autoriser le trafic entrant à partir d’adresses IP de hello.</span><span class="sxs-lookup"><span data-stu-id="c933a-225">Allow inbound traffic from hello IP addresses.</span></span>
>
>    * <span data-ttu-id="c933a-226">__Groupe de sécurité réseau__: autoriser __entrant__ le trafic sur le port __443__ de hello __Internet__.</span><span class="sxs-lookup"><span data-stu-id="c933a-226">__NSG__: Allow __inbound__ traffic on port __443__ from hello __Internet__.</span></span>
>    * <span data-ttu-id="c933a-227">__UDR__: ensemble hello __tronçon suivant__ type de hello itinéraire too__Internet__.</span><span class="sxs-lookup"><span data-stu-id="c933a-227">__UDR__: Set hello __Next Hop__ type of hello route too__Internet__.</span></span>

<span data-ttu-id="c933a-228">Pour obtenir un exemple d’utilisation de Azure PowerShell ou hello CLI d’Azure toocreate groupes de sécurité réseau, consultez hello [HDInsight d’étendre les réseaux virtuels Azure](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg) document.</span><span class="sxs-lookup"><span data-stu-id="c933a-228">For an example of using Azure PowerShell or hello Azure CLI toocreate NSGs, see hello [Extend HDInsight with Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg) document.</span></span>

## <a name="create-hello-hdinsight-cluster"></a><span data-ttu-id="c933a-229">Créer le cluster HDInsight de hello</span><span class="sxs-lookup"><span data-stu-id="c933a-229">Create hello HDInsight cluster</span></span>

> [!WARNING]
> <span data-ttu-id="c933a-230">Vous devez configurer un serveur DNS personnalisé hello avant d’installer HDInsight dans le réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="c933a-230">You must configure hello custom DNS server before installing HDInsight in hello virtual network.</span></span>

<span data-ttu-id="c933a-231">Hello d’utiliser les étapes Bonjour [créer un cluster HDInsight à l’aide de hello portail Azure](./hdinsight-hadoop-create-linux-clusters-portal.md) document toocreate un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c933a-231">Use hello steps in hello [Create an HDInsight cluster using hello Azure portal](./hdinsight-hadoop-create-linux-clusters-portal.md) document toocreate an HDInsight cluster.</span></span>

> [!WARNING]
> * <span data-ttu-id="c933a-232">Lors de la création du cluster, vous devez choisir l’emplacement hello qui contient votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="c933a-232">During cluster creation, you must choose hello location that contains your virtual network.</span></span>
>
> * <span data-ttu-id="c933a-233">Bonjour __paramètres avancés__ partie de la configuration, vous devez sélectionner le réseau virtuel de hello et sous-réseau que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="c933a-233">In hello __Advanced settings__ part of configuration, you must select hello virtual network and subnet that you created earlier.</span></span>

## <a name="connecting-toohdinsight"></a><span data-ttu-id="c933a-234">Connexion tooHDInsight</span><span class="sxs-lookup"><span data-stu-id="c933a-234">Connecting tooHDInsight</span></span>

<span data-ttu-id="c933a-235">La plupart des documentation sur HDInsight suppose que vous avez des cluster toohello d’accès sur hello internet.</span><span class="sxs-lookup"><span data-stu-id="c933a-235">Most documentation on HDInsight assumes that you have access toohello cluster over hello internet.</span></span> <span data-ttu-id="c933a-236">Par exemple, que vous pouvez vous connecter à cluster toohello à https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="c933a-236">For example, that you can connect toohello cluster at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="c933a-237">Cette adresse utilise la passerelle publique hello, qui n’est pas disponible si vous avez utilisé des groupes de sécurité réseau ou d’accès toorestrict UDRs hello internet.</span><span class="sxs-lookup"><span data-stu-id="c933a-237">This address uses hello public gateway, which is not available if you have used NSGs or UDRs toorestrict access from hello internet.</span></span>

<span data-ttu-id="c933a-238">toodirectly connecter tooHDInsight via le réseau virtuel de hello, utilisez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c933a-238">toodirectly connect tooHDInsight through hello virtual network, use hello following steps:</span></span>

1. <span data-ttu-id="c933a-239">noms de domaine complet interne toodiscover hello hello HDInsight des nœuds de cluster, utilisez une des méthodes suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="c933a-239">toodiscover hello internal fully qualified domain names of hello HDInsight cluster nodes, use one of hello following methods:</span></span>

    ```powershell
    $resourceGroupName = "hello resource group that contains hello virtual network used with HDInsight"

    $clusterNICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName | where-object {$_.Name -like "*node*"}

    $nodes = @()
    foreach($nic in $clusterNICs) {
        $node = new-object System.Object
        $node | add-member -MemberType NoteProperty -name "Type" -value $nic.Name.Split('-')[1]
        $node | add-member -MemberType NoteProperty -name "InternalIP" -value $nic.IpConfigurations.PrivateIpAddress
        $node | add-member -MemberType NoteProperty -name "InternalFQDN" -value $nic.DnsSettings.InternalFqdn
        $nodes += $node
    }
    $nodes | sort-object Type
    ```

    ```azurecli
    az network nic list --resource-group <resourcegroupname> --output table --query "[?contains(name,'node')].{NICname:name,InternalIP:ipConfigurations[0].privateIpAddress,InternalFQDN:dnsSettings.internalFqdn}"
    ```

2. <span data-ttu-id="c933a-240">toodetermine hello port un service disponible, consultez hello [Ports utilisés par les services de Hadoop dans HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.</span><span class="sxs-lookup"><span data-stu-id="c933a-240">toodetermine hello port that a service is available on, see hello [Ports used by Hadoop services on HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="c933a-241">Certains services hébergés sur les nœuds principaux hello sont uniquement actifs sur un seul nœud à la fois.</span><span class="sxs-lookup"><span data-stu-id="c933a-241">Some services hosted on hello head nodes are only active on one node at a time.</span></span> <span data-ttu-id="c933a-242">Si vous essayez d’accéder à un service sur un seul nœud principal et il échoue, basculez toohello autre nœud principal.</span><span class="sxs-lookup"><span data-stu-id="c933a-242">If you try accessing a service on one head node and it fails, switch toohello other head node.</span></span>
    >
    > <span data-ttu-id="c933a-243">Par exemple, Ambari n’est actif que sur un nœud principal à la fois.</span><span class="sxs-lookup"><span data-stu-id="c933a-243">For example, Ambari is only active on one head node at a time.</span></span> <span data-ttu-id="c933a-244">Si vous essayez d’accéder à Ambari sur un seul nœud principal et retourne une erreur 404, puis elle s’exécute sur hello autre nœud principal.</span><span class="sxs-lookup"><span data-stu-id="c933a-244">If you try accessing Ambari on one head node and it returns a 404 error, then it is running on hello other head node.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c933a-245">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c933a-245">Next steps</span></span>

* <span data-ttu-id="c933a-246">Pour plus d’informations sur l’utilisation de HDInsight dans un réseau virtuel, consultez [Étendre HDInsight à l’aide de réseaux virtuels Azure](./hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="c933a-246">For more information on using HDInsight in a virtual network, see [Extend HDInsight by using Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md).</span></span>

* <span data-ttu-id="c933a-247">Pour plus d’informations sur les réseaux virtuels Azure, consultez hello [vue d’ensemble du réseau virtuel Azure](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c933a-247">For more information on Azure virtual networks, see hello [Azure Virtual Network overview](../virtual-network/virtual-networks-overview.md).</span></span>

* <span data-ttu-id="c933a-248">Pour plus d’informations sur les groupes de sécurité réseau, consultez [Groupes de sécurité réseau](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="c933a-248">For more information on network security groups, see [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="c933a-249">Pour plus d’informations sur les routages par l’utilisateur, consultez [Routage définis par l’utilisateur et transfert IP](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c933a-249">For more information on user-defined routes, see [USer-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>
