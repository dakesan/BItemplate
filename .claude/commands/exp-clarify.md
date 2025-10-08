---
description: Clarify experiment plan through interactive Q&A
---

User input: $ARGUMENTS

Goal: Identify underspecified areas in the experiment plan (labnote) and resolve them through targeted clarification questions (max 5).

Note: Run this AFTER `/exp-plan` and BEFORE starting the actual experiment to reduce ambiguity and prevent wasted computational resources.

Execution steps:

1. Parse experiment number from $ARGUMENTS or ask user:
   - Format: Exp## (e.g., Exp01)

2. Load project-wide config and labnote:
   - Read `pyproject.toml` section `[tool.bioinfo-experiment.compute]` for default resources
   - Find labnote: `notebook/labnote/Exp##_*.md`
   - If labnote not found, instruct user to run `/exp-plan` first

3. Perform structured coverage scan. For each category, mark status: Clear / Partial / Missing:

   Experiment Objective & Scope:
   - Research question clearly stated (what biological question)
   - Expected outcome defined (qualitative or quantitative)
   - Explicit out-of-scope items

   Input Data (HIGH PRIORITY):
   - **Absolute path** to input file(s) specified
   - Data format explicit (FASTQ, BAM, VCF, CSV, HDF5, etc.)
   - Sample information (single/multiple, paired-end/single-end)
   - Data scale specified (coverage depth, file size, number of samples)
   - Quality assumptions or preprocessing status

   Output Specification (HIGH PRIORITY):
   - **Absolute path** to output directory specified
   - Output format defined (VCF, BAM, TSV, HDF5, etc.)
   - Expected file naming convention
   - Intermediate files handling (keep/delete)

   Analysis Method:
   - Tool/algorithm choice justified (why this tool)
   - Key parameters identified (not all, just critical ones)
   - Reference data specified (genome version, annotation source, database versions)

   Success Criteria & Validation:
   - Quantitative metrics defined (coverage ≥30X, Q-score ≥20, etc.)
   - Expected result range (number of variants, genes, clusters)
   - Validation strategy (visual inspection, known controls, sanity checks)

   Compute Resources:
   - Threads (default: 90 from pyproject.toml, adjust if needed)
   - Memory (default: 358GB from pyproject.toml, adjust if needed)
   - Estimated runtime (hours/days)
   - Disk space required

   Edge Cases & Failure Handling:
   - What constitutes failed run (error codes, missing output)
   - How to handle low-quality data (thresholds for rejection)
   - Retry strategy if applicable

   Biological Context:
   - Hypothesis or biological question
   - How results inform research goals
   - Interpretation criteria (what makes a "good" result biologically)

4. Generate prioritized clarification questions (max 5):

   Priority ranking (ask in this order):
   1. **Path specification** (input/output) - CRITICAL
   2. **Data format & scale** - prevents wrong tool choice
   3. **Success criteria** - prevents uninterpretable results
   4. **Tool/parameter rationale** - prevents poor analysis choices
   5. **Biological context** - ensures meaningful interpretation

   Each question must be answerable with:
   - Multiple choice (2-5 options), OR
   - Short answer (≤10 words for paths, ≤5 words otherwise)

   Skip questions if:
   - Already clearly specified in labnote
   - Low impact on analysis outcome
   - Better deferred to execution phase

5. Sequential questioning (interactive):

   Present ONE question at a time.

   For multiple choice:
   | Option | Description |
   |--------|-------------|
   | A      | [Option A description] |
   | B      | [Option B description] |
   | C      | [Option C description] |
   | Short  | Provide custom answer (≤5 words) |

   For path questions:
   - `Format: Absolute path (e.g., /data/raw/sample.fastq.gz)`

   For short answer:
   - `Format: Short answer (≤5 words)`

   After each answer:
   - Validate format (path exists? format reasonable?)
   - Record in memory
   - Proceed to next question

   Stop when:
   - All critical items resolved, OR
   - User signals completion ("done", "stop", "skip"), OR
   - 5 questions reached

6. Integration (incremental update after EACH answer):

   - Maintain in-memory labnote content
   - Ensure `## Clarifications` section exists
     - Add after `## Objective` if missing
   - Add session header: `### Clarification Session YYYY-MM-DD`
   - Append: `- Q: [question] → A: [answer]`

   Update corresponding sections:
   - **Input Data** answer → Update "Input Data" section with absolute path, format, scale
   - **Output** answer → Update "Expected Output" with path, format
   - **Objective** answer → Refine research question or scope
   - **Method** answer → Add tool justification, parameter rationale
   - **Success criteria** answer → Add quantitative thresholds
   - **Resources** answer → Override project defaults if needed
   - **Edge cases** answer → Add to "Notes" section

   Replace vague statements:
   - "quality data" → "Q-score ≥20"
   - "sufficient coverage" → "≥30X mean coverage"
   - "some samples" → "12 tumor-normal pairs"

   Save file immediately after each integration (atomic write)

7. Validation (after each write):
   - Clarifications section has exactly one bullet per answer
   - Total questions asked ≤ 5
   - Input/Output paths are absolute (start with /)
   - No contradictory statements remain
   - Vague terms replaced with specifics
   - Markdown structure valid

8. Report completion:

   ```
   ✓ Clarification complete for Exp##

   Questions answered: X/5
   Labnote updated: notebook/labnote/Exp##_description.md

   Sections modified:
   - Input Data (path, format, scale specified)
   - Expected Output (path and format defined)
   - Success Criteria (metrics added)

   Coverage Summary:
   | Category | Status |
   |----------|--------|
   | Objective & Scope | ✓ Resolved |
   | Input Data | ✓ Resolved |
   | Output Specification | ✓ Resolved |
   | Analysis Method | Clear (sufficient) |
   | Success Criteria | ✓ Resolved |
   | Compute Resources | Clear (using defaults) |
   | Edge Cases | Deferred (low impact) |
   | Biological Context | Clear (sufficient) |

   Recommendation: Ready to proceed with experiment
   Next: Start analysis or run `/exp-update-labnote Exp##` as you progress
   ```

Behavior rules:

- **ALWAYS prioritize path clarification first** (input and output)
- If no critical ambiguities, report "Experiment plan sufficiently clear" and suggest proceeding
- If labnote missing, instruct `/exp-plan` first
- Never exceed 5 questions total
- For paths, validate they look reasonable (absolute, correct extension)
- Don't ask about minor parameter tuning unless critical
- Respect early termination signals
- If compute resources not mentioned, assume pyproject.toml defaults (90 cores, 358GB RAM)
- Flag high-impact unresolved items if quota reached

Focus clarifications on preventing:
- Missing or wrong input files (wasted setup time)
- Undefined output locations (lost results)
- Uninterpretable results (no success criteria)
- Wrong tool/parameters (wasted compute)
- Unmet biological objectives (misaligned analysis)
