# ExampleMod 1.4.5 逐目录、逐类索引

> 对应本地 `tModLoader-1.4.5/ExampleMod` 快照。先读[中文源码导读](examplemod-1.4.5-source-guide.md)，再把本页当作地图和检索表。

本索引覆盖全部 559 个 C# 文件：447 个参与当前构建，112 个位于 `Old/` 且被 `.csproj` 与 `build.txt` 排除。一个文件可能声明多个类型，所以“文件数”不等于“类数”。“主要方法”收集源码中公开、受保护或内部的方法/构造函数名称，包括 tModLoader Hook；私有实现细节不在表内。类名和 Hook 名保留英文，便于在 IDE 中搜索；职责与实现线索均用中文解释。`public override` 通常是框架回调，不自动等于稳定的跨模组 API。

## 当前参与构建的代码

### `[根目录]`（3 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `ExampleMod.cs` | public partial ExampleMod : Mod | Load, Unload | 模组入口；加载、注册或清理 |
| `ExampleMod.ModCalls.cs` | public partial ExampleMod : Mod | Call | 模组入口；通过表中成员提供专用数据或辅助算法 |
| `ExampleMod.Networking.cs` | public partial ExampleMod : Mod; internal MessageType : byte | HandlePacket | 模组入口；序列化并同步联机状态 |

### `Common`（6 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Common/ExampleCameraModifier.cs` | public ExampleCameraModifier : ICameraModifier | ExampleCameraModifier, Update | 相机修改器；在更新 Hook 中驱动状态/AI |
| `Common/ExampleConditions.cs` | public static ExampleConditions | — | 共享辅助类型；通过表中成员提供专用数据或辅助算法 |
| `Common/ExampleMapLayer.cs` | public ExampleMapLayer : ModMapLayer; public ExampleMapLayerSystem : ModSystem; public ExampleItemMapLayer : ModMapLayer | GetDefaultPosition, Draw, NetSend, NetReceive, GetModdedConstraints | 系统/生命周期、地图层；处理帧、特效或自定义绘制；序列化并同步联机状态 |
| `Common/ExamplePlayerDrawLayer.cs` | public ExamplePlayerDrawLayer : PlayerDrawLayer | GetDefaultVisibility, GetDefaultPosition, Draw | 玩家绘制层；处理帧、特效或自定义绘制 |
| `Common/ExampleRecipeCallbacks.cs` | public static ExampleRecipeCallbacks | DontConsumeChain, RandomlySpawnFireworks | 共享辅助类型；通过表中成员提供专用数据或辅助算法 |
| `Common/ManualMusicRegistrationExample.cs` | public sealed ManualMusicRegistrationExample : ICustomAutoload | Autoload | 自定义自动加载；加载、注册或清理 |

### `Common/Commands`（6 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Common/Commands/ExampleCoinsCommand.cs` | public ExampleCoinsCommand : ModCommand | SetStaticDefaults, Action | 命令；登记类型级静态数据 |
| `Common/Commands/ExampleItemCommand.cs` | public ExampleItemCommand : ModCommand | SetStaticDefaults, Action | 命令；登记类型级静态数据 |
| `Common/Commands/ExampleSummonCommand.cs` | public ExampleSummonCommand : ModCommand | SetStaticDefaults, Action | 命令；登记类型级静态数据 |
| `Common/Commands/ExampleTimeCommand.cs` | public ExampleTimeCommand : ModCommand | SetStaticDefaults, Action | 命令；登记类型级静态数据 |
| `Common/Commands/ModifyServerConfigValueCommand.cs` | public ModifyServerConfigValueCommand : ModCommand | SetStaticDefaults, Action | 命令；登记类型级静态数据 |
| `Common/Commands/ShowFullscreenUICommand.cs` | public ShowFullscreenUICommand : ModCommand | SetStaticDefaults, Action | 命令；登记类型级静态数据 |

### `Common/Configs`（1 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Common/Configs/ExampleModConfig.cs` | public ExampleModConfig : ModConfig | — | 配置；通过表中成员提供专用数据或辅助算法 |

### `Common/Configs/CustomDataTypes`（6 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Common/Configs/CustomDataTypes/ClassUsedAsKey.cs` | public ClassUsedAsKey | Equals, GetHashCode, ToString, FromString | 配置数据类型；通过表中成员提供专用数据或辅助算法 |
| `Common/Configs/CustomDataTypes/ComplexData.cs` | public ComplexData | Equals, GetHashCode | 配置数据类型；通过表中成员提供专用数据或辅助算法 |
| `Common/Configs/CustomDataTypes/Gradient.cs` | public Gradient | Equals, GetHashCode | 配置数据类型；通过表中成员提供专用数据或辅助算法 |
| `Common/Configs/CustomDataTypes/Pair.cs` | public Pair | ToString, Equals, GetHashCode | 配置数据类型；通过表中成员提供专用数据或辅助算法 |
| `Common/Configs/CustomDataTypes/SampleEnum.cs` | public SampleEnum | — | 配置数据类型；通过表中成员提供专用数据或辅助算法 |
| `Common/Configs/CustomDataTypes/SimpleData.cs` | public SimpleData | SimpleData, Equals, GetHashCode | 配置数据类型；通过表中成员提供专用数据或辅助算法 |

### `Common/Configs/CustomUI`（3 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Common/Configs/CustomUI/CornerElement.cs` | public Corner; internal CornerElement : ConfigElement | OnBind, LeftClick, RightClick, Draw | 配置 UI；处理帧、特效或自定义绘制；处理方块放置、导线或玩家交互 |
| `Common/Configs/CustomUI/CustomFloatElement.cs` | internal CustomFloatElement : FloatElement | CustomFloatElement | 配置 UI；通过表中成员提供专用数据或辅助算法 |
| `Common/Configs/CustomUI/GradientElement.cs` | internal GradientElement : ConfigElement | OnBind, Draw | 配置 UI；处理帧、特效或自定义绘制 |

### `Common/Configs/ModConfigShowcases`（8 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Common/Configs/ModConfigShowcases/ModConfigShowcaseAcceptClientChanges.cs` | public ModConfigShowcaseAcceptClientChanges : ModConfig | OnLoaded, AcceptClientChanges, HandleAcceptClientChangesReply | 配置；通过表中成员提供专用数据或辅助算法 |
| `Common/Configs/ModConfigShowcases/ModConfigShowcaseAccessibility.cs` | public ModConfigShowcaseAccessibility : ModConfig | ModConfigShowcaseAccessibility, ShouldSerializeGetter | 配置；通过表中成员提供专用数据或辅助算法 |
| `Common/Configs/ModConfigShowcases/ModConfigShowcaseDataTypes.cs` | public ModConfigShowcaseDataTypes : ModConfig | ModConfigShowcaseDataTypes | 配置；通过表中成员提供专用数据或辅助算法 |
| `Common/Configs/ModConfigShowcases/ModConfigShowcaseDefaultValues.cs` | public ModConfigShowcaseDefaultValues : ModConfig | — | 配置；通过表中成员提供专用数据或辅助算法 |
| `Common/Configs/ModConfigShowcases/ModConfigShowcaseLabels.cs` | public ModConfigShowcaseLabels : ModConfig | — | 配置；通过表中成员提供专用数据或辅助算法 |
| `Common/Configs/ModConfigShowcases/ModConfigShowcaseMisc.cs` | public ModConfigShowcaseMisc : ModConfig | ModConfigShowcaseMisc, OnDeserializedMethod | 配置；通过表中成员提供专用数据或辅助算法 |
| `Common/Configs/ModConfigShowcases/ModConfigShowcaseRanges.cs` | public ModConfigShowcaseRanges : ModConfig | OnDeserializedMethod | 配置；通过表中成员提供专用数据或辅助算法 |
| `Common/Configs/ModConfigShowcases/ModConfigShowcaseSubpages.cs` | public ModConfigShowcaseSubpages : ModConfig; public SubConfigExample; public SubSubConfigExample | ToString, Equals, GetHashCode | 配置；通过表中成员提供专用数据或辅助算法 |

### `Common/CustomVisualEquipType`（7 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Common/CustomVisualEquipType/AutoloadEquip_EarringAttribute.cs` | public AutoloadEquip_EarringAttribute : Attribute | — | 共享辅助类型；通过表中成员提供专用数据或辅助算法 |
| `Common/CustomVisualEquipType/EarringsDrawLayer.cs` | public EarringsDrawLayer : PlayerDrawLayer | GetDefaultVisibility, GetDefaultPosition, Draw | 玩家绘制层；处理帧、特效或自定义绘制 |
| `Common/CustomVisualEquipType/EarringsGlobalItem.cs` | public EarringsGlobalItem : GlobalItem | UpdateVisibleAccessory, UpdateItemDye | 全局物品修改；通过表中成员提供专用数据或辅助算法 |
| `Common/CustomVisualEquipType/EarringsLoader.cs` | public EarringsLoader : ModSystem | ResizeArrays, AddEarringTexture | 系统/生命周期；通过表中成员提供专用数据或辅助算法 |
| `Common/CustomVisualEquipType/EarringsPlayer.cs` | public EarringsPlayer : ModPlayer | ResetEffects | 玩家扩展；处理帧、特效或自定义绘制 |
| `Common/CustomVisualEquipType/RubyEarrings.cs` | public RubyEarrings : ModItem | SetDefaults | 物品；设置实体/物品实例默认值 |
| `Common/CustomVisualEquipType/SapphireEarrings.cs` | public SapphireEarrings : ModItem | SetStaticDefaults, SetDefaults | 物品；登记类型级静态数据；设置实体/物品实例默认值 |

### `Common/EntitySources`（1 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Common/EntitySources/ExampleSourceDependentTweaks.cs` | public sealed ExampleSourceDependentProjectileTweaks : GlobalProjectile; public sealed ExampleSourceDependentItemTweaks : GlobalItem; public sealed ExampleSourceDependentItemTweaks2 : GlobalItem | AppliesToEntity, OnSpawn | 全局物品修改、全局弹幕修改；控制生成或初始化 |

### `Common/GlobalBossBars`（1 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Common/GlobalBossBars/ExampleGlobalBossBar.cs` | public ExampleGlobalBossBar : GlobalBossBar | PreDraw, PostDraw | 共享辅助类型；处理帧、特效或自定义绘制 |

### `Common/GlobalBuffs`（1 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Common/GlobalBuffs/ExampleGlobalBuff.cs` | public ExampleGlobalBuff : GlobalBuff | SetStaticDefaults, Update, PreDraw, ModifyBuffText, RightClick | 全局 Buff 修改；登记类型级静态数据；在更新 Hook 中驱动状态/AI；处理帧、特效或自定义绘制；处理方块放置、导线或玩家交互 |

### `Common/GlobalItems`（6 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Common/GlobalItems/BossBagLoot.cs` | public BossBagLoot : GlobalItem | ModifyItemLoot | 全局物品修改；配置掉落规则 |
| `Common/GlobalItems/ExampleResearchSorting.cs` | public ExampleResearchSorting : GlobalItem | ModifyResearchSorting | 全局物品修改；通过表中成员提供专用数据或辅助算法 |
| `Common/GlobalItems/GelGlobalItem.cs` | public GelGlobalItem : GlobalItem | SetStaticDefaults, AppliesToEntity, ModifyTooltips | 全局物品修改；登记类型级静态数据 |
| `Common/GlobalItems/ShortswordGlobalItem.cs` | public ShortswordGlobalItem : GlobalItem | AppliesToEntity, SetDefaults, Shoot | 全局物品修改；设置实体/物品实例默认值；控制射击、弹药或生成弹幕 |
| `Common/GlobalItems/TorchExtractinatorGlobalItem.cs` | public TorchExtractinatorGlobalItem : GlobalItem; public TorchExtractinatorModSystem : ModSystem | ExtractinatorUse, PostSetupContent | 系统/生命周期、全局物品修改；加载、注册或清理 |
| `Common/GlobalItems/WeaponWithGrowingDamage.cs` | public WeaponWithGrowingDamage : GlobalItem; public DoubleXPSnowBallInExamplePersonShop : GlobalNPC | IsLoadingEnabled, AppliesToEntity, SetStaticDefaults, LoadData, SaveData, NetSend, NetReceive, OnHitNPC, OnHitNPCGeneral, GainExperience, UpdateValue, UpdateInventory, ModifyWeaponDamage, ModifyTooltips, OnCreated, OnStack, SplitStack, ModifyShop | 全局物品修改、全局 NPC 修改；登记类型级静态数据；保存、读取或重置持久状态；序列化并同步联机状态；处理商店、聊天或交互；处理伤害、命中或闪避 |

### `Common/GlobalNPCs`（13 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Common/GlobalNPCs/BuffImmuneGlobalNPC.cs` | public BuffImmuneGlobalNPC : GlobalNPC | SetStaticDefaults, SetDefenseDebuffStaticDefaults, SetDefaults | 全局 NPC 修改；登记类型级静态数据；设置实体/物品实例默认值 |
| `Common/GlobalNPCs/DamageModificationGlobalNPC.cs` | internal DamageModificationGlobalNPC : GlobalNPC | ResetEffects, ModifyIncomingHit, DrawEffects | 全局 NPC 修改；处理帧、特效或自定义绘制；处理伤害、命中或闪避 |
| `Common/GlobalNPCs/DamageOverTimeGlobalNPC.cs` | internal DamageOverTimeGlobalNPC : GlobalNPC | ResetEffects, UpdateLifeRegen | 全局 NPC 修改；处理帧、特效或自定义绘制 |
| `Common/GlobalNPCs/EmotePickerGlobalNPC.cs` | public EmotePickerGlobalNPC : GlobalNPC | PickEmote | 全局 NPC 修改；通过表中成员提供专用数据或辅助算法 |
| `Common/GlobalNPCs/ExampleBestiaryGlobalNPC.cs` | public ExampleBestiaryGlobalNPC : GlobalNPC; private ImportantFlavorTextElement : IBestiaryInfoElement, IBestiaryPrioritizedElement, ICategorizedBestiaryInfoElement | ProvideUIElement, SetBestiary | 全局 NPC 修改；通过表中成员提供专用数据或辅助算法 |
| `Common/GlobalNPCs/ExampleNPCHappiness.cs` | public ExampleNPCHappiness : GlobalNPC | SetStaticDefaults | 全局 NPC 修改；登记类型级静态数据 |
| `Common/GlobalNPCs/ExampleNPCLoot.cs` | public ExampleNPCLoot : GlobalNPC | ModifyNPCLoot, ModifyGlobalLoot | 全局 NPC 修改；配置掉落规则 |
| `Common/GlobalNPCs/ExampleNPCNetSync.cs` | public ExampleNPCNetSync : GlobalNPC | AppliesToEntity, OnSpawn, SendExtraAI, ReceiveExtraAI, AI | 全局 NPC 修改；在更新 Hook 中驱动状态/AI；序列化并同步联机状态；控制生成或初始化 |
| `Common/GlobalNPCs/ExampleNPCShop.cs` | internal ExampleNPCShop : GlobalNPC | ModifyShop | 全局 NPC 修改；处理商店、聊天或交互 |
| `Common/GlobalNPCs/ExampleResourcePickupGlobalNPC.cs` | public ExampleResourcePickupGlobalNPC : GlobalNPC | OnKill | 全局 NPC 修改；通过表中成员提供专用数据或辅助算法 |
| `Common/GlobalNPCs/GobalNPCInteractions.cs` | public GlobalNPCInteractions : GlobalNPC | AppliesToEntity, RegisterChatButtons, PreChatButtonClicked, OnChatButtonClicked | 全局 NPC 修改；处理商店、聊天或交互 |
| `Common/GlobalNPCs/GuideGlobalNPC.cs` | public GuideGlobalNPC : GlobalNPC | AppliesToEntity, AI, EmoteBubblePosition, PartyHatPosition | 全局 NPC 修改；在更新 Hook 中驱动状态/AI |
| `Common/GlobalNPCs/ProjectileModificationGlobalNPC.cs` | public ProjectileModificationGlobalNPC : GlobalNPC | — | 全局 NPC 修改；通过表中成员提供专用数据或辅助算法 |

### `Common/GlobalProjectiles`（3 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Common/GlobalProjectiles/ExampleProjectileModifications.cs` | public ExampleProjectileModifications : GlobalProjectile | SetTrail, SetStaticDefaults, OnHitNPC, PostAI | 全局弹幕修改；登记类型级静态数据；在更新 Hook 中驱动状态/AI；处理伤害、命中或闪避 |
| `Common/GlobalProjectiles/ExampleProjectileNetSync.cs` | public ExampleProjectileNetSync : GlobalProjectile | AppliesToEntity, OnSpawn, SendExtraAI, ReceiveExtraAI, AI | 全局弹幕修改；在更新 Hook 中驱动状态/AI；序列化并同步联机状态；控制生成或初始化 |
| `Common/GlobalProjectiles/ProjectileWithGrowingDamage.cs` | public ProjectileWithGrowingDamage : GlobalProjectile | IsLoadingEnabled, OnSpawn, OnHitNPC | 全局弹幕修改；控制生成或初始化；处理伤害、命中或闪避 |

### `Common/GlobalPylons`（1 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Common/GlobalPylons/ExampleGlobalPylon.cs` | public ExampleGlobalPylon : GlobalPylon | ValidTeleportCheck_PreNPCCount, PreDrawMapIcon, PreCanPlacePylon, ValidTeleportCheck_PreBiomeRequirements, PostValidTeleportCheck | 共享辅助类型；处理帧、特效或自定义绘制 |

### `Common/GlobalTiles`（2 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Common/GlobalTiles/ShakeTrees.cs` | public GlobalShakeTrees : GlobalTile | ShakeTree, PreShakeTree | 全局方块修改；通过表中成员提供专用数据或辅助算法 |
| `Common/GlobalTiles/SunflowerChanges.cs` | public SunflowerChanges : GlobalTile | SetStaticDefaults, Unload | 全局方块修改；加载、注册或清理；登记类型级静态数据 |

### `Common/GlobalWalls`（1 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Common/GlobalWalls/ExampleGlobalWall.cs` | public ExampleGlobalWall : GlobalWall | WallFrame | 全局墙修改；处理帧、特效或自定义绘制 |

### `Common/ItemDropRules/DropConditions`（3 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Common/ItemDropRules/DropConditions/ExampleDropCondition.cs` | public ExampleDropCondition : IItemDropRuleCondition | ExampleDropCondition, CanDrop, CanShowItemDropInUI, GetConditionDescription | 掉落条件；配置掉落规则 |
| `Common/ItemDropRules/DropConditions/ExampleJourneyModeDropCondition.cs` | public ExampleJourneyModeDropCondition : IItemDropRuleCondition | ExampleJourneyModeDropCondition, CanDrop, CanShowItemDropInUI, GetConditionDescription | 掉落条件；配置掉落规则 |
| `Common/ItemDropRules/DropConditions/ExampleSoulCondition.cs` | public ExampleSoulCondition : IItemDropRuleCondition | ExampleSoulCondition, CanDrop, CanShowItemDropInUI, GetConditionDescription | 掉落条件；配置掉落规则 |

### `Common/Players`（18 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Common/Players/ExampleAccessorySlot.cs` | public ExampleModAccessorySlot1 : ModAccessorySlot; public ExampleCustomLocationAndTextureSlot : ModAccessorySlot; public ExampleModWingSlot : ModAccessorySlot | IsHidden, BackgroundDrawColor, SetupContent, CanAcceptItem, ModifyDefaultSwapSlot, IsEnabled, IsVisibleWhenNotEnabled, OnMouseHover | 饰品槽；加载、注册或清理；处理帧、特效或自定义绘制 |
| `Common/Players/ExampleArmorSetBonusPlayer.cs` | public ExampleArmorSetBonusPlayer : ModPlayer | ResetEffects, ArmorSetBonusActivated, ArmorSetBonusHeld, DrawPlayer, TransformDrawData | 玩家扩展；处理帧、特效或自定义绘制 |
| `Common/Players/ExampleBlinkingPlayer.cs` | public ExampleBlinkingPlayer : ModPlayer | PostUpdate | 玩家扩展；在更新 Hook 中驱动状态/AI |
| `Common/Players/ExampleCostumePlayer.cs` | public ExampleCostumePlayer : ModPlayer | ResetEffects, UpdateEquips, FrameEffects, ModifyDrawInfo, ModifyHurt, OnHurt | 玩家扩展；处理帧、特效或自定义绘制；处理伤害、命中或闪避 |
| `Common/Players/ExampleDamageModificationPlayer.cs` | internal ExampleDamageModificationPlayer : ModPlayer | PreUpdate, ResetEffects, ModifyHitNPC, PostUpdateEquips, DrawEffects, ConsumableDodge, ExampleDodgeEffects, HandleExampleDodgeMessage, SendExampleDodgeMessage, ModifyHurt, OnHurt | 玩家扩展；在更新 Hook 中驱动状态/AI；处理帧、特效或自定义绘制；序列化并同步联机状态；处理伤害、命中或闪避 |
| `Common/Players/ExampleExtraJumpModificationPlayer.cs` | public ExampleExtraJumpModificationPlayer : ModPlayer | ModifyExtraJumpDurationMultiplier | 玩家扩展；通过表中成员提供专用数据或辅助算法 |
| `Common/Players/ExampleFishingPlayer.cs` | public ExampleFishingPlayer : ModPlayer | SetStaticDefaults, ResetEffects, ModifyFishingAttempt, CatchFish, CanConsumeBait, ModifyCaughtFish | 玩家扩展；登记类型级静态数据；处理帧、特效或自定义绘制 |
| `Common/Players/ExampleImmunityPlayer.cs` | public ExampleImmunityPlayer : ModPlayer | ResetEffects, PostHurt | 玩家扩展；处理帧、特效或自定义绘制；处理伤害、命中或闪避 |
| `Common/Players/ExampleInfoDisplayPlayer.cs` | public ExampleInfoDisplayPlayer : ModPlayer | ResetInfoAccessories, RefreshInfoAccessoriesFromTeamPlayers | 玩家扩展；通过表中成员提供专用数据或辅助算法 |
| `Common/Players/ExampleInventoryPlayer.cs` | public ExampleInventoryPlayer : ModPlayer | AddStartingItems, ModifyStartingInventory | 玩家扩展；通过表中成员提供专用数据或辅助算法 |
| `Common/Players/ExampleKeybindPlayer.cs` | public ExampleKeybindPlayer : ModPlayer | SetStaticDefaults, ProcessTriggers | 玩家扩展；登记类型级静态数据 |
| `Common/Players/ExampleLuckPlayer.cs` | public ExampleLuckPlayer : ModPlayer | ModifyLuck, PreModifyLuck | 玩家扩展；通过表中成员提供专用数据或辅助算法 |
| `Common/Players/ExampleRecipeMaterialPlayer.cs` | public ExampleRecipeMaterialPlayer : ModPlayer | PostUpdateMiscEffects, AddMaterialsForCrafting | 玩家扩展；处理帧、特效或自定义绘制 |
| `Common/Players/ExampleResourcePlayer.cs` | public ExampleResourcePlayer : ModPlayer | Initialize, ResetEffects, UpdateDead, PostUpdateMiscEffects, PostUpdate, HealExampleResource, HealExampleResourceEffect, HandleExampleResourceEffectMessage, SendExampleResourceEffectMessage | 玩家扩展；在更新 Hook 中驱动状态/AI；处理帧、特效或自定义绘制；序列化并同步联机状态 |
| `Common/Players/ExampleShiftClickSlotPlayer.cs` | public ExampleShiftClickSlotPlayer : ModPlayer | ShiftClickSlot, HoverSlot | 玩家扩展；通过表中成员提供专用数据或辅助算法 |
| `Common/Players/ExampleStatIncreasePlayer.cs` | public ExampleStatIncreasePlayer : ModPlayer | ModifyMaxStats, SyncPlayer, ReceivePlayerSync, CopyClientState, SendClientChanges, SaveData, LoadData | 玩家扩展；保存、读取或重置持久状态；序列化并同步联机状态 |
| `Common/Players/ExampleWeaponEnchantmentPlayer.cs` | public ExampleWeaponEnchantmentPlayer : ModPlayer | ResetEffects, OnHitNPCWithItem, OnHitNPCWithProj, MeleeEffects, EmitEnchantmentVisualsAt | 玩家扩展；处理帧、特效或自定义绘制；处理伤害、命中或闪避 |
| `Common/Players/SimpleModPlayer.cs` | public SimpleModPlayer : ModPlayer; public SimpleAccessory : ModItem | ResetEffects, OnHitNPCWithProj, SetDefaults, UpdateAccessory | 物品、玩家扩展；设置实体/物品实例默认值；处理帧、特效或自定义绘制；处理伤害、命中或闪避；把装备效果写入玩家状态 |

### `Common/Systems`（14 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Common/Systems/ChestItemWorldGen.cs` | public ChestItemWorldGen : ModSystem | PostWorldGen | 系统/生命周期；插入或执行世界生成 |
| `Common/Systems/DownedBossSystem.cs` | public DownedBossSystem : ModSystem | ClearWorld, SaveWorldData, LoadWorldData, NetSend, NetReceive | 系统/生命周期；保存、读取或重置持久状态；序列化并同步联机状态 |
| `Common/Systems/ExampleBiomeTileCount.cs` | public ExampleBiomeTileCount : ModSystem | TileCountsAvailable | 系统/生命周期；统计并判定生态激活 |
| `Common/Systems/ExampleGameTipsSystem.cs` | public ExampleGameTipsSystem : ModSystem | ModifyGameTipVisibility | 系统/生命周期；通过表中成员提供专用数据或辅助算法 |
| `Common/Systems/ExampleTownPetSystem.cs` | public ExampleTownPetSystem : ModSystem | ClearWorld, SaveWorldData, LoadWorldData, NetSend, NetReceive | 系统/生命周期；保存、读取或重置持久状态；序列化并同步联机状态 |
| `Common/Systems/ExampleWorldGenHookingSystem.cs` | public ExampleWorldGenHookingSystem : ModSystem | Load | 系统/生命周期；加载、注册或清理 |
| `Common/Systems/ExampleWorldHeaderSystem.cs` | public ExampleWorldHeaderSystem : ModSystem; public ExampleWorldHeaderPlayer : ModPlayer | SaveWorldHeader, Load, OnEnterWorld | 玩家扩展、系统/生命周期；加载、注册或清理 |
| `Common/Systems/KeybindSystem.cs` | public KeybindSystem : ModSystem | Load, Unload | 系统/生命周期；加载、注册或清理 |
| `Common/Systems/ModIntegrationsSystem.cs` | public ModIntegrationsSystem : ModSystem | PostSetupContent | 系统/生命周期；加载、注册或清理 |
| `Common/Systems/RubbleWorldGen.cs` | public RubbleWorldGen : ModSystem; public ExamplePilesPass : GenPass | ModifyWorldGenTasks, ExamplePilesPass, ApplyPass | 系统/生命周期、世界生成步骤；插入或执行世界生成 |
| `Common/Systems/SimpleDataAtParticularLocations.cs` | public SimpleDataAtParticularLocations : ModSystem | ClearWorld, SaveWorldData, LoadWorldData, PostWorldGen, PreUpdateWorld, UpdateFromNearestInMap | 系统/生命周期；在更新 Hook 中驱动状态/AI；保存、读取或重置持久状态；插入或执行世界生成 |
| `Common/Systems/StatueWorldGen.cs` | public StatueWorldGen : ModSystem | Load | 系统/生命周期；加载、注册或清理 |
| `Common/Systems/TownNPCRespawnSystem.cs` | public TownNPCRespawnSystem : ModSystem | ClearWorld, SaveWorldData, LoadWorldData, NetSend, NetReceive | 系统/生命周期；保存、读取或重置持久状态；序列化并同步联机状态 |
| `Common/Systems/TravelingMerchantSystem.cs` | public TravelingMerchantSystem : ModSystem | PreUpdateWorld, SaveWorldData, LoadWorldData, ClearWorld, NetSend, NetReceive | 系统/生命周期；在更新 Hook 中驱动状态/AI；保存、读取或重置持久状态；序列化并同步联机状态 |

### `Common/UI/ExampleCoinsUI`（4 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Common/UI/ExampleCoinsUI/ExampleCoinsUI.cs` | internal ExampleCoinsUIState : UIState; public UIMoneyDisplay : UIElement; public MoneyCounterGlobalItem : GlobalItem | OnInitialize, UpdateValue, UIMoneyDisplay, AddCoinsPerMinute, GetCoinsPerMinute, DrawSelf, ResetCoins, AppliesToEntity, OnPickup | 全局物品修改、UI 状态、UI 元素；处理帧、特效或自定义绘制；建立、更新或接入 UI 图层 |
| `Common/UI/ExampleCoinsUI/ExampleCoinsUISystem.cs` | public ExampleCoinsUISystem : ModSystem | ShowMyUI, HideMyUI, PostSetupContent, UpdateUI, ModifyInterfaceLayers | 系统/生命周期；加载、注册或清理；建立、更新或接入 UI 图层 |
| `Common/UI/ExampleCoinsUI/ExampleDraggableUIPanel.cs` | public ExampleDraggableUIPanel : UIPanel | LeftMouseDown, LeftMouseUp, Update | 共享辅助类型；在更新 Hook 中驱动状态/AI |
| `Common/UI/ExampleCoinsUI/ExampleUIHoverImageButton.cs` | internal ExampleUIHoverImageButton : UIImageButton | ExampleUIHoverImageButton, DrawSelf | 共享辅助类型；处理帧、特效或自定义绘制 |

### `Common/UI/ExampleDisplaySets`（1 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Common/UI/ExampleDisplaySets/ExampleReversedBarsDisplay.cs` | public ExampleReversedBarsDisplay : ModResourceDisplaySet | Load, DrawLife, DrawMana, PreHover, PreDrawResources | 资源条显示集；加载、注册或清理；处理帧、特效或自定义绘制 |

### `Common/UI/ExampleFullscreenUI`（1 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Common/UI/ExampleFullscreenUI/ExampleFullscreenUI.cs` | internal ExampleFullscreenUI : UIState, ILoadable | Load, Unload, OnInitialize, OnActivate, RefreshContents, UpdateConfigSaveStatusMessage | UI 状态、自定义加载器；加载、注册或清理；序列化并同步联机状态；建立、更新或接入 UI 图层 |

### `Common/UI/ExampleInGameNotification`（2 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Common/UI/ExampleInGameNotification/ExampleInGameNotificationPlayer.cs` | public ExampleInGameNotificationPlayer : ModPlayer | OnEnterWorld | 玩家扩展；通过表中成员提供专用数据或辅助算法 |
| `Common/UI/ExampleInGameNotification/ExampleJoinWorldInGameNotification.cs` | public ExampleJoinWorldInGameNotification : IInGameNotification | Update, DrawInGame, PushAnchor | 共享辅助类型；在更新 Hook 中驱动状态/AI；处理帧、特效或自定义绘制 |

### `Common/UI/ExampleResourceUI`（1 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Common/UI/ExampleResourceUI/ExampleResourceBar.cs` | internal ExampleResourceBar : UIState; internal ExampleResourceUISystem : ModSystem | OnInitialize, Draw, DrawSelf, Update, Load, UpdateUI, ModifyInterfaceLayers | 系统/生命周期、UI 状态；加载、注册或清理；在更新 Hook 中驱动状态/AI；处理帧、特效或自定义绘制；建立、更新或接入 UI 图层 |

### `Common/UI/ResourceOverlay`（2 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Common/UI/ResourceOverlay/VanillaLifeOverlay.cs` | public VanillaLifeOverlay : ModResourceOverlay | PostDrawResource | 资源条覆盖；处理帧、特效或自定义绘制 |
| `Common/UI/ResourceOverlay/VanillaManaOverlay.cs` | public VanillaManaOverlay : ModResourceOverlay | PostDrawResource | 资源条覆盖；处理帧、特效或自定义绘制 |

### `Content`（3 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Content/ExampleInfoDisplay.cs` | public ExampleInfoDisplay : InfoDisplay | SetStaticDefaults, Active, DisplayValue | 信息显示；登记类型级静态数据 |
| `Content/ExampleModMenu.cs` | public ExampleModMenu : ModMenu | Load, OnSelected, PreDrawLogo | 模组菜单；加载、注册或清理；处理帧、特效或自定义绘制 |
| `Content/ExampleRecipes.cs` | public ExampleRecipes : ModSystem | Unload, AddRecipeGroups, AddRecipes, PostAddRecipes | 系统/生命周期；加载、注册或清理；注册或调整配方 |

### `Content/Achievements`（3 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Content/Achievements/AdvancedExampleAchievement.cs` | public AdvancedExampleAchievement : ModAchievement; public CustomTracker : ConditionFloatTracker | SetStaticDefaults, GetModdedConstraints, OnCompleted, CustomTracker, Load | 成就；加载、注册或清理；登记类型级静态数据 |
| `Content/Achievements/ManyExampleWormsKilled.cs` | public ManyExampleWormsKilled : ModAchievement | SetStaticDefaults, Unload | 成就；加载、注册或清理；登记类型级静态数据 |
| `Content/Achievements/MinionBossKilled.cs` | public MinionBossKilled : ModAchievement | SetStaticDefaults, GetDefaultPosition, GetAdvisorPosition | 成就；登记类型级静态数据 |

### `Content/Biomes`（7 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Content/Biomes/ExampleDroplet.cs` | public ExampleDroplet : ModGore | SetStaticDefaults | Gore/视觉碎片；登记类型级静态数据 |
| `Content/Biomes/ExampleSurfaceBackgroundStyle.cs` | public ExampleSurfaceBackgroundStyle : ModSurfaceBackgroundStyle | ModifyFarFades, ChooseFarTexture, ChooseMiddleTexture, ChooseCloseTexture | 地表背景；通过表中成员提供专用数据或辅助算法 |
| `Content/Biomes/ExampleSurfaceBiome.cs` | public ExampleSurfaceBiome : ModBiome | IsBiomeActive | 生态；统计并判定生态激活 |
| `Content/Biomes/ExampleUndergroundBackgroundStyle.cs` | public ExampleUndergroundBackgroundStyle : ModUndergroundBackgroundStyle | FillTextureArray | 地下背景；通过表中成员提供专用数据或辅助算法 |
| `Content/Biomes/ExampleUndergroundBiome.cs` | public ExampleUndergroundBiome : ModBiome | IsBiomeActive, GetWeight | 生态；统计并判定生态激活 |
| `Content/Biomes/ExampleWaterfallStyle.cs` | public ExampleWaterfallStyle : ModWaterfallStyle | AddLight | 瀑布样式；处理帧、特效或自定义绘制 |
| `Content/Biomes/ExampleWaterStyle.cs` | public ExampleWaterStyle : ModWaterStyle | Load, ChooseWaterfallStyle, GetSplashDust, GetDropletGore, LightColorMultiplier, BiomeHairColor, GetRainVariant, GetRainTexture | 水体样式；加载、注册或清理；处理帧、特效或自定义绘制；配置掉落规则 |

### `Content/BossBars`（2 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Content/BossBars/ExampleBossBar.cs` | public ExampleBossBar : ModBossBar | GetIconTexture, PreDraw | Boss 血条；处理帧、特效或自定义绘制 |
| `Content/BossBars/MinionBossBossBar.cs` | public MinionBossBossBar : ModBossBar | GetIconTexture, ModifyInfo | Boss 血条；通过表中成员提供专用数据或辅助算法 |

### `Content/BossBarStyles`（1 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Content/BossBarStyles/ExampleBossBarStyle.cs` | public ExampleBossBarStyle : ModBossBarStyle | Draw | Boss 血条样式；处理帧、特效或自定义绘制 |

### `Content/Buffs`（15 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Content/Buffs/AbsorbTeamDamageBuff.cs` | public AbsorbTeamDamageBuff : ModBuff | SetStaticDefaults, Update | Buff/Debuff；登记类型级静态数据；在更新 Hook 中驱动状态/AI |
| `Content/Buffs/AnimatedBuff.cs` | public AnimatedBuff : ModBuff | SetStaticDefaults, PreDraw, Update | Buff/Debuff；登记类型级静态数据；在更新 Hook 中驱动状态/AI；处理帧、特效或自定义绘制 |
| `Content/Buffs/Blocky.cs` | public Blocky : ModBuff | SetStaticDefaults, Update | Buff/Debuff；登记类型级静态数据；在更新 Hook 中驱动状态/AI |
| `Content/Buffs/ExampleCrateBuff.cs` | public ExampleCrateBuff : ModBuff | Update | Buff/Debuff；在更新 Hook 中驱动状态/AI |
| `Content/Buffs/ExampleCrowdControlledDebuff.cs` | public ExampleCrowdControlledDebuff : ModBuff; public ExampleCrowdControlledDebuffPlayer : ModPlayer | SetStaticDefaults, Update, ResetEffects, PostUpdateMiscEffects, DrawEffects | 玩家扩展、Buff/Debuff；登记类型级静态数据；在更新 Hook 中驱动状态/AI；处理帧、特效或自定义绘制 |
| `Content/Buffs/ExampleDefenseBuff.cs` | public ExampleDefenseBuff : ModBuff | Update | Buff/Debuff；在更新 Hook 中驱动状态/AI |
| `Content/Buffs/ExampleDefenseDebuff.cs` | public ExampleDefenseDebuff : ModBuff | SetStaticDefaults, Update | Buff/Debuff；登记类型级静态数据；在更新 Hook 中驱动状态/AI |
| `Content/Buffs/ExampleDodgeBuff.cs` | internal ExampleDodgeBuff : ModBuff | SetStaticDefaults, Update | Buff/Debuff；登记类型级静态数据；在更新 Hook 中驱动状态/AI |
| `Content/Buffs/ExampleGravityDebuff.cs` | public ExampleGravityDebuff : ModBuff | Update | Buff/Debuff；在更新 Hook 中驱动状态/AI |
| `Content/Buffs/ExampleJavelinDebuff.cs` | public ExampleJavelinDebuff : ModBuff | SetStaticDefaults, Update | Buff/Debuff；登记类型级静态数据；在更新 Hook 中驱动状态/AI |
| `Content/Buffs/ExampleLifeRegenDebuff.cs` | public ExampleLifeRegenDebuff : ModBuff; public ExampleLifeRegenDebuffPlayer : ModPlayer | SetStaticDefaults, Update, ResetEffects, UpdateBadLifeRegen | 玩家扩展、Buff/Debuff；登记类型级静态数据；在更新 Hook 中驱动状态/AI；处理帧、特效或自定义绘制 |
| `Content/Buffs/ExampleMinecartBuff.cs` | public ExampleMinecartBuff : ModBuff | SetStaticDefaults | Buff/Debuff；登记类型级静态数据 |
| `Content/Buffs/ExampleMountBuff.cs` | public ExampleMountBuff : ModBuff | SetStaticDefaults, Update | Buff/Debuff；登记类型级静态数据；在更新 Hook 中驱动状态/AI |
| `Content/Buffs/ExampleWeaponImbue.cs` | public ExampleWeaponImbue : ModBuff | SetStaticDefaults, Update | Buff/Debuff；登记类型级静态数据；在更新 Hook 中驱动状态/AI |
| `Content/Buffs/ExampleWhipAdvancedPlayerBuff.cs` | public ExampleWhipAdvancedPlayerBuff : ModBuff | Update | Buff/Debuff；在更新 Hook 中驱动状态/AI |

### `Content/BuilderToggles`（2 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Content/BuilderToggles/ExampleBuilderToggle.cs` | public ExampleBuilderToggle : BuilderToggle; public ExampleBuilderToggleDimmedLight : BuilderToggle | SetStaticDefaults, Active, DisplayValue, Draw, OnRightClick | 建筑开关；登记类型级静态数据；处理帧、特效或自定义绘制 |
| `Content/BuilderToggles/FreeBaitBuilderToggle.cs` | public FreeBaitBuilderToggle : BuilderToggle | Active, OnLeftClick, OnRightClick, Draw, DrawHover, SetStaticDefaults, DisplayValue | 建筑开关；登记类型级静态数据；处理帧、特效或自定义绘制 |

### `Content/Clouds`（2 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Content/Clouds/AdvancedExampleCloud.cs` | public AdvancedExampleCloud : ModCloud | SpawnChance, OnSpawn, Draw | 云；处理帧、特效或自定义绘制；控制生成或初始化 |
| `Content/Clouds/DefaultCloudsLoader.cs` | public DefaultCloudsLoader : ICustomAutoload | Autoload | 自定义自动加载；加载、注册或清理 |

### `Content/Currencies`（1 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Content/Currencies/ExampleCustomCurrency.cs` | public ExampleCustomCurrency : CustomCurrencySingleCoin; public sealed ExampleCustomCurrencies : ModSystem | ExampleCustomCurrency, PostSetupContent | 系统/生命周期、自定义货币；加载、注册或清理 |

### `Content/CustomModType`（7 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Content/CustomModType/HandsUpVictoryPose.cs` | public HandsUpVictoryPose : ModVictoryPose | SetStaticDefaults, OnStartPose, Update | 自定义内容类型框架；登记类型级静态数据；在更新 Hook 中驱动状态/AI |
| `Content/CustomModType/HandsUpWithFireworksVictoryPose.cs` | public HandsUpWithFireworksVictoryPose : ModVictoryPose | SetStaticDefaults, OnStartPose, Update, OnEndPose | 自定义内容类型框架；登记类型级静态数据；在更新 Hook 中驱动状态/AI |
| `Content/CustomModType/ModVictoryPose.cs` | public abstract ModVictoryPose : ModTexturedType, ILocalizedModType | Register, SetupContent, ElapsedPoseTime, OnStartPose, Update, OnEndPose, GetTextureFrame | 自定义内容类型、自定义内容类型框架；加载、注册或清理；在更新 Hook 中驱动状态/AI；处理帧、特效或自定义绘制 |
| `Content/CustomModType/NonAutoloadVictoryPose.cs` | public NonAutoloadVictoryPose : ModVictoryPose, ICustomAutoload | Autoload, NonAutoloadVictoryPose, SetStaticDefaults, GetTextureFrame, OnStartPose, Update | 自定义自动加载、自定义内容类型框架；加载、注册或清理；登记类型级静态数据；在更新 Hook 中驱动状态/AI；处理帧、特效或自定义绘制 |
| `Content/CustomModType/VictoryPoseID.cs` | public VictoryPoseID; public static Sets | — | 自定义内容类型框架；通过表中成员提供专用数据或辅助算法 |
| `Content/CustomModType/VictoryPoseLoader.cs` | public VictoryPoseLoader | Add, StartPose, CancelPose, GetActivePose | 自定义内容类型框架；通过表中成员提供专用数据或辅助算法 |
| `Content/CustomModType/VictoryPosePlayer.cs` | internal VictoryPosePlayer : ModPlayer; public PoseIconParticle : IParticle | OnHitNPC, StartPose, EndPose, PostUpdate, HandleStartVictoryPoseMessage, SendStartVictoryPoseMessage, HandleCancelVictoryPoseMessage, SendCancelVictoryPoseMessage, PoseIconParticle, Update, Draw | 玩家扩展、自定义内容类型框架；在更新 Hook 中驱动状态/AI；处理帧、特效或自定义绘制；序列化并同步联机状态；处理伤害、命中或闪避 |

### `Content/DamageClasses`（1 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Content/DamageClasses/ExampleDamageClass.cs` | public ExampleDamageClass : DamageClass | GetModifierInheritance, GetEffectInheritance, SetDefaultStats, ShowStatTooltipLine | 伤害类型；通过表中成员提供专用数据或辅助算法 |

### `Content/Dusts`（5 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Content/Dusts/ExampleAdvancedDust.cs` | internal ExampleAdvancedDust : ModDust | OnSpawn, Update | 粒子；在更新 Hook 中驱动状态/AI；控制生成或初始化 |
| `Content/Dusts/ExampleBubble.cs` | public ExampleBubble : ModDust | OnSpawn, Update | 粒子；在更新 Hook 中驱动状态/AI；控制生成或初始化 |
| `Content/Dusts/ExampleCustomDrawDust.cs` | public ExampleCustomDrawDust : ModDust | OnSpawn, GetAlpha, PreDraw | 粒子；处理帧、特效或自定义绘制；控制生成或初始化 |
| `Content/Dusts/ExampleSolutionDust.cs` | public ExampleSolutionDust : ModDust | SetStaticDefaults | 粒子；登记类型级静态数据 |
| `Content/Dusts/Sparkle.cs` | public Sparkle : ModDust | OnSpawn, Update | 粒子；在更新 Hook 中驱动状态/AI；控制生成或初始化 |

### `Content/EmoteBubbles`（5 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Content/EmoteBubbles/ExampleBiomeEmote.cs` | public ExampleBiomeEmote : ModEmoteBubble | SetStaticDefaults, PreDraw, PreDrawInEmoteMenu | 表情；登记类型级静态数据；处理帧、特效或自定义绘制 |
| `Content/EmoteBubbles/ExampleItemEmote.cs` | public ExampleItemEmote : ModEmoteBubble | SetStaticDefaults | 表情；登记类型级静态数据 |
| `Content/EmoteBubbles/ExamplePickaxeEmote.cs` | public ExamplePickaxeEmote : ModEmoteBubble | SetStaticDefaults | 表情；登记类型级静态数据 |
| `Content/EmoteBubbles/MinionBossEmote.cs` | public MinionBossEmote : ModEmoteBubble | SetStaticDefaults, IsUnlocked | 表情；登记类型级静态数据 |
| `Content/EmoteBubbles/NPCEmotes.cs` | public abstract ModTownEmote : ModEmoteBubble; public ExamplePersonEmote : ModTownEmote; public ExampleTravellingMerchantEmote : ModTownEmote; public ExampleBoneMerchantEmote : ModTownEmote | SetStaticDefaults, GetFrame, GetFrameInEmoteMenu, OnSpawn | 表情；登记类型级静态数据；处理帧、特效或自定义绘制；控制生成或初始化 |

### `Content/Hairs`（1 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Content/Hairs/ExampleHair.cs` | public ExampleHair : ModHair | SetStaticDefaults, GetUnlockConditions | 发型；登记类型级静态数据 |

### `Content/Items`（23 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Content/Items/ActiveSoundShowcase.cs` | public ActiveSoundShowcase : ModItem | SetDefaults, Shoot, HoldItem, AddRecipes | 物品；设置实体/物品实例默认值；注册或调整配方；控制射击、弹药或生成弹幕 |
| `Content/Items/CameraModifierShowcase.cs` | public CameraModifierShowcase : ModItem | SetDefaults, UseItem | 物品；设置实体/物品实例默认值；控制物品使用与消耗 |
| `Content/Items/CustomItemDrawingShowcase.cs` | public CustomItemDrawingShowcase : ModItem | Load, SetStaticDefaults, SetDefaults, CanRightClick, ConsumeItem, RightClick, ModifyTooltips, PreDrawInInventory, PostDrawInInventory, PreDrawInWorld, PostDrawInWorld, HoldStyle, ModifyItemDraw | 物品；加载、注册或清理；登记类型级静态数据；设置实体/物品实例默认值；处理帧、特效或自定义绘制；控制物品使用与消耗 |
| `Content/Items/CustomItemSets.cs` | public static CustomItemSets; public CustomItemSetsSystem : ModSystem; public CustomSetsModPlayer : ModPlayer | Load, ResizeArrays, SetStaticDefaults, OnHitAnything | 玩家扩展、系统/生命周期；加载、注册或清理；登记类型级静态数据；处理伤害、命中或闪避 |
| `Content/Items/ExampleBasicFish.cs` | public ExampleBasicFish : ModItem | SetStaticDefaults, SetDefaults, AddRecipes | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/ExampleDataItem.cs` | public ExampleDataItem : ModItem | SetStaticDefaults, ModifyTooltips, UpdateInventory, AddRecipes | 物品；登记类型级静态数据；注册或调整配方 |
| `Content/Items/ExampleDye.cs` | public ExampleDye : ModItem | SetStaticDefaults, SetDefaults | 物品；登记类型级静态数据；设置实体/物品实例默认值 |
| `Content/Items/ExampleGolfBall.cs` | public ExampleGolfBall : ModItem | SetDefaults, ModifyResearchSorting | 物品；设置实体/物品实例默认值 |
| `Content/Items/ExampleHairDye.cs` | public ExampleHairDye : ModItem | SetStaticDefaults, SetDefaults | 物品；登记类型级静态数据；设置实体/物品实例默认值 |
| `Content/Items/ExampleInstancedItem.cs` | public ExampleInstancedItem : ModItem | SetStaticDefaults, SetDefaults, Clone, OnCreated, ModifyTooltips, UseAnimation, SaveData, LoadData, AddRecipes | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方；保存、读取或重置持久状态 |
| `Content/Items/ExampleItem.cs` | public ExampleItem : ModItem | SetStaticDefaults, SetDefaults, AddRecipes, OnResearched | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/ExampleOnBuyItem.cs` | public ExampleOnBuyItem : ModItem | SetStaticDefaults, SetDefaults, OnCreated | 物品；登记类型级静态数据；设置实体/物品实例默认值 |
| `Content/Items/ExamplePaperAirplane.cs` | public ExamplePaperAirplane : ModItem | SetDefaults, AddRecipes | 物品；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/ExampleQuestFish.cs` | public ExampleQuestFish : ModItem | SetStaticDefaults, SetDefaults, IsAnglerQuestAvailable, AnglerQuestChat | 物品；登记类型级静态数据；设置实体/物品实例默认值；处理商店、聊天或交互 |
| `Content/Items/ExampleResearchPresent.cs` | public ExampleResearchPresent : ModItem | SetStaticDefaults, SetDefaults, OnResearched | 物品；登记类型级静态数据；设置实体/物品实例默认值 |
| `Content/Items/ExampleResourcePickup.cs` | public ExampleResourcePickup : ModItem | SetStaticDefaults, SetDefaults, OnPickup, GrabRange | 物品；登记类型级静态数据；设置实体/物品实例默认值 |
| `Content/Items/ExampleSignItem.cs` | public ExampleSignItem : ModItem | SetDefaults, AddRecipes | 物品；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/ExampleSoul.cs` | public ExampleSoul : ModItem | SetStaticDefaults, SetDefaults, PostUpdate, GetAlpha, AddRecipes | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方；在更新 Hook 中驱动状态/AI |
| `Content/Items/ExampleStackableDurabilityItem.cs` | public ExampleStackableDurabilityItem : ModItem | SetStaticDefaults, SetDefaults, SaveData, LoadData, NetSend, NetReceive, PostDrawInInventory, ModifyTooltips, OnStack, OnCreated, AddRecipes | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方；处理帧、特效或自定义绘制；保存、读取或重置持久状态 |
| `Content/Items/ExampleTooltipsItem.cs` | public ExampleTooltipsItem : ModItem | SetStaticDefaults, SetDefaults, GetAlpha, ModifyTooltips, AddRecipes | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/HoldStyleShowcase.cs` | public HoldStyleShowcase : ModItem | SetStaticDefaults, SetDefaults, NetSend, NetReceive, AltFunctionUse, UseItem | 物品；登记类型级静态数据；设置实体/物品实例默认值；序列化并同步联机状态；控制物品使用与消耗 |
| `Content/Items/ShimmerShowcase.cs` | public ShimmerShowcaseConditions : ModItem; public ShimmerShowcaseCustomShimmerResult : ModItem | SetDefaults, AddRecipes | 物品；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/UseStyleShowcase.cs` | public UseStyleShowcase : ModItem | SetStaticDefaults, SetDefaults, NetSend, NetReceive, AltFunctionUse, UseItem | 物品；登记类型级静态数据；设置实体/物品实例默认值；序列化并同步联机状态；控制物品使用与消耗 |

### `Content/Items/Accessories`（14 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Content/Items/Accessories/AbsorbTeamDamageAccessory.cs` | public AbsorbTeamDamageAccessory : ModItem | SetDefaults, UpdateAccessory | 物品；设置实体/物品实例默认值；把装备效果写入玩家状态 |
| `Content/Items/Accessories/ExampleBeard.cs` | public ExampleBeard : ModItem | SetStaticDefaults, SetDefaults | 物品；登记类型级静态数据；设置实体/物品实例默认值 |
| `Content/Items/Accessories/ExampleBoots.cs` | public ExampleBoots : ModItem | SetDefaults, UpdateAccessory, UpdateVanity | 物品；设置实体/物品实例默认值；把装备效果写入玩家状态 |
| `Content/Items/Accessories/ExampleCustomDrawWings.cs` | public ExampleCustomDrawWings : ModItem | Load, SetStaticDefaults, SetDefaults, VerticalWingSpeeds, AddRecipes, ModifyEquipTextureDraw, WingUpdate | 物品；加载、注册或清理；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方；处理帧、特效或自定义绘制 |
| `Content/Items/Accessories/ExampleExtraJumpAccessory.cs` | public ExampleExtraJumpAccessory : ModItem; public SimpleExtraJump : ExtraJump | SetDefaults, UpdateAccessory, AddRecipes, GetDefaultPosition, GetModdedConstraints, GetDurationMultiplier, UpdateHorizontalSpeeds, OnStarted, ShowVisuals | 物品、额外跳跃；设置实体/物品实例默认值；注册或调整配方；把装备效果写入玩家状态 |
| `Content/Items/Accessories/ExampleImmunityAccessory.cs` | public ExampleImmunityAccessory : ModItem | SetDefaults, UpdateAccessory | 物品；设置实体/物品实例默认值；把装备效果写入玩家状态 |
| `Content/Items/Accessories/ExampleInfoAccessory.cs` | public ExampleInfoAccessory : ModItem | SetStaticDefaults, SetDefaults, UpdateInfoAccessory, AddRecipes | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Accessories/ExampleMultiExtraJumpAccessory.cs` | public ExampleMultiExtraJumpAccessory : ModItem; public MultipleUseExtraJump : ExtraJump; public MultipleUseExtraJumpPlayer : ModPlayer | SetDefaults, UpdateAccessory, AddRecipes, ModifyTooltips, GetDefaultPosition, GetDurationMultiplier, OnRefreshed, OnStarted | 物品、玩家扩展、额外跳跃；设置实体/物品实例默认值；注册或调整配方；把装备效果写入玩家状态 |
| `Content/Items/Accessories/ExamplePotionDelayAccessory.cs` | public ExamplePotionDelayAccessory : ModItem | SetDefaults, UpdateAccessory | 物品；设置实体/物品实例默认值；把装备效果写入玩家状态 |
| `Content/Items/Accessories/ExampleResourceAccessory.cs` | public ExampleResourceAccessory : ModItem | SetDefaults, UpdateAccessory | 物品；设置实体/物品实例默认值；把装备效果写入玩家状态 |
| `Content/Items/Accessories/ExampleShield.cs` | public ExampleShield : ModItem; public ExampleDashPlayer : ModPlayer | SetDefaults, UpdateAccessory, AddRecipes, ResetEffects, PreUpdateMovement | 物品、玩家扩展；设置实体/物品实例默认值；注册或调整配方；处理帧、特效或自定义绘制；把装备效果写入玩家状态 |
| `Content/Items/Accessories/ExampleStatBonusAccessory.cs` | public ExampleStatBonusAccessory : ModItem; public ExampleStatBonusAccessoryPlayer : ModPlayer | SetDefaults, UpdateAccessory, ResetEffects, PostUpdateRunSpeeds | 物品、玩家扩展；设置实体/物品实例默认值；处理帧、特效或自定义绘制；把装备效果写入玩家状态 |
| `Content/Items/Accessories/ExampleWings.cs` | public ExampleWings : ModItem | IsLoadingEnabled, SetStaticDefaults, SetDefaults, VerticalWingSpeeds, AddRecipes | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Accessories/WaspNest.cs` | public WaspNest : ModItem; public WaspNestPlayer : ModPlayer | Load, SetDefaults, UpdateAccessory, CanAccessoryBeEquippedWith, ResetEffects, OnHurt | 物品、玩家扩展；加载、注册或清理；设置实体/物品实例默认值；处理帧、特效或自定义绘制；处理伤害、命中或闪避；把装备效果写入玩家状态 |

### `Content/Items/Ammo`（7 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Content/Items/Ammo/ExampleArrow.cs` | public ExampleArrow : ModItem | SetStaticDefaults, SetDefaults, AddRecipes | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Ammo/ExampleBullet.cs` | public ExampleBullet : ModItem | SetStaticDefaults, SetDefaults, AddRecipes | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Ammo/ExampleCustomAmmo.cs` | public ExampleCustomAmmo : ModItem | SetStaticDefaults, SetDefaults, AddRecipes | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Ammo/ExampleGravityDebuffBullet.cs` | public ExampleGravityDebuffBullet : ModItem | SetStaticDefaults, SetDefaults, AddRecipes | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Ammo/ExampleHellSolution.cs` | public ExampleHellSolution : ModItem; public ExampleHellSolutionProjectile : ModProjectile; public ExampleHellSolutionConversion : ModBiomeConversion | SetStaticDefaults, SetDefaults, ModifyResearchSorting, CanDamage, AI, PostSetupContent, HellifyGrass, FindAndConvertTree, HellifyWall | 弹幕、物品；加载、注册或清理；登记类型级静态数据；设置实体/物品实例默认值；在更新 Hook 中驱动状态/AI；处理伤害、命中或闪避 |
| `Content/Items/Ammo/ExampleRocket.cs` | public ExampleRocket : ModItem | SetStaticDefaults, SetDefaults, AddRecipes | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Ammo/ExampleSolution.cs` | public ExampleSolution : ModItem; public ExampleSolutionProjectile : ModProjectile; public ExampleSolutionConversion : ModBiomeConversion | SetStaticDefaults, SetDefaults, ModifyResearchSorting, CanDamage, AI, PostSetupContent, ConvertStone, FindAndConvertTree, ConvertChairs, ConvertWorkbenches, ConvertWalls | 弹幕、物品；加载、注册或清理；登记类型级静态数据；设置实体/物品实例默认值；在更新 Hook 中驱动状态/AI；处理伤害、命中或闪避 |

### `Content/Items/Armor`（6 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Content/Items/Armor/ExampleBreastplate.cs` | public ExampleBreastplate : ModItem | SetDefaults, UpdateEquip, AddRecipes | 物品；设置实体/物品实例默认值；注册或调整配方；把装备效果写入玩家状态 |
| `Content/Items/Armor/ExampleCostume.cs` | public ExampleCostume : ModItem; public BlockyHead : EquipTexture | Load, SetStaticDefaults, SetDefaults, UpdateAccessory, UpdateVanity, IsVanitySet, UpdateVanitySet | 物品；加载、注册或清理；登记类型级静态数据；设置实体/物品实例默认值；把装备效果写入玩家状态 |
| `Content/Items/Armor/ExampleHelmet.cs` | public ExampleHelmet : ModItem | SetStaticDefaults, SetDefaults, IsArmorSet, UpdateArmorSet, AddRecipes | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方；把装备效果写入玩家状态 |
| `Content/Items/Armor/ExampleHood.cs` | public ExampleHood : ModItem | SetStaticDefaults, SetDefaults, IsArmorSet, UpdateArmorSet, ArmorSetShadows, AddRecipes | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方；把装备效果写入玩家状态 |
| `Content/Items/Armor/ExampleLeggings.cs` | public ExampleLeggings : ModItem | SetDefaults, UpdateEquip, AddRecipes | 物品；设置实体/物品实例默认值；注册或调整配方；把装备效果写入玩家状态 |
| `Content/Items/Armor/ExampleTallHelmet.cs` | public ExampleTallHelmet : ModItem | SetStaticDefaults, SetDefaults, AddRecipes | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方 |

### `Content/Items/Armor/Vanity`（2 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Content/Items/Armor/Vanity/ExampleRobe.cs` | public ExampleRobe : ModItem | Load, SetStaticDefaults, SetDefaults, SetMatch | 物品；加载、注册或清理；登记类型级静态数据；设置实体/物品实例默认值 |
| `Content/Items/Armor/Vanity/MinionBossMask.cs` | public MinionBossMask : ModItem | SetDefaults | 物品；设置实体/物品实例默认值 |

### `Content/Items/Consumables`（14 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Content/Items/Consumables/ExampleBuffPotion.cs` | public ExampleBuffPotion : ModItem | SetStaticDefaults, SetDefaults | 物品；登记类型级静态数据；设置实体/物品实例默认值 |
| `Content/Items/Consumables/ExampleCanStackItem.cs` | public ExampleCanStackItem : ModItem | SetStaticDefaults, SetDefaults, CanRightClick, CanStack, OnStack, ModifyItemLoot, SaveData, LoadData, NetSend, NetReceive, ModifyTooltips, OnCreated, AddRecipes | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方；保存、读取或重置持久状态；序列化并同步联机状态 |
| `Content/Items/Consumables/ExampleCratePotion.cs` | public ExampleCratePotion : ModItem | SetStaticDefaults, SetDefaults, AddRecipes | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Consumables/ExampleFishingCrate.cs` | public ExampleFishingCrate : ModItem | SetStaticDefaults, SetDefaults, ModifyResearchSorting, CanRightClick, ModifyItemLoot | 物品；登记类型级静态数据；设置实体/物品实例默认值；配置掉落规则 |
| `Content/Items/Consumables/ExampleFlask.cs` | public ExampleFlask : ModItem | SetStaticDefaults, SetDefaults, AddRecipes | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Consumables/ExampleFoodItem.cs` | public ExampleFoodItem : ModItem | SetStaticDefaults, SetDefaults, OnConsumeItem, AddRecipes | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Consumables/ExampleHealingPotion.cs` | public ExampleHealingPotion : ModItem | SetStaticDefaults, SetDefaults, ModifyTooltips, GetHealLife, ModifyPotionDelay, AddRecipes | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Consumables/ExampleLifeFruit.cs` | internal ExampleLifeFruit : ModItem | SetStaticDefaults, SetDefaults, CanUseItem, UseItem, AddRecipes | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方；控制物品使用与消耗 |
| `Content/Items/Consumables/ExampleManaCrystal.cs` | internal ExampleManaCrystal : ModItem | SetStaticDefaults, SetDefaults, CanUseItem, UseItem, AddRecipes | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方；控制物品使用与消耗 |
| `Content/Items/Consumables/ExampleMultiUseItem.cs` | public ExampleMultiUseItem : ModItem | SetDefaults, SaveData, LoadData, NetSend, NetReceive, ConsumeItem, PostDrawInInventory, OnStack, SplitStack, AddRecipes | 物品；设置实体/物品实例默认值；注册或调整配方；处理帧、特效或自定义绘制；保存、读取或重置持久状态；序列化并同步联机状态 |
| `Content/Items/Consumables/ExampleTownPetLicense.cs` | public ExampleTownPetLicense : ModItem | SetStaticDefaults, SetDefaults, UseItem, ExampleTownPetUnlockOrExchangePet | 物品；登记类型级静态数据；设置实体/物品实例默认值；控制物品使用与消耗 |
| `Content/Items/Consumables/MinionBossBag.cs` | public MinionBossBag : ModItem | SetStaticDefaults, SetDefaults, CanRightClick, ModifyItemLoot | 物品；登记类型级静态数据；设置实体/物品实例默认值；配置掉落规则 |
| `Content/Items/Consumables/MinionBossSummonItem.cs` | public MinionBossSummonItem : ModItem | SetStaticDefaults, SetDefaults, ModifyResearchSorting, CanUseItem, UseItem, AddRecipes | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方；控制物品使用与消耗 |
| `Content/Items/Consumables/PlanteraItem.cs` | public PlanteraItem : ModItem | SetStaticDefaults, SetDefaults, ModifyResearchSorting, CanUseItem, UseItem, AddRecipes | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方；控制物品使用与消耗 |

### `Content/Items/Mounts`（2 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Content/Items/Mounts/ExampleMinecart.cs` | public ExampleMinecart : ModItem | SetDefaults, AddRecipes | 物品；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Mounts/ExampleMountItem.cs` | public ExampleMountItem : ModItem | SetDefaults, AddRecipes | 物品；设置实体/物品实例默认值；注册或调整配方 |

### `Content/Items/Placeable`（22 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Content/Items/Placeable/ExampleBar.cs` | public ExampleBar : ModItem | SetStaticDefaults, SetDefaults, AddRecipes | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Placeable/ExampleBlock.cs` | public ExampleBlock : ModItem | SetStaticDefaults, SetDefaults, AddRecipes, ExtractinatorUse | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Placeable/ExampleCampfire.cs` | public ExampleCampfire : ModItem | SetDefaults, AddRecipes | 物品；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Placeable/ExampleCutTile.cs` | public ExampleCutTile : ModItem | SetStaticDefaults, SetDefaults, AddRecipes | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Placeable/ExampleGem.cs` | public ExampleGem : ModItem | SetDefaults | 物品；设置实体/物品实例默认值 |
| `Content/Items/Placeable/ExampleGemsparkBlock.cs` | public ExampleGemsparkBlock : ModItem | SetDefaults, AddRecipes | 物品；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Placeable/ExampleHerbSeeds.cs` | public ExampleHerbSeeds : ModItem | SetStaticDefaults, SetDefaults, AddRecipes | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Placeable/ExampleLamp.cs` | internal ExampleLamp : ModItem | SetDefaults, AddRecipes | 物品；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Placeable/ExampleLivingFire.cs` | public ExampleLivingFire : ModItem | SetStaticDefaults, SetDefaults, PostUpdate, AddRecipes | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方；在更新 Hook 中驱动状态/AI |
| `Content/Items/Placeable/ExampleMusicBox.cs` | public ExampleMusicBox : ModItem | SetStaticDefaults, SetDefaults | 物品；登记类型级静态数据；设置实体/物品实例默认值 |
| `Content/Items/Placeable/ExampleOre.cs` | public ExampleOre : ModItem | SetStaticDefaults, SetDefaults | 物品；登记类型级静态数据；设置实体/物品实例默认值 |
| `Content/Items/Placeable/ExamplePressurePlate.cs` | public ExamplePressurePlate : ModItem | SetStaticDefaults, SetDefaults | 物品；登记类型级静态数据；设置实体/物品实例默认值 |
| `Content/Items/Placeable/ExamplePylonItem.cs` | public ExamplePylonItem : ModItem | SetDefaults | 物品；设置实体/物品实例默认值 |
| `Content/Items/Placeable/ExamplePylonItemAdvanced.cs` | public ExamplePylonItemAdvanced : ModItem | SetDefaults | 物品；设置实体/物品实例默认值 |
| `Content/Items/Placeable/ExampleSandBlock.cs` | public ExampleSandBlock : ModItem | SetStaticDefaults, SetDefaults, AddRecipes | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Placeable/ExampleSlopedTile.cs` | public ExampleSlopedTile : ModItem | SetDefaults, AddRecipes | 物品；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Placeable/ExampleStatue.cs` | public ExampleStatue : ModItem | SetDefaults, AddRecipes | 物品；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Placeable/ExampleTorch.cs` | public ExampleTorch : ModItem | SetStaticDefaults, SetDefaults, HoldItem, PostUpdate, AddRecipes | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方；在更新 Hook 中驱动状态/AI |
| `Content/Items/Placeable/ExampleTrap.cs` | public ExampleTrap : ModItem, ICustomAutoload | Autoload, GetInternalNameFromStyle, ExampleTrap, SetDefaults, AddRecipes | 物品、自定义自动加载；加载、注册或清理；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Placeable/ExampleWall.cs` | public ExampleWall : ModItem | SetStaticDefaults, SetDefaults, AddRecipes | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Placeable/ExampleWallAdvanced.cs` | public ExampleWallAdvanced : ModItem | SetStaticDefaults, SetDefaults, AddRecipes | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Placeable/ExampleWaterTorch.cs` | public ExampleWaterTorch : ModItem | SetStaticDefaults, SetDefaults, HoldItem, PostUpdate, AddRecipes | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方；在更新 Hook 中驱动状态/AI |

### `Content/Items/Placeable/Banners`（2 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Content/Items/Placeable/Banners/ExampleCustomAISlimeNPCBanner.cs` | public ExampleCustomAISlimeNPCBanner : ModItem | SetDefaults | 物品；设置实体/物品实例默认值 |
| `Content/Items/Placeable/Banners/ExampleWormHeadBanner.cs` | public ExampleWormHeadBanner : ModItem | SetDefaults | 物品；设置实体/物品实例默认值 |

### `Content/Items/Placeable/Furniture`（15 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Content/Items/Placeable/Furniture/ExampleBed.cs` | public ExampleBed : ModItem | SetDefaults, AddRecipes | 物品；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Placeable/Furniture/ExampleChair.cs` | public ExampleChair : ModItem | SetDefaults, AddRecipes | 物品；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Placeable/Furniture/ExampleChandelier.cs` | public ExampleChandelier : ModItem | SetDefaults, AddRecipes | 物品；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Placeable/Furniture/ExampleChest.cs` | public ExampleChest : ModItem; public ExampleChestKey : ModItem | SetDefaults, AddRecipes, SetStaticDefaults | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Placeable/Furniture/ExampleClock.cs` | public ExampleClock : ModItem | SetDefaults, AddRecipes | 物品；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Placeable/Furniture/ExampleDoor.cs` | public ExampleDoor : ModItem | SetDefaults, AddRecipes | 物品；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Placeable/Furniture/ExampleDresser.cs` | public ExampleDresser : ModItem | SetStaticDefaults, SetDefaults, AddRecipes | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Placeable/Furniture/ExamplePlatform.cs` | public ExamplePlatform : ModItem | SetStaticDefaults, SetDefaults, AddRecipes | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Placeable/Furniture/ExampleSink.cs` | public ExampleSink : ModItem | SetDefaults, AddRecipes | 物品；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Placeable/Furniture/ExampleTable.cs` | public ExampleTable : ModItem | SetDefaults, AddRecipes | 物品；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Placeable/Furniture/ExampleToilet.cs` | public ExampleToilet : ModItem | SetDefaults, AddRecipes | 物品；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Placeable/Furniture/ExampleWideBanner.cs` | public ExampleWideBanner : ModItem | SetDefaults, AddRecipes | 物品；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Placeable/Furniture/ExampleWorkbench.cs` | public ExampleWorkbench : ModItem | SetDefaults, ModifyResearchSorting, AddRecipes | 物品；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Placeable/Furniture/MinionBossRelic.cs` | public MinionBossRelic : ModItem | SetDefaults | 物品；设置实体/物品实例默认值 |
| `Content/Items/Placeable/Furniture/MinionBossTrophy.cs` | public MinionBossTrophy : ModItem | SetDefaults | 物品；设置实体/物品实例默认值 |

### `Content/Items/Tools`（9 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Content/Items/Tools/ExampleBugNet.cs` | public ExampleBugNet : ModItem; public ExampleCatchItemModification : GlobalItem | SetStaticDefaults, SetDefaults, CanCatchNPC, AddRecipes, OnSpawn | 物品、全局物品修改；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方；控制生成或初始化 |
| `Content/Items/Tools/ExampleDrill.cs` | public ExampleDrill : ModItem | SetStaticDefaults, SetDefaults, AddRecipes | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Tools/ExampleFishingRod.cs` | public ExampleFishingRod : ModItem | SetStaticDefaults, SetDefaults, HoldItem, Shoot, ModifyFishingLine, AddRecipes | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方；控制射击、弹药或生成弹幕 |
| `Content/Items/Tools/ExampleHamaxe.cs` | public ExampleHamaxe : ModItem | SetDefaults, MeleeEffects, AddRecipes | 物品；设置实体/物品实例默认值；注册或调整配方；处理帧、特效或自定义绘制 |
| `Content/Items/Tools/ExampleHook.cs` | internal ExampleHookItem : ModItem; internal ExampleHookProjectile : ModProjectile | SetDefaults, AddRecipes, Load, SetStaticDefaults, CanUseGrapple, GrappleRange, NumGrappleHooks, GrappleRetreatSpeed, GrapplePullSpeed, GrappleTargetPoint, GrappleCanLatchOnTo, PreDrawExtras | 弹幕、物品；加载、注册或清理；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方；处理帧、特效或自定义绘制 |
| `Content/Items/Tools/ExampleInteractableProjectileItem.cs` | public ExampleInteractableProjectileItem : ModItem | SetDefaults, AddRecipes | 物品；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Tools/ExampleMagicMirror.cs` | internal ExampleMagicMirror : ExampleItem | SetDefaults, UseStyle, ModifyTooltips, AddRecipes | 内容辅助类型；设置实体/物品实例默认值；注册或调整配方；控制物品使用与消耗 |
| `Content/Items/Tools/ExamplePickaxe.cs` | public ExamplePickaxe : ModItem | SetDefaults, MeleeEffects, UseAnimation, AddRecipes | 物品；设置实体/物品实例默认值；注册或调整配方；处理帧、特效或自定义绘制 |
| `Content/Items/Tools/ExampleSandRod.cs` | public ExampleSandRod : ModItem | SetStaticDefaults, SetDefaults, CanUseItem, ModifyShootStats, AddRecipes | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方；控制物品使用与消耗；控制射击、弹药或生成弹幕 |

### `Content/Items/Weapons`（31 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Content/Items/Weapons/ExampleAdvancedFlail.cs` | public ExampleAdvancedFlail : ModItem | SetStaticDefaults, SetDefaults, AddRecipes | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Weapons/ExampleCloneWeapon.cs` | public ExampleCloneWeapon : ModItem | SetDefaults, AddRecipes | 物品；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Weapons/ExampleCustomAmmoGun.cs` | public ExampleCustomAmmoGun : ModItem | SetDefaults, AddRecipes | 物品；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Weapons/ExampleCustomDamageWeapon.cs` | public ExampleCustomDamageWeapon : ModItem | SetDefaults, AddRecipes | 物品；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Weapons/ExampleCustomResourceWeapon.cs` | public ExampleCustomResourceWeapon : ModItem | SetStaticDefaults, SetDefaults, ModifyTooltips, CanUseItem, UseItem, AddRecipes | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方；控制物品使用与消耗 |
| `Content/Items/Weapons/ExampleCustomSwingSword.cs` | public ExampleCustomSwingSword : ModItem | SetDefaults, Shoot, UpdateInventory, MeleePrefix, AddRecipes | 物品；设置实体/物品实例默认值；注册或调整配方；控制射击、弹药或生成弹幕 |
| `Content/Items/Weapons/ExampleCustomUseStyleWeapon.cs` | public ExampleCustomUseStyleWeapon : ModItem; public ExampleCustomUseStylePlayer : ModPlayer; public static ExampleCustomUseStyleItemSets; public ExampleCustomUseStyleGlobalItem : GlobalItem | SetDefaults, SetStaticDefaults, AddRecipes, SyncDirection, ReceiveDirection, Load, AppliesToEntity, UseStyle, UseItemHitbox, UseItemFrame | 物品、玩家扩展、全局物品修改；加载、注册或清理；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方；处理帧、特效或自定义绘制 |
| `Content/Items/Weapons/ExampleExplosive.cs` | public ExampleExplosive : ModItem | SetStaticDefaults, SetDefaults, AddRecipes | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Weapons/ExampleFlail.cs` | internal ExampleFlail : ModItem | SetStaticDefaults, SetDefaults, GetAlpha, AddRecipes | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Weapons/ExampleGun.cs` | public ExampleGun : ModItem | SetDefaults, AddRecipes, HoldoutOffset, ModifyShootStats | 物品；设置实体/物品实例默认值；注册或调整配方；控制射击、弹药或生成弹幕 |
| `Content/Items/Weapons/ExampleHeldProjectileWeapon.cs` | public ExampleHeldProjectileWeapon : ModItem | Load, SetDefaults, Shoot, CanConsumeAmmo, PostDrawInWorld | 物品；加载、注册或清理；设置实体/物品实例默认值；处理帧、特效或自定义绘制；控制射击、弹药或生成弹幕 |
| `Content/Items/Weapons/ExampleJavelin.cs` | public ExampleJavelin : ModItem | SetDefaults, AddRecipes | 物品；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Weapons/ExampleJoustingLance.cs` | public ExampleJoustingLance : ModItem | SetDefaults, MeleePrefix, AddRecipes | 物品；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Weapons/ExampleLastPrism.cs` | public ExampleLastPrism : ModItem | SetDefaults, AddRecipes, CanUseItem | 物品；设置实体/物品实例默认值；注册或调整配方；控制物品使用与消耗 |
| `Content/Items/Weapons/ExampleMagicWeapon.cs` | public ExampleMagicWeapon : ModItem | SetDefaults, AddRecipes, ModifyManaCost | 物品；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Weapons/ExampleMinigun.cs` | public ExampleMinigun : ModItem | SetDefaults, AddRecipes, CanConsumeAmmo, NeedsAmmo, ModifyShootStats, HoldoutOffset | 物品；设置实体/物品实例默认值；注册或调整配方；控制射击、弹药或生成弹幕 |
| `Content/Items/Weapons/ExampleModifiedProjectilesItem.cs` | public ExampleModifiedProjectilesItem : ModItem | SetDefaults, Shoot | 物品；设置实体/物品实例默认值；控制射击、弹药或生成弹幕 |
| `Content/Items/Weapons/ExampleMultiplePrefixCategoryWeapon.cs` | public ExampleMultiplePrefixCategoryWeapon : ModItem | SetDefaults, AddRecipes, MeleePrefix, MagicPrefix, RangedPrefix | 物品；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Weapons/ExampleRocketLauncher.cs` | public ExampleRocketLauncher : ModItem | SetStaticDefaults, SetDefaults, HoldoutOffset | 物品；登记类型级静态数据；设置实体/物品实例默认值 |
| `Content/Items/Weapons/ExampleShootingSword.cs` | public ExampleShootingSword : ModItem | SetDefaults, Shoot, AddRecipes | 物品；设置实体/物品实例默认值；注册或调整配方；控制射击、弹药或生成弹幕 |
| `Content/Items/Weapons/ExampleShortsword.cs` | public ExampleShortsword : ModItem | SetDefaults, MeleePrefix, ApplyPrefix, AddRecipes | 物品；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Weapons/ExampleShotgun.cs` | public ExampleShotgun : ModItem | SetDefaults, Shoot, AddRecipes, HoldoutOffset | 物品；设置实体/物品实例默认值；注册或调整配方；控制射击、弹药或生成弹幕 |
| `Content/Items/Weapons/ExampleSpear.cs` | public ExampleSpear : ModItem | SetStaticDefaults, SetDefaults, CanUseItem, UseItem, AddRecipes | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方；控制物品使用与消耗 |
| `Content/Items/Weapons/ExampleSpecificAmmoGun.cs` | public ExampleSpecificAmmoGun : ModItem | SetDefaults, AddRecipes, HoldoutOffset, UpdateInventory, CanChooseAmmo, CanConsumeAmmo, OnConsumeAmmo, ModifyShootStats | 物品；设置实体/物品实例默认值；注册或调整配方；控制射击、弹药或生成弹幕 |
| `Content/Items/Weapons/ExampleStaff.cs` | public ExampleStaff : ModItem | SetStaticDefaults, SetDefaults, AddRecipes | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Weapons/ExampleSwingingEnergySword.cs` | public ExampleSwingingEnergySword : ModItem | SetDefaults, Shoot, AddRecipes | 物品；设置实体/物品实例默认值；注册或调整配方；控制射击、弹药或生成弹幕 |
| `Content/Items/Weapons/ExampleSword.cs` | public ExampleSword : ModItem | SetDefaults, MeleeEffects, OnHitNPC, AddRecipes | 物品；设置实体/物品实例默认值；注册或调整配方；处理帧、特效或自定义绘制；处理伤害、命中或闪避 |
| `Content/Items/Weapons/ExampleWhip.cs` | public ExampleWhip : ModItem | SetStaticDefaults, SetDefaults, Shoot, AddRecipes, MeleePrefix | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方；控制射击、弹药或生成弹幕 |
| `Content/Items/Weapons/ExampleWhipAdvanced.cs` | public ExampleWhipAdvanced : ModItem; public WhipTagEffect_ExampleWhipAdvanced : WhipTagEffect | SetStaticDefaults, SetDefaults, Shoot, AddRecipes, MeleePrefix, ModifyTaggedHit, OnTaggedHit, OnProcHit, ModifyProcHit | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方；处理伤害、命中或闪避；控制射击、弹药或生成弹幕 |
| `Content/Items/Weapons/ExampleYoyo.cs` | public ExampleYoyo : ModItem | SetStaticDefaults, SetDefaults, AllowPrefix, AddRecipes | 物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Items/Weapons/HitModifiersShowcase.cs` | public HitModifiersShowcase : ModItem | SetStaticDefaults, SetDefaults, NetSend, NetReceive, AltFunctionUse, UseItem, MeleeEffects, ModifyHitNPC, OnHitNPC, ModifyHitPvp, OnHitPvp | 物品；登记类型级静态数据；设置实体/物品实例默认值；处理帧、特效或自定义绘制；序列化并同步联机状态；处理伤害、命中或闪避 |

### `Content/Mounts`（2 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Content/Mounts/ExampleMinecartMount.cs` | public ExampleMinecartMount : ModMount | SetStaticDefaults, UpdateEffects | 坐骑；登记类型级静态数据；处理帧、特效或自定义绘制 |
| `Content/Mounts/ExampleMount.cs` | public ExampleMount : ModMount; protected CarSpecificData | CarSpecificData, SetStaticDefaults, UpdateEffects, SetMount, Draw | 坐骑；登记类型级静态数据；处理帧、特效或自定义绘制 |

### `Content/NPCs`（11 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Content/NPCs/ExampleBoneMerchant.cs` | public ExampleBoneMerchant : ModNPC | Load, SetStaticDefaults, SetDefaults, CanChat, SetBestiary, HitEffect, TownNPCProfile, SetNPCNameList, SpawnChance, GetChat, RegisterChatButtons, AddShops, TownNPCAttackStrength, TownNPCAttackCooldown, TownNPCAttackProj, TownNPCAttackProjSpeed, TownNPCAttackShoot, DrawTownAttackGun | NPC；加载、注册或清理；登记类型级静态数据；设置实体/物品实例默认值；处理帧、特效或自定义绘制；控制生成或初始化 |
| `Content/NPCs/ExampleCritter.cs` | public ExampleCritterNPC : ModNPC; public ExampleCritterItem : ModItem | Load, SetStaticDefaults, SetDefaults, SetBestiary, SpawnChance, HitEffect, OnHitByItem, OnHitByProjectile, GetAlpha, PreAI, OnCaughtBy | 物品、NPC；加载、注册或清理；登记类型级静态数据；设置实体/物品实例默认值；在更新 Hook 中驱动状态/AI；控制生成或初始化 |
| `Content/NPCs/ExampleCustomAISlimeNPC.cs` | public ExampleCustomAISlimeNPC : ModNPC; private ActionState; private Frame | SetStaticDefaults, SetDefaults, SpawnChance, AI, FindFrame, CanFallThroughPlatforms, ModifyCollisionData | NPC；登记类型级静态数据；设置实体/物品实例默认值；在更新 Hook 中驱动状态/AI；处理帧、特效或自定义绘制；控制生成或初始化 |
| `Content/NPCs/ExampleDrawBehindNPC.cs` | public ExampleDrawBehindNPC : ModNPC | SetStaticDefaults, SetDefaults, FindFrame, AI, DrawBehind, PreHoverInteract, CanChat | NPC；登记类型级静态数据；设置实体/物品实例默认值；在更新 Hook 中驱动状态/AI；处理帧、特效或自定义绘制；处理商店、聊天或交互 |
| `Content/NPCs/ExampleGlobalNPC.cs` | public ExampleGlobalNPC : GlobalNPC | AppliesToEntity, OnHitByProjectile, OnHitByItem, ModifyActiveShop, SaveData, LoadData | 全局 NPC 修改；保存、读取或重置持久状态；处理商店、聊天或交互；处理伤害、命中或闪避 |
| `Content/NPCs/ExamplePerson.cs` | public ExamplePerson : ModNPC; public AwesomeifyButton : NPCInteraction; public UpgradeButton : NPCInteraction; public OpenShopOnlyAvailableDuringDay | Load, SetStaticDefaults, SetDefaults, SetBestiary, PreDraw, HitEffect, OnSpawn, CanTownNPCSpawn, CheckConditions, TownNPCProfile, SetNPCNameList, FindFrame, GetChat, RegisterChatButtons, GetText, Condition, Interact, OpenShopOnlyAvailableDuringDay, OnChatButtonClicked, AddShops, ModifyActiveShop, ModifyNPCLoot, CanGoToStatue, OnGoToStatue, StatueTeleport, ModifyDeathMessage, TownNPCAttackStrength, TownNPCAttackCooldown, TownNPCAttackProj, TownNPCAttackProjSpeed, LoadData, SaveData, PickEmote | NPC；加载、注册或清理；登记类型级静态数据；设置实体/物品实例默认值；处理帧、特效或自定义绘制；保存、读取或重置持久状态 |
| `Content/NPCs/ExampleTravelingMerchant.cs` | internal ExampleTravelingMerchant : ModNPC; public ExampleTravelingMerchantShop : AbstractNPCShop; public Pool | PreAI, AddShops, UpdateTravelingMerchant, GetRandomSpawnTime, Load, SetStaticDefaults, SetDefaults, OnSpawn, SetBestiary, HitEffect, UsesPartyHat, CanTownNPCSpawn, TownNPCProfile, SetNPCNameList, GetChat, RegisterChatButtons, AI, ModifyNPCLoot, TownNPCAttackStrength, TownNPCAttackCooldown, TownNPCAttackSwing, DrawTownAttackSwing, Pool, Add, PickItems, ExampleTravelingMerchantShop, AddPool, GenerateNewInventoryList, FillShop | NPC；加载、注册或清理；登记类型级静态数据；设置实体/物品实例默认值；在更新 Hook 中驱动状态/AI；处理帧、特效或自定义绘制 |
| `Content/NPCs/ExampleWorm.cs` | internal ExampleWormHead : WormHead; internal ExampleWormBody : WormBody; internal ExampleWormTail : WormTail | SetStaticDefaults, SetDefaults, SetBestiary, Init, CommonWormInit, SendExtraAI, ReceiveExtraAI, AI | 内容辅助类型；登记类型级静态数据；设置实体/物品实例默认值；在更新 Hook 中驱动状态/AI；序列化并同步联机状态 |
| `Content/NPCs/ExampleZombieThief.cs` | public ExampleZombieThief : ModNPC | SetStaticDefaults, SetDefaults, SetBestiary, AI, SendExtraAI, ReceiveExtraAI, OnKill, SpawnChance, NeedSaving, SaveData, LoadData | NPC；登记类型级静态数据；设置实体/物品实例默认值；在更新 Hook 中驱动状态/AI；保存、读取或重置持久状态；序列化并同步联机状态 |
| `Content/NPCs/PartyZombie.cs` | public PartyZombie : ModNPC | SetStaticDefaults, SetDefaults, ModifyNPCLoot, SpawnChance, AI, SetBestiary, HitEffect, OnHitPlayer, ModifyIncomingHit | NPC；登记类型级静态数据；设置实体/物品实例默认值；在更新 Hook 中驱动状态/AI；控制生成或初始化；配置掉落规则 |
| `Content/NPCs/Worm.cs` | public WormSegmentType; public abstract Worm : ModNPC; public abstract WormHead : Worm; public abstract WormBody : Worm; public abstract WormTail : Worm | DrawHealthBar, PreAI, HeadAI, BodyTailAI, Init, SpawnBodySegments, SpawnSegment, CommonAI_BodyTail | NPC；在更新 Hook 中驱动状态/AI；处理帧、特效或自定义绘制；控制生成或初始化 |

### `Content/NPCs/MinionBoss`（2 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Content/NPCs/MinionBoss/MinionBossBody.cs` | public MinionBossBody : ModNPC | MinionType, MinionCount, Load, BossHeadSlot, SetStaticDefaults, SetDefaults, SetBestiary, ModifyNPCLoot, OnKill, BossLoot, CanHitPlayer, FindFrame, HitEffect, AI | NPC；加载、注册或清理；登记类型级静态数据；设置实体/物品实例默认值；在更新 Hook 中驱动状态/AI；处理帧、特效或自定义绘制 |
| `Content/NPCs/MinionBoss/MinionBossMinion.cs` | public MinionBossMinion : ModNPC | BodyType, SetStaticDefaults, SetDefaults, SetBestiary, GetAlpha, CanHitPlayer, OnKill, HitEffect, AI | NPC；登记类型级静态数据；设置实体/物品实例默认值；在更新 Hook 中驱动状态/AI；处理伤害、命中或闪避 |

### `Content/NPCs/TownPets`（1 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Content/NPCs/TownPets/ExampleTownPet.cs` | public ExampleTownPet : ModNPC; public ExampleTownPetProfile : ITownNPCProfile | Load, SetStaticDefaults, SetDefaults, SetBestiary, CanTownNPCSpawn, TownNPCProfile, SetNPCNameList, GetChat, PreAI, ChatBubblePosition, EmoteBubblePosition, PartyHatPosition, RollVariation, GetNameForVariant, GetTextureNPCShouldUse, GetHeadTextureIndex | NPC；加载、注册或清理；登记类型级静态数据；设置实体/物品实例默认值；在更新 Hook 中驱动状态/AI；控制生成或初始化 |

### `Content/Pets/ExampleLightPet`（3 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Content/Pets/ExampleLightPet/ExampleLightPetBuff.cs` | public ExampleLightPetBuff : ModBuff | SetStaticDefaults, Update | Buff/Debuff；登记类型级静态数据；在更新 Hook 中驱动状态/AI |
| `Content/Pets/ExampleLightPet/ExampleLightPetItem.cs` | public ExampleLightPetItem : ModItem | SetDefaults, AddRecipes, UseStyle | 物品；设置实体/物品实例默认值；注册或调整配方；控制物品使用与消耗 |
| `Content/Pets/ExampleLightPet/ExampleLightPetProjectile.cs` | public ExampleLightPetProjectile : ModProjectile | SetStaticDefaults, SetDefaults, AI | 弹幕；登记类型级静态数据；设置实体/物品实例默认值；在更新 Hook 中驱动状态/AI |

### `Content/Pets/ExamplePet`（3 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Content/Pets/ExamplePet/ExamplePetBuff.cs` | public ExamplePetBuff : ModBuff | SetStaticDefaults, Update | Buff/Debuff；登记类型级静态数据；在更新 Hook 中驱动状态/AI |
| `Content/Pets/ExamplePet/ExamplePetItem.cs` | public ExamplePetItem : ModItem | SetDefaults, UseItem, AddRecipes | 物品；设置实体/物品实例默认值；注册或调整配方；控制物品使用与消耗 |
| `Content/Pets/ExamplePet/ExamplePetProjectile.cs` | public ExamplePetProjectile : ModProjectile | SetStaticDefaults, SetDefaults, PreAI, AI | 弹幕；登记类型级静态数据；设置实体/物品实例默认值；在更新 Hook 中驱动状态/AI |

### `Content/Pets/MinionBossPet`（3 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Content/Pets/MinionBossPet/MinionBossPetBuff.cs` | public MinionBossPetBuff : ModBuff | SetStaticDefaults, Update | Buff/Debuff；登记类型级静态数据；在更新 Hook 中驱动状态/AI |
| `Content/Pets/MinionBossPet/MinionBossPetItem.cs` | public MinionBossPetItem : ModItem | SetDefaults, Shoot | 物品；设置实体/物品实例默认值；控制射击、弹药或生成弹幕 |
| `Content/Pets/MinionBossPet/MinionBossPetProjectile.cs` | public MinionBossPetProjectile : ModProjectile | Load, SetStaticDefaults, CharacterPreviewCustomization, SetDefaults, GetAlpha, PostDraw, AI | 弹幕；加载、注册或清理；登记类型级静态数据；设置实体/物品实例默认值；在更新 Hook 中驱动状态/AI；处理帧、特效或自定义绘制 |

### `Content/Prefixes`（2 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Content/Prefixes/ExampleDerivedPrefix.cs` | public ExampleDerivedPrefix : ExamplePrefix | — | 内容辅助类型；通过表中成员提供专用数据或辅助算法 |
| `Content/Prefixes/ExamplePrefix.cs` | public ExamplePrefix : ModPrefix | RollChance, CanRoll, SetStats, ModifyValue, Apply, GetTooltipLines, SetStaticDefaults | 前缀；登记类型级静态数据 |

### `Content/Projectiles`（32 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Content/Projectiles/ActiveSoundShowcaseProjectile.cs` | public ActiveSoundShowcaseProjectile : ModProjectile; internal ActiveSoundShowcaseStyle | SetStaticDefaults, SetDefaults, OnSpawn, AI, OnKill, OnTileCollide | 弹幕；登记类型级静态数据；设置实体/物品实例默认值；在更新 Hook 中驱动状态/AI；控制生成或初始化 |
| `Content/Projectiles/ExampleAdvancedAnimatedProjectile.cs` | public ExampleAdvancedAnimatedProjectile : ModProjectile; internal ExampleAdvancedAnimatedProjectileItem : ModItem | SetStaticDefaults, SetDefaults, GetAlpha, AI, FadeInAndOut, PreDraw, AddRecipes | 弹幕、物品；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方；在更新 Hook 中驱动状态/AI；处理帧、特效或自定义绘制 |
| `Content/Projectiles/ExampleAdvancedFlailProjectile.cs` | public ExampleAdvancedFlailProjectile : ModProjectile; private AIState | Load, SetStaticDefaults, SetDefaults, AI, OnTileCollide, CanDamage, Colliding, ModifyHitNPC, PreDraw | 弹幕；加载、注册或清理；登记类型级静态数据；设置实体/物品实例默认值；在更新 Hook 中驱动状态/AI；处理帧、特效或自定义绘制 |
| `Content/Projectiles/ExampleArrowProjectile.cs` | public ExampleArrowProjectile : ModProjectile | SetStaticDefaults, SetDefaults, AI, OnKill | 弹幕；登记类型级静态数据；设置实体/物品实例默认值；在更新 Hook 中驱动状态/AI |
| `Content/Projectiles/ExampleBobber.cs` | public ExampleBobber : ModProjectile | SetDefaults, OnSpawn, AI, SendExtraAI, ReceiveExtraAI | 弹幕；设置实体/物品实例默认值；在更新 Hook 中驱动状态/AI；序列化并同步联机状态；控制生成或初始化 |
| `Content/Projectiles/ExampleBullet.cs` | public ExampleBullet : ModProjectile | SetStaticDefaults, SetDefaults, OnTileCollide, PreDraw, OnKill | 弹幕；登记类型级静态数据；设置实体/物品实例默认值；处理帧、特效或自定义绘制 |
| `Content/Projectiles/ExampleCloneProjectile.cs` | public ExampleCloneProjectile : ModProjectile | SetDefaults, OnKill, OnTileCollide | 弹幕；设置实体/物品实例默认值 |
| `Content/Projectiles/ExampleCustomSwingProjectile.cs` | public ExampleCustomSwingProjectile : ModProjectile; private AttackType; private AttackStage | SetStaticDefaults, SetDefaults, OnSpawn, SendExtraAI, ReceiveExtraAI, AI, PreDraw, Colliding, CutTiles, CanDamage, ModifyHitNPC, SetSwordPosition | 弹幕；登记类型级静态数据；设置实体/物品实例默认值；在更新 Hook 中驱动状态/AI；处理帧、特效或自定义绘制；序列化并同步联机状态 |
| `Content/Projectiles/ExampleDrillProjectile.cs` | public ExampleDrillProjectile : ModProjectile | SetDefaults, AI | 弹幕；设置实体/物品实例默认值；在更新 Hook 中驱动状态/AI |
| `Content/Projectiles/ExampleExplosive.cs` | public ExampleExplosive : ModProjectile | SetStaticDefaults, SetDefaults, ModifyHitNPC, OnTileCollide, AI, PrepareBombToBlow, OnKill | 弹幕；登记类型级静态数据；设置实体/物品实例默认值；在更新 Hook 中驱动状态/AI；处理伤害、命中或闪避 |
| `Content/Projectiles/ExampleFlailProjectile.cs` | internal ExampleFlailProjectile : ModProjectile | SetDefaults, GetAlpha, PreDrawExtras, PreDraw, OnHitNPC, OnHitPlayer, AI | 弹幕；设置实体/物品实例默认值；在更新 Hook 中驱动状态/AI；处理帧、特效或自定义绘制；处理伤害、命中或闪避 |
| `Content/Projectiles/ExampleGolfBallProjectile.cs` | public ExampleGolfBallProjectile : ModProjectile | SetStaticDefaults, SetDefaults | 弹幕；登记类型级静态数据；设置实体/物品实例默认值 |
| `Content/Projectiles/ExampleGravityDebuffBullet.cs` | public ExampleGravityDebuffBullet : ModProjectile | SetStaticDefaults, SetDefaults, PreDraw, OnKill, OnHitNPC | 弹幕；登记类型级静态数据；设置实体/物品实例默认值；处理帧、特效或自定义绘制；处理伤害、命中或闪避 |
| `Content/Projectiles/ExampleHeldProjectileWeaponProjectile.cs` | public ExampleHeldProjectileWeaponProjectile : ModProjectile | SetStaticDefaults, SetDefaults, CanDamage, AI | 弹幕；登记类型级静态数据；设置实体/物品实例默认值；在更新 Hook 中驱动状态/AI；处理伤害、命中或闪避 |
| `Content/Projectiles/ExampleHomingProjectile.cs` | public ExampleHomingProjectile : ModProjectile | SetStaticDefaults, SetDefaults, AI, FindClosestNPC, IsValidTarget | 弹幕；登记类型级静态数据；设置实体/物品实例默认值；在更新 Hook 中驱动状态/AI |
| `Content/Projectiles/ExampleInstancedProjectile.cs` | public ExampleInstancedProjectile : ModProjectile | SetDefaults, PreDraw, OnSpawn | 弹幕；设置实体/物品实例默认值；处理帧、特效或自定义绘制；控制生成或初始化 |
| `Content/Projectiles/ExampleInteractableProjectile.cs` | public ExampleInteractableProjectile : ModProjectile | Load, SetStaticDefaults, SetDefaults, PostDraw, AI | 弹幕；加载、注册或清理；登记类型级静态数据；设置实体/物品实例默认值；在更新 Hook 中驱动状态/AI；处理帧、特效或自定义绘制 |
| `Content/Projectiles/ExampleJavelinProjectile.cs` | public ExampleJavelinProjectile : ModProjectile | SetDefaults, AI, OnKill, OnHitNPC, TileCollideStyle, Colliding | 弹幕；设置实体/物品实例默认值；在更新 Hook 中驱动状态/AI；处理伤害、命中或闪避 |
| `Content/Projectiles/ExampleJoustingLanceProjectile.cs` | public ExampleJoustingLanceProjectile : ModProjectile | SetStaticDefaults, SetDefaults, AI, ModifyHitNPC, Colliding, PreDraw | 弹幕；登记类型级静态数据；设置实体/物品实例默认值；在更新 Hook 中驱动状态/AI；处理帧、特效或自定义绘制；处理伤害、命中或闪避 |
| `Content/Projectiles/ExampleLastPrismBeam.cs` | public ExampleLastPrismBeam : ModProjectile | SetDefaults, SendExtraAI, ReceiveExtraAI, AI, Colliding, PreDraw, CutTiles | 弹幕；设置实体/物品实例默认值；在更新 Hook 中驱动状态/AI；处理帧、特效或自定义绘制；序列化并同步联机状态 |
| `Content/Projectiles/ExampleLastPrismHoldout.cs` | public ExampleLastPrismHoldout : ModProjectile | SetStaticDefaults, SetDefaults, CanDamage, AI, PreDraw | 弹幕；登记类型级静态数据；设置实体/物品实例默认值；在更新 Hook 中驱动状态/AI；处理帧、特效或自定义绘制；处理伤害、命中或闪避 |
| `Content/Projectiles/ExamplePaperAirplaneProjectile.cs` | public ExamplePaperAirplaneProjectile : ModProjectile | SetDefaults, AI, PreDraw, OnKill, ModifyHitNPC | 弹幕；设置实体/物品实例默认值；在更新 Hook 中驱动状态/AI；处理帧、特效或自定义绘制；处理伤害、命中或闪避 |
| `Content/Projectiles/ExamplePiercingProjectile.cs` | public ExamplePiercingProjectile : ModProjectile; internal ExamplePiercingProjectileItem : ModItem | SetDefaults, OnHitNPC, AddRecipes | 弹幕、物品；设置实体/物品实例默认值；注册或调整配方；处理伤害、命中或闪避 |
| `Content/Projectiles/ExampleSandBallProjectile.cs` | public abstract ExampleSandBallProjectile : ModProjectile; public ExampleSandBallFallingProjectile : ExampleSandBallProjectile; public ExampleSandBallGunProjectile : ExampleSandBallProjectile | SetStaticDefaults, SetDefaults | 弹幕；登记类型级静态数据；设置实体/物品实例默认值 |
| `Content/Projectiles/ExampleShortswordProjectile.cs` | public ExampleShortswordProjectile : ModProjectile | SetDefaults, AI, ShouldUpdatePosition, CutTiles, Colliding | 弹幕；设置实体/物品实例默认值；在更新 Hook 中驱动状态/AI |
| `Content/Projectiles/ExampleSpearProjectile.cs` | public ExampleSpearProjectile : ModProjectile | SetDefaults, PreAI | 弹幕；设置实体/物品实例默认值；在更新 Hook 中驱动状态/AI |
| `Content/Projectiles/ExampleSwingingEnergySwordProjectile.cs` | public ExampleSwingingEnergySwordProjectile : ModProjectile | SetStaticDefaults, SetDefaults, AI, Colliding, CutTiles, OnHitNPC, OnHitPlayer, PreDraw | 弹幕；登记类型级静态数据；设置实体/物品实例默认值；在更新 Hook 中驱动状态/AI；处理帧、特效或自定义绘制；处理伤害、命中或闪避 |
| `Content/Projectiles/ExampleWhipProjectile.cs` | public ExampleWhipProjectile : ModProjectile | SetStaticDefaults, SetDefaults, PreAI, OnHitNPC, PreDraw | 弹幕；登记类型级静态数据；设置实体/物品实例默认值；在更新 Hook 中驱动状态/AI；处理帧、特效或自定义绘制；处理伤害、命中或闪避 |
| `Content/Projectiles/ExampleWhipProjectileAdvanced.cs` | public ExampleWhipProjectileAdvanced : ModProjectile | SetStaticDefaults, SetDefaults, AI, OnHitNPC, PreDraw | 弹幕；登记类型级静态数据；设置实体/物品实例默认值；在更新 Hook 中驱动状态/AI；处理帧、特效或自定义绘制；处理伤害、命中或闪避 |
| `Content/Projectiles/ExampleYoyoProjectile.cs` | public ExampleYoyoProjectile : ModProjectile | SetStaticDefaults, SetDefaults, PostAI | 弹幕；登记类型级静态数据；设置实体/物品实例默认值；在更新 Hook 中驱动状态/AI |
| `Content/Projectiles/MinionBossEye.cs` | public MinionBossEye : ModProjectile | SetStaticDefaults, SetDefaults, GetAlpha, AI, OnHitPlayer | 弹幕；登记类型级静态数据；设置实体/物品实例默认值；在更新 Hook 中驱动状态/AI；处理伤害、命中或闪避 |
| `Content/Projectiles/SparklingBall.cs` | public SparklingBall : ModProjectile | SetDefaults, AI, OnTileCollide, OnKill, OnHitNPC | 弹幕；设置实体/物品实例默认值；在更新 Hook 中驱动状态/AI；处理伤害、命中或闪避 |

### `Content/Projectiles/Minions`（4 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Content/Projectiles/Minions/ExampleSentry.cs` | public ExampleSentry : ModProjectile | SetStaticDefaults, SetDefaults, TileCollideStyle, OnTileCollide, GetAlpha, AI, OnKill | 弹幕；登记类型级静态数据；设置实体/物品实例默认值；在更新 Hook 中驱动状态/AI |
| `Content/Projectiles/Minions/ExampleSentryItem.cs` | public ExampleSentryItem : ModItem | SetStaticDefaults, SetDefaults, Shoot | 物品；登记类型级静态数据；设置实体/物品实例默认值；控制射击、弹药或生成弹幕 |
| `Content/Projectiles/Minions/ExampleSentryShot.cs` | public ExampleSentryShot : ModProjectile | SetStaticDefaults, SetDefaults, AI, OnKill | 弹幕；登记类型级静态数据；设置实体/物品实例默认值；在更新 Hook 中驱动状态/AI |
| `Content/Projectiles/Minions/ExampleSimpleMinion.cs` | public ExampleSimpleMinionBuff : ModBuff; public ExampleSimpleMinionItem : ModItem; public ExampleSimpleMinion : ModProjectile | SetStaticDefaults, Update, SetDefaults, ModifyShootStats, Shoot, AddRecipes, CanCutTiles, MinionContactDamage, AI | 弹幕、物品、Buff/Debuff；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方；在更新 Hook 中驱动状态/AI；处理伤害、命中或闪避 |

### `Content/Projectiles/Rockets`（4 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Content/Projectiles/Rockets/ExampleGrenadeProjectile.cs` | public ExampleGrenadeProjectile : ModProjectile | SetStaticDefaults, SetDefaults, AI, OnTileCollide, PrepareBombToBlow, OnKill | 弹幕；登记类型级静态数据；设置实体/物品实例默认值；在更新 Hook 中驱动状态/AI |
| `Content/Projectiles/Rockets/ExampleProximityMineProjectile.cs` | public ExampleProximityMineProjectile : ModProjectile | SetStaticDefaults, SetDefaults, AI, OnTileCollide, PrepareBombToBlow, OnKill | 弹幕；登记类型级静态数据；设置实体/物品实例默认值；在更新 Hook 中驱动状态/AI |
| `Content/Projectiles/Rockets/ExampleRocketProjectile.cs` | public ExampleRocketProjectile : ModProjectile | SetStaticDefaults, SetDefaults, AI, OnTileCollide, PrepareBombToBlow, OnKill | 弹幕；登记类型级静态数据；设置实体/物品实例默认值；在更新 Hook 中驱动状态/AI |
| `Content/Projectiles/Rockets/ExampleSnowmanRocketProjectile.cs` | public ExampleSnowmanRocketProjectile : ModProjectile | SetStaticDefaults, SetDefaults, AI, OnTileCollide, PrepareBombToBlow, OnKill | 弹幕；登记类型级静态数据；设置实体/物品实例默认值；在更新 Hook 中驱动状态/AI |

### `Content/Rarities`（2 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Content/Rarities/ExampleHigherTierModRarity.cs` | public ExampleHigherTierModRarity : ModRarity | GetPrefixedRarity | 稀有度；通过表中成员提供专用数据或辅助算法 |
| `Content/Rarities/ExampleModRarity.cs` | public ExampleModRarity : ModRarity | GetPrefixedRarity | 稀有度；通过表中成员提供专用数据或辅助算法 |

### `Content/TileEntities`（3 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Content/TileEntities/AdvancedPylonTileEntity.cs` | public AdvancedPylonTileEntity : TEModdedPylon | NetSend, NetReceive, Update | 内容辅助类型；在更新 Hook 中驱动状态/AI；序列化并同步联机状态 |
| `Content/TileEntities/BasicTileEntity.cs` | public BasicTileEntity : ModTileEntity; public BasicTileEntityTile : ModTile; public BasicTileEntityItem : ModItem | SaveData, LoadData, NetSend, NetReceive, Update, IsTileValidForEntity, SetStaticDefaults, KillMultiTile, SetDrawPositions, MapHoverText, MouseOver, RightClick, KillTile, SetDefaults, AddRecipes | 方块实体、物品、方块；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方；在更新 Hook 中驱动状态/AI；处理帧、特效或自定义绘制 |
| `Content/TileEntities/SimplePylonTileEntity.cs` | public sealed SimplePylonTileEntity : TEModdedPylon | — | 内容辅助类型；通过表中成员提供专用数据或辅助算法 |

### `Content/Tiles`（32 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Content/Tiles/Example1x1Rubble.cs` | public abstract Example1x1RubbleBase : ModTile; public Example1x1RubbleFake : Example1x1RubbleBase; public Example1x1RubbleNatural : Example1x1RubbleBase | SetStaticDefaults, DropCritterChance | 方块；登记类型级静态数据；配置掉落规则 |
| `Content/Tiles/Example2x1Rubble.cs` | public abstract Example2x1RubbleBase : ModTile; public Example2x1RubbleFake : Example2x1RubbleBase; public Example2x1RubbleNatural : Example2x1RubbleBase | SetStaticDefaults, DropCritterChance | 方块；登记类型级静态数据；配置掉落规则 |
| `Content/Tiles/Example3x2Rubble.cs` | public abstract Example3x2RubbleBase : ModTile; public Example3x2RubbleFake : Example3x2RubbleBase; public Example3x2RubbleNatural : Example3x2RubbleBase | SetStaticDefaults, DropCritterChance | 方块；登记类型级静态数据；配置掉落规则 |
| `Content/Tiles/ExampleAnimatedGlowmaskTile.cs` | public ExampleAnimatedGlowmaskTile : ModTile; internal ExampleAnimatedGlowmaskTileItem : ModItem | SetStaticDefaults, AnimateTile, PreDraw, SetDefaults, AddRecipes | 物品、方块；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方；处理帧、特效或自定义绘制 |
| `Content/Tiles/ExampleAnimatedTile.cs` | internal ExampleAnimatedTile : ModTile; internal ExampleAnimatedTileItem : ModItem | Load, SetStaticDefaults, ModifyLight, SetSpriteEffects, AnimateIndividualTile, KillSound, AnimateTile, PreDraw, AdjustMultiTileVineParameters, GetTileFlameData, SetDefaults, AddRecipes | 物品、方块；加载、注册或清理；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方；处理帧、特效或自定义绘制 |
| `Content/Tiles/ExampleBar.cs` | public ExampleBar : ModTile | SetStaticDefaults, TileFrame | 方块；登记类型级静态数据；处理帧、特效或自定义绘制；处理方块放置、导线或玩家交互 |
| `Content/Tiles/ExampleBlock.cs` | public ExampleBlock : ModTile | SetStaticDefaults, NumDust, ChangeWaterfallStyle | 方块；登记类型级静态数据；处理帧、特效或自定义绘制 |
| `Content/Tiles/ExampleCampfire.cs` | public ExampleCampfire : ModTile | SetStaticDefaults, NearbyEffects, MouseOver, HasSmartInteract, RightClick, HitWire, ToggleTile, AnimateTile, AnimateIndividualTile, EmitParticles, ModifyLight, PostDraw | 方块；登记类型级静态数据；处理帧、特效或自定义绘制；处理商店、聊天或交互；处理伤害、命中或闪避；处理方块放置、导线或玩家交互 |
| `Content/Tiles/ExampleCritterCage.cs` | public ExampleCritterCage : ModTile; public ExampleCritterCageItem : ModItem | SetStaticDefaults, SetDrawPositions, AnimateIndividualTile, AnimateTile, SetDefaults, AddRecipes | 物品、方块；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方；处理帧、特效或自定义绘制 |
| `Content/Tiles/ExampleCustomFramingTile.cs` | public ExampleCustomFramingTile : ModTile; internal ExampleCustomFramingTileItem : ModItem | SetStaticDefaults, ModifyFrameMerge, PostTileFrame, SetDefaults, AddRecipes | 物品、方块；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方；处理帧、特效或自定义绘制 |
| `Content/Tiles/ExampleCutTile.cs` | public ExampleCutTile : ModTile | SetStaticDefaults, IsTileDangerous, CreateDust, KillMultiTile | 方块；登记类型级静态数据；处理帧、特效或自定义绘制；处理方块放置、导线或玩家交互 |
| `Content/Tiles/ExampleExposedGem.cs` | public ExampleExposedGem : ModTile | SetStaticDefaults, CanPlace, TileFrame, PlaceInWorld, SetDrawPositions, EmitParticles, CreateDust | 方块；登记类型级静态数据；处理帧、特效或自定义绘制；处理方块放置、导线或玩家交互 |
| `Content/Tiles/ExampleFishingCrate.cs` | internal ExampleFishingCrate : ModTile | SetStaticDefaults, CreateDust | 方块；登记类型级静态数据；处理帧、特效或自定义绘制 |
| `Content/Tiles/ExampleGemsparkBlock.cs` | public ExampleGemsparkBlock : ModTile, ICustomAutoload | Autoload, ExampleGemsparkBlock, SetStaticDefaults, TileFrame, HitWire, ChangeWaterfallStyle | 方块、自定义自动加载；加载、注册或清理；登记类型级静态数据；处理帧、特效或自定义绘制；处理伤害、命中或闪避；处理方块放置、导线或玩家交互 |
| `Content/Tiles/ExampleHerb.cs` | public PlantStage : byte; public ExampleHerb : ModTile | SetStaticDefaults, CanPlace, SetSpriteEffects, SetDrawPositions, CanDrop, GetItemDrops, IsTileSpelunkable, RandomUpdate | 方块；登记类型级静态数据；处理帧、特效或自定义绘制；配置掉落规则 |
| `Content/Tiles/ExampleLamp.cs` | internal ExampleLamp : ModTile | SetStaticDefaults, HitWire, SetSpriteEffects, ModifyLight, EmitParticles, PostDraw | 方块；登记类型级静态数据；处理帧、特效或自定义绘制；处理伤害、命中或闪避；处理方块放置、导线或玩家交互 |
| `Content/Tiles/ExampleLivingFireTile.cs` | public ExampleLivingFireTile : ModTile | SetStaticDefaults, ModifyLight, SetDrawPositions, AnimateTile | 方块；登记类型级静态数据；处理帧、特效或自定义绘制 |
| `Content/Tiles/ExampleMusicBoxTile.cs` | public ExampleMusicBoxTile : ModTile | SetStaticDefaults, MouseOver, HasSmartInteract, EmitParticles | 方块；登记类型级静态数据；处理商店、聊天或交互；处理方块放置、导线或玩家交互 |
| `Content/Tiles/ExampleOre.cs` | public ExampleOre : ModTile; public ExampleOreSystem : ModSystem; public ExampleOrePass : GenPass | SetStaticDefaults, IsTileBiomeSightable, BlessWorldWithExampleOre, ModifyWorldGenTasks, ExampleOrePass, ApplyPass | 方块、系统/生命周期、世界生成步骤；登记类型级静态数据；插入或执行世界生成 |
| `Content/Tiles/ExamplePressurePlate.cs` | public ExamplePressurePlate : ModTile | SetStaticDefaults, IsTileDangerous, HitSwitch, KillTile, SetDrawPositions, AnimateIndividualTile | 方块；登记类型级静态数据；处理帧、特效或自定义绘制；处理伤害、命中或闪避；处理方块放置、导线或玩家交互 |
| `Content/Tiles/ExamplePylonTile.cs` | public ExamplePylonTile : ModPylon | Load, SetStaticDefaults, GetNPCShopEntry, MouseOver, KillMultiTile, ValidTeleportCheck_NPCCount, ValidTeleportCheck_BiomeRequirements, ModifyLight, SpecialDraw, DrawMapIcon | 晶塔；加载、注册或清理；登记类型级静态数据；处理帧、特效或自定义绘制；处理商店、聊天或交互；处理方块放置、导线或玩家交互 |
| `Content/Tiles/ExamplePylonTileAdvanced.cs` | public ExamplePylonTileAdvanced : ModPylon | Load, SetStaticDefaults, GetNPCShopEntry, HasSmartInteract, RightClick, MouseOver, KillMultiTile, ValidTeleportCheck_NPCCount, ValidTeleportCheck_DestinationPostCheck, ValidTeleportCheck_NearbyPostCheck, ModifyTeleportationPosition, ModifyLight, DrawEffects, SpecialDraw, DrawMapIcon | 晶塔；加载、注册或清理；登记类型级静态数据；处理帧、特效或自定义绘制；处理商店、聊天或交互；处理方块放置、导线或玩家交互 |
| `Content/Tiles/ExampleSand.cs` | public ExampleSand : ModTile | SetStaticDefaults, HasWalkDust, WalkDust, Convert | 方块；登记类型级静态数据；处理帧、特效或自定义绘制 |
| `Content/Tiles/ExampleSign.cs` | public ExampleSign : ModTile | SetStaticDefaults, PlaceInWorld, RightClick, KillMultiTile, HasSmartInteract | 方块；登记类型级静态数据；处理商店、聊天或交互；处理方块放置、导线或玩家交互 |
| `Content/Tiles/ExampleSink.cs` | public ExampleSink : ModTile | SetStaticDefaults, NumDust | 方块；登记类型级静态数据；处理帧、特效或自定义绘制 |
| `Content/Tiles/ExampleSlopeTile.cs` | public ExampleSlopeTile : ModTile | SetStaticDefaults, Slope, TileFrame, SwitchTiles, HitSwitch | 方块；登记类型级静态数据；处理帧、特效或自定义绘制；处理伤害、命中或闪避；处理方块放置、导线或玩家交互 |
| `Content/Tiles/ExampleStatue.cs` | public ExampleStatue : ModTile | SetStaticDefaults, HitWire | 方块；登记类型级静态数据；处理伤害、命中或闪避；处理方块放置、导线或玩家交互 |
| `Content/Tiles/ExampleTorch.cs` | public ExampleTorch : ModTile | SetStaticDefaults, MouseOver, GetTorchLuck, NumDust, ModifyLight, SetDrawPositions, PostDraw, EmitParticles | 方块；登记类型级静态数据；处理帧、特效或自定义绘制；处理方块放置、导线或玩家交互 |
| `Content/Tiles/ExampleTransparentShapedTile.cs` | public sealed ExampleTransparentShapedTile : ModTile; public sealed ExampleTransparentShapedTileItem : ModItem | SetStaticDefaults, ModifyLight, SetDefaults, AddRecipes | 物品、方块；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方；处理帧、特效或自定义绘制 |
| `Content/Tiles/ExampleTrap.cs` | public ExampleTrap : ModTile | SetStaticDefaults, GetMapOption, IsTileDangerous, GetItemDrops, CreateDust, PlaceInWorld, Slope, HitWire | 方块；登记类型级静态数据；处理帧、特效或自定义绘制；配置掉落规则；处理伤害、命中或闪避；处理方块放置、导线或玩家交互 |
| `Content/Tiles/ExampleVanillaConversionTiles.cs` | public HallowedFossilTile : ModTile; public CorruptFossilTile : ModTile; public CrimsonFossilTile : ModTile; internal HallowedFossilTileItem : ModItem; internal CorruptFossilTileItem : ModItem; internal CrimsonFossilTileItem : ModItem | SetStaticDefaults, RandomUpdate, ModifyFrameMerge, Convert, SetDefaults, AddRecipes | 物品、方块；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方；处理帧、特效或自定义绘制 |
| `Content/Tiles/TileObjectDataShowcase.cs` | public TileObjectDataShowcase : ModTile; public TileObjectDataShowcaseStyle0 : ModItem; public TileObjectDataShowcaseStyle1 : ModItem; public TileObjectDataShowcaseStyle2 : ModItem; public TileObjectDataShowcaseStyle3 : ModItem | SetStaticDefaults, RightClick, AnimateTile, AnimateIndividualTile, SetDefaults | 物品、方块；登记类型级静态数据；设置实体/物品实例默认值；处理方块放置、导线或玩家交互 |

### `Content/Tiles/Banners`（1 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Content/Tiles/Banners/EnemyBanner.cs` | public EnemyBanner : ModBannerTile; public StyleID; public EnemyBannerLoader : ILoadable; public AutoloadedBannerItem : ModItem | Load, Unload, AutoloadedBannerItem, SetDefaults | 物品、自定义加载器；加载、注册或清理；设置实体/物品实例默认值 |

### `Content/Tiles/Furniture`（15 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Content/Tiles/Furniture/ExampleBed.cs` | public ExampleBed : ModTile | SetStaticDefaults, HasSmartInteract, ModifySmartInteractCoords, ModifySleepingTargetInfo, NumDust, RightClick, MouseOver | 方块；登记类型级静态数据；处理帧、特效或自定义绘制；处理商店、聊天或交互；处理方块放置、导线或玩家交互 |
| `Content/Tiles/Furniture/ExampleChair.cs` | public ExampleChair : ModTile | SetStaticDefaults, NumDust, HasSmartInteract, ModifySittingTargetInfo, RightClick, MouseOver | 方块；登记类型级静态数据；处理帧、特效或自定义绘制；处理商店、聊天或交互；处理方块放置、导线或玩家交互 |
| `Content/Tiles/Furniture/ExampleChandelier.cs` | public ExampleChandelier : ModTile; public StyleID | Load, SetStaticDefaults, HitWire, ModifyLight, EmitParticles, PreDraw, AdjustMultiTileVineParameters, GetTileFlameData, AnimateIndividualTile | 方块；加载、注册或清理；登记类型级静态数据；处理帧、特效或自定义绘制；处理伤害、命中或闪避；处理方块放置、导线或玩家交互 |
| `Content/Tiles/Furniture/ExampleChest.cs` | public ExampleChest : ModTile | SetStaticDefaults, GetItemDrops, GetMapOption, DefaultContainerName, HasSmartInteract, IsLockedChest, UnlockChest, LockChest, MapChestName, NumDust, KillMultiTile, RightClick, MouseOver, MouseOverFar | 方块；登记类型级静态数据；处理帧、特效或自定义绘制；配置掉落规则；处理商店、聊天或交互；处理方块放置、导线或玩家交互 |
| `Content/Tiles/Furniture/ExampleClock.cs` | public ExampleClock : ModTile | SetStaticDefaults, RightClick, NumDust | 方块；登记类型级静态数据；处理帧、特效或自定义绘制；处理方块放置、导线或玩家交互 |
| `Content/Tiles/Furniture/ExampleDoorClosed.cs` | public ExampleDoorClosed : ModTile | SetStaticDefaults, HasSmartInteract, NumDust, MouseOver | 方块；登记类型级静态数据；处理帧、特效或自定义绘制；处理商店、聊天或交互；处理方块放置、导线或玩家交互 |
| `Content/Tiles/Furniture/ExampleDoorOpen.cs` | public ExampleDoorOpen : ModTile | SetStaticDefaults, HasSmartInteract, NumDust, MouseOver | 方块；登记类型级静态数据；处理帧、特效或自定义绘制；处理商店、聊天或交互；处理方块放置、导线或玩家交互 |
| `Content/Tiles/Furniture/ExampleDresser.cs` | public ExampleDresser : ModTile | SetStaticDefaults, DefaultContainerName, HasSmartInteract, ModifySmartInteractCoords, RightClick, MouseOverNearAndFarSharedLogic, MouseOverFar, MouseOver, NumDust, KillMultiTile, MapChestName | 方块；登记类型级静态数据；处理帧、特效或自定义绘制；处理商店、聊天或交互；处理方块放置、导线或玩家交互 |
| `Content/Tiles/Furniture/ExamplePlatform.cs` | public ExamplePlatform : ModTile | SetStaticDefaults, PostSetDefaults, NumDust | 方块；登记类型级静态数据；处理帧、特效或自定义绘制 |
| `Content/Tiles/Furniture/ExampleTable.cs` | public ExampleTable : ModTile | SetStaticDefaults, NumDust | 方块；登记类型级静态数据；处理帧、特效或自定义绘制 |
| `Content/Tiles/Furniture/ExampleToilet.cs` | public ExampleToilet : ModTile | SetStaticDefaults, NumDust, HasSmartInteract, ModifySittingTargetInfo, RightClick, MouseOver, HitWire | 方块；登记类型级静态数据；处理帧、特效或自定义绘制；处理商店、聊天或交互；处理伤害、命中或闪避；处理方块放置、导线或玩家交互 |
| `Content/Tiles/Furniture/ExampleWideBannerTile.cs` | public ExampleWideBannerTile : ModTile | SetStaticDefaults, PreDraw | 方块；登记类型级静态数据；处理帧、特效或自定义绘制 |
| `Content/Tiles/Furniture/ExampleWorkbench.cs` | public ExampleWorkbench : ModTile | SetStaticDefaults, NumDust | 方块；登记类型级静态数据；处理帧、特效或自定义绘制 |
| `Content/Tiles/Furniture/MinionBossRelic.cs` | public MinionBossRelic : ModTile; public MyBossRelic : MinionBossRelic | Load, SetStaticDefaults, CreateDust, SetDrawPositions, DrawEffects, SpecialDraw, PostDrawPlacementPreview | 方块；加载、注册或清理；登记类型级静态数据；处理帧、特效或自定义绘制 |
| `Content/Tiles/Furniture/MinionBossTrophy.cs` | public MinionBossTrophy : ModTile | SetStaticDefaults | 方块；登记类型级静态数据 |

### `Content/Tiles/Plants`（6 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Content/Tiles/Plants/ExampleCactus.cs` | public ExampleCactus : ModCactus | SetStaticDefaults, GetTexture, GetFruitTexture | 仙人掌；登记类型级静态数据 |
| `Content/Tiles/Plants/ExamplePalmTree.cs` | public ExamplePalmTree : ModPalmTree | SetStaticDefaults, GetTexture, SaplingGrowthType, GetOasisTopTextures, GetTopTextures, DropWood | 棕榈树；登记类型级静态数据；配置掉落规则 |
| `Content/Tiles/Plants/ExampleSapling.cs` | public ExampleSapling : ModTile | SetStaticDefaults, NumDust, RandomUpdate, SetSpriteEffects | 方块；登记类型级静态数据；处理帧、特效或自定义绘制 |
| `Content/Tiles/Plants/ExampleTree.cs` | public ExampleTree : ModTree | SetStaticDefaults, GetTexture, SaplingGrowthType, SetTreeFoliageSettings, GetBranchTextures, GetTopTextures, DropWood, Shake, TreeLeaf | 树；登记类型级静态数据；配置掉落规则 |
| `Content/Tiles/Plants/ExampleTreeLeaf.cs` | public ExampleTreeLeaf : ModGore | SetStaticDefaults | Gore/视觉碎片；登记类型级静态数据 |
| `Content/Tiles/Plants/ExampleVine.cs` | public ExampleVine : ModTile; public ExampleVineGlobalTile : GlobalTile; public TestVinesSystem : ModSystem | SetStaticDefaults, PreDraw, SetDrawPositions, SetSpriteEffects, GetItemDrops, RandomUpdate, TileFrame, PostUpdateWorld | 方块、系统/生命周期、全局方块修改；登记类型级静态数据；在更新 Hook 中驱动状态/AI；处理帧、特效或自定义绘制；配置掉落规则；处理方块放置、导线或玩家交互 |

### `Content/Walls`（4 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文职责与实现线索 |
| --- | --- | --- | --- |
| `Content/Walls/ExampleVanillaConversionWalls.cs` | public HallowedFossilWall : ModWall; public CorruptFossilWall : ModWall; public CrimsonFossilWall : ModWall; internal HallowedFossilWallItem : ModItem; internal CorruptFossilWallItem : ModItem; internal CrimsonFossilWallItem : ModItem | SetStaticDefaults, SetDefaults, AddRecipes | 物品、墙；登记类型级静态数据；设置实体/物品实例默认值；注册或调整配方 |
| `Content/Walls/ExampleWall.cs` | public ExampleWall : ModWall | SetStaticDefaults, NumDust | 墙；登记类型级静态数据；处理帧、特效或自定义绘制 |
| `Content/Walls/ExampleWallAdvanced.cs` | public ExampleWallAdvanced : ModWall | SetStaticDefaults, CreateDust, NumDust, AnimateWall, ModifyLight, WallFrame, CanBeTeleportedTo | 墙；登记类型级静态数据；处理帧、特效或自定义绘制 |
| `Content/Walls/ExampleWallUnsafe.cs` | public ExampleWallUnsafe : ModWall | SetStaticDefaults, NumDust | 墙；登记类型级静态数据；处理帧、特效或自定义绘制 |

## `Old/` 历史代码：不参与当前构建

这些文件保留旧算法、Boss、UI 与迁移参考，但包含过时类型和 API。只能学概念，不能按当前模板直接复制。

### `Old`（6 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文状态说明 |
| --- | --- | --- | --- |
| `Old/Angle.cs` | public Angle | Angle, Opposite, ClockwiseFrom, Between | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/ExampleAdvancedRecipe.cs` | public ExampleAdvancedRecipe : ModRecipe; public AdvancedRecipeItem : ModItem | ExampleAdvancedRecipe, RecipeAvailable, OnCraft, SetStaticDefaults, SetDefaults, AddRecipes | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/ExampleConfig.cs` | public ExampleConfigServer : ModConfig; public ExampleConfigClient : ModConfig | OnChanged | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/ExampleMod.cs` | public partial ExampleMod : Mod; internal ExampleModMessageType : byte | Load, Unload, UpdateMusic, ModifySunLightColor, ModifyTransformMatrix, UpdateUI, ModifyInterfaceLayers, NoInvasion, NoBiome, NoZoneAllowWater, NoZone, NormalSpawn, NoZoneNormalSpawn, NoZoneNormalSpawnAllowWater, NoBiomeNormalSpawn, HandlePacket | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/ExamplePlayer.cs` | public ExamplePlayer : ModPlayer | ResetEffects, OnEnterWorld, clientClone, SyncPlayer, SendClientChanges, UpdateDead, Save, Load, SetupStartInventory, UpdateBiomeVisuals, UpdateBadLifeRegen, PreUpdateBuffs, PuritySpiritDebuff, PostUpdateBuffs, PostUpdateEquips, PostUpdateMiscEffects, FrameEffects, PreHurt, Hurt, PreKill, UseTimeMultiplier, OnConsumeMana, AnglerQuestReward, GetFishingLevel, GetDyeTraderReward, DrawEffects, ModifyNurseHeal, PostBuyItem, PostSellItem | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/ExampleWorld.cs` | public ExampleWorld : ModWorld | Initialize, Save, Load, LoadLegacy, NetSend, NetReceive, ModifyWorldGenTasks, PlaceWell, PostWorldGen, ResetNearbyTileEffects, TileCountsAvailable, PreUpdate, PostUpdate, PostDrawTiles, DrawBorderedRect | 旧版实现，仅供算法与迁移参考；不参与当前编译 |

### `Old/Buffs`（7 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文状态说明 |
| --- | --- | --- | --- |
| `Old/Buffs/HeroOne.cs` | public HeroOne : ModBuff | SetDefaults | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Buffs/HeroThree.cs` | public HeroThree : ModBuff | SetDefaults | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Buffs/HeroTwo.cs` | public HeroTwo : ModBuff | SetDefaults | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Buffs/Nullified.cs` | public Nullified : ModBuff | SetDefaults, Update | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Buffs/PurityWisp.cs` | public PurityWisp : ModBuff | SetDefaults, Update | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Buffs/Undead.cs` | public Undead : ModBuff | SetDefaults, Update | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Buffs/Undead2.cs` | public Undead2 : ModBuff | SetDefaults, Update, ReApply | 旧版实现，仅供算法与迁移参考；不参与当前编译 |

### `Old/Commands`（5 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文状态说明 |
| --- | --- | --- | --- |
| `Old/Commands/LagCommand.cs` | public LagCommand : ModCommand | Action | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Commands/NpcTypeCommand.cs` | public NpcTypeCommand : ModCommand | Action | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Commands/ScoreCommand.cs` | public ScoreCommand : ModCommand | Action | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Commands/SoundCommand.cs` | public SoundCommand : ModCommand | Action | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Commands/VolcanoCommand.cs` | internal VolcanoCommand : ModCommand | Action | 旧版实现，仅供算法与迁移参考；不参与当前编译 |

### `Old/Dusts`（9 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文状态说明 |
| --- | --- | --- | --- |
| `Old/Dusts/EtherealFlame.cs` | public EtherealFlame : ModDust | OnSpawn, MidUpdate, GetAlpha | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Dusts/ExampleWaterSplash.cs` | public ExampleWaterSplash : ModDust | SetDefaults, OnSpawn | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Dusts/Flame.cs` | public Flame : ModDust | OnSpawn, Update | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Dusts/Negative.cs` | public Negative : ModDust | OnSpawn | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Dusts/Pixel.cs` | public Pixel : ModDust | OnSpawn, Update | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Dusts/PixelHurt.cs` | public PixelHurt : ModDust | Autoload, OnSpawn, Update | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Dusts/PuriumFlame.cs` | public PuriumFlame : ModDust | OnSpawn, Update | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Dusts/Smoke.cs` | public Smoke : ModDust | OnSpawn, Update | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Dusts/SpectreDust.cs` | public SpectreDust : ModDust | OnSpawn, Update | 旧版实现，仅供算法与迁移参考；不参与当前编译 |

### `Old/Items`（11 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文状态说明 |
| --- | --- | --- | --- |
| `Old/Items/CopperShortsword.cs` | public CopperShortsword : GlobalItem | SetDefaults | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Items/EquipMaterial.cs` | public EquipMaterial : ExampleItem | SetStaticDefaults, AddRecipes, CanBurnInLava | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Items/ExampleDrawTooltips.cs` | internal ExampleDrawTooltips : ModItem | SetStaticDefaults, SetDefaults, PreDrawTooltip, PreDrawTooltipLine, AddRecipes | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Items/ExplorerBag.cs` | public ExplorerBag : ModItem | SetStaticDefaults, SetDefaults, CanRightClick, RightClick, AddRecipes | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Items/Fertilizer.cs` | public Fertilizer : ModItem | SetStaticDefaults, SetDefaults, CanUseItem, UseItem, AddRecipes | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Items/GlobalPotion.cs` | public GlobalPotion : GlobalItem | UseItem | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Items/Infinity.cs` | public Infinity : ModItem; public InfinityGlobalItem : GlobalItem | SetStaticDefaults, SetDefaults, UpdateAccessory, GetAlpha, PreDrawInWorld, PreDrawInInventory, ConsumeItem, ConsumeAmmo, OnMissingMana | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Items/PrefixChanceGlobalItem.cs` | public PrefixChanceGlobalItem : GlobalItem | PrefixChance | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Items/PurityShield.cs` | public PurityShield : ModItem | SetStaticDefaults, SetDefaults | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Items/PuritySpiritBag.cs` | public PuritySpiritBag : ModItem | SetStaticDefaults, SetDefaults, CanRightClick, OpenBossBag | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Items/SparklingSphere.cs` | public SparklingSphere : ModItem | SetStaticDefaults, SetDefaults, HoldStyle, HoldItemFrame, HoldItem, AddRecipes | 旧版实现，仅供算法与迁移参考；不参与当前编译 |

### `Old/Items/Abomination`（7 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文状态说明 |
| --- | --- | --- | --- |
| `Old/Items/Abomination/AbominationBag.cs` | public AbominationBag : ModItem | SetStaticDefaults, SetDefaults, CanRightClick, OpenBossBag | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Items/Abomination/Bubble.cs` | public Bubble : ModItem | SetDefaults | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Items/Abomination/ElementResidue.cs` | public ElementResidue : ModItem | SetStaticDefaults, SetDefaults | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Items/Abomination/FoulOrb.cs` | public FoulOrb : ModItem | SetStaticDefaults, SetDefaults, CanUseItem, UseItem, AddRecipes | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Items/Abomination/Icicle.cs` | public Icicle : ModItem | SetDefaults | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Items/Abomination/ScytheBlade.cs` | public ScytheBlade : ModItem | SetDefaults | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Items/Abomination/SixColorShield.cs` | public SixColorShield : ModItem; public AnkhShield : GlobalItem | SetStaticDefaults, SetDefaults, UpdateAccessory, GetAlpha, CanEquipAccessory | 旧版实现，仅供算法与迁移参考；不参与当前编译 |

### `Old/Items/Accessories`（1 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文状态说明 |
| --- | --- | --- | --- |
| `Old/Items/Accessories/ManaHeart.cs` | public ManaHeart : ModItem | SetStaticDefaults, SetDefaults, UpdateAccessory, ChoosePrefix, AddRecipes | 旧版实现，仅供算法与迁移参考；不参与当前编译 |

### `Old/Items/Armor`（3 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文状态说明 |
| --- | --- | --- | --- |
| `Old/Items/Armor/AbominationMask.cs` | public AbominationMask : ModItem | SetDefaults, DrawHead | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Items/Armor/BunnyMask.cs` | public BunnyMask : ModItem | SetDefaults, DrawHead | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Items/Armor/PuritySpiritMask.cs` | public PuritySpiritMask : ModItem | SetStaticDefaults, SetDefaults, DrawArmorColor | 旧版实现，仅供算法与迁移参考；不参与当前编译 |

### `Old/Items/Placeable`（6 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文状态说明 |
| --- | --- | --- | --- |
| `Old/Items/Placeable/AbominationTrophy.cs` | public AbominationTrophy : ModItem | SetDefaults | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Items/Placeable/BunnyTrophy.cs` | public BunnyTrophy : ModItem | SetDefaults | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Items/Placeable/PuritySpiritTrophy.cs` | public PuritySpiritTrophy : ModItem | SetStaticDefaults, SetDefaults | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Items/Placeable/ScoreBoard.cs` | internal ScoreBoard : ModItem | SetStaticDefaults, SetDefaults | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Items/Placeable/TreeTrophy.cs` | public TreeTrophy : ModItem | SetDefaults | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Items/Placeable/VoidMonolith.cs` | public VoidMonolith : ModItem | SetDefaults, AddRecipes | 旧版实现，仅供算法与迁移参考；不参与当前编译 |

### `Old/Items/Weapons`（5 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文状态说明 |
| --- | --- | --- | --- |
| `Old/Items/Weapons/ExampleCloneItem.cs` | public ExampleCloneItem : ModItem | SetStaticDefaults, SetDefaults, Shoot, AddRecipes | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Items/Weapons/ExampleDualUseWeapon.cs` | public ExampleDualUseWeapon : ModItem | SetStaticDefaults, SetDefaults, AddRecipes, AltFunctionUse, CanUseItem, OnHitNPC, MeleeEffects, Shoot | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Items/Weapons/ExampleLaserWeapon.cs` | public ExampleLaserWeapon : ModItem | SetStaticDefaults, SetDefaults, AddRecipes | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Items/Weapons/ExampleMagicMissile.cs` | public ExampleMagicMissile : ModItem | SetStaticDefaults, SetDefaults, ModifyManaCost, AddRecipes | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Items/Weapons/PurityTotem.cs` | public PurityTotem : ModItem | SetStaticDefaults, SetDefaults, Shoot | 旧版实现，仅供算法与迁移参考；不参与当前编译 |

### `Old/NPCs`（9 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文状态说明 |
| --- | --- | --- | --- |
| `Old/NPCs/DeathAnimation.cs` | public DeathAnimation : ModNPC | SetStaticDefaults, SetDefaults, SpawnChance, PreDraw, PostDraw, CheckDead, FindFrame, AI | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/NPCs/ExampleChestSummon.cs` | public ExampleChestSummon : ModPlayer | PreUpdateBuffs, UpdateAutopause, ChestItemSummonCheck | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/NPCs/ExampleGlobalNPC.cs` | public ExampleGlobalNPC : GlobalNPC | ResetEffects, UpdateLifeRegen, NPCLoot, DrawEffects, EditSpawnRate, GetChat, PreChatButtonClicked | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/NPCs/ExampleTravelingMerchant.cs` | internal ExampleTravelingMerchant : ModNPC | FindNPC, UpdateTravelingMerchant, GetRandomSpawnTime, CreateNewShop, SetStaticDefaults, SetDefaults, Save, Load, HitEffect, CanTownNPCSpawn, TownNPCName, GetChat, SetChatButtons, OnChatButtonClicked, SetupShop, AI, NPCLoot, TownNPCAttackStrength, TownNPCAttackCooldown, TownNPCAttackProj, TownNPCAttackProjSpeed | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/NPCs/FallenSoul.cs` | public FallenSoul : Hover; public PurificationPowder : GlobalProjectile | FallenSoul, SetStaticDefaults, SetDefaults, CanBeHitByItem, CanBeHitByProjectile, HitEffect, CanChat, GetChat, SetChatButtons, OnChatButtonClicked, DrawHealthBar, CustomBehavior, ShouldMove, PostAI | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/NPCs/Fish.cs` | public abstract Fish : ModNPC | AI, FindFrame | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/NPCs/Hover.cs` | public abstract Hover : ModNPC | AI, CustomBehavior, ShouldMove | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/NPCs/Octopus.cs` | public Octopus : Fish | Octopus, SetStaticDefaults, SetDefaults, AI, FindFrame, HitEffect, SpawnChance | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/NPCs/Sarcophagus.cs` | public Sarcophagus : Hover | Sarcophagus, SetStaticDefaults, SetDefaults, CustomBehavior, ShouldMove, FindFrame, NPCLoot, OnHitPlayer, PostDraw, SpawnChance | 旧版实现，仅供算法与迁移参考；不参与当前编译 |

### `Old/NPCs/Abomination`（5 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文状态说明 |
| --- | --- | --- | --- |
| `Old/NPCs/Abomination/Abomination.cs` | public Abomination : ModNPC | SetStaticDefaults, SetDefaults, ScaleExpertStats, AI, SendExtraAI, ReceiveExtraAI, FindFrame, HitEffect, PreNPCLoot, OnHitPlayer, ModifyHitByItem, ModifyHitByProjectile, StrikeNPC, PreDraw, DrawHealthBar | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/NPCs/Abomination/AbominationRun.cs` | public AbominationRun : ModNPC | SetStaticDefaults, SetDefaults, ScaleExpertStats, AI, OnHitPlayer | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/NPCs/Abomination/CaptiveElement.cs` | public CaptiveElement : ModNPC | Autoload, SetStaticDefaults, SetDefaults, ScaleExpertStats, AI, SetPosition, FindFrame, CanHitPlayer, OnHitPlayer, GetDebuff, GetDebuffTime, GetColor, BossHeadSlot, PreDraw | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/NPCs/Abomination/CaptiveElement2.cs` | public CaptiveElement2 : ModNPC | Autoload, SetStaticDefaults, SetDefaults, ScaleExpertStats, AI, FindFrame, HitEffect, PreNPCLoot, NPCLoot, BossLoot, CanHitPlayer, OnHitPlayer, GetDebuff, GetDebuffTime, GetColor, BossHeadSlot, DrawHealthBar | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/NPCs/Abomination/FreedElement.cs` | public FreedElement : ModNPC | SetStaticDefaults, SetDefaults, ScaleExpertStats, AI, PreNPCLoot, CanHitPlayer, OnHitPlayer, GetDebuff, GetDebuffTime, GetColor | 旧版实现，仅供算法与迁移参考；不参与当前编译 |

### `Old/NPCs/PuritySpirit`（4 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文状态说明 |
| --- | --- | --- | --- |
| `Old/NPCs/PuritySpirit/PurityShield.cs` | public PurityShield : ModNPC | SetStaticDefaults, SetDefaults, ScaleExpertStats, AI, FindFrame, HitEffect, CanBeHitByItem, CanBeHitByProjectile, PreDraw, PostDraw | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/NPCs/PuritySpirit/PuritySpirit.cs` | public PuritySpirit : ModNPC; internal Particle; internal PuritySpiritMessageType : byte | SetStaticDefaults, SetDefaults, ScaleExpertStats, AI, FindPlayers, RunAway, Initialize, CheckDead, FinishFight1, FinishFight2, NPCLoot, BossLoot, CanBeHitByItem, ModifyHitByItem, OnHitByItem, CanBeHitByProjectile, ModifyHitByProjectile, OnHitByProjectile, StrikeNPC, PreDraw, PostDraw, DrawHealthBar, HandlePacket, Particle, Update | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/NPCs/PuritySpirit/PuritySpiritScreenShaderData.cs` | public PuritySpiritScreenShaderData : ScreenShaderData | PuritySpiritScreenShaderData, Apply | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/NPCs/PuritySpirit/PuritySpiritSky.cs` | public PuritySpiritSky : CustomSky | Update, Draw, GetCloudAlpha, Activate, Deactivate, Reset, IsActive | 旧版实现，仅供算法与迁移参考；不参与当前编译 |

### `Old/Projectiles`（12 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文状态说明 |
| --- | --- | --- | --- |
| `Old/Projectiles/ElementBall.cs` | public ElementBall : ModProjectile | SetStaticDefaults, SetDefaults, AI, PlaySound, CreateDust, OnHitPlayer, GetName, GetColor | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Projectiles/ElementLaser.cs` | public ElementLaser : ModProjectile | SetStaticDefaults, SetDefaults, AI, OnHitPlayer, Colliding, GetName, GetColor, GetDebuff, GetDebuffTime, PreDraw | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Projectiles/ElementShield.cs` | public ElementShield : ModProjectile | SetStaticDefaults, SetDefaults, AI, OnHitNPC, OnHitPvp, GetAlpha, GetName, LightColor, GetDebuff, GetDebuffTime | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Projectiles/ExampleBehindTilesProjectile.cs` | public ExampleBehindTilesProjectile : ModProjectile; public ExampleBehindTilesProjectileItem : ModItem | SetStaticDefaults, SetDefaults, DrawBehind, AddRecipes | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Projectiles/ExampleCloneProjectile.cs` | public ExampleCloneProjectile : ModProjectile | SetStaticDefaults, SetDefaults, PreKill, OnTileCollide | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Projectiles/ExampleLaser.cs` | public ExampleLaser : ModProjectile | SetDefaults, PreDraw, DrawLaser, Colliding, OnHitNPC, AI, ShouldUpdatePosition, CutTiles | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Projectiles/HealProj.cs` | public HealProj : GlobalProjectile | PreAI | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Projectiles/MagicMissile.cs` | public MagicMissile : ModProjectile | SetDefaults, GetAlpha, AI, Kill | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Projectiles/OctopusArm.cs` | public OctopusArm : ModProjectile | SetDefaults, AI, SendExtraAI, ReceiveExtraAI, Colliding, ModifyHitPlayer, PreDraw, PostDraw | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Projectiles/PixelBall.cs` | public PixelBall : ElementBall | SetStaticDefaults, CreateDust, PlaySound, GetName | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Projectiles/ScorePoint.cs` | internal ScorePoint : ModProjectile | SetDefaults, AI | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Projectiles/ShadowArm.cs` | public ShadowArm : ModProjectile | SetStaticDefaults, SetDefaults, AI, Add, Remove, Colliding, CreateDust, PostDraw | 旧版实现，仅供算法与迁移参考；不参与当前编译 |

### `Old/Projectiles/Minions`（4 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文状态说明 |
| --- | --- | --- | --- |
| `Old/Projectiles/Minions/HoverShooter.cs` | public abstract HoverShooter : Minion | CreateDust, SelectFrame, Behavior, TileCollideStyle | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Projectiles/Minions/Minion.cs` | public abstract Minion : ModProjectile | AI, CheckActive, Behavior | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Projectiles/Minions/PurityBolt.cs` | public PurityBolt : ModProjectile | SetStaticDefaults, SetDefaults, AI, OnTileCollide | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Projectiles/Minions/PurityWisp.cs` | public PurityWisp : HoverShooter | SetStaticDefaults, SetDefaults, CheckActive, CreateDust, SelectFrame | 旧版实现，仅供算法与迁移参考；不参与当前编译 |

### `Old/Projectiles/PuritySpirit`（7 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文状态说明 |
| --- | --- | --- | --- |
| `Old/Projectiles/PuritySpirit/NegativeWall.cs` | public NegativeWall : ModProjectile | SetDefaults, AI, PreDraw | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Projectiles/PuritySpirit/NullLaser.cs` | public NullLaser : ModProjectile | SetStaticDefaults, SetDefaults, SendExtraAI, ReceiveExtraAI, AI, ModifyHitPlayer, Colliding, PreDraw | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Projectiles/PuritySpirit/PureCrystal.cs` | public PureCrystal : ModProjectile | SetStaticDefaults, SetDefaults, SendExtraAI, ReceiveExtraAI, AI, OnHitPlayer, GetAlpha, PostDraw | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Projectiles/PuritySpirit/PurityBeam.cs` | public PurityBeam : ModProjectile | SetStaticDefaults, SetDefaults, AI, ModifyHitPlayer, PreDraw | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Projectiles/PuritySpirit/PuritySnake.cs` | public PuritySnake : ModProjectile | SetStaticDefaults, SetDefaults, AI, ModifyHitPlayer, Colliding, CreateDust | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Projectiles/PuritySpirit/PuritySphere.cs` | public PuritySphere : ModProjectile | SetStaticDefaults, SetDefaults, SendExtraAI, ReceiveExtraAI, AI, GetAlpha, PreDraw | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Projectiles/PuritySpirit/VoidWorld.cs` | public VoidWorld : ModProjectile | SetStaticDefaults, SetDefaults, SendExtraAI, ReceiveExtraAI, AI, ModifyHitPlayer, Colliding, PreDraw | 旧版实现，仅供算法与迁移参考；不参与当前编译 |

### `Old/Sounds/Custom`（1 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文状态说明 |
| --- | --- | --- | --- |
| `Old/Sounds/Custom/WatchOut.cs` | public WatchOut : ModSound | PlaySound | 旧版实现，仅供算法与迁移参考；不参与当前编译 |

### `Old/Sounds/Item`（1 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文状态说明 |
| --- | --- | --- | --- |
| `Old/Sounds/Item/Wooo.cs` | public Wooo : ModSound | PlaySound | 旧版实现，仅供算法与迁移参考；不参与当前编译 |

### `Old/Tiles`（7 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文状态说明 |
| --- | --- | --- | --- |
| `Old/Tiles/AnimatedLoom.cs` | public AnimatedLoom : GlobalTile | AnimateTile | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Tiles/BossTrophy.cs` | public BossTrophy : ModTile | SetDefaults, KillMultiTile | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Tiles/ExampleGlobalTile.cs` | internal sealed ExampleGlobalTile : GlobalTile | Drop | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Tiles/ExampleSapling.cs` | public ExampleSapling : ModTile | SetDefaults, NumDust, RandomUpdate, SetSpriteEffects | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Tiles/Minesweeper.cs` | public Minesweeper : ModTile; public MinesweeperItem : ModItem | SetDefaults, Dangersense, PlaceInWorld, Slope, TileFrame | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Tiles/TEScoreBoard.cs` | public ScoreBoardGlobalNPC : GlobalNPC; public TEScoreBoard : ModTileEntity; public ScoreBoard : ModTile | NPCLoot, GetPlayArea, Update, NetReceive, NetSend, Save, Load, ValidTile, Hook_AfterPlacement, SetDefaults, KillMultiTile, NewRightClick, MouseOver, MouseOverFar, MouseOverBoth | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/Tiles/VoidSky.cs` | public VoidSky : CustomSky | OnLoad, Update, OnTileColor, Draw, GetCloudAlpha, Activate, Deactivate, Reset, IsActive | 旧版实现，仅供算法与迁移参考；不参与当前编译 |

### `Old/UI`（2 个文件）

| 文件 | 声明的类型与基类/接口 | 主要方法/Hook | 中文状态说明 |
| --- | --- | --- | --- |
| `Old/UI/ExamplePersonUI.cs` | internal ExamplePersonUI : UIState | OnInitialize, OnDeactivate, Update, DrawSelf | 旧版实现，仅供算法与迁移参考；不参与当前编译 |
| `Old/UI/VanillaItemSlotWrapper.cs` | internal VanillaItemSlotWrapper : UIElement | VanillaItemSlotWrapper, DrawSelf | 旧版实现，仅供算法与迁移参考；不参与当前编译 |

## 怎样使用这个索引

1. 按需求找基类，例如武器先找 `ModItem`，弹幕行为再找 `ModProjectile`。
2. 在“主要方法/Hook”中找最接近的生命周期，例如 `ModifyShootStats`、`AI`、`SaveData`。
3. 打开源码读字段、条件和网络分支；中文实现线索是导航，不代替方法体。
4. 回到 stable API 核对签名，再让 IDE 生成 override。
5. 若行位于 `Old/`，只提取算法，并用当前 API 重写。


