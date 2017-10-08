---
title: "Création de rapports Active Directory aaaAzure | Documents Microsoft"
description: "Fournit une vue d’ensemble de la création de rapports Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 6141a333-38db-478a-927e-526f1e7614f4
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: c91813acbdc4b0bfcd164169b0b575accac227d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting"></a>Création de rapports Active Directory

Les rapports Azure Active Directory vous permettent d’obtenir de précieuses informations sur le comportement de votre environnement.  
les données de salutation fournie vous permet de :

- déterminer la façon dont les applications et les services sont utilisés ;
- Détecter les risques affectant la santé hello de votre environnement
- résoudre les problèmes empêchant les utilisateurs d’effectuer leur travail.  

architecture de création de rapports Hello s’appuie sur deux axes principaux :

- Rapports de sécurité
- Rapports d’activité

![Reporting](./media/active-directory-reporting-azure-portal/01.png)



## <a name="security-reports"></a>Rapports de sécurité

rapports de sécurité Hello dans Azure Active Directory aident vous tooprotect identités de votre organisation.  
Il existe deux types de rapports de sécurité dans Azure Active Directory :

- **Les utilisateurs avec indicateur de risque** - de hello [utilisateurs signalées pour le rapport de sécurité risque](active-directory-reporting-security-user-at-risk.md), vous obtenez une vue d’ensemble des comptes d’utilisateur qui a été compromise.

- **Connexions risquées** - avec hello [rapport de sécurité de connexion présente des risques](active-directory-reporting-security-risky-sign-ins.md), vous obtenez un indicateur pour les tentatives de connexion qui ont peut-être été exécutées par une personne est ne Hello pas légitime propriétaire d’un compte d’utilisateur. 

**Licence Azure AD tooaccess un rapport de sécurité avez-vous besoin ?**  
Toutes les éditions d’Azure Active Directory vous indiquent les rapports de sécurité Utilisateurs avec indicateur de risque et Connexions à risque.  
Toutefois, au niveau de granularité d’un rapport du hello varie entre les éditions de hello : 

- Bonjour **éditions Azure Active Directory gratuit et Basic**, vous obtenez déjà une liste d’utilisateurs avec indicateur des risques et de connexions présentant un risque. 

- Hello **Azure Active Directory Premium 1** edition étend ce modèle en vous permettant également tooexamine certains hello sous-jacent des événements à risque qui ont été détectés pour chaque rapport. 

- Hello **Azure Active Directory Premium 2** édition fournit des hello plus des informations détaillées sur hello sous-jacent des événements à risque et il vous permet également de stratégies de sécurité tooconfigure répondent automatiquement tooconfigured niveaux de risque.


## <a name="activity-reports"></a>Rapports d’activité

Il existe deux types de rapports d’activité dans Azure Active Directory :

- **Journaux d’audit** - hello [rapport d’activité des journaux d’audit](active-directory-reporting-activity-audit-logs.md) vous fournit des toohello d’accéder à l’historique de toutes les tâches effectuées dans votre client.

- **Connexions** - avec hello [rapport d’activité des connexions](active-directory-reporting-activity-sign-ins.md), vous pouvez déterminer qui a effectué les tâches hello signalés par le rapport de journaux d’audit hello.



Hello **rapport des journaux d’audit** vous fournit des enregistrements d’activités du système pour la conformité.
Entre autres, hello fourni de données vous permet de tooaddress des scénarios courants tels que :

- Qui fait partie de mon client a obtenu le groupe d’administration tooan accès. Qui lui a fourni cet accès ? 

- Je veux liste de hello tooknow des utilisateurs se connectant à une application spécifique, car je le récemment embarquées hello application et souhaitez tooknow si elle effectue également

- Je veux tooknow combien produisent des réinitialisations de mot de passe dans mon client


**Licence Azure AD rapport de journaux d’audit tooaccess hello avez-vous besoin ?**  
rapport de journaux d’audit Hello est disponible pour les fonctionnalités dont vous disposez des licences. Si vous avez une licence pour une fonctionnalité spécifique, vous avez également accès toohello auditer les informations du journal pour celui-ci.

Pour plus d’informations, consultez **comparaison des fonctionnalités de disposition générale de hello, Basic, versions gratuites et Premium** dans [les fonctionnalités Azure Active Directory](https://www.microsoft.com/cloud-platform/azure-active-directory-features).   



Hello **rapport d’activité des connexions** Active tootoofind répond tooquestions telles que :

- Quel est le modèle hello d’authentification d’un utilisateur ?
- Combien d’utilisateurs se sont connectés au cours d’une semaine ?
- Quel est état hello de ces connexions ?


**Licence Azure AD faire, vous devez tooaccess hello rapport d’activité des connexions ?**  
tooaccess hello rapport d’activité des connexions, votre client doit avoir une licence Azure AD Premium associée.


## <a name="programmatic-access"></a>Accès par programme

Dans l’interface utilisateur toohello Ajout, création de rapports Azure Active Directory offre également [l’accès par programme](active-directory-reporting-api-getting-started-azure-portal.md) toohello les données de rapport. données de Hello de ces rapports peuvent être très utile tooyour applications, telles que les systèmes SIEM, l’audit et les outils Business intelligence. Bonjour Azure AD reporting Qu'api fournit des données de toohello de l’accès par programme via un ensemble d’API REST. Vous pouvez appeler ces API à partir de divers outils et langages de programmation. 


## <a name="next-steps"></a>Étapes suivantes

Si vous souhaitez tooknow plus hello différents types de rapports dans Azure Active Directory, consultez :

- [Rapport des utilisateurs avec indicateur de risque](active-directory-reporting-security-user-at-risk.md)
- [Rapport sur les connexions à risque](active-directory-reporting-security-risky-sign-ins.md)
- [Rapport de journaux d’audit](active-directory-reporting-activity-audit-logs.md)
- [Rapport de journaux de connexions](active-directory-reporting-activity-sign-ins.md)

Si vous souhaitez tooknow plus d’informations sur l’accès à Bonjour Bonjour à l’aide de hello API de création de rapports de données de rapport, consultez : 

- [Prise en main de hello Azure Active Directory API de création de rapports](active-directory-reporting-api-getting-started-azure-portal.md)


<!--Image references-->
[1]: ./media/active-directory-reporting-azure-portal/ic195031.png