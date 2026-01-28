# Cosmos DB Agent Kit Testing Framework

This framework provides a structured approach for iteratively testing and improving the Cosmos DB Agent Kit skills.

---

## 🚀 QUICK START: Run a Test Iteration

**Copy and paste one of these prompts into a NEW chat session to run a test iteration.**

### E-Commerce Order API (.NET) - Next iteration
```
I want to run a test iteration for the Cosmos DB Agent Kit.

FIRST: Read the file `skills/cosmosdb-best-practices/AGENTS.md` completely - this contains 
all the Cosmos DB best practices you must follow.

THEN: Read `testing/scenarios/ecommerce-order-api/SCENARIO.md` for the requirements.

THEN: Check `testing/scenarios/ecommerce-order-api/iterations/` to find the next iteration number.

Create a new iteration folder (iteration-002-dotnet or next available) and build the 
application following the .NET prompt in SCENARIO.md. Apply ALL the Cosmos DB best 
practices from AGENTS.md throughout the implementation.

After building, run the app and test all endpoints. Document findings in ITERATION.md.
```

### E-Commerce Order API (Java)
```
I want to run a test iteration for the Cosmos DB Agent Kit.

FIRST: Read `skills/cosmosdb-best-practices/AGENTS.md` completely for Cosmos DB best practices.
THEN: Read `testing/scenarios/ecommerce-order-api/SCENARIO.md` for requirements.
THEN: Check iterations folder for next number.

Create iteration-XXX-java folder and build using the Java prompt. Apply ALL best practices.
Run the app, test endpoints, document findings in ITERATION.md.
```

### Other Scenarios
Replace `ecommerce-order-api` with:
- `iot-device-telemetry` - IoT time-series data
- `gaming-leaderboard` - Real-time leaderboards  
- `ai-chat-rag` - AI chat with vector search
- `multitenant-saas` - Multi-tenant SaaS app

And choose language: `dotnet`, `java`, `python`, `nodejs`, `go`, or `rust`

---

## 🤖 AGENT INSTRUCTIONS (Detailed)

**If you're an AI agent running a test iteration, follow these steps carefully:**

### ⚠️ CRITICAL: Load Skills FIRST

**Before building any application, you MUST load the Cosmos DB skills into your context.**

#### Option A: Read the AGENTS.md file directly (RECOMMENDED)
```
Read the file: skills/cosmosdb-best-practices/AGENTS.md
```
This file contains all 52+ rules. Read it completely before starting the iteration.

#### Option B: Reference the skill folder
If your agent supports workspace skills/instructions:
- **GitHub Copilot**: The `AGENTS.md` file in the workspace should auto-load
- **Cursor**: Add `skills/cosmosdb-best-practices/` to your context
- **Claude**: Use the file attachment or read the AGENTS.md file

#### Option C: Explicit instruction
Start your session with:
```
Before building this application, read and follow all rules in 
skills/cosmosdb-best-practices/AGENTS.md. Apply these Cosmos DB 
best practices throughout the implementation.
```

**Verify skills are loaded** by asking: "What are the Cosmos DB SDK best practices for connection mode?" 
If the agent mentions "Direct mode" and "singleton client", the skills are loaded.

---

### Running an Existing Scenario

1. **⚠️ LOAD THE SKILLS FIRST** (see above - this is mandatory!)

2. **List available scenarios:**
   ```
   testing/scenarios/
   ├── ecommerce-order-api/    ← E-commerce order management
   ├── iot-device-telemetry/   ← IoT time-series data
   ├── gaming-leaderboard/     ← Real-time leaderboards
   ├── ai-chat-rag/            ← AI chat with vector search
   └── multitenant-saas/       ← Multi-tenant SaaS app
   ```

3. **Check which iterations exist** by looking at `scenarios/<name>/iterations/`

4. **Read the SCENARIO.md** to understand requirements and get the prompt

5. **Create a new iteration folder:**
   ```
   scenarios/<name>/iterations/iteration-{NNN}-{language}/
   ```
   Where `{NNN}` is the next number and `{language}` is: `dotnet`, `java`, `python`, `nodejs`, `go`, or `rust`

6. **Build the app** using the prompt from SCENARIO.md (with skills loaded!)

7. **Test the app** - actually run it and verify endpoints work

8. **Document findings** in `ITERATION.md` inside the iteration folder

9. **Clean up** - remove bin/obj, zip source code, delete source files (keep only ITERATION.md + source-code.zip)

### Adding a New Scenario

1. **⚠️ LOAD THE SKILLS FIRST** (see above)
2. Copy `scenarios/_scenario-template.md` to `scenarios/<new-name>/SCENARIO.md`
3. Fill in the requirements, language suitability, and prompts
4. Create `scenarios/<new-name>/iterations/` folder
5. Run first iteration following steps above

---

## Purpose

The goal is to evaluate how well AI agents can build Cosmos DB applications using this skill kit, identify gaps, update the skills, and measure improvement over subsequent iterations.

## Supported Languages

| Language | SDK | Package | Typical Use Cases |
|----------|-----|---------|-------------------|
| **.NET** | Microsoft.Azure.Cosmos | `dotnet add package Microsoft.Azure.Cosmos` | Enterprise APIs, web apps |
| **Java** | azure-cosmos | Maven: `com.azure:azure-cosmos` | Enterprise, Spring Boot |
| **Python** | azure-cosmos | `pip install azure-cosmos` | AI/ML, data science, APIs |
| **Node.js** | @azure/cosmos | `npm install @azure/cosmos` | Serverless, web apps |
| **Go** | azcosmos | `go get github.com/Azure/azure-sdk-for-go/sdk/data/azcosmos` | Cloud-native, microservices |
| **Rust** | azure_data_cosmos | `cargo add azure_data_cosmos` | Systems, high-performance |

## Directory Structure

```
testing/
├── README.md                    # This file (agent instructions)
├── IMPROVEMENTS-LOG.md          # Track all skill improvements
├── scenarios/
│   ├── _scenario-template.md    # Template for new scenarios
│   ├── _iteration-template.md   # Template for iteration docs
│   └── <scenario-name>/
│       ├── SCENARIO.md          # Requirements & prompts (DO NOT MODIFY)
│       └── iterations/
│           ├── iteration-001-dotnet/
│           │   ├── ITERATION.md      # Findings doc (KEEP)
│           │   └── source-code.zip   # Archived source (KEEP)
│           ├── iteration-001-python/
│           └── iteration-002-dotnet/
```

## The Iteration Loop

```
┌─────────────────────────────────────────────────────────────────┐
│  0. LOAD SKILLS: Read skills/cosmosdb-best-practices/AGENTS.md │
│     ⚠️ This step is MANDATORY - do not skip!                   │
└───────────────────────────────┬─────────────────────────────────┘
                                ▼
┌─────────────────────────────────────────────────────────────────┐
│  1. Read SCENARIO.md for requirements and prompt               │
└───────────────────────────────┬─────────────────────────────────┘
                                ▼
┌─────────────────────────────────────────────────────────────────┐
│  2. Create iteration folder: iteration-{N}-{lang}/             │
└───────────────────────────────┬─────────────────────────────────┘
                                ▼
┌─────────────────────────────────────────────────────────────────┐
│  3. Build the app following the prompt                         │
│     • Apply Cosmos DB best practices FROM THE LOADED SKILLS    │
│     • Reference specific rules as you implement                │
└───────────────────────────────┬─────────────────────────────────┘
                                ▼
┌─────────────────────────────────────────────────────────────────┐
│  4. TEST THE APP                                               │
│     • Run it locally (with Cosmos DB Emulator)                 │
│     • Call all endpoints                                       │
│     • Verify data is persisted in Cosmos DB                    │
│     • Note any bugs or issues                                  │
└───────────────────────────────┬─────────────────────────────────┘
                                ▼
┌─────────────────────────────────────────────────────────────────┐
│  5. Document findings in ITERATION.md                          │
│     • Bugs found                                               │
│     • Best practice gaps                                       │
│     • Score (1-10)                                             │
│     • Lessons learned (see Feedback Loop below!)               │
└───────────────────────────────┬─────────────────────────────────┘
                                ▼
┌─────────────────────────────────────────────────────────────────┐
│  6. FEEDBACK LOOP: Review and propose new rules                │
│     • See "Continuous Improvement" section below               │
│     • Create new rules for patterns/issues discovered          │
│     • Update IMPROVEMENTS-LOG.md                               │
└───────────────────────────────┬─────────────────────────────────┘
                                ▼
┌─────────────────────────────────────────────────────────────────┐
│  7. Clean up iteration folder                                  │
│     • Delete bin/, obj/, node_modules/, etc.                   │
│     • Zip all source files to source-code.zip                  │
│     • Delete source files (keep only ITERATION.md + zip)       │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🔄 Continuous Improvement: The Feedback Loop

**After each iteration, review the lessons learned and propose new rules!**

This is a critical part of the testing framework. The goal is to continuously improve the skill kit based on real-world issues encountered during development.

### Step 1: Review Iteration Results

After completing an iteration, analyze the `ITERATION.md` for:

1. **Bugs encountered** - Were there patterns that caused issues?
2. **Workarounds discovered** - Did you find solutions not documented in the rules?
3. **SDK-specific quirks** - Did the SDK behave unexpectedly?
4. **Configuration challenges** - Were there setup issues (emulator, SSL, env vars)?
5. **Missing guidance** - What questions came up that the rules didn't answer?

### Step 2: Check Existing Rules

Before creating a new rule, verify it doesn't already exist:

```
skills/cosmosdb-best-practices/rules/
├── model-*.md       # Data modeling rules
├── partition-*.md   # Partition key rules
├── query-*.md       # Query optimization rules
├── sdk-*.md         # SDK best practices
├── index-*.md       # Indexing strategies
├── throughput-*.md  # Throughput & scaling
├── global-*.md      # Global distribution
├── monitoring-*.md  # Monitoring & diagnostics
└── pattern-*.md     # Design patterns
```

### Step 3: Propose New Rules

If you identify a gap, create a new rule following this template:

```markdown
---
title: Short description of the rule
impact: CRITICAL | HIGH | MEDIUM | LOW
impactDescription: brief explanation of impact
tags: category, sdk, relevant, keywords
---

## Rule Title

Brief description of the problem this rule addresses.

**Problem:**
\`\`\`language
// Code showing the problem
\`\`\`

**Solution:**
\`\`\`language
// Code showing the correct approach
\`\`\`

**Key Points:**
- Important takeaway 1
- Important takeaway 2

Reference: [Link to official docs](url)
```

### Step 4: Categories for New Rules

| Prefix | Category | When to Use |
|--------|----------|-------------|
| `model-` | Data Modeling | Document structure, embedding vs referencing |
| `partition-` | Partition Key Design | Partition key selection, distribution |
| `query-` | Query Optimization | Query patterns, filtering, pagination |
| `sdk-` | SDK Best Practices | Client configuration, connection, retries |
| `index-` | Indexing Strategies | Index policies, composite indexes |
| `throughput-` | Throughput & Scaling | RU provisioning, autoscale |
| `global-` | Global Distribution | Multi-region, consistency |
| `monitoring-` | Monitoring & Diagnostics | Logging, metrics, alerts |
| `pattern-` | Design Patterns | Architecture patterns (e.g., Change Feed) |

### Step 5: Update IMPROVEMENTS-LOG.md

After creating new rules, log them:

```markdown
## 2026-01-28 - Iteration 003 (Java)

### New Rules Created
- `sdk-emulator-ssl.md` - SSL certificate configuration for Java SDK with emulator
- `sdk-java-content-response.md` - contentResponseOnWriteEnabled requirement

### Lessons Learned
- Java SDK requires Gateway mode for emulator (Direct mode fails)
- createItem returns null unless contentResponseOnWriteEnabled is set
```

### Step 6: Regenerate AGENTS.md

After adding rules, rebuild the compiled AGENTS.md:

```bash
npm run build
# or
node scripts/compile.js
```

This ensures the new rules are included when agents load the skills.

### Examples of Rules Added from Iterations

| Iteration | Issue Found | Rule Created |
|-----------|-------------|--------------|
| 001-dotnet | Enum queries returned empty | `sdk-serialization-enums.md` |
| 003-java | SSL handshake failures | `sdk-emulator-ssl.md` |
| 003-java | createItem returned null | `sdk-java-content-response.md` |
| 004-python | System env vars overrode .env | `sdk-local-dev-config.md` |
| Multiple | Cross-partition admin queries | `pattern-change-feed-materialized-views.md` |

### Questions to Ask After Each Iteration

1. ❓ **Was there a bug that a rule could have prevented?**
   → Create a new rule with the problem and solution

2. ❓ **Did you discover a workaround not in the docs?**
   → Document it as a rule for future iterations

3. ❓ **Was there SDK-specific behavior that surprised you?**
   → Add to existing SDK rule or create new one

4. ❓ **Did you spend time debugging configuration issues?**
   → Create a rule to save time for future developers

5. ❓ **Did you find a pattern that could benefit other scenarios?**
   → Create a `pattern-*.md` rule

---

## Scoring Guide

| Score | Description |
|-------|-------------|
| 1-3 | Major issues, app doesn't work, significant intervention needed |
| 4-6 | Functional but with notable gaps or bugs |
| 7-8 | Good result with minor issues |
| 9-10 | Excellent, production-quality code |

## Completed Iterations

| Scenario | Language | Iteration | Skills Loaded? | Score | Key Findings |
|----------|----------|-----------|----------------|-------|--------------|
| ecommerce-order-api | .NET | 001 | ❌ NO (baseline) | 6/10 | Enum serialization bug, no pagination |

> **Note**: Iteration 001 was run WITHOUT skills loaded. This serves as a baseline.
> Future iterations should load skills first to test their effectiveness.

## Next Actions

Based on findings, these actions are tracked:

- [x] ✅ Created `sdk-serialization-enums.md` rule (prevents enum query bug)
- [x] ✅ Added section 4.10 to AGENTS.md for enum serialization
- [ ] Investigate why agent didn't apply existing `query-pagination.md` rule
- [ ] Investigate why agent didn't apply existing `monitoring-ru-consumption.md` rule

## Testing Checklist for Agents

When completing an iteration, verify:

### Build & Test
- [ ] **⚠️ Skills were loaded BEFORE building** (read AGENTS.md first!)
- [ ] App compiles/builds without errors
- [ ] App runs locally with Cosmos DB Emulator
- [ ] All CRUD endpoints work
- [ ] Data persists to Cosmos DB
- [ ] Query endpoints return correct data
- [ ] No obvious security issues

### Documentation
- [ ] ITERATION.md documents all findings
- [ ] ITERATION.md notes which skills were applied/not applied
- [ ] ITERATION.md includes "Lessons Learned" section
- [ ] Score assigned with justification

### Feedback Loop (NEW!)
- [ ] **Reviewed lessons learned for potential new rules**
- [ ] **Checked if issues could have been prevented by a rule**
- [ ] **Created new rules for undocumented patterns/issues**
- [ ] **Updated IMPROVEMENTS-LOG.md with new rules**

### Cleanup
- [ ] Source code is zipped and source files deleted
- [ ] Build artifacts removed (bin/, obj/, node_modules/, target/, etc.)
