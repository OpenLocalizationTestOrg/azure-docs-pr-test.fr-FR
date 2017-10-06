---
title: aaaUsing Azure AD Connect Health avec AD DS | Documents Microsoft
description: Bonjour Azure AD Connect Health page qui explique comment toomonitor les services AD DS.
services: active-directory
documentationcenter: 
author: arluca
manager: femila
editor: curtand
ms.assetid: 19e3cf15-f150-46a3-a10c-2990702cd700
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: e2fb6be65407d02c214dcab385b85d6cb54f48de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-ad-connect-health-with-ad-ds"></a>Utilisation d’Azure AD Connect Health avec AD DS
Hello suivant documentation est toomonitoring spécifique Active Directory Domain Services avec Azure AD Connect Health. Hello pris en charge les versions des services AD DS sont : Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 et Windows Server 2016.

Pour plus d’informations sur la surveillance AD FS avec Azure AD Connect Health, consultez [Utilisation d’Azure AD Connect Health avec AD FS](active-directory-aadconnect-health-adfs.md). En outre, pour plus d’informations sur la surveillance de la synchronisation Azure AD Connect avec Azure AD Connect Health, consultez [Utilisation d’Azure AD Connect Health pour la synchronisation](active-directory-aadconnect-health-sync.md).

![Azure AD Connect Health pour AD DS](./media/active-directory-aadconnect-health/aadconnect-health-adds-entry.png)

## <a name="alerts-for-azure-ad-connect-health-for-ad-ds"></a>Alertes d’Azure AD Connect Health pour AD DS
Hello section d’alertes dans Azure AD Connect Health pour AD DS, vous fournit une liste d’alertes actifs et résolus, les contrôleurs de domaine tooyour connexes. En sélectionnant une alerte active ou résolue ouvre un nouveau panneau avec des informations supplémentaires, ainsi que les étapes de résolution et lie toosupporting documentation. Chaque type d’alerte peut avoir une ou plusieurs instances, qui correspondent tooeach hello des contrôleurs de domaine affectés par cette alerte. Bas hello du panneau d’alerte hello, vous pouvez double-cliquer sur une tooopen de contrôleur de domaine affecté une lame supplémentaire avec plus de détails sur cette instance d’alerte.

Dans ce panneau, vous pouvez activer les notifications par courrier électronique pour les alertes et modifier dans la vue de plage de temps hello. Plage de temps hello de développement, vous permet de toosee les alertes résolues préalable.

![Erreur de synchronisation d’Azure AD Connect](./media/active-directory-aadconnect-health/aadconnect-health-adds-alerts.png)

## <a name="domain-controllers-dashboard"></a>Tableau de bord Contrôleurs de domaine
Ce tableau de bord fournit une vue de topologie de votre environnement, ainsi que les mesures opérationnelles essentielles et l’état d’intégrité de chacun de vos contrôleurs de domaine surveillés. les métriques Hello présentée identifier tooquickly, les contrôleurs de domaine qui pourraient nécessiter des investigations. Par défaut, seul un sous-ensemble des colonnes de hello s’affiche. Toutefois, vous trouverez ensemble de hello de colonnes disponibles, en double-cliquant sur la commande de colonnes hello. Sélection des colonnes de hello plus importantes, désactive ce tableau de bord en un seul simple et placer la santé hello tooview de votre environnement AD DS.

![Contrôleurs de domaine](./media/active-directory-aadconnect-health/aadconnect-health-adds-domainsandsites-dashboard.png)

Contrôleurs de domaine peuvent être regroupés par leur domaine respectif ou d’un site, ce qui est utile pour comprendre la topologie de l’environnement hello. Enfin, si vous double-cliquez sur en-tête du panneau hello, tableau de bord hello optimise tooutilize hello disponible à l’écran immobilier. Cette vue plus large est utile lorsque plusieurs colonnes sont affichées.

## <a name="replication-status-dashboard"></a>Tableau de bord État de la réplication
Ce tableau de bord fournit une vue de la topologie de réplication et état de réplication de contrôleurs de domaine analysés hello. état Hello de la dernière tentative de réplication hello est répertorié, ainsi que de la documentation utile pour les erreurs qui se trouve. Vous pouvez double-cliquer sur un contrôleur de domaine avec une erreur, tooopen un nouveau panneau avec des informations telles que : plus de détails sur l’erreur hello, recommandé d’étapes de résolution, ainsi que des liens tootroubleshooting documentation.

![État de la réplication](./media/active-directory-aadconnect-health/aadconnect-health-adds-replication.png)

## <a name="monitoring"></a>Surveillance
Cette fonctionnalité fournit les tendances de graphiques différents des compteurs de performances, qui sont collectées de manière continue à partir de chacun des contrôleurs de domaine hello analysé. Les performances d’un contrôleur de domaine peuvent être facilement comparées avec tous les autres contrôleurs de domaine surveillés de votre forêt. En outre, vous pouvez afficher plusieurs compteurs de performances côte à côte, ce qui est utile lors du dépannage de problèmes dans votre environnement.

![Surveillance](./media/active-directory-aadconnect-health/aadconnect-health-adds-monitoring.png)

Par défaut, nous avons présélectionné quatre compteurs de performance ; Toutefois, vous pouvez inclure d’autres en cliquant sur la commande de filtre hello et en sélectionnant ou en désactivant des compteurs de performances de votre choix. En outre, vous pouvez double-cliquer sur un tooopen de graphique de compteur de performances un nouveau panneau qui inclut des points de données pour chacun des contrôleurs de domaine hello analysé.

## <a name="related-links"></a>Liens connexes
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Installation de l'agent Azure AD Connect Health](active-directory-aadconnect-health-agent-install.md)
* [Opérations Azure AD Connect Health](active-directory-aadconnect-health-operations.md)
* [Utilisation d’Azure AD Connect Health avec AD FS](active-directory-aadconnect-health-adfs.md)
* [Utilisation d'Azure AD Connect Health pour la synchronisation (en Anglais)](active-directory-aadconnect-health-sync.md)
* [Forum Aux Questions (FAQ) Azure AD Connect Health](active-directory-aadconnect-health-faq.md)
* [Historique de publication des versions d’Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)

