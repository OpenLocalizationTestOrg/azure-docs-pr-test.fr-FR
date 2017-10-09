---
title: "aaaDashboard, analyse, l’échelle, configurer et connexions hybrides dans BizTalk Services | Documents Microsoft"
description: "En savoir plus sur les contrôles hello et surveiller les performances sur les onglets de portail classique hello pour les Services BizTalk : tableau de bord, analyse, l’échelle, configurer et connexions hybrides. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 7a1815db-0de2-4274-8be0-198c1b077324
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: c9fafdad20489571ee3849bbacd2c2b10933154f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="review-hello-dashboard-monitor-scale-configure-and-hybrid-connection-tabs"></a>Passez en revue les onglets de tableau de bord, analyse, l’échelle, configurer et la connexion hybride hello

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Après avoir créé votre BizTalk Service et que vous déployez votre application, vous pouvez modifier certains des paramètres de Service BizTalk hello et surveiller les performances de l’application hello. 

Lorsque vous ouvrez hello portail Azure classic, vous accédez automatiquement à hello **tous les éléments** onglet tooview votre BizTalk Service, sélectionnez votre BizTalk Service Bonjour **tous les éléments** onglet ou sélectionnez hello **BIZTALK SERVICES** onglet ; puis sélectionnez le nom de votre BizTalk Service.

Une nouvelle fenêtre s’ouvre avec hello suivant des onglets. Cette rubrique décrit ces onglets.

## <a name="quickstart-quickstartquickstart"></a>Démarrage rapide (![Démarrage rapide][Quickstart])
En fonction de hello BizTalk Services Édition, toutes les options répertoriées n’est peut-être pas disponibles. 

<table border="1">
    <tr>
        <td><strong>Obtenir les outils de hello</strong></td>
        <td>Télécharger les modèles projet hello SDK des Services BizTalk tooinstall hello Visual Studio sur votre ordinateur de développement local. Ces modèles créent des hello <strong>BizTalk Services</strong> (pont) et hello <strong>artefacts BizTalk Service</strong> projets (transformer) de Visual Studio qui sont déployé tooyour BizTalk Service.
        <br/><br/>
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335">Comment puis-je démarrer à l’aide de hello Azure BizTalk Services SDK </a> et <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">installation Bonjour Azure BizTalk Services SDK</a> listes hello tooget étapes a démarré.
        </td>
    </tr>
    <tr>
        <td><strong>Créer des accords partenaires</strong></td>
        <td>Ouvre hello hébergé sur Azure où vous ajoutez des partenaires et créez X12, AS2, le portail Azure BizTalk Services et des accords EDIFACT EDI.
        <br/><br/>
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuration des composants de messagerie EDI sur le portail BizTalk Services</a> listes hello tooget étapes a démarré.
        </td>
    </tr>

<tr>
        <td><strong>En savoir plus sur les services BizTalk</strong></td>
        <td>Accédez toohello <a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">centre de formation</a> toolearn plus d’informations sur les Services BizTalk Azure.</td>
</tr>
</table>


Dans la barre des tâches hello bas hello, vous pouvez :

<table border="1">

<tr>
<td><strong>Gérer</strong> le déploiement de votre application</td>
<td>Ouvre le portail Azure BizTalk Services hello. Hello portail BizTalk Services hello entrée tooEDI configuration soit, y compris l’ajout de partenaires et la création de X12, AS2 et les accords EDIFACT.
<br/><br/>
Cela est hello identique <strong>créer des accords de partenariat</strong> sur hello <strong>Quick Start</strong> onglet.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuration des composants de messagerie EDI sur le portail BizTalk Services</a> fournit des informations sur hello portail BizTalk Services.</td>
</tr>

<tr>
<td><strong>Informations de connexion</strong> de hello Namespace de contrôle d’accès</td>
<td>Lorsque vous sélectionnez des informations de connexion, puis hello Namespace de contrôle d’accès, émetteur par défaut, et la clé par défaut sont affichés. Vous pouvez copier ces valeurs.
<br/><br/>
Vous pouvez également ouvrir hello portail de contrôle d’accès. <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Créer un contrôle d’accès Namespace</a> fournit des informations sur le portail de contrôle d’accès de hello.</td>
</tr>

<tr>
<td><strong>Synchroniser les clés</strong> Bonjour compte de stockage</td>
<td>Lorsque vous créez un compte de stockage, une clé primaire et une clé secondaire sont automatiquement créées. Ces clés de chiffrement de contrôlent l’accès tooyour compte de stockage. Votre BizTalk Service utilise automatiquement hello clé primaire. <strong>Synchroniser les clés</strong> activer tooswitch utilisateurs entre hello Primary Key et hello clé secondaire sans interrompre hello BizTalk Service.
<br/><br/>
Par exemple, vous souhaitez hello BizTalk Service toouse une nouvelle clé primaire pour hello compte de stockage. toodo cela :
<br/><br/>
<ol>
<li>Sélectionnez votre service BizTalk, puis <strong>Clés de synchronisation</strong>. Sélectionnez hello clé secondaire. Lorsque vous effectuez cette opération, hello BizTalk Service démarre à l’aide de la clé secondaire de hello.</li>
<li>Bonjour portail Azure classic, sélectionnez votre compte de stockage et régénérer hello clé primaire. N’oubliez pas, votre BizTalk Service est hello clé secondaire.</li>
<li>Sélectionnez votre service BizTalk, puis <strong>Clés de synchronisation</strong>. À présent, sélectionnez hello clé primaire. Cela est hello nouvelle clé primaire vous régénéré.</li>
<li>Bonjour portail Azure classic, sélectionnez votre compte de stockage et régénérer hello clé secondaire.</li>
</ol>
<br/>
On parle de « clés de substitution » pour décrire ce processus. objectif de Hello est tooswitch d’utilisateurs tooenable entre hello Primary Key et hello clé secondaire sans interrompre hello BizTalk Service.</td>
</tr>

<tr>
<td><strong>Supprimer</strong> votre application</td>
<td>Lorsque vous sélectionnez Supprimer, votre BizTalk Service et tous les éléments déployés tooit sont supprimés.</td>
</tr>
</table>


## <a name="dashboard"></a>tableau de bord
En fonction de hello BizTalk Services Édition, toutes les options répertoriées n’est peut-être pas disponibles. 

Lorsque vous sélectionnez le nom de votre BizTalk Service, onglet de tableau de bord hello s’affiche. Dans le tableau de bord, vous pouvez :

##### <a name="usage-overview-shows-hello-number-of-used-hybrid-connections"></a>Présentation de l’utilisation : Montre le nombre de hello de connexions hybrides utilisées
Affiche également l’utilisation des données hello en Go. 

##### <a name="metric-graph-shows-a-fixed-list-of-performance-metrics"></a>Graphique métrique : illustre une liste fixe de mesures de performances.
Ces métriques fournissent des valeurs en temps réel concernant l’intégrité hello hello BizTalk Service. Vous pouvez également choisir hello **relatif** ou **absolu** intervalle de temps de valeurs et hello **intervalle** des métriques hello sont affichées dans le graphique de hello. 

Pour obtenir une description de ces métriques de performances, consultez trop[métriques disponibles](#Metrics) dans cette rubrique.

##### <a name="quick-glance-lists-your-biztalk-service-properties"></a>Aperçu rapide : dresse la liste des propriétés de votre service BizTalk.
<table border="1">

<tr>
<td><strong>Mettre à jour les informations d’identification de la base de données de suivi</strong></td>
<td>Modifications hello nom d’utilisateur et mot de passe utilisé toolog dans hello de base de données de suivi.</td>
</tr>
<tr>
<td><strong>Mettre à jour le certificat SSL</strong></td>
<td>Peut mettre à jour hello BizTalk Service toouse un autre certificat SSL. Un certificat SSL auto-signé est créé automatiquement lorsque vous <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">créer hello BizTalk Service</a>.</td>
</tr>
<tr>
<td><strong>Télécharger le certificat</strong></td>
<td>Vous pouvez télécharger le certificat SSL de hello utilisé par votre ordinateur local tooa de BizTalk Service.</td>
</tr>
<tr>
<td><strong>État</strong></td>
<td>Affiche l’état actuel de hello de votre BizTalk Service. Voir <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">Tableau comparatif des états de BizTalk Services</a>. </td>
</tr>
<tr>
<td><strong>URL du service</strong></td>
<td>URL de Hello pour votre BizTalk Service. Cela est hello même comme hello <strong>URL de domaine</strong> entré lors de la création de votre BizTalk Service.</td>
</tr>
<tr>
<td><strong>Adresse IP virtuelle (VIP) publique</strong></td>
<td>adresse IP de Hello affecté tooyour BizTalk Service. Il est utilisé pour tous les points de terminaison d’entrée et est l’adresse de la source hello pour le trafic sortant. Cette adresse IP appartient tooyour BizTalk Service tant qu’il est créé. Si vous supprimez hello BizTalk Service, adresse IP de hello est affecté tooanother BizTalk Service.</td>
</tr>
<tr>
<td><strong>Espace de noms ACS</strong></td>
<td>Authentifie avec hello BizTalk Service.</td>
</tr>
<tr>
<td><strong>Édition</strong></td>
<td>Répertorie les hello que Édition entrée lors de la création de hello BizTalk Service.</td>
</tr>
<tr>
<td><strong>Emplacement</strong></td>
<td>Affiche hello région géographique qui héberge votre BizTalk Service.</td>
</tr>
<tr>
<td><strong>Créé</strong></td>
<td>Hello de date et heure de hello affiche le BizTalk Service a été créé.</td>
</tr>
<tr>
<td><strong>Base de données des suivis</strong></td>
<td>nom de base de données SQL Azure Hello qui stocke hello suivi des tables utilisées par votre BizTalk Service. 
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Configuration requise expliqué</a> fournit des détails sur hello de base de données de suivi.</td>
</tr>
<tr>
<td><strong>Stockage de surveillance/archivage</strong></td>
<td>nom de compte du stockage Azure Hello qui stocke hello surveillent la sortie de votre BizTalk Service.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Configuration requise expliqué</a> fournit des détails sur hello compte de stockage.</td>
</tr>
<tr>
<td><strong>Nom d’abonnement</strong></td>
<td>Répertorie les abonnement hello qui héberge votre BizTalk Service. abonnement de Hello régit l’accès toohello portail Azure classic.</td>
</tr>
<tr>
<td><strong>Identifiant d’abonnement</strong></td>
<td>Lorsqu’un abonnement est créé, un ID d’abonnement est automatiquement généré. Lorsque vous utilisez l’API REST, vous devrez peut-être hello tooenter ID d’abonnement.</td>
</tr>
</table>

[BizTalk Services : Mise en service portail classique d’à l’aide de Azure](http://go.microsoft.com/fwlink/p/?LinkID=302280) listes hello étapes toocreate un BizTalk Service.

##### <a name="manage-connection-information-sync-keys-and-delete-in-hello-task-bar"></a>Gérer les informations de connexion, synchroniser les clés et les supprimer dans la barre des tâches hello :
<table border="1">

<tr>
<td><strong>Gérer</strong> le déploiement de votre application</td>
<td>Hello ouvre le portail Azure BizTalk Services. Hello portail BizTalk Services hello entrée tooEDI configuration soit, y compris l’ajout de partenaires et la création de X12, AS2 et les accords EDIFACT.
<br/><br/>
Cela est hello identique <strong>créer des accords de partenariat</strong> sur hello <strong>Quick Start</strong> onglet.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuration des composants de messagerie EDI sur le portail BizTalk Services</a> fournit des informations sur hello portail BizTalk Services.</td>
</tr>
<tr>
<td><strong>Informations de connexion</strong> de hello Namespace de contrôle d’accès</td>
<td>Affiche hello Namespace de contrôle d’accès, émetteur par défaut et les valeurs de clé par défaut ; qui peut être copié.
<br/><br/>
Vous pouvez également ouvrir hello portail de contrôle d’accès. Ce portail de contrôle d’accès est hello même fonction que l’option d’Active Directory hello dans le volet de navigation gauche hello.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">La gestion de votre ACS Namespace</a> fournit des informations sur le portail de contrôle d’accès de hello.</td>
</tr>
<tr>
<td><strong>Synchroniser les clés</strong> Bonjour compte de stockage</td>
<td>Lorsque vous créez un compte de stockage, une clé primaire et une clé secondaire sont automatiquement créées. Ces clés de chiffrement de contrôlent l’accès tooyour compte de stockage. Votre BizTalk Service utilise automatiquement hello clé primaire. <strong>Synchroniser les clés</strong> activer tooswitch utilisateurs entre hello Primary Key et hello clé secondaire sans interrompre hello BizTalk Service.
<br/><br/>
Par exemple, vous souhaitez hello BizTalk Service toouse une nouvelle clé primaire pour hello compte de stockage. toodo cela :
<br/><br/>
<ol>
<li>Sélectionnez votre service BizTalk, puis <strong>Clés de synchronisation</strong>. Sélectionnez hello clé secondaire. Lorsque vous effectuez cette opération, hello BizTalk Service démarre à l’aide de la clé secondaire de hello.</li>
<li>Bonjour portail Azure classic, sélectionnez votre compte de stockage et régénérer hello clé primaire. N’oubliez pas, votre BizTalk Service est hello clé secondaire.</li>
<li>Sélectionnez votre service BizTalk, puis <strong>Clés de synchronisation</strong>. À présent, sélectionnez hello clé primaire. Cela est hello nouvelle clé primaire vous régénéré.</li>
<li>Bonjour portail Azure classic, sélectionnez votre compte de stockage et régénérer hello clé secondaire.</li>
</ol>
<br/>
On parle de « clés de substitution » pour décrire ce processus. objectif de Hello est tooswitch d’utilisateurs tooenable entre hello Primary Key et hello clé secondaire sans interrompre hello BizTalk Service.</td>
</tr>

<tr>
<td><strong>Supprimer</strong> votre application</td>
<td>Votre BizTalk Service et tous les éléments déployés tooit sont supprimés.</td>
</tr>
</table>


## <a name="monitor"></a>Surveiller
Ne s’applique pas toohello édition gratuite.

Lorsque vous sélectionnez le nom de votre BizTalk Service, onglet de surveillance hello est disponible et hello les informations suivantes :

##### <a name="metric-graph-displays-hello-selected-performance-metrics"></a>Graphique de métrique : Hello d’affiche sélectionné des métriques de performances
Ces métriques fournissent des valeurs en temps réel concernant l’intégrité hello hello BizTalk Service. Vous choisissez les mesures de performances devant s'afficher (jusqu'à six mesures de performances simultanément). 

Vous pouvez également choisir hello **relatif** ou **absolu** intervalle de temps de valeurs et hello **intervalle** des métriques hello sont affichées. 

##### <a name="tooremove-or-display-metrics-in-hello-graph"></a>tooremove ou l’affichage des métriques dans le graphique de hello :
1. Sélectionnez hello **moniteur** onglet.
2. Sélectionnez **ajouter des métriques** dans la barre des tâches hello :  
   ![Sélectionnez Ajouter des métriques.][AddMetrics]
3. Vérifiez les mesures de performances hello souhaité toodisplay.
4. Sélectionnez hello coche tooreturn toohello **moniteur** onglet.
5. Sélectionnez hello cercle suivant toohello métrique toodisplay les valeur de cette mesure dans le graphique de hello.  
   
    Par exemple, hello **l’utilisation du processeur** métrique est grisée ; sa sortie n’est pas affichée dans le graphique de hello :  
   ![La mesure Utilisation du processeur apparaît en grisé][GrayedMetric]  
   
    Sélectionnez hello grisée hello tooenable de cercle **l’utilisation du processeur** toodisplay métrique sa sortie dans le graphique de hello :  
   ![La mesure Utilisation du processeur est activée][EnabledMetric]
6. tooremove une métrique de graphique d’affichage hello et de la liste de hello, sélectionnez **supprimer une métrique** dans la barre des tâches hello. tooadd hello métrique toohello précédent la liste, sélectionnez **ajouter des métriques** dans la barre des tâches hello, vérifiez la métrique de hello et sélectionnez hello coche tooreturn toohello **moniteur** onglet. Sélectionnez hello grisée métrique de cercle tooenable hello.

## <a name="Metrics"></a>Mesures disponibles
Hello suivant des compteurs de performances est disponible :

<table border="1">

<tr>
<td><strong>Latence aller-retour</strong></td>
<td>Affiche le temps moyen de hello nécessaire en millisecondes (ms) les tooprocess que réception d’un message à partir du message de type hello hello temps jusqu'à ce que le message de type hello est entièrement traité par hello BizTalk Service sur tous les ponts. Seuls les messages correctement traités sont comptabilisés.<br/><br/>
En cas de hello suivant des événements, un horodatage est créé :
<ul>
<li>Message entre dans la passerelle de hello</li>
<li>Message est routé toohello destination</li>
<li>Une réponse de la destination est reçue</li>
<li>Destination accusé de réception réponse envoyée toohello passerelle</li>
</ul>
<br/>
Cette mesure indique le résultat hello Hello après le calcul :
<br/><br/>
[Destination accusé de réception réponse envoyée toohello passerelle] - [Message entre dans la passerelle de hello]</td>
</tr>
<tr>
<td><strong>Défaillances à la source</strong></td>
<td>Affiche le nombre total de hello de messages qui ont échoué par hello BizTalk Service lors de l’extraction des messages à partir de points de terminaison source hello.</td>
</tr>
<tr>
<td><strong>Utilisation du processeur</strong></td>
<td>Répertorie les hello % temps processeur moyen de toutes les instances de rôle.</td>
</tr>
<tr>
<td><strong>Latence de traitement</strong></td>
<td>Affiche la durée moyenne hello dans tooprocess millisecondes (ms) un message par hello BizTalk Service sur tous les ponts, à l’exclusion hello temps passé dans les destinations. Seuls les messages correctement traités sont comptabilisés.<br/><br/>
Lorsque chaque hello suivant des événements se produisent, un horodatage est créé :

<ul>
<li>Message entre dans la passerelle de hello</li>
<li>Message est routé toohello destination</li>
<li>Une réponse de la destination est reçue</li>
<li>Destination accusé de réception réponse envoyée toohello passerelle</li>
</ul>
<br/>Cette mesure indique le résultat hello Hello après le calcul :<br/><br/>
[Destination accusé de réception réponse envoyée toohello passerelle] - [Message entre dans la passerelle de hello] - [Destination réponse] + [Message est routé toohello destination]</td>
</tr>
<tr>
<td><strong>Défaillances dans le processus</strong></td>
<td>Affiche le nombre total de hello de messages ayant échoué au cours du traitement par hello BizTalk Service sur tous les ponts hello dans un intervalle de temps.</td>
</tr>
<tr>
<td><strong>Messages envoyés</strong></td>
<td>Affiche hello le nombre total de messages envoyés par hello BizTalk Service sur tous les ponts dans un intervalle de temps. Cette mesure est incrémentée lorsqu’un message envoyé à partir d’un pipeline atteint la destination de routage hello. Cette mesure n'indique pas qu'un message a été traité correctement.<br/><br/>
Dans un scénario de demande-réponse, la métrique de hello est incrémenté lorsque la destination de routage hello envoie un pipeline toohello arrière d’accusé de réception accusé de réception.</td>
</tr>
<tr>
<td><strong>Messages reçus</strong></td>
<td>Affiche hello le nombre total de messages reçus par hello BizTalk Service sur tous les ponts dans un intervalle de temps. Cette mesure est incrémentée lorsqu’un nouveau message est reçu par le pipeline de hello.</td>
</tr>
<tr>
<td><strong>Messages en cours de traitement</strong></td>
<td>Affiche hello nombre total de messages actuellement traités par hello BizTalk Service dans un intervalle de temps.</td>
</tr>
<tr>
<td><strong>Messages traités</strong></td>
<td>Affiche hello nombre total de messages traités correctement par hello BizTalk Service sur tous les ponts dans un intervalle de temps. Cette mesure est incrémentée lorsqu’un message est reçu avec succès par le pipeline de hello et de destination de toohello routé avec succès.</td>
</tr>
</table>


## <a name="scale"></a>Mettre à l'échelle
Dans l’onglet échelle hello, vous pouvez ajouter ou soustraire nombre hello d’unités utilisées par votre BizTalk Service. Par défaut, une seule unité est configurée. Unités supplémentaires peuvent être ajoutées tooscale votre BizTalk Service. Lorsque vous augmentez la montée en puissance hello, vous augmentez le débit. quantité Hello de ressources augmente également, y compris les ponts déployés, les contrats, les connexions métier et la puissance de traitement. Par exemple, vous augmentez échelle hello de 1 unité too2 unités. Dans ce cas, vous pouvez déployer hello double nombre de ponts, double accords de hello, double hello LOB connexions et une puissance de traitement hello double.

Certaines éditions BizTalk n'offrent pas de possibilité de mise à l'échelle. Dans ce cas, une seule unité est autorisée. toodetermine le nombre d’unités peut être monté en votre édition, consultez trop[Services BizTalk : tableau comparatif des éditions](biztalk-editions-feature-chart.md).

Augmentation du nombre hello d’unités peut affecter la tarification. Si vous augmentez les unités hello, en sélectionnant **enregistrer** affiche un message qui vous indique si la facturation est affectée. Vous choisissez ensuite toocontinue. Lorsque vous augmentez le nombre de hello d’unités, hello état du BizTalk Service remplace tooUpdating Active. Dans l’état de mise à jour de hello, votre BizTalk Service se poursuit toorun.

[Tableau comparatif des éditions de BizTalk Services](biztalk-editions-feature-chart.md) définit une « unité ».

## <a name="configure"></a>Configuration
Ne s’applique pas les connexions tooHybrid.

Définit tooNone d’état de la sauvegarde hello ou automatique. Lorsque la valeur tooNone, aucune sauvegarde n’est créés automatiquement. Lorsque la valeur tooAutomatic, vous configurez l’emplacement de sauvegarde hello, fréquence de sauvegarde de hello, combien de temps tookeep hello sauvegarder des fichiers et de hello. 

[Les Services BizTalk : Sauvegarde et restauration](biztalk-backup-restore.md) fournit des détails de hello. 

## <a name="HybridConnections"></a>Connexions hybrides
Connexions hybrides connectent à une application Windows Azure, telles que les applications Web ou des applications mobiles dans Azure App Service, la ressource locale tooan qui utilise un port TCP statique, tels que SQL Server, MySQL, API Web de HTTP et plus les Services Web personnalisés. Connexions hybrides sont gérées dans les Services BizTalk Bonjour portail Azure classic.

toocreate connexions hybrides dans Azure App Service, consultez [accès aux ressources locales à l’aide de connexions hybrides dans Azure App Service](../app-service-web/web-sites-hybrid-connection-get-started.md).

toocreate ou gérer des connexions hybrides dans Azure BizTalk Services, consultez [connexions hybrides](integration-hybrid-connection-overview.md).

## <a name="next"></a>Suivant
Maintenant que vous êtes familiarisé avec les différents onglets de hello, vous pouvez en savoir plus sur les fonctionnalités des Services BizTalk Azure hello :

* [Limitation dans BizTalk Services](biztalk-throttling-thresholds.md)  
* [Nom et clé de l'émetteur dans BizTalk Services](biztalk-issuer-name-issuer-key.md)  
* [Sauvegarde et restauration de BizTalk Services](biztalk-backup-restore.md)

## <a name="see-also"></a>Voir aussi
* [Connexions hybrides](integration-hybrid-connection-overview.md)  
* [Tableau comparatif des éditions Développeur, De base, Standard et Premium de BizTalk Services](biztalk-editions-feature-chart.md)  
* [BizTalk Services : approvisionnement à l’aide du portail Azure Classic](biztalk-provision-services.md)  
* [BizTalk Services : tableau comparatif des états du service BizTalk](biztalk-service-state-chart.md)  
* [Comment puis-je démarrer à l’aide de hello SDK des Services BizTalk Azure](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[Quickstart]: ./media/biztalk-dashboard-monitor-scale-tabs/QuickStartIcon.png
[AddMetrics]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_AddMetrics.png
[GrayedMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_GrayedMetric.png
[EnabledMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_EnabledMetric.png

