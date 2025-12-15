# User Personas: AIDLC Command System

## Overview

| Persona | Experience | Working Style | Primary Goals |
|---------|------------|---------------|---------------|
| Solo Developer | Beginner → Advanced | Individual projects | Quick setup, efficiency |
| Team Lead | Intermediate → Advanced | Team management | Standards, monitoring |
| Team Member | Beginner → Intermediate | Team collaboration | Compliance, guidance |

---

## Persona 1: Solo Developer (Alex)

### Profile
| Attribute | Description |
|-----------|-------------|
| **Name** | Alex Chen |
| **Role** | Full-stack Developer |
| **Experience** | 2-5 years development, varies in AIDLC |
| **Working Style** | Works on personal projects and freelance work |
| **Tech Stack** | TypeScript, React, Node.js, Python |

### Characteristics
- ทำงานคนเดียวกับ personal projects หรือ freelance
- ต้องการ workflow ที่รวดเร็วและมีประสิทธิภาพ
- ไม่มีทีมคอย review ต้องพึ่ง AIDLC เป็น quality gate
- ต้องการ automation เพื่อประหยัดเวลา

### Experience Levels
| Level | Behavior |
|-------|----------|
| **Beginner** | ต้องการ guidance ทุกขั้นตอน, อ่าน prompts ทุกครั้ง |
| **Intermediate** | รู้ขั้นตอน ใช้ shortcuts, ข้าม steps ที่ไม่จำเป็น |
| **Advanced** | ต้องการ efficiency, custom workflows |

### Goals
1. **Primary**: ใช้ AIDLC เพื่อสร้าง high-quality code โดยไม่ต้องมี reviewer
2. **Secondary**: ประหยัดเวลาด้วย automation
3. **Tertiary**: มี documentation สำหรับ future reference

### Pain Points
- ไม่มีเวลาทำ documentation ด้วยตัวเอง
- ต้องการ consistent workflow ข้าม projects
- อยากข้าม stages ที่ไม่จำเป็นโดยไม่ลืม important steps

### User Journey
```
Start Project → /aidlc-init → /aidlc-requirements → /aidlc-plan → 
/aidlc-code → /aidlc-build → Complete
```

---

## Persona 2: Team Lead (Jordan)

### Profile
| Attribute | Description |
|-----------|-------------|
| **Name** | Jordan Lee |
| **Role** | Tech Lead / Architect |
| **Experience** | 7+ years development, 2+ years with AIDLC |
| **Working Style** | Manages team of 3-8 developers |
| **Tech Stack** | Multiple stacks, focuses on architecture |

### Characteristics
- กำหนด standards และ best practices สำหรับทีม
- ต้องการ monitor team's AIDLC compliance
- Review และ approve key decisions
- Customize workflows ตาม project needs

### Experience Levels
| Level | Behavior |
|-------|----------|
| **Intermediate** | Uses standard workflows, occasional customization |
| **Advanced** | Creates custom rules, defines team standards |

### Goals
1. **Primary**: Enforce AIDLC standards across team
2. **Secondary**: Monitor progress และ quality ของ team members
3. **Tertiary**: Reduce time spent on reviews with automated checks

### Pain Points
- ยากที่จะ track ว่าทุกคนทำตาม AIDLC หรือไม่
- ต้องการ visibility ของ team's progress
- อยาก customize rules โดยไม่ break existing workflows

### User Journey
```
Define Standards → /aidlc-init (with team config) → Monitor Progress →
Review /aidlc-status reports → Approve/Request Changes → Guide team
```

---

## Persona 3: Team Member (Sam)

### Profile
| Attribute | Description |
|-----------|-------------|
| **Name** | Sam Park |
| **Role** | Software Developer |
| **Experience** | 1-4 years development, new to AIDLC |
| **Working Style** | Works within team structure |
| **Tech Stack** | Follows team's tech stack |

### Characteristics
- ทำงานตาม team standards
- ต้องการ clear guidance ในแต่ละขั้นตอน
- Reports to Team Lead
- Learning AIDLC methodology

### Experience Levels
| Level | Behavior |
|-------|----------|
| **Beginner** | Follows all prompts, needs extensive guidance |
| **Intermediate** | Knows workflow, still needs AC verification |

### Goals
1. **Primary**: Complete tasks according to team's AIDLC standards
2. **Secondary**: Learn AIDLC methodology effectively
3. **Tertiary**: Get work approved quickly

### Pain Points
- ไม่แน่ใจว่า output ถูกต้องตาม standards หรือไม่
- ต้องการ feedback ก่อน submit for review
- อยากรู้ว่าต้องทำอะไรต่อ

### User Journey
```
Receive Task → /aidlc-status (check standards) → Execute workflow →
/aidlc-status (verify completion) → Submit for review
```

---

## Persona Comparison Matrix

| Aspect | Solo Developer | Team Lead | Team Member |
|--------|---------------|-----------|-------------|
| **Decision Authority** | Full | Defines standards | Follows standards |
| **Customization Need** | Medium | High | Low |
| **Guidance Need** | Varies | Low | High |
| **Monitoring Need** | Self-check | Team-wide | Self-progress |
| **Primary Action** | Execute workflow | Define & monitor | Execute & report |
| **Skip Stages** | Often | Sometimes | Rarely |
| **Error Tolerance** | Medium | Low | Low |

---

## Persona-to-Command Mapping

| Command | Solo Developer | Team Lead | Team Member |
|---------|---------------|-----------|-------------|
| `/aidlc` | ⭐ Primary | ⭐ Primary | ⭐ Primary |
| `/aidlc-init` | ⭐ Primary | ⭐ Primary | Secondary |
| `/aidlc-status` | Secondary | ⭐ Primary | ⭐ Primary |
| `/aidlc-requirements` | ⭐ Primary | Review | ⭐ Primary |
| `/aidlc-stories` | Optional | Review | ⭐ Primary |
| `/aidlc-plan` | ⭐ Primary | ⭐ Primary | Secondary |
| `/aidlc-design` | ⭐ Primary | ⭐ Primary | Secondary |
| `/aidlc-code` | ⭐ Primary | Review | ⭐ Primary |
| `/aidlc-build` | ⭐ Primary | Review | ⭐ Primary |

---

## Document History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2025-12-15 | Initial personas document |

