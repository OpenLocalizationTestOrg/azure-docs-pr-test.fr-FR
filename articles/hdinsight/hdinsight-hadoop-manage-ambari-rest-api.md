---
title: "aaaMonitor et gérer Hadoop avec l’API REST de Ambari - Azure HDInsight | Documents Microsoft"
description: "Découvrez comment toouse Ambari toomonitor et gérer des clusters Hadoop dans HDInsight de Azure. Dans ce document, vous allez apprendre comment toouse hello API REST de Ambari inclus avec HDInsight clusters."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2400530f-92b3-47b7-aa48-875f028765ff
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: 1866a77c8e402231bccbcfba7174253aca41339b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hdinsight-clusters-by-using-hello-ambari-rest-api"></a>Gérer des clusters HDInsight à l’aide de hello API REST de Ambari

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

Découvrez comment toouse hello API REST de Ambari toomanage et analyser les clusters Hadoop dans HDInsight de Azure.

Apache Ambari simplifie la gestion de hello et la surveillance d’un cluster Hadoop en fournissant un web toouse simple API REST et de l’interface utilisateur. Ambari est inclus dans les clusters HDInsight qui utilisent le système d’exploitation de Linux hello. Vous pouvez utiliser Ambari toomonitor hello cluster et apporter des modifications de configuration.

## <a id="whatis"></a>Présentation d'Ambari

[Apache Ambari](http://ambari.apache.org) fournit l’interface utilisateur web qui peut être utilisée tooprovision, gérer et surveiller les clusters Hadoop. Les développeurs peuvent intégrer ces fonctionnalités dans leurs applications à l’aide de hello [API REST de Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).

Ambari est fourni par défaut avec les clusters HDInsight Linux.

## <a name="how-toouse-hello-ambari-rest-api"></a>Comment toouse hello API REST de Ambari

> [!IMPORTANT]
> informations de Hello et d’exemples dans ce document nécessitent un cluster HDInsight qui utilise le système d’exploitation Linux. Pour plus d'informations, consultez [Prise en main de HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).

exemples de Hello dans ce document sont fournies pour hello Bourne shell (interpréteur de commandes) et PowerShell. bash Hello exemples ont été testés avec GNU bash 4.3.11, mais doit fonctionner avec d’autres interpréteurs de commandes Unix. exemples de PowerShell Hello ont été testés avec PowerShell 5.0, mais doivent fonctionner avec PowerShell 3.0 ou version ultérieure.

Si vous utilisez hello __Bourne shell__ (interpréteur de commandes), vous devez disposer de hello installé :

* [cURL](http://curl.haxx.se/): cURL est un utilitaire qui peut être toowork utilisé avec l’API REST à partir de la ligne de commande hello. Dans ce document, il est utilisé toocommunicate avec hello Ambari REST API.

Que vous utilisiez Bash ou PowerShell, vous devez également avoir installé [jq](https://stedolan.github.io/jq/). Jq est un utilitaire permettant de travailler avec des documents JSON. Il est utilisé dans **tous les** hello des exemples de l’interpréteur de commandes, et **un** des exemples de PowerShell hello.

### <a name="base-uri-for-ambari-rest-api"></a>URI de base pour l’API Rest Ambari

URI de base pour l’API REST de Ambari sur HDInsight de hello Hello est https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME, où **CLUSTERNAME** est le nom hello de votre cluster.

> [!IMPORTANT]
> Alors que le nom du cluster hello Bonjour complet partie de nom de domaine de hello URI (CLUSTERNAME.azurehdinsight.net) respecte la casse, autres occurrences Bonjour URI respectent la casse. Par exemple, si votre cluster est nommé `MyCluster`, hello Voici URI valide :
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/MyCluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/MyCluster`
> 
> suit Hello URI renvoie une erreur car hello deuxième occurrence du nom de hello n’est pas hello corrige le cas.
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/mycluster`

### <a name="authentication"></a>Authentification

Connexion tooAmbari sur HDInsight nécessite HTTPS. Nom du compte administrateur utilisez hello (valeur par défaut hello est **admin**) et le mot de passe fourni lors de la création du cluster.

## <a name="examples-authentication-and-parsing-json"></a>Exemples : Authentification et analyse de JSON

Hello suivant exemples montrent comment toomake une demande GET hello Ambari REST API de base :

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
```

> [!IMPORTANT]
> exemples d’interpréteur de commandes Hello dans ce document apporter hello suivant hypothèses :
>
> * nom de connexion de Hello pour le cluster de hello est la valeur par défaut hello `admin`.
> * `$PASSWORD`contient le mot de passe hello hello commande de connexion HDInsight. Vous pouvez définir cette valeur à l’aide de `PASSWORD='mypassword'`.
> * `$CLUSTERNAME`contient le nom hello du cluster de hello. Vous pouvez définir cette valeur à l’aide de `set CLUSTERNAME='clustername'`.

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$resp.Content
```

> [!IMPORTANT]
> exemples de PowerShell Hello dans ce document apporter hello suivant hypothèses :
>
> * `$creds`est un objet d’informations d’identification qui contient la connexion d’administration hello et un mot de passe pour le cluster de hello. Vous pouvez définir cette valeur à l’aide de `$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"` et en fournissant des informations d’identification hello lorsque vous y êtes invité.
> * `$clusterName`est une chaîne qui contient le nom hello du cluster de hello. Vous pouvez définir cette valeur à l’aide de `$clusterName="clustername"`.

Les deux exemples de retournent un document JSON qui commence avec les informations toohello semblable l’exemple suivant :

```json
{
"href" : "http://10.0.0.10:8080/api/v1/clusters/CLUSTERNAME",
"Clusters" : {
    "cluster_id" : 2,
    "cluster_name" : "CLUSTERNAME",
    "health_report" : {
    "Host/stale_config" : 0,
    "Host/maintenance_state" : 0,
    "Host/host_state/HEALTHY" : 7,
    "Host/host_state/UNHEALTHY" : 0,
    "Host/host_state/HEARTBEAT_LOST" : 0,
    "Host/host_state/INIT" : 0,
    "Host/host_status/HEALTHY" : 7,
    "Host/host_status/UNHEALTHY" : 0,
    "Host/host_status/UNKNOWN" : 0,
    "Host/host_status/ALERT" : 0
    ...
```

### <a name="parsing-json-data"></a>Analyse des données JSON

Hello exemple suivant utilise `jq` tooparse hello document de réponse JSON et afficher uniquement hello `health_report` plus d’informations à partir des résultats de hello.

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME" \
| jq '.Clusters.health_report'
```

PowerShell 3.0 et versions ultérieures fournit hello `ConvertFrom-Json` applet de commande, qui convertit le document JSON de hello dans un objet qui est plus facile toowork avec à partir de PowerShell. Hello exemple suivant utilise `ConvertFrom-Json` hello uniquement de toodisplay `health_report` plus d’informations à partir des résultats de hello.

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.Clusters.health_report
```

> [!NOTE]
> Alors que la plupart des exemples de ce document, utilisez `ConvertFrom-Json` toodisplay des éléments à partir du document de réponse hello, hello [configuration de la mise à jour Ambari](#example-update-ambari-configuration) exemple utilise jq. Jq est utilisé dans cet exemple tooconstruct un nouveau modèle de document de réponse JSON hello.

Pour obtenir une référence complète de hello API REST, consultez [V1 de référence d’API Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).

## <a name="example-get-hello-fqdn-of-cluster-nodes"></a>Exemple : Obtenir hello FQDN des nœuds de cluster

Lorsque vous travaillez avec HDInsight, vous devrez peut-être le nom de domaine complet de hello tooknow (FQDN) d’un nœud de cluster. Vous pouvez facilement récupérer hello nom de domaine complet pour hello différents nœuds dans le cluster hello à l’aide de hello exemple suivant :

* **Tous les nœuds**

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts" \
    | jq '.items[].Hosts.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/hosts" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.Hosts.host_name
    ```

* **Nœuds principaux**

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HDFS/components/NAMENODE" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HDFS/components/NAMENODE" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

* **Nœuds de travail**

    ```bash
    curl -u admin:PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/HDFS/components/DATANODE" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HDFS/components/DATANODE" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

* **Nœuds Zookeeper**

    ```bash
    curl -u admin:PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

## <a name="example-get-hello-internal-ip-address-of-cluster-nodes"></a>Exemple : Obtenir l’adresse IP interne de hello des nœuds de cluster

> [!IMPORTANT]
> adresses IP de Hello retournées par les exemples hello dans cette section sont pas directement accessibles sur hello internet. Elles sont uniquement accessibles hello réseau virtuel Azure qui contient le cluster HDInsight de hello.
>
> Pour plus d’informations sur l’utilisation de HDInsight et des réseaux virtuels, consultez [Étendre les fonctionnalités HDInsight à l’aide d’un réseau virtuel Azure personnalisé](hdinsight-extend-hadoop-virtual-network.md).

adresse IP de hello toofind, vous devez connaître le nom hello interne de domaine complet (FQDN) de hello des nœuds de cluster. Une fois que vous avez hello nom de domaine complet, vous pouvez ensuite obtenir l’adresse IP de hello d’hôte de hello. Hello exemples suivants tout d’abord interroger Ambari pourquoi le nom de domaine complet de tous les nœuds d’hôte hello, puis interroge Ambari pour l’adresse IP de hello de chaque hôte.

```bash
for HOSTNAME in $(curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts" | jq -r '.items[].Hosts.host_name')
do
    IP=$(curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts/$HOSTNAME" | jq -r '.Hosts.ip')
  echo "$HOSTNAME <--> $IP"
done
```

```powershell
$uri = "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/hosts"
$resp = Invoke-WebRequest -Uri $uri -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
foreach($item in $respObj.items) {
    $hostName = [string]$item.Hosts.host_name
    $hostInfoResp = Invoke-WebRequest -Uri "$uri/$hostName" `
        -Credential $creds
    $hostInfoObj = ConvertFrom-Json $hostInfoResp 
    $hostIp = $hostInfoObj.Hosts.ip
    "$hostName <--> $hostIp"
}
```

## <a name="example-get-hello-default-storage"></a>Exemple : Obtenir du stockage par défaut hello

Lorsque vous créez un cluster HDInsight, vous devez utiliser un compte de stockage Azure ou le Data Lake Store en tant que stockage de hello par défaut pour le cluster de hello. Vous pouvez utiliser ces informations à Ambari tooretrieve après que hello cluster a été créé. Par exemple, si vous souhaitez que le conteneur de toohello données tooread/écriture à l’extérieur de HDInsight.

Hello exemples suivants extraire configuration de stockage par défaut hello de cluster de hello :

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
| jq '.items[].configurations[].properties["fs.defaultFS"] | select(. != null)'
```

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties.'fs.defaultFS'
```

> [!IMPORTANT]
> Les exemples ci-après renvoient hello première configuration appliquée toohello server (`service_config_version=1`) qui contient ces informations. Si vous récupérez une valeur qui a été modifiée après la création du cluster, vous ont besoin des versions de configuration toolist hello et récupérer la version la plus récente de hello.

valeur de retour de Hello est similaire tooone Hello exemple suivant :

* `wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net`-Cette valeur indique que ce cluster hello utilise un compte de stockage Azure pour le stockage de la valeur par défaut. Hello `ACCOUNTNAME` valeur est le nom hello hello du compte de stockage. Hello `CONTAINER` partie est le nom de hello du conteneur d’objets blob hello hello compte de stockage. conteneur de Hello est racine hello hello stockage compatible de HDFS pour le cluster de hello.

* `adl://home`-Cette valeur indique que le cluster hello utilise une Azure Data Lake Store pour le stockage de la valeur par défaut.

    toofind hello nom du compte Data Lake Store, utilisez hello exemple suivant :

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
    | jq '.items[].configurations[].properties["dfs.adls.home.hostname"] | select(. != null)'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.configurations.properties.'dfs.adls.home.hostname'
    ```

    Hello valeur de retour est similaire trop`ACCOUNTNAME.azuredatalakestore.net`, où `ACCOUNTNAME` est le nom hello Hello compte Data Lake Store.

    répertoire hello toofind Data Lake Store qui contient le stockage hello pour cluster hello, hello utilisez exemple suivant :

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
    | jq '.items[].configurations[].properties["dfs.adls.home.mountpoint"] | select(. != null)'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.configurations.properties.'dfs.adls.home.mountpoint'
    ```

    Hello valeur de retour est similaire trop`/clusters/CLUSTERNAME/`. Cette valeur est un chemin d’accès au sein de hello compte Data Lake Store. Ce chemin d’accès est la racine hello hello système de fichier compatible HDFS pour le cluster de hello. 

> [!NOTE]
> Hello `Get-AzureRmHDInsightCluster` applet de commande fournie par [Azure PowerShell](/powershell/azure/overview) également retourne hello les informations de stockage de cluster de hello.


## <a name="example-get-configuration"></a>Exemple : obtenir la configuration

1. Obtenir des configurations de hello qui sont disponibles pour votre cluster.

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    $respObj = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    $respObj.Content
    ```

    Cet exemple retourne un document JSON contenant la configuration actuelle de hello (identifié par hello *balise* valeur) pour les composants hello installés sur le cluster de hello. Hello exemple suivant est un extrait à partir des données hello retournés à partir d’un type de cluster Spark.
   
   ```json
   "spark-metrics-properties" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   },
   "spark-thrift-fairscheduler" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   },
   "spark-thrift-sparkconf" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   }
   ```

2. Obtenir la configuration hello pour le composant hello qui vous intéressez. Bonjour à l’exemple, remplacez `INITIAL` avec la valeur de balise hello retourné à partir de la demande précédente de hello.

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=core-site&tag=INITIAL"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations?type=core-site&tag=INITIAL" `
        -Credential $creds
    $resp.Content
    ```

    Cet exemple retourne un document JSON contenant la configuration actuelle de hello pour hello `core-site` composant.

## <a name="example-update-configuration"></a>Exemple : mettre à jour la configuration

1. Obtenir la configuration actuelle de hello, qui stocke les Ambari hello souhaitée « configuration » :

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    ```

    Cet exemple retourne un document JSON contenant la configuration actuelle de hello (identifié par hello *balise* valeur) pour les composants hello installés sur le cluster de hello. Hello exemple suivant est un extrait à partir des données hello retournés à partir d’un type de cluster Spark.
   
    ```json
    "spark-metrics-properties" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    },
    "spark-thrift-fairscheduler" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    },
    "spark-thrift-sparkconf" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    }
    ```
   
    Dans cette liste, vous avez besoin d’un nom de hello de toocopy du composant de hello (par exemple, **spark\_thrift\_sparkconf** et hello **balise** valeur.

2. Récupérer configuration hello pour le composant de hello et de la balise à l’aide de hello suivant de commandes :
   
    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=spark-thrift-sparkconf&tag=INITIAL" \
    | jq --arg newtag $(echo version$(date +%s%N)) '.items[] | del(.href, .version, .Config) | .tag |= $newtag | {"Clusters": {"desired_config": .}}' > newconfig.json
    ```

    ```powershell
    $epoch = Get-Date -Year 1970 -Month 1 -Day 1 -Hour 0 -Minute 0 -Second 0
    $now = Get-Date
    $unixTimeStamp = [math]::truncate($now.ToUniversalTime().Subtract($epoch).TotalMilliSeconds)
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations?type=spark-thrift-sparkconf&tag=INITIAL" `
        -Credential $creds
    $resp.Content | jq --arg newtag "version$unixTimeStamp" '.items[] | del(.href, .version, .Config) | .tag |= $newtag | {"Clusters": {"desired_config": .}}' > newconfig.json
    ```

    > [!NOTE]
    > Remplacez **spark-thrift-sparkconf** et **initiale** avec le composant de hello et la balise que vous voulez tooretrieve configuration hello.
   
    Jq donnée utilisé tooturn hello récupérées à partir de HDInsight dans un nouveau modèle de configuration. Plus précisément, ces exemples effectuent hello suivant des actions :
   
    * Crée une valeur unique qui contient « version » de chaîne hello et date hello, qui est stocké dans `newtag`.

    * Crée un document racine pour la nouvelle configuration de votre choix hello.

    * Obtient hello contenu Hello `.items[]` de tableau et l’ajoute sous hello **desired_config** élément.

    * Suppressions hello `href`, `version`, et `Config` éléments, en tant que ces éléments ne sont pas nécessaire toosubmit une nouvelle configuration.

    * Ajoute un élément `tag` avec une valeur de `version#################`. partie numérique de Hello repose sur hello date actuelle. Chaque configuration doit avoir une balise unique.
     
    Enfin, les données de salutation sont enregistrées toohello `newconfig.json` document. structure du document Hello doit apparaître toohello similaire, l’exemple suivant :
     
     ```json
    {
        "Clusters": {
            "desired_config": {
            "tag": "version1459260185774265400",
            "type": "spark-thrift-sparkconf",
            "properties": {
                ....
            },
            "properties_attributes": {
                ....
            }
        }
    }
    ```

3. Ouvrez hello `newconfig.json` document et modifier/ajouter des valeurs Bonjour `properties` objet. valeur de hello Hello exemple suivant modifie `"spark.yarn.am.memory"` de `"1g"` trop`"3g"`. Il ajoute également `"spark.kryoserializer.buffer.max"` avec une valeur de `"256m"`.
   
        "spark.yarn.am.memory": "3g",
        "spark.kyroserializer.buffer.max": "256m",
   
    Enregistrer le fichier de hello une fois que vous avez terminé d’apporter de modifications.

4. Utilisez hello suivant tooAmbari de configuration de commandes toosubmit hello mis à jour.
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" -X PUT -d @newconfig.json "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
    ```

    ```powershell
    $newConfig = Get-Content .\newconfig.json
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body $newConfig
    $resp.Content
    ```
   
    Ces commandes Soumettre contenu hello Hello **newconfig.json** fichier toohello cluster convenance hello nouvelle configuration. demande de Hello renvoie un document JSON. Hello **versionTag** élément dans ce document doit correspondre à version hello vous soumis et hello **configurations** objet contient des modifications de configuration hello que vous avez demandée.

### <a name="example-restart-a-service-component"></a>Exemple : redémarrer un composant de service

À ce stade, si vous examinez l’interface utilisateur web de Ambari hello, hello service Spark indique qu’il doit toobe redémarré pour que la nouvelle configuration de hello puisse prendre effet. Utilisez hello après étapes toorestart hello service.

1. Utilisez hello suivant le mode de maintenance tooenable pour hello service Spark :

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo": {"context": "turning on maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"ON"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo": {"context": "turning on maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"ON"}}}'
    $resp.Content
    ```
   
    Ces commandes envoient un serveur de toohello document JSON qui active le mode de maintenance. Vous pouvez vérifier que hello service est maintenant en mode de maintenance à l’aide de hello demande :
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK" \
    | jq .ServiceInfo.maintenance_state
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK2" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.ServiceInfo.maintenance_state
    ```
   
    Hello valeur de retour est `ON`.

2. Ensuite, utilisez hello suivant tooturn hors service de hello :

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"INSTALLED"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"INSTALLED"}}}'
    $resp.Content
    ```
    
    réponse de Hello est similaire toohello l’exemple suivant :
   
    ```json
    {
        "href" : "http://10.0.0.18:8080/api/v1/clusters/CLUSTERNAME/requests/29",
        "Requests" : {
            "id" : 29,
            "status" : "Accepted"
        }
    }
    ```
    
    > [!IMPORTANT]
    > Hello `href` valeur retournée par cet URI utilise hello une adresse IP interne hello du nœud de cluster. toouse à partir du cluster en dehors de hello, remplacez partie de hello '10.0.0.18:8080' hello nom de domaine complet du cluster de hello. 
    
    Hello suivant les commandes récupérer l’état de hello de demande de hello :

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/requests/29" \
    | jq .Requests.request_status
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/requests/29" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.Requests.request_status
    ```

    Une réponse de `COMPLETED` indique que la demande de hello.

3. Une fois la demande précédente de hello terminée, utilisez hello après toostart hello service.
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"STARTED"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```
   
    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"STARTED"}}}'
    ```
    service de Hello utilise maintenant la configuration de nouveau hello.

4. Enfin, utilisez hello suivant tooturn désactiver le mode maintenance.
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo": {"context": "turning off maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"OFF"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo": {"context": "turning off maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"OFF"}}}'
    ```

## <a name="next-steps"></a>Étapes suivantes

Pour obtenir une référence complète de hello API REST, consultez [V1 de référence d’API Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).

