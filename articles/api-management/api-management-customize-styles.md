---
title: "styles d’aaaCustomize dans le portail des développeurs dans Gestion des API Azure hello | Documents Microsoft"
description: "Découvrez comment les styles de hello toomodify utilisé pour n’importe quelle page dans le portail des développeurs dans Gestion des API Azure hello."
services: api-management
documentationcenter: 
author: antonba
manager: vlvinogr
editor: 
ms.assetid: 186128fe-41c0-4efb-9efe-2478ad4d103f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/09/2017
ms.author: antonba
ms.openlocfilehash: aaaa86527992ba43e64eab5fd35c7f57b573c812
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-hello-styling-of-hello-developer-portal-in-azure-api-management"></a>Personnaliser le style de hello du portail des développeurs hello dans Gestion des API Azure
Il existe trois méthodes fondamentales toocustomize hello portail destiné aux développeurs dans Gestion des API Azure :

* [Modifier le contenu de hello de pages statiques et des éléments de mise en page][modify-content-layout]
* [Mettre à jour les styles de hello utilisés pour les éléments de la page sur le portail des développeurs hello] [ customize-styles] (présentés dans ce guide)
* [Modifier les modèles hello utilisés pour les pages générées par le portail de hello] [ portal-templates] (par exemple, documents de l’API, produits, l’authentification des utilisateurs, etc.)

## <a name="change-headers-styling"></a>Modifier le style du hello d’éléments de la page

Hello couleurs, polices, tailles, espacements et autres éléments associées au style de n’importe quelle page sur le portail hello sont définis par les règles de style. 

Modification des règles de style hello est effectuée à partir de hello **portail des développeurs** tout en étant connecté en tant qu’administrateur. tooget il tout d’abord ouvrir hello portail Azure et cliquez sur **portail de publication** à partir de la barre d’outils du service hello de votre instance de la gestion des API.

![Portail des éditeurs][api-management-management-console]

Cliquez ensuite sur **portail des développeurs** sur hello en haut à droite. 

![Lien vers le portail de développement sur le portail de publication hello][api-management-pp-dp-link]

barre d’outils de personnalisation tooopen hello déplacez votre souris sur l’icône de personnalisation hello, ou sélectionnez-le, puis cliquez sur « styles » à partir de la barre d’outils hello.

![Bouton de la barre d’outils de personnalisation][api-management-customization-toolbar-button]

Il existe deux moyen principal de la modification des règles de style : vous pouvez parcourir liste hello de toutes les règles de style hello partout qui s’affiche par défaut et modifier un style en fonction des besoins, ou vous pouvez choisir **sélectionner un élément sur la page de hello** , puis Cliquez n’importe où sur hello page toosee seuls hello styles de cet élément.

![Customization toolbar][api-management-customization-toolbar]

Cliquez sur hello **sélectionner un élément sur la page de hello** option pour cet exemple.  Éléments deviennent maintenant en surbrillance lorsque vous pointez dessus avec hello souris toosignify styles d’élément que vous devez commencer la modification si vous avez cliqué sur. Hello de déplacer la souris sur le texte hello dans en-tête hello (en général, vous avez hello entreprise nom ici), puis cliquez sur elle. Un ensemble de règles de style nommées et par catégorie s’affiche dans l’éditeur de style hello. Chaque règle représente une propriété de style de l’élément sélectionné de hello. Par exemple, pour le texte d’en-tête hello sélectionné ci-dessus, la taille de hello du texte hello est dans @font-size-h1 alors que le nom de police hello avec des solutions alternatives de hello est @headings-font-family.

> Si vous êtes familiarisé avec [amorçage][bootstrap], ces règles sont en fait [variables LESS] [ LESS variables] dans le thème d’amorçage hello utilisé par hello portail des développeurs.
> 
> 

Modifions la couleur hello du texte de titre hello. Sélectionnez l’entrée de hello Bonjour  **@headings-color**  champ et le type **#000000**. Il s’agit de code hexadécimal hello noir hello. Comme vous le faites, vous voyez qu’un indicateur de carré de couleur s’affiche à fin hello de zone de texte hello. Si vous cliquez sur cet indicateur, un sélecteur de couleurs vous permet de vous toochoose une couleur.

![Color picker][api-management-customization-toolbar-color-picker]

Modifications sont visualisées en temps réel à mesure que vous les apportez, mais sont visibles tooadministrators uniquement. toomake ces modifications tooeveryone visible, cliquez sur hello **publier** bouton dans l’éditeur de style hello et confirmer les modifications hello.

![Publish menu][api-management-customization-toolbar-publish-form]

> toochange hello règles de style qui s’appliquent tooany autre élément sur la page de hello, suivez hello même procédure en tant que vous l’avez fait pour l’en-tête de hello. Cliquez sur **sélectionner un élément sur la page de hello** éditeur de style hello, élément select hello vous intéressez et démarrer modifiant les valeurs hello hello des règles de style affichés sur l’écran hello.
> 
> 


## <a name="next-steps"></a>Étapes suivantes
* Découvrez comment le contenu toocustomize hello du portail des développeurs de pages à l’aide de [modèles portails des développeurs](api-management-developer-portal-templates.md).

[Change hello styling of hello headers]: #change-headers-styling
[Next steps]: #next-steps

[Azure Classic Portal]: https://manage.windowsazure.com/

[api-management-management-console]: ./media/api-management-customize-styles/api-management-management-console.png
[api-management-pp-dp-link]: ./media/api-management-customize-styles/api-management-pp-dp-link.png
[api-management-customization-toolbar-button]: ./media/api-management-customize-styles/api-management-customization-toolbar-button.png
[api-management-customization-toolbar]: ./media/api-management-customize-styles/api-management-customization-toolbar.png
[api-management-customization-toolbar-color-picker]: ./media/api-management-customize-styles/api-management-customization-toolbar-color-picker.png
[api-management-customization-toolbar-publish-form]: ./media/api-management-customize-styles/api-management-customization-toolbar-publish-form.png

[modify-content-layout]: api-management-modify-content-layout.md
[customize-styles]: api-management-customize-styles.md
[portal-templates]: api-management-developer-portal-templates.md

[bootstrap]: http://getbootstrap.com/
[LESS variables]: http://getbootstrap.com/css/
