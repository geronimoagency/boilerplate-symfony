# Technical test for back-end developer

--------- FRENCH VERSION ------------

## Objectifs :
- Créer une page de contact avec des champs dynamiques
```
1. Le formulaire doit enregister les demandes de contact dans une table appellée 'contacts'
2. Au choix du sujet, les champs du formulaire sont mis à jour ( sans refresh de la page )
```

> Voici les différents champs du formulaire de contact ( ceux-ci changent en fonction du sujet sélectionné )
- Champs communs :
    - Sujet [ Choix parmis ("Demande de contact", "Signaler un problème", "Demande d'inscription") ] *required
    
- Champs quand "Demande de contact" est sélectionné :
    - Email [ email ] *required
    - Nom [ Texte court libre ] *required
    - Message [ Texte long libre ] *required
    
- Champs quand "Signaler un problème" est sélectionné :
    - Raison [ Choix parmis ("Une erreur est survenue", "J'ai besoin d'aide", "Autre") ] *required
    - Details [ Texte libre ] *required
    
- Champs quand "Demande d'inscription" est sélectionné :
    - Email [ email ] *required
    - Nom [ Texte court libre ] *required
    - Numéro de téléphone *optional
    - Adresse *required
    - Message [ Texte long libre ] *optionaltest
    
    --------- ENGLISH VERSION ------------
    
    ## Objectives: 
    
Create a contact page with dynamic fields 
1. The form must register the contact requests un a table called « contacts » 
2. When choosing the subject, the fields in the form are updated (no need to refresh the page) 
Find hereunder the fields in a contact form (they change according to the selected subject) 
Common fields: 
Subject [ Choice between (« Contact request », « Notify of a problem », « Registration request ») ] *required
Fields when « Contact request » is selected: 
    Email [ email ] *required
        Surname [ Short free text ] *required
        Message [ Long free text ] *required
Fields when « Notify of a problem » is selected: 
    Object (or reason) [ Chose between (« An error has occurred », « I need help » , « Other ») ] *required
        Details [ Free text ] *required
Fields when « Registration request » is selected: 
    Email [ email ] *required
        Surname (or name) [ Texte court libre ] *required
        Phone number *optional
        Adress *required
        Message [ long free text ] *optionaltest
