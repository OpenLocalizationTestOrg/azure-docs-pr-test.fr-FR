---
title: Licences Azure RemoteApp | Microsoft Docs
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
ms.openlocfilehash: 4c1ad1657ab628283f071afbc9361d67cc301417
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-does-licensing-work-in-azure-remoteapp"></a>Fonctionnement des licences dans Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Pour plus d’informations, lisez [l’annonce](https://go.microsoft.com/fwlink/?linkid=821148) .
> 
> 

Vous avez donc configuré votre service Azure RemoteApp, créé vos modèles et vous êtes prêt à publier des applications pour vos utilisateurs. Toutefois, vous devez encore résoudre la question des licences. Et comprendre comment elles fonctionnent pour RemoteApp et les applications que vous partagez par l’intermédiaire de RemoteApp.

RemoteApp ne requiert pas de licences Windows ni de licences d'accès client du Bureau à distance. Votre abonnement s’occupe du côté RemoteApp lui-même. (Consultez les détails des [plans de tarification](https://azure.microsoft.com/pricing/details/remoteapp).)

Si vous utilisez l’une des images incluses dans votre abonnement, vous pouvez partager n’importe laquelle des applications installées sur cette image sans avoir besoin d’une licence distincte. Par exemple, si vous utilisez l'image de modèle Windows Server 2012 R2 pour créer votre collection, vous pouvez partager System Center Endpoint Protection avec vos utilisateurs. Les seules exceptions à cette règle sont Office 365 ProPlus, qui requiert un abonnement distinct et Office 2013 qui ne peut pas être partagé dans une collection de production.

Si vous voulez utiliser l'image de modèle Office 365 incluse dans RemoteApp, vous devez disposer d'une offre Office 365 ProPlus *existante* . Cela s'applique également à n'importe quelle application Office 365 que vous publiez à l'aide d'un modèle personnalisé. Vous devez activer les applications avec votre propre abonnement. Cela s’applique aux abonnements d’évaluation et payants. Si vous voulez utiliser l’image de modèle Office 365 pendant la période d’évaluation, *et que vous ne disposez pas déjà d’un abonnement*, accédez à la page Office 365 pour [souscrire](https://go.microsoft.com/fwlink/p/?LinkID=403802) un abonnement d’évaluation. Consultez [Comment RemoteApp et Office fonctionnent ensemble](remoteapp-o365.md) pour plus d'informations.

Si pendant la période d’évaluation, vous ne voulez pas bénéficier d’un abonnement d’évaluation à Office 365, utilisez l’image de modèle Office Professionnel Plus 2013 incluse dans RemoteApp. Cette image de modèle peut uniquement être utilisée pendant 30 jours et ne peut pas être convertie en collection payante.

Pour les autres applications, vous devez vous assurer de disposer de la licence appropriée pour partager l'application.

Ce qui paraît logique. Vous pouvez publier une application que vous êtes légalement habilité à partager. Pour cela vous devez vous assurer que vous avez l'autorisation de partager vos programmes.

Notez que vous ne pouvez pas utiliser de contrat de licence d'accès client ou de contrat de licence en volume dans une collection cloud. Vous *pouvez* utiliser un contrat de licence en volume pour activer des applications dans votre collection hybride (sauf pour Office). Vous devez simplement les installer dans votre image de modèle à partir du support de la licence en volume. Suivez les instructions du fournisseur de l'application pour installer des licences dans un environnement Bureau à distance.

