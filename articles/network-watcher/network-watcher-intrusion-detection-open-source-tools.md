---
title: "Détecter les intrusions dans un réseau avec Azure Network Watcher et des outils open source | Microsoft Docs"
description: "Cet article explique comment utiliser Azure Network Watcher et des outils open source pour détecter les intrusions dans un réseau"
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
ms.openlocfilehash: 82d5e525859ebe03b152c63e4debbae469049c12
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="perform-network-intrusion-detection-with-network-watcher-and-open-source-tools"></a><span data-ttu-id="31c99-103">Détecter les intrusions dans un réseau avec Azure Network Watcher et des outils open source</span><span class="sxs-lookup"><span data-stu-id="31c99-103">Perform network intrusion detection with Network Watcher and open source tools</span></span>

<span data-ttu-id="31c99-104">Les captures de paquets sont essentielles pour implémenter des systèmes de détection d’intrusions dans un réseau et surveiller la sécurité du réseau.</span><span class="sxs-lookup"><span data-stu-id="31c99-104">Packet captures are a key component for implementing network intrusion detection systems (IDS) and performing Network Security Monitoring (NSM).</span></span> <span data-ttu-id="31c99-105">Il existe plusieurs outils open source de systèmes de détection d’intrusions qui traitent des captures de paquets et recherchent les signatures des activités malveillantes et des intrusions dans un réseau éventuelles.</span><span class="sxs-lookup"><span data-stu-id="31c99-105">There are several open source IDS tools that process packet captures and look for signatures of possible network intrusions and malicious activity.</span></span> <span data-ttu-id="31c99-106">Les captures de paquets proposées par Network Watcher vous permettent d’analyser votre réseau et de détecter toute vulnérabilité ou intrusion dangereuse.</span><span class="sxs-lookup"><span data-stu-id="31c99-106">Using the packet captures provided by Network Watcher, you can analyze your network for any harmful intrusions or vulnerabilities.</span></span>

<span data-ttu-id="31c99-107">Suricata fait partie de ces outils open source. Il s’agit d’un moteur de systèmes de détection d’intrusions qui utilise des ensembles de règles pour surveiller le trafic réseau et qui déclenche des alertes en cas d’évènements suspects.</span><span class="sxs-lookup"><span data-stu-id="31c99-107">One such open source tool is Suricata, an IDS engine that uses rulesets to monitor network traffic and triggers alerts whenever suspicious events occur.</span></span> <span data-ttu-id="31c99-108">Suricata propose un moteur multithread, ce qui signifie qu’il peut effectuer une analyse du trafic réseau de manière plus rapide et plus efficace.</span><span class="sxs-lookup"><span data-stu-id="31c99-108">Suricata offers a multi-threaded engine, meaning it can perform network traffic analysis with increased speed and efficiency.</span></span> <span data-ttu-id="31c99-109">Pour plus d’informations sur Suricata et ses fonctionnalités, rendez-vous sur le site web correspondant : https://suricata-ids.org/.</span><span class="sxs-lookup"><span data-stu-id="31c99-109">For more details about Suricata and its capabilities, visit their website at https://suricata-ids.org/.</span></span>

## <a name="scenario"></a><span data-ttu-id="31c99-110">Scénario</span><span class="sxs-lookup"><span data-stu-id="31c99-110">Scenario</span></span>

<span data-ttu-id="31c99-111">Cet article explique comment configurer votre environnement pour détecter des intrusions dans un réseau à l’aide de Network Watcher, Suricata et de la pile élastique.</span><span class="sxs-lookup"><span data-stu-id="31c99-111">This article explains how to set up your environment to perform network intrusion detection using Network Watcher, Suricata, and the Elastic Stack.</span></span> <span data-ttu-id="31c99-112">Network Watcher vous fournit les captures de paquets permettant de détecter les intrusions dans un réseau.</span><span class="sxs-lookup"><span data-stu-id="31c99-112">Network Watcher provides you with the packet captures used to perform network intrusion detection.</span></span> <span data-ttu-id="31c99-113">Suricata traite les captures de paquets et déclenche des alertes basées sur les paquets qui correspondent à son ensemble de règles de menaces donné.</span><span class="sxs-lookup"><span data-stu-id="31c99-113">Suricata processes the packet captures and trigger alerts based on packets that match its given ruleset of threats.</span></span> <span data-ttu-id="31c99-114">Ces alertes sont stockées dans un fichier journal sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="31c99-114">These alerts are stored in a log file on your local machine.</span></span> <span data-ttu-id="31c99-115">La pile élastique vous permet d’indexer les journaux générés par Suricata et de les utiliser pour créer un tableau de bord Kibana. Vous bénéficiez ainsi d’une représentation visuelle des journaux et d’un moyen pour obtenir rapidement des informations sur les vulnérabilités éventuelles du réseau.</span><span class="sxs-lookup"><span data-stu-id="31c99-115">Using the Elastic Stack, the logs generated by Suricata can be indexed and used to create a Kibana dashboard, providing you with a visual representation of the logs and a means to quickly gain insights to potential network vulnerabilities.</span></span>  

![scénario d’application web simple][1]

<span data-ttu-id="31c99-117">Les deux outils open source peuvent être configurés sur une machine virtuelle Azure, ce qui vous permet d’effectuer cette analyse dans votre propre environnement réseau Azure.</span><span class="sxs-lookup"><span data-stu-id="31c99-117">Both open source tools can be set up on an Azure VM, allowing you to perform this analysis within your own Azure network environment.</span></span>

## <a name="steps"></a><span data-ttu-id="31c99-118">Étapes</span><span class="sxs-lookup"><span data-stu-id="31c99-118">Steps</span></span>

### <a name="install-suricata"></a><span data-ttu-id="31c99-119">Installer Suricata</span><span class="sxs-lookup"><span data-stu-id="31c99-119">Install Suricata</span></span>

<span data-ttu-id="31c99-120">Pour toutes les autres méthodes d’installation, rendez-vous sur http://suricata.readthedocs.io/en/latest/install.html.</span><span class="sxs-lookup"><span data-stu-id="31c99-120">For all other methods of installation, visit http://suricata.readthedocs.io/en/latest/install.html</span></span>

1. <span data-ttu-id="31c99-121">Dans le terminal de ligne de commande de votre machine virtuelle, exécutez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="31c99-121">In the command-line terminal of your VM run the following commands:</span></span>

    ```
    sudo add-apt-repository ppa:oisf/suricata-stable
    sudo apt-get update
    sudo sudo apt-get install suricata
    ```

1. <span data-ttu-id="31c99-122">Pour vérifier votre installation, exécutez la commande `suricata -h` pour afficher la liste complète des commandes.</span><span class="sxs-lookup"><span data-stu-id="31c99-122">To verify your installation, run the command `suricata -h` to see the full list of commands.</span></span>

### <a name="download-the-emerging-threats-ruleset"></a><span data-ttu-id="31c99-123">Télécharger l’ensemble de règles de menaces émergentes</span><span class="sxs-lookup"><span data-stu-id="31c99-123">Download the Emerging Threats ruleset</span></span>

<span data-ttu-id="31c99-124">À ce stade, Suricata n’a aucune règle à exécuter.</span><span class="sxs-lookup"><span data-stu-id="31c99-124">At this stage, we do not have any rules for Suricata to run.</span></span> <span data-ttu-id="31c99-125">Vous pouvez créer vos propres règles s’il existe des menaces spécifiques à votre réseau que vous souhaitez détecter, mais vous pouvez aussi utiliser des ensembles de règles développées issus de plusieurs fournisseurs, tels que les menaces émergentes ou les règles VRT de Snort.</span><span class="sxs-lookup"><span data-stu-id="31c99-125">You can create your own rules if there are specific threats to your network you would like to detect, or you can also use developed rule sets from a number of providers, such as Emerging Threats, or VRT rules from Snort.</span></span> <span data-ttu-id="31c99-126">Nous utilisons le groupe de règles de menaces émergentes en accès libre ici :</span><span class="sxs-lookup"><span data-stu-id="31c99-126">We use the freely accessible Emerging Threats ruleset here:</span></span>

<span data-ttu-id="31c99-127">Téléchargez l’ensemble de règles et copiez-le dans le répertoire :</span><span class="sxs-lookup"><span data-stu-id="31c99-127">Download the rule set and copy them into the directory:</span></span>

```
wget http://rules.emergingthreats.net/open/suricata/emerging.rules.tar.gz
tar zxf emerging.rules.tar.gz
sudo cp -r rules /etc/suricata/
```

### <a name="process-packet-captures-with-suricata"></a><span data-ttu-id="31c99-128">Traiter les captures de paquets avec Suricata</span><span class="sxs-lookup"><span data-stu-id="31c99-128">Process packet captures with Suricata</span></span>

<span data-ttu-id="31c99-129">Pour traiter les captures de paquets à l’aide de Suricata, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="31c99-129">To process packet captures using Suricata, run the following command:</span></span>

```
sudo suricata -c /etc/suricata/suricata.yaml -r <location_of_pcapfile>
```
<span data-ttu-id="31c99-130">Pour consulter les alertes générées, parcourez le fichier fast.log :</span><span class="sxs-lookup"><span data-stu-id="31c99-130">To check the resulting alerts, read the fast.log file:</span></span>
```
tail -f /var/log/suricata/fast.log
```

### <a name="set-up-the-elastic-stack"></a><span data-ttu-id="31c99-131">Configurer la pile élastique</span><span class="sxs-lookup"><span data-stu-id="31c99-131">Set up the Elastic Stack</span></span>

<span data-ttu-id="31c99-132">Même si les journaux créés par Suricata contiennent des informations importantes sur l’activité de notre réseau, ceux-ci ne sont pas les plus faciles à lire et à comprendre.</span><span class="sxs-lookup"><span data-stu-id="31c99-132">While the logs that Suricata produces contain valuable information about what’s happening on our network, these log files aren’t the easiest to read and understand.</span></span> <span data-ttu-id="31c99-133">En connectant Suricata à la pile élastique, nous pouvons générer un tableau de bord Kibana qui nous permet de rechercher, de créer des graphiques, d’analyser et d’obtenir des informations à partir de nos journaux.</span><span class="sxs-lookup"><span data-stu-id="31c99-133">By connecting Suricata with the Elastic Stack, we can create a Kibana dashboard what allows us to search, graph, analyze, and derive insights from our logs.</span></span>

#### <a name="install-elasticsearch"></a><span data-ttu-id="31c99-134">Installer Elasticsearch</span><span class="sxs-lookup"><span data-stu-id="31c99-134">Install Elasticsearch</span></span>

1. <span data-ttu-id="31c99-135">La Suite Elastic à partir de la version 5.0 et pour les versions ultérieures requiert Java 8.</span><span class="sxs-lookup"><span data-stu-id="31c99-135">The Elastic Stack from version 5.0 and above requires Java 8.</span></span> <span data-ttu-id="31c99-136">Exécutez la commande `java -version` pour vérifier la version que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="31c99-136">Run the command `java -version` to check your version.</span></span> <span data-ttu-id="31c99-137">Si Java n’est pas installé sur votre ordinateur, reportez-vous à la documentation sur le [site web d’Oracle](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html).</span><span class="sxs-lookup"><span data-stu-id="31c99-137">If you do not have java install, refer to documentation on [Oracle's website](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span></span>
1. <span data-ttu-id="31c99-138">Téléchargez le package binaire approprié pour votre système :</span><span class="sxs-lookup"><span data-stu-id="31c99-138">Download the correct binary package for your system:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.2.0.deb
    sudo dpkg -i elasticsearch-5.2.0.deb
    sudo /etc/init.d/elasticsearch start
    ```

    <span data-ttu-id="31c99-139">D’autres méthodes d’installation se trouvent sur la page [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html) (Installation d’Elasticsearch).</span><span class="sxs-lookup"><span data-stu-id="31c99-139">Other installation methods can be found at [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)</span></span>

1. <span data-ttu-id="31c99-140">Vérifiez qu’Elasticsearch est en cours d’exécution avec la commande :</span><span class="sxs-lookup"><span data-stu-id="31c99-140">Verify that Elasticsearch is running with the command:</span></span>

    ```
    curl http://127.0.0.1:9200
    ```

    <span data-ttu-id="31c99-141">Une réponse similaire à celle ci-dessous devrait s’afficher :</span><span class="sxs-lookup"><span data-stu-id="31c99-141">You should see a response similar to this:</span></span>

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

<span data-ttu-id="31c99-142">Pour plus d’informations sur l’installation d’Elasticsearch, reportez-vous à la page [Installation](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html).</span><span class="sxs-lookup"><span data-stu-id="31c99-142">For further instructions on installing Elastic search, refer to the page [Installation](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span></span>

### <a name="install-logstash"></a><span data-ttu-id="31c99-143">Installer Logstash</span><span class="sxs-lookup"><span data-stu-id="31c99-143">Install Logstash</span></span>

1. <span data-ttu-id="31c99-144">Exécutez les commandes suivantes pour installer Logstash :</span><span class="sxs-lookup"><span data-stu-id="31c99-144">To install Logstash run the following commands:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.2.0.deb
    sudo dpkg -i logstash-5.2.0.deb
    ```
1. <span data-ttu-id="31c99-145">Ensuite, nous devons configurer Logstash pour qu’il puisse lire à partir de la sortie du fichier de eve.json.</span><span class="sxs-lookup"><span data-stu-id="31c99-145">Next we need to configure Logstash to read from the output of eve.json file.</span></span> <span data-ttu-id="31c99-146">Créez un fichier logstash.conf à l’aide de :</span><span class="sxs-lookup"><span data-stu-id="31c99-146">Create a logstash.conf file using:</span></span>

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. <span data-ttu-id="31c99-147">Ajoutez le contenu suivant au fichier (veillez à ce que le chemin d’accès au fichier eve.json soit correct) :</span><span class="sxs-lookup"><span data-stu-id="31c99-147">Add the following content to the file (make sure that the path to the eve.json file is correct):</span></span>

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

1. <span data-ttu-id="31c99-148">Assurez-vous d’accorder les autorisations appropriées pour le fichier eve.json afin que Logstash puisse ingérer le fichier.</span><span class="sxs-lookup"><span data-stu-id="31c99-148">Make sure to give the correct permissions to the eve.json file so that Logstash can ingest the file.</span></span>
    
    ```
    sudo chmod 775 /var/log/suricata/eve.json
    ```

1. <span data-ttu-id="31c99-149">Pour démarrer Logstash, exécutez la commande :</span><span class="sxs-lookup"><span data-stu-id="31c99-149">To start Logstash run the command:</span></span>

    ```
    sudo /etc/init.d/logstash start
    ```

<span data-ttu-id="31c99-150">Pour plus d’informations sur l’installation de Logstash, reportez-vous à la [documentation officielle](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html).</span><span class="sxs-lookup"><span data-stu-id="31c99-150">For further instructions on installing Logstash, refer to the [official documentation](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span></span>

### <a name="install-kibana"></a><span data-ttu-id="31c99-151">Installer Kibana</span><span class="sxs-lookup"><span data-stu-id="31c99-151">Install Kibana</span></span>

1. <span data-ttu-id="31c99-152">Exécutez les commandes suivantes pour installer Kibana :</span><span class="sxs-lookup"><span data-stu-id="31c99-152">Run the following commands to install Kibana:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-5.2.0-linux-x86_64.tar.gz
    tar xzvf kibana-5.2.0-linux-x86_64.tar.gz

    ```
1. <span data-ttu-id="31c99-153">Pour exécuter Kibana, exécutez les commandes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="31c99-153">To run Kibana use the commands:</span></span>

    ```
    cd kibana-5.2.0-linux-x86_64/
    ./bin/kibana
    ```

1. <span data-ttu-id="31c99-154">Pour afficher votre interface web Kibana, accédez à `http://localhost:5601`.</span><span class="sxs-lookup"><span data-stu-id="31c99-154">To view your Kibana web interface, navigate to `http://localhost:5601`</span></span>
1. <span data-ttu-id="31c99-155">Dans ce scénario, le modèle d’index utilisé pour les journaux Suricata est « logstash-* ».</span><span class="sxs-lookup"><span data-stu-id="31c99-155">For this scenario, the index pattern used for the Suricata logs is "logstash-*"</span></span>

1. <span data-ttu-id="31c99-156">Si vous souhaitez afficher le tableau de bord Kibana à distance, créez une règle de groupe de sécurité réseau entrante autorisant l’accès au **port 5601**.</span><span class="sxs-lookup"><span data-stu-id="31c99-156">If you want to view the Kibana dashboard remotely, create an inbound NSG rule allowing access to **port 5601**.</span></span>

### <a name="create-a-kibana-dashboard"></a><span data-ttu-id="31c99-157">Créer un tableau de bord Kibana</span><span class="sxs-lookup"><span data-stu-id="31c99-157">Create a Kibana dashboard</span></span>

<span data-ttu-id="31c99-158">Dans le cadre de cet article, nous proposons un exemple de tableau de bord pour que vous puissiez visualiser les tendances et les informations associées à vos alertes.</span><span class="sxs-lookup"><span data-stu-id="31c99-158">For this article, we have provided a sample dashboard for you to view trends and details in your alerts.</span></span>

1. <span data-ttu-id="31c99-159">Téléchargez le fichier du tableau de bord [ici](https://aka.ms/networkwatchersuricatadashboard), le fichier de visualisation [ici](https://aka.ms/networkwatchersuricatavisualization)et le fichier de recherche sauvegardée [ici](https://aka.ms/networkwatchersuricatasavedsearch).</span><span class="sxs-lookup"><span data-stu-id="31c99-159">Download the dashboard file [here](https://aka.ms/networkwatchersuricatadashboard), the visualization file [here](https://aka.ms/networkwatchersuricatavisualization), and the saved search file [here](https://aka.ms/networkwatchersuricatasavedsearch).</span></span>

1. <span data-ttu-id="31c99-160">Dans l’onglet **Gestion** de Kibana, accédez à **Saved Objects** (Objets enregistrés) et importez les trois fichiers.</span><span class="sxs-lookup"><span data-stu-id="31c99-160">Under the **Management** tab of Kibana, navigate to **Saved Objects** and import all three files.</span></span> <span data-ttu-id="31c99-161">Puis, à partir de l’onglet **Tableau de bord**, vous pouvez ouvrir et charger l’exemple de tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="31c99-161">Then from the **Dashboard** tab you can open and load the sample dashboard.</span></span>

<span data-ttu-id="31c99-162">Vous avez également la possibilité de créer vos propres visualisations et tableaux de bord en fonction des mesures qui vous intéressent.</span><span class="sxs-lookup"><span data-stu-id="31c99-162">You can also create your own visualizations and dashboards tailored towards metrics of your own interest.</span></span> <span data-ttu-id="31c99-163">Reportez-vous à la [documentation officielle](https://www.elastic.co/guide/en/kibana/current/visualize.html) de Kibana pour en savoir plus sur la création de visualisations Kibana.</span><span class="sxs-lookup"><span data-stu-id="31c99-163">Read more about creating Kibana visualizations from Kibana's [official documentation](https://www.elastic.co/guide/en/kibana/current/visualize.html).</span></span>

![tableau de bord Kibana][2]

### <a name="visualize-ids-alert-logs"></a><span data-ttu-id="31c99-165">Visualiser les journaux d’alertes de système de détection d’intrusions</span><span class="sxs-lookup"><span data-stu-id="31c99-165">Visualize IDS alert logs</span></span>

<span data-ttu-id="31c99-166">L’exemple de tableau de bord fournit plusieurs visualisations des journaux d’alertes Suricata :</span><span class="sxs-lookup"><span data-stu-id="31c99-166">The sample dashboard provides several visualizations of the Suricata alert logs:</span></span>

1. <span data-ttu-id="31c99-167">Alerts by GeoIP (Alertes par GeoIP) : une carte affichant la répartition des alertes par pays d’origine en fonction de l’emplacement géographique (déterminé par l’adresse IP).</span><span class="sxs-lookup"><span data-stu-id="31c99-167">Alerts by GeoIP – a map showing the distribution of alerts by their country of origin based on geographic location (determined by IP)</span></span>

    ![geo ip][3]

1. <span data-ttu-id="31c99-169">Top 10 Alerts (Top 10 des alertes) : un résumé des 10 alertes déclenchées les plus fréquentes et leur description.</span><span class="sxs-lookup"><span data-stu-id="31c99-169">Top 10 Alerts – a summary of the 10 most frequent triggered alerts and their description.</span></span> <span data-ttu-id="31c99-170">Cliquer sur une alerte permet d’appliquer un filtre sur le tableau de bord pour qu’il affiche uniquement les informations associées à cette alerte spécifique.</span><span class="sxs-lookup"><span data-stu-id="31c99-170">Clicking an individual alert filters down the dashboard to the information pertaining to that specific alert.</span></span>

    ![image 4][4]

1. <span data-ttu-id="31c99-172">Nombre d’alertes : le nombre total d’alertes déclenchées par le groupe de règles.</span><span class="sxs-lookup"><span data-stu-id="31c99-172">Number of Alerts – the total count of alerts triggered by the ruleset</span></span>

    ![image 5][5]

1. <span data-ttu-id="31c99-174">Top 20 Source/Destination IPs/Ports (Top 20 des ports/adresses IP source et de destination) : graphiques à secteurs montrant le top 20 des adresses IP et ports sur lesquels les alertes ont été déclenchées.</span><span class="sxs-lookup"><span data-stu-id="31c99-174">Top 20 Source/Destination IPs/Ports - pie charts showing the top 20 IPs and ports that alerts were triggered on.</span></span> <span data-ttu-id="31c99-175">Vous pouvez appliquer un filtre sur des adresses IP/ports spécifiques pour connaître le nombre et le type d’alertes déclenchées.</span><span class="sxs-lookup"><span data-stu-id="31c99-175">You can filter down on specific IPs/ports to see how many and what kind of alerts are being triggered.</span></span>

    ![image 6][6]

1. <span data-ttu-id="31c99-177">Résumé des alertes : un tableau récapitulant les spécificités de chaque alerte.</span><span class="sxs-lookup"><span data-stu-id="31c99-177">Alert Summary – a table summarizing specific details of each individual alert.</span></span> <span data-ttu-id="31c99-178">Vous pouvez personnaliser ce tableau pour afficher d’autres paramètres qui vous intéressent pour chaque alerte.</span><span class="sxs-lookup"><span data-stu-id="31c99-178">You can customize this table to show other parameters of interest for each alert.</span></span>

    ![image 7][7]

<span data-ttu-id="31c99-180">Pour plus d’informations sur la création de tableaux de bord et de visualisations personnalisés, consultez la [documentation officielle de Kibana](https://www.elastic.co/guide/en/kibana/current/introduction.html).</span><span class="sxs-lookup"><span data-stu-id="31c99-180">For more documentation on creating custom visualizations and dashboards, see [Kibana’s official documentation](https://www.elastic.co/guide/en/kibana/current/introduction.html).</span></span>

## <a name="conclusion"></a><span data-ttu-id="31c99-181">Conclusion</span><span class="sxs-lookup"><span data-stu-id="31c99-181">Conclusion</span></span>

<span data-ttu-id="31c99-182">L’association des captures de paquets fournies par Network Watcher et des outils open source de système de détection d’intrusions tels que Suricata vous permet de détecter les intrusions dans un réseau pour un large éventail de menaces.</span><span class="sxs-lookup"><span data-stu-id="31c99-182">By combining packet captures provided by Network Watcher and open source IDS tools such as Suricata, you can perform network intrusion detection for a wide range of threats.</span></span> <span data-ttu-id="31c99-183">Ces tableaux de bord vous donnent la possibilité d’identifier rapidement les tendances et les anomalies au sein de votre réseau, mais également d’analyser les données pour détecter les causes premières des alertes, telles que des agents utilisateur malveillants ou des ports vulnérables.</span><span class="sxs-lookup"><span data-stu-id="31c99-183">These dashboards allow you to quickly spot trends and anomalies within your network, as well dig into the data to discover root causes of alerts such as malicious user agents or vulnerable ports.</span></span> <span data-ttu-id="31c99-184">Avec ces données extraites, vous pouvez prendre des décisions avisées sur l’attitude et les méthodes à adopter pour protéger votre réseau de toute tentative d’intrusion dangereuse, et créer des règles pour empêcher les intrusions futures.</span><span class="sxs-lookup"><span data-stu-id="31c99-184">With this extracted data, you can make informed decisions on how to react to and protect your network from any harmful intrusion attempts, and create rules to prevent future intrusions to your network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="31c99-185">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="31c99-185">Next steps</span></span>

<span data-ttu-id="31c99-186">Découvrez comment déclencher des captures de paquets en fonction des alertes en vous rendant sur [Use packet capture to do proactive network monitoring with Azure Functions](network-watcher-alert-triggered-packet-capture.md) (Utiliser des captures de paquets pour la surveillance proactive du réseau avec Azure Functions).</span><span class="sxs-lookup"><span data-stu-id="31c99-186">Learn how to trigger packet captures based on alerts by visiting [Use packet capture to do proactive network monitoring with Azure Functions](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="31c99-187">Découvrez comment visualiser vos journaux de flux de groupe de sécurité réseau avec Power BI en consultant la page [Visualizing Network Security Group flow logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md) (Visualisation des journaux de flux de groupe de sécurité réseau avec Power BI).</span><span class="sxs-lookup"><span data-stu-id="31c99-187">Learn how to visualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>



<!-- images -->
[1]: ./media/network-watcher-intrusion-detection-open-source-tools/figure1.png
[2]: ./media/network-watcher-intrusion-detection-open-source-tools/figure2.png
[3]: ./media/network-watcher-intrusion-detection-open-source-tools/figure3.png
[4]: ./media/network-watcher-intrusion-detection-open-source-tools/figure4.png
[5]: ./media/network-watcher-intrusion-detection-open-source-tools/figure5.png
[6]: ./media/network-watcher-intrusion-detection-open-source-tools/figure6.png
[7]: ./media/network-watcher-intrusion-detection-open-source-tools/figure7.png
