# Vue d’ensemble
## [Qu’est-ce qu’Azure Active Directory ?](active-directory-whatis.md)
## [À propos de la gestion des identités Azure](identity-fundamentals.md)
## [Comprendre les solutions d’identité Azure](understand-azure-identity-solutions.md)
## [Choisir une solution d’identité hybride](choose-hybrid-identity-solution.md)
## [Associer les abonnements Azure](active-directory-how-subscriptions-associated-directory.md)
## [FAQ](active-directory-faq.md)
## [Nouveautés](whats-new.md)


# Prise en main
## [Prise en main d'Azure AD](get-started-azure-ad.md)
## [S’inscrire à Azure AD Premium](active-directory-get-started-premium.md)
## [Ajouter un nom de domaine personnalisé](add-custom-domain.md)
## [Configurer la marque de la société](customize-branding.md)
## [Ajouter des utilisateurs dans Azure AD](add-users-azure-active-directory.md)
## [Attribuer des licences à des utilisateurs](license-users-groups.md)
## [Configurer la réinitialisation du mot de passe libre-service](active-directory-passwords-getting-started.md)


# Procédures
## Planifier et concevoir
### [Comprendre l’architecture Azure AD](active-directory-architecture.md)
### [Mappage des revendications dans Azure Active Directory](active-directory-claims-mapping.md)
### [Déployer une solution d’identité hybride](active-directory-hybrid-identity-design-considerations-overview.md)
#### Déterminer la configuration requise
##### [Identité](active-directory-hybrid-identity-design-considerations-business-needs.md)
##### [Synchronisation d’annuaires](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md)
##### [Serveurs MFA](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)
##### [Stratégie votre cycle de vie des identités](active-directory-hybrid-identity-design-considerations-lifecycle-adoption-strategy.md)
#### [Planifier la sécurité des données](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md)
##### [Protection des données](active-directory-hybrid-identity-design-considerations-dataprotection-requirements.md)
##### [Gestion de contenu](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md)
##### [Contrôle d’accès](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)
##### [Réponse aux incidents](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md)
#### Planifier votre cycle de vie des identités
##### [Tâches :](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md)
##### [Stratégie d’adoption](active-directory-hybrid-identity-design-considerations-identity-adoption-strategy.md)
#### [Étapes suivantes](active-directory-hybrid-identity-design-considerations-nextsteps.md)
#### [Comparaison d’outils](active-directory-hybrid-identity-design-considerations-tools-comparison.md)

## Gestion des utilisateurs
### [Ajouter de nouveaux utilisateurs dans Azure AD](add-users-azure-active-directory.md)
### [Gérer les profils utilisateur](active-directory-users-profile-azure-portal.md)
### [Partager des comptes](active-directory-sharing-accounts.md)
### [Affecter des utilisateurs aux rôles d’administration](active-directory-users-assign-role-azure-portal.md)
### [Restaurer un utilisateur supprimé](active-directory-users-restore.md)
### [Ajouter des utilisateurs invités à partir d’un autre répertoire (B2B)](active-directory-b2b-what-is-azure-ad-b2b.md)
#### [Ajout d’utilisateurs B2B par des administrateurs](active-directory-b2b-admin-add-users.md)
#### [Ajout d’utilisateurs B2B par des membres de l’équipe informatique](active-directory-b2b-iw-add-users.md)
#### [API et personnalisation](active-directory-b2b-api.md)
#### [Code et exemples Azure PowerShell](active-directory-b2b-code-samples.md)
#### [Exemple de portail de connexion libre-service](active-directory-b2b-self-service-portal.md)
#### [E-mail d’invitation](active-directory-b2b-invitation-email.md)
#### [Échange d’invitation](active-directory-b2b-redemption-experience.md)
#### [Ajouter des utilisateurs B2B sans invitation](active-directory-b2b-add-user-without-invite.md)
#### [Accès conditionnel pour B2B](active-directory-b2b-mfa-instructions.md)
#### [Stratégies de partage B2B](active-directory-b2b-delegate-invitations.md)
#### [Ajouter un utilisateur B2B à un rôle](active-directory-b2b-add-guest-to-role.md)
#### [Groupes dynamiques et utilisateurs B2B](active-directory-b2b-dynamic-groups.md)
#### [Audit et création de rapports](active-directory-b2b-auditing-and-reporting.md)
#### [B2B pour les organisations hybrides](active-directory-b2b-hybrid-organizations.md)
#### [Partage externe d’Office 365 et de B2B](active-directory-b2b-o365-external-user.md)
#### [Licences B2B](active-directory-b2b-licensing.md)
#### [Limitations actuelles](active-directory-b2b-current-limitations.md)
#### [FORUM AUX QUESTIONS](active-directory-b2b-faq.md)
#### [Résolution de problèmes B2B](active-directory-b2b-troubleshooting.md)
#### [Comprendre l’utilisateur B2B](active-directory-b2b-user-properties.md)
#### [Jeton utilisateur B2B](active-directory-b2b-user-token.md)
#### [B2B pour les applications intégrées Azure AD](active-directory-b2b-configure-saas-apps.md)
#### [Mappage des revendications d’utilisateur B2B](active-directory-b2b-claims-mapping.md)
#### [Comparer la collaboration B2B et B2C](active-directory-b2b-compare-b2c.md)
#### [Obtenir une assistance pour B2B](active-directory-b2b-support.md)

## [Gérer les groupes et les membres](active-directory-manage-groups.md)
### Gérer les groupes
#### [Portail Azure](active-directory-groups-create-azure-portal.md)
#### [Azure PowerShell](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
### [Sélectionner les membres du groupe](active-directory-groups-members-azure-portal.md)
### [Gérer les propriétaires de groupe](active-directory-accessmanagement-managing-group-owners.md)
### [Ajouter une appartenance à un groupe](active-directory-groups-membership-azure-portal.md)
### [Attribuer des licences à l’aide de groupes](active-directory-licensing-whatis-azure-portal.md)
#### [Attribuer des licences à un groupe](active-directory-licensing-group-assignment-azure-portal.md)
#### [Identifier et résoudre les problèmes de licence dans un groupe](active-directory-licensing-group-problem-resolution-azure-portal.md)
#### [Migrer des utilisateurs individuels titulaires d’une licence aux licences par groupe](active-directory-licensing-group-migration-azure-portal.md)
#### [Scénarios supplémentaires pour la gestion des licences par groupe](active-directory-licensing-group-advanced.md)
#### [Exemples Azure PowerShell pour les licences basées sur les groupes](active-directory-licensing-ps-examples.md)
#### [Référence pour les produits et les plans de service dans Azure AD](active-directory-licensing-product-and-service-plan-reference.md)
### [Configurer l’expiration des groupes Office 365](active-directory-groups-lifecycle-azure-portal.md)
### [Afficher tous les groupes](active-directory-groups-view-azure-portal.md)
### [Ajouter l’accès de groupe aux applications SaaS](active-directory-accessmanagement-group-saasapps.md)
### [Restaurer un groupe Office 365 supprimé](active-directory-groups-restore-azure-portal.md)
### Gérer les paramètres de groupe
#### [Portail Azure](active-directory-groups-settings-azure-portal.md)
#### [Applets de commande](active-directory-accessmanagement-groups-settings-cmdlets.md)
### Créer des règles avancées
#### [Portail Azure](active-directory-groups-dynamic-membership-azure-portal.md)
### [Configurer des groupes libre-service](active-directory-accessmanagement-self-service-group-management.md)
### [Résolution des problèmes](active-directory-accessmanagement-troubleshooting.md)

## [Gérer les rapports](active-directory-reporting-azure-portal.md)
### [Activité des connexions](active-directory-reporting-activity-sign-ins.md)
### [Activité des audits](active-directory-reporting-activity-audit-logs.md)
### [Utilisateurs à risque](active-directory-reporting-security-user-at-risk.md)
### [Connexions risquées](active-directory-reporting-security-risky-sign-ins.md)
### [Événements à risque](active-directory-reporting-risk-events.md)
### [FORUM AUX QUESTIONS](active-directory-reporting-faq.md)
### Tâches
#### [Configurer des emplacements nommés](active-directory-named-locations.md)
#### [Afficher les rapports d’activité](active-directory-reporting-migration.md)
#### [Utiliser le pack de contenu Power BI Azure Active Directory](active-directory-reporting-power-bi-content-pack-how-to.md)
### Informations de référence
#### [Rétention](active-directory-reporting-retention.md)
#### [Latences](active-directory-reporting-latencies-azure-portal.md)
#### [Notifications](active-directory-reporting-notifications.md)
#### [Codes d’erreur de l’activité de connexion](active-directory-reporting-activity-sign-ins-errors.md)
#### [Authentification multifacteur](active-directory-reporting-activity-sign-ins-mfa.md)
### Résolution des problèmes
#### [Données d’audit manquantes](active-directory-reporting-troubleshoot-missing-audit-data.md)
#### [Données manquantes dans les téléchargements](active-directory-reporting-troubleshoot-missing-data-download.md)
#### [Erreurs de pack de contenu des journaux d’activité Azure Active Directory](active-directory-reporting-troubleshoot-content-pack.md)
### [Accès par programme](active-directory-reporting-api-getting-started-azure-portal.md)
#### [Référence d’audit](active-directory-reporting-api-audit-reference.md)
#### [Référence de connexion](active-directory-reporting-api-sign-in-activity-reference.md)
#### [Composants requis](active-directory-reporting-api-prerequisites-azure-portal.md)
#### [Exemples d’audit](active-directory-reporting-api-audit-samples.md)
#### [Exemples de connexion](active-directory-reporting-api-sign-in-activity-samples.md)
#### [Utilisation des certificats](active-directory-reporting-api-with-certificates.md)

## Gestion des mots de passe
### [Vue d’ensemble des mots de passe](active-directory-passwords-overview.md)
### Documents utilisateur
#### [Réinitialiser ou modifier votre mot de passe](active-directory-passwords-update-your-own-password.md)
#### [Meilleures pratiques relatives aux mots de passe](active-directory-secure-passwords.md)
#### [S’inscrire pour la réinitialisation du mot de passe en libre-service](active-directory-passwords-reset-register.md)
### [Fonctionnement SSPR](active-directory-passwords-how-it-works.md)
### [Guide de déploiement SSPR](active-directory-passwords-best-practices.md)
### [SSPR et Windows 10](active-directory-passwords-login.md)
### [Stratégies SSPR](active-directory-passwords-policy.md)
### [Personnalisation SSPR](active-directory-passwords-customize.md)
### [Spécifications des données SSPR](active-directory-passwords-data.md)
### [SSPR Reporting](active-directory-passwords-reporting.md)
### Administrateurs informatiques : réinitialiser les mots de passe
#### [Portail Azure](active-directory-users-reset-password-azure-portal.md)
### [Licence SSPR](active-directory-passwords-licensing.md)
### [Réécriture du mot de passe](active-directory-passwords-writeback.md)
### [Résolution des problèmes](active-directory-passwords-troubleshoot.md)
### [FORUM AUX QUESTIONS](active-directory-passwords-faq.md)


## Gérer des appareils
### [Introduction](device-management-introduction.md)
### [À l’aide du portail Azure](device-management-azure-portal.md)
### [Planifier l’exécution d’Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)
### [FAQ](device-management-faq.md)
### Tâches
#### [Configurer les appareils Windows 10 inscrits dans Azure AD](device-management-azuread-registered-devices-windows10-setup.md)
#### [Configurer les appareils joints Azure AD](device-management-azuread-joined-devices-setup.md)
#### [Configurer les appareils joints Azure AD hybrides](device-management-hybrid-azuread-joined-devices-setup.md)
#### [Déployer en local](active-directory-device-registration-on-premises-setup.md)
#### [Enregistrement dans Azure AD lors de la première exécution de Windows 10](device-management-azuread-joined-devices-frx.md)
### Résolution des problèmes
#### [Appareils Windows 10 et Windows Server 2016 joints Azure AD hybrides](device-management-troubleshoot-hybrid-join-windows-current.md)
#### [Appareils Windows hérités joints Azure AD](device-management-troubleshoot-hybrid-join-windows-legacy.md)

## Gérer des applications
### [Vue d’ensemble](active-directory-enable-sso-scenario.md)
### [Prise en main](active-directory-integrating-applications-getting-started.md)
### [Didacticiels d’intégration d’applications SaaS](active-directory-saas-tutorial-list.md)
### [Cloud App Discovery](cloudappdiscovery-get-started.md)
#### [Créer des rapports d’instantanés](cloudappdiscovery-set-up-snapshots.md)
#### [Configurer le reporting continu](https://docs.microsoft.com/cloud-app-security/discovery-docker)
#### [Utiliser un analyseur de journal personnalisé](https://docs.microsoft.com/cloud-app-security/custom-log-parser)
#### Découverte basée sur les agents
##### [Qu’est-ce que Cloud App Discovery ?](active-directory-cloudappdiscovery-whatis.md)
##### [Mettre à jour les paramètres du Registre](active-directory-cloudappdiscovery-registry-settings-for-proxy-services.md)
##### [Comprendre la sécurité et la confidentialité](active-directory-cloudappdiscovery-security-and-privacy-considerations.md)


### [Accéder aux applications à distance avec le proxy d’application](active-directory-application-proxy-get-started.md)
#### Prise en main
##### [Activer le Proxy d’application](active-directory-application-proxy-enable.md)
##### [Publiez des applications](application-proxy-publish-azure-portal.md)
##### [Domaines personnalisés](active-directory-application-proxy-custom-domains.md)
#### [Authentification unique](application-proxy-sso-overview.md)
##### [Authentification unique avec KCD](active-directory-application-proxy-sso-using-kcd.md)
##### [Authentification unique avec en-têtes](application-proxy-ping-access.md)
##### [Authentification unique avec mise au coffre des mots de passe](application-proxy-sso-azure-portal.md)
#### Concepts
##### [Connecteurs](application-proxy-understand-connectors.md)
##### [Sécurité](application-proxy-security-considerations.md)
##### [Réseaux](application-proxy-network-topology-considerations.md)


##### [Mise à niveau à partir de TMG ou UAG](application-proxy-transition-from-uag-tmg.md)

#### Configurations avancées
##### [Publier sur des réseaux distincts](active-directory-application-proxy-connectors-azure-portal.md)
##### [Serveurs proxy](application-proxy-working-with-proxy-servers.md)
##### [Applications prenant en charge les revendications](active-directory-application-proxy-claims-aware-apps.md)
##### [Applications de client natif](active-directory-application-proxy-native-client.md)
##### [Installation sans assistance](active-directory-application-proxy-silent-installation.md)
##### [Page d’accueil personnalisée](application-proxy-office365-app-launcher.md)
##### [Traduire les liens inclus](application-proxy-link-translation.md)
#### Publication de procédures pas à pas
##### [Bureau à distance](application-proxy-publish-remote-desktop.md)
##### [SharePoint](application-proxy-enable-remote-access-sharepoint.md)
##### [Microsoft Teams](application-proxy-teams.md)
#### [Résolution des problèmes](active-directory-application-proxy-troubleshoot.md)

### Gérer les applications d’entreprise
#### [Affecter des utilisateurs](active-directory-coreapps-assign-user-azure-portal.md)
#### [Personnaliser la marque](active-directory-coreapps-change-app-logo-user-azure-portal.md)
#### [Comment désactiver les connexions des utilisateurs ?](active-directory-coreapps-disable-app-azure-portal.md)
#### [Supprimer des utilisateurs](active-directory-coreapps-remove-assignment-azure-portal.md)
#### [Afficher toutes mes applications](active-directory-coreapps-view-azure-portal.md)
#### [Gérer l’approvisionnement de comptes d’utilisateurs](active-directory-enterprise-apps-manage-provisioning.md)
#### [Gérer l’authentification unique pour les applications d’entreprise](active-directory-enterprise-apps-manage-sso.md)
#### [Signature de certificat avancée pour les applications SAML](active-directory-enterprise-apps-advance-certificate-options.md)
#### [Masquer une application à partir de l’expérience utilisateur](active-directory-coreapps-hide-third-party-app.md)
### [Configurer l’accélération automatique de la connexion à l’aide de la stratégie HRD Policy](active-directory-auto-acceleration-using-hrd.md)

### [Gérer l’accès aux applications](active-directory-managing-access-to-apps.md)
#### [Accès par authentification unique](active-directory-appssoaccess-whatis.md)
#### [Certificats pour authentification unique](active-directory-sso-certs.md)
#### [Restrictions du client](active-directory-tenant-restrictions.md)
#### [Utilisez SCIM approvisionner les utilisateurs](active-directory-scim-provisioning.md)

### [Résolution des problèmes](active-directory-application-troubleshoot-content-map.md)
#### [Développement d’applications](active-directory-application-dev-troubleshoot-content-map.md)
##### [Configuration et inscription](active-directory-application-dev-config-content-map.md)
##### [Développement](active-directory-application-dev-development-content-map.md)
#### [Gestion des applications](active-directory-application-management-troubleshoot-content-map.md)
##### [Configuration](active-directory-application-config-content-map.md)
##### [Connexion](active-directory-application-sign-in-content-map.md)
##### [Approvisionnement](active-directory-application-provisioning-content-map.md)
##### [Gestion de l’accès](active-directory-application-access-content-map.md)
##### [Volet d’accès](active-directory-application-access-panel-content-map.md)
##### [Proxy d’application](active-directory-application-proxy-content-map.md)
##### [Accès conditionnel](active-directory-application-conditional-access-content-map.md)
### [Développer des applications](active-directory-applications-guiding-developers-for-lob-applications.md)
### [Bibliothèque de documents ](active-directory-apps-index.md)

## Gérer votre répertoire
### [Azure AD Connect](./connect/active-directory-aadconnect.md)
### Noms de domaine personnalisés
#### [Démarrage rapide](add-custom-domain.md)
#### [Ajouter des noms de domaines personnalisés](active-directory-domains-manage-azure-portal.md)
### [Administration de votre annuaire](active-directory-administer.md)
### [Plusieurs répertoires](active-directory-licensing-directory-independence.md)
### [Inscription libre-service](active-directory-self-service-signup.md)
### [Reprendre un répertoire non managé](domains-admin-takeover.md)
### [Enterprise State Roaming](active-directory-windows-enterprise-state-roaming-overview.md)
#### [Activer](active-directory-windows-enterprise-state-roaming-enable.md)
#### [Paramètres de stratégie de groupe](active-directory-windows-enterprise-state-roaming-group-policy-settings.md)
#### [Paramètres Windows 10](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
#### [FAQ](active-directory-windows-enterprise-state-roaming-faqs.md)
#### [Résolution des problèmes](active-directory-windows-enterprise-state-roaming-troubleshooting.md)


### [Intégrer des identités locales à l’aide d’Azure AD Connect](./connect/active-directory-aadconnect.md)

## [Gérer l’accès à Azure](toc.yml)

## Déléguer l’accès aux ressources
### [Rôles d’administrateur](active-directory-assign-admin-roles-azure-portal.md)
#### [Affecter des rôles d’administrateur](active-directory-users-assign-role-azure-portal.md)
### [Unités administratives](active-directory-administrative-units-management.md)
### [Durées de vie des jetons](active-directory-configurable-token-lifetimes.md)
### [Gérer les comptes d’administration d’accès d’urgence](active-directory-admin-manage-emergency-access-accounts.md)

## Révisions d’accès
### [Vue d’ensemble des révisions d’accès](active-directory-azure-ad-controls-access-reviews-overview.md)
### [Effectuer une révision d’accès](active-directory-azure-ad-controls-complete-access-review.md)
### [Créer une révision d’accès](active-directory-azure-ad-controls-create-access-review.md)
### [Exécution d’une révision de l’accès](active-directory-azure-ad-controls-perform-access-review.md)
### [Exécuter une révision d’accès](active-directory-azure-ad-controls-how-to-review-your-access.md)
### [Accès invité avec révisions d’accès](active-directory-azure-ad-controls-manage-guest-access-with-access-reviews.md)
### [Gestion de l’accès utilisateur avec les révisions](active-directory-azure-ad-controls-manage-user-access-with-access-reviews.md)
### [Gestion des programmes et des contrôles](active-directory-azure-ad-controls-manage-programs-controls.md)


## Sécuriser vos identités
### [Accès conditionnel](active-directory-conditional-access-azure-portal.md)
#### [Contrôles](active-directory-conditional-access-controls.md)
#### [Condition d’emplacement](active-directory-conditional-access-locations.md)
#### [Bien démarrer](active-directory-conditional-access-azure-portal-get-started.md)
#### [meilleures pratiques](active-directory-conditional-access-best-practices.md)
#### [Comprendre les stratégies d’appareil pour les services Office 365](active-directory-conditional-access-device-policies.md)
#### [Migrer les stratégies classiques](active-directory-conditional-access-migration.md)
#### [Outil de simulation](active-directory-conditional-access-whatif.md)
#### Tâches
##### [Migrer une stratégie MFA classique](active-directory-conditional-access-migration-mfa.md)
##### [Configurer l’accès conditionnel basé sur les appareils](active-directory-conditional-access-policy-connected-applications.md)
##### [Configurer l’accès conditionnel basé sur les applications](active-directory-conditional-access-mam.md)
##### [Fournir des conditions d’utilisation pour les utilisateurs et les applications](active-directory-tou.md)
##### [Configurer la connectivité VPN](active-directory-conditional-access-vpn-connectivity-windows10.md)
##### [Configurer SharePoint et Exchange Online](active-directory-conditional-access-no-modern-authentication.md)
##### [Correction](active-directory-conditional-access-device-remediation.md)
#### [Référence technique](active-directory-conditional-access-technical-reference.md)
#### [FAQ](active-directory-conditional-faqs.md)

### Windows Hello
#### [S’authentifier sans mots de passe](active-directory-azureadjoin-passport.md)
#### [Activer Windows Hello Entreprise](active-directory-azureadjoin-passport-deployment.md)
### Authentification par certificat
#### [Android](active-directory-certificate-based-authentication-android.md)
#### [iOS](active-directory-certificate-based-authentication-ios.md)
#### [Bien démarrer](active-directory-certificate-based-authentication-get-started.md)

### [Azure AD Identity Protection](active-directory-identityprotection.md)
#### [Activer](active-directory-identityprotection-enable.md)
#### [Détecter les vulnérabilités](active-directory-identityprotection-vulnerabilities.md)
#### [Événements à risque](active-directory-identity-protection-risk-events.md)
#### [Notifications](active-directory-identityprotection-notifications.md)
#### [Expérience de connexion](active-directory-identityprotection-flows.md)
#### [Simuler des événements à risque](active-directory-identityprotection-playbook.md)
#### [Débloquer des utilisateurs](active-directory-identityprotection-unblock-howto.md)
#### [FAQ](active-directory-identity-protection-faqs.md)
#### [Glossaire](active-directory-identityprotection-glossary.md)
#### [Microsoft Graph](active-directory-identityprotection-graph-getting-started.md)
### [Privileged Identity Management](./privileged-identity-management/active-directory-securing-privileged-access.md)

## [Intégrer d’autres services à Azure AD]()
### [Activer l’intégration de LinkedIn](linkedin-integration.md)

## [Déployer AD DS sur des machines virtuelles Azure](virtual-networks-windows-server-active-directory-virtual-machines.md)
### [Windows Server Active Directory sur les machines virtuelles Azure](active-directory-deploying-ws-ad-guidelines.md)
### [Contrôleur de domaine de réplication dans un réseau virtuel Azure](active-directory-install-replica-active-directory-domain-controller.md)
### [Nouvelle forêt sur un réseau virtuel Azure](active-directory-new-forest-virtual-machine.md)



## [Déployer AD FS dans Azure](active-directory-aadconnect-azure-adfs.md)
### [Haute disponibilité](active-directory-adfs-in-azure-with-azure-traffic-manager.md)
### [Algorithme de hachage de signature de modification](active-directory-federation-sha256-guidance.md)

## [Résolution des problèmes](active-directory-troubleshooting-support-howto.md)
### [Dépannage : l’élément « Active Directory » est manquant ou non disponible](active-directory-troubleshooting.md)

## Déploiement de la preuve de concept (POC) d’Azure AD
### [Manuel POC : Introduction](active-directory-playbook-intro.md)
### [Manuel POC : Ingrédients](active-directory-playbook-ingredients.md)
### [Manuel POC : Mise en œuvre](active-directory-playbook-implementation.md)
### [Manuel POC : Blocs de construction](active-directory-playbook-building-blocks.md)


# Informations de référence
## [Exemples de code](https://azure.microsoft.com/en-us/resources/samples/?service=active-directory)
## [Applets de commande Azure PowerShell](/powershell/azure/overview)
## [Informations de référence sur l’API Java](/java/api)
## [API .NET](/active-directory/adal/microsoft.identitymodel.clients.activedirectory)
## [Restrictions et limites du service](active-directory-service-limits-restrictions.md)

# Rubriques connexes
## [Azure Multi-Factor Authentication](/azure/multi-factor-authentication/)
## [Azure AD Connect](./connect/active-directory-aadconnect.md)
## [Azure AD Connect Health](./connect-health/active-directory-aadconnect-health.md)
## [Azure pour développeurs](./develop/active-directory-how-to-integrate.md)
## [Azure AD Privileged Identity Management](./privileged-identity-management/active-directory-securing-privileged-access.md)

# Ressources
## [Forum de commentaires Azure](https://feedback.azure.com/forums/169401-azure-active-directory)
## [Feuille de route Azure](https://azure.microsoft.com/roadmap/?category=security-identity)
## [Forum MSDN](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=WindowsAzureAD)
## [Tarification](https://azure.microsoft.com/pricing/details/active-directory/)
## [Calculatrice de prix](https://azure.microsoft.com/pricing/calculator/)
## [Mises à jour de service](https://azure.microsoft.com/updates/?product=active-directory)
## [Dépassement de capacité de la pile](http://stackoverflow.com/questions/tagged/azure-active-directory)
## [Vidéos](https://azure.microsoft.com/documentation/videos/index/?services=active-directory)
