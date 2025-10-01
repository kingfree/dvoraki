# Dvoraki 布局

Dvoraki 是在经典 Dvorak 键盘基础上，将原本的 **U** 和 **I** 键互换位置的轻量变体。这样可以让左手食指的基准位承担更高频率的 **i**，在中文拼音和日语罗马字输入中减少手指移动。

## 布局速览

```
' , .  p  y  f  i  u  c  r  l
 a  o  e  i  u  d  h  t  n  s
 ;  q  j  k  x  b  m  w  v  z
```

上表展示了字母区的排列，唯一的差别就是把标准 Dvorak 中的 `u` 和 `i` 互换；数字与符号行保持不变。

## 在 Windows 与 macOS 上部署

- Windows：导入仓库中的 [`dvoraki.reg`](dvoraki.reg) 后重新登录即可覆盖系统级扫描码映射。
- macOS：将 [`karabiner.json`](karabiner.json) 复制到 `~/.config/karabiner/karabiner.json`，或将其中的 `Dvoraki` profile 合并到现有配置中。

两个平台都会把 `Caps Lock` 映射为 `Escape`，如果你在其他布局下已有此习惯，可以直接沿用。

## 拼音输入的改进性

### 数据来源与方法

- 采用 [mozillazg/pinyin-data](https://github.com/mozillazg/pinyin-data) 中的 41,925 条汉字读音，把每个读音等权展开后统计字母频率（把带声调的元音统一为 `a e i o u v`）。[^pinyin-data]
- 根据统计得到的 163,828 个拼音字母，其中 `i` 占 13.37%、`u` 占 10.12%，说明 `i` 的确比 `u` 更常见。
- 将这些频率映射到 QWERTY 与 Dvoraki 键位，比较手指所在行与左右手负载。详细结果保存在 `analysis/pinyin_letter_frequency.csv`、`analysis/pinyin_home_row_comparison.csv` 与 `analysis/pinyin_hand_balance.csv`。

该方法把汉字读音等权视为出现频率，虽不等同于真实语料分布，但能反映拼音结构中元音的占比趋势。

### 结果要点

- **左手基准位的收益**：`i` 的出现概率比 `u` 高出约 3.25 个百分点，因此把 `i` 放到左手食指的静态基准位可以减少向右伸手触键的次数。
- **主键行命中率**：在 QWERTY 上，拼音字母只有 33.96% 落在主键行；Dvoraki 的主键行命中率达到 70.68%，大幅减少手指移至上下排的需求。
- **左右手平衡**：QWERTY 的拼音输入右手负载约 59.67%，左手 40.33%；Dvoraki 把负载重新平衡为左手 57.36%、右手 42.64%，在连打韵母时能更平均地分散压力。

这些指标与 Dvorak 初衷一致——将高频元音集中在主键行——而 Dvoraki 进一步照顾了 `i` 的高频特性。

## 日语罗马字输入的影响

- 日语的基础音节（五十音图）大多由辅音 + 元音组成，只有 `ん`（`n`）和促音例外，意味着每个音节至少包含一个元音。[^gojuon]
- 五十音图中的五个元音（`a i u e o`）作为独立一列，发音时出现频率极高，也常用于延长音与礼貌形结尾（如 `desu`、`masu`）。[^gojuon]
- 因此把全部元音放在主键行、并让常见的 `i`、`u` 均由强壮的食指负责，可减少跨行移动，并让交替敲击辅音与元音时保持良好的节奏；`i` 作为敬语中 `-shi/-chi/-ji` 结尾的常客，更适合占据基准位。

虽然未使用实际语料统计，但从音节结构可以推断 Dvoraki 在罗马字输入时保持甚至放大了 Dvorak 的优势：大量元音集中在主键行，辅音分布于上下行，利于手指交替。

## 使用建议与限制

- 如果你常在中文输入法中使用反查或自定义短语，请注意 Dvoraki 与系统快捷键的冲突，必要时在输入法层重新映射。
- 常见的 `Ctrl+C/X/V/W` 等快捷键需要右手横跨，或依赖双手配合，适应期比字母输入更长；可以考虑通过操作系统或应用的快捷键自定义来缓解。
- 目前尚未制作移动端的输入方案，手机或平板上仍需使用系统自带布局。
- 本仓库的统计基于公开读音词表，未来可以引入语料库频率或实测打字数据进一步验证。

欢迎提交 issue 或 PR 分享实际使用体验与更多语言的打字分析。

[^pinyin-data]: mozillazg, “pinyin-data,” GitHub, accessed 2025-10-01, https://github.com/mozillazg/pinyin-data .
[^gojuon]: “Gojūon,” *Wikipedia*, accessed 2025-10-01, https://en.wikipedia.org/wiki/Goj%C5%ABon .
