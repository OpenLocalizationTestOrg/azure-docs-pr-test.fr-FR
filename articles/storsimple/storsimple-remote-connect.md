---
title: "Se connecter à distance à votre appareil StorSimple | Microsoft Docs"
description: "Explique comment configurer votre appareil pour la gestion à distance et comment se connecter à Windows PowerShell for StorSimple par HTTP ou HTTPS."
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
ms.openlocfilehash: b916173e127394d3ea06eded36285bdbbf884b12
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-remotely-to-your-storsimple-8000-series-device"></a>Connexion à distance à votre appareil StorSimple série 8000

## <a name="overview"></a>Vue d’ensemble
Vous pouvez utiliser l’accès distant Windows PowerShell pour vous connecter à votre appareil StorSimple. Quand vous vous connectez de cette façon, vous ne voyez pas de menu. (Vous voyez un menu seulement si vous utilisez la console série sur l’appareil pour vous connecter). Avec l’accès distant Windows PowerShell, vous vous connectez à une instance d’exécution spécifique. Vous pouvez également spécifier la langue d’affichage. 

Pour plus d’informations sur l’utilisation de l’accès distant Windows PowerShell pour gérer votre appareil, consultez la rubrique [Administrer votre appareil StorSimple à l’aide de Windows PowerShell pour StorSimple](storsimple-windows-powershell-administration.md).

Ce didacticiel explique comment configurer votre appareil pour la gestion à distance, puis comment se connecter à Windows PowerShell pour StorSimple. Vous pouvez utiliser HTTP ou HTTPS pour vous connecter via l’accès distant Windows PowerShell. Cependant, quand vous décidez comment vous connecter à Windows PowerShell pour StorSimple, prenez en compte les points suivants : 

* Une connexion directe à la console série de l’appareil est sécurisée, mais une connexion à la console via des commutateurs réseau ne l’est pas. Méfiez-vous des risques de sécurité lors de la connexion à la console série d’un appareil via des commutateurs réseau. 
* Une connexion via une session HTTP peut offrir davantage de sécurité que la connexion via la console série sur le réseau. Bien que cela ne soit pas la méthode la plus sécurisée, elle est acceptable sur des réseaux approuvés. 
* La connexion via une session HTTPS avec un certificat auto-signé est l’option la plus sécurisée et c’est celle qui est recommandée.

Vous pouvez vous connecter à distance à l’interface Windows PowerShell. Cependant, l’accès à distance à votre appareil StorSimple via l’interface Windows PowerShell n’est pas activé par défaut. Vous devez d’abord activer la gestion à distance sur l’appareil, puis sur le client qui est utilisé pour accéder à votre appareil.

Les étapes décrites dans cet article ont été exécutées sur un système hôte exécutant Windows Server 2012 R2.

## <a name="connect-through-http"></a>Se connecter via HTTP
La connexion à Windows PowerShell pour StorSimple via une session HTTP offre davantage de sécurité que la connexion via la console série de votre appareil StorSimple. Bien que cela ne soit pas la méthode la plus sécurisée, elle est acceptable sur des réseaux approuvés.

Vous pouvez utiliser le portail Azure Classic ou la console série pour configurer la gestion à distance. Choisissez parmi les procédures suivantes :

* [Utiliser le portail Azure Classic pour activer la gestion à distance via HTTP](#use-the-azure-classic-portal-to-enable-remote-management-over-http)
* [Utiliser la console série pour activer la gestion à distance via HTTP](#use-the-serial-console-to-enable-remote-management-over-http)

Après avoir activé la gestion à distance, procédez comme suit pour préparer le client pour une connexion à distance.

* [Préparer le client pour une connexion à distance](#prepare-the-client-for-remote-connection)

### <a name="use-the-azure-classic-portal-to-enable-remote-management-over-http"></a>Utiliser le portail Azure Classic pour activer la gestion à distance via HTTP
Procédez comme suit dans le portail Azure Classic pour activer la gestion à distance via HTTP.

#### <a name="to-enable-remote-management-through-the-azure-classic-portal"></a>Pour activer la gestion à distance via le portail Azure Classic
1. Accédez à **Appareils** > **Configurer** pour votre appareil.
2. Accédez à la section **Gestion à distance** .
3. Définissez **Activer la gestion à distance** sur **Oui**.
4. Vous pouvez maintenant choisir de vous connecter à l’aide de HTTP. (Le choix par défaut est de se connecter via HTTPS.) Assurez-vous que HTTP est sélectionné.
   
   > [!NOTE]
   > Une connexion via HTTP est acceptable uniquement sur des réseaux approuvés.
   > 
   > 
5. Cliquez sur **Enregistrer** au bas de la page.

### <a name="use-the-serial-console-to-enable-remote-management-over-http"></a>Utiliser la console série pour activer la gestion à distance via HTTP
Procédez comme suit sur la console série de l’appareil pour activer la gestion à distance.

#### <a name="to-enable-remote-management-through-the-device-serial-console"></a>Pour activer la gestion à distance via la console série de l’appareil
1. Dans le menu de la console série, sélectionnez l’option 1. Pour plus d’informations sur l’utilisation de la console série sur l’appareil, consultez [Se connecter à Windows PowerShell pour StorSimple via la console série de l’appareil](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).
2. À l’invite, tapez : `Enable-HcsRemoteManagement –AllowHttp`
3. Vous serez averti des vulnérabilités de sécurité résultant de l’utilisation de HTTP pour se connecter à l’appareil. Quand vous y êtes invité, confirmez en tapant **O**.
4. Vérifiez que HTTP est activé en tapant : `Get-HcsSystem`
5. Vérifiez que le champ **RemoteManagementMode** affiche **HttpsAndHttpEnabled**. L’illustration suivante montre ces paramètres dans PuTTY.
   
     ![HTTPS et HTTP en série activés](./media/storsimple-remote-connect/HCS_SerialHttpsAndHttpEnabled.png)

### <a name="prepare-the-client-for-remote-connection"></a>Préparer le client pour une connexion à distance
Procédez comme suit sur le client pour activer la gestion à distance.

#### <a name="to-prepare-the-client-for-remote-connection"></a>Pour préparer le client pour une connexion à distance
1. Démarrez une session Windows PowerShell en tant qu’administrateur.
2. Tapez la commande suivante pour ajouter l’adresse IP de l’appareil StorSimple à la liste des hôtes approuvés du client : 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
     Remplacez <*device_ip*> par l’adresse IP de votre appareil, par exemple : 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. Tapez la commande suivante pour enregistrer les informations d’identification de l’appareil dans une variable : 
   
    ```
    $cred = Get-Credential
    ```
    
4. Dans la boîte de dialogue qui s’affiche :
   
   1. Entrez le nom d’utilisateur au format : *adresse_IP_appareil\AdministrateurSS*.
   2. Tapez le mot de passe de l’administrateur de l’appareil qui a été défini quand l’appareil a été configuré avec l’Assistant Installation. Le mot de passe par défaut est *Password1*.
5. Démarrez une session Windows PowerShell sur l’appareil en tapant cette commande :
   
     `Enter-PSSession -Credential $cred -ConfigurationName SSAdminConsole -ComputerName <device_ip>`
   
   > [!NOTE]
   > Pour créer une session Windows PowerShell pour une utilisation avec l’appareil virtuel StorSimple, ajoutez le paramètre `–Port` et spécifiez le port public que vous avez configuré dans l’accès distant pour l’appliance virtuelle StorSimple.
   > 
   > 
   
     À ce stade, vous devez normalement disposer d’une session Windows PowerShell à distance active sur l’appareil.
   
    ![Accès distant PowerShell en utilisant HTTP](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTP.png)

## <a name="connect-through-https"></a>Se connecter via HTTPS
La connexion à Windows PowerShell pour StorSimple via une session HTTPS est la méthode la plus sécurisée et elle est recommandée pour la connexion à distance à votre appareil Microsoft Azure StorSimple. Les procédures suivantes expliquent comment configurer la console série et les ordinateurs clients pour pouvoir utiliser HTTPS pour se connecter à Windows PowerShell pour StorSimple.

Vous pouvez utiliser le portail Azure Classic ou la console série pour configurer la gestion à distance. Choisissez parmi les procédures suivantes :

* [Utiliser le portail Azure Classic pour activer la gestion à distance via HTTPS](#use-the-azure-classic-portal-to-enable-remote-management-over-https)
* [Utiliser la console série pour activer la gestion à distance via HTTPS](#use-the-serial-console-to-enable-remote-management-over-https)

Après avoir activé la gestion à distance, utilisez les procédures suivantes pour préparer l’hôte pour la gestion à distance et pour se connecter à l’appareil à partir de l’hôte distant.

* [Préparer l’hôte pour la gestion à distance](#prepare-the-host-for-remote-management)
* [Se connecter à l’appareil à partir de l’hôte distant](#connect-to-the-device-from-the-remote-host)

### <a name="use-the-azure-classic-portal-to-enable-remote-management-over-https"></a>Utiliser le portail Azure Classic pour activer la gestion à distance via HTTPS
Procédez comme suit dans le portail Azure Classic pour activer la gestion à distance via HTTPS.

#### <a name="to-enable-remote-management-over-https-from-the-azure-classic-portal"></a>Pour activer la gestion à distance via HTTPS à partir du portail Azure Classic
1. Accédez à **Appareils** > **Configurer** pour votre appareil.
2. Accédez à la section **Gestion à distance** .
3. Définissez **Activer la gestion à distance** sur **Oui**.
4. Vous pouvez maintenant choisir de vous connecter via HTTPS. (Le choix par défaut est de se connecter via HTTPS.) Assurez-vous que HTTPS est sélectionné. 
5. Cliquez sur **Télécharger le certificat de gestion à distance**. Spécifiez un emplacement pour enregistrer ce fichier. Vous devez installer ce certificat sur l’ordinateur client ou sur l’ordinateur hôte que vous utiliserez pour vous connecter à l’appareil.
6. Cliquez sur **Enregistrer** au bas de la page.

### <a name="use-the-serial-console-to-enable-remote-management-over-https"></a>Utiliser la console série pour activer la gestion à distance via HTTPS
Procédez comme suit sur la console série de l’appareil pour activer la gestion à distance.

#### <a name="to-enable-remote-management-through-the-device-serial-console"></a>Pour activer la gestion à distance via la console série de l’appareil
1. Dans le menu de la console série, sélectionnez l’option 1. Pour plus d’informations sur l’utilisation de la console série sur l’appareil, consultez [Se connecter à Windows PowerShell pour StorSimple via la console série de l’appareil](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).
2. À l’invite, tapez :  
   
     `Enable-HcsRemoteManagement`
   
    Ceci doit normalement activer HTTPS sur votre appareil.
3. Vérifiez que HTTPS a été activé en tapant : 
   
     `Get-HcsSystem`
   
    Vérifiez que le champ **RemoteManagementMode** affiche **HttpsEnabled**. L’illustration suivante montre ces paramètres dans PuTTY.
   
     ![HTTPS en série activé](./media/storsimple-remote-connect/HCS_SerialHttpsEnabled.png)
4. Depuis la sortie de `Get-HcsSystem`, copiez le numéro de série de l’appareil et enregistrez-le pour une utilisation ultérieure.
   
   > [!NOTE]
   > Le numéro de série correspond au nom CN du certificat.
   > 
   > 
5. Obtenez un certificat de gestion à distance en tapant : 
   
     `Get-HcsRemoteManagementCert`
   
    Un certificat similaire à celui-ci apparaît.
   
    ![Obtenir un certificat de gestion à distance](./media/storsimple-remote-connect/HCS_GetRemoteManagementCertificate.png)
6. Copiez les informations du certificat de **-----BEGIN CERTIFICATE-----** à **-----END CERTIFICATE-----** dans un éditeur de texte comme le Bloc-notes et enregistrez-les dans un fichier .cer. (Vous allez copier ce fichier sur votre hôte distant lors de la préparation de l’hôte).
   
   > [!NOTE]
   > Pour générer un nouveau certificat, utilisez l’applet de commande `Set-HcsRemoteManagementCert`.
   > 
   > 

### <a name="prepare-the-host-for-remote-management"></a>Préparer l’hôte pour la gestion à distance
Pour préparer l’ordinateur hôte pour une connexion à distance qui utilise une session HTTPS, effectuez les procédures suivantes :

* [Importez le fichier .cer dans le magasin racine du client ou de l’hôte distant](#to-import-the-certificate-on-the-remote-host).
* [Ajoutez les numéros de série des appareils au fichier hosts sur l’hôte distant](#to-add-device-serial-numbers-to-the-remote-host).

Chacune de ces procédures est décrite ci-dessous.

#### <a name="to-import-the-certificate-on-the-remote-host"></a>Pour importer le certificat sur l’hôte distant
1. Cliquez avec le bouton droit sur le fichier .cer et sélectionnez **Installer le certificat**. Ceci démarre l’Assistant Importation de certificat.
   
    ![Assistant Importation de certificat 1](./media/storsimple-remote-connect/HCS_CertificateImportWizard1.png)
2. Pour **Emplacement du magasin**, sélectionnez **Ordinateur local**, puis cliquez sur **Suivant**.
3. Sélectionnez **Placer tous les certificats dans le magasin suivant**, puis cliquez sur **Parcourir**. Accédez au magasin racine de l’hôte distant, puis cliquez sur **Suivant**.
   
    ![Assistant Importation de certificat 2](./media/storsimple-remote-connect/HCS_CertificateImportWizard2.png)
4. Cliquez sur **Terminer**. Un message indiquant que l’importation a réussi s’affiche.
   
    ![Assistant Importation de certificat 3](./media/storsimple-remote-connect/HCS_CertificateImportWizard3.png)

#### <a name="to-add-device-serial-numbers-to-the-remote-host"></a>Pour ajouter des numéros de série d’appareils à l’hôte distant
1. Démarrez le Bloc-notes en tant qu’administrateur, puis ouvrez le fichier hosts qui se trouve dans \Windows\System32\Drivers\etc.
2. Ajoutez les trois entrées suivantes à votre fichier hosts : **Adresse IP de DATA 0**, **Adresse IP fixe du contrôleur 0** et **Adresse IP fixe du contrôleur 1**.
3. Entrez le numéro de série de l’appareil que vous avez enregistré précédemment. Mappez ceci à l’adresse IP, comme le montre l’image suivante. Pour Contrôleur 0 et Contrôleur 1, ajoutez **Controller0** et **Controller1** à la fin du numéro de série (nom CN).
   
    ![Ajout du nom CN au fichier Hosts](./media/storsimple-remote-connect/HCS_AddingCNNameToHostsFile.png)
4. Enregistrez le fichier hosts.

### <a name="connect-to-the-device-from-the-remote-host"></a>Se connecter à l’appareil à partir de l’hôte distant
Utilisez Windows PowerShell et SSL pour entrer dans une session SSAdmin sur votre appareil à partir d’un hôte ou d’un client distant. La session SSAdmin est mappée à l’option 1 dans le menu de la [console série](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) de votre appareil.

Effectuez la procédure suivante sur l’ordinateur à partir duquel vous voulez établir la connexion Windows PowerShell à distance.

#### <a name="to-enter-an-ssadmin-session-on-the-device-by-using-windows-powershell-and-ssl"></a>Pour entrer dans une session SSAdmin sur l’appareil en utilisant Windows PowerShell et SSL
1. Démarrez une session Windows PowerShell en tant qu’administrateur.
2. Ajoutez l’adresse IP de l’appareil aux hôtes approuvés du client en tapant :
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
    où <*device_ip*> par l’adresse IP de votre appareil, par exemple : 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. Créez des informations d’identification en tapant : 
   
     `$cred = New-Object pscredential @("<IP of target device>\SSAdmin", (ConvertTo-SecureString -Force -AsPlainText "<Device Administrator Password>"))`
   
    Où <*IP of target device*> est l’adresse IP de DATA 0 pour votre appareil, par exemple **10.126.173.90** comme dans l’image précédente du fichier hosts. Spécifiez également le mot de passe administrateur pour votre appareil.
4. Créer une session en tapant :
   
     `$session = New-PSSession -UseSSL -ComputerName <Serial number of target device> -Credential $cred -ConfigurationName "SSAdminConsole"`
   
    Pour le paramètre -ComputerName de l’applet de commande, vous devez fournir le <*numéro de série de l’appareil cible*>. Ce numéro de série a été mappé à l’adresse IP de DATA 0 dans le fichier hosts sur l’hôte distant, par exemple, **SHX0991003G44MT** dans l’image suivante.
5. Entrez : 
   
     `Enter-PSSession $session`
6. Patientez quelques minutes, puis vous serez connecté à votre appareil via HTTPS sur SSL. Vous verrez un message indiquant que vous êtes connecté à votre appareil.
   
    ![Accès distant PowerShell en utilisant HTTPS et SSL](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTPSAndSSL.png)

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur [l’utilisation de Windows PowerShell pour gérer votre appareil StorSimple](storsimple-windows-powershell-administration.md).
* En savoir plus sur [l’utilisation du service StorSimple Manager pour gérer votre appareil StorSimple](storsimple-manager-service-administration.md).

