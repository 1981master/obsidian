# 1️⃣ Make sure main is up to date
git checkout main
git pull

# 2️⃣ Create your feature branch
git checkout -b feature

# 3️⃣ Do your work + commit many times
git add .
git commit -m "your message"

# 4️⃣ Rebase your feature branch on top of latest main
git fetch origin
git rebase origin/main
# Resolve conflicts if any:
# git add <resolved-files>
# git rebase --continue

# 5️⃣ Push feature branch to remote and set upstream
git push --set-upstream origin feature
# Now git knows:
# feature (local) → origin/feature (remote)

# 6️⃣ Open PR → merge
