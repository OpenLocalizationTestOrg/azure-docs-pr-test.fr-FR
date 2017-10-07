---
title: "aaaAzure IoT Suite connecté vue d’ensemble de la fabrique | Documents Microsoft"
description: "Obtenir une description de hello Azure IoT Suite connecté solution de fabrique préconfiguré."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: dobett
ms.openlocfilehash: 929b5ed41ef7d82c9b4480d02aa3f0db38931919
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-connected-factory-preconfigured-solution"></a>Prise en main hello connecté fabrique préconfiguré solution

Azure IoT Suite [préconfiguré solutions] [ lnk-preconfigured-solutions] combiner plusieurs Azure IoT services toodeliver bout en bout pour les solutions qui implémentent des scénarios d’entreprise IoT. Hello *fabrique connecté* solution préconfigurée connecte tooand surveille vos appareils industriels. Vous pouvez utiliser des flux de hello hello solution tooanalyze de données à partir de vos appareils et la productivité opérationnelle de toodrive et la rentabilité.

Ce didacticiel vous montre comment tooprovision hello connectées fabrique solution préconfigurée. Il vous guide également dans les fonctionnalités de base hello de solution de hello préconfiguré. Vous pouvez accéder à la plupart de ces fonctionnalités à partir de la solution de hello *tableau de bord* qui déploie dans le cadre de la solution de hello préconfiguré :

![tableau de bord de solution préconfigurée d’usine connectée][img-cf-home]

toocomplete ce didacticiel, vous avez besoin d’un abonnement Azure actif.

> [!NOTE]
> Si vous ne possédez pas de compte, vous pouvez créer un compte d’évaluation gratuit en quelques minutes. Pour plus d’informations, consultez la rubrique [Version d’évaluation gratuite d’Azure][lnk_free_trial].
> 
> 

## <a name="provision-hello-solution"></a>Solution de hello de disposition

1. Ouvrez une session sur tooazureiotsuite.com à l’aide de vos informations d’identification de compte Azure, puis cliquez sur «**+**« toocreate une solution.
2. Cliquez sur **sélectionnez** sur hello **fabrique connecté** vignette.
3. Entrez un **Nom de solution** pour votre solution préconfigurée d’usine connectée.
4. Sélectionnez hello **abonnement** et **région** vous souhaitez toouse tooprovision hello solution.
5. Cliquez sur **créer une Solution** hello toobegin processus de configuration. Ce processus dure généralement plusieurs minutes toorun.

### <a name="while-you-wait-for-hello-provisioning-process-toocomplete"></a>Alors que vous attendez hello toocomplete du processus de configuration

1. Cliquez sur la vignette hello pour votre solution avec **Provisioning** état.
2. Hello d’avis **les États de configuration** comme des services Azure sont déployés dans votre abonnement Azure.
3. Une fois la configuration terminée, modifications d’état hello trop**prêt**.
4. Cliquez sur Détails de hello toosee hello vignette de votre solution dans le volet de droite hello.

> [!NOTE]
> Si vous rencontrez des problèmes de déploiement de solution de hello préconfiguré, passez en revue [autorisations sur le site de azureiotsuite.com hello] [ lnk-permissions] et hello [connecté fabrique FAQ](iot-suite-faq-cf.md). Si les problèmes de hello persistent, créer un ticket de service sur hello [portal][lnk-portal].

Existe-t-il des détails que toosee souhaitées et qui ne sont pas répertoriés pour votre solution ? Faites-nous part de vos suggestions concernant les fonctionnalités sur [UserVoice](https://feedback.azure.com/forums/321918-azure-iot).

## <a name="scenario-overview"></a>Présentation du scénario

Lorsque vous déployez hello connecté solution préconfigurée de fabrique, il est préremplie avec les ressources qui vous permettent de toostep un scénario industrielle commune. Dans ce scénario, plusieurs fabriques connecté le rapport des solutions toohello toocompute requis de valeurs de données de hello l’efficacité globale équipement (OEE) et les indicateurs de performance clés (KPI). Hello sections suivantes vous indiquent comment procéder pour :

* Surveiller des valeurs d’usine, de lignes de production, OEE de poste et KPI
* Analyser les données de télémétrie hello générées à partir de ces appareils à l’aide de la série de temps Azure Insights
* Agir sur les problèmes de toofix d’alertes

Une fonctionnalité clé de ce scénario est que vous pouvez effectuer toutes ces actions à distance à partir du tableau de bord de solution hello. Vous n’avez pas besoin d’appareils de toohello d’accès physique.

## <a name="view-hello-solution-dashboard"></a>Tableau de bord View hello solution

tableau de bord Hello solution vous permet de solution de hello déployé toomanage. Il s’agit d’une représentation hiérarchique d’une configuration d’usine globale. Par exemple, vous pouvez afficher l’OEE et les KPI, publier de nouveaux nœuds pour la télémétrie et les alertes d’action.

1. Lorsque l’approvisionnement hello est terminé et vignette hello pour votre solution préconfigurée indique **prêt**, choisissez **lancer** tooopen votre portail de solution fabrique connecté dans un nouvel onglet.

    ![Lancer la solution de hello préconfiguré][img-launch-solution]

1. Par défaut, portail de solution hello affiche hello *tableau de bord*. zones de tooother toonavigate du portail de hello, utiliser les menus hello sur la partie gauche de la page de hello hello.

    ![Tableau de bord de solution préconfigurée d’usine connectée][cf-img-menu]

tableau de bord Hello affiche hello informations suivantes :

* A **liste de paramètres d’usine** panneau qui affiche l’état de hello, l’emplacement et configuration de production actuelle dans la solution de hello. Lorsque vous exécutez la solution de hello pour la première fois, il existe un nombre de périphériques simulés. simulation de ligne de production Hello est composée de trois serveurs OPC UA réels par ligne de production qui effectuent des tâches simulés et partagent des données. Pour plus d’informations sur OPC UA, consultez hello [connecté fabrique FAQ](iot-suite-faq-cf.md).
* A **carte** qu’emplacement de hello affiche de chaque périphérique connecté toohello solution. solution de Hello peut utiliser les informations de tooplot hello API Bing Maps sur la carte de hello. Si votre abonnement est activé pour l’API Bing Maps Enterprise, cette fonctionnalité est automatiquement utilisée. Dans le cas contraire, consultez hello [FAQ] [ lnk-faq] toolearn comment toomake hello dynamique de la carte.
* Un panneau **Alertes** qui affiche les alertes générées lorsqu’une valeur de télémétrie ou d’OEE/KPI dépasse un seuil spécifique.
* Un **l’efficacité globale équipement** Panneau de configuration qui montre les valeurs d’OEE hello d’ensemble de votre entreprise hello ou hello fabrique/production ligne/station vous visualisez. Cette valeur est issue du niveau de l’entreprise toohello mode station hello. la figure OEE Hello et ses éléments constitutifs peuvent être analysées davantage.
* **Indicateurs de Performance clés** Panneau de configuration qui affiche le nombre hello d’unités de produits et de l’énergie utilisée par l’ensemble de votre entreprise hello ou ligne de fabrique/production hello/station vous visualisez. Ces valeurs sont agrégées à partir d’un niveau de l’entreprise station vue toohello.

## <a name="view-factories"></a>Afficher les usines

Hello *fabriques* panneau affiche hello de l’emplacement géographique de toutes les fabriques de hello dans la solution de hello, leur état et la configuration actuelle de production. À partir de la liste des emplacements hello, vous pouvez naviguer toohello autres niveaux dans la hiérarchie de la solution hello. lignes Hello dans la liste de hello sont des liens hypertexte qui lient les détails des lignes de production hello à cet emplacement. Il est alors possible toodrill dans les détails de la ligne de production hello et la vue du niveau toohello station. Vous pouvez également appliquer une liste de filtres de toohello.

![Usines de la solution préconfigurée d’usine connectée][cf-img-factories] 

1. Hello **Panneau de configuration de fabrique** affiche hello liste fabrique pour cette solution.

2. liste des paramètres d’usine Hello affiche initialement les fabriques de six créés par le processus d’approvisionnement de hello. Vous pouvez ajouter la solution de toohello d’autres appareils simulé et physique.

3. Détails de hello tooview d’une fabrique, cliquez sur une ligne hello dans la liste des paramètres d’usine hello.

4. Détails de hello tooview d’une ligne de production, cliquez sur la ligne hello dans la liste de hello.

5. tooview hello publié nœuds OPC UA d’une station sur la ligne de production hello, cliquez sur la ligne dans la liste de hello hello.

6. tooview plus d’informations sur un nœud spécifique dans la console de hello, cliquez sur la ligne hello dans la liste de hello. Cette action lance le panneau de configuration hello contexte avec des visualisations de temps série Insights. Cliquez sur ces graphiques toodo une analyse plus approfondie dans un environnement hello temps série Insights de l’Explorateur.

## <a name="view-map"></a>Afficher la carte

Si votre abonnement a accès toohello API Bing Maps, hello *fabriques* carte affiche géographique hello et l’état de toutes les fabriques de hello dans les solutions hello. toodrill dans les détails d’emplacement hello, cliquez sur emplacements hello affichés sur la carte de hello.

![Carte de la solution préconfigurée d’usine connectée][cf-img-map]

## <a name="view-alerts"></a>Afficher les alertes

Hello **alerte** Panneau de configuration vous présente les alertes générées en raison tooa signalé valeur ou une valeur calculée de OEE/indicateur de performance clé dépasse son seuil configuré. Ce volet affiche les alertes à chaque niveau de hiérarchie hello, à partir de la vue globale de hello station vue toohello. alertes de Hello contient une description de l’alerte de hello, date, heure, emplacement et le nombre d’occurrences. Vous pouvez exploiter les toohello données ayant provoqué l’alerte de hello à l’aide de hello les données de série un aperçu en temps. Hello temps série Insights données sont visualisées dans hello alertes le cas échéant. Si vous êtes un administrateur, vous pouvez effectuer les actions par défaut sur les alertes hello telles que :

* Alerte de fermer hello.
* Confirmer l’alerte de hello.

Vous pouvez facultativement effectuer d’autres actions plus complexes. Par exemple, pour hello pression OPC UA nœud Hello Assembly, vous pouvez :

* Affichez des informations de support dans une page web dans une nouvelle fenêtre de navigateur.
* Limiter la cause hello d’alerte de hello en appelant une méthode OPC UA sur l’appareil de hello.
* Supprimez la disponibilité hello des actions par défaut de hello.

    ![Alertes de la solution préconfigurée d’usine connectée][cf-img-alerts]

> [!NOTE]
> Ces alertes sont générées par les règles spécifiées dans un fichier de configuration de solution de hello préconfiguré. Ces règles peuvent générer des alertes lorsque hello OEE ou des chiffres de l’indicateur de performance clé ou des valeurs de nœud de UA OPC qui dépassent leur seuil configuré.

1. Hello **panneau d’alertes** affiche hello alertes générées dans cette solution.

2. Détails de hello tooview d’une alerte, cliquez sur l’alerte hello dans Panneau de configuration hello alertes.

3. toofurther analyser les données d’alerte hello, cliquez sur le graphique des hello dans l’environnement de l’Explorateur hello panneau alerte tooopen hello série un aperçu en temps.

4. tooaddress hello alerte, plusieurs actions sont disponibles dans le panneau de configuration alerte hello. Choisir l’option appropriée de hello pour vous et cliquez sur hello exécuter bouton d’action de commande.

## <a name="view-overall-equipment-efficiency"></a>Afficher l’efficacité globale de l’équipement

Taux OEE hello l’efficacité des processus de fabrication hello à l’aide d’une clé paramètres opérationnels liés à la production. OEE est une mesure standard calculée en multipliant le taux de disponibilité hello, taux de performances et le taux de qualité de l’industrie : OEE = disponibilité x qualité des performances x.

![OEE de la solution préconfigurée d’usine connectée][cf-img-oee]

1. tooview OEE pour n’importe quel niveau de hiérarchie de hello, accédez à vue spécifique de toohello vous avez besoin. Hello OEE pour cette vue affiche dans le panneau hello avec chacun des éléments hello qui composent hello pourcentage OEE.

2. toofurther analyser hello OEE pour n’importe quel niveau de données de hiérarchie hello, cliquez sur les hello OEE, de disponibilité, de performances ou de pourcentage de la qualité. Contexte s’affiche un aperçu en temps série alimenté de visualisations qui affiche les données hello dernière heure, des dernières 24 heures et ces 7 derniers jours.

    ![Visualisation TSI de la solution préconfigurée d’usine connectée][cf-img-tsi-visualization]

3. toofurther analyser les données d’alerte hello, cliquez sur graphique hello dans Panneau de configuration alerte hello. Cette action ouvre l’environnement de l’Explorateur hello série un aperçu en temps.

    ![Explorateur TSI de la solution préconfigurée d’usine connectée][cf-img-tsi-explorer]

## <a name="view-key-performance-indicators"></a>Afficher les indicateurs de performance clés

solution de Hello fournit deux indicateurs de performance clés, *unités par heure* et *énergie utilisée en kWh*.

![KPI de la solution préconfigurée d’usine connectée][cf-img-kpi]

1. unités de tooview par heure ou de l’énergie utilisée pour n’importe quel niveau de hiérarchie de hello, accédez à vue spécifique de toohello vous avez besoin. unités Hello par heure et de l’énergie utilisée affichage dans le panneau de configuration hello.

2. unités de tooanalyze par heure ou de l’énergie utilisée pour n’importe quel niveau de hiérarchie hello en outre, cliquez sur la jauge hello Bonjour **indicateurs de Performance clés** Panneau de configuration. Contexte s’affiche avec les visualisations sous tension un aperçu en temps série qui vous tooview des données à partir de hello dernière heure, hello des dernières 24 heures et ces 7 derniers jours.

## <a name="scenario-review"></a>Analyse du scénario

Dans ce scénario, vous analysé vos valeurs fabriques OEE et indicateurs de performance clés, dans le tableau de bord hello. Vous avez puis utilisé un aperçu en temps série tooprovide plus d’informations toohelp affiner davantage les données de télémétrie hello pour toohelp OEE et indicateurs de performance clés à la détection des anomalies. Vous avez également utilisé des problèmes de tooview panneau alerte hello avec votre fabriques et que vous avez utilisé l’alerte hello tooresolve hello actions tooyou disponibles.

## <a name="other-features"></a>Autres fonctionnalités

Hello les sections suivantes décrire certaines fonctionnalités de solution de fabrique hello connecté qui ne sont pas décrites dans le scénario précédent de hello.

## <a name="apply-filters"></a>Appliquer des filtres

1. Cliquez sur hello **chevron** toodisplay une liste de filtres disponibles dans le panneau d’emplacements hello en usine ou hello alertes.

2. Panneau de configuration de filtres Hello s’affiche pour vous. 

    ![Filtres de la solution préconfigurée d’usine connectée][cf-img-alert-filter]

3. Choisissez le filtre hello dont vous avez besoin. Il est également possible tootype le texte libre dans les champs de filtre hello.

4. Hello filtre est ensuite appliqué pour vous. état de filtre Hello est également indiqué dans le tableau de bord hello via un graphique en entonnoir qui affiche les fabriques de hello et des alertes de tables.

    ![Filtres de la solution préconfigurée d’usine connectée][cf-img-alert-filter-funnel]

    > [!NOTE]
    > Un filtre actif n’affecte pas les valeurs OEE et l’indicateur de performance clé des hello affichée, elle filtre uniquement le contenu de liste hello.

5. tooclear un filtre, cliquez sur la forme d’entonnoir hello et cliquez sur filtre dans le panneau de contexte de filtre hello. Hello texte **tous les** s’affiche dans les fabriques hello et des alertes de tables.

## <a name="browse-an-opc-ua-server"></a>Parcourir un serveur OPC UA

Lorsque vous déployez la solution de hello préconfiguré, vous déployez automatiquement des serveurs OPC UA simulés auxquelles vous pouvez accéder via l’Explorateur de solutions hello. Ces serveurs sont des *serveurs OPC UA simulés*. Serveurs simulés facilitent vous tooexperiment avec solution hello préconfiguré sans hello besoin toodeploy réels des serveurs physiques. Si vous ne souhaitez pas tooconnect une solution de toohello server OPC UA réelle, consultez hello [connecter votre solution de fabrique préconfiguré OPC UA appareil toohello connecté] [ lnk-connect-cf] didacticiel.

1. Cliquez sur hello **icône de fabrique** dans la barre de navigation du tableau de bord hello.

    ![Explorateur de serveur de la solution préconfigurée d’usine connectée][cf-img-server-browser]

2. Choisissez un des serveurs de hello à partir de la liste prédéfinie de hello. Cette liste affiche les serveurs hello qui sont déployées automatiquement dans les solutions hello préconfiguré.

    ![Sélection de serveur de la solution préconfigurée d’usine connectée][cf-img-server-choice]

3. Cliquez sur **Connecter**. Une boîte de dialogue de sécurité s’affiche. Pour la simulation de hello, il est sécurisé tooclick **continuer**

4. tooexpand un des nœuds hello dans l’arborescence du serveur hello, cliquez dessus. Les nœuds qui publient des données de télémétrie sont indiqués par une coche.

    ![Arborescence de serveur de la solution préconfigurée d’usine connectée][cf-img-server-tree]

5. Cliquez sur un élément de tooread, écrire, publier ou appeler ce nœud. tooyou de Hello actions disponibles dépendent de vos autorisations et les attributs hello du nœud de hello. Hello lire option toodisplays un panneau de contexte montrant la valeur hello du nœud spécifique de hello. Hello écrire option affiche un panneau de contexte dans lequel vous pouvez entrer une nouvelle valeur. option d’appel Hello affiche un nœud où vous pouvez entrer des paramètres de hello pour l’appel de hello.

## <a name="publish-a-node"></a>Publier un nœud

Lorsque vous parcourez un *server de OPC UA simulé*, vous pouvez également choisir toopublish nouveaux nœuds. Vous pouvez analyser la télémétrie hello à partir de ces nœuds dans la solution de hello. Ces *simulée les serveurs OPC UA* rendre tooexperiment facile avec les solutions hello préconfiguré sans déployer les appareils physiques réelles.

1. Parcourir le nœud tooa Bonjour arborescence OPC UA serveur que vous souhaitez toopublish.

2. Cliquez sur le nœud de hello.

3. Choisissez **Publier**.

    ![L’usine connectée publie le nœud][cf-img-publish-node]

4. Un panneau de contexte s’affiche qui indique que hello publication a réussi. nœud de Hello apparaît dans la vue de niveau station hello avec une coche à côté de lui.

    ![Réussite de la publication de la solution préconfigurée d’usine connectée][cf-img-publish-success]

## <a name="command-and-control"></a>Commande et contrôle

fabrique de Hello connecté vous permet de commande et contrôler vos périphériques directement à partir de cloud de hello. Vous pouvez utiliser cette tooalerts toorespond de fonction générés par le périphérique de hello. Par exemple, vous pouvez envoyer un périphérique toohello de commande à partir du cloud de hello. Vous pouvez rechercher des commandes disponibles de hello Bonjour **StationCommands** nœud Bonjour arborescence du navigateur OPC UA serveurs. Dans ce scénario, vous ouvrez une soupape de version sur la station d’assembly hello d’une ligne de production de Munich. toouse hello commande fonctionnalités de contrôle, vous devez être Bonjour **administrateur** rôle pour hello préconfiguré de déploiement de solutions.

1. Parcourir toohello **StationCommands** nœud Bonjour arborescence du navigateur OPC UA serveur.

2. Choisissez la commande hello que vous souhaitez utiliser.

3. Cliquez sur le nœud de hello.

4. Choisissez **Appel**.

    ![Commande d’appel de la solution préconfigurée d’usine connectée][cf-img-call-command]

5. Un panneau de contexte s’affiche pour vous informer sur lequel la méthode que vous êtes sur toocall et les détails de paramètre s’applique.

6. Choisissez **Appel**.

    ![Contexte d’appel de la solution préconfigurée d’usine connectée][cf-img-call-context]

7. Panneau de configuration de contexte Hello est mise à jour tooinform que hello d’appel de méthode a réussi. Vous pouvez vérifier l’appel hello a réussi en lisant la valeur hello du nœud de pression de hello mis à jour en raison de l’appel de hello.

    ![Réussite de l’appel de la solution préconfigurée d’usine connectée][cf-img-call-success]


## <a name="behind-hello-scenes"></a>Coulisses de hello

Lorsque vous déployez une solution préconfigurée, processus de déploiement hello crée plusieurs ressources Bonjour abonnement Azure que vous avez sélectionné. Vous pouvez afficher ces ressources Bonjour Azure [portal][lnk-portal]. processus de déploiement Hello crée un **groupe de ressources** avec un nom basé sur le nom de hello que vous choisissez pour votre solution préconfigurée :

![Solution préconfigurée Bonjour portail Azure][img-cf-portal]

Vous pouvez afficher les paramètres de hello de chaque ressource en la sélectionnant dans la liste de hello des ressources dans le groupe de ressources hello.

Vous pouvez également afficher le code source de hello pour les solutions hello préconfiguré. Hello fabrique connecté préconfiguré solution le code source est Bonjour [azure iot-connecté-usine] [ lnk-cfgithub] référentiel GitHub :

Lorsque vous avez terminé, vous pouvez supprimer la solution de hello préconfiguré à partir de votre abonnement Azure sur hello [azureiotsuite.com] [ lnk-azureiotsuite] site. Ce site vous permet de supprimer tooeasily que tous hello des ressources qui ont été configurés lors de la création de solutions de hello préconfiguré.

> [!NOTE]
> tooensure que vous supprimez tous les éléments liés toohello préconfiguré solution, supprimez-le sur hello [azureiotsuite.com] [ lnk-azureiotsuite] site. Ne supprimez pas le groupe de ressources hello dans le portail de hello.

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez déployé une solution de travail préconfiguré, vous pouvez continuer de prise en main de IoT Suite en lisant hello suivant des articles :

* [Procédure pas à pas de la solution préconfigurée d’usine connectée][lnk-rm-walkthrough]
* [Connecter votre solution de fabrique connecté préconfiguré toohello périphérique][lnk-connect-cf]
* [Autorisations sur le site de azureiotsuite.com hello][lnk-permissions]

[img-cf-home]:media/iot-suite-connected-factory-overview/cf-dashboard.png
[img-launch-solution]: media/iot-suite-connected-factory-overview/launch-cf.png
[cf-img-menu]: media/iot-suite-connected-factory-overview/cf-dashboard-menu.png
[cf-img-factories]:media/iot-suite-connected-factory-overview/cf-dashboard-factory.png
[cf-img-map]:media/iot-suite-connected-factory-overview/cf-dashboard-map.png
[cf-img-alerts]:media/iot-suite-connected-factory-overview/cf-dashboard-alerts.png
[cf-img-oee]:media/iot-suite-connected-factory-overview/cf-dashboard-oee.png
[cf-img-kpi]:media/iot-suite-connected-factory-overview/cf-dashboard-kpi.png
[cf-img-tsi-visualization]:media/iot-suite-connected-factory-overview/cf-dashboard-tsi.png
[cf-img-tsi-explorer]:media/iot-suite-connected-factory-overview/tsi-explorer.png
[cf-img-server-browser]: media/iot-suite-connected-factory-overview/cf-dashboard-browser.png
[cf-img-server-choice]: media/iot-suite-connected-factory-overview/cf-select-server.png
[cf-img-server-tree]:media/iot-suite-connected-factory-overview/cf-server-tree.png
[cf-img-publish-node]:media/iot-suite-connected-factory-overview/cf-publish-node1.png
[cf-img-publish-success]:media/iot-suite-connected-factory-overview/cf-publish-success.png
[cf-img-call-command]:media/iot-suite-connected-factory-overview/cf-command-and-control-call.png
[cf-img-call-context]:media/iot-suite-connected-factory-overview/cf-command-and-control-call-button.png
[cf-img-call-success]:media/iot-suite-connected-factory-overview/cf-command-and-control-succeed.png
[img-cf-portal]:media/iot-suite-connected-factory-overview/cf-resource-group.png
[cf-img-alert-filter]:media/iot-suite-connected-factory-overview/cf-filter.png
[cf-img-alert-filter-funnel]:media/iot-suite-connected-factory-overview/cf-filter-funnel.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-portal]: http://portal.azure.com/
[lnk-cfgithub]: https://github.com/Azure/azure-iot-connected-factory
[lnk-rm-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[lnk-connect-cf]: iot-suite-connected-factory-gateway-deployment.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-faq]: iot-suite-faq.md