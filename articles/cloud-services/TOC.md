# Vue d’ensemble
## [Présentation de Services cloud](cloud-services-choose-me.md)
## [Création de packages et fichiers de configuration de service cloud](cloud-services-model-and-package.md)

# Prise en main
## [Exemple de service cloud .NET](cloud-services-dotnet-get-started.md)
## [Exemple de service cloud avec les outils Python pour Visual Studio](cloud-services-python-ptvs.md)
## [Configurer un cluster HPC hybride avec Microsoft HPC Pack](cloud-services-setup-hybrid-hpcpack-cluster.md)

# Procédure
## Planification
### [Tailles de machines virtuelles](cloud-services-sizes-specs.md)
### [Mises à jour](cloud-services-update-azure-service.md)

## Développement
### [Créer des rôles web et de travail PHP](../cloud-services-php-create-web-role.md)
### [Créer et déployer une application Node.js](cloud-services-nodejs-develop-deploy-app.md)
### [Créer une application web Node.js avec Express](cloud-services-nodejs-develop-deploy-express-app.md)
### Storage et Visual Studio
#### [Stockage Blob et services connectés](../visual-studio/vs-storage-cloud-services-getting-started-blobs.md)
#### [Stockage File d’attente et services connectés](../visual-studio/vs-storage-cloud-services-getting-started-queues.md)
#### [Stockage Table et services connectés](../visual-studio/vs-storage-cloud-services-getting-started-tables.md)
### Configurer des packages pour une création et un déploiement continu
#### [TFS et Team Build](cloud-services-dotnet-continuous-delivery.md)
### [Configurer les règles de trafic pour un rôle](cloud-services-enable-communication-role-instances.md)
### [Gérer les événements de cycle de vie du service cloud](cloud-services-role-lifecycle-dotnet.md)
### [Socket.io (Node.js)](cloud-services-nodejs-chat-app-socketio.md)
### [Utilisation de Twilio toomake un appel téléphonique (.NET)](../partner-twilio-cloud-services-dotnet-phone-call-web-role.md)
### [New Relic](../store-new-relic-cloud-services-dotnet-application-performance-management.md)

### Configurer des tâches de démarrage
#### [Créer des tâches de démarrage](cloud-services-startup-tasks.md)
#### [Tâches de démarrage courantes](cloud-services-startup-tasks-common.md)
#### [Utilisez une tâche de tooInstall .NET sur un rôle de Service Cloud](cloud-services-dotnet-install-dotnet.md)

### Configurer le Bureau à distance
#### [Portail](cloud-services-role-enable-remote-desktop-new-portal.md)
#### [Portail classique](cloud-services-role-enable-remote-desktop.md)
#### [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md)

## Déployer
### Créer et déployer un service cloud dans le portail
#### [Portail](cloud-services-how-to-create-deploy-portal.md)
#### [Portail classique](cloud-services-how-to-create-deploy.md)
### [Créer un conteneur de service cloud vide dans PowerShell](cloud-services-powershell-create-cloud-container.md)
### Configuration d’un nom de domaine personnalisé
#### [Portail](cloud-services-custom-domain-name-portal.md)
#### [Portail classique](cloud-services-custom-domain-name.md)
### [Effectuer un déploiement intermédiaire d’un service cloud (Node.js)](cloud-services-nodejs-stage-application.md)
### [Se connecter tooa personnalisé contrôleur de domaine](cloud-services-connect-to-custom-domain.md)

## Gérer le service
### Tâches de gestion courantes
#### [Portail](cloud-services-how-to-manage-portal.md)
#### [Portail classique](cloud-services-how-to-manage.md)
### Configurer le service cloud
#### [Portail](cloud-services-how-to-configure-portal.md)
#### [Portail classique](cloud-services-how-to-configure.md)
### [Gérer un service cloud à l’aide d’Azure Automation](automation-manage-cloud-services.md)
### Configurer la mise à l’échelle automatique
#### [Portail](cloud-services-how-to-scale-portal.md)
#### [Portail classique](cloud-services-how-to-scale.md)
### [Utiliser les ressources de Python toomanage Azure](cloud-services-python-how-to-use-service-management.md)

### [Correctifs du SE invité](cloud-services-guestos-msrc-releases.md)
### Suppression du SE invité
#### [Stratégie de suppression](cloud-services-guestos-retirement-policy.md)
#### [Informations relatives à la suppression de la famille 1](cloud-services-guestos-family1-retirement.md)
### [Actualités concernant les versions de SE invité](cloud-services-guestos-update-matrix.md)
### [Aide-mémoire XPath de configuration d’un rôle Services cloud](cloud-services-role-config-xpath.md)

## Gérer des certificats
### [Services cloud et certificats de gestion](cloud-services-certs-create.md)
### Configuration du chiffrement SSL 
#### [Portail](cloud-services-configure-ssl-certificate-portal.md)
#### [Portail classique](cloud-services-configure-ssl-certificate.md)

## Surveiller
### [Surveiller le service cloud](cloud-services-how-to-monitor.md)
### [Tester les performances](../vs-azure-tools-performance-profiling-cloud-services.md)
#### [Tester avec le profileur Visual Studio](cloud-services-performance-testing-visual-studio-profiler.md)
### Activation des diagnostics
#### [PowerShell](cloud-services-diagnostics-powershell.md)
#### [.NET](cloud-services-dotnet-diagnostics.md)
#### [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)
### [Utiliser des compteurs de performances dans les diagnostics Azure](cloud-services-dotnet-diagnostics-performance-counters.md)
### [Stocker et afficher des données de diagnostic dans le stockage Azure](cloud-services-dotnet-diagnostics-storage.md)
### [Suivre un service cloud avec les diagnostics](cloud-services-dotnet-diagnostics-trace-flow.md)
### [Envoyer des données de diagnostic tooApp Insights](cloud-services-dotnet-diagnostics-applicationinsights.md)

## Résolution des problèmes
### Déboguer 
#### [Activer le débogage distant avec la livraison continue](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md)
#### [Options d’un service cloud](../vs-azure-tools-debugging-cloud-services-overview.md)
#### [Service cloud local avec Visual Studio](../vs-azure-tools-debug-cloud-services-virtual-machines.md)
#### [Service cloud publié avec Visual Studio](../vs-azure-tools-intellitrace-debug-published-cloud-services.md)
### [Échec d’allocation de service cloud](cloud-services-allocation-failures.md)
### [Causes courantes de recyclage des rôles de service cloud](cloud-services-troubleshoot-common-issues-which-cause-roles-recycle.md)
### [Taille par défaut du dossier TEMP trop petite pour un rôle](cloud-services-troubleshoot-default-temp-folder-size-too-small-web-worker-role.md)
### [Problèmes de déploiement courants](cloud-services-troubleshoot-deployment-problems.md)
### [Échec de rôle toostart](cloud-services-troubleshoot-roles-that-fail-start.md)
### [Conseils sur la récupération d’urgence](cloud-services-disaster-recovery-guidance.md)
### Forum aux questions sur les services cloud
#### [FAQ sur la disponibilité de l’application et du service](cloud-services-application-and-service-availability-faq.md)
#### [FAQ sur la configuration et la gestion](cloud-services-configuration-and-management-faq.md)
#### [FAQ sur la connectivité et la mise en réseau](cloud-services-connectivity-and-networking-faq.md)
#### [FAQ sur le déploiement](cloud-services-deployment-faq.md)

# Référence
## [Exemples de code](https://azure.microsoft.com/en-us/resources/samples/?service=cloud-services)
## [.csdef XMLSchema](https://msdn.microsoft.com/library/azure/ee758711)
## [.cscfg XMLSchema](https://msdn.microsoft.com/library/azure/ee758710)
## [REST](https://msdn.microsoft.com/library/azure/ee460812)

# Ressources
## [Feuille de route Azure](https://azure.microsoft.com/roadmap/?category=compute)
## [Parcours d’apprentissage](https://azure.microsoft.com/documentation/learning-paths/cloud-services/)
## [Forum MSDN](https://social.msdn.microsoft.com/Forums/en-us/home?forum=windowsazuredevelopment)
## [Tarification](https://azure.microsoft.com/pricing/details/cloud-services/)
## [Calculatrice de prix](https://azure.microsoft.com/pricing/calculator/)
## [Mises à jour de service](https://azure.microsoft.com/updates/?product=cloud-services&updatetype=&platform=)
## [Vidéos](https://azure.microsoft.com/documentation/videos/index/?services=cloud-services)
