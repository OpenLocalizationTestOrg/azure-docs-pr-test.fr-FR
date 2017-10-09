---
title: aaaAuthentication et les autorisations utilisateur dans Azure Analysis Services | Documents Microsoft
description: "En savoir plus sur l’authentification et les autorisations utilisateur dans Azure Analysis Services."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: dd49fd59eec1f68dfe8a0fe373fa612ac46de4e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-user-permissions"></a>Authentification et autorisations utilisateur
Azure Analysis Services utilise Azure Active Directory (Azure AD) pour l’authentification utilisateur et de gestion d’identités. Tout utilisateur qui crée, la gestion ou de connexion tooan Azure Analysis Services server doit avoir une identité d’utilisateur valide un [locataire Azure AD](../active-directory/active-directory-administer.md) Bonjour même abonnement.

Azure Analysis Services prend en charge [la collaboration Azure AD B2B](../active-directory/active-directory-b2b-what-is-azure-ad-b2b.md). Avec B2B, les utilisateurs extérieurs à une organisation peuvent être invités en tant qu’utilisateurs invités dans un répertoire Azure AD. Les invités peuvent être issus d’un autre répertoire client Azure AD ou n’importe quelle adresse e-mail valide. Une fois invité et utilisateur de hello accepte hello invitation envoyée par courrier électronique à partir d’Azure, hello identité de l’utilisateur est ajoutée à l’annuaire toohello locataire. Ces identités peuvent ensuite être ajoutées à des groupes de toosecurity ou en tant que membres d’un rôle de base de données ou administrateur de serveur.

![Architecture de l’authentification Azure Analysis Services](./media/analysis-services-manage-users/aas-manage-users-arch.png)

## <a name="authentication"></a>Authentification
Tous les outils et les applications clientes utilisent une ou plusieurs des hello Analysis Services [les bibliothèques clientes](analysis-services-data-providers.md) (AMO, MSOLAP, ADOMD) tooconnect tooa server. 

Les trois bibliothèques clientes prennent en charge les deux flux interactif d’Azure AD et les méthodes d’authentification non interactive. Hello deux méthodes non interactif, les méthodes de mot de passe Active Directory et l’authentification intégrée Active Directory peuvent être utilisées dans les applications qui utilisent AMOMD et MSOLAP. Ces deux méthodes n’entraînent jamais l’affichage de boîtes de dialogue contextuelles.

Les applications clientes comme Excel et Power BI Desktop, et des outils tels que SSMS et SSDT installent hello dernières versions des bibliothèques hello lors de la mise à jour toohello dernière version. Power BI Desktop, SSMS et SSDT sont mis à jour tous les mois. Excel est [mis à jour avec Office 365](https://support.office.com/en-us/article/When-do-I-get-the-newest-features-in-Office-2016-for-Office-365-da36192c-58b9-4bc9-8d51-bb6eed468516). Mises à jour Office 365 sont moins fréquentes et certaines organisations utilisent le canal de différée hello, mises à jour de signification sont différés des toothree mois.

 Selon l’application cliente de hello ou l’outil que vous utilisez, type hello d’authentification et la façon dont vous vous connectez peut-être différer. Chaque application peut-être prendre en charge des fonctionnalités différentes pour la connexion des services toocloud comme Azure Analysis Services.


### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)
Les serveurs Azure Analysis Services prennent en charge les connexions depuis [SSMS V17.1](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) et versions ultérieures à l’aide de l’authentification Windows, l’authentification du mot de passe Active Directory et l’authentification universelle Active Directory. En général, il est recommandé d'utiliser l’authentification universelle Active Directory, car :

*  Elle prend en charge les méthodes d’authentification interactive et non interactive.

*  Prend en charge les utilisateurs invités de Azure B2B invités dans le locataire d’Azure AS hello. Lors de la connexion tooa serveur, les utilisateurs invités doivent sélectionner l’authentification universelle Active Directory lors de la connexion toohello server.

*  Elle prend en charge authentification multifacteur (MFA). L’authentification Multifacteur Azure permet de toodata d’accès de sauvegarde et les applications avec une gamme d’options de vérification : appel téléphonique, message texte, les cartes à puce avec code confidentiel ou notification d’application mobile. L’authentification multifacteur (MFA) interactive avec Azure AD peut afficher une boîte de dialogue contextuelle de validation.

### <a name="sql-server-data-tools-ssdt"></a>Outils SQL Server Data Tools (SSDT)
SSDT connecte tooAzure Analysis Services à l’aide de l’authentification universelle Active Directory avec prise en charge l’authentification Multifacteur. Les utilisateurs sont demandée toosign dans tooAzure sur le déploiement de première hello à l’aide de leur ID d’organisation (courrier électronique). Les utilisateurs doivent se connecter tooAzure avec un compte disposant d’autorisations d’administrateur de serveur sur le serveur hello que pour qu’ils déploient. Lors de la connexion tooAzure hello première fois, un jeton est attribué. SSDT met en cache hello jeton en mémoire pour futures se reconnecte.

### <a name="power-bi-desktop"></a>Power BI Desktop
Power BI Desktop se connecte tooAzure Analysis Services à l’aide de l’authentification universelle Active Directory avec prise en charge l’authentification Multifacteur. Les utilisateurs sont invités à toosign dans tooAzure sur la première connexion de hello à l’aide de leur ID d’organisation (courrier électronique). Les utilisateurs doivent se connecter tooAzure avec un compte qui est inclus dans un administrateur du serveur ou du rôle de base de données.

### <a name="excel"></a>Excel
Les utilisateurs Excel peuvent se connecter tooa serveur en utilisant un compte Windows, un ID d’organisation (adresse électronique) ou une adresse de messagerie externe. Les identités de messagerie externes doivent exister dans hello Azure AD en tant qu’invité.

## <a name="user-permissions"></a>Autorisations utilisateur

**Les administrateurs de serveur** sont l’instance de serveur spécifique tooan Azure Analysis Services. Ils connectent avec des outils comme le portail Azure, SSMS et SSDT tooperform des tâches comme l’ajout de bases de données et de gestion des rôles d’utilisateur. Par défaut, hello utilisateur qui crée hello serveur est automatiquement ajouté en tant qu’un administrateur de serveur Analysis Services. Les autres administrateurs peuvent être ajoutés à l’aide du portail Azure ou SSMS. Les administrateurs de serveur doivent posséder un compte de locataire Azure AD de hello Bonjour même abonnement. toolearn, voir [gérer les administrateurs de serveur](analysis-services-server-admins.md). 


**Les utilisateurs de base de données** connecter toomodel de bases de données à l’aide d’applications clientes comme Excel ou Power BI. Les utilisateurs doivent être ajoutés toodatabase rôles. Les rôles de bases de données définissent l’administrateur, les processus ou les autorisations de lecture pour une base de données. Il est important de toounderstand les utilisateurs de base de données d’un rôle disposant des autorisations d’administrateur est différent de celui des administrateurs du serveur. Toutefois, par défaut, les administrateurs de serveurs sont également administrateurs de bases de données. toolearn, voir [gérer les utilisateurs et les rôles de base de données](analysis-services-database-users.md).

**Propriétaires de ressources Azure**. Les propriétaires des ressources gèrent les ressources pour un abonnement Azure. Les propriétaires des ressources peuvent ajouter tooOwner d’identités d’utilisateur Azure AD ou contributeur de rôles au sein d’un abonnement à l’aide de **le contrôle d’accès** dans le portail Azure, ou avec les modèles Azure Resource Manager. 

![Contrôle des accès dans le portail Azure](./media/analysis-services-manage-users/aas-manage-users-rbac.png)

Les rôles à ce niveau s’appliquent toousers ou comptes qui ont besoin de tâches tooperform qui peuvent être effectuées dans le portail de hello ou à l’aide de modèles Azure Resource Manager. toolearn, voir [Role-Based Access Control](../active-directory/role-based-access-control-what-is.md). 


## <a name="database-roles"></a>Rôles de bases de données

 Les rôles définis pour un modèle tabulaire sont des rôles de bases de données. Autrement dit, les rôles hello contiennent des membres constitués d’utilisateurs d’Azure AD et les groupes de sécurité qui ont des autorisations spécifiques qui définissent l’action de hello ces membres peuvent effectuer sur une base de données model. Un rôle de base de données est créé en tant qu’objet distinct dans la base de données hello et s’applique uniquement toohello de base de données dans lequel il est créé.   
  
 Par défaut, lorsque vous créez un nouveau projet de modèle tabulaire, projet de modèle hello n’a aucun rôle. Rôles peuvent être définis à l’aide de la boîte de dialogue Gestionnaire de rôles hello dans SSDT. Lorsque les rôles sont définis lors de la conception de projet de modèle, ils sont base de données modèle appliqué toohello uniquement. Lorsque le modèle de hello est déployé, hello même les rôles sont appliqués toohello déployé modèle. Après avoir déployé un modèle, les administrateurs de serveurs et de bases de données peuvent gérer les rôles et les membres à l’aide de SSMS. toolearn, voir [gérer les utilisateurs et les rôles de base de données](analysis-services-database-users.md).
  


## <a name="next-steps"></a>Étapes suivantes

[Gérer les accès tooresources avec les groupes Azure Active Directory](../active-directory/active-directory-manage-groups.md)   
[Gérer les utilisateurs et rôles de bases de données](analysis-services-database-users.md)  
[Gérer les administrateurs de serveurs](analysis-services-server-admins.md)  
[Contrôle d’accès en fonction du rôle](../active-directory/role-based-access-control-what-is.md)  