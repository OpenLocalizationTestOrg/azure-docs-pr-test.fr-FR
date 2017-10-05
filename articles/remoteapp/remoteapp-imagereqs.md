---
title: "Configuration requise pour les images Azure RemoteApp | Microsoft Docs"
description: "En savoir plus sur la configuration requise pour la création d’images à utiliser avec Azure RemoteApp"
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
ms.openlocfilehash: 75b0f8d6b25a80f11002b683152cfb294cbb68bd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="requirements-for-azure-remoteapp-images"></a>Configuration requise pour les images Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Pour plus d’informations, lisez [l’annonce](https://go.microsoft.com/fwlink/?linkid=821148) .
> 
> 

Azure RemoteApp utilise une image Windows Server 2012 R2 pour héberger tous les programmes que vous souhaitez partager avec vos utilisateurs. Pour créer une image personnalisée, vous pouvez commencer avec une image existante ou en [créer une](remoteapp-create-custom-image.md).

> [!TIP]
> Saviez-vous que votre abonnement Azure RemoteApp vous donne accès à une image Windows Server 2012 R2 dans la galerie de machines virtuelles Azure et que vous pouvez l’utiliser pour créer votre propre image de modèle ? [Voyez par vous-même](remoteapp-image-on-azurevm.md).  
> 
> 

Vous trouverez, ci-dessous, les exigences relatives à l’image qui peut être téléchargée en vue d'être utilisée avec Azure RemoteApp :

* Les applications personnalisées ne stockent pas de données localement sur l’image. Ces images sont sans état et ne doivent contenir que des applications.
* L’image ne contient pas de données pouvant être perdues.
* La taille de l'image doit être un multiple de Mo. Si vous tentez de télécharger une image dont la taille n'est pas un multiple exact de Mo, le téléchargement échouera.
* La taille de l'image doit être de 127 Go ou moins.
* Elle doit se trouver dans un fichier VHD (pour l'instant, les fichiers VHDX ne sont pas pris en charge).
* Le disque dur virtuel ne doit pas être une machine virtuelle de deuxième génération.
* Le disque dur virtuel (VHD) peut être de taille fixe ou dynamique. L'utilisation d'un fichier VHD de taille dynamique est recommandée, car le téléchargement sur Azure prend moins de temps qu'un fichier VHD de taille fixe.
* Le disque doit être initialisé à l'aide du type de partitionnement MBR (Enregistrement de démarrage principal). Le style de partition GPT (GUID Partition Table) n'est pas pris en charge.
* Le disque dur virtuel doit contenir une seule installation de Windows Server 2012 R2. Il peut contenir plusieurs volumes, mais un seul contenant une installation de Windows.
* Le rôle RDSH (Hôte de session Bureau à distance) et la fonctionnalité Expérience utilisateur doivent être installés.
* Le rôle de service Broker pour les connexions Bureau à distance ne doit *pas* être installé.
* Le système de fichiers EFS (Encrypting File System) doit être désactivé.
* L'image doit être préparée avec SYSPREP en utilisant les paramètres **/oobe /generalize /shutdown** (n'utilisez PAS le paramètre **/mode:vm**).
* Le téléchargement de votre disque dur virtuel à partir d’une chaîne d’instantanés n’est pas pris en charge.

Consultez [Création d'une image Azure RemoteApp](remoteapp-imageoptions.md) pour plus d'informations sur la création d'images pour Azure RemoteApp.

