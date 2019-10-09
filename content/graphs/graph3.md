---
title: "Flowchart Horizontal"
date: 2019-10-04T21:43:39-04:00
draft: true
---

{{<mermaid align="left">}}
graph LR;
    A[Hard edge] -->|Link text| B(Round edge)
    B --> C{Decision}
    C -->|One| D[Result one]
    C -->|Two| E[Result two]
{{< /mermaid >}}