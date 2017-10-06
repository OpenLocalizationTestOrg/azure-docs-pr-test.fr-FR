---
title: "aaaAzure AD v2 JS SPA guidée par le programme d’installation - configuration (ARP) | Documents Microsoft"
description: "Comment les applications JavaScript SPA peuvent appeler une API qui nécessite des jetons d’accès à partir d’un point de terminaison Azure Active Directory v2 (ARP)"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: 157f4e342cd684294e24da6ee1fad8a7c2fc266a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
## <a name="add-hello-applications-registration-information-tooyour-app"></a>Ajouter des informations tooyour application de l’application hello d’inscription

Dans cette étape, vous devez les URL de redirection hello tooconfigure de vos informations d’inscription de l’application et ajoutez application de JavaScript SPA tooyour hello Id d’Application.

### <a name="configure-redirect-url"></a>Configurer l’URL de redirection

Configurer hello `Redirect URL` champ ci-dessus avec l’URL de hello pour votre page index.html basée sur votre serveur web, puis cliquez sur *mise à jour*.


> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a>Instructions Visual Studio pour obtenir l’URL de redirection
> tooobtain votre URL de redirection, suivez les instructions hello ci-dessous :
> 1.    Dans *l’Explorateur de solutions*, sélectionnez le projet de hello et examinez hello `Properties` fenêtre (si vous ne voyez pas une fenêtre de propriétés, appuyez sur `F4`)
> 2.    Copier la valeur hello à partir de `URL` toohello Presse-papiers :<br/> ![Propriétés du projet](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)<br />
> 3.    Collez la valeur hello comme un `Redirect URL` sur hello en haut de cette page, puis cliquez sur`Update`

<p/>

> #### <a name="setting-redirect-url-for-python"></a>Configuration d’une URL de redirection pour Python
> Pour Python, vous pouvez définir le port du serveur web hello via la ligne de commande. Cet Assistant d’installation utilise le port 8080 hello pour référence, mais vous êtes libre toouse tout port disponible. Dans tous les cas, suivez les instructions de hello sous tooset une URL de redirection dans les informations d’inscription de l’application hello :<br/>
> Définir `http://localhost:8080/` comme un `Redirect URL` hello haut de cette page, ou utilisez `http://localhost:[port]/` si vous utilisez un port TCP personnalisé (où *[port]* est le numéro de port TCP personnalisée hello), puis cliquez sur 'Update'

### <a name="configure-your-javascript-spa-application"></a>Configurer votre application SPA JavaScript

1.  Créez un fichier nommé `msalconfig.js` contenant les informations d’inscription de l’application hello. Si vous utilisez un projet Visual Studio, sélectionnez hello (dossier racine du projet), avec le bouton droit et sélectionnez : `Add`  >  `New Item`  >  `JavaScript File`. Nommez-le `msalconfig.js`.
2.  Ajouter hello suivant code tooyour `msalconfig.js` fichier :

```javascript
var msalconfig = {
    clientID: "[Enter hello application Id here]",
    redirectUri: location.origin
};
``` 
