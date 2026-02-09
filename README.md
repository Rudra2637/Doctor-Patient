## ER Diagram Explanation
This ER diagram represents a doctor appointment booking system where a single user account can manage appointments for multiple individuals.

A *User* is the account holder who logs into the application. One user can create and manage multiple *Patient* profiles (self or family members), resulting in a *one-to-many* relationship between User and Patient.

The *Doctor* entity stores general information about medical professionals. A single doctor can attend multiple appointments, establishing a *one-to-many* relationship between Doctor and Appointment.

Doctor availability is maintained separately in the *Doctor_Availability* entity. Since a doctor can be available on multiple days and time slots, the relationship between Doctor and Doctor_Availability is also *one-to-many*.

The *Appointment* entity is the central entity of the system, connecting patients with doctors. It stores details such as consultation type, time slot, token number, and appointment status.

This design ensures proper normalization, reduces redundancy, and supports scalability for a real-world appointment booking system.


```mermaid
erDiagram

    USER {
        int user_id PK
        string mobile_number
        string auth_token
        datetime created_at
    }

    PATIENT {
        int patient_id PK
        int user_id FK
        string name
        int age
        string sex
        float weight
        string relation
    }

    DOCTOR {
        int doctor_id PK
        string name
        string specialization
        int experience_years
        string qualifications
    }

    DOCTOR_AVAILABILITY {
        int availability_id PK
        int doctor_id FK
        string day_of_week
        time start_time
        time end_time
        int slot_duration
    }

    APPOINTMENT {
        int appt_id PK
        int patient_id FK
        int doctor_id FK
        date appointment_date
        string time_slot
        string consultation_type
        int token_number
        string status
        string payment_status
    }

    USER ||--o{ PATIENT : manages
    PATIENT ||--o{ APPOINTMENT : books
    DOCTOR ||--o{ APPOINTMENT : attends
    DOCTOR ||--o{ DOCTOR_AVAILABILITY : has
