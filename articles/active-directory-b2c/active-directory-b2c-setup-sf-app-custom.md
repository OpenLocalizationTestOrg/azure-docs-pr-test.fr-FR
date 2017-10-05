---
title: "Azure Active Directory B2C : ajout d’un fournisseur SAML Salesforce à l’aide de stratégies personnalisées | Microsoft Docs"
description: "Découvrez comment créer et gérer des stratégies personnalisées Azure Active Directory B2C."
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
ms.openlocfilehash: 269cbd80fb6e861fa8588025eec70b6c6e2890d7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-salesforce-accounts-via-saml"></a><span data-ttu-id="e34c4-103">Azure Active Directory B2C : connexion à l’aide de comptes Salesforce via SAML</span><span class="sxs-lookup"><span data-stu-id="e34c4-103">Azure Active Directory B2C: Sign in by using Salesforce accounts via SAML</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="e34c4-104">Cet article explique comment utiliser des [stratégies personnalisées](active-directory-b2c-overview-custom.md) afin de configurer la connexion pour les utilisateurs d’une organisation Salesforce spécifique.</span><span class="sxs-lookup"><span data-stu-id="e34c4-104">This article shows you how to use [custom policies](active-directory-b2c-overview-custom.md) to set up sign-in for users from a specific Salesforce organization.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e34c4-105">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="e34c4-105">Prerequisites</span></span>

### <a name="azure-ad-b2c-setup"></a><span data-ttu-id="e34c4-106">Configuration d’Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="e34c4-106">Azure AD B2C setup</span></span>

<span data-ttu-id="e34c4-107">Vérifiez que vous avez suivi toutes les étapes montrant comment [bien démarrer avec les stratégies personnalisées](active-directory-b2c-get-started-custom.md) dans Azure Active Directory B2C (Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="e34c4-107">Ensure that you have completed all of the steps that show you how to [get started with custom policies](active-directory-b2c-get-started-custom.md) in Azure Active Directory B2C (Azure AD B2C).</span></span>

<span data-ttu-id="e34c4-108">Vous avez notamment vu les points suivants :</span><span class="sxs-lookup"><span data-stu-id="e34c4-108">These include:</span></span>

* <span data-ttu-id="e34c4-109">Créer un locataire Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="e34c4-109">Create an Azure AD B2C tenant.</span></span>
* <span data-ttu-id="e34c4-110">Créer une application Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="e34c4-110">Create an Azure AD B2C application.</span></span>
* <span data-ttu-id="e34c4-111">Inscrire deux applications de moteur de stratégie</span><span class="sxs-lookup"><span data-stu-id="e34c4-111">Register two policy engine applications.</span></span>
* <span data-ttu-id="e34c4-112">Configurer des clés</span><span class="sxs-lookup"><span data-stu-id="e34c4-112">Set up keys.</span></span>
* <span data-ttu-id="e34c4-113">Configurer le pack de démarrage</span><span class="sxs-lookup"><span data-stu-id="e34c4-113">Set up the starter pack.</span></span>

### <a name="salesforce-setup"></a><span data-ttu-id="e34c4-114">Configuration Salesforce</span><span class="sxs-lookup"><span data-stu-id="e34c4-114">Salesforce setup</span></span>

<span data-ttu-id="e34c4-115">Dans cet article, nous partons du principe que vous avez déjà effectué les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="e34c4-115">In this article, we assume that you have already done the following:</span></span>

* <span data-ttu-id="e34c4-116">Vous êtes déjà inscrit à un compte Salesforce.</span><span class="sxs-lookup"><span data-stu-id="e34c4-116">Signed up for a Salesforce account.</span></span> <span data-ttu-id="e34c4-117">Vous pouvez vous inscrire pour bénéficier d’un [compte Édition Développeur gratuit](https://developer.salesforce.com/signup).</span><span class="sxs-lookup"><span data-stu-id="e34c4-117">You can sign up for a [free Developer Edition account](https://developer.salesforce.com/signup).</span></span>
* <span data-ttu-id="e34c4-118">Vous avez déjà [configuré un domaine My Domain](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) pour votre organisation Salesforce.</span><span class="sxs-lookup"><span data-stu-id="e34c4-118">[Set up a My Domain](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) for your Salesforce organization.</span></span>

## <a name="set-up-salesforce-so-users-can-federate"></a><span data-ttu-id="e34c4-119">Configurer Salesforce pour que les utilisateurs puissent fédérer</span><span class="sxs-lookup"><span data-stu-id="e34c4-119">Set up Salesforce so users can federate</span></span>

<span data-ttu-id="e34c4-120">Pour aider Azure AD B2C à communiquer avec Salesforce, vous devez obtenir l’URL de métadonnées de Salesforce.</span><span class="sxs-lookup"><span data-stu-id="e34c4-120">To help Azure AD B2C communicate with Salesforce, you need to get the Salesforce metadata URL.</span></span>

### <a name="set-up-salesforce-as-an-identity-provider"></a><span data-ttu-id="e34c4-121">Configurer Salesforce en tant que fournisseur d’identité</span><span class="sxs-lookup"><span data-stu-id="e34c4-121">Set up Salesforce as an identity provider</span></span>

> [!NOTE]
> <span data-ttu-id="e34c4-122">Dans cet article, nous supposons que vous utilisez [Salesforce Lightning Experience](https://developer.salesforce.com/page/Lightning_Experience_FAQ).</span><span class="sxs-lookup"><span data-stu-id="e34c4-122">In this article, we assume you are using [Salesforce Lightning Experience](https://developer.salesforce.com/page/Lightning_Experience_FAQ).</span></span>

1. <span data-ttu-id="e34c4-123">[Connectez-vous à Salesforce](https://login.salesforce.com/).</span><span class="sxs-lookup"><span data-stu-id="e34c4-123">[Sign in to Salesforce](https://login.salesforce.com/).</span></span> 
2. <span data-ttu-id="e34c4-124">Dans le menu de gauche, sous **Settings (Paramètres)**, développez **Identity (Identité)**, puis cliquez sur **Identity Provider (Fournisseur d’identité)**.</span><span class="sxs-lookup"><span data-stu-id="e34c4-124">On the left menu, under **Settings**, expand **Identity**, and then click **Identity Provider**.</span></span>
3. <span data-ttu-id="e34c4-125">Cliquez sur **Enable Identity Provider (Activer le fournisseur d’identité)**.</span><span class="sxs-lookup"><span data-stu-id="e34c4-125">Click **Enable Identity Provider**.</span></span>
4. <span data-ttu-id="e34c4-126">Sous **Select the certificate (Sélectionner le certificat)**, sélectionnez le certificat que vous souhaitez que Salesforce utilise pour communiquer avec Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="e34c4-126">Under **Select the certificate**, select the certificate you want Salesforce to use to communicate with Azure AD B2C.</span></span> <span data-ttu-id="e34c4-127">(vous pouvez utiliser le certificat par défaut). Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="e34c4-127">(You can use the default certificate.) Click **Save**.</span></span> 

### <a name="create-a-connected-app-in-salesforce"></a><span data-ttu-id="e34c4-128">Créer une application connectée dans Salesforce</span><span class="sxs-lookup"><span data-stu-id="e34c4-128">Create a connected app in Salesforce</span></span>

1. <span data-ttu-id="e34c4-129">Dans la page **Identity Provider (Fournisseur d’identité)**, accédez à **Service Providers (Fournisseurs de services)**.</span><span class="sxs-lookup"><span data-stu-id="e34c4-129">On the **Identity Provider** page, go to **Service Providers**.</span></span>
2. <span data-ttu-id="e34c4-130">Cliquez sur **Service Providers are now created via Connected Apps (Les fournisseurs de services sont maintenant créés via des applications connectées). Cliquez ici.**</span><span class="sxs-lookup"><span data-stu-id="e34c4-130">Click **Service Providers are now created via Connected Apps. Click here.**</span></span>
3. <span data-ttu-id="e34c4-131">Sous **Basic Information (Informations de base)**, entrez les valeurs requises pour votre application connectée.</span><span class="sxs-lookup"><span data-stu-id="e34c4-131">Under **Basic Information**,  enter the required values for your connected app.</span></span>
4. <span data-ttu-id="e34c4-132">Sous **Web App Settings (Paramètres de l’application web)**, activez la case à cocher **Enable SAML (Activer SAML)**.</span><span class="sxs-lookup"><span data-stu-id="e34c4-132">Under **Web App Settings**, select the **Enable SAML** check box.</span></span>
5. <span data-ttu-id="e34c4-133">Dans le champ **Entity ID (ID d’entité)**, entrez l’URL suivante.</span><span class="sxs-lookup"><span data-stu-id="e34c4-133">In the **Entity ID** field, enter the following URL.</span></span> <span data-ttu-id="e34c4-134">Veillez à remplacer la valeur de `tenantName`.</span><span class="sxs-lookup"><span data-stu-id="e34c4-134">Ensure that you replace the value for `tenantName`.</span></span>
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase
      ```
6. <span data-ttu-id="e34c4-135">Dans le champ **ACS URL (URL ACS)**, entrez l’URL suivante.</span><span class="sxs-lookup"><span data-stu-id="e34c4-135">In the **ACS URL** field, enter the following URL.</span></span> <span data-ttu-id="e34c4-136">Veillez à remplacer la valeur de `tenantName`.</span><span class="sxs-lookup"><span data-stu-id="e34c4-136">Ensure that you replace the value for `tenantName`.</span></span>
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase/samlp/sso/assertionconsumer
      ```
7. <span data-ttu-id="e34c4-137">Conservez les valeurs par défaut pour tous les autres paramètres.</span><span class="sxs-lookup"><span data-stu-id="e34c4-137">Leave the default values for all other settings.</span></span>
8. <span data-ttu-id="e34c4-138">Faites défiler vers le bas de la liste, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="e34c4-138">Scroll to the bottom of the list, and then click **Save**.</span></span>

### <a name="get-the-metadata-url"></a><span data-ttu-id="e34c4-139">Obtenir l’URL des métadonnées</span><span class="sxs-lookup"><span data-stu-id="e34c4-139">Get the metadata URL</span></span>

1. <span data-ttu-id="e34c4-140">Dans la page de présentation de votre application connectée, cliquez sur **Manage (Gérer)**.</span><span class="sxs-lookup"><span data-stu-id="e34c4-140">On the overview page of your connected app, click **Manage**.</span></span>
2. <span data-ttu-id="e34c4-141">Copiez la valeur de **point de terminaison de découverte des métadonnées**, puis enregistrez-la.</span><span class="sxs-lookup"><span data-stu-id="e34c4-141">Copy the value for **Metadata Discovery Endpoint**, and then save it.</span></span> <span data-ttu-id="e34c4-142">Vous l’utiliserez plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="e34c4-142">You'll use it later in this article.</span></span>

### <a name="set-up-salesforce-users-to-federate"></a><span data-ttu-id="e34c4-143">Configurer des utilisateurs Salesforce pour fédérer</span><span class="sxs-lookup"><span data-stu-id="e34c4-143">Set up Salesforce users to federate</span></span>

1. <span data-ttu-id="e34c4-144">Dans la page **Manage (Gérer)** de votre application connectée, accédez à **Profiles (Profils)**.</span><span class="sxs-lookup"><span data-stu-id="e34c4-144">On the **Manage** page of your connected app, go to **Profiles**.</span></span>
2. <span data-ttu-id="e34c4-145">Cliquez sur **Manage Profiles (Gérer les profils)**.</span><span class="sxs-lookup"><span data-stu-id="e34c4-145">Click **Manage Profiles**.</span></span>
3. <span data-ttu-id="e34c4-146">Sélectionnez les profils (ou groupes d’utilisateurs) que vous souhaitez fédérer avec Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="e34c4-146">Select the profiles (or groups of users) that you want to federate with Azure AD B2C.</span></span> <span data-ttu-id="e34c4-147">En tant qu’un administrateur système, activez la case à cocher **Administrateur système** afin de pouvoir fédérer à l’aide de votre compte Salesforce.</span><span class="sxs-lookup"><span data-stu-id="e34c4-147">As a system administrator, select the **System Administrator** check box, so that you can federate by using your Salesforce account.</span></span>

## <a name="generate-a-signing-certificate-for-azure-ad-b2c"></a><span data-ttu-id="e34c4-148">Générer un certificat de signature pour Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="e34c4-148">Generate a signing certificate for Azure AD B2C</span></span>

<span data-ttu-id="e34c4-149">Les demandes envoyées à Salesforce doivent être signées par Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="e34c4-149">Requests sent to Salesforce need to be signed by Azure AD B2C.</span></span> <span data-ttu-id="e34c4-150">Pour générer un certificat de signature, ouvrez Azure PowerShell, puis exécutez les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="e34c4-150">To generate a signing certificate, open Azure PowerShell, and then run the following commands.</span></span>

> [!NOTE]
> <span data-ttu-id="e34c4-151">Veillez à mettre à jour le nom et le mot de passe du locataire dans les deux lignes du haut.</span><span class="sxs-lookup"><span data-stu-id="e34c4-151">Make sure that you update the tenant name and password in the top two lines.</span></span>

```PowerShell
$tenantName = "<YOUR TENANT NAME>.onmicrosoft.com"
$pwdText = "<YOUR PASSWORD HERE>"

$Cert = New-SelfSignedCertificate -CertStoreLocation Cert:\CurrentUser\My -DnsName "SamlIdp.$tenantName" -Subject "B2C SAML Signing Cert" -HashAlgorithm SHA256 -KeySpec Signature -KeyLength 2048

$pwd = ConvertTo-SecureString -String $pwdText -Force -AsPlainText

Export-PfxCertificate -Cert $Cert -FilePath .\B2CSigningCert.pfx -Password $pwd
```

## <a name="add-the-saml-signing-certificate-to-azure-ad-b2c"></a><span data-ttu-id="e34c4-152">Ajouter un certificat de signature SAML à Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="e34c4-152">Add the SAML signing certificate to Azure AD B2C</span></span>

<span data-ttu-id="e34c4-153">Chargez le certificat de signature sur votre locataire Azure AD B2C :</span><span class="sxs-lookup"><span data-stu-id="e34c4-153">Upload the signing certificate to your Azure AD B2C tenant:</span></span> 

1. <span data-ttu-id="e34c4-154">Accédez à votre locataire Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="e34c4-154">Go to your Azure AD B2C tenant.</span></span> <span data-ttu-id="e34c4-155">Cliquez sur **Paramètres** > **Infrastructure d’expérience d’identité** > **Clés de stratégie**.</span><span class="sxs-lookup"><span data-stu-id="e34c4-155">Click **Settings** > **Identity Experience Framework** > **Policy Keys**.</span></span>
2. <span data-ttu-id="e34c4-156">Cliquez sur **+Ajouter**, puis :</span><span class="sxs-lookup"><span data-stu-id="e34c4-156">Click **+Add**, and then:</span></span>
    1. <span data-ttu-id="e34c4-157">Cliquez sur **Options** > **Charger**.</span><span class="sxs-lookup"><span data-stu-id="e34c4-157">Click **Options** > **Upload**.</span></span>
    2. <span data-ttu-id="e34c4-158">Entrez un **Nom** (par exemple, SAMLSigningCert).</span><span class="sxs-lookup"><span data-stu-id="e34c4-158">Enter a **Name** (for example, SAMLSigningCert).</span></span> <span data-ttu-id="e34c4-159">Le préfixe *B2C_1A_* est ajouté automatiquement au nom de votre clé.</span><span class="sxs-lookup"><span data-stu-id="e34c4-159">The prefix *B2C_1A_* is automatically added to the name of your key.</span></span>
    3. <span data-ttu-id="e34c4-160">Pour sélectionner votre certificat, choisissez **contrôle du fichier de téléchargement**.</span><span class="sxs-lookup"><span data-stu-id="e34c4-160">To select your certificate, select **upload file control**.</span></span> 
    4. <span data-ttu-id="e34c4-161">Entrez le mot de passe du certificat que vous avez défini dans le script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e34c4-161">Enter the certificate's password that you set in the PowerShell script.</span></span>
3. <span data-ttu-id="e34c4-162">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="e34c4-162">Click **Create**.</span></span>
4. <span data-ttu-id="e34c4-163">Vérifiez que vous avez créé une clé (par exemple, B2C_1A_SAMLSigningCert).</span><span class="sxs-lookup"><span data-stu-id="e34c4-163">Verify that you've created a key (for example, B2C_1A_SAMLSigningCert).</span></span> <span data-ttu-id="e34c4-164">Prenez note du nom complet (y compris *B2C_1A_*).</span><span class="sxs-lookup"><span data-stu-id="e34c4-164">Take note of the full name (including *B2C_1A_*).</span></span> <span data-ttu-id="e34c4-165">Vous ferez référence à cette clé plus loin dans la stratégie.</span><span class="sxs-lookup"><span data-stu-id="e34c4-165">You will refer to this key later in the policy.</span></span>

## <a name="create-the-salesforce-saml-claims-provider-in-your-base-policy"></a><span data-ttu-id="e34c4-166">Créer le fournisseur de revendications SAML Salesforce dans votre stratégie de base</span><span class="sxs-lookup"><span data-stu-id="e34c4-166">Create the Salesforce SAML claims provider in your base policy</span></span>

<span data-ttu-id="e34c4-167">Vous devez définir Salesforce comme fournisseur de revendications pour que les utilisateurs puissent se connecter à l’aide de Salesforce.</span><span class="sxs-lookup"><span data-stu-id="e34c4-167">You need to define Salesforce as a claims provider so users can sign in by using Salesforce.</span></span> <span data-ttu-id="e34c4-168">En d’autres termes, vous devez spécifier le point de terminaison avec lequel Azure AD B2C communiquera.</span><span class="sxs-lookup"><span data-stu-id="e34c4-168">In other words, you need to specify the endpoint that Azure AD B2C will communicate with.</span></span> <span data-ttu-id="e34c4-169">Le point de terminaison *fournira* un ensemble de *revendications* utilisées par Azure AD B2C pour vérifier qu’un utilisateur spécifique a été authentifié.</span><span class="sxs-lookup"><span data-stu-id="e34c4-169">The endpoint will *provide* a set of *claims* that Azure AD B2C uses to verify that a specific user has authenticated.</span></span> <span data-ttu-id="e34c4-170">Pour faire cela, ajoutez `<ClaimsProvider>` pour Salesforce dans le fichier d’extension de votre stratégie :</span><span class="sxs-lookup"><span data-stu-id="e34c4-170">To do this, add a `<ClaimsProvider>` for Salesforce in the extension file of your policy:</span></span>

1. <span data-ttu-id="e34c4-171">Dans votre répertoire de travail, ouvrez le fichier d’extension (TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="e34c4-171">In your working directory, open the extension file (TrustFrameworkExtensions.xml).</span></span>
2. <span data-ttu-id="e34c4-172">Recherchez la section `<ClaimsProviders>`.</span><span class="sxs-lookup"><span data-stu-id="e34c4-172">Find the `<ClaimsProviders>` section.</span></span> <span data-ttu-id="e34c4-173">Si elle n’existe pas, créez-la sous le nœud racine.</span><span class="sxs-lookup"><span data-stu-id="e34c4-173">If it does not exist, create it under the root node.</span></span>
3. <span data-ttu-id="e34c4-174">Ajoutez un `<ClaimsProvider>` :</span><span class="sxs-lookup"><span data-stu-id="e34c4-174">Add a new `<ClaimsProvider>`:</span></span>

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

<span data-ttu-id="e34c4-175">Sous le nœud `<ClaimsProvider>` :</span><span class="sxs-lookup"><span data-stu-id="e34c4-175">Under the `<ClaimsProvider>` node:</span></span>

1. <span data-ttu-id="e34c4-176">Modifiez la valeur de `<Domain>` en la définissant sur une valeur unique qui distingue `<ClaimsProvider>` d’autres fournisseurs d’identité.</span><span class="sxs-lookup"><span data-stu-id="e34c4-176">Change the value for `<Domain>` to a unique value that distinguishes `<ClaimsProvider>` from other identity providers.</span></span>
2. <span data-ttu-id="e34c4-177">Mettez à jour la valeur de `<DisplayName>` en la définissant sur un nom d’affichage pour le fournisseur de revendications.</span><span class="sxs-lookup"><span data-stu-id="e34c4-177">Update the value for `<DisplayName>` to a display name for the claims provider.</span></span> <span data-ttu-id="e34c4-178">Cette valeur n’est pas utilisée actuellement.</span><span class="sxs-lookup"><span data-stu-id="e34c4-178">Currently, this value is not used.</span></span>

### <a name="update-the-technical-profile"></a><span data-ttu-id="e34c4-179">Mise à jour du profil technique</span><span class="sxs-lookup"><span data-stu-id="e34c4-179">Update the technical profile</span></span>

<span data-ttu-id="e34c4-180">Pour obtenir un jeton SAML à partir de Salesforce, définissez les protocoles qu’Azure AD B2C doit utiliser pour communiquer avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e34c4-180">To get a SAML token from Salesforce, define the protocols that Azure AD B2C will use to communicate with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="e34c4-181">Faites cela dans l’élément `<TechnicalProfile>` de `<ClaimsProvider>` :</span><span class="sxs-lookup"><span data-stu-id="e34c4-181">Do this in the `<TechnicalProfile>` element of `<ClaimsProvider>`:</span></span>

1. <span data-ttu-id="e34c4-182">Mettez à jour l’ID du nœud `<TechnicalProfile>`.</span><span class="sxs-lookup"><span data-stu-id="e34c4-182">Update the ID of the `<TechnicalProfile>` node.</span></span> <span data-ttu-id="e34c4-183">Cet ID est utilisé pour faire référence à ce profil technique à partir d’autres parties de la stratégie.</span><span class="sxs-lookup"><span data-stu-id="e34c4-183">This ID is used to refer to this technical profile from other parts of the policy.</span></span>
2. <span data-ttu-id="e34c4-184">Mettez à jour la valeur pour `<DisplayName>`.</span><span class="sxs-lookup"><span data-stu-id="e34c4-184">Update the value for `<DisplayName>`.</span></span> <span data-ttu-id="e34c4-185">Cette valeur apparaît sur le bouton de connexion dans votre page de connexion.</span><span class="sxs-lookup"><span data-stu-id="e34c4-185">This value is displayed on the sign-in button on your sign-in page.</span></span>
3. <span data-ttu-id="e34c4-186">Mettez à jour la valeur pour `<Description>`.</span><span class="sxs-lookup"><span data-stu-id="e34c4-186">Update the value for `<Description>`.</span></span>
4. <span data-ttu-id="e34c4-187">Salesforce utilise le protocole SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="e34c4-187">Salesforce uses the SAML 2.0 protocol.</span></span> <span data-ttu-id="e34c4-188">Vérifiez que la valeur de `<Protocol>` est **SAML2**.</span><span class="sxs-lookup"><span data-stu-id="e34c4-188">Ensure that the value for `<Protocol>` is **SAML2**.</span></span>

<span data-ttu-id="e34c4-189">Mettez à jour la section `<Metadata>` dans le code XML précédent afin de refléter les paramètres de votre compte Salesforce.</span><span class="sxs-lookup"><span data-stu-id="e34c4-189">Update the `<Metadata>` section in the preceding XML to reflect the settings for your specific Salesforce account.</span></span> <span data-ttu-id="e34c4-190">Dans le code XML, mettez à jour les valeurs de métadonnées :</span><span class="sxs-lookup"><span data-stu-id="e34c4-190">In the XML, update the metadata values:</span></span>

1. <span data-ttu-id="e34c4-191">Mettez à jour la valeur de `<Item Key="PartnerEntity">` avec l’URL des métadonnées de Salesforce que vous avez copiée précédemment.</span><span class="sxs-lookup"><span data-stu-id="e34c4-191">Update the value of `<Item Key="PartnerEntity">` with the Salesforce metadata URL you copied earlier.</span></span> <span data-ttu-id="e34c4-192">Son format est le suivant:</span><span class="sxs-lookup"><span data-stu-id="e34c4-192">It has the following format:</span></span> 

    `https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp/connectedapp.xml`

2. <span data-ttu-id="e34c4-193">Dans la section `<CryptographicKeys>`, mettez à jour la valeur des deux instances de `StorageReferenceId` sur le nom de la clé de votre certificat de signature (par exemple, B2C_1A_SAMLSigningCert).</span><span class="sxs-lookup"><span data-stu-id="e34c4-193">In the `<CryptographicKeys>` section, update the value for both instances of `StorageReferenceId` to the name of the key of your signing certificate (for example, B2C_1A_SAMLSigningCert).</span></span>

### <a name="upload-the-extension-file-for-verification"></a><span data-ttu-id="e34c4-194">Télécharger le fichier d’extension pour la vérification</span><span class="sxs-lookup"><span data-stu-id="e34c4-194">Upload the extension file for verification</span></span>

<span data-ttu-id="e34c4-195">Votre stratégie est à présent configurée pour qu’Azure AD B2C sache comment communiquer avec Salesforce.</span><span class="sxs-lookup"><span data-stu-id="e34c4-195">Your policy is now configured so that Azure AD B2C knows how to communicate with Salesforce.</span></span> <span data-ttu-id="e34c4-196">Essayez de charger le fichier d’extension de votre stratégie pour vérifier qu’il n’y a pas de problème.</span><span class="sxs-lookup"><span data-stu-id="e34c4-196">Try uploading the extension file of your policy, to verify that there aren't any issues so far.</span></span> <span data-ttu-id="e34c4-197">Pour charger le fichier d’extension de votre stratégie :</span><span class="sxs-lookup"><span data-stu-id="e34c4-197">To upload the extension file of your policy:</span></span>

1. <span data-ttu-id="e34c4-198">Dans votre locataire Azure AD B2C, accédez au tableau **Toutes les stratégies**.</span><span class="sxs-lookup"><span data-stu-id="e34c4-198">In your Azure AD B2C tenant, go to the **All Policies** blade.</span></span>
2. <span data-ttu-id="e34c4-199">Activez la case à cocher **Remplacer la stratégie si elle existe**.</span><span class="sxs-lookup"><span data-stu-id="e34c4-199">Select the **Overwrite the policy if it exists** check box.</span></span>
3. <span data-ttu-id="e34c4-200">Chargez le fichier d’extension (TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="e34c4-200">Upload the extension file (TrustFrameworkExtensions.xml).</span></span> <span data-ttu-id="e34c4-201">Vérifiez que sa validation n’échoue pas.</span><span class="sxs-lookup"><span data-stu-id="e34c4-201">Ensure that it doesn't fail validation.</span></span>

## <a name="register-the-salesforce-saml-claims-provider-to-a-user-journey"></a><span data-ttu-id="e34c4-202">Enregistrer le fournisseur de revendications SAML Salesforce dans un parcours utilisateur</span><span class="sxs-lookup"><span data-stu-id="e34c4-202">Register the Salesforce SAML claims provider to a user journey</span></span>

<span data-ttu-id="e34c4-203">Ajoutez ensuite le fournisseur d’identité SAML Salesforce à l’un de vos parcours utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e34c4-203">Next, add the Salesforce SAML identity provider to one of your user journeys.</span></span> <span data-ttu-id="e34c4-204">À ce stade, le fournisseur d’identité a été configuré, mais il n’est disponible dans aucune page d’inscription ou de connexion.</span><span class="sxs-lookup"><span data-stu-id="e34c4-204">At this point, the identity provider has been set up, but it’s not available on any of the user sign-up or sign-in pages.</span></span> <span data-ttu-id="e34c4-205">Pour ajouter le fournisseur d’identité à une page de connexion, commencez par créer un doublon d’un modèle de parcours utilisateur actuel.</span><span class="sxs-lookup"><span data-stu-id="e34c4-205">To add the identity provider to a sign-in page, first, create a duplicate of an existing template user journey.</span></span> <span data-ttu-id="e34c4-206">Ensuite, modifiez le modèle afin qu’il ait également le fournisseur d’identité Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e34c4-206">Then, modify the template so that it also has the Azure AD identity provider.</span></span>

1. <span data-ttu-id="e34c4-207">Ouvrez le fichier de base de votre stratégie (par exemple, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="e34c4-207">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2. <span data-ttu-id="e34c4-208">Recherchez l’élément `<UserJourneys>`, puis copiez l’intégralité de la valeur `<UserJourney>`, en incluant Id=”SignUpOrSignIn”.</span><span class="sxs-lookup"><span data-stu-id="e34c4-208">Find the `<UserJourneys>` element, and then copy the entire `<UserJourney>` value, including Id=”SignUpOrSignIn”.</span></span>
3. <span data-ttu-id="e34c4-209">Ouvrez le fichier d’extension (par exemple, TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="e34c4-209">Open the extension file (for example, TrustFrameworkExtensions.xml).</span></span> <span data-ttu-id="e34c4-210">Recherchez l’élément `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="e34c4-210">Find the `<UserJourneys>` element.</span></span> <span data-ttu-id="e34c4-211">Si l’élément n’existe pas, créez-en un.</span><span class="sxs-lookup"><span data-stu-id="e34c4-211">If the element doesn't exist, create one.</span></span>
4. <span data-ttu-id="e34c4-212">Collez l’intégralité de l’élément `<UserJourney>` copié en tant qu’enfant de l’élément `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="e34c4-212">Paste the entire copied `<UserJourney>` as a child of the `<UserJourneys>` element.</span></span>
5. <span data-ttu-id="e34c4-213">Renommez l’ID du nouvel élément `<UserJourney>` (par exemple, SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="e34c4-213">Rename the ID of the new `<UserJourney>` (for example, SignUpOrSignUsingContoso).</span></span>

### <a name="display-the-identity-provider-button"></a><span data-ttu-id="e34c4-214">Afficher le bouton du fournisseur d’identité</span><span class="sxs-lookup"><span data-stu-id="e34c4-214">Display the identity provider button</span></span>

<span data-ttu-id="e34c4-215">L’élément `<ClaimsProviderSelection>` est analogue à un bouton de fournisseur d’identité sur une page d’inscription ou de connexion.</span><span class="sxs-lookup"><span data-stu-id="e34c4-215">The `<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up or sign-in page.</span></span> <span data-ttu-id="e34c4-216">L’ajout d’un élément `<ClaimsProviderSelection>` pour Salesforce a pour effet qu’un nouveau bouton s’affiche quand un utilisateur accède à cette page.</span><span class="sxs-lookup"><span data-stu-id="e34c4-216">By adding an `<ClaimsProviderSelection>` element for Salesforce, a new button appears when a user goes to this page.</span></span> <span data-ttu-id="e34c4-217">Pour afficher le bouton de fournisseur d’identité :</span><span class="sxs-lookup"><span data-stu-id="e34c4-217">To display the identity provider button:</span></span>

1. <span data-ttu-id="e34c4-218">Dans l’élément `<UserJourney>` que vous avez créé, recherchez l’élément `<OrchestrationStep>` avec `Order="1"`.</span><span class="sxs-lookup"><span data-stu-id="e34c4-218">In the `<UserJourney>` that you created, find the `<OrchestrationStep>` with `Order="1"`.</span></span>
2. <span data-ttu-id="e34c4-219">Ajoutez le code XML suivant :</span><span class="sxs-lookup"><span data-stu-id="e34c4-219">Add the following XML:</span></span>

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

3. <span data-ttu-id="e34c4-220">Définissez `TargetClaimsExchangeId` sur une valeur logique.</span><span class="sxs-lookup"><span data-stu-id="e34c4-220">Set `TargetClaimsExchangeId` to a logical value.</span></span> <span data-ttu-id="e34c4-221">Nous vous recommandons de suivre la même convention de dénomination que pour les autres éléments (par exemple, *\[ClaimProviderName\]Exchange*).</span><span class="sxs-lookup"><span data-stu-id="e34c4-221">We recommend following the same convention as others (for example, *\[ClaimProviderName\]Exchange*).</span></span>

### <a name="link-the-identity-provider-button-to-an-action"></a><span data-ttu-id="e34c4-222">Lier le bouton de fournisseur d’identité à une action</span><span class="sxs-lookup"><span data-stu-id="e34c4-222">Link the identity provider button to an action</span></span>

<span data-ttu-id="e34c4-223">À présent que vous avez un bouton de fournisseur d’identité en place, liez-le à une action.</span><span class="sxs-lookup"><span data-stu-id="e34c4-223">Now that you have an identity provider button in place, link it to an action.</span></span> <span data-ttu-id="e34c4-224">En l’occurrence, l’action pour Azure AD B2C est de communiquer avec Salesforce pour recevoir un jeton SAML.</span><span class="sxs-lookup"><span data-stu-id="e34c4-224">In this case, the action is for Azure AD B2C to communicate with Salesforce to receive a SAML token.</span></span> <span data-ttu-id="e34c4-225">Vous pouvez faire cela en liant le profil technique de votre fournisseur de revendications SAML Salesforce :</span><span class="sxs-lookup"><span data-stu-id="e34c4-225">You can do this by linking the technical profile for your Salesforce SAML claims provider:</span></span>

1. <span data-ttu-id="e34c4-226">Dans le nœud `<UserJourney>`, recherchez l’élément `<OrchestrationStep>` avec `Order="2"`.</span><span class="sxs-lookup"><span data-stu-id="e34c4-226">In the `<UserJourney>` node, find the `<OrchestrationStep>` with `Order="2"`.</span></span>
2. <span data-ttu-id="e34c4-227">Ajoutez le code XML suivant :</span><span class="sxs-lookup"><span data-stu-id="e34c4-227">Add the following XML:</span></span>

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

3. <span data-ttu-id="e34c4-228">Mettez à jour `Id` sur la même valeur que celle utilisée précédemment pour `TargetClaimsExchangeId`.</span><span class="sxs-lookup"><span data-stu-id="e34c4-228">Update `Id` to the same value that you used earlier for `TargetClaimsExchangeId`.</span></span>
4. <span data-ttu-id="e34c4-229">Mettez à jour `TechnicalProfileReferenceId` sur l’`Id` du profil technique que vous avez créé précédemment (par exemple, ContosoProfile).</span><span class="sxs-lookup"><span data-stu-id="e34c4-229">Update `TechnicalProfileReferenceId` to the `Id` of the technical profile you created earlier (for example, ContosoProfile).</span></span>

### <a name="upload-the-updated-extension-file"></a><span data-ttu-id="e34c4-230">Téléchargez le fichier d’extension mis à jour</span><span class="sxs-lookup"><span data-stu-id="e34c4-230">Upload the updated extension file</span></span>

<span data-ttu-id="e34c4-231">Vous avez terminé la modification du fichier d’extension.</span><span class="sxs-lookup"><span data-stu-id="e34c4-231">You are done modifying the extension file.</span></span> <span data-ttu-id="e34c4-232">Enregistrez et chargez ce fichier.</span><span class="sxs-lookup"><span data-stu-id="e34c4-232">Save and upload this file.</span></span> <span data-ttu-id="e34c4-233">Faites en sorte que toutes les validations réussissent.</span><span class="sxs-lookup"><span data-stu-id="e34c4-233">Ensure that all validations succeed.</span></span>

### <a name="update-the-relying-party-file"></a><span data-ttu-id="e34c4-234">Mettre à jour le fichier de partie de confiance</span><span class="sxs-lookup"><span data-stu-id="e34c4-234">Update the relying party file</span></span>

<span data-ttu-id="e34c4-235">Ensuite, mettez à jour le fichier de partie de confiance qui lance le parcours utilisateur que vous avez créé :</span><span class="sxs-lookup"><span data-stu-id="e34c4-235">Next, update the relying party (RP) file that initiates the user journey that you created:</span></span>

1. <span data-ttu-id="e34c4-236">Faites une copie de SignUpOrSignIn.xml dans votre répertoire de travail.</span><span class="sxs-lookup"><span data-stu-id="e34c4-236">Make a copy of SignUpOrSignIn.xml in your working directory.</span></span> <span data-ttu-id="e34c4-237">Ensuite, renommez-le (par exemple, SignUpOrSignInWithAAD.xml).</span><span class="sxs-lookup"><span data-stu-id="e34c4-237">Then, rename it (for example, SignUpOrSignInWithAAD.xml).</span></span>
2. <span data-ttu-id="e34c4-238">Ouvrez le nouveau fichier, puis mettez à jour l’attribut `PolicyId` pour `<TrustFrameworkPolicy>` avec une valeur unique.</span><span class="sxs-lookup"><span data-stu-id="e34c4-238">Open the new file and update the `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value.</span></span> <span data-ttu-id="e34c4-239">Il s’agit du nom de votre stratégie (par exemple, SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="e34c4-239">This is the name of your policy (for example, SignUpOrSignInWithAAD).</span></span>
3. <span data-ttu-id="e34c4-240">Modifiez l’attribut `ReferenceId` dans `<DefaultUserJourney>` pour qu’il corresponde à l’`Id` du nouveau parcours utilisateur que vous avez créé (par exemple, SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="e34c4-240">Modify the `ReferenceId` attribute in `<DefaultUserJourney>` to match the `Id` of the new user journey that you created (for example, SignUpOrSignUsingContoso).</span></span>
4. <span data-ttu-id="e34c4-241">Enregistrez vos modifications, puis chargez le fichier.</span><span class="sxs-lookup"><span data-stu-id="e34c4-241">Save your changes, and then upload the file.</span></span>

## <a name="test-and-troubleshoot"></a><span data-ttu-id="e34c4-242">Tester et résoudre les problèmes</span><span class="sxs-lookup"><span data-stu-id="e34c4-242">Test and troubleshoot</span></span>

<span data-ttu-id="e34c4-243">Pour tester la stratégie personnalisée que vous venez de charger, dans le portail Azure, accédez au panneau Stratégie, puis cliquez sur **Exécuter maintenant**.</span><span class="sxs-lookup"><span data-stu-id="e34c4-243">To test the custom policy that you just uploaded, in the Azure portal, go to the policy blade, and then click **Run now**.</span></span> <span data-ttu-id="e34c4-244">En cas d’échec, consultez [Résoudre les problèmes des stratégies personnalisées](active-directory-b2c-troubleshoot-custom.md).</span><span class="sxs-lookup"><span data-stu-id="e34c4-244">If it fails, see [Troubleshoot custom policies](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e34c4-245">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e34c4-245">Next steps</span></span>

<span data-ttu-id="e34c4-246">Envoyez vos commentaires à l’adresse [AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="e34c4-246">Provide feedback to [AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span></span>
