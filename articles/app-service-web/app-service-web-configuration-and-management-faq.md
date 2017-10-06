---
title: aaaConfiguration FAQ pour les applications web Azure | Documents Microsoft
description: "Obtenir elles sonttrop des réponses aux questions sur la configuration et les problèmes de gestion pour la fonctionnalité d’applications Web hello du Service d’applications Azure."
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 5aa405582813291a4aaf144d2f821ecb20a5edcb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configuration-and-management-faqs-for-web-apps-in-azure"></a>FAQ sur la configuration et la gestion de Web Apps dans Azure

Cet article a elles sonttrop des réponses aux questions (FAQ) sur les problèmes de configuration et de gestion pour hello [fonctionnalité des applications Web d’Azure App Service](https://azure.microsoft.com/services/app-service/web/).

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="are-there-limitations-i-should-be-aware-of-if-i-want-toomove-app-service-resources"></a>Existe-t-il des limitations que je dois être conscient de lise de ressources du Service de l’application toomove ?

Si vous envisagez de toomove du Service d’applications ressources tooa nouveau groupe de ressources ou d’un abonnement, il existe quelques limitations toobe prenant en charge de. Pour en savoir plus, voir [Limitations d’App Service](../azure-resource-manager/resource-group-move-resources.md#app-service-limitations).

## <a name="how-do-i-use-a-custom-domain-name-for-my-web-app"></a>Comment utiliser un nom de domaine personnalisé pour mon application web ?

Pour les réponses aux questions de toocommon sur l’utilisation d’un nom de domaine personnalisé avec votre application web Azure, consultez notre vidéo de sept minutes [ajouter un nom de domaine personnalisé](https://channel9.msdn.com/blogs/Azure-App-Service-Self-Help/Add-a-Custom-Domain-Name). Hello vidéo offre une procédure pas à pas tooadd un nom de domaine personnalisé. Il décrit comment toouse URL de votre propre au lieu de hello *. URL azurewebsites.net avec votre application web de Service d’applications. Vous pouvez également voir une description détaillée de [comment toomap un nom de domaine personnalisé](web-sites-custom-domain-name.md).


## <a name="how-do-i-purchase-a-new-custom-domain-for-my-web-app"></a>Comment acheter un domaine personnalisé pour mon application web ?

toolearn comment toopurchase et configurer un domaine personnalisé pour votre application web du Service d’applications, consultez [acheter et configurer un nom de domaine personnalisé dans le Service d’applications](custom-dns-web-site-buydomains-web-app.md).


## <a name="how-do-i-upload-and-configure-an-existing-ssl-certificate-for-my-web-app"></a>Comment charger et configurer un certificat SSL existant pour mon application web ?

toolearn comment tooupload et configurer un certificat SSL personnalisé existant, consultez [lier une personnalisé SSL certificat tooan Azure application web existante](app-service-web-tutorial-custom-ssl.md#upload).


## <a name="how-do-i-purchase-and-configure-a-new-ssl-certificate-in-azure-for-my-web-app"></a>Comment acheter et configurer un nouveau certificat SSL dans Azure pour mon application web ?

toolearn comment toopurchase et configurer un certificat SSL pour votre application web du Service d’applications, consultez [ajouter un tooyour de certificat SSL du Service d’applications application](web-sites-purchase-ssl-web-site.md).


## <a name="how-do-i-move-application-insights-resources"></a>Comment déplacer des ressources Application Insights ?

Actuellement, Azure Application Insights ne prend en charge d’opération de déplacement hello. Si votre groupe de ressources d’origine inclut une ressource Application Insights, vous ne pouvez pas la déplacer. Si vous incluez des ressources d’Application Insights hello lorsque vous essayez de toomove une application de Service d’applications, hello entière déplacer échoue. Toutefois, Application Insights et hello du Service d’applications plan n’est pas nécessaire de toobe dans hello même groupe de ressources en tant qu’application hello pour hello application toofunction correctement.

Pour en savoir plus, voir [Limitations d’App Service](../azure-resource-manager/resource-group-move-resources.md#app-service-limitations).

## <a name="where-can-i-find-a-guidance-checklist-and-learn-more-about-resource-move-operations"></a>Où trouver une liste de conseils et en savoir plus sur les opérations de déplacement de ressources ?

[Limitations du Service d’applications](../azure-resource-manager/resource-group-move-resources.md#app-service-limitations) vous montre comment toomove ressources tooeither un nouvel abonnement ou tooa nouvelle ressource groupe Bonjour même abonnement. Vous pouvez obtenir des informations sur la liste de vérification déplacement de ressources hello, Découvrez les services qui prennent en charge d’opération de déplacement hello et en savoir plus sur les limitations du Service d’applications et d’autres rubriques.

## <a name="how-do-i-set-hello-server-time-zone-for-my-web-app"></a>Comment définir le fuseau horaire du serveur hello pour mon application web ?

tooset hello serveur horaire pour votre application web :

1. Bonjour portail Azure, dans votre abonnement au Service de l’application, accédez à toohello **paramètres de l’Application** menu.
2. Sous **Paramètres de l’application**, ajoutez le paramètre suivant :
    * Key = WEBSITE_TIME_ZONE
    * Valeur = *hello fuseau horaire*
3. Sélectionnez **Enregistrer**.

## <a name="why-do-my-continuous-webjobs-sometimes-fail"></a>Pourquoi mes tâches web continues échouent-elles parfois ?

Par défaut, les applications web sont déchargées si elles restent inactives pendant un laps de temps défini. Cela permet de préserver les ressources système de hello. Dans les plans de base et Standard, vous pouvez activer hello **Always On** paramètre tookeep hello web application chargée de tout temps hello. Si votre application web s’exécute des tâches Web continues, vous devez activer **Always On**, ou hello tâches Web peuvent ne pas fonctionner de manière fiable. Pour plus d’informations, voir [Création d’une tâche web exécutée en continu](web-sites-create-web-jobs.md#CreateContinuous).

## <a name="how-do-i-get-hello-outbound-ip-address-for-my-web-app"></a>Comment obtenir les adresses IP sortant hello pour mon application web ?

liste de hello tooget des adresses IP sortant pour votre application web :

1. Bonjour portail Azure, dans votre panneau d’application web, accédez à toohello **propriétés** menu.
2. Recherchez les **adresses IP sortantes**.

liste Hello sortant adresses IP s’affiche.

Si votre site Web est hébergé dans un environnement App Service pour PowerApps, toolearn comment tooget votre adresse IP sortante, consultez [adresses réseau sortant](app-service-app-service-environment-network-architecture-overview.md#outbound-network-addresses).

## <a name="how-do-i-get-a-reserved-or-dedicated-inbound-ip-address-for-my-web-app"></a>Comment obtenir une adresse IP entrante réservée ou dédiée pour mon application web ?

tooset une adresse IP dédiée ou réservés pour les appels entrants effectués tooyour site Web d’application Azure, installez et configurez un certificat SSL basé sur IP.

Notez que toouse dédiée ou adresse IP réservée pour les appels entrants, votre plan App Service doit être dans un plan de service de base ou une version ultérieure.

## <a name="can-i-export-my-app-service-certificate-toouse-outside-azure-such-as-for-a-website-hosted-elsewhere"></a>Puis-je exporter me toouse de certificat du Service d’applications en dehors d’Azure, telles que pour un site Web hébergé ailleurs ? 

Les certificats App Service sont considérés comme des ressources Azure. Ils ne sont pas toouse prévue en dehors de vos services Azure. Vous ne pouvez pas exporter toouse en dehors d’Azure. Pour plus d’informations, voir [FAQ sur les certificats App Service et les domaines personnalisés](https://social.msdn.microsoft.com/Forums/azure/f3e6faeb-5ed4-435a-adaa-987d5db43b80/faq-on-app-service-certificates-and-custom-domains?forum=windowsazurewebsitespreview).

## <a name="can-i-export-my-app-service-certificate-toouse-with-other-azure-cloud-services"></a>Puis-je exporter me toouse de certificat du Service d’applications avec d’autres services cloud Azure ?

portail de Hello fournit une expérience de première classe pour le déploiement d’un certificat de Service d’applications via des applications de Service Azure Key Vault tooApp. Toutefois, nous avons reçu des demandes des clients toouse ces certificats à l’extérieur de hello plateforme de Service de l’application, par exemple, avec des Machines virtuelles Azure. toolearn comment toocreate une copie PFX locale de votre application de Service de certificats afin de pouvoir utiliser les certificats hello avec d’autres ressources Azure, consultez [créer une copie locale de PFX d’un certificat de Service d’applications](https://blogs.msdn.microsoft.com/appserviceteam/2017/02/24/creating-a-local-pfx-copy-of-app-service-certificate/).

Pour plus d’informations, voir [FAQ sur les certificats App Service et les domaines personnalisés](https://social.msdn.microsoft.com/Forums/azure/f3e6faeb-5ed4-435a-adaa-987d5db43b80/faq-on-app-service-certificates-and-custom-domains?forum=windowsazurewebsitespreview).


## <a name="why-do-i-see-hello-message-partially-succeeded-when-i-try-tooback-up-my-web-app"></a>Pourquoi le message de salutation « Partiellement réussie » lors de le tooback mon application web ?

Une cause courante de l’échec de la sauvegarde est que certains fichiers sont en cours d’utilisation par une application hello. Les fichiers qui sont en cours d’utilisation sont verrouillées pendant que vous effectuez la sauvegarde de hello. Cela empêche la sauvegarde de ces fichiers et peut aboutir à l’état « Partiellement réussie ». Vous pouvez éventuellement empêcher cela en excluant les fichiers de processus de sauvegarde hello. Vous pouvez choisir tooback des uniquement, ce qui est nécessaire. Pour plus d’informations, consultez [sauvegarde simplement hello parties importantes de votre site avec les applications web Azure](http://www.zainrizvi.io/2015/06/05/creating-partial-backups-of-your-site-with-azure-web-apps/).

## <a name="how-do-i-remove-a-header-from-hello-http-response"></a>Comment supprimer un en-tête de réponse HTTP de hello ?

en-têtes de hello tooremove hello réponse HTTP, mettre à jour le fichier web.config de votre site. Pour plus d’informations, voir [Supprimer les en-têtes de serveur standard sur vos sites web Azure](https://azure.microsoft.com/blog/removing-standard-server-headers-on-windows-azure-web-sites/).

## <a name="is-app-service-compliant-with-pci-standard-30-and-31"></a>App Service est-il conforme aux normes PCI 3.0 et 3.1 ?

Actuellement, hello Web Apps fonctionnalité Azure App Service est en conformité avec la version de sécurité Standard PCI données (DSS) 3.0 de niveau 1. La certification PCI DSS version 3.1 figure sur notre feuille de route. La planification est déjà en cours d’exécution pour comment l’adoption de la norme de dernière hello se poursuit.

La certification PCI DSS version 3.1 nécessite la désactivation du protocole TLS version 1.0. Actuellement, la désactivation de TLS 1.0 n’est pas une option pour la plupart des plans App Service. Toutefois, si vous utilisez l’environnement App Service ou toomigrate disposé votre environnement de Service de tooApp la charge de travail, vous pouvez obtenir le plus grand contrôle de votre environnement. Cela implique de désactiver le protocole TLS 1.0 avec l’aide du support technique Azure. Bonjour proche avenir, nous prévoyons de toomake ces toousers accessible de paramètres.

Pour plus d’informations, voir [Conformité des applications web Microsoft Azure App Service avec les normes PCI 3.0 et 3.1](https://support.microsoft.com/help/3124528).

## <a name="how-do-i-use-hello-staging-environment-and-deployment-slots"></a>Utilisation de l’environnement et les emplacements de déploiement de mise en lots de hello

Dans les plans Standard et Premium du Service d’applications, lorsque vous déployez votre tooApp d’application web Service, vous pouvez déployer tooa emplacement de déploiement distinct au lieu de l’emplacement de production toohello par défaut. Les emplacements de déploiement sont des applications web dynamiques qui ont leurs propres noms d’hôte. Éléments de configuration et de contenu Web application peuvent être échangés entre deux emplacements de déploiement, y compris l’emplacement de production hello.

Pour plus d’informations sur l’utilisation des emplacements de déploiement, voir [Configurer des environnements intermédiaires dans Azure App Service](web-sites-staged-publishing.md).

## <a name="how-do-i-access-and-review-webjob-logs"></a>Comment accéder aux journaux de tâche web (WebJob) et les consulter ?

journaux de la tâche Web tooreview :

1. Connectez-vous à tooyour [site Web de Kudu](https://*yourwebsitename*.scm.azurewebsites.net).
2. Sélectionnez hello la tâche Web.
3. Sélectionnez hello **bascule sortie** bouton.
4. fichier de sortie toodownload hello, sélectionnez hello **télécharger** lien.
5. Pour des exécutions individuelles, sélectionnez **Appel individuel**.
6. Sélectionnez hello **bascule sortie** bouton.
7. Sélectionnez hello de lien de téléchargement.

## <a name="im-trying-toouse-hybrid-connections-with-sql-server-why-do-i-see-hello-message-systemoverflowexception-arithmetic-operation-resulted-in-an-overflow"></a>J’essaie de connexions hybrides de toouse avec SQL Server. Pourquoi les messages hello « System.OverflowException : opération arithmétique a entraîné un dépassement de capacité » ?

Si vous utilisez des connexions hybrides tooaccess SQL Server, une mise à jour de Microsoft .NET sur 10 mai 2016, peut entraîner des connexions toofail. Le message suivant pourrait s’afficher :

```
Exception: System.Data.Entity.Core.EntityException: hello underlying provider failed on Open. —> System.OverflowException: Arithmetic operation resulted in an overflow. or (64 bit Web app) System.OverflowException: Array dimensions exceeded supported range, at System.Data.SqlClient.TdsParser.ConsumePreLoginHandshake
```

### <a name="resolution"></a>Résolution :

Nous travaillons tooupdate toofix du Gestionnaire de connexions hybrides ce problème. Pour des solutions de contournement, voir [Erreur de connexion hybride avec SQL Server : System.OverflowException : L’opération arithmétique a provoqué un dépassement de capacité](https://blogs.msdn.microsoft.com/waws/2016/05/17/hybrid-connection-error-with-sql-server-system-overflowexception-arithmetic-operation-resulted-in-an-overflow/).

## <a name="how-do-i-add-or-edit-a-url-rewrite-rule"></a>Comment ajouter ou modifier une règle de réécriture d’URL ?

tooadd ou modifier une règle de réécriture d’URL :

1. Configurer le Gestionnaire des Services Internet (IIS) afin qu’il connecte tooyour application Service web d’application. toolearn tooconnect tooApp du Gestionnaire des services Internet Service, voir [administration à distance de sites Web Azure à l’aide du Gestionnaire des services Internet](https://azure.microsoft.com/blog/remote-administration-of-windows-azure-websites-using-iis-manager/).
2. Dans le Gestionnaire des Services Internet (IIS), ajoutez ou modifiez une règle de réécriture d’URL. toolearn comment tooadd ou modifier une URL de réécriture règle, consultez [module de réécriture de créer des règles de réécriture d’URL de hello](https://www.iis.net/learn/extensions/url-rewrite-module/creating-rewrite-rules-for-the-url-rewrite-module).

## <a name="how-do-i-control-inbound-traffic-tooapp-service"></a>Comment contrôler le trafic entrant tooApp Service ?

Au niveau du site hello, vous avez deux options pour contrôler le trafic entrant tooApp Service :

* Activer les restrictions dynamiques d’adresse IP. toolearn tooturn sur les restrictions IP dynamiques, voir [restrictions IP et de domaine pour les sites Web Azure](https://azure.microsoft.com/blog/ip-and-domain-restrictions-for-windows-azure-web-sites/).
* Activer la sécurité du module. toolearn tooturn sur le Module de sécurité, voir [ModSecurity pare-feu d’applications web sur des sites Web Azure](https://azure.microsoft.com/blog/modsecurity-for-azure-websites/).

Si vous utilisez App Service Environment, vous pouvez utiliser le [pare-feu Barracuda](https://azure.microsoft.com/blog/configuring-barracuda-web-application-firewall-for-azure-app-service-environment/).

## <a name="how-do-i-block-ports-in-an-app-service-web-app"></a>Comment bloquer des ports dans une application web App Service ?

Bonjour du Service d’applications partagé environnement du client, il n’est pas possible de tooblock des ports spécifiques en raison de l’infrastructure de hello de hello. Les ports TCP 4020, 4016 et 4018 pourraient également être ouverts pour un débogage à distance dans Visual Studio.

Dans App Service Environment, vous contrôlez totalement les trafics entrant et sortant. Vous pouvez utiliser des groupes de sécurité réseau toorestrict ou bloc de ports spécifiques. Pour plus d’informations sur App Service Environment, voir [Présentation d’App Service Environment](https://azure.microsoft.com/blog/introducing-app-service-environment/).

## <a name="how-do-i-capture-an-f12-trace"></a>Comment capturer une trace F12

Pour capturer une trace F12, vous disposez de deux options :

* Trace HTTP F12
* Sortie de la console F12

### <a name="f12-http-trace"></a>Sortie console F12

1. Dans Internet Explorer, accédez à tooyour site. Il est important toosign avant de vous hello les étapes suivantes. Dans le cas contraire, hello F12 trace capture des données d’authentification sensibles.
2. Appuyez sur F12.
3. Vérifiez que hello **réseau** onglet est sélectionné, puis sélectionnez hello verte **lire** bouton.
4. Hello étapes pour reproduire le problème de hello.
5. Sélectionnez hello rouge **arrêter** bouton.
6. Sélectionnez hello **enregistrer** bouton (icône de disquette), enregistrez le dernier hello (dans Internet Explorer et le bord) *ou* dernier hello d’avec le bouton droit et sélectionnez **enregistrer en tant que HAR avec un contenu** () dans Chrome).

### <a name="f12-console-output"></a>Sortie de la console F12

1. Sélectionnez hello **Console** onglet.
2. Pour chaque onglet contient un nombre supérieur à zéro d’éléments, sélectionnez l’onglet de hello (**erreur**, **avertissement**, ou **informations**). Si l’onglet de hello n’est pas sélectionnée, icône d’onglet hello est gris ou le noir lorsque vous déplacez le curseur hello en dehors de celui-ci.
3. Avec le bouton droit dans la zone de message de salutation du volet de hello, puis sélectionnez **copier tous les**.
4. Hello de coller copié du texte dans un fichier, puis enregistrez les fichiers hello.

tooview un fichier HAR, vous pouvez utiliser hello [visionneuse HAR](http://www.softwareishard.com/har/viewer/).

## <a name="why-do-i-get-an-error-when-i-try-tooconnect-an-app-service-web-app-tooa-virtual-network-that-is-connected-tooexpressroute"></a>Je reçois une erreur lors de le tooconnect un Service d’application web application tooa réseau virtuel qui est connecté tooExpressRoute ?

Si vous essayez de tooconnect un Azure web app tooa réseau virtuel qui s’est connecté à tooAzure ExpressRoute, elle échoue. Hello message suivant s’affiche : « Passerelle n’est pas une passerelle VPN. »

Actuellement, vous ne peut pas avoir de point-to-site VPN connexions tooa réseau virtuel qui est connecté tooExpressRoute. Un point-to-site VPN et ExpressRoute ne peuvent pas coexister pour hello même réseau virtuel. Pour plus d’informations, voir [Limites et limitations d’ExpressRoute et des connexions VPN site à site](../expressroute/expressroute-howto-coexist-classic.md#limits-and-limitations).

## <a name="how-do-i-connect-an-app-service-web-app-tooa-virtual-network-that-has-a-static-routing-policy-based-gateway"></a>Comment se connecter un application web application tooa réseau virtuel du Service qui a une passerelle (basée sur une stratégie) de routage statique ?

Actuellement, la connexion à un Service d’application web application tooa réseau virtuel qui a une passerelle (basée sur une stratégie) de routage statique n’est pas pris en charge. Si votre réseau virtuel cible existe déjà, il doit avoir des VPN de point-to-site activé avec une passerelle de routage dynamique, avant de pouvoir être connectés tooan application. Si votre passerelle est toostatic routage, vous ne pouvez pas activer un VPN de point-to-site. 

Pour plus d’informations, voir [Intégrer une application à un réseau Azure Virtual Network](web-sites-integrate-with-vnet.md#getting-started).

## <a name="in-my-app-service-environment-why-can-i-create-only-one-app-service-plan-even-though-i-have-two-workers-available"></a>Dans mon App Service Environment, pourquoi ne puis-je créer qu’un seul plan App Service, même si j’ai deux workers disponibles ?

la tolérance de panne tooprovide, environnement App Service nécessite que chaque pool de travail doit au moins une ressource de calcul supplémentaire. ressources de calcul supplémentaires Hello ne peut pas être assigné à une charge de travail.

Pour plus d’informations, consultez [comment toocreate un environnement App Service](app-service-web-how-to-create-an-app-service-environment.md).

## <a name="why-do-i-see-timeouts-when-i-try-toocreate-an-app-service-environment"></a>Pourquoi les délais d’attente lors de le toocreate un environnement App Service ?

Parfois, la création d’un App Service Environment échoue. Dans ce cas, vous voyez hello Bonjour Qu'activité enregistre l’erreur suivante :
```
ResourceID: /subscriptions/{SubscriptionID}/resourceGroups/Default-Networking/providers/Microsoft.Web/hostingEnvironments/{ASEname}
Error:{"error":{"code":"ResourceDeploymentFailure","message":"hello resource provision operation did not complete within hello allowed timeout period.”}}
```

tooresolve, assurez-vous qu’aucun des hello conditions suivantes sont remplies :
* sous-réseau de Hello est trop petite.
* sous-réseau de Hello n’est pas vide.
* ExpressRoute empêche les besoins en connectivité réseau hello d’un environnement App Service.
* Un groupe de sécurité réseau incorrecte empêche les besoins en connectivité réseau hello d’un environnement App Service.
* Le tunneling forcé est activé.

Pour plus d’informations, voir [Problèmes les plus fréquents lors du déploiement (création) d’un nouvel App Service Environment Azure](https://blogs.msdn.microsoft.com/waws/2016/05/13/most-frequent-issues-when-deploying-creating-a-new-azure-app-service-environment-ase/).

## <a name="why-cant-i-delete-my-app-service-plan"></a>Pourquoi ne puis-je pas supprimer mon plan App Service ?

Vous ne pouvez pas supprimer un plan App Service si toutes les applications de Service d’application sont associées à hello plan App Service. Avant de supprimer un plan App Service, supprimez toutes les applications de Service d’applications associées hello plan App Service.

## <a name="how-do-i-schedule-a-webjob"></a>Comment planifier une tâche web ?

Vous pouvez créer une tâche web planifiée à l’aide d’expressions CRON :

1. Créez un fichier settings.job.
2. Dans ce fichier JSON, incluez une propriété de planification à l’aide d’une expression CRON : 
    ```
    { "schedule": "{second}
    {minute} {hour} {day}
    {month} {day of hello week}" }
    ```

Pour plus d’informations sur les tâches web planifiées, voir [Créer une tâche web planifiée à l’aide d’une expression CRON](web-sites-create-web-jobs.md#CreateScheduledCRON).

## <a name="how-do-i-perform-penetration-testing-for-my-app-service-app"></a>Comment effectuer un test de pénétration pour mon application App Service ?

tests d’intrusion tooperform, [soumettre une demande de](https://security-forms.azure.com/penetration-testing/terms).

## <a name="how-do-i-configure-a-custom-domain-name-for-an-app-service-web-app-that-uses-traffic-manager"></a>Comment configurer un nom de domaine personnalisé pour une application web App Service utilisant Traffic Manager?

toolearn toouse un nom de domaine personnalisé avec une application de Service de l’application qui utilise Azure Traffic Manager pour l’équilibrage de charge, voir [configurer un nom de domaine personnalisé pour une application web Azure avec Traffic Manager](web-sites-traffic-manager-custom-domain-name.md).

## <a name="my-app-service-certificate-is-flagged-for-fraud-how-do-i-resolve-this"></a>Mon certificat App Service est marqué pour une fraude. Comment résoudre ce problème ?

Lors de la vérification de domaine hello d’un fournisseur de certificat du Service d’applications, vous pouvez voir hello message suivant :

« Votre certificat a été marqué, car il est possible qu’il soit frauduleux. Hello demande est actuellement en cours de validation. Si le certificat de hello n’est pas utilisable dans les 24 heures, consultez le support Azure. »

Comme le message de type hello indique, ce processus de vérification de fraude peut prendre too24 heures toocomplete. Pendant ce temps, vous allez continuer toosee message de type hello.

Si votre certificat de Service de l’application continue tooshow ce message après 24 heures, exécutez hello suite du script PowerShell. hello de contacts Hello script [fournisseur certificate](https://www.godaddy.com/) directement le problème de hello tooresolve.

```
Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId <subId>
$actionProperties = @{
    "Name"= "<Customer Email Address>"
    };
Invoke-AzureRmResourceAction -ResourceGroupName "<App Service Certificate Resource Group Name>" -ResourceType Microsoft.CertificateRegistration/certificateOrders -ResourceName "<App Service Certificate Resource Name>" -Action resendRequestEmails -Parameters $actionProperties -ApiVersion 2015-08-01 -Force   
```

## <a name="how-do-authentication-and-authorization-work-in-app-service"></a>Comment fonctionnent l’authentification et l’autorisation dans Azure App Service

Pour une documentation détaillée concernant l’authentification et l’autorisation dans App Service, voir [Sécurité dans Azure App Service](../app-service/app-service-security-readme.md). documentation de Hello comporte également des informations sur la configuration du Service d’applications toouse différents identifient le fournisseur de connexions :
* [Azure Active Directory](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)
* [Facebook](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md)
* [Google](../app-service-mobile/app-service-mobile-how-to-configure-google-authentication.md)
* [Compte Microsoft](../app-service-mobile/app-service-mobile-how-to-configure-microsoft-authentication.md)
* [Twitter](../app-service-mobile/app-service-mobile-how-to-configure-twitter-authentication.md)

## <a name="how-do-i-redirect-hello-default-azurewebsitesnet-domain-toomy-azure-web-apps-custom-domain"></a>Comment rediriger les par défaut de hello *. domaine personnalisé de l’application web Azure azurewebsites.net domaine toomy ?

Lorsque vous créez un nouveau site Web à l’aide de Web Apps dans Azure, une valeur par défaut *sitename*. azurewebsites.net attribué tooyour site. Si vous ajoutez un site tooyour de nom d’hôte personnalisé et que vous ne souhaitez pas que tooaccess en mesure de toobe les utilisateurs par défaut *. azurewebsites.net domaine, vous pouvez rediriger les URL par défaut de hello. toolearn tooredirect tout le trafic à partir par défaut domaine tooyour domaine personnalisé de votre site Web, voir [redirection hello domaine par défaut domaine tooyour personnalisée dans les applications web Azure](http://www.zainrizvi.io/2016/04/07/block-default-azure-websites-domain/).

## <a name="how-do-i-determine-which-version-of-net-version-is-installed-in-app-service"></a>Comment déterminer la version de .NET installée dans App Service ?

Hello plus rapide moyen toofind hello version de Microsoft .NET, qui est installé dans le Service de l’application est à l’aide de la console de Kudu hello. Console de Kudu hello accessible à partir du portail de hello ou à l’aide des URL de hello de votre application de Service d’applications. Pour obtenir des instructions détaillées, consultez [identifier la version .NET hello installé dans le Service d’applications](https://blogs.msdn.microsoft.com/waws/2016/11/02/how-to-determine-the-installed-net-version-in-azure-app-services/).

## <a name="why-isnt-autoscale-working-as-expected"></a>Pourquoi la mise à l’échelle automatique ne fonctionne-t-elle pas comme prévu ?

Si Azure mise à l’échelle n’a pas mis à l’échelle dans ou à l’échelle à l’instance d’application hello web comme prévu, vous pouvez exécuter dans un scénario dans lequel nous intentionnellement ne choisir pas tooscale tooavoid une boucle infinie en raison du trop « bagottement ». Cela se produit généralement lorsqu’il n’est pas une marge suffisante entre les seuils de montée en puissance parallèle et de mise à l’échelle hello. toolearn comment tooavoid « bagottement » et tooread sur les autres meilleures pratiques de mise à l’échelle, consultez [mise à l’échelle les meilleures pratiques](../monitoring-and-diagnostics/insights-autoscale-best-practices.md#autoscale-best-practices).

## <a name="why-does-autoscale-sometimes-scale-only-partially"></a>Pourquoi la mise à l’échelle automatique n’opère-t-elle parfois que partiellement ?

Une mise à l’échelle est déclenchée quand des métriques dépassent les limites préconfigurées. Parfois, vous pouvez remarquer que la capacité de hello n'est que partiellement comparé toowhat prévu. Cela peut se produire lorsque le nombre de hello d’instances n’est pas disponible. Dans ce scénario, mise à l’échelle est partiellement remplit avec le nombre disponible de hello d’instances. Mise à l’échelle exécute ensuite hello rééquilibrage logique tooget plus de capacité. Il alloue hello restant d’instances. Notez que cela peut prendre quelques minutes.

Si vous ne voyez pas nombre hello attendu d’instances après quelques minutes, il peut être, car le remplissage partielle de hello était assez métriques de hello toobring dans les limites de hello. Ou bien, mise à l’échelle peut avoir mis à l’échelle vers le bas, car il a atteint la limite de métriques hello inférieure.

Si aucune de ces conditions s’appliquent et hello problème persiste, envoyez une demande de prise en charge.

## <a name="how-do-i-turn-on-http-compression-for-my-content"></a>Comment activer sur la compression HTTP pour mon contenu ?

tooturn sur la compression pour les types de contenu statiques et dynamiques, ajoutez hello le fichier web.config de niveau application code toohello suivant :

```
<system.webServer>
<urlCompression doStaticCompression="true" doDynamicCompression="true" />
< /system.webServer>
```

Vous pouvez également spécifier dynamique spécifique de hello et les types MIME statique que vous souhaitez toocompress. Pour plus d’informations, consultez notre question réponse sur le forum tooa dans [paramètres httpCompression sur un site Web de Azure simple](https://social.msdn.microsoft.com/Forums/azure/890b6d25-f7dd-4272-8970-da7798bcf25d/httpcompression-settings-on-a-simple-azure-website?forum=windowsazurewebsitespreview).

## <a name="how-do-i-migrate-from-an-on-premises-environment-tooapp-service"></a>Comment migrer à partir d’un tooApp d’environnement local Service ?

sites toomigrate à partir de Windows et Linux tooApp de serveurs web Service, vous pouvez utiliser l’Assistant Migration du Service Azure App. outil de migration Hello crée les bases de données et les applications web dans Azure en fonction des besoins et publie ensuite le contenu de hello. Pour plus d’informations, voir [Assistant Migration d’Azure App Service](https://www.movemetothecloud.net/).
