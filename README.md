# Intervene


## Step 1: Set up Git Repository

In your local file system:

1. Create and enter directory for project

```
> mkdir IV1
> cd IV1
```

2. Create Git repo, add README.md
```
> git init
> echo "# Intervene" >> README.md
> git add README.md
> git commit -m "initial commit"
```

3. Connect to remote, push updates
```
> git remote add origin [SSH/HTTPS address]
> git push -u origin main
```

## Step 2: Create Docker Container

