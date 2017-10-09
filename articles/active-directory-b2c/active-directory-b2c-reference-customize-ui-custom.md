---
title: "Azure B2C Active Directory : Référence : personnaliser l’interface utilisateur d’un parcours de l’utilisateur avec les stratégies personnalisées de hello | Documents Microsoft"
description: "Une rubrique sur les stratégies personnalisées Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/25/2017
ms.author: joroja
ms.openlocfilehash: 11f2a7575b95a186399d83266850fe44d650371b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-hello-ui-of-a-user-journey-with-custom-policies"></a>Personnaliser l’interface utilisateur d’un parcours de l’utilisateur avec les stratégies personnalisées de hello

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

> [!NOTE]
> Cet article est une description avancée du fonctionne de la personnalisation de l’interface utilisateur, et comment tooenable avec les stratégies B2C personnalisé, à l’aide de hello infrastructure expérience d’identité


Une expérience utilisateur transparente est essentielle à toute solution B2C. Par expérience utilisateur transparente, nous entendons une expérience, que ce soit sur l’appareil ou navigateur, qui ne distinguent pas voyage d’un utilisateur via notre service à partir de la clientèle hello qu’ils utilisent.

## <a name="understand-hello-cors-way-for-ui-customization"></a>Comprendre la manière CORS hello pour la personnalisation de l’interface utilisateur

Azure AD B2C permet de vous toocustomize hello-et-l’apparence de l’expérience utilisateur (UX) sur hello différentes pages qui peuvent être potentiellement pris en charge et affichées par Azure AD B2C via vos stratégies personnalisées.

À cette fin, Azure AD B2C exécute le code dans le navigateur de votre client et utilise hello approche moderne et standard [de partage de ressources Cross-Origin (CORS)](http://www.w3.org/TR/cors/) contenu personnalisé de tooload à partir d’une URL spécifique que vous spécifiez dans une stratégie personnalisée modèles de toopoint tooyour HTML5/CSS. CORS est un mécanisme qui permet des ressources limitées, telles que les polices, sur un toobe de la page web demandée à partir d’un autre domaine en dehors du domaine hello d'où proviennent les ressources hello.

Par rapport toohello ancienne méthode traditionnelle de, où les pages de modèle sont détenus par solution hello où vous avez fourni le texte limitée et des images, où un contrôle limité de la disposition et la convivialité a été proposé toomore principaux à des difficultés tooachieve une expérience transparente, hello CORS méthode prend en charge de HTML5 et CSS et vous permettent de :

- Héberger le contenu de hello et solution hello injecte ses contrôles à l’aide d’un script côté client.
- Avoir un contrôle total sur chaque pixel de la disposition et de l’apparence.

Vous pouvez fournir autant de pages de contenu que vous le souhaitez en créant les fichiers HTML5/CSS nécessaires à chaque page.

> [!NOTE]
> Pour des raisons de sécurité, hello utilisation de JavaScript est actuellement bloquée pour la personnalisation. toounblock JavaScript, l’utilisation d’un nom de domaine personnalisé pour votre client Azure AD B2C est nécessaire.

Dans chacun de vos modèles HTML5/CSS, vous fournissez un *ancre* élément, qui correspond toohello requis `<div id=”api”>` élément hello page HTML ou hello contenue comme illustrent ci-après. Azure AD B2C nécessite que toutes les pages de contenu aient cet élément div spécifique.

```
<!DOCTYPE html>
<html>
  <head>
    <title>Your page content’s tile!</title>
  </head>
  <body>
    <div id="api"></div>
  </body>
</html>
```

Du contenu relatif à Active Directory B2C Azure pour la page de hello est injectée dans cet élément div, tandis que hello de page de hello appartient toocontrol. du code JavaScript Hello du B2C Azure AD extrait dans votre contenu et injecte notre HTML dans cet élément div spécifique. Azure AD B2C injecte hello les contrôles comme il convient : contrôle de sélecteur, des contrôles de connexion, des contrôles de (actuellement téléphonique) de multi-Factor et des contrôles de collection attribut de compte. Azure AD B2C garantit que tous les contrôles de hello sont HTML5 conformes et accessible, tous les contrôles hello peuvent être entièrement un style et qu’une contrôle version ne sera pas reculer.

Hello fusionné est finalement afficher le contenu en tant que consommateur de tooyour hello document dynamique.

tooensure Hello ci-dessus fonctionne comme prévu, vous devez :

- Vérifier que votre contenu est accessible et conforme à HTML5
- Vérifier que CORS est activé sur votre serveur de contenu
- Traiter du contenu via HTTPS
- Utiliser des URL absolues comme https://yourdomain/content pour tous les liens et le contenu CSS

> [!TIP]
> tooverify qui hello vous hébergez votre contenu sur des sites a activé des CORS et tester des demandes CORS, vous pouvez utiliser hello site http://test-cors.org/. Site de toothis Merci, vous pouvez simplement envoyer hello CORS demande tooa serveur distant (tootest CORS est prise en charge), ou serveur de test tooa hello CORS demande d’envoi (tooexplore certaines fonctionnalités de CORS).

> [!TIP]
> Hello site http://enable-cors.org/ constitue également une plus de ressources utiles sur CORS.

Grâce toothis approche basée sur les règles CORS, les utilisateurs finaux de hello aura une expérience cohérente entre votre application et les pages hello pris en charge par Azure AD B2C.

## <a name="create-a-storage-account"></a>Créez un compte de stockage.

Comme condition préalable, vous devez toocreate un compte de stockage. Vous aurez besoin d’un abonnement Azure de toocreate un compte de stockage d’objets Blob Azure. Vous pouvez inscrire une évaluation gratuite de hello [site Web Azure](https://azure.microsoft.com/en-us/pricing/free-trial/).

1. Ouvrez une session de navigation et naviguez toohello [portail Azure](https://portal.azure.com).
2. Connectez-vous avec vos informations d’identification d’administration.
3. Cliquez sur **Nouveau** > **Données et stockage** > **Compte de stockage**.  Un panneau **Créer un compte de stockage** s’affiche.
4. Dans **nom**, fournissez un nom pour le compte de stockage hello, par exemple, *contoso369b2c*. Cette valeur sera ultérieurement désignée comme trop*storageAccountName*.
5. Choisissez les sélections appropriées de hello pour hello niveau tarifaire, groupe de ressources hello et abonnement de hello. Assurez-vous que vous avez hello **tooStartboard du code confidentiel** option est activée. Cliquez sur **Créer**.
6. Revenir en arrière toohello tableau d’accueil et cliquez sur le compte de stockage hello que vous venez de créer.
7. Bonjour **Services** , cliquez sur **BLOB**. Un **panneau Service BLOB** s’affiche.
8. Cliquez sur **+ conteneur**.
9. Dans **nom**, fournissez un nom pour le conteneur de hello, par exemple, *b2c*. Cette valeur sera ultérieurement référencé tooas *containerName*.
9. Sélectionnez **Blob** comme hello **type d’accès**. Cliquez sur **Créer**.
10. conteneur Hello que vous avez créé apparaît dans la liste hello sur hello **Panneau de service Blob**.
11. Fermer hello **BLOB** panneau.
12. Sur hello **Panneau de compte de stockage**, cliquez sur hello **clé** icône. Un **panneau Clés d’accès** s’affiche.  
13. Notez la valeur hello **key1**. Cette valeur sera ultérieurement appelée *key1*.

## <a name="downloading-hello-helper-tool"></a>Télécharger l’outil d’assistance de hello

1.  Télécharger l’outil d’assistance hello [GitHub](https://github.com/azureadquickstarts/b2c-azureblobstorage-client/archive/master.zip).
2.  Enregistrer hello *B2C-AzureBlobStorage-Client-master.zip* fichier sur votre ordinateur local.
3.  Extraire le contenu du fichier hello B2C-AzureBlobStorage-Client-master.zip sur votre disque local, par exemple sous hello hello **Pack de personnalisation de l’interface** dossier. Cela va créer un dossier *B2C-AzureBlobStorage-Client-master* en dessous.
4.  Ouvrez ce dossier et extraire le contenu du fichier d’archive hello hello *B2CAzureStorageClient.zip* qu’il contient.

## <a name="upload-hello-ui-customization-pack-sample-files"></a>Télécharger les exemples de fichiers de Pack de personnalisation de l’interface hello

1.  À l’aide de l’Explorateur Windows, accédez à toohello dossier *B2C-AzureBlobStorage-Client-master* situé sous hello *Pack de personnalisation de l’interface* dossier créé dans la section précédente de hello.
2.  Exécutez hello *B2CAzureStorageClient.exe* fichier. Ce programme simplement pour télécharger tous les fichiers hello dans le répertoire hello que vous spécifiez le compte de stockage tooyour et activez l’accès CORS pour ces fichiers.
3.  Lorsque vous y êtes invité, spécifiez : a.  nom de votre compte de stockage de Hello *storageAccountName*, par exemple *contoso369b2c*.
    b.  clé d’accès primaire Hello de votre stockage d’objets blob azure, *key1*, par exemple *contoso369b2c*.
    c.  nom de votre conteneur de stockage blob de stockage, de Hello *Nom_conteneur*, par exemple *b2c*.
    d.  chemin d’accès de Hello Hello *Pack de démarrage* les exemples de fichiers, par exemple *... \B2CTemplates\wingtiptoys*.

Si vous avez suivi les étapes de hello ci-dessus, hello fichiers HTML5 et CSS de hello *Pack de personnalisation de l’interface* pour une société fictive de hello **wingtiptoys** seront maintenant pointer vers le compte de stockage tooyour.  Vous pouvez vérifier que le contenu de hello a été téléchargé correctement en ouvrant le panneau de conteneur associés hello Bonjour portail Azure. Vous pouvez également vérifier que le contenu de hello a été téléchargé correctement en accédant à la page de hello à partir d’un navigateur. Pour plus d’informations, consultez [Azure Active Directory B2C : un outil d’assistance utilisé la fonctionnalité de personnalisation de l’interface (interface utilisateur) toodemonstrate hello page utilisateur](active-directory-b2c-reference-ui-customization-helper-tool.md).

## <a name="ensure-hello-storage-account-has-cors-enabled"></a>Vérifiez le compte de stockage hello a activé des CORS

CORS (partage des ressources Cross-Origin) doit être activé sur votre point de terminaison pour les tooload Premium d’Azure AD B2C votre contenu. Il s’agit, car votre contenu est hébergé sur un autre domaine que le domaine hello Premium d’Azure AD B2C prendra en charge page hello à partir de.

tooverify stockage hello vous hébergez votre contenu sur a CORS activé, poursuivre hello comme suit :

1. Ouvrez une session de navigation et naviguez toohello page *unified.html* à l’aide d’une URL complète de son emplacement dans votre compte de stockage hello `https://<storageAccountName>.blob.core.windows.net/<containerName>/unified.html`. Par exemple, https://contoso369b2c.blob.core.windows.net/b2c/unified.html.
2. Accédez à toohttp://test-cors.org. Ce site permet de tooverify qui hello page que vous utilisez a activé des CORS.  
<!--
![test-cors.org](../../media/active-directory-b2c-customize-ui-of-a-user-journey/test-cors.png)
-->

3. Dans **URL distante**, entrez une URL complète hello pour votre contenu unified.html, puis cliquez sur **envoyer la demande**.
4. Vérifier ce résultat hello Bonjour **résultats** section contient *état XHR : 200*. Cela indique que CORS est activé.
<!--
![CORS enabled](../../media/active-directory-b2c-customize-ui-of-a-user-journey/cors-enabled.png)
-->
compte de stockage Hello doit maintenant contenir un conteneur d’objets blob nommé *b2c* dans notre illustration contienne hello suivant wingtiptoys modèles hello *Starter-Pack*.

<!--
![Correctly configured storage account](../../articles/active-directory-b2c/media/active-directory-b2c-reference-customize-ui-custom/storage-account-final.png)
-->

Hello tableau suivant décrit objectif hello Hello au-dessus de pages de HTML5.

| Modèle HTML5 | Description |
|----------------|-------------|
| *phonefactor.html* | Cette page peut être utilisée comme modèle pour une page d’authentification multi-facteur. |
| *resetpassword.html* | Cette page peut être utilisée comme modèle pour une page de mot de passe oublié. |
| *selfasserted.html* | Cette page peut être utilisée comme modèle pour une page d’inscription à un compte de réseau social, une page d’inscription à un compte local ou une page de connexion à un compte local. |
| *unified.html* | Cette page peut être utilisée comme modèle pour une page de connexion ou d’inscription unifiée. |
| *updateprofile.html* | Cette page peut être utilisée comme modèle pour une page de mise à jour de profil. |

## <a name="add-a-link-tooyour-html5css-templates-tooyour-user-journey"></a>Ajouter un parcours de lien tooyour HTML5/CSS modèles tooyour utilisateur

Vous pouvez ajouter un parcours de lien tooyour HTML5/CSS modèles tooyour utilisateur en modifiant une stratégie personnalisée directement.

Hello toouse modèles HTML5/CSS personnalisé dans votre parcours de l’utilisateur ont toobe spécifié dans une liste de définitions de contenu qui peut être utilisé dans les déplacements de l’utilisateur. À cette fin, facultatif  *<ContentDefinitions>*  élément XML doit être déclaré sous hello  *<BuildingBlocks>*  section de votre fichier XML de stratégie personnalisée.

Hello tableau suivant décrit ensemble hello d’ID de définition du contenu reconnus par le moteur d’expérience hello Azure AD B2C identité et de type hello des pages qui se rapporte toothem.

| ID de définition de contenu | Description |
|-----------------------|-------------|
| *api.error* | **Page d’erreur**. Cette page s’affiche lorsqu’une exception ou une erreur est rencontrée. |
| *api.idpselections* | **Page de sélection du fournisseur d’identité**. Cette page contient une liste d’identité fournisseurs qui hello utilisateur peuvent choisir de pendant la connexion. Il s’agit de fournisseurs d’identité d’entreprise, d’identité de réseaux sociaux tels que Facebook et Google + ou de comptes locaux (basés sur une adresse de messagerie ou un nom d’utilisateur). |
| *api.idpselections.signup* | **Sélection du fournisseur d’identité pour l’inscription**. Cette page contient une liste de fournisseurs qui hello utilisateur peuvent choisir de pendant l’inscription des identités. Il s’agit de fournisseurs d’identité d’entreprise, d’identité de réseaux sociaux tels que Facebook et Google + ou de comptes locaux (basés sur une adresse de messagerie ou un nom d’utilisateur). |
| *api.localaccountpasswordreset* | **Page de mot de passe oublié**. Cette page contient un formulaire utilisateur hello a tooinitiate toofill leur mot de passe réinitialisé.  |
| *api.localaccountsignin* | **Page de connexion à un compte local**. Cette page contient un formulaire de connexion que l’utilisateur hello a toofill lorsque vous vous connectez avec un compte local qui est basé sur une adresse de messagerie ou un nom d’utilisateur. formulaire de Hello peut contenir une zone de texte et une zone d’entrée de mot de passe. |
| *api.localaccountsignup* | **Page d’inscription à un compte local**. Cette page contient un formulaire d’inscription utilisateur hello a toofill lors de l’inscription d’un compte local qui est basé sur une adresse de messagerie ou un nom d’utilisateur. formulaire de Hello peut contenir différents contrôles d’entrée tels que la zone de texte, zone de saisie de mot de passe, case d’option, zones de liste déroulante de sélection unique et sélections plusieurs cases à cocher. |
| *api.phonefactor* | **Page d’authentification multi-facteur**. Cette page permet aux utilisateurs de vérifier leurs numéros de téléphone (par voie textuelle ou vocale) au cours de l’inscription ou de la connexion. |
| *api.selfasserted* | **Page d’inscription à un compte de réseau social**. Cette page contient un formulaire d’inscription utilisateur hello a toofill de s’inscrire à l’aide d’un existant lorsque le compte à partir d’un fournisseur d’identité sociaux tels que Facebook ou Google +. Cette page est similaire toohello au-dessus de page d’inscription compte social à l’exception de hello des champs d’entrée de mot de passe hello. |
| *api.selfasserted.profileupdate* | **Page de mise à jour de profil**. Cette page contient un formulaire utilisateur hello peut utiliser tooupdate son profil. Cette page est similaire toohello au-dessus de page d’inscription compte social à l’exception de hello des champs d’entrée de mot de passe hello. |
| *api.signuporsignin* | **Page de connexion ou d’inscription unifiée**.  Cette page gère l’inscription et la connexion des utilisateurs, qui peuvent utiliser les fournisseurs d’identité d’entreprise, de réseaux sociaux, tels que Facebook ou Google+, ou de comptes locaux.

## <a name="next-steps"></a>Étapes suivantes
[Référence : Comprendre les stratégies personnalisées fonctionnent avec hello infrastructure d’identité expérience dans B2C](active-directory-b2c-reference-custom-policies-understanding-contents.md)
