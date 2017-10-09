---
title: aaaDeploy votre toohello offre Azure Marketplace | Documents Microsoft
description: "En savoir plus sur et suivre les étapes hello instructions toodeploy votre offre--l’image de machine virtuelle, le service de développeur, service de données, etc.--toohello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 8f79b891-84e2-4f41-ba0d-66420e2c6b2e
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2016
ms.author: hascipio
ms.openlocfilehash: ab0bb7c78020187505c2d5f09c4de246987ecd97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-offer-toohello-azure-marketplace"></a>Déployer votre toohello offre Azure Marketplace
Lorsque vous êtes satisfait de votre offre (autrement dit, vous avez testé les scénarios clients, marketing contenu, etc.) et que vous êtes prêt toolaunch, demande **Push tooproduction** sur hello **publier** onglet.  

1. Hello quatre étapes sous la page de procédure pas à pas hello Bonjour portail de publication doit être effectuée et vert. Pour les offres d’ordinateur virtuel, vérifiez que hello suivant les instructions sont suivies.
   
    ![dessin][img-pubportal-walkthru-checked]
2. Sélectionnez hello **publier** onglet à partir de la liste hello sur hello côté gauche.
   
    ![dessin][img-pubportal-menu-publish]
3. Cliquez sur le bouton de hello **demander l’approbation toopush tooproduction**. Une fois hello demande est faite, équipe d’approbation hello exécute une vérification finale, et ensuite votre offre sera disponible Bonjour Azure Marketplace.
   
    ![dessin][img-pubportal-publish-pushproduction]

> [!IMPORTANT]
> En cas de Machines virtuelles, lorsque vous cliquez sur hello bouton demande l’approbation toopush tooproduction, hello suit derrière la scène de hello est effectuée. Vous serez tooview en mesure de hello progression de chaque étape sous l’onglet Publier de hello Bonjour portail de publication. Vous devez vérifier cette page à intervalle régulier (jusqu'à ce que l’état de hello affiche « Liste ») pour toutes les informations d’échec qui ont besoin de correction à partir de votre principal.
> 
> * Dans un premier temps votre demande de production passe équipe certification toohello est chargée de valider le disque dur virtuel hello. Toutefois, si vous mettez à jour votre offre déjà répertoriée et demande de hello a marketing uniquement les modifications, puis hello certification étape est ignorée.
> * À l’étape suivante de hello, demande de hello provenir toohello validation du contenu équipe vérifier hello marketing du contenu de l’offre de hello.
> * Si hello étapes ci-dessus est réussie, offre de hello est approuvé en production. À ce stade, l’état hello deviennent « répertorié » dans le portail de publication hello. Toutefois, cet état de la « Liste » n’implique pas que les processus hello est terminé. Hello suivant les étapes toobe de besoin se termine avant l’offre de hello est disponible dans hello Azure Marketplace.
> * Une fois que l’offre de hello est approuvé en production à l’étape hello ci-dessus, la réplication de début offre de hello pour tous les hello centres de données Azure. En règle générale, il prend 24-48hours pour hello réplication toocomplete mais peut prendre jusqu'à une semaine tooa selon la taille de hello du disque dur virtuel hello. Toutefois, si vous mettez à jour votre offre déjà répertoriée et il a marketing uniquement les modifications, la réplication hello est plus rapide.
> * Lorsque la réplication hello est terminée, puis offre de hello sera disponible Bonjour Azure Marketplace.
> 
> Vous pouvez toujours supprimer une offre de hello alors qu’il est dans un **brouillon** état (par exemple, jamais **Push toostaging** ou **Push tooproduction**). Sur hello **historique** , cliquez sur hello **supprimer le brouillon** bouton bas hello hello page toodelete un brouillon.
> 
> 

## <a name="production-checklist-for-all-virtual-machine-offers"></a>Liste de contrôle de production pour toutes les offres de machines virtuelles
* Assurez-vous que vous avez le statut de partenaire Microsoft Azure Certified
* Sous l’onglet Références (SKU) de hello, option de hello « masquer cette référence SKU de hello Marketplace, car il doit toujours être acheté via un modèle de solution » doit être marqué comme Oui uniquement si hello référence (SKU) fait partie d’un modèle de Solution. Dans tous les hello autres cas, cette option doit toujours être marquée comme étant non.
* N’oubliez pas : Vous ne devez pas modifier hello SKU visibilité paramètre une fois hello référence (SKU) est répertorié. Nous ne prenons pas en charge cette fonctionnalité.
* Assurez-vous que les logos hello respectent les instructions du logo Azure Marketplace toohello répertoriées ci-dessous.
* La description de l’offre et celle de la référence ne peuvent pas être les mêmes.
* Le titre de la référence et le résumé long de l’offre ne peuvent pas être les mêmes.
* Le titre de la référence et le résumé de l’offre ne peuvent pas être les mêmes.
* Les titres de référence ne peuvent pas être les mêmes pour une offre avec plusieurs références.

**Instructions relatives aux logos Azure Marketplace**

* Hello conception Azure a une palette de couleurs simple. Limiter nombre hello principale et les couleurs de base de données secondaire sur votre logo.
* couleurs du thème Hello Hello portail Azure sont blancs et noir. Par conséquent, évitez d’utiliser ces couleurs comme couleur d’arrière-plan hello de vos logos. Utiliser des couleurs qui rendent vos logos dans hello portail Azure. Nous vous recommandons d’utiliser des couleurs primaires simples. Si vous utilisez un arrière-plan transparent, vérifiez que le logo/texte hello n’est pas blanc ou noir.
* N’utilisez pas un arrière-plan dégradé sur le logo de hello.
* Éviter de placer le texte, même votre entreprise ou le nom de marque, sur le logo de hello.
* Hello apparence de votre logo doit être « plat » et évitez de dégradés.
* logo de Hello ne doit pas être étirée.

**Recommandations supplémentaires pour le logo de héros hello :**

* logo de héros Hello est facultative. serveur de publication Hello peut choisir tooupload pas un logo héros. **Icône de héros hello toutefois une fois chargées, ne peut pas être supprimé hello portail de publication. À ce stade, les partenaires hello doivent respecter les règles de Azure Marketplace de hello pour les icônes de héros autre offre de hello ne sera pas tooproduction approuvée.**
* Hello nom complet de l’éditeur, hello et titre de référence (SKU) offrent résumé long s’affichent dans la couleur de police blanc. Par conséquent, vous devez éviter de conservation de n’importe quelle couleur clair en arrière-plan hello Hello héros d’icône. Les arrière-plans noirs, blancs et transparents ne sont pas autorisés pour les icônes.
* Hello nom complet du serveur de publication, titre de référence (SKU), offre hello résumée et hello bouton créent sont incorporés par programmation à l’intérieur du logo de héros hello une fois que l’offre de hello est répertorié. Par conséquent, vous devez entrer un texte lors de la création d’un logo de héros hello. Laissez espace vide à droite de hello, car le texte hello (nom de l’éditeur, titre de référence (SKU), offre hello résumée) est incluse par programme en nous là. espace vide Hello texte hello doit être 415 x 100 sur hello droit (et elle est décalée par 370px de hello gauche).

## <a name="additional-production-checklist-for-already-listed-virtual-machine-offers"></a>Liste de contrôle de production supplémentaire pour les offres de machines virtuelles déjà répertoriées
* Vérifiez que s’il existe déjà une offre avec hello même offrent un nom de votre société. Si Oui, vous devez ajouter une nouvelle version de référence (SKU) de hello dans offre existante de hello au lieu de créer une nouvelle offre en double.
* Disque de données ne doit pas changer entre deux versions de hello même référence (SKU).
* Bonjour Azure Marketplace ne prend pas en charge la tarification de modification de hello répertoriés références (SKU) car il affecte la facturation de clients existants de hello hello. Assurez-vous que vous ne modifiez pas hello tarification des références SKU de hello répertorié dans les régions hello où hello référence (SKU) est disponible. Toutefois, vous pouvez ajouter de nouvelles références SKU ou ajouter des nouvelles régions tooan existant de référence (SKU).

## <a name="next-steps"></a>Étapes suivantes
Une fois que l’offre de hello est dynamique, tester hello client scénarios toovalidate que tous les contrats de hello et fonctionnent correctement dans un environnement de production hello comme environnement de mise en lots hello testées et validées dans.

## <a name="see-also"></a>Voir aussi
* [Mise en route : comment toopublish une toohello offre Azure Marketplace](marketplace-publishing-getting-started.md)

[img-pubportal-walkthru-checked]:media/marketplace-publishing-push-to-production/pubportal-walkthru-checked.png
[img-pubportal-menu-publish]:media/marketplace-publishing-push-to-production/pubportal-menu-publish.png
[img-pubportal-publish-pushproduction]:media/marketplace-publishing-push-to-production/pubportal-publish-pushproduction.png
