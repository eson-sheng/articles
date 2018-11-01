### 其实要的不是「删除」，而是「合并」。

- `git rebase -i <hash>` 从某一个 `commit` 开始
- 在打开的编辑器中，将需要合并的 `commits` 前的 `pick` 修改为 `squash`
- 保存并退出

建议 `git checkout -b squash_some_commits` 新建一个临时分支处理这件事，犯错了删掉重来便是。