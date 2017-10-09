---
title: "mise en route d’aaaAzure AD v2 iOS - configurer | Documents Microsoft"
description: "Cet article explique comment les applications iOS (Swift) peuvent appeler une API qui nécessite des jetons d’accès à partir d’un point de terminaison Azure Active Directory v2."
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
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: 537cc7f0de6cd947fe340566c9e93f8bb08d57a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a>Créer une application (Express)
Maintenant vous devez tooregister votre application Bonjour *portail de l’enregistrement d’Application Microsoft*:
1. Inscrire votre application via hello [portail de l’enregistrement d’Application Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=ios&step=configure)
2.  Entrez un nom pour votre application, ainsi que votre adresse e-mail.
3.  Assurez-vous que l’option hello pour le programme d’installation interactive est activée
4.  Suivez l’ID de l’application hello instructions tooobtain hello et collez-le dans votre code

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a>Ajoutez votre solution de tooyour d’application d’enregistrement d’informations (Avancé)

1.  Accédez trop[portail de l’enregistrement d’Application Microsoft](https://apps.dev.microsoft.com/portal/register-app)
2.  Entrez un nom pour votre application, ainsi que votre adresse e-mail.
3.  Assurez-vous que l’option hello pour le programme d’installation interactive est désactivée
4.  Cliquez sur `Add Platform`, puis sélectionnez `Native Application` et cliquez sur `Save`.
5.  Revenir en arrière tooXcode. Dans `ViewController.swift`, remplacez la ligne hello commençant par '`let kClientID`' avec l’ID d’application hello enregistré :

```swift
let kClientID = "Your_Application_Id_Here"
```

<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
Touche CTRL enfoncée et cliquez sur <code>Info.plist</code> toobring haut du menu contextuel de hello, puis cliquez sur : <code>Open As</code>> <code>Source Code</code>
</li>
<li>
Sous hello <code>dict</code> nœud racine, ajoutez hello :
</li>
</ol>

```xml
<key>CFBundleURLTypes</key>
<array>
    <dict>
        <key>CFBundleTypeRole</key>
        <string>Editor</string>
        <key>CFBundleURLName</key>
        <string>$(PRODUCT_BUNDLE_IDENTIFIER)</string>
        <key>CFBundleURLSchemes</key>
        <array>
            <string>msal[Your_Application_Id_Here]</string>
            <string>auth</string>
        </array>
    </dict>
</array>
```
<ol start="8">
<li>
Remplacez <i> <code>[Your_Application_Id_Here]</code> </i> avec hello Id d’Application vous venez d’enregistrer
</li>
</ol>
