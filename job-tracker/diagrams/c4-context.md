```mermaid

C4Context
    title System Context diagram for Job Tracker
    Person(user, "User", "Uses the system in a browser")
    System(system, "Job Tracker", "The system under design")
    System_Ext(db_ext, "PostgreSQL", "PostgreSQL", "Persistent storage")
    Rel(user, system, "Uses", "HTTPS")
    Rel(system, db_ext, "Reads/writes", "SQL")
