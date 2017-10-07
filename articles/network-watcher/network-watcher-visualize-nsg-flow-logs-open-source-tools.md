---
title: "aaaVisualize les flux NSG de l’Observateur réseau Azure se connecte à l’aide d’outils open source | Documents Microsoft"
description: "Cette page décrit le mode d’ouverture des journaux de flux source outils toovisualize NSG toouse."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e9b2dcad-4da4-4d6b-aee2-6d0afade0cb8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 47cb529d4a1e00e8c4c0fa6885cbf72aed3e74c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-azure-network-watcher-nsg-flow-logs-using-open-source-tools"></a>Visualiser les journaux de flux NSG d’Azure Network Watcher à l’aide d’outils open source

Les journaux des flux de groupe de sécurité réseau fournissent des informations permettant de comprendre le trafic IP entrant et sortant sur les groupes de sécurité réseau. Ces journaux flux affiche sortant et les flux entrants sur une base par la règle, hello flux hello de carte réseau s’applique, 5 tuple plus d’informations sur le flux hello (Source/Destination IP, Port de la Source et de Destination, protocole), et si le trafic de hello a été autorisé ou refusé.

Ces journaux de flux peut être difficile toomanually analyse et obtenir des informations détaillées. Toutefois, il existe de nombreux outils open source qui peuvent aider à visualiser ces données. Cet article fournit une solution toovisualize ces journaux à l’aide de hello pile élastique, qui vous tooquickly index et de visualiser vos journaux de flux dans un tableau de bord Kibana.

## <a name="scenario"></a>Scénario

Dans cet article, nous allons définir une solution qui vous permettra de journaux de flux de groupe de sécurité réseau toovisualize à l’aide de hello pile élastique.  Un plug-in d’entrée Logstash obtiendra les journaux de flux hello directement à partir de l’objet blob de stockage hello configuré pour contenant les journaux de flux hello. Ensuite, les journaux de flux de hello à l’aide de hello pile élastique, seront indexés et utilisé toocreate un Kibana du tableau de bord toovisualize hello des informations.

![scénario][scenario]

## <a name="steps"></a>Étapes

### <a name="enable-network-security-group-flow-logging"></a>Activer les journaux des flux de groupe de sécurité réseau
Pour ce scénario, la journalisation des flux de groupe de sécurité réseau doit être activée sur au moins un groupe de sécurité réseau dans votre compte. Pour obtenir des instructions sur l’activation des journaux de sécurité de flux de réseau, consultez toohello l’article suivant [journalisation tooflow de présentation pour les groupes de sécurité réseau](network-watcher-nsg-flow-logging-overview.md).


### <a name="set-up-hello-elastic-stack"></a>Configurer hello pile élastique
En connectant le groupe de sécurité réseau de flux de journaux avec hello pile élastique, nous pouvons créer un tableau de bord Kibana qui nous permet de toosearch, graphique, analyser et dégager de nos journaux.

#### <a name="install-elasticsearch"></a>Installer Elasticsearch

1. Hello pile élastique de la version 5.0 et versions ultérieures nécessite Java 8. Exécutez la commande hello `java -version` toocheck votre version. Si vous n’avez pas java installation, consultez toodocumentation sur [site Web d’Oracle](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)
1. Téléchargez hello binaire package pour votre système :

    ```
    curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.2.0.deb
    sudo dpkg -i elasticsearch-5.2.0.deb
    sudo /etc/init.d/elasticsearch start
    ```

    D’autres méthodes d’installation se trouvent sur la page [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html) (Installation d’Elasticsearch).

1. Vérifiez que Elasticsearch est en cours d’exécution avec la commande hello :

    ```
    curl http://127.0.0.1:9200
    ```

    Vous devez voir un toothis similaire de réponse :

    ```
    {
    "name" : "Angela Del Toro",
    "cluster_name" : "elasticsearch",
    "version" : {
        "number" : "5.2.0",
        "build_hash" : "8ff36d139e16f8720f2947ef62c8167a888992fe",
        "build_timestamp" : "2016-01-27T13:32:39Z",
        "build_snapshot" : false,
        "lucene_version" : "6.1.0"
    },
    "tagline" : "You Know, for Search"
    }
    ```

Pour plus d’informations sur la recherche élastique lors de l’installation, consultez toohello page [Installation](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)

### <a name="install-logstash"></a>Installer Logstash

1. tooinstall Logstash hello suivant de commandes, exécutez :

    ```
    curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.2.0.deb
    sudo dpkg -i logstash-5.2.0.deb
    ```
1. Ensuite, nous devez tooconfigure Logstash tooaccess et analyse les journaux de flux hello. Créez un fichier logstash.conf à l’aide de :

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. Ajoutez hello contenu toohello le fichier suivant :

  ```
    input {
      azureblob
        {
            storage_account_name => "mystorageaccount"
            storage_access_key => "storageaccesskey"
            container => "nsgflowlogContainerName"
            codec => "json"
        }
      }

      filter {
        split { field => "[records]" }
        split { field => "[records][properties][flows]"}
        split { field => "[records][properties][flows][flows]"}
        split { field => "[records][properties][flows][flows][flowTuples]"}

     mutate{
      split => { "[records][resourceId]" => "/"}
      add_field => {"Subscription" => "%{[records][resourceId][2]}"
                    "ResourceGroup" => "%{[records][resourceId][4]}"
                    "NetworkSecurityGroup" => "%{[records][resourceId][8]}"}
      convert => {"Subscription" => "string"}
      convert => {"ResourceGroup" => "string"}
      convert => {"NetworkSecurityGroup" => "string"}
      split => { "[records][properties][flows][flows][flowTuples]" => ","}
      add_field => {
                  "unixtimestamp" => "%{[records][properties][flows][flows][flowTuples][0]}"
                  "srcIp" => "%{[records][properties][flows][flows][flowTuples][1]}"
                  "destIp" => "%{[records][properties][flows][flows][flowTuples][2]}"
                  "srcPort" => "%{[records][properties][flows][flows][flowTuples][3]}"
                  "destPort" => "%{[records][properties][flows][flows][flowTuples][4]}"
                  "protocol" => "%{[records][properties][flows][flows][flowTuples][5]}"
                  "trafficflow" => "%{[records][properties][flows][flows][flowTuples][6]}"
                  "traffic" => "%{[records][properties][flows][flows][flowTuples][7]}"
                   }
      convert => {"unixtimestamp" => "integer"}
      convert => {"srcPort" => "integer"}
      convert => {"destPort" => "integer"}        
     }

     date{
       match => ["unixtimestamp" , "UNIX"]
     }
    }

    output {
      stdout { codec => rubydebug }
      elasticsearch {
        hosts => "localhost"
        index => "nsg-flow-logs"
      }
    }  

  ```

Pour obtenir des instructions sur l’installation de Logstash, consultez toohello [documentation officielle](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)

### <a name="install-hello-logstash-input-plugin-for-azure-blob-storage"></a>Installer le plug-in hello Logstash d’entrée pour le stockage d’objets blob Azure

Ce plug-in Logstash vous permettra de journaux de flux hello toodirectly accès à partir de leur compte de stockage désignées. tooinstall ce plug-in, à partir du répertoire d’installation Logstash hello par défaut (dans ce cas /usr/share/logstash/bin) exécutez hello commande :

```
logstash-plugin install logstash-input-azureblob
```

toostart Logstash, exécutez la commande hello :

```
sudo /etc/init.d/logstash start
```

Pour plus d’informations sur ce plug-in, consultez toodocumentation [ici](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob)

### <a name="install-kibana"></a>Installer Kibana

1. Exécutez hello suivant de commandes tooinstall Kibana :

  ```
  curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-5.2.0-linux-x86_64.tar.gz
  tar xzvf kibana-5.2.0-linux-x86_64.tar.gz
  ```

1. toorun Kibana utiliser les commandes hello :

  ```
  cd kibana-5.2.0-linux-x86_64/
  ./bin/kibana
  ```

1. tooview votre site web Kibana interface, accédez trop`http://localhost:5601`
1. Pour ce scénario, hello index pour les journaux de flux hello consiste « groupe de sécurité réseau-flux de journaux ». Vous pouvez modifier le modèle d’index hello dans la section de « sortie » hello de votre fichier logstash.conf.

1. Si vous souhaitez Kibana du tableau de bord hello tooview à distance, créez une règle entrante de groupe de sécurité réseau autorisant l’accès trop**port 5601**.

### <a name="create-a-kibana-dashboard"></a>Créer un tableau de bord Kibana

Pour cet article, nous avons fourni un tableau de bord test vous tooview tendances et les détails de vos alertes.

![figure 1][1]

1. Téléchargez le fichier du tableau de bord hello [ici](https://aka.ms/networkwatchernsgflowlogdashboard), fichier de visualisation hello [ici](https://aka.ms/networkwatchernsgflowlogvisualizations)et le fichier de recherche hello enregistré [ici](https://aka.ms/networkwatchernsgflowlogsearch).

1. Sous hello **gestion** onglet naviguer trop de Kibana,**objets enregistrés** et importer les trois fichiers. Puis, à partir de hello **tableau de bord** onglet, vous pouvez ouvrir et charge de tableau de bord exemple hello.

Vous avez également la possibilité de créer vos propres visualisations et tableaux de bord en fonction des mesures qui vous intéressent. Reportez-vous à la [documentation officielle](https://www.elastic.co/guide/en/kibana/current/visualize.html) de Kibana pour en savoir plus sur la création de visualisation Kibana.

### <a name="visualize-nsg-flow-logs"></a>Visualiser les journaux de flux NSG

tableau de bord exemple Hello fournit plusieurs visualisations des journaux de flux hello :

1. Flux à la décision ou de sens dans le temps - graphiques série montrant le numéro de hello de flux sur hello laps de temps en temps. Vous pouvez modifier l’étendue de ces deux visualisations et unité hello de temps. Flux en proportion de hello montre la décision d’autoriser ou refuser des décisions lors de flux en Direction affiche hello proportion de trafic entrant et sortant. Grâce à ces éléments visuels, vous pouvez examiner les tendances du trafic au fil du temps et identifier les pics ou les modèles inhabituels.

  ![figure 2][2]

1. Flux par le Port de Destination/Source : graphiques en secteurs montrant les ports respectifs de tootheir de répartition hello de flux. Grâce à cette vue, vous pouvez visualiser les ports les plus fréquemment utilisés. Si vous cliquez sur un port spécifique dans un graphique à secteurs de hello, reste hello du tableau de bord hello filtre vers le bas tooflows de ce port.

  ![figure 3][3]

1. Nombre de flux et le plus ancien journal ponctualité – vous montrant numéro hello de flux enregistré et date hello du journal plus ancien de hello capturées.

  ![figure 4][4]

1. Flux par groupe de sécurité réseau et de la règle : un graphique à barres affiche la distribution hello de flux au sein de chaque groupe de sécurité réseau, ainsi que la distribution hello de règles au sein de chaque groupe de sécurité réseau. À ce stade, vous pouvez voir le groupe de sécurité réseau et les règles générées hello plus de trafic.

  ![figure 5][5]

1. 10 principaux Source ou la Destination des adresses IP – graphiques à barres en affichant la source des 10 premiers hello et les adresses IP de destination. Vous pouvez ajuster ces tooshow graphiques plus ou moins premières adresses IP. À partir d’ici vous pouvez voir hello qui se produisent généralement des adresses IP ainsi que hello décision de trafic (autorisation ou refus) effectuée vers chaque adresse IP.

  ![figure 6][6]

1. Flux Tuples – ce tableau montre hello les informations contenues dans chaque tuple du flux, ainsi que ses NGS correspondante et la règle.

  ![figure 7][7]

À l’aide de barre de requête hello haut hello du tableau de bord hello, vous pouvez filtrer vers le bas du tableau de bord hello selon n’importe quel paramètre de flux hello, telles que l’ID d’abonnement, groupes de ressources, règle ou toute autre variable dignes d’intérêt. Pour plus d’informations sur les requêtes et les filtres de Kibana, consultez toohello [documentation officielle](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html)

## <a name="conclusion"></a>Conclusion

En combinant les journaux de flux de groupe de sécurité réseau hello avec hello pile élastique, nous avons élaborer moyen puissant et personnalisable toovisualize notre le trafic réseau. Ces tableaux de bord vous tooquickly gain et partage les informations relatives à votre trafic réseau, ainsi que les filtre vers le bas et examiner sur toute manipulation d’éventuelles anomalies. À l’aide de Kibana, vous pouvez personnaliser ces tableaux de bord et créer des visualisations spécifique toomeet les besoins de sécurité, d’audit et de conformité.

## <a name="next-steps"></a>Étapes suivantes

Découvrez comment toovisualize votre flux de groupe de sécurité réseau se connecte à Power BI en vous rendant sur [NSG de visualiser les flux de journaux avec Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)


<!--Image references-->

[scenario]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/scenario.png
[1]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure7.png
