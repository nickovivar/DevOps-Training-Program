# Playbook

## Example 1 - Set name of the play

```
-
  name: "Execute the uptime command on localhost"
  hosts: localhost
  tasks:
    -
      name: Execute the uptime command
      command: uptime
```

## Example 2 - Define a task
## Example 3 - Add another task
## Example 4 - Change the host
## Example 5 - Use inventory file
## Example 6 - Run different tasks in many servers
## Example 7 - Run many tasks in a defined order

