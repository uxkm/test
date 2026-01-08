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
      "label": "Git: switch → feature (prompt)",
      "type": "shell",
      "command": "zsh -lc 'read -r \"ticket?Ticket (ex: S09126): \"; git switch \"feature/${ticket}\"'",
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
      "label": "Git: merge ← origin/feature (prompt)",
      "type": "shell",
      "command": "zsh -lc 'read -r \"ticket?Ticket (ex: S09126): \"; git merge \"origin/feature/${ticket}\"'",
      "problemMatcher": [],
      "group": "git"
    }
  ]
}
