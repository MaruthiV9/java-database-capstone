
# Smart Clinic – Schema Architecture

## Section 1: Architecture Summary

The Smart Clinic application is built using Spring Boot and follows a layered architecture that separates concerns across presentation, business logic, and data persistence. It supports both MVC and REST-based interaction models. Thymeleaf templates are used to render the Admin and Doctor dashboards, while REST APIs provide functionality for patient-facing modules such as Appointments and Patient Records. This hybrid approach allows the system to serve both interactive web users and API consumers like mobile applications.

The backend application interacts with two different databases. MySQL is used to store relational and structured data such as patients, doctors, appointments, and administrative records, while MongoDB manages unstructured and flexible data such as prescriptions. Controllers pass requests to a dedicated service layer, which applies business rules and orchestrates workflows before delegating to repositories. MySQL operations rely on JPA entities, while MongoDB operations use document models annotated with `@Document`.

---

## Section 2: Numbered Flow of Data and Control

1. A user accesses the application through either a Thymeleaf-based dashboard (AdminDashboard or DoctorDashboard) or through REST API endpoints (e.g., Appointments, PatientDashboard).  
2. The incoming request is routed to the correct controller, depending on whether it is an MVC request (HTML) or an API request (JSON).  
3. The controller validates the request and delegates processing to the service layer.  
4. The service layer applies business rules, coordinates workflows (e.g., checking doctor availability), and determines what data operations are required.  
5. The service layer calls the appropriate repository—Spring Data JPA for MySQL or Spring Data MongoDB for MongoDB.  
6. The repository communicates with the underlying database engine, fetches or persists the requested data, and returns it as bound Java model classes (`@Entity` for MySQL, `@Document` for MongoDB).  
7. The service layer returns the processed models to the controller, which then either passes them to a Thymeleaf template for rendering HTML (MVC flow) or serializes them as JSON for API responses (REST flow).  




