---
title: "aaaUnderstand votre Azure détaillées d’utilisation | Documents Microsoft"
description: "Découvrez comment tooread et comprendre les sections hello votre détaillée d’utilisation de volumes partagés de cluster pour votre abonnement Azure"
services: 
documentationcenter: 
author: tonguyen10
manager: tonguyen
editor: 
tags: billing
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: tonguyen
ms.openlocfilehash: c9284bf94bfa9f36cdd5d39e653a35def7c1aa34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-terms-on-your-microsoft-azure-detailed-usage-charges"></a>Comprendre les termes figurant sur le fichier détaillant les frais d’utilisation Microsoft Azure 
Hello d’utilisation détaillées fichier CSV de frais contient tous les jours et les frais d’utilisation de niveau de compteur pour hello en cours de période de facturation. 

tooget votre fichier d’utilisation détaillées, consultez [comment tooget votre facturation Azure facture et les données d’utilisation quotidienne](billing-download-azure-invoice-daily-usage-date.md).
Il est disponible au format .csv, que vous pouvez ouvrir dans une application de feuille de calcul. Si deux versions sont disponibles, téléchargez la version 2. Qui est le format de fichier hello plus récente.

Frais d’utilisation sont hello total **mensuel** frais sur un abonnement. Les frais d’utilisation ne prennent pas en compte les crédits et les remises.

## <a name="detailed-terms-and-descriptions-of-your-detailed-usage-file"></a>Termes et descriptions détaillés de votre fichier sur l’utilisation détaillée
Hello sections suivantes décrivent les termes importants hello indiqués dans la version 2 du fichier d’utilisation détaillées de hello.

### <a name="statement"></a>Instruction
section supérieure de Hello Hello détaillée l’utilisation des volumes partagés de cluster affiche hello services de fichiers que vous avez utilisé pendant la période de facturation du mois hello. Hello tableau suivant répertorie les termes du contrat de hello et descriptions présentées dans cette section.

| Terme | Description |
| --- | --- |
|Période de facturation |période de facturation Hello lorsque les compteurs hello ont été utilisés |
|Catégorie du compteur |Identifie le service de niveau supérieur hello pour l’utilisation de hello |
|Sous-catégorie du compteur |Définit le type hello du service Azure qui peut affecter les taux de hello |
|Nom du compteur |Identifie l’unité de mesure pour le compteur hello consommé de hello |
|Région du compteur |Identifie l’emplacement hello de centre de données hello pour certains services dont le prix est basée sur l’emplacement du centre de données |
|SKU |Identifie l’identificateur système unique de hello pour chaque compteur Azure |
|Unité |Identifie hello unité service de hello est facturé en. Par exemple, Go, heures, 10 000 s. |
|Quantité consommée |quantité de Hello de compteur hello utilisé pendant la période de facturation hello |
|Quantité incluse |quantité de Hello de compteur de hello est incluse sans frais dans votre période de facturation actuelle |
|Quantité de dépassement |Affiche hello différence entre hello quantité consommée et hello inclus une quantité. Ce montant vous est facturé. Pour les offres de paiement à l’utilisation sans quantité inclus avec l’offre de hello, ce total est hello identique hello quantité consommée. |
|Au sein de l'engagement |Affiche les frais de compteur hello soustraites du montant de votre engagement associé à votre offre de 6 ou 12 mois. Les frais de compteur sont soustraits dans l’ordre chronologique. |
|Devise |devise de Hello utilisée dans votre période de facturation actuelle |
|Dépassement |Affiche les frais de compteur hello qui dépassent le montant de l’engagement associé à votre offre de 6 ou 12 mois |
|Taux d'engagement |Affiche le taux d’engagement hello basé sur le montant de l’engagement total hello associé à votre offre de 6 ou 12 mois |
|Tarif |taux de Hello que vous êtes facturé pour chaque unité facturable |
|Valeur |Montre le résultat hello Hello multipliant la colonne Quantity de dépassement par colonne de taux hello. Si hello que quantité consommée ne dépasse pas hello inclus une quantité, aucun frais n’est dans cette colonne. |

### <a name="daily-usage"></a>Utilisation quotidienne

Hello quotidienne section de l’utilisation d’un fichier CSV hello affiche les détails d’utilisation qui affectent les taux de facturation hello. Hello tableau suivant répertorie les termes du contrat de hello et descriptions présentées dans cette section.

| Terme | Description |
| --- | --- |
|Date d'utilisation |date de Hello lorsqu’un compteur de hello a été utilisé |
|Catégorie du compteur |Identifie le service de niveau supérieur hello pour lequel cette utilisation appartient |
|ID du compteur |Hello facturé identificateur compteur qui a utilisé l’utilisation de la facturation de tooprice |
|Sous-catégorie du compteur |Définit le type de service Azure hello qui peut affecter les taux de hello |
|Nom du compteur |Identifie l’unité de mesure pour le compteur hello consommé de hello |
|Région du compteur |Identifie l’emplacement hello de centre de données hello pour certains services dont le prix est basée sur l’emplacement du centre de données |
|Unité |Identifie les unités hello ce compteur hello est facturé en. Par exemple, Go, heures, 10 000 s. |
|Quantité consommée |quantité de Hello de compteur hello qui a été utilisé pour ce jour |
|Emplacement de la ressource |Identifie le centre de données hello où jauge de hello est en cours d’exécution |
|Service consommé |Hello service de plateforme Windows Azure que vous avez utilisé |
|Groupe de ressources |groupe de ressources Hello dans quel hello compteur déployé est en cours d’exécution dans. <br/><br/>Pour plus d’informations, consultez [Présentation d’Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview). |
|ID de l’instance | Identificateur Hello pour le compteur de hello. <br/><br/> identificateur de Hello contient nom hello que vous spécifiez pour le compteur de hello lors de sa création. Il s’agit soit nom hello de ressource de hello ou hello complet ID de ressource. Pour plus d’informations, consultez la page [API Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/resources). |
|Tags | Balise de vous attribuez toohello compteur. Utiliser des enregistrements de facturation toogroup balises.<br/><br/>Par exemple, vous pouvez utiliser des balises toodistribute coûts par département hello qui utilise le compteur de hello. Les services qui prennent en charge l’émission des balises sont des machines virtuelles, de stockage et les services réseau configurés à l’aide de hello [API Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/resources). Pour plus d’informations, voir [Organisation des ressources Azure à l’aide de balises](http://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/). |
|Informations supplémentaires |Métadonnées relatives au service. Par exemple, le type d’image d’une machine virtuelle. |
|Informations sur le service 1 |nom du projet Hello hello service appartient tooon votre abonnement |
|Informations sur le service 2 |Champ hérité capturant les métadonnées facultatives propres au service |

## <a name="how-do-i-make-sure-that-hello-charges-in-my-detailed-usage-file-are-correct"></a>Comment m’assurer que les frais de hello dans mon fichier d’utilisation détaillées sont corrects ?
Si vous voulez plus de détails sur des frais indiqués sur votre fichier sur l’utilisation détaillée, consultez [Comprendre votre facture Microsoft Azure.](./billing-understand-your-bill.md)

## <a name="external"></a>Quels sont les frais associés aux services externes ?
Les services externes (également appelés commandes de la Place de marché) sont fournis par les fournisseurs de services indépendants et sont facturés séparément. frais de Hello n’apparaissent pas sur hello facture Azure. toolearn, voir [comprendre vos frais de service externes Azure](billing-understand-your-azure-marketplace-charges.md).

## <a name="need-help-contact-support"></a>Vous avez besoin d’aide ? Contactez le support technique.
Si vous avez besoin d’aide, [contactez le support technique](https://portal.azure.com/?) pour obtenir une prise en charge rapide de votre problème.
