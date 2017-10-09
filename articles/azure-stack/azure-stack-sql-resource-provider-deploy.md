---
title: "aaaUsing SQL des bases de données sur la pile de Azure | Documents Microsoft"
description: "Découvrez comment vous pouvez déployer des bases de données SQL en tant que service sur la pile d’Azure et adaptateur fournisseur de ressources hello étapes rapides toodeploy hello SQL Server"
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
ms.openlocfilehash: 01418ce7cd708ca8f9e302d6bcd2a43ad33df93f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-sql-databases-on-microsoft-azure-stack"></a>Utiliser des bases de données SQL sur Microsoft Azure Stack


Utilisez hello SQL Server resource fournisseur adaptateur tooexpose bases de données SQL en tant que service de pile de Azure. Une fois que vous installez le fournisseur de ressources hello et connectez tooone ou autres instances de SQL Server, vous et vos utilisateurs peuvent créer des bases de données pour les applications cloud en mode natif, les sites Web basés sur SQL et les charges de travail qui sont basés sur SQL sans avoir tooprovision une machine virtuelle machine (VM) qui héberge SQL Server chaque fois.

fournisseur de ressources Hello ne prend pas en charge toutes les fonctionnalités de gestion de la base de données hello de [base de données SQL Azure](https://azure.microsoft.com/services/sql-database/). Par exemple, les pools de bases de données élastiques et performances de base de données tooscale hello capacité ne sont pas pris en charge. Hello API n’est pas compatible avec la base de données SQL.


## <a name="sql-server-resource-provider-adapter-architecture"></a>Architecture de l’adaptateur de fournisseur de ressource SQL Server
fournisseur de ressources Hello n’est pas basé sur, ni offre toutes les fonctionnalités de gestion de la base de données hello de base de données SQL Azure. Par exemple, les pools de bases de données élastiques et performances de base de données toodial hello capacité haut et bas automatiquement ne sont pas disponibles. Toutefois, hello ressource fournisseur prend en charge similaire créer, lire, mettre à jour et supprimer (CRUD) des opérations.

fournisseur de ressources Hello est constitué de trois composants :

- **adaptateur de fournisseur Hello SQL ressource VM**, qui est un ordinateur virtuel de Windows exécutant les services de fournisseur hello.
- **fournisseur de ressources Hello lui-même**, qui traite les demandes d’approvisionnement et expose les ressources de base de données.
- **Les serveurs qui hébergent SQL Server**, qui offrent de la capacité pour les bases de données, et qui sont appelés « serveurs d’hébergement ». 

Cette version ne crée plus d’instance SQL. Vous devez créer un (ou plusieurs) ou fournir un accès tooexternal les instances de SQL. Il existe un nombre d’options de tooyou disponibles, y compris les modèles Bonjour [galerie de démarrage rapide Azure pile](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/mysql-standalone-server-windows) et d’éléments du Marketplace. 

>[!NOTE]
Si vous avez téléchargé tous les éléments SQL Marketplace, assurez-vous que vous téléchargez également hello IaaS Extension de SQL ou ces ne déploiement pas.


## <a name="deploy-hello-resource-provider"></a>Déployer le fournisseur de ressources hello

1. Si vous ne le n'avez pas déjà fait, inscrire votre kit de développement et de télécharger une image de Windows Server 2016 EVAL hello téléchargeable via la gestion du Marketplace. Vous pouvez également utiliser un script toocreate un [image de Windows Server 2016](https://docs.microsoft.com/azure/azure-stack/azure-stack-add-default-image). exécution de Hello .NET 3.5 n’est plus nécessaire.

2. [Télécharger le fichier de fichiers binaires du fournisseur de ressources hello SQL](https://aka.ms/azurestacksqlrp) et extrayez-le sur l’hôte de kit de développement hello.

3. Connectez-vous à hôte de kit de développement toohello et extraire hello répertoire temporaire de tooa de fichiers de programme d’installation de SQL RP.

4. certificat racine de pile de Azure Hello est récupérée et un certificat auto-signé est créé dans le cadre de ce processus. 

    __Facultatif :__ si vous avez besoin de tooprovide votre propre, préparer les certificats hello et tooa répertoire local si vous le souhaitez toocustomize les certificats hello (script d’installation toohello passé). Vous devez hello certificats suivants :

    a. Un certificat générique pour *.dbadapter.\<région\>.\<fqdn_externe\>. Ce certificat doit être approuvé, tel qu’est émise par une autorité de certification (autrement dit, chaîne hello d’approbation doit exister sans exiger de certificats intermédiaires). (Un certificat de site unique utilisable avec nom VM explicite de hello, que vous fournissez lors de l’installation.)

    b. Hello certificat utilisé par hello Azure Resource Manager pour votre instance de la pile de Azure. S’il n’est pas trouvé, certificat hello est récupérée.


5. Ouvrir un **nouvelle** élevé PowerShell console et de modifier le répertoire toohello où vous avez extrait les fichiers hello. Utilisez une nouvelle fenêtre tooavoid les problèmes qui peuvent survenir à partir des modules PowerShell incorrects déjà chargés sur le système de hello.

6. Si vous avez installé des versions des modules AzureStack PowerShell autres que 1.2.9 ou 1.2.10 hello Azure Resource Manager, vous serez invité à tooremove les ou hello installation ne sera pas effectuée. Cela inclut les versions 1.3 ou ultérieures.

7. Exécutez hello DeploySqlProvider.ps1 script avec des paramètres de hello répertoriée ci-dessous.

script de Hello procède comme suit :

* Si nécessaire, téléchargement d’une version compatible d’Azure PowerShell.
* Télécharger les certificats hello et autres comptes de stockage tooa artefacts sur votre pile Azure.
* Publier des packages de la galerie afin que vous pouvez déployer des bases de données SQL via la galerie de hello.
* Déployer un ordinateur virtuel à l’aide d’image hello Windows Server 2016 créé à l’étape 1 et installer le fournisseur de ressources hello.
* Inscrire un enregistrement DNS local qui mappe le fournisseur de ressources tooyour machine virtuelle.
* Inscrire votre fournisseur de ressources par hello local Azure Resource Manager (client et administrateur).

> [!NOTE]
> Si l’installation de hello prend plus de 90 minutes, il risque d’échouer et vous voyez un message d’erreur sur l’écran hello et dans le fichier journal de hello, mais déploiement de hello est retentée à partir de hello échouent étape. Les systèmes qui ne respectent pas hello mémoire recommandée et les spécifications principales peuvent ne pas être en mesure de toodeploy hello SQL RP.
>

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
$vmLocalAdminCreds = New-Object System.Management.Automation.PSCredential ("sqlrpadmin", $vmLocalAdminPass)

$AdminPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force
$AdminCreds = New-Object System.Management.Automation.PSCredential ("admin@mydomain.onmicrosoft.com", $AdminPass)

# change this as appropriate
$PfxPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force

# Change directory toohello folder where you extracted hello installation files 
# and adjust hello endpoints
<extracted file directory>\DeploySQLProvider.ps1 -DirectoryTenantID $tenantID -AzCredential $AdminCreds -VMLocalCredential $vmLocalAdminCreds -ResourceGroupName "SqlRPRG" -VmName "SqlVM" -ArmEndpoint "https://adminmanagement.local.azurestack.external" -TenantArmEndpoint "https://management.local.azurestack.external" -DefaultSSLCertificatePassword $PfxPass
 ```

### <a name="deploysqlproviderps1-parameters"></a>Paramètres de DeploySqlProvider.ps1
Vous pouvez spécifier ces paramètres dans la ligne de commande hello. Si vous n’effectuez pas ou n’importe quel paramètre validation échoue, vous êtes invité tooprovide hello requis ceux.

| Nom du paramètre | Description | Commentaire ou valeur par défaut |
| --- | --- | --- |
| **DirectoryTenantID** | Bonjour Azure ou ID de répertoire AD FS (guid). | _obligatoire_ |
| **AzCredential** | Fournir des informations d’identification de hello pour hello compte d’administrateur de Service de pile Azure. Vous devez utiliser hello même les informations d’identification que vous avez utilisé pour le déploiement d’Azure pile). | _obligatoire_ |
| **VMLocalCredential** | Définir les informations d’identification de hello pour le compte d’administrateur local hello de fournisseur de ressources SQL hello machine virtuelle. Ce mot de passe est également utilisé pour hello SQL **sa** compte. | _obligatoire_ |
| **ResourceGroupName** | Définissez un nom pour un groupe de ressources dans lequel les éléments créés par ce script seront stockés. Par exemple, *SqlRPRG*. |  _obligatoire_ |
| **VmName** | Définir le nom hello de machine virtuelle de hello sur le fournisseur de ressources tooinstall hello. Par exemple, *SqlVM*. |  _obligatoire_ |
| **DependencyFilesLocalPath** | Vos fichiers de certificats doivent également être placés dans ce répertoire. | _facultatif_ |
| **DefaultSSLCertificatePassword** | mot de passe Hello certificat .pfx de hello | _obligatoire_ |
| **MaxRetryCount** | Définir le nombre de fois où vous voulez que tooretry chaque opération s’il existe un échec.| 2 |
| **RetryDuration** | Définir le délai d’attente hello entre les nouvelles tentatives, en secondes. | 120 |
| **Désinstaller** | Supprimer le fournisseur de ressources hello et toutes les ressources associées (voir les remarques ci-dessous) | Non |
| **DebugMode** | Empêche le nettoyage automatique en cas d’échec. | Non |


## <a name="verify-hello-deployment-using-hello-azure-stack-portal"></a>Vérifier le déploiement hello à l’aide de hello Azure pile portail

> [!NOTE]
>  Après l’achèvement du script d’installation hello, vous devez le panneau admin hello toorefresh hello toosee portail.


1. Sur le bureau de machine virtuelle de Console hello, cliquez sur **Microsoft Azure pile Portal** et connectez-vous au portail toohello en tant qu’administrateur de service hello.

2. Vérifiez que le déploiement de hello a réussi. Cliquez sur **groupes de ressources** &gt; cliquez sur le groupe de ressources hello utilisé et assurez-vous que cette partie d’essentials hello de lectures de panneau (moitié supérieure) hello  **_date_ (réussite)**.

      ![Vérifier le déploiement de hello SQL RP](./media/azure-stack-sql-rp-deploy/sqlrp-verify.png)


## <a name="provide-capacity-by-connecting-tooa-hosting-sql-server"></a>Fournir une capacité en vous connectant tooa hébergeant SQL server

1. Connectez-vous toohello de portail d’administration Azure pile en tant qu’un administrateur de service

2. Créez une machine virtuelle SQL, sauf si vous en avez déjà une disponible. La Gestion de la Place de marché offre certaines options pour le déploiement de machines virtuelles SQL.

3. Cliquez sur **Fournisseurs de ressources** &gt; **SQLAdapter** &gt; **Serveurs d’hébergement** &gt; **+Ajouter**.

    Hello **serveurs d’hébergement SQL** lame est où vous pouvez vous connecter hello fournisseur de ressources SQL Server tooactual instances de SQL Server qui servent de hello back-end du fournisseur de ressources.

    ![Serveurs d’hébergement](./media/azure-stack-sql-rp-deploy/sqlrp-hostingserver.PNG)

4. Remplir le formulaire de hello avec les détails de la connexion hello de votre instance de SQL Server.

    ![Nouveau serveur d’hébergement](./media/azure-stack-sql-rp-deploy/sqlrp-newhostingserver.PNG)

    > [!NOTE]
    > Tant que l’instance SQL hello est accessible par le locataire de hello et administrateur Azure Resource Manager, il peut être placé sous contrôle de fournisseur de ressources hello. l’instance SQL Hello __doit__ être allouées exclusivement toohello RP.

5. Lorsque vous ajoutez des serveurs, vous devez les affecter tooa nouveau ou existants SKU toodifferentiate offres de service. Par exemple, vous peut avoir qu’une instance de SQL Enterprise en fournissant la capacité de la base de données et la sauvegarde automatique, réserver serveurs hautes performances pour les services, nom de référence (SKU) etc. hello doit refléter les propriétés hello afin que les clients peuvent placer leurs bases de données en conséquence et tous les serveurs d’hébergement dans une référence (SKU) doivent avoir hello les mêmes fonctionnalités.

    Exemple :

    ![Références (SKU)](./media/azure-stack-sql-rp-deploy/sqlrp-newsku.png)

>[!NOTE]
Références (SKU) peut prendre jusqu'à toobe d’heure tooan visible dans le portail de hello. Impossible de créer une base de données jusqu'à ce que hello que référence (SKU) est créé.


## <a name="create-your-first-sql-database-tootest-your-deployment"></a>Créer votre première tootest de base de données SQL de votre déploiement

1. Se connecter toohello portail d’administration Azure pile en tant qu’administrateur de service.

2. Cliquez sur **+ Nouveau** &gt; **Données + stockage** &gt; **Base de données SQL Server (préversion)** &gt; **Ajouter**.

3. Renseignez le formulaire hello avec les détails de la base de données, y compris un **nom de la base de données**, **taille maximale**, et la modification hello autres paramètres si nécessaire. Vous êtes invité à toopick une référence (SKU) pour votre base de données. Lorsque les serveurs d’hébergement sont ajoutés, ils sont attribués à une référence (SKU) et bases de données sont créés dans ce pool de serveurs qui composent hello SKU d’hébergement.

    ![Nouvelle base de données](./media/azure-stack-sql-rp-deploy/newsqldb.png)


4. Renseignez hello paramètres de connexion : **connexion de base de données**, et **mot de passe**. Il s’agit d’une information d’identification de l’authentification SQL est créée pour votre accès toothis base de données uniquement. nom d’utilisateur Hello doit être globalement unique. Créez un paramètre de connexion ou sélectionnez-en un qui existe déjà. Vous pouvez réutiliser les paramètres de connexion pour les autres bases de données à l’aide de hello même référence SKU.

    ![Créer une connexion de base de données](./media/azure-stack-sql-rp-deploy/create-new-login.png)


5. Soumettre le formulaire de hello et attendez hello déploiement toocomplete.

    Dans le panneau résultant de hello, notez le champ de « Chaîne de connexion » hello. Vous pouvez utiliser cette chaîne dans toute application qui nécessite un accès à SQL Server (par exemple, une application web) dans Azure Stack.

    ![Récupérer la chaîne de connexion hello](./media/azure-stack-sql-rp-deploy/sql-db-settings.png)

## <a name="add-capacity"></a>Ajouter de la capacité

Augmenter la capacité en ajoutant des hôtes SQL supplémentaires dans le portail d’Azure pile hello et les associer à une référence (SKU) approprié. Si vous le souhaitez toouse une autre instance de SQL au lieu de hello celle installée sur le fournisseur hello machine virtuelle, cliquez sur **fournisseurs de ressources** &gt; **SQLAdapter** &gt; **SQL d’hébergement Serveurs** &gt; **+ ajouter**.

## <a name="making-sql-databases-available-tootenants"></a>Rendre les bases de données SQL tootenants disponibles

Créer des plans et des offres toomake bases de données SQL disponibles pour les locataires. Vous devez créer un plan, ajouter hello Microsoft.SqlAdapter service toohello plan et ajouter un Quota existant ou créez-en un. Si vous créez un quota, vous pouvez spécifier le locataire de hello capacité tooallow hello.
    ![Créer des plans et des offres tooinclude bases de données](./media/azure-stack-sql-rp-deploy/sqlrp-newplan.png)

## <a name="tenant-usage-of-hello-resource-provider"></a>Utilisation de clients de hello fournisseur de ressources

Libre service les bases de données sont fournies via l’utilisation du portail locataire hello.

## <a name="removing-hello-sql-adapter-resource-provider"></a>Suppression de hello fournisseur de ressources de l’adaptateur SQL

Dans le fournisseur de ressources tooremove hello ordre, il est essentiel toofirst supprimer toutes les dépendances.

1. Assurez-vous de qu'avoir hello d’origine package de déploiement que vous avez téléchargé pour cette version du fournisseur de ressources de hello.

2. Toutes les bases de données client doivent être supprimés à partir du fournisseur de ressources hello (cela ne supprimera pas les données de salutation). Doit être effectué par les locataires hello eux-mêmes.

3. Administrateur doit supprimer hello hébergeant des serveurs à partir de hello adaptateur SQL

4. Administrateur doit supprimer tous les plans qui font référence à hello adaptateur SQL.

5. Administrateur doit supprimer toutes les références (SKU) et les quotas associés toohello adaptateur SQL.

6. Réexécutez le script de déploiement hello dans hello - désinstallation de paramètre, les points de terminaison Azure Resource Manager, les DirectoryTenantID et les informations d’identification pour le compte d’administrateur de service de hello.



## <a name="next-steps"></a>Étapes suivantes


Essayez d’autres [services PaaS](azure-stack-tools-paas-services.md) comme hello [fournisseur de ressources MySQL Server](azure-stack-mysql-resource-provider-deploy.md) et hello [fournisseur de ressources des Services d’application](azure-stack-app-service-overview.md).
