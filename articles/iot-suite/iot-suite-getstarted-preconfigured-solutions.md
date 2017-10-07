---
title: "aaaGet main préconfiguré solutions | Documents Microsoft"
description: "Suivez ce didacticiel toolearn comment toodeploy un Azure IoT Suite solution préconfigurée."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 6ab38d1a-b564-469e-8a87-e597aa51d0f7
ms.service: iot-suite
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: a7f46023d26b08de2e8ed48c34c5066a43e3fa38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-preconfigured-solutions"></a>Prise en main des solutions hello préconfiguré

Azure IoT Suite [préconfiguré solutions] [ lnk-preconfigured-solutions] combiner plusieurs Azure IoT services toodeliver bout en bout pour les solutions qui implémentent des scénarios d’entreprise IoT. Hello *surveillance à distance* solution préconfigurée connecte tooand surveille vos appareils. Vous pouvez utiliser des flux de hello hello solution tooanalyze de données à partir de vos appareils et les résultats de l’entreprise tooimprove en rendant les processus à répondre automatiquement toothat des flux de données.

Ce didacticiel vous montre comment la surveillance à distance de tooprovision hello préconfiguré solution. Il vous guide également dans les fonctionnalités de base hello de solution de hello préconfiguré. Vous pouvez accéder à la plupart de ces fonctionnalités à partir de la solution de hello *tableau de bord* qui déploie dans le cadre de la solution de hello préconfiguré :

![Tableau de bord de solution préconfigurée de surveillance à distance][img-dashboard]

toocomplete ce didacticiel, vous avez besoin d’un abonnement Azure actif.

> [!NOTE]
> Si vous ne possédez pas de compte, vous pouvez créer un compte d’évaluation gratuit en quelques minutes. Pour plus d’informations, consultez la rubrique [Version d’évaluation gratuite d’Azure][lnk_free_trial].

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

## <a name="scenario-overview"></a>Présentation du scénario

Lorsque vous déployez hello solution préconfigurée de surveillance à distance, il est préremplie avec les ressources qui permettent de vous toostep via un scénario courant de surveillance à distance. Dans ce scénario, solution de toohello connecté plusieurs périphériques sont reporting des valeurs de température inattendue. Hello sections suivantes vous indiquent comment procéder pour :

* Identifier les périphériques hello envoyez des valeurs de température inattendu.
* Configurez ces périphériques toosend plus détaillées que les données de télémétrie.
* Résoudre les problème de hello en mettant à jour de microprogramme hello sur ces appareils.
* Vérifiez que votre action a résolu le problème de hello.

Une fonctionnalité clé de ce scénario est que vous pouvez effectuer toutes ces actions à distance à partir du tableau de bord de solution hello. Vous n’avez pas besoin d’appareils de toohello d’accès physique.

## <a name="view-hello-solution-dashboard"></a>Tableau de bord View hello solution

tableau de bord Hello solution vous permet de solution de hello déployé toomanage. Par exemple, vous pouvez afficher les données de télémétrie, ajouter des appareils et configurer des règles.

1. Lorsque l’approvisionnement hello est terminé et vignette hello pour votre solution préconfigurée indique **prêt**, choisissez **lancer** tooopen votre portail de solution de surveillance à distance dans un nouvel onglet.

    ![Lancer la solution de hello préconfiguré][img-launch-solution]

1. Par défaut, portail de solution hello affiche hello *tableau de bord*. Vous pouvez naviguer tooother des zones du portail de solution hello à l’aide du menu de hello sur la partie gauche de la page de hello hello.

    ![Tableau de bord de solution préconfigurée de surveillance à distance][img-menu]

tableau de bord Hello affiche hello informations suivantes :

* Une carte qui affiche l’emplacement hello de chaque périphérique connecté toohello solution. Lorsque vous exécutez la solution de hello pour la première fois, il existe des 25 périphériques simulés. périphériques simulés Hello sont implémentés en tant que tâches Web Azure et les solutions hello utilise hello API Bing Maps tooplot d’informations sur la carte de hello. Consultez hello [FAQ] [ lnk-faq] toolearn comment toomake hello dynamique de la carte.
* Un panneau **Historique de télémétrie** qui trace la télémétrie de l’humidité et de la température d’un appareil sélectionné en temps quasi-réel et affiche les données d’agrégation telles que l’humidité maximale, minimale et moyenne.
* Un panneau **Historique des alertes** qui affiche les alarmes récentes lorsqu’une valeur de télémétrie a dépassé un seuil défini. Vous pouvez définir vos propres alarmes dans les exemples de toohello plus créés par la solution de hello préconfiguré.
* Un panneau **Tâches** qui affiche des informations sur les travaux planifiés. Vous pouvez planifier vos propres tâches sur la page **Gestion des tâches**.

## <a name="view-alarms"></a>Afficher les alarmes

panneau d’historique Hello alarme montre que cinq appareils sont reporting supérieure à celle des valeurs de télémétrie attendu.

![Historique TODO alarme sur le tableau de bord de solution hello][img-alarms]

> [!NOTE]
> Ces alertes sont générées par une règle qui est incluse dans la solution de hello préconfiguré. Cette règle génère une alerte lorsque la valeur de la température hello envoyé par un périphérique dépasse 60. Vous pouvez définir vos propres règles et les actions en choisissant [règles](#add-a-rule) et [Actions](#add-an-action) dans le menu de gauche hello.

## <a name="view-devices"></a>Afficher les appareils

Hello *périphériques* liste affiche tous les périphériques de hello inscrit dans les solutions hello. À partir de la liste des appareils hello vous pouvez afficher et modifier les métadonnées de l’appareil, ajouter ou supprimer des appareils et appeler des méthodes sur les appareils. Vous pouvez filtrer et trier la liste hello des périphériques dans la liste des appareils hello. Vous pouvez également personnaliser les colonnes hello indiquées dans la liste des appareils hello.

1. Choisissez **périphériques** liste des appareils tooshow hello pour cette solution.

   ![Liste des appareils hello vue dans le portail de solution hello][img-devicelist]

1. liste des appareils Hello affiche initialement 25 périphériques simulés créés par le processus d’approvisionnement de hello. Vous pouvez ajouter la solution de toohello d’autres appareils simulé et physique.

1. Détails de hello tooview d’un appareil, choisissez un périphérique dans la liste des appareils hello.

   ![Afficher les détails de l’appareil hello dans le portail de solution hello][img-devicedetails]

Hello **détails de l’appareil** panneau contient six sections :

* Une collection de liens qui activent vous toocustomize hello icône périphérique, désactivez hello périphérique, ajouter une règle, appellent une méthode ou envoyant une commande. Pour voir une comparaison des commandes (messages appareil-à-cloud) et des méthodes (méthodes directes), consultez [Conseils pour les communications cloud-à-appareil][lnk-c2d-guidance].
* Hello **appareil double - balises** section vous permet de valeurs de balise tooedit pour appareil de hello. Vous pouvez afficher des valeurs de balise dans la liste des appareils hello et utilisez liste des appareils balise valeurs toofilter hello.
* Hello **appareil double - propriétés de souhaité** section vous permet de tooset propriété valeurs toobe envoyé toohello appareil.
* Hello **appareil double - a signalé des propriétés** section affiche les valeurs de propriété envoyés à partir de l’appareil de hello.
* Hello **propriétés de l’appareil** section affiche les informations de Registre des identités hello tels que le périphérique de hello clés id et l’authentification.
* Hello **travaux récents** section affiche des informations sur tous les travaux qui ont ciblés récemment cet appareil.

## <a name="filter-hello-device-list"></a>Filtrer la liste des appareils hello

Vous pouvez utiliser un filtre toodisplay que les périphériques qui envoient des valeurs de température inattendue. Hello solution préconfigurée de surveillance à distance inclut hello **appareils défectueux** filtrer les appareils tooshow avec une valeur de température moyenne supérieure à 60. Vous pouvez également [créer vos propres filtres](#add-a-filter).

1. Choisissez **ouvrir l’enregistrement de filtre** toodisplay une liste de filtres disponibles. Puis choisissez **appareils défectueux** filtre de hello tooapply :

    ![Afficher la liste hello des filtres][img-unhealthy-filter]

1. liste des appareils Hello affiche maintenant uniquement les périphériques avec une valeur de température moyenne supérieure à 60.

    ![Vue hello périphérique filtrés liste appareils défectueux][img-filtered-unhealthy-list]

## <a name="update-desired-properties"></a>Mettre à jour les propriétés souhaitées

Vous avez désormais identifié un ensemble d’appareils nécessitant une correction. Toutefois, vous décidez que la fréquence de données hello de 15 secondes n’est pas suffisant pour un diagnostic clair du problème de hello. La modification hello télémétrie fréquence toofive secondes tooprovide vous avec toobetter de points de données plus diagnostiquer les problème de hello. Vous pouvez transmettre cette configuration modification tooyour à distance les appareils à partir du portail de solution hello. Vous pouvez modifier hello qu’une seule fois, évaluer l’impact de hello et ensuite agir sur les résultats hello.

Suivez ces étapes de toorun une opération de changement de hello **TelemetryInterval** souhaité de propriété pour les appareils hello affectée. Lorsque les appareils hello réception hello nouvelle **TelemetryInterval** valeur de propriété, ils changent leurs données de télémétrie toosend configuration toutes les cinq secondes au lieu de toutes les 15 secondes :

1. Lors de l’affichage liste hello de périphériques défectueux dans la liste des appareils hello, choisissez **planificateur**, puis **double de périphérique modifier**.

1. Appelez la tâche de hello **intervalle de modification de données de télémétrie**.

1. Modifier la valeur hello hello **propriété souhaitée** nom **souhaitée. Config.TelemetryInterval** toofive secondes.

1. Choisissez **Planification**.

    ![Modifier hello TelemetryInterval propriété toofive secondes][img-change-interval]

1. Vous pouvez surveiller la progression hello du travail hello hello **des tâches de gestion** page hello portail.

> [!NOTE]
> Si vous souhaitez toochange une valeur de propriété souhaitée pour un périphérique, utilisez hello **propriétés souhaitées** section Bonjour **détails de l’appareil** Panneau de configuration au lieu d’exécuter un travail.

Cette tâche définit la valeur hello hello **TelemetryInterval** souhaité de propriété en double d’appareil hello pour tous les hello périphériques sélectionnés par le filtre de hello. les appareils de Hello récupèrent cette valeur à partir du double du périphérique hello et mettre à jour leur comportement. Quand un appareil récupère et traite une propriété spécifique à partir d’un double de l’appareil, il définit la propriété de valeur signalée hello correspondante.

## <a name="invoke-methods"></a>Appeler des méthodes

Pendant l’exécution de tâche de hello, vous remarquez dans liste hello de périphériques défectueux que tous ces périphériques disposant d’un microprogramme ancien (inférieur à la version 1.6) versions.

![Version du microprogramme pour les appareils défectueux hello a signalé l’hello de vue][img-old-firmware]

Cette version du microprogramme peut être la cause première hello de hello inattendue, car vous savez que les autres périphériques intègres ont été récemment mis à jour tooversion 2.0 des valeurs de température. Vous pouvez utiliser hello intégrée **anciens périphériques microprogramme** filtrer tooidentify tous les périphériques avec d’anciennes versions du microprogramme. À partir du portail de hello, vous pouvez ensuite à distance mettre à jour tous les appareils hello exécute toujours les anciennes versions de microprogramme :

1. Choisissez **ouvrir l’enregistrement de filtre** toodisplay une liste de filtres disponibles. Puis choisissez **anciens périphériques microprogramme** filtre de hello tooapply :

    ![Afficher la liste hello des filtres][img-old-filter]

1. liste des appareils Hello affiche maintenant uniquement les appareils avec d’anciennes versions du microprogramme. Cette liste inclut hello cinq appareils identifiés par hello **appareils défectueux** filtre et trois unités supplémentaires :

    ![Liste de périphérique filtrés hello vue affichant les anciens périphériques][img-filtered-old-list]

1. Choisissez **Planificateur de travaux**, puis **Appeler une méthode**.

1. Définissez **nom de la tâche** trop**tooversion de mise à jour de microprogramme 2.0**.

1. Choisissez **InitiateFirmwareUpdate** comme hello **méthode**.

1. Ensemble hello **FwPackageUri** paramètre trop**https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**.

1. Choisissez **Planification**. valeur par défaut Hello est désormais pour toorun de travail hello.

    ![Créer le microprogramme de hello tooupdate de travail des appareils de hello sélectionné][img-method-update]

> [!NOTE]
> Si vous souhaitez tooinvoke une méthode sur un périphérique, choisissez **méthodes** Bonjour **détails de l’appareil** Panneau de configuration au lieu d’exécuter un travail.

Ce travail appelle hello **InitiateFirmwareUpdate** méthode directe sur tous les appareils hello sélectionnés par le filtre de hello. Appareils répondent immédiatement tooIoT Hub et puis initier de façon asynchrone les processus de mise à jour de microprogramme hello. les appareils Hello fournissent les informations d’état sur le processus de mise à jour de microprogramme hello via des valeurs de propriété signalé, comme indiqué dans hello suivant des captures d’écran. Choisissez hello **Actualiser** icône tooupdate hello plus d’informations dans les listes de périphérique et la tâche hello :

![Liste de tâches montrant l’exécution de liste de mise à jour de microprogramme hello][img-update-1]
![liste des appareils montrant l’état de mise à jour de microprogramme][img-update-2]
![travail liste affichant hello microprogramme mise à jour la liste complète][img-update-3]

> [!NOTE]
> Dans un environnement de production, vous pouvez planifier des travaux toorun pendant une fenêtre de maintenance désigné.

## <a name="scenario-review"></a>Analyse du scénario

Dans ce scénario, vous identifié un problème potentiel avec certains de vos périphériques à distance à l’aide de l’historique de hello alarme sur le tableau de bord hello et un filtre. Vous les filtres utilisés hello et un tooremotely de travail configurent hello appareils tooprovide plus d’informations toohelp diagnostiquer le problème de hello. Enfin, vous avez utilisé un filtre et une maintenance tooschedule du travail sur les appareils hello affectée. Si vous retournez toohello le tableau de bord, vous pouvez vérifier qu’il n’y a n’est plus n’importe quel alarmes provenant d’appareils dans votre solution. Vous pouvez utiliser un filtre tooverify qui hello microprogramme est à jour sur tous les appareils hello dans votre solution et qu’il existe des appareils défectueux n’y a plus :

![Filtre indiquant que tous les appareils disposent d’un microprogramme à jour][img-updated]

![Filtre indiquant que tous les appareils sont sains][img-healthy]

## <a name="other-features"></a>Autres fonctionnalités

Hello sections suivantes décrivent certaines fonctionnalités de hello solution préconfigurée de surveillance à distance qui ne sont pas décrits dans le cadre du scénario précédent de hello.

### <a name="customize-columns"></a>Personnaliser les colonnes

Vous pouvez personnaliser les informations de hello affichées dans la liste des appareils hello en choisissant **éditeur colonne**. Vous pouvez ajouter et supprimer des colonnes dans lesquelles figurent des valeurs de balises et de propriétés signalées. Vous pouvez également réorganiser et renommer les colonnes :

   ![Liste des appareils colonne éditeur ion hello][img-columneditor]

### <a name="customize-hello-device-icon"></a>Personnaliser l’icône du périphérique hello

Vous pouvez personnaliser hello appareil icône est affichée dans la liste des périphériques à partir de hello hello **détails de l’appareil** panneau comme suit :

1. Choisissez Bonjour crayon icône tooopen Bonjour **modifier l’image** Panneau de configuration pour un périphérique :

   ![Ouvrir l’éditeur d’image d’appareil][img-startimageedit]

1. Soit charger une nouvelle image ou utilisez une des images existantes de hello, puis choisissez **enregistrer**:

   ![Modifier l’éditeur d’image d’appareil][img-imageedit]

1. Hello image que vous venez de sélectionner affiche Bonjour **icône** colonne pour appareil de hello.

> [!NOTE]
> image de Hello est stockée dans le stockage blob. Une balise en double d’appareil hello contient une image de toohello de lien dans le stockage d’objets blob.

### <a name="add-a-device"></a>Ajout d’un appareil

Lorsque vous déployez la solution de hello préconfiguré, vous déployez automatiquement des 25 périphériques d’exemple que vous pouvez voir dans la liste des appareils hello. Ces appareils sont des *simulations d’appareils* en cours d’exécution dans un Azure WebJob. Appareils simulés facilitent vous tooexperiment avec solution hello préconfiguré sans hello besoin toodeploy réel physique les appareils. Si vous ne souhaitez pas tooconnect une solution de toohello périphérique réel, consultez hello [connecter votre solution préconfigurée de surveillance à distance de toohello périphérique] [ lnk-connect-rm] didacticiel.

Hello étapes suivantes vous montrent comment tooadd une solution de toohello appareil simulé :

1. Parcourir la liste de périphériques de toohello précédent.

1. tooadd un appareil, choisissez **+ ajouter un périphérique** dans hello bas à gauche.

   ![Ajouter une solution toohello préconfiguré de périphérique][img-adddevice]

1. Choisissez **nouveau** sur hello **simulée de périphérique** vignette.

   ![Définir les détails du nouvel appareil dans le tableau de bord][img-addnew]

   Dans Ajout toocreating un nouvel appareil simulé, vous pouvez également ajouter un périphérique physique si vous choisissez toocreate un **personnalisé périphérique**. toolearn en savoir plus sur la connexion de périphériques physiques toohello solution, consultez [connecter votre toohello appareil IoT Suite solution préconfigurée de surveillance à distance][lnk-connect-rm].

1. Sélectionnez **Me laisser définir mon propre ID d’appareil** et ajoutez un nom unique d’ID d’appareil, par exemple **monappareil_01**.

1. Cliquez sur **Créer**.

   ![Enregistrer un nouvel appareil][img-definedevice]

1. Dans l’étape 3 de **ajouter un appareil simulé**, choisissez **fait** liste des appareils tooreturn toohello.

1. Vous pouvez afficher votre appareil **en cours d’exécution** dans la liste des appareils hello.

    ![Afficher le nouvel appareil dans la liste des appareils][img-runningnew]

1. Vous pouvez également afficher hello simulée de télémétrie à partir de votre nouveau périphérique sur le tableau de bord hello :

    ![Afficher la télémétrie du nouvel appareil][img-runningnew-2]

### <a name="disable-and-delete-a-device"></a>Désactiver et supprimer un appareil

Vous pouvez désactiver un appareil puis le supprimer :

![Désactiver et supprimer un appareil][img-disable]

### <a name="add-a-rule"></a>Ajouter une règle

Il n’existe aucune règle pour le nouveau périphérique de hello que vous venez d’ajouter. Dans cette section, vous ajoutez une règle qui déclenche une alerte lors de la température de hello signalés par hello nouveau périphérique dépasse 47 degrés. Avant de commencer, notez que l’historique des données de télémétrie hello pour le nouveau périphérique de hello sur le tableau de bord hello montre la température du périphérique hello ne dépasse jamais 45 degrés.

1. Parcourir la liste de périphériques de toohello précédent.

1. tooadd une règle pour appareil de hello, sélectionnez votre nouveau périphérique Bonjour **liste de périphériques**, puis choisissez **ajouter une règle**.

1. Créer une règle qui utilise **température** en tant que champ de données hello et utilise **AlarmTemp** comme hello lorsque la température de hello dépasse 47 degrés de sortie :

    ![Ajouter une règle d’appareil][img-adddevicerule]

1. Choisissez de vos modifications, toosave **enregistrer et afficher les règles**.

1. Choisissez **commandes** dans le volet d’informations de périphérique hello pour le nouveau périphérique de hello.

    ![Ajouter une règle d’appareil][img-adddevicerule2]

1. Sélectionnez **ChangeSetPointTemp** à partir de la liste de commandes hello et ensemble **SetPointTemp** too45. Puis choisissez **Envoyer la commande** :

    ![Ajouter une règle d’appareil][img-adddevicerule3]

1. Accédez toohello différé du tableau de bord. Après un bref laps de temps, vous verrez une nouvelle entrée Bonjour **alarme historique** volet lors de la température de hello signalé par votre nouveau périphérique dépasse le seuil de degrés 47 hello :

    ![Ajouter une règle d’appareil][img-adddevicerule4]

1. Vous pouvez consulter et modifier toutes les règles sur hello **règles** page du tableau de bord hello :

    ![Répertorier les règles d’appareil][img-rules]

1. Vous pouvez consulter et modifier toutes les actions hello qui peuvent être effectuées dans la règle de tooa de réponse sur hello **Actions** page du tableau de bord hello :

    ![Répertorier les actions d’appareil][img-actions]

> [!NOTE]
> Il est possible toodefine les actions qui peuvent envoyer un message électronique ou SMS dans la réponse tooa règle ou l’intégrer avec un système métier-via un [application logique][lnk-logic-apps]. Pour plus d’informations, consultez hello [tooyour connecter une application de logique Azure IoT Suite de l’analyse à distance de solution préconfigurée][lnk-logicapptutorial].

### <a name="manage-filters"></a>Gérer les filtres

Dans la liste des appareils hello, vous pouvez créer, enregistrer et recharger les filtres toodisplay une liste personnalisée de concentrateur tooyour connecté de périphériques. toocreate un filtre :

1. Choisissez l’icône de filtre hello modifier au-dessus de la liste des appareils hello :

    ![Éditeur de filtre hello ouvert][img-editfiltericon]

1. Bonjour **l’éditeur de filtre**, ajouter des champs de hello, d’opérateurs et de liste de valeurs toofilter hello appareil. Vous pouvez ajouter plusieurs clauses toorefine votre filtre. Choisissez **filtre** filtre de hello tooapply :

    ![Créer un filtre][img-filtereditor]

1. Dans cet exemple, la liste de hello est filtré par le fabricant et le numéro de modèle :

    ![Liste de filtrage][img-filterelist]

1. toosave votre filtre avec un nom personnalisé, choisissez hello **enregistrer en tant que** icône :

    ![Enregistrer un filtre][img-savefilter]

1. tooreapply un filtre que vous avez enregistré précédemment, choisissez hello **ouvrir l’enregistrement de filtre** icône :

    ![Ouvrir un filtre][img-openfilter]

Vous pouvez créer des filtres en fonction de l’id de l’appareil, de son état, des propriétés souhaitées, des propriétés signalées et des balises. Vous ajoutez votre propre appareil tooa de balises personnalisées Bonjour **balises** section Hello **détails de l’appareil** panneau ou exécuter un travail tooupdate des balises sur plusieurs appareils.

> [!NOTE]
> Bonjour **l’éditeur de filtre**, vous pouvez utiliser hello **vue avancée** tooedit hello texte de la requête directement.

### <a name="commands"></a>Commandes

À partir de hello **détails de l’appareil** Panneau de configuration, vous pouvez envoyer un périphérique toohello de commandes. Premier démarrage d’un périphérique, il envoie plus d’informations sur hello commandes que toohello solution prend en charge. Pour en savoir plus sur les différences de hello entre les commandes et les méthodes, consultez [options de cloud-à-appareil Azure IoT Hub][lnk-c2d-guidance].

1. Choisissez **commandes** Bonjour **détails de l’appareil** Panneau de configuration pour le périphérique sélectionné de hello :

   ![Commandes de l’appareil dans le tableau de bord][img-devicecommands]

1. Sélectionnez **PingDevice** à partir de la liste de commandes hello.

1. Choisissez **Envoyer la commande**.

1. Vous pouvez voir l’état hello de commande hello dans l’historique de commande hello.

   ![État de la commande dans le tableau de bord][img-pingcommand]

solution de Hello effectue le suivi d’état hello de chaque commande, qu'il envoie. Initialement le résultat de hello est **en attente**. Lors de l’appareil de hello signale qu’il a exécuté la commande hello, le résultat de hello est défini trop**réussite**.

## <a name="behind-hello-scenes"></a>Coulisses de hello

Lorsque vous déployez une solution préconfigurée, processus de déploiement hello crée plusieurs ressources Bonjour abonnement Azure que vous avez sélectionné. Vous pouvez afficher ces ressources Bonjour Azure [portal][lnk-portal]. processus de déploiement Hello crée un **groupe de ressources** avec un nom basé sur le nom de hello que vous choisissez pour votre solution préconfigurée :

![Solution préconfigurée Bonjour portail Azure][img-portal]

Vous pouvez afficher les paramètres de hello de chaque ressource en la sélectionnant dans la liste de hello des ressources dans le groupe de ressources hello.

Vous pouvez également afficher le code source de hello pour les solutions hello préconfiguré. Bonjour à distance le contrôle de code source de solution préconfigurée est Bonjour [azure-iot-de surveillance à distance] [ lnk-rmgithub] référentiel GitHub :

* Hello **DeviceAdministration** dossier contient le code source hello pour le tableau de bord hello.
* Hello **simulateur** dossier contient le code source hello pour les appareil simulé hello.
* Hello **EventProcessor** dossier contient le code source hello pour hello au processus principal qui gère les données de télémétrie entrants hello.

Lorsque vous avez terminé, vous pouvez supprimer la solution de hello préconfiguré à partir de votre abonnement Azure sur hello [azureiotsuite.com] [ lnk-azureiotsuite] site. Ce site vous permet de supprimer tooeasily que tous hello des ressources qui ont été configurés lors de la création de solutions de hello préconfiguré.

> [!NOTE]
> tooensure que vous supprimez tous les éléments liés toohello préconfiguré solution, supprimez-le sur hello [azureiotsuite.com] [ lnk-azureiotsuite] de site et ne supprimez pas le groupe de ressources hello dans le portail de hello.

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez déployé une solution de travail préconfiguré, vous pouvez continuer de prise en main de IoT Suite en lisant hello suivant des articles :

* [Présentation de la solution préconfigurée de surveillance à distance][lnk-rm-walkthrough]
* [Se connecter à votre solution préconfigurée de surveillance à distance de toohello périphérique][lnk-connect-rm]
* [Autorisations sur le site de azureiotsuite.com hello][lnk-permissions]

[img-launch-solution]: media/iot-suite-getstarted-preconfigured-solutions/launch.png
[img-dashboard]: media/iot-suite-getstarted-preconfigured-solutions/dashboard.png
[img-menu]: media/iot-suite-getstarted-preconfigured-solutions/menu.png
[img-devicelist]: media/iot-suite-getstarted-preconfigured-solutions/devicelist.png
[img-alarms]: media/iot-suite-getstarted-preconfigured-solutions/alarms.png
[img-devicedetails]: media/iot-suite-getstarted-preconfigured-solutions/devicedetails.png
[img-devicecommands]: media/iot-suite-getstarted-preconfigured-solutions/devicecommands.png
[img-pingcommand]: media/iot-suite-getstarted-preconfigured-solutions/pingcommand.png
[img-adddevice]: media/iot-suite-getstarted-preconfigured-solutions/adddevice.png
[img-addnew]: media/iot-suite-getstarted-preconfigured-solutions/addnew.png
[img-definedevice]: media/iot-suite-getstarted-preconfigured-solutions/definedevice.png
[img-runningnew]: media/iot-suite-getstarted-preconfigured-solutions/runningnew.png
[img-runningnew-2]: media/iot-suite-getstarted-preconfigured-solutions/runningnew2.png
[img-rules]: media/iot-suite-getstarted-preconfigured-solutions/rules.png
[img-adddevicerule]: media/iot-suite-getstarted-preconfigured-solutions/addrule.png
[img-adddevicerule2]: media/iot-suite-getstarted-preconfigured-solutions/addrule2.png
[img-adddevicerule3]: media/iot-suite-getstarted-preconfigured-solutions/addrule3.png
[img-adddevicerule4]: media/iot-suite-getstarted-preconfigured-solutions/addrule4.png
[img-actions]: media/iot-suite-getstarted-preconfigured-solutions/actions.png
[img-portal]: media/iot-suite-getstarted-preconfigured-solutions/portal.png
[img-disable]: media/iot-suite-getstarted-preconfigured-solutions/solutionportal_08.png
[img-columneditor]: media/iot-suite-getstarted-preconfigured-solutions/columneditor.png
[img-startimageedit]: media/iot-suite-getstarted-preconfigured-solutions/imagedit1.png
[img-imageedit]: media/iot-suite-getstarted-preconfigured-solutions/imagedit2.png
[img-editfiltericon]: media/iot-suite-getstarted-preconfigured-solutions/editfiltericon.png
[img-filtereditor]: media/iot-suite-getstarted-preconfigured-solutions/filtereditor.png
[img-filterelist]: media/iot-suite-getstarted-preconfigured-solutions/filteredlist.png
[img-savefilter]: media/iot-suite-getstarted-preconfigured-solutions/savefilter.png
[img-openfilter]:  media/iot-suite-getstarted-preconfigured-solutions/openfilter.png
[img-unhealthy-filter]: media/iot-suite-getstarted-preconfigured-solutions/unhealthyfilter.png
[img-filtered-unhealthy-list]: media/iot-suite-getstarted-preconfigured-solutions/unhealthylist.png
[img-change-interval]: media/iot-suite-getstarted-preconfigured-solutions/changeinterval.png
[img-old-firmware]: media/iot-suite-getstarted-preconfigured-solutions/noticeold.png
[img-old-filter]: media/iot-suite-getstarted-preconfigured-solutions/oldfilter.png
[img-filtered-old-list]: media/iot-suite-getstarted-preconfigured-solutions/oldlist.png
[img-method-update]: media/iot-suite-getstarted-preconfigured-solutions/methodupdate.png
[img-update-1]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate1.png
[img-update-2]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate2.png
[img-update-3]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate3.png
[img-updated]: media/iot-suite-getstarted-preconfigured-solutions/updated.png
[img-healthy]: media/iot-suite-getstarted-preconfigured-solutions/healthy.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-logic-apps]: https://azure.microsoft.com/documentation/services/app-service/logic/
[lnk-portal]: http://portal.azure.com/
[lnk-rmgithub]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-logicapptutorial]: iot-suite-logic-apps-tutorial.md
[lnk-rm-walkthrough]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-connect-rm]: iot-suite-connecting-devices.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-faq]: iot-suite-faq.md