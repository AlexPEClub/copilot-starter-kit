# QA Test Results Template

Add this section to the END of the feature spec `/features/PROJ-X.md`:

```markdown
---

## QA Test Results

**Tested:** YYYY-MM-DD
**App URL:** http://localhost:3000
**Tester:** QA Engineer (AI)

### Acceptance Criteria Status

#### AC-1: [Criterion Name]
- [x] Sub-criterion passed
- [ ] BUG: Sub-criterion failed (describe what went wrong)

#### AC-2: [Criterion Name]
- [x] All sub-criteria passed

### Edge Cases Status

#### EC-1: [Edge Case Name]
- [x] Handled correctly

#### EC-2: [Edge Case Name]
- [ ] BUG: Not handled (describe expected vs actual behavior)

### Security Audit Results
- [x] Authentication: Cannot access without login
- [x] Authorization: Users cannot access other users' data
- [x] Input validation: XSS attempts blocked
- [x] Rate limiting: Excessive requests handled
- [ ] BUG: [Security issue description]

### Bugs Found

#### BUG-1: [Bug Title]
- **Severity:** Critical | High | Medium | Low
- **Steps to Reproduce:**
  1. Go to [page]
  2. Do [action]
  3. Expected: [what should happen]
  4. Actual: [what actually happens]
- **Screenshot:** [if visual bug]
- **Priority:** Fix before deployment | Fix in next sprint | Nice to have

### Summary
- **Acceptance Criteria:** X/Y passed
- **Bugs Found:** N total (C critical, H high, M medium, L low)
- **Security:** [Pass / Issues found]
- **Production Ready:** YES / NO
- **Recommendation:** [Deploy / Fix bugs first]
```
