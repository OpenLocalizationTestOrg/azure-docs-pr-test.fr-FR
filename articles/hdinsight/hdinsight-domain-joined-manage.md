---
title: "les clusters appartenant à un domaine de HDInsight aaaManage - Azure | Documents Microsoft"
description: "Découvrez comment toomanage clusters appartenant à un domaine de HDInsight"
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 6ebc4d2f-2f6a-4e1e-ab6d-af4db6b4c87c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/25/2016
ms.author: saurinsh
ms.openlocfilehash: 233ddf0953e981f9a24b77d9dde194d590e5e6d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-domain-joined-hdinsight-clusters-preview"></a>Gestion des clusters HDInsight joints à un domaine (version préliminaire)
Découvrez les utilisateurs hello et rôles hello dans HDInsight de domaine, et comment toomanage clusters HDInsight de joints au domaine.

## <a name="users-of-domain-joined-hdinsight-clusters"></a>Utilisateurs des clusters HDInsight joints à un domaine
Un cluster HDInsight n'est pas joint au domaine a deux comptes d’utilisateur qui sont créés lors de la création du cluster hello :

* **Administrateur Ambari** : ce compte est également appelé *utilisateur Hadoop* ou *utilisateur HTTP*. Ce compte peut être utilisé toolog sur tooAmbari à https://&lt;nomcluster >. azurehdinsight.net. Peut également être toorun utilisé des requêtes sur les vues de Ambari, exécuter des travaux à l’aide des outils externes (par exemple, PowerShell, Templeton, Visual Studio) et s’authentifier avec le pilote ODBC de la ruche de hello et Outils BI (par exemple, Excel, Power BI ou Tableau).
* **Utilisateur SSH** : ce compte peut être utilisé avec SSH et exécuter des commandes sudo. Il possède des privilèges de racine toohello les machines virtuelles Linux.

Un cluster HDInsight appartenant au domaine a trois nouveaux utilisateurs dans Ajout tooAmbari Admin et SSH de l’utilisateur.

* **Ranger admin**: ce compte est hello local Apache Ranger admin. Il ne s’agit pas d’un utilisateur de domaine Active Directory. Ce compte peut être toosetup utilisé des stratégies et effectuer d’autres administrateurs d’utilisateurs ou les administrateurs délégués (de sorte que les utilisateurs peuvent gérer les stratégies). Par défaut, le nom d’utilisateur hello est *admin* et le mot de passe hello est hello identique hello Ambari mot de passe administrateur. mot de passe Hello peut être mis à jour à partir de la page de paramètres hello dans Ranger.
* **Utilisateur de domaine administrateur de cluster**: ce compte est un utilisateur de domaine Active Directory désigné comme administrateur de cluster Hadoop notamment Ambari et Ranger de hello. Vous devez fournir les informations d’identification de cet utilisateur lors de la création du cluster. Cet utilisateur a hello suivant de privilèges :

  * Joindre le domaine de toohello d’ordinateurs et les placer dans hello unité d’organisation que vous spécifiez lors de la création du cluster.
  * Créer des principaux de service au sein de hello unité d’organisation que vous spécifiez lors de la création du cluster.
  * Créer des entrées DNS inversées.

    Hello de Remarque autres utilisateurs AD également posséder les privilèges.

    Il existe certains points de terminaison dans le cluster hello (par exemple, Templeton) qui ne sont pas gérés par Ranger et par conséquent, ne sont pas sécurisées. Ces points de terminaison sont verrouillés pour tous les utilisateurs à l’exception de l’utilisateur de domaine du cluster admin hello.
* **Standard** : pendant la création du cluster, vous pouvez fournir plusieurs groupes Active Directory. les utilisateurs de Hello dans ces groupes seront synchronisé tooRanger et Ambari. Ces utilisateurs sont des utilisateurs de domaine et ont accès tooonly gérés Ranger points de terminaison (par exemple, Hiveserver2). Tous les hello stratégies RBAC et d’audit seront les utilisateurs toothese applicable.

## <a name="roles-of-domain-joined-hdinsight-clusters"></a>Rôles des clusters HDInsight joints à un domaine
HDInsight de domaine ont hello suivant des rôles :

* Administrateur de cluster
* Opérateur de cluster
* Administrateur de services
* Opérateur de service
* Utilisateur de cluster

**autorisations de hello toosee de ces rôles.**

1. Ouvrez hello Ambari interface utilisateur de gestion.  Consultez [hello ouvrir l’interface utilisateur de gestion de Ambari](#open-the-ambari-management-ui).
2. Dans le menu de gauche hello, cliquez sur **rôles**.
3. Cliquez sur hello bleu interrogation toosee hello des autorisations :

    ![Autorisations des rôles de HDInsight joint à un domaine](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-roles-permissions.png)

## <a name="open-hello-ambari-management-ui"></a>Ouvrez hello Ambari interface utilisateur de gestion
1. Ouverture de session toohello [portail Azure](https://portal.azure.com).
2. Ouvrez votre cluster HDInsight dans un panneau. Voir [Énumération et affichage des clusters](hdinsight-administer-use-management-portal.md#list-and-show-clusters).
3. Cliquez sur **tableau de bord** de hello menu supérieur tooopen Ambari.
4. Ouvrez une session sur tooAmbari à l’aide de hello cluster administrateur domaine nom d’utilisateur et mot de passe.
5. Cliquez sur hello **Admin** menu déroulant dans le coin supérieur droit de hello, puis cliquez sur **Ambari de gérer**.

    ![Gérer Ambari HDInsight joint à un domaine](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-manage-ambari.png)

    l’interface utilisateur de Hello ressemble à ceci :

    ![Interface utilisateur de gestion Ambari HDInsight joint à un domaine](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui.png)

## <a name="list-hello-domain-users-synchronized-from-your-active-directory"></a>Liste des utilisateurs du domaine hello synchronisés à partir de votre annuaire Active Directory
1. Ouvrez hello Ambari interface utilisateur de gestion.  Consultez [hello ouvrir l’interface utilisateur de gestion de Ambari](#open-the-ambari-management-ui).
2. Dans le menu de gauche hello, cliquez sur **utilisateurs**. Vous allez voir que tous les utilisateurs de hello synchronisés à partir de votre cluster HDInsight de toohello Active Directory.

    ![Énumération des utilisateurs interface utilisateur de gestion Ambari HDInsight joint à un domaine](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-users.png)

## <a name="list-hello-domain-groups-synchronized-from-your-active-directory"></a>Liste des groupes de domaine hello synchronisés à partir de votre annuaire Active Directory
1. Ouvrez hello Ambari interface utilisateur de gestion.  Consultez [hello ouvrir l’interface utilisateur de gestion de Ambari](#open-the-ambari-management-ui).
2. Dans le menu de gauche hello, cliquez sur **groupes**. Vous allez voir que tous les groupes de hello synchronisés à partir de votre cluster HDInsight de toohello Active Directory.

    ![Énumération des groupes interface utilisateur de gestion Ambari HDInsight joint à un domaine](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-groups.png)

## <a name="configure-hive-views-permissions"></a>Configuration des autorisations des affichages Hive
1. Ouvrez hello Ambari interface utilisateur de gestion.  Consultez [hello ouvrir l’interface utilisateur de gestion de Ambari](#open-the-ambari-management-ui).
2. Dans le menu de gauche hello, cliquez sur **vues**.
3. Cliquez sur **HIVE** détails de hello tooshow.

    ![Affichages Hive interface utilisateur de gestion Ambari HDInsight joint à un domaine](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views.png)
4. Cliquez sur hello **affichage de la ruche** de lier des vues de la ruche tooconfigure.
5. Faites défiler vers le bas toohello **autorisations** section.

    ![Configuration des autorisations affichages Hive interface utilisateur de gestion Ambari HDInsight joint à un domaine](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views-permissions.png)
6. Cliquez sur **ajouter un utilisateur** ou **ajouter un groupe**, puis spécifiez les utilisateurs hello ou groupes qui peuvent utiliser les vues de la ruche.

## <a name="configure-users-for-hello-roles"></a>Configurer des utilisateurs pour les rôles de hello
 toosee une liste de rôles et leurs autorisations, consultez [clusters HDInsight de rôles de domaine](#roles-of-domain---joined-hdinsight-clusters).

1. Ouvrez hello Ambari interface utilisateur de gestion.  Consultez [hello ouvrir l’interface utilisateur de gestion de Ambari](#open-the-ambari-management-ui).
2. Dans le menu de gauche hello, cliquez sur **rôles**.
3. Cliquez sur **ajouter un utilisateur** ou **ajouter un groupe** tooassign les utilisateurs et groupes de rôles de toodifferent.

## <a name="next-steps"></a>Étapes suivantes
* Pour configurer un cluster HDInsight joint à un domaine, consultez [Configuration de clusters HDInsight joints à un domaine](hdinsight-domain-joined-configure.md).
* Pour configurer des stratégies Hive et exécuter des requêtes Hive, consultez [Configuration de stratégies Hive pour les clusters HDInsight joints à un domaine](hdinsight-domain-joined-run-hive.md).
* Pour exécuter des requêtes Hive en utilisant SSH sur des clusters HDInsight joints au domaine, voir [Utiliser SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).
