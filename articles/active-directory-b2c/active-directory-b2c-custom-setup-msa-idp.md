---
title: "Azure Active Directory B2C : ajouter un compte Microsoft (MSA) comme fournisseur d’identité à l’aide de stratégies personnalisées"
description: "Exemple utilisant Microsoft comme fournisseur d’identité à l’aide du protocole OpenID Connect (OIDC)"
services: active-directory-b2c
documentationcenter: 
author: yoelhor
manager: joroja
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: yoelh
ms.openlocfilehash: 577ac612f69015e6790f2fa9f2cfb42c2b524b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-microsoft-account-msa-as-an-identity-provider-using-custom-policies"></a><span data-ttu-id="a2a18-103">Azure Active Directory B2C : ajouter un compte Microsoft (MSA) comme fournisseur d’identité à l’aide de stratégies personnalisées</span><span class="sxs-lookup"><span data-stu-id="a2a18-103">Azure Active Directory B2C: Add Microsoft Account (MSA) as an identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="a2a18-104">Cet article vous explique comment tooenable connectez-vous pour les utilisateurs de compte Microsoft (MSA) via l’utilisation de hello de [des stratégies personnalisées](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="a2a18-104">This article shows you how tooenable sign-in for users from Microsoft account (MSA) through hello use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a2a18-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a2a18-105">Prerequisites</span></span>
<span data-ttu-id="a2a18-106">Hello terminé les étapes Bonjour [mise en route avec les stratégies personnalisées](active-directory-b2c-get-started-custom.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="a2a18-106">Complete hello steps in hello [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="a2a18-107">Ces étapes sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="a2a18-107">These steps include:</span></span>

1.  <span data-ttu-id="a2a18-108">créer une application de compte Microsoft ;</span><span class="sxs-lookup"><span data-stu-id="a2a18-108">Creating a Microsoft account application.</span></span>
2.  <span data-ttu-id="a2a18-109">Ajout de hello Microsoft compte application clé tooAzure AD B2C</span><span class="sxs-lookup"><span data-stu-id="a2a18-109">Adding hello Microsoft account application key tooAzure AD B2C</span></span>
3.  <span data-ttu-id="a2a18-110">Ajout d’une stratégie de tooa de fournisseur de revendications</span><span class="sxs-lookup"><span data-stu-id="a2a18-110">Adding claims provider tooa policy</span></span>
4.  <span data-ttu-id="a2a18-111">L’inscription de voyage de hello Account Microsoft revendications fournisseur tooa utilisateur</span><span class="sxs-lookup"><span data-stu-id="a2a18-111">Registering hello Microsoft Account claims provider tooa user journey</span></span>
5.  <span data-ttu-id="a2a18-112">Téléchargement de stratégie de hello tooan Azure AD B2C de client et de le tester</span><span class="sxs-lookup"><span data-stu-id="a2a18-112">Uploading hello policy tooan Azure AD B2C tenant and test it</span></span>

## <a name="create-a-microsoft-account-application"></a><span data-ttu-id="a2a18-113">Créer une application de compte Microsoft</span><span class="sxs-lookup"><span data-stu-id="a2a18-113">Create a Microsoft account application</span></span>
<span data-ttu-id="a2a18-114">toouse de compte Microsoft en tant que fournisseur d’identité dans Azure Active Directory (Azure AD) B2C, vous devez toocreate une application de compte Microsoft et lui fournir les paramètres appropriés hello.</span><span class="sxs-lookup"><span data-stu-id="a2a18-114">toouse Microsoft account as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Microsoft account application and supply it with hello right parameters.</span></span> <span data-ttu-id="a2a18-115">Il vous faut un compte Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a2a18-115">You need a Microsoft account.</span></span> <span data-ttu-id="a2a18-116">Si vous n’en avez pas, rendez-vous sur [https://www.live.com/](https://www.live.com/).</span><span class="sxs-lookup"><span data-stu-id="a2a18-116">If you don’t have one, visit [https://www.live.com/](https://www.live.com/).</span></span>

1.  <span data-ttu-id="a2a18-117">Accédez toohello [portail de l’enregistrement d’Application Microsoft](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) et connectez-vous avec vos informations d’identification du compte Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a2a18-117">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) and sign in with your Microsoft account credentials.</span></span>
2.  <span data-ttu-id="a2a18-118">Cliquez sur **Ajouter une application**.</span><span class="sxs-lookup"><span data-stu-id="a2a18-118">Click **Add an app**.</span></span>

    ![Compte Microsoft : ajouter une application](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-new-app.png)

3.  <span data-ttu-id="a2a18-120">Donnez un **Nom** à votre application, indiquez une **adresse e-mail de contact**, décochez la case **Aidez-moi à commencer** et cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="a2a18-120">Provide a **Name** for your application, **Contact email**, uncheck **Let us help you get started** and click **Create**.</span></span>

    ![Compte Microsoft : inscrire une application](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-name.png)

4.  <span data-ttu-id="a2a18-122">Copiez la valeur hello **Id de l’Application**. Vous en avez besoin tooconfigure compte Microsoft en tant que fournisseur d’identité dans votre client.</span><span class="sxs-lookup"><span data-stu-id="a2a18-122">Copy hello value of **Application Id**. You need it tooconfigure Microsoft account as an identity provider in your tenant.</span></span>

    ![Compte Microsoft - copier la valeur d’Id de l’Application hello](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-id.png)

5.  <span data-ttu-id="a2a18-124">Cliquez sur **Ajouter une plateforme**.</span><span class="sxs-lookup"><span data-stu-id="a2a18-124">Click on **Add platform**</span></span>

    ![Compte Microsoft - Ajouter une plateforme](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-platform.png)

6.  <span data-ttu-id="a2a18-126">Dans la liste des plateformes hello, choisissez **Web**.</span><span class="sxs-lookup"><span data-stu-id="a2a18-126">From hello platform list, choose **Web**.</span></span>

    ![Compte Microsoft, à partir de la liste des plateformes hello choisissez Web](media/active-directory-b2c-custom-setup-ms-account-idp/msa-web.png)

7.  <span data-ttu-id="a2a18-128">Entrez `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` Bonjour **URI de redirection** champ.</span><span class="sxs-lookup"><span data-stu-id="a2a18-128">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Redirect URIs** field.</span></span> <span data-ttu-id="a2a18-129">Remplacez **{tenant}** par votre nom de client (par exemple, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="a2a18-129">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>

    ![Compte Microsoft : définir des URL de redirection](media/active-directory-b2c-custom-setup-ms-account-idp/msa-redirect-url.png)

8.  <span data-ttu-id="a2a18-131">Cliquez sur **générer un nouveau mot de passe** sous hello **Application Secrets** section.</span><span class="sxs-lookup"><span data-stu-id="a2a18-131">Click on **Generate New Password** under hello **Application Secrets** section.</span></span> <span data-ttu-id="a2a18-132">Copiez le nouveau mot de passe hello affiché sur l’écran.</span><span class="sxs-lookup"><span data-stu-id="a2a18-132">Copy hello new password displayed on screen.</span></span> <span data-ttu-id="a2a18-133">Vous en avez besoin tooconfigure compte Microsoft en tant que fournisseur d’identité dans votre client.</span><span class="sxs-lookup"><span data-stu-id="a2a18-133">You need it tooconfigure Microsoft account as an identity provider in your tenant.</span></span> <span data-ttu-id="a2a18-134">Ce mot de passe est une information d’identification de sécurité importante.</span><span class="sxs-lookup"><span data-stu-id="a2a18-134">This password is an important security credential.</span></span>

    ![Compte Microsoft - générer un nouveau mot de passe](media/active-directory-b2c-custom-setup-ms-account-idp/msa-generate-new-password.png)

    ![Compte Microsoft - copie hello nouveau mot de passe](media/active-directory-b2c-custom-setup-ms-account-idp/msa-new-password.png)

9.  <span data-ttu-id="a2a18-137">Case à cocher hello indiquant **prise en charge du Kit de développement logiciel Live** sous hello **Options avancées** section.</span><span class="sxs-lookup"><span data-stu-id="a2a18-137">Check hello box that says **Live SDK support** under hello **Advanced Options** section.</span></span> <span data-ttu-id="a2a18-138">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="a2a18-138">Click **Save**.</span></span>

    ![Compte Microsoft - Support du Kit SDK Live](media/active-directory-b2c-custom-setup-ms-account-idp/msa-live-sdk-support.png)

## <a name="add-hello-microsoft-account-application-key-tooazure-ad-b2c"></a><span data-ttu-id="a2a18-140">Ajouter hello Microsoft compte application clé tooAzure AD B2C</span><span class="sxs-lookup"><span data-stu-id="a2a18-140">Add hello Microsoft account application key tooAzure AD B2C</span></span>
<span data-ttu-id="a2a18-141">Fédération avec des comptes Microsoft requiert une clé secrète client pour tootrust de compte Microsoft Azure AD B2C au nom de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="a2a18-141">Federation with Microsoft accounts requires a client secret for Microsoft account tootrust Azure AD B2C on behalf of hello application.</span></span> <span data-ttu-id="a2a18-142">Vous devez toostore votre secert d’application de compte Microsoft Azure AD B2C locataire :</span><span class="sxs-lookup"><span data-stu-id="a2a18-142">You need toostore your Microsoft account application secert in Azure AD B2C tenant:</span></span>   

1.  <span data-ttu-id="a2a18-143">Accédez tooyour Azure AD B2C client, puis sélectionnez **B2C paramètres** > **infrastructure expérience d’identité**</span><span class="sxs-lookup"><span data-stu-id="a2a18-143">Go tooyour Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="a2a18-144">Sélectionnez **clés de stratégie** tooview hello disponibles dans votre client.</span><span class="sxs-lookup"><span data-stu-id="a2a18-144">Select **Policy Keys** tooview hello keys available in your tenant.</span></span>
3.  <span data-ttu-id="a2a18-145">Cliquez sur **+Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="a2a18-145">Click **+Add**.</span></span>
4.  <span data-ttu-id="a2a18-146">Pour **Options**, utilisez **Manuel**.</span><span class="sxs-lookup"><span data-stu-id="a2a18-146">For **Options**, use **Manual**.</span></span>
5.  <span data-ttu-id="a2a18-147">Pour **Nom**, utilisez `MSASecret`.</span><span class="sxs-lookup"><span data-stu-id="a2a18-147">For **Name**, use `MSASecret`.</span></span>  
    <span data-ttu-id="a2a18-148">préfixe de Hello `B2C_1A_` peuvent être ajoutées automatiquement.</span><span class="sxs-lookup"><span data-stu-id="a2a18-148">hello prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="a2a18-149">Bonjour **Secret** , entrez votre clé secrète d’application Microsoft à partir de https://apps.dev.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="a2a18-149">In hello **Secret** box, enter your Microsoft application secret from https://apps.dev.microsoft.com</span></span>
7.  <span data-ttu-id="a2a18-150">Pour **Utilisation de la clé**, utilisez **Signature**.</span><span class="sxs-lookup"><span data-stu-id="a2a18-150">For **Key usage**, use **Signature**.</span></span>
8.  <span data-ttu-id="a2a18-151">Cliquez sur **Créer**</span><span class="sxs-lookup"><span data-stu-id="a2a18-151">Click **Create**</span></span>
9.  <span data-ttu-id="a2a18-152">Vérifiez que vous avez créé la clé de hello `B2C_1A_MSASecret`.</span><span class="sxs-lookup"><span data-stu-id="a2a18-152">Confirm that you've created hello key `B2C_1A_MSASecret`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="a2a18-153">Ajouter un fournisseur de revendications à une stratégie d’extension</span><span class="sxs-lookup"><span data-stu-id="a2a18-153">Add a claims provider in your extension policy</span></span>
<span data-ttu-id="a2a18-154">Si vous souhaitez que les utilisateurs toosign à l’aide de Microsoft Account, vous devez toodefine Account Microsoft en tant que fournisseur de revendications.</span><span class="sxs-lookup"><span data-stu-id="a2a18-154">If you want users toosign in by using Microsoft Account, you need toodefine Microsoft Account as a claims provider.</span></span> <span data-ttu-id="a2a18-155">En d’autres termes, vous devez toospecify un point de terminaison Azure AD B2C communique avec.</span><span class="sxs-lookup"><span data-stu-id="a2a18-155">In other words, you need toospecify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="a2a18-156">point de terminaison Hello fournit un ensemble de revendications qui sont utilisées par Azure AD B2C tooverify authentifié un utilisateur spécifique.</span><span class="sxs-lookup"><span data-stu-id="a2a18-156">hello endpoint provides a set of claims that are used by Azure AD B2C tooverify that a specific user has authenticated.</span></span>

<span data-ttu-id="a2a18-157">Définissez le compte Microsoft comme fournisseur de revendications, en ajoutant le nœud `<ClaimsProvider>` à votre fichier de stratégie d’extension :</span><span class="sxs-lookup"><span data-stu-id="a2a18-157">Define Microsoft Account as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1.  <span data-ttu-id="a2a18-158">Ouvrez le fichier de stratégie d’extension hello (TrustFrameworkExtensions.xml) à partir de votre répertoire de travail.</span><span class="sxs-lookup"><span data-stu-id="a2a18-158">Open hello extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="a2a18-159">Si vous avez besoin d’un éditeur XML, [essayez Visual Studio Code](https://code.visualstudio.com/download), un éditeur multiplateforme léger.</span><span class="sxs-lookup"><span data-stu-id="a2a18-159">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2.  <span data-ttu-id="a2a18-160">Recherche hello `<ClaimsProviders>` section</span><span class="sxs-lookup"><span data-stu-id="a2a18-160">Find hello `<ClaimsProviders>` section</span></span>
3.  <span data-ttu-id="a2a18-161">Ajoutez suivant extrait de code XML sous hello `ClaimsProviders` élément :</span><span class="sxs-lookup"><span data-stu-id="a2a18-161">Add following XML snippet under hello `ClaimsProviders` element:</span></span>

    ```xml
<ClaimsProvider>
    <Domain>live.com</Domain>
    <DisplayName>Microsoft Account</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="MSA-OIDC">
        <DisplayName>Microsoft Account</DisplayName>
        <Protocol Name="OpenIdConnect" />
        <Metadata>
        <Item Key="ProviderName">https://login.live.com</Item>
        <Item Key="METADATA">https://login.live.com/.well-known/openid-configuration</Item>
        <Item Key="response_types">code</Item>
        <Item Key="response_mode">form_post</Item>
        <Item Key="scope">openid profile email</Item>
        <Item Key="HttpBinding">POST</Item>
        <Item Key="UsePolicyInRedirectUri">0</Item>
        <Item Key="client_id">Your Microsoft application client id</Item>
        </Metadata>
    <CryptographicKeys>
        <Key Id="client_secret" StorageReferenceId="B2C_1A_MSASecret" />
    </CryptographicKeys>
    <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="live.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="sub" />
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
        <OutputClaim ClaimTypeReferenceId="email" />
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName" />
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName" />
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId" />
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId" />
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-SocialLogin" />
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

4.  <span data-ttu-id="a2a18-162">Remplacez la valeur `client_id` par votre ID client d’application de compte Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a2a18-162">Replace `client_id` value with your Microsoft Account application client Id</span></span>

5.  <span data-ttu-id="a2a18-163">Enregistrez le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="a2a18-163">Save hello file.</span></span>

## <a name="register-hello-microsoft-account-claims-provider-toosign-up-or-sign-in-user-journey"></a><span data-ttu-id="a2a18-164">Inscrire tooSign de fournisseur de revendications de Account Microsoft hello haut ou connectez-vous le voyage d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="a2a18-164">Register hello Microsoft Account claims provider tooSign up or Sign-in user journey</span></span>

<span data-ttu-id="a2a18-165">À ce stade, le fournisseur d’identité hello a été configuré, mais il n’est pas disponible dans les écrans de connexion-haut/connectez-vous hello.</span><span class="sxs-lookup"><span data-stu-id="a2a18-165">At this point, hello identity provider has been set up, but it’s not available in any of hello sign-up/sign-in screens.</span></span> <span data-ttu-id="a2a18-166">Maintenant vous devez tooyour utilisateur du fournisseur tooadd hello Account Microsoft identité `SignUpOrSignIn` parcours de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a2a18-166">Now you need tooadd hello Microsoft Account identity provider tooyour user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="a2a18-167">toomake il est disponible, nous créons un doublon d’un déplacement de modèle à l’utilisateur existant.</span><span class="sxs-lookup"><span data-stu-id="a2a18-167">toomake it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="a2a18-168">Puis nous ajouter le fournisseur d’identité hello Account Microsoft :</span><span class="sxs-lookup"><span data-stu-id="a2a18-168">Then we add hello Microsoft Account identity provider:</span></span>

> [!NOTE]
>
><span data-ttu-id="a2a18-169">Si vous avez copiés précédemment hello `<UserJourneys>` élément à partir du fichier de base de votre fichier d’extension de stratégie toohello `TrustFrameworkExtensions.xml`, vous pouvez ignorer la section de toothis.</span><span class="sxs-lookup"><span data-stu-id="a2a18-169">If you previously copied hello `<UserJourneys>` element from base file of your policy toohello extension file `TrustFrameworkExtensions.xml`, you can skip toothis section.</span></span>

1.  <span data-ttu-id="a2a18-170">Ouvrez le fichier de base hello de votre stratégie (par exemple, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="a2a18-170">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="a2a18-171">Recherche hello `<UserJourneys>` élément et copie hello ensemble du contenu de `<UserJourneys>` nœud.</span><span class="sxs-lookup"><span data-stu-id="a2a18-171">Find hello `<UserJourneys>` element and copy hello entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="a2a18-172">Ouvrez le fichier d’extension hello (par exemple, TrustFrameworkExtensions.xml) et recherche hello `<UserJourneys>` élément.</span><span class="sxs-lookup"><span data-stu-id="a2a18-172">Open hello extension file (for example, TrustFrameworkExtensions.xml) and find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="a2a18-173">Si l’élément de hello n’existe pas, ajoutez-en un.</span><span class="sxs-lookup"><span data-stu-id="a2a18-173">If hello element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="a2a18-174">Coller le contenu entier de hello de `<UserJournesy>` nœud que vous avez copié en tant qu’enfant de hello `<UserJourneys>` élément.</span><span class="sxs-lookup"><span data-stu-id="a2a18-174">Paste hello entire content of `<UserJournesy>` node that you copied as a child of hello `<UserJourneys>` element.</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="a2a18-175">Bouton d’affichage hello</span><span class="sxs-lookup"><span data-stu-id="a2a18-175">Display hello button</span></span>
<span data-ttu-id="a2a18-176">Hello `<ClaimsProviderSelections>` élément définit la liste hello des options de sélection de fournisseur de revendications et leur ordre.</span><span class="sxs-lookup"><span data-stu-id="a2a18-176">hello `<ClaimsProviderSelections>` element defines hello list of claims provider selection options and their order.</span></span>  <span data-ttu-id="a2a18-177">`<ClaimsProviderSelection>`élément est un bouton de fournisseur d’identité tooan analogue sur une connexion-haut/page de connexion.</span><span class="sxs-lookup"><span data-stu-id="a2a18-177">`<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="a2a18-178">Si vous ajoutez un `<ClaimsProviderSelection>` élément pour le compte Microsoft, un nouveau bouton apparaît lorsqu’un utilisateur arrive sur la page de hello.</span><span class="sxs-lookup"><span data-stu-id="a2a18-178">If you add a `<ClaimsProviderSelection>` element for Microsoft account, a new button shows up when a user lands on hello page.</span></span> <span data-ttu-id="a2a18-179">tooadd cet élément :</span><span class="sxs-lookup"><span data-stu-id="a2a18-179">tooadd this element:</span></span>

1.  <span data-ttu-id="a2a18-180">Recherche hello `<UserJourney>` nœud incluant `Id="SignUpOrSignIn"` dans voyage utilisateur hello que vous avez copiée.</span><span class="sxs-lookup"><span data-stu-id="a2a18-180">Find hello `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in hello user journey that you copied.</span></span>
2.  <span data-ttu-id="a2a18-181">Recherchez hello `<OrchestrationStep>` nœud qui inclut`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="a2a18-181">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="a2a18-182">Ajoutez l’extrait de code XML suivant sous le nœud `<ClaimsProviderSelections>` :</span><span class="sxs-lookup"><span data-stu-id="a2a18-182">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="a2a18-183">Action de lien hello bouton tooan</span><span class="sxs-lookup"><span data-stu-id="a2a18-183">Link hello button tooan action</span></span>
<span data-ttu-id="a2a18-184">Maintenant que vous avez un bouton en place, vous devez toolink il tooan action.</span><span class="sxs-lookup"><span data-stu-id="a2a18-184">Now that you have a button in place, you need toolink it tooan action.</span></span> <span data-ttu-id="a2a18-185">action de Hello, dans ce cas, est de toocommunicate Azure AD B2C avec Microsoft Account tooreceive un jeton.</span><span class="sxs-lookup"><span data-stu-id="a2a18-185">hello action, in this case, is for Azure AD B2C toocommunicate with Microsoft Account tooreceive a token.</span></span> <span data-ttu-id="a2a18-186">Lier action tooan du bouton hello en liant le profil de technique hello pour votre fournisseur de revendications Account Microsoft :</span><span class="sxs-lookup"><span data-stu-id="a2a18-186">Link hello button tooan action by linking hello technical profile for your Microsoft Account claims provider:</span></span>

1.  <span data-ttu-id="a2a18-187">Recherche hello `<OrchestrationStep>` qui inclut `Order="2"` Bonjour `<UserJourney>` nœud.</span><span class="sxs-lookup"><span data-stu-id="a2a18-187">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="a2a18-188">Ajoutez l’extrait de code XML suivant sous le nœud `<ClaimsExchanges>` :</span><span class="sxs-lookup"><span data-stu-id="a2a18-188">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

> [!NOTE]
>
>   * <span data-ttu-id="a2a18-189">Assurez-vous de hello `Id` a hello même valeur que celle de `TargetClaimsExchangeId` Bonjour précédant la section</span><span class="sxs-lookup"><span data-stu-id="a2a18-189">Ensure hello `Id` has hello same value as that of `TargetClaimsExchangeId` in hello preceding section</span></span>
>   * <span data-ttu-id="a2a18-190">Vérifiez `TechnicalProfileReferenceId` ID a la valeur toohello de profil technique vous avez créé plus haut (MSA OIDC).</span><span class="sxs-lookup"><span data-stu-id="a2a18-190">Ensure `TechnicalProfileReferenceId` ID is set toohello technical profile you created earlier (MSA-OIDC).</span></span>

## <a name="upload-hello-policy-tooyour-tenant"></a><span data-ttu-id="a2a18-191">Télécharger le client de tooyour stratégie hello</span><span class="sxs-lookup"><span data-stu-id="a2a18-191">Upload hello policy tooyour tenant</span></span>
1.  <span data-ttu-id="a2a18-192">Bonjour [portail Azure](https://portal.azure.com), basculez dans hello [contexte de votre locataire Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md)et ouvrez hello **Azure AD B2C** panneau.</span><span class="sxs-lookup"><span data-stu-id="a2a18-192">In hello [Azure portal](https://portal.azure.com), switch into hello [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open hello **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="a2a18-193">Sélectionnez **Infrastructure d’expérience d’identité**.</span><span class="sxs-lookup"><span data-stu-id="a2a18-193">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="a2a18-194">Ouvrez hello **toutes les stratégies** panneau.</span><span class="sxs-lookup"><span data-stu-id="a2a18-194">Open hello **All Policies** blade.</span></span>
4.  <span data-ttu-id="a2a18-195">Sélectionnez **Charger la stratégie**.</span><span class="sxs-lookup"><span data-stu-id="a2a18-195">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="a2a18-196">Vérifiez **remplacer la stratégie de hello si elle existe** boîte.</span><span class="sxs-lookup"><span data-stu-id="a2a18-196">Check **Overwrite hello policy if it exists** box.</span></span>
6.  <span data-ttu-id="a2a18-197">**Télécharger** TrustFrameworkExtensions.xml et assurez-vous qu’il validation n’échoue pas hello</span><span class="sxs-lookup"><span data-stu-id="a2a18-197">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail hello validation</span></span>

## <a name="test-hello-custom-policy-by-using-run-now"></a><span data-ttu-id="a2a18-198">Tester une stratégie personnalisée de hello à l’aide d’exécuter maintenant</span><span class="sxs-lookup"><span data-stu-id="a2a18-198">Test hello custom policy by using Run Now</span></span>

1.  <span data-ttu-id="a2a18-199">Ouvrez **paramètres d’Azure AD B2C** et accédez trop**infrastructure d’identité expérience**.</span><span class="sxs-lookup"><span data-stu-id="a2a18-199">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
> [!NOTE]
>
><span data-ttu-id="a2a18-200">**Exécutez maintenant** requiert au moins une application toobe préinscrites sur le client de hello.</span><span class="sxs-lookup"><span data-stu-id="a2a18-200">**Run now** requires at least one application toobe preregistered on hello tenant.</span></span> <span data-ttu-id="a2a18-201">toolearn tooregister applications, voir hello Azure AD B2C [prise en main](active-directory-b2c-get-started.md) article ou hello [inscription d’Application](active-directory-b2c-app-registration.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="a2a18-201">toolearn how tooregister applications, see hello Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or hello [Application registration](active-directory-b2c-app-registration.md) article.</span></span>
2.  <span data-ttu-id="a2a18-202">Ouvrez **B2C_1A_signup_signin**, hello stratégie personnalisée partie de confiance (RP) de tiers que vous avez téléchargé.</span><span class="sxs-lookup"><span data-stu-id="a2a18-202">Open **B2C_1A_signup_signin**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="a2a18-203">Sélectionnez **Exécuter maintenant**.</span><span class="sxs-lookup"><span data-stu-id="a2a18-203">Select **Run now**.</span></span>
3.  <span data-ttu-id="a2a18-204">Vous devez être en mesure de toosign à l’aide du compte Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a2a18-204">You should be able toosign in using Microsoft account.</span></span>

## <a name="optional-register-hello-microsoft-account-claims-provider-tooprofile-edit-user-journey"></a><span data-ttu-id="a2a18-205">[Facultatif] Inscrire le parcours de hello Account Microsoft revendications fournisseur tooProfile-Modifier utilisateur</span><span class="sxs-lookup"><span data-stu-id="a2a18-205">[Optional] Register hello Microsoft Account claims provider tooProfile-Edit user journey</span></span>
<span data-ttu-id="a2a18-206">Vous pouvez souhaiter fournisseur d’identité Microsoft Account tooadd hello également tooyour utilisateur `ProfileEdit` parcours de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a2a18-206">You may want tooadd hello Microsoft Account identity provider also tooyour user `ProfileEdit` user journey.</span></span> <span data-ttu-id="a2a18-207">toomake disponibles, nous Répétez hello a deux étapes :</span><span class="sxs-lookup"><span data-stu-id="a2a18-207">toomake it available, we repeat hello last two steps:</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="a2a18-208">Bouton d’affichage hello</span><span class="sxs-lookup"><span data-stu-id="a2a18-208">Display hello button</span></span>
1.  <span data-ttu-id="a2a18-209">Ouvrez le fichier d’extension hello de votre stratégie (par exemple, TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="a2a18-209">Open hello extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="a2a18-210">Recherche hello `<UserJourney>` nœud incluant `Id="ProfileEdit"` dans voyage utilisateur hello que vous avez copiée.</span><span class="sxs-lookup"><span data-stu-id="a2a18-210">Find hello `<UserJourney>` node that includes `Id="ProfileEdit"` in hello user journey that you copied.</span></span>
3.  <span data-ttu-id="a2a18-211">Recherchez hello `<OrchestrationStep>` nœud qui inclut`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="a2a18-211">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="a2a18-212">Ajoutez l’extrait de code XML suivant sous le nœud `<ClaimsProviderSelections>` :</span><span class="sxs-lookup"><span data-stu-id="a2a18-212">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="a2a18-213">Action de lien hello bouton tooan</span><span class="sxs-lookup"><span data-stu-id="a2a18-213">Link hello button tooan action</span></span>
1.  <span data-ttu-id="a2a18-214">Recherche hello `<OrchestrationStep>` qui inclut `Order="2"` Bonjour `<UserJourney>` nœud.</span><span class="sxs-lookup"><span data-stu-id="a2a18-214">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="a2a18-215">Ajoutez l’extrait de code XML suivant sous le nœud `<ClaimsExchanges>` :</span><span class="sxs-lookup"><span data-stu-id="a2a18-215">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="a2a18-216">Tester une stratégie de profil de modification personnalisée hello à l’aide d’exécuter maintenant</span><span class="sxs-lookup"><span data-stu-id="a2a18-216">Test hello custom Profile-Edit policy by using Run Now</span></span>
1.  <span data-ttu-id="a2a18-217">Ouvrez **paramètres d’Azure AD B2C** et accédez trop**infrastructure d’identité expérience**.</span><span class="sxs-lookup"><span data-stu-id="a2a18-217">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="a2a18-218">Ouvrez **B2C_1A_ProfileEdit**, hello stratégie personnalisée partie de confiance (RP) de tiers que vous avez téléchargé.</span><span class="sxs-lookup"><span data-stu-id="a2a18-218">Open **B2C_1A_ProfileEdit**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="a2a18-219">Sélectionnez **Exécuter maintenant**.</span><span class="sxs-lookup"><span data-stu-id="a2a18-219">Select **Run now**.</span></span>
3.  <span data-ttu-id="a2a18-220">Vous devez être en mesure de toosign à l’aide du compte Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a2a18-220">You should be able toosign in using Microsoft account.</span></span>

## <a name="download-hello-complete-policy-files"></a><span data-ttu-id="a2a18-221">Télécharger les fichiers de stratégie complète hello</span><span class="sxs-lookup"><span data-stu-id="a2a18-221">Download hello complete policy files</span></span>
<span data-ttu-id="a2a18-222">Facultatif : Nous vous recommandons de que générer votre scénario à l’aide de vos propres fichiers de stratégie personnalisée hello prise en main des stratégies personnalisées guident au lieu d’utiliser ces exemples de fichiers à la fin.</span><span class="sxs-lookup"><span data-stu-id="a2a18-222">Optional: We recommend you build your scenario using your own Custom policy files after completing hello Getting Started with Custom Policies walk through instead of using these sample files.</span></span>  [<span data-ttu-id="a2a18-223">Exemples de fichiers de stratégie de référence</span><span class="sxs-lookup"><span data-stu-id="a2a18-223">Sample policy files for reference</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-msa-app)
