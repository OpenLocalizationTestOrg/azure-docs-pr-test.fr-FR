---
title: "aaaGet hello même expérience Office 365 sur n’importe quel appareil avec Azure RemoteApp | Documents Microsoft"
description: "Découvrez comment tooshare n’importe quelle application Office 365 avec vos utilisateurs à l’aide d’Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: guscatalano
manager: mbaldwin
editor: 
ms.assetid: 0c971ce9-7d45-4cfb-9737-15b6706047e8
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 11/23/2016
ms.author: guscatal;elizapo
ms.openlocfilehash: 140056c22c8c69b9ec605318e35a72b144da07eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-same-office-365-experience-on-any-device-with-azure-remoteapp"></a>Get hello même expérience Office 365 sur n’importe quel appareil avec Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Cet article décrit comment toodeploy Office 365 sur n’importe quel appareil dans votre entreprise. Les utilisateurs peuvent obtenir les mêmes fonctionnalités hello et l’interface utilisateur d’expérience sur Android, Apple et Windows.

Pour ce faire, nous allons utiliser Azure RemoteApp en hébergeant Office 365 sur des machines virtuelles évolutives dans Azure, auxquelles les utilisateurs peuvent se connecter. Nous appelons cet ensemble de machines virtuelles une « collection cloud ».

## <a name="create-a-cloud-collection"></a>Création d'une collection cloud
Après avoir créé un compte Azure, accédez d’abord trop**RemoteApp** en cliquant sur le lien hello sur hello côté gauche.
![Affichage d’Azure RemoteApp sur hello portail Azure](./media/remoteapp-tutorial-o365anywhere/1-menu.png)

Poursuivez en cliquant sur **nouveau** sur bas de hello et « création rapide » une collection. Fournir le nom, région de hello, abonnement de hello, plan de hello et l’image hello « Proffesional Office 2013 » que nous fournissons.
![Boîte de dialogue Créer](./media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)

Une fois que vous avez terminé le processus de création de collection hello écran hello doit démarrer. Cela peut prendre jusqu'à tooan heures ou des cas.

![En attente](./media/remoteapp-tutorial-o365anywhere/3-waiting.png)

Une fois le processus de hello est terminé, il ressemble à ceci. Si vous cliquez sur **Publication** , vous voyez que la plupart des applications Office ont déjà été publiées.
![La collection a été créée](./media/remoteapp-tutorial-o365anywhere/4-done.png)

![Applications publiées](./media/remoteapp-tutorial-o365anywhere/5-publish.png)

À ce stade, vous pouvez également ajouter des utilisateurs qui ont accès toothis collection en cliquant sur **accès utilisateur**.
![Configuration de l'accès utilisateur](./media/remoteapp-tutorial-o365anywhere/6-user.png)

Maintenant nous allons tester la connexion tooOffice 365 !

## <a name="connect-toooffice-365"></a>Se connecter tooOffice 365
Nous allons head sur trop[https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/), faites défiler la liste et cliquez sur **télécharger des clients** client de Azure RemoteApp tooinstall hello sur périphérique hello sur. captures d’écran Hello ci-dessous sont pour Windows.

Une fois que l’application hello démarre vous serez invité à indiquer toosign avec votre compte Microsoft (anciennement appelé « Live ID »), utilisez hello identique à celui que votre compte Azure pour l’instant. Une fois connecté, vous devriez voir une notification vous indiquant de nouvelles invitations. Cliquez dessus pour afficher une liste comme celle ci-dessous. Accepter l’invitation hello qui correspond à votre adresse de messagerie du propriétaire du compte Azure.

![Nouvelle invitation](./media/remoteapp-tutorial-o365anywhere/7-araclient.png)

Ce que vous voyez lorsque de nouvelles invitations sont disponibles.

![Accepter une application](./media/remoteapp-tutorial-o365anywhere/8-invitation.png)

Une fois que vous acceptez hello invitation, vous devez voir toutes les applications d’Office hello dans le client d’Azure RemoteApp hello.

![Liste des applications](./media/remoteapp-tutorial-o365anywhere/9-work.png)

Lorsque vous cliquez sur une de ces applications, hello doit commencer sur hello de machine virtuelle Azure, vous devez être définis ! Vous n’avez plus qu’à l’utiliser !

![démarrage en cours](./media/remoteapp-tutorial-o365anywhere/10-arastart.png)

![PowerPoint](./media/remoteapp-tutorial-o365anywhere/11-pp.png)

