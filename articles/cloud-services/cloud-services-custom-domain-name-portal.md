---
title: "Configuration d’un nom de domaine personnalisé dans Services cloud | Microsoft Docs"
description: "Découvrez comment exposer votre application ou vos données Azure sur Internet, sur un domaine personnalisé, en configurant les paramètres DNS.  Ces exemples utilisent le portail Azure."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 5783a246-a151-4fb1-b488-441bfb29ee44
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: cf43d86dddc3a68573e1ba1b09118c54f0b16bc5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="configuring-a-custom-domain-name-for-an-azure-cloud-service"></a><span data-ttu-id="70923-104">Configuration d’un nom de domaine personnalisé pour un service cloud Azure</span><span class="sxs-lookup"><span data-stu-id="70923-104">Configuring a custom domain name for an Azure cloud service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="70923-105">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="70923-105">Azure portal</span></span>](cloud-services-custom-domain-name-portal.md)
> * [<span data-ttu-id="70923-106">Portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="70923-106">Azure classic portal</span></span>](cloud-services-custom-domain-name.md)
> 
> 

<span data-ttu-id="70923-107">Lorsque vous créez un service cloud, Azure l'attribue à un sous-domaine de **cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="70923-107">When you create a Cloud Service, Azure assigns it to a subdomain of **cloudapp.net**.</span></span> <span data-ttu-id="70923-108">Par exemple, si votre service cloud s’intitule « contoso », vos utilisateurs peuvent accéder à votre application par le biais d’une URL telle que http://contoso.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="70923-108">For example, if your Cloud Service is named "contoso", your users will be able to access your application on a URL like http://contoso.cloudapp.net.</span></span> <span data-ttu-id="70923-109">Azure attribue également une adresse IP virtuelle.</span><span class="sxs-lookup"><span data-stu-id="70923-109">Azure also assigns a virtual IP address.</span></span>

<span data-ttu-id="70923-110">Toutefois, vous pouvez également exposer votre application sur votre propre nom de domaine, par exemple, **contoso.com**. Cet article explique comment réserver ou configurer un domaine personnalisé avec des rôles Web de service cloud.</span><span class="sxs-lookup"><span data-stu-id="70923-110">However, you can also expose your application on your own domain name, such as **contoso.com**. This article explains how to reserve or configure a custom domain name for Cloud Service web roles.</span></span>

<span data-ttu-id="70923-111">Vous avez compris ce que sont les enregistrements CNAME et A ?</span><span class="sxs-lookup"><span data-stu-id="70923-111">Do you already understand what CNAME and A records are?</span></span> <span data-ttu-id="70923-112">[Passez l’explication](#add-a-cname-record-for-your-custom-domain).</span><span class="sxs-lookup"><span data-stu-id="70923-112">[Jump past the explanation](#add-a-cname-record-for-your-custom-domain).</span></span>

> [!NOTE]
> <span data-ttu-id="70923-113">Les procédures décrites dans cette tâche s’appliquent aux services cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="70923-113">The procedures in this task apply to Azure Cloud Services.</span></span> <span data-ttu-id="70923-114">Pour App Services, consultez [cette page](../app-service-web/web-sites-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="70923-114">For App Services, see [this](../app-service-web/web-sites-custom-domain-name.md).</span></span> <span data-ttu-id="70923-115">Pour les comptes de stockage, consultez [cette page](../storage/blobs/storage-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="70923-115">For storage accounts, see [this](../storage/blobs/storage-custom-domain-name.md).</span></span>
> 
> 

<p/>

> [!TIP]
> <span data-ttu-id="70923-116">Soyez opérationnel plus rapidement. Utilisez la nouvelle [procédure pas à pas d’Azure](http://support.microsoft.com/kb/2990804).</span><span class="sxs-lookup"><span data-stu-id="70923-116">Get going faster--use the NEW Azure [guided walkthrough](http://support.microsoft.com/kb/2990804)!</span></span>  <span data-ttu-id="70923-117">Grâce à elle, l'association d'un nom de domaine personnalisé ET la sécurisation de la communication (SSL) avec les services cloud Azure ou les sites Web Azure deviennent un jeu d'enfants.</span><span class="sxs-lookup"><span data-stu-id="70923-117">It makes associating a custom domain name AND securing communication (SSL) with Azure Cloud Services or Azure Websites a snap.</span></span>
> 
> 

## <a name="understand-cname-and-a-records"></a><span data-ttu-id="70923-118">Présentation des enregistrements CNAME et A</span><span class="sxs-lookup"><span data-stu-id="70923-118">Understand CNAME and A records</span></span>
<span data-ttu-id="70923-119">Bien que fonctionnant différemment, les enregistrements CNAME (ou enregistrements d’alias) et A permettent d’associer un nom de domaine avec un serveur spécifique (ou un service dans ce cas).</span><span class="sxs-lookup"><span data-stu-id="70923-119">CNAME (or alias records) and A records both allow you to associate a domain name with a specific server (or service in this case,) however they work differently.</span></span> <span data-ttu-id="70923-120">Avant de faire votre choix, certains aspects spécifiques sont également à prendre en considération lors de l’utilisation d’enregistrements A avec les services cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="70923-120">There are also some specific considerations when using A records with Azure Cloud services that you should consider before deciding which to use.</span></span>

### <a name="cname-or-alias-record"></a><span data-ttu-id="70923-121">Enregistrement CNAME ou d'alias</span><span class="sxs-lookup"><span data-stu-id="70923-121">CNAME or Alias record</span></span>
<span data-ttu-id="70923-122">Un enregistrement CNAME associe un domaine *spécifique*, tel que **contoso.com** ou **www.contoso.com**, à un nom de domaine canonique.</span><span class="sxs-lookup"><span data-stu-id="70923-122">A CNAME record maps a *specific* domain, such as **contoso.com** or **www.contoso.com**, to a canonical domain name.</span></span> <span data-ttu-id="70923-123">Dans ce cas, le nom de domaine canonique est le nom de domaine **[myapp].cloudapp.net** de votre application hébergée Azure.</span><span class="sxs-lookup"><span data-stu-id="70923-123">In this case, the canonical domain name is the **[myapp].cloudapp.net** domain name of your Azure hosted application.</span></span> <span data-ttu-id="70923-124">Une fois créé, l’enregistrement CNAME émet un alias pour **[myapp].cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="70923-124">Once created, the CNAME creates an alias for the **[myapp].cloudapp.net**.</span></span> <span data-ttu-id="70923-125">L’entrée CNAME devient automatiquement l’adresse IP de votre service **[myapp].cloudapp.net**. Ainsi, même si l’adresse IP du service cloud change, vous n’avez aucune action à effectuer.</span><span class="sxs-lookup"><span data-stu-id="70923-125">The CNAME entry will resolve to the IP address of your **[myapp].cloudapp.net** service automatically, so if the IP address of the cloud service changes, you do not have to take any action.</span></span>

> [!NOTE]
> <span data-ttu-id="70923-126">Certains bureaux d’enregistrement de domaines autorisent le mappage de sous-domaines uniquement lorsqu’un enregistrement CNAME est utilisé (par exemple, www.contoso.com) et non un nom racine (tel que contoso.com). Pour plus d'informations sur les enregistrements CNAME, consultez la documentation fournie par votre bureau d'enregistrement, la [page Wikipédia sur l'enregistrement CNAME](http://en.wikipedia.org/wiki/CNAME_record) ou le document [Noms de domaine IETF - Implémentation et spécification](http://tools.ietf.org/html/rfc1035).</span><span class="sxs-lookup"><span data-stu-id="70923-126">Some domain registrars only allow you to map subdomains when using a CNAME record, such as www.contoso.com, and not root names, such as contoso.com. For more information on CNAME records, see the documentation provided by your registrar, [the Wikipedia entry on CNAME record](http://en.wikipedia.org/wiki/CNAME_record), or the [IETF Domain Names - Implementation and Specification](http://tools.ietf.org/html/rfc1035) document.</span></span>
> 
> 

### <a name="a-record"></a><span data-ttu-id="70923-127">Enregistrement A</span><span class="sxs-lookup"><span data-stu-id="70923-127">A record</span></span>
<span data-ttu-id="70923-128">Un enregistrement *A* mappe un domaine, tel que **contoso.com** ou **www.contoso.com**, *ou un nom de domaine générique* comme **\*.contoso.com**, sur une adresse IP.</span><span class="sxs-lookup"><span data-stu-id="70923-128">An *A* record maps a domain, such as **contoso.com** or **www.contoso.com**, *or a wildcard domain* such as **\*.contoso.com**, to an IP address.</span></span> <span data-ttu-id="70923-129">Dans le cas d’un service cloud Azure, il s’agit de l’adresse IP virtuelle du service.</span><span class="sxs-lookup"><span data-stu-id="70923-129">In the case of an Azure Cloud Service, the virtual IP of the service.</span></span> <span data-ttu-id="70923-130">Le principal avantage d’un enregistrement A par rapport à un enregistrement CNAME est que vous pouvez disposer d’une entrée utilisant un caractère générique (par exemple, \***.contoso.com**), ce qui permet de gérer les demandes pour plusieurs sous-domaines, tels que **mail.contoso.com**, **login.contoso.com** ou **www.contso.com**.</span><span class="sxs-lookup"><span data-stu-id="70923-130">So the main benefit of an A record over a CNAME record is that you can have one entry that uses a wildcard, such as \***.contoso.com**, which would handle requests for multiple sub-domains such as **mail.contoso.com**, **login.contoso.com**, or **www.contso.com**.</span></span>

> [!NOTE]
> <span data-ttu-id="70923-131">L’enregistrement A étant associé à une adresse IP statique, les changements d’adresse IP de votre service cloud ne sont donc pas pris en compte automatiquement.</span><span class="sxs-lookup"><span data-stu-id="70923-131">Since an A record is mapped to a static IP address, it cannot automatically resolve changes to the IP address of your Cloud Service.</span></span> <span data-ttu-id="70923-132">L’adresse IP utilisée par votre service cloud est allouée la première fois que vous effectuez un déploiement vers un emplacement vide (de production ou intermédiaire). Si vous supprimez le déploiement de l’emplacement, l’adresse IP est publiée par Azure et tout déploiement futur dans l’emplacement peut recevoir une nouvelle adresse IP.</span><span class="sxs-lookup"><span data-stu-id="70923-132">The IP address used by your Cloud Service is allocated the first time you deploy to an empty slot (either production or staging.) If you delete the deployment for the slot, the IP address is released by Azure and any future deployments to the slot may be given a new IP address.</span></span>
> 
> <span data-ttu-id="70923-133">De façon assez pratique, l’adresse IP d’un emplacement de déploiement donné (de production ou intermédiaire) est conservée lors du basculement entre les déploiements intermédiaires et de production ou lors de l’exécution de la mise à niveau sur place d’un déploiement existant.</span><span class="sxs-lookup"><span data-stu-id="70923-133">Conveniently, the IP address of a given deployment slot (production or staging) is persisted when swapping between staging and production deployments or performing an in-place upgrade of an existing deployment.</span></span> <span data-ttu-id="70923-134">Pour plus d’informations sur ces actions, consultez la rubrique [Gestion des services cloud](cloud-services-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="70923-134">For more information on performing these actions, see [How to manage cloud services](cloud-services-how-to-manage.md).</span></span>
> 
> 

## <a name="add-a-cname-record-for-your-custom-domain"></a><span data-ttu-id="70923-135">Ajout d’un enregistrement CNAME pour votre domaine personnalisé</span><span class="sxs-lookup"><span data-stu-id="70923-135">Add a CNAME record for your custom domain</span></span>
<span data-ttu-id="70923-136">Pour créer un enregistrement CNAME, vous devez ajouter une nouvelle entrée dans la table DNS de votre domaine personnalisé en utilisant les outils fournis par votre bureau d’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="70923-136">To create a CNAME record, you must add a new entry in the DNS table for your custom domain by using the tools provided by your registrar.</span></span> <span data-ttu-id="70923-137">Chaque bureau d’enregistrement possède sa propre méthode de spécification des enregistrements CNAME, même si le fonctionnement général reste souvent similaire.</span><span class="sxs-lookup"><span data-stu-id="70923-137">Each registrar has a similar but slightly different method of specifying a CNAME record, but the concepts are the same.</span></span>

1. <span data-ttu-id="70923-138">Employez une des méthodes suivantes pour connaître le nom de domaine **.cloudapp.net** attribué à votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="70923-138">Use one of these methods to find the **.cloudapp.net** domain name assigned to your cloud service.</span></span>
   
   * <span data-ttu-id="70923-139">Connectez-vous au [portail Azure], sélectionnez votre service cloud, examinez la section **Essentials**, puis recherchez l’entrée **URL du site**.</span><span class="sxs-lookup"><span data-stu-id="70923-139">Login to the [Azure portal], select your cloud service, look at the **Essentials** section and then find the **Site URL** entry.</span></span>
     
       ![section aperçu rapide indiquant l’URL du site][csurl]
     
       <span data-ttu-id="70923-141">**OR**</span><span class="sxs-lookup"><span data-stu-id="70923-141">**OR**</span></span>
   * <span data-ttu-id="70923-142">Installez et configurez [Azure Powershell](/powershell/azure/overview), puis utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="70923-142">Install and configure [Azure Powershell](/powershell/azure/overview), and then use the following command:</span></span>
     
       ```powershell
       Get-AzureDeployment -ServiceName yourservicename | Select Url
       ```
     
     <span data-ttu-id="70923-143">Enregistrez le nom de domaine utilisé dans l’URL renvoyée par l’une des méthodes, car vous en aurez besoin lors de la création d’un enregistrement CNAME.</span><span class="sxs-lookup"><span data-stu-id="70923-143">Save the domain name used in the URL returned by either method, as you will need it when creating a CNAME record.</span></span>
2. <span data-ttu-id="70923-144">Connectez-vous au site web du bureau d’enregistrement de votre DNS et accédez à la page de gestion DNS.</span><span class="sxs-lookup"><span data-stu-id="70923-144">Log on to your DNS registrar's website and go to the page for managing DNS.</span></span> <span data-ttu-id="70923-145">Recherchez la mention **Nom de domaine**, **DNS** ou **Gestion du nom de serveur**.</span><span class="sxs-lookup"><span data-stu-id="70923-145">Look for links or areas of the site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="70923-146">Maintenant, cherchez où vous pouvez sélectionner ou saisir vos enregistrements CNAME.</span><span class="sxs-lookup"><span data-stu-id="70923-146">Now find where you can select or enter CNAME's.</span></span> <span data-ttu-id="70923-147">Il se peut que vous deviez sélectionner le type d’enregistrement dans une liste déroulante ou accéder à une page de paramètres avancés.</span><span class="sxs-lookup"><span data-stu-id="70923-147">You may have to select the record type from a drop down, or go to an advanced settings page.</span></span> <span data-ttu-id="70923-148">La section recherchée doit normalement comporter les mots **CNAME**, **Alias** ou **Sous-domaines**.</span><span class="sxs-lookup"><span data-stu-id="70923-148">You should look for the words **CNAME**, **Alias**, or **Subdomains**.</span></span>
4. <span data-ttu-id="70923-149">Vous devez également fournir l’alias de domaine ou de sous-domaine pour l’enregistrement CNAME, tel que **www** si vous voulez créer un alias pour **www.domainepersonnalisé.com**. Si vous voulez créer un alias pour le domaine racine, l’entrée correspondante devrait être répertoriée avec le symbole «**@**» dans les outils DNS de votre bureau d’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="70923-149">You must also provide the domain or subdomain alias for the CNAME, such as **www** if you want to create an alias for **www.customdomain.com**. If you want to create an alias for the root domain, it may be listed as the '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="70923-150">Vous devez ensuite fournir un nom d’hôte canonique, qui correspond au domaine **cloudapp.net** de votre application dans le cas présent.</span><span class="sxs-lookup"><span data-stu-id="70923-150">Then, you must provide a canonical host name, which is your application's **cloudapp.net** domain in this case.</span></span>

<span data-ttu-id="70923-151">Par exemple, l’enregistrement CNAME suivant renvoie tout le trafic de **www.contoso.com** vers **contoso.cloudapp.net**, le nom de domaine personnalisé de votre application déployée :</span><span class="sxs-lookup"><span data-stu-id="70923-151">For example, the following CNAME record forwards all traffic from **www.contoso.com** to **contoso.cloudapp.net**, the custom domain name of your deployed application:</span></span>

| <span data-ttu-id="70923-152">Alias/Nom d'hôte/Sous-domaine</span><span class="sxs-lookup"><span data-stu-id="70923-152">Alias/Host name/Subdomain</span></span> | <span data-ttu-id="70923-153">Domaine canonique</span><span class="sxs-lookup"><span data-stu-id="70923-153">Canonical domain</span></span> |
| --- | --- |
| <span data-ttu-id="70923-154">www</span><span class="sxs-lookup"><span data-stu-id="70923-154">www</span></span> |<span data-ttu-id="70923-155">contoso.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="70923-155">contoso.cloudapp.net</span></span> |

> [!NOTE]
> <span data-ttu-id="70923-156">Un utilisateur consultant le site **www.contoso.com** ne verra jamais l’adresse de l’hôte réel (contoso.cloudapp.net). Le processus de transfert est donc invisible pour l’utilisateur final.</span><span class="sxs-lookup"><span data-stu-id="70923-156">A visitor of **www.contoso.com** will never see the true host (contoso.cloudapp.net), so the forwarding process is invisible to the end user.</span></span>
> 
> <span data-ttu-id="70923-157">L'exemple ci-dessus s'applique uniquement au trafic du sous-domaine **www**.</span><span class="sxs-lookup"><span data-stu-id="70923-157">The example above only applies to traffic at the **www** subdomain.</span></span> <span data-ttu-id="70923-158">Puisqu'il n'est pas possible d'utiliser des caractères génériques pour les enregistrements CNAME, vous devez créer un enregistrement CNAME pour chaque domaine/sous-domaine.</span><span class="sxs-lookup"><span data-stu-id="70923-158">Since you cannot use wildcards with CNAME records, you must create one CNAME for each domain/subdomain.</span></span> <span data-ttu-id="70923-159">Pour rediriger le trafic de sous-domaines tels que *.contoso.com vers votre adresse cloudapp.net, vous pouvez configurer une entrée de **redirection d’URL** ou de **transfert d’URL** dans vos paramètres DNS. Vous pouvez également créer un enregistrement A.</span><span class="sxs-lookup"><span data-stu-id="70923-159">If you want to direct  traffic from subdomains, such as *.contoso.com, to your cloudapp.net address, you can configure a **URL Redirect** or **URL Forward** entry in your DNS settings, or create an A record.</span></span>
> 
> 

## <a name="add-an-a-record-for-your-custom-domain"></a><span data-ttu-id="70923-160">Ajouter un enregistrement A pour votre domaine personnalisé</span><span class="sxs-lookup"><span data-stu-id="70923-160">Add an A record for your custom domain</span></span>
<span data-ttu-id="70923-161">Pour créer un enregistrement A, vous devez tout d’abord connaître l’adresse IP virtuelle de votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="70923-161">To create an A record, you must first find the virtual IP address of your cloud service.</span></span> <span data-ttu-id="70923-162">Ajoutez ensuite une entrée dans la table DNS de votre domaine personnalisé à l’aide des outils fournis par votre bureau d’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="70923-162">Then add a new entry in the DNS table for your custom domain by using the tools provided by your registrar.</span></span> <span data-ttu-id="70923-163">Chaque bureau d'enregistrement possède sa propre méthode de spécification des enregistrements A, même si le fonctionnement général reste souvent similaire.</span><span class="sxs-lookup"><span data-stu-id="70923-163">Each registrar has a similar but slightly different method of specifying an A record, but the concepts are the same.</span></span>

1. <span data-ttu-id="70923-164">Utilisez l’une des méthodes suivantes pour obtenir l’adresse IP de votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="70923-164">Use one of the following methods to get the IP address of your cloud service.</span></span>
   
   * <span data-ttu-id="70923-165">Connectez-vous au [portail Azure], sélectionnez votre service cloud, examinez la section **Essentials**, puis recherchez l’entrée **Adresses IP publiques**.</span><span class="sxs-lookup"><span data-stu-id="70923-165">Login to the [Azure portal], select your cloud service, look at the **Essentials** section and then find the **Public IP addresses** entry.</span></span>
     
       ![section aperçu rapide illustrant l’adresse IP virtuelle publique][vip]
     
       <span data-ttu-id="70923-167">**OR**</span><span class="sxs-lookup"><span data-stu-id="70923-167">**OR**</span></span>
   * <span data-ttu-id="70923-168">Installez et configurez [Azure Powershell](/powershell/azure/overview), puis utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="70923-168">Install and configure [Azure Powershell](/powershell/azure/overview), and then use the following command:</span></span>
     
       ```powershell
       get-azurevm -servicename yourservicename | get-azureendpoint -VM {$_.VM} | select Vip
       ```
     
     <span data-ttu-id="70923-169">Enregistrez l’adresse IP. Vous en aurez besoin lors de la création d’un enregistrement A.</span><span class="sxs-lookup"><span data-stu-id="70923-169">Save the IP address, as you will need it when creating an A record.</span></span>
2. <span data-ttu-id="70923-170">Connectez-vous au site web du bureau d’enregistrement de votre DNS et accédez à la page de gestion DNS.</span><span class="sxs-lookup"><span data-stu-id="70923-170">Log on to your DNS registrar's website and go to the page for managing DNS.</span></span> <span data-ttu-id="70923-171">Recherchez la mention **Nom de domaine**, **DNS** ou **Gestion du nom de serveur**.</span><span class="sxs-lookup"><span data-stu-id="70923-171">Look for links or areas of the site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="70923-172">Maintenant, cherchez où vous pouvez sélectionner ou saisir vos enregistrements A.</span><span class="sxs-lookup"><span data-stu-id="70923-172">Now find where you can select or enter A record's.</span></span> <span data-ttu-id="70923-173">Il se peut que vous deviez sélectionner le type d'enregistrement dans une liste déroulante ou accéder à une page de paramètres avancés.</span><span class="sxs-lookup"><span data-stu-id="70923-173">You may have to select the record type from a drop down, or go to an advanced settings page.</span></span>
4. <span data-ttu-id="70923-174">Sélectionnez ou entrez le domaine ou sous-domaine qui utilisera cet enregistrement A.</span><span class="sxs-lookup"><span data-stu-id="70923-174">Select or enter the domain or subdomain that will use this A record.</span></span> <span data-ttu-id="70923-175">Par exemple, sélectionnez **www** si vous souhaitez créer un alias pour **www.domainepersonnalisé.com**. Pour créer une entrée avec des caractères génériques pour l’ensemble des sous-domaines, entrez *****.</span><span class="sxs-lookup"><span data-stu-id="70923-175">For example, select **www** if you want to create an alias for **www.customdomain.com**. If you want to create a wildcard entry for all subdomains, enter '*****'.</span></span> <span data-ttu-id="70923-176">Cela permet de couvrir tous les sous-domaines tels que **mail.domainepersonnalisé.com**, **login.domainepersonnalisé.com** et **www.domainepersonnalisé.com**.</span><span class="sxs-lookup"><span data-stu-id="70923-176">This will cover all sub-domains such as **mail.customdomain.com**, **login.customdomain.com**, and **www.customdomain.com**.</span></span>
   
    <span data-ttu-id="70923-177">Si vous voulez créer un enregistrement A pour le domaine racine, l’entrée correspondante devrait être répertoriée avec le symbole «**@**» dans les outils DNS de votre bureau d’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="70923-177">If you want to create an A record for the root domain, it may be listed as the '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="70923-178">Entrez l’adresse IP de votre service cloud dans le champ prévu à cet effet.</span><span class="sxs-lookup"><span data-stu-id="70923-178">Enter the IP address of your cloud service in the provided field.</span></span> <span data-ttu-id="70923-179">Cette opération permet d’associer le domaine de l’enregistrement A avec l’adresse IP de votre déploiement de service cloud.</span><span class="sxs-lookup"><span data-stu-id="70923-179">This associates the domain entry used in the A record with the IP address of your cloud service deployment.</span></span>

<span data-ttu-id="70923-180">Par exemple, l’enregistrement A suivant transfère tout le trafic de **contoso.com** vers **137.135.70.239**, l’adresse IP de votre application déployée :</span><span class="sxs-lookup"><span data-stu-id="70923-180">For example, the following A record forwards all traffic from **contoso.com** to **137.135.70.239**, the IP address of your deployed application:</span></span>

| <span data-ttu-id="70923-181">Nom d'hôte/Sous domaine</span><span class="sxs-lookup"><span data-stu-id="70923-181">Host name/Subdomain</span></span> | <span data-ttu-id="70923-182">Adresse IP</span><span class="sxs-lookup"><span data-stu-id="70923-182">IP address</span></span> |
| --- | --- |
| @ |<span data-ttu-id="70923-183">137.135.70.239</span><span class="sxs-lookup"><span data-stu-id="70923-183">137.135.70.239</span></span> |

<span data-ttu-id="70923-184">Cet exemple montre comment créer un enregistrement A pour le domaine racine.</span><span class="sxs-lookup"><span data-stu-id="70923-184">This example demonstrates creating an A record for the root domain.</span></span> <span data-ttu-id="70923-185">Pour créer une entrée avec des caractères génériques qui couvre l’ensemble des sous-domaines, entrez ***** comme sous-domaine.</span><span class="sxs-lookup"><span data-stu-id="70923-185">If you wish to create a wildcard entry to cover all subdomains, you would enter '*****' as the subdomain.</span></span>

> [!WARNING]
> <span data-ttu-id="70923-186">Les adresses IP dans Azure sont dynamiques par défaut.</span><span class="sxs-lookup"><span data-stu-id="70923-186">IP addresses in Azure are dynamic by default.</span></span> <span data-ttu-id="70923-187">Vous souhaiterez probablement utiliser une [adresse IP réservée](../virtual-network/virtual-networks-reserved-public-ip.md) pour vous assurer que votre adresse IP ne change pas.</span><span class="sxs-lookup"><span data-stu-id="70923-187">You will probably want to use a [reserved IP address](../virtual-network/virtual-networks-reserved-public-ip.md) to ensure that your IP address does not change.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="70923-188">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="70923-188">Next steps</span></span>
* [<span data-ttu-id="70923-189">Gestion des services cloud</span><span class="sxs-lookup"><span data-stu-id="70923-189">How to Manage Cloud Services</span></span>](cloud-services-how-to-manage.md)
* [<span data-ttu-id="70923-190">Mappage du contenu CDN à un domaine personnalisé</span><span class="sxs-lookup"><span data-stu-id="70923-190">How to Map CDN Content to a Custom Domain</span></span>](../cdn/cdn-map-content-to-custom-domain.md)
* <span data-ttu-id="70923-191">[Configuration générale de votre service cloud](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="70923-191">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="70923-192">Découvrez comment [déployer un service cloud](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="70923-192">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="70923-193">Configurez des [certificats SSL](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="70923-193">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>

[Expose Your Application on a Custom Domain]: #access-app
[Add a CNAME Record for Your Custom Domain]: #add-cname
[Expose Your Data on a Custom Domain]: #access-data
[VIP swaps]: cloud-services-how-to-manage-portal.md#how-to-swap-deployments-to-promote-a-staged-deployment-to-production
[Create a CNAME record that associates the subdomain with the storage account]: #create-cname
[portail Azure]: https://portal.azure.com
[vip]: ./media/cloud-services-custom-domain-name-portal/csvip.png
[csurl]: ./media/cloud-services-custom-domain-name-portal/csurl.png
