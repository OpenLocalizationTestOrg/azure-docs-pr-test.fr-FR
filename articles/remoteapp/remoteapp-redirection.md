---
title: "la redirection d’aaaUsing dans Azure RemoteApp | Documents Microsoft"
description: "Découvrez comment la redirection de tooconfigure et utilisation de RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 2c8c867f-4907-4f2e-9ccd-2eb82bb5b837
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d5739a75cf606bd971268da67b2c5ff0fe5fe19b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-redirection-in-azure-remoteapp"></a>Utilisation de la redirection dans Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

La redirection du périphérique permet à vos utilisateurs interagissent avec les applications à distance à l’aide d’ordinateur local de hello périphériques attachés tootheir, téléphone ou tablette. Par exemple, si vous avez fourni Skype via Azure RemoteApp, l’utilisateur doit caméra hello installée sur leur toowork PC avec Skype. Cela est également vrai pour les imprimantes, les haut-parleurs, les écrans et divers périphériques connectés à un port USB.

RemoteApp tire parti de la redirection de tooprovide de protocole RDP (Remote Desktop) et RemoteFX hello.

## <a name="what-redirection-is-enabled-by-default"></a>Quelle redirection est activée par défaut ?
Lorsque vous utilisez RemoteApp, hello suit les redirections est activée par défaut. informations Hello entre parenthèses afficher les paramètres de protocole RDP hello.

* Lire les sons sur l’ordinateur local de hello (**lire sur cet ordinateur**). (audiomode:i:0)
* Capture audio depuis les ordinateurs local hello et envoi toohello à distance (**enregistrement à partir de cet ordinateur**). (audiocapturemode:i:1)
* Imprimer des imprimantes toolocal (redirectprinters:i:1)
* Ports COM (redirectcomports:i:1)
* Périphérique à carte à puce (redirectsmartcards:i:1)
* Presse-papiers (capacité toocopy et coller) (redirectclipboard:i:1)
* Lissage des polices ClearType (allowfontsmoothing:i:1)
* Rediriger tous les périphériques Plug-and-Play pris en charge. (devicestoredirect:s:*)

## <a name="what-other-redirection-is-available"></a>Quelle autre redirection est disponible ?
Deux options de redirection sont désactivées par défaut :

* La redirection du lecteur (mappage de lecteur) : lecteurs de votre ordinateur local deviennent les lecteurs mappés dans la session à distance de hello. Cela vous permet de vous enregistrer ou ouvrir des fichiers à partir de vos lecteurs locaux pendant que vous travaillez dans la session à distance de hello.
* La redirection de USB : vous pouvez utiliser l’ordinateur local de hello USB périphériques tooyour attaché au sein de la session à distance de hello.

## <a name="change-your-redirection-settings-in-remoteapp"></a>Modification de vos paramètres de redirection dans RemoteApp
Vous pouvez modifier les paramètres de redirection de périphérique hello pour une collection à l’aide de hello Microsoft Azure PowerShell avec le Kit de développement logiciel. Après avoir installé hello nouveau PowerShell et le Kit de développement logiciel, configurez tout d’abord toomanage votre abonnement comme décrit dans [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).

Utiliser un toohello similaire commande tooset hello personnalisé RDP propriétés suivantes :

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

(Notez que  *`n*  est utilisé comme séparateur entre les propriétés individuelles.)

tooget une liste de quelles propriétés RDP personnalisées sont configurées, exécutez hello suivant l’applet de commande. Notez que les propriétés personnalisées seulement sont affichées sous la forme d’un résultat et hello pas les propriétés par défaut :  

    Get-AzureRemoteAppCollection -CollectionName <collection name>

Lorsque vous définissez des propriétés personnalisées vous devez spécifier toutes les propriétés personnalisées de chaque heure ; Sinon, paramètre de hello revient toodisabled.   

### <a name="common-examples"></a>Exemples courants
Hello après la redirection du lecteur tooenable applet de commande, utilisez :  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*"

Utilisez cette applet de commande tooenable redirection USB et lecteur :

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

Utilisez cette applet de commande toodisable le partage du Presse-papiers :  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "redirectclipboard:i:0"

> [!IMPORTANT]
> Être toocompletely vraiment déconnecter tous les utilisateurs de la collection de hello (et pas seulement les déconnecter) avant de tester les modifications hello. tooensure complètement déconnexion des utilisateurs, accédez toohello **Sessions** onglet collection hello Bonjour portail Azure et de déconnexion de tous les utilisateurs sont déconnectés ou connectés. Parfois, peut prendre plusieurs secondes hello lecteurs locaux tooshow dans l’Explorateur d’au sein de la session de hello.
> 
> 

## <a name="change-usb-redirection-settings-on-your-windows-client"></a>Modification des paramètres de redirection USB sur votre client Windows
Si vous souhaitez que la redirection de toouse USB sur un ordinateur qui se connecte tooRemoteApp, il existe 2 actions nécessitant toohappen. 1 - votre administrateur doit la redirection de USB tooenable au niveau de collection hello à l’aide d’Azure PowerShell. 2 - sur chaque appareil sur lequel vous souhaitez la redirection de toouse USB, vous devez tooenable une stratégie de groupe qui l’autorise. Cette étape doit toobe fait pour chaque utilisateur qui souhaite la redirection de toouse USB.

> [!NOTE]
> La redirection USB avec Azure RemoteApp est prise en charge uniquement pour les ordinateurs Windows.
> 
> 

### <a name="enable-usb-redirection-for-hello-remoteapp-collection"></a>Activer la redirection de USB pour hello collection RemoteApp
Utilisez hello après redirection de USB tooenable applet de commande au niveau de collection hello :

    Set-AzureRemoteAppCollection -CollectionName <collection_name> -CustomRdpProperty "nusbdevicestoredirect:s:*"

### <a name="enable-usb-redirection-for-hello-client-computer"></a>Activer la redirection de USB pour l’ordinateur client de hello
paramètres de redirection tooconfigure USB sur votre ordinateur :

1. Ouvrez hello éditeur de stratégie de groupe locale (GPEDIT. MSC). (Exécutez gpedit.msc à partir d'une invite de commandes.)
2. Ouvrez **Configuration ordinateur\Stratégies\Modèles d'administration\Composants Windows\Services Bureau à distance\Client Connexion Bureau à distance\Redirection des périphériques USB RemoteFX**.
3. Double-cliquez sur **Autoriser la redirection RDP d'autres périphériques USB RemoteFX pris en charge à partir de cet ordinateur**.
4. Sélectionnez **activé**, puis sélectionnez **administrateurs et utilisateurs Bonjour RemoteFX USB la Redirection des droits d’accès**.
5. Ouvrez une invite de commandes avec des privilèges d’administrateur et exécutez hello de commande suivante :
   
        gpupdate /force
6. Redémarrez l’ordinateur de hello.

Vous pouvez également utiliser toocreate d’outil de gestion de stratégie de groupe hello et appliquer la stratégie de redirection hello USB pour tous les ordinateurs de votre domaine :

1. Connectez-vous à un contrôleur de domaine hello en tant qu’administrateur de domaine hello.
2. Ouvrez hello Group Policy Management Console. (Cliquez sur **Démarrer > Outils d'administration > Gestion des stratégies de groupe**.)
3. Accédez toohello domaine ou unité d’organisation pour laquelle vous souhaitez que la stratégie de hello de toocreate.
4. Cliquez avec le bouton droit sur **Stratégie de domaine par défaut**, puis cliquez sur **Modifier**.
5. Ouvrez **Configuration ordinateur\Stratégies\Modèles d'administration\Composants Windows\Services Bureau à distance\Client Connexion Bureau à distance\Redirection des périphériques USB RemoteFX**.
6. Double-cliquez sur **Autoriser la redirection RDP d'autres périphériques USB RemoteFX pris en charge à partir de cet ordinateur**.
7. Sélectionnez **activé**, puis sélectionnez **administrateurs et utilisateurs Bonjour RemoteFX USB la Redirection des droits d’accès**.
8. Cliquez sur **OK**.  

