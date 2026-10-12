```mermaid

C4Container
    title Container diagram for Job Tracker
    Person(user, "User", "Uses the system in a browser")
    Container(browser, "Browser", "HTML + HTMX + CSS", "User interface")
    Container(backend, "Django Backend", "Django 6.0.8", "Server-side application logic, HTML rendering")
    ContainerDb(db, "PostgreSQL", "PostgreSQL", "Persistent storage")
    Rel(user, browser, "Uses")
    Rel(browser, backend, "Sends HTTP requests", "HTTPS / HTMX")
    Rel(backend, db, "Reads/writes", "psycopg")