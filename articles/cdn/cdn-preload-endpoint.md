---
title: "Préchargement d’éléments multimédias sur un point de terminaison CDN Azure | Microsoft Docs"
description: "Découvrez comment précharger du contenu mis en cache sur un point de terminaison CDN Azure."
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
ms.openlocfilehash: 1f2dcd9a91bb6e883cbef06373c1acd98bf8d45f
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="pre-load-assets-on-an-azure-cdn-endpoint"></a>Préchargement d’éléments multimédias sur un point de terminaison CDN Azure
[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

Par défaut, les éléments sont d'abord mis en cache lorsqu'ils sont demandés. Cela signifie que la première requête de chaque région peut prendre plus de temps puisque le contenu des serveurs Edge ne sera pas mis en cache et que vous devrez transmettre la requête au serveur d'origine. Le préchargement du contenu permet d'éviter cette latence à la première occurrence.

En plus d’offrir une meilleure expérience client, le préchargement de vos ressources mises en cache peut également réduire le trafic réseau sur le serveur d'origine.

> [!NOTE]
> Le préchargement des ressources est utile lors de grands événements ou lorsque le contenu est disponible simultanément pour un grand nombre d’utilisateurs, par exemple lors de la sortie d’un film ou d’une mise à jour logicielle.
> 
> 

Ce didacticiel vous guide tout au long du préchargement de contenu mis en cache sur tous les nœuds de périphérie CDN Azure.

## <a name="walkthrough"></a>Procédure pas à pas
1. Dans le [portail Azure](https://portal.azure.com), recherchez le profil CDN qui contient le point de terminaison que vous souhaitez précharger.  Le panneau Profil s’ouvre.
2. Cliquez sur le point de terminaison dans la liste.  Le panneau du point de terminaison s’ouvre.
3. Dans le panneau du point de terminaison CDN, cliquez sur le bouton Charger.
   
    ![Panneau du point de terminaison CDN](./media/cdn-preload-endpoint/cdn-endpoint-blade.png)
   
    Le panneau Charger s’ouvre.
   
    ![Panneau de chargement CDN](./media/cdn-preload-endpoint/cdn-load-blade.png)
4. Entrez le chemin complet de chaque élément multimédia que vous souhaitez charger (par exemple, `/pictures/kitten.png`) dans la zone de texte **Chemin d’accès** .
   
   > [!TIP]
   > Après avoir saisi du texte, d’autres zones de texte **Chemin d’accès** s’afficheront pour vous permettre de créer une liste de plusieurs éléments multimédias.  Vous pouvez supprimer des éléments multimédias de la liste en cliquant sur le bouton points de suspension (...).
   > 
   > Les chemins d’accès doivent être une URL relative qui satisfait à [l’expression régulière](https://msdn.microsoft.com/library/az24scfc.aspx) suivante :  
   > >Chargement d’un fichier unique `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`;  
   > >Chargement d’un fichier unique avec chaîne de requête `@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`  
   > 
   > Chaque élément multimédia doit avoir son propre chemin d’accès.  Il n’existe aucune fonctionnalité de caractère générique pour le préchargement d’éléments multimédias.
   > 
   > 
   
    ![Bouton Charger](./media/cdn-preload-endpoint/cdn-load-paths.png)
5. Cliquez sur le bouton **Charger** .
   
    ![Bouton Charger](./media/cdn-preload-endpoint/cdn-load-button.png)

> [!NOTE]
> Il existe une limite de 10 demandes de chargement par minute et par profil CDN. 50 chemins sont autorisés par demande. Chaque chemin a une longueur limitée à 1 024 caractères.
> 
> 

## <a name="see-also"></a>Voir aussi
* [Purger un point de terminaison CDN Azure](cdn-purge-endpoint.md)
* [Référence API REST du CDN Azure - Vider ou pré-charger un point de terminaison](https://msdn.microsoft.com/library/mt634451.aspx)

