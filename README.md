# git_learn
練習用的 包含從無到有 含建立分之 合併 衝突


前置作業:
1. 使用GITHUB 建立一個repository
2. 地端 use vscode (to see the directory. this can see the differencen of branch (main and leo )

++++++++++++++++++++++++++++++++++++++
`
以下是操作 過程
git  init
(自己建立一個 隨便檔案 main.txt)
 git add *.txt
 git commit -m "add main txt"

 git push (fatal: No configured push destination.)
 尚未設定遠端儲存庫的推送目的地。
>> 建立遠端儲存庫。
git remote add origin <遠端儲存庫網址>
<遠端儲存庫網址>
git remote add origin https://github.com/leo41271/git_learn.git

git push -u origin master 將本地分支推送至遠端
-u : 參數將該分支設定為上游分支， 讓以後 只要執行 git push 即可推送

這時候 我建立了該檔案 指令操作.txt 
git add *
git commit -m "add 說明文件 指令操作.txt"
git push

++++++++++
地端 建立 leo 分支  (之後 創建 leo.txt)
git branch leo (建立leo 分支)

git branch (查看你當前位在哪一個分支。 master 通常指 main)
git checkout 分支名 (切換到某某分支)
git checkout -b leo （合併指令 可同時創建並切換分支）

請確認你當前位於哪個分支 git branch 並切換到 leo分支
git checkout leo
建立 一個檔案 leo分支.txt (手動建立)
git add leo分支.txt

git branch main (中間不小心創建一個 我不想創建的分支 晚點做刪除分支的動作)
切換回來 (git checkout leo)
 git commit -m "add 只有在 leo分支才有的檔案(還未merge 之前)"
git push (遠端尚未有leo分支)
git push --set-upstream origin leo (報錯誤給的 指令 或以下 正規一般操作)
git push origin leo

// git 上查看 分支有三個 只有leo 有leo分支.txt 其他分支 main因為從未推過 所以沒東西
(main 為GITHUB 創建時 自動的預設 我剛開始在地端 創建時 
算創建錯誤 稍晚 會將 master 移植到 main 上)>>>

將 master 分支的內容合併到當前的 main 分支並推送至遠端的 main 分支。
後 刪除 地端和遠端 的 master 分支

先確保 該分支都 提交完畢 如果有未提交的更改
git branch
git checkout master
git branch

git add .
git commit -m "提交所有檔案PS 雖然都是同資料夾 但切換checkout leo 分支 才 會看到 leo分支.txt" (當前使用vscode 看檔案目錄結構)

切換到 main 分支
git checkout main
合併 master 分支的內容到 main 分支
git merge master
將合併 master 分支的內容到 main 分支，並在 main 分支中包含了最新的更改(因你剛剛才做 commit)。

將 main 分支推送至遠端的 main
git push origin main

確保遠端的 main 分支已經更新後 ///////////

刪除本地和遠端的 master 分支
git branch -d master          # 刪除本地的 master 分支
git push origin --delete master    # 刪除遠端的 master 分支
=========================== 資料打玩到這 開始 前面 的 git add . 操作
git push origin main 前面執行到 這時
        To https://github.com/leo41271/git_learn.git
         ! [rejected]        main -> main (non-fast-forward)
        error: failed to push some refs to 'https://github.com/leo41271/git_learn.git'
        hint: Updates were rejected because the tip of your current branch is behind
        hint: its remote counterpart. Integrate the remote changes (e.g.
        hint: 'git pull ...') before pushing again.
        hint: See the 'Note about fast-forwards' in 'git push --help' for details.
表示 我再推送至遠端 分支 時 已經有新的提交(我在剛開始時 在 git 上 因為再推送遠端時 要有 
推送遠端的網址 所以創建該 Repository>> Repositories New ，創建好後 已經有檔案。)

而我的本地 main 分支相對於遠端分支落後 為解決>>
git pull origin main
        From https://github.com/leo41271/git_learn
         * branch            main       -> FETCH_HEAD
        fatal: refusing to merge unrelated histories
Git 拒絕合併無關的歷史記錄 解決這個問題的方法是執行帶有 --allow-unrelated-histories 選項的 git pull 
git pull origin main --allow-unrelated-histories

解決後 繼續本來後續操作
git push origin main
 git branch
  git add .
  git commit -m "更新 指令操作.txt"
  git push
        fatal: The current branch main has no upstream branch.
        To push the current branch and set the remote as upstream, use
            git push --set-upstream origin main
        To have this happen automatically for branches without a tracking
        upstream, see 'push.autoSetupRemote' in 'git help config'.
git push 時，Git 無法找到與當前分支 main 相關聯的上游分支（upstream branch）

git push --set-upstream origin main
將當前的 main 分支推送至遠端並設定遠端分支 origin/main 為 main 分支的上游分支
以後只要 git push

接著做好 main 推送後 進行 刪除分支動作
git branch -d master          # 刪除本地的 master 分支
        warning: not deleting branch 'master' that is not yet merged to
                 'refs/remotes/origin/master', even though it is merged to HEAD.
        error: The branch 'master' is not fully merged.
        If you are sure you want to delete it, run 'git branch -D master'.
尚未完整合併到遠端的 但我要地端 遠端都刪除 所以沒差
git branch -D master
git branch 確認地端已經刪除
git push origin --delete master    # 刪除遠端的 master 分支
到網頁查看 遠端確認刪除沒
確認已經刪除
( PS 在做一些操作時 確保當前分支)



==============================================經歷步驟2
雙虛線以下是跟 leo分歧 操作 展現 之後會進行 merge 操作，操作時 會產生衝突來解決。
我需要選擇衝突檔案 解決挑選 更動部分。
git checkout leo
        error: Your local changes to the following files would be overwritten by checkout:
                指令操作.txt
        Please commit your changes or stash them before you switch branches.
        Aborting
有三種作法
    1提交更改 : git add 指令操作.txt
                git commit -m "我更改的main 操作"
                OK 後再切換到分支 (注意 遠端的狀態!! 是落後的)
    2儲藏更改 : 不想提交更改 但仍然想切換到 leo 分支
                git stash
    3放棄更改 : git checkout -- 指令操作.txt
                git checkout leo
                在這句之前我們先提交一次 作法1
我們選擇步驟二
我們選擇步驟二 (原本這裡的 被我捨棄了 上面那行 因為衝突關係 在我切回 main 分之時消失 因為我 已經 pop 用掉了儲存)
git stash pop (回到原來的分支或其他分支時，可以使用 git stash pop 命令將儲藏的更改還原並從儲藏堆疊中刪除。)
git stash apply : 指定特定的儲藏索引
git stash show : 查看儲藏的更改 而不想立即還原
add commit push 做一次
git add .
git commit -m "git stash pop 操作的使用"
git push

--------------------------經歷步驟4
現在要 merge leo分支
git checkout main
git merge leo
此時產生衝突 需要自己選擇
解決衝突後 執行 commit 以提交 Push
push 後 main 為最新。換 leo分支
--------------------------經歷步驟1
切換分支leo 產生內容 好了之後 再切回 main 在同檔案 新增一些東西
虛線以下 是 切換到 leo分支
因為落後進度 
git pull origin main
讓 leo 指令txt 補滿 然後多新增了 虛線以下的內容再分之leo
告一段落。 push 到自己的分支
git add .
git commit -m "準備之後合併會產生 衝突的 分支內容"

=======================經歷步驟3
當main 切換到 leo (在使用 git stash後， 成功切換leo 後>> git stash pop)
會產生衝突，我選擇原本的
並提交上面內容
 git add .
 git commit -m "測試 git stash git stash pop 測試 pop 效果"


||||||||||||||||||||||||||||||||||||||||
注意我接收了兩著地變更
但在 merge 前 其實我merge了兩次 但第一次沒有衝突 我就切換到 leo
想起我剛剛沒有push 因次 push 後 在切換回來 進行merge
現在要 add commit push 到 leo 進行 地端的整理。

合併後 看到 原本只存在於 leo 分支的 leo分支.txt 被合併進來
我在 這裡再推一次做紀錄。
add commit push

////////////////////////////////////
在分支leo pull下來之後 只有當按更新 。
現在 add commit push 最後這段 再到 main 觀察
`


if it can help you and like it plz give me a star.
有幫到你 對您受益 還請不吝嗇 給我一個 星星
