---
title: "aaaLog ticket de Support pour la série StorSimple 8000 | Documents Microsoft"
description: "Découvrez comment demander de toocreate une prise en charge et démarrer une session de support sur votre appareil StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 2ebc20fe-f490-4749-8e43-c9fac86f1676
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/27/2017
ms.author: alkohli;anbacker
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e1a3aa3c56e036c782c4fb502c477dc0feaa0ccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="contact-microsoft-support-for-your-storsimple"></a>Contactez le support technique Microsoft pour votre système StorSimple
Si vous rencontrez des problèmes avec votre solution Microsoft Azure StorSimple, vous pouvez créer une demande de service pour le support technique. Dans une session en ligne avec votre ingénieur du support technique, vous devez également toostart une session de prise en charge sur votre appareil StorSimple. Cet article vous guide tout au long des procédures suivantes :

* Comment demander de toocreate une prise en charge.
* Comment toostart une session de prise en charge dans hello interface Windows PowerShell de votre appareil StorSimple.

Hello de révision [SLA de prise en charge série StorSimple 8000 et informations](https://msdn.microsoft.com/library/mt433077.aspx) avant de créer une demande de Support.

## <a name="create-a-support-request"></a>Création d’une demande de support
Effectuez hello suivant les étapes toocreate une demande de support :

#### <a name="toocreate-a-support-request"></a>toocreate une demande de support
1. Bonjour [portail Azure classic](https://manage.windowsazure.com/), dans le coin supérieur droit hello, cliquez sur le nom de votre compte, puis sur **contactez le Support technique Microsoft**.
   
    ![Contacter le support MS via le Portail de gestion](./media/storsimple-contact-microsoft-support/Ibiza1.png)
2. Vous serez redirigé toohello nouveau Azure portail (portal.azure.com). Cliquez sur hello **nouveau prend en charge la demande** vignette.
   
    ![Contacter le support MS avec le nouveau portail](./media/storsimple-contact-microsoft-support/Ibiza2.png)
   
    Sur la droite de l’écran hello hello hello **nouveau prend en charge la demande** volet s’affiche. 
   
    ![Volet Nouvelle demande de support](./media/storsimple-contact-microsoft-support/Ibiza3a.png)
3. Bonjour **notions de base** boîte de dialogue, hello complet suivant :                                
   
   1. À partir de hello **émettre type** la liste déroulante, sélectionnez **technique**.
   2. Sélectionnez un **abonnement** à partir de la liste déroulante de hello.
   3. À partir de hello **Service** la liste déroulante, sélectionnez **StorSimple**. 
   4. Sélectionnez un **plan de Support** à partir de la liste déroulante de hello. Vous avez besoin d’un tooenable du plan de support payant le Support technique.
4. Cliquez sur **Suivant**. Hello **problème** boîte de dialogue s’affiche.
   
    ![Volet Nouvelle demande de support](./media/storsimple-contact-microsoft-support/Ibiza5a.png) 
5. Bonjour **problème** boîte de dialogue, hello complet suivant :
   
   1. Sélectionnez un **gravité** niveau à partir de la liste déroulante de hello.
   2. Sélectionnez un **type de problème** à partir de la liste déroulante de hello.
   3. Sélectionnez un **catégorie** à partir de la liste déroulante de hello. 
   4. Bonjour **détails** zone, décrivez brièvement votre problème.
   5. Bonjour **laps de temps** zone, indiquez si hello date, heure et fuseau horaire correspondant toohello dernière occurrence du problème.
   6. Sous **téléchargement du fichier**, cliquez sur le package de prise en charge de hello dossier icône toobrowse tooyour.
   7. Sélectionnez hello **partager des informations de diagnostic** case à cocher.
6. Cliquez sur **Suivant**. Hello **les informations de Contact** boîte de dialogue s’affiche.
   
    ![Volet Nouvelle demande de support](./media/storsimple-contact-microsoft-support/Ibiza6a.png) 
7. Entrez vos informations de contact et sélectionnez une méthode de contact (téléphone ou courrier électronique). 
8. Sélectionnez hello **enregistrer les modifications apportées contacts pour les demandes de prise en charge future** case à cocher.
9. Cliquez sur **Créer**.

Une fois que vous avez envoyé votre demande, un ingénieur du Support vous contactera dès que possible tooproceed avec votre demande.

## <a name="start-a-support-session-in-windows-powershell-for-storsimple"></a>Démarrage d’une session de support dans Windows PowerShell pour StorSimple
tootroubleshoot les problèmes que vous pouvez rencontrer avec l’appareil StorSimple hello, vous devez tooengage avec l’équipe de Support technique de Microsoft hello. Support technique de Microsoft peut-être toouse un toolog de session de prise en charge sur les appareils tooyour. 

Hello suivants toostart une session de prise en charge les étapes :

#### <a name="toostart-a-support-session"></a>toostart une session de prise en charge
1. Accès hello le périphérique directement à l’aide de console série de hello ou via une session telnet à partir d’un ordinateur distant. toodo, suivez les étapes hello dans [console série du périphérique toohello tooconnect utilisez PuTTY](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).
2. Dans la session hello qui s’ouvre, appuyez sur hello **entrée** tooget clé une invite de commandes.
3. Dans le menu de console série hello, sélectionnez l’option 1, **connecter avec un accès complet**.
4. À l’invite de hello, tapez Bonjour suivant de mot de passe : 
   
    `Password1`
5. À l’invite de hello, tapez Bonjour de commande suivante :
   
    `Enable-HcsSupportAccess`
6. Tooyou, une chaîne chiffrée s’affiche. Copiez cette chaîne dans un éditeur de texte comme le Bloc-notes.
7. Enregistrer cette chaîne et les envoyer dans un tooMicrosoft de message de messagerie prise en charge. 

> [!IMPORTANT]
> Vous pouvez désactiver l’accès au support en exécutant `Disable-HcsSupportAccess`. l’appareil StorSimple Hello tente également l’accès au support toodisable 8 heures après le début de la session de hello. Il s’agit d’un toochange pratique meilleures informations d’identification de votre appareil StorSimple après le lancement d’une session de support.
> 
> 

