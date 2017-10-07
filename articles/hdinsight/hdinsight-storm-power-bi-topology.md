---
title: aaaUse Apache Storm avec Power BI - Azure HDInsight | Documents Microsoft
description: "Créez un rapport Power BI en utilisant les données d’une topologie C# s’exécutant sur un cluster Apache Storm dans HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 36fe3b9c-5232-4464-8d75-95403b6da7a1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/31/2017
ms.author: larryfr
ms.openlocfilehash: 194cd8220bd60475af1d64a110e4b23ef92e1bc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-power-bi-toovisualize-data-from-an-apache-storm-topology"></a>Utiliser les données de toovisualize Power BI à partir d’une topologie d’Apache Storm

Power BI vous permet d’afficher les données toovisually sous forme de rapports. Ce document fournit un exemple de procédure toouse Apache Storm sur les données de toogenerate HDInsight pour Power BI.

> [!NOTE]
> Hello étapes décrites dans ce document reposent sur un environnement de développement Windows avec Visual Studio. projet compilé de Hello peut être soumis tooa HDInsight de basés sur Linux cluster. Seuls les clusters basés sur Linux créés après le 28/10/2016 prennent en charge les topologies SCP.NET.
>
> toouse une topologie c# avec un cluster basé sur Linux, hello de mise à jour de package NuGet de Microsoft.SCP.Net.SDK utilisé par votre projet de tooversion 0.10.0.6 ou une version ultérieure. version Hello du package de hello doit également correspondre version majeure de hello de Storm installé sur HDInsight. Par exemple, Storm sur les versions 3.3 et 3.4 de HDInsight utilise Storm 0.10.x, tandis que HDInsight 3.5 utilise Storm 1.0.x.
>
> Topologies c# sur des clusters basés sur Linux doivent utiliser .NET 4.5 et utiliser toorun Mono sur le cluster HDInsight de hello. La plupart des éléments fonctionnent. Toutefois, vous devez vérifier hello [Mono compatibilité](http://www.mono-project.com/docs/about-mono/compatibility/) document pour identifier les éventuelles incompatibilités.
>
> Pour obtenir une version Java de ce projet, qui fonctionne avec HDInsight Linux ou Windows, consultez [Traitement des événements Azure Event Hubs avec Storm sur HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).

## <a name="prerequisites"></a>Composants requis

* Un utilisateur Azure Active Directory avec un accès [Power BI](https://powerbi.com).
* Un cluster HDInsight. Pour plus d’informations, consultez [Prise en main de Storm sur HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).

  > [!IMPORTANT]
  > Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* (L’une des versions suivantes de hello) de Visual Studio

  * Visual Studio 2012 avec [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)
  * Visual Studio 2013 avec [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) ou [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)
  * [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
  * Visual Studio 2017 (toute édition)

* Hello outils HDInsight pour Visual Studio : consultez [prise en main à l’aide des outils de hello HDInsight pour Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) pour plus d’informations sur les informations d’installation.

## <a name="how-it-works"></a>Fonctionnement

Cet exemple contient une topologie Storm en C# qui génère de façon aléatoire les données du journal Internet Information Services (IIS). Ces données sont ensuite écrites tooa base de données SQL, et à partir de là, il est utilisé toogenerate des rapports dans Power BI.

Hello suivant fichiers implémentent hello principales fonctionnalités de cet exemple :

* **SqlAzureBolt.cs**: écrit les informations de produit dans hello Storm topologie tooSQL de base de données.
* **IISLogsTable.sql**: hello Transact-SQL instructions utilisées toogenerate hello base de données stockées dans les données de salutation.

> [!WARNING]
> Créer la table de hello dans la base de données SQL avant le début de la topologie de hello sur votre cluster HDInsight.

## <a name="download-hello-example"></a>Télécharger l’exemple de hello

Télécharger hello [exemple de HDInsight c# Storm Power BI](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi). toodownload, une branche/clonage à l’aide de [git](http://git-scm.com/), ou utilisez hello **télécharger** toodownload de lier un fichier ZIP d’archive de hello.

## <a name="create-a-database"></a>Créer une base de données

1. toocreate une base de données, utilisez les étapes de hello Bonjour [didacticiel de base de données SQL](../sql-database/sql-database-get-started.md) document.

2. Base de données toohello de se connecter par hello suivant les étapes dans hello [connecter tooa base de données SQL avec Visual Studio](../sql-database/sql-database-connect-query.md) document.

3. Dans l’Explorateur d’objets, avec le bouton droit de la base de données hello et sélectionnez **nouvelle requête**. Coller le contenu de hello hello **IISLogsTable.sql** fichier inclus dans hello téléchargé le projet dans la fenêtre de requête hello, puis utilisez Ctrl + Maj + E tooexecute hello requête. Vous devez recevoir un message qui hello commandes s’est terminées correctement.

## <a name="configure-hello-sample"></a>Configurer l’exemple hello

1. À partir de hello [portail Azure](https://portal.azure.com), sélectionnez votre base de données SQL. À partir de hello **Essentials** section hello de base de données du Panneau de SQL, sélectionnez **afficher les chaînes de connexion de base de données**. À partir de la liste hello qui s’affiche, copiez hello **ADO.NET (authentification SQL)** plus d’informations.

2. Ouvrez l’exemple hello dans Visual Studio. À partir de **l’Explorateur de solutions**, ouvrez hello **App.config** de fichiers et recherchez hello entrée suivante :

        <add key="SqlAzureConnectionString" value="##TOBEFILLED##" />

    Remplacez hello **TOBEFILLED ## ##** valeur avec la chaîne de connexion de base de données hello copiée à l’étape précédente de hello. Remplacez **{votre\_nom d’utilisateur}** et **{votre\_mot de passe}** avec le nom d’utilisateur hello et le mot de passe pour la base de données hello.

3. Enregistrez et fermez les fichiers hello.

## <a name="deploy-hello-sample"></a>Déployer l’exemple hello

1. À partir de **l’Explorateur de solutions**, avec le bouton hello **StormToSQL** de projet et sélectionnez **envoyer tooStorm sur HDInsight**. Cluster HDInsight de hello SELECT à partir de hello **Cluster Storm** boîte de dialogue de liste déroulante.

   > [!NOTE]
   > Il peut prendre quelques secondes que hello **Cluster Storm** toopopulate de liste déroulante des noms de serveur.
   >
   > Si vous y êtes invité, entrez les informations d’identification de connexion hello pour votre abonnement Azure. Si vous avez plusieurs abonnements, connectez-vous toohello qui contient votre Storm sur le cluster HDInsight.

2. Lors de la topologie de hello a été envoyée, hello __visionneuse de topologie__ s’affiche. tooview cette topologie, l’entrée de SqlAzureWriterTopology hello select à partir de la liste de hello.

    ![topologies de Hello, avec la topologie hello sélectionné](./media/hdinsight-storm-power-bi-topology/topologyview.png)

    Vous pouvez utiliser cette toosee afficher des informations sur la topologie de hello ou double-cliquez sur un composant entrée (par exemple hello SqlAzureBolt) toosee informations tooa spécifique dans une topologie de hello.

3. Après avoir hello topologie a exécuté pendant quelques minutes, fenêtre de requête SQL toohello retour vous avez utilisé la base de données toocreate hello. Remplacez les instructions existantes hello hello suivant la requête :

        select * from iislogs;

    Utilisez Ctrl + Maj + requête de hello tooexecute E et vous devez réception toohello similaire de résultats données suivantes :

        1    2016-05-27 17:57:14.797    255.255.255.255    /bar    GET    200
        2    2016-05-27 17:57:14.843    127.0.0.1    /spam/eggs    POST    500
        3    2016-05-27 17:57:14.850    123.123.123.123    /eggs    DELETE    200
        4    2016-05-27 17:57:14.853    127.0.0.1    /foo    POST    404
        5    2016-05-27 17:57:14.853    10.9.8.7    /bar    GET    200
        6    2016-05-27 17:57:14.857    192.168.1.1    /spam    DELETE    200

    Ces données ont été écrites à partir de la topologie de Storm hello.

## <a name="create-a-report"></a>Créer un rapport

1. Se connecter toohello [connecteur de base de données SQL Azure](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) pour Power BI. 

2. Dans **Databases** (Bases de données), sélectionnez **Get** (Obtenir).

3. Sélectionnez **Azure SQL Database** (Base de données SQL Microsoft Azure), puis sélectionnez **Connect** (Se connecter).

    > [!NOTE]
    > Vous pouvez être invité à toodownload hello Power BI Desktop toocontinue. Dans ce cas, utilisez hello suivant les étapes tooconnect :
    >
    > 1. Ouvrez Power BI Desktop et sélectionnez __obtenir les données__.
    > 2 - Sélectionnez __Azure__, puis sélectionnez __Base de données Azure SQL__.

4. Entrez hello informations tooconnect tooyour base de données SQL Azure. Vous pouvez trouver ces informations en visitant hello [portail Azure](https://portal.azure.com) et en sélectionnant votre base de données SQL.

   > [!NOTE]
   > Vous pouvez également définir un intervalle d’actualisation hello et des filtres personnalisés à l’aide de **activer les Options avancées** hello à partir de la boîte de dialogue connexion.

5. Une fois que vous vous êtes connecté, vous verrez un nouveau dataset avec hello que même nom en tant que base de données hello, vous êtes connecté. Sélectionnez toobegin de jeu de données hello conception d’un rapport.

6. À partir de **champs**, développez hello **IISLOGS** entrée. toocreate provient d’un rapport que listes hello URI, cochez la case hello **URISTEM**.

    ![Création d’un rapport](./media/hdinsight-storm-power-bi-topology/createreport.png)

7. Ensuite, faites glisser **méthode** toohello rapport. Bonjour rapport mises à jour toolist Bonjour découle et méthode HTTP correspondante de hello utilisé pour hello requête HTTP.

    ![Ajout de données de la méthode hello](./media/hdinsight-storm-power-bi-topology/uristemandmethod.png)

8. À partir de hello **visualisations** colonne, sélectionnez hello **champs** icône, puis sélectionnez hello bas ensuite trop**méthode** Bonjour **valeurs**section. toodisplay a accédé au nombre de combien de fois un URI, sélectionnez **nombre**.

    ![Nombre de tooa des méthodes de modification](./media/hdinsight-storm-power-bi-topology/count.png)

9. Ensuite, sélectionnez hello **empilé** toochange affichage des informations de hello.

    ![Modification tooa empilé](./media/hdinsight-storm-power-bi-topology/stackedcolumn.png)

10. rapport de hello toosave, sélectionnez **enregistrer** et entrez un nom pour le rapport de hello.

## <a name="stop-hello-topology"></a>Arrêter la topologie de hello

topologie de Hello continue toorun jusqu'à ce que vous l’arrêtez ou supprimez hello Storm sur le cluster HDInsight. toostop hello topologie, effectuer hello comme suit :

1. Dans Visual Studio, renvoyer la visionneuse de topologie toohello et sélectionnez hello topologie.

2. Sélectionnez hello **Kill** topologie de bouton toostop hello.

    ![Kill sur la topologie hello résumé bouton](./media/hdinsight-storm-power-bi-topology/killtopology.png)

## <a name="delete-your-cluster"></a>Supprimer votre cluster

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Étapes suivantes

Dans ce document, vous avez appris comment le toosend des données à partir d’un tooSQL de topologie tempête de base de données, puis pour visualiser les données hello à l’aide de Power BI. Pour plus d’informations sur la façon de toowork avec d’autres technologies Azure à l’aide de Storm sur HDInsight, consultez hello suivant du document :

* [Exemples de topologies pour Storm dans HDInsight](hdinsight-storm-example-topology.md)
