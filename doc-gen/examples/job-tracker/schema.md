```mermaid

erDiagram
    Bookmark {
        uuid id PK
        bigint status FK
        bigint type FK
        bigint resource FK
    }
    BookmarkStatus {
        bigint id PK
        slug code UK
    }
    BookmarkType {
        bigint id PK
        slug code UK
    }
    Company {
        uuid id PK
    }
    Course {
        uuid id PK
        bigint status FK
    }
    CourseStatus {
        bigint id PK
        slug code UK
    }
    CourseTask {
        uuid id PK
        uuid course FK
    }
    CoverLetterTemplate {
        bigint id PK
    }
    Event {
        uuid id PK
        uuid job FK
        bigint type FK
    }
    EventType {
        bigint id PK
        slug code UK
    }
    Exam {
        uuid id PK
        bigint resource FK
    }
    Job {
        uuid id PK
        bigint status FK
        bigint source FK
    }
    JobStatus {
        bigint id PK
        slug code UK
    }
    Project {
        uuid id PK
        bigint status FK
    }
    ProjectStatus {
        bigint id PK
        slug code UK
    }
    ProjectTask {
        uuid id PK
        uuid project FK
    }
    Resource {
        bigint id PK
        varchar domain UK
    }
    Source {
        bigint id PK
        varchar domain UK
    }
    Tool {
        uuid id PK
        bigint resource FK
    }
    Trainer {
        uuid id PK
        bigint resource FK
    }
    TrainerTask {
        uuid id PK
        uuid trainer FK
    }

    BookmarkStatus ||--o{ Bookmark : "fk"
    BookmarkType ||--o{ Bookmark : "fk"
    Resource ||--o{ Bookmark : "fk"
    CourseStatus ||--o{ Course : "fk"
    Course ||--o{ CourseTask : "fk"
    EventType ||--o{ Event : "fk"
    Job ||--o{ Event : "fk"
    Resource ||--o{ Exam : "fk"
    JobStatus ||--o{ Job : "fk"
    Source ||--o{ Job : "fk"
    ProjectStatus ||--o{ Project : "fk"
    Project ||--o{ ProjectTask : "fk"
    Resource ||--o{ Tool : "fk"
    Resource ||--o{ Trainer : "fk"
    Trainer ||--o{ TrainerTask : "fk"
