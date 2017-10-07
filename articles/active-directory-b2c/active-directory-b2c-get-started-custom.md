---
title: "Azure Active Directory B2C : Bien démarrer avec les stratégies personnalisées | Microsoft Docs"
description: "Comment tooget main d’Azure Active Directory B2C des stratégies personnalisées"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 658c597e-3787-465e-b377-26aebc94e46d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: joroja;parahk;gsacavdm
ms.openlocfilehash: 5ee133806395cddf18682769a6cad149889d82d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-get-started-with-custom-policies"></a>Azure Active Directory B2C : bien démarrer avec les stratégies personnalisées

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Après avoir terminé les étapes de hello dans cet article, votre stratégie personnalisée prend en charge « compte » s’inscrire ou se connecter à l’aide d’une adresse de messagerie et le mot de passe. Vous préparez également votre environnement à l’ajout de fournisseurs d’identité (par exemple Facebook ou Azure AD). Nous vous encourageons toocomplete ces étapes avant d’être lu sur d’autres utilisations de hello infrastructure d’expérience identité Azure Active Directory (Azure AD) B2C.

## <a name="prerequisites"></a>Composants requis

Avant de continuer, vérifiez que vous disposez d’un locataire Azure AD B2C, qui est pour l’ensemble de vos utilisateurs, applications, stratégies, etc. Si vous n’avez pas déjà, vous devez trop[créer un client Azure AD B2C](active-directory-b2c-get-started.md). Fortement, nous encourageons tous les développeurs de toocomplete hello procédures pas à pas de Azure AD B2C stratégie intégrée et configurer leurs applications avec des stratégies intégrées avant de continuer. Une fois que vous apportez une modification mineure toohello stratégie nom tooinvoke hello stratégie personnalisée, vos applications fonctionneront avec les deux types de stratégies.

>[!NOTE]
>tooaccess modification de la stratégie personnalisée, vous avez besoin d’un client de tooyour lié abonnement Azure valide. Si vous n’avez pas [lié votre tooan de locataire Azure AD B2C abonnement Azure](active-directory-b2c-how-to-enable-billing.md) ou votre abonnement Azure est désactivé, le bouton d’infrastructure d’identité expérience hello n’est pas disponible.

## <a name="add-signing-and-encryption-keys-tooyour-b2c-tenant-for-use-by-custom-policies"></a>Ajout d’un locataire de tooyour B2C clés de signature et de chiffrement pour une utilisation par les stratégies personnalisées

1. Ouvrez hello **infrastructure d’identité expérience** lame dans vos paramètres de client Azure Active Directory B2C.
2. Sélectionnez **clés de stratégie** tooview hello disponibles dans votre client.
3. S’il n’existe pas, créez B2C_1A_TokenSigningKeyContainer :<br>
    a. Sélectionnez **Ajouter**. <br>
    b. Sélectionnez **Générer**.<br>
    c. Pour **Nom**, utilisez `TokenSigningKeyContainer`. <br> 
    préfixe de Hello `B2C_1A_` peuvent être ajoutées automatiquement.<br>
    d. Pour **Type de clé**, utilisez **RSA**.<br>
    e. Pour **Dates**, utilisez les valeurs par défaut hello. <br>
    f. Pour **Utilisation de la clé**, utilisez **Signature**.<br>
    g. Sélectionnez **Créer**.<br>
4. S’il n’existe pas, créez B2C_1A_TokenEncryptionKeyContainer :<br>
 a. Sélectionnez **Ajouter**.<br>
 b. Sélectionnez **Générer**.<br>
 c. Pour **Nom**, utilisez `TokenEncryptionKeyContainer`. <br>
   préfixe de Hello `B2C_1A`_ peuvent être ajoutées automatiquement.<br>
 d. Pour **Type de clé**, utilisez **RSA**.<br>
 e. Pour **Dates**, utilisez les valeurs par défaut hello.<br>
 f. Pour **Utilisation de la clé**, utilisez **Chiffrement**.<br>
 g. Sélectionnez **Créer**.<br>
5. Créez B2C_1A_FacebookSecret. <br>
Si vous disposez déjà d’un secret d’application Facebook, ajoutez-le en tant que stratégie clé tooyour client. Dans le cas contraire, vous devez créer la clé de hello avec une valeur d’espace réservé afin que vos stratégies passé la validation du.<br>
 a. Sélectionnez **Ajouter**.<br>
 b. Pour **Options**, utilisez **Manuel**.<br>
 c. Pour **Nom**, utilisez `FacebookSecret`. <br>
 préfixe de Hello `B2C_1A_` peuvent être ajoutées automatiquement.<br>
 d. Bonjour **Secret** , entrez votre FacebookSecret de developers.facebook.com ou `0` comme espace réservé. *Il ne s’agit pas de votre ID d’application Facebook.* <br>
 e. Pour **Utilisation de la clé**, utilisez **Signature**. <br>
 f. Cliquez sur **Créer** et confirmez la création.

## <a name="register-identity-experience-framework-applications"></a>Inscrire les applications de l’infrastructure d’expérience d’identité

Azure AD B2C nécessite tooregister deux applications supplémentaires qui sont utilisées par toosign de moteur hello haut et connecter les utilisateurs.

>[!NOTE]
>Vous devez créer deux applications qui activer connectez-vous à l’aide de comptes locaux : IdentityExperienceFramework (une application web) et ProxyIdentityExperienceFramework (une application native) avec une autorisation à partir de l’application de IdentityExperienceFramework hello de délégué. Les comptes locaux existent uniquement dans votre client. Vos utilisateurs s’inscrire avec un tooaccess de combinaison adresse/mot de passe par courrier électronique unique vos applications client inscrit.

### <a name="create-hello-identityexperienceframework-application"></a>Créer l’application de IdentityExperienceFramework hello

1. Bonjour [portail Azure](https://portal.azure.com), basculez dans hello [contexte de votre locataire Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md).
2. Ouvrez hello **Azure Active Directory** blade (pas hello **Azure AD B2C** panneau). Vous devrez peut-être tooselect **plus Services** toofind il.
3. Sélectionnez **Inscriptions d’applications**.
4. Sélectionnez **Nouvelle inscription d’application**.
   * Pour **Nom**, utilisez `IdentityExperienceFramework`.
   * Pour **Type d’application**, utilisez **Application/API web**.
   * Pour **URL de connexion**, utilisez `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`, où `yourtenant` est le nom de domaine de votre locataire Azure AD B2C.
5. Sélectionnez **Créer**.
6. Lorsqu’il est créé, sélectionnez l’application hello nouvellement créé **IdentityExperienceFramework**.<br>
   * Sélectionner **Propriétés**.<br>
   * Copiez l’ID de l’application hello et l’enregistrer pour une date ultérieure.

### <a name="create-hello-proxyidentityexperienceframework-application"></a>Créer l’application de ProxyIdentityExperienceFramework hello

1. Sélectionnez **Inscriptions d’applications**.
1. Sélectionnez **Nouvelle inscription d’application**.
   * Pour **Nom**, utilisez `ProxyIdentityExperienceFramework`.
   * Pour **Type d’application**, utilisez **Native**.
   * Pour **URI de redirection**, utilisez `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`, où `yourtenant` est votre locataire Azure AD B2C.
1. Sélectionnez **Créer**.
1. Une fois qu’il a été créé, sélectionnez l’application hello **ProxyIdentityExperienceFramework**.<br>
   * Sélectionner **Propriétés**. <br>
   * Copiez l’ID de l’application hello et l’enregistrer pour une date ultérieure.
1. Sélectionnez **Autorisations requises**.
1. Sélectionnez **Ajouter**.
1. Sélectionnez **Sélectionner une API**.
1. Rechercher le nom hello IdentityExperienceFramework. Sélectionnez **IdentityExperienceFramework** dans hello des résultats, puis cliquez sur **sélectionnez**.
1. Cochez hello ensuite trop**accès IdentityExperienceFramework**, puis cliquez sur **sélectionnez**.
1. Sélectionnez **Terminé**.
1. Sélectionnez **Accorder des autorisations** puis confirmez en sélectionnant **Oui**.

## <a name="download-starter-pack-and-modify-policies"></a>Télécharger le pack de démarrage et modifier les stratégies

Les stratégies personnalisées sont un ensemble de fichiers XML qui doivent toobe téléchargé tooyour Azure AD B2C locataire. Nous fournissons starter packs tooget vous faire rapidement. Chaque pack starter Bonjour suivant liste contient hello plus petit nombre de profils techniques et des trajets utilisateur nécessaire les scénarios de hello tooachieve décrits :
 * LocalAccounts. Permet d’utiliser de hello de comptes locaux uniquement.
 * SocialAccounts. Permet d’utiliser de hello de comptes sociaux (ou fédérées) uniquement.
 * **SocialAndLocalAccounts**. Nous utilisons ce fichier pour la procédure pas à pas hello.
 * SocialAndLocalAccountsWithMFA. Les options d’authentification sociale, locale et multifacteur sont incluses ici.

Chaque pack de démarrage contient :

* Hello [fichier de base](active-directory-b2c-overview-custom.md#policy-files) de stratégie de hello. Peu de modifications est requise toohello de base.
* Hello [fichier d’extension](active-directory-b2c-overview-custom.md#policy-files) de stratégie de hello.  C’est sur ce fichier que portent la plupart des modifications de la configuration.
* Les [fichiers de partie de confiance](active-directory-b2c-overview-custom.md#policy-files) sont des fichiers propres à chaque tâche, appelés par l’application.

>[!NOTE]
>Si votre éditeur XML prend en charge la validation, valider les fichiers de hello contre hello TrustFrameworkPolicy_0.3.0.0.xsd XSD qui se trouve dans le répertoire racine de hello du pack de démarrage hello. La validation du schéma XML identifie les erreurs avant le chargement.

 C’est parti :

1. Téléchargez active-directory-b2c-custom-policy-starterpack depuis GitHub. [Téléchargez le fichier .zip de hello](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/archive/master.zip) ou exécutez

    ```console
    git clone https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack
    ```
2. Ouvrez le dossier de SocialAndLocalAccounts hello.  fichier de base Hello (TrustFrameworkBase.xml) dans ce dossier contient le contenu nécessaire pour les comptes locaux et sociale/entreprise. contenu de réseaux sociaux Hello n’interfère pas avec les étapes hello pour l’obtention des comptes locaux et en cours d’exécution.
3. Ouvrez TrustFrameworkBase.xml. Si vous avez besoin d’un éditeur XML, [essayez Visual Studio Code](https://code.visualstudio.com/download), un éditeur multiplateforme léger.
4. Dans la racine de hello `TrustFrameworkPolicy` élément, de mise à jour hello `TenantId` et `PublicPolicyUri` attributs, en remplaçant `yourtenant.onmicrosoft.com` avec le nom de domaine hello de votre locataire Azure AD B2C :
   ```xml
    <TrustFrameworkPolicy
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:xsd="http://www.w3.org/2001/XMLSchema"
    xmlns="http://schemas.microsoft.com/online/cpim/schemas/2013/06"
    PolicySchemaVersion="0.3.0.0"
    TenantId="yourtenant.onmicrosoft.com"
    PolicyId="B2C_1A_TrustFrameworkBase"
    PublicPolicyUri="http://yourtenant.onmicrosoft.com">
    ```
   >[!NOTE]
   >`PolicyId`est le nom de la stratégie hello que vous voyez dans le portail de hello et nom hello par lequel ce fichier de stratégie est référencé par d’autres fichiers de stratégie.

5. Enregistrez le fichier de hello.
6. Ouvrez TrustFrameworkExtensions.xml. Apporter des deux modifications hello en remplaçant `yourtenant.onmicrosoft.com` avec votre client Azure Active Directory B2C. Rendre hello même remplacement Bonjour `<TenantId>` élément pour un total de trois modifications. Enregistrez le fichier de hello.
7. Ouvrez SignUpOrSignIn.xml. Apporter des modifications mêmes hello en remplaçant `yourtenant.onmicrosoft.com` avec votre client Azure AD B2C dans trois emplacements. Enregistrez le fichier de hello.
8. Ouvrez hello réinitialiser et profil de modifier des fichiers. Apporter des modifications mêmes hello en remplaçant `yourtenant.onmicrosoft.com` avec votre client Azure AD B2C trois emplacements dans chaque fichier. Enregistrez les fichiers hello.

### <a name="add-hello-application-ids-tooyour-custom-policy"></a>Ajouter la stratégie personnalisée tooyour ID d’application hello
Ajoutez le fichier extensions toohello hello application ID (`TrustFrameworkExtensions.xml`) :

1. Dans le fichier des extensions hello (TrustFrameworkExtensions.xml), rechercher les élément hello `<TechnicalProfile Id="login-NonInteractive">`.
2. Remplacez les deux instances de `IdentityExperienceFrameworkAppId` avec l’ID d’application hello Hello application infrastructure expérience d’identité que vous avez créé précédemment. Voici un exemple :

   ```xml
   <Item Key="client_id">8322dedc-cbf4-43bc-8bb6-141d16f0f489</Item>
   ```
3. Remplacez les deux instances de `ProxyIdentityExperienceFrameworkAppId` avec l’ID d’application hello Hello application Proxy identité expérience Framework que vous avez créé précédemment.
4. Enregistrez votre fichier d’extensions.

## <a name="upload-hello-policies-tooyour-tenant"></a>Télécharger le client de tooyour stratégies hello

1. Bonjour [portail Azure](https://portal.azure.com), basculez dans hello [contexte de votre locataire Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md)et ouvrez hello **Azure AD B2C** panneau.
2. Sélectionnez **Infrastructure d’expérience d’identité**.
3. Sélectionnez **Charger la stratégie**.

    >[!WARNING]
    >fichiers de stratégie personnalisée Hello doivent être téléchargés dans hello suivant l’ordre :

1. Chargez TrustFrameworkBase.xml.
2. Chargez TrustFrameworkExtensions.xml.
3. Chargez SignUpOrSignin.xml.
4. Chargez vos autres fichiers de stratégie.

Lorsqu’un fichier est téléchargé, nom hello hello du fichier de stratégie est précédé de `B2C_1A_`.

## <a name="test-hello-custom-policy-by-using-run-now"></a>Tester une stratégie personnalisée de hello à l’aide d’exécuter maintenant

1. Ouvrez **paramètres d’Azure AD B2C** et accédez trop**infrastructure d’identité expérience**.

   >[!NOTE]
   >**Exécutez maintenant** requiert au moins une application toobe préinscrites sur le client de hello. Applications doivent être inscrit dans le locataire hello B2C, à l’aide de hello **Applications** sélection du menu dans Azure AD B2C ou à l’aide de hello identité expérience Framework tooinvoke stratégies intégrées et personnalisées. Seule une inscription par application est nécessaire.<br><br>
   toolearn tooregister applications, voir hello Azure AD B2C [prise en main](active-directory-b2c-get-started.md) article ou hello [inscription d’Application](active-directory-b2c-app-registration.md) l’article.  

2. Ouvrez B2C_1A_signup_signin, hello stratégie personnalisée partie de confiance (RP) de tiers que vous avez téléchargé. Sélectionnez **Exécuter maintenant**.

3. Vous devez être en mesure de toosign à l’aide d’une adresse de messagerie.

4. Connectez-vous avec hello même compte tooconfirm que vous avez hello configuration correcte.

>[!NOTE]
>Souvent, la mauvaise configuration de l’application IdentityExperienceFramework est à l’origine des échecs de connexion.


## <a name="next-steps"></a>Étapes suivantes

### <a name="add-facebook-as-an-identity-provider"></a>Ajouter Facebook en tant que fournisseur d’identité
tooset de Facebook :
1. [Configurez une application Facebook dans developers.facebook.com](active-directory-b2c-setup-fb-app.md).
2. [Ajout d’un locataire de secret principal tooyour Azure AD B2C application hello Facebook](#add-signing-and-encryption-keys-to-your-b2c-tenant-for-use-by-custom-policies).
3. Dans le fichier de stratégie TrustFrameworkExtensions hello, remplacez la valeur hello `client_id` avec l’ID d’application Facebook hello :

   ```xml
   <TechnicalProfile Id="Facebook-OAUTH">
     <Metadata>
     <!--Replace hello value of client_id in this technical profile with hello Facebook app ID"-->
       <Item Key="client_id">00000000000000</Item>
   ```
4. Téléchargez le client tooyour fichier hello TrustFrameworkExtensions.xml stratégie.
5. Test à l’aide de **exécuter maintenant** ou en appelant la stratégie hello directement à partir de votre application enregistrée.

### <a name="add-azure-active-directory-as-an-identity-provider"></a>Ajouter Azure Active Directory en tant que fournisseur d’identité
fichier de base Hello déjà utilisé dans ce guide de mise en route contient hello contenu dont vous avez besoin pour l’ajout d’autres fournisseurs d’identité. Pour plus d’informations sur la configuration des connexions, consultez hello [Azure Active Directory B2C : se connecter à l’aide de comptes Azure AD](active-directory-b2c-setup-aad-custom.md) l’article.

Pour une vue d’ensemble des scénarios personnalisés dans Azure AD B2C utiliser hello infrastructure d’identité expérience, consultez hello [Azure Active Directory B2C : stratégies personnalisées](active-directory-b2c-overview-custom.md) l’article. 
