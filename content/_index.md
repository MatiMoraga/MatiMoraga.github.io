---
# Leave the homepage title empty to use the site title
title: 'Matías Moraga'
summary: ''
date: 2026-01-05
type: landing

sections:
  # Developer Hero
  - block: dev-hero
    id: hero
    content:
      username: me
      greeting: "Hola, soy"
      show_status: true
      show_scroll_indicator: true
      typewriter:
        enable: true
        prefix: "Me especializo en"
        strings:
          - "modelamiento y optimización de procesos"
          - "diseño de equipos"
          - "evaluación de proyectos"
        type_speed: 70
        delete_speed: 40
        pause_time: 2500
      cta_buttons:
        - text: Ver mi trabajo
          url: "#projects"
          icon: arrow-down
        - text: Contáctame
          url: "#contact"
          icon: envelope
    design:
      style: centered
      avatar_shape: circle
      animations: false
      background:
        color:
          light: "#fafafa"
          dark: "#0a0a0f"
      spacing:
        padding: ["6rem", "0", "4rem", "0"]

  # Portfolio
  - block: portfolio
    id: projects
    content:
      title: "Proyectos personales"
      subtitle: "Una selección de mis proyectos más recientes"
      count: 0
      filters:
        folders:
          - projects
      buttons:
        - name: Todos
          tag: '*'
        - name: Oil & Gas
          tag: Oil & Gas
        - name: Minería
          tag: Minería
        - name: Celulosa y papel
          tag: Celulosa y papel
        - name: Tratamiento de aguas
          tag: Tratamiento de aguas
        - name: Alimentos
          tag: Alimentos
      default_button_index: 0
    design:
      columns: 3
      background:
        color:
          light: "#ffffff"
          dark: "#0d0d12"
      spacing:
        padding: ["4rem", "0", "4rem", "0"]

  # Tech Stack
  - block: tech-stack
    id: skills
    content:
      title: "Habilidades"
      subtitle: "Tecnologías y herramientas que uso"
      categories:
        - name: Lenguajes
          items:
            - name: MATLAB
              icon: devicon/matlab
            - name: Python
              icon: devicon/python
        - name: Softwares
          items:
            - name: Excel
              icon: custom/excel
            - name: PowerBI
              icon: custom/powerbi
            - name: AutoCAD
              icon: custom/autocad
        - name: Simuladores
          items:
            - name: Aspen Hysys
              icon: custom/aspen-hysys
            - name: DWSIM
              icon: custom/dwsim
    design:
      style: grid
      show_levels: false
      background:
        color:
          light: "#f5f5f5"
          dark: "#08080c"
      spacing:
        padding: ["4rem", "0", "4rem", "0"]

  # Experience Timeline
  - block: resume-experience
    id: experience
    content:
      title: "Experiencia"
      date_format: Jan 2006
      items:
        - title: Practicante de ingeniería
          company: Green I&C
          company_url: ''
          company_logo: ''
          location: Santiago, Chile
          date_start: '2022-01-03'
          date_end: '2022-03-11'
          description: |2-
            * Apoyo y revisión de documentación en proyectos de ingeniería de carácter técnico-ambiental para los sectores minero y energético: cuantificación de huella de carbono, análisis de riesgos, diseño de equipos y simulación de procesos.
            * Proyecto de práctica en estudio y análisis de simulaciones hidráulicas de carga y descarga de combustibles.
        - title: Practicante de ingeniería
          company: FPC TISSUE
          company_url: ''
          company_logo: ''
          location: Santiago, Chile
          date_start: '2020-02-03'
          date_end: '2020-02-28'
          description: |2-
            * Colaborador en la elaboración del documento oficial "Manual de la Química del Extremo Húmedo".
        - title: Practicante de laboratorio
          company: Energía León
          company_url: ''
          company_logo: ''
          location: Chile
          date_start: '2019-02-04'
          date_end: '2019-03-01'
          description: |2-
            * Ayudante de laboratorio para la medición de parámetros y análisis de aguas industriales en planta de energía y calderas.
    design:
      columns: '1'
      background:
        color:
          light: "#ffffff"
          dark: "#0d0d12"
      spacing:
        padding: ["4rem", "0", "4rem", "0"]

  # Contact Section
  - block: contact-info
    id: contact
    content:
      title: Contacto
      subtitle: "Trabajemos juntos"
      text: |-
        Siempre estoy interesado en escuchar sobre nuevos proyectos y oportunidades.
        ¡No dudes en escribirme!
      email: matias.moraga.pendola@gmail.com
      autolink: true
    design:
      columns: '1'
      background:
        color:
          light: "#ffffff"
          dark: "#0d0d12"
      spacing:
        padding: ["4rem", "0", "4rem", "0"]

  # CTA Card
  - block: cta-card
    content:
      title: "Abierto a nuevas oportunidades"
      text: |-
        Actualmente busco oportunidades laborales como **ingeniero de proyectos o ingeniero de procesos** a nivel Trainee o Junior.
        
        Conversemos sobre cómo puedo aportar a tu equipo.
      button:
        text: 'Descargar curriculum'
        url: uploads/resume.pdf
        new_tab: true
    design:
      card:
        css_class: 'bg-gradient-to-br from-primary-200 via-primary-100 to-secondary-200 dark:from-primary-600 dark:via-primary-700 dark:to-secondary-700'
        text_color: dark
      background:
        color:
          light: "#f5f5f5"
          dark: "#08080c"
      spacing:
        padding: ["4rem", "0", "6rem", "0"]
---
    
  # Recent Blog Posts
  # - block: collection
  #   id: blog
  #   content:
  #     title: Publicaciones recientes
  #     subtitle: 'Reflexiones sobre ingeniería, procesos y más'
  #     text: ''
  #     filters:
  #       folders:
  #         - blog
  #       exclude_featured: false
  #     count: 3
  #     order: desc
  #   design:
  #     view: card
  #     columns: 3
  #     background:
  #       color:
  #         light: "#f5f5f5"
  #         dark: "#08080c"
  #     spacing:
  #       padding: ["4rem", "0", "4rem", "0"]
  
