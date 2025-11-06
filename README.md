## Automation of Mirroring to GitLab

> Purpose: To automate the mirroring of a GitHub repository to GitLab using a GitHub Actions
> workflow. Constraints: CLI only, no GUI.

#### Part of the script to create a private repository

```sh
# Prior to this, I run a gitcreate function, structuring the repo
mkrepo(){
  local repo_name=$(dir)
  local gl_url="git@gitlab.com:AnthonySJHenry/${repo_name}.git"
  local gh_url="git@github.com:AnthonySJHenry/${repo_name}.git"
  glab repo create "$repo_name" --private
  git remote add gitlab "$gl_url"
  git push -u gitlab main
  gh repo create "$repo_name" --source=. --private --remote "github"
  gh secret set GL_PAT --body "$GL_PAT"
  git push -u github main
}
```
