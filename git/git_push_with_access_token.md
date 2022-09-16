# get a access token
**in GitHub**

Settings -> Developer settings

# Git push with access token

```zsh
git push https://<GITHUB_ACCESS_TOKEN>@github.com/<GITHUB_USERNAME>/<REPOSITORY_NAME>.git
```

# Add a token to zsh environment valuable
```zsh
export GITHUB_TOKEN="ghp_0102..."
```

# Add a token to local
> [^1] You can use secrets.GITHUB_TOKEN as a password on your repository URL. So you might add this before your git push line:

```zsh
git remote set-url --push origin https://your_username:$GITHUB_TOKEN@github.com/your/repo
```

[^1]: [push-to-origin-from-github-action](https://stackoverflow.com/questions/57921401/push-to-origin-from-github-action)

