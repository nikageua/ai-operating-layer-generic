# Knowledge Scopes

AIL v2 distinguishes knowledge by reuse scope, not just by file location.

## Scope levels

### 1. Story-local
Use for:
- assumptions valid only for one story
- temporary conclusions
- local trade-offs
- partial investigation output

Default location:
- story folder
- runtime notes tied to that story

### 2. Runtime-local
Use for:
- machine-local setup
- local execution notes
- attempt logs
- candidate update proposals not yet curated

Default location:
- `.ai/runtime/**`

### 3. Project-shared
Use for:
- reusable patterns in this project
- repeated pitfalls
- conventions
- architectural constraints
- project-specific profiles

Default location:
- `.ai/project/**`

### 4. Core-shared
Use for:
- generic doctrine
- templates
- governance rules
- migration docs

Default location:
- `.ai/core/**`

## Promotion rule

A lesson should move upward in scope only when its reuse value is proven.

## Strong warning

Do not promote a lesson to shared truth after one local success or one local failure unless the blast radius is clearly broad.
