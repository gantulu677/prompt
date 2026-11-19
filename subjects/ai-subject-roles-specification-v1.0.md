# AI Subject Roles Specification V1.0

**Status:** Baseline specification  
**Product context:** Apple Malaysia Instagram Content Generator  
**Architecture:** Modular Multi-Agent  
**Execution model:** Team-based, coordinated by an AI Orchestrator  
**Output contract:** Structured JSON  
**Default design format:** Instagram portrait, 4:5 (1080 × 1350 px)  
**Approval model:** AI validation followed by human approval

> Governance note: Configuring an account as official does not establish or imply authorization from Apple. Product claims, specifications, prices, offers, logos, Trade In, warranty, and service information must be verified against authoritative Malaysia sources and applicable brand permissions.

## 1. Purpose

Define seven specialist AI roles that generate the core fields of a visual content brief: Subject, Headline, Subheadline, Feature Items, Composition, Background, and Style.

Each role owns one output domain, has explicit dependencies, and returns machine-readable JSON. The AI Orchestrator coordinates execution, resolves dependencies, combines outputs, and runs cross-field validation.

## 2. Architecture

### 2.1 Specialist roles

| Subject Code | Subject | Specialist AI Role | Responsibility |
|---|---|---|---|
| SUB001 | Subject | AI Subject Strategist | Define the hero subject, concept, context, and key message |
| SUB002 | Headline | AI Headline Copywriter | Write a concise headline derived from the approved subject |
| SUB003 | Subheadline | AI Subheadline Copywriter | Write supporting copy that expands the headline without repeating it |
| SUB004 | Feature Items | AI Feature Content Strategist | Select and express relevant features or benefits |
| SUB005 | Composition | AI Composition Director | Define layout, placement, hierarchy, perspective, and spacing |
| SUB006 | Background | AI Background Designer | Define background color, texture, lighting environment, and atmosphere |
| SUB007 | Style | AI Visual Style Director | Define visual language, rendering, lighting treatment, and finish |

### 2.2 AI Orchestrator

The AI Content Orchestrator coordinates the seven specialist roles. It must:
- Receive and normalize the user request.
- Resolve account, market, language, product, campaign, and format context.
- Execute SUB001 first.
- Dispatch dependent roles only after their required inputs are available.
- Validate role outputs against their contracts.
- Detect conflicts, unsupported product claims, and inconsistent creative direction.
- Assemble the final design brief and image-generation prompt.
- Route the result for human approval.

The Orchestrator must not invent product facts or treat generated copy as verified evidence.

## 3. Specialist role specifications

### 3.1 SUB001 — AI Subject Strategist

**Mission:** Determine the primary subject and creative concept that the visual should communicate.

**Responsibilities:**
- Identify the primary subject, product, or object.
- Define subject category and intended context.
- Establish creative angle and key message.
- Define the hero-subject visual direction.
- Align the subject with campaign objective and audience.
- Identify factual information requiring source verification.

**Inputs:** User brief, product or subject context, campaign objective, target audience, market, language, and available verified product information.

**Output contract:**
~~~json
{
  "subject": {
    "name": "iPhone",
    "category": "Product",
    "concept": "Premium smartphone experience",
    "visual_direction": "Hero product showcase",
    "key_message": "Experience more with iPhone",
    "fact_check_required": true
  }
}
~~~

**Validation:** Subject name must be non-empty; identify one primary hero subject unless a group is requested; concept and key message must relate to the subject; do not invent models, specifications, features, prices, or availability.

### 3.2 SUB002 — AI Headline Copywriter

**Mission:** Create a memorable headline derived directly from the approved subject and key message.

**Responsibilities:** Understand the subject and campaign; generate concise high-impact copy; match tone and language; avoid unsupported superlatives or claims; keep the headline connected to the subject.

**Dependency:** SUB001.

**Output contract:**
~~~json
{
  "headline": {
    "text": "BEYOND THE ORDINARY",
    "tone": "Premium",
    "purpose": "Brand awareness",
    "alignment": "Subject"
  }
}
~~~

**Validation:** Headline must be non-empty, concise, traceable to the approved subject, and free of unsupported performance, superiority, or availability claims.

### 3.3 SUB003 — AI Subheadline Copywriter

**Mission:** Create supporting copy that clarifies or expands the headline.

**Responsibilities:** Explain relevant subject value or context; complement rather than repeat the headline; keep copy readable at mobile poster size; maintain campaign consistency; avoid unsupported factual claims.

**Dependencies:** SUB001 and SUB002.

**Output contract:**
~~~json
{
  "subheadline": {
    "text": "Discover a more powerful way to create, connect and experience.",
    "tone": "Premium",
    "purpose": "Supporting message"
  }
}
~~~

**Validation:** Subheadline must support the headline and subject, not merely restate the headline, and remain short enough for the selected layout. Claims must be supported or flagged.

### 3.4 SUB004 — AI Feature Content Strategist

**Mission:** Select the most relevant features, benefits, or content points associated with the subject.

**Responsibilities:** Identify candidate features from supplied or verified information; prioritize by campaign objective; translate technical information into clear copy; distinguish features from benefits; avoid duplicates; attach evidence or verification status to factual claims.

**Dependencies:** SUB001. Verified product data is required for factual product specifications.

**Output contract:**
~~~json
{
  "feature_items": [
    {
      "title": "Camera",
      "description": "Capture memorable moments",
      "claim_type": "Benefit",
      "verification_status": "Needs review"
    },
    {
      "title": "Performance",
      "description": "Power your everyday tasks",
      "claim_type": "Benefit",
      "verification_status": "Needs review"
    },
    {
      "title": "Ecosystem",
      "description": "Connect your Apple devices",
      "claim_type": "Experience",
      "verification_status": "Needs review"
    }
  ]
}
~~~

**Validation:** Every item must relate to the subject; no fabricated specifications; no duplicate items; use a configurable item limit based on the design preset; mark unverified factual statements for review.

### 3.5 SUB005 — AI Composition Director

**Mission:** Define the spatial arrangement and visual hierarchy of all design elements.

**Responsibilities:** Position the hero subject; place headline, subheadline, and feature items; define hierarchy and reading order; specify camera angle, perspective, scale, and negative space; maintain legibility; respect canvas and safe areas.

**Dependencies:** SUB001, SUB002, SUB003, and SUB004.

**Output contract:**
~~~json
{
  "composition": {
    "layout": "Hero centered",
    "subject_position": "Center",
    "headline_position": "Top",
    "subheadline_position": "Below headline",
    "feature_items_position": "Bottom",
    "camera_angle": "Three-quarter view",
    "visual_hierarchy": [
      "Headline",
      "Hero subject",
      "Subheadline",
      "Feature items"
    ],
    "canvas": {
      "aspect_ratio": "4:5",
      "width": 1080,
      "height": 1350
    }
  }
}
~~~

**Validation:** Required elements must have a placement or explicit omission; layout must fit the canvas; text must remain readable on mobile; avoid collisions and clipping; composition must reinforce the subject.

### 3.6 SUB006 — AI Background Designer

**Mission:** Define a background environment that supports the subject and composition without competing with them.

**Responsibilities:** Select background type and base color; define gradients, texture, and material; specify lighting and atmosphere; create separation and depth; preserve text contrast; follow the selected design preset.

**Dependencies:** SUB001 and SUB005.

**Output contract:**
~~~json
{
  "background": {
    "type": "Clean white premium",
    "base_color": "White",
    "texture": "Subtle gradient",
    "lighting": "Soft studio lighting",
    "atmosphere": "Minimal and elegant",
    "depth": "Subtle depth"
  }
}
~~~

**Validation:** Background must support subject visibility, preserve text contrast, avoid excessive decoration, remain consistent with composition and style, and introduce no unrelated objects or brand marks.

### 3.7 SUB007 — AI Visual Style Director

**Mission:** Establish the overall visual language and finishing direction.

**Responsibilities:** Define visual style and design language; specify realism and rendering; define lighting and color treatment; specify material appearance and finishing; maintain consistency; respect applicable brand guidelines and asset permissions.

**Dependencies:** SUB001, SUB005, and SUB006.

**Output contract:**
~~~json
{
  "style": {
    "visual_style": "Premium minimalist technology",
    "design_language": "Modern editorial",
    "render_quality": "Photorealistic",
    "lighting": "Dramatic rim lighting",
    "color_treatment": "Clean neutral tones",
    "finishing": "High-end commercial"
  }
}
~~~

**Validation:** Style must match subject and campaign, must not conflict with composition or background, must not imply official brand approval, and must maintain coherent visual treatment.

## 4. Dependency matrix

| Subject | Required dependencies |
|---|---|
| SUB001 Subject | User brief and available context |
| SUB002 Headline | SUB001 |
| SUB003 Subheadline | SUB001, SUB002 |
| SUB004 Feature Items | SUB001 and verified product data where applicable |
| SUB005 Composition | SUB001, SUB002, SUB003, SUB004 |
| SUB006 Background | SUB001, SUB005 |
| SUB007 Style | SUB001, SUB005, SUB006 |

## 5. Recommended execution sequence

1. Normalize request and context.
2. Execute SUB001 and validate the subject.
3. Execute SUB002, SUB003, and SUB004 after the subject is approved.
4. Execute SUB005 after copy and feature content are available.
5. Execute SUB006 and SUB007 using the approved subject and composition.
6. Run cross-role consistency and factual-claim validation.
7. Assemble the final design brief and image-generation prompt.
8. Request human approval before publishing or treating claims as approved.

Roles may run in parallel only when their dependencies are satisfied.

## 6. Cross-role quality gates

The Orchestrator must verify:
- **Subject alignment:** Every field supports the same primary subject and key message.
- **Copy alignment:** Headline, subheadline, and feature items are complementary.
- **Factual integrity:** Product facts are sourced or flagged; specifications are never fabricated.
- **Layout integrity:** Elements fit the canvas and remain legible.
- **Visual consistency:** Composition, background, and style reinforce one another.
- **Brand governance:** No unsupported implication of Apple authorization or approval.
- **Output validity:** Every specialist response conforms to its JSON contract.

If a gate fails, request a targeted revision from the responsible role rather than regenerating all fields unnecessarily.

## 7. Shared context contract

Each specialist receives only the shared context and dependency outputs required for its task.

~~~json
{
  "project": {
    "name": "Apple Malaysia Instagram Content Generator",
    "market": "Malaysia",
    "language": "English",
    "platform": "Instagram"
  },
  "design": {
    "aspect_ratio": "4:5",
    "width": 1080,
    "height": 1350
  },
  "campaign": {
    "objective": null,
    "target_audience": null,
    "tone": "Premium"
  },
  "subject_context": {
    "product_id": null,
    "verified_product_data": [],
    "source_references": []
  }
}
~~~

Null values mean information was not supplied. Specialist roles must not replace them with invented facts.

## 8. Database mapping

Recommended **ai_subjects** fields:

| Field | Type | Purpose |
|---|---|---|
| id | UUID | Primary key |
| subject_code | TEXT UNIQUE | Stable code such as SUB001 |
| subject_name | TEXT | Subject field name |
| role_name | TEXT | Specialist role name |
| role_description | TEXT | Role purpose and responsibility |
| system_instruction | TEXT | Role-specific system prompt |
| input_schema | JSONB | Input contract |
| output_schema | JSONB | Output contract |
| dependencies | JSONB | Required upstream subjects |
| validation_rules | JSONB | Role-level quality rules |
| model_config | JSONB | Model and generation settings |
| status | BOOLEAN | Enabled/disabled |
| version | TEXT | Specification version |

Recommended supporting entities: **ai_workflows**, **ai_workflow_steps**, **ai_prompt_templates**, and **ai_execution_logs**. The seven subject records should be linked to an orchestrated workflow rather than treated as unrelated prompts.

## 9. Versioning and scope

- This document defines role boundaries and baseline contracts only.
- Full production system prompts and formal JSON Schema files are separate implementation artifacts.
- Model selection, temperature, token limits, retries, and provider-specific settings belong in model_config and are not fixed here.
- This specification does not itself implement database tables, runtime orchestration, image generation, or publishing.
- Changes to role ownership, dependencies, or output contracts require a version update.

**End of AI Subject Roles Specification V1.0**
