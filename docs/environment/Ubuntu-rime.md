# Ubuntu安装配置Rime输入法

输入法平台：ibus

```terminal
sudo apt install ibus-rime
```

- 在ubuntu系统设置里 -> 区域&语言（Region & Language） -> 输入法（Input Sources）设置为Rime
- 在配置中配置rime
```terminal
cd ~/.config/ibus/rime/
sudo gedit default.custom.yaml
```

  yaml中写入配置

  ```Text
  schema_list:   
  - schema: luna_pinyin_simp #simp是简体，第一位是默认输入法
  menu:
    page_size: 9 #每页候选词个数
  ascii_composer:
    switch_key:
      Shift_L: commit_code #左shift提交字母
  ```

- 写好保存，重启ibus
```terminal
ibus restart
```

- 最后在`~/.config/ibus/rime/build/luna_pinyin.schema.yaml`里，拉到底
  ```Text
  switches:
    - name: ascii_mode
      reset: 0
      states: ["中文", "西文"]
    - name: full_shape
      states: ["半角", "全角"]
    - name: simplification
      reset: 1   # 加上一行，改为默认简体
      states: ["漢字", "汉字"]
    - name: ascii_punct
      states: ["。，", "．，"]
  ```