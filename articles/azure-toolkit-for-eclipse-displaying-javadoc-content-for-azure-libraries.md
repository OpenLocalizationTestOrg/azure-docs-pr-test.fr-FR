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
# <a name="displaying-javadoc-content-in-eclipse-for-hello-azure-libraries-package-for-java"></a><span data-ttu-id="54600-103">Affichage de contenu Javadoc dans Eclipse pour hello Package de bibliothèques Azure pour Java</span><span class="sxs-lookup"><span data-stu-id="54600-103">Displaying Javadoc Content in Eclipse for hello Azure Libraries Package for Java</span></span>
<span data-ttu-id="54600-104">Hello contenu Javadoc pour hello bibliothèques Azure pour Java peut être affiché dans votre environnement Eclipse en associant hello Javadoc toohello contenu bibliothèques Azure pour Java.</span><span class="sxs-lookup"><span data-stu-id="54600-104">hello Javadoc content for hello Azure Libraries for Java can be viewed within your Eclipse environment by associating hello Javadoc content toohello Azure Libraries for Java.</span></span> <span data-ttu-id="54600-105">Hello étapes suivantes vous montrent comment toouse cette fonctionnalité dans Eclipse.</span><span class="sxs-lookup"><span data-stu-id="54600-105">hello following steps show you how toouse this functionality within Eclipse.</span></span>

<span data-ttu-id="54600-106">Cette procédure suppose que vous avez déjà ajouté hello bibliothèque Azure pour le chemin d’accès de build Java tooyour.</span><span class="sxs-lookup"><span data-stu-id="54600-106">This procedure assumes you have already added hello Azure Library for Java tooyour build path.</span></span>

## <a name="toodisplay-javadoc-content-in-eclipse-for-hello-azure-libraries-for-java"></a><span data-ttu-id="54600-107">toodisplay contenu Javadoc dans Eclipse pour hello bibliothèques Azure pour Java</span><span class="sxs-lookup"><span data-stu-id="54600-107">toodisplay Javadoc content in Eclipse for hello Azure Libraries for Java</span></span>
* <span data-ttu-id="54600-108">Dans l’Explorateur de projets d’Eclipse, Bonjour **bibliothèques référencées** section de votre projet, le menu contextuel Ouvrir hello hello bibliothèque Azure pour JAR.</span><span class="sxs-lookup"><span data-stu-id="54600-108">Within Eclipse's Project Explorer, in hello **Referenced Libraries** section of your project, open hello context menu for hello Azure Library for Java JAR.</span></span> <span data-ttu-id="54600-109">Par exemple, **microsoft-windowsazure-api-0.1.0.jar** (numéro de version hello peut-être être différentes, la version que vous avez installé).</span><span class="sxs-lookup"><span data-stu-id="54600-109">For example, **microsoft-windowsazure-api-0.1.0.jar** (hello version number may be different, dependent upon which version you have installed).</span></span>

* <span data-ttu-id="54600-110">Cliquez sur **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="54600-110">Click **Properties**.</span></span>

* <span data-ttu-id="54600-111">Au sein de hello **propriétés** boîte de dialogue, dans le volet gauche de hello, cliquez sur **emplacement Javadoc**.</span><span class="sxs-lookup"><span data-stu-id="54600-111">Within hello **Properties** dialog, in hello left-hand pane, click **Javadoc Location**.</span></span> <span data-ttu-id="54600-112">Hello **emplacement Javadoc** boîte de dialogue s’affiche.</span><span class="sxs-lookup"><span data-stu-id="54600-112">hello **Javadoc Location** dialog is displayed.</span></span>

* <span data-ttu-id="54600-113">Vous pouvez spécifier une **URL Javadoc** ou un **Javadoc dans archive**.</span><span class="sxs-lookup"><span data-stu-id="54600-113">You can specify a **Javadoc URL**, or a **Javadoc in archive**.</span></span>

   * <span data-ttu-id="54600-114">Si vous choisissez toospecify un **URL de Javadoc**, utilisez hello URL comme **http://dl.windowsazure.com/javadoc** ou **http://dl.windowsazure.com/storage/javadoc**.</span><span class="sxs-lookup"><span data-stu-id="54600-114">If you choose toospecify a **Javadoc URL**, use hello URLs such as **http://dl.windowsazure.com/javadoc** or **http://dl.windowsazure.com/storage/javadoc**.</span></span>

   * <span data-ttu-id="54600-115">Si vous choisissez toouse **Javadoc dans une archive**, vous pouvez spécifier un fichier externe ou un fichier de l’espace de travail.</span><span class="sxs-lookup"><span data-stu-id="54600-115">If you choose toouse **Javadoc in archive**, you can specify an external file, or a workspace file.</span></span>

   <span data-ttu-id="54600-116">Faites votre choix et parcourez/validez en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="54600-116">Make your choice and browse/validate as needed.</span></span> <span data-ttu-id="54600-117">Hello exemple suivant associe hello les bibliothèques Azure pour Java hello JAR Javadoc correspondant a été téléchargé localement dossier tooa nommé **c:\MyAzureJARs**.</span><span class="sxs-lookup"><span data-stu-id="54600-117">hello following example associates hello Azure Libraries for Java with hello corresponding Javadoc JAR that has been downloaded locally tooa folder named **c:\MyAzureJARs**.</span></span>

   ![][ic553487]

* <span data-ttu-id="54600-118">*Étape facultative* : cliquez sur **Valider**.</span><span class="sxs-lookup"><span data-stu-id="54600-118">*Optional Step*: Click **Validate**.</span></span> <span data-ttu-id="54600-119">Problèmes potentiels avec hello JAR Javadoc pourraient apparaître ici.</span><span class="sxs-lookup"><span data-stu-id="54600-119">Potential issues with hello Javadoc JAR could be displayed here.</span></span>

* <span data-ttu-id="54600-120">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="54600-120">Click **OK**.</span></span>

<span data-ttu-id="54600-121">Une fois associé à la bibliothèque de hello, hello contenu Javadoc doit s’afficher dans votre IDE Eclipse.</span><span class="sxs-lookup"><span data-stu-id="54600-121">Once associated with hello library, hello Javadoc content should display within your Eclipse IDE.</span></span> <span data-ttu-id="54600-122">Par exemple, si `blob` est défini de type `CloudBlockBlob` dans votre code, hello Voici un exemple de contenu Javadoc qui apparaît lorsque vous tapez `blob.acquireLease` dans le code :</span><span class="sxs-lookup"><span data-stu-id="54600-122">For example, if `blob` is defined of type `CloudBlockBlob` within your code, hello following is an example of Javadoc content that appears when you type `blob.acquireLease` in code:</span></span>

![][ic553488]

## <a name="see-also"></a><span data-ttu-id="54600-123">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="54600-123">See Also</span></span>
<span data-ttu-id="54600-124">[Kit de ressources Azure pour Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="54600-124">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="54600-125">[Création d’une application Hello World pour Azure dans Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="54600-125">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="54600-126">[Lors de l’installation hello boîte à outils Azure pour Eclipse][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="54600-126">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="54600-127">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez hello [centre de développement Java Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="54600-127">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic553487]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553487.png
[ic553488]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553488.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh698319.aspx -->
