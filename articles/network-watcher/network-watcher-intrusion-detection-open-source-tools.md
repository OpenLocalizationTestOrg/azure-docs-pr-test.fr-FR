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
# <a name="perform-network-intrusion-detection-with-network-watcher-and-open-source-tools"></a><span data-ttu-id="93951-103">Détecter les intrusions dans un réseau avec Azure Network Watcher et des outils open source</span><span class="sxs-lookup"><span data-stu-id="93951-103">Perform network intrusion detection with Network Watcher and open source tools</span></span>

<span data-ttu-id="93951-104">Les captures de paquets sont essentielles pour implémenter des systèmes de détection d’intrusions dans un réseau et surveiller la sécurité du réseau.</span><span class="sxs-lookup"><span data-stu-id="93951-104">Packet captures are a key component for implementing network intrusion detection systems (IDS) and performing Network Security Monitoring (NSM).</span></span> <span data-ttu-id="93951-105">Il existe plusieurs outils open source de systèmes de détection d’intrusions qui traitent des captures de paquets et recherchent les signatures des activités malveillantes et des intrusions dans un réseau éventuelles.</span><span class="sxs-lookup"><span data-stu-id="93951-105">There are several open source IDS tools that process packet captures and look for signatures of possible network intrusions and malicious activity.</span></span> <span data-ttu-id="93951-106">À l’aide de captures de paquets hello fournies par l’Observateur réseau, vous pouvez analyser votre réseau pour des intrusions dangereuses ou les vulnérabilités.</span><span class="sxs-lookup"><span data-stu-id="93951-106">Using hello packet captures provided by Network Watcher, you can analyze your network for any harmful intrusions or vulnerabilities.</span></span>

<span data-ttu-id="93951-107">Cet outil open source est Suricata, un moteur d’ID qui utilise des groupes de règles du trafic réseau toomonitor et déclenche des alertes quand des événements suspects se produisent.</span><span class="sxs-lookup"><span data-stu-id="93951-107">One such open source tool is Suricata, an IDS engine that uses rulesets toomonitor network traffic and triggers alerts whenever suspicious events occur.</span></span> <span data-ttu-id="93951-108">Suricata propose un moteur multithread, ce qui signifie qu’il peut effectuer une analyse du trafic réseau de manière plus rapide et plus efficace.</span><span class="sxs-lookup"><span data-stu-id="93951-108">Suricata offers a multi-threaded engine, meaning it can perform network traffic analysis with increased speed and efficiency.</span></span> <span data-ttu-id="93951-109">Pour plus d’informations sur Suricata et ses fonctionnalités, rendez-vous sur le site web correspondant : https://suricata-ids.org/.</span><span class="sxs-lookup"><span data-stu-id="93951-109">For more details about Suricata and its capabilities, visit their website at https://suricata-ids.org/.</span></span>

## <a name="scenario"></a><span data-ttu-id="93951-110">Scénario</span><span class="sxs-lookup"><span data-stu-id="93951-110">Scenario</span></span>

<span data-ttu-id="93951-111">Cet article explique comment tooset des tooperform de votre environnement réseau à l’aide de l’Observateur réseau, Suricata, la détection d’intrusion et hello pile élastique.</span><span class="sxs-lookup"><span data-stu-id="93951-111">This article explains how tooset up your environment tooperform network intrusion detection using Network Watcher, Suricata, and hello Elastic Stack.</span></span> <span data-ttu-id="93951-112">Observateur réseau fournit que des paquets de hello capture la détection d’intrusion réseau tooperform utilisé.</span><span class="sxs-lookup"><span data-stu-id="93951-112">Network Watcher provides you with hello packet captures used tooperform network intrusion detection.</span></span> <span data-ttu-id="93951-113">Captures de paquets de Suricata processus hello et déclencher des alertes basées sur les paquets qui correspondent à son groupe de règles donné de menaces.</span><span class="sxs-lookup"><span data-stu-id="93951-113">Suricata processes hello packet captures and trigger alerts based on packets that match its given ruleset of threats.</span></span> <span data-ttu-id="93951-114">Ces alertes sont stockées dans un fichier journal sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="93951-114">These alerts are stored in a log file on your local machine.</span></span> <span data-ttu-id="93951-115">À l’aide de hello pile élastique, les journaux de hello générés par Suricata peuvent être indexées et utilisé toocreate un tableau de bord Kibana, en vous fournissant une représentation visuelle des journaux de hello et une vulnérabilité de moyens tooquickly gain insights toopotential réseau.</span><span class="sxs-lookup"><span data-stu-id="93951-115">Using hello Elastic Stack, hello logs generated by Suricata can be indexed and used toocreate a Kibana dashboard, providing you with a visual representation of hello logs and a means tooquickly gain insights toopotential network vulnerabilities.</span></span>  

![scénario d’application web simple][1]

<span data-ttu-id="93951-117">Les deux outils open source peuvent être configurés sur une machine virtuelle Azure, ce qui vous tooperform cette analyse dans votre environnement réseau Azure.</span><span class="sxs-lookup"><span data-stu-id="93951-117">Both open source tools can be set up on an Azure VM, allowing you tooperform this analysis within your own Azure network environment.</span></span>

## <a name="steps"></a><span data-ttu-id="93951-118">Étapes</span><span class="sxs-lookup"><span data-stu-id="93951-118">Steps</span></span>

### <a name="install-suricata"></a><span data-ttu-id="93951-119">Installer Suricata</span><span class="sxs-lookup"><span data-stu-id="93951-119">Install Suricata</span></span>

<span data-ttu-id="93951-120">Pour toutes les autres méthodes d’installation, rendez-vous sur http://suricata.readthedocs.io/en/latest/install.html.</span><span class="sxs-lookup"><span data-stu-id="93951-120">For all other methods of installation, visit http://suricata.readthedocs.io/en/latest/install.html</span></span>

1. <span data-ttu-id="93951-121">Dans un terminal de ligne de commande de votre machine virtuelle hello exécutez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="93951-121">In hello command-line terminal of your VM run hello following commands:</span></span>

    ```
    sudo add-apt-repository ppa:oisf/suricata-stable
    sudo apt-get update
    sudo sudo apt-get install suricata
    ```

1. <span data-ttu-id="93951-122">tooverify votre installation, exécutez la commande hello `suricata -h` toosee hello la liste complète des commandes.</span><span class="sxs-lookup"><span data-stu-id="93951-122">tooverify your installation, run hello command `suricata -h` toosee hello full list of commands.</span></span>

### <a name="download-hello-emerging-threats-ruleset"></a><span data-ttu-id="93951-123">Télécharger hello émergentes de menaces ruleset</span><span class="sxs-lookup"><span data-stu-id="93951-123">Download hello Emerging Threats ruleset</span></span>

<span data-ttu-id="93951-124">À ce stade, nous avons des règles pour Suricata toorun.</span><span class="sxs-lookup"><span data-stu-id="93951-124">At this stage, we do not have any rules for Suricata toorun.</span></span> <span data-ttu-id="93951-125">Vous pouvez créer vos propres règles si il n’y réseau tooyour de menaces spécifiques vous aimeriez toodetect, ou vous pouvez également utiliser développé des ensembles de règles à partir d’un nombre de fournisseurs, tels que les menaces émergentes ou règles VRT Snort.</span><span class="sxs-lookup"><span data-stu-id="93951-125">You can create your own rules if there are specific threats tooyour network you would like toodetect, or you can also use developed rule sets from a number of providers, such as Emerging Threats, or VRT rules from Snort.</span></span> <span data-ttu-id="93951-126">Nous utilisons ici hello librement accessibles émergentes de menaces ruleset :</span><span class="sxs-lookup"><span data-stu-id="93951-126">We use hello freely accessible Emerging Threats ruleset here:</span></span>

<span data-ttu-id="93951-127">Télécharger l’ensemble de règles hello et copiez-les dans le répertoire de hello :</span><span class="sxs-lookup"><span data-stu-id="93951-127">Download hello rule set and copy them into hello directory:</span></span>

```
wget http://rules.emergingthreats.net/open/suricata/emerging.rules.tar.gz
tar zxf emerging.rules.tar.gz
sudo cp -r rules /etc/suricata/
```

### <a name="process-packet-captures-with-suricata"></a><span data-ttu-id="93951-128">Traiter les captures de paquets avec Suricata</span><span class="sxs-lookup"><span data-stu-id="93951-128">Process packet captures with Suricata</span></span>

<span data-ttu-id="93951-129">paquet de tooprocess capture à l’aide de Suricata, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="93951-129">tooprocess packet captures using Suricata, run hello following command:</span></span>

```
sudo suricata -c /etc/suricata/suricata.yaml -r <location_of_pcapfile>
```
<span data-ttu-id="93951-130">toocheck hello résultant d’alertes, de lire le fichier de fast.log hello :</span><span class="sxs-lookup"><span data-stu-id="93951-130">toocheck hello resulting alerts, read hello fast.log file:</span></span>
```
tail -f /var/log/suricata/fast.log
```

### <a name="set-up-hello-elastic-stack"></a><span data-ttu-id="93951-131">Configurer hello pile élastique</span><span class="sxs-lookup"><span data-stu-id="93951-131">Set up hello Elastic Stack</span></span>

<span data-ttu-id="93951-132">Alors que les journaux de hello Suricata produit contiennent des informations importantes sur ce qui se passe sur votre réseau, ces fichiers journaux ne sont pas tooread plus simple de hello et comprennent.</span><span class="sxs-lookup"><span data-stu-id="93951-132">While hello logs that Suricata produces contain valuable information about what’s happening on our network, these log files aren’t hello easiest tooread and understand.</span></span> <span data-ttu-id="93951-133">En vous connectant à Suricata avec hello pile élastique, nous pouvons créer un tableau de bord Kibana qui nous permet de toosearch, graphique, analyser et dégager de nos journaux.</span><span class="sxs-lookup"><span data-stu-id="93951-133">By connecting Suricata with hello Elastic Stack, we can create a Kibana dashboard what allows us toosearch, graph, analyze, and derive insights from our logs.</span></span>

#### <a name="install-elasticsearch"></a><span data-ttu-id="93951-134">Installer Elasticsearch</span><span class="sxs-lookup"><span data-stu-id="93951-134">Install Elasticsearch</span></span>

1. <span data-ttu-id="93951-135">Hello pile élastique de la version 5.0 et versions ultérieures nécessite Java 8.</span><span class="sxs-lookup"><span data-stu-id="93951-135">hello Elastic Stack from version 5.0 and above requires Java 8.</span></span> <span data-ttu-id="93951-136">Exécutez la commande hello `java -version` toocheck votre version.</span><span class="sxs-lookup"><span data-stu-id="93951-136">Run hello command `java -version` toocheck your version.</span></span> <span data-ttu-id="93951-137">Si vous n’avez pas java installation, consultez toodocumentation sur [site Web d’Oracle](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span><span class="sxs-lookup"><span data-stu-id="93951-137">If you do not have java install, refer toodocumentation on [Oracle's website](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span></span>
1. <span data-ttu-id="93951-138">Téléchargez hello binaire package pour votre système :</span><span class="sxs-lookup"><span data-stu-id="93951-138">Download hello correct binary package for your system:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.2.0.deb
    sudo dpkg -i elasticsearch-5.2.0.deb
    sudo /etc/init.d/elasticsearch start
    ```

    <span data-ttu-id="93951-139">D’autres méthodes d’installation se trouvent sur la page [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html) (Installation d’Elasticsearch).</span><span class="sxs-lookup"><span data-stu-id="93951-139">Other installation methods can be found at [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)</span></span>

1. <span data-ttu-id="93951-140">Vérifiez que Elasticsearch est en cours d’exécution avec la commande hello :</span><span class="sxs-lookup"><span data-stu-id="93951-140">Verify that Elasticsearch is running with hello command:</span></span>

    ```
    curl http://127.0.0.1:9200
    ```

    <span data-ttu-id="93951-141">Vous devez voir un toothis similaire de réponse :</span><span class="sxs-lookup"><span data-stu-id="93951-141">You should see a response similar toothis:</span></span>

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

<span data-ttu-id="93951-142">Pour plus d’informations sur la recherche élastique lors de l’installation, consultez toohello page [Installation](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span><span class="sxs-lookup"><span data-stu-id="93951-142">For further instructions on installing Elastic search, refer toohello page [Installation](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span></span>

### <a name="install-logstash"></a><span data-ttu-id="93951-143">Installer Logstash</span><span class="sxs-lookup"><span data-stu-id="93951-143">Install Logstash</span></span>

1. <span data-ttu-id="93951-144">tooinstall Logstash hello suivant de commandes, exécutez :</span><span class="sxs-lookup"><span data-stu-id="93951-144">tooinstall Logstash run hello following commands:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.2.0.deb
    sudo dpkg -i logstash-5.2.0.deb
    ```
1. <span data-ttu-id="93951-145">Ensuite, nous devons tooread de Logstash tooconfigure à partir de la sortie hello du fichier de eve.json.</span><span class="sxs-lookup"><span data-stu-id="93951-145">Next we need tooconfigure Logstash tooread from hello output of eve.json file.</span></span> <span data-ttu-id="93951-146">Créez un fichier logstash.conf à l’aide de :</span><span class="sxs-lookup"><span data-stu-id="93951-146">Create a logstash.conf file using:</span></span>

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. <span data-ttu-id="93951-147">Ajouter hello contenu toohello le fichier suivant (Assurez-vous que ce fichier de eve.json toohello hello chemin d’accès est correct) :</span><span class="sxs-lookup"><span data-stu-id="93951-147">Add hello following content toohello file (make sure that hello path toohello eve.json file is correct):</span></span>

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

1. <span data-ttu-id="93951-148">Vérifiez que toogive hello autorisations correctes toohello eve.json le fichier afin que Logstash peuvent traiter des fichiers de hello.</span><span class="sxs-lookup"><span data-stu-id="93951-148">Make sure toogive hello correct permissions toohello eve.json file so that Logstash can ingest hello file.</span></span>
    
    ```
    sudo chmod 775 /var/log/suricata/eve.json
    ```

1. <span data-ttu-id="93951-149">toostart Logstash, exécutez la commande hello :</span><span class="sxs-lookup"><span data-stu-id="93951-149">toostart Logstash run hello command:</span></span>

    ```
    sudo /etc/init.d/logstash start
    ```

<span data-ttu-id="93951-150">Pour obtenir des instructions sur l’installation de Logstash, consultez toohello [documentation officielle](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span><span class="sxs-lookup"><span data-stu-id="93951-150">For further instructions on installing Logstash, refer toohello [official documentation](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span></span>

### <a name="install-kibana"></a><span data-ttu-id="93951-151">Installer Kibana</span><span class="sxs-lookup"><span data-stu-id="93951-151">Install Kibana</span></span>

1. <span data-ttu-id="93951-152">Exécutez hello suivant de commandes tooinstall Kibana :</span><span class="sxs-lookup"><span data-stu-id="93951-152">Run hello following commands tooinstall Kibana:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-5.2.0-linux-x86_64.tar.gz
    tar xzvf kibana-5.2.0-linux-x86_64.tar.gz

    ```
1. <span data-ttu-id="93951-153">toorun Kibana utiliser les commandes hello :</span><span class="sxs-lookup"><span data-stu-id="93951-153">toorun Kibana use hello commands:</span></span>

    ```
    cd kibana-5.2.0-linux-x86_64/
    ./bin/kibana
    ```

1. <span data-ttu-id="93951-154">tooview votre site web Kibana interface, accédez trop`http://localhost:5601`</span><span class="sxs-lookup"><span data-stu-id="93951-154">tooview your Kibana web interface, navigate too`http://localhost:5601`</span></span>
1. <span data-ttu-id="93951-155">Pour ce scénario, hello index pour hello Suricata journaux consiste « logstash-* »</span><span class="sxs-lookup"><span data-stu-id="93951-155">For this scenario, hello index pattern used for hello Suricata logs is "logstash-*"</span></span>

1. <span data-ttu-id="93951-156">Si vous souhaitez Kibana du tableau de bord hello tooview à distance, créez une règle entrante de groupe de sécurité réseau autorisant l’accès trop**port 5601**.</span><span class="sxs-lookup"><span data-stu-id="93951-156">If you want tooview hello Kibana dashboard remotely, create an inbound NSG rule allowing access too**port 5601**.</span></span>

### <a name="create-a-kibana-dashboard"></a><span data-ttu-id="93951-157">Créer un tableau de bord Kibana</span><span class="sxs-lookup"><span data-stu-id="93951-157">Create a Kibana dashboard</span></span>

<span data-ttu-id="93951-158">Pour cet article, nous avons fourni un tableau de bord test vous tooview tendances et les détails de vos alertes.</span><span class="sxs-lookup"><span data-stu-id="93951-158">For this article, we have provided a sample dashboard for you tooview trends and details in your alerts.</span></span>

1. <span data-ttu-id="93951-159">Téléchargez le fichier du tableau de bord hello [ici](https://aka.ms/networkwatchersuricatadashboard), fichier de visualisation hello [ici](https://aka.ms/networkwatchersuricatavisualization)et le fichier de recherche hello enregistré [ici](https://aka.ms/networkwatchersuricatasavedsearch).</span><span class="sxs-lookup"><span data-stu-id="93951-159">Download hello dashboard file [here](https://aka.ms/networkwatchersuricatadashboard), hello visualization file [here](https://aka.ms/networkwatchersuricatavisualization), and hello saved search file [here](https://aka.ms/networkwatchersuricatasavedsearch).</span></span>

1. <span data-ttu-id="93951-160">Sous hello **gestion** onglet naviguer trop de Kibana,**objets enregistrés** et importer les trois fichiers.</span><span class="sxs-lookup"><span data-stu-id="93951-160">Under hello **Management** tab of Kibana, navigate too**Saved Objects** and import all three files.</span></span> <span data-ttu-id="93951-161">Puis, à partir de hello **tableau de bord** onglet, vous pouvez ouvrir et charge de tableau de bord exemple hello.</span><span class="sxs-lookup"><span data-stu-id="93951-161">Then from hello **Dashboard** tab you can open and load hello sample dashboard.</span></span>

<span data-ttu-id="93951-162">Vous avez également la possibilité de créer vos propres visualisations et tableaux de bord en fonction des mesures qui vous intéressent.</span><span class="sxs-lookup"><span data-stu-id="93951-162">You can also create your own visualizations and dashboards tailored towards metrics of your own interest.</span></span> <span data-ttu-id="93951-163">Reportez-vous à la [documentation officielle](https://www.elastic.co/guide/en/kibana/current/visualize.html) de Kibana pour en savoir plus sur la création de visualisations Kibana.</span><span class="sxs-lookup"><span data-stu-id="93951-163">Read more about creating Kibana visualizations from Kibana's [official documentation](https://www.elastic.co/guide/en/kibana/current/visualize.html).</span></span>

![tableau de bord Kibana][2]

### <a name="visualize-ids-alert-logs"></a><span data-ttu-id="93951-165">Visualiser les journaux d’alertes de système de détection d’intrusions</span><span class="sxs-lookup"><span data-stu-id="93951-165">Visualize IDS alert logs</span></span>

<span data-ttu-id="93951-166">tableau de bord exemple Hello fournit plusieurs visualisations de journaux d’alertes hello Suricata :</span><span class="sxs-lookup"><span data-stu-id="93951-166">hello sample dashboard provides several visualizations of hello Suricata alert logs:</span></span>

1. <span data-ttu-id="93951-167">Alertes par GeoIP – une carte montrant les distribution hello des alertes par leur pays d’origine en fonction de l’emplacement géographique (déterminé par IP)</span><span class="sxs-lookup"><span data-stu-id="93951-167">Alerts by GeoIP – a map showing hello distribution of alerts by their country of origin based on geographic location (determined by IP)</span></span>

    ![geo ip][3]

1. <span data-ttu-id="93951-169">Top 10 alertes – un résumé des alertes de hello 10 plus fréquents déclenchée et leur description.</span><span class="sxs-lookup"><span data-stu-id="93951-169">Top 10 Alerts – a summary of hello 10 most frequent triggered alerts and their description.</span></span> <span data-ttu-id="93951-170">En cliquant sur une alerte individuelle filtre vers le bas hello du tableau de bord toohello informations toothat alerte en question.</span><span class="sxs-lookup"><span data-stu-id="93951-170">Clicking an individual alert filters down hello dashboard toohello information pertaining toothat specific alert.</span></span>

    ![image 4][4]

1. <span data-ttu-id="93951-172">Nombre d’alertes : hello le nombre total d’alertes déclenchées par le groupe de règles hello</span><span class="sxs-lookup"><span data-stu-id="93951-172">Number of Alerts – hello total count of alerts triggered by hello ruleset</span></span>

    ![image 5][5]

1. <span data-ttu-id="93951-174">20 premiers Source ou la Destination des adresses IP/Ports - graphiques à secteurs montrant hello top 20 adresses IP et ports alertes ont été déclenchées sur.</span><span class="sxs-lookup"><span data-stu-id="93951-174">Top 20 Source/Destination IPs/Ports - pie charts showing hello top 20 IPs and ports that alerts were triggered on.</span></span> <span data-ttu-id="93951-175">Vous pouvez filtrer vers le bas sur toosee d’adresses IP/ports spécifique le nombre et le type d’alerte soit déclenchée.</span><span class="sxs-lookup"><span data-stu-id="93951-175">You can filter down on specific IPs/ports toosee how many and what kind of alerts are being triggered.</span></span>

    ![image 6][6]

1. <span data-ttu-id="93951-177">Résumé des alertes : un tableau récapitulant les spécificités de chaque alerte.</span><span class="sxs-lookup"><span data-stu-id="93951-177">Alert Summary – a table summarizing specific details of each individual alert.</span></span> <span data-ttu-id="93951-178">Vous pouvez personnaliser ce tooshow de table autres paramètres d’intérêt pour chaque alerte.</span><span class="sxs-lookup"><span data-stu-id="93951-178">You can customize this table tooshow other parameters of interest for each alert.</span></span>

    ![image 7][7]

<span data-ttu-id="93951-180">Pour plus d’informations sur la création de tableaux de bord et de visualisations personnalisés, consultez la [documentation officielle de Kibana](https://www.elastic.co/guide/en/kibana/current/introduction.html).</span><span class="sxs-lookup"><span data-stu-id="93951-180">For more documentation on creating custom visualizations and dashboards, see [Kibana’s official documentation](https://www.elastic.co/guide/en/kibana/current/introduction.html).</span></span>

## <a name="conclusion"></a><span data-ttu-id="93951-181">Conclusion</span><span class="sxs-lookup"><span data-stu-id="93951-181">Conclusion</span></span>

<span data-ttu-id="93951-182">L’association des captures de paquets fournies par Network Watcher et des outils open source de système de détection d’intrusions tels que Suricata vous permet de détecter les intrusions dans un réseau pour un large éventail de menaces.</span><span class="sxs-lookup"><span data-stu-id="93951-182">By combining packet captures provided by Network Watcher and open source IDS tools such as Suricata, you can perform network intrusion detection for a wide range of threats.</span></span> <span data-ttu-id="93951-183">Ces tableaux de bord permettre de vous tooquickly identifier les tendances et les anomalies dans votre réseau, et explorez hello données toodiscover causes principales des alertes, telles que les agents utilisateurs malveillants ou des ports vulnérables.</span><span class="sxs-lookup"><span data-stu-id="93951-183">These dashboards allow you tooquickly spot trends and anomalies within your network, as well dig into hello data toodiscover root causes of alerts such as malicious user agents or vulnerable ports.</span></span> <span data-ttu-id="93951-184">Avec ces données extraites, vous pouvez prendre des décisions éclairées sur comment tooreact tooand protéger votre réseau à partir de toute tentative d’intrusion dangereux et créer des règles tooprevent intrusions futures tooyour réseau.</span><span class="sxs-lookup"><span data-stu-id="93951-184">With this extracted data, you can make informed decisions on how tooreact tooand protect your network from any harmful intrusion attempts, and create rules tooprevent future intrusions tooyour network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="93951-185">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="93951-185">Next steps</span></span>

<span data-ttu-id="93951-186">Découvrez comment tootrigger paquet capture en fonction des alertes en vous rendant sur [utiliser l’analyse du réseau proactive toodo paquet capture avec les fonctions de Azure](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="93951-186">Learn how tootrigger packet captures based on alerts by visiting [Use packet capture toodo proactive network monitoring with Azure Functions](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="93951-187">Découvrez comment toovisualize votre flux de groupe de sécurité réseau se connecte à Power BI en vous rendant sur [NSG de visualiser les flux de journaux avec Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="93951-187">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>



<!-- images -->
[1]: ./media/network-watcher-intrusion-detection-open-source-tools/figure1.png
[2]: ./media/network-watcher-intrusion-detection-open-source-tools/figure2.png
[3]: ./media/network-watcher-intrusion-detection-open-source-tools/figure3.png
[4]: ./media/network-watcher-intrusion-detection-open-source-tools/figure4.png
[5]: ./media/network-watcher-intrusion-detection-open-source-tools/figure5.png
[6]: ./media/network-watcher-intrusion-detection-open-source-tools/figure6.png
[7]: ./media/network-watcher-intrusion-detection-open-source-tools/figure7.png
