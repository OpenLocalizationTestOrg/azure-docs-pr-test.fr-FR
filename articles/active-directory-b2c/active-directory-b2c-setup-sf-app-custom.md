---
title: "Azure Active Directory B2C : ajout d’un fournisseur SAML Salesforce à l’aide de stratégies personnalisées | Microsoft Docs"
description: "En savoir plus sur la façon de toocreate et gérer des stratégies personnalisées Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: d7f4143f-cd7c-4939-91a8-231a4104dc2c
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 06/11/2017
ms.author: parakhj
ms.openlocfilehash: f14c9d96980ff124110db7cfb58bf7cd81750b7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-salesforce-accounts-via-saml"></a><span data-ttu-id="c571c-103">Azure Active Directory B2C : connexion à l’aide de comptes Salesforce via SAML</span><span class="sxs-lookup"><span data-stu-id="c571c-103">Azure Active Directory B2C: Sign in by using Salesforce accounts via SAML</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="c571c-104">Cet article vous montre comment toouse [des stratégies personnalisées](active-directory-b2c-overview-custom.md) tooset des connectez-vous pour les utilisateurs à partir d’une organisation de force de vente spécifique.</span><span class="sxs-lookup"><span data-stu-id="c571c-104">This article shows you how toouse [custom policies](active-directory-b2c-overview-custom.md) tooset up sign-in for users from a specific Salesforce organization.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c571c-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c571c-105">Prerequisites</span></span>

### <a name="azure-ad-b2c-setup"></a><span data-ttu-id="c571c-106">Configuration d’Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="c571c-106">Azure AD B2C setup</span></span>

<span data-ttu-id="c571c-107">Vérifiez que vous avez effectué toutes les étapes de hello qui vous montrent comment trop[prise en main des stratégies personnalisées](active-directory-b2c-get-started-custom.md) dans Azure Active Directory B2C (B2C Active Directory de Azure).</span><span class="sxs-lookup"><span data-stu-id="c571c-107">Ensure that you have completed all of hello steps that show you how too[get started with custom policies](active-directory-b2c-get-started-custom.md) in Azure Active Directory B2C (Azure AD B2C).</span></span>

<span data-ttu-id="c571c-108">Vous avez notamment vu les points suivants :</span><span class="sxs-lookup"><span data-stu-id="c571c-108">These include:</span></span>

* <span data-ttu-id="c571c-109">Créer un locataire Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="c571c-109">Create an Azure AD B2C tenant.</span></span>
* <span data-ttu-id="c571c-110">Créer une application Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="c571c-110">Create an Azure AD B2C application.</span></span>
* <span data-ttu-id="c571c-111">Inscrire deux applications de moteur de stratégie</span><span class="sxs-lookup"><span data-stu-id="c571c-111">Register two policy engine applications.</span></span>
* <span data-ttu-id="c571c-112">Configurer des clés</span><span class="sxs-lookup"><span data-stu-id="c571c-112">Set up keys.</span></span>
* <span data-ttu-id="c571c-113">Configurer le pack de démarrage hello.</span><span class="sxs-lookup"><span data-stu-id="c571c-113">Set up hello starter pack.</span></span>

### <a name="salesforce-setup"></a><span data-ttu-id="c571c-114">Configuration Salesforce</span><span class="sxs-lookup"><span data-stu-id="c571c-114">Salesforce setup</span></span>

<span data-ttu-id="c571c-115">Dans cet article, nous supposons que vous avez déjà effectué les suivant hello :</span><span class="sxs-lookup"><span data-stu-id="c571c-115">In this article, we assume that you have already done hello following:</span></span>

* <span data-ttu-id="c571c-116">Vous êtes déjà inscrit à un compte Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c571c-116">Signed up for a Salesforce account.</span></span> <span data-ttu-id="c571c-117">Vous pouvez vous inscrire pour bénéficier d’un [compte Édition Développeur gratuit](https://developer.salesforce.com/signup).</span><span class="sxs-lookup"><span data-stu-id="c571c-117">You can sign up for a [free Developer Edition account](https://developer.salesforce.com/signup).</span></span>
* <span data-ttu-id="c571c-118">Vous avez déjà [configuré un domaine My Domain](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) pour votre organisation Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c571c-118">[Set up a My Domain](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) for your Salesforce organization.</span></span>

## <a name="set-up-salesforce-so-users-can-federate"></a><span data-ttu-id="c571c-119">Configurer Salesforce pour que les utilisateurs puissent fédérer</span><span class="sxs-lookup"><span data-stu-id="c571c-119">Set up Salesforce so users can federate</span></span>

<span data-ttu-id="c571c-120">toohelp Azure AD B2C communiquer avec Salesforce, vous avez besoin d’URL de métadonnées tooget hello Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c571c-120">toohelp Azure AD B2C communicate with Salesforce, you need tooget hello Salesforce metadata URL.</span></span>

### <a name="set-up-salesforce-as-an-identity-provider"></a><span data-ttu-id="c571c-121">Configurer Salesforce en tant que fournisseur d’identité</span><span class="sxs-lookup"><span data-stu-id="c571c-121">Set up Salesforce as an identity provider</span></span>

> [!NOTE]
> <span data-ttu-id="c571c-122">Dans cet article, nous supposons que vous utilisez [Salesforce Lightning Experience](https://developer.salesforce.com/page/Lightning_Experience_FAQ).</span><span class="sxs-lookup"><span data-stu-id="c571c-122">In this article, we assume you are using [Salesforce Lightning Experience](https://developer.salesforce.com/page/Lightning_Experience_FAQ).</span></span>

1. <span data-ttu-id="c571c-123">[Connectez-vous à tooSalesforce](https://login.salesforce.com/).</span><span class="sxs-lookup"><span data-stu-id="c571c-123">[Sign in tooSalesforce](https://login.salesforce.com/).</span></span> 
2. <span data-ttu-id="c571c-124">Dans hello gauche menu, sous **paramètres**, développez **identité**, puis cliquez sur **fournisseur d’identité**.</span><span class="sxs-lookup"><span data-stu-id="c571c-124">On hello left menu, under **Settings**, expand **Identity**, and then click **Identity Provider**.</span></span>
3. <span data-ttu-id="c571c-125">Cliquez sur **Enable Identity Provider (Activer le fournisseur d’identité)**.</span><span class="sxs-lookup"><span data-stu-id="c571c-125">Click **Enable Identity Provider**.</span></span>
4. <span data-ttu-id="c571c-126">Sous **certificat de hello sélectionnez**, sélectionnez certificat hello toocommunicate toouse de Salesforce avec Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="c571c-126">Under **Select hello certificate**, select hello certificate you want Salesforce toouse toocommunicate with Azure AD B2C.</span></span> <span data-ttu-id="c571c-127">(Vous pouvez utiliser de certificat par défaut de hello). Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="c571c-127">(You can use hello default certificate.) Click **Save**.</span></span> 

### <a name="create-a-connected-app-in-salesforce"></a><span data-ttu-id="c571c-128">Créer une application connectée dans Salesforce</span><span class="sxs-lookup"><span data-stu-id="c571c-128">Create a connected app in Salesforce</span></span>

1. <span data-ttu-id="c571c-129">Sur hello **fournisseur d’identité** page, aller trop**fournisseurs de services**.</span><span class="sxs-lookup"><span data-stu-id="c571c-129">On hello **Identity Provider** page, go too**Service Providers**.</span></span>
2. <span data-ttu-id="c571c-130">Cliquez sur **Service Providers are now created via Connected Apps (Les fournisseurs de services sont maintenant créés via des applications connectées). Cliquez ici.**</span><span class="sxs-lookup"><span data-stu-id="c571c-130">Click **Service Providers are now created via Connected Apps. Click here.**</span></span>
3. <span data-ttu-id="c571c-131">Sous **des informations de base**, entrez les valeurs hello requis pour votre application connectée.</span><span class="sxs-lookup"><span data-stu-id="c571c-131">Under **Basic Information**,  enter hello required values for your connected app.</span></span>
4. <span data-ttu-id="c571c-132">Sous **paramètres de l’application Web**, sélectionnez hello **SAML d’activer** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="c571c-132">Under **Web App Settings**, select hello **Enable SAML** check box.</span></span>
5. <span data-ttu-id="c571c-133">Bonjour **ID d’entité** , saisissez hello suivant l’URL.</span><span class="sxs-lookup"><span data-stu-id="c571c-133">In hello **Entity ID** field, enter hello following URL.</span></span> <span data-ttu-id="c571c-134">Veillez à remplacer la valeur hello pour `tenantName`.</span><span class="sxs-lookup"><span data-stu-id="c571c-134">Ensure that you replace hello value for `tenantName`.</span></span>
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase
      ```
6. <span data-ttu-id="c571c-135">Bonjour **URL ACS** , saisissez hello suivant l’URL.</span><span class="sxs-lookup"><span data-stu-id="c571c-135">In hello **ACS URL** field, enter hello following URL.</span></span> <span data-ttu-id="c571c-136">Veillez à remplacer la valeur hello pour `tenantName`.</span><span class="sxs-lookup"><span data-stu-id="c571c-136">Ensure that you replace hello value for `tenantName`.</span></span>
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase/samlp/sso/assertionconsumer
      ```
7. <span data-ttu-id="c571c-137">Laissez les valeurs par défaut de hello pour tous les autres paramètres.</span><span class="sxs-lookup"><span data-stu-id="c571c-137">Leave hello default values for all other settings.</span></span>
8. <span data-ttu-id="c571c-138">Faites défiler bas toohello de liste de hello, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="c571c-138">Scroll toohello bottom of hello list, and then click **Save**.</span></span>

### <a name="get-hello-metadata-url"></a><span data-ttu-id="c571c-139">Obtenir l’URL des métadonnées de hello</span><span class="sxs-lookup"><span data-stu-id="c571c-139">Get hello metadata URL</span></span>

1. <span data-ttu-id="c571c-140">Sur la page de vue d’ensemble de hello de votre application connectée, cliquez sur **gérer**.</span><span class="sxs-lookup"><span data-stu-id="c571c-140">On hello overview page of your connected app, click **Manage**.</span></span>
2. <span data-ttu-id="c571c-141">Copiez la valeur hello pour **point de terminaison de métadonnées de découverte**, puis enregistrez-le.</span><span class="sxs-lookup"><span data-stu-id="c571c-141">Copy hello value for **Metadata Discovery Endpoint**, and then save it.</span></span> <span data-ttu-id="c571c-142">Vous l’utiliserez plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="c571c-142">You'll use it later in this article.</span></span>

### <a name="set-up-salesforce-users-toofederate"></a><span data-ttu-id="c571c-143">Configurer la force de vente utilisateurs toofederate</span><span class="sxs-lookup"><span data-stu-id="c571c-143">Set up Salesforce users toofederate</span></span>

1. <span data-ttu-id="c571c-144">Sur hello **gérer** page de votre application connectée, accédez trop**profils**.</span><span class="sxs-lookup"><span data-stu-id="c571c-144">On hello **Manage** page of your connected app, go too**Profiles**.</span></span>
2. <span data-ttu-id="c571c-145">Cliquez sur **Manage Profiles (Gérer les profils)**.</span><span class="sxs-lookup"><span data-stu-id="c571c-145">Click **Manage Profiles**.</span></span>
3. <span data-ttu-id="c571c-146">Sélectionnez les profils hello (ou groupes d’utilisateurs) que vous souhaitez toofederate avec Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="c571c-146">Select hello profiles (or groups of users) that you want toofederate with Azure AD B2C.</span></span> <span data-ttu-id="c571c-147">En tant qu’un administrateur système, sélectionnez hello **administrateur système** case, afin que vous pouvez fédérer à l’aide de votre compte Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c571c-147">As a system administrator, select hello **System Administrator** check box, so that you can federate by using your Salesforce account.</span></span>

## <a name="generate-a-signing-certificate-for-azure-ad-b2c"></a><span data-ttu-id="c571c-148">Générer un certificat de signature pour Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="c571c-148">Generate a signing certificate for Azure AD B2C</span></span>

<span data-ttu-id="c571c-149">Les demandes envoyées tooSalesforce besoin toobe est signé par Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="c571c-149">Requests sent tooSalesforce need toobe signed by Azure AD B2C.</span></span> <span data-ttu-id="c571c-150">toogenerate un certificat de signature, ouvrez Azure PowerShell et exécutez hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="c571c-150">toogenerate a signing certificate, open Azure PowerShell, and then run hello following commands.</span></span>

> [!NOTE]
> <span data-ttu-id="c571c-151">Assurez-vous que vous mettez à jour nom hello du client et le mot de passe dans les premières lignes de deux hello.</span><span class="sxs-lookup"><span data-stu-id="c571c-151">Make sure that you update hello tenant name and password in hello top two lines.</span></span>

```PowerShell
$tenantName = "<YOUR TENANT NAME>.onmicrosoft.com"
$pwdText = "<YOUR PASSWORD HERE>"

$Cert = New-SelfSignedCertificate -CertStoreLocation Cert:\CurrentUser\My -DnsName "SamlIdp.$tenantName" -Subject "B2C SAML Signing Cert" -HashAlgorithm SHA256 -KeySpec Signature -KeyLength 2048

$pwd = ConvertTo-SecureString -String $pwdText -Force -AsPlainText

Export-PfxCertificate -Cert $Cert -FilePath .\B2CSigningCert.pfx -Password $pwd
```

## <a name="add-hello-saml-signing-certificate-tooazure-ad-b2c"></a><span data-ttu-id="c571c-152">Ajouter tooAzure de certificat signature hello SAML AD B2C</span><span class="sxs-lookup"><span data-stu-id="c571c-152">Add hello SAML signing certificate tooAzure AD B2C</span></span>

<span data-ttu-id="c571c-153">Télécharger hello client tooyour Azure AD B2C de certificat de signature :</span><span class="sxs-lookup"><span data-stu-id="c571c-153">Upload hello signing certificate tooyour Azure AD B2C tenant:</span></span> 

1. <span data-ttu-id="c571c-154">Accédez tooyour Azure AD B2C locataire.</span><span class="sxs-lookup"><span data-stu-id="c571c-154">Go tooyour Azure AD B2C tenant.</span></span> <span data-ttu-id="c571c-155">Cliquez sur **Paramètres** > **Infrastructure d’expérience d’identité** > **Clés de stratégie**.</span><span class="sxs-lookup"><span data-stu-id="c571c-155">Click **Settings** > **Identity Experience Framework** > **Policy Keys**.</span></span>
2. <span data-ttu-id="c571c-156">Cliquez sur **+Ajouter**, puis :</span><span class="sxs-lookup"><span data-stu-id="c571c-156">Click **+Add**, and then:</span></span>
    1. <span data-ttu-id="c571c-157">Cliquez sur **Options** > **Charger**.</span><span class="sxs-lookup"><span data-stu-id="c571c-157">Click **Options** > **Upload**.</span></span>
    2. <span data-ttu-id="c571c-158">Entrez un **Nom** (par exemple, SAMLSigningCert).</span><span class="sxs-lookup"><span data-stu-id="c571c-158">Enter a **Name** (for example, SAMLSigningCert).</span></span> <span data-ttu-id="c571c-159">préfixe de Hello *B2C_1A_* est automatiquement ajouté nom toohello de votre clé.</span><span class="sxs-lookup"><span data-stu-id="c571c-159">hello prefix *B2C_1A_* is automatically added toohello name of your key.</span></span>
    3. <span data-ttu-id="c571c-160">tooselect votre certificat, sélectionnez **contrôle du fichier de téléchargement**.</span><span class="sxs-lookup"><span data-stu-id="c571c-160">tooselect your certificate, select **upload file control**.</span></span> 
    4. <span data-ttu-id="c571c-161">Entrez le mot de passe du certificat hello que vous définissez dans le script PowerShell de hello.</span><span class="sxs-lookup"><span data-stu-id="c571c-161">Enter hello certificate's password that you set in hello PowerShell script.</span></span>
3. <span data-ttu-id="c571c-162">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="c571c-162">Click **Create**.</span></span>
4. <span data-ttu-id="c571c-163">Vérifiez que vous avez créé une clé (par exemple, B2C_1A_SAMLSigningCert).</span><span class="sxs-lookup"><span data-stu-id="c571c-163">Verify that you've created a key (for example, B2C_1A_SAMLSigningCert).</span></span> <span data-ttu-id="c571c-164">Prenez note du nom complet de hello (y compris *B2C_1A_*).</span><span class="sxs-lookup"><span data-stu-id="c571c-164">Take note of hello full name (including *B2C_1A_*).</span></span> <span data-ttu-id="c571c-165">Vous ferez référence clé toothis plus loin dans la stratégie de hello.</span><span class="sxs-lookup"><span data-stu-id="c571c-165">You will refer toothis key later in hello policy.</span></span>

## <a name="create-hello-salesforce-saml-claims-provider-in-your-base-policy"></a><span data-ttu-id="c571c-166">Créer hello fournisseur de revendications Salesforce SAML dans votre stratégie de base</span><span class="sxs-lookup"><span data-stu-id="c571c-166">Create hello Salesforce SAML claims provider in your base policy</span></span>

<span data-ttu-id="c571c-167">Vous devez toodefine Salesforce comme fournisseur de revendications pour les utilisateurs peuvent se connecter à l’aide de Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c571c-167">You need toodefine Salesforce as a claims provider so users can sign in by using Salesforce.</span></span> <span data-ttu-id="c571c-168">En d’autres termes, vous devez toospecify hello point de terminaison qui communiquent avec Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="c571c-168">In other words, you need toospecify hello endpoint that Azure AD B2C will communicate with.</span></span> <span data-ttu-id="c571c-169">point de terminaison Hello sera *fournir* un ensemble de *revendications* que Azure AD B2C utilise tooverify authentifié un utilisateur spécifique.</span><span class="sxs-lookup"><span data-stu-id="c571c-169">hello endpoint will *provide* a set of *claims* that Azure AD B2C uses tooverify that a specific user has authenticated.</span></span> <span data-ttu-id="c571c-170">toodo, ajoutez un `<ClaimsProvider>` pour Salesforce dans le fichier d’extension hello de votre stratégie :</span><span class="sxs-lookup"><span data-stu-id="c571c-170">toodo this, add a `<ClaimsProvider>` for Salesforce in hello extension file of your policy:</span></span>

1. <span data-ttu-id="c571c-171">Dans votre répertoire de travail, ouvrez le fichier d’extension hello (TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="c571c-171">In your working directory, open hello extension file (TrustFrameworkExtensions.xml).</span></span>
2. <span data-ttu-id="c571c-172">Recherche hello `<ClaimsProviders>` section.</span><span class="sxs-lookup"><span data-stu-id="c571c-172">Find hello `<ClaimsProviders>` section.</span></span> <span data-ttu-id="c571c-173">Si elle n’existe pas, créez-le sous le nœud racine de hello.</span><span class="sxs-lookup"><span data-stu-id="c571c-173">If it does not exist, create it under hello root node.</span></span>
3. <span data-ttu-id="c571c-174">Ajoutez un `<ClaimsProvider>` :</span><span class="sxs-lookup"><span data-stu-id="c571c-174">Add a new `<ClaimsProvider>`:</span></span>

    ```XML
    <ClaimsProvider>
      <Domain>salesforce</Domain>
      <DisplayName>Salesforce</DisplayName>
      <TechnicalProfiles>
        <TechnicalProfile Id="salesforce">
          <DisplayName>Salesforce</DisplayName>
          <Description>Login with your Salesforce account</Description>
          <Protocol Name="SAML2"/>
          <Metadata>
            <Item Key="RequestsSigned">false</Item>
            <Item Key="WantsEncryptedAssertions">false</Item>
            <Item Key="WantsSignedAssertions">false</Item>
            <Item Key="PartnerEntity">https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp.xml</Item>
          </Metadata>
          <CryptographicKeys>
            <Key Id="SamlAssertionSigning" StorageReferenceId="B2C_1A_SAMLSigningCert"/>
            <Key Id="SamlMessageSigning" StorageReferenceId="B2C_1A_SAMLSigningCert"/>
          </CryptographicKeys>
          <OutputClaims>
            <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="userId"/>
            <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name"/>
            <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name"/>
            <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email"/>
            <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="username"/>
            <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="externalIdp"/>
            <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="SAMLIdp" />
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

<span data-ttu-id="c571c-175">Sous hello `<ClaimsProvider>` nœud :</span><span class="sxs-lookup"><span data-stu-id="c571c-175">Under hello `<ClaimsProvider>` node:</span></span>

1. <span data-ttu-id="c571c-176">Modifier la valeur hello pour `<Domain>` tooa valeur unique qui distingue `<ClaimsProvider>` à partir d’autres fournisseurs d’identité.</span><span class="sxs-lookup"><span data-stu-id="c571c-176">Change hello value for `<Domain>` tooa unique value that distinguishes `<ClaimsProvider>` from other identity providers.</span></span>
2. <span data-ttu-id="c571c-177">Mettre à jour la valeur hello pour `<DisplayName>` fournisseur de revendications de nom d’affichage tooa pour hello.</span><span class="sxs-lookup"><span data-stu-id="c571c-177">Update hello value for `<DisplayName>` tooa display name for hello claims provider.</span></span> <span data-ttu-id="c571c-178">Cette valeur n’est pas utilisée actuellement.</span><span class="sxs-lookup"><span data-stu-id="c571c-178">Currently, this value is not used.</span></span>

### <a name="update-hello-technical-profile"></a><span data-ttu-id="c571c-179">Mettre à jour le profil de technique hello</span><span class="sxs-lookup"><span data-stu-id="c571c-179">Update hello technical profile</span></span>

<span data-ttu-id="c571c-180">tooget un jeton SAML de Salesforce, définir des protocoles hello que Azure AD B2C utilisera toocommunicate avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c571c-180">tooget a SAML token from Salesforce, define hello protocols that Azure AD B2C will use toocommunicate with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="c571c-181">Cela Bonjour `<TechnicalProfile>` élément de `<ClaimsProvider>`:</span><span class="sxs-lookup"><span data-stu-id="c571c-181">Do this in hello `<TechnicalProfile>` element of `<ClaimsProvider>`:</span></span>

1. <span data-ttu-id="c571c-182">Mise à jour ID hello Hello `<TechnicalProfile>` nœud.</span><span class="sxs-lookup"><span data-stu-id="c571c-182">Update hello ID of hello `<TechnicalProfile>` node.</span></span> <span data-ttu-id="c571c-183">Cet ID est utilisé toorefer toothis profil technique à partir d’autres parties de la stratégie de hello.</span><span class="sxs-lookup"><span data-stu-id="c571c-183">This ID is used toorefer toothis technical profile from other parts of hello policy.</span></span>
2. <span data-ttu-id="c571c-184">Mettre à jour la valeur hello pour `<DisplayName>`.</span><span class="sxs-lookup"><span data-stu-id="c571c-184">Update hello value for `<DisplayName>`.</span></span> <span data-ttu-id="c571c-185">Cette valeur est affichée sur le bouton hello de connexion dans votre page de connexion.</span><span class="sxs-lookup"><span data-stu-id="c571c-185">This value is displayed on hello sign-in button on your sign-in page.</span></span>
3. <span data-ttu-id="c571c-186">Mettre à jour la valeur hello pour `<Description>`.</span><span class="sxs-lookup"><span data-stu-id="c571c-186">Update hello value for `<Description>`.</span></span>
4. <span data-ttu-id="c571c-187">Force de vente utilise le protocole de hello SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="c571c-187">Salesforce uses hello SAML 2.0 protocol.</span></span> <span data-ttu-id="c571c-188">Que cette valeur hello `<Protocol>` est **SAML2**.</span><span class="sxs-lookup"><span data-stu-id="c571c-188">Ensure that hello value for `<Protocol>` is **SAML2**.</span></span>

<span data-ttu-id="c571c-189">Hello de mise à jour `<Metadata>` section Bonjour précédant les paramètres XML tooreflect hello pour votre compte Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c571c-189">Update hello `<Metadata>` section in hello preceding XML tooreflect hello settings for your specific Salesforce account.</span></span> <span data-ttu-id="c571c-190">Bonjour XML, mettez à jour les valeurs de métadonnées hello :</span><span class="sxs-lookup"><span data-stu-id="c571c-190">In hello XML, update hello metadata values:</span></span>

1. <span data-ttu-id="c571c-191">Mettre à jour la valeur hello `<Item Key="PartnerEntity">` avec l’URL de métadonnées hello Salesforce vous avez copiée précédemment.</span><span class="sxs-lookup"><span data-stu-id="c571c-191">Update hello value of `<Item Key="PartnerEntity">` with hello Salesforce metadata URL you copied earlier.</span></span> <span data-ttu-id="c571c-192">Il a hello suivant le format :</span><span class="sxs-lookup"><span data-stu-id="c571c-192">It has hello following format:</span></span> 

    `https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp/connectedapp.xml`

2. <span data-ttu-id="c571c-193">Bonjour `<CryptographicKeys>` section, la valeur hello de mise à jour pour les deux instances de `StorageReferenceId` nom toohello de clé hello de votre certificat de signature (par exemple, B2C_1A_SAMLSigningCert).</span><span class="sxs-lookup"><span data-stu-id="c571c-193">In hello `<CryptographicKeys>` section, update hello value for both instances of `StorageReferenceId` toohello name of hello key of your signing certificate (for example, B2C_1A_SAMLSigningCert).</span></span>

### <a name="upload-hello-extension-file-for-verification"></a><span data-ttu-id="c571c-194">Télécharger le fichier d’extension hello pour la vérification</span><span class="sxs-lookup"><span data-stu-id="c571c-194">Upload hello extension file for verification</span></span>

<span data-ttu-id="c571c-195">Votre stratégie est désormais configurée pour que Azure AD B2C sait comment toocommunicate auprès de Salesforce.</span><span class="sxs-lookup"><span data-stu-id="c571c-195">Your policy is now configured so that Azure AD B2C knows how toocommunicate with Salesforce.</span></span> <span data-ttu-id="c571c-196">Essayez de télécharger le fichier d’extension hello de votre stratégie, tooverify qu’il ne sont pas tous les problèmes jusqu'à présent.</span><span class="sxs-lookup"><span data-stu-id="c571c-196">Try uploading hello extension file of your policy, tooverify that there aren't any issues so far.</span></span> <span data-ttu-id="c571c-197">fichier d’extension tooupload hello de votre stratégie :</span><span class="sxs-lookup"><span data-stu-id="c571c-197">tooupload hello extension file of your policy:</span></span>

1. <span data-ttu-id="c571c-198">Dans votre locataire Azure AD B2C, accédez à toohello **toutes les stratégies** panneau.</span><span class="sxs-lookup"><span data-stu-id="c571c-198">In your Azure AD B2C tenant, go toohello **All Policies** blade.</span></span>
2. <span data-ttu-id="c571c-199">Sélectionnez hello **remplacer la stratégie de hello si elle existe** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="c571c-199">Select hello **Overwrite hello policy if it exists** check box.</span></span>
3. <span data-ttu-id="c571c-200">Téléchargez le fichier d’extension hello (TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="c571c-200">Upload hello extension file (TrustFrameworkExtensions.xml).</span></span> <span data-ttu-id="c571c-201">Vérifiez que sa validation n’échoue pas.</span><span class="sxs-lookup"><span data-stu-id="c571c-201">Ensure that it doesn't fail validation.</span></span>

## <a name="register-hello-salesforce-saml-claims-provider-tooa-user-journey"></a><span data-ttu-id="c571c-202">Inscrire hello voyage de Salesforce SAML revendications fournisseur tooa utilisateur</span><span class="sxs-lookup"><span data-stu-id="c571c-202">Register hello Salesforce SAML claims provider tooa user journey</span></span>

<span data-ttu-id="c571c-203">Ensuite, ajoutez hello tooone de fournisseur d’identité Salesforce SAML de votre parcours de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c571c-203">Next, add hello Salesforce SAML identity provider tooone of your user journeys.</span></span> <span data-ttu-id="c571c-204">À ce stade, le fournisseur d’identité hello a été configuré, mais il n’est pas disponible sur les pages d’inscription ou de la connexion du utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="c571c-204">At this point, hello identity provider has been set up, but it’s not available on any of hello user sign-up or sign-in pages.</span></span> <span data-ttu-id="c571c-205">tooadd hello identité fournisseur tooa-page de connexion, commencez par créer un doublon d’un déplacement de modèle à l’utilisateur existant.</span><span class="sxs-lookup"><span data-stu-id="c571c-205">tooadd hello identity provider tooa sign-in page, first, create a duplicate of an existing template user journey.</span></span> <span data-ttu-id="c571c-206">Ensuite, modifiez le modèle de hello afin qu’il puisse également le fournisseur d’identité Azure AD hello.</span><span class="sxs-lookup"><span data-stu-id="c571c-206">Then, modify hello template so that it also has hello Azure AD identity provider.</span></span>

1. <span data-ttu-id="c571c-207">Ouvrez le fichier de base hello de votre stratégie (par exemple, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="c571c-207">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2. <span data-ttu-id="c571c-208">Recherche hello `<UserJourneys>` élément, puis hello copie entière `<UserJourney>` valeur, Id = « SignUpOrSignIn ».</span><span class="sxs-lookup"><span data-stu-id="c571c-208">Find hello `<UserJourneys>` element, and then copy hello entire `<UserJourney>` value, including Id=”SignUpOrSignIn”.</span></span>
3. <span data-ttu-id="c571c-209">Ouvrez le fichier d’extension hello (par exemple, TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="c571c-209">Open hello extension file (for example, TrustFrameworkExtensions.xml).</span></span> <span data-ttu-id="c571c-210">Recherche hello `<UserJourneys>` élément.</span><span class="sxs-lookup"><span data-stu-id="c571c-210">Find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="c571c-211">Si l’élément de hello n’existe pas, créez-le.</span><span class="sxs-lookup"><span data-stu-id="c571c-211">If hello element doesn't exist, create one.</span></span>
4. <span data-ttu-id="c571c-212">Hello coller ensemble copié `<UserJourney>` en tant qu’enfant de hello `<UserJourneys>` élément.</span><span class="sxs-lookup"><span data-stu-id="c571c-212">Paste hello entire copied `<UserJourney>` as a child of hello `<UserJourneys>` element.</span></span>
5. <span data-ttu-id="c571c-213">Renommer des ID hello Hello nouvelle `<UserJourney>` (par exemple, SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="c571c-213">Rename hello ID of hello new `<UserJourney>` (for example, SignUpOrSignUsingContoso).</span></span>

### <a name="display-hello-identity-provider-button"></a><span data-ttu-id="c571c-214">Bouton d’affichage hello identité fournisseur</span><span class="sxs-lookup"><span data-stu-id="c571c-214">Display hello identity provider button</span></span>

<span data-ttu-id="c571c-215">Hello `<ClaimsProviderSelection>` élément est le bouton de fournisseur d’identité tooan analogue sur une page d’inscription ou de connexion.</span><span class="sxs-lookup"><span data-stu-id="c571c-215">hello `<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up or sign-in page.</span></span> <span data-ttu-id="c571c-216">En ajoutant un `<ClaimsProviderSelection>` élément pour Salesforce, un nouveau bouton s’affiche lorsqu’un utilisateur est toothis page.</span><span class="sxs-lookup"><span data-stu-id="c571c-216">By adding an `<ClaimsProviderSelection>` element for Salesforce, a new button appears when a user goes toothis page.</span></span> <span data-ttu-id="c571c-217">bouton de fournisseur toodisplay hello identité :</span><span class="sxs-lookup"><span data-stu-id="c571c-217">toodisplay hello identity provider button:</span></span>

1. <span data-ttu-id="c571c-218">Bonjour `<UserJourney>` que vous avez créé, recherche hello `<OrchestrationStep>` avec `Order="1"`.</span><span class="sxs-lookup"><span data-stu-id="c571c-218">In hello `<UserJourney>` that you created, find hello `<OrchestrationStep>` with `Order="1"`.</span></span>
2. <span data-ttu-id="c571c-219">Ajoutez hello XML suivant :</span><span class="sxs-lookup"><span data-stu-id="c571c-219">Add hello following XML:</span></span>

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

3. <span data-ttu-id="c571c-220">Définissez `TargetClaimsExchangeId` tooa les valeur logique.</span><span class="sxs-lookup"><span data-stu-id="c571c-220">Set `TargetClaimsExchangeId` tooa logical value.</span></span> <span data-ttu-id="c571c-221">Nous vous recommandons de suivant hello même convention que d’autres (par exemple,  *\[ClaimProviderName\]Exchange*).</span><span class="sxs-lookup"><span data-stu-id="c571c-221">We recommend following hello same convention as others (for example, *\[ClaimProviderName\]Exchange*).</span></span>

### <a name="link-hello-identity-provider-button-tooan-action"></a><span data-ttu-id="c571c-222">Action du lien hello identité fournisseur bouton tooan</span><span class="sxs-lookup"><span data-stu-id="c571c-222">Link hello identity provider button tooan action</span></span>

<span data-ttu-id="c571c-223">Maintenant que vous avez un bouton de fournisseur d’identité en place, liez-le tooan action.</span><span class="sxs-lookup"><span data-stu-id="c571c-223">Now that you have an identity provider button in place, link it tooan action.</span></span> <span data-ttu-id="c571c-224">Dans ce cas, l’action de hello est pour toocommunicate Azure AD B2C avec Salesforce tooreceive un jeton SAML.</span><span class="sxs-lookup"><span data-stu-id="c571c-224">In this case, hello action is for Azure AD B2C toocommunicate with Salesforce tooreceive a SAML token.</span></span> <span data-ttu-id="c571c-225">Faire cela en liant le profil de technique hello pour votre SAML Salesforce fournisseur de revendications :</span><span class="sxs-lookup"><span data-stu-id="c571c-225">You can do this by linking hello technical profile for your Salesforce SAML claims provider:</span></span>

1. <span data-ttu-id="c571c-226">Bonjour `<UserJourney>` nœud, rechercher hello `<OrchestrationStep>` avec `Order="2"`.</span><span class="sxs-lookup"><span data-stu-id="c571c-226">In hello `<UserJourney>` node, find hello `<OrchestrationStep>` with `Order="2"`.</span></span>
2. <span data-ttu-id="c571c-227">Ajoutez hello XML suivant :</span><span class="sxs-lookup"><span data-stu-id="c571c-227">Add hello following XML:</span></span>

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

3. <span data-ttu-id="c571c-228">Mise à jour `Id` toohello même valeur que vous avez utilisé précédemment pour `TargetClaimsExchangeId`.</span><span class="sxs-lookup"><span data-stu-id="c571c-228">Update `Id` toohello same value that you used earlier for `TargetClaimsExchangeId`.</span></span>
4. <span data-ttu-id="c571c-229">Mise à jour `TechnicalProfileReferenceId` toohello `Id` Hello technique du profil que vous avez créé précédemment (par exemple, ContosoProfile).</span><span class="sxs-lookup"><span data-stu-id="c571c-229">Update `TechnicalProfileReferenceId` toohello `Id` of hello technical profile you created earlier (for example, ContosoProfile).</span></span>

### <a name="upload-hello-updated-extension-file"></a><span data-ttu-id="c571c-230">Télécharger le fichier d’extension de mise à jour de hello</span><span class="sxs-lookup"><span data-stu-id="c571c-230">Upload hello updated extension file</span></span>

<span data-ttu-id="c571c-231">Vous avez terminé la modification d’extension hello.</span><span class="sxs-lookup"><span data-stu-id="c571c-231">You are done modifying hello extension file.</span></span> <span data-ttu-id="c571c-232">Enregistrez et chargez ce fichier.</span><span class="sxs-lookup"><span data-stu-id="c571c-232">Save and upload this file.</span></span> <span data-ttu-id="c571c-233">Faites en sorte que toutes les validations réussissent.</span><span class="sxs-lookup"><span data-stu-id="c571c-233">Ensure that all validations succeed.</span></span>

### <a name="update-hello-relying-party-file"></a><span data-ttu-id="c571c-234">Mettre à jour le fichier de partie de confiance hello</span><span class="sxs-lookup"><span data-stu-id="c571c-234">Update hello relying party file</span></span>

<span data-ttu-id="c571c-235">Ensuite, mettre à jour les hello fichier partie de confiance du tiers (RP) qui lance le voyage utilisateur hello que vous avez créé :</span><span class="sxs-lookup"><span data-stu-id="c571c-235">Next, update hello relying party (RP) file that initiates hello user journey that you created:</span></span>

1. <span data-ttu-id="c571c-236">Faites une copie de SignUpOrSignIn.xml dans votre répertoire de travail.</span><span class="sxs-lookup"><span data-stu-id="c571c-236">Make a copy of SignUpOrSignIn.xml in your working directory.</span></span> <span data-ttu-id="c571c-237">Ensuite, renommez-le (par exemple, SignUpOrSignInWithAAD.xml).</span><span class="sxs-lookup"><span data-stu-id="c571c-237">Then, rename it (for example, SignUpOrSignInWithAAD.xml).</span></span>
2. <span data-ttu-id="c571c-238">Hello de fichier et de mise à jour de nouveau hello ouvrir `PolicyId` attribut `<TrustFrameworkPolicy>` avec une valeur unique.</span><span class="sxs-lookup"><span data-stu-id="c571c-238">Open hello new file and update hello `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value.</span></span> <span data-ttu-id="c571c-239">Il s’agit de nom hello de votre stratégie (par exemple, SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="c571c-239">This is hello name of your policy (for example, SignUpOrSignInWithAAD).</span></span>
3. <span data-ttu-id="c571c-240">Modifier hello `ReferenceId` attribut `<DefaultUserJourney>` toomatch hello `Id` de hello nouvel utilisateur voyage que vous avez créé (par exemple, SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="c571c-240">Modify hello `ReferenceId` attribute in `<DefaultUserJourney>` toomatch hello `Id` of hello new user journey that you created (for example, SignUpOrSignUsingContoso).</span></span>
4. <span data-ttu-id="c571c-241">Enregistrer vos modifications et télécharger les fichiers hello.</span><span class="sxs-lookup"><span data-stu-id="c571c-241">Save your changes, and then upload hello file.</span></span>

## <a name="test-and-troubleshoot"></a><span data-ttu-id="c571c-242">Tester et résoudre les problèmes</span><span class="sxs-lookup"><span data-stu-id="c571c-242">Test and troubleshoot</span></span>

<span data-ttu-id="c571c-243">stratégie personnalisée tootest hello que vous venez de télécharger, Bonjour portail Azure, accédez toohello Panneau de la stratégie, puis cliquez sur **exécuter maintenant**.</span><span class="sxs-lookup"><span data-stu-id="c571c-243">tootest hello custom policy that you just uploaded, in hello Azure portal, go toohello policy blade, and then click **Run now**.</span></span> <span data-ttu-id="c571c-244">En cas d’échec, consultez [Résoudre les problèmes des stratégies personnalisées](active-directory-b2c-troubleshoot-custom.md).</span><span class="sxs-lookup"><span data-stu-id="c571c-244">If it fails, see [Troubleshoot custom policies](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c571c-245">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c571c-245">Next steps</span></span>

<span data-ttu-id="c571c-246">Fournir des commentaires trop[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="c571c-246">Provide feedback too[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span></span>
