---
title: "aaaPower tableau de bord d’intégrité du véhicule et du pilotage habituelles - Azure | Documents Microsoft"
description: "Utiliser les fonctionnalités de hello des aperçus Cortana Intelligence toogain prédictives et en temps réel sur l’intégrité du véhicule et du pilotage habituelles."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: aaeb29a5-4a13-4eab-bbf1-885690d86c56
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: bradsev
ms.openlocfilehash: 0bd054d943387ecad7301236eebae22458173aba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-template-power-bi-dashboard-setup-instructions"></a>Instructions de configuration du tableau de bord Power BI pour le modèle de la solution Vehicle Telemetry Analytics
Cela **menu** lie chapitres toohello dans ce manuel. 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

Hello solution du véhicule télémétrie Analytique présente comment les concessions de voiture, constructeurs automobiles et aux entreprises d’assurance peuvent tirer parti des fonctionnalités de hello de Cortana Intelligence toogain prédictives et en temps réel des informations sur l’intégrité du véhicule et du pilotage améliorations de toodrive habitudes dans la zone de hello du client expérience, R & D et campagnes marketing. Ce document contient des instructions étape par étape sur la configuration des rapports de Power BI hello et tableau de bord une fois la solution de hello est déployée dans votre abonnement. 

## <a name="prerequisites"></a>Composants requis
1. Déployer hello [Analytique de télémétrie](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90) solution  
2. [Installez Microsoft Power BI Desktop](http://www.microsoft.com/download/details.aspx?id=45331)
3. Un [abonnement Azure](https://azure.microsoft.com/pricing/free-trial/). Si vous n’avez pas d’abonnement Azure, commencez par un abonnement Azure gratuit
4. Compte Microsoft Power BI

## <a name="cortana-intelligence-suite-components"></a>Composants Cortana Intelligence Suite
Dans le cadre du modèle de solution hello véhicule télémétrie Analytique, hello suivant Cortana Intelligence services est déployé dans votre abonnement.

* **Event Hubs** pour l’ingestion dans Azure de millions d’événements de télémétrie de véhicules.
* **STREAM ANALYTICS** , pour une visibilité en temps réel sur l’état des véhicules et une conservation de ces données dans un stockage à long terme afin d’enrichir les analyses par lots.
* **Apprentissage** pour la détection d’anomalie en temps réel et les analyses prédictives toogain de traitement par lots.
* **HDInsight** est exploitée tootransform des données à grande échelle
* **Fabrique de données** gère l’orchestration, la planification, la gestion des ressources et la surveillance de pipeline de traitement par lots hello.

**POWER BI** offre à cette solution un tableau de bord complet permettant de visualiser à la fois les données en temps réel et les analyses prédictives. 

solution de Hello utilise deux sources de données différentes : **simulée véhicule signaux et le jeu de données de diagnostic** et **catalogue du véhicule**.

Un simulateur de télématique des véhicules est intégré à cette solution. Il émet des informations de diagnostic et signale un état toohello correspondant du véhicule de hello et modèle conduite à un moment donné dans le temps. 

Hello véhicule catalogue est un mappage de toomodel référence dataset contenant VIN

## <a name="power-bi-dashboard-preparation"></a>Préparation du tableau de bord Power BI
### <a name="setup-power-bi-real-time-dashboard"></a>Configuration du tableau de bord Power BI en temps réel

**Démarrer l’application de tableau de bord en temps réel hello** une fois le déploiement de hello est terminé, vous devez suivre les Instructions de fonctionnement de manuel de hello

* Téléchargez l’application de tableau de bord en temps réel RealtimeDashboardApp.zip et décompressez-le.
*  Dans le dossier de décompressé hello, ouvrez le fichier de configuration d’application 'RealtimeDashboardApp.exe.config', appSettings de remplacement pour les connexions de service Eventhub, stockage d’objets Blob et ML avec des valeurs hello Bonjour Instructions d’opération manuelle, puis enregistrez vos modifications.
* Exécutez l’application RealtimeDashboardApp.exe. Une fenêtre de connexion contextuelle, fournissez vos informations d’identification valides pour Power BI et cliquez sur hello **accepter** bouton. Ensuite, application hello démarre toorun.

   ![Connectez-vous tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/5-sign-into-powerbi.png)
   
   ![Autorisations du tableau de bord Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-powerbi-dashboard-permissions.png)

* Site Web de connexion tooPowerBI et créer le tableau de bord en temps réel.

Maintenant, vous êtes prêt tooconfigure hello tableau de bord avec toogain visualisations enrichies en temps réel et des analyses prédictives sur l’intégrité du véhicule et du pilotage habituelles. Il prend environ 45 minutes tooan heure toocreate hello tous les rapports et configurer le tableau de bord hello. 

### <a name="configure-power-bi-reports"></a>Configurer les rapports Power BI
les rapports en temps réel Hello et tableau de bord hello prennent environ 30 et 45 minutes toocomplete. Parcourir trop[http://powerbi.com](http://powerbi.com) et de la connexion.

![Connectez-vous tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-1-powerbi-signin.png)

Un nouveau jeu de données est généré dans Power BI. Cliquez sur hello **ConnectedCarsRealtime** jeu de données.

![Jeu de données Connected Cars en temps réel sélectionné](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/7-select-connected-cars-realtime-dataset.png)

Enregistrer à l’aide de rapport vide hello **Ctrl + s**.

![Enregistrez le rapport vide](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/8-save-blank-report.png)

Nommez le rapport *Vehicle Telemetry Analytics Real-time - Reports*.

![Nommez le rapport](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/9-provide-report-name.png)

## <a name="real-time-reports"></a>Rapports en temps réel
Il existe trois rapports en temps réel dans cette solution :

1. Véhicules opérationnels
2. Véhicules nécessitant une maintenance
3. Statistiques relatives à l’état des véhicules

Vous pouvez choisir tooconfigure tous les rapports en temps réel trois hello ou arrêter après n’importe quelle étape et continuer toohello la section suivante de la configuration des rapports de lot hello. Nous vous recommandons de vous toocreate tous les hello trois rapports insights complète de toovisualize hello du chemin d’accès en temps réel de hello de solution de hello.  

### <a name="1-vehicles-in-operation"></a>1. Véhicules opérationnels
Double-cliquez sur **Page 1** et renommez-la trop « Véhicules dans l’opération. »  
    ![Connected Cars - Véhicules opérationnels](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)  

Sélectionnez **vin** dans **Champs** et choisissez **« Carte »** comme type de visualisation.  

Une visualisation sous forme de carte est créée, comme illustré ci-dessous.  
    ![Connected Cars - Sélectionner le numéro d’identification du véhicule](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4b.png)

Cliquez sur Nouvelle visualisation hello zone vide tooadd.  

Sélectionnez **Ville** et **vin** dans Champs. Changez de visualisation trop**« Mappage »**. Faites glisser **vin** dans la zone de valeurs. Faites glisser **Ville** à partir des champs trop**légende** zone.   
    ![Connected Cars - Visualisation sous forme de carte](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)

Sélectionnez **format** section **visualisations**, cliquez sur **titre** et modifiez hello **texte** trop**véhicules » dans opération par ville »**.  
    ![Connected Cars - Véhicules opérationnels par ville](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)   

La visualisation finale doit être telle qu’illustrée ci-dessous.    
    ![Connected Cars - Visualisation finale](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4e.png)

Cliquez sur Nouvelle visualisation hello zone vide tooadd.  

Sélectionnez **Ville** et **vin**, modifiez le type de visualisation trop**Histogramme groupé**. Vérifiez le champ **Ville** dans la zone **Axe** et **vin** dans la zone **Valeur**.  

Triez le graphique par **« Nombre de vin »**.  
    ![Connected Cars - Nombre de numéros d’identification de véhicule](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)  

Graphique de modification **titre** trop**« Véhicules dans l’opération par ville »**  

Cliquez sur hello **Format** section, puis sélectionnez **couleurs des données**, cliquez sur hello **« Sur »** trop**afficher tout**  
    ![Connected Cars - Afficher toutes les couleurs de données](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)  

Modifier la couleur hello de ville individuel en cliquant sur l’icône de couleur.  
    ![Connected Cars - Modifier les couleurs](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4h.png)  

Cliquez sur Nouvelle visualisation hello zone vide tooadd.  

Sélectionnez la visualisation **Histogramme groupé** dans la zone Visualisations, faites glisser le champ **Ville** dans la zone **Axe**, **Modèle** dans la zone **Légende** et **vin** dans la zone **Valeur**.  
    ![Connected Cars - Histogramme groupé](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)  
    ![Connected Cars - Rendu](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)

Réorganisez toutes les visualisations sur cette page comme indiqué dans la figure.  
    ![Connected Cars - Visualisations](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4k.png)

Vous avez correctement configuré le rapport en temps réel de « Véhicules dans l’opération » hello. Vous pouvez passer l’état en temps réel de toocreate hello suivant ou arrêter ici et configurer le tableau de bord hello. 

### <a name="2-vehicles-requiring-maintenance"></a>2. Véhicules nécessitant une maintenance
Cliquez sur ![ajouter](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd un nouveau rapport, renommez-le trop**« Véhicules nécessitant une Maintenance »**

![Connected Cars - Véhicules nécessitant une maintenance](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4l.png)  

Sélectionnez **vin** champ et modifiez le type de visualisation trop**carte**.  
    ![Connected Cars - Visualisation du numéro d’identification du véhicule sous forme de carte](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)  

Nous avons un champ nommé « MaintenanceLabel » dans le jeu de données hello. Ce champ peut avoir une valeur de « 0 » ou « 1 ». Elle est définie par le modèle d’Azure Machine Learning hello approvisionné en tant que partie de la solution et intégrés avec le chemin d’accès en temps réel de hello. valeur de Hello « 1 » indique un véhicule requiert une maintenance. 

tooadd un **niveau Page** filtre pour afficher des données de véhicules, qui nécessitent la maintenance : 

1. Hello de glisser **« MaintenanceLabel »** dans **filtres au niveau de la Page**.  
   ![Connected Cars - Filtres au niveau de la page](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)  
2. Cliquez sur le menu **Filtrage de base** situé en bas du filtre de niveau page MaintenanceLabel.  
   ![Connected Cars - Filtrage de base](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)  
3. Affectez-lui la valeur filtre trop**« 1 »**    
   ![Connected Cars - Valeur de filtre](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)  

Cliquez sur Nouvelle visualisation hello zone vide tooadd.  

Sélectionnez **Histogramme groupé** dans la section Visualisations.  
![Connected Cars - Visualisation du numéro d’identification du véhicule sous forme de carte](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)  
![Connected Cars - Histogramme groupé](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)

Champ de glisser **modèle** dans **axe** zone, **Vin** trop**valeur** zone. Triez ensuite la visualisation par **Nombre de vin**.  Graphique de modification **titre** trop**« Véhicules nécessitant une maintenance par modèle »**  

Faites glisser les champs **vin** dans la zone **Saturation de la couleur** située dans la section **Champs** ![Champs](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png)de l’onglet **Visualisation**.  
![Connected Cars - Saturation des couleurs](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)  

Modifiez **Couleurs des données** dans les visualisations à partir de la section **Format**.  
Définissez **F2C812** comme couleur minimale.  
Définissez **FF6300** comme couleur maximale.  
![Connected Cars - Changements de couleur](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)  
![Connected Cars - Nouvelles couleurs de visualisation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)  

Cliquez sur Nouvelle visualisation hello zone vide tooadd.  

Sélectionnez **Histogramme groupé** dans la zone Visualisations, faites glisser le champ **vin** dans la zone **Valeur** et le champ **Ville** dans la zone **Axe**. Triez le graphique par **« Nombre de vin »**. Graphique de modification **titre** trop**« Véhicules exigeant une maintenance par ville »**   
![Connected Cars - Véhicules nécessitant une maintenance par ville](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)  

Cliquez sur Nouvelle visualisation hello zone vide tooadd.  

Sélectionnez **carte à plusieurs lignes** visualisation à partir des visualisations, faites glisser **modèle** et **vin** dans hello **champs** zone.  
![Connected Cars - Carte à plusieurs lignes](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)    

Réorganisation tous de visualisation de hello, rapport final de hello se présente comme suit :  
![Connected Cars - Carte à plusieurs lignes](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4v.png)  

Vous avez correctement configuré le rapport en temps réel de hello « Véhicules nécessitant une Maintenance ». Vous pouvez passer l’état en temps réel de toocreate hello suivant ou arrêter ici et configurer le tableau de bord hello. 

### <a name="3-vehicles-health-statistics"></a>3. Statistiques relatives à l’état des véhicules
Cliquez sur ![ajouter](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd nouveau rapport, renommez-le trop**« Statistiques d’intégrité de véhicules »**  

Sélectionnez **jauge** visualisation à partir des visualisations, puis faites glisser hello **vitesse** dans **, la valeur minimale, maximale valeur** zones.  
![Connected Cars - Carte à plusieurs lignes](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)  

Modifier l’agrégation par défaut de hello de **vitesse** dans **valeur zone** trop**moyenne** 

Modifier l’agrégation par défaut de hello de **vitesse** dans **zone de Minimum** trop**Minimum**

Modifier l’agrégation par défaut de hello de **vitesse** dans **zone de Maximum** trop**maximale**

![Connected Cars - Carte à plusieurs lignes](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4x.png)  

Renommer hello **jauge titre** trop**« Vitesse moyenne »** 

![Connected Cars - Jauge](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4y.png)  

Cliquez sur Nouvelle visualisation hello zone vide tooadd.  

Vous pouvez également ajouter une **jauge** pour l’**huile moteur moyenne**, le **carburant moyen** et la **température moteur moyenne**.  

Modifier l’agrégation par défaut de hello des champs de chaque jauge comme indiqué ci-dessus comme suit dans **« Vitesse moyenne »** de jauge.

![Connected Cars - Jauges](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4z.png)

Cliquez sur Nouvelle visualisation hello zone vide tooadd.

Sélectionnez **courbes et histogramme groupé** à partir des visualisations, puis faites glisser **Ville** dans **axe partagé**, faites glisser **vitesse**, **champs tirepressure et engineoil** dans **les valeurs de colonne** zone, changer le type d’agrégation trop**moyenne**. 

Hello de glisser **engineTemperature** dans **les valeurs de ligne** zone, modifier le type d’agrégation hello trop**moyenne**. 

![Connected Cars - Champs de visualisations](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4aa.png)

Graphique de hello modification **titre** trop**« Moyenne vitesse pression des pneus, pétrole de moteur et de température du moteur »**.  

![Connected Cars - Champs de visualisations](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4bb.png)

Cliquez sur Nouvelle visualisation hello zone vide tooadd.

Sélectionnez **Treemap** visualisation à partir des visualisations, faites glisser hello **modèle** dans hello **groupe** zone et faites glisser hello champ  **MaintenanceProbability** dans hello **valeurs** zone.

Graphique de hello modification **titre** trop**« Modèles véhicule nécessitant une maintenance »**.

![Connected Cars - Modifier le titre du graphique](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4cc.png)

Cliquez sur Nouvelle visualisation hello zone vide tooadd.

Sélectionnez **100 % de graphique à barres empilées** de visualisation, faites glisser hello **Ville** dans hello **axe** zone et faites glisser hello **MaintenanceProbability**, **RecallProbability** champs dans hello **valeur** zone.

![Connected Cars - Ajouter une visualisation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4dd.png)

Cliquez sur **Format**, sélectionnez **couleurs des données**et ensemble hello **MaintenanceProbability** toohello valeur de couleur **« F2C80F »**.

Hello de modification **titre** Hello graphique trop**« Probabilité de véhicule Maintenance & rappeler par City »**.

![Connected Cars - Ajouter une visualisation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ee.png)

Cliquez sur Nouvelle visualisation hello zone vide tooadd.

Sélectionnez **graphique en aires** de visualisation à partir des visualisations, faites glisser hello **modèle** dans hello **axe** zone et faites glisser hello **engineOil, tirepressure, vitesse et MaintenanceProbability** champs dans hello **valeurs** zone. Changer le type d’agrégation trop**« Moyenne »**. 

![Connected Cars - Modifier le type d’agrégation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ff.png)

Modifier le titre de hello du graphique de hello trop**« Moyenne pétrole de moteur, probabilité pression, la vitesse et la maintenance des pneus par modèle »**.

![Connected Cars - Modifier le titre du graphique](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4gg.png)

Cliquez sur Nouvelle visualisation hello zone vide tooadd :

1. Dans la section Visualisations, sélectionnez **Nuage de points** .
2. Hello de glisser **modèle** dans hello **détails** et **légende** zone.
3. Hello de glisser **carburant** dans hello **axe des abscisses** zone, modifiez d’agrégation de hello trop**moyenne**.
4. Faites glisser **engineTemparature** dans **zone de l’axe des y**, changent d’agrégation de hello**moyenne**
5. Hello de glisser **vin** dans hello **taille** zone.

![Connected Cars - Ajouter une visualisation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4hh.png)

Graphique de hello modification **titre** trop**« Moyennes de carburant, température moteur par modèle »**.

![Connected Cars - Modifier le titre du graphique](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ii.png)

rapport final de Hello ressemble à celle ci-dessous.

![Connected Cars - Rapport final](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4jj.png)

### <a name="pin-visualizations-from-hello-reports-toohello-real-time-dashboard"></a>Code confidentiel des visualisations à partir du tableau de bord en temps réel de la toohello de hello rapports
Créer un tableau de bord vide en cliquant sur l’icône plus hello tooDashboards suivant. Vous pouvez le nommer « Vehicle Telemetry - Tableau de bord d’analyse ».

![Connected Cars - Tableau de bord](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.5.png)

Visualisation de code confidentiel hello de hello au-dessus du tableau de bord toohello rapports. 

![Connected Cars - Tableau de bord](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.6.png)

tableau de bord Hello doit se présenter comme suit lorsque tous les de hello trois rapports sont créés et de hello correspondant visualisations sont épinglées toohello le tableau de bord. Si vous n’avez pas créé tous les rapports de hello, votre tableau de bord peut différer. 

![Connected Cars - Tableau de bord](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-4.0.png)

Félicitations ! Vous venez de créer le tableau de bord en temps réel hello. À mesure que vous tooexecute CarEventGenerator.exe et RealtimeDashboardApp.exe, vous devez voir les mises à jour dynamiques sur le tableau de bord hello. Il doit prendre hello de toocomplete too15 environ 10 minutes comme suit.

## <a name="setup-power-bi-batch-processing-dashboard"></a>Configuration du tableau de bord de traitement par lots de Power BI
> [!NOTE]
> Il prend environ deux heures (à partir de l’achèvement réussi de hello du déploiement de hello) pour hello fin tooend lot toofinish l’exécution du pipeline de traitement et de traiter une valeur d’année de données générées. Par conséquent, attendez hello toofinish avant de procéder aux étapes suivantes de hello de traitement. 
> 
> 

**Télécharger le fichier de concepteur hello Power BI**

* Un fichier de concepteur préconfiguré Power BI est inclus dans le cadre du déploiement de hello Instructions d’opération manuelle
* Recherchez 2. Tableau de bord du traitement de lot le programme d’installation Power BI vous pouvez télécharger un modèle de Power BI hello pour le traitement par lots de tableau de bord appelé **ConnectedCarsPbiReport.pbix**.
* Enregistrez le fichier en local

**Configurer les rapports Power BI**

* Fichier de concepteur hello ouvrir '**ConnectedCarsPbiReport.pbix**' à l’aide de Power BI Desktop. Si vous ne pas déjà avez, installez hello Power BI Desktop à partir de [installation de Power BI Desktop](http://www.microsoft.com/download/details.aspx?id=45331). 
* Cliquez sur hello **modifier les requêtes**.

![Modifier une requête Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/10-edit-powerbi-query.png)

* Double-cliquez sur hello **Source**.

![Définir la source Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/11-set-powerbi-source.png)

* Mettre à jour la chaîne de connexion de serveur avec le serveur SQL Azure hello qui ont été configuré dans le cadre du déploiement de hello.  Rechercher dans les Instructions d’opération manuelle hello sous 

    4. Base de données SQL Azure
    
    * Serveur : somethingsrv.database.windows.net
    * Base de données : connectedcar
    * Nom d’utilisateur : nom d’utilisateur
    * Mot de passe : vous pouvez gérer votre mot de passe SQL Server à partir du portail Azure

* Laissez la **base de données** en tant que *connectedcar*.

![Définir la base de données Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/12-set-powerbi-database.png)

* Cliquez sur **OK**.
* Vous verrez **informations d’identification Windows** onglet sélectionné par défaut, également le modifier**informations d’identification de base de données** en cliquant sur **base de données** onglet à droite.
* Fournir hello **nom d’utilisateur** et **mot de passe** de votre base de données SQL Azure qui a été spécifié pendant l’installation de son déploiement.

![Fournir les informations d’identification de la base de données](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/13-provide-database-credentials.png)

* Cliquez sur **Connexion**
* Répétez hello étapes ci-dessus pour chaque hello trois autres requêtes présentes dans le volet droit, puis mettre à jour les détails de connexion de source de données hello.
* Cliquez sur **Fermer et charger**. Jeux de données fichier Power BI Desktop est des tables de base de données Azure tooSQL connecté.
* **Fermez** le fichier Power BI Desktop.

![Fermez Power BI Desktop](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/14-close-powerbi-desktop.png)

* Cliquez sur **enregistrer** bouton les modifications de hello toosave. 

Vous avez maintenant configuré tous les rapports hello correspondant toohello chemin de traitement par lots dans les solutions hello. 

## <a name="upload-toopowerbicom"></a>Télécharger trop*powerbi.com*
1. Accédez toohello portail de web Power BI au http://powerbi.com et à la connexion.
2. Cliquez sur **Get Data**  
3. Téléchargez hello fichier Power BI Desktop.  
4. tooupload, cliquez sur **obtenir des données -> fichiers Get -> fichier Local**  
5. Accédez toohello **»**ConnectedCarsPbiReport.pbix**»**  
6. Une fois que le fichier de hello est chargé, vous serez tooyour arrière un espace de travail Power BI.  

Un jeu de données, un rapport et un tableau de bord vide sont alors créés.  

Code confidentiel graphiques nouveau tableau de bord tooa appelé **tableau de bord véhicule télémétrie Analytique** dans **Power BI**. Cliquez sur le tableau de bord vide hello créé ci-dessus, puis accédez toohello **rapports** cliquez sur la section hello téléchargé nouveau rapport.  

![Vehicle Telemetry Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard1.png) 

**Remarque hello rapport comporte six pages :**  
Page 1 : densité de véhicules  
Page 2 : intégrité des véhicules en temps réel  
Page 3 : véhicules utilisés de manière intensive   
Page 4 : véhicules rappelés  
Page 5 : véhicules économes en carburant  
Page 6 : logo de Contoso  

![Connected Cars Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard2.png)

**À partir de la Page 3**, épingler des éléments suivants de hello :  

1. Nombre de vin  
   ![Connected Cars Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard3.png) 
2. Véhicules utilisés de manière intensive par modèle – Graphique en cascade   
   ![Vehicle Telemetry - Épingler des graphiques 4](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard4.png)

**À partir de la Page 5**, épingler des éléments suivants de hello : 

1. Nombre de vin    
   ![Vehicle Telemetry - Épingler des graphiques 5](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard5.png)  
2. Véhicules économes en carburant par modèle : histogramme groupé   
   ![Vehicle Telemetry - Épingler des graphiques 6](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard6.png)

**À partir de la Page 4**, épingler des éléments suivants de hello :  

1. Nombre de vin  
   ![Vehicle Telemetry - Épingler des graphiques 7](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard7.png) 
2. Véhicules rappelés par ville, modèle : Compartimentage   
   ![Vehicle Telemetry - Épingler des graphiques 8](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard8.png)  

**À partir de la Page 6**, épingler des éléments suivants de hello :  

1. Logo Contoso Motors   
   ![Vehicle Telemetry - Épingler des graphiques 9](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard9.png)

**Organiser hello le tableau de bord**  

1. Accédez toohello le tableau de bord
2. Pointez sur chaque graphique et renommez-la en fonction de hello d’affectation de noms fournis dans l’image du tableau de bord complet hello ci-dessous. Également déplacer des graphiques hello autour toolook comme tableau de bord hello ci-dessous.  
   ![Vehicle Telemetry - Organiser le tableau de bord 2](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard2.png)  
   ![Vehicle Telemetry Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard.png)
3. Si vous avez créé tous les rapports hello comme indiqué dans ce document, hello final tableau de bord terminé doit ressembler à hello figure suivante. 

![Vehicle Telemetry - Organiser le tableau de bord 2](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard3.png)

Félicitations ! Vous venez de créer des rapports hello et hello toogain du tableau de bord en temps réel, prédictive et des informations de lot sur l’intégrité du véhicule et du pilotage habituelles.  
