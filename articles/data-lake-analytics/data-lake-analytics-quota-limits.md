---
title: "aaaAzure limites de Quota de données Lake Analytique | Documents Microsoft"
description: "Découvrez comment tooadjust et l’augmentation de quota limite dans les comptes Azure données Lake Analytique (ADLA)."
services: data-lake-analytics
keywords: Service Analytique Azure Data Lake
documentationcenter: 
author: omidm1
editor: omidm1
ms.assetid: 49416f38-fcc7-476f-a55e-d67f3f9c1d34
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: omidm
ms.openlocfilehash: 875c4d00e0c57414031e50754495c02162bdca48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-lake-analytics-quota-limits"></a>Limites de quota pour Azure Data Lake Analytics

Découvrez comment tooadjust et l’augmentation de quota limite dans les comptes Azure données Lake Analytique (ADLA). Il vous sera plus simple d’appréhender le comportement de vos tâches U-SQL si vous connaissez ces limites. Toutes les limites de quota sont paramétrés, vous pouvez augmenter les limites maximales hello par approcher toous.

## <a name="azure-subscriptions-limits"></a>Limites des abonnements Azure

**Nombre maximal de comptes ADLA par abonnement :** 5.

 Ceci est hello le nombre maximal de comptes ADLA que vous pouvez créer par abonnement. Si vous essayez de compte ADLA toocreate un sixième, vous obtiendrez une erreur « Vous avez atteint nombre maximal de hello des comptes Analytique lac de données autorisés (5) dans la zone sous le nom de l’abonnement ». Dans ce cas, supprimez tous les comptes ADLA inutilisés ou atteindre toous par [ouvrant un ticket de support](#increase-maximum-quota-limits).

## <a name="adla-account-limits"></a>Limites des comptes ADLA

**Nombre maximal d’unités Analytics par compte :**  250

Il s’agit de nombre maximal de hello de AUs pouvant s’exécuter simultanément dans votre compte. Si le nombre total d’unités Analytics exécutées dans l’ensemble des tâches dépasse cette limite, les tâches les plus récentes sont automatiquement placées dans la file d’attente. Par exemple :

* Si vous avez un seul travail en cours d’exécution avec 250 AUs, lorsque vous soumettez une seconde tâche attend dans la file d’attente des travaux hello hello première tâche se termine.
* Si vous avez déjà cinq tâches en cours d’exécution et que chacune utilise 50 AUs, lorsque vous soumettez une tâche sixième dont a besoin de 20 AUs qu’elle attend dans la file d’attente des travaux hello sont 20 AUs disponibles.

**Nombre maximal de tâches U-SQL simultanées par compte :** 20

Ceci est hello le nombre maximal de tâches pouvant s’exécuter simultanément dans votre compte. Au-dessus de cette valeur, les tâches les plus récentes sont automatiquement placées dans la file d’attente.

## <a name="adjust-adla-quota-limits-per-account"></a>Ajuster les limites de quota ADLA par compte

1. Ouverture de session toohello [portail Azure](https://portal.azure.com).
2. Choisissez un compte ADLA existant.
3. Cliquez sur **Propriétés**.
4. Ajuster **parallélisme** et **travaux simultanés** toosuit vos besoins.

    ![Volet du portail Azure Data Lake Analytics](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-properties.png)

## <a name="increase-maximum-quota-limits"></a>Augmenter les limites de quota maximales

1. Ouvrez une demande de support dans le Portail Azure.

    ![Volet du portail Azure Data Lake Analytics](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-help-support.png)

    ![Volet du portail Azure Data Lake Analytics](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request.png)
2. Sélectionnez le type de problème hello **Quota**.
3. Sélectionnez votre **Abonnement** (vérifiez qu’il ne s’agit pas d’une version d’essai).
4. Sélectionnez le type de quota **Data Lake Analytics**.

    ![Volet du portail Azure Data Lake Analytics](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-basics.png)

5. Dans le panneau de problème hello, expliquez votre limite de l’augmentation demandée avec **détails** de pourquoi vous devez cette capacité supplémentaire.

    ![Volet du portail Azure Data Lake Analytics](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-details.png)

6. Vérifiez vos informations de contact et créer une demande de prise en charge hello.

Microsoft vérifie votre demande et tente de tooaccommodate dès que possible les besoins de votre entreprise.

## <a name="next-steps"></a>Étapes suivantes

* [Vue d'ensemble de Microsoft Azure Data Lake Analytics](data-lake-analytics-overview.md)
* [Gestion d'Azure Data Lake Analytics à l'aide d'Azure PowerShell](data-lake-analytics-manage-use-powershell.md)
* [Surveiller et résoudre les problèmes des tâches Azure Data Lake Analytics à l’aide du portail Azure](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
