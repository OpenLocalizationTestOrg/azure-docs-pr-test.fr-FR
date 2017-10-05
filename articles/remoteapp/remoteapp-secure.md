---
title: "Sécuriser des applications et des ressources dans Azure RemoteApp | Microsoft Docs"
description: "Apprendre à verrouiller des applications et des ressources dans Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7fbade87-a453-426d-bfa5-c72227ea83cd
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 1c052906788f0f4fe4ca9fd6d3af63336245174a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="secure-apps-and-resources-in-azure-remoteapp"></a>Sécurisation des applications et des ressources dans Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Pour plus d’informations, lisez [l’annonce](https://go.microsoft.com/fwlink/?linkid=821148) .
> 
> 

Azure RemoteApp fournit aux utilisateurs un accès aux applications Windows gérées de manière centralisée, ce qui vous permet de contrôler ce que peuvent faire les utilisateurs.  Cela est particulièrement utile lorsque l'utilisateur se connecte à partir d'un appareil non géré (comme leur MacBook personnel) et que vous souhaitez contrôler l'accès ou l’expérience de l'utilisateur.

Par exemple, si vous utilisez Active Directory pour l'authentification des utilisateurs et que vous souhaitez empêcher les utilisateurs de copier des données d'une application, vous pouvez configurer une stratégie de groupe Bureau à distance pour empêcher les utilisateurs de copier des données.

Autre exemple : Si vous souhaitez bloquer l'accès à Internet pour une application particulière de votre collection. Vous pouvez créer une règle de pare-feu Windows qui bloque l'accès lorsque vous créez l'image pour votre collection.

## <a name="implementation-options"></a>Options d’implémentation
  Voici les principales options d'implémentation qui peuvent être utilisées individuellement ou en tandem en fonction des besoins :

1. Si votre collection RemoteApp est jointe au domaine, vous pouvez appliquer n’importe quelle [stratégie de groupe](https://technet.microsoft.com/library/cc725828.aspx) (à l’exception des stratégies d'expiration d’inactivité et de déconnexion décrites [ici](../azure-subscription-service-limits.md)).
2. Comme alternative à la stratégie de groupe (si votre collection n'est pas jointe au domaine ou que vous n'avez pas les autorisations appropriées dans Active Directory), vous pouvez configurer des [stratégies locales](https://technet.microsoft.com/library/cc775702.aspx) dans votre image de modèle.  Notez que ce groupe de stratégies prévaut sur les stratégies locales en cas de conflit.
3. Certains paramètres du système d'exploitation/de l’application ne sont pas configurables via la stratégie, mais peuvent l’être via la clé de registre en utilisant [l’outil RegEdit](remoteapp-hybridtrouble.md) lors de la configuration de votre image de modèle.
4. Vous pouvez utiliser le [pare-feu Windows](http://windows.microsoft.com/en-US/windows-8/Windows-Firewall-from-start-to-finish) pour contrôler l'accès réseau vers et depuis l'ordinateur sur lequel l'application est exécutée. Assurez-vous que vous ne bloquez pas les URL et les ports définis ici.
5. Vous pouvez utiliser [AppLocker](https://technet.microsoft.com/library/hh831440.aspx) pour contrôler les applications et les fichiers que les utilisateurs peuvent exécuter. Par exemple, les utilisateurs expérimentés peuvent déterminer comment exécuter les applications que vous n'avez pas publiées mais qui sont disponibles dans l'image que vous avez utilisée pour créer la collection - AppLocker peut bloquer ce processus.

## <a name="detailed-information"></a>Informations détaillées
* Les stratégies RDS suivantes seront sans doute plus utiles :
  * [Redirection d’appareils et de ressources](https://technet.microsoft.com/library/ee791794.aspx)
  * [Redirection d’imprimantes](https://technet.microsoft.com/library/ee791784.aspx)
  * [Profils](https://technet.microsoft.com/library/ee791865.aspx).
* Notez que la configuration des redirections via le module PowerShell pour RemoteApp (comme indiqué [ici](remoteapp-redirection.md)) s'appuie sur l'ordinateur client pour appliquer la stratégie. Si la sécurité est votre principal objectif, vous souhaiterez appliquer la stratégie via la stratégie locale de l’image de modèle ou via la stratégie de groupe.
* [Stratégies Windows Server 2012 R2](https://technet.microsoft.com/library/hh831791.aspx).
* [Stratégies Office 2013](https://technet.microsoft.com/library/cc178969.aspx) (y compris [la personnalisation de la barre d'outils Office](https://technet.microsoft.com/library/cc179143.aspx)).

