---
title: "aaaMigrate votre tooSQL de données Data Warehouse | Documents Microsoft"
description: "Conseils pour migrer votre tooAzure de données SQL Data Warehouse pour développer des solutions."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: d78f954a-f54c-4aa4-9040-919bc6414887
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/29/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: fe4c6b7e82094c59c45e06be6da225fee1b707ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-data"></a>Migration de vos données
Les données peuvent être déplacées à partir de différentes sources dans SQL Data Warehouse avec divers outils.  Copie de la définition d’application SSIS et bcp peuvent tous être utilisé tooachieve cet objectif. Toutefois, comme la quantité hello des données augmente, vous devez considérer sur la décomposition des processus de migration de données hello en étapes. Cela vous offre hello opportunité toooptimize chaque étape aussi bien pour les performances et résilience tooensure une migration régulier des données.

Cet article explique tout d’abord les scénarios de migration simple hello de copie de la définition d’application, SSIS et bcp. Il rechercher un peu plus loin dans la migration de hello peut être optimisée.

## <a name="azure-data-factory-adf-copy"></a>Azure Data Factory (ADF) Copy
[ADF Copy][ADF Copy] fait partie intégrante d’[Azure Data Factory][Azure Data Factory]. Vous pouvez utiliser ADF copie tooexport vos fichiers tooflat de données résidant sur le stockage local, les fichiers plats tooremote conservées dans le stockage blob Azure, ou directement dans l’entrepôt de données SQL.

Si vos données commencent dans les fichiers plats, vous devez tout d’abord tootransfer il tooAzure objet blob de stockage avant de lancer une charge dans l’entrepôt de données SQL. Une fois que les données de salutation sont transférées vers le stockage d’objets blob Azure, vous pouvez choisir toouse [ADF copie] [ ADF Copy] toopush à nouveau les données hello dans SQL Data Warehouse.

PolyBase fournit également une option de hautes performances pour le chargement des données de salutation. Si vous optez pour cette solution, cela ne signifie pas que vous utilisez deux outils au lieu d’un. Si vous avez besoin des performances optimales hello, utilisez PolyBase. Si vous souhaitez une expérience unique outil (et les données de salutation ne sont pas massives) ADF est la solution.


> 
> 

Principal sur toohello article à une grande suivant [exemples d’ADF][ADF samples].

## <a name="integration-services"></a>Integration Services
Integration Services (SSIS) est un outil puissant et flexible d’extraction, de transformation et de chargement (ETL, Extract Transform and Load) qui prend en charge des workflows complexes, la transformation des données et diverses options de chargement des données. Utiliser SSIS toosimply transfert données tooAzure ou dans le cadre d’une migration plus large.

> [!NOTE]
> SSIS peut exporter tooUTF-8 sans marque d’ordre d’octet dans le fichier de hello hello. tooconfigure cela vous devez d’abord utiliser hello dérivées des données colonne composant tooconvert hello caractère dans hello page de codes données flux toouse hello 65001 UTF-8. Une fois que les colonnes hello ont été convertis, écrivez hello données toohello fichier plat destination adaptateur en vérifiant que 65001 a également été sélectionné en tant que page de code hello pour le fichier de hello.
> 
> 

SSIS connecte tooSQL l’entrepôt de données comme il se connecte le déploiement de SQL Server tooa. Toutefois, vos connexions devrez toobe à l’aide d’un gestionnaire de connexions ADO.NET. Vous devez également prendre soin tooconfigure hello « Utiliser bulk insert lorsqu’il est disponible » débit toomaximize de paramètre. Reportez-vous toohello [adaptateur de destination ADO.NET] [ ADO.NET destination adapter] toolearn article plus d’informations sur cette propriété.

> [!NOTE]
> Connexion tooAzure SQL Data Warehouse à l’aide d’OLE DB n’est pas pris en charge.
> 
> 

En outre, il est toujours possible de hello qu’un package peut échouer en raison de problèmes réseau ou toothrottling. Conception de packages afin qu’ils peuvent reprendre à hello point de défaillance, sans répétition de travail qui sont terminés avant la défaillance de hello.

Pour plus d’informations, consultez hello [documentation de SSIS][SSIS documentation].

## <a name="bcp"></a>bcp
bcp est un utilitaire de ligne de commande qui est conçu pour l’importation et l’exportation des données des fichiers plats. Des activités de transformation peuvent avoir lieu durant l’exportation des données. transformations de simple tooperform utilisent une requête tooselect et transforment des données de hello. Une fois exporté, les fichiers plats hello peuvent ensuite être chargées directement dans la base de données SQL Data Warehouse hello cible hello.

> [!NOTE]
> Il est souvent une bonne idée tooencapsulate hello exporter des transformations utilisées au cours des données dans une vue de système de source de hello. Cela garantit que la logique hello est conservée et les processus hello sont répétée.
> 
> 

Les avantages de bcp sont les suivants :

* Simplicité. commandes de bcp sont toobuild simple et exécuter
* Processus de chargement redémarrable. Une fois exporté hello de charge peut être exécutée un nombre de fois

Les limites de l’utilitaire bcp sont les suivantes :

* bcp fonctionne avec des fichiers plats en format tableau uniquement. Cette solution ne prend pas en charge les fichiers aux formats xml ou JSON.
* Fonctionnalités de transformation de données sont limitées toohello étape d’exportation uniquement et sont de nature simples
* bcp n’a pas été adapté toobe fiable lorsque le chargement des données sur hello internet. Toute instabilité du réseau peut provoquer une erreur de chargement.
* bcp s’appuie sur le schéma hello être présents dans la base de données toohello préalable charger hello cible

Pour plus d’informations, consultez [utiliser des données de tooload bcp dans SQL Data Warehouse][Use bcp tooload data into SQL Data Warehouse].

## <a name="optimizing-data-migration"></a>Optimisation de la migration des données
Un processus de migration des données SQLDW peut être efficacement divisé en trois étapes distinctes :

1. Exportation des données sources
2. Transfert de données tooAzure
3. Charger dans la base de données SQLDW hello cible

Chaque étape peut être optimisée individuellement toocreate un processus de migration solide, redémarrés et fiable qui optimise les performances à chaque étape.

## <a name="optimizing-data-load"></a>Optimisation du chargement des données
En examinant ces valeurs dans l’ordre inverse pour un instant ; Hello plus rapide des tooload données sont via PolyBase. Optimisation pour un processus de chargement de PolyBase impose des conditions préalables sur hello étapes précédentes afin qu’il soit meilleures toounderstand cela initial. Il s'agit de :

1. Encodage des fichiers de données
2. Formatage des fichiers de données
3. Définition de l’emplacement des fichiers de données

### <a name="encoding"></a>Encodage
PolyBase requiert toobe de fichiers de données UTF-8 ou UTF-16FE. 



### <a name="format-of-data-files"></a>Formatage des fichiers de données
PolyBase requiert un terminateur de ligne fixe \n ou un renvoi à la ligne. Les fichiers de données doivent respecter les toothis standard. Il n’existe aucune restriction relative aux terminateurs de chaînes ou de colonnes.

Vous devez toodefine toutes les colonnes dans le fichier de hello en tant que partie de la table externe dans PolyBase. Assurez-vous que toutes les colonnes exportées sont requis et que les types hello sont conformes à des normes toohello requis.

Veuillez référer toohello [migrer votre schéma] article pour plus de détails sur les types de données pris en charge.

### <a name="location-of-data-files"></a>Définition de l’emplacement des fichiers de données
SQL Data Warehouse utilise exclusivement les données de tooload PolyBase à partir du stockage d’objets Blob Azure. Par conséquent, les données de salutation doivent avoir été tout d’abord transférées vers le stockage d’objets blob.

## <a name="optimizing-data-transfer"></a>Optimisation du transfert des données
Une des parties de la migration des données les plus lentes hello est transfert hello de hello données tooAzure. Cette étape peut être associée à une problématique de bande passante et entraver la progression, en réduisant la fiabilité du réseau. Par défaut, migration tooAzure de données est sur internet hello ainsi le risque d’erreurs de transfert en cours sont relativement peu susceptibles de hello. Toutefois, ces erreurs peuvent nécessiter toobe données envoyée à nouveau en totalité ou en partie.

Heureusement, vous avez plusieurs vitesse de hello tooimprove options et la résilience de ce processus :

### <a name="expressrouteexpressroute"></a>[ExpressRoute][ExpressRoute]
Vous souhaiterez peut-être à l’aide de tooconsider [ExpressRoute] [ ExpressRoute] toospeed de transfert de hello. [ExpressRoute] [ ExpressRoute] fournit vous avec un tooAzure connexion privée hello afin de la connexion de hello ne passe pas par internet public. Vous n’êtes aucunement obligé de recourir à cette option. Toutefois, cela permettra d’accroître le débit lors de la distribution des données tooAzure à partir d’un site local ou de colocalisation.

avantages de l’utilisation de Hello [ExpressRoute] [ ExpressRoute] sont :

1. Accroissement de la fiabilité
2. Augmentation de la vitesse du réseau
3. Réduction de la latence du réseau
4. Amélioration de la sécurité du réseau

[ExpressRoute] [ ExpressRoute] est bénéfique pour plusieurs scénarios ; hello non seulement de migration.

Vous êtes intéressé ? Pour plus d’informations et la tarification, visitez hello [documentation d’ExpressRoute][ExpressRoute documentation].

### <a name="azure-import-and-export-service"></a>Azure Import Export Service
Bonjour Azure Service d’importation et exportation est un processus de transfert de données conçu pour les grandes (en Go ++) toomassive (To ++) les transferts de données dans Azure. Elle implique l’écriture de votre toodisks de données et copie les centre de données Azure tooan. contenu du disque Hello est ensuite chargées dans les objets BLOB de stockage Azure à votre place.

Une vue d’ensemble du processus d’exportation importation hello est comme suit :

1. Configurer un stockage d’objets Blob Azure conteneur tooreceive hello de données
2. Exportation de stockage de données toolocal
3. Copiez hello données too3.5 pouce SATA II/III lecteurs de disque dur à l’aide de hello [outil d’importation/exportation Azure]
4. Créer un travail d’importation à l’aide de hello Azure Import Service et exportation qui fournit les fichiers de journal hello produits par hello [outil d’importation/exportation Azure]
5. Expédier les disques de hello votre centre de données Azure désigné
6. Vos données sont le conteneur de stockage d’objets Blob Azure tooyour transférés
7. Charger des données de hello dans SQLDW à l’aide de PolyBase

### <a name="azcopyazcopy-utility"></a>Utilitaire [AZCopy][AZCopy]
Hello [AZCopy][AZCopy] utilitaire est un excellent outil pour obtenir vos données transférées dans les objets BLOB de stockage Azure. Il est conçu pour les petites (Mo ++) toovery volumineux (en Go ++) des transferts de données. [AZCopy] a été conçue tooprovide bon résilient débit lorsque le transfert de données tooAzure, de sorte qu’est la solution idéale pour l’étape de transfert de données hello. Une fois transférées, vous pouvez charger des données hello à l’aide de PolyBase dans SQL Data Warehouse. Vous pouvez également intégrer AZCopy dans vos packages SSIS, en appliquant une tâche d’exécution du processus.

toouse AZCopy, vous allez tout d’abord besoin toodownload et installez-le. Une [version de production][production version] et une [préversion][preview version] sont disponibles.

tooupload un fichier à partir de votre système de fichiers que vous devez une commande telle que hello une ci-dessous :

```
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:abc.txt
```

Voici les étapes possibles d’un processus de niveau supérieur :

1. Configurer un stockage Azure blob conteneur tooreceive hello de données
2. Exportation de stockage de données toolocal
3. AZCopy vos données dans le conteneur de stockage d’objets Blob Azure hello
4. Charger des données de hello dans l’entrepôt de données SQL à l’aide de PolyBase

Documentation complète disponible : [AZCopy][AZCopy].

## <a name="optimizing-data-export"></a>Optimisation de l’exportation des données
En outre tooensuring qu’exportation de hello est conforme toohello besoins par PolyBase vous peut également demander à exporter de hello toooptimize hello tooimprove hello du processus de données supplémentaires.



### <a name="data-compression"></a>Compression des données
PolyBase peut lire les données compressées au format gzip. Si vous êtes en mesure de toocompress votre toogzip des fichiers de données, puis vous serez minimiser hello données poussées dans le réseau de hello.

### <a name="multiple-files"></a>Fichiers multiples
Avec rupture des tables volumineuses en plusieurs fichiers permet non seulement d’exporter la vitesse tooimprove, mais également avec transfert re-startability et hello facilité de gestion globale des données hello qu’une seule fois dans le stockage d’objets blob Azure hello. Une des hello de nombreuses fonctionnalités intéressantes de PolyBase est sa capacité à lire tous les fichiers à l’intérieur d’un dossier hello et traiter en tant qu’une seule table. Il est donc une bonne idée tooisolate hello des fichiers pour chaque table dans son propre dossier.

PolyBase prend également en charge une fonction appelée « balayage de dossier récursif ». Vous pouvez utiliser cette fonctionnalité toofurther améliorer votre gestion des données d’organisation hello de tooimprove de vos données exportées.

toolearn en savoir plus sur le chargement des données avec PolyBase, consultez [PolyBase d’utilisation des données de tooload dans SQL Data Warehouse][Use PolyBase tooload data into SQL Data Warehouse].

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur la migration, consultez [migrer votre entrepôt de données de tooSQL solution][Migrate your solution tooSQL Data Warehouse].
Pour obtenir des conseils supplémentaires en matière de développement, consultez la [vue d’ensemble du développement][development overview].

<!--Image references-->

<!--Article references-->
[AZCopy]:../storage/common/storage-use-azcopy.md
[ADF Copy]: ../data-factory/data-factory-data-movement-activities.md 
[ADF samples]: ../data-factory/data-factory-samples.md
[ADF Copy examples]: ../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md
[development overview]: sql-data-warehouse-overview-develop.md
[Migrate your solution tooSQL Data Warehouse]: sql-data-warehouse-overview-migrate.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[Use bcp tooload data into SQL Data Warehouse]: sql-data-warehouse-load-with-bcp.md
[Use PolyBase tooload data into SQL Data Warehouse]: sql-data-warehouse-get-started-load-with-polybase.md


<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory]: http://azure.microsoft.com/services/data-factory/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[ExpressRoute documentation]: http://azure.microsoft.com/documentation/services/expressroute/

[production version]: http://aka.ms/downloadazcopy/
[preview version]: http://aka.ms/downloadazcopypr/
[ADO.NET destination adapter]: https://msdn.microsoft.com/library/bb934041.aspx
[SSIS documentation]: https://msdn.microsoft.com/library/ms141026.aspx
