---
title: "aaaMonitor et gérer des pipelines de données - Azure | Documents Microsoft"
description: "Découvrez comment toouse hello toomonitor d’application de gestion et de surveillance et de gérer les pipelines et les fabriques de données Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: f3f07bc4-6dc3-4d4d-ac22-0be62189d578
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: spelluru
ms.openlocfilehash: 5e4ef6ec5fb8ebc9bda0be7899a39a51d58403d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-hello-monitoring-and-management-app"></a>Surveiller et gérer les pipelines Azure Data Factory à l’aide d’application de gestion et de surveillance hello
> [!div class="op_single_selector"]
> * [Utilisation du portail Azure/d’Azure PowerShell](data-factory-monitor-manage-pipelines.md)
> * [Utilisation de l’application de surveillance et gestion](data-factory-monitor-manage-app.md)
>
>

Cet article décrit comment toouse hello toomonitor d’application de surveillance et de gestion, gérer et déboguer vos pipelines de fabrique de données. Il fournit également des informations sur comment toocreate tooget informé sur les échecs des alertes. Vous pouvez commencer à utiliser à l’aide d’application hello en hello regarder suivant vidéo :

> [!NOTE]
> interface utilisateur de Hello illustré hello vidéo peut correspondre pas exactement à ce que vous voyez dans le portail de hello. Il est légèrement plus anciens, mais les concepts restent hello même. 

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-Data-Factory-Monitoring-and-Managing-Big-Data-Piplines/player]
>

## <a name="launch-hello-monitoring-and-management-app"></a>Lancer l’application de gestion et de surveillance hello
toolaunch hello moniteur et l’application de gestion, cliquez sur hello **analyse et gestion** vignette sur hello **Data Factory** Panneau de votre fabrique de données.

![Analyse de la vignette sur la page d’accueil de Data Factory hello](./media/data-factory-monitor-manage-app/MonitoringAppTile.png)

Vous devez voir hello surveillance et gestion d’application à ouvrir dans une fenêtre distincte.  

![Application de surveillance et gestion](./media/data-factory-monitor-manage-app/AppLaunched.png)

> [!NOTE]
> Si vous voyez ce navigateur hello est bloqué au niveau de « Autorisation... », désactivez hello **bloquer les cookies tiers et les données de site** --ou les conserver ce fait, créez une exception pour **login.microsoftonline.com** , puis essayez à nouveau tooopen hello application.


Dans la liste des activités Windows hello dans le volet du milieu hello, vous consultez une fenêtre d’activité pour chaque exécution d’une activité. Par exemple, si vous disposez de toutes les heures hello activité planifiée toorun de cinq heures, vous consultez cinq windows d’activité associés à des tranches de données de cinq. Si vous ne voyez pas windows d’activité dans la liste hello bas hello, procédez comme hello suivant :
 
- Hello de mise à jour **l’heure de début** et **heure de fin** filtres à Bonjour toomatch supérieur Bonjour début et fin de votre pipeline, puis cliquez sur hello **appliquer** bouton.  
- liste des activités Windows Hello n’est pas actualisée automatiquement. Cliquez sur hello **Actualiser** bouton de barre d’outils hello hello **Windows de l’activité** liste.  

Si vous n’avez un tootest d’application Data Factory ces étapes avec, hello didacticiel : [copier les données de stockage d’objets Blob tooSQL de base de données à l’aide de la fabrique de données](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

## <a name="understand-hello-monitoring-and-management-app"></a>Comprendre hello analyse et la gestion d’application
Il existe trois onglets sur hello gauche : **l’Explorateur de ressources**, **affichages analyse**, et **alertes**. premier onglet de Hello (**l’Explorateur de ressources**) est sélectionnée par défaut.

### <a name="resource-explorer"></a>Explorateur de ressources
Il affiche hello qui suit :

* l’Explorateur de ressources de Hello **arborescence** dans le volet gauche de hello.
* Hello **vue de diagramme** haut hello, dans le volet du milieu hello.
* Hello **Windows de l’activité** liste à la fin de hello dans le volet du milieu hello.
* Hello **propriétés**, **activité fenêtre Explorateur**, et **Script** onglets dans le volet de droite hello.

Dans l’Explorateur de ressources, vous consultez toutes les ressources (pipelines, des groupes de données, les services liés) dans la fabrique de données hello dans une arborescence. Lorsque vous sélectionnez un objet dans l’Explorateur de ressources :

* Hello associé à l’entité est mis en surbrillance dans la vue de diagramme de hello de fabrique de données.
* [Associés windows de l’activité](data-factory-scheduling-and-execution.md) sont mises en surbrillance dans la liste des activités Windows hello bas hello.  
* propriétés Hello de l’objet sélectionné de hello sont affichées dans la fenêtre de propriétés hello dans le volet de droite hello.
* Hello définition JSON de l’objet sélectionné de hello est indiqué, le cas échéant. Par exemple : un service lié, un jeu de données ou un pipeline.

![Explorateur de ressources](./media/data-factory-monitor-manage-app/ResourceExplorer.png)

Consultez hello [de planification et de l’exécution](data-factory-scheduling-and-execution.md) article pour plus d’informations sur les fenêtres de l’activité.

### <a name="diagram-view"></a>Vue du diagramme
Hello, vue de diagramme d’une fabrique de données fournit un volet de verre toomonitor et gérer une fabrique de données et ses composants. Lorsque vous sélectionnez une entité de la fabrique de données (jeu de données/pipeline) dans la vue de diagramme de hello :

* entité de fabrique de données Hello est sélectionnée dans la vue de l’arborescence hello.
* Hello associé à l’activité windows sont mises en surbrillance dans la liste des activités Windows hello.
* propriétés Hello de l’objet sélectionné de hello sont affichées dans la fenêtre de propriétés hello.

Lorsque le pipeline de hello est activé (pas dans un état suspendu), il est indiqué par une ligne verte :

![Pipeline en cours d’exécution](./media/data-factory-monitor-manage-app/PipelineRunning.png)

Vous pouvez suspendre, reprendre ou terminer un pipeline en la sélectionnant dans la vue de diagramme hello et à l’aide des boutons de hello sur la barre de commandes hello.

![Pause/reprise sur la barre de commandes hello](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)
 
Il existe trois boutons de barre de commandes pour le pipeline hello Bonjour vue de diagramme. Vous pouvez utiliser le pipeline de hello deuxième bouton toopause hello. Suspension ne terminer hello activités en cours d’exécution et leur permet de continuer toocompletion. troisième bouton de Hello suspend pipeline de hello et s’arrête ses activités existantes. bouton de première Hello reprend le pipeline de hello. Lorsque votre pipeline est suspendu, hello du pipeline de hello devient. Par exemple, un pipeline suspendu ressemble dans hello suivant image : 

![Pipeline suspendu](./media/data-factory-monitor-manage-app/PipelinePaused.png)

Vous pouvez sélections plusieurs pipelines de deux ou plusieurs en utilisant la touche Ctrl de hello. Vous pouvez utiliser des boutons de barre pour hello commande toopause/reprise plusieurs pipelines à la fois.

Vous pouvez également cliquer sur un pipeline toosuspend de sélectionner des options, reprendre et arrêter un pipeline. 

![Menu contextuel pour un pipeline](./media/data-factory-monitor-manage-app/right-click-menu-for-pipeline.png)

Cliquez sur hello **ouvrir pipeline** option toosee toutes les activités de hello dans le pipeline de hello. 

![Menu Ouvrir un pipeline](./media/data-factory-monitor-manage-app/OpenPipelineMenu.png)

Dans la vue du pipeline hello ouvert, vous voyez toutes les activités dans le pipeline de hello. Dans cet exemple, le pipeline ne contient qu’une seule activité : une activité de copie. 

![Pipeline ouvert](./media/data-factory-monitor-manage-app/OpenedPipeline.png)

toogo sauvegarder toohello de vue précédente, cliquez sur le nom de fabrique de données hello dans le menu de navigation hello haut hello.

Dans la vue du pipeline hello, lorsque vous sélectionnez un jeu de données de sortie ou lorsque vous déplacez votre souris sur le dataset de sortie hello, vous consultez fenêtre contextuelle d’activité Windows hello pour ce jeu de données.

![Fenêtre contextuelle d’activité Windows](./media/data-factory-monitor-manage-app/ActivityWindowsPopup.png)

Vous pouvez également cliquer sur Détails de toosee fenêtre de l’activité pour qu’il Bonjour **propriétés** fenêtre dans le volet de droite hello.

![Propriétés des fenêtres d’activité](./media/data-factory-monitor-manage-app/ActivityWindowProperties.png)

Dans le volet droit de hello, basculez toohello **activité fenêtre Explorateur** onglet toosee plus de détails.

![Explorateur de fenêtres d’activité](./media/data-factory-monitor-manage-app/ActivityWindowExplorer.png)

Vous voyez également **résolu variables** à chaque tentative d’exécution d’une activité dans hello **tentatives** section.

![Variables résolues](./media/data-factory-monitor-manage-app/ResolvedVariables.PNG)

Commutateur toohello **Script** onglet Définition de script toosee hello JSON pour l’objet sélectionné de hello.   

![Onglet Script](./media/data-factory-monitor-manage-app/ScriptTab.png)

Les fenêtres d’activité s’affichent à trois emplacements différents :

* Hello Windows activité contextuel Bonjour vue de diagramme (volet central).
* Hello Explorer de fenêtre d’activité dans le volet de droite hello.
* liste d’activités Windows Hello dans le volet du bas hello.

Dans fenêtre contextuelle d’activité Windows hello et Explorer de fenêtre d’activité, vous pouvez faire défiler toohello semaine précédente et hello semaine suivante à l’aide de hello flèches droite et gauche.

![Flèches gauche/droite de l’Explorateur de fenêtres d’activité](./media/data-factory-monitor-manage-app/ActivityWindowExplorerLeftRightArrows.png)

Bas hello hello vue de diagramme, vous voyez ces boutons : zoom avant, Zoom arrière, Zoom tooFit, effectuer un Zoom de 100 %, la mise en forme de verrou. Hello **mise en forme de verrou** bouton vous empêche de déplacer accidentellement des tables et des pipelines Bonjour vue de diagramme. L’option est activée par défaut. Vous pouvez désactiver cette option et déplacer des entités dans le diagramme de hello. Lorsque vous le désactivez, vous pouvez utiliser des pipelines et les tables de position hello derniers bouton tooautomatically. Vous pouvez également effectuer un zoom ou de sortie à l’aide de la roulette de souris hello.

![Commandes de zoom de la vue schématique](./media/data-factory-monitor-manage-app/DiagramViewZoomCommands.png)

### <a name="activity-windows-list"></a>Liste des fenêtres d’activité
liste des activités Windows Hello bas hello du volet du milieu hello affiche toutes les fenêtres d’activité pour hello dataset que vous avez sélectionné dans hello l’Explorateur de ressources ou hello vue de diagramme. Par défaut, la liste de hello est dans l’ordre décroissant, ce qui signifie que vous voyez dernière fenêtre d’activité hello haut hello.

![Liste des fenêtres d’activité](./media/data-factory-monitor-manage-app/ActivityWindowsList.png)

Cette liste n’actualise pas automatiquement, afin d’utiliser hello sur bouton Actualiser de hello barre d’outils toomanually Actualiser.  

Windows de l’activité peuvent être dans un des hello suivant des États :

<table>
<tr>
    <th align="left">État</th><th align="left">État secondaire</th><th align="left">Description</th>
</tr>
<tr>
    <td rowspan="8">En attente</td><td>ScheduleTime</td><td>temps de Hello n’a pas encore être motivée par de toorun de fenêtre d’activité hello.</td>
</tr>
<tr>
<td>DatasetDependencies</td><td>les dépendances en amont Hello ne sont pas prêts.</td>
</tr>
<tr>
<td>ComputeResources</td><td>ressources de calcul Hello ne sont pas disponibles.</td>
</tr>
<tr>
<td>ConcurrencyLimit</td> <td>Toutes les instances d’activité hello sont occupés autres fenêtres de l’activité en cours d’exécution.</td>
</tr>
<tr>
<td>ActivityResume</td><td>activité Hello est suspendue et ne peut pas exécuter windows d’activité hello jusqu'à sa reprise.</td>
</tr>
<tr>
<td>Retry</td><td>exécution de l’activité Hello est renouvelée.</td>
</tr>
<tr>
<td>Validation</td><td>La validation n’a pas encore démarré.</td>
</tr>
<tr>
<td>ValidationRetry</td><td>La validation est toobe en attente une nouvelle tentée.</td>
</tr>
<tr>
<tr>
<td rowspan="2">InProgress</td><td>Validation</td><td>La validation est en cours.</td>
</tr>
<td>-</td>
<td>fenêtre d’activité Hello est en cours de traitement.</td>
</tr>
<tr>
<td rowspan="4">Échec</td><td>TimedOut</td><td>exécution de l’activité Hello a pris plus de temps que ce qui est autorisé par activité hello.</td>
</tr>
<tr>
<td>Canceled</td><td>fenêtre d’activité Hello a été annulée par l’utilisateur.</td>
</tr>
<tr>
<td>Validation</td><td>La validation a échoué.</td>
</tr>
<tr>
<td>-</td><td>fenêtre d’activité Hello échec toobe généré ou validé.</td>
</tr>
<td>Ready</td><td>-</td><td>fenêtre d’activité Hello est prêt à être utilisé.</td>
</tr>
<tr>
<td>Ignoré</td><td>-</td><td>fenêtre d’activité Hello n’a pas été traitée.</td>
</tr>
<tr>
<td>Aucun</td><td>-</td><td>Une fenêtre d’activité tooexist avec un état différent, mais a été réinitialisée.</td>
</tr>
</table>


Lorsque vous cliquez sur une fenêtre d’activité dans la liste de hello, vous consultez des informations à son Bonjour **l’Explorateur Windows activité** ou hello **propriétés** fenêtre sur hello droite.

![Explorateur de fenêtres d’activité](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-2.png)

### <a name="refresh-activity-windows"></a>Actualiser les fenêtres d’activité
Détails de Hello ne sont pas automatiquement actualisées, alors utilisez le bouton d’actualisation hello (hello deuxième bouton) sur la liste de windows toomanually actualisation hello activité de la barre de commandes hello.  

### <a name="properties-window"></a>Fenêtre Propriétés
fenêtre de propriétés Hello est volet le plus à droite de hello d’application de gestion et de surveillance hello.

![Fenêtre Propriétés](./media/data-factory-monitor-manage-app/PropertiesWindow.png)

Il affiche les propriétés de l’élément hello que vous avez sélectionné dans hello l’Explorateur de ressources (arborescence), vue de diagramme ou la liste des activités Windows.

### <a name="activity-window-explorer"></a>Explorateur de fenêtres d’activité
Hello **activité fenêtre Explorateur** fenêtre est en volet le plus à droite de hello d’application de gestion et de surveillance hello. Il affiche les détails de la fenêtre d’activité hello que vous avez sélectionné dans la fenêtre contextuelle d’activité Windows hello ou une liste d’activités Windows hello.

![Explorateur de fenêtres d’activité](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-3.png)

Vous pouvez basculer la fenêtre d’activité tooanother en cliquant dessus dans l’affichage du calendrier hello haut hello. Vous pouvez également utiliser les boutons flèche gauche/droite hello à fenêtres activité hello toosee supérieur hello semaine précédente ou hello semaine suivante.

Vous pouvez utiliser les boutons de barre d’outils hello dans la fenêtre d’activité hello bas volet toorerun hello ou actualiser les détails de hello dans le volet de hello.

### <a name="script"></a>Script
Vous pouvez utiliser hello **Script** hello de tooview onglet Définition JSON de hello sélectionné entity Data Factory (service lié, dataset ou pipeline).

![Onglet Script](./media/data-factory-monitor-manage-app/ScriptTab.png)

## <a name="use-system-views"></a>Utiliser les vues système
Surveillance et gestion de l’application Hello inclut les vues système intégrées (**windows d’activité récente**, **Échec de windows de l’activité**, **windows de l’activité en cours**) qui permettent de windows les activités récentes/échec/en cours de tooview de votre fabrique de données.

Commutateur toohello **affichages analyse** onglet sur la gauche hello en cliquant dessus.

![Onglet Vues de surveillance](./media/data-factory-monitor-manage-app/MonitoringViewsTab.png)

Actuellement, trois vues système sont prises en charge. Sélectionnez une option toosee récente activité windows, windows de l’activité qui a échoué ou les activités en cours d’exécution windows dans la liste des activités Windows hello (bas hello du volet du milieu hello).

Lorsque vous sélectionnez hello **windows d’activité récente** option, vous voyez toutes les fenêtres d’activité récente dans l’ordre décroissant de hello **heure de la dernière tentative**.

Vous pouvez utiliser hello **Échec de windows de l’activité** afficher toosee tout échoué de l’activité windows dans la liste de hello. Sélectionnez une fenêtre d’activité ayant échoué dans hello liste toosee plus d’informations sur elle Bonjour **propriétés** fenêtre ou hello **activité fenêtre Explorateur**. Vous pouvez également télécharger tous les journaux d’une fenêtre d’activité ayant échoué.

## <a name="sort-and-filter-activity-windows"></a>Trier et filtrer les fenêtres d’activité
Hello de modification **l’heure de début** et **heure de fin** paramètres dans windows d’activité toofilter de barre de commandes hello. Après avoir modifié l’heure de début hello et l’heure de fin, cliquez sur hello bouton suivant toohello fin heure toorefresh hello Windows de l’activité de la liste.

![Heures de début et de fin](./media/data-factory-monitor-manage-app/StartAndEndTimes.png)

> [!NOTE]
> Actuellement, toutes les heures sont au format UTC dans l’application de gestion et de surveillance hello.
>
>

Bonjour **liste activité Windows**, cliquez sur le nom hello d’une colonne (par exemple : état).

![Menu déroulant de la liste des fenêtres d’activité](./media/data-factory-monitor-manage-app/ActivityWindowsListColumnMenu.png)

Vous pouvez effectuer les suivant hello :

* Trier dans l’ordre croissant.
* Trier dans l’ordre décroissant.
* Filtrer selon une ou plusieurs valeurs (Prêt, En attente, etc.).

Lorsque vous spécifiez un filtre sur une colonne, vous voyez le bouton Filtrer hello activé pour cette colonne, ce qui indique que les valeurs hello dans la colonne de hello sont les valeurs filtrées.

![Filtrer sur une colonne de la liste des activités Windows hello](./media/data-factory-monitor-manage-app/ActivityWindowsListFilterInColumn.png)

Vous pouvez utiliser hello mêmes filtres tooclear de fenêtre indépendante. tooclear tous les filtres pour la liste activité Windows hello, cliquez sur bouton Effacer le filtre de hello sur la barre de commandes hello.

![Effacer tous les filtres de la liste des activités Windows hello](./media/data-factory-monitor-manage-app/ClearAllFiltersActivityWindowsList.png)

## <a name="perform-batch-actions"></a>Exécuter des opérations de traitement par lot
### <a name="rerun-selected-activity-windows"></a>Réexécuter les fenêtres d’activité sélectionnées
Sélectionnez une fenêtre d’activité et cliquez sur hello flèche bas pour le premier bouton de barre de commande hello, sélectionnez **réexécuter** / **réexécuter avec situés en amont dans le pipeline**. Lorsque vous sélectionnez hello **réexécuter avec situés en amont dans le pipeline** option, elle exécute à nouveau toutes les fenêtres d’activité en amont ainsi.
    ![Réexécuter une fenêtre d’activité](./media/data-factory-monitor-manage-app/ReRunSlice.png)

Vous pouvez également sélectionner plusieurs fenêtres d’activité dans la liste de hello et réexécuter à hello même temps. Vous pourriez windows d’activité toofilter basés sur l’état de hello (par exemple : **n’a pas pu**)--hello échoué de l’activité windows puis exécutez à nouveau après avoir corrigé le problème hello hello activité windows toofail. Consultez hello section suivante pour plus d’informations sur le filtrage windows d’activité dans la liste de hello.  

### <a name="pauseresume-multiple-pipelines"></a>Mettre en pause/relancer plusieurs pipelines
Vous pouvez sélectionner plusieurs pipelines de deux ou plusieurs en utilisant la touche Ctrl de hello. Vous pouvez utiliser les boutons de barre de commandes hello (qui sont mises en surbrillance dans le rectangle de hello rouge de hello suivant image) toopause/reprise les.

![Pause/reprise sur la barre de commandes hello](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)

## <a name="create-alerts"></a>Créez des alertes
Hello **alertes** page vous permet de créer une alerte et afficher/modifier/supprimer des alertes existantes. Vous pouvez également désactiver ou activer une alerte. toosee hello page alertes, cliquez sur hello **alertes** onglet.

![Onglet Alertes](./media/data-factory-monitor-manage-app/AlertsTab.png)

### <a name="toocreate-an-alert"></a>toocreate une alerte
1. Cliquez sur **ajouter une alerte** tooadd une alerte. Vous consultez hello **détails** page.

    ![Créer des alertes - page Détails](./media/data-factory-monitor-manage-app/CreateAlertDetailsPage.png)
2. Spécifiez hello **nom** et **Description** alerte de hello, puis cliquez sur **suivant**. Vous devez voir hello **filtres** page.

    ![Créer des alertes - page Filtres](./media/data-factory-monitor-manage-app/CreateAlertFiltersPage.png)
3. Sélectionnez hello **événement**, **état**, et **sous-état** (facultatif) que vous souhaitez toocreate un service de fabrique de données pour des alertes, puis cliquez sur **suivant**. Vous devez voir hello **destinataires** page.

    ![Créer des alertes - page Destinataires](./media/data-factory-monitor-manage-app/CreateAlertRecipientsPage.png)
4. Sélectionnez hello **envoyer par courrier électronique les administrateurs d’abonnements** option et/ou entrez un **par courrier électronique des administrateurs supplémentaires**, puis cliquez sur **Terminer**. Vous devez voir l’alerte hello dans la liste de hello.

    ![Liste des alertes](./media/data-factory-monitor-manage-app/AlertsList.png)

Dans la liste des alertes hello, utilisez les boutons de hello associés hello alerte tooedit/delete/désactiver/activer une alerte.

### <a name="eventstatussubstatus"></a>Événement/statut/état secondaire
Hello tableau suivant fournit hello liste des événements disponibles et les États (sous-états).

| Nom de l'événement | État | État secondaire |
| --- | --- | --- |
| Exécution de l’activité démarrée |Démarré |Démarrage en cours |
| Exécution de l’activité terminée |Réussi |Réussi |
| Exécution de l’activité terminée |Ayant échoué |Échec de l’allocation des ressources<br/><br/>Échec de l’exécution<br/><br/>Timed Out<br/><br/>Failed Validation<br/><br/>Abandonné |
| Création d’un cluster HDI à la demande démarrée |Démarré |-|
| Cluster HDI à la demande créé correctement |Réussi |-|
| Cluster HDI à la demande supprimé |Réussi |-|

### <a name="tooedit-delete-or-disable-an-alert"></a>tooedit, supprimer ou désactiver une alerte

Utilisez hello suivant tooedit de boutons (mis en surbrillance en rouge), supprimer ou désactiver une alerte.

![Boutons d’alertes](./media/data-factory-monitor-manage-app/AlertButtons.png)
