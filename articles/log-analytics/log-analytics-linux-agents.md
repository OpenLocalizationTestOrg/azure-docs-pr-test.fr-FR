---
redirect_url: /azure/log-analytics/log-analytics-agent-linux
redirect_document_id: TRUE
ROBOTS: NOINDEX
ms.openlocfilehash: 8332bdd39effab8c2ac9a75ca9a1e2510c940719
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-your-linux-computers-to-log-analytics"></a><span data-ttu-id="645e3-101">Connecter vos ordinateurs Linux à Log Analytics</span><span class="sxs-lookup"><span data-stu-id="645e3-101">Connect your Linux computers to Log Analytics</span></span>
<span data-ttu-id="645e3-102">Avec Log Analytics, vous pouvez collecter et exploiter les données générées par des ordinateurs Linux.</span><span class="sxs-lookup"><span data-stu-id="645e3-102">Using Log Analytics, you can collect and act on data generated from Linux computers.</span></span> <span data-ttu-id="645e3-103">L’ajout de données collectées sur Linux dans OMS vous permet de gérer les systèmes Linux et les solutions de conteneur comme Docker, indépendamment de l’emplacement de vos ordinateurs.</span><span class="sxs-lookup"><span data-stu-id="645e3-103">Adding data collected from Linux to OMS allows you to manage Linux systems and container solutions like Docker, regardless of where your computers are located — virtually anywhere.</span></span> <span data-ttu-id="645e3-104">Les sources de données peuvent résider sur des serveurs physiques de votre centre de données local, sur des ordinateurs virtuels dans un service hébergé sur le cloud comme Amazon Web Services (AWS) ou Microsoft Azure, voire sur votre ordinateur portable.</span><span class="sxs-lookup"><span data-stu-id="645e3-104">Data sources might reside in your on-premises datacenter as physical servers, virtual computers in a cloud-hosted service like Amazon Web Services (AWS) or Microsoft Azure, or even the laptop on your desk.</span></span> <span data-ttu-id="645e3-105">De plus, OMS collecte les données des ordinateurs Windows de la même façon, prenant en charge un véritable environnement informatique hybride.</span><span class="sxs-lookup"><span data-stu-id="645e3-105">In addition, OMS also collects data from Windows computers similarly, so it supports a truly hybrid IT environment.</span></span>

<span data-ttu-id="645e3-106">Vous pouvez afficher et gérer les données de toutes ces sources avec Log Analytics dans OMS, via un portail unique.</span><span class="sxs-lookup"><span data-stu-id="645e3-106">You can view and manage data from all of those sources with Log Analytics in OMS with a single management portal.</span></span> <span data-ttu-id="645e3-107">Plus besoin de multiplier les systèmes de surveillance des données. De plus, vous pouvez exporter toutes les données que vous souhaitez vers la solution ou le système d’analyse marketing dont vous disposez.</span><span class="sxs-lookup"><span data-stu-id="645e3-107">This reduces the need to monitor it using many different systems, makes it easy to consume, and you can export any data you like to whatever business analytics solution or system that you already have.</span></span>

<span data-ttu-id="645e3-108">Cet article est un guide de démarrage rapide qui vous aide à collecter et gérer les données de vos ordinateurs Linux à l’aide de l’Agent OMS pour Linux.</span><span class="sxs-lookup"><span data-stu-id="645e3-108">This article is a quick start guide that will help you collect and manage data for your Linux computers using the OMS Agent for Linux.</span></span> <span data-ttu-id="645e3-109">Pour obtenir des détails plus techniques, tels que la configuration du serveur proxy, des informations sur les mesures CollectD, et des sources de données JSON personnalisées, consultez la [présentation de l’Agent OMS pour Linux](https://github.com/Microsoft/OMS-Agent-for-Linux) (en anglais) et la [documentation complète de l’Agent OMS pour Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md) (en anglais) sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="645e3-109">For more technical details such as proxy server configuration, information about CollectD metrics, and custom JSON data sources, you’ll find that information at [OMS Agent for Linux overview](https://github.com/Microsoft/OMS-Agent-for-Linux) and [OMS Agent for Linux full documentation](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md) on GitHub.</span></span>

<span data-ttu-id="645e3-110">Pour l’instant, vous pouvez collecter les types de données suivants sur des ordinateurs Linux :</span><span class="sxs-lookup"><span data-stu-id="645e3-110">Currently, you can collect the following types of data from Linux computers:</span></span>

* <span data-ttu-id="645e3-111">Mesures de performances</span><span class="sxs-lookup"><span data-stu-id="645e3-111">Performance metrics</span></span>
* <span data-ttu-id="645e3-112">Événements Syslog</span><span class="sxs-lookup"><span data-stu-id="645e3-112">Syslog events</span></span>
* <span data-ttu-id="645e3-113">Alertes de Nagios et Zabbix</span><span class="sxs-lookup"><span data-stu-id="645e3-113">Alerts from Nagios and Zabbix</span></span>
* <span data-ttu-id="645e3-114">Journaux, inventaire et mesures de performances du conteneur Docker</span><span class="sxs-lookup"><span data-stu-id="645e3-114">Docker container performance metrics, inventory and logs</span></span>

## <a name="supported-linux-versions"></a><span data-ttu-id="645e3-115">Versions de Linux prises en charge</span><span class="sxs-lookup"><span data-stu-id="645e3-115">Supported Linux versions</span></span>
<span data-ttu-id="645e3-116">Les versions x86 et x64 sont officiellement prises en charge sur diverses distributions de Linux.</span><span class="sxs-lookup"><span data-stu-id="645e3-116">Both x86 and x64 versions are officially supported on a variety of Linux distributions.</span></span> <span data-ttu-id="645e3-117">Toutefois, l’Agent OMS pour Linux peut également s’exécuter dans d’autres distributions non répertoriées.</span><span class="sxs-lookup"><span data-stu-id="645e3-117">However, the OMS Agent for Linux might also run on other distributions not listed.</span></span>

* <span data-ttu-id="645e3-118">Amazon Linux 2012.09 à 2015.09</span><span class="sxs-lookup"><span data-stu-id="645e3-118">Amazon Linux 2012.09 through 2015.09</span></span>
* <span data-ttu-id="645e3-119">CentOS Linux 5, 6 et 7</span><span class="sxs-lookup"><span data-stu-id="645e3-119">CentOS Linux 5, 6, and 7</span></span>
* <span data-ttu-id="645e3-120">Oracle Linux 5, 6 et 7</span><span class="sxs-lookup"><span data-stu-id="645e3-120">Oracle Linux 5, 6, and 7</span></span>
* <span data-ttu-id="645e3-121">Red Hat Enterprise Linux Server 5, 6 et 7</span><span class="sxs-lookup"><span data-stu-id="645e3-121">Red Hat Enterprise Linux Server 5, 6 and 7</span></span>
* <span data-ttu-id="645e3-122">Debian GNU/Linux 6, 7 et 8</span><span class="sxs-lookup"><span data-stu-id="645e3-122">Debian GNU/Linux 6, 7, and 8</span></span>
* <span data-ttu-id="645e3-123">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10</span><span class="sxs-lookup"><span data-stu-id="645e3-123">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10</span></span>
* <span data-ttu-id="645e3-124">SUSE Linux Enterprise Server 11 et 12</span><span class="sxs-lookup"><span data-stu-id="645e3-124">SUSE Linux Enterprise Server 11 and 12</span></span>

## <a name="oms-agent-for-linux"></a><span data-ttu-id="645e3-125">Agent OMS pour Linux</span><span class="sxs-lookup"><span data-stu-id="645e3-125">OMS Agent for Linux</span></span>
<span data-ttu-id="645e3-126">L’Agent Operations Management Suite pour Linux comprend plusieurs packages.</span><span class="sxs-lookup"><span data-stu-id="645e3-126">The Operations Management Suite Agent for Linux comprises multiple packages.</span></span> <span data-ttu-id="645e3-127">Les packages suivants sont disponibles en exécutant l’application shell avec `--extract`.</span><span class="sxs-lookup"><span data-stu-id="645e3-127">The release file contains the following packages, available by running the shell bundle with `--extract`.</span></span>

| <span data-ttu-id="645e3-128">**Package**</span><span class="sxs-lookup"><span data-stu-id="645e3-128">**Package**</span></span> | <span data-ttu-id="645e3-129">**Version**</span><span class="sxs-lookup"><span data-stu-id="645e3-129">**Version**</span></span> | <span data-ttu-id="645e3-130">**Description**</span><span class="sxs-lookup"><span data-stu-id="645e3-130">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="645e3-131">omsagent</span><span class="sxs-lookup"><span data-stu-id="645e3-131">omsagent</span></span> |<span data-ttu-id="645e3-132">1.1.0</span><span class="sxs-lookup"><span data-stu-id="645e3-132">1.1.0</span></span> |<span data-ttu-id="645e3-133">Agent Operations Management Suite pour Linux</span><span class="sxs-lookup"><span data-stu-id="645e3-133">The Operations Management Suite Agent for Linux</span></span> |
| <span data-ttu-id="645e3-134">omsconfig</span><span class="sxs-lookup"><span data-stu-id="645e3-134">omsconfig</span></span> |<span data-ttu-id="645e3-135">1.1.1</span><span class="sxs-lookup"><span data-stu-id="645e3-135">1.1.1</span></span> |<span data-ttu-id="645e3-136">Agent de configuration de l’Agent OMS</span><span class="sxs-lookup"><span data-stu-id="645e3-136">Configuration agent for the OMS Agent</span></span> |
| <span data-ttu-id="645e3-137">omi</span><span class="sxs-lookup"><span data-stu-id="645e3-137">omi</span></span> |<span data-ttu-id="645e3-138">1.0.8.3</span><span class="sxs-lookup"><span data-stu-id="645e3-138">1.0.8.3</span></span> |<span data-ttu-id="645e3-139">Open Management Infrastructure (OMI) - Serveur CIM léger</span><span class="sxs-lookup"><span data-stu-id="645e3-139">Open Management Infrastructure (OMI) -- a lightweight CIM Server</span></span> |
| <span data-ttu-id="645e3-140">scx</span><span class="sxs-lookup"><span data-stu-id="645e3-140">scx</span></span> |<span data-ttu-id="645e3-141">1.6.2</span><span class="sxs-lookup"><span data-stu-id="645e3-141">1.6.2</span></span> |<span data-ttu-id="645e3-142">Fournisseurs CIM OMI pour les mesures de performances des systèmes d’exploitation</span><span class="sxs-lookup"><span data-stu-id="645e3-142">OMI CIM Providers for operating system performance metrics</span></span> |
| <span data-ttu-id="645e3-143">apache-cimprov</span><span class="sxs-lookup"><span data-stu-id="645e3-143">apache-cimprov</span></span> |<span data-ttu-id="645e3-144">1.0.0</span><span class="sxs-lookup"><span data-stu-id="645e3-144">1.0.0</span></span> |<span data-ttu-id="645e3-145">Fournisseur de surveillance des performances d’Apache HTTP Server pour OMI.</span><span class="sxs-lookup"><span data-stu-id="645e3-145">Apache HTTP Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="645e3-146">Installé uniquement si Apache HTTP Server est détecté.</span><span class="sxs-lookup"><span data-stu-id="645e3-146">Only installed if Apache HTTP Server is detected.</span></span> |
| <span data-ttu-id="645e3-147">mysql-cimprov</span><span class="sxs-lookup"><span data-stu-id="645e3-147">mysql-cimprov</span></span> |<span data-ttu-id="645e3-148">1.0.0</span><span class="sxs-lookup"><span data-stu-id="645e3-148">1.0.0</span></span> |<span data-ttu-id="645e3-149">Fournisseur de surveillance des performances de MySQL Server pour OMI.</span><span class="sxs-lookup"><span data-stu-id="645e3-149">MySQL Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="645e3-150">Installé uniquement si MySQL/MariaDB Server est détecté.</span><span class="sxs-lookup"><span data-stu-id="645e3-150">Only installed if MySQL/MariaDB server is detected.</span></span> |
| <span data-ttu-id="645e3-151">docker-cimprov</span><span class="sxs-lookup"><span data-stu-id="645e3-151">docker-cimprov</span></span> |<span data-ttu-id="645e3-152">0.1.0</span><span class="sxs-lookup"><span data-stu-id="645e3-152">0.1.0</span></span> |<span data-ttu-id="645e3-153">Fournisseur de Docker pour OMI.</span><span class="sxs-lookup"><span data-stu-id="645e3-153">Docker provider for OMI.</span></span> <span data-ttu-id="645e3-154">Installé uniquement si Docker est détecté.</span><span class="sxs-lookup"><span data-stu-id="645e3-154">Only installed if Docker is detected.</span></span> |

### <a name="additional-installation-artifacts"></a><span data-ttu-id="645e3-155">Artefacts d’installation supplémentaires</span><span class="sxs-lookup"><span data-stu-id="645e3-155">Additional installation artifacts</span></span>
<span data-ttu-id="645e3-156">Après avoir installé les packages de l’Agent OMS pour Linux, les modifications de configuration système suivantes sont appliquées.</span><span class="sxs-lookup"><span data-stu-id="645e3-156">After installing the OMS agent for Linux packages, the following additional system-wide configuration changes are applied.</span></span> <span data-ttu-id="645e3-157">Ces artefacts sont supprimés lorsque le package omsagent est désinstallé.</span><span class="sxs-lookup"><span data-stu-id="645e3-157">These artifacts are removed when the omsagent package is uninstalled.</span></span>

* <span data-ttu-id="645e3-158">Un utilisateur sans privilège nommé `omsagent` est créé.</span><span class="sxs-lookup"><span data-stu-id="645e3-158">A non-privileged user named: `omsagent` is created.</span></span> <span data-ttu-id="645e3-159">Il s’agit du compte utilisé par le démon omsagent pour s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="645e3-159">This is the account the omsagent daemon runs as</span></span>
* <span data-ttu-id="645e3-160">Un fichier « include » sudoers est créé à l’emplacement /etc/sudoers.d/omsagent. Il autorise omsagent à redémarrer les démons syslog et omsagent.</span><span class="sxs-lookup"><span data-stu-id="645e3-160">A sudoers “include” file is created at /etc/sudoers.d/omsagent This authorizes omsagent to restart the syslog and omsagent daemons.</span></span> <span data-ttu-id="645e3-161">Si les directives « include » sudo ne sont pas prises en charge dans la version installée de sudo, ces entrées sont inscrites dans /etc/sudoers.</span><span class="sxs-lookup"><span data-stu-id="645e3-161">If sudo “include” directives are not supported in the installed version of sudo, these entries will be written to /etc/sudoers.</span></span>
* <span data-ttu-id="645e3-162">La configuration de syslog est modifiée pour transférer un sous-ensemble d’événements à l’agent.</span><span class="sxs-lookup"><span data-stu-id="645e3-162">The syslog configuration is modified to forward a subset of events to the agent.</span></span> <span data-ttu-id="645e3-163">Pour plus d’informations, consultez la section **Configuration de la collecte des données** ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="645e3-163">For more information, see the **Configuring Data Collection** section below</span></span>

### <a name="linux-data-collection-details"></a><span data-ttu-id="645e3-164">Détails sur la collecte de données Linux</span><span class="sxs-lookup"><span data-stu-id="645e3-164">Linux data collection details</span></span>
<span data-ttu-id="645e3-165">Le tableau suivant présente les méthodes de collecte des données et d’autres informations sur le mode de collecte.</span><span class="sxs-lookup"><span data-stu-id="645e3-165">The following table shows data collection methods and other details about how data is collected.</span></span>

| <span data-ttu-id="645e3-166">source</span><span class="sxs-lookup"><span data-stu-id="645e3-166">source</span></span> | <span data-ttu-id="645e3-167">Agent direct</span><span class="sxs-lookup"><span data-stu-id="645e3-167">Direct Agent</span></span> | <span data-ttu-id="645e3-168">Agent SCOM</span><span class="sxs-lookup"><span data-stu-id="645e3-168">SCOM agent</span></span> | <span data-ttu-id="645e3-169">Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="645e3-169">Azure Storage</span></span> | <span data-ttu-id="645e3-170">SCOM requis ?</span><span class="sxs-lookup"><span data-stu-id="645e3-170">SCOM required?</span></span> | <span data-ttu-id="645e3-171">Données de l’agent SCOM envoyées via un groupe d’administration</span><span class="sxs-lookup"><span data-stu-id="645e3-171">SCOM agent data sent via management group</span></span> | <span data-ttu-id="645e3-172">Fréquence de collecte</span><span class="sxs-lookup"><span data-stu-id="645e3-172">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="645e3-173">Zabbix</span><span class="sxs-lookup"><span data-stu-id="645e3-173">Zabbix</span></span> |![Oui](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="645e3-179">1 minute</span><span class="sxs-lookup"><span data-stu-id="645e3-179">1 minute</span></span> |
| <span data-ttu-id="645e3-180">Nagios</span><span class="sxs-lookup"><span data-stu-id="645e3-180">Nagios</span></span> |![Oui](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="645e3-186">À l’arrivée</span><span class="sxs-lookup"><span data-stu-id="645e3-186">on arrival</span></span> |
| <span data-ttu-id="645e3-187">syslog</span><span class="sxs-lookup"><span data-stu-id="645e3-187">syslog</span></span> |![Oui](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="645e3-193">Depuis Azure Storage : 10 minutes ; depuis l’agent : à l’arrivée</span><span class="sxs-lookup"><span data-stu-id="645e3-193">from Azure storage: 10 minutes; from agent: on arrival</span></span> |
| <span data-ttu-id="645e3-194">Compteurs de performances Linux</span><span class="sxs-lookup"><span data-stu-id="645e3-194">Linux performance counters</span></span> |![Oui](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="645e3-200">Comme prévu, minimum de 10 secondes</span><span class="sxs-lookup"><span data-stu-id="645e3-200">As scheduled, minimum of 10 seconds</span></span> |
| <span data-ttu-id="645e3-201">Suivi des modifications</span><span class="sxs-lookup"><span data-stu-id="645e3-201">change tracking</span></span> |![Oui](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="645e3-207">Toutes les heures</span><span class="sxs-lookup"><span data-stu-id="645e3-207">hourly</span></span> |

### <a name="package-requirements"></a><span data-ttu-id="645e3-208">Packages requis</span><span class="sxs-lookup"><span data-stu-id="645e3-208">Package Requirements</span></span>
| <span data-ttu-id="645e3-209">**Package requis**</span><span class="sxs-lookup"><span data-stu-id="645e3-209">**Required package**</span></span> | <span data-ttu-id="645e3-210">**Description**</span><span class="sxs-lookup"><span data-stu-id="645e3-210">**Description**</span></span> | <span data-ttu-id="645e3-211">**Version minimum**</span><span class="sxs-lookup"><span data-stu-id="645e3-211">**Minimum version**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="645e3-212">Glibc</span><span class="sxs-lookup"><span data-stu-id="645e3-212">Glibc</span></span> |<span data-ttu-id="645e3-213">Bibliothèque C de GNU</span><span class="sxs-lookup"><span data-stu-id="645e3-213">GNU C library</span></span> |<span data-ttu-id="645e3-214">2.5-12</span><span class="sxs-lookup"><span data-stu-id="645e3-214">2.5-12</span></span> |
| <span data-ttu-id="645e3-215">Openssl</span><span class="sxs-lookup"><span data-stu-id="645e3-215">Openssl</span></span> |<span data-ttu-id="645e3-216">Bibliothèques OpenSSL</span><span class="sxs-lookup"><span data-stu-id="645e3-216">OpenSSL libraries</span></span> |<span data-ttu-id="645e3-217">0.9.8e ou 1.0</span><span class="sxs-lookup"><span data-stu-id="645e3-217">0.9.8e or 1.0</span></span> |
| <span data-ttu-id="645e3-218">Curl</span><span class="sxs-lookup"><span data-stu-id="645e3-218">Curl</span></span> |<span data-ttu-id="645e3-219">Client web cURL</span><span class="sxs-lookup"><span data-stu-id="645e3-219">cURL web client</span></span> |<span data-ttu-id="645e3-220">7.15.5</span><span class="sxs-lookup"><span data-stu-id="645e3-220">7.15.5</span></span> |
| <span data-ttu-id="645e3-221">Python-ctypes</span><span class="sxs-lookup"><span data-stu-id="645e3-221">Python-ctypes</span></span> |<span data-ttu-id="645e3-222">Bibliothèques de fonctions</span><span class="sxs-lookup"><span data-stu-id="645e3-222">function libraries</span></span> |<span data-ttu-id="645e3-223">n/a</span><span class="sxs-lookup"><span data-stu-id="645e3-223">n/a</span></span> |
| <span data-ttu-id="645e3-224">PAM</span><span class="sxs-lookup"><span data-stu-id="645e3-224">PAM</span></span> |<span data-ttu-id="645e3-225">Pluggable Authentication Modules</span><span class="sxs-lookup"><span data-stu-id="645e3-225">Pluggable authentication Modules</span></span> |<span data-ttu-id="645e3-226">n/a</span><span class="sxs-lookup"><span data-stu-id="645e3-226">n/a</span></span> |

> [!NOTE]
> <span data-ttu-id="645e3-227">rsyslog ou syslog-ng est requis pour collecter les messages syslog.</span><span class="sxs-lookup"><span data-stu-id="645e3-227">Either rsyslog or syslog-ng are required to collect syslog messages.</span></span> <span data-ttu-id="645e3-228">Le démon syslog par défaut sur la version 5 de Red Hat Enterprise Linux, CentOS et Oracle Linux (sysklog) ne prend pas en charge la collecte des événements syslog.</span><span class="sxs-lookup"><span data-stu-id="645e3-228">The default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="645e3-229">Pour collecter les données syslog avec cette version de ces distributions, le démon rsyslog doit être installé et configuré à la place de sysklog.</span><span class="sxs-lookup"><span data-stu-id="645e3-229">To collect syslog data from this version of these distributions, the rsyslog daemon should be installed and configured to replace sysklog.</span></span>
>
>

## <a name="quick-install"></a><span data-ttu-id="645e3-230">Installation rapide</span><span class="sxs-lookup"><span data-stu-id="645e3-230">Quick install</span></span>
<span data-ttu-id="645e3-231">Exécutez les commandes suivantes pour télécharger l’omsagent, valider la somme de contrôle, puis installer et intégrer l’agent.</span><span class="sxs-lookup"><span data-stu-id="645e3-231">Run the following commands to download the omsagent, validate the checksum, then  install and onboard the agent.</span></span> <span data-ttu-id="645e3-232">Ces commandes sont de type 64 bits.</span><span class="sxs-lookup"><span data-stu-id="645e3-232">Commands are for 64-bit.</span></span> <span data-ttu-id="645e3-233">L’ID et la clé primaire de l’espace de travail sont disponibles sur le portail OMS dans **Paramètres**, sous l’onglet **Sources connectées**.</span><span class="sxs-lookup"><span data-stu-id="645e3-233">The Workspace ID and Primary Key are found in the OMS portal under **Settings** on the **Connected Sources** tab.</span></span>

![détails sur l’espace de travail](./media/log-analytics-linux-agents/oms-direct-agent-primary-key.png)

```
wget https://raw.githubusercontent.com/Microsoft/OMS-Agent-for-Linux/master/installer/scripts/onboard_agent.sh && sh onboard_agent.sh -w <YOUR OMS WORKSPACE ID> -s <YOUR OMS WORKSPACE PRIMARY KEY>
```

<span data-ttu-id="645e3-235">Il existe plusieurs autres méthodes pour installer l’agent et le mettre à niveau.</span><span class="sxs-lookup"><span data-stu-id="645e3-235">There are a variety of other methods to install the agent and upgrade it.</span></span> <span data-ttu-id="645e3-236">Pour les découvrir, consultez [Steps to install the OMS Agent for Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux).</span><span class="sxs-lookup"><span data-stu-id="645e3-236">You can read more about them at [Steps to install the OMS Agent for Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux).</span></span>

<span data-ttu-id="645e3-237">Vous pouvez également regarder la [présentation vidéo d’Azure](https://www.youtube.com/watch?v=mF1wtHPEzT0).</span><span class="sxs-lookup"><span data-stu-id="645e3-237">You can also view the [Azure video walkthrough](https://www.youtube.com/watch?v=mF1wtHPEzT0).</span></span>

## <a name="choose-your-linux-data-collection-method"></a><span data-ttu-id="645e3-238">Choisir la mode de collecte des données Linux</span><span class="sxs-lookup"><span data-stu-id="645e3-238">Choose your Linux data collection method</span></span>
<span data-ttu-id="645e3-239">Le choix des types de données à collecter varie selon que vous souhaitez utiliser le portail OMS ou modifier plusieurs fichiers de configuration directement sur vos clients Linux.</span><span class="sxs-lookup"><span data-stu-id="645e3-239">How you choose the data types you'd like to collect depends on whether you want to use the OMS portal or if you want edit various configuration files directly on your Linux clients.</span></span> <span data-ttu-id="645e3-240">Si vous choisissez d’utiliser le portail, la configuration est automatiquement envoyée à tous vos clients Linux.</span><span class="sxs-lookup"><span data-stu-id="645e3-240">If you choose to use the portal, the configuration is sent to all of your Linux clients automatically.</span></span> <span data-ttu-id="645e3-241">Si vous avez besoin de différentes configurations pour différents clients Linux, vous devez modifier les fichiers de chaque client ou utiliser une solution telle que PowerShell DSC, Chef ou Puppet.</span><span class="sxs-lookup"><span data-stu-id="645e3-241">If you need different configurations for different Linux clients, you will need to edit client files individually – or use an alternative like PowerShell DSC, Chef, or Puppet.</span></span>

<span data-ttu-id="645e3-242">Vous pouvez spécifier les événements syslog et les compteurs de performances que vous souhaitez collecter, à l’aide des fichiers de configuration sur les ordinateurs Linux.</span><span class="sxs-lookup"><span data-stu-id="645e3-242">You can specify the syslog events and performance counters that you want to collect using configuration files on the Linux computers.</span></span> <span data-ttu-id="645e3-243">*Si vous avez choisi de configurer la collecte des données en modifiant les fichiers de configuration de l’agent, vous devez désactiver la configuration centralisée.*</span><span class="sxs-lookup"><span data-stu-id="645e3-243">*If you chose to configure data collection by editing agent configuration files, you should disable the centralized configuration.*</span></span>  <span data-ttu-id="645e3-244">Les instructions ci-dessous permettent de configurer la collecte des données dans les fichiers de configuration de l’agent, mais aussi de désactiver la configuration centralisée sur tous les agents OMS pour Linux ou sur chaque ordinateur individuellement.</span><span class="sxs-lookup"><span data-stu-id="645e3-244">Instructions are provided below to configure data collection in the agent's configuration files as well as to disable central configuration for all OMS Agents for Linux, or individual computers.</span></span>

### <a name="disable-oms-management-for-an-individual-linux-computer"></a><span data-ttu-id="645e3-245">Désactiver la gestion OMS sur un ordinateur Linux</span><span class="sxs-lookup"><span data-stu-id="645e3-245">Disable OMS management for an individual Linux computer</span></span>
<span data-ttu-id="645e3-246">La collecte centralisée des données de configuration est désactivée sur un ordinateur Linux grâce au script OMS_MetaConfigHelper.py.</span><span class="sxs-lookup"><span data-stu-id="645e3-246">Centralized data collection for configuration data is disabled for an individual Linux computer with the OMS_MetaConfigHelper.py script.</span></span> <span data-ttu-id="645e3-247">Ce script est très utile si quelques ordinateurs requièrent une configuration spéciale.</span><span class="sxs-lookup"><span data-stu-id="645e3-247">This can be useful if a subset of computers should have a specialized configuration.</span></span>

<span data-ttu-id="645e3-248">Pour désactiver la configuration centralisée :</span><span class="sxs-lookup"><span data-stu-id="645e3-248">To disable centralized configuration:</span></span>

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```

<span data-ttu-id="645e3-249">Pour réactiver la configuration centralisée :</span><span class="sxs-lookup"><span data-stu-id="645e3-249">To re-enable centralized configuration:</span></span>

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py –enable
```

## <a name="linux-performance-counters"></a><span data-ttu-id="645e3-250">Compteurs de performances Linux</span><span class="sxs-lookup"><span data-stu-id="645e3-250">Linux performance counters</span></span>
<span data-ttu-id="645e3-251">Les compteurs de performances Linux sont similaires aux compteurs de performances Windows : ils fonctionnent de la même façon.</span><span class="sxs-lookup"><span data-stu-id="645e3-251">Linux performance counters are similar to Windows performance counters—both operate similarly.</span></span> <span data-ttu-id="645e3-252">Vous pouvez utiliser les procédures suivantes pour les ajouter et les configurer.</span><span class="sxs-lookup"><span data-stu-id="645e3-252">You can use the following procedures to add and configure them.</span></span> <span data-ttu-id="645e3-253">Une fois ces compteurs ajoutés dans OMS, les données sont collectées toutes les 30 secondes.</span><span class="sxs-lookup"><span data-stu-id="645e3-253">After they are added to OMS, data is collected for them every 30 seconds.</span></span>

### <a name="to-add-a-linux-performance-counter-in-oms"></a><span data-ttu-id="645e3-254">Pour ajouter un compteur de performances Linux dans OMS</span><span class="sxs-lookup"><span data-stu-id="645e3-254">To add a Linux performance counter in OMS</span></span>
1. <span data-ttu-id="645e3-255">Pour configurer des agents OMS pour Linux à l’aide du portail OMS, ajoutez des compteurs de performances Linux dans la page Paramètres, puis cliquez sur **Données**.</span><span class="sxs-lookup"><span data-stu-id="645e3-255">To configure OMS Agents for Linux using the OMS portal, you can add Linux performance counters on the Settings page, click **Data**.</span></span>  
2. <span data-ttu-id="645e3-256">Dans la page **Paramètres**, sous **Données**, cliquez sur **Compteurs de performance Linux**, puis sélectionnez ou tapez le nom du compteur à ajouter.</span><span class="sxs-lookup"><span data-stu-id="645e3-256">On the **Settings** page under **Data** , click **Linux performance counters** and then select or type the name of the counter you want to add.</span></span>  
    <span data-ttu-id="645e3-257">![données](./media/log-analytics-linux-agents/oms-settings-data01.png)</span><span class="sxs-lookup"><span data-stu-id="645e3-257">![data](./media/log-analytics-linux-agents/oms-settings-data01.png)</span></span>
3. <span data-ttu-id="645e3-258">Si vous ne connaissez pas le nom complet du compteur, commencez à taper les premières lettres et la liste des compteurs correspondants s’affiche.</span><span class="sxs-lookup"><span data-stu-id="645e3-258">If you don't know the full name of the counter, you can start typing a partial name and a list of available counters will appear.</span></span> <span data-ttu-id="645e3-259">Lorsque vous avez trouvé le compteur à ajouter, cliquez sur son nom dans la liste puis sur l’icône de signe plus pour l’ajouter.</span><span class="sxs-lookup"><span data-stu-id="645e3-259">When you find the counter you want to add, click the name in the list and then click the plus icon to add the counter.</span></span>
4. <span data-ttu-id="645e3-260">Une fois ajouté, le compteur apparaît dans la liste des compteurs avec une barre de couleur.</span><span class="sxs-lookup"><span data-stu-id="645e3-260">After you add the counter, it appears in the list of counters highlighted with a colored bar.</span></span>
5. <span data-ttu-id="645e3-261">Par défaut, l’option **Appliquer la configuration ci-dessous à mes machines** est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="645e3-261">By default, the **Apply below configuration to my machines** option is selected.</span></span> <span data-ttu-id="645e3-262">Si vous souhaitez désactiver l’envoi des données de configuration, décochez la case.</span><span class="sxs-lookup"><span data-stu-id="645e3-262">If you want to disable sending configuration data, clear the selection.</span></span>
6. <span data-ttu-id="645e3-263">Lorsque vous avez terminé la modification des compteurs de performances, en bas de la page, cliquez sur **Enregistrer** pour finaliser vos modifications.</span><span class="sxs-lookup"><span data-stu-id="645e3-263">When you are done modifying performance counters, at the bottom of the page click **Save** to finalize your changes.</span></span> <span data-ttu-id="645e3-264">Les modifications de configuration que vous avez apportées sont ensuite envoyées à tous les Agents OMS pour Linux enregistrés dans OMS, généralement dans les 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="645e3-264">The configuration changes that you've made are then sent to all the OMS Agents for Linux that are registered with OMS, typically within 5 minutes.</span></span>

### <a name="configure-linux-performance-counters-in-oms"></a><span data-ttu-id="645e3-265">Configurer des compteurs de performances Linux dans OMS</span><span class="sxs-lookup"><span data-stu-id="645e3-265">Configure Linux performance counters in OMS</span></span>
<span data-ttu-id="645e3-266">Pour les compteurs de performances Windows, vous pouvez choisir une instance spécifique de chaque compteur de performances.</span><span class="sxs-lookup"><span data-stu-id="645e3-266">For Windows performance counters, you can choose a specific instance for each performance counter.</span></span> <span data-ttu-id="645e3-267">En revanche, pour les compteurs de performances Linux, l’instance de compteur que vous choisissez s’applique à tous les compteurs enfants du compteur parent.</span><span class="sxs-lookup"><span data-stu-id="645e3-267">However, for Linux performance counters, whatever instance of a counter that you choose applies to all child counters of the parent counter.</span></span> <span data-ttu-id="645e3-268">Le tableau suivant montre les instances courantes disponibles pour les compteurs de performances Linux et Windows.</span><span class="sxs-lookup"><span data-stu-id="645e3-268">The following table shows the common instances available to both Linux and Windows performance counters.</span></span>

| <span data-ttu-id="645e3-269">**Nom de l’instance**</span><span class="sxs-lookup"><span data-stu-id="645e3-269">**Instance name**</span></span> | <span data-ttu-id="645e3-270">**Signification**</span><span class="sxs-lookup"><span data-stu-id="645e3-270">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="645e3-271">\_Total</span><span class="sxs-lookup"><span data-stu-id="645e3-271">\_Total</span></span> |<span data-ttu-id="645e3-272">Total de toutes les instances</span><span class="sxs-lookup"><span data-stu-id="645e3-272">Total of all the instances</span></span> |
| \* |<span data-ttu-id="645e3-273">Toutes les instances</span><span class="sxs-lookup"><span data-stu-id="645e3-273">All instances</span></span> |
| <span data-ttu-id="645e3-274">(/&#124;/var)</span><span class="sxs-lookup"><span data-stu-id="645e3-274">(/&#124;/var)</span></span> |<span data-ttu-id="645e3-275">Correspond aux instances nommées : / ou /var</span><span class="sxs-lookup"><span data-stu-id="645e3-275">Matches instances named: / or /var</span></span> |

<span data-ttu-id="645e3-276">De même, l’intervalle d’échantillonnage que vous choisissez pour un compteur parent s’applique à tous ses compteurs enfants.</span><span class="sxs-lookup"><span data-stu-id="645e3-276">Similarly, the sample interval that you choose for a parent counter applies to all its child counters.</span></span> <span data-ttu-id="645e3-277">En d’autres termes, tous les intervalles d’échantillonnage et toutes les instances des compteurs enfants sont liés entre elles.</span><span class="sxs-lookup"><span data-stu-id="645e3-277">In other words, all the child counter sample intervals and instances are tied together.</span></span>

### <a name="add-and-configure-performance-metrics-with-linux"></a><span data-ttu-id="645e3-278">Ajouter et configurer des mesures de performances avec Linux</span><span class="sxs-lookup"><span data-stu-id="645e3-278">Add and configure performance metrics with Linux</span></span>
<span data-ttu-id="645e3-279">Les mesures de performances à collecter sont contrôlées par la configuration du fichier /etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf.</span><span class="sxs-lookup"><span data-stu-id="645e3-279">Performance metrics to collect are controlled by the configuration in /etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf.</span></span> <span data-ttu-id="645e3-280">Pour obtenir les classes et mesures disponibles pour l’Agent OMS pour Linux, consultez [Available Performance Metrics](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics) .</span><span class="sxs-lookup"><span data-stu-id="645e3-280">See [Available performance metrics](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics) for available classes and metrics for the OMS Agent for Linux.</span></span>

<span data-ttu-id="645e3-281">Chaque objet, ou catégorie, de mesures de performances à collecter doit être défini dans le fichier de configuration comme un seul élément `<source>` .</span><span class="sxs-lookup"><span data-stu-id="645e3-281">Each object, or category, of performance metrics to collect should be defined in the configuration file as a single `<source>` element.</span></span> <span data-ttu-id="645e3-282">La syntaxe suit le modèle suivant.</span><span class="sxs-lookup"><span data-stu-id="645e3-282">The syntax follows the pattern below.</span></span>

```
<source>
  type oms_omi  
  object_name "Processor"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

<span data-ttu-id="645e3-283">Les paramètres configurables de cet élément sont :</span><span class="sxs-lookup"><span data-stu-id="645e3-283">The configurable parameters of this element are:</span></span>

* <span data-ttu-id="645e3-284">**Object\_name** : nom de l’objet à collecter.</span><span class="sxs-lookup"><span data-stu-id="645e3-284">**Object\_name**: the object name for the collection.</span></span>
* <span data-ttu-id="645e3-285">**Instance\_regex** : a *expression régulière* définissant les instances à collecter.</span><span class="sxs-lookup"><span data-stu-id="645e3-285">**Instance\_regex**: a *regular expression* defining which instances to collect.</span></span> <span data-ttu-id="645e3-286">La valeur `.*` spécifie toutes les instances.</span><span class="sxs-lookup"><span data-stu-id="645e3-286">The value: `.*` specifies all instances.</span></span> <span data-ttu-id="645e3-287">Pour ne collecter les mesures de processeur que de l’instance \_Total, vous pouvez spécifier `_Total`.</span><span class="sxs-lookup"><span data-stu-id="645e3-287">To collect processor metrics for only the \_Total instance, you could specify `_Total`.</span></span> <span data-ttu-id="645e3-288">Pour ne collecter les mesures de processeur que des instances crond ou sshd, vous pouvez spécifier `(crond|sshd)`.</span><span class="sxs-lookup"><span data-stu-id="645e3-288">To collect process metrics for only the crond or sshd instances, you could specify: `(crond|sshd)`.</span></span>
* <span data-ttu-id="645e3-289">**Counter\_name\_regex** : *expression régulière* définissant les compteurs (de l’objet) à collecter.</span><span class="sxs-lookup"><span data-stu-id="645e3-289">**Counter\_name\_regex**: a *regular expression* defining which counters (for the object) to collect.</span></span> <span data-ttu-id="645e3-290">Pour collecter tous les compteurs de l’objet, spécifiez : `.*`.</span><span class="sxs-lookup"><span data-stu-id="645e3-290">To collect all counters for the object, specify: `.*`.</span></span> <span data-ttu-id="645e3-291">Pour ne collecter que les compteurs du fichier d’échange de l’objet mémoire, vous pouvez spécifier : `.+Swap.+`</span><span class="sxs-lookup"><span data-stu-id="645e3-291">To collect only swap space counters for the memory object, you could specify: `.+Swap.+`</span></span>
* <span data-ttu-id="645e3-292">**Interval**: fréquence de collecte des compteurs de l’objet.</span><span class="sxs-lookup"><span data-stu-id="645e3-292">**Interval:**: the frequency at which the object's counters are collected.</span></span>

<span data-ttu-id="645e3-293">La configuration par défaut des mesures de performances est la suivante :</span><span class="sxs-lookup"><span data-stu-id="645e3-293">The default configuration for performance metrics is:</span></span>

```
<source>
  type oms_omi
  object_name "Physical Disk"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 5m
</source>

<source>
  type oms_omi
  object_name "Logical Disk"
  instance_regex ".*
  counter_name_regex ".*"
  interval 5m
</source>

<source>
  type oms_omi
  object_name "Processor"
  instance_regex ".*
  counter_name_regex ".*"
  interval 30s
</source>

<source>
  type oms_omi
  object_name "Memory"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

### <a name="enable-mysql-performance-counters-using-linux-commands"></a><span data-ttu-id="645e3-294">Activer des compteurs de performances MySQL à l’aide de commandes Linux</span><span class="sxs-lookup"><span data-stu-id="645e3-294">Enable MySQL performance counters using Linux commands</span></span>
<span data-ttu-id="645e3-295">Si MySQL Server ou MariaDB Server est détecté sur l’ordinateur où omsagent est installé, un fournisseur de surveillance des performances de MySQL Server est automatiquement installé.</span><span class="sxs-lookup"><span data-stu-id="645e3-295">If MySQL Server or MariaDB Server is detected on the computer when the omsagent bundle is installed, a performance monitoring provider for MySQL Server is automatically installed.</span></span> <span data-ttu-id="645e3-296">Ce fournisseur se connecte au serveur MySQL/MariaDB local pour afficher les statistiques de performances.</span><span class="sxs-lookup"><span data-stu-id="645e3-296">This provider connects to the local MySQL/MariaDB server to expose performance statistics.</span></span> <span data-ttu-id="645e3-297">Vous devez configurer les informations d’identification de l’utilisateur MySQL, afin que le fournisseur puisse accéder à MySQL Server.</span><span class="sxs-lookup"><span data-stu-id="645e3-297">You need to configure MySQL user credentials so that the provider can access the MySQL Server.</span></span>

<span data-ttu-id="645e3-298">Pour définir le compte utilisateur par défaut du serveur MySQL sur l’hôte local, utilisez l’exemple de commande suivant.</span><span class="sxs-lookup"><span data-stu-id="645e3-298">To define a default user account for the MySQL server on localhost, use the following command example.</span></span>

> [!NOTE]
> <span data-ttu-id="645e3-299">Le fichier des informations d’identification doit être accessible en lecture par le compte omsagent.</span><span class="sxs-lookup"><span data-stu-id="645e3-299">The credentials file must be readable by the omsagent account.</span></span> <span data-ttu-id="645e3-300">L’exécution de la commande mycimprovauth comme omsgent est recommandée.</span><span class="sxs-lookup"><span data-stu-id="645e3-300">Running the mycimprovauth command as omsgent is recommended.</span></span>
>
>

```
sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>

sudo /opt/omi/bin/service_control restart
```


<span data-ttu-id="645e3-301">Sinon, vous pouvez spécifier les informations d’identification MySQL requises dans un fichier, en créant le fichier : /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth.</span><span class="sxs-lookup"><span data-stu-id="645e3-301">Alternatively, you can specify the required MySQL credentials in a file, by creating the file: /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth.</span></span> <span data-ttu-id="645e3-302">Pour plus d’informations sur la gestion des informations d’identification MySQL à des fins de surveillance par le fichier mysql-auth, consultez [Gérer des informations d’identification de surveillance de MySQL dans le fichier d’authentification](#manage-mysql-monitoring-credentials-in-the-authentication-file).</span><span class="sxs-lookup"><span data-stu-id="645e3-302">For more information about managing MySQL credentials for monitoring through the mysql-auth file, see [Manage MySQL monitoring credentials in the authentication file](#manage-mysql-monitoring-credentials-in-the-authentication-file).</span></span>

<span data-ttu-id="645e3-303">Pour plus d’informations sur les autorisations d’objet requises par l’utilisateur MySQL pour collecter les données de performances de MySQL Server, consultez [Autorisations de base de données requises par l’utilisateur MySQL pour collecter les données de performances de MySQL Server](#database-permissions-required-for-mysql-performance-counters) .</span><span class="sxs-lookup"><span data-stu-id="645e3-303">See [Database permissions required for MySQL performance counters](#database-permissions-required-for-mysql-performance-counters) for details about object permissions required by the MySQL user to collect MySQL Server performance data.</span></span>

### <a name="enable-apache-http-server-performance-counters-using-linux-commands"></a><span data-ttu-id="645e3-304">Activer les compteurs de performances d’Apache HTTP Server à l’aide de commandes Linux</span><span class="sxs-lookup"><span data-stu-id="645e3-304">Enable Apache HTTP Server performance counters using Linux commands</span></span>
<span data-ttu-id="645e3-305">Si Apache HTTP Server est détecté sur l’ordinateur où omsagent est installé, un fournisseur de surveillance des performances d’Apache HTTP Server est automatiquement installé.</span><span class="sxs-lookup"><span data-stu-id="645e3-305">If Apache HTTP Server is detected on the computer when the omsagent bundle is installed, a performance monitoring provider for Apache HTTP Server is automatically installed.</span></span> <span data-ttu-id="645e3-306">Ce fournisseur repose sur un « module » Apache qui doit être chargé dans Apache HTTP Server afin d’accéder aux données de performances.</span><span class="sxs-lookup"><span data-stu-id="645e3-306">This provider relies on an Apache "module" that must be loaded into the Apache HTTP Server in order to access performance data.</span></span>

<span data-ttu-id="645e3-307">Vous pouvez charger le module avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="645e3-307">You can load the module with the following command:</span></span>

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

<span data-ttu-id="645e3-308">Pour décharger le module de surveillance Apache, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="645e3-308">To unload the Apache monitoring module, run the following command:</span></span>

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```
### <a name="to-view-performance-data-with-log-analytics"></a><span data-ttu-id="645e3-309">Pour afficher les données de performances avec Log Analytics</span><span class="sxs-lookup"><span data-stu-id="645e3-309">To view performance data with Log Analytics</span></span>
1. <span data-ttu-id="645e3-310">Dans le portail Operations Management Suite, cliquez sur la mosaïque Recherche de journal.</span><span class="sxs-lookup"><span data-stu-id="645e3-310">In the Operations Management Suite portal, click the Log Search tile.</span></span>
2. <span data-ttu-id="645e3-311">Dans la barre de recherche, tapez `* (Type=Perf)` pour afficher tous les compteurs de performances.</span><span class="sxs-lookup"><span data-stu-id="645e3-311">In the search bar, type `* (Type=Perf)` to view all performance counters.</span></span>

<span data-ttu-id="645e3-312">Comme OMS collecte également les données des compteurs de performances Windows, vous devez restreindre la recherche aux données spécifiquement Linux.</span><span class="sxs-lookup"><span data-stu-id="645e3-312">Because OMS also collects Windows performance counter data, you should scope-down the search to Linux-specific data.</span></span> <span data-ttu-id="645e3-313">Ainsi, l’exemple suivant affiche les données de performances concernant un exemple de serveur Linux nommé Chorizo21.</span><span class="sxs-lookup"><span data-stu-id="645e3-313">So, the following example would show performance data specific to an example Linux server named Chorizo21.</span></span>

```
Type=Perf Computer=chorizo*
```

![exemple de serveur affiché dans les résultats de la recherche](./media/log-analytics-linux-agents/oms-perfsearch01.png)

<span data-ttu-id="645e3-315">Dans les résultats, vous pouvez cliquer sur **Mesures** pour afficher les compteurs pour lesquels des données ont été collectées.</span><span class="sxs-lookup"><span data-stu-id="645e3-315">In the results, you can click **Metrics** to view the counters that data was collected for.</span></span> <span data-ttu-id="645e3-316">Les données en temps réel sont indiquées sous forme graphique pour chaque compteur.</span><span class="sxs-lookup"><span data-stu-id="645e3-316">Real-time data is shown as graphs for each counter.</span></span>

![Mesures](./media/log-analytics-linux-agents/oms-perfmetrics01.png)

## <a name="syslog"></a><span data-ttu-id="645e3-318">syslog</span><span class="sxs-lookup"><span data-stu-id="645e3-318">Syslog</span></span>
<span data-ttu-id="645e3-319">Syslog est un protocole de journalisation des événements, similaire aux Journaux des événements Windows : les deux fonctionnent de la même façon lorsqu’ils sont affichés dans OMS.</span><span class="sxs-lookup"><span data-stu-id="645e3-319">Syslog is an event logging protocol similar to Windows Event logs—both operate similarly when displayed in OMS.</span></span>

### <a name="to-add-a-new-linux-syslog-facility-in-oms"></a><span data-ttu-id="645e3-320">Pour ajouter une nouvelle fonctionnalité syslog Linux dans OMS</span><span class="sxs-lookup"><span data-stu-id="645e3-320">To add a new Linux syslog facility in OMS</span></span>
1. <span data-ttu-id="645e3-321">Dans la page **Paramètres** sous **Données**, cliquez sur **Syslog** puis, à gauche de l’icône plus, tapez le nom de la fonctionnalité Syslog à ajouter.</span><span class="sxs-lookup"><span data-stu-id="645e3-321">On the **Settings** page under **Data** , click **Syslog** and then to the left of the plus icon, type the name of the syslog facility that you want to add.</span></span>
    <span data-ttu-id="645e3-322">![Syslog Linux](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)</span><span class="sxs-lookup"><span data-stu-id="645e3-322">![Linux syslog](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)</span></span>
2. <span data-ttu-id="645e3-323">Si vous ne connaissez pas le nom complet de la fonctionnalité, tapez les premières lettres et la liste des fonctionnalités syslog correspondantes s’affiche.</span><span class="sxs-lookup"><span data-stu-id="645e3-323">If you don’t know the full name of the facility, you can start typing a partial name and a list of available syslog facilities will appear.</span></span> <span data-ttu-id="645e3-324">Lorsque vous avez trouvé la fonctionnalité syslog à ajouter, cliquez sur son nom dans la liste puis sur l’icône de signe plus pour l’ajouter.</span><span class="sxs-lookup"><span data-stu-id="645e3-324">When you find the syslog facility that you want to add, click the name in the list and then click the plus icon to add the syslog facility.</span></span>
3. <span data-ttu-id="645e3-325">Une fois la fonctionnalité ajoutée, le compteur apparaît dans la liste des compteurs avec une barre de couleur.</span><span class="sxs-lookup"><span data-stu-id="645e3-325">After you add the facility, it appears in the list of highlighted with a colored bar.</span></span> <span data-ttu-id="645e3-326">Ensuite, choisissez les niveaux de gravité (catégories d’informations sur les fonctionnalités syslog) que vous souhaitez collecter.</span><span class="sxs-lookup"><span data-stu-id="645e3-326">Next, choose the severities (categories of syslog facility information) that you want to collect.</span></span>
4. <span data-ttu-id="645e3-327">En bas de la page, cliquez sur **Enregistrer** pour finaliser vos modifications.</span><span class="sxs-lookup"><span data-stu-id="645e3-327">At the bottom of the page click **Save** to finalize your changes.</span></span> <span data-ttu-id="645e3-328">Les modifications de configuration que vous avez apportées sont ensuite envoyées à tous les Agents OMS pour Linux enregistrés dans OMS, généralement dans les 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="645e3-328">The configuration changes that you’ve made are then sent to all the OMS Agents for Linux that are registered with OMS, typically within 5 minutes.</span></span>

### <a name="configure-linux-syslog-facilities-in-linux"></a><span data-ttu-id="645e3-329">Configurer des fonctionnalités syslog Linux dans Linux</span><span class="sxs-lookup"><span data-stu-id="645e3-329">Configure Linux syslog facilities in Linux</span></span>
<span data-ttu-id="645e3-330">Des événements syslog sont envoyés du démon syslog, par exemple rsyslog ou syslog-ng, à un port local écouté par l’agent.</span><span class="sxs-lookup"><span data-stu-id="645e3-330">Syslog events are sent from the syslog daemon, for example rsyslog or syslog-ng, to a local port that the agent is listening on.</span></span> <span data-ttu-id="645e3-331">Le port par défaut est 25224.</span><span class="sxs-lookup"><span data-stu-id="645e3-331">By default, port 25224.</span></span> <span data-ttu-id="645e3-332">Lorsque l’agent est installé, une configuration syslog par défaut est appliquée.</span><span class="sxs-lookup"><span data-stu-id="645e3-332">When the agent is installed, a default syslog configuration is applied.</span></span> <span data-ttu-id="645e3-333">Elle se trouve à l’emplacement suivant :</span><span class="sxs-lookup"><span data-stu-id="645e3-333">This is found at:</span></span>

<span data-ttu-id="645e3-334">Rsyslog : /etc/rsyslog.d/rsyslog-oms.conf</span><span class="sxs-lookup"><span data-stu-id="645e3-334">Rsyslog: /etc/rsyslog.d/rsyslog-oms.conf</span></span>

<span data-ttu-id="645e3-335">Syslog-ng : /etc/syslog-ng/syslog-ng.conf</span><span class="sxs-lookup"><span data-stu-id="645e3-335">Syslog-ng: /etc/syslog-ng/syslog-ng.conf</span></span>

<span data-ttu-id="645e3-336">La configuration syslog par défaut de l’agent OMS télécharge les événements syslog de toutes les fonctionnalités ayant au moins le niveau de gravité Avertissement.</span><span class="sxs-lookup"><span data-stu-id="645e3-336">The default OMS agent syslog configuration uploads syslog events from all facilities with a severity of warning or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="645e3-337">Si vous modifiez cette configuration, vous devez redémarrer le démon syslog pour que les modifications prennent effet.</span><span class="sxs-lookup"><span data-stu-id="645e3-337">If you edit the syslog configuration, you must restart the syslog daemon for the changes to take effect.</span></span>
>
>

<span data-ttu-id="645e3-338">La configuration syslog par défaut de l’Agent OMS pour Linux dans OMS est la suivante :</span><span class="sxs-lookup"><span data-stu-id="645e3-338">The default syslog configuration for the OMS Agent for Linux for OMS is:</span></span>

#### <a name="rsyslog"></a><span data-ttu-id="645e3-339">Rsyslog</span><span class="sxs-lookup"><span data-stu-id="645e3-339">Rsyslog</span></span>
```
kern.warning       @127.0.0.1:25224
user.warning       @127.0.0.1:25224
daemon.warning     @127.0.0.1:25224
auth.warning       @127.0.0.1:25224
syslog.warning     @127.0.0.1:25224
uucp.warning       @127.0.0.1:25224
authpriv.warning   @127.0.0.1:25224
ftp.warning        @127.0.0.1:25224
cron.warning       @127.0.0.1:25224
local0.warning     @127.0.0.1:25224
local1.warning     @127.0.0.1:25224
local2.warning     @127.0.0.1:25224
local3.warning     @127.0.0.1:25224
local4.warning     @127.0.0.1:25224
local5.warning     @127.0.0.1:25224
local6.warning     @127.0.0.1:25224
local7.warning     @127.0.0.1:25224
```

#### <a name="syslog-ng"></a><span data-ttu-id="645e3-340">Syslog-ng</span><span class="sxs-lookup"><span data-stu-id="645e3-340">Syslog-ng</span></span>
```
#OMS_facility = all
filter f_warning_oms { level(warning); };
destination warning_oms { tcp("127.0.0.1" port(25224)); };
log { source(src); filter(f_warning_oms); destination(warning_oms); };
```

### <a name="to-view-all-syslog-events-with-log-analytics"></a><span data-ttu-id="645e3-341">Pour afficher tous les événements Syslog avec Log Analytics</span><span class="sxs-lookup"><span data-stu-id="645e3-341">To view all Syslog events with Log Analytics</span></span>
1. <span data-ttu-id="645e3-342">Dans le portail Operations Management Suite, cliquez sur la mosaïque **Recherche de journal** .</span><span class="sxs-lookup"><span data-stu-id="645e3-342">In the Operations Management Suite portal, click the **Log Search** tile.</span></span>
2. <span data-ttu-id="645e3-343">Dans le groupe **Gestion de journal** , sélectionnez une recherche syslog prédéfinie puis exécutez-la.</span><span class="sxs-lookup"><span data-stu-id="645e3-343">In the **Log Management** grouping, choose a predefined syslog search and then select one to run it.</span></span>

<span data-ttu-id="645e3-344">Cet exemple montre tous les événements Syslog.</span><span class="sxs-lookup"><span data-stu-id="645e3-344">This example shows all Syslog events.</span></span>

![Événements syslog affichés dans Recherche de journal](./media/log-analytics-linux-agents/oms-linux-syslog.png)

<span data-ttu-id="645e3-346">Maintenant, vous pouvez examiner les résultats de la recherche plus en détail.</span><span class="sxs-lookup"><span data-stu-id="645e3-346">Now you can drill into search results.</span></span>

## <a name="linux-alerts"></a><span data-ttu-id="645e3-347">Alertes Linux</span><span class="sxs-lookup"><span data-stu-id="645e3-347">Linux alerts</span></span>
<span data-ttu-id="645e3-348">Si vous utilisez Nagios ou Zabbix pour gérer vos ordinateurs Linux, OMS peut recevoir les alertes générées par ces outils.</span><span class="sxs-lookup"><span data-stu-id="645e3-348">If you use Nagios or Zabbix to manage your Linux machines, then OMS can receive the alerts generated from those tools.</span></span> <span data-ttu-id="645e3-349">Toutefois, il n’existe actuellement aucune méthode pour configurer les données d’alerte entrantes à l’aide du portail OMS.</span><span class="sxs-lookup"><span data-stu-id="645e3-349">However, there is currently no method to configure incoming alert data using the OMS portal.</span></span> <span data-ttu-id="645e3-350">En revanche, vous devez modifier un fichier de configuration pour commencer à envoyer des alertes à OMS.</span><span class="sxs-lookup"><span data-stu-id="645e3-350">Instead, you will need to edit a config file to start sending alerts to OMS.</span></span>

### <a name="collect-alerts-from-nagios"></a><span data-ttu-id="645e3-351">Collecter les alertes de Nagios</span><span class="sxs-lookup"><span data-stu-id="645e3-351">Collect alerts from Nagios</span></span>
<span data-ttu-id="645e3-352">Pour collecter les alertes d’un serveur Nagios, vous devez apporter les modifications de configuration suivantes.</span><span class="sxs-lookup"><span data-stu-id="645e3-352">To collect alerts from a Nagios server, you need to make the following configuration changes.</span></span>

1. <span data-ttu-id="645e3-353">Accordez à l’utilisateur **omsagent** un accès en lecture au fichier journal Nagios (/var/log/nagios/nagios.log).</span><span class="sxs-lookup"><span data-stu-id="645e3-353">Grant the user **omsagent** read access to the Nagios log file (i.e. /var/log/nagios/nagios.log).</span></span> <span data-ttu-id="645e3-354">Si le fichier nagios.log appartient au groupe **nagios**, vous pouvez ajouter l’utilisateur **omsagent** au groupe **nagios**.</span><span class="sxs-lookup"><span data-stu-id="645e3-354">Assuming the nagios.log file is owned by the group **nagios** , you can add the user **omsagent** to the **nagios** group.</span></span>

    ```
    sudo usermod –a -G nagios omsagent
    ```
2. <span data-ttu-id="645e3-355">Modifiez le fichier de configuration omsagent.conf (/etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf).</span><span class="sxs-lookup"><span data-stu-id="645e3-355">Modify the omsagent.confconfiguration file (/etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf).</span></span> <span data-ttu-id="645e3-356">Vérifiez que les entrées suivantes sont présentes et non mises en commentaire :</span><span class="sxs-lookup"><span data-stu-id="645e3-356">Ensure the following entries are present and not commented out:</span></span>

    ```
    <source>
    type tail
    #Update path to point to your nagios.log
    path /var/log/nagios/nagios.log
    format none
    tag oms.nagios
    </source>

    <filter oms.nagios>
    type filter_nagios_log
    </filter>
    ```
3. <span data-ttu-id="645e3-357">Redémarrez le démon omsagent :</span><span class="sxs-lookup"><span data-stu-id="645e3-357">Restart the omsagent daemon:</span></span>

    ```
    sudo /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="collect-alerts-from-zabbix"></a><span data-ttu-id="645e3-358">Collecter les alertes de Zabbix</span><span class="sxs-lookup"><span data-stu-id="645e3-358">Collect alerts from Zabbix</span></span>
<span data-ttu-id="645e3-359">Pour collecter les alertes d’un serveur Zabbix, vous allez effectuer des étapes similaires à celles de Nagios ci-dessus, mais vous devez spécifier un utilisateur et un mot de passe en *clair*.</span><span class="sxs-lookup"><span data-stu-id="645e3-359">To collect alerts from a Zabbix server, you'll perform similar steps to those for Nagios above, except you'll need to specify a user and password in *clear text*.</span></span> <span data-ttu-id="645e3-360">Cette solution n’est pas idéale, mais elle devrait changer rapidement.</span><span class="sxs-lookup"><span data-stu-id="645e3-360">This is not ideal, but will likely change soon.</span></span> <span data-ttu-id="645e3-361">Pour résoudre ce problème, nous vous recommandons de créer l’utilisateur et de ne lui accorder que l’autorisation de surveillance.</span><span class="sxs-lookup"><span data-stu-id="645e3-361">To address this issue, we recommend that you create the user and grant it permission to monitor only.</span></span>

<span data-ttu-id="645e3-362">Une section du fichier de configuration omsagent.conf (/etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf) pour Zabbix pourrait ressembler à celle ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="645e3-362">An example section of the omsagent.conf configuration file  (/etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf) for Zabbix should resemble the following:</span></span>

```
<source>
  type zabbix_alerts
  run_interval 1m
  tag oms.zabbix
  zabbix_url http://localhost/zabbix/api_jsonrpc.php
  zabbix_username Admin
  zabbix_password zabbix
</source>

```

### <a name="view-alerts-in-log-analytics-search"></a><span data-ttu-id="645e3-363">Afficher les alertes dans la recherche Log Analytics</span><span class="sxs-lookup"><span data-stu-id="645e3-363">View alerts in Log Analytics search</span></span>
<span data-ttu-id="645e3-364">Après avoir configuré vos ordinateurs Linux pour envoyer des alertes à OMS, vous pouvez utiliser quelques requêtes simples pour afficher les alertes.</span><span class="sxs-lookup"><span data-stu-id="645e3-364">After you've configured your Linux computers to send alerts to OMS, you can use a few simple log search queries to view the alerts.</span></span> <span data-ttu-id="645e3-365">La requête suivante renvoie toutes les alertes enregistrées qui ont été générées.</span><span class="sxs-lookup"><span data-stu-id="645e3-365">The following search query example returns all the recorded alerts that were generated.</span></span> <span data-ttu-id="645e3-366">Par exemple, en cas de problème dans votre infrastructure informatique, les résultats de la requête suivante peuvent en révéler la cause.</span><span class="sxs-lookup"><span data-stu-id="645e3-366">For example, if some sort of problem occurs in your IT infrastructure, then results for the following example query might indicate where the problem might originate.</span></span> <span data-ttu-id="645e3-367">Et vous pouvez facilement examiner les alertes par système source afin de restreindre votre champ d’investigation.</span><span class="sxs-lookup"><span data-stu-id="645e3-367">And, you can easily drill in to the alerts by source system to help narrow your investigation.</span></span> <span data-ttu-id="645e3-368">L’avantage est que vous n’avez plus à utiliser différents systèmes de gestion. Si vos alertes sont envoyées à OMS, vous pouvez utiliser cet outil.</span><span class="sxs-lookup"><span data-stu-id="645e3-368">The benefit is that you don't necessarily have to go to various management systems from the start—provided that your alerts are sent to OMS, you can start there.</span></span>

```
Type=Alert
```

#### <a name="to-view-all-nagios-alerts-with-log-analytics"></a><span data-ttu-id="645e3-369">Pour afficher toutes les alertes Nagios avec Log Analytics</span><span class="sxs-lookup"><span data-stu-id="645e3-369">To view all Nagios alerts with Log Analytics</span></span>
1. <span data-ttu-id="645e3-370">Dans le portail Operations Management Suite, cliquez sur la mosaïque **Recherche de journal** .</span><span class="sxs-lookup"><span data-stu-id="645e3-370">In the Operations Management Suite portal, click the **Log Search** tile.</span></span>
2. <span data-ttu-id="645e3-371">Dans la barre de requête, tapez la requête suivante :</span><span class="sxs-lookup"><span data-stu-id="645e3-371">In the query bar, type the following search query</span></span>

    ```
    Type=Alert SourceSystem=Nagios
    ```
   ![Alertes Nagios affichées dans Recherche de journal](./media/log-analytics-linux-agents/oms-linux-nagios-alerts.png)

<span data-ttu-id="645e3-373">Après avoir consulté les résultats de la recherche, vous pouvez examiner les détails supplémentaires tels que *AlertState*.</span><span class="sxs-lookup"><span data-stu-id="645e3-373">After you see the search results, you can drill into additional details such as *AlertState*.</span></span>

### <a name="to-view-all-zabbix-alerts-with-log-analytics"></a><span data-ttu-id="645e3-374">Pour afficher tous les événements Zabbix avec Log Analytics</span><span class="sxs-lookup"><span data-stu-id="645e3-374">To view all Zabbix alerts with Log Analytics</span></span>
1. <span data-ttu-id="645e3-375">Dans le portail Operations Management Suite, cliquez sur la mosaïque **Recherche de journal** .</span><span class="sxs-lookup"><span data-stu-id="645e3-375">In the Operations Management Suite portal, click the **Log Search** tile.</span></span>
2. <span data-ttu-id="645e3-376">Dans la barre de requête, tapez la requête suivante :</span><span class="sxs-lookup"><span data-stu-id="645e3-376">In the query bar, type the following search query</span></span>

    ```
    Type=Alert SourceSystem=Zabbix
    ```
   ![Alertes Zabbix affichées dans Recherche de journal](./media/log-analytics-linux-agents/oms-linux-zabbix-alerts.png)

<span data-ttu-id="645e3-378">Après avoir consulté les résultats de la recherche, vous pouvez examiner les détails supplémentaires tels que *AlertName*.</span><span class="sxs-lookup"><span data-stu-id="645e3-378">After you see the search results, you can drill into additional details such as *AlertName*.</span></span>

## <a name="compatibility-with-system-center-operations-manager"></a><span data-ttu-id="645e3-379">Compatibilité avec System Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="645e3-379">Compatibility with System Center Operations Manager</span></span>
<span data-ttu-id="645e3-380">L’Agent OMS pour Linux partage ses fichiers binaires avec l’agent System Center Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="645e3-380">The OMS Agent for Linux shares agent binaries with the System Center Operations Manager agent.</span></span> <span data-ttu-id="645e3-381">L’installation de l’Agent OMS pour Linux sur un système géré par Operations Manager met à niveau les packages OMI et SCX sur l’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="645e3-381">Installing the OMS Agent for Linux on a system currently managed by Operations Manager upgrades the OMI and SCX packages on the computer to a newer version.</span></span> <span data-ttu-id="645e3-382">L’Agent OMS pour Linux et System Center 2012 R2 sont compatibles.</span><span class="sxs-lookup"><span data-stu-id="645e3-382">The OMS Agent for Linux and System Center 2012 R2 are compatible.</span></span> <span data-ttu-id="645e3-383">Toutefois, **System Center 2012 SP1 et ses versions antérieures ne sont actuellement pas compatibles avec l’Agent OMS pour Linux.**</span><span class="sxs-lookup"><span data-stu-id="645e3-383">However, **System Center 2012 SP1 and earlier versions are currently not compatible or supported with the OMS Agent for Linux.**</span></span>

> [!NOTE]
> <span data-ttu-id="645e3-384">Si l’Agent OMS pour Linux est installé sur un ordinateur non géré par Operations Manager, et que vous décidez ensuite de gérer l’ordinateur avec Operations Manager, vous devez modifier la configuration d’OMI avant de détecter l’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="645e3-384">If the OMS Agent for Linux is installed to a computer that is not currently managed by Operations Manager, and you later want to manage the computer with Operations Manager, you must modify the OMI configuration before you discover the computer.</span></span> <span data-ttu-id="645e3-385">**Cette étape n’est pas nécessaire si l’agent Operations Manager est installé avant l’Agent OMS pour Linux.**</span><span class="sxs-lookup"><span data-stu-id="645e3-385">**This step is not needed if the Operations Manager agent is installed before the OMS Agent for Linux.**</span></span>
>
>

### <a name="to-enable-the-oms-agent-for-linux-to-communicate-with-operations-manager"></a><span data-ttu-id="645e3-386">Pour permettre à l’Agent OMS pour Linux de communiquer avec Operations Manager</span><span class="sxs-lookup"><span data-stu-id="645e3-386">To enable the OMS Agent for Linux to communicate with Operations Manager</span></span>
1. <span data-ttu-id="645e3-387">Modifiez le fichier /etc/opt/omi/conf/omiserver.conf.</span><span class="sxs-lookup"><span data-stu-id="645e3-387">Edit the file /etc/opt/omi/conf/omiserver.conf</span></span>
2. <span data-ttu-id="645e3-388">Vérifiez que la ligne commençant par **httpsport =** spécifie le port 1270.</span><span class="sxs-lookup"><span data-stu-id="645e3-388">Ensure that the line beginning with **httpsport=** defines the port 1270.</span></span> <span data-ttu-id="645e3-389">Par exemple `httpsport=1270`</span><span class="sxs-lookup"><span data-stu-id="645e3-389">Such as `httpsport=1270`</span></span>
3. <span data-ttu-id="645e3-390">Redémarrez le serveur OMI.</span><span class="sxs-lookup"><span data-stu-id="645e3-390">Restart the OMI server:</span></span>

    ```
    sudo /opt/omi/bin/service_control restart
    ```

## <a name="database-permissions-required-for-mysql-performance-counters"></a><span data-ttu-id="645e3-391">Autorisations de base de données requises par l’utilisateur MySQL pour collecter les données de performances de MySQL Server</span><span class="sxs-lookup"><span data-stu-id="645e3-391">Database permissions required for MySQL performance counters</span></span>
<span data-ttu-id="645e3-392">Pour accorder des autorisations à un utilisateur surveillant MySQL, l’utilisateur doit posséder l’autorisation « GRANT option », ainsi que l’autorisation accordée.</span><span class="sxs-lookup"><span data-stu-id="645e3-392">To grant permissions to a MySQL monitoring user, the granting user must have the 'GRANT option' privilege as well as the privilege being granted.</span></span>

<span data-ttu-id="645e3-393">Pour que l’utilisateur MySQL renvoie les données de performances, il doit accéder aux requêtes suivantes :</span><span class="sxs-lookup"><span data-stu-id="645e3-393">In order for the MySQL User to return performance data the user will need access to the following queries:</span></span>

```
SHOW GLOBAL STATUS;
SHOW GLOBAL VARIABLES:
```

<span data-ttu-id="645e3-394">Outre ces requêtes, l’utilisateur de MySQL requiert un accès SELECT aux tables par défaut suivantes :</span><span class="sxs-lookup"><span data-stu-id="645e3-394">In addition to these queries the MySQL user requires SELECT access to the following default tables:</span></span>

* <span data-ttu-id="645e3-395">information_schema</span><span class="sxs-lookup"><span data-stu-id="645e3-395">information_schema</span></span>
* <span data-ttu-id="645e3-396">mysql</span><span class="sxs-lookup"><span data-stu-id="645e3-396">mysql</span></span>

<span data-ttu-id="645e3-397">Ces privilèges peuvent être accordés à l’aide des commandes Grant suivantes.</span><span class="sxs-lookup"><span data-stu-id="645e3-397">These privileges can be granted by running the following grant commands.</span></span>

```
GRANT SELECT ON information_schema.* TO ‘monuser’@’localhost’;
GRANT SELECT ON mysql.* TO ‘monuser’@’localhost’;
```

## <a name="manage-mysql-monitoring-credentials-in-the-authentication-file"></a><span data-ttu-id="645e3-398">Gérer des informations d’identification de surveillance de MySQL dans le fichier d’authentification</span><span class="sxs-lookup"><span data-stu-id="645e3-398">Manage MySQL monitoring credentials in the authentication file</span></span>
<span data-ttu-id="645e3-399">Les sections suivantes vous aident à gérer les informations d’identification de MySQL.</span><span class="sxs-lookup"><span data-stu-id="645e3-399">The following sections help you manage MySQL credentials.</span></span>

### <a name="configure-the-mysql-omi-provider"></a><span data-ttu-id="645e3-400">Configurer le fournisseur OMI de MySQL</span><span class="sxs-lookup"><span data-stu-id="645e3-400">Configure the MySQL OMI provider</span></span>
<span data-ttu-id="645e3-401">Le fournisseur OMI de MySQL nécessite un utilisateur MySQL préconfiguré et des bibliothèques clientes MySQL installées pour interroger les informations d’intégrité et de performances de l’instance MySQL.</span><span class="sxs-lookup"><span data-stu-id="645e3-401">The MySQL OMI provider requires a preconfigured MySQL user and installed MySQL client libraries in order to query the performance/health information from the MySQL instance.</span></span>

### <a name="mysql-omi-authentication-file"></a><span data-ttu-id="645e3-402">Fichier d’authentification OMI de MySQL</span><span class="sxs-lookup"><span data-stu-id="645e3-402">MySQL OMI authentication file</span></span>
<span data-ttu-id="645e3-403">Le fournisseur OMI de MySQL utilise un fichier d’authentification pour déterminer l’adresse de liaison et le port écouté par l’instance MySQL, ainsi que les informations d’identification à utiliser pour collecter des mesures.</span><span class="sxs-lookup"><span data-stu-id="645e3-403">MySQL OMI provider uses an authentication file to determine what bind-address and port the MySQL instance is listening on and what credentials to use to gather metrics.</span></span> <span data-ttu-id="645e3-404">Pendant l’installation, le fournisseur OMI de MySQL recherche dans les fichiers de configuration my.cnf (emplacements par défaut) l’adresse de liaison et le port, et configure partiellement le fichier d’authentification OMI de MySQL.</span><span class="sxs-lookup"><span data-stu-id="645e3-404">During installation the MySQL OMI provider will scan MySQL my.cnf configuration files (default locations) for bind-address and port and partially set the MySQL OMI authentication file.</span></span>

<span data-ttu-id="645e3-405">Pour surveiller une instance de serveur MySQL, ajoutez un fichier d’authentification OMI MySQL prégénéré dans le répertoire correct.</span><span class="sxs-lookup"><span data-stu-id="645e3-405">To complete monitoring of a MySQL server instance, add a pre-generated MySQL OMI authentication file into the correct directory.</span></span>

### <a name="authentication-file-format"></a><span data-ttu-id="645e3-406">Format du fichier d’authentification</span><span class="sxs-lookup"><span data-stu-id="645e3-406">Authentication file format</span></span>
<span data-ttu-id="645e3-407">Le fichier d’authentification OMI de MySQL est un fichier texte qui contient les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="645e3-407">The MySQL OMI authentication file is a text file that contains information about:</span></span>

* <span data-ttu-id="645e3-408">Port</span><span class="sxs-lookup"><span data-stu-id="645e3-408">Port</span></span>
* <span data-ttu-id="645e3-409">Adresse de liaison</span><span class="sxs-lookup"><span data-stu-id="645e3-409">Bind-Address</span></span>
* <span data-ttu-id="645e3-410">Nom d’utilisateur MySQL</span><span class="sxs-lookup"><span data-stu-id="645e3-410">MySQL username</span></span>
* <span data-ttu-id="645e3-411">Mot de passe encodé en base 64</span><span class="sxs-lookup"><span data-stu-id="645e3-411">Base64 encoded password</span></span>

<span data-ttu-id="645e3-412">Le fichier d’authentification OMI de MySQL n’accorde que des droits de lecture/écriture à l’utilisateur de Linux qui l’a généré.</span><span class="sxs-lookup"><span data-stu-id="645e3-412">The MySQL OMI authentication file only grants privileges for read/write to the Linux user that generated it.</span></span>

```
[Port]=[Bind-Address], [username], [Base64 encoded Password]
(Port)=(Bind-Address), (username), (Base64 encoded Password)
(Port)=(Bind-Address), (username), (Base64 encoded Password)
AutoUpdate=[true|false]
```

<span data-ttu-id="645e3-413">Un fichier d’authentification OMI de MySQL par défaut contient une instance et un numéro de port par défaut, selon les informations disponibles et analysées dans le fichier de configuration MySQL trouvé.</span><span class="sxs-lookup"><span data-stu-id="645e3-413">A default MySQL OMI authentication file contains a default instance and a port number depending on what information is available and parsed from the found MySQL configuration file.</span></span>

<span data-ttu-id="645e3-414">L’instance par défaut est un moyen pour faciliter la gestion de plusieurs instances MySQL sur un hôte Linux et est représentée par l’instance avec le port 0.</span><span class="sxs-lookup"><span data-stu-id="645e3-414">The default instance is a means to make managing multiple MySQL instances on one Linux host easier, and is denoted by the instance with port 0.</span></span> <span data-ttu-id="645e3-415">Toutes les instances ajoutées hériteront des propriétés de l’instance par défaut.</span><span class="sxs-lookup"><span data-stu-id="645e3-415">All added instances will inherit properties set from the default instance.</span></span> <span data-ttu-id="645e3-416">Par exemple, si l’instance MySQL à l’écoute du port 3308 est ajoutée, l’adresse de liaison, le nom d’utilisateur et le mot de passe encodé en base 64 de l’instance par défaut sont utilisés pour tester et surveiller l’instance à l’écoute de 3308.</span><span class="sxs-lookup"><span data-stu-id="645e3-416">For example, if MySQL instance listening on port '3308' is added, the default instance's bind-address, username, and Base64 encoded password will be used to try and monitor the instance listening on 3308.</span></span> <span data-ttu-id="645e3-417">Si l’instance sur 3308 est liée à une autre adresse et utilise les mêmes nom d’utilisateur et mot de passe MySQL, seule la répétition de l’adresse de liaison est nécessaire. Les autres propriétés seront héritées.</span><span class="sxs-lookup"><span data-stu-id="645e3-417">If the instance on 3308 is binded to another address and uses the same MySQL username and password pair only the respecification of the bind-address is needed and the other properties will be inherited.</span></span>

<span data-ttu-id="645e3-418">Voici à quoi peuvent ressembler des fichiers d’authentification.</span><span class="sxs-lookup"><span data-stu-id="645e3-418">Examples of the authentication file resemble the following.</span></span>

<span data-ttu-id="645e3-419">Instance par défaut et instance avec port 3308 :</span><span class="sxs-lookup"><span data-stu-id="645e3-419">Default instance and instance with port 3308:</span></span>

```
0=127.0.0.1, myuser, cnBwdA==3308=, ,AutoUpdate=true
```

<span data-ttu-id="645e3-420">Instance par défaut et instance avec port 3308 + mot de passe différent encodé en base 64 :</span><span class="sxs-lookup"><span data-stu-id="645e3-420">Default instance and instance with port 3308 + different Base 64 encoded password:</span></span>

```
0=127.0.0.1, myuser, cnBwdA==3308=127.0.1.1, , AutoUpdate=true
```


| <span data-ttu-id="645e3-421">**Propriété**</span><span class="sxs-lookup"><span data-stu-id="645e3-421">**Property**</span></span> | <span data-ttu-id="645e3-422">**Description**</span><span class="sxs-lookup"><span data-stu-id="645e3-422">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="645e3-423">Port</span><span class="sxs-lookup"><span data-stu-id="645e3-423">Port</span></span> |<span data-ttu-id="645e3-424">Le port représente le port actif écouté par l’instance MySQL.</span><span class="sxs-lookup"><span data-stu-id="645e3-424">Port represents the current port the MySQL instance is listening on.</span></span>  <span data-ttu-id="645e3-425">Le port 0 implique que les propriétés suivantes sont utilisées pour l’instance par défaut.</span><span class="sxs-lookup"><span data-stu-id="645e3-425">The port 0 implies that the properties following are used for default instance.</span></span> |
| <span data-ttu-id="645e3-426">Adresse de liaison</span><span class="sxs-lookup"><span data-stu-id="645e3-426">Bind-Address</span></span> |<span data-ttu-id="645e3-427">Cette adresse est l’adresse de liaison MySQL actuelle.</span><span class="sxs-lookup"><span data-stu-id="645e3-427">the Bind Address is the current MySQL bind-address</span></span> |
| <span data-ttu-id="645e3-428">username</span><span class="sxs-lookup"><span data-stu-id="645e3-428">username</span></span> |<span data-ttu-id="645e3-429">Il s’agit du nom d’utilisateur MySQL que vous souhaitez utiliser pour surveiller l’instance de serveur MySQL.</span><span class="sxs-lookup"><span data-stu-id="645e3-429">This the username of the MySQL user you wish to use to monitor the MySQL server instance.</span></span> |
| <span data-ttu-id="645e3-430">Mot de passe encodé en base 64</span><span class="sxs-lookup"><span data-stu-id="645e3-430">Base64 encoded Password</span></span> |<span data-ttu-id="645e3-431">Il s’agit du mot de passe encodé en base 64, de l’utilisateur surveillant MySQL.</span><span class="sxs-lookup"><span data-stu-id="645e3-431">This is the password of the MySQL monitoring user encoded in Base64.</span></span> |
| <span data-ttu-id="645e3-432">AutoUpdate</span><span class="sxs-lookup"><span data-stu-id="645e3-432">AutoUpdate</span></span> |<span data-ttu-id="645e3-433">Lors de sa mise à niveau, le fournisseur OMI de MySQL recherche les modifications dans le fichier my.cnf et remplace le fichier d’authentification OMI de MySQL.</span><span class="sxs-lookup"><span data-stu-id="645e3-433">When the MySQL OMI Provider is upgraded the provider will rescan for changes in the my.cnf file and overwrite the MySQL OMI Authentication file.</span></span> <span data-ttu-id="645e3-434">Activez (True) ou désactivez (False) cet indicateur selon que le fichier d’authentification OMI de MySQL requiert ou non des mises à jour.</span><span class="sxs-lookup"><span data-stu-id="645e3-434">Set this flag to true or false depending on required updates to the MySQL OMI authentication file.</span></span> |

#### <a name="authentication-file-location"></a><span data-ttu-id="645e3-435">Emplacement du fichier d’authentification</span><span class="sxs-lookup"><span data-stu-id="645e3-435">Authentication file location</span></span>
<span data-ttu-id="645e3-436">Le fichier d’authentification OMI de MySQL doit être situé à l’emplacement suivant et s’appeler « mysql-auth » :</span><span class="sxs-lookup"><span data-stu-id="645e3-436">The MySQL OMI Authentication File should be located in the following location and named "mysql-auth":</span></span>

<span data-ttu-id="645e3-437">/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth</span><span class="sxs-lookup"><span data-stu-id="645e3-437">/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth</span></span>

<span data-ttu-id="645e3-438">L’utilisateur omsagent doit posséder le fichier (ou le répertoire auth/omsagent).</span><span class="sxs-lookup"><span data-stu-id="645e3-438">The file (and auth/omsagent directory) should be owned by the omsagent user.</span></span>

## <a name="agent-logs"></a><span data-ttu-id="645e3-439">Journaux de l’agent</span><span class="sxs-lookup"><span data-stu-id="645e3-439">Agent logs</span></span>
<span data-ttu-id="645e3-440">Les journaux de l’Agent OMS pour Linux se trouvent à l’emplacement suivant :</span><span class="sxs-lookup"><span data-stu-id="645e3-440">The logs for the OMS Agent for Linux is at:</span></span>

<span data-ttu-id="645e3-441">/var/opt/microsoft/omsagent/&lt;workspace id&gt;/log/</span><span class="sxs-lookup"><span data-stu-id="645e3-441">/var/opt/microsoft/omsagent/&lt;workspace id&gt;/log/</span></span>

<span data-ttu-id="645e3-442">Les journaux de l’Agent OMS pour Linux pour le programme omsconfig (configuration de l’agent) se trouvent à l’emplacement suivant :</span><span class="sxs-lookup"><span data-stu-id="645e3-442">The logs for the OMS Agent for Linux for omsconfig (agent configuration) program is at:</span></span>

<span data-ttu-id="645e3-443">/var/opt/microsoft/omsconfig/log/</span><span class="sxs-lookup"><span data-stu-id="645e3-443">/var/opt/microsoft/omsconfig/log/</span></span>

<span data-ttu-id="645e3-444">Les journaux des composants OMI et SCX (qui fournissent des données de mesures de performances) se trouvent à l’emplacement suivant :</span><span class="sxs-lookup"><span data-stu-id="645e3-444">Logs for the OMI and SCX components (which provide performance metrics data) is at:</span></span>

<span data-ttu-id="645e3-445">/var/opt/omi/log/ et /var/opt/microsoft/scx/log</span><span class="sxs-lookup"><span data-stu-id="645e3-445">/var/opt/omi/log/ and /var/opt/microsoft/scx/log</span></span>

## <a name="troubleshooting-the-oms-agent-for-linux"></a><span data-ttu-id="645e3-446">Résolution de problèmes de l’Agent OMS pour Linux</span><span class="sxs-lookup"><span data-stu-id="645e3-446">Troubleshooting the OMS Agent for Linux</span></span>
<span data-ttu-id="645e3-447">Pour diagnostiquer et résoudre des problèmes courants, utilisez les informations suivantes.</span><span class="sxs-lookup"><span data-stu-id="645e3-447">Use the following information to diagnose and troubleshoot common issues.</span></span>

<span data-ttu-id="645e3-448">Si aucune des informations de résolution de problèmes de cette section ne vous est utile, les ressources suivantes peuvent également vous aider à résoudre votre problème.</span><span class="sxs-lookup"><span data-stu-id="645e3-448">If none of the troubleshooting information in this section helps you, you can also use the following resources to help resolve your problem.</span></span>

* <span data-ttu-id="645e3-449">Les clients bénéficiant du Support Premier peuvent soumettre un cas de support via le site [Premier](https://premier.microsoft.com/)</span><span class="sxs-lookup"><span data-stu-id="645e3-449">Customers with Premier support can log a support case via [Premier](https://premier.microsoft.com/)</span></span>
* <span data-ttu-id="645e3-450">Les clients titulaires d’un contrat de support Azure peuvent soumettre des cas de support via le [portail Azure](https://manage.windowsazure.com/?getsupport=true)</span><span class="sxs-lookup"><span data-stu-id="645e3-450">Customers with Azure support agreements can log support cases in the [Azure portal](https://manage.windowsazure.com/?getsupport=true)</span></span>
* <span data-ttu-id="645e3-451">Déposer un [problème GitHub](https://github.com/Microsoft/OMS-Agent-for-Linux/issues)</span><span class="sxs-lookup"><span data-stu-id="645e3-451">File a [GitHub Issue](https://github.com/Microsoft/OMS-Agent-for-Linux/issues)</span></span>
* <span data-ttu-id="645e3-452">Forum de commentaires pour formuler des idées et créer des rapports de bogue [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)</span><span class="sxs-lookup"><span data-stu-id="645e3-452">Feedback forum for ideas and to create a bug report [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)</span></span>

### <a name="important-log-locations"></a><span data-ttu-id="645e3-453">Emplacement de journaux importants</span><span class="sxs-lookup"><span data-stu-id="645e3-453">Important log locations</span></span>
| <span data-ttu-id="645e3-454">Fichier</span><span class="sxs-lookup"><span data-stu-id="645e3-454">File</span></span> | <span data-ttu-id="645e3-455">Chemin</span><span class="sxs-lookup"><span data-stu-id="645e3-455">Path</span></span> |
| --- | --- |
| <span data-ttu-id="645e3-456">Fichier journal de l’Agent OMS pour Linux</span><span class="sxs-lookup"><span data-stu-id="645e3-456">OMS Agent for Linux Log File</span></span> |`/var/opt/microsoft/omsagent/<workspace id>/log/omsagent.log ` |
| <span data-ttu-id="645e3-457">Fichier journal de configuration de l’Agent OMS</span><span class="sxs-lookup"><span data-stu-id="645e3-457">OMS Agent Configuration Log File</span></span> |`/var/opt/microsoft/omsconfig/omsconfig.log` |

### <a name="important-configuration-files"></a><span data-ttu-id="645e3-458">Fichiers de configuration importants</span><span class="sxs-lookup"><span data-stu-id="645e3-458">Important configuration files</span></span>
| <span data-ttu-id="645e3-459">Catégorie</span><span class="sxs-lookup"><span data-stu-id="645e3-459">Catergory</span></span> | <span data-ttu-id="645e3-460">Emplacement du fichier</span><span class="sxs-lookup"><span data-stu-id="645e3-460">File Location</span></span> |
| --- | --- |
| <span data-ttu-id="645e3-461">syslog</span><span class="sxs-lookup"><span data-stu-id="645e3-461">Syslog</span></span> |<span data-ttu-id="645e3-462">`/etc/syslog-ng/syslog-ng.conf` ou `/etc/rsyslog.conf` ou `/etc/rsyslog.d/95-omsagent.conf`</span><span class="sxs-lookup"><span data-stu-id="645e3-462">`/etc/syslog-ng/syslog-ng.conf` or `/etc/rsyslog.conf` or `/etc/rsyslog.d/95-omsagent.conf`</span></span> |
| <span data-ttu-id="645e3-463">Performances, Nagios, Zabbix, sortie OMS et agent général</span><span class="sxs-lookup"><span data-stu-id="645e3-463">Performance, Nagios, Zabbix, OMS output and general agent</span></span> |`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` |
| <span data-ttu-id="645e3-464">Configurations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="645e3-464">Additional configurations</span></span> |`/etc/opt/microsoft/omsagent/<workspace id>/omsagent.d/*.conf` |

> [!NOTE]
> <span data-ttu-id="645e3-465">Les fichiers de changement de configuration pour les compteurs de performances et Syslog sont remplacés si la Configuration du portail OMS est activée.</span><span class="sxs-lookup"><span data-stu-id="645e3-465">Editing configuration files for performance counters and syslog are overwritten if OMS Portal Configuration is enabled.</span></span> <span data-ttu-id="645e3-466">Vous pouvez désactiver la configuration sur le portail OMS pour tous les nœuds ou un seul d’entre eux en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="645e3-466">You can disable configuration in the OMS Portal (for all nodes) or for single nodes by running the following:</span></span>
>
>

```
sudo su omsagent -c /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```


### <a name="enable-debug-logging"></a><span data-ttu-id="645e3-467">Activer l’enregistrement du débogage</span><span class="sxs-lookup"><span data-stu-id="645e3-467">Enable debug logging</span></span>
<span data-ttu-id="645e3-468">Pour activer l’enregistrement du débogage, vous pouvez utiliser le plug-in de sortie OMS et une sortie détaillée.</span><span class="sxs-lookup"><span data-stu-id="645e3-468">To enable debug logging, you can use the OMS output plugin and verbose output.</span></span>

#### <a name="oms-output-plugin"></a><span data-ttu-id="645e3-469">Plug-in de sortie OMS</span><span class="sxs-lookup"><span data-stu-id="645e3-469">OMS output plugin</span></span>
<span data-ttu-id="645e3-470">FluentD permet au plug-in de spécifier des niveaux de journalisation pour différents niveaux du journal en relation avec les entrées et sorties.</span><span class="sxs-lookup"><span data-stu-id="645e3-470">FluentD allows the plugin to specify logging levels for different log levels for inputs and outputs.</span></span> <span data-ttu-id="645e3-471">Pour spécifier un autre niveau du journal pour une sortie OMS, modifiez la configuration générale de l’agent dans le fichier `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`.</span><span class="sxs-lookup"><span data-stu-id="645e3-471">To specify a different log level for OMS output, edit the general agent configuration in the `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` file.</span></span>

<span data-ttu-id="645e3-472">Près du bas du fichier de configuration, modifiez la propriété `log_level` de `info` en `debug`.</span><span class="sxs-lookup"><span data-stu-id="645e3-472">Near the bottom of the configuration file, change the `log_level` property from `info` to `debug`.</span></span>

 ```
 <match oms.** docker.**>
  type out_oms
  log_level debug
  num_threads 5
  buffer_chunk_limit 5m
  buffer_type file
  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms*.buffer
  buffer_queue_limit 10
  flush_interval 20s
  retry_limit 10
  retry_wait 30s
</match>
 ```

<span data-ttu-id="645e3-473">La journalisation du débogage vous permet de voir les chargements par lot sur le Service OMS, répartis par type, nombre d’éléments de données et temps d’envoi.</span><span class="sxs-lookup"><span data-stu-id="645e3-473">Debug logging allows you to see batched uploads to the OMS Service separated by type, number of data items, and time taken to send.</span></span>

<span data-ttu-id="645e3-474">*Exemple de journal activé pour le débogage :*</span><span class="sxs-lookup"><span data-stu-id="645e3-474">*Example debug enabled log:*</span></span>

```
Success sending oms.nagios x 1 in 0.14s
Success sending oms.omi x 4 in 0.52s
Success sending oms.syslog.authpriv.info x 1 in 0.91s
```

#### <a name="verbose-output"></a><span data-ttu-id="645e3-475">Sortie détaillée.</span><span class="sxs-lookup"><span data-stu-id="645e3-475">Verbose output</span></span>
<span data-ttu-id="645e3-476">Au lieu d’utiliser le plug-in de sortie OMS, vous pouvez acheminer les éléments de données directement vers `stdout`, qui est visible dans le fichier journal de l’Agent OMS pour Linux.</span><span class="sxs-lookup"><span data-stu-id="645e3-476">Instead of using the OMS output plugin, you can also output data items directly to `stdout`, which is visible in the OMS Agent for Linux log file.</span></span>

<span data-ttu-id="645e3-477">Dans le fichier de configuration générale de l’Agent OMS sur `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, commentez le plug-in de sortie OMS en ajoutant le symbole `#` au début de chaque ligne.</span><span class="sxs-lookup"><span data-stu-id="645e3-477">In the OMS general agent configuration file at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, comment-out the OMS output plugin by adding a `#` in front of each line.</span></span>

```
#<match oms.** docker.**>
#  type out_oms
#  log_level info
#  num_threads 5
#  buffer_chunk_limit 5m
#  buffer_type file
#  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms*.buffer
#  buffer_queue_limit 10
#  flush_interval 20s
#  retry_limit 10
#  retry_wait 30s
#</match>
```

<span data-ttu-id="645e3-478">Sous le plug-in de sortie, retirez le commentaire de la section suivante en supprimant le symbole `#` au début de chaque ligne.</span><span class="sxs-lookup"><span data-stu-id="645e3-478">Below the output plugin, remove the comment in the following section by removing the `#` symbol at the beginning of each line.</span></span>

```
<match **>
  type stdout
</match>
```

### <a name="forwarded-syslog-messages-do-not-appear-in-the-log"></a><span data-ttu-id="645e3-479">Les messages Syslog transférés n’apparaissent pas dans le journal</span><span class="sxs-lookup"><span data-stu-id="645e3-479">Forwarded Syslog messages do not appear in the log</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="645e3-480">Causes probables</span><span class="sxs-lookup"><span data-stu-id="645e3-480">Probable causes</span></span>
* <span data-ttu-id="645e3-481">La configuration appliquée au serveur Linux n’autorise pas la collecte des fonctionnalités et/ou niveaux du journal envoyés.</span><span class="sxs-lookup"><span data-stu-id="645e3-481">The configuration applied to the Linux server does not allow collection of the sent facilities and/or log levels</span></span>
* <span data-ttu-id="645e3-482">Le message Syslog n’est pas transmis correctement au serveur Linux.</span><span class="sxs-lookup"><span data-stu-id="645e3-482">Syslog is not being forwarded correctly to the Linux server</span></span>
* <span data-ttu-id="645e3-483">Le nombre de messages transmis par seconde est trop élevé pour être géré avec la configuration de base de l’Agent OMS pour Linux.</span><span class="sxs-lookup"><span data-stu-id="645e3-483">The number of messages being forwarded per second are too large for the base configuration of the OMS Agent for Linux to handle</span></span>

#### <a name="resolutions"></a><span data-ttu-id="645e3-484">Résolutions</span><span class="sxs-lookup"><span data-stu-id="645e3-484">Resolutions</span></span>
* <span data-ttu-id="645e3-485">Vérifiez que la configuration du portail OMS pour Syslog possède toutes les fonctionnalités nécessaires et les niveaux du journal corrects.</span><span class="sxs-lookup"><span data-stu-id="645e3-485">Verify that the configuration in the OMS Portal for Syslog has all the facilities and the correct log levels</span></span>
  * <span data-ttu-id="645e3-486">**Portail OMS > Paramètres > Données > Syslog**</span><span class="sxs-lookup"><span data-stu-id="645e3-486">**OMS Portal > Settings > Data > Syslog**</span></span>
* <span data-ttu-id="645e3-487">Vérifiez que les démons de messagerie Syslog natifs (`rsyslog`, `syslog-ng`) sont en mesure de recevoir les messages transférés.</span><span class="sxs-lookup"><span data-stu-id="645e3-487">Verify that native syslog messaging daemons (`rsyslog`, `syslog-ng`) are able to receive the forwarded messages</span></span>
* <span data-ttu-id="645e3-488">Vérifiez les paramètres de pare-feu sur le serveur Syslog pour vous assurer que les messages ne sont pas bloqués.</span><span class="sxs-lookup"><span data-stu-id="645e3-488">Check firewall settings on the Syslog server to ensure that messages are not being blocked</span></span>
* <span data-ttu-id="645e3-489">Simulez un message Syslog à OMS à l’aide de la commande `logger`. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="645e3-489">Simulate a Syslog message to OMS using the `logger` command - for example:</span></span>
  * `logger -p local0.err "This is my test message"`

### <a name="problems-connecting-to-oms-when-using-a-proxy"></a><span data-ttu-id="645e3-490">Problèmes de connexion à OMS lors de l’utilisation d’un proxy</span><span class="sxs-lookup"><span data-stu-id="645e3-490">Problems connecting to OMS when using a proxy</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="645e3-491">Causes probables</span><span class="sxs-lookup"><span data-stu-id="645e3-491">Probable causes</span></span>
* <span data-ttu-id="645e3-492">Le proxy spécifié lors de l’installation et la configuration de l’agent est incorrect.</span><span class="sxs-lookup"><span data-stu-id="645e3-492">The proxy specified when installing and configuring the agent is incorrect</span></span>
* <span data-ttu-id="645e3-493">Les points de terminaison du Service OMS ne sont pas approuvés dans votre centre de données.</span><span class="sxs-lookup"><span data-stu-id="645e3-493">The OMS Service endpoints are not whitelistested in your datacenter</span></span>

#### <a name="resolutions"></a><span data-ttu-id="645e3-494">Résolutions</span><span class="sxs-lookup"><span data-stu-id="645e3-494">Resolutions</span></span>
* <span data-ttu-id="645e3-495">Réinstallez l’Agent OMS pour Linux à l’aide de la commande suivante avec l’option `-v` activée.</span><span class="sxs-lookup"><span data-stu-id="645e3-495">Reinstall the OMS Agent for Linux using the following command with the option `-v` enabled.</span></span> <span data-ttu-id="645e3-496">Cela autorise une sortie détaillée de l’agent qui se connecte via le proxy au Service OMS.</span><span class="sxs-lookup"><span data-stu-id="645e3-496">This allows verbose output of the agent connecting through the proxy to the OMS Service.</span></span>
  * `/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`
  * <span data-ttu-id="645e3-497">Consultez la documentation relative au proxy d’OMS fournie dans la rubrique [Configuring the agent for use with an HTTP proxy server](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server) (Configuration de l’agent pour une utilisation avec un serveur proxy HTTP).</span><span class="sxs-lookup"><span data-stu-id="645e3-497">Review the documentation for OMS proxy at [Configuring the agent for use with an HTTP proxy server](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server)</span></span>
* <span data-ttu-id="645e3-498">Vérifiez que les points de terminaison du Service OMS suivants sont approuvés.</span><span class="sxs-lookup"><span data-stu-id="645e3-498">Verify that the following OMS Service endpoints are whitelisted</span></span>

| <span data-ttu-id="645e3-499">Ressource de l'agent</span><span class="sxs-lookup"><span data-stu-id="645e3-499">Agent Resource</span></span> | <span data-ttu-id="645e3-500">Ports</span><span class="sxs-lookup"><span data-stu-id="645e3-500">Ports</span></span> |
| --- | --- |
| <span data-ttu-id="645e3-501">&#42;.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="645e3-501">&#42;.ods.opinsights.azure.com</span></span> |<span data-ttu-id="645e3-502">Port 443</span><span class="sxs-lookup"><span data-stu-id="645e3-502">Port 443</span></span> |
| <span data-ttu-id="645e3-503">&#42;.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="645e3-503">&#42;.oms.opinsights.azure.com</span></span> |<span data-ttu-id="645e3-504">Port 443</span><span class="sxs-lookup"><span data-stu-id="645e3-504">Port 443</span></span> |
| <span data-ttu-id="645e3-505">ods.systemcenteradvisor.com</span><span class="sxs-lookup"><span data-stu-id="645e3-505">ods.systemcenteradvisor.com</span></span> |<span data-ttu-id="645e3-506">Port 443</span><span class="sxs-lookup"><span data-stu-id="645e3-506">Port 443</span></span> |
| <span data-ttu-id="645e3-507">&#42;.blob.core.windows.net/</span><span class="sxs-lookup"><span data-stu-id="645e3-507">&#42;.blob.core.windows.net/</span></span> |<span data-ttu-id="645e3-508">Port 443</span><span class="sxs-lookup"><span data-stu-id="645e3-508">Port 443</span></span> |

### <a name="a-403-error-is-displayed-when-onboarding"></a><span data-ttu-id="645e3-509">Une erreur 403 s’affiche lors de l’intégration</span><span class="sxs-lookup"><span data-stu-id="645e3-509">A 403 error is displayed when onboarding</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="645e3-510">Causes probables</span><span class="sxs-lookup"><span data-stu-id="645e3-510">Probable causes</span></span>
* <span data-ttu-id="645e3-511">La date et l’heure sont incorrectes sur le serveur Linux.</span><span class="sxs-lookup"><span data-stu-id="645e3-511">The date and time are incorrect on Linux Server</span></span>
* <span data-ttu-id="645e3-512">L’ID et la clé d’espace de travail utilisés sont incorrects.</span><span class="sxs-lookup"><span data-stu-id="645e3-512">The Workspace ID and Workspace Key used are incorrect</span></span>

#### <a name="resolution"></a><span data-ttu-id="645e3-513">Résolution :</span><span class="sxs-lookup"><span data-stu-id="645e3-513">Resolution</span></span>
* <span data-ttu-id="645e3-514">Vérifiez l’heure sur votre serveur Linux avec la commande `date`.</span><span class="sxs-lookup"><span data-stu-id="645e3-514">Verify the time on your Linux server with the `date` command.</span></span> <span data-ttu-id="645e3-515">Si les données sont postérieures ou antérieures de 15 minutes par rapport à l’heure actuelle, l’intégration échoue.</span><span class="sxs-lookup"><span data-stu-id="645e3-515">If the data is greater than or less than 15 minutes from the current time, then onboarding fails.</span></span> <span data-ttu-id="645e3-516">Pour corriger ce problème, mettez à jour de la date et/ou le fuseau horaire de votre serveur Linux.</span><span class="sxs-lookup"><span data-stu-id="645e3-516">To correct this, update the date and/or timezone of your Linux server.</span></span>
* <span data-ttu-id="645e3-517">La dernière version de l’Agent OMS pour Linux vous avertit si un décalage horaire entraîne l’échec de l’intégration.</span><span class="sxs-lookup"><span data-stu-id="645e3-517">The latest version of the OMS Agent for Linux notifies you if a time difference is causing onboarding failure</span></span>
* <span data-ttu-id="645e3-518">Recommencez l’intégration à l’aide de l’ID et de la clé d’espace de travail corrects.</span><span class="sxs-lookup"><span data-stu-id="645e3-518">Re-onboard using the correct Workspace ID and Workspace Key.</span></span> <span data-ttu-id="645e3-519">Pour plus d’informations, voir [Onboarding using the command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) (Intégration à l’aide de la ligne de commande).</span><span class="sxs-lookup"><span data-stu-id="645e3-519">See  [Onboarding using the command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>

### <a name="a-500-error-or-404-error-appears-in-the-log-file-after-onboarding"></a><span data-ttu-id="645e3-520">Une erreur 500 ou 404 apparaît dans le fichier journal après l’intégration</span><span class="sxs-lookup"><span data-stu-id="645e3-520">A 500 error or 404 error appears in the log file after onboarding</span></span>
<span data-ttu-id="645e3-521">Il s’agit d’un problème connu qui se produit lors du premier chargement de données Linux dans un espace de travail OMS.</span><span class="sxs-lookup"><span data-stu-id="645e3-521">This is a known issue that occurs during the first upload of Linux data into an OMS workspace.</span></span> <span data-ttu-id="645e3-522">Cela n’affecte pas les données envoyées et ne génère pas d’autres problèmes.</span><span class="sxs-lookup"><span data-stu-id="645e3-522">This does not affect data being sent or other problems.</span></span> <span data-ttu-id="645e3-523">Vous pouvez ignorer les erreurs lors de l’intégration initiale.</span><span class="sxs-lookup"><span data-stu-id="645e3-523">You can ignore the errors when initially onboarding.</span></span>

### <a name="nagios-data-does-not-appear-in-the-oms-portal"></a><span data-ttu-id="645e3-524">Les données Nagios n’apparaissant pas dans le portail OMS</span><span class="sxs-lookup"><span data-stu-id="645e3-524">Nagios data does not appear in the OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="645e3-525">Causes probables</span><span class="sxs-lookup"><span data-stu-id="645e3-525">Probable causes</span></span>
* <span data-ttu-id="645e3-526">L’utilisateur omsagent n’a pas les autorisations nécessaires pour lire le fichier journal Nagios.</span><span class="sxs-lookup"><span data-stu-id="645e3-526">The omsagent user does not have permissions to read from the Nagios log file</span></span>
* <span data-ttu-id="645e3-527">Les sections de source et de filtre Nagios sont toujours commentées dans le fichier omsagent.conf.</span><span class="sxs-lookup"><span data-stu-id="645e3-527">The Nagios source and filter sections are still commented in the omsagent.conf file</span></span>

#### <a name="resolutions"></a><span data-ttu-id="645e3-528">Résolutions</span><span class="sxs-lookup"><span data-stu-id="645e3-528">Resolutions</span></span>
* <span data-ttu-id="645e3-529">Ajoutez l’utilisateur omsagent afin de lire à partir du fichier Nagios.</span><span class="sxs-lookup"><span data-stu-id="645e3-529">Add the omsagent user in order to read from the Nagios file.</span></span> <span data-ttu-id="645e3-530">Pour plus d’informations, voir [Nagios alerts](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts) (Alertes Nagios).</span><span class="sxs-lookup"><span data-stu-id="645e3-530">See [Nagios alerts](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts) for more information.</span></span>
* <span data-ttu-id="645e3-531">Dans l’Agent OMS pour le fichier de configuration générale de Linux sur `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, assurez-vous que les commentaires ont été supprimés **des deux** sections de source et de filtre Nagios, comme dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="645e3-531">In the OMS Agent for Linux general configuration file at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, ensure that **both** the Nagios source and filter sections have comments removed, similar to the following example.</span></span>

```
<source>
  type tail
  path /var/log/nagios/nagios.log
  format none
  tag oms.nagios
</source>

<filter oms.nagios>
  type filter_nagios_log
</filter>
```


### <a name="linux-data-doesnt-appear-in-the-oms-portal"></a><span data-ttu-id="645e3-532">Les données Linux n’apparaissent pas dans le portail OMS</span><span class="sxs-lookup"><span data-stu-id="645e3-532">Linux data doesn't appear in the OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="645e3-533">Causes probables</span><span class="sxs-lookup"><span data-stu-id="645e3-533">Probable causes</span></span>
* <span data-ttu-id="645e3-534">L’intégration au Service OMS a échoué.</span><span class="sxs-lookup"><span data-stu-id="645e3-534">Onboarding to the OMS Service failed</span></span>
* <span data-ttu-id="645e3-535">La connexion au Service OMS est bloquée.</span><span class="sxs-lookup"><span data-stu-id="645e3-535">Connection to the OMS Service is blocked</span></span>
* <span data-ttu-id="645e3-536">Les données de l’Agent OMS pour Linux sont sauvegardées.</span><span class="sxs-lookup"><span data-stu-id="645e3-536">The OMS Agent for Linux data is backed-up</span></span>

#### <a name="resolutions"></a><span data-ttu-id="645e3-537">Résolutions</span><span class="sxs-lookup"><span data-stu-id="645e3-537">Resolutions</span></span>
* <span data-ttu-id="645e3-538">Vérifiez que l’intégration au Service OMS a réussi en vous assurant que le fichier `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` existe.</span><span class="sxs-lookup"><span data-stu-id="645e3-538">Verify that onboarding to the OMS Service was successful by verifying that the `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` exists.</span></span>
* <span data-ttu-id="645e3-539">Recommencez l’intégration à l’aide de la ligne de commande omsadmin.sh.</span><span class="sxs-lookup"><span data-stu-id="645e3-539">Re-onboard using the omsadmin.sh command line.</span></span> <span data-ttu-id="645e3-540">Pour plus d’informations, voir [Onboarding using the command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) (Intégration à l’aide de la ligne de commande).</span><span class="sxs-lookup"><span data-stu-id="645e3-540">See [Onboarding using the command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>
* <span data-ttu-id="645e3-541">Si vous utilisez un proxy, suivez les étapes de résolution de problèmes de proxy décrites plus haut.</span><span class="sxs-lookup"><span data-stu-id="645e3-541">If using a proxy, use the proxy troubleshooting steps above</span></span>
* <span data-ttu-id="645e3-542">Dans certains cas, lorsque l’Agent OMS pour Linux ne peut pas communiquer avec le Service OMS, les données de l’Agent sont sauvegardées à la taille de mémoire tampon saturée de 50 Mo.</span><span class="sxs-lookup"><span data-stu-id="645e3-542">In some cases, when the OMS Agent for Linux cannot communicate with the OMS Service, data on the Agent is backed-up to the full buffer size of 50 MB.</span></span> <span data-ttu-id="645e3-543">Redémarrez l’Agent OMS pour Linux en exécutant la commande `/opt/microsoft/omsagent/bin/service_control restart`.</span><span class="sxs-lookup"><span data-stu-id="645e3-543">Restart the OMS Agent for Linux by running the `/opt/microsoft/omsagent/bin/service_control restart` command.</span></span>
  >[AZURE.NOTE] <span data-ttu-id="645e3-544">Ce problème est résolu dans l’Agent version 1.1.0-28 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="645e3-544">This issue is fixed in Agent version 1.1.0-28 and later.</span></span>

### <a name="syslog-linux-performance-counter-configuration-is-not-applied-in-the-oms-portal"></a><span data-ttu-id="645e3-545">La configuration du compteur de performances Syslog Linux n’est pas appliquée dans le portail OMS</span><span class="sxs-lookup"><span data-stu-id="645e3-545">Syslog Linux performance counter configuration is not applied in the OMS portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="645e3-546">Causes probables</span><span class="sxs-lookup"><span data-stu-id="645e3-546">Probable causes</span></span>
* <span data-ttu-id="645e3-547">L’agent de configuration de l’Agent OMS pour Linux n’a pas pu extraire la configuration la plus récente à partir du portail OMS.</span><span class="sxs-lookup"><span data-stu-id="645e3-547">The configuration agent in the OMS Agent for Linux has not retrieved the latest configuration from the OMS portal.</span></span>
* <span data-ttu-id="645e3-548">Les paramètres modifiés dans le portail n’ont pas été appliqués.</span><span class="sxs-lookup"><span data-stu-id="645e3-548">The revised settings in the portal were not applied</span></span>

#### <a name="resolutions"></a><span data-ttu-id="645e3-549">Résolutions</span><span class="sxs-lookup"><span data-stu-id="645e3-549">Resolutions</span></span>
<span data-ttu-id="645e3-550">`omsconfig` est l’agent de configuration de l’Agent OMS pour Linux qui récupère les changements de configuration du portail OMS toutes les 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="645e3-550">`omsconfig` is the configuration agent in the OMS Agent for Linux that retrieves OMS portal configuration changes every 5 minutes.</span></span> <span data-ttu-id="645e3-551">Cette configuration est ensuite appliquée aux fichiers de configuration de l’Agent OMS pour Linux dans `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`.</span><span class="sxs-lookup"><span data-stu-id="645e3-551">This configuration is then applied to the OMS Agent for Linux configuration files located at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`.</span></span>

* <span data-ttu-id="645e3-552">Dans certains cas, l’agent de configuration de l’Agent OMS pour Linux n’est pas en mesure de communiquer avec le service de configuration du portail, de sorte que la configuration la plus récente n’est pas appliquée.</span><span class="sxs-lookup"><span data-stu-id="645e3-552">In some cases, the OMS Agent for Linux configuration agent might not be able to communicate with the portal configuration service resulting in latest configuration not being applied.</span></span>
* <span data-ttu-id="645e3-553">Vérifiez que l’agent `omsconfig` est installé avec les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="645e3-553">Verify that the `omsconfig` agent is installed with the following:</span></span>

  * <span data-ttu-id="645e3-554">`dpkg --list omsconfig` ou `rpm -qi omsconfig`</span><span class="sxs-lookup"><span data-stu-id="645e3-554">`dpkg --list omsconfig` or `rpm -qi omsconfig`</span></span>
  * <span data-ttu-id="645e3-555">S’il n’est pas installé, réinstallez la dernière version de l’Agent OMS pour Linux.</span><span class="sxs-lookup"><span data-stu-id="645e3-555">If not installed, reinstall the latest version of the OMS Agent for Linux</span></span>
* <span data-ttu-id="645e3-556">Vérifiez que l’agent `omsconfig` peut communiquer avec le Service OMS.</span><span class="sxs-lookup"><span data-stu-id="645e3-556">Verify that the `omsconfig` agent can communicate with the OMS service</span></span>

  * <span data-ttu-id="645e3-557">Exécutez la commande `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'`.</span><span class="sxs-lookup"><span data-stu-id="645e3-557">Run the `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` command</span></span>
    * <span data-ttu-id="645e3-558">La commande ci-dessus retourne la configuration que l’agent récupère à partir du portail, dont les paramètres Syslog, les compteurs de performances Linux et les journaux personnalisés</span><span class="sxs-lookup"><span data-stu-id="645e3-558">The command above returns the configuration that agent retrieves from the portal, including Syslog settings, Linux performance counters, and custom logs</span></span>
    * <span data-ttu-id="645e3-559">En cas d’échec de la commande ci-dessus, exécutez la commande `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py`.</span><span class="sxs-lookup"><span data-stu-id="645e3-559">If the command above fails, run the `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` command.</span></span> <span data-ttu-id="645e3-560">Cette commande force l’agent omsconfig à communiquer avec le Service OMS pour récupérer la configuration la plus récente.</span><span class="sxs-lookup"><span data-stu-id="645e3-560">This command forces the omsconfig agent to communicate with the OMS service to retrieve the latest configuration.</span></span>

### <a name="custom-linux-log-data-does-not-appear-in-the-oms-portal"></a><span data-ttu-id="645e3-561">Les données du journal Linux personnalisé n’apparaissent pas sur le portail OMS</span><span class="sxs-lookup"><span data-stu-id="645e3-561">Custom Linux log data does not appear in the OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="645e3-562">Causes probables</span><span class="sxs-lookup"><span data-stu-id="645e3-562">Probable causes</span></span>
* <span data-ttu-id="645e3-563">L’intégration au Service OMS a échoué.</span><span class="sxs-lookup"><span data-stu-id="645e3-563">Onboarding to OMS Service failed</span></span>
* <span data-ttu-id="645e3-564">Le paramètre **Appliquer la configuration suivante à mes serveurs Linux** n’a pas été sélectionné.</span><span class="sxs-lookup"><span data-stu-id="645e3-564">The **Apply the following configuration to my Linux Servers** setting has not been selected</span></span>
* <span data-ttu-id="645e3-565">L’agent omsconfig n’a pas récupéré le dernier journal personnalisé sur le portail.</span><span class="sxs-lookup"><span data-stu-id="645e3-565">omsconfig has not picked up the latest custom log from the portal</span></span>
* <span data-ttu-id="645e3-566">Le programme `omsagent` ne peut pas accéder au journal personnalisé en raison d’un problème d’autorisation ou parce que le programme `omsagent` est introuvable.</span><span class="sxs-lookup"><span data-stu-id="645e3-566">The `omsagent` use is unable to access the custom log due to a permissions problem or `omsagent` was not found.</span></span> <span data-ttu-id="645e3-567">Dans ce cas, la sortie suivante s’affiche :</span><span class="sxs-lookup"><span data-stu-id="645e3-567">In this case, you'll see the following output:</span></span>
  * `[DATETIME] [warn]: file not found. Continuing without tailing it.`
  * `[DATETIME] [error]: file not accessible by omsagent.`
* <span data-ttu-id="645e3-568">Il s’agit d’un problème connu lié à la condition de concurrence, qui a été résolu dans l’Agent OMS pour Linux version 1.1.0-217.</span><span class="sxs-lookup"><span data-stu-id="645e3-568">This is a known issue with the Race Condition that was fixed in the OMS Agent for Linux version 1.1.0-217</span></span>

#### <a name="resolutions"></a><span data-ttu-id="645e3-569">Résolutions</span><span class="sxs-lookup"><span data-stu-id="645e3-569">Resolutions</span></span>
* <span data-ttu-id="645e3-570">Vérifiez que vous avez correctement effectué l’intégration en déterminant si le fichier `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` existe.</span><span class="sxs-lookup"><span data-stu-id="645e3-570">Verify that you've successfully onboarded, by determining whether the `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` file exists.</span></span>
  * <span data-ttu-id="645e3-571">Si nécessaire, recommencez l’intégration à l’aide de la ligne de commande omsadmin.sh.</span><span class="sxs-lookup"><span data-stu-id="645e3-571">If needed, onboard again using the omsadmin.sh command line.</span></span> <span data-ttu-id="645e3-572">Pour plus d’informations, voir [Onboarding using the command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) (Intégration à l’aide de la ligne de commande).</span><span class="sxs-lookup"><span data-stu-id="645e3-572">See [Onboarding using the command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>
* <span data-ttu-id="645e3-573">Sur le portail OMS, dans **Paramètres** sous l’onglet **Données**, vérifiez que l’option **Appliquer la configuration suivante à mes serveurs Linux** est activée.</span><span class="sxs-lookup"><span data-stu-id="645e3-573">In the OMS Portal, under **Settings** on the **Data** tab, ensure that the **Apply the following configuration to my Linux Servers** setting is selected</span></span>  
  <span data-ttu-id="645e3-574">![appliquer la configuration](./media/log-analytics-linux-agents/customloglinuxenabled.png)</span><span class="sxs-lookup"><span data-stu-id="645e3-574">![apply configuration](./media/log-analytics-linux-agents/customloglinuxenabled.png)</span></span>
* <span data-ttu-id="645e3-575">Vérifiez que l’agent `omsconfig` peut communiquer avec le Service OMS.</span><span class="sxs-lookup"><span data-stu-id="645e3-575">Verify that the `omsconfig` agent can communicate with the OMS service</span></span>

  * <span data-ttu-id="645e3-576">Exécutez la commande `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'`.</span><span class="sxs-lookup"><span data-stu-id="645e3-576">Run the `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` command</span></span>
  * <span data-ttu-id="645e3-577">La commande ci-dessus retourne la configuration que l’agent récupère à partir du portail, dont les paramètres Syslog, les compteurs de performances Linux et les journaux personnalisés.</span><span class="sxs-lookup"><span data-stu-id="645e3-577">The command above returns the configuration that agent retrieves from the Portal, including Syslog settings, Linux performance counters, and custom Logs</span></span>
  * <span data-ttu-id="645e3-578">En cas d’échec de la commande ci-dessus, exécutez la commande `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py`.</span><span class="sxs-lookup"><span data-stu-id="645e3-578">If the command above fails, run the `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` command.</span></span> <span data-ttu-id="645e3-579">Cette commande force l’agent omsconfig à communiquer avec le Service OMS pour récupérer la configuration la plus récente.</span><span class="sxs-lookup"><span data-stu-id="645e3-579">This command forces the omsconfig agent to communicate with OMS service and retrieve the latest configuration.</span></span>

<span data-ttu-id="645e3-580">Au lieu que l’utilisateur de l’Agent OMS pour Linux opère en tant qu’utilisateur `root` privilégié, l’Agent OMS pour Linux opère en tant qu’utilisateur `omsagent` .</span><span class="sxs-lookup"><span data-stu-id="645e3-580">Instead of the OMS Agent for Linux user running as a privileged user `root`, the OMS Agent for Linux runs as the `omsagent` user.</span></span> <span data-ttu-id="645e3-581">Dans la plupart des cas, une autorisation explicite doit être accordée à l’utilisateur pour la lecture de certains fichiers.</span><span class="sxs-lookup"><span data-stu-id="645e3-581">In most cases, explicit permission must be granted to the user in order to read certain files.</span></span>

<span data-ttu-id="645e3-582">Pour accorder l’autorisation à l’utilisateur `omsagent`, exécutez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="645e3-582">To grant permission to `omsagent` user, run the following commands:</span></span>

1. <span data-ttu-id="645e3-583">Ajoutez l’utilisateur `omsagent` à un groupe spécifique avec `sudo usermod -a -G <GROUPNAME> <USERNAME>`.</span><span class="sxs-lookup"><span data-stu-id="645e3-583">Add the `omsagent` user to a specific group with `sudo usermod -a -G <GROUPNAME> <USERNAME>`</span></span>
2. <span data-ttu-id="645e3-584">Accordez l’accès en lecture universel au fichier requis avec `sudo chmod -R ugo+rw <FILE DIRECTORY>`.</span><span class="sxs-lookup"><span data-stu-id="645e3-584">Grant universal read access to the required file with `sudo chmod -R ugo+rw <FILE DIRECTORY>`</span></span>

<span data-ttu-id="645e3-585">Il existe un problème connu lié à la condition de concurrence, qui a été résolu dans l’Agent OMS pour Linux version 1.1.0-217.</span><span class="sxs-lookup"><span data-stu-id="645e3-585">There is a known issue with the Race Condition that was fixed in the OMS Agent for Linux version 1.1.0-217.</span></span> <span data-ttu-id="645e3-586">Après mise à jour vers le dernier agent, exécutez la commande suivante pour obtenir la dernière version du plug-in de sortie :</span><span class="sxs-lookup"><span data-stu-id="645e3-586">After updating to the latest agent, run the following command to get the latest version of the output plugin:</span></span>

```
sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf
```

## <a name="known-limitations"></a><span data-ttu-id="645e3-587">Limites connues</span><span class="sxs-lookup"><span data-stu-id="645e3-587">Known limitations</span></span>
<span data-ttu-id="645e3-588">Consultez les sections suivantes pour en savoir plus sur les limites actuelles de l’Agent OMS pour Linux.</span><span class="sxs-lookup"><span data-stu-id="645e3-588">Review the following sections to learn about current limitations of the OMS Agent for Linux.</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="645e3-589">Azure Diagnostics</span><span class="sxs-lookup"><span data-stu-id="645e3-589">Azure Diagnostics</span></span>
<span data-ttu-id="645e3-590">Pour les machines virtuelles Linux s’exécutant dans Azure, des étapes supplémentaires peuvent être nécessaires pour permettre la collecte des données par Azure Diagnostics et Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="645e3-590">For Linux virtual machines running in Azure, additional steps may be required to allow data collection by Azure Diagnostics and Operations Management Suite.</span></span> <span data-ttu-id="645e3-591">**version 2.2** d’Extension Diagnostics pour Linux est nécessaire pour la compatibilité avec l’Agent OMS pour Linux.</span><span class="sxs-lookup"><span data-stu-id="645e3-591">**Version 2.2** of the Diagnostics Extension for Linux is required for compatibility with the OMS Agent for Linux.</span></span>

<span data-ttu-id="645e3-592">Pour plus d’informations sur l’installation et la configuration de l’Extension Diagnostics pour Linux, voir [Utiliser la commande de l’interface de ligne de commande Azure afin d’activer l’extension de diagnostic Linux](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension).</span><span class="sxs-lookup"><span data-stu-id="645e3-592">For more information on installing and configuring the Diagnostic Extension for Linux, see [Use the Azure CLI command to enable Linux Diagnostic Extension](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension).</span></span>

<span data-ttu-id="645e3-593">**Mise à niveau de l’Extension Diagnostics pour Linux 2.0 vers 2.2 avec l’interface de ligne de commande Azure en mode ASM :**</span><span class="sxs-lookup"><span data-stu-id="645e3-593">**Upgrading the Linux Diagnostics Extension from 2.0 to 2.2 Azure CLI ASM:**</span></span>

```
azure vm extension set -u <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.0
azure vm extension set <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

<span data-ttu-id="645e3-594">**ARM**</span><span class="sxs-lookup"><span data-stu-id="645e3-594">**ARM**</span></span>

```
azure vm extension set -u <resource-group> <vm-name> Microsoft.Insights.VMDiagnosticsSettings Microsoft.OSTCExtensions 2.0
azure vm extension set <resource-group> <vm-name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

<span data-ttu-id="645e3-595">Ces exemples de commandes font référence à un fichier nommé PrivateConfig.json.</span><span class="sxs-lookup"><span data-stu-id="645e3-595">These command examples reference a file named PrivateConfig.json.</span></span> <span data-ttu-id="645e3-596">Le format de ce fichier doit ressembler à l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="645e3-596">The format of that file should resemble the following sample.</span></span>

```
    {
    "storageAccountName":"the storage account to receive data",
    "storageAccountKey":"the key of the account"
    }
```

### <a name="sysklog-is-not-supported"></a><span data-ttu-id="645e3-597">Sysklog n’est pas pris en charge</span><span class="sxs-lookup"><span data-stu-id="645e3-597">Sysklog is not supported</span></span>
<span data-ttu-id="645e3-598">rsyslog ou syslog-ng est requis pour collecter les messages syslog.</span><span class="sxs-lookup"><span data-stu-id="645e3-598">Either rsyslog or syslog-ng are required to collect syslog messages.</span></span> <span data-ttu-id="645e3-599">Le démon syslog par défaut sur la version 5 de Red Hat Enterprise Linux, CentOS et Oracle Linux (sysklog) ne prend pas en charge la collecte des événements syslog.</span><span class="sxs-lookup"><span data-stu-id="645e3-599">The default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="645e3-600">Pour collecter les données syslog avec cette version de ces distributions, le démon rsyslog doit être installé et configuré à la place de sysklog.</span><span class="sxs-lookup"><span data-stu-id="645e3-600">To collect syslog data from this version of these distributions, the rsyslog daemon should be installed and configured to replace sysklog.</span></span> <span data-ttu-id="645e3-601">Pour plus d’informations sur le remplacement de sysklog par rsyslog, consultez [Install the newly built rsyslog RPM](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM).</span><span class="sxs-lookup"><span data-stu-id="645e3-601">For more information on replacing sysklog with rsyslog, see [Install the newly built rsyslog RPM](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM).</span></span>

## <a name="next-steps"></a><span data-ttu-id="645e3-602">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="645e3-602">Next Steps</span></span>
* <span data-ttu-id="645e3-603">[Ajoutez des solutions Log Analytics à partir de la galerie de solutions](log-analytics-add-solutions.md) pour ajouter des fonctionnalités et collecter des données.</span><span class="sxs-lookup"><span data-stu-id="645e3-603">[Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md) to add functionality and gather data.</span></span>
* <span data-ttu-id="645e3-604">Familiarisez-vous avec les [recherches de journal](log-analytics-log-searches.md) pour afficher les informations détaillées collectées par les solutions.</span><span class="sxs-lookup"><span data-stu-id="645e3-604">Get familiar with [log searches](log-analytics-log-searches.md) to view detailed information gathered by solutions.</span></span>
* <span data-ttu-id="645e3-605">Utilisez les [tableaux de bord](log-analytics-dashboards.md) pour enregistrer et afficher vos propres recherches personnalisées.</span><span class="sxs-lookup"><span data-stu-id="645e3-605">Use [dashboards](log-analytics-dashboards.md) to save and display your own custom searches.</span></span>
