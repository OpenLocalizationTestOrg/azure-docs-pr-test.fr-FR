---
title: "aaaConfigure CHAP pour appareil de série StorSimple 8000 | Documents Microsoft"
description: "Décrit comment tooconfigure hello CHAP Challenge Handshake Authentication Protocol () sur un appareil StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 467044d7-7885-4382-90bd-3148dbbd341f
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 272ef2c184f56ad262e55410357494c72e45cf83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-chap-for-your-storsimple-device"></a>Configuration de CHAP pour votre appareil StorSimple
Ce didacticiel explique comment tooconfigure CHAP pour votre appareil StorSimple. procédure de Hello détaillée dans cet article s’applique tooStorSimple 8000 series, ainsi que les appareils StorSimple 1200.

CHAP est l’abréviation de Challenge Handshake Authentication Protocol. Il est un schéma d’authentification utilisé par les serveurs toovalidate hello identité des clients distants. vérification de Hello est basée sur un mot de passe partagé ou un secret. Le protocole CHAP peut être à sens unique (unidirectionnel) ou mutuel (bidirectionnel). Authentification CHAP unidirectionnelle est lorsque hello cible authentifie un initiateur. Authentification CHAP mutuelle ou inverse, sur hello autre part, requiert que la cible de hello authentifier l’initiateur de hello et puis hello initiateur doit authentifier hello cible. L’authentification de l’initiateur peut être implémentée sans authentification cible. Toutefois, l’authentification cible peut être implémentée uniquement si l’authentification de l’initiateur est également implémentée. 

Comme meilleure pratique, nous vous recommandons de que vous utilisez la sécurité CHAP. tooenhance iSCSI.

> [!NOTE]
> N’oubliez pas que IPSEC n’est pas actuellement pris en charge sur les appareils StorSimple.
> 
> 

paramètres de CHAP de Hello sur l’appareil StorSimple hello peuvent être configurés dans hello suivant façons :

* Authentification unidirectionnelle ou unidirectionnelle
* Authentification bidirectionnelle, mutuelle ou inverse

Dans chacun de ces cas, le portail hello pour appareil de hello et le logiciel initiateur iSCSI du serveur hello doit toobe configuré. Hello des instructions détaillées sur cette configuration sont décrites dans hello suivant le didacticiel.

## <a name="unidirectional-or-one-way-authentication"></a>Authentification unidirectionnelle ou unidirectionnelle
Dans une authentification unidirectionnelle, cible de hello authentifie initiateur de hello. Cette authentification nécessite de configurer les paramètres de l’initiateur CHAP hello sur l’appareil StorSimple hello et hello le logiciel initiateur iSCSI sur l’ordinateur hôte de hello. Hello des procédures détaillées pour votre appareil StorSimple et hôte Windows sont décrites ci-après.

#### <a name="tooconfigure-your-device-for-one-way-authentication"></a>tooconfigure votre appareil avec l’authentification unidirectionnelle
1. Bonjour portail Azure classic sur hello **périphériques** , cliquez sur hello **configurer** onglet.
   
    ![CHAP Initiator](./media/storsimple-configure-chap/IC740943.png)
2. Faites défiler vers le bas sur cette page et hello **initiateur CHAP** section :
   
   1. Indiquez un nom d’utilisateur pour votre initiateur CHAP.
   2. Spécifiez un mot de passe pour votre initiateur CHAP.
      
    > [!IMPORTANT]
    > nom d’utilisateur CHAP Hello doit contenir 233 caractères maximum. mot de passe CHAP Hello doit comprendre entre 12 et 16 caractères. Un nom d’utilisateur ou le mot de passe plus long entraîne un échec d’authentification sur l’ordinateur hôte de Windows hello.
   
   3. Confirmer le mot de passe hello.
3. Cliquez sur **Enregistrer**. Un message de confirmation s’affiche. Cliquez sur **OK** modifications de hello toosave.

#### <a name="tooconfigure-one-way-authentication-on-hello-windows-host-server"></a>serveur hôte de l’authentification unidirectionnelle de tooconfigure sur hello Windows
1. Sur le serveur hôte de Windows hello, démarrez l’initiateur iSCSI hello.
2. Bonjour **propriétés de l’initiateur iSCSI** fenêtre, effectuez hello comme suit :
   
   1. Cliquez sur hello **découverte** onglet.
      
       ![iSCSI Initiator Properties](./media/storsimple-configure-chap/IC740944.png)
   2. Cliquez sur **Discover Portal**.
3. Bonjour **détecter un portail cible** boîte de dialogue :
   
   1. Spécifier l’adresse IP de hello de votre appareil.
   2. Cliquez sur **Avancé**.
      
       ![Découvrir le portail cible](./media/storsimple-configure-chap/IC740945.png)
4. Bonjour **paramètres avancés** boîte de dialogue :
   
   1. Sélectionnez hello **ouverture de session activer CHAP** case à cocher.
   2. Bonjour **nom** champ, le nom d’utilisateur hello approvisionnement que vous avez spécifié pour hello initiateur CHAP dans le portail classique de hello.
   3. Bonjour **secret cible** champ, alimentation hello mot de passe que vous avez spécifié pour hello initiateur CHAP dans le portail classique de hello.
   4. Cliquez sur **OK**.
      
       ![Paramètres avancés - Généraux](./media/storsimple-configure-chap/IC740946.png)
5. Sur hello **cibles** onglet Hello **propriétés de l’initiateur iSCSI** fenêtre, l’état du périphérique hello doit apparaître en tant que **connecté**. Si vous utilisez un appareil StorSimple 1200, chaque volume est monté en tant que cible iSCSI comme indiqué ci-dessous. Par conséquent, étapes 3 et 4 devez toobe répété pour chaque volume.
   
    ![Volumes montés en tant que cibles distinctes](./media/storsimple-configure-chap/chap4.png)
   
   > [!IMPORTANT]
   > Si vous modifiez le nom iSCSI de hello, nouveau nom de hello sera utilisé pour les nouvelles sessions iSCSI. Les nouveaux paramètres ne sont pas appliqués aux sessions existantes tant que vous n’avez pas quitté puis relancé la session.
   > 
   > 

Pour plus d’informations sur la configuration du protocole CHAP sur le serveur hôte de Windows hello, accédez trop[considérations supplémentaires](#additional-considerations).

## <a name="bidirectional-or-mutual-authentication"></a>Authentification bidirectionnelle ou mutuelle
Dans une authentification bidirectionnelle, cible de hello authentifie l’initiateur de hello et puis initiateur de hello authentifie la cible de hello. Cela nécessite de paramètres de l’initiateur hello utilisateur tooconfigure hello CHAP, ainsi que hello inverse les paramètres CHAP sur l’appareil de hello et le logiciel initiateur iSCSI sur l’hôte de hello. Hello procédures suivantes décrivent l’authentification mutuelle hello étapes tooconfigure sur l’appareil de hello et sur l’ordinateur hôte de Windows hello.

#### <a name="tooconfigure-your-device-for-mutual-authentication"></a>tooconfigure votre appareil pour l’authentification mutuelle
1. Bonjour portail Azure classic sur hello **périphériques** , cliquez sur hello **configurer** onglet.
   
    ![CHAP Target](./media/storsimple-configure-chap/IC740948.png)
2. Faites défiler vers le bas sur cette page et hello **cible CHAP** section :
   
   1. Indiquez le **nom d’utilisateur CHAP inverse** de votre appareil.
   2. Indiquez le **mot de passe CHAP inverse** de votre appareil.
   3. Confirmer le mot de passe hello.
3. Bonjour **initiateur CHAP** section :
   
   1. Indiquez un **nom d’utilisateur** pour votre appareil.
   2. Indiquez un **mot de passe** pour votre appareil.
   3. Confirmer le mot de passe hello.
4. Cliquez sur **Enregistrer**. Un message de confirmation s’affiche. Cliquez sur **OK** modifications de hello toosave.

#### <a name="tooconfigure-bidirectional-authentication-on-hello-windows-host-server"></a>serveur hôte de tooconfigure une authentification bidirectionnelle sur hello Windows
1. Sur le serveur hôte de Windows hello, démarrez l’initiateur iSCSI hello.
2. Bonjour **propriétés de l’initiateur iSCSI** fenêtre, cliquez sur hello **Configuration** onglet.
3. Cliquez sur **CHAP**.
4. Bonjour **iSCSI Initiator code Secret CHAP mutuel** boîte de dialogue :
   
   1. Hello de type **inverser un mot de passe CHAP** que vous avez configuré dans hello portail Azure classic.
   2. Cliquez sur **OK**.
      
       ![Secret CHAP mutuel de l’initiateur iSCSI](./media/storsimple-configure-chap/IC740949.png)
5. Cliquez sur hello **cibles** onglet.
6. Cliquez sur hello **Connect** bouton. 
7. Bonjour **connecter tooTarget** boîte de dialogue, cliquez sur **avancé**.
8. Bonjour **propriétés avancées** boîte de dialogue :
   
   1. Sélectionnez hello **ouverture de session activer CHAP** case à cocher.
   2. Bonjour **nom** champ, le nom d’utilisateur hello approvisionnement que vous avez spécifié pour hello initiateur CHAP dans le portail classique de hello.
   3. Bonjour **secret cible** champ, alimentation hello mot de passe que vous avez spécifié pour hello initiateur CHAP dans le portail classique de hello.
   4. Sélectionnez hello **effectuer une authentification mutuelle** case à cocher.
      
       ![Paramètres avancés - Authentification mutuelle](./media/storsimple-configure-chap/IC740950.png)
   5. Cliquez sur **OK** configuration CHAP de hello toocomplete

Pour plus d’informations sur la configuration du protocole CHAP sur le serveur hôte de Windows hello, accédez trop[considérations supplémentaires](#additional-considerations).

## <a name="additional-considerations"></a>Considérations supplémentaires
Hello **connexion rapide** fonctionnalité ne prend pas en charge les connexions pour lesquelles le protocole CHAP est activé. Lorsque le protocole CHAP est activé, assurez-vous que vous utilisez hello **Connect** bouton est disponible sur hello **cibles** cible de tooa tooconnect onglet.

![Se connecter tootarget](./media/storsimple-configure-chap/IC740947.png)

Bonjour **connecter tooTarget** boîte de dialogue qui est présenté, sélectionnez hello **ajouter la liste des cibles favorites toohello connexion** case à cocher. Cela garantit que chaque fois que hello ordinateur redémarre, une tentative est faite toorestore hello connexion toohello cibles favorites des iSCSI.

## <a name="errors-during-configuration"></a>Erreurs lors de la configuration
Si votre configuration CHAP est incorrecte, vous êtes probablement toosee un **Échec de l’authentification** message d’erreur.

## <a name="verification-of-chap-configuration"></a>Vérification de la configuration CHAP
Vous pouvez vérifier que CHAP est utilisé, hello comme suit.

#### <a name="tooverify-your-chap-configuration"></a>tooverify votre configuration CHAP
1. Cliquez sur **Favorite Targets**.
2. Sélectionnez la cible de hello pour lequel vous avez activé l’authentification.
3. Cliquez sur **Details**.
   
    ![Cibles favorites des propriétés de l’initiateur iSCSI](./media/storsimple-configure-chap/IC740951.png)
4. Bonjour **détails sur les cibles favorites** boîte de dialogue, notez hello entrée hello **authentification** champ. Si la configuration de hello a réussi, vous devriez voir **CHAP**.
   
    ![Détails sur les cibles favorites](./media/storsimple-configure-chap/IC740952.png)

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur la [sécurité StorSimple](storsimple-security.md).
* En savoir plus sur [à l’aide de hello tooadminister du service StorSimple Manager votre appareil StorSimple](storsimple-manager-service-administration.md).

