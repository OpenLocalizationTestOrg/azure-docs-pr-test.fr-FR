---
title: "aaaAzure service Centre de sécurité et de la base de données SQL Azure | Documents Microsoft"
description: "Cet article explique comment Security Center peut vous aider à sécuriser vos bases de données dans Azure SQL Database."
services: sql-database
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: f109adfd-daed-4257-9692-2042a1399480
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 173590500f0ce64140f214ada24b9692e01dbd4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-and-azure-sql-database-service"></a>Azure Security Center et service SQL Database
[Centre de sécurité Azure](https://azure.microsoft.com/documentation/services/security-center/) vous aide à empêcher, détecter et répondre toothreats. Il fournit une surveillance de la sécurité et une gestion des stratégies intégrées pour l’ensemble de vos abonnements Azure, vous aidant ainsi à détecter les menaces qui pourraient passer inaperçues. De plus, il est compatible avec un vaste écosystème de solutions de sécurité.

Cet article explique comment Security Center peut vous aider à sécuriser vos bases de données dans Azure SQL Database.

## <a name="why-use-security-center"></a>Pourquoi utiliser Security Center ?
Centre de sécurité vous permet de protéger les données dans la base de données SQL en offrant une visibilité sécurité hello de tous vos serveurs et bases de données. Avec Security Center, vous pouvez :

* définir des stratégies pour l’audit et le chiffrement de SQL Database ;
* Surveillance de la sécurité hello des ressources de base de données SQL dans tous vos abonnements.
* identifier et corriger rapidement les problèmes de sécurité ;
* intégrer les alertes de la [détection de menaces Azure SQL Database](../sql-database/sql-database-threat-detection.md).

En outre, toohelping protéger vos ressources de base de données SQL, le centre de sécurité fournit également la surveillance de la sécurité et de gestion pour les machines virtuelles, Services de cloud computing, Services d’application, les réseaux virtuels et bien plus encore. Pour en savoir plus sur Security Center, cliquez [ici](security-center-intro.md).

## <a name="prerequisites"></a>Composants requis
tooget a démarré avec le centre de sécurité, vous devez disposer d’un tooMicrosoft d’abonnement Azure. niveau gratuit de Hello du centre de sécurité est activée dans votre abonnement. Pour plus d’informations sur les niveaux Gratuit et Standard de Security Center, consultez [Tarification de Security Center](https://azure.microsoft.com/pricing/details/security-center/).

Le Centre de sécurité prend en charge l’accès en fonction du rôle. toolearn en savoir plus sur le contrôle d’accès basé sur un rôle (RBAC) dans Azure, consultez [contrôle d’accès basé sur le rôle d’Active Directory Azure](../active-directory/role-based-access-control-configure.md). Hello Forum aux questions du centre de sécurité fournit des informations sur [la gestion des autorisations dans le centre de sécurité](security-center-faq.md#permissions).

## <a name="access-security-center"></a>Accéder au Centre de sécurité
Vous accéder au centre de sécurité à partir de hello [portail Azure](https://azure.microsoft.com/features/azure-portal/). [Connectez-vous au portail de toohello](https://portal.azure.com/) et sélectionnez hello **option de centre de sécurité**.

![Vidéos de Security Center][1]

Hello **centre de sécurité** panneau s’ouvre.
![Panneau Security Center][2]

## <a name="set-security-policy"></a>Définir une stratégie de sécurité
Une stratégie de sécurité définit l’ensemble de hello de contrôles qui sont recommandés pour les ressources hello spécifié abonnement ou groupe de ressources. Dans le centre de sécurité, vous définissez des stratégies pour vos abonnements ou les groupes de ressources en fonction de la société tooyour aux besoins de sécurité et de type hello d’applications ou de la sensibilité des données hello dans chaque abonnement.

Recommandations pour l’audit SQL et le chiffrement transparent des données SQL (TDE), vous pouvez définir une stratégie tooshow.

* Lorsque vous activez **détection des menaces et de l’audit SQL**, centre de sécurité vous recommande que l’audit d’accès tooAzure de base de données activée pour la conformité, avancées de détection et à des fins d’investigation.
* Lorsque vous activez **SQL Transparent Data Encryption**, Security Center recommande l’activation du chiffrement au repos pour votre base de données Azure SQL Database, ainsi que pour les sauvegardes associées et les fichiers journaux de transaction.

tooset une stratégie de sécurité, sélectionnez hello **stratégie** vignette sur le panneau de centre de sécurité hello. Sur hello **stratégie de sécurité** panneau, sélectionnez hello abonnement sur lequel la stratégie de sécurité tooenable hello. Sélectionnez **stratégie de prévention de** et **sur** hello recommandations de sécurité que vous souhaitez toouse pour cet abonnement.
![Stratégie de sécurité][3]

toolearn, voir [définir des stratégies de sécurité](security-center-policies.md).

## <a name="manage-security-recommendation"></a>Gérer les recommandations de sécurité
Centre de sécurité analyse régulièrement l’état de la sécurité de vos ressources Azure hello. Lorsqu’il identifie des failles de sécurité potentielles, il crée des recommandations. recommandations de Hello vous guident tout au long des processus de hello de configuration de contrôles de hello si nécessaire.

Après avoir défini une stratégie de sécurité, le centre de sécurité analyse état de sécurité hello des vulnérabilités potentielles tooidentify ressources. recommandations de Hello sont affichées sous forme de tableau, où chaque ligne représente une recommandation particulière. Utilisez hello tableau suivant comme un toohelp de référence que vous comprenez les recommandations de hello disponibles pour la base de données SQL Azure et quelles chaque recommandation ne si vous l’appliquez. Sélectionner une recommandation ouvre l’article tooan qui explique comment tooimplement hello recommandation dans le centre de sécurité.

| Recommandation | Description |
| --- | --- |
| [Activer l’audit et la détection des menaces sur les serveurs SQL](security-center-enable-auditing-on-sql-servers.md) |Recommande l’activation de l’audit et de la détection des menaces pour les serveurs SQL Database. (Service SQL Database uniquement. N’inclut pas Microsoft SQL Server en cours d’exécution sur vos machines virtuelles.) |
| [Activer l’audit et la détection des menaces sur les bases de données SQL](security-center-enable-auditing-on-sql-databases.md) |Recommande l’activation de l’audit et de la détection des menaces pour les bases de données SQL Database. (Service SQL Database uniquement. N’inclut pas Microsoft SQL Server en cours d’exécution sur vos machines virtuelles.) |
| [Activer Transparent Data Encryption](security-center-enable-transparent-data-encryption.md) |Recommande l’activation du chiffrement pour les bases de données SQL. (Service SQL Database uniquement.) |

recommandations toosee pour vos ressources Azure, sélectionnez hello **recommandations** vignette sur le panneau de centre de sécurité hello. Sur hello **recommandations** panneau, sélectionnez une recommandation toosee les détails. Dans cet exemple, nous allons sélectionner **Activer l’audit et la détection des menaces sur les serveurs SQL**.

![Recommandations][4]

Comme illustré ci-dessous montre le centre de sécurité hello de serveurs SQL Server où l’audit et détection ne sont pas activés. Une fois que vous activez l’audit, vous pouvez configurer les paramètres de détection des menaces et alertes de sécurité de tooreceive des paramètres de messagerie. La détection des menaces vous avertit qu’il détecte des activités de base de données anormales qui indiquent de base de données des toohello des menaces de sécurité potentielles. alertes de Hello sont affichées dans le tableau de bord de centre de sécurité hello.
![Audit et détection des menaces][5]

Suivez les étapes de hello dans [détection des menaces de base de données SQL Bonjour Azure portal](../sql-database/sql-database-threat-detection-portal.md) tooturn sur et configurer la détection des menaces et liste de hello tooconfigure d’adresses de messagerie qui recevront les alertes de sécurité lors de la détection des activités anormales sont.

toolearn en savoir plus sur les recommandations, consultez [gestion des recommandations de sécurité](security-center-recommendations.md).

## <a name="monitor-security-health"></a>Surveiller l’intégrité de la sécurité
Après avoir activé [des stratégies de sécurité](security-center-policies.md) pour les ressources d’un abonnement, le centre de sécurité analysera sécurité hello des vulnérabilités potentielles tooidentify ressources.  Vous pouvez afficher l’état de la sécurité de vos ressources hello Bonjour **contrôle d’intégrité de sécurité** vignette. Lorsque vous cliquez sur **données** Bonjour **contrôle d’intégrité de sécurité** vignette, hello **ressources de données** panneau s’ouvre avec les recommandations de SQL pour des problèmes tels que l’audit et transparent chiffrement des données n’est ne pas activé. Elle contient également des recommandations pour l’état d’intégrité général hello de base de données hello.
![Intégrité de la sécurité des ressources][6]

toolearn, voir [contrôle d’intégrité de la sécurité](security-center-monitoring.md).

## <a name="manage-and-respond-toosecurity-alerts"></a>Gérer et répondre toosecurity alertes
Centre de sécurité collecte, analyse automatiquement et intègre des données de journal de [SQL Azure la détection des menaces](../sql-database/sql-database-threat-detection.md), ainsi que d’autres ressources Azure, les menaces réelles toodetect et réduire les faux positifs. Une liste des alertes de sécurité hiérarchisée est indiquée dans le centre de sécurité, ainsi que de hello informations dont vous avez besoin tooquickly examiner le problème de hello et des recommandations sur la manière tooremediate une attaque.

alertes toosee, sélectionnez hello **alertes de sécurité** vignette sur le panneau de centre de sécurité hello. Sur hello **alertes de sécurité** panneau, sélectionnez une alerte toolearn en savoir plus sur les événements hello ayant déclenché l’alerte de hello et, si elle existe, les étapes doivent tootake tooremediate une attaque. Dans cet exemple, nous allons sélectionner **Injection potentielle de code SQL**.
![Alertes de sécurité][7]

Comme illustré ci-dessous, le centre de sécurité fournit des détails supplémentaires qui offrent un aperçu de quel alerte déclenchée hello, hello la ressource, de cible lorsque hello applicable adresse IP source et des recommandations sur la façon de tooremediate.
![Injection potentielle de code SQL][8]

toolearn, voir [répond et de la gestion des alertes de toosecurity](security-center-managing-and-responding-alerts.md).

## <a name="next-steps"></a>Étapes suivantes
* [Forum aux questions du centre de sécurité](security-center-faq.md) : Forum aux questions sur l’utilisation hello service de recherche.
* [Guide de planification et les opérations du centre de sécurité](security-center-planning-and-operations-guide.md) - suivent un ensemble d’étapes et tâches toooptimize votre utilisation du centre de sécurité basée sur les exigences de sécurité de votre organisation et le modèle de gestion de cloud.
* [Sécurité des données de Security Center](security-center-data-security.md) : découvrez comment Security Center collecte et traite des données sur vos ressources Azure, notamment des informations de configuration, des métadonnées, des journaux des événements, des fichiers de vidage sur incident et plus encore.
* [La gestion des incidents de sécurité](security-center-incident.md) -en savoir plus de la sécurité de hello toouse fonctionnalité disponible dans le centre de sécurité tooassist d’alerte dans la gestion des incidents de sécurité.

<!--Image references-->
[1]: ./media/security-center-sql-database/security-center.png
[2]: ./media/security-center-sql-database/security-center-blade.png
[3]: ./media/security-center-sql-database/security-policy.png
[4]: ./media/security-center-sql-database/recommendation.png
[5]: ./media/security-center-sql-database/turn-on-auditing.png
[6]: ./media/security-center-sql-database/monitor-health.png
[7]: ./media/security-center-sql-database/alert.png
[8]: ./media/security-center-sql-database/sql-injection.png
