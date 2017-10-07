---
title: "aaaAzure accès conditionnel pour les applications SaaS | Documents Microsoft"
description: "Accès conditionnel dans Azure AD permet de vous tooconfigure l’authentification multifacteur par application règles d’accès et d’accéder aux tooblock hello pour les utilisateurs non sur un réseau approuvé. "
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 51a1ee61-3ffe-4f65-b8de-ff21903e1e74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 69748014c0c8e266ba66562980c784aba4c68d80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-active-directory-conditional-access"></a>Prise en main de l’accès conditionnel à Azure Active Directory (AD)
Azure Active Directory Conditional Access pour les applications [SaaS](https://azure.microsoft.com/overview/what-is-saas/) et les applications connectées à Azure AD vous invitent à configurer un accès conditionnel en fonction du groupe, de l’emplacement et du critère de diffusion des applications. 

Avec un accès conditionnel basé sur le critère de diffusion des applications, vous pouvez définir des règles d’accès MFA (Multi-Factor Authentication) par application. L’authentification Multifacteur par application permet d’accéder de tooblock de capacité hello pour les utilisateurs qui ne sont pas sur un réseau approuvé. Vous pouvez appliquer l’authentification Multifacteur règles tooall utilisateurs qui sont assignés toohello application, ou uniquement pour les utilisateurs au sein de spécifié les groupes de sécurité.  Les utilisateurs peuvent être exclus d’authentification multifacteur hello si elles accèdent à hello application à partir d’une adresse IP à l’intérieur du réseau de l’organisation hello.

Ces fonctionnalités seront disponibles toocustomers qui ont acheté une licence Azure Active Directory Premium.

## <a name="scenario-prerequisites"></a>Configuration requise pour le scénario
* Une licence Azure Active Directory Premium
* Client Azure Active Directory fédéré ou géré
* Les clients fédérés nécessitent l’activation de l’authentification multifacteur.

## <a name="configure-per-application-access-rules"></a>Configurer des règles d’accès par application
Cette section décrit comment accéder aux tooconfigure par application des règles.

1. Se connecter toohello portail Azure classic à l’aide d’un compte qui est un administrateur global pour Azure AD.
2. Dans le volet gauche de hello, sélectionnez **Active Directory**.
3. Sur l’onglet du répertoire hello, sélectionnez votre annuaire.
4. Sélectionnez hello **Applications** onglet.
5. Application hello sélectionnez hello règle est définie pour.
6. Sélectionnez hello **configurer** onglet.
7. Faites défiler vers le bas la section de règles d’accès toohello. Sélectionnez la règle d’accès souhaité hello.
8. Spécifiez les utilisateurs hello hello règle s’applique à.
9. Activer la stratégie d’hello en sélectionnant **activé toobe sur**.

## <a name="understanding-access-rules"></a>Présentation des règles d’accès
Cette section donne une description détaillée des règles d’accès hello pris en charge dans hello l’accès conditionnel Application Azure.

### <a name="specifying-hello-users-hello-access-rules-apply-to"></a>En spécifiant les utilisateurs de hello hello règles s’appliquent à l’accès
Par défaut, la stratégie de hello s’appliquent tooall les utilisateurs qui ont accès toohello application. Toutefois, vous pouvez également restreindre toousers stratégie hello qui sont membres de hello spécifié les groupes de sécurité. Hello **ajouter un groupe** bouton est tooselect utilisé un ou plusieurs groupes à partir de la boîte de dialogue Sélection de groupe hello hello de règle d’accès seront applique à. Cette boîte de dialogue peut également être utilisé tooremove sélectionné groupes. Lorsque les règles de hello sont tooGroups de tooapply sélectionné, les règles d’accès hello ne seront appliquées que pour les utilisateurs qui appartiennent tooone Hello spécifié les groupes de sécurité.

Groupes de sécurité peuvent également être explicitement exclus de la stratégie de hello en sélectionnant hello **sauf** option et en spécifiant un ou plusieurs groupes. Les utilisateurs qui sont membres d’un groupe dans hello **sauf** liste ne sera pas d’exigence de sujet toohello l’authentification multifacteur, même s’ils sont un membre d’un groupe s’applique cette règle d’accès de hello pour.
règle d’accès Hello ci-dessous nécessite tous les utilisateurs de l’authentification multifacteur toouse hello gestionnaires groupe lors de l’accès d’application hello.

![Définition des règles d’accès conditionnel avec l’authentification multifacteur](./media/active-directory-conditional-access-azuread-connected-apps/conditionalaccess-saas-apps.png)

## <a name="conditional-access-rules-with-mfa"></a>Règles d’accès conditionnel avec l’authentification multifacteur
Si un utilisateur a été configuré à l’aide de la fonctionnalité de l’authentification multifacteur hello par utilisateur, ce paramètre sur l’utilisateur de hello permet de combiner avec des règles de l’authentification multifacteur hello de l’application hello. Cela signifie que d’un utilisateur qui a été configuré pour l’authentification multifacteur par utilisateur seront tooperform obligatoire l’authentification multifacteur, même si elles ont été exemptés de règles d’authentification multifacteur application hello. En savoir plus sur l’authentification multifacteur et sur les paramètres pour chaque utilisateur.

### <a name="access-rule-options"></a>Options de règle d’accès
Hello options suivantes est prises en charge :

* **Exiger l’authentification multifacteur**: hello aux règles d’accès toowhom hello pourront l’authentification multifacteur toocomplete requis avant d’accéder à application hello hello stratégie s’applique à.
* **Exiger une authentification multifacteur en déplacement**: un utilisateur provenant d’une adresse IP approuvée ne sera pas l’authentification multifacteur tooperform requis. Hello approuvés de plages d’adresses IP peuvent être configurés sur la page Paramètres de l’authentification multifacteur hello.
* **Bloquer l’accès quand l’utilisateur n’est pas au travail**: un utilisateur qui ne dispose pas d’une adresse IP approuvée est bloqué. Hello approuvés de plages d’adresses IP peuvent être configurés sur la page Paramètres de l’authentification multifacteur hello.

### <a name="setting-rule-status"></a>Définition de l’état des règles
État de règle d’accès permet l’activation ou désactivation des règles de hello. Hello règles d’accès sont désactivées, exigence de l’authentification multifacteur hello n’est pas appliquée.

### <a name="access-rule-evaluation"></a>Évaluation des règles d’accès
Les règles d'accès sont évaluées lorsqu'un utilisateur accède à une application fédérée qui utilise OAuth 2.0, OpenID Connect, SAML ou WS-Federation. En outre, les règles d’accès sont évaluées lorsque hello OAuth 2.0 et OpenID Connect utilisent un tooacquire de jeton d’actualisation un jeton d’accès. Si l’évaluation de la stratégie échoue lorsqu’un jeton d’actualisation est utilisé, hello erreur **invalid_grant** est renvoyé, cela indique que l’utilisateur hello doit toore-authentifier toohello client.

### <a name="configure-federation-services-tooprovide-multi-factor-authentication"></a>Configurer l’authentification multifacteur de fédération services tooprovide
Pour les clients fédérés, l’authentification Multifacteur peut être effectuée par Azure Active Directory ou par hello serveur AD FS local.

Par défaut, l’authentification multifacteur a lieu sur une page hébergée par Azure Active Directory. tooconfigure l’authentification Multifacteur localement, hello **– SupportsMFA** propriété doit être définie trop**true** dans Azure Active Directory, à l’aide du module de hello Azure AD pour Windows PowerShell.

Hello suivant montre comment tooenable localement l’authentification Multifacteur à l’aide de hello [applet de commande Set-MsolDomainFederationSettings](https://msdn.microsoft.com/library/azure/dn194088.aspx) sur le client de hello contoso.com :

    Set-MsolDomainFederationSettings -DomainName contoso.com -SupportsMFA $true

Dans Ajout toosetting cet indicateur, instance de client fédéré ADFS hello doit être configuré l’authentification multifacteur tooperform. Suivez les instructions de hello pour [déploiement d’Azure multi-Factor Authentication local](../multi-factor-authentication/multi-factor-authentication-get-started-server.md).

## <a name="related-articles"></a>Articles connexes
* [Sécurisation de l’accès tooOffice 365 et d’autres applications connectées tooAzure Active Directory](active-directory-conditional-access.md)
* [Index d’articles pour la gestion des applications dans Azure Active Directory](active-directory-apps-index.md)

