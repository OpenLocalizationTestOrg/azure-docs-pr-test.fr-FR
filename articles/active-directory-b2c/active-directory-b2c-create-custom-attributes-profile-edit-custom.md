---
title: "Azure B2C Active Directory : Ajouter vos propres stratégies de toocustom d’attributs et utiliser dans le profil modifier | Documents Microsoft"
description: "Une procédure pas à pas sur l’utilisation des propriétés d’extension, les attributs personnalisés et de les inclure dans l’interface utilisateur hello"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: joroja
ms.openlocfilehash: 8cc9c6a38d7652797ba54a3e02078ac2bf4a693b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-creating-and-using-custom-attributes-in-a-custom-profile-edit-policy"></a><span data-ttu-id="a9345-103">Azure Active Directory B2C : création et utilisation d’attributs personnalisés dans une stratégie personnalisée de modification de profil</span><span class="sxs-lookup"><span data-stu-id="a9345-103">Azure Active Directory B2C: Creating and using custom attributes in a custom profile edit policy</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="a9345-104">Dans cet article, vous créez un attribut personnalisé dans votre annuaire Azure AD B2C et utilisez ce nouvel attribut comme une revendication personnalisée dans un parcours de hello profil Modifier utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a9345-104">In this article, you create a custom attribute in your Azure AD B2C directory and use this new attribute as a custom claim in hello profile edit user journey.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a9345-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a9345-105">Prerequisites</span></span>

<span data-ttu-id="a9345-106">Hello terminé les étapes dans l’article de hello [prise en main des stratégies personnalisées](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="a9345-106">Complete hello steps in hello article [Getting Started with Custom Policies](active-directory-b2c-get-started-custom.md).</span></span>

## <a name="use-custom-attributes-toocollect-information-about-your-customers-in-azure-active-directory-b2c-using-custom-policies"></a><span data-ttu-id="a9345-107">Utiliser les informations de toocollect d’attributs personnalisés sur vos clients dans Azure Active Directory B2C, à l’aide de stratégies personnalisées</span><span class="sxs-lookup"><span data-stu-id="a9345-107">Use custom attributes toocollect information about your customers in Azure Active Directory B2C using custom policies</span></span>
<span data-ttu-id="a9345-108">Votre répertoire Azure Active Directory (Azure AD) B2C est fourni avec un ensemble intégré d’attributs : prénom, nom, ville, code postal, userPrincipalName, etc.  Vous devez souvent toocreate vos propres attributs.</span><span class="sxs-lookup"><span data-stu-id="a9345-108">Your Azure Active Directory (Azure AD) B2C directory comes with a built-in set of attributes: Given Name, Surname, City, Postal Code, userPrincipalName, etc.  You often need toocreate your own attributes.</span></span>  <span data-ttu-id="a9345-109">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="a9345-109">For example:</span></span>
* <span data-ttu-id="a9345-110">Une application côté client doit toopersist un attribut tel que « LoyaltyNumber ».</span><span class="sxs-lookup"><span data-stu-id="a9345-110">A customer-facing application needs toopersist an attribute such as "LoyaltyNumber."</span></span>
* <span data-ttu-id="a9345-111">Un fournisseur d’identité a un identificateur d’utilisateur unique qui doit être enregistré, par exemple « uniqueUserGUID ».</span><span class="sxs-lookup"><span data-stu-id="a9345-111">An identity provider has a unique user identifier that must be saved such as "uniqueUserGUID.""</span></span>
* <span data-ttu-id="a9345-112">Un parcours de l’utilisateur personnalisée a besoin d’état de hello toopersist d’utilisateur, tels que « migrationStatus ».</span><span class="sxs-lookup"><span data-stu-id="a9345-112">A custom user journey needs toopersist hello state of user such as "migrationStatus."</span></span>

<span data-ttu-id="a9345-113">Avec Azure AD B2C, vous pouvez étendre le jeu hello d’attributs stockés sur chaque compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a9345-113">With Azure AD B2C, you can extend hello set of attributes stored on each user account.</span></span> <span data-ttu-id="a9345-114">Vous pouvez également lire et écrire ces attributs à l’aide de hello [API Azure AD Graph](active-directory-b2c-devquickstarts-graph-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="a9345-114">You can also read and write these attributes by using hello [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span></span>

<span data-ttu-id="a9345-115">Propriétés d’extension étendent le schéma hello des objets utilisateur de hello dans le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="a9345-115">Extension properties extend hello schema of hello user objects in hello directory.</span></span>  <span data-ttu-id="a9345-116">propriété d’extension Hello termes du contrat, les attributs personnalisés et les revendication personnalisée, consultez toohello même chose dans le contexte de hello de ce nom d’article et hello varie selon le contexte hello (application, objet, de stratégie).</span><span class="sxs-lookup"><span data-stu-id="a9345-116">hello terms extension property, custom attribute and custom claim refer toohello same thing in hello context of this article and hello name varies depending on hello context (application, object, policy).</span></span>

<span data-ttu-id="a9345-117">Les propriétés d’extension ne peuvent être inscrites que sur un objet application, même si elles peuvent contenir des données pour un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a9345-117">Extension properties can only be registered on an Application object even though they may contain data for a User.</span></span> <span data-ttu-id="a9345-118">propriété de Hello est attaché toohello application.</span><span class="sxs-lookup"><span data-stu-id="a9345-118">hello property is attached toohello application.</span></span> <span data-ttu-id="a9345-119">objet de l’Application Hello doit être accordé un accès en écriture tooregister une propriété d’extension.</span><span class="sxs-lookup"><span data-stu-id="a9345-119">hello Application object must be granted write access tooregister an extension property.</span></span> <span data-ttu-id="a9345-120">Propriétés d’extension 100 (pour tous les types et toutes les applications) peuvent être écrits tooany un seul objet.</span><span class="sxs-lookup"><span data-stu-id="a9345-120">100 Extension properties (across ALL types and ALL applications) can be written tooany single object.</span></span> <span data-ttu-id="a9345-121">Propriétés d’extension sont ajoutés toohello type d’annuaire cible et devient immédiatement accessibles dans le locataire d’annuaire hello Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="a9345-121">Extension properties are added toohello target directory type and becomes immediately accessible in hello Azure AD B2C directory tenant.</span></span>
<span data-ttu-id="a9345-122">Si l’application hello est supprimée, les propriétés d’Extension, ainsi que les données contenues dans les pour tous les utilisateurs sont également supprimées.</span><span class="sxs-lookup"><span data-stu-id="a9345-122">If hello application is deleted, those Extension properties along with any data contained in them for all users are also removed.</span></span> <span data-ttu-id="a9345-123">Si une propriété d’extension est supprimée par hello Application, elle est supprimée de hello cibler des objets d’annuaire et hello valeurs supprimés.</span><span class="sxs-lookup"><span data-stu-id="a9345-123">If an extension property is deleted by hello Application, it is removed on hello target directory objects, and hello values deleted.</span></span>

<span data-ttu-id="a9345-124">Propriétés d’extension existent uniquement dans un contexte d’une Application inscrite dans le locataire de hello hello.</span><span class="sxs-lookup"><span data-stu-id="a9345-124">Extension properties exist only in hello context of a registered  Application in hello tenant.</span></span> <span data-ttu-id="a9345-125">id d’objet Hello de l’Application doit être inclus dans hello TechnicalProfile qui l’utilisent.</span><span class="sxs-lookup"><span data-stu-id="a9345-125">hello object id of that Application must be included in hello TechnicalProfile that use it.</span></span>

>[!NOTE]
><span data-ttu-id="a9345-126">répertoire de Hello Azure AD B2C inclut généralement une application Web nommée `b2c-extensions-app`.</span><span class="sxs-lookup"><span data-stu-id="a9345-126">hello Azure AD B2C directory typically includes a Web App named `b2c-extensions-app`.</span></span>  <span data-ttu-id="a9345-127">Cette application est principalement utilisée par les stratégies intégrées hello b2c pour les revendications personnalisées hello créées via hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a9345-127">This application is primarily used by hello b2c built-in  policies for hello custom claims created via hello Azure portal.</span></span>  <span data-ttu-id="a9345-128">L’utilisation de ce tooregister des extensions d’application pour les stratégies personnalisées b2c est recommandée uniquement pour les utilisateurs expérimentés.</span><span class="sxs-lookup"><span data-stu-id="a9345-128">Using this application tooregister extensions for b2c custom policies is recommended only for advanced users.</span></span>  <span data-ttu-id="a9345-129">Instructions correspondantes sont inclus dans hello section étapes suivantes dans cet article.</span><span class="sxs-lookup"><span data-stu-id="a9345-129">Instructions for this are included in hello Next Steps section in this article.</span></span>


## <a name="creating-a-new-application-toostore-hello-extension-properties"></a><span data-ttu-id="a9345-130">Création d’un nouveau toostore d’application les propriétés d’extension hello</span><span class="sxs-lookup"><span data-stu-id="a9345-130">Creating a new application toostore hello extension properties</span></span>

1. <span data-ttu-id="a9345-131">Ouvrez une session de navigation et naviguez toohello [le portail Azure](https://portal.azure.com) et connectez-vous avec les informations d’identification administratives de hello annuaire B2C tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="a9345-131">Open a browsing session and navigate toohello [Azure porta](https://portal.azure.com) and sign in with administrative credentials of hello B2C Directory you wish tooconfigure.</span></span>
1. <span data-ttu-id="a9345-132">Cliquez sur **Azure Active Directory** sur le menu de navigation gauche hello.</span><span class="sxs-lookup"><span data-stu-id="a9345-132">Click **Azure Active Directory** on hello left navigation menu.</span></span> <span data-ttu-id="a9345-133">Vous devrez peut-être toofind en sélectionnant plus de services >.</span><span class="sxs-lookup"><span data-stu-id="a9345-133">You may need toofind it by selecting More services>.</span></span>
1. <span data-ttu-id="a9345-134">Sélectionnez **Inscriptions des applications**, puis cliquez sur **Nouvelle inscription d’application**.</span><span class="sxs-lookup"><span data-stu-id="a9345-134">Select **App registrations** and click **New application registration**</span></span>
1. <span data-ttu-id="a9345-135">Fournir suivant de hello recommandé entrées :</span><span class="sxs-lookup"><span data-stu-id="a9345-135">Provide hello following recommended entries:</span></span>
  * <span data-ttu-id="a9345-136">Spécifiez un nom pour l’application web de hello : **WebApp-GraphAPI-DirectoryExtensions**</span><span class="sxs-lookup"><span data-stu-id="a9345-136">Specify a name for hello web application: **WebApp-GraphAPI-DirectoryExtensions**</span></span>
  * <span data-ttu-id="a9345-137">Type d’application : application web/API</span><span class="sxs-lookup"><span data-stu-id="a9345-137">Application type: Web app/API</span></span>
  * <span data-ttu-id="a9345-138">URL d’ouverture de session : https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions</span><span class="sxs-lookup"><span data-stu-id="a9345-138">Sign-on URL:https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions</span></span>
1. <span data-ttu-id="a9345-139">Sélectionnez **Créer.</span><span class="sxs-lookup"><span data-stu-id="a9345-139">Select **Create.</span></span> <span data-ttu-id="a9345-140">Réussite s’affiche dans hello **des notifications**</span><span class="sxs-lookup"><span data-stu-id="a9345-140">Successful completion appears in hello **notifications**</span></span>
1. <span data-ttu-id="a9345-141">Sélectionnez application web de hello nouvellement créé : **WebApp-GraphAPI-DirectoryExtensions**</span><span class="sxs-lookup"><span data-stu-id="a9345-141">Select hello newly created web application: **WebApp-GraphAPI-DirectoryExtensions**</span></span>
1. <span data-ttu-id="a9345-142">Dans Paramètres, sélectionnez **Autorisations requises**.</span><span class="sxs-lookup"><span data-stu-id="a9345-142">Select Settings: **Required permissions**</span></span>
1. <span data-ttu-id="a9345-143">Dans API, sélectionnez **Windows Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a9345-143">Select API **Windows Active Directory**</span></span>
1. <span data-ttu-id="a9345-144">Dans Autorisations d’application, cochez l’option **Lire et écrire les données de l’annuaire**, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="a9345-144">Place a checkmark in Application Permissions: **Read and write directory data**, and **Save**</span></span>
1. <span data-ttu-id="a9345-145">Sélectionnez **Accorder des autorisations**, puis confirmez en cliquant sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="a9345-145">Choose **Grant permissions** and confirm **Yes**.</span></span>
1. <span data-ttu-id="a9345-146">Copiez tooyour Presse-papiers et enregistrer hello suivant des identificateurs de WebApp-GraphAPI-DirectoryExtensions > Paramètres > Propriétés ></span><span class="sxs-lookup"><span data-stu-id="a9345-146">Copy tooyour clipboard and save hello following identifiers from WebApp-GraphAPI-DirectoryExtensions>Settings>Properties></span></span>
*  <span data-ttu-id="a9345-147">**ID de l’application**.</span><span class="sxs-lookup"><span data-stu-id="a9345-147">**Application ID** .</span></span> <span data-ttu-id="a9345-148">Exemple : `103ee0e6-f92d-4183-b576-8c3739027780`</span><span class="sxs-lookup"><span data-stu-id="a9345-148">Example: `103ee0e6-f92d-4183-b576-8c3739027780`</span></span>
* <span data-ttu-id="a9345-149">**ID objet**.</span><span class="sxs-lookup"><span data-stu-id="a9345-149">**Object ID**.</span></span> <span data-ttu-id="a9345-150">Exemple : `80d8296a-da0a-49ee-b6ab-fd232aa45201`</span><span class="sxs-lookup"><span data-stu-id="a9345-150">Example: `80d8296a-da0a-49ee-b6ab-fd232aa45201`</span></span>



## <a name="modifying-your-custom-policy-tooadd-hello-applicationobjectid"></a><span data-ttu-id="a9345-151">Modification de votre hello tooadd de stratégie personnalisée ApplicationObjectId</span><span class="sxs-lookup"><span data-stu-id="a9345-151">Modifying your custom policy tooadd hello ApplicationObjectId</span></span>

```xml
    <ClaimsProviders>
        <ClaimsProvider>
              <DisplayName>Azure Active Directory</DisplayName>
            <TechnicalProfile Id="AAD-Common">
              <DisplayName>Azure Active Directory</DisplayName>
              <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.AzureActiveDirectoryProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
              <!-- Provide objectId and appId before using extension properties. -->
              <Metadata>
                <Item Key="ApplicationObjectId">insert objectId here</Item>
                <Item Key="ClientId">insert appId here</Item>
              </Metadata>
            <!-- End of changes -->
              <CryptographicKeys>
                <Key Id="issuer_secret" StorageReferenceId="TokenSigningKeyContainer" />
              </CryptographicKeys>
              <IncludeInSso>false</IncludeInSso>
              <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
            </TechnicalProfile>
        </ClaimsProvider>
    </ClaimsProviders>
```

>[!NOTE]
><span data-ttu-id="a9345-152">Hello <TechnicalProfile Id="AAD-Common"> est tooas référencé « commune », car ses éléments sont inclus dans et réutilisées dans tous les hello Azure Active Directory TechnicalProfiles à l’aide hello élément :`<IncludeTechnicalProfile ReferenceId="AAD-Common" />`</span><span class="sxs-lookup"><span data-stu-id="a9345-152">hello <TechnicalProfile Id="AAD-Common"> is referred tooas "common" because its elements are included in and reused in all hello Azure Active Directory TechnicalProfiles by using hello element: `<IncludeTechnicalProfile ReferenceId="AAD-Common" />`</span></span>

>[!NOTE]
><span data-ttu-id="a9345-153">Lorsque hello TechnicalProfile écrit pour la propriété d’extension hello première heure toohello nouvellement créé, vous pouvez rencontrer une erreur à usage unique.</span><span class="sxs-lookup"><span data-stu-id="a9345-153">When hello TechnicalProfile writes for hello first time toohello newly created extension property, you may experience a one-time error.</span></span>  <span data-ttu-id="a9345-154">propriété d’extension Hello est créée hello première fois, qu'il est utilisé.</span><span class="sxs-lookup"><span data-stu-id="a9345-154">hello extension property is created hello first time it is used.</span></span>  

## <a name="using-hello-new-extension-property--custom-attribute-in-a-user-journey"></a><span data-ttu-id="a9345-155">À l’aide de la nouvelle propriété d’extension hello / d’attribut personnalisé dans un parcours de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="a9345-155">Using hello new extension property / custom attribute in a user journey</span></span>


1. <span data-ttu-id="a9345-156">Hello Ouvrir fichier Party(RP) de partie de confiance qui décrit votre stratégie de modifier le parcours de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a9345-156">Open hello Relying Party(RP) file that describes your policy edit user journey.</span></span>  <span data-ttu-id="a9345-157">Si vous démarrez, il peut être conseillée toodownload votre version déjà configurée de hello RP-PolicyEdit fichier directement à partir de hello section de stratégie personnalisée de B2C Azure Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a9345-157">If you are starting out, it may be advisable toodownload your already configured version of hello RP-PolicyEdit file directly from hello Azure B2C Custom Policy section in hello Azure portal.</span></span>  <span data-ttu-id="a9345-158">Vous pouvez également ouvrir votre fichier XML à partir de votre dossier de stockage.</span><span class="sxs-lookup"><span data-stu-id="a9345-158">Alternatively, open your XML file from your storage folder.</span></span>
2. <span data-ttu-id="a9345-159">Ajoutez une revendication personnalisée `loyaltyId`.</span><span class="sxs-lookup"><span data-stu-id="a9345-159">Add a custom claim `loyaltyId`.</span></span>  <span data-ttu-id="a9345-160">En incluant hello personnalisé de revendication Bonjour `<RelyingParty>` élément, elle est passée comme un paramètre de toohello UserJourney TechnicalProfiles et inclus dans le jeton hello pour une application hello.</span><span class="sxs-lookup"><span data-stu-id="a9345-160">By including hello custom claim in hello `<RelyingParty>` element, it is passed as a parameter toohello UserJourney TechnicalProfiles and included in hello token for hello application.</span></span>
```xml
<RelyingParty>
   <DefaultUserJourney ReferenceId="ProfileEdit" />
   <TechnicalProfile Id="PolicyProfile">
     <DisplayName>PolicyProfile</DisplayName>
     <Protocol Name="OpenIdConnect" />
     <OutputClaims>
       <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>
       <OutputClaim ClaimTypeReferenceId="city" />

       <OutputClaim ClaimTypeReferenceId="extension_loyaltyId" />

     </OutputClaims>
     <SubjectNamingInfo ClaimType="sub" />
   </TechnicalProfile>
 </RelyingParty>
 ```
3. <span data-ttu-id="a9345-161">Ajouter un fichier de stratégie de revendication définition toohello Extension `TrustFrameworkExtensions.xml` à l’intérieur de hello `<ClaimsSchema>` élément, comme indiqué.</span><span class="sxs-lookup"><span data-stu-id="a9345-161">Add a claim definition toohello Extension policy file  `TrustFrameworkExtensions.xml` inside hello `<ClaimsSchema>` element as shown.</span></span>
```xml
<ClaimsSchema>
        <ClaimType Id="extension_loyaltyId">
            <DisplayName>Loyalty Identification Tag</DisplayName>
            <DataType>string</DataType>
            <UserHelpText>Your loyalty number from your membership card</UserHelpText>
            <UserInputType>TextBox</UserInputType>
        </ClaimType>
</ClaimsSchema>
```
4. <span data-ttu-id="a9345-162">Ajouter hello même revendication le fichier de définition de stratégie de Base toohello `TrustFrameworkBase.xml`.</span><span class="sxs-lookup"><span data-stu-id="a9345-162">Add hello same claim definition toohello Base policy file `TrustFrameworkBase.xml`.</span></span>  
><span data-ttu-id="a9345-163">Ajout d’un `ClaimType` définition dans la base de hello et fichier des extensions hello n’est normalement pas nécessaire, toutefois, étant donné que les étapes suivantes hello ajoutera hello extension_loyaltyId tooTechnicalProfiles dans le fichier de Base hello, programme de validation de stratégie hello rejette téléchargement de hello hello fichier de base sans lui.</span><span class="sxs-lookup"><span data-stu-id="a9345-163">Adding a `ClaimType` definition in both hello base and hello extensions file is normally not necessary, however since hello next steps will add hello extension_loyaltyId tooTechnicalProfiles in hello Base file, hello policy validator will reject hello upload of hello base file without it.</span></span>
><span data-ttu-id="a9345-164">Il peut être utile tootrace l’exécution de hello hello utilisateur voyage est nommé « ProfileEdit » dans le fichier de TrustFrameworkBase.xml hello.</span><span class="sxs-lookup"><span data-stu-id="a9345-164">It may be useful tootrace hello execution of hello user journey named "ProfileEdit" in hello TrustFrameworkBase.xml file.</span></span>  <span data-ttu-id="a9345-165">Recherchez le voyage d’utilisateur hello Hello même nom dans votre éditeur et observez qu’Orchestration étape 5 appelle hello TechnicalProfileReferenceID = « SelfAsserted-ProfileUpdate ».</span><span class="sxs-lookup"><span data-stu-id="a9345-165">Search for hello user journey of hello same name in your editor and observe that Orchestration Step 5 invokes hello TechnicalProfileReferenceID="SelfAsserted-ProfileUpdate".</span></span>  <span data-ttu-id="a9345-166">Rechercher et examiner cette toofamiliarize TechnicalProfile avec les flux hello.</span><span class="sxs-lookup"><span data-stu-id="a9345-166">Search and inspect this TechnicalProfile toofamiliarize yourself with hello flow.</span></span>
5. <span data-ttu-id="a9345-167">Ajouter loyaltyId comme entrée et sortie de revendication Bonjour TechnicalProfile « SelfAsserted-ProfileUpdate »</span><span class="sxs-lookup"><span data-stu-id="a9345-167">Add loyaltyId as input and output claim in hello TechnicalProfile "SelfAsserted-ProfileUpdate"</span></span>
```xml
<TechnicalProfile Id="SelfAsserted-ProfileUpdate">
          <DisplayName>User ID signup</DisplayName>
          <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.SelfAssertedAttributeProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
          <Metadata>
            <Item Key="ContentDefinitionReferenceId">api.selfasserted.profileupdate</Item>
          </Metadata>
          <IncludeInSso>false</IncludeInSso>
          <InputClaims>

            <InputClaim ClaimTypeReferenceId="alternativeSecurityId" />
            <InputClaim ClaimTypeReferenceId="userPrincipalName" />

            <!-- Optional claims. These claims are collected from hello user and can be modified. Any claim added here should be updated in the
                 ValidationTechnicalProfile referenced below so it can be written toodirectory after being updateed by hello user, i.e. AAD-UserWriteProfileUsingObjectId. -->
            <InputClaim ClaimTypeReferenceId="givenName" />
            <InputClaim ClaimTypeReferenceId="surname" />
            <InputClaim ClaimTypeReferenceId="extension_loyaltyId"/>
          </InputClaims>
          <OutputClaims>
            <!-- Required claims -->
            <OutputClaim ClaimTypeReferenceId="executed-SelfAsserted-Input" DefaultValue="true" />

            <!-- Optional claims. These claims are collected from hello user and can be modified. Any claim added here should be updated in the
                 ValidationTechnicalProfile referenced below so it can be written toodirectory after being updateed by hello user, i.e. AAD-UserWriteProfileUsingObjectId. -->
            <OutputClaim ClaimTypeReferenceId="givenName" />
            <OutputClaim ClaimTypeReferenceId="surname" />
            <OutputClaim ClaimTypeReferenceId="extension_loyaltyId"/>
          </OutputClaims>
          <ValidationTechnicalProfiles>
            <ValidationTechnicalProfile ReferenceId="AAD-UserWriteProfileUsingObjectId" />
          </ValidationTechnicalProfiles>
        </TechnicalProfile>
```
6. <span data-ttu-id="a9345-168">Ajoute la revendication dans la valeur de hello toopersist TechnicalProfile « AAD-UserWriteProfileUsingObjectId » de revendication hello dans la propriété d’extension hello, pour l’utilisateur actuel de hello dans le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="a9345-168">Add claim in TechnicalProfile "AAD-UserWriteProfileUsingObjectId" toopersist hello value of hello claim in hello extension property, for hello current user in hello directory.</span></span>
```xml
<TechnicalProfile Id="AAD-UserWriteProfileUsingObjectId">
          <Metadata>
            <Item Key="Operation">Write</Item>
            <Item Key="RaiseErrorIfClaimsPrincipalAlreadyExists">false</Item>
            <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
          </Metadata>
          <IncludeInSso>false</IncludeInSso>
          <InputClaims>
            <InputClaim ClaimTypeReferenceId="objectId" Required="true" />
          </InputClaims>
          <PersistedClaims>
            <!-- Required claims -->
            <PersistedClaim ClaimTypeReferenceId="objectId" />

            <!-- Optional claims -->
            <PersistedClaim ClaimTypeReferenceId="givenName" />
            <PersistedClaim ClaimTypeReferenceId="surname" />
            <PersistedClaim ClaimTypeReferenceId="extension_loyaltyId" />

          </PersistedClaims>
          <IncludeTechnicalProfile ReferenceId="AAD-Common" />
        </TechnicalProfile>
```
7. <span data-ttu-id="a9345-169">Ajouter la revendication dans la valeur de hello tooread TechnicalProfile « AAD-UserReadUsingObjectId » de l’attribut extension hello chaque fois qu’un utilisateur se connecte.</span><span class="sxs-lookup"><span data-stu-id="a9345-169">Add claim in TechnicalProfile "AAD-UserReadUsingObjectId" tooread hello value of hello extension attribute every time a user logs in.</span></span> <span data-ttu-id="a9345-170">Jusque-là hello TechnicalProfiles ont été modifiés dans les flux hello de comptes locaux uniquement.</span><span class="sxs-lookup"><span data-stu-id="a9345-170">Thus far hello TechnicalProfiles have been changed in hello flow of local accounts only.</span></span>  <span data-ttu-id="a9345-171">Si le nouvel attribut de hello est souhaité dans le flux hello d’un compte sociale/fédérée, un ensemble différent de TechnicalProfiles doit toobe modifié.</span><span class="sxs-lookup"><span data-stu-id="a9345-171">If hello new attribute is desired in hello flow of a social/federated account, a different set of TechnicalProfiles needs toobe changed.</span></span> <span data-ttu-id="a9345-172">Reportez-vous aux étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="a9345-172">See Next Steps.</span></span>

```xml
<!-- hello following technical profile is used tooread data after user authenticates. -->
     <TechnicalProfile Id="AAD-UserReadUsingObjectId">
       <Metadata>
         <Item Key="Operation">Read</Item>
         <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
       </Metadata>
       <IncludeInSso>false</IncludeInSso>
       <InputClaims>
         <InputClaim ClaimTypeReferenceId="objectId" Required="true" />
       </InputClaims>
       <OutputClaims>
         <!-- Optional claims -->
         <OutputClaim ClaimTypeReferenceId="signInNames.emailAddress" />
         <OutputClaim ClaimTypeReferenceId="displayName" />
         <OutputClaim ClaimTypeReferenceId="otherMails" />
         <OutputClaim ClaimTypeReferenceId="givenName" />
         <OutputClaim ClaimTypeReferenceId="surname" />
         <OutputClaim ClaimTypeReferenceId="extension_loyaltyId" />
       </OutputClaims>
       <IncludeTechnicalProfile ReferenceId="AAD-Common" />
     </TechnicalProfile>
```


>[!IMPORTANT]
><span data-ttu-id="a9345-173">élément IncludeTechnicalProfile de Hello ajoute tous les éléments de hello de AAD courantes toothis TechnicalProfile.</span><span class="sxs-lookup"><span data-stu-id="a9345-173">hello IncludeTechnicalProfile element adds all hello elements of AAD-Common toothis TechnicalProfile.</span></span>

## <a name="test-hello-custom-policy-using-run-now"></a><span data-ttu-id="a9345-174">Tester une stratégie personnalisée de hello à l’aide de « Exécuter maintenant »</span><span class="sxs-lookup"><span data-stu-id="a9345-174">Test hello custom policy using "Run Now"</span></span>
1. <span data-ttu-id="a9345-175">Ouvrez hello **Azure AD B2C panneau** et accédez trop**identité expérience Framework > stratégies personnalisées**.</span><span class="sxs-lookup"><span data-stu-id="a9345-175">Open hello **Azure AD B2C Blade** and navigate too**Identity Experience Framework > Custom policies**.</span></span>
1. <span data-ttu-id="a9345-176">Stratégie personnalisée hello que vous avez téléchargé, puis cliquez sur hello **exécuter maintenant** bouton.</span><span class="sxs-lookup"><span data-stu-id="a9345-176">Select hello custom policy that you uploaded, and click hello **Run now** button.</span></span>
1. <span data-ttu-id="a9345-177">Vous devez être en mesure de toosign à l’aide d’une adresse de messagerie.</span><span class="sxs-lookup"><span data-stu-id="a9345-177">You should be able toosign up using an email address.</span></span>

<span data-ttu-id="a9345-178">le jeton d’id Hello a renvoyé tooyour application inclut la nouvelle propriété d’extension hello comme une revendication personnalisée précédée par extension_loyaltyId.</span><span class="sxs-lookup"><span data-stu-id="a9345-178">hello  id token sent back tooyour application includes hello new extension property as a custom claim preceded by extension_loyaltyId.</span></span> <span data-ttu-id="a9345-179">Consultez les exemples.</span><span class="sxs-lookup"><span data-stu-id="a9345-179">See example.</span></span>

```
{
  "exp": 1493585187,
  "nbf": 1493581587,
  "ver": "1.0",
  "iss": "https://login.microsoftonline.com/f06c2fe8-709f-4030-85dc-38a4bfd9e82d/v2.0/",
  "sub": "a58e7c6c-7535-4074-93da-b0023fbaf3ac",
  "aud": "4e87c1dd-e5f5-4ac8-8368-bc6a98751b8b",
  "acr": "b2c_1a_trustframeworkprofileedit",
  "nonce": "defaultNonce",
  "iat": 1493581587,
  "auth_time": 1493581587,
  "extension_loyaltyId": "abc",
  "city": "Redmond"
}
```

## <a name="next-steps"></a><span data-ttu-id="a9345-180">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a9345-180">Next steps</span></span>

<span data-ttu-id="a9345-181">Ajouter hello nouvelle revendication toohello des flux pour les connexions de réseaux sociaux compte en modifiant hello TechnicalProfiles répertoriés.</span><span class="sxs-lookup"><span data-stu-id="a9345-181">Add hello new claim toohello flows for social account logins by changing hello TechnicalProfiles listed.</span></span> <span data-ttu-id="a9345-182">Ces deux TechnicalProfiles sont utilisées par compte sociale/fédéré connexions toowrite et lire les données d’utilisateur hello à l’aide de hello alternativeSecurityId comme hello recherche d’objet d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="a9345-182">These two TechnicalProfiles are used by social/federated account logins toowrite and read hello user data using hello alternativeSecurityId as hello locator of hello user object.</span></span>
```
  <TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">

  <TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```

<span data-ttu-id="a9345-183">À l’aide de hello même attributs d’extension entre les stratégies intégrées et personnalisées.</span><span class="sxs-lookup"><span data-stu-id="a9345-183">Using hello same extension attributes between built-in and custom policies.</span></span>
<span data-ttu-id="a9345-184">Lorsque vous ajoutez des attributs d’extension (c'est-à-dire dans les attributs personnalisés) via l’utilisation du portail hello, ces attributs sont inscrits à l’aide de hello ** b2c-extensions-app qui existe dans chaque locataire b2c.</span><span class="sxs-lookup"><span data-stu-id="a9345-184">When you add extension attributes (aka custom attributes) via hello portal experience, those attributes are registered using hello **b2c-extensions-app that exists in every b2c tenant.</span></span>  <span data-ttu-id="a9345-185">toouse ces attributs d’extension dans votre stratégie personnalisée :</span><span class="sxs-lookup"><span data-stu-id="a9345-185">toouse these extension attributes in your custom policy:</span></span>
1. <span data-ttu-id="a9345-186">Au sein de votre client b2c dans portal.azure.com, accédez trop**Azure Active Directory** et sélectionnez **inscriptions d’application**</span><span class="sxs-lookup"><span data-stu-id="a9345-186">Within your b2c tenant in portal.azure.com, navigate too**Azure Active Directory** and select **App registrations**</span></span>
2. <span data-ttu-id="a9345-187">Recherchez **b2c-extensions-app**, puis sélectionnez-la.</span><span class="sxs-lookup"><span data-stu-id="a9345-187">Find your **b2c-extensions-app** and select it</span></span>
3. <span data-ttu-id="a9345-188">Sous hello d’enregistrement 'Essentials' **ID d’Application** et hello **ID d’objet**</span><span class="sxs-lookup"><span data-stu-id="a9345-188">Under 'Essentials' record hello **Application ID** and hello **Object ID**</span></span>
4. <span data-ttu-id="a9345-189">Ajoutez-les aux métadonnées de votre profil technique AAD-Common de la façon suivante :</span><span class="sxs-lookup"><span data-stu-id="a9345-189">Include them in your AAD-Common Technical profile metadata like as follows:</span></span>

```xml
    <ClaimsProviders>
        <ClaimsProvider>
              <DisplayName>Azure Active Directory</DisplayName>
            <TechnicalProfile Id="AAD-Common">
              <DisplayName>Azure Active Directory</DisplayName>
              <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.AzureActiveDirectoryProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
              <!-- Provide objectId and appId before using extension properties. -->
              <Metadata>
                <Item Key="ApplicationObjectId">insert objectId here</Item> <!-- This is hello "Object ID" from hello "b2c-extensions-app"-->
                <Item Key="ClientId">insert appId here</Item> <!--This is hello "Application ID" from hello "b2c-extensions-app"-->
              </Metadata>
```

<span data-ttu-id="a9345-190">cohérence tookeep avec l’expérience du portail hello, créez ces attributs à l’aide d’interface utilisateur du portail hello *avant* vous les utilisez dans vos stratégies personnalisées.</span><span class="sxs-lookup"><span data-stu-id="a9345-190">tookeep consistency with hello portal experience, create these attributes using hello portal UI *before* you use them in your custom policies.</span></span>  <span data-ttu-id="a9345-191">Lorsque vous créez un attribut « ActivationStatus » dans le portail de hello, vous devez faire référence tooit comme suit :</span><span class="sxs-lookup"><span data-stu-id="a9345-191">When you create an attribute "ActivationStatus" in hello portal, you must refer tooit as follows:</span></span>

```
extension_ActivationStatus in hello custom policy
extension_<app-guid>_ActivationStatus via hello Graph API.
```


## <a name="reference"></a><span data-ttu-id="a9345-192">Référence</span><span class="sxs-lookup"><span data-stu-id="a9345-192">Reference</span></span>

* <span data-ttu-id="a9345-193">A **profil technique (TP)** est un type d’élément qui peut être considéré comme un *fonction* qui définit le nom d’un point de terminaison, ses métadonnées, son protocole et détails hello exchange de revendications hello d’identité Expérience Framework doit effectuer.</span><span class="sxs-lookup"><span data-stu-id="a9345-193">A **Technical Profile (TP)** is an element type that can be thought of as a *function* that defines an endpoint’s name, its metadata, its protocol, and details hello exchange of claims that hello Identity Experience Framework should perform.</span></span>  <span data-ttu-id="a9345-194">Lorsque cela *fonction* est appelée dans une étape d’orchestration ou à partir d’un autre TechnicalProfile, hello InputClaims et OutputClaims sont fournies par l’appelant de hello en tant que paramètres.</span><span class="sxs-lookup"><span data-stu-id="a9345-194">When this *function* is called in an orchestration step or from another TechnicalProfile, hello InputClaims and OutputClaims are provided as parameters by hello caller.</span></span>


* <span data-ttu-id="a9345-195">Pour un traitement complet sur les propriétés d’extension, consultez l’article hello [Active les EXTENSIONS de schéma | CONCEPTS DE L’API GRAPH](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)</span><span class="sxs-lookup"><span data-stu-id="a9345-195">For full treatment on extension properties, see hello article [DIRECTORY SCHEMA EXTENSIONS | GRAPH API CONCEPTS](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)</span></span>

>[!NOTE]
><span data-ttu-id="a9345-196">Attributs d’extension dans l’API Graph sont nommées à l’aide de la convention de hello `extension_ApplicationObjectID_attributename`.</span><span class="sxs-lookup"><span data-stu-id="a9345-196">Extension attributes in Graph API are named using hello convention `extension_ApplicationObjectID_attributename`.</span></span> <span data-ttu-id="a9345-197">Les stratégies personnalisées pour désigner les attributs tooextensions extension_attributename, par conséquent, l’omission de hello ApplicationObjectId Bonjour XML</span><span class="sxs-lookup"><span data-stu-id="a9345-197">Custom policies refer tooextensions attributes as extension_attributename, thus omitting hello ApplicationObjectId in hello XML</span></span>
