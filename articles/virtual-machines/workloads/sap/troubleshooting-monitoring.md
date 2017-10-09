---
title: aaaTroubleshooting et surveillance de HANA SAP sur Azure (Instances de grande taille) | Documents Microsoft
description: "Résolvez les problèmes et surveillez SAP HANA sur Azure (grandes instances)."
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1f1cd35820e227fd99af495431cd4b826aa53600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootroubleshoot-and-monitor-sap-hana-large-instances-on-azure"></a>Comment tootroubleshoot et analyse SAP HANA (instances de grande taille) sur Azure


## <a name="monitoring-in-sap-hana-on-azure-large-instances"></a>Surveillance de SAP HANA sur Azure (grandes instances)

SAP HANA sur Azure (Instances de grande taille) n’est pas différente de n’importe quel autre déploiement IaaS, vous devez toomonitor que hello du système d’exploitation et application hello cela et comment ces consomment hello suivant des ressources :

- UC
- Mémoire
- Bande passante réseau
- Espace disque

Comme avec les Machines virtuelles Azure, vous devez toofigure indique si les classes de ressources hello susmentionnées sont suffisants, ou si ces obtient épuisées. Voici plus de détails sur chacune des différentes classes de hello :

**La consommation des ressources du processeur :** ratio de hello SAP définie pour certaines charges de travail par rapport à HANA est appliquée toomake sûr qu’il doit y avoir suffisamment toowork disponible de ressources du processeur par le biais des données hello qui sont stockées en mémoire. Néanmoins, il peut arriver où HANA consomme beaucoup d’UC à exécuter des requêtes d’échéance toomissing index ou des problèmes similaires. Cela signifie que vous devez surveiller la consommation des ressources du processeur de l’unité de grande instance HANA hello, ainsi que des ressources UC utilisée par les services HANA hello spécifiques.

**La consommation de mémoire :** est important toomonitor à partir de HANA, ainsi qu’en dehors de HANA sur l’unité de hello. Dans HANA, surveiller la façon dont les données de salutation consomme HANA alloué de la mémoire dans toostay order dans hello requis d’instructions de SAP de dimensionnement. Vous souhaitez également la consommation de mémoire de toomonitor hello grande Instance niveau toomake assurer que les logiciels supplémentaires HANA-non installé ne consomment trop de mémoire et par conséquent sont en concurrence avec HANA pour la mémoire.

**La bande passante réseau :** passerelle de réseau virtuel Azure hello est limitée de la bande passante des données en transit dans hello réseau virtuel Azure, il est donc utile toomonitor les données de salutation reçues par tous les hello machines virtuelles de Azure dans un toofigure de réseau virtuel comment fermer vous sont les limites de toohello de hello Azure référence (SKU), vous avez sélectionné la passerelle. Sur l’unité d’Instance est importante HANA hello, il fait sens toomonitor entrants et sortants le trafic réseau également et suivre tookeep de volumes hello qui sont gérés au fil du temps.

**Espace disque :** la consommation d’espace disque augmente généralement au fil du temps. Il existe plusieurs raisons à cela, les principales étant les suivantes : augmentation du volume de données, exécution de sauvegardes des journaux de transaction, stockage des fichiers de trace et création d’instantanés du stockage. Par conséquent, il est l’utilisation d’espace disque important toomonitor et gérer l’espace disque hello associé hello HANA grande Instance unité.

## <a name="monitoring-and-troubleshooting-from-hana-side"></a>Surveillance et dépannage à partir de HANA

Dans l’ordre tooeffectively analyser tooSAP de problèmes connexes HANA sur Azure (Instances de grande taille), il est utile toonarrow vers le bas hello cause d’un problème. SAP a publié une grande quantité de documentation toohelp vous.

Vous trouverez applicable FAQ tooSAP connexes HANA performances Bonjour suit les Notes SAP :

- [Note SAP #2222200 – FAQ : réseau SAP HANA](https://launchpad.support.sap.com/#/notes/2222200)
- [Note SAP #2100040 – FAQ : processeur SAP HANA](https://launchpad.support.sap.com/#/notes/0002100040)
- [Note SAP #199997 – FAQ : mémoire SAP HANA](https://launchpad.support.sap.com/#/notes/2177064)
- [Note SAP #200000 – FAQ : optimisation des performances de SAP HANA](https://launchpad.support.sap.com/#/notes/2000000)
- [Note SAP #199930 – FAQ : analyse d’E/S SAP HANA](https://launchpad.support.sap.com/#/notes/1999930)
- [Note SAP #2177064 – FAQ : incidents et redémarrage du service SAP HANA](https://launchpad.support.sap.com/#/notes/2177064)

**Alertes SAP HANA**

Dans un premier temps, vérifiez hello SAP HANA alerte le journal actuel. Dans SAP HANA Studio, accédez trop**Console d’Administration : alertes : afficher : toutes les alertes**. Cet onglet affiche toutes les alertes de SAP HANA pour valeurs spécifiques (mémoire physique disponible, l’utilisation du processeur, etc.) qui se trouvent en dehors de hello valeur minimale et maximales seuils. Par défaut, les vérifications sont effectuées automatiquement toutes les 15 minutes.

![Dans SAP HANA Studio, accédez à tooAdministration Console : alertes : afficher : toutes les alertes](./media/troubleshooting-monitoring/image1-show-alerts.png)

**UC**

Pour une alerte déclenchée en raison du paramètre de seuil tooimproper, une résolution est tooreset toohello par défaut ou une valeur de seuil plus raisonnable.

![Réinitialiser la valeur par défaut de toohello ou une valeur de seuil plus raisonnable](./media/troubleshooting-monitoring/image2-cpu-utilization.png)

Hello suivant alertes peut-être indiquer des problèmes de ressources de processeur :

- Utilisation du processeur hôte (alerte 5)
- Dernière opération de point de sauvegarde (alerte 28)
- Durée du point de sauvegarde (alerte 54)

Vous pouvez remarquer la consommation élevée de processeur sur votre base de données SAP HANA à partir de hello suivantes :

- L’alerte 5 (Utilisation du processeur hôte) est déclenchée pour l’utilisation actuelle ou passée du processeur
- Hello affiche l’utilisation du processeur sur l’écran de présentation hello

![Affiche l’utilisation du processeur sur l’écran de présentation hello](./media/troubleshooting-monitoring/image3-cpu-usage.png)

graphique de charge Hello peut afficher la consommation élevée de l’UC, ou une consommation élevée Bonjour dernières :

![graphique de charge Hello peut afficher consommation élevée de l’UC, ou une consommation élevée Bonjour précédentes](./media/troubleshooting-monitoring/image4-load-graph.png)

Une alerte déclenchée en raison de l’utilisation du processeur de toohigh peut être dû à plusieurs raisons, y compris, mais non limité à : l’exécution de certaines transactions, le chargement de données en retrait des tâches longues instructions SQL et les performances de requête non optimaux (par exemple, avec BW sur HANA cubes).

Consultez toohello [dépannage de SAP HANA : provoque connexes du processeur et les Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false) de site pour les étapes de dépannage détaillées.

**Système d’exploitation**

Une des plus importantes de hello vérifie pour SAP HANA sur Linux est toomake assurer que les Pages de grande Transparent sont désactivées, consultez [2131662 de # de la Note SAP – Transparent énorme Pages (THP) sur les serveurs SAP HANA](https://launchpad.support.sap.com/#/notes/2131662).

- Vous pouvez vérifier si les Pages énorme Transparent sont activés via hello Linux commande suivante : **cat /sys/kernel/mm/transparent\_hugepage/activé**
- Si _toujours_ est placé entre crochets, comme indiqué ci-dessous, cela signifie que les Pages de grande Transparent hello sont activés : madvise [toujours] jamais ; si _jamais_ est placé entre crochets, comme indiqué ci-dessous, cela signifie que hello Transparent Pages énormes sont désactivées : madvise toujours [jamais]

Hello après la commande Linux doit retourner la valeur nothing : **rpm - qa | grep ulimit.** Si _ulimit_ est installé, désinstallez-le immédiatement.

**Mémoire**

Vous pouvez observer ce montant hello de mémoire allouée par hello SAP HANA, base de données est plus élevée que prévu. Hello suivant les alertes indique des problèmes de mémoire :

- Utilisation de la mémoire physique de l’hôte (alerte 1)
- Utilisation de la mémoire du serveur de noms (alerte 12)
- Utilisation totale de la mémoire des tables de la banque des colonnes (alerte 40)
- Utilisation de la mémoire des services (alerte 43)
- Utilisation de la mémoire du stockage principal des tables de la banque des colonnes (alerte 45)
- Fichiers de vidage runtime (alerte 46)

Consultez toohello [dépannage de SAP HANA : problèmes de mémoire](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false) de site pour les étapes de dépannage détaillées.

**Réseau**

Consultez trop[2081065 de # SAP Remarque : résolution des problèmes de réseau de HANA SAP](https://launchpad.support.sap.com/#/notes/2081065) et effectuer des étapes dans cette Note SAP de dépannage du réseau de hello.

1. Analyse des temps d’aller-retour entre le client et le serveur.
  R : Exécuter le script SQL de hello [ _HANA\_réseau\_Clients_](https://launchpad.support.sap.com/#/notes/1969700)_._
  
2. Analysez la communication entre les nœuds.
  A. Exécutez le script SQL [_HANA\_Réseau\_Services_](https://launchpad.support.sap.com/#/notes/1969700)_._

3. Exécutez la commande Linux **ifconfig** (sortie de hello indique si les pertes de paquets sont produisent).
4. Exécutez la commande Linux **tcpdump**.

En outre, utilisez ouvrir la source de hello [IPERF](https://iperf.fr/) outil (ou similaire) toomeasure des performances de réseau véritable application.

Consultez toohello [dépannage de SAP HANA : mise en réseau des performances et des problèmes de connectivité](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false) de site pour les étapes de dépannage détaillées.

**Stockage**

À partir d’un point de vue de l’utilisateur final, une application (ou système hello dans son ensemble) s’exécute lentement, ne répond pas ou peut sembler même toohang si des problèmes avec les performances d’e/s. Bonjour **Volumes** onglet dans SAP HANA Studio, vous pouvez voir hello attaché volumes et les volumes sont utilisés par chaque service.

![Dans l’onglet de Volumes hello dans SAP HANA Studio, vous pouvez voir hello attaché volumes et les volumes sont utilisés par chaque service](./media/troubleshooting-monitoring/image5-volumes-tab-a.png)

Les volumes associés dans la partie inférieure de hello d’écran hello de que vous pouvez voir les détails hello volumes, tels que les fichiers et les statistiques d’e/s.

![Les volumes associés dans la partie inférieure de hello d’écran hello de que vous pouvez voir les détails hello volumes, tels que les fichiers et les statistiques d’e/s](./media/troubleshooting-monitoring/image6-volumes-tab-b.png)

Consultez toohello [dépannage de SAP HANA : e/s associées Causes principales et les Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false) et [dépannage de SAP HANA : disque connexes Causes principales et les Solutions](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false) de site pour les étapes de dépannage détaillées.

**Outils de diagnostic**

Effectuez une vérification d’intégrité de SAP HANA via HANA\_Configuration\_Minichecks. Cet outil signale les problèmes techniques critiques potentiels qui devraient déjà avoir déclenché une alerte dans SAP HANA Studio.

Consultez trop[1969700 de # SAP Remarque : collection d’instructions SQL pour SAP HANA](https://launchpad.support.sap.com/#/notes/1969700) et téléchargez hello SQL Statements.zip fichier joint toothat Remarque. Stockez ce fichier .zip sur le disque dur local hello.

Dans Studio SAP HANA, hello **informations système** droit Bonjour **nom** colonne et sélectionnez **instructions d’importation SQL**.

![Dans SAP HANA Studio, sur l’onglet informations de système de hello, avec le bouton droit dans la colonne de nom hello et sélectionnez Importer des instructions SQL](./media/troubleshooting-monitoring/image7-import-statements-a.png)

Sélectionnez hello SQL Statements.zip fichier stocké localement, et un dossier avec des instructions SQL correspondantes hello est importé. À ce stade, hello que nombreux différents contrôles de diagnostic peuvent être exécutés avec les instructions SQL.

Par exemple, les besoins en bande passante de réplication du système SAP HANA tootest, droit hello **la bande passante** instruction sous **réplication : la bande passante** et sélectionnez **ouvrir** dans la Console SQL.

instruction SQL complète de Hello ouvre permettant toobe de paramètres d’entrée (section modification) modifié et exécutées.

![instruction SQL complète de Hello ouvre permettant toobe de paramètres d’entrée (section modification) modifié et exécutée](./media/troubleshooting-monitoring/image8-import-statements-b.png)

Un autre exemple est avec le bouton droit sur les instructions hello sous **réplication : vue d’ensemble**. Sélectionnez **Execute** à partir du menu contextuel de hello :

![Un autre exemple est avec le bouton droit sur les instructions hello sous réplication : vue d’ensemble. Cliquez sur Exécuter à partir du menu contextuel de hello](./media/troubleshooting-monitoring/image9-import-statements-c.png)

Vous obtenez ainsi des informations qui vous aident à résoudre le problème :

![Vous obtenez ainsi des informations qui vous aident à résoudre le problème](./media/troubleshooting-monitoring/image10-import-statements-d.png)

De même hello pour HANA\_Configuration\_Minichecks et recherchez les _X_ marques Bonjour _C_ (critique) colonne.

Exemples de sortie :

**HANA\_Configuration\_MiniChecks\_Rev102.01+1** pour les vérifications SAP HANA générales.

![HANA\_Configuration\_MiniChecks\_Rev102.01+1 pour les vérifications SAP HANA générales](./media/troubleshooting-monitoring/image11-configuration-minichecks.png)

**HANA\_Services\_Overview** pour une vue d’ensemble des exécutions actuelles des services SAP HANA.

![HANA\_Services\_Overview pour une vue d’ensemble des exécutions actuelles des services SAP HANA](./media/troubleshooting-monitoring/image12-services-overview.png)

**HANA\_Services\_Statistics** pour les informations de service SAP HANA (processeur, mémoire, etc.).

![HANA\_Services\_Statistics pour les informations de service SAP HANA ](./media/troubleshooting-monitoring/image13-services-statistics.png)

**HANA\_Configuration\_vue d’ensemble\_Rev110 +** pour des informations générales sur l’instance de SAP HANA hello.

![HANA\_Configuration\_vue d’ensemble\_Rev110 + pour des informations générales sur l’instance de SAP HANA hello](./media/troubleshooting-monitoring/image14-configuration-overview.png)

**HANA\_Configuration\_paramètres\_Rev70 +** toocheck les paramètres de SAP HANA.

![HANA\_Configuration\_paramètres\_toocheck Rev70 +, paramètres de SAP HANA](./media/troubleshooting-monitoring/image15-configuration-parameters.png)

