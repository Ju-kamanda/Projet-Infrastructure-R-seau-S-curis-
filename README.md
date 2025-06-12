# Projet-Infrastructure-R-seau-S-curis-
📌 1. Titre du projet
----------------------
Projet Infrastructure Réseau Sécurisé
VPN IPsec · SSH · VLANs · ACLs

🎯 2. Objectif du projet
-------------------------

Ce projet simule une architecture réseau d'entreprise sécurisée, répartie sur plusieurs départements, avec des mécanismes de sécurité et d’accès distants.

🧱 3. Architecture du réseau
-----------------------------
VLANs et Adressage IP:

--/        Routeur0 2911

VLAN 10 : CYBER/RESEAU / Static IP 192.168.10.0/24
VLAN 11 : VENTE/ADMIN (Administration de la société) / Dynamic IP 192.168.11.0/24 (Routeur0 2911)
VLAN 12 : GRAPH (Graphisme) / 192.168.12.0/24
VLAN 13 : SERVEUR / 192.168.14.0/24 (interfacegigabit0/1 'gateway : 192.168.14.1)

Portserial : 10.0.0.2 255.255.255.252 se0/0/0 network 10.0.0.2/30
Pour accéder à ce routeur : @#sechack ()

--/        Routeur3 2811 

interface se0/2/0 : 10.0.0.1 255.255.255.252 network 10.0.0.0/30
interface se0/2/1 : 20.0.0.1 255.255.255.252 network 20.0.0.0/30

--/        Routeur1 2911

interface se0/0/0 : 20.0.0.2 255.255.255.252 network 20.0.0.0/
interface gigaeth0/0 : 192.168.13.1 255.255.255.0 network 192.168.13.0/24 (CIDR) NB : Réseau distant de l'ADMIN.

--/         Routage inter-vlans assuré par le routeur0 2911

Serveur centralisé (DNS; WEB): Mon siteweb en plein développement a été utilisé comme prototype
Serveur DNS : 192.168.14.1, nom de domaine : monportefolio.com
Serveur WEB : 192.168.14.1

--/         Routage RIP
Router> enable
Router# configure terminal
Router(config)# router rip
Router(config-router)# version 2                <-- Active RIP v2
Router(config-router)# no auto-summary          <-- Désactive le résumé auto (important)
Router(config-router)# network 192.168.14.0      <-- Réseau 1
Router(config-router)# network 10.0.0.0         <-- Réseau 2
Router(config-router)# exit

--/         ACLs configurées pour :

** Limiter l'accès entre VLANs
** Restreindre les accès au serveur

access-list 100 permit ip 192.168.13.0 0.0.0.255 192.168.14.0 0.0.0.255 (Routeur1 2911)
access-list 100 permit ip 192.168.14.0 0.0.0.255 192.168.13.0 0.0.0.255 (Routeur0 2911)

🔧 4. Fonctionnalités
----------------------

Fonction	Description

VPN IPsec	Tunnel sécurisé entre 2 routeurs
SSH	Connexion distante sécurisée sur routeurs
VLANs	Séparation logique des départements
ACLs	Contrôle d'accès inter-VLANs et vers le serveur
Trunking	Entre switchs et routeurs
DHCP (optionnel)	Attribution dynamique des IPs

🛠️ 5. Matériel utilisé
----------------------
Routeurs Cisco 2811 et 2911
Switchs 2960

PCs; serveurs; Accespoint, Télephone 
Cisco Packet Tracer

🔑 6. Sécurité
---------------
///* Utilisation de mots de passe chiffrés

Accès via SSH uniquement (Telnet désactivé)
------------------------------------------
le PC admin peut accéder au routeur de l'entrep à distance.
commande : ssh -l junior@# 10.0.0.2
user : junior@
password : pentest@
user : junior@#
password : chiffré (faire un show run dans le routeur0 2911)

///* ACLs bloquant les VLANs non autorisés

Tunnel VPN avec crypto ISAKMP + IPsec
Config. VPN avec ipsec-isakmp
Transform-set 
La mappage etc...
crypto isakmp key @Shodan#1589

🚀 7. Instructions d'utilisation
---------------------------------
Ouvrir le fichier .pkt dans Cisco Packet Tracer

Vérifier que le tunnel VPN est actif (ping inter-sites)

Tester les accès SSH depuis un PC vers les serveurs

Essayer d’accéder entre VLANs pour tester les ACLs

Lire le guide pour les détails IP/VLAN

✍️ 8. Auteur / Contexte
------------------------

Projet réalisé par Junior
Passionné des réseaux informatiques et Cybersécurité.

📎 9. Fichiers inclus
----------------------

ProjetInfraSécurisée.pkt
guide-technique.txt
reseau-securise.zip : archive compressée contenant tous les fichiers 
