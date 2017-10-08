---
title: aaaWork avec existant local serveurs proxy et Azure AD | Documents Microsoft
description: "Décrit comment toowork avec existant local serveurs proxy."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.openlocfilehash: 7f8cec4f676f99bead5211bcbcf23056bd7f211f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-existing-on-premises-proxy-servers"></a><span data-ttu-id="54f29-103">Travailler avec des serveurs proxy locaux existants</span><span class="sxs-lookup"><span data-stu-id="54f29-103">Work with existing on-premises proxy servers</span></span>

<span data-ttu-id="54f29-104">Cet article explique comment toowork de connecteurs de Proxy d’Application Azure Active Directory (Azure AD) tooconfigure avec des serveurs proxy sortant.</span><span class="sxs-lookup"><span data-stu-id="54f29-104">This article explains how tooconfigure Azure Active Directory (Azure AD) Application Proxy connectors toowork with outbound proxy servers.</span></span> <span data-ttu-id="54f29-105">Il est destiné aux clients avec des environnements réseau qui ont des proxys existants.</span><span class="sxs-lookup"><span data-stu-id="54f29-105">It is intended for customers with network environments that have existing proxies.</span></span>

<span data-ttu-id="54f29-106">Nous allons commencer par examiner les scénarios de déploiement principaux suivants :</span><span class="sxs-lookup"><span data-stu-id="54f29-106">We start by looking at these main deployment scenarios:</span></span>
* <span data-ttu-id="54f29-107">Configurer les connecteurs toobypass les proxys sortants sur site.</span><span class="sxs-lookup"><span data-stu-id="54f29-107">Configure connectors toobypass your on-premises outbound proxies.</span></span>
* <span data-ttu-id="54f29-108">Configurez des connecteurs toouse un tooaccess proxy sortant Proxy d’Application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="54f29-108">Configure connectors toouse an outbound proxy tooaccess Azure AD Application Proxy.</span></span>

<span data-ttu-id="54f29-109">Pour plus d’informations sur le fonctionnement des connecteurs, consultez [Présentation des connecteurs de proxy d’application Azure AD](application-proxy-understand-connectors.md).</span><span class="sxs-lookup"><span data-stu-id="54f29-109">For more information about how connectors work, see [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md).</span></span>

## <a name="configure-hello-outbound-proxy"></a><span data-ttu-id="54f29-110">Configurer un proxy sortant de hello</span><span class="sxs-lookup"><span data-stu-id="54f29-110">Configure hello outbound proxy</span></span>

<span data-ttu-id="54f29-111">Si vous avez un proxy sortant dans votre environnement, utilisez un compte avec le proxy sortant du hello tooconfigure les autorisations appropriées.</span><span class="sxs-lookup"><span data-stu-id="54f29-111">If you have an outbound proxy in your environment, use an account with appropriate permissions tooconfigure hello outbound proxy.</span></span> <span data-ttu-id="54f29-112">Étant donné que le programme d’installation Bonjour s’exécute dans le contexte hello d’utilisateur hello qui effectue l’installation de hello, vous pouvez vérifier la configuration de hello à l’aide de Microsoft Edge ou un autre navigateur Internet.</span><span class="sxs-lookup"><span data-stu-id="54f29-112">Because hello installer runs in hello context of hello user who's doing hello installation, you can check hello configuration by using Microsoft Edge or another Internet browser.</span></span>

<span data-ttu-id="54f29-113">paramètres du proxy tooconfigure hello dans Microsoft Edge :</span><span class="sxs-lookup"><span data-stu-id="54f29-113">tooconfigure hello proxy settings in Microsoft Edge:</span></span>

1. <span data-ttu-id="54f29-114">Accédez trop**paramètres** > **afficher les paramètres avancés** > **ouvrir les paramètres Proxy** > **l’installation manuelle du Proxy** .</span><span class="sxs-lookup"><span data-stu-id="54f29-114">Go too**Settings** > **View Advanced Settings** > **Open Proxy Settings** > **Manual Proxy Setup**.</span></span>
2. <span data-ttu-id="54f29-115">Définissez **utiliser un serveur proxy** trop**sur**, sélectionnez hello **n’utilisez pas serveur de proxy hello pour les adresses locales (intranet)** case à cocher, puis les tooreflect modification hello adresse et port votre serveur proxy local.</span><span class="sxs-lookup"><span data-stu-id="54f29-115">Set **Use a proxy server** too**On**, select hello **Don’t use hello proxy server for local (intranet) addresses** check box, and then change hello address and port tooreflect your local proxy server.</span></span>
3. <span data-ttu-id="54f29-116">Renseignez les paramètres du proxy nécessaire hello.</span><span class="sxs-lookup"><span data-stu-id="54f29-116">Fill in hello necessary proxy settings.</span></span>

   ![Boîte de dialogue des paramètres de proxy](./media/application-proxy-working-with-proxy-servers/proxy-bypass-local-addresses.png)

## <a name="bypass-outbound-proxies"></a><span data-ttu-id="54f29-118">Proxys sortants de contournement</span><span class="sxs-lookup"><span data-stu-id="54f29-118">Bypass outbound proxies</span></span>

<span data-ttu-id="54f29-119">Les connecteurs ont des composants de système d’exploitation sous-jacents qui effectuent des demandes sortantes.</span><span class="sxs-lookup"><span data-stu-id="54f29-119">Connectors have underlying OS components that make outbound requests.</span></span> <span data-ttu-id="54f29-120">Ces composants tente automatiquement de toolocate un serveur proxy sur le réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="54f29-120">These components automatically attempt toolocate a proxy server on hello network.</span></span> <span data-ttu-id="54f29-121">Ils utilisent la détection automatique WPAD (Web Proxy), s’il est activé dans l’environnement de hello.</span><span class="sxs-lookup"><span data-stu-id="54f29-121">They use Web Proxy Auto-Discovery (WPAD), if it's enabled in hello environment.</span></span>

<span data-ttu-id="54f29-122">composants du système d’exploitation Hello tentative toolocate un serveur proxy en effectuant une recherche DNS pour wpad.domainsuffix.</span><span class="sxs-lookup"><span data-stu-id="54f29-122">hello OS components attempt toolocate a proxy server by carrying out a DNS lookup for wpad.domainsuffix.</span></span> <span data-ttu-id="54f29-123">Si cela résout dans DNS, une demande HTTP est effectuée puis toohello IP adresse wpad.dat.</span><span class="sxs-lookup"><span data-stu-id="54f29-123">If this resolves in DNS, an HTTP request is then made toohello IP address for wpad.dat.</span></span> <span data-ttu-id="54f29-124">Cette demande devient un script de configuration du proxy hello dans votre environnement.</span><span class="sxs-lookup"><span data-stu-id="54f29-124">This request becomes hello proxy configuration script in your environment.</span></span> <span data-ttu-id="54f29-125">connecteur de Hello utilise cette tooselect script un serveur proxy sortant.</span><span class="sxs-lookup"><span data-stu-id="54f29-125">hello connector uses this script tooselect an outbound proxy server.</span></span> <span data-ttu-id="54f29-126">Toutefois, le trafic de connecteur peut toujours pas abouti, en raison des paramètres de configuration supplémentaire nécessaires sur le proxy hello.</span><span class="sxs-lookup"><span data-stu-id="54f29-126">However, connector traffic might still not go through, because of additional configuration settings needed on hello proxy.</span></span>

<span data-ttu-id="54f29-127">Vous pouvez configurer toobypass de connecteur hello votre tooensure proxy local qu’il utilise directe connectivité toohello Azure services.</span><span class="sxs-lookup"><span data-stu-id="54f29-127">You can configure hello connector toobypass your on-premises proxy tooensure that it uses direct connectivity toohello Azure services.</span></span> <span data-ttu-id="54f29-128">Nous recommandons cette approche (si votre stratégie réseau le permet), car elle signifie que vous disposez d’un moins toomaintain de configuration.</span><span class="sxs-lookup"><span data-stu-id="54f29-128">We recommend this approach (if your network policy allows for it), because it means that you have one less configuration toomaintain.</span></span>

<span data-ttu-id="54f29-129">l’utilisation de proxy sortant toodisable pour le connecteur de hello, modifier le fichier de C:\Program Files\Microsoft AAD application Proxy Connector\ApplicationProxyConnectorService.exe.config hello et ajouter hello *system.net* section indiquée dans cet exemple de code :</span><span class="sxs-lookup"><span data-stu-id="54f29-129">toodisable outbound proxy usage for hello connector, edit hello C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add hello *system.net* section shown in this code sample:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.net>
    <defaultProxy enabled="false"></defaultProxy>
  </system.net>
  <runtime>
    <gcServer enabled="true"/>
  </runtime>
  <appSettings>
    <add key="TraceFilename" value="AadAppProxyConnector.log" />
  </appSettings>
</configuration>
```
<span data-ttu-id="54f29-130">tooensure que service de mise à jour du connecteur hello ignore également les proxy hello, apporter un modification toohello ApplicationProxyConnectorUpdaterService.exe.config un fichier similaire situé dans C:\Program Files\Microsoft AAD application Proxy Connector mise à jour.</span><span class="sxs-lookup"><span data-stu-id="54f29-130">tooensure that hello Connector Updater service also bypasses hello proxy, make a similar change toohello ApplicationProxyConnectorUpdaterService.exe.config file located at C:\Program Files\Microsoft AAD App Proxy Connector Updater.</span></span>

<span data-ttu-id="54f29-131">Être sûr de copies de toomake des fichiers d’origine de hello, au cas où vous avez besoin des fichiers .config de toorevert toohello par défaut.</span><span class="sxs-lookup"><span data-stu-id="54f29-131">Be sure toomake copies of hello original files, in case you need toorevert toohello default .config files.</span></span>

## <a name="use-hello-outbound-proxy-server"></a><span data-ttu-id="54f29-132">Utiliser un serveur proxy sortant hello</span><span class="sxs-lookup"><span data-stu-id="54f29-132">Use hello outbound proxy server</span></span>

<span data-ttu-id="54f29-133">Certains environnements nécessitent tous les toogo le trafic sortant via un proxy sortant, sans exception.</span><span class="sxs-lookup"><span data-stu-id="54f29-133">Some environments require all outbound traffic toogo through an outbound proxy, without exception.</span></span> <span data-ttu-id="54f29-134">Par conséquent, en ignorant les proxy hello n’est pas une option.</span><span class="sxs-lookup"><span data-stu-id="54f29-134">As a result, bypassing hello proxy is not an option.</span></span>

<span data-ttu-id="54f29-135">Vous pouvez configurer hello connecteur trafic toogo via le proxy sortant hello, comme indiqué dans hello suivant schéma :</span><span class="sxs-lookup"><span data-stu-id="54f29-135">You can configure hello connector traffic toogo through hello outbound proxy, as shown in hello following diagram:</span></span>

 ![Configuration du connecteur les toogo de trafic via un proxy sortant de tooAzure AD Proxy d’Application](./media/application-proxy-working-with-proxy-servers/configure-proxy-settings.png)

<span data-ttu-id="54f29-137">Par conséquent d’obtenir uniquement le trafic sortant, il est sans tooconfigure besoin accès via votre pare-feu entrant.</span><span class="sxs-lookup"><span data-stu-id="54f29-137">As a result of having only outbound traffic, there's no need tooconfigure inbound access through your firewalls.</span></span>

### <a name="step-1-configure-hello-connector-and-related-services-toogo-through-hello-outbound-proxy"></a><span data-ttu-id="54f29-138">Étape 1 : Configurer le connecteur de hello et liées toogo services via le proxy sortant hello</span><span class="sxs-lookup"><span data-stu-id="54f29-138">Step 1: Configure hello connector and related services toogo through hello outbound proxy</span></span>

<span data-ttu-id="54f29-139">Comme indiqué précédemment, si WPAD est activée dans l’environnement de hello et correctement configuré, connecteur de hello détecte automatiquement toouse de serveur et de la tentative de proxy sortant hello il.</span><span class="sxs-lookup"><span data-stu-id="54f29-139">As covered earlier, if WPAD is enabled in hello environment and configured appropriately, hello connector will automatically discover hello outbound proxy server and attempt toouse it.</span></span> <span data-ttu-id="54f29-140">Toutefois, vous pouvez configurer explicitement toogo de connecteur hello via un proxy sortant.</span><span class="sxs-lookup"><span data-stu-id="54f29-140">However, you can explicitly configure hello connector toogo through an outbound proxy.</span></span>

<span data-ttu-id="54f29-141">toodo, modifiez le fichier de C:\Program Files\Microsoft AAD application Proxy Connector\ApplicationProxyConnectorService.exe.config hello et ajouter hello *system.net* section indiquée dans cet exemple de code.</span><span class="sxs-lookup"><span data-stu-id="54f29-141">toodo so, edit hello C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add hello *system.net* section shown in this code sample.</span></span> <span data-ttu-id="54f29-142">Modification *proxyserver:8080* tooreflect votre nom de serveur proxy local ou une adresse IP et un hello qu’elle est à l’écoute sur le port.</span><span class="sxs-lookup"><span data-stu-id="54f29-142">Change *proxyserver:8080* tooreflect your local proxy server name or IP address, and hello port that it's listening on.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.net>  
    <defaultProxy>   
      <proxy proxyaddress="http://proxyserver:8080" bypassonlocal="True" usesystemdefault="True"/>   
    </defaultProxy>  
  </system.net>
  <runtime>
    <gcServer enabled="true"/>
  </runtime>
  <appSettings>
    <add key="TraceFilename" value="AadAppProxyConnector.log" />
  </appSettings>
</configuration>
```

<span data-ttu-id="54f29-143">Ensuite, configurez le proxy hello toouse du service de mise à jour du connecteur hello en effectuant un fichier de toohello modification similaire situé dans C:\Program Files\Microsoft AAD application Proxy Connector Updater\ApplicationProxyConnectorUpdaterService.exe.config.</span><span class="sxs-lookup"><span data-stu-id="54f29-143">Next, configure hello Connector Updater service toouse hello proxy by making a similar change toohello file located at C:\Program Files\Microsoft AAD App Proxy Connector Updater\ApplicationProxyConnectorUpdaterService.exe.config.</span></span>

### <a name="step-2-configure-hello-proxy-tooallow-traffic-from-hello-connector-and-related-services-tooflow-through"></a><span data-ttu-id="54f29-144">Étape 2 : Configurer hello proxy tooallow le trafic de connecteur de hello et tooflow services connexes via</span><span class="sxs-lookup"><span data-stu-id="54f29-144">Step 2: Configure hello proxy tooallow traffic from hello connector and related services tooflow through</span></span>

<span data-ttu-id="54f29-145">Il existe quatre aspects tooconsider au proxy sortant de hello :</span><span class="sxs-lookup"><span data-stu-id="54f29-145">There are four aspects tooconsider at hello outbound proxy:</span></span>
* <span data-ttu-id="54f29-146">Règles sortantes du proxy</span><span class="sxs-lookup"><span data-stu-id="54f29-146">Proxy outbound rules</span></span>
* <span data-ttu-id="54f29-147">Authentification du proxy</span><span class="sxs-lookup"><span data-stu-id="54f29-147">Proxy authentication</span></span>
* <span data-ttu-id="54f29-148">Ports du proxy</span><span class="sxs-lookup"><span data-stu-id="54f29-148">Proxy ports</span></span>
* <span data-ttu-id="54f29-149">Inspection SSL</span><span class="sxs-lookup"><span data-stu-id="54f29-149">SSL inspection</span></span>

#### <a name="proxy-outbound-rules"></a><span data-ttu-id="54f29-150">Règles sortantes du proxy</span><span class="sxs-lookup"><span data-stu-id="54f29-150">Proxy outbound rules</span></span>
<span data-ttu-id="54f29-151">Autoriser toohello accès suivant les points de terminaison pour l’accès au service de connecteur :</span><span class="sxs-lookup"><span data-stu-id="54f29-151">Allow access toohello following endpoints for connector service access:</span></span>

* <span data-ttu-id="54f29-152">*.msappproxy.net</span><span class="sxs-lookup"><span data-stu-id="54f29-152">*.msappproxy.net</span></span>
* <span data-ttu-id="54f29-153">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="54f29-153">*.servicebus.windows.net</span></span>

<span data-ttu-id="54f29-154">Autorise l’inscription initiale, toohello d’accès suivant les points de terminaison :</span><span class="sxs-lookup"><span data-stu-id="54f29-154">For initial registration, allow access toohello following endpoints:</span></span>

* <span data-ttu-id="54f29-155">login.windows.net</span><span class="sxs-lookup"><span data-stu-id="54f29-155">login.windows.net</span></span>
* <span data-ttu-id="54f29-156">login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="54f29-156">login.microsoftonline.com</span></span>

<span data-ttu-id="54f29-157">Si vous ne pouvez pas autoriser la connexion par le nom de domaine complet et ont besoin de plages d’adresses IP toospecify utiliser à la place, ces options :</span><span class="sxs-lookup"><span data-stu-id="54f29-157">If you can't allow connectivity by FQDN and need toospecify IP ranges instead, use these options:</span></span>

* <span data-ttu-id="54f29-158">Autoriser l’accès sortant du connecteur hello tooall destinations.</span><span class="sxs-lookup"><span data-stu-id="54f29-158">Allow hello connector outbound access tooall destinations.</span></span>
* <span data-ttu-id="54f29-159">Autoriser l’accès sortant du connecteur hello trop[plages d’adresses IP de centre de données Azure](https://www.microsoft.com/en-gb/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="54f29-159">Allow hello connector outbound access too[Azure datacenter IP ranges](https://www.microsoft.com/en-gb/download/details.aspx?id=41653).</span></span> <span data-ttu-id="54f29-160">défi Hello à l’aide de la liste de hello des plages d’adresses IP de centre de données Azure est qu’il est mis à jour chaque semaine.</span><span class="sxs-lookup"><span data-stu-id="54f29-160">hello challenge with using hello list of Azure datacenter IP ranges is that it's updated weekly.</span></span> <span data-ttu-id="54f29-161">Vous devez tooput un processus dans tooensure lieu que les règles d’accès sont mis à jour en conséquence.</span><span class="sxs-lookup"><span data-stu-id="54f29-161">You need tooput a process in place tooensure that your access rules are updated accordingly.</span></span>

#### <a name="proxy-authentication"></a><span data-ttu-id="54f29-162">Authentification du proxy</span><span class="sxs-lookup"><span data-stu-id="54f29-162">Proxy authentication</span></span>

<span data-ttu-id="54f29-163">L’authentification proxy n'est actuellement pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="54f29-163">Proxy authentication is not currently supported.</span></span> <span data-ttu-id="54f29-164">Notre recommandation actuelle est destinations Internet de la toohello tooallow hello connecteur l’accès anonyme.</span><span class="sxs-lookup"><span data-stu-id="54f29-164">Our current recommendation is tooallow hello connector anonymous access toohello Internet destinations.</span></span>

#### <a name="proxy-ports"></a><span data-ttu-id="54f29-165">Ports du proxy</span><span class="sxs-lookup"><span data-stu-id="54f29-165">Proxy ports</span></span>

<span data-ttu-id="54f29-166">connecteur de Hello rend les connexions SSL sortantes en utilisant la méthode de connexion hello.</span><span class="sxs-lookup"><span data-stu-id="54f29-166">hello connector makes outbound SSL-based connections by using hello CONNECT method.</span></span> <span data-ttu-id="54f29-167">Cette méthode définit essentiellement un tunnel via le proxy sortant hello.</span><span class="sxs-lookup"><span data-stu-id="54f29-167">This method essentially sets up a tunnel through hello outbound proxy.</span></span> <span data-ttu-id="54f29-168">Configurer hello proxy server tooallow tunneling tooports 443 et 80.</span><span class="sxs-lookup"><span data-stu-id="54f29-168">Configure hello proxy server tooallow tunneling tooports 443 and 80.</span></span>

>[!NOTE]
><span data-ttu-id="54f29-169">Lorsque Service Bus s’exécute via le protocole HTTPS, il utilise le port 443.</span><span class="sxs-lookup"><span data-stu-id="54f29-169">When Service Bus runs over HTTPS, it uses port 443.</span></span> <span data-ttu-id="54f29-170">Toutefois, par défaut, Service Bus tente de connexions TCP directes et revient tooHTTPS uniquement si une connexion directe échoue.</span><span class="sxs-lookup"><span data-stu-id="54f29-170">However, by default, Service Bus attempts direct TCP connections and falls back tooHTTPS only if direct connectivity fails.</span></span>

<span data-ttu-id="54f29-171">tooensure hello Service Bus, le trafic est également envoyé via le serveur proxy sortant de hello, assurez-vous que le connecteur hello ne peut pas se connecter directement toohello des services Azure pour les ports 9350, 9352 et 5671.</span><span class="sxs-lookup"><span data-stu-id="54f29-171">tooensure that hello Service Bus traffic is also sent through hello outbound proxy server, ensure that hello connector cannot directly connect toohello Azure services for ports 9350, 9352, and 5671.</span></span>

#### <a name="ssl-inspection"></a><span data-ttu-id="54f29-172">Inspection SSL</span><span class="sxs-lookup"><span data-stu-id="54f29-172">SSL inspection</span></span>
<span data-ttu-id="54f29-173">N’utilisez pas l’inspection SSL pour le trafic de connecteur hello, car il provoque des problèmes pour le trafic de connecteur hello.</span><span class="sxs-lookup"><span data-stu-id="54f29-173">Do not use SSL inspection for hello connector traffic, because it causes problems for hello connector traffic.</span></span>

## <a name="troubleshoot-connector-proxy-problems-and-service-connectivity-issues"></a><span data-ttu-id="54f29-174">Résoudre les problèmes courants de proxy de connecteur et de connectivité du service</span><span class="sxs-lookup"><span data-stu-id="54f29-174">Troubleshoot connector proxy problems and service connectivity issues</span></span>
<span data-ttu-id="54f29-175">Vous devez maintenant voir tout le trafic circulant via le proxy hello.</span><span class="sxs-lookup"><span data-stu-id="54f29-175">Now you should see all traffic flowing through hello proxy.</span></span> <span data-ttu-id="54f29-176">Si vous rencontrez des problèmes, doit favoriser le hello suivant des informations de dépannage.</span><span class="sxs-lookup"><span data-stu-id="54f29-176">If you have problems, hello following troubleshooting information should help.</span></span>

<span data-ttu-id="54f29-177">Hello la meilleure façon tooidentify et résoudre les problèmes de connectivité du connecteur problèmes est tootake un réseau de capture sur le service du connecteur hello lors du démarrage du service Connecteur hello.</span><span class="sxs-lookup"><span data-stu-id="54f29-177">hello best way tooidentify and troubleshoot connector connectivity issues is tootake a network capture on hello connector service while starting hello connector service.</span></span> <span data-ttu-id="54f29-178">Cela peut être une tâche ardue, aussi examinons quelques conseils rapides sur la capture et le filtrage des traces réseau.</span><span class="sxs-lookup"><span data-stu-id="54f29-178">This can be a daunting task, so let’s look at quick tips on capturing and filtering network traces.</span></span>

<span data-ttu-id="54f29-179">Vous pouvez utiliser hello analyse de l’outil de votre choix.</span><span class="sxs-lookup"><span data-stu-id="54f29-179">You can use hello monitoring tool of your choice.</span></span> <span data-ttu-id="54f29-180">Pour des raisons de hello de cet article, nous avons utilisé Microsoft Network Monitor 3.4.</span><span class="sxs-lookup"><span data-stu-id="54f29-180">For hello purposes of this article, we used Microsoft Network Monitor 3.4.</span></span> <span data-ttu-id="54f29-181">Vous pouvez [le télécharger à partir de Microsoft](https://www.microsoft.com/download/details.aspx?id=4865).</span><span class="sxs-lookup"><span data-stu-id="54f29-181">You can [download it from Microsoft](https://www.microsoft.com/download/details.aspx?id=4865).</span></span>

<span data-ttu-id="54f29-182">les exemples Hello et les filtres que nous utilisons dans les sections suivantes de hello sont spécifique tooNetwork moniteur, mais les principes hello peuvent être appliqué tooany l’outil d’analyse.</span><span class="sxs-lookup"><span data-stu-id="54f29-182">hello examples and filters that we use in hello following sections are specific tooNetwork Monitor, but hello principles can be applied tooany analysis tool.</span></span>

### <a name="take-a-capture-by-using-network-monitor"></a><span data-ttu-id="54f29-183">Prendre une capture à l’aide de Network Monitor</span><span class="sxs-lookup"><span data-stu-id="54f29-183">Take a capture by using Network Monitor</span></span>

<span data-ttu-id="54f29-184">toostart une capture :</span><span class="sxs-lookup"><span data-stu-id="54f29-184">toostart a capture:</span></span>

1. <span data-ttu-id="54f29-185">Ouvrez Network Monitor, puis cliquez sur **Nouvelle capture**.</span><span class="sxs-lookup"><span data-stu-id="54f29-185">Open Network Monitor and click **New Capture**.</span></span>
2. <span data-ttu-id="54f29-186">Cliquez sur hello **Démarrer** bouton.</span><span class="sxs-lookup"><span data-stu-id="54f29-186">Click hello **Start** button.</span></span>

   ![Fenêtre de Network Monitor](./media/application-proxy-working-with-proxy-servers/network-capture.png)

<span data-ttu-id="54f29-188">Après avoir effectué une capture, cliquez sur hello **arrêter** bouton tooend il.</span><span class="sxs-lookup"><span data-stu-id="54f29-188">After you complete a capture, click hello **Stop** button tooend it.</span></span>

### <a name="take-a-capture-of-connector-traffic"></a><span data-ttu-id="54f29-189">Effectuez une capture du trafic de connecteur</span><span class="sxs-lookup"><span data-stu-id="54f29-189">Take a capture of connector traffic</span></span>

<span data-ttu-id="54f29-190">Pour le dépannage initiale, effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="54f29-190">For initial troubleshooting, perform hello following steps:</span></span>

1. <span data-ttu-id="54f29-191">À partir de services.msc, arrêtez le service de connecteur Proxy d’Application Azure AD de hello.</span><span class="sxs-lookup"><span data-stu-id="54f29-191">From services.msc, stop hello Azure AD Application Proxy Connector service.</span></span>
2. <span data-ttu-id="54f29-192">Démarrer la capture de réseau hello.</span><span class="sxs-lookup"><span data-stu-id="54f29-192">Start hello network capture.</span></span>
3. <span data-ttu-id="54f29-193">Démarrer le service de connecteur Proxy d’Application Azure AD hello.</span><span class="sxs-lookup"><span data-stu-id="54f29-193">Start hello Azure AD Application Proxy Connector service.</span></span>
4. <span data-ttu-id="54f29-194">Arrêter la capture de réseau hello.</span><span class="sxs-lookup"><span data-stu-id="54f29-194">Stop hello network capture.</span></span>

   ![Service de connecteur de proxy d’application Azure AD dans services.msc](./media/application-proxy-working-with-proxy-servers/services-local.png)

### <a name="look-at-hello-requests-from-hello-connector-toohello-proxy-server"></a><span data-ttu-id="54f29-196">Examiner les demandes de hello à partir du serveur de proxy hello connecteur toohello</span><span class="sxs-lookup"><span data-stu-id="54f29-196">Look at hello requests from hello connector toohello proxy server</span></span>

<span data-ttu-id="54f29-197">Maintenant que vous avez une capture réseau, vous êtes prêt toofilter il.</span><span class="sxs-lookup"><span data-stu-id="54f29-197">Now that you’ve got a network capture, you're ready toofilter it.</span></span> <span data-ttu-id="54f29-198">toolooking de clé Hello au niveau de la trace de hello est de comprendre comment capturer les toofilter hello.</span><span class="sxs-lookup"><span data-stu-id="54f29-198">hello key toolooking at hello trace is understanding how toofilter hello capture.</span></span>

<span data-ttu-id="54f29-199">Un filtre est comme suit (où 8080 est le port du service proxy hello) :</span><span class="sxs-lookup"><span data-stu-id="54f29-199">One filter is as follows (where 8080 is hello proxy service port):</span></span>

<span data-ttu-id="54f29-200">**(http.Request or http.Response) and tcp.port==8080**</span><span class="sxs-lookup"><span data-stu-id="54f29-200">**(http.Request or http.Response) and tcp.port==8080**</span></span>

<span data-ttu-id="54f29-201">Si vous entrez ce filtre Bonjour **filtre d’affichage** et sélectionnez **appliquer**, filtres de trafic hello capturée en fonction de filtre de hello.</span><span class="sxs-lookup"><span data-stu-id="54f29-201">If you enter this filter in hello **Display Filter** window and select **Apply**, it filters hello captured traffic based on hello filter.</span></span>

<span data-ttu-id="54f29-202">Hello filtre précédent montre simplement hello demandes et réponses HTTP à partir de port du proxy hello.</span><span class="sxs-lookup"><span data-stu-id="54f29-202">hello preceding filter shows just hello HTTP requests and responses to/from hello proxy port.</span></span> <span data-ttu-id="54f29-203">Pour un démarrage du connecteur sur lequel le connecteur de hello est toouse configuré un serveur proxy, le filtre de hello indiquerait quelque chose comme ceci :</span><span class="sxs-lookup"><span data-stu-id="54f29-203">For a connector startup where hello connector is configured toouse a proxy server, hello filter would show something like this:</span></span>

 ![Exemple de liste de requêtes et réponses HTTP filtrées](./media/application-proxy-working-with-proxy-servers/http-requests.png)

<span data-ttu-id="54f29-205">Vous maintenant spécifiquement recherchez hello que Connect demande qui illustrent la communication avec le serveur de proxy hello.</span><span class="sxs-lookup"><span data-stu-id="54f29-205">You're now specifically looking for hello CONNECT requests that show communication with hello proxy server.</span></span> <span data-ttu-id="54f29-206">En cas de succès, vous obtenez une réponse HTTP OK (200).</span><span class="sxs-lookup"><span data-stu-id="54f29-206">Upon success, you get an HTTP OK (200) response.</span></span>

<span data-ttu-id="54f29-207">Si vous voyez les autres codes de réponse, telles que 407 ou 502, proxy de hello est nécessitant une authentification ou ne pas autoriser le trafic de hello pour une raison quelconque.</span><span class="sxs-lookup"><span data-stu-id="54f29-207">If you see other response codes, such as 407 or 502, hello proxy is requiring authentication or not allowing hello traffic for some other reason.</span></span> <span data-ttu-id="54f29-208">À ce stade, vous impliquez l’équipe de support technique de votre serveur proxy.</span><span class="sxs-lookup"><span data-stu-id="54f29-208">At this point, you engage your proxy server support team.</span></span>

### <a name="identify-failed-tcp-connection-attempts"></a><span data-ttu-id="54f29-209">Identifier les tentatives de connexion TCP ayant échoué</span><span class="sxs-lookup"><span data-stu-id="54f29-209">Identify failed TCP connection attempts</span></span>

<span data-ttu-id="54f29-210">Hello autre scénario courant dans lequel vous pouvez être intéressé est lorsque hello connecteur tente tooconnect directement, mais il échoue.</span><span class="sxs-lookup"><span data-stu-id="54f29-210">hello other common scenario that you may be interested in is when hello connector is trying tooconnect directly, but it's failing.</span></span>

<span data-ttu-id="54f29-211">Un autre filtre de moniteur réseau qui permet d’identifier ce problème vous tooeasily est la suivante :</span><span class="sxs-lookup"><span data-stu-id="54f29-211">Another Network Monitor filter that helps you tooeasily identify this problem is:</span></span>

<span data-ttu-id="54f29-212">**property.TCPSynRetransmit**</span><span class="sxs-lookup"><span data-stu-id="54f29-212">**property.TCPSynRetransmit**</span></span>

<span data-ttu-id="54f29-213">Un paquet SYN est envoyé de premier paquet de hello tooestablish une connexion TCP.</span><span class="sxs-lookup"><span data-stu-id="54f29-213">A SYN packet is hello first packet sent tooestablish a TCP connection.</span></span> <span data-ttu-id="54f29-214">Si ce paquet ne retourne pas une réponse, hello SYN est retentée.</span><span class="sxs-lookup"><span data-stu-id="54f29-214">If this packet doesn’t return a response, hello SYN is reattempted.</span></span> <span data-ttu-id="54f29-215">Vous pouvez utiliser hello précédant toosee de filtre des requêtes SYN retransmis.</span><span class="sxs-lookup"><span data-stu-id="54f29-215">You can use hello preceding filter toosee any retransmitted SYNs.</span></span> <span data-ttu-id="54f29-216">Ensuite, vous pouvez vérifier si ces requêtes SYN correspondre tooany liés au connecteur du trafic.</span><span class="sxs-lookup"><span data-stu-id="54f29-216">Then, you can check whether these SYNs correspond tooany connector-related traffic.</span></span>

<span data-ttu-id="54f29-217">Hello suivant montre une tentative de connexion ayant échoué port de Bus tooService 9352 :</span><span class="sxs-lookup"><span data-stu-id="54f29-217">hello following example shows a failed connection attempt tooService Bus port 9352:</span></span>

 ![Exemple de réponse à une tentative de connexion ayant échoué](./media/application-proxy-working-with-proxy-servers/failed-connection-attempt.png)

<span data-ttu-id="54f29-219">Si vous voyez quelque chose comme hello précédant la réponse, connecteur de hello tente toocommunicate directement avec hello Service service Bus Azure.</span><span class="sxs-lookup"><span data-stu-id="54f29-219">If you see something like hello preceding response, hello connector is trying toocommunicate directly with hello Azure Service Bus service.</span></span> <span data-ttu-id="54f29-220">Si vous prévoyez de hello connecteur toomake des connexions directes toohello Azure services, cette réponse est une indication que vous avez un problème réseau ou un pare-feu.</span><span class="sxs-lookup"><span data-stu-id="54f29-220">If you expect hello connector toomake direct connections toohello Azure services, this response is a clear indication that you have a network or firewall problem.</span></span>

>[!NOTE]
><span data-ttu-id="54f29-221">Si vous êtes toouse configuré un serveur proxy, cette réponse peut signifier que Service Bus tente une connexion TCP directe avant de basculer tooattempting une connexion via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="54f29-221">If you are configured toouse a proxy server, this response might mean that Service Bus is attempting a direct TCP connection before switching tooattempting a connection over HTTPS.</span></span>
>

<span data-ttu-id="54f29-222">L’analyse des traces réseau n’est pas faite pour tout le monde.</span><span class="sxs-lookup"><span data-stu-id="54f29-222">Network trace analysis is not for everyone.</span></span> <span data-ttu-id="54f29-223">Mais il peut être une outil précieux tooget rapidement des informations sur ce qui se passe votre réseau.</span><span class="sxs-lookup"><span data-stu-id="54f29-223">But it can be a valuable tool tooget quick information about what's going on with your network.</span></span>

<span data-ttu-id="54f29-224">Si vous continuez toostruggle avec des problèmes de connectivité du connecteur, créez un ticket avec notre équipe de support.</span><span class="sxs-lookup"><span data-stu-id="54f29-224">If you continue toostruggle with connector connectivity issues, create a ticket with our support team.</span></span> <span data-ttu-id="54f29-225">équipe de Hello peut vous aider à résoudre le problème.</span><span class="sxs-lookup"><span data-stu-id="54f29-225">hello team can assist you with further troubleshooting.</span></span>

<span data-ttu-id="54f29-226">Pour plus d’informations sur la résolution des erreurs avec le connecteur de proxy d’application, consultez [Résoudre les problèmes du proxy d’application](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).</span><span class="sxs-lookup"><span data-stu-id="54f29-226">For information about resolving errors with Application Proxy Connector, see [Troubleshoot Application Proxy](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).</span></span>

## <a name="next-steps"></a><span data-ttu-id="54f29-227">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="54f29-227">Next steps</span></span>

[<span data-ttu-id="54f29-228">Présentation des connecteurs de proxy d’application Azure AD</span><span class="sxs-lookup"><span data-stu-id="54f29-228">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)<br><span data-ttu-id="54f29-229">
[Comment toosilently installer hello connecteur Proxy d’Application Azure AD](active-directory-application-proxy-silent-installation.md)</span><span class="sxs-lookup"><span data-stu-id="54f29-229">
[How toosilently install hello Azure AD Application Proxy Connector ](active-directory-application-proxy-silent-installation.md)</span></span>
