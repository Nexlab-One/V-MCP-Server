# Updating V Language and V UI Repositories

This repository includes both the V language repository and the V UI repository as a submodule. Here's how to keep both up to date.

## Initial Setup

If you just cloned this repository, initialize the submodules:

```bash
git submodule update --init --recursive
```

## Updating V Language Repository

The V language repository is the main repository. To update it from upstream:

```bash
# Fetch from upstream
git fetch upstream

# Merge upstream changes
git merge upstream/master

# Or use pull if you prefer
git pull upstream master
```

## Updating V UI Submodule

To update the V UI submodule to the latest version:

```bash
# Navigate to the submodule
cd v-ui

# Fetch and update to latest
git fetch origin
git checkout master
git pull origin master

# Go back to main repo
cd ..

# Commit the submodule update
git add v-ui
git commit -m "Update v-ui submodule to latest"
```

## Updating Both Repositories

To update both repositories at once:

```bash
# Update V language repo
git fetch upstream
git merge upstream/master

# Update V UI submodule
cd v-ui
git fetch origin
git checkout master
git pull origin master
cd ..

# Commit both updates
git add v-ui
git commit -m "Update V language and V UI to latest"
```

## Automated Update Script

You can create a simple script to automate this:

```bash
#!/bin/bash
# update-repos.sh

echo "Updating V language repository..."
git fetch upstream
git merge upstream/master

echo "Updating V UI submodule..."
cd v-ui
git fetch origin
git checkout master
git pull origin master
cd ..

echo "Staging changes..."
git add v-ui

echo "Done! Review changes with 'git status' and commit when ready."
```

## Verifying Updates

After updating, verify the MCP server can access the new content:

```bash
cd v-mcp-server
python -c "import main; config = main.VServerConfig.from_env(); server = main.VDocumentationServer(config); print('V examples:', len(server.get_examples_list())); print('V UI examples:', len(server.get_v_ui_examples_list()))"
```

## Troubleshooting

### Submodule is empty
If the `v-ui` directory is empty:

```bash
git submodule update --init --recursive
```

### Submodule shows as modified
If git shows the submodule as modified but you haven't changed it:

```bash
# This usually means the submodule is on a different commit
cd v-ui
git status
# If you want to reset to the committed version:
git checkout <commit-hash>
cd ..
```

### MCP server can't find V UI
If the MCP server reports V UI is not available:

1. Check that the submodule is initialized:
   ```bash
   git submodule status
   ```

2. Verify the path exists:
   ```bash
   ls -la v-ui/examples
   ```

3. Check the server configuration:
   ```bash
   cd v-mcp-server
   python -c "import main; config = main.VServerConfig.from_env(); print('V UI Path:', config.v_ui_path)"
   ```
