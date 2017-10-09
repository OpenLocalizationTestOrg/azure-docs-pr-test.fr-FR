---
title: aaaWhat est Azure Analysis Services | Documents Microsoft
description: "Obtenir une image de grande hello d’Analysis Services dans Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 83d7a29c-57ae-4aa0-8327-72dd8f00247d
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/01/2017
ms.author: owend
ms.openlocfilehash: 48830a86f47a8ddc7770e6c44dd56c29927fe582
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-analysis-services"></a>Qu’est-ce qu’Azure Analysis Services ?
![Azure Analysis Services](./media/analysis-services-overview/aas-overview-aas-icon.png)

Azure Analysis Services fournit des données d’entreprise de modélisation dans le cloud de hello. Il s’agit d’une plateforme en tant que service (PaaS) entièrement gérée et intégrée aux services de plateforme de données Azure. 

Analysis Services vous permet de regrouper et combiner des données provenant de plusieurs sources, de définir des mesures et de sécuriser vos données dans un seul modèle de données sémantique approuvé. modèle de données Hello un moyen plus facile et plus rapide pour votre toobrowse les utilisateurs des volumes importants de données avec les applications clientes telles que Power BI, Excel, Reporting Services, applications de tiers et personnalisées.

![Sources de données](./media/analysis-services-overview/aas-overview-data-sources.png)

Extraire [cette vidéo](https://sec.ch9.ms/ch9/d6dd/a1cda46b-ef03-4cea-8f11-68da23c5d6dd/AzureASoverview_high.mp4) toolearn comment Azure Analysis Services s’intégrer à Microsoft de l’ensemble des fonctionnalités de BI et comment vous pouvez tirer parti de la mise en route de vos modèles de données dans le cloud de hello.

## <a name="built-on-sql-server-analysis-services"></a>Basé sur SQL Server Analysis Services
Azure Analysis Services est compatible avec de nombreuses fonctionnalités d’exception déjà intégrées à SQL Server Analysis Services Enterprise Edition. Azure Analysis Services prend en charge les modèles tabulaires au hello 1200 et 1400 [niveaux de compatibilité](analysis-services-compat-level.md). Les partitions, la sécurité au niveau des lignes, les relations bidirectionnelles et les traductions sont toutes prises en charge. Des modes en mémoire et des modes DirectQuery signifient des requêtes ultra-rapides sur des jeux de données massifs et complexes.

Les modèles tabulaires offrent un développement rapide et sont hautement personnalisables. Pour les développeurs, les modèles tabulaires incluent des objets de modèle toodescribe hello le modèle d’objet tabulaire (TOM). TOM est exposé au format JSON via hello [TMSL Tabular Model Scripting Language ()](https://docs.microsoft.com/sql/analysis-services/tabular-model-scripting-language-tmsl-reference) et hello langage de définition de données AMO via hello [Microsoft.AnalysisServices.Tabular](https://msdn.microsoft.com/library/microsoft.analysisservices.tabular.aspx) espace de noms.

## <a name="better-with-azure"></a>Meilleur avec Azure
Azure Analysis Services s’intègre à de nombreux services Azure, ce qui vous toobuild sophistiqué des solutions d’analytique. Intégration avec [Azure Active Directory](../active-directory/active-directory-whatis.md) fournit des données critiques de tooyour un accès sécurisé en fonction du rôle. Intégrer [Azure Data Factory](../data-factory/data-factory-introduction.md) pipelines en incluant une activité qui charge des données dans le modèle de hello. [Azure Automation](../automation/automation-intro.md) et [Azure Functions](../azure-functions/functions-overview.md) sont utilisables pour une orchestration légère de modèles à l’aide d’un code personnalisé.

## <a name="get-up-and-running-quickly"></a>Opérationnel rapidement
Dans le portail Azure, vous pouvez [créer un serveur](analysis-services-create-server.md) en quelques minutes. Et, avec les [modèles](../azure-resource-manager/resource-manager-create-first-template.md) Azure Resource Manager et PowerShell, vous pouvez approvisionner des serveurs à l’aide d’un modèle déclaratif. Un même modèle vous permet de déployer plusieurs services, ainsi que d’autres composants Azure tels que des comptes de stockage et Azure Functions. 

Une fois que vous avez créé un serveur, vous pouvez créer un modèle tabulaire directement dans le portail Azure. Avec la nouvelle hello (version préliminaire) [les fonctionnalités du Concepteur Web](analysis-services-create-model-portal.md), vous pouvez vous connecter tooan Azure SQL Database, la source de données Azure SQL Data Warehouse, ou importer un fichier .pbix de Power BI Desktop. Relations entre les tables sont créées automatiquement, et vous pouvez créer des mesures ou modifier le fichier model.bim de hello au format json droite à partir de votre navigateur.

## <a name="scale-tooyour-needs"></a>Mise à l’échelle tooyour besoins
Azure Analysis Services est disponible pour les niveaux Développeur, De base et Standard. Dans chaque niveau, les coûts de plan varient la taille d’alimentation, QPUs et la mémoire conséquente tooprocessing. Lorsque vous créez un serveur, vous sélectionnez un plan au sein d’un niveau. Vous pouvez modifier les plans ou vers le bas dans hello de même niveau ou niveau supérieur de tooa mise à niveau, mais vous ne pouvez pas rétrograder à partir d’un niveau inférieur de la tooa de niveau supérieur.

Montez en puissance, descendez en puissance ou suspendez votre serveur. Utilisez hello portail Azure ou contrôle total à la volée à l’aide de PowerShell. Vous paierez uniquement pour ce que vous utiliserez. toolearn en savoir plus sur les différents plans de hello et niveaux et utilisez hello calculatrice toodetermine hello droite plan de tarification, consultez [Analysis Services de la tarification Azure](https://azure.microsoft.com/pricing/details/analysis-services/).

## <a name="keep-your-data-close"></a>Conserver vos données à proximité
Les serveurs Analysis Services Azure peuvent être créés dans suivant de hello [régions Azure](https://azure.microsoft.com/regions/):

| Amérique | Europe | Asie-Pacifique |
|----------|--------|--------------|
|  Sud du Brésil<br> Centre du Canada<br> Est des États-Unis 2<br> États-Unis - partie centrale septentrionale<br> Centre-Sud des États-Unis<br> Ouest-Centre des États-Unis<br> Ouest des États-Unis | Europe du Nord<br> Sud du Royaume-Uni<br> Europe de l'Ouest |   Sud-est de l’Australie<br> Est du Japon<br> Asie du Sud-Est<br> Inde occidentale  |

Nouvelles régions sont ajoutées toutes les périodes de hello, cette liste peut donc être incomplet. Vous choisissez un emplacement lorsque vous créez votre serveur dans le portail Azure ou à l’aide des modèles Azure Resource Manager. tooget hello meilleures performances, choisissez un emplacement le plus proche de votre base d’utilisateurs plus grand. Garantissez-vous une [haute disponibilité](analysis-services-bcdr.md) en déployant vos modèles sur des serveurs redondants dans plusieurs régions.

## <a name="migrate-your-existing-tabular-models"></a>Migrer vos modèles tabulaires existants
Si vous avez déjà des solutions de modèles de SQL Server Analysis Services sur site existantes, vous pouvez migrer tooAzure Analysis Services sans apporter de modifications importantes. toomigrate, vous pouvez utiliser SSDT toodeploy votre serveur tooyour de modèle. Ou, dans SSMS, vous pouvez utiliser la fonction de sauvegarde et restauration ou TMSL.

Si vous avez des sources de données locales, vous devez tooinstall et configurer un [passerelle de données locale](analysis-services-gateway.md). Si vous avez des rôles et les membres du rôle déjà configurés, migrer des rôles, mais vous avez tooreadd les membres du rôle à l’aide de SSMS ou PowerShell.

## <a name="connect-toopopular-data-sources"></a>Connecter des sources de données toopopular
Azure Analysis Services prend en charge [connexion toodata](analysis-services-datasource.md) locales de votre organisation et dans le cloud de hello. Combinez des données provenant de sources de données locales et d’un cloud pour une solution hybride. 

Nouveaux modèles tabulaires de 1400 utilisent hello moderne obtenir des données de SSDT, selon le langage de requête formule hello M. Obtenir des données, vous avez plus de transformation de données et les fonctionnalités de l’application Web hybride et hello capacité toocreate et modifiez vos propres requêtes de langage de formule M avancées. Par exemple, avec les modèles tabulaires 1400, vous pouvez modéliser sur les fichiers de données dans Azure Blob Storage.

## <a name="use-hello-tools-you-already-know"></a>Utiliser les outils de hello que vous connaissez déjà

![Outils de développement BI](./media/analysis-services-overview/aas-overview-dev-tools.png)

#### <a name="sql-server-data-tools-ssdt-for-visual-studio"></a>SQL Server Data Tools pour Visual Studio (SSDT)
Développer et déployer des modèles avec hello libre [SQL Server Data Tools (SSDT) pour Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx). SSDT inclut des modèles de projet Analysis Services opérationnels rapidement. SSDT inclut désormais hello moderne obtenir des données source de données de requêtes et de l’application Web hybride fonctionnalités pour les modèles tabulaires 1400. Si vous êtes familiarisé avec obtenir des données dans Power BI Desktop et Excel 2016, vous savez déjà comment il est facile de toocreate les requêtes de sources de données hautement personnalisée.

#### <a name="sql-server-management-studio"></a>SQL Server Management Studio
Gérez vos serveurs et bases de données model à l’aide de [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx). Connecter des serveurs tooyour dans le cloud de hello. Exécutez les scripts TMSL directement à partir de la fenêtre de requête XMLA hello et automatiser des tâches à l’aide des scripts TMSL. De nouvelles fonctionnalités sont régulièrement implémentées : SSMS est mis à jour tous les mois.

#### <a name="powershell"></a>PowerShell
Tâches de gestion de ressources de serveur, comme la création de serveurs, la suspension ou la reprise des opérations de serveur ou la modification du niveau de service hello (niveau) utilisent les applets de commande Azure Resource Manager (Azure Resource Manager). Autres tâches de gestion des bases de données telles que l’ajout ou la suppression de membres du rôle, le traitement, ou en cours d’exécution des scripts TMSL utiliser des applets de commande dans le module SqlServer de hello. Modules Azure Resource Manager et SQL Server sont disponibles dans hello [PowerShell gallery](https://www.powershellgallery.com/).


## <a name="your-data-is-secure"></a>Sécuriser vos données
![Visualisations de données](./media/analysis-services-overview/aas-overview-secure.png)

#### <a name="authentication"></a>Authentification
L’authentification utilisateur pour Azure Analysis Services est gérée par [Azure Active Directory (AAD)](../active-directory/active-directory-whatis.md). Lors de la tentative de toolog dans la base de données tooan Azure Analysis Services, les utilisateurs une identité de compte d’organisation avec la base de données access toohello ils essaient tooaccess. Ces identités d’utilisateur doivent être membres de la valeur par défaut de hello Azure Active Directory pour l’abonnement de hello où réside hello Azure Analysis Services serveur. toolearn, voir [d’authentification et les autorisations utilisateur](analysis-services-manage-users.md).

#### <a name="data-security"></a>Sécurité des données
Azure Analysis Services utilise le stockage Blob Azure storage toopersist et les métadonnées des bases de données Analysis Services. Les fichiers de données Blob sont chiffrés à l’aide du chiffrement côté serveur (SSE) Azure Blob. Si vous utilisez le mode Requête directe, seules les métadonnées sont stockées. les données réelles Hello sont accessible à partir de la source de données hello au moment de la requête.

#### <a name="on-premises-data-sources"></a>Sources de données locales
Sécuriser l’accès toodata résidant localement dans votre organisation est obtenue en installant et configurant un [passerelle de données locale](analysis-services-gateway.md). Les passerelles constituent toodata d’accès pour les requêtes directes et les modes en mémoire. Lorsqu’un modèle Azure Analysis Services connecte la source de données locale tooan, une requête est créée avec informations d’identification chiffrée de hello pour la source de données locale hello. service de cloud de passerelle Hello analyse hello requête et exécute un push de hello demande tooan Azure Service Bus. passerelle locale de Hello interroge hello Azure Service Bus pour les demandes en attente. passerelle de Hello puis obtient hello requête, déchiffre les informations d’identification hello et connecte toohello source de données pour l’exécution. Hello résultats sont ensuite envoyés à partir de la source de données hello, sauvegarder toohello passerelle et ensuite sur toohello Azure Analysis Services de base de données.

Azure Analysis Services est régie par hello [termes du contrat de Services en ligne Microsoft](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) et hello [déclaration de confidentialité Microsoft Online Services](https://www.microsoft.com/privacystatement/OnlineServices/Default.aspx).
toolearn en savoir plus sur la sécurité dans Azure, consultez hello [Microsoft Trust Center](https://www.microsoft.com/trustcenter/Security/AzureSecurity).

## <a name="supports-hello-latest-client-tools"></a>Prend en charge des outils clients de la dernière hello
![Visualisations de données](./media/analysis-services-overview/aas-overview-clients.png)

Les outils modernes d’exploration et de visualisation de données comme Power BI, Excel et d’autres outils tiers fournissent aux utilisateurs des informations hautement interactives et visuellement riches sur vos données de modèles.

Les clients utilisent MSOLAP, AMO ou ADOMD [les bibliothèques clientes](analysis-services-data-providers.md) serveurs des Services tooconnect tooAnalysis. Les applications clientes Microsoft telles que Power BI Desktop et Excel installent les trois bibliothèques clientes. Mais n’oubliez pas, selon la version de hello ou la fréquence des mises à jour, les bibliothèques clientes peut-être pas les versions les plus récentes hello requises par Azure Analysis Services. Hello va de même toocustom applications ou autres interfaces telles que AsCmd, TOM, ADOMD.NET. Ces applications requièrent généralement l’installation manuelle des bibliothèques de hello en tant que partie d’un package.


## <a name="get-help"></a>Obtenir de l’aide

#### <a name="documentation"></a>Documentation
Azure Analysis Services est toomanage et tooset simple des. Vous pouvez trouver toutes les informations de hello vous devez toocreate et gérez vos services de serveur ici. Lorsque vous créez un serveur de données modèle toodeploy tooyour, il a bien même hello car il s’agit de la création d’un modèle de données que vous déployez le serveur local de tooan. Une bibliothèque importante de concepts, de procédures, de didacticiels et d’articles de référence est disponible dans [Analysis Services](https://docs.microsoft.com/sql/analysis-services/analysis-services).

#### <a name="videos"></a>Vidéos
Visionnez différentes vidéos utiles dans [Azure Analysis Services sur Channel 9](https://channel9.msdn.com/series/Azure-Analysis-Services).

#### <a name="blogs"></a>Blogs
Les choses évoluent rapidement. Vous pouvez toujours obtenir les dernières informations en hello sur hello [blog de l’équipe Analysis Services](https://blogs.msdn.microsoft.com/analysisservices/) et [blog Azure](https://azure.microsoft.com/blog/).

#### <a name="community"></a>Communauté
Analysis Services a une communauté active d’utilisateurs. Participez à des conversations de hello [forum Azure Analysis Services](https://aka.ms/azureanalysisservicesforum).

## <a name="feedback"></a>Commentaires
Vous avez des suggestions ou des demandes de fonctionnalités ? Être tooleave que vos commentaires sur [Azure Analysis Services commentaires](https://aka.ms/azureanalysisservicesfeedback).

Vous avez des suggestions sur la documentation de hello ? Vous pouvez ajouter des commentaires à l’aide de Livefyre bas hello de chaque article.

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous en savez plus sur Azure Analysis Services, il est temps tooget a démarré. Découvrez comment trop[créer un serveur](analysis-services-create-server.md) dans Azure. Lorsque votre serveur est prêt, parcourez hello [didacticiel Adventure Works](tutorials/aas-adventure-works-tutorial.md) toolearn comment toocreate un modèle tabulaire entièrement fonctionnel et déployez-le tooyour server.
