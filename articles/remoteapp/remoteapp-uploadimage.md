---
title: "aaaUpload une image personnalisée pour Azure RemoteApp | Documents Microsoft"
description: "Découvrez comment tooupload personnalisé d’images pour Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: 299e0510-1a6b-4fdf-914a-3631b061a360
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: ericor
ms.openlocfilehash: 6ad40fe58795ece37f4c7900be01bc713938da87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-custom-image-for-azure-remoteapp"></a>Téléchargement d'une image personnalisée pour Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Maintenant que vous avez créé votre image de modèle personnalisé ou que vous avez mis à jour avec les modifications, vous devez tooupload cette bibliothèque d’images tooyour image Azure RemoteApp. Suivez ces étapes.

## <a name="before-you-start"></a>Avant de commencer
1. Vérifiez que votre image personnalisée répond à hello [spécifications de l’image](remoteapp-imagereqs.md) et [configuration requise pour application](remoteapp-appreqs.md).
2. Installer hello [module Azure PowerShell](/powershell/azure/overview).

## <a name="step-by-step-on-how-tooupload-custom-image"></a>Étape par étape sur l’image personnalisée de tooupload
1. Ouvrez le portail de gestion Azure et accédez toohello RemoteApp page.
2. Sur hello **images de modèle** , cliquez sur **télécharger** bas hello de page de hello.
3. Entrez un nom convivial pour votre image et spécifier l’emplacement du compte de stockage hello. Vérifiez hello trouve hello même emplacement que votre collection RemoteApp ou un emplacement où vous voulez toocreate un.
4. Lorsque vous y êtes invité, télécharger hello script tooyour PC local.
5. Copier les paramètres de commande hello dans le Presse-papiers de tooyour de zone de texte hello.
6. Ouvrez une fenêtre Windows PowerShell avec élévation de privilèges.
7. À partir de hello élevés fenêtre Windows PowerShell, accédez toohello même répertoire où vous avez téléchargé le script de hello.
8. Hello de coller copier la commande et appuyez sur **entrée**.
   
   processus de téléchargement Hello commence et durée dépendent de nombreux facteurs, notamment votre vitesse du réseau et la taille d’image de hello
9. Si votre téléchargement ne réussit pas à cause d’interruption du réseau ou les choses comme cela, vous pouvez toujours reprendre les processus de téléchargement hello que vous a commencé. tooresume un téléchargement, exécuter le script hello en utilisant hello même ligne de commande.

> [!WARNING]
> Ne modifiez jamais de script de téléchargement hello. Vérifications spécifiques ont été implémentée tooensure qui hello image répond aux exigences de l’image hello et exigences de l’application.
> 
> 

## <a name="common-problems"></a>Problèmes courants
* Veillez à utiliser Windows PowerShell, et non Azure PowerShell. Vous devez le module Azure PowerShell de hello tooinstall, car certains modules sont nécessaires au cours du processus de téléchargement hello.
* Script de hello ne modifient jamais, sont les validations de commodité.
* Si le fichier de disque dur virtuel hello obtient verrouillé pendant le téléchargement, copiez le fichier de hello ou déplacez-le tooa nouveau emplacement et la tentative de téléchargement à nouveau. Un processus Windows peut empêcher le téléchargement.  

