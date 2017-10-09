---
title: "aaaCreate ticket de Support ou cas de série StorSimple 8000 | Documents Microsoft"
description: "Découvrez comment toolog prennent en charge la demande et démarrer une session de support sur votre appareil de série StorSimple 8000."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: alkohli;
ms.openlocfilehash: 832e3ac739dafa6dd8c24aaea38aef9c6f1b27b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="contact-microsoft-support"></a>Contacter le support Microsoft

Hello, le Gestionnaire de périphériques StorSimple fournit une fonctionnalité de hello trop**connecter une nouvelle demande de support** dans le panneau de résumé de service hello. Si vous rencontrez des problèmes avec votre solution StorSimple, vous pouvez créer une demande de service pour obtenir un support technique. Dans une session en ligne avec votre ingénieur du support technique, vous devez également toostart une session de prise en charge sur votre appareil StorSimple. Cet article vous guide tout au long des procédures suivantes :

* Comment demander de toocreate une prise en charge.
* Cycle de vie à partir de portail de hello demander toomanage une prise en charge.
* Comment toostart une session de prise en charge dans hello interface Windows PowerShell de votre appareil StorSimple.

Hello de révision [SLA de prise en charge série StorSimple 8000 et informations](https://msdn.microsoft.com/library/mt433077.aspx) avant de créer une demande de Support.

## <a name="create-a-support-request"></a>Création d’une demande de support

En fonction de votre [plan de support](https://azure.microsoft.com/support/plans/), vous pouvez créer des tickets de support pour un problème sur votre appareil StorSimple directement à partir de panneau Résumé du service Gestionnaire de périphériques StorSimple hello. Effectuez hello suivant les étapes toocreate une demande de support :

#### <a name="toocreate-a-support-request"></a>toocreate une demande de support

1. Atteindre le service du Gestionnaire de périphériques StorSimple tooyour. Dans Paramètres du panneau Résumé hello service, accédez trop**prise en charge + dépannage** section, puis cliquez sur **nouveau prend en charge la demande**.
     
    ![Contacter le support MS avec le nouveau portail](./media/storsimple-8000-contact-microsoft-support/contactsupport1.png)
   
2. Bonjour **nouveau prend en charge la demande** panneau, sélectionnez **notions de base**. Bonjour **notions de base** panneau, hello comme suit :
   1. À partir de hello **émettre type** la liste déroulante, sélectionnez **technique**.
   2. Hello actuel **abonnement**, **Service** type et hello **ressource** (Gestionnaire de périphériques StorSimple service) sont automatiquement sélectionnés. 
   3. Sélectionnez un **plan de Support** à partir de la liste de déroulante hello si vous avez plusieurs plans associés à votre abonnement. Vous avez besoin d’un tooenable du plan de support payant le Support technique.
   4. Cliquez sur **Suivant**.

       ![Contacter le support MS avec le nouveau portail](./media/storsimple-8000-contact-microsoft-support/contactsupport2.png)

3. Bonjour **nouveau prend en charge la demande** panneau, sélectionnez **étape 2 problème**. Bonjour **problème** panneau, hello comme suit :
    
    1. Choisissez hello **gravité**.
    2. Spécifiez si le problème de hello est toohello connexes appliance ou hello service du Gestionnaire de périphériques StorSimple.
    3. Choisissez un **catégorie** pour ce problème et offrent une meilleure **détails** sur le problème de hello.
    4. Fournissez hello date et l’heure pour le problème de hello.
    5. Bonjour **téléchargement du fichier**, cliquez sur le package de prise en charge de hello dossier icône toobrowse tooyour.
    6. Sélectionnez la case à cocher **Partager les informations de diagnostic**.
    7. Cliquez sur **Suivant**.

       ![Contacter le support MS avec le nouveau portail](./media/storsimple-8000-contact-microsoft-support/contactsupport3.png) 

4. Bonjour **nouveau prend en charge la demande** panneau, cliquez sur **étape 3 coordonnées**. Bonjour **les informations de Contact** panneau, hello comme suit :

    1. Bonjour **options de Contact**hello language et fournir votre méthode de contact préférée (téléphone ou courrier électronique). temps de réponse Hello est automatiquement sélectionné en fonction de votre plan d’abonnement.
    2. Dans les informations de Contact de hello, fournissez votre nom, par courrier électronique, contact facultatif, le pays. Sélectionnez hello **enregistrer les modifications apportées contacts pour les demandes de prise en charge future** case à cocher.
    3. Cliquez sur **Créer**.
   
        ![Contacter le support MS avec le nouveau portail](./media/storsimple-8000-contact-microsoft-support/contactsupport5.png)   

    Support technique de Microsoft utilise cette tooreach informations out tooyou pour plus d’informations, de diagnostic et de résolution.
Une fois que vous avez envoyé votre demande, un ingénieur du Support vous contactera dès que possible tooproceed avec votre demande.

## <a name="manage-a-support-request"></a>Gérer une demande de support

Après avoir créé un ticket de support, vous pouvez gérer hello du cycle de vie du ticket hello de portail de hello.

#### <a name="toomanage-your-support-requests"></a>demande de support technique de votre toomanage

1. tooget toohello aide et prend en charge de la page, accédez trop**Parcourir > aide + support**.

    ![Gérer les demandes de support](./media/storsimple-8000-contact-microsoft-support/managesupport1.png)

2. Un tableau qui répertorie tous les prise en charge de hello demande s’affiche dans hello **aide + support** panneau.

    ![Gérer les demandes de support](./media/storsimple-8000-contact-microsoft-support/managesupport2.png)

3. Sélectionnez une demande de support. Vous pouvez afficher le statut de hello et détails hello pour cette demande. Cliquez sur **+ nouveau message** si vous souhaitez toofollow haut de cette demande.

    ![Gérer les demandes de support](./media/storsimple-8000-contact-microsoft-support/managesupport3.png)

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


## <a name="next-steps"></a>Étapes suivantes

Découvrez comment trop[diagnostiquer et résoudre le périphérique de la gamme des problèmes connexes tooyour StorSimple 8000](storsimple-troubleshoot-deployment.md)
