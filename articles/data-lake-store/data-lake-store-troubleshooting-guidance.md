---
title: aaaFrequently aux questions pour Azure Data Lake Store | Documents Microsoft
description: "Aide à la résolution ou à l’atténuation des problèmes rencontrés avec Azure Data Lake Store"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: bf7fd555-3e30-43ce-b28c-c3ad0a241fdb
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: eeabdeef18f3b72901bd1a14283f85dd9c0ead44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-azure-data-lake-store"></a>Forum aux questions pour Azure Data Lake Store
Dans cet article, vous découvrirez tooAzure connexe du Forum aux questions sur Data Lake Store.

## <a name="how-can-i-further-protect-my-data-from-region-wide-disasters-or-accidental-deletions"></a>Comment puis-je renforcer la protection de mes données contre les sinistres régionaux et les suppressions accidentelles ?
les données de salutation dans votre compte Azure Data Lake Store sont résilient tootransient des défaillances de matériel dans une région via les réplicas automatisés. Cela garantit la durabilité et une haute disponibilité, hello de réunion contrat SLA de Azure données Lake Store. Voici quelques conseils sur la façon dont toofurther protéger vos données à partir des pannes à l’échelle de la région rares ou les suppressions accidentelles.

### <a name="disaster-recovery-guidance"></a>Guide de récupération d’urgence
Il est essentiel pour chaque client tooprepare leur propre plan de récupération d’urgence. Consultez votre plan de récupération d’urgence toohello documentation sur Azure sous toobuild. Voici quelques ressources qui peuvent vous aider à créer votre propre plan.

* [Récupération d’urgence et haute disponibilité pour les applications Azure](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md)
* [Guide technique de la résilience Azure](../resiliency/resiliency-technical-guidance.md)

#### <a name="best-practices"></a>Meilleures pratiques
Nous vous conseillons de copier vos données critiques de tooanother compte Data Lake Store dans une autre région ayant une fréquence aligné toohello des besoins de votre plan de récupération d’urgence. Il existe une multitude de l’intégration des données méthodes toocopy [ADLCopy](data-lake-store-copy-data-azure-storage-blob.md), [Azure PowerShell](data-lake-store-get-started-powershell.md) ou [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md). Azure Data Factory est un service utile pour créer et déployer des pipelines de déplacement des données à intervalles réguliers.

Si une panne régionale se produit, vous pouvez ensuite accéder vos données dans la région de hello où les données de salutation a été copiées. Vous pouvez surveiller hello [tableau de bord d’intégrité de Service Azure](https://azure.microsoft.com/status/) toodetermine hello l’état du service Azure monde hello.

### <a name="data-corruption-or-accidental-deletion-recovery-guidance"></a>Aide à la récupération suite à une corruption de données ou à une suppression accidentelle
Si Azure Data Lake Store assure la résilience des données via des réplicas automatisés, cela ne protège aucunement votre application (ou les développeurs/utilisateurs) de la corruption des données ou d’une suppression accidentelle.

#### <a name="best-practices"></a>Meilleures pratiques
tooprevent une suppression accidentelle, nous vous recommandons de définir des stratégies d’accès correct hello pour votre compte Data Lake Store.  Cela inclut l’application [verrous des ressources Azure](../azure-resource-manager/resource-group-lock-resources.md) toolock vers le bas des ressources importantes, ainsi que des application contrôle d’accès au niveau compte et le fichier à l’aide de hello disponible [les fonctionnalités de sécurité Data Lake Store](data-lake-store-security-overview.md). Nous vous recommandons également de créer régulièrement des copies de vos données critiques avec [ADLCopy](data-lake-store-copy-data-azure-storage-blob.md), [Azure PowerShell](data-lake-store-get-started-powershell.md) ou [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md) dans un autre compte Data Lake Store, dossier ou abonnement Azure.  Cela peut être utilisé toorecover à partir d’un incident de corruption ou de suppression de données. Azure Data Factory est un service utile pour créer et déployer des pipelines de déplacement des données à intervalles réguliers.

Les organisations peuvent également activer [journalisation des diagnostics](data-lake-store-diagnostic-logs.md) pour leurs Azure Data Lake Store compte toocollect des pistes d’audit d’accès aux données qui fournit des informations qui peuvent avoir supprimé ou mis à jour un fichier.

## <a name="next-steps"></a>Étapes suivantes
* [Prise en main d’Azure Data Lake Store](data-lake-store-get-started-portal.md)
* [Sécuriser les données dans Data Lake Store](data-lake-store-secure-data.md)

