---
title: "données aaaImport dans Machine Learning Studio à partir de sources de données en ligne | Documents Microsoft"
description: "Comment tooimport vos données d’apprentissage Azure Machine Learning Studio à partir de différentes sources en ligne."
keywords: "importer des données, format de données, types de données, sources de données, données d'apprentissage"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 701b93fe-765b-4d15-a1cf-9b607f17add6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;garye
ms.openlocfilehash: aae6907cdd0b4dc373ae08c2569caa276c198b49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="import-data-into-azure-machine-learning-studio-from-various-online-data-sources-with-hello-import-data-module"></a>Importer des données dans Azure Machine Learning Studio à partir de différentes sources de données en ligne avec le module d’importation de données hello
Cet article décrit la prise en charge de hello pour l’importation de données en ligne à partir de différentes sources et les informations de hello nécessaire toomove des données à partir de ces sources dans une expérience Azure Machine Learning.

> [!NOTE]
> Cet article fournit des informations générales sur hello [importer des données] [ import-data] module. Pour plus d’informations sur les types de données, vous pouvez accéder à hello, formats, des paramètres et des réponses aux questions de toocommon, consultez rubrique de référence de module hello pour hello [importer des données] [ import-data] module.
> 
> 

<!-- -->

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

## <a name="introduction"></a>Introduction
À l’aide de hello [importer des données] [ import-data] module, vous pouvez accéder aux données à partir de plusieurs sources de données en ligne pendant l’exécution de votre expérience [Azure Machine Learning Studio](https://studio.azureml.net/Home):

* Une URL web avec HTTP
* Hadoop avec HiveQL
* Stockage des objets blob
* Table Azure
* Base de données Azure SQL ou SQL Server sur les machines virtuelles Azure
* Base de données SQL Server locale
* Un fournisseur de flux de données, actuellement, OData
* Azure Cosmos DB (anciennement DocumentDB)

tooaccess des sources de données en ligne dans votre expérience Studio, ajouter hello [importer des données] [ import-data] tooyour de module, sélectionnez hello **source de données**, puis fournissez les paramètres hello nécessaires données de salutation tooaccess. les sources de données en ligne Hello qui sont prises en charge sont répertoriés dans le tableau hello ci-dessous. Ce tableau récapitule également les formats de fichier hello qui sont prises en charge et les paramètres qui sont utilisés tooaccess hello des données.

Notez que ces données étant accessibles pendant l’exécution de votre expérience, elles ne sont disponibles que pour cette expérience. En comparaison, les données ayant été stockées dans un module de dataset sont expérience tooany disponibles dans votre espace de travail.

> [!IMPORTANT]
> Actuellement, hello [importer des données] [ import-data] et [exporter les données] [ export-data] modules peuvent lire et écrire des données uniquement à partir de stockage Azure créé à l’aide de hello Modèle de déploiement classique. En d’autres termes, hello nouveau type de compte de stockage d’objets Blob Azure qui offre un niveau d’accès de stockage à chaud ou niveau d’accès de stockage froid n’est pas encore pris en charge. 
> 
> En règle générale, les comptes de stockage Azure que vous avez peut-être créés avant que cette option de service ne soit disponible ne devraient pas être affectés. 
> Si vous avez besoin de toocreate un nouveau compte, sélectionnez **classique** pour hello déploiement de modèle, ou utilisez le Gestionnaire de ressources et sélectionnez **usage général** plutôt que **stockage d’objets Blob** pour **Compte kind**. 
> 
> Pour plus d’informations, consultez [Stockage des objets blob Azure : niveaux de stockage chauds et froids](../storage/blobs/storage-blob-storage-tiers.md).
> 
> 

## <a name="supported-online-data-sources"></a>Sources de données en ligne prises en charge
Azure Machine Learning **importer des données** module prend en charge hello les sources de données suivantes :

| source de données | Description | Paramètres |
| --- | --- | --- |
| URL Web via HTTP |Lit les données au format CSV (valeurs séparées par des virgules), TSV (valeurs séparées par des tabulations), ARFF (format de fichier de relation d’attribut) et SVM-light (Machines vectorielles (SVM clair)), à partir de n’importe quelle URL web qui utilise le protocole HTTP |<b>URL</b>: Spécifie le nom complet du fichier hello, y compris les URL du site hello et nom de fichier hello, avec n’importe quelle extension de hello. <br/><br/><b>Format de données</b>: Spécifie les formats d’une des données de salutation pris en charge : CSV, TSV, ARFF ou SVM-light. Si les données de salutation possède une ligne d’en-tête, il est utilisé tooassign les noms de colonnes. |
| Hadoop/HDFS |Lit les données à partir d’un stockage distribué dans Hadoop. Vous spécifiez les données hello souhaité à l’aide de HiveQL, un langage de requête de type SQL. HiveQL peut également être utilisé tooaggregate données et effectuer un filtrage avant d’ajouter des données de hello tooMachine Learning Studio. |<b>Requête de base de données Hive</b>: Spécifie la requête Hive de hello utilisé toogenerate les données de salutation.<br/><br/><b>URI du serveur HCatalog </b> : nom de hello spécifié de votre cluster à l’aide du format de hello  *&lt;votre nom de cluster&gt;. azurehdinsight.net.*<br/><br/><b>Nom du compte utilisateur Hadoop</b>: Spécifie le compte d’utilisateur Hadoop hello nom utilisé le cluster de hello tooprovision.<br/><br/><b>Mot de passe utilisateur Hadoop</b> : Spécifie hello des informations d’identification utilisées lors de la configuration de cluster de hello. Pour plus d’informations, consultez [Création de clusters Hadoop dans HDInsight](../hdinsight/hdinsight-provision-clusters.md).<br/><br/><b>Emplacement des données de sortie</b>: Spécifie si les données de salutation sont stockées dans un système de fichiers distribués Hadoop (HDFS) ou dans Azure. <br/><ul>Si vous stockez des données de sortie dans HDFS, spécifiez l’URI du serveur HDFS hello. (Être vraiment toouse hello nom du cluster HDInsight sans le préfixe HTTPS:// de hello). <br/><br/>Si vous stockez vos données de sortie dans Azure, vous devez spécifier le nom de compte de stockage Windows Azure hello, clé d’accès et du nom de conteneur de stockage.</ul> |
| Base de données SQL |Lit les données stockées dans une base de données SQL Azure ou dans une base de données SQL Server s’exécutant sur une machine virtuelle Azure. |<b>Nom du serveur de base de données</b>: Spécifie le nom hello du serveur hello sur quel hello base de données est en cours d’exécution.<br/><ul>En cas de la base de données SQL Azure Entrez le nom du serveur hello qui est généré. En général, il présente sous forme de hello  *&lt;generated_identifier&gt;. database.windows.net.* <br/><br/>Dans le cas d’un serveur SQL hébergé sur une machine virtuelle Azure, entrez *tcp:&lt;Virtual Machine DNS Name&gt;, 1433*</ul><br/><b>Nom de la base de données </b>: Spécifie le nom hello de base de données hello sur le serveur de hello. <br/><br/><b>Nom du compte utilisateur Server</b>: Spécifie un nom d’utilisateur pour un compte qui dispose des autorisations d’accès pour la base de données hello. <br/><br/><b>Mot de passe utilisateur Server</b>: Spécifie le mot de passe hello hello compte d’utilisateur.<br/><br/><b>Accepter n’importe quel certificat du serveur</b>: utilisez cette option (moins sûr) si vous souhaitez tooskip examiner le certificat de site hello avant de lire vos données.<br/><br/><b>Requête de base de données</b>: entrez une instruction SQL qui décrit les données hello tooread. |
| Base de données SQL locale |Lit les données stockées dans une base de données SQL locale. |<b>Passerelle de données</b>: Spécifie le nom hello Hello passerelle de gestion des données installées sur un ordinateur sur lequel il peut accéder à votre base de données SQL Server. Pour plus d’informations sur la configuration de passerelle de hello, consultez [effectuer avancé analytique à l’aide des données à partir d’un serveur de SQL server sur site Azure Machine Learning](machine-learning-use-data-from-an-on-premises-sql-server.md).<br/><br/><b>Nom du serveur de base de données</b>: Spécifie le nom hello du serveur hello sur quel hello base de données est en cours d’exécution.<br/><br/><b>Nom de la base de données </b>: Spécifie le nom hello de base de données hello sur le serveur de hello. <br/><br/><b>Nom du compte utilisateur Server</b>: Spécifie un nom d’utilisateur pour un compte qui dispose des autorisations d’accès pour la base de données hello. <br/><br/><b>Nom d’utilisateur et mot de passe</b>: cliquez sur <b>entrer des valeurs</b> tooenter vos informations d’identification de base de données. Vous pouvez utiliser l’authentification intégrée Windows ou l’authentification SQL Server en fonction de la configuration de votre serveur local SQL Server.<br/><br/><b>Requête de base de données</b>: entrez une instruction SQL qui décrit les données hello tooread. |
| table Azure |Lit les données à partir de hello service de Table dans le stockage Azure.<br/><br/>Si vous lisez rarement des grandes quantités de données, utilisez hello Service de Table Azure. Il fournit une solution de stockage ultra disponible, flexible, non relationnelle (NoSQL), économique et hautement évolutive. |Hello options Bonjour **importer des données** varient selon que vous accédez à des informations publiques ou à un compte de stockage privé qui nécessite des informations d’identification de connexion. Cela est déterminé par hello <b>Type d’authentification</b> qui peut avoir la valeur « PublicOrSAS » ou « Compte », chacune d’elles possède son propre ensemble de paramètres. <br/><br/><b>Public ou accès Signature partagé (SAS) URI</b>: hello paramètres sont :<br/><br/><ul><b>URI de la table</b>: Spécifie hello Public ou l’URL SAS pour la table de hello.<br/><br/><b>Spécifie les tooscan de lignes hello pour les noms de propriété</b>: les valeurs hello sont <i>TopN</i> tooscan hello un nombre spécifié de lignes, ou <i>ScanAll</i> tooget toutes les lignes dans la table de hello. <br/><br/>Si les données de salutation sont homogènes et prévisibles, il est recommandé de sélectionner *TopN* et entrez un nombre pour N. Pour les tables volumineuses, cela peut être plus rapide lors de la lecture.<br/><br/>Si les données de salutation sont structurées avec des jeux de propriétés qui varient en fonction de la profondeur de hello et la position de la table de hello, choisissez hello *ScanAll* option tooscan toutes les lignes. Cela garantit l’intégrité de hello de votre propriété résultante et la conversion de métadonnées.<br/><br/></ul><b>Compte de stockage privé</b>: hello paramètres sont : <br/><br/><ul><b>Nom du compte</b>: Spécifie le nom hello du compte hello contenant hello table tooread.<br/><br/><b>Clé de compte</b>: Spécifie la clé de stockage hello associée au compte de hello.<br/><br/><b>Nom de la table</b> : Spécifie le nom hello de table hello contenant hello données tooread.<br/><br/><b>Tooscan de lignes pour les noms de propriété</b>: les valeurs hello sont <i>TopN</i> tooscan hello un nombre spécifié de lignes, ou <i>ScanAll</i> tooget toutes les lignes dans la table de hello.<br/><br/>Si les données de salutation sont homogènes et prévisibles, nous vous recommandons de sélectionner *TopN* et entrez un nombre pour N. Pour les tables volumineuses, cela peut être plus rapide lors de la lecture.<br/><br/>Si les données de salutation sont structurées avec des jeux de propriétés qui varient en fonction de la profondeur de hello et la position de la table de hello, choisissez hello *ScanAll* option tooscan toutes les lignes. Cela garantit l’intégrité de hello de votre propriété résultante et la conversion de métadonnées.<br/><br/> |
| un stockage Azure Blob |Lit les données stockées dans le service d’objets Blob hello dans le stockage Azure, y compris les images, de texte non structuré ou de données binaires.<br/><br/>Vous pouvez utiliser hello Blob service toopublicly exposez les données, ou tooprivately magasin application. Vous pouvez accéder à vos données depuis n’importe où grâce à des connexions HTTP ou HTTPS. |Hello options Bonjour **importer des données** modification module selon que vous accédez à des informations publiques ou à un compte de stockage privé qui nécessite des informations d’identification de connexion. Cela est déterminé par hello <b>Type d’authentification</b> qui peut avoir une valeur de « PublicOrSAS » ou « Compte ».<br/><br/><b>Public ou accès Signature partagé (SAS) URI</b>: hello paramètres sont :<br/><br/><ul><b>URI</b>: Spécifie hello Public ou l’URL SAS pour l’objet blob de stockage hello.<br/><br/><b>Format de fichier</b>: Spécifie le format hello de données de hello Bonjour service Blob. formats de Hello pris en charge sont CSV, TSV et ARFF.<br/><br/></ul><b>Compte de stockage privé</b>: hello paramètres sont : <br/><br/><ul><b>Nom du compte</b>: Spécifie nom hello du compte hello qui contient le blob hello souhaité tooread.<br/><br/><b>Clé de compte</b>: Spécifie la clé de stockage hello associée au compte de hello.<br/><br/><b>Chemin d’accès toocontainer, répertoire ou blob </b> : Spécifie le nom hello du blob hello contenant hello données tooread.<br/><br/><b>Format du fichier BLOB</b>: Spécifie le format hello de données de hello dans le service blob hello. Hello formats de données pris en charge sont CSV, TSV, ARFF, CSV avec un encodage spécifié et Excel. <br/><br/><ul>Si le format de hello est CSV ou TSV, être tooindicate que si le fichier de hello contient une ligne d’en-tête.<br/><br/>Vous pouvez utiliser hello option tooread des données Excel à partir de classeurs Excel. Bonjour <i>format de données Excel</i> option, indiquez si les données de salutation sont dans une plage de feuille de calcul Excel ou dans un tableau Excel. Bonjour <i>feuille Excel ou table incorporée </i>option, spécifiez le nom hello de feuille de hello ou de la table que vous souhaitez tooread à partir de.</ul><br/> |
| Fournisseur de flux de données |Lit les données d’un fournisseur de flux pris en charge. Actuellement, seul format de protocole Open Data Protocol (OData) hello est pris en charge. |<b>Type de données de contenu</b>: Spécifie le format d’OData hello.<br/><br/><b>URL source</b>: Spécifie une URL complète pour le flux de données hello hello. <br/>Par exemple, hello suivant lectures d’URL à partir de la base de données Northwind hello : http://services.odata.org/northwind/northwind.svc/ |

## <a name="next-steps"></a>Étapes suivantes

[Déploiement de services web Azure ML utilisant les modules d’importation et d’exportation des données](machine-learning-web-services-that-use-import-export-modules.md)


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[export-data]: https://msdn.microsoft.com/library/azure/7A391181-B6A7-4AD4-B82D-E419C0D6522C/
