---
title: "aaaAzure Active Directory un accès conditionnel FAQ | Documents Microsoft"
description: "Obtenir elles sonttrop des réponses aux questions sur l’accès conditionnel dans Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 14f7fc83-f4bb-41bf-b6f1-a9bb97717c34
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: d23acbb01217d7e9717d1a43de1b46a929404118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-conditional-access-faqs"></a>Forum aux questions sur l’accès conditionnel Azure Active Directory

## <a name="which-applications-work-with-conditional-access-policies"></a>A quelles applications les stratégies d’accès conditionnel s’appliquent-elles ?

Pour plus d’informations sur les applications qui fonctionnent avec les stratégies d’accès conditionnel, consultez [Applications et navigateurs qui utilisent des règles d’accès conditionnel dans Azure Active Directory](active-directory-conditional-access-supported-apps.md).

## <a name="are-conditional-access-policies-enforced-for-b2b-collaboration-and-guest-users"></a>Les stratégies d’accès conditionnel s’appliquent-elles à la collaboration B2B et aux utilisateurs invités ?

Les stratégies sont appliquées aux utilisateurs dans le cadre d’une collaboration business-to-business (B2B). Toutefois, dans certains cas, un utilisateur ne peut pas être exigences hello toosatisfy en mesure de la stratégie. Par exemple, il est possible que l’organisation d’un utilisateur invité ne prenne pas en charge l’authentification multifacteur. 



## <a name="does-a-sharepoint-online-policy-also-apply-tooonedrive-for-business"></a>Une stratégie SharePoint Online également applique-t-elle tooOneDrive for Business ?

Oui. Une stratégie SharePoint Online s’applique également tooOneDrive for Business.


## <a name="why-cant-i-set-a-policy-on-client-apps-like-word-or-outlook"></a>Pourquoi ne puis-je pas définir une stratégie pour les applications clientes telles que Word ou Outlook ?

Une stratégie d’accès conditionnel définit les conditions requises pour accéder à un service. Elle est appliquée lorsque le service d’authentification toothat se produit. stratégie de Hello n’est pas définie directement sur une application cliente. Au lieu de cela, elle est appliquée quand un client appelle un service. Par exemple, une stratégie définie sur SharePoint applique tooclients appel de SharePoint. Une stratégie définie sur Exchange applique tooOutlook.

## <a name="does-a-conditional-access-policy-apply-tooservice-accounts"></a>Une stratégie d’accès conditionnel s’applique tooservice comptes ?

Stratégies d’accès conditionnel s’appliquent à des comptes d’utilisateur tooall. Cela inclut les comptes d’utilisateur utilisés comme comptes de service. Souvent, un compte de service qui s’exécute sans assistance ne peut pas satisfaire les exigences de hello d’une stratégie d’accès conditionnel. Par exemple, l’authentification multifacteur peut être obligatoire. Les comptes de service peuvent être exclus d’une stratégie à l’aide des paramètres de gestion de stratégie d’accès conditionnel. 

## <a name="are-graph-apis-available-for-configuring-conditional-access-policies"></a>Des API graphiques sont-elles disponibles pour la configuration des stratégies d’accès conditionnel ?

Actuellement, non. 

## <a name="what-is-hello-default-exclusion-policy-for-unsupported-device-platforms"></a>Qu’est la stratégie d’exclusion par défaut hello pour les plateformes d’appareils non pris en charge ?

À l’heure actuelle, les stratégies d’accès conditionnel sont appliquées de manière sélective aux utilisateurs d’appareils iOS et Android. Les applications sur d’autres plateformes d’appareils sont, par défaut, pas affectées par la stratégie d’accès conditionnel hello pour les appareils iOS et Android. Un administrateur client peut choisir toooverride hello stratégie globale toodisallow accès toousers sur les plateformes qui ne sont pas pris en charge.


## <a name="how-do-conditional-access-policies-work-for-microsoft-teams"></a>Comment les stratégies d’accès conditionnel fonctionnent-elles pour Microsoft Teams ?  

Microsoft Teams s’appuie fortement sur Exchange Online et SharePoint Online pour les principaux scénarios de productivité, tels que les réunions, les calendriers et le partage de fichiers. Stratégies d’accès conditionnel qui sont définies pour ces applications cloud s’appliquent tooMicrosoft équipes lorsqu’un utilisateur se connecte.

Microsoft Teams est également pris en charge séparément en tant qu’application cloud dans les stratégies d’accès conditionnel Azure Active Directory. Stratégies d’autorité de certificat sont définies pour une application cloud s’appliquent tooMicrosoft équipes lorsqu’un utilisateur se connecte.

Les clients de bureau Microsoft Teams pour Windows et Mac prennent en charge l’authentification moderne. L’authentification moderne permet connectez-vous basé sur les applications clientes Office hello Azure Active Directory Authentication Library (ADAL) tooMicrosoft sur plusieurs plateformes. 
