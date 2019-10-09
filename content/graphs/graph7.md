---
title: "Git"
date: 2019-10-04T21:47:54-04:00
draft: true
---

{{<mermaid>}}
gitGraph:
options
{
  "nodeSpacing": 150,
  "nodeRadius": 10
}
end
  commit
  branch newbranch
  checkout newbranch
  commit
  commit
  checkout master
  commit
  commit
  merge newbranch
{{</mermaid>}}
