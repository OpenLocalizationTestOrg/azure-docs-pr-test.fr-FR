---
title: "aaaAzure référence technique d’Active Directory Access conditionnel | Documents Microsoft"
description: "Avec le contrôle d’accès conditionnel, Azure Active Directory vérifie les conditions spécifiques hello que vous choisissez lors de l’authentification utilisateur de hello et avant d’autoriser l’accès toohello application. Lorsque ces conditions sont réunies, hello utilisateur authentifié et autorisé accès toohello application."
services: active-directory.
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 56a5bade-7dcc-4dcf-8092-a7d4bf5df3c1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: ee201405d1d17f130607a95bf455b60cd222dd0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-conditional-access-technical-reference"></a>Référence technique d’Azure Active Directory Conditional Access

## <a name="services-enabled-with-conditional-access"></a>Services activés avec accès conditionnel

Les règles d’accès conditionnel sont prises en charge sur différents types d’application Azure AD. Cette liste comprend les éléments suivants :


* Applications inscrites avec hello Proxy d’Application Azure
* Application distante Azure
* Applications métiers et mutualisées développées inscrites auprès d’Azure AD
* Dynamics CRM
* Applications fédérées à partir de la galerie d’applications Azure AD hello
* Microsoft Office 365 Yammer
* Microsoft Office 365 Exchange Online
* Microsoft Office 365 SharePoint Online (y compris OneDrive Entreprise)
* Microsoft Power BI 
* Applications de l’authentification unique de mot de passe à partir de la galerie d’applications hello Azure AD
* Visual Studio Team Services
* Microsoft Teams









## <a name="enable-access-rules"></a>Activer les règles d’accès
Chaque règle peut être activée ou désactivée sur la base de l’application. Lorsque les règles sont **ON** ils seront activés et appliquées pour les utilisateurs l’accès à application hello. Lorsqu’ils sont **OFF** ils ne doivent pas être utilisés et seront affecte pas les utilisateurs sur le hello de connexion.

## <a name="applying-rules-toospecific-users"></a>Appliquant les règles des utilisateurs toospecific
Les règles peuvent être toospecific appliqué des jeux d’utilisateurs basés sur le groupe de sécurité en définissant **s’appliquent à**. **Appliquer à** peut être défini trop**tous les utilisateurs** ou **groupes**. Lorsque la valeur trop**tous les utilisateurs** règles que hello s’appliquent utilisateur tooany avec application toohello d’accès. Hello **groupes** option permet de sécurité spécifiques et toobe de groupes de distribution sélectionné, les règles sont appliquées uniquement pour ces groupes.

Lors du déploiement d’une règle, il est courant toofirst appliquer un ensemble limité d’utilisateurs, qui sont membres d’un groupe de pilotage. Une fois que la règle de hello complète peut être appliquée trop**tous les utilisateurs**. Cela entraîne la règle hello toobe appliquée pour tous les utilisateurs de l’organisation de hello.

Sélectionnez des groupes peuvent également être exemptées de stratégie à l’aide de hello **sauf** option. Tous les membres de ces groupes seront exclus et ce, même s’ils apparaissent dans un groupe inclus.

## <a name="at-work-networks"></a>Réseaux Au bureau
Règles d’accès conditionnel qui utilisent un réseau « au travail », s’appuient sur les plages d’adresses IP approuvés qui ont été configurés dans Azure AD, ou l’utilisation de hello « à l’intérieur du réseau d’entreprise » de revendication d’AD FS. Ces règles incluent les éléments suivants :

* Exiger l’authentification multifacteur à l’extérieur de l’entreprise
* Bloquer l’accès quand l’utilisateur n’est pas au bureau

Options pour la spécification des réseaux Au bureau

1. Configurer des plages d’adresses IP approuvées Bonjour [page de configuration de l’authentification multifacteur](../multi-factor-authentication/multi-factor-authentication-whats-next.md). Stratégie d’accès conditionnel utilise les plages hello configuré sur chaque demande et le jeton d’émission tooevaluate les règles d’authentification. 
2. Configurer l’utilisation de hello à l’intérieur de revendication du réseau d’entreprise, cette option peut être utilisée avec les répertoires fédérés, à l’aide d’AD FS. toolearn en savoir plus sur hello à l’intérieur des revendications de réseau d’entreprise, consultez [Tusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).


## <a name="rules-based-on-application-sensitivity"></a>Règles basées sur le critère de diffusion des applications
Les règles sont configurées par application qui permet de toobe de services de valeur élevée hello sécurisé sans impact sur les services d’accès tooother. Règles d’accès conditionnel peuvent être configurés sur hello **configurer** onglet de l’application hello. 

Règles actuellement proposées :

* **Imposer l’authentification multifacteur**
  
  * Tous les utilisateurs que cette stratégie est appliquée toowill être tooauthenticate requis via l’authentification multifacteur au moins une fois.
* **Exiger l’authentification multifacteur à l’extérieur de l’entreprise**
  
  * Si cette stratégie est appliquée, tous les utilisateurs seront requis toohave effectuée l’authentification multifacteur au moins une fois si elles accéder au service de hello à partir d’un emplacement distant non liés au travail. S’ils se déplacent à partir d’un emplacement de tooremote de travail, elles seront tooperform obligatoire l’authentification multifacteur lors de l’accès au service de hello.
* **Bloquer l’accès quand l’utilisateur n’est pas au bureau** 
  
  * Lorsque des utilisateurs changent d’emplacement de travail tooa distant, ils ne peuvent pas si hello « Bloquer l’accès à l’extérieur de travail » la stratégie est appliquée toothem.  Ils seront de nouveau autorisés à y accéder lorsqu’ils se trouvent au bureau.

## <a name="related-topics"></a>Rubriques connexes
* [Sécurisation de l’accès tooOffice 365 et d’autres applications connectées tooAzure Active Directory](active-directory-conditional-access.md)
* [Index d’articles pour la gestion des applications dans Azure Active Directory](active-directory-apps-index.md)

