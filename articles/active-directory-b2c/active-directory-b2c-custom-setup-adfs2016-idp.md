---
title: "Azure Active Directory B2C : Ajout d’ADFS en tant que fournisseur d’identités SAML à l’aide de stratégies personnalisées"
description: "Une procédure-tooarticle sur la configuration de 2016 ADFS à l’aide du protocole SAML et les stratégies personnalisées"
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
ms.openlocfilehash: 30fb7700e7834e3d91fab1fc1b169b761584b204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-adfs-as-a-saml-identity-provider-using-custom-policies"></a>Azure Active Directory B2C : Ajout d’ADFS en tant que fournisseur d’identités SAML à l’aide de stratégies personnalisées

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Cet article vous explique comment tooenable connectez-vous pour les utilisateurs de compte AD FS via l’utilisation de hello de [des stratégies personnalisées](active-directory-b2c-overview-custom.md).

## <a name="prerequisites"></a>Composants requis

Hello terminé les étapes Bonjour [mise en route avec les stratégies personnalisées](active-directory-b2c-get-started-custom.md) l’article.

Ces étapes sont les suivantes :

1.  Création d’une approbation de partie de confiance ADFS.
2.  Ajout de hello ADFS de confiance certificat tooAzure AD B2C.
3.  Ajout de stratégie tooa de fournisseur de revendications.
4.  Compte d’ADFS hello l’enregistrement des revendications voyage de fournisseur tooa utilisateur.
5.  Téléchargement de stratégie de hello tooan Azure AD B2C de client et de le tester.

## <a name="toocreate-a-claims-aware-relying-party-trust"></a>toocreate une approbation de partie de confiance prenant en charge les revendications

toouse AD FS en tant que fournisseur d’identité dans Azure Active Directory (Azure AD) B2C, vous devez toocreate une ADFS de confiance et lui fournir les paramètres appropriés hello.

tooadd une nouvelle partie de confiance faire confiance à l’aide de composant logiciel enfichable hello AD FS Management et configurer manuellement les paramètres de hello, effectuer hello suivant la procédure sur un serveur de fédération.

L’appartenance au **administrateurs**, ou équivalent, sur l’ordinateur local de hello est toocomplete requise minimale de hello cette procédure. Examinez les informations relatives à l’aide des comptes appropriés de hello et les appartenances au groupe [locaux et les groupes de domaine par défaut](http://go.microsoft.com/fwlink/?LinkId=83477)

1.  Dans Gestionnaire de serveur, cliquez sur **Outils**, puis sélectionnez sur **Gestion ADFS**.

2.  Cliquez sur **Ajouter une approbation de partie de confiance**.
    ![Ajouter une approbation de partie de confiance](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-1.png)

3.  Sur hello **Bienvenue** choisissez **prenant en charge des revendications** et cliquez sur **Démarrer**.
    ![Sur la page d’accueil hello, choisissez prenant en charge des revendications](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-2.png)
4.  Sur hello **sélectionner une Source de données** , cliquez sur **entrer manuellement les données sur la partie de confiance hello**, puis cliquez sur **suivant**.
    ![Entrer des informations sur la partie de confiance hello](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-3.png)

5.  Sur hello **spécifier le nom complet** , tapez un nom dans **nom d’affichage**, sous **Notes** tapez une description pour cette partie de confiance, puis cliquez sur **suivant** .
    ![Spécifier le nom d’affichage et les notes](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-4.png)
6.  facultatif. Si vous avez un certificat de chiffrement de jeton facultatif, puis sur hello **configurer le certificat** , cliquez sur **Parcourir** toolocate votre fichier de certificat, puis cliquez sur **suivant** .
    ![Configurer le certificat](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-5.png)
7.  Sur hello **configurer l’URL** page, sélectionnez hello **activer la prise en charge de hello protocole WebSSO SAML 2.0** case à cocher. Sous **URL du service SSO SAML 2.0 confiance**, tapez l’URL du point de terminaison du service Security Assertion Markup Language (SAML) hello pour cette partie de confiance, puis cliquez sur **suivant**.  Pourquoi **URL du service SSO SAML 2.0 confiance**, collez hello `https://login.microsoftonline.com/te/{tenant}.onmicrosoft.com/{policy}`. Remplacez {tenant} avec le nom de votre locataire (par exemple, contosob2c.onmicrosoft.com) et remplacez hello {stratégie} avec votre nom de la stratégie extensions (par exemple, B2C_1A_TrustFrameworkExtensions).
    > [!IMPORTANT]
    >nom de la stratégie Hello est hello une stratégie de signup_or_signin hérite, dans ce cas, il est : `B2C_1A_TrustFrameworkExtensions`.
    >Par exemple hello URL peut être : https://login.microsoftonline.com/te/**contosob2c**.onmicrosoft.com/**B2C_1A_TrustFrameworkBase**.

    ![URL du service SSO SAML 2.0 de la partie de confiance](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-6.png)
8. Sur hello **configurer les identificateurs** , spécifiez hello même URL que l’étape précédente de hello, cliquez sur **ajouter** tooadd les toohello liste, puis cliquez sur **suivant**.
    ![Identificateurs d’approbation de partie de confiance](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-7.png)
9.  Sur hello **stratégie de contrôle d’accès choisissez** sélectionner une stratégie, puis cliquez sur **suivant**.
    ![Choisir la stratégie de contrôle d’accès](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-8.png)
10.  Sur hello **tooAdd approbation de prêt** page, passez en revue les paramètres de hello, puis cliquez sur **suivant** toosave les informations de confidentialité de votre partie de confiance.
    ![Enregistrer vos informations d’approbation de partie de confiance](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-9.png)
11.  Sur hello **Terminer** , cliquez sur **fermer**, cette action affiche automatiquement hello **modifier les règles de revendication** boîte de dialogue.
    ![Modifier les règles de revendication](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-10.png)
12. Cliquez sur **Ajouter une règle**.  
      ![Ajouter une nouvelle règle](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-1.png)
13.  Dans **Modèle de règle de revendication**, sélectionnez **Envoyer les attributs LDAP en tant que revendications**.
    ![Sélectionner la règle de modèle « Envoyer les attributs LDAP comme des revendications »](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-2.png)
14.  Fournissez le **Nom de règle de revendication**. Pourquoi **magasin d’attributs** sélectionnez **Sélectionnez Active Directory** ajouter hello suivant des revendications, puis cliquez sur **Terminer** et **OK**.
    ![Définir les propriétés de règle](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-3.png)
15.  Dans le Gestionnaire de serveur, sélectionnez **confiance** sélectionnez hello de confiance vous avez créé, puis cliquez sur **propriétés**.
    ![Modifier les propriétés de la partie de confiance](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-1.png)
16.  Un hello partie de confiance tiers fenêtre de propriétés d’approbation (B2C démo) cliquez sur **Signature** onglet et cliquez sur **ajouter**.  
    ![Définir signature](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-2.png)
17.  Ajoutez votre certificat de signature (fichier .cert sans clé privée).  
    ![Ajouter votre certificat de signature](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-3.png)
18.  Fenêtre de propriétés d’approbation (B2C démo) tiers hello partie de confiance sur **avancé** onglet et modifier hello **algorithme de hachage sécurisé** trop**SHA-1**, cliquez sur **surOk**.  
    ![Définir l’algorithme de hachage sécurisé tooSHA-1](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-4.png)

## <a name="add-hello-adfs-account-application-key-tooazure-ad-b2c"></a>Ajouter hello ADFS compte application clé tooAzure AD B2C
Fédération avec les comptes AD FS requiert une clé secrète client pour ADFS tootrust de compte Azure AD B2C au nom de l’application hello. Vous avez besoin de toostore votre certificat ADFS dans votre locataire Azure AD B2C. 

1.  Accédez tooyour Azure AD B2C client, puis sélectionnez **B2C paramètres** > **infrastructure expérience d’identité**
2.  Sélectionnez **clés de stratégie** tooview hello disponibles dans votre client.
3.  Cliquez sur **+Ajouter**.
4.  Pour **Options**, utilisez **Télécharger**.
5.  Pour **Nom**, utilisez `ADFSSamlCert`.  
    préfixe de Hello `B2C_1A_` peuvent être ajoutées automatiquement.
6.  Dans le téléchargement du fichier hello, ** sélectionnez votre fichier de certificat .pfx avec la clé privée. Remarque : ce certificat (avec la clé privée de hello) doit être hello même que celui qui a délivré et utilisé pour la partie de confiance AD FS hello.
![Télécharger la clé de stratégie](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-cert.png)
7.  Cliquez sur **Créer**
8.  Vérifiez que vous avez créé la clé de hello `B2C_1A_ADFSSamlCert`.

## <a name="add-a-claims-provider-in-your-extension-policy"></a>Ajouter un fournisseur de revendications à une stratégie d’extension
Si vous souhaitez que les utilisateurs toosign à l’aide du compte d’ADFS, vous devez compte ADFS de toodefine comme fournisseur de revendications. En d’autres termes, vous devez toospecify un point de terminaison Azure AD B2C communique avec. point de terminaison Hello fournit un ensemble de revendications qui sont utilisées par Azure AD B2C tooverify authentifié un utilisateur spécifique.

Définissez ADFS comme fournisseur de revendications, en ajoutant le nœud `<ClaimsProvider>` dans votre fichier de stratégie d’extension :

1. Ouvrez le fichier de stratégie d’extension hello (TrustFrameworkExtensions.xml) à partir de votre répertoire de travail. Si vous avez besoin d’un éditeur XML, [essayez Visual Studio Code](https://code.visualstudio.com/download), un éditeur multiplateforme léger.
2. Recherche hello `<ClaimsProviders>` section
3. Ajouter hello suivant extrait de code XML sous hello `ClaimsProviders` élément et remplacer `identityProvider` avec votre serveur DNS (valeur arbitraire qui indique votre domaine) et enregistrer le fichier de hello. 

```xml
<ClaimsProvider>
    <Domain>contoso.com</Domain>
    <DisplayName>Contoso ADFS</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="Contoso-SAML2">
        <DisplayName>Contoso ADFS</DisplayName>
        <Description>Login with your Contoso account</Description>
        <Protocol Name="SAML2"/>
        <Metadata>
        <Item Key="RequestsSigned">false</Item>
        <Item Key="WantsEncryptedAssertions">false</Item>
        <Item Key="PartnerEntity">https://{your_ADFS_domain}/federationmetadata/2007-06/federationmetadata.xml</Item>
        </Metadata>
        <CryptographicKeys>
        <Key Id="SamlAssertionSigning" StorageReferenceId="B2C_1A_ADFSSamlCert"/>
        <Key Id="SamlMessageSigning" StorageReferenceId="B2C_1A_ADFSSamlCert"/>
        </CryptographicKeys>
        <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="userPrincipalName" />
        <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name"/>
        <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name"/>
        <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email"/>
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name"/>
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="contoso.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication"/>
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

## <a name="register-hello-adfs-account-claims-provider-toosign-up-or-sign-in-user-journey"></a>Inscrire hello ADFS compte revendications fournisseur tooSign des ou se connecter dans le parcours de l’utilisateur
À ce stade, le fournisseur d’identité hello a été configuré.  Toutefois, il n’est pas disponible dans les écrans de connexion-haut/connectez-vous hello. Maintenant vous devez utilisateur tooyour fournisseur de l’identité tooadd hello ADFS compte `SignUpOrSignIn` parcours de l’utilisateur. toomake il est disponible, nous créons un doublon d’un déplacement de modèle à l’utilisateur existant.  Ensuite, nous la modifier pour qu’elle comporte le fournisseur d’identité ADFS hello :
    >[!NOTE]
    >If you previously copied hello `<UserJourneys>` element from base file of your policy toohello extension file (TrustFrameworkExtensions.xml) you can skip this section.
1.  Ouvrez le fichier de base hello de votre stratégie (par exemple, TrustFrameworkBase.xml).
2.  Recherche hello `<UserJourneys>` élément et copie hello ensemble du contenu de `<UserJourneys>` nœud.
3.  Ouvrez le fichier d’extension hello (par exemple, TrustFrameworkExtensions.xml) et recherche hello `<UserJourneys>` élément. Si l’élément de hello n’existe pas, ajoutez-en un.
4.  Coller le contenu entier de hello de `<UserJournesy>` nœud que vous avez copié en tant qu’enfant de hello `<UserJourneys>` élément.

### <a name="display-hello-button"></a>Bouton d’affichage hello
Hello `<ClaimsProviderSelections>` élément définit la liste hello des options de sélection de fournisseur de revendications et leur ordre.  `<ClaimsProviderSelection>`élément est un bouton de fournisseur d’identité tooan analogue sur une connexion-haut/page de connexion. Si vous ajoutez un `<ClaimsProviderSelection>` élément ADFS compte, un nouveau bouton apparaît lorsqu’un utilisateur arrive sur la page de hello. tooadd cet élément :

1.  Recherche hello `<UserJourney>` nœud incluant `Id="SignUpOrSignIn"` dans voyage utilisateur hello que vous avez copiée.
2.  Recherchez hello `<OrchestrationStep>` nœud qui inclut`Order="1"`
3.  Ajoutez l’extrait de code XML suivant sous le nœud `<ClaimsProviderSelections>` :

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```
### <a name="link-hello-button-tooan-action"></a>Action de lien hello bouton tooan

Maintenant que vous avez un bouton en place, vous devez toolink il tooan action. action de Hello, dans ce cas, est de toocommunicate Azure AD B2C avec ADFS compte tooreceive un jeton. Action de tooan bouton lien hello en liant le profil de technique hello pour votre fournisseur de revendications AD FS compte :

1.  Recherche hello `<OrchestrationStep>` qui inclut `Order="2"` Bonjour `<UserJourney>` nœud.
2.  Ajoutez l’extrait de code XML suivant sous le nœud `<ClaimsExchanges>` :

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

> [!NOTE]
> * Assurez-vous de hello `Id` a hello même valeur que celle de `TargetClaimsExchangeId` Bonjour précédant la section.
> * Vérifiez `TechnicalProfileReferenceId` a la valeur toohello de profil technique vous avez créé plus haut (Contoso-SAML2).

## <a name="upload-hello-policy-tooyour-tenant"></a>Télécharger le client de tooyour stratégie hello
1.  Bonjour [portail Azure](https://portal.azure.com), basculez dans hello [contexte de votre locataire Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md)et ouvrez hello **Azure AD B2C** panneau.
2.  Sélectionnez **Infrastructure d’expérience d’identité**.
3.  Ouvrez hello **toutes les stratégies** panneau.
4.  Sélectionnez **Charger la stratégie**.
5.  Vérifiez **remplacer la stratégie de hello si elle existe** boîte.
6.  **Télécharger** TrustFrameworkExtensions.xml et assurez-vous qu’il validation n’échoue pas hello

## <a name="test-hello-custom-policy-by-using-run-now"></a>Tester une stratégie personnalisée de hello à l’aide d’exécuter maintenant
1.  Ouvrez **paramètres d’Azure AD B2C** et accédez trop**infrastructure d’identité expérience**.
2.  Ouvrez **B2C_1A_signup_signin**, hello stratégie personnalisée partie de confiance (RP) de tiers que vous avez téléchargé. Sélectionnez **Exécuter maintenant**.
3.  Vous devez être en mesure de toosign à l’aide du compte d’ADFS.

## <a name="optional-register-hello-adfs-account-claims-provider-tooprofile-edit-user-journey"></a>[Facultatif] Inscrire le voyage utilisateur de hello ADFS compte revendications fournisseur tooProfile-modifier
Vous pouvez souhaiter fournisseur d’identité tooadd hello ADFS compte également tooyour utilisateur `ProfileEdit` parcours de l’utilisateur. toomake disponibles, nous Répétez hello a deux étapes :

### <a name="display-hello-button"></a>Bouton d’affichage hello
1.  Ouvrez le fichier d’extension hello de votre stratégie (par exemple, TrustFrameworkExtensions.xml).
2.  Recherche hello `<UserJourney>` nœud incluant `Id="ProfileEdit"` dans voyage utilisateur hello que vous avez copiée.
3.  Recherchez hello `<OrchestrationStep>` nœud qui inclut`Order="1"`
4.  Ajoutez l’extrait de code XML suivant sous le nœud `<ClaimsProviderSelections>` :

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```

### <a name="link-hello-button-tooan-action"></a>Action de lien hello bouton tooan
1.  Recherche hello `<OrchestrationStep>` qui inclut `Order="2"` Bonjour `<UserJourney>` nœud.
2.  Ajoutez l’extrait de code XML suivant sous le nœud `<ClaimsExchanges>` :

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a>Tester une stratégie de profil de modification personnalisée hello à l’aide d’exécuter maintenant
1.  Ouvrez **paramètres d’Azure AD B2C** et accédez trop**infrastructure d’identité expérience**.
2.  Ouvrez **B2C_1A_ProfileEdit**, hello stratégie personnalisée partie de confiance (RP) de tiers que vous avez téléchargé. Sélectionnez **Exécuter maintenant**.
3.  Vous devez être en mesure de toosign à l’aide du compte d’ADFS.

## <a name="download-hello-complete-policy-files"></a>Télécharger les fichiers de stratégie complète hello
Facultatif : Nous vous recommandons de que générer votre scénario à l’aide de vos propres fichiers de stratégie personnalisée hello prise en main des stratégies personnalisées guident à la fin. [Exemples de fichiers de stratégie pour référence uniquement](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-adfs2016-app)
