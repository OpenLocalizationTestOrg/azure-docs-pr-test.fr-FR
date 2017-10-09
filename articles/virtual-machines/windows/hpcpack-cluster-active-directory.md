---
title: aaaHPC Pack cluster avec Azure Active Directory | Documents Microsoft
description: "Découvrez comment toointegrate une 2016 de Pack HPC cluster dans Azure avec Azure Active Directory"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
ms.assetid: 9edf9559-db02-438b-8268-a6cba7b5c8b7
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 11/14/2016
ms.author: danlep
ms.openlocfilehash: 0806e544a468e27ca0567e18c55554811584fbc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-hpc-pack-cluster-in-azure-using-azure-active-directory"></a>Gérer un cluster HPC Pack dans Azure avec Azure Active Directory
[Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) prend en charge l’intégration avec [Azure Active Directory](../../active-directory/index.md) (Azure AD) pour les administrateurs qui déploient un cluster HPC Pack dans Azure.



Suivez les étapes de hello dans cet article pour hello suivant de tâches de niveau élevés : 
* Intégrer manuellement votre cluster HPC Pack avec votre locataire Azure AD
* Gérer et planifier des travaux dans votre cluster HPC Pack dans Azure 

Intégration d’une solution de cluster HPC Pack à Azure AD suit les étapes standard toointegrate autres applications et services. Cet article suppose que vous êtes familiarisé avec la gestion des utilisateurs de base dans Azure AD. Pour plus d’informations et d’arrière-plan, consultez hello [documentation Azure Active Directory](../../active-directory/index.md) et hello suivant la section.

## <a name="benefits-of-integration"></a>Avantages de l’intégration


Azure Active Directory (Azure AD) est une architecture mutualisé nuage annuaire et identité de service de gestion qui fournit l’accès de l’authentification unique (SSO) toocloud solutions.

Intégration d’un cluster HPC Pack avec Azure AD peut vous aider à atteindre hello suivant des objectifs :

* Supprimez contrôleur de domaine Active Directory hello traditionnel de cluster HPC Pack de hello. Cela peut permettre de réduire les coûts de hello de gestion de cluster de hello si cela n’est pas nécessaire pour votre entreprise et des processus de déploiement accélération hello.
* Exploiter hello avantages mis par Azure AD suivants :
    *   Authentification unique 
    *   À l’aide d’une identité Active Directory locale pour un cluster HPC Pack hello dans Azure 

    ![Environnement Azure Active Directory](./media/hpcpack-cluster-active-directory/aad.png)


## <a name="prerequisites"></a>Composants requis
* **Cluster HPC Pack 2016 déployé dans des machines virtuelles** : pour connaître les étapes, consultez [Déployer un cluster HPC Pack 2016 dans Azure](hpcpack-2016-cluster.md). Vous devez le nom DNS hello du nœud principal hello et les informations d’identification de hello d’un administrateur de cluster pour effectuer les étapes hello dans cet article.

  > [!NOTE]
  > L’intégration d’Azure Active Directory n’est pas prise en charge dans les versions de HPC Pack antérieures au HPC Pack 2016.



* **Ordinateur client** -vous avez besoin d’un Windows ou Windows Server client ordinateur trop exécuter des utilitaires clients HPC Pack. Si vous souhaitez uniquement le portail web de toouse hello HPC Pack ou les travaux de toosubmit d’API REST, vous pouvez utiliser n’importe quel ordinateur client de votre choix.

* **Utilitaires clients HPC Pack** -installer les utilitaires clients HPC Pack hello sur l’ordinateur client de hello, à l’aide du package d’installation gratuit hello disponible à partir de hello Microsoft Download Center.


## <a name="step-1-register-hello-hpc-cluster-server-with-your-azure-ad-tenant"></a>Étape 1 : Inscrire un serveur de cluster HPC hello avec votre client Azure AD
1. Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com).
2. Cliquez sur **Active Directory** dans hello du menu de gauche, puis cliquez sur répertoire hello dans votre abonnement. Vous devez disposer de ressources de tooaccess d’autorisation dans le répertoire de hello.
3. Cliquez sur **Utilisateurs** et vérifiez que des comptes utilisateur ont déjà été créés ou configurés.
4. Cliquez sur **Applications** > **Ajouter**, puis cliquez sur **Ajouter une application développée par mon organisation**. Entrez hello informations dans l’Assistant de hello suivantes :
    * **Nom** : HPCPackClusterServer.
    * **Type** : sélectionnez **Application web et/ou API web**.
    * **URL de l’authentification**hello - URL de base pour l’exemple hello, qui est par défaut`https://hpcserver`
    * **URI ID d’application** - `https://<Directory_name>/<application_name>`. Remplacez `<Directory_name`> avec le nom complet de votre client Azure AD, par exemple, de hello `hpclocal.onmicrosoft.com`et remplacez `<application_name>` avec hello nom vous avez choisi précédemment.

5. Une fois l’application hello est ajoutée, cliquez sur **configurer**. Configurer les propriétés suivantes de hello :
    * Sélectionnez **Oui** pour **Application mutualisée**.
    * Sélectionnez **Oui** pour **utilisateur attribution obligatoire tooaccess application**.

6. Cliquez sur **Enregistrer**. Une fois l’enregistrement terminé, cliquez sur **Gérer le manifeste**. Cette action permet de télécharger le fichier JSON du manifeste de votre application. Manifeste de hello téléchargé modifier en recherchant hello `appRoles` définition et l’ajout de hello suivant le rôle d’application :
    ```json
    "appRoles": [
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "displayName": "HpcAdminMirror",
        "id": "61e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "description": "HpcAdminMirror",
        "value": "HpcAdminMirror"
        },
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "description": "HpcUsers",
        "displayName": "HpcUsers",
        "id": "91e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "value": "HpcUsers"
        }
    ],
    ```
7. Enregistrez le fichier de hello. Puis, dans le portail hello, cliquez sur **gérer manifeste** > **télécharger le manifeste**. Vous pouvez ensuite télécharger le manifeste de hello modifié.
8. Cliquez sur **Utilisateurs**, sélectionnez un utilisateur, puis cliquez sur **Affecter**. Attribuez l’un des utilisateurs toohello hello rôles disponibles (HpcUsers ou HpcAdminMirror). Répétez cette étape avec des utilisateurs supplémentaires dans le répertoire de hello. Pour plus d’informations générales sur les utilisateurs de cluster, consultez [Gestion des utilisateurs de clusters](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx).

   > [!NOTE] 
   > les utilisateurs toomanage, nous recommandons d’utiliser le panneau d’aperçu hello Azure Active Directory Bonjour [portail Azure](https://portal.azure.com).
   >


## <a name="step-2-register-hello-hpc-cluster-client-with-your-azure-ad-tenant"></a>Étape 2 : Inscrire un client de cluster HPC hello avec votre client Azure AD

1. Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com).
2. Cliquez sur **Active Directory** dans hello du menu de gauche, puis cliquez sur répertoire hello dans votre abonnement. Vous devez disposer de ressources de tooaccess d’autorisation dans le répertoire de hello.
3. Cliquez sur **Applications** > **Ajouter**, puis cliquez sur **Ajouter une application développée par mon organisation**. Entrez hello informations dans l’Assistant de hello suivantes :

    * **Nom** : HPCPackClusterClient.
    * **Type** : sélectionnez **Application cliente native**
    * **URI de redirection** - `http://hpcclient`

4. Une fois l’application hello est ajoutée, cliquez sur **configurer**. Hello de copie **ID Client** valeur et l’enregistrer. Vous en aurez besoin plus tard lors de la configuration de votre application.

5. Dans **autorisations tooother applications**, cliquez sur **ajouter une Application**. Rechercher et ajouter une application de HpcPackClusterServer hello (créée à l’étape 1).

6. Bonjour **autorisations déléguées** liste déroulante, sélectionnez **accès HpcClusterServer**. Cliquez ensuite sur **Enregistrer**.


## <a name="step-3-configure-hello-hpc-cluster"></a>Étape 3 : Configurer le cluster HPC de hello

1. Se connecter toohello HPC Pack 2016 le nœud principal dans Azure.

2. Démarrez PowerShell HPC.

3. Exécutez hello de commande suivante :

    ```powershell

    Set-HpcClusterRegistry -SupportAAD true -AADInstance https://login.microsoftonline.com/ -AADAppName HpcClusterServer -AADTenant <your AAD tenant name> -AADClientAppId <client ID> -AADClientAppRedirectUri http://hpcclient
    ```
    où

    * `AADTenant`Spécifie le nom de client Azure AD hello, tel que`hpclocal.onmicrosoft.com`
    * `AADClientAppId`Spécifie l’ID de client hello pour l’application hello créée à l’étape 2.

4. Redémarrez le service de HpcSchedulerStateful hello.

    Dans un cluster avec plusieurs nœuds principal, vous pouvez exécuter hello suivant de commandes PowerShell de hello du nœud principal tooswitch hello réplica principal pour le service de HpcSchedulerStateful hello :

    ```powershell
    Connect-ServiceFabricCluster

    Move-ServiceFabricPrimaryReplica –ServiceName “fabric:/HpcApplication/SchedulerStatefulService”

    ```

## <a name="step-4-manage-and-submit-jobs-from-hello-client"></a>Étape 4 : Gérer et envoyer des travaux à partir du client de hello

tooinstall les utilitaires clients HPC Pack hello sur votre ordinateur, téléchargez les fichiers d’installation de HPC Pack 2016 (installation complète) à partir de hello Microsoft Download Center. Lorsque vous commencez l’installation de hello, choisissez option d’installation de hello pour hello **utilitaires clients HPC Pack**.

ordinateur client de hello tooprepare, installez-en hello utilisé au cours de [le programme d’installation HPC cluster](hpcpack-2016-cluster.md) sur l’ordinateur client de hello. Windows standards d’utilisation de certificats gestion procédures tooinstall hello certificat public toohello **certificats-utilisateur actuel** > **autorités de Certification racines de confiance** stocker. 

Vous pouvez maintenant exécuter des commandes de HPC Pack hello ou utilisez hello HPC Pack travail manager GUI toosubmit et gérer des travaux de cluster à l’aide du compte de hello Azure AD. Pour les options d’envoi de travail, consultez [de cluster HPC d’envoyer des travaux tooan HPC Pack dans Azure](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster).

> [!NOTE]
> Lorsque vous essayez de cluster HPC Pack toohello de tooconnect dans Azure pour hello première fois, une fenêtre contextuelle s’affiche. Entrez votre toolog d’informations d’identification Azure AD dans. jeton de Hello est ensuite mis en cache. Ultérieur cluster toohello de connexions dans Azure utilisation hello mis en cache le jeton, sauf si des modifications de l’authentification ou hello mis en cache est désactivé.
>
  
Par exemple, après avoir effectué les étapes précédentes hello, vous pouvez interroger pour les travaux à partir d’un client local comme suit :

```powershell 
Get-HpcJob –State All –Scheduler https://<Azure load balancer DNS name> -Owner <Azure AD account>
```

## <a name="useful-cmdlets-for-job-submission-with-azure-ad-integration"></a>Applets de commande utiles pour l’envoi de travaux avec l’intégration Azure AD 

### <a name="manage-hello-local-token-cache"></a>Gérer le cache de jetons local hello

HPC Pack 2016 fournit deux nouvelles applets de commande PowerShell HPC toomanage hello local du cache de jetons. Ces applets de commande sont utiles pour envoyer des travaux en mode non interactif. Consultez hello l’exemple suivant :

```powershell
Remove-HpcTokenCache

$SecurePassword = "<password>" | ConvertTo-SecureString -AsPlainText -Force

Set-HpcTokenCache -UserName <AADUsername> -Password $SecurePassword -scheduler https://<Azure load balancer DNS name> 
```

### <a name="set-hello-credentials-for-submitting-jobs-using-hello-azure-ad-account"></a>Définir les informations d’identification hello pour soumettre des tâches à l’aide du compte de hello Azure AD 

Vous pouvez être amené travail hello toorun utilisateur de cluster HPC hello (pour un cluster HPC appartenant au domaine, exécuter en tant qu’un utilisateur de domaine, pour un cluster HPC non joints au domaine, exécuter en tant qu’un utilisateur local sur le nœud principal de hello).

1. Utilisez hello suit les informations d’identification de commandes tooset hello :

    ```powershell
    $localUser = “<username>”

    $localUserPassword=”<password>”

    $secpasswd = ConvertTo-SecureString $localUserPassword -AsPlainText -Force

    $mycreds = New-Object System.Management.Automation.PSCredential ($localUser, $secpasswd)

    Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name>
    ```

2. Puis soumettez le travail de hello comme suit. tâche du Hello s’exécute sous $localUser sur les nœuds de calcul hello.

    ```powershell
    $emptycreds = New-Object System.Management.Automation.PSCredential ($localUser, (new-object System.Security.SecureString))
    ...
    $job = New-HpcJob –Scheduler https://<Azure load balancer DNS name>

    Add-HpcTask -Job $job -CommandLine "ping localhost" -Scheduler https://<Azure load balancer DNS name>

    Submit-HpcJob -Job $job -Scheduler https://<Azure load balancer DNS name> -Credential $emptycreds
    ```
    
   Si `–Credential` n’est pas spécifié avec `Submit-HpcJob`, hello tâche s’exécute sous un utilisateur mappé local comme hello compte Azure AD. (cluster HPC de hello crée un utilisateur local avec hello comme hello tâche hello de Azure AD compte toorun du même nom.)
    
3. Définir les données étendues pour hello compte Azure AD. Cela est utile lors de l’exécution d’un travail MPI sur des nœuds Linux à l’aide du compte de hello Azure AD.

   * Définir les données étendues pour hello compte Azure AD elle-même

      ```powershell
      Set-HpcJobCredential -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data> -AadUser
      ```
      
   * Définir les données étendues et exécuter en tant qu’utilisateur du cluster HPC
   
      ```powershell
      Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data>
      ```

