---
title: "Interactive d’Active Directory v2 JS SPA aaaAzure configuration - configurer | Documents Microsoft"
description: "Comment les applications JavaScript SPA peuvent appeler une API qui nécessite des jetons d’accès à partir d’un point de terminaison Azure Active Directory v2"
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
ms.openlocfilehash: 1b93298d4bd4e17dd261dbb75502a122c30aac97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
## <a name="register-your-application"></a>Inscrivez votre application

Il existe plusieurs façons toocreate une application, sélectionnez un d’eux :

### <a name="option-1-register-your-application-express-mode"></a>Option 1 : Inscrire votre application (mode Express)
Maintenant vous devez tooregister votre application Bonjour *portail de l’enregistrement d’Application Microsoft*:

1.  Inscrire votre application via hello [portail de l’enregistrement d’Application Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=singlePageApp&appTech=javascriptSpa&step=configure)
2.  Entrez un nom pour votre application, ainsi que votre adresse e-mail.
3.  Assurez-vous qu’option de hello *guidée par le programme d’installation* est activée
4.  Suivez l’ID de l’application hello instructions tooobtain hello et collez-le dans votre code

### <a name="option-2-register-your-application-advanced-mode"></a>Option 2 : Inscrire votre application (mode Avancé)

1. Accédez toohello [portail de l’enregistrement d’Application Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister une application
2. Entrez un nom pour votre application, ainsi que votre adresse e-mail. 
3. Assurez-vous qu’option de hello *guidée par le programme d’installation* est désactivée
4.  Cliquez sur `Add Platform`, puis sélectionnez `Web`.
5. Ajouter hello `Redirect URL` qui correspondent aux URL de l’application toohello basée sur votre serveur web. Consultez les sections hello ci-dessous pour obtenir des instructions sur la façon de tooset / obtenir l’URL de redirection hello dans Visual Studio et Python.
6. Cliquez sur *Enregistrer*.

> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a>Instructions Visual Studio pour obtenir l’URL de redirection
> Suivez hello instructions tooobtain votre URL de redirection :
> 1.    Dans *l’Explorateur de solutions*, sélectionnez le projet de hello et examinez hello `Properties` fenêtre (si vous ne voyez pas une fenêtre de propriétés, appuyez sur `F4`)
> 2.    Copier la valeur hello à partir de `URL` toohello Presse-papiers :<br/> ![Propriétés du projet](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)<br />
> 3.    Commutateur arrière toohello *portail de l’enregistrement d’Application* et collez la valeur hello en tant qu’un `Redirect URL` et cliquez sur « Enregistrer »

<p/>

> #### <a name="setting-redirect-url-for-python"></a>Configuration d’une URL de redirection pour Python
> Pour Python, vous pouvez définir le port du serveur web hello via la ligne de commande. Cet Assistant d’installation utilise le port 8080 hello pour référence, mais vous êtes libre toouse tout port disponible. Dans tous les cas, suivez les instructions de hello sous tooset une URL de redirection dans les informations d’inscription de l’application hello :<br/>
> - Commutateur toohello arrière *portail de l’enregistrement d’Application* et définissez `http://localhost:8080/` comme un `Redirect URL`, ou utilisez `http://localhost:[port]/` si vous utilisez un port TCP personnalisé (où *[port]* est le port TCP personnalisé hello nombre) et cliquez sur « Enregistrer »


#### <a name="configure-your-javascript-spa"></a>Configurer une application SPA JavaScript

1.  Créez un fichier nommé `msalconfig.js` contenant les informations d’inscription de l’application hello. Si vous utilisez un projet Visual Studio, sélectionnez hello (dossier racine du projet), avec le bouton droit et sélectionnez : `Add`  >  `New Item`  >  `JavaScript File`. Nommez-le `msalconfig.js`.
2.  Ajouter hello suivant code tooyour `msalconfig.js` fichier :

```javascript
var msalconfig = {
    clientID: "Enter_the_Application_Id_here",
    redirectUri: location.origin
};
```
<ol start="3">
<li>
Remplacez <code>Enter_the_Application_Id_here</code> par hello Id d’Application vous venez d’enregistrer
</li>
</ol>
