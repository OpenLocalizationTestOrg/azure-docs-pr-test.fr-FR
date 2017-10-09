---
title: "Azure Active Directory B2C : réinitialisation de mot de passe libre-service | Microsoft Docs"
description: "Une rubrique illustrant comment réinitialiser les tooset le mot de passe libre-service pour vos consommateurs dans Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: curtand
ms.assetid: c87ed86e-1520-42b1-8c31-46cd44ed5310
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: ff87eea42259b610702da73af35d0a38eb7dd33d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-set-up-self-service-password-reset-for-your-consumers"></a>Azure Active Directory B2C : configuration de la réinitialisation du mot de passe libre-service pour vos consommateurs
Avec hello fonctionnalité de réinitialisation de mot de passe libre-service, vos consommateurs (qui se sont inscrites pour les comptes locaux) peuvent réinitialiser leurs mots de passe sur leurs propres. Cela réduit considérablement la charge hello votre personnel de prise en charge, en particulier si votre application a des millions de consommateurs en l’utilisant sur une base régulière. Actuellement, nous prenons uniquement en charge l’utilisation d’une adresse électronique vérifiée comme méthode de récupération. Nous allons ajouter des méthodes de récupération supplémentaires (numéro de téléphone vérifié, les questions de sécurité, etc.) dans les futures hello.

> [!NOTE]
> Cet article s’applique à un mot de passe tooself service utilisée dans le contexte de hello d’une stratégie de réinitialisation. Si vous avez besoin de stratégies de réinitialisation de mot de passe entièrement personnalisables appelées à partir de votre application, consultez [cet article](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).
> 
> 

Par défaut, la réinitialisation de mot de passe libre-service ne sera pas activée pour votre annuaire. Utilisez hello suivant les étapes tooturn sur :

1. Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com/) comme hello administrateur de l’abonnement. Il s’agit de hello même travail ou scolaire compte ou hello du même compte Microsoft que vous avez utilisé toocreate votre annuaire.
2. Accédez à extension d’Active Directory toohello sur la barre de navigation hello sur le côté gauche de hello.
3. Trouver votre répertoire sous hello **répertoire** onglet et cliquez dessus.
4. Cliquez sur hello **configurer** onglet.
5. Faites défiler vers le bas toohello **stratégie de réinitialisation du mot de passe utilisateur** hello section et bascule **les utilisateurs activés pour la réinitialisation du mot de passe** option trop**Oui**. Notez que hello **autre adresse de messagerie** option est activée ; laisser car il s’agit.
   
    ![Réinitialisation de mot de passe libre-service](./media/active-directory-b2c-reference-sspr/sspr.png)
6. Cliquez sur **enregistrer** bas hello de page de hello. Vous avez terminé !

tootest, utiliser la fonctionnalité « Exécuter maintenant » hello sur toute stratégie d’authentification qui a des comptes locaux en tant que fournisseur d’identité. Sur la connexion du hello compte local page (où vous entrez une adresse de messagerie et mot de passe, ou un nom d’utilisateur et le mot de passe), cliquez sur **ne peut pas accéder à votre compte ?** expérience du consommateur tooverify hello.

> [!NOTE]
> Hello pages de réinitialisation de mot de passe libre-service peuvent être personnalisés à l’aide de hello [fonctionnalité de marque de société](../active-directory/active-directory-add-company-branding.md).
> 
> 

