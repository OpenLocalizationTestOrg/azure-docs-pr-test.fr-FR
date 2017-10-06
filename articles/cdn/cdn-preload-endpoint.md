---
title: aaaPre-chargement des ressources sur un point de terminaison CDN Azure | Documents Microsoft
description: "Découvrez comment toopre-charge mise en cache le contenu sur un point de terminaison CDN Azure."
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 5ea3eba5-1335-413e-9af3-3918ce608a83
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 08ac4b834f1ac8ce59d22e65fa8adea11bafcf17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="pre-load-assets-on-an-azure-cdn-endpoint"></a>Préchargement d’éléments multimédias sur un point de terminaison CDN Azure
[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

Par défaut, les éléments sont d'abord mis en cache lorsqu'ils sont demandés. Cela signifie que hello première requête de chaque région peut être plus longue, étant donné que les serveurs de périphérie hello n’aura pas le contenu hello mis en cache et devez serveur d’origine toohello tooforward hello demande. Le préchargement du contenu permet d'éviter cette latence à la première occurrence.

En outre tooproviding une meilleure expérience client, préchargement vos ressources mises en cache peut également réduire le trafic réseau sur le serveur d’origine hello.

> [!NOTE]
> Préchargement des ressources est utile pour les événements de grande taille ou de contenu qui devient tooa accessibles simultanément un grand nombre d’utilisateurs, comme une nouvelle version de film ou d’une mise à jour logicielle.
> 
> 

Ce didacticiel vous guide tout au long du préchargement de contenu mis en cache sur tous les nœuds de périphérie CDN Azure.

## <a name="walkthrough"></a>Procédure pas à pas
1. Bonjour [Azure Portal](https://portal.azure.com), parcourir le profil CDN toohello contenant hello de point de terminaison souhaité toopre en charge.  Panneau de profil Hello s’ouvre.
2. Cliquez sur le point de terminaison hello dans la liste de hello.  Panneau de point de terminaison Hello s’ouvre.
3. À partir du Panneau de point de terminaison CDN hello, cliquez sur le bouton charger de hello.
   
    ![Panneau du point de terminaison CDN](./media/cdn-preload-endpoint/cdn-endpoint-blade.png)
   
    Panneau de charge Hello s’ouvre.
   
    ![Panneau de chargement CDN](./media/cdn-preload-endpoint/cdn-load-blade.png)
4. Entrez le chemin d’accès complet de hello de chaque élément multimédia, vous souhaitez tooload (par exemple, `/pictures/kitten.png`) Bonjour **chemin d’accès** zone de texte.
   
   > [!TIP]
   > Plus **chemin d’accès** zones de texte s’affiche après que vous entrez le texte tooallow toobuild une liste de plusieurs ressources.  Vous pouvez supprimer des éléments multimédias à partir de la liste de hello en cliquant sur le bouton de sélection (...) hello.
   > 
   > Chemins d’accès doivent être une URL relative qui correspond à la suivante de hello [expression régulière](https://msdn.microsoft.com/library/az24scfc.aspx):  
   > >Chargement d’un fichier unique `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`;  
   > >Chargement d’un fichier unique avec chaîne de requête `@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`  
   > 
   > Chaque élément multimédia doit avoir son propre chemin d’accès.  Il n’existe aucune fonctionnalité de caractère générique pour le préchargement d’éléments multimédias.
   > 
   > 
   
    ![Bouton Charger](./media/cdn-preload-endpoint/cdn-load-paths.png)
5. Cliquez sur hello **charge** bouton.
   
    ![Bouton Charger](./media/cdn-preload-endpoint/cdn-load-button.png)

> [!NOTE]
> Il existe une limite de 10 demandes de chargement par minute et par profil CDN. 50 chemins sont autorisés par demande. Chaque chemin a une longueur limitée à 1 024 caractères.
> 
> 

## <a name="see-also"></a>Voir aussi
* [Purger un point de terminaison CDN Azure](cdn-purge-endpoint.md)
* [Référence API REST du CDN Azure - Vider ou pré-charger un point de terminaison](https://msdn.microsoft.com/library/mt634451.aspx)

