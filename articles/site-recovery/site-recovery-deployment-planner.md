---
title: "planification de déploiement de Site Recovery aaaAzure pour VMware pour Azure | Documents Microsoft"
description: "Il s’agit de guide de l’utilisateur planner déploiement Azure Site Recovery hello."
services: site-recovery
documentationcenter: 
author: nsoneji
manager: garavd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 08/28/2017
ms.author: nisoneji
ms.openlocfilehash: a8c13cd47850575769e0186528807bc525bdeec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-site-recovery-deployment-planner"></a>Azure Site Recovery deployment planner
Cet article est un guide d’utilisateur de planification de déploiement Azure Site Recovery hello pour les déploiements de production de VMware à Azure.

## <a name="overview"></a>Vue d'ensemble

Avant de commencer la protection des machines virtuelles de VMware (VM) à l’aide de Site Recovery, allouer suffisamment de bande passante, en fonction de votre taux de modification de données quotidienne, toomeet de votre objectif de point de récupération souhaité (RPO). Être toodeploy vraiment hello bon nombre de serveurs de configuration et les processus serveurs locaux.

Vous devez également le type approprié de toocreate hello et le nombre de comptes de stockage Azure cible. Vous créez des comptes de stockage standard ou premium, en tenant compte de la croissance de vos serveurs de production sources en raison d’une utilisation accrue au fil du temps. Vous choisissez le type de stockage hello par machine virtuelle, en fonction des caractéristiques de charge de travail (par exemple, des opérations de lecture/écriture d’e/s par s ou évolution des données) et limite de la récupération de Site.

Aperçu public du module de déploiement Hello Site Recovery est un outil de ligne de commande qui est actuellement disponible uniquement pour le scénario de VMware à Azure hello. Vous pouvez à distance à l’aide de cet outil (avec aucun impact sur la production quelque) toounderstand hello de bande passante en matière de stockage Azure pour la réussite de la réplication de profil vos machines virtuelles VMware et test de basculement. Vous pouvez exécuter l’outil de hello sans installer n’importe quel Site Recovery composants locaux. Toutefois, tooget précis obtenu des résultats de débit, nous vous conseillons d’exécuter le Planificateur de hello sur un serveur Windows qui répond aux exigences minimales hello hello récupération de Site du serveur de configuration que vous devez éventuellement toodeploy comme l’une des premières étapes de hello dans le déploiement de production.

outil de Hello fournit hello les détails suivants :

**Évaluation de la compatibilité**

* Une évaluation de l’éligibilité de la machine virtuelle en fonction du nombre de disques, de la taille du disque, des E/S par seconde, de l’activité et du type de démarrage (EFI/BIOS)
* bande passante réseau Hello estimé qui est requis pour la réplication delta

**Besoin de bande passante réseau et évaluation de RPO**

* bande passante réseau Hello estimé qui est requis pour la réplication delta
* débit Hello qu’obtiennent à partir de récupération de Site local tooAzure
* nombre de Hello de machines virtuelles toobatch, en fonction de hello estimé réplication initiale de la bande passante toocomplete dans un délai donné

**Exigences de l’infrastructure Azure**

* spécification de type (compte de stockage standard ou premium) de stockage de Hello pour chaque machine virtuelle
* Nombre total de Hello de toobe de comptes de stockage standard et premium définie pour la réplication
* Suggestions d’affectation de noms pour les comptes de stockage en fonction des conseils liés au Stockage Azure
* sélection élective de compte de stockage Hello pour toutes les machines virtuelles
* nombre de Hello de cœurs Azure toobe configurer avant le basculement de test ou sur l’abonnement de hello
* Hello recommandée de machine virtuelle Azure de taille pour chaque machine virtuelle sur site

**Exigences de l’infrastructure locale**
* Hello nombre requis de serveurs de configuration et toobe de serveurs de processus déployé localement

>[!IMPORTANT]
>
>Étant donné que l’utilisation est probablement tooincrease au fil du temps, toutes les hello outil précédent, les calculs sont effectués en supposant que d’un facteur de croissance de 30 pour cent de caractéristiques de charge de travail et à l’aide d’une valeur du 95ème centile de hello toutes les métriques de profilage (évolution d’IOPS, de lecture/écriture et donc les deux sens). Ces deux éléments (facteur de croissance et calcul de centile), sont configurables. toolearn en savoir plus sur le facteur de croissance, consultez la section, « considérations de facteur de croissance » hello. toolearn savoir plus sur la valeur de centile, consultez la section de « Valeur de centile utilisé pour le calcul de hello » de hello.
>

## <a name="requirements"></a>Configuration requise
outil de Hello comprend deux phases principales : la génération de profils et de rapport. Il existe également une troisième option toocalculate de débit uniquement. exigences Hello pour serveur hello à partir de quels hello profilage et le débit mesure est initiée sont présentés dans hello tableau suivant :

| Configuration requise du serveur | Description|
|---|---|
|Profilage et mesure du débit| <ul><li>Système d’exploitation : Microsoft Windows Server 2012 R2<br>(dans l’idéal, correspondant au moins hello [dimensionner des recommandations pour le serveur de configuration hello](https://aka.ms/asr-v2a-on-prem-components))</li><li>Configuration de la machine : 8 processeurs virtuels, 16 Go de RAM, disque dur de 300 Go</li><li>[Microsoft .NET Framework 4.5](https://aka.ms/dotnet-framework-45)</li><li>[VMware vSphere PowerCLI 6.0 R3](https://aka.ms/download_powercli)</li><li>[Microsoft Visual C++ Redistributable pour Visual Studio 2012](https://aka.ms/vcplusplus-redistributable)</li><li>TooAzure d’accès Internet à partir de ce serveur</li><li>Compte Azure Storage</li><li>Accès d’administrateur sur le serveur de hello</li><li>Au minimum 100 Go d’espace disque disponible (en supposant que 1 000 machines virtuelles avec une moyenne de trois disques chacune, profilage pour 30 jours)</li><li>Paramètres de niveau de VMware vCenter statistiques doivent être définis too2 ou niveau élevé</li><li>Autoriser le port 443 : planification du déploiement du système utilise ce port tooconnect toovCenter serveur/ESXi hôte</ul></ul>|
| Génération de rapport | Un PC Windows ou serveur Windows Server doté de Microsoft Excel 2013 ou version ultérieure |
| Autorisations utilisateur | Autorisation en lecture seule hello compte d’utilisateur qui a utilisé hôte tooaccess hello VMware vCenter server/VMware vSphere ESXi lors du profilage |

> [!NOTE]
>
>outil de Hello peut profiler uniquement des machines virtuelles avec des disques VMDK et RDM. Il ne peut pas profiler les machines virtuelles équipées de disques iSCSI ou NFS. Récupération de site prend en charge iSCSI et les disques NFS des serveurs VMware, mais planification du déploiement hello n’étant pas invité hello et il profils uniquement à l’aide des compteurs de performance vCenter, outil de hello n’a pas de visibilité de ces types de disques.
>

## <a name="download-and-extract-hello-public-preview"></a>Téléchargez et installez la version préliminaire publique de hello
1. Télécharger la version la plus récente de hello hello [version préliminaire publique de récupération de Site déploiement planner](https://aka.ms/asr-deployment-planner).  
outil de Hello est empaqueté dans un dossier .zip. version actuelle de Hello de l’outil de hello prend en charge uniquement le scénario de VMware à Azure hello.

2. Copiez hello .zip dossier toohello Windows server à partir de laquelle vous voulez que toorun hello outil.  
Vous pouvez exécuter les outil hello à partir de Windows Server 2012 R2 si les serveur hello réseau accès tooconnect toohello vCenter server/ESXi hôte vSphere contenant toobe de machines virtuelles Bonjour profilée. Toutefois, nous vous recommandons d’exécuter hello outil sur un serveur dont la configuration matérielle répond aux hello [indications de dimensionnement de serveur de configuration](https://aka.ms/asr-v2a-on-prem-components). Si vous avez déjà déployé le Site Recovery composants locaux, exécuter l’outil de hello hello serveur de configuration.

 Nous vous recommandons d’avoir hello même configuration matérielle en tant que serveur de configuration hello (qui dispose d’un serveur intégré dans le processus) sur le serveur hello sur lequel vous exécutez l’outil de hello. Une telle configuration garantit que le débit hello obtenue que hello outil rapports correspondances hello débit réel qui permettent d’obtenir de la récupération de Site lors de la réplication. calcul du débit Hello dépend de la bande passante réseau disponible sur le serveur de hello et la configuration matérielle (UC, stockage et ainsi de suite) du serveur de hello. Si vous exécutez l’outil de hello à partir de n’importe quel autre serveur, débit de hello est calculé à partir de cette tooMicrosoft serveur Azure. En outre, étant donné que la configuration matérielle de hello du serveur de hello peut différer de celle du serveur de configuration hello, débit hello obtenue hello outil rapports risquent d’être erronée.

3. Extraire le dossier de .zip hello.  
dossier de Hello contient plusieurs fichiers et sous-dossiers. le fichier exécutable Hello est ASRDeploymentPlanner.exe dans le dossier parent de hello.

    Exemple :  
    Copiez tooE de fichier .zip hello : \ de lecteur et l’extraire.
   E:\ASR Deployment Planner-Preview_v1.2.zip

    E:\ASR Deployment Planner-Preview_v1.2\ ASR Deployment Planner-Preview_v1.2\ ASRDeploymentPlanner.exe

## <a name="capabilities"></a>Fonctionnalités
Vous pouvez exécuter l’outil de ligne de commande hello (ASRDeploymentPlanner.exe) dans un des hello suivant trois modes :

1. Profilage  
2. Génération de rapport
3. GetThroughput

Exécutez d’abord, outil de hello dans l’évolution des données de mode toogather machine virtuelle et des IOPS de profilage. Ensuite, exécutez rapport hello toogenerate hello toofind hello configuration réseau de bande passante et de stockage requise.

## <a name="profiling"></a>Profilage
Dans le mode de profilage, outil de planification du déploiement hello connecte toohello vCenter server/vSphere données de performances ESXi hôte toocollect sur hello machine virtuelle.

* Le profilage n’affecte pas les performances de hello de production de hello machines virtuelles, car aucune connexion directe n’est établie toothem. Toutes les données de performances sont collectées à partir de hello vCenter server/ESXi hôte vSphere.
* tooensure qu’est un impact négligeable sur les serveur hello en raison de profilage, hello outil requêtes hello vCenter server/ESXi hôte vSphere toutes les 15 minutes. Cet intervalle de requête ne pas compromettre les précision profilage, car l’outil de hello stocke les données de compteur de performance de toutes les minutes.

### <a name="create-a-list-of-vms-tooprofile"></a>Créer une liste des ordinateurs virtuels tooprofile
Tout d’abord, vous devez obtenir la liste des toobe de machines virtuelles Bonjour profilée. Vous pouvez obtenir tous les noms de hello de machines virtuelles sur un hôte ESXi du serveur/vSphere vCenter à l’aide des commandes de PowerCLI hello VMware vSphere Bonjour suivant la procédure. Ou bien, vous pouvez répertorier un nom convivial hello ou les adresses IP de hello machines virtuelles que vous souhaitez tooprofile manuellement.

1. Connectez-vous toohello VM que VMware vSphere PowerCLI est installé dans.
2. Ouvrez la console de PowerCLI hello VMware vSphere.
3. Vérifiez que la stratégie d’exécution hello est activé pour le script de hello. Si elle est désactivée, lancez hello VMware vSphere PowerCLI console en mode administrateur, puis l’activer en exécutant hello commande suivante :

            Set-ExecutionPolicy –ExecutionPolicy AllSigned

4. Vous pouvez hello de toorun option besoin de commande suivante si VIServer de se connecter n’est pas reconnu en tant que nom hello d’applet de commande.
 
            Add-PSSnapin VMware.VimAutomation.Core 

5. tooget tous les noms des ordinateurs virtuels sur un serveur vCenter/vSphere ESXi hello d’hébergeront et enregistrer hello liste dans un fichier .txt, exécution hello deux commandes répertoriées ici.
Remplacez &lsaquo;server name&rsaquo;, &lsaquo;user name&rsaquo;, &lsaquo;password&rsaquo; et &lsaquo;outputfile.txt&rsaquo; par vos entrées.

            Connect-VIServer -Server <server name> -User <user name> -Password <password>

            Get-VM |  Select Name | Sort-Object -Property Name >  <outputfile.txt>

6. Ouvrez le fichier de sortie hello dans le bloc-notes et copiez les noms de tous les ordinateurs virtuels que vous souhaitez tooprofile tooanother fichier (par exemple, ProfileVMList.txt), un nom de machine virtuelle par ligne hello. Ce fichier est utilisé en tant qu’entrée toohello *- VMListFile* paramètre de l’outil de ligne de commande hello.

    ![Liste des noms de machine virtuelle dans la planification du déploiement hello](./media/site-recovery-deployment-planner/profile-vm-list.png)

### <a name="start-profiling"></a>Démarrer le profilage
Après avoir configuré la liste hello des toobe de machines virtuelles de profilage, vous pouvez exécuter l’outil de hello dans le mode de profilage. Ici est hello liste de paramètres obligatoires et facultatives de hello outil toorun dans le mode de profilage.

ASRDeploymentPlanner.exe -Operation StartProfiling /?

| Nom du paramètre | Description |
|---|---|
| -Operation | StartProfiling |
| -Server | nom de domaine complet de Hello ou adresse IP de hello vCenter server/ESXi hôte vSphere dont machines virtuelles sont toobe profilé.|
| -User | Hello utilisateur nom tooconnect toohello vCenter server/ESXi hôte vSphere. utilisateur de Hello doit toohave accès en lecture seule, au minimum.|
| -VMListFile | fichier Hello qui contient la liste hello de toobe de machines virtuelles de profilage. chemin d’accès du fichier Hello peut être absolu ou relatif. fichier de Hello doit contenir une seule machine virtuelle nom/adresse IP par ligne. Nom d’ordinateur virtuel spécifié dans le fichier de hello doit être hello identique au nom d’ordinateur virtuel hello sur hello vCenter server/ESXi hôte vSphere.<br>Par exemple, le fichier hello VMList.txt contient hello suivant des machines virtuelles :<ul><li>virtual_machine_A</li><li>10.150.29.110</li><li>virtual_machine_B</li><ul> |
| -NoOfDaysToProfile | nombre de Hello de jours pendant laquelle le profilage est toobe exécution. Nous vous recommandons de profilage depuis plus de 15 jours tooensure qui hello du modèle de charge de travail dans votre environnement sur hello spécifié période est prise en charge et utilisé tooprovide une recommandation précise. |
| -Répertoire | (Facultatif) hello UNC universal naming convention () ou toostore de chemin d’accès au répertoire local générées pendant le profilage des données de profilage. Si un nom de répertoire n’est pas accordée, répertoire hello nommé 'ProfiledData' sous le chemin d’accès actuel de hello sera utilisé comme répertoire par défaut de hello. |
| -Mot de passe | (Facultatif) hello mot de passe toouse tooconnect toohello vCenter server/ESXi hôte vSphere. Si vous ne spécifiez pas un maintenant, vous demandera il lors de l’exécution de commande hello.|
| -StorageAccountName | Nom de compte de stockage de hello (facultatif) est le débit de hello toofind utilisé réalisable pour la réplication de données à partir des locaux tooAzure. Hello outil téléchargements test toothis stockage compte toocalculate le débit des données.|
| -StorageAccountKey | Clé de compte de stockage hello (facultatif) qui utilise le compte de stockage tooaccess hello. Accédez toohello portail Azure > comptes de stockage ><*nom de compte de stockage*>> Paramètres > clés d’accès > Key1 (ou clé d’accès primaire pour le compte de stockage classique). |
| -Environment | (Facultatif) Votre environnement de compte Stockage Azure cible. Ce paramètre peut être défini sur l’une des trois valeurs suivantes : AzureCloud, AzureUSGovernment, AzureChinaCloud. La valeur par défaut est AzureCloud. Utilisez le paramètre hello lorsque votre région Azure cible est clouds Azure du gouvernement ou Azure Chine. |


Il est recommandé que vous profilez vos machines virtuelles pendant au moins 15 too30 jours. Au cours de profilage période de hello, ASRDeploymentPlanner.exe continue à fonctionner. l’outil Hello prend entrée au moment du profilage en jours. Si vous souhaitez tooprofile pendant quelques heures ou minutes pour un test rapide de l’outil de hello, dans la version préliminaire publique de hello, vous devez temps de hello tooconvert dans la mesure équivalent hello en jours. Par exemple, tooprofile pendant 30 minutes, hello entrée doit être 30/(60*24) = 0,021 jours. Hello minimale autorisée de profilage de temps est de 30 minutes.

Pendant le profilage, vous pouvez éventuellement aussi passer un nom de compte de stockage et le débit hello toofind clés qui permettent d’obtenir de la récupération de Site au moment de hello de réplication du serveur de configuration hello ou tooAzure de serveur de processus. Si la clé et le nom de compte de stockage hello ne sont pas transmis pendant le profilage, outil de hello ne calcule pas le débit réalisable.

Vous pouvez exécuter plusieurs instances d’outil hello pour différents jeux de machines virtuelles. Assurez-vous que les noms de machine virtuelle hello ne sont pas répétées dans des hello jeux de profilage. Par exemple, si vous avez profilé dix ordinateurs virtuels (VM1 via VM10) et après quelques jours que vous souhaitez tooprofile un autre cinq machines virtuelles (VM11 via VM15), vous pouvez exécuter l’outil de hello à partir d’une autre console de ligne de commande pour hello deuxième ensemble de machines virtuelles (VM11 via VM15). Vérifiez que hello deuxième ensemble d’ordinateurs virtuels n’ont pas tous les noms de machine virtuelle à partir de la première instance de profilage hello ou que vous utilisez un répertoire de sortie différent pour la deuxième exécution de hello. Si deux instances de l’outil de hello sont utilisées pour le profilage hello même des machines virtuelles et utilisez Bonjour même répertoire de sortie, les rapports hello généré seront incorrectes.

Configurations de machine virtuelle sont capturées une fois au début de hello de profilage de l’opération de hello et stockées dans un fichier appelé VMDetailList.xml. Ces informations sont utilisées lors de la génération de rapports de hello. Toute modification de la configuration d’ordinateur virtuel (par exemple, un nombre accru de cœurs, les disques ou les cartes réseau) à partir de la fin de toohello hello début du profilage n’est pas capturée. Si une configuration de machine virtuelle profilée a changé au cours de hello de profilage en version préliminaire publique de hello, voici informations les plus récentes VM hello solution de contournement tooget lors de la génération de rapports de hello :

* Sauvegarder VMdetailList.xml et supprimez-le hello son emplacement actuel.
* Passez - et - mot de passe des arguments lors de la génération de rapports hello.

Hello profilage commande génère plusieurs fichiers Bonjour Active le profilage. Ne supprimez pas les fichiers de hello, car cela affecte donc la génération de rapports.

#### <a name="example-1-profile-vms-for-30-days-and-find-hello-throughput-from-on-premises-tooazure"></a>Exemple 1 : Machines virtuelles de profil pour 30 jours et un débit de hello rechercher à partir de local tooAzure
```
ASRDeploymentPlanner.exe -Operation StartProfiling -Directory “E:\vCenter1_ProfiledData” -Server vCenter1.contoso.com -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt”  -NoOfDaysToProfile  30  -User vCenterUser1 -StorageAccountName  asrspfarm1 -StorageAccountKey Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

#### <a name="example-2-profile-vms-for-15-days"></a>Exemple 2 : profiler des machines virtuelles pendant 15 jours

```
ASRDeploymentPlanner.exe -Operation StartProfiling -Directory “E:\vCenter1_ProfiledData” -Server vCenter1.contoso.com -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt”  -NoOfDaysToProfile  15  -User vCenterUser1
```

#### <a name="example-3-profile-vms-for-1-hour-for-a-quick-test-of-hello-tool"></a>Exemple 3 : Machines virtuelles de profil une heure pour un test rapide de l’outil de hello
```
ASRDeploymentPlanner.exe -Operation StartProfiling -Directory “E:\vCenter1_ProfiledData” -Server vCenter1.contoso.com -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt”  -NoOfDaysToProfile  0.04  -User vCenterUser1
```

>[!NOTE]
>
>* Si cet outil hello de serveur de hello est en cours d’exécution a été redémarré ou est en panne, ou si vous fermez hello outil à l’aide de Ctrl + C, les données de profilage de hello est conservé. Toutefois, il existe un risque d’hello manquant des 15 dernières minutes de données profilées. Dans ce cas, réexécutez l’outil hello du mode de profilage après redémarrage du serveur de hello.
>* Lorsque nom de compte de stockage hello et la clé sont passés, hello outil mesures hello de débit en hello dernière étape de profilage. Si l’outil de hello est fermée avant la fin de profilage, le débit de hello n’est pas calculé. débit de hello toofind avant de générer hello rapport, vous pouvez exécuter l’opération de GetThroughput hello à partir de la console de ligne de commande de hello. Sinon, les rapports hello généré ne contient pas d’informations sur le débit hello.


## <a name="generate-a-report"></a>Générer un rapport
outil de Hello génère un en charge les macros Microsoft Excel (fichier XLSM) en tant que sortie de rapport hello, qui résume toutes les recommandations de déploiement hello. rapport de Hello est nommé DeploymentPlannerReport_ <*identificateur numérique unique*> .xlsm et placé dans hello spécifié le répertoire.

Une fois le profilage terminé, vous pouvez exécuter l’outil de hello en mode de génération de rapports. Hello tableau suivant contient une liste de toorun de paramètres obligatoires et facultatives outil en mode de génération de rapports.

`ASRDeploymentPlanner.exe -Operation GenerateReport /?`

|Nom du paramètre | Description |
|-|-|
| -Operation | GenerateReport |
| -Server |  Hello vCenter/vSphere complet serveur nom de domaine ou l’adresse IP (utilisez hello même nom ou adresse IP que vous avez utilisé au moment de hello de profilage) où Bonjour profilée machines virtuelles dont la déclaration est toobe généré sont situés. Notez que si vous avez utilisé un serveur vCenter au moment de hello de profilage, vous ne pouvez pas utiliser un serveur vSphere pour la génération de rapports et vice versa.|
| -VMListFile | fichier Hello qui contient la liste hello de machines virtuelles profilées qui hello du rapport est toobe généré pour. chemin d’accès du fichier Hello peut être absolu ou relatif. fichier de Hello doit contenir un nom de machine virtuelle ou une adresse IP par ligne. les noms de machine virtuelle Hello qui sont spécifiés dans le fichier de hello doit être hello identique à celui des noms de machine virtuelle hello sur hello vCenter server/ESXi hôte vSphere et de correspondance, ce qui a été utilisé pendant le profilage.|
| -Répertoire | (Facultatif) hello UNC ou chemin d’accès du répertoire local où hello profilage des données (fichiers générés pendant le profilage) est stocké. Ces données sont requises pour la génération d’un rapport de hello. Si aucun nom n’est spécifié, le répertoire ProfiledData est utilisé. |
| -GoalToCompleteIR | Hello (facultatif) le nombre d’heures dans le hello la réplication initiale de hello profilé machines virtuelles doit toobe s’est terminée. rapport de Hello généré fournit hello plusieurs ordinateurs virtuels pour lesquels la réplication initiale peut être effectuée en hello spécifié temps. valeur par défaut Hello est de 72 heures. |
| -User | (Facultatif) hello utilisateur nom toouse tooconnect toohello vCenter/serveur vSphere. nom du Hello est utilisé toofetch hello dernières informations de configuration de machines virtuelles, telles que nombre hello de disques, nombre de cœurs et nombre de cartes réseau, toouse dans les rapports hello de hello. Si le nom de hello n’est pas fourni, les informations de configuration hello collectées au début de hello Hello réunion de lancement de profilage sont utilisées. |
| -Mot de passe | (Facultatif) hello mot de passe toouse tooconnect toohello vCenter server/ESXi hôte vSphere. Si le mot de passe hello n’est pas spécifié en tant que paramètre, vous demandera il ultérieurement lors de l’exécution de commande hello. |
| -DesiredRPO | Hello (facultatif) souhaitée point de récupération, en minutes. valeur par défaut Hello est de 15 minutes.|
| -Bandwidth | Bande passante en Mbits/s. Bonjour paramètre toouse toocalculate Bonjour RPO qui peut être obtenue pour hello spécifié de la bande passante. |
| -StartDate | Date et heure de début (facultatif) hello dans MM-JJ-YYYY:HH:MM (format 24 heures). Le paramètre *StartDate* doit être spécifié avec le paramètre *EndDate*. Lors de la date de début est spécifié, les rapports de hello sont générées pour les données de Bonjour profilée collectées entre StartDate et EndDate. |
| -EndDate | Date de fin hello (facultatif) et d’heure dans MM-JJ-YYYY:HH:MM (format 24 heures). Le paramètre *EndDate* doit être spécifié avec le paramètre *StartDate*. Lors de la date de fin est spécifié, les rapports de hello sont générées pour les données de Bonjour profilée collectées entre StartDate et EndDate. |
| -GrowthFactor | Facteur de croissance hello (facultatif), exprimée en pourcentage. valeur par défaut Hello est de 30 pour cent. |
| -UseManagedDisks | (Facultatif) UseManagedDisks - Oui/Non. La valeur par défaut est Oui. nombre de Hello d’ordinateurs virtuels qui peut être placé dans un seul compte de stockage est calculé en tenant compte de si le basculement/Test de basculement des machines virtuelles est effectuée sur le disque managé au lieu de disk non managé. |

#### <a name="example-1-generate-a-report-with-default-values-when-hello-profiled-data-is-on-hello-local-drive"></a>Exemple 1 : Générer un rapport avec les valeurs par défaut lorsque les données de profilage de hello sont sur le disque local hello
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “\\PS1-W2K12R2\vCenter1_ProfiledData” -VMListFile “\\PS1-W2K12R2\vCenter1_ProfiledData\ProfileVMList1.txt”
```

#### <a name="example-2-generate-a-report-when-hello-profiled-data-is-on-a-remote-server"></a>Exemple 2 : Générer un rapport lorsque les données Bonjour profilée se trouvent sur un serveur distant
Doit avoir accès en lecture/écriture sur le répertoire distant de hello.
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “\\PS1-W2K12R2\vCenter1_ProfiledData” -VMListFile “\\PS1-W2K12R2\vCenter1_ProfiledData\ProfileVMList1.txt”
```

#### <a name="example-3-generate-a-report-with-a-specific-bandwidth-and-goal-toocomplete-ir-within-specified-time"></a>Exemple 3 : Générer un rapport avec un toocomplete spécifique de la bande passante et objectif infrarouge dans le temps spécifié
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “E:\vCenter1_ProfiledData” -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt” -Bandwidth 100 -GoalToCompleteIR 24
```

#### <a name="example-4-generate-a-report-with-a-5-percent-growth-factor-instead-of-hello-default-30-percent"></a>Exemple 4 : Générer un rapport avec un facteur de croissance de 5 pour cent au lieu de 30 pour cent de la valeur par défaut hello
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “E:\vCenter1_ProfiledData” -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt” -GrowthFactor 5
```

#### <a name="example-5-generate-a-report-with-a-subset-of-profiled-data"></a>Exemple 5 : générer un rapport contenant un sous-ensemble de données profilées
Par exemple, vous disposez de 30 jours de données profilées et que vous souhaitez toogenerate un rapport d’uniquement 20 jours.
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “E:\vCenter1_ProfiledData” -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt” -StartDate  01-10-2017:12:30 -EndDate 01-19-2017:12:30
```

#### <a name="example-6-generate-a-report-for-5-minute-rpo"></a>Exemple 6 : générer un rapport pour un RPO de 5 minutes
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “E:\vCenter1_ProfiledData” -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt”  -DesiredRPO 5
```

## <a name="percentile-value-used-for-hello-calculation"></a>Valeur de centile utilisé pour le calcul de hello
**Quelle valeur de centile par défaut hello de mesures de performances collectées pendant le profilage est hello outil à utiliser lorsqu’il génère un rapport ?**

Hello outil par défaut toohello 95e centile des valeurs de lecture/écriture e/s, d’écriture e/s et évolution des données qui sont collectées pendant le profilage de tous les ordinateurs virtuels de hello. Cette mesure permet de s’assurer que pic centile 100ième hello vos machines virtuelles peuvent présenter des événements temporaires est toodetermine non utilisé votre configuration requise du compte de stockage et de bande passante de la source cible. Par exemple, un événement temporaire peut être une tâche de sauvegarde exécutée une fois par jour, une indexation de base de données périodique ou une activité de génération de rapport d’analyse ou d’autres événements similaires ponctuels et de courte durée.

Donne qu'une image exacte des caractéristiques de la charge de travail réelle et il vous donne à l’aide des valeurs de 95e centile hello de meilleures performances lorsque les charges de travail hello sont exécutent sur Azure. Nous ne prévoyez pas que vous devez toochange ce nombre. Si vous modifiez la valeur de hello (toohello 90e centile, par exemple), vous pouvez mettre à jour le fichier de configuration hello *ASRDeploymentPlanner.exe.config* dans hello dossier par défaut et l’enregistrer toogenerate un nouveau rapport hello existant de profilage données.
```
<add key="WriteIOPSPercentile" value="95" />      
<add key="ReadWriteIOPSPercentile" value="95" />      
<add key="DataChurnPercentile" value="95" />
```

## <a name="growth-factor-considerations"></a>Considérations relatives au facteur de croissance
**Pourquoi devrais-je tenir compte du facteur de croissance lors de la planification de déploiement ?**

Il est critique tooaccount croissance dans les caractéristiques de charge de travail, en supposant une possible augmentation d’utilisation au fil du temps. Une fois la protection est en place, si vous modifiez des caractéristiques de votre charge de travail, vous ne pouvez pas changer tooa autre compte de stockage pour la protection sans désactivation et réactivation de protection de hello.

Par exemple, supposons que, aujourd’hui, votre machine virtuelle s’intègre dans un compte de réplication de stockage standard. Hello trois prochains mois, plusieurs modifications qui sont susceptibles de toooccur :

* nombre de Hello d’utilisateurs de l’application hello qui s’exécute sur la machine virtuelle de hello augmente.
* évolution accrue résultant de Hello sur hello machine virtuelle requiert un stockage hello VM toogo toopremium afin que la réplication de la récupération de Site peut suivre le rythme.
* Par conséquent, vous avez toodisable et réactiver le compte de stockage premium protection tooa.

Nous recommandons vivement que vous planifiez la croissance lors de la planification du déploiement et lors de la valeur par défaut de hello est de 30 pour cent. Vous êtes hello expert sur des projections de croissance et le modèle de votre utilisation application, et vous pouvez modifier ce nombre en conséquence lors de la génération d’un rapport. En outre, vous pouvez générer plusieurs rapports avec différents facteurs de croissance par hello même profilage des données et déterminer les recommandations de la bande passante de source et de stockage cible convient le mieux.

rapport Microsoft Excel de Hello généré contient hello informations suivantes :

* [Input](site-recovery-deployment-planner.md#input)
* [Recommandations](site-recovery-deployment-planner.md#recommendations-with-desired-rpo-as-input)
* [Recommandations : entrée de bande passante](site-recovery-deployment-planner.md#recommendations-with-available-bandwidth-as-input)
* [VM&lt;-&gt;Storage Placement](site-recovery-deployment-planner.md#vm-storage-placement)
* [Compatible VMs](site-recovery-deployment-planner.md#compatible-vms)
* [Incompatible VMs](site-recovery-deployment-planner.md#incompatible-vms)

![Deployment planner](./media/site-recovery-deployment-planner/dp-report.png)

## <a name="get-throughput"></a>GetThroughput

débit hello tooestimate qui permettent d’obtenir de la récupération de Site à partir des locaux tooAzure lors de la réplication, exécuter l’outil de hello en mode de GetThroughput. outil de Hello calcule débit hello à partir du serveur hello hello outil est en cours d’exécution. Dans l’idéal, ce serveur est basé sur le guide de dimensionnement hello configuration serveur. Si vous avez déjà déployé le Site Recovery infrastructure composants locaux, exécutez outil de hello sur le serveur de configuration hello.

Ouvrez une console de ligne de commande et accédez toohello dossier de l’outil de planification du déploiement de Site Recovery. Exécutez ASRDeploymentPlanner.exe avec les paramètres ci-dessous.

`ASRDeploymentPlanner.exe -Operation GetThroughput /?`

|Nom du paramètre | Description |
|-|-|
| -Operation | GetThroughput |
| -Répertoire | (Facultatif) hello UNC ou chemin d’accès du répertoire local où hello profilage des données (fichiers générés pendant le profilage) est stocké. Ces données sont requises pour la génération d’un rapport de hello. Si aucun nom de répertoire n’est spécifié, le répertoire ProfiledData est utilisé. |
| -StorageAccountName | nom de compte de stockage Hello qui a utilisé la bande passante de hello toofind consommée pour la réplication de données à partir de local tooAzure. Hello outil téléchargements test données toothis stockage compte toofind hello la bande passante consommée. |
| -StorageAccountKey | clé de compte de stockage Hello qui utilise le compte de stockage tooaccess hello. Accédez toohello portail Azure > comptes de stockage ><*nom de compte de stockage*>> Paramètres > clés d’accès > Key1 (ou une clé d’accès primaire pour un compte de stockage classique). |
| -VMListFile | fichier Hello qui contient la liste hello de toobe de machines virtuelles de profilage pour le calcul de la bande passante de hello consommée. chemin d’accès du fichier Hello peut être absolu ou relatif. fichier de Hello doit contenir une seule machine virtuelle nom/adresse IP par ligne. les noms de machine virtuelle Hello spécifiés dans le fichier de hello doit être hello identique à celui des noms de machine virtuelle hello sur hello vCenter server/ESXi hôte vSphere.<br>Par exemple, le fichier hello VMList.txt contient hello suivant des machines virtuelles :<ul><li>VM_A</li><li>10.150.29.110</li><li>VM_B</li></ul>|
| -Environment | (Facultatif) Votre environnement de compte Stockage Azure cible. Ce paramètre peut être défini sur l’une des trois valeurs suivantes : AzureCloud, AzureUSGovernment, AzureChinaCloud. La valeur par défaut est AzureCloud. Utilisez le paramètre hello lorsque votre région Azure cible est clouds Azure du gouvernement ou Azure Chine. |

outil de Hello crée plusieurs fichiers de 64 Mo asrvhdfile <> # .vhd (où « # » est le nombre de hello de fichiers) sur le répertoire spécifié de hello. outil de Hello télécharge hello fichiers toohello compte toofind hello du débit de stockage. Une fois que le débit hello est mesuré, outil de hello supprime tous les fichiers de hello du compte de stockage hello et du serveur local de hello. Si l’outil de hello est arrêté pour une raison quelconque pendant qu’il est de calculer le débit, elle ne supprime pas les fichiers hello du stockage de hello ou serveur local de hello. Vous devez toodelete les manuellement.

Hello le débit est mesuré à un point spécifié dans le temps, et il est le débit maximal hello qui permettent d’obtenir de la récupération de Site lors de la réplication, sous réserve que tous les autres facteurs demeurent hello même. Par exemple, si n’importe quelle application commence à consommer davantage de bande passante sur hello varie en fonction du même réseau, le débit réel hello lors de la réplication. Si vous exécutez hello GetThroughput commande à partir d’un serveur de configuration, outil de hello est sans se préoccuper de toutes les machines virtuelles protégées et la réplication en cours. Hello résultat du débit mesuré de hello est différent si hello GetThroughput opération est exécutée lorsque hello protégée des machines virtuelles ont importante des données d’évolution du. Nous vous recommandons d’exécuter hello outil à différents points dans le temps pendant le profilage toounderstand quelles débit niveaux peuvent être atteints à différents moments. Dans le rapport de hello, outil de hello montre débit mesuré dernière de hello.

### <a name="example"></a>Exemple
```
ASRDeploymentPlanner.exe -Operation GetThroughput -Directory  E:\vCenter1_ProfiledData -VMListFile E:\vCenter1_ProfiledData\ProfileVMList1.txt  -StorageAccountName  asrspfarm1 -StorageAccountKey by8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

>[!NOTE]
>
> Exécuter l’outil de hello sur un serveur qui a hello même stockage et les caractéristiques de l’UC en tant que serveur de configuration hello.
>
> Pour la réplication, définissez Bonjour la bande passante recommandée toomeet Bonjour RPO 100 % du temps de hello. Après avoir défini la bande passante droite hello, si vous ne voyez pas augmenter le débit hello obtenue signalé par l’outil de hello, procédez comme hello suivant :
>
>  1. Vérifiez toodetermine s’il y a aucun réseau de qualité de Service (QoS) qui limitent le débit de la récupération de Site.
>
>  2. Vérifiez toodetermine si votre archivage Site Recovery est Bonjour plus proche de la latence du réseau toominimize de région Microsoft Azure physiquement pris en charge.
>
>  3. Vérifiez votre toodetermine de caractéristiques de stockage local si vous pouvez améliorer le matériel hello (par exemple, disque dur tooSSD).
>
>  4. Modifier les paramètres de récupération de Site de hello dans le serveur de processus hello trop[augmenter la bande passante réseau utilisée pour la réplication hello](./site-recovery-plan-capacity-vmware.md#control-network-bandwidth).

## <a name="recommendations-with-desired-rpo-as-input"></a>Recommandations liées au RPO souhaité en tant qu’entrée

### <a name="profiled-data"></a>Données profilées

![affichage des données de profilage Hello dans la planification du déploiement hello](./media/site-recovery-deployment-planner/profiled-data-period.png)

**La période de données profilées**: période hello pendant le hello le profilage a été exécuté. Par défaut, outil de hello inclut toutes les données de profil dans le calcul de hello, sauf si elle génère des rapports de hello pour une période spécifique à l’aide d’options StartDate et EndDate pendant la génération du rapport.

**Nom du serveur**: nom de hello ou adresse IP de hello VMware vCenter ou l’hôte ESXi les rapports dont ordinateurs virtuels sont généré.

**Vous le souhaitez RPO**: objectif de point de récupération hello pour votre déploiement. Par défaut, hello requis de la bande passante réseau est calculée pour les valeurs RPO de 15, 30 et 60 minutes. En fonction de sélection de hello, hello affecté sont mis à jour sur la feuille de hello. Si vous avez utilisé hello *DesiredRPOinMin* paramètre lors de la génération de rapports hello, que la valeur est affichée dans le résultat souhaité de RPO de hello.

### <a name="profiling-overview"></a>Vue d’ensemble du profilage

![Résultats de profilage dans la planification du déploiement hello](./media/site-recovery-deployment-planner/profiling-overview.png)

**Nombre total de profilage des Machines virtuelles**: hello nombre total d’ordinateurs virtuels dont les données profilées sont disponibles. Si hello VMListFile possède des noms de toutes les machines virtuelles qui ont été profilées pas, ces machines virtuelles ne sont pas considérés comme dans la génération de rapports hello et sont exclus de nombre de machines virtuelles profilée total hello.

**Les ordinateurs virtuels compatibles**: hello du nombre d’ordinateurs virtuels qui peuvent être tooAzure protégé à l’aide de récupération de Site. Il est hello le nombre total de compatibles machines virtuelles pour le hello les besoins en bande passante, nombre de comptes de stockage, le nombre de cœurs Azure et nombre de serveurs de configuration et les serveurs de traitement supplémentaires sont calculées. Détails de Hello de chaque machine virtuelle compatible sont disponibles dans hello « Machines virtuelles compatibles » section.

**Les Machines virtuelles incompatible**: hello du nombre d’ordinateurs virtuels profilées qui ne sont pas compatibles pour la protection avec la récupération de Site. raisons Hello incompatibilité sont notées dans hello « Machines virtuelles Incompatible » section. Si hello VMListFile possède des noms de toutes les machines virtuelles qui ont été profilées pas, ces machines virtuelles sont exclus de nombre de machines virtuelles hello incompatible. Ces machines virtuelles sont répertoriés comme « Données introuvable » à fin hello de section de hello » Incompatible machines virtuelles ».

**Desired RPO** : votre objectif de point de récupération souhaité, en minutes. rapport de Hello est généré pour les trois valeurs RPO : 15 (valeur par défaut), 30 et 60 minutes. recommandation de la bande passante Hello dans les rapports hello est modifiée en fonction de votre sélection dans la liste de hello déroulante souhaité le RPO en hello en haut à droite de la feuille de hello. Si vous avez généré le rapport de hello à l’aide de hello *- DesiredRPO* paramètre avec une valeur personnalisée, cette valeur personnalisée affiche par défaut de hello dans la liste de hello souhaité le RPO de liste déroulante.

### <a name="required-network-bandwidth-mbps"></a>Bande passante réseau requise (Mbits/s)

![Besoins en bande passante dans la planification du déploiement hello](./media/site-recovery-deployment-planner/required-network-bandwidth.png)

**toomeet RPO 100 % du temps de hello :** hello recommandé de bande passante en Mbits/s toobe allouée toomeet votre RPO souhaitée 100 % du temps de hello. Cette quantité de bande passante doit être dédié pour la réplication delta de l’état stable de tous vos tooavoid de machines virtuelles compatible des violations de RPO.

**toomeet RPO 90 pour cent de temps de hello**: en raison de la tarification haut débit ou pour toute autre raison, si vous ne pouvez pas définir toomeet de bande passante nécessaire hello votre RPO souhaitée 100 % du temps de hello, vous pouvez choisir toogo avec une faible bande passante qui peut répondre à votre RPO souhaitée 90 pour cent de temps de hello. implications en matière de toounderstand hello de la définition de cette bande passante réduite, les rapports hello fournit une analyse de simulation sur le nombre de hello et la durée de RPO violations tooexpect.

**Débit réalisé :** débit hello du serveur hello sur lequel vous avez exécuté la région Microsoft Azure hello GetThroughput commande toohello où se trouve le compte de stockage hello. Ce nombre de débit indique niveau hello estimé que vous pouvez obtenir lorsque vous protégez hello compatibles machines virtuelles à l’aide de récupération de Site, sous réserve que votre serveur de configuration ou les caractéristiques de réseau et de stockage de serveur de processus restent hello même que celui de serveur Hello à partir de laquelle vous avez exécuté les outil hello.

Pour la réplication, vous devez définir Bonjour la bande passante recommandée toomeet Bonjour RPO 100 % du temps de hello. Après avoir défini la bande passante de hello, si vous ne voyez pas toute augmentation du débit hello obtenue, comme indiqué par l’outil de hello, procédez comme hello suivant :

1. Vérifiez toosee s’il y a aucun réseau de qualité de Service (QoS) qui limitent le débit de la récupération de Site.

2. Vérifiez toosee si votre archivage Site Recovery est Bonjour plus proche de la latence du réseau toominimize de région Microsoft Azure physiquement pris en charge.

3. Vérifiez votre toodetermine de caractéristiques de stockage local si vous pouvez améliorer le matériel hello (par exemple, disque dur tooSSD).

4. Modifier les paramètres de récupération de Site de hello dans le serveur de processus hello trop[augmenter la bande passante du réseau hello quantité utilisée pour la réplication](./site-recovery-plan-capacity-vmware.md#control-network-bandwidth).

Si vous exécutez hello outil sur un serveur de configuration ou un serveur de processus qui a déjà protégé des machines virtuelles, exécuter hello plusieurs fois l’outil. Hello obtenue débit nombre change en fonction de la quantité de hello d’évolution du code en cours de traitement à ce stade dans le temps.

Pour tous les déploiements Site Recovery d’entreprise, nous vous recommandons d’utiliser [ExpressRoute](https://aka.ms/expressroute).

### <a name="required-storage-accounts"></a>Comptes de stockage requis
Hello ci-dessous illustre graphique nombre total de hello de stockage des comptes (standard et premium) qui sont requis tooprotect tous les hello compatibles machines virtuelles. toolearn toouse de compte de stockage pour chaque machine virtuelle, consultez la section de « placement de stockage de l’ordinateur virtuel » de hello.

![Comptes de stockage requise de planification du déploiement hello](./media/site-recovery-deployment-planner/required-azure-storage-accounts.png)

### <a name="required-number-of-azure-cores"></a>Required number of Azure cores
Ce résultat est le nombre total de hello de toobe cœurs configurer avant le basculement ou test de basculement de tous les hello compatibles machines virtuelles. Si trop peu de cœurs sont disponibles dans l’abonnement de hello, récupération de Site échoue toocreate VMs au moment de hello de basculement ou test.

![Nombre de cœurs Azure dans la planification du déploiement hello requis](./media/site-recovery-deployment-planner/required-number-of-azure-cores.png)

### <a name="required-on-premises-infrastructure"></a>Required on-premises infrastructure
Cette figure est le nombre total de hello de serveurs de configuration et serveurs supplémentaires processus toobe configuré que suffirait tooprotect tous hello compatibles machines virtuelles. En fonction de la prise en charge de hello [dimensionner des recommandations pour le serveur de configuration hello](https://aka.ms/asr-v2a-on-prem-components), outil de hello peut recommander des serveurs supplémentaires. recommandation de Hello est basée sur hello plus grand de l’évolution du code de hello par jour ou de nombre maximal de hello d’ordinateurs virtuels protégés (en supposant une moyenne de trois disques par machine virtuelle), la plus élevée étant atteint premier sur le serveur de configuration de hello ou un serveur de processus supplémentaire hello. Vous trouverez des détails hello d’évolution totale du code par jour et le nombre total de disques protégés Bonjour section de « Entrée ».

![Obligatoire-l’infrastructure locale dans la planification du déploiement hello](./media/site-recovery-deployment-planner/required-on-premises-infrastructure.png)

### <a name="what-if-analysis"></a>Analyse de scénarios
Cette analyse présente le nombre de violations peut se produire au cours de hello profilage période lorsque vous définissez qu'une faible bande passante pour hello souhaité RPO toobe remplie uniquement 90 pour cent de temps de hello. Une ou plusieurs violations de RPO peuvent se produire sur un jour donné. graphique de Hello affiche la pointe de hello RPO de la journée de hello.
Cette analyse, vous pouvez décider si nombre hello de violations de RPO sur tous les jours et PIC atteint par jour RPO est acceptable avec hello spécifié à faible bande passante. S’il est acceptable, vous pouvez allouer une bande passante inférieure hello pour la réplication, sinon allouer hello beaucoup de bande passante convenance toomeet suggérée hello RPO 100 % du temps de hello.

![Analyse de simulation dans la planification du déploiement hello](./media/site-recovery-deployment-planner/what-if-analysis.png)

### <a name="recommended-vm-batch-size-for-initial-replication"></a>Recommended VM batch size for initial replication
Dans cette section, nous vous recommandons de nombre hello de machines virtuelles pouvant être protégées dans la réplication initiale de hello toocomplete parallèles dans les 72 heures par hello suggéré souhaité de la bande passante toomeet RPO 100 % du temps hello définie. Cette valeur est configurable. toochange il au moment de la génération de rapports, utilisez hello *GoalToCompleteIR* paramètre.

graphique ici Hello affiche une plage de valeurs de la bande passante et d’une calculée VM lot taille nombre toocomplete la réplication initiale dans 72 heures, en fonction de la moyenne de hello détecté VM taille ensemble hello compatibles machines virtuelles.

Dans la version préliminaire publique de hello, rapport de hello ne spécifie pas les machines virtuelles doivent être inclus dans un lot. Vous pouvez utiliser la taille du disque hello hello « Compatible machines virtuelles » section toofind illustré de taille de la machine virtuelle et les sélectionner pour un lot, ou vous pouvez sélectionner des machines virtuelles de hello en fonction des caractéristiques de charge de travail connus. heure d’achèvement Hello des modifications de la réplication initiale hello proportionnellement, selon la taille de disque de machine virtuelle réel hello, utilisé l’espace disque et du débit du réseau disponible.

![Taille de lot recommandée de machines virtuelles](./media/site-recovery-deployment-planner/recommended-vm-batch-size.png)

### <a name="growth-factor-and-percentile-values-used"></a>Growth factor and percentile values used
Cette section bas hello hello centile affiche hello utilisé pour tous les compteurs de performances hello de machines virtuelles de Bonjour profilée (valeur par défaut est 95e centile) de la feuille et hello facteur de croissance (valeur par défaut est 30 pour cent) qui est utilisée dans tous les calculs hello.

![Growth factor and percentile values used](./media/site-recovery-deployment-planner/max-iops-and-data-churn-setting.png)

## <a name="recommendations-with-available-bandwidth-as-input"></a>Recommandations relatives à la bande passante disponible comme entrée

![Recommandations relatives à la bande passante disponible comme entrée](./media/site-recovery-deployment-planner/profiling-overview-bandwidth-input.png)

Vous pouvez vous trouver dans une situation dans laquelle vous ne pouvez pas configurer une bande passante supérieure à x Mbits/s pour la réplication Site Recovery. outil de Hello vous permet de la bande passante disponible de tooinput (à l’aide de hello - paramètre de bande passante pendant la génération de rapports) et get hello RPO réalisable en minutes. Avec cette valeur RPO réalisable, vous pouvez décider si vous avez besoin de tooset supplémentaires de bande passante ou si vous êtes OK avec disposer d’une solution de récupération d’urgence avec ce RPO.

![RPO possible pour une bande passante de 500 Mbits/s](./media/site-recovery-deployment-planner/achievable-rpos.png)

## <a name="input"></a>Entrée
feuille de calcul entrée Hello fournit qu'une vue d’ensemble de Bonjour profilée environnement VMware.

![Vue d’ensemble de Bonjour profilée environnement VMware](./media/site-recovery-deployment-planner/Input.png)

**Date de début** et **Date de fin**: hello les dates de début et de fin de hello pris en compte pour la génération de rapports de données de profilage. Par défaut, date de début hello est date hello profilage au démarrage, et la date de fin hello est hello lorsque le profilage s’arrête. Cela peut être hello « StartDate » et « EndDate » valeurs si le rapport de hello est généré avec ces paramètres.

**Nombre total de jours de profilage**: nombre total de hello de jours de profilage entre hello commencer et se terminer de dates pour le hello rapport est généré.

**Nombre d’ordinateurs virtuels compatibles**: nombre total de hello de machines virtuelles de compatibles quelle bande passante du réseau hello requise, nombre requis de stockage des comptes, les cœurs Microsoft Azure, les serveurs de configuration et sont des serveurs de traitement supplémentaires calculée.

**Nombre total de disques sur tous les ordinateurs virtuels compatibles**: nombre de hello est utilisé comme l’un des hello entrées toodecide hello différents serveurs de configuration et toobe de serveurs de processus supplémentaires utilisés dans le déploiement de hello.

**Nombre moyen de disques par machine virtuelle compatibles**: nombre moyen de hello de disques calculée sur tous les ordinateurs virtuels compatibles.

**Taille du disque (Go) moyenne**: taille de disque moyenne hello calculée sur tous les ordinateurs virtuels compatibles.

**Souhaitée (en minutes) de RPO**: soit hello par défaut valeur point de récupération objectif ou hello passé pour le paramètre de 'DesiredRPO' hello au moment de hello de tooestimate de génération de rapport requis la bande passante.

**Souhaité de la bande passante (Mbps)**: hello valeur que vous avez passé pour le paramètre de 'La bande passante' hello lors de tooestimate de génération de rapports hello RPO réalisable.

**Évolution du code de données classiques observée par jour (Go)**: hello moyenne des données évolution observés dans le profilage de tous les jours. Ce numéro est utilisé comme un nombre hello entrées toodecide hello de serveurs de configuration et toobe de serveurs de processus supplémentaires utilisés dans le déploiement de hello.


## <a name="vm-storage-placement"></a>VM-storage placement

![VM-storage placement](./media/site-recovery-deployment-planner/vm-storage-placement.png)

**Type de stockage de disque**: soit un compte standard ou premium, qui est utilisé tooreplicate tous hello correspondant de machines virtuelles mentionnés dans hello **tooPlace de machines virtuelles** colonne.

**Suggéré préfixe**: hello suggérée préfixe à trois caractères qui peut être utilisé pour le compte de stockage hello d’affectation de noms. Vous pouvez utiliser votre propre préfixe, mais les suggestions de l’outil hello suivant hello [une convention d’affectation de noms pour les comptes de stockage de partition](https://aka.ms/storage-performance-checklist).

**Compte nom suggéré**: nom de compte de stockage hello après avoir inclus les préfixe suggéré hello. Remplacez hello nom entre crochets hello (< et >) avec vos entrées personnalisées.

**Compte de stockage de journal**: tous les journaux de réplication hello sont stockés dans un compte de stockage standard. Pour les machines virtuelles qui répliquent tooa compte de stockage premium, configurer un compte de stockage standard supplémentaire pour le stockage du journal. Un seul et même compte de stockage standard des journaux peut être utilisé par plusieurs comptes de stockage de réplication premium. Machines virtuelles qui correspondent à un stockage répliqué toostandard comptes utilisent hello même compte de stockage pour les journaux.

**Journal compte nom suggéré**: votre compte de stockage journal nom après avoir inclus les préfixe suggéré hello. Remplacez hello nom entre crochets hello (< et >) avec vos entrées personnalisées.

**Résumé de la sélection élective**: un résumé des hello total charge des machines virtuelles sur le compte de stockage hello lors de la réplication hello et test de basculement ou basculement. Il inclut le nombre total de hello de machines virtuelles mappés toohello compte de stockage total en lecture/écriture e/s sur tous les ordinateurs virtuels placés dans ce compte de stockage, le nombre total d’écriture (réplication) IOPS, taille totale d’installation pour tous les disques et nombre total de disques.

**Machines virtuelles tooPlace**: une liste de tous les hello des machines virtuelles qui doivent être placés sur hello donné du compte de stockage pour optimiser les performances et l’utilisation.

## <a name="compatible-vms"></a>Machines virtuelles compatibles
![Feuille de calcul Excel des machines virtuelles compatibles](./media/site-recovery-deployment-planner/compatible-vms.png)

**Nom de machine virtuelle**: hello nom d’ordinateur virtuel ou d’adresse IP qui est utilisé dans hello VMListFile lorsqu’un rapport est généré. Cette colonne répertorie également les disques hello (VMDK) qui sont des machines virtuelles de toohello attaché. vCenter toodistinguish machines virtuelles avec des noms en double ou les adresses IP, les noms de hello incluent les nom d’hôte ESXi hello. Hello hôtes ESXi répertoriés est hello une où hello machine virtuelle a été placé lors de l’outil de hello découverts pendant hello période de profilage.

**VM Compatibility** : les valeurs sont **Oui** et **Oui**\*. **Oui** \* concerne les instances dans le hello machine virtuelle est un ajustement pour [stockage Azure Premium](https://aka.ms/premium-storage-workload). Ici, Bonjour profilée évolution de haute ou IOPS convenant à hello P20 ou une catégorie de P30, mais la taille de hello du disque de hello, il toobe mappée vers le bas tooa P10 ou P20. compte de stockage Hello décide quel disque de stockage premium tapez toomap un disque, en fonction de sa taille. Par exemple :
* < 128 Go : disque P10.
* 128 Go too512 Go est un P20.
* 512 Go too1024 Go est un P30.
* 1025 too2048 Go est un P40.
* 2049 too4095 Go est un P50.

Si les caractéristiques d’un disque hello placer dans hello P20 ou P30 catégorie, mais la taille de hello est mappé vers le bas du type de disque de stockage tooa inférieure premium, outil de hello marque cette machine virtuelle en tant que **Oui**\*. outil de Hello recommande également transformer hello source disque taille toofit hello recommandé de type de disque de stockage premium ou de les modifier après le type basculement hello cible disque.

**Storage Type** : standard ou premium.

**Suggéré préfixe**: préfixe de compte de stockage de trois caractères hello.

**Compte de stockage**: nom hello qui utilise le préfixe de compte de stockage suggérée hello.

**E/s de lecture/écriture (avec le facteur de croissance)**: hello pointe la charge de travail en lecture/écriture e/s sur disque de hello (valeur par défaut est 95e centile), y compris le facteur de croissance future hello (valeur par défaut est 30 pour cent). Notez que hello total en lecture/écriture e/s d’une machine virtuelle n’est pas toujours somme hello d’en lecture/écriture disques de machine virtuelle hello individuels e/s, hello pointe en lecture/écriture e/s de hello VM étant pointe hello de somme de hello de ses différents disques en lecture/écriture e/s lors de chaque minute de hello période de profilage.

**Évolution de données en Mbits/s (avec le facteur de croissance)**: taux d’évolution hello pointe sur le disque de hello (valeur par défaut est 95e centile), y compris le facteur de croissance future hello (valeur par défaut est 30 pour cent). Notez que hello évolution totale des données de hello VM n’est pas toujours somme hello d’évolution de données des disques de machine virtuelle hello individuels, car évolution de données pointe hello Hello machine virtuelle est pointe hello de somme hello d’évolution de ses différents disques pendant chaque minute de hello période de profilage.

**Taille de machine virtuelle Azure**: hello idéale mappés taille de machine virtuelle Azure Cloud Services pour ce local machine virtuelle. mappage de Hello est basé sur mémoire hello local VM, nombre de disques/cœurs/cartes réseau et les e/s de lecture/écriture. recommandation de Hello est toujours hello plus bas Azure VM taille qui correspond à l’ensemble des caractéristiques de machine virtuelle locale hello.

**Nombre de disques**: hello nombre total de disques de machine virtuelle (VMDK) sur la machine virtuelle de hello.

**Taille (Go) du disque**: hello taille totale de programme d’installation de tous les disques de machine virtuelle de hello. outil de Hello montre également la taille du disque hello pour chacun des disques hello Bonjour machine virtuelle.

**Cœurs**: nombre hello du processeur cœurs sur hello machine virtuelle.

**Mémoire (Mo)**: hello RAM sur hello machine virtuelle.

**Cartes réseau**: hello du nombre de cartes réseau sur la machine virtuelle de hello.

**Type de démarrage**: il est de type de démarrage de hello machine virtuelle. Le type de démarrage peut prendre la valeur BIOS ou EFI. Pour l’instant, Azure Site Recovery ne prend en charge que le type de démarrage BIOS. Tous les ordinateurs virtuels hello du type de démarrage EFI sont répertoriées dans la feuille de calcul de machines virtuelles Incompatible.

**Type de système d’exploitation**: hello est le type de système d’exploitation de hello machine virtuelle. Ce type peut prendre la valeur Windows ou Linux.

## <a name="incompatible-vms"></a>Machines virtuelles incompatibles

![Feuille de calcul Excel des machines virtuelles incompatibles](./media/site-recovery-deployment-planner/incompatible-vms.png)

**Nom de machine virtuelle**: hello nom d’ordinateur virtuel ou d’adresse IP qui est utilisé dans hello VMListFile lorsqu’un rapport est généré. Cette colonne répertorie également hello VMDK qui sont attachés toohello VMs. vCenter toodistinguish machines virtuelles avec des noms en double ou les adresses IP, les noms de hello incluent les nom d’hôte ESXi hello. Hello hôtes ESXi répertoriés est hello une où hello machine virtuelle a été placé lors de l’outil de hello découverts pendant hello période de profilage.

**Compatibilité de la machine virtuelle**: indique pourquoi hello donné de machine virtuelle est incompatible avec la récupération de Site. Hello les raisons sont décrites pour chaque disque incompatible de hello machine virtuelle et, en fonction publié sur [limites de stockage](https://aka.ms/azure-storage-scalbility-performance), peut être hello suivants :

* La taille du disque est > 4095 Go. Actuellement, le stockage Azure ne prend pas en charge les tailles de disques de données supérieures à 4095 Go.
* Le disque du système d’exploitation est  > 2048 Go. Actuellement, le stockage Azure ne prend pas en charge les tailles de disques de systèmes d’exploitation supérieures à 2048 Go.
* Le type de démarrage est EFI. Pour l’instant, Azure Site Recovery ne prend en charge que les machines virtuelles qui présentent le type de démarrage BIOS.

* Taille de machine virtuelle (réplication + TFO) dépasse la limite de taille de compte de stockage hello pris en charge (35 To). Cette incompatibilité se produit généralement lorsqu’un seul disque Bonjour machine virtuelle a une caractéristique de performances qui dépasse hello maximales limites prises en charge Azure ou de récupération de Site pour le stockage standard. Une telle instance exécute un push hello machine virtuelle dans la zone de stockage premium hello. Toutefois, hello maximale taille prise en charge d’un compte de stockage premium est 35 To et une seule protégé la machine virtuelle ne peut pas être protégé sur plusieurs comptes de stockage. Notez également que, lorsqu’un test de basculement est exécutée sur une machine virtuelle protégée, elle s’exécute dans hello même compte de stockage où de progression de la réplication. Dans ce cas, 2 x taille hello du disque hello pour tooprogress de réplication et test de basculement toosucceed en parallèle.
* Les E/S par seconde source excèdent la limite des E/S par seconde prise en charge par le stockage qui est de 5 000 par disque.
* Les E/S par seconde source excèdent la limite des E/S par seconde prise en charge par le stockage qui est de 80 000 par machine virtuelle.
* Évolution moyenne de données dépasse pris en charge Site Recovery évolution la limite de 10 Mbits/s pour la taille moyenne des e/s de disque de hello.
* L’évolution du total des données sur tous les disques sur la machine virtuelle de hello dépasse hello maximale prise en charge Site Recovery évolution la limite de 54 Mbits/s par machine virtuelle.
* Écriture effective moyenne par seconde dépasse la limite de Site Recovery IOPS de hello pris en charge de 840 pour le disque.
* Stockage de cliché instantané calculée dépasse la limite de stockage de capture instantanée de hello pris en charge de 10 To.

**E/s de lecture/écriture (avec le facteur de croissance)**: hello pics de charge e/s sur disque de hello (valeur par défaut est 95e centile), y compris le facteur de croissance future hello (valeur par défaut est 30 pour cent). Notez que hello total en lecture/écriture e/s de hello VM n’est pas toujours somme hello d’en lecture/écriture disques de machine virtuelle hello individuels e/s, hello pointe en lecture/écriture e/s de hello VM étant pointe hello de somme de hello de ses différents disques en lecture/écriture e/s lors de chaque minute de hello période de profilage.

**Évolution de données en Mbits/s (avec le facteur de croissance)**: taux d’évolution hello pointe sur le disque de hello (valeur par défaut 95e centile), y compris le facteur de croissance future hello (valeur par défaut 30 pour cent). Notez que hello évolution totale des données de hello VM n’est pas toujours somme hello d’évolution de données des disques de machine virtuelle hello individuels, car évolution de données pointe hello Hello machine virtuelle est pointe hello de somme hello d’évolution de ses différents disques pendant chaque minute de hello période de profilage.

**Nombre de disques**: hello nombre total de VMDK sur hello machine virtuelle.

**Taille (Go) du disque**: hello taille totale de programme d’installation de tous les disques de machine virtuelle de hello. outil de Hello montre également la taille du disque hello pour chacun des disques hello Bonjour machine virtuelle.

**Cœurs**: nombre hello du processeur cœurs sur hello machine virtuelle.

**Mémoire (Mo)**: quantité hello de mémoire vive sur hello machine virtuelle.

**Cartes réseau**: hello du nombre de cartes réseau sur la machine virtuelle de hello.

**Type de démarrage**: il est de type de démarrage de hello machine virtuelle. Le type de démarrage peut prendre la valeur BIOS ou EFI. Pour l’instant, Azure Site Recovery ne prend en charge que le type de démarrage BIOS. Tous les ordinateurs virtuels hello du type de démarrage EFI sont répertoriées dans la feuille de calcul de machines virtuelles Incompatible.

**Type de système d’exploitation**: hello est le type de système d’exploitation de hello machine virtuelle. Ce type peut prendre la valeur Windows ou Linux.


## <a name="site-recovery-limits"></a>Limites Azure Site Recovery

**Stockage de réplication cible** | **Taille d’E/S moyenne de disque source** |**Activité des données moyenne de disque source** | **Total de l’activité des données de disque source par jour**
---|---|---|---
Stockage Standard | 8 Ko | 2 Mbits/s | 168 Go par disque
Disque P10 Premium | 8 Ko | 2 Mbits/s | 168 Go par disque
Disque P10 Premium | 16 Ko | 4 Mbits/s | 336 Go par disque
Disque P10 Premium | 32 Ko ou plus | 8 Mbits/s | 672 Go par disque
Disque Premium P20 ou P30 | 8 Ko  | 5 Mbits/s | 421 Go par disque
Disque Premium P20 ou P30 | 16 Ko ou plus |10 Mbits/s | 842 Go par disque

Il s’agit de moyennes en partant sur un chevauchement d’E/S de 30 pour cent. Site Recovery est capable de gérer un débit plus élevé en fonction du ratio de chevauchement, de tailles d’écriture plus grandes et du comportement d’E/S des charges de travail réelles. Hello nombres précédents supposent un retard de traitement par défaut de cinq minutes. Autrement dit, une fois que les données sont chargées, elles sont traitées, et un point de récupération est créé dans un délai de cinq minutes.

Les limites sont basées sur nos tests, mais ne peuvent pas couvrir toutes les combinaisons d’E/S d’application possibles. Les résultats réels varient en fonction de la combinaison d’E/S de votre application. Pour de meilleurs résultats, même après la planification du déploiement, nous conseillons d’effectuer des tests à l’aide d’une image de test de basculement tooget hello performances réelles de très nombreuses applications.

## <a name="updating-hello-deployment-planner"></a>Mise à jour de la planification du déploiement hello
projets de déploiement tooupdate hello, procédez comme hello suivant :

1. Télécharger la version la plus récente de hello hello [planification de déploiement Azure Site Recovery](https://aka.ms/asr-deployment-planner).

2. Copie hello .zip dossier tooa le serveur que vous souhaitez toorun sur.

3. Extraire le dossier de .zip hello.

4. Effectuez une des manières suivantes les hello :
 * Si la version la plus récente hello ne contient pas un correctif de profilage et le profilage est déjà en cours d’exécution sur votre version actuelle du module de hello, continuer le profilage hello.
 * Si la version la plus récente hello ne contient pas un correctif de profilage, nous vous recommandons d’arrêter le profilage dans votre version actuelle et de redémarrer hello profilage avec la nouvelle version de hello.

  >[!NOTE]
  >
  >Quand vous démarrez le profilage avec hello nouvelle version, passe hello que même chemin d’accès du répertoire de sortie afin que hello outil ajoute les données de profil sur hello des fichiers existants. Un ensemble complet de données profilées sera toogenerate hello état utilisé. Si vous passez d’un répertoire de sortie différent, de nouveaux fichiers sont créés et anciennes données de profilage n’est pas utilisé rapport de hello toogenerate.
  >
  >Chaque nouvelle planification de déploiement est une mise à jour cumulative du fichier .zip de hello. Vous n’avez pas besoin toocopy hello les plus récents fichiers toohello dossier précédent. Vous pouvez créer un dossier et l’utiliser.


## <a name="version-history"></a>Historique des versions

### <a name="131"></a>1.3.1
Dernière mise à jour : 19 juillet, 2017

La nouvelle fonctionnalité suivante est ajoutée :

* La prise en charge des disques volumineux (> 1To) a été ajoutée à la génération de rapport. Maintenant, vous pouvez utiliser la réplication tooplan déploiement planner pour les ordinateurs virtuels qui ont des tailles de disque supérieurs à 1 To (4095 en Go au maximum).
En savoir plus sur la [Prise en charge des disques volumineux sur Azure Site Recovery](https://azure.microsoft.com/en-us/blog/azure-site-recovery-large-disks/)


### <a name="13"></a>1.3
Mise à jour : 9 mai 2017

La nouvelle fonctionnalité suivante est ajoutée :

* Ajout de la prise en charge des disques gérés dans la génération de rapport. Hello nombre d’ordinateurs virtuels peut être placé stockage tooa compte est calculée selon si géré disque est sélectionnée pour le basculement de basculement et de Test.        


### <a name="12"></a>1.2
Mise à jour : 7 avril 2017

Ajout des correctifs suivants :

* Démarrage ajouté tapez check (BIOS ou EFI) pour chaque ordinateur virtuel de toodetermine si l’ordinateur virtuel de hello est compatible ou non pour la protection de hello.
* Ajout du système d’exploitation de type d’informations pour chaque ordinateur virtuel dans hello Compatible de machines virtuelles et les feuilles de calcul de machines virtuelles Incompatible.
* Hello GetThroughput opération est maintenant pris en charge dans les régions du gouvernement et de la Chine Microsoft Azure hello.
* Ajout de quelques autres vérifications préalables pour les serveurs vCenter et ESXi.
* État incorrect a été mise en route généré quand les paramètres régionaux a toonon-anglais.


### <a name="11"></a>1.1
Mise à jour : 9 mars 2017

Hello fixe suivants :

* outil de Hello ne peut pas profiler des machines virtuelles si hello vCenter a deux ou plusieurs ordinateurs virtuels avec hello même nom ou l’adresse IP entre différents hôtes ESXi.
* Copie et recherche est désactivée pour hello Compatible de machines virtuelles et les machines virtuelles Incompatible des feuilles de calcul.

### <a name="10"></a>1.0
Mise à jour : 23 février 2017

Azure Site Recovery déploiement Planner version préliminaire publique 1.0 a hello problèmes connus suivants (toobe traité dans les mises à jour à venir) :

* outil de Hello fonctionne uniquement pour les scénarios de VMware à Azure, pas pour les déploiements de Hyper-V vers Azure. Pour les scénarios de Hyper-V vers Azure, utilisez hello [outil de planification de capacité Hyper-V](./site-recovery-capacity-planning-for-hyper-v-replication.md).
* Hello GetThroughput opération n’est pas pris en charge dans les régions du gouvernement et de la Chine Microsoft Azure hello.
* outil de Hello ne peut pas profiler des machines virtuelles si le serveur vCenter hello a deux ou plusieurs ordinateurs virtuels avec hello même nom ou l’adresse IP entre différents hôtes ESXi. Dans cette version, outil de hello ignore le profilage pour les noms de machine virtuelle en double ou les adresses IP dans hello VMListFile. solution de contournement Hello est tooprofile hello machines virtuelles à l’aide d’un ordinateur hôte ESXi plutôt que le serveur vCenter hello. Vous devez exécuter une instance par hôte ESXi.
