---
title: "aaaCreate HBase des clusters dans un réseau virtuel - Azure | Documents Microsoft"
description: "Prise en main de HBase dans Azure HDInsight Découvrez comment les clusters toocreate HDInsight HBase sur un réseau virtuel Azure."
keywords: 
services: hdinsight,virtual-network
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 8de8e446-f818-4e61-8fad-e9d38421e80d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 097338a5a650bb607a9f6f9ddb59bb88d098b56f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hbase-clusters-on-hdinsight-in-azure-virtual-network"></a>Création de clusters HBase sur HDInsight dans un réseau virtuel Microsoft Azure
Découvrez comment toocreate HDInsight HBase de Azure de clusters dans un [réseau virtuel Azure][1].

Avec l’intégration de réseau virtuel, clusters HBase peuvent être déployé toohello même virtuel réseau en tant que vos applications, ainsi que les applications peuvent communiquer directement avec HBase. Hello les avantages suivants :

* Une connexion directe hello web toohello de nœuds d’application de cluster HBase hello, qui permet la communication via RPC HBase Java appeler les API de (RPC).
* Amélioration des performances en évitant à votre trafic de transiter par plusieurs passerelles et équilibrages de charge.
* Hello capacité tooprocess des informations sensibles de manière plus sécurisée sans exposer un point de terminaison public.

### <a name="prerequisites"></a>Composants requis
Avant de commencer ce didacticiel, vous devez disposer des éléments suivants de hello :

* **Un abonnement Azure**. Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Un poste de travail sur lequel est installé Azure PowerShell**. Consultez la page [Installation et utilisation d’Azure PowerShell](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/).

## <a name="create-hbase-cluster-into-virtual-network"></a>Création de clusters HBase sur un réseau virtuel
Dans cette section, vous créez un cluster HBase de basés sur Linux avec un compte de stockage Azure dépendant hello dans un réseau virtuel Azure à l’aide un [modèle Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md). Pour d’autres méthodes de création de cluster et les paramètres de hello, consultez [HDInsight de créer des clusters](hdinsight-hadoop-provision-linux-clusters.md). Pour plus d’informations sur l’utilisation d’un modèle de toocreate Hadoop dans HDInsight les clusters, consultez [Hadoop de créer des clusters dans HDInsight à l’aide de modèles Azure Resource Manager](hdinsight-hadoop-create-windows-clusters-arm-templates.md)

> [!NOTE]
> Certaines propriétés sont codés en dur dans le modèle de hello. Par exemple :
>
> * **Emplacement** : Est des États-Unis 2
> * **Version de cluster** : 3.5
> * **Nombre de nœuds de travail du cluster** : 2
> * **Compte de stockage par défaut** : une chaîne unique
> * **Nom du réseau virtuel** : &lt;Nom du cluster&gt;-réseau virtuel
> * **Espace d’adressage du réseau virtuel** : 10.0.0.0/16
> * **Nom du sous-réseau** : subnet1
> * **Plage d’adresses de sous-réseau** : 10.0.0.0/24
>
> &lt;Nom du cluster > est remplacé par le nom de cluster de hello que vous fournissez lors de l’utilisation du modèle de hello.
>
>

1. Cliquez sur hello suit image tooopen hello template Bonjour portail Azure. Hello modèle se trouve dans [modèles de démarrage rapide Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/).

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-provision-vnet/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. À partir de hello **les déploiement personnalisé** panneau, entrez hello propriétés suivantes :

   * **Abonnement**: sélectionnez un cluster HDInsight d’abonnement Azure utilisé toocreate hello, compte de stockage dépendant de hello et hello réseau virtuel Azure.
   * **Groupe de ressources** : sélectionnez **Créer** et donnez un nouveau nom au groupe de ressources.
   * **Emplacement**: sélectionnez un emplacement pour le groupe de ressources hello.
   * **ClusterName**: entrez un nom pour hello Hadoop cluster toobe est créé.
   * **Nom de connexion et mot de passe de cluster**: nom de connexion par défaut hello est **admin**.
   * **Mot de passe et le nom d’utilisateur SSH**: nom d’utilisateur par défaut de hello est **sshuser**.  Vous pouvez le renommer.
   * **J’accepte les conditions hello susmentionnées générales toohello**: (Sélectionner)
3. Cliquez sur **Achat**. Cela prend environ environ 20 minutes toocreate un cluster. Une fois que le cluster de hello est créé, vous pouvez cliquer sur Panneau de cluster hello dans tooopen de portail hello il.

Après avoir terminé le didacticiel de hello, vous pourriez cluster hello de toodelete. Avec HDInsight, vos données sont stockées Azure Storage, pour que vous puissiez supprimer un cluster en toute sécurité s’il n’est pas en cours d’utilisation. Vous devez également payer pour un cluster HDInsight, même lorsque vous ne l’utilisez pas. Étant donné que les frais de hello pour le cluster de hello sont autant de fois plus de frais hello pour le stockage, il est judicieux économique toodelete clusters lorsqu’ils ne sont pas en cours d’utilisation. Pour obtenir des instructions de hello de la suppression d’un cluster, consultez [Hadoop de gérer les clusters dans HDInsight à l’aide de hello Azure portal](hdinsight-administer-use-management-portal.md#delete-clusters).

toobegin fonctionne avec votre nouveau cluster HBase, vous pouvez utiliser les procédures hello trouvés dans [commencer à utiliser HBase avec Hadoop dans HDInsight](hdinsight-hbase-tutorial-get-started.md).

## <a name="connect-toohello-hbase-cluster-using-hbase-java-rpc-apis"></a>Connecter le cluster de HBase toohello à l’aide des API de RPC HBase Java
1. Création d’une infrastructure en tant que service (IaaS) virtual machine dans hello même réseau virtuel Azure et hello même sous-réseau. Pour plus d’informations sur la création d’une machine virtuelle IaaS, consultez [Création d’une machine virtuelle exécutant Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md). Lorsque hello comme suit dans ce document, vous devez utiliser hello valeurs pour la configuration de réseau hello suivantes :

   * **Réseau virtuel** : &lt;Nom du cluster&gt;-réseau virtuel
   * **Sous-réseau** : subnet1

   > [!IMPORTANT]
   > Remplacez &lt;nom de Cluster > avec le nom de hello que vous avez utilisé lors de la création du cluster HDInsight de hello dans les étapes précédentes.
   >
   >

   À l’aide de ces valeurs, hello ordinateur virtuel est placé dans hello même réseau virtuel et sous-réseau que le cluster HDInsight de hello. Cette configuration autorise les toodirectly communiquent entre eux. Il existe un moyen toocreate un cluster HDInsight avec un nœud vide. nœud de périmètre Hello peut être cluster de hello toomanage utilisé.  Pour plus d’informations, consultez [Utiliser des nœuds de périmètre vides dans HDInsight](hdinsight-apps-use-edge-node.md).

2. Lorsque vous utilisez un tooHBase de tooconnect d’application Java à distance, vous devez utiliser le nom de domaine complet de hello (FQDN). toodetermine, vous devez obtenir le suffixe DNS spécifique à la connexion hello du cluster de HBase hello. toodo, vous pouvez utiliser une des méthodes suivantes de hello :

   * Utilisez un toomake de navigateur Web un appel de Ambari :

     Parcourir toohttps : / /&lt;nom_cluster >.azurehdinsight.net/api/v1/clusters/&lt;nom_cluster > / héberge ? minimal_response = true. Il trouve un fichier JSON avec des suffixes DNS hello.
   * Utilisez le site Web de Ambari hello :

     1. Parcourir trop https://&lt;nomcluster >. azurehdinsight.net.
     2. Cliquez sur **hôtes** à partir du menu du haut hello.
   * Utilisez les appels REST Curl toomake :

    ```bash
        curl -u <username>:<password> -k https://<clustername>.azurehdinsight.net/ambari/api/v1/clusters/<clustername>.azurehdinsight.net/services/hbase/components/hbrest
    ```

     Bonjour données JavaScript Objet Notation (JSON) est retourné, trouver l’entrée de « host_name » hello. Il contient hello nom de domaine complet pour les nœuds dans le cluster de hello hello. Par exemple :

         ...
         "host_name": "wordkernode0.<clustername>.b1.cloudapp.net
         ...

     partie Hello de début de nom de domaine hello avec le nom du cluster hello est le suffixe DNS de hello. Par exemple, mon_cluster.b1.cloudapp.net.
   * Utilisation d'Azure PowerShell

     Hello utilisation suivant hello de Azure PowerShell script tooregister **Get-ClusterDetail** (fonction), qui peut être suffixe DNS de hello tooreturn utilisé :

    ```powershell
        function Get-ClusterDetail(
            [String]
            [Parameter( Position=0, Mandatory=$true )]
            $ClusterDnsName,
            [String]
            [Parameter( Position=1, Mandatory=$true )]
            $Username,
            [String]
            [Parameter( Position=2, Mandatory=$true )]
            $Password,
            [String]
            [Parameter( Position=3, Mandatory=$true )]
            $PropertyName
            )
        {
        <#
            .SYNOPSIS
            Displays information toofacilitate an HDInsight cluster-to-cluster scenario within hello same virtual network.
            .Description
            This command shows hello following 4 properties of an HDInsight cluster:
            1. ZookeeperQuorum (supports only HBase type cluster)
                Shows hello value of HBase property "hbase.zookeeper.quorum".
            2. ZookeeperClientPort (supports only HBase type cluster)
                Shows hello value of HBase property "hbase.zookeeper.property.clientPort".
            3. HBaseRestServers (supports only HBase type cluster)
                Shows a list of host FQDNs that run hello HBase REST server.
            4. FQDNSuffix (supports all cluster types)
                Shows hello FQDN suffix of hosts in hello cluster.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperQuorum
            This command shows hello value of HBase property "hbase.zookeeper.quorum".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperClientPort
            This command shows hello value of HBase property "hbase.zookeeper.property.clientPort".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName HBaseRestServers
            This command shows a list of host FQDNs that run hello HBase REST server.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName FQDNSuffix
            This command shows hello FQDN suffix of hosts in hello cluster.
        #>

            $DnsSuffix = ".azurehdinsight.net"

            $ClusterFQDN = $ClusterDnsName + $DnsSuffix
            $webclient = new-object System.Net.WebClient
            $webclient.Credentials = new-object System.Net.NetworkCredential($Username, $Password)

            if($PropertyName -eq "ZookeeperQuorum")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.quorum"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                Write-host $JsonObject.items[0].properties.'hbase.zookeeper.quorum'
            }
            if($PropertyName -eq "ZookeeperClientPort")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.property.clientPort"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                Write-host $JsonObject.items[0].properties.'hbase.zookeeper.property.clientPort'
            }
            if($PropertyName -eq "HBaseRestServers")
            {
                $Url1 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.rest.port"
                $Response1 = $webclient.DownloadString($Url1)
                $JsonObject1 = $Response1 | ConvertFrom-Json
                $PortNumber = $JsonObject1.items[0].properties.'hbase.rest.port'

                $Url2 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/hbase/components/hbrest"
                $Response2 = $webclient.DownloadString($Url2)
                $JsonObject2 = $Response2 | ConvertFrom-Json
                foreach ($host_component in $JsonObject2.host_components)
                {
                    $ConnectionString = $host_component.HostRoles.host_name + ":" + $PortNumber
                    Write-host $ConnectionString
                }
            }
            if($PropertyName -eq "FQDNSuffix")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/YARN/components/RESOURCEMANAGER"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                $FQDN = $JsonObject.host_components[0].HostRoles.host_name
                $pos = $FQDN.IndexOf(".")
                $Suffix = $FQDN.Substring($pos + 1)
                Write-host $Suffix
            }
        }
    ```

     Après l’exécution du script PowerShell de Azure hello, utilisez hello commande suivante suffixe DNS de hello tooreturn à l’aide de hello **Get-ClusterDetail** (fonction). Spécifiez votre nom de cluster HDInsight HBase, ainsi que le nom et le mot de passe de l'administrateur lors de l'utilisation de cette commande.

    ```powershell
        Get-ClusterDetail -ClusterDnsName <yourclustername> -PropertyName FQDNSuffix -Username <clusteradmin> -Password <clusteradminpassword>
    ```

     Cette commande retourne le suffixe DNS de hello. Par exemple, **votre_nom_cluster.b4.internal.cloudapp.net**.


<!--
3.    Change hello primary DNS suffix configuration of hello virtual machine. This enables hello virtual machine tooautomatically resolve hello host name of hello HBase cluster without explicit specification of hello suffix. For example, hello *workernode0* host name will be correctly resolved tooworkernode0 of hello HBase cluster.

    toomake hello configuration change:

    1. RDP into hello virtual machine.
    2. Open **Local Group Policy Editor**. hello executable is gpedit.msc.
    3. Expand **Computer Configuration**, expand **Administrative Templates**, expand **Network**, and then click **DNS Client**.
    - Set **Primary DNS Suffix** toohello value obtained in step 2:

        ![hdinsight.hbase.primary.dns.suffix][img-primary-dns-suffix]
    4. Click **OK**.
    5. Reboot hello virtual machine.
-->

tooverify qui hello d’ordinateur virtuel peuvent communiquer avec hello cluster HBase, utilisez la commande de hello `ping headnode0.<dns suffix>` à partir de l’ordinateur virtuel de hello. Par exemple, ping headnode0.mon_cluster.b1.cloudapp.net.

toouse ces informations dans une application Java, vous pouvez suivre les étapes de hello dans [Maven d’utiliser toobuild Java applications qui utilisent HBase hdinsight (Hadoop)](hdinsight-hbase-build-java-maven.md) toocreate une application. application de hello toohave se connecter à distance HBase tooa, modifier hello **hbase-site.XML** fichier cette hello de toouse exemple nom de domaine complet pour soigneur. Par exemple :

    <property>
        <name>hbase.zookeeper.quorum</name>
        <value>zookeeper0.<dns suffix>,zookeeper1.<dns suffix>,zookeeper2.<dns suffix></value>
    </property>

> [!NOTE]
> Pour plus d’informations sur la résolution de noms dans les réseaux virtuels Azure, y compris la manière toouse votre propre serveur DNS, consultez [résolution de noms (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).
>
>

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous avez appris comment toocreate un cluster HBase. toolearn, voir :

* [Prise en main de HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Utiliser des nœuds de périphérie vides dans HDInsight](hdinsight-apps-use-edge-node.md)
* [Configuration de la géo-réplication HBase dans HDInsigtht](hdinsight-hbase-replication.md)
* [Créer des clusters Hadoop dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md)
* [Prise en main de HBase avec Hadoop dans HDInsight](hdinsight-hbase-tutorial-get-started.md)
* [Analyse de sentiments Twitter avec HBase dans HDInsight](hdinsight-hbase-analyze-twitter-sentiment.md)
* [Présentation du réseau virtuel][vnet-overview]

[1]: http://azure.microsoft.com/services/virtual-network/
[2]: http://technet.microsoft.com/library/ee176961.aspx
[3]: http://technet.microsoft.com/library/hh847889.aspx

[hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[vnet-overview]: ../virtual-network/virtual-networks-overview.md
[vm-create]: ../virtual-machines/virtual-machines-windows-hero-tutorial.md

[azure-portal]: https://portal.azure.com
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp

[hdinsight-powershell-reference]: https://msdn.microsoft.com/library/dn858087.aspx


[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter


[powershell-install]: /powershell/azureps-cmdlets-docs


[hdinsight-customize-cluster]: hdinsight-hadoop-customize-cluster.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]: ../hdinsight-hadoop-use-blob-storage.md#powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-ODBC-driver.md
[hdinsight-hbase-replication-dns]: hdinsight-hbase-geo-replication-configure-DNS.md

[img-dns-surffix]: ./media/hdinsight-hbase-provision-vnet/DNSSuffix.png
[img-primary-dns-suffix]: ./media/hdinsight-hbase-provision-vnet/PrimaryDNSSuffix.png
[img-provision-cluster-page1]: ./media/hdinsight-hbase-provision-vnet/hbasewizard1.png "Détails de configuration pour le nouveau cluster de HBase hello"
[img-provision-cluster-page5]: ./media/hdinsight-hbase-provision-vnet/hbasewizard5.png "Utilisez l’Action de Script toocustomize un cluster HBase"

[azure-preview-portal]: https://portal.azure.com
