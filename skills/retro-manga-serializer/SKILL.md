---
name: retro-manga-serializer
description: Create continuous multi-page serialized comics in 90s retro watercolor manga style based on user stories and character designs. All narrative boxes, speech balloons, and lettering must use Simplified Chinese. Supports interactive page-by-page confirmation before continuing.
---

# Retro Manga Serializer

基于用户提供的故事剧本与角色设定，连续生成 90 年代复古水彩手绘风格的多页连载漫画。支持逐页交互式确认、严格的角色一致性控制与全简体中文排版规范。

## 何时触发 (When to Use)

- 用户提供故事大纲、分镜剧本或创意想法，希望改编为连载漫画时。
- 用户要求生成 90 年代日漫/台漫复古水彩绘本风格（墨线勾边、水彩淡彩晕染、纸张纹理）时。
- 用户需要交互式分步出图流程（“确认当前页/格无误后，再推进下一页，直到本话完结”）。

---

## 核心工作流 (Execution Steps)

### 第 1 步：角色设定与视觉锚点锁定
- **提取角色特征**：分析用户提供的角色图或文字描述，提取固定视觉锚点（毛发/发型、核心服饰、随身道具、专属色号、标志性微表情）。
- **设定转换**：若角色为 3D 渲染或实物玩偶，需将其笔触与光影扁平化转译为“2D 钢笔墨线 + 手绘淡彩质感”，保留关键特征但去除 3D 塑料感与数码高光。

### 第 2 步：剧本拆解与分页节奏规划
- 单页画格数量控制在 **4 ~ 6 格**，遵循起承转合的分镜动线：
  - **开篇格**：环境交代/大景深或角色出场。
  - **中段格**：动态互动、戏剧转折、特写反应。
  - **终末格**：悬念钩子、情绪定格或场景过渡。
- 明确标注每一格的景别、角色动作、微表情、背景环境、旁白与对白台词。

### 第 3 步：语言与排版规范 (Language & Layout)
- **文字规范**：所有画面内嵌文字（旁白框、对话气泡、拟声词/效果字、末格标识）**必须强制使用简体中文**。
- **对话框形式**：
  - 旁白：白底、黑细边矩形框（Caption Box）。
  - 对白：经典椭圆气泡（Speech Balloon）。
  - 效果字：手绘粗墨线拟声字（如“哒哒哒”、“铃铃铃”）。
- **篇章标记**：
  - 连载未完页尾：右下角标注 `（第N话完，待续……）` 或 `（待续）`。
  - 故事终结页尾：右下角标注 `（本话完）` 或 `（完结）`。

### 第 4 步：交互式连载推进 (Interactive Generation)
1. 生成当前页分镜图。
2. 主动向用户出示画面并询问反馈：
   > “当前第 X 页已生成，请确认画面与剧情是否符合预期？若满意请回复‘继续’或‘可以’，将生成下一页；如需调整细节请直接说明。”
3. 用户确认通过后，承接上一页剧情生成下一页，直至故事完结。

---

## 画风提示词工程规范 (Prompt Engineering)

针对底层生图引擎（Midjourney / FLUX / SD / DALL-E），提示词需统一注入以下视觉参数：

### 正向风格关键词 (Positive Modifiers)
- `Art Style`: 90s vintage anime art style, retro watercolor manga, hand-drawn ink and wash illustration, classic Japanese comic strip layout, nostalgic slice-of-life manga, colored pencil accents, visible paper texture.
- `Panel Structure`: multi-panel comic page layout, clear sequential storytelling, white rectangular caption boxes, speech bubbles with simplified Chinese text.
- `Color & Lighting`: soft natural daylight, gentle watercolor wash, muted retro palette, delicate shading, organic watercolor bleeding.

### 负面规避词 (Negative Prompts)
- `Avoid`: 3D digital render, hyper-realistic, glossy plastic texture, modern CGI, dark neon lighting, deformed hands, broken speech bubbles, traditional Chinese characters.