---
title: "aaaManage tooAzure de l’accès à l’aide de rôles de facturation | Documents Microsoft"
description: 
services: 
documentationcenter: 
author: vikramdesai01
manager: vikdesai
editor: 
tags: billing
ms.assetid: e4c4d136-2826-4938-868f-a7e67ff6b025
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: vikdesai
ms.openlocfilehash: 5937fac5ffa5ca204eb03a1dcbc5e800b3d5eb74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-access-toobilling-information-for-azure-using-role-based-access-control"></a>Gérer les informations de toobilling d’accès pour Azure à l’aide du contrôle d’accès basé sur un rôle

Vous pouvez accorder l’accès pour Azure toomembers informations facturation de votre équipe en affectant une des hello suivant abonnement tooyour de rôles utilisateur : administrateur de compte, administrateur de Service, coadministrateur, propriétaire, collaborateur, lecteur et lecteur de facturation. Ils auraient pas accès toobilling informations Bonjour [portail Azure](https://portal.azure.com/), et ils peuvent utiliser hello [API de facturation](billing-usage-rate-card-overview.md) tooprogrammatically obtenir factures (une fois choisi-entrant) et les détails d’utilisation. Pour plus d’informations sur les utilisateurs pouvant accorder des rôles, et sur ce que les rôles permettent de faire, consultez [Rôles dans Azure RBAC](../active-directory/role-based-access-built-in-roles.md).

## <a name="opt-in"></a>Autoriser des utilisateurs supplémentaires tooaccess factures

Hello administrateur de compte doit s’abonner à l’aide de hello [portail Azure](https://portal.azure.com/) autoriser l’accès tooinvoices pour d’autres utilisateurs et via l’API.

1. Comme hello administrateur de compte, sélectionnez votre abonnement à partir de hello [panneau d’abonnements](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) dans le portail Azure.

1. Sélectionnez **factures** , puis **tooinvoices d’accès**.

    ![Capture d’écran montre comment accéder à tooinvoices toodelegate](./media/billing-manage-access/AA-optin.png)

1. Activer **sur** les accès hello suivie de l’enregistrement des modifications de hello, tooallow des utilisateurs dans l’abonnement rôles étendus toodownload facture.

    ![Capture d’écran montre marche / arrêt toodelegate accès tooinvoice](./media/billing-manage-access/AA-optinAllow.png)

Si vous activez permet d’administrateur de Service, coadministrateur, propriétaire, collaborateur, lecteur et de facturation de lecteur sur les factures PDF hello abonnement toodownload Bonjour portail Azure. Toutefois, les factures antérieures à 2016 de décembre sont toohello uniquement disponible administrateur de compte pour l’instant.

Hello administrateur de compte peut également configurer toohave les factures envoyées par courrier électronique. toolearn, voir [obtenir votre facture par courrier électronique](billing-download-azure-invoice-daily-usage-date.md).

## <a name="adding-users-toohello-billing-reader-role"></a>Ajout de rôle de lecteur de facturation toohello utilisateurs

rôle de lecteur de facturation Hello dispose d’informations de facturation toosubscription accès en lecture seule dans le portail Azure et aucun tooservices accès tels que les machines virtuelles et les comptes de stockage. Affecter toosomeone de rôle de lecteur de facturation hello qui doit accéder aux informations de facturation toohello mais pas hello capacité toomanage Azure services. Ce rôle convient aux utilisateurs d’une organisation qui procèdent uniquement à la gestion financière et des coûts pour des abonnements Azure.

1. Sélectionnez votre abonnement à partir de hello [panneau d’abonnements](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) dans le portail Azure.

1. Sélectionnez **Contrôle d’accès (IAM)**, puis cliquez sur **Ajouter**.

    ![Capture d’écran montre IAM dans le panneau d’abonnement hello](./media/billing-manage-access/select-iam.PNG)

1. Choisissez **lecteur de facturation** Bonjour **sélectionner un rôle** page.

    ![Capture d’écran montre la facturation de lecteur dans la vue de fenêtre contextuelle hello](./media/billing-manage-access/select-roles.PNG)

1. Type de messagerie hello pour utilisateur hello souhaité tooinvite, puis cliquez sur **OK** invitation de hello toosend.

    ![Capture d’écran tooenter messagerie tooinvite une personne](./media/billing-manage-access/add-user.PNG)

1. Suivez les instructions de toolog de courrier électronique d’invitation hello dans comme un lecteur de facturation.

    ![Capture d’écran que hello du lecteur de facturation peut voir dans le portail Azure](./media/billing-manage-access/billing-reader-view.png)

> [!NOTE]
> fonctionnalité de lecteur de facturation Hello est en version préliminaire et ne prend pas en charge les abonnements de l’entreprise (EA) ou non globale clouds.

## <a name="adding-users-tooother-roles"></a>Ajout de rôles d’utilisateurs tooother

Les utilisateurs d’autres rôles, tels que Propriétaire ou Collaborateur, peuvent non seulement accéder aux informations de facturation, mais également à des services Azure. toomanage ces rôles, consultez [ajouter ou modifier les rôles administrateur Azure qui gèrent les abonnement hello ou services](billing-add-change-azure-subscription-administrator.md).

## <a name="who-can-access-hello-account-centerhttpsaccountwindowsazurecom"></a>Qui peut accéder à hello [centre des comptes](https://account.windowsazure.com)?

Centre des comptes toohello pouvez vous connecter uniquement hello administrateur de compte. Hello administrateur de compte est propriétaire légal de hello d’abonnement de hello. Par défaut, hello personne inscrit ou acheté hello abonnement Azure est hello administrateur de compte, à moins que hello [la propriété d’abonnement a été transférée](billing-subscription-transfer.md) toosomebody else. Hello administrateur de compte peut créer des abonnements, annuler les abonnements, modifiez l’adresse de facturation hello pour un abonnement et gérer les stratégies d’accès pour l’abonnement de hello.

## <a name="need-help-contact-support"></a>Vous avez besoin d’aide ? Contactez le support technique.

Si vous en avez d’autres questions, [contactez le support technique](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget votre problème résolu rapidement.
