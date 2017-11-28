---
title: "Collecte des performances d’application Linux dans OMS Log Analytics | Documents Microsoft"
description: "Cet article fournit des détails sur la configuration de l’agent OMS pour Linux pour collecter les compteurs de performances pour MySQL et Apache HTTP Server."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: f1d5bde4-6b86-4b8e-b5c1-3ecbaba76198
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/04/2017
ms.author: magoedte
ms.openlocfilehash: 04ea6f728e59ec8b47e54fe45e1adc6cbbfb85ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="collect-performance-counters-for-linux-applications-in-log-analytics"></a><span data-ttu-id="dbab0-103">Collecte des compteurs de performances pour les applications Linux dans Log Analytics</span><span class="sxs-lookup"><span data-stu-id="dbab0-103">Collect performance counters for Linux applications in Log Analytics</span></span> 
<span data-ttu-id="dbab0-104">Cet article fournit des détails sur la configuration de l’[agent OMS pour Linux](https://github.com/Microsoft/OMS-Agent-for-Linux) pour la collecte des compteurs de performances pour des applications spécifiques.</span><span class="sxs-lookup"><span data-stu-id="dbab0-104">This article provides details for configuring the [OMS Agent for Linux](https://github.com/Microsoft/OMS-Agent-for-Linux) to collect performance counters for specific applications.</span></span>  <span data-ttu-id="dbab0-105">Les applications incluses dans cet article sont :</span><span class="sxs-lookup"><span data-stu-id="dbab0-105">The applications included in this article are:</span></span>  

- [<span data-ttu-id="dbab0-106">MySQL</span><span class="sxs-lookup"><span data-stu-id="dbab0-106">MySQL</span></span>](#MySQL)
- [<span data-ttu-id="dbab0-107">Apache HTTP Server</span><span class="sxs-lookup"><span data-stu-id="dbab0-107">Apache HTTP Server</span></span>](#apache-http-server)

## <a name="mysql"></a><span data-ttu-id="dbab0-108">MySQL</span><span class="sxs-lookup"><span data-stu-id="dbab0-108">MySQL</span></span>
<span data-ttu-id="dbab0-109">Si le serveur MySQL ou MariaDB est détecté sur l’ordinateur lorsque l’agent OMS est installé, un fournisseur de surveillance des performances pour le serveur MySQL est automatiquement installé.</span><span class="sxs-lookup"><span data-stu-id="dbab0-109">If MySQL Server or MariaDB Server is detected on the computer when the OMS agent is installed, a performance monitoring provider for MySQL Server will be automatically installed.</span></span> <span data-ttu-id="dbab0-110">Ce fournisseur se connecte au serveur MySQL/MariaDB local pour afficher les statistiques de performances.</span><span class="sxs-lookup"><span data-stu-id="dbab0-110">This provider connects to the local MySQL/MariaDB server to expose performance statistics.</span></span> <span data-ttu-id="dbab0-111">Vous devez configurer les informations d’identification de l’utilisateur MySQL, afin que le fournisseur puisse accéder au serveur MySQL.</span><span class="sxs-lookup"><span data-stu-id="dbab0-111">MySQL user credentials must be configured so that the provider can access the MySQL Server.</span></span>

### <a name="configure-mysql-credentials"></a><span data-ttu-id="dbab0-112">Configuration des informations d’identification de MySQL</span><span class="sxs-lookup"><span data-stu-id="dbab0-112">Configure MySQL credentials</span></span>
<span data-ttu-id="dbab0-113">Le fournisseur MySQL OMI nécessite un utilisateur MySQL préconfiguré et des bibliothèques clientes MySQL installées pour pouvoir interroger les informations d’intégrité et de performances de l’instance MySQL.</span><span class="sxs-lookup"><span data-stu-id="dbab0-113">The MySQL OMI provider requires a preconfigured MySQL user and installed MySQL client libraries in order to query the performance and health information from the MySQL instance.</span></span>  <span data-ttu-id="dbab0-114">Ces informations d’identification sont stockées dans un fichier d’authentification, lui-même stocké sur l’agent Linux.</span><span class="sxs-lookup"><span data-stu-id="dbab0-114">These credentials are stored in an authentication file that's stored on the Linux agent.</span></span>  <span data-ttu-id="dbab0-115">Le fichier d’authentification indique l’adresse de liaison et le port qu’écoute l’instance MySQL, ainsi que les informations d’identification à utiliser pour collecter des mesures.</span><span class="sxs-lookup"><span data-stu-id="dbab0-115">The authentication file specifies what bind-address and port the MySQL instance is listening on and what credentials to use to gather metrics.</span></span>  

<span data-ttu-id="dbab0-116">Pendant l’installation de l’agent OMS pour Linux, le fournisseur MySQL OMI recherche l’adresse de liaison et le port dans les fichiers de configuration my.cnf MySQL (emplacements par défaut), et configurera partiellement le fichier d’authentification OMI MySQL.</span><span class="sxs-lookup"><span data-stu-id="dbab0-116">During installation of the OMS Agent for Linux the MySQL OMI provider will scan MySQL my.cnf configuration files (default locations) for bind-address and port and partially set the MySQL OMI authentication file.</span></span>

<span data-ttu-id="dbab0-117">Le fichier d’authentification MySQL est stocké dans `/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth`.</span><span class="sxs-lookup"><span data-stu-id="dbab0-117">The MySQL authentication file is stored at `/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth`.</span></span>


### <a name="authentication-file-format"></a><span data-ttu-id="dbab0-118">Format du fichier d’authentification</span><span class="sxs-lookup"><span data-stu-id="dbab0-118">Authentication file format</span></span>
<span data-ttu-id="dbab0-119">Le format du fichier d’authentification OMI MySQL est le suivant</span><span class="sxs-lookup"><span data-stu-id="dbab0-119">Following is the format for the MySQL OMI authentication file</span></span>

    [Port]=[Bind-Address], [username], [Base64 encoded Password]
    (Port)=(Bind-Address), (username), (Base64 encoded Password)
    (Port)=(Bind-Address), (username), (Base64 encoded Password)
    AutoUpdate=[true|false]

<span data-ttu-id="dbab0-120">Les entrées du fichier d’authentification sont décrites dans le tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="dbab0-120">The entries in the authentication file are described in the following table.</span></span>

| <span data-ttu-id="dbab0-121">Propriété</span><span class="sxs-lookup"><span data-stu-id="dbab0-121">Property</span></span> | <span data-ttu-id="dbab0-122">Description</span><span class="sxs-lookup"><span data-stu-id="dbab0-122">Description</span></span> |
|:--|:--|
| <span data-ttu-id="dbab0-123">Port</span><span class="sxs-lookup"><span data-stu-id="dbab0-123">Port</span></span> | <span data-ttu-id="dbab0-124">Représente le port actif sur lequel écoute l’instance MySQL.</span><span class="sxs-lookup"><span data-stu-id="dbab0-124">Represents the current port the MySQL instance is listening on.</span></span> <span data-ttu-id="dbab0-125">Le port 0 indique que les propriétés suivantes sont utilisées pour l’instance par défaut.</span><span class="sxs-lookup"><span data-stu-id="dbab0-125">Port 0 specifies that the properties following are used for default instance.</span></span> |
| <span data-ttu-id="dbab0-126">Adresse de liaison</span><span class="sxs-lookup"><span data-stu-id="dbab0-126">Bind-Address</span></span>| <span data-ttu-id="dbab0-127">Adresse de liaison MySQL active.</span><span class="sxs-lookup"><span data-stu-id="dbab0-127">Current MySQL bind-address.</span></span> |
| <span data-ttu-id="dbab0-128">username</span><span class="sxs-lookup"><span data-stu-id="dbab0-128">username</span></span>| <span data-ttu-id="dbab0-129">Utilisateur MySQL utilisé pour surveiller l’instance de serveur MySQL.</span><span class="sxs-lookup"><span data-stu-id="dbab0-129">MySQL user used to use to monitor the MySQL server instance.</span></span> |
| <span data-ttu-id="dbab0-130">Mot de passe encodé en base 64</span><span class="sxs-lookup"><span data-stu-id="dbab0-130">Base64 encoded Password</span></span>| <span data-ttu-id="dbab0-131">Mot de passe de l’utilisateur surveillant MySQL encodé en Base64.</span><span class="sxs-lookup"><span data-stu-id="dbab0-131">Password of the MySQL monitoring user encoded in Base64.</span></span> |
| <span data-ttu-id="dbab0-132">AutoUpdate</span><span class="sxs-lookup"><span data-stu-id="dbab0-132">AutoUpdate</span></span>| <span data-ttu-id="dbab0-133">Indique si les modifications doivent à nouveau être recherchées dans le fichier my.cnf et si le fichier d’authentification MySQL OMI doit être remplacé lorsque le fournisseur MySQL est mis à niveau.</span><span class="sxs-lookup"><span data-stu-id="dbab0-133">Specifies whether to rescan for changes in the my.cnf file and overwrite the MySQL OMI Authentication file when the MySQL OMI Provider is upgraded.</span></span> |

### <a name="default-instance"></a><span data-ttu-id="dbab0-134">Instance par défaut</span><span class="sxs-lookup"><span data-stu-id="dbab0-134">Default instance</span></span>
<span data-ttu-id="dbab0-135">Le fichier d’authentification MySQL OMI peut définir un numéro d’instance et de port par défaut pour gérer plusieurs instances de MySQL sur un hôte Linux plus facilement.</span><span class="sxs-lookup"><span data-stu-id="dbab0-135">The MySQL OMI authentication file can define a default instance and port number to make managing multiple MySQL instances on one Linux host easier.</span></span>  <span data-ttu-id="dbab0-136">L’instance par défaut est définie par une instance avec le port 0.</span><span class="sxs-lookup"><span data-stu-id="dbab0-136">The default instance is denoted by an instance with port 0.</span></span> <span data-ttu-id="dbab0-137">Toutes les instances supplémentaires hériteront des propriétés définies à partir de l’instance par défaut, sauf si elles indiquent des valeurs différentes.</span><span class="sxs-lookup"><span data-stu-id="dbab0-137">All additional instances will inherit properties set from the default instance unless they specify different values.</span></span> <span data-ttu-id="dbab0-138">Par exemple, si l’instance MySQL qui écoute le port 3308 est ajoutée, l’adresse de liaison, le nom d’utilisateur et le mot de passe encodé en Base64 de l’instance par défaut sont utilisés pour tester et surveiller l’instance qui écoute le port 3308.</span><span class="sxs-lookup"><span data-stu-id="dbab0-138">For example, if MySQL instance listening on port ‘3308’ is added, the default instance’s bind-address, username, and Base64 encoded password will be used to try and monitor the instance listening on 3308.</span></span> <span data-ttu-id="dbab0-139">Si l’instance sur le port 3308 est liée à une autre adresse et utilise les mêmes nom d’utilisateur et mot de passe MySQL, seule l’adresse de liaison est nécessaire. Les autres propriétés seront héritées.</span><span class="sxs-lookup"><span data-stu-id="dbab0-139">If the instance on 3308 is bound to another address and uses the same MySQL username and password pair only the bind-address is needed, and the other properties will be inherited.</span></span>

<span data-ttu-id="dbab0-140">Le tableau suivant contient des exemples de paramètres d’instance</span><span class="sxs-lookup"><span data-stu-id="dbab0-140">The following table has example instance settings</span></span> 

| <span data-ttu-id="dbab0-141">Description</span><span class="sxs-lookup"><span data-stu-id="dbab0-141">Description</span></span> | <span data-ttu-id="dbab0-142">Fichier</span><span class="sxs-lookup"><span data-stu-id="dbab0-142">File</span></span> |
|:--|:--|
| <span data-ttu-id="dbab0-143">Instance par défaut et instance avec le port 3308.</span><span class="sxs-lookup"><span data-stu-id="dbab0-143">Default instance and instance with port 3308.</span></span> | `0=127.0.0.1, myuser, cnBwdA==`<br>`3308=, ,`<br>`AutoUpdate=true` |
| <span data-ttu-id="dbab0-144">Instance par défaut et instance avec le port 3308 et un autre nom d’utilisateur et un autre mot de passe.</span><span class="sxs-lookup"><span data-stu-id="dbab0-144">Default instance and instance with port 3308 and different user name and password.</span></span> | `0=127.0.0.1, myuser, cnBwdA==`<br>`3308=127.0.1.1, myuser2,cGluaGVhZA==`<br>`AutoUpdate=true` |


### <a name="mysql-omi-authentication-file-program"></a><span data-ttu-id="dbab0-145">Programme du fichier d’authentification OMI MySQL</span><span class="sxs-lookup"><span data-stu-id="dbab0-145">MySQL OMI Authentication File Program</span></span>
<span data-ttu-id="dbab0-146">Le programme du fichier d’authentification OMI MySQL est inclus dans l’installation du fournisseur OMI MySQL. Il peut être utilisé pour modifier le fichier d’authentification OMI MySQL.</span><span class="sxs-lookup"><span data-stu-id="dbab0-146">Included with the installation of the MySQL OMI provider is a MySQL OMI authentication file program which can be used to edit the MySQL OMI Authentication file.</span></span> <span data-ttu-id="dbab0-147">Vous trouverez le programme du fichier d’authentification à l’emplacement suivant.</span><span class="sxs-lookup"><span data-stu-id="dbab0-147">The authentication file program can be found at the following location.</span></span>

    /opt/microsoft/mysql-cimprov/bin/mycimprovauth

> [!NOTE]
> <span data-ttu-id="dbab0-148">Le fichier des informations d’identification doit être accessible en lecture par le compte omsagent.</span><span class="sxs-lookup"><span data-stu-id="dbab0-148">The credentials file must be readable by the omsagent account.</span></span> <span data-ttu-id="dbab0-149">L’exécution de la commande mycimprovauth comme omsgent est recommandée.</span><span class="sxs-lookup"><span data-stu-id="dbab0-149">Running the mycimprovauth command as omsgent is recommended.</span></span>

<span data-ttu-id="dbab0-150">Le tableau suivant fournit des détails sur la syntaxe pour utiliser mycimprovauth.</span><span class="sxs-lookup"><span data-stu-id="dbab0-150">The following table provides details on the syntax for using mycimprovauth.</span></span>

| <span data-ttu-id="dbab0-151">Opération</span><span class="sxs-lookup"><span data-stu-id="dbab0-151">Operation</span></span> | <span data-ttu-id="dbab0-152">Exemple</span><span class="sxs-lookup"><span data-stu-id="dbab0-152">Example</span></span> | <span data-ttu-id="dbab0-153">Description</span><span class="sxs-lookup"><span data-stu-id="dbab0-153">Description</span></span>
|:--|:--|:--|
| <span data-ttu-id="dbab0-154">autoupdate *false\\</span><span class="sxs-lookup"><span data-stu-id="dbab0-154">autoupdate *false\\</span></span>|<span data-ttu-id="dbab0-155">true*</span><span class="sxs-lookup"><span data-stu-id="dbab0-155">true*</span></span> | <span data-ttu-id="dbab0-156">mycimprovauth autoupdate false</span><span class="sxs-lookup"><span data-stu-id="dbab0-156">mycimprovauth autoupdate false</span></span> | <span data-ttu-id="dbab0-157">Définit si le fichier d’authentification sera automatiquement mis à jour au redémarrage ou lors de la mise à jour.</span><span class="sxs-lookup"><span data-stu-id="dbab0-157">Sets whether or not the authentication file will be automatically updated on restart or update.</span></span> |
| <span data-ttu-id="dbab0-158">default *adresse_de_liaison nom_utilisateur mot_de_passe*</span><span class="sxs-lookup"><span data-stu-id="dbab0-158">default *bind-address username password*</span></span> | <span data-ttu-id="dbab0-159">mycimprovauth default 127.0.0.1 root pwd</span><span class="sxs-lookup"><span data-stu-id="dbab0-159">mycimprovauth default 127.0.0.1 root pwd</span></span> | <span data-ttu-id="dbab0-160">Définit l’instance par défaut dans le fichier d’authentification OMI MySQL.</span><span class="sxs-lookup"><span data-stu-id="dbab0-160">Sets the default instance in the MySQL OMI authentication file.</span></span><br><span data-ttu-id="dbab0-161">Le champ du mot de passe doit être renseigné en texte brut ; le mot de passe dans le fichier d’authentification MySQL OMI sera encodé en Base64.</span><span class="sxs-lookup"><span data-stu-id="dbab0-161">The password field should be entered in plain text - the password in the MySQL OMI authentication file will be Base 64 encoded.</span></span> |
| <span data-ttu-id="dbab0-162">delete *valeur_par_défaut\\</span><span class="sxs-lookup"><span data-stu-id="dbab0-162">delete *default\\</span></span>|<span data-ttu-id="dbab0-163">num_port*</span><span class="sxs-lookup"><span data-stu-id="dbab0-163">port_num*</span></span> | <span data-ttu-id="dbab0-164">mycimprovauth 3308</span><span class="sxs-lookup"><span data-stu-id="dbab0-164">mycimprovauth 3308</span></span> | <span data-ttu-id="dbab0-165">Supprime l’instance indiquée par valeur par défaut ou numéro de port.</span><span class="sxs-lookup"><span data-stu-id="dbab0-165">Deletes the specified instance by either default or by port number.</span></span> |
| <span data-ttu-id="dbab0-166">help</span><span class="sxs-lookup"><span data-stu-id="dbab0-166">help</span></span> | <span data-ttu-id="dbab0-167">mycimprov help</span><span class="sxs-lookup"><span data-stu-id="dbab0-167">mycimprov help</span></span> | <span data-ttu-id="dbab0-168">Imprime une liste de commandes à utiliser.</span><span class="sxs-lookup"><span data-stu-id="dbab0-168">Prints out a list of commands to use.</span></span> |
| <span data-ttu-id="dbab0-169">print</span><span class="sxs-lookup"><span data-stu-id="dbab0-169">print</span></span> | <span data-ttu-id="dbab0-170">mycimprov print</span><span class="sxs-lookup"><span data-stu-id="dbab0-170">mycimprov print</span></span> | <span data-ttu-id="dbab0-171">Imprime un fichier d’authentification OMI MySQL facile à lire.</span><span class="sxs-lookup"><span data-stu-id="dbab0-171">Prints out an easy to read MySQL OMI authentication file.</span></span> |
| <span data-ttu-id="dbab0-172">update num_port *adresse_de_liaison nom_utilisateur mot_de_passe*</span><span class="sxs-lookup"><span data-stu-id="dbab0-172">update port_num *bind-address username password*</span></span> | <span data-ttu-id="dbab0-173">mycimprov update 3307 127.0.0.1 root pwd</span><span class="sxs-lookup"><span data-stu-id="dbab0-173">mycimprov update 3307 127.0.0.1 root pwd</span></span> | <span data-ttu-id="dbab0-174">Met à jour l’instance indiquée ou ajoute l’instance si elle n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="dbab0-174">Updates the specified instance or adds the instance if it does not exist.</span></span> |

<span data-ttu-id="dbab0-175">Les exemples de commande suivants définissent un compte utilisateur par défaut pour le serveur MySQL sur localhost.</span><span class="sxs-lookup"><span data-stu-id="dbab0-175">The following example commands define a default user account for the MySQL server on localhost.</span></span>  <span data-ttu-id="dbab0-176">Le champ du mot de passe doit être renseigné en texte brut ; le mot de passe dans le fichier d’authentification MySQL OMI sera encodé en Base64</span><span class="sxs-lookup"><span data-stu-id="dbab0-176">The password field should be entered in plain text - the password in the MySQL OMI authentication file will be Base 64 encoded</span></span>

    sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>'
    sudo /opt/omi/bin/service_control restart

### <a name="database-permissions-required-for-mysql-performance-counters"></a><span data-ttu-id="dbab0-177">Autorisations de base de données requises pour les compteurs de performances MySQL</span><span class="sxs-lookup"><span data-stu-id="dbab0-177">Database Permissions Required for MySQL Performance Counters</span></span>
<span data-ttu-id="dbab0-178">L’utilisateur MySQL requiert l’accès aux requêtes suivantes pour collecter les données de performances du serveur MySQL.</span><span class="sxs-lookup"><span data-stu-id="dbab0-178">The MySQL User requires access to the following queries to collect MySQL Server performance data.</span></span> 

    SHOW GLOBAL STATUS;
    SHOW GLOBAL VARIABLES:


<span data-ttu-id="dbab0-179">L’utilisateur MySQL requiert également un accès SELECT aux tables par défaut suivantes.</span><span class="sxs-lookup"><span data-stu-id="dbab0-179">The MySQL user also requires SELECT access to the following default tables.</span></span>

- <span data-ttu-id="dbab0-180">information_schema</span><span class="sxs-lookup"><span data-stu-id="dbab0-180">information_schema</span></span>
- <span data-ttu-id="dbab0-181">mysql.</span><span class="sxs-lookup"><span data-stu-id="dbab0-181">mysql.</span></span> 

<span data-ttu-id="dbab0-182">Ces privilèges peuvent être accordés à l’aide des commandes Grant suivantes.</span><span class="sxs-lookup"><span data-stu-id="dbab0-182">These privileges can be granted by running the following grant commands.</span></span>

    GRANT SELECT ON information_schema.* TO ‘monuser’@’localhost’;
    GRANT SELECT ON mysql.* TO ‘monuser’@’localhost’;


> [!NOTE]
> <span data-ttu-id="dbab0-183">Pour accorder des autorisations à un utilisateur surveillant MySQL, l’utilisateur qui souhaite accorder un privilège doit posséder le privilège « GRANT option », ainsi que le privilège accordé.</span><span class="sxs-lookup"><span data-stu-id="dbab0-183">To grant permissions to a MySQL monitoring user the granting user must have the ‘GRANT option’ privilege as well as the privilege being granted.</span></span>

### <a name="define-performance-counters"></a><span data-ttu-id="dbab0-184">Définition des compteurs de performances</span><span class="sxs-lookup"><span data-stu-id="dbab0-184">Define performance counters</span></span>

<span data-ttu-id="dbab0-185">Une fois l’agent OMS pour Linux configuré pour envoyer des données vers Log Analytics, vous devez configurer les compteurs de performances à collecter.</span><span class="sxs-lookup"><span data-stu-id="dbab0-185">Once you configure the OMS Agent for Linux to send data to Log Analytics, you must configure the performance counters to collect.</span></span>  <span data-ttu-id="dbab0-186">Utilisez la procédure décrite dans [Sources de données de performances Windows et Linux dans Log Analytics](log-analytics-data-sources-windows-events.md) avec les compteurs de le tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="dbab0-186">Use the procedure in [Windows and Linux performance data sources in Log Analytics](log-analytics-data-sources-windows-events.md) with the counters in the following table.</span></span>

| <span data-ttu-id="dbab0-187">Nom d’objet</span><span class="sxs-lookup"><span data-stu-id="dbab0-187">Object Name</span></span> | <span data-ttu-id="dbab0-188">Nom de compteur</span><span class="sxs-lookup"><span data-stu-id="dbab0-188">Counter Name</span></span> |
|:--|:--|
| <span data-ttu-id="dbab0-189">MySQL Database</span><span class="sxs-lookup"><span data-stu-id="dbab0-189">MySQL Database</span></span> | <span data-ttu-id="dbab0-190">Disk Space in Bytes</span><span class="sxs-lookup"><span data-stu-id="dbab0-190">Disk Space in Bytes</span></span> |
| <span data-ttu-id="dbab0-191">MySQL Database</span><span class="sxs-lookup"><span data-stu-id="dbab0-191">MySQL Database</span></span> | <span data-ttu-id="dbab0-192">Tables</span><span class="sxs-lookup"><span data-stu-id="dbab0-192">Tables</span></span> |
| <span data-ttu-id="dbab0-193">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="dbab0-193">MySQL Server</span></span> | <span data-ttu-id="dbab0-194">Aborted Connection Pct</span><span class="sxs-lookup"><span data-stu-id="dbab0-194">Aborted Connection Pct</span></span> |
| <span data-ttu-id="dbab0-195">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="dbab0-195">MySQL Server</span></span> | <span data-ttu-id="dbab0-196">Connection Use Pct</span><span class="sxs-lookup"><span data-stu-id="dbab0-196">Connection Use Pct</span></span> |
| <span data-ttu-id="dbab0-197">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="dbab0-197">MySQL Server</span></span> | <span data-ttu-id="dbab0-198">Disk Space Use in Bytes</span><span class="sxs-lookup"><span data-stu-id="dbab0-198">Disk Space Use in Bytes</span></span> |
| <span data-ttu-id="dbab0-199">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="dbab0-199">MySQL Server</span></span> | <span data-ttu-id="dbab0-200">Full Table Scan Pct</span><span class="sxs-lookup"><span data-stu-id="dbab0-200">Full Table Scan Pct</span></span> |
| <span data-ttu-id="dbab0-201">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="dbab0-201">MySQL Server</span></span> | <span data-ttu-id="dbab0-202">InnoDB Buffer Pool Hit Pct</span><span class="sxs-lookup"><span data-stu-id="dbab0-202">InnoDB Buffer Pool Hit Pct</span></span> |
| <span data-ttu-id="dbab0-203">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="dbab0-203">MySQL Server</span></span> | <span data-ttu-id="dbab0-204">InnoDB Buffer Pool Use Pct</span><span class="sxs-lookup"><span data-stu-id="dbab0-204">InnoDB Buffer Pool Use Pct</span></span> |
| <span data-ttu-id="dbab0-205">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="dbab0-205">MySQL Server</span></span> | <span data-ttu-id="dbab0-206">InnoDB Buffer Pool Use Pct</span><span class="sxs-lookup"><span data-stu-id="dbab0-206">InnoDB Buffer Pool Use Pct</span></span> |
| <span data-ttu-id="dbab0-207">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="dbab0-207">MySQL Server</span></span> | <span data-ttu-id="dbab0-208">Key Cache Hit Pct</span><span class="sxs-lookup"><span data-stu-id="dbab0-208">Key Cache Hit Pct</span></span> |
| <span data-ttu-id="dbab0-209">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="dbab0-209">MySQL Server</span></span> | <span data-ttu-id="dbab0-210">Key Cache Use Pct</span><span class="sxs-lookup"><span data-stu-id="dbab0-210">Key Cache Use Pct</span></span> |
| <span data-ttu-id="dbab0-211">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="dbab0-211">MySQL Server</span></span> | <span data-ttu-id="dbab0-212">Key Cache Write Pct</span><span class="sxs-lookup"><span data-stu-id="dbab0-212">Key Cache Write Pct</span></span> |
| <span data-ttu-id="dbab0-213">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="dbab0-213">MySQL Server</span></span> | <span data-ttu-id="dbab0-214">Query Cache Hit Pct</span><span class="sxs-lookup"><span data-stu-id="dbab0-214">Query Cache Hit Pct</span></span> |
| <span data-ttu-id="dbab0-215">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="dbab0-215">MySQL Server</span></span> | <span data-ttu-id="dbab0-216">Query Cache Prunes Pct</span><span class="sxs-lookup"><span data-stu-id="dbab0-216">Query Cache Prunes Pct</span></span> |
| <span data-ttu-id="dbab0-217">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="dbab0-217">MySQL Server</span></span> | <span data-ttu-id="dbab0-218">Query Cache Use Pct</span><span class="sxs-lookup"><span data-stu-id="dbab0-218">Query Cache Use Pct</span></span> |
| <span data-ttu-id="dbab0-219">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="dbab0-219">MySQL Server</span></span> | <span data-ttu-id="dbab0-220">Table Cache Hit Pct</span><span class="sxs-lookup"><span data-stu-id="dbab0-220">Table Cache Hit Pct</span></span> |
| <span data-ttu-id="dbab0-221">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="dbab0-221">MySQL Server</span></span> | <span data-ttu-id="dbab0-222">Table Cache Use Pct</span><span class="sxs-lookup"><span data-stu-id="dbab0-222">Table Cache Use Pct</span></span> |
| <span data-ttu-id="dbab0-223">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="dbab0-223">MySQL Server</span></span> | <span data-ttu-id="dbab0-224">Table Lock Contention Pct</span><span class="sxs-lookup"><span data-stu-id="dbab0-224">Table Lock Contention Pct</span></span> |

## <a name="apache-http-server"></a><span data-ttu-id="dbab0-225">Apache HTTP Server</span><span class="sxs-lookup"><span data-stu-id="dbab0-225">Apache HTTP Server</span></span> 
<span data-ttu-id="dbab0-226">Si Apache HTTP Server est détecté sur l’ordinateur lors de l’installation du groupe omsagent, un fournisseur de surveillance des performances pour Apache HTTP Server est automatiquement installé.</span><span class="sxs-lookup"><span data-stu-id="dbab0-226">If Apache HTTP Server is detected on the computer when the omsagent bundle is installed, a performance monitoring provider for Apache HTTP Server will be automatically installed.</span></span> <span data-ttu-id="dbab0-227">Ce fournisseur repose sur un module Apache qui doit être chargé dans Apache HTTP Server afin d’accéder aux données de performances.</span><span class="sxs-lookup"><span data-stu-id="dbab0-227">This provider relies on an Apache module that must be loaded into the Apache HTTP Server in order to access performance data.</span></span> <span data-ttu-id="dbab0-228">Le module peut être chargé à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="dbab0-228">The module can be loaded with the following command:</span></span>
```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

<span data-ttu-id="dbab0-229">Pour décharger le module de surveillance Apache, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="dbab0-229">To unload the Apache monitoring module, run the following command:</span></span>
```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```

### <a name="define-performance-counters"></a><span data-ttu-id="dbab0-230">Définition des compteurs de performances</span><span class="sxs-lookup"><span data-stu-id="dbab0-230">Define performance counters</span></span>

<span data-ttu-id="dbab0-231">Une fois l’agent OMS pour Linux configuré pour envoyer des données vers Log Analytics, vous devez configurer les compteurs de performances à collecter.</span><span class="sxs-lookup"><span data-stu-id="dbab0-231">Once you configure the OMS Agent for Linux to send data to Log Analytics, you must configure the performance counters to collect.</span></span>  <span data-ttu-id="dbab0-232">Utilisez la procédure décrite dans [Sources de données de performances Windows et Linux dans Log Analytics](log-analytics-data-sources-windows-events.md) avec les compteurs de le tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="dbab0-232">Use the procedure in [Windows and Linux performance data sources in Log Analytics](log-analytics-data-sources-windows-events.md) with the counters in the following table.</span></span>

| <span data-ttu-id="dbab0-233">Nom d’objet</span><span class="sxs-lookup"><span data-stu-id="dbab0-233">Object Name</span></span> | <span data-ttu-id="dbab0-234">Nom de compteur</span><span class="sxs-lookup"><span data-stu-id="dbab0-234">Counter Name</span></span> |
|:--|:--|
| <span data-ttu-id="dbab0-235">Apache HTTP Server</span><span class="sxs-lookup"><span data-stu-id="dbab0-235">Apache HTTP Server</span></span> | <span data-ttu-id="dbab0-236">Busy Workers</span><span class="sxs-lookup"><span data-stu-id="dbab0-236">Busy Workers</span></span> |
| <span data-ttu-id="dbab0-237">Apache HTTP Server</span><span class="sxs-lookup"><span data-stu-id="dbab0-237">Apache HTTP Server</span></span> | <span data-ttu-id="dbab0-238">Idle Workers</span><span class="sxs-lookup"><span data-stu-id="dbab0-238">Idle Workers</span></span> |
| <span data-ttu-id="dbab0-239">Apache HTTP Server</span><span class="sxs-lookup"><span data-stu-id="dbab0-239">Apache HTTP Server</span></span> | <span data-ttu-id="dbab0-240">Pct Busy Workers</span><span class="sxs-lookup"><span data-stu-id="dbab0-240">Pct Busy Workers</span></span> |
| <span data-ttu-id="dbab0-241">Apache HTTP Server</span><span class="sxs-lookup"><span data-stu-id="dbab0-241">Apache HTTP Server</span></span> | <span data-ttu-id="dbab0-242">Total Pct CPU</span><span class="sxs-lookup"><span data-stu-id="dbab0-242">Total Pct CPU</span></span> |
| <span data-ttu-id="dbab0-243">Apache Virtual Host</span><span class="sxs-lookup"><span data-stu-id="dbab0-243">Apache Virtual Host</span></span> | <span data-ttu-id="dbab0-244">Errors per Minute - Client</span><span class="sxs-lookup"><span data-stu-id="dbab0-244">Errors per Minute - Client</span></span> |
| <span data-ttu-id="dbab0-245">Apache Virtual Host</span><span class="sxs-lookup"><span data-stu-id="dbab0-245">Apache Virtual Host</span></span> | <span data-ttu-id="dbab0-246">Errors per Minute - Server</span><span class="sxs-lookup"><span data-stu-id="dbab0-246">Errors per Minute - Server</span></span> |
| <span data-ttu-id="dbab0-247">Apache Virtual Host</span><span class="sxs-lookup"><span data-stu-id="dbab0-247">Apache Virtual Host</span></span> | <span data-ttu-id="dbab0-248">KB per Request</span><span class="sxs-lookup"><span data-stu-id="dbab0-248">KB per Request</span></span> |
| <span data-ttu-id="dbab0-249">Apache Virtual Host</span><span class="sxs-lookup"><span data-stu-id="dbab0-249">Apache Virtual Host</span></span> | <span data-ttu-id="dbab0-250">Requests KB per Second</span><span class="sxs-lookup"><span data-stu-id="dbab0-250">Requests KB per Second</span></span> |
| <span data-ttu-id="dbab0-251">Apache Virtual Host</span><span class="sxs-lookup"><span data-stu-id="dbab0-251">Apache Virtual Host</span></span> | <span data-ttu-id="dbab0-252">Requests per Second</span><span class="sxs-lookup"><span data-stu-id="dbab0-252">Requests per Second</span></span> |



## <a name="next-steps"></a><span data-ttu-id="dbab0-253">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dbab0-253">Next steps</span></span>
* <span data-ttu-id="dbab0-254">[Collecter les compteurs de performances](log-analytics-data-sources-performance-counters.md) à partir d’agents Linux.</span><span class="sxs-lookup"><span data-stu-id="dbab0-254">[Collect performance counters](log-analytics-data-sources-performance-counters.md) from Linux agents.</span></span>
* <span data-ttu-id="dbab0-255">En savoir plus sur les [recherches de journal](log-analytics-log-searches.md) pour analyser les données collectées dans des sources de données et des solutions.</span><span class="sxs-lookup"><span data-stu-id="dbab0-255">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span> 