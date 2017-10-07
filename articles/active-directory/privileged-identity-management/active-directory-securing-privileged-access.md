---
title: "aaaSecuring accès privilégié dans Azure AD | Documents Microsoft"
description: "Une rubrique qui explique hello s’approche de sécurisation des accès privilégiés entre Azure, Azure Active Directory et Microsoft Online Services."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: mwahl
ms.assetid: 235a0ce9-1daf-4433-8f65-9c6afcd64d08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: kgremban
ms.custom: pim
ms.openlocfilehash: 694835dc5c41640673dbd996d44b0d1f217220de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-privileged-access-in-azure-ad"></a>Sécurisation de l’accès privilégié dans Azure AD
Sécurisation des privilèges de l’accès est une première étape essentielle toohelp protéger les ressources d’entreprise dans une organisation moderne. Les comptes privilégiés sont ceux qui administrent et gèrent des systèmes informatiques. Pirates informatiques ciblent les données et les systèmes de ces comptes toogain accès tooan l’organisation. toosecure un accès privilégié, vous devez isoler les comptes hello et systèmes hello d’être exposées tooa des utilisateurs malveillants.

Plus les utilisateurs commencent tooget privilégié l’accès via les services de cloud computing. Il peut s’agit d’administrateurs généraux d’Office 365, d’administrateurs d’abonnements Azure et d’utilisateurs qui disposent d’un accès administrateur à des machines virtuelles ou à des applications SaaS.

Microsoft vous recommande de suivre la feuille de route établie dans la rubrique [Sécurisation de l’accès privilégié](https://technet.microsoft.com/library/mt631194.aspx)(en anglais).

Pour les clients utilisant Azure Active Directory, Office 365 ou d’autres services et applications Microsoft, ces principes s’appliquent, que les comptes d’utilisateurs soient gérés et authentifiés par Active Directory ou dans Azure Active Directory. Hello sections suivantes fournissent plus d’informations sur Azure AD toosupport de fonctionnalités sécurisation de l’accès privilégié.

## <a name="azure-multi-factor-authentication"></a>Azure Multi-Factor Authentication
sécurité de hello tooincrease d’authentification d’administrateur, vous devez exiger vérification en deux étapes avant l’octroi de privilèges. Vérification en deux étapes est une méthode de vérification qui vous êtes nécessite l’utilisation de hello de plus qu’un nom d’utilisateur et le mot de passe. Il fournit une deuxième couche de sécurité toouser connexions et transactions.

Azure multi-Factor Authentication (MFA) est la solution de vérification en deux étapes de Microsoft, qui vous aide à protéger les accès toodata et des applications tout en répondant à la demande de l’utilisateur pour un processus de connexion simple. Elle fournit une authentification renforcée via un éventail d’options de vérification simples, dont :

- appels téléphoniques
- messages texte
- notifications d’application mobile
- codes de vérification d’application mobile
- jetons OATH tiers

Pour une vue d’ensemble du fonctionnement de l’authentification multifacteur Azure consultez hello suivant vidéo :

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]

Pour plus d’informations, consultez [MFA pour Office 365 et MFA pour Azure](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/).

## <a name="time-bound-privileges"></a>Privilèges limités dans le temps
Certaines organisations peuvent estimer qu’elles ont trop d’utilisateurs ayant des rôles à privilèges élevés. Un utilisateur a peut-être été ajouté rôle toohello pour une activité spécifique, comme toosign pour un service, mais n’a pas d’utiliser ces privilèges fréquemment par la suite.

durée d’exposition toolower hello de privilèges et visibilité leur utilisation, limite les utilisateurs tooonly est prise sur leurs privilèges « juste à temps » (JIT), lorsqu’ils ont besoin tooperform une tâche. Pour Azure Active Directory et Microsoft Online Services, vous pouvez utiliser [Azure AD Privileged Identity Management (PIM)](http://aka.ms/AzurePIM).

![Tableau de bord PIM][2]

## <a name="attack-detection"></a>Détection des attaques
[Azure Active Directory Identity Protection](../active-directory-identityprotection.md) offre une vue consolidée des événements à risque et des vulnérabilités potentielles qui affectent les identités de votre organisation. Basé sur les événements à risque, Identity Protection calcule un niveau de risque d’utilisateur pour chaque utilisateur, ce qui vous tooconfigure des stratégies en fonction des risques tooautomatically protéger hello identités de votre organisation. Ces stratégies, ainsi que d’autres contrôles d’accès conditionnel fournis par Azure Active Directory et EMS, peuvent automatiquement bloquer hello utilisateur ou des suggestions qui incluent des réinitialisations de mot de passe et la mise en œuvre l’authentification multifacteur.

![Azure AD Identity Protection][3]

## <a name="conditional-access"></a>Accès conditionnel
Avec le contrôle d’accès conditionnel, Azure Active Directory vérifie les conditions spécifiques hello choisie lors de l’authentification d’un utilisateur, avant d’autoriser l’accès tooan application. Lorsque ces conditions sont réunies, hello utilisateur authentifié et autorisé accès toohello application.

![Définition des règles d’accès conditionnel avec l’authentification multifacteur][4]

## <a name="related-articles"></a>Articles connexes
* Activation [d’Azure Multi-Factor Authentication](../../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)
* Activation [d’Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-configure.md)
* Activation [d’Azure AD Identity Protection](../active-directory-identityprotection.md)
* Activation des [contrôles d’accès conditionnel](../active-directory-conditional-access.md)

Pour plus d’informations sur la création d’un plan de sécurité complète, voir hello « responsabilités du client et la feuille de route » section hello [Microsoft Cloud Security pour Enterprise Architects](http://aka.ms/securecustomer) document. Pour plus d’informations sur l’engagement tooassist de services de Microsoft avec une des rubriques suivantes, contactez votre représentant Microsoft ou visitez notre [page des solutions inquiétudes](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx).

<!--Image references-->
[1]: ../media/active-directory-privileged-identity-management-configure/Search_PIM.png
[2]: ../media/active-directory-privileged-identity-management-configure/PIM_Dash.png
[3]: ../media/active-directory-identityprotection/29.png
[4]: ../media/active-directory-conditional-access/conditionalaccess-saas-apps.png
