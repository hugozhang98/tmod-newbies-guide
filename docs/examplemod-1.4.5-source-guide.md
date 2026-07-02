# ExampleMod 1.4.5 源码导读：从入口到各模块

> 适合已经会创建、构建并重载一个 tModLoader 模组，但还不熟悉大型模组如何拆分代码的开发者。

本文分析的源码是本机目录 `D:\downloads\新建文件夹\tModLoader-1.4.5\tModLoader-1.4.5\ExampleMod`。目录名标为 `1.4.5`，但快照内的 `description.txt` 仍链接到 `1.4.4`，`README.md` 则引导读者查看 `stable` 分支；下载包也没有 Git 提交信息。因此本文把它称为“本地 1.4.5 目录快照”，所有结论以这份文件本身为准，不声称它等于某个可验证的正式发布提交。

配套资料：

- [逐目录、逐 C# 文件类型与方法索引](examplemod-1.4.5-class-index.md)：查一个类属于什么类型、有哪些主要 Hook。
- [官方 ExampleMod（stable）](https://github.com/tModLoader/tModLoader/tree/stable/ExampleMod)：用于在线对照；上游更新后可能与本地快照不同。
- [tModLoader stable API](https://docs.tmodloader.net/docs/stable/)：核对 Hook 的当前签名与调用条件。

## 1. 先抓住总原则：它没有手写的“总注册表”

ExampleMod 的主类很短，并不代表其他代码没有执行。tModLoader 会扫描模组程序集里的可加载类型：继承 `ModItem`、`ModProjectile`、`ModNPC`、`ModTile`、`ModPlayer`、`ModSystem` 等基类的类型会按框架规则注册；实现 `ILoadable` 或 `ICustomAutoload` 的类型也能进入加载流程。

所以：

- `Content/Items/Weapons/ExampleGun.cs` 放在这个目录只是为了人类阅读；真正让它成为物品的是 `ExampleGun : ModItem`。
- 文件名、文件夹名与命名空间不负责注册。移动文件后，只要命名空间、资源路径和引用仍正确，内容仍可加载。
- `SetStaticDefaults`、`SetDefaults`、`AddRecipes`、`AI` 等方法不是由主类逐个调用，而是 tModLoader 在对应生命周期调用。
- `[Autoload(Side = ModSide.Client)]`、`ICustomAutoload.Autoload`、`IsLoadingEnabled` 等机制可以进一步限制或定制自动加载。

这也是阅读 ExampleMod 的第一把钥匙：不要找一个不存在的 `RegisterEverything()`；应先看“继承了谁”，再看“重写了哪些 Hook”。

## 2. 构建边界与总体规模

这份快照共有 1219 个文件、559 个 `.cs` 文件。当前构建实际纳入 447 个 C# 文件：根目录 3 个、`Common/` 112 个、`Content/` 332 个。`Old/` 下另有 112 个旧 C# 文件，但明确被排除。

`build.txt` 与 `.csproj` 做了两层排除：

```text
buildIgnore = *.csproj, *.user, obj\*, bin\*, .vs\*, Old\*
<Compile Remove="Old\**" />
```

前者控制打包，后者控制编译。因此 `Old/` 是历史博物馆，不是当前模组的一部分。看到其中的 `ModWorld`、旧字段名或旧网络写法时，只能学思路，不能复制到当前代码。

根元数据的含义如下：

| 文件 | 作用 | 本快照要点 |
| --- | --- | --- |
| `build.txt` | 模组作者、显示名、版本、打包策略 | `includeSource = true`，版本为教学用的 `9999.0`，忽略 `Old/` |
| `ExampleMod.csproj` | .NET/tML 构建入口 | 导入上级 `tModLoader.targets`，使用最新 C# 语法，移除 `Old/**` |
| `ExampleMod.sln` | IDE 解决方案 | 方便 Visual Studio/Rider 打开项目 |
| `.editorconfig` | 代码风格 | 统一缩进、命名和分析器规则 |
| `Properties/launchSettings.json` | 客户端/服务端调试配置 | 分别定义 `Terraria`、`TerrariaServer` 启动项 |
| `description*.txt`、`changelog.txt` | 游戏内、工坊与更新说明 | 支持 `{ModVersion}` 等构建时占位符 |
| `icon*.png` | 模组列表与工坊图标 | 与游戏内容贴图无关 |

## 3. 完整目录大纲

```text
ExampleMod/
├─ ExampleMod.cs                    # Mod 主类：共享资源路径、Load/Unload 说明
├─ ExampleMod.Networking.cs         # 数据包编号与 HandlePacket 分派
├─ ExampleMod.ModCalls.cs           # 给其他模组使用的 Mod.Call 接口
├─ build.txt / .csproj / .sln       # 构建、打包、IDE
├─ description*.txt / changelog.txt # 发布元数据
├─ icon*.png                        # 模组图标
├─ Assets/                          # 不与某个内容类同名的集中资源
│  ├─ Effects/                      # .fx 源 Shader 与编译后的 .xnb
│  ├─ Music/                        # 音乐与授权说明
│  ├─ Sounds/                       # 自定义音效
│  └─ Textures/                     # 背景、图鉴预览、菜单太阳/月亮
├─ Common/                          # 共享状态、全局修改、系统、配置与 UI（112 C#）
│  ├─ Commands/                     # 聊天/控制台命令
│  ├─ Configs/                      # ModConfig、数据类型、配置 UI
│  ├─ CustomVisualEquipType/        # 自定义耳饰视觉槽的完整加载链
│  ├─ EntitySources/                # 按 IEntitySource 判断生成来源
│  ├─ GlobalBossBars/               # 修改所有/指定 Boss 血条
│  ├─ GlobalBuffs/                  # 修改 Buff 的全局行为
│  ├─ GlobalItems/                  # 修改原版或多种物品
│  ├─ GlobalNPCs/                   # NPC 全局行为、掉落、商店、网络
│  ├─ GlobalProjectiles/            # 弹幕全局行为与额外同步
│  ├─ GlobalPylons/                 # 晶塔全局检查与绘制
│  ├─ GlobalTiles/ / GlobalWalls/   # 方块/墙的全局 Hook
│  ├─ ItemDropRules/                # 自定义掉落条件
│  ├─ Players/                      # 玩家临时状态、永久状态、装备效果、按键
│  ├─ Systems/                      # 世界状态、世界生成、集成、生命周期
│  └─ UI/                           # 自定义 UI、资源条、覆盖层与通知
├─ Content/                         # 模组真正增加的内容类型（332 C#）
│  ├─ Achievements/                 # 成就与自定义进度跟踪
│  ├─ Biomes/                       # 地表/地下生态、背景、水与雨
│  ├─ BossBars/ / BossBarStyles/    # Boss 血条实例与整体样式
│  ├─ Buffs/                        # Buff、Debuff 及配套 ModPlayer
│  ├─ BuilderToggles/               # 建筑信息开关
│  ├─ Clouds/                       # 云及手动批量加载
│  ├─ Currencies/                   # 自定义商店货币
│  ├─ CustomModType/                # 从零实现 VictoryPose 内容类型
│  ├─ DamageClasses/                # 自定义伤害职业
│  ├─ Dusts/                        # 粒子更新与自绘
│  ├─ EmoteBubbles/                 # 表情与城镇 NPC 表情
│  ├─ Hairs/                        # 发型与解锁条件
│  ├─ Items/                        # 物品（147 C#，见下一节）
│  ├─ Mounts/                       # 坐骑与矿车行为
│  ├─ NPCs/                         # 普通敌怪、城镇 NPC、宠物 NPC、Boss
│  ├─ Pets/                         # 宠物的 Item + Buff + Projectile 三件套
│  ├─ Prefixes/                     # 前缀与继承示例
│  ├─ Projectiles/                  # 弹幕、近战持有弹幕、召唤物、火箭
│  ├─ Rarities/                     # 自定义稀有度
│  ├─ TileEntities/                 # 可保存、逐 tick 更新的方块实体
│  ├─ Tiles/                        # 地形块、家具、植物、晶塔、机关
│  └─ Walls/                        # 墙与环境转换
├─ Localization/                    # 英、俄、简中正文与配置本地化
├─ Old/                             # 112 个被编译/打包同时排除的历史示例
└─ Properties/launchSettings.json   # 调试启动配置
```

### 3.1 `Content/Items` 的二级结构

| 目录 | C# 文件数 | 主要内容 |
| --- | ---: | --- |
| `Items/` 根 | 23 | 基础物品、绘制、音效、数据实例、研究、微光、使用姿势 |
| `Accessories/` | 14 | 属性饰品、翅膀、冲刺、额外跳、信息饰品、自定义资源 |
| `Ammo/` | 7 | 箭、子弹、火箭、自定义弹药、溶液与环境转换 |
| `Armor/` | 8 | 护甲、套装、染色/装备贴图、时装 |
| `Consumables/` | 14 | 药水、食物、宝箱袋、永久属性、Boss 召唤、城镇宠物许可 |
| `Mounts/` | 2 | 坐骑和矿车召唤物品 |
| `Placeable/` | 39 | 材料块、墙、火把、机关、晶塔、旗帜与家具放置物 |
| `Tools/` | 9 | 镐、锤斧、钻头、钓竿、虫网、钩爪、魔镜、沙枪 |
| `Weapons/` | 31 | 各伤害类型和多种射击/挥舞/持有弹幕范式 |

贴图通常与类同目录、同基础名，例如 `ExampleGun.cs` 对应 `ExampleGun.png`。特殊装备层使用 `_Head`、`_Body`、`_Legs`、`_Wings` 等后缀。集中资源才进入 `Assets/`；这两种摆放方式都存在。

## 4. 从启动到退出的线性调用链

下面是理解整套项目最有用的一条主线。它是生命周期关系，不表示所有同阶段类型之间有稳定的文件顺序。

### 4.1 构建阶段

1. `.csproj` 导入 `tModLoader.targets`。
2. 编译根目录、`Common/` 与 `Content/` 的 C#；剔除 `Old/**`。
3. 根据 `build.txt` 打包资源、源码、描述和图标。
4. `.hjson` 本地化与资源路径在加载时由 tML 解析。

### 4.2 模组实例与类型发现

1. tML 创建唯一的 `ExampleMod : Mod` 实例。
2. 扫描程序集中的 `ModType`、`ModSystem`、`ModPlayer`、`Global*`、`ILoadable` 等类型。
3. 检查 `[Autoload]`、`ICustomAutoload`、`IsLoadingEnabled` 等加载条件。
4. 注册类型并分配 `Type`/`Slot` 等运行时 ID。

目录不参与这一步。`ExampleWings.IsLoadingEnabled` 可读取配置决定是否加载；UI 系统用 `[Autoload(Side = ModSide.Client)]` 避免专用服务器触碰客户端对象；`DefaultCloudsLoader`、`EnemyBannerLoader` 展示手动批量注册。

### 4.3 加载与静态定义

1. `Load()` 适合注册资源、按键、事件或额外槽位。根 `ExampleMod.Load()` 故意为空，官方建议把逻辑放到对应 `ModSystem`/`ModType`。
2. `SetStaticDefaults()` 设置每种类型只需建立一次的数据：研究数量、ID Sets、地图条目、图鉴属性、Boss 头、动画帧、免疫关系、本地化引用等。
3. `ResizeArrays()` 一类 Hook 在内容数量确定后扩充或填充按 Type 索引的数据；耳饰加载器和自定义集合使用它。
4. `PostSetupContent()` 在内容都可查询后做跨模组集成、货币注册、提取机映射等。

判断标准：数据描述“这一种内容是什么”通常放静态阶段；描述“这个实体实例现在是什么状态”不能塞进静态字段。

### 4.4 实例默认值与配方

1. `SetDefaults()` 填充 `Item`、`Projectile`、`NPC` 等模板的宽高、伤害、AI、碰撞、稀有度和使用方式。
2. `AddRecipeGroups()` 先注册配方组。
3. 各 `ModItem.AddRecipes()` 与集中式 `ExampleRecipes.AddRecipes()` 注册配方。
4. `PostAddRecipes()` 可以遍历并修改已经存在的配方。

`SetStaticDefaults` 不会给每个实例执行；`SetDefaults` 可能反复用于创建/重置实例。不要把玩家存档或战斗进度放错位置。

### 4.5 进入世界与运行时

- `ModPlayer.Initialize`、`ResetEffects`、`Update*` 管玩家状态。饰品每 tick 把开关/加成重新设为真，下一 tick 先由 `ResetEffects` 清回默认值。
- `ModSystem.ClearWorld` 清空上一个世界的静态状态；`LoadWorldData`/`SaveWorldData` 读写世界存档；`PreUpdateWorld` 等 Hook 驱动世界逻辑。
- `ModItem` 响应使用、射击、堆叠、拾取、绘制与合成。
- `ModProjectile.AI`、`ModNPC.AI` 驱动实体；`OnHit*`、`OnKill` 处理结果。
- `ModTile` 大多被动响应放置、破坏、绘制、导线、随机更新；`ModTileEntity.Update` 才能可靠地每 tick 保存和更新单个位置的数据。
- UI 的 `ModSystem.UpdateUI` 更新 `UserInterface`，`ModifyInterfaceLayers` 把绘制委托插入原版图层。

### 4.6 保存、同步与卸载

- 玩家永久数据：`ModPlayer.SaveData/LoadData`。
- 世界永久数据：`ModSystem.SaveWorldData/LoadWorldData`，并在 `ClearWorld` 恢复默认值。
- 单实体额外数据：`GlobalItem`、`ModNPC`、`ModProjectile`、`ModTileEntity` 各自的 `SaveData`/`NetSend`/`NetReceive` 或 `SendExtraAI`/`ReceiveExtraAI`。
- 模组自定义消息：发送方先写一个 `MessageType` 字节，再按固定顺序写负载；`ExampleMod.HandlePacket` 读取同样的顺序并分派。
- `Unload()` 撤销事件订阅和外部静态引用。根文件强调防御式卸载；单纯属于可卸载程序集的静态字段通常无需机械地全设为 `null`。

## 5. 三个主入口文件分别负责什么

### 5.1 `ExampleMod.cs`

`public partial class ExampleMod : Mod` 是唯一模组主类。`partial` 让同一个类拆到三个文件：

- `AssetPath = "ExampleMod/Assets/"` 是集中资源路径前缀。
- `Load()` 为空，用注释说明不要把所有加载逻辑堆进主类。
- `Unload()` 为空，用注释说明事件订阅、外部程序集引用和防御式清理。

它的“空”本身就是架构示范：业务功能应靠各类型自己的 Hook 进入系统。

### 5.2 `ExampleMod.Networking.cs`

它把网络协议集中为 `MessageType : byte` 和 `HandlePacket(BinaryReader, whoAmI)`：

1. 发送方 `GetPacket()`。
2. 第一个字节写消息类型。
3. 后续字段按该类型的协议顺序写入。
4. 接收方先 `ReadByte()`，再由 `switch` 调到拥有业务状态的类。
5. 服务器收到客户端消息时，常用 `whoAmI` 覆盖客户端声称的玩家编号，防止伪造；需要时再转发给其他客户端。

主类只做路由，具体处理放回 `ExampleStatIncreasePlayer`、`ExampleDamageModificationPlayer`、`ExampleResourcePlayer`、`VictoryPosePlayer`、`ExamplePerson` 等类。这比把所有业务写在网络入口里更容易维护。

### 5.3 `ExampleMod.ModCalls.cs`

`Call(params object[] args)` 是无编译期引用时的跨模组协议。当前支持：

| 首参数 | 其他参数 | 返回 | 实现 |
| --- | --- | --- | --- |
| `"downedMinionBoss"` | 无 | `bool` | 返回 `DownedBossSystem.downedMinionBoss` |
| `"showMinionCount"` | 无 | `bool` | 返回本地玩家信息显示开关 |
| `"setMinionCount"` | `bool` | `true` | 写入本地玩家开关 |
| 整数 `4` | 无 | `int` | 返回 `ExampleBiomeTileCount.exampleBlockCount` |
| 其他 | — | `false` | 兜底 |

它先检查 `args` 非空、至少一个元素，再用模式匹配识别命令。真实模组应把命令名、参数数量、参数类型、返回类型和错误行为当作稳定协议记录下来。

## 6. `Common/`：共享代码怎样组织

`Common` 的含义是“多个内容会共享或它会修改一类现有内容”，不等于 C# 的 `public`。目录里既有公共类型，也有 `internal` 类型。

| 子目录/文件组 | 如何实现 | 代表类 |
| --- | --- | --- |
| `Commands` | 继承 `ModCommand`，在 `SetStaticDefaults` 定义命令，在 `Action` 解析参数、改变状态 | `ExampleItemCommand`、`ExampleTimeCommand`、`ShowFullscreenUICommand` |
| `Configs` | 继承 `ModConfig`，公开字段/属性并加 `[DefaultValue]`、`[Range]`、`[ReloadRequired]` 等特性；复杂对象实现相等、字符串转换或自定义 `ConfigElement` | `ExampleModConfig`、各 `ModConfigShowcase*`、`GradientElement` |
| `CustomVisualEquipType` | 特性标记物品；`EarringsLoader.ResizeArrays` 扫描并登记贴图；`GlobalItem` 把可见物品和染料写入 `ModPlayer`；`PlayerDrawLayer` 绘制 | `AutoloadEquip_EarringAttribute`、`EarringsLoader`、`EarringsPlayer`、`EarringsDrawLayer` |
| `EntitySources` | `GlobalItem/GlobalProjectile.OnSpawn` 检查 `IEntitySource` 的具体类型，只对特定来源应用修改 | `ExampleSourceDependent*Tweaks` |
| `GlobalItems` | `AppliesToEntity` 缩小作用范围，再用物品 Hook 修改属性、射击、掉落、堆叠、存档与提示 | `ShortswordGlobalItem`、`WeaponWithGrowingDamage` |
| `GlobalNPCs` | 全局掉落、商店、幸福度、聊天交互、DOT、受击、额外 AI 同步 | `ExampleNPCLoot`、`ExampleNPCShop`、`ExampleNPCNetSync` |
| `GlobalProjectiles` | 修改一组弹幕并用 `SendExtraAI/ReceiveExtraAI` 同步额外字段 | `ExampleProjectileModifications`、`ExampleProjectileNetSync` |
| `GlobalBossBars/Buffs/Pylons/Tiles/Walls` | 对相应原版/模组类型的共同行为做横切修改 | `ExampleGlobalBossBar`、`ExampleGlobalBuff`、`SunflowerChanges` |
| `ItemDropRules` | 实现 `IItemDropRuleCondition` 的掉落判定、图鉴可见性与条件说明 | `ExampleDropCondition`、`ExampleSoulCondition` |
| `Players` | 每名玩家一个 `ModPlayer` 实例；分别负责装备状态、永久属性、资源、钓鱼、按键、绘制、伤害等领域 | `ExampleStatIncreasePlayer`、`ExampleResourcePlayer`、`ExampleKeybindPlayer` |
| `Systems` | 模组/世界级单例，承接生命周期、世界存档、世界生成、跨模组集成、按键注册 | `DownedBossSystem`、`KeybindSystem`、`ModIntegrationsSystem` |
| `UI` | `UIState` 建树，`UserInterface` 持有状态，`ModSystem` 更新并插入绘制层；客户端限定避免服务端加载 | `ExampleCoinsUIState`、`ExampleCoinsUISystem`、`ExampleResourceUISystem` |
| 根目录共享类 | 可复用条件、配方回调、地图层、相机修改器、玩家绘制层、手动音乐加载 | `ExampleConditions`、`ExampleRecipeCallbacks`、`ExampleMapLayer` |

几个值得拆开理解的实现：

- `WeaponWithGrowingDamage` 设置 `InstancePerEntity = true`，让经验属于每个物品实例；保存、网络、合堆、拆堆都必须处理经验，避免复制。伤害增幅与提示只读取这个实例状态。
- `ExampleStatIncreasePlayer` 保存永久果实/水晶次数，`ModifyMaxStats` 把次数换算成基础生命/魔力；`CopyClientState` 制作快照，`SendClientChanges` 只在变化时同步。
- `DownedBossSystem` 在 `ClearWorld` 清零，在 `SaveWorldData/LoadWorldData` 保存，在 `NetSend/NetReceive` 用位标志同步。
- `ModIntegrationsSystem.PostSetupContent` 先 `TryGetMod`，再检查版本，最后按对方文档调用 `BossChecklist.Call`；这是可选依赖的典型结构。
- `ExampleCoinsUISystem` 只管 UI 生命周期；具体元素、拖拽面板、按钮分别是独立类。UI 没有塞进 `Mod` 主类。

## 7. `Content/`：每类内容怎样落地

| 模块 | 核心基类 | 典型实现方式 |
| --- | --- | --- |
| `Achievements` | `ModAchievement` | 在 `SetStaticDefaults` 组合条件/位置；高级例子自定义追踪器与完成回调 |
| `Biomes` | `ModBiome`、背景/水样式类型 | `IsBiomeActive` 读取系统统计和玩家位置；属性选择音乐、背景、水、火把；独立样式类负责纹理和颜色 |
| `BossBars` | `ModBossBar`、`ModBossBarStyle` | 修改图标、盾值/生命信息或完全接管绘制 |
| `Buffs` | `ModBuff` | `SetStaticDefaults` 声明 Debuff 等静态集合；`Update` 修改 Player/NPC；复杂效果交给配套 `ModPlayer` 重置和执行 |
| `BuilderToggles` | `BuilderToggle` | 保存开关状态，处理左右键，绘制图标与悬停文本 |
| `Clouds` | `ModCloud` | 决定生成概率、初始化运动并自绘；加载器展示多实例手动注册 |
| `Currencies` | `CustomCurrencySingleCoin` | 以 ExampleItem 为币种，在 `PostSetupContent` 注册货币 ID |
| `CustomModType` | 自定义 `ModVictoryPose : ModTexturedType` | 自己实现注册、ID 列表、Sets、内容子类、Player 运行时与跨模组 API |
| `DamageClasses` | `DamageClass` | 决定继承哪些职业属性/效果，给默认属性并控制提示行 |
| `Dusts` | `ModDust` | `OnSpawn` 初始化，`Update` 控制运动/寿命，`PreDraw` 可完全自绘 |
| `EmoteBubbles` | `ModEmoteBubble` | 注册表情，决定解锁、帧、生成时机；城镇表情再封装 NPC 关联 |
| `Hairs` | `ModHair` | 设置类别并返回解锁条件 |
| `Mounts` | `ModMount` | 定义帧、速度、跳跃与特殊数据；物品/Buff 在其他目录负责召唤和维持 |
| `NPCs` | `ModNPC`、`GlobalNPC`、虫体基类 | 定义静态集合、默认值、生成、AI、帧、图鉴、掉落、聊天/商店及网络状态 |
| `Pets` | `ModItem + ModBuff + ModProjectile` | 物品施加 Buff/生成弹幕，Buff 续期，宠物弹幕跟随玩家并处理动画 |
| `Prefixes` | `ModPrefix` | 决定能否出现、属性乘区、价格、提示；派生类展示复用 |
| `Projectiles` | `ModProjectile` | 默认碰撞/阵营/伤害类型；`AI` 状态机；命中、死亡、碰撞、绘制、额外 AI 同步 |
| `Rarities` | `ModRarity` | 定义颜色和加前缀后的稀有度迁移 |
| `TileEntities` | `ModTileEntity` | 保存/同步位置数据并逐 tick 更新；配套 Tile 负责放置、销毁和交互 |
| `Tiles` | `ModTile`、植物/晶塔派生类型 | 静态 Tile Sets、`TileObjectData`、地图、掉落、导线、绘制、帧、世界生成 |
| `Walls` | `ModWall` | 墙的地图、粉尘、动画、发光、帧与环境转换 |

逐文件的类型、基类和 Hook 已全部放入[配套索引](examplemod-1.4.5-class-index.md)。索引把参与构建的 447 个文件与 `Old/` 的 112 个文件分开，避免旧 API 混入主线。

## 8. 五条跨文件功能链

只按文件夹读容易把内容看成孤岛。下面五条链能说明模块如何合作。

### 8.1 枪、弹药与弹幕

```text
ExampleGun : ModItem
  └─ Item.useAmmo = AmmoID.Bullet
       └─ ExampleBullet : ModItem
            └─ Item.shoot = ModContent.ProjectileType<ExampleBullet>()
                 └─ ExampleBullet : ModProjectile
                      ├─ SetDefaults：碰撞、穿透、AIType、extraUpdates
                      ├─ OnTileCollide：扣穿透并反弹
                      ├─ PreDraw：按 oldPos 画拖尾
                      └─ OnKill：粉尘与声音
```

武器提供基础伤害、速度和弹药类别；弹药补充伤害并决定弹幕 Type；弹幕不需要在 `SetDefaults` 重复写最终伤害，因为生成时会收到计算后的 `damage`。`ExampleGun.ModifyShootStats` 还展示射出前替换弹幕类型。

### 8.2 永久生命提升

```text
ExampleLifeFruit.UseItem
  ├─ 检查原版生命升级与使用上限
  ├─ Player.UseHealthMaxIncreasingItem(...)
  └─ ExampleStatIncreasePlayer.exampleLifeFruits++
       ├─ ModifyMaxStats：次数 × LifePerFruit
       ├─ SaveData/LoadData：保存角色
       ├─ CopyClientState/SendClientChanges：发现变化
       └─ SyncPlayer/ReceivePlayerSync/HandlePacket：联机同步
```

物品只负责“发生一次消费”；长期状态属于 `ModPlayer`。这是比把次数存在 `ModItem` 里更正确的职责划分。

### 8.3 自定义生态

```text
ExampleBiomeTileCount.TileCountsAvailable
  └─ 统计 ExampleBlock 数量
       └─ ExampleSurfaceBiome.IsBiomeActive
            ├─ 至少 40 块
            ├─ 世界中间三分之一
            └─ 地表/天空高度
                 ├─ 选择背景与音乐
                 ├─ 选择 WaterStyle/WaterfallStyle
                 └─ 选择生态火把与篝火
```

Tile 数量由系统统一统计，Biome 只组合条件，视觉/水体再委托给专门样式类。这个拆法比每个玩家每 tick 扫描附近 Tile 更高效。

### 8.4 Boss 内容闭环

```text
MinionBossSummonItem.UseItem
  └─ 单机直接生成 / 客户端请求服务器生成
       └─ MinionBossBody
            ├─ 第一阶段：服务器生成并同步护盾小怪
            ├─ 小怪清空：NPC.ai[] 切换第二阶段 + netUpdate
            ├─ 第二阶段：移动与生成 MinionBossEye
            ├─ ModifyNPCLoot：袋、遗物、面具、宠物等
            └─ OnKill
                 ├─ DownedBossSystem 标记并保存
                 ├─ ExampleOreSystem 祝福矿物
                 └─ 成就/跨模组 Boss Checklist 使用该状态
```

Boss 并不只是一份 AI 文件；召唤物、主体、小怪、弹幕、血条、掉落、家具、宠物、成就、世界进度和兼容层共同形成完整功能。

### 8.5 自定义资源与 UI

```text
ExampleResourcePlayer
  ├─ Initialize/ResetEffects：基础上限与临时加成
  ├─ PostUpdateMiscEffects：计时恢复并 Clamp
  ├─ HealExampleResource：改变权威数值
  └─ HealExampleResourceEffect + packet：同步战斗文字

ExampleResourceAccessory.UpdateAccessory → 提高上限/恢复/吸附
ExampleCustomResourceWeapon.CanUseItem/UseItem → 检查并消耗资源
ExampleResourceUISystem → 客户端更新与插入界面层
ExampleResourceBar → 读取本地 ModPlayer 并绘制渐变条
```

玩法状态、物品规则和显示层是三件事。专用服务器不会加载 `[Autoload(Side = ModSide.Client)]` 的 UI 系统，但玩家资源逻辑仍存在。

## 9. 公共类、公共方法与真正的外部 API

这里要区分三个概念：

1. `Common/` 是目录职责，不代表访问修饰符。
2. `public` 只表示程序集访问级别；大量 `public override` 是 tML 调用的 Hook，不是给其他模组主动调用的 API。
3. 真正的跨模组接口需要作者明确承诺协议。ExampleMod 明确展示了 `Mod.Call` 和 `VictoryPoseLoader` 两种方式。

### 9.1 明确面向其他模组的接口

| 接口 | 作用 | 实现方式 |
| --- | --- | --- |
| `ExampleMod.Call(...)` | 无硬引用地查询 Boss 状态、信息显示状态或 Tile 数量 | 字符串/整数命令 + `object[]` 参数 + `object` 返回；运行时校验 |
| `ModVictoryPose` | 让有编译期模组引用的第三方定义新胜利姿势 | 继承自定义 `ModTexturedType`，覆写 `PoseTime`、文本和绘制/更新 Hook |
| `VictoryPoseLoader.VictoryPoses` | 只读访问全部姿势 | 向外暴露 `IReadOnlyList`，内部仍持有可变 `List` |
| `VictoryPoseLoader.StartPose` | 为本地玩家启动并同步姿势 | 调 `VictoryPosePlayer.StartPose`，客户端成功后发包 |
| `VictoryPoseLoader.CancelPose` | 结束并同步当前姿势 | 清玩家状态，客户端发取消包 |
| `VictoryPoseLoader.GetActivePose` | 查询指定玩家姿势 | 读取其 `VictoryPosePlayer` |

有编译期引用时，自定义 `ModType` 方式具有强类型、自动纹理/本地化、`ModContent.Find/GetInstance` 和 ID Sets 等优势；没有硬依赖时，`Mod.Call` 更松耦合，但参数错误只能运行时发现。

### 9.2 项目内部常用的公共辅助入口

| 类型/成员 | 作用 | 核心实现 |
| --- | --- | --- |
| `ExampleMod.AssetPath` | 集中资源前缀 | 编译期常量，避免到处重复 `ExampleMod/Assets/` |
| `ExampleConditions.InExampleBiome` | 可复用配方/商店条件 | `Condition` 保存本地化键和布尔委托 |
| `ExampleConditions.DownedMinionBoss` | 可复用进度条件 | 委托读取 `DownedBossSystem` |
| `ExampleRecipeCallbacks.DontConsumeChain` | 配方不消耗锁链 | 消耗回调把 `amount` 改为 0 |
| `RandomlySpawnFireworks` | 合成后随机烟花和纸屑 | OnCraft 回调使用来源生成弹幕/物品 |
| `EarringsLoader.AddEarringTexture` | 为物品 Type 登记耳饰贴图 | `ModContent.Request` 后写入 Type→Asset 字典 |
| `ExampleResourcePlayer.HealExampleResource` | 增加并限制自定义资源 | `Math.Clamp` 后触发本地视觉与网络同步 |
| `ExampleStatIncreasePlayer.ReceivePlayerSync` | 读取永久属性包 | 读取顺序与 `SyncPlayer` 写入顺序严格一致 |
| `ExampleDamageModificationPlayer.*Dodge*` | 闪避效果及消息收发 | 玩法 Hook 决定闪避，静态方法负责转发视觉 |
| `ExampleCoinsUISystem.ShowMyUI/HideMyUI` | 切换 UI | 给 `UserInterface` 设置具体 `UIState` 或 `null` |
| `ExampleOreSystem.BlessWorldWithExampleOre` | Boss 后生成矿 | 仅单机/服务端执行，线程池运行矿脉循环并广播文本 |
| `BasicTileEntityTile.MapHoverText` | 显示方块实体填充度 | 先安全查 TileEntity，再区分区块未加载/实体缺失 |
| `Worm.Init/SpawnBodySegments` | 虫体 NPC 基类入口 | 头部生成身体链，段间用 AI 索引关联 |
| `ExampleHomingProjectile.FindClosestNPC` | 找最近合法目标 | 遍历活动 NPC，以距离和可命中条件筛选 |

其余公共 Hook 和辅助方法全部列在[逐类索引](examplemod-1.4.5-class-index.md)。复制辅助类前仍应检查它依赖的字段、网络权威方、资源路径和生命周期；`public` 不代表“脱离上下文即可复用”。

## 10. 网络协议逐项梳理

| `MessageType` | 发送者/触发点 | 负载 | 接收处理 |
| --- | --- | --- | --- |
| `ExampleStatIncreasePlayerSync` | `ExampleStatIncreasePlayer.SyncPlayer` | 玩家、果实次数、水晶次数 | 写入 ModPlayer；服务器转发 |
| `ExampleTeleportToStatue` | `ExamplePerson.OnGoToStatue` | NPC 索引 | 找到活动的 ExamplePerson 后执行传送视觉/逻辑 |
| `ExampleDodge` | 玩家闪避效果 | 玩家与效果所需数据 | `HandleExampleDodgeMessage`，服务器校正玩家并转发 |
| `ExampleTownPetUnlockOrExchange` | 城镇宠物许可 | 本例无额外负载 | 服务器/接收方改变世界宠物解锁状态 |
| `ExampleResourceEffect` | 自定义资源恢复 | 玩家、恢复量 | 只同步 CombatText 效果，服务器转发 |
| `StartVictoryPose` | `VictoryPoseLoader.StartPose` | 玩家、Pose Type | 远端玩家强制启动，服务器转发 |
| `CancelVictoryPose` | `VictoryPoseLoader.CancelPose` | 玩家 | 应结束远端姿势并转发 |
| `SendCustomUseStylePlayerDirection` | 自定义使用姿势玩家 | 玩家、挥舞角度/方向 | 更新远端使用姿势状态 |

协议的读写顺序、整数宽度和条件分支必须镜像。服务器处理来自客户端的玩家相关消息时，优先信任 `whoAmI`，不能盲信包里的玩家索引。

## 11. 存档位置速查

| 数据属于谁 | 示例 | 放置位置 |
| --- | --- | --- |
| 某个角色永久拥有 | 果实/水晶使用次数 | `ExampleStatIncreasePlayer.SaveData/LoadData` |
| 当前 tick 装备产生 | 资源上限加成、免疫、饰品开关 | `ModPlayer.ResetEffects` 清零，饰品 `UpdateAccessory` 重设 |
| 某个世界永久拥有 | Boss 击败、宠物许可、商人状态 | 对应 `ModSystem.SaveWorldData/LoadWorldData/ClearWorld` |
| 某一物品实例拥有 | 武器经验、耐久、多用途物品状态 | `ModItem`/`GlobalItem` 的实例字段 + Save/Net + 堆叠处理 |
| 某个放置位置拥有 | 水桶方块填充度 | `ModTileEntity` 保存、同步、更新 |
| NPC/弹幕短期额外状态 | 随机 AI 值、来源修改次数 | `ai[]`/`localAI[]` 或 `SendExtraAI/ReceiveExtraAI` |
| 纯客户端显示 | UI 展开、局部纹理状态 | 客户端 UI 系统，不写世界权威状态 |

## 12. `Old/` 应该怎样看

`Old/` 包含旧 Boss、旧世界类、旧 UI、旧声音、旧 Buff/Tile/Projectile 等 112 个 C# 文件。它的价值是算法、状态机、视觉想法和历史迁移参考；它的风险是 API 已变。

阅读规则：

1. 先确认同类需求是否已在当前 `Common/` 或 `Content/` 中有新示例。
2. 旧代码只提取算法，不复制类型名、Hook 签名和字段访问。
3. 在 stable API 查当前 Hook，让 IDE 生成 override。
4. 用 `ModSystem`、`ModPlayer`、`ModContent`、新掉落规则和当前网络 API 重新表达。

`Old/ExampleWorld.cs : ModWorld`、旧 `modItem/projectile` 风格正是判断“不能直接粘贴”的警报。

## 13. 源码快照中值得警惕的两个细节

ExampleMod 是教学样例，也应该带着审查意识阅读。

- `ExampleMod.ModCalls.cs` 的 `"setMinionCount"` 分支直接访问 `args[1]`，但没有先检查 `args.Length >= 2`。调用者漏参数时会得到索引异常。自己的公开协议应先验证参数数量，再验证类型。
- `MessageType` 定义了 `CancelVictoryPose`，`VictoryPosePlayer` 也会发送并提供处理函数，但这份快照的 `HandlePacket` 没有对应 `case`。取消包会落入 unknown message 警告。若把该示例搬进自己的模组，应补上路由，并在双客户端验证。

这两点不是让你否定 ExampleMod，而是提醒：示例展示的是方法，不是免检代码。版本快照、注释与实际分支也可能暂时不同步。

## 14. 新手最合适的阅读顺序

不要从 559 个文件按字母读到尾。推荐顺序：

1. 根目录 `build.txt`、`ExampleMod.cs`：先理解构建边界与自动加载。
2. `Content/Items/ExampleItem.cs`：静态默认、实例默认、配方、本地化。
3. `ExampleGun.cs` → 弹药 `ExampleBullet.cs` → 弹幕 `ExampleBullet.cs`：走通物品到实体。
4. `ExampleStatBonusAccessory` 或 `ExampleResourceAccessory` → 对应 `ModPlayer`：理解每 tick 重置。
5. `ExampleCustomAISlimeNPC`：看清状态枚举、AI、帧和平台穿越。
6. `Items/Placeable/ExampleBlock.cs` → `Tiles/ExampleBlock.cs`：区分放置物和世界 Tile。
7. `BasicTileEntity.cs`：学习持久位置数据、服务器权威与防复制。
8. `DownedBossSystem.cs` 与 `ExampleStatIncreasePlayer.cs`：世界/角色存档和同步。
9. `ExampleResourceBar.cs`：最后再把玩法状态接到 UI。
10. `MinionBossBody.cs`：把 AI、网络、掉落、世界进度、血条和内容闭环串起来。
11. `CustomModType/README.md` 及其代码：理解框架级扩展，不建议作为第一个功能。

每读一个文件都回答五个问题：它继承谁？谁创建它？哪个 Hook 先执行？状态属于类型还是实例？单机/客户端/服务器谁有权修改？回答不出来就先在逐类索引和 API 文档中查，而不是继续往下抄。

## 15. 分析覆盖与维护方式

本文的目录数量来自本地快照递归统计；逐类索引扫描了全部 559 个 C# 文件，并用 `build.txt`/`.csproj` 将 447 个当前文件与 112 个 `Old/` 文件分开。索引记录每个文件声明的类型、基类/接口和公开、受保护或内部的主要方法名；主文再按生命周期与跨文件功能链解释实现。

上游更新后建议这样维护：

1. 先比较 `build.txt` 和 `.csproj`，确认编译边界是否变化。
2. 统计新增/删除/移动的 `.cs` 文件。
3. 优先检查根入口、`ModSystem`、网络枚举与公开 Loader/API。
4. 再按基类检查新增 Hook。
5. 更新逐类索引，最后更新本文的功能链与数量。

最重要的结论只有一句：ExampleMod 不是一个从 `Main()` 顺序往下执行的普通程序，而是一组由 tModLoader 生命周期编排、通过状态与 Type 互相连接的内容组件。先沿 Hook 和数据所有权读，目录才会从“几百个文件”变成一张可导航的地图。
