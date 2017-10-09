---
title: aaaAdding Azure Search tooBlob stockage | Documents Microsoft
description: "Créer un index dans le code à l’aide de hello API REST de Azure Search HTTP."
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
ms.service: search
ms.topic: article
ms.date: 05/04/2017
ms.author: ashmaka
ms.openlocfilehash: a3801790067bf169693b500e83799286b7387a77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="searching-blob-storage-with-azure-search"></a>Recherche dans le Stockage Blob avec la Recherche Azure

Recherche dans hello divers types de contenu stockées dans le stockage Blob Azure peut être un problème difficile de toosolve. Toutefois, vous pouvez indexer et rechercher hello du contenu de vos objets BLOB en seulement quelques clics à l’aide d’Azure Search. La recherche dans le Stockage Blob nécessite d’approvisionner un service Recherche Azure. Hello différentes limites de service et niveaux d’Azure Search tarifaires se trouvent sur hello [page de tarification](https://aka.ms/azspricing).

## <a name="what-is-azure-search"></a>Présentation d’Azure Search
[Azure Search](https://aka.ms/whatisazsearch) est une solution de recherche qui facilite la tâche de recherche en texte intégral robuste de développeurs tooadd rencontre tooweb et des applications mobiles. En tant que service, Azure Search supprime hello besoin toomanage n’importe quelle infrastructure recherche tout en offrant un [99,9 % du temps SLA](https://aka.ms/azuresearchsla).

Avec prise en charge avancée pour 56 langues, Recherche Azure peut analyser votre contenu et gérer intelligemment les constructions spécifiques à chaque langue. Azure Search fournit également une expérience utilisateur de recherche riches hello outils toobuild. Il est simple tooadd des fonctionnalités telles que la navigation par facettes et les suggestions de recherche de tampon clavier positionnement interfaces toouser de mise en surbrillance à l’aide d’Azure Search. toolearn sur les fonctionnalités de la recherche d’Azure, vous pouvez lire du service hello [documentation](https://aka.ms/azsearchdocs).

## <a name="crack-open-and-search-through-hello-content-of-enterprise-document-formats"></a>Peut-il ouvrir et parcourez le contenu de hello de formats de documents d’entreprise
Avec prise en charge pour [d’extraction de document](https://aka.ms/azsblobindexer) dans le stockage d’objets Blob Azure, Azure Search peut indexer le contenu de hello un grand nombre de types de fichiers stockés dans des objets BLOB :
- PDF
- Microsoft Office : DOCX/DOC, XLSX/XLS, PPTX/PPT, MSG (e-mails Outlook)
- HTML
- Fichiers de texte brut

Par extraction de texte et les métadonnées de ces types de fichiers, il est facile toosearch entre plusieurs formats de fichiers avec une seule requête toofind hello documents les plus pertinents, quelle que soit le type. À l’indexation hello les métadonnées de contenu et hello de documents Microsoft Office, PDF et des messages électroniques, il toobuild possibles d’une solution de gestion de contenu d’entreprise robuste à l’aide du stockage d’objets Blob et Azure Search.

## <a name="search-through-your-blob-metadata"></a>Effectuer des recherches dans vos métadonnées d’objets blob
Un scénario courant qui le rend facile toosort via des objets BLOB de n’importe quel type de contenu est tooindex hello blob personnalisée, définie par l’utilisateur métadonnées ainsi que de hello propriétés système pour chacun de vos objets BLOB. De cette façon, les informations pour chaque objet blob sont indexées, quelle que soit le type hello du document dans le blob hello afin de trier facilement et de facette dans l’ensemble de votre contenu du stockage Blob.

[En savoir que plus sur l’indexation des métadonnées d’objets blob.](https://aka.ms/azsblobmetadataindexing)

## <a name="image-search"></a>Recherche d’images
De Azure Search recherche en texte intégral, une navigation par facettes et des fonctionnalités de tri peuvent être appliqué toohello les métadonnées des images stockées dans des objets BLOB.

Si ces images sont traités au préalable à l’aide de hello [ordinateur Vision API](https://www.microsoft.com/cognitive-services/computer-vision-api) à partir des Services de Microsoft cognitifs, il est possible de tooindex hello visual contenu de chaque image, y compris la reconnaissance OCR et de l’écriture manuscrite. Nous travaillons sur l’ajout de OCR et autres fonctions de traitement de l’image directement tooAzure recherche, si vous êtes intéressé par ces fonctionnalités Veuillez soumettre une demande sur notre [UserVoice](https://aka.ms/azsuv) ou [envoyez-nous un e-mail](mailto:azscustquestions@microsoft.com).

## <a name="index-and-search-through-json-blobs"></a>Indexation et recherche à l’aide des objets blob JSON
Azure Search peut être configuré tooextract structuré contenus dans des objets BLOB qui contiennent JSON. Azure Search peut lire les objets BLOB JSON et analyser le contenu de hello structurée dans les champs appropriés de hello d’un document Azure Search. Azure Search peut également prendre des objets BLOB qui contient un tableau d’objets JSON et de mappent chaque élément tooa distinct Azure recherche dans le document.

Notez que l’analyse de JSON n’est pas actuellement configurable via le portail de hello. [En savoir plus sur l’analyse des objets JSON dans Recherche Azure.](https://aka.ms/azsjsonblobindexing)

## <a name="quick-start"></a>Démarrage rapide
Azure Search peut être ajouté tooblobs directement à partir de panneau portail du stockage Blob hello.

![](./media/search-blob-storage-integration/blob-blade.png)

En cliquant sur hello option « Ajouter Azure recherche » lance un flux dans lequel vous pouvez sélectionner un service Azure Search existant ou créer un nouveau service. Si vous créez un nouveau service, vous quitterez l’expérience portail de votre compte Stockage. Vous devez toore-accédez panneau portail du stockage toohello et resélectionnez option de « Ajouter Azure Search » hello, où vous pouvez sélectionner le service existant de hello.

### <a name="next-steps"></a>Étapes suivantes
En savoir plus sur hello indexeur d’objet Blob Azure Search Bonjour complète [documentation](https://aka.ms/azsblobindexer).
