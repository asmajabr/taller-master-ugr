# Exercise Outcomes Submission

**Student/Group Name**: ASMA JARADAT, Individual (virtual mode, i have no group)
**Level Completed**: master-of-the-universe
**Date**: 2026-01-03

---

## 📋 Exercise Summary

### Exercise: Git Advanced Workflow & Security
**Status**: ✅ Completed

**What I did**:
Completed all parts (1–5):
- Configured branch protection rules on `main`.
- Created feature branch and PR workflow.
- Implemented GPG commit signing and verified on GitHub.
- Reviewed `.gitignore` for sensitive patterns.
- Scanned history for secrets and large files.
- accomplished security audit and documented best practices.

**All Commands I Used**:
```bash
git checkout master-of-the-universe
git checkout -b feature/protected-workflow
git add workflow.txt
git commit -S -m "feat: Add workflow documentation"
git push origin feature/protected-workflow
git checkout main
git pull origin main
echo "test" > direct-push.txt
git add direct-push.txt
git commit -m "Attempting direct push"
git push origin main  # This should fail if protections are active!
git checkout master-of-the-universe
git checkout -b feature/protected-workflow
echo "Proper workflow following branch protection" > workflow.txt
git add workflow.txt
git commit -S -m "feat: Add workflow documentation"
git push origin feature/protected-workflow
git checkout feature/protected-workflow
git log --oneline --decorate --graph --left-right --cherry-pick origin/main...HEAD
clear
gpg --full-generate-key
gpg --list-secret-keys --keyid-format=long
gpg --armor --export  F76A5FB3A01DC002A4858D6940E49CED14881D32
git config --global user.signingkey F76A5FB3A01DC002A4858D6940E49CED14881D32
git config --global commit.gpgsign true
gpg --edit-key 1C6298A4EB3B4BD5
echo "Signed commit test 1" > signed-1.txt
git add signed-1.txt
git commit -S -m "feat: Add first signed commit"
echo "Signed commit test 2" > signed-2.txt
git add signed-2.txt
git commit -S -m "feat: Add second signed commit"
git log --show-signature -2
git push origin feature/protected-workflow
git push --force-with-lease origin feature/protected-workflow
git status
git add .
git commit -m 'add print screens'
git push origin feature/protected-workflow
git fetch origin
git pull --rebase origin feature/protected-workflo
git pull --rebase origin feature/protected-workflow
git push --force-with-lease origin feature/protected-workflow
git log -p | grep -i "password\|api_key\|secret\|token"
git log -p | grep -i "password\|api_key\|secret\|token" | head -20
git rev-list --objects --all |   git cat-file --batch-check='%(objecttype) %(objectname) %(objectsize) %(rest)' |   sed -n 's/^blob //p' |   sort --numeric-sort --key=2 |   tail -n 10
git add .
git commit -m  'last commit to upload all pics to include in outcomes.md'
git push origin feature/workflow
git push origin feature/protected-workflow
git checkout master-of-the-universe
git checkout -b i-have-nogroup-outcomes/master-of-the-universe
git checkout main -- OUTCOME_TEMPLATE.md
cp OUTCOME_TEMPLATE.md OUTCOMES.md

# GPG setup
gpg --full-generate-key
gpg --list-secret-keys --keyid-format=long
gpg --armor --export F76A5FB3A01DC002A4858D6940E49CED14881D32
git config --global user.signingkey F76A5FB3A01DC002A4858D6940E49CED14881D32
git config --global commit.gpgsign true

# Signed commits
git commit -S -m "feat: Add signed commit"

# Secret detection
git log -p | grep -i "password\|api_key\|secret\|token" | head -20

# Large file scan
git rev-list --objects --all |   git cat-file --batch-check='%(objecttype) %(objectname) %(objectsize) %(rest)' |   sed -n 's/^blob //p' |   sort --numeric-sort --key=2 |   tail -n 10
```

**Results/Output**:
```text
# Secret scan result:
Matches found only in README text, no actual secrets.
![secret](image.png)

# Large file scan result:
Largest files are PNG screenshots (60–85 KB), no sensitive data.
![largeFiles](image-1.png)
```

**Screenshots**:
- PR1.PNG: Branch protection settings
- PR2.PNG: Pull Request creation
- PR_REVIEW.PNG: Review required
- PR_MERGE.PNG: Successful merge
- gitlog.PNG: Verified commits
- GitHub security settings screenshot

---

## 🎯 Key Learnings
**Main concepts I learned**:
1. How branch protection enforces secure workflows.
2. Secret management strategies and GitHub security features.
3. Why GPG signing prevents impersonation.

**Skills I improved**:
- Configuring secure Git workflows.
- Using GPG for commit signing.
- Auditing repositories for sensitive data.

---

## 🚧 Challenges Faced
### Challenge 1: Push rejected due to remote changes
**Problem**: Remote branch had commits I didn’t have locally (due to the pull request I tried from that branch to to main)
**Solution**: Used `git fetch` and `git pull --rebase` to integrate changes and pushed using --force-with-lease
**Commands**:
```bash
git fetch origin
git pull --rebase origin feature/protected-workflow
git push --force-with-lease origin feature/protected-workflow

```

### Challenge 2: SSH and GPG setup
**Problem**: Initial SSH key not loaded, GPG key not recognized.
**Solution**: Started ssh-agent, added key, configured GPG signing.

---

## 💬 Personal Reflection
**What surprised me**: How strict branch protection and signed commits are in enterprise workflows.
**What I found most difficult**: Resolving push rejections and configuring GPG correctly.
**What I found most useful**: Verified badge and GitHub security features.
**How I would apply this in real projects**: Enforce signed commits, branch protection, and secret scanning in CI/CD pipelines.

---

## 📊 Self-Assessment
| Topic | Confidence (1-5) | Notes |
|-------|------------------|-------|
| Basic Git commands | 5 | Confident |
| Branching & merging | 5 | Confident |
| Remote operations | 5 | Confident |
| Conflict resolution | 4 | Learned rebase |
| History rewriting | 4 | Understand filter-repo |
| Git hooks | 3 | Basic knowledge |
| Security practices | 5 | GPG, secret scanning |

---

## 🔗 Evidence/Artifacts
- Branch: `feature/protected-workflow`
- Key commits: Signed commits with Verified badge
- Additional files: OUTCOMES.md, screenshots

---

## ✅ Completion Checklist
- [✅] Completed all parts
- [✅] Documented commands and outputs
- [✅] Added screenshots
- [✅] Reflection and self-assessment
- [✅] Pushed outcome branch

---

## 📝 Additional Comments
This exercise was challenging but valuable for mastering secure Git workflows.

**Submission Date**: 2026-01-03
**Ready for Review**: ✅ Yes
