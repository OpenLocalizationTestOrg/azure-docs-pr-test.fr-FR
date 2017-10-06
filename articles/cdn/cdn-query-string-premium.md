---
title: "aaaControl comportement de mise en cache CDN Azure avec les chaînes de requête - Premium | Documents Microsoft"
description: "Chaîne de requête Azure CDN mise en cache des contrôles de façon dont les fichiers sont toobe mis en cache s’ils contiennent des chaînes de requête."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 99db4a85-4f5f-431f-ac3a-69e05518c997
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 5c97cf0230ae13fd378bfce49481f3135a5ef101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings---premium"></a>Contrôle du comportement de mise en cache du CDN Azure avec des chaînes de requête - Premium
> [!div class="op_single_selector"]
> * [Standard](cdn-query-string.md)
> * [CDN Azure Premium fourni par Verizon](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a>Vue d'ensemble
Chaîne de requête mise en cache des contrôles de façon dont les fichiers sont toobe mis en cache s’ils contiennent des chaînes de requête.

> [!IMPORTANT]
> produits Standard et Premium CDN Hello fournissent hello même fonctionnalité de mise en cache de chaîne de requête, mais diffère de l’interface utilisateur de hello.  Ce document décrit l’interface hello pour **Azure CDN Premium de Verizon**.  Pour la mise en cache des chaînes de requête avec le **CDN Azure Standard fourni par Akamai** et le **CDN Azure Standard fourni par Verizon**, consultez [Contrôle du comportement de mise en cache des demandes CDN avec des chaînes de requête](cdn-query-string.md).
> 
> 

Trois modes sont disponibles :

* **standard-cache**: c’est le mode par défaut hello.  nœud de périmètre CDN Hello passera la chaîne de requête hello à partir de l’origine de toohello hello demandeur sur la première demande de hello et asset hello de cache.  Toutes les demandes ultérieures pour cet élément multimédia qui sont pris en charge à partir du nœud de périmètre hello ignore la chaîne de requête hello jusqu'à ce que les ressources mises en cache hello expire.
* **Aucun cache**: dans ce mode, les demandes de chaînes de requête ne sont pas mis en cache au niveau du nœud de périmètre CDN hello.  nœud de périmètre Hello récupère les ressources hello directement à partir de l’origine de hello et lui transmet demandeur toohello avec chaque demande.
* **unique-cache** : ce mode traite chaque demande avec une chaîne de requête comme élément multimédia unique avec son propre cache.  Par exemple, hello origine hello pour une demande de réponse *foo.ashx?q=bar* seraient mis en cache dans le nœud de périmètre hello et retourné pour les caches suivantes avec cette même chaîne de requête.  Une demande de *foo.ashx?q=somethingelse* mise en cache comme un actif distinct avec sa propre toolive le temps.

## <a name="changing-query-string-caching-settings-for-premium-cdn-profiles"></a>Modification des paramètres de mise en cache des chaînes de requête pour les profils CDN Premium
1. À partir du Panneau de profil hello CDN, cliquez sur hello **gérer** bouton.
   
    ![Bouton de gestion du panneau de profil CDN](./media/cdn-query-string-premium/cdn-manage-btn.png)
   
    portail de gestion CDN Hello s’ouvre.
2. Pointage hello **grand HTTP** tab, puis pointez sur hello **paramètres de Cache** menu volant.  Cliquez sur **Mise en cache des chaînes de requête**.
   
    Les options de mise en cache des chaînes de requête s'affichent.
   
    ![Options de mise en cache des chaînes de requête CDN](./media/cdn-query-string-premium/cdn-query-string.png)
3. Après avoir effectué votre sélection, cliquez sur hello **mise à jour** bouton.

> [!IMPORTANT]
> modifications apportées aux paramètres de Hello n’est peut-être pas immédiatement visible, comme le temps requis pour toopropagate d’inscription hello via hello CDN.  Pour les profils du <b>CDN Azure fourni par Verizon</b>, la propagation s’effectue généralement dans un délai de 90 minutes, mais elle peut prendre plus de temps dans certains cas.
> 
> 

