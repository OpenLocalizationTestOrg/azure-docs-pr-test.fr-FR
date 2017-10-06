---
title: "Azure Active Directory B2C : utilisation de la personnalisation de la langue | Microsoft Docs"
description: 
services: active-directory-b2c
documentationcenter: 
author: sama
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/25/2017
ms.author: sama
ms.openlocfilehash: a8e4037014f5adf929dac7b5dc4db72ba0f5b292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-using-language-customization"></a>Azure Active Directory B2C : utilisation de la personnalisation de la langue

>[!NOTE] 
>Cette fonctionnalité est en version préliminaire publique.  Il est recommandé d’utiliser un client de test lors de l’utilisation de cette fonctionnalité.  Nous ne planifions pas sur les modifications avec rupture à partir de la version disponibilité générale toohello hello, mais nous nous réservons toomake de droite hello de ces fonctionnalités modifications tooimprove hello.  Une fois que vous avez eu une fonctionnalité de tootry chance, veuillez fournir vos commentaires sur votre expérience et comment nous pouvons améliorer.  Vous pouvez fournir des commentaires via le portail Azure de hello outil face hello émoticône haut hello à droite.   S’il existe une exigence métier requiert que vous toogo dynamique à l’aide de cette fonctionnalité au cours de la phase d’aperçu hello, nous dire à vos scénarios et nous pouvons vous fournir une assistance et des conseils appropriés de hello.  Vous pouvez nous contacter à l’adresse [aadb2cpreview@microsoft.com](mailto:aadb2cpreview@microsoft.com).

Personnalisation de langue vous permet de toochange toosuit de langue différente de tooa votre client a besoin de route de l’utilisateur.  Nous fournissons des traductions pour 36 langues (voir [Informations supplémentaires](#additional-information)).  Même si votre expérience est disponible que pour un seul langage, vous pouvez personnaliser n’importe quel texte sur hello pages toosuit vos besoins.  

## <a name="how-does-language-customization-work"></a>Fonctionnement de la personnalisation de la langue
Personnalisation de la langue permet tooselect quelles langues votre parcours de l’utilisateur est disponible dans.  Une fois que la fonctionnalité de hello est activée, vous pouvez fournir le paramètre de chaîne de requête hello, ui_locales, à partir de votre application.  Lorsque vous appelez dans Azure AD B2C, nous traduire vos paramètres régionaux toohello de page que vous avez indiqué.  À l’aide du type de configuration vous donne un contrôle complet sur les langues hello dans votre parcours de l’utilisateur et ignore les paramètres de langue de hello du navigateur du client hello. Vous pouvez également ne pas avoir besoin de ce niveau de contrôle sur les langues que votre client voit.  Si vous ne fournissez pas un paramètre ui_locales, hello expérience client est dictée par leurs paramètres de navigateur.  Vous pouvez toujours contrôler quels langues votre parcours de l’utilisateur est traduite tooby ajoutant comme un langage pris en charge.  Si le navigateur d’un client est set tooshow une langue vous ne souhaitez pas toosupport, puis langage hello sélectionnée comme valeur par défaut dans des cultures prises en charge est affiché à la place.

1. **paramètres régionaux de l’interface utilisateur spécifiés language** -une fois que vous activez la personnalisation de la langue, votre parcours de l’utilisateur est la langue traduite toohello spécifiée ici
2. **Navigateur demandé langage** -si aucune interface utilisateur-paramètres régionaux a été spécifié, il traduit toohello navigateur demandé de langage, **s’il a été inclus dans les langues prises en charge**
3. **Langue par défaut de stratégie** -si le navigateur de hello ne spécifie pas un langage ou si elle spécifie un qui n’est pas pris en charge, il se traduit par la langue par défaut de stratégie toohello

>[!NOTE]
>Si vous utilisez des attributs d’utilisateur personnalisé, vous devez tooprovide vos propres traductions. Consultez « [Personnaliser vos chaînes](#customize-your-strings) » pour plus d’informations.
>

## <a name="support-uilocales-requested-languages"></a>Prendre en charge les langues demandées par le paramètre ui_locales 
En activant la personnalisation de langue sur une stratégie, vous pouvez désormais contrôler langage hello de parcours d’utilisateur hello en ajoutant le paramètre d’ui_locales hello.
1. [Suivez ces Panneau de fonctionnalités étapes toonavigate toohello B2C hello portail Azure.](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-app-registration#navigate-to-b2c-settings)
2. Accédez à stratégie tooa que vous souhaitez tooenable pour les traductions.
3. Cliquez sur **Personnalisation de la langue**.
4. Lecture hello avertissement avec soin.  Une fois activée, la personnalisation de la langue ne peut pas être désactivée.
5. Activer la fonctionnalité de hello et cliquez sur **OK**.
6. Enregistrer votre stratégie sur hello angle supérieur gauche de votre **modifier la stratégie** panneau.

## <a name="select-which-languages-your-user-journey-supports"></a>Sélectionner les langues prises en charge par votre parcours utilisateur 
Créer une liste de langues autorisées pour votre toobe de voyage utilisateur traduite dans lorsque le paramètre d’ui_locales hello n’est pas fourni.
1. Vérifiez que la personnalisation de la langue est activée dans votre stratégie, comme vu précédemment.
2. Dans votre panneau **Modifier une stratégie**, sélectionnez **Personnalisation de la langue**.
3. Vous accédez tooyour **langues prises en charge** panneau.  D’ici, vous pouvez sélectionner **Ajouter une langue**.
4. Sélectionnez tous les langages hello que vous aimeriez toobe pris en charge.  

>[!NOTE]
>Si un paramètre ui_locales n’est pas fourni, puis hello page est langue du navigateur du client toohello traduit uniquement si elle figure dans cette liste
>

5. Cliquez sur **Ok** bas hello
6. Fermer hello **personnalisation de langage** panneau et **enregistrer** votre stratégie.

## <a name="customize-your-strings"></a>Personnaliser vos chaînes
« Personnalisation de langue » vous permet de toocustomize toute chaîne dans votre parcours de l’utilisateur.
1. Vérifiez votre stratégie « personnalisation de langage' activée à partir des instructions précédentes hello.
2. Dans votre panneau **Modifier une stratégie**, sélectionnez **Personnalisation de la langue**.
3. Dans le menu de navigation gauche hello, sélectionnez **télécharger le contenu**.
4. Sélectionnez la page hello tooedit.
5. Dans la liste déroulante de hello, sélectionnez la langue hello tooedit pour.
6. Cliquez sur **Télécharger**. 

Ces étapes vous fournissent un fichier JSON que vous pouvez utiliser toostart modifier vos chaînes.

### <a name="changing-any-string-on-hello-page"></a>La modification de n’importe quelle chaîne sur la page de hello
1. Ouvrez hello fichier JSON téléchargés à partir de les instructions fournies dans un éditeur JSON.
2. Rechercher hello élément toochange.  Vous pouvez trouver hello `StringId` de chaîne hello que vous recherchez, ou recherchez hello `Value` vous souhaitez toochange.
3. Hello de mise à jour `Value` attribut avec ce que vous souhaitez afficher.
4. Enregistrez le fichier de hello et télécharger vos modifications.

### <a name="changing-extension-attributes"></a>Modification des attributs d’extension
Si vous cherchez la chaîne hello de toochange pour un attribut utilisateur personnalisée, ou que vous souhaitez toohello d’un tooadd JSON, il est Bonjour suivant le format :
```JSON
{
  "LocalizedStrings": [
    {
      "ElementType": "ClaimType",
      "ElementId": "extension_<ExtensionAttribute>",
      "StringId": "DisplayName",
      "Override": false,
      "Value": "<ExtensionAttributeValue>"
    }
    [...]
}
```
>[!IMPORTANT]
>Si vous avez besoin d’une chaîne de toooverride, assurez-vous que tooset hello `Override` valeur trop`true`.  Si la valeur de hello n’est pas modifiée, l’entrée de hello est ignorée. 
>

Remplacez `<ExtensionAttribute>` par nom hello de votre attribut utilisateur personnalisée.  
Remplacez `<ExtensionAttributeValue>` avec hello nouvelle chaîne toobe est affiché.

### <a name="using-localizedcollections"></a>Utilisation de LocalizedCollections
Si vous souhaitez tooprovide une liste de l’ensemble de valeurs pour les réponses, vous devez toocreate une `LocalizedCollections`.  Un élément `LocalizedCollections` est un tableau de paires `Name` et `Value`.  Hello `Name` est ce qui est affiché et hello `Value` est ce qui est retourné dans la revendication de hello.  tooadd un `LocalizedCollections`, il a hello suivant le format :

```JSON
{
  "LocalizedStrings": [...],
  "LocalizedCollections": [{
      "ElementType":"ClaimType", 
      "ElementId":"<UserAttribute>",
      "TargetCollection":"Restriction",
      "Override": false,
      "Items":[
           {
                "Name":"<Response1>",
                "Value":"<Value1>"
           },
           {
                "Name":"<Response2>",
                "Value":"<Value2>"
           }
     ]
  }]
}
```
>[!IMPORTANT]
>Si vous avez besoin d’une chaîne de toooverride, assurez-vous que tooset hello `Override` valeur trop`true`.  Si la valeur de hello n’est pas modifiée, l’entrée de hello est ignorée. 
>

* `ElementId`est hello utilisateur attribut par ce `LocalizedCollections` constitue une réponse à
* `Name`hello valeur indiqué toohello utilisateur
* `Value`est ce qui est retourné dans la revendication de hello lorsque cette option est sélectionnée.

### <a name="upload-your-changes"></a>Charger vos modifications
1. Une fois que vous avez terminé le fichier JSON tooyour des modifications de hello, accédez tooyour arrière B2C locataire.
2. Dans votre panneau **Modifier une stratégie**, sélectionnez **Personnalisation de la langue**.
3. Dans le menu de navigation gauche hello, sélectionnez **télécharger du contenu**.
4. Sélectionnez hello page tooupload les modifications apportées à.
5. Si vous souhaitez tooupload une langue que vous avez fournis précédemment JSON pour, vous devez les entrées précédentes du toodelete hello.  Vous pouvez le supprimer en cliquant sur hello `...` hello à droite de ce langage et sélectionnez **supprimer**.
6. Cliquez sur **ajouter** sur le coin supérieur gauche de hello.
7. Sélectionnez la langue hello de votre fichier JSON.
8. Cliquez sur le bouton dossier hello hello droite et recherchez votre fichier JSON.
9. Cliquez sur hello **télécharger** bouton bas hello du Panneau de hello.
10. Revenir en arrière tooyour **modifier la stratégie** panneau, cliquez sur **enregistrer**.

## <a name="additional-information"></a>Informations supplémentaires
### <a name="recommendations-for-language-customization"></a>Recommandations pour la personnalisation de la langue
Il est recommandé uniquement dans les ressources de langue tooyour entrées pour les chaînes vous mettant explicitement que vous souhaitez tooreplace.  Nous appliquer un fichier de toohello de limite de taille est compilé en dehors de toutes les traductions de votre JSON.  Si vos fichiers obtenir trop volumineux, il affecte les performances de hello de votre parcours de l’utilisateur.
### <a name="page-ui-customization-labels-are-removed-once-language-customization-is-enabled"></a>Les étiquettes de personnalisation de l’interface utilisateur de la page sont supprimées une fois que la personnalisation de la langue est activée.
Lorsque vous activez la personnalisation de la langue, les modifications précédemment appliquées aux étiquettes via la personnalisation de l’interface utilisateur de la page sont supprimées, à l’exception des attributs utilisateur personnalisés.  Cette modification est effectuée de conflits tooavoid dans laquelle vous pouvez modifier vos chaînes.  Vous pouvez continuer toochange vos étiquettes et autres chaînes en téléchargeant des ressources linguistiques dans « Personnalisation de langage ».
### <a name="microsoft-is-committed-tooprovide-hello-most-up-to-date-translations-for-your-use"></a>Microsoft est validée tooprovide hello des traductions plus récentes pour votre utilisation
Nous ne cesserons d’améliorer nos traductions pour qu’elles soient conformes à vos attentes.  Nous allons identifier les bogues et les modifications dans la terminologie globale et permettre les mises à jour hello fonctionneront en toute transparence dans votre parcours de l’utilisateur.
### <a name="support-for-right-to-left-languages"></a>Prise en charge des langues s’écrivant de droite à gauche
Il n’y a aucune prise en charge des langues de droite à gauche. Si vous avez besoin de cette fonctionnalité, votez pour elle dans la page de [Commentaires Azure](https://feedback.azure.com/forums/169401-azure-active-directory/suggestions/19393000-provide-language-support-for-right-to-left-languag).
### <a name="social-identity-provider-translations"></a>Traductions des fournisseurs d’identité de réseaux sociaux
Nous fournissons des connexions de toosocial OIDC paramètre hello ui_locales, mais ils ne sont pas respectées par certains fournisseurs d’identité sociaux, notamment Facebook et Google. 
### <a name="browser-behavior"></a>Comportement du navigateur
Chrome et Firefox deux demander pour leur définition de la langue et s’il est un langage pris en charge, il s’affiche avant la valeur par défaut hello.  Bord actuellement ne demande pas un langage et devient la langue par défaut de toohello droites.
### <a name="known-issues"></a>Problèmes connus
* Téléchargement de ressources de langue pour la page de l’authentification Multifacteur hello dans une profil modifier une stratégie est actuellement indisponible.
* `LocalizedCollections`ne sont pas générés pour les valeurs lorsqu’il est requis par le type de réponse hello
### <a name="what-if-i-want-a-language-that-isnt-supported"></a>Que se passe-t-il si je veux une langue qui n’est pas prise en charge ?
Nous préparons tooprovide une extension de cette fonctionnalité qui vous permet de tooupload une ressource JSON vers 'langues personnalisées'.  fonctionnalité de Hello vous permet de nom de hello toospecify et pour n’importe quel langage de code de langue et fournir *tous les* hello traductions pour cette langue.  Si vous avez besoin de cette fonctionnalité, envoyez-nous votre scénario à l’adresse [aadb2cpreview@microsoft.com](mailto:aadb2cpreview@microsoft.com).  

### <a name="what-languages-are-supported"></a>Quelles sont les langues prises en charge ?

| language              | Code de langue |
|-----------------------|---------------|
| Bangla                | bn            |
| Tchèque                 | cs            |
| Danois                | da            |
| Allemand                | de            |
| Grec                 | el            |
| Français               | en            |
| Espagnol               | es            |
| Finnois               | fi            |
| Français                | fr            |
| Goudjrati              | gu            |
| Hindi                 | hi            |
| Croate              | hr            |
| Hongrois             | hu            |
| Italien               | it            |
| Japonais              | ja            |
| Kannada               | kn            |
| Coréen                | ko            |
| Malayalam             | ml            |
| Marathi               | mr            |
| Malais                 | ms            |
| Norvégien Bokmål      | nb            |
| Néerlandais                 | nl            |
| Pendjabi               | pa            |
| Polonais                | pl            |
| Portugais - Brésil   | pt-br         |
| Portugais - Portugal | pt-pt         |
| Roumain              | ro            |
| Russe               | ru            |
| Slovaque                | sk            |
| Suédois               | sv            |
| Tamoul                 | ta            |
| Télougou                | te            |
| Thaï                  | th            |
| Turc               | tr            |
| Chinois - simplifié  | zh-hans       |
| Chinois - traditionnel | zh-hant       |
