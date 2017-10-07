---
title: aaaHadoop composants et des versions - Azure HDInsight | Documents Microsoft
description: "Découvrez les composants Hadoop hello et les versions dans les niveaux de service HDInsight et hello disponibles dans cette distribution de cloud de Hortonworks Data Platform."
keywords: "les versions Hadoop, les composants écosystème hadoop, des composants hadoop, la version de hadoop toocheck"
services: hdinsight
editor: cgronlun
manager: asadk
author: bprakash
tags: azure-portal
documentationcenter: 
ms.assetid: 367b3f4a-f7d3-4e59-abd0-5dc59576f1ff
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/14/2017
ms.author: bprakash
ms.openlocfilehash: b661d901b0113458c3501ec06454fc8841189672
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-hello-hadoop-components-and-versions-available-with-hdinsight"></a>Quels sont les composants de Hadoop hello et les versions disponibles avec HDInsight ?

En savoir plus sur les composants d’écosystème hello Apache Hadoop et des versions de Microsoft Azure HDInsight, ainsi que les niveaux de service Standard et Premium de hello. En outre, découvrez comment toocheck les versions des composants Hadoop dans HDInsight. 

Chaque version de HDInsight est une distribution cloud d’une version de la solution Hortonworks Data Platform (HDP).

## <a name="hadoop-components-available-with-different-hdinsight-versions"></a>Composants Hadoop disponibles avec différentes versions de HDInsight
Azure HDInsight prend en charge plusieurs versions de cluster Hadoop qui peuvent être déployées à tout moment. Chaque choix version crée une version spécifique de la distribution de HDP hello et un ensemble de composants qui sont contenues dans cette distribution. À compter du 17 février 2017, version du cluster par défaut hello utilisée par Azure HDInsight est 3.5 et est basée sur HDP 2.5.

les versions des composants Hello associées aux versions de cluster HDInsight sont répertoriées dans hello tableau suivant. 

> [!NOTE]
> version par défaut de Hello pour hello service HDInsight peut changer sans préavis. Si vous avez une dépendance de version, spécifiez la version de HDInsight hello lorsque vous créez vos clusters avec hello SDK .NET avec Azure PowerShell et CLI d’Azure.

| Composant | HDInsight 3.6 (par défaut) | HDInsight 3.5 | HDInsight 3.4 | HDInsight 3.3 | HDInsight 3.2 | HDInsight 3.1 | HDInsight 3.0 |
| --- | --- | --- | --- | --- | --- | --- |--- |
| Hortonworks Data Platform |2.6 |2.5 |2.4 |2.3 |2.2 |2.1.7 |2.0 |
| Apache Hadoop et YARN |2.7.3 |2.7.3 |2.7.1 |2.7.1 |2.6.0 |2.4.0 |2.2.0 |
| Apache Tez |0.7.0 |0.7.0 |0.7.0 |0.7.0 |0.5.2 |0.4.0 |-|
| Apache Pig |0.16.0 |0.16.0 |0.15.0 |0.15.0 |0.14.0 |0.12.1 |0.12.0 |
| Apache Hive et HCatalog |1.2.1 |1.2.1 |1.2.1 |1.2.1 |0.14.0 |0.13.1 |0.12.0 |
| Apache Hive2 | 2.1.0 |-|-|-|-|-|-|
| Apache Tez/Hive2 | 0.8.4 |-|-|-|-|-|-|
| Apache Ranger | 0.7.0 |0.6.0 |-|-|-|-|-|
| Apache HBase |1.1.2 |1.1.2 |1.1.2 |1.1.1 |0.98.4 |0.98.0 |-|
| Apache Sqoop |1.4.6 |1.4.6 |1.4.6 |1.4.6 |1.4.5 |1.4.4 |1.4.4 |
| Apache Oozie |4.2.0 |4.2.0 |4.2.0 |4.2.0 |4.1.0 |4.0.0 |4.0.0 |
| Apache Zookeeper |3.4.6 |3.4.6 |3.4.6 |3.4.6 |3.4.6 |3.4.5 |3.4.5 |
| Apache Storm |1.1.0 |1.0.1 |0.10.0 |0.10.0 |0.9.3 |0.9.1 |-|
| Apache Mahout |0.9.0+ |0.9.0+ |0.9.0+ |0.9.0+ |0.9.0 |0.9.0 |-|
| Apache Phoenix |4.7.0 |4.7.0 |4.4.0 |4.4.0 |4.2.0 |4.0.0.2.1.7.0-2162 |-|
| Apache Spark |2.1.0 (Linux uniquement) |1.6.2 + 2.0 (Linux uniquement) |1.6.0 (Linux uniquement) |1.5.2 (Linux uniquement, version expérimentale) |1.3.1 (Windows uniquement) |-|-|
| Apache Kafka | 0.10.0 | 0.10.0 | 0.9.0 |-|-|-|-|
| Apache Ambari | 2.5.0 | 2.4.0 | 2.2.1 | 2.1.0 |-|-|-|
| Apache Zeppelin | 0.7.0 |-|-|-|-|-|-|
| Mono |4.2.1 |4.2.1 |3.2.8 |-|-|-|

## <a name="check-for-current-hadoop-component-version-information"></a>Comment vérifier les informations de version du composant Hadoop actuel

versions des composants Hello Hadoop écosystème associées aux versions de cluster HDInsight peuvent changer à tooHDInsight de mises à jour. composants de Hadoop toocheck hello et tooverify les versions sont utilisées pour un cluster, utilisez hello Ambari REST API. Hello **GetComponentInformation** commande récupère les informations sur les composants de service. Pour plus d’informations, consultez hello [Ambari documentation][ambari-docs].

Pour les clusters Windows, une autre façon toocheck hello la version du composant est toolog tooa cluster à l’aide du Bureau à distance et examiner le contenu hello du répertoire de C:\apps\dist\ hello.

> [!IMPORTANT]
> Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou version ultérieure. Pour en savoir plus, voir [Mise hors service de HDInsight sur Windows](#hdinsight-windows-retirement).

### <a name="release-notes"></a>Notes de publication

Consultez [notes de version de HDInsight](hdinsight-release-notes.md) pour notes supplémentaires sur les versions les plus récentes de HDInsight hello.

## <a name="supported-hdinsight-versions"></a>Versions de HDInsight prises en charge
Hello tableau suivant répertorie les versions hello de HDInsight qui sont actuellement disponibles sur hello portail Azure. les versions HDP Hello qui correspondent tooeach HDInsight version sont répertoriées, ainsi que les dates de publication de produit hello. dates d’expiration et de retrait du support Hello sont également fournies, lorsqu’ils sont connus.

> [!NOTE]
> Après la prise en charge pour une version a expiré, il peut être disponible via le portail classique de Microsoft Azure hello. Toutefois, les versions de cluster continuent toobe disponible à l’aide de hello `Version` paramètre Bonjour Windows PowerShell [New-AzureRmHDInsightCluster](https://msdn.microsoft.com/library/mt619331.aspx) des commandes et hello .NET SDK jusqu'à ce que la version de hello date de suppression.
> 
> Les clusters à haute disponibilité avec deux nœuds principaux sont déployés par défaut pour les clusters HDInsight 2.1 et versions ultérieures. Ils ne sont pas disponibles pour les clusters HDInsight version 1.6.

| Version de HDInsight | Version de la plateforme HDP | SYSTÈME D’EXPLOITATION DE LA MACHINE VIRTUELLE | Haute disponibilité | Date de lancement | Disponibilité sur hello portail Azure | Date d’expiration du support | Date de mise hors service |
| --- | --- | --- | --- | --- | --- | --- | --- |
| HDInsight 3.6 |HDP 2.6 |Ubuntu 16 |Oui |4 avril 2017 |Oui | | |
| HDInsight 3.5 |HDP 2.5 |Ubuntu 16 |Oui |30 septembre 2016 |Oui |5 septembre 2017 |31 mai 2018 |
| HDInsight 3.4 |HDP 2.4 |Ubuntu 14.0.4 LTS |Oui |29 mars 2016 |Oui |29 décembre 2016 |9 janvier 2018 |
| HDInsight 3.3 |HDP 2.3 |Windows Server 2012 R2 |Oui |2 décembre 2015 |Oui |27 juin 2016 |31 juillet 2018 |
| HDInsight 3.3 |HDP 2.3 |Ubuntu 14.0.4 LTS |Oui |2 décembre 2015 |Oui |27 juin 2016 |31 juillet 2017 |
| HDInsight 3.2 |HDP 2.2 |Ubuntu 12.04 LTS ou Windows Server 2012 R2 |Oui |18 février 2015 |Non |1 mars 2016 |1 avril 2017 |
| HDInsight 3.1 |HDP 2,1 |Windows Server 2012 R2 |Oui |24 juin 2014 |Non |18 mai 2015 |30 juin 2016 |
| HDInsight 3.0 |HDP 2,0 |Windows Server 2012 R2 |Oui |11 février 2014 |Non |17 septembre 2014 |30 juin 2015 |
| HDInsight 2.1 |HDP 1,3 |Windows Server 2012 R2 |Oui |28 octobre 2013 |Non |12 mai 2014 |31 mai 2015 |
| HDInsight 1.6 |HDP 1.1 | |Non |28 octobre 2013 |Non |26 avril 2014 |31 mai 2015 |

## <a name="hdinsight-windows-retirement"></a>Mise hors service de HDInsight sur Windows
Microsoft Azure HDInsight version 3.3 était la dernière version de HDInsight sur Windows hello. Hello date de suppression pour HDInsight sur Windows est le 31 juillet 2018. Si vous disposez de tous les clusters HDInsight sur Windows 3.3 ou version antérieure, vous devez migrer tooHDInsight sur Linux (HDInsight version 3.5 ou version ultérieure) avant le 31 juillet 2018. Migration toohello système d’exploitation Linux vous permet de tooretain hello capacité toocreate ou redimensionner vos clusters HDInsight. La prise en charge de HDInsight version 3.3 sur Windows a expiré le 27 juin 2016.

À partir de HDInsight version 3.4, Microsoft a publié HDInsight uniquement sur hello du système d’exploitation Linux. Par conséquent, certains composants hello dans HDInsight sont disponibles pour Linux uniquement. Ceux-ci incluent Apache Ranger Kafka, Hive interactif, Spark, HDInsight, applications et Azure Data Lake Store en tant que système de fichiers principal hello. Les versions futures de HDInsight sont disponibles uniquement sur hello du système d’exploitation Linux. Aucune version de HDInsight ne sera proposée sur Windows. 

## <a name="faqs"></a>FAQ

### <a name="what-is-hello-timeline-for-retiring-hdinsight-on-windows"></a>Quelle est la chronologie hello pour mettre hors service HDInsight sur Windows ?
31 juillet 2018, est hello date de suppression pour HDInsight sur Windows. Si hello planifié date de suppression est différent de votre région, vous serez averti séparément. 

### <a name="what-is-hello-impact-of-retiring-hdinsight-on-windows-for-existing-customers"></a>Nouveautés d’impact hello de mise hors service HDInsight sur Windows pour les clients existants ?
Une fois HDInsight mis hors service sur Windows, vous ne pourrez plus créer de clusters HDInsight sur Windows, ni redimensionner un cluster HDInsight existant sur ce système. La prise en charge de HDInsight version 3.3 a expiré le 27 juin 2016. Par conséquent, la résolution des bogues et le support ne sont plus assurés pour HDInsight 3.3 et versions antérieures. Les versions futures de HDInsight sont disponibles uniquement sur hello du système d’exploitation Linux. Aucune version de HDInsight ne sera proposée sur Windows.
 
### <a name="which-versions-of-hdinsight-on-windows-are-affected"></a>Quelles sont les versions de HDInsight sur Windows qui seront affectées ?
Azure HDInsight version 3.3 est la dernière version de HDInsight pour Windows hello. Avant de HDInsight sur Windows est retiré, toutes les fenêtres de HDInsight clusters version 3.3 ou une version antérieure doit être migré tooHDInsight sur Linux version 3.5 ou version ultérieure. Migration de votre tooHDInsight de clusters sur Linux vous permet de nouveaux clusters tooretain hello capacité toocreate ou redimensionner des clusters existants. 

### <a name="what-do-i-need-toodo"></a>Comment dois-je toodo ?
Migrer votre cluster HDInsight Linux de HDInsight Windows clusters tooa pris en charge avant le 31 juillet 2018. Pour en savoir plus hello [document de migration HDInsight](https://docs.microsoft.com/en-gb/azure/hdinsight/hdinsight-migrate-from-windows-to-linux). Pour plus d’informations sur les versions d’Azure HDInsight, consultez la liste des hello [versions prises en charge](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-component-versioning#supported-hdinsight-versions). 

### <a name="where-do-i-find-hello-cluster-os-type"></a>Où trouver le type de système d’exploitation de cluster hello ?
Bonjour portail Azure, accédez à toohello page Vue d’ensemble de HDInsight Cluster et recherchez **Cluster type** sous **Essentials**. types de système d’exploitation de cluster Hello sont répertoriés dans cette page. 

### <a name="i-cant-migrate-tooan-hdinsight-linux-cluster-by-july-31-2018-what-is-hello-impact-toomy-hdinsight-windows-cluster"></a>Je ne parviens pas à migrer tooan cluster HDInsight Linux en au 31 juillet 2018. Qu’est hello impact toomy cluster HDInsight Windows ?
Hello cluster HDInsight Windows s’exécute en tant que-est, mais vous ne pouvez pas créer un cluster HDInsight Windows ou redimensionner un cluster HDInsight Windows existant. 

### <a name="my-cluster-has-a-net-dependency-how-do-i-resolve-this-dependency-on-linux"></a>Mon cluster présente une dépendance à .NET. Comment puis-je la résoudre sur Linux ?
Vous pouvez résoudre votre dépendance de cluster Linux à l’aide de hello [projet Mono](http://www.mono-project.com/). Cette implémentation open source de .NET est disponible pour les clusters HDInsight sur Linux. Pour en savoir plus hello [document de migration HDInsight](https://docs.microsoft.com/en-gb/azure/hdinsight/hdinsight-migrate-from-windows-to-linux). 

### <a name="im-a-new-customer-for-hdinsight-on-windows-how-can-i-create-an-hdinsight-windows-cluster"></a>Je n’utilise HDInsight sur Windows que depuis peu. Comment puis-je créer un cluster HDInsight sur Windows ?
Depuis le 3 juillet 2017, seuls les clients HDInsight sur Windows existants peuvent créer des clusters HDInsight sur Windows. Nouveaux clients ne peut pas créer un cluster HDInsight Windows Bonjour portail Azure à l’aide de PowerShell ou hello SDK. Nous recommandons aux nouveaux clients de créer un cluster HDInsight sur Linux. Les clients existants peuvent créer de nouvelles fenêtres HDInsight clusters jusqu'à hello HDInsight sur Windows date de suppression. 

### <a name="is-there-a-pricing-impact-associated-with-moving-from-hdinsight-on-windows-toohdinsight-on-linux"></a>Existe-t-il un impact sur la tarification associée au déplacement de HDInsight sur tooHDInsight Windows sur Linux ?
Non, hello tarification est hello même pour HDInsight sur un système d’exploitation. 

### <a name="what-are-hello-customer-advantages-associated-with-hello-move-tooonly-using-hdinsight-on-linux"></a>Quels sont les avantages de client hello associés hello déplacer tooonly à l’aide de HDInsight sur Linux ?
* Temps de commercialisation plus rapide des technologies de données volumineuses open source via hello service HDInsight
* Communauté et écosystème de support importants
* Capacité tooexercise activement par hello ouvrir Communauté source pour Hadoop et d’autres technologies de données volumineuses

### <a name="does-hdinsight-on-linux-provide-additional-functionality-beyond-what-is-available-in-hdinsight-on-windows"></a>La version de HDInsight sur Linux propose-t-elle des fonctionnalités supplémentaires par rapport à la version de ce logiciel sous Windows ?
À partir de HDInsight version 3.4, Microsoft a publié HDInsight uniquement sur hello du système d’exploitation Linux. Par conséquent, certains composants hello dans HDInsight sont disponibles pour Linux uniquement. Ceux-ci incluent Apache Ranger Kafka, Hive interactif, Spark, HDInsight, applications et Azure Data Lake Store en tant que système de fichiers principal hello. 

## <a name="service-level-agreement-for-hdinsight-cluster-versions"></a>Contrat de niveau de service pour les versions de cluster HDInsight
contrat de niveau de service (SLA) Hello est définie en termes d’un _prise en charge de fenêtre_. fenêtre de prise en charge Hello est hello durée pendant laquelle une version du cluster HDInsight est pris en charge par le support technique et Service clientèle Microsoft. Si la version de hello a un _prennent en charge de la date d’expiration_ qui a passé, le cluster HDInsight de hello est en dehors de la fenêtre de prise en charge hello. Pour plus d’informations sur les versions prises en charge, consultez la liste des hello [prise en charge des versions du cluster HDInsight](https://docs.microsoft.com/en-gb/azure/hdinsight/hdinsight-migrate-from-windows-to-linux). date d’expiration de prise en charge Hello pour une version X (une fois une version plus récente de X + 1 est disponible) de HDInsight spécifié est calculée comme hello plus tard de :  

* La formule 1 : Ajouter la date de toohello de 180 jours lorsque la version du cluster HDInsight hello X a été publiée.
* Formule 2 : Ajouter la date de toohello de 90 jours lorsque version du cluster HDInsight hello X + 1 est mis à disposition dans le portail Azure.

Hello _date de retrait_ est date hello après lequel la version du cluster hello ne peut pas être créée sur HDInsight. Depuis le 31 juillet 2017, vous ne pouvez pas redimensionner un cluster HDInsight après sa date de mise hors service. 

> [!NOTE]
> Les clusters HDInsight Windows (y compris les versions 2.1, 3.0, 3.1, 3.2 et 3.3) s’exécuter sur la famille de systèmes d’exploitation invité Azure version 4, qui utilise la version 64 bits de hello de Windows Server 2012 R2. Famille de systèmes d’exploitation invité Azure version 4 prend en charge les versions du .NET Framework hello 4.0, 4.5, 4.5.1 et 4.5.2.

## <a name="hortonworks-release-notes-associated-with-hdinsight-versions"></a>Notes de publication de Hortonworks associées aux versions de HDInsight

section de Hello fournit des liens toorelease notes pour les distributions Hortonworks Data Platform hello et composants Apache qui sont utilisés avec HDInsight.
* Le cluster HDInsight version 3.6 utilise une distribution Hadoop basée sur [Hortonworks Data Platform 2.6](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.6.0/bk_release-notes/content/ch_relnotes.html).
* Le cluster HDInsight version 3.5 utilise une distribution Hadoop basée sur [Hortonworks Data Platform 2.5](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.5.0/bk_release-notes/content/ch_relnotes_v250.html). La version 3.5 du cluster HDInsight est hello _par défaut_ cluster Hadoop qui est créé dans hello portail Azure.
* Le cluster HDInsight version 3.4 utilise une distribution Hadoop basée sur [Hortonworks Data Platform 2.4](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.4.0/bk_HDP_RelNotes/content/ch_relnotes_v240.html).
* Le cluster HDInsight version 3.3 utilise une distribution Hadoop basée sur [Hortonworks Data Platform 2.3](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.3.0/bk_HDP_RelNotes/content/ch_relnotes_v230.html).

  * [Notes de publication Apache Storm](https://storm.apache.org/2015/11/05/storm0100-released.html) sont disponibles sur le site Web de Apache hello.
  * [Notes de publication Apache Hive](https://issues.apache.org/jira/secure/ReleaseNote.jspa?version=12332384&styleName=Text&projectId=12310843) sont disponibles sur le site Web de Apache hello.
* Le cluster HDInsight version 3.2 utilise une distribution Hadoop basée sur [Hortonworks Data Platform 2.2][hdp-2-2].

  * Des notes de publication sont proposées pour des composants Apache spécifiques : [Hive 0.14](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310843&version=12326450), [Pig 0.14](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310730&version=12326954), [HBase 0.98.4](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310753&version=12326810), [Phoenix 4.2.0](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12315120&version=12327581), [M/R 2.6](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310941&version=12327180), [HDFS 2.6](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310942&version=12327181), [YARN 2.6](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12313722&version=12327197), [Common](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12310240&version=12327179), [Tez 0.5.2](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12314426&version=12328742), [Ambari 2.0](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12312020&version=12327486), [Storm 0.9.3](https://issues.apache.org/jira/secure/ReleaseNote.jspa?projectId=12314820&version=12327112) et [Oozie 4.1.0](https://issues.apache.org/jira/secure/ReleaseNote.jspa?version=12324960&projectId=12311620).
* Le cluster HDInsight version 3.1 utilise une distribution Hadoop basée sur [Hortonworks Data Platform 2.1.7][hdp-2-1-7]. Les clusters HDInsight 3.1 créés avant le 7 novembre 2014 sont basés sur [Hortonworks Data Platform 2.1.1][hdp-2-1-1].
* Le cluster HDInsight version 3.0 utilise une distribution Hadoop basée sur [Hortonworks Data Platform 2.0][hdp-2-0-8].
* Le cluster HDInsight version 2.1 utilise une distribution Hadoop basée sur [Hortonworks Data Platform 1.3][hdp-1-3-0].
* Le cluster HDInsight version 1.6 utilise une distribution Hadoop basée sur [Hortonworks Data Platform 1.1][hdp-1-1-0].

## <a name="hdinsight-standard-and-hdinsight-premium"></a>HDInsight Standard et HDInsight Premium

HDInsight Azure fournit les offres de cloud de données volumineuses hello dans deux catégories : _Standard_ et _Premium_. Hello tableau suivant répertorie les fonctionnalités qui sont disponibles _uniquement_ dans HDInsight Premium. Fonctionnalités qui ne sont pas explicitement décrits dans la table de hello sont disponibles dans HDInsight Standard et Premium.

> [!NOTE]
> Hello HDInsight Premium offre est actuellement en version préliminaire et est disponible uniquement pour les clusters Linux.

| Fonctionnalité HDInsight Premium | Description |
| --- | --- |
| Clusters HDInsight joints à un domaine |Joindre des clusters HDInsight tooAzure des domaines Active Directory (Azure AD) pour la sécurité au niveau de l’entreprise. Dans HDInsight Premium, vous pouvez configurer une liste d’employés à partir de votre entreprise qui peut s’authentifier via toolog Azure AD sur le cluster HDInsight de tooan. administrateur d’entreprise Hello pouvez configurer le contrôle d’accès basé sur un rôle pour la sécurité de la ruche à l’aide de [Apache Ranger](http://hortonworks.com/apache/ranger/) et restreindre toouse d’accès aux données que nécessaire. Enfin, hello administrateur pouvez auditer les données accédées par les employés et les modifications tooaccess contrôler les stratégies, et atteindre un niveau élevé de la gouvernance des ressources d’entreprise. Pour plus d’informations, consultez la section [Configurer des clusters HDInsight joints à un domaine](hdinsight-domain-joined-configure.md). |

### <a name="cluster-types-supported-in-hdinsight-premium"></a>Types de clusters pris en charge par HDInsight Premium
Hello tableau suivant répertorie les types de cluster hello qui sont pris en charge dans HDInsight Premium.

| Type de cluster | Standard | Premium (version préliminaire) |
| --- | --- | --- |
| Hadoop |Oui |Oui (HDInsight 3.6 uniquement) |
| Spark |Oui |Non |
| HBase |OUI |Non |
| Storm |OUI |Non |
| R Server |Oui |Non |
| Hive interactif (version préliminaire) |Oui |Non |
| Kafka (préversion) |Oui |Non | 

### <a name="support-for-azure-data-lake-store-in-hdinsight-premium"></a>Prise en charge d’Azure Data Lake Store dans HDInsight Premium

Les clusters HDInsight Premium ne permettent pas à l’utilisation d’Azure Data Lake Store en tant que stockage principal. Vous pouvez néanmoins utiliser cette fonction en tant que stockage complémentaire avec des clusters HDInsight Premium.

### <a name="pricing-and-sla"></a>Tarifs et contrat SLA
Pour plus d’informations sur la tarification et le contrat SLA pour l’édition Premium de HDInsight, consultez [Tarification HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).

## <a name="default-node-configuration-and-virtual-machine-sizes-for-clusters"></a>Tailles des machines virtuelles et configuration des nœuds par défaut pour les clusters
Hello suivant des tailles de machine virtuelle (VM) tables liste hello par défaut pour les clusters HDInsight.

> [!IMPORTANT]
> Si vous avez besoin de plus de 32 nœuds worker dans un cluster, vous devez sélectionner une taille de nœud principal avec au moins 8 cœurs et 14 Go de RAM.
> 
> 

* Toutes les régions prises en charge à l’exception du sud du Brésil et de l’ouest du Japon :

  | Type de cluster | Hadoop | HBase | Storm | Spark | R Server |
  | --- | --- | --- | --- | --- | --- |
  | Head : taille de machine virtuelle par défaut |D3 v2 |D3 v2 |A3 |D12 v2 |D12 v2 |
  | Head : tailles de machine virtuelle recommandées |D3 v2, D4 v2, D12 v2 |D3 v2, D4 v2, D12 v2 |A3, A4, A5 |D12 v2, D13 v2, D14 v2 |D12 v2, D13 v2, D14 v2 |
  | Worker : taille de machine virtuelle par défaut |D3 v2 |D3 v2 |D3 v2 |Windows : D12 v2 ; Linux : D4 v2 |Windows : D12 v2 ; Linux : D4 v2 |
  | Worker : tailles de machine virtuelle recommandées |D3 v2, D4 v2, D12 v2 |D3 v2, D4 v2, D12 v2 |D3 v2, D4 v2, D12 v2 |Windows : D12 v2, D13 v2, D14 v2; Linux : D4 v2, D12 v2, D13 v2, D14 v2 |Windows : D12 v2, D13 v2, D14 v2; Linux : D4 v2, D12 v2, D13 v2, D14 v2 |
  | Zookeeper : taille de machine virtuelle par défaut | |A3 |A2 | | |
  | Zookeeper : tailles de machine virtuelle recommandées | |A3, A4, A5 |A2, A3, A4 | | |
  | Edge : taille de machine virtuelle par défaut | | | | |Windows : D12 v2 ; Linux : D4 v2 |
  | Edge : taille de machine virtuelle recommandée | | | | |Windows : D12 v2, D13 v2, D14 v2; Linux : D4 v2, D12 v2, D13 v2, D14 v2 |
* Sud du Brésil et ouest du Japon uniquement (aucune taille pour V2) :

  | Type de cluster | Hadoop | HBase | Storm | Spark | R Server |
  | --- | --- | --- | --- | --- | --- |
  | Head : taille de machine virtuelle par défaut |D3 |D3 |A3 |D12 |D12 |
  | Head : tailles de machine virtuelle recommandées |D3, D4, D12 |D3, D4, D12 |A3, A4, A5 |D12, D13, D14 |D12, D13, D14 |
  | Worker : taille de machine virtuelle par défaut |D3 |D3 |D3 |Windows : D12 v2 ; Linux : D4 |Windows : D12 ; Linux : D4 |
  | Worker : tailles de machine virtuelle recommandées |D3, D4, D12 |D3, D4, D12 |D3, D4, D12 |Windows : D12, D13, D14 ; Linux : D4, D12, D13, D14 |Windows : D12, D13, D14 ; Linux : D4, D12, D13, D14 |
  | Zookeeper : taille de machine virtuelle par défaut | |A2 |A2 | | |
  | Zookeeper : tailles de machine virtuelle recommandées | |A2, A3, A4 |A2, A3, A4 | | |
  | Edge : tailles de machine virtuelle par défaut | | | | |Windows : D12 ; Linux : D4 |
  | Edge : tailles de machine virtuelle recommandées | | | | |Windows : D12, D13, D14 ; Linux : D4, D12, D13, D14 |

> [!NOTE]
> - Head est appelé *Nimbus* pour hello Storm cluster type.
> - Processus de travail est appelé *superviseur* pour hello Storm cluster type.
> - Processus de travail est appelé *région* pour hello HBase le type de cluster.

## <a name="next-steps"></a>Étapes suivantes
- [Création de clusters Hadoop dans HDInsight](hdinsight-hadoop-provision-linux-clusters.md)
- [Travailler à partir d’un PC Windows dans Hadoop sur HDInsight](hdinsight-hadoop-windows-tools.md)

[Supported HDInsight versions]:(#supported-hdinsight-versions)

[image-hdi-versioning-versionscreen]: ./media/hdinsight-component-versioning/hdi-versioning-version-screen.png

[wa-forums]: http://azure.microsoft.com/support/forums/

[connect-excel-with-hive-ODBC]: hdinsight-connect-excel-hive-ODBC-driver.md

[hdp-2-2]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.2.0/HDP_2.2.0_Release_Notes_20141202_version/index.html

[hdp-2-1-7]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.7-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.7.html

[hdp-2-1-1]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.1/bk_releasenotes_hdp_2.1/content/ch_relnotes-hdp-2.1.1.html

[hdp-2-0-8]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.8.0/bk_releasenotes_hdp_2.0/content/ch_relnotes-hdp2.0.8.0.html

[hdp-1-3-0]: http://docs.hortonworks.com/HDPDocuments/HDP1/HDP-1.3.0/bk_releasenotes_hdp_1.x/content/ch_relnotes-hdp1.3.0_1.html

[hdp-1-1-0]: http://docs.hortonworks.com/HDPDocuments/HDP1/HDP-Win-1.1/bk_releasenotes_HDP-Win/content/ch_relnotes-hdp-win-1.1.0_1.html

[ambari-docs]: https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md

[zookeeper]: http://zookeeper.apache.org/
