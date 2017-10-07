---
title: aaaInstall Visual Studio et SSDT pour SQL Data Warehouse | Documents Microsoft
description: "Installer les outils de développement Visual Studio et SSDT pour Azure SQL Data Warehouse"
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 0ed9b406-9b42-4fe6-b963-fe0a5b48aac1
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 03/30/2017
ms.author: anvang;barbkess
ms.openlocfilehash: cf49c13d5cab598ed127f5702c04168b62ede0dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-visual-studio-and-ssdt-for-sql-data-warehouse"></a>Installer Visual Studio et SSDT pour SQL Data Warehouse
applications toodevelop pour SQL Data Warehouse, nous recommandons à l’aide de la version la plus récente de Visual Studio hello avec la version la plus récente de SQL Server Data Tools (SSDT) hello.  Visual Studio 2013 Update 5 avec SSDT est également pris en charge pour la compatibilité descendante.  

À l’aide de Visual Studio avec SSDT vous permettra de toouse hello Explorateur d’objets SQL Server toovisually Explorer les tables, vues, procédures stockées et beaucoup plus d’objets dans votre entrepôt de données SQL, ainsi que d’exécuter des requêtes.

> [!NOTE]
> SQL Data Warehouse ne prend pas actuellement en charge les projets de base de données Visual Studio.  Cette fonctionnalité sera ajoutée dans une version ultérieure.
> 
> 

## <a name="step-1-install-visual-studio"></a>Étape 1 : Installer Visual Studio
Suivez ces toodownload de liens et d’installer Visual Studio. Si vous disposez déjà de Visual Studio 2013 ou version ultérieure est installé, vous pouvez ignorer tooStep 2, installez SSDT.

1. [Téléchargez Visual Studio][].
2. Suivez hello [installation de Visual Studio] [ Installing Visual Studio] guide sur MSDN et choisir la configuration par défaut de hello.

## <a name="step-2-install-ssdt"></a>Étape 2 : Installer SSDT
tooinstall SSDT pour Visual Studio Cochez simplement une mise à jour SSDT à partir de Visual Studio en suivant ces étapes.

1. Dans Visual Studio, cliquez sur **Outils** / **Extensions et mises à jour...** / **Mises à jour**
2. Sélectionnez **Mises à jour du produit** puis recherchez **Mise à jour Microsoft SQL Server pour les outils de base de données**.

Si une mise à jour n’est trouvé, vous devez hello dernière version installée.  tooconfirm SSDT est installé, cliquez sur **aide** / **sur Microsoft Visual Studio** et recherchez SQL Server Data Tools dans la liste de hello.  version la plus récente de SSDT Hello est 14.0.60525.0.  Si hello option tooinstall n’est pas disponible à partir de Visual Studio, vous pouvez aussi visiter hello [de téléchargement SSDT] [ SSDT Download] page toodownload et installer SSDT manuellement.

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez la version la plus récente de SSDT hello, vous êtes prêt trop[connecter] [ connect] tooyour SQL Data Warehouse.

<!--Anchors-->

<!--Image references-->

<!--Articles-->
[connect]: ./sql-data-warehouse-query-visual-studio.md

<!--Other-->
[Téléchargez Visual Studio]: https://www.visualstudio.com/downloads/
[Installing Visual Studio]: https://msdn.microsoft.com/library/e2h7fzkw.aspx
[SSDT Download]: https://msdn.microsoft.com/library/mt204009.aspx
