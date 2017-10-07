---
title: aaaSecure aux applications et ressources dans Azure RemoteApp | Documents Microsoft
description: "Découvrez comment toolock vers le bas aux applications et ressources dans Azure RemoteApp"
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
ms.openlocfilehash: 26325826e92855a12a0087f19a3e32cbe1116449
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-apps-and-resources-in-azure-remoteapp"></a>Sécurisation des applications et des ressources dans Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Azure RemoteApp fournit aux utilisateurs accès géré par toocentrally les applications Windows, qui vous permet de contrôler ce que vos utilisateurs peuvent et ne peuvent pas faire.  Cela est particulièrement utile lors de la connexion à partir d’un appareil non géré (par exemple, leur Macbook personnel) et que vous souhaitez toocontrol hello l’accès utilisateur ou de l’expérience d’utilisateur de hello.

Par exemple, si vous utilisez Active Directory pour l’authentification utilisateur et que vous souhaitez tooprevent vos utilisateurs à partir de la copie des données en dehors d’une application, vous pouvez configurer un utilisateur tooblock de stratégie de groupe de bureau à distance à partir de la copie de données.

Autre exemple : Si vous souhaitez un accès internet tooblock pour une application particulière dans votre collection. Vous pouvez créer une règle de pare-feu Windows que les blocs hello accès lorsque vous créez l’image de hello pour votre collection.

## <a name="implementation-options"></a>Options d’implémentation
  Voici les options d’implémentation de la clé de hello, qui peuvent être utilisées individuellement ou en tandem en fonction des besoins :

1. Si votre collection RemoteApp est joint à un domaine, vous pouvez appliquer les [stratégie de groupe](https://technet.microsoft.com/library/cc725828.aspx) (avec l’exception hello hello en attente et déconnexion du délai d’attente des stratégies de décrites [ici](../azure-subscription-service-limits.md)).
2. Un tooGroup autre stratégie (si votre collection n’est pas joint à un domaine ou vous n’avez pas les autorisations appropriées hello dans Active Directory), vous pouvez configurer [stratégies locales](https://technet.microsoft.com/library/cc775702.aspx) dans votre image de modèle.  Notez que ce groupe de stratégies prévaut sur les stratégies locales en cas de conflit.
3. Certains paramètres du système d’exploitation/application ne sont pas configurables via la stratégie, mais peut être via la clé de Registre à l’aide de hello [outil RegEdit](remoteapp-hybridtrouble.md) lors de la configuration de votre image de modèle.
4. Vous pouvez utiliser [pare-feu Windows](http://windows.microsoft.com/en-US/windows-8/Windows-Firewall-from-start-to-finish) toocontrol tooand de l’accès réseau à partir de l’ordinateur hello où l’application hello est en cours d’exécution. Assurez-vous que vous ne bloquez pas hello URL et ports définis ici.
5. Vous pouvez utiliser [AppLocker](https://technet.microsoft.com/library/hh831440.aspx) toocontrol les applications et les fichiers des utilisateurs peuvent exécuter. Par exemple, les utilisateurs expérimentés peuvent déterminer comment l’image vous avez utilisé toocreate hello collection toorun applications que vous n’avez pas publié mais qui sont disponibles dans hello - AppLocker peut bloquer ce.

## <a name="detailed-information"></a>Informations détaillées
* Hello suivant des stratégies des services Bureau à distance est probablement toobe plus utiles :
  * [Redirection d’appareils et de ressources](https://technet.microsoft.com/library/ee791794.aspx)
  * [Redirection d’imprimantes](https://technet.microsoft.com/library/ee791784.aspx)
  * [Profils](https://technet.microsoft.com/library/ee791865.aspx).
* Notez que la configuration de redirections via hello RemoteApp PowerShell module (comme [ici](remoteapp-redirection.md)) s’appuie sur hello machine tooenforce hello la stratégie client, donc si la sécurité est l’objectif principal de hello vous allez stratégie de hello tooenforce via Hello stratégie locale d’image de modèle ou via la stratégie de groupe.
* [Stratégies Windows Server 2012 R2](https://technet.microsoft.com/library/hh831791.aspx).
* [Les stratégies d’Office 2013](https://technet.microsoft.com/library/cc178969.aspx) (y compris [comment toocustomize hello barre d’outils Office](https://technet.microsoft.com/library/cc179143.aspx)).

