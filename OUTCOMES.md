# Master Level Exercise Outcomes

**Student/Group Name**: Asma Jaradat, "Individual - virtual mode, I have no group"
**Level Completed**: Master
**Date**: 02/01/2026

---

## 📋 Exercise Summary
**Exercise**: Master Level – History Rewriting with Amend and Rebase
**Status**: ✅ Completed

---

## ✅ Part 1 – Amending Commits
### Commands Used
```bash
echo "version=1.0" > config.txt
git add config.txt
git commit -m "Add configuration file"

echo "environment=production" >> config.txt
git add config.txt
git commit --amend -m "Add complete configuration file"

git log --oneline -n 3
```

**Before & After**:
- Before amend: Two commits (initial + missing config)
- After amend: One commit with full configuration

---

## ✅ Part 2 – Interactive Rebase
### Commands Used
```bash
echo "Feature A" > featureA.txt
git add featureA.txt
git commit -m "Add feature A"

echo "Feature B" > featureB.txt
git add featureB.txt
git commit -m "Add feature B"

echo "Fix typo in A" >> featureA.txt
git add featureA.txt
git commit -m "Fix typo"

git rebase -i HEAD~3
![rebase](image-6.png)
```

**Result**:
- "Fix typo" squashed into previous commit
- "Add feature B" message reworded
- Clean history: Two commits instead of three
![reword](image-7.png)![successfulrebase](image-8.png)

---

## ✅ Part 3 – Rebasing a Branch
### Commands Used
```bash
git checkout -b feature/awesome-feature
echo "Awesome Feature" > awesome.txt
git add awesome.txt
git commit -m "Add awesome feature"

git checkout master
echo "Master update" > master-update.txt
git add master-update.txt
git commit -m "Update on master branch"

git checkout feature/awesome-feature
git rebase master

git log --graph --oneline --all -n 10
```

**Result**:
- Feature branch rebased on updated master
- Linear history (no merge commit)

---

## ✅ Part 4 – Understanding Risks
- Commit SHAs changed after amend/rebase → proof of history rewrite
 When we run git commit --amend or git rebase, Git creates new commits instead of editing the old ones.
 This means the SHA identifiers change:
 proof:
  Before: 6570dce Add feature B
  After:  cec3444 Add feature B using reword
  # altough it's powerful but it's dangerous because it changes the identity of commits

- Why not rewrite public history:
      - Breaks collaboration, causes conflicts
      - If others have already pulled the old commits, rewriting them causes divergence.
      - Leads to merge conflicts, broken builds, and confusion.
- Safe workflow:
      - Rebase/amend only on private branches
      - Use: git push --force-with-lease  instead of --force for safety
      - Document the rewrites in team communication

---


**Merge vs Rebase**:
```mermaid
graph TD
A[Commit A] --> B[Commit B]
B --> E[Commit E]
B --> C[Feature C]
C --> D[Feature D]
```
After Merge: Adds merge commit
After Rebase: C and D replayed on top of E → linear history

---

## 🗨 Personal Reflection
Working through this exercise I learned the 2 sides  power and risks of rewriting Git history. I learned how `git commit --amend` and `git rebase -i` can create a clean, professional commit log by squashing and rewording commits. The most challenging part was fixing interactive rebase errors caused by incorrect syntax and OneDrive locks. Resolving these issues helped me understand Git internals and recovery commands like `git rebase --abort` and manual cleanup of `.git/rebase-merge`.  

Rebasing a branch clarified why teams prefer linear history for clarity, but also why rewriting shared history is dangerous. I now understand the importance of using `--force-with-lease` instead of `--force` when pushing rewritten history. In real projects, I would only rebase private feature branches before pushing and always communicate changes to the team. This exercise reinforced that Git is not just about commands—it’s about collaboration, safety, and maintaining integrity in workflows.  

---

## ✅ Self-Assessment
| Topic                | Confidence (1-5) | Notes                                  |
|----------------------|-------------------|----------------------------------------|
| Amend commits        | 5                | Comfortable with `--amend`            |
| Interactive rebase   | 4                | Practiced fixup, reword, squash       |
| Rebasing branches    | 4                | Learned linear history vs merge       |
| Risk management      | 4                | Understand safe workflows             |
| Force push options   | 4                | Prefer `--force-with-lease`           |

---

## 🔗 Evidence
- Outcome branch: https://github.com/asmajabr/taller-master-ugr/tree/i-have-nogroup-outcomes/master
- Screenshots: <img width="1128" height="570" alt="reword" src="https://github.com/user-attachments/assets/49ed13ff-a067-4672-99d2-8232bb2ea8c8" />
<img width="999" height="268" alt="rebase2" src="https://github.com/user-attachments/assets/266150e7-dd59-4ea4-87f3-4a179b82e2b0" />
<img width="909" height="184" alt="rebase_history" src="https://github.com/user-attachments/assets/23bf37a0-bcda-4576-b320-0031b2f2fb7b" />
<img width="1050" height="229" alt="rebase_branch2" src="https://github.com/user-attachments/assets/afdfb357-af41-4cd9-87f5-d8d6fd770d89" />
<img width="1039" height="428" alt="rebase_branch" src="https://github.com/user-attachments/assets/3e2e4977-6e07-4ed2-af83-fffed3ab08f2" />
<img width="818" height="521" alt="rebase" src="https://github.com/user-attachments/assets/f21116b5-17cf-4d97-b01c-92e0ce28bf31" />
<img width="1058" height="394" alt="gitlog_" src="https://github.com/user-attachments/assets/fef2dcec-b2ed-4da6-ae9d-3ca6e3f951e8" />
<img width="1120" height="692" alt="gitlog" src="https://github.com/user-attachments/assets/ac93c3d9-206f-4fbb-9d25-c53c4e65f2b4" />
<img width="1058" height="394" alt="examine_sha" src="https://github.com/user-attachments/assets/f17d94d5-b9c2-4003-aa3e-3ca8b048b047" />
<img width="1136" height="604" alt="commands_history2" src="https://github.com/user-attachments/assets/cb29a2e2-119c-4c3c-af59-29b875551032" />
<img width="1053" height="707" alt="commands_history" src="https://github.com/user-attachments/assets/0026fcbf-2e49-4dde-b201-bbeb3f8ceb8f" />


✅ Ready for Review.
