```bash
%% 如果 .cargo 文件夹存在 %%
cd .cargo
%% 如果 .cargo 文件夹不存在 %%
%% 创建 .cargo 文件夹 %%
mkdir .cargo

%% 查看当前目录结构 %%
tree

%% 创建 config.toml 文件 %%
type nul>config.toml
```

# 替换 crates.io 源

```toml
%% 替换 crates.io 源 %%
%% https://course.rs/first-try/slowly-downloading.html#%E8%A6%86%E7%9B%96%E9%BB%98%E8%AE%A4%E7%9A%84%E9%95%9C%E5%83%8F%E5%9C%B0%E5%9D%80 %%
%% https://www.jianshu.com/p/71fb28974cf6 %%
%% https://doc.rust-lang.org/cargo/reference/source-replacement.html#configuration %%

[source.crates-io]
replace-with = 'ustc'

[source.ustc]
registry = "https://mirrors.ustc.edu.cn/crates.io-index"
```
