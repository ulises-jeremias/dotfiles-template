# 🚀 Template Setup Guide

This guide will help you set up your own personalized dotfiles using this template repository.

## 📋 Prerequisites

- **Linux Distribution**: Arch Linux (preferred) or Debian-based distros
- **Git**: For cloning and managing your dotfiles
- **Chezmoi**: Will be installed automatically during setup

## 🔧 Quick Setup

### 1. Fork This Repository

1. Go to [this repository](https://github.com/ulises-jeremias/dotfiles-template)
2. Click the "Fork" button to create your own copy
3. Clone your forked repository:

```bash
git clone https://github.com/<your-username>/dotfiles-template ~/.dotfiles
cd ~/.dotfiles
```

### 2. Run the Installation Script

```bash
chmod +x install.sh
./install.sh
```

The installer will:

- Install chezmoi if not present
- Prompt you for personal information (name, email)
- Ask about enabling personal configurations
- Set up the dotfiles framework

### 3. Configure Personal Settings

During the installation, you'll be prompted for:

- **Full Name**: Used in git config and templates
- **Email Address**: For git commits and personal configs
- **Personal Mode**: Enable if you want to use SSH keys and credentials
- **Docker**: Whether to install Docker-related configurations
- **Hardware Type**: For graphics drivers and specific optimizations

### 4. Personalize Repository References (Recommended)

To make the template fully yours and have independent documentation, replace all references to the original repository and author:

#### Replace Repository URLs

```bash
# Replace repository URLs in all files
find ~/.dotfiles -type f \( -name "*.md" -o -name "*.sh" -o -name "*.yml" -o -name "*.csv" -o -name "*.toml" \) \
  -exec sed -i 's|ulises-jeremias/dotfiles-template|YOUR_USERNAME/YOUR_REPO_NAME|g' {} \;

# Example: if your repo is "john-doe/my-dotfiles"
find ~/.dotfiles -type f \( -name "*.md" -o -name "*.sh" -o -name "*.yml" -o -name "*.csv" -o -name "*.toml" \) \
  -exec sed -i 's|ulises-jeremias/dotfiles-template|john-doe/my-dotfiles|g' {} \;
```

#### Replace Author Information

```bash
# Replace author name in documentation and scripts
find ~/.dotfiles -type f \( -name "*.md" -o -name "*.sh" \) \
  -exec sed -i 's|Ulises Jeremias Cornejo Fandos|YOUR_FULL_NAME|g' {} \;

find ~/.dotfiles -type f \( -name "*.md" -o -name "*.sh" \) \
  -exec sed -i 's|ulises-jeremias|YOUR_USERNAME|g' {} \;

# Example replacements
find ~/.dotfiles -type f \( -name "*.md" -o -name "*.sh" \) \
  -exec sed -i 's|Ulises Jeremias Cornejo Fandos|John Doe|g' {} \;

find ~/.dotfiles -type f \( -name "*.md" -o -name "*.sh" \) \
  -exec sed -i 's|ulises-jeremias|john-doe|g' {} \;
```

#### Update Email References

```bash
# Replace email in documentation (optional)
find ~/.dotfiles -type f \( -name "*.md" -o -name "*.sh" \) \
  -exec sed -i 's|ulisescf\.24@gmail\.com|your-email@domain.com|g' {} \;
```

#### Update Project Name (Optional)

```bash
# If you want to rename the project from HorneroConfig
find ~/.dotfiles -type f \( -name "*.md" -o -name "*.sh" \) \
  -exec sed -i 's|HorneroConfig|YourProjectName|g' {} \;
```

> [!TIP]
> After making these changes, commit them to your repository:
>
> ```bash
> cd ~/.dotfiles
> git add .
> git commit -m "Personalize repository references and documentation"
> git push
> ```

.

> [!NOTE]
> These changes will make your documentation completely independent from the original repository. You can then enable GitHub Pages or wiki on your own repository to host the documentation.

## Setting Up Your Own Documentation

After personalizing the repository references, you can set up your own independent documentation:

### Enable GitHub Pages

1. **Go to your repository settings** on GitHub
2. **Navigate to Pages section**
3. **Select source**: Deploy from a branch
4. **Choose branch**: `main` and folder `docs/`
5. **Save** - Your documentation will be available at `https://YOUR_USERNAME.github.io/YOUR_REPO_NAME`

### Enable GitHub Wiki

1. **Go to your repository settings**
2. **Check "Wikis"** in the Features section
3. **Copy wiki content** from the `docs/wiki/` folder to your new wiki pages

### Customize Documentation

You can now freely modify:

- Project name and branding
- Add your own screenshots and examples
- Document your personal customizations
- Remove sections you don't use

### Quick Reference: What to Replace

Here's a quick checklist of what you might want to personalize:

| Original                            | Replace With              | Where Found                 |
| ----------------------------------- | ------------------------- | --------------------------- |
| `ulises-jeremias/dotfiles-template` | `your-username/your-repo` | All documentation, scripts  |
| `Ulises Jeremias Cornejo Fandos`    | `Your Full Name`          | License, copyright headers  |
| `ulisescf.24@gmail.com`             | `your-email@domain.com`   | Contact information         |
| `HorneroConfig`                     | `YourProjectName`         | Project branding (optional) |
| `ulises-jeremias`                   | `your-username`           | GitHub references           |

> **⚠️ Important**: Always test your dotfiles in a safe environment (like the playground) after making these changes to ensure everything still works correctly.

## �🔐 Setting Up Credentials (Optional)

If you enabled personal mode, you can set up your credentials:

### SSH Keys

1. Generate your SSH keys (if you don't have them):

    ```bash
    ssh-keygen -t rsa -b 4096 -C "your-email@domain.com"
    ```

2. Add your keys to the template:

    ```bash
    # Edit the SSH key files
    chezmoi edit ~/.ssh/personal_rsa
    chezmoi edit ~/.ssh/bitbucket_rsa

    # Apply changes
    chezmoi apply
    ```

### API Keys

Set up API keys for services you use:

```bash
# GitHub API token for notifications
chezmoi edit ~/.config/credentials/github_access_token_notifications

# OpenAI API key (for shell-gpt)
chezmoi edit ~/.config/credentials/openai_api_key_for_dotfiles

# Apply changes
chezmoi apply
```

## 🎨 Customization

### Themes and Rice Configurations

Browse available themes:

```bash
dots rice-selector
```

Change themes:

```bash
dots rice <theme-name>
```

### Personal Aliases

Add your personal aliases:

```bash
chezmoi edit ~/.zsh_aliases
chezmoi apply
```

### Window Manager Preferences

The template supports multiple window managers:

- **i3**: Tiling window manager
- **Openbox**: Lightweight stacking WM
- **XFCE4**: Full desktop environment

Configure during installation or change later with:

```bash
dots config-manager
```

## 📝 Maintaining Your Dotfiles

### Adding New Files

```bash
# Add a new config file to chezmoi
chezmoi add ~/.config/new-app/config

# Edit the file
chezmoi edit ~/.config/new-app/config

# Apply changes
chezmoi apply
```

### Updating from Template

To get updates from the original template:

```bash
# Add the original template as upstream
git remote add upstream https://github.com/ulises-jeremias/dotfiles-template

# Fetch updates
git fetch upstream

# Merge non-personal changes (be careful here)
git merge upstream/main
```

### Syncing Across Machines

```bash
# On your first machine, push changes
chezmoi cd
git add .
git commit -m "Update configurations"
git push

# On other machines, pull changes
chezmoi cd
git pull
cd -
chezmoi apply
```

## 🛠️ Troubleshooting

### Installation Issues

1. **Permission denied**: Make sure install.sh is executable

   ```bash
   chmod +x install.sh
   ```

2. **Chezmoi not found**: Install manually

   ```bash
   sh -c "$(curl -fsLS get.chezmoi.io)"
   ```

3. **Missing dependencies**: Run the dependency installer

   ```bash
   ~/.local/bin/dots-dependencies
   ```

### Configuration Issues

1. **SSH keys not working**: Check permissions

   ```bash
   chmod 700 ~/.ssh
   chmod 600 ~/.ssh/*_rsa
   chmod 644 ~/.ssh/*.pub
   ```

2. **API services not working**: Verify your API keys are correctly set

   ```bash
   cat ~/.config/credentials/github_access_token_notifications
   ```

### Getting Help

- 📖 [Full Documentation](https://github.com/ulises-jeremias/dotfiles-template/wiki)
- 🐛 [Report Issues](https://github.com/ulises-jeremias/dotfiles-template/issues)
- 💬 [Discussions](https://github.com/ulises-jeremias/dotfiles-template/discussions)

## 🔄 Next Steps

After setup:

1. **Explore the tools**: Run `dots` to see all available commands
2. **Customize themes**: Use `dots rice-selector` to find your style
3. **Set up security**: Run `dots security-audit` for security recommendations
4. **Configure services**: Set up your preferred password manager, cloud sync, etc.

Welcome to your new dotfiles setup! 🎉
