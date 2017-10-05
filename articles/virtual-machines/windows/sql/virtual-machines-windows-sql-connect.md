---
title: "Se connecter à une machine virtuelle SQL Server (Resource Manager) | Microsoft Docs"
description: "Découvrez comment vous connecter à SQL Server exécuté sur une machine virtuelle dans Azure. Cette rubrique utilise le modèle de déploiement classique. Les scénarios diffèrent selon la configuration réseau et l’emplacement du client."
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
ms.openlocfilehash: 67ba43f9456bbeffbf602067586143c4c68af672
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="connect-to-a-sql-server-virtual-machine-on-azure-resource-manager"></a><span data-ttu-id="f8779-105">Se connecter à une machine virtuelle SQL Server sur Azure (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="f8779-105">Connect to a SQL Server Virtual Machine on Azure (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f8779-106">Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="f8779-106">Resource Manager</span></span>](virtual-machines-windows-sql-connect.md)
> * [<span data-ttu-id="f8779-107">Classique</span><span class="sxs-lookup"><span data-stu-id="f8779-107">Classic</span></span>](../classic/sql-connect.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="f8779-108">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="f8779-108">Overview</span></span>

<span data-ttu-id="f8779-109">Cette rubrique décrit comment se connecter à votre instance de SQL Server exécuté sur une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="f8779-109">This topic describes how to connect to your SQL Server instance running on an Azure virtual machine.</span></span> <span data-ttu-id="f8779-110">Elle aborde certains [scénarios de connectivité générale](#connection-scenarios) et fournit une [procédure détaillée pour configurer la connectivité à SQL Server dans une machine virtuelle Azure](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="f8779-110">It covers some [general connectivity scenarios](#connection-scenarios) and then provides [detailed steps for configuring SQL Server connectivity in an Azure VM](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="f8779-111">Si vous préférez suivre une procédure pas-à-pas complète d’approvisionnement et de connectivité, voir [Approvisionnement d’une machine virtuelle SQL Server dans Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="f8779-111">If you would rather have a full walk-through of both provisioning and connectivity, see [Provisioning a SQL Server Virtual Machine on Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

## <a name="connection-scenarios"></a><span data-ttu-id="f8779-112">Scénarios de connexion</span><span class="sxs-lookup"><span data-stu-id="f8779-112">Connection scenarios</span></span>

<span data-ttu-id="f8779-113">La méthode utilisée par un client pour se connecter à un serveur SQL Server exécuté sur une machine virtuelle diffère selon l’emplacement du client et la configuration du réseau.</span><span class="sxs-lookup"><span data-stu-id="f8779-113">The way a client connects to SQL Server running on a Virtual Machine differs depending on the location of the client and the networking configuration.</span></span>

<span data-ttu-id="f8779-114">Si vous configurez un ordinateur virtuel SQL Server dans le portail Azure, vous avez la possibilité de spécifier le type de **connectivité SQL**.</span><span class="sxs-lookup"><span data-stu-id="f8779-114">If you provision a SQL Server VM in the Azure portal, you have the option of specifying the type of **SQL connectivity**.</span></span>

![Option de connectivité SQL publique lors de l’approvisionnement](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity.png)

<span data-ttu-id="f8779-116">Les options de connectivité sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="f8779-116">Your options for connectivity include:</span></span>

| <span data-ttu-id="f8779-117">Option</span><span class="sxs-lookup"><span data-stu-id="f8779-117">Option</span></span> | <span data-ttu-id="f8779-118">Description</span><span class="sxs-lookup"><span data-stu-id="f8779-118">Description</span></span> |
|---|---|
| <span data-ttu-id="f8779-119">**Public**</span><span class="sxs-lookup"><span data-stu-id="f8779-119">**Public**</span></span> | <span data-ttu-id="f8779-120">Se connecter à SQL Server via Internet</span><span class="sxs-lookup"><span data-stu-id="f8779-120">Connect to SQL Server over the internet</span></span> |
| <span data-ttu-id="f8779-121">**Privé**</span><span class="sxs-lookup"><span data-stu-id="f8779-121">**Private**</span></span> | <span data-ttu-id="f8779-122">se connecter à SQL Server dans le même réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="f8779-122">Connect to SQL Server in the same virtual network</span></span> |
| <span data-ttu-id="f8779-123">**Local**</span><span class="sxs-lookup"><span data-stu-id="f8779-123">**Local**</span></span> | <span data-ttu-id="f8779-124">Se connecter à SQL Server localement dans le même réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="f8779-124">Connect to SQL Server locally on the same virtual machine</span></span> | 

<span data-ttu-id="f8779-125">Les sections suivantes expliquent les options **Public** et **Privé** plus en détail.</span><span class="sxs-lookup"><span data-stu-id="f8779-125">The following sections explain the **Public** and **Private** options in more detail.</span></span>

## <a name="connect-to-sql-server-over-the-internet"></a><span data-ttu-id="f8779-126">Se connecter à SQL Server via Internet</span><span class="sxs-lookup"><span data-stu-id="f8779-126">Connect to SQL Server over the Internet</span></span>

<span data-ttu-id="f8779-127">Si vous souhaitez vous connecter à votre moteur de base de données SQL Server à partir d’Internet, sélectionnez **Public** pour le type **connectivité SQL** dans le portail lors de la configuration.</span><span class="sxs-lookup"><span data-stu-id="f8779-127">If you want to connect to your SQL Server database engine from the Internet, select **Public** for the **SQL connectivity** type in the portal during provisioning.</span></span> <span data-ttu-id="f8779-128">Le portail effectue automatiquement les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="f8779-128">The portal automatically does the following steps:</span></span>

* <span data-ttu-id="f8779-129">Il active le protocole TCP/IP pour SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f8779-129">Enables the TCP/IP protocol for SQL Server.</span></span>
* <span data-ttu-id="f8779-130">Il configure une règle de pare-feu pour ouvrir le port TCP de SQL Server (1433 par défaut).</span><span class="sxs-lookup"><span data-stu-id="f8779-130">Configures a firewall rule to open the SQL Server TCP port (default 1433).</span></span>
* <span data-ttu-id="f8779-131">Il active l’authentification SQL Server, requis pour l’accès public.</span><span class="sxs-lookup"><span data-stu-id="f8779-131">Enables SQL Server Authentication, required for public access.</span></span>
* <span data-ttu-id="f8779-132">Il configure le groupe de sécurité réseau sur l’ordinateur virtuel pour tout trafic TCP sur le port SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f8779-132">Configures the network security group on the VM to all TCP traffic on the SQL Server port.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f8779-133">Les images de machine virtuelle des éditions SQL Server Developer et Express n’activent pas automatiquement le protocole TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="f8779-133">The virtual machine images for the SQL Server Developer and Express editions do not automatically enable the TCP/IP protocol.</span></span> <span data-ttu-id="f8779-134">Pour les éditions Developer et Express, vous devez utiliser le gestionnaire de configuration SQL Server pour [activer manuellement le protocole TCP/IP](#manualtcp) après création de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f8779-134">For Developer and Express editions, you must use SQL Server Configuration Manager to [manually enable the TCP/IP protocol](#manualtcp) after creating the VM.</span></span>

<span data-ttu-id="f8779-135">Tout client disposant d’un accès à Internet peut se connecter à l’instance SQL Server en spécifiant l’adresse IP publique de la machine virtuelle ou le nom DNS attribué à cette adresse IP.</span><span class="sxs-lookup"><span data-stu-id="f8779-135">Any client with internet access can connect to the SQL Server instance by specifying either the public IP address of the virtual machine or any DNS label assigned to that IP address.</span></span> <span data-ttu-id="f8779-136">Si le port SQL Server est le port 1433, il est inutile de le spécifier dans la chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="f8779-136">If the SQL Server port is 1433, you do not need to specify it in the connection string.</span></span> <span data-ttu-id="f8779-137">La chaîne de connexion suivante se connecte à une machine virtuelle SQL avec un nom DNS de `sqlvmlabel.eastus.cloudapp.azure.com` à l’aide de l’authentification SQL (vous pouvez également utiliser l’adresse IP publique).</span><span class="sxs-lookup"><span data-stu-id="f8779-137">The following connection string connects to a SQL VM with a DNS label of `sqlvmlabel.eastus.cloudapp.azure.com` using SQL Authentication (you could also use the public IP address).</span></span>

```
Server=sqlvmlabel.eastus.cloudapp.azure.com;Integrated Security=false;User ID=<login_name>;Password=<your_password>
```

<span data-ttu-id="f8779-138">Même si cette méthode permet aux clients de se connecter via Internet, cela ne signifie pas que tout le monde peut se connecter à votre serveur SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f8779-138">Although this enables connectivity for clients over the internet, this does not imply that anyone can connect to your SQL Server.</span></span> <span data-ttu-id="f8779-139">Les clients externes doivent entrer les nom d’utilisateur et mot de passe corrects.</span><span class="sxs-lookup"><span data-stu-id="f8779-139">Outside clients have to the correct username and password.</span></span> <span data-ttu-id="f8779-140">Toutefois, pour renforcer la sécurité, vous pouvez éviter d’utiliser le port 1433 bien connu.</span><span class="sxs-lookup"><span data-stu-id="f8779-140">However, for additional security, you can avoid the well-known port 1433.</span></span> <span data-ttu-id="f8779-141">Par exemple, si vous avez configuré SQL Server pour écouter sur le port 1500 et établi des règles de pare-feu et de groupe de sécurité réseau appropriées, vous pouvez vous connecter en ajoutant le numéro de port au nom du serveur.</span><span class="sxs-lookup"><span data-stu-id="f8779-141">For example, if you configured SQL Server to listen on port 1500 and established proper firewall and network security group rules, you could connect by appending the port number to the Server name.</span></span> <span data-ttu-id="f8779-142">L’exemple suivant modifie le précédent en ajoutant un numéro de port personnalisé, **1500**, au nom du serveur :</span><span class="sxs-lookup"><span data-stu-id="f8779-142">The following example alters the previous one by adding a custom port number, **1500**, to the server name:</span></span>

```
Server=sqlvmlabel.eastus.cloudapp.azure.com,1500;Integrated Security=false;User ID=<login_name>;Password=<your_password>"
```

> [!NOTE]
> <span data-ttu-id="f8779-143">Lorsque vous interrogez SQL Server dans une machine virtuelle sur Internet, toutes les données sortantes depuis le centre de données Azure sont sujettes à la [tarification sur les transferts de données sortantes](https://azure.microsoft.com/pricing/details/data-transfers/) standard.</span><span class="sxs-lookup"><span data-stu-id="f8779-143">When you query SQL Server in a VM over the internet, all outgoing data from the Azure datacenter is subject to normal [pricing on outbound data transfers](https://azure.microsoft.com/pricing/details/data-transfers/).</span></span>

## <a name="connect-to-sql-server-within-a-virtual-network"></a><span data-ttu-id="f8779-144">Se connecter à SQL Server dans un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="f8779-144">Connect to SQL Server within a virtual network</span></span>

<span data-ttu-id="f8779-145">Lorsque vous choisissez l’option **Privé** comme type de **connectivité SQL** dans le portail, Azure effectue une configuration identique à **Public** pour la plupart des paramètres.</span><span class="sxs-lookup"><span data-stu-id="f8779-145">When you choose **Private** for the **SQL connectivity** type in the portal, Azure configures most of the settings identical to **Public**.</span></span> <span data-ttu-id="f8779-146">La seule différence est qu’il n’existe aucune règle de groupe de sécurité réseau pour autoriser le trafic externe sur le port SQL Server (1433 par défaut).</span><span class="sxs-lookup"><span data-stu-id="f8779-146">The one difference is that there is no network security group rule to allow outside traffic on the SQL Server port (default 1433).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f8779-147">Les images de machine virtuelle des éditions SQL Server Developer et Express n’activent pas automatiquement le protocole TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="f8779-147">The virtual machine images for the SQL Server Developer and Express editions do not automatically enable the TCP/IP protocol.</span></span> <span data-ttu-id="f8779-148">Pour les éditions Developer et Express, vous devez utiliser le gestionnaire de configuration SQL Server pour [activer manuellement le protocole TCP/IP](#manualtcp) après création de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f8779-148">For Developer and Express editions, you must use SQL Server Configuration Manager to [manually enable the TCP/IP protocol](#manualtcp) after creating the VM.</span></span>

<span data-ttu-id="f8779-149">La connectivité privée est souvent utilisée conjointement avec [Réseau virtuel](../../../virtual-network/virtual-networks-overview.md) et permet plusieurs scénarios.</span><span class="sxs-lookup"><span data-stu-id="f8779-149">Private connectivity is often used in conjunction with [Virtual Network](../../../virtual-network/virtual-networks-overview.md), which enables several scenarios.</span></span> <span data-ttu-id="f8779-150">Vous pouvez connecter des machines virtuelles au sein d’un même réseau virtuel, même si elles existent dans différents groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="f8779-150">You can connect VMs in the same virtual network, even if those VMs exist in different resource groups.</span></span> <span data-ttu-id="f8779-151">De plus, un [VPN de site à site](../../../vpn-gateway/vpn-gateway-site-to-site-create.md)permet de créer une architecture hybride qui connecte les machines virtuelles aux machines et réseaux locaux.</span><span class="sxs-lookup"><span data-stu-id="f8779-151">And with a [site-to-site VPN](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), you can create a hybrid architecture that connects VMs with on-premises networks and machines.</span></span>

<span data-ttu-id="f8779-152">Les réseaux virtuels vous permettent également d’associer vos machines virtuelles Azure à un domaine.</span><span class="sxs-lookup"><span data-stu-id="f8779-152">Virtual networks also enable     you to join your Azure VMs to a domain.</span></span> <span data-ttu-id="f8779-153">Il s’agit de la seule façon d’utiliser l’authentification Windows pour SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f8779-153">This is the only way to use Windows Authentication to SQL Server.</span></span> <span data-ttu-id="f8779-154">Les autres scénarios de connexion requièrent l’authentification SQL avec des noms d’utilisateur et mots de passe.</span><span class="sxs-lookup"><span data-stu-id="f8779-154">The other connection scenarios require SQL Authentication with user names and passwords.</span></span>

<span data-ttu-id="f8779-155">En supposant que vous ayez configuré le DNS sur votre réseau virtuel, vous pouvez vous connecter à votre instance SQL Server en spécifiant le nom d’ordinateur de la machine virtuelle SQL Server dans la chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="f8779-155">Assuming that you have configured DNS in your virtual network, you can connect to your SQL Server instance by specifying the SQL Server VM computer name in the connection string.</span></span> <span data-ttu-id="f8779-156">L’exemple suivant part également du principe que l’authentification Windows a également été configurée et que l’utilisateur a accès à l’instance SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f8779-156">The following example also assumes that Windows Authentication has also been configured and that the user has been granted access to the SQL Server instance.</span></span>

```
Server=mysqlvm;Integrated Security=true
```

## <span data-ttu-id="f8779-157"><a id="change"></a>Modifier les paramètres de connectivité SQL</span><span class="sxs-lookup"><span data-stu-id="f8779-157"><a id="change"></a> Change SQL connectivity settings</span></span>

<span data-ttu-id="f8779-158">Vous pouvez modifier les paramètres de connectivité pour votre machine virtuelle de SQL Server dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f8779-158">You can change the connectivity settings for your SQL Server virtual machine in the Azure portal.</span></span>

1. <span data-ttu-id="f8779-159">Dans le portail Azure, sélectionnez **Machines virtuelles**.</span><span class="sxs-lookup"><span data-stu-id="f8779-159">In the Azure portal, select **Virtual Machines**.</span></span>

2. <span data-ttu-id="f8779-160">Sélectionnez votre machine virtuelle SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f8779-160">Select your SQL Server VM.</span></span>

3. <span data-ttu-id="f8779-161">Sous **paramètres**, cliquez sur **Configuration de SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="f8779-161">Under **Settings**, click **SQL Server configuration**.</span></span>

4. <span data-ttu-id="f8779-162">Modifiez le **niveau de connectivité SQL** suivant le paramètre requis.</span><span class="sxs-lookup"><span data-stu-id="f8779-162">Change the **SQL connectivity level** to your required setting.</span></span> <span data-ttu-id="f8779-163">Vous pouvez éventuellement utiliser cette zone pour modifier le port SQL Server ou les paramètres d’authentification SQL.</span><span class="sxs-lookup"><span data-stu-id="f8779-163">You can optionally use this area to change the SQL Server port or the SQL Authentication settings.</span></span>

   ![Modifier la connectivité SQL](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity-change.png)

5. <span data-ttu-id="f8779-165">Attendez quelques minutes pour terminer la mise à jour.</span><span class="sxs-lookup"><span data-stu-id="f8779-165">Wait several minutes for the update to complete.</span></span>

   ![Notification de mise à jour de la machine virtuelle SQL](./media/virtual-machines-windows-sql-connect/sql-vm-updating-notification.png)

## <span data-ttu-id="f8779-167"><a id="manualtcp"></a> Activer le protocole TCP/IP pour les éditions Developer et Express</span><span class="sxs-lookup"><span data-stu-id="f8779-167"><a id="manualtcp"></a> Enable TCP/IP for Developer and Express editions</span></span>

<span data-ttu-id="f8779-168">Lors de la configuration des paramètres de connectivité de SQL Server, Azure n’active pas automatiquement le protocole TCP/IP pour les éditions SQL Server Developer et Express.</span><span class="sxs-lookup"><span data-stu-id="f8779-168">When changing SQL Server connectivity settings, Azure does not automatically enable the TCP/IP protocol for SQL Server Developer and Express editions.</span></span> <span data-ttu-id="f8779-169">Les étapes ci-dessous expliquent comment activer manuellement le protocole TCP/IP pour vous connecter à distance via une adresse IP.</span><span class="sxs-lookup"><span data-stu-id="f8779-169">The steps below explain how to manually enable TCP/IP so that you can connect remotely by IP address.</span></span>

<span data-ttu-id="f8779-170">Connectez-vous d’abord à la machine virtuelle à l’aide du Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="f8779-170">First, connect to the SQL Server machine with remote desktop.</span></span>

> [!INCLUDE [Connect to SQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-remote-desktop-connect.md)]

<span data-ttu-id="f8779-171">Ensuite, activez le protocole TCP/IP avec le **gestionnaire de configuration SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="f8779-171">Next, enable the TCP/IP protocol with **SQL Server Configuration Manager**.</span></span>

> [!INCLUDE [Connect to SQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-connection-tcp-protocol.md)]

## <a name="connect-with-ssms"></a><span data-ttu-id="f8779-172">Connexion avec SSMS</span><span class="sxs-lookup"><span data-stu-id="f8779-172">Connect with SSMS</span></span>

<span data-ttu-id="f8779-173">Les étapes suivantes décrivent comment créer un nom DNS pour votre machine virtuelle Azure et vous connecter à SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="f8779-173">The following steps show how to create an optional DNS Label for your Azure VM and then connect with SQL Server Management Studio (SSMS).</span></span>

[!INCLUDE [Connect to SQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]

## <a name="next-steps"></a><span data-ttu-id="f8779-174">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f8779-174">Next Steps</span></span>

<span data-ttu-id="f8779-175">Pour obtenir des instructions d’approvisionnement en plus de ces étapes de connectivité, voir [Approvisionnement d’une machine virtuelle SQL Server dans Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="f8779-175">To see provisioning instructions along with these connectivity steps, see [Provisioning a SQL Server Virtual Machine on Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

<span data-ttu-id="f8779-176">Pour d’autres rubriques relatives à l’utilisation de SQL Server sur des machines virtuelles Azure, voir [SQL Server sur les machines virtuelles Azure](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f8779-176">For other topics related to running SQL Server in Azure VMs, see [SQL Server on Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>