---
title: "aaaDisplaying contenu Javadoc dans Eclipse pour hello Package de bibliothèques Azure pour Java"
description: "Comment toodisplay hello contenu Javadoc pour les bibliothèques de Azure hello dans Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 30f8b6a1-1d76-4d1c-861b-1db478c46e6b
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 8070023a24dc07eca8df906db5b8b662ceed6ccc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="displaying-javadoc-content-in-eclipse-for-hello-azure-libraries-package-for-java"></a>Affichage de contenu Javadoc dans Eclipse pour hello Package de bibliothèques Azure pour Java
Hello contenu Javadoc pour hello bibliothèques Azure pour Java peut être affiché dans votre environnement Eclipse en associant hello Javadoc toohello contenu bibliothèques Azure pour Java. Hello étapes suivantes vous montrent comment toouse cette fonctionnalité dans Eclipse.

Cette procédure suppose que vous avez déjà ajouté hello bibliothèque Azure pour le chemin d’accès de build Java tooyour.

## <a name="toodisplay-javadoc-content-in-eclipse-for-hello-azure-libraries-for-java"></a>toodisplay contenu Javadoc dans Eclipse pour hello bibliothèques Azure pour Java
* Dans l’Explorateur de projets d’Eclipse, Bonjour **bibliothèques référencées** section de votre projet, le menu contextuel Ouvrir hello hello bibliothèque Azure pour JAR. Par exemple, **microsoft-windowsazure-api-0.1.0.jar** (numéro de version hello peut-être être différentes, la version que vous avez installé).

* Cliquez sur **Propriétés**.

* Au sein de hello **propriétés** boîte de dialogue, dans le volet gauche de hello, cliquez sur **emplacement Javadoc**. Hello **emplacement Javadoc** boîte de dialogue s’affiche.

* Vous pouvez spécifier une **URL Javadoc** ou un **Javadoc dans archive**.

   * Si vous choisissez toospecify un **URL de Javadoc**, utilisez hello URL comme **http://dl.windowsazure.com/javadoc** ou **http://dl.windowsazure.com/storage/javadoc**.

   * Si vous choisissez toouse **Javadoc dans une archive**, vous pouvez spécifier un fichier externe ou un fichier de l’espace de travail.

   Faites votre choix et parcourez/validez en fonction des besoins. Hello exemple suivant associe hello les bibliothèques Azure pour Java hello JAR Javadoc correspondant a été téléchargé localement dossier tooa nommé **c:\MyAzureJARs**.

   ![][ic553487]

* *Étape facultative* : cliquez sur **Valider**. Problèmes potentiels avec hello JAR Javadoc pourraient apparaître ici.

* Cliquez sur **OK**.

Une fois associé à la bibliothèque de hello, hello contenu Javadoc doit s’afficher dans votre IDE Eclipse. Par exemple, si `blob` est défini de type `CloudBlockBlob` dans votre code, hello Voici un exemple de contenu Javadoc qui apparaît lorsque vous tapez `blob.acquireLease` dans le code :

![][ic553488]

## <a name="see-also"></a>Voir aussi
[Kit de ressources Azure pour Eclipse][Azure Toolkit for Eclipse]

[Création d’une application Hello World pour Azure dans Eclipse][Creating a Hello World Application for Azure in Eclipse]

[Lors de l’installation hello boîte à outils Azure pour Eclipse][Installing hello Azure Toolkit for Eclipse] 

Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez hello [centre de développement Java Azure][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic553487]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553487.png
[ic553488]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553488.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh698319.aspx -->
