# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a warmup repository for the 10xDevs.pl training program focused on AI-assisted development. The project implements a banking system to practice test-driven development, specification-driven implementation, and AI collaboration workflows.

## Development Commands

### Setup
```bash
npm install
```

### Testing
```bash
# Run all tests
npm test

# Run tests in watch mode (recommended during development)
npx vitest --watch

# Run a single test file
npx vitest banking/banking.test.ts
```

Note: The test runner is Vitest 3.0.9, which auto-discovers `*.test.ts` files.

## Code Architecture

### Module Structure

The codebase follows a domain-driven design pattern centered around the `banking/` module:

- **banking/banking.ts** - Core domain logic implementing business operations
  - `createAccount()` - Account creation with validation
  - `processWithdrawal()` - Withdrawal processing (implementation target for exercises)
  - `generateTransactionId()` - Transaction ID generation utility

- **banking/types.ts** - Shared TypeScript interfaces defining the domain model
  - `BankAccount`, `AccountOwner` - Account entities
  - `WithdrawalRequest`, `WithdrawalResult` - Operation DTOs
  - `WithdrawalError` - Error codes: `INSUFFICIENT_FUNDS`, `INVALID_AMOUNT`, `ACCOUNT_NOT_FOUND`

- **banking/banking.test.ts** - Vitest test suite covering:
  - Account creation validation (3 tests)
  - Withdrawal processing scenarios (5 tests: success, insufficient funds, invalid amount, currency mismatch, invalid account)

- **banking/banking-spec.md** - Business specification in Polish defining functional requirements and validation rules

### Directory Organization

```
banking/          - Domain logic, tests, types, and specifications
prompts/          - AI collaboration prompt templates (English & Polish)
  ├── decomposer.md / decomposer_pl.md     - Problem decomposition prompts
  └── unblocker.md / unblocker_pl.md       - Learning blocker resolution prompts
charts/           - Mermaid diagrams (e.g., request.md for sequence diagrams)
docs/             - Static assets
```

### TypeScript Configuration

The project uses TypeScript 5.8.2 with strict mode enabled (`tsconfig.json`):
- Target: ES2016
- Module: CommonJS
- Strict type checking enforced
- No `any` types allowed (per CONVENTIONS.md)

### Coding Conventions

From `.github/copilot-instructions.md` and `CONVENTIONS.md`:
- Use TypeScript 5.7+ with strict mode
- Prefer `const` over `let` and `var`
- Avoid `any` type
- Use two-space indentation
- PascalCase for type names (e.g., `WithdrawalRequest`)
- camelCase for functions (e.g., `processWithdrawal`)
- Keep files focused: domain logic in `banking/`, supporting files in respective directories

### Testing Approach

Follow the existing test structure from `banking/banking.test.ts`:
- Use nested `describe`/`it` blocks for organization
- Test both happy paths and error scenarios
- Assert specific error codes and messages
- Name test files `<feature>.test.ts` co-located with implementation
- Update `banking-spec.md` when adding new behaviors

### Commit Guidelines

Follow Conventional Commits pattern:
- `feat: add overdraft guard`
- `fix: correct balance calculation`
- `chore: update prompts`
- `test: add currency validation cases`

Include failing test reproductions when fixing bugs and attach `npm test` output to PRs.

### AI Collaboration

The repository is designed for AI-assisted development:
- Reference `banking-spec.md` for business requirements (written in Polish)
- Use prompt templates in `prompts/` for problem decomposition and learning assistance
- Follow the implementation workflow: spec → test → implementation
- Leverage the `.cursor/rules/hooks.mdc` for React Hooks validation when applicable

### Environment Configuration

The `.env.template` shows configuration for Aider tool with multiple AI models (OpenRouter, Google Gemini, OpenAI, Anthropic). The development workflow assumes AI coding assistants (Cursor, Copilot, Aider, Windsurf, Cline) will be used.

## Node Version

Node.js 22 (specified in `.nvmrc`)
