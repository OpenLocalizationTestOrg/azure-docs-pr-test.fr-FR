---
title: "aaaConnect à distance à l’appareil StorSimple tooyour | Documents Microsoft"
description: "Explique comment tooconfigure votre appareil pour la gestion à distance et comment tooconnect tooWindows PowerShell pour StorSimple via HTTP ou HTTPS."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 923377aa-f451-4656-87de-5e95a34a6a2a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 55ed8fcdd997901301e0adc164a302216cde0332
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-remotely-tooyour-storsimple-8000-series-device"></a>Se connecter à distance les appareils tooyour StorSimple 8000

## <a name="overview"></a>Vue d'ensemble
Vous pouvez utiliser l’appareil StorSimple Windows PowerShell remoting tooconnect tooyour. Quand vous vous connectez de cette façon, vous ne voyez pas de menu. (Vous consultez un menu uniquement si vous utilisez la console série de hello sur hello appareil tooconnect.) Avec accès à distance de Windows PowerShell, vous vous connectez tooa les instance d’exécution spécifique. Vous pouvez également spécifier la langue d’affichage hello. 

Pour plus d’informations sur l’utilisation de Windows PowerShell remoting toomanage votre appareil, consultez trop[utiliser Windows PowerShell pour StorSimple tooadminister votre appareil StorSimple](storsimple-windows-powershell-administration.md).

Ce didacticiel explique comment tooconfigure votre appareil pour l’administration à distance et puis tooconnect tooWindows PowerShell pour StorSimple. Vous pouvez utiliser HTTP ou HTTPS tooconnect via la communication à distance de Windows PowerShell. Toutefois, lorsque vous décidez comment tooconnect tooWindows PowerShell pour StorSimple, considérez les éléments suivants de hello : 

* Connexion directe toohello console série du périphérique est sécurisé, mais il connexion console série toohello sur les commutateurs de réseau n’est pas. Soyez prudent hello des risques de sécurité lors de la connexion de la console série du périphérique toohello sur les commutateurs réseau. 
* Connexion via une session HTTP peut offrir davantage de sécurité que la connexion via la console série de hello réseau hello. Bien que cela n’est pas la méthode hello plus sécurisée, il est acceptable sur des réseaux approuvés. 
* La connexion via une session HTTPS avec un certificat auto-signé est hello plus sûre et hello option recommandée.

Vous pouvez vous connecter à distance interface Windows PowerShell de toohello. Cependant, l’appareil StorSimple tooyour accès à distance via l’interface Windows PowerShell de hello n’est pas activée par défaut. Vous devez tooenable la gestion à distance sur l’appareil de hello tout d’abord et que vous puis sur hello client qui est utilisé tooaccess votre appareil.

les étapes de Hello décrites dans cet article ont été effectuées sur un système hôte exécutant Windows Server 2012 R2.

## <a name="connect-through-http"></a>Se connecter via HTTP
Connexion tooWindows PowerShell pour StorSimple via une session HTTP offre davantage de sécurité que la connexion via la console série de hello de votre appareil StorSimple. Bien que cela n’est pas la méthode hello plus sécurisée, il est acceptable sur des réseaux approuvés.

Vous pouvez utiliser hello portail Azure classic ou gestion à distance du tooconfigure hello console série. Sélectionnez hello procédures suivantes :

* [Utiliser la gestion à distance de tooenable de portail classique Azure hello sur HTTP](#use-the-azure-classic-portal-to-enable-remote-management-over-http)
* [Utiliser la gestion à distance de hello console série tooenable sur HTTP](#use-the-serial-console-to-enable-remote-management-over-http)

Après avoir activé la gestion à distance, utilisez hello suivant la procédure tooprepare hello du client pour une connexion à distance.

* [Préparer le client de hello pour la connexion à distance](#prepare-the-client-for-remote-connection)

### <a name="use-hello-azure-classic-portal-tooenable-remote-management-over-http"></a>Utiliser la gestion à distance de tooenable de portail classique Azure hello sur HTTP
Effectuer hello suivant les étapes de gestion à distance de tooenable de portail classique Azure hello sur HTTP.

#### <a name="tooenable-remote-management-through-hello-azure-classic-portal"></a>tooenable de gestion à distance via le portail Azure classic de hello
1. Accédez à **Appareils** > **Configurer** pour votre appareil.
2. Faites défiler vers le bas toohello **gestion à distance** section.
3. Définissez **activer la gestion à distance** trop**Oui**.
4. Vous pouvez maintenant choisir tooconnect à l’aide de HTTP. (valeur par défaut hello est tooconnect via le protocole HTTPS). Assurez-vous que HTTP est sélectionné.
   
   > [!NOTE]
   > Une connexion via HTTP est acceptable uniquement sur des réseaux approuvés.
   > 
   > 
5. Cliquez sur **enregistrer** bas hello de page de hello.

### <a name="use-hello-serial-console-tooenable-remote-management-over-http"></a>Utiliser la gestion à distance de hello console série tooenable sur HTTP
Effectuer hello hello gestion des appareils console série tooenable à distance comme suit.

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a>tooenable de gestion à distance via la console série du périphérique hello
1. Dans le menu de console série hello, sélectionnez l’option 1. Pour plus d’informations sur l’utilisation de la console série de hello sur l’appareil de hello, accédez trop[connecter tooWindows PowerShell pour StorSimple via la console série du périphérique](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).
2. À l’invite de hello, tapez :`Enable-HcsRemoteManagement –AllowHttp`
3. Vous serez notifié des failles de sécurité hello de l’unité de toohello tooconnect HTTP. Quand vous y êtes invité, confirmez en tapant **O**.
4. Vérifiez que HTTP est activé en tapant : `Get-HcsSystem`
5. Vérifiez que hello **RemoteManagementMode** champ indique **HttpsAndHttpEnabled**.hello après l’illustration montre ces paramètres dans PuTTY.
   
     ![HTTPS et HTTP en série activés](./media/storsimple-remote-connect/HCS_SerialHttpsAndHttpEnabled.png)

### <a name="prepare-hello-client-for-remote-connection"></a>Préparer le client de hello pour la connexion à distance
Effectuer hello sur la gestion à distance de hello client tooenable comme suit.

#### <a name="tooprepare-hello-client-for-remote-connection"></a>client de hello tooprepare pour la connexion à distance
1. Démarrez une session Windows PowerShell en tant qu’administrateur.
2. Tapez hello commande tooadd hello IP adresse de la liste des hôtes approuvés du client toohello hello StorSimple périphérique suivante : 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
     Remplacez <*device_ip*> avec l’adresse IP de hello de votre appareil, par exemple : 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. Tapez ce qui suit hello toosave hello appareil informations d’identification dans une variable de commande : 
   
    ```
    $cred = Get-Credential
    ```
    
4. Dans la boîte de dialogue hello qui s’affiche :
   
   1. Nom d’utilisateur de type hello dans ce format : *device_ip\SSAdmin*.
   2. Tapez le mot de passe administrateur de périphérique hello qui a été défini lors de l’appareil de hello a été configuré avec l’Assistant Installation de hello. mot de passe Hello *Password1*.
5. Démarrer une session Windows PowerShell sur l’appareil de hello en tapant cette commande :
   
     `Enter-PSSession -Credential $cred -ConfigurationName SSAdminConsole -ComputerName <device_ip>`
   
   > [!NOTE]
   > toocreate une session Windows PowerShell pour une utilisation avec un appareil virtuel StorSimple de hello, ajouter hello `–Port` paramètre et spécifiez le port public hello que vous avez configuré dans la communication à distance pour un équipement virtuel StorSimple.
   > 
   > 
   
     À ce stade, vous devez disposer d’un appareil actif toohello de session à distance Windows PowerShell.
   
    ![Accès distant PowerShell en utilisant HTTP](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTP.png)

## <a name="connect-through-https"></a>Se connecter via HTTPS
Connexion tooWindows PowerShell pour StorSimple via une session HTTPS est hello plus sûre et la méthode de connexion à distance appareil de Microsoft Azure StorSimple tooyour recommandée. Hello procédures suivantes explique comment tooset des hello séries console et les ordinateurs clients afin que vous puissiez utiliser HTTPS tooconnect tooWindows PowerShell pour StorSimple.

Vous pouvez utiliser hello portail Azure classic ou gestion à distance du tooconfigure hello console série. Sélectionnez hello procédures suivantes :

* [Utiliser la gestion à distance de tooenable de portail classique Azure hello sur HTTPS](#use-the-azure-classic-portal-to-enable-remote-management-over-https)
* [Utiliser la gestion à distance de hello console série tooenable sur HTTPS](#use-the-serial-console-to-enable-remote-management-over-https)

Après avoir activé la gestion à distance, utilisez hello suivant les procédures tooprepare hello ordinateur hôte pour une gestion à distance et se connecter toohello appareil à partir de l’hôte distant de hello.

* [Préparer l’hôte de hello pour la gestion à distance](#prepare-the-host-for-remote-management)
* [Se connecter toohello appareil à partir de l’hôte distant de hello](#connect-to-the-device-from-the-remote-host)

### <a name="use-hello-azure-classic-portal-tooenable-remote-management-over-https"></a>Utiliser la gestion à distance de tooenable de portail classique Azure hello sur HTTPS
Effectuer hello suivant les étapes de gestion à distance de hello tooenable de portail classique Azure via le protocole HTTPS.

#### <a name="tooenable-remote-management-over-https-from-hello-azure-classic-portal"></a>tooenable de gestion à distance via HTTPS à partir de hello portail Azure classic
1. Accédez à **Appareils** > **Configurer** pour votre appareil.
2. Faites défiler vers le bas toohello **gestion à distance** section.
3. Définissez **activer la gestion à distance** trop**Oui**.
4. Vous pouvez maintenant choisir tooconnect à l’aide de HTTPS. (valeur par défaut hello est tooconnect via le protocole HTTPS). Assurez-vous que HTTPS est sélectionné. 
5. Cliquez sur **Télécharger le certificat de gestion à distance**. Spécifiez un emplacement toosave ce fichier. Vous devez tooinstall ce certificat sur l’ordinateur client ou l’hôte de hello que vous allez utiliser tooconnect toohello appareil.
6. Cliquez sur **enregistrer** bas hello de page de hello.

### <a name="use-hello-serial-console-tooenable-remote-management-over-https"></a>Utiliser la gestion à distance de hello console série tooenable sur HTTPS
Effectuer hello hello gestion des appareils console série tooenable à distance comme suit.

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a>tooenable de gestion à distance via la console série du périphérique hello
1. Dans le menu de console série hello, sélectionnez l’option 1. Pour plus d’informations sur l’utilisation de la console série de hello sur l’appareil de hello, accédez trop[connecter tooWindows PowerShell pour StorSimple via la console série du périphérique](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).
2. À l’invite de hello, tapez : 
   
     `Enable-HcsRemoteManagement`
   
    Ceci doit normalement activer HTTPS sur votre appareil.
3. Vérifiez que HTTPS a été activé en tapant : 
   
     `Get-HcsSystem`
   
    Vérifiez que hello **RemoteManagementMode** champ indique **HttpsEnabled**.hello après l’illustration montre ces paramètres dans PuTTY.
   
     ![HTTPS en série activé](./media/storsimple-remote-connect/HCS_SerialHttpsEnabled.png)
4. À partir de la sortie de hello de `Get-HcsSystem`, copiez le numéro de série hello du périphérique de hello et l’enregistrer pour une utilisation ultérieure.
   
   > [!NOTE]
   > numéro de série Hello mappe le nom CN de toohello dans le certificat de hello.
   > 
   > 
5. Obtenez un certificat de gestion à distance en tapant : 
   
     `Get-HcsRemoteManagementCert`
   
    Une similaire toohello suivant du certificat s’affiche.
   
    ![Obtenir un certificat de gestion à distance](./media/storsimple-remote-connect/HCS_GetRemoteManagementCertificate.png)
6. Copier les informations de hello certificat hello de **---BEGIN CERTIFICATE---** trop**---END CERTIFICATE---** dans un éditeur de texte tel que le bloc-notes et enregistrez-le en tant que fichier .cer. (Vous allez copier cet hôte distant tooyour de fichier lorsque vous préparez l’ordinateur hôte de hello.)
   
   > [!NOTE]
   > toogenerate un nouveau certificat, utilisez hello `Set-HcsRemoteManagementCert` applet de commande.
   > 
   > 

### <a name="prepare-hello-host-for-remote-management"></a>Préparer l’hôte de hello pour la gestion à distance
l’ordinateur hôte pour une connexion à distance qui utilise une session HTTPS, tooprepare hello effectuer hello procédures suivantes :

* [Importer le fichier .cer hello dans le magasin racine de hello du client de hello ou un hôte distant](#to-import-the-certificate-on-the-remote-host).
* [Ajouter hello appareil des numéros de série toohello fichier hosts sur votre hôte distant](#to-add-device-serial-numbers-to-the-remote-host).

Chacune de ces procédures est décrite ci-dessous.

#### <a name="tooimport-hello-certificate-on-hello-remote-host"></a>certificat de hello tooimport sur l’hôte distant de hello
1. Avec le bouton droit de fichier .cer hello et sélectionnez **installer le certificat**. Ceci démarrera hello Assistant Importation de certificat.
   
    ![Assistant Importation de certificat 1](./media/storsimple-remote-connect/HCS_CertificateImportWizard1.png)
2. Pour **Emplacement du magasin**, sélectionnez **Ordinateur local**, puis cliquez sur **Suivant**.
3. Sélectionnez **placer tous les certificats dans hello suivant magasin**, puis cliquez sur **Parcourir**. Accédez magasin racine de toohello de votre hôte distant, puis cliquez sur **suivant**.
   
    ![Assistant Importation de certificat 2](./media/storsimple-remote-connect/HCS_CertificateImportWizard2.png)
4. Cliquez sur **Terminer**. Un message vous indiquant que hello importation a réussi s’affiche.
   
    ![Assistant Importation de certificat 3](./media/storsimple-remote-connect/HCS_CertificateImportWizard3.png)

#### <a name="tooadd-device-serial-numbers-toohello-remote-host"></a>hôte distant toohello des numéros de série du périphérique tooadd
1. Démarrez le bloc-notes en tant qu’administrateur, puis ouvrez le fichier d’hôtes hello situé dans \Windows\System32\Drivers\etc.
2. Ajouter hello trois entrées tooyour hôtes fichier suivant : **adresse IP de DATA 0**, **adresse IP fixe du contrôleur 0**, et **adresse IP fixe du contrôleur 1**.
3. Entrez le numéro de série hello appareil que vous avez enregistré précédemment. Mapper cette adresse IP de toohello comme indiqué dans hello suivant l’image. Pour les contrôleurs 0 et 1, ajoutez **Controller0** et **Controller1** à fin hello hello au numéro de série (nom CN).
   
    ![Ajout du fichier toohosts nom CN](./media/storsimple-remote-connect/HCS_AddingCNNameToHostsFile.png)
4. Enregistrer le fichier hôtes hello.

### <a name="connect-toohello-device-from-hello-remote-host"></a>Se connecter toohello appareil à partir de l’hôte distant de hello
Utiliser Windows PowerShell et SSL tooenter une session SSAdmin sur votre appareil à partir d’un client ou un hôte distant. session de Hello SSAdmin mappe toooption 1 Bonjour [console série](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu de votre appareil.

Effectuer hello suivant la procédure sur l’ordinateur hello à partir de laquelle vous voulez toomake hello à distance Windows PowerShell.

#### <a name="tooenter-an-ssadmin-session-on-hello-device-by-using-windows-powershell-and-ssl"></a>tooenter une session SSAdmin sur l’appareil hello à l’aide de Windows PowerShell et SSL
1. Démarrez une session Windows PowerShell en tant qu’administrateur.
2. Ajoutez hello appareil IP adresse toohello hôtes approuvés du client en tapant :
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
    Où <*device_ip*> est l’adresse IP de hello de votre appareil, par exemple : 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. Créez des informations d’identification en tapant : 
   
     `$cred = New-Object pscredential @("<IP of target device>\SSAdmin", (ConvertTo-SecureString -Force -AsPlainText "<Device Administrator Password>"))`
   
    Où <*IP du périphérique cible*> est l’adresse IP de hello de DATA 0 pour votre appareil, par exemple, **10.126.173.90** comme indiqué dans hello précédant l’image du fichier d’hôtes hello. Vous devez également fournir un mot de passe administrateur hello pour votre appareil.
4. Créer une session en tapant :
   
     `$session = New-PSSession -UseSSL -ComputerName <Serial number of target device> -Credential $cred -ConfigurationName "SSAdminConsole"`
   
    Pour le paramètre - ComputerName hello dans l’applet de commande hello fournir hello <*numéro de série du périphérique cible*>. Ce numéro de série a été mappé adresse toohello de DATA 0 dans le fichier d’hôtes hello sur votre hôte distant. par exemple, **SHX0991003G44MT** comme indiqué dans hello suivant l’image.
5. Entrez : 
   
     `Enter-PSSession $session`
6. Vous devez toowait quelques minutes, et vous serez ensuite appareil tooyour connecté via HTTPS sur SSL. Vous verrez un message indiquant que vous êtes connecté tooyour appareil.
   
    ![Accès distant PowerShell en utilisant HTTPS et SSL](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTPSAndSSL.png)

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur [votre appareil StorSimple à l’aide de Windows PowerShell tooadminister](storsimple-windows-powershell-administration.md).
* En savoir plus sur [à l’aide de hello tooadminister du service StorSimple Manager votre appareil StorSimple](storsimple-manager-service-administration.md).

