---
title: "aaaAzure SQL données entrepôt Forum aux Questions | Documents Microsoft"
description: "Cet article répertorie les questions fréquemment posées par les clients et les développeurs sur Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: 812CA525-3BF3-49DF-8DF3-FB4342464F4F
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: overview
ms.date: 3/1/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: 09fd3f65d9507b09fcb8f477742c7d020add2755
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-frequently-asked-questions"></a>Foire aux questions SQL Data Warehouse

## <a name="general"></a>Généralités

Q : Quelles sont les solutions offertes par SQL DW en matière de sécurité des données ?

R. SQL DW propose plusieurs solutions de protection des données, comme le chiffrement TDE et les audits. Pour plus d’informations, consultez [Sécurité].

Q : Où puis-je trouver les normes juridiques et commerciales auxquelles SQL DW est conforme ?

R : Visitez hello [Microsoft Compliance] page pour différentes offres de conformité par produit par exemple, le SOC et ISO. Tout d’abord choisir par titre de la conformité, puis développez Azure hello dans l’étendue Microsoft nuage section services sur le côté droit de hello de hello page toosee quels services sont des services Azure est conformes.

Q : Puis-je connecter Power BI ?

R. Oui. Bien que Power BI prenne en charge les requêtes directes avec SQL DW, il n’est pas destiné à traiter un grand nombre d’utilisateurs ou de données en temps réel. Pour une utilisation en production de Power BI, nous recommandons d’utiliser Power BI en complément d’Azure Analysis Services ou d’Analysis Service IaaS. 

Q : Quelles sont les limites de capacité de SQL Data Warehouse ?

R. Consultez notre page [Limites de capacité] actuelle. 

Q : Pourquoi ma Mise à l’échelle/Pause/Reprise est-elle si longue ?

R : Un certain nombre de facteurs peut influencer la durée hello pour les opérations de gestion de calcul. Une cause fréquente des opérations avec une durée d’exécution longue est l’annulation de transactions. Quand une opération de mise à l’échelle ou de pause est lancée, toutes les sessions entrantes sont bloquées et les requêtes sont vidées. Dans le système de type hello tooleave de commande dans un état stable, les transactions doivent être restaurées avant une opération puisse commencer. Hello plus grand nombre de hello et la plus grande taille de journal hello des transactions, opération hello plue de hello est bloquée hello système tooa stable état de restauration.

## <a name="user-support"></a>Service client

Q : J’ai une suggestion de fonctionnalité, où dois-je l’envoyer ?

R. Si vous souhaitez faire une demande de fonctionnalité, envoyez-la sur notre page [UserVoice].

Q : Comment faire x ?

R. Pour obtenir de l’aide concernant le développement avec SQL Data Warehouse, vous pouvez poser des questions sur notre page [Stack Overflow]. 

Q : Comment envoyer un ticket de support ?

R. Les [tickets de support] peuvent être déposés sur le Portail Azure.

## <a name="sql-languagefeature-support"></a>Prise en charge de fonctionnalités / langages SQL 

Q : Quels sont les types de données pris en charge par SQL Data Warehouse ?

R. Consultez la page [Types de données] SQL Data Warehouse.

Q : Quelles fonctionnalités de table prenez-vous en charge ?

R. SQL Data Warehouse prend en charge de nombreuses fonctionnalités, mais pas toutes ; celles qui ne sont pas prises en charge sont documentées dans [Fonctionnalités de table non prises en charge].

## <a name="tooling-and-administration"></a>Outils et administration

Q : Prenez-vous en charge les projets de base de données dans Visual Studio ?

R. À l’heure actuelle, nous ne prenons pas en charge les projets de base de données dans Visual Studio pour SQL Data Warehouse. Si vous souhaitez que toocast un tooget vote cette fonctionnalité, visitez notre User Voice [demande des fonctionnalités des projets de base de données].

Q : SQL Data Warehouse prend-il en charge les API REST ?

R. Oui. La plupart des fonctionnalités REST utilisables avec SQL Database sont également disponibles avec SQL Data Warehouse. Vous trouverez des informations sur les API sur les pages de documentation REST ou sur [MSDN].


## <a name="loading"></a>Chargement

Q : Quels pilotes clients prenez-vous en charge ?

R : Prise en charge de pilote pour l’entrepôt de données se trouvent sur hello [les chaînes de connexion] page

Q : Quels sont les formats de fichier pris en charge par PolyBase avec SQL Data Warehouse ?

R : Orc, RC, Parquet et le texte plat délimité

Q : que se connecter à l’aide de PolyBase de toofrom SQL DW ? 

R : [Azure Data Lake Store] et [Azure Storage Blobs].

Q : est poussée vers le bas de calcul possible lors de la connexion tooAzure d’objets BLOB de stockage ou ADLS ? 

R : non, SQL Data Warehouse PolyBase interagit uniquement les composants de stockage hello. 

Q : puis-je connecter tooHDI ?

R : HDI pouvez utiliser ADLS ou WASB comme couche HDFS hello. Si vous avez l’un des deux comme couche HDFS, vous pouvez charger ces données dans SQL DW. Toutefois, vous ne pouvez pas générer instance HDI de poussée vers le bas calcul toohello. 

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur SQL Data Warehouse dans son ensemble, consultez notre page [Vue d’ensemble].


<!-- Article references -->
[UserVoice]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[les chaînes de connexion]: ./sql-data-warehouse-connection-strings.md
[Stack Overflow]: http://stackoverflow.com/questions/tagged/azure-sqldw
[tickets de support]: ./sql-data-warehouse-get-started-create-support-ticket.md
[Sécurité]: ./sql-data-warehouse-overview-manage-security.md
[Microsoft Compliance]: https://www.microsoft.com/en-us/trustcenter/compliance/complianceofferings
[Limites de capacité]: ./sql-data-warehouse-service-capacity-limits.md
[Types de données]: ./sql-data-warehouse-tables-data-types.md
[Fonctionnalités de table non prises en charge]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[Azure Data Lake Store]: ./sql-data-warehouse-load-from-azure-data-lake-store.md
[Azure Storage Blobs]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[demande des fonctionnalités des projets de base de données]: https://feedback.azure.com/forums/307516-sql-data-warehouse/suggestions/13313247-database-project-from-visual-studio-to-support-azu
[MSDN]: https://msdn.microsoft.com/en-us/library/azure/mt163685.aspx
[Vue d’ensemble]: ./sql-data-warehouse-overview-faq.md