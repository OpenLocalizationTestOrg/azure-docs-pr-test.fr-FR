---
title: "objets BLOB aaaUsing hello Azure CDN tooaccess avec des domaines personnalisés via HTTPS"
description: "Découvrez comment toointegrate hello CDN Azure avec tooaccess de stockage d’objets blob objets BLOB avec des domaines personnalisés via HTTPS"
services: storage
documentationcenter: 
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: mihauss
ms.openlocfilehash: 678e24a7dde5cb2f8feea177bb47c92f61035e66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cdn-tooaccess-blobs-with-custom-domains-over-https"></a>Avec des objets BLOB de hello Azure CDN tooaccess avec des domaines personnalisés via HTTPS

Le réseau de distribution de contenu (CDN) Azure prend désormais en charge le protocole HTTPS pour les noms de domaine personnalisés.
Vous pouvez tirer parti de cette fonctionnalité tooaccess objets BLOB de stockage à l’aide de votre domaine personnalisé via le protocole HTTPS. toodo par conséquent, vous devez tout d’abord tooenable Azure CDN sur votre objet blob point de terminaison et mapper hello CDN tooa nom de domaine personnalisé. Une fois ces étapes, l’activation de HTTPS pour votre domaine personnalisé est simplifié via l’activation en un clic, la gestion des certificats terminée et toutes les données avec aucun coût supplémentaire toonormal la tarification CDN.

Cette possibilité est importante, car elle permet la confidentialité hello tooprotect et l’intégrité des données de vos données d’application web sensibles lors de leur transit. À l’aide de hello SSL protocole tooserve le trafic via HTTPS garantit que les données sont chiffrées lorsqu’elles sont envoyées sur hello internet. Le protocole HTTPS assure la confiance et l’authentification, et protège également vos applications web contre les attaques.

> [!NOTE]
> En outre tooproviding SSL prend en charge pour les noms de domaine personnalisé, hello CDN Azure peut vous aider à faire évoluer votre contenu haut débit d’application toodeliver monde hello.
> toolearn plus, consultez [vue d’ensemble de hello Azure CDN](../cdn/cdn-overview.md).
>
>

## <a name="quick-start"></a>Démarrage rapide

Il s’agit hello étapes requises tooenable HTTPS pour votre point de terminaison de stockage personnalisé d’objet blob :

1.  [Intégrer un compte de stockage Azure au CDN Azure](../cdn/cdn-create-a-storage-account-with-cdn.md).
    Cet article vous guide tout au long de la création d’un compte de stockage Bonjour portail Azure si vous n'avez pas déjà fait.
2.  [Domaine personnalisé de carte Azure CDN contenu tooa](../cdn/cdn-map-content-to-custom-domain.md).
3.  [Activer le protocole HTTPS sur un domaine personnalisé CDN Azure](../cdn/cdn-custom-ssl.md).

## <a name="shared-access-signatures"></a>Les signatures d’accès partagé

Si votre point de terminaison de stockage d’objets blob est toodisallow configuré l’accès en lecture anonyme, vous devez tooprovide une [Signature d’accès partagé (SAS)](storage-dotnet-shared-access-signature-part-1.md) dans chaque demande d’émission de jeton que vous apportez tooyour des domaines personnalisés. Par défaut, les points de terminaison de stockage d’objets blob interdisent l’accès en lecture anonyme. Consultez [Gestion de l’accès en lecture anonyme aux conteneurs et aux objets blob](storage-manage-access-to-resources.md) pour en savoir plus sur les signatures d’accès partagé.

CDN Azure ne respecte pas les jetons SAS restrictions toohello ajouté. Par exemple, tous les jetons SAP ont un délai d’expiration. Cela signifie que le contenu peut toujours être accessible avec une SAP expirée jusqu'à ce que ce contenu est purgé de noeuds hello CDN. Vous pouvez contrôler la durée pendant laquelle données mises en cache sur hello CDN en définissant les en-tête de réponse de la mémoire cache de hello. Consultez la rubrique [Gérer l’expiration des objets blob de stockage Azure dans CDN Azure](../cdn/cdn-manage-expiration-of-blob-content.md) pour plus d’informations.

Si vous créez plusieurs URL de SAP pour hello même point de terminaison des objets blob, nous vous recommandons d’activation de mise en cache de chaîne de requête pour votre CDN Azure. Il s’agit de tooensure chaque URL traitée comme une entité unique. Pour plus d’informations, consultez [Contrôle du comportement de mise en cache du CDN Azure avec des chaînes de requête](../cdn/cdn-query-string.md).

## <a name="http-toohttps-redirection"></a>Redirection de tooHTTPS HTTP

Vous pouvez choisir tooHTTPS de trafic HTTP tooredirect. Cela requiert l’utilisation de l’offre de premium d’Azure CDN hello de Verizon. Vous devez trop[comportement de remplacer le HTTP à l’aide du moteur de règles d’Azure CDN](../cdn/cdn-rules-engine.md) avec la règle suivante :

![](./media/storage-https-custom-domain-cdn/redirect-to-https.png)

« Nom de point de terminaison Cdn » fait référence à toohello nom que vous avez configuré pour votre point de terminaison CDN. Vous pouvez sélectionner cette valeur à partir de la liste déroulante de hello. « Chemin d’origine » fait référence au chemin d’accès de hello dans votre compte de stockage d’origine où se trouve votre contenu statique.
Si vous hébergez tout le contenu statique dans un conteneur unique, remplacez « chemin d’origine » nom hello de ce conteneur.

Pour approfondir les règles, consultez hello [fonctionnalités du moteur de règles d’Azure CDN](../cdn/cdn-rules-engine-reference-features.md).

## <a name="pricing-and-billing"></a>Tarification et facturation

Lorsque vous accédez à des objets BLOB via un CDN Azure, vous payez [coûts du stockage d’objets Blob](https://azure.microsoft.com/pricing/details/storage/blobs/) pour le trafic entre les noeuds hello et l’origine de hello (stockage d’objets Blob), et [prix CDN](https://azure.microsoft.com/pricing/details/cdn/) pour les données accédées à partir des noeuds hello.

Par exemple, supposons que vous avez un compte de stockage dans l’ouest des États-Unis qui est accessible via un CDN Azure. Si une personne de hello du Royaume-Uni tente tooaccess d'entre hello des objets BLOB dans ce compte de stockage via hello CDN, Azure vérifie d’abord hello nœud le plus proche de hello du Royaume-Uni pour cet objet blob. Si trouvé, il accède à cette copie de l’objet blob de hello et utilisera la tarification CDN, car il est accessible sur hello CDN. Si la valeur n’est pas trouvée, Azure copie hello blob toohello nœud de périmètre, ce qui entraîne une sortie et des frais de transaction comme spécifié dans hello tarification du stockage d’objets Blob, puis accéder au fichier hello sur le nœud de périmètre hello, ce qui entraîne la facturation CDN.

Lorsque vous examinez hello [CDN page de tarification](https://azure.microsoft.com/pricing/details/cdn/), notez que HTTPS prennent en charge pour les noms de domaine personnalisé est uniquement disponible pour Azure CDN Verizon produits (Standard ou Premium).

## <a name="next-steps"></a>Étapes suivantes

[Configurer un nom de domaine personnalisé pour un point de terminaison de stockage Blob](storage-custom-domain-name.md)
