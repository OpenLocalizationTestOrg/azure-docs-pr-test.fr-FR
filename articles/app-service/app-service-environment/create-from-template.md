---
title: "aaaCreate un environnement de Service d’applications Azure à l’aide d’un modèle de gestionnaire de ressources"
description: "Explique comment toocreate un environnement externe ou d’équilibrage de charge interne Azure App Service à l’aide d’un modèle de gestionnaire de ressources"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 6eb7d43d-e820-4a47-818c-80ff7d3b6f8e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: c8aeedee675a6e931169b725ee916cc7fa8f762f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-ase-by-using-an-azure-resource-manager-template"></a>Créer un ASE à l’aide d’un modèle Azure Resource Manager

## <a name="overview"></a>Vue d'ensemble
Les environnements Azure App Service (ASE, App Service Environment) peuvent être créés avec un point de terminaison accessible via Internet ou un point de terminaison sur une adresse interne d’un réseau virtuel Azure. S’il est créé avec un point de terminaison interne, ce point de terminaison est fourni par un composant Azure appelé équilibreur de charge interne (ILB, Internal Load Balancer). Hello ASE sur une adresse IP interne est appelé un environnement app service Équilibrage de charge interne. Hello ASE avec un point de terminaison public est appelé un environnement app service externe. 

Un environnement app service peut être créé à l’aide de hello portail Azure ou un modèle Azure Resource Manager. Cet article explique les étapes de hello et de syntaxe, vous devez toocreate une ASE externes ou les ASE d’équilibrage de charge avec les modèles de gestionnaire de ressources. toolearn toocreate ASE Bonjour portail Azure, voir [rendre ASE externe] [ MakeExternalASE] ou [rendre un environnement app service Équilibrage de charge interne][MakeILBASE].

Lorsque vous créez un environnement app service Bonjour portail Azure, vous pouvez créer votre réseau virtuel à hello en même temps ou choisissez un toodeploy de réseau virtuel préexistant dans. Lorsque vous créez un ASE à partir d’un modèle, vous devez commencer avec : 

* Un réseau virtuel Resource Manager.
* Un sous-réseau de ce réseau virtuel. Nous vous recommandons d’une taille de sous-réseau ASE de `/25` avec une croissance future tooaccomodate 128 adresses. Après que hello ASE est créé, vous ne pouvez pas modifier la taille de hello.
* ID de ressource Hello à partir de votre réseau virtuel. Vous pouvez obtenir ces informations à partir de hello portail Azure sous propriétés de votre réseau virtuel.
* Hello abonnement toodeploy dans.
* Hello emplacement toodeploy dans.

tooautomate votre création ASE :

1. Créer hello ASE à partir d’un modèle. Si vous créez un ASE externe, vous avez terminé après cette étape. Si vous créez un environnement app service Équilibrage de charge interne, il existe quelques toodo plus de choses.

2. Une fois votre ASE ILB créé, un certificat SSL correspondant à votre domaine ASE ILB est chargé.

3. Hello téléchargé certificat SSL est affecté toohello ASE d’équilibrage de charge interne en tant que son certificat SSL de « default ».  Ce certificat est utilisé pour tooapps de trafic SSL sur hello ASE d’équilibrage de charge interne lorsqu’ils utilisent le domaine racine commun hello qui est attribué toohello ASE (par exemple, https://someapp.mycustomrootcomain.com).


## <a name="create-hello-ase"></a>Créer hello ASE
Un modèle Azure Resource Manager permettant de créer un ASE et son fichier de paramètres associé est disponible sous forme d’[exemple][quickstartasev2create] sur GitHub.

Si vous souhaitez toomake ASE équilibrage de charge interne, utilisez ces modèles de gestionnaire de ressources [exemples][quickstartilbasecreate]. Ils prenant en charge les cas d’usage toothat. La plupart des paramètres hello Bonjour *azuredeploy.parameters.json* fichier sont courantes toohello la création de ASEs d’équilibrage de charge interne et externe ASEs. Hello liste suivante appelle les paramètres out de la Remarque spéciale, ou qui sont uniques, lorsque vous créez un environnement app service Équilibrage de charge interne :

* *interalLoadBalancingMode*: dans la plupart des cas, définissez cette too3, ce qui signifie que le trafic HTTP/HTTPS sur les ports 80/443, et les ports de canal de contrôle et de données hello écoutés service hello FTP tooby hello ASE, sera lié tooan alloué par l’équilibrage de charge de réseau virtuel adresse interne. Si cette propriété a la valeur too2, uniquement hello FTP relatives au service de ports (canaux de contrôle et de données) sont adresse d’équilibrage de charge interne tooan liée. Hello le trafic HTTP/HTTPS reste sur l’adresse IP virtuelle publique de hello.
* *un suffixe DNS*: ce paramètre définit le domaine racine par défaut hello est attribué toohello ASE. Variante de public de hello du Service d’applications Azure, domaine racine de la valeur par défaut hello pour toutes les applications web est *azurewebsites.net*. Comme un environnement app service Équilibrage de charge interne est le réseau virtuel du client de tooa interne, il n’a aucune domaine de racine par défaut du service public sens toouse hello. Au lieu de cela, un ILB ASE doit avoir un domaine racine par défaut approprié pour une utilisation au sein du réseau virtuel interne d’une société. Par exemple, Contoso Corporation peut utiliser un domaine de la racine par défaut de *contoso.com interne* pour les applications qui sont prévu toobe pouvant être résolu et accessible uniquement dans le réseau virtuel de Contoso. 
* *ipSslAddressCount*: ce paramètre par défaut automatiquement tooa la valeur 0 dans hello *azuredeploy.json* fichier, car l’équilibrage de charge interne ASEs ont uniquement une seule adresse d’équilibrage de charge interne. Il n’existe pas d’adresse IP SSL explicite pour un ASE ILB. Par conséquent, toozero doit être définie à hello pool d’adresses IP SSL pour un environnement app service Équilibrage de charge interne. Autrement, une erreur d’approvisionnement se produit. 

Après avoir hello *azuredeploy.parameters.json* fichier est renseigné, créer hello ASE à l’aide d’extrait de code PowerShell hello. Modifier l’emplacement hello chemins toomatch hello Gestionnaire de ressources du fichier de modèle sur votre ordinateur. N’oubliez pas de toosupply vos propres valeurs pour le nom du Gestionnaire de ressources de déploiement hello et le nom de groupe de ressources hello :

    $templatePath="PATH\azuredeploy.json"
    $parameterPath="PATH\azuredeploy.parameters.json"

    New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

Cela prend environ une heure pour hello ASE toobe est créé. Puis hello ASE s’affiche dans le portail hello dans liste hello de ASEs pour l’abonnement hello qui a déclenché le déploiement de hello.

## <a name="upload-and-configure-hello-default-ssl-certificate"></a>Télécharger et configurer le certificat SSL de « default » hello
Un certificat SSL doit être associé à hello ASE comme hello « default » certificat SSL utilisé tooestablish SSL connexions tooapps. Si le suffixe DNS hello de ASE valeur par défaut est *contoso.com interne*, un toohttps://some-random-app.internal-contoso.com connexion requiert un certificat SSL valide pour **-contoso.com .internal* . 

Pour disposer d’un certificat SSL valide, vous pouvez recourir à des autorités de certification internes, acheter un certificat à un émetteur externe, ou utiliser un certificat auto-signé. Quelle que soit la source de hello du certificat SSL de hello, hello suivant des attributs de certificat doit être configuré correctement :

* **Objet**: cet attribut doit être défini trop **.votre-racine-domaine-here.com*.
* **Autre nom de l’objet** : cet attribut doit inclure à la fois **.votre-domaine-racine-ici.com* et **.scm.votre-domaine-racine-ici.com*. Toohello de connexions SSL site SCM/Kudu associé à chaque application utiliser une adresse sous forme de hello *your-app-name.scm.your-root-domain-here.com*.

Une fois le certificat SSL valide obtenu, deux étapes préparatoires supplémentaires sont nécessaires. Certificat SSL de hello Convert/enregistrer comme fichier .pfx. N’oubliez pas de fichier .pfx hello doit inclure tous les intermédiaire et les certificats racine. Sécurisez-le avec un mot de passe.

fichier .pfx de Hello doit toobe converti en une chaîne encodée base64, car le certificat SSL de hello est téléchargé à l’aide d’un modèle de gestionnaire de ressources. Étant donné que les modèles de gestionnaire de ressources sont des fichiers texte, fichier .pfx de hello doit être converti en une chaîne en base 64. Ainsi, il peut être inclus en tant que paramètre de modèle de hello.

Utilisez hello suivant extrait de code PowerShell :

* générer un certificat auto-signé ;
* Exporter le certificat de hello en tant que fichier .pfx.
* Convertir le fichier .pfx de hello en une chaîne codée en base64.
* Enregistrez-le hello chaîne codée en base64 tooa distinct. 

Ce code PowerShell pour le codage base64 est une adaptation de hello [blog des scripts PowerShell][examplebase64encoding]:

        $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "*.internal-contoso.com","*.scm.internal-contoso.com"

        $certThumbprint = "cert:\localMachine\my\" + $certificate.Thumbprint
        $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText

        $fileName = "exportedcert.pfx"
        Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password     

        $fileContentBytes = get-content -encoding byte $fileName
        $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)
        $fileContentEncoded | set-content ($fileName + ".b64")

Une fois que le certificat SSL de hello est généré avec succès et convertie la chaîne codée en base64 de tooa, utiliser modèle de gestionnaire de ressources exemple hello [configurer un certificat SSL par défaut hello] [ quickstartconfiguressl] sur GitHub. 

Hello paramètres Bonjour *azuredeploy.parameters.json* fichier sont répertoriées ici :

* *appServiceEnvironmentName*: nom hello Hello ASE d’équilibrage de charge en cours de configuration.
* *existingAseLocation*: chaîne de texte contenant hello région Azure où hello ASE d’équilibrage de charge interne a été déployé.  Par exemple : « Centre-Sud des États-Unis ».
* *pfxBlobString*: hello la représentation sous forme de chaîne encodée based64 du fichier .pfx de hello. Utilisez l’extrait de code hello présentée précédemment et copier la chaîne hello contenue dans « exportedcert.pfx.b64 ». Coller comme valeur hello Hello *pfxBlobString* attribut.
* *mot de passe*: le fichier .pfx hello hello mot de passe utilisé toosecure.
* *certificateThumbprint*: hello empreinte numérique du certificat. Si vous récupérez cette valeur à partir de PowerShell (par exemple, *$certificate. L’empreinte numérique* de hello extrait de code précédent), vous pouvez utiliser la valeur hello est. Si vous copiez la valeur de hello à partir de la boîte de dialogue de certificat Windows hello, n’oubliez pas toostrip les espaces superflus de hello. Hello *certificateThumbprint* doit ressembler à AF3143EB61D43F6727842115BB7F17BBCECAECAE.
* *certificateName*: un identificateur de chaîne conviviale de votre choix utilisé certificat de hello tooidentity. nom de Hello est utilisé en tant que partie d’identificateur de gestionnaire de ressources unique hello pour hello *Microsoft.Web/certificates* entité qui représente le certificat SSL de hello. nom de Hello *doit* se terminer par hello suivant suffixe : \_yourASENameHere_InternalLoadBalancingASE. Hello portail Azure utilise ce suffixe, comme un indicateur de hello certificat est utilisé toosecure ASE activé d’équilibrage de charge interne.

Un exemple abrégé du fichier *azuredeploy.parameters.json* est présenté ici :

    {
         "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json",
         "contentVersion": "1.0.0.0",
         "parameters": {
              "appServiceEnvironmentName": {
                   "value": "yourASENameHere"
              },
              "existingAseLocation": {
                   "value": "East US 2"
              },
              "pfxBlobString": {
                   "value": "MIIKcAIBAz...snip...snip...pkCAgfQ"
              },
              "password": {
                   "value": "PASSWORDGOESHERE"
              },
              "certificateThumbprint": {
                   "value": "AF3143EB61D43F6727842115BB7F17BBCECAECAE"
              },
              "certificateName": {
                   "value": "DefaultCertificateFor_yourASENameHere_InternalLoadBalancingASE"
              }
         }
    }

Après avoir hello *azuredeploy.parameters.json* fichier est renseigné, configurer un certificat SSL de hello par défaut à l’aide d’extrait de code PowerShell hello. Modifiez toomatch de chemins d’accès de fichier hello où se trouvent les fichiers de modèle de gestionnaire de ressources hello sur votre ordinateur. N’oubliez pas de toosupply vos propres valeurs pour le nom du Gestionnaire de ressources de déploiement hello et le nom de groupe de ressources hello :

     $templatePath="PATH\azuredeploy.json"
     $parameterPath="PATH\azuredeploy.parameters.json"

     New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

Il prend environ 40 minutes par modification de hello tooapply ASE front-end. Par exemple, pour ASE dimensionné par défaut qui utilise deux frontaux, le modèle de hello prend autour d’une heure et 20 minutes toocomplete. Pendant l’exécution de modèle de hello, hello ASE ne peut pas mettre à l’échelle.  

Une fois le modèle de hello terminée, applications sur hello ASE d’équilibrage de charge interne est accessible via le protocole HTTPS. connexions de Hello sont sécurisées à l’aide du certificat SSL de hello par défaut. certificat SSL de Hello par défaut est utilisé lorsque les applications sur hello ASE d’équilibrage de charge interne sont adressées à l’aide d’une combinaison de nom de l’application hello plus le nom d’hôte par défaut hello. Par exemple, https://mycustomapp.internal-contoso.com utilise le certificat SSL par défaut hello pour **-contoso.com .internal*.

Toutefois, tout comme les applications qui s’exécutent sur le service partagé de hello publique, les développeurs peuvent configurer des noms d’hôtes personnalisés pour les applications individuelles. Ils peuvent également configurer des liaisons de certificat SNI SSL uniques pour différentes applications.

## <a name="app-service-environment-v1"></a>Environnement App Service v1 ##
L’environnement App Service est disponible en deux versions : ASEv1 et ASEv2. Hello informations précédentes était basé sur ASEv2. Cette indique la section hello de différences entre ASEv1 et ASEv2.

Dans ASEv1, vous gérez toutes les ressources de hello manuellement. Qui inclut frontaux hello, aux employés et les adresses IP utilisées pour SSL basée sur IP. Avant que vous pouvez faire évoluer votre plan App Service, vous devez monter en charge pool de travail hello que vous souhaitez toohost il.

Les versions ASEv1 et ASEv2 utilisent un modèle de tarification différent. Dans ASEv1, vous payez pour chaque cœur alloué. Cela inclut les cœurs utilisés pour les serveurs frontaux ou les workers qui n’hébergent pas de charge de travail. Dans ASEv1, taille de l’échelle de la valeur maximale par défaut hello d’un environnement app service est 55 nombre total d’hôtes. dont les workers et les frontends. Un avantage tooASEv1 est qu’il peut être déployé dans un réseau virtuel classique et un réseau virtuel du Gestionnaire de ressources. toolearn en savoir plus sur ASEv1, consultez [introduction de v1 environnement App Service][ASEv1Intro].

toocreate un ASEv1 à l’aide d’un modèle de gestionnaire de ressources, consultez [créer un v1 ASE d’équilibrage de charge interne avec un modèle de gestionnaire de ressources][ILBASEv1Template].


<!--Links-->
[quickstartilbasecreate]: http://azure.microsoft.com/documentation/templates/201-web-app-asev2-ilb-create
[quickstartasev2create]: http://azure.microsoft.com/documentation/templates/201-web-app-asev2-create
[quickstartconfiguressl]: http://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-configure-default-ssl
[quickstartwebapponasev2create]: http://azure.microsoft.com/documentation/templates/201-web-app-asp-app-on-asev2-create
[examplebase64encoding]: http://powershellscripts.blogspot.com/2007/02/base64-encode-file.html 
[configuringDefaultSSLCertificate]: https://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-configure-default-ssl/
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
[ILBASEv1Template]: ../../app-service-web/app-service-app-service-environment-create-ilb-ase-resourcemanager.md
