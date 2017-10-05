---
title: Travailler avec des serveurs proxy locaux existants et Azure AD | Microsoft Docs
description: Explique comment travailler avec des serveurs proxy locaux existants.
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
ms.openlocfilehash: bdca442755507c4ffe8d43692c5b7f2aa3a746f3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="work-with-existing-on-premises-proxy-servers"></a><span data-ttu-id="30cf4-103">Travailler avec des serveurs proxy locaux existants</span><span class="sxs-lookup"><span data-stu-id="30cf4-103">Work with existing on-premises proxy servers</span></span>

<span data-ttu-id="30cf4-104">Cet article explique comment configurer les connecteurs de proxy d’application Azure Active Directory (Azure AD) pour fonctionner avec des serveurs proxy sortants.</span><span class="sxs-lookup"><span data-stu-id="30cf4-104">This article explains how to configure Azure Active Directory (Azure AD) Application Proxy connectors to work with outbound proxy servers.</span></span> <span data-ttu-id="30cf4-105">Il est destiné aux clients avec des environnements réseau qui ont des proxys existants.</span><span class="sxs-lookup"><span data-stu-id="30cf4-105">It is intended for customers with network environments that have existing proxies.</span></span>

<span data-ttu-id="30cf4-106">Nous allons commencer par examiner les scénarios de déploiement principaux suivants :</span><span class="sxs-lookup"><span data-stu-id="30cf4-106">We start by looking at these main deployment scenarios:</span></span>
* <span data-ttu-id="30cf4-107">Configurer des connecteurs pour contourner vos proxys sortants locaux.</span><span class="sxs-lookup"><span data-stu-id="30cf4-107">Configure connectors to bypass your on-premises outbound proxies.</span></span>
* <span data-ttu-id="30cf4-108">Configurer des connecteurs pour utiliser un proxy sortant afin d’accéder au proxy d’application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="30cf4-108">Configure connectors to use an outbound proxy to access Azure AD Application Proxy.</span></span>

<span data-ttu-id="30cf4-109">Pour plus d’informations sur le fonctionnement des connecteurs, consultez [Présentation des connecteurs de proxy d’application Azure AD](application-proxy-understand-connectors.md).</span><span class="sxs-lookup"><span data-stu-id="30cf4-109">For more information about how connectors work, see [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md).</span></span>

## <a name="configure-the-outbound-proxy"></a><span data-ttu-id="30cf4-110">Configuration du serveur proxy sortant</span><span class="sxs-lookup"><span data-stu-id="30cf4-110">Configure the outbound proxy</span></span>

<span data-ttu-id="30cf4-111">Si votre environnement comporte un proxy sortant, utilisez un compte avec les autorisations appropriées pour le configurer.</span><span class="sxs-lookup"><span data-stu-id="30cf4-111">If you have an outbound proxy in your environment, use an account with appropriate permissions to configure the outbound proxy.</span></span> <span data-ttu-id="30cf4-112">Étant donné que le programme d’installation s’exécute dans le contexte de l’utilisateur qui effectue l’installation, vous pouvez vérifier la configuration à l’aide de Microsoft Edge ou d’un autre navigateur Internet.</span><span class="sxs-lookup"><span data-stu-id="30cf4-112">Because the installer runs in the context of the user who's doing the installation, you can check the configuration by using Microsoft Edge or another Internet browser.</span></span>

<span data-ttu-id="30cf4-113">Pour configurer les paramètres de proxy dans Microsoft Edge :</span><span class="sxs-lookup"><span data-stu-id="30cf4-113">To configure the proxy settings in Microsoft Edge:</span></span>

1. <span data-ttu-id="30cf4-114">Accédez à **Paramètres** > **Afficher les paramètres avancés** > **Ouvrir les paramètres de proxy** > **Configuration manuelle du proxy**.</span><span class="sxs-lookup"><span data-stu-id="30cf4-114">Go to **Settings** > **View Advanced Settings** > **Open Proxy Settings** > **Manual Proxy Setup**.</span></span>
2. <span data-ttu-id="30cf4-115">Définissez **Utiliser un serveur proxy** sur **Activé**, cochez la case **Ne pas utiliser le serveur proxy pour les adresses intranet locale**, puis modifiez l’adresse et le port pour refléter votre serveur proxy local.</span><span class="sxs-lookup"><span data-stu-id="30cf4-115">Set **Use a proxy server** to **On**, select the **Don’t use the proxy server for local (intranet) addresses** check box, and then change the address and port to reflect your local proxy server.</span></span>
3. <span data-ttu-id="30cf4-116">Renseignez les paramètres de proxy nécessaires.</span><span class="sxs-lookup"><span data-stu-id="30cf4-116">Fill in the necessary proxy settings.</span></span>

   ![Boîte de dialogue des paramètres de proxy](./media/application-proxy-working-with-proxy-servers/proxy-bypass-local-addresses.png)

## <a name="bypass-outbound-proxies"></a><span data-ttu-id="30cf4-118">Proxys sortants de contournement</span><span class="sxs-lookup"><span data-stu-id="30cf4-118">Bypass outbound proxies</span></span>

<span data-ttu-id="30cf4-119">Les connecteurs ont des composants de système d’exploitation sous-jacents qui effectuent des demandes sortantes.</span><span class="sxs-lookup"><span data-stu-id="30cf4-119">Connectors have underlying OS components that make outbound requests.</span></span> <span data-ttu-id="30cf4-120">Ces composants tentent automatiquement de localiser un serveur de proxy sur le réseau.</span><span class="sxs-lookup"><span data-stu-id="30cf4-120">These components automatically attempt to locate a proxy server on the network.</span></span> <span data-ttu-id="30cf4-121">Ils utilisent Web Proxy Auto-Discovery (WPAD), si WPAD est activé dans l’environnement.</span><span class="sxs-lookup"><span data-stu-id="30cf4-121">They use Web Proxy Auto-Discovery (WPAD), if it's enabled in the environment.</span></span>

<span data-ttu-id="30cf4-122">Les composants du système d’exploitation tentent de localiser un serveur proxy en effectuant une recherche DNS pour wpad.domainsuffix.</span><span class="sxs-lookup"><span data-stu-id="30cf4-122">The OS components attempt to locate a proxy server by carrying out a DNS lookup for wpad.domainsuffix.</span></span> <span data-ttu-id="30cf4-123">Si un DNS est renvoyé, une requête HTTP est alors effectuée sur l’adresse IP pour wpad.dat.</span><span class="sxs-lookup"><span data-stu-id="30cf4-123">If this resolves in DNS, an HTTP request is then made to the IP address for wpad.dat.</span></span> <span data-ttu-id="30cf4-124">Cette requête devient le script de configuration de proxy dans votre environnement.</span><span class="sxs-lookup"><span data-stu-id="30cf4-124">This request becomes the proxy configuration script in your environment.</span></span> <span data-ttu-id="30cf4-125">Le connecteur utilise ce script pour sélectionner un serveur proxy sortant.</span><span class="sxs-lookup"><span data-stu-id="30cf4-125">The connector uses this script to select an outbound proxy server.</span></span> <span data-ttu-id="30cf4-126">Toutefois, le trafic du connecteur peut ne pas toujours passer, en raison des paramètres de configuration supplémentaires nécessaires sur le serveur proxy.</span><span class="sxs-lookup"><span data-stu-id="30cf4-126">However, connector traffic might still not go through, because of additional configuration settings needed on the proxy.</span></span>

<span data-ttu-id="30cf4-127">Vous pouvez configurer le connecteur de sorte qu’il contourne votre proxy local pour vous assurer qu’il utilise une connexion directe aux services Azure.</span><span class="sxs-lookup"><span data-stu-id="30cf4-127">You can configure the connector to bypass your on-premises proxy to ensure that it uses direct connectivity to the Azure services.</span></span> <span data-ttu-id="30cf4-128">C’est ce que nous recommandons (si votre stratégie réseau le permet), car cela signifie que vous aurez une configuration de moins à mettre à jour.</span><span class="sxs-lookup"><span data-stu-id="30cf4-128">We recommend this approach (if your network policy allows for it), because it means that you have one less configuration to maintain.</span></span>

<span data-ttu-id="30cf4-129">Pour désactiver l’utilisation d’un proxy sortant pour le connecteur, modifiez le fichier C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config et ajoutez la section *system.net* indiquée dans cet exemple de code :</span><span class="sxs-lookup"><span data-stu-id="30cf4-129">To disable outbound proxy usage for the connector, edit the C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add the *system.net* section shown in this code sample:</span></span>

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
<span data-ttu-id="30cf4-130">Pour être sûr que le connecteur du service de mise à jour contourne également le proxy, apportez une modification similaire au fichier ApplicationProxyConnectorUpdaterService.exe.config situé dans C:\Program Files\Microsoft AAD application Proxy Connector Updater.</span><span class="sxs-lookup"><span data-stu-id="30cf4-130">To ensure that the Connector Updater service also bypasses the proxy, make a similar change to the ApplicationProxyConnectorUpdaterService.exe.config file located at C:\Program Files\Microsoft AAD App Proxy Connector Updater.</span></span>

<span data-ttu-id="30cf4-131">Veillez à faire des copies des fichiers d’origine, au cas où vous devriez restaurer les fichiers par défaut.</span><span class="sxs-lookup"><span data-stu-id="30cf4-131">Be sure to make copies of the original files, in case you need to revert to the default .config files.</span></span>

## <a name="use-the-outbound-proxy-server"></a><span data-ttu-id="30cf4-132">Utiliser le serveur proxy sortant</span><span class="sxs-lookup"><span data-stu-id="30cf4-132">Use the outbound proxy server</span></span>

<span data-ttu-id="30cf4-133">Certains environnements clients requièrent que tout le trafic sortant passe par un proxy sortant, sans exception.</span><span class="sxs-lookup"><span data-stu-id="30cf4-133">Some environments require all outbound traffic to go through an outbound proxy, without exception.</span></span> <span data-ttu-id="30cf4-134">Par conséquent, le contournement du serveur proxy n’est pas une option.</span><span class="sxs-lookup"><span data-stu-id="30cf4-134">As a result, bypassing the proxy is not an option.</span></span>

<span data-ttu-id="30cf4-135">Vous pouvez configurer le trafic du connecteur pour passer par le serveur proxy sortant comme indiqué dans le diagramme suivant :</span><span class="sxs-lookup"><span data-stu-id="30cf4-135">You can configure the connector traffic to go through the outbound proxy, as shown in the following diagram:</span></span>

 ![Configuration du trafic de connecteur pour passer par un proxy sortant vers un proxy d’application Azure AD](./media/application-proxy-working-with-proxy-servers/configure-proxy-settings.png)

<span data-ttu-id="30cf4-137">Conséquence de la présence seule de trafic sortant, il est inutile de configurer l’accès entrant à travers vos pare-feu.</span><span class="sxs-lookup"><span data-stu-id="30cf4-137">As a result of having only outbound traffic, there's no need to configure inbound access through your firewalls.</span></span>

### <a name="step-1-configure-the-connector-and-related-services-to-go-through-the-outbound-proxy"></a><span data-ttu-id="30cf4-138">Étape 1 : Configurer le connecteur et les services liés pour passer par le proxy sortant</span><span class="sxs-lookup"><span data-stu-id="30cf4-138">Step 1: Configure the connector and related services to go through the outbound proxy</span></span>

<span data-ttu-id="30cf4-139">Comme indiqué précédemment, si WPAD est activé dans l’environnement et correctement configuré, le connecteur détecte automatiquement le serveur proxy sortant et tente de l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="30cf4-139">As covered earlier, if WPAD is enabled in the environment and configured appropriately, the connector will automatically discover the outbound proxy server and attempt to use it.</span></span> <span data-ttu-id="30cf4-140">Toutefois, vous pouvez configurer explicitement le connecteur pour passer par un proxy sortant.</span><span class="sxs-lookup"><span data-stu-id="30cf4-140">However, you can explicitly configure the connector to go through an outbound proxy.</span></span>

<span data-ttu-id="30cf4-141">Pour ce faire, modifiez le fichier C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config et ajoutez la section *system.net* indiquée dans cet exemple de code.</span><span class="sxs-lookup"><span data-stu-id="30cf4-141">To do so, edit the C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add the *system.net* section shown in this code sample.</span></span> <span data-ttu-id="30cf4-142">Modifiez *proxyserver:8080* afin de refléter le nom de votre serveur proxy local ou l’adresse IP et le port qu’il écoute.</span><span class="sxs-lookup"><span data-stu-id="30cf4-142">Change *proxyserver:8080* to reflect your local proxy server name or IP address, and the port that it's listening on.</span></span>

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

<span data-ttu-id="30cf4-143">Configurez ensuite le service de mise à jour du connecteur pour utiliser le proxy en apportant une modification similaire au fichier situé dans C:\Program Files\Microsoft AAD App Proxy Connector Updater\ApplicationProxyConnectorUpdaterService.exe.config.</span><span class="sxs-lookup"><span data-stu-id="30cf4-143">Next, configure the Connector Updater service to use the proxy by making a similar change to the file located at C:\Program Files\Microsoft AAD App Proxy Connector Updater\ApplicationProxyConnectorUpdaterService.exe.config.</span></span>

### <a name="step-2-configure-the-proxy-to-allow-traffic-from-the-connector-and-related-services-to-flow-through"></a><span data-ttu-id="30cf4-144">Étape 2 : Configurer le serveur proxy pour autoriser le passage du trafic à partir du connecteur et des services connexes</span><span class="sxs-lookup"><span data-stu-id="30cf4-144">Step 2: Configure the proxy to allow traffic from the connector and related services to flow through</span></span>

<span data-ttu-id="30cf4-145">Il y a quatre aspects à prendre en compte au niveau du proxy sortant :</span><span class="sxs-lookup"><span data-stu-id="30cf4-145">There are four aspects to consider at the outbound proxy:</span></span>
* <span data-ttu-id="30cf4-146">Règles sortantes du proxy</span><span class="sxs-lookup"><span data-stu-id="30cf4-146">Proxy outbound rules</span></span>
* <span data-ttu-id="30cf4-147">Authentification du proxy</span><span class="sxs-lookup"><span data-stu-id="30cf4-147">Proxy authentication</span></span>
* <span data-ttu-id="30cf4-148">Ports du proxy</span><span class="sxs-lookup"><span data-stu-id="30cf4-148">Proxy ports</span></span>
* <span data-ttu-id="30cf4-149">Inspection SSL</span><span class="sxs-lookup"><span data-stu-id="30cf4-149">SSL inspection</span></span>

#### <a name="proxy-outbound-rules"></a><span data-ttu-id="30cf4-150">Règles sortantes du proxy</span><span class="sxs-lookup"><span data-stu-id="30cf4-150">Proxy outbound rules</span></span>
<span data-ttu-id="30cf4-151">Autorisez l’accès aux points de terminaison suivants pour l’accès au service de connecteur :</span><span class="sxs-lookup"><span data-stu-id="30cf4-151">Allow access to the following endpoints for connector service access:</span></span>

* <span data-ttu-id="30cf4-152">*.msappproxy.net</span><span class="sxs-lookup"><span data-stu-id="30cf4-152">*.msappproxy.net</span></span>
* <span data-ttu-id="30cf4-153">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="30cf4-153">*.servicebus.windows.net</span></span>

<span data-ttu-id="30cf4-154">Pour l’inscription initiale, autorisez l’accès aux points de terminaison suivants :</span><span class="sxs-lookup"><span data-stu-id="30cf4-154">For initial registration, allow access to the following endpoints:</span></span>

* <span data-ttu-id="30cf4-155">login.windows.net</span><span class="sxs-lookup"><span data-stu-id="30cf4-155">login.windows.net</span></span>
* <span data-ttu-id="30cf4-156">login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="30cf4-156">login.microsoftonline.com</span></span>

<span data-ttu-id="30cf4-157">Si vous ne pouvez pas autoriser la connectivité par le nom de domaine complet et devez spécifier des plages d’adresses IP à la place, utilisez ces options :</span><span class="sxs-lookup"><span data-stu-id="30cf4-157">If you can't allow connectivity by FQDN and need to specify IP ranges instead, use these options:</span></span>

* <span data-ttu-id="30cf4-158">Autoriser l’accès sortant du connecteur vers toutes les destinations.</span><span class="sxs-lookup"><span data-stu-id="30cf4-158">Allow the connector outbound access to all destinations.</span></span>
* <span data-ttu-id="30cf4-159">Autoriser l’accès sortant du connecteur vers des [plages d’adresses IP de centre de données Azure](https://www.microsoft.com/en-gb/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="30cf4-159">Allow the connector outbound access to [Azure datacenter IP ranges](https://www.microsoft.com/en-gb/download/details.aspx?id=41653).</span></span> <span data-ttu-id="30cf4-160">Le problème lié à l’utilisation de la liste de plages d’adresses IP de centre de données Azure est qu’elle est mise à jour chaque semaine.</span><span class="sxs-lookup"><span data-stu-id="30cf4-160">The challenge with using the list of Azure datacenter IP ranges is that it's updated weekly.</span></span> <span data-ttu-id="30cf4-161">Vous devez mettre un processus en place pour garantir que vos règles d’accès sont mises à jour en conséquence.</span><span class="sxs-lookup"><span data-stu-id="30cf4-161">You need to put a process in place to ensure that your access rules are updated accordingly.</span></span>

#### <a name="proxy-authentication"></a><span data-ttu-id="30cf4-162">Authentification du proxy</span><span class="sxs-lookup"><span data-stu-id="30cf4-162">Proxy authentication</span></span>

<span data-ttu-id="30cf4-163">L’authentification proxy n'est actuellement pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="30cf4-163">Proxy authentication is not currently supported.</span></span> <span data-ttu-id="30cf4-164">Notre recommandation actuelle est de permettre au connecteur d’accéder de façon anonyme aux destinations Internet.</span><span class="sxs-lookup"><span data-stu-id="30cf4-164">Our current recommendation is to allow the connector anonymous access to the Internet destinations.</span></span>

#### <a name="proxy-ports"></a><span data-ttu-id="30cf4-165">Ports du proxy</span><span class="sxs-lookup"><span data-stu-id="30cf4-165">Proxy ports</span></span>

<span data-ttu-id="30cf4-166">Le connecteur établit les connexions sortantes SSL à l’aide de la méthode CONNECT.</span><span class="sxs-lookup"><span data-stu-id="30cf4-166">The connector makes outbound SSL-based connections by using the CONNECT method.</span></span> <span data-ttu-id="30cf4-167">Cette méthode sert à définir un tunnel via le serveur proxy sortant.</span><span class="sxs-lookup"><span data-stu-id="30cf4-167">This method essentially sets up a tunnel through the outbound proxy.</span></span> <span data-ttu-id="30cf4-168">Configurez le serveur proxy pour autoriser le tunneling vers les ports 443 et 80.</span><span class="sxs-lookup"><span data-stu-id="30cf4-168">Configure the proxy server to allow tunneling to ports 443 and 80.</span></span>

>[!NOTE]
><span data-ttu-id="30cf4-169">Lorsque Service Bus s’exécute via le protocole HTTPS, il utilise le port 443.</span><span class="sxs-lookup"><span data-stu-id="30cf4-169">When Service Bus runs over HTTPS, it uses port 443.</span></span> <span data-ttu-id="30cf4-170">Toutefois, par défaut, Service Bus tente des connexions TCP directes et bascule sur HTTPS uniquement si la connectivité directe échoue.</span><span class="sxs-lookup"><span data-stu-id="30cf4-170">However, by default, Service Bus attempts direct TCP connections and falls back to HTTPS only if direct connectivity fails.</span></span>

<span data-ttu-id="30cf4-171">Pour vous assurer que le trafic Service Bus est également envoyé via le serveur proxy sortant, assurez-vous que le connecteur ne peut pas se connecter directement aux services Azure pour les ports 9350, 9352 et 5671.</span><span class="sxs-lookup"><span data-stu-id="30cf4-171">To ensure that the Service Bus traffic is also sent through the outbound proxy server, ensure that the connector cannot directly connect to the Azure services for ports 9350, 9352, and 5671.</span></span>

#### <a name="ssl-inspection"></a><span data-ttu-id="30cf4-172">Inspection SSL</span><span class="sxs-lookup"><span data-stu-id="30cf4-172">SSL inspection</span></span>
<span data-ttu-id="30cf4-173">N’utilisez pas l’inspection SSL pour le trafic de connecteur, car cela entraîne des problèmes pour le trafic du connecteur.</span><span class="sxs-lookup"><span data-stu-id="30cf4-173">Do not use SSL inspection for the connector traffic, because it causes problems for the connector traffic.</span></span>

## <a name="troubleshoot-connector-proxy-problems-and-service-connectivity-issues"></a><span data-ttu-id="30cf4-174">Résoudre les problèmes courants de proxy de connecteur et de connectivité du service</span><span class="sxs-lookup"><span data-stu-id="30cf4-174">Troubleshoot connector proxy problems and service connectivity issues</span></span>
<span data-ttu-id="30cf4-175">Vous devriez maintenant voir tout le trafic transitant par le proxy.</span><span class="sxs-lookup"><span data-stu-id="30cf4-175">Now you should see all traffic flowing through the proxy.</span></span> <span data-ttu-id="30cf4-176">Si vous rencontrez des problèmes, les informations de résolution des problèmes suivantes devraient vous aider.</span><span class="sxs-lookup"><span data-stu-id="30cf4-176">If you have problems, the following troubleshooting information should help.</span></span>

<span data-ttu-id="30cf4-177">Le meilleur moyen d’identifier et de résoudre les problèmes de connectivité de connecteur consiste à prendre une capture réseau sur le service de connecteur au démarrage de ce dernier.</span><span class="sxs-lookup"><span data-stu-id="30cf4-177">The best way to identify and troubleshoot connector connectivity issues is to take a network capture on the connector service while starting the connector service.</span></span> <span data-ttu-id="30cf4-178">Cela peut être une tâche ardue, aussi examinons quelques conseils rapides sur la capture et le filtrage des traces réseau.</span><span class="sxs-lookup"><span data-stu-id="30cf4-178">This can be a daunting task, so let’s look at quick tips on capturing and filtering network traces.</span></span>

<span data-ttu-id="30cf4-179">Vous pouvez utiliser l’outil de surveillance de votre choix.</span><span class="sxs-lookup"><span data-stu-id="30cf4-179">You can use the monitoring tool of your choice.</span></span> <span data-ttu-id="30cf4-180">Dans le cadre de cet article, nous avons utilisé Microsoft Network Monitor 3.4.</span><span class="sxs-lookup"><span data-stu-id="30cf4-180">For the purposes of this article, we used Microsoft Network Monitor 3.4.</span></span> <span data-ttu-id="30cf4-181">Vous pouvez [le télécharger à partir de Microsoft](https://www.microsoft.com/download/details.aspx?id=4865).</span><span class="sxs-lookup"><span data-stu-id="30cf4-181">You can [download it from Microsoft](https://www.microsoft.com/download/details.aspx?id=4865).</span></span>

<span data-ttu-id="30cf4-182">Les exemples et les filtres que nous utilisons dans les sections suivantes sont spécifiques à Network Monitor, mais les principes peuvent être appliqués à n’importe quel outil d’analyse.</span><span class="sxs-lookup"><span data-stu-id="30cf4-182">The examples and filters that we use in the following sections are specific to Network Monitor, but the principles can be applied to any analysis tool.</span></span>

### <a name="take-a-capture-by-using-network-monitor"></a><span data-ttu-id="30cf4-183">Prendre une capture à l’aide de Network Monitor</span><span class="sxs-lookup"><span data-stu-id="30cf4-183">Take a capture by using Network Monitor</span></span>

<span data-ttu-id="30cf4-184">Pour démarrer une capture :</span><span class="sxs-lookup"><span data-stu-id="30cf4-184">To start a capture:</span></span>

1. <span data-ttu-id="30cf4-185">Ouvrez Network Monitor, puis cliquez sur **Nouvelle capture**.</span><span class="sxs-lookup"><span data-stu-id="30cf4-185">Open Network Monitor and click **New Capture**.</span></span>
2. <span data-ttu-id="30cf4-186">Cliquez sur le bouton **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="30cf4-186">Click the **Start** button.</span></span>

   ![Fenêtre de Network Monitor](./media/application-proxy-working-with-proxy-servers/network-capture.png)

<span data-ttu-id="30cf4-188">Lorsque vous avez terminé une capture, cliquez sur le bouton **Arrêter** pour l’arrêter.</span><span class="sxs-lookup"><span data-stu-id="30cf4-188">After you complete a capture, click the **Stop** button to end it.</span></span>

### <a name="take-a-capture-of-connector-traffic"></a><span data-ttu-id="30cf4-189">Effectuez une capture du trafic de connecteur</span><span class="sxs-lookup"><span data-stu-id="30cf4-189">Take a capture of connector traffic</span></span>

<span data-ttu-id="30cf4-190">Pour commencer la résolution des problèmes, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="30cf4-190">For initial troubleshooting, perform the following steps:</span></span>

1. <span data-ttu-id="30cf4-191">À partir de services.msc, arrêtez le service de connecteur de proxy d’application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="30cf4-191">From services.msc, stop the Azure AD Application Proxy Connector service.</span></span>
2. <span data-ttu-id="30cf4-192">Démarrez la capture réseau.</span><span class="sxs-lookup"><span data-stu-id="30cf4-192">Start the network capture.</span></span>
3. <span data-ttu-id="30cf4-193">Démarrez le service de connecteur de proxy d’application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="30cf4-193">Start the Azure AD Application Proxy Connector service.</span></span>
4. <span data-ttu-id="30cf4-194">Arrêtez la capture réseau.</span><span class="sxs-lookup"><span data-stu-id="30cf4-194">Stop the network capture.</span></span>

   ![Service de connecteur de proxy d’application Azure AD dans services.msc](./media/application-proxy-working-with-proxy-servers/services-local.png)

### <a name="look-at-the-requests-from-the-connector-to-the-proxy-server"></a><span data-ttu-id="30cf4-196">Examiner les requêtes du connecteur au serveur proxy</span><span class="sxs-lookup"><span data-stu-id="30cf4-196">Look at the requests from the connector to the proxy server</span></span>

<span data-ttu-id="30cf4-197">Maintenant que vous avez une capture réseau, vous pouvez la filtrer.</span><span class="sxs-lookup"><span data-stu-id="30cf4-197">Now that you’ve got a network capture, you're ready to filter it.</span></span> <span data-ttu-id="30cf4-198">La clé de l’analyse de la trace est de comprendre comment filtrer la capture.</span><span class="sxs-lookup"><span data-stu-id="30cf4-198">The key to looking at the trace is understanding how to filter the capture.</span></span>

<span data-ttu-id="30cf4-199">Voici un filtre (où 8080 est le port du service proxy) :</span><span class="sxs-lookup"><span data-stu-id="30cf4-199">One filter is as follows (where 8080 is the proxy service port):</span></span>

<span data-ttu-id="30cf4-200">**(http.Request or http.Response) and tcp.port==8080**</span><span class="sxs-lookup"><span data-stu-id="30cf4-200">**(http.Request or http.Response) and tcp.port==8080**</span></span>

<span data-ttu-id="30cf4-201">Si vous entrez ce filtre dans la fenêtre de **filtre d’affichage** et sélectionnez **Appliquer**, le trafic capturé est filtré en fonction du filtre.</span><span class="sxs-lookup"><span data-stu-id="30cf4-201">If you enter this filter in the **Display Filter** window and select **Apply**, it filters the captured traffic based on the filter.</span></span>

<span data-ttu-id="30cf4-202">Le filtre précédent affiche uniquement les requêtes et réponses HTTP vers/depuis le port du proxy.</span><span class="sxs-lookup"><span data-stu-id="30cf4-202">The preceding filter shows just the HTTP requests and responses to/from the proxy port.</span></span> <span data-ttu-id="30cf4-203">Pour un démarrage de connecteur sur lequel le connecteur est configuré pour utiliser un serveur proxy, ce filtre ressemblerait à ceci :</span><span class="sxs-lookup"><span data-stu-id="30cf4-203">For a connector startup where the connector is configured to use a proxy server, the filter would show something like this:</span></span>

 ![Exemple de liste de requêtes et réponses HTTP filtrées](./media/application-proxy-working-with-proxy-servers/http-requests.png)

<span data-ttu-id="30cf4-205">Vous recherchez maintenant spécifiquement les requêtes CONNECT indiquant une communication avec le serveur proxy.</span><span class="sxs-lookup"><span data-stu-id="30cf4-205">You're now specifically looking for the CONNECT requests that show communication with the proxy server.</span></span> <span data-ttu-id="30cf4-206">En cas de succès, vous obtenez une réponse HTTP OK (200).</span><span class="sxs-lookup"><span data-stu-id="30cf4-206">Upon success, you get an HTTP OK (200) response.</span></span>

<span data-ttu-id="30cf4-207">Si vous voyez d’autres codes de réponse, comme 407 ou 502, le proxy nécessite une authentification ou n’autorise pas le trafic pour une raison quelconque.</span><span class="sxs-lookup"><span data-stu-id="30cf4-207">If you see other response codes, such as 407 or 502, the proxy is requiring authentication or not allowing the traffic for some other reason.</span></span> <span data-ttu-id="30cf4-208">À ce stade, vous impliquez l’équipe de support technique de votre serveur proxy.</span><span class="sxs-lookup"><span data-stu-id="30cf4-208">At this point, you engage your proxy server support team.</span></span>

### <a name="identify-failed-tcp-connection-attempts"></a><span data-ttu-id="30cf4-209">Identifier les tentatives de connexion TCP ayant échoué</span><span class="sxs-lookup"><span data-stu-id="30cf4-209">Identify failed TCP connection attempts</span></span>

<span data-ttu-id="30cf4-210">L’autre scénario courant qui peut vous intéresser est lorsque le connecteur essaie de se connecter directement, mais qu’il échoue.</span><span class="sxs-lookup"><span data-stu-id="30cf4-210">The other common scenario that you may be interested in is when the connector is trying to connect directly, but it's failing.</span></span>

<span data-ttu-id="30cf4-211">Voici un autre filtre Network Monitor qui vous permet d’identifier facilement ce problème :</span><span class="sxs-lookup"><span data-stu-id="30cf4-211">Another Network Monitor filter that helps you to easily identify this problem is:</span></span>

<span data-ttu-id="30cf4-212">**property.TCPSynRetransmit**</span><span class="sxs-lookup"><span data-stu-id="30cf4-212">**property.TCPSynRetransmit**</span></span>

<span data-ttu-id="30cf4-213">Un paquet SYN est le premier paquet envoyé pour établir une connexion TCP.</span><span class="sxs-lookup"><span data-stu-id="30cf4-213">A SYN packet is the first packet sent to establish a TCP connection.</span></span> <span data-ttu-id="30cf4-214">Si ce paquet ne renvoie aucune réponse, le SYN est renvoyé.</span><span class="sxs-lookup"><span data-stu-id="30cf4-214">If this packet doesn’t return a response, the SYN is reattempted.</span></span> <span data-ttu-id="30cf4-215">Vous pouvez utiliser le filtre précédent pour voir les SYN retransmis.</span><span class="sxs-lookup"><span data-stu-id="30cf4-215">You can use the preceding filter to see any retransmitted SYNs.</span></span> <span data-ttu-id="30cf4-216">Ensuite, vous pouvez vérifiez si ces SYN correspondent à du trafic lié à un connecteur.</span><span class="sxs-lookup"><span data-stu-id="30cf4-216">Then, you can check whether these SYNs correspond to any connector-related traffic.</span></span>

<span data-ttu-id="30cf4-217">L’exemple suivant montre une tentative de connexion ayant échoué pour le port de Service Bus 9352 :</span><span class="sxs-lookup"><span data-stu-id="30cf4-217">The following example shows a failed connection attempt to Service Bus port 9352:</span></span>

 ![Exemple de réponse à une tentative de connexion ayant échoué](./media/application-proxy-working-with-proxy-servers/failed-connection-attempt.png)

<span data-ttu-id="30cf4-219">Si vous voyez quelque chose comme la réponse précédente, le connecteur tente de communiquer directement avec le service Service Bus d’Azure.</span><span class="sxs-lookup"><span data-stu-id="30cf4-219">If you see something like the preceding response, the connector is trying to communicate directly with the Azure Service Bus service.</span></span> <span data-ttu-id="30cf4-220">Si vous vous attendez à ce que le connecteur établisse des connexions directes avec les services Azure, cette réponse est une indication claire que vous avez un problème de réseau ou de pare-feu.</span><span class="sxs-lookup"><span data-stu-id="30cf4-220">If you expect the connector to make direct connections to the Azure services, this response is a clear indication that you have a network or firewall problem.</span></span>

>[!NOTE]
><span data-ttu-id="30cf4-221">Si vous avez effectué la configuration de sorte à utiliser un serveur proxy, cette réponse peut indiquer que Service Bus tente une connexion TCP directe avant de tenter de se connecter via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="30cf4-221">If you are configured to use a proxy server, this response might mean that Service Bus is attempting a direct TCP connection before switching to attempting a connection over HTTPS.</span></span>
>

<span data-ttu-id="30cf4-222">L’analyse des traces réseau n’est pas faite pour tout le monde.</span><span class="sxs-lookup"><span data-stu-id="30cf4-222">Network trace analysis is not for everyone.</span></span> <span data-ttu-id="30cf4-223">Mais il peut s’agir d’un outil précieux pour obtenir rapidement des informations sur ce qui se passe avec votre réseau.</span><span class="sxs-lookup"><span data-stu-id="30cf4-223">But it can be a valuable tool to get quick information about what's going on with your network.</span></span>

<span data-ttu-id="30cf4-224">Si vous continuez à rencontrer des problèmes de connectivité avec le connecteur, créez un ticket auprès de notre équipe de support technique.</span><span class="sxs-lookup"><span data-stu-id="30cf4-224">If you continue to struggle with connector connectivity issues, create a ticket with our support team.</span></span> <span data-ttu-id="30cf4-225">L’équipe peut vous aider dans la suite de la résolution des problèmes.</span><span class="sxs-lookup"><span data-stu-id="30cf4-225">The team can assist you with further troubleshooting.</span></span>

<span data-ttu-id="30cf4-226">Pour plus d’informations sur la résolution des erreurs avec le connecteur de proxy d’application, consultez [Résoudre les problèmes du proxy d’application](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).</span><span class="sxs-lookup"><span data-stu-id="30cf4-226">For information about resolving errors with Application Proxy Connector, see [Troubleshoot Application Proxy](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).</span></span>

## <a name="next-steps"></a><span data-ttu-id="30cf4-227">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="30cf4-227">Next steps</span></span>

[<span data-ttu-id="30cf4-228">Présentation des connecteurs de proxy d’application Azure AD</span><span class="sxs-lookup"><span data-stu-id="30cf4-228">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)<br><span data-ttu-id="30cf4-229">
[Comment installer silencieusement le connecteur du Proxy d'application Azure AD](active-directory-application-proxy-silent-installation.md)</span><span class="sxs-lookup"><span data-stu-id="30cf4-229">
[How to silently install the Azure AD Application Proxy Connector ](active-directory-application-proxy-silent-installation.md)</span></span>
