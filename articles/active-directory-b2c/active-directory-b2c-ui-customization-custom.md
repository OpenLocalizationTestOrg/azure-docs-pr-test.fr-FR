---
title: "Personnalisation d’une interface utilisateur avec des stratégies personnalisées - Azure AD B2C | Microsoft Docs"
description: "Apprenez comment personnaliser une interface utilisateur (UI) dans Azure AD B2C à l’aide de stratégies personnalisées."
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 658c597e-3787-465e-b377-26aebc94e46d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/04/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: 6f00995e54c9f9ef27cc51e38f3de07cd5817cc1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-configure-ui-customization-in-a-custom-policy"></a>Azure Active Directory B2C : Configurer la personnalisation de l’interface utilisateur dans une stratégie personnalisée

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Après avoir suivi cet article, vous disposerez d’une stratégie personnalisée d’inscription et de connexion avec votre marque et votre apparence. Avec Azure Active Directory B2C (B2C Active Directory de Azure), vous obtenez presque plein contrôle du contenu HTML et CSS de hello qui a présenté toousers. Lorsque vous utilisez une stratégie personnalisée, vous configurez personnalisation de l’interface utilisateur de XML au lieu d’utiliser des contrôles Bonjour portail Azure. 

## <a name="prerequisites"></a>Composants requis

Avant de commencer, effectuez les étapes de la section [Bien démarrer avec les stratégies personnalisées](active-directory-b2c-get-started-custom.md). Vous devez disposer d’une stratégie personnalisée fonctionnelle pour l’inscription et la connexion avec des comptes locaux.

## <a name="page-ui-customization"></a>Personnalisation de l’interface utilisateur de la page

En utilisant la fonctionnalité de personnalisation de l’interface utilisateur de page hello, vous pouvez personnaliser hello apparence et la convivialité d’une stratégie personnalisée. Vous pouvez également conserver la cohérence visuelle et de la marque entre votre application et Azure AD B2C.

Voici comment cela fonctionne : Azure AD B2C exécute le code dans le navigateur client et utilise une approche moderne appelée [partage des ressources cross-origin (CORS)](http://www.w3.org/TR/cors/). Tout d’abord, vous spécifiez une URL dans la stratégie personnalisée de hello avec du contenu HTML personnalisé. Azure AD B2C fusionne avec hello du contenu HTML qui est chargé à partir de l’URL, puis affiche hello page toohello des éléments d’interface utilisateur.

## <a name="create-your-html5-content"></a>Créer votre contenu HTML5

Créer un fichier HTML avec un nom de marque de votre produit dans le titre de hello.

1. Copiez hello suivant extrait de code HTML. Il est bien formé HTML5 avec un élément vide appelée  *\<div id = « api »\>\</div\>*  qui se trouve dans hello  *\<corps\>*  balises. Cet élément indique où le contenu de Azure AD B2C est toobe inséré.

   ```html
   <!DOCTYPE html>
   <html>
   <head>
       <title>My Product Brand Name</title>
   </head>
   <body>
       <div id="api"></div>
   </body>
   </html>
   ```

   >[!NOTE]
   >Pour des raisons de sécurité, hello utilisation de JavaScript est actuellement bloquée pour la personnalisation.

2. Coller l’extrait de code hello copié dans un éditeur de texte, puis enregistrez le fichier hello en tant que *ui.html personnaliser*.

## <a name="create-an-azure-blob-storage-account"></a>Créer un compte de stockage d’objets blob Azure

>[!NOTE]
> Dans cet article, nous utilisons notre contenu toohost de stockage d’objets Blob Azure. Vous pouvez choisir toohost votre contenu sur un serveur web, mais vous devez [activer CORS sur votre serveur web](https://enable-cors.org/server.html).

toohost ce contenu HTML dans le stockage Blob, hello suivant :

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Sur hello **Hub** menu, sélectionnez **nouveau** > **stockage** > **compte de stockage**.
3. Entrez un **nom** unique pour votre compte de stockage.
4. Le champ **Modèle de déploiement** peut conserver la valeur **Gestionnaire de ressources**.
5. Modification **type de compte** trop**stockage d’objets Blob**.
6. Le champ **Performances** peut conserver la valeur **Standard**.
7. Le champ **Réplication** peut conserver la valeur **RA-GRS**.
8. Le champ **Niveau d’accès** peut conserver la valeur **À chaud**.
9. Le champ **Chiffrement du service de stockage** peut conserver la valeur **Désactivé**.
10. Sélectionnez un **abonnement** pour votre compte de stockage.
11. Créez un **Groupe de ressources** ou sélectionnez-en un.
12. Sélectionnez hello **emplacement géographique** pour votre compte de stockage.
13. Cliquez sur **créer** compte de stockage toocreate hello.  
    Une fois le déploiement de hello est terminé, hello **compte de stockage** panneau s’ouvre automatiquement.

## <a name="create-a-container"></a>Créez un conteneur.

toocreate un conteneur public dans le stockage Blob, hello suivant :

1. Cliquez sur hello **vue d’ensemble** onglet.
2. Cliquez sur **Conteneur**.
3. Dans le champ **Nom**, saisissez **$root**.
4. Définissez **type d’accès** trop**Blob**.
5. Cliquez sur **$root** tooopen conteneur hello.
6. Cliquez sur **Télécharger**.
7. Cliquez sur icône du dossier hello suivant trop**sélectionner un fichier**.
8. Accédez trop**ui.html personnaliser**, que vous avez créés précédemment dans hello [personnalisation de la Page UI](#the-page-ui-customization-feature) section.
9. Cliquez sur **Télécharger**.
10. Sélectionnez blob ui.html personnaliser hello que vous avez téléchargé.
11. Suivant trop**URL**, cliquez sur **copie**.
12. Dans un navigateur, collez les URL hello copié et accédez toohello site. Si le site de hello n’est pas accessible, vérifiez que type d’accès de conteneur de hello est défini trop**blob**.

## <a name="configure-cors"></a>Configuration de CORS

Configurer le stockage d’objets Blob pour le partage des ressources Cross-Origin de manière hello suivante :

>[!NOTE]
>Vous souhaitez tootry fonctionnalité de personnalisation de l’interface utilisateur hello à l’aide de notre exemple de code HTML et CSS contenu ? Nous vous avons fourni [un outil d’assistance simple](active-directory-b2c-reference-ui-customization-helper-tool.md) qui charge et configure notre exemple de contenu sur votre compte de stockage Blob. Si vous utilisez hello outil, passez directement trop[modifier votre stratégie personnalisée s’inscrire ou connectez-vous](#modify-your-sign-up-or-sign-in-custom-policy).

1. Sur hello **stockage** panneau, sous **paramètres**, ouvrez **CORS**.
2. Cliquez sur **Add**.
3. Pour **Origines autorisées**, saisissez un astérisque (\*).
4. Bonjour **verbes autorisés** liste déroulante, sélectionnez **obtenir** et **OPTIONS**.
5. Pour **En-têtes autorisés**, saisissez un astérisque (\*).
6. Pour **En-têtes exposés**, saisissez un astérisque (\*).
7. Dans le champ **Âge maximal (secondes)**, saisissez **200**.
8. Cliquez sur **Ajouter**.

## <a name="test-cors"></a>Tester CORS

Vérifiez que vous êtes prêt de manière hello suivante :

1. Accédez toohello [test-cors.org](http://test-cors.org/) site Web, puis coller les URL de hello Bonjour **URL distante** boîte.
2. Cliquez sur **Envoyer la demande**.  
    Si vous recevez une erreur, assurez-vous que vos [paramètres CORS](#configure-cors) sont corrects. Que vous deviez également tooclear cache de votre navigateur ou ouvrez une session de navigation en privé en appuyant sur Ctrl + Maj + P.

## <a name="modify-your-sign-up-or-sign-in-custom-policy"></a>Modifier votre stratégie personnalisée d’inscription ou de connexion

Sous le niveau supérieur de hello  *\<TrustFrameworkPolicy\>*  de balise, vous devez rechercher  *\<BuildingBlocks\>*  balise. Au sein de hello  *\<BuildingBlocks\>*  balises, ajoutez un  *\<ContentDefinitions\>*  balise en copiant hello l’exemple suivant. Remplacez *your_storage_account* avec nom hello de votre compte de stockage.

  ```xml
  <BuildingBlocks>
    <ContentDefinitions>
      <ContentDefinition Id="api.idpselections">
        <LoadUri>https://{your_storage_account}.blob.core.windows.net/customize-ui.html</LoadUri>
      </ContentDefinition>
    </ContentDefinitions>
  </BuildingBlocks>
  ```

## <a name="upload-your-updated-custom-policy"></a>Téléchargement de votre stratégie personnalisée mise à jour

1. Bonjour [portail Azure](https://portal.azure.com), [basculer en contexte hello de votre locataire Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md), puis ouvrez hello **Azure AD B2C** panneau.
2. Cliquez sur **Toutes les stratégies**.
3. Cliquez sur **Charger la stratégie**.
4. Télécharger `SignUpOrSignin.xml` avec hello  *\<ContentDefinitions\>*  balise que vous avez ajouté précédemment.

## <a name="test-hello-custom-policy-by-using-run-now"></a>Tester une stratégie personnalisée de hello à l’aide de **exécuter maintenant**

1. Sur hello **Azure AD B2C** panneau, accédez trop**toutes les stratégies**.
2. Stratégie personnalisée hello que vous avez téléchargé, puis cliquez sur hello **exécuter maintenant** bouton.
3. Vous devez être en mesure de toosign à l’aide d’une adresse de messagerie.

## <a name="reference"></a>Référence

Vous trouverez ici des exemples de modèles pour la personnalisation de l’interface utilisateur :

```
git clone https://github.com/azureadquickstarts/b2c-azureblobstorage-client
```

dossier de sample_templates/wingtip Hello contient hello HTML fichiers suivants :

| Modèle HTML5 | Description |
|----------------|-------------|
| *phonefactor.html* | Utilisez ce fichier en tant que modèle pour une page d’authentification multifacteur. |
| *resetpassword.html* | Utilisez ce fichier en tant que modèle pour une page relative à un mot de passe oublié. |
| *selfasserted.html* | Utilisez ce fichier en tant que modèle pour une page d’inscription à un compte de réseau social, une page d’inscription à un compte local ou une page de connexion à un compte local. |
| *unified.html* | Utilisez ce fichier en tant que modèle pour une page de connexion ou d’inscription unifiée. |
| *updateprofile.html* | Utilisez ce fichier en tant que modèle pour une page de mise à jour de profil. |

Bonjour [modifier votre section de stratégie personnalisée de s’inscrire ou connectez-vous](#modify-your-sign-up-or-sign-in-custom-policy), vous avez configuré la définition du contenu hello pour `api.idpselections`. Hello complet de définition du contenu ID qui sont reconnus par l’infrastructure d’expérience hello Azure AD B2C identité et leurs descriptions sont dans hello tableau suivant :

| ID de définition du contenu | Description | 
|-----------------------|-------------|
| *api.error* | **Page d’erreur**. Cette page s’affiche lorsqu’une exception ou une erreur est rencontrée. |
| *api.idpselections* | **Page de sélection du fournisseur d’identité**. Cette page contient une liste d’identité fournisseurs qui hello utilisateur peuvent choisir de pendant la connexion. Il s’agit de fournisseurs d’identité d’entreprise, de fournisseurs d’identité de réseaux sociaux tels que Facebook et Google + ou de comptes locaux. |
| *api.idpselections.signup* | **Sélection du fournisseur d’identité pour l’inscription**. Cette page contient une liste de fournisseurs qui hello utilisateur peuvent choisir de pendant l’inscription des identités. Il s’agit de fournisseurs d’identité d’entreprise, de fournisseurs d’identité de réseaux sociaux tels que Facebook et Google + ou de comptes locaux. |
| *api.localaccountpasswordreset* | **Page de mot de passe oublié**. Cette page contient un formulaire utilisateur hello doit suivre tooinitiate un mot de passe réinitialisé.  |
| *api.localaccountsignin* | **Page de connexion à un compte local**. Cette page contient un formulaire de connexion que l’utilisateur doit renseigner lors de la connexion à un compte local basé sur une adresse e-mail ou un nom d’utilisateur. formulaire de Hello peut contenir une zone de texte et une zone d’entrée de mot de passe. |
| *api.localaccountsignup* | **Page d’inscription à un compte local**. Cette page contient un formulaire d’inscription que l’utilisateur doit renseigner lors de la connexion à un compte local basé sur une adresse e-mail ou un nom d’utilisateur. formulaire de Hello peut contenir divers contrôles d’entrée, comme une zone de texte, une zone de mot de passe, une case d’option, zones de liste déroulante de sélection unique et sélections plusieurs cases à cocher. |
| *api.phonefactor* | **Page d’authentification multi-facteur**. Cette page permet aux utilisateurs de vérifier leurs numéros de téléphone (par voie textuelle ou vocale) au cours de l’inscription ou de la connexion. |
| *api.selfasserted* | **Page d’inscription à un compte de réseau social**. Cette page contient un formulaire d’inscription que l’utilisateur doit remplir lors de l’inscription à l’aide d’un compte existant proposé par un fournisseur d’identité de réseaux sociaux tel que Facebook ou Google +. Cette page est similaire toohello précédant la page d’inscription du compte de réseaux sociaux, à l’exception des champs d’entrée de mot de passe hello. |
| *api.selfasserted.profileupdate* | **Page de mise à jour de profil**. Cette page contient un formulaire que les utilisateurs peuvent utiliser tooupdate son profil. Cette page est similaire toohello compte sociaux page d’inscription, à l’exception des champs d’entrée de mot de passe hello. |
| *api.signuporsignin* | **Page de connexion ou d’inscription unifiée**. Cette page gère les deux hello d’inscription et de connexion des utilisateurs, ce qui peuvent utiliser des fournisseurs d’identité entreprise, fournisseurs d’identité sociaux tels que Facebook ou Google + ou les comptes locaux.  |

## <a name="next-steps"></a>Étapes suivantes

Pour en savoir plus les éléments personnalisables de l’interface utilisateur, lisez le [guide de référence relatif à la personnalisation de l’interface utilisateur pour des stratégies intégrées](active-directory-b2c-reference-ui-customization.md).
