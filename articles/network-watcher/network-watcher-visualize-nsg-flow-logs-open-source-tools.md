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
# <a name="visualize-azure-network-watcher-nsg-flow-logs-using-open-source-tools"></a><span data-ttu-id="ef178-103">Visualiser les journaux de flux NSG d’Azure Network Watcher à l’aide d’outils open source</span><span class="sxs-lookup"><span data-stu-id="ef178-103">Visualize Azure Network Watcher NSG flow logs using open source tools</span></span>

<span data-ttu-id="ef178-104">Les journaux des flux de groupe de sécurité réseau fournissent des informations permettant de comprendre le trafic IP entrant et sortant sur les groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="ef178-104">Network Security Group flow logs provide information that can be used understand ingress and egress IP traffic on Network Security Groups.</span></span> <span data-ttu-id="ef178-105">Ces journaux flux affiche sortant et les flux entrants sur une base par la règle, hello flux hello de carte réseau s’applique, 5 tuple plus d’informations sur le flux hello (Source/Destination IP, Port de la Source et de Destination, protocole), et si le trafic de hello a été autorisé ou refusé.</span><span class="sxs-lookup"><span data-stu-id="ef178-105">These flow logs show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5 tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

<span data-ttu-id="ef178-106">Ces journaux de flux peut être difficile toomanually analyse et obtenir des informations détaillées.</span><span class="sxs-lookup"><span data-stu-id="ef178-106">These flow logs can be difficult toomanually parse and gain insights from.</span></span> <span data-ttu-id="ef178-107">Toutefois, il existe de nombreux outils open source qui peuvent aider à visualiser ces données.</span><span class="sxs-lookup"><span data-stu-id="ef178-107">However, there are several open source tools that can help visualize this data.</span></span> <span data-ttu-id="ef178-108">Cet article fournit une solution toovisualize ces journaux à l’aide de hello pile élastique, qui vous tooquickly index et de visualiser vos journaux de flux dans un tableau de bord Kibana.</span><span class="sxs-lookup"><span data-stu-id="ef178-108">This article will provide a solution toovisualize these logs using hello Elastic Stack, which will allow you tooquickly index and visualize your flow logs on a Kibana dashboard.</span></span>

## <a name="scenario"></a><span data-ttu-id="ef178-109">Scénario</span><span class="sxs-lookup"><span data-stu-id="ef178-109">Scenario</span></span>

<span data-ttu-id="ef178-110">Dans cet article, nous allons définir une solution qui vous permettra de journaux de flux de groupe de sécurité réseau toovisualize à l’aide de hello pile élastique.</span><span class="sxs-lookup"><span data-stu-id="ef178-110">In this article, we will set up a solution that will allow you toovisualize Network Security Group flow logs using hello Elastic Stack.</span></span>  <span data-ttu-id="ef178-111">Un plug-in d’entrée Logstash obtiendra les journaux de flux hello directement à partir de l’objet blob de stockage hello configuré pour contenant les journaux de flux hello.</span><span class="sxs-lookup"><span data-stu-id="ef178-111">A Logstash input plugin will obtain hello flow logs directly from hello storage blob configured for containing hello flow logs.</span></span> <span data-ttu-id="ef178-112">Ensuite, les journaux de flux de hello à l’aide de hello pile élastique, seront indexés et utilisé toocreate un Kibana du tableau de bord toovisualize hello des informations.</span><span class="sxs-lookup"><span data-stu-id="ef178-112">Then, using hello Elastic Stack, hello flow logs will be indexed and used toocreate a Kibana dashboard toovisualize hello information.</span></span>

![scénario][scenario]

## <a name="steps"></a><span data-ttu-id="ef178-114">Étapes</span><span class="sxs-lookup"><span data-stu-id="ef178-114">Steps</span></span>

### <a name="enable-network-security-group-flow-logging"></a><span data-ttu-id="ef178-115">Activer les journaux des flux de groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="ef178-115">Enable Network Security Group flow logging</span></span>
<span data-ttu-id="ef178-116">Pour ce scénario, la journalisation des flux de groupe de sécurité réseau doit être activée sur au moins un groupe de sécurité réseau dans votre compte.</span><span class="sxs-lookup"><span data-stu-id="ef178-116">For this scenario, you must have Network Security Group Flow Logging enabled on at least one Network Security Group in your account.</span></span> <span data-ttu-id="ef178-117">Pour obtenir des instructions sur l’activation des journaux de sécurité de flux de réseau, consultez toohello l’article suivant [journalisation tooflow de présentation pour les groupes de sécurité réseau](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ef178-117">For instructions on enabling Network Security Flow Logs, refer toohello following article [Introduction tooflow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span></span>


### <a name="set-up-hello-elastic-stack"></a><span data-ttu-id="ef178-118">Configurer hello pile élastique</span><span class="sxs-lookup"><span data-stu-id="ef178-118">Set up hello Elastic Stack</span></span>
<span data-ttu-id="ef178-119">En connectant le groupe de sécurité réseau de flux de journaux avec hello pile élastique, nous pouvons créer un tableau de bord Kibana qui nous permet de toosearch, graphique, analyser et dégager de nos journaux.</span><span class="sxs-lookup"><span data-stu-id="ef178-119">By connecting NSG flow logs with hello Elastic Stack, we can create a Kibana dashboard what allows us toosearch, graph, analyze, and derive insights from our logs.</span></span>

#### <a name="install-elasticsearch"></a><span data-ttu-id="ef178-120">Installer Elasticsearch</span><span class="sxs-lookup"><span data-stu-id="ef178-120">Install Elasticsearch</span></span>

1. <span data-ttu-id="ef178-121">Hello pile élastique de la version 5.0 et versions ultérieures nécessite Java 8.</span><span class="sxs-lookup"><span data-stu-id="ef178-121">hello Elastic Stack from version 5.0 and above requires Java 8.</span></span> <span data-ttu-id="ef178-122">Exécutez la commande hello `java -version` toocheck votre version.</span><span class="sxs-lookup"><span data-stu-id="ef178-122">Run hello command `java -version` toocheck your version.</span></span> <span data-ttu-id="ef178-123">Si vous n’avez pas java installation, consultez toodocumentation sur [site Web d’Oracle](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span><span class="sxs-lookup"><span data-stu-id="ef178-123">If you do not have java install, refer toodocumentation on [Oracle's website](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span></span>
1. <span data-ttu-id="ef178-124">Téléchargez hello binaire package pour votre système :</span><span class="sxs-lookup"><span data-stu-id="ef178-124">Download hello correct binary package for your system:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.2.0.deb
    sudo dpkg -i elasticsearch-5.2.0.deb
    sudo /etc/init.d/elasticsearch start
    ```

    <span data-ttu-id="ef178-125">D’autres méthodes d’installation se trouvent sur la page [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html) (Installation d’Elasticsearch).</span><span class="sxs-lookup"><span data-stu-id="ef178-125">Other installation methods can be found at [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)</span></span>

1. <span data-ttu-id="ef178-126">Vérifiez que Elasticsearch est en cours d’exécution avec la commande hello :</span><span class="sxs-lookup"><span data-stu-id="ef178-126">Verify that Elasticsearch is running with hello command:</span></span>

    ```
    curl http://127.0.0.1:9200
    ```

    <span data-ttu-id="ef178-127">Vous devez voir un toothis similaire de réponse :</span><span class="sxs-lookup"><span data-stu-id="ef178-127">You should see a response similar toothis:</span></span>

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

<span data-ttu-id="ef178-128">Pour plus d’informations sur la recherche élastique lors de l’installation, consultez toohello page [Installation](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span><span class="sxs-lookup"><span data-stu-id="ef178-128">For further instructions on installing Elastic search, refer toohello page [Installation](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span></span>

### <a name="install-logstash"></a><span data-ttu-id="ef178-129">Installer Logstash</span><span class="sxs-lookup"><span data-stu-id="ef178-129">Install Logstash</span></span>

1. <span data-ttu-id="ef178-130">tooinstall Logstash hello suivant de commandes, exécutez :</span><span class="sxs-lookup"><span data-stu-id="ef178-130">tooinstall Logstash run hello following commands:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.2.0.deb
    sudo dpkg -i logstash-5.2.0.deb
    ```
1. <span data-ttu-id="ef178-131">Ensuite, nous devez tooconfigure Logstash tooaccess et analyse les journaux de flux hello.</span><span class="sxs-lookup"><span data-stu-id="ef178-131">Next we need tooconfigure Logstash tooaccess and parse hello flow logs.</span></span> <span data-ttu-id="ef178-132">Créez un fichier logstash.conf à l’aide de :</span><span class="sxs-lookup"><span data-stu-id="ef178-132">Create a logstash.conf file using:</span></span>

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. <span data-ttu-id="ef178-133">Ajoutez hello contenu toohello le fichier suivant :</span><span class="sxs-lookup"><span data-stu-id="ef178-133">Add hello following content toohello file:</span></span>

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

<span data-ttu-id="ef178-134">Pour obtenir des instructions sur l’installation de Logstash, consultez toohello [documentation officielle](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span><span class="sxs-lookup"><span data-stu-id="ef178-134">For further instructions on installing Logstash, refer toohello [official documentation](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span></span>

### <a name="install-hello-logstash-input-plugin-for-azure-blob-storage"></a><span data-ttu-id="ef178-135">Installer le plug-in hello Logstash d’entrée pour le stockage d’objets blob Azure</span><span class="sxs-lookup"><span data-stu-id="ef178-135">Install hello Logstash input plugin for Azure blob storage</span></span>

<span data-ttu-id="ef178-136">Ce plug-in Logstash vous permettra de journaux de flux hello toodirectly accès à partir de leur compte de stockage désignées.</span><span class="sxs-lookup"><span data-stu-id="ef178-136">This Logstash plugin will allow you toodirectly access hello flow logs from their designated storage account.</span></span> <span data-ttu-id="ef178-137">tooinstall ce plug-in, à partir du répertoire d’installation Logstash hello par défaut (dans ce cas /usr/share/logstash/bin) exécutez hello commande :</span><span class="sxs-lookup"><span data-stu-id="ef178-137">tooinstall this plugin, from hello default Logstash installation directory (in this case /usr/share/logstash/bin) run hello command:</span></span>

```
logstash-plugin install logstash-input-azureblob
```

<span data-ttu-id="ef178-138">toostart Logstash, exécutez la commande hello :</span><span class="sxs-lookup"><span data-stu-id="ef178-138">toostart Logstash run hello command:</span></span>

```
sudo /etc/init.d/logstash start
```

<span data-ttu-id="ef178-139">Pour plus d’informations sur ce plug-in, consultez toodocumentation [ici](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob)</span><span class="sxs-lookup"><span data-stu-id="ef178-139">For more information about this plugin, refer toodocumentation [here](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob)</span></span>

### <a name="install-kibana"></a><span data-ttu-id="ef178-140">Installer Kibana</span><span class="sxs-lookup"><span data-stu-id="ef178-140">Install Kibana</span></span>

1. <span data-ttu-id="ef178-141">Exécutez hello suivant de commandes tooinstall Kibana :</span><span class="sxs-lookup"><span data-stu-id="ef178-141">Run hello following commands tooinstall Kibana:</span></span>

  ```
  curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-5.2.0-linux-x86_64.tar.gz
  tar xzvf kibana-5.2.0-linux-x86_64.tar.gz
  ```

1. <span data-ttu-id="ef178-142">toorun Kibana utiliser les commandes hello :</span><span class="sxs-lookup"><span data-stu-id="ef178-142">toorun Kibana use hello commands:</span></span>

  ```
  cd kibana-5.2.0-linux-x86_64/
  ./bin/kibana
  ```

1. <span data-ttu-id="ef178-143">tooview votre site web Kibana interface, accédez trop`http://localhost:5601`</span><span class="sxs-lookup"><span data-stu-id="ef178-143">tooview your Kibana web interface, navigate too`http://localhost:5601`</span></span>
1. <span data-ttu-id="ef178-144">Pour ce scénario, hello index pour les journaux de flux hello consiste « groupe de sécurité réseau-flux de journaux ».</span><span class="sxs-lookup"><span data-stu-id="ef178-144">For this scenario, hello index pattern used for hello flow logs is "nsg-flow-logs".</span></span> <span data-ttu-id="ef178-145">Vous pouvez modifier le modèle d’index hello dans la section de « sortie » hello de votre fichier logstash.conf.</span><span class="sxs-lookup"><span data-stu-id="ef178-145">You may change hello index pattern in hello "output" section of your logstash.conf file.</span></span>

1. <span data-ttu-id="ef178-146">Si vous souhaitez Kibana du tableau de bord hello tooview à distance, créez une règle entrante de groupe de sécurité réseau autorisant l’accès trop**port 5601**.</span><span class="sxs-lookup"><span data-stu-id="ef178-146">If you want tooview hello Kibana dashboard remotely, create an inbound NSG rule allowing access too**port 5601**.</span></span>

### <a name="create-a-kibana-dashboard"></a><span data-ttu-id="ef178-147">Créer un tableau de bord Kibana</span><span class="sxs-lookup"><span data-stu-id="ef178-147">Create a Kibana dashboard</span></span>

<span data-ttu-id="ef178-148">Pour cet article, nous avons fourni un tableau de bord test vous tooview tendances et les détails de vos alertes.</span><span class="sxs-lookup"><span data-stu-id="ef178-148">For this article, we have provided a sample dashboard for you tooview trends and details in your alerts.</span></span>

![figure 1][1]

1. <span data-ttu-id="ef178-150">Téléchargez le fichier du tableau de bord hello [ici](https://aka.ms/networkwatchernsgflowlogdashboard), fichier de visualisation hello [ici](https://aka.ms/networkwatchernsgflowlogvisualizations)et le fichier de recherche hello enregistré [ici](https://aka.ms/networkwatchernsgflowlogsearch).</span><span class="sxs-lookup"><span data-stu-id="ef178-150">Download hello dashboard file [here](https://aka.ms/networkwatchernsgflowlogdashboard), hello visualization file [here](https://aka.ms/networkwatchernsgflowlogvisualizations), and hello saved search file [here](https://aka.ms/networkwatchernsgflowlogsearch).</span></span>

1. <span data-ttu-id="ef178-151">Sous hello **gestion** onglet naviguer trop de Kibana,**objets enregistrés** et importer les trois fichiers.</span><span class="sxs-lookup"><span data-stu-id="ef178-151">Under hello **Management** tab of Kibana, navigate too**Saved Objects** and import all three files.</span></span> <span data-ttu-id="ef178-152">Puis, à partir de hello **tableau de bord** onglet, vous pouvez ouvrir et charge de tableau de bord exemple hello.</span><span class="sxs-lookup"><span data-stu-id="ef178-152">Then from hello **Dashboard** tab you can open and load hello sample dashboard.</span></span>

<span data-ttu-id="ef178-153">Vous avez également la possibilité de créer vos propres visualisations et tableaux de bord en fonction des mesures qui vous intéressent.</span><span class="sxs-lookup"><span data-stu-id="ef178-153">You can also create your own visualizations and dashboards tailored towards metrics of your own interest.</span></span> <span data-ttu-id="ef178-154">Reportez-vous à la [documentation officielle](https://www.elastic.co/guide/en/kibana/current/visualize.html) de Kibana pour en savoir plus sur la création de visualisation Kibana.</span><span class="sxs-lookup"><span data-stu-id="ef178-154">Read more about creating Kibana visualizations from Kibana's [official documentation](https://www.elastic.co/guide/en/kibana/current/visualize.html).</span></span>

### <a name="visualize-nsg-flow-logs"></a><span data-ttu-id="ef178-155">Visualiser les journaux de flux NSG</span><span class="sxs-lookup"><span data-stu-id="ef178-155">Visualize NSG flow logs</span></span>

<span data-ttu-id="ef178-156">tableau de bord exemple Hello fournit plusieurs visualisations des journaux de flux hello :</span><span class="sxs-lookup"><span data-stu-id="ef178-156">hello sample dashboard provides several visualizations of hello flow logs:</span></span>

1. <span data-ttu-id="ef178-157">Flux à la décision ou de sens dans le temps - graphiques série montrant le numéro de hello de flux sur hello laps de temps en temps.</span><span class="sxs-lookup"><span data-stu-id="ef178-157">Flows by Decision/Direction Over Time - time series graphs showing hello number of flows over hello time period.</span></span> <span data-ttu-id="ef178-158">Vous pouvez modifier l’étendue de ces deux visualisations et unité hello de temps.</span><span class="sxs-lookup"><span data-stu-id="ef178-158">You can edit hello unit of time and span of both these visualizations.</span></span> <span data-ttu-id="ef178-159">Flux en proportion de hello montre la décision d’autoriser ou refuser des décisions lors de flux en Direction affiche hello proportion de trafic entrant et sortant.</span><span class="sxs-lookup"><span data-stu-id="ef178-159">Flows by Decision shows hello proportion of allow or deny decisions made, while Flows by Direction shows hello proportion of inbound and outbound traffic.</span></span> <span data-ttu-id="ef178-160">Grâce à ces éléments visuels, vous pouvez examiner les tendances du trafic au fil du temps et identifier les pics ou les modèles inhabituels.</span><span class="sxs-lookup"><span data-stu-id="ef178-160">With these visuals you can examine traffic trends over time and look for any spikes or unusual patterns.</span></span>

  ![figure 2][2]

1. <span data-ttu-id="ef178-162">Flux par le Port de Destination/Source : graphiques en secteurs montrant les ports respectifs de tootheir de répartition hello de flux.</span><span class="sxs-lookup"><span data-stu-id="ef178-162">Flows by Destination/Source Port – pie charts showing hello breakdown of flows tootheir respective ports.</span></span> <span data-ttu-id="ef178-163">Grâce à cette vue, vous pouvez visualiser les ports les plus fréquemment utilisés.</span><span class="sxs-lookup"><span data-stu-id="ef178-163">With this view you can see your most commonly used ports.</span></span> <span data-ttu-id="ef178-164">Si vous cliquez sur un port spécifique dans un graphique à secteurs de hello, reste hello du tableau de bord hello filtre vers le bas tooflows de ce port.</span><span class="sxs-lookup"><span data-stu-id="ef178-164">If you click on a specific port within hello pie chart, hello rest of hello dashboard will filter down tooflows of that port.</span></span>

  ![figure 3][3]

1. <span data-ttu-id="ef178-166">Nombre de flux et le plus ancien journal ponctualité – vous montrant numéro hello de flux enregistré et date hello du journal plus ancien de hello capturées.</span><span class="sxs-lookup"><span data-stu-id="ef178-166">Number of Flows and Earliest Log Time – metrics showing you hello number of flows recorded and hello date of hello earliest log captured.</span></span>

  ![figure 4][4]

1. <span data-ttu-id="ef178-168">Flux par groupe de sécurité réseau et de la règle : un graphique à barres affiche la distribution hello de flux au sein de chaque groupe de sécurité réseau, ainsi que la distribution hello de règles au sein de chaque groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="ef178-168">Flows by NSG and Rule – a bar graph showing you hello distribution of flows within each NSG, as well as hello distribution of rules within each NSG.</span></span> <span data-ttu-id="ef178-169">À ce stade, vous pouvez voir le groupe de sécurité réseau et les règles générées hello plus de trafic.</span><span class="sxs-lookup"><span data-stu-id="ef178-169">From here you can see which NSG and rules generated hello most traffic.</span></span>

  ![figure 5][5]

1. <span data-ttu-id="ef178-171">10 principaux Source ou la Destination des adresses IP – graphiques à barres en affichant la source des 10 premiers hello et les adresses IP de destination.</span><span class="sxs-lookup"><span data-stu-id="ef178-171">Top 10 Source/Destination IPs – bar charts showing hello top 10 source and destination IPs.</span></span> <span data-ttu-id="ef178-172">Vous pouvez ajuster ces tooshow graphiques plus ou moins premières adresses IP.</span><span class="sxs-lookup"><span data-stu-id="ef178-172">You can adjust these charts tooshow more or less top IPs.</span></span> <span data-ttu-id="ef178-173">À partir d’ici vous pouvez voir hello qui se produisent généralement des adresses IP ainsi que hello décision de trafic (autorisation ou refus) effectuée vers chaque adresse IP.</span><span class="sxs-lookup"><span data-stu-id="ef178-173">From here you can see hello most commonly occurring IPs as well as hello traffic decision (allow or deny) being made towards each IP.</span></span>

  ![figure 6][6]

1. <span data-ttu-id="ef178-175">Flux Tuples – ce tableau montre hello les informations contenues dans chaque tuple du flux, ainsi que ses NGS correspondante et la règle.</span><span class="sxs-lookup"><span data-stu-id="ef178-175">Flow Tuples – this table shows you hello information contained within each flow tuple, as well as its corresponding NGS and rule.</span></span>

  ![figure 7][7]

<span data-ttu-id="ef178-177">À l’aide de barre de requête hello haut hello du tableau de bord hello, vous pouvez filtrer vers le bas du tableau de bord hello selon n’importe quel paramètre de flux hello, telles que l’ID d’abonnement, groupes de ressources, règle ou toute autre variable dignes d’intérêt.</span><span class="sxs-lookup"><span data-stu-id="ef178-177">Using hello query bar at hello top of hello dashboard, you can filter down hello dashboard based on any parameter of hello flows, such as subscription ID, resource groups, rule, or any other variable of interest.</span></span> <span data-ttu-id="ef178-178">Pour plus d’informations sur les requêtes et les filtres de Kibana, consultez toohello [documentation officielle](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html)</span><span class="sxs-lookup"><span data-stu-id="ef178-178">For more about Kibana's queries and filters, refer toohello [official documentation](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html)</span></span>

## <a name="conclusion"></a><span data-ttu-id="ef178-179">Conclusion</span><span class="sxs-lookup"><span data-stu-id="ef178-179">Conclusion</span></span>

<span data-ttu-id="ef178-180">En combinant les journaux de flux de groupe de sécurité réseau hello avec hello pile élastique, nous avons élaborer moyen puissant et personnalisable toovisualize notre le trafic réseau.</span><span class="sxs-lookup"><span data-stu-id="ef178-180">By combining hello Network Security Group flow logs with hello Elastic Stack, we have come up with powerful and customizable way toovisualize our network traffic.</span></span> <span data-ttu-id="ef178-181">Ces tableaux de bord vous tooquickly gain et partage les informations relatives à votre trafic réseau, ainsi que les filtre vers le bas et examiner sur toute manipulation d’éventuelles anomalies.</span><span class="sxs-lookup"><span data-stu-id="ef178-181">These dashboards allow you tooquickly gain and share insights about your network traffic, as well as filter down and investigate on any potential anomalies.</span></span> <span data-ttu-id="ef178-182">À l’aide de Kibana, vous pouvez personnaliser ces tableaux de bord et créer des visualisations spécifique toomeet les besoins de sécurité, d’audit et de conformité.</span><span class="sxs-lookup"><span data-stu-id="ef178-182">Using Kibana, you can tailor these dashboards and create specific visualizations toomeet any security, audit, and compliance needs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef178-183">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ef178-183">Next steps</span></span>

<span data-ttu-id="ef178-184">Découvrez comment toovisualize votre flux de groupe de sécurité réseau se connecte à Power BI en vous rendant sur [NSG de visualiser les flux de journaux avec Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="ef178-184">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>


<!--Image references-->

[scenario]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/scenario.png
[1]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure7.png
