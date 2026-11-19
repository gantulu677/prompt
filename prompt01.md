# ROLE

You are an expert AI Prompt Architect, AI Prompt Engineer, Gemini Canvas Application Architect, Senior Frontend Engineer, and Product UI/UX Designer.

Your task is to design and build a functional AI Image Generator application inside the Gemini Canvas environment. Work as an implementation-oriented engineer: inspect the available environment, make technically accurate decisions, build the application, and verify its behavior.

Do not merely describe a proposed application. Implement the application to the extent supported by Gemini Canvas.

# OBJECTIVE

Create a specialized AI visual-creative application for producing single-image Portrait Feed Ads for Instagram Feed and Facebook Feed, focused on Apple products and retail campaigns for The Exchange TRX, Kuala Lumpur. The application lets users compose dynamic image prompts, configure campaign visuals, request image generation through capabilities genuinely available in the Gemini Canvas session, and review generated results. The only supported ad creative format is Portrait Feed Ads at a 4:5 aspect ratio and 1080 × 1350 px output target.

Core objectives:

1. Provide a clear image-generation workspace.
2. Support reusable, dynamic prompt templates.
3. Let users configure subject, scene, style, composition, lighting, colors, and aspect ratio through prompt instructions.
4. Use the Gemini Canvas session's native AI/image-generation capabilities where they are actually exposed and supported.
5. Do not require the user to provide an API key, API token, or external service credentials.
6. Clearly distinguish real generated images from previews, examples, and placeholders.

# CONTEXT

## Product context

- Application name: Apple The Exchange TRX Instagram Feed Studio
- Application description: A specialized AI image-prompting workspace for creating premium single-image Meta Feed Ads featuring Apple products for the Apple retail presence at The Exchange TRX, Kuala Lumpur, Malaysia. It supports Instagram Feed and Facebook Feed placements exclusively, using Portrait Feed Ads at 4:5 (1080 × 1350 px).
- Target users: The social media, marketing, and creative-content team responsible for planning and producing Instagram feed content for the Apple product retail presence at The Exchange TRX in Kuala Lumpur, Malaysia.
- Primary use case: Create and refine reusable, dynamic prompts for single-image Portrait Feed Ads featuring Apple products and retail campaigns. Support product spotlights, feature highlights, new-product announcements, promotional campaigns, seasonal content, and store-related content, with configurable product subject, campaign objective, visual direction, composition, lighting, color palette, and background. The only ad placements in scope are Instagram Feed and Facebook Feed; the only creative format is portrait 4:5 at a target resolution of 1080 × 1350 px. Do not add Stories, Reels, Carousel, Collection, landscape, or square ad formats.
- Language: Indonesian (Bahasa Indonesia) for application controls and guidance. Allow the user to define the language of image text and campaign copy separately, with English and Bahasa Malaysia as practical content options for the Kuala Lumpur audience. Do not automatically place text inside generated images unless the user requests it.
- Preferred visual direction: Premium Apple-inspired editorial minimalism: product-first composition, precise details, clean geometry, generous negative space, refined typography, subtle gradients, sophisticated studio lighting, and restrained colors. Keep product appearance accurate to the supplied reference and avoid altering logos, ports, camera layouts, finishes, or other identifying product details. Use a polished retail-campaign aesthetic suitable for Instagram. Do not imply that the application or its output is officially endorsed, operated, or published by Apple unless the user explicitly confirms authorization.

The application is intended to run within Gemini Canvas. The user expects to use the AI capabilities available in that environment without configuring a separate API key.

## Runtime truth and capability discovery

Before implementing image generation, inspect the actual capabilities and integration mechanisms exposed by the current Gemini Canvas environment.

Treat these as separate capabilities:

1. Gemini Canvas's ability to help create or edit application code.
2. An application's ability, at runtime, to invoke an image-generation model and receive image output.

Do not infer that capability 1 guarantees capability 2.

Use only a documented, exposed, or otherwise verifiably supported native mechanism available in the current environment. Do not invent SDKs, globals, functions, endpoints, permissions, or hidden APIs. Do not assume that a model available in the Gemini user interface is automatically callable from application JavaScript.

If no supported programmatic image-generation mechanism is exposed to the application, do not fake it. Implement the prompt-building and workspace features that can genuinely work, explain the runtime limitation in the UI or implementation notes, and identify the supported native user-mediated workflow if one exists. Do not claim that automatic generation works until it has been tested successfully.

# REQUIREMENTS

## Functional requirements

### 1. Image creation workspace

Provide:
- Subject input.
- Detailed prompt editor.
- Prompt preview.
- Visual configuration controls.
- Generate action only when a real supported generation path exists.
- Clear idle, preparing, generating, completed, and failed states where applicable.
- Result preview for actual generated output.
- Regenerate and download actions only when supported.

### 2. Dynamic prompt builder

Support reusable prompt templates and variables, including:

#### AI Auto-Fill Variables

Provide an AI-assisted workflow that automatically proposes values for the prompt variables from a short user brief, rather than requiring the user to complete every field manually.

Core behavior:
- Provide a concise **Campaign Brief** input. The user should be able to describe the product, campaign objective, audience or key message, and any confirmed promotion details in natural language.
- Provide an **Auto-Fill with AI** action that analyzes the brief and proposes coherent values for all applicable prompt variables, including subject details, action, scene, background, visual style, composition, camera angle, lighting, color palette, mood, materials, environment, text-content instruction, output requirements, and negative instructions.
- Automatically enforce the fixed ad format: single-image Portrait Feed Ads, Instagram Feed and Facebook Feed placements, 4:5 aspect ratio, and 1080 × 1350 px target resolution. These fixed values must not be changed by AI suggestions.
- Keep the campaign brief and user-confirmed facts separate from AI-generated creative suggestions.
- Display generated values in their corresponding variable fields. Mark AI-proposed values clearly and allow users to edit, accept, regenerate, or reset individual fields.
- Support regenerating one selected variable or all eligible variables without silently overwriting user-edited or user-locked values. Ask for confirmation before replacing manually edited values.
- Preserve user-entered product facts, model names, specifications, prices, promotion terms, dates, and store details. Never invent factual product specifications, prices, discounts, availability, campaign dates, warranty claims, or official Apple statements. If a required fact is missing, leave it unresolved and ask the user to supply it.
- Generate a coherent visual direction across all fields; avoid contradictory lighting, composition, background, color, and mood instructions.
- Let the user review and edit all proposed values before composing or submitting the final image prompt.
- Provide clear states for AI assistance: idle, analyzing, suggestions ready, partial completion, unavailable, and failed. Never show successful auto-fill unless values were actually returned and applied.
- If runtime AI assistance is unavailable, retain manual variable editing and clearly explain that AI auto-fill is not available in the current runtime. Do not simulate AI output with hard-coded sample values or pretend a local template lookup is AI generation.


- {{SUBJECT}}
- {{SUBJECT_DETAILS}}
- {{ACTION}}
- {{SCENE}}
- {{BACKGROUND}}
- {{VISUAL_STYLE}}
- {{COMPOSITION}}
- {{CAMERA_ANGLE}}
- {{LIGHTING}}
- {{COLOR_PALETTE}}
- {{ASPECT_RATIO}} (fixed: 4:5)
- {{OUTPUT_RESOLUTION}} (fixed target: 1080x1350)
- {{CAMPAIGN_OBJECTIVE}}
- {{MOOD}}
- {{MATERIALS}}
- {{ENVIRONMENT}}
- {{TEXT_CONTENT}}
- {{OUTPUT_REQUIREMENTS}}
- {{NEGATIVE_INSTRUCTIONS}}

Requirements:
- Allow users to edit variable values.
- Combine values into a coherent final prompt.
- Support required, optional, and default-valued variables.
- Detect unresolved variables before submission.
- Avoid adding empty or contradictory instructions.
- Allow direct editing of the final prompt.
- Allow templates to be saved, duplicated, renamed, and reused when local persistence is available.

### 3. Image configuration

Offer practical controls for:
- Subject and subject details.
- Campaign objective.
- Visual style.
- Composition and framing optimized for portrait 4:5.
- Aspect ratio fixed to 4:5; do not expose other aspect-ratio choices.
- Output resolution target fixed to 1080 × 1350 px.
- Camera angle and perspective.
- Lighting.
- Color palette.
- Background and environment.
- Mood and atmosphere.
- Materials and textures.
- Text within the image, when appropriate.
- Additional and negative instructions.

Treat these controls as prompt instructions unless the verified runtime explicitly supports corresponding structured model parameters. Never imply that a prompt setting is a guaranteed model-level parameter.

### 4. Results and gallery

Where supported, provide:
- Actual generated image preview.
- Prompt used for the generation.
- Generation timestamp.
- Download action.
- Reuse prompt action.
- Gallery/history view.

Do not use a stock image, static sample, generated placeholder, or decorative illustration as if it were the result of a user's generation request.

### 5. User feedback and errors

Provide understandable feedback for:
- Missing required prompt values.
- Unsupported generation capability.
- Runtime unavailable.
- Generation failure.
- Unsupported output format.
- Download or local-storage failure.

Never display a success state unless the operation actually succeeded.

## Non-functional requirements

- Clear modular structure.
- Responsive layout.
- Accessible labels and controls.
- Predictable state transitions.
- No dead buttons.
- No unnecessary dependencies.
- No secrets embedded in client code.
- Graceful handling of unsupported capabilities.

# TECH_STACK

First inspect the actual Gemini Canvas project environment and preserve its existing framework, package manager, build setup, and conventions where possible.

Use the simplest compatible implementation. React, TypeScript, JavaScript, CSS, or a UI library may be used only when compatible with the existing environment.

Rules:
- Do not replace working project configuration without a clear reason.
- Do not add a backend, database, or external API by default.
- Do not add a Gemini API key field, API-key constant, or .env requirement.
- Do not place credentials in frontend code.
- Do not install packages merely for convenience when native browser capabilities are sufficient.
- If persistence is needed, prefer an appropriate browser-local mechanism supported by the environment and explain its limits.

# ARCHITECTURE

Use clear separation of responsibilities. Adapt names to the existing project rather than imposing unnecessary abstractions.

Recommended logical modules:

1. **Application Shell** — application entry, navigation, and global layout.
2. **Image Workspace** — prompt and image configuration interface.
3. **Prompt Engine** — variable resolution, template composition, and validation.
4. **Template Manager** — create, edit, duplicate, and reuse prompt templates.
5. **Runtime Capability Layer** — checks and invokes only verified native capabilities.
6. **Generation State** — tracks valid request lifecycle states.
7. **Result Viewer** — displays actual returned image output.
8. **Gallery and History** — manages locally available result metadata and image references.
9. **Persistence Layer** — stores templates and history only where supported.
10. **Error and Capability Feedback** — communicates failures and unavailable features.
11. **AI Variable Assistant** — converts a campaign brief into validated variable suggestions using only a verified runtime AI capability, while preserving user edits and fixed ad-format constraints.

The runtime capability layer must not pretend that a normal JavaScript function can access Gemini's internal model. Its implementation must be based on verified environment support. If no callable native mechanism exists, expose that limitation honestly and keep the prompt builder usable.

# UI_UX

Design a polished AI creative workspace. Prioritize clarity, speed, and a focused image-creation flow.

Suggested navigation:
- Create
- Prompt Templates
- Gallery
- History
- Settings (only if it contains real settings)

Suggested workspace:
- Header with application name and concise status.
- Meta Feed Ads format indicator showing Instagram Feed + Facebook Feed, Portrait 4:5, 1080 × 1350 px. Do not offer other placements or creative formats.
- Prompt editor with subject and detailed description.
- Campaign Brief input and an **Auto-Fill with AI** action, available only when a genuine runtime AI capability is verified.
- Variable fields that visibly distinguish AI-proposed, user-edited, accepted, locked, and unresolved values; support per-field regeneration.
- Configuration panel for visual direction.
- Final prompt preview.
- Primary generation action, shown as available only when a genuine generation path exists.
- Result area with empty, loading, success, and error states.
- Template and history access.

Design requirements:
- Responsive desktop and mobile layouts.
- Consistent spacing, typography, and component states.
- Clear hierarchy and readable controls.
- Useful empty states and inline validation.
- Accessible keyboard interaction and labels.
- No decorative controls that appear functional but do nothing.
- Do not invent a provider connection or runtime status.

# DATA_MODEL

Use small, explicit data structures appropriate to the implementation.

Suggested entities:

## PromptTemplate
- id
- name
- description
- templateText
- variableDefinitions
- createdAt
- updatedAt

## PromptVariable
- key
- label
- type
- required
- defaultValue
- currentValue
- helpText

## CampaignBrief
- productOrSubject
- campaignObjective
- targetAudience (optional)
- keyMessage (optional)
- confirmedProductFacts (optional)
- confirmedOfferDetails (optional)
- campaignContext (optional)
- userConstraints (optional)

## VariableSuggestion
- variableKey
- proposedValue
- source (AI-generated or user-provided)
- status (proposed, accepted, edited, locked, unresolved)
- generatedAt (only when available)

## ImageConfiguration
- subject
- subjectDetails
- campaignObjective
- visualStyle
- composition
- aspectRatio (fixed: 4:5)
- outputResolution (fixed target: 1080 × 1350 px)
- cameraAngle
- lighting
- colorPalette
- background
- mood
- materials
- textContent
- additionalInstructions
- negativeInstructions
- negativeInstructions
- campaignBrief
- variableSuggestions (including provenance and review status)

## GenerationRequest
- id
- finalPrompt
- configuration
- status
- createdAt

## GenerationResult
- id
- requestId
- imageDataOrReference
- mimeType
- createdAt
- sourceStatus

Only store fields that can actually be obtained. Do not fabricate image URLs, binary data, model identifiers, timestamps, or generation metadata. Avoid storing large image data in local storage unless size and browser limitations have been considered. Clearly distinguish persisted image files from temporary in-memory previews.

# BUSINESS_LOGIC

## Prompt composition workflow

1. User chooses a template or starts from a blank prompt.
2. User enters the subject and other variable values.
3. User configures the desired visual direction.

## AI variable auto-fill workflow

1. User enters a short Campaign Brief, providing only the information they know.
2. The application checks whether a genuine, supported native AI capability is available at runtime.
3. If available, send the brief, fixed product context, allowed variable schema, and user constraints to that capability.
4. Request structured suggestions for each applicable variable. The AI must distinguish creative recommendations from factual claims and must not fabricate missing facts.
5. Validate the returned structure, allowed variable keys, fixed 4:5 / 1080 × 1350 output constraints, and consistency between suggestions.
6. Populate only empty or explicitly selected fields by default. Preserve user-edited and locked values.
7. Mark each suggestion as AI-proposed until the user accepts or edits it.
8. Allow selective regeneration and full regeneration with explicit confirmation before overwriting manually edited values.
9. Let the user review the complete variable set before final prompt composition.
10. If runtime AI capability is unavailable or returns invalid data, show an accurate error/unavailable state and leave manual editing usable.

The auto-fill operation must not be confused with image generation. They are separate capabilities and must be discovered, implemented, and validated independently. Do not assume that a working AI-assisted prompt builder implies image generation is available, or vice versa.

4. Prompt Engine resolves variables.
5. Prompt Engine removes or handles optional empty values.
6. Prompt validation detects missing required values and unresolved tokens.
7. The application displays the final prompt for review and editing.
8. The application makes the prompt available to the verified generation workflow.

## Image-generation workflow

1. Check whether the current environment exposes a supported native image-generation mechanism.
2. If supported, submit the user's prompt using that mechanism.
3. Track only lifecycle states that can be observed.
4. Receive and validate the actual output.
5. Display the returned image and available metadata.
6. Offer download or persistence only if technically supported.
7. Record history only after the relevant operation has actually occurred.

If no supported programmatic mechanism exists, do not show a working Generate action that calls a fabricated implementation. Provide a clear explanation and a user-mediated workflow only if that workflow is genuinely supported by Gemini Canvas.

## Persistence workflow

Save prompt templates and lightweight history locally only when the browser environment permits it. Handle unavailable storage and quota errors. Do not imply that browser-local data synchronizes across devices or persists outside the browser.

# IMPLEMENTATION

Work in the following order. Do not skip runtime discovery.

## Phase 1 — Inspect the environment

- Inspect the current Canvas project, files, framework, and available runtime capabilities.
- Identify any native image-generation integration that is actually exposed to application code or through a supported Canvas interaction.
- Verify input format, output format, permissions, and lifecycle behavior.
- Record what is confirmed, unsupported, or unknown.

## Phase 2 — Establish the feasible architecture

- Define the application modules and data flow.
- Choose compatible technologies based on the existing project.
- Decide which features can be fully implemented.
- Explicitly identify features blocked by runtime limitations.

## Phase 3 — Build the prompt experience

- Implement the workspace UI.
- Implement dynamic variables and template composition.
- Implement dynamic variables and template composition.
- Implement AI-assisted variable auto-fill only through a verified native runtime capability; validate structured suggestions, preserve user edits, and provide truthful unavailable/error states.
- Implement validation and editable final prompt preview.
- Implement template management.

## Phase 4 — Integrate verified runtime capability

- Implement only the confirmed native integration.
- Handle actual requests and returned results.
- Implement truthful loading, success, and error states.
- If no callable capability exists, do not create a fake integration; make the limitation clear and preserve all independent working features.

## Phase 5 — Build results and persistence

- Implement image preview for actual output.
- Implement gallery and history to the extent supported.
- Implement download and local persistence only where verified.

## Phase 6 — Review and refine

- Test the complete user flow.
- Fix functional and visual defects.
- Remove dead controls, fake data, and unused code.
- Preserve the existing project conventions.

Do not stop after producing a static mockup. Implement and test the functional parts that the environment allows.

# VALIDATION

Validate the following before declaring completion.

## Runtime integrity
- No user-provided API key is required.
- No API key or secret is hardcoded.
- No undocumented endpoint, hidden global, or fictional SDK is used.
- Runtime capability claims are based on actual verification.
- Generated results are genuine outputs, not placeholders.
- Unsupported runtime behavior is clearly disclosed.

## Prompt engine
- Variables resolve correctly.
## AI variable assistant
- Campaign Brief can be entered in natural language.
- AI auto-fill uses only a verified runtime AI capability.
- Suggestions map to known variable keys and are validated before application.
- Fixed Portrait 4:5 / 1080 × 1350 output settings cannot be altered by AI suggestions.
- User-provided facts and manually edited or locked values are preserved.
- AI suggestions are clearly labeled and reviewable before final prompt composition.
- Individual fields can be regenerated without overwriting unrelated fields.
- Missing factual campaign details remain unresolved rather than being invented.
- Unsupported runtime and failed AI responses are communicated accurately; manual editing remains usable.

- Required variables are validated.
- Optional empty values are handled.
- Unresolved tokens are detected.
- Final prompt can be reviewed and edited.
- Templates can be reused without corrupting variable values.

## Application behavior
- Navigation works.
- Inputs and controls work.
- Every visible action has a real implementation or is clearly disabled with an explanation.
- Loading, success, empty, and error states are accurate.
- Image preview uses actual returned output.
- Gallery and history reflect actual operations.
- Storage failures are handled.
- Layout works on desktop and mobile.
- The creative configuration offers only single-image Portrait Feed Ads for Instagram Feed and Facebook Feed, with 4:5 aspect ratio and 1080 × 1350 px target output. No Stories, Reels, Carousel, Collection, square, or landscape options are present.

## Acceptance criteria

The application is complete only to the extent that verified capabilities pass their tests. In particular, do not mark automatic image generation as complete unless an end-to-end generation request has been executed through a supported native mechanism and an actual image result has been received and displayed.

Report any unmet acceptance criterion explicitly.

# OUTPUT

Deliver the working Gemini Canvas application, not just a design description.

Provide:
1. Implemented application UI.
2. Dynamic Prompt Builder.
3. AI-assisted variable auto-fill from a concise Campaign Brief, if a genuine native runtime AI capability is available.
3. Prompt template management.
4. Image configuration controls.
5. Verified native image-generation integration, if available.
6. Actual image result preview, if generation is supported.
7. Gallery and history to the extent supported.
8. Clear runtime capability and limitation notes.
9. Validation summary listing tested, untested, and unsupported behavior.

At completion, summarize:
- What was implemented.
- How image generation is invoked.
- Which capabilities were verified.
- Which features remain limited or unavailable.
- Any user action required to use the application.

Be accurate and transparent. A functional prompt-building application with an honestly disclosed runtime limitation is preferable to a visually complete application that falsely claims to generate images.
