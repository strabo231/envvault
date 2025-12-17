[![Test EnvVault](https://github.com/strabo231/envvault/actions/workflows/test.yml/badge.svg)](https://github.com/strabo231/envvault/actions/workflows/test.yml)

# EnvVault - Secure Environment Variable Manager

Stop committing secrets! EnvVault securely manages environment variables across dev, staging, and production.

## Why EnvVault?

**The Problem:** .env files everywhere
- .env, .env.local, .env.production, .env.staging...
- Accidentally commit secrets to git
- Hard to sync across machines
- No audit trail
- Team collaboration nightmare

**The Solution:** Centralized, encrypted vault
- One vault, multiple environments
- Never commit secrets
- Easy switching between environments
- Audit log of all changes
- Export .env files on demand

## Installation

```bash
curl -sSL https://raw.githubusercontent.com/strabo231/envvault/main/install.sh | bash
```

**Requirements:**
```bash
# Ubuntu/Debian
sudo apt install jq

# macOS
brew install jq
```

## Quick Start

```bash
# Initialize vault
envvault init

# Set variables
envvault set DATABASE_URL "postgres://..." --env prod
envvault set API_KEY "secret-key" --env dev

# List variables
envvault list --env dev

# Export to .env
envvault export --env prod > .env

# Switch environment
envvault use prod
```

## Commands

```
init                Initialize vault
set <key> <value>   Store variable
get <key>           Retrieve variable
list                List all variables
export              Generate .env file
import <file>       Import .env file
use <env>           Switch environment
envs                List environments
search <query>      Search variables
audit               Show audit log
```

## Features

🔐 **Encrypted storage** - Variables stored securely  
🎯 **Multiple environments** - dev, staging, prod, custom  
🔄 **Easy switching** - One command to change envs  
📤 **Export to .env** - Generate files on demand  
📥 **Import existing** - Migrate from .env files  
🔍 **Search** - Find variables quickly  
📊 **Audit log** - Track all changes  
⚠️ **Never commit** - Vault stays local  

## Usage

**Initialize vault:**
```bash
envvault init
```

**Set variables:**
```bash
envvault set DATABASE_URL "postgres://localhost/mydb" --env dev
envvault set API_KEY "dev-key-123" --env dev
envvault set API_KEY "prod-key-456" --env prod
```

**List variables:**
```bash
envvault list --env dev
```
```
═══════════════════════════════════════════════════════════════
           ENVIRONMENT: DEV
═══════════════════════════════════════════════════════════════

KEY                            VALUE
────────────────────────────────────────────────────────────────
DATABASE_URL                   postgres://localhost/mydb
API_KEY                        dev-key-123

ℹ 2 variables in dev
```

**Get specific variable:**
```bash
envvault get DATABASE_URL --env dev
```

**Export to .env:**
```bash
envvault export --env prod > .env
```

**Import existing .env:**
```bash
envvault import .env.local --env dev
```

**Switch environment:**
```bash
envvault use prod
envvault list  # Now shows prod variables
```

**Search:**
```bash
envvault search "API" --env dev
```

## Use Cases

**Development Workflow:**
```bash
# Set up dev environment
envvault set DATABASE_URL "postgres://localhost/dev" --env dev
envvault set REDIS_URL "redis://localhost" --env dev

# Work on dev
envvault use dev
envvault export > .env

# Switch to staging
envvault use staging
envvault export > .env
```

**Team Onboarding:**
```bash
# New dev gets vault file
envvault init
envvault import team-config.env --env dev
envvault export --env dev > .env
```

**CI/CD:**
```bash
# Generate production .env in CI
envvault export --env prod > .env
```

**Migration:**
```bash
# Import existing .env files
envvault import .env.development --env dev
envvault import .env.production --env prod
```

## Security

**What's encrypted:**
- All variable values
- Vault file: `~/.envvault/vault.json`

**What's NOT encrypted:**
- Variable names (keys)
- Environment names

**Best practices:**
- Never commit `~/.envvault/` to git
- Add to .gitignore: `.envvault/`
- Back up vault file securely
- Rotate keys regularly

## Audit Log

Track all vault operations:

```bash
envvault audit
```
```
2024-12-15 10:23:45 | SET    | dev  | API_KEY
2024-12-15 10:24:12 | GET    | dev  | DATABASE_URL
2024-12-15 10:25:33 | EXPORT | prod | all
```

## Comparison

| Feature | .env files | EnvVault |
|---------|-----------|----------|
| Multiple envs | Multiple files | One vault |
| Security | Plain text | Encrypted |
| Switching | Manual | One command |
| Audit trail | None | Built-in |
| Team sync | Git (unsafe!) | Encrypted file |
| Search | grep | Built-in |

## Requirements

- Bash 4.0+
- jq (JSON processor)

## License

MIT License

## Author

Sean - [@strabo231](https://github.com/strabo231)

---

**Manage secrets. Stay secure. Sleep well.** 🔐
