# HyDE Custom Branch Workflow

Below is a concise Git workflow in English for creating and maintaining a custom branch of the HyDE repository, while keeping up-to-date with the original upstream changes. Feel free to add or adjust commands as needed.

```bash
# 1. Clone the original HyDE repository
git clone git@github.com:HyDE-Project/HyDE.git
cd hyde

# 2. Add the original repo as an 'upstream' remote
git remote add upstream git@github.com:0xGeN02/HyDE.git

# 3. Verify your remotes
git remote -v
# origin  https://github.com/yourname/hyde.git (fetch)
# origin  https://github.com/yourname/hyde.git (push)
# upstream  https://github.com/username/hyde.git (fetch)
# upstream  https://github.com/username/hyde.git (push)

# 4. Create and switch to your custom branch
git checkout -b xgen0_home

# 5. Make your local changes
# e.g., edit Configs/.hyde.zshrc to adjust startup scripts

# 6. Commit your changes
git add Configs/.hyde.zshrc
git commit -m "Customize HyDE startup configuration"

# 7. Push your branch to your fork (origin)
git push -u origin xgen0_home

# --- Regular update steps ---

# 8. Fetch upstream changes
git fetch upstream

# 9. Merge upstream/master into your custom branch
git checkout xgen0_home
git merge upstream/master

# 10. Resolve any merge conflicts, then commit
# (edit conflicted files, then:)
git add <resolved-files>
git commit

# 11. Push updated custom branch
git push

# 12. (Optional) Keep your local master in sync
git checkout master
git pull upstream master

# 13. (Optional) Clean up stale branches locally
git branch -d weather
git branch -d list

# 14. (Optional) Automate upstream updates with an alias
# Add the following to your ~/.gitconfig under [alias]:
#   update-hyde = !git fetch upstream && git checkout xgen0_home && git merge upstream/master && git push
```

## Tips & Extras

- **Stashing local work**: If you have uncommitted changes when updating:

  ```bash
  git stash save "WIP: my local tweaks"
  git fetch upstream
  git merge upstream/master
  git stash pop
  ```

- **Rebasing instead of merging**: For a linear history:

  ```bash
  git checkout xgen0_home
  git fetch upstream
  git rebase upstream/master
  git push --force-with-lease
  ```

- **Dotfile management**: Consider using [GNU Stow](https://www.gnu.org/software/stow/) to manage personal config files outside the repo.

- **Deleting remote branches**: When a feature branch is done or stale:

  ```bash
  git push origin --delete feature-branch
  ```

With this setup, you’ll maintain a clean custom branch (`xgen0_home`) with your personal tweaks, while seamlessly pulling in updates from the official HyDE repository.
