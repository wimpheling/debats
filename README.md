# LES-DEBATS.FR

# Base de données

## Tracking des modifications:
https://github.com/grantmcconnaughey/django-field-history

## Debat
- nom
- Emission (référence)
- date
- nombre de vues
- Invités (référence multiple : Intervenant)
- Animateurs (référence multiple : Intervenant)
- Videos (référence multiple)
- Tags (tags, il doit y avoir un plugin django pour gérer ca)
### API

  #### lire
  - url : _/debat/:id_
  - accès public
  - retourne les champs de l'objet débat avec toutes les tables jointes renseignées (nom des invités, contenus videos etc)
  -

  ### listes par criteres
   - url : _/debat/_
   - accès public
   - criteres : filtres par
     - année
     - intervenant (en invité ou en animateur ou les 2)
     - tag
     - video
   - paginée par 10
   - triée (ordre des résultats) par
     - date d'upload
     - nombre de vues

  ### ajouter
   - crud standard
   - accès reservé aux membres connectés

 ### editer
   - la demande d'édition est stockée dans une nouvelle table mais pas
   - acces reservé aux membres connectés
   - chaque modification doit etre loggée et visible

  ### effacer
   - crud standard
   - acces reservé aux admins


## Emission
- Titre
- Media (référence)
- Auteur (reference utilisateur)
- Date de création
- Date de modification

### API

  - **API STANDARD A UTILISER POUR MEDIA VIDEO INTERVENANT**

  #### lire
  - url : _/emission/:id_
  - accès public

  #### editer
  - cf editer page

  #### effacer
  - reservé aux admins

  #### créer
  - reservé aux users

  ### liste
  - acces public
  - totalité ou filtrable par recherche (pour les autocomplete)

## Media
- Nom
- Logo
- Auteur (reference utilisateur)
- Date de création
- Date de modification

## Video
- Lien Video (url youtube / dailymotion)
- Auteur (reference utilisateur)
- Date de création
- Date de modification

  _Todo : intégrer d'autres source media (bfm etc) ? voir ce qui existe en plugin django ou js_

## Intervenant (invité ou animateur)
- Nom
- Prénom(s)
- Photo
- Voir plus de champs (description, lien wikipedia, age ...)
- Auteur (reference utilisateur)
- Date de création
- Date de modification

## Compte utilisateur
- Username
- Nom
- Prénom
- Email
- Mot de passe
- Token twitter
- Token FB
- Admin (booleen)

### API : standard, on va essayer d'utiliser un plugin de django pour gérer cette partie

## Demande de modifications
- auteur (reference Utilisateur)
- date
- accepté par (reference utilisateur)
- date d'acceptation
- refusé par (reference utilisateur)
- date de refus
- statut (en attente/accepte/refuse)
- type d objet
- id de l'objet
- propriete de l'objet
- nouvelle valeur

  ### API

  #### liste
  - url : _modification/_
  - filtrable par statut
  - triée par date
  - reservé aux users
  - si on n'est pas admin, ne retourne que la liste des modifs dont je suis l'auteur

  ### accepter
  - reservé aux admins
  - la demande est marquée comme acceptée et la date d'acceptation mise à jour
  - la propriété de l'objet est mise à jour selon les données saisies dans la demande

  ### refuser
  - reservé aux admins
  - la demande est marquée comme refusée et la date de refus est mise à jour
