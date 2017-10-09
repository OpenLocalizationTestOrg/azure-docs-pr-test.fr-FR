---
title: "stratégies de périphérique d’accès conditionnel aaaAzure Active Directory pour les services Office 365 | Documents Microsoft"
description: "Découvrez comment toohelp de stratégies de périphérique de l’accès conditionnel tooprovision sécurisation des ressources d’entreprise, tout en conservant tooservices de conformité et d’accès utilisateur."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8664c0bb-bba1-4012-b321-e9c8363080a0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 38229a8d9766efbf0e6b17875b3018011c6b4ea3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="active-directory-conditional-access-device-policies-for-office-365-services"></a>Stratégies d’accès conditionnel d’Active Directory basées sur les appareils pour les services Office 365

Accès conditionnel nécessite plusieurs éléments toowork. Il implique entre autres un utilisateur authentifié avec une authentification multifacteur, un appareil authentifié et un appareil conforme. Dans cet article, nous concentrer principalement sur les conditions basées sur les périphériques que votre organisation peut utiliser toohelp contrôle de services de 365 tooOffice accès. 

Les utilisateurs d’entreprise que les services de tooaccess Office 365 comme Exchange et SharePoint Online à l’entreprise ou école à partir de leurs appareils personnels. Vous souhaitez hello accès toobe sécurisé. Vous pouvez configurer l’accès conditionnel appareil stratégies toohelp Vérifiez ressources d’entreprise plus sécurisés, lors de l’octroi de tooservices d’accès pour les utilisateurs qui utilisent des appareils conformes. Vous pouvez définir tooOffice de stratégies d’accès conditionnel 365 dans le portail d’accès conditionnel Microsoft Intune hello.

Azure Active Directory (Azure AD) applique l’accès conditionnel stratégies toohelp un accès sécurisé tooOffice 365 les services. Vous pouvez créer une stratégie d’accès conditionnel qui empêche un utilisateur utilisant un appareil non conforme d’accéder à un service Office 365. utilisateur de Hello doit respecter les stratégies de périphérique toohello société avant que le service d’accès toohello est accordé. Vous pouvez également créer une stratégie qui impose aux utilisateurs tooenroll leur tooan d’accès aux périphériques toogain service Office 365. Les stratégies peuvent être appliquées tooall des utilisateurs dans une organisation ou limitées tooa quelques groupes de cibles. Vous pouvez ajouter la stratégie tooa de groupes plus cible au fil du temps.

Un composant requis pour l’application de stratégies de périphérique est que les utilisateurs doivent inscrire leurs appareils avec le service d’inscription de périphérique hello Azure AD. Vous pouvez choisir tooturn sur l’authentification multifacteur pour les appareils qui inscrivent avec hello service d’inscription de périphérique Azure AD. L’authentification multifacteur est recommandée pour hello service d’inscription de périphérique Azure Active Directory. Lorsque l’authentification multifacteur est activée, les utilisateurs qui inscrire leurs appareils sur hello service d’inscription de périphérique Azure AD sont invités à accepter une authentification multifacteur.

## <a name="how-does-a-conditional-access-policy-work"></a>Fonctionnement d’une stratégie d’accès conditionnel

Lorsqu’un utilisateur demande l’accès tooan service Office 365 à partir d’une plate-forme de périphérique pris en charge, Azure AD authentifie utilisateur de hello et l’équipement hello. Service Azure AD octroie l’accès toohello uniquement si l’utilisateur de hello est conforme à la stratégie pour le service de hello toohello. Les utilisateurs sur les appareils qui ne sont pas inscrits sont reçoivent des instructions sur la façon de tooenroll et devenir conformes tooaccess d’entreprise aux services Office 365. Les utilisateurs sur des appareils iOS et Android est requis tooenroll leurs appareils à l’aide d’application de portail d’entreprise Intune hello. Lorsqu’un utilisateur inscrit un appareil, appareil de hello est inscrit auprès d’Azure AD et il est inscrit pour la conformité et de gestion des appareils. Vous devez utiliser le service hello Azure Active Directory device registration avec Microsoft Intune pour la gestion des appareils mobiles pour les services Office 365. L’inscription d’appareils est requise pour les utilisateurs tooaccess services Office 365 lors de l’application des stratégies de périphérique.

Quand un utilisateur inscrit avec succès un périphérique, le périphérique de hello devient approuvé. Azure AD donne aux applications de toocompany hello authentifié utilisateur accès avec authentification unique. Azure AD applique un accès conditionnel stratégie toogrant tooa service d’accès non seulement utilisateur hello hello demande l’accès, mais que chaque utilisateur hello renouvelle une demande d’accès. Hello est refusé accès tooservices lorsque les informations d’identification de connexion sont modifiées, appareil de hello est perdu ou volé ou conditions de hello de stratégie de hello ne sont pas remplies au moment de hello de demande de renouvellement.

## <a name="deployment-considerations"></a>Points à prendre en considération pour le déploiement

Vous devez utiliser hello Azure AD d’inscription service tooregister périphériques.

Lorsque les utilisateurs locaux sont sur toobe authentifié, les Services de fédération Active Directory (AD FS) (version 1.0 et versions ultérieures) est requis. L’authentification multifacteur pour l’espace de travail échoue lorsque le fournisseur d’identité hello n’est pas capable de l’authentification multifacteur. Par exemple, vous ne pouvez pas utiliser l’authentification multifacteur avec AD FS 2.0. Vérifiez que hello local AD FS fonctionne avec l’authentification multifacteur et qu’une méthode d’authentification multifacteur valide est en place avant d’activer l’authentification multifacteur pour device registration service hello Azure AD. Par exemple, AD FS sur Windows Server 2012 R2 a des fonctionnalités d’authentification multifacteur. Vous devez également définir une méthode d’authentification valide supplémentaires (authentification multifacteur) sur le serveur de hello AD FS avant d’activer l’authentification multifacteur pour un service d’inscription de périphérique hello Azure AD. Pour plus d’informations sur les méthodes d’authentification multifacteur prises en charge dans AD FS, consultez [Configurer des méthodes d’authentification supplémentaires pour AD FS](/windows-server/identity/ad-fs/operations/configure-additional-authentication-methods-for-ad-fs).

## <a name="next-steps"></a>Étapes suivantes

*   Pour toute question toocommon de réponses, consultez [accès conditionnel Azure Active Directory FAQ](active-directory-conditional-faqs.md).
