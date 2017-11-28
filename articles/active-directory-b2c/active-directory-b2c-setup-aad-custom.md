---
title: "Azure Active Directory B2C : Ajouter un fournisseur Azure AD à l’aide de stratégies personnalisées | Microsoft Docs"
description: "Découvrir les stratégies personnalisées Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 31f0dfe5-1ad0-4a25-a53b-8acc71bcea72
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/04/2017
ms.author: parakhj
ms.openlocfilehash: 9b0c32086cebc171d91da2e7bfb48136723ccd4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-azure-ad-accounts"></a><span data-ttu-id="d23b4-103">Azure Active Directory B2C : se connecter à l’aide de comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="d23b4-103">Azure Active Directory B2C: Sign in by using Azure AD accounts</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="d23b4-104">Cet article vous explique comment tooenable connectez-vous pour les utilisateurs à partir d’une organisation Azure Active Directory (Azure AD) spécifique à l’aide de hello de [des stratégies personnalisées](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="d23b4-104">This article shows you how tooenable sign-in for users from a specific Azure Active Directory (Azure AD) organization through hello use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d23b4-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d23b4-105">Prerequisites</span></span>

<span data-ttu-id="d23b4-106">Hello terminé les étapes Bonjour [mise en route avec les stratégies personnalisées](active-directory-b2c-get-started-custom.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="d23b4-106">Complete hello steps in hello [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="d23b4-107">Ces étapes sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="d23b4-107">These steps include:</span></span>

1. <span data-ttu-id="d23b4-108">Création d’un locataire Azure Active Directory B2C (Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="d23b4-108">Creating an Azure Active Directory B2C (Azure AD B2C) tenant.</span></span>
2. <span data-ttu-id="d23b4-109">Création d’une application Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="d23b4-109">Creating an Azure AD B2C application.</span></span>
3. <span data-ttu-id="d23b4-110">Inscription de deux applications de moteur de stratégie.</span><span class="sxs-lookup"><span data-stu-id="d23b4-110">Registering two policy-engine applications.</span></span>
4. <span data-ttu-id="d23b4-111">Configuration des clés.</span><span class="sxs-lookup"><span data-stu-id="d23b4-111">Setting up keys.</span></span>
5. <span data-ttu-id="d23b4-112">Configuration d’un pack de démarrage hello.</span><span class="sxs-lookup"><span data-stu-id="d23b4-112">Setting up hello starter pack.</span></span>

## <a name="create-an-azure-ad-app"></a><span data-ttu-id="d23b4-113">Création d’une application Azure AD</span><span class="sxs-lookup"><span data-stu-id="d23b4-113">Create an Azure AD app</span></span>

<span data-ttu-id="d23b4-114">tooenable connectez-vous pour les utilisateurs spécifiques à une organisation Azure AD, vous devez tooregister une application au sein de client de hello d’organisation Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d23b4-114">tooenable sign-in for users from a specific Azure AD organization, you need tooregister an application within hello organizational Azure AD tenant.</span></span>

>[!NOTE]
> <span data-ttu-id="d23b4-115">Nous utilisons « contoso.com » pour le locataire de hello d’organisation Azure AD et « fabrikamb2c.onmicrosoft.com » en tant que client hello Azure AD B2C Bonjour suivant les instructions.</span><span class="sxs-lookup"><span data-stu-id="d23b4-115">We use "contoso.com" for hello organizational Azure AD tenant and "fabrikamb2c.onmicrosoft.com" as hello Azure AD B2C tenant in hello following instructions.</span></span>

1. <span data-ttu-id="d23b4-116">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d23b4-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="d23b4-117">Dans la barre supérieure de hello, sélectionnez votre compte.</span><span class="sxs-lookup"><span data-stu-id="d23b4-117">On hello top bar, select your account.</span></span> <span data-ttu-id="d23b4-118">À partir de hello **répertoire** , choisissez locataire hello d’organisation Azure AD où vous souhaitez tooregister votre application (contoso.com).</span><span class="sxs-lookup"><span data-stu-id="d23b4-118">From hello **Directory** list, choose hello organizational Azure AD tenant where you want tooregister your application (contoso.com).</span></span>
1. <span data-ttu-id="d23b4-119">Sélectionnez **davantage de services** dans le volet gauche de hello et recherchez « Inscriptions d’application ».</span><span class="sxs-lookup"><span data-stu-id="d23b4-119">Select **More services** in hello left pane, and search for "App registrations."</span></span>
1. <span data-ttu-id="d23b4-120">Sélectionnez **Nouvelle inscription d’application**.</span><span class="sxs-lookup"><span data-stu-id="d23b4-120">Select **New application registration**.</span></span>
1. <span data-ttu-id="d23b4-121">Entrez un nom pour votre application (par exemple, `Azure AD B2C App`).</span><span class="sxs-lookup"><span data-stu-id="d23b4-121">Enter a name for your application (for example, `Azure AD B2C App`).</span></span>
1. <span data-ttu-id="d23b4-122">Sélectionnez **application Web / API** hello pour type d’application.</span><span class="sxs-lookup"><span data-stu-id="d23b4-122">Select **Web app / API** for hello application type.</span></span>
1. <span data-ttu-id="d23b4-123">Pour **URL de connexion**, entrez hello suivant URL, où `yourtenant` remplacé par le nom de votre client Azure AD B2C hello (`fabrikamb2c.onmicrosoft.com`) :</span><span class="sxs-lookup"><span data-stu-id="d23b4-123">For **Sign-on URL**, enter hello following URL, where `yourtenant` is replaced by hello name of your Azure AD B2C tenant (`fabrikamb2c.onmicrosoft.com`):</span></span>

    ```
    https://login.microsoftonline.com/te/yourtenant.onmicrosoft.com/oauth2/authresp
    ```

1. <span data-ttu-id="d23b4-124">Enregistrer l’ID d’application hello.</span><span class="sxs-lookup"><span data-stu-id="d23b4-124">Save hello application ID.</span></span>
1. <span data-ttu-id="d23b4-125">Sélectionnez l’application hello nouvellement créé.</span><span class="sxs-lookup"><span data-stu-id="d23b4-125">Select hello newly created application.</span></span>
1. <span data-ttu-id="d23b4-126">Sous hello **paramètres** panneau, sélectionnez **clés**.</span><span class="sxs-lookup"><span data-stu-id="d23b4-126">Under hello **Settings** blade, select **Keys**.</span></span>
1. <span data-ttu-id="d23b4-127">Créez une clé et enregistrez-la.</span><span class="sxs-lookup"><span data-stu-id="d23b4-127">Create a new key, and save it.</span></span> <span data-ttu-id="d23b4-128">Vous allez l’utiliser dans les étapes de hello dans la section suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="d23b4-128">You will use it in hello steps in hello next section.</span></span>

## <a name="add-hello-azure-ad-key-tooazure-ad-b2c"></a><span data-ttu-id="d23b4-129">Ajouter tooAzure de clé hello AD Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="d23b4-129">Add hello Azure AD key tooAzure AD B2C</span></span>

<span data-ttu-id="d23b4-130">Vous avez besoin de clé d’application toostore hello contoso.com dans votre locataire Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="d23b4-130">You need toostore hello contoso.com application key in your Azure AD B2C tenant.</span></span> <span data-ttu-id="d23b4-131">toodo cela :</span><span class="sxs-lookup"><span data-stu-id="d23b4-131">toodo this:</span></span>
1. <span data-ttu-id="d23b4-132">Accédez tooyour Azure AD B2C client, puis sélectionnez **B2C paramètres** > **infrastructure d’identité expérience** > **clés de stratégie**.</span><span class="sxs-lookup"><span data-stu-id="d23b4-132">Go tooyour Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework** > **Policy Keys**.</span></span>
1. <span data-ttu-id="d23b4-133">Sélectionnez **+Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="d23b4-133">Select **+Add**.</span></span>
1. <span data-ttu-id="d23b4-134">Sélectionnez ou entrez les options suivantes :</span><span class="sxs-lookup"><span data-stu-id="d23b4-134">Select or enter these options:</span></span>
   * <span data-ttu-id="d23b4-135">Sélectionnez **Manuel**.</span><span class="sxs-lookup"><span data-stu-id="d23b4-135">Select **Manual**.</span></span>
   * <span data-ttu-id="d23b4-136">Pour **Nom**, choisissez un nom correspondant au nom de votre locataire Azure AD (par exemple, `ContosoAppSecret`).</span><span class="sxs-lookup"><span data-stu-id="d23b4-136">For **Name**, choose a name that matches your Azure AD tenant name (for example, `ContosoAppSecret`).</span></span>  <span data-ttu-id="d23b4-137">préfixe de Hello `B2C_1A_` est ajouté automatiquement nom toohello de votre clé.</span><span class="sxs-lookup"><span data-stu-id="d23b4-137">hello prefix `B2C_1A_` is added automatically toohello name of your key.</span></span>
   * <span data-ttu-id="d23b4-138">Collez votre clé d’application Bonjour **Secret** boîte.</span><span class="sxs-lookup"><span data-stu-id="d23b4-138">Paste your application key in hello **Secret** box.</span></span>
   * <span data-ttu-id="d23b4-139">Sélectionnez **Signature**.</span><span class="sxs-lookup"><span data-stu-id="d23b4-139">Select **Signature**.</span></span>
1. <span data-ttu-id="d23b4-140">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="d23b4-140">Select **Create**.</span></span>
1. <span data-ttu-id="d23b4-141">Vérifiez que vous avez créé la clé de hello `B2C_1A_ContosoAppSecret`.</span><span class="sxs-lookup"><span data-stu-id="d23b4-141">Confirm that you've created hello key `B2C_1A_ContosoAppSecret`.</span></span>


## <a name="add-a-claims-provider-in-your-base-policy"></a><span data-ttu-id="d23b4-142">Ajoutez un fournisseur de revendications dans votre stratégie de base</span><span class="sxs-lookup"><span data-stu-id="d23b4-142">Add a claims provider in your base policy</span></span>

<span data-ttu-id="d23b4-143">Si vous souhaitez que les utilisateurs toosign à l’aide d’Azure AD, vous devez toodefine Azure AD comme fournisseur de revendications.</span><span class="sxs-lookup"><span data-stu-id="d23b4-143">If you want users toosign in by using Azure AD, you need toodefine Azure AD as a claims provider.</span></span> <span data-ttu-id="d23b4-144">En d’autres termes, vous devez toospecify un point de terminaison communique avec Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="d23b4-144">In other words, you need toospecify an endpoint that Azure AD B2C will communicate with.</span></span> <span data-ttu-id="d23b4-145">point de terminaison Hello fournissent un ensemble de revendications qui sont utilisés par Azure AD B2C tooverify authentifié un utilisateur spécifique.</span><span class="sxs-lookup"><span data-stu-id="d23b4-145">hello endpoint will provide a set of claims that are used by Azure AD B2C tooverify that a specific user has authenticated.</span></span> 

<span data-ttu-id="d23b4-146">Vous pouvez définir Azure AD comme fournisseur de revendications en ajoutant Azure AD toohello `<ClaimsProvider>` nœud dans le fichier d’extension hello de votre stratégie :</span><span class="sxs-lookup"><span data-stu-id="d23b4-146">You can define Azure AD as a claims provider by adding Azure AD toohello `<ClaimsProvider>` node in hello extension file of your policy:</span></span>

1. <span data-ttu-id="d23b4-147">Ouvrez le fichier d’extension hello (TrustFrameworkExtensions.xml) à partir de votre répertoire de travail.</span><span class="sxs-lookup"><span data-stu-id="d23b4-147">Open hello extension file (TrustFrameworkExtensions.xml) from your working directory.</span></span>
1. <span data-ttu-id="d23b4-148">Recherche hello `<ClaimsProviders>` section.</span><span class="sxs-lookup"><span data-stu-id="d23b4-148">Find hello `<ClaimsProviders>` section.</span></span> <span data-ttu-id="d23b4-149">Si elle n’existe pas, l’ajouter sous le nœud racine de hello.</span><span class="sxs-lookup"><span data-stu-id="d23b4-149">If it does not exist, add it under hello root node.</span></span>
1. <span data-ttu-id="d23b4-150">Ajoutez un nœud `<ClaimsProvider>` comme suit :</span><span class="sxs-lookup"><span data-stu-id="d23b4-150">Add a new `<ClaimsProvider>` node as follows:</span></span>

    ```XML
    <ClaimsProvider>
        <Domain>Contoso</Domain>
        <DisplayName>Login using Contoso</DisplayName>
        <TechnicalProfiles>
            <TechnicalProfile Id="ContosoProfile">
                <DisplayName>Contoso Employee</DisplayName>
                <Description>Login with your Contoso account</Description>
                <Protocol Name="OpenIdConnect"/>
                <OutputTokenFormat>JWT</OutputTokenFormat>
                <Metadata>
                    <Item Key="METADATA">https://login.windows.net/contoso.com/.well-known/openid-configuration</Item>
                    <Item Key="ProviderName">https://sts.windows.net/00000000-0000-0000-0000-000000000000/</Item>
                    <Item Key="client_id">00000000-0000-0000-0000-000000000000</Item>
                    <Item Key="IdTokenAudience">00000000-0000-0000-0000-000000000000</Item>
                    <Item Key="response_types">id_token</Item>
                    <Item Key="UsePolicyInRedirectUri">false</Item>
                </Metadata>
                <CryptographicKeys>
                    <Key Id="client_secret" StorageReferenceId="B2C_1A_ContosoAppSecret"/>
                </CryptographicKeys>
                <OutputClaims>
                    <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="oid"/>
                    <OutputClaim ClaimTypeReferenceId="tenantId" PartnerClaimType="tid"/>
                    <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name" />
                    <OutputClaim ClaimTypeReferenceId="surName" PartnerClaimType="family_name" />
                    <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
                    <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="contosoAuthentication" />
                    <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="AzureADContoso" />
                </OutputClaims>
                <OutputClaimsTransformations>
                    <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName"/>
                    <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName"/>
                    <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId"/>
                    <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId"/>
                </OutputClaimsTransformations>
                <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop"/>
            </TechnicalProfile>
        </TechnicalProfiles>
    </ClaimsProvider>
    ```

1. <span data-ttu-id="d23b4-151">Sous hello `<ClaimsProvider>` nœud, la valeur hello de mise à jour pour `<Domain>` tooa valeur unique qui peut être utilisé toodistinguish à partir d’autres fournisseurs d’identité.</span><span class="sxs-lookup"><span data-stu-id="d23b4-151">Under hello `<ClaimsProvider>` node, update hello value for `<Domain>` tooa unique value that can be used toodistinguish it from other identity providers.</span></span>
1. <span data-ttu-id="d23b4-152">Sous hello `<ClaimsProvider>` nœud, la valeur hello de mise à jour pour `<DisplayName>` fournisseur de revendications de nom convivial tooa hello.</span><span class="sxs-lookup"><span data-stu-id="d23b4-152">Under hello `<ClaimsProvider>` node, update hello value for `<DisplayName>` tooa friendly name for hello claims provider.</span></span> <span data-ttu-id="d23b4-153">Cette valeur n’est pas utilisée actuellement.</span><span class="sxs-lookup"><span data-stu-id="d23b4-153">This value is not currently used.</span></span>

### <a name="update-hello-technical-profile"></a><span data-ttu-id="d23b4-154">Mettre à jour le profil de technique hello</span><span class="sxs-lookup"><span data-stu-id="d23b4-154">Update hello technical profile</span></span>

<span data-ttu-id="d23b4-155">tooget un jeton à partir du point de terminaison hello Azure AD, vous devez les protocoles de hello toodefine que Azure AD B2C doit utiliser toocommunicate avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d23b4-155">tooget a token from hello Azure AD endpoint, you need toodefine hello protocols that Azure AD B2C should use toocommunicate with Azure AD.</span></span> <span data-ttu-id="d23b4-156">Cette opération est effectuée à l’intérieur de hello `<TechnicalProfile>` élément de `<ClaimsProvider>`.</span><span class="sxs-lookup"><span data-stu-id="d23b4-156">This is done inside hello `<TechnicalProfile>` element of  `<ClaimsProvider>`.</span></span>
1. <span data-ttu-id="d23b4-157">Mise à jour ID hello Hello `<TechnicalProfile>` nœud.</span><span class="sxs-lookup"><span data-stu-id="d23b4-157">Update hello ID of hello `<TechnicalProfile>` node.</span></span> <span data-ttu-id="d23b4-158">Cet ID est utilisé toorefer toothis profil technique à partir d’autres parties de la stratégie de hello.</span><span class="sxs-lookup"><span data-stu-id="d23b4-158">This ID is used toorefer toothis technical profile from other parts of hello policy.</span></span>
1. <span data-ttu-id="d23b4-159">Mettre à jour la valeur hello pour `<DisplayName>`.</span><span class="sxs-lookup"><span data-stu-id="d23b4-159">Update hello value for `<DisplayName>`.</span></span> <span data-ttu-id="d23b4-160">Cette valeur s’affichera sur le bouton hello de connexion sur votre écran de connexion.</span><span class="sxs-lookup"><span data-stu-id="d23b4-160">This value will be displayed on hello sign-in button on your sign-in screen.</span></span>
1. <span data-ttu-id="d23b4-161">Mettre à jour la valeur hello pour `<Description>`.</span><span class="sxs-lookup"><span data-stu-id="d23b4-161">Update hello value for `<Description>`.</span></span>
1. <span data-ttu-id="d23b4-162">Azure AD utilise le protocole OpenID Connect de hello, assurez-vous que valeur hello pour `<Protocol>` est `"OpenIdConnect"`.</span><span class="sxs-lookup"><span data-stu-id="d23b4-162">Azure AD uses hello OpenID Connect protocol, so ensure that hello value for `<Protocol>` is `"OpenIdConnect"`.</span></span>

<span data-ttu-id="d23b4-163">Vous devez tooupdate hello `<Metadata>` section dans le fichier XML de hello référencé des paramètres de configuration tooearlier tooreflect hello pour spécifique à votre client Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d23b4-163">You need tooupdate hello `<Metadata>` section in hello XML file referred tooearlier tooreflect hello configuration settings for your specific Azure AD tenant.</span></span> <span data-ttu-id="d23b4-164">Dans le fichier XML de hello, mettre à jour les valeurs de métadonnées hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d23b4-164">In hello XML file, update hello metadata values as follows:</span></span>

1. <span data-ttu-id="d23b4-165">Définissez `<Item Key="METADATA">` trop`https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, où `yourAzureADtenant` est votre nom de client Azure AD (contoso.com).</span><span class="sxs-lookup"><span data-stu-id="d23b4-165">Set `<Item Key="METADATA">` too`https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, where `yourAzureADtenant` is your Azure AD tenant name (contoso.com).</span></span>
1. <span data-ttu-id="d23b4-166">Ouvrez votre toohello navigateur et allez `METADATA` URL que vous venez de mettre à jour.</span><span class="sxs-lookup"><span data-stu-id="d23b4-166">Open your browser and go toohello `METADATA` URL that you just updated.</span></span>
1. <span data-ttu-id="d23b4-167">Dans le navigateur de hello, recherche d’objet 'd’attribut issuer' hello et copiez sa valeur.</span><span class="sxs-lookup"><span data-stu-id="d23b4-167">In hello browser, look for hello 'issuer' object and copy its value.</span></span> <span data-ttu-id="d23b4-168">Il doit ressembler à hello suivant : `https://sts.windows.net/{tenantId}/`.</span><span class="sxs-lookup"><span data-stu-id="d23b4-168">It should look like hello following: `https://sts.windows.net/{tenantId}/`.</span></span>
1. <span data-ttu-id="d23b4-169">Collez la valeur hello pour `<Item Key="ProviderName">` dans le fichier XML de hello.</span><span class="sxs-lookup"><span data-stu-id="d23b4-169">Paste hello value for `<Item Key="ProviderName">` in hello XML file.</span></span>
1. <span data-ttu-id="d23b4-170">Définissez `<Item Key="client_id">` toohello ID de l’application à partir de l’inscription d’une application hello.</span><span class="sxs-lookup"><span data-stu-id="d23b4-170">Set `<Item Key="client_id">` toohello application ID from hello app registration.</span></span>
1. <span data-ttu-id="d23b4-171">Définissez `<Item Key="IdTokenAudience">` toohello ID de l’application à partir de l’inscription d’une application hello.</span><span class="sxs-lookup"><span data-stu-id="d23b4-171">Set `<Item Key="IdTokenAudience">` toohello application ID from hello app registration.</span></span>
1. <span data-ttu-id="d23b4-172">Vérifiez que `<Item Key="response_types">` est défini trop`id_token`.</span><span class="sxs-lookup"><span data-stu-id="d23b4-172">Ensure that `<Item Key="response_types">` is set too`id_token`.</span></span>
1. <span data-ttu-id="d23b4-173">Vérifiez que `<Item Key="UsePolicyInRedirectUri">` est défini trop`false`.</span><span class="sxs-lookup"><span data-stu-id="d23b4-173">Ensure that `<Item Key="UsePolicyInRedirectUri">` is set too`false`.</span></span>

<span data-ttu-id="d23b4-174">Vous devez également le code secret toolink hello Azure AD que vous avez enregistré dans votre toohello de locataire Azure AD B2C Azure AD `<ClaimsProvider>` informations :</span><span class="sxs-lookup"><span data-stu-id="d23b4-174">You also need toolink hello Azure AD secret that you registered in your Azure AD B2C tenant toohello Azure AD `<ClaimsProvider>` information:</span></span>

* <span data-ttu-id="d23b4-175">Bonjour `<CryptographicKeys>` section Bonjour précédant le fichier XML, mettre à jour la valeur hello pour `StorageReferenceId` toohello ID de référence de clé secrète hello que vous avez définie (par exemple, `ContosoAppSecret`).</span><span class="sxs-lookup"><span data-stu-id="d23b4-175">In hello `<CryptographicKeys>` section in hello preceding XML file, update hello value for `StorageReferenceId` toohello reference ID of hello secret that you defined (for example, `ContosoAppSecret`).</span></span>

### <a name="upload-hello-extension-file-for-verification"></a><span data-ttu-id="d23b4-176">Télécharger le fichier d’extension hello pour la vérification</span><span class="sxs-lookup"><span data-stu-id="d23b4-176">Upload hello extension file for verification</span></span>

<span data-ttu-id="d23b4-177">À ce stade, vous avez configuré votre stratégie afin que Azure AD B2C sait comment toocommunicate avec votre annuaire Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d23b4-177">By now, you have configured your policy so that Azure AD B2C knows how toocommunicate with your Azure AD directory.</span></span> <span data-ttu-id="d23b4-178">Essayez de télécharger le fichier d’extension hello de votre tooconfirm simplement stratégie qu’il ne possède pas les problèmes de jusqu'à présent.</span><span class="sxs-lookup"><span data-stu-id="d23b4-178">Try uploading hello extension file of your policy just tooconfirm that it doesn't have any issues so far.</span></span> <span data-ttu-id="d23b4-179">toodo pour :</span><span class="sxs-lookup"><span data-stu-id="d23b4-179">toodo so:</span></span>

1. <span data-ttu-id="d23b4-180">Ouvrez hello **toutes les stratégies** panneau dans votre locataire Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="d23b4-180">Open hello **All Policies** blade in your Azure AD B2C tenant.</span></span>
1. <span data-ttu-id="d23b4-181">Vérifiez hello **remplacer la stratégie de hello si elle existe** boîte.</span><span class="sxs-lookup"><span data-stu-id="d23b4-181">Check hello **Overwrite hello policy if it exists** box.</span></span>
1. <span data-ttu-id="d23b4-182">Télécharger le fichier d’extension hello (TrustFrameworkExtensions.xml) et assurez-vous qu’il validation n’échoue pas hello.</span><span class="sxs-lookup"><span data-stu-id="d23b4-182">Upload hello extension file (TrustFrameworkExtensions.xml), and ensure that it does not fail hello validation.</span></span>

## <a name="register-hello-azure-ad-claims-provider-tooa-user-journey"></a><span data-ttu-id="d23b4-183">Inscrire le parcours de hello Azure AD revendications fournisseur tooa utilisateur</span><span class="sxs-lookup"><span data-stu-id="d23b4-183">Register hello Azure AD claims provider tooa user journey</span></span>

<span data-ttu-id="d23b4-184">Vous devez maintenant tooadd hello Azure AD identity fournisseur tooone de votre parcours de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d23b4-184">You now need tooadd hello Azure AD identity provider tooone of your user journeys.</span></span> <span data-ttu-id="d23b4-185">À ce stade, le fournisseur d’identité hello a été configuré, mais il n’est pas disponible dans les écrans de connexion-haut/connectez-vous hello.</span><span class="sxs-lookup"><span data-stu-id="d23b4-185">At this point, hello identity provider has been set up, but it’s not available in any of hello sign-up/sign-in screens.</span></span> <span data-ttu-id="d23b4-186">toomake il est disponible, nous crée un doublon d’un déplacement de modèle à l’utilisateur existant et modifiez-le afin qu’il puisse également le fournisseur d’identité hello Azure AD :</span><span class="sxs-lookup"><span data-stu-id="d23b4-186">toomake it available, we will create a duplicate of an existing template user journey, and then modify it so that it also has hello Azure AD identity provider:</span></span>

1. <span data-ttu-id="d23b4-187">Ouvrez le fichier de base hello de votre stratégie (par exemple, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="d23b4-187">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
1. <span data-ttu-id="d23b4-188">Recherche hello `<UserJourneys>` hello élément et copie entière `<UserJourney>` nœud inclut `Id="SignUpOrSignIn"`.</span><span class="sxs-lookup"><span data-stu-id="d23b4-188">Find hello `<UserJourneys>` element and copy hello entire `<UserJourney>` node that includes `Id="SignUpOrSignIn"`.</span></span>
1. <span data-ttu-id="d23b4-189">Ouvrez le fichier d’extension hello (par exemple, TrustFrameworkExtensions.xml) et recherche hello `<UserJourneys>` élément.</span><span class="sxs-lookup"><span data-stu-id="d23b4-189">Open hello extension file (for example, TrustFrameworkExtensions.xml) and find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="d23b4-190">Si l’élément de hello n’existe pas, ajoutez-en un.</span><span class="sxs-lookup"><span data-stu-id="d23b4-190">If hello element doesn't exist, add one.</span></span>
1. <span data-ttu-id="d23b4-191">Hello coller entière `<UserJourney>` nœud que vous avez copié en tant qu’enfant de hello `<UserJourneys>` élément.</span><span class="sxs-lookup"><span data-stu-id="d23b4-191">Paste hello entire `<UserJourney>` node that you copied as a child of hello `<UserJourneys>` element.</span></span>
1. <span data-ttu-id="d23b4-192">Renommer des ID hello de parcours d’utilisateur nouveau hello (par exemple, renommer en tant que `SignUpOrSignUsingContoso`).</span><span class="sxs-lookup"><span data-stu-id="d23b4-192">Rename hello ID of hello new user journey (for example, rename as `SignUpOrSignUsingContoso`).</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="d23b4-193">Hello d’affichage « bouton »</span><span class="sxs-lookup"><span data-stu-id="d23b4-193">Display hello "button"</span></span>

<span data-ttu-id="d23b4-194">Hello `<ClaimsProviderSelection>` élément est le bouton de fournisseur d’identité tooan analogue sur un connexion-haut/écran de connexion.</span><span class="sxs-lookup"><span data-stu-id="d23b4-194">hello `<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up/sign-in screen.</span></span> <span data-ttu-id="d23b4-195">Si vous ajoutez un `<ClaimsProviderSelection>` élément pour Azure AD, un nouveau bouton apparaît lorsqu’un utilisateur arrive sur la page de hello.</span><span class="sxs-lookup"><span data-stu-id="d23b4-195">If you add a `<ClaimsProviderSelection>` element for Azure AD, a new button shows up when a user lands on hello page.</span></span> <span data-ttu-id="d23b4-196">tooadd cet élément :</span><span class="sxs-lookup"><span data-stu-id="d23b4-196">tooadd this element:</span></span>

1. <span data-ttu-id="d23b4-197">Recherche hello `<OrchestrationStep>` nœud incluant `Order="1"` dans voyage utilisateur hello que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="d23b4-197">Find hello `<OrchestrationStep>` node that includes `Order="1"` in hello user journey that you just created.</span></span>
1. <span data-ttu-id="d23b4-198">Ajoutez hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="d23b4-198">Add hello following:</span></span>

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

1. <span data-ttu-id="d23b4-199">Définissez `TargetClaimsExchangeId` tooan les valeur appropriée.</span><span class="sxs-lookup"><span data-stu-id="d23b4-199">Set `TargetClaimsExchangeId` tooan appropriate value.</span></span> <span data-ttu-id="d23b4-200">Nous vous recommandons de suivant hello même convention que d’autres :  *\[ClaimProviderName\]Exchange*.</span><span class="sxs-lookup"><span data-stu-id="d23b4-200">We recommend following hello same convention as others: *\[ClaimProviderName\]Exchange*.</span></span>

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="d23b4-201">Action de lien hello bouton tooan</span><span class="sxs-lookup"><span data-stu-id="d23b4-201">Link hello button tooan action</span></span>

<span data-ttu-id="d23b4-202">Maintenant que vous avez un bouton en place, vous devez toolink il tooan action.</span><span class="sxs-lookup"><span data-stu-id="d23b4-202">Now that you have a button in place, you need toolink it tooan action.</span></span> <span data-ttu-id="d23b4-203">action de Hello, dans ce cas, est de toocommunicate Azure AD B2C avec Azure AD tooreceive un jeton.</span><span class="sxs-lookup"><span data-stu-id="d23b4-203">hello action, in this case, is for Azure AD B2C toocommunicate with Azure AD tooreceive a token.</span></span> <span data-ttu-id="d23b4-204">Action de tooan bouton lien hello en liant le profil de technique hello pour votre fournisseur de revendications d’Azure AD :</span><span class="sxs-lookup"><span data-stu-id="d23b4-204">Link hello button tooan action by linking hello technical profile for your Azure AD claims provider:</span></span>

1. <span data-ttu-id="d23b4-205">Recherche hello `<OrchestrationStep>` qui inclut `Order="2"` Bonjour `<UserJourney>` nœud.</span><span class="sxs-lookup"><span data-stu-id="d23b4-205">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
1. <span data-ttu-id="d23b4-206">Ajoutez hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="d23b4-206">Add hello following:</span></span>

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

1. <span data-ttu-id="d23b4-207">Mise à jour `Id` toohello même valeur que celle de `TargetClaimsExchangeId` Bonjour précédant la section.</span><span class="sxs-lookup"><span data-stu-id="d23b4-207">Update `Id` toohello same value as that of `TargetClaimsExchangeId` in hello preceding section.</span></span>
1. <span data-ttu-id="d23b4-208">Mise à jour `TechnicalProfileReferenceId` ID toohello Hello technique du profil que vous avez créé précédemment (ContosoProfile).</span><span class="sxs-lookup"><span data-stu-id="d23b4-208">Update `TechnicalProfileReferenceId` toohello ID of hello technical profile you created earlier (ContosoProfile).</span></span>

### <a name="upload-hello-updated-extension-file"></a><span data-ttu-id="d23b4-209">Télécharger le fichier d’extension de mise à jour de hello</span><span class="sxs-lookup"><span data-stu-id="d23b4-209">Upload hello updated extension file</span></span>

<span data-ttu-id="d23b4-210">Vous avez terminé la modification d’extension hello.</span><span class="sxs-lookup"><span data-stu-id="d23b4-210">You are done modifying hello extension file.</span></span> <span data-ttu-id="d23b4-211">Enregistrez-le.</span><span class="sxs-lookup"><span data-stu-id="d23b4-211">Save it.</span></span> <span data-ttu-id="d23b4-212">Puis téléchargez le fichier de hello et assurez-vous que toutes les validations réussissent.</span><span class="sxs-lookup"><span data-stu-id="d23b4-212">Then upload hello file, and ensure that all validations succeed.</span></span>

### <a name="update-hello-rp-file"></a><span data-ttu-id="d23b4-213">Fichier de mise à jour hello RP</span><span class="sxs-lookup"><span data-stu-id="d23b4-213">Update hello RP file</span></span>

<span data-ttu-id="d23b4-214">Vous devez maintenant tooupdate hello partie de confiance (RP) de tiers fichier qui exécutera voyage utilisateur hello que vous venez de créer :</span><span class="sxs-lookup"><span data-stu-id="d23b4-214">You now need tooupdate hello relying party (RP) file that will initiate hello user journey that you just created:</span></span>

1. <span data-ttu-id="d23b4-215">Faites une copie de SignUpOrSignIn.xml dans votre répertoire de travail et renommez-le (par exemple, renommer tooSignUpOrSignInWithAAD.xml).</span><span class="sxs-lookup"><span data-stu-id="d23b4-215">Make a copy of SignUpOrSignIn.xml in your working directory, and rename it (for example, rename it tooSignUpOrSignInWithAAD.xml).</span></span>
1. <span data-ttu-id="d23b4-216">Hello de fichier et de mise à jour de nouveau hello ouvrir `PolicyId` attribut `<TrustFrameworkPolicy>` avec une valeur unique (par exemple, SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="d23b4-216">Open hello new file and update hello `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value (for example, SignUpOrSignInWithAAD).</span></span> <br> <span data-ttu-id="d23b4-217">Ce sera le nom hello de votre stratégie (par exemple, B2C\_1 a\_SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="d23b4-217">This will be hello name of your policy (for example, B2C\_1A\_SignUpOrSignInWithAAD).</span></span>
1. <span data-ttu-id="d23b4-218">Modifier hello `ReferenceId` attribut `<DefaultUserJourney>` ID de hello toomatch nouveau voyage utilisateur hello, que vous avez créé (SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="d23b4-218">Modify hello `ReferenceId` attribute in `<DefaultUserJourney>` toomatch hello ID of hello new user journey that you created (SignUpOrSignUsingContoso).</span></span>
1. <span data-ttu-id="d23b4-219">Enregistrer vos modifications et téléchargez le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="d23b4-219">Save your changes, and upload hello file.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="d23b4-220">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="d23b4-220">Troubleshooting</span></span>

<span data-ttu-id="d23b4-221">Tester une stratégie personnalisée hello que vous venez de télécharger en cliquant sur son panneau **exécuter maintenant**.</span><span class="sxs-lookup"><span data-stu-id="d23b4-221">Test hello custom policy that you just uploaded by opening its blade and clicking **Run now**.</span></span> <span data-ttu-id="d23b4-222">problèmes de toodiagnose, en savoir plus sur [dépannage](active-directory-b2c-troubleshoot-custom.md).</span><span class="sxs-lookup"><span data-stu-id="d23b4-222">toodiagnose problems, read about [troubleshooting](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d23b4-223">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d23b4-223">Next steps</span></span>

<span data-ttu-id="d23b4-224">Fournir des commentaires trop[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="d23b4-224">Provide feedback too[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span></span>
