---
title: aaaHow tooupgrade projets toohello version actuelle de hello Windows Azure tools | Documents Microsoft
description: "Découvrez comment tooupgrade Azure projet dans la version actuelle de Visual Studio toohello Hello Windows Azure tools"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1d64070a-078d-468a-87f4-e6715de6475f
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: c89ba43af0f2fd9db46ce0c90f0da3d70dc1510b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupgrade-projects-toohello-current-version-of-hello-azure-tools-for-visual-studio"></a>Comment tooupgrade projets toohello la version actuelle de hello Windows Azure Tools pour Visual Studio
## <a name="overview"></a>Vue d'ensemble
Après avoir installé la version actuelle de hello de hello Azure Tools (ou une version précédente est plus récente que la version 1.6), tous les projets qui ont été créés à l’aide d’un Azure Tools version 1.6 (novembre 2011) sera mis à niveau automatiquement dès que vous les ouvrez. Si vous avez créé des projets à l’aide de hello 1.6 (novembre 2011) de mise en production de ces outils et vous avez toujours cette version installée, vous pouvez ouvrir ces projets dans une version antérieure de hello et décider ultérieurement si tooupgrade les.

## <a name="how-your-project-changes-when-you-upgrade-it"></a>Changements provoqués par la mise à niveau de votre projet
Si un projet est installée automatiquement ou si vous spécifiez que vous souhaitez tooupgrade qu'il, votre projet est modifié toowork avec les versions actuelles de certains assemblys, et certaines propriétés sont également modifiées comme décrit dans cette section. Si votre projet nécessite d’autres modifications de toobe compatible avec la version plus récente de hello des outils de hello, vous devez effectuer ces modifications manuellement.

* fichier web.config de Hello pour les rôles web et le fichier app.config de hello pour les rôles de travail sont mis à jour tooreference hello nouvelle version de Microsoft.WindowsAzure.Diagnostics.DiagnosticMonitoirTraceListener.dll.
* les assemblys Microsoft.WindowsAzure.StorageClient.dll, Microsoft.WindowsAzure.Diagnostics.dll et Microsoft.WindowsAzure.ServiceRuntime.dll Hello sont mis à niveau toohello nouvelles versions.
* Les profils de publication qui ont été stockées dans le fichier de projet Azure hello (.ccproj) sont déplacés tooa fichier distinct, avec l’extension .azurePubXml hello, Bonjour **publier** sous-répertoire.
* Certaines propriétés Bonjour le profil de publication est mis à jour toosupport les fonctionnalités nouvelles et modifiées. **AllowUpgrade** est remplacé par **DeploymentReplacementMethod**, car vous pouvez mettre à jour un service cloud déployé de manière simultanée ou incrémentielle.
* Hello propriété **UseIISExpressByDefault** est ajouté et que toofalse hello serveur web qui est utilisé pour le débogage ne changer pas automatiquement à partir d’Internet Information Services (IIS) tooIIS Express. IIS Express est serveur de web hello par défaut pour les projets qui sont créés avec des versions plus récentes de hello des outils de hello.
* Si la mise en cache Azure est hébergé dans un ou plusieurs des rôles de votre projet, certaines propriétés dans la configuration du service hello (fichier .cscfg) et la définition de service (fichier .csdef) sont modifiées lorsqu’un projet est mis à niveau. Si le projet de hello utilise le package de NuGet de mise en cache Azure hello, projet de hello est version la plus récente du package de hello toohello mis à niveau. Vous devez ouvrir le fichier web.config de hello et vérifier la que la configuration client hello a été correctement conservée pendant le processus de mise à niveau hello. Si vous avez ajouté hello référence tooAzure mise en cache client les assemblys sans utiliser le package NuGet de hello, ces assemblys ne sont pas mis à jour ; Vous devez mettre à jour manuellement ces versions de nouvelles références toohello.

> [!IMPORTANT]
> Pour les projets F #, vous devez manuellement mettre à jour tooAzure référence les assemblys afin qu’ils référencent des versions plus récentes de hello de ces assemblys.
> 
> 

### <a name="how-tooupgrade-an-azure-project-toohello-current-release"></a>Comment tooupgrade Azure project toohello la mise en production actuelle
1. Installation hello version actuelle de hello Azure Tools dans l’installation de Visual Studio hello que vous souhaitez toouse pour hello mis à niveau le projet et le projet puis ouvrez hello que vous souhaitez tooupgrade. Si le projet de hello a été créé avec un Azure Tools version 1.6 (novembre 2011), projet de hello est la version actuelle de toohello automatiquement mis à niveau. Si le projet de hello a été créé avec hello version de novembre 2011 et que la version est toujours installée, projet de hello s’ouvre dans cette version.
2. Dans l’Explorateur de solutions, ouvrez hello raccourci menu hello nœud de projet, choisissez **propriétés**, puis choisissez hello **Application** hello boîte de dialogue qui s’affiche.
   
    Hello **Application** onglet affiche la version des outils hello qui a associé à un projet de hello. Si la version actuelle de hello de Azure Tools s’affiche, projet de hello a déjà été mis à niveau. Si vous avez installé une version plus récente des outils de hello à onglet hello montre, une **mise à niveau** bouton s’affiche.
3. Choisissez hello **mise à niveau** bouton tooupgrade une version des outils de hello du projet toohello actuel.
4. Générez le projet de hello, puis résolvez les erreurs qui résultent de modifications de l’API. Pour plus d’informations sur comment toomodify votre code pour la nouvelle version de hello, consultez la documentation de hello pour hello API spécifique.

