# 阀门中英文对照管理系统

##  项目预览
<img width="1365" height="809" alt="QQ20250801-131411" src="https://github.com/user-attachments/assets/b8189b68-2f13-49f3-af46-8f644ff72870" />


##  hub.docker.com地址
https://hub.docker.com/r/xingshu1990/valve-query

##  功能介绍

一个基于Flask的Web应用程序，用于管理阀门的中英文对照信息。
暂无自带数据，
当前版本的项目仅为展示、搭建环境用，
后续将会持续补充数据，作为默认数据。

## 功能特性

### 🔧 核心功能
- **数据管理**: 添加、编辑、删除阀门对照信息
- **文件上传**: 支持PDF、DOC、DOCX、TXT、JPG、JPEG、PNG格式文件
- **数据展示**: 响应式表格，支持分页、搜索、排序
- **批量导入**: 支持Excel和CSV文件批量导入
- **数据导出**: 导出当前所有数据为Excel文件

### 📊 数据字段
- **缩写** (abbreviation): 阀门缩写
- **英文描述** (english_desc): 英文全称
- **中文描述** (chinese_desc): 中文名称
- **文件路径** (file_path): 相关文档文件

## 安装和运行

### 1. 安装依赖
```bash
pip install -r requirements.txt
```

### 2. 运行应用
```bash
python run.py
```

应用将在 `http://搭建设备的ip:5100` 启动

### 3. Docker部署
```bash
docker build -t valve-query .
docker run -p 5100:5100 valve-query
```

## 使用说明

### 添加单个记录
1. 在页面顶部的表单中填写阀门信息
2. 可选择上传相关文件
3. 点击"添加"按钮

### 编辑记录
1. 在表格中点击对应记录的"编辑"按钮
2. 在弹出的模态框中修改信息
3. 点击"保存更改"

### 批量导入数据

#### 方法1: 使用模板文件
```bash
python create_template.py
```
这将创建一个示例Excel文件 `uploads/valve_import_template.xlsx`

#### 方法2: 准备自己的数据文件
Excel或CSV文件必须包含以下列：
- `abbreviation`: 缩写
- `english_desc`: 英文描述  
- `chinese_desc`: 中文描述

#### 导入步骤
1. 在"批量导入"区域选择准备好的文件
2. 点击"批量导入"按钮
3. 系统会显示导入结果

### 导出数据
点击"导出数据"按钮，系统会下载包含所有当前数据的Excel文件。

## API接口

### 获取所有阀门数据
```
GET /api/valves
```

### 添加新阀门
```
POST /api/valves
Content-Type: multipart/form-data
```

### 更新阀门信息
```
PUT /api/valves/<id>
Content-Type: multipart/form-data
```

### 删除阀门
```
DELETE /api/valves/<id>
```

### 批量导入
```
POST /api/import
Content-Type: multipart/form-data
```

### 导出数据
```
GET /api/export
```

## 文件结构

```
valve-query/
├── app/
│   ├── __init__.py          # Flask应用主文件
│   ├── models.py            # 数据模型
│   ├── static/
│   │   └── main.js          # 前端JavaScript
│   └── templates/
│       └── index.html       # 主页面模板
├── uploads/                 # 文件上传目录
├── create_template.py       # 创建导入模板
├── Dockerfile              # Docker配置
├── requirements.txt         # Python依赖
├── run.py                  # 应用入口
└── README.md               # 说明文档
```

## 技术栈

- **后端**: Flask 2.3.2 + Flask-SQLAlchemy 3.0.3
- **数据库**: SQLite
- **前端**: Bootstrap 5.3.0 + jQuery + DataTables
- **文件处理**: pandas + openpyxl
- **容器化**: Docker

## 注意事项

1. 确保 `uploads` 目录有写入权限
2. 导入的Excel/CSV文件必须包含指定的列名
3. 文件上传大小可能受服务器配置限制
4. 建议定期备份数据库文件 `valves.db`

