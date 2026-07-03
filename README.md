# 微博开放平台过审站点（方案 C：GitHub Pages）

为微博开放平台应用（ID 334703178）过审搭建的项目说明静态站。内容按桌面 2.txt 方案撰写，
数据边界表述与《A Pre-Registered Two-Tier Fusion Framework...》注册报告逐条对齐。

## 站点结构

```
weibo-risk/                      项目说明五页（首页/方法/隐私/授权/删除）
oauth/weibo/callback/index.html  OAuth 授权回调页（前端读 ?code= 显示成功/失败）
oauth/weibo/cancel/index.html    取消授权回调页
```

## 部署步骤（约 10 分钟）

1. 在 GitHub 新建仓库，仓库名必须是 `<你的用户名>.github.io`（根站点，这样回调路径才能在域名根部）。
2. 把本文件夹内的 `weibo-risk/` 和 `oauth/` 两个目录推送到仓库根目录：
   ```bash
   cd weibo-risk-site
   git init && git add weibo-risk oauth && git commit -m "research site"
   git branch -M main
   git remote add origin https://github.com/<用户名>/<用户名>.github.io.git
   git push -u origin main
   ```
3. 仓库 Settings → Pages 确认 Source = main 分支（根站点默认自动启用）。
4. 等待几分钟，验证以下 4 个地址全部可访问且非 404。

## 微博后台（open.weibo.com/apps/334703178）填写对照

| 字段 | 填写值 |
|---|---|
| 应用地址 | `https://<用户名>.github.io/weibo-risk/` |
| 授权回调页 | `https://<用户名>.github.io/oauth/weibo/callback` |
| 取消授权回调页 | `https://<用户名>.github.io/oauth/weibo/cancel` |
| 安全域名 | `<用户名>.github.io` |
| 应用服务 IP | 静态托管无固定 IP，可留空；若必填，填写 `ping <用户名>.github.io` 得到的 GitHub Pages 出口 IP（185.199.108.153 等四个之一），并知悉其可能变动 |
| 应用名称 | 微博公开内容传播结构研究 |
| 应用简介 | 见 2.txt 第十一节文案（与首页一致） |

## 部署前必改的占位符

全部 7 个 HTML 中搜索替换：
- `[姓名]`、`[学院 / 课题组 / 实验室]` → 真实信息
- `xxx@xxx.edu.cn`（出现在 5 个文件中）→ 真实学术邮箱

## 已知风险（方案 C 固有）

1. **无 ICP 备案**：github.io 为海外域名，微博审核可能因备案问题驳回。若被驳回，
   迁移到方案 A（国内云 + 备案域名）时本站文件可直接复用，仅需改后台四个地址。
2. **无后端**：回调页仅展示授权结果；用授权码换 access token 需研究人员在本地受控
   环境手动完成（连通性测试够用）。**App Secret 绝不能写入本站任何文件。**
3. 提交审核前：在微博后台**重置一次 App Secret**（此前截图曾暴露）。

## 提审前检查清单（对照 2.txt 第十二节）

- [ ] 四个地址 HTTPS 可访问、非空白非 404
- [ ] 占位符已全部替换为真实信息
- [ ] 应用名称/简介已改为中性学术表述
- [ ] 后台应用地址、安全域名、两个回调页同属 `<用户名>.github.io`
- [ ] App Secret 已重置且未出现在任何仓库/网页/截图中
