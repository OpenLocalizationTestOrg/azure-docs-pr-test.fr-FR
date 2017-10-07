---
title: "événements aaaCorrelate au fil du temps avec Storm et HBase sur HDInsight"
description: "Découvrez comment toocorrelate les événements qui arrivent à des moments différents, à l’aide de Storm et HBase sur HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 17d11479-2d02-4790-8d29-05fb38351479
ms.service: hdinsight
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: f915eef77bbda5b02bfd02ad0b5a4923ff2f4f26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="correlate-events-that-arrive-at-different-times-using-storm-and-hbase"></a>Corrélation des événements au fil du temps avec Storm et HBase

En utilisant une banque de données persistante avec Apache Storm, vous pouvez associer les entrées de données qui arrivent à des moments différents. Par exemple, lier des événements de connexion et de déconnexion pour un toocalculate de session utilisateur comment durée pendant laquelle les session hello a duré.

Dans ce document, vous apprendrez comment toocreate une topologie c# tempête de base qui effectue le suivi des événements de connexion et déconnexion des sessions de l’utilisateur et calcule la durée hello de session de hello. topologie de Hello utilise HBase comme un magasin de données persistantes. HBase vous permet également tooperform les requêtes de traitement par lots sur des informations supplémentaires du tooproduce hello les données d’historique. telles que le nombre de sessions utilisateur ayant démarré ou ayant pris fin pendant une période spécifique.

## <a name="prerequisites"></a>Composants requis

* Visual Studio et hello HDInsight tools pour Visual Studio. Pour plus d’informations, consultez [prise en main à l’aide des outils de hello HDInsight pour Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

* Apache Storm sur un cluster HDInsight (Windows).

  > [!WARNING]
  > Ne SCP.NET topologies sont pris en charge sur des clusters basés sur Linux une tempête créés après le 28/10/2016, hello HBase SDK pour le package .NET disponible à partir du 28/10/2016 ne fonctionne pas correctement sur HDInsight de basés sur Linux

* Un cluster Apache HBase sur HDInsight (Linux ou Windows).

  > [!IMPORTANT]
  > Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* [Java](https://java.com) 1.7 ou version ultérieure sur votre environnement de développement. Java est utilisé toopackage hello topologie lorsqu’il est soumis toohello HDInsight cluster.

  * Hello **JAVA_HOME** environnement variable doit toohello de point de répertoire qui contient Java.
  * Hello **%JAVA_HOME%/bin** répertoire doit être dans le chemin d’accès de hello

## <a name="architecture"></a>Architecture

![Diagramme du flux de données hello via la topologie de hello](./media/hdinsight-storm-correlation-topology/correlationtopology.png)

Corrélation des événements requiert l’un identificateur commun pour la source d’événement hello. Par exemple, un ID d’utilisateur, ID de session ou autre élément de données qui est un) unique et (b) inclus dans toutes les données envoyées tooStorm. Cet exemple utilise un toorepresent de valeur GUID d’un ID de session.

Cet exemple se compose de deux clusters HDInsight :

* HBase : magasin de données persistant pour les données d’historique
* Storm : utilisé tooingest les données entrantes

les données de salutation sont générées aléatoirement par topologie de Storm hello et comprend hello éléments suivants :

* Session ID : GUID qui identifie de façon unique chaque session
* Event : événement START ou END Pour cet exemple, START se produit toujours avant END
* : Hello heure de l’événement de hello.

Ces données sont traitées et stockées dans HBase.

### <a name="storm-topology"></a>Topologie Storm

Lorsqu’une session démarre, une **Démarrer** événement est reçu par la topologie de hello et connecté tooHBase. Lorsqu’un **fin** événement est reçu, la topologie de hello récupère hello **Démarrer** événement et calcule la durée hello entre hello deux. Cela **durée** valeur est ensuite stockée dans HBase avec hello **fin** informations sur les événements.

> [!IMPORTANT]
> Alors que cette topologie illustre un modèle de base hello, une solution de production devez tootake conception pourquoi les scénarios suivants :
>
> * Événements se produisant dans le désordre
> * Événements en double
> * Événements supprimés

exemple de topologie Hello est composée de hello suivant des composants :

* Session.cs : simule une session utilisateur en créant un ID de session aléatoire, dure de session hello heure et la durée pendant laquelle démarrer.

* Spout.cs : crée 100 sessions, émet un événement de début, attend un délai aléatoire de hello pour chaque session, puis émet un événement de fin. Recycle terminé sessions toogenerate nouveaux.

* HBaseLookupBolt.cs : utilise hello session ID toolook des informations de session dans HBase. Lorsqu’un événement de fin est traité, il recherche les événements de début correspondante hello et calcule la durée hello de session de hello.

* HBaseBolt.cs : stocke les informations dans HBase.

* TypeHelper.cs : Aide à la conversion de type lors de la lecture / écriture tooHBase.

### <a name="hbase-schema"></a>Schéma HBase

Dans HBase, les données de salutation sont stockées dans une table avec hello suivant/paramètres du schéma :

* Clé de ligne : hello ID de session est utilisé en tant que clé hello pour les lignes de cette table.

* Famille de colonne : nom de famille hello est 'cf'. Les colonnes stockées dans cette famille sont :

  * event : START ou END.

  * Durée : durée hello en millisecondes hello événement s’est produite.

  * Durée : hello longueur entre l’événement de début et de fin.

* VERSIONS : famille de 'cf' hello a pour valeur tooretain 5 des versions de chaque ligne.

  > [!NOTE]
  > Les versions sont un journal des valeurs précédentes stockées pour une clé de ligne spécifique. Par défaut, HBase retourne uniquement la valeur hello pour la version la plus récente d’une ligne hello. Dans ce cas, hello même ligne est utilisé pour tous les événements (début, fin.) pour que chaque version d’une ligne est identifiée par la valeur d’horodateur hello. Les versions fournissent une vue historique des événements consignés pour un ID spécifique.

## <a name="download-hello-project"></a>Télécharger le projet de hello

exemple de projet Hello peut être téléchargé à partir de [https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation](https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation).

Ce téléchargement contient hello suivant les projets c# :

* CorrelationTopology : topologie Storm C# qui émet de manière aléatoire des événements start et end pour les sessions utilisateur. Chaque session dure entre 1 et 5 minutes.

* SessionInfo : Application console c# qui crée la table HBase à hello et fournit des exemples de requêtes tooreturn d’informations sur les données de session stockée.

## <a name="create-hello-table"></a>Créer la table de hello

1. Ouvrez hello **SessionInfo** projet dans Visual Studio.

2. Dans **l’Explorateur de solutions**, avec le bouton hello **SessionInfo** de projet et sélectionnez **propriétés**.

    ![Capture d’écran de menu avec les propriétés sélectionnées](./media/hdinsight-storm-correlation-topology/selectproperties.png)

3. Sélectionnez **paramètres**, puis hello de l’ensemble des valeurs suivantes :

   * HBaseClusterURL : cluster de HBase tooyour hello URL. Par exemple, https://myhbasecluster.azurehdinsight.net.

   * HBaseClusterUserName : compte d’utilisateur admin/HTTP hello pour votre cluster

   * HBaseClusterPassword : mot de passe hello pour le compte d’utilisateur admin/HTTP hello

   * HBaseTableName : nom de hello de toouse de table hello avec cet exemple

   * HBaseTableColumnFamily : nom de famille de colonne hello

     ![Image de la boîte de dialogue Paramètres](./media/hdinsight-storm-correlation-topology/settings.png)

4. Exécutez la solution de hello. Lorsque vous y êtes invité, sélectionnez table de hello toocreate clé hello « c » sur votre cluster HBase.

## <a name="build-and-deploy-hello-storm-topology"></a>Générer et déployer la topologie de Storm hello

1. Ouvrez hello **CorrelationTopology** solution dans Visual Studio.

2. Dans **l’Explorateur de solutions**, avec le bouton hello **CorrelationTopology** de projet et sélectionnez Propriétés.

3. Dans la fenêtre de propriétés hello, sélectionnez **paramètres** et entrez les valeurs de configuration hello pour ce projet. 5 premiers Hello sont hello les mêmes valeurs utilisées par hello **SessionInfo** projet :

   * HBaseClusterURL : cluster de HBase tooyour hello URL. Par exemple, https://myhbasecluster.azurehdinsight.net.

   * HBaseClusterUserName : compte d’utilisateur admin/HTTP hello pour votre cluster.

   * HBaseClusterPassword : hello mot de passe de compte d’utilisateur admin/HTTP hello.

   * HBaseTableName : nom de hello de toouse de table hello avec cet exemple. Cette valeur est hello même nom de la table utilisée dans le projet de SessionInfo hello.

   * HBaseTableColumnFamily : nom de famille colonne hello. Cette valeur est hello même nom de famille de colonne utilisée dans le projet de SessionInfo hello.

   > [!IMPORTANT]
   > Ne modifiez pas hello HBaseTableColumnNames, comme valeurs par défaut de la hello sont utilisées par des noms de hello **SessionInfo** tooretrieve données.

4. Enregistrer les propriétés de hello, puis générez le projet de hello.

5. Dans **l’Explorateur de solutions**, cliquez sur le projet de hello et sélectionnez **envoyer tooStorm sur HDInsight**. Si vous y êtes invité, entrez les informations d’identification de l’hello pour votre abonnement Azure.

   ![Image de hello envoyer l’élément de menu toostorm](./media/hdinsight-storm-correlation-topology/submittostorm.png)

6. Bonjour **soumettre une topologie** boîte de dialogue, cluster Storm de hello sélectionnez vous que toodeploy cette topologie.

   > [!NOTE]
   > Hello première fois que vous envoyez une topologie, il peut prendre quelques secondes nom de hello tooretrieve vos clusters HDInsight.

7. Une fois que la topologie de hello, a été téléchargé et soumis toohello cluster hello **affichage de la topologie Storm** s’ouvre et affiche hello topologie en cours d’exécution. les données de salutation toorefresh, sélectionnez hello **CorrelationTopology** et utiliser le bouton d’actualisation hello en hello haut à droite de la page de hello.

   ![Image de l’affichage de la topologie hello](./media/hdinsight-storm-correlation-topology/topologyview.png)

   Lors de la topologie de hello commence à générer des données, hello valeur Bonjour **EMISE** par incréments de colonne.

   > [!NOTE]
   > Si hello **affichage de la topologie Storm** ne pas ouvrir automatiquement, utilisez hello suivant les étapes tooopen il :
   >
   > 1. Dans l’**Explorateur de solutions**, développez **Azure**, puis **HDInsight**.
   > 2. Cluster avec le bouton hello Storm hello topologie est en cours d’exécution, puis sélectionnez **vue Storm Topologies**

## <a name="query-hello-data"></a>Interroger des données hello

Une fois que les données a été émises, utilisez hello étapes tooquery hello données suivantes.

1. Retourner toohello **SessionInfo** projet. S’il n’est pas en cours d’exécution, démarrez une nouvelle instance du projet.

2. Lorsque vous y êtes invité, sélectionnez **s** toosearch pour l’événement de début. Vous sont demandée tooenter de début et de fin de temps toodefine une plage de temps - seuls les événements entre ces deux heures sont retournés.

    Suivant de hello utilisez mettre en forme lors de l’entrée de démarrage de hello et heure de fin : hh : mm et « am » ou « pm ». Par exemple, 11:20.

    tooreturn connecté, événements, utilisez une heure de début avant hello Storm topologie a été déployée à partir d’et une heure de fin de maintenant. les données de retour Hello contient toohello similaire d’entrées après le texte :

        Session e6992b3e-79be-4991-afcf-5cb47dd1c81c started at 6/5/2015 6:10:15 PM. Timestamp = 1433527820737

Recherche de hello de fin événements fonctionne même en tant qu’événements de début. Toutefois, les événements de fin sont générés au hasard entre 1 et 5 minutes après l’événement de début hello. Vous avez peut-être tootry quelques événements de fin de hello de toofind de plages de temps. Événements de fin contiennent également durée hello de session hello - différence hello entre l’heure de l’événement START hello et événements de fin. Voici un exemple de données pour les événements END :

    Session fc9fa8e6-6892-4073-93b3-a587040d892e lasted 2 minutes, and ended at 6/5/2015 6:12:15 PM

> [!NOTE]
> Alors que les valeurs de durée hello que vous entrez sont en heure locale, temps hello renvoyés par la requête de hello est au format UTC.

## <a name="stop-hello-topology"></a>Arrêter la topologie de hello

Lorsque vous êtes topologie de hello toostop prêt, retourner toohello **CorrelationTopology** projet dans Visual Studio. Bonjour **affichage de la topologie Storm**, sélectionnez la topologie de hello et l’utiliser hello **Kill** bouton en haut de hello d’affichage de la topologie hello.

## <a name="delete-your-cluster"></a>Supprimer votre cluster

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’exemples Storm, consultez la page [Exemples de topologies pour Storm dans HDInsight](hdinsight-storm-example-topology.md).
