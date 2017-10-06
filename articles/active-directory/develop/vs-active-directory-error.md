---
title: erreurs de toodiagnose aaaHow par hello Assistant de connexion Azure Active Directory
description: "Assistant de connexion Hello Active Directory a détecté un type d’authentification incompatible"
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: dd89ea63-4e45-4da1-9642-645b9309670a
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 03/05/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: f71c5b41457c0c8db05042e8d5f723e58ad11844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnosing-errors-with-hello-azure-active-directory-connection-wizard"></a>Diagnostic d’erreurs avec hello Assistant de connexion Azure Active Directory
Lors de la détection de code d’authentification précédente, Assistant de hello a détecté un type d’authentification incompatible.   

## <a name="what-is-being-checked"></a>Quel est l'objet de la vérification ?
**Remarque :** toocorrectly détecter le code précédent de l’authentification dans un projet, hello projet doit être généré.  Si vous avez rencontré cette erreur et que vous n’avez pas de code d’authentification précédent dans votre projet, régénérez et réessayez.

### <a name="project-types"></a>Types de projet
Assistant de Hello vérifie type hello du projet que vous développez afin qu’il peut injecter des logique d’authentification approprié hello dans les projets hello.  S’il existe un contrôleur qui dérive de `ApiController` dans le projet de hello, projet de hello est considéré comme un projet WebAPI.  S’il existe uniquement les contrôleurs qui dérivent de `MVC.Controller` dans le projet de hello, projet de hello est considéré comme un projet MVC.  Rien n’est pas pris en charge par l’Assistant de hello.

### <a name="compatible-authentication-code"></a>Code d’authentification compatible
Assistant de Hello recherche également des paramètres d’authentification qui ont été précédemment configurés avec l’Assistant de hello ou sont compatibles avec l’Assistant de hello.  Si tous les paramètres sont présents, il est considéré comme un cas réentrant, et les paramètres de hello d’Affichage de hello Assistant s’ouvre.  Si seuls certains des paramètres de hello sont présents, il est considéré comme un cas d’erreur.

Dans un projet MVC, hello Assistant vérifie les hello suivant les paramètres, qui résultent de l’utilisation précédente de l’Assistant de hello :

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:AADInstance" value="" />
    <add key="ida:PostLogoutRedirectUri" value="" />

En outre, hello Assistant vérifie les hello suivant les paramètres dans un projet d’API Web, qui résultent de l’utilisation précédente de l’Assistant de hello :

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:Audience" value="" />

### <a name="incompatible-authentication-code"></a>Code d’authentification incompatible
Enfin, Assistant de hello tente de versions toodetect du code d’authentification qui ont été configurées avec les versions précédentes de Visual Studio. Si cette erreur s'affiche, cela signifie que votre projet comporte un type d'authentification incompatible. Assistant de Hello détecte hello suivant les types d’authentification à partir de versions antérieures de Visual Studio :

* Authentification Windows 
* Comptes d'utilisateur individuels 
* Comptes professionnels 

toodetect l’authentification Windows dans un projet MVC, hello Assistant recherche hello `authentication` élément à partir de votre **web.config** fichier.

<pre>
    &lt;configuration&gt;
        &lt;system.web&gt;
            <span style="background-color: yellow">&lt;authentication mode="Windows" /&gt;</span>
        &lt;/system.web&gt;
    &lt;/configuration&gt;
</pre>

toodetect l’authentification Windows dans un projet d’API Web, hello Assistant recherche hello `IISExpressWindowsAuthentication` élément à partir de votre projet **.csproj** fichier :

<pre>
    &lt;Project&gt;
        &lt;PropertyGroup&gt;
            <span style="background-color: yellow">&lt;IISExpressWindowsAuthentication&gt;enabled&lt;/IISExpressWindowsAuthentication&gt;</span>
        &lt;/PropertyGroup>
    &lt;/Project&gt;
</pre>

l’authentification de comptes d’utilisateur individuels toodetect, Assistant de hello recherche pour l’élément de package hello du votre **Packages.config** fichier.

<pre>
    &lt;packages&gt;
        <span style="background-color: yellow">&lt;package id="Microsoft.AspNet.Identity.EntityFramework" version="2.1.0" targetFramework="net45" /&gt;</span>
    &lt;/packages&gt;
</pre>

toodetect un ancien formulaire d’authentification de compte de société, Assistant de hello recherche hello suit l’élément à partir de **web.config**:

<pre>
    &lt;configuration&gt;
        &lt;appSettings&gt;
            <span style="background-color: yellow">&lt;add key="ida:Realm" value="***" /&gt;</span>
        &lt;/appSettings&gt;
    &lt;/configuration&gt;
</pre>

type d’authentification toochange hello, supprimez le type d’authentification incompatible hello et réexécutez hello.

Pour plus d’informations, consultez la page [Scénarios d’authentification pour Azure AD](active-directory-authentication-scenarios.md).

#<a name="next-steps"></a>Étapes suivantes
- [Scénarios d’authentification pour Azure AD](active-directory-authentication-scenarios.md)