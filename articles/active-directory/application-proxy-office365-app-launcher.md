---
title: "aaaSet une page d’accueil personnalisée pour les applications publiées à l’aide du Proxy d’Application Azure AD | Documents Microsoft"
description: "Décrit les principes de base hello des connecteurs de Proxy d’Application Azure AD"
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
ms.date: 08/17/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 5bb695e904d285c3b440520f107c7bf63ba5cac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-a-custom-home-page-for-published-apps-by-using-azure-ad-application-proxy"></a><span data-ttu-id="6e29a-103">Définir une page d’accueil personnalisée pour les applications publiées à l’aide du proxy d’application Azure AD</span><span class="sxs-lookup"><span data-stu-id="6e29a-103">Set a custom home page for published apps by using Azure AD Application Proxy</span></span>

<span data-ttu-id="6e29a-104">Cet article explique comment tooconfigure applications toodirect utilisateurs tooa page d’accueil personnalisée.</span><span class="sxs-lookup"><span data-stu-id="6e29a-104">This article discusses how tooconfigure apps toodirect users tooa custom home page.</span></span> <span data-ttu-id="6e29a-105">Lorsque vous publiez une application avec le Proxy d’Application, vous définissez une URL interne, mais qui n’est parfois pas page hello que vos utilisateurs doivent tout d’abord voir.</span><span class="sxs-lookup"><span data-stu-id="6e29a-105">When you publish an application with Application Proxy, you set an internal URL but sometimes that's not hello page your users should see first.</span></span> <span data-ttu-id="6e29a-106">Définir une page d’accueil personnalisée afin que vos utilisateurs atteindre la page de droite toohello lorsqu’ils accèdent à des applications de hello de hello volet d’accès Azure Active Directory ou le Lanceur d’applications hello Office 365.</span><span class="sxs-lookup"><span data-stu-id="6e29a-106">Set a custom home page so that your users go toohello right page when they access hello apps from hello Azure Active Directory Access Panel or hello Office 365 app launcher.</span></span>

<span data-ttu-id="6e29a-107">Lorsque les utilisateurs lancent l’application hello, ils sont dirigés par URL de domaine par défaut toohello racine pour l’application publiée hello.</span><span class="sxs-lookup"><span data-stu-id="6e29a-107">When users launch hello app, they're directed by default toohello root domain URL for hello published app.</span></span> <span data-ttu-id="6e29a-108">page d’accueil Hello est généralement définie en tant qu’URL de la page d’accueil hello.</span><span class="sxs-lookup"><span data-stu-id="6e29a-108">hello landing page is typically set as hello home page URL.</span></span> <span data-ttu-id="6e29a-109">Utilisez des URL de page d’accueil personnalisée hello Azure AD PowerShell module toodefine tooland d’utilisateurs d’application sur une page spécifique au sein de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="6e29a-109">Use hello Azure AD PowerShell module toodefine custom home page URLs when you want app users tooland on a specific page within hello app.</span></span> 

<span data-ttu-id="6e29a-110">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="6e29a-110">For example:</span></span>
- <span data-ttu-id="6e29a-111">À l’intérieur de votre réseau d’entreprise, les utilisateurs accéder trop*https://ExpenseApp/login/login.aspx* toosign dans et accéder à votre application.</span><span class="sxs-lookup"><span data-stu-id="6e29a-111">Inside your corporate network, users go too*https://ExpenseApp/login/login.aspx* toosign in and access your app.</span></span>
- <span data-ttu-id="6e29a-112">Étant donné que vous disposez d’autres ressources comme les images que le Proxy d’Application doit tooaccess au niveau supérieur de hello hello structure des dossiers, vous publiez application hello avec *https://ExpenseApp* comme hello URL interne.</span><span class="sxs-lookup"><span data-stu-id="6e29a-112">Because you have other assets like images that Application Proxy needs tooaccess at hello top level of hello folder structure, you publish hello app with *https://ExpenseApp* as hello internal URL.</span></span>
- <span data-ttu-id="6e29a-113">Hello URL externe par défaut est *https://ExpenseApp-contoso.msappproxy.net*, qui ne prend pas vos informations d’identification toohello les utilisateurs dans la page.</span><span class="sxs-lookup"><span data-stu-id="6e29a-113">hello default external URL is *https://ExpenseApp-contoso.msappproxy.net*, which doesn't take your users toohello sign in page.</span></span>  
- <span data-ttu-id="6e29a-114">Définissez *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* comme hello toogive URL de page d’accueil de vos utilisateurs une expérience transparente.</span><span class="sxs-lookup"><span data-stu-id="6e29a-114">Set *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* as hello home page URL toogive your users a seamless experience.</span></span> 

>[!NOTE]
><span data-ttu-id="6e29a-115">Lorsque vous accordez aux utilisateurs un accès toopublished applications, les applications de hello s’affichent dans hello [panneau d’accès Azure AD](active-directory-saas-access-panel-introduction.md) et hello [Lanceur d’applications Office 365](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).</span><span class="sxs-lookup"><span data-stu-id="6e29a-115">When you give users access toopublished apps, hello apps are displayed in hello [Azure AD Access Panel](active-directory-saas-access-panel-introduction.md) and hello [Office 365 app launcher](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="6e29a-116">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="6e29a-116">Before you start</span></span>

<span data-ttu-id="6e29a-117">Avant de définir des URL de la page d’accueil hello, gardez Bonjour esprit suivant les exigences :</span><span class="sxs-lookup"><span data-stu-id="6e29a-117">Before you set hello home page URL, keep in mind hello following requirements:</span></span>

* <span data-ttu-id="6e29a-118">Vérifiez que ce chemin d’accès hello que vous spécifiez est un chemin d’accès de sous-domaine de hello URL racine du domaine.</span><span class="sxs-lookup"><span data-stu-id="6e29a-118">Ensure that hello path you specify is a subdomain path of hello root domain URL.</span></span>

  <span data-ttu-id="6e29a-119">Si l’URL de domaine à la racine de hello est, par exemple, https://apps.contoso.com/app1/, URL de page d’accueil hello que vous configurez doit commencer par https://apps.contoso.com/app1/.</span><span class="sxs-lookup"><span data-stu-id="6e29a-119">If hello root-domain URL is, for example, https://apps.contoso.com/app1/, hello home page URL that you configure must start with https://apps.contoso.com/app1/.</span></span>

* <span data-ttu-id="6e29a-120">Si vous apportez une modification toohello publié l’application, la modification de hello peut réinitialiser la valeur hello d’URL de la page d’accueil hello.</span><span class="sxs-lookup"><span data-stu-id="6e29a-120">If you make a change toohello published app, hello change might reset hello value of hello home page URL.</span></span> <span data-ttu-id="6e29a-121">Lorsque vous mettez à jour application hello Bonjour futures, vous devez vérifier de nouveau et, si nécessaire, mettez à jour les URL de la page d’accueil hello.</span><span class="sxs-lookup"><span data-stu-id="6e29a-121">When you update hello app in hello future, you should recheck and, if necessary, update hello home page URL.</span></span>

## <a name="change-hello-home-page-in-hello-azure-portal"></a><span data-ttu-id="6e29a-122">Modifier la page d’accueil hello hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="6e29a-122">Change hello home page in hello Azure portal</span></span>

1. <span data-ttu-id="6e29a-123">Connectez-vous à toohello [portail Azure](https://portal.azure.com) en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="6e29a-123">Sign in toohello [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="6e29a-124">Accédez trop**Azure Active Directory** > **inscriptions d’application** et choisissez votre application à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="6e29a-124">Navigate too**Azure Active Directory** > **App registrations** and choose your application from hello list.</span></span> 
3. <span data-ttu-id="6e29a-125">Sélectionnez **propriétés** à partir des paramètres de hello.</span><span class="sxs-lookup"><span data-stu-id="6e29a-125">Select **Properties** from hello settings.</span></span>
4. <span data-ttu-id="6e29a-126">Hello de mise à jour **URL de la page d’accueil** champ avec votre nouveau chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="6e29a-126">Update hello **Home page URL** field with your new path.</span></span> 

   ![Fournir la nouvelle URL de la page d’accueil](./media/application-proxy-office365-app-launcher/homepage.png)

5. <span data-ttu-id="6e29a-128">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="6e29a-128">Select **Save**</span></span>

## <a name="change-hello-home-page-with-powershell"></a><span data-ttu-id="6e29a-129">Modifier la page d’accueil hello avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="6e29a-129">Change hello home page with PowerShell</span></span>

### <a name="install-hello-azure-ad-powershell-module"></a><span data-ttu-id="6e29a-130">Installer le module PowerShell Azure AD de hello</span><span class="sxs-lookup"><span data-stu-id="6e29a-130">Install hello Azure AD PowerShell module</span></span>

<span data-ttu-id="6e29a-131">Avant de définir une URL de la page d’accueil personnalisée à l’aide de PowerShell, installer le module PowerShell Azure AD de hello.</span><span class="sxs-lookup"><span data-stu-id="6e29a-131">Before you define a custom home page URL by using PowerShell, install hello Azure AD PowerShell module.</span></span> <span data-ttu-id="6e29a-132">Vous pouvez télécharger le package de hello de hello [PowerShell Gallery](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131), qui utilise hello de point de terminaison de l’API Graph.</span><span class="sxs-lookup"><span data-stu-id="6e29a-132">You can download hello package from hello [PowerShell Gallery](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131), which uses hello Graph API endpoint.</span></span> 

<span data-ttu-id="6e29a-133">tooinstall hello du package, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="6e29a-133">tooinstall hello package, follow these steps:</span></span>

1. <span data-ttu-id="6e29a-134">Ouvrez une fenêtre PowerShell standard et puis exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="6e29a-134">Open a standard PowerShell window, and then run hello following command:</span></span>

    ```
     Install-Module -Name AzureAD
    ```
    <span data-ttu-id="6e29a-135">Si vous exécutez la commande hello en tant que non-administrateur, utilisez hello `-scope currentuser` option.</span><span class="sxs-lookup"><span data-stu-id="6e29a-135">If you're running hello command as a non-admin, use hello `-scope currentuser` option.</span></span>
2. <span data-ttu-id="6e29a-136">Pendant l’installation de hello, sélectionnez **Y** tooinstall deux packages de Nuget.org. Les deux packages sont requis.</span><span class="sxs-lookup"><span data-stu-id="6e29a-136">During hello installation, select **Y** tooinstall two packages from Nuget.org. Both packages are required.</span></span> 

### <a name="find-hello-objectid-of-hello-app"></a><span data-ttu-id="6e29a-137">Recherche hello ObjectID de l’application hello</span><span class="sxs-lookup"><span data-stu-id="6e29a-137">Find hello ObjectID of hello app</span></span>

<span data-ttu-id="6e29a-138">Obtenir hello ObjectID de l’application hello et recherchez application hello par sa page d’accueil.</span><span class="sxs-lookup"><span data-stu-id="6e29a-138">Obtain hello ObjectID of hello app, and then search for hello app by its home page.</span></span>

1. <span data-ttu-id="6e29a-139">Ouvrez PowerShell et importer le module de hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6e29a-139">Open PowerShell and import hello Azure AD module.</span></span>

    ```
    Import-Module AzureAD
    ```

2. <span data-ttu-id="6e29a-140">Se connecter toohello module Azure AD en tant qu’administrateur de locataire hello.</span><span class="sxs-lookup"><span data-stu-id="6e29a-140">Sign in toohello Azure AD module as hello tenant administrator.</span></span>

    ```
    Connect-AzureAD
    ```
3. <span data-ttu-id="6e29a-141">Recherchez l’application hello en fonction de son URL de la page d’accueil.</span><span class="sxs-lookup"><span data-stu-id="6e29a-141">Find hello app based on its home page URL.</span></span> <span data-ttu-id="6e29a-142">Vous pouvez trouver des URL de hello dans le portail de hello en accédant trop**Azure Active Directory** > **des applications d’entreprise** > **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="6e29a-142">You can find hello URL in hello portal by going too**Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span> <span data-ttu-id="6e29a-143">Cet exemple utilise *sharepoint-iddemo*.</span><span class="sxs-lookup"><span data-stu-id="6e29a-143">This example uses *sharepoint-iddemo*.</span></span>

    ```
    Get-AzureADApplication | where { $_.Homepage -like “sharepoint-iddemo” } | fl DisplayName, Homepage, ObjectID
    ```
4. <span data-ttu-id="6e29a-144">Vous devez obtenir un résultat similaire toohello celui présenté ici.</span><span class="sxs-lookup"><span data-stu-id="6e29a-144">You should get a result that's similar toohello one shown here.</span></span> <span data-ttu-id="6e29a-145">Copiez hello ObjectID GUID toouse dans la section suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="6e29a-145">Copy hello ObjectID GUID toouse in hello next section.</span></span>

    ```
    DisplayName : SharePoint
    Homepage    : https://sharepoint-iddemo.msappproxy.net/
    ObjectId    : 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

### <a name="update-hello-home-page-url"></a><span data-ttu-id="6e29a-146">Mettre à jour des URL de la page d’accueil hello</span><span class="sxs-lookup"><span data-stu-id="6e29a-146">Update hello home page URL</span></span>

<span data-ttu-id="6e29a-147">Bonjour même module PowerShell que vous avez utilisé pour l’étape 1, effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="6e29a-147">In hello same PowerShell module that you used for step 1, perform hello following steps:</span></span>

1. <span data-ttu-id="6e29a-148">Vérifiez que vous disposez hello corriger l’application, puis remplacez *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* avec hello ObjectID que vous avez copié dans hello précédant l’étape.</span><span class="sxs-lookup"><span data-stu-id="6e29a-148">Confirm that you have hello correct app, and replace *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* with hello ObjectID that you copied in hello preceding step.</span></span>

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4.
    ```

 <span data-ttu-id="6e29a-149">Maintenant que vous avez confirmé l’application hello, vous êtes prêt tooupdate hello page d’accueil, comme suit.</span><span class="sxs-lookup"><span data-stu-id="6e29a-149">Now that you've confirmed hello app, you're ready tooupdate hello home page, as follows.</span></span>

2. <span data-ttu-id="6e29a-150">Créer des modifications hello à toomake un toohold d’objet application vide.</span><span class="sxs-lookup"><span data-stu-id="6e29a-150">Create a blank application object toohold hello changes that you want toomake.</span></span> <span data-ttu-id="6e29a-151">Cette variable contient des valeurs hello que vous souhaitez tooupdate.</span><span class="sxs-lookup"><span data-stu-id="6e29a-151">This variable holds hello values that you want tooupdate.</span></span> <span data-ttu-id="6e29a-152">Rien n’est créé lors de cette étape.</span><span class="sxs-lookup"><span data-stu-id="6e29a-152">Nothing is created in this step.</span></span>

    ```
    $appnew = New-Object “Microsoft.Open.AzureAD.Model.Application”
    ```

3. <span data-ttu-id="6e29a-153">La valeur hello page d’accueil URL toohello souhaité.</span><span class="sxs-lookup"><span data-stu-id="6e29a-153">Set hello home page URL toohello value that you want.</span></span> <span data-ttu-id="6e29a-154">valeur de Hello doit être un chemin d’accès de sous-domaine de l’application publiée hello.</span><span class="sxs-lookup"><span data-stu-id="6e29a-154">hello value must be a subdomain path of hello published app.</span></span> <span data-ttu-id="6e29a-155">Par exemple, si vous modifiez hello URL de page d’accueil à partir de *https://sharepoint-iddemo.msappproxy.net/* trop*https://sharepoint-iddemo.msappproxy.net/hybrid/*, application utilisateurs accèdent directement toohello personnalisé page d’accueil.</span><span class="sxs-lookup"><span data-stu-id="6e29a-155">For example, if you change hello home page URL from *https://sharepoint-iddemo.msappproxy.net/* too*https://sharepoint-iddemo.msappproxy.net/hybrid/*, app users go directly toohello custom home page.</span></span>

    ```
    $homepage = “https://sharepoint-iddemo.msappproxy.net/hybrid/”
    ```
4. <span data-ttu-id="6e29a-156">Rendre hello mise à jour à l’aide de hello GUID (ObjectID) que vous avez copié dans « étape 1 : rechercher hello ObjectID de l’application hello. »</span><span class="sxs-lookup"><span data-stu-id="6e29a-156">Make hello update by using hello GUID (ObjectID) that you copied in "Step 1: Find hello ObjectID of hello app."</span></span>

    ```
    Set-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4 -Homepage $homepage
    ```
5. <span data-ttu-id="6e29a-157">tooconfirm que la modification de hello a réussi, redémarrez l’application hello.</span><span class="sxs-lookup"><span data-stu-id="6e29a-157">tooconfirm that hello change was successful, restart hello app.</span></span>

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

>[!NOTE]
><span data-ttu-id="6e29a-158">Les modifications que vous apportez toohello application peuvent réinitialiser les URL de la page d’accueil hello.</span><span class="sxs-lookup"><span data-stu-id="6e29a-158">Any changes that you make toohello app might reset hello home page URL.</span></span> <span data-ttu-id="6e29a-159">Si l’URL de votre page d’accueil se réinitialise, répétez l’étape 2.</span><span class="sxs-lookup"><span data-stu-id="6e29a-159">If your home page URL resets, repeat step 2.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e29a-160">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6e29a-160">Next steps</span></span>

- [<span data-ttu-id="6e29a-161">Activer tooSharePoint l’accès à distance avec le Proxy d’Application Azure AD</span><span class="sxs-lookup"><span data-stu-id="6e29a-161">Enable remote access tooSharePoint with Azure AD Application Proxy</span></span>](application-proxy-enable-remote-access-sharepoint.md)
- [<span data-ttu-id="6e29a-162">Activer le Proxy d’Application Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="6e29a-162">Enable Application Proxy in hello Azure portal</span></span>](active-directory-application-proxy-enable.md)
