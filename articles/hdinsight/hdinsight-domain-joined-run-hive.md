---
title: "stratégies de ruche aaaConfigure dans HDInsight appartenant au domaine - Azure | Documents Microsoft"
description: "Découvrir..."
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 3fade1e5-c2e1-4ad5-b371-f95caea23f6d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/25/2016
ms.author: saurinsh
ms.openlocfilehash: 56f2bf9d872abc5f772b886fcf91c2e2422092f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hive-policies-in-domain-joined-hdinsight-preview"></a>Configuration de stratégies Hive dans HDInsight joint à un domaine (version préliminaire)
Découvrez comment les stratégies d’Apache Ranger tooconfigure pour la ruche. Dans cet article, vous créez deux Ranger stratégies toorestrict accès toohello hivesampletable. Hello hivesampletable est fourni avec des clusters HDInsight. Une fois que vous avez configuré des stratégies de hello, vous utilisez Excel et ODBC driver tooconnect tooHive les tables dans HDInsight.

## <a name="prerequisites"></a>Composants requis
* Un cluster HDInsight joint à un domaine. Consultez [Configuration de cluster HDInsight joints à un domaine](hdinsight-domain-joined-configure.md).
* Une station de travail avec Office 2016, Office 2013 ProPlus, Office 365 Pro Plus, l’édition autonome d’Excel 2013 ou Office Professionnel Plus 2010.

## <a name="connect-tooapache-ranger-admin-ui"></a>Se connecter tooApache Ranger l’interface utilisateur
**tooconnect tooRanger Admin UI**

1. À partir d’un navigateur, connectez-vous tooRanger Admin UI. URL de Hello est https://&lt;nom_cluster >.azurehdinsight.net/Ranger/.

   > [!NOTE]
   > Ranger utilise des informations d’identification différentes de celles du cluster Hadoop. navigateurs tooprevent à l’aide de la mise en cache des informations d’identification Hadoop, utiliser le nouveau navigateur inprivate fenêtre tooconnect toohello Ranger l’interface utilisateur.
   >
   >
2. Connectez-vous à l’aide du mot de passe et le nom d’utilisateur domaine hello cluster administrateur :

    ![Page d’accueil Ranger joint à un domaine HDInsight](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-ranger-home-page.png)

    Actuellement, Ranger fonctionne uniquement avec Yarn et Hive.

## <a name="create-domain-users"></a>Création d’utilisateurs du domaine
Dans [Configuration de clusters HDInsight joints à un domaine](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad), vous avez créé hiveruser1 et hiveuser2. Vous allez utiliser le compte d’utilisateur en deux hello dans ce didacticiel.

## <a name="create-ranger-policies"></a>Création de stratégies Ranger
Dans cette section, vous allez créer deux stratégies Ranger pour accéder à hivesampletable. Vous accordez une autorisation select sur différents ensembles de colonnes. Les deux utilisateurs ont été créés dans [Configuration de clusters HDInsight joints à un domaine](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad).  Dans la section suivante de hello, vous allez tester les deux stratégies de hello dans Excel.

**stratégies de Ranger toocreate**

1. Ouvrez l’interface utilisateur Ranger. Consultez [tooApache Ranger l’interface utilisateur de connexion](#connect-to-apache-ranager-admin-ui).
2. Cliquez sur **&lt;ClusterName>_hive** sous **Hive**. Deux stratégies préconfigurées doivent s’afficher.
3. Cliquez sur **ajouter une nouvelle stratégie**, puis entrez hello valeurs suivantes :

   * Nom de la stratégie : read-hivesampletable-all
   * Base de données Hive : par défaut
   * table : hivesampletable
   * Colonne Hive : *
   * Sélectionner un utilisateur : hiveuser1
   * Autorisations : select

     ![Configuration de stratégie Hive pour Ranger joint à un domaine HDInsight](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-configure-ranger-policy.png).

     > [!NOTE]
     > Si un utilisateur de domaine n’est pas rempli dans Sélectionner un utilisateur, attendez quelques instants pour Ranger les toosync avec AAD.
     >
     >
4. Cliquez sur **ajouter** stratégie de hello toosave.
5. Répétez hello deux dernières étapes toocreate une autre stratégie avec hello propriétés suivantes :

   * Nom de la stratégie : read-hivesampletable-devicemake
   * Base de données Hive : par défaut
   * table : hivesampletable
   * Colonne Hive : clientid, devicemake
   * Sélectionner un utilisateur : hiveuser2
   * Autorisations : select

## <a name="create-hive-odbc-data-source"></a>Création d’une source de données ODBC Hive
Vous trouverez des instructions Hello dans [source de données ODBC de la ruche créer](hdinsight-connect-excel-hive-odbc-driver.md).  

    Propriété|Description
    ---|---
    Data Source Name|Donner à une source de données tooyour nom
    Host|Entrez &lt;HDInsightClusterName>.azurehdinsight.net. Par exemple, myHDICluster.azurehdinsight.net
    Port|Utilisez <strong>443</strong>. (Ce port a été modifié à partir de too443 563.)
    Base de données|Utilisez <strong>Default</strong>.
    Hive Server Type|Sélectionnez <strong>Hive Server 2</strong>.
    Mechanism|Sélectionnez <strong>Azure HDInsight Service</strong>.
    HTTP Path|Laissez cette valeur vide.
    User Name|Entrez hiveuser1@contoso158.onmicrosoft.com. Mettre à jour de nom de domaine hello s’il est différent.
    Mot de passe|Entrez le mot de passe hello pour hiveuser1.
    </table>

Assurez-vous que tooclick **Test** avant d’enregistrer la source de données hello.

## <a name="import-data-into-excel-from-hdinsight"></a>Importation de données dans Microsoft Excel à partir de HDInsight
Dans la dernière section de hello, vous avez configuré deux stratégies.  hiveuser1 a hello l’autorisation select sur toutes les colonnes hello et hiveuser2 a hello l’autorisation select sur deux colonnes. Dans cette section, vous empruntez l’identité hello deux utilisateurs tooimport des données dans Excel.

1. Ouvrez un nouveau classeur ou un classeur existant dans Excel.
2. À partir de hello **données** , cliquez sur **d’autres Sources de données**, puis cliquez sur **à partir de l’Assistant de connexion données** toolaunch hello **Assistant de connexion de données**.

    ![Assistant Ouvrir la connexion de données][img-hdi-simbahiveodbc.excel.dataconnection]
3. Sélectionnez **DSN ODBC** comme source de données hello, puis cliquez sur **suivant**.
4. À partir de sources de données ODBC, sélectionnez hello source de données nom que vous avez créé à l’étape précédente de hello et puis cliquez sur **suivant**.
5. Nouveau mot de passe hello pour cluster hello dans l’Assistant de hello, puis cliquez sur **OK**. Attendez que hello **sélectionner une base de données et de Table** tooopen de la boîte de dialogue. Cette opération peut prendre quelques secondes.
6. Sélectionnez **hivesampletable**, puis cliquez sur **Suivant**.
7. Cliquez sur **Terminer**.
8. Bonjour **importer des données** boîte de dialogue, vous pouvez modifier ou spécifier la requête de hello. toodo, cliquez sur **propriétés**. Cette opération peut prendre quelques secondes.
9. Cliquez sur hello **définition** est du texte de la commande hello onglet :

       SELECT * FROM "HIVE"."default"."hivesampletable"

   Par des stratégies de Ranger hello que vous définies, hiveuser1 a l’autorisation select sur toutes les colonnes hello.  Par conséquent, cette requête fonctionne avec les informations d’identification de hiveuser1, mais cette requête ne fonctionne pas avec les informations d’identification de hiveuser2.

   ![Propriétés de connexion][img-hdi-simbahiveodbc-excel-connectionproperties]
10. Cliquez sur **OK** boîte de dialogue Propriétés de connexion tooclose hello.
11. Cliquez sur **OK** tooclose hello **importer des données** boîte de dialogue.  
12. Entrez à nouveau le mot de passe hello hiveuser1, puis cliquez sur **OK**. Il prend quelques secondes avant de données obtient tooExcel importé. Une fois terminé, 11 colonnes de données doivent s’afficher.

stratégie de deuxième tootest hello (en lecture-hivesampletable-devicemake) que vous avez créé dans la dernière section de hello

1. Ajoutez une nouvelle feuille dans Excel.
2. Suivez la dernière procédure tooimport hello les données de salutation.  Hello seul changement que vous prendrez est informations d’identification de toouse hiveuser2 au lieu de hiveuser1. Cela échoue car hiveuser2 a seulement deux colonnes de toosee d’autorisation. Vous obtiendra hello l’erreur suivante :

        [Microsoft][HiveODBC] (35) Error from Hive: error code: '40000' error message: 'Error while compiling statement: FAILED: HiveAccessControlException Permission denied: user [hiveuser2] does not have [SELECT] privilege on [default/hivesampletable/clientid,country ...]'.
3. Suivez hello même données tooimport de procédure. Cette fois-ci, utilisez les informations d’identification de hiveuser2 et également modifier instruction select de hello from :

        SELECT * FROM "HIVE"."default"."hivesampletable"

    to:

        SELECT clientid, devicemake FROM "HIVE"."default"."hivesampletable"

    Une fois terminé, deux colonnes de données importées doivent s’afficher.

## <a name="next-steps"></a>Étapes suivantes
* Pour configurer un cluster HDInsight joint à un domaine, consultez [Configuration de clusters HDInsight joints à un domaine](hdinsight-domain-joined-configure.md).
* Pour gérer un cluster HDInsight joint à un domaine, consultez [Gestion de clusters HDInsight joints à un domaine](hdinsight-domain-joined-manage.md).
* Pour exécuter des requêtes Hive en utilisant SSH sur des clusters HDInsight joints au domaine, voir [Utiliser SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).
* Pour la connexion de la ruche à l’aide de la ruche de JDBC, consultez [connecter tooHive sur Azure HDInsight à l’aide du pilote JDBC de la ruche de hello](hdinsight-connect-hive-jdbc-driver.md)
* Pour la connexion tooHadoop Excel à l’aide de la ruche de ODBC, consultez [tooHadoop connexion Excel avec hello pilote ODBC de la ruche de Microsoft](hdinsight-connect-excel-hive-odbc-driver.md)
* Pour la connexion tooHadoop Excel à l’aide de Power Query, consultez [tooHadoop Excel de se connecter à l’aide de Power Query](hdinsight-connect-excel-power-query.md)
