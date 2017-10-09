---
title: aaaCreate un package de support StorSimple | Documents Microsoft
description: "Découvrez comment toocreate, déchiffrer et modifier un package de prise en charge pour votre appareil StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: eac76f5f-5db1-4c92-af8c-54053b91e66c
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 209aeee50e823fd2ca96ababd1d0cf3ea9cdad53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-storsimple-support-package"></a>Création et gestion d’un package de prise en charge StorSimple
## <a name="overview"></a>Vue d'ensemble
Un package de prise en charge de StorSimple est un mécanisme facile à utiliser qui collecte tous les journaux appropriés tooassist Support technique de Microsoft à résoudre les problèmes de votre appareil StorSimple. Hello fichiers journaux collectés sont chiffrés et compressés.

Ce didacticiel inclut des instructions pas à pas toocreate et à gérer hello prise en charge.

## <a name="create-and-upload-a-support-package-in-hello-azure-classic-portal"></a>Créer et télécharger un package de prise en charge dans hello portail Azure classic
Vous pouvez créer et télécharger un site de Support technique de Microsoft support package toohello via hello **Maintenance** page du service hello Bonjour portail Azure classic.

> [!NOTE]
> téléchargement de Hello nécessite une clé de la prise en charge. Votre ingénieur du support technique doit fournir ce tooyou dans un message électronique.
> 
> 

Un package de prise en charge chiffré et compressé (fichier .cab) est créé et téléchargé toohello prise en charge de site. ingénieur de support Hello peut ensuite extraire ce package à partir du site du support technique pour résoudre les problème hello hello.

Effectuer hello dans toocreate portail classique hello un package de prise en charge comme suit.

#### <a name="toocreate-a-support-package-in-hello-azure-classic-portal"></a>toocreate un package de prise en charge dans hello portail Azure classic
1. Sélectionnez **Appareils** > **Maintenance**.
2. Bonjour **package de Support** section, sélectionnez **package de prise en charge de création et téléchargement**.
3. Bonjour **package de prise en charge de création et téléchargement** boîte de dialogue zone, hello suivant :
   
    ![Créer un package de support](./media/storsimple-create-manage-support-package/IC740923.png)
   
   * Bonjour **de support** texte, entrez la clé de sécurité hello. Votre ingénieur de support technique de Microsoft doit envoyer tooyou de cette clé de sécurité par courrier électronique.
   * Sélectionnez hello case tooprovide consentement tooautomatically téléchargement hello prise en charge de package toohello Support Microsoft site.
   * Cliquez sur une icône de coche hello ![Icône en forme de coche](./media/storsimple-create-manage-support-package/IC740895.png).

## <a name="manually-create-a-support-package"></a>Créer manuellement un package de support
Dans certains cas, vous devez toomanually créer le package de prise en charge de hello via Windows PowerShell pour StorSimple. Par exemple :

* Si vous avez besoin des informations sensibles tooremove à partir de votre journal des fichiers préalable toosharing avec le Support technique de Microsoft.
* Si vous avez des difficultés à télécharger le package hello en raison de problèmes de tooconnectivity.

Vous pouvez partager votre package de support généré manuellement avec le support Microsoft par e-mail. Effectuer hello suivant les étapes toocreate un package de prise en charge dans Windows PowerShell pour StorSimple.

#### <a name="toocreate-a-support-package-in-windows-powershell-for-storsimple"></a>toocreate un package de prise en charge dans Windows PowerShell pour StorSimple
1. toostart une session Windows PowerShell en tant qu’administrateur sur l’ordinateur distant hello qui a utilisé l’appareil StorSimple tooconnect tooyour, entrez hello de commande suivante :
   
    `Start PowerShell`
2. Dans la session Windows PowerShell de hello, connectez-vous toohello SSAdmin Console de votre appareil :
   
   * À l’invite de commandes hello, entrez :
     
       `$MS = New-PSSession -ComputerName <IP address for DATA 0> -Credential SSAdmin -ConfigurationName "SSAdminConsole"`
   * Dans la boîte de dialogue hello qui s’ouvre, entrez votre mot de passe administrateur. mot de passe par défaut Hello est la suivante :
     
      `Password1`
     
      ![Boîte de dialogue des informations d’identification PowerShell](./media/storsimple-create-manage-support-package/IC740962.png)
   * Sélectionnez **OK**.
   * À l’invite de commandes hello, entrez :
     
      `Enter-PSSession $MS`
3. Dans session hello qui s’ouvre, entrez la commande appropriée hello.
   
   * Pour les partages réseau protégés par un mot de passe, saisissez :
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" –Credential "Username" -Force`
     
       Vous êtes invité à entrer pour un mot de passe, un dossier partagé du réseau toohello chemin d’accès et un mot de passe de chiffrement (car le package de prise en charge hello est chiffré). Un package de prise en charge est ensuite créé dans le dossier spécifié de hello.
   * Pour les partages qui ne sont pas protégé par mot de passe, vous n’avez pas besoin hello `-Credential` paramètre. Entrez hello suivantes :
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" -Force`
     
       package de prise en charge Hello est créé pour les deux contrôleurs dans le dossier partagé du réseau spécifié hello. Il s’agit d’un fichier chiffré et compressé, qui peut être envoyé tooMicrosoft prise en charge pour le dépannage. Pour plus d'informations, consultez [Contacter le support technique de Microsoft](storsimple-contact-microsoft-support.md).

### <a name="hello-export-hcssupportpackage-cmdlet-parameters"></a>Hello des paramètres d’applet de commande Export-HcsSupportPackage
Vous pouvez utiliser hello paramètres avec l’applet de commande Export-HcsSupportPackage de hello suivants.

| Paramètre | Obligatoire ou facultatif | Description |
| --- | --- | --- |
| `-Path` |Requis |Utilisez emplacement de hello tooprovide du dossier partagé sur le réseau hello dans le hello package de prise en charge est placé. |
| `-EncryptionPassphrase` |Requis |Utilisez tooprovide une phrase secrète de toohelp chiffrer hello prise en charge du package. |
| `-Credential` |Facultatif |Utilisez toosupply informations d’identification pour le dossier partagé du réseau hello. |
| `-Force` |Facultatif |Utilisez l’étape de confirmation de phrase secrète tooskip hello chiffrement. |
| `-PackageTag` |Facultatif |Utilisez toospecify un répertoire sous *chemin d’accès* prise en charge hello package est placé. valeur par défaut Hello est [nom appareil]-[date et actuelles : dd-mm-aaaa-hh-mm-ss]. |
| `-Scope` |Facultatif |Spécifiez en tant que **Cluster** (par défaut), toocreate un package de prise en charge pour les deux contrôleurs. Si vous souhaitez toocreate un package uniquement pour le contrôleur actuel de hello, spécifiez **contrôleur**. |

## <a name="edit-a-support-package"></a>Modification d'un package de support
Une fois que vous avez généré un package de prise en charge, vous devrez peut-être des informations sensibles tooedit hello package tooremove. Cela peut inclure les noms de volume, adresses IP d’appareil et sauvegarde des fichiers de journaux hello.

> [!IMPORTANT]
> Vous pouvez uniquement modifier un package de support qui a été généré à l'aide de Windows PowerShell pour StorSimple. Vous ne pouvez pas modifier un package créé dans hello portail classique Azure avec le service StorSimple Manager.
> 
> 

tooedit un package de support avant de le télécharger sur le site de Support technique de Microsoft hello, package de support hello d’abord le déchiffrer, modifier des fichiers de hello, puis le rechiffrer. Effectuer hello comme suit.

#### <a name="tooedit-a-support-package-in-windows-powershell-for-storsimple"></a>tooedit un package de prise en charge dans Windows PowerShell pour StorSimple
1. Générer un package de prise en charge, comme décrit dans les versions antérieures, [toocreate un package de prise en charge dans Windows PowerShell pour StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).
2. [Télécharger le script de hello](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) localement sur votre client.
3. Importez le module Windows PowerShell de hello. Spécifiez hello chemin d’accès toohello dossier local dans lequel vous avez téléchargé le script de hello. module de hello tooimport, entrez :
   
    `Import-module <Path toohello folder that contains hello Windows PowerShell script>`
4. Tous les fichiers de hello sont *.aes* fichiers compressés et chiffrés. toodecompress et déchiffrer les fichiers, entrez :
   
    `Open-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    Notez que les extensions de fichier réel hello sont maintenant affichées pour tous les fichiers hello.
   
    ![Modifier un package de support](./media/storsimple-create-manage-support-package/IC750706.png)
5. Lorsque vous êtes invité à entrer hello phrase secrète de chiffrement, entrez la phrase secrète hello que vous avez utilisé lors de la création de package de support hello.
   
        cmdlet Open-HcsSupportPackage at command pipeline position 1
   
        Supply values for hello following parameters:EncryptionPassphrase: ****
6. Parcourir un dossier toohello qui contient les fichiers journaux hello. Hello fichiers journaux sont désormais décompressés et déchiffrés, il aura donc des extensions de fichier d’origine. Modifier ces tooremove fichiers toutes les informations spécifiques au client, telles que les noms de volume et les adresses IP d’appareil et enregistrez les fichiers de hello.
7. Hello fermer les fichiers toocompress avec gzip et leur chiffrement avec AES-256. Il s’agit de la vitesse et de sécurité lors du transfert du package de support hello sur un réseau. toocompress et chiffrer des fichiers, entrez hello suivante :
   
    `Close-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    ![Modifier un package de support](./media/storsimple-create-manage-support-package/IC750707.png)
8. Lorsque vous y êtes invité, fournissez une phrase secrète de chiffrement pour le package de prise en charge modifié hello.
   
        cmdlet Close-HcsSupportPackage at command pipeline position 1
        Supply values for hello following parameters:EncryptionPassphrase: ****
9. Écrivez hello nouvelle phrase secrète, afin que vous pouvez le partager avec le Support technique de Microsoft lorsqu’il est demandé.

### <a name="example-editing-files-in-a-support-package-on-a-password-protected-share"></a>Exemple : Modification de fichiers dans un package de support sur un partage protégé par mot de passe
Bonjour à l’exemple suivant montre comment toodecrypt, modifier et rechiffrer un package de prise en charge.

        PS C:\WINDOWS\system32> Import-module C:\Users\Default\StorSimple\SupportPackage\HCSSupportPackageTools.psm1

        PS C:\WINDOWS\system32> Open-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Open-HcsSupportPackage at command pipeline position 1

        Supply values for hello following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32> Close-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Close-HcsSupportPackage at command pipeline position 1

        Supply values for hello following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32>

## <a name="next-steps"></a>Étapes suivantes
* Découvrez comment trop[utilisation prise en charge de packages et périphérique se connecte tootroubleshoot votre déploiement de périphérique](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).
* Découvrez comment trop[utilisez hello tooadminister du service StorSimple Manager de votre appareil StorSimple](storsimple-manager-service-administration.md).

