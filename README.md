# OCR_AWS
TEMPLATE AWS

/!\ LES TEMPLATES SONT IDEPENDANTS LES UN DES AUTRES


CONTENU:

1- Template création VPC + Security groups :
    1 vpc + 3 sous réseaux et table de routage
    Security groupe pour ec2 rds et loadbalancer

2- Template création DB aurora mysql en multi az

3- Création de 2 instances wordpress + 1 autoscaling group + 1 load balancer + 1 instance intranet (page html fixe) + 1 instance serveur vpn (strongswan)


PREREQUIS:
 
/!\ Afin de ne pas divulguer  les données confidentiels, ces seront importés à partir de secretManager. Il est donc important de les créer au préalable.
Idéalement, il faudra les nommées DB_WORDPRESS et VPN

Dans le cas contraire,il faudra le modifier dans les scripts de configuration et non les templates AWS

Script configuration:
Docker: https://raw.githubusercontent.com/zaracky/OCR_P10/master/configuration-docker.bash
Vpn: https://raw.githubusercontent.com/zaracky/OCR_P10/master/configurationvpn.bash

A noter également qu'en cas de personalisation, il vous faudra heberger ces fichiers et indiquer le bon url pour que template le recupere.




UTILISATION:

1- LE VPC

Aucun parametre n'est à renseigner

Le template vas vous créer un VPC nommé "mon VPC" contenant 2 sous reseau public (10.0.100.0/24 et 10.0.101.0/24) et 1 sous reseau privée (10.0.0.0/24)

Les routes se feront par defaut vers l'internet gateway.

3 security groups vont être crées:
1 Pour le loadbalancer autorisant l'accès au port 80
1 Pour les instances EC2 autorisant l'accès au port 80 uniquement par le loadbalancer
1 Pour les bases de données autorisant la connexion au port 3306 uniquement par les instances EC2


2- La base RDS

Voici les paramètres à indiquer lors de l'execution du template:
-Le type d'instance
- Le nom de la database
- Le nom de l'utilisateur de la base
- Le mot de passe de l'utilisateur de la base
- Le VPC ou ils seront crées
-Les subnets qui pourront y accèder (par defaut 2 minimum)
-Le security group rattaché

Le template vas créer un cluster de base de données AURORA-MYSQL. Il s'agit d'un noeud Maitre/Replica sur deux zone de disponibilités.
L'avantage ici est d'avoir un mecanisme de disponibilité mais également d'avoir des bases de données manager par AWS.

Par exemple, l'administration (MAJ,Maintenance..) et la sauvegarde (frequence personalisable) sont géres par Amazon

3- LoadBalancer et EC2

Voici les paramètres à indiquer lors de l'execution du template:
-Le VPC ou ils seront crées
- Les subnets publique dédié au instance Wordpress
- Le subnet privé dédié idéalement au instance VPN et Intranet
- La clé de connexion au instances
- Le security group rattaché aux instances
-Le security group rattaché au loadbalancer


