

![Machines virtuelles dans un service cloud autonome](./media/virtual-machines-common-classic-connect-vms/CloudServiceExample.png)

Si vous placez vos machines virtuelles dans un réseau virtuel, vous pouvez choisir le nombre de services cloud vous souhaitez toouse pour charge les ensembles de disponibilité et de l’équilibrage de la. En outre, vous pouvez organiser les ordinateurs virtuels de hello sur les sous-réseaux dans hello comme votre site et s’y connecter tooyour de réseau virtuel hello local réseau. Voici un exemple :

![Machines virtuelles dans un réseau virtuel](./media/virtual-machines-common-classic-connect-vms/VirtualNetworkExample.png)

Les réseaux virtuels sont hello recommandé de façon tooconnect virtual machines dans Azure. Il est recommandé de Hello est tooconfigure à chaque niveau de votre application dans un service cloud distinct. Toutefois, vous devrez peut-être toocombine certains ordinateurs virtuels à partir de différents niveaux d’application dans hello même cloud tooremain service hello dans d’au maximum 200 services de cloud computing par abonnement. tooreview cela et autres limites, consultez [abonnement Azure et limites de Service, Quotas et contraintes](../articles/azure-subscription-service-limits.md).

## <a name="connect-vms-in-a-virtual-network"></a>Connexion de machines virtuelles dans un réseau virtuel
tooconnect les machines virtuelles dans un réseau virtuel :

1. Créer un réseau virtuel de hello Bonjour [portail Azure](../articles/virtual-network/virtual-networks-create-vnet-classic-pportal.md) et spécifiez « déploiement classique ».
2. Ensemble de hello de services de cloud pour votre déploiement de tooreflect de création pour la haute disponibilité et l’équilibrage de charge. Bonjour portail Azure, cliquez sur **Nouveau > calcul > service Cloud** pour chaque service cloud.

  Lorsque vous renseignez les détails du service cloud hello, choisissez hello même _groupe de ressources_ utilisé avec un réseau virtuel hello.

3. toocreate chaque nouvelle virtuel de l’ordinateur, cliquez sur **Nouveau > calcul**, puis sélectionnez hello approprié image de machine virtuelle à partir de hello **applications proposées**.

  Bonjour VM **notions de base** panneau, choisissez hello même _groupe de ressources_ utilisé avec un réseau virtuel hello.

  ![Panneau Concepts de base de la machine virtuelle lors de l’utilisation d’un réseau virtuel](./media/virtual-machines-common-classic-connect-vms/CreateVM_Basics_VN.png)

4. Pendant que vous remplissez hello VM **paramètres**, choisissez hello correct _service de cloud computing_ ou _réseau virtuel_ pour hello machine virtuelle.

  Azure sélectionnera hello autres éléments en fonction de votre sélection.

  ![Panneau Paramètres de la machine virtuelle lors de l’utilisation d’un réseau virtuel](./media/virtual-machines-common-classic-connect-vms/CreateVM_Settings_VN.png)


## <a name="connect-vms-in-a-standalone-cloud-service"></a>Connexion de machines virtuelles dans un service cloud autonome
tooconnect les machines virtuelles dans un service de cloud autonome :

1. Créer un service de cloud computing hello Bonjour [portail Azure](http://portal.azure.com). Cliquez sur **Nouveau > Compute > Service cloud**. Ou bien, vous pouvez créer le service de cloud computing hello pour votre déploiement lorsque vous créez votre première machine virtuelle.
2. Lorsque vous créez des machines virtuelles de hello, choisissez hello même groupe de ressources utilisé avec le service de cloud computing hello.

  ![Ajouter un service cloud existant de machine virtuelle tooan](./media/virtual-machines-common-classic-connect-vms/CreateVM_Basics_SA.png)

3.  Lorsque vous renseignez les détails de l’ordinateur virtuel hello, choisissez-en hello du service cloud créé dans la première étape de hello.

  ![Sélection d'un service cloud pour une machine virtuelle](./media/virtual-machines-common-classic-connect-vms/CreateVM_Settings_SA.png)
