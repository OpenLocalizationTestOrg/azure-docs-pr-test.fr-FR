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
# <a name="connect-tookafka-on-hdinsight-preview-through-an-azure-virtual-network"></a>Se connecter tooKafka sur HDInsight (aperçu) via un réseau virtuel Azure

Découvrez comment toodirectly connecter tooKafka sur HDInsight à l’aide de réseaux virtuels Azure. Ce document fournit des informations sur la connexion tooKafka hello suivant des configurations à l’aide de :

* À partir des ressources d’un réseau local. Cette connexion est établie à l’aide d’un périphérique VPN (logiciel ou matériel) sur votre réseau local.
* À partir d’un environnement de développement à l’aide d’un client de logiciel VPN.

## <a name="architecture-and-planning"></a>Architecture et planification

HDInsight n’autorise pas de connexion directe tooKafka via hello internet public. Au lieu de cela, les clients Kafka (producteurs et consommateurs) doivent utiliser un des hello des méthodes de connexion suivantes :

* Exécuter le client de hello Bonjour même réseau virtuel que Kafka sur HDInsight. Cette configuration est utilisée dans hello [démarrer avec Apache Kafka (aperçu) sur HDInsight](hdinsight-apache-kafka-get-started.md) document. Hello exécute client directement sur hello HDInsight des nœuds de cluster ou sur un autre ordinateur virtuel dans hello même réseau.

* Connecter un réseau privé, par exemple, votre réseau local, réseau virtuel de toohello. Cette configuration permet aux clients dans votre travail de toodirectly de réseau local avec Kafka. tooenable cette configuration, effectuer hello tâches suivantes :

    1. Créez un réseau virtuel.
    2. Créez une passerelle VPN qui utilise une configuration de site à site. configuration de Hello utilisée dans ce document connecte tooa périphérique de passerelle VPN de votre réseau local.
    3. Créer un serveur DNS dans le réseau virtuel de hello.
    4. Configurer le transfert entre le serveur DNS hello dans chaque réseau.
    5. Installez Kafka sur HDInsight dans le réseau virtuel de hello.

    Pour plus d’informations, consultez hello [connecter tooKafka à partir d’un réseau local](#on-premises) section. 

* Se connecter à l’aide d’une passerelle VPN et le client VPN du réseau virtuel toohello des ordinateurs individuels. tooenable cette configuration, effectuer hello tâches suivantes :

    1. Créez un réseau virtuel.
    2. Créez une passerelle VPN qui utilise une configuration de point à site. Cette configuration offre un client VPN qui peut être installé sur les clients Windows.
    3. Installez Kafka sur HDInsight dans le réseau virtuel de hello.
    4. Configurez Kafka pour la publication d’adresses IP. Cette configuration permet de hello tooconnect de client à l’aide de noms de domaine à la place d’adressage IP.
    5. Téléchargez et utilisez le client VPN de hello sur le système de développement hello.

    Pour plus d’informations, consultez hello [connecter tooKafka avec un client VPN](#vpnclient) section.

    > [!WARNING]
    > Cette configuration est recommandée uniquement à des fins de développement en raison de hello limites suivantes :
    >
    > * Chaque client doit se connecter à l’aide d’un client de logiciel VPN. Azure fournit uniquement un client Windows.
    > * client de Hello ne transmet pas de nom résolution demandes toohello réseau virtuel, vous devez donc utiliser toocommunicate avec Kafka d’adressage IP. Communication IP nécessite une configuration supplémentaire sur le cluster de Kafka de hello.

Pour plus d’informations sur l’utilisation de HDInsight dans un réseau virtuel, consultez [Étendre HDInsight à l’aide de réseaux virtuels Azure](./hdinsight-extend-hadoop-virtual-network.md).

## <a id="on-premises"></a>Se connecter tooKafka à partir d’un réseau local

toocreate un cluster Kafka qui communique avec votre réseau local, suivez les étapes de hello Bonjour [réseau de se connecter de HDInsight tooyour local](./connect-on-premises-network.md) document.

> [!IMPORTANT]
> Lorsque vous créez le cluster HDInsight de hello, sélectionnez hello __Kafka__ type de cluster.

Les étapes suivantes créent hello configuration suivante :

* Réseau virtuel Azure
* Passerelle VPN de site à site
* Compte de stockage Azure (utilisé par HDInsight)
* Kafka sur HDInsight

tooverify qu’un client Kafka peut se connecter à toohello cluster à partir de locale, utilisez les étapes de hello Bonjour [exemple : client Python](#python-client) section.

## <a id="vpnclient"></a>Se connecter tooKafka avec un client VPN

Utilisez les étapes de hello dans cette hello toocreate de section configuration suivante :

* Réseau virtuel Azure
* Passerelle VPN de point à site
* Compte Stockage Azure (utilisé par HDInsight)
* Kafka sur HDInsight

1. Suivez les étapes de hello Bonjour [fonctionne avec des certificats auto-signés pour des connexions de Point-to-site](../vpn-gateway/vpn-gateway-certificates-point-to-site.md) document. Ce document crée des certificats hello nécessaires pour la passerelle de hello.

2. Ouvrez une invite de PowerShell et utilisez hello suivant toolog de code dans tooyour abonnement Azure :

    ```powershell
    Add-AzureRmAccount
    # If you have multiple subscriptions, uncomment tooset hello subscription
    #Select-AzureRmSubscription -SubscriptionName "name of your subscription"
    ```

3. Utilisez hello suivant variables toocreate du code qui contiennent des informations de configuration :

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

4. Groupe de ressources Azure hello toocreate et le réseau virtuel de code suivant de hello d’utilisation :

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
    > Il peut prendre quelques minutes pour que cette toocomplete de processus.

5. Utilisez hello suivant code toocreate hello compte de stockage Azure et blob conteneur :

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

6. Utilisez hello suivant du cluster HDInsight de code toocreate hello :

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
  > Ce processus prend environ 20 minutes toocomplete.

8. Utilisez hello suivant l’applet de commande tooretrieve hello URL pour le client de VPN Windows hello pour le réseau virtuel de hello :

    ```powershell
    Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName `
        -VirtualNetworkGatewayName $vpnName `
        -ProcessorArchitecture Amd64
    ```

    client de VPN Windows hello toodownload, utilisez hello retourné URI dans votre navigateur web.

### <a name="configure-kafka-for-ip-advertising"></a>Configuration de Kafka pour la publication d’adresses IP

Par défaut, soigneur renvoie le nom de domaine de hello Hello Kafka courtiers tooclients. Cette configuration ne fonctionne pas avec hello client VPN logiciel car il ne peut pas utiliser la résolution de noms pour les entités de réseau virtuel de hello. Pour cette configuration, utilisez hello qui suit les adresses IP de tooadvertise Kafka tooconfigure des étapes au lieu des noms de domaine :

1. À l’aide d’un navigateur web, accédez à toohttps://CLUSTERNAME.azurehdinsight.net. Remplacez __CLUSTERNAME__ avec nom hello Hello Kafka sur le cluster HDInsight.

    Lorsque vous y êtes invité, utilisez le nom d’utilisateur hello HTTPS et le mot de passe pour le cluster de hello. Hello l’interface utilisateur de Ambari Web de cluster de hello s’affiche.

2. Sélectionnez des informations tooview sur Kafka, __Kafka__ à partir de la liste hello sur hello gauche.

    ![Liste des services avec l’option Kafka en surbrillance](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-service.png)

3. tooview configuration de Kafka, sélectionnez __configurations__ à partir du haut et au milieu hello.

    ![Liens vers les configurations Kafka](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-config.png)

4. toofind hello __kafka-env__ configuration, entrez `kafka-env` Bonjour __filtre__ champ sur le coin supérieur droit de hello.

    ![Configuration Kafka, pour kafka-env](./media/hdinsight-apache-kafka-connect-vpn-gateway/search-for-kafka-env.png)

5. les adresses IP de tooadvertise Kafka tooconfigure, ajouter hello suivant en bas de toohello texte Hello __kafka-env-modèle__ champ :

    ```
    # Configure Kafka tooadvertise IP addresses instead of FQDN
    IP_ADDRESS=$(hostname -i)
    echo advertised.listeners=$IP_ADDRESS
    sed -i.bak -e '/advertised/{/advertised@/!d;}' /usr/hdp/current/kafka-broker/conf/server.properties
    echo "advertised.listeners=PLAINTEXT://$IP_ADDRESS:9092" >> /usr/hdp/current/kafka-broker/conf/server.properties
    ```

6. interface hello tooconfigure qui écoute Kafka, entrez `listeners` Bonjour __filtre__ champ sur le coin supérieur droit de hello.

7. tooconfigure toolisten Kafka sur toutes les interfaces réseau, de modifier la valeur hello Bonjour __écouteurs__ champ trop`PLAINTEXT://0.0.0.0:9092`.

8. modifications de configuration toosave hello, utilisez hello __enregistrer__ bouton. Entrez un message texte qui décrit les modifications de hello. Sélectionnez __OK__ une fois hello modifications ont été enregistrées.

    ![Bouton pour enregistrer la configuration](./media/hdinsight-apache-kafka-connect-vpn-gateway/save-button.png)

9. erreurs tooprevent lors du redémarrage Kafka, utilisez hello __Actions Service__ sélectionnez __activer sur le Mode Maintenance__. Sélectionnez OK toocomplete cette opération.

    ![Actions de service, avec l’option Activer le mode de maintenance en surbrillance](./media/hdinsight-apache-kafka-connect-vpn-gateway/turn-on-maintenance-mode.png)

10. toorestart Kafka, utilisez hello __redémarrer__ sélectionnez __redémarrer l’affectées toutes les__. Confirmer le redémarrage de hello et utilisez hello __OK__ bouton une fois l’opération de hello.

    ![Bouton Redémarrer avec l’option Restart All Affected (Redémarrer tous les éléments affectés) en surbrillance](./media/hdinsight-apache-kafka-connect-vpn-gateway/restart-button.png)

11. mode de maintenance toodisable, utilisez hello __Actions Service__ sélectionnez __activer en Mode Maintenance__. Sélectionnez **OK** toocomplete cette opération.

### <a name="connect-toohello-vpn-gateway"></a>Passerelle VPN de toohello de connexion

tooconnect toohello passerelle VPN un __client Windows__, utilisez hello __connecter tooAzure__ section Hello [configurer une connexion de Point-to-Site](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate) document.

## <a id="python-client"></a> Exemple : client Python

toovalidate connectivité tooKafka, utilisez hello suivant les étapes toocreate et exécutez un producteur de Python et un consommateur :

1. Utilisez une des hello suivant hello tooretrieve de méthodes entièrement qualifié le nom de domaine (FQDN) et les adresses IP des nœuds hello Bonjour cluster de Kafka :

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

    Ce script suppose que `$resourceGroupName` est le nom hello hello Azure du groupe de ressources qui contient le réseau virtuel de hello.

    Enregistrez hello a retourné des informations pour une utilisation dans les étapes suivantes hello.

2. Hello utilisation suivant tooinstall hello [kafka-python](http://kafka-python.readthedocs.io/) client :

        pip install kafka-python

3. toosend données tooKafka, hello utilisation après le code Python :

  ```python
  from kafka import KafkaProducer
  # Replace hello `ip_address` entries with hello IP address of your worker nodes
  # NOTE: you don't need hello full list of worker nodes, just one or two.
  producer = KafkaProducer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'])
  for _ in range(50):
      producer.send('testtopic', b'test message')
  ```

    Remplacez hello `'kafka_broker'` entrées avec des adresses hello retourné à l’étape 1 de cette section :

    * Si vous utilisez un __client logiciel VPN__, remplacez hello `kafka_broker` entrées avec l’adresse IP de hello vos nœuds de travail.

    * Si vous avez __activé la résolution de noms via un serveur DNS personnalisé__, remplacez hello `kafka_broker` entrées avec hello FQDN hello de nœuds de travail.

    > [!NOTE]
    > Ce code envoie la chaîne de hello `test message` toohello rubrique `testtopic`. Hello est par défaut de Kafka sur HDInsight rubrique de hello toocreate s’il n’existe pas.

4. messages de type hello tooretrieve de Kafka, utilisez hello suivant code Python :

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

    Remplacez hello `'kafka_broker'` entrées avec des adresses hello retourné à l’étape 1 de cette section :

    * Si vous utilisez un __client logiciel VPN__, remplacez hello `kafka_broker` entrées avec l’adresse IP de hello vos nœuds de travail.

    * Si vous avez __activé la résolution de noms via un serveur DNS personnalisé__, remplacez hello `kafka_broker` entrées avec hello FQDN hello de nœuds de travail.

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur l’utilisation de HDInsight avec un réseau virtuel, consultez hello [étendre Azure HDInsight à l’aide d’un réseau virtuel Azure](hdinsight-extend-hadoop-virtual-network.md) document.

Pour plus d’informations sur la création d’un réseau virtuel Azure avec la passerelle Point-to-Site VPN, consultez hello suivant des documents :

* [Configurer une connexion de Point à Site à l’aide de hello portail Azure](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md)

* [Configuration d’une connexion de point à site à un réseau virtuel à l’aide de PowerShell](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

Pour plus d’informations sur l’utilisation avec Kafka sur HDInsight, consultez hello suivant des documents :

* [Prise en main de Kafka sur HDInsight](hdinsight-apache-kafka-get-started.md)
* [MirrorMaker permet de créer un réplica Kafka sur un cluster HDInsight (version préliminaire)](hdinsight-apache-kafka-mirroring.md)
