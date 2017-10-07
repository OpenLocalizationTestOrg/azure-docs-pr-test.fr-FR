---
title: Gestionnaire de licences RemoteApp aaaAzure | Documents Microsoft
description: "Découvrez comment fonctionnent les licences dans Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: ff8ebd20-61a1-4f10-87a6-234a170534c9
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: dfa808a65ea6b1a78bf74f3daddb9a84e186eebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-licensing-work-in-azure-remoteapp"></a>Fonctionnement des licences dans Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Par conséquent, vous avez défini votre service Azure RemoteApp, créé vos modèles et prêt toopublish applications tooyour utilisateurs. Mais il existe toujours un toofigure chose dernière out : Gestionnaire de licences. Simplement fonctionnement des licences pour RemoteApp et pour les applications de hello que vous partagez via RemoteApp

RemoteApp ne requiert pas de licences Windows ni de licences d'accès client du Bureau à distance. Votre abonnement prend en charge de hello côté RemoteApp lui-même. (Vérifiez les détails de hello Hello [plans de tarification](https://azure.microsoft.com/pricing/details/remoteapp).)

Si vous utilisez une des images de hello est inclus dans votre abonnement, vous pouvez partager des applications hello installées sur cette image sans avoir besoin d’une licence distincte. Par exemple, si vous utilisez hello Windows Server 2012 R2 modèle image toobuild votre collection, vous pouvez partager de System Center Endpoint Protection avec vos utilisateurs. Hello uniquement les règles de toothis exceptions sont Office 365 ProPlus, ce qui nécessite un abonnement distinct, et Office 2013, qui ne peut pas être partagée dans un regroupement de préproduction.

Si vous souhaitez toouse hello Office 365 modèle image qui est fourni avec RemoteApp, vous devez avoir un *existant* plan Office 365 ProPlus. Hello qu'est également vrai pour n’importe quelle application Office 365 que vous publiez à l’aide d’un modèle personnalisé. Vous devez tooactivate hello applications avec votre propre abonnement. Cela s’applique aux abonnements d’évaluation et payants. Si vous souhaitez l’image de modèle toouse hello Office 365 pendant la période d’évaluation de hello, *et vous n’avez pas déjà un abonnement*, accédez toohello Office 365 page trop[inscrire](https://go.microsoft.com/fwlink/p/?LinkID=403802) pour un abonnement d’évaluation. Consultez [Comment RemoteApp et Office fonctionnent ensemble](remoteapp-o365.md) pour plus d'informations.

Si, pendant la période d’évaluation de hello, vous ne souhaitez pas d’évaluation tooget un Office 365, utilisez image de modèle d’Office 2013 Professionnel Plus hello est fourni avec RemoteApp. Cette image de modèle peut uniquement être utilisée pendant 30 jours et ne peut pas être convertie en collection payante.

Pour les autres applications, vous devez toomake que vous avez hello licence tooshare hello application.

Ce qui paraît logique. Vous pouvez publier n’importe quelle application que vous pouvez légalement tooshare. Et vous devez toomake que vous êtes vraiment intitulée tooshare vos programmes.

Notez que vous ne pouvez pas utiliser de contrat de licence d'accès client ou de contrat de licence en volume dans une collection cloud. Vous *pouvez* utiliser une application de tooactivate de contrat de licence en Volume dans votre collection hybride (à l’exception d’Office). Vous devez simplement tooinstall en fonction de votre modèle de l’image à partir de hello support de licence en Volume. Suivez les informations hello hello application fournisseur tooinstall des licences dans un environnement de bureau à distance.

