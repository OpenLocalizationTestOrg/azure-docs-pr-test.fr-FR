---
title: "détection d’intrusion réseau aaaPerform avec l’Observateur de réseau Azure et d’outils open source | Documents Microsoft"
description: "Cet article décrit comment toouse Observateur de réseau Azure et tooperform d’outils open source du réseau de détection des intrusions"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 0f043f08-19e1-4125-98b0-3e335ba69681
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b5a909b827ab32ad6b2fd8e2911a944fd940249e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="perform-network-intrusion-detection-with-network-watcher-and-open-source-tools"></a>Détecter les intrusions dans un réseau avec Azure Network Watcher et des outils open source

Les captures de paquets sont essentielles pour implémenter des systèmes de détection d’intrusions dans un réseau et surveiller la sécurité du réseau. Il existe plusieurs outils open source de systèmes de détection d’intrusions qui traitent des captures de paquets et recherchent les signatures des activités malveillantes et des intrusions dans un réseau éventuelles. À l’aide de captures de paquets hello fournies par l’Observateur réseau, vous pouvez analyser votre réseau pour des intrusions dangereuses ou les vulnérabilités.

Cet outil open source est Suricata, un moteur d’ID qui utilise des groupes de règles du trafic réseau toomonitor et déclenche des alertes quand des événements suspects se produisent. Suricata propose un moteur multithread, ce qui signifie qu’il peut effectuer une analyse du trafic réseau de manière plus rapide et plus efficace. Pour plus d’informations sur Suricata et ses fonctionnalités, rendez-vous sur le site web correspondant : https://suricata-ids.org/.

## <a name="scenario"></a>Scénario

Cet article explique comment tooset des tooperform de votre environnement réseau à l’aide de l’Observateur réseau, Suricata, la détection d’intrusion et hello pile élastique. Observateur réseau fournit que des paquets de hello capture la détection d’intrusion réseau tooperform utilisé. Captures de paquets de Suricata processus hello et déclencher des alertes basées sur les paquets qui correspondent à son groupe de règles donné de menaces. Ces alertes sont stockées dans un fichier journal sur votre ordinateur local. À l’aide de hello pile élastique, les journaux de hello générés par Suricata peuvent être indexées et utilisé toocreate un tableau de bord Kibana, en vous fournissant une représentation visuelle des journaux de hello et une vulnérabilité de moyens tooquickly gain insights toopotential réseau.  

![scénario d’application web simple][1]

Les deux outils open source peuvent être configurés sur une machine virtuelle Azure, ce qui vous tooperform cette analyse dans votre environnement réseau Azure.

## <a name="steps"></a>Étapes

### <a name="install-suricata"></a>Installer Suricata

Pour toutes les autres méthodes d’installation, rendez-vous sur http://suricata.readthedocs.io/en/latest/install.html.

1. Dans un terminal de ligne de commande de votre machine virtuelle hello exécutez hello suivant de commandes :

    ```
    sudo add-apt-repository ppa:oisf/suricata-stable
    sudo apt-get update
    sudo sudo apt-get install suricata
    ```

1. tooverify votre installation, exécutez la commande hello `suricata -h` toosee hello la liste complète des commandes.

### <a name="download-hello-emerging-threats-ruleset"></a>Télécharger hello émergentes de menaces ruleset

À ce stade, nous avons des règles pour Suricata toorun. Vous pouvez créer vos propres règles si il n’y réseau tooyour de menaces spécifiques vous aimeriez toodetect, ou vous pouvez également utiliser développé des ensembles de règles à partir d’un nombre de fournisseurs, tels que les menaces émergentes ou règles VRT Snort. Nous utilisons ici hello librement accessibles émergentes de menaces ruleset :

Télécharger l’ensemble de règles hello et copiez-les dans le répertoire de hello :

```
wget http://rules.emergingthreats.net/open/suricata/emerging.rules.tar.gz
tar zxf emerging.rules.tar.gz
sudo cp -r rules /etc/suricata/
```

### <a name="process-packet-captures-with-suricata"></a>Traiter les captures de paquets avec Suricata

paquet de tooprocess capture à l’aide de Suricata, exécutez hello de commande suivante :

```
sudo suricata -c /etc/suricata/suricata.yaml -r <location_of_pcapfile>
```
toocheck hello résultant d’alertes, de lire le fichier de fast.log hello :
```
tail -f /var/log/suricata/fast.log
```

### <a name="set-up-hello-elastic-stack"></a>Configurer hello pile élastique

Alors que les journaux de hello Suricata produit contiennent des informations importantes sur ce qui se passe sur votre réseau, ces fichiers journaux ne sont pas tooread plus simple de hello et comprennent. En vous connectant à Suricata avec hello pile élastique, nous pouvons créer un tableau de bord Kibana qui nous permet de toosearch, graphique, analyser et dégager de nos journaux.

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
1. Ensuite, nous devons tooread de Logstash tooconfigure à partir de la sortie hello du fichier de eve.json. Créez un fichier logstash.conf à l’aide de :

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. Ajouter hello contenu toohello le fichier suivant (Assurez-vous que ce fichier de eve.json toohello hello chemin d’accès est correct) :

    ```ruby
    input {
    file {
        path => ["/var/log/suricata/eve.json"]
        codec =>  "json"
        type => "SuricataIDPS"
    }

    }

    filter {
    if [type] == "SuricataIDPS" {
        date {
        match => [ "timestamp", "ISO8601" ]
        }
        ruby {
        code => "
            if event.get('[event_type]') == 'fileinfo'
            event.set('[fileinfo][type]', event.get('[fileinfo][magic]').to_s.split(',')[0])
            end
        "
        }

        ruby{
        code => "
            if event.get('[event_type]') == 'alert'
            sp = event.get('[alert][signature]').to_s.split(' group ')
            if (sp.length == 2) and /\A\d+\z/.match(sp[1])
                event.set('[alert][signature]', sp[0])
            end
            end
            "
        }
    }

    if [src_ip]  {
        geoip {
        source => "src_ip"
        target => "geoip"
        #database => "/opt/logstash/vendor/geoip/GeoLiteCity.dat"
        add_field => [ "[geoip][coordinates]", "%{[geoip][longitude]}" ]
        add_field => [ "[geoip][coordinates]", "%{[geoip][latitude]}"  ]
        }
        mutate {
        convert => [ "[geoip][coordinates]", "float" ]
        }
        if ![geoip.ip] {
        if [dest_ip]  {
            geoip {
            source => "dest_ip"
            target => "geoip"
            #database => "/opt/logstash/vendor/geoip/GeoLiteCity.dat"
            add_field => [ "[geoip][coordinates]", "%{[geoip][longitude]}" ]
            add_field => [ "[geoip][coordinates]", "%{[geoip][latitude]}"  ]
            }
            mutate {
            convert => [ "[geoip][coordinates]", "float" ]
            }
        }
        }
    }
    }

    output {
    elasticsearch {
        hosts => "localhost"
    }
    }
    ```

1. Vérifiez que toogive hello autorisations correctes toohello eve.json le fichier afin que Logstash peuvent traiter des fichiers de hello.
    
    ```
    sudo chmod 775 /var/log/suricata/eve.json
    ```

1. toostart Logstash, exécutez la commande hello :

    ```
    sudo /etc/init.d/logstash start
    ```

Pour obtenir des instructions sur l’installation de Logstash, consultez toohello [documentation officielle](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)

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
1. Pour ce scénario, hello index pour hello Suricata journaux consiste « logstash-* »

1. Si vous souhaitez Kibana du tableau de bord hello tooview à distance, créez une règle entrante de groupe de sécurité réseau autorisant l’accès trop**port 5601**.

### <a name="create-a-kibana-dashboard"></a>Créer un tableau de bord Kibana

Pour cet article, nous avons fourni un tableau de bord test vous tooview tendances et les détails de vos alertes.

1. Téléchargez le fichier du tableau de bord hello [ici](https://aka.ms/networkwatchersuricatadashboard), fichier de visualisation hello [ici](https://aka.ms/networkwatchersuricatavisualization)et le fichier de recherche hello enregistré [ici](https://aka.ms/networkwatchersuricatasavedsearch).

1. Sous hello **gestion** onglet naviguer trop de Kibana,**objets enregistrés** et importer les trois fichiers. Puis, à partir de hello **tableau de bord** onglet, vous pouvez ouvrir et charge de tableau de bord exemple hello.

Vous avez également la possibilité de créer vos propres visualisations et tableaux de bord en fonction des mesures qui vous intéressent. Reportez-vous à la [documentation officielle](https://www.elastic.co/guide/en/kibana/current/visualize.html) de Kibana pour en savoir plus sur la création de visualisations Kibana.

![tableau de bord Kibana][2]

### <a name="visualize-ids-alert-logs"></a>Visualiser les journaux d’alertes de système de détection d’intrusions

tableau de bord exemple Hello fournit plusieurs visualisations de journaux d’alertes hello Suricata :

1. Alertes par GeoIP – une carte montrant les distribution hello des alertes par leur pays d’origine en fonction de l’emplacement géographique (déterminé par IP)

    ![geo ip][3]

1. Top 10 alertes – un résumé des alertes de hello 10 plus fréquents déclenchée et leur description. En cliquant sur une alerte individuelle filtre vers le bas hello du tableau de bord toohello informations toothat alerte en question.

    ![image 4][4]

1. Nombre d’alertes : hello le nombre total d’alertes déclenchées par le groupe de règles hello

    ![image 5][5]

1. 20 premiers Source ou la Destination des adresses IP/Ports - graphiques à secteurs montrant hello top 20 adresses IP et ports alertes ont été déclenchées sur. Vous pouvez filtrer vers le bas sur toosee d’adresses IP/ports spécifique le nombre et le type d’alerte soit déclenchée.

    ![image 6][6]

1. Résumé des alertes : un tableau récapitulant les spécificités de chaque alerte. Vous pouvez personnaliser ce tooshow de table autres paramètres d’intérêt pour chaque alerte.

    ![image 7][7]

Pour plus d’informations sur la création de tableaux de bord et de visualisations personnalisés, consultez la [documentation officielle de Kibana](https://www.elastic.co/guide/en/kibana/current/introduction.html).

## <a name="conclusion"></a>Conclusion

L’association des captures de paquets fournies par Network Watcher et des outils open source de système de détection d’intrusions tels que Suricata vous permet de détecter les intrusions dans un réseau pour un large éventail de menaces. Ces tableaux de bord permettre de vous tooquickly identifier les tendances et les anomalies dans votre réseau, et explorez hello données toodiscover causes principales des alertes, telles que les agents utilisateurs malveillants ou des ports vulnérables. Avec ces données extraites, vous pouvez prendre des décisions éclairées sur comment tooreact tooand protéger votre réseau à partir de toute tentative d’intrusion dangereux et créer des règles tooprevent intrusions futures tooyour réseau.

## <a name="next-steps"></a>Étapes suivantes

Découvrez comment tootrigger paquet capture en fonction des alertes en vous rendant sur [utiliser l’analyse du réseau proactive toodo paquet capture avec les fonctions de Azure](network-watcher-alert-triggered-packet-capture.md)

Découvrez comment toovisualize votre flux de groupe de sécurité réseau se connecte à Power BI en vous rendant sur [NSG de visualiser les flux de journaux avec Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)



<!-- images -->
[1]: ./media/network-watcher-intrusion-detection-open-source-tools/figure1.png
[2]: ./media/network-watcher-intrusion-detection-open-source-tools/figure2.png
[3]: ./media/network-watcher-intrusion-detection-open-source-tools/figure3.png
[4]: ./media/network-watcher-intrusion-detection-open-source-tools/figure4.png
[5]: ./media/network-watcher-intrusion-detection-open-source-tools/figure5.png
[6]: ./media/network-watcher-intrusion-detection-open-source-tools/figure6.png
[7]: ./media/network-watcher-intrusion-detection-open-source-tools/figure7.png
