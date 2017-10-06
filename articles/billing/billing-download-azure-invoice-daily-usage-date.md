---
title: "aaaDownload Azure facturation facture et tous les jours les données d’utilisation | Documents Microsoft"
description: "Décrit comment toodownload ou afficher votre facturation Azure facture et les données d’utilisation quotidienne."
keywords: "facturation, facture, téléchargement de facture, facture Azure, utilisation d’Azure"
services: 
documentationcenter: 
author: genlin
manager: tonguyen
editor: 
tags: billing
ms.assetid: 6d568d1d-3bd6-4348-97d0-1098b5fe0661
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: genli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2826df10f39914fcaeb9985271dadde550c68dfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="download-or-view-your-azure-billing-invoice-and-daily-usage-data"></a>Télécharger ou afficher votre facture Azure et vos données d’utilisation quotidienne
Vous pouvez télécharger votre facture hello [portail Azure](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) ou envoyer par courrier électronique. toodownload votre utilisation quotidienne, l’accédez toohello [centre des comptes Azure](https://account.windowsazure.com). Seuls certains rôles ont tooget d’autorisation les informations de facturation et d’utilisation, comme hello administrateur de compte de facturation. toolearn savoir plus sur la mise en route d’accès toobilling plus d’informations, consultez [tooAzure d’accès de gérer à l’aide de rôles de facturation](billing-manage-access.md).

## <a name="get-your-invoice-in-email-pdf"></a>Obtenir votre facture par e-mail (.pdf)
Vous pouvez choisir et configurer des tooreceive des destinataires supplémentaires votre Azure facture dans un message électronique. Cette fonctionnalité n’est peut-être pas disponible pour certains abonnements tels que les offres de support, les contrats Entreprise ou Azure dans Open.

1. Sélectionnez votre abonnement à partir de hello [panneau d’abonnements](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade). Choisissez cette option pour chacun de vos abonnements. Cliquez sur **Factures** pour sélectionner **l’envoi de votre facture par E-mail**. 

    ![Capture d’écran hello acceptation de flux](./media/billing-download-azure-invoice-daily-usage-date/InvoicesDeepLink.PNG)
    
2. Cliquez sur **participer** et acceptez les termes du contrat de hello.

    ![Capture d’écran hello acceptation de flux](./media/billing-download-azure-invoice-daily-usage-date/InvoiceArticleStep2.PNG)
 
3. Une fois que vous avez accepté le contrat de hello, vous pouvez configurer des destinataires supplémentaires.

    ![Capture d’écran hello acceptation de flux](./media/billing-download-azure-invoice-daily-usage-date/InvoiceArticleStep3.PNG)
    
Si vous n’obtenez pas un message électronique après avoir suivi les étapes de hello, assurez-vous que votre adresse de messagerie est correcte dans hello [préférences de communication sur votre profil](https://account.windowsazure.com/profile).

## <a name="download-invoice-from-azure-portal-pdf"></a>Télécharger la facture à partir du portail Azure (.pdf)

1. Sélectionnez votre abonnement à partir de hello [panneau d’abonnements](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) dans le portail Azure en tant que [un utilisateur avec accès tooinvoices](billing-manage-access.md).

2. Sélectionnez **Factures**. 

    ![Capture d’écran qui affiche l’option de facturation et d’utilisation de hello](./media/billing-download-azure-invoice-daily-usage-date/billingandusage.png) 

3. Cliquez sur **télécharger la facture** tooview une copie de votre facture PDF. Si elle indique **non disponible**, consultez [pourquoi ne puis-je pas voir une facture pour hello dernière période de facturation ?](#noinvoice)

    ![Capture d’écran qui affiche les périodes de facturation, option de téléchargement hello et total des frais pour chaque période de facturation](./media/billing-download-azure-invoice-daily-usage-date/billing4.png)

4. Vous pouvez également consulter votre utilisation quotidienne en cliquant sur la période de facturation hello. 

Pour plus d’informations sur votre facture, consultez la page [Comprendre votre facture Microsoft Azure](billing-understand-your-bill.md). Pour obtenir de l’aide sur la gestion des coûts, consultez [Éviter les coûts inattendus avec la gestion de la facturation et des coûts dans Azure](billing-getting-started.md).

## <a name="download-usage-from-hello-account-center-csv"></a>Télécharger l’utilisation de hello centre des comptes (.csv)

1. L’authentification à hello [centre des comptes Azure](https://account.windowsazure.com/subscriptions) comme hello administrateur de compte.

2. Sélectionnez l’abonnement hello pour lequel vous souhaitez des informations de facturation et d’utilisation hello.

3. Sélectionnez **HISTORIQUE DE FACTURATION**. 

    ![Capture d’écran qui montre l’option d’historique de facturation](./media/billing-download-azure-invoice-daily-usage-date/Billinghisotry.png)

4. Vous pouvez voir vos instructions pour hello dernières périodes de facturation six et hello non facturés période en cours. 

    ![Capture d’écran qui affiche les périodes de facturation, options toodownload facture et l’utilisation quotidienne et total des frais pour chaque période de facturation](./media/billing-download-azure-invoice-daily-usage-date/billingSum.png)

5. Sélectionnez **afficher la déclaration actuelle** toosee une estimation de vos frais à hello durée hello estimée a été générée. Cette information est uniquement mise à jour quotidiennement et peut ne pas inclure l’ensemble de votre utilisation. Votre facture mensuelle peut différer de l’estimation.

    ![Capture d’écran qui affiche l’option d’afficher la déclaration actuelle hello](./media/billing-download-azure-invoice-daily-usage-date/billingSum2.png)

    ![Capture d’écran qui affiche l’estimation hello de frais actuels](./media/billing-download-azure-invoice-daily-usage-date/billingSum3.png)

6. Sélectionnez **télécharger l’utilisation** toodownload hello données d’utilisation quotidienne dans un fichier CSV. Si deux versions sont disponibles, téléchargez la version 2.

    ![Capture d’écran qui affiche l’option Télécharger l’utilisation de hello](./media/billing-download-azure-invoice-daily-usage-date/DLusage.png)

Uniquement hello administrateur de compte peut accéder au centre des comptes Azure hello. Autres administrateurs de facturation, par exemple un propriétaire, obtenir des informations d’utilisation à l’aide de hello [API facturation](billing-usage-rate-card-overview.md).

Pour plus d’informations sur votre utilisation quotidienne, consultez la page [Comprendre votre facture Microsoft Azure](billing-understand-your-bill.md). Pour obtenir de l’aide sur la gestion des coûts, consultez [Éviter les coûts inattendus avec la gestion de la facturation et des coûts dans Azure](billing-getting-started.md).

## <a name="noinvoice"></a>Pourquoi ne puis-je pas voir une facture pour hello dernière période de facturation ?

Si vous ne voyez pas de facture, cela peut être pour plusieurs raisons :

- Vous disposez d’un crédit mensuel pour votre abonnement qui n’est pas dépassé ou vous disposez d’un essai gratuit. Une facture est générée uniquement lorsque vous avez quelque chose à payer.

- Il est moins de 30 jours à partir du jour hello que vous vous êtes abonné tooAzure.

- facture de Hello n’est pas encore générée. Attendez la fin hello de période de facturation hello.

- Si vous n’êtes pas hello administrateur de compte, anciennes factures ne peuvent pas être tooyou d’est disponible.

## <a name="need-help-contact-support"></a>Vous avez besoin d’aide ? Contactez le support technique.
Si vous en avez d’autres questions, [contactez le support technique](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget votre problème résolu rapidement.

