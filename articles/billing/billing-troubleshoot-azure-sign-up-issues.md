---
title: "aaaTroubleshoot Azure problèmes d’inscription | Documents Microsoft"
description: "Décrit comment tootroubleshoot certains Azure commun se connectent des problèmes."
services: 
documentationcenter: 
author: JiangChen79
manager: adpick
editor: 
tags: billing,top-support-issue
ms.assetid: a0907da1-cb2d-41d1-a97f-43841fabe355
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: cjiang
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ee649bfc3be7ba1fe2dd863fac09e1c2311d835b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-sign-up-issues-for-azure"></a>Résoudre les problèmes d’inscription pour Azure
Si vous ne pouvez pas vous inscrire à Azure, utilisez les conseils de hello dans cet article tootroubleshoot commun les problèmes. Si vous rencontrez un problème avec votre carte de crédit lors de l’inscription, consultez la page [Votre carte bancaire est refusée lors de l’inscription à Azure](billing-credit-card-fails-during-azure-sign-up.md). Si vous avez un compte Azure, mais ne peut pas se connecter, consultez [je ne parviens pas à se connecter toomanage mon abonnement Azure](billing-cannot-login-subscription.md).

## <a name="progress-bar-hangs-in-identity-verification-by-card-section"></a>La barre de progression se bloque dans la section « Vérification d’identité par carte »

vérification d’identité toocomplete hello par carte, les cookies tiers doivent être autorisés pour votre navigateur.

![Capture d’écran de vérification d’identité par section de carte négatif pendant l’inscription de hello](./media/billing-troubleshoot-azure-sign-up-issues/identity-verification-hangs.PNG)

Utiliser des paramètres de cookies de votre navigateur hello suivant les étapes tooupdate.

1. Si vous êtes à l’aide de Chrome, accédez trop**paramètres** > **afficher les paramètres avancés** > **confidentialité** > **contenu paramètres**. Décochez **Bloquer les cookies et les données de site tiers**.
2. Si vous utilisez Edge, passez trop**paramètres** > **afficher les paramètres avancés** > **Cookies**. Sélectionnez **Ne pas bloquer les cookies**.
3. Actualiser hello Azure page d’inscription, puis vérifiez si hello problème est résolu.
4. Si l’actualisation hello n’a pas résolu le problème de hello, quittez et redémarrez votre navigateur, puis réessayez.

## <a name="credit-card-form-doesnt-support-my-billing-address"></a>Le formulaire relatif à la carte de crédit ne prend pas en charge mon adresse de facturation
Votre adresse de facturation doit toobe dans les pays hello que vous avez sélectionné dans hello **vous concernant** section. Assurez-vous que vous sélectionnez pays hello.

## <a name="no-text-messages-or-calls-during-sign-up-account-verification"></a>Aucun message texte ni appel lors de la vérification du compte à l’inscription
S’il est généralement beaucoup plus rapide, cela peut prendre jusqu'à minutes toofour toobe de code de vérification remis. numéro de téléphone Hello que vous entrez pour la vérification ne sont pas stockée en tant qu’un numéro de contact pour le compte de hello.

Voici quelques conseils supplémentaires :
* Un numéro de téléphone VOIP ne peut pas être utilisé pour le processus de vérification de téléphone hello.
* Numéro de téléphone hello double vérification vous entrez, y compris le code de pays hello vous avez sélectionné dans le menu déroulant de hello.
* Si votre téléphone ne reçoit des messages texte (SMS), essayez de hello **m’appeler** option.
* Vérifiez que votre téléphone peut recevoir des appels ou des SMS provenant d’un numéro basé aux États-Unis.

Lorsque vous obtenez le message de texte hello ou appel téléphonique, entrez le code qui s’affiche dans la zone de texte hello.

## <a name="credit-card-declined-or-not-accepted"></a>Carte de crédit refusée
Les cartes de crédit ou de débit virtuelles ou prépayées ne sont pas acceptées comme mode de paiement pour les abonnements Azure. toosee, ce qui peut entraîner votre toobe carte refusée, consultez [votre carte de débit ou de la carte de crédit est refusée à Azure d’abonnement](billing-credit-card-fails-during-azure-sign-up.md).

## <a name="free-trial-is-not-available"></a>« L'essai gratuit n'est pas disponible »
Vous utilisez un abonnement Azure Bonjour précédentes Hello Azure les conditions d’utilisation limite l’activation d’évaluation gratuite uniquement pour un utilisateur qui est nouvelle tooAzure. Si vous avez déjà souscrit un autre type d’abonnement Azure, vous ne pouvez pas activer une version d'évaluation gratuite. Inscrivez-vous à un [abonnement de type paiement à l’utilisation](https://azure.microsoft.com/offers/ms-azr-0003p/).

## <a name="i-saw-a-charge-on-my-free-trial-account"></a>J’ai vu des frais sur mon compte d’essai gratuit
Vous pouvez voir un petit contenir de vérification sur votre compte de carte de crédit une fois inscrit, ce qui est supprimé dans les 3 jours too5. Si vous êtes soucieux quant à la gestion des coûts, lisez-en davantage sur la [prévention des coûts inattendus](https://docs.microsoft.com/azure/billing/billing-getting-started).

## <a name="cant-activate-azure-benefit-plan-like-msdn-bizspark-bizsparkplus-or-mpn"></a>Je n’arrive pas à activer un plan d’avantages Azure de type MSDN, BizSpark, BizSparkPlus ou MPN
Assurez-vous que vous utilisez hello droite connectez-vous informations d’identification. Vérifiez ensuite hello avantage programme toomake que que vous êtes éligible. 

* MSDN
  * Vérifiez l’état de votre éligibilité dans votre [page de compte MSDN](https://msdn.microsoft.com/subscriptions/manage/default.aspx).
  * Si vous ne peut pas vérifier votre statut, contactez hello [centres abonnements MSDN](https://msdn.microsoft.com/subscriptions/contactus.aspx)
* BizSpark
  * Connectez-vous à toohello [BizSpark portail](https://www.microsoft.com/bizspark/default.aspx#start-two) et vérifier l’état de votre éligibilité de BizSpark et BizSpark Plus.
  * Si vous ne peut pas vérifier l’état, vous pouvez [obtenir de l’aide sur les forums de BizSpark hello](http://aka.ms/bzforums).
* MPN
  * Connectez-vous à toohello [portal MPN](https://mspartner.microsoft.com/en/us/Pages/Locale.aspx) et vérifiez l’état de votre éligibilité. Si vous avez hello approprié [compétences de plateforme Cloud](https://mspartner.microsoft.com/en/us/pages/membership/cloud-platform-competency.aspx), vous pouvez bénéficier d’avantages supplémentaires.
  * Si vous ne pouvez pas vérifier votre état, contactez le [support MPN](https://mspartner.microsoft.com/en/us/Pages/Support/Premium/contact-support.aspx).

## <a name="cant-activate-new-azure-in-open-subscription"></a>Je n’arrive pas à activer un nouvel abonnement Azure dans Open
toocreate un abonnement Azure dans Open, vous devez disposer d’une clé d’Activation de Service en ligne (OSA) valide au moins un tooit associé jeton Azure dans Open. Si vous ne disposez d’aucune clé OSA, contactez l’un des partenaires Microsoft répertoriés dans [Microsoft Pinpoint](http://pinpoint.microsoft.com/).

## <a name="need-help-contact-support"></a>Vous avez besoin d’aide ? Contactez le support technique.
Si vous avez besoin d’aide, [contactez le support technique](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget votre problème résolu rapidement.
