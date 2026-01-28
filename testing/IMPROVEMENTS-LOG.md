# Improvements Log

This document tracks all skill improvements made as a result of testing iterations. Each entry links the improvement back to the test scenario and iteration that identified the need.

---

## Format

Each improvement entry should include:
- **Date**: When the improvement was made
- **Scenario**: Which test scenario identified the need
- **Iteration**: Which iteration discovered the issue
- **Issue**: What problem was observed
- **Improvement**: What was changed in the skills
- **Files Modified**: List of skill files changed

---

## Improvements

#### 2026-01-28: Cross-Iteration Review - New Rules from Lessons Learned

Based on reviewing all iteration ITERATION.md files and identifying patterns that could become rules:

**NEW RULES CREATED:**

1. **`pattern-change-feed-materialized-views.md`** (HIGH impact)
   - **Source**: Iterations 001, 002, 003 all noted cross-partition queries for admin endpoints
   - **Issue**: Status/date queries require expensive cross-partition fan-out
   - **Solution**: Document Change Feed pattern to maintain separate container optimized for admin queries
   - **Benefit**: Converts cross-partition queries into single-partition lookups

2. **`sdk-java-content-response.md`** (MEDIUM impact)
   - **Source**: Iteration 003-java discovered createItem returned null
   - **Issue**: Java SDK doesn't return document content after write operations by default
   - **Solution**: Set `contentResponseOnWriteEnabled(true)` at client or request level
   - **Benefit**: Prevents confusion when created items appear null

3. **`sdk-local-dev-config.md`** (MEDIUM impact)
   - **Source**: Iteration 004-python encountered system env vars overriding .env file
   - **Issue**: Developers with Azure CLI configured have COSMOS_ENDPOINT pointing to cloud, not emulator
   - **Solution**: Use `load_dotenv(override=True)`, environment-specific configs, and log endpoint at startup
   - **Benefit**: Prevents accidental connections to production during local development

**EXISTING RULE ENHANCED:**

4. **`sdk-emulator-ssl.md`** - Now covers ALL SDKs
   - **Previous**: Java-only SSL certificate guidance
   - **Enhanced**: Added .NET, Python, Node.js examples for Gateway mode and SSL handling
   - **Benefit**: Single reference for all SDK emulator configuration

**COMPILE SCRIPT UPDATED:**
- Added `pattern-` prefix for Design Patterns category (section 9)

**FILES MODIFIED:**
- `rules/pattern-change-feed-materialized-views.md` (new)
- `rules/sdk-java-content-response.md` (new)
- `rules/sdk-local-dev-config.md` (new)
- `rules/sdk-emulator-ssl.md` (enhanced)
- `rules/_sections.md` (added section 9)
- `SKILL.md` (updated quick reference)
- `scripts/compile.js` (added pattern- prefix)
- `AGENTS.md` (regenerated - now 53 rules)
- `testing/README.md` (added Continuous Improvement / Feedback Loop section)

---

#### 2026-01-28: Iteration 003 - Java SDK Validation (ecommerce-order-api)

- **Scenario**: ecommerce-order-api
- **Iteration**: 003-java (WITH skills)
- **Result**: ✅ **SUCCESS** - Critical enum serialization test passed
- **Improvement Validated**: Rule 4.10 works across both .NET and Java SDKs
- **Score**: 9.0/10
- **Key Rules Applied**:
  - 4.10: `@JsonValue`/`@JsonCreator` for enum serialization ✅
  - 4.1: Singleton CosmosAsyncClient via Spring @Bean ✅
  - 4.2: Async APIs with Project Reactor (Mono<T>) ✅
  - 4.3: ThrottlingRetryOptions configured ✅
  - 1.1: Embedded OrderItems ✅
  - 2.1: High-cardinality partition key (customerId) ✅
  - 3.1/3.5: Single-partition queries with SqlParameter ✅
  - 5.2: Composite indexes ✅
- **Observations**: 
  - The skill kit successfully guided Java-specific enum serialization
  - Gateway mode required for emulator (Direct mode has SSL issues)
  - `contentResponseOnWriteEnabled(true)` needed to get item back after create
- **Tests**: 5/6 passing (date range query has format issue, not enum-related)

**NEW RULE CREATED**: `sdk-emulator-ssl` - Configure SSL for Cosmos DB Emulator in Java
- **Issue**: Java SDK fails with SSL handshake errors when connecting to emulator
- **Solution**: Import emulator certificate into JDK truststore + use Gateway mode
- **Files Modified**: 
  - `rules/sdk-emulator-ssl.md` (new file)
  - `SKILL.md` (added to quick reference)
  - `AGENTS.md` (regenerated)

#### 2026-01-28: Iteration 002 - Skills Successfully Applied (ecommerce-order-api)

- **Scenario**: ecommerce-order-api
- **Iteration**: 002-dotnet (WITH skills)
- **Result**: ✅ **SUCCESS** - All tests passed, including the critical enum serialization test
- **Improvement Validated**: Rule 4.10 (enum serialization) was applied correctly, fixing the bug from iteration-001
- **Score**: 9.1/10 (vs 6/10 in baseline iteration-001)
- **Key Rules Applied**:
  - 4.10: JsonStringEnumConverter configured ✅
  - 4.1: Singleton CosmosClient ✅
  - 4.4: Direct connection mode ✅
  - 1.1: Embedded OrderItems ✅
  - 2.1/2.4: High-cardinality partition key (customerId) ✅
  - 3.1/3.2: Single-partition queries with projections ✅
  - 5.2: Composite indexes ✅
- **Observations**: 
  - The skill kit successfully prevented the enum serialization bug
  - Agent applied 18+ rules from the skill kit
  - Cross-partition queries (status/date) are unavoidable given partition key choice - could add guidance for Change Feed patterns

#### 2026-01-27: Testing Framework - Skills Must Be Loaded First

- **Scenario**: ecommerce-order-api
- **Iteration**: 001-dotnet
- **Issue**: Iteration 001 was run WITHOUT loading the skill kit first, making it a baseline test rather than a skill kit test
- **Improvement**: Updated testing framework documentation to emphasize skills MUST be loaded before each iteration
- **Files Modified**: 
  - `testing/README.md` - Added "CRITICAL: Install Skills FIRST" section
  - `testing/scenarios/_iteration-template.md` - Added "Skills Verification" section
  - `iteration-001-dotnet/ITERATION.md` - Marked as baseline (no skills)

#### 2026-01-27: Enum Serialization Mismatch Bug (ecommerce-order-api)

- **Scenario**: ecommerce-order-api
- **Iteration**: 001-dotnet
- **Issue**: Agent generated code where Cosmos SDK stored enums as integers but queries searched for strings, causing status queries to return empty results
- **Improvement**: ✅ Added new rule `sdk-serialization-enums.md` with guidance on consistent enum serialization
- **Priority**: HIGH
- **Files Modified**: 
  - `rules/sdk-serialization-enums.md` (new)
  - `AGENTS.md` (added section 4.10)

#### 2026-01-27: Missing Pagination Pattern (ecommerce-order-api)

- **Scenario**: ecommerce-order-api
- **Iteration**: 001-dotnet
- **Issue**: List queries returned all results without pagination, which would fail at scale
- **Analysis**: Rule `query-pagination.md` already exists with good content - the agent simply didn't apply it
- **Action**: No rule change needed, but highlights that agents may not always apply existing rules
- **Priority**: HIGH (for observation)
- **Files Modified**: None - rule already exists

#### 2026-01-27: Missing RU Diagnostics Logging (ecommerce-order-api)

- **Scenario**: ecommerce-order-api
- **Iteration**: 001-dotnet
- **Issue**: No logging of CosmosDiagnostics or RU consumption for debugging/monitoring
- **Analysis**: Rule `monitoring-ru-consumption.md` already exists with comprehensive SDK examples - agent didn't apply it
- **Action**: No rule change needed - rule has .NET examples with logging, telemetry, and middleware patterns
- **Priority**: MEDIUM (for observation)
- **Files Modified**: None - rule already exists

---

## Release History

### v1.0.0 (Initial Release)

- Initial set of 48 rules covering:
  - Data modeling (6 rules)
  - Partition key design (6 rules)
  - Query optimization (6 rules)
  - SDK best practices (9 rules)
  - Indexing strategies (5 rules)
  - Throughput & scaling (5 rules)
  - Global distribution (6 rules)
  - Monitoring & diagnostics (5 rules)
