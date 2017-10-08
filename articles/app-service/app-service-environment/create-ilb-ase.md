---
title: "aaaCreate et utilisez un équilibreur de charge interne avec un environnement Azure App Service"
description: "Pour plus d’informations sur la façon de toocreate et utiliser un environnement de Service d’applications Azure isolé d’internet"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 0f4c1fa4-e344-46e7-8d24-a25e247ae138
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: d019ca6f231c3acfdab4cd380db375a076802f7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-use-an-internal-load-balancer-with-an-app-service-environment"></a>Créer et utiliser un équilibreur de charge interne avec un environnement App Service #

 Un environnement Azure App Service est un déploiement d’Azure App Service dans un sous-réseau de réseau virtuel Azure. Il existe deux façons toodeploy un environnement App Service (ASE) : 

- avec une adresse IP virtuelle sur une adresse IP externe, solution souvent appelée ASE externe ;
- Avec une adresse IP virtuelle sur une adresse IP interne, souvent appelé un environnement app service Équilibrage de charge interne, car le point de terminaison interne hello est un équilibreur de charge interne (ILB). 

Cet article vous explique comment toocreate un environnement app service Équilibrage de charge interne. Pour une vue d’ensemble sur hello ASE, consultez [les environnements de Service Introduction tooApp][Intro]. toolearn toocreate ASE externe, voir [créer un environnement app service externe][MakeExternalASE].

## <a name="overview"></a>Vue d'ensemble ##

Vous pouvez déployer un ASE avec un point de terminaison accessible via Internet ou avec une adresse IP de votre réseau virtuel. tooset hello adresse IP de tooa adresse de réseau virtuel, hello ASE doit être déployé avec un équilibrage de charge interne. Lorsque vous déployez votre ASE avec un ILB, vous devez indiquer :

-   votre propre domaine que vous utilisez lorsque vous créez vos applications ;
-   certificat de Hello utilisé pour le protocole HTTPS.
-   la gestion DNS pour votre domaine.

En retour, vous pouvez effectuer des tâches telles que :

-   Héberger des applications intranet en toute sécurité dans le cloud hello, laquelle vous accédez via Azure ExpressRoute VPN de site à site.
-   Hôte des applications dans le cloud de hello qui ne sont pas répertoriées dans les serveurs DNS publics.
-   créer des applications principales isolées d’Internet auxquelles vos applications frontales peuvent s’intégrer en toute sécurité.

### <a name="disabled-functionality"></a>Fonctionnalités désactivées ###

Lorsque vous utilisez un ASE ILB, vous ne pouvez pas effectuer certaines opérations :

-   utiliser SSL basé sur IP ;
-   Affecter des adresses IP toospecific applications.
-   Acheter et utiliser un certificat avec une application via hello portail Azure. Vous pouvez obtenir des certificats directement auprès d’une autorité de certification et les utiliser avec vos applications. Vous ne peut pas obtenir via hello portail Azure.

## <a name="create-an-ilb-ase"></a>Créer un environnement ASE ILB ##

toocreate ASE équilibrage de charge interne :

1. Bonjour portail Azure, sélectionnez **nouveau** > **Web + Mobile** > **environnement App Service**.

2. Sélectionnez votre abonnement.

3. Sélectionnez ou créez un groupe de ressources.

4. Sélectionnez ou créez un réseau virtuel.

5. Si vous sélectionnez un réseau virtuel existant, vous devez toocreate un Bonjour toohold de sous-réseau ASE. Assurez-vous que la taille tooset un sous-réseau suffisamment grand tooaccommodate croissance future de votre ASE. Nous recommandons la taille `/25`, qui comprend 128 adresses et peut gérer un ASE de taille maximale. Vous pouvez sélectionner la taille minimale Hello est un `/28`. Une fois que l’infrastructure doit, cette taille peut comporter tooa mis à l’échelle de 11 instances.

    * Excède la valeur maximale par défaut de 100 instances hello dans vos plans de Service d’applications.

    * Mettez à l’échelle jusqu’à près de 100 instances, mais avec une mise à l’échelle du serveur frontal plus rapide.

6. Sélectionnez **Réseau virtuel/Emplacement** > **Configuration du réseau virtuel**. Ensemble hello **Type d’adresse IP virtuelle** trop**interne**.

7. Entrez un nom de domaine. Ce domaine est hello celui utilisé pour les applications créées dans cette ASE. Quelques restrictions s’appliquent. Ce ne peut pas être :

    * net   

    * azurewebsites.net

    * p.azurewebsites.net

    * &lt;asename&gt;.p.azurewebsites.net

   nom de domaine personnalisé Hello utilisé pour les applications et nom de domaine hello utilisé par votre ASE ne peut pas se chevaucher. Pour un environnement app service Équilibrage de charge interne avec le nom de domaine hello _contoso.com_, vous ne pouvez pas utiliser des noms de domaines personnalisés pour vos applications telles que :

    * www.contoso.com

    * abcd.def.contoso.com

    * abcd.contoso.com

   Si vous connaissez les noms de domaines personnalisés hello pour vos applications, choisissez un domaine pour hello ASE d’équilibrage de charge interne qui ne sont pas avoir un conflit avec les noms de domaine personnalisé. Dans cet exemple, vous pouvez utiliser quelque chose comme *contoso-internal.com* pour le domaine hello de votre ASE car qui ne sont pas en conflit avec les noms de domaines personnalisés qui se terminent par *. contoso.com*.

8. Sélectionnez **OK**, puis **Créer**.

    ![Création d’un environnement App Service][1]

Sur hello **réseau virtuel** panneau, il existe un **Configuration du réseau virtuel** option. Vous pouvez l’utiliser tooselect une adresse IP externe ou une adresse IP virtuelle interne. valeur par défaut Hello est **externe**. Si vous sélectionnez **Externe**, votre ASE utilise une adresse IP virtuelle accessible via Internet. Si vous sélectionnez **Interne**, votre ASE est configuré avec un ILB sur une adresse IP au sein de votre réseau virtuel.

Après avoir sélectionné **interne**, hello capacité tooadd plusieurs adresses tooyour ASE est supprimé. Au lieu de cela, vous devez domaine hello tooprovide hello ASE. Dans un environnement app service avec une adresse IP externe, un nom hello Hello QU'ASE est utilisé dans le domaine de hello pour les applications créées dans ce ASE.

Si vous définissez **Type d’adresse IP virtuelle** trop**interne**, votre nom ASE n’est pas utilisé dans le domaine de hello pour hello ASE. Vous spécifiez explicitement les domaine hello. Si votre domaine est *contoso.corp.net* et que vous créez une application dans la mesure où ASE nommé *timereporting*, hello URL pour cette application est timereporting.contoso.corp.net.


## <a name="create-an-app-in-an-ilb-ase"></a>Créer une application dans un ASE ILB ##

Vous créez une application dans un environnement app service Équilibrage de charge interne Bonjour même façon que vous créez une application dans un environnement app service normalement.

1. Bonjour portail Azure, sélectionnez **nouveau** > **Web + Mobile** > **Web** ou **Mobile** ou  **Application API**.

2. Entrez le nom hello de l’application hello.

3. Sélectionnez l’abonnement de hello.

4. Sélectionnez ou créez un groupe de ressources.

5. Sélectionnez ou créez un plan App Service. Si vous voulez toocreate un nouveau plan de Service d’applications, sélectionnez votre ASE en tant qu’emplacement de hello. Sélectionnez hello worker pool dans lequel votre toobe du plan App Service créé. Lorsque vous créez hello plan App Service, sélectionnez votre ASE comme emplacement de hello et le pool de travail hello. Lorsque vous spécifiez le nom de l’application hello de hello, domaine hello sous le nom de votre application est remplacé par le domaine de hello pour votre ASE.

6. Sélectionnez **Créer**. Si vous souhaitez hello application tooappear sur votre tableau de bord, sélectionnez le **toodashboard du code confidentiel** case à cocher.

    ![Création de plan App Service][2]

    Sous **nom de l’application**, nom de domaine hello est domaine hello tooreflect mis à jour votre ASE.

## <a name="post-ilb-ase-creation-validation"></a>Validation après la création de l’ASE ILB ##

Un environnement app service Équilibrage de charge interne est légèrement différent que hello non - équilibrage de charge interne ASE. Comme déjà indiqué, vous devez toomanage votre propre serveur DNS. Vous avez également tooprovide votre propre certificat pour les connexions HTTPS.

Après avoir créé votre ASE, nom de domaine hello montre domaine hello spécifié. Un nouvel élément nommé **Certificat ILB** apparaît dans le menu **Paramètre**. Hello ASE est créé avec un certificat qui ne spécifie pas de domaine d’équilibrage de charge interne ASE hello. Si vous utilisez hello ASE avec ce certificat, votre navigateur vous indique qu’il n’est pas valide. Ce certificat rend plus facile tootest HTTPS, mais vous devez tooupload votre propre certificat de domaine d’équilibrage de charge interne ASE tooyour liée. Cette étape est nécessaire, que votre certificat soit auto-signé ou acquis auprès d’une autorité de certification.

![Nom de domaine de l’ASE ILB][3]

Votre ASE ILB a besoin d’un certificat SSL valide. Vous pouvez recourir à des autorités de certification internes, acheter un certificat à un émetteur externe, ou utiliser un certificat auto-signé. Quelle que soit la source de hello du certificat SSL de hello, hello des attributs de certificat suivants doivent toobe configuré correctement :

* **Objet**: cet attribut doit être défini too*.your-racine-domaine-ici.
* **Autre nom de l’objet** : cet attribut doit inclure à la fois **.votre-domaine-racine-ici* et **.scm.votre-domaine-racine-ici*. Toohello de connexions SSL site SCM/Kudu associé à chaque application utiliser une adresse sous forme de hello *your-app-name.scm.your-root-domain-here*.

Certificat SSL de hello Convert/enregistrer comme fichier .pfx. fichier .pfx de Hello doit inclure tous les intermédiaire et les certificats racine. Sécurisez-le avec un mot de passe.

Si vous voulez toocreate un certificat auto-signé, vous pouvez utiliser les commandes de PowerShell hello ici. Être toouse que votre nom de domaine ASE d’équilibrage de charge interne à la place de *internal.contoso.com*: 

    $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "\*.internal-contoso.com","\*.scm.internal-contoso.com"
    
    $certThumbprint = "cert:\localMachine\my\" +$certificate.Thumbprint
    $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText
    
    $fileName = "exportedcert.pfx" 
    Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password

certificat Hello qui génèrent de ces commandes PowerShell est signalé par les navigateurs, car le certificat de hello n’a pas été créé par une autorité de certification qui figure dans la chaîne de confiance de votre navigateur. tooget un certificat de confiance de votre navigateur, il se procurer à partir de l’autorité de certification dans la chaîne de votre navigateur d’approbation. 

![Définir un certificat ILB][4]

tooupload vos propres certificats et le test d’accès :

1. Une fois hello ASE est créé, accédez à toohello ASE UI. Sélectionnez **ASE** > **Paramètres** > **Certificat ILB**.

2. certificat d’équilibrage de charge interne tooset hello, sélectionnez le fichier de certificat .pfx hello et entrez le mot de passe hello. Cette étape prend quelques tooprocess de temps. Un message s’affiche, indiquant qu’une opération de chargement est en cours.

3. Obtenir l’adresse d’équilibrage de charge interne hello pour votre ASE. Sélectionnez **ASE** > **Propriétés** > **Adresse IP virtuelle**.

4. Créer une application web dans votre ASE après que hello ASE est créé.

5. Créez une machine virtuelle si vous n’en avez pas dans ce réseau virtuel.

    > [!NOTE] 
    > N’essayez pas cet ordinateur virtuel dans toocreate hello même sous-réseau que hello ASE, car il sera échouer ou provoquer des problèmes.
    >
    >

6. Définissez hello DNS pour votre domaine ASE. Vous pouvez utiliser un caractère générique avec votre domaine dans votre DNS. tests de certaines simples toodo, modifier le fichier d’hôtes hello sur votre machine virtuelle tooset hello web app Nom toohello adresse IP de l’adresse IP virtuelle :

    a. Si votre ASE a le nom de domaine hello _. ilbase.com_ et que vous créez l’application hello web nommée _mytestapp_, elle est traitée pour _mytestapp.ilbase.com_. Vous définissez ensuite _mytestapp.ilbase.com_ adresse d’équilibrage de charge interne tooresolve toohello. (Sous Windows, fichier d’hôtes hello est à _C:\Windows\System32\drivers\etc\_.)

    b. tootest web déploiement publication ou accès toohello avancée de la console, créer un enregistrement pour _mytestapp.scm.ilbase.com_.

7. Utilisez un navigateur sur cette machine virtuelle, puis accédez à https://mytestapp.ilbase.com (Ou accédez toowhatever que le nom de votre application web est à votre domaine.)

8. Utilisez un navigateur sur cette machine virtuelle, puis accédez à https://mytestapp.ilbase.com. Si vous utilisez un certificat auto-signé, accepter un manque de hello de sécurité.

    adresse IP de Hello pour votre équilibrage de charge interne est répertorié sous **des adresses IP**. Cette liste a également utilisés par l’adresse IP externe de hello et pour le trafic entrant de gestion des adresses IP hello.

    ![Adresse IP de l’ILB][5]

### <a name="web-jobs-functions-and-hello-ilb-ase"></a>Web des travaux, fonctions et hello ASE d’équilibrage de charge interne

Les fonctions et les tâches web sont pris en charge sur un environnement app service Équilibrage de charge interne, mais pour hello toowork portail avec eux, vous devez disposer de site de réseau accès toohello SCM.  Cela signifie que votre navigateur doit être sur un ordinateur hôte est sous ou réseau virtuel de toohello connecté.  

Lorsque vous utilisez des fonctions de Azure sur un environnement app service Équilibrage de charge interne, vous pouvez obtenir un message d’erreur indiquant que « nous ne sommes pas en mesure de tooretrieve vos fonctions pour l’instant. Veuillez réessayer plus tard. » Cette erreur se produit car hello l’interface utilisateur de fonctions s’appuie sur site SCM hello via le protocole HTTPS et le certificat hello n’est pas dans la chaîne du navigateur hello d’approbation. Les tâches Web présente un problème similaire. tooavoid ce problème, vous pouvez effectuer hello suivantes :

- Ajouter un magasin de certificats approuvés hello certificat tooyour. cela débloque Edge et Internet Explorer.
- Utilisez Chrome accéder d’abord site SCM toohello accepter les certificats non approuvés hello et, puis passez toohello portal.
- Utiliser un certificat commercial qui figure dans la chaîne d’approbation de votre navigateur.  Il est préférable de hello.  

## <a name="dns-configuration"></a>Configuration DNS ##

Lorsque vous utilisez une adresse IP externe, hello DNS est géré par Azure. N’importe quelle application créée dans votre ASE est automatiquement ajoutée tooAzure DNS, qui est un serveur DNS public. Dans un environnement ASE ILB, vous devez gérer votre propre service DNS. Pour un domaine donné, telles que _contoso.net_, vous devez toocreate A DNS des enregistrements dans votre système DNS cette adresse d’équilibrage de charge interne point tooyour pour :

- *.contoso.net
- *.scm.contoso.net

Si votre domaine ASE d’équilibrage de charge interne est utilisé pour plusieurs éléments en dehors de cette ASE, vous devrez peut-être toomanage DNS selon le nom d’application. Cette méthode est complexe, car vous devez tooadd chaque nouveau nom d’application dans votre serveur DNS lorsque vous la créez. C’est pourquoi nous vous recommandons d’utiliser un domaine dédié.

## <a name="publish-with-an-ilb-ase"></a>Publier avec un ASE ILB ##

Pour chaque application créée, il existe deux points de terminaison. Dans un ASE ILB, vous avez *&lt;nom d’application>.&lt;domaine ASE ILB>* et *&lt;nom d’application>.scm.&lt;>*. 

nom du site Hello SCM vous amène console appelée hello Kudu toohello **portail avancée**, à l’intérieur hello portail Azure. console de Kudu Hello vous permet d’afficher les variables d’environnement, explorez hello disque, utilisez une console et bien plus encore. Pour plus d’informations, voir [Kudu console for Azure App Service (Console Kudu pour Azure App Service)][Kudu]. 

Dans le mutualisée hello du Service d’applications et dans un environnement app service externe, il est l’authentification unique entre hello portail Azure et de la console de Kudu hello. Pour hello ASE d’équilibrage de charge interne, toutefois, vous devez toouse votre publication toosign d’informations d’identification dans la console de Kudu hello.

Systèmes de l’élément de configuration basé sur Internet, tels que GitHub et Visual Studio Team Services ne fonctionnent pas avec un environnement app service Équilibrage de charge interne, car le point de terminaison publication hello n’est pas accessible d’internet. Au lieu de cela, vous devez toouse un système de l’élément de configuration qui utilise un modèle d’extraction, telles que Dropbox.

les points de terminaison de publication Hello pour les applications dans un environnement app service Équilibrage de charge interne utilisent hello de domaine que hello avec QU'ASE d’équilibrage de charge interne a été créé. Ce domaine s’affiche dans le profil de publication de l’application hello et dans le panneau de portail de l’application hello (**vue d’ensemble** > **Essentials** et **propriétés**). Si vous disposez d’un environnement app service Équilibrage de charge interne avec un sous-domaine de hello *contoso.net* et une application nommée *MonTest*, utilisez *mytest.contoso.net* pour FTP et *mytest.scm.contoso.net*  pour le déploiement web.

## <a name="couple-an-ilb-ase-with-a-waf-device"></a>Coupler un ASE ILB avec un dispositif WAF ##

Azure App Service fournit de nombreuses mesures de sécurité qui protègent hello système. Ils aident également à toodetermine si une application a été piratée. meilleure protection de Hello pour une application web est toocouple une plateforme d’hébergement, tels que le Service application Azure, avec un pare-feu d’applications web (WAF). Hello ASE d’équilibrage de charge interne a un point de terminaison d’application d’isolé du réseau, il est approprié pour une telle utilisation.

toolearn plus en détail comment tooconfigure votre ASE d’équilibrage de charge interne avec un périphérique WAF, consultez [configurer un pare-feu d’applications web avec votre environnement App Service][ASEWAF]. Cet article explique comment toouse appliance Barracuda virtuelle avec votre ASE. Une autre option consiste à toouse passerelle d’Application Azure. Passerelle d’application utilise hello OWASP avoir core règles toosecure toutes les applications placées derrière lui. Pour plus d’informations sur la passerelle d’Application, consultez [pare-feu d’applications web Azure Introduction toohello][AppGW].

## <a name="get-started"></a>Prise en main ##

Tous les articles et procédure-tooinstructions pour ASEs sont disponibles dans le [fichier Lisezmoi pour les environnements App Service][ASEReadme].

* tooget main ASEs, consultez [les environnements de Service Introduction tooApp][Intro].
* Pour plus d’informations sur la plateforme Azure App Service de hello, consultez [Azure App Service](http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/).
 
<!--Image references-->
[1]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-network.png
[2]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-webapp.png
[3]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-certificate.png
[4]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-certificate2.png
[5]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-ipaddresses.png

<!--Links-->
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
