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
      "command": "git switch pub",
      "problemMatcher": [],
      "group": "git"
    },
    {
      "label": "Git: switch → feature (input)",
      "type": "shell",
      "command": "git switch feature/${input:ticket}",
      "problemMatcher": [],
      "group": "git"
    },
    {
      "label": "Git: merge ← origin/pub",
      "type": "shell",
      "command": "git merge origin/pub",
      "problemMatcher": [],
      "group": "git"
    },
    {
      "label": "Git: merge ← origin/feature (input)",
      "type": "shell",
      "command": "git merge origin/feature/${input:ticket}",
      "problemMatcher": [],
      "group": "git"
    }
  ],
  "inputs": [
    {
      "id": "ticket",
      "type": "promptString",
      "description": "사번 입력 (예: S09126)"
    }
  ]
}

```
{% endraw %}

---
