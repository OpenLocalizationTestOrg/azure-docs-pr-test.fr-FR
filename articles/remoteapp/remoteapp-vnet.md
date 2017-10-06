---
title: "toouse de réseau virtuel Azure hello aaaValidate avec Azure RemoteApp | Documents Microsoft"
description: "Découvrez comment toomake que votre réseau virtuel Azure est prêt toouse avec Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b573ba02-4587-4be5-9821-27bd891a73b2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 5587556c264356e6ab6039b983a38cb2b95ed268
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="validate-hello-azure-vnet-toouse-with-azure-remoteapp"></a>Valider toouse de réseau virtuel Azure hello avec Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Avant d’utiliser un réseau virtuel Azure avec Azure RemoteApp, vous pourriez toovalidate hello réseau virtuel. Cette action permet d'éviter les problèmes de connectivité.

toovalidate votre réseau virtuel Azure, procédez comme hello suivant :

1. Créer une machine virtuelle Azure à l’intérieur du sous-réseau hello Hello réseau virtuel de Azure vous souhaitez toouse avec Azure RemoteApp.
2. Se connecter toothat machine virtuelle à l’aide de hello **Connect** option hello portail de gestion.
3. Jointure toohello de machine virtuelle hello même domaine que vous souhaitez toouse avec Azure RemoteApp. Si vous créez une collection hybride qui connecte le réseau local de tooyour, joignez hello machine virtuelle tooyour dans le domaine local.

Si l’opération réussit, hello réseau virtuel Azure est prêt toouse avec RemoteApp.

Pour plus d’informations sur les flux de travail de collection hello hybride de bout en bout, consultez hello suivant des articles :

* [Comment tooplan votre réseau virtuel pour Azure RemoteApp](remoteapp-planvnet.md)
* [Création d'une collection hybride](remoteapp-create-hybrid-deployment.md)
* [Déployer Azure RemoteApp collection tooyour réseau virtuel Azure (avec prise en charge pour ExpressRoute)](http://blogs.msdn.com/b/rds/archive/2015/04/23/deploy-azure-remoteapp-collection-to-your-azure-virtual-network-with-support-for-expressroute.aspx)

