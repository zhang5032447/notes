#### 撤销commit

取消commit:  git reset --soft HEAD^

撤销add:  git reset HEAD

 1、误add单个文件 git reset HEAD 将file退回到unstage区 2、误add多个文件，只撤销部分文件 git reset HEAD 将file退回到unstage区

git rm 与 git reset的区别 git rm：用于从工作区和索引中删除文件 git reset：用于将当前HEAD复位到指定状态。一般用于撤消之前的一些操作(如：git add,git commit等)。

git rm file_path 删除暂存区和分支上的文件，同时工作区也不需要 git rm --cached file_path 删除暂存区或分支上的文件, 但工作区需要使用, 只是不希望被版本控制（适用于已经被git add,但是又想撤销的情况） git reset HEAD 回退暂存区里的文件



```json

key: alert_msg
value: {
  "nudity": { // 涉黄
    "en": "11",
    "zh": "22"
  },
  "smoking": {  // 吸烟
    "en": "11"
  },
  "violence": {  // 暴力
    "en": "11"
  },
  "male": {     // 男性
    "en": "11"
  },
  "nobody": {   // 无人
    "en": "11"
  }
}
```

