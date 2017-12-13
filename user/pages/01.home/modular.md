---
title: Ceevee
menu: home

form:
    name: my-nice-form
    action: /home
    fields:
        - name: name
          label: Nom
          placeholder: Entrez votre nom
          autocomplete: on
          type: text
          validate:
            required: true

        - name: email
          label: Email
          placeholder: Entrez votre adresse e-mail
          type: text
          validate:
            rule: email
            required: true

        - name: message
          label: Message
          size: long
          placeholder: Entrez votre message ici
          type: textarea
          validate:
            required: true

    buttons:
        - type: submit
          value: Envoyer
          class: submit

    process:
        - email:
            from: "{{ config.plugins.email.from }}"
            to:
              - "{{ config.plugins.email.to }}"
              - "{{ form.value.email }}"
            subject: "[Feedback] {{ form.value.name|e }}"
            body: "{% include 'forms/data.html.twig' %}"
        - save:
            fileprefix: feedback-
            dateformat: Ymd-His-u
            extension: txt
            body: "{% include 'forms/data.txt.twig' %}"
        - message: Merci, je vous répondrai au plus vite !
        - display: thankyou

onpage_menu: true
content:
    items: @self.modular
    order:
        by: default
        dir: asc
        custom:
            - _about
            - _resume
            - _portfolio
            - _call
            - _testimonials
            - _contact
---
