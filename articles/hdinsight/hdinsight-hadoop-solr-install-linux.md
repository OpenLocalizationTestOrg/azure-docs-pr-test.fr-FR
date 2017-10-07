---
title: "Action de Script d’aaaUse tooinstall Solr sur HDInsight basés sur Linux - Azure | Documents Microsoft"
description: "Découvrez comment tooinstall Solr sur basés sur Linux HDInsight Hadoop clusters à l’aide des Actions de Script."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: cc93ed5c-a358-456a-91a4-f179185c0e98
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: larryfr
ms.openlocfilehash: 4c179032b95ae187f1830d8927f8796372fa8ebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-solr-on-hdinsight-hadoop-clusters"></a>Installation et utilisation de Solr sur des clusters HDInsight Hadoop

Découvrez comment tooinstall Solr sur Azure HDInsight en utilisant l’Action de Script. Solr est une puissante plateforme de recherche qui fournit des fonctionnalités de recherche au niveau de l'entreprise pour les données gérées par Hadoop.

> [!IMPORTANT]
    > étapes de Hello dans ce document nécessitent un cluster HDInsight qui utilise Linux. Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

> [!IMPORTANT]
> exemple de script Hello utilisé dans ce document installe Solr 4.9 avec une configuration spécifique. Si vous souhaitez que le cluster de Solr hello tooconfigure avec différents regroupements, partitions, schémas, les réplicas, etc., vous devez modifier le script de hello et les fichiers binaires de Solr.

## <a name="whatis"></a>Présentation de Solr

[Apache Solr](http://lucene.apache.org/solr/features.html) est une plateforme de recherche d’entreprise qui permet d’effectuer de puissantes opérations de recherche en texte intégral sur des données. Tandis que Hadoop permet de stocker et gérer des quantités importantes de données, Apache Solr fournit les fonctionnalités de recherche hello tooquickly extraire des données hello.

> [!WARNING]
> Composants fournis avec le cluster HDInsight de hello sont entièrement pris en charge par Microsoft.
>
> Les composants personnalisés, tels que Solr, réception efforcera toohelp vous toofurther hello de dépannage. Prise en charge de Microsoft ne peut pas être en mesure de tooresolve des problèmes avec des composants personnalisés. Vous devrez peut-être les Communautés de tooengage hello open source pour obtenir une assistance. Vous pouvez, par exemple, utiliser de nombreux sites de communauté, comme le [forum MSDN sur HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). En outre, les projets Apache ont des sites de projet sur [http://apache.org](http://apache.org). Par exemple : [Hadoop](http://hadoop.apache.org/).

## <a name="what-hello-script-does"></a>Le script hello effectue

Ce script fait hello suivant du cluster HDInsight de toohello modifications :

* Installe Solr 4.9 dans `/usr/hdp/current/solr`
* Crée un utilisateur, **solrusr**, qui est utilisé toorun hello Solr service
* Jeux de **solruser** en tant que propriétaire hello de`/usr/hdp/current/solr`
* Ajoute une configuration [Upstart](http://upstart.ubuntu.com/) qui démarre Solr automatiquement.

## <a name="install"></a>Installer Solr à l’aide d’actions de script

Un tooinstall de script d’exemple Solr sur un cluster HDInsight est disponible à l’adresse hello l’emplacement suivant :

    https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh

toocreate un cluster avec Solr installé, utilisez hello étapes Bonjour [HDInsight de créer des clusters](hdinsight-hadoop-create-linux-clusters-portal.md) document. Au cours du processus de création de hello, utilisez hello suivant les étapes tooinstall Solr :

1. À partir de hello __résumé du Cluster__ settings__ select__Advanced, puis les lames, __actions de Script__. Utilisez hello suivant formulaire hello toopopulate :

   * **NOM**: entrez un nom convivial pour l’action de script hello.
   * **URI du script** : https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh
   * **HEAD**: cochez cette option.
   * **WORKER** : cochez cette option
   * **SOIGNEUR**: Vérifiez tooinstall de cette option sur le nœud de soigneur hello
   * **PARAMETERS**: laissez ce champ vide.

2. En bas de hello Hello **actions de Script** panneau, utilisez hello **sélectionnez** configuration hello toosave du bouton. Enfin, utilisez hello **suivant** bouton tooreturn toohello __résumé du Cluster__

3. À partir de hello __résumé du Cluster__ page, sélectionnez __créer__ cluster hello de toocreate.

## <a name="usesolr"></a>Utilisation de Solr dans HDInsight

> [!IMPORTANT]
> étapes Hello de cette section présentent les fonctionnalités de Solr base. Pour plus d’informations sur l’utilisation de Solr, consultez hello [Apache Solr site](http://lucene.apache.org/solr/).

### <a name="index-data"></a>Données d'index

Utilisez hello suivant les étapes tooadd exemple données tooSolr, puis de la requête :

1. Connecter le cluster HDInsight de toohello à l’aide de SSH :

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

     > [!IMPORTANT]
     > Plus loin dans ce document utilisent un SSL tunnel tooconnect toohello Solr interface utilisateur web. toouse ces étapes, vous devez établir une connexion SSL du tunnel, puis configurez votre navigateur toouse il.
     >
     > Pour plus d’informations, consultez hello [utiliser SSH Tunneling hdinsight](hdinsight-linux-ambari-ssh-tunnel.md) document.

2. Utilisez hello commandes toohave Solr index exemple données suivantes :

    ```bash
    cd /usr/hdp/current/solr/example/exampledocs
    java -jar post.jar solr.xml monitor.xml
    ```

    Hello le résultat suivant toohello console :

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes toohttp://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    Hello `post.jar` utilitaire ajoute hello **solr.xml** et **monitor.xml** index toohello de documents.
  
3. Utilisez hello suivant commande tooquery hello Solr REST API :

    ```bash
    curl "http://localhost:8983/solr/collection1/select?q=*%3A*&wt=json&indent=true"
    ```

    Cette commande recherche **collection1** les documents correspondant à  **\*:\***  (encodé sous la forme \*% 3 a\* dans la chaîne de requête hello). Hello suivant du document JSON est un exemple de réponse de hello :

            "response": {
                "numFound": 2,
                "start": 0,
                "maxScore": 1,
                "docs": [
                  {
                    "id": "SOLR1000",
                    "name": "Solr, hello Enterprise Search Server",
                    "manu": "Apache Software Foundation",
                    "cat": [
                      "software",
                      "search"
                    ],
                    "features": [
                      "Advanced Full-Text Search Capabilities using Lucene",
                      "Optimized for High Volume Web Traffic",
                      "Standards Based Open Interfaces - XML and HTTP",
                      "Comprehensive HTML Administration Interfaces",
                      "Scalability - Efficient Replication tooother Solr Search Servers",
                      "Flexible and Adaptable with XML configuration and Schema",
                      "Good unicode support: héllo (hello with an accent over hello e)"
                    ],
                    "price": 0,
                    "price_c": "0,USD",
                    "popularity": 10,
                    "inStock": true,
                    "incubationdate_dt": "2006-01-17T00:00:00Z",
                    "_version_": 1486960636996878300
                  },
                  {
                    "id": "3007WFP",
                    "name": "Dell Widescreen UltraSharp 3007WFP",
                    "manu": "Dell, Inc.",
                    "manu_id_s": "dell",
                    "cat": [
                      "electronics and computer1"
                    ],
                    "features": [
                      "30\" TFT active matrix LCD, 2560 x 1600, .25mm dot pitch, 700:1 contrast"
                    ],
                    "includes": "USB cable",
                    "weight": 401.6,
                    "price": 2199,
                    "price_c": "2199,USD",
                    "popularity": 6,
                    "inStock": true,
                    "store": "43.17614,-90.57341",
                    "_version_": 1486960637584081000
                  }
                ]
              }

### <a name="using-hello-solr-dashboard"></a>À l’aide du tableau de bord hello Solr

tableau de bord Solr Hello est une interface utilisateur qui vous permet de toowork avec Solr via votre navigateur web. tableau de bord Solr Hello n’est pas exposée directement sur hello Internet à partir de votre cluster HDInsight. Vous pouvez utiliser un tooaccess de tunnel SSH il. Pour plus d’informations sur l’utilisation d’un tunnel SSH, consultez hello [utiliser SSH Tunneling hdinsight](hdinsight-linux-ambari-ssh-tunnel.md) document.

Une fois que vous avez établi un tunnel SSH, utilisez hello suivant du tableau de bord étapes toouse hello Solr :

1. Déterminer le nom d’hôte hello pour le nœud principal de principal hello :

   1. Utilisez le nœud principal du cluster toohello tooconnect SSH. Par exemple, `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.

       Pour plus d’informations sur l’utilisation de SSH, consultez hello [utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

   2. Utilisez hello tooget hello nom d’hôte complet de commande suivante :

        ```bash
        hostname -f
        ```

        Cette commande retourne un toohello similaire valeur suivant le nom d’hôte :

            hn0-myhdi-nfebtpfdv1nubcidphpap2eq2b.ex.internal.cloudapp.net

        Enregistrer la valeur hello retourné, qu’il est utilisé ultérieurement.

2. Dans votre navigateur, connectez-vous trop**http://HOSTNAME:8983/solr / #/**, où **nom d’hôte** est le nom hello déterminée dans les étapes précédentes hello.

    demande de Hello est routée via hello SSH tunnel toohello Solr interface utilisateur web sur votre cluster. Hello similaire toohello suivant l’image apparaît :

    ![Image du tableau de bord Solr.](./media/hdinsight-hadoop-solr-install-linux/solrdashboard.png)

3. À partir du volet de gauche hello, utilisez hello **Core sélecteur** tooselect de liste déroulante **collection1**. Plusieurs entrées doivent apparaître sous **collection1**.

4. À partir des entrées hello ci-dessous **collection1**, sélectionnez **requête**. Utilisez hello après la page de recherche de valeurs toopopulate hello :

   * Bonjour **q** texte, entrez  **\*:**\*. Cette requête renvoie tous les documents de hello sont indexés dans Solr. Si vous souhaitez toosearch une chaîne spécifique au sein de documents de hello, vous pouvez entrer ici cette chaîne.
   * Bonjour **wt** zone de texte, le format de sortie hello select. La valeur par défaut est **json**.

     Enfin, sélectionnez hello **exécuter la requête** bouton bas hello pate de recherche hello.

     ![Utilisez l’Action de Script toocustomize un cluster](./media/hdinsight-hadoop-solr-install-linux/hdi-solr-dashboard-query.png)

     sortie de Hello retourne hello deux documents que vous avez ajouté toohello index précédemment. Hello est similaire toohello suivant document JSON de sortie :

           "response": {
               "numFound": 2,
               "start": 0,
               "maxScore": 1,
               "docs": [
                 {
                   "id": "SOLR1000",
                   "name": "Solr, hello Enterprise Search Server",
                   "manu": "Apache Software Foundation",
                   "cat": [
                     "software",
                     "search"
                   ],
                   "features": [
                     "Advanced Full-Text Search Capabilities using Lucene",
                     "Optimized for High Volume Web Traffic",
                     "Standards Based Open Interfaces - XML and HTTP",
                     "Comprehensive HTML Administration Interfaces",
                     "Scalability - Efficient Replication tooother Solr Search Servers",
                     "Flexible and Adaptable with XML configuration and Schema",
                     "Good unicode support: héllo (hello with an accent over hello e)"
                   ],
                   "price": 0,
                   "price_c": "0,USD",
                   "popularity": 10,
                   "inStock": true,
                   "incubationdate_dt": "2006-01-17T00:00:00Z",
                   "_version_": 1486960636996878300
                 },
                 {
                   "id": "3007WFP",
                   "name": "Dell Widescreen UltraSharp 3007WFP",
                   "manu": "Dell, Inc.",
                   "manu_id_s": "dell",
                   "cat": [
                     "electronics and computer1"
                   ],
                   "features": [
                     "30\" TFT active matrix LCD, 2560 x 1600, .25mm dot pitch, 700:1 contrast"
                   ],
                   "includes": "USB cable",
                   "weight": 401.6,
                   "price": 2199,
                   "price_c": "2199,USD",
                   "popularity": 6,
                   "inStock": true,
                   "store": "43.17614,-90.57341",
                   "_version_": 1486960637584081000
                 }
               ]
             }

### <a name="starting-and-stopping-solr"></a>Démarrage et arrêt de Solr

Utilisez hello suivant les commandes toomanually arrêter et démarrer des Solr :

```bash
sudo stop solr
sudo start solr
```

## <a name="backup-indexed-data"></a>Sauvegarde de données indexées

Hello suivant tooback étapes Solr données toohello par défaut l’espace de stockage pour votre cluster, utilisez :

1. Se connecter cluster toohello à l’aide de SSH, puis utilisez hello suivant le nom d’hôte de commande tooget hello pour le nœud principal de hello :

    ```bash
    hostname -f
    ```

2. Utilisez hello suivant commande toocreate un instantané des données de hello indexé. Remplacez **nom d’hôte** avec nom hello retourné à partir de la commande précédente hello :

    ```bash
    curl http://HOSTNAME:8983/solr/replication?command=backup
    ```

    réponse de Hello est similaire toohello XML suivant :

        <?xml version="1.0" encoding="UTF-8"?>
        <response>
          <lst name="responseHeader">
            <int name="status">0</int>
            <int name="QTime">9</int>
          </lst>
          <str name="status">OK</str>
        </response>

3. Remplacez les répertoires`/usr/hdp/current/solr/example/solr`. Il y a ici un sous-répertoire pour chaque collection. Chaque répertoire de la collection contient un `data` répertoire qui contient l’instantané hello pour collection de hello.

4. toocreate une archive compressée du dossier de capture instantanée hello, hello utilisez commande suivante :

    ```bash
    tar -zcf snapshot.20150806185338855.tgz snapshot.20150806185338855
    ```

    Remplacez hello `snapshot.20150806185338855` nom hello d’instantané de hello pour votre collection de valeurs.

    Cette commande crée une archive nommée **snapshot.20150806185338855.tgz**, qui contient le contenu de hello Hello **snapshot.20150806185338855** active.

5. Vous pouvez ensuite stocker le stockage de principal du cluster toohello hello archive à l’aide de hello commande suivante :

    ```bash
    hdfs dfs -put snapshot.20150806185338855.tgz /example/data
    ```

Pour plus d’informations sur l’utilisation de sauvegardes et de restaurations Solr, consultez [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups).

## <a name="next-steps"></a>Étapes suivantes

* [Installation de Giraph sur des clusters HDInsight](hdinsight-hadoop-giraph-install-linux.md). Utilisez tooinstall de personnalisation de cluster que giraph sur HDInsight Hadoop de clusters. Giraph vous permet de graphique tooperform traitement à l’aide de Hadoop et peut être utilisé avec Azure HDInsight.

* [Installer Hue sur les clusters HDInsight](hdinsight-hadoop-hue-linux.md). Utilisez cluster personnalisation tooinstall teinte sur des clusters HDInsight Hadoop. La teinte représente qu'un ensemble d’applications Web utilisé toointeract avec un cluster Hadoop.

[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
