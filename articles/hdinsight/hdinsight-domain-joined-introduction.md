---
title: "sécurité aaaHadoop - appartenant au domaine des clusters HDInsight - Azure | Documents Microsoft"
description: "Découvrir..."
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7dc6847d-10d4-4b5c-9c83-cc513cf91965
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/31/2016
ms.author: saurinsh
ms.openlocfilehash: 5a9469402a61bcba4017e1ff4bd06dfba23ac963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-toohadoop-security-with-domain-joined-hdinsight-clusters-preview"></a>Une présentation de la sécurité tooHadoop avec des clusters de HDInsight appartenant à un domaine (version préliminaire)

Jusqu’à présent, Azure HDInsight ne prenait en charge qu’un seul administrateur local d’utilisateurs. Cela fonctionnait à merveille pour les petites équipes d’application ou les services. En tant que Hadoop basé sur les charges de travail acquises popularité plus dans le secteur d’entreprise hello, hello besoin pour entreprise les capacités de niveau comme active directory en fonction de l’authentification, de prise en charge multi-utilisateur et de contrôle d’accès basé sur les rôles est devenu plus en plus importantes. À l’aide de clusters HDInsight de domaine, vous pouvez créer un domaine Active Directory de HDInsight cluster joint tooan, configurer une liste d’employés à partir de l’entreprise de hello, qui peuvent s’authentifier via toolog Azure Active Directory sur tooHDInsight cluster. Toute personne extérieure à hello entreprise ne peut pas se connecter ou accéder au cluster HDInsight de hello. Hello administrateur d’entreprise permettre configurer le contrôle d’accès basé sur les rôles de sécurité de la ruche à l’aide [Apache Ranger](http://hortonworks.com/apache/ranger/), donc restreindre l’accès toodata tooonly autant que nécessaire. Enfin, hello admin peut auditer l’accès aux données de hello par les employés et stratégies, d'où un degré élevé de la gouvernance des ressources d’entreprise de contrôle de tooaccess de toutes les modifications apportées.

> [!NOTE]
> Hello nouvelles fonctionnalités décrites dans cette version préliminaire sont disponibles uniquement sur les clusters HDInsight de basés sur Linux pour les charges de travail Hive. Hello autres charges de travail, tels que HBase, Spark, Storm et Kafka, est activée dans les futures mises à jour.

> [!IMPORTANT]
> Oozie n’est pas activé sur HDInsight joint à un domaine.

## <a name="benefits"></a>Avantages
La sécurité d’entreprise est constituée de quatre piliers majeurs : sécurité du périmètre, authentification, autorisation et chiffrement.

![Piliers des avantages des clusters HDInsight joints à un domaine](./media/hdinsight-domain-joined-introduction/hdinsight-domain-joined-four-pillars.png).

### <a name="perimeter-security"></a>Sécurité du périmètre
La sécurité du périmètre dans HDInsight est obtenue grâce aux réseaux virtuels et au service de passerelle. Aujourd'hui, un administrateur d’entreprise permettre créer un cluster HDInsight à l’intérieur d’un réseau virtuel et utiliser les groupes de sécurité réseau (règles de pare-feu entrante ou sortante) toorestrict accès toohello réseau virtuel. Uniquement entrant hello les adresses IP définies dans hello règles de pare-feu sera en mesure de toocommunicate avec le cluster HDInsight de hello, et offrir la sécurité de périmètre. Le service de passerelle permet d’obtenir un autre niveau de sécurité du périmètre. Hello passerelle est service hello qui agit en tant que première ligne de défense pour n’importe quel cluster de HDInsight toohello demande entrante. Il accepte une demande de hello, valide et seulement lui permet ensuite de hello demande toopass toohello autres nœuds de cluster, et offrir la sécurité du périmètre tooother les nœuds de nom et les données dans un cluster de hello.

### <a name="authentication"></a>Authentification
Avec cette version préliminaire publique, un administrateur d’entreprise peut configurer un cluster HDInsight joint à un domaine, dans un [réseau virtuel](https://azure.microsoft.com/services/virtual-network/). nœuds Hello du cluster HDInsight de hello sera domaine toohello jointe géré par l’entreprise de hello. Ceci s’effectue grâce aux [Services de domaine Azure Active Directory](../active-directory-domain-services/active-directory-ds-overview.md). Tous les nœuds hello cluster de hello sont tooa joint à un domaine qui hello entreprise gère. Avec cette configuration, les employés d’entreprise de hello peuvent se connecter sur les nœuds de cluster toohello à l’aide de leurs informations d’identification de domaine. Ils peuvent également utiliser leur tooauthenticate d’informations d’identification de domaine avec les autres points de terminaison approuvés comme toointeract teinte, vues de Ambari, ODBC, JDBC, PowerShell et API REST avec cluster de hello. Hello administrateur possède un contrôle total sur la limitation du nombre de hello d’utilisateurs à interagir avec le cluster hello via ces points de terminaison.

### <a name="authorization"></a>Autorisation
Un suivi de la plupart des entreprises est préférable que pas chaque employé a accès aux ressources de l’entreprise tooall. De même, avec cette version, hello administrateur peut définir des stratégies de contrôle d’accès basé sur les rôles pour les ressources de cluster hello. Par exemple, peut configurer hello admin [Apache Ranger](http://hortonworks.com/apache/ranger/) tooset des stratégies de contrôle d’accès pour la ruche. Cette fonctionnalité garantit que les employés soient en mesure de tooaccess uniquement autant de données dont ils ont besoin toobe réussie dans leur travail. Cluster de toohello accès SSH est également limité toohello uniquement administrateur.

### <a name="auditing"></a>Audit
En même temps que la protection hello HDInsight ressources de cluster à partir des utilisateurs non autorisés et sécurisation des données hello, l’audit de tous les accès aux ressources de cluster toohello et hello données sont nécessaire tootrack accès non autorisé ou non des ressources de hello. Avec cette version préliminaire, hello admin permettre afficher et toutes les ressources de cluster d’accès toohello HDInsight et les données de rapport. Hello admin permettre également afficher et rapport toutes les modifications des stratégies de contrôle d’accès toohello dans Apache Ranger pris en charge les points de terminaison. Un cluster HDInsight de domaine utilise les journaux de hello familiers Apache Ranger UI toosearch d’audit. Sur le serveur principal hello, Ranger utilise [Apache Solr](http://hortonworks.com/apache/solr/) pour le stockage et la recherche des journaux de hello.

### <a name="encryption"></a>Chiffrement
Protection des données est importante pour la sécurité de l’organisation réunion et les exigences de conformité, et ainsi que de limiter l’accès toodata des employés non autorisés, il doit également être sécurisée en la chiffrant. Les deux hello banques de données pour les clusters HDInsight, objet Blob de stockage Azure, et de stockage lac de données Azure prennent en charge transparente côté serveur [chiffrement des données](../storage/common/storage-service-encryption.md) au repos. Les clusters HDInsight sécurisés fonctionnent en toute transparence avec cette fonctionnalité de chiffrement des données côté serveur au repos.

## <a name="next-steps"></a>Étapes suivantes
* Pour configurer un cluster HDInsight joint à un domaine, consultez [Configuration de clusters HDInsight joints à un domaine](hdinsight-domain-joined-configure.md).
* Pour gérer un cluster HDInsight joint à un domaine, consultez [Gestion de clusters HDInsight joints à un domaine](hdinsight-domain-joined-manage.md).
* Pour configurer des stratégies Hive et exécuter des requêtes Hive, consultez [Configuration de stratégies Hive pour les clusters HDInsight joints à un domaine](hdinsight-domain-joined-run-hive.md).
* Pour exécuter des requêtes Hive en utilisant SSH sur des clusters HDInsight joints au domaine, voir [Utiliser SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).
