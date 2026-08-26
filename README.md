# Spring Cloud API Edge Gateway

## Student Information
* **Name:** Lahiru Mudith
* **Student Number:** CMS-ST-2026
* **GCP Project ID:** `cms-cloud-architecture`

---

## Service Overview
The **API Gateway** acts as the single entry gateway for the entire backend microservice mesh. All requests from the user dashboard client route through this gateway, which dynamically resolves logical service locations registered in Eureka and load-balances the traffic downstream.

* **Default Port:** `7000`
* **Technology:** Spring Cloud Gateway (Reactive WebFlux / Netty engine).
* **Target Environment:** OpenJDK 25, Spring Boot 4.1.1, Spring Cloud 2025.1.3.

---

## Centralized Routing Table
Routes are loaded dynamically from the Config Server properties sheet:
[`platform/api-gateway.yaml`](file:///C:/Users/Lahiru%20Mudith/Documents/Study/IJSE/4th%20Sem/Enterprise%20Cloud%20Architectur/Projects/Clinic-Management-System/cms-platform/config-server/src/main/resources/configurations/platform/api-gateway.yaml)

### Route Mappings:
1. **Patient Service Route:**
   * **Path:** `/api/v1/patients/**`
   * **Destination:** `lb://PATIENT-SERVICE`
2. **Doctor Service Route:**
   * **Path:** `/api/v1/doctors/**`
   * **Destination:** `lb://DOCTOR-SERVICE`
3. **Appointment Service Route:**
   * **Path:** `/api/v1/appointments/**`
   * **Destination:** `lb://APPOINTMENT-SERVICE`

---

## Global Cross-Origin (CORS) Configuration
To accommodate frontend browser integrations, the gateway defines global CORS allowances:
* **Allowed Origins:** `*` (Allows localhost:3000 node clients to connect).
* **Allowed Methods:** All (`GET`, `POST`, `PUT`, `DELETE`, `OPTIONS`).
* **Allowed Headers:** `*` (Permits standard JSON and multipart form attachments).

---

## Build and Run

### Build Command:
```bash
mvn clean package -DskipTests
```

### Execution Command:
```bash
java -jar target/Api-Gateway-1.0.0.jar
```
