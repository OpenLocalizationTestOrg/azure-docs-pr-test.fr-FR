---
title: "aaaConfigure un nom de domaine personnalisé pour une application web dans Azure App Service qui utilise le Traffic Manager pour l’équilibrage de charge."
description: "Utilisation d’un nom de domaine personnalisé pour une application web dans Azure App Service intégrant Traffic Manager pour équilibrer la charge."
services: app-service\web
documentationcenter: 
author: cephalin
manager: cfowler
editor: 
ms.assetid: 0f96c0e7-0901-489b-a95a-e3b66ca0a1c2
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: cephalin
ms.openlocfilehash: dfde5fc6b445b30b10e03dcb03e8d072130d9377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-custom-domain-name-for-a-web-app-in-azure-app-service-using-traffic-manager"></a>Configuration d’un nom de domaine personnalisé pour une application web dans Azure App Service utilisant Traffic Manager
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro-traffic-manager.md)]

Cet article contient des instructions génériques sur l’utilisation d’un nom de domaine personnalisé avec Azure App Service utilisant Traffic Manager pour équilibrer la charge.

[!INCLUDE [tmwebsitefooter](../../includes/custom-dns-web-site-traffic-manager-notes.md)]

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a>Présentation des enregistrements DNS
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-traffic-manager.md)]

<a name="bkmk_configsharedmode"></a>

## <a name="configure-your-web-apps-for-standard-mode"></a>Configuration de vos applications web en mode Standard
[!INCLUDE [modes](../../includes/custom-dns-web-site-modes-traffic-manager.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a>Ajout d'un enregistrement DNS pour votre domaine personnalisé
> [!NOTE]
> Si vous avez acheté domaine via Azure App Service Web Apps ignorer comme suit et reportez-vous toohello dernière étape de [acheter un domaine pour les applications Web](custom-dns-web-site-buydomains-web-app.md) l’article.
> 
> 

tooassociate votre domaine personnalisé avec une application web dans Azure App Service, vous devez ajouter une nouvelle entrée dans la table de hello DNS pour votre domaine personnalisé à l’aide des outils fournis par hello de domaines que vous avez acheté votre nom de domaine à partir de. Utilisez hello suivant toolocate d’étapes et les outils du DNS hello.

1. Connectez-vous au compte tooyour votre bureau d’enregistrement de domaine et recherchez une page de gestion des enregistrements DNS. Recherchez des liens ou les zones du site de hello étiquetés comme étant **nom de domaine**, **DNS**, ou **gestion des noms de serveur**. Souvent un lien toothis page se trouve être affichage des informations de votre compte, puis en consultant un lien comme **mes domaines**.
2. Une fois que vous avez trouvé la page de gestion hello pour votre nom de domaine, recherchez un lien qui vous permet des enregistrements DNS tooedit hello. Il est probablement répertorié en tant que lien de configuration de **fichier de zone**, d’**enregistrements DNS** ou **avancé**.
   
   * page de Hello possèdent généralement des enregistrements déjà créés, par exemple, l’association d’une entrée '**@**'ou'\*' avec une page 'stationnement domaine'. Cette page peut également contenir des enregistrements pour des sous-domaines courants, tels que **www**.
   * page de Hello fera mention **enregistrements CNAME**, ou fournissez une liste déroulante tooselect un type d’enregistrement. Elle peut également mentionner d’autres enregistrements, tels que des **enregistrements A** et des **enregistrements MX**. Dans certains cas, les enregistrements CNAME sont appelés différemment, par exemple **Enregistrement d'alias**.
   * page de Hello aura également des champs qui vous permettent de trop**carte** d’un **nom d’hôte** ou **nom de domaine** nom de domaine tooanother.
3. Bien que les spécificités de hello de chaque bureau d’enregistrement de varient, en général vous mappez *de* votre nom de domaine personnalisé (tel que **contoso.com**,) *à* nom de domaine Traffic Manager hello (**contoso.trafficmanager.net**) qui est utilisé pour votre application web.
   
   > [!NOTE]
   > Vous pouvez également, si un enregistrement est déjà en cours d’utilisation et que vous devez toopreemptively lier votre tooit d’applications, vous pouvez créer un enregistrement CNAME supplémentaire. Par exemple, les lier toopreemptively **www.contoso.com** tooyour l’application web, créez un enregistrement CNAME à partir de **awverify.www** trop**contoso.trafficmanager.net**. Vous pouvez ensuite ajouter « www.contoso.com » tooyour application Web sans modifier l’enregistrement CNAME de « www » hello. Pour plus d’informations, consultez [Créer des enregistrements DNS pour une application web dans un domaine personnalisé][CREATEDNS].
   > 
   > 
4. Une fois que vous avez terminé d’ajouter ou modifier des enregistrements DNS auprès de votre bureau d’enregistrement, enregistrer les modifications de hello.

<a name="enabledomain"></a>

## <a name="enable-traffic-manager"></a>Activation de Traffic Manager
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-traffic-manager.md)]

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations, consultez hello [centre de développement Node.js](/develop/nodejs/).

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[CREATEDNS]: ../dns/dns-web-sites-custom-domain.md
