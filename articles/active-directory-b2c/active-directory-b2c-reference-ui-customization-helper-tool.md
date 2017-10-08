---
title: "Azure Active Directory B2C : outil d’assistance de personnalisation d’interface de page | Microsoft Docs"
description: "Un outil d’assistance utilisé la fonctionnalité de personnalisation de l’interface utilisateur de toodemonstrate hello page dans Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: ae935d52-3520-4a94-b66e-b35bb40e7514
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: swkrish
ms.openlocfilehash: 5137ac112019369b4244a925df1acb96fefb758f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-a-helper-tool-used-toodemonstrate-hello-page-user-interface-ui-customization-feature"></a>Azure B2C Active Directory : Un outil d’assistance utilisé la fonctionnalité de personnalisation de l’interface (interface utilisateur) toodemonstrate hello page utilisateur
Cet article est un toohello d’accompagnement [article de personnalisation de l’interface utilisateur principale](active-directory-b2c-reference-ui-customization.md) dans Azure Active Directory (Azure AD) B2C. Hello étapes suivantes décrivent comment tooexercise hello la fonctionnalité de personnalisation de l’interface utilisateur de page à l’aide des exemples de code HTML et CSS contenu que nous vous avons fourni.

## <a name="get-an-azure-ad-b2c-tenant"></a>Obtention d’un client Azure AD B2C
Avant de pouvoir personnaliser quoi que ce soit, vous devez trop[obtenir un locataire Azure AD B2C](active-directory-b2c-get-started.md) si vous n’en avez pas encore.

## <a name="create-a-sign-up-or-sign-in-policy"></a>Création d’une stratégie d’inscription ou de connexion
Hello nous avons fourni des exemples de contenu peut être utilisé toocustomze deux des pages dans un [stratégie d’inscription ou connectez-vous](active-directory-b2c-reference-policies.md): hello [unifiée-page de connexion](active-directory-b2c-reference-ui-customization.md) et hello [attributs automatique déclarées page](active-directory-b2c-reference-ui-customization.md). Lors de la [création de votre stratégie d’inscription ou de connexion](active-directory-b2c-reference-policies.md#create-a-sign-up-or-sign-in-policy), ajoutez le compte local (adresse de messagerie), Facebook, Google et Microsoft en tant que **fournisseurs d’identité**. Ceux-ci sont hello uniquement IDPs acceptant à notre exemple de contenu HTML.  Vous pouvez également, si vous le souhaitez, ajouter un sous-ensemble de ces fournisseurs d’identité acceptés.

## <a name="register-an-application"></a>Inscrire une application
Vous devez trop[inscrire une application](active-directory-b2c-app-registration.md) dans votre B2C locataire qui peut être utilisé tooexecute votre stratégie. Après l’inscription de votre application, vous disposez de plusieurs options que vous pouvez utiliser tooactually exécuter votre stratégie d’inscription :

* Créer un Hello Azure AD B2C démarrage rapide applications répertoriées dans hello « Démarrer » de section de [signer configurer et connectent des consommateurs dans vos applications](active-directory-b2c-overview.md#get-started).
* Hello utilisez prégénérée [Azure AD B2C laboratoire](https://aadb2cplayground.azurewebsites.net) application. Si vous choisissez de laboratoire de hello toouse, vous devez inscrire une application dans votre client B2C à l’aide de hello **URI de redirection** `https://aadb2cplayground.azurewebsites.net/`.
* Hello d’utilisation **exécuter maintenant** bouton sur votre stratégie Bonjour [portail Azure](https://portal.azure.com/).

## <a name="customize-your-policy"></a>Personnalisation de votre stratégie
toocustomize hello et l’apparence de votre stratégie, vous devez toofirst créer des fichiers HTML et CSS à l’aide des conventions spécifiques de hello d’Azure Active Directory B2C. Vous pouvez ensuite charger votre emplacement disponible publiquement tooa contenu statique afin que Azure AD B2C puissent y accéder. Il peut s’agir de votre propre serveur web dédié, d’Azure Blob Storage, du réseau de distribution de contenu (CDN) Azure ou de n’importe quel autre fournisseur d’hébergement de ressources statiques. seules conditions requises de Hello sont que le contenu est disponible via le protocole HTTPS et est accessible à l’aide de CORS. Une fois que vous avez exposé votre contenu statique sur le web de hello, vous pouvez modifier votre stratégie toopoint toothis emplacement et votre contenu tooyour clients présents. Hello [article de personnalisation de l’interface utilisateur principale](active-directory-b2c-reference-ui-customization.md) décrit en détail le fonctionne de la fonctionnalité de personnalisation hello Azure Active Directory B2C.

Pour des raisons de hello de ce didacticiel, nous avons déjà créé des exemples de contenu et il hébergé sur le stockage d’objets Blob Azure. exemple de contenu Hello est une personnalisation de base dans le thème hello de notre société fictive, « Wingtip Toys ». tootry il dans votre propre stratégie, procédez comme suit :

1. Se connecter à locataire tooyour sur hello [portail Azure](https://portal.azure.com/) et accédez Panneau de fonctionnalités toohello B2C.
2. Cliquez sur **Stratégies d’inscription ou de connexion**, puis sur votre stratégie (par exemple, « b2c\_1\_sign\_up\_sign\_in »).
3. Cliquez sur **Personnalisation de l’interface utilisateur de la page**, puis sur **Page d’inscription ou de connexion unifiée**.
4. Hello de bascule **page personnalisée utiliser** basculer trop**Oui**. Bonjour **URI de la page personnalisée** , saisissez `https://wingtiptoysb2c.blob.core.windows.net/b2c/wingtip/unified.html`. Cliquez sur **OK**.
5. Cliquez sur **page d’inscription à un compte Local**. Hello de bascule **utiliser un modèle personnalisé** basculer trop**Oui**. Bonjour **URI de la page personnalisée** , saisissez `https://wingtiptoysb2c.blob.core.windows.net/b2c/wingtip/selfasserted.html`.
6. Répétition hello même étape de hello **page d’inscription sociaux compte**.
   Cliquez sur **OK** deux fois les panneaux de personnalisation du UI tooclose hello.
7. Cliquez sur **Enregistrer**.

Vous pouvez maintenant tester votre stratégie personnalisée. Vous pouvez utiliser votre propre laboratoire d’Azure AD B2C application ou hello si vous le souhaitez, mais vous pouvez également cliquer sur hello **exécuter maintenant** dans le panneau de la stratégie hello. Sélectionnez votre application dans la zone de liste déroulante hello et choisissez l’URI de redirection hello approprié. Cliquez sur hello **exécuter maintenant** bouton. Un nouvel onglet de navigateur s’ouvre et vous pouvez exécuter via une expérience utilisateur de hello de s’inscrire à votre application avec le nouveau contenu de hello en place !

## <a name="upload-hello-sample-content-tooazure-blob-storage"></a>Télécharger hello exemple tooAzure contenu stockage d’objets Blob
Si vous souhaitez que toohost de stockage d’objets Blob Azure toouse votre page de contenu, vous pouvez créer votre propre compte de stockage et utiliser notre tooupload d’outil d’assistance B2C vos fichiers.

### <a name="create-a-storage-account"></a>Créez un compte de stockage.
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).
2. Cliquez sur **+ Nouveau** > **Données et stockage** > **Compte de stockage**. Vous aurez besoin d’un abonnement Azure de toocreate un compte de stockage d’objets Blob Azure. Vous pouvez inscrire une évaluation gratuite de hello [site Web Azure](https://azure.microsoft.com/pricing/free-trial/).
3. Fournir un **nom** pour le compte de stockage hello (par exemple, « contoso ») et les choix hello les sélections appropriées pour **niveau tarifaire**, **groupe de ressources** et  **Abonnement**. Assurez-vous que vous avez hello **tooStartboard du code confidentiel** option est activée. Cliquez sur **Créer**.
4. Revenir en arrière toohello tableau d’accueil et cliquez sur le compte de stockage hello que vous venez de créer.
5. Bonjour **Résumé** , cliquez sur **conteneurs**, puis cliquez sur **+ ajouter**.
6. Fournir un **nom** pour le conteneur hello (par exemple, « b2c »), puis sélectionnez **Blob** comme hello **type d’accès**. Cliquez sur **OK**.
7. conteneur Hello que vous avez créé apparaît dans la liste hello sur hello **BLOB** panneau. Notez les URL hello du conteneur de hello ; par exemple, il doit ressembler trop`https://contoso.blob.core.windows.net/b2c`. Fermer hello **BLOB** panneau.
8. Dans le panneau de compte de stockage hello, cliquez sur **clés** et notez les valeurs hello Hello **nom de compte de stockage** et **clé d’accès primaire** champs.

> [!NOTE]
> **Clé d’accès primaire** est une information de sécurité importante.
> 
> 

### <a name="download-hello-helper-tool-and-sample-files"></a>Télécharger les fichiers d’exemple et outil d’assistance hello
Vous pouvez télécharger hello [stockage d’objets Blob Azure d’assistance outil et exemples les fichiers sous forme de fichier .zip](https://github.com/azureadquickstarts/b2c-azureblobstorage-client/archive/master.zip) ou cloner à partir de GitHub :

```
git clone https://github.com/azureadquickstarts/b2c-azureblobstorage-client
```

Ce référentiel contient un répertoire `sample_templates\wingtip` qui regroupe un exemple de contenu HTML et CSS, et des images. Pour ces modèles tooreference votre propre compte de stockage d’objets Blob Azure, vous devez les fichiers tooedit hello HTML. Ouvrez `unified.html` et `selfasserted.html` et remplacez toutes les instances de `https://localhost` avec l’URL de hello de votre propre conteneur que vous avez écrite dans les étapes précédentes hello. Vous devez utiliser le chemin d’accès absolu de hello Hello les fichiers HTML, car dans ce cas, hello HTML sera pris en charge par Azure AD, dans le domaine de hello `https://login.microsoftonline.com`.

### <a name="upload-hello-sample-files"></a>Télécharger les fichiers d’exemple hello
Dans la même référentiel de hello, décompressez `B2CAzureStorageClient.zip` et exécution hello `B2CAzureStorageClient.exe` au sein du fichier. Ce programme simplement pour télécharger tous les fichiers hello dans le répertoire hello que vous spécifiez le compte de stockage tooyour et activez l’accès CORS pour ces fichiers. Si vous avez suivi les étapes de hello ci-dessus, hello HTML et des fichiers CSS seront maintenant pointer vers le compte de stockage tooyour. Notez que hello nom de votre compte de stockage fait partie de hello qui précède `blob.core.windows.net`; par exemple, `contoso`. Vous pouvez vérifier que le contenu de hello a été téléchargé correctement en essayant de tooaccess `https://{storage-account-name}.blob.core.windows.net/{container-name}/wingtip/unified.html` sur un navigateur. Utilisez également [http://test-cors.org/](http://test-cors.org/) toomake assurer que le contenu hello est maintenant activés des CORS. (Recherchez « état XHR : 200 » dans le résultat de hello.)

### <a name="customize-your-policy-again"></a>Nouvelle personnalisation de votre stratégie
Maintenant que vous avez téléchargé hello exemple tooyour contenu propre stockage Azure, vous devez modifier votre stratégie d’inscription de tooreference il. Répétez les étapes hello hello [« Personnaliser votre stratégie »](#customize-your-policy) section ci-dessus, cette fois à l’aide des URL de votre propre compte stockage. Par exemple, hello emplacement de votre `unified.html` fichier serait `<url-of-your-container>/wingtip/unified.html`.

Vous pouvez désormais utiliser hello **exécuter maintenant** tooexecute de votre propre application ou de bouton à nouveau votre stratégie. Hello résultat doit rechercher quasiment hello même : vous avez utilisé hello même exemple de code HTML et CSS dans les deux cas. Toutefois, vos stratégies référencent maintenant votre propre instance de stockage d’objets Blob Azure et sont tooedit libre et de télécharger les fichiers hello à nouveau en tant que vous Veuillez. Pour plus d’informations sur la personnalisation de hello HTML et CSS, consultez toohello [article de personnalisation de l’interface utilisateur principale](active-directory-b2c-reference-ui-customization.md).

