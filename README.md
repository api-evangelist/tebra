# Tebra (tebra)

Tebra is a healthcare technology company providing an all-in-one operating system for independent medical practices - EHR, practice management, medical billing, patient engagement, and practice growth. Tebra was formed from the 2021 merger of **Kareo** (practice management and billing) and **PatientPop** (practice growth), and its developer surface still reflects that lineage.

Tebra exposes **two documented API surfaces**, both request/response over HTTPS:

1. **Tebra SOAP Practice Management API** - the former **Kareo Integration API**, still served at `https://webservice.kareo.com/services/soap/2.1/KareoServices.svc` (WSDL at `?wsdl`). Covers patients, appointments, providers, practices, charges, encounters, payments, transactions, and documents. **Access is partner / administrator gated** - a practice System Administrator must generate a customer key and grant permissions; there is no self-serve public signup. Authentication uses a customer key plus username and password. Tebra does **not** push data to external systems, so integrators poll (recommended every 5-15 minutes).

2. **Tebra Clinical Data API** - a REST **patient-access** API published under [tebra.com/macra](https://www.tebra.com/macra) for ONC / 21st Century Cures Act compliance, at `https://api.tebra.com/clinical/v1/api`. It exposes USCDI clinical data for a single authenticated patient. Authentication uses an **API Key** in the `X-Api-Key` header that the **patient** generates from the Tebra Patient Portal (My Account > API Access Key), at no charge.

> **Access model, honestly:** The practice-management (SOAP) surface is not open/self-serve - it is gated behind a customer key and partner onboarding. The clinical surface is a patient-access API keyed to an individual patient's own record, not a bulk practice data API. SOAP operation names in this catalog are confirmed from the live WSDL; the REST clinical resource paths and `X-Api-Key` auth are confirmed from Tebra's General API Documentation, while the request parameters and response schemas in the OpenAPI are modeled and should be verified against current Tebra docs.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/tebra/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/tebra/refs/heads/main/apis.yml)

## Tags

- Healthcare
- Practice Management
- EHR
- Medical Billing
- Patient Engagement
- Kareo
- PatientPop

## Timestamps

- **Created:** 2026-07-10
- **Modified:** 2026-07-10

## APIs

### Tebra Patients API (SOAP)

SOAP operations for patient records - `GetPatient`, `GetPatients`, `GetAllPatients`, `CreatePatient`, `UpdatePatient`, `UpdatePatientsExternalID`, `UpdatePrimaryPatientCase`.

- **Human URL:** [https://helpme.tebra.com/Tebra_PM/12_API_and_Integration](https://helpme.tebra.com/Tebra_PM/12_API_and_Integration)
- **Base URL:** `https://webservice.kareo.com/services/soap/2.1`
- [Documentation](https://helpme.tebra.com/Tebra_PM/12_API_and_Integration)
- [WSDL](https://webservice.kareo.com/services/soap/2.1/KareoServices.svc?wsdl)

### Tebra Appointments API (SOAP)

SOAP scheduling operations - `GetAppointment`, `GetAppointments`, `CreateAppointment`, `UpdateAppointment`, `UpdateAppointmentStatus`, `DeleteAppointment`, `GetAppointmentReasons`, `CreateAppointmentReason`.

- **Human URL:** [https://helpme.tebra.com/Tebra_PM/12_API_and_Integration](https://helpme.tebra.com/Tebra_PM/12_API_and_Integration)
- **Base URL:** `https://webservice.kareo.com/services/soap/2.1`
- [Documentation](https://helpme.tebra.com/Tebra_PM/12_API_and_Integration)
- [WSDL](https://webservice.kareo.com/services/soap/2.1/KareoServices.svc?wsdl)

### Tebra Providers and Practices API (SOAP)

SOAP reference-data operations - `GetProviders`, `GetPractices`, `GetServiceLocations`, `GetProcedureCodes`.

- **Human URL:** [https://helpme.tebra.com/Tebra_PM/12_API_and_Integration](https://helpme.tebra.com/Tebra_PM/12_API_and_Integration)
- **Base URL:** `https://webservice.kareo.com/services/soap/2.1`
- [Documentation](https://helpme.tebra.com/Tebra_PM/12_API_and_Integration)
- [WSDL](https://webservice.kareo.com/services/soap/2.1/KareoServices.svc?wsdl)

### Tebra Billing and Claims API (SOAP)

SOAP revenue-cycle operations - `GetCharges`, `GetEncounterDetails`, `CreateEncounter`, `UpdateEncounterStatus`, `GetPayments`, `CreatePayment`, `GetTransactions`.

- **Human URL:** [https://helpme.tebra.com/Tebra_PM/12_API_and_Integration](https://helpme.tebra.com/Tebra_PM/12_API_and_Integration)
- **Base URL:** `https://webservice.kareo.com/services/soap/2.1`
- [Documentation](https://helpme.tebra.com/Tebra_PM/12_API_and_Integration)
- [WSDL](https://webservice.kareo.com/services/soap/2.1/KareoServices.svc?wsdl)

### Tebra Documents API (SOAP)

SOAP document and vendor utilities - `CreateDocument`, `DeleteDocument`, `GetExternalVendors`, `RegisterExternalVendor`, `GetCustomerIdFromKey`, `GetThrottles`.

- **Human URL:** [https://helpme.tebra.com/Tebra_PM/12_API_and_Integration](https://helpme.tebra.com/Tebra_PM/12_API_and_Integration)
- **Base URL:** `https://webservice.kareo.com/services/soap/2.1`
- [Documentation](https://helpme.tebra.com/Tebra_PM/12_API_and_Integration)
- [WSDL](https://webservice.kareo.com/services/soap/2.1/KareoServices.svc?wsdl)

### Tebra Clinical Data API (REST)

REST patient-access API (ONC / Cures Act) exposing USCDI clinical data for a single authenticated patient - conditions, medications, allergies, immunizations, vital signs, procedures, encounters, care plans, goals, devices, diagnostic reports, smoking status, and a binary clinical summary.

- **Human URL:** [https://www.tebra.com/macra](https://www.tebra.com/macra)
- **Base URL:** `https://api.tebra.com/clinical/v1/api`
- [Documentation](https://www.tebra.com/macra)
- [API Reference (General API Documentation PDF)](https://www.tebra.com/wp-content/uploads/2023/10/General_API_Documentation-Tebra.pdf)
- [OpenAPI](openapi/tebra-clinical-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/tebra-clinical.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)

## Common Properties

- [LinkedIn](https://www.linkedin.com/company/tebra)
- [Website](https://www.tebra.com)
- [Documentation](https://helpme.tebra.com/Tebra_PM/12_API_and_Integration)
- [Plans](plans/tebra-plans-pricing.yml)
- [Rate Limits](rate-limits/tebra-rate-limits.yml)
- [Fin Ops](finops/tebra-finops.yml)

## Review

Does Tebra expose a documented public WebSocket API? **No.** Both API surfaces are request/response over HTTPS (SOAP for practice management, REST for clinical patient access), and Tebra explicitly does not push data to external systems - integrators poll. See [review.yml](review.yml).

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
