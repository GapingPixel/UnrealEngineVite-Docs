# Engine Coding Guidelines

## Core Principles
### Stability first.
Code must remain predictable and safe under both MSVC and Clang.
### Performance-focused.
All changes must consider CPU, GPU, and memory impact, with ARM-class ~1 GHz CPU as a baseline target. Performance measured on a local desktop CPU must not be treated as sufficient or representative of real-world target hardware.
### Strict Clang 16+ compliance.
No MSVC-specific behavior, compiler extensions, or undefined constructs.
### Licensing clarity.
All contributions must be copyright-clean.
Code may be included only if it is:
- Original work by the contributor or
- Licensed under permissive licenses (e.g. MIT, Apache 2.0, BSD, Zlib)
### ABI safety.
Do not modify engine bitmask layouts, payload structures, serialization formats, or any CPU/GPU-shared binary contracts.

## Forbidden Usage
1. Recursion
- Recursion is banned; use iterative patterns.
2. No virtual functions 
- Do not add new virtuals unless strictly required.
3. Kismet/Blueprint API additions
- No new BlueprintCallable or BlueprintPure functions unless explicitly approved.
4. Template usage avoidance
- Avoid templates unless they provide a clear performance or architectural benefit.
- Do not introduce template-heavy patterns that increase compile times, binary size, or code complexity.
5. ABI-breaking modifications
Do NOT modify:
- Ray tracing payload bitfields
- Shader-visible enums or flags
- Packed bitmasks used by RHI or RenderCore
- Reflection system bitmask definitions
- Any CPU/GPU shared struct layouts

Such modifications break PSO caching, ray tracing stability, serialization, and cross-platform/vendor GPU behavior.

## Commit Naming
Use the following Prefixes:

[Optimization] </br>
[Rendering Feature] </br>
[VR] </br>
[Mobile] </br>
[Plugin] </br>
[Fix] </br>

When making backports or adding a plugin, include the correct links to original commits/repos.

Technical Standards
1. No undefined behavior or non-standard extensions.
2. Avoid implicit type conversions.
3. Maintain memory correctness: avoid large stack allocations, minimize dynamic memory
4. Prefer constexpr, FORCEINLINE, and zero-cost abstractions.

Performance Rules
1. Favor contiguous memory and cache-friendly layouts.
2. Avoid unpredictable branching in hot paths.
3. No FString processing, reflection calls, dynamic allocation, or virtual dispatch inside per-frame loops.
4. Use SIMD-friendly math (SSE/AVX/NEON) when appropriate.

WIP work/Branches
1. Commit to alternative branches to pass WIP work
2. Give a brief commentary on what’s left to be done
3. Delete unnecessary temporal branches
4. Make other forkers aware of the WIP work

Verification Requirements
1. Compilation
- Must compile cleanly under MSVC and be Clang compliant.
2. Stability
- No crashes on startup, shutdown, or on the Tech Showcase project.
- No log spam.
- Guard all code not necessary for shipping
3. ABI
- All shader-visible structs must remain bit-for-bit identical.
- No changes to payloads, bitmask layouts, uniform buffers, or reflection flags.
- ABI violations result in immediate rejection.

Review Checklist
Before PR, one must confirm:
- No recursion
- No added virtual calls (and cache existing engine virtuals where possible)
- No new Kismet exposure
- Copyright-free code
- ABI and bitmask integrity preserved
- Strict Clang compliance
- No undefined behavior
- No performance regressions
- No unnecessary binary size increases
- No shader or RHI ABI mismatches
