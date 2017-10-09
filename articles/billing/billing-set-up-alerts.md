---
title: "aaaSet des alertes de facturation ou crédit pour les abonnements Azure | Documents Microsoft"
description: Describes how you can set up alerts on your Azure bill so you can avoid billing surprises.
keywords: "alerte de crédit, alerte de facturation"
services: 
documentationcenter: 
author: vikdesai
manager: tonguyen
editor: 
tags: billing
ms.assetid: 9b7b3eeb-cd9d-4690-86a3-51b1e2a8974f
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: vikdesai
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 711b9c72c59874792b0e229cdc5ec0fa517c24c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-billing-or-credit-alerts-for-your-microsoft-azure-subscriptions"></a>Configurer des alertes de facturation ou de crédit pour vos abonnements Microsoft Azure
Si vous êtes hello Admin. compte pour un abonnement Azure, vous pouvez utiliser hello Azure facturation Service d’alerte facturation de toocreate personnalisé des alertes qui vous aident à surveillez et gérez l’activité de facturation pour vos comptes Azure.

Ce service est en version préliminaire, donc vous devez tooenable il dans la page des fonctionnalités en version préliminaire hello tout d’abord.

## <a name="set-hello-alert-threshold-and-email-recipients"></a>Définir les destinataires de messagerie et le seuil d’alerte hello
1. Visitez [page des fonctionnalités en version préliminaire hello](https://account.windowsazure.com/PreviewFeatures) et activer **Service d’alerte de facturation**.

1. Une fois que vous recevez un e-mail de confirmation hello que le service de facturation hello est activé pour votre abonnement, visitez [page des abonnements hello](https://account.windowsazure.com/Subscriptions) dans le portail du compte hello. Cliquez sur votre choix toomonitor, puis cliquez sur l’abonnement hello **alertes**.

    ![Capture d’écran d’affichage d’abonnements hello du centre de compte Azure, des alertes en surbrillance][Image1]

2. Ensuite, cliquez sur **ajouter alertes** toocreate votre première application. Vous pouvez définir un total de cinq alertes de facturation par abonnement, un seuil propre et tootwo les destinataires de courrier électronique pour chaque alerte.

    ![Capture d’écran de hello affichage des alertes, où vous pouvez ajouter l’alerte][Image2]

3. Lorsque vous ajoutez une alerte, vous lui donnez un nom unique, choisissez un seuil de dépense, choisissez hello les adresses de messagerie où les alertes sont envoyées. Lorsque vous configurez le seuil de hello, vous pouvez choisir un **Total de facturation** ou un **du crédit** de hello **alerte pour** liste. Pour un total de facturation, une alerte est envoyée lorsque les dépenses de l’abonnement de dépasse le seuil de hello. Pour un crédit monétaire, une alerte est envoyée lorsque les crédits monétaires descendent en dessous de la limite de hello. Les crédits monétaires s’appliquent généralement à tooFree des abonnements d’évaluation et de Visual Studio.

    ![Capture d’écran d’affichage d’alerte Ajout hello, dans laquelle vous pouvez configurer les destinataires][Image3]

Azure prend en charge n’importe quelle adresse de messagerie, mais ne vérifiez que les adresses de messagerie hello fonctionne, vérifiez donc attentivement les fautes de frappe.

## <a name="check-on-your-alerts"></a>Vérifier vos alertes
Après avoir défini des alertes, hello centre des comptes les répertorie et indique combien de plus, vous pouvez configurer des. Pour chaque alerte, vous consultez hello limite de date et heure de qu'envoi, s’il s’agit d’une alerte pour un Total de facturation ou crédit monétaire et hello que permet de paramétrer. format de date et d’heure Hello est 24 heures heure universelle coordonnée (UTC) et la date de hello est aaaa-mm-jj format. Cliquez sur hello plus se connecter à une alerte dans hello liste tooedit ou hello-Corbeille toodelete il.

## <a name="billing-alerts-for-enterprise-agreement-ea-customers"></a>Alertes de facturation pour les clients Contrat Entreprise
Les clients Contrat Entreprise (EA) peuvent recevoir des alertes pour chaque département pour une inscription en définissant des quotas de dépense. Consultez [Quotas de service de dépense](https://ea.azure.com/helpdocs/departmentSpendingQuotas) dans les tooget portail EA hello a démarré.

## <a name="learn-more-about-azure-cost-management"></a>En savoir plus sur la gestion des coûts dans Azure
- Estimer les coûts à l’aide de hello [calculatrice de prix](https://azure.microsoft.com/pricing/calculator/), [coût total de l’outil de calcul de la propriété](https://aka.ms/azure-tco-calculator), et lorsque vous ajoutez un service.
- [Passez en revue régulièrement votre utilisation et vos coûts dans le portail Azure](billing-getting-started.md#costs).
- Activez les [Recommandations de coûts du conseiller Azure](../advisor/advisor-cost-recommendations.md).

toolearn, voir [conseils sur la gestion des coûts Azure](billing-getting-started.md).

[Image1]: ./media/azure-billing-set-up-alerts/billingalert1.png 
[Image2]: ./media/azure-billing-set-up-alerts/billingalert2.png
[Image3]: ./media/azure-billing-set-up-alerts/billingalerts3.png 
