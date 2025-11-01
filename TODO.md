# Bioinformatics Experiment Skill Testing & Refinement

## Overview

This TODO list guides the systematic testing and refinement of the `bioinformatics-experiment` skill. Each workflow will be executed in order, issues will be documented, and improvements will be implemented.

## Testing Workflow

### Phase 1: Experiment Planning Workflow

**Goal**: Create a new experiment labnote with proper structure

**Steps**:
- [ ] Execute Experiment Planning Workflow
- [ ] Verify experiment number assignment (should be Exp01)
- [ ] Check labnote file creation in `notebook/labnote/`
- [ ] Validate template placeholder replacement
- [ ] Document any issues or improvements needed

**Test Case**: Create an experiment for "RNA-seq quality control"
- Input: Sample RNA-seq data
- Output: Quality control metrics and reports

---

### Phase 2: Experiment Clarification Workflow

**Goal**: Resolve ambiguities in the experiment plan through targeted Q&A

**Steps**:
- [ ] Execute Experiment Clarification Workflow on Exp01
- [ ] Test coverage scan functionality
- [ ] Answer prioritized questions (max 5)
- [ ] Verify labnote updates after each answer
- [ ] Validate path specifications are absolute
- [ ] Check that vague terms are replaced with specifics
- [ ] Document any issues or improvements needed

**Expected Clarifications**:
- Input data absolute paths
- Output directory structure
- Data format and scale
- Success criteria (quantitative metrics)
- Compute resource allocation

---

### Phase 3: Labnote Update Workflow

**Goal**: Update experiment labnote with commands, results, and observations

**Steps**:
- [ ] Execute Labnote Update Workflow for Exp01
- [ ] Test adding process steps with commands
- [ ] Test adding results/observations
- [ ] Test adding issues encountered
- [ ] Verify timeline format in labnote
- [ ] Check reproducibility of recorded commands
- [ ] Document any issues or improvements needed

**Test Updates**:
- Add FastQC execution command
- Record quality metrics results
- Note any quality issues found

---

### Phase 4: Report Generation Workflow

**Goal**: Create analysis report from completed experiment(s)

**Steps**:
- [ ] Execute Report Generation Workflow for Exp01
- [ ] Verify labnote data extraction
- [ ] Check auto-filled sections (objective, data, pipeline, software)
- [ ] Validate placeholder sections for human interpretation
- [ ] Test citation system (labnotes, figures, data files)
- [ ] Document any issues or improvements needed

**Expected Sections**:
- Auto-filled: Objective, Data Description, Pipeline Steps, Software Versions
- Human-written: Results Interpretation, Biological Implications, Discussion, Conclusions

---

## Phase 5: Issue Collection & Refinement

**Identified Issues**:

### Phase 1 Issues (Experiment Planning):
- [x] **Experiment number should be requested from user**: Currently auto-increments, but user may want to specify (e.g., continuing from existing experiments)
- [x] **Template contains residual "Action required" messages**: First line of template has unnecessary instruction
- [ ] Validate with real use case (~/Desktop/Squidiff)

### Phase 2 Issues (Experiment Clarification):
- [ ] Need to test with Squidiff use case
- [ ] Validate careful, step-by-step questioning approach
- [ ] Test text refinement quality

### General Issues:
- [x] **Need emphasis on careful writing**: All workflows should emphasize thoughtful, deliberate text composition
- [ ] macOS grep compatibility (no -P flag support)

**Improvement Areas**:
- [x] Workflow logic improvements: Add experiment number request to Planning Workflow
- [ ] Template enhancements: Remove unnecessary "Action required" messages
- [x] Error handling: macOS-compatible commands
- [x] User experience optimization: Let user specify experiment number
- [x] Documentation clarity: Add "careful writing" philosophy to all workflows

---

## Phase 6: Implementation of Improvements

### CRITICAL: Design Misunderstanding Identified (2025-11-01)

**Previous (INCORRECT) Design**:
- ❌ 1 labnote file = 1 experiment
- ❌ File naming: `Exp##_description.md` (e.g., `Exp01_rnaseq-qc.md`)
- ❌ Auto-incrementing experiment numbers
- ❌ Each file contains single Trial sections

**Correct Design** (based on ~/Documents/Hiro/obsidian-note):
- ✓ **1 labnote file = 1 experiment theme (containing multiple Exp## sections)**
- ✓ **File naming**: `YYYYMMDD_<experiment-title>.md` (e.g., `20250125_squidiff-testing.md`)
- ✓ **User provides**: Date and experiment title (not auto-generated)
- ✓ **File structure**:
  ```markdown
  # YYYYMMDD_experiment-title

  >[!Todo] Background
  >- Overall experiment purpose

  ## 実験1: Exp01 (Purpose/Phase)
  >[!Works] Methods
  >[!Done] Results

  ## 実験2: Exp02 (Purpose/Phase)
  >[!Works] Methods
  >[!Done] Results

  >[!Important] Discussion
  ## Conclusions
  ```

**Required Changes**:

**Priority 1 (Critical - Complete Redesign)**:
- [ ] Redesign Workflow 1: Create labnote file with YYYYMMDD_title.md naming
- [ ] Redesign Workflow 2: Add new Exp## section to existing labnote
- [ ] Redesign Workflow 3: Update specific Exp## section within labnote
- [ ] Redesign Workflow 4: Generate lab report from labnote(s)
- [ ] Create new labnote template matching obsidian-note format
- [ ] Create new lab report template
- [ ] Update all workflow references to match new design

**Priority 2 (Important)**:
- [ ] Add Obsidian callout syntax support ([!Todo], [!Works], [!Done], [!Important])
- [ ] Add wikilink support for cross-referencing
- [ ] Integrate with ~/Desktop/Squidiff as test case

**Priority 3 (Nice to have)**:
- [ ] Multi-labnote aggregation for reports
- [ ] Protocol reference system ([[protocol_*]])
- [ ] Auto-generated table templates

---

## Testing Notes

### What to Look For:

1. **Workflow Execution**:
   - Does each workflow execute without errors?
   - Are prompts clear and actionable?
   - Is the user experience smooth?

2. **File Operations**:
   - Are files created in correct locations?
   - Are filenames following conventions?
   - Are file contents properly formatted?

3. **Data Integrity**:
   - Are placeholders replaced correctly?
   - Are paths absolute and valid?
   - Are commands reproducible?

4. **Template Quality**:
   - Are templates well-structured?
   - Do they provide useful scaffolding?
   - Are they AI-readable (60%) and human-readable (40%)?

5. **Integration**:
   - Do workflows chain together naturally?
   - Is information preserved across workflows?
   - Are references and citations working?

---

## Success Criteria

- [ ] All 4 workflows execute successfully end-to-end
- [ ] Generated files match expected structure
- [ ] No critical bugs or blockers
- [ ] User experience is intuitive
- [ ] Documentation is accurate

---

## Next Steps After Testing

1. Document all findings in this file
2. Create improvement backlog
3. Prioritize and implement fixes
4. Retest affected workflows
5. Update skill documentation
6. Update templates as needed
