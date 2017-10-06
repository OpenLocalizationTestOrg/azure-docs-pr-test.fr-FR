---
title: aaaAzure multilingue recherche | Documents Microsoft
description: Azure Search prend en charge 56 langages, tirant parti des analyseurs de langue de la technologie Lucene et Natural Language Processing de Microsoft.
services: search
documentationcenter: 
author: yahnoosh
manager: pablocas
editor: 
ms.assetid: 55a00b44-804d-41bb-9c96-e6ea498616f5
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/23/2017
ms.author: jlembicz
ms.openlocfilehash: 9a2e567a82ee563521c12ea320f6c484a8e73f04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-index-for-documents-in-multiple-languages-in-azure-search"></a>Création d’un index de documents dans plusieurs langues dans Azure Search
> [!div class="op_single_selector"]
>
> * [Portail](search-language-support.md)
> * [REST](https://msdn.microsoft.com/library/azure/dn879793.aspx)
> * [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.search.models.analyzername.aspx)
>
>

Unleashing power hello des analyseurs de langage est aussi simple que la propriété d’un paramètre sur un champ de recherche dans la définition de l’index hello. Maintenant, vous pouvez effectuer cette étape dans le portail de hello.

Vous trouverez ci-dessous des captures d’écran de hello panneaux du portail Azure pour Azure Search qui permettent aux utilisateurs toodefine un schéma d’index. À partir de ce panneau, les utilisateurs peuvent créer tous les champs de hello et définir la propriété d’analyseur hello pour chacun d’eux.

> [!IMPORTANT]
> Vous pouvez uniquement définir un analyseur de langue lors de la définition de champ, comme dans lors de la création d’un nouvel index à partir de hello d’arrière-plan, ou lors de l’ajout d’un index existant de nouveau champ tooan. Assurez-vous que vous spécifiez entièrement tous les attributs, y compris l’Analyseur de hello, lors de la création du champ de hello. Vous ne seront pas être en mesure de tooedit les attributs hello ou modifier le type d’analyseur hello une fois que vous enregistrez vos modifications.
>
>

## <a name="define-a-new-field-definition"></a>Définir une nouvelle définition de champ
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com) et panneau de service hello ouverte de votre service de recherche.
2. Cliquez sur **ajouter un index** dans la commande hello barre haut hello toostart de tableau de bord de service hello un nouvel index, ou ouvrez un tooset index existants sur les nouveaux champs que vous ajoutez un analyseur de tooan l’index existant.
3. Panneau de champs Hello s’affiche, vous propose des options pour la définition de schéma hello d’index de hello, y compris hello analyseur onglet utilisé pour le choix d’un analyseur de langage.
4. Dans les champs, démarrez une définition de champ en fournissant un nom, en choisissant le type de données hello et en définissant consultables, récupérables dans les résultats de recherche, utilisables dans des structures de navigation de facette, champ de hello toomark attributs sous forme de texte complète pouvant être trié et ainsi de suite.
5. Avant de le déplacer sur le champ suivant de toohello, ouvrez hello **analyseur** onglet.

![][1]
*tooselect un analyseur, cliquez sur l’onglet d’Analyseur de hello dans Panneau de champs hello*

## <a name="choose-an-analyzer"></a>Choisir un analyseur
1. Faites défiler le champ de hello toofind que vous définissez.
2. Si vous n’avez pas marqué comme champ hello en tant que recherche, cliquez sur hello case à cocher maintenant toomark en tant que **Searchable**.
3. Cliquez sur hello analyseur zone toodisplay hello liste des analyseurs de disponibles.
4. Choisissez l’Analyseur de hello souhaité toouse.

![][2]
*Sélectionnez un des analyseurs hello pris en charge pour chaque champ.*

Par défaut, tous les champs interrogeables utilisent hello [Lucene Standard analyseur](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) qui est indépendant du langage. liste complète de hello tooview de prise en charge des analyseurs, consultez [prise en charge linguistique dans Azure Search](https://msdn.microsoft.com/library/azure/dn879793.aspx).

Une fois que l’Analyseur de langue hello est sélectionnée pour un champ, il sera utilisé avec chaque demande de recherche et d’indexation pour ce champ. Lorsqu’une requête est émise par rapport à plusieurs champs à l’aide de différents analyseurs, hello requête ne sera traitée indépendamment par des analyseurs de droite hello pour chaque champ.

Plusieurs applications web et mobiles servent utilisateurs monde hello, à l’aide de différentes langues. Il est possible de toodefine un index pour un scénario à ceci en créant un champ pour chaque langue prise en charge.

![][3]
*Définition d'index avec un champ de description pour chaque langue prise en charge*

Si la langue hello d’agent hello émission d’une requête est connu, une demande de recherche peut être étendue tooa champ spécifique à l’aide de hello **searchFields** paramètre de requête. Hello requête suivante va être émise uniquement par rapport à la description de hello en polonais :

`https://[service name].search.windows.net/indexes/[index name]/docs?search=darmowy&searchFields=description_pl&api-version=2016-09-01`

Vous pouvez interroger votre index à partir du portail de hello, à l’aide de **rechercher dans l’Explorateur** toopaste dans un toohello similaire requête celle qui précède. Rechercher dans l’Explorateur est disponible à partir de la barre de commandes hello dans le panneau de service hello. Consultez [interroger votre index Azure Search dans le portail de hello](search-explorer.md) pour plus d’informations.

Parfois hello langue de l’agent hello en émettant une requête ne connaît pas, dans quels cas hello les requête peut être exécutée simultanément sur tous les champs. Si nécessaire, la préférence de résultats dans une langue donnée peut être définie à l'aide des [profils de score](https://msdn.microsoft.com/library/azure/dn798928.aspx). Dans l’exemple hello ci-dessous, correspondances trouvées dans la description de hello en anglais auront un score supérieur toomatches relatif dans polonais et Français :

    "scoringProfiles": [
      {
        "name": "englishFirst",
        "text": {
          "weights": { "description_en": 2 }
        }
      }
    ]

`https://[service name].search.windows.net/indexes/[index name]/docs?search=Microsoft&scoringProfile=englishFirst&api-version=2016-09-01`

Si vous êtes un développeur de .NET, notez que vous pouvez configurer les analyseurs de langage à l’aide de hello [Azure Search .NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Search). Hello dernière version inclut la prise en charge des analyseurs de langage Microsoft hello également.

<!-- Image References -->
[1]: ./media/search-language-support/AnalyzerTab.png
[2]: ./media/search-language-support/SelectAnalyzer.png
[3]: ./media/search-language-support/IndexDefinition.png
