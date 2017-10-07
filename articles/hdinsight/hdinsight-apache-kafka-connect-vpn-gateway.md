---
title: "tooKafka aaaConnect à l’aide de réseaux virtuels - Azure HDInsight | Documents Microsoft"
description: "Découvrez comment toodirectly connecter tooKafka sur HDInsight via un réseau virtuel Azure. Découvrez comment tooconnect tooKafka à partir de clients de développement à l’aide d’une passerelle VPN, ou à partir de clients dans votre site réseau à l’aide d’un périphérique de passerelle VPN."
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.devlang: 
ms.custom: hdinsightactive
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/01/2017
ms.author: larryfr
ms.openlocfilehash: 03542fe14b9a1d010dffa22a8f8d96b098a1576e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tookafka-on-hdinsight-preview-through-an-azure-virtual-network"></a><span data-ttu-id="1a48d-104">Se connecter tooKafka sur HDInsight (aperçu) via un réseau virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="1a48d-104">Connect tooKafka on HDInsight (preview) through an Azure Virtual Network</span></span>

<span data-ttu-id="1a48d-105">Découvrez comment toodirectly connecter tooKafka sur HDInsight à l’aide de réseaux virtuels Azure.</span><span class="sxs-lookup"><span data-stu-id="1a48d-105">Learn how toodirectly connect tooKafka on HDInsight using Azure Virtual Networks.</span></span> <span data-ttu-id="1a48d-106">Ce document fournit des informations sur la connexion tooKafka hello suivant des configurations à l’aide de :</span><span class="sxs-lookup"><span data-stu-id="1a48d-106">This document provides information on connecting tooKafka using hello following configurations:</span></span>

* <span data-ttu-id="1a48d-107">À partir des ressources d’un réseau local.</span><span class="sxs-lookup"><span data-stu-id="1a48d-107">From resources in an on-premises network.</span></span> <span data-ttu-id="1a48d-108">Cette connexion est établie à l’aide d’un périphérique VPN (logiciel ou matériel) sur votre réseau local.</span><span class="sxs-lookup"><span data-stu-id="1a48d-108">This connection is established by using a VPN device (software or hardware) on your local network.</span></span>
* <span data-ttu-id="1a48d-109">À partir d’un environnement de développement à l’aide d’un client de logiciel VPN.</span><span class="sxs-lookup"><span data-stu-id="1a48d-109">From a development environment using a VPN software client.</span></span>

## <a name="architecture-and-planning"></a><span data-ttu-id="1a48d-110">Architecture et planification</span><span class="sxs-lookup"><span data-stu-id="1a48d-110">Architecture and planning</span></span>

<span data-ttu-id="1a48d-111">HDInsight n’autorise pas de connexion directe tooKafka via hello internet public.</span><span class="sxs-lookup"><span data-stu-id="1a48d-111">HDInsight does not allow direct connection tooKafka over hello public internet.</span></span> <span data-ttu-id="1a48d-112">Au lieu de cela, les clients Kafka (producteurs et consommateurs) doivent utiliser un des hello des méthodes de connexion suivantes :</span><span class="sxs-lookup"><span data-stu-id="1a48d-112">Instead, Kafka clients (producers and consumers) must use one of hello following connection methods:</span></span>

* <span data-ttu-id="1a48d-113">Exécuter le client de hello Bonjour même réseau virtuel que Kafka sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1a48d-113">Run hello client in hello same virtual network as Kafka on HDInsight.</span></span> <span data-ttu-id="1a48d-114">Cette configuration est utilisée dans hello [démarrer avec Apache Kafka (aperçu) sur HDInsight](hdinsight-apache-kafka-get-started.md) document.</span><span class="sxs-lookup"><span data-stu-id="1a48d-114">This configuration is used in hello [Start with Apache Kafka (preview) on HDInsight](hdinsight-apache-kafka-get-started.md) document.</span></span> <span data-ttu-id="1a48d-115">Hello exécute client directement sur hello HDInsight des nœuds de cluster ou sur un autre ordinateur virtuel dans hello même réseau.</span><span class="sxs-lookup"><span data-stu-id="1a48d-115">hello client runs directly on hello HDInsight cluster nodes or on another virtual machine in hello same network.</span></span>

* <span data-ttu-id="1a48d-116">Connecter un réseau privé, par exemple, votre réseau local, réseau virtuel de toohello.</span><span class="sxs-lookup"><span data-stu-id="1a48d-116">Connect a private network, such as your on-premises network, toohello virtual network.</span></span> <span data-ttu-id="1a48d-117">Cette configuration permet aux clients dans votre travail de toodirectly de réseau local avec Kafka.</span><span class="sxs-lookup"><span data-stu-id="1a48d-117">This configuration allows clients in your on-premises network toodirectly work with Kafka.</span></span> <span data-ttu-id="1a48d-118">tooenable cette configuration, effectuer hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="1a48d-118">tooenable this configuration, perform hello following tasks:</span></span>

    1. <span data-ttu-id="1a48d-119">Créez un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="1a48d-119">Create a virtual network.</span></span>
    2. <span data-ttu-id="1a48d-120">Créez une passerelle VPN qui utilise une configuration de site à site.</span><span class="sxs-lookup"><span data-stu-id="1a48d-120">Create a VPN gateway that uses a site-to-site configuration.</span></span> <span data-ttu-id="1a48d-121">configuration de Hello utilisée dans ce document connecte tooa périphérique de passerelle VPN de votre réseau local.</span><span class="sxs-lookup"><span data-stu-id="1a48d-121">hello configuration used in this document connects tooa VPN gateway device in your on-premises network.</span></span>
    3. <span data-ttu-id="1a48d-122">Créer un serveur DNS dans le réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="1a48d-122">Create a DNS server in hello virtual network.</span></span>
    4. <span data-ttu-id="1a48d-123">Configurer le transfert entre le serveur DNS hello dans chaque réseau.</span><span class="sxs-lookup"><span data-stu-id="1a48d-123">Configure forwarding between hello DNS server in each network.</span></span>
    5. <span data-ttu-id="1a48d-124">Installez Kafka sur HDInsight dans le réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="1a48d-124">Install Kafka on HDInsight into hello virtual network.</span></span>

    <span data-ttu-id="1a48d-125">Pour plus d’informations, consultez hello [connecter tooKafka à partir d’un réseau local](#on-premises) section.</span><span class="sxs-lookup"><span data-stu-id="1a48d-125">For more information, see hello [Connect tooKafka from an on-premises network](#on-premises) section.</span></span> 

* <span data-ttu-id="1a48d-126">Se connecter à l’aide d’une passerelle VPN et le client VPN du réseau virtuel toohello des ordinateurs individuels.</span><span class="sxs-lookup"><span data-stu-id="1a48d-126">Connect individual machines toohello virtual network using a VPN gateway and VPN client.</span></span> <span data-ttu-id="1a48d-127">tooenable cette configuration, effectuer hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="1a48d-127">tooenable this configuration, perform hello following tasks:</span></span>

    1. <span data-ttu-id="1a48d-128">Créez un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="1a48d-128">Create a virtual network.</span></span>
    2. <span data-ttu-id="1a48d-129">Créez une passerelle VPN qui utilise une configuration de point à site.</span><span class="sxs-lookup"><span data-stu-id="1a48d-129">Create a VPN gateway that uses a point-to-site configuration.</span></span> <span data-ttu-id="1a48d-130">Cette configuration offre un client VPN qui peut être installé sur les clients Windows.</span><span class="sxs-lookup"><span data-stu-id="1a48d-130">This configuration provides a VPN client that can be installed on Windows clients.</span></span>
    3. <span data-ttu-id="1a48d-131">Installez Kafka sur HDInsight dans le réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="1a48d-131">Install Kafka on HDInsight into hello virtual network.</span></span>
    4. <span data-ttu-id="1a48d-132">Configurez Kafka pour la publication d’adresses IP.</span><span class="sxs-lookup"><span data-stu-id="1a48d-132">Configure Kafka for IP advertising.</span></span> <span data-ttu-id="1a48d-133">Cette configuration permet de hello tooconnect de client à l’aide de noms de domaine à la place d’adressage IP.</span><span class="sxs-lookup"><span data-stu-id="1a48d-133">This configuration allows hello client tooconnect using IP addressing instead of domain names.</span></span>
    5. <span data-ttu-id="1a48d-134">Téléchargez et utilisez le client VPN de hello sur le système de développement hello.</span><span class="sxs-lookup"><span data-stu-id="1a48d-134">Download and use hello VPN client on hello development system.</span></span>

    <span data-ttu-id="1a48d-135">Pour plus d’informations, consultez hello [connecter tooKafka avec un client VPN](#vpnclient) section.</span><span class="sxs-lookup"><span data-stu-id="1a48d-135">For more information, see hello [Connect tooKafka with a VPN client](#vpnclient) section.</span></span>

    > [!WARNING]
    > <span data-ttu-id="1a48d-136">Cette configuration est recommandée uniquement à des fins de développement en raison de hello limites suivantes :</span><span class="sxs-lookup"><span data-stu-id="1a48d-136">This configuration is only recommended for development purposes because of hello following limitations:</span></span>
    >
    > * <span data-ttu-id="1a48d-137">Chaque client doit se connecter à l’aide d’un client de logiciel VPN.</span><span class="sxs-lookup"><span data-stu-id="1a48d-137">Each client must connect using a VPN software client.</span></span> <span data-ttu-id="1a48d-138">Azure fournit uniquement un client Windows.</span><span class="sxs-lookup"><span data-stu-id="1a48d-138">Azure only provides a Windows-based client.</span></span>
    > * <span data-ttu-id="1a48d-139">client de Hello ne transmet pas de nom résolution demandes toohello réseau virtuel, vous devez donc utiliser toocommunicate avec Kafka d’adressage IP.</span><span class="sxs-lookup"><span data-stu-id="1a48d-139">hello client does not pass name resolution requests toohello virtual network, so you must use IP addressing toocommunicate with Kafka.</span></span> <span data-ttu-id="1a48d-140">Communication IP nécessite une configuration supplémentaire sur le cluster de Kafka de hello.</span><span class="sxs-lookup"><span data-stu-id="1a48d-140">IP communication requires additional configuration on hello Kafka cluster.</span></span>

<span data-ttu-id="1a48d-141">Pour plus d’informations sur l’utilisation de HDInsight dans un réseau virtuel, consultez [Étendre HDInsight à l’aide de réseaux virtuels Azure](./hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="1a48d-141">For more information on using HDInsight in a virtual network, see [Extend HDInsight by using Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md).</span></span>

## <span data-ttu-id="1a48d-142"><a id="on-premises"></a>Se connecter tooKafka à partir d’un réseau local</span><span class="sxs-lookup"><span data-stu-id="1a48d-142"><a id="on-premises"></a> Connect tooKafka from an on-premises network</span></span>

<span data-ttu-id="1a48d-143">toocreate un cluster Kafka qui communique avec votre réseau local, suivez les étapes de hello Bonjour [réseau de se connecter de HDInsight tooyour local](./connect-on-premises-network.md) document.</span><span class="sxs-lookup"><span data-stu-id="1a48d-143">toocreate a Kafka cluster that communicates with your on-premises network, follow hello steps in hello [Connect HDInsight tooyour on-premises network](./connect-on-premises-network.md) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1a48d-144">Lorsque vous créez le cluster HDInsight de hello, sélectionnez hello __Kafka__ type de cluster.</span><span class="sxs-lookup"><span data-stu-id="1a48d-144">When creating hello HDInsight cluster, select hello __Kafka__ cluster type.</span></span>

<span data-ttu-id="1a48d-145">Les étapes suivantes créent hello configuration suivante :</span><span class="sxs-lookup"><span data-stu-id="1a48d-145">These steps create hello following configuration:</span></span>

* <span data-ttu-id="1a48d-146">Réseau virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="1a48d-146">Azure Virtual Network</span></span>
* <span data-ttu-id="1a48d-147">Passerelle VPN de site à site</span><span class="sxs-lookup"><span data-stu-id="1a48d-147">Site-to-site VPN gateway</span></span>
* <span data-ttu-id="1a48d-148">Compte de stockage Azure (utilisé par HDInsight)</span><span class="sxs-lookup"><span data-stu-id="1a48d-148">Azure Storage account (used by HDInsight)</span></span>
* <span data-ttu-id="1a48d-149">Kafka sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="1a48d-149">Kafka on HDInsight</span></span>

<span data-ttu-id="1a48d-150">tooverify qu’un client Kafka peut se connecter à toohello cluster à partir de locale, utilisez les étapes de hello Bonjour [exemple : client Python](#python-client) section.</span><span class="sxs-lookup"><span data-stu-id="1a48d-150">tooverify that a Kafka client can connect toohello cluster from on-premises, use hello steps in hello [Example: Python client](#python-client) section.</span></span>

## <span data-ttu-id="1a48d-151"><a id="vpnclient"></a>Se connecter tooKafka avec un client VPN</span><span class="sxs-lookup"><span data-stu-id="1a48d-151"><a id="vpnclient"></a> Connect tooKafka with a VPN client</span></span>

<span data-ttu-id="1a48d-152">Utilisez les étapes de hello dans cette hello toocreate de section configuration suivante :</span><span class="sxs-lookup"><span data-stu-id="1a48d-152">Use hello steps in this section toocreate hello following configuration:</span></span>

* <span data-ttu-id="1a48d-153">Réseau virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="1a48d-153">Azure Virtual Network</span></span>
* <span data-ttu-id="1a48d-154">Passerelle VPN de point à site</span><span class="sxs-lookup"><span data-stu-id="1a48d-154">Point-to-site VPN gateway</span></span>
* <span data-ttu-id="1a48d-155">Compte Stockage Azure (utilisé par HDInsight)</span><span class="sxs-lookup"><span data-stu-id="1a48d-155">Azure Storage Account (used by HDInsight)</span></span>
* <span data-ttu-id="1a48d-156">Kafka sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="1a48d-156">Kafka on HDInsight</span></span>

1. <span data-ttu-id="1a48d-157">Suivez les étapes de hello Bonjour [fonctionne avec des certificats auto-signés pour des connexions de Point-to-site](../vpn-gateway/vpn-gateway-certificates-point-to-site.md) document.</span><span class="sxs-lookup"><span data-stu-id="1a48d-157">Follow hello steps in hello [Working with self-signed certificates for Point-to-site connections](../vpn-gateway/vpn-gateway-certificates-point-to-site.md) document.</span></span> <span data-ttu-id="1a48d-158">Ce document crée des certificats hello nécessaires pour la passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="1a48d-158">This document creates hello certificates needed for hello gateway.</span></span>

2. <span data-ttu-id="1a48d-159">Ouvrez une invite de PowerShell et utilisez hello suivant toolog de code dans tooyour abonnement Azure :</span><span class="sxs-lookup"><span data-stu-id="1a48d-159">Open a PowerShell prompt and use hello following code toolog in tooyour Azure subscription:</span></span>

    ```powershell
    Add-AzureRmAccount
    # If you have multiple subscriptions, uncomment tooset hello subscription
    #Select-AzureRmSubscription -SubscriptionName "name of your subscription"
    ```

3. <span data-ttu-id="1a48d-160">Utilisez hello suivant variables toocreate du code qui contiennent des informations de configuration :</span><span class="sxs-lookup"><span data-stu-id="1a48d-160">Use hello following code toocreate variables that contain configuration information:</span></span>

    ```powershell
    # Prompt for generic information
    $resourceGroupName = Read-Host "What is hello resource group name?"
    $baseName = Read-Host "What is hello base name? It is used toocreate names for resources, such as 'net-basename' and 'kafka-basename':"
    $location = Read-Host "What Azure Region do you want toocreate hello resources in?"
    $rootCert = Read-Host "What is hello file path toohello root certificate? It is used toosecure hello VPN gateway."

    # Prompt for HDInsight credentials
    $adminCreds = Get-Credential -Message "Enter hello HTTPS user name and password for hello HDInsight cluster" -UserName "admin"
    $sshCreds = Get-Credential -Message "Enter hello SSH user name and password for hello HDInsight cluster" -UserName "sshuser"

    # Names for Azure resources
    $networkName = "net-$baseName"
    $clusterName = "kafka-$baseName"
    $storageName = "store$baseName" # Can't use dashes in storage names
    $defaultContainerName = $clusterName
    $defaultSubnetName = "default"
    $gatewaySubnetName = "GatewaySubnet"
    $gatewayPublicIpName = "GatewayIp"
    $gatewayIpConfigName = "GatewayConfig"
    $vpnRootCertName = "rootcert"
    $vpnName = "VPNGateway"

    # Network settings
    $networkAddressPrefix = "10.0.0.0/16"
    $defaultSubnetPrefix = "10.0.0.0/24"
    $gatewaySubnetPrefix = "10.0.1.0/24"
    $vpnClientAddressPool = "172.16.201.0/24"

    # HDInsight settings
    $HdiWorkerNodes = 4
    $hdiVersion = "3.5"
    $hdiType = "Kafka"
    ```

4. <span data-ttu-id="1a48d-161">Groupe de ressources Azure hello toocreate et le réseau virtuel de code suivant de hello d’utilisation :</span><span class="sxs-lookup"><span data-stu-id="1a48d-161">Use hello following code toocreate hello Azure resource group and virtual network:</span></span>

    ```powershell
    # Create hello resource group that contains everything
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create hello subnet configuration
    $defaultSubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $defaultSubnetName `
        -AddressPrefix $defaultSubnetPrefix
    $gatewaySubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $gatewaySubnetName `
        -AddressPrefix $gatewaySubnetPrefix

    # Create hello subnet
    New-AzureRmVirtualNetwork -Name $networkName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -AddressPrefix $networkAddressPrefix `
        -Subnet $defaultSubnetConfig, $gatewaySubnetConfig

    # Get hello network & subnet that were created
    $network = Get-AzureRmVirtualNetwork -Name $networkName `
        -ResourceGroupName $resourceGroupName
    $gatewaySubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $gatewaySubnetName `
        -VirtualNetwork $network
    $defaultSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $defaultSubnetName `
        -VirtualNetwork $network

    # Set a dynamic public IP address for hello gateway subnet
    $gatewayPublicIp = New-AzureRmPublicIpAddress -Name $gatewayPublicIpName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -AllocationMethod Dynamic
    $gatewayIpConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name $gatewayIpConfigName `
        -Subnet $gatewaySubnet `
        -PublicIpAddress $gatewayPublicIp

    # Get hello certificate info
    # Get hello full path in case a relative path was passed
    $rootCertFile = Get-ChildItem $rootCert
    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($rootCertFile)
    $certBase64 = [System.Convert]::ToBase64String($cert.RawData)
    $p2sRootCert = New-AzureRmVpnClientRootCertificate -Name $vpnRootCertName `
        -PublicCertData $certBase64

    # Create hello VPN gateway
    New-AzureRmVirtualNetworkGateway -Name $vpnName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -IpConfigurations $gatewayIpConfig `
        -GatewayType Vpn `
        -VpnType RouteBased `
        -EnableBgp $false `
        -GatewaySku Standard `
        -VpnClientAddressPool $vpnClientAddressPool `
        -VpnClientRootCertificates $p2sRootCert
    ```

    > [!WARNING]
    > <span data-ttu-id="1a48d-162">Il peut prendre quelques minutes pour que cette toocomplete de processus.</span><span class="sxs-lookup"><span data-stu-id="1a48d-162">It can take several minutes for this process toocomplete.</span></span>

5. <span data-ttu-id="1a48d-163">Utilisez hello suivant code toocreate hello compte de stockage Azure et blob conteneur :</span><span class="sxs-lookup"><span data-stu-id="1a48d-163">Use hello following code toocreate hello Azure Storage Account and blob container:</span></span>

    ```powershell
    # Create hello storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $storageName `
        -Type Standard_GRS `
        -Location $location

    # Get hello storage account keys and create a context
    $defaultStorageKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName `
        -Name $storageName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageName `
        -StorageAccountKey $defaultStorageKey

    # Create hello default storage container
    New-AzureStorageContainer -Name $defaultContainerName `
        -Context $storageContext
    ```

6. <span data-ttu-id="1a48d-164">Utilisez hello suivant du cluster HDInsight de code toocreate hello :</span><span class="sxs-lookup"><span data-stu-id="1a48d-164">Use hello following code toocreate hello HDInsight cluster:</span></span>

    ```powershell
    # Create hello HDInsight cluster
    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $clusterName `
        -Location $location `
        -ClusterSizeInNodes $hdiWorkerNodes `
        -ClusterType $hdiType `
        -OSType Linux `
        -Version $hdiVersion `
        -HttpCredential $adminCreds `
        -SshCredential $sshCreds `
        -DefaultStorageAccountName "$storageName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageKey `
        -DefaultStorageContainer $defaultContainerName `
        -VirtualNetworkId $network.Id `
        -SubnetName $defaultSubnet.Id
    ```

  > [!WARNING]
  > <span data-ttu-id="1a48d-165">Ce processus prend environ 20 minutes toocomplete.</span><span class="sxs-lookup"><span data-stu-id="1a48d-165">This process takes around 20 minutes toocomplete.</span></span>

8. <span data-ttu-id="1a48d-166">Utilisez hello suivant l’applet de commande tooretrieve hello URL pour le client de VPN Windows hello pour le réseau virtuel de hello :</span><span class="sxs-lookup"><span data-stu-id="1a48d-166">Use hello following cmdlet tooretrieve hello URL for hello Windows VPN client for hello virtual network:</span></span>

    ```powershell
    Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName `
        -VirtualNetworkGatewayName $vpnName `
        -ProcessorArchitecture Amd64
    ```

    <span data-ttu-id="1a48d-167">client de VPN Windows hello toodownload, utilisez hello retourné URI dans votre navigateur web.</span><span class="sxs-lookup"><span data-stu-id="1a48d-167">toodownload hello Windows VPN client, use hello returned URI in your web browser.</span></span>

### <a name="configure-kafka-for-ip-advertising"></a><span data-ttu-id="1a48d-168">Configuration de Kafka pour la publication d’adresses IP</span><span class="sxs-lookup"><span data-stu-id="1a48d-168">Configure Kafka for IP advertising</span></span>

<span data-ttu-id="1a48d-169">Par défaut, soigneur renvoie le nom de domaine de hello Hello Kafka courtiers tooclients.</span><span class="sxs-lookup"><span data-stu-id="1a48d-169">By default, Zookeeper returns hello domain name of hello Kafka brokers tooclients.</span></span> <span data-ttu-id="1a48d-170">Cette configuration ne fonctionne pas avec hello client VPN logiciel car il ne peut pas utiliser la résolution de noms pour les entités de réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="1a48d-170">This configuration does not work with hello VPN software client, as it cannot use name resolution for entities in hello virtual network.</span></span> <span data-ttu-id="1a48d-171">Pour cette configuration, utilisez hello qui suit les adresses IP de tooadvertise Kafka tooconfigure des étapes au lieu des noms de domaine :</span><span class="sxs-lookup"><span data-stu-id="1a48d-171">For this configuration, use hello following steps tooconfigure Kafka tooadvertise IP addresses instead of domain names:</span></span>

1. <span data-ttu-id="1a48d-172">À l’aide d’un navigateur web, accédez à toohttps://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="1a48d-172">Using a web browser, go toohttps://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="1a48d-173">Remplacez __CLUSTERNAME__ avec nom hello Hello Kafka sur le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1a48d-173">Replace __CLUSTERNAME__ with hello name of hello Kafka on HDInsight cluster.</span></span>

    <span data-ttu-id="1a48d-174">Lorsque vous y êtes invité, utilisez le nom d’utilisateur hello HTTPS et le mot de passe pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="1a48d-174">When prompted, use hello HTTPS user name and password for hello cluster.</span></span> <span data-ttu-id="1a48d-175">Hello l’interface utilisateur de Ambari Web de cluster de hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="1a48d-175">hello Ambari Web UI for hello cluster is displayed.</span></span>

2. <span data-ttu-id="1a48d-176">Sélectionnez des informations tooview sur Kafka, __Kafka__ à partir de la liste hello sur hello gauche.</span><span class="sxs-lookup"><span data-stu-id="1a48d-176">tooview information on Kafka, select __Kafka__ from hello list on hello left.</span></span>

    ![Liste des services avec l’option Kafka en surbrillance](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-service.png)

3. <span data-ttu-id="1a48d-178">tooview configuration de Kafka, sélectionnez __configurations__ à partir du haut et au milieu hello.</span><span class="sxs-lookup"><span data-stu-id="1a48d-178">tooview Kafka configuration, select __Configs__ from hello top middle.</span></span>

    ![Liens vers les configurations Kafka](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-config.png)

4. <span data-ttu-id="1a48d-180">toofind hello __kafka-env__ configuration, entrez `kafka-env` Bonjour __filtre__ champ sur le coin supérieur droit de hello.</span><span class="sxs-lookup"><span data-stu-id="1a48d-180">toofind hello __kafka-env__ configuration, enter `kafka-env` in hello __Filter__ field on hello upper right.</span></span>

    ![Configuration Kafka, pour kafka-env](./media/hdinsight-apache-kafka-connect-vpn-gateway/search-for-kafka-env.png)

5. <span data-ttu-id="1a48d-182">les adresses IP de tooadvertise Kafka tooconfigure, ajouter hello suivant en bas de toohello texte Hello __kafka-env-modèle__ champ :</span><span class="sxs-lookup"><span data-stu-id="1a48d-182">tooconfigure Kafka tooadvertise IP addresses, add hello following text toohello bottom of hello __kafka-env-template__ field:</span></span>

    ```
    # Configure Kafka tooadvertise IP addresses instead of FQDN
    IP_ADDRESS=$(hostname -i)
    echo advertised.listeners=$IP_ADDRESS
    sed -i.bak -e '/advertised/{/advertised@/!d;}' /usr/hdp/current/kafka-broker/conf/server.properties
    echo "advertised.listeners=PLAINTEXT://$IP_ADDRESS:9092" >> /usr/hdp/current/kafka-broker/conf/server.properties
    ```

6. <span data-ttu-id="1a48d-183">interface hello tooconfigure qui écoute Kafka, entrez `listeners` Bonjour __filtre__ champ sur le coin supérieur droit de hello.</span><span class="sxs-lookup"><span data-stu-id="1a48d-183">tooconfigure hello interface that Kafka listens on, enter `listeners` in hello __Filter__ field on hello upper right.</span></span>

7. <span data-ttu-id="1a48d-184">tooconfigure toolisten Kafka sur toutes les interfaces réseau, de modifier la valeur hello Bonjour __écouteurs__ champ trop`PLAINTEXT://0.0.0.0:9092`.</span><span class="sxs-lookup"><span data-stu-id="1a48d-184">tooconfigure Kafka toolisten on all network interfaces, change hello value in hello __listeners__ field too`PLAINTEXT://0.0.0.0:9092`.</span></span>

8. <span data-ttu-id="1a48d-185">modifications de configuration toosave hello, utilisez hello __enregistrer__ bouton.</span><span class="sxs-lookup"><span data-stu-id="1a48d-185">toosave hello configuration changes, use hello __Save__ button.</span></span> <span data-ttu-id="1a48d-186">Entrez un message texte qui décrit les modifications de hello.</span><span class="sxs-lookup"><span data-stu-id="1a48d-186">Enter a text message describing hello changes.</span></span> <span data-ttu-id="1a48d-187">Sélectionnez __OK__ une fois hello modifications ont été enregistrées.</span><span class="sxs-lookup"><span data-stu-id="1a48d-187">Select __OK__ once hello changes have been saved.</span></span>

    ![Bouton pour enregistrer la configuration](./media/hdinsight-apache-kafka-connect-vpn-gateway/save-button.png)

9. <span data-ttu-id="1a48d-189">erreurs tooprevent lors du redémarrage Kafka, utilisez hello __Actions Service__ sélectionnez __activer sur le Mode Maintenance__.</span><span class="sxs-lookup"><span data-stu-id="1a48d-189">tooprevent errors when restarting Kafka, use hello __Service Actions__ button and select __Turn On Maintenance Mode__.</span></span> <span data-ttu-id="1a48d-190">Sélectionnez OK toocomplete cette opération.</span><span class="sxs-lookup"><span data-stu-id="1a48d-190">Select OK toocomplete this operation.</span></span>

    ![Actions de service, avec l’option Activer le mode de maintenance en surbrillance](./media/hdinsight-apache-kafka-connect-vpn-gateway/turn-on-maintenance-mode.png)

10. <span data-ttu-id="1a48d-192">toorestart Kafka, utilisez hello __redémarrer__ sélectionnez __redémarrer l’affectées toutes les__.</span><span class="sxs-lookup"><span data-stu-id="1a48d-192">toorestart Kafka, use hello __Restart__ button and select __Restart All Affected__.</span></span> <span data-ttu-id="1a48d-193">Confirmer le redémarrage de hello et utilisez hello __OK__ bouton une fois l’opération de hello.</span><span class="sxs-lookup"><span data-stu-id="1a48d-193">Confirm hello restart, and then use hello __OK__ button after hello operation has completed.</span></span>

    ![Bouton Redémarrer avec l’option Restart All Affected (Redémarrer tous les éléments affectés) en surbrillance](./media/hdinsight-apache-kafka-connect-vpn-gateway/restart-button.png)

11. <span data-ttu-id="1a48d-195">mode de maintenance toodisable, utilisez hello __Actions Service__ sélectionnez __activer en Mode Maintenance__.</span><span class="sxs-lookup"><span data-stu-id="1a48d-195">toodisable maintenance mode, use hello __Service Actions__ button and select __Turn Off Maintenance Mode__.</span></span> <span data-ttu-id="1a48d-196">Sélectionnez **OK** toocomplete cette opération.</span><span class="sxs-lookup"><span data-stu-id="1a48d-196">Select **OK** toocomplete this operation.</span></span>

### <a name="connect-toohello-vpn-gateway"></a><span data-ttu-id="1a48d-197">Passerelle VPN de toohello de connexion</span><span class="sxs-lookup"><span data-stu-id="1a48d-197">Connect toohello VPN gateway</span></span>

<span data-ttu-id="1a48d-198">tooconnect toohello passerelle VPN un __client Windows__, utilisez hello __connecter tooAzure__ section Hello [configurer une connexion de Point-to-Site](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate) document.</span><span class="sxs-lookup"><span data-stu-id="1a48d-198">tooconnect toohello VPN gateway from a __Windows client__, use hello __Connect tooAzure__ section of hello [Configure a Point-to-Site connection](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate) document.</span></span>

## <span data-ttu-id="1a48d-199"><a id="python-client"></a> Exemple : client Python</span><span class="sxs-lookup"><span data-stu-id="1a48d-199"><a id="python-client"></a> Example: Python client</span></span>

<span data-ttu-id="1a48d-200">toovalidate connectivité tooKafka, utilisez hello suivant les étapes toocreate et exécutez un producteur de Python et un consommateur :</span><span class="sxs-lookup"><span data-stu-id="1a48d-200">toovalidate connectivity tooKafka, use hello following steps toocreate and run a Python producer and consumer:</span></span>

1. <span data-ttu-id="1a48d-201">Utilisez une des hello suivant hello tooretrieve de méthodes entièrement qualifié le nom de domaine (FQDN) et les adresses IP des nœuds hello Bonjour cluster de Kafka :</span><span class="sxs-lookup"><span data-stu-id="1a48d-201">Use one of hello following methods tooretrieve hello fully qualified domain name (FQDN) and IP addresses of hello nodes in hello Kafka cluster:</span></span>

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

    <span data-ttu-id="1a48d-202">Ce script suppose que `$resourceGroupName` est le nom hello hello Azure du groupe de ressources qui contient le réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="1a48d-202">This script assumes that `$resourceGroupName` is hello name of hello Azure resource group that contains hello virtual network.</span></span>

    <span data-ttu-id="1a48d-203">Enregistrez hello a retourné des informations pour une utilisation dans les étapes suivantes hello.</span><span class="sxs-lookup"><span data-stu-id="1a48d-203">Save hello returned information for use in hello next steps.</span></span>

2. <span data-ttu-id="1a48d-204">Hello utilisation suivant tooinstall hello [kafka-python](http://kafka-python.readthedocs.io/) client :</span><span class="sxs-lookup"><span data-stu-id="1a48d-204">Use hello following tooinstall hello [kafka-python](http://kafka-python.readthedocs.io/) client:</span></span>

        pip install kafka-python

3. <span data-ttu-id="1a48d-205">toosend données tooKafka, hello utilisation après le code Python :</span><span class="sxs-lookup"><span data-stu-id="1a48d-205">toosend data tooKafka, use hello following Python code:</span></span>

  ```python
  from kafka import KafkaProducer
  # Replace hello `ip_address` entries with hello IP address of your worker nodes
  # NOTE: you don't need hello full list of worker nodes, just one or two.
  producer = KafkaProducer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'])
  for _ in range(50):
      producer.send('testtopic', b'test message')
  ```

    <span data-ttu-id="1a48d-206">Remplacez hello `'kafka_broker'` entrées avec des adresses hello retourné à l’étape 1 de cette section :</span><span class="sxs-lookup"><span data-stu-id="1a48d-206">Replace hello `'kafka_broker'` entries with hello addresses returned from step 1 in this section:</span></span>

    * <span data-ttu-id="1a48d-207">Si vous utilisez un __client logiciel VPN__, remplacez hello `kafka_broker` entrées avec l’adresse IP de hello vos nœuds de travail.</span><span class="sxs-lookup"><span data-stu-id="1a48d-207">If you are using a __Software VPN client__, replace hello `kafka_broker` entries with hello IP address of your worker nodes.</span></span>

    * <span data-ttu-id="1a48d-208">Si vous avez __activé la résolution de noms via un serveur DNS personnalisé__, remplacez hello `kafka_broker` entrées avec hello FQDN hello de nœuds de travail.</span><span class="sxs-lookup"><span data-stu-id="1a48d-208">If you have __enabled name resolution through a custom DNS server__, replace hello `kafka_broker` entries with hello FQDN of hello worker nodes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1a48d-209">Ce code envoie la chaîne de hello `test message` toohello rubrique `testtopic`.</span><span class="sxs-lookup"><span data-stu-id="1a48d-209">This code sends hello string `test message` toohello topic `testtopic`.</span></span> <span data-ttu-id="1a48d-210">Hello est par défaut de Kafka sur HDInsight rubrique de hello toocreate s’il n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="1a48d-210">hello default configuration of Kafka on HDInsight is toocreate hello topic if it does not exist.</span></span>

4. <span data-ttu-id="1a48d-211">messages de type hello tooretrieve de Kafka, utilisez hello suivant code Python :</span><span class="sxs-lookup"><span data-stu-id="1a48d-211">tooretrieve hello messages from Kafka, use hello following Python code:</span></span>

   ```python
   from kafka import KafkaConsumer
   # Replace hello `ip_address` entries with hello IP address of your worker nodes
   # Again, you only need one or two, not hello full list.
   # Note: auto_offset_reset='earliest' resets hello starting offset toohello beginning
   #       of hello topic
   consumer = KafkaConsumer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'],auto_offset_reset='earliest')
   consumer.subscribe(['testtopic'])
   for msg in consumer:
     print (msg)
   ```

    <span data-ttu-id="1a48d-212">Remplacez hello `'kafka_broker'` entrées avec des adresses hello retourné à l’étape 1 de cette section :</span><span class="sxs-lookup"><span data-stu-id="1a48d-212">Replace hello `'kafka_broker'` entries with hello addresses returned from step 1 in this section:</span></span>

    * <span data-ttu-id="1a48d-213">Si vous utilisez un __client logiciel VPN__, remplacez hello `kafka_broker` entrées avec l’adresse IP de hello vos nœuds de travail.</span><span class="sxs-lookup"><span data-stu-id="1a48d-213">If you are using a __Software VPN client__, replace hello `kafka_broker` entries with hello IP address of your worker nodes.</span></span>

    * <span data-ttu-id="1a48d-214">Si vous avez __activé la résolution de noms via un serveur DNS personnalisé__, remplacez hello `kafka_broker` entrées avec hello FQDN hello de nœuds de travail.</span><span class="sxs-lookup"><span data-stu-id="1a48d-214">If you have __enabled name resolution through a custom DNS server__, replace hello `kafka_broker` entries with hello FQDN of hello worker nodes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a48d-215">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1a48d-215">Next steps</span></span>

<span data-ttu-id="1a48d-216">Pour plus d’informations sur l’utilisation de HDInsight avec un réseau virtuel, consultez hello [étendre Azure HDInsight à l’aide d’un réseau virtuel Azure](hdinsight-extend-hadoop-virtual-network.md) document.</span><span class="sxs-lookup"><span data-stu-id="1a48d-216">For more information on using HDInsight with a virtual network, see hello [Extend Azure HDInsight using an Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span>

<span data-ttu-id="1a48d-217">Pour plus d’informations sur la création d’un réseau virtuel Azure avec la passerelle Point-to-Site VPN, consultez hello suivant des documents :</span><span class="sxs-lookup"><span data-stu-id="1a48d-217">For more information on creating an Azure Virtual Network with Point-to-Site VPN gateway, see hello following documents:</span></span>

* [<span data-ttu-id="1a48d-218">Configurer une connexion de Point à Site à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="1a48d-218">Configure a Point-to-Site connection using hello Azure portal</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md)

* [<span data-ttu-id="1a48d-219">Configuration d’une connexion de point à site à un réseau virtuel à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="1a48d-219">Configure a Point-to-Site connection using Azure PowerShell</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

<span data-ttu-id="1a48d-220">Pour plus d’informations sur l’utilisation avec Kafka sur HDInsight, consultez hello suivant des documents :</span><span class="sxs-lookup"><span data-stu-id="1a48d-220">For more information on working with Kafka on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="1a48d-221">Prise en main de Kafka sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="1a48d-221">Get started with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="1a48d-222">MirrorMaker permet de créer un réplica Kafka sur un cluster HDInsight (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="1a48d-222">Use mirroring with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
