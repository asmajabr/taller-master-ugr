# taller-master-ugr

A repository to showcase how GitHub works to master students

# Master of the Universe Level Exercise

Welcome to the Master of the Universe level! This expert-level exercise focuses on repository security, branch protection rules, and professional best practices including GPG signing for verified commits.

## Exercise - Branch Protection Rules and Security Best Practices (GPG Signing & Sensitive Data Management)
**Objective**: Implement enterprise-grade branch protection rules and security best practices including GPG-signed verified commits and secure data management.

**Tasks**:

### Part 1: Set Up Branch Protection Rules on GitHub
1. Navigate to your repository on GitHub
2. Go to Settings → Branches → Add branch protection rule
3. Configure protection for the `main` branch:
   * Branch name pattern: `main`
   * ✅ Require a pull request before merging
   * ✅ Require approvals (at least 1)
   * ✅ Dismiss stale pull request approvals when new commits are pushed
   * ✅ Require review from Code Owners (reference the existing CODEOWNERS file)
   * ✅ Require status checks to pass before merging
   * ✅ Require branches to be up to date before merging
   * ✅ Require conversation resolution before merging
   * ✅ Require signed commits (for master-of-the-universe level)
   * ✅ Include administrators (enforce rules on admins too)

4. Review the existing `CODEOWNERS` file in the repository root
5. Understand how code owners are automatically requested for review on PRs

### Part 2: Test Protected Branch Workflow
1. Try to push directly to main (should be blocked if protections are configured on GitHub):
   ```bash
   git checkout main
   git pull origin main
   echo "test" > direct-push.txt
   git add direct-push.txt
   git commit -m "Attempting direct push"
   git push origin main  # This should fail if protections are active!
   ```

2. Proper workflow - create a feature branch and PR:
   ```bash
   git checkout master-of-the-universe
   git checkout -b feature/protected-workflow
   echo "Proper workflow following branch protection" > workflow.txt
   git add workflow.txt
   git commit -S -m "feat: Add workflow documentation"
   git push origin feature/protected-workflow
   ```

3. On GitHub:
   * Create a Pull Request to main
   * Note the required reviews and checks
   * Observe code owner review requests
   * Document the protection rules in action

### Part 3: Set Up GPG Commit Signing for Verified Commits
1. Generate a GPG key:
   * Follow: [Generate GPG key](https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key)
   ```bash
   gpg --full-generate-key
   # Choose: RSA and RSA, 4096 bits, no expiration (or set expiration)
   # Enter your name and email (must match GitHub email)
   ```

2. List your GPG keys:
   ```bash
   gpg --list-secret-keys --keyid-format=long
   ```

3. Export your GPG public key:
   ```bash
   gpg --armor --export YOUR_KEY_ID
   ```

4. Add GPG key to GitHub:
   * Go to GitHub Settings → SSH and GPG keys → New GPG key
   * Paste your public key
   * [Add GPG key to GitHub](https://docs.github.com/en/authentication/managing-commit-signature-verification/adding-a-gpg-key-to-your-github-account)

5. Configure Git to use your GPG key:
   ```bash
   git config --global user.signingkey YOUR_KEY_ID
   git config --global commit.gpgsign true
   ```
   * [Tell Git about signing key](https://docs.github.com/en/authentication/managing-commit-signature-verification/telling-git-about-your-signing-key)

6. Associate email with GPG key:
   * [Associate email with GPG key](https://docs.github.com/en/authentication/managing-commit-signature-verification/associating-an-email-with-your-gpg-key)

7. Make several signed commits:
   ```bash
   echo "Signed commit test 1" > signed-1.txt
   git add signed-1.txt
   git commit -S -m "feat: Add first signed commit"
   
   echo "Signed commit test 2" > signed-2.txt
   git add signed-2.txt
   git commit -S -m "feat: Add second signed commit"
   
   git log --show-signature -2
   ```

8. Push and verify on GitHub (should show "Verified" badge on each commit)

### Part 4: Managing Sensitive Data Securely
1. **Prevention** - Review and enhance `.gitignore`:
   ```bash
   # Ensure .gitignore includes common sensitive patterns:
   # .env files
   # API keys
   # Credentials
   # Private keys (.key, .pem files)
   # etc.
   ```

2. **Detection** - Scan for potential secrets in repository history:
   ```bash
   # Check for sensitive patterns in commit history
   git log -p | grep -i "password\|api_key\|secret\|token" | head -20
   
   # Check for large files that might contain sensitive data
   git rev-list --objects --all | \
     git cat-file --batch-check='%(objecttype) %(objectname) %(objectsize) %(rest)' | \
     sed -n 's/^blob //p' | \
     sort --numeric-sort --key=2 | \
     tail -n 10
   ```

3. **Understanding Remediation** - Know how to remove sensitive data if found:
   * Research `git-filter-repo` or `BFG Repo-Cleaner`
   * Understand the implications of rewriting history
   * Know when to rotate credentials vs. removing from history
   * Document the process even if not performing it

4. **GitHub Security Features** - Enable on your repository:
   * Navigate to Settings → Code security and analysis
   * Review available features:
     - Dependency graph
     - Dependabot alerts
     - Dependabot security updates
     - Secret scanning (if available)
     - Code scanning
   * Enable what's available for your repository

### Part 5: Security Audit and Best Practices
1. Conduct a security review:
   * Audit current repository for security issues
   * Document any findings
   * Review all commits for verification status
   * Check protection rules are working as expected

2. Document security best practices:
   * Why GPG signing prevents impersonation
   * How branch protection supports code quality
   * Why sensitive data should never be committed
   * Best practices for secret management (environment variables, secret vaults)
   * Security in CI/CD pipelines

**Success Criteria**:
- You have configured branch protection rules on GitHub for the main branch
- You understand how CODEOWNERS work and when they're triggered
- You can demonstrate the difference between protected and unprotected workflows
- All your commits are GPG signed and show "Verified" badge on GitHub
- You have configured automatic commit signing in Git
- You have a comprehensive `.gitignore` file preventing sensitive data commits
- You can identify sensitive patterns in repository history
- You understand how to remove sensitive data from Git history (process, not necessarily execution)
- You know when to rotate credentials vs. attempting history cleanup
- Repository security features are enabled where available
- You can articulate security best practices for professional team environments

---

## 📤 Submitting Your Work

### 🌟 Congratulations on Reaching Master of the Universe Level! 🌟

You're demonstrating elite-level Git expertise with enterprise security practices. This final submission showcases your professional readiness.

### Step 1: Create Your Outcome Branch

```bash
git checkout master-of-the-universe
git checkout -b group-X-outcomes/master-of-the-universe
```

### Step 2: Document Your Outcomes

1. **Get the template**:
   ```bash
   git checkout main -- OUTCOME_TEMPLATE.md
   cp OUTCOME_TEMPLATE.md OUTCOMES.md
   ```

2. **Complete comprehensive documentation**:

   **Part 1 - Branch Protection Rules**:
   - Screenshots of GitHub branch protection settings configured
   - Explanation of each protection rule and its purpose
   - Documentation referencing the CODEOWNERS file
   - Evidence of how protections affect workflow
   
   **Part 2 - Protected Workflow Testing**:
   - Demonstration of blocked direct push (screenshot or error message)
   - Feature branch PR workflow documentation
   - GitHub PR interface showing protection requirements
   - Understanding of code owner review process
   
   **Part 3 - GPG Signing Setup**:
   - GPG key generation output (you can redact sensitive parts)
   - GitHub GPG key configuration screenshots
   - Git configuration commands used
   - `git log --show-signature` output showing multiple verified commits
   - GitHub commits showing "Verified" badges (screenshots)
   
   **Part 4 - Sensitive Data Management**:
   - Review of `.gitignore` file ensuring comprehensive coverage
   - Repository history scan for sensitive patterns (output)
   - Documentation of remediation approaches (process understanding)
   - Understanding of when to rotate credentials
   
   **Part 5 - Security Audit and Best Practices**:
   - Security audit findings from your repository
   - GitHub security features enabled (screenshots)
   - Best practices documentation:
     * Why GPG signing prevents impersonation
     * How branch protection supports secure collaboration
     * Secret management best practices

3. **Security-focused challenges**:
   - GPG configuration issues across OS/platforms?
   - Difficulties with commit signing in IDE/editor?
   - Understanding branch protection trade-offs?
   - Challenges scanning for sensitive patterns?
   - Balancing security with developer productivity?

4. **Professional reflection** (minimum 250 words):
   - Why is commit verification critical in enterprise environments?
   - How do branch protection rules prevent security incidents?
   - What's your strategy for secret management in real projects?
   - How would you implement these practices in your organization?
   - What trade-offs exist between security and development velocity?
   - How do these practices integrate with DevSecOps principles?

### Step 3: Package Security Artifacts

Create organized security documentation:

```bash
mkdir security-artifacts
# Export your public GPG key
gpg --armor --export YOUR_KEY_ID > security-artifacts/public-key.asc
# Copy relevant security documentation
echo "Branch Protection Rules applied on GitHub" > security-artifacts/protection-rules.txt
git add security-artifacts/
```

### Step 4: Commit and Push (With GPG Signature!)

```bash
git add OUTCOMES.md security-artifacts/
git commit -S -m "docs: Add master-of-the-universe level exercise outcomes for Group X"
git log --show-signature -1  # Verify your signature
git push origin group-X-outcomes/master-of-the-universe
```

### What to Include

✅ **Part 1 Requirements**:
- Complete branch protection configuration with screenshots
- Explanation of each rule (PR reviews, signed commits, status checks, etc.)
- CODEOWNERS file review and understanding
- Discussion of security vs. workflow balance

✅ **Part 2 Requirements**:
- Evidence of blocked direct push attempt
- Feature branch and PR creation workflow
- GitHub PR interface showing active protections
- Understanding of approval requirements

✅ **Part 3 Requirements**:
- GPG key successfully configured and added to GitHub
- Minimum 5 signed commits showing "Verified" badge on GitHub
- `git log --show-signature` output
- Automatic signing configured in Git
- Public GPG key in security-artifacts/

✅ **Part 4 Requirements**:
- Comprehensive `.gitignore` review
- Repository scan for sensitive patterns (command output)
- Understanding of data remediation approaches
- Documentation of credential rotation best practices

✅ **Part 5 Requirements**:
- Security audit findings and recommendations
- GitHub security features documented
- Best practices guide for team implementation
- Professional security mindset demonstrated

✅ **Security Best Practices Demonstrated**:
- All submission commits are GPG signed
- No secrets in repository (even test/dummy ones)
- Professional `.gitignore` covering common scenarios
- Security-first mindset in all documentation
- Proactive security measures explained

✅ **General Requirements**:
- Professional-quality documentation (250+ word reflection)
- Screenshots of all GitHub configurations
- Complete command history with outputs
- Security artifacts packaged properly
- Self-assessment including security topics
- Clear explanations of security trade-offs

### Evaluation Criteria

| Criterion | Weight | Key Focus for Master of Universe |
|-----------|--------|-----------------------------------|
| Completion | 20% | Exercise completed with all parts and enterprise-grade implementations |
| Understanding | 25% | Deep security knowledge, branch protection policies, GPG signing |
| Practical Skills | 25% | Working GPG signatures, proper protections configured, security tooling |
| Problem-Solving | 20% | Security configuration challenges, policy design decisions |
| **Security Practices** | 10% | Commit signing consistency, secret management, audit capabilities |

**Minimum score to complete training**: 85/100

### Critical Security Topics

🔐 **Commit Signing**:
- Why does commit signing matter for supply chain security?
- What attacks does GPG signing prevent?
- How do you verify someone else's signed commits?
- What happens if you lose your GPG key?

🔐 **Branch Protection**:
- How do protection rules prevent unauthorized changes?
- What's the minimum viable set of protections?
- How do you balance security with emergency fixes?
- What are the limitations of branch protection?

🔐 **Secret Management**:
- Why is removing secrets from history insufficient?
- What's your secret rotation strategy after exposure?
- How do you prevent secrets in commits (pre-commit hooks)?
- What tools help detect secrets in repositories?

🔐 **Security Audit**:
- What are the top security risks in Git repositories?
- How do you conduct a comprehensive security review?
- What GitHub security features are most important?
- How does Git security fit into DevSecOps?

### Excellence Indicators

💎 GPG key configured with expiration and backup plan  
💎 Branch protection rules follow industry best practices  
💎 `.gitignore` includes security-sensitive patterns  
💎 Secret detection automated (pre-commit hooks)  
💎 Comprehensive security audit with prioritized findings  
💎 Documentation includes threat models and mitigations  
💎 All security practices explained with real-world context  

### Common Pitfalls to Avoid

⚠️ Unsigned commits in submission (must be signed!)  
⚠️ Weak or incomplete branch protection rules  
⚠️ Generic `.gitignore` without security focus  
⚠️ Not actually removing sensitive data, just hiding it  
⚠️ GPG key without email matching GitHub  
⚠️ Security theater without understanding the "why"  

### Resources

- Commit signature verification: https://docs.github.com/en/authentication/managing-commit-signature-verification
- Branch protection: https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches
- GitHub security features: https://docs.github.com/en/code-security
- Git-filter-repo: https://github.com/newren/git-filter-repo
- BFG Repo-Cleaner: https://rtyley.github.io/bfg-repo-cleaner/
- OWASP Git Security: https://owasp.org/www-community/attacks/Git

---

## 🎓 Training Completion

**Congratulations!** 🎉 You've completed all levels of Git mastery. You now have the skills to work professionally with Git in enterprise environments, manage complex workflows, and maintain security best practices.

### What You've Achieved

✨ **Newbie**: Mastered Git fundamentals and basic workflows  
✨ **Intermediate**: Conquered merging, conflicts, and collaboration  
✨ **Master**: Mastered history rewriting, branching strategies, and automation  
✨ **Master of Universe**: Achieved enterprise-level security and governance expertise  

### Your Professional Git Portfolio

Your completed outcome branches demonstrate:
- ✅ Technical proficiency across all Git features
- ✅ Problem-solving abilities in complex scenarios
- ✅ Security-first mindset and best practices
- ✅ Professional documentation and communication skills
- ✅ Ready for enterprise Git workflows

### Next Steps

**Continue Learning**:
- 🚀 Practice these skills in real projects
- 🚀 Contribute to open-source projects on GitHub
- 🚀 Learn about GitOps and Infrastructure as Code
- 🚀 Explore CI/CD integration with Git workflows
- 🚀 Study advanced topics: Git LFS, submodules, subtrees
- 🚀 Share your knowledge with others through mentoring

**Professional Development**:
- Add Git expertise to your CV/resume
- Share your learning journey on LinkedIn
- Write blog posts about complex Git topics
- Contribute to Git-related projects or documentation

**Stay Current**:
- Follow Git release notes and new features
- Join Git communities and forums
- Attend conferences or meetups about version control
- Explore emerging tools in the Git ecosystem

---

**Thank you for completing this training!** Your dedication to mastering Git will serve you well in your professional career. 🌟
=======
A Git Training Repository for Master Students at UGR

This repository is designed to help master students develop professional Git skills through hands-on exercises organized by difficulty level.

## 📚 Training Structure

This repository contains exercises across **four difficulty levels**, each in its own branch. You must complete all exercises in each branch before progressing to the next level. After finishing a level, create an outcome branch to document and submit your work for evaluation.

### 🌱 Newbie Level
**Branch**: `newbie`  
**Exercise**: 1  
**Topics**:
- Basic Git commands (init, clone, add, commit, status, log)
- Creating and switching branches
- Basic remote operations (push, pull)

**You MUST start here**: We consider you new to Git or need a refresher on the basics.

```bash
git checkout newbie
```

### 🔧 Intermediate Level
**Branch**: `intermediate`  
**Exercise**: 1  
**Topics**:
- Merging branches and resolving conflicts
- Using tags for releases

**Continue here**: You're now comfortable with basic Git but need to deepen your understanding of collaboration workflows.

```bash
git checkout intermediate
```

### 🎯 Master Level
**Branch**: `master`  
**Exercise**: 1  
**Topics**:
- Rewriting history (rebase, amend commits, interactive rebase)

**Now is time for a level up. Continue here**: You want to master advanced Git techniques used in professional environments.

```bash
git checkout master
```

### 🌟 Master of the Universe Level
**Branch**: `master-of-the-universe`  
**Exercise**: 1  
**Topics**:
- Branch protection rules and secure workflows
- Security best practices (GPG signing, managing sensitive data)
- Verified commits and security auditing

**Now is time for a level up. Continue here**: You want to master advanced Git techniques used in professional environments.

```bash
git checkout master-of-the-universe
```

## 🚀 Getting Started

1. **Clone the repository**:
   ```bash
   git clone git@github.com:miguel-oltra/taller-master-ugr.git
   cd taller-master-ugr
   ```

2. **Choose your level**: Checkout the branch for your skill level
   ```bash
   git checkout <branch-name>
   ```

3. **Read the exercises**: Each branch has a README.md with detailed exercises

4. **Complete the exercises**: Follow the instructions and practice!

## 📖 Additional Resources

- **Git Documentation**: https://git-scm.com/doc
- **Interactive Git Tutorial**: https://learngitbranching.js.org/
- **GitHub Skills**: https://skills.github.com/
- **SSH Setup**: [Configure SSH credentials](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)
- **GPG Setup**: [Managing commit signature verification](https://docs.github.com/en/authentication/managing-commit-signature-verification)

## 💡 Learning Path

We recommend following this progression:

```
Newbie → Intermediate → Master → Master of the Universe
```

However, feel free to jump to any level that matches your current knowledge.

## 🎓 Training Topics Covered

- **Git Key Features**: Local and remote operations, commits, working tree, staging area
- **Branching**: Creation, merging, strategies
- **History Management**: Viewing logs, rewriting history
- **Hooks**: Pre-commit, post-commit, pre-push automation
- **Security**: SSH keys, GPG keys, verified commits
- **Collaboration Workflows**: GitHub Flow, Git Flow, Forking workflow
- **Digital Trends**: GitOps, Infrastructure as Code, CI/CD, DevSecOps

## 📊 Exercise Overview

| Level | Exercise | Time Estimate | Key Skills |
|-------|----------|---------------|------------|
| Newbie | 1 | 1-2 hours | Foundation & basics |
| Intermediate | 1 | 2-3 hours | Collaboration & conflict resolution |
| Master | 1 | 3-4 hours | Advanced techniques & automation |
| Master of the Universe | 1 | 2-3 hours | Security & governance |

## 📤 Submitting Your Work

After completing your exercises, you must submit your work for evaluation by creating an outcome branch.

### Branch Naming Convention

Create a branch following this pattern:
```
group-[X]-outcomes/[level]
```

**Examples**:
- `group-A-outcomes/newbie`
- `group-B-outcomes/intermediate`
- `group-C-outcomes/master`
- `group-D-outcomes/master-of-the-universe`

### Submission Steps

1. **Complete all exercises** in your chosen level branch

2. **Create your outcome branch** from the exercise branch:
   ```bash
   # Example for Group A completing newbie level
   git checkout newbie
   git checkout -b group-A-outcomes/newbie
   ```

3. **Copy and complete the outcome template**:
   ```bash
   cp OUTCOME_TEMPLATE.md OUTCOMES.md
   # Edit OUTCOMES.md with your information
   ```

4. **Document your work** in `OUTCOMES.md`:
   - Summary of each exercise completed
   - Commands used with their outputs
   - Screenshots or logs demonstrating your work
   - Challenges faced and how you solved them
   - Personal reflection on what you learned

5. **Commit your outcome documentation**:
   ```bash
   git add OUTCOMES.md
   git commit -m "docs: Add outcomes for [level] level exercises"
   ```

6. **Push your outcome branch** to the remote:
   ```bash
   git push origin group-A-outcomes/newbie
   ```

7. **Create a Pull Request** (if required by your instructor):
   - Go to the repository on GitHub
   - Create a PR from your outcome branch to `main`
   - Add a clear title: "Outcomes: Group A - Newbie Level"
   - Add any additional comments or questions

### Required Documentation

Your `OUTCOMES.md` file must include:

✅ **Exercise Summaries**: Brief description of what you accomplished  
✅ **Commands & Outputs**: All key commands with their results  
✅ **Evidence**: Screenshots, logs, or commit hashes  
✅ **Challenges**: Problems faced and solutions found  
✅ **Reflection**: What you learned and how you'll apply it  
✅ **Self-Assessment**: Your confidence rating for each topic  

### Evaluation Criteria

Your work will be assessed based on:

1. **Completion of Exercises** (20%) - Did you finish all exercises?
2. **Understanding of Concepts** (25%) - Do you understand the "why" behind commands?
3. **Practical Application** (25%) - Did you use commands correctly and efficiently?
4. **Problem-Solving Skills** (20%) - How well did you handle challenges?
5. **Security Practices** (10%) - For Master of the Universe level only

See `EVALUATION_CRITERIA.md` for detailed rubric.

### Tips for Success

💡 **Be thorough**: Document everything, even small wins  
💡 **Be honest**: Share real challenges, not just successes  
💡 **Be reflective**: Show what you learned, not just what you did  
💡 **Be clear**: Use proper formatting and organization  
💡 **Be professional**: Treat this like a work portfolio  

### Need Help?

- Check the `OUTCOME_TEMPLATE.md` for guidance
- Review `EVALUATION_CRITERIA.md` to understand expectations
- Ask your instructor if you have questions
- Collaborate with your group members

---
## 🤖 Using GenAI Tools to Accelerate Your Learning

### Recommended Approach

#### ✅ Good Uses of AI

- **Explaining concepts**: Ask AI to explain what a command does and why
- **Debugging errors**: Share error messages to understand what went wrong
- **Exploring alternatives**: "What's the difference between rebase and merge?"
- **Reviewing your work**: Ask AI to review your git log and suggest improvements
- **Learning best practices**: "What's a good commit message format?"
- **Understanding documentation**: Have AI explain complex Git documentation

#### ❌ Avoid These Pitfalls

- Copying commands without understanding them
- Having AI complete entire exercises without your participation
- Submitting AI-generated reflections as your own thoughts
- Using AI to skip the learning process entirely

---

## 🤝 Contributing

This is a training repository. Students should:
- Create feature branches for their work
- Practice proper commit messages
- Use Pull Requests for collaboration exercises
- Submit outcomes using the standardized process above

## 📝 License

This repository is for educational purposes as part of the UGR Master's program.

## 👨‍🏫 Instructor

Created for Git Technology training at Universidad de Granada (UGR).

---

**Ready to begin?** Choose your level and checkout the corresponding branch to start learning! 🚀


