---
title: "Azure Active Directory B2C : Ajout de Google+ en tant que fournisseur d’identités OAuth2 à l’aide de stratégies personnalisées"
description: "Exemple d’utilisation de Google+ en tant que fournisseur d’identité à l’aide du protocole OAuth2"
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
ms.openlocfilehash: 4feff21979c9c3b3b12c7a1cae4db0121d1bd79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-google-as-an-oauth2-identity-provider-using-custom-policies"></a><span data-ttu-id="6be48-103">Azure Active Directory B2C : Ajout de Google+ en tant que fournisseur d’identités OAuth2 à l’aide de stratégies personnalisées</span><span class="sxs-lookup"><span data-stu-id="6be48-103">Azure Active Directory B2C: Add Google+ as an OAuth2 identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="6be48-104">Ce guide vous explique comment tooenable connectez-vous pour les utilisateurs à partir de Google + compte via l’utilisation de hello de [des stratégies personnalisées](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="6be48-104">This guide shows you how tooenable sign-in for users from Google+ account through hello use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6be48-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="6be48-105">Prerequisites</span></span>

<span data-ttu-id="6be48-106">Hello terminé les étapes Bonjour [mise en route avec les stratégies personnalisées](active-directory-b2c-get-started-custom.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="6be48-106">Complete hello steps in hello [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="6be48-107">Ces étapes sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="6be48-107">These steps include:</span></span>

1.  <span data-ttu-id="6be48-108">Création d’une application de compte Google+.</span><span class="sxs-lookup"><span data-stu-id="6be48-108">Creating a Google+ account application.</span></span>
2.  <span data-ttu-id="6be48-109">Ajout de hello Google + compte application clé tooAzure AD B2C</span><span class="sxs-lookup"><span data-stu-id="6be48-109">Adding hello Google+ account application key tooAzure AD B2C</span></span>
3.  <span data-ttu-id="6be48-110">Ajout d’une stratégie de tooa de fournisseur de revendications</span><span class="sxs-lookup"><span data-stu-id="6be48-110">Adding claims provider tooa policy</span></span>
4.  <span data-ttu-id="6be48-111">L’inscription hello Google + compte revendications fournisseur tooa utilisateur voyage</span><span class="sxs-lookup"><span data-stu-id="6be48-111">Registering hello Google+ account claims provider tooa user journey</span></span>
5.  <span data-ttu-id="6be48-112">Téléchargement de stratégie de hello tooan Azure AD B2C de client et de le tester</span><span class="sxs-lookup"><span data-stu-id="6be48-112">Uploading hello policy tooan Azure AD B2C tenant and test it</span></span>

## <a name="create-a-google-account-application"></a><span data-ttu-id="6be48-113">Création d’une application de compte Google+</span><span class="sxs-lookup"><span data-stu-id="6be48-113">Create a Google+ account application</span></span>
<span data-ttu-id="6be48-114">toouse + Google comme fournisseur d’identité dans Azure Active Directory (Azure AD) B2C, vous devez toocreate une application Google + et lui fournir les paramètres appropriés hello.</span><span class="sxs-lookup"><span data-stu-id="6be48-114">toouse Google+ as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Google+ application and supply it with hello right parameters.</span></span> <span data-ttu-id="6be48-115">Vous pouvez inscrire une application Google+ ici : [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp)</span><span class="sxs-lookup"><span data-stu-id="6be48-115">You can register a Google+ application here: [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp)</span></span>

1.  <span data-ttu-id="6be48-116">Accédez toohello [Console des développeurs Google](https://console.developers.google.com/) et connectez-vous avec vos informations d’identification compte Google +.</span><span class="sxs-lookup"><span data-stu-id="6be48-116">Go toohello [Google Developers Console](https://console.developers.google.com/) and sign in with your Google+ account credentials.</span></span>
2.  <span data-ttu-id="6be48-117">Cliquez sur **Créer un projet**, saisissez un **nom de projet**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="6be48-117">Click **Create project**, enter a **Project name**, and then click **Create**.</span></span>

3.  <span data-ttu-id="6be48-118">Cliquez sur hello **menu projets**.</span><span class="sxs-lookup"><span data-stu-id="6be48-118">Click on hello **Projects menu**.</span></span>

    ![Compte Google+ - Sélectionner le projet](media/active-directory-b2c-custom-setup-goog-idp/goog-add-new-app1.png)

4.  <span data-ttu-id="6be48-120">Cliquez sur hello  **+**  bouton.</span><span class="sxs-lookup"><span data-stu-id="6be48-120">Click on hello **+** button.</span></span>

    ![Compte Google+ - Créer un nouveau projet](media/active-directory-b2c-custom-setup-goog-idp//goog-add-new-app2.png)

5.  <span data-ttu-id="6be48-122">Entrez un **Nom de projet**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="6be48-122">Enter a **Project name**, and then click **Create**.</span></span>

    ![Compte Google+ : Nouveau projet](media/active-directory-b2c-custom-setup-goog-idp//goog-app-name.png)

6.  <span data-ttu-id="6be48-124">Attendez que le projet de hello est prêt, cliquez sur hello **menu projets**.</span><span class="sxs-lookup"><span data-stu-id="6be48-124">Wait until hello project is ready and click on hello **Projects menu**.</span></span>

    ![Compte Google + - en attente jusqu'à ce que le nouveau projet est prêt toouse](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app1.png)

7.  <span data-ttu-id="6be48-126">Cliquez sur le nom de votre projet.</span><span class="sxs-lookup"><span data-stu-id="6be48-126">Click on your project name.</span></span>

    ![Compte Google + - projet hello Select](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app2.png)

8.  <span data-ttu-id="6be48-128">Cliquez sur **API Manager** puis cliquez sur **informations d’identification** Bonjour barre de navigation gauche.</span><span class="sxs-lookup"><span data-stu-id="6be48-128">Click **API Manager** and then click **Credentials** in hello left navigation.</span></span>
9.  <span data-ttu-id="6be48-129">Cliquez sur hello **écran de consentement OAuth** onglet en haut de hello.</span><span class="sxs-lookup"><span data-stu-id="6be48-129">Click hello **OAuth consent screen** tab at hello top.</span></span>

    ![Compte Google+ - Définition de l’écran de consentement OAuth](media/active-directory-b2c-custom-setup-goog-idp/goog-add-cred.png)

10.  <span data-ttu-id="6be48-131">Sélectionnez ou spécifiez une valeur valide pour **Adresse de messagerie**, fournissez une valeur pour **Nom de produit**, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="6be48-131">Select or specify a valid **Email address**, provide a **Product name**, and click **Save**.</span></span>

    ![Google+ - Informations d’identification de l’application](media/active-directory-b2c-custom-setup-goog-idp/goog-consent-screen.png)

11.  <span data-ttu-id="6be48-133">Cliquez sur **Nouvelles informations d’identification**, puis sur **ID client OAuth**.</span><span class="sxs-lookup"><span data-stu-id="6be48-133">Click **New credentials** and then choose **OAuth client ID**.</span></span>

    ![Google+ - Créer de nouvelles informations d’identification d’application](media/active-directory-b2c-custom-setup-goog-idp/goog-add-oauth2-client-id.png)

12.  <span data-ttu-id="6be48-135">Sous **Type d’application**, sélectionnez **Application web**.</span><span class="sxs-lookup"><span data-stu-id="6be48-135">Under **Application type**, select **Web application**.</span></span>

    ![Google+ - Sélectionner un type d’application](media/active-directory-b2c-custom-setup-goog-idp/goog-web-app.png)

13.  <span data-ttu-id="6be48-137">Fournir un **nom** pour votre application, entrez `https://login.microsoftonline.com` Bonjour **autorisé de JavaScript origines** champ, et `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` Bonjour **autorisés rediriger URI**champ.</span><span class="sxs-lookup"><span data-stu-id="6be48-137">Provide a **Name** for your application, enter `https://login.microsoftonline.com` in hello **Authorized JavaScript origins** field, and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Authorized redirect URIs** field.</span></span> <span data-ttu-id="6be48-138">Remplacez **{tenant}** par votre nom de client (par exemple, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="6be48-138">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="6be48-139">Hello **{tenant}** valeur respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="6be48-139">hello **{tenant}** value is case-sensitive.</span></span> <span data-ttu-id="6be48-140">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="6be48-140">Click **Create**.</span></span>

    ![Google+ - Fournir les origines autorisées de JavaScript et les URI de redirection](media/active-directory-b2c-custom-setup-goog-idp/goog-create-client-id.png)

14.  <span data-ttu-id="6be48-142">Copier les valeurs hello de **Id Client** et **clé secrète Client**.</span><span class="sxs-lookup"><span data-stu-id="6be48-142">Copy hello values of **Client Id** and **Client secret**.</span></span> <span data-ttu-id="6be48-143">Vous devez les deux tooconfigure Google + comme fournisseur d’identité dans votre client.</span><span class="sxs-lookup"><span data-stu-id="6be48-143">You need both tooconfigure Google+ as an identity provider in your tenant.</span></span> <span data-ttu-id="6be48-144">**Client secret** est une information d’identification de sécurité importante.</span><span class="sxs-lookup"><span data-stu-id="6be48-144">**Client secret** is an important security credential.</span></span>

    ![Google + - valeurs hello de copie de la clé secrète du Client et Id de client](media/active-directory-b2c-custom-setup-goog-idp/goog-client-secret.png)

## <a name="add-hello-google-account-application-key-tooazure-ad-b2c"></a><span data-ttu-id="6be48-146">Ajouter hello Google + compte application clé tooAzure AD B2C</span><span class="sxs-lookup"><span data-stu-id="6be48-146">Add hello Google+ account application key tooAzure AD B2C</span></span>
<span data-ttu-id="6be48-147">Fédération avec Google + comptes requiert une clé secrète client pour Google + compte tootrust Azure AD B2C au nom de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="6be48-147">Federation with Google+ accounts requires a client secret for Google+ account tootrust Azure AD B2C on behalf of hello application.</span></span> <span data-ttu-id="6be48-148">Vous devez toostore votre secret d’application Google + dans Azure AD B2C client :</span><span class="sxs-lookup"><span data-stu-id="6be48-148">You need toostore your Google+ application secret in Azure AD B2C tenant:</span></span>  

1.  <span data-ttu-id="6be48-149">Accédez tooyour Azure AD B2C client, puis sélectionnez **B2C paramètres** > **infrastructure expérience d’identité**</span><span class="sxs-lookup"><span data-stu-id="6be48-149">Go tooyour Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="6be48-150">Sélectionnez **clés de stratégie** tooview hello disponibles dans votre client.</span><span class="sxs-lookup"><span data-stu-id="6be48-150">Select **Policy Keys** tooview hello keys available in your tenant.</span></span>
3.  <span data-ttu-id="6be48-151">Cliquez sur **+Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="6be48-151">Click **+Add**.</span></span>
4.  <span data-ttu-id="6be48-152">Pour **Options**, utilisez **Manuel**.</span><span class="sxs-lookup"><span data-stu-id="6be48-152">For **Options**, use **Manual**.</span></span>
5.  <span data-ttu-id="6be48-153">Pour **Nom**, utilisez `GoogleSecret`.</span><span class="sxs-lookup"><span data-stu-id="6be48-153">For **Name**, use `GoogleSecret`.</span></span>  
    <span data-ttu-id="6be48-154">préfixe de Hello `B2C_1A_` peuvent être ajoutées automatiquement.</span><span class="sxs-lookup"><span data-stu-id="6be48-154">hello prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="6be48-155">Bonjour **Secret** , entrez votre clé secrète d’application Microsoft à partir de https://apps.dev.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="6be48-155">In hello **Secret** box, enter your Microsoft application secret from https://apps.dev.microsoft.com</span></span>
7.  <span data-ttu-id="6be48-156">Pour **Utilisation de la clé**, utilisez **Signature**.</span><span class="sxs-lookup"><span data-stu-id="6be48-156">For **Key usage**, use **Signature**.</span></span>
8.  <span data-ttu-id="6be48-157">Cliquez sur **Créer**</span><span class="sxs-lookup"><span data-stu-id="6be48-157">Click **Create**</span></span>
9.  <span data-ttu-id="6be48-158">Vérifiez que vous avez créé la clé de hello `B2C_1A_GoogleSecret`.</span><span class="sxs-lookup"><span data-stu-id="6be48-158">Confirm that you've created hello key `B2C_1A_GoogleSecret`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="6be48-159">Ajouter un fournisseur de revendications à une stratégie d’extension</span><span class="sxs-lookup"><span data-stu-id="6be48-159">Add a claims provider in your extension policy</span></span>

<span data-ttu-id="6be48-160">Si vous souhaitez que les utilisateurs toosign à l’aide du compte Google +, vous devez toodefine Google + compte comme un fournisseur de revendications.</span><span class="sxs-lookup"><span data-stu-id="6be48-160">If you want users toosign in by using Google+ account, you need toodefine Google+ account as a claims provider.</span></span> <span data-ttu-id="6be48-161">En d’autres termes, vous devez toospecify un point de terminaison Azure AD B2C communique avec.</span><span class="sxs-lookup"><span data-stu-id="6be48-161">In other words, you need toospecify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="6be48-162">point de terminaison Hello fournit un ensemble de revendications qui sont utilisées par Azure AD B2C tooverify authentifié un utilisateur spécifique.</span><span class="sxs-lookup"><span data-stu-id="6be48-162">hello endpoint provides a set of claims that are used by Azure AD B2C tooverify that a specific user has authenticated.</span></span>

<span data-ttu-id="6be48-163">Définissez le compte Google+ comme fournisseur de revendications, en ajoutant le nœud `<ClaimsProvider>` dans votre fichier de stratégie d’extension :</span><span class="sxs-lookup"><span data-stu-id="6be48-163">Define Google+ Account as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1.  <span data-ttu-id="6be48-164">Ouvrez le fichier de stratégie d’extension hello (TrustFrameworkExtensions.xml) à partir de votre répertoire de travail.</span><span class="sxs-lookup"><span data-stu-id="6be48-164">Open hello extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="6be48-165">Si vous avez besoin d’un éditeur XML, [essayez Visual Studio Code](https://code.visualstudio.com/download), un éditeur multiplateforme léger.</span><span class="sxs-lookup"><span data-stu-id="6be48-165">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2.  <span data-ttu-id="6be48-166">Recherche hello `<ClaimsProviders>` section</span><span class="sxs-lookup"><span data-stu-id="6be48-166">Find hello `<ClaimsProviders>` section</span></span>
3.  <span data-ttu-id="6be48-167">Ajouter hello suivant extrait de code XML sous hello `ClaimsProviders` élément et remplacer `client_id` valeur avec votre ID de client application compte Google + avant d’enregistrer le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="6be48-167">Add hello following XML snippet under hello `ClaimsProviders` element and replace `client_id` value with your Google+ account application client ID before saving hello file.</span></span>  

```xml
<ClaimsProvider>
    <Domain>google.com</Domain>
    <DisplayName>Google</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="Google-OAUTH">
        <DisplayName>Google</DisplayName>
        <Protocol Name="OAuth2" />
        <Metadata>
        <Item Key="ProviderName">google</Item>
        <Item Key="authorization_endpoint">https://accounts.google.com/o/oauth2/auth</Item>
        <Item Key="AccessTokenEndpoint">https://accounts.google.com/o/oauth2/token</Item>
        <Item Key="ClaimsEndpoint">https://www.googleapis.com/oauth2/v1/userinfo</Item>
        <Item Key="scope">email</Item>
        <Item Key="HttpBinding">POST</Item>
        <Item Key="UsePolicyInRedirectUri">0</Item>
        <Item Key="client_id">Your Google+ application ID</Item>
        </Metadata>
        <CryptographicKeys>
        <Key Id="client_secret" StorageReferenceId="B2C_1A_GoogleSecret" />
        </CryptographicKeys>
        <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="id" />
        <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email" />
        <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name" />
        <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name" />
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="google.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName" />
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName" />
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId" />
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId" />
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-SocialLogin" />
        <ErrorHandlers>
        <ErrorHandler>
            <ErrorResponseFormat>json</ErrorResponseFormat>
            <ResponseMatch>$[?(@@.error == 'invalid_grant')]</ResponseMatch>
            <Action>Reauthenticate</Action>
            <!--In case of authorization code used error, we don't want hello user tooselect his account again.-->
            <!--AdditionalRequestParameters Key="prompt">select_account</AdditionalRequestParameters-->
        </ErrorHandler>
        </ErrorHandlers>
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

## <a name="register-hello-google-account-claims-provider-toosign-up-or-sign-in-user-journey"></a><span data-ttu-id="6be48-168">Inscrire hello Google + compte revendications fournisseur tooSign des ou connectez-vous de parcours de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="6be48-168">Register hello Google+ account claims provider tooSign up or Sign in user journey</span></span>

<span data-ttu-id="6be48-169">fournisseur d’identité Hello a été configuré.</span><span class="sxs-lookup"><span data-stu-id="6be48-169">hello identity provider has been set up.</span></span>  <span data-ttu-id="6be48-170">Toutefois, il n’est pas disponible dans les écrans de connexion-haut/connectez-vous hello.</span><span class="sxs-lookup"><span data-stu-id="6be48-170">However, it is not available in any of hello sign-up/sign-in screens.</span></span> <span data-ttu-id="6be48-171">Ajouter hello Google + compte fournisseur tooyour utilisateur de l’identité `SignUpOrSignIn` parcours de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6be48-171">Add hello Google+ account identity provider tooyour user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="6be48-172">toomake il est disponible, nous créons un doublon d’un déplacement de modèle à l’utilisateur existant.</span><span class="sxs-lookup"><span data-stu-id="6be48-172">toomake it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="6be48-173">Puis nous ajouter hello Google + fournisseur d’identité du compte :</span><span class="sxs-lookup"><span data-stu-id="6be48-173">Then we add hello Google+ account identity provider:</span></span>

>[!NOTE]
>
><span data-ttu-id="6be48-174">Si vous avez copié hello `<UserJourneys>` élément à partir du fichier de base de votre fichier d’extension de stratégie toohello (TrustFrameworkExtensions.xml), vous pouvez ignorer toothis section.</span><span class="sxs-lookup"><span data-stu-id="6be48-174">If you copied hello `<UserJourneys>` element from base file of your policy toohello extension file (TrustFrameworkExtensions.xml), you can skip toothis section.</span></span>

1.  <span data-ttu-id="6be48-175">Ouvrez le fichier de base hello de votre stratégie (par exemple, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="6be48-175">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="6be48-176">Recherche hello `<UserJourneys>` élément et copie hello ensemble du contenu de `<UserJourneys>` nœud.</span><span class="sxs-lookup"><span data-stu-id="6be48-176">Find hello `<UserJourneys>` element and copy hello entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="6be48-177">Ouvrez le fichier d’extension hello (par exemple, TrustFrameworkExtensions.xml) et recherche hello `<UserJourneys>` élément.</span><span class="sxs-lookup"><span data-stu-id="6be48-177">Open hello extension file (for example, TrustFrameworkExtensions.xml) and find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="6be48-178">Si l’élément de hello n’existe pas, ajoutez-en un.</span><span class="sxs-lookup"><span data-stu-id="6be48-178">If hello element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="6be48-179">Coller le contenu entier de hello de `<UserJournesy>` nœud que vous avez copié en tant qu’enfant de hello `<UserJourneys>` élément.</span><span class="sxs-lookup"><span data-stu-id="6be48-179">Paste hello entire content of `<UserJournesy>` node that you copied as a child of hello `<UserJourneys>` element.</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="6be48-180">Bouton d’affichage hello</span><span class="sxs-lookup"><span data-stu-id="6be48-180">Display hello button</span></span>
<span data-ttu-id="6be48-181">Hello `<ClaimsProviderSelections>` élément définit la liste hello des options de sélection de fournisseur de revendications et leur ordre.</span><span class="sxs-lookup"><span data-stu-id="6be48-181">hello `<ClaimsProviderSelections>` element defines hello list of claims provider selection options and their order.</span></span>  <span data-ttu-id="6be48-182">`<ClaimsProviderSelection>`élément est un bouton de fournisseur d’identité tooan analogue sur une connexion-haut/page de connexion.</span><span class="sxs-lookup"><span data-stu-id="6be48-182">`<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="6be48-183">Si vous ajoutez un `<ClaimsProviderSelection>` élément compte Google +, un nouveau bouton apparaît lorsqu’un utilisateur arrive sur la page de hello.</span><span class="sxs-lookup"><span data-stu-id="6be48-183">If you add a `<ClaimsProviderSelection>` element for Google+ account, a new button shows up when a user lands on hello page.</span></span> <span data-ttu-id="6be48-184">tooadd cet élément :</span><span class="sxs-lookup"><span data-stu-id="6be48-184">tooadd this element:</span></span>

1.  <span data-ttu-id="6be48-185">Recherche hello `<UserJourney>` nœud incluant `Id="SignUpOrSignIn"` dans voyage utilisateur hello que vous avez copiée.</span><span class="sxs-lookup"><span data-stu-id="6be48-185">Find hello `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in hello user journey that you copied.</span></span>
2.  <span data-ttu-id="6be48-186">Recherchez hello `<OrchestrationStep>` nœud qui inclut`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="6be48-186">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="6be48-187">Ajoutez l’extrait de code XML suivant sous le nœud `<ClaimsProviderSelections>` :</span><span class="sxs-lookup"><span data-stu-id="6be48-187">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="6be48-188">Action de lien hello bouton tooan</span><span class="sxs-lookup"><span data-stu-id="6be48-188">Link hello button tooan action</span></span>
<span data-ttu-id="6be48-189">Maintenant que vous avez un bouton en place, vous devez toolink il tooan action.</span><span class="sxs-lookup"><span data-stu-id="6be48-189">Now that you have a button in place, you need toolink it tooan action.</span></span> <span data-ttu-id="6be48-190">action de Hello, dans ce cas, est de toocommunicate Azure AD B2C avec Google + compte tooreceive un jeton.</span><span class="sxs-lookup"><span data-stu-id="6be48-190">hello action, in this case, is for Azure AD B2C toocommunicate with Google+ account tooreceive a token.</span></span>

1.  <span data-ttu-id="6be48-191">Recherche hello `<OrchestrationStep>` qui inclut `Order="2"` Bonjour `<UserJourney>` nœud.</span><span class="sxs-lookup"><span data-stu-id="6be48-191">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="6be48-192">Ajoutez l’extrait de code XML suivant sous le nœud `<ClaimsExchanges>` :</span><span class="sxs-lookup"><span data-stu-id="6be48-192">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

>[!NOTE]
>
> * <span data-ttu-id="6be48-193">Assurez-vous de hello `Id` a hello même valeur que celle de `TargetClaimsExchangeId` Bonjour précédant la section</span><span class="sxs-lookup"><span data-stu-id="6be48-193">Ensure hello `Id` has hello same value as that of `TargetClaimsExchangeId` in hello preceding section</span></span>
> * <span data-ttu-id="6be48-194">Vérifiez `TechnicalProfileReferenceId` ID a la valeur toohello de profil technique vous avez créé plus haut (Google OAUTH).</span><span class="sxs-lookup"><span data-stu-id="6be48-194">Ensure `TechnicalProfileReferenceId` ID is set toohello technical profile you created earlier (Google-OAUTH).</span></span>

## <a name="upload-hello-policy-tooyour-tenant"></a><span data-ttu-id="6be48-195">Télécharger le client de tooyour stratégie hello</span><span class="sxs-lookup"><span data-stu-id="6be48-195">Upload hello policy tooyour tenant</span></span>
1.  <span data-ttu-id="6be48-196">Bonjour [portail Azure](https://portal.azure.com), basculez dans hello [contexte de votre locataire Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md)et ouvrez hello **Azure AD B2C** panneau.</span><span class="sxs-lookup"><span data-stu-id="6be48-196">In hello [Azure portal](https://portal.azure.com), switch into hello [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open hello **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="6be48-197">Sélectionnez **Infrastructure d’expérience d’identité**.</span><span class="sxs-lookup"><span data-stu-id="6be48-197">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="6be48-198">Ouvrez hello **toutes les stratégies** panneau.</span><span class="sxs-lookup"><span data-stu-id="6be48-198">Open hello **All Policies** blade.</span></span>
4.  <span data-ttu-id="6be48-199">Sélectionnez **Charger la stratégie**.</span><span class="sxs-lookup"><span data-stu-id="6be48-199">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="6be48-200">Vérifiez **remplacer la stratégie de hello si elle existe** boîte.</span><span class="sxs-lookup"><span data-stu-id="6be48-200">Check **Overwrite hello policy if it exists** box.</span></span>
6.  <span data-ttu-id="6be48-201">**Télécharger** TrustFrameworkExtensions.xml et assurez-vous qu’il validation n’échoue pas hello</span><span class="sxs-lookup"><span data-stu-id="6be48-201">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail hello validation</span></span>

## <a name="test-hello-custom-policy-by-using-run-now"></a><span data-ttu-id="6be48-202">Tester une stratégie personnalisée de hello à l’aide d’exécuter maintenant</span><span class="sxs-lookup"><span data-stu-id="6be48-202">Test hello custom policy by using Run Now</span></span>
1.  <span data-ttu-id="6be48-203">Ouvrez **paramètres d’Azure AD B2C** et accédez trop**infrastructure d’identité expérience**.</span><span class="sxs-lookup"><span data-stu-id="6be48-203">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>

    >[!NOTE]
    >
    >    <span data-ttu-id="6be48-204">**Exécutez maintenant** requiert au moins une application toobe préinscrites sur le client de hello.</span><span class="sxs-lookup"><span data-stu-id="6be48-204">**Run now** requires at least one application toobe preregistered on hello tenant.</span></span> 
    >    <span data-ttu-id="6be48-205">toolearn tooregister applications, voir hello Azure AD B2C [prise en main](active-directory-b2c-get-started.md) article ou hello [inscription d’Application](active-directory-b2c-app-registration.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="6be48-205">toolearn how tooregister applications, see hello Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or hello [Application registration](active-directory-b2c-app-registration.md) article.</span></span>


2.  <span data-ttu-id="6be48-206">Ouvrez **B2C_1A_signup_signin**, hello stratégie personnalisée partie de confiance (RP) de tiers que vous avez téléchargé.</span><span class="sxs-lookup"><span data-stu-id="6be48-206">Open **B2C_1A_signup_signin**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="6be48-207">Sélectionnez **Exécuter maintenant**.</span><span class="sxs-lookup"><span data-stu-id="6be48-207">Select **Run now**.</span></span>
3.  <span data-ttu-id="6be48-208">Vous devez être en mesure de toosign à l’aide du compte Google +.</span><span class="sxs-lookup"><span data-stu-id="6be48-208">You should be able toosign in using Google+ account.</span></span>

## <a name="optional-register-hello-google-account-claims-provider-tooprofile-edit-user-journey"></a><span data-ttu-id="6be48-209">[Facultatif] Inscrire hello Google + compte revendications fournisseur tooProfile-Modifier utilisateur voyage</span><span class="sxs-lookup"><span data-stu-id="6be48-209">[Optional] Register hello Google+ account claims provider tooProfile-Edit user journey</span></span>
<span data-ttu-id="6be48-210">Vous pouvez souhaiter tooadd hello Google + compte fournisseur d’identité également tooyour utilisateur `ProfileEdit` parcours de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6be48-210">You may want tooadd hello Google+ account identity provider also tooyour user `ProfileEdit` user journey.</span></span> <span data-ttu-id="6be48-211">toomake disponibles, nous Répétez hello a deux étapes :</span><span class="sxs-lookup"><span data-stu-id="6be48-211">toomake it available, we repeat hello last two steps:</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="6be48-212">Bouton d’affichage hello</span><span class="sxs-lookup"><span data-stu-id="6be48-212">Display hello button</span></span>
1.  <span data-ttu-id="6be48-213">Ouvrez le fichier d’extension hello de votre stratégie (par exemple, TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="6be48-213">Open hello extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="6be48-214">Recherche hello `<UserJourney>` nœud incluant `Id="ProfileEdit"` dans voyage utilisateur hello que vous avez copiée.</span><span class="sxs-lookup"><span data-stu-id="6be48-214">Find hello `<UserJourney>` node that includes `Id="ProfileEdit"` in hello user journey that you copied.</span></span>
3.  <span data-ttu-id="6be48-215">Recherchez hello `<OrchestrationStep>` nœud qui inclut`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="6be48-215">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="6be48-216">Ajoutez l’extrait de code XML suivant sous le nœud `<ClaimsProviderSelections>` :</span><span class="sxs-lookup"><span data-stu-id="6be48-216">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="6be48-217">Action de lien hello bouton tooan</span><span class="sxs-lookup"><span data-stu-id="6be48-217">Link hello button tooan action</span></span>
1.  <span data-ttu-id="6be48-218">Recherche hello `<OrchestrationStep>` qui inclut `Order="2"` Bonjour `<UserJourney>` nœud.</span><span class="sxs-lookup"><span data-stu-id="6be48-218">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="6be48-219">Ajoutez l’extrait de code XML suivant sous le nœud `<ClaimsExchanges>` :</span><span class="sxs-lookup"><span data-stu-id="6be48-219">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="6be48-220">Tester une stratégie de profil de modification personnalisée hello à l’aide d’exécuter maintenant</span><span class="sxs-lookup"><span data-stu-id="6be48-220">Test hello custom Profile-Edit policy by using Run Now</span></span>

1.  <span data-ttu-id="6be48-221">Ouvrez **paramètres d’Azure AD B2C** et accédez trop**infrastructure d’identité expérience**.</span><span class="sxs-lookup"><span data-stu-id="6be48-221">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="6be48-222">Ouvrez **B2C_1A_ProfileEdit**, hello stratégie personnalisée partie de confiance (RP) de tiers que vous avez téléchargé.</span><span class="sxs-lookup"><span data-stu-id="6be48-222">Open **B2C_1A_ProfileEdit**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="6be48-223">Sélectionnez **Exécuter maintenant**.</span><span class="sxs-lookup"><span data-stu-id="6be48-223">Select **Run now**.</span></span>
3.  <span data-ttu-id="6be48-224">Vous devez être en mesure de toosign à l’aide du compte Google +.</span><span class="sxs-lookup"><span data-stu-id="6be48-224">You should be able toosign in using Google+ account.</span></span>

## <a name="download-hello-complete-policy-files"></a><span data-ttu-id="6be48-225">Télécharger les fichiers de stratégie complète hello</span><span class="sxs-lookup"><span data-stu-id="6be48-225">Download hello complete policy files</span></span>
<span data-ttu-id="6be48-226">Facultatif : Nous vous recommandons de que générer votre scénario à l’aide de vos propres fichiers de stratégie personnalisée hello prise en main des stratégies personnalisées guident au lieu d’utiliser ces exemples de fichiers à la fin.</span><span class="sxs-lookup"><span data-stu-id="6be48-226">Optional: We recommend you build your scenario using your own Custom policy files after completing hello Getting Started with Custom Policies walk through instead of using these sample files.</span></span>  [<span data-ttu-id="6be48-227">Exemples de fichiers de stratégie de référence</span><span class="sxs-lookup"><span data-stu-id="6be48-227">Sample policy files for reference</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-goog-app)
