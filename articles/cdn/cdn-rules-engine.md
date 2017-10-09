---
title: "comportement aaaOverride HTTP à l’aide du moteur de règles d’Azure CDN hello | Documents Microsoft"
description: "moteur de règles Hello vous permet de toocustomize comment les requêtes HTTP sont gérés par le CDN Azure, telles que le blocage de remise hello de certains types de contenu, définir une stratégie de mise en cache et modifier les en-têtes HTTP."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 625a912b-91f2-485d-8991-128cc194ee71
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: dd7194be9dbda43180c64568d3e1f52c5c513a7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="override-http-behavior-using-hello-azure-cdn-rules-engine"></a>Remplacer le comportement HTTP à l’aide du moteur de règles hello CDN Azure
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a>Vue d'ensemble
moteur de règles Hello vous permet de toocustomize comment sont gérées les demandes HTTP, telles que le blocage remise hello de certains types de contenu, la définition d’une stratégie de mise en cache et la modification des en-têtes HTTP.  Ce didacticiel va vous montrer la création d’une règle modifiera hello mise en cache de comportement des composants CDN.  Contenu vidéo est également disponible dans hello »[Voir aussi](#see-also)« section.

   > [!TIP] 
   > Pour une syntaxe de toohello référence détaillée, consultez [référence du moteur de règles](cdn-rules-engine-reference.md).
   > 


## <a name="tutorial"></a>Didacticiel
1. À partir du Panneau de profil hello CDN, cliquez sur hello **gérer** bouton.
   
    ![Bouton de gestion du panneau de profil CDN](./media/cdn-rules-engine/cdn-manage-btn.png)
   
    portail de gestion CDN Hello s’ouvre.
2. Cliquez sur hello **grand HTTP** onglet, suivi **moteur de règles**.
   
    Les options d'une nouvelle règle s'affichent.
   
    ![Options de nouvelle règle CDN](./media/cdn-rules-engine/cdn-new-rule.png)
   
   > [!IMPORTANT]
   > commande Hello dans lequel plusieurs règles sont répertoriés affecte comment elles sont gérées. Une règle suivante peut remplacer les actions de hello spécifiées par une règle précédente.
   > 
   > 
3. Entrez un nom dans hello **nom / Description** zone de texte.
4. Identifier le type hello de hello règle s’applique à des demandes.  Par défaut, hello **toujours** condition de correspondance est sélectionnée.  Pour ce didacticiel, vous allez utiliser **Toujours** , donc conservez cette option.
   
   ![Condition de correspondance CDN](./media/cdn-rules-engine/cdn-request-type.png)
   
   > [!TIP]
   > Il existe de nombreux types de correspondance conditions disponibles dans la liste déroulante de hello.  En cliquant sur hello bleu icône d’information toohello gauche de la condition de correspondance hello explique condition hello actuellement sélectionné en détail.
   > 
   >  Pour hello une liste complète des expressions conditionnelles en détail, consultez [Expressions conditionnelles du moteur de règles](cdn-rules-engine-reference-match-conditions.md).
   >  
   > Pour hello une liste complète des conditions de correspondance en détail, consultez [condition correspond à moteur de règles](cdn-rules-engine-reference-match-conditions.md).
   > 
   > 
5. Cliquez sur hello  **+**  bouton ensuite trop**fonctionnalités** tooadd une nouvelle fonctionnalité.  Dans la liste déroulante hello hello gauche, sélectionnez **Force interne Max-Age**.  Dans la zone de texte hello qui s’affiche, entrez **300**.  Laissez hello restant des valeurs par défaut.
   
   ![Fonctionnalité CDN](./media/cdn-rules-engine/cdn-new-feature.png)
   
   > [!NOTE]
   > Comme avec les conditions de correspondance, en cliquant sur toohello d’icône d’information hello bleue à gauche de hello nouvelle fonctionnalité affichera les détails sur cette fonctionnalité.  Dans les cas de hello de **Force interne Max-Age**, nous allons substitution de l’élément multimédia hello **Cache-Control** et **Expires** en-têtes toocontrol lorsque le nœud de périmètre CDN hello actualisera hello ressource à partir de l’origine de hello.  Notre exemple de 300 secondes signifie le nœud de périmètre CDN hello mettra en cache les ressources hello pendant 5 minutes avant d’actualiser asset hello à partir de son origine.
   > 
   > Pour hello une liste complète des fonctionnalités en détail, consultez [les détails sur les fonctionnalités du moteur de règles](cdn-rules-engine-reference-features.md).
   > 
   > 
6. Cliquez sur hello **ajouter** nouvelle règle bouton toosave hello.  nouvelle règle de Hello est maintenant en attente d’approbation. Une fois qu’elle a été approuvée, hello statut deviendra **XML en attente** trop**XML Active**.
   
   > [!IMPORTANT]
   > Les modifications de règles peuvent prendre jusqu'à toopropagate de minutes too90 via hello CDN.
   > 
   > 

## <a name="see-also"></a>Voir aussi
* [Vue d'ensemble d'Azure CDN](cdn-overview.md)
* [Référence du moteur de règles](cdn-rules-engine-reference.md)
* [Conditions de correspondance du moteur de règles](cdn-rules-engine-reference-match-conditions.md)
* [Expressions conditionnelles du moteur de règles](cdn-rules-engine-reference-conditional-expressions.md)
* [Fonctionnalités du moteur de règles](cdn-rules-engine-reference-features.md)
* [Le comportement par défaut HTTP à l’aide du moteur de règles hello](cdn-rules-engine.md)
* [Azure Friday : les nouvelles fonctionnalités Premium puissantes du CDN Azure](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (vidéo)