---
title: "aaaSet de glossaire métier de hello pour baliser les régi dans Azure Data Catalog | Documents Microsoft"
description: "Procédure-tooarticle glossaire métier hello mise en surbrillance dans Azure Data Catalog pour définir et utiliser un tootag de vocabulaire métier commun inscrit des ressources de données."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: b3d63dbe-1ae7-499f-bc46-42124e950cd6
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: c9adf663bd08ac3c0c7b5d3551e6af409fe69ebc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-business-glossary-for-governed-tagging"></a>Paramétrer glossaire métier de hello régie marquage
## <a name="introduction"></a>Introduction
Azure Data Catalog permet la découverte de la source de données, afin de pouvoir facilement découvrir et comprendre les sources de données hello devez tooperform analyse et de prendre des décisions. Ces fonctionnalités font impressionnants hello lorsque vous pouvez rechercher et comprendre hello plus large gamme de sources de données disponibles.

L’une des fonctionnalités de Data Catalog qui favorise une meilleure compréhension des données de ressources est le balisage. En utilisant le balisage, vous pouvez associer des mots clés à un élément multimédia ou une colonne, qui à son tour rend plus facile asset de hello toodiscover via la recherche. Marquage vous aide également à plus facilement comprendre le contexte de hello et l’intention de l’élément multimédia de hello.

Cependant, le balisage peut parfois engendrer des problèmes qui lui sont propres. Voici quelques exemples de problèmes potentiels liés au balisage :

* Hello l’utilisation de texte développé sur d’autres personnes et les abréviations sur certaines ressources. Cette incohérence entraîne une dégradation découverte hello d’actifs, même si l’intention de hello a été actifs de hello tootag avec hello même balise.
* Le sens peut varier, selon le contexte. Par exemple, une balise appelée *chiffre d’affaires* sur un client, jeu de données peut signifier chiffre d’affaires par le client, mais hello même balise sur un jeu de données de ventes trimestriel, cela peut signifier chiffre d’affaires trimestriel de société de hello.  

toohelp résoudre des problèmes similaires, le catalogue de données inclut un glossaire métier.

À l’aide de glossaire de hello catalogue de données métier, une organisation peut documenter les termes métier importants et leur définitions de toocreate un vocabulaire métier commun. Cette gouvernance permet une cohérence dans l’utilisation des données de l’entreprise hello. Après avoir défini un terme de glossaire métier de hello, il peut être affecté tooa ressource de données dans le catalogue de hello. Cette approche, *régie marquage*, est hello même approche balisage.

## <a name="glossary-availability-and-privileges"></a>Disponibilité du glossaire et privilèges
glossaire métier de Hello est uniquement disponible dans hello Édition Standard d’Azure Data Catalog. Hello données catalogue gratuit n’inclut pas un glossaire et il ne fournit pas de fonctionnalités pour baliser les régi.

Vous pouvez accéder à glossaire métier de hello via hello **glossaire** option dans le menu de navigation du portail hello catalogue de données.  

![L’accès à glossaire métier de hello](./media/data-catalog-how-to-business-glossary/01-portal-menu.png)

Les administrateurs de catalogue de données et les membres du glossaire hello rôle Administrateurs permettre créer, modifier et supprimer des termes du glossaire glossaire métier de hello. Tous les utilisateurs du catalogue de données peuvent afficher les définitions des termes hello et baliser des éléments avec des termes de glossaire.

![Ajout d’un nouveau terme de glossaire](./media/data-catalog-how-to-business-glossary/02-new-term.png)

## <a name="creating-glossary-terms"></a>Création de termes de glossaire
Administrateurs de catalogue de données et glossaire peut créer des termes de glossaire en cliquant sur hello **nouveau terme** bouton. Chaque terme de glossaire contient hello champs qui suivent :

* Une définition d’entreprise pour le terme de hello
* Une description qui capture hello prévu ou professionnelles des règles pour les ressources hello ou une colonne
* Une liste des parties prenantes qui connaissent hello plus sur le terme de hello
* terme parent Hello, qui définit la hiérarchie hello dans le hello terme est organisé

## <a name="glossary-term-hierarchies"></a>Hiérarchies de termes de glossaire
À l’aide de glossaire métier de catalogue de données hello, une organisation peut décrire son vocabulaire métier en tant que hiérarchie de termes du contrat, et il peut créer une classification de termes qui représente mieux sa classification de l’entreprise.

Un terme doit être unique à un niveau donné de la hiérarchie. Les noms en double ne sont pas autorisés. Il n’existe aucun toohello limiter le nombre de niveaux dans une hiérarchie, mais une hiérarchie est souvent plus faciles à comprendre quand il existe trois niveaux ou moins.

utilisation de Hello des hiérarchies de glossaire métier de hello est facultative. Laisser hello terme le champ parent vide pour les termes du glossaire crée une liste de plats (non hiérarchiques) des termes de glossaire de hello.  

## <a name="tagging-assets-with-glossary-terms"></a>Balisage de ressources avec des termes de glossaire
Une fois les termes du glossaire ont été définies dans le catalogue de hello, expérience hello marquage actifs est glossaire de hello toosearch optimisé comme un utilisateur tape une balise. portail de catalogue de données Hello affiche une liste de correspondance toochoose de termes de glossaire de. Si l’utilisateur de hello sélectionne un terme de glossaire à partir de la liste de hello, terme de hello est ajouté toohello actif en tant que balise (également appelée une balise glossaire). Hello utilisateur peut également choisir toocreate une nouvelle balise en tapant un terme qui n’est pas hello glossaire (également appelé une balise de l’utilisateur).

![Ressource de données balisée avec une balise utilisateur et deux balises de glossaire](./media/data-catalog-how-to-business-glossary/03-tagged-asset.png)

> [!NOTE]
> Balises de l’utilisateur sont hello uniquement le type de balise pris en charge dans hello données catalogue gratuit.
>
>

### <a name="hover-behavior-on-tags"></a>Comportement du pointage sur les balises
Dans le portail du catalogue de données hello, hello deux types de balises sont les comportements visuellement distinctes et présentes pointage différents. Lorsque vous pointez sur une balise de l’utilisateur, vous pouvez voir le texte de balise hello et hello ou les utilisateurs qui ont ajouté hello. Lorsque vous pointez sur une balise de glossaire, vous consultez également hello définition du terme de glossaire hello et une lien tooopen hello entreprise glossaire tooview hello complète définition du terme de hello.

### <a name="search-filters-for-tags"></a>Filtres de recherche pour les balises
Les balises de glossaire comme les balises utilisateur peuvent non seulement faire l’objet de recherches, mais elles peuvent aussi servir de filtres dans une recherche.

## <a name="summary"></a>Résumé
À l’aide de glossaire métier de hello dans Azure Data Catalog et hello régie marquage il active, vous pouvez identifier, gérer et découvrir des ressources de données de façon cohérente. glossaire métier de Hello pouvez promouvoir l’apprentissage de vocabulaire d’entreprise hello par les membres de l’organisation. glossaire de Hello prend également en charge la capture des métadonnées explicites, pour simplifier la compréhension et la découverte de l’élément multimédia.

## <a name="next-steps"></a>Étapes suivantes
* [Documentation de l’API REST pour les opérations de glossaire métier](https://msdn.microsoft.com/library/mt708855.aspx)
