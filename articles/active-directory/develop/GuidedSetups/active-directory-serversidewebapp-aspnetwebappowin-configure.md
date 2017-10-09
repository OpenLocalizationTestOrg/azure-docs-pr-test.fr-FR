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
ms.openlocfilehash: e666be4622ad30aaa1e12e49ae56bbe1e129b2a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a>Créer une application (Express)
Maintenant vous devez tooregister votre application Bonjour *portail de l’enregistrement d’Application Microsoft*:
1. Inscrire votre application via hello [portail de l’enregistrement d’Application Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=serverSideWebApp&appTech=aspNetWebAppOwin&step=configure)
2.  Entrez un nom pour votre application, ainsi que votre adresse e-mail.
3.  Assurez-vous que l’option hello pour le programme d’installation interactive est activée
4.  Suivez les instructions de hello tooadd une application de tooyour URL de redirection

## <a name="add-your-application-registration-information-tooyour-solution-advanced"></a>Ajoutez votre solution de tooyour d’application d’enregistrement d’informations (Avancé)
Maintenant vous devez tooregister votre application Bonjour *portail de l’enregistrement d’Application Microsoft*:
1. Accédez toohello [portail de l’enregistrement d’Application Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister une application
2. Entrez un nom pour votre application, ainsi que votre adresse e-mail. 
3.  Assurez-vous que l’option hello pour le programme d’installation interactive est désactivée
4.  Cliquez sur `Add Platform`, puis sélectionnez `Web`.
5.  Revenir en arrière tooVisual Studio et, dans l’Explorateur de solutions, sélectionnez le projet de hello et examinez les fenêtre de propriétés de hello (si vous ne voyez pas une fenêtre de propriétés, appuyez sur F4)
6.  Changent avec SSL activé`True`
7.  Copiez hello URL SSL et ajouter cette liste de toohello URL de l’URL de redirection dans la liste du portail hello d’inscription d’URL de redirection :<br/><br/>![Propriétés du projet](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)<br />
8.  Ajoutez hello qui suit dans `web.config` situé dans le dossier racine de hello section hello `configuration\appSettings`:

```xml
<add key="ClientId" value="Enter_the_Application_Id_here" />
<add key="redirectUri" value="Enter_the_Redirect_URL_here" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
<!-- Workaround for Docs conversion bug -->
<ol start="9">
<li>
Remplacez `ClientId` par hello Id d’Application vous venez d’enregistrer
</li>
<li>
Remplacez `redirectUri` par hello URL SSL de votre projet
</li>
</ol>
<!-- End Docs -->
