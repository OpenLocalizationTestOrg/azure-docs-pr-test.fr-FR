---
title: "aaaNetwork solution de l’Analyseur de performances dans Azure journal Analytique | Documents Microsoft"
description: "Moniteur de performances réseau dans l’Analytique des journaux Azure vous permet de surveiller les performances de hello de vos réseaux de près de real-time-toodetect et de localiser les goulots d’étranglement des performances réseau."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 5b9c9c83-3435-488c-b4f6-7653003ae18a
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.openlocfilehash: e074948221fdd003c640861d759c4ce69ced1cd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="network-performance-monitor-solution-in-log-analytics"></a>Solution Analyseur de performances réseau dans Log Analytics

![Symbole de Network Performance Monitor](./media/log-analytics-network-performance-monitor/npm-symbol.png)

Ce document décrit comment tooset à distance et utilisez hello solution d’analyse des performances réseau dans Analytique de journal, ce qui vous permet de surveiller les performances de hello de vos réseaux de près de real-time-toodetect et de localiser les goulots d’étranglement des performances réseau. Avec hello solution d’analyse des performances réseau, vous pouvez surveiller la perte de hello et la latence entre deux réseaux, des sous-réseaux ou les serveurs. Analyse des performances réseau détecte des problèmes de réseau, comme le trafic blackholing, des erreurs de routage et des problèmes que méthodes d’analyse réseau classiques ne sont pas en mesure de toodetect. L’Analyseur de performances réseau génère des alertes et des notifications en cas de dépassement d’un seuil pour une liaison réseau. Ces seuils peuvent être appris automatiquement par le système de hello ou vous pouvez configurer les règles d’alerte personnalisés toouse. Analyse des performances réseau garantit la détection en temps voulu des problèmes de performances réseau et localise source hello de segment de réseau particulier tooa hello problème ou du périphérique.

Vous pouvez détecter les problèmes de réseau avec hello solution du tableau de bord qui affiche des informations récapitulatives sur votre réseau, y compris les événements de contrôle d’intégrité réseau récents, les liens de réseau défectueux et des liens de sous-réseau qui sont confrontés à une latence et les pertes de paquets. Vous pouvez Explorer dans un réseau lien tooview hello état actuel des liens de sous-réseau, ainsi que des liens de nœud à l’autre. Vous pouvez également afficher des tendances historiques de hello de perte et de latence à hello réseau, un sous-réseau et au niveau du nœud à l’autre. Vous pouvez détecter des problèmes réseau temporaires en affichant des graphiques de tendance historique de pertes de paquets et de latence, et localiser les goulots d’étranglement du réseau sur une carte topologique. graphique de topologie interactif Hello vous permet d’itinéraires de saut par saut réseau toovisualize hello et déterminer source hello problème de hello. Comme d’autres solutions, vous pouvez utiliser la recherche de journal pour l’analytique différents rapports personnalisés de spécifications toocreate basés sur des données de hello collectées par le moniteur de performances réseau.

solution de Hello utilise des transactions synthétiques comme des pannes de réseau toodetect mécanisme principal. Par conséquent, vous pouvez l’utiliser sans vous soucier du fournisseur ou du modèle d’un appareil réseau spécifique. Elle opère indifféremment dans des environnements locaux, cloud (IaaS) et hybrides. solution de Hello découvre automatiquement les hello la topologie réseau et des itinéraires différents dans votre réseau.

Réseau standard analyse produits se concentrent sur hello d’analyse réseau de l’intégrité du périphérique (routeurs, commutateurs, etc.) mais ne fournissent pas d’insights en hello réelle de qualité de connectivité réseau entre les deux points, analyseur de performances réseau.

### <a name="using-hello-solution-standalone"></a>À l’aide de hello solution autonome
Si vous souhaitez que la qualité hello toomonitor des connexions réseau entre les charges de travail critiques, réseaux, les centres de données ou les sites office, puis vous pouvez utiliser solution d’analyse des performances réseau hello seul toomonitor état de la connectivité entre :

* plusieurs centres de données ou sites de bureau connectés via un réseau public ou privé ;
* charges de travail critiques exécutant des applications métier ;
* services de cloud public comme Microsoft Azure ou les réseaux Amazon Web Services (AWS) et sur site, si vous disposez d’IaaS (VM) disponible et passerelles configuré tooallow la communication entre les réseaux locaux et cloud
* réseaux Azure et locaux lorsque vous utilisez ExpressRoute.

### <a name="using-hello-solution-with-other-networking-tools"></a>À l’aide de la solution de hello avec d’autres outils de mise en réseau
Si vous souhaitez toomonitor une ligne d’application d’entreprise, vous pouvez utiliser hello solution d’analyse des performances réseau comme une accompagnement solution tooother réseau des outils. Un réseau lent peut entraîner des applications de tooslow et analyse des performances réseau peuvent vous aider à étudier des problèmes de performances d’application sont dus à des problèmes réseau sous-jacents. Comme solution de hello ne requiert pas de n’importe quel toonetwork accèdent aux appareils, administrateur de l’application hello n’a pas besoin toorely sur un réseau équipe tooprovide des informations sur comment réseau de hello affecter les applications.

En outre, si vous est déjà investissez dans d’autres outils d’analyse de réseau, puis les solutions hello peuvent compléter ces outils, car les solutions de surveillance réseau plus traditionnelles ne fournissent pas de vue d’ensemble de mesures de performances réseau de bout en bout, comme la perte et la latence.  Hello solution d’analyse des performances réseau peut aider à combler cet écart.

## <a name="installing-and-configuring-agents-for-hello-solution"></a>Installation et configuration des agents pour les solutions hello
Utilisez des agents de tooinstall de processus de base hello à [tooLog d’ordinateurs Windows de se connecter Analytique](log-analytics-windows-agents.md) et [connecter Operations Manager tooLog Analytique](log-analytics-om-agents.md).

> [!NOTE]
> Vous devez agents tooinstall au moins 2 dans l’ordre toohave suffisamment toodiscover de données et surveiller les ressources de votre réseau. Sinon, la solution hello reste dans un état de configuration jusqu'à ce que vous installez et configurez des agents supplémentaires.
>
>

### <a name="where-tooinstall-hello-agents"></a>Où tooinstall hello agents
Avant d’installer des agents, envisagez de topologie hello de votre réseau et les parties de hello réseau que vous souhaitez toomonitor. Nous vous recommandons d’installer plusieurs agents pour chaque sous-réseau que vous souhaitez toomonitor. En d’autres termes, pour chaque sous-réseau que vous souhaitez toomonitor, choisissez deux ou plusieurs serveurs ou ordinateurs virtuels et installer l’agent de hello sur ces derniers.

Si vous ne savez pas sur la topologie de votre réseau hello, installer des agents de hello sur les serveurs avec des charges de travail critiques où vous souhaitez les performances du réseau toomonitor hello. Par exemple, vous pourriez suivre tookeep d’une connexion réseau entre un serveur Web et un serveur exécutant SQL Server. Dans ce cas, vous devez installer un agent sur les deux serveurs.

Agents analysent la connectivité réseau (liens) entre les hôtes--pas des hôtes hello eux-mêmes. Toomonitor c’est le cas, un lien réseau, vous devez installer des agents sur les deux points de terminaison de cette liaison.

### <a name="configure-agents"></a>Configurer les agents

Si vous avez l’intention de protocole ICMP toouse hello pour les transactions synthétiques, vous devez hello tooenable suivant les règles de pare-feu de manière fiable utilisant ICMP :

```
netsh advfirewall firewall add rule name="NPMDICMPV4Echo" protocol="icmpv4:8,any" dir=in action=allow
netsh advfirewall firewall add rule name="NPMDICMPV6Echo" protocol="icmpv6:128,any" dir=in action=allow
netsh advfirewall firewall add rule name="NPMDICMPV4DestinationUnreachable" protocol="icmpv4:3,any" dir=in action=allow
netsh advfirewall firewall add rule name="NPMDICMPV6DestinationUnreachable" protocol="icmpv6:1,any" dir=in action=allow
netsh advfirewall firewall add rule name="NPMDICMPV4TimeExceeded" protocol="icmpv4:11,any" dir=in action=allow
netsh advfirewall firewall add rule name="NPMDICMPV6TimeExceeded" protocol="icmpv6:3,any" dir=in action=allow
```


Si vous avez l’intention toouse hello protocole TCP, vous devez tooopen les ports de pare-feu pour ces tooensure ordinateurs agents capable de communiquer. Vous devez toodownload et puis exécutez hello [EnableRules.ps1 PowerShell script](https://gallery.technet.microsoft.com/OMS-Network-Performance-04a66634) sans aucun paramètre dans une fenêtre PowerShell avec des privilèges d’administrateur.

script de Hello crée des clés de Registre requises par hello moniteur de performances réseau et crée le pare-feu Windows de connexions TCP toocreate règles tooallow agents entre eux. les clés de Registre Hello créés par un script de hello également spécifient si toolog hello déboguer des journaux et chemin d’accès de hello pour les fichiers de journaux hello. Il définit également les ports TCP de l’agent hello utilisé pour la communication. les valeurs Hello pour ces clés sont définies automatiquement par script de hello, donc vous ne devez pas modifier manuellement ces clés.

port Hello ouverte par défaut est 8084. Vous pouvez utiliser un port personnalisé en fournissant le paramètre hello `portNumber` toohello script. Toutefois, hello même port doit être utilisé sur tous les ordinateurs hello où le script de hello est exécutée.

> [!NOTE]
> Hello EnableRules.ps1 script configure des règles de pare-feu Windows uniquement sur un ordinateur hello où le script de hello est exécutée. Si vous avez un pare-feu de réseau, il se peut que vous devez vous assurer qu’il permet le trafic destiné au port TCP de hello utilisé par le moniteur de performances réseau.
>
>

## <a name="configuring-hello-solution"></a>Configuration de solution de hello
Utilisez hello suivant tooinstall des informations et configurer une solution de hello.

1. Hello solution d’analyse des performances réseau récupère les données des ordinateurs exécutant Windows Server 2008 SP 1 ou version ultérieure ou Windows 7 SP1 ou version ultérieure, qui sont hello même spécifications sous la forme hello Microsoft Monitoring Agent (MMA). Des agents de la solution Analyseur de performances réseau peuvent également s’exécuter sur les systèmes d’exploitation clients/de bureau Windows (Windows 10, Windows 8.1, Windows 8 et Windows 7).
    >[!NOTE]
    >agents Hello pour les systèmes d’exploitation Windows server prend en charge les protocoles TCP et ICMP comme des protocoles hello pour une transaction synthétique. Toutefois, les agents de hello pour les systèmes d’exploitation clients Windows prennent uniquement en charge ICMP en tant que protocole hello pour une transaction synthétique.

2. Ajouter l’espace de travail tooyour hello pour l’Analyseur de performances réseau solution à partir de [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.NetworkMonitoringOMS?tab=Overview) ou à l’aide de hello est décrite dans [solutions Analytique de journal ajouter à partir de la galerie des Solutions de hello](log-analytics-add-solutions.md).  
   ![Symbole de l’Analyseur de performances réseau](./media/log-analytics-network-performance-monitor/npm-symbol.png)
3. Dans le portail OMS hello, vous verrez une nouvelle vignette intitulée **analyse des performances réseau** avec le message de type hello *Solution nécessite une configuration supplémentaire*. Vous devez tooconfigure hello solution tooadd des réseaux basés sur des sous-réseaux et les nœuds qui sont découverts par les agents. Cliquez sur **analyse des performances réseau** toostart de la configuration réseau par défaut de hello.  
   ![La solution nécessite une configuration supplémentaire](./media/log-analytics-network-performance-monitor/npm-config.png)

### <a name="configure-hello-solution-with-a-default-network"></a>Configurer une solution de hello avec un réseau par défaut
Sur la page de configuration hello, vous verrez un seul réseau nommé **par défaut**. Lorsque vous n’avez pas défini tous les réseaux, tous les sous-réseaux détectés automatiquement de hello sont placés dans le réseau par défaut de hello.

Chaque fois que vous créez un réseau, vous ajoutez un tooit de sous-réseau et que le sous-réseau est supprimé de réseau par défaut de hello. Si vous supprimez un réseau, tous les sous-réseaux de son sont automatiquement retournés réseau par défaut de toohello.

En d’autres termes, le réseau par défaut de hello est conteneur hello pour tous les sous-réseaux hello qui ne sont pas contenues dans n’importe quel réseau définies par l’utilisateur. Impossible de modifier ou de supprimer le réseau par défaut de hello. Il reste toujours dans le système de hello. En revanche, vous pouvez créer autant de réseaux que nécessaire.

Dans la plupart des cas, seront disposés dans un réseau de plusieurs sous-réseaux hello dans votre organisation et vous devez en créer une ou plusieurs réseaux toologically de sous-réseaux de votre groupe.

### <a name="create-new-networks"></a>Créer des réseaux
Dans l’Analyseur de performances réseau, un réseau est un conteneur de sous-réseaux. Vous pouvez créer un réseau avec n’importe quel nom que vous souhaitez et ajoutez des sous-réseaux toohello réseau. Par exemple, vous pouvez créer un réseau nommé *Building1* et ajouter des sous-réseaux, ou vous pouvez créer un réseau nommé *DMZ* , puis ajoutez tous les sous-réseaux appartenant toodemilitarized toothis réseau.

#### <a name="toocreate-a-new-network"></a>toocreate un nouveau réseau
1. Cliquez sur **ajouter réseau** puis tapez le nom de réseau hello et une description.
2. Sélectionnez un ou plusieurs sous-réseaux, puis cliquez sur **Ajouter**.
3. Cliquez sur **enregistrer** configuration de hello toosave.  
   ![Ajouter un réseau](./media/log-analytics-network-performance-monitor/npm-add-network.png)

### <a name="wait-for-data-aggregation"></a>Attendre l’agrégation de données
Une fois que vous avez enregistré la configuration hello pour la première fois, les solutions hello commence à collecter des informations de perte et la latence du paquet réseau entre les nœuds hello dans lequel les agents sont installés. Ce processus peut prendre du temps, parfois plus de 30 minutes. Au cours de cet état, une vignette de moniteur de performances réseau hello dans la page Vue d’ensemble de hello affiche un message indiquant *agrégation des données dans le processus*.

![Agrégation des données en cours](./media/log-analytics-network-performance-monitor/npm-aggregation.png)

Lorsque les données de salutation a été téléchargées, vous verrez hello moniteur de performances réseau mis à jour de mosaïque affichant les données.

![Vignette Analyseur de performances réseau](./media/log-analytics-network-performance-monitor/npm-tile.png)

Cliquez sur le tableau de bord de l’Analyseur de performances réseau hello vignette tooview hello.

![Tableau de bord de l’Analyseur de performances réseau](./media/log-analytics-network-performance-monitor/npm-dash01.png)

### <a name="edit-monitoring-settings-for-subnets"></a>Modifier les paramètres d’analyse pour les sous-réseaux
Tous les sous-réseaux où au moins un agent a été installé sont répertoriés sur hello **sous-réseaux** onglet dans la page de configuration hello.

#### <a name="tooenable-or-disable-monitoring-for-particular-subnetworks"></a>tooenable ou la désactivation de la surveillance pour les sous-réseaux particuliers
1. Toohello suivant de hello activez ou désactivez case **ID de sous-réseau** et vérifiez que **utilisé pour la surveillance** est sélectionné ou effacé, le cas échéant. Vous pouvez activer ou désactiver plusieurs sous-réseaux. Lorsque désactivé, les sous-réseaux ne sont pas contrôlés car les agents hello sera mis à jour toostop autres agents exécutant la commande ping.
2. Choisissez les nœuds hello que vous souhaitez toomonitor pour un sous-réseau spécifique en sélectionnant un sous-réseau de hello à partir de la liste de hello et le déplacement de hello nœuds requis entre les listes hello contenant des nœuds non contrôlées et surveillés.
   Vous pouvez ajouter une personnalisée **description** toohello de sous-réseau, si vous le souhaitez.
3. Cliquez sur **enregistrer** configuration de hello toosave.  
   ![Modifier un sous-réseau](./media/log-analytics-network-performance-monitor/npm-edit-subnet.png)

### <a name="choose-nodes-toomonitor"></a>Choisissez les nœuds toomonitor
Tous les nœuds de hello qui disposent d’un agent installé sur ces derniers sont répertoriés dans hello **nœuds** onglet.

#### <a name="tooenable-or-disable-monitoring-for-nodes"></a>tooenable ou la désactivation de la surveillance pour les nœuds
1. Activez ou désactivez les nœuds hello que vous souhaitez toomonitor ou arrêtez l’analyse.
2. Cliquez sur **Utiliser pour la surveillance** ou désactivez cette option selon le cas.
3. Cliquez sur **Enregistrer**.  
   ![Activer l’analyse du nœud](./media/log-analytics-network-performance-monitor/npm-enable-node-monitor.png)

### <a name="set-monitoring-rules"></a>Définir les règles d’analyse
Analyse des performances réseau génère les événements de contrôle d’intégrité sur la connectivité hello entre une paire de nœuds ou de liens de sous-réseau ou réseau lorsqu’un seuil est dépassé. Ces seuils peuvent être appris automatiquement par le système de hello ou vous pouvez configurer les règles d’alerte personnalisés.

Hello *règle par défaut* est créé par le système de hello et crée un événement de contrôle d’intégrité chaque fois que la perte ou la latence entre n’importe quelle paire de réseaux ou sous-réseau lie le seuil d’apprises système hello violations. Vous pouvez choisir une règle de valeur par défaut toodisable hello et créer des règles d’analyse personnalisées

#### <a name="toocreate-custom-monitoring-rules"></a>toocreate personnalisé des règles de surveillance
1. Cliquez sur **ajouter une règle** Bonjour **moniteur** onglet et entrez le nom de la règle hello et une description.
2. Sélectionnez paire hello du réseau ou sous-réseau toomonitor de liens à partir des listes de hello.
3. Tout d’abord sélectionnez réseau hello dans le hello premier sous-réseau/s d’intérêt est contenu à partir de la liste déroulante de hello réseau, puis hello sous-réseau/s à partir de la liste déroulante de sous-réseau correspondant hello.
   Sélectionnez **tous les sous-réseaux** si vous souhaitez toomonitor tous hello sous-réseaux dans une liaison réseau. De même, sélectionnez hello autres sous-réseau/s d’intérêt. Vous pouvez cliquer sur **ajouter une Exception** tooexclude d’analyse pour le sous-réseau spécifique des liens de sélection de hello vous avez apportées.
4. Choisissez entre le protocole ICMP et le protocole TCP pour l’exécution des transactions synthétiques.
5. Si vous ne souhaitez pas toocreate les événements de contrôle d’intégrité pour les éléments hello que vous avez sélectionné, puis désactivez **activer le contrôle d’intégrité sur les liens hello couvertes par cette règle**.
6. Choisissez les conditions d’analyse.
   Vous pouvez définir des seuils personnalisés pour la génération d’événements d’intégrité en tapant des valeurs de seuil. Chaque fois que la valeur de hello de condition de hello est supérieure au seuil sélectionné pour la paire de réseau/sous-réseau sélectionné hello, un événement de contrôle d’intégrité est généré.
7. Cliquez sur **enregistrer** configuration de hello toosave.  
   ![Créer un règle d’analyse personnalisée](./media/log-analytics-network-performance-monitor/npm-monitor-rule.png)

Vous pouvez intégrer la règle d’analyse que vous avez enregistrée à Gestion des alertes en cliquant sur **Créer une alerte**. Une règle d’alerte est automatiquement créée avec la requête de recherche hello et autres requises paramètres renseignés automatiquement. À l’aide d’une règle d’alerte, vous pouvez recevoir les alertes par courrier électronique, en plus des alertes de toohello existantes au sein de NPM. Les alertes peuvent également déclencher des actions correctives avec les runbooks ou elles peuvent s’intégrer aux solutions existantes de gestion des services à l’aide des webhooks. Vous pouvez cliquer sur **gérer une alerte** paramètres d’alerte tooedit hello.

### <a name="choose-hello-right-protocol-icmp-or-tcp"></a>Choisissez hello droite ICMP protocol ou TCP

Analyse des performances réseau (NPM) utilise des métriques de performances réseau des transactions synthétiques toocalculate comme pour la latence de lien et de perte de paquets. toounderstand cela mieux, envisagez fin NPM agent connecté tooone d’une liaison réseau. Cette NPM agent envoie sonde paquets tooa deuxième NPM agent tooanother connecté fin de réseau de hello. Hello deuxième agent répond avec les paquets de réponse. Ce processus est répété plusieurs fois. En mesurant le nombre hello de réponses et durée tooreceive chaque réponse, premier d’agent NPM hello évalue la latence de liaison et supprime des paquets.

Hello format, la taille et la séquence de ces paquets est déterminée par hello protocole que vous choisissez lorsque vous créez des règles d’analyse. Selon le protocole de paquets hello, hello les périphériques réseau intermédiaires (routeurs, commutateurs, etc.) peut traiter ces paquets différemment. Par conséquent, votre choix de protocole affecte précision hello des résultats de hello. Et votre choix de protocole détermine également si vous devez prendre toutes les étapes manuelles après avoir déployé la solution NPM hello.

NPM offre que Hello de choix entre les protocoles ICMP et TCP pour l’exécution de transactions synthétiques.
Si vous choisissez ICMP lorsque vous créez une règle de transaction synthétique, les agents NPM hello utilisent latence du réseau ICMP ECHO messages toocalculate hello et une perte de paquets. Hello d’utilise d’écho ICMP même message envoyé par utilitaire Ping classique de hello. Lorsque vous utilisez TCP comme protocole de hello, agents NPM envoient le paquet TCP SYN réseau hello. Elle est suivie par une négociation TCP fin et en supprimant ensuite la connexion hello à l’aide de paquets RST.

#### <a name="points-tooconsider-before-choosing-hello-protocol"></a>Tooconsider points avant de choisir le protocole de hello
Tenez compte des hello informations suivantes avant de choisir un toouse de protocole :

##### <a name="discovering-multiple-network-routes"></a>Détection de plusieurs routages réseau
TCP est plus précis dans le cadre de la détection de plusieurs routages et nécessite moins d’agents dans chaque sous-réseau. Par exemple, un ou deux agents utilisant TCP peuvent détecter tous les chemins redondants entre les sous-réseaux. Toutefois, vous avez besoin de plusieurs agents à l’aide des résultats similaires ICMP tooachieve. Avec ICMP, si vous avez *N* routages entre deux sous-réseaux, il vous faut plus de 5*N* agents dans un sous-réseau source ou de destination.

##### <a name="accuracy-of-results"></a>Précision des résultats
Routeurs et commutateurs ont tendance tooassign tooICMP ECHO paquets comparées tooTCP paquets à faible priorité. Dans certaines situations, lorsque des périphériques réseau sont très chargés, hello obtenu par le protocole TCP plus étroitement reflètent une perte de hello et latence rencontrés par les applications. Cela se produit, car la plupart du trafic d’application hello diffusées via TCP. Dans ce cas, ICMP fournit moins précis tooTCP de résultats comparés.

##### <a name="firewall-configuration"></a>Configuration du pare-feu
Protocole TCP nécessite que les paquets TCP sont envoyées tooa le port de destination. port par défaut de Hello utilisé par les agents NPM est 8084, cependant, vous pouvez le modifier quand vous configurez des agents. Par conséquent, vous devez tooensure que votre pare-feu réseau ou les règles du groupe de sécurité réseau (dans Azure) sont autorisant le trafic sur le port hello. Vous devez également toomake assurer que le pare-feu local hello sur les ordinateurs hello dans lequel les agents sont installés est configuré trafic tooallow sur ce port.

Vous pouvez utiliser les règles de pare-feu de tooconfigure des scripts PowerShell sur vos ordinateurs qui exécutent Windows, toutefois vous devez tooconfigure votre pare-feu réseau manuellement.

Contrairement à TCP, le protocole ICMP n’utilise pas de port. Dans la plupart des scénarios d’entreprise, le trafic ICMP est autorisé par le biais tooallow de pare-feux hello outils de diagnostic réseau toouse que hello utilitaire Ping. Par conséquent, si vous pouvez tester un ordinateur à partir d’un autre, vous pouvez utiliser le protocole ICMP hello sans avoir tooconfigure pare-feu manuellement.

> [!NOTE]
> Au cas où vous ne savez pas quel toouse de protocole, choisissez toostart ICMP avec. Si vous n’êtes pas satisfait des résultats de hello, vous pouvez toujours passer tooTCP plus tard.


#### <a name="how-tooswitch-hello-protocol"></a>Comment tooswitch hello protocole

Si vous avez choisi toouse ICMP durant le déploiement, vous pouvez basculer tooTCP à tout moment en modifiant la règle d’analyse de la valeur par défaut hello.

##### <a name="tooedit-hello-default-monitoring-rule"></a>règle d’analyse par défaut hello tooedit
1.  Accédez trop**des performances réseau** > **moniteur** > **configurer** > **analyse** puis cliquez sur **règle par défaut**.
2.  Faites défiler toohello **protocole** section et sélectionnez le protocole hello que vous souhaitez toouse.
3.  Cliquez sur **enregistrer** paramètre hello de tooapply.

Même si la règle par défaut de hello est à l’aide d’un protocole spécifique, vous pouvez créer des règles avec un autre protocole. Vous pouvez même créer une combinaison de règles où certaines des règles de hello utiliseraient ICMP, un autre utilise TCP.




## <a name="data-collection-details"></a>Détails sur la collecte de données
Analyse des performances réseau utilise des paquets de négociation TCP SYN SYNACK-accusé de réception lorsque TCP est choisi et réponse d’écho ICMP écho ICMP lorsque ICMP est choisi comme hello protocole toocollect perte et la latence d’informations. Traceroute est également des informations sur la topologie tooget utilisé.

Hello tableau suivant répertorie les méthodes de collecte de données et d’autres détails sur la façon dont les données sont collectées pour l’analyse des performances réseau.

| plateforme | Agent direct | Agent SCOM | Stockage Azure | SCOM requis ? | Données de l’agent SCOM envoyées via un groupe d’administration | fréquence de collecte |
| --- | --- | --- | --- | --- | --- | --- |
| Windows | &#8226; | &#8226; |  |  |  |Liaisons TCP/Messages ICMP ECHO toutes les 5 secondes, données envoyées toutes les 3 minutes |

solution de Hello utilise le contrôle d’intégrité de transactions synthétiques tooassess hello du réseau de hello. Agents OMS installés à différents points dans les paquets hello réseau exchange TCP ou d’écho ICMP (selon le protocole de hello sélectionné pour l’analyse) avec l’autre. Dans le processus de hello, agents Découvrez hello aller-retour temps et paquet perte, le cas échéant. Périodiquement, chaque agent effectue également un itinéraire de trace tooother toofind agents que tous hello différents itinéraires réseau hello qui doit être testée. À l’aide de ces données, les agents hello peuvent déduire la latence réseau hello et chiffres de perte de paquets. tests de Hello sont répétés toutes les cinq secondes et les données sont agrégées pour une période de trois minutes par les agents de hello avant de le télécharger service de journal Analytique toohello.

> [!NOTE]
> Bien que les agents de communiquer entre eux, souvent, ils ne génèrent pas un trafic réseau important lors des tests de hello. Agents dépendent uniquement une perte de TCP SYN SYNACK-accusé de réception de la négociation paquets toodetermine hello et latence--aucune donnée, les paquets sont échangés. Pendant ce processus, les agents communiquent avec d’autres uniquement si nécessaire et la topologie de communication de l’agent hello est optimisée tooreduce du trafic réseau.
>
>

## <a name="using-hello-solution"></a>À l’aide de la solution de hello
Cette section décrit toutes les fonctions de tableau de bord hello et comment toouse les.

### <a name="solution-overview-tile"></a>Vignette Vue d’ensemble de la solution
Après avoir activé la solution d’analyse des performances réseau hello, vignette de solution hello sur la page de vue d’ensemble d’OMS hello fournit une vue d’ensemble rapide de l’intégrité du réseau hello. Il affiche un graphique en anneau montrant le numéro de hello de liens de sous-réseau corrects et incorrects. Lorsque vous cliquez sur la vignette de hello, il ouvre le tableau de bord de solution hello.

![Vignette Analyseur de performances réseau](./media/log-analytics-network-performance-monitor/npm-tile.png)

### <a name="network-performance-monitor-solution-dashboard"></a>Tableau de bord de la solution l’Analyseur de performances réseau
Hello **réseau Résumé** panneau affiche un résumé des réseaux hello, ainsi que leur taille relative. Elle est suivie de mosaïques affichant le nombre total de liaisons de réseau, des liens de sous-réseau et chemins d’accès dans le système hello (un chemin d’accès se compose d’adresses IP de hello de deux hôtes avec des agents et tous les sauts de hello entre eux).

Hello **premiers événements de contrôle d’intégrité réseau** panneau fournit une liste des événements de contrôle d’intégrité les plus récents et les alertes dans le système de hello et l’heure de hello, étant donné que les événements hello a été active. Un événement d’état ou d’une alerte est générée chaque fois qu’une perte de paquets hello ou une latence d’un lien réseau ou sous-réseau dépasse un seuil.

Hello **les liens réseau défectueux haut** panneau affiche la liste des liens réseau défectueux. Voici des liens réseau hello présentant un ou plusieurs événements de contrôle d’intégrité négatifs sur les moment hello.

Hello **en haut des liens de sous-réseau avec perte de plus** et **liens de sous-réseau avec une latence plus** panneaux afficher les liens de sous-réseau supérieure hello par une perte de paquets et premiers liens de sous-réseau à la latence, respectivement. Une latence élevée ou des pertes de paquets pourraient être attendues sur certaines liaisons réseau. Ces liens apparaissent dans les listes des dix premiers hello mais ne sont pas marqué comme étant défectueux.

Hello **requêtes courantes** panneau contient un ensemble de requêtes de recherche qui extraient réseau raw directement les données de surveillance. Vous pouvez utiliser ces requêtes comme point de départ pour créer vos propres requêtes de génération de rapports personnalisés.

![Tableau de bord de l’Analyseur de performances réseau](./media/log-analytics-network-performance-monitor/npm-dash01.png)

### <a name="drill-down-for-depth"></a>Explorer en profondeur
Vous pouvez cliquer sur les différents liens de hello solution du tableau de bord toodrill déroulante plus profond dans une zone d’intérêt. Par exemple, lorsque vous voyez une alerte ou un lien réseau défectueux s’affichent dans le tableau de bord hello, vous pouvez cliquer dessus tooinvestigate davantage. Vous serez dirigé tooa page qui répertorie tous les liens de sous-réseau hello pour le lien de réseau particulier hello. Vous serez toosee en mesure de hello perte, latence état et de contrôle d’intégrité de chaque lien de sous-réseau et rapidement trouver les liens de sous-réseau sont problème hello. Vous pouvez ensuite cliquer sur **afficher les liens de nœud** toosee lier de tous les liens de nœud hello pour le sous-réseau défectueux de hello. Ensuite, vous pouvez voir les liens de nœud à l’autre et obtenir des liens de nœud défectueux hello.

Vous pouvez cliquer sur **View topology** topologie de saut par saut hello tooview des itinéraires de hello entre les nœuds source et de destination hello. Hello itinéraires défectueux ou sauts sont affichés en rouge afin que vous puissiez rapidement identifier la partie spécifique du tooa hello problème de réseau de hello.

![Explorer les données en détail](./media/log-analytics-network-performance-monitor/npm-drill.png)

### <a name="network-state-recorder"></a>Enregistreur de l’état du réseau

Chaque vue affiche une capture instantanée de l’intégrité de votre réseau à un moment précis dans le temps. Par défaut, l’état le plus récent hello est indiqué. barre de Hello en hello haut hello affiche hello point dans le temps pour lequel état de hello est affiché. Vous pouvez choisir toogo en temps et vue instantané hello de l’intégrité de votre réseau en cliquant sur la barre de hello sur **Actions**. Vous pouvez également choisir de tooenable ou désactiver l’actualisation automatique pour n’importe quelle page pendant que vous affichez l’état le plus récent hello.

![état du réseau](./media/log-analytics-network-performance-monitor/network-state.png)

#### <a name="trend-charts"></a>Graphiques de tendances
À chaque niveau que vous avez Zoom, vous pouvez voir les tendances hello de perte et la latence pour une liaison de réseau. Des graphiques de tendances sont également disponibles pour les liens de sous-réseau et de nœud. Vous pouvez modifier l’intervalle de temps hello pour hello graphique tooplot à l’aide du contrôle au moment de hello haut hello du graphique de hello.

Graphiques de tendances montrent une perspective historique des performances hello d’une liaison réseau. Des problèmes réseau sont temporaires et seraient toocatch dur en consultant état actuel de hello du réseau de hello. Il s’agit, car les problèmes peuvent rapidement de surface et disparaissent avant toute personne Remarques uniquement tooreappear à un moment ultérieur dans le temps. Ces problèmes temporaires peuvent également être difficiles pour les administrateurs de l’application, car celles émet souvent surface comme inexpliqués augmente dans le temps de réponse application, même si tous les composants de l’application s’affichent correctement toorun.

Vous pouvez facilement détecter ces types de problèmes en examinant un graphique de tendance où le problème de hello apparaît comme un pic soudain une perte de latence ou un paquet réseau.

![Graphique de tendances](./media/log-analytics-network-performance-monitor/npm-trend.png)

#### <a name="hop-by-hop-topology-map"></a>Carte topologique tronçon par tronçon
Affiche l’Analyseur de performances vous hello topologie saut par saut des itinéraires entre deux nœuds sur un mappage de topologie interactive du réseau. Vous pouvez afficher hello topologique en sélectionnant un nœud de lien, puis cliquez sur **topologie de la vue**. En outre, vous pouvez afficher la carte topologique de hello en cliquant sur **chemins** vignette sur le tableau de bord hello. Lorsque vous cliquez sur **chemins d’accès** sur le tableau de bord hello, vous aurez tooselect hello nœuds source et de destination à partir du Panneau de gauche hello, puis cliquez sur **tracer** tooplot les itinéraires de hello entre les nœuds de hello deux.

carte topologique de Hello affiche le nombre d’itinéraires sont hello entre les deux nœuds et les chemins d’accès hello prennent des paquets de données. Goulots d’étranglement des performances réseau sont marqués en rouge sur la carte de topologie hello. Vous pouvez rechercher une connexion réseau défectueux ou un périphérique réseau défectueux en examinant les éléments de couleur rouges sur la carte de topologie hello.

Lorsque vous cliquez sur un nœud ou un pointage dessus sur la carte de topologie hello, vous verrez les propriétés hello du nœud hello comme nom de domaine complet et l’adresse IP. Cliquez sur un toosee saut s’adresse IP. Vous pouvez choisir toofilter itinéraires particuliers à l’aide de filtres de hello dans volet réductible hello. Et, vous pouvez également simplifier les topologies de réseau hello en masquant les sauts intermédiaires hello à l’aide du curseur de hello dans le volet d’actions hello. Vous pouvez zoom dans ou hors du mappage de topologie hello à l’aide de la roulette de votre souris.

Notez cette topologie hello indiquée dans le mappage de hello est la topologie de couche 3 et ne contient pas de connexions et les périphériques de couche 2.

![Carte topologique tronçon par tronçon](./media/log-analytics-network-performance-monitor/npm-topology.png)

#### <a name="fault-localization"></a>Localisation des erreurs
Analyse des performances réseau est goulots d’étranglement du réseau en mesure de toofind hello sans connexion toohello les périphériques réseau. Selon les données hello collectées à partir du réseau de hello et en appliquant des algorithmes avancés sur le graphique de réseau hello, analyse des performances réseau rend une estimation PROBABILISTE de parties hello du réseau qui sont source de hello plus probable du problème de hello.

Cette approche est goulots d’étranglement du réseau toodetermine utile hello lors de l’accès toohops n’est pas disponible car il ne nécessite pas tout toobe données rassemblée à partir de périphériques réseau de hello tels que des commutateurs ou routeurs. Cela est également utile lorsque les sauts hello entre deux nœuds ne sont pas dans votre contrôle administratif. Par exemple, les sauts de hello peut-être routeurs de fournisseur de services Internet.

### <a name="log-analytics-search"></a>Recherche Log Analytics
Toutes les données graphiquement exposée via le tableau de bord de l’Analyseur de performances réseau hello et pages de zoom est également disponible en mode natif dans la recherche de journal Analytique. Vous pouvez interroger les données hello à l’aide du langage de requête de recherche hello et créer des rapports personnalisés en exportant hello données tooExcel ou Power BI. Hello **requêtes courantes** panneau dans le tableau de bord hello a certaines requêtes utiles que vous pouvez utiliser comme point de départ pour créer vos propres requêtes et les rapports de hello.

![Requêtes de recherche](./media/log-analytics-network-performance-monitor/npm-queries.png)

## <a name="investigate-hello-root-cause-of-a-health-alert"></a>Examiner la cause première hello d’une alerte d’intégrité
Maintenant que vous avez lu sur le moniteur de performances réseau, examinons une enquête simple en cause racine hello pour un événement de contrôle d’intégrité.

1. Sur la page de vue d’ensemble de hello, vous obtenez un aperçu rapide de contrôle d’intégrité hello de votre réseau en observant hello **analyse des performances réseau** vignette. Notez que, en dehors des sous-réseaux hello 6, des liens en cours d’analyse, 2 ne sont pas intègres. Cela mérite d’être examiné. Cliquez sur le tableau de bord de solution hello vignette tooview hello.  
   ![Vignette Moniteur de performances réseau](./media/log-analytics-network-performance-monitor/npm-investigation01.png)
2. Dans l’image d’exemple hello ci-dessous, vous remarquerez qu’il existe un événement de contrôle d’intégrité un lien réseau qui n’est pas sain. Vous décidez de problème de hello tooinvestigate, puis cliquez sur hello **DMZ2-DMZ1** toofind de lien réseau out racine hello de problème de hello.  
   ![Exemple de liaison réseau défectueuse](./media/log-analytics-network-performance-monitor/npm-investigation02.png)
3. page de zoom Hello affiche tous les liens de sous-réseau hello dans **DMZ2-DMZ1** liaison réseau. Vous remarquerez que pour les deux liens de sous-réseau hello, latence de hello a dépassé le seuil de hello effectue la liaison de réseau hello défectueux. Vous pouvez également voir les tendances de latence hello de deux liens de sous-réseau hello. Vous pouvez utiliser hello durée de commande de sélection dans hello graphique toofocus hello plage de temps. Vous pouvez voir hello heure hello lorsque la latence a atteint sa pointe. Vous pouvez rechercher ultérieurement des journaux hello pour résoudre ce problème de temps période tooinvestigate hello. Cliquez sur **afficher les liens de nœud** toodrill déroulante davantage.  
   ![Exemple de liens de sous-réseau défectueux](./media/log-analytics-network-performance-monitor/npm-investigation03.png)
4. Page précédente toohello similaire, page détaillée de hello pour le lien du sous-réseau particulier hello répertorie ses liens de nœud qui le composent. Vous pouvez effectuer des actions similaires ici que vous l’avez fait à l’étape précédente de hello. Cliquez sur **View topology** topologie de hello tooview entre les nœuds de hello 2.  
   ![Exemple de liens de nœud défectueux](./media/log-analytics-network-performance-monitor/npm-investigation04.png)
5. Tous les chemins d’accès de hello entre les nœuds de hello 2 sélectionné sont tracées dans le mappage de topologie hello. Vous pouvez visualiser la topologie de saut par saut hello des itinéraires entre deux nœuds sur la carte de topologie hello. Il vous donne une vision claire des itinéraires combien existent entre deux nœuds de hello et prenez les chemins d’accès hello des paquets de données. Les goulots d’étranglement des performances du réseau sont marqués en rouge. Vous pouvez rechercher une connexion réseau défectueux ou un périphérique réseau défectueux en examinant les éléments de couleur rouges sur la carte de topologie hello.  
   ![Exemple d’affichage topologique défectueux](./media/log-analytics-network-performance-monitor/npm-investigation05.png)
6. perte de Hello, la latence et nombre de hello de sauts dans chaque chemin d’accès peuvent être examinés dans hello **Action** volet. Utilisez hello barre de défilement tooview hello détails de ces chemins d’accès non intègres.  Utilisez hello filtres tooselect hello chemins d’accès avec saut non intègre de hello afin de cette topologie hello hello uniquement pour les chemins d’accès est tracée. Vous pouvez utiliser votre toozoom de roulette de la souris dans ou en dehors de la carte de topologie hello.

   Bonjour sous image vous pouvez voir clairement hello la cause racine de hello problème zones toohello section spécifique du réseau de hello en examinant les chemins d’accès hello et sauts de couleur rouge. En cliquant sur un nœud dans le mappage de topologie hello révèle propriétés hello du nœud hello, y compris hello nom de domaine complet et l’adresse IP. En cliquant sur un tronçon montre hello adresseIP de saut de hello.  
   ![topologie défectueuse : exemple de détails d’un chemin](./media/log-analytics-network-performance-monitor/npm-investigation06.png)

## <a name="provide-feedback"></a>Fournir des commentaires

- **UserVoice** -vous pouvez publier vos idées de fonctionnalités d’analyse des performances réseau que vous souhaitez nous toowork sur. Visitez notre [page UserVoice](https://feedback.azure.com/forums/267889-log-analytics/category/188146-network-monitoring).
- **Rejoignez notre cohorte** : nous sommes toujours ravis d’accueillir de nouveaux clients dans notre cohorte. Dans le cadre de celui-ci, vous accédez en avant-première toonew fonctionnalités et aidez-nous à améliorer l’analyse des performances réseau. Si vous souhaitez y participer, répondez à cette [enquête rapide](https://aka.ms/npmcohort).

## <a name="next-steps"></a>Étapes suivantes
* [Rechercher des journaux](log-analytics-log-searches.md) tooview détaillé des enregistrements de données de performances réseau.
