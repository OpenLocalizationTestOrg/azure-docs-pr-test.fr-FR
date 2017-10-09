---
title: "distribution de contenu Azure pour votre scénario d’aaaOptimize"
description: "La remise toooptimize du contenu pour des scénarios spécifiques"
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: v-semcev
ms.openlocfilehash: 922a92fdbf7e6e21f2b5ae9a2fb4ac32735fc15a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-azure-content-delivery-for-your-scenario"></a>Optimiser la distribution de contenu Azure pour votre scénario

Lorsque vous fournissez le contenu tooa grand public mondial, il est remise hello optimisé de tooensure critiques de votre contenu. Bonjour Azure Content Delivery Network peut optimiser l’expérience hello en fonction de type hello du contenu que vous avez. Le contenu peut être un site web, un flux temps réel, une vidéo ou un fichier volumineux pour téléchargement. Lorsque vous créez un point de terminaison de réseau (CDN) de diffusion de contenu, vous spécifiez un scénario Bonjour **optimisé pour** option. Votre choix détermine quels optimisation est appliqué toohello contenu distribué à partir du point de terminaison CDN hello.

Choix d’optimisation est les performances de diffusion de contenu tooimprove toouse conçue comportements des meilleures pratiques et une meilleure origine décharger. Vos choix de scénario affecte les performances en modifiant les configurations de mise en cache partielle, objet de segmentation et stratégie de nouvelle tentative hello origine échec. 

Cet article fournit une vue d’ensemble des différentes fonctionnalités d’optimisation et des situations dans lesquelles les utiliser. Pour plus d’informations sur les fonctionnalités et limitations, voir les articles respectifs de hello sur chaque type d’optimisation individuels.

> [!NOTE]
> Votre **optimisé pour** options peuvent varier en fonction de fournisseur hello vous sélectionnez. Les fournisseurs CDN s’appliquent à des améliorations de différentes façons, selon le scénario de hello. 

## <a name="provider-options"></a>Options de fournisseur

Bonjour Azure Content Delivery Network à partir d’Akamai prend en charge :

* Livraison web générale 

* Diffusion multimédia en continu générale

* Diffusion multimédia en continu de vidéo à la demande

* Téléchargement de fichiers volumineux

* Accélération de site dynamique 

Hello Azure Content Delivery Network de Verizon prend en charge la diffusion sur le web général uniquement. Il peut être utilisé pour la vidéo à la demande et le téléchargement de fichiers volumineux. Vous n’avez tooselect un type d’optimisation.

Nous vous recommandons vivement de tester les variations de performances entre le fournisseur optimal de hello tooselect différents fournisseurs pour la remise de votre.

## <a name="select-and-configure-optimization-types"></a>Sélectionner et configurer les types d’optimisations

toocreate un nouveau point de terminaison, sélectionnez un type d’optimisation qui correspond le mieux à scénario de hello et type de contenu que vous souhaitez hello toodeliver de point de terminaison. **Remise de web général** est sélectionnée par défaut de hello. Vous pouvez mettre à jour option d’optimisation hello pour n’importe quel point de terminaison Akamai existant à tout moment. Cette modification n’interrompt pas la remise de hello CDN. 

1. Sélectionnez un point de terminaison dans un profil Standard Akamai.

    ![Sélection de point de terminaison ](./media/cdn-optimization-overview/01_Akamai.png)

2. Sous **PARAMÈTRES**, sélectionnez **Optimisation**. Sélectionnez un type de hello **optimisé pour** liste déroulante.

    ![Optimisation et sélection de type](./media/cdn-optimization-overview/02_Select.png)

## <a name="optimization-for-specific-scenarios"></a>Optimisation pour des scénarios spécifiques

Vous pouvez optimiser le point de terminaison CDN hello pour un des scénarios suivants de hello. 

### <a name="general-web-delivery"></a>Livraison web générale

La remise de web général est l’option d’optimisation courante hello. Elle est conçue pour l’optimisation de contenu web générale, par exemple, de pages web et d’applications web. Cette optimisation peut également être utilisée pour les téléchargements de fichiers et de vidéos.

Un site web classique contient du contenu statique et dynamique. Contenu statique inclut des images, des bibliothèques JavaScript et des feuilles de style qui peuvent être mis en cache et remis toodifferent utilisateurs. Le contenu dynamique est personnalisé pour un utilisateur individuel, telles que les annonces sont adaptés tooa profil d’utilisateur. Le contenu dynamique n’est pas mis en cache, car il est utilisateur tooeach uniques, telles que le contenu du panier d’achat. La livraison web générale peut optimiser votre site web tout entier. 

> [!NOTE]
> Si vous utilisez hello Azure Content Delivery Network à partir d’Akamai, vous pourriez toouse cette optimisation si votre taille de fichier moyenne est inférieure à 10 Mo. Si votre taille de fichier moyenne est supérieure à 10 Mo, sélectionnez **téléchargement de fichiers volumineux** de hello **optimisé pour** liste déroulante.

### <a name="general-media-streaming"></a>Diffusion multimédia en continu générale

Si vous avez besoin de point de terminaison toouse hello pour la diffusion en continu et la diffusion en continu de vidéo à la demande, nous vous recommandons d’optimisation de diffusion en continu de media général.

Diffusion multimédia en continu d’est sensible à la casse du temps, car les paquets qui arrivent en retard sur le client de hello peuvent entraîner une dégradation confort, telles que la mise en mémoire tampon fréquentes de contenu vidéo. L’optimisation de diffusion multimédia en continu réduit la latence hello de diffusion de contenu multimédia et fournit une expérience de diffusion en continu lisse pour les utilisateurs. 

Ce scénario est courant pour les clients du service multimédia Azure. Lorsque vous utilisez des services multimédias Azure, vous obtenez un point de terminaison de diffusion qui peut être utilisé pour la diffusion en continu en direct et à la demande. Avec ce scénario, les clients ne doivent tooswitch tooanother point de terminaison lorsqu’ils sont modifiés à partir de la diffusion en continu live tooon à la demande. L’optimisation de la diffusion multimédia en continu générale prend en charge ce type de scénario.

Bonjour Azure Content Delivery Network de Verizon utilise hello web général remise optimisation type toodeliver diffusion de contenu multimédia.

toolearn en savoir plus sur le support de diffusion en continu de l’optimisation, consultez [l’optimisation de diffusion multimédia en continu](cdn-media-streaming-optimization.md).

### <a name="video-on-demand-media-streaming"></a>Diffusion multimédia en continu de vidéo à la demande

L’optimisation de la diffusion multimédia en continu de vidéo à la demande améliore le contenu de diffusion en continu de vidéo à la demande. Si vous utilisez un point de terminaison de diffusion en continu de vidéo à la demande, vous pourriez toouse cette option.

Bonjour Azure Content Delivery Network de Verizon utilise hello web général remise optimisation type toodeliver diffusion de contenu multimédia.

toolearn en savoir plus sur le support de diffusion en continu de l’optimisation, consultez [l’optimisation de diffusion multimédia en continu](cdn-media-streaming-optimization.md).

> [!NOTE]
> Si le point de terminaison hello sert principalement le contenu de la vidéo à la demande, utilisez ce type d’optimisation. Hello principale différence entre cette optimisation et optimisation de diffusion en continu de media général hello est le délai de nouvelle tentative de connexion hello. délai d’attente Hello est beaucoup plus court toowork avec des scénarios de diffusion en continu en direct.

### <a name="large-file-download"></a>Téléchargement de fichiers volumineux

Si vous utilisez hello Azure Content Delivery Network à partir d’Akamai, vous devez utiliser des fichiers de toodeliver du téléchargement d’un fichier volumineux plus 1,8 Go. Bonjour Azure Content Delivery Network de Verizon n’a pas une limitation sur le fichier de taille de l’optimisation de la remise général web de téléchargement.

Si vous utilisez hello Azure Content Delivery Network, à partir d’Akamai, les téléchargements de fichiers volumineux sont optimisés pour contenu supérieur à 10 Mo. Si la taille de votre fichier moyenne est inférieure à 10 Mo, vous pourriez diffusion sur le web général toouse. Si la taille de vos fichiers moyenne est constamment supérieure à 10 Mo, il peut être plus efficace toocreate un point de terminaison distinct pour les fichiers volumineux. Par exemple, les mises à jour de microprogrammes ou de logiciels sont généralement des fichiers volumineux.

Bonjour Azure Content Delivery Network de Verizon utilise hello web général remise optimisation type toodeliver diffusion de contenu multimédia.

toolearn en savoir plus sur l’optimisation d’un fichier volumineux, consultez [optimisation des fichiers volumineux](cdn-large-file-optimization.md).

### <a name="dynamic-site-acceleration"></a>Accélération de site dynamique

 L’accélération de site dynamique est disponible à partir de profils de réseau de distribution de contenu Akamai et Verizon. Cette optimisation implique un toouse de frais supplémentaires. Pour plus d’informations, consultez hello page de tarification.

Accélération de site dynamique inclut diverses techniques qui bénéficient d’une latence hello et les performances du contenu dynamique. Ces techniques incluent l’optimisation d’itinéraire et de réseau, l’optimisation TCP, et bien plus. 

Vous pouvez utiliser cette tooaccelerate d’optimisation de l’application web qui inclut de nombreuses réponses ne sont pas mis en cache. Les résultats de recherche, les transactions de validation ou les données en temps réel en sont des exemples. Vous pouvez continuer toouse CDN mise en cache les fonctionnalités principales pour les données statiques. 



