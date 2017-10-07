---
title: build aaaCommand en ligne pour Azure | Documents Microsoft
description: "Génération en ligne de commande pour Azure"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 94b35d0d-0d35-48b6-b48b-3641377867fd
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/05/2017
ms.author: kraigb
ms.openlocfilehash: 295b61ba162dd4373ee3f56cc1462decb3e16762
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="building-azure-projects-from-hello-command-line"></a>Génération de projets Azure à partir de la ligne de commande hello
À l’aide de hello Microsoft Build Engine (MSBuild), vous pouvez générer des produits dans des environnements de laboratoire de génération où Visual Studio n’est pas installé. MSBuild utilise pour les fichiers projet un format XML extensible et entièrement pris en charge par Microsoft. À l’aide du format de fichier hello MSBuild, vous pouvez décrire les éléments doivent être générées pour un ou plusieurs plateformes et configurations.

Vous pouvez également exécuter MSBuild à la ligne de commande hello et cette rubrique décrit cette approche. En définissant des propriétés sur la ligne de commande hello, vous pouvez créer des configurations spécifiques d’un projet. De même, vous pouvez également définir des cibles de hello MSBuild génère. Pour plus d’informations sur les paramètres de ligne de commande et MSBuild, consultez la page [Référence de la ligne de commande MSBuild](https://msdn.microsoft.com/library/ms164311.aspx).

## <a name="msbuild-parameters"></a>Paramètres MSBuild
toocreate de façon la plus simple Hello un package est toorun MSBuild avec hello `/t:Publish` option. Par défaut, cette commande crée un répertoire dans la relation toohello racine dossier hello projet, tel que `<ProjectDirectory>\bin\Configuration\app.publish\`. Lorsque vous générez un projet Windows Azure, deux fichiers sont générés : hello du fichier de package lui-même et le fichier de configuration associé hello :

* Fichier de package (`project.cspkg`)
* Fichier de configuration (`ServiceConfiguration.TargetProfile.cscfg`)

Par défaut, tous les projets Azure comprennent un fichier de configuration de service pour les versions locales (débogage) et un autre pour les versions cloud (gestion intermédiaire ou production). Mais vous pouvez ajouter ou supprimer des fichiers de configuration de service selon vos besoins. Lorsque vous créez un package dans Visual Studio, vous êtes invité le tooinclude du fichier de configuration de service en même temps que le package de hello. Lorsque vous générez un package à l’aide de MSBuild, le fichier de configuration du service local hello est inclus par défaut. fichier tooinclude une configuration de service différents, jeu hello `TargetProfile` propriété Hello commande MSBuild (`MSBuild /t:Publish /p:TargetProfile=ProfileName`).

Si vous souhaitez toouse un autre répertoire pour hello stocké des fichiers de configuration et de package, définir le chemin à l’aide de hello hello `/p:PublishDir=Directory\` option, y compris hello séparateur de barre oblique inverse de fin.

## <a name="next-steps"></a>Étapes suivantes
Une fois le package de hello est créé, vous pouvez le déployer tooAzure. Pour obtenir un didacticiel qui montre comment tooautomate ce processus, consultez [livraison continue pour les Services de Cloud dans Azure](./cloud-services/cloud-services-dotnet-continuous-delivery.md).

