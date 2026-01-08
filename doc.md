# test

{% raw %}
```scss

// .vscode/tasks.json 
{{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "Git: switch → pub",
      "type": "shell",
      "command": "zsh -lc 'git switch pub'",
      "group": "git",
      "problemMatcher": []
    },

    {
      "label": "Git: switch → feature/S09126",
      "type": "shell",
      "command": "zsh -lc 'git switch feature/S09126'",
      "group": "git",
      "problemMatcher": []
    },

    {
      "label": "Git: merge ← origin/pub",
      "type": "shell",
      "command": "zsh -lc 'git merge origin/pub'",
      "group": "git",
      "problemMatcher": []
    },

    {
      "label": "Git: merge ← origin/feature/S09126",
      "type": "shell",
      "command": "zsh -lc 'git merge origin/feature/S09126'",
      "group": "git",
      "problemMatcher": []
    },

    {
      "label": "Git: push → feature/S09126",
      "type": "shell",
      "command": "zsh -lc 'git push -u origin feature/S09126'",
      "group": "git",
      "problemMatcher": []
    }
  ]
}

```
{% endraw %}

---
