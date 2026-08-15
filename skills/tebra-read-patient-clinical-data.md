---
name: tebra-read-patient-clinical-data
description: Read a patient's USCDI-aligned clinical record (demographics, conditions, medications, allergies, vitals, immunizations, care plan/team, documents) from the Tebra FHIR API using SMART on FHIR OAuth 2.0.
api: tebra:tebra-fhir-api
operations:
- getPatient
- getAllergyIntolerance
- getCondition
- getMedicationRequest
- getObservation
- getImmunization
- getCarePlan
- getCareTeam
- getDocumentReference
---

# Read patient clinical data (Tebra FHIR API)

Ground truth: `openapi/tebra-fhir-api-openapi.yml`, confirmed live 2026-08-14 (401 without a
token on every resource GET, 302 on the authorize endpoint).

## 1. Authenticate

Choose the SMART on FHIR flow that matches your app:

- **User-facing app** (patient or provider present): 3-legged authorization-code flow.
  - `GET https://fhir.prd.cloud.tebra.com/smartauth/oauth/authorize`
  - `POST https://fhir.prd.cloud.tebra.com/smartauth/oauth/token`
- **Backend service** (no end user): 2-legged client-credentials flow.
  - `POST https://fhir.prd.cloud.tebra.com/smartauth/oauth/token`

Both apps must be registered first through the appSphere developer portal
(`https://fhir.prd.cloud.tebra.com/appsphere/portal/#/login`) and reviewed by Tebra's FHIR
solutions team before the flow will issue tokens. See `authentication/tebra-authentication.yml`
and `scopes/tebra-scopes.yml` for the full scheme + scope list (scope strings are API
Evangelist's derivation from Tebra's documented resource list - Tebra's own guide does not
publish an enumerated scope catalog).

## 2. Resolve the patient

Call `getPatient` (`GET /Patient?id=<id>`) to confirm you have the right patient before
requesting clinical detail. `id` is required; `identifier`, `name`, `birthdate+name`, and
`gender+name` are optional match parameters per Tebra's guide.

## 3. Pull clinical resources

Every resource below is scoped with `patient=<id>` (required unless noted) - call only what
your use case needs, per Tebra's API Terms of Use (4.1: do not access information beyond what
the agreement/documentation allows):

| operationId | Returns |
|---|---|
| `getAllergyIntolerance` | Allergies / adverse reactions |
| `getCondition` | Problems, health concerns, encounter diagnoses |
| `getMedicationRequest` | Medication history (`patient` + `intent` required) |
| `getObservation` | Vitals, labs, smoking status (`patient` required; `code`/`category`/`date` narrow it) |
| `getImmunization` | Immunization history |
| `getCarePlan` | Assessment and plan of treatment (`patient` + `category` required) |
| `getCareTeam` | Care team members (`patient` + `status` required) |
| `getDocumentReference` | Clinical notes and other documents (`patient` required) |
| `getDiagnosticReport` | Lab results and report/note DiagnosticReports |
| `getEncounter` | Visit/encounter records |
| `getGoal` | Patient goals |
| `getDevice` | Implantable devices (UDI) |
| `getProcedure` | Procedures |
| `getProvenance` | Author/date provenance for any of the above (`patient` + `_revinclude=Provenance`) |

## 4. Handle errors

Responses are standard FHIR `OperationOutcome` bodies. See
`errors/tebra-problem-types.yml` for the confirmed code table (400/401/403/404/408/429 client;
500/502/503/504 server). On `429`, back off - Tebra's guide does not publish the exact quota,
only that it exists.

## 5. Respect the license

Per the FHIR API Terms of Use (4.5): patient-facing read access must remain free to the patient
- you may charge for your application, but not for the patient's own access to their data. Do not
redistribute or syndicate access to the API itself (4.5), and do not exceed reasonable request
volume (4.7).
