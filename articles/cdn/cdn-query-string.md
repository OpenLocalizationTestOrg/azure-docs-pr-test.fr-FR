---
title: "comportement de mise en cache CDN Azure avec les chaînes de requête d’aaaControl | Documents Microsoft"
description: "Chaîne de requête Azure CDN mise en cache des contrôles de façon dont les fichiers sont toobe mis en cache s’ils contiennent des chaînes de requête."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 17410e4f-130e-489c-834e-7ca6d6f9778d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: e7a138b2decec624a29eb703ad9a291d19c44ee8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings"></a>Contrôle du comportement de mise en cache du CDN Azure avec des chaînes de requête
> [!div class="op_single_selector"]
> * [Standard](cdn-query-string.md)
> * [CDN Azure Premium fourni par Verizon](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a>Vue d'ensemble
Chaîne de requête mise en cache des contrôles de façon dont les fichiers sont toobe mis en cache s’ils contiennent des chaînes de requête.

> [!IMPORTANT]
> produits Standard et Premium CDN Hello fournissent hello même fonctionnalité de mise en cache de chaîne de requête, mais diffère de l’interface utilisateur de hello.  Ce document décrit l’interface hello pour **Azure CDN Standard à partir d’Akamai** et **Azure CDN Standard de Verizon**.  Pour la mise en cache des chaînes de requête avec le **CDN Azure Premium fourni par Verizon**, consultez [Contrôle du comportement de mise en cache des demandes CDN avec des chaînes de requête – Premium](cdn-query-string-premium.md).
> 
> 

Trois modes sont disponibles :

* **Ignorer les chaînes de requête**: c’est le mode par défaut hello.  nœud de périmètre CDN Hello passera la chaîne de requête hello à partir de l’origine de toohello hello demandeur sur la première demande de hello et asset hello de cache.  Toutes les demandes ultérieures pour cet élément multimédia qui sont pris en charge à partir du nœud de périmètre hello ignore la chaîne de requête hello jusqu'à ce que les ressources mises en cache hello expire.
* **Ignorer la mise en cache pour les URL avec des chaînes de requête**: dans ce mode, les demandes de chaînes de requête ne sont pas mis en cache au niveau du nœud de périmètre CDN hello.  nœud de périmètre Hello récupère les ressources hello directement à partir de l’origine de hello et lui transmet demandeur toohello avec chaque demande.
* **Mettre en cache chaque URL unique** : ce mode traite chaque demande avec une chaîne de requête comme élément multimédia unique avec son propre cache.  Par exemple, hello origine hello pour une demande de réponse *foo.ashx?q=bar* seraient mis en cache dans le nœud de périmètre hello et retourné pour les caches suivantes avec cette même chaîne de requête.  Une demande de *foo.ashx?q=somethingelse* mise en cache comme un actif distinct avec sa propre toolive le temps.

## <a name="changing-query-string-caching-settings-for-standard-cdn-profiles"></a>Modification des paramètres de mise en cache des chaînes de requête pour les profils CDN Standard
1. À partir du Panneau de profil CDN hello, cliquez sur le point de terminaison CDN hello toomanage vous le souhaitez.
   
    ![Points de terminaison du panneau de profil CDN](./media/cdn-query-string/cdn-endpoints.png)
   
    Panneau de point de terminaison CDN Hello s’ouvre.
2. Cliquez sur hello **configurer** bouton.
   
    ![Bouton de gestion du panneau de profil CDN](./media/cdn-query-string/cdn-config-btn.png)
   
    Panneau de Configuration CDN Hello s’ouvre.
3. Sélectionnez un paramètre de hello **comportement de mise en cache de chaîne de requête** liste déroulante.
   
    ![Options de mise en cache des chaînes de requête CDN](./media/cdn-query-string/cdn-query-string.png)
4. Après avoir effectué votre sélection, cliquez sur hello **enregistrer** bouton.

> [!IMPORTANT]
> modifications apportées aux paramètres de Hello n’est peut-être pas immédiatement visible, comme le temps requis pour toopropagate d’inscription hello via hello CDN.  Pour <b>Azure CDN fourni par Akamai</b> , la propagation s’effectue généralement dans un délai d’une minute.  Pour les profils du <b>CDN Azure fourni par Verizon</b>, la propagation s’effectue généralement dans un délai de 90 minutes, mais elle peut prendre plus de temps dans certains cas.
> 
> 

