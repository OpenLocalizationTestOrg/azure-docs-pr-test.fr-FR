---
title: "les abonnements aaaNo a détecté l’erreur lorsque essayez toosign dans tooAzure portal ou centre des comptes Azure | Documents Microsoft"
description: "Fournit des solutions de hello pour un problème dans lequel les abonnements non trouvent une erreur se produit lorsque vous connecter tooAzure portail ou le centre de gestion Azure."
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.assetid: d1545298-99db-4941-8e97-f24a06bb7cb6
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: genli
ms.openlocfilehash: def4d4a1f883dd948fe8132f2d85abc4c23ae624
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="no-subscriptions-found-error-in-azure-portal-or-azure-account-center"></a>Erreur Aucun abonnement trouvé dans le portail Azure ou le centre des comptes Azure
Vous pouvez recevoir un message d’erreur « Aucun abonnement trouvé » lorsque vous essayez de toosign dans toohello [portail Azure](https://portal.azure.com/) ou hello [centre des comptes Azure](https://account.windowsazure.com/Subscriptions). Cet article fournit une solution à ce problème.

## <a name="symptom"></a>Symptôme

Lorsque vous essayez de toosign dans toohello [portail Azure](https://portal.azure.com/) ou hello [centre des comptes Azure](https://account.windowsazure.com/Subscriptions), vous recevez hello message d’erreur suivant : « Aucun abonnement trouvé ».

## <a name="cause"></a>Cause :

Ce problème se produit si votre compte ne dispose pas des autorisations suffisantes. 

## <a name="solution"></a>Solution

Assurez-vous que vous vous connecter en tant qu’administrateur correct de hello. Un administrateur de compte peut accéder au centre des comptes hello uniquement. Les administrateurs de service (SA) et Coadministrateurs (CA) ont accès autorisation toohello uniquement portail Azure ou hello portail Azure classic.

### <a name="scenario-1-error-message-is-received-in-hello-azure-portalhttpsportalazurecom"></a>Scénario 1 : Message d’erreur est reçu dans hello [portail Azure](https://portal.azure.com)

toofix ce problème :

* Vérifiez que hello correct de répertoire Azure est sélectionné en cliquant sur votre compte en haut de hello à droite.

  ![Répertoire hello sélectionnez hello haut à droite de hello portail Azure](./media/billing-no-subscriptions-found/directory-switch.png)

* Si hello droite Azure directory est activée mais toujours le message hello, [votre compte a été ajouté en tant que propriétaire](billing-add-change-azure-subscription-administrator.md).

### <a name="scenario-2-error-message-is-received-in-hello-azure-account-centerhttpsaccountwindowsazurecomsubscriptions"></a>Scénario 2 : Message d’erreur est reçu dans hello [centre des comptes Azure](https://account.windowsazure.com/Subscriptions)

Vérifiez si le compte hello que vous avez utilisé est hello administrateur de compte. tooverify qui hello compte administrateur est, procédez comme suit :

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Dans le menu du Hub hello, sélectionnez **abonnement**.
3. Sélectionnez hello abonnement que vous souhaitez toocheck, puis sélectionnez **paramètres**.
4. Sélectionner **Propriétés**. administrateur du compte d’abonnement de hello Hello s’affiche dans hello **Admin. compte** boîte.

## <a name="need-help-contact-support"></a>Vous avez besoin d’aide ? Contactez le support technique.
Si vous avez besoin d’aide, [contactez le support technique](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) tooget votre problème résolu rapidement. 
