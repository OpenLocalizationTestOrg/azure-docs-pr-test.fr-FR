---
title: aaaPowerShell pour la gestion des appareils StorSimple | Documents Microsoft
description: "Découvrez comment toouse Windows PowerShell pour StorSimple toomanage votre appareil StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 0ff3bb0d-897a-4676-bdcb-402c2628dac5
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/18/2016
ms.author: alkohli@microsoft.com
ms.openlocfilehash: 1adcbb8bb89e3e3b4f328aac198690476c2a78cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-windows-powershell-for-storsimple-tooadminister-your-device"></a>Utiliser Windows PowerShell pour StorSimple tooadminister votre appareil
## <a name="overview"></a>Vue d'ensemble
Windows PowerShell pour StorSimple fournit une interface de ligne de commande que vous pouvez utiliser toomanage votre appareil Microsoft Azure StorSimple. Comme le suggère le nom hello, il est une interface de ligne de commande basé sur Windows PowerShell, qui est créée dans une instance d’exécution contrainte. Du point de vue hello d’utilisateur hello à la ligne de commande hello, une instance d’exécution contrainte apparaît comme une version limitée de Windows PowerShell. Tout en conservant certaines hello des fonctionnalités de base de Windows PowerShell, cette interface possède les applets de commande dédiées supplémentaires pour la gestion de votre appareil Microsoft Azure StorSimple. 

Cet article décrit hello Windows PowerShell pour StorSimple fonctionnalités, y compris comment vous pouvez connecter toothis interface et contient des procédures toostep-à-pas de liens ou des flux de travail que vous pouvez effectuer à l’aide de cette interface. flux de travail Hello comprendre comment tooregister votre appareil, configurez l’interface de réseau hello sur votre appareil, installer les mises à jour nécessitent toobe de périphérique hello en mode maintenance, de modifier l’état de l’appareil hello, et résoudre les problèmes que vous pouvez rencontrer.

Après avoir lu cet article, vous pourrez :

* Connectez l’appareil StorSimple tooyour à l’aide de Windows PowerShell pour StorSimple.
* Administrez votre appareil StorSimple à l’aide de Windows PowerShell for StorSimple.
* Obtenez de l’aide dans Windows PowerShell for StorSimple.

> [!NOTE]
> * Windows PowerShell pour les applets de commande StorSimple permettent de toomanage votre appareil StorSimple à partir d’une console série ou à distance via la communication à distance de Windows PowerShell. Pour plus d’informations sur chacune des cmdlets hello qui peut être utilisé dans cette interface, consultez trop[référence d’applet de commande pour Windows PowerShell pour StorSimple](https://technet.microsoft.com/library/dn688168.aspx).
> * applets de commande Azure PowerShell StorSimple Hello sont une autre collection d’applets de commande qui permettent de tooautomate au niveau du service StorSimple et les tâches de migration à partir de la ligne de commande hello. Pour plus d’informations sur hello applets de commande Azure PowerShell pour StorSimple, accédez à toohello [référence d’applet de commande Azure StorSimple](/powershell/module/azure/?view=azuresmps-3.7.0).
> 
> 

Vous pouvez accéder hello Windows PowerShell pour StorSimple à l’aide d’une des méthodes suivantes de hello :

* [Connecter la console série du périphérique tooStorSimple](#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console)
* [Se connecter à distance tooStorSimple à l’aide de Windows PowerShell](#connect-remotely-to-storsimple-using-windows-powershell-for-storsimple)

## <a name="connect-toowindows-powershell-for-storsimple-via-hello-device-serial-console"></a>Se connecter tooWindows PowerShell pour StorSimple via la console série du périphérique hello
Vous pouvez [télécharger PuTTY](http://www.putty.org/) ou similaires émulation logicielle tooconnect tooWindows PowerShell pour StorSimple. Vous devez tooconfigure PuTTY spécifiquement tooaccess hello appareil Microsoft Azure StorSimple. Hello rubriques suivantes contiennent les étapes détaillées sur la façon tooconfigure PuTTy et connecter toohello appareil. Différentes options de menu de console série de hello sont également expliquées.

### <a name="putty-settings"></a>Paramètres puTTY
Assurez-vous que vous utilisez hello suivant l’interface Windows PowerShell de paramètres PuTTY tooconnect toohello à partir de la console série de hello.

#### <a name="tooconfigure-putty"></a>tooconfigure PuTTY
1. Bonjour PuTTY **Reconfiguration** la boîte de dialogue hello **catégorie** volet, sélectionnez **clavier**.
2. Vérifiez que hello options suivantes sont sélectionnées (ce sont les paramètres par défaut hello lorsque vous démarrez une nouvelle session). 
   
   | Élément du clavier | Sélectionnez |
   | --- | --- |
   | Touche Retour arrière |Ctrl+? (127) |
   | Touches Origine et Fin |Standard |
   | Touches de fonction et pavé numérique |ÉCHAP[n~ |
   | État initial des touches de direction |Normal |
   | État initial du pavé numérique |Normal |
   | Activer des fonctionnalités supplémentaires du clavier |Ctrl+Alt est différent de AltGr |
   
    ![Paramètres de PuTTY pris en charge](./media/storsimple-windows-powershell-administration/IC740877.png)
3. Cliquez sur **Apply**.
4. Bonjour **catégorie** volet, sélectionnez **traduction**.
5. Bonjour **jeu de caractères distant** zone de liste, sélectionnez **UTF-8**.
6. Sous **Gestion des caractères de dessin de ligne**, sélectionnez **Utiliser des points de code de dessin de ligne Unicode**. Hello l’illustration suivante montre les sélections PuTTY correctes hello.
   
    ![Paramètres puTTY pour UTF](./media/storsimple-windows-powershell-administration/IC740878.png)
7. Cliquez sur **Apply**.

Vous pouvez maintenant utiliser la console série du périphérique toohello tooconnect PuTTY en procédant comme hello comme suit.

[!INCLUDE [storsimple-use-putty](../../includes/storsimple-use-putty.md)]

### <a name="about-hello-serial-console"></a>Sur la console série de hello
Lorsque vous accédez à interface Windows PowerShell de hello de votre unité StorSimple via la console série de hello, un message de bannière s’affiche, suivi par les options de menu. 

message de bannière Hello contient des informations de périphérique StorSimple base telles que le modèle de hello, nom, version du logiciel installé et l’état du contrôleur hello vous accédez à. Hello suivant image montre un exemple de message de bannière.

![Message de bannière série](./media/storsimple-windows-powershell-administration/IC741098.png)

> [!IMPORTANT]
> Vous pouvez utiliser tooidentify de message de bannière hello que hello contrôleur que vous soyez connecté toois actif ou passif.
> 
> 

Hello ci-dessous illustre d’image hello différentes options d’instance d’exécution qui sont disponibles dans le menu de console série hello.

![Inscrire votre appareil 2](./media/storsimple-windows-powershell-administration/IC740906.png)

Vous pouvez choisir parmi hello suivant les paramètres :

1. **Ouvrez une session avec un accès complet** cette option vous permet de tooconnect (avec les informations d’identification appropriées hello) toohello **SSAdminConsole** instance d’exécution sur le contrôleur de hello local. (le contrôleur local de hello est contrôleur hello auquel vous accédez actuellement via la console série de hello de votre appareil StorSimple.) Cette option peut également être utilisée tooallow tooaccess de Support technique de Microsoft sans restriction tootroubleshoot d’instance d’exécution (une session de support) des problèmes de périphériques possible. Une fois que vous utilisez l’option 1 toolog, vous pouvez autoriser ingénieur de Support technique de Microsoft hello tooaccess sans restriction d’instance d’exécution en exécutant une cmdlet spécifique. Pour plus d’informations, consultez trop[démarrer une session de support](storsimple-contact-microsoft-support.md#start-a-support-session-in-windows-powershell-for-storsimple).
2. **Connectez-vous au contrôleur toopeer avec un accès complet** cette option est la même hello en tant qu’option 1, à ceci près que vous pouvez vous connecter (avec les informations d’identification appropriées hello) toohello **SSAdminConsole** instance d’exécution sur le contrôleur homologue de hello. Étant donné que l’appareil StorSimple hello est un appareil haute disponibilité avec deux contrôleurs dans une configuration actif / passif, homologue fait référence toohello autre contrôleur de périphérique hello auquel vous accédez via la console série de hello).
   Toooption similaires 1, cette option peut également être instance d’exécution de tooaccess sans restriction de Support technique de Microsoft tooallow utilisé sur un contrôleur homologue.
3. **Se connecter avec un accès limité** cette option est utilisée tooaccess interface Windows PowerShell en mode limited. Des informations d’identification d’accès ne vous sont pas demandées. Cette option connecte tooa plus restreint instance d’exécution toooptions 1 et 2.  Certaines des tâches hello qui sont disponibles via l’option 1 qui **ne peut pas* être effectuée dans cette instance d’exécution sont :
   
   * Réinitialiser les paramètres d’usine toohello
   * Mot de passe de modification hello
   * Activer ou désactiver l’accès du support
   * Appliquer des mises à jour
   * Installer des correctifs 

    > [!NOTE]
    > Cette option de hello préféré est si vous avez oublié de mot de passe administrateur de périphérique hello et ne peut pas se connecter via l’option 1 ou 2.

4. **Modifier la langue** cette option vous permet de langue d’affichage toochange hello sur l’interface Windows PowerShell de hello. langues Hello prises en charge sont l’anglais, japonais, russe, Français, coréen, espagnol, italien, allemand, chinois et portugais (Brésil).

## <a name="connect-remotely-toostorsimple-using-windows-powershell-for-storsimple"></a>Se connecter à distance tooStorSimple à l’aide de Windows PowerShell pour StorSimple
Vous pouvez utiliser l’appareil StorSimple Windows PowerShell remoting tooconnect tooyour. Quand vous vous connectez de cette façon, vous ne voyez pas de menu. (Vous consultez un menu uniquement si vous utilisez la console série de hello sur hello périphérique tooconnect. Connexion à distance vous amène directement toohello équivalent de « option 1 – accès total » sur la console série de hello.) Avec accès à distance de Windows PowerShell, vous vous connectez tooa les instance d’exécution spécifique. Vous pouvez également spécifier la langue d’affichage hello. 

Bonjour langue d’affichage est indépendante du langage hello que vous définissez à l’aide de hello **modifier la langue** option dans le menu de console série hello. PowerShell distant reprendra automatiquement aux paramètres régionaux hello du périphérique de hello que vous vous connectez à partir de si none est spécifié.

> [!NOTE]
> Si vous travaillez avec les hôtes virtuels Microsoft Azure et les appareils virtuels StorSimple, vous pouvez utiliser Windows PowerShell remoting et hello hôte virtuel tooconnect toohello périphérique virtuel. Si vous avez configuré un emplacement de partage sur l’ordinateur hôte de hello sur les informations de toosave à partir de la session Windows PowerShell de hello, sachez que hello que tout le monde principal inclut uniquement les utilisateurs authentifiés. Par conséquent, si vous avez défini un accès hello partage tooallow par tout le monde et vous connectez sans spécifier les informations d’identification, entité de sécurité anonyme non authentifié hello sera utilisée et vous verrez une erreur. toofix ce problème, sur hello partager hôte, vous devez activer le compte invité de hello et accorder à part de toohello hello invité compte un accès complet ou que vous devez spécifier les informations d’identification valides avec hello applet de commande Windows PowerShell.
> 
> 

Vous pouvez utiliser HTTP ou HTTPS tooconnect via la communication à distance de Windows PowerShell. Suivez les instructions de hello Bonjour suivant didacticiels :

* [Se connecter à distance en utilisant HTTP](storsimple-remote-connect.md#connect-through-http)
* [Se connecter à distance en utilisant HTTPS](storsimple-remote-connect.md#connect-through-https)

## <a name="connection-security-considerations"></a>Considérations sur la sécurité des connexions
Lorsque vous décidez comment tooconnect tooWindows PowerShell pour StorSimple, considérez les éléments suivants de hello :

* Connexion directe toohello console série du périphérique est sécurisé, mais il connexion console série toohello sur les commutateurs de réseau n’est pas. Soyez prudent hello des risques de sécurité lors de la connexion toodevice série sur les commutateurs réseau.
* Connexion via une session HTTP peut offrir davantage de sécurité que la connexion via la console série de hello sur le réseau. Bien que cela n’est pas la méthode hello plus sécurisée, il est acceptable sur des réseaux approuvés.
* Connexion via une session HTTPS est hello plus sûre et hello option recommandée.

## <a name="administer-your-storsimple-device-using-windows-powershell-for-storsimple"></a>Administrer votre appareil StorSimple à l’aide de Windows PowerShell pour StorSimple
Hello tableau suivant présente un résumé de toutes les tâches de gestion courantes hello et flux de travail complexes qui peut être effectuées dans l’interface Windows PowerShell de hello de votre appareil StorSimple. Pour plus d’informations sur chaque flux de travail, cliquez sur l’entrée appropriée de hello dans la table de hello.

#### <a name="windows-powershell-for-storsimple-workflows"></a>Flux de travail Windows PowerShell pour StorSimple
| Si vous le souhaitez toodo... | Suivez cette procédure. |
| --- | --- |
| Inscrire votre appareil |[Configurer et inscrire l’appareil de hello à l’aide de Windows PowerShell pour StorSimple](storsimple-deployment-walkthrough.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple) |
| Configurer le proxy web </br>Afficher les paramètres de proxy web |[Configurer le proxy web pour votre appareil StorSimple](storsimple-configure-web-proxy.md) |
| Modifier les paramètres d’interface réseau DATA 0 sur votre appareil |[Modifier l’interface réseau DATA 0 pour votre appareil StorSimple](storsimple-modify-data-0.md) |
| Arrêter un contrôleur  </br> Redémarrage ou arrêt d’un contrôleur </br> Arrêt d'un appareil</br>Rétablir les paramètres par défaut de hello appareil toofactory |[Gérer les contrôleurs de l’appareil](storsimple-manage-device-controller.md) |
| Installer des mises à jour et des correctifs en mode maintenance |[Mettre à jour votre appareil](storsimple-update-device.md) |
| Entrer en mode maintenance  </br>Quitter le mode maintenance |[Modes de l’appareil StorSimple](storsimple-device-modes.md) |
| Créer un package de support </br>Déchiffrer et modifier un package de support |[Création et gestion d’un package de prise en charge](storsimple-create-manage-support-package.md) |
| Démarrer une session de support</br> |[Démarrage d’une session de support dans Windows PowerShell pour StorSimple](storsimple-create-manage-support-package.md#manually-create-a-support-package) |

## <a name="get-help-in-windows-powershell-for-storsimple"></a>Obtenir de l’aide dans Windows PowerShell pour StorSimple
Dans Windows PowerShell pour StorSimple, une aide sur les applets de commande est disponible. Une version mise à jour en ligne de cette aide est également disponible, que vous pouvez utiliser tooupdate hello aide sur votre système.

Obtention d’aide dans cette interface est toothat similaires dans Windows PowerShell, et la plupart des applets de commande relatives à l’aide de hello ne fonctionnera pas. Vous trouverez une aide pour Windows PowerShell en ligne dans la bibliothèque TechNet de hello : [écriture de scripts avec Windows PowerShell](http://go.microsoft.com/fwlink/?LinkID=108518).

Hello Voici une brève description de types hello d’aide pour cette interface Windows PowerShell, y compris comment tooupdate hello aide.

#### <a name="tooget-help-for-a-cmdlet"></a>tooget aide pour une applet de commande
* tooget aide pour toute applet de commande ou d’une fonction, hello utilisez commande suivante :`Get-Help <cmdlet-name>`
* tooget aide en ligne pour une applet de commande, utilisez hello applet de commande précédente avec hello `-Online` paramètre :`Get-Help <cmdlet-name> -Online`
* Pour l’aide complète, vous pouvez utiliser hello `–Full` paramètre et pour obtenir des exemples, utilisez hello `–Examples` paramètre.

#### <a name="tooupdate-help"></a>tooupdate aide
Vous pouvez facilement mettre à jour hello aide dans l’interface Windows PowerShell hello. Effectuer hello suivant les étapes tooupdate hello aide sur votre système.

#### <a name="tooupdate-cmdlet-help"></a>applet de commande tooupdate Help
1. Démarrez Windows PowerShell avec hello **exécuter en tant qu’administrateur** option.
2. À l’invite de commandes hello, tapez :`Update-Help`
3. Hello mis à jour l’aide à installer les fichiers.
4. Après installation des fichiers d’aide hello, tapez : `Get-Help Get-Command`. Ceci affiche une liste des applets de commande pour lesquelles de l’aide est disponible.

> [!NOTE]
> tooget une liste de toutes les cmdlets disponibles hello dans une instance d’exécution, ouvrez une session dans l’option de menu correspondante toohello et exécutez hello `Get-Command` applet de commande.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
Si vous rencontrez des problèmes avec votre appareil StorSimple lorsque vous effectuez une des hello au-dessus de flux de travail, consultez trop[outils de dépannage des déploiements de StorSimple](storsimple-troubleshoot-deployment.md#tools-for-troubleshooting-storsimple-deployments).

