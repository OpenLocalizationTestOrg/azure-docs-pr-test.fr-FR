---
title: "aaaTips pour l’utilisation de Hadoop dans HDInsight basés sur Linux - Azure | Documents Microsoft"
description: "Obtenir des conseils d’implémentation pour l’utilisation des clusters HDInsight basés sur Linux (Hadoop) sur un environnement familier de Linux en cours d’exécution dans hello cloud Azure."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c41c611c-5798-4c14-81cc-bed1e26b5609
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: a555622605079c9beae88ece872042e36d540c7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="information-about-using-hdinsight-on-linux"></a>Informations sur l’utilisation de HDInsight sous Linux

Les clusters HDInsight Azure fournissent Hadoop sur un environnement familier de Linux, en cours d’exécution dans hello cloud Azure. En principe, il fonctionne comme tout autre Hadoop sur une installation Linux. Ce document présente des différences spécifiques que vous devriez connaître.

> [!IMPORTANT]
> Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="prerequisites"></a>Composants requis

La plupart des étapes hello dans ce document utilisent hello suivant des utilitaires que vous devrez peut-être toobe installé sur votre système.

* [cURL](https://curl.haxx.se/) -utilisé toocommunicate avec les services web
* [jq](https://stedolan.github.io/jq/) -tooparse JSON documents utilisés
* [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) (version préliminaire) - utilisé tooremotely gérer les services Azure

## <a name="users"></a>Utilisateurs

Sauf s’il est [joint à un domaine](hdinsight-domain-joined-introduction.md), HDInsight doit être considéré comme un système **mono-utilisateur**. Un compte d’utilisateur SSH est créé avec le cluster hello, avec les autorisations de niveau administrateur. Comptes SSH supplémentaires peuvent être créés, mais ils possèdent également des clusters de toohello accès administrateur.

HDInsight joint à un domaine prend en charge la présence de plusieurs utilisateurs et des paramètres d’autorisation et de rôles plus précis. Pour plus d’informations, consultez la section [Gestion des clusters HDInsight joints à un domaine](hdinsight-domain-joined-manage.md).

## <a name="domain-names"></a>Noms de domaine

Hello complet toouse (FQDN) de nom de domaine lors de la connexion toohello cluster à partir de hello internet est  **&lt;nomcluster >. azurehdinsight.net** ou (SSH)  **&lt;clustername-ssh >. azurehdinsight.net**.

En interne, chaque nœud de cluster de hello a un nom qui est attribué lors de la configuration de cluster. noms de cluster toofind hello, consultez hello **hôtes** page hello Ambari Web UI. Vous pouvez également utiliser hello suivant tooreturn une liste des ordinateurs hôtes à partir de l’API REST de Ambari de hello :

    curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/hosts" | jq '.items[].Hosts.host_name'

Remplacez **mot de passe** avec mot de passe hello du compte d’administrateur hello, et **CLUSTERNAME** avec nom hello de votre cluster. Cette commande retourne un document JSON qui contient une liste d’hôtes hello dans un cluster de hello. Jq est utilisé tooextract hello `host_name` valeur de l’élément pour chaque hôte.

Si vous avez besoin de nom de hello toofind du nœud de hello pour un service spécifique, vous pouvez interroger Ambari pour ce composant. Par exemple, hôtes de hello toofind pour le nœud de nom hello HDFS, utilisez hello de commande suivante :

    curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/HDFS/components/NAMENODE" | jq '.host_components[].HostRoles.host_name'

Cette commande retourne un document JSON décrivant hello service, et puis jq extrait de hello uniquement `host_name` valeur pour les ordinateurs hôtes de hello.

## <a name="remote-access-tooservices"></a>Accès à distance tooservices

* **Ambari (Web)** : https://&lt;clustername&gt;.azurehdinsight.net

    S’authentifier en utilisant le mot de passe et d’utilisateur administrateur de cluster hello et se tooAmbari.

    L’authentification en texte clair - utilisez HTTPS toohelp Assurez-vous toujours que hello connexion est sécurisée.

    > [!IMPORTANT]
    > Partie du site web hello interfaces utilisateur disponibles via Ambari accéder aux nœuds à l’aide d’un nom de domaine interne. Domaine interne, les noms ne sont pas accessibles publiquement via hello internet. Vous pouvez recevoir des erreurs « serveur introuvable » lors de la tentative tooaccess certaines fonctionnalités sur hello Internet.
    >
    > toouse hello toutes les fonctionnalités de hello Ambari web l’interface utilisateur, utilisez un SSH tunnel tooproxy web trafic toohello nœud principal du cluster. Consultez [utiliser SSH Tunneling tooaccess Ambari web de l’interface utilisateur, ResourceManager, JobHistory, NameNode, Oozie et autres interfaces utilisateur web](hdinsight-linux-ambari-ssh-tunnel.md)

* **Ambari (REST)** : https://&lt;clustername&gt;.azurehdinsight.net/ambari

    > [!NOTE]
    > S’authentifier à l’aide d’un mot de passe et d’utilisateur administrateur de cluster hello.
    >
    > L’authentification en texte clair - utilisez HTTPS toohelp Assurez-vous toujours que hello connexion est sécurisée.

* **WebHCat (Templeton)** - https://&lt;clustername&gt;.azurehdinsight.net/templeton

    > [!NOTE]
    > S’authentifier à l’aide d’un mot de passe et d’utilisateur administrateur de cluster hello.
    >
    > L’authentification en texte clair - utilisez HTTPS toohelp Assurez-vous toujours que hello connexion est sécurisée.

* **SSH** - &lt;clustername&gt;-ssh.azurehdinsight.net sur le port 22 ou 23. Le port 22 est nœud primaire principal utilisé tooconnect toohello, tandis que 23 est toohello tooconnect utilisé secondaire. Pour plus d’informations sur les nœuds principal hello, consultez [clusters de disponibilité et la fiabilité de Hadoop dans HDInsight](hdinsight-high-availability-linux.md).

    > [!NOTE]
    > Vous pouvez uniquement accéder hello principal nœuds via SSH à partir d’un ordinateur client. Une fois connecté, vous pouvez ensuite accéder à des nœuds de travail hello à partir d’un nœud principal à l’aide de SSH.

## <a name="file-locations"></a>Emplacements des fichiers

Fichiers Hadoop se trouvent sur des nœuds de cluster hello en `/usr/hdp`. Ce répertoire contient hello dans les sous-répertoires de suivant :

* **2.2.4.9-1**: nom du répertoire hello est version hello Hello Hortonworks Data Platform utilisé par HDInsight. nombre de Hello sur votre cluster peut être différent de celui hello une répertoriées ici.
* **en cours**: ce répertoire contient toosubdirectories liens sous hello **2.2.4.9-1** active. Ce répertoire existe afin que vous n’avez pas numéro de version tooremember hello.

Vous trouverez des exemples de données et de fichiers JAR sur le système HDSF (Hadoop Distributed File System) dans `/example` et `/HdiSamples`.

## <a name="hdfs-azure-storage-and-data-lake-store"></a>HDFS, stockage Azure et Data Lake Store

Dans la plupart des distributions Hadoop, HDFS est sauvegardé par le stockage local sur les ordinateurs hello dans un cluster de hello. L’utilisation du stockage peut être coûteuse pour une solution basée sur le cloud où vous êtes facturé à l’heure ou à la minute pour les ressources de calcul.

HDInsight utilise les objets BLOB dans le stockage Azure ou Azure Data Lake Store comme magasin par défaut de hello. Ces services fournissent hello avantages suivants :

* Un stockage à long terme peu coûteux
* Un accès à partir de services externes tels que les sites Web, les utilitaires de téléchargement de fichier, les kits de développement logiciel (SDK) en différentes langues et les navigateurs Web

> [!WARNING]
> HDInsight prend uniquement en charge les comptes de stockage Azure à __usage général__. Il ne prend pas en charge hello __stockage d’objets Blob__ type de compte.

Un compte Azure Storage peut contenir jusqu'à too4.75 To, bien que les objets BLOB individuels (ou des fichiers d’un point de vue HDInsight) peuvent uniquement atteindre la too195 go. Azure Data Lake Store peut croître dynamiquement toohold codage de fichiers, des fichiers individuels supérieures à un pétaoctet. Pour plus d’informations, voir [Understanding blobs](https://docs.microsoft.com/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs) (Présentation des objets blob) et [Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).

Lorsque vous utilisez le stockage Azure ou Data Lake Store, vous n’avez rien de spécial à partir des données de hello HDInsight tooaccess toodo. Par exemple, hello commande suivante répertorie les fichiers Bonjour `/example/data` dossier que qu’il soit stocké sur le stockage Azure ou Data Lake Store :

    hdfs dfs -ls /example/data

### <a name="uri-and-scheme"></a>URI et schéma

Certaines commandes peuvent vous amener schéma de hello toospecify dans le cadre de hello URI lors de l’accès à un fichier. Par exemple, hello composant de Storm-HDFS requiert schéma de hello toospecify. Lorsque vous utilisez un stockage non définis par défaut (stockage ajouté en tant que cluster toohello de stockage « supplémentaire »), vous devez toujours utiliser le schéma de hello dans le cadre de hello URI.

Lorsque vous utilisez __Azure Storage__, utilisez une des hello suit les schémas d’URI :

* `wasb:///` : accès au stockage par défaut via une communication non chiffrée.

* `wasbs:///` : accès au stockage par défaut via une communication chiffrée.  schéma de wasbs Hello est pris en charge uniquement à partir de HDInsight version 3.6 et versions ultérieures.

* `wasb://<container-name>@<account-name>.blob.core.windows.net/` : utilisé pour communiquer avec un compte de stockage autre que celui par défaut. Par exemple, si vous avez un compte de stockage supplémentaire ou si vous accédez à des données stockées dans un compte de stockage accessible au public.

Lorsque vous utilisez __Data Lake Store__, utilisez une des hello suit les schémas d’URI :

* `adl:///`: Accès hello par défaut Data Lake Store pour le cluster de hello.

* `adl://<storage-name>.azuredatalakestore.net/` : utilisé pour communiquer avec un Data Lake Store autre que celui par défaut. Également utilisé tooaccess des données en dehors du répertoire racine de hello de votre cluster HDInsight.

> [!IMPORTANT]
> Lorsque vous utilisez Data Lake Store en tant que magasin par défaut de hello pour HDInsight, vous devez spécifier un chemin d’accès au sein de hello magasin toouse en tant que racine hello de stockage de HDInsight. chemin d’accès par défaut de Hello est `/clusters/<cluster-name>/`.
>
> Lorsque vous utilisez `/` ou `adl:///` tooaccess, vous pouvez uniquement accès aux données les données stockées dans la racine de hello (par exemple, `/clusters/<cluster-name>/`) du cluster de hello. données tooaccess n’importe où dans le magasin de hello, utilisez hello `adl://<storage-name>.azuredatalakestore.net/` format.

### <a name="what-storage-is-hello-cluster-using"></a>Quel type de stockage hello cluster est à l’aide

Vous pouvez utiliser la configuration de stockage par défaut Ambari tooretrieve hello pour le cluster de hello. Utilisez hello ci-dessous les informations de configuration HDFS tooretrieve curl d’à l’aide de commandes, filtrer à l’aide de [jq](https://stedolan.github.io/jq/):

```curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["fs.defaultFS"] | select(. != null)'```

> [!NOTE]
> Cela retourne hello première configuration appliquée toohello server (`service_config_version=1`), qui contient ces informations. Vous devrez peut-être toolist toutes les versions de configuration toofind hello version la plus récente.

Cette commande retourne un toohello similaire valeur suivant l’URI :

* `wasb://<container-name>@<account-name>.blob.core.windows.net` si vous utilisez un compte de stockage Azure.

    nom du compte Hello est nom hello hello Azure du compte de stockage, alors que le nom du conteneur hello est le conteneur d’objets blob hello qui est racine hello hello de stockage de cluster.

* `adl://home` si vous utilisez Azure Data Lake Store. tooget hello nom Data Lake Store, utilisez hello après l’appel REST :

    ```curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["dfs.adls.home.hostname"] | select(. != null)'```

    Cette commande renvoie hello suivant le nom d’hôte : `<data-lake-store-account-name>.azuredatalakestore.net`.

    répertoire de hello tooget au sein de la banque de hello racine hello pour HDInsight, hello utiliser après l’appel REST :

    ```curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["dfs.adls.home.mountpoint"] | select(. != null)'```

    Cette commande retourne un toohello comme chemin d’accès suivant le chemin d’accès : `/clusters/<hdinsight-cluster-name>/`.

Vous trouverez également des informations de stockage de hello à l’aide de hello portail Azure à l’aide de hello comme suit :

1. Bonjour [portail Azure](https://portal.azure.com/), sélectionnez votre cluster HDInsight.

2. À partir de hello **propriétés** section, sélectionnez **comptes de stockage**. informations de stockage Hello pour le cluster de hello s’affiche.

### <a name="how-do-i-access-files-from-outside-hdinsight"></a>Comment accéder à des fichiers situés en dehors de HDInsight ?

Il existe un différentes manières tooaccess des données à partir du cluster HDInsight de hello en dehors. Hello Voici quelques liens tooutilities et les kits de développement logiciel qui peuvent être utilisé toowork avec vos données :

Si vous utilisez __Azure Storage__, consultez hello suivant les liens pour les méthodes que vous pouvez accéder à vos données :

* [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2): commandes de l’interface de ligne de commande fonctionnant avec Azure. Après l’installation, utilisez hello `az storage` commande de l’aide sur l’utilisation du stockage, ou `az storage blob` pour des commandes spécifiques à l’objet blob.
* [blobxfer.py](https://github.com/Azure/azure-batch-samples/tree/master/Python/Storage): script python pour travailler avec des objets blob dans Azure Storage.
* Divers Kits de développement logiciel (SDK) :

    * [Java](https://github.com/Azure/azure-sdk-for-java)
    * [Node.JS](https://github.com/Azure/azure-sdk-for-node)
    * [PHP](https://github.com/Azure/azure-sdk-for-php)
    * [Python](https://github.com/Azure/azure-sdk-for-python)
    * [Ruby](https://github.com/Azure/azure-sdk-for-ruby)
    * [.NET](https://github.com/Azure/azure-sdk-for-net)
    * [API REST d’Azure Storage](https://msdn.microsoft.com/library/azure/dd135733.aspx)

Si vous utilisez __Azure Data Lake Store__, consultez hello suivant les liens pour les méthodes que vous pouvez accéder à vos données :

* [Navigateur Web](../data-lake-store/data-lake-store-get-started-portal.md)
* [PowerShell](../data-lake-store/data-lake-store-get-started-powershell.md)
* [Azure CLI 2.0](../data-lake-store/data-lake-store-get-started-cli-2.0.md)
* [API REST WebHDFS](../data-lake-store/data-lake-store-get-started-rest-api.md)
* [Data Lake Tools pour Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504)
* [.NET](../data-lake-store/data-lake-store-get-started-net-sdk.md)
* [Java](../data-lake-store/data-lake-store-get-started-java-sdk.md)
* [Python](../data-lake-store/data-lake-store-get-started-python.md)

## <a name="scaling"></a>Mise à l’échelle de votre cluster

cluster Hello mise à l’échelle de fonctionnalité vous permet de numéro de hello toodynamically modification de nœuds de données utilisé par un cluster. Vous pouvez effectuer des opérations de mise à l’échelle pendant que d’autres travaux ou processus s’exécutent sur un cluster.

types de cluster différent Hello sont affectés par la mise à l’échelle comme suit :

* **Hadoop**: lorsque vous diminuez le nombre de hello de nœuds dans un cluster, certains services hello dans un cluster de hello sont redémarrés. Opérations de mise à l’échelle peut entraîner des travaux en cours d’exécution ou en attente de toofail à l’achèvement de hello Hello opération de mise à l’échelle. Vous pouvez renvoyer les tâches de hello une fois l’opération hello est terminée.
* **HBase**: serveurs régionaux sont automatiquement équilibrés quelques minutes après l’achèvement de l’opération de mise à l’échelle de hello. serveurs régionaux solde de toomanually, utilisez hello comme suit :

    1. Connectez le cluster HDInsight de toohello à l’aide de SSH. Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

    2. Utilisez hello suivant du shell HBase de hello toostart :

            hbase shell

    3. Une fois chargé, hello shell HBase utilisez hello suivant les serveurs régionaux toomanually solde hello :

            balancer

* **Storm** : vous devez rééquilibrer les topologies Storm en cours d’exécution après l’exécution d’une opération de mise à l’échelle. Rééquilibrage permet de paramètres de parallélisme hello topologie tooreadjust selon hello nouveau nombre de nœuds de cluster de hello. topologies de toorebalance en cours d’exécution, utilisez une des options suivantes de hello :

    * **SSH**: connecter toohello serveur et les suivants de hello d’utilisation des commandes toorebalance une topologie :

            storm rebalance TOPOLOGYNAME

        Vous pouvez également spécifier des indicateurs de parallélisme paramètres toooverride hello initialement fournis par une topologie de hello. Par exemple, `storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10` reconfigure hello le processus de travail too5 topologie et les exécuteurs de 10 pour le composant de jaune-éclair hello 3 exécuteurs pour le composant bleu-bec de hello.

    * **L’interface utilisateur de renverser**: utilisez hello étapes suivantes décrites toorebalance une topologie à l’aide de hello Storm UI.

        1. Ouvrez **https://CLUSTERNAME.azurehdinsight.net/stormui** dans votre navigateur web, où CLUSTERNAME est nom hello de votre cluster Storm. Si vous y êtes invité, entrez le nom de l’administrateur (admin) du cluster HDInsight hello et le mot de passe spécifié lors de la création du cluster de hello.
        2. Sélectionnez hello topologie que vous souhaitez toorebalance, puis sélectionnez hello **rééquilibrer** bouton. Entrer un délai de hello avant hello rééquilibrage opération est effectuée.

Pour obtenir des informations spécifiques sur la mise à l’échelle de votre cluster HDInsight, consultez :

* [Gérer les clusters Hadoop dans HDInsight à l’aide de hello portail Azure](hdinsight-administer-use-portal-linux.md#scale-clusters)
* [Gestion des clusters Hadoop dans HDInsight au moyen d’Azure PowerShell](hdinsight-administer-use-command-line.md#scale-clusters)

## <a name="how-do-i-install-hue-or-other-hadoop-component"></a>Comment installer Hue (ou un autre composant Hadoop) ?

HDInsight est un service géré. Si Azure détecte un problème avec le cluster de hello, il peut supprimer hello Échec de nœud et créer un nœud tooreplace il. Si vous installez manuellement des éléments sur le cluster de hello, elles ne sont pas conservées lors de cette opération se produit. Utilisez plutôt [Actions de script HDInsight](hdinsight-hadoop-customize-cluster.md). Une action de script peut être hello utilisé toomake modifications suivantes :

* Installer et configurer un service ou un site web comme Spark ou Hue.
* Installez et configurez un composant qui nécessite des modifications de configuration sur plusieurs nœuds de cluster de hello. Par exemple, une variable d’environnement nécessaire, la création d’un répertoire de journalisation ou la création d’un fichier de configuration.

Les actions de script sont des scripts Bash. les scripts Hello exécuter lors de la configuration de cluster et peuvent être utilisé tooinstall et configurer des composants supplémentaires sur le cluster de hello. Les exemples de script sont fournies pour l’installation de hello suivant des composants :

* [Hue](hdinsight-hadoop-hue-linux.md)
* [Giraph](hdinsight-hadoop-giraph-install-linux.md)
* [Solr](hdinsight-hadoop-solr-install-linux.md)

Pour plus d’informations sur le développement de vos propres actions de script, consultez [Développement d’actions de Script avec HDInsight](hdinsight-hadoop-script-actions-linux.md).

### <a name="jar-files"></a>Fichiers Jar

Certaines technologies Hadoop sont fournies dans des fichiers jar autonomes, qui contiennent des fonctions utilisées dans le cadre d’un travail MapReduce ou à partir de Pig ou Hive. Alors que ceux-ci peuvent être installées à l’aide des Actions de Script, ils souvent ne nécessitent pas de configuration et peuvent être téléchargé toohello cluster après la mise en service et utilisées directement. Si vous souhaitez que le composant de hello que toomake survit à la réinitialisation du cluster de hello, vous pouvez stocker le fichier jar hello dans le stockage par défaut hello pour votre cluster (WASB ou ADL).

Par exemple, si vous souhaitez que la version la plus récente hello toouse de [DataFu](http://datafu.incubator.apache.org/), vous pouvez télécharger le fichier jar contenant le projet de hello et téléchargez-le toohello HDInsight cluster. Puis suivez documentation de DataFu hello toouse de Pig ou Hive.

> [!IMPORTANT]
> Certains composants sont des fichiers jar autonome sont fournis avec HDInsight, mais ne sont pas dans le chemin d’accès hello. Si vous recherchez un composant spécifique, vous pouvez utiliser hello suivez toosearch pour celui-ci sur votre cluster :
>
> ```find / -name *componentname*.jar 2>/dev/null```
>
> Cette commande retourne le chemin d’accès de hello de tous les fichiers jar correspondant.

toouse une version différente d’un composant de téléchargement hello version vous avez besoin et l’utiliser dans vos tâches.

> [!WARNING]
> Les composants fournis avec le cluster HDInsight de hello sont entièrement gérés et le Support technique de Microsoft vous aide à tooisolate et résoudre les problèmes connexes toothese composants.
>
> Les composants personnalisés de réception efforcera toohelp vous toofurther hello de dépannage. Cela peut entraîner hello de résoudre ou demandant que vous tooengage les canaux disponibles pour hello ouvrir technologies source où se trouve une grande expérience pour cette technologie. Vous pouvez, par exemple, utiliser de nombreux sites de communauté, comme le [forum MSDN sur HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). En outre, les projets Apache ont des sites de projet sur [http://apache.org](http://apache.org) ; par exemple, [Hadoop](http://hadoop.apache.org/) ou [Spark](http://spark.apache.org/).

## <a name="next-steps"></a>Étapes suivantes

* [Migrer à partir de HDInsight basés sur Windows basée sur les tooLinux](hdinsight-migrate-from-windows-to-linux.md)
* [Utilisation de Hive avec HDInsight](hdinsight-use-hive.md)
* [Utilisation de Pig avec HDInsight](hdinsight-use-pig.md)
* [Utilisation des tâches MapReduce avec HDInsight](hdinsight-use-mapreduce.md)
