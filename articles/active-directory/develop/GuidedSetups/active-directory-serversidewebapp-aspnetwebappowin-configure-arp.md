---
title: aaaAzure AD v2 ASP.NET Web Server mise en route - Config | Documents Microsoft
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
ms.openlocfilehash: badc47e131290a56a507592f944a0fc7093260a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
## <a name="configure-your-aspnet-web-app-with-hello-applications-registration-information"></a>Configurer votre application de Web ASP.NET avec les informations d’inscription de l’application hello

Dans cette étape, vous configurerez votre toouse projet SSL et ensuite utiliser hello URL SSL tooconfigure des informations d’inscription de votre application. Après cela, ajoutez l’application hello' solution tooyour des informations d’inscription via *web.config*.

1.  Dans l’Explorateur de solutions, sélectionnez le projet de hello et examinez hello `Properties` fenêtre (si vous ne voyez pas une fenêtre de propriétés, appuyez sur F4)
2.  Modification `SSL Enabled` trop`True`
3.  Copier la valeur hello à partir de `SSL URL` ci-dessus et collez-le dans hello `Redirect URL` champ haut hello de cette page, puis cliquez sur *mise à jour*:<br/><br/>![Propriétés du projet](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)<br />
4.  Ajoutez hello qui suit dans `web.config` fichier situé dans le dossier racine, sous la section `configuration\appSettings`:

```xml
<add key="ClientId" value="[Enter hello application Id here]" />
<add key="RedirectUri" value="[Enter hello Redirect URL here]" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
