---
title: "détection de l’audit et de la menace aaaEnable sur les serveurs SQL Server dans le centre de sécurité Azure | Documents Microsoft"
description: "Ce document vous montre comment tooimplement hello recommandation du centre de sécurité Azure ** activer l’audit et menace pour la détection sur les serveurs SQL **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 042fca4d-7dab-4172-8614-e8c21ccb4960
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: terrylan
ms.openlocfilehash: b082c48cdbc386f14e677f4e13a7f306f37fd0e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-servers-in-azure-security-center"></a>Activer l’audit et la détection des menaces sur les serveurs SQL dans Azure Security Center
Azure Security Center vous recommande d’activer l’audit et la détection des menaces pour toutes les bases de données sur vos serveurs SQL Azure si l’audit n’est pas déjà activé. L’audit et la détection des menaces peuvent vous aider à respecter une conformité réglementaire, à comprendre l’activité de la base de données et à découvrir des discordances et des anomalies susceptibles d’indiquer des problèmes pour l’entreprise ou des violations de la sécurité.

Une fois que vous avez activé l’audit, vous pouvez configurer la détection des menaces paramètres et des messages électroniques tooreceive sécurité les alertes. La détection des menaces détecte des activités de base de données anormales indiquant de base de données des toohello des menaces de sécurité potentielles. Cela vous permet de toodetect et répond toopotential menaces qu’ils se produisent.

Cette recommandation s’applique toohello service SQL Azure uniquement. Il n’inclut pas SQL Server en cours d’exécution sur vos ordinateurs virtuels dans les Services d’Infrastructure Azure (IaaS Azure).

> [!NOTE]
> Ce document présente le service de hello à l’aide d’un exemple de déploiement.  Il ne s’agit pas d’un guide pas à pas.
>
>

## <a name="implement-hello-recommendation"></a>Implémenter la recommandation de hello
1. Bonjour **recommandations** panneau, sélectionnez **activer l’audit et menace pour la détection sur les serveurs SQL**.  Cette opération ouvre hello **activer l’audit et menace pour la détection sur les serveurs SQL** panneau.

   ![Activer l’audit sur les serveurs SQL][1]
2. Sélectionnez une détection d’audit et de la menace des tooenable du serveur SQL. Cette opération ouvre hello **audit et la détection des menaces** panneau.

3. Sur hello **audit et la détection des menaces** panneau, sélectionnez **ON** sous **audit**.

   ![Activer l’audit des paramètres][2]
4. Suivez les étapes de hello dans [l’audit de base de données SQL dans hello portail Azure](../sql-database/sql-database-auditing-portal.md) stockage tooconfigure où vos journaux d’audit sera stocké. Hello compte de stockage de l’abonnement pour la collecte de données est compte de stockage par défaut hello.
5. Suivez les étapes de hello dans [prise en main la détection des menaces de base de données SQL](../sql-database/sql-database-threat-detection.md) tooturn sur et configurer la détection des menaces et liste de hello tooconfigure d’adresses de messagerie qui recevront les alertes de sécurité lors de la détection des activités anormales.

## <a name="see-also"></a>Voir aussi
Cet article vous a montré comment tooimplement hello recommandation du centre de sécurité « Activer l’audit et la détection sur les serveurs SQL de la menace ». toolearn savoir plus sur la sécurisation de votre base de données SQL, voir hello :

* [Sécurisation de votre base de données SQL](../sql-database/sql-database-security-overview.md)

toolearn en savoir plus sur le centre de sécurité, voir hello :

* [Définition des stratégies de sécurité dans le centre de sécurité Azure](security-center-policies.md) --Découvrez comment tooconfigure des stratégies de sécurité pour vos abonnements Azure et les groupes de ressources.
* [Gestion des recommandations de sécurité dans Azure Security Center](security-center-recommendations.md) : découvrez comment les recommandations peuvent vous aider à protéger vos ressources Azure.
* [Contrôle d’intégrité de la sécurité dans le centre de sécurité Azure](security-center-monitoring.md) --Découvrez comment toomonitor hello d’intégrité de vos ressources Azure.
* [Toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md) --Découvrez comment les alertes toosecurity toomanage et y répondre.
* [Surveillance des solutions de partenaire avec Azure Security Center](security-center-partner-solutions.md) --Découvrez comment toomonitor hello état d’intégrité de vos solutions de partenaire.
* [Forum aux questions sur Azure Security Center](security-center-faq.md) --rechercher Forum aux questions sur l’utilisation du service de hello.
* [Blog de sécurité Azure](http://blogs.msdn.com/b/azuresecurity/) --obtenir les dernières informations de sécurité Azure hello et informations.

<!--Image references-->
[1]: ./media/security-center-enable-auditing-on-sql-server/enable-auditing-on-sql-servers.png
[2]: ./media/security-center-enable-auditing-on-sql-server/auditing-settings-blade.png
