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
- [ ] List all issues found during testing
- [ ] Prioritize issues by severity
- [ ] Categorize by workflow

**Improvement Areas**:
- [ ] Workflow logic improvements
- [ ] Template enhancements
- [ ] Error handling
- [ ] User experience optimization
- [ ] Documentation clarity

---

## Phase 6: Implementation of Improvements

**Priority 1 (Critical)**:
- [ ] TBD based on testing

**Priority 2 (Important)**:
- [ ] TBD based on testing

**Priority 3 (Nice to have)**:
- [ ] TBD based on testing

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
