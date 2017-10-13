---
title: "Prise en main d’Azure AD v2 avec les applications de serveur web ASP.NET - Configuration | Microsoft Docs"
description: "Implémentation de la connexion Microsoft dans une solution ASP.NET avec une application basée sur un navigateur web traditionnel utilisant le standard OpenID Connect"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 8a1650a65e7980f4a13fa4edc7918b0099bb5464
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
## <a name="configure-your-aspnet-web-app-with-the-applications-registration-information"></a>Configurer votre application Web ASP.NET avec les informations d’inscription de l’application

Dans cette étape, vous allez configurer votre projet pour utiliser SSL, puis vous servir de l’URL SSL pour configurer les informations d’inscription de votre application. Ensuite, ajoutez les informations d’inscription de l’application à votre solution via *web.config*.

1.  Dans l’Explorateur de solutions, sélectionnez le projet et examinez la fenêtre `Properties` (si vous ne voyez pas une fenêtre de propriétés, appuyez sur F4).
2.  Remplacez `SSL Enabled` par `True` :
3.  Copiez la valeur de `SSL URL` ci-dessus et collez-la dans le champ `Redirect URL` en haut de cette page, puis cliquez sur *Mettre à jour* :<br/><br/>![Propriétés du projet](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)<br />
4.  Ajoutez le code suivant dans le fichier `web.config` situé dans le dossier racine, sous la section `configuration\appSettings` :

```xml
<add key="ClientId" value="[Enter the application Id here]" />
<add key="RedirectUri" value="[Enter the Redirect URL here]" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
