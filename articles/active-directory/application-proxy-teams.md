---
title: "aaaAccess applications du Proxy d’application Azure AD dans des équipes | Documents Microsoft"
description: "Utiliser le Proxy d’Application Azure AD tooaccess votre application sur site via Microsoft Teams."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 13c36e43ae6349df09272e308ad4f40451cbbeb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="access-your-on-premises-applications-through-microsoft-teams"></a>Accéder aux applications locales via Microsoft Teams

Azure Proxy d’Application Active Directory vous donne un seul signe-tooon applications locales où que vous soyez et Teams Microsoft rationalise vos efforts de collaboration en un seul emplacement. Intégration hello deux ensemble signifie que vos utilisateurs peuvent être productifs avec leurs coéquipiers dans tous les cas. 

Vos utilisateurs peuvent ajouter des canaux d’équipes cloud applications tootheir [à l’aide des onglets](https://support.office.com/article/Video-Using-Tabs-7350a03e-017a-4a00-a6ae-1c9fe8c497b3?ui=en-US&rs=en-US&ad=US), mais que se passe-t-il si ce site SharePoint ou l’outil de planification elles utilisent toutes est hébergée sur site ? Proxy d’application est la solution de hello. Ils peuvent ajouter des applications publiées via le Proxy d’Application tootheir à l’aide de canaux hello mêmes URL externes, ils utilisent toujours tooaccess leurs applications à distance. Et, étant donné que le Proxy d’Application s’authentifie via Azure Active Directory, hello même seule expérience d’authentification s’effectue.


## <a name="install-hello-application-proxy-connector-and-publish-your-app"></a>Installer le connecteur de Proxy d’Application hello et publier votre application

Si vous n’avez pas déjà fait, [configurer le Proxy d’Application pour votre client et installer le connecteur de hello](active-directory-application-proxy-enable.md). Ensuite, [publiez votre application locale](application-proxy-publish-azure-portal.md) pour l’accès à distance. Lorsque vous publiez une application hello, notez les URL externe hello, car vos utilisateurs finaux ont besoin de ces informations lorsqu’elles ajoutent hello application tooTeams.

Si vous avez déjà vos aurez publiées mais que vous ne connaissez pas leurs URL externes, recherchez-les dans hello [portail Azure](https://portal.azure.com). Connectez-vous, puis accédez trop**Azure Active Directory** > **des applications d’entreprise** > **toutes les applications** > sélectionner votre application > **Le proxy d’application**.

## <a name="add-your-app-tooteams"></a>Ajouter votre tooTeams d’application

Une fois que vous publiez application hello via le Proxy d’Application, informez vos utilisateurs que vous pouvez l’ajouter en tant qu’un onglet directement dans leurs canaux équipes. Demandez-leur d’effectuer les trois étapes suivantes :

1. Accédez toohello équipes de canal où vous souhaitez tooadd cette application et sélectionnent  **+**  tooadd un onglet.

   ![Sélectionner Ajouter un onglet](./media/application-proxy-teams/add-tab.png)

2. Sélectionnez **site Web** à partir des options de l’onglet hello.

   ![Ajouter un site web](./media/application-proxy-teams/website.png)

3. Donnez un nom à onglet de hello et définir l’URL externe du Proxy d’Application toohello URL hello. 

   ![Configurer le nom et l’URL de l’onglet](./media/application-proxy-teams/tab-name-url.png)

Une fois qu’un membre de l’équipe ajoute un onglet de hello, il s’affiche pour tout le monde dans le canal de hello. Tous les utilisateurs qui ont accès toohello application obtiennent l’accès d’authentification unique avec informations d’identification hello qu’ils utilisent pour Teams Microsoft. Tous les utilisateurs qui n’ont pas accès toohello application onglet hello dans des équipes s’affiche, mais sont bloquées jusqu'à ce que vous leur attribuer des autorisations toohello local application hello Azure version publiée portail de l’application hello. 

## <a name="next-steps"></a>Étapes suivantes

- Découvrez comment trop[publier des sites SharePoint locaux](application-proxy-enable-remote-access-sharepoint.md) avec le Proxy d’Application.
- Configurer votre toouse applications [des domaines personnalisés](active-directory-application-proxy-custom-domains.md) pour leur URL externe. 
