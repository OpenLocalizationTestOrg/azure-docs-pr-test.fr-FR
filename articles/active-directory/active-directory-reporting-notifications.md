---
title: aaaAzure Notifications de rapports Active Directory
description: "Comment toouse hello notifications de création de rapports Azure Active Directory pour l’authentification suspectes ins."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ae6d4b0e-5931-4cb3-98bf-9be91b381c92
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.custom: oldportal
ms.reviewer: dhanyahk
ms.openlocfilehash: 3843c45eaf9d68e671943bfdbc7ab68933f38fbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-notifications"></a>Notifications de rapports Azure Active Directory
## <a name="what-reports-generate-email-notifications"></a>Quels rapports génèrent les notifications par courrier électronique
À ce stade, uniquement hello anormales dans les déclencheurs de rapport d’activité de messagerie des notifications.

## <a name="what-is-an-irregular-sign-in"></a>Qu'est-ce qu'une « connexion anormale » ?
Connexions anormales sont celles qui ont été identifiées par nos algorithmes, sur la base de hello d’une condition « voyage impossible » associée à un emplacement de connexion anormal et le dispositif d’apprentissage. Cela peut indiquer qu’un pirate a essayé de toosign en utilisant ce compte.

## <a name="who-receives-hello-email-notifications"></a>Qui reçoit des notifications par courrier électronique de hello ?
messagerie de Hello est envoyée tooall les administrateurs généraux titulaires d’une licence Active Directory Premium. tooensure qu'il est remis, nous envoyer ainsi toohello administrateurs autre adresse de messagerie. Administrateurs doivent inclure aad-alerts-noreply@mail.windowsazure.com dans leur liste d’expéditeurs fiables pour ne pas manquer par courrier électronique hello.

## <a name="how-often-are-these-emails-sent"></a>Quelle est la fréquence d’envoi de ces courriers électroniques ?
courrier électronique de Hello est envoyé si 10 nouvelle irrégulières connectez-vous activités se produisent dans hello 30 derniers jours, ou depuis le dernier courrier électronique de hello a été envoyé, si elle est inférieure.

## <a name="how-do-i-access-hello-report-mentioned-in-hello-email"></a>Comment accéder aux rapports hello mentionné par courrier électronique hello ?
Lorsque vous cliquez sur le lien de hello, vous serez redirigé toohello page de rapport dans hello portail Azure classic. Dans l’ordre tooaccess hello rapport, vous devez toobe les deux :

* Un administrateur ou un coadministrateur de votre abonnement Azure
* Un administrateur global dans le répertoire de hello et attribué une licence Active Directory Premium. Pour plus d’informations, consultez la page [Éditions d’Azure Active Directory](active-directory-editions.md).

## <a name="can-i-turn-off-these-emails"></a>Puis-je désactiver ces courriers électroniques ?
Oui, tooturn notifications liées connexions tooanomalous dans hello portail Azure classic, cliquez sur **configurer**, puis sélectionnez **désactivé** sous hello **Notifications**section.

## <a name="whats-next"></a>Étapes suivantes
* Curieux de savoir quels rapports de sécurité, d'audit et d'activité sont disponibles ? Découvrez [Rapports de sécurité, d'audit et d'activité d'Azure AD](active-directory-view-access-usage-reports.md)
* [Prise en main d’Azure Active Directory Premium (AD)](active-directory-get-started-premium.md)
* [Ajouter des logos tooyour pages de connexion et du volet d’accès de la société](active-directory-add-company-branding.md)

