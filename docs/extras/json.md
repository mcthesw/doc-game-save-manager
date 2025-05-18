# Json文件说明

## GameSaveManager.config.json

```json5
{
  "version": "1.5.0", // 配置文件的版本
  "backup_path": "./save_data", // 备份文件存放路径，暂时不可变，不要更改
  "games": [ // 存放所有游戏的数组
    {
      "name": "测试游戏", // 当前游戏的名字
      "save_paths": [ // 存放当前游戏所有存档文件/文件夹的路径
        {
          "unit_type": "Folder", // 存档的类型，Folder (文件夹) 或 File (文件)
          "paths": { // 存档的路径 (按设备ID映射)
            "device_id_1": "X:\\Tests\\存档案例1\\文件夹案例1", // 示例设备1的路径
            "device_id_2": "Y:\\GameSaves\\测试游戏\\文件夹案例1"  // 示例设备2的路径
          },
          "delete_before_apply": false // 应用存档时是否删除原存档
        },
        {
          "unit_type": "File",
          "paths": {
            "device_id_1": "X:\\Tests\\存档案例1\\文件图片1.jpg",
            "device_id_2": "Y:\\GameSaves\\测试游戏\\文件图片1.jpg"
          },
          "delete_before_apply": true
        }
      ],
      "game_paths": { // 游戏的启动路径 (按设备ID映射)
        "device_id_1": "X:\\Games\\测试游戏\\start.exe", // 示例设备1的游戏启动路径
        "device_id_2": "" // 示例设备2的游戏启动路径 (可为空)
      }
    }
    // ... 更多游戏
  ],
  "settings": { // 软件的设置信息
    "prompt_when_not_described": true, // 未描述存档时是否提示
    "extra_backup_when_apply": false, // 应用存档时是否额外备份
    "show_edit_button": false, // 是否显示编辑按钮（尽量不要使用这个功能）
    "prompt_when_auto_backup": true, // 自动备份时是否提示
    "exit_to_tray": false, // 是否最小化到托盘
    "cloud_settings": { // 云同步的设置
      "always_sync": false, // 随时同步
      "auto_sync_interval": 0, // 自动同步的间隔 (单位：分钟，0为禁用)
      "root_path": "/test-game-save-manager", // 云端的根路径
      "backend": { // 云同步后端的设置
        "type": "WebDAV", // 目前支持 WebDAV, AmazonS3 等
        "endpoint": "https://cloud.example.com/dav",
        "username": "user",
        "password": "password"
        // 根据不同的 backend 类型，这里还会有其他特定字段
      }
    },
    "locale": "zh_SIMPLIFIED", // 语言信息, 例如: en, zh_SIMPLIFIED, zh_TRADITIONAL
    "default_delete_before_apply": false, // 新添加的游戏是否先删除存档再应用
    "default_expend_favorites_tree": false, // 是否默认展开收藏树
    "home_page": "/dashboard", // 默认主页路径
    "log_to_file": true, // 日志是否记录到文件
    "add_new_to_favorites": false // 是否把新加入的游戏添加到收藏夹内
  },
  "favorites": [ // 收藏夹树
    {
      "node_id": "uuid_string_1", // 节点ID，使用UUID4
      "label": "游戏或文件夹名", // 游戏名或文件夹名，用于导航和显示
      "is_leaf": true, // true代表是游戏，false代表是文件夹
      "children": null // 如果 is_leaf 为 false, 这里是子节点数组 Array<FavoriteNode>
    }
    // ... 更多收藏项或文件夹
  ],
  "quick_action": { // 快捷操作相关设置
    "quick_action_game": { // 快捷操作对应的游戏
      "name": "快捷操作指定的游戏名", // 必须是 "games" 数组中已存在的游戏名
      // 注意: quick_action_game 内部的 save_paths 和 game_paths 结构与 games[].save_paths 和 games[].game_paths 一致
      // 但通常 quick_action 只关注游戏名
      "save_paths": [
        {
          "unit_type": "Folder",
          "paths": { /* 设备ID: 路径 */ },
          "delete_before_apply": false
        }
      ],
      "game_paths": { /* 设备ID: 路径 */ }
    },
    "hotkeys": { // 快捷键定义
      "apply": ["CONTROL", "ALT", "F1"], // 应用存档的快捷键
      "backup": ["SHIFT", "CONTROL", "S"] // 备份存档的快捷键
    }
  },
  "devices": { // 设备列表 (设备ID -> 设备信息)
    "device_id_1": { // 设备的唯一ID (通常是UUID)
      "id": "device_id_1", // 设备唯一ID
      "name": "我的电脑" // 设备名称
    },
    "device_id_2": {
      "id": "device_id_2",
      "name": "笔记本"
    }
    // ... 更多设备
  }
}
```

## save_data/游戏名/Backups.json

```json5
{
  "name": "测试游戏", // 游戏名
  "backups": [ // 存档的备份数组
    {
      "date": "2024-02-19_00-20-51", // 备份的日期，作为唯一标识符
      "describe": "初始状态", // 备份的描述
      "path": "./save_data\\测试游戏\\2024-02-19_00-20-51.zip", // 存放备份的路径
        "size": 5591 // 备份文件体积，单位是 KiB
    }
  ]
}
```
