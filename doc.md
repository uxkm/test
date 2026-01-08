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



{
  "label": "Git: pub ← feature/S09126 (pull + merge)",
  "type": "shell",
  "command": "zsh -lc 'set -e; git switch pub && git pull && git merge origin/feature/S09126'",
  "group": "git",
  "problemMatcher": []
},
{
  "label": "Git: feature/S09126 ← pub (merge + commit + push)",
  "type": "shell",
  "command": "zsh -lc 'set -e; git switch feature/S09126 && git merge origin/pub && git commit -m \"chore: merge pub into feature/S09126\" || true && git push origin feature/S09126'",
  "group": "git",
  "problemMatcher": []
}
```
{% endraw %}

---
