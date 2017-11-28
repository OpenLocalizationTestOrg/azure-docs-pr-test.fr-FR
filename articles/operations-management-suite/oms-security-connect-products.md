---
title: "aaaConnecting vos produits de sécurité toohello sécurité d’Operations Management Suite (OMS) et la Solution d’Audit | Documents Microsoft"
description: "Ce document vous aide à vous tooconnect votre tooOperations de produits de sécurité Gestion Suite de Solution de sécurité et d’Audit à l’aide du Format d’événement commun."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 46eee484-e078-4bad-8c89-c88a3508f6aa
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: yurid
ms.openlocfilehash: 0f4b372d0379987c4e249628a3c8d52733be65c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-your-security-products-toohello-operations-management-suite-oms-security-and-audit-solution"></a><span data-ttu-id="c695c-103">La connexion de vos produits de sécurité toohello sécurité d’Operations Management Suite (OMS) et la Solution d’Audit</span><span class="sxs-lookup"><span data-stu-id="c695c-103">Connecting your security products toohello Operations Management Suite (OMS) Security and Audit Solution</span></span> 
<span data-ttu-id="c695c-104">Ce document vous permet de connecter vos produits de sécurité en hello sécurité OMS et de la Solution d’Audit.</span><span class="sxs-lookup"><span data-stu-id="c695c-104">This document helps you connect your security products into hello OMS Security and Audit Solution.</span></span> <span data-ttu-id="c695c-105">Hello sources suivantes est prises en charge :</span><span class="sxs-lookup"><span data-stu-id="c695c-105">hello following sources are supported:</span></span>

- <span data-ttu-id="c695c-106">Événements au format d’événement courant (CEF)</span><span class="sxs-lookup"><span data-stu-id="c695c-106">Common Event Format (CEF) events</span></span>
- <span data-ttu-id="c695c-107">Événements Cisco ASA</span><span class="sxs-lookup"><span data-stu-id="c695c-107">Cisco ASA events</span></span>


## <a name="what-is-cef"></a><span data-ttu-id="c695c-108">Qu’est-ce que CEF ?</span><span class="sxs-lookup"><span data-stu-id="c695c-108">What is CEF?</span></span>
<span data-ttu-id="c695c-109">Format d’événement commun (CEF) est un format standard en plus des messages Syslog, utilisé par nombreux fournisseurs tooallow événement interopérabilité de la sécurité entre différentes plateformes.</span><span class="sxs-lookup"><span data-stu-id="c695c-109">Common Event Format (CEF) is an industry standard format on top of Syslog messages, used by many security vendors tooallow event interoperability among different platforms.</span></span> <span data-ttu-id="c695c-110">OMS Solution de sécurité et d’Audit prennent en charge les intégrer les données à l’aide de CEF, ce qui vous permet de tooconnect vos produits de sécurité avec la sécurité d’OMS.</span><span class="sxs-lookup"><span data-stu-id="c695c-110">OMS Security and Audit Solution support data ingestion using CEF, which enables you tooconnect your security products with OMS Security.</span></span> 

<span data-ttu-id="c695c-111">En connectant votre tooOMS de source de données, vous êtes parti tootake en mesure de hello suivant des fonctions qui font partie de cette plateforme :</span><span class="sxs-lookup"><span data-stu-id="c695c-111">By connecting your data source tooOMS, you are able tootake advantage of hello following capabilities that are part of this platform:</span></span>

- <span data-ttu-id="c695c-112">Recherche et corrélation</span><span class="sxs-lookup"><span data-stu-id="c695c-112">Search & Correlation</span></span>
- <span data-ttu-id="c695c-113">Audit</span><span class="sxs-lookup"><span data-stu-id="c695c-113">Auditing</span></span>
- <span data-ttu-id="c695c-114">Alerte</span><span class="sxs-lookup"><span data-stu-id="c695c-114">Alert</span></span>
- <span data-ttu-id="c695c-115">Informations sur les menaces</span><span class="sxs-lookup"><span data-stu-id="c695c-115">Threat Intelligence</span></span>
- <span data-ttu-id="c695c-116">Problèmes notables</span><span class="sxs-lookup"><span data-stu-id="c695c-116">Notable Issues</span></span>

## <a name="collection-of-security-solution-logs"></a><span data-ttu-id="c695c-117">Collection des journaux des solutions de sécurité</span><span class="sxs-lookup"><span data-stu-id="c695c-117">Collection of security solution logs</span></span>

<span data-ttu-id="c695c-118">OMS Security prend en charge la collecte de journaux à l’aide du format CEF sur Syslogs et des journaux [Cisco ASA](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/).</span><span class="sxs-lookup"><span data-stu-id="c695c-118">OMS Security supports collection of logs using CEF over Syslogs and [Cisco ASA](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/) logs.</span></span> <span data-ttu-id="c695c-119">Dans cet exemple, la source de hello (ordinateur qui génère des journaux de hello) est un ordinateur Linux en cours d’exécution les démon syslog-ng et cible de hello est sécurité OMS.</span><span class="sxs-lookup"><span data-stu-id="c695c-119">In this example, hello source (computer that generates hello logs) is a Linux computer running syslog-ng daemon and hello target is OMS Security.</span></span> <span data-ttu-id="c695c-120">Vous devez hello tooperform suivant l’ordinateur Linux hello tooprepare tâches :</span><span class="sxs-lookup"><span data-stu-id="c695c-120">tooprepare hello Linux computer you will need tooperform hello following tasks:</span></span>

- <span data-ttu-id="c695c-121">Téléchargez hello Agent OMS pour Linux, version 1.2.0-25 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="c695c-121">Download hello OMS Agent for Linux, version 1.2.0-25 or above.</span></span>
- <span data-ttu-id="c695c-122">Suivez hello section **Guide d’installation rapide** de [cet article](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux) tooinstall et espace de travail tooyour hello intégrer l’agent.</span><span class="sxs-lookup"><span data-stu-id="c695c-122">Follow hello section **Quick Install Guide** from [this article](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux) tooinstall and onboard hello agent tooyour workspace.</span></span>

<span data-ttu-id="c695c-123">En règle générale, l’agent de hello est installé sur un ordinateur différent de hello un sur les journaux de hello sont générés.</span><span class="sxs-lookup"><span data-stu-id="c695c-123">Typically, hello agent is installed on a different computer from hello one on which hello logs are generated.</span></span> <span data-ttu-id="c695c-124">Ordinateur de l’agent de transfert hello journaux toohello nécessitent généralement hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c695c-124">Forwarding hello logs toohello agent machine will usually require hello following steps:</span></span>

- <span data-ttu-id="c695c-125">Configurer hello journalisation produit/machine tooforward hello événements requis toohello démon syslog (rsyslog ou syslog-ng) sur l’ordinateur agent hello.</span><span class="sxs-lookup"><span data-stu-id="c695c-125">Configure hello logging product/machine tooforward hello required events toohello syslog daemon (rsyslog or syslog-ng) on hello agent machine.</span></span>
- <span data-ttu-id="c695c-126">Activer le démon syslog hello messages de tooreceive hello agent ordinateur à partir d’un système distant.</span><span class="sxs-lookup"><span data-stu-id="c695c-126">Enable hello syslog daemon on hello agent machine tooreceive messages from a remote system.</span></span>

<span data-ttu-id="c695c-127">Sur l’ordinateur agent hello, les événements de hello doivent toobe envoyé à partir de hello syslog démon toolocal le port UDP 25226.</span><span class="sxs-lookup"><span data-stu-id="c695c-127">On hello agent machine, hello events need toobe sent from hello syslog daemon toolocal UDP port 25226.</span></span> <span data-ttu-id="c695c-128">Hello agent est en attente pour les événements entrants sur ce port.</span><span class="sxs-lookup"><span data-stu-id="c695c-128">hello agent is listening for incoming events on this port.</span></span> <span data-ttu-id="c695c-129">Hello Voici un exemple de configuration pour l’envoi de tous les événements à partir de l’agent toohello hello système local (vous pouvez modifier hello configuration toofit vos paramètres locaux) :</span><span class="sxs-lookup"><span data-stu-id="c695c-129">hello following is an example configuration for sending all events from hello local system toohello agent (you can modify hello configuration toofit your local settings):</span></span>

1. <span data-ttu-id="c695c-130">Fenêtre de terminal ouverte hello et accédez toohello active */etc/syslog-ng /*</span><span class="sxs-lookup"><span data-stu-id="c695c-130">Open hello terminal window, and go toohello directory */etc/syslog-ng/*</span></span> 
2. <span data-ttu-id="c695c-131">Créer un nouveau fichier *sécurité-config-omsagent.conf* et ajoutez hello suivant contenu : OMS_facility = local4</span><span class="sxs-lookup"><span data-stu-id="c695c-131">Create a new file *security-config-omsagent.conf* and add hello following content:  OMS_facility = local4</span></span>
    
    <span data-ttu-id="c695c-132">filter f_local4_oms { facility(local4); };</span><span class="sxs-lookup"><span data-stu-id="c695c-132">filter f_local4_oms { facility(local4); };</span></span>

    <span data-ttu-id="c695c-133">destination security_oms { tcp("127.0.0.1" port(25226)); };</span><span class="sxs-lookup"><span data-stu-id="c695c-133">destination security_oms { tcp("127.0.0.1" port(25226)); };</span></span>

    <span data-ttu-id="c695c-134">log { source(src); filter(f_local4_oms); destination(security_oms); };</span><span class="sxs-lookup"><span data-stu-id="c695c-134">log { source(src); filter(f_local4_oms); destination(security_oms); };</span></span>
    
3. <span data-ttu-id="c695c-135">Télécharger le fichier de hello *security_events.conf* et le placer à */etc/opt/microsoft/omsagent/conf/omsagent.d/* dans l’ordinateur de l’Agent OMS hello.</span><span class="sxs-lookup"><span data-stu-id="c695c-135">Download hello file *security_events.conf* and place at */etc/opt/microsoft/omsagent/conf/omsagent.d/* in hello OMS Agent computer.</span></span>
4. <span data-ttu-id="c695c-136">Tapez la commande hello ci-dessous démon syslog de hello toorestart : *pour exécuter syslog-ng :*</span><span class="sxs-lookup"><span data-stu-id="c695c-136">Type hello command below toorestart hello syslog daemon:  *For syslog-ng run:*</span></span>
    
    ```
    sudo service rsyslog restart
    ```

    <span data-ttu-id="c695c-137">*Pour rsyslog exécutez :*</span><span class="sxs-lookup"><span data-stu-id="c695c-137">*For rsyslog run:*</span></span>
    
    ```
    /etc/init.d/syslog-ng restart
    ```
5. <span data-ttu-id="c695c-138">Tapez la commande hello ci-dessous toorestart hello OMS Agent :</span><span class="sxs-lookup"><span data-stu-id="c695c-138">Type hello command below toorestart hello OMS Agent:</span></span>

    <span data-ttu-id="c695c-139">*Pour syslog-ng, exécutez :*</span><span class="sxs-lookup"><span data-stu-id="c695c-139">*For syslog-ng run:*</span></span>
    
    ```
    sudo service omsagent restart
    ```

    <span data-ttu-id="c695c-140">*Pour rsyslog exécutez :*</span><span class="sxs-lookup"><span data-stu-id="c695c-140">*For rsyslog run:*</span></span>
    
    ```
    systemctl restart omsagent
    ```
6. <span data-ttu-id="c695c-141">Tapez la commande hello ci-dessous et examinez les hello tooconfirm de résultats qu’il n’y a pas d’erreurs dans le journal de l’Agent OMS hello :</span><span class="sxs-lookup"><span data-stu-id="c695c-141">Type hello command below and review hello result tooconfirm that there are no errors in hello OMS Agent log:</span></span>

    ``` 
    tail /var/opt/microsoft/omsagent/log/omsagent.log
    ```

## <a name="reviewing-collected-security-events"></a><span data-ttu-id="c695c-142">Examen des événements de sécurité collectés</span><span class="sxs-lookup"><span data-stu-id="c695c-142">Reviewing collected security events</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

<span data-ttu-id="c695c-143">Après la hello configuration, les événements de sécurité hello démarrera toobe ingéré par la sécurité d’OMS.</span><span class="sxs-lookup"><span data-stu-id="c695c-143">After hello configuration is over, hello security event will start toobe ingested by OMS Security.</span></span> <span data-ttu-id="c695c-144">toovisualize ces événements, ouvrez hello recherche de journal, tapez la commande hello *Type = CommonSecurityLog* hello du champ de recherche et appuyez sur ENTRÉE.</span><span class="sxs-lookup"><span data-stu-id="c695c-144">toovisualize those events, open hello Log Search, type hello command *Type=CommonSecurityLog* in hello search field and press ENTER.</span></span> <span data-ttu-id="c695c-145">Hello suivant montre les résultats hello de cette commande, notez que dans ce cas OMS sécurité déjà ingéré des journaux de sécurité à partir de plusieurs fournisseurs :</span><span class="sxs-lookup"><span data-stu-id="c695c-145">hello following example shows hello result of this command, notice that in this case OMS Security already ingested security logs from multiple vendors:</span></span>
   
![Évaluation de la base de référence de la solution de sécurité et d’audit d’OMS](./media/oms-security-connect-products/oms-security-connect-products-fig1.png)

<span data-ttu-id="c695c-147">Vous pouvez affiner la recherche pour un fournisseur unique, par exemple, toovisualize Cisco en ligne se connecte, tapez : *Type = CommonSecurityLog DeviceVendor = Cisco*.</span><span class="sxs-lookup"><span data-stu-id="c695c-147">You can refine this search for one single vendor, for example, toovisualize online Cisco logs, type: *Type=CommonSecurityLog DeviceVendor=Cisco*.</span></span> <span data-ttu-id="c695c-148">Hello « CommonSecurityLog » a des champs prédéfinis, pour n’importe quel en-tête CEF, y compris l’extensios base hello, lors d’une autre extension « Extension personnalisée » ou non, est inséré dans le champ de « AdditionalExtensions ».</span><span class="sxs-lookup"><span data-stu-id="c695c-148">hello “CommonSecurityLog” has predefined fields for any CEF header including hello basic extensios, while any other extension whether it’s “Custom Extension” or not, will be inserted into "AdditionalExtensions" field.</span></span> <span data-ttu-id="c695c-149">Vous pouvez utiliser les champs de tooget dédié de fonction de champs personnalisés hello à partir de celui-ci.</span><span class="sxs-lookup"><span data-stu-id="c695c-149">You can use hello Custom Fields feature tooget dedicated fields from it.</span></span> 

### <a name="accessing-computers-missing-baseline-assessment"></a><span data-ttu-id="c695c-150">Accès aux ordinateurs sans évaluation de la ligne de base</span><span class="sxs-lookup"><span data-stu-id="c695c-150">Accessing computers missing baseline assessment</span></span>
<span data-ttu-id="c695c-151">OMS prend en charge le profil de base de membre de domaine hello sur Windows Server 2008 R2 jusqu'à tooWindows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="c695c-151">OMS supports hello domain member baseline profile on Windows Server 2008 R2 up tooWindows Server 2012 R2.</span></span> <span data-ttu-id="c695c-152">La ligne de base de Windows Server 2016 n’est pas encore finalisée. Elle sera ajoutée dès sa publication.</span><span class="sxs-lookup"><span data-stu-id="c695c-152">Windows Server 2016 baseline isn’t final yet and will be added as soon as it is published.</span></span> <span data-ttu-id="c695c-153">Tous les autres systèmes d’exploitation analysés par OMS sécurité et Audit évaluation de la ligne de base apparaissent sous hello **ordinateurs manquant d’évaluation de la ligne de base** section.</span><span class="sxs-lookup"><span data-stu-id="c695c-153">All other operating systems scanned via OMS Security and Audit baseline assessment appear under hello **Computers missing baseline assessment** section.</span></span>

## <a name="see-also"></a><span data-ttu-id="c695c-154">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="c695c-154">See also</span></span>
<span data-ttu-id="c695c-155">Dans ce document, vous avez appris comment tooconnect votre tooOMS de solution CEF.</span><span class="sxs-lookup"><span data-stu-id="c695c-155">In this document, you learned how tooconnect your CEF solution tooOMS.</span></span> <span data-ttu-id="c695c-156">toolearn en savoir plus sur la sécurité d’OMS, consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="c695c-156">toolearn more about OMS Security, see hello following articles:</span></span>

* [<span data-ttu-id="c695c-157">Présentation - Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="c695c-157">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="c695c-158">Surveillance et réponse tooSecurity alertes Operations Management Suite de Solution de sécurité et d’Audit</span><span class="sxs-lookup"><span data-stu-id="c695c-158">Monitoring and Responding tooSecurity Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="c695c-159">Surveillance des ressources dans la solution de sécurité et d’audit d’Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="c695c-159">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

