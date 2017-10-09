---
title: aaaCreate une image Azure RemoteApp | Documents Microsoft
description: "En savoir plus sur les options de hello disponibles pour la création d’images pour Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: cb0f9424-6185-45a1-abe9-c23f1edf34f2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 54e63b6fa13addfcda96ce581910e1ac48d91e70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-remoteapp-image"></a>Création d’une image Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Azure RemoteApp utilise des images toohold hello applications que vous partagez avec vos utilisateurs. (Nous prendre votre image et l’utiliser machines virtuelles toocreate - ce que les utilisateurs de hello accèdent quand ils se connectent à Azure RemoteApp.) toocreate une collection Azure RemoteApp avec un choix d’applications, qu’il s’agisse de cloud ou hybride, vous commencez par créer une image avec les applications installées. Ensuite, créez un regroupement qui utilise cette image, affecter des utilisateurs toohello collection et publier des utilisateurs de toothose d’applications.

Plusieurs choix s’offrent à vous pour créer ou utiliser des images. Hello base [exigence](remoteapp-imagereqs.md) pour une image est qu’il exécutent Windows Server 2012 R2 et hello hôte de Session de bureau à distance (RDSH) rôle est installé. La procédure commence à devenir intéressante au moment de choisir le mode de configuration.

Vous avez hello options suivantes lorsqu’il s’agit de tooimages :

* Vous pouvez importer et utiliser une [image basée sur une machine virtuelle Azure](remoteapp-image-on-azurevm.md). Cette fonction est utile pour les applications cœur de métier nécessitant des paramètres personnalisés. Vous pouvez personnaliser toowork d’image hello pour une application hello.
* Vous pouvez [créer et charger une image personnalisée](remoteapp-create-custom-image.md). Cette fonction est utile si vous disposez déjà d’une image que vous utilisez pour le déploiement local de vos services Bureau à distance.
* Vous pouvez utiliser une des hello [images de modèle](remoteapp-images.md) inclus dans votre abonnement RemoteApp. Ces images sont créées et gérées par l’équipe de RemoteApp hello et contiennent certaines applications standards (par exemple hello Office suite) que vous pouvez créer des utilisateurs de tooyour disponibles. Notez que cette image d’Office 365 Pro Plus hello uniquement peut être utilisée dans un environnement de production.

Quelle que soit l’où vous avez obtenu votre image ou comment vous la créez, vous souhaiterez toomake que vous comprenez hello [spécifications des applications](remoteapp-appreqs.md) tooensure votre application fonctionne correctement dans RemoteApp. Ensuite, la prochaine étape de hello est toocreate un [cloud](remoteapp-create-cloud-deployment.md) ou [hybride](remoteapp-create-hybrid-deployment.md) collection.

