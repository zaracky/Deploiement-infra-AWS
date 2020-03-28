# OCR_AWS
template aws

1- Template création VPC + Security groups :
    1 vpc + 3 sous réseaux et table de routage
    Security groupe pour ec2 rds et loadbalancer

2- Template création DB aurora mysql en multi az

3- Création instance wordpress + load balancer + une instance intranet (page html fixe) + une instance serveur vpn (strongswan)


/!\ Toutes les données confidentiels seront importés à partir de secretManager. Les lignes à modifier se trouvent dans les scripts de configuration et non les templates AWS


Script configuration:
Docker: https://raw.githubusercontent.com/zaracky/OCR_P10/master/configuration-docker.bash
Vpn: https://raw.githubusercontent.com/zaracky/OCR_P10/master/configurationvpn.bash
