---
title: aaaMigrate tooAzure le Gestionnaire de ressources des outils pour HDInsight | Documents Microsoft
description: "Comment toomigrate tooAzure Gestionnaire de ressources du développement des outils pour les clusters HDInsight"
services: hdinsight
editor: cgronlun
manager: jhubbard
author: nitinme
documentationcenter: 
ms.assetid: 05efedb5-6456-4552-87ff-156d77fbe2e1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: c087ae63d2544e5badae6be9c258f783aa92e2ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-tooazure-resource-manager-based-development-tools-for-hdinsight-clusters"></a>Outils de développement basé sur le Gestionnaire de ressources tooAzure migration pour les clusters HDInsight

HDInsight déconseille les outils Azure Service Manager (ASM) pour HDInsight. Si vous utilisez Azure PowerShell ou CLI d’Azure hello HDInsight .NET SDK toowork avec des clusters HDInsight, vous êtes invités toouse hello Azure Resource Manager ARM versions de PowerShell, CLI et Kit de développement .NET à l’avenir. Cet article fournit des pointeurs sur la façon de toomigrate toohello nouveau ARM approche. Autant que possible, cet article souligne également les différences de hello entre les approches ASM et ARM hello pour HDInsight.

> [!IMPORTANT]
> prise en charge de Hello pour ASM en fonction de PowerShell, CLI, et Kit de développement .NET va interrompre son **le 1er janvier 2017**.
> 
> 

## <a name="migrating-azure-cli-tooazure-resource-manager"></a>Migration tooAzure CLI d’Azure Resource Manager
Hello CLI d’Azure maintenant par défaut le mode tooAzure Resource Manager (ARM), sauf si vous mettez à niveau à partir d’une installation précédente ; Dans ce cas, vous devrez peut-être toouse hello `azure config mode arm` tooARM en mode tooswitch de commande.

commandes de base Hello que hello CLI d’Azure fourni toowork avec HDInsight à l’aide d’Azure Service Management (ASM) hello sont identiques lors de l’utilisation de ARM ; Toutefois certains paramètres et les commutateurs peuvent avoir des nouveaux noms, et plusieurs nouveaux paramètres sont disponibles lors de l’utilisation de ARM. Par exemple, vous pouvez maintenant utiliser `azure hdinsight cluster create` toospecify hello réseau virtuel Azure et qui doit être créé dans un cluster, ou la ruche et les informations du magasin de métadonnées Oozie.

Les commandes de base pour travailler avec HDInsight via le Azure Resource Manager sont :

* `azure hdinsight cluster create` - crée un nouveau cluster HDInsight
* `azure hdinsight cluster delete` - supprime un cluster HDInsight existant
* `azure hdinsight cluster show` -affiche des informations sur un cluster existant
* `azure hdinsight cluster list` - répertorie les clusters HDInsight pour votre abonnement Azure

Hello d’utilisation `-h` passer des paramètres de hello tooinspect et les options disponibles pour chaque commande.

### <a name="new-commands"></a>Nouvelles commandes
Les nouvelles commandes disponibles avec Azure Resource Manager sont :

* `azure hdinsight cluster resize`-dynamiquement les modifications hello nombre de nœuds de cluster de hello travail
* `azure hdinsight cluster enable-http-access`-permet de cluster de toohello accès HTTPs (sur par défaut)
* `azure hdinsight cluster disable-http-access`-désactive le cluster de toohello accès HTTPs
* `azure hdinsight script-action` - fournit des commandes pour créer/gérer des actions de script sur un cluster
* `azure hdinsight config`-Fournit des commandes pour la création d’un fichier de configuration qui peut être utilisé avec hello `hdinsight cluster create` tooprovide les informations de configuration de la commande.

### <a name="deprecated-commands"></a>Commandes déconseillées
Si vous utilisez hello `azure hdinsight job` commandes toosubmit travaux tooyour HDInsight cluster ceux-ci ne sont pas disponibles via les commandes de hello ARM. Si vous devez tooprogrammatically submit travaux tooHDInsight à partir de scripts, vous devez utiliser à la place hello API REST fournie par HDInsight. Pour plus d’informations sur la soumission de travaux à l’aide des API REST, consultez hello suivant des documents.

* [Exécution à distance des tâches MapReduce avec Hadoop sur HDInsight à l’aide de Curl](hdinsight-hadoop-use-mapreduce-curl.md)
* [Exécution de requêtes Hive avec Hadoop dans HDInsight via Curl](hdinsight-hadoop-use-hive-curl.md)
* [Exécution à distance des tâches Pig avec Hadoop sur HDInsight à l’aide de Curl](hdinsight-hadoop-use-pig-curl.md)

Pour plus d’informations sur les autres façons de toorun MapReduce, Hive, porc de manière interactive, consultez [MapReduce utilisation avec Hadoop dans HDInsight](hdinsight-use-mapreduce.md), [utilisez Hive avec Hadoop dans HDInsight](hdinsight-use-hive.md), et [utilisez Pig avec Hadoop sur HDInsight](hdinsight-use-pig.md).

### <a name="examples"></a>Exemples
**Création d’un cluster**

* Ancienne commande (ASM) - `azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`
* Nouvelle commande (ARM) - `azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`

**Suppression d’un cluster**

* Ancienne commande (ASM) - `azure hdinsight cluster delete myhdicluster`
* Nouvelle commande (ARM) - `azure hdinsight cluster delete mycluster -g myresourcegroup`

**Énumérer les clusters**

* Ancienne commande (ASM) - `azure hdinsight cluster list`
* Nouvelle commande (ARM) - `azure hdinsight cluster list`

> [!NOTE]
> Pour la commande liste hello spécifiant hello le groupe de ressources à l’aide `-g` retourne uniquement les clusters hello dans le groupe de ressources spécifié hello.
> 
> 

**Afficher les informations du cluster**

* Ancienne commande (ASM) - `azure hdinsight cluster show myhdicluster`
* Nouvelle commande (ARM) - `azure hdinsight cluster show myhdicluster -g myresourcegroup`

## <a name="migrating-azure-powershell-tooazure-resource-manager"></a>Migration Azure PowerShell tooAzure Gestionnaire de ressources
Hello des informations générales sur Azure PowerShell en mode Azure Resource Manager (ARM) de hello trouverez [à l’aide de Azure PowerShell avec Azure Resource Manager](../powershell-azure-resource-manager.md).

Hello applets de commande Azure PowerShell ARM peut être installé côte à côte avec hello ASM applets de commande. applets de commande Hello à partir des deux modes de hello peuvent être distingués par leurs noms.  le mode Hello ARM a *AzureRmHDInsight* dans les noms d’applet de commande hello comparaison trop*AzureHDInsight* en mode ASM hello.  Par exemple, *New-AzureRmHDInsightCluster* et *New-AzureHDInsightCluster*. Toutefois, certains paramètres et commutateurs peuvent avoir des nouveaux noms, et de nombreux nouveaux paramètres sont disponibles lorsque vous utilisez ARM.  Par exemple, plusieurs applets de commande exigent un nouveau commutateur appelé *-ResourceGroupName*. 

Avant de pouvoir utiliser les applets de commande HDInsight hello, vous devez vous connecter tooyour compte Azure et créer un nouveau groupe de ressources :

* Login-AzureRmAccount ou [Select-AzureRmProfile](https://msdn.microsoft.com/library/mt619310.aspx). Consultez [Authentification d’un principal du service à l’aide d’Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [New-AzureRmResourceGroup](https://msdn.microsoft.com/library/mt603739.aspx)

### <a name="renamed-cmdlets"></a>Applets de commande renommées
hello toolist HDInsight ASM des applets de commande dans la console Windows PowerShell :

    help *azurermhdinsight*

Hello tableau suivant répertorie hello ASM applets de commande et leurs noms dans le mode hello ARM :

| Applets de commande ASM | Applets de commande ARM |
| --- | --- |
| Add-AzureHDInsightConfigValues |[Add-AzureRmHDInsightConfigValues](https://msdn.microsoft.com/library/mt603530.aspx) |
| Add-AzureHDInsightMetastore |[Add-AzureRmHDInsightMetastore](https://msdn.microsoft.com/library/mt603670.aspx) |
| Add-AzureHDInsightScriptAction |[Add-AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) |
| Add-AzureHDInsightStorage |[Add-AzureRmHDInsightStorage](https://msdn.microsoft.com/library/mt619445.aspx) |
| Get-AzureHDInsightCluster |[Get-AzureRmHDInsightCluster](https://msdn.microsoft.com/library/mt619371.aspx) |
| Get-AzureHDInsightJob |[Get-AzureRmHDInsightJob](https://msdn.microsoft.com/library/mt603590.aspx) |
| Get-AzureHDInsightJobOutput |[Get-AzureRmHDInsightJobOutput](https://msdn.microsoft.com/library/mt603793.aspx) |
| Get-AzureHDInsightProperties |[Get-AzureRmHDInsightProperties](https://msdn.microsoft.com/library/mt603546.aspx) |
| Grant-AzureHDInsightHttpServicesAccess |[Grant-AzureRmHDInsightHttpServicesAccess](https://msdn.microsoft.com/library/mt619407.aspx) |
| Grant-AzureHdinsightRdpAccess |[Grant-AzureRmHDInsightRdpServicesAccess](https://msdn.microsoft.com/library/mt603717.aspx) |
| Invoke-AzureHDInsightHiveJob |[Invoke-AzureRmHDInsightHiveJob](https://msdn.microsoft.com/library/mt603593.aspx) |
| New-AzureHDInsightCluster |[New-AzureRmHDInsightCluster](https://msdn.microsoft.com/library/mt619331.aspx) |
| New-AzureHDInsightClusterConfig |[New-AzureRmHDInsightClusterConfig](https://msdn.microsoft.com/library/mt603700.aspx) |
| New-AzureHDInsightHiveJobDefinition |[New-AzureRmHDInsightHiveJobDefinition](https://msdn.microsoft.com/library/mt619448.aspx) |
| New-AzureHDInsightMapReduceJobDefinition |[New-AzureRmHDInsightMapReduceJobDefinition](https://msdn.microsoft.com/library/mt603626.aspx) |
| New-AzureHDInsightPigJobDefinition |[New-AzureRmHDInsightPigJobDefinition](https://msdn.microsoft.com/library/mt603671.aspx) |
| New-AzureHDInsightSqoopJobDefinition |[New-AzureRmHDInsightSqoopJobDefinition](https://msdn.microsoft.com/library/mt608551.aspx) |
| New-AzureHDInsightStreamingMapReduceJobDefinition |[New-AzureRmHDInsightStreamingMapReduceJobDefinition](https://msdn.microsoft.com/library/mt603626.aspx) |
| Remove-AzureHDInsightCluster |[Remove-AzureRmHDInsightCluster](https://msdn.microsoft.com/library/mt619431.aspx) |
| Revoke-AzureHDInsightHttpServicesAccess |[Revoke-AzureRmHDInsightHttpServicesAccess](https://msdn.microsoft.com/library/mt619375.aspx) |
| Revoke-AzureHdinsightRdpAccess |[Revoke-AzureRmHDInsightRdpServicesAccess](https://msdn.microsoft.com/library/mt603523.aspx) |
| Set-AzureHDInsightClusterSize |[Set-AzureRmHDInsightClusterSize](https://msdn.microsoft.com/library/mt603513.aspx) |
| Set-AzureHDInsightDefaultStorage |[Set-AzureRmHDInsightDefaultStorage](https://msdn.microsoft.com/library/mt603486.aspx) |
| Start-AzureHDInsightJob |[Start-AzureRmHDInsightJob](https://msdn.microsoft.com/library/mt603798.aspx) |
| Stop-AzureHDInsightJob |[Stop-AzureRmHDInsightJob](https://msdn.microsoft.com/library/mt619424.aspx) |
| Use-AzureHDInsightCluster |[Use-AzureRmHDInsightCluster](https://msdn.microsoft.com/library/mt619442.aspx) |
| Wait-AzureHDInsightJob |[Wait-AzureRmHDInsightJob](https://msdn.microsoft.com/library/mt603834.aspx) |

### <a name="new-cmdlets"></a>Nouvelles applets de commande
Hello Voici hello nouvelles applets de commande qui sont disponibles uniquement dans le mode hello ARM. 

**Applets de commandes associées à une action de script :**

* **Get-AzureRmHDInsightPersistedScriptAction**: Obtient hello persistante des actions de script pour un cluster et les répertorie dans l’ordre chronologique ou obtient les détails d’une action de script persistantes spécifié. 
* **Get-AzureRmHDInsightScriptActionHistory**: Obtient l’historique des actions de script hello pour un cluster et répertorie dans l’ordre chronologique inverse ou obtient les détails d’une action de script exécutée précédemment. 
* **Remove-AzureRmHDInsightPersistedScriptAction**: retire une action de script persistante d’un cluster HDInsight.
* **Set-AzureRmHDInsightPersistedScriptAction**: définit un toobe d’action de script précédemment exécuté une action de script persistantes.
* **AzureRmHDInsightScriptAction envoyer**: soumet un cluster Azure HDInsight tooan de nouveau script action. 

Pour plus d’informations sur l’utilisation, consultez la page [Personnaliser des clusters HDInsight à l’aide d’une action de script](hdinsight-hadoop-customize-cluster-linux.md).

**Applets de commande associées à l’identité du cluster :**

* **AzureRmHDInsightClusterIdentity ajouter**: ajoute un objet de configuration de cluster identité tooa cluster afin que hello cluster HDInsight peut accéder aux magasins de LAC de données Azure. Consultez la page [Créer un cluster HDInsight avec Data Lake Store à l’aide d’Azure PowerShell](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md).

### <a name="examples"></a>Exemples
**Créer un cluster**

Ancienne commande (ASM) : 

    New-AzureHDInsightCluster `
        -Name $clusterName `
        -Location $location `
        -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $storageAccountKey `
        -DefaultStorageContainerName $containerName `
        -ClusterSizeInNodes 2 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.2" `
        -Credential $httpCredential `
        -SshCredential $sshCredential

Nouvelle commande (ARM) :

    New-AzureRmHDInsightCluster `
        -ClusterName $clusterName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $storageAccountKey `
        -DefaultStorageContainer $containerName  `
        -ClusterSizeInNodes 2 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.2" `
        -HttpCredential $httpcredentials `
        -SshCredential $sshCredentials


**Supprimer un cluster**

Ancienne commande (ASM) :

    Remove-AzureHDInsightCluster -name $clusterName 

Nouvelle commande (ARM) :

    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName 

**Répertorier un cluster**

Ancienne commande (ASM) :

    Get-AzureHDInsightCluster

Nouvelle commande (ARM) :

    Get-AzureRmHDInsightCluster 

**Afficher le cluster**

Ancienne commande (ASM) :

    Get-AzureHDInsightCluster -Name $clusterName

Nouvelle commande (ARM) :

    Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -clusterName $clusterName


#### <a name="other-samples"></a>Autres exemples
* [Création de clusters HDInsight](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
* [Envoi de tâches Hive](hdinsight-hadoop-use-hive-powershell.md)
* [Envoi de tâches Pig](hdinsight-hadoop-use-pig-powershell.md)
* [Envoi de tâches Sqoop](hdinsight-hadoop-use-sqoop-powershell.md)

## <a name="migrating-toohello-arm-based-hdinsight-net-sdk"></a>Migration toohello basés sur ARM HDInsight .NET SDK
Hello basée sur la gestion des services Azure [(ASM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt416619.aspx) est désormais déconseillée. Vous êtes invité toouse hello basée sur la gestion des ressources Azure [(ARM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt271028.aspx). Hello packages HDInsight de base ASM suivants sont déconseillés.

* `Microsoft.WindowsAzure.Management.HDInsight`
* `Microsoft.Hadoop.Client`

Cette section fournit des pointeurs toomore plus d’informations sur la façon de tooperform certaine tâches à l’aide de hello basés sur ARM Kit de développement logiciel.

| Comment... à l’aide de hello basés sur ARM des SDK HDInsight | Liens |
| --- | --- |
| Créer des clusters basés sur Linux dans HDInsight à l’aide du Kit de développement logiciel (SDK) .NET |Consultez [Créer des clusters basés sur Linux dans HDInsight à l’aide du Kit de développement logiciel (SDK) .NET](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md) |
| Personnaliser un cluster à l’aide d’une action de script avec le Kit de développement logiciel (SDK) .NET |Consultez [Personnaliser des clusters HDInsight sous Linux à l’aide d’une action de script](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action) |
| Authentifier des applications de manière interactive à l’aide d’Azure Active Directory avec le Kit de développement logiciel (SDK) .NET |Consultez [Exécution de requêtes Hive avec le Kit de développement logiciel (SDK) .NET](hdinsight-hadoop-use-hive-dotnet-sdk.md). extrait de code Hello dans cet article utilise l’approche de l’authentification interactive hello. |
| Authentifier des applications de manière non interactive à l’aide d’Azure Active Directory avec le Kit de développement logiciel (SDK) .NET |Consultez [Créer des applications HDInsight d’authentification non interactives](hdinsight-create-non-interactive-authentication-dotnet-applications.md) |
| Envoyer une tâche Hive à l’aide du Kit de développement logiciel (SDK) .NET |Consulter [Envoi de tâches Hive](hdinsight-hadoop-use-hive-dotnet-sdk.md) |
| Envoyer une tâche Pig à l’aide du Kit de développement logiciel (SDK) .NET |Consulter [Envoi de tâches Pig](hdinsight-hadoop-use-pig-dotnet-sdk.md) |
| Envoyer une tâche Sqoop à l’aide du Kit de développement logiciel (SDK) .NET |Consulter [Envoi de tâches Sqoop](hdinsight-hadoop-use-sqoop-dotnet-sdk.md) |
| Répertorier les clusters HDInsight à l’aide du Kit de développement logiciel (SDK) .NET |Consulter [Répertorier les clusters HDInsight](hdinsight-administer-use-dotnet-sdk.md#list-clusters) |
| Mettre à l’échelle les clusters HDInsight à l’aide du Kit de développement logiciel (SDK) .NET |Consulter [Mettre à l’échelle les clusters HDInsight](hdinsight-administer-use-dotnet-sdk.md#scale-clusters) |
| Autorisations GRANT/revoke accès tooHDInsight clusters à l’aide du Kit de développement .NET |Consultez [clusters de tooHDInsight accès Grant/revoke.](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access) |
| Mettre à jour les informations d’identification de l’utilisateur HTTP pour les clusters HDInsight à l’aide du Kit de développement logiciel (SDK) .NET |Consulter [Mettre à jour les informations d’identification de l’utilisateur HTTP pour les clusters HDInsight](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials) |
| Rechercher le compte de stockage par défaut hello pour les clusters HDInsight à l’aide du Kit de développement .NET |Consultez [trouver le compte de stockage par défaut hello pour les clusters HDInsight](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account) |
| Supprimer des clusters HDInsight à l’aide du Kit de développement logiciel (SDK) .NET |Consulter [Supprimer des clusters HDInsight](hdinsight-administer-use-dotnet-sdk.md#delete-clusters) |

### <a name="examples"></a>Exemples
Voici quelques exemples sur la façon dont une opération est effectuée à l’aide de hello basée sur ASM Kit de développement logiciel et extrait de code équivalent hello pour hello basés sur ARM Kit de développement logiciel.

**Création d’un client CRUD de cluster**

* Ancienne commande (ASM)
  
        //Certificate auth
        //This logs hello application in using a subscription administration certificate, which is not offered in Azure Resource Manager (ARM)
  
        const string subid = "454467d4-60ca-4dfd-a556-216eeeeeeee1";
        var cred = new HDInsightCertificateCredential(new Guid(subid), new X509Certificate2(@"path\to\certificate.cer"));
        var client = HDInsightClient.Connect(cred);
* Nouvelle commande (ARM) (autorisation du principal de service)
  
        //Service principal auth
        //This will log hello application in as itself, rather than on behalf of a specific user.
        //For details, including how tooset up hello application, see:
        //   https://azure.microsoft.com/en-us/documentation/articles/hdinsight-create-non-interactive-authentication-dotnet-applications/
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.ServicePrincipal, Id = clientId };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, tenantId, secretKey, ShowDialog.Never).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);
* Nouvelle commande (ARM) (autorisation de l’utilisateur)
  
        //User auth
        //This will log hello application in on behalf of hello user.
        //hello end-user will see a login popup.
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.User, Id = username };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, AuthenticationFactory.CommonAdTenant, password, ShowDialog.Auto).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);

**Création d’un cluster**

* Ancienne commande (ASM)
  
        var clusterInfo = new ClusterCreateParameters
                    {
                        Name = dnsName,
                        DefaultStorageAccountKey = key,
                        DefaultStorageContainer = defaultStorageContainer,
                        DefaultStorageAccountName = storageAccountDnsName,
                        ClusterSizeInNodes = 1,
                        ClusterType = type,
                        Location = "West US",
                        UserName = "admin",
                        Password = "*******",
                        Version = version,
                        HeadNodeSize = NodeVMSize.Large,
                    };
        clusterInfo.CoreConfiguration.Add(new KeyValuePair<string, string>("config1", "value1"));
        client.CreateCluster(clusterInfo);
* Nouvelle commande (ARM)
  
        var clusterCreateParameters = new ClusterCreateParameters
            {
                Location = "West US",
                ClusterType = "Hadoop",
                Version = "3.1",
                OSType = OSType.Linux,
                DefaultStorageAccountName = "mystorage.blob.core.windows.net",
                DefaultStorageAccountKey =
                    "O9EQvp3A3AjXq/W27rst1GQfLllhp0gUeiUUn2D8zX2lU3taiXSSfqkZlcPv+nQcYUxYw==",
                UserName = "hadoopuser",
                Password = "*******",
                HeadNodeSize = "ExtraLarge",
                RdpUsername = "hdirp",
                RdpPassword = ""*******",
                RdpAccessExpiry = new DateTime(2025, 3, 1),
                ClusterSizeInNodes = 5
            };
        var coreConfigs = new Dictionary<string, string> {{"config1", "value1"}};
        clusterCreateParameters.Configurations.Add(ConfigurationKey.CoreSite, coreConfigs);

**Activation de l’accès HTTP**

* Ancienne commande (ASM)
  
        client.EnableHttp(dnsName, "West US", "admin", "*******");
* Nouvelle commande (ARM)
  
        var httpParams = new HttpSettingsParameters
        {
               HttpUserEnabled = true,
               HttpUsername = "admin",
               HttpPassword = "*******",
        };
        client.Clusters.ConfigureHttpSettings(resourceGroup, dnsname, httpParams);

**Suppression d’un cluster**

* Ancienne commande (ASM)
  
        client.DeleteCluster(dnsName);
* Nouvelle commande (ARM)
  
        client.Clusters.Delete(resourceGroup, dnsname);

