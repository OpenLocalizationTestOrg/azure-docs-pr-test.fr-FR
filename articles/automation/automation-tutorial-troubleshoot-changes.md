---
title: "Dépanner les modifications apportées à une machine virtuelle Azure | Microsoft Docs"
description: "Utilisez Change Tracking pour dépanner celles apportées à une machine virtuelle Azure."
services: automation
keywords: modification, suivi, automatisation
author: jennyhunter-msft
ms.author: jehunte
ms.date: 12/14/2017
ms.topic: tutorial
ms.custom: mvc
manager: carmonm
ms.openlocfilehash: 0aefa175d676bd7e98841d3a1e9ff5a8c90b7deb
ms.sourcegitcommit: 9292e15fc80cc9df3e62731bafdcb0bb98c256e1
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/10/2018
---
# <a name="troubleshoot-changes-in-your-environment"></a>Dépanner les modifications apportées à votre environnement

Dans ce didacticiel, vous allez apprendre à dépanner les modifications apportées à une machine virtuelle Azure. En activant le suivi des modifications, vous pouvez suivre celles apportées aux logiciels, fichiers, démons Linux, services Windows et clés de registre Windows présents sur vos ordinateurs.
L’identification de ces modifications de configuration peut vous aider à mettre à jour les problèmes opérationnels constatés dans votre environnement.

Ce didacticiel vous montre comment effectuer les opérations suivantes :

> [!div class="checklist"]
> * Intégrer une machine virtuelle pour le suivi des modifications et l’inventaire
> * Rechercher les journaux des modifications des services arrêtés
> * Configurer le suivi des modifications
> * Activer la connexion du journal d’activité
> * Déclencher un événement
> * Afficher les modifications

## <a name="prerequisites"></a>Conditions préalables

Pour suivre ce didacticiel, vous avez besoin des éléments suivants :

* Un abonnement Azure. Si vous n’avez pas encore d’abonnement, vous pouvez [activer vos avantages abonnés MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou créer [un compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).
* Un [compte Automation](automation-offering-get-started.md) qui contiendra les runbooks Watcher et d’action, ainsi que la tâche d’observateur.
* Une [machine virtuelle](../virtual-machines/windows/quick-create-portal.md) à intégrer.

## <a name="log-in-to-azure"></a>Connexion à Azure

Connectez-vous au Portail Azure à l’adresse http://portal.azure.com.

## <a name="enable-change-tracking-and-inventory"></a>Activer le suivi des modifications et l’inventaire

Pour ce didacticiel, vous devez d’abord activer Suivi des modifications et inventaire pour votre machine virtuelle. Si vous avez déjà activé une autre solution d’automatisation pour une machine virtuelle, cette étape n’est pas nécessaire.

1. Dans le menu de gauche, sélectionnez **Machines virtuelles**, puis choisissez une machine virtuelle dans la liste.
1. Dans le menu de gauche, sous la section **Opérations**, cliquez sur **Inventaire**. La page **Enable Change tracking and Inventory** (Activer le suivi des modifications et inventaire) s’ouvre.

Une validation est effectuée pour déterminer si l’option de suivi des modifications et inventaire est bien activée pour cette machine virtuelle.
La validation inclut la vérification de l’existence d’un espace de travail Log Analytics et d’un compte Automation lié, et si la solution est dans l’espace de travail.

Un espace de travail [Log Analytics](../log-analytics/log-analytics-overview.md?toc=%2fazure%2fautomation%2ftoc.json) est utilisé pour collecter les données générées par les fonctionnalités et les services, comme l’inventaire.
L’espace de travail fournit un emplacement unique permettant de consulter et d’analyser les données provenant de plusieurs sources.

Le processus de validation vérifie également que la machine virtuelle est configurée avec le Microsoft Monitoring Agent (MMA) et un worker hybride.
Cet agent sert à communiquer avec la machine virtuelle et à obtenir des informations sur les logiciels installés.
Le processus de validation vérifie également que la machine virtuelle est configurée avec le Microsoft Monitoring Agent (MMA) et un Automation hybrid runbook worker.

Si ces conditions préalables ne sont pas remplies, une bannière apparaît vous permettant d’activer la solution.

![Bannière de configuration intégrée du suivi des modifications et de l’inventaire](./media/automation-tutorial-troubleshoot-changes/enableinventory.png)

Pour activer la solution, cliquez sur la bannière.
Si la validation n’identifie pas l’un des prérequis suivants, il est automatiquement ajouté :

* Espace de travail [Log Analytics](../log-analytics/log-analytics-overview.md?toc=%2fazure%2fautomation%2ftoc.json)
* [Automation](./automation-offering-get-started.md)
* Un [worker runbook hybride](./automation-hybrid-runbook-worker.md) est activé sur la machine virtuelle

L’écran **Change Tracking and Inventory** (Suivi des modifications et inventaire) s’ouvre. Configurez l’emplacement, l’espace de travail Log Analytics et un compte Automation à utiliser, puis cliquez sur **Activer**. Si les champs sont grisés, cela signifie qu’une autre solution d’automatisation est activée pour la machine virtuelle, et les mêmes espace de travail et compte Automation doivent être utilisés.

![Fenêtre de la solution d’activation du suivi des modifications](./media/automation-tutorial-troubleshoot-changes/installed-software-enable.png)

L’activation de la solution peut prendre jusqu'à 15 minutes. Pendant ce temps, vous ne devez pas fermer la fenêtre du navigateur.
Une fois la solution activée, des informations sur les logiciels installés et les modifications apportées à la machine virtuelle sont envoyées à Log Analytics.
Entre 30 minutes et 6 heures peuvent être nécessaires pour que les données soient disponibles pour l’analyse.


## <a name="using-change-tracking-in-log-analytics"></a>Utiliser le suivi des modifications dans Log Analytics

Le suivi des modifications génère des données de journal qui sont envoyées à Log Analytics. Pour rechercher les journaux en exécutant des requêtes, sélectionnez **Log Analytics** en haut de la fenêtre **Suivi des modifications**.
Les données de suivi des modifications sont stockées sous le type **ConfigurationData**. L’exemple de requête Log Analytics ci-après renvoie tous les services Windows arrêtés.

```
ConfigurationChange
| where ConfigChangeType == "WindowsServices" and SvcState == "Stopped"
```

Pour en savoir plus sur l’exécution et la recherche de fichiers journaux dans Log Analytics, consultez [Azure Log Analytics](https://docs.loganalytics.io/index).

## <a name="configure-change-tracking"></a>Configurer le suivi des modifications

Le suivi des modifications vous donne la possibilité d’effectuer le suivi des changements de configuration apportés à votre machine virtuelle. Les étapes suivantes vous montrent comment configurer le suivi des clés de Registre et des fichiers.
 
Pour choisir les fichiers et clés de Registre à collecter et dont effectuer le suivi, sélectionnez **Modifier les paramètres** en haut de la page **Suivi des modifications**.

> [!NOTE]
> L’inventaire et le suivi des modifications utilisent les mêmes paramètres de collecte, et ces paramètres sont configurés au niveau de l’espace de travail.

Dans la fenêtre **Configuration de l’espace de travail**, ajoutez les clés de Registre Windows, puis les fichiers Windows ou Linux à suivre, comme décrit dans les trois sections suivantes.

### <a name="add-a-windows-registry-key"></a>Ajouter une clé de Registre Windows

1. Dans l’onglet **Registre Windows**, sélectionnez **Ajouter**.
    La fenêtre **Ajouter le Registre Windows pour le suivi des modifications**.

   ![Ajouter un Registre pour le suivi des modifications](./media/automation-vm-change-tracking/change-add-registry.png)

2. Sous **Activé**, sélectionnez **True**.
3. Dans la zone **Nom de l’élément**, entrez un nom convivial.
4. (Facultatif) Dans la zone **Groupe**, entrez un nom de groupe.
5. Dans la zone **Clé de Registre Windows**, entrez le nom de la clé de Registre que vous souhaitez suivre.
6. Sélectionnez **Enregistrer**.

### <a name="add-a-windows-file"></a>Ajouter un fichier Windows

1. Dans l’onglet **Fichiers Windows**, sélectionnez **Ajouter**. La fenêtre **Ajouter le fichier Windows pour le suivi des modifications**.

   ![Ajouter un fichier Windows pour le suivi des modifications](./media/automation-vm-change-tracking/change-add-win-file.png)

2. Sous **Activé**, sélectionnez **True**.
3. Dans la zone **Nom de l’élément**, entrez un nom convivial.
4. (Facultatif) Dans la zone **Groupe**, entrez un nom de groupe.
5. Dans la zone **Entrer le chemin**, entrez le chemin d’accès complet et le nom du fichier que vous souhaitez suivre.
6. Sélectionnez **Enregistrer**.

### <a name="add-a-linux-file"></a>Ajouter un fichier Linux

1. Dans l’onglet **Fichiers Linux**, sélectionnez **Ajouter**. La fenêtre **Ajouter le fichier Linux pour le suivi des modifications**.

   ![Ajouter un fichier Linux pour le suivi des modifications](./media/automation-vm-change-tracking/change-add-linux-file.png)

2. Sous **Activé**, sélectionnez **True**.
3. Dans la zone **Nom de l’élément**, entrez un nom convivial.
4. (Facultatif) Dans la zone **Groupe**, entrez un nom de groupe.
5. Dans la zone **Entrer le chemin**, entrez le chemin d’accès complet et le nom du fichier que vous souhaitez suivre.
6. Dans la zone **Type de chemin**, sélectionnez **Fichier** ou **Répertoire**.
7. Sous **Récursivité**, sélectionnez **Activé** pour suivre les modifications apportées au chemin d’accès spécifié et à tous les fichiers et chemins d’accès qui se trouvent sous ce dernier. Pour suivre uniquement le chemin d’accès ou fichier sélectionné, sélectionnez **Désactivé**.
8. Sous **Utiliser sudo**, sélectionnez **Activé** pour suivre les fichiers qui nécessitent la commande `sudo` pour y accéder. Dans le cas contraire, sélectionnez **Désactivé**.
9. Sélectionnez **Enregistrer**.

## <a name="enable-activity-log-connection"></a>Activer la connexion du journal d’activité

À partir de la page **Suivi des modifications** sur votre machine virtuelle, sélectionnez **Manage Activity Log Connection** (Gérer la connexion du journal d’activité). Cette tâche ouvre la page **Journal des activités Azure**. Sélectionnez **Connexion** pour connecter le suivi des modifications au journal des activités Azure pour votre machine virtuelle.

Une fois ce paramètre activé, accédez à la page **Vue d’ensemble** de votre machine virtuelle, puis sélectionnez **Arrêter** pour l’arrêter. Lorsque vous y êtes invité, sélectionnez **Oui** pour arrêter la machine virtuelle. Celle-ci étant libérée, sélectionnez **Démarrer** pour redémarrer votre machine virtuelle.

Le fait d’arrêter et de démarrer une machine virtuelle enregistre un événement dans son journal d’activité. Revenez à la page **Suivi des modifications**. Sélectionnez l’onglet **Événements** au bas de la page. Après un certain temps, les événements apparaissent dans le graphique et le tableau. Comme dans l’étape précédente, chaque événement peut être sélectionné pour en afficher le détail.

![Comment afficher le détail des modifications dans le portail](./media/automation-tutorial-troubleshoot-changes/viewevents.png)

## <a name="view-changes"></a>Afficher les modifications

Lorsque la solution de suivi des modifications et d’inventaire est activée, vous pouvez afficher les résultats sur la page **Suivi des modifications**.

À partir de votre machine virtuelle, sélectionnez **Suivi des modifications** sous **OPÉRATIONS**.

![Capture d’écran montrant la liste des modifications apportées à la machine virtuelle](./media/automation-tutorial-troubleshoot-changes/change-tracking-list.png)

Le graphique affiche les modifications qui se sont produites au fil du temps.
Après avoir ajouté une connexion au journal d’activité, le graphique linéaire dans la partie supérieure affiche les événements du journal des activités Azure.
Chacune des lignes des graphiques à barres représente un autre type de modification dont il est possible d’effectuer le suivi.
Ces types sont les démons Linux, les fichiers, les clés de Registre Windows, les logiciels et les services Windows.
L’onglet Modification présente le détail des modifications indiquées dans la visualisation, par ordre décroissant, c’est-à-dire le plus récent en premier.
L’onglet **Événements** du tableau affiche les événements du journal d’activité connecté, ainsi que les informations correspondantes, les plus récentes en premier.

Vous pouvez voir, dans les résultats, que plusieurs modifications ont été apportées au système, y compris aux logiciels et services. Vous pouvez utiliser les filtres en haut de la page pour filtrer les résultats par **type de modification** ou par plage de temps.

En sélectionnant une modification **WindowsServices**, vous ouvrez la fenêtre **Détails de la modification**. Cette fenêtre présente les détails de la modification, ainsi que les valeurs avant et après. Dans ce cas, le service Protection logicielle a été arrêté.

![Comment afficher le détail des modifications dans le portail](./media/automation-tutorial-troubleshoot-changes/change-details.png)

## <a name="next-steps"></a>Étapes suivantes

Dans ce tutoriel, vous avez appris à effectuer les opérations suivantes :

> [!div class="checklist"]
> * Intégrer une machine virtuelle pour le suivi des modifications et l’inventaire
> * Rechercher les journaux des modifications des services arrêtés
> * Configurer le suivi des modifications
> * Activer la connexion du journal d’activité
> * Déclencher un événement
> * Afficher les modifications

Accédez ensuite à la vue d’ensemble de la solution de suivi des modifications et d’inventaire pour en savoir plus.

> [!div class="nextstepaction"]
> [Solution de gestion des changements et d’inventaire](../log-analytics/log-analytics-change-tracking.md?toc=%2fazure%2fautomation%2ftoc.json)
