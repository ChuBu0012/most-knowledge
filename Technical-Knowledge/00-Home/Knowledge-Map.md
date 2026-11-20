---
title: Knowledge Map
type: map
tags: [technical-knowledge, map]
status: published
last_verified: 2026-11-20
---

# Knowledge Map

แผนที่นี้แสดงความรู้ทั้งหมดในขอบเขตปัจจุบันเป็นโหนดที่เชื่อมตาม prerequisites, implementation และ integration. Obsidian Graph View ใช้ internal wikilinks ในแต่ละโน้ตเพื่อให้เดินทางและกรองคลัสเตอร์ได้; Mermaid ด้านล่างเป็นภาพรวมที่อ่านได้จากหน้าเดียว

## เลือกเส้นทางเรียน

- **Web UI:** [[JavaScript]] → [[TypeScript]] → เลือก [[React]], [[Vue]] หรือ [[SvelteKit]] → state/forms/data → [[Vitest]] / [[Playwright]]
- **React server rendering:** [[React Rendering Model]] → [[React Server and Client Components]] → [[Next.js with TypeScript]] หรือ [[React Router Framework]]
- **Go API:** [[Go]] → [[Go Context]] / [[Go Error Handling]] → [[Gin]] หรือ [[Fiber]] → [[Go Testing]]
- **TypeScript API:** [[JavaScript Execution Model]] → [[TypeScript]] → [[Hono]], [[Express]] หรือ [[Elysia]] → [[Zod Runtime Validation]]
- **Python API:** [[Python]] → [[FastAPI]] → [[OpenAPI]] → auth/testing/container
- **Data access:** [[SQL]] → [[Database-Transactions]] / [[SQL Indexes and Query Plans]] → [[Prisma]], [[GORM]] หรือ [[sqlc]]
- **Identity:** [[HTTP Request Lifecycle]] → [[OAuth Authorization Code with PKCE]] → [[JWT Validation]] / [[Cookie and Session Security]]
- **Operations:** [[Docker Image Layers and Reproducible Builds]] → [[Docker Compose Service Networking and Health]] → [[Nginx Reverse Proxy Request Flow]]; เพิ่ม [[RabbitMQ Acknowledgements and Redelivery]] เมื่อมีงาน async

## Technology graph

โหนดทั้งหมดเป็น local notes. Graph View ใช้ wikilinks จริงของ vault; Mermaid นี้เป็นภาพรวมที่สร้างจาก internal links ของ technology/concept notes ณ 2026-11-20.

```mermaid
flowchart LR
  subgraph sg0["HTTP"]
    n31["HTTP"]
    n33["HTTP Request Lifecycle"]
  end
  subgraph sg1["Programming"]
    n35["JavaScript"]
    n36["JavaScript Closures"]
    n37["JavaScript Error Handling"]
    n38["JavaScript Execution Model"]
    n39["JavaScript Modules"]
    n40["JavaScript Promises"]
  end
  subgraph sg2["SQL"]
    n6["Database Transactions"]
    n82["SQL"]
    n83["SQL Indexes and Query Plans"]
  end
  subgraph sg3["Type-System"]
    n99["TypeScript"]
    n100["TypeScript Generics"]
    n101["TypeScript Structural Types"]
    n102["TypeScript Type Narrowing"]
  end
  subgraph sg4["Next.js"]
    n44["Next.js Cache Boundaries and Revalidation"]
    n45["Next.js with TypeScript"]
  end
  subgraph sg5["Nuxt"]
    n50["Nuxt"]
    n51["Nuxt Data Fetching and Request Context"]
  end
  subgraph sg6["React"]
    n65["React"]
    n66["React Component Composition"]
    n67["React Component Identity and Keys"]
    n68["React Effect Synchronization"]
    n71["React Rendering Model"]
    n73["React Server and Client Components"]
    n74["React State and Batching"]
    n75["React TypeScript Props and Events"]
    n76["React with TypeScript"]
  end
  subgraph sg7["React-Router"]
    n72["React Router Framework"]
  end
  subgraph sg8["SvelteKit"]
    n87["Svelte Runes and Reactivity"]
    n88["SvelteKit"]
    n89["SvelteKit Load Functions and Form Actions"]
  end
  subgraph sg9["Vite"]
    n107["Vite"]
    n108["Vite Development and Production Builds"]
  end
  subgraph sg10["Vue"]
    n110["Vue"]
    n111["Vue Composables"]
    n112["Vue Reactivity and Computed State"]
    n113["Vue TypeScript Props and Emits"]
    n114["Vue with TypeScript"]
  end
  subgraph sg11["03-Frontend-Libraries"]
    n0["Browser Form State"]
  end
  subgraph sg12["DaisyUI"]
    n4["DaisyUI"]
  end
  subgraph sg13["Pinia"]
    n55["Pinia"]
    n56["Pinia Store State Actions and Getters"]
  end
  subgraph sg14["React-Hook-Form"]
    n69["React Hook Form"]
    n70["React Hook Form Registration and Validation"]
  end
  subgraph sg15["Reka-UI"]
    n80["Reka UI"]
  end
  subgraph sg16["Tailwind-CSS"]
    n90["Tailwind CSS"]
    n104["Utility-First CSS and Design Tokens"]
  end
  subgraph sg17["TanStack"]
    n43["List Virtualization and Windowing"]
    n91["TanStack Form"]
    n92["TanStack Query"]
    n93["TanStack Query Cache Lifecycle"]
    n94["TanStack Router"]
    n95["TanStack Router Loaders and URL State"]
    n96["TanStack Table"]
    n97["TanStack Table Row Models and Features"]
    n98["TanStack Virtual"]
  end
  subgraph sg18["VeeValidate"]
    n105["VeeValidate"]
    n106["VeeValidate Form and Field Lifecycle"]
  end
  subgraph sg19["Zod"]
    n115["Zod"]
    n116["Zod Runtime Validation"]
  end
  subgraph sg20["Zustand"]
    n117["Zustand"]
    n118["Zustand Store Selectors and Persistence"]
  end
  subgraph sg21["Bun"]
    n1["Bun"]
    n2["Bun Runtime Compatibility and Deployment"]
  end
  subgraph sg22["Elysia"]
    n11["Elysia"]
    n12["Elysia Schemas Plugins and Type Inference"]
  end
  subgraph sg23["Express"]
    n13["Express"]
    n14["Express Middleware Ordering and Errors"]
  end
  subgraph sg24["FastAPI"]
    n15["FastAPI"]
    n16["FastAPI Dependency Injection and Lifetimes"]
  end
  subgraph sg25["Fiber"]
    n17["Fiber"]
  end
  subgraph sg26["Gin"]
    n18["Gin"]
  end
  subgraph sg27["Go"]
    n19["Go"]
    n20["Go Channels"]
    n21["Go Context"]
    n22["Go Error Handling"]
    n23["Go Goroutines"]
    n24["Go HTTP Handler Boundaries"]
  end
  subgraph sg28["Hono"]
    n29["Hono"]
    n30["Hono Middleware and Request Validation"]
  end
  subgraph sg29["JavaScript-Runtime"]
    n49["Node.js"]
  end
  subgraph sg30["Nitro"]
    n48["Nitro"]
  end
  subgraph sg31["Python"]
    n62["Python"]
  end
  subgraph sg32["05-Database"]
    n5["Database Connection Pooling"]
    n59["PostgreSQL"]
  end
  subgraph sg33["GORM"]
    n27["GORM"]
    n28["GORM Transactions and Associations"]
  end
  subgraph sg34["Prisma"]
    n60["Prisma"]
    n61["Prisma Data Model and Migration Safety"]
  end
  subgraph sg35["Redis"]
    n77["Redis"]
    n78["Redis Cache-Aside"]
    n79["Redis Persistence and Durability Choices"]
  end
  subgraph sg36["sqlc"]
    n84["sqlc"]
    n85["sqlc Query Contracts and Generated Code"]
  end
  subgraph sg37["06-Security"]
    n3["Cookie and Session Security"]
    n32["HTTP Authentication"]
    n42["JWT Validation"]
    n53["OAuth Authorization Code with PKCE"]
    n81["Session Management"]
  end
  subgraph sg38["JWT"]
    n41["JWT"]
  end
  subgraph sg39["OAuth-2.0"]
    n52["OAuth 2.0"]
  end
  subgraph sg40["07-Testing"]
    n103["Unit Integration and End-to-End Tests"]
  end
  subgraph sg41["Go-Testing"]
    n25["Go Table-Driven Tests"]
    n26["Go Testing"]
  end
  subgraph sg42["Playwright"]
    n57["Playwright"]
    n58["Playwright Locators and Auto-Waiting"]
  end
  subgraph sg43["Vitest"]
    n109["Vitest"]
  end
  subgraph sg44["Docker"]
    n7["Docker"]
    n10["Docker Image Layers and Reproducible Builds"]
  end
  subgraph sg45["Docker-Compose"]
    n8["Docker Compose"]
    n9["Docker Compose Service Networking and Health"]
  end
  subgraph sg46["Nginx"]
    n46["Nginx"]
    n47["Nginx Reverse Proxy Request Flow"]
  end
  subgraph sg47["RabbitMQ"]
    n63["RabbitMQ"]
    n64["RabbitMQ Acknowledgements and Redelivery"]
  end
  subgraph sg48["API-Design"]
    n34["HTTP Semantics and REST"]
    n54["OpenAPI"]
  end
  subgraph sg49["Application-Architecture"]
    n86["State Management Concepts"]
  end
  n0 --> n105
  n0 --> n116
  n0 --> n57
  n0 --> n69
  n0 --> n91
  n1 --> n109
  n1 --> n29
  n1 --> n33
  n1 --> n35
  n1 --> n38
  n1 --> n39
  n10 --> n19
  n10 --> n46
  n10 --> n7
  n10 --> n8
  n100 --> n102
  n100 --> n115
  n100 --> n76
  n101 --> n100
  n101 --> n54
  n101 --> n76
  n102 --> n100
  n102 --> n115
  n102 --> n15
  n102 --> n76
  n103 --> n109
  n103 --> n26
  n103 --> n57
  n103 --> n6
  n104 --> n108
  n104 --> n4
  n104 --> n80
  n104 --> n90
  n105 --> n0
  n105 --> n110
  n105 --> n112
  n105 --> n115
  n105 --> n116
  n105 --> n55
  n106 --> n0
  n106 --> n105
  n106 --> n112
  n106 --> n116
  n107 --> n108
  n107 --> n109
  n107 --> n110
  n107 --> n39
  n107 --> n65
  n107 --> n88
  n108 --> n109
  n108 --> n110
  n108 --> n39
  n108 --> n65
  n108 --> n88
  n109 --> n103
  n109 --> n107
  n109 --> n108
  n109 --> n26
  n109 --> n57
  n11 --> n1
  n11 --> n102
  n11 --> n29
  n11 --> n33
  n11 --> n34
  n11 --> n99
  n110 --> n111
  n110 --> n112
  n110 --> n114
  n110 --> n50
  n110 --> n55
  n111 --> n105
  n111 --> n112
  n111 --> n50
  n111 --> n55
  n112 --> n105
  n112 --> n110
  n112 --> n114
  n112 --> n55
  n113 --> n102
  n113 --> n112
  n113 --> n114
  n113 --> n116
  n114 --> n102
  n114 --> n105
  n114 --> n110
  n114 --> n111
  n114 --> n112
  n114 --> n55
  n114 --> n99
  n115 --> n102
  n115 --> n116
  n115 --> n69
  n115 --> n91
  n115 --> n99
  n116 --> n102
  n116 --> n105
  n116 --> n54
  n116 --> n69
  n116 --> n91
  n117 --> n65
  n117 --> n74
  n117 --> n86
  n117 --> n92
  n118 --> n117
  n118 --> n3
  n118 --> n74
  n118 --> n86
  n12 --> n1
  n12 --> n102
  n12 --> n11
  n12 --> n34
  n13 --> n29
  n13 --> n33
  n13 --> n34
  n13 --> n35
  n13 --> n37
  n13 --> n52
  n14 --> n116
  n14 --> n13
  n14 --> n33
  n14 --> n37
  n15 --> n33
  n15 --> n34
  n15 --> n52
  n15 --> n53
  n15 --> n54
  n15 --> n62
  n16 --> n103
  n16 --> n15
  n16 --> n33
  n16 --> n53
  n16 --> n6
  n17 --> n13
  n17 --> n18
  n17 --> n19
  n17 --> n21
  n17 --> n33
  n17 --> n34
  n18 --> n17
  n18 --> n19
  n18 --> n21
  n18 --> n22
  n18 --> n31
  n18 --> n33
  n18 --> n34
  n19 --> n17
  n19 --> n18
  n19 --> n20
  n19 --> n21
  n19 --> n22
  n19 --> n23
  n19 --> n26
  n19 --> n84
  n2 --> n1
  n2 --> n10
  n2 --> n38
  n2 --> n58
  n20 --> n21
  n20 --> n23
  n20 --> n26
  n21 --> n18
  n21 --> n20
  n21 --> n23
  n21 --> n63
  n22 --> n17
  n22 --> n18
  n22 --> n19
  n22 --> n26
  n23 --> n20
  n23 --> n21
  n23 --> n26
  n23 --> n63
  n24 --> n17
  n24 --> n18
  n24 --> n19
  n24 --> n21
  n24 --> n22
  n24 --> n34
  n25 --> n103
  n25 --> n22
  n25 --> n26
  n26 --> n103
  n26 --> n17
  n26 --> n18
  n26 --> n19
  n26 --> n22
  n26 --> n25
  n27 --> n19
  n27 --> n22
  n27 --> n5
  n27 --> n6
  n27 --> n84
  n28 --> n22
  n28 --> n27
  n28 --> n5
  n28 --> n6
  n28 --> n83
  n29 --> n1
  n29 --> n11
  n29 --> n13
  n29 --> n33
  n29 --> n34
  n29 --> n37
  n3 --> n32
  n3 --> n46
  n3 --> n53
  n3 --> n81
  n30 --> n116
  n30 --> n29
  n30 --> n33
  n30 --> n52
  n31 --> n15
  n31 --> n46
  n31 --> n52
  n32 --> n31
  n33 --> n15
  n33 --> n31
  n33 --> n32
  n33 --> n46
  n33 --> n52
  n34 --> n15
  n34 --> n18
  n34 --> n33
  n34 --> n52
  n34 --> n54
  n35 --> n36
  n35 --> n37
  n35 --> n38
  n35 --> n39
  n35 --> n40
  n35 --> n49
  n35 --> n65
  n35 --> n99
  n36 --> n100
  n36 --> n71
  n36 --> n86
  n37 --> n109
  n37 --> n15
  n37 --> n18
  n37 --> n40
  n38 --> n31
  n38 --> n39
  n38 --> n40
  n38 --> n49
  n39 --> n1
  n39 --> n107
  n39 --> n49
  n39 --> n99
  n4 --> n104
  n4 --> n80
  n4 --> n90
  n40 --> n31
  n40 --> n38
  n40 --> n71
  n40 --> n92
  n41 --> n3
  n41 --> n32
  n41 --> n42
  n41 --> n52
  n41 --> n53
  n42 --> n32
  n42 --> n41
  n42 --> n53
  n42 --> n81
  n43 --> n58
  n43 --> n93
  n43 --> n96
  n43 --> n98
  n44 --> n3
  n44 --> n45
  n44 --> n73
  n44 --> n93
  n45 --> n107
  n45 --> n3
  n45 --> n34
  n45 --> n52
  n45 --> n65
  n45 --> n73
  n45 --> n76
  n46 --> n15
  n46 --> n3
  n46 --> n31
  n46 --> n33
  n46 --> n47
  n46 --> n7
  n47 --> n33
  n47 --> n46
  n47 --> n52
  n47 --> n9
  n48 --> n31
  n49 --> n31
  n5 --> n27
  n5 --> n59
  n5 --> n6
  n5 --> n60
  n5 --> n83
  n5 --> n84
  n50 --> n110
  n50 --> n111
  n50 --> n114
  n50 --> n3
  n50 --> n48
  n51 --> n111
  n51 --> n3
  n51 --> n33
  n51 --> n48
  n51 --> n50
  n52 --> n31
  n52 --> n33
  n52 --> n41
  n52 --> n42
  n52 --> n53
  n52 --> n81
  n53 --> n33
  n53 --> n42
  n53 --> n52
  n53 --> n81
  n54 --> n31
  n55 --> n110
  n55 --> n111
  n55 --> n112
  n55 --> n114
  n55 --> n50
  n55 --> n86
  n56 --> n111
  n56 --> n112
  n56 --> n55
  n56 --> n86
  n57 --> n103
  n57 --> n109
  n57 --> n3
  n57 --> n58
  n57 --> n65
  n57 --> n88
  n58 --> n103
  n58 --> n32
  n58 --> n57
  n59 --> n31
  n6 --> n27
  n6 --> n59
  n6 --> n60
  n6 --> n63
  n6 --> n82
  n6 --> n84
  n60 --> n5
  n60 --> n59
  n60 --> n6
  n60 --> n83
  n60 --> n99
  n61 --> n5
  n61 --> n6
  n61 --> n60
  n61 --> n83
  n62 --> n31
  n63 --> n19
  n63 --> n21
  n63 --> n6
  n63 --> n64
  n63 --> n77
  n63 --> n8
  n64 --> n21
  n64 --> n6
  n64 --> n63
  n64 --> n9
  n65 --> n117
  n65 --> n45
  n65 --> n66
  n65 --> n67
  n65 --> n68
  n65 --> n71
  n65 --> n73
  n65 --> n74
  n65 --> n76
  n65 --> n92
  n66 --> n117
  n66 --> n71
  n66 --> n74
  n67 --> n66
  n67 --> n71
  n67 --> n74
  n68 --> n36
  n68 --> n57
  n68 --> n71
  n68 --> n92
  n69 --> n0
  n69 --> n115
  n69 --> n116
  n69 --> n65
  n69 --> n91
  n7 --> n10
  n7 --> n46
  n7 --> n77
  n7 --> n8
  n7 --> n9
  n70 --> n0
  n70 --> n116
  n70 --> n58
  n70 --> n69
  n71 --> n67
  n71 --> n68
  n71 --> n73
  n71 --> n74
  n71 --> n76
  n72 --> n29
  n72 --> n33
  n72 --> n34
  n72 --> n45
  n72 --> n65
  n72 --> n73
  n73 --> n32
  n73 --> n45
  n73 --> n52
  n73 --> n71
  n73 --> n72
  n74 --> n117
  n74 --> n67
  n74 --> n71
  n74 --> n86
  n74 --> n92
  n75 --> n100
  n75 --> n102
  n75 --> n66
  n75 --> n76
  n76 --> n100
  n76 --> n102
  n76 --> n115
  n76 --> n65
  n76 --> n66
  n76 --> n69
  n76 --> n71
  n76 --> n99
  n77 --> n6
  n77 --> n63
  n77 --> n7
  n77 --> n78
  n78 --> n27
  n78 --> n6
  n78 --> n60
  n78 --> n77
  n78 --> n8
  n78 --> n84
  n79 --> n6
  n79 --> n77
  n79 --> n78
  n79 --> n9
  n8 --> n10
  n8 --> n63
  n8 --> n7
  n8 --> n77
  n8 --> n9
  n80 --> n104
  n80 --> n110
  n80 --> n112
  n80 --> n4
  n80 --> n90
  n81 --> n31
  n82 --> n31
  n83 --> n59
  n83 --> n6
  n83 --> n60
  n83 --> n82
  n83 --> n84
  n84 --> n19
  n84 --> n5
  n84 --> n6
  n84 --> n82
  n84 --> n83
  n85 --> n26
  n85 --> n6
  n85 --> n82
  n85 --> n83
  n85 --> n84
  n86 --> n31
  n87 --> n107
  n87 --> n57
  n87 --> n88
  n87 --> n99
  n88 --> n107
  n88 --> n108
  n88 --> n57
  n88 --> n58
  n88 --> n87
  n88 --> n99
  n89 --> n0
  n89 --> n52
  n89 --> n87
  n89 --> n88
  n9 --> n5
  n9 --> n63
  n9 --> n7
  n9 --> n77
  n90 --> n104
  n90 --> n107
  n90 --> n108
  n90 --> n4
  n90 --> n80
  n91 --> n0
  n91 --> n105
  n91 --> n115
  n91 --> n116
  n91 --> n69
  n92 --> n110
  n92 --> n115
  n92 --> n40
  n92 --> n6
  n92 --> n65
  n92 --> n93
  n92 --> n96
  n93 --> n115
  n93 --> n40
  n93 --> n74
  n93 --> n94
  n93 --> n96
  n94 --> n115
  n94 --> n34
  n94 --> n65
  n94 --> n92
  n94 --> n95
  n95 --> n116
  n95 --> n34
  n95 --> n93
  n95 --> n94
  n96 --> n43
  n96 --> n90
  n96 --> n92
  n96 --> n93
  n96 --> n98
  n97 --> n34
  n97 --> n43
  n97 --> n93
  n97 --> n96
  n98 --> n110
  n98 --> n43
  n98 --> n65
  n98 --> n96
  n99 --> n100
  n99 --> n101
  n99 --> n102
  n99 --> n115
  n99 --> n35
  n99 --> n76
```

ขอบเขตกราฟ: 45 technology overviews, 74 concepts และ 541 directed links.
