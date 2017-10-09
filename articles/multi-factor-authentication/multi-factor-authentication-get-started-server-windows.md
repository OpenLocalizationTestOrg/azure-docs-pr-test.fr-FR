---
title: "aaaWindows l’authentification et le serveur Azure MFA | Documents Microsoft"
description: "Il s’agit de page d’authentification multifacteur Azure hello qui va vous aider à déployer l’authentification Windows et le serveur Azure multi-Factor Authentication."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 19a4043f-c4ce-43c0-80e7-2548ee92cb74
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/06/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 0fc38fd751966bf883d4eae7c48055988922af80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-authentication-and-azure-multi-factor-authentication-server"></a>Authentification Windows et serveur Azure Multi-Factor Authentication
Utiliser la section de l’authentification Windows hello de tooenable du serveur Azure multi-Factor Authentication hello et configurer l’authentification Windows pour les applications. Avant de configurer l’authentification Windows, gardez hello suivant liste à l’esprit :

* Après l’installation, redémarrez hello Azure multi-Factor Authentication pour effet de tootake Services Terminal Server.
* Si « Correspondance d’utilisateur nécessitent Azure multi-Factor Authentication » est activée et que vous n’êtes pas dans la liste des utilisateurs hello, vous ne serez pas en mesure de toolog dans une machine de hello après le redémarrage.
* Adresses IP approuvées que sont dépend de si application hello fournir hello IP du client avec l’authentification de hello. Actuellement, seul Terminal Services est pris en charge.  

> [!NOTE]
> Cette fonctionnalité n’est pas pris en charge toosecure Terminal Server sur Windows Server 2012 R2.

## <a name="toosecure-an-application-with-windows-authentication-use-hello-following-procedure"></a>toosecure une application avec l’authentification Windows, hello utilisation suivant la procédure.
1. Bonjour serveur Azure multi-Factor Authentication, cliquez sur icône de l’authentification Windows hello.
   ![Authentification Windows](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)
2. Vérifiez hello **activer l’authentification Windows** case à cocher. Par défaut, cette case est désactivée.
3. onglet Applications de Hello permet hello administrateur tooconfigure une ou plusieurs applications pour l’authentification Windows.
4. Sélectionnez un serveur ou une application – permet de spécifier si le serveur ou l’application hello est activée. Cliquez sur **OK**.
5. Cliquez sur **Ajouter…**.
6. onglet adresses IP approuvées de Hello vous permet de tooskip Azure multi-Factor Authentication pour les sessions Windows provenant d’adresses IP spécifique. Par exemple, si les employés utilisent l’application hello hello bureau et à domicile, vous pouvez décider de que vous ne souhaitez pas leur téléphone sonne pour Azure multi-Factor Authentication au bureau de hello. Pour ce faire, vous spécifiez hello office sous-réseau en tant qu’adresse IP approuvée.
7. Cliquez sur **Ajouter…**.
8. Sélectionnez **adresse IP unique** si vous souhaitez que tooskip une adresse IP unique.
9. Sélectionnez **plage d’adresses IP** si vous souhaitez que tooskip une plage entière d’IP. Exemple 10.63.193.1-10.63.193.100.
10. Sélectionnez **sous-réseau** si vous souhaitez que toospecify une plage d’adresses IP à l’aide de la notation de sous-réseau. Entrez l’adresse IP de début du sous-réseau hello et choisissez hello un masque de réseau approprié à partir de la liste déroulante de hello.
11. Cliquez sur **OK**.

## <a name="next-steps"></a>Étapes suivantes

- [Configurer des appareils VPN tiers pour Azure MFA Server](multi-factor-authentication-advanced-vpn-configurations.md)

- [Améliorer votre infrastructure d’authentification existante avec hello extension du serveur NPS pour Azure MFA](multi-factor-authentication-nps-extension.md)
