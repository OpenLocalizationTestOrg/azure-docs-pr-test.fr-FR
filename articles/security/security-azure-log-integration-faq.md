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
# <a name="azure-log-integration-faq"></a>Forum aux questions sur l’intégration des journaux Azure
Cet article contient les réponses à certaines questions fréquemment posées sur l’intégration des journaux Azure. 

Intégration d’Azure journal est un service de système d’exploitation Windows que vous pouvez utiliser les journaux bruts toointegrate à partir de vos ressources Azure dans vos systèmes de gestion (SIEM) local sécurité événements et des informations. Cette intégration offre un tableau de bord unifiée pour tous vos actifs, localement ou dans le cloud de hello. pour vous permettre d’agréger, de mettre en corrélation, d’analyser et d’alerter en cas d’événements de sécurité associés à vos applications.

## <a name="is-hello-azure-log-integration-software-free"></a>Est un logiciel d’intégration des journaux Azure de hello libre ?
Oui. Il n’existe aucun frais pour hello logiciel d’intégration des journaux Azure.

## <a name="where-is-azure-log-integration-available"></a>Où l’intégration des journaux Azure est-elle disponible ?

Elle est actuellement disponible dans les versions commerciales d’Azure et dans Azure Government, mais n’est pas disponible en Chine ni en Allemagne.

## <a name="how-can-i-see-hello-storage-accounts-from-which-azure-log-integration-is-pulling-azure-vm-logs"></a>Comment puis-je voir les comptes de stockage hello à partir de laquelle intégration des journaux Azure collecte des journaux de machine virtuelle Azure ?
Exécutez la commande hello **liste des sources azlog**.

## <a name="how-can-i-tell-which-subscription-hello-azure-log-integration-logs-are-from"></a>Comment puis-je savoir quel hello abonnement Azure intégration du journal proviennent de journaux ?

Dans les cas de hello des journaux d’audit qui sont placés dans hello **AzureResourcemanagerJson** répertoires, ID d’abonnement hello est dans le nom du fichier journal hello. Cela vaut également pour les journaux Bonjour **AzureSecurityCenterJson** dossier. Par exemple :

20170407T070805_2768037.0000000023.**1111e5ee-1111-111b-a11e-1e111e1111dc**.json

Les journaux d’audit Azure Active Directory incluent les ID de client hello en tant que partie du nom de hello.

Les journaux de diagnostic sont lus à partir d’un concentrateur d’événements n’incluent pas d’ID d’abonnement hello en tant que partie du nom de hello. Au lieu de cela, ils comprennent le nom convivial de hello spécifié dans le cadre de la création de source de concentrateur d’événements hello hello. 

## <a name="how-can-i-update-hello-proxy-configuration"></a>Comment puis-je mettre à jour la configuration proxy hello ?
Si le paramètre de proxy n’autorise pas directement accès au stockage Azure, ouvrez hello **AZLOG. EXE. CONFIGURATION** fichier **c:\Program Files\Microsoft Azure journal intégration**. Mise à jour Bonjour fichier tooinclude Bonjour **defaultProxy** section avec l’adresse du proxy hello de votre organisation. Une fois la mise à jour de hello est effectuée, arrêter et démarrer le service de hello à l’aide des commandes hello **net stop azlog** et **net démarrer azlog**.

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

## <a name="how-can-i-see-hello-subscription-information-in-windows-events"></a>Comment puis-je voir les informations d’abonnement hello dans des événements Windows ?
Ajoutez le nom convivial toohello ID d’abonnement hello lors de l’ajout de la source de hello :

    Azlog source add <sourcefriendlyname>.<subscription id> <StorageName> <StorageKey>  
l’événement Hello XML a hello suivant les métadonnées, y compris l’ID d’abonnement hello :

![XML de l’événement][1]

## <a name="error-messages"></a>messages d'erreur
### <a name="when-i-run-hello-command-azlog-createazureid-why-do-i-get-hello-following-error"></a>Lors de l’exécution commande hello **azlog createazureid**, je reçois hello l’erreur suivante ?
Error:

  *Échec toocreate AAD Application - client 72f988bf-86f1-41af-91ab-2d7cd011db37 - raison = « Interdit » - Message = 'pas de privilèges suffisants de l’opération de toocomplete hello'.*

Hello **azlog createazureid** toocreate un principal de service dans tous les locataires hello Azure AD pour les abonnements hello hello connexion Azure a accès à des tentatives de commande. Si votre connexion Azure est un utilisateur invité dans ce locataire Azure AD, commande hello échoue avec « opération privilèges insuffisants toocomplete hello. » Demandez les locataire hello admin tooadd votre compte en tant qu’utilisateur de client de hello.

### <a name="when-i-run-hello-command-azlog-authorize-why-do-i-get-hello-following-error"></a>Lors de l’exécution commande hello **azlog autoriser**, je reçois hello l’erreur suivante ?
Error:

  *Avertissement de création d’attribution de rôle - AuthorizationFailed : client de hello janedo@microsoft.com' avec l’objet id 'fe9e03e4-4dad-4328-910f-fd24a9660bd2' autorisation tooperform aucune action n’est « Microsoft.Authorization/roleAssignments/write » sur l’étendue ' / abonnements / 70d 95299-d689-4c 97-b971-0d8ff0000000 ».*

Hello **azlog autoriser** commande attribue hello rôle de principal du service du lecteur toohello Azure AD (créée avec **azlog createazureid**) les abonnements toohello fourni. Si hello connexion Azure n’est pas un coadministrateur ou un propriétaire d’abonnement de hello, elle échoue avec un message d’erreur « Échec de l’autorisation ». Azure basé sur le rôle de contrôle d’accès (RBAC) de coadministrateur ou un propriétaire est toocomplete nécessaire à cette action.

## <a name="where-can-i-find-hello-definition-of-hello-properties-in-hello-audit-log"></a>Où puis-je trouver définition hello des propriétés de hello dans le journal d’audit de hello ?
Consultez l'article :

* [Opérations d’audit avec Azure Resource Manager](../azure-resource-manager/resource-group-audit.md)
* [Liste des événements de gestion hello dans un abonnement de hello API REST du moniteur de Azure](https://msdn.microsoft.com/library/azure/dn931934.aspx)

## <a name="where-can-i-find-details-on-azure-security-center-alerts"></a>Où puis-je trouver plus d’informations sur les alertes de l’Azure Security Center ?
Consultez [toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure](../security-center/security-center-managing-and-responding-alerts.md).

## <a name="how-can-i-modify-what-is-collected-with-vm-diagnostics"></a>Comment puis-je modifier les données collectées avec les diagnostics de la machine virtuelle ?
Pour plus d’informations sur la façon dont tooget, modifier et définir la configuration de Diagnostics Windows Azure hello, consultez [tooenable utiliser PowerShell Diagnostics Azure dans une machine virtuelle exécutant Windows](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Hello, l’exemple suivant obtient la configuration des Diagnostics Windows Azure hello :

    -AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient
    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

    $xmlconfig | Out-File -Encoding utf8 -FilePath "d:\WADConfig.xml"

Hello, l’exemple suivant modifie la configuration des Diagnostics Windows Azure hello. Dans cette configuration, uniquement l’événement ID 4624 et 4625 d’ID d’événement sont collectés à partir du journal des événements de sécurité hello. Microsoft Antimalware pour Azure événements sont collectés à partir du journal des événements système hello. Pour plus d’informations sur l’utilisation de hello d’expressions XPath, consultez [consommation d’événements](https://msdn.microsoft.com/library/windows/desktop/dd996910(v=vs.85)).

    <WindowsEventLog scheduledTransferPeriod="PT1M">
        <DataSource name="Security!*[System[(EventID=4624 or EventID=4625)]]" />
        <DataSource name="System!*[System[Provider[@Name='Microsoft Antimalware']]]"/>
    </WindowsEventLog>

Hello exemple suivant définit configuration des Diagnostics Windows Azure hello :

    $diagnosticsconfig_path = "d:\WADConfig.xml"
    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName log3121 -StorageAccountKey <storage key>

Une fois que vous apportez des modifications, vérifiez tooensure de compte de stockage hello que hello correct d’événements sont collectés.

Si vous rencontrez des problèmes pendant l’installation de hello et de configuration, ouvrez un [demande de support](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request). Sélectionnez **journal intégration** en tant que service hello pour lequel vous demandez la prise en charge.

## <a name="can-i-use-azure-log-integration-toointegrate-network-watcher-logs-into-my-siem"></a>Puis-je utiliser des journaux de l’Observateur réseau Azure journal intégration toointegrate dans mon SIEM ?

Azure Network Watcher génère de grandes quantités d’informations de journalisation. Ces journaux ne sont pas toobe revient envoyé tooa SIEM. destination Hello pris en charge uniquement pour les journaux de l’Observateur réseau est un compte de stockage. Intégration d’Azure journal ne prend pas en charge la lecture de ces journaux et ce qui les rend disponible tooa SIEM.

<!--Image references-->
[1]: ./media/security-azure-log-integration-faq/event-xml.png
