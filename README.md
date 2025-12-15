# AIDLC Command System for Cursor

<div align="center">

**ระบบ Custom Commands สำหรับ Cursor IDE**  
**ใช้หลักการ AI Development Life Cycle (AIDLC)**

[![Cursor](https://img.shields.io/badge/Cursor-IDE-blue)](https://cursor.com)
[![Commands](https://img.shields.io/badge/Commands-14-green)](.cursor/commands/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

</div>

---

## 🎯 What is AIDLC?

**AI Development Life Cycle (AIDLC)** คือ framework สำหรับพัฒนาซอฟต์แวร์โดยใช้ AI เป็นผู้ช่วย ครอบคลุม 3 phases:

| Phase | Focus | Description |
|-------|-------|-------------|
| 🔵 **INCEPTION** | WHAT | วิเคราะห์ความต้องการ + ออกแบบ |
| 🟢 **CONSTRUCTION** | HOW | Functional design + Code generation |
| 🟡 **OPERATIONS** | RUN | Deploy + Monitor (future) |

---

## 📦 Installation

### Option 1: ใช้ Script (แนะนำ) ✨

```bash
# Clone repo
git clone <repo-url> aidlc-template
cd aidlc-template

# ติดตั้งไปยัง project
./scripts/install-to-project.sh /path/to/your/project

# หรือ ติดตั้งแบบ Global
./scripts/install-global.sh
```

### Option 2: Copy ทั้งโฟลเดอร์ `.cursor/`

```bash
# Clone หรือ download repo นี้
git clone <repo-url> aidlc-template

# Copy ไปยัง project ที่ต้องการใช้
cp -r aidlc-template/.cursor/ your-project/.cursor/
```

### Option 3: Global Installation (ใช้ได้ทุก project)

```bash
# Copy commands ไปที่ global folder
cp -r .cursor/commands/* ~/.cursor/commands/

# Copy rules ไปที่ global folder
mkdir -p ~/.cursor/rules/
cp -r .cursor/rules/* ~/.cursor/rules/
```

> ⚠️ **หมายเหตุ**: หลังจาก copy แล้ว **ต้อง Restart Cursor IDE** เพื่อให้ commands แสดง

---

## 🚀 Quick Start

### 1. เปิด Cursor Chat

กด `Cmd+L` (Mac) หรือ `Ctrl+L` (Windows)

### 2. เริ่มใช้งาน

```
/aidlc
```

AI จะเริ่ม workflow ให้อัตโนมัติ

---

## 📋 Available Commands (14 Commands)

### Main Commands

| Command | Description |
|---------|-------------|
| `/aidlc` | 🏁 เริ่มหรือ resume workflow |
| `/aidlc-init` | 📂 Initialize project structure |
| `/aidlc-status` | 📊 แสดงสถานะปัจจุบัน |
| `/aidlc-multi-repo` | 🔗 Configure multi-repo projects |

### 🔵 INCEPTION Commands

| Command | Description |
|---------|-------------|
| `/aidlc-reverse` | 🔍 Reverse engineering (brownfield) |
| `/aidlc-requirements` | 📝 วิเคราะห์ความต้องการ |
| `/aidlc-stories` | 👤 สร้าง user stories |
| `/aidlc-plan` | 🗺️ วางแผน workflow |
| `/aidlc-design` | 🏗️ ออกแบบ application |
| `/aidlc-units` | 📦 แบ่ง units of work |

### 🟢 CONSTRUCTION Commands

| Command | Description |
|---------|-------------|
| `/aidlc-functional` | ⚙️ Functional design |
| `/aidlc-nfr` | 📐 NFR requirements & design |
| `/aidlc-infra` | ☁️ Infrastructure design |
| `/aidlc-code` | 💻 Code generation |
| `/aidlc-build` | 🔨 Build & test instructions |

---

## 📁 Distribution Contents

```
aidlc-command-cursor/
├── .cursor/
│   ├── commands/              # 📌 14 AIDLC Commands
│   │   ├── aidlc.md           # Main entry
│   │   ├── aidlc-init.md
│   │   ├── aidlc-status.md
│   │   ├── aidlc-reverse.md
│   │   ├── aidlc-requirements.md
│   │   ├── aidlc-stories.md
│   │   ├── aidlc-plan.md
│   │   ├── aidlc-design.md
│   │   ├── aidlc-units.md
│   │   ├── aidlc-functional.md
│   │   ├── aidlc-nfr.md
│   │   ├── aidlc-infra.md
│   │   ├── aidlc-code.md
│   │   ├── aidlc-build.md
│   │   └── README.md          # Commands documentation
│   └── rules/
│       └── aidlc-rules/       # 📚 AIDLC Reference Rules
│           ├── aws-aidlc-rules/
│           │   └── core-workflow.mdc
│           └── aws-aidlc-rule-details/
│               ├── common/    # Shared utilities
│               ├── inception/ # INCEPTION phase rules
│               ├── construction/ # CONSTRUCTION phase rules
│               └── operations/   # OPERATIONS phase rules (future)
├── scripts/                   # 🛠️ Helper Scripts
│   ├── install-global.sh      # ติดตั้งแบบ Global
│   ├── install-to-project.sh  # ติดตั้งไปยัง project
│   └── prepare-distribution.sh # เตรียมสำหรับแจกจ่าย
├── DISTRIBUTION.md            # 📦 Distribution guide
└── README.md
```

### 📂 Generated Structure (เมื่อใช้ AIDLC)

เมื่อ run `/aidlc` จะสร้าง `aidlc-docs/` folder:

```
your-project/
├── .cursor/                   # Commands & Rules
├── aidlc-docs/               # 📝 Generated artifacts
│   ├── audit/                # Branch-based audit logs
│   │   ├── audit-index.md
│   │   ├── main.md
│   │   └── feature-*.md
│   ├── inception/
│   │   ├── plans/
│   │   ├── requirements/
│   │   ├── user-stories/
│   │   └── application-design/
│   ├── construction/
│   │   ├── {unit-name}/
│   │   └── build-and-test/
│   └── aidlc-state.md        # Workflow state
└── [your source code]
```

---

## 💡 Usage Examples

### เริ่มโปรเจกต์ใหม่ (Greenfield)

```
/aidlc
```

### วิเคราะห์ความต้องการพร้อม context

```
/aidlc-requirements Build a REST API for user management with JWT auth
```

### ทำงานต่อจากที่หยุดไว้

```
/aidlc
```

AI จะอ่าน state จาก `aidlc-state.md` และ resume จาก stage ล่าสุด

### ดูสถานะปัจจุบัน

```
/aidlc-status
```

### ใช้กับโปรเจกต์ที่มี code อยู่แล้ว (Brownfield)

```
/aidlc
```

AI จะตรวจจับและเริ่ม Reverse Engineering อัตโนมัติ

---

## 🔗 Multi-Repository Projects

AIDLC รองรับโปรเจกต์ที่แยก Frontend, Backend, Jobs ออกจากกัน:

### Quick Setup

```
/aidlc-multi-repo
```

### Configuration

สร้าง `aidlc-docs/related-projects.md`:

```markdown
# Related Projects

| Project | Type | Path | Description |
|---------|------|------|-------------|
| my-frontend | Frontend | ../my-frontend | React SPA |
| my-backend | Backend | ../my-backend | Node.js API |
| my-jobs | Jobs | ../my-jobs | Background workers |
```

### How It Works

1. **Requirements**: แสดง impact ต่อทุก project
2. **Code Generation**: สร้าง cross-repo change notes
3. **Build & Test**: รวม integration test instructions

### Cursor Multi-Root Workspace (แนะนำ)

เปิดทุก repo ใน workspace เดียว:

1. File → Add Folder to Workspace
2. เพิ่มทุก related project
3. Save as `.code-workspace`

---

## 👥 Team Collaboration

### Branch-Based Audit System

AIDLC ใช้ระบบ audit แยกตาม Git branch:

```
aidlc-docs/audit/
├── audit-index.md          # Master index
├── main.md                 # Main branch audit
├── feature-user-auth.md    # Feature branch audit
├── bugfix-login-fix.md     # Bugfix branch audit
└── archived/               # Merged branch audits
```

**Benefits**:
- ✅ แยก audit ตาม feature branch
- ✅ ง่ายต่อการ review ใน PR
- ✅ ทีมทำงานพร้อมกันได้
- ✅ Archive อัตโนมัติเมื่อ merge

### แนะนำสำหรับทีม

1. **Commit `aidlc-docs/`** ลง repo เพื่อให้ทีมเห็น artifacts ร่วมกัน
2. **ใช้ feature branch** เพื่อให้ audit logs แยกกัน
3. **Review `aidlc-docs/` ใน PR** เพื่อดู requirements และ design

---

## ❓ Troubleshooting

### Commands ไม่แสดงใน Cursor?

1. ตรวจสอบว่า `.cursor/commands/` อยู่ที่ project root
2. **Restart Cursor IDE** (ปิดแล้วเปิดใหม่)
3. ลอง reload window: `Cmd+Shift+P` → "Reload Window"

### ต้องการเริ่มใหม่ทั้งหมด?

```bash
rm -rf aidlc-docs/
/aidlc-init
```

### Error: "Cannot find rule file"?

ตรวจสอบว่า copy ทั้ง `.cursor/commands/` และ `.cursor/rules/` แล้ว

### ใช้กับ Global และ Project-level พร้อมกัน?

Project-level (`.cursor/commands/`) จะ override global (`~/.cursor/commands/`)

---

## 🔗 Links

- 📖 [Cursor Commands Docs](https://cursor.com/docs/agent/chat/commands)
- 📂 [Commands README](.cursor/commands/README.md)
- 📋 [Changelog](CHANGELOG.md)
- 📦 [Distribution Guide](DISTRIBUTION.md)

---

## 📝 Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.4 | 2025-12-15 | Added multi-repository support (frontend/backend/jobs) |
| 1.3 | 2025-12-15 | Updated all rules/commands for branch-based audit consistency |
| 1.2 | 2025-12-15 | Added automatic CHANGELOG management for projects |
| 1.1 | 2025-12-15 | Added team collaboration docs, improved installation guide |
| 1.0 | 2025-12-15 | Initial release |

---

## 📄 License

MIT License - ใช้ได้อย่างอิสระ

---

<div align="center">

**Made with ❤️ using AIDLC**

*ระบบพัฒนาซอฟต์แวร์ด้วย AI อย่างมีระบบ*

</div>

