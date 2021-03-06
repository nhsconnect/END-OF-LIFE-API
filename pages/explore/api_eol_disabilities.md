---
title: Disabilities Atomic Unit
keywords: usecase, Disability
tags: [rest, fhir, workflow,api]
sidebar: foundations_sidebar
permalink: api_eol_disabilities.html
summary: Atomic Unit to capture the disabilities for a patient.
toc: false
---
{% include custom/search.warnbanner.html %}

### Disabilities ###

Where a patient has any known disabilities, these may be captured by a healthcare professional as part of the End of life Care Plan. There are no limitations to what disabilities may be recorded, with each disability SNOMED coded within the record.

The following FHIR profiles are used to form the Disabilities Atomic Unit:

- [EOL-Patient-1](https://fhir.nhs.uk/STU3/StructureDefinition/EOL-Patient-1)
- [CareConnect-ProblemList-1](https://fhir.hl7.org.uk/STU3/StructureDefinition/CareConnect-ProblemList-1)
- [CareConnect-ProblemHeader-Condition-1](https://fhir.hl7.org.uk/STU3/StructureDefinition/CareConnect-ProblemHeader-Condition-1)
- [CareConnect-Practitioner-1](https://fhir.hl7.org.uk/STU3/StructureDefinition/CareConnect-Practitioner-1) (EOL mandates name.text)
- [CareConnect-PractitionerRole-1](https://fhir.hl7.org.uk/STU3/StructureDefinition/CareConnect-PractitionerRole-1)
- [CareConnect-Organization-1](https://fhir.hl7.org.uk/STU3/StructureDefinition/CareConnect-Organization-1)


### Disabilities data item mapping to FHIR profiles ###

The disabilities data items are fulfilled by elements within the FHIR resources listed below:

| EOL Data Item                       | FHIR resource element                                                   | Mandatory/Required/Optional |
|-------------------------------------|-------------------------------------------------------------------------|-----------------------------|
| List of Disabilities				  | CareConnect-ProblemList-1.entry.item											| Optional					|
| Patient Disability Code				  | CareConnect-ProblemHeader-Condition-1.code | Optional |
| Patient Disability Additional Notes | CareConnect-ProblemHeader-Condition-1.code.text | Mandatory |
| Professional Recording Disabilities | CareConnect-ProblemList-1.source | Mandatory |


### CareConnect-ProblemHeader-Condition-1.code (codeableConcept) Guidance ###

Where the sending system supports a terminology system:

* The codeableConcept.coding element MUST be populated with:
    * system: identity of the terminology system (e.g. SNOMED-CT) 
    * code: symbol in syntax defined by the system
	* display: representation defined by the system
* the codeableConcept.text field MUST be populated with the display value from the codeableConcept.coding.display element e.g. ‘Asthma (disorder)’
* the codeableConcept.text field MAY contain free text to capture more detail associated with the codeableConcept.coding.code e.g. ‘Patient uses blue inhaler to relieve symptoms’

Where the sending system does not support a terminology system:

* the codeableConcept.text field MUST be populated with a text description of the concept as a human readable narrative e.g ‘Asthma’. 
* the codeableConcept.text field MAY contain free text to capture more detail associated with the concept e.g. ‘Patient uses blue inhaler to relieve symptoms’.

<!--
### CareConnect-ProblemHeader-Condition-1.code Guidance ###

Where the sending system supports a disability code:

* The condition.code element MUST be populated with:
    * the terminology system (e.g. SNOMED-CT) 
    * code
	* display value
* the condition.code.text field MUST be populated with the display value from the condition.code.display element e.g. ‘Asthma (disorder)’
* the condition.code.text field MAY contain free text to capture more detail associated with the condition.code e.g. ‘Patient uses blue inhaler to relieve symptoms’

Where the sending system does not support a disability code:

* the condition.code.text field MUST be populated with a text description of the condition as a human readable narrative e.g ‘Asthma’. 
* the condition.code.text field MAY contain free text to capture more detail associated with the condition e.g. ‘Patient uses blue inhaler to relieve symptoms’
-->

### Disabilities Example XML ###

<script src="https://gist.github.com/IOPS-DEV/e4740ee872d5bc5be5c254ce42c6dc7b.js"></script>

<script src="https://gist.github.com/IOPS-DEV/5648828bd8b611fa938b3562a5c3e162.js"></script>

### Care Connect Profiles ###

Where possible, Care Connect profiles have been used to develop the End of Life API. On this occasion it has not been possible to do this. The table below highlights the Care Connect profile(s) replaced with a bespoke version and the rationale behind this.

| Care Connect Profile 	| Rationale for Change								     | New Component Required					 	   |
|-----------------------|--------------------------------------------------------|-------------------------------------------------|
| CareConnect-Condition-1 | Cardinality change									 | code.text requires 1:1 cardinality   		   |


End of Life will engage with the healthcare community and INTEROPen in the future to propose these changes to the Care Connect profiles(s).
