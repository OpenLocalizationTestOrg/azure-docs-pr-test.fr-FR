---
title: "problèmes de stockage de fichier Azure aaaTroubleshoot dans Windows | Documents Microsoft"
description: "Résolution des problèmes liés au stockage Azure File dans Windows"
services: storage
documentationcenter: 
author: genlin
manager: willchen
editor: na
tags: storage
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: genli
ms.openlocfilehash: 19529d8af5d98790e2e381cd21ad4d0284acb124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-windows"></a>Résoudre les problèmes liés au stockage Azure File dans Windows

Cet article répertorie les problèmes courants qui sont associé tooMicrosoft de stockage de fichier Azure lorsque vous vous connectez à partir de clients Windows. Il fournit également les causes possibles et les solutions de ces problèmes. En outre des étapes de résolution des problèmes de toohello dans cet article, vous pouvez également utiliser [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) pour vous assurer que Windows hello environnement client a des éléments de configuration. AzFileDiagnostics automatise la détection de la plupart des symptômes hello citées dans cet article et permet d’ajouter des performances optimales de tooget votre environnement. Vous pouvez également trouver ces informations dans hello [de résolution des problèmes de partages de fichiers de Azure](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares) qui fournit les étapes tooassist des problèmes de partages de fichiers Azure de connexion de mappage/montage.


<a id="error53-67-87"></a>
## <a name="error-53-error-67-or-error-87-when-you-mount-or-unmount-an-azure-file-share"></a>Les messages « Erreur 53 », « Erreur 67 » ou « Erreur 87 » s’affichent lorsque vous montez ou démontez un partage de fichiers Azure

Lorsque vous essayez de toomount un partage de fichiers en local ou à partir d’un autre centre de données, vous pouvez recevoir hello les erreurs suivantes :

- Erreur système 53. chemin d’accès réseau de Hello est introuvable.
- Erreur système 67. Impossible de trouver le nom de réseau Hello.
- Erreur système 87. le paramètre Hello est incorrect.

### <a name="cause-1-unencrypted-communication-channel"></a>Cause 1 : Canal de communication non chiffrée

Pour des raisons de sécurité, les partages de fichiers tooAzure sont bloquées si le canal de communication hello n’est pas chiffré, et si la tentative de connexion de hello n’est pas effectuée à partir de connexions hello même centre de données où résident les partages de fichiers Azure hello. Chiffrement de canal de communication est fourni uniquement si hello client de l’utilisateur du système d’exploitation prend en charge le chiffrement SMB.

Windows 8, Windows Server 2012 et les versions ultérieures de chaque demande de négociation système incluant SMB 3.0, prenant en charge le chiffrement.

### <a name="solution-for-cause-1"></a>Solution pour la cause 1

Se connecter à partir d’un client qui effectue hello suivantes :

- Répond aux exigences de hello de Windows 8 et Windows Server 2012 ou versions ultérieures
- Se connecte à partir d’une machine virtuelle dans hello même centre de données comme compte de stockage Azure qui est utilisé pour le partage de fichiers Azure hello de hello

### <a name="cause-2-port-445-is-blocked"></a>Cause 2 : Le Port 445 est bloqué

Erreur système 53 ou l’erreur système 67 peut se produire si le port 445 les communications sortantes tooan fichier Azure stockage centre de données est bloquée. Résumé de hello toosee de fournisseurs de services Internet autoriser ou interdire l’accès à partir du port 445, accédez trop[TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx).

toounderstand s’il s’agit du message « Erreur système 53 » hello raison hello, vous pouvez utiliser le point de terminaison TCP:445 Portqry tooquery hello. Si le point de terminaison TCP:445 hello est affiché comme filtrés, hello le port TCP est bloqué. Voici un exemple de requête :

  `g:\DataDump\Tools\Portqry>PortQry.exe -n [storage account name].file.core.windows.net -p TCP -e 445`

Si le port TCP 445 est bloqué par une règle de chemin d’accès réseau de hello, vous verrez hello suivant de sortie :

  `TCP port 445 (microsoft-ds service): FILTERED`

Pour plus d’informations sur la façon toouse Portqry, consultez [Description de l’utilitaire de ligne de commande Portqry.exe hello](https://support.microsoft.com/help/310099).

### <a name="solution-for-cause-2"></a>Solution pour la cause 2

Fonctionne avec votre service informatique service tooopen le port 445 sortant trop[plages d’adresses IP de Azure](https://www.microsoft.com/download/details.aspx?id=41653).

### <a name="cause-3-ntlmv1-is-enabled"></a>Cause 3 : NTLMv1 est activé

Erreur système 53 ou erreur 87 du système peut se produire si la communication NTLMv1 est activée sur le client de hello. Le stockage Azure File prend uniquement en charge l’authentification NTLMv2. Le fait d’activer NTLMv1 crée un client moins sécurisé. Par conséquent, les communications sont bloquées pour le stockage Azure File. 

toodetermine s’il s’agit de cause hello d’erreur de hello, vérifiez que hello suivant la sous-clé de Registre est définie la valeur tooa 3 :

**HKLM\SYSTEM\CurrentControlSet\Control\Lsa &gt; LmCompatibilityLevel**

Pour plus d’informations, consultez hello [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) rubrique sur TechNet.

### <a name="solution-for-cause-3"></a>Solution pour la cause 3

Rétablir hello **LmCompatibilityLevel** valeur par défaut toohello 3 Bonjour suivant la sous-clé de Registre :

  **HKLM\SYSTEM\CurrentControlSet\Control\Lsa**

<a id="error1816"></a>
## <a name="error-1816-not-enough-quota-is-available-tooprocess-this-command-when-you-copy-tooan-azure-file-share"></a>Erreur 1816 « pas de suffisamment de quota est disponible tooprocess cette commande » lorsque vous copiez le partage de fichiers Azure tooan

### <a name="cause"></a>Cause :

Erreur 1816 se produit lorsque vous atteignez la limite supérieure de hello de handles ouverts simultanées autorisées pour un fichier sur l’ordinateur de hello où le partage de fichiers hello est en cours monté.

### <a name="solution"></a>Solution

Réduire le nombre hello de handles ouverts simultanées en fermant certaines poignées, puis recommencez. Pour plus d’informations, consultez [Liste de contrôle des performances et de l’extensibilité de Microsoft Azure Storage](../common/storage-performance-checklist.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-tooand-from-azure-file-storage-in-windows"></a>Fichier lente copie tooand à partir du stockage Windows Azure File

Vous pouvez voir le ralentissement des performances lorsque vous essayez de tootransfer toohello de fichiers Azure File service.

- Si vous n’avez pas une exigence de taille d’e/s minimale spécifique, nous recommandons d’utiliser 1 Mo comme hello taille d’e/s pour des performances optimales.
-   Si vous connaissez taille finale de hello d’un fichier que vous étendez avec écrit et votre logiciel n’a pas des problèmes de compatibilité lorsque hello non écrit la fin du fichier de hello contient des zéros non significatifs, puis ensemble hello taille de fichier à l’avance, au lieu d’effectuer chaque écriture une écriture d’extension.
-   Utilisez hello droite copy (méthode) :
    -   Utilisez [AZCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#file-copy) pour les transferts entre deux partages de fichiers.
    -   Utilisez [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) entre des partages de fichiers sur un ordinateur local.

### <a name="considerations-for-windows-81-or-windows-server-2012-r2"></a>Informations pour Windows 8.1 ou Windows Server 2012 R2

Pour les clients qui exécutent Windows 8.1 ou Windows Server 2012 R2, assurez-vous que ce hello [KB3114025](https://support.microsoft.com/help/3114025) correctif logiciel est installé. Ce correctif logiciel améliore les performances de hello de créer et fermer des descripteurs.

Vous pouvez exécuter hello suivant toocheck de script si hello correctif a été installé :

`reg query HKLM\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies`

Si le correctif est installé, hello sortie suivante s’affiche :

`HKEY_Local_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies {96c345ef-3cac-477b-8fcd-bea1a564241c} REG_DWORD 0x1`

> [!Note]
> Les images de Windows Server 2012 R2 dans Azure Marketplace ont le correctif logiciel KB3114025 installé par défaut à compter de décembre 2015.

<a id="shareismissing"></a>
## <a name="no-folder-with-a-drive-letter-in-my-computer"></a>Aucun dossier avec une lettre de lecteur dans **Poste de travail**

Si vous mappez un partage de fichiers Azure en tant qu’administrateur à l’aide de nette utilisation, le partage de hello apparaît toobe manquant.

### <a name="cause"></a>Cause :

Par défaut, l’Explorateur Windows ne s’exécute pas en tant qu’administrateur. Si vous exécutez l’utilisation de nette à partir d’une invite de commandes d’administration, vous mappez un lecteur réseau hello en tant qu’administrateur. Étant donné que les lecteurs mappés sont centrées sur l’utilisateur, compte d’utilisateur hello est enregistré dans n’affiche pas hello lecteurs s’ils sont montés sous un compte d’utilisateur différent.

### <a name="solution"></a>Solution
Montez hello partage à partir d’une ligne de commande non administrateur. Vous pouvez également suivre [cette rubrique TechNet](https://technet.microsoft.com/library/ee844140.aspx) tooconfigure hello **EnableLinkedConnections** valeur de Registre.

<a id="netuse"></a>
## <a name="net-use-command-fails-if-hello-storage-account-contains-a-forward-slash"></a>Commande net use échoue si le compte de stockage hello contient une barre oblique

### <a name="cause"></a>Cause :

commande net use de Hello interprète une barre oblique (/) comme option de ligne de commande. Si le nom de votre compte d’utilisateur commence par une barre oblique, mappage de lecteur hello échoue.

### <a name="solution"></a>Solution

Vous pouvez utiliser une des hello suivant toowork étapes contourner problème de hello :

- Exécutez hello suivant de commande PowerShell :

  `New-SmbMapping -LocalPath y: -RemotePath \\server\share -UserName accountName -Password "password can contain / and \ etc" `

  À partir d’un fichier de commandes, vous pouvez exécuter commande hello de cette façon :

  `Echo new-smbMapping ... | powershell -command –`

- Placez entre guillemets doubles hello de clé toowork résoudre ce problème, à moins que la barre oblique hello est le premier caractère de hello. S’il s’agit, utilisez le mode interactif hello et entrez votre mot de passe séparément ou régénérer vos clés de tooget une clé qui ne commence pas par une barre oblique.

<a id="cannotaccess"></a>
## <a name="application-or-service-cannot-access-a-mounted-azure-file-storage-drive"></a>L’application ou service ne peut pas accéder à un lecteur monté de stockage Azure File

### <a name="cause"></a>Cause :

Les lecteurs sont montés par l’utilisateur. Si votre application ou service s’exécute sous un compte d’utilisateur différent hello qui hello lecteur monté, application hello ne verrez pas le lecteur de hello.

### <a name="solution"></a>Solution

Utilisez une des hello suivant solutions :

-   Monter le lecteur de hello de hello même compte d’utilisateur qui contient l’application hello. Vous pouvez utiliser un outil tel que PsExec.
- Passer le nom de compte de stockage hello et la clé des paramètres de nom et mot de passe d’utilisateur de la commande net use de hello hello.

Après avoir suivi ces instructions, vous pouvez recevoir hello message d’erreur suivant lorsque vous exécutez nette utilisation pour le compte de service réseau ou de systèmes hello : « erreur du système 1312 s’est produite. Une session ouverte spécifiée n’existe pas. Il se peut qu’elle ait été déjà fermée. » Si cela se produit, assurez-vous que ce nom d’utilisateur de hello est passé toonet utilisation inclut des informations de domaine (par exemple : « [nom du compte de stockage]. file.core.windows .net »).

<a id="doesnotsupportencryption"></a>
## <a name="error-you-are-copying-a-file-tooa-destination-that-does-not-support-encryption"></a>Erreur « Vous copiez une destination de tooa de fichier qui ne prend pas en charge le chiffrement »

Lorsqu’un fichier est copié sur le réseau de hello, hello est déchiffrée sur ordinateur source de hello, transmis en texte brut, puis de nouveau chiffrée à la destination de hello. Toutefois, vous pouvez voir l’erreur suivante lorsque vous essayez de toocopy un fichier chiffré de hello : «, vous copiez hello fichier tooa destination qui ne prend pas en charge le chiffrement. »

### <a name="cause"></a>Cause :
Ce problème peut se survenir si vous utilisez le système de fichiers EFS (Encrypting File System). Les fichiers chiffrés par BitLocker peuvent être copié tooAzure le stockage de fichiers. Toutefois, le stockage Azure File ne prend pas en charge le système de fichiers EFS NTFS.

### <a name="workaround"></a>Solution de contournement
toocopy un fichier réseau hello, vous devez tout d’abord le déchiffrer. Utilisez une des méthodes suivantes de hello :

- Hello d’utilisation **copier /d** commande. Il permet de hello chiffré fichiers toobe enregistré en tant que fichiers déchiffrés à la destination de hello.
- Hello du jeu de clé de Registre suivante :
  - Chemin d’accès = HKLM\Software\Policies\Microsoft\Windows\System
  - Type de valeur = DWORD
  - Nom = CopyFileAllowDecryptedRemoteDestination
  - Valeur = 1

N’oubliez pas de que clé de Registre paramètre hello affecte toutes les opérations de copie sont effectuées toonetwork partages.

## <a name="need-help-contact-support"></a>Vous avez besoin d’aide ? Contactez le support technique.
Si vous avez besoin d’aide, [contactez le support technique](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget votre problème résolu rapidement.
