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
# <a name="configuring-a-custom-domain-name-for-a-web-app-in-azure-app-service-using-traffic-manager"></a><span data-ttu-id="b1cc4-103">Configuration d’un nom de domaine personnalisé pour une application web dans Azure App Service utilisant Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="b1cc4-103">Configuring a custom domain name for a web app in Azure App Service using Traffic Manager</span></span>
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro-traffic-manager.md)]

<span data-ttu-id="b1cc4-104">Cet article contient des instructions génériques sur l’utilisation d’un nom de domaine personnalisé avec Azure App Service utilisant Traffic Manager pour équilibrer la charge.</span><span class="sxs-lookup"><span data-stu-id="b1cc4-104">This article provides generic instructions for using a custom domain name with Azure App Service that use Traffic Manager for load balancing.</span></span>

[!INCLUDE [tmwebsitefooter](../../includes/custom-dns-web-site-traffic-manager-notes.md)]

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a><span data-ttu-id="b1cc4-105">Présentation des enregistrements DNS</span><span class="sxs-lookup"><span data-stu-id="b1cc4-105">Understanding DNS records</span></span>
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-traffic-manager.md)]

<a name="bkmk_configsharedmode"></a>

## <a name="configure-your-web-apps-for-standard-mode"></a><span data-ttu-id="b1cc4-106">Configuration de vos applications web en mode Standard</span><span class="sxs-lookup"><span data-stu-id="b1cc4-106">Configure your web apps for standard mode</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-modes-traffic-manager.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a><span data-ttu-id="b1cc4-107">Ajout d'un enregistrement DNS pour votre domaine personnalisé</span><span class="sxs-lookup"><span data-stu-id="b1cc4-107">Add a DNS record for your custom domain</span></span>
> [!NOTE]
> <span data-ttu-id="b1cc4-108">Si vous avez acheté domaine via Azure App Service Web Apps ignorer comme suit et reportez-vous toohello dernière étape de [acheter un domaine pour les applications Web](custom-dns-web-site-buydomains-web-app.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="b1cc4-108">If you have purchased domain through Azure App Service Web Apps then skip following steps and refer toohello final step of [Buy Domain for Web Apps](custom-dns-web-site-buydomains-web-app.md) article.</span></span>
> 
> 

<span data-ttu-id="b1cc4-109">tooassociate votre domaine personnalisé avec une application web dans Azure App Service, vous devez ajouter une nouvelle entrée dans la table de hello DNS pour votre domaine personnalisé à l’aide des outils fournis par hello de domaines que vous avez acheté votre nom de domaine à partir de.</span><span class="sxs-lookup"><span data-stu-id="b1cc4-109">tooassociate your custom domain with a web app in Azure App Service, you must add a new entry in hello DNS table for your custom domain by using tools provided by hello domain registrar that you purchased your domain name from.</span></span> <span data-ttu-id="b1cc4-110">Utilisez hello suivant toolocate d’étapes et les outils du DNS hello.</span><span class="sxs-lookup"><span data-stu-id="b1cc4-110">Use hello following steps toolocate and use hello DNS tools.</span></span>

1. <span data-ttu-id="b1cc4-111">Connectez-vous au compte tooyour votre bureau d’enregistrement de domaine et recherchez une page de gestion des enregistrements DNS.</span><span class="sxs-lookup"><span data-stu-id="b1cc4-111">Sign in tooyour account at your domain registrar, and look for a page for managing DNS records.</span></span> <span data-ttu-id="b1cc4-112">Recherchez des liens ou les zones du site de hello étiquetés comme étant **nom de domaine**, **DNS**, ou **gestion des noms de serveur**.</span><span class="sxs-lookup"><span data-stu-id="b1cc4-112">Look for links or areas of hello site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span> <span data-ttu-id="b1cc4-113">Souvent un lien toothis page se trouve être affichage des informations de votre compte, puis en consultant un lien comme **mes domaines**.</span><span class="sxs-lookup"><span data-stu-id="b1cc4-113">Often a link toothis page can be found be viewing your account information, and then looking for a link such as **My domains**.</span></span>
2. <span data-ttu-id="b1cc4-114">Une fois que vous avez trouvé la page de gestion hello pour votre nom de domaine, recherchez un lien qui vous permet des enregistrements DNS tooedit hello.</span><span class="sxs-lookup"><span data-stu-id="b1cc4-114">Once you have found hello management page for your domain name, look for a link that allows you tooedit hello DNS records.</span></span> <span data-ttu-id="b1cc4-115">Il est probablement répertorié en tant que lien de configuration de **fichier de zone**, d’**enregistrements DNS** ou **avancé**.</span><span class="sxs-lookup"><span data-stu-id="b1cc4-115">This might be listed as a **Zone file**, **DNS Records**, or as an **Advanced** configuration link.</span></span>
   
   * <span data-ttu-id="b1cc4-116">page de Hello possèdent généralement des enregistrements déjà créés, par exemple, l’association d’une entrée '**@**'ou'\*' avec une page 'stationnement domaine'.</span><span class="sxs-lookup"><span data-stu-id="b1cc4-116">hello page will most likely have a few records already created, such as an entry associating '**@**' or '\*' with a 'domain parking' page.</span></span> <span data-ttu-id="b1cc4-117">Cette page peut également contenir des enregistrements pour des sous-domaines courants, tels que **www**.</span><span class="sxs-lookup"><span data-stu-id="b1cc4-117">It may also contain records for common sub-domains such as **www**.</span></span>
   * <span data-ttu-id="b1cc4-118">page de Hello fera mention **enregistrements CNAME**, ou fournissez une liste déroulante tooselect un type d’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="b1cc4-118">hello page will mention **CNAME records**, or provide a drop-down tooselect a record type.</span></span> <span data-ttu-id="b1cc4-119">Elle peut également mentionner d’autres enregistrements, tels que des **enregistrements A** et des **enregistrements MX**.</span><span class="sxs-lookup"><span data-stu-id="b1cc4-119">It may also mention other records such as **A records** and **MX records**.</span></span> <span data-ttu-id="b1cc4-120">Dans certains cas, les enregistrements CNAME sont appelés différemment, par exemple **Enregistrement d'alias**.</span><span class="sxs-lookup"><span data-stu-id="b1cc4-120">In some cases, CNAME records will be called by other names such as an **Alias Record**.</span></span>
   * <span data-ttu-id="b1cc4-121">page de Hello aura également des champs qui vous permettent de trop**carte** d’un **nom d’hôte** ou **nom de domaine** nom de domaine tooanother.</span><span class="sxs-lookup"><span data-stu-id="b1cc4-121">hello page will also have fields that allow you too**map** from a **Host name** or **Domain name** tooanother domain name.</span></span>
3. <span data-ttu-id="b1cc4-122">Bien que les spécificités de hello de chaque bureau d’enregistrement de varient, en général vous mappez *de* votre nom de domaine personnalisé (tel que **contoso.com**,) *à* nom de domaine Traffic Manager hello (**contoso.trafficmanager.net**) qui est utilisé pour votre application web.</span><span class="sxs-lookup"><span data-stu-id="b1cc4-122">While hello specifics of each registrar vary, in general you map *from* your custom domain name (such as **contoso.com**,) *to* hello Traffic Manager domain name (**contoso.trafficmanager.net**) that is used for your web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b1cc4-123">Vous pouvez également, si un enregistrement est déjà en cours d’utilisation et que vous devez toopreemptively lier votre tooit d’applications, vous pouvez créer un enregistrement CNAME supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="b1cc4-123">Alternatively, if a record is already in use and you need toopreemptively bind your apps tooit, you can create an additional CNAME record.</span></span> <span data-ttu-id="b1cc4-124">Par exemple, les lier toopreemptively **www.contoso.com** tooyour l’application web, créez un enregistrement CNAME à partir de **awverify.www** trop**contoso.trafficmanager.net**.</span><span class="sxs-lookup"><span data-stu-id="b1cc4-124">For example, toopreemptively bind **www.contoso.com** tooyour web app, create a CNAME record from **awverify.www** too**contoso.trafficmanager.net**.</span></span> <span data-ttu-id="b1cc4-125">Vous pouvez ensuite ajouter « www.contoso.com » tooyour application Web sans modifier l’enregistrement CNAME de « www » hello.</span><span class="sxs-lookup"><span data-stu-id="b1cc4-125">You can then add "www.contoso.com" tooyour Web App without changing hello "www" CNAME record.</span></span> <span data-ttu-id="b1cc4-126">Pour plus d’informations, consultez [Créer des enregistrements DNS pour une application web dans un domaine personnalisé][CREATEDNS].</span><span class="sxs-lookup"><span data-stu-id="b1cc4-126">For more information, see [Create DNS records for a web app in a custom domain][CREATEDNS].</span></span>
   > 
   > 
4. <span data-ttu-id="b1cc4-127">Une fois que vous avez terminé d’ajouter ou modifier des enregistrements DNS auprès de votre bureau d’enregistrement, enregistrer les modifications de hello.</span><span class="sxs-lookup"><span data-stu-id="b1cc4-127">Once you have finished adding or modifying DNS records at your registrar, save hello changes.</span></span>

<a name="enabledomain"></a>

## <a name="enable-traffic-manager"></a><span data-ttu-id="b1cc4-128">Activation de Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="b1cc4-128">Enable Traffic Manager</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-traffic-manager.md)]

## <a name="next-steps"></a><span data-ttu-id="b1cc4-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b1cc4-129">Next steps</span></span>
<span data-ttu-id="b1cc4-130">Pour plus d’informations, consultez hello [centre de développement Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="b1cc4-130">For more information, see hello [Node.js Developer Center](/develop/nodejs/).</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[CREATEDNS]: ../dns/dns-web-sites-custom-domain.md
