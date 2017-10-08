---
title: "Azure Active Directory B2C : désactiver la vérification par e-mail lors de l’inscription du consommateur | Microsoft Docs"
description: "Une rubrique illustrant comment toodisable envoyer par courrier électronique vérification au cours du consommateur d’inscription dans Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 433f32b8-96d2-4113-aa82-efcf42fa9827
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/06/2017
ms.author: parakhj
ms.openlocfilehash: a8a42eddcb577725f04d70e1b1ebbebf10b5937c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-disable-email-verification-during-consumer-sign-up"></a>Azure Active Directory B2C : désactiver la vérification par e-mail lors de l’inscription du consommateur
Lorsque activé, permet d’Azure Active Directory (Azure AD) B2C un consommateur hello toosign de capacité pour les applications en fournissant une adresse de messagerie et de création d’un compte local. Azure AD B2C garantit des adresses de messagerie valides en exigeant que les consommateurs tooverify leur pendant le processus d’inscription hello. Elle évite également d’un processus automatisé malveillant à partir de la génération des comptes factices pour les applications de hello.

Certains développeurs d’applications préfèrent la vérification du courrier électronique tooskip pendant le processus d’inscription hello et ont à la place des consommateurs vérifier adresse de messagerie hello plus tard. toosupport cela, Azure AD B2C peut être la vérification du courrier électronique toodisable configuré. Cela crée un processus de connexion plus lisse et offre aux développeurs hello flexibilité toodifferentiate hello consommateurs qui ont vérifié leur adresse de messagerie à partir de ces consommateurs qui n’ont pas.

Par défaut, la vérification est activée pour les stratégies d’inscription. Utilisez hello suivant les étapes tooturn désactivé :

1. [Suivez ces Panneau de fonctionnalités étapes toonavigate toohello B2C hello Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).
2. Cliquez sur les **stratégies d’inscription** ou les **stratégies d’inscription ou de connexion** selon la configuration de l'inscription.
3. Cliquez sur votre tooopen stratégie (par exemple, « B2C_1_SiUp ») il. Cliquez sur **modifier** haut hello du Panneau de hello.
4. Cliquez sur la fonctionnalité de **personnalisation de l’interface utilisateur de page**.
5. Cliquez sur **page d’inscription à un compte Local**.
6. Cliquez sur **adresse de messagerie** Bonjour **nom** colonne sous hello **des attributs d’abonnement** section.
7. Hello de bascule **exiger la vérification** option trop**non**.
8. Cliquez sur **OK** bas hello jusqu'à ce que vous atteigniez hello **modifier la stratégie** panneau.
9. Cliquez sur **enregistrer** haut hello du Panneau de hello. Vous avez terminé !

> [!NOTE]
> La désactivation de vérification de courrier électronique dans le processus d’inscription hello peut entraîner un toospam. Si vous désactivez hello par défaut, nous vous recommandons d’ajouter votre propre système de vérification.
> 
> 

Nous sommes toujours ouvrir toofeedback ainsi que des suggestions ! Si vous rencontrez des difficultés avec cette rubrique, ou que vous avez des recommandations pour améliorer ce contenu, nous aimerions connaître votre opinion bas hello de page de hello. Pour les demandes de fonctionnalités, ajoutez-les trop[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).
