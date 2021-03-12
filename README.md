# password

## 密碼儲存方式

- 明文保存

  密碼是"123456"，直接將"123456"儲存在資料庫中

- 對稱加密

  使用 AES、RSA 等演算法，這種方式加密是可以通過解密來還原出原始密碼的

- 單向 Hash

  使用 MD5、SHA1 等演算法，無法通過計算還原出原始密碼，但隨著彩虹表技術的興起，可以建立彩虹表進行查表破解，目前這種方式已經很不安全了

- 特殊 Hash

  在 HASH 演算法基礎上增加隨機鹽，使得彩虹表的建表難度大幅增加

- pbkdf2

  該演算法原理大致相當於在 HASH 演算法基礎上增加隨機鹽，並進行多次 HASH 運算，隨機鹽使得彩虹表的建表難度大幅增加，而多次 HASH 也使得建表和破解的難度都大幅增加

| 演算法    | 特點         | 有效破解方式 | 破解難度 | 其他               |
| --------- | ------------ | ------------ | -------- | ------------------ |
| 明文保存  | 實現簡單     | 無需破解     | 簡單     |                    |
| 對稱加密  | 可以解出明文 | 獲取密鑰     | 中       | 需要確保密鑰不洩漏 |
| 單向 Hash | 不可解密     | 碰撞, 彩虹表 | 中       |                    |
| 特殊 Hash | 不可解密     | 碰撞, 彩虹表 | 中       | 需要確保鹽不洩漏   |
| pbkdf2    | 不可解密     | 無           | 難       | 需要確保鹽不洩漏   |

<br>
<br>
<br>

## 兩步驟驗證 (2FA：Two-Factor Authentication)

- TOTP

  TOTP 的概念，就是網站產生一組金鑰，並以當下的時間作為參數，運算出一個雜湊值，並取最後 6 位數作為一次性密碼，如 : Google Authenticator