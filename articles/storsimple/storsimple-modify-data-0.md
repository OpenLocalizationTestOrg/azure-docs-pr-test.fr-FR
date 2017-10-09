---
title: "aaaModify hello DATA 0 paramètres sur un appareil StorSimple | Documents Microsoft"
description: "Découvrez comment toouse Windows PowerShell pour StorSimple tooreconfigure hello interface réseau DATA 0 sur votre appareil StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 58e3d509-f425-4a7f-b650-d496a7c85193
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: caec51c3344d953299253301c2a0d7577d553c6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="modify-hello-data-0-network-interface-settings-on-your-storsimple-device"></a>Modifier les paramètres d’interface hello données réseau 0 sur votre appareil StorSimple
## <a name="overview"></a>Vue d'ensemble
Votre appareil Microsoft Azure StorSimple a six interfaces réseau allant de DATA 0 tooDATA 5. Hello interface de données 0 est toujours configurée via l’interface Windows PowerShell de hello ou de la console série de hello et est automatiquement activé pour le cloud. Notez que vous ne pouvez pas configurer d’interface réseau DATA 0 via hello portail Azure classic. 

Hello DATA 0 interface est d’abord configuré via l’Assistant d’installation hello lors du déploiement initial de l’appareil StorSimple hello. Lors de l’appareil de hello est dans un mode de fonctionnement, vous devrez peut-être tooreconfigure DATA 0 paramètres. Ce didacticiel fournit deux méthodes de paramètres de réseau 0 toomodify données, à la fois par le biais de Windows PowerShell pour StorSimple.

Après avoir lu ce didacticiel, vous pourrez :

* Modifier des données 0 paramètre l’Assistant Installation hello réseau
* Modifier les paramètres de réseau 0 données via hello `Set-HcsNetInterface` applet de commande

## <a name="modify-data-0-network-settings-through-setup-wizard"></a>Modification des paramètres réseau de DATA 0 via l’Assistant Installation
Vous pouvez reconfigurer les paramètres de réseau 0 de données en vous connectant interface Windows PowerShell de toohello de votre appareil StorSimple et de lancer une session de l’Assistant d’installation. Effectuer hello suivant les étapes toomodify DATA 0 paramètres :

#### <a name="toomodify-data-0-network-settings-through-setup-wizard"></a>paramètres de réseau 0 toomodify données via l’Assistant Installation
1. Dans le menu de console série hello, sélectionnez l’option 1, **connecter avec un accès complet**. Lorsque vous y êtes invité fournir hello **mot de passe administrateur**. mot de passe par défaut Hello est `Password1`.
2. À l’invite de commandes hello, tapez :
   
    `Invoke-HcsSetupWizard`
3. Un Assistant d’installation s’affiche toohelp vous configurez hello DATA 0 interface de votre appareil. Fournir de nouvelles valeurs de masque de réseau, la passerelle et adresse IP de hello.

> [!NOTE]
> Hello fixé contrôleurs IPs devez toobe reconfiguré via hello **configurer** page de l’appareil StorSimple hello Bonjour portail Azure classic. Pour plus d’informations, consultez trop[modifier des interfaces réseau](storsimple-modify-device-config.md#modify-network-interfaces).
> 
> 

## <a name="modify-data-0-network-settings-through-set-hcsnetinterface-cmdlet"></a>Modification des paramètres réseau de DATA 0 via l’applet de commande Set-HcsNetInterface
Un tooreconfigure autre façon DATA 0 est d’interface réseau via l’utilisation de hello de hello `Set-HcsNetInterface` applet de commande. applet de commande Hello est exécuté à partir de l’interface Windows PowerShell de hello de votre appareil StorSimple. Lorsque vous utilisez cette procédure, les IP fixé du contrôleur hello peut également être configuré ici. Effectuer hello suivant les étapes toomodify hello DATA 0 paramètres : 

#### <a name="toomodify-data-0-network-settings-through-hello-set-hcsnetinterface-cmdlet"></a>paramètres de réseau 0 toomodify données via l’applet de commande Set-HcsNetInterface de hello
1. Dans le menu de console série hello, sélectionnez l’option 1, **connecter avec un accès complet**. Lorsque vous y êtes invité fournir le mot de passe administrateur de périphérique hello. mot de passe par défaut Hello est `Password1`.
2. À l’invite de commandes hello, tapez :
   
    `Set-HCSNetInterface -InterfaceAlias Data0 -IPv4Address <> -IPv4Netmask <> -IPv4Gateway <> -Controller0IPv4Address <> -Controller1IPv4Address <> -IsiScsiEnabled 1 -IsCloudEnabled 1`
   
    Dans les crochets hello en angle, tapez hello valeurs suivantes pour DATA 0 :
   
   * Adresse IPv4
   * Passerelle IPv4
   * Masque de sous-réseau IPv4
   * Adresse IPv4 fixe du contrôleur 0
   * Adresse IPv4 fixe du contrôleur 1
     
     Pour plus d’informations sur l’utilisation de hello de cette applet de commande, accédez trop[Windows PowerShell pour la référence d’applet de commande StorSimple](https://technet.microsoft.com/library/dn688161.aspx).

## <a name="next-steps"></a>Étapes suivantes
* tooconfigure les interfaces réseau autres que DATA 0, vous pouvez utiliser hello [page Configurer Bonjour portail Azure classic](storsimple-modify-device-config.md). 
* Si vous rencontrez des problèmes lors de la configuration des interfaces réseau, consultez trop[résoudre les problèmes de déploiement](storsimple-troubleshoot-deployment.md).

