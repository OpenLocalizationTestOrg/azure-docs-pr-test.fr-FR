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
# <a name="diagnosing-errors-with-hello-azure-active-directory-connection-wizard"></a><span data-ttu-id="dc4f5-103">Diagnostic d’erreurs avec hello Assistant de connexion Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dc4f5-103">Diagnosing errors with hello Azure Active Directory Connection Wizard</span></span>
<span data-ttu-id="dc4f5-104">Lors de la détection de code d’authentification précédente, Assistant de hello a détecté un type d’authentification incompatible.</span><span class="sxs-lookup"><span data-stu-id="dc4f5-104">While detecting previous authentication code, hello wizard detected an incompatible authentication type.</span></span>   

## <a name="what-is-being-checked"></a><span data-ttu-id="dc4f5-105">Quel est l'objet de la vérification ?</span><span class="sxs-lookup"><span data-stu-id="dc4f5-105">What is being checked?</span></span>
<span data-ttu-id="dc4f5-106">**Remarque :** toocorrectly détecter le code précédent de l’authentification dans un projet, hello projet doit être généré.</span><span class="sxs-lookup"><span data-stu-id="dc4f5-106">**Note:** toocorrectly detect previous authentication code in a project, hello project must be built.</span></span>  <span data-ttu-id="dc4f5-107">Si vous avez rencontré cette erreur et que vous n’avez pas de code d’authentification précédent dans votre projet, régénérez et réessayez.</span><span class="sxs-lookup"><span data-stu-id="dc4f5-107">If you encountered this error and you don't have a previous authentication code in your project, rebuild and try again.</span></span>

### <a name="project-types"></a><span data-ttu-id="dc4f5-108">Types de projet</span><span class="sxs-lookup"><span data-stu-id="dc4f5-108">Project Types</span></span>
<span data-ttu-id="dc4f5-109">Assistant de Hello vérifie type hello du projet que vous développez afin qu’il peut injecter des logique d’authentification approprié hello dans les projets hello.</span><span class="sxs-lookup"><span data-stu-id="dc4f5-109">hello wizard checks hello type of project you’re developing so it can inject hello right authentication logic into hello project.</span></span>  <span data-ttu-id="dc4f5-110">S’il existe un contrôleur qui dérive de `ApiController` dans le projet de hello, projet de hello est considéré comme un projet WebAPI.</span><span class="sxs-lookup"><span data-stu-id="dc4f5-110">If there is any controller that derives from `ApiController` in hello project, hello project is considered a WebAPI project.</span></span>  <span data-ttu-id="dc4f5-111">S’il existe uniquement les contrôleurs qui dérivent de `MVC.Controller` dans le projet de hello, projet de hello est considéré comme un projet MVC.</span><span class="sxs-lookup"><span data-stu-id="dc4f5-111">If there are only controllers that derive from `MVC.Controller` in hello project, hello project is considered an MVC project.</span></span>  <span data-ttu-id="dc4f5-112">Rien n’est pas pris en charge par l’Assistant de hello.</span><span class="sxs-lookup"><span data-stu-id="dc4f5-112">Anything else is not supported by hello wizard.</span></span>

### <a name="compatible-authentication-code"></a><span data-ttu-id="dc4f5-113">Code d’authentification compatible</span><span class="sxs-lookup"><span data-stu-id="dc4f5-113">Compatible Authentication Code</span></span>
<span data-ttu-id="dc4f5-114">Assistant de Hello recherche également des paramètres d’authentification qui ont été précédemment configurés avec l’Assistant de hello ou sont compatibles avec l’Assistant de hello.</span><span class="sxs-lookup"><span data-stu-id="dc4f5-114">hello wizard also checks for authentication settings that have been previously configured with hello wizard or are compatible with hello wizard.</span></span>  <span data-ttu-id="dc4f5-115">Si tous les paramètres sont présents, il est considéré comme un cas réentrant, et les paramètres de hello d’Affichage de hello Assistant s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="dc4f5-115">If all settings are present, it is considered a re-entrant case, and hello wizard opens display hello settings.</span></span>  <span data-ttu-id="dc4f5-116">Si seuls certains des paramètres de hello sont présents, il est considéré comme un cas d’erreur.</span><span class="sxs-lookup"><span data-stu-id="dc4f5-116">If only some of hello settings are present, it is considered an error case.</span></span>

<span data-ttu-id="dc4f5-117">Dans un projet MVC, hello Assistant vérifie les hello suivant les paramètres, qui résultent de l’utilisation précédente de l’Assistant de hello :</span><span class="sxs-lookup"><span data-stu-id="dc4f5-117">In an MVC project, hello wizard checks for any of hello following settings, which result from previous use of hello wizard:</span></span>

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:AADInstance" value="" />
    <add key="ida:PostLogoutRedirectUri" value="" />

<span data-ttu-id="dc4f5-118">En outre, hello Assistant vérifie les hello suivant les paramètres dans un projet d’API Web, qui résultent de l’utilisation précédente de l’Assistant de hello :</span><span class="sxs-lookup"><span data-stu-id="dc4f5-118">In addition, hello wizard checks for any of hello following settings in a Web API project, which result from previous use of hello wizard:</span></span>

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:Audience" value="" />

### <a name="incompatible-authentication-code"></a><span data-ttu-id="dc4f5-119">Code d’authentification incompatible</span><span class="sxs-lookup"><span data-stu-id="dc4f5-119">Incompatible Authentication Code</span></span>
<span data-ttu-id="dc4f5-120">Enfin, Assistant de hello tente de versions toodetect du code d’authentification qui ont été configurées avec les versions précédentes de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dc4f5-120">Finally, hello wizard attempts toodetect versions of authentication code that have been configured with previous versions of Visual Studio.</span></span> <span data-ttu-id="dc4f5-121">Si cette erreur s'affiche, cela signifie que votre projet comporte un type d'authentification incompatible.</span><span class="sxs-lookup"><span data-stu-id="dc4f5-121">If you received this error, it means your project contains an incompatible authentication type.</span></span> <span data-ttu-id="dc4f5-122">Assistant de Hello détecte hello suivant les types d’authentification à partir de versions antérieures de Visual Studio :</span><span class="sxs-lookup"><span data-stu-id="dc4f5-122">hello wizard detects hello following types of authentication from previous versions of Visual Studio:</span></span>

* <span data-ttu-id="dc4f5-123">Authentification Windows</span><span class="sxs-lookup"><span data-stu-id="dc4f5-123">Windows Authentication</span></span> 
* <span data-ttu-id="dc4f5-124">Comptes d'utilisateur individuels</span><span class="sxs-lookup"><span data-stu-id="dc4f5-124">Individual User Accounts</span></span> 
* <span data-ttu-id="dc4f5-125">Comptes professionnels</span><span class="sxs-lookup"><span data-stu-id="dc4f5-125">Organizational Accounts</span></span> 

<span data-ttu-id="dc4f5-126">toodetect l’authentification Windows dans un projet MVC, hello Assistant recherche hello `authentication` élément à partir de votre **web.config** fichier.</span><span class="sxs-lookup"><span data-stu-id="dc4f5-126">toodetect Windows Authentication in an MVC project, hello wizard looks for hello `authentication` element from your **web.config** file.</span></span>

<pre>
    &lt;configuration&gt;
        &lt;system.web&gt;
            <span style="background-color: yellow">&lt;authentication mode="Windows" /&gt;</span>
        &lt;/system.web&gt;
    &lt;/configuration&gt;
</pre>

<span data-ttu-id="dc4f5-127">toodetect l’authentification Windows dans un projet d’API Web, hello Assistant recherche hello `IISExpressWindowsAuthentication` élément à partir de votre projet **.csproj** fichier :</span><span class="sxs-lookup"><span data-stu-id="dc4f5-127">toodetect Windows Authentication in a Web API project, hello wizard looks for hello `IISExpressWindowsAuthentication` element from your project's **.csproj** file:</span></span>

<pre>
    &lt;Project&gt;
        &lt;PropertyGroup&gt;
            <span style="background-color: yellow">&lt;IISExpressWindowsAuthentication&gt;enabled&lt;/IISExpressWindowsAuthentication&gt;</span>
        &lt;/PropertyGroup>
    &lt;/Project&gt;
</pre>

<span data-ttu-id="dc4f5-128">l’authentification de comptes d’utilisateur individuels toodetect, Assistant de hello recherche pour l’élément de package hello du votre **Packages.config** fichier.</span><span class="sxs-lookup"><span data-stu-id="dc4f5-128">toodetect Individual User Accounts authentication, hello wizard looks for hello package element from your **Packages.config** file.</span></span>

<pre>
    &lt;packages&gt;
        <span style="background-color: yellow">&lt;package id="Microsoft.AspNet.Identity.EntityFramework" version="2.1.0" targetFramework="net45" /&gt;</span>
    &lt;/packages&gt;
</pre>

<span data-ttu-id="dc4f5-129">toodetect un ancien formulaire d’authentification de compte de société, Assistant de hello recherche hello suit l’élément à partir de **web.config**:</span><span class="sxs-lookup"><span data-stu-id="dc4f5-129">toodetect an old form of Organizational Account authentication, hello wizard looks for hello following element from **web.config**:</span></span>

<pre>
    &lt;configuration&gt;
        &lt;appSettings&gt;
            <span style="background-color: yellow">&lt;add key="ida:Realm" value="***" /&gt;</span>
        &lt;/appSettings&gt;
    &lt;/configuration&gt;
</pre>

<span data-ttu-id="dc4f5-130">type d’authentification toochange hello, supprimez le type d’authentification incompatible hello et réexécutez hello.</span><span class="sxs-lookup"><span data-stu-id="dc4f5-130">toochange hello authentication type, remove hello incompatible authentication type and run hello wizard again.</span></span>

<span data-ttu-id="dc4f5-131">Pour plus d’informations, consultez la page [Scénarios d’authentification pour Azure AD](active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="dc4f5-131">For more information, see [Authentication Scenarios for Azure AD](active-directory-authentication-scenarios.md).</span></span>

#<a name="next-steps"></a><span data-ttu-id="dc4f5-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dc4f5-132">Next steps</span></span>
- [<span data-ttu-id="dc4f5-133">Scénarios d’authentification pour Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc4f5-133">Authentication Scenarios for Azure AD</span></span>](active-directory-authentication-scenarios.md)