# test

{% raw %}
```scss

// .vscode/tasks.json 
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "Git: switch → pub",
      "type": "shell",
      "command": "zsh -lc 'git switch pub'",
      "problemMatcher": [],
      "group": "git",
      "presentation": {
        "reveal": "always",
        "panel": "shared",
        "focus": true
      }
    },

    {
      "label": "Git: switch → feature (prompt)",
      "type": "shell",
      "command": "zsh -lc 'read -r \"ticket?Ticket (ex: S09126): \"; git switch \"feature/${ticket}\"'",
      "problemMatcher": [],
      "group": "git",
      "presentation": {
        "reveal": "always",
        "panel": "shared",
        "focus": true
      }
    },

    {
      "label": "Git: merge ← origin/pub",
      "type": "shell",
      "command": "zsh -lc 'git merge origin/pub'",
      "problemMatcher": [],
      "group": "git",
      "presentation": {
        "reveal": "always",
        "panel": "shared",
        "focus": true
      }
    },

    {
      "label": "Git: merge ← origin/feature (prompt)",
      "type": "shell",
      "command": "zsh -lc 'read -r \"ticket?Ticket (ex: S09126): \"; git merge \"origin/feature/${ticket}\"'",
      "problemMatcher": [],
      "group": "git",
      "presentation": {
        "reveal": "always",
        "panel": "shared",
        "focus": true
      }
    }
  ]
}

```
{% endraw %}

---
