# git branch 怎麼用

在 Git 中，分支（Branch）就像是一條獨立的時間線，讓你在開發新功能或修復錯誤（Bug）時，不會影響到主要程式碼（Main line）( •̀ ω •́ )✧

幫你整理了一份超實用的 `git branch` 操作筆記！📝✨

---

### 1. 檢視分支（Listing Branches）🔍

* **列出本地所有分支（Local branches）：**
```bash
git branch

```


*(目前所在的分支前面會標註 `*` 號，且通常會顯示綠色)*
* **查看遠端分支（Remote branches）：**
```bash
git branch -r

```


* **查看所有分支（包含本地與遠端，All branches）：**
```bash
git branch -a

```


* **查看各分支最後一次提交（Commit）資訊：**
```bash
git branch -v

```



---

### 2. 建立分支（Creating a Branch）🌱

* **建立新分支（只建立，不會切換過去）：**
```bash
git branch <branch-name>

```


*範例：`git branch feature-login*`

---

### 3. 切換分支（Switching Branches）🔄

* **切換至指定分支（傳統指令）：**
```bash
git checkout <branch-name>

```


* **切換至指定分支（現代建議指令）：**
```bash
git switch <branch-name>

```


* **建立並直接切換過去（超常用捷徑！）：**
```bash
# 現代寫法
git switch -c <branch-name>

# 傳統寫法
git checkout -b <branch-name>

```



---

### 4. 重新命名分支（Renaming a Branch）✏️

* **修改目前所在分支的名稱：**
```bash
git branch -m <new-branch-name>

```


* **修改指定分支的名稱：**
```bash
git branch -m <old-branch-name> <new-branch-name>

```



---

### 5. 刪除分支（Deleting a Branch）🗑️

> ⚠️ **注意：** 不能刪除目前「正位於」的分支，請先切換至其他分支（如 `main`）再刪除喔！(｀･ω･´)ゞ

* **安全刪除（Safe delete，已合併過才會允許刪除）：**
```bash
git branch -d <branch-name>

```


* **強制刪除（Force delete，即使沒合併也會直接刪除）：**
```bash
git branch -D <branch-name>

```


* **刪除遠端分支（Delete remote branch）：**
```bash
git push origin --delete <branch-name>

```



---

### 6. 日常開發工作流程示範（Workflow Example）💻

```bash
# 1. 建立並切換到新功能分支
git switch -c feature-cart

# 2. 開發寫 code、提交存檔
git add .
git commit -m "feat: add shopping cart feature"

# 3. 功能完成後，切回主分支
git switch main

# 4. 把新功能合併（Merge）進主分支
git merge feature-cart

# 5. 合併完畢，刪除已經功成身退的分支
git branch -d feature-cart

```

簡單來說：**`git checkout -b` 就是把「建立分支」與「切換分支」兩件事合在一起的二合一快捷鍵！** (๑•̀ㅂ•́)و✧

幫你整理了一張清晰的對照筆記 📝✨：

---

### 1. 核心關係拆解（The Relationship）🔍

執行下面這一行：

```bash
git checkout -b feature-login

```

**完全等同於**依序執行以下兩條獨立指令：

```bash
git branch feature-login     # 1. 建立分支（Create Branch）
git checkout feature-login   # 2. 切換分支（Switch/Checkout Branch）

```

* 參數 `-b` 的意思就是 **branch**，代表「建立新分支後直接 checkout 過去」。

---

### 2. 兩者的核心功能差異（Comparison Table）📊

| 指令（Command） | 建立分支？（Create） | 切換過去？（Switch） | HEAD 指標移動？（HEAD Move） |
| --- | --- | --- | --- |
| `git branch <name>` | **Yes** | **No**（停留在原地） | 否，仍指著當前分支 |
| `git checkout -b <name>` | **Yes** | **Yes**（立即切換） | **是，指向新分支** |

> 💡 **名詞小備註：**
> * **HEAD**：Git 用來標記「你目前正位於哪個提交或分支」的指標（Pointer）。
> * 用 `git branch` 只是多開了一條分支線，但你的 `HEAD` 還在原分支；
> * 用 `git checkout -b` 則是開好新線的同時，順便把 `HEAD` 移過去。
> 
> 

---

### 3. 現代 Git 的新選擇：`switch -c` 🚀

因為 `git checkout` 在 Git 裡負擔的任務太多（既能切換分支，又能還原檔案（Restore files）），所以 Git 在 2.23 版本之後推出了語意更專一的指令：

* `git switch -c <name>` （`-c` 代表 **create**）

它跟 `git checkout -b <name>` 的效果**一模一樣**，現在也非常推薦使用這個寫法喔！( •̀ ω •́ )✧