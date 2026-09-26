# Contributing Guidelines

We welcome contributions to the **Developer Intelligence Platform**! Please follow these engineering guidelines to maintain codebase quality.

## Development Setup

1. Fork and clone the repository.
2. Install dependencies:
   ```bash
   npm install
   ```
3. Set up local database:
   ```bash
   npx prisma db push
   npx tsx prisma/seed.ts
   ```
4. Verify tests pass:
   ```bash
   npx vitest run
   ```

## Code Quality Standards
- **Strict TypeScript:** Do not use `any` unless strictly required for external dynamic payloads.
- **Modularity:** Keep UI components, analysis engines, and security validators cleanly separated under `components/` and `lib/`.
- **Testing:** New analysis rules or security validation logic must include accompanying unit tests in `*.test.ts`.
- **No Hallucinated Claims:** Ensure all intelligence and analysis features display factual data without marketing embellishments.

## Commit Conventions
Follow Conventional Commits:
- `feat:` New features
- `fix:` Bug fixes
- `test:` Adding or refactoring tests
- `docs:` Documentation updates
- `refactor:` Code improvements without behavioral changes
