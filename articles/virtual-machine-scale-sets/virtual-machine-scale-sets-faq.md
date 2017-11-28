---
title: "échelle de machines virtuelles aaaAzure définit des questions fréquentes | Documents Microsoft"
description: "Obtenir elles sonttrop des réponses aux questions sur les machines virtuelles identiques."
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/20/2017
ms.author: negat
ms.custom: na
ms.openlocfilehash: 0deb9e2bb79f87f17bbf748397b94dc53070cfbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-scale-sets-faqs"></a><span data-ttu-id="43926-103">FAQ sur les groupes de machines virtuelles identiques Azure</span><span class="sxs-lookup"><span data-stu-id="43926-103">Azure virtual machine scale sets FAQs</span></span>

<span data-ttu-id="43926-104">Obtenez des réponses aux questions sur l’échelle de machines virtuelles d’elles sonttrop définit dans Azure.</span><span class="sxs-lookup"><span data-stu-id="43926-104">Get answers toofrequently asked questions about virtual machine scale sets in Azure.</span></span>

## <a name="autoscale"></a><span data-ttu-id="43926-105">Autoscale</span><span class="sxs-lookup"><span data-stu-id="43926-105">Autoscale</span></span>

### <a name="what-are-best-practices-for-azure-autoscale"></a><span data-ttu-id="43926-106">Quelles sont les meilleures pratiques pour la mise à l’échelle automatique d’Azure ?</span><span class="sxs-lookup"><span data-stu-id="43926-106">What are best practices for Azure Autoscale?</span></span>

<span data-ttu-id="43926-107">Pour connaître les meilleures pratiques pour la mise à l’échelle automatique, consultez [Meilleures pratiques pour la mise à l’échelle automatique des machines virtuelles](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-best-practices).</span><span class="sxs-lookup"><span data-stu-id="43926-107">For best practices for Autoscale, see [Best practices for autoscaling virtual machines](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-best-practices).</span></span>

### <a name="where-do-i-find-metric-names-for-autoscaling-that-uses-host-based-metrics"></a><span data-ttu-id="43926-108">Où trouver les noms des métriques pour la mise à l’échelle automatique utilisant des métriques basées sur les hôtes ?</span><span class="sxs-lookup"><span data-stu-id="43926-108">Where do I find metric names for autoscaling that uses host-based metrics?</span></span>

<span data-ttu-id="43926-109">Pour obtenir les noms des métriques pour la mise à l’échelle automatique utilisant des métriques basées sur les hôtes, consultez [Métriques prises en charge avec Azure Monitor](https://azure.microsoft.com/documentation/articles/monitoring-supported-metrics/).</span><span class="sxs-lookup"><span data-stu-id="43926-109">For metric names for autoscaling that uses host-based metrics, see [Supported metrics with Azure Monitor](https://azure.microsoft.com/documentation/articles/monitoring-supported-metrics/).</span></span>

### <a name="are-there-any-examples-of-autoscaling-based-on-an-azure-service-bus-topic-and-queue-length"></a><span data-ttu-id="43926-110">Existe-t-il des exemples de mise à l’échelle automatique basée sur une rubrique Azure Service Bus et une longueur de file d’attente ?</span><span class="sxs-lookup"><span data-stu-id="43926-110">Are there any examples of autoscaling based on an Azure Service Bus topic and queue length?</span></span>

<span data-ttu-id="43926-111">Oui.</span><span class="sxs-lookup"><span data-stu-id="43926-111">Yes.</span></span> <span data-ttu-id="43926-112">Pour obtenir des exemples de mise à l’échelle automatique basée sur une rubrique Azure Service Bus et une longueur de file d’attente, consultez [Métriques courantes pour la mise à l’échelle automatique d’Azure Monitor](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/).</span><span class="sxs-lookup"><span data-stu-id="43926-112">For examples of autoscaling based on an Azure Service Bus topic and queue length, see [Azure Monitor autoscaling common metrics](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/).</span></span>

<span data-ttu-id="43926-113">Pour une file d’attente Service Bus, utilisez hello suivant JSON :</span><span class="sxs-lookup"><span data-stu-id="43926-113">For a Service Bus queue, use hello following JSON:</span></span>

```json
"metricName": "MessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue"
```

<span data-ttu-id="43926-114">Pour une file d’attente de stockage, utilisez hello suivant JSON :</span><span class="sxs-lookup"><span data-stu-id="43926-114">For a storage queue, use hello following JSON:</span></span>

```json
"metricName": "ApproximateMessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ClassicStorage/storageAccounts/mystorage/services/queue/queues/mystoragequeue"
```

<span data-ttu-id="43926-115">Remplacez les exemples de valeurs par les URI (Uniform Resource Identifiers) de votre ressource.</span><span class="sxs-lookup"><span data-stu-id="43926-115">Replace example values with your resource Uniform Resource Identifiers (URIs).</span></span>


### <a name="should-i-autoscale-by-using-host-based-metrics-or-a-diagnostics-extension"></a><span data-ttu-id="43926-116">Dois-je utiliser la mise à l’échelle automatique avec des métriques basées sur les hôtes ou une extension de diagnostics ?</span><span class="sxs-lookup"><span data-stu-id="43926-116">Should I autoscale by using host-based metrics or a diagnostics extension?</span></span>

<span data-ttu-id="43926-117">Vous pouvez créer un paramètre de mise à l’échelle sur un métriques de machine virtuelle toouse au niveau hôte ou les métriques de basé sur le système d’exploitation invité.</span><span class="sxs-lookup"><span data-stu-id="43926-117">You can create an autoscale setting on a VM toouse host-level metrics or guest OS-based metrics.</span></span>

<span data-ttu-id="43926-118">Pour obtenir la liste des métriques prises en charge, consultez [Métriques courantes pour la mise à l’échelle automatique d’Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-common-metrics).</span><span class="sxs-lookup"><span data-stu-id="43926-118">For a list of supported metrics, see [Azure Monitor autoscaling common metrics](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-common-metrics).</span></span> 

<span data-ttu-id="43926-119">Pour obtenir un exemple complet pour les groupes de machines virtuelles identiques, consultez [Configuration avancée de la mise à l’échelle automatique à l’aide de modèles Resource Manager pour les groupes de machines virtuelles identiques](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-advanced-autoscale-virtual-machine-scale-sets).</span><span class="sxs-lookup"><span data-stu-id="43926-119">For a full sample for virtual machine scale sets, see [Advanced autoscale configuration by using Resource Manager templates for virtual machine scale sets](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-advanced-autoscale-virtual-machine-scale-sets).</span></span> 

<span data-ttu-id="43926-120">exemple Hello utilise la métrique de l’UC au niveau hôte hello et une métrique de nombre de messages.</span><span class="sxs-lookup"><span data-stu-id="43926-120">hello sample uses hello host-level CPU metric and a message count metric.</span></span>



### <a name="how-do-i-set-alert-rules-on-a-virtual-machine-scale-set"></a><span data-ttu-id="43926-121">Comment définir des règles d’alerte sur un groupe de machines virtuelles identiques ?</span><span class="sxs-lookup"><span data-stu-id="43926-121">How do I set alert rules on a virtual machine scale set?</span></span>

<span data-ttu-id="43926-122">Vous pouvez créer des alertes sur des métriques pour les groupes de machines virtuelles identiques via PowerShell ou l’interface CLI Azure.</span><span class="sxs-lookup"><span data-stu-id="43926-122">You can create alerts on metrics for virtual machine scale sets via PowerShell or Azure CLI.</span></span> <span data-ttu-id="43926-123">Pour plus d’informations, consultez [Exemples de démarrage rapide Azure Monitor PowerShell](https://azure.microsoft.com/documentation/articles/insights-powershell-samples/#create-alert-rules) et [Exemples de démarrage CLI interplateforme Azure Monitor](https://azure.microsoft.com/documentation/articles/insights-cli-samples/#work-with-alerts).</span><span class="sxs-lookup"><span data-stu-id="43926-123">For more information, see [Azure Monitor PowerShell quick start samples](https://azure.microsoft.com/documentation/articles/insights-powershell-samples/#create-alert-rules) and [Azure Monitor cross-platform CLI quick start samples](https://azure.microsoft.com/documentation/articles/insights-cli-samples/#work-with-alerts).</span></span>

<span data-ttu-id="43926-124">Hello TargetResourceId d’ensemble d’échelle de machine virtuelle hello ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="43926-124">hello TargetResourceId of hello virtual machine scale set looks like this:</span></span> 

<span data-ttu-id="43926-125">/subscriptions/yoursubscriptionid/resourceGroups/yourresourcegroup/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmssname</span><span class="sxs-lookup"><span data-stu-id="43926-125">/subscriptions/yoursubscriptionid/resourceGroups/yourresourcegroup/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmssname</span></span>

<span data-ttu-id="43926-126">Vous pouvez choisir n’importe quel compteur de performances de machine virtuelle comme tooset de métrique hello une alerte.</span><span class="sxs-lookup"><span data-stu-id="43926-126">You can choose any VM performance counter as hello metric tooset an alert for.</span></span> <span data-ttu-id="43926-127">Pour plus d’informations, consultez [métriques du système d’exploitation invité pour les machines virtuelles Windows basée sur le Gestionnaire de ressources](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-resource-manager-based-windows-vms) et [métriques du système d’exploitation invité pour les machines virtuelles Linux](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-linux-vms) Bonjour [mesures courantes de l’échelle automatique de moniteur Azure](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/)l’article.</span><span class="sxs-lookup"><span data-stu-id="43926-127">For more information, see [Guest OS metrics for Resource Manager-based Windows VMs](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-resource-manager-based-windows-vms) and [Guest OS metrics for Linux VMs](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-linux-vms) in hello [Azure Monitor autoscaling common metrics](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/) article.</span></span>

### <a name="how-do-i-set-up-autoscale-on-a-virtual-machine-scale-set-by-using-powershell"></a><span data-ttu-id="43926-128">Comment configurer la mise à l’échelle automatique sur un groupe de machines virtuelles identiques à l’aide de PowerShell ?</span><span class="sxs-lookup"><span data-stu-id="43926-128">How do I set up autoscale on a virtual machine scale set by using PowerShell?</span></span>

<span data-ttu-id="43926-129">tooset de mise à l’échelle sur une échelle de machine virtuelle définie à l’aide de PowerShell, voir hello blog [comment tooadd tooan de mise à l’échelle mise à l’échelle de machine virtuelle Azure définie](https://msftstack.wordpress.com/2017/03/05/how-to-add-autoscale-to-an-azure-vm-scale-set/).</span><span class="sxs-lookup"><span data-stu-id="43926-129">tooset up autoscale on a virtual machine scale set by using PowerShell, see hello blog post [How tooadd autoscale tooan Azure virtual machine scale set](https://msftstack.wordpress.com/2017/03/05/how-to-add-autoscale-to-an-azure-vm-scale-set/).</span></span>




## <a name="certificates"></a><span data-ttu-id="43926-130">Certificats</span><span class="sxs-lookup"><span data-stu-id="43926-130">Certificates</span></span>

### <a name="how-do-i-securely-ship-a-certificate-toohello-vm-how-do-i-provision-a-virtual-machine-scale-set-toorun-a-website-where-hello-ssl-for-hello-website-is-shipped-securely-from-a-certificate-configuration-hello-common-certificate-rotation-operation-would-be-almost-hello-same-as-a-configuration-update-operation-do-you-have-an-example-of-how-toodo-this"></a><span data-ttu-id="43926-131">Comment expédier en toute sécurité un toohello certificat machine virtuelle ?</span><span class="sxs-lookup"><span data-stu-id="43926-131">How do I securely ship a certificate toohello VM?</span></span> <span data-ttu-id="43926-132">Comment pour configurer un toorun de jeu de machine virtuelle mise à l’échelle un site Web où hello SSL pour le site Web de hello est envoyée en toute sécurité à partir d’une configuration de certificat ?</span><span class="sxs-lookup"><span data-stu-id="43926-132">How do I provision a virtual machine scale set toorun a website where hello SSL for hello website is shipped securely from a certificate configuration?</span></span> <span data-ttu-id="43926-133">(opération de rotation du certificat commun hello serait être presque hello identique à une opération de mise à jour de configuration.) Disposez-vous d’un exemple de procédure toodo cela ?</span><span class="sxs-lookup"><span data-stu-id="43926-133">(hello common certificate rotation operation would be almost hello same as a configuration update operation.) Do you have an example of how toodo this?</span></span> 

<span data-ttu-id="43926-134">toosecurely livrer un toohello certificat machine virtuelle, vous pouvez installer un certificat client directement dans un magasin de certificats Windows coffre du client hello de clés.</span><span class="sxs-lookup"><span data-stu-id="43926-134">toosecurely ship a certificate toohello VM, you can install a customer certificate directly into a Windows certificate store from hello customer's key vault.</span></span>

<span data-ttu-id="43926-135">Utilisez hello suivant JSON :</span><span class="sxs-lookup"><span data-stu-id="43926-135">Use hello following JSON:</span></span>

```json
"secrets": [
    {
        "sourceVault": {
            "id": "/subscriptions/{subscriptionid}/resourceGroups/myrg1/providers/Microsoft.KeyVault/vaults/mykeyvault1"
        },
        "vaultCertificates": [
            {
                "certificateUrl": "https://mykeyvault1.vault.azure.net/secrets/{secretname}/{secret-version}",
                "certificateStore": "certificateStoreName"
            }
        ]
    }
]
```

<span data-ttu-id="43926-136">code de Hello prend en charge Windows et Linux.</span><span class="sxs-lookup"><span data-stu-id="43926-136">hello code supports Windows and Linux.</span></span>

<span data-ttu-id="43926-137">Pour plus d’informations, consultez [Création ou mise à jour d’un groupe de machines virtuelles identiques](https://msdn.microsoft.com/library/mt589035.aspx).</span><span class="sxs-lookup"><span data-stu-id="43926-137">For more information, see [Create or update a virtual machine scale set](https://msdn.microsoft.com/library/mt589035.aspx).</span></span>


### <a name="example-of-self-signed-certificate"></a><span data-ttu-id="43926-138">Exemple de certificat auto-signé</span><span class="sxs-lookup"><span data-stu-id="43926-138">Example of Self-signed certificate</span></span>

1.  <span data-ttu-id="43926-139">Créez un certificat auto-signé dans un coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="43926-139">Create a self-signed certificate in a key vault.</span></span>

    <span data-ttu-id="43926-140">Utilisez hello suivant de commandes PowerShell :</span><span class="sxs-lookup"><span data-stu-id="43926-140">Use hello following PowerShell commands:</span></span>

    ```powershell
    Import-Module "C:\Users\mikhegn\Downloads\Service-Fabric-master\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

    Login-AzureRmAccount

    Invoke-AddCertToKeyVault -SubscriptionId <Your SubID> -ResourceGroupName KeyVault -Location westus -VaultName MikhegnVault -CertificateName VMSSCert -Password VmssCert -CreateSelfSignedCertificate -DnsName vmss.mikhegn.azure.com -OutputPath c:\users\mikhegn\desktop\
    ```

    <span data-ttu-id="43926-141">Ceci permet de commande vous hello entrée pour le modèle de gestionnaire de ressources Azure hello.</span><span class="sxs-lookup"><span data-stu-id="43926-141">This command gives you hello input for hello Azure Resource Manager template.</span></span>

    <span data-ttu-id="43926-142">Pour obtenir un exemple de toocreate un certificat auto-signé dans un coffre de clés, voir [scénarios de sécurité du cluster Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/).</span><span class="sxs-lookup"><span data-stu-id="43926-142">For an example of how toocreate a self-signed certificate in a key vault, see [Service Fabric cluster security scenarios](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/).</span></span>

2.  <span data-ttu-id="43926-143">Modifier le modèle de gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="43926-143">Change hello Resource Manager template.</span></span>

    <span data-ttu-id="43926-144">Ajouter cette propriété trop**virtualMachineProfile**, définie des ressources dans le cadre de hello échelle de machines virtuelles :</span><span class="sxs-lookup"><span data-stu-id="43926-144">Add this property too**virtualMachineProfile**, as part of hello virtual machine scale set resource:</span></span>

    ```json 
    "osProfile": {
        "computerNamePrefix": "[variables('namingInfix')]",
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]",
        "secrets": [
            {
                "sourceVault": {
                    "id": "[resourceId('KeyVault', 'Microsoft.KeyVault/vaults', 'MikhegnVault')]"
                },
                "vaultCertificates": [
                    {
                        "certificateUrl": "https://mikhegnvault.vault.azure.net:443/secrets/VMSSCert/20709ca8faee4abb84bc6f4611b088a4",
                        "certificateStore": "My"
                    }
                ]
            }
        ]
    }
    ```
  

### <a name="can-i-specify-an-ssh-key-pair-toouse-for-ssh-authentication-with-a-linux-virtual-machine-scale-set-from-a-resource-manager-template"></a><span data-ttu-id="43926-145">Puis-je spécifier une toouse de paire de clés SSH pour l’authentification SSH avec une échelle de machine virtuelle Linux définir à partir d’un modèle de gestionnaire de ressources ?</span><span class="sxs-lookup"><span data-stu-id="43926-145">Can I specify an SSH key pair toouse for SSH authentication with a Linux virtual machine scale set from a Resource Manager template?</span></span>  

<span data-ttu-id="43926-146">Oui.</span><span class="sxs-lookup"><span data-stu-id="43926-146">Yes.</span></span> <span data-ttu-id="43926-147">Hello API REST pour **osProfile** est l’API REST de machine virtuelle standard toohello similaire.</span><span class="sxs-lookup"><span data-stu-id="43926-147">hello REST API for **osProfile** is similar toohello standard VM REST API.</span></span> 

<span data-ttu-id="43926-148">Incluez **osProfile** dans votre modèle :</span><span class="sxs-lookup"><span data-stu-id="43926-148">Include **osProfile** in your template:</span></span>

```json 
"osProfile": {
    "computerName": "[variables('vmName')]",
    "adminUsername": "[parameters('adminUserName')]",
    "linuxConfiguration": {
        "disablePasswordAuthentication": "true",
        "ssh": {
            "publicKeys": [
                {
                    "path": "[variables('sshKeyPath')]",
                    "keyData": "[parameters('sshKeyData')]"
                }
            ]
        }
    }
}
```
 
<span data-ttu-id="43926-149">Ce bloc JSON est utilisé dans [modèle de démarrage rapide de hello 101-vm-sshkey GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="43926-149">This JSON block is used in [hello 101-vm-sshkey GitHub quick start template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span></span>
 
<span data-ttu-id="43926-150">Hello profil de système d’exploitation est également utilisé dans [hello grelayhost.json GitHub rapide démarrer modèle](https://github.com/ExchMaster/gadgetron/blob/master/Gadgetron/Templates/grelayhost.json).</span><span class="sxs-lookup"><span data-stu-id="43926-150">hello OS profile also is used in [hello grelayhost.json GitHub quick start template](https://github.com/ExchMaster/gadgetron/blob/master/Gadgetron/Templates/grelayhost.json).</span></span>

<span data-ttu-id="43926-151">Pour plus d’informations, consultez [Création ou mise à jour d’un groupe de machines virtuelles identiques](https://msdn.microsoft.com/library/azure/mt589035.aspx#linuxconfiguration).</span><span class="sxs-lookup"><span data-stu-id="43926-151">For more information, see [Create or update a virtual machine scale set](https://msdn.microsoft.com/library/azure/mt589035.aspx#linuxconfiguration).</span></span>
  

### <a name="how-do-i-remove-deprecated-certificates"></a><span data-ttu-id="43926-152">Comment supprimer des certificats obsolètes ?</span><span class="sxs-lookup"><span data-stu-id="43926-152">How do I remove deprecated certificates?</span></span> 

<span data-ttu-id="43926-153">tooremove déconseillée certificats, remove hello ancien certificat à partir de la liste de certificats de coffre hello.</span><span class="sxs-lookup"><span data-stu-id="43926-153">tooremove deprecated certificates, remove hello old certificate from hello vault certificates list.</span></span> <span data-ttu-id="43926-154">Conservez tous les certificats hello que vous souhaitez tooremain sur votre ordinateur dans la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="43926-154">Leave all hello certificates that you want tooremain on your computer in hello list.</span></span> <span data-ttu-id="43926-155">Cela ne supprime pas de certificat de hello de toutes vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="43926-155">This does not remove hello certificate from all your VMs.</span></span> <span data-ttu-id="43926-156">Aussi, il n’ajoute pas de hello certificat toonew les ordinateurs virtuels qui sont créés dans l’ensemble d’échelle de machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="43926-156">It also does not add hello certificate toonew VMs that are created in hello virtual machine scale set.</span></span> 

<span data-ttu-id="43926-157">certificat de hello tooremove à partir de machines virtuelles existantes, écrire un script personnalisé pour extension toomanually supprimer hello des certificats à partir de votre magasin de certificats.</span><span class="sxs-lookup"><span data-stu-id="43926-157">tooremove hello certificate from existing VMs, write a custom script extension toomanually remove hello certificates from your certificate store.</span></span>
 
### <a name="how-do-i-inject-an-existing-ssh-public-key-into-hello-virtual-machine-scale-set-ssh-layer-during-provisioning-i-want-toostore-hello-ssh-public-key-values-in-azure-key-vault-and-then-use-them-in-my-resource-manager-template"></a><span data-ttu-id="43926-158">Comment injecter une clé publique SSH existante dans hello machine virtuelle mise à l’échelle ensemble SSH couche lors de la configuration ?</span><span class="sxs-lookup"><span data-stu-id="43926-158">How do I inject an existing SSH public key into hello virtual machine scale set SSH layer during provisioning?</span></span> <span data-ttu-id="43926-159">J’ai choix toostore hello SSH valeurs de clé publique dans le coffre de clés Azure, puis les utiliser dans mon modèle de gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="43926-159">I want toostore hello SSH public key values in Azure Key Vault, and then use them in my Resource Manager template.</span></span>

<span data-ttu-id="43926-160">Si vous fournissez uniquement avec une clé SSH publique hello machines virtuelles, vous n’avez pas besoin tooput les clés publiques hello dans le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="43926-160">If you are providing hello VMs only with a public SSH key, you don't need tooput hello public keys in Key Vault.</span></span> <span data-ttu-id="43926-161">Les clés publiques ne sont pas secrètes.</span><span class="sxs-lookup"><span data-stu-id="43926-161">Public keys are not secret.</span></span>
 
<span data-ttu-id="43926-162">Vous pouvez fournir les clés publiques SSH en texte brut lorsque vous créez une machine virtuelle Linux :</span><span class="sxs-lookup"><span data-stu-id="43926-162">You can provide SSH public keys in plain text when you create a Linux VM:</span></span>

```json
"linuxConfiguration": {
    "ssh": {
        "publicKeys": [
            {
                "path": "path",
                "keyData": "publickey"
            }
        ]
    }
```
 
<span data-ttu-id="43926-163">nom d’élément linuxConfiguration</span><span class="sxs-lookup"><span data-stu-id="43926-163">linuxConfiguration element name</span></span> | <span data-ttu-id="43926-164">Requis</span><span class="sxs-lookup"><span data-stu-id="43926-164">Required</span></span> | <span data-ttu-id="43926-165">Type</span><span class="sxs-lookup"><span data-stu-id="43926-165">Type</span></span> | <span data-ttu-id="43926-166">Description</span><span class="sxs-lookup"><span data-stu-id="43926-166">Description</span></span>
--- | --- | --- | --- |  ---
<span data-ttu-id="43926-167">ssh</span><span class="sxs-lookup"><span data-stu-id="43926-167">ssh</span></span> | <span data-ttu-id="43926-168">Non</span><span class="sxs-lookup"><span data-stu-id="43926-168">No</span></span> | <span data-ttu-id="43926-169">Collection</span><span class="sxs-lookup"><span data-stu-id="43926-169">Collection</span></span> | <span data-ttu-id="43926-170">Spécifie la configuration de clé SSH hello pour un système d’exploitation Linux</span><span class="sxs-lookup"><span data-stu-id="43926-170">Specifies hello SSH key configuration for a Linux OS</span></span>
<span data-ttu-id="43926-171">path</span><span class="sxs-lookup"><span data-stu-id="43926-171">path</span></span> | <span data-ttu-id="43926-172">Oui</span><span class="sxs-lookup"><span data-stu-id="43926-172">Yes</span></span> | <span data-ttu-id="43926-173">String</span><span class="sxs-lookup"><span data-stu-id="43926-173">String</span></span> | <span data-ttu-id="43926-174">Spécifie le chemin d’accès du fichier hello Linux où les clés SSH hello ou un certificat doit être situé</span><span class="sxs-lookup"><span data-stu-id="43926-174">Specifies hello Linux file path where hello SSH keys or certificate should be located</span></span>
<span data-ttu-id="43926-175">keyData</span><span class="sxs-lookup"><span data-stu-id="43926-175">keyData</span></span> | <span data-ttu-id="43926-176">Oui</span><span class="sxs-lookup"><span data-stu-id="43926-176">Yes</span></span> | <span data-ttu-id="43926-177">String</span><span class="sxs-lookup"><span data-stu-id="43926-177">String</span></span> | <span data-ttu-id="43926-178">Spécifie une clé publique SSH encodée en base64</span><span class="sxs-lookup"><span data-stu-id="43926-178">Specifies a base64-encoded SSH public key</span></span>

<span data-ttu-id="43926-179">Pour obtenir un exemple, consultez [modèle de démarrage rapide de hello 101-vm-sshkey GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="43926-179">For an example, see [hello 101-vm-sshkey GitHub quick start template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span></span>

 
### <a name="when-i-run-update-azurermvmss-after-adding-more-than-one-certificate-from-hello-same-key-vault-i-see-hello-following-message"></a><span data-ttu-id="43926-180">Lors de l’exécution `Update-AzureRmVmss` après l’ajout de plusieurs certificats à partir de hello même clé de coffre, voir hello message suivant :</span><span class="sxs-lookup"><span data-stu-id="43926-180">When I run `Update-AzureRmVmss` after adding more than one certificate from hello same key vault, I see hello following message:</span></span>
 
><span data-ttu-id="43926-181">Update-AzureRmVmss : List secret (Afficher la liste des secrets) contient des instances répétées de /subscriptions/<my-subscription-id>/resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev, ce qui n’est pas autorisé.</span><span class="sxs-lookup"><span data-stu-id="43926-181">Update-AzureRmVmss: List secret contains repeated instances of /subscriptions/<my-subscription-id>/resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev, which is disallowed.</span></span>
 
<span data-ttu-id="43926-182">Cela peut se produire si vous essayez de toore-ajouter hello même coffre au lieu d’utiliser un nouveau certificat de coffre pour le coffre source existant hello.</span><span class="sxs-lookup"><span data-stu-id="43926-182">This can happen if you try toore-add hello same vault instead of using a new vault certificate for hello existing source vault.</span></span> <span data-ttu-id="43926-183">Hello `Add-AzureRmVmssSecret` commande ne fonctionne pas correctement si vous ajoutez des clés secrètes supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="43926-183">hello `Add-AzureRmVmssSecret` command does not work correctly if you are adding additional secrets.</span></span>
 
<span data-ttu-id="43926-184">tooadd plus secrets à partir de hello même coffre de clés, de mise à jour hello $vmss.properties.osProfile.secrets[0].vaultCertificates liste.</span><span class="sxs-lookup"><span data-stu-id="43926-184">tooadd more secrets from hello same key vault, update hello $vmss.properties.osProfile.secrets[0].vaultCertificates list.</span></span>
 
<span data-ttu-id="43926-185">Pour hello prévu la structure d’entrée, consultez [créer ou mettre à jour un ordinateur virtuel défini](https://msdn.microsoft.com/library/azure/mt589035.aspx).</span><span class="sxs-lookup"><span data-stu-id="43926-185">For hello expected input structure, see [Create or update a virtual machine set](https://msdn.microsoft.com/library/azure/mt589035.aspx).</span></span>
 
<span data-ttu-id="43926-186">Trouver secret de hello dans l’objet de jeu hello machine virtuelle mise à l’échelle qui se trouve dans le coffre de clés hello.</span><span class="sxs-lookup"><span data-stu-id="43926-186">Find hello secret in hello virtual machine scale set object that is in hello key vault.</span></span> <span data-ttu-id="43926-187">Ajoutez ensuite votre liste de toohello de référence (hello URL et le nom du magasin des secrets hello) de certificat associé au coffre de hello.</span><span class="sxs-lookup"><span data-stu-id="43926-187">Then, add your certificate reference (hello URL and hello secret store name) toohello list associated with hello vault.</span></span>

> [!NOTE] 
> <span data-ttu-id="43926-188">Actuellement, vous ne peut pas supprimer les certificats d’ordinateurs virtuels à l’aide de hello machine virtuelle mise à l’échelle ensemble API.</span><span class="sxs-lookup"><span data-stu-id="43926-188">Currently, you cannot remove certificates from VMs by using hello virtual machine scale set API.</span></span>
>

<span data-ttu-id="43926-189">Nouvelles machines virtuelles ne possèdent pas de certificat d’ancien hello.</span><span class="sxs-lookup"><span data-stu-id="43926-189">New VMs will not have hello old certificate.</span></span> <span data-ttu-id="43926-190">Toutefois, les ordinateurs virtuels qui ont des certificats de hello et qui sont déjà déployé aura ancien certificat de hello.</span><span class="sxs-lookup"><span data-stu-id="43926-190">However, VMs that have hello certificate and which are already deployed will have hello old certificate.</span></span>
 
### <a name="can-i-push-certificates-toohello-virtual-machine-scale-set-without-providing-hello-password-when-hello-certificate-is-in-hello-secret-store"></a><span data-ttu-id="43926-191">Puis-je push échelle de machines virtuelles toohello certificats défini sans fournir de mot de passe hello lorsque hello certificat dans le magasin des secrets hello ?</span><span class="sxs-lookup"><span data-stu-id="43926-191">Can I push certificates toohello virtual machine scale set without providing hello password, when hello certificate is in hello secret store?</span></span>

<span data-ttu-id="43926-192">Vous n’avez pas besoin de mots de passe toohard-code dans les scripts.</span><span class="sxs-lookup"><span data-stu-id="43926-192">You do not need toohard-code passwords in scripts.</span></span> <span data-ttu-id="43926-193">Vous pouvez récupérer de manière dynamique les mots de passe avec des autorisations hello vous utilisez le script de déploiement toorun hello.</span><span class="sxs-lookup"><span data-stu-id="43926-193">You can dynamically retrieve passwords with hello permissions you use toorun hello deployment script.</span></span> <span data-ttu-id="43926-194">Si vous avez un script qui se déplace d’un certificat à partir du coffre de clés de magasin des secrets hello, hello magasin des secrets `get certificate` commande génère également un mot de passe hello du fichier .pfx de hello.</span><span class="sxs-lookup"><span data-stu-id="43926-194">If you have a script that moves a certificate from hello secret store key vault, hello secret store `get certificate` command also outputs hello password of hello .pfx file.</span></span>
 
### <a name="how-does-hello-secrets-property-of-virtualmachineprofileosprofile-for-a-virtual-machine-scale-set-work-why-do-i-need-hello-sourcevault-value-when-i-have-toospecify-hello-absolute-uri-for-a-certificate-by-using-hello-certificateurl-property"></a><span data-ttu-id="43926-195">Comment la propriété Secrets hello virtualMachineProfile.osProfile pour une échelle de machine virtuelle définie travail ?</span><span class="sxs-lookup"><span data-stu-id="43926-195">How does hello Secrets property of virtualMachineProfile.osProfile for a virtual machine scale set work?</span></span> <span data-ttu-id="43926-196">Pourquoi dois-je valeur sourceVault de hello lorsque j’ai toospecify hello URI absolu d’un certificat à l’aide hello certificateUrl propriété ?</span><span class="sxs-lookup"><span data-stu-id="43926-196">Why do I need hello sourceVault value when I have toospecify hello absolute URI for a certificate by using hello certificateUrl property?</span></span> 

<span data-ttu-id="43926-197">Une référence de certificat Windows Remote Management (WinRM) doit être présente dans hello propriété Secrets de hello profil de système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="43926-197">A Windows Remote Management (WinRM) certificate reference must be present in hello Secrets property of hello OS profile.</span></span> 

<span data-ttu-id="43926-198">Hello indiquant le coffre source hello vise stratégies de liste (ACL) du contrôle d’accès tooenforce qui existent dans le modèle de Service Cloud Azure d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="43926-198">hello purpose of indicating hello source vault is tooenforce access control list (ACL) policies that exist in a user's Azure Cloud Service model.</span></span> <span data-ttu-id="43926-199">Si le coffre source hello n’est pas spécifié, les utilisateurs ne disposant pas d’autorisations toodeploy ou access secrets tooa coffre de clés est en mesure de toothrough un fournisseur de ressources de calcul (CRP).</span><span class="sxs-lookup"><span data-stu-id="43926-199">If hello source vault isn't specified, users who do not have permissions toodeploy or access secrets tooa key vault would be able toothrough a Compute Resource Provider (CRP).</span></span> <span data-ttu-id="43926-200">Les listes ACL existent même pour les ressources qui n’existent pas.</span><span class="sxs-lookup"><span data-stu-id="43926-200">ACLs exist even for resources that do not exist.</span></span>

<span data-ttu-id="43926-201">Si vous fournissez un ID de coffre incorrect de la source, mais une URL valide de coffre de clés, une erreur est signalée lorsque vous interrogez les opération hello.</span><span class="sxs-lookup"><span data-stu-id="43926-201">If you provide an incorrect source vault ID but a valid key vault URL, an error is reported when you poll hello operation.</span></span>
 
### <a name="if-i-add-secrets-tooan-existing-virtual-machine-scale-set-are-hello-secrets-injected-into-existing-vms-or-only-into-new-ones"></a><span data-ttu-id="43926-202">Si j’ajoute tooan secrets existant de machines virtuelles identiques, les secrets hello sont injectées dans des machines virtuelles existantes, ou uniquement dans d’autres ?</span><span class="sxs-lookup"><span data-stu-id="43926-202">If I add secrets tooan existing virtual machine scale set, are hello secrets injected into existing VMs, or only into new ones?</span></span> 

<span data-ttu-id="43926-203">Les certificats sont ajoutés tooall vos machines virtuelles, même préexistant ceux.</span><span class="sxs-lookup"><span data-stu-id="43926-203">Certificates are added tooall your VMs, even preexisting ones.</span></span> <span data-ttu-id="43926-204">Si votre échelle de machines virtuelles upgradePolicy propriété la valeur est défini trop**manuelle**, hello ajouté certificat toohello machine virtuelle lorsque vous effectuez une mise à jour manuelle sur hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="43926-204">If your virtual machine scale set upgradePolicy property is set too**manual**, hello certificate is added toohello VM when you perform a manual update on hello VM.</span></span>
 
### <a name="where-do-i-put-certificates-for-linux-vms"></a><span data-ttu-id="43926-205">Où dois-je placer les certificats pour les machines virtuelles Linux ?</span><span class="sxs-lookup"><span data-stu-id="43926-205">Where do I put certificates for Linux VMs?</span></span>

<span data-ttu-id="43926-206">toolearn toodeploy des certificats pour les ordinateurs virtuels Linux, voir [tooVMs de certificats à partir d’un coffre de clés gérée par le client de déployer](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/).</span><span class="sxs-lookup"><span data-stu-id="43926-206">toolearn how toodeploy certificates for Linux VMs, see [Deploy certificates tooVMs from a customer-managed key vault](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/).</span></span>
  
### <a name="how-do-i-add-a-new-vault-certificate-tooa-new-certificate-object"></a><span data-ttu-id="43926-207">Comment ajouter un nouveau coffre certificat tooa nouvel objet de certificat ?</span><span class="sxs-lookup"><span data-stu-id="43926-207">How do I add a new vault certificate tooa new certificate object?</span></span>

<span data-ttu-id="43926-208">tooadd un secret coffre certificat tooan existant, consultez hello l’exemple PowerShell suivant.</span><span class="sxs-lookup"><span data-stu-id="43926-208">tooadd a vault certificate tooan existing secret, see hello following PowerShell example.</span></span> <span data-ttu-id="43926-209">Utilisez un seul objet secret.</span><span class="sxs-lookup"><span data-stu-id="43926-209">Use only one secret object.</span></span>
 
```powershell
$newVaultCertificate = New-AzureRmVmssVaultCertificateConfig -CertificateStore MY -CertificateUrl https://sansunallapps1.vault.azure.net:443/secrets/dg-private-enc/55fa0332edc44a84ad655298905f1809
 
$vmss.VirtualMachineProfile.OsProfile.Secrets[0].VaultCertificates.Add($newVaultCertificate)
 
Update-AzureRmVmss -VirtualMachineScaleSet $vmss -ResourceGroup $rg -Name $vmssName
```
 
### <a name="what-happens-toocertificates-if-you-reimage-a-vm"></a><span data-ttu-id="43926-210">Que passe-t-il toocertificates si vous réinitialisez un ordinateur virtuel ?</span><span class="sxs-lookup"><span data-stu-id="43926-210">What happens toocertificates if you reimage a VM?</span></span>

<span data-ttu-id="43926-211">Si vous réinitialisez une machine virtuelle, les certificats sont supprimés.</span><span class="sxs-lookup"><span data-stu-id="43926-211">If you reimage a VM, certificates are deleted.</span></span> <span data-ttu-id="43926-212">Réinitialisation des suppressions hello totalité du disque du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="43926-212">Reimaging deletes hello entire OS disk.</span></span> 
 
### <a name="what-happens-if-you-delete-a-certificate-from-hello-key-vault"></a><span data-ttu-id="43926-213">Que se passe-t-il si vous supprimez un certificat à partir du coffre de clés hello ?</span><span class="sxs-lookup"><span data-stu-id="43926-213">What happens if you delete a certificate from hello key vault?</span></span>

<span data-ttu-id="43926-214">Si la clé secrète de hello est supprimé hello coffre de clés, et puis vous exécutez `stop deallocate` pour toutes vos machines virtuelles et les démarrer à nouveau, vous rencontrerez une erreur.</span><span class="sxs-lookup"><span data-stu-id="43926-214">If hello secret is deleted from hello key vault, and then you run `stop deallocate` for all your VMs and then start them again, you will encounter a failure.</span></span> <span data-ttu-id="43926-215">Hello panne hello CRP doit secrets de hello tooretrieve hello coffre de clés, mais il ne peut pas.</span><span class="sxs-lookup"><span data-stu-id="43926-215">hello failure occurs because hello CRP needs tooretrieve hello secrets from hello key vault, but it cannot.</span></span> <span data-ttu-id="43926-216">Dans ce scénario, vous pouvez supprimer les certificats hello modèle du jeu de mise à l’échelle hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="43926-216">In this scenario, you can delete hello certificates from hello virtual machine scale set model.</span></span> 

<span data-ttu-id="43926-217">composant de CRP Hello ne persiste pas les clés secrètes du client.</span><span class="sxs-lookup"><span data-stu-id="43926-217">hello CRP component does not persist customer secrets.</span></span> <span data-ttu-id="43926-218">Si vous exécutez `stop deallocate` pour tous les ordinateurs virtuels dans l’ensemble d’échelle de machine virtuelle hello, hello est supprimé.</span><span class="sxs-lookup"><span data-stu-id="43926-218">If you run `stop deallocate` for all VMs in hello virtual machine scale set, hello cache is deleted.</span></span> <span data-ttu-id="43926-219">Dans ce scénario, les secrets sont récupérés à partir du coffre de clés hello.</span><span class="sxs-lookup"><span data-stu-id="43926-219">In this scenario, secrets are retrieved from hello key vault.</span></span>

<span data-ttu-id="43926-220">Ce problème ne se produit pas lors de la montée en puissance parallèle, car il existe une copie mise en cache du secret hello dans Azure Service Fabric (de modèle de fabric unique client hello).</span><span class="sxs-lookup"><span data-stu-id="43926-220">You don't encounter this problem when scaling out because there is a cached copy of hello secret in Azure Service Fabric (in hello single-fabric tenant model).</span></span>
 
### <a name="why-do-i-have-toospecify-hello-exact-location-for-hello-certificate-url-httpsname-of-hello-vaultvaultazurenet443secretsexact-location-as-indicated-in-service-fabric-cluster-security-scenarioshttpsazuremicrosoftcomdocumentationarticlesservice-fabric-cluster-security"></a><span data-ttu-id="43926-221">Pourquoi dois-je emplacement exact de toospecify hello pour hello certificat URL (https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>), comme indiqué dans [scénarios de sécurité du cluster Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)?</span><span class="sxs-lookup"><span data-stu-id="43926-221">Why do I have toospecify hello exact location for hello certificate URL (https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>), as indicated in [Service Fabric cluster security scenarios](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)?</span></span>
 
<span data-ttu-id="43926-222">Hello documentation d’Azure Key Vault stipule que hello QU'API REST de Secret obtenir doit retourner la version la plus récente du code secret hello hello si la version de hello n’est pas spécifiée.</span><span class="sxs-lookup"><span data-stu-id="43926-222">hello Azure Key Vault documentation states that hello Get Secret REST API should return hello latest version of hello secret if hello version is not specified.</span></span>
 
<span data-ttu-id="43926-223">Méthode</span><span class="sxs-lookup"><span data-stu-id="43926-223">Method</span></span> | <span data-ttu-id="43926-224">URL</span><span class="sxs-lookup"><span data-stu-id="43926-224">URL</span></span>
--- | ---
<span data-ttu-id="43926-225">GET</span><span class="sxs-lookup"><span data-stu-id="43926-225">GET</span></span> | <span data-ttu-id="43926-226">https://mykeyvault.vault.azure.net/secrets/{secret-name}/{secret-version}?api-version={api-version}</span><span class="sxs-lookup"><span data-stu-id="43926-226">https://mykeyvault.vault.azure.net/secrets/{secret-name}/{secret-version}?api-version={api-version}</span></span>

<span data-ttu-id="43926-227">Remplacez {*secret-name*} avec le nom de hello, puis remplacez {*secret-version*} avec version hello du secret de hello souhaité tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="43926-227">Replace {*secret-name*} with hello name, and replace {*secret-version*} with hello version of hello secret you want tooretrieve.</span></span> <span data-ttu-id="43926-228">version du secret Hello peut être exclue.</span><span class="sxs-lookup"><span data-stu-id="43926-228">hello secret version might be excluded.</span></span> <span data-ttu-id="43926-229">Dans ce cas, la version actuelle de hello est récupérée.</span><span class="sxs-lookup"><span data-stu-id="43926-229">In that case, hello current version is retrieved.</span></span>
  
### <a name="why-do-i-have-toospecify-hello-certificate-version-when-i-use-key-vault"></a><span data-ttu-id="43926-230">Pourquoi dois-je version des certificats toospecify hello lorsque j’utilise le coffre de clés ?</span><span class="sxs-lookup"><span data-stu-id="43926-230">Why do I have toospecify hello certificate version when I use Key Vault?</span></span>

<span data-ttu-id="43926-231">Hello version de certificat hello coffre de clés besoin toospecify hello vise toomake il effacer toohello utilisateur quel certificat est déployé sur leurs ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="43926-231">hello purpose of hello Key Vault requirement toospecify hello certificate version is toomake it clear toohello user what certificate is deployed on their VMs.</span></span>

<span data-ttu-id="43926-232">Si vous créez une machine virtuelle, puis mettez à jour votre clé secrète dans le coffre de clés hello, un nouveau certificat hello n’est pas téléchargé tooyour VMs.</span><span class="sxs-lookup"><span data-stu-id="43926-232">If you create a VM and then update your secret in hello key vault, hello new certificate is not downloaded tooyour VMs.</span></span> <span data-ttu-id="43926-233">Mais vos machines virtuelles tooreference et nouvelles machines virtuelles obtiennent le nouveau code secret hello.</span><span class="sxs-lookup"><span data-stu-id="43926-233">But your VMs appear tooreference it, and new VMs get hello new secret.</span></span> <span data-ttu-id="43926-234">tooavoid, vous êtes tooreference requis une version de secret principal.</span><span class="sxs-lookup"><span data-stu-id="43926-234">tooavoid this, you are required tooreference a secret version.</span></span>

### <a name="my-team-works-with-several-certificates-that-are-distributed-toous-as-cer-public-keys-what-is-hello-recommended-approach-for-deploying-these-certificates-tooa-virtual-machine-scale-set"></a><span data-ttu-id="43926-235">Mon équipe travaille avec plusieurs certificats sont distribués toous en tant que les clés publiques .cer.</span><span class="sxs-lookup"><span data-stu-id="43926-235">My team works with several certificates that are distributed toous as .cer public keys.</span></span> <span data-ttu-id="43926-236">Qu’est hello approche pour le déploiement de ces certificats tooa machines virtuelles identiques recommandée ?</span><span class="sxs-lookup"><span data-stu-id="43926-236">What is hello recommended approach for deploying these certificates tooa virtual machine scale set?</span></span>

<span data-ttu-id="43926-237">toodeploy .cer clés publiques tooa machines virtuelles identiques, vous pouvez générer un fichier .pfx qui contient uniquement les fichiers .cer.</span><span class="sxs-lookup"><span data-stu-id="43926-237">toodeploy .cer public keys tooa virtual machine scale set, you can generate a .pfx file that contains only .cer files.</span></span> <span data-ttu-id="43926-238">toodo cela, utilisez `X509ContentType = Pfx`.</span><span class="sxs-lookup"><span data-stu-id="43926-238">toodo this, use `X509ContentType = Pfx`.</span></span> <span data-ttu-id="43926-239">Par exemple, charger le fichier .cer de hello en tant qu’objet x509Certificate2 en c# ou PowerShell, puis appelez la méthode hello.</span><span class="sxs-lookup"><span data-stu-id="43926-239">For example, load hello .cer file as an x509Certificate2 object in C# or PowerShell, and then call hello method.</span></span> 

<span data-ttu-id="43926-240">Pour plus d’informations, consultez [Méthode X509Certificate.Export (X509ContentType, chaîne)](https://msdn.microsoft.com/library/24ww6yzk(v=vs.110.aspx)).</span><span class="sxs-lookup"><span data-stu-id="43926-240">For more information, see [X509Certificate.Export Method (X509ContentType, String)](https://msdn.microsoft.com/library/24ww6yzk(v=vs.110.aspx)).</span></span>

### <a name="i-do-not-see-an-option-for-users-toopass-in-certificates-as-base64-strings-most-other-resource-providers-have-this-option"></a><span data-ttu-id="43926-241">Je ne vois pas une option pour toopass les utilisateurs dans les certificats sous forme de chaînes de format base64.</span><span class="sxs-lookup"><span data-stu-id="43926-241">I do not see an option for users toopass in certificates as base64 strings.</span></span> <span data-ttu-id="43926-242">La plupart des autres fournisseurs de ressources proposent cette option.</span><span class="sxs-lookup"><span data-stu-id="43926-242">Most other resource providers have this option.</span></span>

<span data-ttu-id="43926-243">tooemulate en passant un certificat sous forme de chaîne base64, vous pouvez extraire hello dernières URL avec version dans un modèle de gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="43926-243">tooemulate passing in a certificate as a base64 string, you can extract hello latest versioned URL in a Resource Manager template.</span></span> <span data-ttu-id="43926-244">Inclure hello suivant la propriété JSON dans votre modèle de gestionnaire de ressources :</span><span class="sxs-lookup"><span data-stu-id="43926-244">Include hello following JSON property in your Resource Manager template:</span></span>

```json 
"certificateUrl": "[reference(resourceId(parameters('vaultResourceGroup'), 'Microsoft.KeyVault/vaults/secrets', parameters('vaultName'), parameters('secretName')), '2015-06-01').secretUriWithVersion]"
```
 
### <a name="do-i-have-toowrap-certificates-in-json-objects-in-key-vaults"></a><span data-ttu-id="43926-245">Ai-je besoin de certificats de toowrap dans des objets JSON dans des coffres de clé ?</span><span class="sxs-lookup"><span data-stu-id="43926-245">Do I have toowrap certificates in JSON objects in key vaults?</span></span>

<span data-ttu-id="43926-246">Dans les groupes de machines virtuelles identiques et les machines virtuelles, les certificats doivent être encapsulés dans des objets JSON.</span><span class="sxs-lookup"><span data-stu-id="43926-246">In virtual machine scale sets and VMs, certificates must be wrapped in JSON objects.</span></span> 

<span data-ttu-id="43926-247">Nous avons également prendre en charge hello type de contenu application/x-pkcs12.</span><span class="sxs-lookup"><span data-stu-id="43926-247">We also support hello content type application/x-pkcs12.</span></span> <span data-ttu-id="43926-248">Pour obtenir des instructions sur l’utilisation du type de contenu application/x-pkcs12, consultez [Certificats PFX dans Azure Key Vault](http://www.rahulpnath.com/blog/pfx-certificate-in-azure-key-vault/).</span><span class="sxs-lookup"><span data-stu-id="43926-248">For instructions on using application/x-pkcs12, see [PFX certificates in Azure Key Vault](http://www.rahulpnath.com/blog/pfx-certificate-in-azure-key-vault/).</span></span>
 
<span data-ttu-id="43926-249">Actuellement, nous ne prenons pas en charge les fichiers .cer.</span><span class="sxs-lookup"><span data-stu-id="43926-249">We currently do not support .cer files.</span></span> <span data-ttu-id="43926-250">les fichiers .cer toouse, les exporter dans des conteneurs .pfx.</span><span class="sxs-lookup"><span data-stu-id="43926-250">toouse .cer files, export them into .pfx containers.</span></span>



## <a name="compliance"></a><span data-ttu-id="43926-251">Conformité</span><span class="sxs-lookup"><span data-stu-id="43926-251">Compliance</span></span>

### <a name="are-virtual-machine-scale-sets-pci-compliant"></a><span data-ttu-id="43926-252">Les groupes de machines virtuelles identiques sont-ils compatibles avec PCI ?</span><span class="sxs-lookup"><span data-stu-id="43926-252">Are virtual machine scale sets PCI-compliant?</span></span>

<span data-ttu-id="43926-253">Machines virtuelles identiques sont une fine couche API par-dessus hello CRP.</span><span class="sxs-lookup"><span data-stu-id="43926-253">Virtual machine scale sets are a thin API layer on top of hello CRP.</span></span> <span data-ttu-id="43926-254">Les deux composants font partie de plateforme de calcul hello Bonjour Azure arborescence du service.</span><span class="sxs-lookup"><span data-stu-id="43926-254">Both components are part of hello compute platform in hello Azure service tree.</span></span>

<span data-ttu-id="43926-255">Du point de vue de la conformité, les machines virtuelles identiques sont un élément fondamental de la plateforme de calcul Azure hello.</span><span class="sxs-lookup"><span data-stu-id="43926-255">From a compliance perspective, virtual machine scale sets are a fundamental part of hello Azure compute platform.</span></span> <span data-ttu-id="43926-256">Ils partagent une équipe, outils, processus, méthodologie de déploiement, les contrôles de sécurité, juste-à-temps (JIT) compilation, analyse, alertes et ainsi de suite, avec CRP hello lui-même.</span><span class="sxs-lookup"><span data-stu-id="43926-256">They share a team, tools, processes, deployment methodology, security controls, just-in-time (JIT) compilation, monitoring, alerting, and so on, with hello CRP itself.</span></span> <span data-ttu-id="43926-257">Machines virtuelles identiques sont Payment Card Industry (PCI)-conforme car hello CRP fait partie de l’attestation de sécurité Standard PCI données (DSS) actuel hello.</span><span class="sxs-lookup"><span data-stu-id="43926-257">Virtual machine scale sets are Payment Card Industry (PCI)-compliant because hello CRP is part of hello current PCI Data Security Standard (DSS) attestation.</span></span>

<span data-ttu-id="43926-258">Pour plus d’informations, consultez [hello Microsoft Trust Center](https://www.microsoft.com/TrustCenter/Compliance/PCI).</span><span class="sxs-lookup"><span data-stu-id="43926-258">For more information, see [hello Microsoft Trust Center](https://www.microsoft.com/TrustCenter/Compliance/PCI).</span></span>






## <a name="extensions"></a><span data-ttu-id="43926-259">Extensions</span><span class="sxs-lookup"><span data-stu-id="43926-259">Extensions</span></span>

### <a name="how-do-i-delete-a-virtual-machine-scale-set-extension"></a><span data-ttu-id="43926-260">Comment supprimer une extension de groupe de machines virtuelles identiques ?</span><span class="sxs-lookup"><span data-stu-id="43926-260">How do I delete a virtual machine scale set extension?</span></span>

<span data-ttu-id="43926-261">toodelete une échelle de machines virtuelles définie une extension, hello d’utiliser l’exemple PowerShell suivant :</span><span class="sxs-lookup"><span data-stu-id="43926-261">toodelete a virtual machine scale set extension, use hello following PowerShell example:</span></span>

```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" 

$vmss=Remove-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name "extensionName"

Update-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" -VirtualMacineScaleSet $vmss
```
 
<span data-ttu-id="43926-262">Vous pouvez trouver la valeur d’extensionName hello dans `$vmss`.</span><span class="sxs-lookup"><span data-stu-id="43926-262">You can find hello extensionName value in `$vmss`.</span></span>
   
### <a name="is-there-a-virtual-machine-scale-set-template-example-that-integrates-with-operations-management-suite"></a><span data-ttu-id="43926-263">Existe-t-il un exemple de modèle de groupe de machines virtuelles identiques qui s’intègre à Operations Management Suite ?</span><span class="sxs-lookup"><span data-stu-id="43926-263">Is there a virtual machine scale set template example that integrates with Operations Management Suite?</span></span>

<span data-ttu-id="43926-264">Exemple de modèle qui s’intègre à Operations Management Suite pour une échelle de machines virtuelles, consultez l’exemple de deuxième de hello dans [déployer un cluster Azure Service Fabric et activer l’analyse à l’aide de journal Analytique](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/ServiceFabric).</span><span class="sxs-lookup"><span data-stu-id="43926-264">For a virtual machine scale set template example that integrates with Operations Management Suite, see hello second example in [Deploy an Azure Service Fabric cluster and enable monitoring by using Log Analytics](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/ServiceFabric).</span></span>
   
### <a name="extensions-seem-toorun-in-parallel-on-virtual-machine-scale-sets-this-causes-my-custom-script-extension-toofail-what-can-i-do-toofix-this"></a><span data-ttu-id="43926-265">Extensions semblent toorun en parallèle sur les machines virtuelles identiques.</span><span class="sxs-lookup"><span data-stu-id="43926-265">Extensions seem toorun in parallel on virtual machine scale sets.</span></span> <span data-ttu-id="43926-266">Cela provoque une mon toofail d’extension de script personnalisé.</span><span class="sxs-lookup"><span data-stu-id="43926-266">This causes my custom script extension toofail.</span></span> <span data-ttu-id="43926-267">Que puis-je faire toofix cela ?</span><span class="sxs-lookup"><span data-stu-id="43926-267">What can I do toofix this?</span></span>

<span data-ttu-id="43926-268">toolearn sur le séquencement d’extension dans les machines virtuelles identiques, consultez [séquencement d’Extension dans les machines virtuelles Azure identiques](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/).</span><span class="sxs-lookup"><span data-stu-id="43926-268">toolearn about extension sequencing in virtual machine scale sets, see [Extension sequencing in Azure virtual machine scale sets](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/).</span></span>
 
 
### <a name="how-do-i-reset-hello-password-for-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="43926-269">Comment réinitialiser un mot de passe hello pour les machines virtuelles dans mes machines virtuelles identiques ?</span><span class="sxs-lookup"><span data-stu-id="43926-269">How do I reset hello password for VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="43926-270">tooreset hello mot de passe pour les machines virtuelles dans votre échelle de machines virtuelles définie, utilisez les extensions d’accès de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="43926-270">tooreset hello password for VMs in your virtual machine scale set, use VM access extensions.</span></span> 

<span data-ttu-id="43926-271">Utilisez hello l’exemple PowerShell suivant :</span><span class="sxs-lookup"><span data-stu-id="43926-271">Use hello following PowerShell example:</span></span>

```powershell
$vmssName = "myvmss"
$vmssResourceGroup = "myvmssrg"
$publicConfig = @{"UserName" = "newuser"}
$privateConfig = @{"Password" = "********"}
 
$extName = "VMAccessAgent"
$publisher = "Microsoft.Compute"
$vmss = Get-AzureRmVmss -ResourceGroupName $vmssResourceGroup -VMScaleSetName $vmssName
$vmss = Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name $extName -Publisher $publisher -Setting $publicConfig -ProtectedSetting $privateConfig -Type $extName -TypeHandlerVersion "2.0" -AutoUpgradeMinorVersion $true
Update-AzureRmVmss -ResourceGroupName $vmssResourceGroup -Name $vmssName -VirtualMachineScaleSet $vmss
```
 
 
### <a name="how-do-i-add-an-extension-tooall-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="43926-272">Comment ajouter une extension de tooall machines virtuelles dans mes machines virtuelles identiques ?</span><span class="sxs-lookup"><span data-stu-id="43926-272">How do I add an extension tooall VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="43926-273">Si la stratégie de mise à jour est défini trop**automatique**, redéploiement modèle hello avec de nouvelles propriétés d’extension hello met à jour tous les ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="43926-273">If update policy is set too**automatic**, redeploying hello template with hello new extension properties updates all VMs.</span></span>

<span data-ttu-id="43926-274">Si la stratégie de mise à jour est défini trop**manuelle**, tout d’abord mettre à jour les extension hello et mettre à jour manuellement toutes les instances de vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="43926-274">If update policy is set too**manual**, first update hello extension, and then manually update all instances in your VMs.</span></span>

  
### <a name="if-hello-extensions-associated-with-an-existing-virtual-machine-scale-set-are-updated-are-existing-vms-affected-that-is-will-hello-vms-not-match-hello-virtual-machine-scale-set-model-or-are-they-ignored-when-an-existing-machine-is-service-healed-or-reimaged-are-hello-scripts-that-are-currently-configured-on-hello-virtual-machine-scale-set-executed-or-are-hello-scripts-that-were-configured-when-hello-vm-was-first-created-used"></a><span data-ttu-id="43926-275">Si les extensions hello associées à un ensemble d’échelle de machine virtuelle existants sont mis à jour, sont déjà affectés de machines virtuelles ?</span><span class="sxs-lookup"><span data-stu-id="43926-275">If hello extensions associated with an existing virtual machine scale set are updated, are existing VMs affected?</span></span> <span data-ttu-id="43926-276">(Autrement dit, sera hello des machines virtuelles *pas* modèle du jeu de mise à l’échelle correspondance hello machine virtuelle ?) Ou sont-elles ignorées ?</span><span class="sxs-lookup"><span data-stu-id="43926-276">(That is, will hello VMs *not* match hello virtual machine scale set model?) Or are they ignored?</span></span> <span data-ttu-id="43926-277">Lorsqu’un ordinateur existant est réparé de service ou réinitialisé, sont des scripts hello actuellement configurés sur l’ensemble d’échelle de machine virtuelle hello exécuté, ou des scripts hello qui ont été configurées lorsque hello que machine virtuelle a été créée tout d’abord utilisé ?</span><span class="sxs-lookup"><span data-stu-id="43926-277">When an existing machine is service-healed or reimaged, are hello scripts that are currently configured on hello virtual machine scale set executed, or are hello scripts that were configured when hello VM was first created used?</span></span>

<span data-ttu-id="43926-278">Si la valeur de définition d’extension hello dans l’échelle de machines virtuelles hello modèle est mis à jour et hello upgradePolicy propriété trop**automatique**, il met à jour les machines virtuelles de hello.</span><span class="sxs-lookup"><span data-stu-id="43926-278">If hello extension definition in hello virtual machine scale set model is updated and hello upgradePolicy property is set too**automatic**, it updates hello VMs.</span></span> <span data-ttu-id="43926-279">Si la propriété upgradePolicy de hello est définie trop**manuel**, les extensions sont marquées comme modèle de hello ne correspond ne pas.</span><span class="sxs-lookup"><span data-stu-id="43926-279">If hello upgradePolicy property is set too**manual**, extensions are flagged as not matching hello model.</span></span> 

<span data-ttu-id="43926-280">Si une machine virtuelle existante est réparé de service, il apparaît sous la forme d’un redémarrage, et les extensions hello ne sont pas réexécutées.</span><span class="sxs-lookup"><span data-stu-id="43926-280">If an existing VM is service-healed, it appears as a reboot, and hello extensions are not rerun.</span></span> <span data-ttu-id="43926-281">Si elle est réinitialisée, elle est similaire à remplacer le lecteur de hello du système d’exploitation avec l’image source de hello.</span><span class="sxs-lookup"><span data-stu-id="43926-281">If it is reimaged, it's like replacing hello OS drive with hello source image.</span></span> <span data-ttu-id="43926-282">N’importe quel spécialisation du modèle de dernière hello, telles que les extensions, sont exécutés.</span><span class="sxs-lookup"><span data-stu-id="43926-282">Any specialization from hello latest model, such as extensions, are run.</span></span>
 
### <a name="how-do-i-join-a-virtual-machine-scale-set-tooan-azure-ad-domain"></a><span data-ttu-id="43926-283">Comment participer à un domaine de machine virtuelle mise à l’échelle ensemble tooan Azure AD ?</span><span class="sxs-lookup"><span data-stu-id="43926-283">How do I join a virtual machine scale set tooan Azure AD domain?</span></span>

<span data-ttu-id="43926-284">toojoin un domaine Azure Active Directory (Azure AD) de machine virtuelle mise à l’échelle ensemble tooan, vous pouvez définir une extension.</span><span class="sxs-lookup"><span data-stu-id="43926-284">toojoin a virtual machine scale set tooan Azure Active Directory (Azure AD) domain, you can define an extension.</span></span> 

<span data-ttu-id="43926-285">toodefine une extension, utilisez la propriété JsonADDomainExtension de hello :</span><span class="sxs-lookup"><span data-stu-id="43926-285">toodefine an extension, use hello JsonADDomainExtension property:</span></span>

```json
"extensionProfile": {
    "extensions": [
        {
            "name": "joindomain",
            "properties": {
                "publisher": "Microsoft.Compute",
                "type": "JsonADDomainExtension",
                "typeHandlerVersion": "1.3",
                "settings": {
                    "Name": "[parameters('domainName')]",
                    "OUPath": "[variables('ouPath')]",
                    "User": "[variables('domainAndUsername')]",
                    "Restart": "true",
                    "Options": "[variables('domainJoinOptions')]"
                },
                "protectedsettings": {
                    "Password": "[parameters('domainJoinPassword')]"
                }
            }
        }
    ]
}
```
 
### <a name="my-virtual-machine-scale-set-extension-is-trying-tooinstall-something-that-requires-a-reboot-for-example-commandtoexecute-powershellexe--executionpolicy-unrestricted-install-windowsfeature-name-fs-resource-manager-includemanagementtools"></a><span data-ttu-id="43926-286">Mon extension de jeu de mise à l’échelle de machine virtuelle tente de tooinstall une action qui nécessite un redémarrage.</span><span class="sxs-lookup"><span data-stu-id="43926-286">My virtual machine scale set extension is trying tooinstall something that requires a reboot.</span></span> <span data-ttu-id="43926-287">Par exemple, « commandToExecute » : « powershell.exe -ExecutionPolicy Unrestricted Install-WindowsFeature –Name FS-Resource-Manager –IncludeManagementTools »</span><span class="sxs-lookup"><span data-stu-id="43926-287">For example, "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted Install-WindowsFeature –Name FS-Resource-Manager –IncludeManagementTools"</span></span>

<span data-ttu-id="43926-288">Si votre extension de jeu de machine virtuelle mise à l’échelle est la tentative de tooinstall une action qui nécessite un redémarrage, vous pouvez utiliser l’extension Azure Automation DSC (Automation DSC) de hello.</span><span class="sxs-lookup"><span data-stu-id="43926-288">If your virtual machine scale set extension is trying tooinstall something that requires a reboot, you can use hello Azure Automation Desired State Configuration (Automation DSC) extension.</span></span> <span data-ttu-id="43926-289">Si le système d’exploitation de hello est Windows Server 2012 R2, Azure extrait à l’installation de Windows Management Framework (WMF) 5.0 hello, redémarrage et puis continue à la configuration de hello.</span><span class="sxs-lookup"><span data-stu-id="43926-289">If hello operating system is Windows Server 2012 R2, Azure pulls in hello Windows Management Framework (WMF) 5.0 setup, reboots, and then continues with hello configuration.</span></span> 
 
### <a name="how-do-i-turn-on-antimalware-in-my-virtual-machine-scale-set"></a><span data-ttu-id="43926-290">Comment activer le logiciel anti-programme malveillant dans mon groupe de machines virtuelles identiques ?</span><span class="sxs-lookup"><span data-stu-id="43926-290">How do I turn on antimalware in my virtual machine scale set?</span></span>

<span data-ttu-id="43926-291">tooturn sur les logiciels anti-programme malveillant sur votre échelle de machines virtuelles définir, utilisez les hello l’exemple PowerShell suivant :</span><span class="sxs-lookup"><span data-stu-id="43926-291">tooturn on antimalware on your virtual machine scale set, use hello following PowerShell example:</span></span>

```powershell
$rgname = 'autolap'
$vmssname = 'autolapbr'
$location = 'eastus'
 
# Retrieve hello most recent version number of hello extension.
$allVersions= (Get-AzureRmVMExtensionImage -Location $location -PublisherName "Microsoft.Azure.Security" -Type "IaaSAntimalware").Version
$versionString = $allVersions[($allVersions.count)-1].Split(".")[0] + "." + $allVersions[($allVersions.count)-1].Split(".")[1]
 
$VMSS = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname
echo $VMSS
Add-AzureRmVmssExtension -VirtualMachineScaleSet $VMSS -Name "IaaSAntimalware" -Publisher "Microsoft.Azure.Security" -Type "IaaSAntimalware" -TypeHandlerVersion $versionString
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $VMSS 
```

### <a name="i-need-tooexecute-a-custom-script-thats-hosted-in-a-private-storage-account-hello-script-runs-successfully-when-hello-storage-is-public-but-when-i-try-toouse-a-shared-access-signature-sas-it-fails-this-message-is-displayed-missing-mandatory-parameters-for-valid-shared-access-signature-linksas-works-fine-from-my-local-browser"></a><span data-ttu-id="43926-292">J’ai besoin tooexecute un script personnalisé qui est hébergé dans un compte de stockage privé.</span><span class="sxs-lookup"><span data-stu-id="43926-292">I need tooexecute a custom script that's hosted in a private storage account.</span></span> <span data-ttu-id="43926-293">script de Hello s’exécute correctement lorsque le stockage de hello est publique, mais lorsque je tente de toouse une Signature d’accès partagé (SAS), il échoue.</span><span class="sxs-lookup"><span data-stu-id="43926-293">hello script runs successfully when hello storage is public, but when I try toouse a Shared Access Signature (SAS), it fails.</span></span> <span data-ttu-id="43926-294">Ce message s’affiche : « Paramètres obligatoires manquants pour la signature d’accès partagé valide ».</span><span class="sxs-lookup"><span data-stu-id="43926-294">This message is displayed: “Missing mandatory parameters for valid Shared Access Signature”.</span></span> <span data-ttu-id="43926-295">Le lien et la SAP fonctionnent correctement à partir de mon navigateur local.</span><span class="sxs-lookup"><span data-stu-id="43926-295">Link+SAS works fine from my local browser.</span></span>

<span data-ttu-id="43926-296">tooexecute un script personnalisé qui est hébergé dans un compte de stockage privé, configurer des paramètres protégés avec clé de compte de stockage hello et le nom.</span><span class="sxs-lookup"><span data-stu-id="43926-296">tooexecute a custom script that's hosted in a private storage account, set up protected settings with hello storage account key and name.</span></span> <span data-ttu-id="43926-297">Pour plus d’informations, consultez [Extension de script personnalisé pour Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/#template-example-for-a-windows-vm-with-protected-settings).</span><span class="sxs-lookup"><span data-stu-id="43926-297">For more information, see [Custom Script Extension for Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/#template-example-for-a-windows-vm-with-protected-settings).</span></span>







## <a name="networking"></a><span data-ttu-id="43926-298">Mise en réseau</span><span class="sxs-lookup"><span data-stu-id="43926-298">Networking</span></span>
 
### <a name="is-it-possible-tooassign-a-network-security-group-nsg-tooa-scale-set-so-that-it-will-apply-tooall-hello-vm-nics-in-hello-set"></a><span data-ttu-id="43926-299">Il est possible tooassign une échelle de tooa du groupe de sécurité réseau (NSG) est définie, afin qu’il applique tooall hello NIC de machine virtuelle dans le jeu de hello ?</span><span class="sxs-lookup"><span data-stu-id="43926-299">Is it possible tooassign a Network Security Group (NSG) tooa scale set, so that it will apply tooall hello VM NICs in hello set?</span></span>

<span data-ttu-id="43926-300">Oui.</span><span class="sxs-lookup"><span data-stu-id="43926-300">Yes.</span></span> <span data-ttu-id="43926-301">Un groupe de sécurité réseau peuvent être appliqué directement de l’ensemble d’échelle de tooa par référencement dans la section des configurations hello du profil de réseau hello.</span><span class="sxs-lookup"><span data-stu-id="43926-301">A Network Security Group can be applied directly tooa scale set by referencing it in hello networkInterfaceConfigurations section of hello network profile.</span></span> <span data-ttu-id="43926-302">Exemple :</span><span class="sxs-lookup"><span data-stu-id="43926-302">Example:</span></span>

```json
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
            "name": "nic1",
            "properties": {
                "primary": "true",
                "ipConfigurations": [
                    {
                        "name": "ip1",
                        "properties": {
                            "subnet": {
                                "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                            }
                "loadBalancerInboundNatPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                                }
                            ],
                            "loadBalancerBackendAddressPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                                 }
                            ]
                        }
                    }
                ],
                "networkSecurityGroup": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/networkSecurityGroups/', variables('nsgName'))]"
                }
            }
        }
    ]
}
```

### <a name="how-do-i-do-a-vip-swap-for-virtual-machine-scale-sets-in-hello-same-subscription-and-same-region"></a><span data-ttu-id="43926-303">Comment faire un échange d’adresses IP virtuelles pour l’échelle de machines virtuelles définit Bonjour même abonnement et la même région ?</span><span class="sxs-lookup"><span data-stu-id="43926-303">How do I do a VIP swap for virtual machine scale sets in hello same subscription and same region?</span></span>

<span data-ttu-id="43926-304">Si vous avez deux virtuel échelle de machines définit avec équilibrage de charge Azure les serveurs frontaux, et elles sont dans hello même abonnement et la région, vous pouvez libérer des adresses IP publiques hello à partir de chacun d’eux et affecter toohello autres.</span><span class="sxs-lookup"><span data-stu-id="43926-304">If you have two virtual machine scale sets with Azure Load Balancer front-ends, and they are in hello same subscription and region, you could deallocate hello public IP addresses from each one, and assign toohello other.</span></span> <span data-ttu-id="43926-305">Consultez [VIP Swap: Blue-green deployment in Azure Resource Manager](https://msftstack.wordpress.com/2017/02/24/vip-swap-blue-green-deployment-in-azure-resource-manager/) (Échange d’adresse IP virtuelle (VIP) : Déploiement Bleu/vert dans Azure Resource Manager) pour avoir un exemple.</span><span class="sxs-lookup"><span data-stu-id="43926-305">See [VIP Swap: Blue-green deployment in Azure Resource Manager](https://msftstack.wordpress.com/2017/02/24/vip-swap-blue-green-deployment-in-azure-resource-manager/) for example.</span></span> <span data-ttu-id="43926-306">Cela implique un délai si comme hello ressources sont libérées/allouée au niveau du réseau hello.</span><span class="sxs-lookup"><span data-stu-id="43926-306">This does imply a delay though as hello resources are deallocated/allocated at hello network level.</span></span> <span data-ttu-id="43926-307">Une option plus rapide est toouse passerelle d’Application Azure avec deux pools principaux et une règle de routage.</span><span class="sxs-lookup"><span data-stu-id="43926-307">A faster option is toouse Azure Application Gateway with two backend pools, and a routing rule.</span></span> <span data-ttu-id="43926-308">Une autre option consiste à héberger votre application avec [Azure App service](https://azure.microsoft.com/en-us/services/app-service/), qui fournit une assistance pour basculer rapidement entre emplacements intermédiaires et emplacements de production.</span><span class="sxs-lookup"><span data-stu-id="43926-308">Alternatively, you could host your application with [Azure App service](https://azure.microsoft.com/en-us/services/app-service/) which provides support for fast switching between staging and production slots.</span></span>
 
### <a name="how-do-i-specify-a-range-of-private-ip-addresses-toouse-for-static-private-ip-address-allocation"></a><span data-ttu-id="43926-309">Comment pour spécifier une plage de toouse d’adresses IP privée pour l’allocation d’adresse IP privée statique ?</span><span class="sxs-lookup"><span data-stu-id="43926-309">How do I specify a range of private IP addresses toouse for static private IP address allocation?</span></span>

<span data-ttu-id="43926-310">Les adresses IP sont sélectionnées à partir d’un sous-réseau que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="43926-310">IP addresses are selected from a subnet that you specify.</span></span> 

<span data-ttu-id="43926-311">méthode d’allocation Hello d’adresses IP de machine virtuelle mise à l’échelle ensemble est toujours « dynamique », mais cela ne signifie pas que ces adresses IP peuvent changer.</span><span class="sxs-lookup"><span data-stu-id="43926-311">hello allocation method of virtual machine scale set IP addresses is always “dynamic,” but that doesn't mean that these IP addresses can change.</span></span> <span data-ttu-id="43926-312">Dans ce cas, « dynamiques » signifie uniquement que vous ne spécifiez pas d’adresse IP de hello dans une demande PUT.</span><span class="sxs-lookup"><span data-stu-id="43926-312">In this case, "dynamic" only means that you do not specify hello IP address in a PUT request.</span></span> <span data-ttu-id="43926-313">Spécifiez hello statique définie à l’aide de sous-réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="43926-313">Specify hello static set by using hello subnet.</span></span> 
    
### <a name="how-do-i-deploy-a-virtual-machine-scale-set-tooan-existing-azure-virtual-network"></a><span data-ttu-id="43926-314">Comment déployer un machine virtuelle mise à l’échelle ensemble tooan Azure réseau virtuel existant ?</span><span class="sxs-lookup"><span data-stu-id="43926-314">How do I deploy a virtual machine scale set tooan existing Azure virtual network?</span></span> 

<span data-ttu-id="43926-315">toodeploy une échelle de machines virtuelles tooan le réseau virtuel Azure existant, consultez [déployer un machine virtuelle mise à l’échelle ensemble tooan réseau virtuel existant](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="43926-315">toodeploy a virtual machine scale set tooan existing Azure virtual network, see [Deploy a virtual machine scale set tooan existing virtual network](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-existing-vnet).</span></span> 

### <a name="how-do-i-add-hello-ip-address-of-hello-first-vm-in-a-virtual-machine-scale-set-toohello-output-of-a-template"></a><span data-ttu-id="43926-316">Comment ajouter des adresses IP de hello Hello première machine virtuelle dans une échelle de machine virtuelle définie sortie toohello d’un modèle ?</span><span class="sxs-lookup"><span data-stu-id="43926-316">How do I add hello IP address of hello first VM in a virtual machine scale set toohello output of a template?</span></span>

<span data-ttu-id="43926-317">consultez de première machine virtuelle dans une sortie de toohello de jeu de machine virtuelle mise à l’échelle d’un modèle, adresse IP tooadd hello hello [ARM : adresses IP privées de d’obtenir mise](http://stackoverflow.com/questions/42790392/arm-get-vmsss-private-ips).</span><span class="sxs-lookup"><span data-stu-id="43926-317">tooadd hello IP address of hello first VM in a virtual machine scale set toohello output of a template, see [ARM: Get VMSS's private IPs](http://stackoverflow.com/questions/42790392/arm-get-vmsss-private-ips).</span></span>

### <a name="can-i-use-scale-sets-with-accelerated-networking"></a><span data-ttu-id="43926-318">Puis-je me servir de groupes identiques lors d’une mise en réseau accélérée ?</span><span class="sxs-lookup"><span data-stu-id="43926-318">Can I use scale sets with Accelerated Networking?</span></span>

<span data-ttu-id="43926-319">Oui.</span><span class="sxs-lookup"><span data-stu-id="43926-319">Yes.</span></span> <span data-ttu-id="43926-320">toouse accelerated mise en réseau, définissez enableAcceleratedNetworking tootrue dans votre échelle les paramètres de configurations de définir.</span><span class="sxs-lookup"><span data-stu-id="43926-320">toouse accelerated networking, set enableAcceleratedNetworking tootrue in your scale set's networkInterfaceConfigurations settings.</span></span> <span data-ttu-id="43926-321">Par exemple,</span><span class="sxs-lookup"><span data-stu-id="43926-321">E.g.</span></span>
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
    {
        "name": "niconfig1",
        "properties": {
        "primary": true,
        "enableAcceleratedNetworking" : true,
        "ipConfigurations": [
                ]
            }
            }
        ]
        }
    }
    ]
}
```

### <a name="how-can-i-configure-hello-dns-servers-used-by-a-scale-set"></a><span data-ttu-id="43926-322">Comment puis-je configurer des serveurs DNS de hello utilisés par un ensemble d’échelle ?</span><span class="sxs-lookup"><span data-stu-id="43926-322">How can I configure hello DNS servers used by a scale set?</span></span>

<span data-ttu-id="43926-323">toocreate une échelle de machine virtuelle définie avec une configuration DNS personnalisée, ajoutez la que section de configurations du jeu d’une échelle de toohello paquet dnsSettings JSON.</span><span class="sxs-lookup"><span data-stu-id="43926-323">toocreate a VM scale set with a custom DNS configuration, add a dnsSettings JSON packet toohello scale set networkInterfaceConfigurations section.</span></span> <span data-ttu-id="43926-324">Exemple :</span><span class="sxs-lookup"><span data-stu-id="43926-324">Example:</span></span>
```json
    "dnsSettings":{
        "dnsServers":["10.0.0.6", "10.0.0.5"]
    }
```

### <a name="how-can-i-configure-a-scale-set-tooassign-a-public-ip-address-tooeach-vm"></a><span data-ttu-id="43926-325">Comment puis-je configurer un tooassign de jeu de mise à l’échelle un tooeach d’adresse IP publique machine virtuelle ?</span><span class="sxs-lookup"><span data-stu-id="43926-325">How can I configure a scale set tooassign a public IP address tooeach VM?</span></span>

<span data-ttu-id="43926-326">toocreate une échelle de machine virtuelle défini qui affecte un tooeach d’adresse IP publique machine virtuelle, assurez-vous que la version hello API Hello Microsoft.Compute/virtualMAchineScaleSets ressource est 2017-03-30 et ajouter un _publicipaddressconfiguration_ paquet JSON ensemble d’échelle de toohello de section de configurations IP.</span><span class="sxs-lookup"><span data-stu-id="43926-326">toocreate a VM scale set that assigns a public IP address tooeach VM, make sure hello API version of hello Microsoft.Compute/virtualMAchineScaleSets resource is 2017-03-30, and add a _publicipaddressconfiguration_ JSON packet toohello scale set ipConfigurations section.</span></span> <span data-ttu-id="43926-327">Exemple :</span><span class="sxs-lookup"><span data-stu-id="43926-327">Example:</span></span>

```json
    "publicipaddressconfiguration": {
        "name": "pub1",
        "properties": {
        "idleTimeoutInMinutes": 15
        }
    }
```

### <a name="can-i-configure-a-scale-set-toowork-with-multiple-application-gateways"></a><span data-ttu-id="43926-328">Puis-je configurer un toowork de jeu de mise à l’échelle avec plusieurs passerelles d’Application ?</span><span class="sxs-lookup"><span data-stu-id="43926-328">Can I configure a scale set toowork with multiple Application Gateways?</span></span>

<span data-ttu-id="43926-329">Oui.</span><span class="sxs-lookup"><span data-stu-id="43926-329">Yes.</span></span> <span data-ttu-id="43926-330">Vous pouvez ajouter hello id de ressources pour plusieurs passerelle d’Application principal adresse pools toohello _applicationGatewayBackendAddressPools_ liste Bonjour _ipConfigurations_ section de votre ensemble d’échelle profil de réseau.</span><span class="sxs-lookup"><span data-stu-id="43926-330">You can add hello resource id's for multiple Application Gateway backend address pools toohello _applicationGatewayBackendAddressPools_ list in hello _ipConfigurations_ section of your scale set network profile.</span></span>

## <a name="scale"></a><span data-ttu-id="43926-331">Mettre à l'échelle</span><span class="sxs-lookup"><span data-stu-id="43926-331">Scale</span></span>

### <a name="in-what-case-would-i-create-a-virtual-machine-scale-set-with-fewer-than-two-vms"></a><span data-ttu-id="43926-332">Dans quel cas dois-je créer un groupe de machines virtuelles identiques avec moins de deux machines virtuelles ?</span><span class="sxs-lookup"><span data-stu-id="43926-332">In what case would I create a virtual machine scale set with fewer than two VMs?</span></span>

<span data-ttu-id="43926-333">L’une des raisons toocreate une échelle de machines virtuelles avec ensemble moins de deux machines virtuelles sont propriétés élastique de hello toouse d’une échelle de machine virtuelle définies.</span><span class="sxs-lookup"><span data-stu-id="43926-333">One reason toocreate a virtual machine scale set with fewer than two VMs would be toouse hello elastic properties of a virtual machine scale set.</span></span> <span data-ttu-id="43926-334">Par exemple, vous pouvez déployer un ensemble d’échelle de machine virtuelle avec zéro toodefine de machines virtuelles votre infrastructure sans payer les coûts en cours d’exécution de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="43926-334">For example, you could deploy a virtual machine scale set with zero VMs toodefine your infrastructure without paying VM running costs.</span></span> <span data-ttu-id="43926-335">Ensuite, lorsque vous êtes prêt toodeploy VMs, augmentez hello « capacité » du nombre d’instances hello machine virtuelle mise à l’échelle ensemble toohello production.</span><span class="sxs-lookup"><span data-stu-id="43926-335">Then, when you are ready toodeploy VMs, increase hello “capacity” of hello virtual machine scale set toohello production instance count.</span></span>

<span data-ttu-id="43926-336">Une autre raison de créer un groupe de machines virtuelles identiques avec moins de deux machines virtuelles est si vous vous souciez moins de la disponibilité par rapport à l’utilisation d’un groupe à haute disponibilité avec des machines virtuelles discrètes.</span><span class="sxs-lookup"><span data-stu-id="43926-336">Another reason you might create a virtual machine scale set with fewer than two VMs is if you're concerned less with availability than in using an availability set with discrete VMs.</span></span> <span data-ttu-id="43926-337">Machines virtuelles identiques vous donnent un toowork moyen avec des unités de calcul indifférencié sont fongibles.</span><span class="sxs-lookup"><span data-stu-id="43926-337">Virtual machine scale sets give you a way toowork with undifferentiated compute units that are fungible.</span></span> <span data-ttu-id="43926-338">Cette uniformité est un atout pour les groupes de machines virtuelles identiques par rapport aux groupes à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="43926-338">This uniformity is a key differentiator for virtual machine scale sets versus availability sets.</span></span> <span data-ttu-id="43926-339">De nombreuses charges de travail sans état n’effectuent pas le suivi des unités individuelles.</span><span class="sxs-lookup"><span data-stu-id="43926-339">Many stateless workloads do not track individual units.</span></span> <span data-ttu-id="43926-340">Si la charge de travail hello supprime, vous pouvez unité de calcul tooone à l’échelle et évoluer puis réduire à la charge de travail hello augmente.</span><span class="sxs-lookup"><span data-stu-id="43926-340">If hello workload drops, you can scale down tooone compute unit, and then scale up toomany when hello workload increases.</span></span>

### <a name="how-do-i-change-hello-number-of-vms-in-a-virtual-machine-scale-set"></a><span data-ttu-id="43926-341">Comment modifier le nombre de hello d’ordinateurs virtuels dans un ensemble d’échelle de machine virtuelle ?</span><span class="sxs-lookup"><span data-stu-id="43926-341">How do I change hello number of VMs in a virtual machine scale set?</span></span>

<span data-ttu-id="43926-342">nombre de hello toochange d’ordinateurs virtuels dans un ensemble d’échelle de machine virtuelle, consultez [modifier le nombre d’instances hello d’un ensemble d’échelle de machine virtuelle](https://msftstack.wordpress.com/2016/05/13/change-the-instance-count-of-an-azure-vm-scale-set/).</span><span class="sxs-lookup"><span data-stu-id="43926-342">toochange hello number of VMs in a virtual machine scale set, see [Change hello instance count of a virtual machine scale set](https://msftstack.wordpress.com/2016/05/13/change-the-instance-count-of-an-azure-vm-scale-set/).</span></span>

### <a name="how-do-i-define-custom-alerts-for-when-certain-thresholds-are-reached"></a><span data-ttu-id="43926-343">Comment définir des alertes personnalisées lorsque certains seuils sont atteints ?</span><span class="sxs-lookup"><span data-stu-id="43926-343">How do I define custom alerts for when certain thresholds are reached?</span></span>

<span data-ttu-id="43926-344">Vous bénéficiez d’une certaine flexibilité dans la façon dont vous gérez les alertes pour les seuils spécifiés.</span><span class="sxs-lookup"><span data-stu-id="43926-344">You have some flexibility in how you handle alerts for specified thresholds.</span></span> <span data-ttu-id="43926-345">Vous pouvez, par exemple, définir des webhooks personnalisés.</span><span class="sxs-lookup"><span data-stu-id="43926-345">For example, you can define customized webhooks.</span></span> <span data-ttu-id="43926-346">Hello webhook l’exemple suivant peut d’un modèle de gestionnaire de ressources :</span><span class="sxs-lookup"><span data-stu-id="43926-346">hello following webhook example is from a Resource Manager template:</span></span>

```json
{
    "type": "Microsoft.Insights/autoscaleSettings",
    "apiVersion": "[variables('insightsApi')]",
    "name": "autoscale",
    "location": "[parameters('resourceLocation')]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]"
    ],
    "properties": {
        "name": "autoscale",
        "targetResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/',  resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
        "enabled": true,
        "notifications": [
            {
                "operation": "Scale",
                "email": {
                    "sendToSubscriptionAdministrator": true,
                    "sendToSubscriptionCoAdministrators": true,
                    "customEmails": [
                        "youremail@address.com"
                    ]
                },
                "webhooks": [
                    {
                        "serviceUri": "https://events.pagerduty.com/integration/0b75b57246814149b4d87fa6e1273687/enqueue",
                        "properties": {
                            "key1": "custommetric",
                            "key2": "scalevmss"
                        }
                    }
                ]
            }
        ],
```

<span data-ttu-id="43926-347">Dans cet exemple, une alerte passe tooPagerduty.com lorsqu’un seuil est atteint.</span><span class="sxs-lookup"><span data-stu-id="43926-347">In this example, an alert goes tooPagerduty.com when a threshold is reached.</span></span>



## <a name="patching-and-operations"></a><span data-ttu-id="43926-348">Application de correctifs et opérations</span><span class="sxs-lookup"><span data-stu-id="43926-348">Patching and operations</span></span>

### <a name="how-do-i-create-a-scale-set-in-an-existing-resource-group"></a><span data-ttu-id="43926-349">Comment créer un groupe identique dans un groupe de ressources existant ?</span><span class="sxs-lookup"><span data-stu-id="43926-349">How do I create a scale set in an existing resource group?</span></span>

<span data-ttu-id="43926-350">Création d’ensembles de montée en puissance dans une ressource existante groupe n’est pas encore possible de hello portail Azure, mais vous pouvez spécifier un groupe de ressources lorsque le déploiement d’une mise à l’échelle définie à partir d’un modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="43926-350">Creating scale sets in an existing resource group is not yet possible from hello Azure portal, but you can specify an existing resource group when deploying a scale set from an Azure Resource Manager template.</span></span> <span data-ttu-id="43926-351">Vous pouvez également spécifier un groupe de ressources existant lors de la création d’un groupe identique à l’aide d’Azure PowerShell ou de l’interface CLI.</span><span class="sxs-lookup"><span data-stu-id="43926-351">You can also specify an existing resource group when creating a scale set using Azure PowerShell or CLI.</span></span>

### <a name="can-we-move-a-scale-set-tooanother-resource-group"></a><span data-ttu-id="43926-352">Nous pouvons déplacer qu'un groupe de ressources tooanother le surapprovisionnement ?</span><span class="sxs-lookup"><span data-stu-id="43926-352">Can we move a scale set tooanother resource group?</span></span>

<span data-ttu-id="43926-353">Oui, vous pouvez déplacer l’échelle ensemble ressources tooa nouvel abonnement ou groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="43926-353">Yes, you can move scale set resources tooa new subscription or resource group.</span></span>

### <a name="how-tooi-update-my-virtual-machine-scale-set-tooa-new-image-how-do-i-manage-patching"></a><span data-ttu-id="43926-354">Comment mettre à jour des tooI mon échelle de machines virtuelles définies tooa nouvelle image ?</span><span class="sxs-lookup"><span data-stu-id="43926-354">How tooI update my virtual machine scale set tooa new image?</span></span> <span data-ttu-id="43926-355">Comment gérer la mise à jour corrective ?</span><span class="sxs-lookup"><span data-stu-id="43926-355">How do I manage patching?</span></span>

<span data-ttu-id="43926-356">tooupdate votre échelle de machines virtuelles définie tooa nouvelle image et la mise à jour corrective toomanage, consultez [mise à niveau d’un ensemble d’échelle de machine virtuelle](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-upgrade-scale-set).</span><span class="sxs-lookup"><span data-stu-id="43926-356">tooupdate your virtual machine scale set tooa new image, and toomanage patching, see [Upgrade a virtual machine scale set](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-upgrade-scale-set).</span></span>

### <a name="can-i-use-hello-reimage-operation-tooreset-a-vm-without-changing-hello-image-that-is-i-want-reset-a-vm-toofactory-settings-rather-than-tooa-new-image"></a><span data-ttu-id="43926-357">Puis-je utiliser hello réinitialisation opération tooreset une machine virtuelle sans modifier l’image de hello ?</span><span class="sxs-lookup"><span data-stu-id="43926-357">Can I use hello reimage operation tooreset a VM without changing hello image?</span></span> <span data-ttu-id="43926-358">(Autrement dit, je souhaite réinitialiser un paramètres toofactory d’ordinateurs virtuels au lieu de la nouvelle image de tooa.)</span><span class="sxs-lookup"><span data-stu-id="43926-358">(That is, I want reset a VM toofactory settings rather than tooa new image.)</span></span>

<span data-ttu-id="43926-359">Oui, vous pouvez utiliser hello réinitialisation opération tooreset une machine virtuelle sans modifier l’image de hello.</span><span class="sxs-lookup"><span data-stu-id="43926-359">Yes, you can use hello reimage operation tooreset a VM without changing hello image.</span></span> <span data-ttu-id="43926-360">Toutefois, si la valeur de l’échelle de l’ordinateur virtuel fait référence à une image de plateforme avec `version = latest`, votre machine virtuelle peut mettre à jour tooa de l’image du système d’exploitation ultérieure lorsque vous appelez `reimage`.</span><span class="sxs-lookup"><span data-stu-id="43926-360">However, if your virtual machine scale set references a platform image with `version = latest`, your VM can update tooa later OS image when you call `reimage`.</span></span>

<span data-ttu-id="43926-361">Pour plus d’informations, consultez [Gérer toutes les machines virtuelles dans un groupe de machines virtuelles identiques](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-all-vms-in-a-set).</span><span class="sxs-lookup"><span data-stu-id="43926-361">For more information, see [Manage all VMs in a virtual machine scale set](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-all-vms-in-a-set).</span></span>



## <a name="troubleshooting"></a><span data-ttu-id="43926-362">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="43926-362">Troubleshooting</span></span>

### <a name="how-do-i-turn-on-boot-diagnostics"></a><span data-ttu-id="43926-363">Comment activer les diagnostics de démarrage ?</span><span class="sxs-lookup"><span data-stu-id="43926-363">How do I turn on boot diagnostics?</span></span>

<span data-ttu-id="43926-364">tooturn sur les diagnostics de démarrage, commencez par créer un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="43926-364">tooturn on boot diagnostics, first, create a storage account.</span></span> <span data-ttu-id="43926-365">Ensuite, placez ce bloc JSON dans vos machines virtuelles identiques **virtualMachineProfile**et mettre à jour hello machines virtuelles identiques :</span><span class="sxs-lookup"><span data-stu-id="43926-365">Then, put this JSON block in your virtual machine scale set **virtualMachineProfile**, and update hello virtual machine scale set:</span></span>

```json
"diagnosticsProfile": {
    "bootDiagnostics": {
        "enabled": true,
        "storageUri": "http://yourstorageaccount.blob.core.windows.net"
    }
}
```

<span data-ttu-id="43926-366">Lorsqu’un nouvel ordinateur virtuel est créé, hello propriété InstanceView Hello VM affiche les détails de hello pour la capture d’écran de hello et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="43926-366">When a new VM is created, hello InstanceView property of hello VM shows hello details for hello screenshot, and so on.</span></span> <span data-ttu-id="43926-367">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="43926-367">Here's an example:</span></span>
 
```json
"bootDiagnostics": {
    "consoleScreenshotBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.screenshot.bmp",
    "serialConsoleLogBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.serialconsole.log"
  }
```


## <a name="virtual-machine-properties"></a><span data-ttu-id="43926-368">Propriétés de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="43926-368">Virtual machine properties</span></span>

### <a name="how-do-i-get-property-information-for-each-vm-without-making-multiple-calls-for-example-how-would-i-get-hello-fault-domain-for-each-of-hello-100-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="43926-369">Comment obtenir des informations sur les propriétés de chaque machine virtuelle sans avoir à effectuer plusieurs appels ?</span><span class="sxs-lookup"><span data-stu-id="43926-369">How do I get property information for each VM without making multiple calls?</span></span> <span data-ttu-id="43926-370">Par exemple, comment serait obtenir domaine d’erreur hello pour chacun des hello 100 machines virtuelles dans mes machines virtuelles identiques ?</span><span class="sxs-lookup"><span data-stu-id="43926-370">For example, how would I get hello fault domain for each of hello 100 VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="43926-371">informations sur les propriétés tooget pour chaque ordinateur virtuel sans effectuer plusieurs appels, vous pouvez appeler `ListVMInstanceViews` en effectuant une API REST `GET` sur hello suivant l’URI de ressource :</span><span class="sxs-lookup"><span data-stu-id="43926-371">tooget property information for each VM without making multiple calls, you can call `ListVMInstanceViews` by doing a REST API `GET` on hello following resource URI:</span></span>

<span data-ttu-id="43926-372">/subscriptions/<subscription_id>/resourceGroups/<resource_group_name>/providers/Microsoft.Compute/virtualMachineScaleSets/<scaleset_name>/virtualMachines?$expand=instanceView&$select=instanceView</span><span class="sxs-lookup"><span data-stu-id="43926-372">/subscriptions/<subscription_id>/resourceGroups/<resource_group_name>/providers/Microsoft.Compute/virtualMachineScaleSets/<scaleset_name>/virtualMachines?$expand=instanceView&$select=instanceView</span></span>

### <a name="can-i-pass-different-extension-arguments-toodifferent-vms-in-a-virtual-machine-scale-set"></a><span data-ttu-id="43926-373">Puis-je transmettre arguments d’extension différentes machines virtuelles de toodifferent dans un ensemble d’échelle de machine virtuelle ?</span><span class="sxs-lookup"><span data-stu-id="43926-373">Can I pass different extension arguments toodifferent VMs in a virtual machine scale set?</span></span>

<span data-ttu-id="43926-374">Non, vous ne pouvez pas passer arguments d’extension de différentes toodifferent VM dans un ensemble d’échelle de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="43926-374">No, you cannot pass different extension arguments toodifferent VMs in a virtual machine scale set.</span></span> <span data-ttu-id="43926-375">Toutefois, les extensions peuvent agir en fonction des propriétés uniques de hello Hello machine virtuelle s’exécutent sur, comme sur le nom de l’ordinateur hello.</span><span class="sxs-lookup"><span data-stu-id="43926-375">However, extensions can act based on hello unique properties of hello VM they are running on, such as on hello machine name.</span></span> <span data-ttu-id="43926-376">Extensions également peuvent interroger les métadonnées d’instance sur http://169.254.169.254 tooget plus d’informations sur la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="43926-376">Extensions also can query instance metadata on http://169.254.169.254 tooget more information about hello VM.</span></span>

### <a name="why-are-there-gaps-between-my-virtual-machine-scale-set-vm-machine-names-and-vm-ids-for-example-0-1-3"></a><span data-ttu-id="43926-377">Pourquoi y a-t-il des écarts entre les noms de machines virtuelles de mon groupe de machines virtuelles identiques et les ID des machines virtuelles ?</span><span class="sxs-lookup"><span data-stu-id="43926-377">Why are there gaps between my virtual machine scale set VM machine names and VM IDs?</span></span> <span data-ttu-id="43926-378">Par exemple : 0, 1, 3...</span><span class="sxs-lookup"><span data-stu-id="43926-378">For example: 0, 1, 3...</span></span>

<span data-ttu-id="43926-379">Il existe des écarts entre votre machine virtuelle mise à l’échelle ensemble VM machine noms et les ID de machine virtuelle, car la valeur de l’échelle de l’ordinateur virtuel **overprovision** propriété a la valeur par défaut toohello **true**.</span><span class="sxs-lookup"><span data-stu-id="43926-379">There are gaps between your virtual machine scale set VM machine names and VM IDs because your virtual machine scale set **overprovision** property is set toohello default value of **true**.</span></span> <span data-ttu-id="43926-380">Si un surapprovisionnement est défini trop**true**, davantage d’ordinateurs virtuels que celle demandée sont créés.</span><span class="sxs-lookup"><span data-stu-id="43926-380">If overprovisioning is set too**true**, more VMs than requested are created.</span></span> <span data-ttu-id="43926-381">Les machines virtuelles supplémentaires sont ensuite supprimées.</span><span class="sxs-lookup"><span data-stu-id="43926-381">Extra VMs are then deleted.</span></span> <span data-ttu-id="43926-382">Dans ce cas, vous obtenir la fiabilité du déploiement accrue, mais à des frais de hello de d’affectation de noms contigu et la traduction d’adresses réseau (NAT) contiguës de règles.</span><span class="sxs-lookup"><span data-stu-id="43926-382">In this case, you gain increased deployment reliability, but at hello expense of contiguous naming and contiguous Network Address Translation (NAT) rules.</span></span> 

<span data-ttu-id="43926-383">Vous pouvez définir cette propriété trop**false**.</span><span class="sxs-lookup"><span data-stu-id="43926-383">You can set this property too**false**.</span></span> <span data-ttu-id="43926-384">Pour les petits groupes de machines virtuelles identiques, cela n’affecte pas vraiment la fiabilité du déploiement.</span><span class="sxs-lookup"><span data-stu-id="43926-384">For small virtual machine scale sets, this doesn't significantly affect deployment reliability.</span></span>

### <a name="what-is-hello-difference-between-deleting-a-vm-in-a-virtual-machine-scale-set-and-deallocating-hello-vm-when-should-i-choose-one-over-hello-other"></a><span data-ttu-id="43926-385">Qu’est la différence hello entre la suppression d’une machine virtuelle dans un ensemble d’échelle de machine virtuelle et de désallocation hello machine virtuelle ?</span><span class="sxs-lookup"><span data-stu-id="43926-385">What is hello difference between deleting a VM in a virtual machine scale set and deallocating hello VM?</span></span> <span data-ttu-id="43926-386">Quand dois-je choisir un sur hello autres ?</span><span class="sxs-lookup"><span data-stu-id="43926-386">When should I choose one over hello other?</span></span>

<span data-ttu-id="43926-387">Hello principale différence entre la suppression d’une machine virtuelle dans un ensemble d’échelle de machine virtuelle et de désallocation hello machine virtuelle est que `deallocate` ne supprime pas hello les disques durs virtuels (VHD).</span><span class="sxs-lookup"><span data-stu-id="43926-387">hello main difference between deleting a VM in a virtual machine scale set and deallocating hello VM is that `deallocate` doesn’t delete hello virtual hard disks (VHDs).</span></span> <span data-ttu-id="43926-388">Il existe des coûts de stockage associés à l’exécution de `stop deallocate`.</span><span class="sxs-lookup"><span data-stu-id="43926-388">There are storage costs associated with running `stop deallocate`.</span></span> <span data-ttu-id="43926-389">Vous pourrez utiliser un ou l’autre pour l’une des hello suivant raisons hello :</span><span class="sxs-lookup"><span data-stu-id="43926-389">You might use one or hello other for one of hello following reasons:</span></span>

- <span data-ttu-id="43926-390">Vous souhaitez toostop coûts de calcul, mais vous souhaitez que l’état de disque tookeep hello Hello machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="43926-390">You want toostop paying compute costs, but you want tookeep hello disk state of hello VMs.</span></span>
- <span data-ttu-id="43926-391">Vous souhaitez toostart un ensemble de machines virtuelles plus rapidement que vous pouvez monter en charge un ensemble d’échelle de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="43926-391">You want toostart a set of VMs more quickly than you could scale out a virtual machine scale set.</span></span>
  - <span data-ttu-id="43926-392">Scénario de toothis connexes, vous avez peut-être créé votre propre moteur de mise à l’échelle et que vous souhaitez une échelle de bout en bout plus rapide.</span><span class="sxs-lookup"><span data-stu-id="43926-392">Related toothis scenario, you might have created your own autoscale engine and want a faster end-to-end scale.</span></span>
- <span data-ttu-id="43926-393">Vous avez un groupe de machines virtuelles identiques qui est distribué inégalement entre les domaines d’erreur ou les domaines de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="43926-393">You have a virtual machine scale set that is unevenly distributed across fault domains or update domains.</span></span> <span data-ttu-id="43926-394">Cela peut être dû au fait que vous avez supprimé sélectivement des machines virtuelles, ou parce que des machines virtuelles ont été supprimées après le sur-approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="43926-394">This might be because you selectively deleted VMs, or because VMs were deleted after overprovisioning.</span></span> <span data-ttu-id="43926-395">En cours d’exécution `stop deallocate` suivie `start` sur l’ordinateur virtuel de hello échelle définie uniformément distribue des machines virtuelles de hello entre domaines d’erreur ou de domaines de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="43926-395">Running `stop deallocate` followed by `start` on hello virtual machine scale set evenly distributes hello VMs across fault domains or update domains.</span></span>

