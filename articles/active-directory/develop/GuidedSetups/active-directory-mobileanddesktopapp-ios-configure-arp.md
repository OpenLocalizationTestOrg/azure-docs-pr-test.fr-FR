---
title: aaaAzure AD v2 iOS route - configurer ARP () | Documents Microsoft
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
ms.openlocfilehash: e5087e13160243d808b1d02771fa66fb332cfad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
## <a name="add-hello-applications-registration-information-tooyour-app"></a><span data-ttu-id="955e1-103">Ajouter une application de l’application hello d’enregistrement d’informations tooyour</span><span class="sxs-lookup"><span data-stu-id="955e1-103">Add hello application’s registration information tooyour app</span></span>

<span data-ttu-id="955e1-104">Dans cette étape, vous avez besoin d’un projet de tooyour tooadd hello Id d’Application :</span><span class="sxs-lookup"><span data-stu-id="955e1-104">In this step, you need tooadd hello Application Id tooyour project:</span></span>

1.  <span data-ttu-id="955e1-105">Dans `ViewController.swift`, remplacez la ligne hello commençant par '`let kClientID`' avec :</span><span class="sxs-lookup"><span data-stu-id="955e1-105">In `ViewController.swift`, replace hello line starting with '`let kClientID`' with:</span></span>
```swift
let kClientID = "[Enter hello application Id here]"
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="955e1-106">Touche CTRL enfoncée et cliquez sur <code>Info.plist</code> toobring haut du menu contextuel de hello, puis cliquez sur : <code>Open As</code>> <code>Source Code</code>
</span><span class="sxs-lookup"><span data-stu-id="955e1-106">Control+click <code>Info.plist</code> toobring up hello contextual menu, and then click: <code>Open As</code> > <code>Source Code</code>
</span></span></li>
<li>
<span data-ttu-id="955e1-107">Sous hello <code>dict</code> nœud racine, ajoutez hello :</span><span class="sxs-lookup"><span data-stu-id="955e1-107">Under hello <code>dict</code> root node, add hello following:</span></span>
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
            <string>msal[Enter hello application Id here]</string>
            <string>auth</string>
        </array>
    </dict>
</array>
```
