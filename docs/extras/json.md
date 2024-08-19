# Json文件说明

## GameSaveManager.config.json

```json5
{
  "version": "1.3.0", // 配置文件的版本
  "backup_path": "./save_data", // 备份文件存放路径，暂时不可变，不要更改
  "games": [ // 存放所有游戏的数组
    {
      "name": "测试游戏", // 当前游戏的名字
      "save_paths": [ // 存放当前游戏所有存档文件/文件夹的路径
        {
          "unit_type": "Folder", // 存档的类型，文件夹或文件
          "path": "X:\\Tests\\存档案例1 - 复制\\文件夹案例1（空文件夹）", // 存档的路径
          "delete_before_apply": false // 应用存档时是否删除原存档
        },
        {
          "unit_type": "File",
          "path": "X:\\Tests\\存档案例1\\文件图片1.jpg",
          "delete_before_apply": false
        }
      ],
      "game_path": "" // 游戏的启动路径
    }
  ],
  "settings": { // 软件的设置信息
    "prompt_when_not_described": false, // 未描述存档时是否提示
    "extra_backup_when_apply": false, // 应用存档时是否额外备份
    "show_edit_button": false, // 是否显示编辑按钮（尽量不要使用这个功能）
    "prompt_when_auto_backup": true, // 自动备份时是否提示
    "exit_to_tray": false, // 是否最小化到托盘
    "cloud_settings": { // 云同步的设置
      "always_sync": true, // 随时同步
      "auto_sync_interval": 0, // 自动同步的间隔，暂不可用
      "root_path": "/game-save-manager", // 云端的根路径
      "backend": { // 云同步后端的设置
        "type": "WebDAV",
        "endpoint": "https://XXXXX/dav",
        "username": "XXXX@XX.com",
        "password": "XXXXX"
      },
    "locale": "zh_SIMPLIFIED", // 语言信息
    "default_delete_before_apply": true, // 新添加的游戏是否先删除存档再应用
    "default_expend_favorites_tree": true, // 是否默认展开收藏树
    "home_page": "/management/test单文件", // 默认主页路径
    "log_to_file": false // 日志是否记录到文件
    },
    "favorites": [ // 收藏夹树
      {
        "node_id": "e8dfbdb2-421a-4835-a40d-f5652f24a629", // 节点ID，使用UUID4
        "label": "test", // 游戏名，用于router导航
        "is_leaf": true, // true代表是游戏，false代表是文件夹
        "children": null // 下方可以嵌套自己一样的结构，类型为 Array<FavoriteNode>?
      },
    ]
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
      "path": "./save_data\\测试游戏\\2024-02-19_00-20-51.zip" // 存放备份的路径
    }
  ]
}
```