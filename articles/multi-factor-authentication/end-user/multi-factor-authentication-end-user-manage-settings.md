---
title: "aaaManage vos paramètres de vérification en deux étapes | Documents Microsoft"
description: "Gérez l’utilisation d’Azure Multi-Factor Authentication, notamment la modification des informations de contact ou la configuration des appareils."
services: multi-factor-authentication
keywords: "client de l'authentification multifacteur, problème d'authentification, ID de corrélation"
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: d3372d9a-9ad1-4609-bdcf-2c4ca9679a3b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: 2c974b08c584943f3c5a6b9bf16497d1706e8329
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-settings-for-two-step-verification"></a>Gérer les paramètres de la vérification en deux étapes
Cet article répond aux questions concernant les paramètres de tooupdate pour l’authentification multifacteur ou de vérification en deux étapes. Si vous rencontrez des problèmes de connexion tooyour compte, consultez trop[rencontre des problèmes avec la vérification en deux étapes](multi-factor-authentication-end-user-troubleshoot.md) pour la résolution des problèmes.

## <a name="where-toofind-hello-settings-page"></a>Où toofind hello page Paramètres
Selon la façon dont vous utilisez Azure Multi-Factor Authentication, vous pouvez modifier vos paramètres (comme votre numéro de téléphone) de différentes manières.

Si votre administrateur informatique envoyé une URL spécifique ou de la vérification en deux étapes de toomanage étapes, suivez ces instructions. Dans le cas contraire, suivant les instructions de hello doit fonctionner pour les autres. Si vous suivez ces étapes, mais ne pas afficher hello les mêmes options, ce qui signifie que votre entreprise ou école portail personnalisé de leur propres. Demandez à votre administrateur pour le portail de l’authentification multifacteur Azure hello lien tooyour.

1. Connectez-vous trop[https://myapps.microsoft.com](https://myapps.microsoft.com)  
2. Sélectionnez le nom de votre compte dans hello en haut à droite, puis sélectionnez **profil**.  
3. Sélectionnez **Vérification de sécurité supplémentaire**.  

    ![MyApps](./media/multi-factor-authentication-end-user-manage/myapps1.png)
4. charge de la page de vérification de sécurité supplémentaires de Hello avec vos paramètres.

    ![Vérification](./media/multi-factor-authentication-end-user-manage/proofup.png)

## <a name="i-want-toochange-my-phone-number-or-add-a-secondary-number"></a>Souhaitée toochange mon numéro de téléphone, ou ajouter un numéro secondaire
Il est important tooconfigure un numéro de téléphone d’authentification secondaire.  Étant donné que le nombre et votre application mobile de téléphone de votre serveur principal sont probablement sur hello même de téléphone, numéro de téléphone secondaire de hello est le seul moyen de la hello vous serez en mesure de tooget dans votre compte si votre téléphone est perdu ou volé.

> [!NOTE]
> Si vous n’ont le numéro de téléphone principal accès tooyour et avez besoin d’aide dans tooyour compte, consultez notre rubriques d’aide dans [rencontre des problèmes avec la vérification en deux étapes](multi-factor-authentication-end-user-troubleshoot.md).  

**toochange numéro de téléphone de votre serveur principal :**  

1. Sur la page de vérification de sécurité supplémentaires de hello, sélectionnez la zone de texte hello avec votre numéro de téléphone et le modifier avec votre nouveau numéro de téléphone.  
2. Sélectionnez **Enregistrer**.  
3. Numéro de hello que vous utilisez pour votre option préférée de vérification, vous avez nouveau numéro de tooverify hello avant que vous pouvez l’enregistrer.  

**tooadd un numéro de téléphone secondaire :**  

1. Sur la page de vérification de sécurité supplémentaires de hello, hello case à cocher ensuite trop**autre téléphone d’authentification.**  
2. Entrez votre numéro de téléphone secondaire dans la zone de texte hello.  
3. Sélectionnez **Enregistrer**. Vos modifications sont apportées.  

## <a name="require-two-step-verification-again-on-a-device-youve-marked-as-trusted"></a>Exiger une nouvelle vérification en deux étapes sur un appareil marqué comme approuvé

Selon les paramètres de votre organisation, vous pouvez disposer d’une case à cocher libellée « Ne plus me le demander pendant **X** jours » lorsque vous effectuez une vérification en deux étapes sur votre navigateur. Si vous activez cette case à cocher et perdez votre appareil ou pensez que votre compte est compromis, vous devez restaurer vos appareils tooall de vérification en deux étapes. 

1. Sur la page de vérification de sécurité supplémentaires de hello, sélectionnez **l’authentification multifacteur de restauration sur les appareils déjà de confiance**.
2. Hello prochaine que connexion sur n’importe quel appareil, vous serez invité à tooperform en deux étapes vérification. 

## <a name="how-do-i-clean-up-microsoft-authenticator-from-my-old-device-and-move-tooa-new-one"></a>Comment nettoyer Microsoft Authenticator à partir de mon appareil ancien et déplacer tooa nouveau ?
Lorsque vous désinstallez l’application hello à partir de votre appareil ou un périphérique hello de réinitialisation, elle ne supprime pas l’activation de hello principal hello. Pour plus d’informations, consultez [Microsoft Authenticator](microsoft-authenticator-app-how-to.md).

## <a name="next-steps"></a>Étapes suivantes
* Obtenir des conseils de dépannage et de l’aide dans [Problèmes avec la vérification en deux étapes](multi-factor-authentication-end-user-troubleshoot.md)
* Configurer des [mots de passe d’application](multi-factor-authentication-end-user-app-passwords.md) pour les applications qui ne prennent pas en charge la vérification en deux étapes
