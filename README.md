# Tebra (tebra)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
