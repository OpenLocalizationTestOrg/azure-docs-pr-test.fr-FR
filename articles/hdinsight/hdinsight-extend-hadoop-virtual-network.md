---
title: aaaExtend HDInsight avec Virtual Network - Azure | Documents Microsoft
description: "Découvrez comment toouse réseau virtuel Azure tooconnect HDInsight tooother cloud ressources ou des ressources dans votre centre de données"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 37b9b600-d7f8-4cb1-a04a-0b3a827c6dcc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: larryfr
ms.openlocfilehash: ba80be4d9f280c6c62fa8acc996ef5f921acdbbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="extend-azure-hdinsight-using-an-azure-virtual-network"></a>Étendre HDInsight à l’aide d’un réseau virtuel Azure

Découvrez comment toouse HDInsight avec un [réseau virtuel Azure](../virtual-network/virtual-networks-overview.md). À l’aide d’un réseau virtuel Azure permet de hello les scénarios suivants :

* Connexion tooHDInsight directement à partir d’un réseau local.

* Connexion HDInsight toodata stocke dans un réseau virtuel Azure.

* Directement l’accès aux services Hadoop qui ne sont pas disponibles publiquement sur hello internet. Par exemple, les API Kafka ou hello HBase Java API.

> [!WARNING]
> informations Hello dans ce document nécessitent une compréhension de la mise en réseau TCP/IP. Si vous n’êtes pas familiarisé avec la mise en réseau TCP/IP, vous devez en partenariat avec personne avant d’apporter des modifications tooproduction réseaux.

## <a name="planning"></a>Planification

Hello Voici les questions de hello auxquelles vous devez répondre lors de la planification tooinstall HDInsight dans un réseau virtuel :

* Avez-vous besoin de tooinstall HDInsight dans un réseau virtuel existant ? Ou bien créez-vous un réseau ?

    Si vous utilisez un réseau virtuel existant, vous devrez peut-être la configuration du réseau toomodify hello avant que vous puissiez installer HDInsight. Pour plus d’informations, consultez hello [ajouter le réseau virtuel tooan HDInsight](#existingvnet) section.

* Voulez-vous contenant le réseau virtuel de HDInsight tooanother du réseau virtuel hello tooconnect ou votre réseau local ?

    tooeasily travail avec des ressources sur des réseaux, vous pouvez peut-être toocreate DNS personnalisé et configurer la redirection DNS. Pour plus d’informations, consultez hello [connecter plusieurs réseaux](#multinet) section.

* Voulez-vous vraiment toorestrict/redirection tooHDInsight de trafic entrant ou sortant ?

    HDInsight doit avoir un communication avec des adresses IP spécifiques dans le centre de données Azure hello illimité. Il existe également plusieurs ports qui doivent être autorisés au travers de pare-feu pour la communication du client. Pour plus d’informations, consultez hello [contrôler le trafic réseau](#networktraffic) section.

## <a id="existingvnet"></a>Ajouter le réseau virtuel tooan HDInsight

Utilisez les étapes hello dans toodiscover de cette section Comment tooadd un tooan HDInsight nouveau existant du réseau virtuel Azure.

> [!NOTE]
> Vous ne pouvez pas ajouter un cluster HDInsight existant à un réseau virtuel.

1. Si vous utilisez un classique ou le modèle de déploiement de gestionnaire de ressources pour le réseau virtuel de hello ?

    HDInsight 3.4 et versions ultérieures nécessitent un réseau virtuel Resource Manager. Les versions antérieures de HDInsight nécessitaient un réseau virtuel classique.

    Si votre réseau existant est un réseau virtuel classique, vous devez créer un réseau virtuel du Gestionnaire de ressources et connectez-vous hello deux. [Connexion classique des réseaux virtuels toonew réseaux virtuels](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).

    Une fois joint, HDInsight sur hello Gestionnaire de ressources du réseau peut interagir avec les ressources réseau classiques de hello.

2. Voulez-vous utiliser un tunneling forcé ? Le tunneling forcé est un paramètre de sous-réseau qui force le périphérique tooa de trafic Internet sortant pour l’inspection et la journalisation. HDInsight ne prend pas en charge le tunneling forcé. Supprimez le tunneling forcé avant d’installer HDInsight dans un sous-réseau, ou de créer un sous-réseau pour HDInsight.

3. Utilisez-vous des groupes de sécurité réseau, itinéraires définis par l’utilisateur ou le trafic toorestrict de dispositifs de réseau virtuel dans ou en dehors du réseau virtuel de hello ?

    Un service géré, HDInsight requiert un accès illimité tooseveral des adresses IP dans le centre de données Azure hello. communication tooallow avec ces adresses IP, mettre à jour les groupes de sécurité réseau existant ou des itinéraires de défini par l’utilisateur.

    HDInsight héberge plusieurs services qui une série de ports. Ne bloquent pas le trafic des ports toothese. Pour obtenir la liste de tooallow de ports à travers des pare-feu d’appliance virtuelle, consultez hello [sécurité](#security) section.

    toofind votre configuration de sécurité existante, hello utilisation suivant les commandes Azure PowerShell ou CLI d’Azure :

    * groupes de sécurité réseau ;

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
        get-azurermnetworksecuritygroup -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
        az network nsg list --resource-group $RESOURCEGROUP
        ```

        Pour plus d’informations, consultez hello [résoudre les groupes de sécurité réseau](../virtual-network/virtual-network-nsg-troubleshoot-portal.md) document.

        > [!IMPORTANT]
        > Les règles de groupe de sécurité réseau sont appliquées dans un ordre basé sur leur priorité. Hello première règle qui correspond au modèle de trafic hello est appliquée, et aucune autre ne sont appliquées à ce trafic. Ordre des règles à partir de tooleast plus permissif permissif. Pour plus d’informations, consultez hello [filtrer le trafic réseau avec les groupes de sécurité réseau](../virtual-network/virtual-networks-nsg.md) document.

    * Itinéraires définis par l’utilisateur

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
        get-azurermroutetable -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
        az network route-table list --resource-group $RESOURCEGROUP
        ```

        Pour plus d’informations, consultez hello [résoudre les itinéraires](../virtual-network/virtual-network-routes-troubleshoot-portal.md) document.

4. Créer un cluster HDInsight et sélectionnez hello réseau virtuel Azure lors de la configuration. Utilisez les étapes de hello Bonjour suivant le processus de création de documents toounderstand hello cluster :

    * [Créer HDInsight à l’aide de hello portail Azure](hdinsight-hadoop-create-linux-clusters-portal.md)
    * [Créer un cluster HDInsight à l’aide d’Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
    * [Créer un cluster HDInsight à l’aide de l’interface de ligne de commande Azure 1.0](hdinsight-hadoop-create-linux-clusters-azure-cli.md)
    * [Créer un cluster HDInsight à l’aide d’un modèle Azure Resource Manager](hdinsight-hadoop-create-linux-clusters-arm-templates.md)

  > [!IMPORTANT]
  > Ajout de HDInsight tooa des réseaux virtuels sont une étape de configuration facultatives. Être sûr de réseau virtuel hello de tooselect lors de la configuration de cluster de hello.

## <a id="multinet"></a>Connexion de plusieurs réseaux

défi le plus important Hello avec une configuration de réseau multiples est la résolution de noms entre des réseaux hello.

Azure assure la résolution de noms pour les services Azure installés dans un réseau virtuel. Cette résolution de nom intégré permet toohello de tooconnect HDInsight suivant des ressources à l’aide d’un nom de domaine complet (FQDN) :

* Est disponible sur n’importe quelle ressource hello internet. Par exemple, microsoft.com ou google.com.

* N’importe quelle ressource est hello dans même réseau virtuel Azure, à l’aide de hello __nom DNS interne__ de ressource de hello. Par exemple, lorsque vous utilisez la résolution de noms par défaut hello, hello Voici exemple interne DNS noms tooHDInsight attribué de nœuds de travail :

    * wn0-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net
    * wn2-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net

    Les deux nœuds peuvent communiquer directement entre eux et avec d’autres nœuds dans HDInsight en utilisant des noms DNS internes.

résolution de noms par défaut Hello est __pas__ autoriser HDInsight tooresolve noms hello de ressources dans des réseaux qui sont jointes toohello des réseaux virtuels. Par exemple, il est commun toojoin toohello des réseaux virtuels du réseau de votre site. Uniquement hello par défaut résolution du nom, HDInsight ne peut pas accéder aux ressources réseau local de hello par nom. Hello inverse est également true, les ressources de votre réseau local ne peut pas accéder aux ressources de réseau virtuel de hello par nom.

> [!WARNING]
> Vous devez créer un serveur DNS personnalisé hello et configurer toouse de réseau virtuel hello avant la création d’hello cluster HDInsight.

résolution de noms tooenable entre le réseau virtuel de hello et les ressources dans les réseaux jointes, vous devez effectuer hello suivant des actions :

1. Créer un serveur DNS personnalisé Bonjour Azure Virtual Network où vous prévoyez de tooinstall HDInsight.

2. Configurer hello réseau virtuel toouse hello serveur DNS personnalisé.

3. Recherche hello Qu'azure affecté le suffixe DNS pour votre réseau virtuel. Cette valeur est trop similaire`0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`. Pour plus d’informations sur la recherche de suffixe DNS de hello, consultez hello [exemple : Custom DNS](#example-dns) section.

4. Configurer le transfert entre les serveurs DNS de hello. configuration de Hello dépend du type hello du réseau à distance.

    * Si le réseau à distance de hello est un réseau local, configurez DNS comme suit :
        
        * __DNS personnalisé__ (dans le réseau virtuel de hello) :

            * Transférer les demandes pour le suffixe DNS de hello du programme de résolution de Azure récursive toohello hello réseau virtuel (168.63.129.16). Azure gère les demandes de ressources de réseau virtuel de hello

            * Transférer toutes les autres demandes toohello locale DNS server. Hello locale DNS gère toutes les autres demandes de résolution de nom, y compris les requêtes de ressources internet telles que Microsoft.com.

        * __DNS local__: demandes de hello réseau virtuel DNS suffixe toohello un serveur DNS personnalisé. un serveur DNS personnalisé Hello transmet ensuite le programme de résolution toohello récursive Azure.

        Demandes de configuration de cette itinéraires pour complet des noms de domaine qui contiennent le suffixe DNS hello hello réseau virtuel toohello un serveur DNS personnalisé. Toutes les autres demandes (même pour les adresses internet publics) sont gérées par le serveur DNS hello local.

    * Si le réseau à distance de hello est un autre réseau virtuel Azure, configurez DNS comme suit :

        * __DNS personnalisé__ (dans chaque réseau virtuel) :

            * Demandes pour le suffixe DNS de hello des réseaux virtuels de hello sont transférées toohello des serveurs DNS personnalisés. Hello DNS de chaque réseau virtuel est chargé de résoudre des ressources au sein de son réseau.

            * Transférer toutes les autres demandes toohello récursive Azure programme de résolution. programme de résolution récursive Hello est responsable de la résolution local et les ressources internet.

        serveur DNS de Hello pour chaque réseau transfère les demandes toohello autres, en fonction de suffixe DNS. Autres requêtes sont résolues à l’aide du programme de résolution récursive Azure hello.

    Pour obtenir un exemple de chaque configuration, consultez hello [exemple : Custom DNS](#example-dns) section.

Pour plus d’informations, consultez hello [résolution de noms pour les machines virtuelles et Instances de rôle](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) document.

## <a name="directly-connect-toohadoop-services"></a>Se connecter directement des services de tooHadoop

La plupart des documentation sur HDInsight suppose que vous avez des cluster toohello d’accès sur hello internet. Par exemple, que vous pouvez vous connecter à cluster toohello à https://CLUSTERNAME.azurehdinsight.net. Cette adresse utilise la passerelle publique hello, qui n’est pas disponible si vous avez utilisé des groupes de sécurité réseau ou d’accès toorestrict UDRs hello internet.

tooconnect tooAmbari et autres pages web via un réseau virtuel de hello, utilisez hello comme suit :

1. noms de domaine complet interne toodiscover hello (FQDN) des nœuds de cluster HDInsight hello, utilisez une des méthodes suivantes de hello :

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

    Dans la liste hello de nœuds retournés, rechercher hello nom de domaine complet pour hello noeuds head, hello FQDN tooconnect tooAmbari et autres services web. Par exemple, utilisez `http://<headnode-fqdn>:8080` tooaccess Ambari.

    > [!IMPORTANT]
    > Certains services hébergés sur les nœuds principaux hello sont uniquement actifs sur un seul nœud à la fois. Si vous essayez d’accéder à un service sur un seul nœud principal, et retourne une erreur 404, basculez toohello autre nœud principal.

2. nœud de hello toodetermine et de port d’un service est disponible, consultez hello [Ports utilisés par les services de Hadoop dans HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.

## <a id="networktraffic"></a> Contrôler le trafic réseau

Le trafic réseau dans des réseaux virtuels Azure peut être contrôlé à l’aide de hello méthodes suivantes :

* **Groupes de sécurité réseau** (NSG) permettent de réseau de toohello toofilter trafic entrant et sortant. Pour plus d’informations, consultez hello [filtrer le trafic réseau avec les groupes de sécurité réseau](../virtual-network/virtual-networks-nsg.md) document.

    > [!WARNING]
    > HDInsight ne prend pas en charge la restriction du trafic sortant.

* **Itinéraires définis par l’utilisateur** (UDR) définissent le flux de trafic entre les ressources réseau de hello. Pour plus d’informations, consultez hello [itinéraires définis par l’utilisateur et le transfert IP](../virtual-network/virtual-networks-udr-overview.md) document.

* **Réseau virtuel** répliquer fonctionnalité hello des périphériques tels que les routeurs et pare-feu. Pour plus d’informations, consultez hello [dispositifs réseau](https://azure.microsoft.com/solutions/network-appliances) document.

Un service géré, HDInsight nécessite les services de gestion et de contrôle d’intégrité de tooAzure Bonjour Azure cloud un accès illimité. Lorsque vous utilisez des groupes de sécurité réseau et des itinéraires définis par l’utilisateur, vous devez vous assurer que ces services peuvent toujours communiquer avec HDInsight.

HDInsight expose des services sur plusieurs ports. Lorsque vous utilisez un pare-feu d’appliance virtuelle, vous devez autoriser le trafic sur hello ports utilisés pour ces services. Pour plus d’informations, consultez hello [ports requis].

### <a id="hdinsight-ip"></a> HDInsight avec des groupes de sécurité réseau et des itinéraires définis par l’utilisateur

Si vous prévoyez d’utiliser **groupes de sécurité réseau** ou **itinéraires définis par l’utilisateur** toocontrol le trafic réseau, effectuer hello suivant des actions avant d’installer HDInsight :

1. Identifiez hello région Azure que vous envisagez de toouse pour HDInsight.

2. Identifiez les adresses IP hello requis par HDInsight. Pour plus d’informations, consultez hello [les adresses IP requises par HDInsight](#hdinsight-ip) section.

3. Créer ou modifier des groupes de sécurité réseau hello ou défini par l’utilisateur les itinéraires de sous-réseau hello que vous envisagez de tooinstall HDInsight dans.

    * __Groupes de sécurité réseau__: autoriser __entrant__ le trafic sur le port __443__ à partir d’adresses IP de hello.
    * __Itinéraires définis par l’utilisateur__: créer une itinéraire tooeach une adresse IP et de définir hello __type de tronçon suivant__ too__Internet__.

Pour plus d’informations sur les groupes de sécurité réseau ou des itinéraires définis par l’utilisateur, consultez hello suivant la documentation :

* [Groupe de sécurité réseau](../virtual-network/virtual-networks-nsg.md)

* [Itinéraires définis par l’utilisateur](../virtual-network/virtual-networks-udr-overview.md)

#### <a name="forced-tunneling"></a>Tunneling forcé

Le tunneling forcé est une configuration de routage défini par l’utilisateur où tout le trafic à partir d’un sous-réseau de réseau tooa forcé ou emplacement, tel que votre réseau local. HDInsight ne prend __pas__ en charge le tunneling forcé.

## <a id="hdinsight-ip"></a> Adresses IP requises

> [!IMPORTANT]
> Hello Azure health et services de gestion doivent être en mesure de toocommunicate avec HDInsight. Si vous utilisez des groupes de sécurité réseau ou des itinéraires définis par l’utilisateur, vous pouvez autoriser le trafic hello adresses IP pour ces tooreach services HDInsight.
>
> Si vous n’utilisez pas le trafic de toocontrol itinéraires définis par l’utilisateur ou de groupes de sécurité réseau, vous pouvez ignorer cette section.

Si vous utilisez des groupes de sécurité réseau ou des itinéraires définis par l’utilisateur, vous devez autoriser le trafic hello Azure health et gestion des services tooreach HDInsight. Utilisez hello suivant les étapes toofind hello adresses IP qui doivent être autorisées :

1. Vous devez toujours autoriser le trafic à partir de hello suivant des adresses IP :

    | Adresse IP | Port autorisé | Direction |
    | ---- | ----- | ----- |
    | 168.61.49.99 | 443 | Trafic entrant |
    | 23.99.5.239 | 443 | Trafic entrant |
    | 168.61.48.131 | 443 | Trafic entrant |
    | 138.91.141.162 | 443 | Trafic entrant |

2. Si votre cluster HDInsight est dans un des hello suivant des régions, vous devez autoriser le trafic provenant d’adresses IP de hello répertoriées pour la région de hello :

    > [!IMPORTANT]
    > Si hello région Azure que vous utilisez n’est pas répertorié, utilisez uniquement les adresses IP quatre hello à l’étape 1.

    | Pays | Région | Adresses IP autorisées | Port autorisé | Direction |
    | ---- | ---- | ---- | ---- | ----- |
    | Asie | Est de l'Asie | 23.102.235.122</br>52.175.38.134 | 443 | Trafic entrant |
    | &nbsp; | Asie du Sud-Est | 13.76.245.160</br>13.76.136.249 | 443 | Trafic entrant |
    | Australie | Est de l’Australie | 104.210.84.115</br>13.75.152.195 | 443 | Trafic entrant |
    | &nbsp; | Sud-est de l’Australie | 13.77.2.56</br>13.77.2.94 | 443 | Trafic entrant |
    | Brésil | Sud du Brésil | 191.235.84.104</br>191.235.87.113 | 443 | Trafic entrant |
    | Canada | Est du Canada | 52.229.127.96</br>52.229.123.172 | 443 | Trafic entrant |
    | &nbsp; | Centre du Canada | 52.228.37.66</br>52.228.45.222 | 443 | Trafic entrant |
    | Chine | Chine du Nord | 42.159.96.170</br>139.217.2.219 | 443 | Trafic entrant |
    | &nbsp; | Chine orientale | 42.159.198.178</br>42.159.234.157 | 443 | Trafic entrant |
    | Europe | Europe du Nord | 52.164.210.96</br>13.74.153.132 | 443 | Trafic entrant |
    | &nbsp; | Europe de l'Ouest| 52.166.243.90</br>52.174.36.244 | 443 | Trafic entrant |
    | Allemagne | Centre de l’Allemagne | 51.4.146.68</br>51.4.146.80 | 443 | Trafic entrant |
    | &nbsp; | Nord-Est de l’Allemagne | 51.5.150.132</br>51.5.144.101 | 443 | Trafic entrant |
    | Inde | Inde centrale | 52.172.153.209</br>52.172.152.49 | 443 | Trafic entrant |
    | Japon | Est du Japon | 13.78.125.90</br>13.78.89.60 | 443 | Trafic entrant |
    | &nbsp; | Ouest du Japon | 40.74.125.69</br>138.91.29.150 | 443 | Trafic entrant |
    | Corée du Sud | Centre de la Corée | 52.231.39.142</br>52.231.36.209 | 433 | Trafic entrant |
    | &nbsp; | Corée du Sud | 52.231.203.16</br>52.231.205.214 | 443 | Trafic entrant
    | Royaume-Uni | Ouest du Royaume-Uni | 51.141.13.110</br>51.141.7.20 | 443 | Trafic entrant |
    | &nbsp; | Sud du Royaume-Uni | 51.140.47.39</br>51.140.52.16 | 443 | Trafic entrant |
    | États-Unis | Centre des États-Unis | 13.67.223.215</br>40.86.83.253 | 443 | Trafic entrant |
    | &nbsp; | États-Unis - partie centrale septentrionale | 157.56.8.38</br>157.55.213.99 | 443 | Trafic entrant |
    | &nbsp; | Centre-Ouest des États-Unis | 52.161.23.15</br>52.161.10.167 | 443 | Trafic entrant |
    | &nbsp; | Ouest des États-Unis 2 | 52.175.211.210</br>52.175.222.222 | 443 | Trafic entrant |

    Pour plus d’informations sur l’IP de hello des adresses toouse pour Azure Government, consultez hello [Azure Government Intelligence + Analytique](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics) document.

3. Si vous utilisez un serveur DNS personnalisé avec votre réseau virtuel, vous devez également autoriser l’accès à partir de __168.63.129.16__. Cette adresse est celle d’un programme de résolution récursive d’Azure. Pour plus d’informations, consultez hello [la résolution de noms pour les ordinateurs virtuels et de rôle instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) document.

Pour plus d’informations, consultez hello [contrôler le trafic réseau](#networktraffic) section.

## <a id="hdinsight-ports"></a> Ports requis

Si vous prévoyez d’utiliser un réseau **pare-feu d’appliance virtuelle** toosecure hello réseau virtuel, et vous devez autoriser le trafic sortant sur hello suivant des ports :

* 53
* 443
* 1433
* 11000-11999
* 14000-14999

Pour obtenir la liste des ports utilisés pour des services spécifiques, consultez hello [Ports utilisés par les services de Hadoop dans HDInsight](hdinsight-hadoop-port-settings-for-services.md) document.

Pour plus d’informations sur les règles de pare-feu pour les équipements virtuels, consultez hello [scénario d’appliance virtuelle](../virtual-network/virtual-network-scenario-udr-gw-nva.md) document.

## <a id="hdinsight-nsg"></a>Exemple : groupes de sécurité réseau avec HDInsight

exemples Hello dans cette section illustrent le fonctionnement des règles de groupe de sécurité réseau toocreate qui autorisent des services de gestion Azure toocommunicate HDInsight avec hello. Avant d’utiliser les exemples de hello, ajustez hello IP adresses toomatch hello ceux pour hello région Azure que vous utilisez. Vous pouvez trouver ces informations dans hello [HDInsight avec des groupes de sécurité réseau et les itinéraires définis par l’utilisateur](#hdinsight-ip) section.

### <a name="azure-resource-management-template"></a>Modèle de gestion des ressources Azure

Hello modèle de gestion des ressources suivant crée un réseau virtuel qui restreint le trafic entrant, mais autorise le trafic à partir d’adresses IP de hello requis par HDInsight. Ce modèle crée également un cluster HDInsight dans le réseau virtuel de hello.

* [Déployer un réseau virtuel Azure sécurisé et un cluster Hadoop HDInsight](https://azure.microsoft.com/resources/templates/101-hdinsight-secure-vnet/)

> [!IMPORTANT]
> Modifier les adresses IP hello utilisés dans cette hello de toomatch exemple région Azure que vous utilisez. Vous pouvez trouver ces informations dans hello [HDInsight avec des groupes de sécurité réseau et les itinéraires définis par l’utilisateur](#hdinsight-ip) section.

### <a name="azure-powershell"></a>Azure PowerShell

Utilisez hello suivant toocreate de script PowerShell un réseau virtuel qui restreint le trafic entrant et autorise le trafic de hello des adresses IP pour la région Europe du Nord hello.

> [!IMPORTANT]
> Modifier les adresses IP hello utilisés dans cette hello de toomatch exemple région Azure que vous utilisez. Vous pouvez trouver ces informations dans hello [HDInsight avec des groupes de sécurité réseau et les itinéraires définis par l’utilisateur](#hdinsight-ip) section.

```powershell
$vnetName = "Replace with your virtual network name"
$resourceGroupName = "Replace with hello resource group hello virtual network is in"
$subnetName = "Replace with hello name of hello subnet that you plan toouse for HDInsight"
# Get hello Virtual Network object
$vnet = Get-AzureRmVirtualNetwork `
    -Name $vnetName `
    -ResourceGroupName $resourceGroupName
# Get hello region hello Virtual network is in.
$location = $vnet.Location
# Get hello subnet object
$subnet = $vnet.Subnets | Where-Object Name -eq $subnetName
# Create a Network Security Group.
# And add exemptions for hello HDInsight health and management services.
$nsg = New-AzureRmNetworkSecurityGroup `
    -Name "hdisecure" `
    -ResourceGroupName $resourceGroupName `
    -Location $location `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -name "hdirule1" `
        -Description "HDI health and management address 52.164.210.96" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "52.164.210.96" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 300 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 13.74.153.132" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "13.74.153.132" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 301 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 168.61.49.99" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "168.61.49.99" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 302 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 23.99.5.239" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "23.99.5.239" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 303 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 168.61.48.131" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "168.61.48.131" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 304 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 138.91.141.162" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "138.91.141.162" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 305 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "blockeverything" `
        -Description "Block everything else" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "*" `
        -SourceAddressPrefix "Internet" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Deny `
        -Priority 500 `
        -Direction Inbound
# Set hello changes toohello security group
Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
# Apply hello NSG toohello subnet
Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name $subnetName `
    -AddressPrefix $subnet.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

> [!IMPORTANT]
> Cet exemple montre comment le trafic sur des adresses IP hello requis entrant tooadd règles tooallow. Il ne contient pas une règle toorestrict accès entrant depuis d’autres sources.
>
> Hello, l’exemple suivant montre comment accéder à tooenable SSH à partir de hello Internet :
>
> ```powershell
> Add-AzureRmNetworkSecurityRuleConfig -Name "SSH" -Description "SSH" -Protocol "*" -SourcePortRange "*" -DestinationPortRange "22" -SourceAddressPrefix "*" -DestinationAddressPrefix "VirtualNetwork" -Access Allow -Priority 306 -Direction Inbound
> ```

### <a name="azure-cli"></a>Interface de ligne de commande Azure

Utilisez hello suivant les étapes toocreate un réseau virtuel qui restreint le trafic entrant, mais autorise le trafic à partir d’adresses IP de hello requis par HDInsight.

1. Hello utilisation suivant toocreate de commande nommé d’un nouveau groupe de sécurité réseau `hdisecure`. Remplacez **RESOURCEGROUPNAME** avec le groupe de ressources hello contient hello réseau virtuel Azure. Remplacez **emplacement** avec l’emplacement hello (région), ce groupe hello a été créé dans.

    ```azurecli
    az network nsg create -g RESOURCEGROUPNAME -n hdisecure -l LOCATION
    ```

    Une fois le groupe de hello a été créé, vous recevez des informations sur le nouveau groupe de hello.

2. Utilisez hello suivant tooadd règles toohello nouveau groupe de sécurité réseau qui autorisent les communications entrantes sur le port 443 à partir de hello service de contrôle d’intégrité et de gestion Azure HDInsight. Remplacez **RESOURCEGROUPNAME** avec nom hello hello du groupe de ressources contenant hello réseau virtuel Azure.

    > [!IMPORTANT]
    > Modifier les adresses IP hello utilisés dans cette hello de toomatch exemple région Azure que vous utilisez. Vous pouvez trouver ces informations dans hello [HDInsight avec des groupes de sécurité réseau et les itinéraires définis par l’utilisateur](#hdinsight-ip) section.

    ```azurecli
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule1 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "52.164.210.96" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 300 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "13.74.153.132" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 301 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.49.99" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 302 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "23.99.5.239" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 303 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.48.131" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 304 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "138.91.141.162" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 305 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n block --protocol "*" --source-port-range "*" --destination-port-range "*" --source-address-prefix "Internet" --destination-address-prefix "VirtualNetwork" --access "Deny" --priority 500 --direction "Inbound"
    ```

3. tooretrieve hello identificateur unique pour ce groupe de sécurité réseau, utilisez hello de commande suivante :

    ```azurecli
    az network nsg show -g RESOURCEGROUPNAME -n hdisecure --query 'id'
    ```

    Cette commande retourne un toohello similaire valeur suit texte :

        "/subscriptions/SUBSCRIPTIONID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"

    Utilisez des guillemets doubles autour d’id dans la commande hello si vous n’obtenez pas les résultats de hello attendu.

4. Utilisez hello suivant commande tooapply hello sécurité groupe tooa sous-réseau. Remplacez hello __GUID__ et __RESOURCEGROUPNAME__ valeurs avec hello ceux qui sont retournées à partir de l’étape précédente de hello. Remplacez __VNETNAME__ et __SUBNETNAME__ avec le nom de réseau virtuel hello et le nom du sous-réseau que vous souhaitez toocreate.

    ```azurecli
    az network vnet subnet update -g RESOURCEGROUPNAME --vnet-name VNETNAME --name SUBNETNAME --set networkSecurityGroup.id="/subscriptions/GUID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"
    ```

    Une fois cette commande terminée, vous pouvez installer HDInsight dans hello réseau virtuel.

> [!IMPORTANT]
> Ces étapes uniquement ouvrir accès toohello HDInsight d’intégrité et de gestion de service sur hello cloud Azure. N’importe quel autre accès toohello cluster HDInsight à partir de l’extérieur hello réseau virtuel est bloquée. tooenable accès à partir du réseau virtuel externe hello, vous devez ajouter des règles de groupe de sécurité réseau supplémentaires.
>
> Hello, l’exemple suivant montre comment accéder à tooenable SSH à partir de hello Internet :
>
> ```azurecli
> az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule5 --protocol "*" --source-port-range "*" --destination-port-range "22" --source-address-prefix "*" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 306 --direction "Inbound"
> ```

## <a id="example-dns"></a> Exemple : configuration de DNS

### <a name="name-resolution-between-a-virtual-network-and-a-connected-on-premises-network"></a>Résolution de noms entre un réseau virtuel et un réseau local connecté

Cet exemple montre comment hello suivant hypothèses :

* Vous avez un réseau virtuel Azure qui est le réseau local de tooan connecté à l’aide d’une passerelle VPN.

* un serveur DNS personnalisé Hello dans le réseau virtuel de hello est en cours d’exécution Unix ou Linux comme système d’exploitation de hello.

* [Lier](https://www.isc.org/downloads/bind/) est installé sur un serveur DNS personnalisé hello.

Sur hello un serveur DNS personnalisé dans le réseau virtuel de hello :

1. Utiliser Azure PowerShell ou CLI d’Azure toofind hello suffixe DNS du réseau virtuel de hello :

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. Sur hello un serveur DNS personnalisé pour le réseau virtuel de hello, utilisez hello après le texte en tant que contenu hello Hello `/etc/bind/named.conf.local` fichier :

    ```
    // Forward requests for hello virtual network suffix tooAzure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {168.63.129.16;}; # Azure recursive resolver
    };
    ```

    Remplacez hello `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` valeur dont le suffixe DNS hello votre réseau virtuel.

    Cette configuration achemine toutes les requêtes DNS pour le suffixe DNS de hello du programme de résolution de Azure récursive toohello hello réseau virtuel.

2. Sur hello un serveur DNS personnalisé pour le réseau virtuel de hello, utilisez hello après le texte en tant que contenu hello Hello `/etc/bind/named.conf.options` fichier :

    ```
    // Clients tooaccept requests from
    // TODO: Add hello IP range of hello joined network toothis list
    acl goodclients {
        10.0.0.0/16; # IP address range of hello virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            # All other requests are sent toohello following
            forwarders {
                192.168.0.1; # Replace with hello IP address of your on-premises DNS server
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform tooRFC1035
            listen-on { any; };
    };
    ```
    
    * Remplacez hello `10.0.0.0/16` la valeur de la plage d’adresses IP hello de votre réseau virtuel. Cette entrée permet que la résolution de noms demande des adresses à l’intérieur de cette plage.

    * Ajouter la plage d’adresses IP hello de toohello de réseau local hello `acl goodclients { ... }` section.  entrée autorise les demandes de résolution de noms à partir des ressources dans un réseau local de hello.
    
    * Remplacez la valeur de hello `192.168.0.1` avec l’adresse IP de hello du serveur DNS local. Cette entrée achemine toutes les autres demandes toohello locale DNS serveur DNS.

3. configuration de hello toouse, redémarrez la liaison. Par exemple, `sudo service bind9 restart`.

4. Ajouter un serveur DNS de redirecteur conditionnel toohello local. Configurer les demandes de toosend de redirecteur conditionnel hello le suffixe DNS à partir d’un serveur DNS personnalisé étape 1 toohello hello.

    > [!NOTE]
    > Consultez la documentation de hello pour votre logiciel DNS pour plus de détails sur la façon de tooadd un redirecteur conditionnel.

Après avoir effectué ces étapes, vous pouvez vous connecter tooresources dans un réseau à l’aide de noms de domaine complet (FQDN). Vous pouvez maintenant installer HDInsight dans le réseau virtuel de hello.

### <a name="name-resolution-between-two-connected-virtual-networks"></a>Résolution de noms entre deux réseaux virtuels connectés

Cet exemple montre comment hello suivant hypothèses :

* Vous avez deux réseaux virtuels Azure connectés à l’aide d’une passerelle VPN ou d’une homologation.

* un serveur DNS personnalisé Hello dans les deux réseaux exécute Linux ou Unix en tant que système d’exploitation de hello.

* [Lier](https://www.isc.org/downloads/bind/) est installé sur des serveurs DNS personnalisés hello.

1. Utiliser Azure PowerShell ou CLI d’Azure toofind hello suffixe DNS de deux réseaux virtuels :

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. Hello utilisation après le texte en tant que contenu hello Hello `/etc/bind/named.config.local` fichier sur un serveur DNS personnalisé hello. Effectuez cette modification sur un serveur DNS personnalisé hello dans les deux réseaux virtuels.

    ```
    // Forward requests for hello virtual network suffix tooAzure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # hello IP address of hello DNS server in hello other virtual network
    };
    ```

    Remplacez hello `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` valeur dont le suffixe DNS hello hello __autres__ réseau virtuel. Cette entrée achemine les requêtes pour le suffixe DNS hello hello réseau distant toohello DNS personnalisé de ce réseau.

3. Sur hello des serveurs DNS personnalisés dans les deux réseaux virtuels, utilisez hello après le texte en tant que contenu hello Hello `/etc/bind/named.conf.options` fichier :

    ```
    // Clients tooaccept requests from
    acl goodclients {
        10.1.0.0/16; # hello IP address range of one virtual network
        10.0.0.0/16; # hello IP address range of hello other virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            forwarders {
            168.63.129.16;   # Azure recursive resolver         
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform tooRFC1035
            listen-on { any; };
    };
    ```
    
    * Remplacez hello `10.0.0.0/16` et `10.1.0.0/16` valeurs hello IP adresse des plages de vos réseaux virtuels. Cette entrée permet aux ressources de chaque réseau de demandes toomake des serveurs DNS de hello.

    Toutes les demandes qui ne sont pas pour les suffixes DNS de hello des réseaux virtuels de hello (par exemple, microsoft.com) est géré par le programme de résolution récursive Azure hello.

4. configuration de hello toouse, redémarrez la liaison. Par exemple, `sudo service bind9 restart` sur les deux serveurs DNS.

Après avoir effectué ces étapes, vous pouvez vous connecter tooresources dans le réseau virtuel de hello à l’aide de noms de domaine complet (FQDN). Vous pouvez maintenant installer HDInsight dans le réseau virtuel de hello.

## <a name="next-steps"></a>Étapes suivantes

* Pour obtenir un exemple de bout en bout de la configuration de réseau local de HDInsight tooconnect tooan, consultez [réseau de se connecter de HDInsight tooan local](./connect-on-premises-network.md).

* Pour plus d’informations sur les réseaux virtuels Azure, consultez hello [vue d’ensemble du réseau virtuel Azure](../virtual-network/virtual-networks-overview.md).

* Pour plus d’informations sur les groupes de sécurité réseau, consultez [Groupes de sécurité réseau](../virtual-network/virtual-networks-nsg.md).

* Pour plus d’informations sur les routages par l’utilisateur, consultez [Routage définis par l’utilisateur et transfert IP](../virtual-network/virtual-networks-udr-overview.md).