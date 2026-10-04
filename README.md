# Script-Controlled ACL – Restrict Record Access Based on Field Value

A ServiceNow lab that uses script-controlled Access Control Lists (ACLs) so only permitted roles can
read, create, edit and delete records of a custom table. Users with role `bb1` see only
**EEE-branch** records, and administrators keep full access.

**Team ID:** SWTID-2026-6519 · **Team size:** 5

| Role | Name |
|---|---|
| Team Leader | Suhas V |
| Team Member | Sureshbabu M |
| Team Member | Vignesh Kumar S |
| Team Member | Anuja P |
| Team Member | Archana S |

## What was built
| Item | Detail |
|---|---|
| Test user | `EEEUser` |
| Roles | `bb1` (read), `bb2` (create), `bb3` (write), `bb4` (delete) |
| Table | `u_institution_details` (Roll No., Student, Faculty, Branch, Email, Phone, Description) |
| Read ACL | role `bb1` + data condition *Branch is EEE* + advanced script |
| Create / Write / Delete ACLs | roles `bb2` / `bb3` / `bb4` |
| Verification | Impersonated an EEE user, a user without roles, and admin |

## Read ACL script
```js
(function () {
  if (gs.hasRole('admin')) { return true; }   // admin: full access
  if (gs.hasRole('bb1'))   { return true; }   // EEE users (Branch is EEE condition limits records)
  return false;                               // everyone else: denied
})();
```

## Project documents
All phase documents are in the `Project Templates - Completed` folder:
1. Ideation Phase – problem statement, empathy map, brainstorming
2. Requirement Analysis – requirements, data flow diagram and user stories, technology stack
3. Project Design – problem-solution fit, proposed solution, solution architecture
4. Project Planning – backlog, sprints, velocity, burndown
5. Project Development – performance testing, UAT, UAT report
6. Project Documentation – final project report

## Results
- Admin sees all records, a user without roles sees none, and a `bb1` user sees only EEE records.
- `bb1+bb2` get the **New** button, `bb1–bb3` can edit, and `bb1–bb4` can delete.
- 9 / 9 test cases passed.
