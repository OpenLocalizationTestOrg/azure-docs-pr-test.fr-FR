---
title: "configuration requise d’aaaAzure RemoteApp image | Documents Microsoft"
description: "En savoir plus sur la configuration requise de hello pour créer des toobe d’images utilisé avec Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7cbb90f4-6dc9-462c-a429-088cdb57414e
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 4e35203eb93a866d4e0bd591d42b34746c7ffa4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="requirements-for-azure-remoteapp-images"></a>Configuration requise pour les images Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Azure RemoteApp utilise un toohost d’image de Windows Server 2012 R2 tous les programmes hello que vous souhaitez tooshare avec vos utilisateurs. toocreate une image personnalisée, vous pouvez démarrer avec une image existante ou [créer un nouveau](remoteapp-create-custom-image.md).

> [!TIP]
> Saviez-vous que votre Azure RemoteApp abonnement vous donne dans qu'accès image de Windows Server 2012 R2 tooa hello galerie de machine virtuelle Azure que vous pouvez utiliser toocreate votre propre image de modèle ? [Voyez par vous-même](remoteapp-image-on-azurevm.md).  
> 
> 

exigences de Hello d’image hello qui peuvent être téléchargés pour une utilisation avec Azure RemoteApp sont :

* Applications personnalisées ne stockent des données localement sur l’image de hello. Ces images sont sans état et ne doivent contenir que des applications.
* image de Hello ne contient pas de données qui peuvent être perdues.
* taille de l’image Hello doit être un multiple de nombre de Mo. Si vous essayez de tooupload une image qui n’est pas un multiple exact, le téléchargement de hello échoue.
* taille de l’image Hello doit être 127 Go ou plus petit.
* Elle doit se trouver dans un fichier VHD (pour l'instant, les fichiers VHDX ne sont pas pris en charge).
* Hello disque dur virtuel ne doit pas être un ordinateur virtuel de génération 2.
* Hello disque dur virtuel peut être de taille fixe ou expansion dynamique. Un disque dur virtuel de taille dynamique est recommandé, car il prend moins tooAzure tooupload de temps qu’un fichier de disque dur virtuel de taille fixe.
* disque de Hello doit être initialisé à l’aide du style de partitionnement hello enregistrement de démarrage principal (MBR). Hello style de partition GUID partition GPT (table) n’est pas pris en charge.
* Hello disque dur virtuel doit contenir une seule installation de Windows Server 2012 R2. Il peut contenir plusieurs volumes, mais un seul contenant une installation de Windows.
* rôle d’ordinateur hôte de Session de bureau à distance (RDSH) Hello et la fonctionnalité expérience utilisateur hello doivent être installés.
* rôle du service Broker pour les connexions Bureau à distance Hello doit *pas* être installé.
* Hello EFS (ENCRYPTING file) doit être désactivée.
* Hello image doit être préparée avec Sysprep à l’aide des paramètres de hello **/oobe /generalize /shutdown** (ne pas utiliser hello **/mode : VM** paramètre).
* Le téléchargement de votre disque dur virtuel à partir d’une chaîne d’instantanés n’est pas pris en charge.

Consultez [Création d'une image Azure RemoteApp](remoteapp-imageoptions.md) pour plus d'informations sur la création d'images pour Azure RemoteApp.

