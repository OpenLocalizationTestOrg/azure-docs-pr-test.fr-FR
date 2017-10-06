---
title: "Création de rapports Azure Active Directory : Prise en main | Microsoft Docs"
description: "Listes hello différents rapports disponibles dans le rapport d’Azure Active Directory"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 7ac99919-8df5-4424-9298-fc7c025ba949
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: f47875708398391dd7f3efdc56a741fdba273b76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-active-directory-reporting"></a>Prise en main de la création de rapports Azure Active Directory
## <a name="what-it-is"></a>Présentation
Azure Active Directory (Azure AD) comprend des rapports sur la sécurité, les activités et l’audit concernant votre annuaire. Voici une liste des rapports hello inclus :

### <a name="security-reports"></a>Rapports de sécurité
* Connexions à partir de sources inconnues
* Connexions après plusieurs échecs
* Connexions depuis plusieurs zones géographiques
* Connexions depuis des adresses IP avec des activités suspectes
* Activité de connexion anormale
* Connexions à partir d’appareils potentiellement infectés
* Utilisateurs ayant une activité de connexion anormale

### <a name="activity-reports"></a>Rapports d’activité
* Utilisation des applications : résumé
* Utilisation des applications : présentation détaillée
* Tableau de bord de l’application
* Erreurs de configuration de compte
* Appareils des utilisateur individuels
* Activité des utilisateurs individuels
* Rapport d'activité de groupes
* Rapport d’activité de l’enregistrement de la réinitialisation de mot de passe
* Activité de réinitialisation de mot de passe

### <a name="audit-reports"></a>Rapport d’audit
* Rapport d’audit d’annuaire

> [!TIP]
> Pour plus d’informations sur la création de rapports Azure AD, consultez la page [Affichage de vos rapports d’accès et d’utilisation](active-directory-view-access-usage-reports.md).
> 
> 

## <a name="how-it-works"></a>Fonctionnement
### <a name="reporting-pipeline"></a>Pipeline de création de rapports
pipeline de création de rapports Hello se compose de trois étapes principales. Chaque fois qu’un utilisateur se connecte, ou une authentification est effectuée, suivant de hello se produit :

* Tout d’abord, hello utilisateur authentifié (avec ou sans succès) et hello est stocké dans les bases de données de service hello Azure Active Directory.
* À intervalles réguliers, toutes les connexions récentes sont traitées. À ce stade, nos algorithmes de sécurité et de surveillance des activités anormales recherchent toute activité suspecte dans les connexions récentes.
* Après traitement, les rapports de hello sont écrites, mis en cache et pris en charge dans hello portail Azure classic.

### <a name="report-generation-times"></a>Durée de génération des rapports
En raison du volume important de toohello d’authentifications et signe que connexions traitées par hello plateforme d’Azure AD, hello plus récent connexions traitées sont, en moyenne, datant d’une heure. Dans de rares cas, il peut falloir too8 heures tooprocess hello plus récente de connexions.

Vous trouverez connectez-vous hello plus récente traitée en examinant le texte d’aide hello haut hello de chaque rapport.

![Texte d’aide en haut de hello de chaque rapport](./media/active-directory-reporting-getting-started/reportingWatermark.PNG)

> [!TIP]
> Pour plus d’informations sur la création de rapports Azure AD, consultez la page [Affichage de vos rapports d’accès et d’utilisation](active-directory-view-access-usage-reports.md).
> 
> 

## <a name="getting-started"></a>Prise en main
### <a name="sign-into-hello-azure-classic-portal"></a>Se connecter à hello de portail Azure classic
Tout d’abord, vous devez toosign dans hello [portail Azure classic](https://manage.windowsazure.com) en tant qu’un administrateur global ou de conformité. Vous doit également être un administrateur de service d’abonnement Azure ou un coadministrateur ou être à l’aide de hello « accès tooAzure AD » abonnement Azure.

### <a name="navigate-tooreports"></a>Accédez tooReports
tooview rapports, accédez à onglet Rapports de toohello haut hello de votre annuaire.

S’il s’agit d’affichage des rapports de hello pour la première fois, vous devez boîte de dialogue tooagree tooa avant de pouvoir afficher les rapports hello. Il s’agit de tooensure qu’il est acceptable pour les administrateurs de votre organisation de tooview ces données, qui peuvent être considérées comme des informations personnelles dans certains pays.

![Boîte de dialogue](./media/active-directory-reporting-getting-started/dialogBox.png)

### <a name="explore-each-report"></a>Explorer chaque rapport
Naviguer dans chaque rapport toosee hello de données collectées et hello-connexions traitées. Vous trouverez une [liste de tous les rapports hello ici](active-directory-reporting-guide.md).

![Tous les rapports](./media/active-directory-reporting-getting-started/reportsMain.png)

### <a name="download-hello-reports-as-csv"></a>Télécharger des rapports de hello en tant que volume partagé de cluster
Chaque rapport peut être téléchargé dans un fichier CSV (valeurs séparées par des virgules). Vous pouvez utiliser ces fichiers dans Excel, Power BI ou analyse tiers programmes toofurther analyser vos données.

toodownload un rapport en tant que volume partagé de cluster, accédez toohello rapport et cliquez sur « Télécharger » en bas de hello.

![Bouton de téléchargement](./media/active-directory-reporting-getting-started/downloadButton.png)

> [!TIP]
> Pour plus d’informations sur la création de rapports Azure AD, consultez la page [Affichage de vos rapports d’accès et d’utilisation](active-directory-view-access-usage-reports.md).
> 
> 

## <a name="next-steps"></a>Étapes suivantes
### <a name="customize-alerts-for-anomalous-sign-in-activity"></a>Personnalisation des alertes d’activité anormale dans les connexions
Accédez à onglet de « Configurer » toohello de votre répertoire.

Faire défiler vers la section de « Notifications » toohello.

Activer ou désactiver la section de « Notifications par courrier électronique de connexions anormales » hello.

![Hello section Notifications](./media/active-directory-reporting-getting-started/notificationsSection.png)

### <a name="integrate-with-hello-azure-ad-reporting-api"></a>Hello intégrer des API de création de rapports AD Azure
Consultez [prise en main de hello API Reporting](active-directory-reporting-api-getting-started.md).

### <a name="engage-multi-factor-authentication-on-users"></a>Application de l’authentification multifacteur aux utilisateurs
Sélectionnez un utilisateur dans un rapport.

Cliquez sur hello « Activer l’authentification Multifacteur » en bas de hello d’écran hello.

![bouton de l’authentification multifacteur Hello bas hello écran hello](./media/active-directory-reporting-getting-started/mfaButton.png)

> [!TIP]
> Pour plus d’informations sur la création de rapports Azure AD, consultez la page [Affichage de vos rapports d’accès et d’utilisation](active-directory-view-access-usage-reports.md).
> 
> 

## <a name="learn-more"></a>En savoir plus
### <a name="audit-events"></a>Événements d'audit
Obtenir des informations sur les événements sont auditées dans répertoire hello dans [Azure Active Directory Reporting événements d’Audit](active-directory-reporting-audit-events.md).

### <a name="api-integration"></a>Intégration de l’API
Consultez [prise en main de hello API Reporting](active-directory-reporting-api-getting-started.md) et hello [documentation de référence API](https://msdn.microsoft.com/library/azure/mt126081.aspx).

### <a name="get-in-touch"></a>Prendre contact
Envoyez un message à [aadreportinghelp@microsoft.com](mailto:aadreportinghelp@microsoft.com) pour faire part de vos commentaires, obtenir de l’aide ou poser une question.

> [!TIP]
> Pour plus d’informations sur la création de rapports Azure AD, consultez la page [Affichage de vos rapports d’accès et d’utilisation](active-directory-view-access-usage-reports.md).
> 
> 

