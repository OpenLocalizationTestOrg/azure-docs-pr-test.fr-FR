---
title: "outil d’évaluation de solutions d’analyse décisionnelle aaaCortana | Documents Microsoft"
description: "Microsoft Partner ici sont toutes les étapes de hello vous devez toofollow toopublish votre tooAppSource de solution Cortana Intelligence."
services: machine-learning
documentationcenter: 
author: AnupamMicrosoft
manager: jhubbard
editor: cgronlun
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: anupams;v-bruham;garye
ms.openlocfilehash: 76cde4e2090c121683b7026f3d80f90f64566607
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="cortana-intelligence-solution-evaluation-tool"></a>Outil d’évaluation de la solution Cortana Intelligence
## <a name="overview"></a>Vue d'ensemble
Vous pouvez utiliser hello Cortana Intelligence solution d’évaluation outil tooassess vos solutions d’analytique avancée pour la conformité avec les meilleures pratiques recommandées par Microsoft. Microsoft est heureux toowork avec nos partenaires (éditeurs de logiciels indépendants / SIs) tooprovide des solutions de haute qualité pour les clients, revendeurs et l’implémentation. Ce guide décrivent les processus de hello d’à l’aide de l’outil d’évaluation hello Solution avec votre solution et décrivent les meilleures pratiques spécifiques hello dans les vérifications pour.

## <a name="getting-started"></a>Prise en main
Veuillez [télécharger](https://aka.ms/aa-evaluation-tool-download) et installer l’outil d’évaluation de hello Cortana Intelligence solution.

Configuration requise :
- Windows 10 : [site officiel pour Windows 10](https://www.microsoft.com/en-us/windows)
- Azure PowerShell : [Installation et configuration d’Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0)

## <a name="identifying-your-app"></a>Identification de votre application
Une fois l’installation terminée, ouvrez l’outil de hello et commencez votre évaluation première.

![Outil d’évaluation ouvert](./media/cortana-intelligence-appsource-evaluation-tool/1-open-evaluation-tool.png)

Fournissez les informations d’identification relatives à votre solution.

![Connexion à un abonnement Azure](./media/cortana-intelligence-appsource-evaluation-tool/2-connect-azure-subscription.png)

Se connecter tooyour abonnement Azure et fournir hello groupe de ressources contenant votre application.

![Sélection des ressources](./media/cortana-intelligence-appsource-evaluation-tool/3-select-resources.png)

Une fois le groupe de ressources hello ont été chargée, sélectionnez les ressources hello qui sont inclus dans votre solution et identifient accessibilité hello toutes les ressources de données en tant que :
- Ingestion
- Consommation
- Interne

Nous utilisons ces informations toobetter comprendre comment votre solution utilise différents composants et tooensure orientés utilisateur composants sont cohérentes avec les meilleures pratiques.

### <a name="ingestion"></a>Ingestion
Réception dans ce cas signifie que toutes les sources de données sont toopull utilisé dans les données à partir de la solution de hello externe ou que tous les services en dehors de la solution de hello utilisent les données de toopush dans celui-ci.

### <a name="consumption"></a>Consommation
Dans ce cas, la consommation signifie les jeux de données qui sont utilisées toopush données tooend utilisateurs, directement ou indirectement. Par exemple :
- Jeux de données utilisés dans une requête directe à partir de PowerBI
- Jeux de données interrogés dans une application web

>[!NOTE]
Si une ressource spécifique est utilisée pour l’ingestion et la consommation, choisissez **Consommation**.

### <a name="internal"></a>Interne
Choisissez cette option pour toutes les ressources de données utilisées uniquement pour le traitement d’applications internes.

Ensuite, vous serez invité à tooprovide les informations d’identification valides pour les bases de données spécifiés à l’étape précédente de hello :

![Configuration préalable aux tests](./media/cortana-intelligence-appsource-evaluation-tool/4-set-test-prerequisites.png)

## <a name="solution-test-cases"></a>Cas de test de la solution
outil de solution Hello effectuera une collection de tests automatisés sur votre solution.

![Configuration de l’exécution des tests](./media/cortana-intelligence-appsource-evaluation-tool/5-set-test-execution.png)

Une fois hello tests terminés, vous serez invité tooprovide une explication ou la justification de la raison pour laquelle votre solution n’est pas conforme avec la spécification de hello.

![Indication d’une justification professionnelle](./media/cortana-intelligence-appsource-evaluation-tool/6-provide-business-justification.png)

Par exemple, si votre solution publie tooAzure SQL DW, évaluation hello tests requièrent tooalso vous publiez tooAzure Analysis Services. 

Votre solution peut utiliser des machines virtuelles IaaS exécutant SQL Server Analysis Services au lieu d’Azure Analysis Services. Il s’agit d’une raison acceptable de l’échec du test de hello.
## <a name="packaging-your-evaluation-results"></a>Empaquetage de vos résultats d’évaluation
Après avoir effectué les cas de test hello, votre package d’évaluation sera exporté tooa archive ZIP, et vous demandera tooprovide commentaires sur l’outil d’évaluation hello. 

Vous devez tooshare du fichier compressé avec Microsoft pour votre toobe solution évaluée avant la mise en route toobe approbation ajouté des résultats de ce test tooAppSource

![Notation de l’outil d’évaluation](./media/cortana-intelligence-appsource-evaluation-tool/7-grade-evaluation-tool.png)

Au-dessus de la section de cet article traite des diverses fonctionnalités de l’outil de hello, maintenant nous allons vous présenter les types des meilleures pratiques qui prend la valeur cet outil.

## <a name="security-evaluation-considerations"></a>Considérations sur l’évaluation de la sécurité
### <a name="databases-should-use-azure-active-directory-authentication"></a>Les bases de données doivent utiliser l’authentification Azure Active Directory
Toutes les ressources de SQL Azure ou Azure SQL DW dans hello sloution doivent être activées avec l’authentification Azure Active Directory (AAD). AAD fournit un emplacement unique de toomanage toutes les identités et les rôles.

| Pour plus d’informations sur l’un des sujets suivants : | Lisez l’article : |
| --- | --- |
| AAD avec SQL Database et SQL Data Warehouse | [Utiliser l’authentification Azure Active Directory pour l’authentification auprès de SQL Database ou de SQL Data Warehouse](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-aad-authentication) |
| Configuration et gestion d’AAD | [Configurer et gérer l’authentification Azure Active Directory avec SQL Database ou SQL Data Warehouse](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-aad-authentication-configure) |
| Authentification des applications web Azure | [Authentification et autorisation dans Azure App Service](https://docs.microsoft.com/en-us/azure/app-service/app-service-authentication-overview) |
| Configuration des applications web avec AAD | [Comment tooconfigure votre connexion de Service d’applications application toouse Azure Active Directory](https://docs.microsoft.com/en-us/azure/app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication)|

### <a name="datasets-accessible-tooend-users-should-support-role-based-access-control"></a>Jeux de données accessible tooend-les utilisateurs doivent prendre en charge le contrôle d’accès basé sur le rôle
Lors de l’exécution de l’outil d’évaluation hello, vous serez invité toospecify toute création de rapports ou la publication de ressources. Il est supposé que ces ressources sont destinées à un accès par les utilisateurs finaux et non par les développeurs. Ces ressources doivent être fournissent contrôle d’accès basé sur un rôle (RBAC) dans l’ordre tooensure que les utilisateurs finaux sont uniquement en mesure de tooaccess autorisé des données.

Plus précisément, un des hello suivant des ressources Azure peut être configuré avec RBAC et sont considérées comme acceptable :
- Sécurisé HDInsight, consultez [une présentation de la sécurité tooHadoop avec appartenant au domaine des clusters HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-domain-joined-introduction)
- Azure SQL : voir [Utiliser l’authentification Azure Active Directory pour l’authentification auprès de SQL Database ou de SQL Data Warehouse]( https://docs.microsoft.com/en-us/azure/sql-database/sql-database-aad-authentication)
- Azure Analysis Services : voir [Manage database roles and users for Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-database-users) (Gérer les utilisateurs et rôles de base de données pour Azure Analysis Services)
- Azure SQL Data Warehouse (sachez que, dans la mesure où SQL DW ne prend pas en charge RBAC, cette solution n’est pas recommandée pour un accès direct de l’utilisateur final).

Si vous utilisez un autre type de ressource qui prend en charge RBAC, spécifiez que dans la justification de cas de test hello.

### <a name="azure-data-lake-store-should-use-at-rest-encryption"></a>Azure Data Lake Store doit utiliser le chiffrement au repos
Azure Data Lake Store (ADLS) prend en charge le chiffrement au repos par défaut avec des clés de chiffrement gérées par ADLS. Vous pouvez également configurer le chiffrement à l’aide de Key Vault.

Pour plus d’informations sur la spécification des paramètres de chiffrement ADLS, voir [Créer un compte Azure Data Lake Store](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-get-started-portal#create-an-azure-data-lake-store-account).

### <a name="azure-sql-and-azure-sql-data-warehouse-should-use-encryption"></a>Azure SQL et Azure SQL Data Warehouse doivent utiliser le chiffrement
Azure SQL et Azure SQL DW prennent en charge le chiffrement TDE (Transparent Data Encryption), qui assure le chiffrement et le déchiffrement en temps réel des fichiers journaux et de données.

| Pour plus d’informations sur l’un des sujets suivants : | Lisez l’article : |
| --- | --- |
| Chiffrement transparent des données (TDE) | [Chiffrement transparent des données](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-tde) |
| Azure SQL Data Warehouse avec TDE | [Prise en main du chiffrement transparent des données (TDE)](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-encryption-tde-tsql) |
| Configuration d’Azure SQL avec TDE | [Transparent Data Encryption avec Azure SQL Database](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database) |
| Configuration d’Azure SQL avec Always Encrypted | [Key Vault : SQL Database avec Always Encrypted](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-always-encrypted-azure-key-vault)|

En outre tooTDE, SQL Azure prend également en charge la Always Encrypted, une nouvelle technologie de chiffrement de données qui garantit que les données sont chiffrées non seulement au repos pendant le déplacement entre client et serveur, mais aussi lors des données est en cours d’utilisation lors de l’exécution de commandes sur le serveur de hello.

### <a name="any-virtual-machines-must-be-deployed-from-hello-azure-marketplace"></a>Toutes les Machines virtuelles doivent être déployés à partir de hello Azure Marketplace
Dans l’ordre tooprovide un niveau de sécurité sur AppSource, nous avons besoin que tous les ordinateurs virtuels déployés dans le cadre d’une solution d’analyse décisionnelle de Cortana être certifiés et publiés sur hello Azure Marketplace.

liste actuelle de hello toosearch d’images Azure Marketplace, consultez [Microsoft Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute).

Pour plus d’informations sur la façon dont toopublish une image de machine virtuelle pour Azure Marketplace, consultez [Guide toocreate une image de machine virtuelle pour hello Azure Marketplace](https://docs.microsoft.com/en-us/azure/marketplace-publishing/marketplace-publishing-vm-image-creation).

## <a name="scalability-evaluation-considerations"></a>Considérations sur l’évaluation de l’extensibilité
### <a name="cortana-intelligence-solutions-should-include-a-scalable-big-data-platform"></a>Les solutions Cortana Intelligence doivent inclure une plateforme Big Data évolutive.
Solutions d’analyse décisionnelle de Cortana doivent pouvoir évoluer toovery les tailles de données de grande taille. Dans Azure, cela signifie qu’ils doivent inclure l’un des deux plateformes de données à l’échelle pétaoctet hello :
- Azure Data Lake Store
- Azure SQL Data Warehouse

Si votre solution ne requiert pas de prise en charge de ces tailles de données ou si vous utilisez une plateforme de données de remplacement, veuillez préciser dans la justification de cas de test hello.
### <a name="cortana-intelligence-solutions-should-include-dedicated-ingestion-data-environments"></a>Les solutions Cortana Intelligence doivent inclure des environnements de données d’ingestion dédiés.
D’une manière générale, il est préférable que les solutions Cortana Intelligence n’insèrent pas de données directement dans des sources de données relationnelles. Au lieu de cela, les données brutes doivent être stockées dans un environnement non structuré, avec des insertions/mises à jour idempotentes dans tous les magasins relationnels avec Azure Data Factory.

Pour plus d’informations sur la copie des données avec Azure Data Factory, voir [Didacticiel : Créer un pipeline avec l’activité de copie à l’aide de Visual Studio](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-copy-activity-tutorial-using-visual-studio).

### <a name="azure-sql-data-warehouse-should-use-polybase-for-data-ingestion"></a>Microsoft Azure SQL Data Warehouse doit utiliser PolyBase pour l’ingestion de données
Azure SQL DW prend en charge PolyBase, pour une ingestion de données parallèle et hautement évolutive. PolyBase vous permet de toouse Azure SQL DW tooissue l’interrogation des jeux de données externes stockées dans le stockage d’objets Blob Azure ou d’Azure Data Lake Store. Cela fournit des méthodes de tooalternative des mises à jour en bloc des performances supérieures.

Pour obtenir des instructions sur la prise en main de PolyBase et Azure SQL DW, consultez [Charger des données avec PolyBase dans SQL Data Warehouse](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-get-started-load-with-polybase).

Pour plus d’informations sur les meilleures pratiques avec PolyBase et Azure SQL DW, consultez [Guide d’utilisation de PolyBase dans SQL Data Warehouse](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-load-polybase-guide).

## <a name="availability-evaluation-considerations"></a>Considérations sur l’évaluation de la disponibilité

### <a name="datasets-accessible-tooend-users-should-support-a-large-volume-of-concurrent-users"></a>Les utilisateurs tooend accessible de jeux de données doivent prendre en charge un volume important d’utilisateurs simultanés
Lors de l’exécution de l’outil d’évaluation hello, vous serez invité toospecify toute création de rapports ou la publication de ressources. Il est supposé que ces ressources sont destinées à un accès par les utilisateurs finaux et non par les développeurs. Ces ressources doivent prendre en charge un nombre d’utilisateurs simultanés moyen à élevé.

Plus précisément, Azure SQL Data Warehouse ne doit pas être aux utilisateurs de tooend disponibles de la source de données unique hello. Si l’entrepôt de données SQL Azure est fournie en tant que ressource pour les utilisateurs avec pouvoir, Azure Analysis Services doit être rendus disponible tootypical utilisateurs.

Pour plus d’informations sur les limites d’accès simultané d’Azure SQL DW, consultez [Gestion de la concurrence et des charges de travail dans SQL Data Warehouse](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-develop-concurrency).

Pour plus d’informations sur Azure Analysis Services, consultez [Qu’est-ce qu’Azure Analysis Services ?](https://docs.microsoft.com/azure/analysis-services/analysis-services-overview).

### <a name="azure-sql-resources-should-have-a-read-only-replica-for-failover"></a>Les ressources Azure SQL doivent disposer d’un réplica en lecture seule pour le basculement
Bases de données SQL Azure prend en charge l’instance secondaire tooa de géo-réplication. Cette instance peut ensuite être utilisée comme une application de haute disponibilité de basculement instance tooprovide.

Pour plus d’informations sur la géoréplication pour les bases de données Azure SQL, consultez [Vue d’ensemble : groupes de basculement et géo-réplication active](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-geo-replication-overview).

Pour obtenir des instructions sur la façon de tooconfigure géo-réplication pour SQL Azure, consultez [configurer géo-réplication active pour la base de données SQL Azure avec Transact-SQL](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-geo-replication-transact-sql).

### <a name="azure-sql-data-warehouse-should-have-geo-redundant-backups-enabled"></a>Les sauvegardes géoredondantes doivent être activées sur Azure SQL Data Warehouse
Entrepôt de données SQL Azure prend en charge le stockage à redondance toogeo sauvegardes quotidiennes. Cette géo-réplication garantit que vous pouvez restaurer l’entrepôt de données hello même dans les situations où vous ne peut pas accéder aux instantanés stockés dans votre région principale. Cette fonctionnalité est activée par défaut et ne doit pas être désactivée pour les solutions Cortana Intelligence.

Pour plus d’informations sur les sauvegardes Azure SQL DW et la restauration, consultez [Sauvegardes SQL Data Warehouse](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-backups).

### <a name="virtual-machines-should-be-configured-with-availability-sets"></a>Les machines virtuelles doivent être configurées avec des groupes à haute disponibilité
Machines virtuelles doit être configurés dans les groupes à haute disponibilité affectera les hello toominimize ordre des événements de maintenance planifiées et non planifiées.

Pour plus d’informations sur la disponibilité de la machine virtuelle Azure, consultez [gérer la disponibilité hello de machines virtuelles Windows Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability).

## <a name="other-evaluation-considerations"></a>Autres considérations sur l’évaluation
### <a name="cortana-intelligence-apps-should-use-a-centralized-tool-for-data-orchestration"></a>Les applications Cortana Intelligence doivent utiliser un outil centralisé pour l’orchestration des données
L’utilisation d’un outil unique pour la gestion et la planification de la transformation et du déplacement des données garantit la cohérence des données critiques. Cette méthode fournit une logique claire vis-à-vis de la logique de nouvelle tentative, de la gestion des dépendances, des alertes/de la journalisation, etc. Nous vous recommandons d’utiliser hello [Azure Data Factory](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-introduction) pour l’orchestration de données dans Azure.

Si vous utilisez un ou plusieurs outils autres qu’Azure Data Factory pour l’orchestration des données, décrivez-les.
### <a name="azure-machine-learning-models-should-be-retrained-using-azure-data-factory"></a>Les modèles Microsoft Azure Machine Learning doivent être reformés avec Azure Data Factory
Azure Machine Learning (AzureML) de fournit des outils de toouse facile pour la création de hello et de déploiement de pipelines d’apprentissage et de modélisation prédictive. Toutefois, il est important que les déploiements de production de ces modèles AzureML n’est pas basé sur un seul jeu de données fixe, mais au lieu de cela adapte toohello changement dynamique de phénomènes du monde réel.

Pour plus d’informations sur la création de services web de reformation, voir [Reformation des modèles Machine Learning par programme](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-retrain-models-programmatically).

Pour plus d’informations sur l’automatisation des processus d’apprentissage hello modèle à l’aide d’Azure Data Factory, consultez [les modèles de mise à jour d’Azure Machine Learning à l’aide de la mise à jour de ressource activité](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-azure-ml-update-resource-activity).

## <a name="existing-documentation"></a>Documentation existante
[Microsoft Azure Certified de toogrow votre entreprise de cloud](https://azure.microsoft.com/en-us/marketplace/programs/certified/)

[Microsoft Azure Certified pour Cortana Intelligence](https://azure.microsoft.com/en-us/marketplace/programs/certified/cortana/)

