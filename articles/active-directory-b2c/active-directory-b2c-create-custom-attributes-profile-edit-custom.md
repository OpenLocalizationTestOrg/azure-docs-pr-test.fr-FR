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
# <a name="azure-active-directory-b2c-creating-and-using-custom-attributes-in-a-custom-profile-edit-policy"></a>Azure Active Directory B2C : création et utilisation d’attributs personnalisés dans une stratégie personnalisée de modification de profil

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Dans cet article, vous créez un attribut personnalisé dans votre annuaire Azure AD B2C et utilisez ce nouvel attribut comme une revendication personnalisée dans un parcours de hello profil Modifier utilisateur.

## <a name="prerequisites"></a>Composants requis

Hello terminé les étapes dans l’article de hello [prise en main des stratégies personnalisées](active-directory-b2c-get-started-custom.md).

## <a name="use-custom-attributes-toocollect-information-about-your-customers-in-azure-active-directory-b2c-using-custom-policies"></a>Utiliser les informations de toocollect d’attributs personnalisés sur vos clients dans Azure Active Directory B2C, à l’aide de stratégies personnalisées
Votre répertoire Azure Active Directory (Azure AD) B2C est fourni avec un ensemble intégré d’attributs : prénom, nom, ville, code postal, userPrincipalName, etc.  Vous devez souvent toocreate vos propres attributs.  Par exemple :
* Une application côté client doit toopersist un attribut tel que « LoyaltyNumber ».
* Un fournisseur d’identité a un identificateur d’utilisateur unique qui doit être enregistré, par exemple « uniqueUserGUID ».
* Un parcours de l’utilisateur personnalisée a besoin d’état de hello toopersist d’utilisateur, tels que « migrationStatus ».

Avec Azure AD B2C, vous pouvez étendre le jeu hello d’attributs stockés sur chaque compte d’utilisateur. Vous pouvez également lire et écrire ces attributs à l’aide de hello [API Azure AD Graph](active-directory-b2c-devquickstarts-graph-dotnet.md).

Propriétés d’extension étendent le schéma hello des objets utilisateur de hello dans le répertoire de hello.  propriété d’extension Hello termes du contrat, les attributs personnalisés et les revendication personnalisée, consultez toohello même chose dans le contexte de hello de ce nom d’article et hello varie selon le contexte hello (application, objet, de stratégie).

Les propriétés d’extension ne peuvent être inscrites que sur un objet application, même si elles peuvent contenir des données pour un utilisateur. propriété de Hello est attaché toohello application. objet de l’Application Hello doit être accordé un accès en écriture tooregister une propriété d’extension. Propriétés d’extension 100 (pour tous les types et toutes les applications) peuvent être écrits tooany un seul objet. Propriétés d’extension sont ajoutés toohello type d’annuaire cible et devient immédiatement accessibles dans le locataire d’annuaire hello Azure Active Directory B2C.
Si l’application hello est supprimée, les propriétés d’Extension, ainsi que les données contenues dans les pour tous les utilisateurs sont également supprimées. Si une propriété d’extension est supprimée par hello Application, elle est supprimée de hello cibler des objets d’annuaire et hello valeurs supprimés.

Propriétés d’extension existent uniquement dans un contexte d’une Application inscrite dans le locataire de hello hello. id d’objet Hello de l’Application doit être inclus dans hello TechnicalProfile qui l’utilisent.

>[!NOTE]
>répertoire de Hello Azure AD B2C inclut généralement une application Web nommée `b2c-extensions-app`.  Cette application est principalement utilisée par les stratégies intégrées hello b2c pour les revendications personnalisées hello créées via hello portail Azure.  L’utilisation de ce tooregister des extensions d’application pour les stratégies personnalisées b2c est recommandée uniquement pour les utilisateurs expérimentés.  Instructions correspondantes sont inclus dans hello section étapes suivantes dans cet article.


## <a name="creating-a-new-application-toostore-hello-extension-properties"></a>Création d’un nouveau toostore d’application les propriétés d’extension hello

1. Ouvrez une session de navigation et naviguez toohello [le portail Azure](https://portal.azure.com) et connectez-vous avec les informations d’identification administratives de hello annuaire B2C tooconfigure.
1. Cliquez sur **Azure Active Directory** sur le menu de navigation gauche hello. Vous devrez peut-être toofind en sélectionnant plus de services >.
1. Sélectionnez **Inscriptions des applications**, puis cliquez sur **Nouvelle inscription d’application**.
1. Fournir suivant de hello recommandé entrées :
  * Spécifiez un nom pour l’application web de hello : **WebApp-GraphAPI-DirectoryExtensions**
  * Type d’application : application web/API
  * URL d’ouverture de session : https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions
1. Sélectionnez **Créer. Réussite s’affiche dans hello **des notifications**
1. Sélectionnez application web de hello nouvellement créé : **WebApp-GraphAPI-DirectoryExtensions**
1. Dans Paramètres, sélectionnez **Autorisations requises**.
1. Dans API, sélectionnez **Windows Active Directory**.
1. Dans Autorisations d’application, cochez l’option **Lire et écrire les données de l’annuaire**, puis cliquez sur **Enregistrer**.
1. Sélectionnez **Accorder des autorisations**, puis confirmez en cliquant sur **Oui**.
1. Copiez tooyour Presse-papiers et enregistrer hello suivant des identificateurs de WebApp-GraphAPI-DirectoryExtensions > Paramètres > Propriétés >
*  **ID de l’application**. Exemple : `103ee0e6-f92d-4183-b576-8c3739027780`
* **ID objet**. Exemple : `80d8296a-da0a-49ee-b6ab-fd232aa45201`



## <a name="modifying-your-custom-policy-tooadd-hello-applicationobjectid"></a>Modification de votre hello tooadd de stratégie personnalisée ApplicationObjectId

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
>Hello <TechnicalProfile Id="AAD-Common"> est tooas référencé « commune », car ses éléments sont inclus dans et réutilisées dans tous les hello Azure Active Directory TechnicalProfiles à l’aide hello élément :`<IncludeTechnicalProfile ReferenceId="AAD-Common" />`

>[!NOTE]
>Lorsque hello TechnicalProfile écrit pour la propriété d’extension hello première heure toohello nouvellement créé, vous pouvez rencontrer une erreur à usage unique.  propriété d’extension Hello est créée hello première fois, qu'il est utilisé.  

## <a name="using-hello-new-extension-property--custom-attribute-in-a-user-journey"></a>À l’aide de la nouvelle propriété d’extension hello / d’attribut personnalisé dans un parcours de l’utilisateur


1. Hello Ouvrir fichier Party(RP) de partie de confiance qui décrit votre stratégie de modifier le parcours de l’utilisateur.  Si vous démarrez, il peut être conseillée toodownload votre version déjà configurée de hello RP-PolicyEdit fichier directement à partir de hello section de stratégie personnalisée de B2C Azure Bonjour portail Azure.  Vous pouvez également ouvrir votre fichier XML à partir de votre dossier de stockage.
2. Ajoutez une revendication personnalisée `loyaltyId`.  En incluant hello personnalisé de revendication Bonjour `<RelyingParty>` élément, elle est passée comme un paramètre de toohello UserJourney TechnicalProfiles et inclus dans le jeton hello pour une application hello.
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
3. Ajouter un fichier de stratégie de revendication définition toohello Extension `TrustFrameworkExtensions.xml` à l’intérieur de hello `<ClaimsSchema>` élément, comme indiqué.
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
4. Ajouter hello même revendication le fichier de définition de stratégie de Base toohello `TrustFrameworkBase.xml`.  
>Ajout d’un `ClaimType` définition dans la base de hello et fichier des extensions hello n’est normalement pas nécessaire, toutefois, étant donné que les étapes suivantes hello ajoutera hello extension_loyaltyId tooTechnicalProfiles dans le fichier de Base hello, programme de validation de stratégie hello rejette téléchargement de hello hello fichier de base sans lui.
>Il peut être utile tootrace l’exécution de hello hello utilisateur voyage est nommé « ProfileEdit » dans le fichier de TrustFrameworkBase.xml hello.  Recherchez le voyage d’utilisateur hello Hello même nom dans votre éditeur et observez qu’Orchestration étape 5 appelle hello TechnicalProfileReferenceID = « SelfAsserted-ProfileUpdate ».  Rechercher et examiner cette toofamiliarize TechnicalProfile avec les flux hello.
5. Ajouter loyaltyId comme entrée et sortie de revendication Bonjour TechnicalProfile « SelfAsserted-ProfileUpdate »
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
6. Ajoute la revendication dans la valeur de hello toopersist TechnicalProfile « AAD-UserWriteProfileUsingObjectId » de revendication hello dans la propriété d’extension hello, pour l’utilisateur actuel de hello dans le répertoire de hello.
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
7. Ajouter la revendication dans la valeur de hello tooread TechnicalProfile « AAD-UserReadUsingObjectId » de l’attribut extension hello chaque fois qu’un utilisateur se connecte. Jusque-là hello TechnicalProfiles ont été modifiés dans les flux hello de comptes locaux uniquement.  Si le nouvel attribut de hello est souhaité dans le flux hello d’un compte sociale/fédérée, un ensemble différent de TechnicalProfiles doit toobe modifié. Reportez-vous aux étapes suivantes.

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
>élément IncludeTechnicalProfile de Hello ajoute tous les éléments de hello de AAD courantes toothis TechnicalProfile.

## <a name="test-hello-custom-policy-using-run-now"></a>Tester une stratégie personnalisée de hello à l’aide de « Exécuter maintenant »
1. Ouvrez hello **Azure AD B2C panneau** et accédez trop**identité expérience Framework > stratégies personnalisées**.
1. Stratégie personnalisée hello que vous avez téléchargé, puis cliquez sur hello **exécuter maintenant** bouton.
1. Vous devez être en mesure de toosign à l’aide d’une adresse de messagerie.

le jeton d’id Hello a renvoyé tooyour application inclut la nouvelle propriété d’extension hello comme une revendication personnalisée précédée par extension_loyaltyId. Consultez les exemples.

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

## <a name="next-steps"></a>Étapes suivantes

Ajouter hello nouvelle revendication toohello des flux pour les connexions de réseaux sociaux compte en modifiant hello TechnicalProfiles répertoriés. Ces deux TechnicalProfiles sont utilisées par compte sociale/fédéré connexions toowrite et lire les données d’utilisateur hello à l’aide de hello alternativeSecurityId comme hello recherche d’objet d’utilisateur hello.
```
  <TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">

  <TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```

À l’aide de hello même attributs d’extension entre les stratégies intégrées et personnalisées.
Lorsque vous ajoutez des attributs d’extension (c'est-à-dire dans les attributs personnalisés) via l’utilisation du portail hello, ces attributs sont inscrits à l’aide de hello ** b2c-extensions-app qui existe dans chaque locataire b2c.  toouse ces attributs d’extension dans votre stratégie personnalisée :
1. Au sein de votre client b2c dans portal.azure.com, accédez trop**Azure Active Directory** et sélectionnez **inscriptions d’application**
2. Recherchez **b2c-extensions-app**, puis sélectionnez-la.
3. Sous hello d’enregistrement 'Essentials' **ID d’Application** et hello **ID d’objet**
4. Ajoutez-les aux métadonnées de votre profil technique AAD-Common de la façon suivante :

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

cohérence tookeep avec l’expérience du portail hello, créez ces attributs à l’aide d’interface utilisateur du portail hello *avant* vous les utilisez dans vos stratégies personnalisées.  Lorsque vous créez un attribut « ActivationStatus » dans le portail de hello, vous devez faire référence tooit comme suit :

```
extension_ActivationStatus in hello custom policy
extension_<app-guid>_ActivationStatus via hello Graph API.
```


## <a name="reference"></a>Référence

* A **profil technique (TP)** est un type d’élément qui peut être considéré comme un *fonction* qui définit le nom d’un point de terminaison, ses métadonnées, son protocole et détails hello exchange de revendications hello d’identité Expérience Framework doit effectuer.  Lorsque cela *fonction* est appelée dans une étape d’orchestration ou à partir d’un autre TechnicalProfile, hello InputClaims et OutputClaims sont fournies par l’appelant de hello en tant que paramètres.


* Pour un traitement complet sur les propriétés d’extension, consultez l’article hello [Active les EXTENSIONS de schéma | CONCEPTS DE L’API GRAPH](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)

>[!NOTE]
>Attributs d’extension dans l’API Graph sont nommées à l’aide de la convention de hello `extension_ApplicationObjectID_attributename`. Les stratégies personnalisées pour désigner les attributs tooextensions extension_attributename, par conséquent, l’omission de hello ApplicationObjectId Bonjour XML
