---
title: aaaPublish une application dans Azure RemoteApp | Documents Microsoft
description: "Découvrez comment toopublish applications et ressources dans Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: c7e1a2cd-8e1f-4a33-bd43-8032ec9ac952
ms.service: remoteapp
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d7d92187e9ed999ac79554c9bb61f56a8eceeb31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopublish-an-app-in-remoteapp"></a>Comment toopublish une application de RemoteApp
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Après avoir créé votre collection RemoteApp, vous devez toopublish hello applications ou les ressources que vous souhaitez toomake disponible pour vos utilisateurs. Hello images de modèle fournis avec votre abonnement n’ont quelques applications publiées par défaut - tooshare hello d’autres applications, vous devez toopublish les.

> [!NOTE]
> Avez-vous besoin d’une application de tooupdate ? Vous devez trop[mise à jour hello image](remoteapp-update.md) première.
> 
> 

Sur hello **publication** dans le portail de hello, cliquez sur **publier**. Vous pouvez ajouter une application à partir de votre image de modèle **Démarrer** menu ou fournissez hello chemin d’accès toowhere hello application est installée sur l’image de modèle hello. Si vous choisissez tooadd hello **Démarrer** menu, choisissez hello application toopublish à partir de la liste de hello. Si vous choisissez application toohello de tooprovide hello chemin d’accès, entrez un nom pour l’application hello et application de toohello hello chemin d’accès. Utiliser des variables dans le chemin d’accès hello - par exemple, « % lecteur_système % » au lieu de « c:\".

> [!NOTE]
> Si vous souhaitez tooadd votre application à partir de hello **Démarrer** menu, vous devez toohave *ajouté ce toohello application **Démarrer** menu sur votre image de modèle.* Dans le cas contraire, RemoteApp s’affiche uniquement les *est* sur hello **Démarrer** menu et vous ne sera pas. 
> 
> toomake que votre application est Bonjour **Démarrer** menu, placez un fichier de raccourci - **.lnk** : hello %systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs dossier.
> 
> Si vous avez oublié tooadd hello application toohello **Démarrer** menu lorsque vous avez créé le modèle de hello, choisissez application toohello de tooadd hello chemin d’accès. (Ou recréez votre image de modèle, mais c'est un peu plus de travail.)
> 
> 

