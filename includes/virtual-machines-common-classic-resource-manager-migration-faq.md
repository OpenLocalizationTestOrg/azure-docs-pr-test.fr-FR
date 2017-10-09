# <a name="frequently-asked-questions-about-classic-tooazure-resource-manager-migration"></a>Forum aux questions sur classique tooAzure migration du Gestionnaire de ressources

## <a name="does-this-migration-plan-affect-any-of-my-existing-services-or-applications-that-run-on-azure-virtual-machines"></a>Ce plan de migration affecte-t-il l’un de mes services ou applications existants qui s’exécutent sur des machines virtuelles Azure ? 

Non. machines virtuelles de Hello (classiques) sont entièrement prise en charge des services de la disponibilité générale. Vous pouvez continuer à toouse tooexpand de ces ressources votre empreinte sur Microsoft Azure.

## <a name="what-happens-toomy-vms-if-i-dont-plan-on-migrating-in-hello-near-future"></a>Que passe-t-il toomy VMs si vous ne prévoyez pas sur la migration Bonjour futur proche ? 

Nous ne sommes pas désapprouve hello classic API et la ressource de modèle existant. Nous souhaitons toomake migration facile, compte tenu de hello fonctionnalités avancées qui sont disponibles dans le modèle de déploiement du Gestionnaire de ressources hello. Nous vous recommandons vivement de consulter [certaines des améliorations de hello](../articles/azure-resource-manager/resource-manager-deployment-model.md) qui font partie d’IaaS sous le Gestionnaire de ressources.

## <a name="what-does-this-migration-plan-mean-for-my-existing-tooling"></a>Quelles sont les implications de ce plan de migration pour mes outils existants ? 

Mise à jour de votre modèle de déploiement du Gestionnaire de ressources de toohello outils est une des modifications les plus importantes hello que vous avez tooaccount pour dans vos plans de migration.

## <a name="how-long-will-hello-management-plane-downtime-be"></a>La durée pendant laquelle sera temps mort du plan de gestion hello ? 

Il dépend de nombre hello des ressources qui sont en cours de migration. Pour les déploiements plus petits (plusieurs dizaines de machines virtuelles), complet de migration hello doit prendre moins d’une heure. Pour les déploiements à grande échelle (des centaines d’ordinateurs virtuels), migration de hello peut prendre quelques heures.

## <a name="can-i-roll-back-after-my-migrating-resources-are-committed-in-resource-manager"></a>Puis-je procéder à une restauration après avoir validé la migration de mes ressources dans Resource Manager ? 

Vous pouvez annuler votre migration tant que ressources de hello sont Bonjour préparé l’état. La restauration n’est pas prise en charge une fois que les ressources hello ont été correctement migrés via une opération de validation hello.

## <a name="can-i-roll-back-my-migration-if-hello-commit-operation-fails"></a>Puis-je restaurer mon migration si l’opération de validation hello échoue ? 

Impossible d’abandonner la migration si l’opération de validation hello échoue. Toutes les opérations de migration, y compris les opérations de validation hello, sont idempotent. Nous vous recommandons que vous réessayez hello après une courte période. Si vous rencontrez toujours une erreur, créez un ticket de support ou créer un billet de forum avec hello ClassicIaaSMigration balise notre [Forum sur la machine virtuelle](https://social.msdn.microsoft.com/Forums/azure/home?forum=WAVirtualMachinesforWindows).

## <a name="do-i-have-toobuy-another-express-route-circuit-if-i-have-toouse-iaas-under-resource-manager"></a>Dois-je toobuy un autre circuit express route si j’ai toouse IaaS sous le Gestionnaire de ressources ? 

Non. Nous avons récemment activé [déplacement des circuits ExpressRoute à partir du modèle de déploiement du Gestionnaire de ressources hello classique toohello](../articles/expressroute/expressroute-move.md). Vous n’avez toobuy un circuit ExpressRoute de nouveau si vous avez déjà une.

## <a name="what-if-i-had-configured-role-based-access-control-policies-for-my-classic-iaas-resources"></a>Que se passera-t-il si j’ai configuré des stratégies de contrôle d’accès en fonction du rôle (RBAC) pour mes ressources IaaS Classic ? 

Pendant la migration, les ressources de hello transforment de classique tooResource Manager. Par conséquent, nous vous recommandons hello RBAC stratégie mises à jour nécessitant toohappen après la migration.

## <a name="i-backed-up-my-classic-vms-in-a-backup-vault-can-i-migrate-my-vms-from-classic-mode-tooresource-manager-mode-and-protect-them-in-a-recovery-services-vault"></a>J’ai sauvegardé mes machines virtuelles classiques dans un coffre de sauvegarde Azure. Puis-je migrer mes machines virtuelles à partir du mode de gestionnaire tooResource en mode classique et les protéger dans un coffre Recovery Services ? 

Classiques points de récupération de machine virtuelle dans un coffre de sauvegarde ne faire migrer automatiquement le coffre Recovery Services tooa lorsque vous déplacez hello VM de tooResource classique en mode de gestionnaire. Suivez ces étapes tootransfer vos sauvegardes de machine virtuelle :

1. Dans le coffre de sauvegarde hello, accédez à toohello **éléments protégés** onglet et sélectionnez hello machine virtuelle. Cliquez sur [Arrêter la protection](../articles/backup/backup-azure-manage-vms-classic.md#stop-protecting-virtual-machines). Laissez l’option *Supprimer les données de sauvegarde associées***non cochée**.
2. Suppression de l’extension de sauvegarde/capture instantanée hello à partir de la machine virtuelle de hello.
3. Migrer hello virtual machine du mode de gestionnaire tooResource en mode classique. Assurez-vous que les informations réseau et de stockage hello machine virtuelle de toohello correspondante est également migrées dans le mode de gestionnaire tooResource.
4. Créer un coffre Recovery Services et configurer sauvegarde sur hello migrés à l’aide de l’ordinateur virtuel **sauvegarde** action au-dessus du tableau de bord coffre. Pour plus d’informations sur la sauvegarde d’une machine virtuelle tooa Recovery Services coffre, consultez l’article hello, [protéger des machines virtuelles Azure dans un coffre Recovery Services](../articles/backup/backup-azure-vms-first-look-arm.md).

## <a name="can-i-validate-my-subscription-or-resources-toosee-if-theyre-capable-of-migration"></a>Puis-je valider des mon abonnement ou les ressources toosee s’ils sont capables de migration ? 

Oui. Dans l’option de migration de plateforme prise en charge de hello, hello première étape de préparation de migration est toovalidate que les ressources hello sont capables de migration. En cas de hello valider l’opération échoue, vous recevez des messages pour les motifs hello migration de hello ne peut pas être effectuée.

## <a name="what-happens-if-i-run-into-a-quota-error-while-preparing-hello-iaas-resources-for-migration"></a>Que se passe-t-il si j’exécute une erreur de quota lors de la préparation des ressources de hello IaaS pour la migration ? 

Nous vous recommandons d’abandonner votre migration et de s’un quotas de prise en charge de demande tooincrease hello hello région de hello migration machines virtuelles. Une fois la demande de quota hello est approuvée, vous pouvez démarrer l’exécution des étapes de migration hello à nouveau.

## <a name="how-do-i-report-an-issue"></a>Comment signaler un problème ? 

Validez vos problèmes et les questions sur la migration tooour [Forum sur la machine virtuelle](https://social.msdn.microsoft.com/Forums/azure/home?forum=WAVirtualMachinesforWindows), avec le mot clé de hello ClassicIaaSMigration. Nous vous recommandons de poster toutes vos questions sur ce forum. Si vous avez un contrat de prise en charge, vous êtes toolog Bienvenue ainsi un ticket de support.

## <a name="what-if-i-dont-like-hello-names-of-hello-resources-that-hello-platform-chose-during-migration"></a>Que se passe-t-il si je n’aime pas les noms de hello de ressources hello hello plateforme choisi lors de la migration ? 

Toutes les ressources hello que vous fournissez explicitement pour les noms dans le modèle de déploiement classique de hello sont conservés pendant la migration. Dans certains cas, de nouvelles ressources seront créées. Par exemple, une interface réseau est créée pour chaque machine virtuelle. Nous avons actuellement ne prend en charge hello capacité toocontrol hello noms de ces nouvelles ressources créés pendant la migration. Connecter votre voix pour cette fonctionnalité sur hello [forum de commentaires Azure](http://feedback.azure.com).

## <a name="can-i-migrate-expressroute-circuits-used-across-subscriptions-with-authorization-links"></a>Puis-je migrer des circuits ExpressRoute utilisés dans les abonnements avec des liens d’autorisation ? 

Les circuits ExpressRoute utilisant des liens d’autorisation entre abonnements ne peuvent pas être migrés automatiquement sans temps d’arrêt. Il existe des étapes manuelles permettant de migrer ces circuits. Consultez [ExpressRoute de migrer des circuits et associé des réseaux virtuels à partir du modèle de déploiement du Gestionnaire de ressources hello classique toohello](../articles/expressroute/expressroute-migration-classic-resource-manager.md) pour plus d’informations et les étapes.

## <a name="i-got-a-message-vm-is-reporting-hello-overall-agent-status-as-not-ready-hence-hello-vm-cannot-be-migrated-ensure-that-hello-vm-agent-is-reporting-overall-agent-status-as-ready-or-vm-contains-extension-whose-status-is-not-being-reported-from-hello-vm-hence-this-vm-cannot-be-migrated-"></a>J’ai reçu un message *« machine virtuelle est reporting hello état global de l’agent en tant que non prêt. Par conséquent, hello machine virtuelle ne peut pas être migré. Vérifiez que l’Agent de machine virtuelle hello est signalent l’état de l’agent global comme prêt »* ou * « machine virtuelle contient une Extension dont l’état n’est pas signalée à partir de la machine virtuelle de hello. Par conséquent, elle ne peut pas faire l’objet d’une migration. ». *

Ce message est reçu lorsque hello machine virtuelle n’a pas de connectivité sortante toohello internet. agent de machine virtuelle Hello utilise le compte de stockage Azure hello connectivité sortante tooreach de mise à jour d’état de l’agent hello toutes les cinq minutes.
