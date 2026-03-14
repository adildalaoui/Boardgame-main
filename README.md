# Projet Java avec un pipeline sur Jenkins et AWS EC2

## Description

Ce projet est une application Java avec un pipeline basique sur Jenkins, hébergé sur une instance AWS EC2.
Le pipeline compile, teste et package l’application automatiquement pour chaque branche Git.
Un système de post-actions permet de :
déclencher un second pipeline après succès du premier
envoyer une notification par email avec le statut du build

## Technologies

- Java 17
- Apache Maven (test et packaging)
- Jenkins (pipeline multibranche + webhook GitHub)
- AWS EC2 (serveur pour Jenkins)
- Email Extension Plugin (Jenkins)

## Pipeline

Étapes principales :

mvn test → exécution des tests
mvn package → génération du package

Post-actions :
Si succès → déclenchement du pipeline secondaire (job-2)
Toujours → envoi d’un email avec le statut du build

## Installation

1. Instance EC2

sudo apt update
sudo apt install openjdk-17-jdk -y
java -version
   
2. Jenkins
   
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt update
sudo apt install jenkins -y
sudo systemctl start jenkins
sudo systemctl enable jenkins

Accès : http://<EC2_IP>:8080


3. Configuration Jenkins

 - Installer les plugins : GitHub, Pipeline, Email Extension
 - Créer un Multibranch Pipeline avec webhook
 - Définir le Jenkinsfile avec les étapes test, package et post-actions
   
## Pipeline 

Chaque commit sur GitHub déclenche automatiquement le pipeline principal
Post-actions : déclenchement du pipeline secondaire + email de notification

