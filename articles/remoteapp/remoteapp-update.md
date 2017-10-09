---
title: aaaUpdate votre collection Azure RemoteApp | Documents Microsoft
description: "Découvrez comment tooupdate votre collection Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: e553d432-e581-48fe-b996-c432357eb64a
ms.service: remoteapp
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 849d7abfdfad4dbe6a235d2a28c71f7943eb812c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="update-a-collection-in-azure-remoteapp"></a>Mise à jour d’une collection dans Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Il arrivera un moment, inévitablement, lorsque vous devez tooupdate hello applications ou l’image dans votre collection Azure RemoteApp. Si vous utilisez une des images hello inclus dans votre abonnement Azure RemoteApp, dans la collection un cloud ou hybride, mises à jour toutes les sont gérées par Azure RemoteApp lui-même, vous pouvez compter.

Toutefois, si vous utilisez une image personnalisée (que vous avez créé à partir de zéro ou que vous avez créé en modifiant un de nos images), vous êtes responsable de la gestion d’applications et image de hello. Si vous devez tooupdate votre image ou l’une des applications hello qu’il contient, vous devez toocreate une nouvelle version mise à jour d’image de hello, puis image existante du hello remplacer dans votre collection avec cette nouvelle image mis à jour.

Comment mettre à jour votre collection ? C’est simple :

1. Image de hello de mise à jour que vous avez utilisé dans votre collection. Appliquez tous les correctifs et toutes les mises à jour nécessaires, puis enregistrez-la sous un nouveau nom.
2. [Télécharger](remoteapp-uploadimage.md) ou [importer](remoteapp-image-on-azurevm.md) tooRemoteApp de cette image.
3. Maintenant, hello collection page, cliquez sur **mise à jour**.
4. Choisissez nouvelle image de hello hello **Image de modèle** liste.
5. Voici une partie difficile de hello - vous devez toodecide comment toodeal avec tous les utilisateurs qui utilisent actuellement une application dans la collection de hello. Vous avez hello options suivantes :
   
   * **Donner aux utilisateurs 60 minutes après la mise à jour hello**. Dès que la mise à jour de hello est terminée, Azure RemoteApp affichera un message tooany active les utilisateurs les invitant à toosave leur travail et le journal désactivé et reconnectez-vous. Une fois les 60 minutes écoulées, tous les utilisateurs actifs qui ne se sont pas déconnectés seront automatiquement déconnectés. Les utilisateurs peuvent se reconnecter immédiatement.
   * **Déconnecter immédiatement les utilisateurs**. Dès que la mise à jour de hello est terminée, déconnecter tous les utilisateurs automatiquement sans avertissement. Si vous choisissez cette option, les utilisateurs risquent de perdre des données. Toutefois, ils peuvent se reconnecter toohello application immédiatement.
6. Cliquez sur mise à jour de hello coche toostart hello.

