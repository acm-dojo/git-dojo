# Git Dojo

An interactive learning environment for mastering Git version control system and collaboration skills.

The Git Dojo provides a comprehensive, hands-on approach to learning essential version control concepts through practical challenges. Students progress through modules covering everything from basic repository management to advanced collaboration workflows.

## 🏗️ Structure

The dojo is defined by [dojo.yml](./dojo.yml) and consists of progressive modules:

### 📚 Modules and Challenges

#### 1. **Local Repository Management** (`local`)
- **init** - Initialize a Git repository (`git init`)
- **commit** - Stage and commit changes (`git add`, `git commit`)

#### 2. **Remote Repository Interaction** (`remote`)
- **clone** - Clone repositories (`git clone`)
- **sync** - Push and pull changes (`git pull`, `git push`)

#### 3. **Good Git Practices** (`good-practices`)
- **ignore** - Ignore files with `.gitignore`
- **branch** - Work with branches (`git branch`, `git checkout`)
- **reset** - Time travel with Git (`git reset`)

#### 4. **Troubleshooting** (`troubleshooting`)
- **undo-commit** - Undo local commits (`git reset HEAD~1`)
- **fix-force-push** - Fix force push issues (`git reset --hard`, `git push --force`)

### Content Modules
Educational content is organized in `core/contents/` following Git workflow progression:
- **local.init** - Repository initialization
- **local.commit** - Staging and committing changes
- **remote.clone** - Cloning repositories
- **remote.sync** - Pushing and pulling changes
- **good-practices.ignore** - Using .gitignore
- **good-practices.branch** - Branch management
- **good-practices.reset** - Git time travel
- **troubleshooting.undo-commit** - Undoing commits
- **troubleshooting.fix-force-push** - Fixing force push issues

## 📖 Curriculum Overview

Refer to [WHAT_TO_TEACH.md](https://github.com/acm-dojo/git-dojo-core/blob/main/WHAT_TO_TEACH.md) for more details.