# MoveIt Pick — external manipulation skill

This project was previously known as AgenticROS.


Marketplace package for the `pick_object` capability (`external_ros_node` → MoveIt `MoveGroup`).

```bash
npx @corebrum/synapse skills install @corebrum/moveit-pick
# or: chrismatthieu/moveit-pick
```

Corebrum Synapse does **not** launch MoveIt. Bring up your MoveIt2 / MoveGroup stack on the robot (or sim), then install this skill.

Until core adds a MoveGroup goal helper, pass an **explicit `goal`** object matching `moveit_msgs/action/MoveGroup` for your planning group and grasp pose.

## Mission example

```json
{
  "mission": {
    "name": "pick at pose",
    "steps": [
      {
        "id": "pick",
        "capability": "pick_object",
        "inputs": {
          "goal": {
            "request": {
              "group_name": "arm",
              "num_planning_attempts": 5,
              "allowed_planning_time": 5.0
            }
          }
        }
      }
    ]
  }
}
```

Shape the `goal` to your MoveIt config (planning group, end-effector, grasp). The `x` / `y` / `z` input fields are documentation hints only.

## Requirements

- MoveIt MoveGroup advertising `move_action` (`moveit_msgs/action/MoveGroup`)
- Transport with action support (local DDS / rosbridge preferred; Zenoh depends on bridge config)
- Operator-owned MoveIt bringup (`sim-arm` MoveIt2 CI is still WIP)

## Status

| Item | Status |
|------|--------|
| Manifest / npm / marketplace | Shipped |
| `synapse up sim-arm` + MoveIt2 | WIP (joint jogging works; MoveGroup not in sim yet) |
| CI demo | Not claimed |
