---
description: Data Model Notes
---

# Data Model

### Data vs Metadata

* Data
  * Patients, Encounters, Observations
  * Requires metadata
  * Private, secure information
    * ex. name, phone number, DOB
* Metadata
  * Concept dictionary, forms, report definitions
    * ex. address hierarchy, phone types
  * Shareable, open to others

### Visits, Encounters, Observations

* Visits
  * Time period when patient is in clinic
  * Defines time period of patient care and treatment
  * Can consist of one or more encounters
* Encounters
  * Brief time a patient has a single location and provider
  * Every form creates an encounter
  * Can belong to visit, but not necessarily&#x20;
  * ex. registration, picking up medication, lab test administration
  * Every encounter includes:
    * patient\_id
    * location\_id
    * encounter\_datetime
    * provider
    * encounter\_type
    * visit\_id (optional)
* Observation
  * Details of an encounter
  * ex. registration encounter -> occupation, gender = observations
  * ex. pharmacy encounter -> drug, dosage = observations

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption><p>BISB</p></figcaption></figure>

### Person, Relationship&#x20;

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption><p>provider? I hardly know her</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption><p>as long as the outcome is income</p></figcaption></figure>

### Patient

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption><p>Patience is a virtue </p></figcaption></figure>

### Roles, Privileges

* Roles
  * Group of privileges
  * Roles may inherit from other roles
  * Users may have one or more role(s)
* Privileges
  * Authorization to perform certain actions
  * Defined by the core system and modules

### Providers

* I hardly know her
* Provide care or services to patients
* Any healthcare worker a patient can have an encounter with is considered a provider in the openMRS system
* ex. clinician, receptionist, lab tech, pharmacist

