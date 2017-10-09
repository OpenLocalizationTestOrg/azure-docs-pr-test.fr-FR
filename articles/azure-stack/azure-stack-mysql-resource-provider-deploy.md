---
title: "aaaUse MySQL de bases de données en tant que PaaS dans Azure pile | Documents Microsoft"
description: "Découvrez comment vous pouvez déployer hello fournisseur de ressources MySQL et fournissent des bases de données MySQL en tant que service sur la pile de Azure"
services: azure-stack
documentationCenter: 
author: JeffGoldner
manager: bradleyb
editor: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: JeffGo
ms.openlocfilehash: 634e408eae9f3d8257a8610c60def0978ce333c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-mysql-databases-on-microsoft-azure-stack"></a>Utiliser des bases de données MySQL sur Microsoft Azure Stack


Vous pouvez déployer un fournisseur de ressources MySQL sur Azure Stack. Après avoir déployé le fournisseur de ressources hello, vous pouvez créer des bases de données via des modèles de déploiement Azure Resource Manager et des serveurs MySQL et fournir des bases de données MySQL en tant que service. Les bases de données MySQL, qui sont courantes sur les sites web, prennent en charge de nombreuses plateformes de site web. Par exemple, après avoir déployé le fournisseur de ressources hello, vous pouvez créer des sites Web WordPress à partir de la plateforme d’applications Web Azure hello comme un module complémentaire de service (PaaS) pour la pile de Azure.

le fournisseur de MySQL toodeploy hello sur un système qui n’a pas accès à internet, vous pouvez copier les fichiers hello [mysql-connector-net-6.9.9.msi](https://dev.mysql.com/get/Download/sConnector-Net/mysql-connector-net-6.9.9.msi) tooa local partager et fournir ce nom de partage lorsque vous y êtes invité (voir ci-dessous). Vous devez également installer les modules Azure et Azure pile PowerShell hello.


## <a name="mysql-server-resource-provider-adapter-architecture"></a>Architecture de l’adaptateur de fournisseur de ressources MySQL Server

fournisseur de ressources Hello est constitué de trois composants :

- **adaptateur de fournisseur ressources Hello MySQL VM**, qui est un ordinateur virtuel de Windows exécutant les services de fournisseur hello.
- **fournisseur de ressources Hello lui-même**, qui traite les demandes d’approvisionnement et expose les ressources de base de données.
- **Les serveurs qui hébergent MySQL Server**, qui fournissent de la capacité pour les bases de données, appelés serveurs d’hébergement. 

Cette version ne crée plus d’instance de MySQL. Vous devez les créer ou fournir un accès tooexternal les instances de SQL. Vous pouvez visiter hello [galerie de démarrage rapide Azure pile](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/mysql-standalone-server-windows) pour un exemple de modèle que vous pouvez créer un serveur MySQL pour vous ou télécharger et déployer un serveur MySQL de hello Marketplace.

## <a name="deploy-hello-resource-provider"></a>Déployer le fournisseur de ressources hello

1. Si vous ne le n'avez pas déjà fait, inscrire votre kit de développement et télécharger hello Windows Server Datacenter 2016 - Eval image téléchargeable via la gestion du Marketplace. Vous pouvez également utiliser un script toocreate un [image de Windows Server 2016](https://docs.microsoft.com/azure/azure-stack/azure-stack-add-default-image).

2. [Télécharger le fichier de fichiers binaires du fournisseur de ressources hello MySQL](https://aka.ms/azurestackmysqlrp) et extrayez-le sur l’hôte de kit de développement hello.

3. Connectez-vous à hôte de kit de développement toohello, puis extraire hello répertoire temporaire de tooa de fichiers de programme d’installation de MySQL RP.

4. certificat racine de pile de Azure Hello est récupérée et un certificat auto-signé est créé dans le cadre de ce processus. 

    __Facultatif :__ si vous avez besoin de tooprovide votre propre, préparer les certificats hello et tooa répertoire local si vous le souhaitez toocustomize les certificats hello (script d’installation toohello passé). Éléments de hello suivants sont nécessaires :

    a. Un certificat générique pour *.dbadapter.\<région\>.\<fqdn_externe\>. Ce certificat doit être approuvé, tel qu’est émise par une autorité de certification (autrement dit, chaîne hello d’approbation doit exister sans exiger de certificats intermédiaires). (Un certificat de site unique utilisable avec nom VM explicite de hello, que vous fournissez lors de l’installation.)

    b. Hello certificat utilisé par hello Azure Resource Manager pour votre instance de la pile de Azure. S’il n’est pas trouvé, certificat hello est récupérée.

5. Ouvrir un **nouvelle** élevé PowerShell console et de modifier le répertoire toohello où vous avez extrait les fichiers hello. Utilisez une nouvelle fenêtre tooavoid les problèmes qui peuvent survenir à partir des modules PowerShell incorrects déjà chargés sur le système de hello.

6. Si vous avez installé des versions des modules AzureStack PowerShell autres que 1.2.9 ou 1.2.10 hello Azure Resource Manager, vous serez invité à tooremove les ou hello installation ne sera pas effectuée. Cela inclut les versions 1.3 ou ultérieures.

7. Exécutez DeployMySqlProvider.ps1.

Ce script effectue les étapes suivantes :

* Si nécessaire, téléchargement d’une version compatible d’Azure PowerShell.
* Téléchargez hello connecteur MySQL binaire (Cela peut être fourni en mode hors connexion).
* Télécharger le certificat de hello et tous les autres tooan artefacts compte de stockage Azure pile.
* Publier des packages de la galerie afin que vous pouvez déployer des bases de données MySQL via la galerie de hello.
* Déploiement d’une machine virtuelle qui héberge votre fournisseur de ressources.
* Inscrire un enregistrement DNS local qui mappe le fournisseur de ressources tooyour machine virtuelle.
* Inscrire votre fournisseur de ressources par hello local Azure Resource Manager.

Spécifiez au moins hello paramètres requis sur la ligne de commande hello ou, si vous exécutez sans paramètres, vous êtes invité à tooenter les. 

Voici un exemple, vous pouvez exécuter à partir de hello PowerShell invite (mais modifier des points de terminaison hello compte des informations et du portail si nécessaire) :


```
# Install hello AzureRM.Bootstrapper module
Install-Module -Name AzureRm.BootStrapper -Force

# Installs and imports hello API Version Profile required by Azure Stack into hello current PowerShell session.
Use-AzureRmProfile -Profile 2017-03-09-profile
Install-Module -Name AzureStack -RequiredVersion 1.2.10 -Force

# Download hello Azure Stack Tools from GitHub and set hello environment
cd c:\
Invoke-Webrequest https://github.com/Azure/AzureStack-Tools/archive/master.zip -OutFile master.zip
Expand-Archive master.zip -DestinationPath . -Force

# This endpoint may be different for your installation
Import-Module C:\AzureStack-Tools-master\Connect\AzureStack.Connect.psm1
Add-AzureRmEnvironment -Name AzureStackAdmin -ArmEndpoint "https://adminmanagement.local.azurestack.external" 

# For AAD, use hello following
$tenantID = Get-AzsDirectoryTenantID -AADTenantName "<your directory name>" -EnvironmentName AzureStackAdmin

# For ADFS, replace hello previous line with
# $tenantID = Get-AzsDirectoryTenantID -ADFS -EnvironmentName AzureStackAdmin

$vmLocalAdminPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force
$vmLocalAdminCreds = New-Object System.Management.Automation.PSCredential ("mysqlrpadmin", $vmLocalAdminPass)

$AdminPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force
$AdminCreds = New-Object System.Management.Automation.PSCredential ("admin@mydomain.onmicrosoft.com", $AdminPass)

# change this as appropriate
$PfxPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force

# Change directory toohello folder where you extracted hello installation files 
# and adjust hello endpoints
<extracted file directory>\DeployMySQLProvider.ps1 -DirectoryTenantID $tenantID -AzCredential $AdminCreds -VMLocalCredential $vmLocalAdminCreds -ResourceGroupName "MySqlRG" -VmName "MySQLRP" -ArmEndpoint "https://adminmanagement.local.azurestack.external" -TenantArmEndpoint "https://management.local.azurestack.external" -DefaultSSLCertificatePassword $PfxPass -DependencyFilesLocalPath
 ```

### <a name="deploymysqlproviderps1-parameters"></a>Paramètres de DeployMySqlProvider.ps1

Vous pouvez spécifier ces paramètres dans la ligne de commande hello. Si vous n’effectuez pas ou n’importe quel paramètre validation échoue, vous êtes invité tooprovide hello requis ceux.

| Nom du paramètre | Description | Commentaire ou valeur par défaut |
| --- | --- | --- |
| **DirectoryTenantID** | Bonjour Azure ou ID de répertoire AD FS (guid) | _obligatoire_ |
| **ArmEndpoint** | Bonjour Azure pile d’administration Gestionnaire de ressources du point de terminaison Azure | _obligatoire_ |
| **TenantArmEndpoint** | Bonjour Azure pile client Gestionnaire de ressources du point de terminaison Azure | _obligatoire_ |
| **AzCredential** | Références du compte administrateur de Service de pile Azure (hello utilisez même compte que vous avez utilisé pour le déploiement d’Azure pile) | _obligatoire_ |
| **VMLocalCredential** | compte d’administrateur local Hello de fournisseur de ressources MySQL hello machine virtuelle | _obligatoire_ |
| **ResourceGroupName** | Groupe de ressources pour les éléments hello créés par ce script |  _obligatoire_ |
| **VmName** | Nom de l’exploitation de machine virtuelle hello fournisseur de ressources hello |  _obligatoire_ |
| **AcceptLicense** | Ignore Bonjour tooaccept invite Bonjour le licence GPL (http://www.gnu.org/licenses/old-licenses/gpl-2.0.html) | |
| **DependencyFilesLocalPath** | Chemin d’accès tooa partage local contenant [mysql-connector-net-6.9.9.msi](https://dev.mysql.com/get/Downloads/Connector-Net/mysql-connector-net-6.9.9.msi). Si vous les fournissez, les fichiers de certificats doivent être placés dans ce répertoire. | _facultatif_ |
| **DefaultSSLCertificatePassword** | mot de passe Hello certificat .pfx de hello | _obligatoire_ |
| **MaxRetryCount** | Chaque opération est retentée en cas d’échec | 2 |
| **RetryDuration** | Délai d’attente entre les tentatives, en secondes | 120 |
| **Désinstaller** | Supprimer le fournisseur de ressources hello | Non |
| **DebugMode** | Empêche le nettoyage automatique en cas d’échec. | Non |


En fonction des vitesses téléchargement et les performances du système hello, installation peut prendre en l’espace de 20 minutes ou en tant que long en plusieurs heures. Vous devez actualiser le portail d’administration hello si le panneau de MySQLAdapter hello n’est pas disponible.

> [!NOTE]
> Si l’installation de hello prend plus de 90 minutes, elle peut échouer et vous verrez un message d’erreur sur l’écran hello et dans le fichier journal de hello. déploiement de Hello est retentée à partir de hello échouent étape. Les systèmes qui ne respectent pas hello mémoire recommandée et les spécifications principales peuvent ne pas être en mesure de toodeploy hello MySQL RP.


## <a name="provide-capacity-by-connecting-tooa-mysql-hosting-server"></a>Fournir une capacité en vous connectant tooa serveur d’hébergement MySQL

1. Connectez-vous toohello de portail de la pile de Azure en tant qu’un administrateur de service.

2. Cliquez sur **Fournisseurs de ressources** &gt; **MySQLAdapter** &gt; **Serveurs d’hébergement** &gt; **+ Ajouter**.

    Hello **serveurs d’hébergement MySQL** lame est où vous pouvez vous connecter hello fournisseur de ressources MySQL Server tooactual instances de MySQL Server qui servent de hello back-end du fournisseur de ressources.

    ![Serveurs d’hébergement](./media/azure-stack-mysql-rp-deploy/mysql-add-hosting-server-2.png)

3. Remplir le formulaire de hello avec les détails de la connexion de votre instance de serveur MySQL hello. Fournir le nom de domaine complet hello (FQDN) ou une adresse IPv4 valide et pas hello VM nom court. Cette installation ne fournit plus d’instance de MySQL par défaut. Hello taille fournie permet de gérer la capacité de base de données hello fournisseur de ressources hello. Il doit être toohello fermer la capacité physique du serveur de base de données hello.

    > [!NOTE]
    > Tant qu’instance de MySQL hello est accessible par le locataire de hello et administrateur Azure Resource Manager, il peut être placé sous contrôle de fournisseur de ressources hello. instance de MySQL Hello __doit__ être allouées exclusivement toohello RP.

4. Lorsque vous ajoutez des serveurs, vous devez les affecter tooa nouveau ou existante SKU tooallow différentiation entre des offres de service. Par exemple, Impossible de dispose d’une instance de l’entreprise en fournissant la capacité de la base de données et la sauvegarde automatique, de réserver les serveurs hautes performances pour les services, nom de référence (SKU) etc. hello doit refléter les propriétés hello afin que les clients peuvent placer leurs bases de données en conséquence et tous les serveurs d’hébergement dans une référence (SKU) doivent avoir hello les mêmes fonctionnalités.

    ![Créer une référence (SKU) MySQL](./media/azure-stack-mysql-rp-deploy/mysql-new-sku.png)


>[!NOTE]
Références (SKU) peut prendre jusqu'à toobe d’heure tooan visible dans le portail de hello. Impossible de créer une base de données jusqu'à ce que hello que référence (SKU) est créé.


## <a name="create-your-first-mysql-database-tootest-your-deployment"></a>Créer votre première tootest de base de données MySQL à votre déploiement


1. Se connecter toohello portail de la pile de Azure en tant qu’administrateur de service.

2. Cliquez sur hello **+ nouveau** bouton &gt; **données + stockage** &gt; **base de données MySQL (version préliminaire)**.

3. Renseignez le formulaire hello avec les détails de base de données hello.

    ![Créer une base de données MySQL test](./media/azure-stack-mysql-rp-deploy/mysql-create-db.png)

4. Sélectionnez une référence (SKU).

    ![Sélectionner une référence](./media/azure-stack-mysql-rp-deploy/mysql-select-a-sku.png)

5. Créez un paramètre de connexion. paramètre de connexion Hello peut être réutilisé ou créer une nouvelle. Nom d’utilisateur hello et le mot de passe pour la base de données hello contient.

    ![Créer une connexion de base de données](./media/azure-stack-mysql-rp-deploy/create-new-login.png)

    chaîne de connexion Hello inclut le nom de serveur de base de données réels hello. Copier à partir du portail de hello.

    ![Obtenir la chaîne de connexion hello pour la base de données MySQL hello](./media/azure-stack-mysql-rp-deploy/mysql-db-created.png)

> [!NOTE]
> Hello hello des noms d’utilisateur ne peut pas dépasser 32 caractères avec MySQL 5.7 ou 16 caractères dans les éditions antérieures. Il s’agit d’une limitation des implémentations de MySQL hello.


## <a name="add-capacity"></a>Ajouter de la capacité

Augmenter la capacité en ajoutant des serveurs MySQL dans le portail d’Azure pile hello. Si vous le souhaitez toouse une autre instance de MySQL, cliquez sur **fournisseurs de ressources** &gt; **MySQLAdapter** &gt; **serveurs d’hébergement MySQL** &gt; **+ Ajouter**.


## <a name="making-mysql-databases-available-tootenants"></a>Rendre les bases de données MySQL tootenants disponibles
Créer des plans et des offres toomake MySQL de bases de données disponibles pour les locataires. Ajouter un service de Microsoft.MySqlAdapter hello, ajouter un quota, un etc..

![Créer des plans et des offres tooinclude bases de données](./media/azure-stack-mysql-rp-deploy/mysql-new-plan.png)

## <a name="removing-hello-mysql-adapter-resource-provider"></a>Suppression de hello fournisseur de ressources MySQL adaptateur

fournisseur de ressources tooremove hello, il est essentiel toofirst supprimer toutes les dépendances.

1. Assurez-vous de qu'avoir hello d’origine package de déploiement que vous avez téléchargé pour cette version du fournisseur de ressources de hello.

2. Toutes les bases de données client doivent être supprimés à partir du fournisseur de ressources hello (cela ne supprimera pas les données de salutation). Doit être effectué par les locataires hello eux-mêmes.

3. Les locataires doivent annuler l’inscription à partir de l’espace de noms hello.

4. Administrateur doit supprimer hello hébergeant des serveurs à partir de hello MySQL adaptateur

5. Administrateur doit supprimer tous les plans qui font référence à hello MySQL adaptateur.

6. Administrateur doit supprimer n’importe quel toohello associé de quotas MySQL adaptateur.

7. Réexécutez le script de déploiement hello dans hello - désinstallation de paramètre, les points de terminaison Azure Resource Manager, les DirectoryTenantID et les informations d’identification pour le compte d’administrateur de service de hello.




## <a name="next-steps"></a>Étapes suivantes


Essayez d’autres [services PaaS](azure-stack-tools-paas-services.md) comme hello [fournisseur de ressources SQL Server](azure-stack-sql-resource-provider-deploy.md) et hello [fournisseur de ressources des Services d’application](azure-stack-app-service-overview.md).
