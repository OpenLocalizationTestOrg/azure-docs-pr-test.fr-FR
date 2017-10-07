---
title: aaaPurge un point de terminaison CDN Azure | Documents Microsoft
description: "Découvrez comment toopurge toutes les mises en cache contenu à partir d’un point de terminaison CDN Azure."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 0b50230b-fe82-4740-90aa-95d4dde8bd4f
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: a09f4a49aa1e2d7655ecae44b5126c11c28fd599
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="purge-an-azure-cdn-endpoint"></a>Purger un point de terminaison CDN Azure
## <a name="overview"></a>Vue d'ensemble
Noeuds CDN Azure mettra en cache les ressources jusqu'à ce que time-to-live (TTL) l’élément multimédia hello expire.  Après expiration de durée de vie de l’élément multimédia hello, lorsqu’un client demande un élément multimédia de hello à partir du nœud de périmètre hello, nœud de périmètre hello récupère une copie mise à jour de demande du client hello asset tooserve hello et stocker hello l’actualisation du cache.

toomake pratique Hello meilleures que vos utilisateurs obtiennent toujours copie la plus récente de vos ressources hello est tooversion actifs pour chaque mise à jour et les publier en tant que nouvelles URL.  CDN récupère immédiatement les nouvelles ressources de hello pour les demandes de client suivants hello.  Vous souhaiterez parfois toopurge mis en cache le contenu à partir de tous les nœuds de bord et les forcer tous les composants mis à jour de tooretrieve de nouveau.  Cela peut être dû à application web de tooyour tooupdates ou des ressources de mise à jour tooquickly qui contiennent des informations incorrectes.

> [!TIP]
> Notez que la purge efface uniquement hello mis en cache le contenu sur les serveurs de périmètre CDN hello.  Les caches en aval, tels que les serveurs proxy et les caches de navigateur local, peuvent contenir toujours une copie mise en cache du fichier de hello.  Il est important tooremember cela lorsque vous définissez un fichier durée de vie.  Vous pouvez forcer une client en aval toorequest hello version la plus récente de votre fichier en lui donnant un nom unique chaque fois que vous mettez à jour, ou en tirant parti des [mise en cache de la chaîne de requête](cdn-query-string.md).  
> 
> 

Ce didacticiel vous guide dans le processus de vidage des éléments multimédias de tous les nœuds d’un point de terminaison.

## <a name="walkthrough"></a>Procédure pas à pas
1. Bonjour [Azure Portal](https://portal.azure.com), recherchez le profil CDN toohello contenant le point de terminaison hello toopurge vous le souhaitez.
2. À partir du Panneau de profil CDN hello, cliquez sur le bouton de purge hello.
   
    ![Panneau du profil CDN](./media/cdn-purge-endpoint/cdn-profile-blade.png)
   
    Panneau de Purge Hello s’ouvre.
   
    ![Panneau de vidage CDN](./media/cdn-purge-endpoint/cdn-purge-blade.png)
3. Sur hello purger panneau, sélectionnez hello service adresse toopurge à partir de la liste déroulante de hello URL.
   
    ![Formulaire de vidage](./media/cdn-purge-endpoint/cdn-purge-form.png)
   
   > [!NOTE]
   > Vous pouvez également obtenir le panneau de Purge toohello en cliquant sur hello **purger** bouton sur le panneau de point de terminaison CDN hello.  Dans ce cas, hello **URL** champ sera prérempli avec l’adresse du service hello de ce point de terminaison spécifique.
   > 
   > 
4. Sélectionnez les ressources toopurge de hello noeuds.  Si vous le souhaitez tooclear tous les éléments multimédias, cliquez sur hello **effacera tous les** case à cocher.  Dans le cas contraire, chemin d’accès de type hello de chaque élément multimédia vous souhaitez toopurge Bonjour **chemin d’accès** zone de texte. Sous les formats sont pris en charge dans le chemin d’accès hello.
    1. **Purge d’URL unique**: immobilisation de Purge en spécifiant une URL complète hello, avec ou sans l’extension de fichier hello, par exemple,`/pictures/strasbourg.png`;`/pictures/strasbourg`
    2. **Vidage de caractères génériques** : l’astérisque (\*) peut être utilisé comme caractère générique. Purger tous les dossiers, sous-dossiers et fichiers sous un point de terminaison avec `/*` hello du chemin d’accès ou purger tous les sous-dossiers et fichiers dans un dossier spécifique en spécifiant le dossier hello suivie `/*`, par exemple,`/pictures/*`.  Notez que le vidage de caractère générique n’est pas compatible avec Azure CDN par Akamai. 
    3. **Vider le domaine racine**: racine hello de Purge du point de terminaison hello avec « / » dans le chemin d’accès hello.
   
   > [!TIP]
   > Chemins d’accès doit être spécifiés pour purger et doit être une URL relative qui correspondent à des éléments suivants de hello [expression régulière](https://msdn.microsoft.com/library/az24scfc.aspx). Le **vidage totale** et le **vidage de caractère générique** ne sont pas pris en charge par compatible avec **Azure CDN par Akamai**.
   > > Vidage d’URL unique `@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`  
   > > Chaîne de requête `@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`  
   > > Vidage de caractère générique `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`. 
   > 
   > Plus **chemin d’accès** zones de texte s’affiche après que vous entrez le texte tooallow toobuild une liste de plusieurs ressources.  Vous pouvez supprimer des éléments multimédias à partir de la liste de hello en cliquant sur le bouton de sélection (...) hello.
   > 
5. Cliquez sur hello **purger** bouton.
   
    ![Bouton Vider](./media/cdn-purge-endpoint/cdn-purge-button.png)

> [!IMPORTANT]
> Vider les demandes de prendre environ 2 à 3 minutes tooprocess avec **Azure CDN de Verizon** (Standard ou Premium) et environ 7 minutes avec **CDN Azure à partir d’Akamai**.  Le CDN Azure impose une limite de 50 demandes de vidage simultanées à un moment donné. 
> 
> 

## <a name="see-also"></a>Voir aussi
* [Préchargement d’éléments multimédias sur un point de terminaison CDN Azure](cdn-preload-endpoint.md)
* [Référence API REST du CDN Azure - Vider ou pré-charger un point de terminaison](https://msdn.microsoft.com/library/mt634451.aspx)

