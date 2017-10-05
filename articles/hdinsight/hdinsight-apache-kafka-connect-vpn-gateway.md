---
title: "Se connecter à Kafka à l’aide de réseaux virtuels - Azure HDInsight | Microsoft Docs"
description: "Découvrez comment vous connecter directement à Kafka sur HDInsight via un réseau virtuel Azure. Découvrez comment se connecter à Kafka à partir de clients de développement à l’aide d’une passerelle VPN, ou à partir de clients de votre réseau local à l’aide d’un périphérique de passerelle VPN."
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
ms.openlocfilehash: 245bee7c1dbb0236afdc2506e7ab84b5573cbc85
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="connect-to-kafka-on-hdinsight-preview-through-an-azure-virtual-network"></a><span data-ttu-id="d165d-104">Se connecter à Kafka sur HDInsight (version préliminaire) via un réseau virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="d165d-104">Connect to Kafka on HDInsight (preview) through an Azure Virtual Network</span></span>

<span data-ttu-id="d165d-105">Découvrez comment vous connecter directement à Kafka sur HDInsight à l’aide de réseaux virtuels Azure.</span><span class="sxs-lookup"><span data-stu-id="d165d-105">Learn how to directly connect to Kafka on HDInsight using Azure Virtual Networks.</span></span> <span data-ttu-id="d165d-106">Ce document fournit des informations sur la connexion à Kafka en utilisant les configurations suivantes :</span><span class="sxs-lookup"><span data-stu-id="d165d-106">This document provides information on connecting to Kafka using the following configurations:</span></span>

* <span data-ttu-id="d165d-107">À partir des ressources d’un réseau local.</span><span class="sxs-lookup"><span data-stu-id="d165d-107">From resources in an on-premises network.</span></span> <span data-ttu-id="d165d-108">Cette connexion est établie à l’aide d’un périphérique VPN (logiciel ou matériel) sur votre réseau local.</span><span class="sxs-lookup"><span data-stu-id="d165d-108">This connection is established by using a VPN device (software or hardware) on your local network.</span></span>
* <span data-ttu-id="d165d-109">À partir d’un environnement de développement à l’aide d’un client de logiciel VPN.</span><span class="sxs-lookup"><span data-stu-id="d165d-109">From a development environment using a VPN software client.</span></span>

## <a name="architecture-and-planning"></a><span data-ttu-id="d165d-110">Architecture et planification</span><span class="sxs-lookup"><span data-stu-id="d165d-110">Architecture and planning</span></span>

<span data-ttu-id="d165d-111">HDInsight n’autorise pas la connexion directe à Kafka via l’internet public.</span><span class="sxs-lookup"><span data-stu-id="d165d-111">HDInsight does not allow direct connection to Kafka over the public internet.</span></span> <span data-ttu-id="d165d-112">Au lieu de cela, les clients de Kafka (producteurs et consommateurs) doivent utiliser une des méthodes de connexion suivantes :</span><span class="sxs-lookup"><span data-stu-id="d165d-112">Instead, Kafka clients (producers and consumers) must use one of the following connection methods:</span></span>

* <span data-ttu-id="d165d-113">Exécutez le client dans le même réseau virtuel que Kafka sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d165d-113">Run the client in the same virtual network as Kafka on HDInsight.</span></span> <span data-ttu-id="d165d-114">Cette configuration est utilisée dans le document [Démarrer avec Apache Kafka (version préliminaire) sur HDInsight](hdinsight-apache-kafka-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d165d-114">This configuration is used in the [Start with Apache Kafka (preview) on HDInsight](hdinsight-apache-kafka-get-started.md) document.</span></span> <span data-ttu-id="d165d-115">Le client s’exécute directement sur les nœuds du cluster HDInsight ou sur une autre machine virtuelle dans le même réseau.</span><span class="sxs-lookup"><span data-stu-id="d165d-115">The client runs directly on the HDInsight cluster nodes or on another virtual machine in the same network.</span></span>

* <span data-ttu-id="d165d-116">Connectez un réseau privé, notamment votre réseau local, au réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="d165d-116">Connect a private network, such as your on-premises network, to the virtual network.</span></span> <span data-ttu-id="d165d-117">Cette configuration permet aux clients de votre réseau local de travailler directement avec Kafka.</span><span class="sxs-lookup"><span data-stu-id="d165d-117">This configuration allows clients in your on-premises network to directly work with Kafka.</span></span> <span data-ttu-id="d165d-118">Pour activer cette configuration, effectuez les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="d165d-118">To enable this configuration, perform the following tasks:</span></span>

    1. <span data-ttu-id="d165d-119">Créez un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="d165d-119">Create a virtual network.</span></span>
    2. <span data-ttu-id="d165d-120">Créez une passerelle VPN qui utilise une configuration de site à site.</span><span class="sxs-lookup"><span data-stu-id="d165d-120">Create a VPN gateway that uses a site-to-site configuration.</span></span> <span data-ttu-id="d165d-121">La configuration utilisée dans ce document se connecte à un périphérique de passerelle VPN de votre réseau local.</span><span class="sxs-lookup"><span data-stu-id="d165d-121">The configuration used in this document connects to a VPN gateway device in your on-premises network.</span></span>
    3. <span data-ttu-id="d165d-122">Créez un serveur DNS dans le réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="d165d-122">Create a DNS server in the virtual network.</span></span>
    4. <span data-ttu-id="d165d-123">Configurez le transfert entre les serveurs DNS de chaque réseau.</span><span class="sxs-lookup"><span data-stu-id="d165d-123">Configure forwarding between the DNS server in each network.</span></span>
    5. <span data-ttu-id="d165d-124">Installez Kafka sur HDInsight dans le réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="d165d-124">Install Kafka on HDInsight into the virtual network.</span></span>

    <span data-ttu-id="d165d-125">Pour plus d’informations, consultez la section [Se connecter à Kafka à partir d’un réseau local](#on-premises).</span><span class="sxs-lookup"><span data-stu-id="d165d-125">For more information, see the [Connect to Kafka from an on-premises network](#on-premises) section.</span></span> 

* <span data-ttu-id="d165d-126">Connectez des machines individuelles au réseau virtuel à l’aide d’une passerelle VPN et d’un client VPN.</span><span class="sxs-lookup"><span data-stu-id="d165d-126">Connect individual machines to the virtual network using a VPN gateway and VPN client.</span></span> <span data-ttu-id="d165d-127">Pour activer cette configuration, effectuez les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="d165d-127">To enable this configuration, perform the following tasks:</span></span>

    1. <span data-ttu-id="d165d-128">Créez un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="d165d-128">Create a virtual network.</span></span>
    2. <span data-ttu-id="d165d-129">Créez une passerelle VPN qui utilise une configuration de point à site.</span><span class="sxs-lookup"><span data-stu-id="d165d-129">Create a VPN gateway that uses a point-to-site configuration.</span></span> <span data-ttu-id="d165d-130">Cette configuration offre un client VPN qui peut être installé sur les clients Windows.</span><span class="sxs-lookup"><span data-stu-id="d165d-130">This configuration provides a VPN client that can be installed on Windows clients.</span></span>
    3. <span data-ttu-id="d165d-131">Installez Kafka sur HDInsight dans le réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="d165d-131">Install Kafka on HDInsight into the virtual network.</span></span>
    4. <span data-ttu-id="d165d-132">Configurez Kafka pour la publication d’adresses IP.</span><span class="sxs-lookup"><span data-stu-id="d165d-132">Configure Kafka for IP advertising.</span></span> <span data-ttu-id="d165d-133">Cette configuration permet au client de se connecter à l’aide de l’adressage IP au lieu des noms de domaine.</span><span class="sxs-lookup"><span data-stu-id="d165d-133">This configuration allows the client to connect using IP addressing instead of domain names.</span></span>
    5. <span data-ttu-id="d165d-134">Téléchargez et utilisez le client VPN sur le système de développement.</span><span class="sxs-lookup"><span data-stu-id="d165d-134">Download and use the VPN client on the development system.</span></span>

    <span data-ttu-id="d165d-135">Pour plus d’informations, consultez la section [Se connecter à Kafka avec un client VPN](#vpnclient).</span><span class="sxs-lookup"><span data-stu-id="d165d-135">For more information, see the [Connect to Kafka with a VPN client](#vpnclient) section.</span></span>

    > [!WARNING]
    > <span data-ttu-id="d165d-136">Cette configuration est recommandée uniquement à des fins de développement en raison des limitations suivantes :</span><span class="sxs-lookup"><span data-stu-id="d165d-136">This configuration is only recommended for development purposes because of the following limitations:</span></span>
    >
    > * <span data-ttu-id="d165d-137">Chaque client doit se connecter à l’aide d’un client de logiciel VPN.</span><span class="sxs-lookup"><span data-stu-id="d165d-137">Each client must connect using a VPN software client.</span></span> <span data-ttu-id="d165d-138">Azure fournit uniquement un client Windows.</span><span class="sxs-lookup"><span data-stu-id="d165d-138">Azure only provides a Windows-based client.</span></span>
    > * <span data-ttu-id="d165d-139">Le client ne transmet pas de demandes de résolution de noms au réseau virtuel. Vous devez donc utiliser l’adressage IP pour communiquer avec Kafka.</span><span class="sxs-lookup"><span data-stu-id="d165d-139">The client does not pass name resolution requests to the virtual network, so you must use IP addressing to communicate with Kafka.</span></span> <span data-ttu-id="d165d-140">La communication IP nécessite une configuration supplémentaire sur le cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="d165d-140">IP communication requires additional configuration on the Kafka cluster.</span></span>

<span data-ttu-id="d165d-141">Pour plus d’informations sur l’utilisation de HDInsight dans un réseau virtuel, consultez [Étendre HDInsight à l’aide de réseaux virtuels Azure](./hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="d165d-141">For more information on using HDInsight in a virtual network, see [Extend HDInsight by using Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md).</span></span>

## <span data-ttu-id="d165d-142"><a id="on-premises"></a> Se connecter à Kafka à partir d’un réseau local</span><span class="sxs-lookup"><span data-stu-id="d165d-142"><a id="on-premises"></a> Connect to Kafka from an on-premises network</span></span>

<span data-ttu-id="d165d-143">Pour créer un cluster Kafka qui communique avec votre réseau local, suivez les étapes du document [Connecter HDInsight à votre réseau local](./connect-on-premises-network.md).</span><span class="sxs-lookup"><span data-stu-id="d165d-143">To create a Kafka cluster that communicates with your on-premises network, follow the steps in the [Connect HDInsight to your on-premises network](./connect-on-premises-network.md) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d165d-144">Lorsque vous créez le cluster HDInsight, sélectionnez __Kafka__ comme type de cluster.</span><span class="sxs-lookup"><span data-stu-id="d165d-144">When creating the HDInsight cluster, select the __Kafka__ cluster type.</span></span>

<span data-ttu-id="d165d-145">Les étapes ci-après créent la configuration suivante :</span><span class="sxs-lookup"><span data-stu-id="d165d-145">These steps create the following configuration:</span></span>

* <span data-ttu-id="d165d-146">Réseau virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="d165d-146">Azure Virtual Network</span></span>
* <span data-ttu-id="d165d-147">Passerelle VPN de site à site</span><span class="sxs-lookup"><span data-stu-id="d165d-147">Site-to-site VPN gateway</span></span>
* <span data-ttu-id="d165d-148">Compte de stockage Azure (utilisé par HDInsight)</span><span class="sxs-lookup"><span data-stu-id="d165d-148">Azure Storage account (used by HDInsight)</span></span>
* <span data-ttu-id="d165d-149">Kafka sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="d165d-149">Kafka on HDInsight</span></span>

<span data-ttu-id="d165d-150">Pour vérifier qu’un client Kafka peut se connecter localement au cluster, utilisez les étapes décrites dans la section [Exemple : client Python](#python-client).</span><span class="sxs-lookup"><span data-stu-id="d165d-150">To verify that a Kafka client can connect to the cluster from on-premises, use the steps in the [Example: Python client](#python-client) section.</span></span>

## <span data-ttu-id="d165d-151"><a id="vpnclient"></a> Se connecter à Kafka avec un client VPN</span><span class="sxs-lookup"><span data-stu-id="d165d-151"><a id="vpnclient"></a> Connect to Kafka with a VPN client</span></span>

<span data-ttu-id="d165d-152">En suivant les étapes de cette section, vous pouvez créer la configuration ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="d165d-152">Use the steps in this section to create the following configuration:</span></span>

* <span data-ttu-id="d165d-153">Réseau virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="d165d-153">Azure Virtual Network</span></span>
* <span data-ttu-id="d165d-154">Passerelle VPN de point à site</span><span class="sxs-lookup"><span data-stu-id="d165d-154">Point-to-site VPN gateway</span></span>
* <span data-ttu-id="d165d-155">Compte Stockage Azure (utilisé par HDInsight)</span><span class="sxs-lookup"><span data-stu-id="d165d-155">Azure Storage Account (used by HDInsight)</span></span>
* <span data-ttu-id="d165d-156">Kafka sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="d165d-156">Kafka on HDInsight</span></span>

1. <span data-ttu-id="d165d-157">Suivez les étapes du document [Utilisation des certificats auto-signés pour les connexions de point à site](../vpn-gateway/vpn-gateway-certificates-point-to-site.md).</span><span class="sxs-lookup"><span data-stu-id="d165d-157">Follow the steps in the [Working with self-signed certificates for Point-to-site connections](../vpn-gateway/vpn-gateway-certificates-point-to-site.md) document.</span></span> <span data-ttu-id="d165d-158">Ce document crée les certificats nécessaires pour la passerelle.</span><span class="sxs-lookup"><span data-stu-id="d165d-158">This document creates the certificates needed for the gateway.</span></span>

2. <span data-ttu-id="d165d-159">Ouvrez une invite de commande PowerShell et utilisez le code suivant pour vous connecter à votre abonnement Azure :</span><span class="sxs-lookup"><span data-stu-id="d165d-159">Open a PowerShell prompt and use the following code to log in to your Azure subscription:</span></span>

    ```powershell
    Add-AzureRmAccount
    # If you have multiple subscriptions, uncomment to set the subscription
    #Select-AzureRmSubscription -SubscriptionName "name of your subscription"
    ```

3. <span data-ttu-id="d165d-160">Utilisez le code suivant pour créer des variables qui contiennent des informations de configuration :</span><span class="sxs-lookup"><span data-stu-id="d165d-160">Use the following code to create variables that contain configuration information:</span></span>

    ```powershell
    # Prompt for generic information
    $resourceGroupName = Read-Host "What is the resource group name?"
    $baseName = Read-Host "What is the base name? It is used to create names for resources, such as 'net-basename' and 'kafka-basename':"
    $location = Read-Host "What Azure Region do you want to create the resources in?"
    $rootCert = Read-Host "What is the file path to the root certificate? It is used to secure the VPN gateway."

    # Prompt for HDInsight credentials
    $adminCreds = Get-Credential -Message "Enter the HTTPS user name and password for the HDInsight cluster" -UserName "admin"
    $sshCreds = Get-Credential -Message "Enter the SSH user name and password for the HDInsight cluster" -UserName "sshuser"

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

4. <span data-ttu-id="d165d-161">Utilisez le code suivant pour créer le réseau virtuel et le groupe de ressources Azure :</span><span class="sxs-lookup"><span data-stu-id="d165d-161">Use the following code to create the Azure resource group and virtual network:</span></span>

    ```powershell
    # Create the resource group that contains everything
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create the subnet configuration
    $defaultSubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $defaultSubnetName `
        -AddressPrefix $defaultSubnetPrefix
    $gatewaySubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $gatewaySubnetName `
        -AddressPrefix $gatewaySubnetPrefix

    # Create the subnet
    New-AzureRmVirtualNetwork -Name $networkName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -AddressPrefix $networkAddressPrefix `
        -Subnet $defaultSubnetConfig, $gatewaySubnetConfig

    # Get the network & subnet that were created
    $network = Get-AzureRmVirtualNetwork -Name $networkName `
        -ResourceGroupName $resourceGroupName
    $gatewaySubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $gatewaySubnetName `
        -VirtualNetwork $network
    $defaultSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $defaultSubnetName `
        -VirtualNetwork $network

    # Set a dynamic public IP address for the gateway subnet
    $gatewayPublicIp = New-AzureRmPublicIpAddress -Name $gatewayPublicIpName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -AllocationMethod Dynamic
    $gatewayIpConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name $gatewayIpConfigName `
        -Subnet $gatewaySubnet `
        -PublicIpAddress $gatewayPublicIp

    # Get the certificate info
    # Get the full path in case a relative path was passed
    $rootCertFile = Get-ChildItem $rootCert
    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($rootCertFile)
    $certBase64 = [System.Convert]::ToBase64String($cert.RawData)
    $p2sRootCert = New-AzureRmVpnClientRootCertificate -Name $vpnRootCertName `
        -PublicCertData $certBase64

    # Create the VPN gateway
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
    > <span data-ttu-id="d165d-162">Ce processus peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="d165d-162">It can take several minutes for this process to complete.</span></span>

5. <span data-ttu-id="d165d-163">Utilisez le code suivant pour créer le compte Stockage Azure et le conteneur de blobs :</span><span class="sxs-lookup"><span data-stu-id="d165d-163">Use the following code to create the Azure Storage Account and blob container:</span></span>

    ```powershell
    # Create the storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $storageName `
        -Type Standard_GRS `
        -Location $location

    # Get the storage account keys and create a context
    $defaultStorageKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName `
        -Name $storageName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageName `
        -StorageAccountKey $defaultStorageKey

    # Create the default storage container
    New-AzureStorageContainer -Name $defaultContainerName `
        -Context $storageContext
    ```

6. <span data-ttu-id="d165d-164">Utilisez le code suivant pour créer le cluster HDInsight :</span><span class="sxs-lookup"><span data-stu-id="d165d-164">Use the following code to create the HDInsight cluster:</span></span>

    ```powershell
    # Create the HDInsight cluster
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
  > <span data-ttu-id="d165d-165">Ce processus prend environ 20 minutes.</span><span class="sxs-lookup"><span data-stu-id="d165d-165">This process takes around 20 minutes to complete.</span></span>

8. <span data-ttu-id="d165d-166">Utilisez la cmdlet suivante pour récupérer l’URL du client VPN Windows pour le réseau virtuel :</span><span class="sxs-lookup"><span data-stu-id="d165d-166">Use the following cmdlet to retrieve the URL for the Windows VPN client for the virtual network:</span></span>

    ```powershell
    Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName `
        -VirtualNetworkGatewayName $vpnName `
        -ProcessorArchitecture Amd64
    ```

    <span data-ttu-id="d165d-167">Pour télécharger le client VPN Windows, utilisez l’URI renvoyé dans votre navigateur web.</span><span class="sxs-lookup"><span data-stu-id="d165d-167">To download the Windows VPN client, use the returned URI in your web browser.</span></span>

### <a name="configure-kafka-for-ip-advertising"></a><span data-ttu-id="d165d-168">Configuration de Kafka pour la publication d’adresses IP</span><span class="sxs-lookup"><span data-stu-id="d165d-168">Configure Kafka for IP advertising</span></span>

<span data-ttu-id="d165d-169">Par défaut, Zookeeper renvoie le nom de domaine des répartiteurs Kafka aux clients.</span><span class="sxs-lookup"><span data-stu-id="d165d-169">By default, Zookeeper returns the domain name of the Kafka brokers to clients.</span></span> <span data-ttu-id="d165d-170">Cette configuration ne fonctionne pas avec le client logiciel VPN, car il ne peut pas utiliser la résolution de noms pour les entités du réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="d165d-170">This configuration does not work with the VPN software client, as it cannot use name resolution for entities in the virtual network.</span></span> <span data-ttu-id="d165d-171">Suivez les étapes ci-dessous pour configurer Kafka afin qu’il publie des adresses IP au lieu des noms de domaine :</span><span class="sxs-lookup"><span data-stu-id="d165d-171">For this configuration, use the following steps to configure Kafka to advertise IP addresses instead of domain names:</span></span>

1. <span data-ttu-id="d165d-172">Accédez à https://CLUSTERNAME.azurehdinsight.net via votre navigateur web.</span><span class="sxs-lookup"><span data-stu-id="d165d-172">Using a web browser, go to https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="d165d-173">Remplacez __CLUSTERNAME__ par le nom du cluster Kafka sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d165d-173">Replace __CLUSTERNAME__ with the name of the Kafka on HDInsight cluster.</span></span>

    <span data-ttu-id="d165d-174">Lorsque vous y êtes invité, utilisez le nom et le mot de passe utilisateur HTTPS correspondant au cluster.</span><span class="sxs-lookup"><span data-stu-id="d165d-174">When prompted, use the HTTPS user name and password for the cluster.</span></span> <span data-ttu-id="d165d-175">L’interface utilisateur web d’Ambari pour le cluster s’affiche.</span><span class="sxs-lookup"><span data-stu-id="d165d-175">The Ambari Web UI for the cluster is displayed.</span></span>

2. <span data-ttu-id="d165d-176">Pour afficher plus d’informations sur Kafka, sélectionnez __Kafka__ dans la liste sur la gauche.</span><span class="sxs-lookup"><span data-stu-id="d165d-176">To view information on Kafka, select __Kafka__ from the list on the left.</span></span>

    ![Liste des services avec l’option Kafka en surbrillance](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-service.png)

3. <span data-ttu-id="d165d-178">Pour afficher la configuration Kafka, sélectionnez __Configurations__ en haut et au centre de la page.</span><span class="sxs-lookup"><span data-stu-id="d165d-178">To view Kafka configuration, select __Configs__ from the top middle.</span></span>

    ![Liens vers les configurations Kafka](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-config.png)

4. <span data-ttu-id="d165d-180">Pour trouver la configuration __kafka-env__, entrez `kafka-env` dans le champ __Filtre__ situé en haut à droite.</span><span class="sxs-lookup"><span data-stu-id="d165d-180">To find the __kafka-env__ configuration, enter `kafka-env` in the __Filter__ field on the upper right.</span></span>

    ![Configuration Kafka, pour kafka-env](./media/hdinsight-apache-kafka-connect-vpn-gateway/search-for-kafka-env.png)

5. <span data-ttu-id="d165d-182">Pour configurer Kafka afin qu’il publie des adresses IP, ajoutez le texte suivant au bas du champ __kafka-env-template__ :</span><span class="sxs-lookup"><span data-stu-id="d165d-182">To configure Kafka to advertise IP addresses, add the following text to the bottom of the __kafka-env-template__ field:</span></span>

    ```
    # Configure Kafka to advertise IP addresses instead of FQDN
    IP_ADDRESS=$(hostname -i)
    echo advertised.listeners=$IP_ADDRESS
    sed -i.bak -e '/advertised/{/advertised@/!d;}' /usr/hdp/current/kafka-broker/conf/server.properties
    echo "advertised.listeners=PLAINTEXT://$IP_ADDRESS:9092" >> /usr/hdp/current/kafka-broker/conf/server.properties
    ```

6. <span data-ttu-id="d165d-183">Pour configurer l’interface écoutée par Kafka, entrez `listeners` dans le champ __Filtre__ situé en haut à droite.</span><span class="sxs-lookup"><span data-stu-id="d165d-183">To configure the interface that Kafka listens on, enter `listeners` in the __Filter__ field on the upper right.</span></span>

7. <span data-ttu-id="d165d-184">Pour configurer Kafka afin qu’il écoute toutes les interfaces réseau, remplacez la valeur du champ __écouteurs__ par `PLAINTEXT://0.0.0.0:9092`.</span><span class="sxs-lookup"><span data-stu-id="d165d-184">To configure Kafka to listen on all network interfaces, change the value in the __listeners__ field to `PLAINTEXT://0.0.0.0:9092`.</span></span>

8. <span data-ttu-id="d165d-185">Utilisez le bouton __Enregistrer__ pour enregistrer les modifications apportées à la configuration.</span><span class="sxs-lookup"><span data-stu-id="d165d-185">To save the configuration changes, use the __Save__ button.</span></span> <span data-ttu-id="d165d-186">Entrez un message texte décrivant les modifications.</span><span class="sxs-lookup"><span data-stu-id="d165d-186">Enter a text message describing the changes.</span></span> <span data-ttu-id="d165d-187">Sélectionnez __OK__ une fois les modifications apportées.</span><span class="sxs-lookup"><span data-stu-id="d165d-187">Select __OK__ once the changes have been saved.</span></span>

    ![Bouton pour enregistrer la configuration](./media/hdinsight-apache-kafka-connect-vpn-gateway/save-button.png)

9. <span data-ttu-id="d165d-189">Pour éviter des erreurs lors du redémarrage de Kafka, utilisez le bouton __Service Actions__ (Actions du service) et sélectionnez __Activer le mode de maintenance__.</span><span class="sxs-lookup"><span data-stu-id="d165d-189">To prevent errors when restarting Kafka, use the __Service Actions__ button and select __Turn On Maintenance Mode__.</span></span> <span data-ttu-id="d165d-190">Sélectionnez OK pour terminer cette opération.</span><span class="sxs-lookup"><span data-stu-id="d165d-190">Select OK to complete this operation.</span></span>

    ![Actions de service, avec l’option Activer le mode de maintenance en surbrillance](./media/hdinsight-apache-kafka-connect-vpn-gateway/turn-on-maintenance-mode.png)

10. <span data-ttu-id="d165d-192">Pour redémarrer Kafka, utilisez le bouton __Redémarrer__ et sélectionnez __Restart All Affected__ (Redémarrer tous les éléments affectés).</span><span class="sxs-lookup"><span data-stu-id="d165d-192">To restart Kafka, use the __Restart__ button and select __Restart All Affected__.</span></span> <span data-ttu-id="d165d-193">Confirmez le redémarrage, puis utilisez le bouton __OK__ une fois l’opération terminée.</span><span class="sxs-lookup"><span data-stu-id="d165d-193">Confirm the restart, and then use the __OK__ button after the operation has completed.</span></span>

    ![Bouton Redémarrer avec l’option Restart All Affected (Redémarrer tous les éléments affectés) en surbrillance](./media/hdinsight-apache-kafka-connect-vpn-gateway/restart-button.png)

11. <span data-ttu-id="d165d-195">Pour désactiver le mode de maintenance, utilisez le bouton __Service Actions__ (Actions du service) et sélectionnez __Désactiver le mode de maintenance__.</span><span class="sxs-lookup"><span data-stu-id="d165d-195">To disable maintenance mode, use the __Service Actions__ button and select __Turn Off Maintenance Mode__.</span></span> <span data-ttu-id="d165d-196">Sélectionnez **OK** pour terminer cette opération.</span><span class="sxs-lookup"><span data-stu-id="d165d-196">Select **OK** to complete this operation.</span></span>

### <a name="connect-to-the-vpn-gateway"></a><span data-ttu-id="d165d-197">Connexion à la passerelle VPN</span><span class="sxs-lookup"><span data-stu-id="d165d-197">Connect to the VPN gateway</span></span>

<span data-ttu-id="d165d-198">Pour vous connecter à la passerelle VPN à partir d’un __client Windows__, suivez la section __Connexion à Azure__ du document [Configuration d’une connexion de point à site à un réseau virtuel à l’aide de PowerShell](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate).</span><span class="sxs-lookup"><span data-stu-id="d165d-198">To connect to the VPN gateway from a __Windows client__, use the __Connect to Azure__ section of the [Configure a Point-to-Site connection](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate) document.</span></span>

## <span data-ttu-id="d165d-199"><a id="python-client"></a> Exemple : client Python</span><span class="sxs-lookup"><span data-stu-id="d165d-199"><a id="python-client"></a> Example: Python client</span></span>

<span data-ttu-id="d165d-200">Pour valider la connectivité à Kafka, procédez comme suit pour créer et exécuter un producteur et un consommateur Python :</span><span class="sxs-lookup"><span data-stu-id="d165d-200">To validate connectivity to Kafka, use the following steps to create and run a Python producer and consumer:</span></span>

1. <span data-ttu-id="d165d-201">Pour récupérer le nom de domaine complet (FQDN) et les adresses IP des nœuds du cluster Kafka, utilisez l’une des méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="d165d-201">Use one of the following methods to retrieve the fully qualified domain name (FQDN) and IP addresses of the nodes in the Kafka cluster:</span></span>

    ```powershell
    $resourceGroupName = "The resource group that contains the virtual network used with HDInsight"

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

    <span data-ttu-id="d165d-202">Ce script suppose que `$resourceGroupName` est le nom du groupe de ressources Azure qui contient le réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="d165d-202">This script assumes that `$resourceGroupName` is the name of the Azure resource group that contains the virtual network.</span></span>

    <span data-ttu-id="d165d-203">Enregistrez les informations retournées afin de les utiliser dans les étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="d165d-203">Save the returned information for use in the next steps.</span></span>

2. <span data-ttu-id="d165d-204">Utilisez ce qui suit pour installer le client [kafka-python](http://kafka-python.readthedocs.io/) :</span><span class="sxs-lookup"><span data-stu-id="d165d-204">Use the following to install the [kafka-python](http://kafka-python.readthedocs.io/) client:</span></span>

        pip install kafka-python

3. <span data-ttu-id="d165d-205">Pour envoyer des données à Kafka, utilisez le code Python suivant :</span><span class="sxs-lookup"><span data-stu-id="d165d-205">To send data to Kafka, use the following Python code:</span></span>

  ```python
  from kafka import KafkaProducer
  # Replace the `ip_address` entries with the IP address of your worker nodes
  # NOTE: you don't need the full list of worker nodes, just one or two.
  producer = KafkaProducer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'])
  for _ in range(50):
      producer.send('testtopic', b'test message')
  ```

    <span data-ttu-id="d165d-206">Remplacez les entrées `'kafka_broker'` par les adresses renvoyées à partir de l’étape 1 de cette section :</span><span class="sxs-lookup"><span data-stu-id="d165d-206">Replace the `'kafka_broker'` entries with the addresses returned from step 1 in this section:</span></span>

    * <span data-ttu-id="d165d-207">Si vous utilisez un __client logiciel VPN__, remplacez les entrées `kafka_broker` avec l’adresse IP de vos nœuds de travail.</span><span class="sxs-lookup"><span data-stu-id="d165d-207">If you are using a __Software VPN client__, replace the `kafka_broker` entries with the IP address of your worker nodes.</span></span>

    * <span data-ttu-id="d165d-208">Si vous avez __activé la résolution de noms via un serveur DNS personnalisé__, remplacez les entrées `kafka_broker` avec le nom de domaine complet des nœuds de travail.</span><span class="sxs-lookup"><span data-stu-id="d165d-208">If you have __enabled name resolution through a custom DNS server__, replace the `kafka_broker` entries with the FQDN of the worker nodes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d165d-209">Ce code envoie la chaîne `test message` à la rubrique `testtopic`.</span><span class="sxs-lookup"><span data-stu-id="d165d-209">This code sends the string `test message` to the topic `testtopic`.</span></span> <span data-ttu-id="d165d-210">La configuration par défaut de Kafka sur HDInsight consiste à créer la rubrique si elle n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="d165d-210">The default configuration of Kafka on HDInsight is to create the topic if it does not exist.</span></span>

4. <span data-ttu-id="d165d-211">Pour récupérer les messages à partir de Kafka, utilisez le code Python suivant :</span><span class="sxs-lookup"><span data-stu-id="d165d-211">To retrieve the messages from Kafka, use the following Python code:</span></span>

   ```python
   from kafka import KafkaConsumer
   # Replace the `ip_address` entries with the IP address of your worker nodes
   # Again, you only need one or two, not the full list.
   # Note: auto_offset_reset='earliest' resets the starting offset to the beginning
   #       of the topic
   consumer = KafkaConsumer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'],auto_offset_reset='earliest')
   consumer.subscribe(['testtopic'])
   for msg in consumer:
     print (msg)
   ```

    <span data-ttu-id="d165d-212">Remplacez les entrées `'kafka_broker'` par les adresses renvoyées à partir de l’étape 1 de cette section :</span><span class="sxs-lookup"><span data-stu-id="d165d-212">Replace the `'kafka_broker'` entries with the addresses returned from step 1 in this section:</span></span>

    * <span data-ttu-id="d165d-213">Si vous utilisez un __client logiciel VPN__, remplacez les entrées `kafka_broker` avec l’adresse IP de vos nœuds de travail.</span><span class="sxs-lookup"><span data-stu-id="d165d-213">If you are using a __Software VPN client__, replace the `kafka_broker` entries with the IP address of your worker nodes.</span></span>

    * <span data-ttu-id="d165d-214">Si vous avez __activé la résolution de noms via un serveur DNS personnalisé__, remplacez les entrées `kafka_broker` avec le nom de domaine complet des nœuds de travail.</span><span class="sxs-lookup"><span data-stu-id="d165d-214">If you have __enabled name resolution through a custom DNS server__, replace the `kafka_broker` entries with the FQDN of the worker nodes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d165d-215">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d165d-215">Next steps</span></span>

<span data-ttu-id="d165d-216">Pour plus d’informations sur l’utilisation de HDInsight avec un réseau virtuel, consultez le document [Étendre HDInsight à l’aide d’un réseau virtuel Azure](hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="d165d-216">For more information on using HDInsight with a virtual network, see the [Extend Azure HDInsight using an Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span>

<span data-ttu-id="d165d-217">Pour plus d’informations sur la création d’un réseau virtuel Azure avec une passerelle VPN de point à site, consultez les documents suivants :</span><span class="sxs-lookup"><span data-stu-id="d165d-217">For more information on creating an Azure Virtual Network with Point-to-Site VPN gateway, see the following documents:</span></span>

* [<span data-ttu-id="d165d-218">Configuration d’une connexion point à site à un réseau virtuel à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="d165d-218">Configure a Point-to-Site connection using the Azure portal</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md)

* [<span data-ttu-id="d165d-219">Configuration d’une connexion de point à site à un réseau virtuel à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="d165d-219">Configure a Point-to-Site connection using Azure PowerShell</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

<span data-ttu-id="d165d-220">Pour plus d’informations sur l’utilisation de Kafka sur HDInsight, consultez les documents suivants :</span><span class="sxs-lookup"><span data-stu-id="d165d-220">For more information on working with Kafka on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="d165d-221">Prise en main de Kafka sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="d165d-221">Get started with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="d165d-222">MirrorMaker permet de créer un réplica Kafka sur un cluster HDInsight (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="d165d-222">Use mirroring with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
