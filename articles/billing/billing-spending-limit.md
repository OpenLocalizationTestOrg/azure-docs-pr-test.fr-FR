---
title: "limiter les aaaUnderstand de dépense Azure | Documents Microsoft"
description: "Décrit comment fonctionne de limite de dépense Azure et tooremove il"
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: genli
ms.openlocfilehash: ed01401a07c3d0e7edebe42fb1482b7b60b1df51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-spending-limit-and-how-tooremove-it"></a>Comprendre la limite de dépense Azure et comment tooremove il

La limite de dépense d’Azure est une limite sur l’utilisation de votre abonnement Azure. Tous les nouveaux clients qui s’inscrivent pour hello d’évaluation ou les offres qui comprend des crédits sur plusieurs mois ont hello activé par défaut de limite de dépense. limite de dépense de Hello est $0. Elle ne peut pas être modifiée. Hello limite de dépense n’est pas disponible pour les types d’abonnement tels que les abonnements de paiement à l’utilisation et les plans de l’engagement. Consultez hello [la liste complète des offres Azure et disponibilité hello Hello limite de dépense](https://azure.microsoft.com/support/legal/offer-details/).

## <a name="what-happens-when-i-reach-hello-spending-limit"></a>Que se passe-t-il lorsque j’atteignent la limite de dépense de hello ?

Lorsque votre utilisation entraîne des frais d’échappement mensuel hello inclus dans votre offre, services hello que vous avez déployés sont désactivées pour rest hello de ce mois de facturation. Par exemple, si vous avez déployé des services cloud, ces services sont retirés de la production et vos machines virtuelles Azure sont arrêtées et désallouées. tooprevent vos services d’être désactivé, vous pouvez choisir tooremove votre limite de dépense. Lorsque vos services sont désactivés, données hello dans vos comptes de stockage et les bases de données sont disponibles de manière pour les administrateurs en lecture seule. Hello début Hello mois de facturation suivant, si votre offre comprend des crédits sur plusieurs mois, votre abonnement sera réactivée. Vous pouvez redéployer vos Services Cloud et avoir des bases de données et les comptes de stockage tooyour un accès complet.

Une fois que la version d’évaluation gratuite hello atteint la limite de dépense de hello, vous pouvez réactiver les abonnements hello et automatiquement [offre de paiement à l’utilisation standard de mise à niveau tooour](billing-upgrade-azure-subscription.md) dans les 90 jours.

Pour recevoir des notifications lorsque vous atteignez la limite de dépense de votre offre de hello. Ouvrez une session sur toohello [centre des comptes Azure](https://account.windowsazure.com), sélectionnez **compte**, puis sélectionnez **abonnements**. Vous voyez des notifications concernant les abonnements qui ont atteint hello limite de dépense.

## <a name="things-you-are-charged-for-even-if-you-have-a-spending-limit-enabled"></a>Éléments faisant l’objet d’une facturation même si une limite de dépense est fixée

Certains services Azure et [achats sur le Marketplace](https://azure.microsoft.com/marketplace/) peut entraîner une baisse des frais sous le mode de paiement hello (CC) même si une limite de dépense est définie. Les licences de Visual studio, Azure Active Directory premium, plans de support et la plupart des tiers qui marquée services vendus par hello Marketplace sont des exemples.


## <a name="when-not-toouse-hello-spending-limit"></a>Lorsque toouse pas hello limite de dépense

limite de dépense de Hello pourrait vous empêcher de déployer ou à l’aide de certains services Microsoft et marché. Voici les scénarios hello où vous devez supprimer hello limite de dépense de votre abonnement.

- Vous envisagez de toodeploy les premières images tiers comme Oracle et des services tels que Visual Studio Team Services. Ce scénario vous oblige à tooexceed votre limite de dépense presque immédiatement et provoque le votre toobe abonnement désactivé.

- Vous avez des services dont le fonctionnement ne peut pas être interrompu.

- Les services et ressources avec des paramètres tels que des adresses IP virtuelles que vous ne souhaitez pas toolose. Ces paramètres sont perdus lorsque hello services et ressources sont libérées.


## <a name="remove-hello-spending-limit"></a>Supprimer la limite de dépense de hello

Vous pouvez supprimer hello plafond tant qu’il existe une méthode de paiement valide associée à votre abonnement à tout moment. Pour les offres qui ont un crédit sur plusieurs mois, vous pouvez réactiver également hello limite de dépense au début de hello de votre prochain cycle de facturation.

tooremove vos dépenses limiter, procédez comme suit :

1. Ouvrez une session sur toohello [centre des comptes Azure](https://account.windowsazure.com).

2. Sélectionnez un abonnement.

3. Si l’abonnement hello est désactivé en raison toohello limite de dépense soit atteinte, cliquez sur cette notification : « Abonnement a atteint la limite de dépense de hello et a été désactivé tooprevent frais ». Sinon, cliquez sur **supprimer limite de dépense** Bonjour **état de l’abonnement** zone.

4. Sélectionnez une option adaptée à votre situation.

|Option|Résultat|
|-------|-----|
|Supprimer la limite de dépense pour une durée indéterminée|Supprime la limite de dépense sans l’activer automatiquement au démarrage de hello Hello prochaine période de facturation de hello.|
|Supprimer la limite de dépense pour hello en cours de période de facturation|Supprime la limite de dépense afin qu’il active la précédent automatiquement au démarrage de hello Hello prochaine période de facturation de hello.|

## <a name="need-help-contact-support"></a>Vous avez besoin d’aide ? Contactez le support technique.
Si vous avez besoin d’aide, [contactez le support technique](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget votre problème résolu rapidement.
