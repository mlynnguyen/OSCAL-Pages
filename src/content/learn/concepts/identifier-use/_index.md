---
title: Identifier Use and UUIDs
date: 2022-01-25 17:05:15 -0500
description: Provides details on the scope and uniqueness of identifiers used within the OSCAL models.
suppresstopiclist: true
weight: 50
toc:
  enabled: true
sidenav:
  focusrenderdepth: 2
  activerenderdepth: 2
  inactiverenderdepth: 2
aliases:
  - /concepts/identifier-use/
---

<br>
<div class="usa-card-group">
    <div class="usa-card tablet:grid-col">
        <div class="usa-card__container">
            <div class="usa-card__body">
                
In OSCAL, **identifiers** play a critical role in referencing and linking data consistently and reliably across models. Whether human-readable or machine-generated, these identifiers ensure that elements within OSCAL documents or across multiple documents can be uniquely and accurately referenced.

This page provides an overview of how identifiers are used in OSCAL, with a focus on the role of **machine-oriented and Universally Unique Identifiers (UUIDs)**. You'll learn about the types of identifiers supported in OSCAL, why UUIDs are used, and how they contribute to maintaining data integrity and consistency across complex systems. 
            </div>
        </div>
    </div>
</div>


---

### Identifier Types
By design, OSCAL supports **two main types of identifiers**: [*machine-oriented*](#1-machine-oriented-identifiers) and [*human-oriented*](#2-human-oriented-identifiers) identifiers. The OSCAL models dictate which are used for different data items.

#### 1. Machine-Oriented Identifiers

**Machine-oriented** identifiers provide a persistent identity for an entity within the OSCAL models, which can be used in other locations within related OSCAL models to reference the associated entity. 

These identifiers are intended to be auto-generated by tools when the entity is initially created. In OSCAL, a machine-oriented identifier is implemented using a Universally Unique Identifier (UUID) as defined by [RFC 4122](https://tools.ietf.org/html/rfc4122). A UUID is represented in OSCAL using the [UUID datatype](https://pages.nist.gov/OSCAL-Reference/models/datatypes/#uuid).
UUIDs were chosen because:
- Programming interfaces exist in most programming environments to generate a UUID
- UUIDs can be issued without a central authority
- UUIDs are represented in 128 bits, providing for a large address space with low risk of identifier collisions for randomly generated values

{{<callout>}}The opaque nature of UUIDs, which consist of a series of hexadecimal characters, makes them less than ideal for wildcard matching scenarios.  Thus, their use in OSCAL is intended for identification only where an exact match is required. Where wildcard matching is needed, the other data elements associated with the entity should be evaluated for a match instead. {{</callout>}}

The [OSCAL XML Reference Index](https://pages.nist.gov/OSCAL-Reference/models/latest/complete/xml-index/#/@uuid) and [OSCAL JSON Reference Index](https://pages.nist.gov/OSCAL-Reference/models/latest/complete/json-index/#/uuid) provide a listing of UUIDs in the core OSCAL models.  References to these identifiers typically follow a naming convention of the object type followed by “-uuid”.  For example, see the XML reference index for [location-uuid](https://pages.nist.gov/OSCAL-Reference/models/latest/complete/xml-index/#/location-uuid) (or [location-uuids](https://pages.nist.gov/OSCAL-Reference/models/latest/complete/json-index/#/uuid) in the JSON reference index).

<br>

#### 2. Human-Oriented Identifiers

A **human-oriented** identifier incorporates semantic that support readability and processing by humans. OSCAL implements human-oriented identifiers as [token](https://pages.nist.gov/OSCAL-Reference/models/datatypes/#token) data types, which are non-colonized names.  For example, control identifiers in a catalog may use a nomenclature that is familiar to the intended audience, allowing them to quickly determine what security control is being referred to, simply by its identifier value.  

The [OSCAL XML Reference Index](https://pages.nist.gov/OSCAL-Reference/models/latest/complete/xml-index/#/@id) and [OSCAL JSON Reference Index](https://pages.nist.gov/OSCAL-Reference/models/latest/complete/json-index/#/id) provide a comprehensive listing of the human-oriented IDs in the core OSCAL models.  References to these IDs are typically named according to the referenced object type (e.g., control) followed by “-id”, as seen here in the [XML Reference Index](https://pages.nist.gov/OSCAL-Reference/models/latest/complete/xml-index/#/@control-id) (and likewise [JSON Reference Index](https://pages.nist.gov/OSCAL-Reference/models/latest/complete/json-index/#/control-id) in the JSON reference index).

<br>

---

### Uniqueness
OSCAL identifier uniqueness is categorized as <em id="locally-unique">*locally-unique*</em> or <em id="globally-unique">*globally-unique*</em>.  As implied by the category name, **locally-unique** identifiers must be unique within the current document, whereas **globally-unique** identifiers are guaranteed to be unique across all other identifiers.  OSCAL’s [*machine-oriented*](#1-machine-oriented-identifiers) UUID identifiers are always globally-unique.  [*Human-oriented*](#2-human-oriented-identifiers) identifiers must be defined and managed organizationally and are more susceptible to identifier duplication or collisions. Thus, human-oriented identifiers are less likely or cannot be guaranteed to be globally-unique.

<br>

---

### Scope

Identifiers that are only intended for use within the same OSCAL instance are categorized as <em id="instance">*instance*</em> scope.  However, since OSCAL supports composition relationships, there are many cases where identifiers in a source OSCAL instance need to be referenced from other OSCAL instances.  These are considered <em id="cross-instance">*cross-instance*</em> scoped identifier references.  The figure below illustrates how the core OSCAL models relationships are established through import and link mechanisms, enabling **cross-instance** references.

![A diagram depicting the relationships between OSCAL models. The solid black arrows depict relationships implemented via the import mechanism (e.g., import, import-profile, import-component-definition, import-ssp, and import-ap), whereas the dashed red line arrows illustrate relationships established through links.](oscal-model-relationships.svg)

The following import types are supported:
- import - see [XML index](https://pages.nist.gov/OSCAL-Reference/models/latest/complete/xml-index/#/import) or [JSON index](https://pages.nist.gov/OSCAL-Reference/models/latest/complete/json-index/#/imports)
- import-component-definition - see [XML index](https://pages.nist.gov/OSCAL-Reference/models/latest/complete/xml-index/#/import-component-definition) or [JSON index](https://pages.nist.gov/OSCAL-Reference/models/latest/complete/json-index/#/import-component-definitions)
- import-profile - see [XML index](https://pages.nist.gov/OSCAL-Reference/models/latest/complete/xml-index/#/import-profile) or [JSON index](https://pages.nist.gov/OSCAL-Reference/models/latest/complete/json-index/#/import-profile)
- import-ssp - see [XML index](https://pages.nist.gov/OSCAL-Reference/models/latest/complete/xml-index/#/import-ssp) or [JSON index](https://pages.nist.gov/OSCAL-Reference/models/latest/complete/json-index/#/import-ssp)
- import-ap - see [XML index](https://pages.nist.gov/OSCAL-Reference/models/latest/complete/xml-index/#/import-ap) or [JSON index](https://pages.nist.gov/OSCAL-Reference/models/latest/complete/json-index/#/import-ap)

When implementing cross-instance references, identifier must be referenced in the context of the containing resource. The appropriate import attribute should be used (similar to a namespacing) to deconflict identifiers with the same values in the associated OSCAL instances.  This is particularly important for human-oriented identifiers that may not be globally unique but still require cross-instance scoping.  For example, this technique allows for the same control IDs to be used and referenced in a profile and its imported catalog(s) without conflict.  

<br>

---

### Identifier Scope Across OSCAL Models
Each OSCAL model defines its own set of identifiers, which may be references either within the same model or across related models in a broader OSCAL document ecosystem. Understanding how identifiers are scoped and referenced is essential for ensuring consistent data linkage and model integrity.

The following section describes **how identifiers are defined and scoped** in each OSCAL model, from catalogs and profiles to system security plans (SSPs), assessment plans (APs), and more. You'll also find tables listing the core identifiers used in each model, along with their types (machine-oriented or human-oriented) and how they're represented in XML and JSON.

The next section describes the identifier scoping per defining model.

<br>

#### **Catalog Identifiers**
Identifiers defined in a catalog may be referenced locally or from an importing profile ([see the diagram in the Scope section](#scope)). Additionally, identifiers defined in a catalog may be referenced in other upstream OSCAL instances in a hierarchical set of associated OSCAL documents (e.g., SSPs, assessment plans, assessment results, and POA&Ms). The table below provides a listing of the core OSCAL catalog model identifiers.

|**Defining Model**|**Identifier Type**|**Identifiers**|
|:------|:-------|:-----:|
|Catalog|Machine-Oriented|[XML Index](https://pages.nist.gov/OSCAL-Reference/models/latest/catalog/xml-index/#/@uuid) &#124; [JSON Index](https://pages.nist.gov/OSCAL-Reference/models/latest/catalog/json-index/#/uuid)|
|Catalog|Human-Oriented|[XML Index](https://pages.nist.gov/OSCAL-Reference/models/latest/catalog/xml-index/#/@id) &#124; [JSON Index](https://pages.nist.gov/OSCAL-Reference/models/latest/catalog/json-index/#/id)|

<br>

#### **Profile Identifiers**
Identifiers defined in a profile may be referenced locally or from an importing profile or SSP ([see the diagram in the Scope section](#scope)). Component definitions can reference these identifiers through its [control-implementation - source](https://pages.nist.gov/OSCAL-Reference/models/latest/component-definition/xml-reference/#/component-definition/component/control-implementation/@source) reference to the profile.  Other upstream OSCAL models, including assessment plans, assessment results, and POA&Ms can also reference these profile identifiers via the hierarchical set of associated OSCAL documents.  The table below provides a listing of the core OSCAL profile model identifiers.

|**Defining Model**|**Identifier Type**|**Identifiers**|
|:------|:-------|:-----:|
|Profile|Machine-Oriented|[XML Index](https://pages.nist.gov/OSCAL-Reference/models/latest/profile/xml-index/#/@uuid) &#124; [JSON Index](https://pages.nist.gov/OSCAL-Reference/models/latest/profile/json-index/#/uuid)|
|Profile|Human-Oriented|[XML Index](https://pages.nist.gov/OSCAL-Reference/models/latest/profile/xml-index/#/@id) &#124; [JSON Index](https://pages.nist.gov/OSCAL-Reference/models/latest/profile/json-index/#/id)|

<br>

#### **Component Definition Identifiers**
Identifiers defined in a component definition may be referenced locally or from an importing component definition instance ([see the diagram in the Scope section](#scope)). SSPs may also reference identifiers from a component definitions through its implementation of links for a given component.Other upstream OSCAL models, including assessment plans, assessment results, and POA&Ms can also reference these component definition indirectly (e.g., via reference to an SSP component that has a a link to a component definition).  The table below provides a listing of the core OSCAL component definition model identifiers.

|**Defining Model**|**Identifier Type**|**Identifiers**|
|:------|:-------|:-----:|
|Component Definition|Machine-Oriented|[XML Index](https://pages.nist.gov/OSCAL-Reference/models/latest/component-definition/xml-index/#/@uuid) &#124; [JSON Index](https://pages.nist.gov/OSCAL-Reference/models/latest/component-definition/json-index/#/uuid)|
|Component Definition|Human-Oriented|[XML Index](https://pages.nist.gov/OSCAL-Reference/models/latest/component-definition/xml-index/#/@id) &#124; [JSON Index](https://pages.nist.gov/OSCAL-Reference/models/latest/component-definition/json-index/#/id)|

<br>

#### **SSP Identifiers**
Identifiers defined in an SSP may be referenced locally or from an importing AP or POA&M ([see the diagram in the Scope section](#scope)). SSP identifiers can also be referenced from the AR through its hierarchical relationship with AP. The table below provides a listing of the core OSCAL SSP model identifiers.

|**Defining Model**|**Identifier Type**|**Identifiers**|
|:------|:-------|:-----:|
|SSP|Machine-Oriented|[XML Index](https://pages.nist.gov/OSCAL-Reference/models/latest/system-security-plan/xml-index/#/@uuid) &#124; [JSON Index](https://pages.nist.gov/OSCAL-Reference/models/latest/system-security-plan/json-index/#/uuid)|
|SSP|Human-Oriented|[XML Index](https://pages.nist.gov/OSCAL-Reference/models/latest/system-security-plan/xml-index/#/@id) &#124; [JSON Index](https://pages.nist.gov/OSCAL-Reference/models/latest/system-security-plan/json-index/#/id)|

<br>

#### **AP Identifiers**
Identifiers defined in an AP may be referenced locally or from an importing AR ([see the diagram in the Scope section](#scope)). The table below provides a listing of the core OSCAL AP model identifiers.

|**Defining Model**|**Identifier Type**|**Identifiers**|
|:------|:-------|:-----:|
|AP|Machine-Oriented|[XML Index](https://pages.nist.gov/OSCAL-Reference/models/latest/assessment-plan/xml-index/#/@uuid) &#124; [JSON Index](https://pages.nist.gov/OSCAL-Reference/models/latest/assessment-plan/json-index/#/uuid)|
|AP|Human-Oriented|[XML Index](https://pages.nist.gov/OSCAL-Reference/models/latest/assessment-plan/xml-index/#/@id) &#124; [JSON Index](https://pages.nist.gov/OSCAL-Reference/models/latest/assessment-plan/json-index/#/id)|

<br>

#### **AR Identifiers**
Identifiers defined in an AR may be referenced locally ([see the diagram in the Scope section](#scope)).  However, observations, risks, and findings may also be referenced implicitly in the POA&M. The table below provides a listing of the core OSCAL AR model identifiers.

|**Defining Model**|**Identifier Type**|**Identifiers**|
|:------|:-------|:-----:|
|AR|Machine-Oriented|[XML Index](https://pages.nist.gov/OSCAL-Reference/models/latest/assessment-results/xml-index/#/@uuid) &#124; [JSON Index](https://pages.nist.gov/OSCAL-Reference/models/latest/assessment-results/json-index/#/uuid)|
|AR|Human-Oriented|[XML Index](https://pages.nist.gov/OSCAL-Reference/models/latest/assessment-results/xml-index/#/@id) &#124; [JSON Index](https://pages.nist.gov/OSCAL-Reference/models/latest/assessment-results/json-index/#/id)|

<br>

#### **POA&M Identifiers**
Identifiers defined in a POA&M are only referenced locally ([see the diagram in the Scope section](#scope)). The table below provides a listing of the core OSCAL POA&M model identifiers.

|**Defining Model**|**Identifier Type**|**Identifiers**|
|:------|:-------|:-----:|
|POA&M|Machine-Oriented|[XML Index](https://pages.nist.gov/OSCAL-Reference/models/latest/plan-of-action-and-milestones/xml-index/#/@uuid) &#124; [JSON Index](https://pages.nist.gov/OSCAL-Reference/models/latest/plan-of-action-and-milestones/json-index/#/uuid)|
|POA&M|Human-Oriented|[XML Index](https://pages.nist.gov/OSCAL-Reference/models/latest/plan-of-action-and-milestones/xml-index/#/@id) &#124; [JSON Index](https://pages.nist.gov/OSCAL-Reference/models/latest/plan-of-action-and-milestones/json-index/#/id)|

<br>

---

### Consistency
Identifier (value) must be managed across revisions of the same document.  In general, [OSCAL identifiers](/concepts/layer/overview/#identifier-use) have *per-subject* consistency.  They should only be changed if the underlying identified subject has changed in a significant way that no longer represents the same identified subject.

<br>
