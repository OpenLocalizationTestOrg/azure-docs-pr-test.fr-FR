---
title: aaaConnect tooa Machine virtuelle de SQL Server (Gestionnaire de ressources) | Documents Microsoft
description: "Découvrez comment tooconnect tooSQL Server en cours d’exécution sur un ordinateur virtuel dans Azure. Cette rubrique utilise le modèle de déploiement classique hello. scénarios de Hello diffèrent en fonction de la configuration du réseau hello et l’emplacement de hello du client de hello."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-resource-manager
ms.assetid: aa5bf144-37a3-4781-892d-e0e300913d03
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/14/2017
ms.author: jroth
ms.openlocfilehash: 7b127c14c37b9a72c19ed17f8b1dad61c7bc2d38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-sql-server-virtual-machine-on-azure-resource-manager"></a><span data-ttu-id="babf2-105">Se connecter tooa Machine virtuelle de SQL Server sur Azure (Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="babf2-105">Connect tooa SQL Server Virtual Machine on Azure (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="babf2-106">Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="babf2-106">Resource Manager</span></span>](virtual-machines-windows-sql-connect.md)
> * [<span data-ttu-id="babf2-107">Classique</span><span class="sxs-lookup"><span data-stu-id="babf2-107">Classic</span></span>](../classic/sql-connect.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="babf2-108">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="babf2-108">Overview</span></span>

<span data-ttu-id="babf2-109">Cette rubrique décrit comment tooconnect tooyour SQL Server de l’instance en cours d’exécution sur une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="babf2-109">This topic describes how tooconnect tooyour SQL Server instance running on an Azure virtual machine.</span></span> <span data-ttu-id="babf2-110">Elle aborde certains [scénarios de connectivité générale](#connection-scenarios) et fournit une [procédure détaillée pour configurer la connectivité à SQL Server dans une machine virtuelle Azure](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="babf2-110">It covers some [general connectivity scenarios](#connection-scenarios) and then provides [detailed steps for configuring SQL Server connectivity in an Azure VM](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="babf2-111">Si vous préférez suivre une procédure pas-à-pas complète d’approvisionnement et de connectivité, voir [Approvisionnement d’une machine virtuelle SQL Server dans Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="babf2-111">If you would rather have a full walk-through of both provisioning and connectivity, see [Provisioning a SQL Server Virtual Machine on Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

## <a name="connection-scenarios"></a><span data-ttu-id="babf2-112">Scénarios de connexion</span><span class="sxs-lookup"><span data-stu-id="babf2-112">Connection scenarios</span></span>

<span data-ttu-id="babf2-113">moyen de Hello un client connecte tooSQL Server s’exécutant sur un ordinateur virtuel diffère selon l’emplacement de hello du client de hello et configuration de réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="babf2-113">hello way a client connects tooSQL Server running on a Virtual Machine differs depending on hello location of hello client and hello networking configuration.</span></span>

<span data-ttu-id="babf2-114">Si vous configurez un ordinateur virtuel SQL Server Bonjour portail Azure, vous pouvez hello de spécification de type hello de **connectivité SQL**.</span><span class="sxs-lookup"><span data-stu-id="babf2-114">If you provision a SQL Server VM in hello Azure portal, you have hello option of specifying hello type of **SQL connectivity**.</span></span>

![Option de connectivité SQL publique lors de l’approvisionnement](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity.png)

<span data-ttu-id="babf2-116">Les options de connectivité sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="babf2-116">Your options for connectivity include:</span></span>

| <span data-ttu-id="babf2-117">Option</span><span class="sxs-lookup"><span data-stu-id="babf2-117">Option</span></span> | <span data-ttu-id="babf2-118">Description</span><span class="sxs-lookup"><span data-stu-id="babf2-118">Description</span></span> |
|---|---|
| <span data-ttu-id="babf2-119">**Public**</span><span class="sxs-lookup"><span data-stu-id="babf2-119">**Public**</span></span> | <span data-ttu-id="babf2-120">Se connecter tooSQL Server sur hello internet</span><span class="sxs-lookup"><span data-stu-id="babf2-120">Connect tooSQL Server over hello internet</span></span> |
| <span data-ttu-id="babf2-121">**Privé**</span><span class="sxs-lookup"><span data-stu-id="babf2-121">**Private**</span></span> | <span data-ttu-id="babf2-122">Se connecter tooSQL Server Bonjour même réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="babf2-122">Connect tooSQL Server in hello same virtual network</span></span> |
| <span data-ttu-id="babf2-123">**Local**</span><span class="sxs-lookup"><span data-stu-id="babf2-123">**Local**</span></span> | <span data-ttu-id="babf2-124">Se connecter tooSQL Server localement sur hello même machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="babf2-124">Connect tooSQL Server locally on hello same virtual machine</span></span> | 

<span data-ttu-id="babf2-125">Hello sections suivantes expliquent hello **Public** et **privé** options plus en détail.</span><span class="sxs-lookup"><span data-stu-id="babf2-125">hello following sections explain hello **Public** and **Private** options in more detail.</span></span>

## <a name="connect-toosql-server-over-hello-internet"></a><span data-ttu-id="babf2-126">Se connecter tooSQL Server sur hello Internet</span><span class="sxs-lookup"><span data-stu-id="babf2-126">Connect tooSQL Server over hello Internet</span></span>

<span data-ttu-id="babf2-127">Si vous souhaitez que le moteur de base de données SQL Server tooconnect tooyour de hello Internet, sélectionnez **Public** pour hello **connectivité SQL** type dans le portail hello lors de la configuration.</span><span class="sxs-lookup"><span data-stu-id="babf2-127">If you want tooconnect tooyour SQL Server database engine from hello Internet, select **Public** for hello **SQL connectivity** type in hello portal during provisioning.</span></span> <span data-ttu-id="babf2-128">portail de Hello automatiquement hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="babf2-128">hello portal automatically does hello following steps:</span></span>

* <span data-ttu-id="babf2-129">Active le protocole TCP/IP hello pour SQL Server.</span><span class="sxs-lookup"><span data-stu-id="babf2-129">Enables hello TCP/IP protocol for SQL Server.</span></span>
* <span data-ttu-id="babf2-130">Configure un Bonjour de tooopen de règle de pare-feu le port TCP du serveur SQL (1433 par défaut).</span><span class="sxs-lookup"><span data-stu-id="babf2-130">Configures a firewall rule tooopen hello SQL Server TCP port (default 1433).</span></span>
* <span data-ttu-id="babf2-131">Il active l’authentification SQL Server, requis pour l’accès public.</span><span class="sxs-lookup"><span data-stu-id="babf2-131">Enables SQL Server Authentication, required for public access.</span></span>
* <span data-ttu-id="babf2-132">Configure un groupe de sécurité réseau hello sur hello VM tooall TCP le trafic sur hello port SQL Server.</span><span class="sxs-lookup"><span data-stu-id="babf2-132">Configures hello network security group on hello VM tooall TCP traffic on hello SQL Server port.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="babf2-133">les éditions Express et les images de machine virtuelle Hello pourquoi SQL Server Developer n’activent pas automatiquement de protocole de hello TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="babf2-133">hello virtual machine images for hello SQL Server Developer and Express editions do not automatically enable hello TCP/IP protocol.</span></span> <span data-ttu-id="babf2-134">Pour les éditions développeur et Express, vous devez utiliser le Gestionnaire de Configuration SQL Server trop[activer manuellement le protocole de hello TCP/IP](#manualtcp) après la création d’hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="babf2-134">For Developer and Express editions, you must use SQL Server Configuration Manager too[manually enable hello TCP/IP protocol](#manualtcp) after creating hello VM.</span></span>

<span data-ttu-id="babf2-135">N’importe quel client ayant accès à internet peut se connecter à instance de SQL Server toohello en spécifiant hello adresse IP publique de machine virtuelle de hello ou n’importe quel nom DNS adresse IP de toothat.</span><span class="sxs-lookup"><span data-stu-id="babf2-135">Any client with internet access can connect toohello SQL Server instance by specifying either hello public IP address of hello virtual machine or any DNS label assigned toothat IP address.</span></span> <span data-ttu-id="babf2-136">Si hello port SQL Server est 1433, vous n’avez pas besoin de toospecify dans la chaîne de connexion hello.</span><span class="sxs-lookup"><span data-stu-id="babf2-136">If hello SQL Server port is 1433, you do not need toospecify it in hello connection string.</span></span> <span data-ttu-id="babf2-137">Hello suivant de chaîne de connexion connecte tooa SQL VM avec un nom DNS de `sqlvmlabel.eastus.cloudapp.azure.com` à l’aide de l’authentification SQL (vous pouvez utiliser également l’adresse IP publique de hello).</span><span class="sxs-lookup"><span data-stu-id="babf2-137">hello following connection string connects tooa SQL VM with a DNS label of `sqlvmlabel.eastus.cloudapp.azure.com` using SQL Authentication (you could also use hello public IP address).</span></span>

```
Server=sqlvmlabel.eastus.cloudapp.azure.com;Integrated Security=false;User ID=<login_name>;Password=<your_password>
```

<span data-ttu-id="babf2-138">Bien que cela permet la connectivité pour les clients sur internet de hello, cela ne signifie pas que tout le monde peut se connecter tooyour SQL Server.</span><span class="sxs-lookup"><span data-stu-id="babf2-138">Although this enables connectivity for clients over hello internet, this does not imply that anyone can connect tooyour SQL Server.</span></span> <span data-ttu-id="babf2-139">Clients externes ont le mot de passe et le nom d’utilisateur correct de toohello.</span><span class="sxs-lookup"><span data-stu-id="babf2-139">Outside clients have toohello correct username and password.</span></span> <span data-ttu-id="babf2-140">Toutefois, pour renforcer la sécurité, vous pouvez éviter le port connu hello 1433.</span><span class="sxs-lookup"><span data-stu-id="babf2-140">However, for additional security, you can avoid hello well-known port 1433.</span></span> <span data-ttu-id="babf2-141">Par exemple, si vous avez configuré toolisten de SQL Server sur le port 1500 et établi de pare-feu appropriés et règles de groupe de sécurité réseau, vous pouvez connecter en ajoutant le nom du serveur hello port numéro toohello.</span><span class="sxs-lookup"><span data-stu-id="babf2-141">For example, if you configured SQL Server toolisten on port 1500 and established proper firewall and network security group rules, you could connect by appending hello port number toohello Server name.</span></span> <span data-ttu-id="babf2-142">Hello exemple suivant modifie hello précédent en ajoutant un numéro de port personnalisé, **1500**, nom du serveur toohello :</span><span class="sxs-lookup"><span data-stu-id="babf2-142">hello following example alters hello previous one by adding a custom port number, **1500**, toohello server name:</span></span>

```
Server=sqlvmlabel.eastus.cloudapp.azure.com,1500;Integrated Security=false;User ID=<login_name>;Password=<your_password>"
```

> [!NOTE]
> <span data-ttu-id="babf2-143">Lorsque vous interrogez SQL Server dans une machine virtuelle sur hello internet, toutes les données sortantes à partir de hello Azure datacenter est sujet toonormal [tarification des transferts de données sortantes](https://azure.microsoft.com/pricing/details/data-transfers/).</span><span class="sxs-lookup"><span data-stu-id="babf2-143">When you query SQL Server in a VM over hello internet, all outgoing data from hello Azure datacenter is subject toonormal [pricing on outbound data transfers](https://azure.microsoft.com/pricing/details/data-transfers/).</span></span>

## <a name="connect-toosql-server-within-a-virtual-network"></a><span data-ttu-id="babf2-144">Se connecter tooSQL Server dans un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="babf2-144">Connect tooSQL Server within a virtual network</span></span>

<span data-ttu-id="babf2-145">Lorsque vous choisissez **privé** pour hello **connectivité SQL** type dans le portail hello, Azure configure la plupart des paramètres hello identiques trop**Public**.</span><span class="sxs-lookup"><span data-stu-id="babf2-145">When you choose **Private** for hello **SQL connectivity** type in hello portal, Azure configures most of hello settings identical too**Public**.</span></span> <span data-ttu-id="babf2-146">Hello une différence est qu’il n’y a aucune tooallow de règle de groupe de sécurité réseau à l’extérieur du trafic sur le port de SQL Server hello (1433 par défaut).</span><span class="sxs-lookup"><span data-stu-id="babf2-146">hello one difference is that there is no network security group rule tooallow outside traffic on hello SQL Server port (default 1433).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="babf2-147">les éditions Express et les images de machine virtuelle Hello pourquoi SQL Server Developer n’activent pas automatiquement de protocole de hello TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="babf2-147">hello virtual machine images for hello SQL Server Developer and Express editions do not automatically enable hello TCP/IP protocol.</span></span> <span data-ttu-id="babf2-148">Pour les éditions développeur et Express, vous devez utiliser le Gestionnaire de Configuration SQL Server trop[activer manuellement le protocole de hello TCP/IP](#manualtcp) après la création d’hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="babf2-148">For Developer and Express editions, you must use SQL Server Configuration Manager too[manually enable hello TCP/IP protocol](#manualtcp) after creating hello VM.</span></span>

<span data-ttu-id="babf2-149">La connectivité privée est souvent utilisée conjointement avec [Réseau virtuel](../../../virtual-network/virtual-networks-overview.md) et permet plusieurs scénarios.</span><span class="sxs-lookup"><span data-stu-id="babf2-149">Private connectivity is often used in conjunction with [Virtual Network](../../../virtual-network/virtual-networks-overview.md), which enables several scenarios.</span></span> <span data-ttu-id="babf2-150">Vous pouvez connecter des machines virtuelles dans le même réseau virtuel, même si ces ordinateurs virtuels existent dans différents groupes de ressources de hello.</span><span class="sxs-lookup"><span data-stu-id="babf2-150">You can connect VMs in hello same virtual network, even if those VMs exist in different resource groups.</span></span> <span data-ttu-id="babf2-151">De plus, un [VPN de site à site](../../../vpn-gateway/vpn-gateway-site-to-site-create.md)permet de créer une architecture hybride qui connecte les machines virtuelles aux machines et réseaux locaux.</span><span class="sxs-lookup"><span data-stu-id="babf2-151">And with a [site-to-site VPN](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), you can create a hybrid architecture that connects VMs with on-premises networks and machines.</span></span>

<span data-ttu-id="babf2-152">Réseaux virtuels également activer vous toojoin votre domaine tooa de machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="babf2-152">Virtual networks also enable     you toojoin your Azure VMs tooa domain.</span></span> <span data-ttu-id="babf2-153">Il s’agit de hello seule façon toouse l’authentification Windows tooSQL Server.</span><span class="sxs-lookup"><span data-stu-id="babf2-153">This is hello only way toouse Windows Authentication tooSQL Server.</span></span> <span data-ttu-id="babf2-154">Hello autres scénarios de connexion requièrent l’authentification SQL avec des noms d’utilisateur et mots de passe.</span><span class="sxs-lookup"><span data-stu-id="babf2-154">hello other connection scenarios require SQL Authentication with user names and passwords.</span></span>

<span data-ttu-id="babf2-155">En supposant que vous avez configuré DNS dans votre réseau virtuel, vous pouvez connecter l’instance de SQL Server tooyour en spécifiant le nom de l’ordinateur hello machine virtuelle SQL Server dans la chaîne de connexion hello.</span><span class="sxs-lookup"><span data-stu-id="babf2-155">Assuming that you have configured DNS in your virtual network, you can connect tooyour SQL Server instance by specifying hello SQL Server VM computer name in hello connection string.</span></span> <span data-ttu-id="babf2-156">Hello également des exemple suivant suppose que l’authentification Windows a été également configurée et que l’utilisateur hello a reçu l’instance de SQL Server toohello access.</span><span class="sxs-lookup"><span data-stu-id="babf2-156">hello following example also assumes that Windows Authentication has also been configured and that hello user has been granted access toohello SQL Server instance.</span></span>

```
Server=mysqlvm;Integrated Security=true
```

## <span data-ttu-id="babf2-157"><a id="change"></a>Modifier les paramètres de connectivité SQL</span><span class="sxs-lookup"><span data-stu-id="babf2-157"><a id="change"></a> Change SQL connectivity settings</span></span>

<span data-ttu-id="babf2-158">Vous pouvez modifier les paramètres de connectivité hello pour votre machine virtuelle de SQL Server dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="babf2-158">You can change hello connectivity settings for your SQL Server virtual machine in hello Azure portal.</span></span>

1. <span data-ttu-id="babf2-159">Bonjour portail Azure, sélectionnez **virtuels**.</span><span class="sxs-lookup"><span data-stu-id="babf2-159">In hello Azure portal, select **Virtual Machines**.</span></span>

2. <span data-ttu-id="babf2-160">Sélectionnez votre machine virtuelle SQL Server.</span><span class="sxs-lookup"><span data-stu-id="babf2-160">Select your SQL Server VM.</span></span>

3. <span data-ttu-id="babf2-161">Sous **paramètres**, cliquez sur **Configuration de SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="babf2-161">Under **Settings**, click **SQL Server configuration**.</span></span>

4. <span data-ttu-id="babf2-162">Hello de modification **le niveau de connectivité SQL** tooyour requis définition.</span><span class="sxs-lookup"><span data-stu-id="babf2-162">Change hello **SQL connectivity level** tooyour required setting.</span></span> <span data-ttu-id="babf2-163">Vous pouvez éventuellement utiliser cette hello toochange de zone port SQL Server ou les paramètres de l’authentification SQL hello.</span><span class="sxs-lookup"><span data-stu-id="babf2-163">You can optionally use this area toochange hello SQL Server port or hello SQL Authentication settings.</span></span>

   ![Modifier la connectivité SQL](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity-change.png)

5. <span data-ttu-id="babf2-165">Attendez quelques minutes pour toocomplete de mise à jour hello.</span><span class="sxs-lookup"><span data-stu-id="babf2-165">Wait several minutes for hello update toocomplete.</span></span>

   ![Notification de mise à jour de la machine virtuelle SQL](./media/virtual-machines-windows-sql-connect/sql-vm-updating-notification.png)

## <span data-ttu-id="babf2-167"><a id="manualtcp"></a> Activer le protocole TCP/IP pour les éditions Developer et Express</span><span class="sxs-lookup"><span data-stu-id="babf2-167"><a id="manualtcp"></a> Enable TCP/IP for Developer and Express editions</span></span>

<span data-ttu-id="babf2-168">Lorsque vous modifiez les paramètres de connectivité de SQL Server, Azure n’active pas automatiquement le protocole de hello TCP/IP pour les éditions Express et SQL Server Developer.</span><span class="sxs-lookup"><span data-stu-id="babf2-168">When changing SQL Server connectivity settings, Azure does not automatically enable hello TCP/IP protocol for SQL Server Developer and Express editions.</span></span> <span data-ttu-id="babf2-169">les étapes de Hello ci-dessous expliquent comment toomanually activer TCP/IP afin de pouvoir vous connecter à distance par adresse IP.</span><span class="sxs-lookup"><span data-stu-id="babf2-169">hello steps below explain how toomanually enable TCP/IP so that you can connect remotely by IP address.</span></span>

<span data-ttu-id="babf2-170">Tout d’abord, connectez toohello l’ordinateur SQL Server avec le Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="babf2-170">First, connect toohello SQL Server machine with remote desktop.</span></span>

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-remote-desktop-connect.md)]

<span data-ttu-id="babf2-171">Ensuite, activez le protocole TCP/IP de hello avec **Gestionnaire de Configuration SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="babf2-171">Next, enable hello TCP/IP protocol with **SQL Server Configuration Manager**.</span></span>

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-connection-tcp-protocol.md)]

## <a name="connect-with-ssms"></a><span data-ttu-id="babf2-172">Connexion avec SSMS</span><span class="sxs-lookup"><span data-stu-id="babf2-172">Connect with SSMS</span></span>

<span data-ttu-id="babf2-173">Hello étapes suivantes montrent comment toocreate un DNS facultatif d’étiquette pour votre machine virtuelle Azure et connectez-vous avec SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="babf2-173">hello following steps show how toocreate an optional DNS Label for your Azure VM and then connect with SQL Server Management Studio (SSMS).</span></span>

[!INCLUDE [Connect tooSQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]

## <a name="next-steps"></a><span data-ttu-id="babf2-174">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="babf2-174">Next Steps</span></span>

<span data-ttu-id="babf2-175">instructions de configuration toosee en même temps que ces étapes de connectivité, consultez [approvisionnement d’une Machine virtuelle de SQL Server sur Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="babf2-175">toosee provisioning instructions along with these connectivity steps, see [Provisioning a SQL Server Virtual Machine on Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

<span data-ttu-id="babf2-176">Pour les autres rubriques connexes toorunning SQL Server dans des machines virtuelles Azure, consultez [SQL Server sur des Machines virtuelles Azure](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="babf2-176">For other topics related toorunning SQL Server in Azure VMs, see [SQL Server on Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
