# g1_ros2

Unitree G1（29 自由度モデル）を ROS 2 Humble + MoveIt 2 で扱うためのパッケージ集。
Path Reuse 法の多関節検証（両腕 14 関節、腰込み上半身 17 関節）に使う。

| パッケージ | 由来 | 内容 |
|---|---|---|
| `g1_description` | [isri-aist/g1_description](https://github.com/isri-aist/g1_description)（main、git subtree で取り込み） | URDF（`g1_29dof.urdf`, `g1_23dof.urdf`）とメッシュ |
| `g1_moveit_config` | [ravijo/g1_moveit_config](https://github.com/ravijo/g1_moveit_config)（main、git subtree で取り込み） | MoveIt 2 設定。上流は `right_arm` / `left_arm`（各 7 関節）のみ |

このリポジトリで加えたもの（`g1_moveit_config`）:
- `config/g1_29dof.urdf.xacro`, `config/g1_29dof.ros2_control.xacro`: 両腕 14 ＋ 腰 3 関節を `mock_components/GenericSystem` で動かす ros2_control。脚は固定
- `config/ros2_controllers.yaml`, `config/moveit_controllers.yaml`: `waist_controller` を追加
- `config/g1_29dof.srdf`: planning group `both_arms`（14）、`waist`（3）、`upper_body`（17）を追加
- `.setup_assistant`: URDF を上の xacro に変更

## 起動

```bash
colcon build --symlink-install --packages-select g1_description g1_moveit_config
source install/setup.bash
ros2 launch g1_moveit_config demo.launch.py
```

ライセンスは各パッケージの LICENSE に従う（いずれも BSD）。
