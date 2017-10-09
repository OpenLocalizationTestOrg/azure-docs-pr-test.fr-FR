---
title: "aaaProtecting SQL Azure services et données dans le centre de sécurité Azure | Documents Microsoft"
description: "Ce document traite des recommandations d’Azure Security Center qui peuvent vous aider à protéger vos données et le service SQL Azure et à rester en conformité avec les stratégies de sécurité."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: bcae6987-05d0-4208-bca8-6a6ce7c9a1e3
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/03/2017
ms.author: terrylan
ms.openlocfilehash: 75d782d3c2418f9645139e4cd6ecb7765c488f91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-azure-sql-service-and-data-in-azure-security-center"></a>Protection des données et du service SQL Azure dans Azure Security Center
Centre de sécurité Azure analyse l’état de la sécurité de vos ressources Azure hello. Lorsque le centre de sécurité identifie les éventuelles failles de sécurité, il crée des recommandations qui vous guident tout au long des processus de hello de configuration de contrôles de hello nécessité.  Recommandations s’appliquent à des types de ressources tooAzure : machines virtuelles (VM), mise en réseau, SQL et les applications et les données.

Cet article traite des recommandations qui s’appliquent tooAzure SQL services et des données. Les recommandations se concentrent autour de l’audit des bases de données et des serveurs SQL Azure, de l’activation du chiffrement pour les bases de données SQL et de l’activation du chiffrement pour votre compte de stockage Azure.  Tableau hello ci-dessous comme un toohelp de référence que vous comprenez hello disponible SQL service recommandations et les données et ce que fait chacun d’eux si vous l’appliquez.

## <a name="available-sql-service-and-data-recommendations"></a>Recommandations disponibles pour les données et le service SQL
| Recommandation | Description |
| --- | --- |
| [Activer l’audit et la détection des menaces dans les serveurs SQL](security-center-enable-auditing-on-sql-servers.md) |Recommande l’activation de l’audit et de la détection des menaces pour les serveurs SQL Azure (service Azure SQL uniquement ; ne comprend pas les serveurs SQL exécutés sur des machines virtuelles). |
| [Activer l’audit et la détection des menaces dans les bases de données SQL](security-center-enable-auditing-on-sql-databases.md) |Recommande l’activation de l’audit et de la détection des menaces pour les bases de données SQL Azure (service Azure SQL uniquement ; ne comprend pas les serveurs SQL exécutés sur des machines virtuelles). |
| [Activer le chiffrement transparent des données des bases de données SQL](security-center-enable-transparent-data-encryption.md) |Recommande l’activation du chiffrement pour les bases de données SQL (service Azure SQL uniquement). |

## <a name="see-also"></a>Voir aussi
toolearn en savoir plus sur les recommandations qui s’appliquent les types de ressources Azure tooother, voir hello :

* [Protection de vos machines virtuelles dans Azure Security Center](security-center-virtual-machine-recommendations.md)
* [Protection de vos applications dans Azure Security Center](security-center-application-recommendations.md)
* [Protection de votre réseau dans Azure Security Center](security-center-network-recommendations.md)

toolearn en savoir plus sur le centre de sécurité, voir hello :

* [Définition des stratégies de sécurité dans le centre de sécurité Azure](security-center-policies.md) --Découvrez comment tooconfigure des stratégies de sécurité pour vos abonnements Azure et les groupes de ressources.
* [Toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md) --Découvrez comment les alertes toosecurity toomanage et y répondre.
* [Forum aux questions sur Azure Security Center](security-center-faq.md) --rechercher Forum aux questions sur l’utilisation du service de hello.
