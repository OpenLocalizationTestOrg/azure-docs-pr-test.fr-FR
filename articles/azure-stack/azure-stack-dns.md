---
title: aaaDNS dans la pile de Azure | Documents Microsoft
description: DNS dans Azure Stack
services: azure-stack
documentationcenter: 
author: ScottNapolitan
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/27/2017
ms.author: victorh
ms.openlocfilehash: 8620178833ac29e9653cce332b7c5d89bbdea0af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="dns-in-azure-stack"></a>DNS dans Azure Stack
Pile Azure inclut hello suivant les fonctionnalités DNS :
* Prise en charge de la résolution de nom d’hôte DNS
* Création et gestion des enregistrements et zones DNS à l’aide d’API

## <a name="support-for-dns-hostname-resolution"></a>Prise en charge de la résolution de nom d’hôte DNS
Vous pouvez spécifier une étiquette de nom de domaine DNS pour une ressource IP publique, qui crée un mappage pour *domainnamelabel.location*. cloudapp.azurestack.external toohello adresse IP publique Bonjour Azure pile géré des serveurs DNS.  

Par exemple, si vous créez une ressource IP publique avec **contoso** en tant qu’étiquette de nom de domaine Bonjour emplacement de pile Azure locale, hello le nom de domaine complet (FQDN) **contoso.local.cloudapp.azurestack.external** résout l’adresse IP publique de toohello de ressource de hello. Vous pouvez utiliser ce nom de domaine complet de toocreate un enregistrement CNAME qui pointe l’adresse IP publique de toohello dans la pile de Azure de domaine personnalisé.

> [!IMPORTANT]
> Chaque étiquette de nom de domaine créée doit être unique dans son emplacement Azure Stack.

Si vous créez des adresse IP publique hello à l’aide du portail de hello, il ressemble à ceci :

![Création d’une adresse IP publique](media/azure-stack-whats-new-dns/image01.png)

Cette configuration est utile si vous souhaitez tooassociate une adresse IP publique avec une ressource à charge équilibrée. Par exemple, vous pouvez avoir un équilibreur de charge traitant les demandes à partir d’une application web. Derrière la charge de hello équilibrage de charge est un site web situé sur un ou plusieurs ordinateurs virtuels. Désormais, vous pouvez accéder hello le site web avec équilibrage de charge par un nom DNS, plutôt que par une adresse IP.

## <a name="create-and-manage-dns-zones-and-records-using-api"></a>Créer et gérer des enregistrements et zones DNS à l’aide d’API
Vous pouvez créer et gérer des enregistrements et des zones DNS dans Azure Stack.  

Azure Stack fournit un service DNS comme celui d’Azure, à l’aide d’API qui sont cohérentes avec les API DNS Azure.  En hébergeant vos domaines dans Azure pile DNS, vous pouvez gérer vos enregistrements DNS avec hello même informations d’identification, API, outils, la facturation et la prise en charge en tant que vos autres services Azure. 

Pour des raisons évidentes, infrastructure de DNS de pile Azure hello est plus compact que d’Azure. Par conséquent, hello étendue, l’échelle et les performances dépendent de montée en puissance hello du déploiement d’Azure pile hello et environnement hello où il est déployé.  Par conséquent, des éléments tels que les performances, la disponibilité, la distribution globale et haute disponibilité (HA) peuvent varier de déploiement toodeployment.

## <a name="comparison-with-azure-dns"></a>Comparaison avec le système DNS Azure
DNS dans la pile de Azure est semblable tooDNS dans Azure, avec deux exceptions majeures :
* **Il ne prend pas en charge les enregistrements AAAA**

    Azure Stack ne prend pas en charge les enregistrements AAAA, car il ne prend pas en charge les adresses IPv6.  Il s’agit d’une différence essentielle entre les systèmes DNS Azure et Azure Stack.
* **Il n’est pas multilocataire**

    Contrairement à Azure, hello Service DNS dans la pile de Azure n’est pas multilocataire. Afin que chaque client ne peut pas créer hello même zone DNS. Uniquement hello premier abonnement qui tente de zone de hello toocreate réussit, et les requêtes suivantes échouent.  Il s’agit d’un problème connu et d’une différence essentielle entre le système DNS dans Azure et dans Azure Stack. Ce problème sera résolu dans une version ultérieure.

En outre, il existe des différences mineures dans la façon dont le système DNS Azure Stack implémente les balises, les métadonnées, les ETags et les limites.

Bonjour informations suivantes s’applique spécifiquement tooAzure DNS de la pile et varient légèrement d’Azure DNS. toolearn en savoir plus sur Azure DNS, consultez [DNS zones et enregistrements](../dns/dns-zones-records.md) au site de documentation de Microsoft Azure hello.

### <a name="tags-metadata-and-etags"></a>Balises, métadonnées et ETags

**Balises**

Le système DNS Azure Stack prend en charge l’utilisation de balises Azure Resource Manager sur des ressources de zone DNS. Il ne prend pas en charge les balises sur les jeux d’enregistrements DNS, bien que l’alternative « métadonnées » soit prise en charge sur les jeux d’enregistrements DNS comme expliqué ci-dessous.

**Métadonnées**

Comme une alternative toorecord définie des balises, Azure pile DNS prend en charge annoter les jeux d’enregistrements à l’aide de 'metadata'. Tootags similaire, métadonnées permet de vous tooassociate paires nom-valeur avec chaque jeu d’enregistrements. Par exemple, cela peut être objectif de hello toorecord utile de chaque jeu d’enregistrements. Contrairement aux balises, les métadonnées ne peut pas être utilisé tooprovide une vue filtrée de votre facture Azure et ne peut pas être spécifiée dans une stratégie Azure Resource Manager.

**ETags**

Supposons que deux personnes ou les deux processus essaient toomodify DNS de l’enregistrement par hello même temps. Lequel gagne ? Et le gagnant hello sait que leur avez remplacée modifications créées par quelqu'un d’autre ?

DNS de pile Azure utilise Etags toohandle modifications simultanées toohello même ressource en toute sécurité. Les ETags sont différents des « Balises » Azure Resource Manager. Chaque ressource DNS (zone ou jeu d’enregistrements) est associée à un Etag. Chaque fois qu’une ressource est récupérée, son Etag l’est également. Lors de la mise à jour d’une ressource, vous pouvez choisir toopass précédent hello Etag qui Azure pile DNS permet de vérifier que hello Etag correspond à serveur hello. Car chaque ressource tooa de mise à jour entraîne hello Etag à chaque fois, une non-correspondance d’Etag indique une modification simultanée s’est produite. ETag peut également être utilisé lors de la création d’un nouveau tooensure de ressources que les ressources hello n’existent pas déjà.

Par défaut, Azure pile DNS PowerShell utilise les Etags tooblock modifications simultanées toozones et jeux d’enregistrements. Hello facultatif *-remplacer* commutateur peut être utilisé toosuppress vérification Etag, auquel cas tout simultanées les modifications qui se sont produites sont remplacées.

Au niveau de hello Hello API REST de Azure pile DNS, les Etags sont spécifiés à l’aide d’en-têtes HTTP. Leur comportement est donné dans hello tableau suivant :

| En-tête | Comportement|
|--------|---------|
| Aucun   | PUT réussit toujours (aucune vérification Etag)|
| If-match| PUT ne réussit que si la ressource existe et que l’Etag correspond|
| If-match *| PUT réussit seulement si la ressource existe|
| If-none-match *| PUT réussit seulement si la ressource n’existe pas|

### <a name="limits"></a>limites

Hello suivant les limites par défaut s’appliquent lorsque vous utilisez Azure pile DNS :

| Ressource| Limite par défaut|
|---------|--------------|
| Zones par abonnement| 100|
| Jeux d’enregistrements par zone| 5 000|
| Enregistrements par jeu d’enregistrements| 20|

## <a name="next-steps"></a>Étapes suivantes
[Introduction aux noms de domaine internationaux (IDN) pour Azure Stack](azure-stack-understanding-dns.md)
