---
redirect_url: /azure/log-analytics/log-analytics-agent-linux
redirect_document_id: True
ROBOTS: NOINDEX
ms.openlocfilehash: 8b526144cd565f6750368e12970f008e66cc2023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-linux-computers-toolog-analytics"></a><span data-ttu-id="52385-101">Se connecter à votre tooLog d’ordinateurs Linux Analytique</span><span class="sxs-lookup"><span data-stu-id="52385-101">Connect your Linux computers tooLog Analytics</span></span>
<span data-ttu-id="52385-102">Avec Log Analytics, vous pouvez collecter et exploiter les données générées par des ordinateurs Linux.</span><span class="sxs-lookup"><span data-stu-id="52385-102">Using Log Analytics, you can collect and act on data generated from Linux computers.</span></span> <span data-ttu-id="52385-103">Ajout des données collectées à partir de Linux tooOMS vous permet de toomanage les systèmes Linux et les solutions de conteneur comme Docker, quel que soit l’endroit où se trouvent vos ordinateurs, virtuellement n’importe où.</span><span class="sxs-lookup"><span data-stu-id="52385-103">Adding data collected from Linux tooOMS allows you toomanage Linux systems and container solutions like Docker, regardless of where your computers are located — virtually anywhere.</span></span> <span data-ttu-id="52385-104">Sources de données peuvent résider dans votre centre de données local en tant que serveurs physiques, des ordinateurs virtuels dans un service hébergé dans le cloud, comme Amazon Web Services (AWS) ou Microsoft Azure, ou même hello ordinateur portable sur votre bureau.</span><span class="sxs-lookup"><span data-stu-id="52385-104">Data sources might reside in your on-premises datacenter as physical servers, virtual computers in a cloud-hosted service like Amazon Web Services (AWS) or Microsoft Azure, or even hello laptop on your desk.</span></span> <span data-ttu-id="52385-105">De plus, OMS collecte les données des ordinateurs Windows de la même façon, prenant en charge un véritable environnement informatique hybride.</span><span class="sxs-lookup"><span data-stu-id="52385-105">In addition, OMS also collects data from Windows computers similarly, so it supports a truly hybrid IT environment.</span></span>

<span data-ttu-id="52385-106">Vous pouvez afficher et gérer les données de toutes ces sources avec Log Analytics dans OMS, via un portail unique.</span><span class="sxs-lookup"><span data-stu-id="52385-106">You can view and manage data from all of those sources with Log Analytics in OMS with a single management portal.</span></span> <span data-ttu-id="52385-107">Ceci réduit le besoin de hello toomonitor à l’aide de différents systèmes et les rend facile tooconsume, et vous pouvez exporter les données de votre choix toowhatever business analytique solution ou du système que vous avez déjà.</span><span class="sxs-lookup"><span data-stu-id="52385-107">This reduces hello need toomonitor it using many different systems, makes it easy tooconsume, and you can export any data you like toowhatever business analytics solution or system that you already have.</span></span>

<span data-ttu-id="52385-108">Cet article est un guide de démarrage rapide qui vous permet de collecter et de gérer les données de vos ordinateurs Linux à l’aide de hello Agent OMS pour Linux.</span><span class="sxs-lookup"><span data-stu-id="52385-108">This article is a quick start guide that will help you collect and manage data for your Linux computers using hello OMS Agent for Linux.</span></span> <span data-ttu-id="52385-109">Pour obtenir des détails plus techniques, tels que la configuration du serveur proxy, des informations sur les mesures CollectD, et des sources de données JSON personnalisées, consultez la [présentation de l’Agent OMS pour Linux](https://github.com/Microsoft/OMS-Agent-for-Linux) (en anglais) et la [documentation complète de l’Agent OMS pour Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md) (en anglais) sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="52385-109">For more technical details such as proxy server configuration, information about CollectD metrics, and custom JSON data sources, you’ll find that information at [OMS Agent for Linux overview](https://github.com/Microsoft/OMS-Agent-for-Linux) and [OMS Agent for Linux full documentation](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md) on GitHub.</span></span>

<span data-ttu-id="52385-110">Actuellement, vous pouvez collecter hello suivant les types de données à partir d’ordinateurs Linux :</span><span class="sxs-lookup"><span data-stu-id="52385-110">Currently, you can collect hello following types of data from Linux computers:</span></span>

* <span data-ttu-id="52385-111">Mesures de performances</span><span class="sxs-lookup"><span data-stu-id="52385-111">Performance metrics</span></span>
* <span data-ttu-id="52385-112">Événements Syslog</span><span class="sxs-lookup"><span data-stu-id="52385-112">Syslog events</span></span>
* <span data-ttu-id="52385-113">Alertes de Nagios et Zabbix</span><span class="sxs-lookup"><span data-stu-id="52385-113">Alerts from Nagios and Zabbix</span></span>
* <span data-ttu-id="52385-114">Journaux, inventaire et mesures de performances du conteneur Docker</span><span class="sxs-lookup"><span data-stu-id="52385-114">Docker container performance metrics, inventory and logs</span></span>

## <a name="supported-linux-versions"></a><span data-ttu-id="52385-115">Versions de Linux prises en charge</span><span class="sxs-lookup"><span data-stu-id="52385-115">Supported Linux versions</span></span>
<span data-ttu-id="52385-116">Les versions x86 et x64 sont officiellement prises en charge sur diverses distributions de Linux.</span><span class="sxs-lookup"><span data-stu-id="52385-116">Both x86 and x64 versions are officially supported on a variety of Linux distributions.</span></span> <span data-ttu-id="52385-117">Toutefois, hello Agent OMS pour Linux peut également s’exécuter sur les autres distributions non répertoriées.</span><span class="sxs-lookup"><span data-stu-id="52385-117">However, hello OMS Agent for Linux might also run on other distributions not listed.</span></span>

* <span data-ttu-id="52385-118">Amazon Linux 2012.09 à 2015.09</span><span class="sxs-lookup"><span data-stu-id="52385-118">Amazon Linux 2012.09 through 2015.09</span></span>
* <span data-ttu-id="52385-119">CentOS Linux 5, 6 et 7</span><span class="sxs-lookup"><span data-stu-id="52385-119">CentOS Linux 5, 6, and 7</span></span>
* <span data-ttu-id="52385-120">Oracle Linux 5, 6 et 7</span><span class="sxs-lookup"><span data-stu-id="52385-120">Oracle Linux 5, 6, and 7</span></span>
* <span data-ttu-id="52385-121">Red Hat Enterprise Linux Server 5, 6 et 7</span><span class="sxs-lookup"><span data-stu-id="52385-121">Red Hat Enterprise Linux Server 5, 6 and 7</span></span>
* <span data-ttu-id="52385-122">Debian GNU/Linux 6, 7 et 8</span><span class="sxs-lookup"><span data-stu-id="52385-122">Debian GNU/Linux 6, 7, and 8</span></span>
* <span data-ttu-id="52385-123">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10</span><span class="sxs-lookup"><span data-stu-id="52385-123">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10</span></span>
* <span data-ttu-id="52385-124">SUSE Linux Enterprise Server 11 et 12</span><span class="sxs-lookup"><span data-stu-id="52385-124">SUSE Linux Enterprise Server 11 and 12</span></span>

## <a name="oms-agent-for-linux"></a><span data-ttu-id="52385-125">Agent OMS pour Linux</span><span class="sxs-lookup"><span data-stu-id="52385-125">OMS Agent for Linux</span></span>
<span data-ttu-id="52385-126">Hello Operations Management Suite Agent pour Linux comprend plusieurs packages.</span><span class="sxs-lookup"><span data-stu-id="52385-126">hello Operations Management Suite Agent for Linux comprises multiple packages.</span></span> <span data-ttu-id="52385-127">fichier de la version Hello contient hello suivant des packages, disponibles en cours d’exécution offre groupée du noyau hello avec `--extract`.</span><span class="sxs-lookup"><span data-stu-id="52385-127">hello release file contains hello following packages, available by running hello shell bundle with `--extract`.</span></span>

| <span data-ttu-id="52385-128">**Package**</span><span class="sxs-lookup"><span data-stu-id="52385-128">**Package**</span></span> | <span data-ttu-id="52385-129">**Version**</span><span class="sxs-lookup"><span data-stu-id="52385-129">**Version**</span></span> | <span data-ttu-id="52385-130">**Description**</span><span class="sxs-lookup"><span data-stu-id="52385-130">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="52385-131">omsagent</span><span class="sxs-lookup"><span data-stu-id="52385-131">omsagent</span></span> |<span data-ttu-id="52385-132">1.1.0</span><span class="sxs-lookup"><span data-stu-id="52385-132">1.1.0</span></span> |<span data-ttu-id="52385-133">Hello Operations Management Suite Agent pour Linux</span><span class="sxs-lookup"><span data-stu-id="52385-133">hello Operations Management Suite Agent for Linux</span></span> |
| <span data-ttu-id="52385-134">omsconfig</span><span class="sxs-lookup"><span data-stu-id="52385-134">omsconfig</span></span> |<span data-ttu-id="52385-135">1.1.1</span><span class="sxs-lookup"><span data-stu-id="52385-135">1.1.1</span></span> |<span data-ttu-id="52385-136">Agent de configuration pour hello Agent OMS</span><span class="sxs-lookup"><span data-stu-id="52385-136">Configuration agent for hello OMS Agent</span></span> |
| <span data-ttu-id="52385-137">omi</span><span class="sxs-lookup"><span data-stu-id="52385-137">omi</span></span> |<span data-ttu-id="52385-138">1.0.8.3</span><span class="sxs-lookup"><span data-stu-id="52385-138">1.0.8.3</span></span> |<span data-ttu-id="52385-139">Open Management Infrastructure (OMI) - Serveur CIM léger</span><span class="sxs-lookup"><span data-stu-id="52385-139">Open Management Infrastructure (OMI) -- a lightweight CIM Server</span></span> |
| <span data-ttu-id="52385-140">scx</span><span class="sxs-lookup"><span data-stu-id="52385-140">scx</span></span> |<span data-ttu-id="52385-141">1.6.2</span><span class="sxs-lookup"><span data-stu-id="52385-141">1.6.2</span></span> |<span data-ttu-id="52385-142">Fournisseurs CIM OMI pour les mesures de performances des systèmes d’exploitation</span><span class="sxs-lookup"><span data-stu-id="52385-142">OMI CIM Providers for operating system performance metrics</span></span> |
| <span data-ttu-id="52385-143">apache-cimprov</span><span class="sxs-lookup"><span data-stu-id="52385-143">apache-cimprov</span></span> |<span data-ttu-id="52385-144">1.0.0</span><span class="sxs-lookup"><span data-stu-id="52385-144">1.0.0</span></span> |<span data-ttu-id="52385-145">Fournisseur de surveillance des performances d’Apache HTTP Server pour OMI.</span><span class="sxs-lookup"><span data-stu-id="52385-145">Apache HTTP Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="52385-146">Installé uniquement si Apache HTTP Server est détecté.</span><span class="sxs-lookup"><span data-stu-id="52385-146">Only installed if Apache HTTP Server is detected.</span></span> |
| <span data-ttu-id="52385-147">mysql-cimprov</span><span class="sxs-lookup"><span data-stu-id="52385-147">mysql-cimprov</span></span> |<span data-ttu-id="52385-148">1.0.0</span><span class="sxs-lookup"><span data-stu-id="52385-148">1.0.0</span></span> |<span data-ttu-id="52385-149">Fournisseur de surveillance des performances de MySQL Server pour OMI.</span><span class="sxs-lookup"><span data-stu-id="52385-149">MySQL Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="52385-150">Installé uniquement si MySQL/MariaDB Server est détecté.</span><span class="sxs-lookup"><span data-stu-id="52385-150">Only installed if MySQL/MariaDB server is detected.</span></span> |
| <span data-ttu-id="52385-151">docker-cimprov</span><span class="sxs-lookup"><span data-stu-id="52385-151">docker-cimprov</span></span> |<span data-ttu-id="52385-152">0.1.0</span><span class="sxs-lookup"><span data-stu-id="52385-152">0.1.0</span></span> |<span data-ttu-id="52385-153">Fournisseur de Docker pour OMI.</span><span class="sxs-lookup"><span data-stu-id="52385-153">Docker provider for OMI.</span></span> <span data-ttu-id="52385-154">Installé uniquement si Docker est détecté.</span><span class="sxs-lookup"><span data-stu-id="52385-154">Only installed if Docker is detected.</span></span> |

### <a name="additional-installation-artifacts"></a><span data-ttu-id="52385-155">Artefacts d’installation supplémentaires</span><span class="sxs-lookup"><span data-stu-id="52385-155">Additional installation artifacts</span></span>
<span data-ttu-id="52385-156">Après avoir installé l’agent OMS de hello pour les packages Linux, hello les modifications de système de configuration supplémentaires suivantes sont appliquées.</span><span class="sxs-lookup"><span data-stu-id="52385-156">After installing hello OMS agent for Linux packages, hello following additional system-wide configuration changes are applied.</span></span> <span data-ttu-id="52385-157">Ces artefacts sont supprimés lors de la désinstallation du package omsagent hello.</span><span class="sxs-lookup"><span data-stu-id="52385-157">These artifacts are removed when hello omsagent package is uninstalled.</span></span>

* <span data-ttu-id="52385-158">Un utilisateur sans privilège nommé `omsagent` est créé.</span><span class="sxs-lookup"><span data-stu-id="52385-158">A non-privileged user named: `omsagent` is created.</span></span> <span data-ttu-id="52385-159">Il s’agit hello compte hello omsagent démon exécute en tant que</span><span class="sxs-lookup"><span data-stu-id="52385-159">This is hello account hello omsagent daemon runs as</span></span>
* <span data-ttu-id="52385-160">Un fichier « include » de programmes sudo est créé à /etc/sudoers.d/omsagent ce qui autorise omsagent toorestart hello syslog et omsagent démons.</span><span class="sxs-lookup"><span data-stu-id="52385-160">A sudoers “include” file is created at /etc/sudoers.d/omsagent This authorizes omsagent toorestart hello syslog and omsagent daemons.</span></span> <span data-ttu-id="52385-161">Si les directives « include » de sudo ne sont pas pris en charge dans la version installée de hello de sudo, ces entrées sont écrites trop/etc/programmes sudo.</span><span class="sxs-lookup"><span data-stu-id="52385-161">If sudo “include” directives are not supported in hello installed version of sudo, these entries will be written too/etc/sudoers.</span></span>
* <span data-ttu-id="52385-162">configuration de syslog Hello est modifié tooforward un sous-ensemble de l’agent de toohello d’événements.</span><span class="sxs-lookup"><span data-stu-id="52385-162">hello syslog configuration is modified tooforward a subset of events toohello agent.</span></span> <span data-ttu-id="52385-163">Pour plus d’informations, consultez hello **collecte des données de configuration de** section ci-dessous</span><span class="sxs-lookup"><span data-stu-id="52385-163">For more information, see hello **Configuring Data Collection** section below</span></span>

### <a name="linux-data-collection-details"></a><span data-ttu-id="52385-164">Détails sur la collecte de données Linux</span><span class="sxs-lookup"><span data-stu-id="52385-164">Linux data collection details</span></span>
<span data-ttu-id="52385-165">Hello tableau suivant présente les méthodes de collecte de données et d’autres détails sur la façon dont les données sont collectées.</span><span class="sxs-lookup"><span data-stu-id="52385-165">hello following table shows data collection methods and other details about how data is collected.</span></span>

| <span data-ttu-id="52385-166">source</span><span class="sxs-lookup"><span data-stu-id="52385-166">source</span></span> | <span data-ttu-id="52385-167">Agent direct</span><span class="sxs-lookup"><span data-stu-id="52385-167">Direct Agent</span></span> | <span data-ttu-id="52385-168">Agent SCOM</span><span class="sxs-lookup"><span data-stu-id="52385-168">SCOM agent</span></span> | <span data-ttu-id="52385-169">Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="52385-169">Azure Storage</span></span> | <span data-ttu-id="52385-170">SCOM requis ?</span><span class="sxs-lookup"><span data-stu-id="52385-170">SCOM required?</span></span> | <span data-ttu-id="52385-171">Données de l’agent SCOM envoyées via un groupe d’administration</span><span class="sxs-lookup"><span data-stu-id="52385-171">SCOM agent data sent via management group</span></span> | <span data-ttu-id="52385-172">Fréquence de collecte</span><span class="sxs-lookup"><span data-stu-id="52385-172">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="52385-173">Zabbix</span><span class="sxs-lookup"><span data-stu-id="52385-173">Zabbix</span></span> |![Oui](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="52385-179">1 minute</span><span class="sxs-lookup"><span data-stu-id="52385-179">1 minute</span></span> |
| <span data-ttu-id="52385-180">Nagios</span><span class="sxs-lookup"><span data-stu-id="52385-180">Nagios</span></span> |![Oui](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="52385-186">À l’arrivée</span><span class="sxs-lookup"><span data-stu-id="52385-186">on arrival</span></span> |
| <span data-ttu-id="52385-187">syslog</span><span class="sxs-lookup"><span data-stu-id="52385-187">syslog</span></span> |![Oui](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="52385-193">Depuis Azure Storage : 10 minutes ; depuis l’agent : à l’arrivée</span><span class="sxs-lookup"><span data-stu-id="52385-193">from Azure storage: 10 minutes; from agent: on arrival</span></span> |
| <span data-ttu-id="52385-194">Compteurs de performances Linux</span><span class="sxs-lookup"><span data-stu-id="52385-194">Linux performance counters</span></span> |![Oui](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="52385-200">Comme prévu, minimum de 10 secondes</span><span class="sxs-lookup"><span data-stu-id="52385-200">As scheduled, minimum of 10 seconds</span></span> |
| <span data-ttu-id="52385-201">Suivi des modifications</span><span class="sxs-lookup"><span data-stu-id="52385-201">change tracking</span></span> |![Oui](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |<span data-ttu-id="52385-207">Toutes les heures</span><span class="sxs-lookup"><span data-stu-id="52385-207">hourly</span></span> |

### <a name="package-requirements"></a><span data-ttu-id="52385-208">Packages requis</span><span class="sxs-lookup"><span data-stu-id="52385-208">Package Requirements</span></span>
| <span data-ttu-id="52385-209">**Package requis**</span><span class="sxs-lookup"><span data-stu-id="52385-209">**Required package**</span></span> | <span data-ttu-id="52385-210">**Description**</span><span class="sxs-lookup"><span data-stu-id="52385-210">**Description**</span></span> | <span data-ttu-id="52385-211">**Version minimum**</span><span class="sxs-lookup"><span data-stu-id="52385-211">**Minimum version**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="52385-212">Glibc</span><span class="sxs-lookup"><span data-stu-id="52385-212">Glibc</span></span> |<span data-ttu-id="52385-213">Bibliothèque C de GNU</span><span class="sxs-lookup"><span data-stu-id="52385-213">GNU C library</span></span> |<span data-ttu-id="52385-214">2.5-12</span><span class="sxs-lookup"><span data-stu-id="52385-214">2.5-12</span></span> |
| <span data-ttu-id="52385-215">Openssl</span><span class="sxs-lookup"><span data-stu-id="52385-215">Openssl</span></span> |<span data-ttu-id="52385-216">Bibliothèques OpenSSL</span><span class="sxs-lookup"><span data-stu-id="52385-216">OpenSSL libraries</span></span> |<span data-ttu-id="52385-217">0.9.8e ou 1.0</span><span class="sxs-lookup"><span data-stu-id="52385-217">0.9.8e or 1.0</span></span> |
| <span data-ttu-id="52385-218">Curl</span><span class="sxs-lookup"><span data-stu-id="52385-218">Curl</span></span> |<span data-ttu-id="52385-219">Client web cURL</span><span class="sxs-lookup"><span data-stu-id="52385-219">cURL web client</span></span> |<span data-ttu-id="52385-220">7.15.5</span><span class="sxs-lookup"><span data-stu-id="52385-220">7.15.5</span></span> |
| <span data-ttu-id="52385-221">Python-ctypes</span><span class="sxs-lookup"><span data-stu-id="52385-221">Python-ctypes</span></span> |<span data-ttu-id="52385-222">Bibliothèques de fonctions</span><span class="sxs-lookup"><span data-stu-id="52385-222">function libraries</span></span> |<span data-ttu-id="52385-223">n/a</span><span class="sxs-lookup"><span data-stu-id="52385-223">n/a</span></span> |
| <span data-ttu-id="52385-224">PAM</span><span class="sxs-lookup"><span data-stu-id="52385-224">PAM</span></span> |<span data-ttu-id="52385-225">Pluggable Authentication Modules</span><span class="sxs-lookup"><span data-stu-id="52385-225">Pluggable authentication Modules</span></span> |<span data-ttu-id="52385-226">n/a</span><span class="sxs-lookup"><span data-stu-id="52385-226">n/a</span></span> |

> [!NOTE]
> <span data-ttu-id="52385-227">Rsyslog ou syslog-ng est des messages syslog toocollect requis.</span><span class="sxs-lookup"><span data-stu-id="52385-227">Either rsyslog or syslog-ng are required toocollect syslog messages.</span></span> <span data-ttu-id="52385-228">démon syslog par défaut de Hello version 5 de Red Hat Enterprise Linux, CentOS et Oracle Linux (sysklog) n’est pas pris en charge pour la collecte d’événements syslog.</span><span class="sxs-lookup"><span data-stu-id="52385-228">hello default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="52385-229">toocollect les données syslog de cette version de ces distributions, hello rsyslog démon doit être installé et configuré tooreplace sysklog.</span><span class="sxs-lookup"><span data-stu-id="52385-229">toocollect syslog data from this version of these distributions, hello rsyslog daemon should be installed and configured tooreplace sysklog.</span></span>
>
>

## <a name="quick-install"></a><span data-ttu-id="52385-230">Installation rapide</span><span class="sxs-lookup"><span data-stu-id="52385-230">Quick install</span></span>
<span data-ttu-id="52385-231">Exécutez hello suivant de commandes toodownload hello omsagent, valider la somme de contrôle hello, puis installer et l’agent de hello intégré.</span><span class="sxs-lookup"><span data-stu-id="52385-231">Run hello following commands toodownload hello omsagent, validate hello checksum, then  install and onboard hello agent.</span></span> <span data-ttu-id="52385-232">Ces commandes sont de type 64 bits.</span><span class="sxs-lookup"><span data-stu-id="52385-232">Commands are for 64-bit.</span></span> <span data-ttu-id="52385-233">Hello ID de l’espace de travail et la clé primaire sont trouvent dans le portail OMS de hello sous **paramètres** sur hello **Sources connectées** onglet.</span><span class="sxs-lookup"><span data-stu-id="52385-233">hello Workspace ID and Primary Key are found in hello OMS portal under **Settings** on hello **Connected Sources** tab.</span></span>

![détails sur l’espace de travail](./media/log-analytics-linux-agents/oms-direct-agent-primary-key.png)

```
wget https://raw.githubusercontent.com/Microsoft/OMS-Agent-for-Linux/master/installer/scripts/onboard_agent.sh && sh onboard_agent.sh -w <YOUR OMS WORKSPACE ID> -s <YOUR OMS WORKSPACE PRIMARY KEY>
```

<span data-ttu-id="52385-235">Il existe une multitude d’autres tooinstall méthodes hello agent et le mettre à niveau.</span><span class="sxs-lookup"><span data-stu-id="52385-235">There are a variety of other methods tooinstall hello agent and upgrade it.</span></span> <span data-ttu-id="52385-236">Vous pouvez en savoir plus sur ces méthodes dans [hello de tooinstall étapes Agent OMS pour Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux).</span><span class="sxs-lookup"><span data-stu-id="52385-236">You can read more about them at [Steps tooinstall hello OMS Agent for Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux).</span></span>

<span data-ttu-id="52385-237">Vous pouvez également afficher hello [procédure pas à pas vidéo Azure](https://www.youtube.com/watch?v=mF1wtHPEzT0).</span><span class="sxs-lookup"><span data-stu-id="52385-237">You can also view hello [Azure video walkthrough](https://www.youtube.com/watch?v=mF1wtHPEzT0).</span></span>

## <a name="choose-your-linux-data-collection-method"></a><span data-ttu-id="52385-238">Choisir la mode de collecte des données Linux</span><span class="sxs-lookup"><span data-stu-id="52385-238">Choose your Linux data collection method</span></span>
<span data-ttu-id="52385-239">Façon dont vous choisissez hello types de données que vous le feriez comme toocollect varie selon que vous souhaitez toouse du portail OMS hello ou si vous souhaitez modifier différents fichiers de configuration directement sur vos clients Linux.</span><span class="sxs-lookup"><span data-stu-id="52385-239">How you choose hello data types you'd like toocollect depends on whether you want toouse hello OMS portal or if you want edit various configuration files directly on your Linux clients.</span></span> <span data-ttu-id="52385-240">Si vous choisissez de portail de hello toouse, configuration de hello est envoyée automatiquement tooall vos clients Linux.</span><span class="sxs-lookup"><span data-stu-id="52385-240">If you choose toouse hello portal, hello configuration is sent tooall of your Linux clients automatically.</span></span> <span data-ttu-id="52385-241">Si vous avez besoin de configurations différentes pour différents clients Linux, vous avez besoin de fichiers du client tooedit individuellement ou utiliser une solution alternative comme PowerShell DSC, Chef ou Puppet.</span><span class="sxs-lookup"><span data-stu-id="52385-241">If you need different configurations for different Linux clients, you will need tooedit client files individually – or use an alternative like PowerShell DSC, Chef, or Puppet.</span></span>

<span data-ttu-id="52385-242">Vous pouvez spécifier les événements syslog hello et des compteurs de performance que vous souhaitez toocollect à l’aide de fichiers de configuration sur les ordinateurs Linux hello.</span><span class="sxs-lookup"><span data-stu-id="52385-242">You can specify hello syslog events and performance counters that you want toocollect using configuration files on hello Linux computers.</span></span> <span data-ttu-id="52385-243">*Si vous avez choisi de collecte de données tooconfigure en modifiant les fichiers de configuration de l’agent, vous devez désactiver la configuration centralisée de hello.*</span><span class="sxs-lookup"><span data-stu-id="52385-243">*If you chose tooconfigure data collection by editing agent configuration files, you should disable hello centralized configuration.*</span></span>  <span data-ttu-id="52385-244">Les instructions sont fournies ci-dessous tooconfigure collecte des données dans l’agent hello les fichiers de configuration, ainsi que toodisable de configuration centrale pour tous les Agents OMS pour Linux ou des ordinateurs individuels.</span><span class="sxs-lookup"><span data-stu-id="52385-244">Instructions are provided below tooconfigure data collection in hello agent's configuration files as well as toodisable central configuration for all OMS Agents for Linux, or individual computers.</span></span>

### <a name="disable-oms-management-for-an-individual-linux-computer"></a><span data-ttu-id="52385-245">Désactiver la gestion OMS sur un ordinateur Linux</span><span class="sxs-lookup"><span data-stu-id="52385-245">Disable OMS management for an individual Linux computer</span></span>
<span data-ttu-id="52385-246">Collecte centralisée des données de configuration est désactivée pour un ordinateur Linux avec hello du script OMS_MetaConfigHelper.py.</span><span class="sxs-lookup"><span data-stu-id="52385-246">Centralized data collection for configuration data is disabled for an individual Linux computer with hello OMS_MetaConfigHelper.py script.</span></span> <span data-ttu-id="52385-247">Ce script est très utile si quelques ordinateurs requièrent une configuration spéciale.</span><span class="sxs-lookup"><span data-stu-id="52385-247">This can be useful if a subset of computers should have a specialized configuration.</span></span>

<span data-ttu-id="52385-248">toodisable configuration centralisée :</span><span class="sxs-lookup"><span data-stu-id="52385-248">toodisable centralized configuration:</span></span>

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```

<span data-ttu-id="52385-249">toore-activer une configuration centralisée :</span><span class="sxs-lookup"><span data-stu-id="52385-249">toore-enable centralized configuration:</span></span>

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py –enable
```

## <a name="linux-performance-counters"></a><span data-ttu-id="52385-250">Compteurs de performances Linux</span><span class="sxs-lookup"><span data-stu-id="52385-250">Linux performance counters</span></span>
<span data-ttu-id="52385-251">Compteurs de performances Linux sont des compteurs de performances tooWindows similaires, les deux fonctionnent de la même façon.</span><span class="sxs-lookup"><span data-stu-id="52385-251">Linux performance counters are similar tooWindows performance counters—both operate similarly.</span></span> <span data-ttu-id="52385-252">Vous pouvez utiliser hello suivant les procédures tooadd et les configurer.</span><span class="sxs-lookup"><span data-stu-id="52385-252">You can use hello following procedures tooadd and configure them.</span></span> <span data-ttu-id="52385-253">Après que les avoir ajoutés tooOMS, données sont collectées pour ces toutes les 30 secondes.</span><span class="sxs-lookup"><span data-stu-id="52385-253">After they are added tooOMS, data is collected for them every 30 seconds.</span></span>

### <a name="tooadd-a-linux-performance-counter-in-oms"></a><span data-ttu-id="52385-254">tooadd un compteur de performances Linux dans OMS</span><span class="sxs-lookup"><span data-stu-id="52385-254">tooadd a Linux performance counter in OMS</span></span>
1. <span data-ttu-id="52385-255">tooconfigure Agents OMS pour Linux à l’aide du portail OMS hello, vous pouvez ajouter des compteurs de performances Linux dans la page Paramètres de hello, cliquez sur **données**.</span><span class="sxs-lookup"><span data-stu-id="52385-255">tooconfigure OMS Agents for Linux using hello OMS portal, you can add Linux performance counters on hello Settings page, click **Data**.</span></span>  
2. <span data-ttu-id="52385-256">Sur hello **paramètres** page sous **données** , cliquez sur **compteurs de performances Linux** , puis sélectionnez ou tapez hello nom du compteur de hello souhaité tooadd.</span><span class="sxs-lookup"><span data-stu-id="52385-256">On hello **Settings** page under **Data** , click **Linux performance counters** and then select or type hello name of hello counter you want tooadd.</span></span>  
    <span data-ttu-id="52385-257">![données](./media/log-analytics-linux-agents/oms-settings-data01.png)</span><span class="sxs-lookup"><span data-stu-id="52385-257">![data](./media/log-analytics-linux-agents/oms-settings-data01.png)</span></span>
3. <span data-ttu-id="52385-258">Si vous ne connaissez le nom complet de hello du compteur de hello, vous pouvez commencer en tapant un nom partiel, et une liste des compteurs disponibles s’affiche.</span><span class="sxs-lookup"><span data-stu-id="52385-258">If you don't know hello full name of hello counter, you can start typing a partial name and a list of available counters will appear.</span></span> <span data-ttu-id="52385-259">Lorsque vous avez trouvé le compteur de hello vous souhaitez tooadd, cliquez sur nom hello dans la liste de hello puis hello plus hello de tooadd icône compteur.</span><span class="sxs-lookup"><span data-stu-id="52385-259">When you find hello counter you want tooadd, click hello name in hello list and then click hello plus icon tooadd hello counter.</span></span>
4. <span data-ttu-id="52385-260">Après avoir ajouté le compteur de hello, il apparaît dans la liste hello des compteurs mis en surbrillance avec une barre de couleur.</span><span class="sxs-lookup"><span data-stu-id="52385-260">After you add hello counter, it appears in hello list of counters highlighted with a colored bar.</span></span>
5. <span data-ttu-id="52385-261">Par défaut, hello **appliquer machines toomy de configuration ci-dessous** option est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="52385-261">By default, hello **Apply below configuration toomy machines** option is selected.</span></span> <span data-ttu-id="52385-262">Si vous souhaitez toodisable envoi de données de configuration, désactivez la sélection de hello.</span><span class="sxs-lookup"><span data-stu-id="52385-262">If you want toodisable sending configuration data, clear hello selection.</span></span>
6. <span data-ttu-id="52385-263">Lorsque vous avez terminé la modification des compteurs de performance, en bas de hello de page de hello cliquez sur **enregistrer** toofinalize vos modifications.</span><span class="sxs-lookup"><span data-stu-id="52385-263">When you are done modifying performance counters, at hello bottom of hello page click **Save** toofinalize your changes.</span></span> <span data-ttu-id="52385-264">les modifications de configuration Hello que vous avez apportées sont ensuite envoyées tooall hello Agents OMS pour Linux qui sont inscrits auprès d’OMS, généralement dans les 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="52385-264">hello configuration changes that you've made are then sent tooall hello OMS Agents for Linux that are registered with OMS, typically within 5 minutes.</span></span>

### <a name="configure-linux-performance-counters-in-oms"></a><span data-ttu-id="52385-265">Configurer des compteurs de performances Linux dans OMS</span><span class="sxs-lookup"><span data-stu-id="52385-265">Configure Linux performance counters in OMS</span></span>
<span data-ttu-id="52385-266">Pour les compteurs de performances Windows, vous pouvez choisir une instance spécifique de chaque compteur de performances.</span><span class="sxs-lookup"><span data-stu-id="52385-266">For Windows performance counters, you can choose a specific instance for each performance counter.</span></span> <span data-ttu-id="52385-267">Toutefois, pour les compteurs de performances Linux, l’instance de compteur que vous choisissez s’applique ses compteurs enfants tooall compteur parent de hello.</span><span class="sxs-lookup"><span data-stu-id="52385-267">However, for Linux performance counters, whatever instance of a counter that you choose applies tooall child counters of hello parent counter.</span></span> <span data-ttu-id="52385-268">Hello tableau suivant montre les instances courantes hello les compteurs de performances Linux et Windows tooboth disponibles.</span><span class="sxs-lookup"><span data-stu-id="52385-268">hello following table shows hello common instances available tooboth Linux and Windows performance counters.</span></span>

| <span data-ttu-id="52385-269">**Nom de l’instance**</span><span class="sxs-lookup"><span data-stu-id="52385-269">**Instance name**</span></span> | <span data-ttu-id="52385-270">**Signification**</span><span class="sxs-lookup"><span data-stu-id="52385-270">**Meaning**</span></span> |
| --- | --- |
| <span data-ttu-id="52385-271">\_Total</span><span class="sxs-lookup"><span data-stu-id="52385-271">\_Total</span></span> |<span data-ttu-id="52385-272">Nombre total de toutes les instances de hello</span><span class="sxs-lookup"><span data-stu-id="52385-272">Total of all hello instances</span></span> |
| \* |<span data-ttu-id="52385-273">Toutes les instances</span><span class="sxs-lookup"><span data-stu-id="52385-273">All instances</span></span> |
| <span data-ttu-id="52385-274">(/&#124;/var)</span><span class="sxs-lookup"><span data-stu-id="52385-274">(/&#124;/var)</span></span> |<span data-ttu-id="52385-275">Correspond aux instances nommées : / ou /var</span><span class="sxs-lookup"><span data-stu-id="52385-275">Matches instances named: / or /var</span></span> |

<span data-ttu-id="52385-276">De même, intervalle d’échantillonnage hello que vous choisissez pour un compteur parent s’applique tooall ses compteurs enfants.</span><span class="sxs-lookup"><span data-stu-id="52385-276">Similarly, hello sample interval that you choose for a parent counter applies tooall its child counters.</span></span> <span data-ttu-id="52385-277">En d’autres termes, tous les intervalles d’échantillonnage compteur hello enfant et les instances sont tous liés entre eux.</span><span class="sxs-lookup"><span data-stu-id="52385-277">In other words, all hello child counter sample intervals and instances are tied together.</span></span>

### <a name="add-and-configure-performance-metrics-with-linux"></a><span data-ttu-id="52385-278">Ajouter et configurer des mesures de performances avec Linux</span><span class="sxs-lookup"><span data-stu-id="52385-278">Add and configure performance metrics with Linux</span></span>
<span data-ttu-id="52385-279">Toocollect des métriques de performances sont contrôlées par la configuration hello dans/etc/opt/microsoft/omsagent/&lt;id de l’espace de travail&gt;/conf/omsagent.conf.</span><span class="sxs-lookup"><span data-stu-id="52385-279">Performance metrics toocollect are controlled by hello configuration in /etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf.</span></span> <span data-ttu-id="52385-280">Consultez [métriques de performances disponibles](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics) pour connaître les classes et les métriques pour hello Agent OMS pour Linux.</span><span class="sxs-lookup"><span data-stu-id="52385-280">See [Available performance metrics](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics) for available classes and metrics for hello OMS Agent for Linux.</span></span>

<span data-ttu-id="52385-281">Chaque objet ou la catégorie de toocollect des métriques de performances doit être définie dans le fichier de configuration hello en tant qu’un seul `<source>` élément.</span><span class="sxs-lookup"><span data-stu-id="52385-281">Each object, or category, of performance metrics toocollect should be defined in hello configuration file as a single `<source>` element.</span></span> <span data-ttu-id="52385-282">syntaxe de Hello suit le modèle hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="52385-282">hello syntax follows hello pattern below.</span></span>

```
<source>
  type oms_omi  
  object_name "Processor"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

<span data-ttu-id="52385-283">Hello les paramètres configurables de cet élément sont :</span><span class="sxs-lookup"><span data-stu-id="52385-283">hello configurable parameters of this element are:</span></span>

* <span data-ttu-id="52385-284">**Objet\_nom**: nom de l’objet de collection de hello hello.</span><span class="sxs-lookup"><span data-stu-id="52385-284">**Object\_name**: hello object name for hello collection.</span></span>
* <span data-ttu-id="52385-285">**Instance\_regex**: un *expression régulière* définissant l’instances toocollect.</span><span class="sxs-lookup"><span data-stu-id="52385-285">**Instance\_regex**: a *regular expression* defining which instances toocollect.</span></span> <span data-ttu-id="52385-286">valeur de Hello : `.*` spécifie toutes les instances.</span><span class="sxs-lookup"><span data-stu-id="52385-286">hello value: `.*` specifies all instances.</span></span> <span data-ttu-id="52385-287">métriques de processeur toocollect pour hello uniquement \_nombre Total d’instances, vous pouvez spécifier `_Total`.</span><span class="sxs-lookup"><span data-stu-id="52385-287">toocollect processor metrics for only hello \_Total instance, you could specify `_Total`.</span></span> <span data-ttu-id="52385-288">les métriques de processus toocollect pour hello uniquement les instances crond ou sshd uniquement, vous pouvez spécifier : `(crond|sshd)`.</span><span class="sxs-lookup"><span data-stu-id="52385-288">toocollect process metrics for only hello crond or sshd instances, you could specify: `(crond|sshd)`.</span></span>
* <span data-ttu-id="52385-289">**Compteur\_nom\_regex**: un *expression régulière* définissant le toocollect compteurs (pour l’objet de hello).</span><span class="sxs-lookup"><span data-stu-id="52385-289">**Counter\_name\_regex**: a *regular expression* defining which counters (for hello object) toocollect.</span></span> <span data-ttu-id="52385-290">Spécifiez de tous les compteurs pour l’objet de hello, toocollect : `.*`.</span><span class="sxs-lookup"><span data-stu-id="52385-290">toocollect all counters for hello object, specify: `.*`.</span></span> <span data-ttu-id="52385-291">toocollect permutation compteurs d’espace pour l’objet de mémoire hello, vous pouvez spécifier :`.+Swap.+`</span><span class="sxs-lookup"><span data-stu-id="52385-291">toocollect only swap space counters for hello memory object, you could specify: `.+Swap.+`</span></span>
* <span data-ttu-id="52385-292">**Intervalle :**: hello fréquence à quels hello les compteurs de l’objet sont collectés.</span><span class="sxs-lookup"><span data-stu-id="52385-292">**Interval:**: hello frequency at which hello object's counters are collected.</span></span>

<span data-ttu-id="52385-293">configuration par défaut de Hello pour les métriques de performances est la suivante :</span><span class="sxs-lookup"><span data-stu-id="52385-293">hello default configuration for performance metrics is:</span></span>

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

### <a name="enable-mysql-performance-counters-using-linux-commands"></a><span data-ttu-id="52385-294">Activer des compteurs de performances MySQL à l’aide de commandes Linux</span><span class="sxs-lookup"><span data-stu-id="52385-294">Enable MySQL performance counters using Linux commands</span></span>
<span data-ttu-id="52385-295">Si MySQL Server ou MariaDB Server est détecté sur l’ordinateur de hello lorsque hello du bundle omsagent, un fournisseur pour MySQL Server d’analyse des performances sont automatiquement installé.</span><span class="sxs-lookup"><span data-stu-id="52385-295">If MySQL Server or MariaDB Server is detected on hello computer when hello omsagent bundle is installed, a performance monitoring provider for MySQL Server is automatically installed.</span></span> <span data-ttu-id="52385-296">Ce fournisseur connecte toohello local MySQL/MariaDB server tooexpose les statistiques de performances.</span><span class="sxs-lookup"><span data-stu-id="52385-296">This provider connects toohello local MySQL/MariaDB server tooexpose performance statistics.</span></span> <span data-ttu-id="52385-297">Vous avez besoin d’informations d’identification utilisateur MySQL de tooconfigure afin que hello fournisseur d’accéder à hello MySQL Server.</span><span class="sxs-lookup"><span data-stu-id="52385-297">You need tooconfigure MySQL user credentials so that hello provider can access hello MySQL Server.</span></span>

<span data-ttu-id="52385-298">toodefine compte d’un utilisateur par défaut pour le serveur MySQL de hello sur localhost, hello utilisez exemple de commande suivant.</span><span class="sxs-lookup"><span data-stu-id="52385-298">toodefine a default user account for hello MySQL server on localhost, use hello following command example.</span></span>

> [!NOTE]
> <span data-ttu-id="52385-299">fichier d’informations d’identification de Hello doit être accessible en lecture hello omsagent compte.</span><span class="sxs-lookup"><span data-stu-id="52385-299">hello credentials file must be readable by hello omsagent account.</span></span> <span data-ttu-id="52385-300">Est recommandé d’exécuter la commande mycimprovauth de hello pour omsgent.</span><span class="sxs-lookup"><span data-stu-id="52385-300">Running hello mycimprovauth command as omsgent is recommended.</span></span>
>
>

```
sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>

sudo /opt/omi/bin/service_control restart
```


<span data-ttu-id="52385-301">Vous pouvez également spécifier hello requis des informations d’identification MySQL dans un fichier, en créant un fichier hello : /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth. Pour plus d’informations sur la gestion des informations d’identification MySQL pour l’analyse via le fichier de hello mysql-auth, consultez [MySQL gérer analyse les informations d’identification dans le fichier d’authentification hello](#manage-mysql-monitoring-credentials-in-the-authentication-file).</span><span class="sxs-lookup"><span data-stu-id="52385-301">Alternatively, you can specify hello required MySQL credentials in a file, by creating hello file: /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth. For more information about managing MySQL credentials for monitoring through hello mysql-auth file, see [Manage MySQL monitoring credentials in hello authentication file](#manage-mysql-monitoring-credentials-in-the-authentication-file).</span></span>

<span data-ttu-id="52385-302">Consultez [de base de données des autorisations requises pour les compteurs de performances MySQL](#database-permissions-required-for-mysql-performance-counters) pour plus d’informations sur les autorisations d’objet requises par hello MySQL utilisateur toocollect données de performances MySQL Server.</span><span class="sxs-lookup"><span data-stu-id="52385-302">See [Database permissions required for MySQL performance counters](#database-permissions-required-for-mysql-performance-counters) for details about object permissions required by hello MySQL user toocollect MySQL Server performance data.</span></span>

### <a name="enable-apache-http-server-performance-counters-using-linux-commands"></a><span data-ttu-id="52385-303">Activer les compteurs de performances d’Apache HTTP Server à l’aide de commandes Linux</span><span class="sxs-lookup"><span data-stu-id="52385-303">Enable Apache HTTP Server performance counters using Linux commands</span></span>
<span data-ttu-id="52385-304">Si Apache HTTP Server est détecté sur l’ordinateur de hello lorsque hello du bundle omsagent, un fournisseur pour Apache HTTP Server d’analyse des performances sont automatiquement installé.</span><span class="sxs-lookup"><span data-stu-id="52385-304">If Apache HTTP Server is detected on hello computer when hello omsagent bundle is installed, a performance monitoring provider for Apache HTTP Server is automatically installed.</span></span> <span data-ttu-id="52385-305">Ce fournisseur repose sur un « module » Apache qui doit être chargé dans Apache HTTP Server de hello ordre tooaccess les données de performance.</span><span class="sxs-lookup"><span data-stu-id="52385-305">This provider relies on an Apache "module" that must be loaded into hello Apache HTTP Server in order tooaccess performance data.</span></span>

<span data-ttu-id="52385-306">Vous pouvez charger le module de hello avec hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="52385-306">You can load hello module with hello following command:</span></span>

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

<span data-ttu-id="52385-307">toounload hello module d’analyse Apache, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="52385-307">toounload hello Apache monitoring module, run hello following command:</span></span>

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```
### <a name="tooview-performance-data-with-log-analytics"></a><span data-ttu-id="52385-308">données de performances tooview avec Analytique de journal</span><span class="sxs-lookup"><span data-stu-id="52385-308">tooview performance data with Log Analytics</span></span>
1. <span data-ttu-id="52385-309">Dans le portail Operations Management Suite hello, cliquez sur la vignette de recherche de journal hello.</span><span class="sxs-lookup"><span data-stu-id="52385-309">In hello Operations Management Suite portal, click hello Log Search tile.</span></span>
2. <span data-ttu-id="52385-310">Dans la barre de recherche de hello, tapez `* (Type=Perf)` tooview tous les compteurs de performances.</span><span class="sxs-lookup"><span data-stu-id="52385-310">In hello search bar, type `* (Type=Perf)` tooview all performance counters.</span></span>

<span data-ttu-id="52385-311">Comme OMS collecte également les données de compteur de performance Windows, vous devez limiter hello recherche tooLinux propres données.</span><span class="sxs-lookup"><span data-stu-id="52385-311">Because OMS also collects Windows performance counter data, you should scope-down hello search tooLinux-specific data.</span></span> <span data-ttu-id="52385-312">Par conséquent, hello exemple suivant affichera-t-il les performances données tooan spécifique exemple de serveur Linux nommé Chorizo21.</span><span class="sxs-lookup"><span data-stu-id="52385-312">So, hello following example would show performance data specific tooan example Linux server named Chorizo21.</span></span>

```
Type=Perf Computer=chorizo*
```

![exemple de serveur affiché dans les résultats de la recherche](./media/log-analytics-linux-agents/oms-perfsearch01.png)

<span data-ttu-id="52385-314">Dans les résultats de hello, vous pouvez cliquer sur **métriques** compteurs hello tooview collectées pour les données.</span><span class="sxs-lookup"><span data-stu-id="52385-314">In hello results, you can click **Metrics** tooview hello counters that data was collected for.</span></span> <span data-ttu-id="52385-315">Les données en temps réel sont indiquées sous forme graphique pour chaque compteur.</span><span class="sxs-lookup"><span data-stu-id="52385-315">Real-time data is shown as graphs for each counter.</span></span>

![Mesures](./media/log-analytics-linux-agents/oms-perfmetrics01.png)

## <a name="syslog"></a><span data-ttu-id="52385-317">syslog</span><span class="sxs-lookup"><span data-stu-id="52385-317">Syslog</span></span>
<span data-ttu-id="52385-318">Syslog est un protocole tooWindows similaire des journaux des événements de journalisation des événements, les deux fonctionnent de manière similaire dans OMS.</span><span class="sxs-lookup"><span data-stu-id="52385-318">Syslog is an event logging protocol similar tooWindows Event logs—both operate similarly when displayed in OMS.</span></span>

### <a name="tooadd-a-new-linux-syslog-facility-in-oms"></a><span data-ttu-id="52385-319">tooadd une nouvelle fonction syslog de Linux dans OMS</span><span class="sxs-lookup"><span data-stu-id="52385-319">tooadd a new Linux syslog facility in OMS</span></span>
1. <span data-ttu-id="52385-320">Sur hello **paramètres** page sous **données** , cliquez sur **Syslog** puis toohello à gauche de l’icône plus hello, tapez hello nom de la fonction syslog de hello que vous souhaitez tooadd.</span><span class="sxs-lookup"><span data-stu-id="52385-320">On hello **Settings** page under **Data** , click **Syslog** and then toohello left of hello plus icon, type hello name of hello syslog facility that you want tooadd.</span></span>
    <span data-ttu-id="52385-321">![syslog de Linux](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)</span><span class="sxs-lookup"><span data-stu-id="52385-321">![Linux syslog](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)</span></span>
2. <span data-ttu-id="52385-322">Si vous ne connaissez le nom complet de hello de facilité de hello, vous pouvez commencer en tapant un nom partiel, et une liste des fonctions syslog disponibles s’affiche.</span><span class="sxs-lookup"><span data-stu-id="52385-322">If you don’t know hello full name of hello facility, you can start typing a partial name and a list of available syslog facilities will appear.</span></span> <span data-ttu-id="52385-323">Lorsque vous trouvez la fonction syslog de hello que vous souhaitez tooadd, cliquez sur nom hello dans la liste de hello puis hello plus hello de tooadd icône fonction syslog.</span><span class="sxs-lookup"><span data-stu-id="52385-323">When you find hello syslog facility that you want tooadd, click hello name in hello list and then click hello plus icon tooadd hello syslog facility.</span></span>
3. <span data-ttu-id="52385-324">Après avoir ajouté la fonctionnalité de hello, il apparaît dans la liste hello de mise en surbrillance avec une barre de couleur.</span><span class="sxs-lookup"><span data-stu-id="52385-324">After you add hello facility, it appears in hello list of highlighted with a colored bar.</span></span> <span data-ttu-id="52385-325">Ensuite, choisissez hello, niveaux de gravité (catégories d’information sur les fonctions syslog) que vous souhaitez toocollect.</span><span class="sxs-lookup"><span data-stu-id="52385-325">Next, choose hello severities (categories of syslog facility information) that you want toocollect.</span></span>
4. <span data-ttu-id="52385-326">Au bas de hello de page de hello cliquez sur **enregistrer** toofinalize vos modifications.</span><span class="sxs-lookup"><span data-stu-id="52385-326">At hello bottom of hello page click **Save** toofinalize your changes.</span></span> <span data-ttu-id="52385-327">les modifications de configuration Hello que vous avez apportées sont ensuite envoyées tooall hello Agents OMS pour Linux qui sont inscrits auprès d’OMS, généralement dans les 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="52385-327">hello configuration changes that you’ve made are then sent tooall hello OMS Agents for Linux that are registered with OMS, typically within 5 minutes.</span></span>

### <a name="configure-linux-syslog-facilities-in-linux"></a><span data-ttu-id="52385-328">Configurer des fonctionnalités syslog Linux dans Linux</span><span class="sxs-lookup"><span data-stu-id="52385-328">Configure Linux syslog facilities in Linux</span></span>
<span data-ttu-id="52385-329">Événements syslog sont envoyés du démon syslog de hello, par exemple rsyslog ou syslog-ng, port local de tooa que l’agent hello écoute.</span><span class="sxs-lookup"><span data-stu-id="52385-329">Syslog events are sent from hello syslog daemon, for example rsyslog or syslog-ng, tooa local port that hello agent is listening on.</span></span> <span data-ttu-id="52385-330">Le port par défaut est 25224.</span><span class="sxs-lookup"><span data-stu-id="52385-330">By default, port 25224.</span></span> <span data-ttu-id="52385-331">Lorsque l’agent hello est installé, une configuration de syslog par défaut est appliquée.</span><span class="sxs-lookup"><span data-stu-id="52385-331">When hello agent is installed, a default syslog configuration is applied.</span></span> <span data-ttu-id="52385-332">Elle se trouve à l’emplacement suivant :</span><span class="sxs-lookup"><span data-stu-id="52385-332">This is found at:</span></span>

<span data-ttu-id="52385-333">Rsyslog : /etc/rsyslog.d/rsyslog-oms.conf</span><span class="sxs-lookup"><span data-stu-id="52385-333">Rsyslog: /etc/rsyslog.d/rsyslog-oms.conf</span></span>

<span data-ttu-id="52385-334">Syslog-ng : /etc/syslog-ng/syslog-ng.conf</span><span class="sxs-lookup"><span data-stu-id="52385-334">Syslog-ng: /etc/syslog-ng/syslog-ng.conf</span></span>

<span data-ttu-id="52385-335">configuration de syslog Hello par défaut OMS agent télécharge les événements syslog de toutes les fonctions ayant un niveau de gravité d’avertissement ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="52385-335">hello default OMS agent syslog configuration uploads syslog events from all facilities with a severity of warning or higher.</span></span>

> [!NOTE]
> <span data-ttu-id="52385-336">Si vous modifiez la configuration syslog hello, vous devez redémarrer le démon syslog hello hello modifications tootake effet.</span><span class="sxs-lookup"><span data-stu-id="52385-336">If you edit hello syslog configuration, you must restart hello syslog daemon for hello changes tootake effect.</span></span>
>
>

<span data-ttu-id="52385-337">Hello configuration syslog par défaut pour hello Agent OMS pour Linux pour OMS est la suivante :</span><span class="sxs-lookup"><span data-stu-id="52385-337">hello default syslog configuration for hello OMS Agent for Linux for OMS is:</span></span>

#### <a name="rsyslog"></a><span data-ttu-id="52385-338">Rsyslog</span><span class="sxs-lookup"><span data-stu-id="52385-338">Rsyslog</span></span>
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

#### <a name="syslog-ng"></a><span data-ttu-id="52385-339">Syslog-ng</span><span class="sxs-lookup"><span data-stu-id="52385-339">Syslog-ng</span></span>
```
#OMS_facility = all
filter f_warning_oms { level(warning); };
destination warning_oms { tcp("127.0.0.1" port(25224)); };
log { source(src); filter(f_warning_oms); destination(warning_oms); };
```

### <a name="tooview-all-syslog-events-with-log-analytics"></a><span data-ttu-id="52385-340">tooview tous les événements Syslog avec Analytique de journal</span><span class="sxs-lookup"><span data-stu-id="52385-340">tooview all Syslog events with Log Analytics</span></span>
1. <span data-ttu-id="52385-341">Dans le portail Operations Management Suite hello, cliquez sur hello **recherche de journal** vignette.</span><span class="sxs-lookup"><span data-stu-id="52385-341">In hello Operations Management Suite portal, click hello **Log Search** tile.</span></span>
2. <span data-ttu-id="52385-342">Bonjour **gestion du journal** de regroupement, sélectionnez une recherche syslog prédéfinie et puis sélectionnez un toorun il.</span><span class="sxs-lookup"><span data-stu-id="52385-342">In hello **Log Management** grouping, choose a predefined syslog search and then select one toorun it.</span></span>

<span data-ttu-id="52385-343">Cet exemple montre tous les événements Syslog.</span><span class="sxs-lookup"><span data-stu-id="52385-343">This example shows all Syslog events.</span></span>

![Événements syslog affichés dans Recherche de journal](./media/log-analytics-linux-agents/oms-linux-syslog.png)

<span data-ttu-id="52385-345">Maintenant, vous pouvez examiner les résultats de la recherche plus en détail.</span><span class="sxs-lookup"><span data-stu-id="52385-345">Now you can drill into search results.</span></span>

## <a name="linux-alerts"></a><span data-ttu-id="52385-346">Alertes Linux</span><span class="sxs-lookup"><span data-stu-id="52385-346">Linux alerts</span></span>
<span data-ttu-id="52385-347">Si vous utilisez Nagios ou Zabbix toomanage que vos ordinateurs Linux, puis OMS peut recevoir des alertes de hello générées à partir de ces outils.</span><span class="sxs-lookup"><span data-stu-id="52385-347">If you use Nagios or Zabbix toomanage your Linux machines, then OMS can receive hello alerts generated from those tools.</span></span> <span data-ttu-id="52385-348">Toutefois, il n’existe actuellement aucune méthode tooconfigure données d’alerte entrantes à l’aide du portail OMS hello.</span><span class="sxs-lookup"><span data-stu-id="52385-348">However, there is currently no method tooconfigure incoming alert data using hello OMS portal.</span></span> <span data-ttu-id="52385-349">Au lieu de cela, vous devez tooedit une tooOMS alertes config fichier toostart envoi.</span><span class="sxs-lookup"><span data-stu-id="52385-349">Instead, you will need tooedit a config file toostart sending alerts tooOMS.</span></span>

### <a name="collect-alerts-from-nagios"></a><span data-ttu-id="52385-350">Collecter les alertes de Nagios</span><span class="sxs-lookup"><span data-stu-id="52385-350">Collect alerts from Nagios</span></span>
<span data-ttu-id="52385-351">toocollect les alertes d’un serveur Nagios, vous devez hello toomake suit les modifications de configuration.</span><span class="sxs-lookup"><span data-stu-id="52385-351">toocollect alerts from a Nagios server, you need toomake hello following configuration changes.</span></span>

1. <span data-ttu-id="52385-352">Utilisateur de subventions hello **omsagent** fichier de journal accès en lecture toohello Nagios (c'est-à-dire /var/log/nagios/nagios.log).</span><span class="sxs-lookup"><span data-stu-id="52385-352">Grant hello user **omsagent** read access toohello Nagios log file (i.e. /var/log/nagios/nagios.log).</span></span> <span data-ttu-id="52385-353">En supposant que le fichier de hello nagios.log est détenu par groupe de hello **nagios** , vous pouvez ajouter hello utilisateur **omsagent** toohello **nagios** groupe.</span><span class="sxs-lookup"><span data-stu-id="52385-353">Assuming hello nagios.log file is owned by hello group **nagios** , you can add hello user **omsagent** toohello **nagios** group.</span></span>

    ```
    sudo usermod –a -G nagios omsagent
    ```
2. <span data-ttu-id="52385-354">Modifier le fichier de configuration omsagent.conf hello (/ etc/opt/microsoft/omsagent/&lt;id de l’espace de travail&gt;/conf/omsagent.conf).</span><span class="sxs-lookup"><span data-stu-id="52385-354">Modify hello omsagent.confconfiguration file (/etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf).</span></span> <span data-ttu-id="52385-355">Vérifiez que hello suivant entrées est présents et pas commentées :</span><span class="sxs-lookup"><span data-stu-id="52385-355">Ensure hello following entries are present and not commented out:</span></span>

    ```
    <source>
    type tail
    #Update path toopoint tooyour nagios.log
    path /var/log/nagios/nagios.log
    format none
    tag oms.nagios
    </source>

    <filter oms.nagios>
    type filter_nagios_log
    </filter>
    ```
3. <span data-ttu-id="52385-356">Redémarrez le démon omsagent de hello :</span><span class="sxs-lookup"><span data-stu-id="52385-356">Restart hello omsagent daemon:</span></span>

    ```
    sudo /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="collect-alerts-from-zabbix"></a><span data-ttu-id="52385-357">Collecter les alertes de Zabbix</span><span class="sxs-lookup"><span data-stu-id="52385-357">Collect alerts from Zabbix</span></span>
<span data-ttu-id="52385-358">toocollect des alertes à partir d’un serveur Zabbix, à suivre est similaire étapes toothose de nagios décrite ci-dessus, mais vous devez toospecify un utilisateur et mot de passe dans *clair*.</span><span class="sxs-lookup"><span data-stu-id="52385-358">toocollect alerts from a Zabbix server, you'll perform similar steps toothose for Nagios above, except you'll need toospecify a user and password in *clear text*.</span></span> <span data-ttu-id="52385-359">Cette solution n’est pas idéale, mais elle devrait changer rapidement.</span><span class="sxs-lookup"><span data-stu-id="52385-359">This is not ideal, but will likely change soon.</span></span> <span data-ttu-id="52385-360">tooaddress ce problème, nous vous recommandons de créer un utilisateur de hello et de lui accorder toomonitor autorisation uniquement.</span><span class="sxs-lookup"><span data-stu-id="52385-360">tooaddress this issue, we recommend that you create hello user and grant it permission toomonitor only.</span></span>

<span data-ttu-id="52385-361">Une section de l’exemple de fichier de configuration omsagent.conf hello (/ etc/opt/microsoft/omsagent/&lt;id de l’espace de travail&gt;/conf/omsagent.conf) pour Zabbix suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="52385-361">An example section of hello omsagent.conf configuration file  (/etc/opt/microsoft/omsagent/&lt;workspace id&gt;/conf/omsagent.conf) for Zabbix should resemble hello following:</span></span>

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

### <a name="view-alerts-in-log-analytics-search"></a><span data-ttu-id="52385-362">Afficher les alertes dans la recherche Log Analytics</span><span class="sxs-lookup"><span data-stu-id="52385-362">View alerts in Log Analytics search</span></span>
<span data-ttu-id="52385-363">Une fois que vous avez configuré votre tooOMS d’alertes Linux ordinateurs toosend, vous pouvez utiliser quelques du journal des simples requêtes tooview hello les alertes de recherche.</span><span class="sxs-lookup"><span data-stu-id="52385-363">After you've configured your Linux computers toosend alerts tooOMS, you can use a few simple log search queries tooview hello alerts.</span></span> <span data-ttu-id="52385-364">Hello exemple de requête de recherche ci-dessous retourne toutes les alertes hello enregistrée qui ont été générées.</span><span class="sxs-lookup"><span data-stu-id="52385-364">hello following search query example returns all hello recorded alerts that were generated.</span></span> <span data-ttu-id="52385-365">Par exemple, si un problème quelconque se produit dans votre infrastructure informatique, puis les résultats pour hello exemple de requête peut-être indiquer où le problème de hello suivant.</span><span class="sxs-lookup"><span data-stu-id="52385-365">For example, if some sort of problem occurs in your IT infrastructure, then results for hello following example query might indicate where hello problem might originate.</span></span> <span data-ttu-id="52385-366">Et, vous pouvez explorer facilement dans les alertes de toohello par toohelp du système source étroit votre examen.</span><span class="sxs-lookup"><span data-stu-id="52385-366">And, you can easily drill in toohello alerts by source system toohelp narrow your investigation.</span></span> <span data-ttu-id="52385-367">Bonjour avantage est que vous ne sont pas nécessairement des systèmes de gestion toovarious toogo à partir du début de hello : condition que vos alertes sont envoyées tooOMS, vous pouvez commencer de là.</span><span class="sxs-lookup"><span data-stu-id="52385-367">hello benefit is that you don't necessarily have toogo toovarious management systems from hello start—provided that your alerts are sent tooOMS, you can start there.</span></span>

```
Type=Alert
```

#### <a name="tooview-all-nagios-alerts-with-log-analytics"></a><span data-ttu-id="52385-368">tooview Nagios toutes les alertes avec Analytique de journal</span><span class="sxs-lookup"><span data-stu-id="52385-368">tooview all Nagios alerts with Log Analytics</span></span>
1. <span data-ttu-id="52385-369">Dans le portail Operations Management Suite hello, cliquez sur hello **recherche de journal** vignette.</span><span class="sxs-lookup"><span data-stu-id="52385-369">In hello Operations Management Suite portal, click hello **Log Search** tile.</span></span>
2. <span data-ttu-id="52385-370">Dans la barre de requête hello, tapez Bonjour suivant la requête de recherche</span><span class="sxs-lookup"><span data-stu-id="52385-370">In hello query bar, type hello following search query</span></span>

    ```
    Type=Alert SourceSystem=Nagios
    ```
   ![Alertes Nagios affichées dans Recherche de journal](./media/log-analytics-linux-agents/oms-linux-nagios-alerts.png)

<span data-ttu-id="52385-372">Une fois que vous voyez les résultats de la recherche hello, vous pouvez explorer des détails supplémentaires, comme *AlertState*.</span><span class="sxs-lookup"><span data-stu-id="52385-372">After you see hello search results, you can drill into additional details such as *AlertState*.</span></span>

### <a name="tooview-all-zabbix-alerts-with-log-analytics"></a><span data-ttu-id="52385-373">tooview toutes les alertes Zabbix Analytique de journal</span><span class="sxs-lookup"><span data-stu-id="52385-373">tooview all Zabbix alerts with Log Analytics</span></span>
1. <span data-ttu-id="52385-374">Dans le portail Operations Management Suite hello, cliquez sur hello **recherche de journal** vignette.</span><span class="sxs-lookup"><span data-stu-id="52385-374">In hello Operations Management Suite portal, click hello **Log Search** tile.</span></span>
2. <span data-ttu-id="52385-375">Dans la barre de requête hello, tapez Bonjour suivant la requête de recherche</span><span class="sxs-lookup"><span data-stu-id="52385-375">In hello query bar, type hello following search query</span></span>

    ```
    Type=Alert SourceSystem=Zabbix
    ```
   ![Alertes Zabbix affichées dans Recherche de journal](./media/log-analytics-linux-agents/oms-linux-zabbix-alerts.png)

<span data-ttu-id="52385-377">Une fois que vous voyez les résultats de la recherche hello, vous pouvez explorer des détails supplémentaires, comme *AlertName*.</span><span class="sxs-lookup"><span data-stu-id="52385-377">After you see hello search results, you can drill into additional details such as *AlertName*.</span></span>

## <a name="compatibility-with-system-center-operations-manager"></a><span data-ttu-id="52385-378">Compatibilité avec System Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="52385-378">Compatibility with System Center Operations Manager</span></span>
<span data-ttu-id="52385-379">Hello Agent OMS pour Linux partage des fichiers binaires avec l’agent de System Center Operations Manager hello.</span><span class="sxs-lookup"><span data-stu-id="52385-379">hello OMS Agent for Linux shares agent binaries with hello System Center Operations Manager agent.</span></span> <span data-ttu-id="52385-380">Installation hello Agent OMS pour Linux sur un système actuellement géré par Operations Manager les mises à niveau hello packages OMI et SCX sur une version plus récente de hello ordinateur tooa.</span><span class="sxs-lookup"><span data-stu-id="52385-380">Installing hello OMS Agent for Linux on a system currently managed by Operations Manager upgrades hello OMI and SCX packages on hello computer tooa newer version.</span></span> <span data-ttu-id="52385-381">Hello Agent OMS pour Linux et System Center 2012 R2 sont compatibles.</span><span class="sxs-lookup"><span data-stu-id="52385-381">hello OMS Agent for Linux and System Center 2012 R2 are compatible.</span></span> <span data-ttu-id="52385-382">Toutefois, **System Center 2012 SP1 et les versions antérieures ne sont actuellement pas compatibles ni prises en charge avec hello Agent OMS pour Linux.**</span><span class="sxs-lookup"><span data-stu-id="52385-382">However, **System Center 2012 SP1 and earlier versions are currently not compatible or supported with hello OMS Agent for Linux.**</span></span>

> [!NOTE]
> <span data-ttu-id="52385-383">Si hello Agent OMS pour Linux est installé tooa ordinateur qui n’est pas actuellement géré par Operations Manager et que vous décidez d’ordinateur de hello toomanage avec Operations Manager, vous devez modifier la configuration de hello OMI avant de découvrir hello ordinateur.</span><span class="sxs-lookup"><span data-stu-id="52385-383">If hello OMS Agent for Linux is installed tooa computer that is not currently managed by Operations Manager, and you later want toomanage hello computer with Operations Manager, you must modify hello OMI configuration before you discover hello computer.</span></span> <span data-ttu-id="52385-384">**Cette étape n’est pas nécessaire si l’agent Operations Manager de hello est installé avant hello Agent OMS pour Linux.**</span><span class="sxs-lookup"><span data-stu-id="52385-384">**This step is not needed if hello Operations Manager agent is installed before hello OMS Agent for Linux.**</span></span>
>
>

### <a name="tooenable-hello-oms-agent-for-linux-toocommunicate-with-operations-manager"></a><span data-ttu-id="52385-385">tooenable hello Agent OMS pour toocommunicate Linux avec Operations Manager</span><span class="sxs-lookup"><span data-stu-id="52385-385">tooenable hello OMS Agent for Linux toocommunicate with Operations Manager</span></span>
1. <span data-ttu-id="52385-386">Modifier hello fichier /etc/opt/omi/conf/omiserver.conf</span><span class="sxs-lookup"><span data-stu-id="52385-386">Edit hello file /etc/opt/omi/conf/omiserver.conf</span></span>
2. <span data-ttu-id="52385-387">Vérifiez que hello ligne commençant par **httpsport =** définit le port 1270 hello.</span><span class="sxs-lookup"><span data-stu-id="52385-387">Ensure that hello line beginning with **httpsport=** defines hello port 1270.</span></span> <span data-ttu-id="52385-388">Par exemple `httpsport=1270`</span><span class="sxs-lookup"><span data-stu-id="52385-388">Such as `httpsport=1270`</span></span>
3. <span data-ttu-id="52385-389">Redémarrez le serveur OMI de hello :</span><span class="sxs-lookup"><span data-stu-id="52385-389">Restart hello OMI server:</span></span>

    ```
    sudo /opt/omi/bin/service_control restart
    ```

## <a name="database-permissions-required-for-mysql-performance-counters"></a><span data-ttu-id="52385-390">Autorisations de base de données requises par l’utilisateur MySQL pour collecter les données de performances de MySQL Server</span><span class="sxs-lookup"><span data-stu-id="52385-390">Database permissions required for MySQL performance counters</span></span>
<span data-ttu-id="52385-391">toogrant autorisations tooa utilisateur d’analyse MySQL, utilisateur hello doit avoir hello privilège « GRANT option », ainsi que des privilèges hello accordée.</span><span class="sxs-lookup"><span data-stu-id="52385-391">toogrant permissions tooa MySQL monitoring user, hello granting user must have hello 'GRANT option' privilege as well as hello privilege being granted.</span></span>

<span data-ttu-id="52385-392">Dans l’ordre pour hello MySQL utilisateur utilisateur de hello de données de performances tooreturn aura besoin d’accès toohello requêtes suivantes :</span><span class="sxs-lookup"><span data-stu-id="52385-392">In order for hello MySQL User tooreturn performance data hello user will need access toohello following queries:</span></span>

```
SHOW GLOBAL STATUS;
SHOW GLOBAL VARIABLES:
```

<span data-ttu-id="52385-393">En outre, utilisateur de MySQL toothese requêtes hello requiert toohello accès choisi par défaut tables suivantes :</span><span class="sxs-lookup"><span data-stu-id="52385-393">In addition toothese queries hello MySQL user requires SELECT access toohello following default tables:</span></span>

* <span data-ttu-id="52385-394">information_schema</span><span class="sxs-lookup"><span data-stu-id="52385-394">information_schema</span></span>
* <span data-ttu-id="52385-395">mysql</span><span class="sxs-lookup"><span data-stu-id="52385-395">mysql</span></span>

<span data-ttu-id="52385-396">Ces privilèges peuvent être accordés en exécutant hello suivant de commandes grant.</span><span class="sxs-lookup"><span data-stu-id="52385-396">These privileges can be granted by running hello following grant commands.</span></span>

```
GRANT SELECT ON information_schema.* too‘monuser’@’localhost’;
GRANT SELECT ON mysql.* too‘monuser’@’localhost’;
```

## <a name="manage-mysql-monitoring-credentials-in-hello-authentication-file"></a><span data-ttu-id="52385-397">Gérer l’analyse des informations d’identification dans le fichier d’authentification hello MySQL</span><span class="sxs-lookup"><span data-stu-id="52385-397">Manage MySQL monitoring credentials in hello authentication file</span></span>
<span data-ttu-id="52385-398">Hello sections suivantes vous gérez les informations d’identification MySQL.</span><span class="sxs-lookup"><span data-stu-id="52385-398">hello following sections help you manage MySQL credentials.</span></span>

### <a name="configure-hello-mysql-omi-provider"></a><span data-ttu-id="52385-399">Configurer hello fournisseur OMI MySQL</span><span class="sxs-lookup"><span data-stu-id="52385-399">Configure hello MySQL OMI provider</span></span>
<span data-ttu-id="52385-400">Hello fournisseur OMI MySQL requiert un utilisateur MySQL soit préconfiguré et les bibliothèques clientes MySQL installées dans les informations de performances/intégrité tooquery hello ordre à partir de l’instance de MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="52385-400">hello MySQL OMI provider requires a preconfigured MySQL user and installed MySQL client libraries in order tooquery hello performance/health information from hello MySQL instance.</span></span>

### <a name="mysql-omi-authentication-file"></a><span data-ttu-id="52385-401">Fichier d’authentification OMI de MySQL</span><span class="sxs-lookup"><span data-stu-id="52385-401">MySQL OMI authentication file</span></span>
<span data-ttu-id="52385-402">Le fournisseur OMI MySQL utilise un toodetermine de fichier d’authentification quelle instance de MySQL hello adresse de liaison et le port d’écoute et les informations d’identification toouse toogather métriques.</span><span class="sxs-lookup"><span data-stu-id="52385-402">MySQL OMI provider uses an authentication file toodetermine what bind-address and port hello MySQL instance is listening on and what credentials toouse toogather metrics.</span></span> <span data-ttu-id="52385-403">Au cours de hello d’installation OMI MySQL fournisseur recherchera les fichiers de configuration MySQL my.cnf (emplacements par défaut) adresse de liaison et un port et partiellement hello de jeu de fichier d’authentification OMI MySQL.</span><span class="sxs-lookup"><span data-stu-id="52385-403">During installation hello MySQL OMI provider will scan MySQL my.cnf configuration files (default locations) for bind-address and port and partially set hello MySQL OMI authentication file.</span></span>

<span data-ttu-id="52385-404">toocomplete d’analyse d’une instance de serveur MySQL, pour ajouter un fichier d’authentification OMI MySQL prégénéré dans le répertoire approprié de hello.</span><span class="sxs-lookup"><span data-stu-id="52385-404">toocomplete monitoring of a MySQL server instance, add a pre-generated MySQL OMI authentication file into hello correct directory.</span></span>

### <a name="authentication-file-format"></a><span data-ttu-id="52385-405">Format du fichier d’authentification</span><span class="sxs-lookup"><span data-stu-id="52385-405">Authentication file format</span></span>
<span data-ttu-id="52385-406">Hello fichier d’authentification OMI MySQL est un fichier texte qui contient des informations sur :</span><span class="sxs-lookup"><span data-stu-id="52385-406">hello MySQL OMI authentication file is a text file that contains information about:</span></span>

* <span data-ttu-id="52385-407">Port</span><span class="sxs-lookup"><span data-stu-id="52385-407">Port</span></span>
* <span data-ttu-id="52385-408">Adresse de liaison</span><span class="sxs-lookup"><span data-stu-id="52385-408">Bind-Address</span></span>
* <span data-ttu-id="52385-409">Nom d’utilisateur MySQL</span><span class="sxs-lookup"><span data-stu-id="52385-409">MySQL username</span></span>
* <span data-ttu-id="52385-410">Mot de passe encodé en base 64</span><span class="sxs-lookup"><span data-stu-id="52385-410">Base64 encoded password</span></span>

<span data-ttu-id="52385-411">Hello fichier d’authentification OMI MySQL accorde uniquement des droits en lecture/écriture toohello Linux utilisateur qui l’a généré.</span><span class="sxs-lookup"><span data-stu-id="52385-411">hello MySQL OMI authentication file only grants privileges for read/write toohello Linux user that generated it.</span></span>

```
[Port]=[Bind-Address], [username], [Base64 encoded Password]
(Port)=(Bind-Address), (username), (Base64 encoded Password)
(Port)=(Bind-Address), (username), (Base64 encoded Password)
AutoUpdate=[true|false]
```

<span data-ttu-id="52385-412">Un fichier d’authentification OMI MySQL par défaut contient une instance par défaut et un numéro de port, selon les informations disponibles et analysé à partir de hello fichier de configuration MySQL trouvé.</span><span class="sxs-lookup"><span data-stu-id="52385-412">A default MySQL OMI authentication file contains a default instance and a port number depending on what information is available and parsed from hello found MySQL configuration file.</span></span>

<span data-ttu-id="52385-413">instance par défaut de Hello un toomake signifie que la gestion de plusieurs instances MySQL sur un même hôte Linux plus facile et est représentée par l’instance de hello associée au port 0.</span><span class="sxs-lookup"><span data-stu-id="52385-413">hello default instance is a means toomake managing multiple MySQL instances on one Linux host easier, and is denoted by hello instance with port 0.</span></span> <span data-ttu-id="52385-414">Toutes les instances ajoutées héritent des propriétés définies à partir de l’instance par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="52385-414">All added instances will inherit properties set from hello default instance.</span></span> <span data-ttu-id="52385-415">Par exemple, si l’instance MySQL à l’écoute sur le port « 3308 » est ajoutée, l’instance par défaut de hello adresse de liaison, nom d’utilisateur et mot de passe codé en Base64 seront être tootry utilisé d’analyser hello instance à l’écoute du port 3308.</span><span class="sxs-lookup"><span data-stu-id="52385-415">For example, if MySQL instance listening on port '3308' is added, hello default instance's bind-address, username, and Base64 encoded password will be used tootry and monitor hello instance listening on 3308.</span></span> <span data-ttu-id="52385-416">Si instance hello du port 3308 est lié tooanother adresse et utilise hello le même nom d’utilisateur MySQL et paire mot de passe hello uniquement respecification Hello adresse de liaison est nécessaire et hello autres propriétés sont héritées.</span><span class="sxs-lookup"><span data-stu-id="52385-416">If hello instance on 3308 is binded tooanother address and uses hello same MySQL username and password pair only hello respecification of hello bind-address is needed and hello other properties will be inherited.</span></span>

<span data-ttu-id="52385-417">Vous trouverez des exemples de fichier d’authentification hello suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="52385-417">Examples of hello authentication file resemble hello following.</span></span>

<span data-ttu-id="52385-418">Instance par défaut et instance avec port 3308 :</span><span class="sxs-lookup"><span data-stu-id="52385-418">Default instance and instance with port 3308:</span></span>

```
0=127.0.0.1, myuser, cnBwdA==3308=, ,AutoUpdate=true
```

<span data-ttu-id="52385-419">Instance par défaut et instance avec port 3308 + mot de passe différent encodé en base 64 :</span><span class="sxs-lookup"><span data-stu-id="52385-419">Default instance and instance with port 3308 + different Base 64 encoded password:</span></span>

```
0=127.0.0.1, myuser, cnBwdA==3308=127.0.1.1, , AutoUpdate=true
```


| <span data-ttu-id="52385-420">**Propriété**</span><span class="sxs-lookup"><span data-stu-id="52385-420">**Property**</span></span> | <span data-ttu-id="52385-421">**Description**</span><span class="sxs-lookup"><span data-stu-id="52385-421">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="52385-422">Port</span><span class="sxs-lookup"><span data-stu-id="52385-422">Port</span></span> |<span data-ttu-id="52385-423">Le port représente hello de port actuel hello MySQL instance écoute.</span><span class="sxs-lookup"><span data-stu-id="52385-423">Port represents hello current port hello MySQL instance is listening on.</span></span>  <span data-ttu-id="52385-424">le port de Hello 0 implique que les propriétés hello suivantes sont utilisées pour l’instance par défaut.</span><span class="sxs-lookup"><span data-stu-id="52385-424">hello port 0 implies that hello properties following are used for default instance.</span></span> |
| <span data-ttu-id="52385-425">Adresse de liaison</span><span class="sxs-lookup"><span data-stu-id="52385-425">Bind-Address</span></span> |<span data-ttu-id="52385-426">Adresse de liaison de Hello est hello actuel MySQL adresse de liaison</span><span class="sxs-lookup"><span data-stu-id="52385-426">hello Bind Address is hello current MySQL bind-address</span></span> |
| <span data-ttu-id="52385-427">username</span><span class="sxs-lookup"><span data-stu-id="52385-427">username</span></span> |<span data-ttu-id="52385-428">Ce nom d’utilisateur hello d’utilisateur MySQL de hello vous souhaitez instance toouse toomonitor hello MySQL server.</span><span class="sxs-lookup"><span data-stu-id="52385-428">This hello username of hello MySQL user you wish toouse toomonitor hello MySQL server instance.</span></span> |
| <span data-ttu-id="52385-429">Mot de passe encodé en base 64</span><span class="sxs-lookup"><span data-stu-id="52385-429">Base64 encoded Password</span></span> |<span data-ttu-id="52385-430">Il s’agit d’un mot de passe hello de hello utilisateur d’analyse MySQL codé en Base64.</span><span class="sxs-lookup"><span data-stu-id="52385-430">This is hello password of hello MySQL monitoring user encoded in Base64.</span></span> |
| <span data-ttu-id="52385-431">AutoUpdate</span><span class="sxs-lookup"><span data-stu-id="52385-431">AutoUpdate</span></span> |<span data-ttu-id="52385-432">Quand hello fournisseur OMI MySQL est mis à niveau le fournisseur de hello pour les modifications dans le fichier my.cnf hello et remplacer le fichier d’authentification OMI MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="52385-432">When hello MySQL OMI Provider is upgraded hello provider will rescan for changes in hello my.cnf file and overwrite hello MySQL OMI Authentication file.</span></span> <span data-ttu-id="52385-433">Définissez cet indicateur tootrue ou false en fonction de mises à jour requises toohello OMI MySQL fichier d’authentification.</span><span class="sxs-lookup"><span data-stu-id="52385-433">Set this flag tootrue or false depending on required updates toohello MySQL OMI authentication file.</span></span> |

#### <a name="authentication-file-location"></a><span data-ttu-id="52385-434">Emplacement du fichier d’authentification</span><span class="sxs-lookup"><span data-stu-id="52385-434">Authentication file location</span></span>
<span data-ttu-id="52385-435">Hello fichier d’authentification OMI MySQL doit être situé dans hello l’emplacement suivant et nommé « mysql-auth » :</span><span class="sxs-lookup"><span data-stu-id="52385-435">hello MySQL OMI Authentication File should be located in hello following location and named "mysql-auth":</span></span>

<span data-ttu-id="52385-436">/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth</span><span class="sxs-lookup"><span data-stu-id="52385-436">/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth</span></span>

<span data-ttu-id="52385-437">fichier de Hello (et le répertoire auth/omsagent) doivent être possédés par l’utilisateur omsagent de hello.</span><span class="sxs-lookup"><span data-stu-id="52385-437">hello file (and auth/omsagent directory) should be owned by hello omsagent user.</span></span>

## <a name="agent-logs"></a><span data-ttu-id="52385-438">Journaux de l’agent</span><span class="sxs-lookup"><span data-stu-id="52385-438">Agent logs</span></span>
<span data-ttu-id="52385-439">journaux Hello pour hello Agent OMS pour Linux est à :</span><span class="sxs-lookup"><span data-stu-id="52385-439">hello logs for hello OMS Agent for Linux is at:</span></span>

<span data-ttu-id="52385-440">/var/opt/microsoft/omsagent/&lt;workspace id&gt;/log/</span><span class="sxs-lookup"><span data-stu-id="52385-440">/var/opt/microsoft/omsagent/&lt;workspace id&gt;/log/</span></span>

<span data-ttu-id="52385-441">journaux Hello pour hello situé de l’Agent OMS pour Linux pour les programme omsconfig (configuration de l’agent) :</span><span class="sxs-lookup"><span data-stu-id="52385-441">hello logs for hello OMS Agent for Linux for omsconfig (agent configuration) program is at:</span></span>

<span data-ttu-id="52385-442">/var/opt/microsoft/omsconfig/log/</span><span class="sxs-lookup"><span data-stu-id="52385-442">/var/opt/microsoft/omsconfig/log/</span></span>

<span data-ttu-id="52385-443">Les journaux des composants OMI et SCX hello (qui fournissent les données de métriques de performances) se trouve à :</span><span class="sxs-lookup"><span data-stu-id="52385-443">Logs for hello OMI and SCX components (which provide performance metrics data) is at:</span></span>

<span data-ttu-id="52385-444">/var/opt/omi/log/ et /var/opt/microsoft/scx/log</span><span class="sxs-lookup"><span data-stu-id="52385-444">/var/opt/omi/log/ and /var/opt/microsoft/scx/log</span></span>

## <a name="troubleshooting-hello-oms-agent-for-linux"></a><span data-ttu-id="52385-445">Résolution des problèmes de hello Agent OMS pour Linux</span><span class="sxs-lookup"><span data-stu-id="52385-445">Troubleshooting hello OMS Agent for Linux</span></span>
<span data-ttu-id="52385-446">Utilisez hello suivant informations toodiagnose et résoudre les problèmes courants.</span><span class="sxs-lookup"><span data-stu-id="52385-446">Use hello following information toodiagnose and troubleshoot common issues.</span></span>

<span data-ttu-id="52385-447">Si aucun des hello informations de dépannage de cette section vous aide à vous, vous pouvez également utiliser hello suivant ressources toohelp résoudre votre problème.</span><span class="sxs-lookup"><span data-stu-id="52385-447">If none of hello troubleshooting information in this section helps you, you can also use hello following resources toohelp resolve your problem.</span></span>

* <span data-ttu-id="52385-448">Les clients bénéficiant du Support Premier peuvent soumettre un cas de support via le site [Premier](https://premier.microsoft.com/)</span><span class="sxs-lookup"><span data-stu-id="52385-448">Customers with Premier support can log a support case via [Premier](https://premier.microsoft.com/)</span></span>
* <span data-ttu-id="52385-449">Clients avec les contrats de support Azure peuvent se connecter les cas de prise en charge hello [portail Azure](https://manage.windowsazure.com/?getsupport=true)</span><span class="sxs-lookup"><span data-stu-id="52385-449">Customers with Azure support agreements can log support cases in hello [Azure portal](https://manage.windowsazure.com/?getsupport=true)</span></span>
* <span data-ttu-id="52385-450">Déposer un [problème GitHub](https://github.com/Microsoft/OMS-Agent-for-Linux/issues)</span><span class="sxs-lookup"><span data-stu-id="52385-450">File a [GitHub Issue](https://github.com/Microsoft/OMS-Agent-for-Linux/issues)</span></span>
* <span data-ttu-id="52385-451">Forum de commentaires pour les idées et toocreate un rapport de bogue [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)</span><span class="sxs-lookup"><span data-stu-id="52385-451">Feedback forum for ideas and toocreate a bug report [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)</span></span>

### <a name="important-log-locations"></a><span data-ttu-id="52385-452">Emplacement de journaux importants</span><span class="sxs-lookup"><span data-stu-id="52385-452">Important log locations</span></span>
| <span data-ttu-id="52385-453">Fichier</span><span class="sxs-lookup"><span data-stu-id="52385-453">File</span></span> | <span data-ttu-id="52385-454">Chemin</span><span class="sxs-lookup"><span data-stu-id="52385-454">Path</span></span> |
| --- | --- |
| <span data-ttu-id="52385-455">Fichier journal de l’Agent OMS pour Linux</span><span class="sxs-lookup"><span data-stu-id="52385-455">OMS Agent for Linux Log File</span></span> |`/var/opt/microsoft/omsagent/<workspace id>/log/omsagent.log ` |
| <span data-ttu-id="52385-456">Fichier journal de configuration de l’Agent OMS</span><span class="sxs-lookup"><span data-stu-id="52385-456">OMS Agent Configuration Log File</span></span> |`/var/opt/microsoft/omsconfig/omsconfig.log` |

### <a name="important-configuration-files"></a><span data-ttu-id="52385-457">Fichiers de configuration importants</span><span class="sxs-lookup"><span data-stu-id="52385-457">Important configuration files</span></span>
| <span data-ttu-id="52385-458">Catégorie</span><span class="sxs-lookup"><span data-stu-id="52385-458">Catergory</span></span> | <span data-ttu-id="52385-459">Emplacement du fichier</span><span class="sxs-lookup"><span data-stu-id="52385-459">File Location</span></span> |
| --- | --- |
| <span data-ttu-id="52385-460">syslog</span><span class="sxs-lookup"><span data-stu-id="52385-460">Syslog</span></span> |<span data-ttu-id="52385-461">`/etc/syslog-ng/syslog-ng.conf` ou `/etc/rsyslog.conf` ou `/etc/rsyslog.d/95-omsagent.conf`</span><span class="sxs-lookup"><span data-stu-id="52385-461">`/etc/syslog-ng/syslog-ng.conf` or `/etc/rsyslog.conf` or `/etc/rsyslog.d/95-omsagent.conf`</span></span> |
| <span data-ttu-id="52385-462">Performances, Nagios, Zabbix, sortie OMS et agent général</span><span class="sxs-lookup"><span data-stu-id="52385-462">Performance, Nagios, Zabbix, OMS output and general agent</span></span> |`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` |
| <span data-ttu-id="52385-463">Configurations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="52385-463">Additional configurations</span></span> |`/etc/opt/microsoft/omsagent/<workspace id>/omsagent.d/*.conf` |

> [!NOTE]
> <span data-ttu-id="52385-464">Les fichiers de changement de configuration pour les compteurs de performances et Syslog sont remplacés si la Configuration du portail OMS est activée.</span><span class="sxs-lookup"><span data-stu-id="52385-464">Editing configuration files for performance counters and syslog are overwritten if OMS Portal Configuration is enabled.</span></span> <span data-ttu-id="52385-465">Vous pouvez désactiver la configuration Bonjour portail OMS (pour tous les nœuds) ou pour les nœuds uniques en exécutant hello suivante :</span><span class="sxs-lookup"><span data-stu-id="52385-465">You can disable configuration in hello OMS Portal (for all nodes) or for single nodes by running hello following:</span></span>
>
>

```
sudo su omsagent -c /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```


### <a name="enable-debug-logging"></a><span data-ttu-id="52385-466">Activer l’enregistrement du débogage</span><span class="sxs-lookup"><span data-stu-id="52385-466">Enable debug logging</span></span>
<span data-ttu-id="52385-467">débogage de tooenable journalisation, vous pouvez utiliser le plug-in sortie hello OMS et la sortie des commentaires.</span><span class="sxs-lookup"><span data-stu-id="52385-467">tooenable debug logging, you can use hello OMS output plugin and verbose output.</span></span>

#### <a name="oms-output-plugin"></a><span data-ttu-id="52385-468">Plug-in de sortie OMS</span><span class="sxs-lookup"><span data-stu-id="52385-468">OMS output plugin</span></span>
<span data-ttu-id="52385-469">FluentD permet hello plug-in toospecify niveaux de journalisation pour les niveaux de journal différent pour les entrées et sorties.</span><span class="sxs-lookup"><span data-stu-id="52385-469">FluentD allows hello plugin toospecify logging levels for different log levels for inputs and outputs.</span></span> <span data-ttu-id="52385-470">toospecify un niveau de journal différent pour la sortie d’OMS, modifier la configuration de l’agent générales de hello Bonjour `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` fichier.</span><span class="sxs-lookup"><span data-stu-id="52385-470">toospecify a different log level for OMS output, edit hello general agent configuration in hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` file.</span></span>

<span data-ttu-id="52385-471">Bas hello hello du fichier de configuration, modifiez hello `log_level` propriété à partir de `info` trop`debug`.</span><span class="sxs-lookup"><span data-stu-id="52385-471">Near hello bottom of hello configuration file, change hello `log_level` property from `info` too`debug`.</span></span>

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

<span data-ttu-id="52385-472">Enregistrement de débogage vous permet de toohello de téléchargements toosee traités par lot Service OMS séparé par type, le nombre d’éléments de données et durée toosend.</span><span class="sxs-lookup"><span data-stu-id="52385-472">Debug logging allows you toosee batched uploads toohello OMS Service separated by type, number of data items, and time taken toosend.</span></span>

<span data-ttu-id="52385-473">*Exemple de journal activé pour le débogage :*</span><span class="sxs-lookup"><span data-stu-id="52385-473">*Example debug enabled log:*</span></span>

```
Success sending oms.nagios x 1 in 0.14s
Success sending oms.omi x 4 in 0.52s
Success sending oms.syslog.authpriv.info x 1 in 0.91s
```

#### <a name="verbose-output"></a><span data-ttu-id="52385-474">Sortie détaillée.</span><span class="sxs-lookup"><span data-stu-id="52385-474">Verbose output</span></span>
<span data-ttu-id="52385-475">Au lieu d’utiliser le plug-in sortie hello OMS, vous pouvez également directement la sortie des éléments de données trop`stdout`, qui est visible dans hello Agent OMS pour Linux du journal.</span><span class="sxs-lookup"><span data-stu-id="52385-475">Instead of using hello OMS output plugin, you can also output data items directly too`stdout`, which is visible in hello OMS Agent for Linux log file.</span></span>

<span data-ttu-id="52385-476">Dans fichier de configuration générale de l’agent hello OMS à `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, commentez hello OMS plug-in de sortie en ajoutant un `#` devant chaque ligne.</span><span class="sxs-lookup"><span data-stu-id="52385-476">In hello OMS general agent configuration file at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, comment-out hello OMS output plugin by adding a `#` in front of each line.</span></span>

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

<span data-ttu-id="52385-477">Hello plug-in de la sortie ci-dessous, de supprimer le commentaire hello Bonjour suivant la section en supprimant hello `#` symbole au début de hello de chaque ligne.</span><span class="sxs-lookup"><span data-stu-id="52385-477">Below hello output plugin, remove hello comment in hello following section by removing hello `#` symbol at hello beginning of each line.</span></span>

```
<match **>
  type stdout
</match>
```

### <a name="forwarded-syslog-messages-do-not-appear-in-hello-log"></a><span data-ttu-id="52385-478">Les messages Syslog transférés n’apparaissent pas dans le journal de hello</span><span class="sxs-lookup"><span data-stu-id="52385-478">Forwarded Syslog messages do not appear in hello log</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="52385-479">Causes probables</span><span class="sxs-lookup"><span data-stu-id="52385-479">Probable causes</span></span>
* <span data-ttu-id="52385-480">Hello configuration appliquée toohello Linux server ne pas autoriser la collecte d’installations de hello envoyé et/ou niveaux de journal</span><span class="sxs-lookup"><span data-stu-id="52385-480">hello configuration applied toohello Linux server does not allow collection of hello sent facilities and/or log levels</span></span>
* <span data-ttu-id="52385-481">Syslog n'est pas transmis correctement toohello Linux server</span><span class="sxs-lookup"><span data-stu-id="52385-481">Syslog is not being forwarded correctly toohello Linux server</span></span>
* <span data-ttu-id="52385-482">nombre de Hello de messages transférés par seconde est trop élevée pour la configuration de base hello Hello Agent OMS pour Linux toohandle</span><span class="sxs-lookup"><span data-stu-id="52385-482">hello number of messages being forwarded per second are too large for hello base configuration of hello OMS Agent for Linux toohandle</span></span>

#### <a name="resolutions"></a><span data-ttu-id="52385-483">Résolutions</span><span class="sxs-lookup"><span data-stu-id="52385-483">Resolutions</span></span>
* <span data-ttu-id="52385-484">Vérifiez que la configuration hello Bonjour portail OMS pour Syslog a toutes les installations de hello et niveaux de journal correct hello</span><span class="sxs-lookup"><span data-stu-id="52385-484">Verify that hello configuration in hello OMS Portal for Syslog has all hello facilities and hello correct log levels</span></span>
  * <span data-ttu-id="52385-485">**Portail OMS &gt; Paramètres &gt; Données &gt; Syslog**</span><span class="sxs-lookup"><span data-stu-id="52385-485">**OMS Portal > Settings > Data > Syslog**</span></span>
* <span data-ttu-id="52385-486">Vérifiez que syslog natif démons de messagerie (`rsyslog`, `syslog-ng`) est en mesure de tooreceive messages hello transmis</span><span class="sxs-lookup"><span data-stu-id="52385-486">Verify that native syslog messaging daemons (`rsyslog`, `syslog-ng`) are able tooreceive hello forwarded messages</span></span>
* <span data-ttu-id="52385-487">Vérifiez les paramètres de pare-feu sur hello Syslog serveur tooensure que les messages ne sont pas bloqués</span><span class="sxs-lookup"><span data-stu-id="52385-487">Check firewall settings on hello Syslog server tooensure that messages are not being blocked</span></span>
* <span data-ttu-id="52385-488">Simuler un tooOMS de message Syslog à l’aide de hello `logger` commande - par exemple :</span><span class="sxs-lookup"><span data-stu-id="52385-488">Simulate a Syslog message tooOMS using hello `logger` command - for example:</span></span>
  * `logger -p local0.err "This is my test message"`

### <a name="problems-connecting-toooms-when-using-a-proxy"></a><span data-ttu-id="52385-489">Problèmes de connexion tooOMS lors de l’utilisation d’un proxy</span><span class="sxs-lookup"><span data-stu-id="52385-489">Problems connecting tooOMS when using a proxy</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="52385-490">Causes probables</span><span class="sxs-lookup"><span data-stu-id="52385-490">Probable causes</span></span>
* <span data-ttu-id="52385-491">Hello de proxy spécifié lorsque l’agent de hello lors de l’installation et la configuration est incorrecte</span><span class="sxs-lookup"><span data-stu-id="52385-491">hello proxy specified when installing and configuring hello agent is incorrect</span></span>
* <span data-ttu-id="52385-492">points de terminaison de Service OMS Hello ne sont pas whitelistested dans votre centre de données</span><span class="sxs-lookup"><span data-stu-id="52385-492">hello OMS Service endpoints are not whitelistested in your datacenter</span></span>

#### <a name="resolutions"></a><span data-ttu-id="52385-493">Résolutions</span><span class="sxs-lookup"><span data-stu-id="52385-493">Resolutions</span></span>
* <span data-ttu-id="52385-494">Réinstallez hello Agent OMS pour Linux à l’aide de hello suivant de commande avec l’option de hello `-v` activé.</span><span class="sxs-lookup"><span data-stu-id="52385-494">Reinstall hello OMS Agent for Linux using hello following command with hello option `-v` enabled.</span></span> <span data-ttu-id="52385-495">Ainsi, la sortie des commentaires de l’agent de hello qui se connectent via hello proxy toohello Service OMS.</span><span class="sxs-lookup"><span data-stu-id="52385-495">This allows verbose output of hello agent connecting through hello proxy toohello OMS Service.</span></span>
  * `/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`
  * <span data-ttu-id="52385-496">Passez en revue la documentation hello pour le proxy d’OMS à [agent hello de configuration pour une utilisation avec un serveur proxy HTTP](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server)</span><span class="sxs-lookup"><span data-stu-id="52385-496">Review hello documentation for OMS proxy at [Configuring hello agent for use with an HTTP proxy server](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server)</span></span>
* <span data-ttu-id="52385-497">Vérifiez que hello suivant les points de terminaison de Service OMS sont dans la liste approuvée</span><span class="sxs-lookup"><span data-stu-id="52385-497">Verify that hello following OMS Service endpoints are whitelisted</span></span>

| <span data-ttu-id="52385-498">Ressource de l'agent</span><span class="sxs-lookup"><span data-stu-id="52385-498">Agent Resource</span></span> | <span data-ttu-id="52385-499">Ports</span><span class="sxs-lookup"><span data-stu-id="52385-499">Ports</span></span> |
| --- | --- |
| <span data-ttu-id="52385-500">&#42;.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="52385-500">&#42;.ods.opinsights.azure.com</span></span> |<span data-ttu-id="52385-501">Port 443</span><span class="sxs-lookup"><span data-stu-id="52385-501">Port 443</span></span> |
| <span data-ttu-id="52385-502">&#42;.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="52385-502">&#42;.oms.opinsights.azure.com</span></span> |<span data-ttu-id="52385-503">Port 443</span><span class="sxs-lookup"><span data-stu-id="52385-503">Port 443</span></span> |
| <span data-ttu-id="52385-504">ods.systemcenteradvisor.com</span><span class="sxs-lookup"><span data-stu-id="52385-504">ods.systemcenteradvisor.com</span></span> |<span data-ttu-id="52385-505">Port 443</span><span class="sxs-lookup"><span data-stu-id="52385-505">Port 443</span></span> |
| <span data-ttu-id="52385-506">&#42;.blob.core.windows.net/</span><span class="sxs-lookup"><span data-stu-id="52385-506">&#42;.blob.core.windows.net/</span></span> |<span data-ttu-id="52385-507">Port 443</span><span class="sxs-lookup"><span data-stu-id="52385-507">Port 443</span></span> |

### <a name="a-403-error-is-displayed-when-onboarding"></a><span data-ttu-id="52385-508">Une erreur 403 s’affiche lors de l’intégration</span><span class="sxs-lookup"><span data-stu-id="52385-508">A 403 error is displayed when onboarding</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="52385-509">Causes probables</span><span class="sxs-lookup"><span data-stu-id="52385-509">Probable causes</span></span>
* <span data-ttu-id="52385-510">hello date et l’heure sont incorrectes sur le serveur Linux</span><span class="sxs-lookup"><span data-stu-id="52385-510">hello date and time are incorrect on Linux Server</span></span>
* <span data-ttu-id="52385-511">Hello ID de l’espace de travail et la clé d’espace de travail utilisée sont incorrectes</span><span class="sxs-lookup"><span data-stu-id="52385-511">hello Workspace ID and Workspace Key used are incorrect</span></span>

#### <a name="resolution"></a><span data-ttu-id="52385-512">Résolution :</span><span class="sxs-lookup"><span data-stu-id="52385-512">Resolution</span></span>
* <span data-ttu-id="52385-513">Vérifiez le temps de hello sur votre serveur Linux avec hello `date` commande.</span><span class="sxs-lookup"><span data-stu-id="52385-513">Verify hello time on your Linux server with hello `date` command.</span></span> <span data-ttu-id="52385-514">Si hello données sont supérieures ou inférieure à 15 minutes à partir de hello heure actuelle, l’intégration échoue.</span><span class="sxs-lookup"><span data-stu-id="52385-514">If hello data is greater than or less than 15 minutes from hello current time, then onboarding fails.</span></span> <span data-ttu-id="52385-515">toocorrect, mettre à jour la date de hello et/ou de fuseau horaire de votre serveur Linux.</span><span class="sxs-lookup"><span data-stu-id="52385-515">toocorrect this, update hello date and/or timezone of your Linux server.</span></span>
* <span data-ttu-id="52385-516">version la plus récente de l’Agent OMS pour Linux de hello Hello vous avertit si une différence de temps est entraînent l’échec de l’intégration</span><span class="sxs-lookup"><span data-stu-id="52385-516">hello latest version of hello OMS Agent for Linux notifies you if a time difference is causing onboarding failure</span></span>
* <span data-ttu-id="52385-517">À l’aide de RE-onboard hello correct ID et la clé de l’espace de travail.</span><span class="sxs-lookup"><span data-stu-id="52385-517">Re-onboard using hello correct Workspace ID and Workspace Key.</span></span> <span data-ttu-id="52385-518">Consultez [l’intégration à l’aide de la ligne de commande hello](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="52385-518">See  [Onboarding using hello command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>

### <a name="a-500-error-or-404-error-appears-in-hello-log-file-after-onboarding"></a><span data-ttu-id="52385-519">Une erreur 500 ou erreur 404 s’affiche dans le fichier journal de hello après l’intégration</span><span class="sxs-lookup"><span data-stu-id="52385-519">A 500 error or 404 error appears in hello log file after onboarding</span></span>
<span data-ttu-id="52385-520">Il s’agit d’un problème connu qui se produit lors du chargement de première hello de données de Linux dans un espace de travail OMS.</span><span class="sxs-lookup"><span data-stu-id="52385-520">This is a known issue that occurs during hello first upload of Linux data into an OMS workspace.</span></span> <span data-ttu-id="52385-521">Cela n’affecte pas les données envoyées et ne génère pas d’autres problèmes.</span><span class="sxs-lookup"><span data-stu-id="52385-521">This does not affect data being sent or other problems.</span></span> <span data-ttu-id="52385-522">Vous pouvez ignorer les erreurs de hello lorsque initialement l’intégration.</span><span class="sxs-lookup"><span data-stu-id="52385-522">You can ignore hello errors when initially onboarding.</span></span>

### <a name="nagios-data-does-not-appear-in-hello-oms-portal"></a><span data-ttu-id="52385-523">Données de Nagios n’apparaissant pas dans hello portail OMS</span><span class="sxs-lookup"><span data-stu-id="52385-523">Nagios data does not appear in hello OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="52385-524">Causes probables</span><span class="sxs-lookup"><span data-stu-id="52385-524">Probable causes</span></span>
* <span data-ttu-id="52385-525">utilisateur omsagent de Hello n’a pas les autorisations tooread à partir du fichier de journal Nagios hello</span><span class="sxs-lookup"><span data-stu-id="52385-525">hello omsagent user does not have permissions tooread from hello Nagios log file</span></span>
* <span data-ttu-id="52385-526">Hello Nagios source et les sections de filtre sont toujours commentées dans le fichier de omsagent.conf hello</span><span class="sxs-lookup"><span data-stu-id="52385-526">hello Nagios source and filter sections are still commented in hello omsagent.conf file</span></span>

#### <a name="resolutions"></a><span data-ttu-id="52385-527">Résolutions</span><span class="sxs-lookup"><span data-stu-id="52385-527">Resolutions</span></span>
* <span data-ttu-id="52385-528">Ajoutez hello omsagent utilisateur tooread de commande à partir du fichier de Nagios hello.</span><span class="sxs-lookup"><span data-stu-id="52385-528">Add hello omsagent user in order tooread from hello Nagios file.</span></span> <span data-ttu-id="52385-529">Pour plus d’informations, voir [Nagios alerts](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts) (Alertes Nagios).</span><span class="sxs-lookup"><span data-stu-id="52385-529">See [Nagios alerts](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts) for more information.</span></span>
* <span data-ttu-id="52385-530">Dans hello Agent OMS pour le fichier de configuration générale de Linux à `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, vérifiez que **les deux** hello Nagios source et filtre sections comportent des commentaires, supprimés, toohello similaire, l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="52385-530">In hello OMS Agent for Linux general configuration file at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, ensure that **both** hello Nagios source and filter sections have comments removed, similar toohello following example.</span></span>

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


### <a name="linux-data-doesnt-appear-in-hello-oms-portal"></a><span data-ttu-id="52385-531">Les données Linux n’apparaissent pas dans hello portail OMS</span><span class="sxs-lookup"><span data-stu-id="52385-531">Linux data doesn't appear in hello OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="52385-532">Causes probables</span><span class="sxs-lookup"><span data-stu-id="52385-532">Probable causes</span></span>
* <span data-ttu-id="52385-533">Échec de l’intégration toohello Service OMS</span><span class="sxs-lookup"><span data-stu-id="52385-533">Onboarding toohello OMS Service failed</span></span>
* <span data-ttu-id="52385-534">Connexion toohello Service OMS est bloquée.</span><span class="sxs-lookup"><span data-stu-id="52385-534">Connection toohello OMS Service is blocked</span></span>
* <span data-ttu-id="52385-535">Hello Agent OMS pour Linux données est sauvegardée</span><span class="sxs-lookup"><span data-stu-id="52385-535">hello OMS Agent for Linux data is backed-up</span></span>

#### <a name="resolutions"></a><span data-ttu-id="52385-536">Résolutions</span><span class="sxs-lookup"><span data-stu-id="52385-536">Resolutions</span></span>
* <span data-ttu-id="52385-537">Vérifiez que l’intégration de toohello Service OMS a réussi en vérifiant que hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` existe.</span><span class="sxs-lookup"><span data-stu-id="52385-537">Verify that onboarding toohello OMS Service was successful by verifying that hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` exists.</span></span>
* <span data-ttu-id="52385-538">À l’aide de RE-onboard hello la ligne de commande omsadmin.sh.</span><span class="sxs-lookup"><span data-stu-id="52385-538">Re-onboard using hello omsadmin.sh command line.</span></span> <span data-ttu-id="52385-539">Consultez [l’intégration à l’aide de la ligne de commande hello](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="52385-539">See [Onboarding using hello command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>
* <span data-ttu-id="52385-540">Si vous utilisez un proxy, utilisez hello proxy étapes de dépannage ci-dessus</span><span class="sxs-lookup"><span data-stu-id="52385-540">If using a proxy, use hello proxy troubleshooting steps above</span></span>
* <span data-ttu-id="52385-541">Dans certains cas, lorsque hello Agent OMS pour Linux ne peuvent pas communiquer avec hello Service OMS, données sur l’Agent de hello sont taille de mémoire tampon saturée sauvegardé toohello de 50 Mo.</span><span class="sxs-lookup"><span data-stu-id="52385-541">In some cases, when hello OMS Agent for Linux cannot communicate with hello OMS Service, data on hello Agent is backed-up toohello full buffer size of 50 MB.</span></span> <span data-ttu-id="52385-542">Redémarrez hello Agent OMS pour Linux en exécutant hello `/opt/microsoft/omsagent/bin/service_control restart` commande.</span><span class="sxs-lookup"><span data-stu-id="52385-542">Restart hello OMS Agent for Linux by running hello `/opt/microsoft/omsagent/bin/service_control restart` command.</span></span>
  >[AZURE.NOTE] <span data-ttu-id="52385-543">Ce problème est résolu dans l’Agent version 1.1.0-28 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="52385-543">This issue is fixed in Agent version 1.1.0-28 and later.</span></span>

### <a name="syslog-linux-performance-counter-configuration-is-not-applied-in-hello-oms-portal"></a><span data-ttu-id="52385-544">Configuration de compteur de performances Syslog Linux n’est pas appliquée dans portail OMS : hello</span><span class="sxs-lookup"><span data-stu-id="52385-544">Syslog Linux performance counter configuration is not applied in hello OMS portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="52385-545">Causes probables</span><span class="sxs-lookup"><span data-stu-id="52385-545">Probable causes</span></span>
* <span data-ttu-id="52385-546">l’agent de configuration Hello Bonjour Agent OMS pour Linux n’a pas récupéré configuration la plus récente hello à partir du portail OMS hello.</span><span class="sxs-lookup"><span data-stu-id="52385-546">hello configuration agent in hello OMS Agent for Linux has not retrieved hello latest configuration from hello OMS portal.</span></span>
* <span data-ttu-id="52385-547">Hello révision des paramètres dans le portail de hello n'ont pas été appliquées</span><span class="sxs-lookup"><span data-stu-id="52385-547">hello revised settings in hello portal were not applied</span></span>

#### <a name="resolutions"></a><span data-ttu-id="52385-548">Résolutions</span><span class="sxs-lookup"><span data-stu-id="52385-548">Resolutions</span></span>
<span data-ttu-id="52385-549">`omsconfig`est de l’agent de configuration hello Bonjour Agent OMS pour Linux qui Récupère les modifications de configuration du portail OMS toutes les 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="52385-549">`omsconfig` is hello configuration agent in hello OMS Agent for Linux that retrieves OMS portal configuration changes every 5 minutes.</span></span> <span data-ttu-id="52385-550">Cette configuration est appliquée toohello Agent OMS pour Linux les fichiers de configuration situé à `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`.</span><span class="sxs-lookup"><span data-stu-id="52385-550">This configuration is then applied toohello OMS Agent for Linux configuration files located at `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`.</span></span>

* <span data-ttu-id="52385-551">Dans certains cas, les hello Agent OMS pour l’agent de configuration Linux peut-être pas en mesure de toocommunicate avec le service de configuration du portail hello résultant dans la configuration la plus récente ne s’applique ne pas.</span><span class="sxs-lookup"><span data-stu-id="52385-551">In some cases, hello OMS Agent for Linux configuration agent might not be able toocommunicate with hello portal configuration service resulting in latest configuration not being applied.</span></span>
* <span data-ttu-id="52385-552">Vérifiez que hello `omsconfig` agent est installé avec les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="52385-552">Verify that hello `omsconfig` agent is installed with hello following:</span></span>

  * <span data-ttu-id="52385-553">`dpkg --list omsconfig` ou `rpm -qi omsconfig`</span><span class="sxs-lookup"><span data-stu-id="52385-553">`dpkg --list omsconfig` or `rpm -qi omsconfig`</span></span>
  * <span data-ttu-id="52385-554">Le cas contraire, réinstaller la version la plus récente hello Hello Agent OMS pour Linux</span><span class="sxs-lookup"><span data-stu-id="52385-554">If not installed, reinstall hello latest version of hello OMS Agent for Linux</span></span>
* <span data-ttu-id="52385-555">Vérifiez que hello `omsconfig` agent peut communiquer avec hello service OMS</span><span class="sxs-lookup"><span data-stu-id="52385-555">Verify that hello `omsconfig` agent can communicate with hello OMS service</span></span>

  * <span data-ttu-id="52385-556">Exécutez hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` commande</span><span class="sxs-lookup"><span data-stu-id="52385-556">Run hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` command</span></span>
    * <span data-ttu-id="52385-557">Hello commande ci-dessus retourne hello configuration que l’agent récupère à partir du portail hello, notamment les paramètres de Syslog, les compteurs de performances Linux et les journaux personnalisés</span><span class="sxs-lookup"><span data-stu-id="52385-557">hello command above returns hello configuration that agent retrieves from hello portal, including Syslog settings, Linux performance counters, and custom logs</span></span>
    * <span data-ttu-id="52385-558">En cas d’échec de la commande hello ci-dessus, utilisez hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` commande.</span><span class="sxs-lookup"><span data-stu-id="52385-558">If hello command above fails, run hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` command.</span></span> <span data-ttu-id="52385-559">Cette commande force hello omsconfig agent toocommunicate avec hello OMS service tooretrieve hello configuration la plus récente.</span><span class="sxs-lookup"><span data-stu-id="52385-559">This command forces hello omsconfig agent toocommunicate with hello OMS service tooretrieve hello latest configuration.</span></span>

### <a name="custom-linux-log-data-does-not-appear-in-hello-oms-portal"></a><span data-ttu-id="52385-560">Les données de journal Linux personnalisées n’apparaissent pas dans hello portail OMS</span><span class="sxs-lookup"><span data-stu-id="52385-560">Custom Linux log data does not appear in hello OMS Portal</span></span>
#### <a name="probable-causes"></a><span data-ttu-id="52385-561">Causes probables</span><span class="sxs-lookup"><span data-stu-id="52385-561">Probable causes</span></span>
* <span data-ttu-id="52385-562">Échec du Service d’intégration tooOMS</span><span class="sxs-lookup"><span data-stu-id="52385-562">Onboarding tooOMS Service failed</span></span>
* <span data-ttu-id="52385-563">Hello **hello appliquer suivant toomy de configuration des serveurs Linux** paramètre n’a pas été sélectionné.</span><span class="sxs-lookup"><span data-stu-id="52385-563">hello **Apply hello following configuration toomy Linux Servers** setting has not been selected</span></span>
* <span data-ttu-id="52385-564">omsconfig n’a pas récupéré de journal personnalisées de hello plus récente à partir du portail de hello</span><span class="sxs-lookup"><span data-stu-id="52385-564">omsconfig has not picked up hello latest custom log from hello portal</span></span>
* <span data-ttu-id="52385-565">Hello `omsagent` sert de journal personnalisées de hello tooaccess impossible en raison de problèmes d’autorisation tooa ou `omsagent` n’a été trouvé.</span><span class="sxs-lookup"><span data-stu-id="52385-565">hello `omsagent` use is unable tooaccess hello custom log due tooa permissions problem or `omsagent` was not found.</span></span> <span data-ttu-id="52385-566">Dans ce cas, vous verrez hello suivant de sortie :</span><span class="sxs-lookup"><span data-stu-id="52385-566">In this case, you'll see hello following output:</span></span>
  * `[DATETIME] [warn]: file not found. Continuing without tailing it.`
  * `[DATETIME] [error]: file not accessible by omsagent.`
* <span data-ttu-id="52385-567">Il s’agit d’un problème connu avec hello Condition de concurrence qui a été résolu dans hello Agent OMS pour Linux version 1.1.0-217</span><span class="sxs-lookup"><span data-stu-id="52385-567">This is a known issue with hello Race Condition that was fixed in hello OMS Agent for Linux version 1.1.0-217</span></span>

#### <a name="resolutions"></a><span data-ttu-id="52385-568">Résolutions</span><span class="sxs-lookup"><span data-stu-id="52385-568">Resolutions</span></span>
* <span data-ttu-id="52385-569">Vérifiez que vous avez correctement été intégré, en déterminant si hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` fichier existe.</span><span class="sxs-lookup"><span data-stu-id="52385-569">Verify that you've successfully onboarded, by determining whether hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` file exists.</span></span>
  * <span data-ttu-id="52385-570">Si nécessaire, intégrer à nouveau à l’aide de la ligne de commande omsadmin.sh hello.</span><span class="sxs-lookup"><span data-stu-id="52385-570">If needed, onboard again using hello omsadmin.sh command line.</span></span> <span data-ttu-id="52385-571">Consultez [l’intégration à l’aide de la ligne de commande hello](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="52385-571">See [Onboarding using hello command line](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) for more information.</span></span>
* <span data-ttu-id="52385-572">Dans hello portail OMS, sous **paramètres** sur hello **données** , vérifiez que hello **hello appliquer suivant toomy de configuration des serveurs Linux** paramètre est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="52385-572">In hello OMS Portal, under **Settings** on hello **Data** tab, ensure that hello **Apply hello following configuration toomy Linux Servers** setting is selected</span></span>  
  <span data-ttu-id="52385-573">![appliquer la configuration](./media/log-analytics-linux-agents/customloglinuxenabled.png)</span><span class="sxs-lookup"><span data-stu-id="52385-573">![apply configuration](./media/log-analytics-linux-agents/customloglinuxenabled.png)</span></span>
* <span data-ttu-id="52385-574">Vérifiez que hello `omsconfig` agent peut communiquer avec hello service OMS</span><span class="sxs-lookup"><span data-stu-id="52385-574">Verify that hello `omsconfig` agent can communicate with hello OMS service</span></span>

  * <span data-ttu-id="52385-575">Exécutez hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` commande</span><span class="sxs-lookup"><span data-stu-id="52385-575">Run hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` command</span></span>
  * <span data-ttu-id="52385-576">Hello commande ci-dessus retourne hello configuration que l’agent récupère à partir de hello portail, y compris les paramètres de Syslog, compteurs de performances Linux et des journaux personnalisés</span><span class="sxs-lookup"><span data-stu-id="52385-576">hello command above returns hello configuration that agent retrieves from hello Portal, including Syslog settings, Linux performance counters, and custom Logs</span></span>
  * <span data-ttu-id="52385-577">En cas d’échec de la commande hello ci-dessus, utilisez hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` commande.</span><span class="sxs-lookup"><span data-stu-id="52385-577">If hello command above fails, run hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` command.</span></span> <span data-ttu-id="52385-578">Cette commande force hello omsconfig agent toocommunicate avec le service OMS et récupérer la configuration la plus récente hello.</span><span class="sxs-lookup"><span data-stu-id="52385-578">This command forces hello omsconfig agent toocommunicate with OMS service and retrieve hello latest configuration.</span></span>

<span data-ttu-id="52385-579">Au lieu de hello Agent OMS pour utilisateur Linux en cours d’exécution en tant qu’un utilisateur doté de privilèges `root`, hello Agent OMS pour Linux s’exécute en tant que hello `omsagent` utilisateur.</span><span class="sxs-lookup"><span data-stu-id="52385-579">Instead of hello OMS Agent for Linux user running as a privileged user `root`, hello OMS Agent for Linux runs as hello `omsagent` user.</span></span> <span data-ttu-id="52385-580">Dans la plupart des cas, l’autorisation explicite doit être octroyés à l’utilisateur de toohello dans l’ordre tooread certains fichiers.</span><span class="sxs-lookup"><span data-stu-id="52385-580">In most cases, explicit permission must be granted toohello user in order tooread certain files.</span></span>

<span data-ttu-id="52385-581">autorisation de toogrant trop`omsagent` utilisateur, exécutez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="52385-581">toogrant permission too`omsagent` user, run hello following commands:</span></span>

1. <span data-ttu-id="52385-582">Ajouter hello `omsagent` groupe spécifique d’utilisateurs tooa avec`sudo usermod -a -G <GROUPNAME> <USERNAME>`</span><span class="sxs-lookup"><span data-stu-id="52385-582">Add hello `omsagent` user tooa specific group with `sudo usermod -a -G <GROUPNAME> <USERNAME>`</span></span>
2. <span data-ttu-id="52385-583">Accorder l’accès en lecture universel toohello de fichier requis avec`sudo chmod -R ugo+rw <FILE DIRECTORY>`</span><span class="sxs-lookup"><span data-stu-id="52385-583">Grant universal read access toohello required file with `sudo chmod -R ugo+rw <FILE DIRECTORY>`</span></span>

<span data-ttu-id="52385-584">Il existe un problème connu avec la Condition de concurrence qui a été résolu dans hello Agent OMS pour Linux version 1.1.0-217 de hello.</span><span class="sxs-lookup"><span data-stu-id="52385-584">There is a known issue with hello Race Condition that was fixed in hello OMS Agent for Linux version 1.1.0-217.</span></span> <span data-ttu-id="52385-585">Après la mise à jour de l’agent toohello plus récent, exécutez hello suivant commande tooget hello version la plus récente du plug-in de la sortie hello :</span><span class="sxs-lookup"><span data-stu-id="52385-585">After updating toohello latest agent, run hello following command tooget hello latest version of hello output plugin:</span></span>

```
sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf
```

## <a name="known-limitations"></a><span data-ttu-id="52385-586">Limites connues</span><span class="sxs-lookup"><span data-stu-id="52385-586">Known limitations</span></span>
<span data-ttu-id="52385-587">Passez en revue hello suivant toolearn sections sur les limites actuelles de hello Agent OMS pour Linux.</span><span class="sxs-lookup"><span data-stu-id="52385-587">Review hello following sections toolearn about current limitations of hello OMS Agent for Linux.</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="52385-588">Azure Diagnostics</span><span class="sxs-lookup"><span data-stu-id="52385-588">Azure Diagnostics</span></span>
<span data-ttu-id="52385-589">Pour les machines virtuelles Linux s’exécutant dans Azure, des étapes supplémentaires peuvent être collecte des données tooallow requis par les Diagnostics Azure et Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="52385-589">For Linux virtual machines running in Azure, additional steps may be required tooallow data collection by Azure Diagnostics and Operations Management Suite.</span></span> <span data-ttu-id="52385-590">**La version 2.2** hello Extension Diagnostics pour Linux est nécessaire pour la compatibilité avec hello Agent OMS pour Linux.</span><span class="sxs-lookup"><span data-stu-id="52385-590">**Version 2.2** of hello Diagnostics Extension for Linux is required for compatibility with hello OMS Agent for Linux.</span></span>

<span data-ttu-id="52385-591">Pour plus d’informations sur l’installation et configuration de hello Extension Diagnostics pour Linux, consultez [utiliser tooenable de commande CLI d’Azure hello Extension Diagnostics Linux](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension).</span><span class="sxs-lookup"><span data-stu-id="52385-591">For more information on installing and configuring hello Diagnostic Extension for Linux, see [Use hello Azure CLI command tooenable Linux Diagnostic Extension](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension).</span></span>

<span data-ttu-id="52385-592">**Mise à niveau hello Extension de Diagnostics Linux à partir de 2.0 too2.2 ASM CLI de Azure :**</span><span class="sxs-lookup"><span data-stu-id="52385-592">**Upgrading hello Linux Diagnostics Extension from 2.0 too2.2 Azure CLI ASM:**</span></span>

```
azure vm extension set -u <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.0
azure vm extension set <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

<span data-ttu-id="52385-593">**ARM**</span><span class="sxs-lookup"><span data-stu-id="52385-593">**ARM**</span></span>

```
azure vm extension set -u <resource-group> <vm-name> Microsoft.Insights.VMDiagnosticsSettings Microsoft.OSTCExtensions 2.0
azure vm extension set <resource-group> <vm-name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

<span data-ttu-id="52385-594">Ces exemples de commandes font référence à un fichier nommé PrivateConfig.json.</span><span class="sxs-lookup"><span data-stu-id="52385-594">These command examples reference a file named PrivateConfig.json.</span></span> <span data-ttu-id="52385-595">format Hello de ce fichier doit ressembler à hello suivant l’exemple.</span><span class="sxs-lookup"><span data-stu-id="52385-595">hello format of that file should resemble hello following sample.</span></span>

```
    {
    "storageAccountName":"hello storage account tooreceive data",
    "storageAccountKey":"hello key of hello account"
    }
```

### <a name="sysklog-is-not-supported"></a><span data-ttu-id="52385-596">Sysklog n’est pas pris en charge</span><span class="sxs-lookup"><span data-stu-id="52385-596">Sysklog is not supported</span></span>
<span data-ttu-id="52385-597">Rsyslog ou syslog-ng est des messages syslog toocollect requis.</span><span class="sxs-lookup"><span data-stu-id="52385-597">Either rsyslog or syslog-ng are required toocollect syslog messages.</span></span> <span data-ttu-id="52385-598">démon syslog par défaut de Hello version 5 de Red Hat Enterprise Linux, CentOS et Oracle Linux (sysklog) n’est pas pris en charge pour la collecte d’événements syslog.</span><span class="sxs-lookup"><span data-stu-id="52385-598">hello default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="52385-599">toocollect les données syslog de cette version de ces distributions, hello rsyslog démon doit être installé et configuré tooreplace sysklog.</span><span class="sxs-lookup"><span data-stu-id="52385-599">toocollect syslog data from this version of these distributions, hello rsyslog daemon should be installed and configured tooreplace sysklog.</span></span> <span data-ttu-id="52385-600">Pour plus d’informations sur le remplacement de sysklog par rsyslog, consultez [installer le RPM rsyslog de hello nouvellement créé](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM).</span><span class="sxs-lookup"><span data-stu-id="52385-600">For more information on replacing sysklog with rsyslog, see [Install hello newly built rsyslog RPM](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM).</span></span>

## <a name="next-steps"></a><span data-ttu-id="52385-601">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="52385-601">Next Steps</span></span>
* <span data-ttu-id="52385-602">[Ajouter des solutions d’Analytique de journal à partir de la galerie des Solutions de hello](log-analytics-add-solutions.md) tooadd fonctionnalité et collecter les données.</span><span class="sxs-lookup"><span data-stu-id="52385-602">[Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md) tooadd functionality and gather data.</span></span>
* <span data-ttu-id="52385-603">Se familiariser avec [recherche de journal](log-analytics-log-searches.md) tooview détaillées des informations collectées par les solutions.</span><span class="sxs-lookup"><span data-stu-id="52385-603">Get familiar with [log searches](log-analytics-log-searches.md) tooview detailed information gathered by solutions.</span></span>
* <span data-ttu-id="52385-604">Utilisez [tableaux de bord](log-analytics-dashboards.md) toosave et afficher vos propres recherche.</span><span class="sxs-lookup"><span data-stu-id="52385-604">Use [dashboards](log-analytics-dashboards.md) toosave and display your own custom searches.</span></span>
