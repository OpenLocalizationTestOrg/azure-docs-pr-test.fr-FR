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
ms.openlocfilehash: 6c073d70debfdc3560405955d65fa9ccaa7d8b1f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-azure-ad-accounts"></a><span data-ttu-id="adcd8-103">Azure Active Directory B2C : se connecter à l’aide de comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="adcd8-103">Azure Active Directory B2C: Sign in by using Azure AD accounts</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="adcd8-104">Cet article explique comment autoriser la connexion d’utilisateurs d’une organisation Azure Active Directory (Azure AD) spécifique en utilisant des [stratégies personnalisées](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="adcd8-104">This article shows you how to enable sign-in for users from a specific Azure Active Directory (Azure AD) organization through the use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="adcd8-105">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="adcd8-105">Prerequisites</span></span>

<span data-ttu-id="adcd8-106">Suivez les étapes décrites dans [Bien démarrer avec les stratégies personnalisées](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="adcd8-106">Complete the steps in the [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="adcd8-107">Ces étapes sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="adcd8-107">These steps include:</span></span>

1. <span data-ttu-id="adcd8-108">Création d’un locataire Azure Active Directory B2C (Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="adcd8-108">Creating an Azure Active Directory B2C (Azure AD B2C) tenant.</span></span>
2. <span data-ttu-id="adcd8-109">Création d’une application Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="adcd8-109">Creating an Azure AD B2C application.</span></span>
3. <span data-ttu-id="adcd8-110">Inscription de deux applications de moteur de stratégie.</span><span class="sxs-lookup"><span data-stu-id="adcd8-110">Registering two policy-engine applications.</span></span>
4. <span data-ttu-id="adcd8-111">Configuration des clés.</span><span class="sxs-lookup"><span data-stu-id="adcd8-111">Setting up keys.</span></span>
5. <span data-ttu-id="adcd8-112">Configuration du pack de démarrage.</span><span class="sxs-lookup"><span data-stu-id="adcd8-112">Setting up the starter pack.</span></span>

## <a name="create-an-azure-ad-app"></a><span data-ttu-id="adcd8-113">Création d’une application Azure AD</span><span class="sxs-lookup"><span data-stu-id="adcd8-113">Create an Azure AD app</span></span>

<span data-ttu-id="adcd8-114">Pour autoriser la connexion des utilisateurs d’une organisation Azure AD spécifique, vous devez inscrire une application au sein du locataire Azure AD de l’organisation.</span><span class="sxs-lookup"><span data-stu-id="adcd8-114">To enable sign-in for users from a specific Azure AD organization, you need to register an application within the organizational Azure AD tenant.</span></span>

>[!NOTE]
> <span data-ttu-id="adcd8-115">Nous utilisons « contoso.com » pour l’organisation (locataire) Azure AD et « fabrikamb2c.onmicrosoft.com » comme locataire Azure AD B2C dans les instructions suivantes.</span><span class="sxs-lookup"><span data-stu-id="adcd8-115">We use "contoso.com" for the organizational Azure AD tenant and "fabrikamb2c.onmicrosoft.com" as the Azure AD B2C tenant in the following instructions.</span></span>

1. <span data-ttu-id="adcd8-116">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="adcd8-116">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="adcd8-117">Dans le menu supérieur, sélectionnez votre compte.</span><span class="sxs-lookup"><span data-stu-id="adcd8-117">On the top bar, select your account.</span></span> <span data-ttu-id="adcd8-118">Dans la liste **Répertoire**, choisissez l’organisation (locataire) Azure AD auprès de laquelle vous voulez inscrire votre application (contoso.com).</span><span class="sxs-lookup"><span data-stu-id="adcd8-118">From the **Directory** list, choose the organizational Azure AD tenant where you want to register your application (contoso.com).</span></span>
1. <span data-ttu-id="adcd8-119">Cliquez sur **Autres services** dans le volet gauche, puis recherchez « Inscriptions d’applications ».</span><span class="sxs-lookup"><span data-stu-id="adcd8-119">Select **More services** in the left pane, and search for "App registrations."</span></span>
1. <span data-ttu-id="adcd8-120">Sélectionnez **Nouvelle inscription d’application**.</span><span class="sxs-lookup"><span data-stu-id="adcd8-120">Select **New application registration**.</span></span>
1. <span data-ttu-id="adcd8-121">Entrez un nom pour votre application (par exemple, `Azure AD B2C App`).</span><span class="sxs-lookup"><span data-stu-id="adcd8-121">Enter a name for your application (for example, `Azure AD B2C App`).</span></span>
1. <span data-ttu-id="adcd8-122">Pour le type d’application, sélectionnez **Application web/API**.</span><span class="sxs-lookup"><span data-stu-id="adcd8-122">Select **Web app / API** for the application type.</span></span>
1. <span data-ttu-id="adcd8-123">Pour **URL de connexion**, entrez l’URL suivante où `yourtenant` est remplacé par le nom de votre locataire Azure AD B2C (`fabrikamb2c.onmicrosoft.com`) :</span><span class="sxs-lookup"><span data-stu-id="adcd8-123">For **Sign-on URL**, enter the following URL, where `yourtenant` is replaced by the name of your Azure AD B2C tenant (`fabrikamb2c.onmicrosoft.com`):</span></span>

    ```
    https://login.microsoftonline.com/te/yourtenant.onmicrosoft.com/oauth2/authresp
    ```

1. <span data-ttu-id="adcd8-124">Enregistrez l’ID de l’application.</span><span class="sxs-lookup"><span data-stu-id="adcd8-124">Save the application ID.</span></span>
1. <span data-ttu-id="adcd8-125">Sélectionnez l’application que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="adcd8-125">Select the newly created application.</span></span>
1. <span data-ttu-id="adcd8-126">Dans le panneau **Paramètres**, sélectionnez **Clés**.</span><span class="sxs-lookup"><span data-stu-id="adcd8-126">Under the **Settings** blade, select **Keys**.</span></span>
1. <span data-ttu-id="adcd8-127">Créez une clé et enregistrez-la.</span><span class="sxs-lookup"><span data-stu-id="adcd8-127">Create a new key, and save it.</span></span> <span data-ttu-id="adcd8-128">Vous allez l’utiliser dans les étapes de la prochaine section.</span><span class="sxs-lookup"><span data-stu-id="adcd8-128">You will use it in the steps in the next section.</span></span>

## <a name="add-the-azure-ad-key-to-azure-ad-b2c"></a><span data-ttu-id="adcd8-129">Ajouter la clé d’Azure AD à Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="adcd8-129">Add the Azure AD key to Azure AD B2C</span></span>

<span data-ttu-id="adcd8-130">Vous devez stocker la clé d’application contoso.com dans votre locataire Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="adcd8-130">You need to store the contoso.com application key in your Azure AD B2C tenant.</span></span> <span data-ttu-id="adcd8-131">Pour ce faire :</span><span class="sxs-lookup"><span data-stu-id="adcd8-131">To do this:</span></span>
1. <span data-ttu-id="adcd8-132">Accédez à votre locataire Azure AD B2C, puis sélectionnez **Paramètres Azure AD B2C** > **Infrastructure d’expérience d’identité** > **Clés de stratégie**.</span><span class="sxs-lookup"><span data-stu-id="adcd8-132">Go to your Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework** > **Policy Keys**.</span></span>
1. <span data-ttu-id="adcd8-133">Sélectionnez **+Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="adcd8-133">Select **+Add**.</span></span>
1. <span data-ttu-id="adcd8-134">Sélectionnez ou entrez les options suivantes :</span><span class="sxs-lookup"><span data-stu-id="adcd8-134">Select or enter these options:</span></span>
   * <span data-ttu-id="adcd8-135">Sélectionnez **Manuel**.</span><span class="sxs-lookup"><span data-stu-id="adcd8-135">Select **Manual**.</span></span>
   * <span data-ttu-id="adcd8-136">Pour **Nom**, choisissez un nom correspondant au nom de votre locataire Azure AD (par exemple, `ContosoAppSecret`).</span><span class="sxs-lookup"><span data-stu-id="adcd8-136">For **Name**, choose a name that matches your Azure AD tenant name (for example, `ContosoAppSecret`).</span></span>  <span data-ttu-id="adcd8-137">Le préfixe `B2C_1A_` est ajouté automatiquement au nom de votre clé.</span><span class="sxs-lookup"><span data-stu-id="adcd8-137">The prefix `B2C_1A_` is added automatically to the name of your key.</span></span>
   * <span data-ttu-id="adcd8-138">Collez votre clé d’application dans la zone **Secret**.</span><span class="sxs-lookup"><span data-stu-id="adcd8-138">Paste your application key in the **Secret** box.</span></span>
   * <span data-ttu-id="adcd8-139">Sélectionnez **Signature**.</span><span class="sxs-lookup"><span data-stu-id="adcd8-139">Select **Signature**.</span></span>
1. <span data-ttu-id="adcd8-140">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="adcd8-140">Select **Create**.</span></span>
1. <span data-ttu-id="adcd8-141">Vérifiez que vous avez créé la clé `B2C_1A_ContosoAppSecret`.</span><span class="sxs-lookup"><span data-stu-id="adcd8-141">Confirm that you've created the key `B2C_1A_ContosoAppSecret`.</span></span>


## <a name="add-a-claims-provider-in-your-base-policy"></a><span data-ttu-id="adcd8-142">Ajoutez un fournisseur de revendications dans votre stratégie de base</span><span class="sxs-lookup"><span data-stu-id="adcd8-142">Add a claims provider in your base policy</span></span>

<span data-ttu-id="adcd8-143">Si vous souhaitez que les utilisateurs se connectent à l’aide d’Azure AD, vous devez définir Azure AD comme fournisseur de revendications.</span><span class="sxs-lookup"><span data-stu-id="adcd8-143">If you want users to sign in by using Azure AD, you need to define Azure AD as a claims provider.</span></span> <span data-ttu-id="adcd8-144">En d’autres termes, vous devez spécifier un point de terminaison avec lequel Azure AD B2C communiquera.</span><span class="sxs-lookup"><span data-stu-id="adcd8-144">In other words, you need to specify an endpoint that Azure AD B2C will communicate with.</span></span> <span data-ttu-id="adcd8-145">Le point de terminaison fournit un ensemble de revendications utilisées par Azure AD B2C pour vérifier qu’un utilisateur spécifique s’est authentifié.</span><span class="sxs-lookup"><span data-stu-id="adcd8-145">The endpoint will provide a set of claims that are used by Azure AD B2C to verify that a specific user has authenticated.</span></span> 

<span data-ttu-id="adcd8-146">Vous pouvez définir Azure AD comme fournisseur de revendications en ajoutant Azure AD au nœud `<ClaimsProvider>` dans le fichier d’extension de votre stratégie :</span><span class="sxs-lookup"><span data-stu-id="adcd8-146">You can define Azure AD as a claims provider by adding Azure AD to the `<ClaimsProvider>` node in the extension file of your policy:</span></span>

1. <span data-ttu-id="adcd8-147">Ouvrez le fichier d’extension (TrustFrameworkExtensions.xml) à partir de votre répertoire de travail.</span><span class="sxs-lookup"><span data-stu-id="adcd8-147">Open the extension file (TrustFrameworkExtensions.xml) from your working directory.</span></span>
1. <span data-ttu-id="adcd8-148">Recherchez la section `<ClaimsProviders>`.</span><span class="sxs-lookup"><span data-stu-id="adcd8-148">Find the `<ClaimsProviders>` section.</span></span> <span data-ttu-id="adcd8-149">Si elle n’existe pas, ajoutez-la sous le nœud racine.</span><span class="sxs-lookup"><span data-stu-id="adcd8-149">If it does not exist, add it under the root node.</span></span>
1. <span data-ttu-id="adcd8-150">Ajoutez un nœud `<ClaimsProvider>` comme suit :</span><span class="sxs-lookup"><span data-stu-id="adcd8-150">Add a new `<ClaimsProvider>` node as follows:</span></span>

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

1. <span data-ttu-id="adcd8-151">Sous le nœud `<ClaimsProvider>`, mettez à jour la valeur de `<Domain>` sur une valeur unique utilisable pour la distinguer d’autres fournisseurs d’identité.</span><span class="sxs-lookup"><span data-stu-id="adcd8-151">Under the `<ClaimsProvider>` node, update the value for `<Domain>` to a unique value that can be used to distinguish it from other identity providers.</span></span>
1. <span data-ttu-id="adcd8-152">Sous le nœud `<ClaimsProvider>`, mettez à jour la valeur de `<DisplayName>` sur un nom convivial pour le fournisseur de revendications.</span><span class="sxs-lookup"><span data-stu-id="adcd8-152">Under the `<ClaimsProvider>` node, update the value for `<DisplayName>` to a friendly name for the claims provider.</span></span> <span data-ttu-id="adcd8-153">Cette valeur n’est pas utilisée actuellement.</span><span class="sxs-lookup"><span data-stu-id="adcd8-153">This value is not currently used.</span></span>

### <a name="update-the-technical-profile"></a><span data-ttu-id="adcd8-154">Mise à jour du profil technique</span><span class="sxs-lookup"><span data-stu-id="adcd8-154">Update the technical profile</span></span>

<span data-ttu-id="adcd8-155">Pour obtenir un jeton à partir du point de terminaison Azure AD, vous devez définir les protocoles qu’Azure AD B2C doit utiliser pour communiquer avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="adcd8-155">To get a token from the Azure AD endpoint, you need to define the protocols that Azure AD B2C should use to communicate with Azure AD.</span></span> <span data-ttu-id="adcd8-156">Cela s’effectue à l’intérieur de l’élément `<TechnicalProfile>` de `<ClaimsProvider>`.</span><span class="sxs-lookup"><span data-stu-id="adcd8-156">This is done inside the `<TechnicalProfile>` element of  `<ClaimsProvider>`.</span></span>
1. <span data-ttu-id="adcd8-157">Mettez à jour l’ID du nœud `<TechnicalProfile>`.</span><span class="sxs-lookup"><span data-stu-id="adcd8-157">Update the ID of the `<TechnicalProfile>` node.</span></span> <span data-ttu-id="adcd8-158">Cet ID est utilisé pour faire référence à ce profil technique à partir d’autres parties de la stratégie.</span><span class="sxs-lookup"><span data-stu-id="adcd8-158">This ID is used to refer to this technical profile from other parts of the policy.</span></span>
1. <span data-ttu-id="adcd8-159">Mettez à jour la valeur pour `<DisplayName>`.</span><span class="sxs-lookup"><span data-stu-id="adcd8-159">Update the value for `<DisplayName>`.</span></span> <span data-ttu-id="adcd8-160">Cette valeur s’affiche sur le bouton Se connecter dans votre écran de connexion.</span><span class="sxs-lookup"><span data-stu-id="adcd8-160">This value will be displayed on the sign-in button on your sign-in screen.</span></span>
1. <span data-ttu-id="adcd8-161">Mettez à jour la valeur pour `<Description>`.</span><span class="sxs-lookup"><span data-stu-id="adcd8-161">Update the value for `<Description>`.</span></span>
1. <span data-ttu-id="adcd8-162">Azure AD utilisant le protocole OpenID Connect, vérifiez que la valeur de `<Protocol>` est bien `"OpenIdConnect"`.</span><span class="sxs-lookup"><span data-stu-id="adcd8-162">Azure AD uses the OpenID Connect protocol, so ensure that the value for `<Protocol>` is `"OpenIdConnect"`.</span></span>

<span data-ttu-id="adcd8-163">Vous devez mettre à jour la section `<Metadata>` dans le XML évoqué précédemment pour refléter les paramètres de configuration de votre locataire Azure AD spécifique.</span><span class="sxs-lookup"><span data-stu-id="adcd8-163">You need to update the `<Metadata>` section in the XML file referred to earlier to reflect the configuration settings for your specific Azure AD tenant.</span></span> <span data-ttu-id="adcd8-164">Dans le fichier XML, mettez à jour les valeurs des métadonnées comme suit :</span><span class="sxs-lookup"><span data-stu-id="adcd8-164">In the XML file, update the metadata values as follows:</span></span>

1. <span data-ttu-id="adcd8-165">Définissez `<Item Key="METADATA">` sur `https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, où `yourAzureADtenant` est le nom de votre locataire Azure AD (contoso.com).</span><span class="sxs-lookup"><span data-stu-id="adcd8-165">Set `<Item Key="METADATA">` to `https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, where `yourAzureADtenant` is your Azure AD tenant name (contoso.com).</span></span>
1. <span data-ttu-id="adcd8-166">Ouvrez votre navigateur, puis accédez à l’URL `METADATA` que vous venez de mettre à jour.</span><span class="sxs-lookup"><span data-stu-id="adcd8-166">Open your browser and go to the `METADATA` URL that you just updated.</span></span>
1. <span data-ttu-id="adcd8-167">Dans le navigateur, recherchez l’objet « issuer » et copiez sa valeur.</span><span class="sxs-lookup"><span data-stu-id="adcd8-167">In the browser, look for the 'issuer' object and copy its value.</span></span> <span data-ttu-id="adcd8-168">Elle doit ressembler à ceci : `https://sts.windows.net/{tenantId}/`.</span><span class="sxs-lookup"><span data-stu-id="adcd8-168">It should look like the following: `https://sts.windows.net/{tenantId}/`.</span></span>
1. <span data-ttu-id="adcd8-169">Collez la valeur de `<Item Key="ProviderName">` dans le fichier XML.</span><span class="sxs-lookup"><span data-stu-id="adcd8-169">Paste the value for `<Item Key="ProviderName">` in the XML file.</span></span>
1. <span data-ttu-id="adcd8-170">Définissez `<Item Key="client_id">` sur l’ID d’application de l’inscription de l’application.</span><span class="sxs-lookup"><span data-stu-id="adcd8-170">Set `<Item Key="client_id">` to the application ID from the app registration.</span></span>
1. <span data-ttu-id="adcd8-171">Définissez `<Item Key="IdTokenAudience">` sur l’ID d’application de l’inscription de l’application.</span><span class="sxs-lookup"><span data-stu-id="adcd8-171">Set `<Item Key="IdTokenAudience">` to the application ID from the app registration.</span></span>
1. <span data-ttu-id="adcd8-172">Vérifiez que `<Item Key="response_types">` est défini sur `id_token`.</span><span class="sxs-lookup"><span data-stu-id="adcd8-172">Ensure that `<Item Key="response_types">` is set to `id_token`.</span></span>
1. <span data-ttu-id="adcd8-173">Vérifiez que `<Item Key="UsePolicyInRedirectUri">` est défini sur `false`.</span><span class="sxs-lookup"><span data-stu-id="adcd8-173">Ensure that `<Item Key="UsePolicyInRedirectUri">` is set to `false`.</span></span>

<span data-ttu-id="adcd8-174">Vous devez également lier le secret Azure AD que vous avez inscrit dans votre locataire Azure AD B2C aux informations `<ClaimsProvider>` d’Azure AD :</span><span class="sxs-lookup"><span data-stu-id="adcd8-174">You also need to link the Azure AD secret that you registered in your Azure AD B2C tenant to the Azure AD `<ClaimsProvider>` information:</span></span>

* <span data-ttu-id="adcd8-175">Dans la section `<CryptographicKeys>` du fichier XML ci-dessus, mettez à jour la valeur pour `StorageReferenceId` sur l’ID de référence du secret que vous avez défini (par exemple, `ContosoAppSecret`).</span><span class="sxs-lookup"><span data-stu-id="adcd8-175">In the `<CryptographicKeys>` section in the preceding XML file, update the value for `StorageReferenceId` to the reference ID of the secret that you defined (for example, `ContosoAppSecret`).</span></span>

### <a name="upload-the-extension-file-for-verification"></a><span data-ttu-id="adcd8-176">Télécharger le fichier d’extension pour la vérification</span><span class="sxs-lookup"><span data-stu-id="adcd8-176">Upload the extension file for verification</span></span>

<span data-ttu-id="adcd8-177">À ce stade, vous avez configuré votre stratégie afin qu’Azure AD B2C sache comment communiquer avec votre répertoire Azure AD.</span><span class="sxs-lookup"><span data-stu-id="adcd8-177">By now, you have configured your policy so that Azure AD B2C knows how to communicate with your Azure AD directory.</span></span> <span data-ttu-id="adcd8-178">Essayez de télécharger le fichier d’extension de votre stratégie juste pour confirmer qu’il ne présente aucun problème pour le moment.</span><span class="sxs-lookup"><span data-stu-id="adcd8-178">Try uploading the extension file of your policy just to confirm that it doesn't have any issues so far.</span></span> <span data-ttu-id="adcd8-179">Pour ce faire :</span><span class="sxs-lookup"><span data-stu-id="adcd8-179">To do so:</span></span>

1. <span data-ttu-id="adcd8-180">Accédez au panneau **Toutes les stratégies** dans votre locataire Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="adcd8-180">Open the **All Policies** blade in your Azure AD B2C tenant.</span></span>
1. <span data-ttu-id="adcd8-181">Cochez la case **Remplacer la stratégie si elle existe**.</span><span class="sxs-lookup"><span data-stu-id="adcd8-181">Check the **Overwrite the policy if it exists** box.</span></span>
1. <span data-ttu-id="adcd8-182">Téléchargez le fichier d’extension (TrustFrameworkExtensions.xml) et vérifiez que sa validation n’échoue pas.</span><span class="sxs-lookup"><span data-stu-id="adcd8-182">Upload the extension file (TrustFrameworkExtensions.xml), and ensure that it does not fail the validation.</span></span>

## <a name="register-the-azure-ad-claims-provider-to-a-user-journey"></a><span data-ttu-id="adcd8-183">Inscrire le fournisseur de revendications AD Azure dans un parcours utilisateur</span><span class="sxs-lookup"><span data-stu-id="adcd8-183">Register the Azure AD claims provider to a user journey</span></span>

<span data-ttu-id="adcd8-184">Vous devez maintenant ajouter le fournisseur d’identité Azure AD à l’un de vos parcours utilisateur.</span><span class="sxs-lookup"><span data-stu-id="adcd8-184">You now need to add the Azure AD identity provider to one of your user journeys.</span></span> <span data-ttu-id="adcd8-185">À ce stade, le fournisseur d’identité a été configuré, mais il n’est disponible dans aucun des écrans d’inscription ou de connexion.</span><span class="sxs-lookup"><span data-stu-id="adcd8-185">At this point, the identity provider has been set up, but it’s not available in any of the sign-up/sign-in screens.</span></span> <span data-ttu-id="adcd8-186">Pour changer cela, nous créons un doublon d’un modèle de parcours utilisateur et le modifions afin qu’il dispose également du fournisseur d’identité Azure AD :</span><span class="sxs-lookup"><span data-stu-id="adcd8-186">To make it available, we will create a duplicate of an existing template user journey, and then modify it so that it also has the Azure AD identity provider:</span></span>

1. <span data-ttu-id="adcd8-187">Ouvrez le fichier de base de votre stratégie (par exemple, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="adcd8-187">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
1. <span data-ttu-id="adcd8-188">Recherchez l’élément `<UserJourneys>` et copiez l’ensemble du nœud `<UserJourney>` qui inclut `Id="SignUpOrSignIn"`.</span><span class="sxs-lookup"><span data-stu-id="adcd8-188">Find the `<UserJourneys>` element and copy the entire `<UserJourney>` node that includes `Id="SignUpOrSignIn"`.</span></span>
1. <span data-ttu-id="adcd8-189">Ouvrez le fichier d’extension (par exemple, TrustFrameworkExtensions.xml), puis recherchez l’élément `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="adcd8-189">Open the extension file (for example, TrustFrameworkExtensions.xml) and find the `<UserJourneys>` element.</span></span> <span data-ttu-id="adcd8-190">Si l’élément n’existe pas, ajoutez-en un.</span><span class="sxs-lookup"><span data-stu-id="adcd8-190">If the element doesn't exist, add one.</span></span>
1. <span data-ttu-id="adcd8-191">Collez l’intégralité du nœud `<UserJourney>` que vous avez copié en tant qu’enfant de l’élément `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="adcd8-191">Paste the entire `<UserJourney>` node that you copied as a child of the `<UserJourneys>` element.</span></span>
1. <span data-ttu-id="adcd8-192">Renommez l’ID du nouveau parcours utilisateur (par exemple, en `SignUpOrSignUsingContoso`).</span><span class="sxs-lookup"><span data-stu-id="adcd8-192">Rename the ID of the new user journey (for example, rename as `SignUpOrSignUsingContoso`).</span></span>

### <a name="display-the-button"></a><span data-ttu-id="adcd8-193">Afficher le « bouton »</span><span class="sxs-lookup"><span data-stu-id="adcd8-193">Display the "button"</span></span>

<span data-ttu-id="adcd8-194">L’élément `<ClaimsProviderSelection>` est analogue à un bouton de fournisseur d’identité sur un écran d’inscription/de connexion.</span><span class="sxs-lookup"><span data-stu-id="adcd8-194">The `<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up/sign-in screen.</span></span> <span data-ttu-id="adcd8-195">Si vous ajoutez un élément `<ClaimsProviderSelection>` pour Azure AD, un nouveau bouton apparaît quand un utilisateur accède à la page.</span><span class="sxs-lookup"><span data-stu-id="adcd8-195">If you add a `<ClaimsProviderSelection>` element for Azure AD, a new button shows up when a user lands on the page.</span></span> <span data-ttu-id="adcd8-196">Pour ajouter cet élément :</span><span class="sxs-lookup"><span data-stu-id="adcd8-196">To add this element:</span></span>

1. <span data-ttu-id="adcd8-197">Recherchez le nœud `<OrchestrationStep>` incluant `Order="1"` dans le parcours utilisateur que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="adcd8-197">Find the `<OrchestrationStep>` node that includes `Order="1"` in the user journey that you just created.</span></span>
1. <span data-ttu-id="adcd8-198">Ajoutez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="adcd8-198">Add the following:</span></span>

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

1. <span data-ttu-id="adcd8-199">Définissez `TargetClaimsExchangeId` sur une valeur appropriée.</span><span class="sxs-lookup"><span data-stu-id="adcd8-199">Set `TargetClaimsExchangeId` to an appropriate value.</span></span> <span data-ttu-id="adcd8-200">Nous vous recommandons de suivre la même convention que pour les autres : *\[ClaimProviderName\]Exchange*.</span><span class="sxs-lookup"><span data-stu-id="adcd8-200">We recommend following the same convention as others: *\[ClaimProviderName\]Exchange*.</span></span>

### <a name="link-the-button-to-an-action"></a><span data-ttu-id="adcd8-201">Lier le bouton à une action</span><span class="sxs-lookup"><span data-stu-id="adcd8-201">Link the button to an action</span></span>

<span data-ttu-id="adcd8-202">Maintenant que vous avez un bouton en place, vous devez le lier à une action.</span><span class="sxs-lookup"><span data-stu-id="adcd8-202">Now that you have a button in place, you need to link it to an action.</span></span> <span data-ttu-id="adcd8-203">L’action est, dans ce cas, la communication d’Azure AD B2C avec Azure AD pour recevoir un jeton.</span><span class="sxs-lookup"><span data-stu-id="adcd8-203">The action, in this case, is for Azure AD B2C to communicate with Azure AD to receive a token.</span></span> <span data-ttu-id="adcd8-204">Liez le bouton à une action en liant le profil technique de votre fournisseur de revendications Azure AD :</span><span class="sxs-lookup"><span data-stu-id="adcd8-204">Link the button to an action by linking the technical profile for your Azure AD claims provider:</span></span>

1. <span data-ttu-id="adcd8-205">Recherchez l’élément `<OrchestrationStep>` qui inclut `Order="2"` dans le nœud `<UserJourney>`.</span><span class="sxs-lookup"><span data-stu-id="adcd8-205">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
1. <span data-ttu-id="adcd8-206">Ajoutez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="adcd8-206">Add the following:</span></span>

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

1. <span data-ttu-id="adcd8-207">Mettez à jour `Id` sur la même valeur que celle de `TargetClaimsExchangeId` dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="adcd8-207">Update `Id` to the same value as that of `TargetClaimsExchangeId` in the preceding section.</span></span>
1. <span data-ttu-id="adcd8-208">Mettez à jour `TechnicalProfileReferenceId` sur l’ID du profil technique créé précédemment (ContosoProfile).</span><span class="sxs-lookup"><span data-stu-id="adcd8-208">Update `TechnicalProfileReferenceId` to the ID of the technical profile you created earlier (ContosoProfile).</span></span>

### <a name="upload-the-updated-extension-file"></a><span data-ttu-id="adcd8-209">Téléchargez le fichier d’extension mis à jour</span><span class="sxs-lookup"><span data-stu-id="adcd8-209">Upload the updated extension file</span></span>

<span data-ttu-id="adcd8-210">Vous avez terminé la modification du fichier d’extension.</span><span class="sxs-lookup"><span data-stu-id="adcd8-210">You are done modifying the extension file.</span></span> <span data-ttu-id="adcd8-211">Enregistrez-le.</span><span class="sxs-lookup"><span data-stu-id="adcd8-211">Save it.</span></span> <span data-ttu-id="adcd8-212">Chargez ensuite le fichier et vérifiez que toutes les validations réussissent.</span><span class="sxs-lookup"><span data-stu-id="adcd8-212">Then upload the file, and ensure that all validations succeed.</span></span>

### <a name="update-the-rp-file"></a><span data-ttu-id="adcd8-213">Mise à jour du fichier RP</span><span class="sxs-lookup"><span data-stu-id="adcd8-213">Update the RP file</span></span>

<span data-ttu-id="adcd8-214">Vous devez maintenant mettre à jour le fichier de partie de confiance qui initialisera le parcours utilisateur que vous venez de créer :</span><span class="sxs-lookup"><span data-stu-id="adcd8-214">You now need to update the relying party (RP) file that will initiate the user journey that you just created:</span></span>

1. <span data-ttu-id="adcd8-215">Effectuez une copie de SignUpOrSignIn.xml dans votre répertoire de travail et renommez-le (par exemple, SignUpOrSignInWithAAD.xml).</span><span class="sxs-lookup"><span data-stu-id="adcd8-215">Make a copy of SignUpOrSignIn.xml in your working directory, and rename it (for example, rename it to SignUpOrSignInWithAAD.xml).</span></span>
1. <span data-ttu-id="adcd8-216">Ouvrez le nouveau fichier et mettez à jour l’attribut `PolicyId` pour `<TrustFrameworkPolicy>` avec une valeur unique (par exemple, SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="adcd8-216">Open the new file and update the `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value (for example, SignUpOrSignInWithAAD).</span></span> <br> <span data-ttu-id="adcd8-217">Celle-ci correspond au nom de votre stratégie (par exemple, B2C\_1A\_SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="adcd8-217">This will be the name of your policy (for example, B2C\_1A\_SignUpOrSignInWithAAD).</span></span>
1. <span data-ttu-id="adcd8-218">Modifiez l’attribut `ReferenceId` dans `<DefaultUserJourney>` pour qu’il corresponde à l’ID du nouveau parcours utilisateur que vous avez créé (SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="adcd8-218">Modify the `ReferenceId` attribute in `<DefaultUserJourney>` to match the ID of the new user journey that you created (SignUpOrSignUsingContoso).</span></span>
1. <span data-ttu-id="adcd8-219">Enregistrez vos modifications et chargez le fichier.</span><span class="sxs-lookup"><span data-stu-id="adcd8-219">Save your changes, and upload the file.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="adcd8-220">Résolution de problèmes</span><span class="sxs-lookup"><span data-stu-id="adcd8-220">Troubleshooting</span></span>

<span data-ttu-id="adcd8-221">Testez la stratégie personnalisée que vous venez de charger en ouvrant son panneau et en cliquant sur **Exécuter maintenant**.</span><span class="sxs-lookup"><span data-stu-id="adcd8-221">Test the custom policy that you just uploaded by opening its blade and clicking **Run now**.</span></span> <span data-ttu-id="adcd8-222">Pour diagnostiquer des problèmes, consultez la page sur la [résolution des problèmes](active-directory-b2c-troubleshoot-custom.md).</span><span class="sxs-lookup"><span data-stu-id="adcd8-222">To diagnose problems, read about [troubleshooting](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="adcd8-223">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="adcd8-223">Next steps</span></span>

<span data-ttu-id="adcd8-224">Envoyez vos commentaires à l’adresse [AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="adcd8-224">Provide feedback to [AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span></span>
