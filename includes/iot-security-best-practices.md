# <a name="internet-of-things-security-best-practices"></a>Meilleures pratiques de sécurité pour l’Internet des objets (IoT)
toosecure une infrastructure Internet of Things (IoT) nécessite une stratégie de sécurité en profondeur rigoureuse. Cette stratégie requiert que vous toosecure les données dans le cloud de hello, de protéger l’intégrité des données lors de leur transit sur hello internet public et configurer en toute sécurité des appareils. Chaque couche génère une plus grande assurance de sécurité Bonjour infrastructure globale.

## <a name="secure-an-iot-infrastructure"></a>Sécuriser une infrastructure IoT
Cette stratégie de sécurité en profondeur peut être développée et exécutée avec la participation active des différents acteurs impliqués dans la fabrication de hello, de développement et de déploiement de l’infrastructure et des appareils IoT. Voici une description générale de ces acteurs.  

* **Fabricant de matériel IoT/intégrateur**: en règle générale, il s’agit de fabricants hello du matériel IoT déployé, intégrateurs assemblage matériel à partir de différents fabricants ou des fournisseurs de matériel pour un déploiement IoT fabriqué intégré ou par d’autres fournisseurs.
* **Développeur de solutions IoT**: développement hello d’une solution IoT se traduit généralement par un développeur de solutions. Ce développeur peut faire partie d’une équipe interne ou être un intégrateur système spécialisé dans cette activité. Hello développeur de solutions IoT permettre développer des différents composants de la solution de IoT hello à partir de zéro, intégrer les différents composants prêts à l’emploi ou open source ou adopter des solutions préconfigurées avec adaptation mineure.
* **Responsable du déploiement de la solution IoT**: solution après une IoT est développée, elle doit toobe déployé dans le champ de hello. Cela implique le déploiement du matériel, l’interconnexion de périphériques et le déploiement de solutions dans le cloud de hello ou de périphériques matériels.
* **Opérateur de solution IoT**: après hello IoT solution est déployée, elle nécessite des opérations à long terme, surveillance, la maintenance et les mises à niveau. Cela est possible par une équipe interne qui comprend les spécialistes de la technologie d’informations, les opérations de matériel les équipes de maintenance et des spécialistes de domaine qui contrôlent le comportement correct de hello d’infrastructure IoT globale.

les sections de Hello qui suivent fournissent les meilleures pratiques pour chacun de ces lecteurs toohelp développent, déploiement et exploiter une infrastructure IoT sécurisée.

## <a name="iot-hardware-manufacturerintegrator"></a>Fabricant/intégrateur de matériel IoT
Hello Voici hello meilleures pratiques pour les fabricants de matériel IoT et intégrateurs de matériel.

* **Portée toominimum requise**: conception de matériel hello doit inclure les fonctionnalités minimales hello requises pour l’opération de matériel de hello et rien de plus. Un exemple est ports USB de tooinclude uniquement si nécessaire pour l’opération hello du périphérique de hello. Ces fonctionnalités supplémentaires d’ouvrir l’unité de hello pour les vecteurs d’attaque indésirables qui doit être évitée.
* **Assurez-vous matériel falsifications**: Build mécanismes toodetect physique toute falsification, telles que l’ouverture de la couverture de périphérique hello ou le retrait d’une partie de l’appareil de hello. Ces signaux la falsification peut faire partie de hello données flux téléchargé toohello cloud, ce qui pourrait d’avertir les opérateurs de ces événements.
* **Intégrer la sécurité au matériel** : Si le coût des marchandises vendues le permet, intégrez des fonctionnalités de sécurité, telles qu’un stockage sécurisé et chiffré, ou une fonctionnalité de démarrage basée sur un Module de plateforme sécurisée (TPM). Ces fonctionnalités Vérifiez des périphériques plus sécurisés et vous aider à protéger hello infrastructure IoT globale.
* **Sécuriser les mises à niveau**: mise à jour pendant la durée de vie hello du périphérique de hello est inévitables. Création des appareils avec des chemins d’accès sécurisés pour les mises à niveau et assurance de chiffrement de versions du microprogramme permettra hello appareil toobe sécurisé pendant et après les mises à niveau.

## <a name="iot-solution-developer"></a>Développeur de solutions IoT
Hello Voici hello meilleures pratiques pour les développeurs de solutions IoT :

* **Suivez la méthodologie de développement de logiciels sécurisés**: développement de logiciels sécurisés requiert des sol vous réfléchissez à la sécurité, de la création de hello du projet de hello tous les mise en œuvre de hello moyen tooits, le test et déploiement. choix de Hello des plateformes, les langages et les outils est influencées avec cette méthodologie. Hello cycle de développement de sécurité de Microsoft fournit un logiciel sécurisé toobuilding de procédure pas à pas.
* **Choisissez des logiciels open source avec précaution**: logiciels Open source fournit une opportunité tooquickly développer des solutions. Lorsque vous choisissez des logiciels open source, envisagez de niveau d’activité hello de communauté hello pour chaque composant open source. Avec une communauté active, les logiciels bénéficient d’un vaste soutien, et les problèmes sont identifiés et traités. Ce n’est nécessairement pas le cas d’un logiciel open source obscur et inactif : les problèmes ne sont probablement pas identifiés.
* **Intégrer avec précaution**: existent de nombreuses failles de sécurité logiciels à la limite de hello de bibliothèques et d’API. Fonctionnalités qui ne sont peut-être pas requises pour le déploiement en cours de hello peuvent toujours être disponible via une couche API. tooensure de sécurité globale, assurez-vous que toocheck toutes les interfaces des composants en cours d’intégration pour les failles de sécurité.      

## <a name="iot-solution-deployer"></a>Responsable du déploiement de solutions IoT
Hello Voici les meilleures pratiques pour les responsables de déploiement de solution IoT :

* **Déployer le matériel en toute sécurité**: IoT déploiements peuvent nécessiter toobe matériel déployé dans des emplacements non sécurisés, comme dans les espaces publics ou des paramètres régionaux non supervisés. Dans ce cas, assurez-vous que le déploiement de matériel est inviolable toohello mesure. Si USB ou autres ports sont disponibles sur le matériel de hello, assurez-vous qu’ils sont couverts en toute sécurité. De nombreux vecteurs d’attaque peuvent les utiliser comme point d’entrée.
* **Protéger les clés d’authentification**: pendant le déploiement, chaque appareil nécessite l’ID de périphérique et des clés d’authentification générés par le service de cloud computing hello associées. Protéger ces clés physiquement même après le déploiement de hello. N’importe quelle touche compromise utilisable par un toomasquerade malveillant périphérique comme un périphérique existant.

## <a name="iot-solution-operator"></a>Opérateur de solutions IoT
Hello Voici les méthodes conseillées pour les opérateurs de solution IoT hello :

* **Conserver le système hello toodate**: Assurez-vous que les systèmes d’exploitation et tous les pilotes de périphérique sont toohello mis à niveau des versions plus récentes. Si vous activez les mises à jour automatiques dans Windows 10 (IoT ou autres références (SKU)), Microsoft les conserve des toodate, en fournissant un système d’exploitation sécurisé pour les appareils IoT. En conservant les autres systèmes d’exploitation (tel que Linux) toodate permet de garantir qu’ils sont également protégés contre les attaques malveillantes.
* **Protection contre les activités malveillantes**: si le système d’exploitation de hello permet, installez hello dernières antivirus et anti-programme malveillant fonctionnalités sur chaque système d’exploitation. Ceci peut contribuer à atténuer la plupart des menaces externes. Vous pouvez protéger la plupart des systèmes d’exploitation contre les menaces en prenant les mesures appropriées.
* **Audit fréquemment**: infrastructure de l’audit des IoT pour les problèmes de sécurité est essentielle lors de la réponse toosecurity incidents. La plupart des systèmes d’exploitation fournissent la journalisation des événements prédéfinis qui doit être examinés fréquemment toomake qu’aucune faille de sécurité. Informations d’audit peuvent être envoyées en tant qu’un service de cloud de télémétrie distinct flux toohello où il peut être analysé.
* **Protégez physiquement infrastructure de IoT hello**: hello pire pour lancer des attaques de sécurité contre IoT infrastructure à l’aide de l’accès physique toodevices. Une pratique de sécurité importantes est tooprotect par rapport à une utilisation malveillante de ports USB et d’autres opérations d’accès physique. Enregistre un toouncovering clé violations qui se sont produites d’un accès physique, par exemple d’utilisation de port USB. Là encore, Windows 10 (IoT et autres références) peut assurer une journalisation détaillée de ces événements.
* **Protéger les informations d’identification cloud**: informations d’identification de l’authentification Cloud utilisées pour la configuration et l’utilisation d’un déploiement IoT sont éventuellement accès toogain moyen plus simple de hello et compromettre un système IoT. Protéger les informations d’identification hello en modifiant le mot de passe hello fréquemment et éviter d’utiliser ces informations d’identification sur des ordinateurs publics.

Les fonctionnalités des différents appareils IoT peuvent varier. Certains appareils peuvent être des ordinateurs exécutant des systèmes d’exploitation courants, tandis que d’autres peuvent exécuter des systèmes d’exploitation très légers. Hello meilleures pratiques de sécurité décrits précédemment peuvent être des périphériques toothese applicables à des degrés divers. Si fourni, le déploiement et sécurité des meilleures pratiques supplémentaires provenant de fabricants hello de ces appareils doivent être suivies.

Certains appareils existants et limités n’ont peut-être pas été conçus spécifiquement pour un déploiement IoT. Ces appareils peuvent ne disposent pas de données de tooencrypt fonctionnalité hello, connectez-vous avec hello Internet ou fournir l’audit avancé. Dans ce cas, une passerelle de champ modernes et sécurisés peut agréger des données à partir des périphériques hérités et offrent une sécurité hello requise pour la connexion de ces appareils sur Internet de hello. Passerelles de champ peuvent fournir une authentification sécurisée, la négociation de sessions chiffrées, réception de commandes à partir de cloud de hello et de nombreuses autres fonctionnalités de sécurité.
