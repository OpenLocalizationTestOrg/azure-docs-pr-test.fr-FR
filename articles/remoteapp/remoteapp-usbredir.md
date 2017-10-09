---
title: "aaaHow vous redirigez les périphériques USB dans Azure RemoteApp ? | Microsoft Docs"
description: "Découvrez comment toouse une redirection pour les périphériques USB dans Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 191d98af-2f5a-4307-9042-aae0e4049f9f
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 661b90c0910167d76ac3886b5af7a32d00b3943f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-you-redirect-usb-devices-in-azure-remoteapp"></a>Comment rediriger les périphériques USB dans Azure RemoteApp ?
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

La redirection du périphérique permet aux utilisateurs d’utiliser hello USB périphériques attachés tootheir ordinateur ou un Tablet PC avec les applications de hello dans Azure RemoteApp. Par exemple, si vous avez partagé Skype via Azure RemoteApp, vos utilisateurs doivent toouse en mesure de toobe leurs appareils de l’appareil.

Avant de poursuivre, assurez-vous de lire les informations de redirection de USB hello dans [à l’aide de la redirection dans Azure RemoteApp](remoteapp-redirection.md). Toutefois hello recommandé nusbdevicestoredirect:s : * ne fonctionne pas pour les caméras web USB et de ne pas fonctionner pour certaines imprimantes USB ou les périphériques multifonctions USB. Par conception et pour des raisons de sécurité, administrateur d’Azure RemoteApp hello a tooenable redirection par la classe de dispositifs de GUID ou par ID d’instance de périphérique avant que vos utilisateurs peuvent utiliser ces appareils.

Bien que cet article traite de la redirection de caméra web, vous pouvez utiliser un imprimantes USB de tooredirect approche similaire et autres périphériques multifonctions USB qui ne sont pas redirigés par hello **nusbdevicestoredirect:s :*** commande.

## <a name="redirection-options-for-usb-devices"></a>Options de redirection pour périphériques USB
Azure RemoteApp utilise des mécanismes très similaires pour rediriger les périphériques USB hello ceux disponibles pour les Services Bureau à distance. Hello technologie vous permet de choisir méthode de redirection correct hello pour un périphérique donné, hello tooget meilleur des deux principales et la redirection de périphériques USB RemoteFX à l’aide de hello **usbdevicestoredirect:s :** commande. Il existe quatre éléments toothis commande :

| Ordre de traitement | Paramètre | Description |
| --- | --- | --- |
| 1 |* |Sélectionne tous les périphériques non sélectionnés par la redirection de haut niveau. Remarque : Dès le départ, * ne fonctionne pas pour les webcams USB. |
| {Identificateur global unique} |Sélectionne tous les appareils qui correspondent aux hello spécifié classe le programme d’installation de périphérique. | |
| USB\InstanceID |Sélectionne un périphérique USB spécifié pour hello donnée d’ID d’instance. | |
| 2 |-USB\Instance ID |Supprime les paramètres de redirection de hello pour le périphérique spécifié de hello. |

## <a name="redirecting-a-usb-device-by-using-hello-device-class-guid"></a>Redirection d’un périphérique USB à l’aide du GUID de la classe hello appareil
Il existe deux façons toofind hello périphérique GUID de la classe qui peut être utilisé pour la redirection. 

option de première Hello est toouse hello [tooVendors définies périphérique le programme d’installation Classes disponible](https://msdn.microsoft.com/library/windows/hardware/ff553426.aspx). Choisir la classe hello qui correspond au mieux à l’ordinateur local de hello appareil toohello attaché. Pour les appareils photo numériques, il peut s’agir de la classe de périphérique d’acquisition d’image ou de la classe de périphérique de capture vidéo. Vous devez toodo des tests avec Bonjour appareil classes toofind Bonjour correct de la classe GUID qui fonctionne avec hello localement attaché un périphérique USB (dans notre webcam hello cas).

Un meilleur moyen de hello deuxième option est toofollow ces périphérique étapes toofind hello classe GUID :

1. Ouvrir le Gestionnaire de périphériques de hello, recherchez appareil hello sera redirigé et faites un clic droit, puis ouvrez les propriétés de hello.
   ![Ouvrez le Gestionnaire de périphériques de hello](./media/remoteapp-usbredir/ra-devicemanager.png)
2. Sur hello **détails** , choisir la propriété de hello **Guid de la classe**. valeur Hello qui apparaît est hello GUID de classe pour ce type de périphérique.
   ![Propriétés de caméra](./media/remoteapp-usbredir/ra-classguid.png)
3. Utilisez hello Guid de la classe valeur tooredirect les appareils qui lui correspondent.

Par exemple :

        Set-AzureRemoteAppCollection -CollectionName <collection name> -CustomRdpProperty "nusbdevicestoredirect:s:<Class Guid value>"

Vous pouvez combiner plusieurs redirections d’appareil Bonjour même applet de commande. Par exemple : tooredirect le stockage local et la clé USB de caméra web, l’applet de commande ressemble à ceci :

        Set-AzureRemoteAppCollection -CollectionName <collection name> -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:<Class Guid value>"

Lorsque vous définissez la redirection du périphérique par le GUID de la classe tous les appareils qui correspondent aux que le GUID de la classe Bonjour spécifié collection sont redirigés. Par exemple, s’il existe plusieurs ordinateurs sur le réseau local de hello ayant hello même les webcams USB, vous pouvez exécuter une applet de commande unique de tooredirect tous les webcams hello.

## <a name="redirecting-a-usb-device-by-using-hello-device-instance-id"></a>Redirection d’un périphérique USB à l’aide des ID d’instance hello appareil
Si vous souhaitez un contrôle plus précis et que vous souhaitez que la redirection de toocontrol par périphérique, vous pouvez utiliser hello **USB\InstanceID** paramètre de la redirection.

plus difficiles Hello cette méthode trouve un ID d’instance du périphérique hello USB. Vous aurez besoin d’accès toohello ordinateur et le périphérique USB spécifique de hello. Exécutez ensuite les opérations qui suivent :

1. Activer la redirection du périphérique hello dans la Session Bureau à distance, comme décrit dans [comment puis-je utiliser mes périphériques et les ressources dans une session Bureau à distance ?](http://windows.microsoft.com/en-us/windows7/How-can-I-use-my-devices-and-resources-in-a-Remote-Desktop-session)
2. Ouvrez une connexion Bureau à distance, puis cliquez sur **Afficher les options**.
3. Cliquez sur **enregistrer en tant que** toosave hello connexion tooan RDP fichier de paramètres courant.  
    ![Enregistrer les paramètres de hello dans un fichier RDP](./media/remoteapp-usbredir/ra-saveasrdp.png)
4. Choisissez un nom de fichier et un emplacement, par exemple MyConnection.rdp et ce PC\Documents et enregistrer le fichier de hello.
5. Ouvrez hello MyConnection.rdp fichier à l’aide d’un éditeur de texte et rechercher l’ID d’instance hello du périphérique de hello souhaité tooredirect.

Maintenant, utiliser les ID d’instance hello hello suivant l’applet de commande :

    Set-AzureRemoteAppCollection -CollectionName <collection name> -CustomRdpProperty "nusbdevicestoredirect:s: USB\<Device InstanceID value>"



### <a name="help-us-help-you"></a>Vos commentaires nous aideront à mieux vous servir
Saviez-vous que toorating d’ajout de cet article et de faire des commentaires vers le bas, vous pouvez effectuer modifications toohello article ? Il manque des informations ? Des informations sont erronées ? Certains passages ne sont pas clairs ? Faites défiler et cliquez sur **modifier sur GitHub** toomake modifications - ces proviendront toous pour révision et, une fois que nous se déconnecter sur ces derniers, vous verrez alors vos modifications et des améliorations ici.

