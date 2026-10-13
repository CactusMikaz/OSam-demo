# OSam

這個 repo 只有一個檔案 `osam.html`：一個用說的就能用的個人秘書，部署成使用者自己的私人 Claude Artifact。

## 使用者說「幫我部署」或「幫我更新」時

1. 完整讀過 `osam.html`，內容**不要修改**
2. 先用 Artifact 工具 `action: "list"` 看使用者有沒有已經部署過的 OSam（標題是「OSam」）
   - **有**：傳那個網址當 `url`，發布 `osam.html` 更新它，**明確傳下面這組 capabilities**（沿用舊的不會打開新功能，例如傳圖片）；不要動資料庫
   - **沒有**：發布成新的 Artifact，`icon` 用 `chat`，`pin: true`，capabilities 用下面這組
3. 不要寫任何初始資料，第一次打開就是空白的
4. 最後給使用者網址，並提醒：用手機 Claude App 打開，第一次跟 OSam 說話會跳出授權，按允許

```json
{
  "db": { "rules": [ { "path": "", "read": "owner", "write": "owner" } ] },
  "sample": { "images": true },
  "user": {},
  "mcp": { "servers": [ { "server": "Parallel Search", "tools": ["web_search", "web_fetch"] } ] }
}
```

- 資料規則一定要是「只有擁有者讀寫」：秘書裡會有使用者的私人資料
- `mcp` 是給「上網查資料」用的。使用者的 claude.ai 沒有連 **Parallel Search** 連接器的話，把 `mcp` 那一項拿掉再發布，並告訴使用者：之後到 claude.ai「設定 → 連接器」連上，再請你重新部署一次就能查網路
- `sample` 的 `images: true` 讓使用者可以傳照片給 OSam
- 更新完，用 `README.md` 最上面那版的「這版改了什麼」跟使用者說一下
- 回覆使用者用繁體中文
