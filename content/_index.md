---
# Leave the homepage title empty to use the site title
title: 'Matías Moraga'
summary: ''
date: 2026-01-05
type: landing

sections:
  # Developer Hero - Gradient background with name, role, social, and CTAs
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
  
  # Filterable Portfolio - Alpine.js powered project filtering
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
        - name: Tratamiento de aguas
          tag: Tratamiento de aguas
      default_button_index: 0
    design:
      columns: 3
      background:
        color:
          light: "#ffffff"
          dark: "#0d0d12"
      spacing:
        padding: ["4rem", "0", "4rem", "0"]
  
  # Visual Tech Stack - Icons organized by category
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
              icon: devicon/excel
            - name: PowerBI
              icon: devicon/powerbi
        - name: Simuladores
          items:
            - name: Aspen Hysys
              icon: devicon/aspen
            - name: DWSIM
              icon: devicon/dwsim
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
      title: Experiencia
      date_format: Jan 2006
      items:
        - title: Senior Software Engineer
          company: Tech Corp
          company_url: ''
          company_logo: ''
          location: San Francisco, CA
          date_start: '2023-01-01'
          date_end: ''
          description: |2-
            * Lead development of microservices architecture serving 1M+ users
            * Improved API response time by 40% through optimization
            * Mentored team of 5 junior developers
            * Tech stack: React, Node.js, PostgreSQL, AWS
        - title: Full-Stack Developer
          company: Startup Inc
          company_url: ''
          company_logo: ''
          location: Remote
          date_start: '2021-06-01'
          date_end: '2022-12-31'
          description: |2-
            * Built and deployed 3 production applications from scratch
            * Implemented CI/CD pipeline reducing deployment time by 60%
            * Collaborated with design team on UI/UX improvements
            * Tech stack: Next.js, Express, MongoDB, Docker
        - title: Junior Developer
          company: Web Agency
          company_url: ''
          company_logo: ''
          location: New York, NY
          date_start: '2020-01-01'
          date_end: '2021-05-31'
          description: |2-
            * Developed client websites using modern web technologies
            * Maintained and updated legacy codebases
            * Participated in code reviews and agile ceremonies
            * Tech stack: React, WordPress, PHP, MySQL
    design:
      columns: '1'
      background:
        color:
          light: "#ffffff"
          dark: "#0d0d12"
      spacing:
        padding: ["4rem", "0", "4rem", "0"]
  
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
