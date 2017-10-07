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
# <a name="azure-virtual-machine-scale-sets-faqs"></a>FAQ sur les groupes de machines virtuelles identiques Azure

Obtenez des réponses aux questions sur l’échelle de machines virtuelles d’elles sonttrop définit dans Azure.

## <a name="autoscale"></a>Autoscale

### <a name="what-are-best-practices-for-azure-autoscale"></a>Quelles sont les meilleures pratiques pour la mise à l’échelle automatique d’Azure ?

Pour connaître les meilleures pratiques pour la mise à l’échelle automatique, consultez [Meilleures pratiques pour la mise à l’échelle automatique des machines virtuelles](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-best-practices).

### <a name="where-do-i-find-metric-names-for-autoscaling-that-uses-host-based-metrics"></a>Où trouver les noms des métriques pour la mise à l’échelle automatique utilisant des métriques basées sur les hôtes ?

Pour obtenir les noms des métriques pour la mise à l’échelle automatique utilisant des métriques basées sur les hôtes, consultez [Métriques prises en charge avec Azure Monitor](https://azure.microsoft.com/documentation/articles/monitoring-supported-metrics/).

### <a name="are-there-any-examples-of-autoscaling-based-on-an-azure-service-bus-topic-and-queue-length"></a>Existe-t-il des exemples de mise à l’échelle automatique basée sur une rubrique Azure Service Bus et une longueur de file d’attente ?

Oui. Pour obtenir des exemples de mise à l’échelle automatique basée sur une rubrique Azure Service Bus et une longueur de file d’attente, consultez [Métriques courantes pour la mise à l’échelle automatique d’Azure Monitor](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/).

Pour une file d’attente Service Bus, utilisez hello suivant JSON :

```json
"metricName": "MessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue"
```

Pour une file d’attente de stockage, utilisez hello suivant JSON :

```json
"metricName": "ApproximateMessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ClassicStorage/storageAccounts/mystorage/services/queue/queues/mystoragequeue"
```

Remplacez les exemples de valeurs par les URI (Uniform Resource Identifiers) de votre ressource.


### <a name="should-i-autoscale-by-using-host-based-metrics-or-a-diagnostics-extension"></a>Dois-je utiliser la mise à l’échelle automatique avec des métriques basées sur les hôtes ou une extension de diagnostics ?

Vous pouvez créer un paramètre de mise à l’échelle sur un métriques de machine virtuelle toouse au niveau hôte ou les métriques de basé sur le système d’exploitation invité.

Pour obtenir la liste des métriques prises en charge, consultez [Métriques courantes pour la mise à l’échelle automatique d’Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-common-metrics). 

Pour obtenir un exemple complet pour les groupes de machines virtuelles identiques, consultez [Configuration avancée de la mise à l’échelle automatique à l’aide de modèles Resource Manager pour les groupes de machines virtuelles identiques](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-advanced-autoscale-virtual-machine-scale-sets). 

exemple Hello utilise la métrique de l’UC au niveau hôte hello et une métrique de nombre de messages.



### <a name="how-do-i-set-alert-rules-on-a-virtual-machine-scale-set"></a>Comment définir des règles d’alerte sur un groupe de machines virtuelles identiques ?

Vous pouvez créer des alertes sur des métriques pour les groupes de machines virtuelles identiques via PowerShell ou l’interface CLI Azure. Pour plus d’informations, consultez [Exemples de démarrage rapide Azure Monitor PowerShell](https://azure.microsoft.com/documentation/articles/insights-powershell-samples/#create-alert-rules) et [Exemples de démarrage CLI interplateforme Azure Monitor](https://azure.microsoft.com/documentation/articles/insights-cli-samples/#work-with-alerts).

Hello TargetResourceId d’ensemble d’échelle de machine virtuelle hello ressemble à ceci : 

/subscriptions/yoursubscriptionid/resourceGroups/yourresourcegroup/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmssname

Vous pouvez choisir n’importe quel compteur de performances de machine virtuelle comme tooset de métrique hello une alerte. Pour plus d’informations, consultez [métriques du système d’exploitation invité pour les machines virtuelles Windows basée sur le Gestionnaire de ressources](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-resource-manager-based-windows-vms) et [métriques du système d’exploitation invité pour les machines virtuelles Linux](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-linux-vms) Bonjour [mesures courantes de l’échelle automatique de moniteur Azure](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/)l’article.

### <a name="how-do-i-set-up-autoscale-on-a-virtual-machine-scale-set-by-using-powershell"></a>Comment configurer la mise à l’échelle automatique sur un groupe de machines virtuelles identiques à l’aide de PowerShell ?

tooset de mise à l’échelle sur une échelle de machine virtuelle définie à l’aide de PowerShell, voir hello blog [comment tooadd tooan de mise à l’échelle mise à l’échelle de machine virtuelle Azure définie](https://msftstack.wordpress.com/2017/03/05/how-to-add-autoscale-to-an-azure-vm-scale-set/).




## <a name="certificates"></a>Certificats

### <a name="how-do-i-securely-ship-a-certificate-toohello-vm-how-do-i-provision-a-virtual-machine-scale-set-toorun-a-website-where-hello-ssl-for-hello-website-is-shipped-securely-from-a-certificate-configuration-hello-common-certificate-rotation-operation-would-be-almost-hello-same-as-a-configuration-update-operation-do-you-have-an-example-of-how-toodo-this"></a>Comment expédier en toute sécurité un toohello certificat machine virtuelle ? Comment pour configurer un toorun de jeu de machine virtuelle mise à l’échelle un site Web où hello SSL pour le site Web de hello est envoyée en toute sécurité à partir d’une configuration de certificat ? (opération de rotation du certificat commun hello serait être presque hello identique à une opération de mise à jour de configuration.) Disposez-vous d’un exemple de procédure toodo cela ? 

toosecurely livrer un toohello certificat machine virtuelle, vous pouvez installer un certificat client directement dans un magasin de certificats Windows coffre du client hello de clés.

Utilisez hello suivant JSON :

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

code de Hello prend en charge Windows et Linux.

Pour plus d’informations, consultez [Création ou mise à jour d’un groupe de machines virtuelles identiques](https://msdn.microsoft.com/library/mt589035.aspx).


### <a name="example-of-self-signed-certificate"></a>Exemple de certificat auto-signé

1.  Créez un certificat auto-signé dans un coffre de clés.

    Utilisez hello suivant de commandes PowerShell :

    ```powershell
    Import-Module "C:\Users\mikhegn\Downloads\Service-Fabric-master\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

    Login-AzureRmAccount

    Invoke-AddCertToKeyVault -SubscriptionId <Your SubID> -ResourceGroupName KeyVault -Location westus -VaultName MikhegnVault -CertificateName VMSSCert -Password VmssCert -CreateSelfSignedCertificate -DnsName vmss.mikhegn.azure.com -OutputPath c:\users\mikhegn\desktop\
    ```

    Ceci permet de commande vous hello entrée pour le modèle de gestionnaire de ressources Azure hello.

    Pour obtenir un exemple de toocreate un certificat auto-signé dans un coffre de clés, voir [scénarios de sécurité du cluster Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/).

2.  Modifier le modèle de gestionnaire de ressources hello.

    Ajouter cette propriété trop**virtualMachineProfile**, définie des ressources dans le cadre de hello échelle de machines virtuelles :

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
  

### <a name="can-i-specify-an-ssh-key-pair-toouse-for-ssh-authentication-with-a-linux-virtual-machine-scale-set-from-a-resource-manager-template"></a>Puis-je spécifier une toouse de paire de clés SSH pour l’authentification SSH avec une échelle de machine virtuelle Linux définir à partir d’un modèle de gestionnaire de ressources ?  

Oui. Hello API REST pour **osProfile** est l’API REST de machine virtuelle standard toohello similaire. 

Incluez **osProfile** dans votre modèle :

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
 
Ce bloc JSON est utilisé dans [modèle de démarrage rapide de hello 101-vm-sshkey GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).
 
Hello profil de système d’exploitation est également utilisé dans [hello grelayhost.json GitHub rapide démarrer modèle](https://github.com/ExchMaster/gadgetron/blob/master/Gadgetron/Templates/grelayhost.json).

Pour plus d’informations, consultez [Création ou mise à jour d’un groupe de machines virtuelles identiques](https://msdn.microsoft.com/library/azure/mt589035.aspx#linuxconfiguration).
  

### <a name="how-do-i-remove-deprecated-certificates"></a>Comment supprimer des certificats obsolètes ? 

tooremove déconseillée certificats, remove hello ancien certificat à partir de la liste de certificats de coffre hello. Conservez tous les certificats hello que vous souhaitez tooremain sur votre ordinateur dans la liste de hello. Cela ne supprime pas de certificat de hello de toutes vos machines virtuelles. Aussi, il n’ajoute pas de hello certificat toonew les ordinateurs virtuels qui sont créés dans l’ensemble d’échelle de machine virtuelle hello. 

certificat de hello tooremove à partir de machines virtuelles existantes, écrire un script personnalisé pour extension toomanually supprimer hello des certificats à partir de votre magasin de certificats.
 
### <a name="how-do-i-inject-an-existing-ssh-public-key-into-hello-virtual-machine-scale-set-ssh-layer-during-provisioning-i-want-toostore-hello-ssh-public-key-values-in-azure-key-vault-and-then-use-them-in-my-resource-manager-template"></a>Comment injecter une clé publique SSH existante dans hello machine virtuelle mise à l’échelle ensemble SSH couche lors de la configuration ? J’ai choix toostore hello SSH valeurs de clé publique dans le coffre de clés Azure, puis les utiliser dans mon modèle de gestionnaire de ressources.

Si vous fournissez uniquement avec une clé SSH publique hello machines virtuelles, vous n’avez pas besoin tooput les clés publiques hello dans le coffre de clés. Les clés publiques ne sont pas secrètes.
 
Vous pouvez fournir les clés publiques SSH en texte brut lorsque vous créez une machine virtuelle Linux :

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
 
nom d’élément linuxConfiguration | Requis | Type | Description
--- | --- | --- | --- |  ---
ssh | Non | Collection | Spécifie la configuration de clé SSH hello pour un système d’exploitation Linux
path | Oui | String | Spécifie le chemin d’accès du fichier hello Linux où les clés SSH hello ou un certificat doit être situé
keyData | Oui | String | Spécifie une clé publique SSH encodée en base64

Pour obtenir un exemple, consultez [modèle de démarrage rapide de hello 101-vm-sshkey GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).

 
### <a name="when-i-run-update-azurermvmss-after-adding-more-than-one-certificate-from-hello-same-key-vault-i-see-hello-following-message"></a>Lors de l’exécution `Update-AzureRmVmss` après l’ajout de plusieurs certificats à partir de hello même clé de coffre, voir hello message suivant :
 
>Update-AzureRmVmss : List secret (Afficher la liste des secrets) contient des instances répétées de /subscriptions/<my-subscription-id>/resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev, ce qui n’est pas autorisé.
 
Cela peut se produire si vous essayez de toore-ajouter hello même coffre au lieu d’utiliser un nouveau certificat de coffre pour le coffre source existant hello. Hello `Add-AzureRmVmssSecret` commande ne fonctionne pas correctement si vous ajoutez des clés secrètes supplémentaires.
 
tooadd plus secrets à partir de hello même coffre de clés, de mise à jour hello $vmss.properties.osProfile.secrets[0].vaultCertificates liste.
 
Pour hello prévu la structure d’entrée, consultez [créer ou mettre à jour un ordinateur virtuel défini](https://msdn.microsoft.com/library/azure/mt589035.aspx).
 
Trouver secret de hello dans l’objet de jeu hello machine virtuelle mise à l’échelle qui se trouve dans le coffre de clés hello. Ajoutez ensuite votre liste de toohello de référence (hello URL et le nom du magasin des secrets hello) de certificat associé au coffre de hello.

> [!NOTE] 
> Actuellement, vous ne peut pas supprimer les certificats d’ordinateurs virtuels à l’aide de hello machine virtuelle mise à l’échelle ensemble API.
>

Nouvelles machines virtuelles ne possèdent pas de certificat d’ancien hello. Toutefois, les ordinateurs virtuels qui ont des certificats de hello et qui sont déjà déployé aura ancien certificat de hello.
 
### <a name="can-i-push-certificates-toohello-virtual-machine-scale-set-without-providing-hello-password-when-hello-certificate-is-in-hello-secret-store"></a>Puis-je push échelle de machines virtuelles toohello certificats défini sans fournir de mot de passe hello lorsque hello certificat dans le magasin des secrets hello ?

Vous n’avez pas besoin de mots de passe toohard-code dans les scripts. Vous pouvez récupérer de manière dynamique les mots de passe avec des autorisations hello vous utilisez le script de déploiement toorun hello. Si vous avez un script qui se déplace d’un certificat à partir du coffre de clés de magasin des secrets hello, hello magasin des secrets `get certificate` commande génère également un mot de passe hello du fichier .pfx de hello.
 
### <a name="how-does-hello-secrets-property-of-virtualmachineprofileosprofile-for-a-virtual-machine-scale-set-work-why-do-i-need-hello-sourcevault-value-when-i-have-toospecify-hello-absolute-uri-for-a-certificate-by-using-hello-certificateurl-property"></a>Comment la propriété Secrets hello virtualMachineProfile.osProfile pour une échelle de machine virtuelle définie travail ? Pourquoi dois-je valeur sourceVault de hello lorsque j’ai toospecify hello URI absolu d’un certificat à l’aide hello certificateUrl propriété ? 

Une référence de certificat Windows Remote Management (WinRM) doit être présente dans hello propriété Secrets de hello profil de système d’exploitation. 

Hello indiquant le coffre source hello vise stratégies de liste (ACL) du contrôle d’accès tooenforce qui existent dans le modèle de Service Cloud Azure d’un utilisateur. Si le coffre source hello n’est pas spécifié, les utilisateurs ne disposant pas d’autorisations toodeploy ou access secrets tooa coffre de clés est en mesure de toothrough un fournisseur de ressources de calcul (CRP). Les listes ACL existent même pour les ressources qui n’existent pas.

Si vous fournissez un ID de coffre incorrect de la source, mais une URL valide de coffre de clés, une erreur est signalée lorsque vous interrogez les opération hello.
 
### <a name="if-i-add-secrets-tooan-existing-virtual-machine-scale-set-are-hello-secrets-injected-into-existing-vms-or-only-into-new-ones"></a>Si j’ajoute tooan secrets existant de machines virtuelles identiques, les secrets hello sont injectées dans des machines virtuelles existantes, ou uniquement dans d’autres ? 

Les certificats sont ajoutés tooall vos machines virtuelles, même préexistant ceux. Si votre échelle de machines virtuelles upgradePolicy propriété la valeur est défini trop**manuelle**, hello ajouté certificat toohello machine virtuelle lorsque vous effectuez une mise à jour manuelle sur hello machine virtuelle.
 
### <a name="where-do-i-put-certificates-for-linux-vms"></a>Où dois-je placer les certificats pour les machines virtuelles Linux ?

toolearn toodeploy des certificats pour les ordinateurs virtuels Linux, voir [tooVMs de certificats à partir d’un coffre de clés gérée par le client de déployer](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/).
  
### <a name="how-do-i-add-a-new-vault-certificate-tooa-new-certificate-object"></a>Comment ajouter un nouveau coffre certificat tooa nouvel objet de certificat ?

tooadd un secret coffre certificat tooan existant, consultez hello l’exemple PowerShell suivant. Utilisez un seul objet secret.
 
```powershell
$newVaultCertificate = New-AzureRmVmssVaultCertificateConfig -CertificateStore MY -CertificateUrl https://sansunallapps1.vault.azure.net:443/secrets/dg-private-enc/55fa0332edc44a84ad655298905f1809
 
$vmss.VirtualMachineProfile.OsProfile.Secrets[0].VaultCertificates.Add($newVaultCertificate)
 
Update-AzureRmVmss -VirtualMachineScaleSet $vmss -ResourceGroup $rg -Name $vmssName
```
 
### <a name="what-happens-toocertificates-if-you-reimage-a-vm"></a>Que passe-t-il toocertificates si vous réinitialisez un ordinateur virtuel ?

Si vous réinitialisez une machine virtuelle, les certificats sont supprimés. Réinitialisation des suppressions hello totalité du disque du système d’exploitation. 
 
### <a name="what-happens-if-you-delete-a-certificate-from-hello-key-vault"></a>Que se passe-t-il si vous supprimez un certificat à partir du coffre de clés hello ?

Si la clé secrète de hello est supprimé hello coffre de clés, et puis vous exécutez `stop deallocate` pour toutes vos machines virtuelles et les démarrer à nouveau, vous rencontrerez une erreur. Hello panne hello CRP doit secrets de hello tooretrieve hello coffre de clés, mais il ne peut pas. Dans ce scénario, vous pouvez supprimer les certificats hello modèle du jeu de mise à l’échelle hello machine virtuelle. 

composant de CRP Hello ne persiste pas les clés secrètes du client. Si vous exécutez `stop deallocate` pour tous les ordinateurs virtuels dans l’ensemble d’échelle de machine virtuelle hello, hello est supprimé. Dans ce scénario, les secrets sont récupérés à partir du coffre de clés hello.

Ce problème ne se produit pas lors de la montée en puissance parallèle, car il existe une copie mise en cache du secret hello dans Azure Service Fabric (de modèle de fabric unique client hello).
 
### <a name="why-do-i-have-toospecify-hello-exact-location-for-hello-certificate-url-httpsname-of-hello-vaultvaultazurenet443secretsexact-location-as-indicated-in-service-fabric-cluster-security-scenarioshttpsazuremicrosoftcomdocumentationarticlesservice-fabric-cluster-security"></a>Pourquoi dois-je emplacement exact de toospecify hello pour hello certificat URL (https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>), comme indiqué dans [scénarios de sécurité du cluster Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)?
 
Hello documentation d’Azure Key Vault stipule que hello QU'API REST de Secret obtenir doit retourner la version la plus récente du code secret hello hello si la version de hello n’est pas spécifiée.
 
Méthode | URL
--- | ---
GET | https://mykeyvault.vault.azure.net/secrets/{secret-name}/{secret-version}?api-version={api-version}

Remplacez {*secret-name*} avec le nom de hello, puis remplacez {*secret-version*} avec version hello du secret de hello souhaité tooretrieve. version du secret Hello peut être exclue. Dans ce cas, la version actuelle de hello est récupérée.
  
### <a name="why-do-i-have-toospecify-hello-certificate-version-when-i-use-key-vault"></a>Pourquoi dois-je version des certificats toospecify hello lorsque j’utilise le coffre de clés ?

Hello version de certificat hello coffre de clés besoin toospecify hello vise toomake il effacer toohello utilisateur quel certificat est déployé sur leurs ordinateurs virtuels.

Si vous créez une machine virtuelle, puis mettez à jour votre clé secrète dans le coffre de clés hello, un nouveau certificat hello n’est pas téléchargé tooyour VMs. Mais vos machines virtuelles tooreference et nouvelles machines virtuelles obtiennent le nouveau code secret hello. tooavoid, vous êtes tooreference requis une version de secret principal.

### <a name="my-team-works-with-several-certificates-that-are-distributed-toous-as-cer-public-keys-what-is-hello-recommended-approach-for-deploying-these-certificates-tooa-virtual-machine-scale-set"></a>Mon équipe travaille avec plusieurs certificats sont distribués toous en tant que les clés publiques .cer. Qu’est hello approche pour le déploiement de ces certificats tooa machines virtuelles identiques recommandée ?

toodeploy .cer clés publiques tooa machines virtuelles identiques, vous pouvez générer un fichier .pfx qui contient uniquement les fichiers .cer. toodo cela, utilisez `X509ContentType = Pfx`. Par exemple, charger le fichier .cer de hello en tant qu’objet x509Certificate2 en c# ou PowerShell, puis appelez la méthode hello. 

Pour plus d’informations, consultez [Méthode X509Certificate.Export (X509ContentType, chaîne)](https://msdn.microsoft.com/library/24ww6yzk(v=vs.110.aspx)).

### <a name="i-do-not-see-an-option-for-users-toopass-in-certificates-as-base64-strings-most-other-resource-providers-have-this-option"></a>Je ne vois pas une option pour toopass les utilisateurs dans les certificats sous forme de chaînes de format base64. La plupart des autres fournisseurs de ressources proposent cette option.

tooemulate en passant un certificat sous forme de chaîne base64, vous pouvez extraire hello dernières URL avec version dans un modèle de gestionnaire de ressources. Inclure hello suivant la propriété JSON dans votre modèle de gestionnaire de ressources :

```json 
"certificateUrl": "[reference(resourceId(parameters('vaultResourceGroup'), 'Microsoft.KeyVault/vaults/secrets', parameters('vaultName'), parameters('secretName')), '2015-06-01').secretUriWithVersion]"
```
 
### <a name="do-i-have-toowrap-certificates-in-json-objects-in-key-vaults"></a>Ai-je besoin de certificats de toowrap dans des objets JSON dans des coffres de clé ?

Dans les groupes de machines virtuelles identiques et les machines virtuelles, les certificats doivent être encapsulés dans des objets JSON. 

Nous avons également prendre en charge hello type de contenu application/x-pkcs12. Pour obtenir des instructions sur l’utilisation du type de contenu application/x-pkcs12, consultez [Certificats PFX dans Azure Key Vault](http://www.rahulpnath.com/blog/pfx-certificate-in-azure-key-vault/).
 
Actuellement, nous ne prenons pas en charge les fichiers .cer. les fichiers .cer toouse, les exporter dans des conteneurs .pfx.



## <a name="compliance"></a>Conformité

### <a name="are-virtual-machine-scale-sets-pci-compliant"></a>Les groupes de machines virtuelles identiques sont-ils compatibles avec PCI ?

Machines virtuelles identiques sont une fine couche API par-dessus hello CRP. Les deux composants font partie de plateforme de calcul hello Bonjour Azure arborescence du service.

Du point de vue de la conformité, les machines virtuelles identiques sont un élément fondamental de la plateforme de calcul Azure hello. Ils partagent une équipe, outils, processus, méthodologie de déploiement, les contrôles de sécurité, juste-à-temps (JIT) compilation, analyse, alertes et ainsi de suite, avec CRP hello lui-même. Machines virtuelles identiques sont Payment Card Industry (PCI)-conforme car hello CRP fait partie de l’attestation de sécurité Standard PCI données (DSS) actuel hello.

Pour plus d’informations, consultez [hello Microsoft Trust Center](https://www.microsoft.com/TrustCenter/Compliance/PCI).






## <a name="extensions"></a>Extensions

### <a name="how-do-i-delete-a-virtual-machine-scale-set-extension"></a>Comment supprimer une extension de groupe de machines virtuelles identiques ?

toodelete une échelle de machines virtuelles définie une extension, hello d’utiliser l’exemple PowerShell suivant :

```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" 

$vmss=Remove-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name "extensionName"

Update-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" -VirtualMacineScaleSet $vmss
```
 
Vous pouvez trouver la valeur d’extensionName hello dans `$vmss`.
   
### <a name="is-there-a-virtual-machine-scale-set-template-example-that-integrates-with-operations-management-suite"></a>Existe-t-il un exemple de modèle de groupe de machines virtuelles identiques qui s’intègre à Operations Management Suite ?

Exemple de modèle qui s’intègre à Operations Management Suite pour une échelle de machines virtuelles, consultez l’exemple de deuxième de hello dans [déployer un cluster Azure Service Fabric et activer l’analyse à l’aide de journal Analytique](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/ServiceFabric).
   
### <a name="extensions-seem-toorun-in-parallel-on-virtual-machine-scale-sets-this-causes-my-custom-script-extension-toofail-what-can-i-do-toofix-this"></a>Extensions semblent toorun en parallèle sur les machines virtuelles identiques. Cela provoque une mon toofail d’extension de script personnalisé. Que puis-je faire toofix cela ?

toolearn sur le séquencement d’extension dans les machines virtuelles identiques, consultez [séquencement d’Extension dans les machines virtuelles Azure identiques](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/).
 
 
### <a name="how-do-i-reset-hello-password-for-vms-in-my-virtual-machine-scale-set"></a>Comment réinitialiser un mot de passe hello pour les machines virtuelles dans mes machines virtuelles identiques ?

tooreset hello mot de passe pour les machines virtuelles dans votre échelle de machines virtuelles définie, utilisez les extensions d’accès de machine virtuelle. 

Utilisez hello l’exemple PowerShell suivant :

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
 
 
### <a name="how-do-i-add-an-extension-tooall-vms-in-my-virtual-machine-scale-set"></a>Comment ajouter une extension de tooall machines virtuelles dans mes machines virtuelles identiques ?

Si la stratégie de mise à jour est défini trop**automatique**, redéploiement modèle hello avec de nouvelles propriétés d’extension hello met à jour tous les ordinateurs virtuels.

Si la stratégie de mise à jour est défini trop**manuelle**, tout d’abord mettre à jour les extension hello et mettre à jour manuellement toutes les instances de vos machines virtuelles.

  
### <a name="if-hello-extensions-associated-with-an-existing-virtual-machine-scale-set-are-updated-are-existing-vms-affected-that-is-will-hello-vms-not-match-hello-virtual-machine-scale-set-model-or-are-they-ignored-when-an-existing-machine-is-service-healed-or-reimaged-are-hello-scripts-that-are-currently-configured-on-hello-virtual-machine-scale-set-executed-or-are-hello-scripts-that-were-configured-when-hello-vm-was-first-created-used"></a>Si les extensions hello associées à un ensemble d’échelle de machine virtuelle existants sont mis à jour, sont déjà affectés de machines virtuelles ? (Autrement dit, sera hello des machines virtuelles *pas* modèle du jeu de mise à l’échelle correspondance hello machine virtuelle ?) Ou sont-elles ignorées ? Lorsqu’un ordinateur existant est réparé de service ou réinitialisé, sont des scripts hello actuellement configurés sur l’ensemble d’échelle de machine virtuelle hello exécuté, ou des scripts hello qui ont été configurées lorsque hello que machine virtuelle a été créée tout d’abord utilisé ?

Si la valeur de définition d’extension hello dans l’échelle de machines virtuelles hello modèle est mis à jour et hello upgradePolicy propriété trop**automatique**, il met à jour les machines virtuelles de hello. Si la propriété upgradePolicy de hello est définie trop**manuel**, les extensions sont marquées comme modèle de hello ne correspond ne pas. 

Si une machine virtuelle existante est réparé de service, il apparaît sous la forme d’un redémarrage, et les extensions hello ne sont pas réexécutées. Si elle est réinitialisée, elle est similaire à remplacer le lecteur de hello du système d’exploitation avec l’image source de hello. N’importe quel spécialisation du modèle de dernière hello, telles que les extensions, sont exécutés.
 
### <a name="how-do-i-join-a-virtual-machine-scale-set-tooan-azure-ad-domain"></a>Comment participer à un domaine de machine virtuelle mise à l’échelle ensemble tooan Azure AD ?

toojoin un domaine Azure Active Directory (Azure AD) de machine virtuelle mise à l’échelle ensemble tooan, vous pouvez définir une extension. 

toodefine une extension, utilisez la propriété JsonADDomainExtension de hello :

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
 
### <a name="my-virtual-machine-scale-set-extension-is-trying-tooinstall-something-that-requires-a-reboot-for-example-commandtoexecute-powershellexe--executionpolicy-unrestricted-install-windowsfeature-name-fs-resource-manager-includemanagementtools"></a>Mon extension de jeu de mise à l’échelle de machine virtuelle tente de tooinstall une action qui nécessite un redémarrage. Par exemple, « commandToExecute » : « powershell.exe -ExecutionPolicy Unrestricted Install-WindowsFeature –Name FS-Resource-Manager –IncludeManagementTools »

Si votre extension de jeu de machine virtuelle mise à l’échelle est la tentative de tooinstall une action qui nécessite un redémarrage, vous pouvez utiliser l’extension Azure Automation DSC (Automation DSC) de hello. Si le système d’exploitation de hello est Windows Server 2012 R2, Azure extrait à l’installation de Windows Management Framework (WMF) 5.0 hello, redémarrage et puis continue à la configuration de hello. 
 
### <a name="how-do-i-turn-on-antimalware-in-my-virtual-machine-scale-set"></a>Comment activer le logiciel anti-programme malveillant dans mon groupe de machines virtuelles identiques ?

tooturn sur les logiciels anti-programme malveillant sur votre échelle de machines virtuelles définir, utilisez les hello l’exemple PowerShell suivant :

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

### <a name="i-need-tooexecute-a-custom-script-thats-hosted-in-a-private-storage-account-hello-script-runs-successfully-when-hello-storage-is-public-but-when-i-try-toouse-a-shared-access-signature-sas-it-fails-this-message-is-displayed-missing-mandatory-parameters-for-valid-shared-access-signature-linksas-works-fine-from-my-local-browser"></a>J’ai besoin tooexecute un script personnalisé qui est hébergé dans un compte de stockage privé. script de Hello s’exécute correctement lorsque le stockage de hello est publique, mais lorsque je tente de toouse une Signature d’accès partagé (SAS), il échoue. Ce message s’affiche : « Paramètres obligatoires manquants pour la signature d’accès partagé valide ». Le lien et la SAP fonctionnent correctement à partir de mon navigateur local.

tooexecute un script personnalisé qui est hébergé dans un compte de stockage privé, configurer des paramètres protégés avec clé de compte de stockage hello et le nom. Pour plus d’informations, consultez [Extension de script personnalisé pour Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/#template-example-for-a-windows-vm-with-protected-settings).







## <a name="networking"></a>Mise en réseau
 
### <a name="is-it-possible-tooassign-a-network-security-group-nsg-tooa-scale-set-so-that-it-will-apply-tooall-hello-vm-nics-in-hello-set"></a>Il est possible tooassign une échelle de tooa du groupe de sécurité réseau (NSG) est définie, afin qu’il applique tooall hello NIC de machine virtuelle dans le jeu de hello ?

Oui. Un groupe de sécurité réseau peuvent être appliqué directement de l’ensemble d’échelle de tooa par référencement dans la section des configurations hello du profil de réseau hello. Exemple :

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

### <a name="how-do-i-do-a-vip-swap-for-virtual-machine-scale-sets-in-hello-same-subscription-and-same-region"></a>Comment faire un échange d’adresses IP virtuelles pour l’échelle de machines virtuelles définit Bonjour même abonnement et la même région ?

Si vous avez deux virtuel échelle de machines définit avec équilibrage de charge Azure les serveurs frontaux, et elles sont dans hello même abonnement et la région, vous pouvez libérer des adresses IP publiques hello à partir de chacun d’eux et affecter toohello autres. Consultez [VIP Swap: Blue-green deployment in Azure Resource Manager](https://msftstack.wordpress.com/2017/02/24/vip-swap-blue-green-deployment-in-azure-resource-manager/) (Échange d’adresse IP virtuelle (VIP) : Déploiement Bleu/vert dans Azure Resource Manager) pour avoir un exemple. Cela implique un délai si comme hello ressources sont libérées/allouée au niveau du réseau hello. Une option plus rapide est toouse passerelle d’Application Azure avec deux pools principaux et une règle de routage. Une autre option consiste à héberger votre application avec [Azure App service](https://azure.microsoft.com/en-us/services/app-service/), qui fournit une assistance pour basculer rapidement entre emplacements intermédiaires et emplacements de production.
 
### <a name="how-do-i-specify-a-range-of-private-ip-addresses-toouse-for-static-private-ip-address-allocation"></a>Comment pour spécifier une plage de toouse d’adresses IP privée pour l’allocation d’adresse IP privée statique ?

Les adresses IP sont sélectionnées à partir d’un sous-réseau que vous spécifiez. 

méthode d’allocation Hello d’adresses IP de machine virtuelle mise à l’échelle ensemble est toujours « dynamique », mais cela ne signifie pas que ces adresses IP peuvent changer. Dans ce cas, « dynamiques » signifie uniquement que vous ne spécifiez pas d’adresse IP de hello dans une demande PUT. Spécifiez hello statique définie à l’aide de sous-réseau de hello. 
    
### <a name="how-do-i-deploy-a-virtual-machine-scale-set-tooan-existing-azure-virtual-network"></a>Comment déployer un machine virtuelle mise à l’échelle ensemble tooan Azure réseau virtuel existant ? 

toodeploy une échelle de machines virtuelles tooan le réseau virtuel Azure existant, consultez [déployer un machine virtuelle mise à l’échelle ensemble tooan réseau virtuel existant](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-existing-vnet). 

### <a name="how-do-i-add-hello-ip-address-of-hello-first-vm-in-a-virtual-machine-scale-set-toohello-output-of-a-template"></a>Comment ajouter des adresses IP de hello Hello première machine virtuelle dans une échelle de machine virtuelle définie sortie toohello d’un modèle ?

consultez de première machine virtuelle dans une sortie de toohello de jeu de machine virtuelle mise à l’échelle d’un modèle, adresse IP tooadd hello hello [ARM : adresses IP privées de d’obtenir mise](http://stackoverflow.com/questions/42790392/arm-get-vmsss-private-ips).

### <a name="can-i-use-scale-sets-with-accelerated-networking"></a>Puis-je me servir de groupes identiques lors d’une mise en réseau accélérée ?

Oui. toouse accelerated mise en réseau, définissez enableAcceleratedNetworking tootrue dans votre échelle les paramètres de configurations de définir. Par exemple,
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

### <a name="how-can-i-configure-hello-dns-servers-used-by-a-scale-set"></a>Comment puis-je configurer des serveurs DNS de hello utilisés par un ensemble d’échelle ?

toocreate une échelle de machine virtuelle définie avec une configuration DNS personnalisée, ajoutez la que section de configurations du jeu d’une échelle de toohello paquet dnsSettings JSON. Exemple :
```json
    "dnsSettings":{
        "dnsServers":["10.0.0.6", "10.0.0.5"]
    }
```

### <a name="how-can-i-configure-a-scale-set-tooassign-a-public-ip-address-tooeach-vm"></a>Comment puis-je configurer un tooassign de jeu de mise à l’échelle un tooeach d’adresse IP publique machine virtuelle ?

toocreate une échelle de machine virtuelle défini qui affecte un tooeach d’adresse IP publique machine virtuelle, assurez-vous que la version hello API Hello Microsoft.Compute/virtualMAchineScaleSets ressource est 2017-03-30 et ajouter un _publicipaddressconfiguration_ paquet JSON ensemble d’échelle de toohello de section de configurations IP. Exemple :

```json
    "publicipaddressconfiguration": {
        "name": "pub1",
        "properties": {
        "idleTimeoutInMinutes": 15
        }
    }
```

### <a name="can-i-configure-a-scale-set-toowork-with-multiple-application-gateways"></a>Puis-je configurer un toowork de jeu de mise à l’échelle avec plusieurs passerelles d’Application ?

Oui. Vous pouvez ajouter hello id de ressources pour plusieurs passerelle d’Application principal adresse pools toohello _applicationGatewayBackendAddressPools_ liste Bonjour _ipConfigurations_ section de votre ensemble d’échelle profil de réseau.

## <a name="scale"></a>Mettre à l'échelle

### <a name="in-what-case-would-i-create-a-virtual-machine-scale-set-with-fewer-than-two-vms"></a>Dans quel cas dois-je créer un groupe de machines virtuelles identiques avec moins de deux machines virtuelles ?

L’une des raisons toocreate une échelle de machines virtuelles avec ensemble moins de deux machines virtuelles sont propriétés élastique de hello toouse d’une échelle de machine virtuelle définies. Par exemple, vous pouvez déployer un ensemble d’échelle de machine virtuelle avec zéro toodefine de machines virtuelles votre infrastructure sans payer les coûts en cours d’exécution de machine virtuelle. Ensuite, lorsque vous êtes prêt toodeploy VMs, augmentez hello « capacité » du nombre d’instances hello machine virtuelle mise à l’échelle ensemble toohello production.

Une autre raison de créer un groupe de machines virtuelles identiques avec moins de deux machines virtuelles est si vous vous souciez moins de la disponibilité par rapport à l’utilisation d’un groupe à haute disponibilité avec des machines virtuelles discrètes. Machines virtuelles identiques vous donnent un toowork moyen avec des unités de calcul indifférencié sont fongibles. Cette uniformité est un atout pour les groupes de machines virtuelles identiques par rapport aux groupes à haute disponibilité. De nombreuses charges de travail sans état n’effectuent pas le suivi des unités individuelles. Si la charge de travail hello supprime, vous pouvez unité de calcul tooone à l’échelle et évoluer puis réduire à la charge de travail hello augmente.

### <a name="how-do-i-change-hello-number-of-vms-in-a-virtual-machine-scale-set"></a>Comment modifier le nombre de hello d’ordinateurs virtuels dans un ensemble d’échelle de machine virtuelle ?

nombre de hello toochange d’ordinateurs virtuels dans un ensemble d’échelle de machine virtuelle, consultez [modifier le nombre d’instances hello d’un ensemble d’échelle de machine virtuelle](https://msftstack.wordpress.com/2016/05/13/change-the-instance-count-of-an-azure-vm-scale-set/).

### <a name="how-do-i-define-custom-alerts-for-when-certain-thresholds-are-reached"></a>Comment définir des alertes personnalisées lorsque certains seuils sont atteints ?

Vous bénéficiez d’une certaine flexibilité dans la façon dont vous gérez les alertes pour les seuils spécifiés. Vous pouvez, par exemple, définir des webhooks personnalisés. Hello webhook l’exemple suivant peut d’un modèle de gestionnaire de ressources :

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

Dans cet exemple, une alerte passe tooPagerduty.com lorsqu’un seuil est atteint.



## <a name="patching-and-operations"></a>Application de correctifs et opérations

### <a name="how-do-i-create-a-scale-set-in-an-existing-resource-group"></a>Comment créer un groupe identique dans un groupe de ressources existant ?

Création d’ensembles de montée en puissance dans une ressource existante groupe n’est pas encore possible de hello portail Azure, mais vous pouvez spécifier un groupe de ressources lorsque le déploiement d’une mise à l’échelle définie à partir d’un modèle Azure Resource Manager. Vous pouvez également spécifier un groupe de ressources existant lors de la création d’un groupe identique à l’aide d’Azure PowerShell ou de l’interface CLI.

### <a name="can-we-move-a-scale-set-tooanother-resource-group"></a>Nous pouvons déplacer qu'un groupe de ressources tooanother le surapprovisionnement ?

Oui, vous pouvez déplacer l’échelle ensemble ressources tooa nouvel abonnement ou groupe de ressources.

### <a name="how-tooi-update-my-virtual-machine-scale-set-tooa-new-image-how-do-i-manage-patching"></a>Comment mettre à jour des tooI mon échelle de machines virtuelles définies tooa nouvelle image ? Comment gérer la mise à jour corrective ?

tooupdate votre échelle de machines virtuelles définie tooa nouvelle image et la mise à jour corrective toomanage, consultez [mise à niveau d’un ensemble d’échelle de machine virtuelle](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-upgrade-scale-set).

### <a name="can-i-use-hello-reimage-operation-tooreset-a-vm-without-changing-hello-image-that-is-i-want-reset-a-vm-toofactory-settings-rather-than-tooa-new-image"></a>Puis-je utiliser hello réinitialisation opération tooreset une machine virtuelle sans modifier l’image de hello ? (Autrement dit, je souhaite réinitialiser un paramètres toofactory d’ordinateurs virtuels au lieu de la nouvelle image de tooa.)

Oui, vous pouvez utiliser hello réinitialisation opération tooreset une machine virtuelle sans modifier l’image de hello. Toutefois, si la valeur de l’échelle de l’ordinateur virtuel fait référence à une image de plateforme avec `version = latest`, votre machine virtuelle peut mettre à jour tooa de l’image du système d’exploitation ultérieure lorsque vous appelez `reimage`.

Pour plus d’informations, consultez [Gérer toutes les machines virtuelles dans un groupe de machines virtuelles identiques](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-all-vms-in-a-set).



## <a name="troubleshooting"></a>Résolution des problèmes

### <a name="how-do-i-turn-on-boot-diagnostics"></a>Comment activer les diagnostics de démarrage ?

tooturn sur les diagnostics de démarrage, commencez par créer un compte de stockage. Ensuite, placez ce bloc JSON dans vos machines virtuelles identiques **virtualMachineProfile**et mettre à jour hello machines virtuelles identiques :

```json
"diagnosticsProfile": {
    "bootDiagnostics": {
        "enabled": true,
        "storageUri": "http://yourstorageaccount.blob.core.windows.net"
    }
}
```

Lorsqu’un nouvel ordinateur virtuel est créé, hello propriété InstanceView Hello VM affiche les détails de hello pour la capture d’écran de hello et ainsi de suite. Voici un exemple :
 
```json
"bootDiagnostics": {
    "consoleScreenshotBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.screenshot.bmp",
    "serialConsoleLogBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.serialconsole.log"
  }
```


## <a name="virtual-machine-properties"></a>Propriétés de machine virtuelle

### <a name="how-do-i-get-property-information-for-each-vm-without-making-multiple-calls-for-example-how-would-i-get-hello-fault-domain-for-each-of-hello-100-vms-in-my-virtual-machine-scale-set"></a>Comment obtenir des informations sur les propriétés de chaque machine virtuelle sans avoir à effectuer plusieurs appels ? Par exemple, comment serait obtenir domaine d’erreur hello pour chacun des hello 100 machines virtuelles dans mes machines virtuelles identiques ?

informations sur les propriétés tooget pour chaque ordinateur virtuel sans effectuer plusieurs appels, vous pouvez appeler `ListVMInstanceViews` en effectuant une API REST `GET` sur hello suivant l’URI de ressource :

/subscriptions/<subscription_id>/resourceGroups/<resource_group_name>/providers/Microsoft.Compute/virtualMachineScaleSets/<scaleset_name>/virtualMachines?$expand=instanceView&$select=instanceView

### <a name="can-i-pass-different-extension-arguments-toodifferent-vms-in-a-virtual-machine-scale-set"></a>Puis-je transmettre arguments d’extension différentes machines virtuelles de toodifferent dans un ensemble d’échelle de machine virtuelle ?

Non, vous ne pouvez pas passer arguments d’extension de différentes toodifferent VM dans un ensemble d’échelle de machine virtuelle. Toutefois, les extensions peuvent agir en fonction des propriétés uniques de hello Hello machine virtuelle s’exécutent sur, comme sur le nom de l’ordinateur hello. Extensions également peuvent interroger les métadonnées d’instance sur http://169.254.169.254 tooget plus d’informations sur la machine virtuelle de hello.

### <a name="why-are-there-gaps-between-my-virtual-machine-scale-set-vm-machine-names-and-vm-ids-for-example-0-1-3"></a>Pourquoi y a-t-il des écarts entre les noms de machines virtuelles de mon groupe de machines virtuelles identiques et les ID des machines virtuelles ? Par exemple : 0, 1, 3...

Il existe des écarts entre votre machine virtuelle mise à l’échelle ensemble VM machine noms et les ID de machine virtuelle, car la valeur de l’échelle de l’ordinateur virtuel **overprovision** propriété a la valeur par défaut toohello **true**. Si un surapprovisionnement est défini trop**true**, davantage d’ordinateurs virtuels que celle demandée sont créés. Les machines virtuelles supplémentaires sont ensuite supprimées. Dans ce cas, vous obtenir la fiabilité du déploiement accrue, mais à des frais de hello de d’affectation de noms contigu et la traduction d’adresses réseau (NAT) contiguës de règles. 

Vous pouvez définir cette propriété trop**false**. Pour les petits groupes de machines virtuelles identiques, cela n’affecte pas vraiment la fiabilité du déploiement.

### <a name="what-is-hello-difference-between-deleting-a-vm-in-a-virtual-machine-scale-set-and-deallocating-hello-vm-when-should-i-choose-one-over-hello-other"></a>Qu’est la différence hello entre la suppression d’une machine virtuelle dans un ensemble d’échelle de machine virtuelle et de désallocation hello machine virtuelle ? Quand dois-je choisir un sur hello autres ?

Hello principale différence entre la suppression d’une machine virtuelle dans un ensemble d’échelle de machine virtuelle et de désallocation hello machine virtuelle est que `deallocate` ne supprime pas hello les disques durs virtuels (VHD). Il existe des coûts de stockage associés à l’exécution de `stop deallocate`. Vous pourrez utiliser un ou l’autre pour l’une des hello suivant raisons hello :

- Vous souhaitez toostop coûts de calcul, mais vous souhaitez que l’état de disque tookeep hello Hello machines virtuelles.
- Vous souhaitez toostart un ensemble de machines virtuelles plus rapidement que vous pouvez monter en charge un ensemble d’échelle de machine virtuelle.
  - Scénario de toothis connexes, vous avez peut-être créé votre propre moteur de mise à l’échelle et que vous souhaitez une échelle de bout en bout plus rapide.
- Vous avez un groupe de machines virtuelles identiques qui est distribué inégalement entre les domaines d’erreur ou les domaines de mise à jour. Cela peut être dû au fait que vous avez supprimé sélectivement des machines virtuelles, ou parce que des machines virtuelles ont été supprimées après le sur-approvisionnement. En cours d’exécution `stop deallocate` suivie `start` sur l’ordinateur virtuel de hello échelle définie uniformément distribue des machines virtuelles de hello entre domaines d’erreur ou de domaines de mise à jour.

