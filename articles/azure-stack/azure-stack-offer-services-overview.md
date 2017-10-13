---
title: Offre de services dans Azure Stack | Microsoft Docs
description: "En tant qu’opérateur cloud, vous pouvez proposer des services à vos utilisateurs."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: erikje
ms.openlocfilehash: 7a54771d99f2719fcc345496b152a5d3acc02121
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="overview-of-offering-services-in-azure-stack"></a>Vue d’ensemble de l’offre de services dans Azure Stack

*S’applique à : systèmes intégrés Azure Stack et Kit de développement Azure Stack*

[Microsoft Azure Stack](azure-stack-poc.md) est une plateforme cloud hybride qui vous permet de fournir des services à partir de votre centre de données. En tant que fournisseur de services, vous pouvez proposer des services à vos locataires. Au sein d’une entreprise ou d’une agence gouvernementale, vous pouvez proposer des services locaux à vos employés. Vous pouvez proposer entre autres les services suivants :

- Services Paas (Platform as a Service) tels que App Services, Mobile Apps, API Apps, API Functions, SQL, MySQL.

Vous pouvez même combiner des services pour intégrer et créer des solutions complexes pour différents utilisateurs.

Pour fournir ces services à vos utilisateurs, vous devez créer [des plans, des offres et des quotas](azure-stack-plan-offer-quota-overview.md). Vos utilisateurs peuvent ensuite s’abonner à vos offres pour utiliser les services.

## <a name="plan-your-service-offers"></a>Planifier vos offres de service

Quand vous planifiez vos offres, gardez à l’esprit les points suivants :

**Offres d’évaluation** : vous pouvez utiliser des offres d’évaluation pour attirer de nouveaux utilisateurs, qui peuvent ensuite effectuer une mise à niveau pour obtenir des services supplémentaires. Pour créer une offre d’évaluation, créez un petit [plan de base](azure-stack-plan-offer-quota-overview.md#base-plan) avec un plan complémentaire facultatif plus important.

**Planification de la capacité** : peut-être craignez-vous que des utilisateurs s’accaparent de grandes quantités de ressources et encombrent le système pour tous les autres utilisateurs. Pour améliorer les performances, vous pouvez [configurer vos plans avec des quotas](azure-stack-plan-offer-quota-overview.md#plans) afin de limiter l’utilisation.

**Fournisseurs délégués** : vous pouvez accorder à d’autres personnes la capacité à créer des offres dans votre environnement. Par exemple, si vous êtes fournisseur de services, vous pouvez [déléguer](azure-stack-delegated-provider.md) cette capacité à vos revendeurs. Si vous êtes une organisation, vous pouvez déléguer à d’autres divisions/filiales.

## <a name="next-steps"></a>Étapes suivantes
[En savoir plus sur les offres, les plans, les quotas et les abonnements](azure-stack-plan-offer-quota-overview.md)

