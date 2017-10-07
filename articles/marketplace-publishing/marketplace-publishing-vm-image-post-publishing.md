---
title: "aaaManaging Bonjour Azure Marketplace de l’image de votre machine virtuelle | Documents Microsoft"
description: "Guide détaillé sur la façon dont toomanage votre image de machine virtuelle Bonjour Azure Marketplace après la publication initiale"
services: Azure Marketplace
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: cc8648d4-59c2-4678-b47d-992300677537
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 08/03/2016
ms.author: hascipio;
ms.openlocfilehash: 47a082e686e1248ceacb844d3c0f2f5c33133dab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="post-production-guide-for-virtual-machine-offers-in-hello-azure-marketplace"></a>Guide de post production pour la machine virtuelle offre Bonjour Azure Marketplace
Cet article explique comment vous pouvez mettre à jour une offre en ordinateur virtuel Bonjour Azure Marketplace. Il vous guide dans les processus de hello d’ajout d’une ou plusieurs nouvelles références (SKU) tooan offre existante. Il vous guide également dans le processus hello de la suppression d’une offre de live ordinateur virtuel ou de la référence (SKU) de hello Marketplace.

Une fois une offre/référence (SKU) soit préparé Bonjour [portail Azure](http://portal.azure.com), vous ne pouvez pas modifier hello suivant des zones de texte :

* **Offrent identificateur**: Bonjour publication portail, accédez trop**virtuels** et sélectionnez votre offre. Cliquez ensuite sur **IMAGES DE MACHINE VIRTUELLE** > **Identificateur de l’offre**.
* **Identificateur de référence (SKU)**: Bonjour publication portail, accédez trop**virtuels** et sélectionnez votre offre. Cliquez ensuite sur **Références (SKU)** > **Ajouter une référence (SKU)**.
* **Publisher Namespace**: Bonjour publication portail, accédez trop**virtuels** > **procédure pas à pas** > **indiquent nous sur votre société** (figurant sous « Étape 2 inscrire votre entreprise ») > **Publisher Namespace** > **Namespace**.

Une fois hello offre/référence (SKU) est répertorié dans hello [Marketplace](http://azure.microsoft.com/marketplace), vous ne pouvez pas modifier hello suivant des zones de texte :

* **Offrent identificateur**: Bonjour publication portail, accédez trop**virtuels** et sélectionnez votre offre. Cliquez ensuite sur **IMAGES DE MACHINE VIRTUELLE** > **Identificateur de l’offre**.
* **Identificateur de référence (SKU)**: Bonjour publication portail, accédez trop**virtuels** et sélectionnez votre offre. Cliquez ensuite sur **Références (SKU)** > **Ajouter une référence (SKU)**.
* **Publisher Namespace**: Bonjour publication portail, accédez trop**virtuels** > **procédure pas à pas** > **indiquent nous sur votre société** (figurant sous « Étape 2 inscrire ») **Publisher Namespace** > **Namespace**.
* **Ports**: Bonjour publication portail, accédez trop**virtuels** et sélectionnez votre offre. Cliquez ensuite sur **IMAGES DE MACHINE VIRTUELLE** > **Ports ouverts**.
* **Modification de la tarification des références (SKU) répertoriées**
* **Modification du modèle de facturation des références (SKU) répertoriées**
* **Suppression des régions de facturation des références répertoriées**
* **Nombre de SKU(s) répertoriés de disque de données hello modification**

## <a name="update-hello-technical-details-of-a-sku"></a>Mettre à jour des détails techniques hello d’une référence (SKU)
tooadd un toohello version nouvelle liste de référence (SKU) et republier votre offre, suivez ces étapes :

1. Connectez-vous à toohello [portail de publication](https://publish.windowsazure.com).
2. Accédez toohello **virtuels** et sélectionnez votre offre.
3. Dans le menu hello hello gauche, cliquez sur hello **IMAGES de machine virtuelle** onglet.
4. Bonjour **SKU** section, recherchez hello référence (SKU) que vous souhaitez tooupdate.
5. Ajouter un nouveau numéro de version pour hello référence (SKU), puis cliquez sur hello  **+**  bouton. nouvelle version de Hello doit être au format X.Y.Z, où X, Y et Z sont des entiers. Les modifications de la version doivent uniquement être incrémentielles.
6. Bonjour **URL de disque dur virtuel du système d’exploitation** zone, entrez la signature d’accès partagé hello URI créé pour le VHD de système d’exploitation hello et enregistrer les modifications de hello.

   > [!IMPORTANT]
   > Vous ne pouvez pas incrémentation/décrémentation nombre de disques de données hello d’une référence (SKU) répertorié. Vous devez dans ce cas toocreate une nouvelle référence SKU. Pour obtenir des instructions détaillées, consultez toohello section [ajouter une nouvelle référence SKU sous une offre répertoriée](#add-a-new-sku-under-a-listed-offer).
   >
   >
7. Accédez toohello **publier** onglet, puis cliquez sur **PUSH tooSTAGING**. Pour obtenir des instructions détaillées sur le test de votre offre dans hello environnement intermédiaire, consultez [tester votre offre de la machine virtuelle pour hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
8. Une fois que vous avez testé votre offre de mise en lots, accédez à toohello **publier** onglet Bonjour portail de publication. Cliquez sur **demander une approbation tooPUSH tooPRODUCTION** toorepublish votre offre Bonjour Marketplace.

    ![Images de machine virtuelle](media/marketplace-publishing-vm-image-post-publishing/img01_07.png)

## <a name="update-hello-nontechnical-details-of-an-offer-or-a-sku"></a>Mettre à jour les détails techniques de hello d’une offre ou une référence (SKU)
Vous pouvez mettre à jour non technique hello (marketing, juridiques, prise en charge, catégories) les détails de votre offre dynamique ou de référence (SKU) Bonjour Marketplace.

### <a name="update-hello-offer-description-and-logos"></a>Mettre à jour la description de l’offre hello et logos
tooupdate hello détails de l’offre et republiez votre offre, procédez comme suit :

1. Connectez-vous à toohello [portail de publication](https://publish.windowsazure.com).
2. Accédez toohello **virtuels** et sélectionnez votre offre.
3. Dans le menu hello hello gauche, cliquez sur hello **MARKETING** onglet.
4. Cliquez sur **Anglais (États-Unis)**.
5. Cliquez sur hello **détails** onglet. Bonjour **Description** section, mise à jour hello offre **titre**, **Résumé**, et **résumé LONG** et enregistrer les modifications de hello.

   > [!NOTE]
   > Lorsque vous mettez à jour les informations de référence (SKU) hello, tenez compte de ces restrictions : 
   * N’entrez pas de texte en double pour la description de l’offre hello et une description de référence (SKU) hello.
   * N’entrez pas de texte en double pour le titre de référence (SKU) hello et offre hello résumée. 
   * N’entrez pas de texte en double pour le titre de référence (SKU) hello et synthèse de l’offre hello.
   >
   >

    ![Détails](media/marketplace-publishing-vm-image-post-publishing/img02.1_05.png)
6. Bonjour **LOGOS** section Hello **détails** , onglet de la mise à jour des logos de hello. Vérifiez que les logos hello suivent hello [des recommandations Azure Marketplace](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content).

   > [!NOTE]
   > Une bannière est facultative. Vous pouvez choisir pas tooupload une icône héros. Toutefois, après une icône héros est téléchargée, il n’existe aucun toodelete configurer à partir de hello portail de publication. Suivez hello [des recommandations icône héros](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content).
   >
   >
7. Accédez toohello **publier** onglet, puis cliquez sur **PUSH tooSTAGING**. Pour obtenir des instructions détaillées sur le test de votre offre dans hello environnement intermédiaire, consultez [tester votre offre de la machine virtuelle pour hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
8. Une fois que vous avez testé votre offre de mise en lots, accédez à toohello **publier** onglet Bonjour portail de publication. Cliquez sur **demander une approbation tooPUSH tooPRODUCTION** toorepublish votre offre Bonjour Marketplace.

    ![Logos](media/marketplace-publishing-vm-image-post-publishing/img02.1_08.png)

### <a name="update-hello-sku-description"></a>Mettre à jour la description de référence (SKU) hello
hello tooupdate référence (SKU) des détails et republiez votre offre, procédez comme suit :

1. Connectez-vous à toohello [portail de publication](https://publish.windowsazure.com).
2. Accédez toohello **virtuels** et sélectionnez votre offre.
3. Dans le menu hello hello gauche, cliquez sur hello **MARKETING** onglet.
4. Cliquez sur **Anglais (États-Unis)**.
5. Cliquez sur hello **PLANS** onglet. Bonjour **références (SKU)** section, mise à jour de la référence (SKU) de hello **titre**, **Résumé**, et **DESCRIPTION** et enregistrer les modifications de hello.

   > [!NOTE]
   > Lorsque vous mettez à jour les informations de référence (SKU) hello, tenez compte de ces restrictions : 
   * N’entrez pas de texte en double pour la description de l’offre hello et une description de référence (SKU) hello. 
   * N’entrez pas de texte en double pour le titre de référence (SKU) hello et offre hello résumée. 
   * N’entrez pas de texte en double pour le titre de référence (SKU) hello et synthèse de l’offre hello.
   >
   >
6. Accédez toohello **publier** onglet, puis cliquez sur **PUSH tooSTAGING**. Pour obtenir des instructions détaillées sur le test de votre offre dans hello environnement intermédiaire, consultez [tester votre offre de la machine virtuelle pour hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
7. Une fois que vous avez testé votre offre de mise en lots, accédez à toohello **publier** onglet Bonjour portail de publication. Cliquez sur **demander une approbation tooPUSH tooPRODUCTION** toorepublish votre offre Bonjour Marketplace.

    ![Abonnements](media/marketplace-publishing-vm-image-post-publishing/img02.2_07.png)

### <a name="change-existing-links-or-add-new-links"></a>Modifier ou ajouter des liens
toochange les liaisons existantes ou ajouter de nouvelles liaisons et puis republier votre offre, procédez comme suit :

1. Connectez-vous à toohello [portail de publication](https://publish.windowsazure.com).
2. Accédez toohello **virtuels** et sélectionnez votre offre.
3. Dans le menu hello hello gauche, cliquez sur hello **MARKETING** onglet.
4. Cliquez sur **Anglais (États-Unis)**.
5. Cliquez sur hello **liens** onglet.
6. tooadd un nouveau lien, Bonjour **liens** , cliquez sur **+ ajouter un lien**. Bonjour **ajouter un lien** boîte de dialogue, entrez le lien de hello **titre** et **URL** et enregistrer les modifications de hello. Vous pouvez entrer tout lien contenant des informations pouvant aider les clients.
7. tooupdate ou supprimer un lien existant, sélectionnez le lien de hello et cliquez sur hello **modifier** bouton ou hello **supprimer** bouton.

   > [!NOTE]
   > Assurez-vous que les liens hello que vous avez entré dans cette section fonctionnent correctement, car ces liens obtient validés lors du processus de demande de production.
   >
   >
8. Accédez toohello **publier** onglet, puis cliquez sur **PUSH tooSTAGING**. Pour obtenir des instructions détaillées sur le test de votre offre dans hello environnement intermédiaire, consultez [tester votre offre de la machine virtuelle pour hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
9. Une fois que vous avez testé votre offre de mise en lots, accédez à toohello **publier** onglet Bonjour portail de publication. Cliquez sur **demander une approbation tooPUSH tooPRODUCTION** toorepublish votre offre Bonjour Marketplace.

    ![Liens](media/marketplace-publishing-vm-image-post-publishing/img02.3_09-01.png)

    ![Ajouter un lien](media/marketplace-publishing-vm-image-post-publishing/img02.3-2.png)

### <a name="change-an-existing-sample-image-or-add-a-new-sample-image"></a>Modifier ou ajouter un exemple d’image
toochange un exemple existant de l’image ou ajouter de nouvelles images d’exemple et puis republier votre offre, procédez comme suit :

> [!NOTE]
> Image de qu’un seul échantillon est affichée dans hello [portail Azure](https://portal.azure.com).
>
>

1. Connectez-vous à toohello [portail de publication](https://publish.windowsazure.com).
2. Accédez toohello **virtuels** et sélectionnez votre offre.
3. Dans le menu hello hello gauche, cliquez sur hello **MARKETING** onglet.
4. Cliquez sur **Anglais (États-Unis)**.
5. Cliquez sur hello **exemples d’IMAGES** onglet.
6. tooadd une nouvelle image d’exemple, Bonjour **exemples d’Images** , cliquez sur **télécharger une IMAGE** et enregistrer les modifications de hello.

   > [!NOTE]
   > L’ajout d’un exemple d’image est facultatif.
   >
7. Accédez toohello **publier** onglet, puis cliquez sur **PUSH tooSTAGING**. Pour obtenir des instructions détaillées sur le test de votre offre dans hello environnement intermédiaire, consultez [tester votre offre de la machine virtuelle pour hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
8. Une fois que vous avez testé votre offre de mise en lots, accédez à toohello **publier** onglet Bonjour portail de publication. Cliquez sur **demander une approbation tooPUSH tooPRODUCTION** toorepublish votre offre Bonjour Marketplace.

    ![Exemples d’images](media/marketplace-publishing-vm-image-post-publishing/img02.4_09.png)

### <a name="update-hello-legal-content"></a>Mettre à jour le contenu juridique hello
tooupdate hello contenu juridique et republiez votre offre, procédez comme suit :

1. Connectez-vous à toohello [portail de publication](https://publish.windowsazure.com).
2. Accédez toohello **virtuels** et sélectionnez votre offre.
3. Dans le menu hello hello gauche, cliquez sur hello **MARKETING** onglet.
4. Cliquez sur **Anglais (États-Unis)**.
5. Cliquez sur hello **juridique** onglet. Bonjour **juridique** section, mettre à jour vos stratégies/conditions d’utilisation. Entrez ou collez hello stratégies/conditions Bonjour **les conditions d’utilisation** zone et d’enregistrer les modifications de hello.
6. limite de caractères Hello pour les conditions légales d’utilisation de hello est 1 million de caractères.
7. Accédez toohello **publier** onglet, puis cliquez sur **PUSH tooSTAGING**. Pour obtenir des instructions détaillées sur le test de votre offre dans hello environnement intermédiaire, consultez [tester votre offre de la machine virtuelle pour hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
8. Une fois que vous avez testé votre offre de mise en lots, accédez à toohello **publier** onglet Bonjour portail de publication. Cliquez sur **demander une approbation tooPUSH tooPRODUCTION** toorepublish votre offre Bonjour Marketplace.

    ![Informations juridiques](media/marketplace-publishing-vm-image-post-publishing/img02.5_08.png)

### <a name="update-hello-support-information"></a>Mettre à jour les informations de prise en charge de hello
tooupdate hello prend en charge les informations et republiez votre offre, procédez comme suit :

1. Connectez-vous à toohello [portail de publication](https://publish.windowsazure.com).
2. Accédez toohello **virtuels** et sélectionnez votre offre.
3. Dans le menu hello hello gauche, cliquez sur hello **prise en charge** onglet.
4. Bonjour **contactez ingénierie** section, les informations de contact engineering hello mise à jour. Ces informations sont utilisées pour la communication interne entre les partenaires hello et Microsoft uniquement.
5. Bonjour **Support technique** section, mettre à jour les informations de contact de support hello et hello **prennent en charge les URL**. Ces informations sont utilisées pour la communication interne entre les partenaires hello et Microsoft uniquement.

   > [!NOTE]
   > Si vous souhaitez tooprovide uniquement le support par courrier électronique, entrez un numéro de téléphone factice Bonjour **Support technique** section. Dans ce cas, hello par courrier électronique que vous avez fourni est utilisé à la place.
   >
   >
6. Accédez toohello **publier** onglet, puis cliquez sur **PUSH tooSTAGING**. Pour obtenir des instructions détaillées sur le test de votre offre dans hello environnement intermédiaire, consultez [tester votre offre de la machine virtuelle pour hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
7. Une fois que vous avez testé votre offre de mise en lots, accédez à toohello **publier** onglet Bonjour portail de publication. Cliquez sur **demander une approbation tooPUSH tooPRODUCTION** toorepublish votre offre Bonjour Marketplace.

    ![Support](media/marketplace-publishing-vm-image-post-publishing/img02.6_07.png)

### <a name="update-hello-categories"></a>Mettre à jour des catégories de hello
hello tooupdate catégories de section de votre offre et republiez votre offre, procédez comme suit :

1. Connectez-vous à toohello [portail de publication](https://publish.windowsazure.com).
2. Accédez toohello **virtuels** et sélectionnez votre offre.
3. Dans le menu hello hello gauche, cliquez sur hello **catégories** onglet.
4. Bonjour **catégories** section, mettre à jour des catégories de hello pour votre offre et enregistrer les modifications de hello. Vous pouvez choisir les catégories de toofive pour la galerie Azure Marketplace de hello.
5. Accédez toohello **publier** onglet, puis cliquez sur **PUSH tooSTAGING**. Pour obtenir des instructions détaillées sur le test de votre offre dans hello environnement intermédiaire, consultez [tester votre offre de la machine virtuelle pour hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
6. Une fois que vous avez testé votre offre de mise en lots, accédez à toohello **publier** onglet Bonjour portail de publication. Cliquez sur **demander une approbation tooPUSH tooPRODUCTION** toorepublish votre offre Bonjour Marketplace.

    ![Catégories](media/marketplace-publishing-vm-image-post-publishing/img02.7_06.png)

## <a name="add-a-new-sku-under-a-listed-offer"></a>Ajouter une référence (SKU) à une offre répertoriée
tooadd une nouvelle référence (SKU) dans votre offre live, procédez comme suit :

1. Connectez-vous à toohello [portail de publication](https://publish.windowsazure.com).
2. Accédez toohello **virtuels** et sélectionnez votre offre.
3. Dans le menu hello hello gauche, cliquez sur hello **SKU** onglet. Cliquez ensuite sur **Add a SKU** (Ajouter une référence (SKU)). 
4. Dans la boîte de dialogue hello, entrez un **identificateur de référence (SKU)** en minuscules. Sélectionnez hello **mettre votre propre modèle de facturation de licence (BYOL)** case à cocher si vous souhaitez toopublish hello nouvelle référence (SKU) avec un modèle de facturation BYOL. Sinon, désactivez hello. Cliquez sur hello cycle d’interrogation toocreate une nouvelle référence SKU. Si vous n’avez pas choisi le modèle de facturation hello BYOL, le modèle de facturation hello est définie automatiquement toohourly. Si vous souhaitez essai gratuit de 30 jours hello pour le modèle de facturation horaire hello, sélectionnez **un mois** pour **est une version d’évaluation gratuite disponible ?** Autrement, sélectionnez **Pas de version d’évaluation**. (**Est une version d’évaluation gratuite disponible ?**  s’affiche uniquement si vous n’avez pas sélectionné BYOL lors de la création d’hello nouvelle référence (SKU).)

   > [!IMPORTANT]
   > **Masquer cette référence SKU de hello Marketplace, car il doit toujours être acheté via un modèle de solution** doit être **Oui** *uniquement* si vous avez approuvé pour la publication d’un modèle de solution. Dans le cas contraire, cette option doit toujours être définie sur **Non**.
   >
   >
4. Dans le menu hello hello gauche, cliquez sur hello **IMAGES de machine virtuelle** onglet et découvrez hello nouvelle référence (SKU) que vous avez créée.
5. tooset jusqu'à hello nouvelle référence (SKU), consultez [obtenir la certification de votre image de machine virtuelle](marketplace-publishing-vm-image-creation.md#5-obtain-certification-for-your-vm-image) pour obtenir des conseils.
6. tooadd marketing documents pour hello nouvelle référence (SKU), consultez [Marketplace fournissent contenu commercial](marketplace-publishing-push-to-staging.md#step-1-provide-marketplace-marketing-content).
7. tooadd informations de tarification pour hello nouvelle référence (SKU), consultez [définir votre prix](marketplace-publishing-push-to-staging.md#step-2-set-your-prices).
8. Accédez toohello **publier** onglet, puis cliquez sur **PUSH tooSTAGING**. Pour obtenir des instructions détaillées sur le test de votre offre dans hello environnement intermédiaire, consultez [tester votre offre de la machine virtuelle pour hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
9. Une fois que vous avez testé votre offre de mise en lots, accédez à toohello **publier** onglet Bonjour portail de publication. Cliquez sur **demander une approbation tooPUSH tooPRODUCTION** toorepublish votre offre Bonjour Marketplace.

    ![Références (SKU)](media/marketplace-publishing-vm-image-post-publishing/img03_09-01.png)

    ![Ajoutez une référence (SKU)](media/marketplace-publishing-vm-image-post-publishing/img03_09-02.png)

## <a name="change-hello-data-disk-count-for-a-listed-sku"></a>Modifier le nombre de disques de données de hello pour une référence (SKU) répertorié
Vous ne pouvez pas incrémentation/décrémentation nombre de disques de données hello d’une référence (SKU) répertorié. Vous devez dans ce cas toocreate une nouvelle référence SKU. Pour obtenir des instructions détaillées, consultez toohello section [ajouter une nouvelle référence SKU sous une offre répertoriée](#add-a-new-sku-under-a-listed-offer).

## <a name="delete-a-listed-offer-from-hello-marketplace"></a>Supprimer une offre répertoriée hello Marketplace
Divers aspects doivent toobe pris en charge dans les cas de hello d’un tooremove demande une offre en direct. recommandations de tooget de hello prise en charge team tooremove une offre répertoriée de hello Marketplace, procédez comme suit :

1. Génère un ticket de support sur hello [créer un incident](https://support.microsoft.com/en-us/getsupport?wf=0&tenant=ClassicCommercial&oaspworkflow=start_1.0.0.0&locale=en-us&supportregion=en-us&pesid=15635&ccsid=635993707583706681) page.

2. Pour **Gestion des offres**, sélectionnez **Type de problème**, puis, pour **Modification d’une offre et/ou d’une référence (SKU) déjà en production**, sélectionnez **Catégorie**.
3. Soumettre la demande de hello.

équipe de support Hello vous guide tout au long des processus de suppression hello offre/référence (SKU).

> [!NOTE]
> Vous pouvez toujours supprimer une offre de hello alors qu’il est dans l’état Brouillon (mais pas d’intermédiaire ou de Production). Sur hello **historique** , cliquez sur **annuler le brouillon**.
>
>

## <a name="delete-a-listed-sku-from-hello-marketplace"></a>Supprimer une référence (SKU) répertorié hello Marketplace
toodelete une référence (SKU) répertorié de hello Marketplace, procédez comme suit :

1. Connectez-vous à toohello [portail de publication](https://publish.windowsazure.com).

2. Accédez toohello **virtuels** et sélectionnez votre offre.
3. Dans le volet hello hello gauche, cliquez sur hello **SKU** onglet.
4. Sélectionnez hello référence (SKU) que vous le souhaitez toodelete et cliquez sur hello **supprimer** bouton.
5. Accédez toohello **publier** onglet Bonjour portail de publication. Cliquez sur **tooPRODUCTION tooPUSH de demander une approbation** offre de hello toorepublish Bonjour Marketplace.
6. Une fois que l’offre de hello est republiée dans hello Marketplace, hello référence (SKU) est supprimé de hello Marketplace et hello portail Azure.

## <a name="delete-hello-current-version-of-a-listed-sku-from-hello-marketplace"></a>Supprimer version actuelle de hello d’une référence (SKU) répertorié hello Marketplace
version actuelle de hello toodelete d’une référence (SKU) répertorié de hello Marketplace, procédez comme suit : 

1. Connectez-vous à toohello [portail de publication](https://publish.windowsazure.com).

2. Accédez toohello **virtuels** et sélectionnez votre offre.
3. Dans le menu hello hello gauche, cliquez sur hello **IMAGES de machine virtuelle** onglet.
4. Sélectionnez hello SKU dont actuel version souhaité toodelete, cliquez sur hello **supprimer** bouton.
5. Accédez toohello **publier** onglet Bonjour portail de publication. Cliquez sur **tooPRODUCTION tooPUSH de demander une approbation** offre de hello toorepublish Bonjour Marketplace.
6. Une fois que l’offre de hello obtient republié Bonjour Marketplace, hello version actuelle de hello répertorié référence (SKU) est supprimé de hello Marketplace et hello portail Azure. Hello référence (SKU) est ensuite restaurée version précédente de tooits.

## <a name="revert-hello-listing-price-tooproduction-values"></a>Rétablir hello répertoriant les valeurs des prix tooproduction
valeurs de tooproduction toorevert hello liste de prix, procédez comme suit :

1. Connectez-vous à toohello [portail de publication](https://publish.windowsazure.com).
2. Accédez toohello **virtuels** et sélectionnez votre offre.
3. Dans le menu hello hello gauche, cliquez sur hello **tarification** onglet.
4. Sélectionnez une région dont vous souhaitez que le prix tooreset.

    ![Régions de tarification](media/marketplace-publishing-vm-image-post-publishing/img08-04.png)
5. Pour les références (SKU) avec un modèle de facturation toutes les heures, réinitialiser les prix hello pour tous les cœurs hello lorsqu’ils sont en production pour la région sélectionnée hello. Références (SKU) avec un modèle de facturation BYOL, rendez hello référence (SKU) disponible dans la région de hello en sélectionnant la case à cocher hello hello SKU Bonjour **EXTERNALLY-LICENSED (BYOL) référence (SKU) disponibilité** section.

    ![Modèles de tarification](media/marketplace-publishing-vm-image-post-publishing/img08-05.png)
6. Cliquez sur **AUTOPRICE OTHER MARKETS BASED ON PRICES IN UNITED STATES** (TARIFICATION AUTOMATIQUE POUR LES AUTRES MARCHÉS EN FONCTION DES PRIX AUX ÉTATS-UNIS).

   > [!NOTE]
   > étiquette du bouton Hello peut être différent selon la région hello que vous sélectionnez. Étant donné que nous avons sélectionné États-Unis, bouton de hello est étiqueté **AUTOPRICE autres marchés basés sur les prix IN États-Unis**.
   >
   >

    ![Tarifer automatiquement](media/marketplace-publishing-vm-image-post-publishing/img08-06.png)
7. Sur la page 1 de l’Assistant de Autoprice hello, choisissez de marché de base hello et cliquez sur hello **flèche** bouton.

    ![Marché de base](media/marketplace-publishing-vm-image-post-publishing/img08-07.png)
8. Dans la page 2, choisir des plans de service et les compteurs (cœurs), cliquez sur hello **flèche** bouton.

    ![Plans de service et compteurs](media/marketplace-publishing-vm-image-post-publishing/img08-08.png)
9. Dans la page 3, cliquez sur **bascule toutes les** tooselect toutes les régions. Vous pouvez aussi activer manuellement les cases à cocher de régions spécifiques. Cliquez sur hello **flèche** bouton.

    ![Choisir des marchés](media/marketplace-publishing-vm-image-post-publishing/img08-09.png)
10. Sur 4, examinez les taux de change hello, cliquez sur **Terminer**. Assistant de Hello réinitialise hello tarification conséquente tooyour sélections.

11. Sur hello **tarification** , cliquez sur **affichage résumé et les modifications**.
    Pour **View Version** (Version d’affichage), sélectionnez **Draft** (Brouillon), puis, pour **Compare with** (Comparer à), sélectionnez **Production**. Si vous ne voyez aucune différence de prix, hello tarification restaurer les valeurs de production toohello avec succès.

    ![Afficher le résumé et les modifications](media/marketplace-publishing-vm-image-post-publishing/img08-11.png)
12. Accédez toohello **publier** onglet, puis cliquez sur **PUSH tooSTAGING**. Pour obtenir des instructions détaillées sur le test de votre offre dans hello environnement intermédiaire, consultez [tester votre offre de la machine virtuelle pour hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
13. Une fois que vous avez testé votre offre de mise en lots, accédez à toohello **publier** onglet Bonjour portail de publication. Cliquez sur **demander une approbation tooPUSH tooPRODUCTION** toorepublish votre offre Bonjour Marketplace.

## <a name="revert-hello-billing-model-tooproduction-values"></a>Rétablir les valeurs tooproduction du modèle de facturation de hello
toorevert hello facturation tooproduction valeurs du modèle, procédez comme suit :

1. Connectez-vous à toohello [portail de publication](https://publish.windowsazure.com).

2. Accédez toohello **virtuels** et sélectionnez votre offre.
3. Dans le menu hello hello gauche, cliquez sur hello **SKU** onglet.
4. Cliquez sur hello **modifier** modèle de facturation bouton toorevert hello. Dans la fenêtre hello qui s’ouvre, activez ou désactivez hello **de facturation et de gestion de licences est effectuée en externe à partir de Azure (également appelé mettre votre propre licence)** case à cocher.

    ![Modifier la facturation](media/marketplace-publishing-vm-image-post-publishing/img09-04.png)
5. Suivez les étapes de hello dans « Hello Revert répertoriant les valeurs des prix tooproduction » de cet article.
6. Accédez toohello **publier** onglet, puis cliquez sur **PUSH tooSTAGING**. Pour obtenir des instructions détaillées sur le test de votre offre dans hello environnement intermédiaire, consultez [tester votre offre de la machine virtuelle pour hello Marketplace](marketplace-publishing-vm-image-test-in-staging.md).
7. Une fois que vous avez testé votre offre de mise en lots, accédez à toohello **publier** onglet Bonjour portail de publication. Cliquez sur **demander une approbation tooPUSH tooPRODUCTION** toorepublish votre offre Bonjour Marketplace.

## <a name="revert-hello-visibility-setting-of-a-listed-sku-toohello-production-value"></a>Rétablir le paramètre de visibilité hello d’une valeur de production toohello référence (SKU) répertorié
paramètre de visibilité hello toorevert d’une valeur de production SKU toohello répertoriée, procédez comme suit :

1. Connectez-vous à toohello [portail de publication](https://publish.windowsazure.com).

2. Accédez toohello **virtuels** et sélectionnez votre offre.
3. Dans le menu hello hello gauche, cliquez sur hello **SKU** onglet.
4. Sélectionnez votre référence (SKU) et rétablir le paramètre de visibilité hello Hello valeur de la production toohello référence (SKU).

    ![Visibilité](media/marketplace-publishing-vm-image-post-publishing/img10-04.png)
5. Une fois que vous avez terminé avec les modifications de hello, cliquez sur **demander une approbation tooPUSH tooPRODUCTION** toorepublish votre offre Bonjour Marketplace.

## <a name="see-also"></a>Voir aussi
* [Main : Publier un toohello offre Azure Marketplace](marketplace-publishing-getting-started.md)
* [Présentation de vos rapports de paiement Azure Marketplace](marketplace-publishing-report-payout.md)
* [Affichage et modification de « l’offre incitative revendeurs » des fournisseurs de solutions Cloud dans Azure Marketplace](marketplace-publishing-csp-incentive.md)
* [Résoudre les problèmes de publication courants Bonjour Marketplace](marketplace-publishing-support-common-issues.md)
* [Obtenir de l’aide en tant qu’éditeur](marketplace-publishing-get-publisher-support.md)
* [Créer une image de machine virtuelle locale](marketplace-publishing-vm-image-creation-on-premise.md)
* [Créer une machine virtuelle exécutant Windows dans le portail Azure en version préliminaire de hello](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
