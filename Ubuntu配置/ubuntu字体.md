yuan@yuan-TpX13G2:~$ fc-match sans-serif DejaVuSans.ttf: "DejaVu Sans" "Book"
使用ubuntu22.04, spotify是deb版本


> `fc-match sans-serif` → **DejaVu Sans**

这说明：  
👉 **你的系统把 DejaVu Sans 当成默认 sans-serif**  
👉 **Spotify（Electron）优先使用了它**  
👉 **DejaVu Sans 对中文是“半残支持”，于是“复”字出问题**

在 **Ubuntu 22.04 + Spotify deb** 这个组合下，**最干净、最稳妥的修复方案**如下。

---

## ✅ 终极推荐方案（一次解决）

### 第一步：安装 Noto CJK（如果你还没装）

`sudo apt update sudo apt install fonts-noto-cjk fonts-noto-cjk-extra`

---

### 第二步（关键）：让系统的 sans-serif 指向中文友好的字体

Ubuntu **默认不会**自动把 CJK 字体放进 sans-serif 回退链里，所以我们要**手动改 fontconfig**。

#### 1️⃣ 创建用户级字体配置（不会影响系统更新）

`mkdir -p ~/.config/fontconfig nano ~/.config/fontconfig/fonts.conf`

#### 2️⃣ 粘贴下面这份「为 Electron / Spotify 特化」的配置

~~~xml 
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>

  <!-- 强制 sans-serif 优先使用中文字体 -->
  <match>
    <test name="family">
      <string>sans-serif</string>
    </test>
    <edit name="family" mode="prepend" binding="strong">
      <string>Noto Sans CJK SC</string>
    </edit>
  </match>

  <!-- 避免 DejaVu 抢中文 -->
  <match>
    <test name="family">
      <string>DejaVu Sans</string>
    </test>
    <edit name="family" mode="append">
      <string>Noto Sans CJK SC</string>
    </edit>
  </match>

</fontconfig>

~~~

保存退出。

---

### 第三步：刷新字体缓存

`fc-cache -fv`

---

### 第四步：验证（很重要）

`fc-match sans-serif`

**理想结果：**

`NotoSansCJK-Regular.ttc: "Noto Sans CJK SC"`

如果你看到这个，说明 **Spotify 一定会正常显示中文**。

---

### 第五步：重启 Spotify

`pkill spotify spotify`

---

## 🎯 为什么这个方案一定能修好你的“复”字？

- Spotify deb = **直接吃系统 fontconfig**
    
- Electron 默认使用 `sans-serif`
    
- 你当前的 `sans-serif → DejaVu Sans`
    
- DejaVu：
    
    - 中文覆盖不完整
        
    - 复杂结构字（复、鬱、龜、鬆）容易出事
        
- **Noto Sans CJK**：
    
    - 全 CJK 覆盖
        
    - Google 官方，Electron 首选