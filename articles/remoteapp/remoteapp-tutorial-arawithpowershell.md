---
title: aaaUse avec Azure RemoteApp, les applets de commande PowerShell | Documents Microsoft
description: "Découvrez comment toouse applets de commande Windows PowerShell dans Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: guscatalano
manager: mbaldwin
editor: 
ms.assetid: 7d3d5ded-6f73-4de6-a8ac-c1d622e842a2
ms.service: remoteapp
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: a09cae2093e2c3a4a2ed673b5d148a22ceb935f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-windows-powershell-cmdlets-with-azure-remoteapp"></a>Utiliser les applets de commande Windows PowerShell avec Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

 Vous pouvez utiliser des tooadminister d’applets de commande PowerShell de Azure RemoteApp hello et mettre à jour de vos collections. Utilisez hello suivant tooget informations a démarré.

## <a name="get-hello-cmdlets"></a>Obtenir les applets de commande hello
- - -
Tout d’abord télécharger les applets de commande Powershell Azure hello [ici](http://go.microsoft.com/?linkid=9811175), applets de commande hello RemoteApp sont inclus. 

Extraire hello [aide d’applet de commande Azure RemoteApp](/powershell/module/azure?view=azuresmps-3.7.0).

## <a name="configure-azure-cmdlets-toouse-your-subscription"></a>Configurer les applets de commande Azure toouse votre abonnement
- - -
Suivez [ce guide](/powershell/azure/overview) afin de pouvoir utiliser les applets de commande hello sur votre abonnement Azure.

Vous pouvez utiliser ces tooget étapes démarrage rapide :

1. Téléchargez et installez hello [applets de commande Azure PowerShell](http://go.microsoft.com/?linkid=9811175).
2. Lancez Microsoft Azure PowerShell.
3. Exécutez **Add-AzureAccount** tooauthenticate tooyour abonnement Azure. Lorsque vous y êtes invité, entrez hello du même nom d’utilisateur et mot de passe que vous utilisez toosign dans tooAzure portal.  
4. Exécutez **Get-AzureSubscription** les abonnements de hello toolist associés à votre compte d’utilisateur. 
5. Exécutez **Select-AzureSubscription - SubscriptionName &lt;nom de l’abonnement&gt;**  ou **Select-AzureSubscription - SubscriptionId &lt;ID d’abonnement&gt;**  toospecify hello abonnement toouse.

Félicitations, votre console Azure PowerShell est configuré et prêt toouse. N’oubliez pas que vous devez toorepeate les étapes 2 à 5 chaque fois que vous démarrez la console Azure PowerShell de hello hello.  


## <a name="list-all-collections"></a>Afficher la liste de toutes les collections
- - -
     Get-AzureRemoteAppCollection

## <a name="delete-a-collection"></a>Supprimer une collection
- - -
    Remove-AzureRemoteAppCollection <enter collection name>

Exemple : `Remove-AzureRemoteAppCollection ContosoProduction`.

## <a name="create-a-cloud-collection"></a>Création d'une collection cloud
- - -
Il est simple, exécutez hello de commande suivante :

    New-AzureRemoteAppCollection -Collectionname RAppO365Col1 -ImageName "Office 365 ProPlus (Subscription required)" -Plan Basic -Location "West US" - Description "Office 365 Collection."

Hello au-dessus de commande publie automatiquement les applications Microsoft Office 365 (Excel, OneNote, Outlook, PowerPoint, Visio et Word).

Création de la collection peut prendre 30 minutes ou plu toocomplete. Par conséquent, cette commande renvoie un ID de suivi que vous pouvez utiliser de la manière suivante :

    Get-AzureRemoteAppOperationResult -TrackingId xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

Une fois que la collection de hello est terminée, vous pouvez ajouter toohello regroupement des utilisateurs avec hello de commande suivante :

    Add-AzureRemoteAppUser -CollectionName RAppO365Col1 -Type microsoftAccount -UserUpn someone@domain.com

Vous avez terminé ! Cet utilisateur doit être l’application de toohello tooconnect en mesure d’à l’aide du client d’Azure RemoteApp hello trouvé [ici](https://www.remoteapp.windowsazure.com/).

## <a name="available-cmdlets"></a>Applets de commande disponibles
Il existe un grand nombre d’autres commandes qui nous ont, documentation hello pour les est bientôt disponibles :

Applets de commande de base de la collection RemoteApp : 

* New-AzureRemoteAppCollection
* Get-AzureRemoteAppCollection
* Set-AzureRemoteAppCollection
* Update-AzureRemoteAppCollection
* Remove-AzureRemoteAppCollection
* Add-AzureRemoteAppUser
* Get-AzureRemoteAppUser
* Remove-AzureRemoteAppUser
* Get-AzureRemoteAppSession
* Disconnect-AzureRemoteAppSession
* Invoke-AzureRemoteAppSessionLogoff
* Send-AzureRemoteAppSessionMessage
* Get-AzureRemoteAppProgram
* Get-AzureRemoteAppStartMenuProgram
* Publish-AzureRemoteAppProgram
* Unpublish-AzureRemoteAppProgram
* Get-AzureRemoteAppCollectionUsageDetails
* Get-AzureRemoteAppCollectionUsageSummary
* Get-AzureRemoteAppPlan

Applets de commande du réseau virtuel RemoteApp :

* New-AzureRemoteAppVNet
* Get-AzureRemoteAppVNet
* Set-AzureRemoteAppVNet
* Remove-AzureRemoteAppVNet
* Get-AzureRemoteAppVpnDevice
* Get-- AzureRemoteAppVpnDeviceConfigScript
* Reset-AzureRemoteAppVpnSharedKey

Applets de commande de l’image du modèle RemoteApp :

* New-AzureRemoteAppTemplateImage
* Get-AzureRemoteAppTemplateImage
* Rename-AzureRemoteAppTemplateImage
* Remove-AzureRemoteAppTemplateImage

Autres applets de commande RemoteApp :

* Get-AzureRemoteAppLocation
* Get-AzureRemoteAppWorkspace
* Set-AzureRemoteAppWorkspace
* Get-AzureRemoteAppOperationResult

