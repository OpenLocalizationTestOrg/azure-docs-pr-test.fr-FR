---
title: "aaaAzure Forum aux questions sur l’intégration de journal | Documents Microsoft"
description: "Cet article répond à des questions sur l’intégration des journaux Azure."
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TerryLanfear
ms.assetid: d06d1ac5-5c3b-49de-800e-4d54b3064c64
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload8: na
ms.date: 08/07/2017
ms.author: TomSh
ms.custom: azlog
ms.openlocfilehash: e886035c9a180d0cd5fcbe9cc02483782df6dbe4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-log-integration-faq"></a><span data-ttu-id="731a0-103">Forum aux questions sur l’intégration des journaux Azure</span><span class="sxs-lookup"><span data-stu-id="731a0-103">Azure Log Integration FAQ</span></span>
<span data-ttu-id="731a0-104">Cet article contient les réponses à certaines questions fréquemment posées sur l’intégration des journaux Azure.</span><span class="sxs-lookup"><span data-stu-id="731a0-104">This article answers frequently asked questions (FAQ) about Azure Log Integration.</span></span> 

<span data-ttu-id="731a0-105">Intégration d’Azure journal est un service de système d’exploitation Windows que vous pouvez utiliser les journaux bruts toointegrate à partir de vos ressources Azure dans vos systèmes de gestion (SIEM) local sécurité événements et des informations.</span><span class="sxs-lookup"><span data-stu-id="731a0-105">Azure Log Integration is a Windows operating system service that you can use toointegrate raw logs from your Azure resources into your on-premises security information and event management (SIEM) systems.</span></span> <span data-ttu-id="731a0-106">Cette intégration offre un tableau de bord unifiée pour tous vos actifs, localement ou dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="731a0-106">This integration provides a unified dashboard for all your assets, on-premises or in hello cloud.</span></span> <span data-ttu-id="731a0-107">pour vous permettre d’agréger, de mettre en corrélation, d’analyser et d’alerter en cas d’événements de sécurité associés à vos applications.</span><span class="sxs-lookup"><span data-stu-id="731a0-107">You can then aggregate, correlate, analyze, and alert for security events associated with your applications.</span></span>

## <a name="is-hello-azure-log-integration-software-free"></a><span data-ttu-id="731a0-108">Est un logiciel d’intégration des journaux Azure de hello libre ?</span><span class="sxs-lookup"><span data-stu-id="731a0-108">Is hello Azure Log Integration software free?</span></span>
<span data-ttu-id="731a0-109">Oui.</span><span class="sxs-lookup"><span data-stu-id="731a0-109">Yes.</span></span> <span data-ttu-id="731a0-110">Il n’existe aucun frais pour hello logiciel d’intégration des journaux Azure.</span><span class="sxs-lookup"><span data-stu-id="731a0-110">There is no charge for hello Azure Log Integration software.</span></span>

## <a name="where-is-azure-log-integration-available"></a><span data-ttu-id="731a0-111">Où l’intégration des journaux Azure est-elle disponible ?</span><span class="sxs-lookup"><span data-stu-id="731a0-111">Where is Azure Log Integration available?</span></span>

<span data-ttu-id="731a0-112">Elle est actuellement disponible dans les versions commerciales d’Azure et dans Azure Government, mais n’est pas disponible en Chine ni en Allemagne.</span><span class="sxs-lookup"><span data-stu-id="731a0-112">It is currently available in Azure Commercial and Azure Government and is not available in China or Germany.</span></span>

## <a name="how-can-i-see-hello-storage-accounts-from-which-azure-log-integration-is-pulling-azure-vm-logs"></a><span data-ttu-id="731a0-113">Comment puis-je voir les comptes de stockage hello à partir de laquelle intégration des journaux Azure collecte des journaux de machine virtuelle Azure ?</span><span class="sxs-lookup"><span data-stu-id="731a0-113">How can I see hello storage accounts from which Azure Log Integration is pulling Azure VM logs?</span></span>
<span data-ttu-id="731a0-114">Exécutez la commande hello **liste des sources azlog**.</span><span class="sxs-lookup"><span data-stu-id="731a0-114">Run hello command **azlog source list**.</span></span>

## <a name="how-can-i-tell-which-subscription-hello-azure-log-integration-logs-are-from"></a><span data-ttu-id="731a0-115">Comment puis-je savoir quel hello abonnement Azure intégration du journal proviennent de journaux ?</span><span class="sxs-lookup"><span data-stu-id="731a0-115">How can I tell which subscription hello Azure Log Integration logs are from?</span></span>

<span data-ttu-id="731a0-116">Dans les cas de hello des journaux d’audit qui sont placés dans hello **AzureResourcemanagerJson** répertoires, ID d’abonnement hello est dans le nom du fichier journal hello.</span><span class="sxs-lookup"><span data-stu-id="731a0-116">In hello case of audit logs that are placed in hello **AzureResourcemanagerJson** directories, hello subscription ID is in hello log file name.</span></span> <span data-ttu-id="731a0-117">Cela vaut également pour les journaux Bonjour **AzureSecurityCenterJson** dossier.</span><span class="sxs-lookup"><span data-stu-id="731a0-117">This is also true for logs in hello **AzureSecurityCenterJson** folder.</span></span> <span data-ttu-id="731a0-118">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="731a0-118">For example:</span></span>

<span data-ttu-id="731a0-119">20170407T070805_2768037.0000000023.**1111e5ee-1111-111b-a11e-1e111e1111dc**.json</span><span class="sxs-lookup"><span data-stu-id="731a0-119">20170407T070805_2768037.0000000023.**1111e5ee-1111-111b-a11e-1e111e1111dc**.json</span></span>

<span data-ttu-id="731a0-120">Les journaux d’audit Azure Active Directory incluent les ID de client hello en tant que partie du nom de hello.</span><span class="sxs-lookup"><span data-stu-id="731a0-120">Azure Active Directory audit logs include hello tenant ID as part of hello name.</span></span>

<span data-ttu-id="731a0-121">Les journaux de diagnostic sont lus à partir d’un concentrateur d’événements n’incluent pas d’ID d’abonnement hello en tant que partie du nom de hello.</span><span class="sxs-lookup"><span data-stu-id="731a0-121">Diagnostic logs that are read from an event hub do not include hello subscription ID as part of hello name.</span></span> <span data-ttu-id="731a0-122">Au lieu de cela, ils comprennent le nom convivial de hello spécifié dans le cadre de la création de source de concentrateur d’événements hello hello.</span><span class="sxs-lookup"><span data-stu-id="731a0-122">Instead, they include hello friendly name specified as part of hello creation of hello event hub source.</span></span> 

## <a name="how-can-i-update-hello-proxy-configuration"></a><span data-ttu-id="731a0-123">Comment puis-je mettre à jour la configuration proxy hello ?</span><span class="sxs-lookup"><span data-stu-id="731a0-123">How can I update hello proxy configuration?</span></span>
<span data-ttu-id="731a0-124">Si le paramètre de proxy n’autorise pas directement accès au stockage Azure, ouvrez hello **AZLOG. EXE. CONFIGURATION** fichier **c:\Program Files\Microsoft Azure journal intégration**.</span><span class="sxs-lookup"><span data-stu-id="731a0-124">If your proxy setting does not allow Azure storage access directly, open hello **AZLOG.EXE.CONFIG** file in **c:\Program Files\Microsoft Azure Log Integration**.</span></span> <span data-ttu-id="731a0-125">Mise à jour Bonjour fichier tooinclude Bonjour **defaultProxy** section avec l’adresse du proxy hello de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="731a0-125">Update hello file tooinclude hello **defaultProxy** section with hello proxy address of your organization.</span></span> <span data-ttu-id="731a0-126">Une fois la mise à jour de hello est effectuée, arrêter et démarrer le service de hello à l’aide des commandes hello **net stop azlog** et **net démarrer azlog**.</span><span class="sxs-lookup"><span data-stu-id="731a0-126">After hello update is done, stop and start hello service by using hello commands **net stop azlog** and **net start azlog**.</span></span>

    <?xml version="1.0" encoding="utf-8"?>
    <configuration>
      <system.net>
        <connectionManagement>
          <add address="*" maxconnection="400" />
        </connectionManagement>
        <defaultProxy>
          <proxy usesystemdefault="true"
          proxyaddress=http://127.0.0.1:8888
          bypassonlocal="true" />
        </defaultProxy>
      </system.net>
      <system.diagnostics>
        <performanceCounters filemappingsize="20971520" />
      </system.diagnostics>   

## <a name="how-can-i-see-hello-subscription-information-in-windows-events"></a><span data-ttu-id="731a0-127">Comment puis-je voir les informations d’abonnement hello dans des événements Windows ?</span><span class="sxs-lookup"><span data-stu-id="731a0-127">How can I see hello subscription information in Windows events?</span></span>
<span data-ttu-id="731a0-128">Ajoutez le nom convivial toohello ID d’abonnement hello lors de l’ajout de la source de hello :</span><span class="sxs-lookup"><span data-stu-id="731a0-128">Append hello subscription ID toohello friendly name while adding hello source:</span></span>

    Azlog source add <sourcefriendlyname>.<subscription id> <StorageName> <StorageKey>  
<span data-ttu-id="731a0-129">l’événement Hello XML a hello suivant les métadonnées, y compris l’ID d’abonnement hello :</span><span class="sxs-lookup"><span data-stu-id="731a0-129">hello event XML has hello following metadata, including hello subscription ID:</span></span>

![XML de l’événement][1]

## <a name="error-messages"></a><span data-ttu-id="731a0-131">messages d'erreur</span><span class="sxs-lookup"><span data-stu-id="731a0-131">Error messages</span></span>
### <a name="when-i-run-hello-command-azlog-createazureid-why-do-i-get-hello-following-error"></a><span data-ttu-id="731a0-132">Lors de l’exécution commande hello **azlog createazureid**, je reçois hello l’erreur suivante ?</span><span class="sxs-lookup"><span data-stu-id="731a0-132">When I run hello command **azlog createazureid**, why do I get hello following error?</span></span>
<span data-ttu-id="731a0-133">Error:</span><span class="sxs-lookup"><span data-stu-id="731a0-133">Error:</span></span>

  <span data-ttu-id="731a0-134">*Échec toocreate AAD Application - client 72f988bf-86f1-41af-91ab-2d7cd011db37 - raison = « Interdit » - Message = 'pas de privilèges suffisants de l’opération de toocomplete hello'.*</span><span class="sxs-lookup"><span data-stu-id="731a0-134">*Failed toocreate AAD Application - Tenant 72f988bf-86f1-41af-91ab-2d7cd011db37 - Reason = 'Forbidden' - Message = 'Insufficient privileges toocomplete hello operation.'*</span></span>

<span data-ttu-id="731a0-135">Hello **azlog createazureid** toocreate un principal de service dans tous les locataires hello Azure AD pour les abonnements hello hello connexion Azure a accès à des tentatives de commande.</span><span class="sxs-lookup"><span data-stu-id="731a0-135">hello **azlog createazureid** command attempts toocreate a service principal in all hello Azure AD tenants for hello subscriptions that hello Azure login has access to.</span></span> <span data-ttu-id="731a0-136">Si votre connexion Azure est un utilisateur invité dans ce locataire Azure AD, commande hello échoue avec « opération privilèges insuffisants toocomplete hello. »</span><span class="sxs-lookup"><span data-stu-id="731a0-136">If your Azure login is only a guest user in that Azure AD tenant, hello command fails with "Insufficient privileges toocomplete hello operation."</span></span> <span data-ttu-id="731a0-137">Demandez les locataire hello admin tooadd votre compte en tant qu’utilisateur de client de hello.</span><span class="sxs-lookup"><span data-stu-id="731a0-137">Ask hello tenant admin tooadd your account as a user in hello tenant.</span></span>

### <a name="when-i-run-hello-command-azlog-authorize-why-do-i-get-hello-following-error"></a><span data-ttu-id="731a0-138">Lors de l’exécution commande hello **azlog autoriser**, je reçois hello l’erreur suivante ?</span><span class="sxs-lookup"><span data-stu-id="731a0-138">When I run hello command **azlog authorize**, why do I get hello following error?</span></span>
<span data-ttu-id="731a0-139">Error:</span><span class="sxs-lookup"><span data-stu-id="731a0-139">Error:</span></span>

  <span data-ttu-id="731a0-140">*Avertissement de création d’attribution de rôle - AuthorizationFailed : client de hello janedo@microsoft.com' avec l’objet id 'fe9e03e4-4dad-4328-910f-fd24a9660bd2' autorisation tooperform aucune action n’est « Microsoft.Authorization/roleAssignments/write » sur l’étendue ' / abonnements / 70d 95299-d689-4c 97-b971-0d8ff0000000 ».*</span><span class="sxs-lookup"><span data-stu-id="731a0-140">*Warning creating Role Assignment - AuthorizationFailed: hello client janedo@microsoft.com' with object id 'fe9e03e4-4dad-4328-910f-fd24a9660bd2' does not have authorization tooperform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/70d95299-d689-4c97-b971-0d8ff0000000'.*</span></span>

<span data-ttu-id="731a0-141">Hello **azlog autoriser** commande attribue hello rôle de principal du service du lecteur toohello Azure AD (créée avec **azlog createazureid**) les abonnements toohello fourni.</span><span class="sxs-lookup"><span data-stu-id="731a0-141">hello **azlog authorize** command assigns hello role of reader toohello Azure AD service principal (created with **azlog createazureid**) toohello provided subscriptions.</span></span> <span data-ttu-id="731a0-142">Si hello connexion Azure n’est pas un coadministrateur ou un propriétaire d’abonnement de hello, elle échoue avec un message d’erreur « Échec de l’autorisation ».</span><span class="sxs-lookup"><span data-stu-id="731a0-142">If hello Azure login is not a co-administrator or an owner of hello subscription, it fails with an "Authorization Failed" error message.</span></span> <span data-ttu-id="731a0-143">Azure basé sur le rôle de contrôle d’accès (RBAC) de coadministrateur ou un propriétaire est toocomplete nécessaire à cette action.</span><span class="sxs-lookup"><span data-stu-id="731a0-143">Azure Role-Based Access Control (RBAC) of co-administrator or owner is needed toocomplete this action.</span></span>

## <a name="where-can-i-find-hello-definition-of-hello-properties-in-hello-audit-log"></a><span data-ttu-id="731a0-144">Où puis-je trouver définition hello des propriétés de hello dans le journal d’audit de hello ?</span><span class="sxs-lookup"><span data-stu-id="731a0-144">Where can I find hello definition of hello properties in hello audit log?</span></span>
<span data-ttu-id="731a0-145">Consultez l'article :</span><span class="sxs-lookup"><span data-stu-id="731a0-145">See:</span></span>

* [<span data-ttu-id="731a0-146">Opérations d’audit avec Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="731a0-146">Audit operations with Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-audit.md)
* [<span data-ttu-id="731a0-147">Liste des événements de gestion hello dans un abonnement de hello API REST du moniteur de Azure</span><span class="sxs-lookup"><span data-stu-id="731a0-147">List hello management events in a subscription in hello Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931934.aspx)

## <a name="where-can-i-find-details-on-azure-security-center-alerts"></a><span data-ttu-id="731a0-148">Où puis-je trouver plus d’informations sur les alertes de l’Azure Security Center ?</span><span class="sxs-lookup"><span data-stu-id="731a0-148">Where can I find details on Azure Security Center alerts?</span></span>
<span data-ttu-id="731a0-149">Consultez [toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure](../security-center/security-center-managing-and-responding-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="731a0-149">See [Managing and responding toosecurity alerts in Azure Security Center](../security-center/security-center-managing-and-responding-alerts.md).</span></span>

## <a name="how-can-i-modify-what-is-collected-with-vm-diagnostics"></a><span data-ttu-id="731a0-150">Comment puis-je modifier les données collectées avec les diagnostics de la machine virtuelle ?</span><span class="sxs-lookup"><span data-stu-id="731a0-150">How can I modify what is collected with VM diagnostics?</span></span>
<span data-ttu-id="731a0-151">Pour plus d’informations sur la façon dont tooget, modifier et définir la configuration de Diagnostics Windows Azure hello, consultez [tooenable utiliser PowerShell Diagnostics Azure dans une machine virtuelle exécutant Windows](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="731a0-151">For details on how tooget, modify, and set hello Azure Diagnostics configuration, see [Use PowerShell tooenable Azure Diagnostics in a virtual machine running Windows](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="731a0-152">Hello, l’exemple suivant obtient la configuration des Diagnostics Windows Azure hello :</span><span class="sxs-lookup"><span data-stu-id="731a0-152">hello following example gets hello Azure Diagnostics configuration:</span></span>

    -AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient
    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

    $xmlconfig | Out-File -Encoding utf8 -FilePath "d:\WADConfig.xml"

<span data-ttu-id="731a0-153">Hello, l’exemple suivant modifie la configuration des Diagnostics Windows Azure hello.</span><span class="sxs-lookup"><span data-stu-id="731a0-153">hello following example modifies hello Azure Diagnostics configuration.</span></span> <span data-ttu-id="731a0-154">Dans cette configuration, uniquement l’événement ID 4624 et 4625 d’ID d’événement sont collectés à partir du journal des événements de sécurité hello.</span><span class="sxs-lookup"><span data-stu-id="731a0-154">In this configuration, only event ID 4624 and event ID 4625 are collected from hello security event log.</span></span> <span data-ttu-id="731a0-155">Microsoft Antimalware pour Azure événements sont collectés à partir du journal des événements système hello.</span><span class="sxs-lookup"><span data-stu-id="731a0-155">Microsoft Antimalware for Azure events are collected from hello system event log.</span></span> <span data-ttu-id="731a0-156">Pour plus d’informations sur l’utilisation de hello d’expressions XPath, consultez [consommation d’événements](https://msdn.microsoft.com/library/windows/desktop/dd996910(v=vs.85)).</span><span class="sxs-lookup"><span data-stu-id="731a0-156">For details on hello use of XPath expressions, see [Consuming Events](https://msdn.microsoft.com/library/windows/desktop/dd996910(v=vs.85)).</span></span>

    <WindowsEventLog scheduledTransferPeriod="PT1M">
        <DataSource name="Security!*[System[(EventID=4624 or EventID=4625)]]" />
        <DataSource name="System!*[System[Provider[@Name='Microsoft Antimalware']]]"/>
    </WindowsEventLog>

<span data-ttu-id="731a0-157">Hello exemple suivant définit configuration des Diagnostics Windows Azure hello :</span><span class="sxs-lookup"><span data-stu-id="731a0-157">hello following example sets hello Azure Diagnostics configuration:</span></span>

    $diagnosticsconfig_path = "d:\WADConfig.xml"
    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName log3121 -StorageAccountKey <storage key>

<span data-ttu-id="731a0-158">Une fois que vous apportez des modifications, vérifiez tooensure de compte de stockage hello que hello correct d’événements sont collectés.</span><span class="sxs-lookup"><span data-stu-id="731a0-158">After you make changes, check hello storage account tooensure that hello correct events are collected.</span></span>

<span data-ttu-id="731a0-159">Si vous rencontrez des problèmes pendant l’installation de hello et de configuration, ouvrez un [demande de support](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request).</span><span class="sxs-lookup"><span data-stu-id="731a0-159">If you have any issues during hello installation and configuration, please open a [support request](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request).</span></span> <span data-ttu-id="731a0-160">Sélectionnez **journal intégration** en tant que service hello pour lequel vous demandez la prise en charge.</span><span class="sxs-lookup"><span data-stu-id="731a0-160">Select **Log Integration** as hello service for which you are requesting support.</span></span>

## <a name="can-i-use-azure-log-integration-toointegrate-network-watcher-logs-into-my-siem"></a><span data-ttu-id="731a0-161">Puis-je utiliser des journaux de l’Observateur réseau Azure journal intégration toointegrate dans mon SIEM ?</span><span class="sxs-lookup"><span data-stu-id="731a0-161">Can I use Azure Log Integration toointegrate Network Watcher logs into my SIEM?</span></span>

<span data-ttu-id="731a0-162">Azure Network Watcher génère de grandes quantités d’informations de journalisation.</span><span class="sxs-lookup"><span data-stu-id="731a0-162">Azure Network Watcher generates large quantities of logging information.</span></span> <span data-ttu-id="731a0-163">Ces journaux ne sont pas toobe revient envoyé tooa SIEM.</span><span class="sxs-lookup"><span data-stu-id="731a0-163">These logs are not meant toobe sent tooa SIEM.</span></span> <span data-ttu-id="731a0-164">destination Hello pris en charge uniquement pour les journaux de l’Observateur réseau est un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="731a0-164">hello only supported destination for Network Watcher logs is a storage account.</span></span> <span data-ttu-id="731a0-165">Intégration d’Azure journal ne prend pas en charge la lecture de ces journaux et ce qui les rend disponible tooa SIEM.</span><span class="sxs-lookup"><span data-stu-id="731a0-165">Azure Log Integration does not support reading these logs and making them available tooa SIEM.</span></span>

<!--Image references-->
[1]: ./media/security-azure-log-integration-faq/event-xml.png
