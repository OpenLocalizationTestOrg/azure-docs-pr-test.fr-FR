---
title: aaaPrepare un tooAzure tooupload de disque dur virtuel Windows | Documents Microsoft
description: "Comment tooprepare un VHDX ou un disque dur virtuel Windows avant de le télécharger tooAzure"
services: virtual-machines-windows
documentationcenter: 
author: glimoli
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7802489d-33ec-4302-82a4-91463d03887a
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: genli
ms.openlocfilehash: 530390e4c6a4f66ddfd4da23338f9bb3708c299f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-windows-vhd-or-vhdx-tooupload-tooazure"></a>Préparer un tooAzure tooupload Windows VHD ou VHDX
Avant de télécharger des machines virtuelles Windows (VM) à partir de local tooMicrosoft Azure, vous devez préparer hello disque dur virtuel (VHD ou VHDX). Azure prend en charge uniquement la génération 1 des machines virtuelles qui sont au format de fichier de disque dur virtuel hello et disposer d’un disque de taille fixe. taille maximale de Hello autorisé pour hello que disque dur virtuel est de 1 023 go. Vous pouvez convertir une génération 1 machine virtuelle à partir de hello VHDX tooVHD de système de fichiers et de taille dynamique disque toofixed taille. En revanche, vous ne pouvez pas modifier la génération d’une machine virtuelle. Pour plus d’informations, consultez la page [Dois-je créer une machine virtuelle de génération 1 ou 2 dans Hyper-V ?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v)

Pour plus d’informations sur la stratégie de prise en charge hello pour machine virtuelle Azure, consultez [prise en charge du logiciel Microsoft server pour Microsoft Azure Virtual Machines](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines).

> [!Note]
> les instructions de Hello dans cet article s’appliquent toohello 64 bits de Windows Server 2008 R2 et le système d’exploitation de serveur Windows ultérieur. Pour plus d’informations sur l’exécution de la version 32 bits du système d’exploitation avec Azure, consultez l’article [Prise en charge pour les systèmes d’exploitation 32 bits sur des machines virtuelles Azure](https://support.microsoft.com/help/4021388/support-for-32-bit-operating-systems-in-azure-virtual-machines).

## <a name="convert-hello-virtual-disk-toovhd-and-fixed-size-disk"></a>Convertir tooVHD de disque virtuel hello et de disque de taille fixe 
Si vous avez besoin de tooconvert votre toohello de disque virtuel requis format pour Azure, utilisez une des méthodes hello dans cette section. Sauvegardez hello machine virtuelle avant d’exécuter des processus de conversion de disque virtuel hello et assurez-vous que ce disque dur virtuel Windows fonctionne correctement sur le serveur local de hello de hello. Corrigez les erreurs dans hello machine virtuelle avant que vous essayez de tooconvert ou téléchargez tooAzure.

Après la conversion de disque de hello, créez un ordinateur virtuel qui utilise le disque de hello converti. Démarrez et connectez-vous à toofinish de machine virtuelle toohello préparation hello machine virtuelle pour le téléchargement.

### <a name="convert-disk-using-hyper-v-manager"></a>Convertir un disque à l’aide du Gestionnaire Hyper-V
1. Ouvrez le Gestionnaire Hyper-V et sélectionnez votre ordinateur local sur hello gauche. Dans le menu de hello situé au-dessus de la liste des ordinateurs hello, cliquez sur **Action** > **modifier le disque**.
2. Sur hello **rechercher un disque dur virtuel** écran, recherchez et sélectionnez votre disque virtuel.
3. Sur hello **choisir une Action** écran, puis sélectionnez **convertir** et **suivant**.
4. Si vous avez besoin de tooconvert vhdx, sélectionnez **VHD** puis cliquez sur **suivant**
5. Si vous avez besoin de tooconvert à partir d’un disque dynamique, sélectionnez **une taille fixe** puis cliquez sur **suivant**
6. Recherchez et sélectionnez un chemin d’accès toosave hello nouveau fichier VHD à.
7. Cliquez sur **Terminer**.

>[!NOTE]
>commandes Hello dans cet article doivent être exécutées sur une session PowerShell avec élévation de privilèges.

### <a name="convert-disk-by-using-powershell"></a>Convertir un disque à l’aide de PowerShell
Vous pouvez convertir un disque virtuel à l’aide de hello [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) commande dans Windows PowerShell. Sélectionnez **Exécuter en tant qu’administrateur** lorsque vous démarrez PowerShell. 

Hello exemple de commande suivant convertit VHDX tooVHD et d’une extension dynamique toofixed-taille du disque :

```Powershell
Convert-VHD –Path c:\test\MY-VM.vhdx –DestinationPath c:\test\MY-NEW-VM.vhd -VHDType Fixed
```
Dans cette commande, remplacez la valeur hello pour «-chemin d’accès « avec hello chemin d’accès toohello disque dur virtuel souhaité tooconvert et hello une valeur pour «-DestinationPath » avec hello nouveaux nom et chemin de hello converti le disque.

### <a name="convert-from-vmware-vmdk-disk-format"></a>Convertir à partir du format de disque VMDK VMware
Si vous disposez d’une image de machine virtuelle Windows Bonjour [format de fichier VMDK](https://en.wikipedia.org/wiki/VMDK), convertissez-le tooa disque dur virtuel à l’aide de hello [convertisseur de machine virtuelle Microsoft](https://www.microsoft.com/download/details.aspx?id=42497). Pour plus d’informations, consultez l’article de blog hello [comment tooConvert un disque dur virtuel de tooHyper-v VMDK VMware](http://blogs.msdn.com/b/timomta/archive/2015/06/11/how-to-convert-a-vmware-vmdk-to-hyper-v-vhd.aspx).

## <a name="set-windows-configurations-for-azure"></a>Définir les configurations Windows pour Azure

Sur la machine virtuelle que vous prévoyez de hello tooAzure tooupload, exécuter toutes les commandes suivant de hello étapes à partir d’un [fenêtre d’invite de commandes avec élévation de privilèges](https://technet.microsoft.com/library/cc947813.aspx):

1. Supprimer un itinéraire statique persistant sur la table de routage hello :
   
   * table d’itinéraires hello tooview, exécutez `route print` à l’invite de commandes hello.
   * Vérifiez hello **les itinéraires de persistance** sections. S’il existe un itinéraire persistant, utiliser [itinéraire delete](https://technet.microsoft.com/library/cc739598.apx) tooremove il.
2. Supprimer de proxy WinHTTP hello :
   
    ```PowerShell
    netsh winhttp reset proxy
    ```
3. Définir la stratégie de réseau SAN de disque hello trop[Onlineall](https://technet.microsoft.com/library/gg252636.aspx). 
   
    ```PowerShell
    diskpart 
    ```
    Dans la fenêtre d’invite de commandes ouverte hello, tapez Bonjour suivant de commandes :

     ```DISKPART
    san policy=onlineall
    exit   
    ```

4. Définir la durée de temps universel coordonné (UTC) pour Windows et hello trop de type de démarrage du service de temps de Windows (w32time) de hello**automatiquement**:
   
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\TimeZoneInformation' -name "RealTimeIsUniversal" 1 -Type DWord

    Set-Service -Name w32time -StartupType Auto
    ```
5. Définir hello power profil toohello **hautes performances**:

    ```PowerShell
    powercfg /setactive SCHEME_MIN
    ```

## <a name="check-hello-windows-services"></a>Vérifier les services de Windows hello
Assurez-vous que chaque hello suivant des services Windows a toohello **les valeurs par défaut Windows**. Il s’agit de chiffres de minimale hello de services toomake que cette machine virtuelle hello dispose d’une connectivité doivent être définis. paramètres de démarrage hello tooreset, exécutez hello suivant de commandes :
   
```PowerShell
Set-Service -Name bfe -StartupType Auto
Set-Service -Name dhcp -StartupType Auto
Set-Service -Name dnscache -StartupType Auto
Set-Service -Name IKEEXT -StartupType Auto
Set-Service -Name iphlpsvc -StartupType Auto
Set-Service -Name netlogon -StartupType Manual
Set-Service -Name netman -StartupType Manual
Set-Service -Name nsi -StartupType Auto
Set-Service -Name termService -StartupType Manual
Set-Service -Name MpsSvc -StartupType Auto
Set-Service -Name RemoteRegistry -StartupType Auto
```

## <a name="update-remote-desktop-registry-settings"></a>Mettre à jour les paramètres de registre du Bureau à distance
Assurez-vous que hello suivant les paramètres sont correctement configurés pour la connexion Bureau à distance :

>[!Note] 
>Vous pouvez recevoir un message d’erreur lorsque vous exécutez hello **Set-ItemProperty-Path ' HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services - nom &lt;nom de l’objet&gt; &lt;valeur&gt;** dans ces étapes. message d’erreur Hello peut être ignoré en toute sécurité. Cela ne signifie que ce domaine hello repousse pas que la configuration via un objet de stratégie de groupe.
>
>

1. Le protocole RDP (Remote Desktop Protocol) est activé :
   
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -Value 0 -Type DWord

    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "fDenyTSConnections" -Value 0 -Type DWord
    ```
   
2. Hello port RDP est correctement configuré (par défaut le port 3389) :
   
    ```PowerShell
   Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "PortNumber" 3389 -Type DWord
    ```
    Lorsque vous déployez une machine virtuelle, les règles par défaut de hello sont créés sur le port 3389. Si vous souhaitez que le numéro de port toochange hello, faites-le après que hello ordinateur virtuel est déployé dans Azure.

3. Hello d’écoute dans toutes les interfaces réseau :
   
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "LanAdapter" 0 -Type DWord
   ```
4. Configurer le mode d’authentification au niveau du réseau de hello pour les connexions RDP hello :
   
    ```PowerShell
   Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "UserAuthentication" 1 -Type DWord

    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "SecurityLayer" 1 -Type DWord

    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "fAllowSecProtocolNegotiation" 1 -Type DWord
     ```

5. Valeur hello KeepAlive :
    
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "KeepAliveEnable" 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "KeepAliveInterval" 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "KeepAliveTimeout" 1 -Type DWord
    ```
6. Reconnectez-vous ：
    
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "fDisableAutoReconnect" 0 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "fInheritReconnectSame" 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "fReconnectSame" 0 -Type DWord
    ```
7. Limite hello le nombre de connexions simultanées :
    
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "MaxInstanceCount" 4294967295 -Type DWord
    ```
8. S’il existe que des certificats auto-signés liée port d’écoute RDP toohello, supprimez-les :
    
    ```PowerShell
    Remove-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "SSLCertificateSHA1Hash"
    ```
    Il s’agit de toomake assurer que vous pouvez vous connecter au début de hello lorsque vous déployez hello machine virtuelle. Vous pouvez également le consulter sur une étape ultérieure après hello qu'ordinateur virtuel est déployé dans Azure, si nécessaire.

9. Si hello machine virtuelle doit faire partie d’un domaine, vérifiez que tous les hello suivant toomake paramètres sûr que les anciens paramètres de hello ne sont pas rétablis. stratégies de Hello qui doivent être vérifiées sont les suivants de hello :
    
    - Le protocole RDP est activé :

         Configuration ordinateur\Stratégies\Paramètres Windows\Modèles d’administration\Composants\Services Bureau à distance\Hôte de session Bureau à distance\Connexions :
         
         **Autoriser les utilisateurs tooconnect à distance à l’aide du Bureau à distance**

    - Stratégie de groupe d’authentification au niveau du réseau :

        Paramètres\Modèles d’administration\Composants\Services Bureau à distance\Hôte de session Bureau à distance\Sécurité : 
        
        **Demander l’authentification utilisateur via l’authentification au niveau du réseau pour les connexions distantes**
    
    - Paramètres keep alive :

        Configuration ordinateur\Stratégies\Paramètres Windows\Modèles d’administration\Composants Windows\Services Bureau à distance\Hôte de session Bureau à distance\Connexions : 
        
        **Configurer l’intervalle de connexion keep-alive**

    - Paramètres de reconnexion :

        Configuration ordinateur\Stratégies\Paramètres Windows\Modèles d’administration\Composants Windows\Services Bureau à distance\Hôte de session Bureau à distance\Connexions : 
        
        **Reconnexion automatique**

    - Limiter le nombre de hello de paramètres de connexion :

        Configuration ordinateur\Stratégies\Paramètres Windows\Modèles d’administration\Composants Windows\Services Bureau à distance\Hôte de session Bureau à distance\Connexions : 
        
        **Limiter le nombre de connexions**

## <a name="configure-windows-firewall-rules"></a>Configurer les règles du Pare-feu Windows
1. Activer le pare-feu Windows sur hello trois profils (domaine, Standard et Public) :

   ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\services\SharedAccess\Parameters\FirewallPolicy\DomainProfile' -name "EnableFirewall" -Value 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\services\SharedAccess\Parameters\FirewallPolicy\PublicProfile' -name "EnableFirewall" -Value 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\services\SharedAccess\Parameters\FirewallPolicy\Standardprofile' -name "EnableFirewall" -Value 1 -Type DWord
   ```

2. Exécutez hello suivant de commande PowerShell tooallow WinRM via des profils de pare-feu hello trois (domaine, privé et Public) et activer hello service PowerShell distant :
   
   ```PowerShell
    Enable-PSRemoting -force
    netsh advfirewall firewall set rule dir=in name="Windows Remote Management (HTTP-In)" new enable=yes
    netsh advfirewall firewall set rule dir=in name="Windows Remote Management (HTTP-In)" new enable=yes
   ```
3. Activer hello suivant le trafic RDP hello pare-feu règles tooallow 

   ```PowerShell
    netsh advfirewall firewall set rule group="Remote Desktop" new enable=yes
   ```   
4. Activer hello fichier et les règles de partage d’imprimante afin que hello VM peut répondre tooa utilitaire ping à l’intérieur de hello réseau virtuel :

   ```PowerShell
    netsh advfirewall firewall set rule dir=in name="File and Printer Sharing (Echo Request - ICMPv4-In)" new enable=yes
   ``` 
5. Si hello machine virtuelle doit faire partie d’un domaine, vérifiez hello suivant toomake paramètres sûr que les anciens paramètres de hello ne sont pas rétablis. stratégies de Hello AD qui doivent être vérifiées sont les suivants de hello :

    - Activer les profils de pare-feu Windows hello

        Configuration ordinateur\Stratégies\Paramètres Windows\Modèles d’administration\Réseau\Connexion réseau\Pare-feu Windows\Profil de domaine\Pare-feu Windows : **protéger toutes les connexions réseau**

       Configuration ordinateur\Stratégies\Paramètres Windows\Modèles d’administration\Réseau\Connexion réseau\Pare-feu Windows\Profil standard\Pare-feu Windows : **protéger toutes les connexions réseau**

    - Activer le protocole RDP 

        Configuration ordinateur\Stratégies\Paramètres Windows\Modèles d’administration\Réseau\Connexion réseau\Pare-feu Windows\Profil de domaine\Pare-feu Windows : **autoriser les exceptions du Bureau à distance en entrée**

        Configuration ordinateur\Stratégies\Paramètres Windows\Modèles d’administration\Réseau\Connexion réseau\Pare-feu Windows\Profil standard\Pare-feu Windows : **autoriser les exceptions du Bureau à distance en entrée**

    - Activer le protocole ICMP-V4

        Configuration ordinateur\Stratégies\Paramètres Windows\Modèles d’administration\Réseau\Connexion réseau\Pare-feu Windows\Profil de domaine\Pare-feu Windows : **autoriser les exceptions ICMP**

        Configuration ordinateur\Stratégies\Paramètres Windows\Modèles d’administration\Réseau\Connexion réseau\Pare-feu Windows\Profil standard\Pare-feu Windows : **autoriser les exceptions ICMP**

## <a name="verify-vm-is-healthy-secure-and-accessible-with-rdp"></a>Vérifier que la machine virtuelle est saine, sécurisée et accessible via une connexion RDP 
1. disque de hello que toomake est intègre et cohérentes, exécuter une opération de vérification de disque au redémarrage de l’ordinateur virtuel suivant hello :

    ```PowerShell
    Chkdsk /f
    ```
    Assurez-vous qu’hello affiche un disque propre et sain.

2. Définir des paramètres de données de Configuration de démarrage (BCD) hello. 

    > [!Note]
    > Veillez à exécuter ces commandes dans une fenêtre de commande avec privilèges élevés et **NON** dans PowerShell :
   
   ```CMD
   bcdedit /set {bootmgr} integrityservices enable
   
   bcdedit /set {default} device partition=C:
   
   bcdedit /set {default} integrityservices enable
   
   bcdedit /set {default} recoveryenabled Off
   
   bcdedit /set {default} osdevice partition=C:
   
   bcdedit /set {default} bootstatuspolicy IgnoreAllFailures
   ```
3. Vérifiez que ce référentiel du service Windows hello est cohérent. tooperform, exécution hello commande suivante :

    ```PowerShell
    winmgmt /verifyrepository
    ```
    Si le référentiel de hello est endommagé, consultez [WMI : espace de stockage endommagé, ou non](https://blogs.technet.microsoft.com/askperf/2014/08/08/wmi-repository-corruption-or-not).

4. Assurez-vous que toute autre application n’utilise pas le port 3389 hello. Ce port est utilisé pour hello service RDP dans Azure. Vous pouvez exécuter **netstat - anob** toosee quels ports sont utilisés sur la machine virtuelle de hello dans :

    ```PowerShell
    netstat -anob
    ```

5. Si hello VHD de Windows que vous souhaitez tooupload est un contrôleur de domaine, puis procédez comme suit :

    R : Suivez [ces étapes supplémentaires](https://support.microsoft.com/kb/2904015) disque de hello tooprepare.

    B. Assurez-vous que vous connaissez le mot de passe DSRM hello au cas où vous toostart hello machine virtuelle en mode DSRM à un moment donné. Vous souhaiterez peut-être toorefer toothis lien tooset hello [mot de passe DSRM](https://technet.microsoft.com/library/cc754363(v=ws.11).aspx).

6. Assurez-vous que le compte administrateur intégré hello et le mot de passe sont connus tooyou. Vous pouvez souhaitez tooreset hello administrateur local mot de passe actuel et vous assurer que vous pouvez utiliser ce compte toosign dans tooWindows via hello connexion RDP. Cette autorisation d’accès est contrôlée par l’objet de stratégie de groupe « Autoriser la connexion via les Services Bureau à distance » hello. Vous pouvez afficher cet objet Bonjour éditeur de stratégie de groupe sous :

    Configuration ordinateur\Paramètres Windows\Paramètres de sécurité\Stratégies locales\Attribution des droits utilisateur

7. Vérifiez que hello suivant AD stratégies toomake que ne bloque l’accès RDP via RDP ni à partir du réseau de hello :

    - Configuration ordinateur\Paramètres Windows\Paramètres sécurité\Stratégies locales\Attribution des droits Assignment\Deny accès toothis un ordinateur à partir du réseau de hello

    - Configuration de l’ordinateur\Paramètres Windows\Paramètres de sécurité\Stratégies locales\Attribution des droits utilisateurs\Refuser la connexion via les services Bureau à distance


8. Redémarrage hello VM toomake assurer que Windows est toujours sain peut être atteint à l’aide de connexion de RDP hello. À ce stade, vous pouvez souhaitez de toocreate une machine virtuelle dans votre local Hyper-V toomake vraiment hello que complètement démarrage de la machine virtuelle et ensuite tester s’il s’agit de RDP est accessible.

9. Supprimez tous les filtres de TDI (Transport Driver Interface) supplémentaires, tels que les logiciels qui analysent les paquets TCP ou les pare-feu supplémentaires. Vous pouvez également le consulter sur une étape ultérieure après hello qu'ordinateur virtuel est déployé dans Azure, si nécessaire.

10. Désinstallez tous les autres logiciels tiers et pilote les composants connexes toophysical ou une autre technologie de virtualisation.

### <a name="install-windows-updates"></a>Installer les mises à jour Windows
configuration d’idéale Hello est trop**ont le niveau de correctif logiciel hello d’ordinateur hello en hello dernières**. Si ce n’est pas possible, assurez-vous que hello après les mises à jour sont installées :

|                       |                   |           |                                       Version de fichier minimale x64       |                                      |                                      |                            |
|-------------------------|-------------------|------------------------------------|---------------------------------------------|--------------------------------------|--------------------------------------|----------------------------|
| Composant               | Fichier binaire            | Windows 7 et Windows Server 2008 R2 | Windows 8 et Windows Server 2012             | Windows 8.1 et Windows Server 2012 R2 | Windows 10 et Windows Server 2016 RS1 | Windows 10 RS2             |
| Storage                 | disk.sys          | 6.1.7601.23403 - KB3125574         | 6.2.9200.17638 / 6.2.9200.21757 - KB3137061 | 6.3.9600.18203 - KB3137061           | -                                    | -                          |
|                         | storport.sys      | 6.1.7601.23403 - KB3125574         | 6.2.9200.17188 / 6.2.9200.21306 - KB3018489 | 6.3.9600.18573 - KB4022726           | 10.0.14393.1358 - KB4022715          | 10.0.15063.332             |
|                         | ntfs.sys          | 6.1.7601.23403 - KB3125574         | 6.2.9200.17623 / 6.2.9200.21743 - KB3121255 | 6.3.9600.18654 - KB4022726           | 10.0.14393.1198 - KB4022715          | 10.0.15063.447             |
|                         | Iologmsg.dll      | 6.1.7601.23403 - KB3125574         | 6.2.9200.16384 - KB2995387                  | -                                    | -                                    | -                          |
|                         | Classpnp.sys      | 6.1.7601.23403 - KB3125574         | 6.2.9200.17061 / 6.2.9200.21180 - KB2995387 | 6.3.9600.18334 - KB3172614           | 10.0.14393.953 - KB4022715           | -                          |
|                         | Volsnap.sys       | 6.1.7601.23403 - KB3125574         | 6.2.9200.17047 / 6.2.9200.21165 - KB2975331 | 6.3.9600.18265 - KB3145384           | -                                    | 10.0.15063.0               |
|                         | partmgr.sys       | 6.1.7601.23403 - KB3125574         | 6.2.9200.16681 - KB2877114                  | 6.3.9600.17401 - KB3000850           | 10.0.14393.953 - KB4022715           | 10.0.15063.0               |
|                         | volmgr.sys        |                                    |                                             |                                      |                                      | 10.0.15063.0               |
|                         | Volmgrx.sys       | 6.1.7601.23403 - KB3125574         | -                                           | -                                    | -                                    | 10.0.15063.0               |
|                         | Msiscsi.sys       | 6.1.7601.23403 - KB3125574         | 6.2.9200.21006 - KB2955163                  | 6.3.9600.18624 - KB4022726           | 10.0.14393.1066 - KB4022715          | 10.0.15063.447             |
|                         | Msdsm.sys         | 6.1.7601.23403 - KB3125574         | 6.2.9200.21474 - KB3046101                  | 6.3.9600.18592 - KB4022726           | -                                    | -                          |
|                         | Mpio.sys          | 6.1.7601.23403 - KB3125574         | 6.2.9200.21190 - KB3046101                  | 6.3.9600.18616 - KB4022726           | 10.0.14393.1198 - KB4022715          | -                          |
|                         | Fveapi.dll        | 6.1.7601.23311 - KB3125574         | 6.2.9200.20930 - KB2930244                  | 6.3.9600.18294 - KB3172614           | 10.0.14393.576 - KB4022715           | -                          |
|                         | Fveapibase.dll    | 6.1.7601.23403 - KB3125574         | 6.2.9200.20930 - KB2930244                  | 6.3.9600.17415 - KB3172614           | 10.0.14393.206 - KB4022715           | -                          |
| Réseau                 | netvsc.sys        | -                                  | -                                           | -                                    | 10.0.14393.1198 - KB4022715          | 10.0.15063.250 - KB4020001 |
|                         | mrxsmb10.sys      | 6.1.7601.23816 - KB4022722         | 6.2.9200.22108 - KB4022724                  | 6.3.9600.18603 - KB4022726           | 10.0.14393.479 - KB4022715           | 10.0.15063.483             |
|                         | mrxsmb20.sys      | 6.1.7601.23816 - KB4022722         | 6.2.9200.21548 - KB4022724                  | 6.3.9600.18586 - KB4022726           | 10.0.14393.953 - KB4022715           | 10.0.15063.483             |
|                         | mrxsmb.sys        | 6.1.7601.23816 - KB4022722         | 6.2.9200.22074 - KB4022724                  | 6.3.9600.18586 - KB4022726           | 10.0.14393.953 - KB4022715           | 10.0.15063.0               |
|                         | tcpip.sys         | 6.1.7601.23761 - KB4022722         | 6.2.9200.22070 - KB4022724                  | 6.3.9600.18478 - KB4022726           | 10.0.14393.1358 - KB4022715          | 10.0.15063.447             |
|                         | http.sys          | 6.1.7601.23403 - KB3125574         | 6.2.9200.17285 - KB3042553                  | 6.3.9600.18574 - KB4022726           | 10.0.14393.251 - KB4022715           | 10.0.15063.483             |
|                         | vmswitch.sys      | 6.1.7601.23727 - KB4022719         | 6.2.9200.22117 - KB4022724                  | 6.3.9600.18654 - KB4022726           | 10.0.14393.1358 - KB4022715          | 10.0.15063.138             |
| Principal                    | ntoskrnl.exe      | 6.1.7601.23807 - KB4022719         | 6.2.9200.22170 - KB4022718                  | 6.3.9600.18696 - KB4022726           | 10.0.14393.1358 - KB4022715          | 10.0.15063.483             |
| Services Bureau à distance | rdpcorets.dll     | 6.2.9200.21506 - KB4022719         | 6.2.9200.22104 - KB4022724                  | 6.3.9600.18619 - KB4022726           | 10.0.14393.1198 - KB4022715          | 10.0.15063.0               |
|                         | termsrv.dll       | 6.1.7601.23403 - KB3125574         | 6.2.9200.17048 - KB2973501                  | 6.3.9600.17415 - KB3000850           | 10.0.14393.0 - KB4022715             | 10.0.15063.0               |
|                         | termdd.sys        | 6.1.7601.23403 - KB3125574         | -                                           | -                                    | -                                    | -                          |
|                         | win32k.sys        | 6.1.7601.23807 - KB4022719         | 6.2.9200.22168 - KB4022718                  | 6.3.9600.18698 - KB4022726           | 10.0.14393.594 - KB4022715           | -                          |
|                         | rdpdd.dll         | 6.1.7601.23403 - KB3125574         | -                                           | -                                    | -                                    | -                          |
|                         | rdpwd.sys         | 6.1.7601.23403 - KB3125574         | -                                           | -                                    | -                                    | -                          |
| Sécurité                | Échéance tooWannaCrypt | KB4012212                          | KB4012213                                   | KB4012213                            | KB4012606                            | KB4012606                  |
|                         |                   |                                    | KB4012216                                   |                                      | KB4013198                            | KB4013198                  |
|                         |                   | KB4012215                          | KB4012214                                   | KB4012216                            | KB4013429                            | KB4013429                  |
|                         |                   |                                    | KB4012217                                   |                                      | KB4013429                            | KB4013429                  |
       
### Lorsque toouse sysprep<a id="step23"></a>    

Sysprep est un processus risque d’être exécuté dans une installation de windows va réinitialiser installation hello du système de hello et fournit un « out of hello box experience » en supprimant toutes les données personnelles et de la réinitialisation de plusieurs composants. Cela s’effectue généralement si vous voulez toocreate un modèle à partir de laquelle vous pouvez déployer plusieurs autres ordinateurs virtuels qui ont une configuration spécifique. On appelle cela une **image généralisée**.

Si, au lieu de cela, vous souhaitez uniquement toocreate une machine virtuelle à partir d’un disque, vous n’avez pas toouse sysprep. Dans ce cas, vous pouvez simplement créer hello machine virtuelle à partir de ce qui est appelé un **image spécialisée**.

Pour plus d’informations sur comment toocreate une machine virtuelle à partir d’un disque spécialisé, consultez :

- [Créer une machine virtuelle à partir d’un disque spécialisé](create-vm-specialized.md)
- [Créer une machine virtuelle à partir d’un disque dur virtuel spécialisé](https://azure.microsoft.com/resources/templates/201-vm-specialized-vhd/)

Si vous souhaitez toocreate une image généralisée, vous devez toorun sysprep. Pour plus d’informations sur Sysprep, consultez [comment tooUse Sysprep : Introduction](http://technet.microsoft.com/library/bb457073.aspx). 

Tous les rôles ou toutes les applications installés sur un ordinateur Windows ne prennent pas forcément en charge cette généralisation. Par conséquent, avant de vous exécutez cette procédure, consultez le toohello suivant l’article toomake que ce rôle hello de cet ordinateur est pris en charge par sysprep. Pour plus d’informations, consultez la page [Prise en charge de Sysprep pour les rôles serveur](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).

### <a name="steps-toogeneralize-a-vhd"></a>Étapes toogeneralize un disque dur virtuel

>[!NOTE]
> Après l’exécution de sysprep.exe comme spécifié dans hello comme suit, désactiver hello machine virtuelle et n’activez pas elle en tant que vous créez une image à partir de celui-ci dans Azure.

1. Connectez-vous toohello machine virtuelle Windows.
2. Exécutez une **invite de commandes** en tant qu’administrateur. 
3. Remplacez le répertoire hello pour : **%windir%\system32\sysprep**, puis exécutez **sysprep.exe**.
3. Bonjour **outil de préparation système** boîte de dialogue, sélectionnez **entrer le système Out-of-Box Experience (OOBE)**et assurez-vous que hello **Generalize** case à cocher est activée.

    ![Outil de préparation système](media/prepare-for-upload-vhd-image/syspre.png)
4. Dans **Options d’arrêt**, sélectionnez **Arrêter**.
5. Cliquez sur **OK**.
6. Sysprep est terminée, arrêtez hello machine virtuelle. N’utilisez pas **redémarrer** tooshut hello machine virtuelle vers le bas.
7. Hello disque dur virtuel est à présent prêt toobe téléchargé. Pour plus d’informations sur comment toocreate une machine virtuelle à partir d’un disque généralisé, consultez [télécharger un disque dur virtuel généralisé et son utilisation toocreate un nouvelles machines virtuelles dans Azure](sa-upload-generalized.md).


## <a name="complete-recommended-configurations"></a>Remplir les configurations recommandées
Hello, suivant les paramètres n’affecte pas le téléchargement du disque dur virtuel. Toutefois, nous vous recommandons vivement de les configurer.

* Installer hello [Agent des ordinateurs virtuels Azure](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Vous pouvez ensuite activer les extensions de machine virtuelle. extensions de machine virtuelle Hello implémentent la plupart des fonctionnalités critiques de hello que vous souhaitez toouse avec vos machines virtuelles telles que la réinitialisation des mots de passe, configuration RDP et ainsi de suite. Pour plus d'informations, consultez les pages suivantes :

    - Billet de blog en anglais [VM Agent and Extensions – Part 1](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-1/)
    - Billet de blog en anglais [VM Agent and Extensions – Part 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/)
* journal de vidage Hello peut être utile pour résoudre les problèmes de blocage de Windows. Activer la collecte de journal de vidage hello :
  
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "CrashDumpEnable" -Value "2" -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "DumpFile" -Value "%SystemRoot%\MEMORY.DMP"
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "AutoReboot" -Value 0 -Type DWord
    New-Item -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps'
    New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpFolder" -Value "c:\CrashDumps"
    New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpCount" -Value 10 -Type DWord
    New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpType" -Value 2 -Type DWord
    Set-Service -Name WerSvc -StartupType Manual
    ```
    Si vous recevez des erreurs au cours des procédures de hello les étapes de cet article, cela signifie que les clés de Registre hello existe déjà. Dans ce cas, utilisez hello suivant à la place les commandes :

    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "CrashDumpEnable" -Value "2" -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "DumpFile" -Value "%SystemRoot%\MEMORY.DMP"
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpFolder" -Value "c:\CrashDumps"
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpCount" -Value 10 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpType" -Value 2 -Type DWord
    Set-Service -Name WerSvc -StartupType Manual
    ```
*  Après la création d’hello machine virtuelle dans Azure, nous vous recommandons de placer hello du fichier d’échange sur hello » temporelle « volume tooimprove performances. Pour ce faire :

    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management' -name "PagingFiles" -Value "D:\pagefile"
    ```
Si n’importe quel disque de données est attachée toohello VM, lettre de lecteur du volume de lecteur temporelle hello est généralement « d ». Cette désignation peut être différente, selon le nombre de hello de lecteurs disponibles et les paramètres hello que vous définissez.

## <a name="next-steps"></a>Étapes suivantes
* [Télécharger un tooAzure d’image de machine virtuelle Windows pour les déploiements de gestionnaire de ressources](upload-generalized-managed.md)

